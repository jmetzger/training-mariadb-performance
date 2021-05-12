# pt-online-schema-change 

## Requirements 

  * Install percona-toolkit 

## Documentation 

  * https://www.percona.com/doc/percona-toolkit/3.0/pt-online-schema-change.html

## What does it do ?

```
# Altering table without blocking them 
# Do a dry-run beforehand 
pt-online-schema-change --alter "ADD INDEX idx_city (city)" --dry-run D=contributions,t=donors
# 
pt-online-schema-change --alter "ADD INDEX idx_city (city)" --execute D=contributions,t=donors


```
