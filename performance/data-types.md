# Data Types (also for joins) 


````
===== Part 3: Optimize Schema and Data Types =====

==== Basics ====

  * Smaller is better 
    * but: do not underestimate the range 
  * Simple is good 
  * Avoid NULL (if possible) 

=== Smaller is usually better ===

  * Smaller data types are usually faster
      * because they use less space 
        * on disk
        * in memory
        * in the CPU cache 
      * they need less CPU cycles to process
     
=== Do not underestimate the range ===

  * Choose the smallest data type \\ you think you will not exceed
  * because increasing the data type range in your schema later \\ can be painful and time consuming


=== Simple is good ===
  
  * e.g. integers are cheaper to compare than characters
    * because character sets and collation (sorting rules) \\ make character comparisons complicated
  * Example dates / ip's 
    * you should store dates and times in MYSQL's built-in types instead of strings
    * you should integers for IP addresses

=== Avoid NULL (if possible) === 

  * Best: Specify columns as NOT NULL 
    * unless you intend to store NULL (the absence of a value) in them 
  * Why ?
    * Harder for MySQL to optimize queries that refer to nullable columns 
      * they make indexes, index statistics and value comparisons more complicated
  * Performance improvement between NULL and NOT NULL is small 
    * make it no priority to change it on an existing schema
  * BUT: When you plan to index column 
    * THEN: NOT NULL please 
 
==== Alias Data Types do not decrease performance ====
  
  * There are some aliases for other data types around 
    * e.g. 
      * INTEGER, BOOL, NUMERIC
  * The use of these instead of the original data type
    * does not decrease performance 

==== INT(1) - 1 is not the length of the data type ====

  * INT(1) and INT(16) might be confusing
    * They are the same datatype with the same length 
    * 1 or 16 - specifies the number of characters in
      * MySQL's interactive tools (e.g. mysql - client) 


==== Real Numbers ====

=== exact / inexact types ===

  * FLOAT, DOUBLE 
    * approximate calculations with standard floating-point math 
  * DECIMAL type 
    * exact numbers (since MySQL 5.0)
  * Exact is done by SERVER not CPU (because CPU does not support it) 
  * Floating point is significantly faster
    * because the CPU performs it natively 

=== DECIMAL ===

  * in MySQL 5.0+: 65 digits 
  * DECIMAL uses more space for storing data (than FLOAT)
  * Use it only, when you really need exact results for fractional numbers
    * e.g. financial data 
  * Alternative: BIGINT 

==== Strings ====

=== VARCHAR ===

  * VARCHAR uses 1 or 2 extra bytes to record the value length 
    * 1 byte if the columns' maximum length is 255 bytes 
    * 2 bytes it it is more 
  * VARCHAR helps performance because it saves space 
  * Use VARCHAR when the maximum length is much larger than the average length 
    * + when updates to the fields are rare  \\ so fragmentation is not a problem.       
 
=== CHAR ===

  * Can use less space then VARCHAR 
    * because it only uses the space it needs   
  * Use if:
    * for storing very short strings 
    * all values are nearly the same length 
    * Data is changed frequently (no problems with defragmentation)
  * Example:
    * sha256 - values for user passwords (always the same length)

=== BLOB / TEXT ===

== Sorting ==

  * MySQL sorts BLOB and TEXT columns differently from other types 
  * Does not sort by full length 
    * only sorts the first (Variable:) max_sort_length bytes of such columns 
  * If you only want to sort by the first few characters, you can:
    * decrease the max_sort_length server variable 
    * or use:
    * ORDER BY SUBSTRING(column,length) 
  * MySQL can't index the full length of these data types \\ and can't use the indexes for sorting

== ON-DISK temporary tables and sort files (I) ==

  * the memory storage engine does not support BLOB and TEXT - Types 
  * Queries that use BLOB and TEXT and need an implicit temporary table 
    * have to use on-disk temporary tables even for a few rows
  * Result: 
    * Performance Overhead 
  * BEST SOLUTION:
    * Avoid using BLOB and TEXT-types (unless you really need them)
    * or: MySQL 8: https://mysqlserverteam.com/mysql-8-0-support-for-blobs-in-temptable-engine/
    * if you can't avoid them 
      * SUBSTRING(column,length) for every BLOB - column 
  * How to find out (in mysql - session) ? 
      * Step 1: Explain: Result -> using temporary, filesort
        * What does "filesort" mean: https://www.percona.com/blog/2009/03/05/what-does-using-filesort-mean-in-mysql/ 
      * Step 2: flush status  
      * Step 3: show status like 'created_tmp_disk_tables%'
      * Step 4: Execute query without Explain
      * Step 5: show status like 'created_tmp_disk_tables%'
        * See -> If created_tmp_disk_tables% increased     

== ON-DISK temporary tables and sort files (II) ==
 
  * Nice walkthrough: https://www.fromdual.com/avoid-temporay-disk-tables-with-mysql

=== ENUM (instead of string) ===

  * Advantage:
    * Really compact in saving space
  * Downside: 
    * Expensive, when new values are added often 
      * ALTER operation   



==== Data Types for Joins (I) ====

  * Keys should be of the same type and length (range) 
  * They should be exactly the same type (including signed/unsigned)
  * No good idea to join data of type string (overhead) 
    * alternative
      * lookup tables with primary keys instead 
  * no varchar/no enum/set please 
    * e.g. enum internally uses 
  * mixing data types can cause performance problems  

==== Data Types for Joins (II) ====

  * Integer Types 
    * Best choice for identifiers, because they're fast and they work with AUTO_INCREMENT
  * ENUM and SET 
    * Poor choice for identifiers 
  * String Types 
    * Avoid string types for identifiers if possible 
    * They can take a log of space 
    * They are generally slower than integer types 
    * Be cautious when using string identifiers with MyISAM tables 
      * MyISAM uses packed indexes for strings(by defaults) \\ which can make lookups much slower
      * Up to 6x worse performance 
  * Random strings
    * Be careful with them (MD5(),SHA1(),UUID())
    * Each new value will be distributed over a large space 
    * Result: 
      * INSERT slow 
        * Insert has to go into random location in indexes 
          * Results are page splits, random disk access, clustered index fragmentation \\ (for clustered storage engines)
      * SELECT (some types) slow 
        * logical neightboured rows will be widely spread on disk and in memory   
      * All data is equally hot (no advantage of having any particular data cached)      
  
==== Autogenerated Schemas ====

  * Beware of autogenerated schemas 
  * they are less than optimal 
  * they do not respect the advantages/disadvantages of mysql, when it comes to performance 

==== Design Gotchas ==== 

=== Too many columns (situation) ===

  * MySQL storage engine does:
    * copy rows between the server and the storage engine 
      * in a row buffer format. 
      * The server then decodes the buffer into columns.
  * But it can be costly to turn the row buffer \\ into the row data structure with the decoded columns.
  * MyISAM fixed row format matches the server's row format exactly
    * no conversion is needed.
  * MyISAM variable row format and InnoDB row format
    * always requires conversion 
    * The cost of the conversion depends on the number of columns 
    * We talk about hundred of columns here.
    
=== Too many columns (advice) ===

  * Only have the columns in the structure that you really need 

=== Too many joins (situation) ===
  
  * EAV (entity-attribute-value) - design pattern 
    * does not work well in MYSQL 
  * MySQL: limitation of 61 tables per join 
  
=== Too many joins (advice) ===

  * 12 or fewer tables per query
    * if you want queries to execute fast and with high concurrency 

=== Beware of overusing ENUM ===

  * Sometimes it is just an integer, that should be foreign_keyed to a lookup/dictionary table 

=== NULL - please not ===

  * Consider alternatives when possible 
  * Also, if you need to store a "no value" fact \\ in a table, you might not need to use NULL
    * Perhaps you can use zero, a special value, or an empty string instead.      

```
