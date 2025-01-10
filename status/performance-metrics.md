# Performance metrics in Status 

```
# Description: Number of joins which used a full scan of the first table.
# ->
Select_scan 

# No index at all 
Select_full_join

# Using index scan - 2nd worst
Select_full_range_join

#
Select_range_check
```
