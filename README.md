# MariaDB Performance Training (deutsch)   

## Agenda 

  1. Performance / Theorie - Aspekte der MariaDB - Architektur 
     * [Architektur Server (Schritte)](performance/mysql-server-architecture.md)
     * [CPU oder io-Last klären](top-cpu-io-load.md)
     * [Storage Engines](storage-engines.md) 
     * [InnoDB - Struktur](/innodb/innodb-structure.md)
     * [InnoDB - Optimierung](/innodb/innodb.md)
     * [InnoDB - innodb_log_file_size berechnen](innodb/calculate-innodb-logfile-size.md)
     * [Query - Cache](/performance/query-cache.md)
     * [3-Phasen-Datengröße](3-phases-of-data-size-and-performance-impact.md)
  1. Installation
     * [Installation (Rocky/Redhat) - 10.6](installation-rocky.md)
     * [Open Mariadb to the outside world - port and firewall](installation/listening-where.md)
  1. Konfiguration 
     * [Slow query log](slow-query-log.md) 
  1. Administration 
     * [Standard storage engine bestimmen](default-storage-engine.md)
     * [Show status](show-status.md)
     * [Server System Variablen - show variables](show-variables.md)
     * [systemctl/jorunalctl - Server starten,stoppen/Logs](systemctl-journalctl.md) 
     * [User verwalten](user.md)
  1. Joins
     * [Joins - Overview](overview/joins.md)
  1. Performance und Optimierung von SQL-Statements 
     * [Explain verwenden](/indexes/explain.md)
     * [Do not use '*' whenever possible](/performance/select-no-star-please.md) 
     * [Indexes](indexes/index.md)
     * [profiling-get-time-for-execution-of.query](/indexes/profiling.md)
     * [Kein function in where verwenden](/performance/no-function-in-where.md)
     * [Optimizer-hints (and why you should not use them)](performance/optimizer-hints.md)
     * [Query-Plans aka Explains](performance/query-plans.md)
     * [Query Pläne und die Key-Länge](query-plans-explain-keylen.md)
     * [Index und Likes](indexes/like-index-not-index.md)
     * [Index und Joins](indexes/join-index.md)
     * [Find out cardinality without index](/indexes/cardinality.md)
     * [Index and Functions](index-and-functions.md)
     * [index and group by](indexes/groupby.md)
     * [forcing good index](/indexes/force-index.md)
     * [forcing bad index](indexes/force-wrong-index.md)
  1. Performance - Views
     * [Performance - Views](performance/views.md)
  1. Performance Schema
     * [Performance Schema - slow queries](performance_schema/find-slow-queries.md)
  1. Performance Metrics from status
     * [Performance Metrics from status](status/performance-metrics.md)
  1. Locks
     * [How does innodb implicit locking work](locks/innodb-implicit-locks.md)
     * [Exercise - identify deadlocks](locks/deadlocks.md)  
  1. Tools 
     * [Percona Toolkit](/tools/percona-toolkit.md) 
     * [pt-query-digest - analyze slow logs](/tools/pt-query-digest.md)
     * [pt-online-schema-change howto](/tools/pt-online-schema-change.md)
     * [Example sys-schema and Reference](/tools/sys.md)
  1. Beispieldaten
     * [Verleihdatenbank - sakila](sakila.md)
     * [Setup training data "contributions"](/indexes/setup-training-data-contributions.md)
  1. Managing big tables 
     * [Using Partitions - Walkthrough](partitions/partitions-explain.md)
  1. Replication
     * [Replikation mit GTID](https://www.admin-magazin.de/Das-Heft/2017/02/MySQL-Replikation-mit-GTIDs)
     * [Replikation Read/Write - Split: ](https://proxysql.com/blog/configure-read-write-split/)
  1. Fragen und Antworten 
     * [Fragen und Antworten](q-and-a.md)
  1. Projektarbeit/-optimierung 
     * [Praktisch Umsetzung in 3-Schritten](project-3-steps.md)
  1. Dokumentation (Performance) 
     * [MySQL - Performance - PDF](http://schulung.t3isp.de/documents/pdfs/mysql/mysql-performance.pdf)
     * [Effective MySQL](https://www.amazon.com/Effective-MySQL-Optimizing-Statements-Oracle/dp/0071782796)
     * [Analyze statt Explain](https://mariadb.com/kb/en/analyze-statement/)
  1. Dokumentation (Releases)
     * [Identify Long-Term Support Releases](https://mariadb.com/kb/en/mariadb-server-release-dates/)  
  1. Dokumentation (Server System Variables / Alter inplace)
     * [Server System Variables](https://mariadb.com/kb/en/server-system-variables/)
     * [Inplace Alter](https://mariadb.com/kb/en/innodb-online-ddl-operations-with-the-inplace-alter-algorithm/)
  1. Dokumentation (Indexes)
    * [Recipes for settings indexes](https://mariadb.com/kb/en/building-the-best-index-for-a-given-select/)
  1. Dokumenation (Virtual Columns / Persistentn)
     * [Persistent / Virtual Columns](https://mariadb.com/kb/en/generated-columns/)
  1. Backup/Restore
     * [Mariabackup](backup-restore/mariabackup.md)
        
     

