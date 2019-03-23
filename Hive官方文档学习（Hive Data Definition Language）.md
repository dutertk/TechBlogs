# Hive Data Definition Language

1. ## Create/Drop/Alter/Use Database

### Create Database

```mysql
CREATE (DATABASE|SCHEMA) [IF NOT EXISTS] database_name
[COMMENT database_comment]
[LOCATION hdfs_path]
[WITH DBPROPERTIES(property_name=property_value)];
```

**官网注释：schema和database是一样的（they mean the same thing）**

### Drop Database

```mysql
DROP (DATABASE|SCHEMA) [IF EXISTS] database_name [RESTRICT|CASCADE];
```

**官网注释：默认的模式是RESTRICT，即如果数据库不是空的，就不能删除该数据库。使用CASCADE可以强制删除非空数据库**

### Use Database

```mysql
use database_name;
use default;
select current_database();
```

**注：切换数据库以及显示当前正在使用的哪个数据库**

2. ## Create/Drop/Truncate Table

```mysql
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name
[(col_name data_type [COMMENT col_comment])]
[COMMENT table_comment]
[PARTITIONED BY (col_name data_type [COMMENT col_comment])]
[CLUSTERED BY (col_name, col_name)...[SORTED BY (col_name [ASC|DESC])] INTO num_buckets BUCKETS]
[SKEWED BY (col_name,col_name...)]
on (col_value,col_value...),(col_vlaue,col_value...),...)
[SORTED AS DIRECTORIES]
[
  [ROW FROMAT row_format]
  [STORED AS file_format]
]
[LOCATION hdfs_path]

CREATE [TEMPORARY][EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name
like existing_table_or_view_name
[LOCATION hdfs_path]

row_format
:DELIMITED [FIELDS TERMINATED BY CHAR[ESCAPED BY char]]
[MAP KEYS TERMINATED BY char]

constraint_specification:
:[,PRIMARY KEY (col_name,...) DISABLE NOVALIDATE] 
[, CONSTRAINT constraint_name FOREIGN KEY (col_name,...) REFERENCES table_name(col_name,...)]


```

**官网注释：**

- 表和列的注释使用单引号
- 管理（内部）表和外部表的不同：
  - 管理表数据由Hive自身管理，外部表由HDFS管理；
  - 管理部数据存储的位置是/user/hive/warehouse,外部表存储的数据位置由自己制定；
  - 删除管理表会直接删除元数据及存储数据；删除外部表仅会删除元数据，HDFS上的文件并不会被删除；
- Hive默认创建的是管理表

### Partitioned Tables

分区表：通过使用**PARTITIONED BY**来创建分区表。一个表可以有一个甚至多个分区，在HDFS中显示为数据的层级目录结构。也就是在系统上建立文件夹，把分类数据放在不同文件夹下，加快查询速度。

```mysql
CREATE TABLE page_view(viewTime INT, userid BIGINT,
     page_url STRING, referrer_url STRING,
     ip STRING COMMENT 'IP Address of the User')
 COMMENT 'This is the page view table'
 PARTITIONED BY(dt STRING, country STRING)
 ROW FORMAT DELIMITED
   FIELDS TERMINATED BY '\001'
STORED AS SEQUENCEFILE;
```





表和列的注释使用单引号

