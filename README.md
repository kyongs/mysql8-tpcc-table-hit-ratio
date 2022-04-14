# mysql8-tpcc-table-hit-ratio

This project modifies mysql8.0.27 code to get the information about each tpcc table's hit ratio by Innodb server status.

#### Fixed Files

```
Fixing TPCC table space id
> storage/innobase/srv/srv0srv.cc:553
> storage/innobase/include/srv0srv.h:684
> storage/innobase/fil/fil0fil.cc:2829
```
