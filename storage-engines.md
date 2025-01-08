# Storage Engines 

## Why ?

```
Let's you choose:
How your data is stored
```

## What ?

  * Performance, features and other characteristics you want

## Where ? 

  * Theoretically you can use a different engine for every table 
  * But: For performance optimization and future, it is better to concentrate on one 

## What do they do ?

  * In charge for: Responsible for storing and retrieving all data stored in MariaDB
  * Each storage engine has its:
    * Drawbacks and benefits
  * Server communicates with them through the storage engine API 
    * this interface hides differences
    * makes them largely transparent at query layer
    * api contains a couple of dozen low-level functions e.g. “begin a transaction”, “fetch the row that has this primary key”

## Storage Engine do not ....

  * Storage Engines do not parse SQL
  * Storage Engines do not communicate with each other

## They simply .....

  * They simply respond to requests from the server

## Which are the most important one ?

  * InnoDB (currently default engine) 
  * MyISAM/Aria
  * Memory
  * CSV
  * Blackhole (/dev/null)
  * Archive
  * Partition
  * (Federated/FederatedX)

## Comparison MyISAM vs. InnoDB  

### On Detail: MyISAM - Storage Engine

#### Features 

  * table locks 
  * Locks are done table-wide
  * no automatic data-recovery
  * you can loose more data on crashes than with e.g. InnoDB
  * no transactions
  * only indices are save in memory through MySQL
  * compact saving (data is saved really dense)
  * table scans are quick

### In Detail: InnoDB - Storage Engine

#### Features

  * support hot backups (because of transactions)
  * transactions are supported
  * foreign keys are supported
  * row-level locking
  * multi-versioning
  * indexes refer to the data through primary keys
  * indexes can quickly get huge in size
    * if size of primary index is not small

### Difference MyISAM / Aria 

  * Crash Recovery (only difference)

