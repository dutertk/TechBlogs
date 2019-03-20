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

**官网注释：默认的模式是**RESTRICT**，即如果数据库不是空的，就不能删除该数据库。使用CASCADE可以强制删除非空数据库**

### Use Database

```mysql
use database_name;
use default;
select current_database();
```

**注：切换数据库以及显示当前正在使用的哪个数据库**

2. ## Create/Drop/Truncate Table

