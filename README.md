# mysql8-tpcc-table-hit-ratio

## About

This project is to get the information about tpcc table's hit ratio.
<br/>

## Build/Installation

to detailed information, click here!🤚

```

```

<br/>

## Development Process

#### 1. Make the TPC-C table space ids to global variables.

(Every time when MySQL is initialized, table space ids changes, so we have to make tablespace ids to a variable to keep track on them.)<br/><br/>

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
tpcc_wh_disk_rd       // warehouse disk read counts (page was not in buffer)
tpcc_dist_disk_rd    // district disk read counts
tpcc_cust_disk_rd    // customer disk read counts
tpcc_stk_disk_rd     // stock disk read counts
tpcc_itm_disk_rd     // item disk read counts
tpcc_or_disk_rd      // orders disk read counts
tpcc_no_disk_rd      // new orders disk read counts
tpcc_ol_disk_rd      // order line disk read counts
tpcc_his_disk_rd     // history disk read counts

tpcc_wh_buf_rd       // warehouse buffer read counts (page was in buffer!)
tpcc_dist_buf_rd     // district buffer read counts
tpcc_cust_buf_rd     // customer buffer read counts
tpcc_stk_buf_rd      // stock buffer read counts
tpcc_itm_buf_rd      // item buffer read counts
tpcc_or_buf_rd       // orders buffer read counts
tpcc_no_buf_rd       // new orders buffer read counts
tpcc_ol_buf_rd       // order line buffer read counts
tpcc_his_buf_rd      // history buffer read counts

tpcc_total_rd            // total read request counts (sum of tpcc + system config + mysql database)
```

<br/><br/>

#### 2. Increase the corresponding read variables.

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
> storage/innobase/buf/buf0rea.cc:121
> storage/innobase/srv/buf0buf.cc:3507
```
