# mysql8-tpcc-table-hit-ratio

This project modifies mysql8.0.27 code to get the information about each tpcc table's hit ratio by Innodb server status.

#### 1. Make the TPC-C table space ids to global variables.

(Because when MySQL is initialized, table space id can be changed, we have to make to a variable to keep track on them.)<br/><br/>

Changed Files

```
> storage/innobase/srv/srv0srv.cc:553
> storage/innobase/include/srv0srv.h:708
> storage/innobase/fil/fil0fil.cc:2829
```

Variables

```c++
srv_ol_space_id     //order line table space id
srv_no_space_id     // new orders table space id
srv_stk_space_id    // stock table space id
srv_cust_space_id   // customer table space id
srv_or_space_id     // orders table space id
srv_dist_space_id   // district table space id
srv_wh_space_id     // warehouse table space id
srv_itm_space_id    // item table space id
srv_his_space_id    // history table space id
```

<br/><br/>

#### 2. Initialize the disk read variables, and the buffer read variables to print on InnoDB Status.

Changed Files

```
> storage/innobase/srv/srv0srv.cc:1543
> storage/innobase/srv/srv0srv.h:1165
> storage/innobase/srv/srv0srv.h:77
```

Variables

```c++
tpcc_warehouse_disk_reads   // warehouse disk read counts (page was not in buffer)
tpcc_district_disk_reads    // district disk read counts
tpcc_customer_disk_reads    // customer disk read counts
tpcc_stock_disk_reads       // stock disk read counts
tpcc_item_disk_reads        // item disk read counts
tpcc_orders_disk_reads      // orders disk read counts
tpcc_new_orders_disk_reads  // new orders disk read counts
tpcc_order_line_disk_reads  // order line disk read counts
tpcc_history_disk_reads     // history disk read counts

tpcc_warehouse_buf_reads    // warehouse buffer read counts (page was in buffer!)
tpcc_district_buf_reads     // district buffer read counts
tpcc_customer_buf_reads     // customer buffer read counts
tpcc_stock_buf_reads        // stock buffer read counts
tpcc_item_buf_reads         // item buffer read counts
tpcc_orders_buf_reads       // orders buffer read counts
tpcc_new_orders_buf_reads   // new orders buffer read counts
tpcc_order_line_buf_reads   // order line buffer read counts
tpcc_history_buf_reads      // history buffer read counts

tpcc_total_reads            // total read request counts (sum of tpcc + system config + mysql database)
```

<br/><br/>
