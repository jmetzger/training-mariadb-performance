# InnoDB Implicit Locks 

## How do the work in general 

  * Implicit locks are done by InnoDB itself 
  * We can only partly influence them. 
  
## Who wants what ? 

```
<who?, what?, how?, granted?>
```

## Explanation (a bit clumsy) 

  * IS and IX (intended share an intended write lock) 
  * IS and IX can be trigged on SQL
  * IX -> SUFFIX -> FOR UPDATE (this triggers a IX lock) 
  * IX and IS are the first step (on table layer) 
  * After that IX -> tries to get an write lock on row-level -> X 
  * Works unless there is another X 
  * IX and IS is not retrieved on TABLE spaced operations (construction --- alter) 

## Lock Type compability matrix 

```
    X           IX          S           IS
X   Conflict    Conflict    Conflict    Conflict
IX  Conflict    Compatible  Conflict    Compatible
S   Conflict    Conflict    Compatible  Compatible
IS  Conflict    Compatible  Compatible  Compatible
```


## The best explanation across the internet ;o) 

  * http://stackoverflow.com/questions/25903764/why-is-an-ix-lock-compatible-with-another-ix-lock-in-innodb|IX_and_IS-locks

```
Many people, both visitors and curators, enter the museum. 
The visitors want to view paintings, so they wear a badge labeled "IS". 
The curators may replace paintings, so they wear a badge labeled "IX". 
There can be many people in the museum at the same time, with both types of badges. 
They don't block each other.

During their visit, the serious art fans will get as close to the painting as they can, 
and study it for lengthy periods. 

They're happy to let other art fans stand next to them before the same painting. 
They therefore are doing SELECT ... LOCK IN SHARE MODE and they have "S" lock, 
because they at least don't want the painting to be replaced while they're studying it.

The curators can replace a painting, but they are courteous to the serious art fans, 
and they'll wait until these viewers are done and move on. 
So they are trying to do SELECT ... FOR UPDATE (or else simply UPDATE or DELETE). 
They will acquire "X" locks at this time, by hanging a little sign up saying "exhibit being redesigned." 
The serious art fans want to see the art presented in a proper manner, with nice lighting and some descriptive placque. 
They'll wait for the redesign to be done before they approach (they get a lock wait if they try).
```
