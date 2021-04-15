
### MySQL Commands

`$ mysql -u [username] -p;`

Connect to MySQL Server with a specified database using a username and password:
`$ mysql -u [username] -p [database];`

Exit mysql command-line client:
`$ exit`

Export data using mysqldump tool | Backup Database to SQL File
`$ mysqldump -u [username] -p [database] > data_backup.sql;`
`mysqldump -u Username -p dbNameYouWant > databasename_backup.sql`

Restore from backup SQL File
`$ mysql - u Username -p dbNameYouWant < databasename_backup.sql;`

To clear MySQL screen console window on Linux, you use the following command:
`$ mysql> system clear;`

Repair Tables After Unclean Shutdown
`$ mysqlcheck --all-databases; `
`$ mysqlcheck --all-databases --fast;`

### DML

+ #### SHOW
```sql
  SHOW DATABASES;
  SHOW TABLES;
  SHOW FIELDS FROM table / DESCRIBE table;
  SHOW CREATE TABLE table;
  SHOW PROCESSLIST;
  KILL process_number;
```

+ #### Database
```sql
  CREATE DATABASE DatabaseName CHARACTER SET utf8;
  CREATE DATABASE [IF NOT EXISTS] database_name;
  USE database_name;
  DROP DATABASE [IF EXISTS] database_name;
  ALTER DATABASE DatabaseName CHARACTER SET utf8;
```

+ #### Tables
```sql
  DESCRIBE table_name;
  DESCRIBE table_name column_name;

  CREATE TABLE [IF NOT EXISTS] table_name(column_list);
  CREATE TABLE table (..., PRIMARY KEY (column1, column2))
  CREATE TABLE table (..., FOREIGN KEY (column1, column2) REFERENCES table2(t2_column1, t2_column2))
  CREATE TABLE table (column1 type1, column2 type2);
  CREATE TABLE table (column1 type1, column2 type2, INDEX (column));
  CREATE TABLE table (column1 type1, column2 type2, PRIMARY KEY (column1));
  CREATE TABLE table (column1 type1, column2 type2, PRIMARY KEY (column1,column2));
  CREATE TABLE table1 (fk_column1 type1, column2 type2, ...,
  FOREIGN KEY (fk_column1) REFERENCES table2 (t2_columnA)) [ON UPDATE|ON DELETE] [CASCADE|SET NULL]
  CREATE TABLE table1 (fk_column1 type1, fk_column2 type2, ..., FOREIGN KEY (fk_column1, fk_column2) REFERENCES table2 (t2_columnA, t2_columnB))
  
  ALTER TABLE table ADD [COLUMN] column_name;
  ALTER TABLE table ADD I NDEX [name](column, ...);
  ALTER TABLE table ADD PRIMARY KEY (column_name,...);
  ALTER TABLE table ADD CONSTRAINT uq_email UNIQUE(email);
  ALTER TABLE table ADD new_name_column1 type1
  ALTER TABLE table ADD new_name_column1 type1 FIRST
  ALTER TABLE table ADD new_name_column1 type1 AFTER another_column
  ALTER TABLE table ADD INDEX (column);

  ALTER TABLE table MODIFY column1 type1
  ALTER TABLE table MODIFY column1 type1 NOT NULL ...
  ALTER TABLE table MODIFY column1 type1 FIRST
  ALTER TABLE table MODIFY column1 type1 AFTER another_column

  ALTER TABLE table CHANGE old_name_column1 new_name_column1 type1
  ALTER TABLE table CHANGE old_name_column1 new_name_column1 type1 NOT NULL ...
  ALTER TABLE table CHANGE old_name_column1 new_name_column1 type1 FIRST
  ALTER TABLE table CHANGE old_name_column1 new_name_column1 type1 AFTER another_column

  ALTER TABLE table ALTER column1 SET DEFAULT ...
  ALTER TABLE table ALTER column1 DROP DEFAULT

  ALTER TABLE table DROP column1
  ALTER TABLE table DROP [COLUMN] column_name;
  ALTER TABLE table DROP PRIMARY KEY;

  DROP TABLE [IF EXISTS] table_name;

  UPDATE table1 SET column1=new_value1 WHERE condition;
  UPDATE table1, table2 SET column1=new_value1, column2=new_value2, ... WHERE table1.id1 = table2.id2 AND condition;

  DELETE FROM table_name;
  DELETE FROM table1 / TRUNCATE table1
  DELETE FROM table1 WHERE condition
  DELETE FROM table1, table2 FROM table1, table2 WHERE table1.id1 =table2.id2 AND condition

  
```

+ #### Indexes
```sql
  CREATE INDEX index_name ON table_name (column,...);
  DROP INDEX index_name;
  CREATE UNIQUE INDEX index_name ON table_name (column,...);
```

+ #### Views
```sql 
  CREATE VIEW [IF NOT EXISTS] view_name AS select_statement;
  CREATE VIEW [IF NOT EXISTS] view_name AS select_statement WITH CHECK OPTION;
  CREATE OR REPLACE view_name AS select_statement;
  DROP VIEW [IF EXISTS] view_name;
  DROP VIEW [IF EXISTS] view1, view2, ...;
  RENAME TABLE view_name TO new_view_name;
  SHOW FULL TABLES [{FROM | IN } database_name] WHERE table_type = 'VIEW';
```

+ #### SELECT
```sql
  SELECT * FROM table;
  SELECT * FROM table1, table2;
  SELECT column1, column2, ... FROM table_name;
  SELECT column1 AS alias_name, expression AS alias, FROM table_name;
  SELECT ... FROM ... WHERE condition
  SELECT ... FROM ... WHERE condition GROUPBY column;
  SELECT ... FROM ... WHERE condition GROUPBY column HAVING condition2;
  SELECT ... FROM ... WHERE condition ORDER BY column1, column2;
  SELECT ... FROM ... WHERE condition ORDER BY column1, column2 DESC;
  SELECT ... FROM ... WHERE condition LIMIT 10;
  SELECT DISTINCT column FROM ...
  SELECT DISTINCT column1, column2 FROM table_name;
  SELECT COUNT(*) FROM table_name;
```

+ #### SELECT JOIN
```sql
  SELECT select_list FROM table1 INNER JOIN table2 ON condition;
  SELECT ... FROM t1 JOIN t2 ON t1.id1 = t2.id2 WHERE condition;
  SELECT ... FROM t1 LEFT JOIN t2 ON t1.id1 = t2.id2 WHERE condition;
  SELECT ... FROM t1 JOIN (t2 JOIN t3 ON ...) ON ...
  SELECT select_list FROM table1 LEFT JOIN table2 ON condition;
  SELECT select_list FROM table1 RIGHT JOIN table2 ON condition;
```

+ #### Conditions
```sql
  column1 = value1
  column1 <> value1
  column1 LIKE 'value _ %'
  column1 LIKE '%value%'
  column1 IS NULL
  column1 IS NOT NULL
  column1 IS IN (value1, value2)
  column1 IS NOT IN (value1, value2)
  condition1 AND condition2
  condition1 OR condition2
```

+ #### INSERT 
```sql
  INSERT INTO table1 (column1, column2) VALUES (value1, value2);
```

+ #### Users and Privileges
```sql
  CREATE USER 'user'@'localhost';
  GRANT ALL PRIVILEGES ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
  GRANT SELECT, INSERT, DELETE ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
  REVOKE ALL PRIVILEGES ON base.* FROM 'user'@'host'; -- one permission only
  REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user'@'host'; -- all permissions
  FLUSH PRIVILEGES;

  SET PASSWORD = PASSWORD('new_pass');
  SET PASSWORD FOR 'user'@'host' = PASSWORD('new_pass');
  SET PASSWORD = OLD_PASSWORD('new_pass');

  DROP USER 'user'@'host';
```

+ ### Main Data Types
```sql
  TINYINT (1o: -217+128)
  SMALLINT (2o: +-65 000)
  MEDIUMINT (3o: +-16 000 000)
  INT (4o: +- 2 000 000 000)
  BIGINT (8o: +-9.10^18)
  FLOAT(M,D)
  DOUBLE(M,D)
  FLOAT(D=0->53)
  TIME (HH:MM)
  YEAR (AAAA)
  DATE (AAAA-MM-JJ)
  DATETIME (AAAA-MM-JJ HH:MM; années 1000->9999)
  TIMESTAMP (like DATETIME, but 1970->2038, compatible with Unix)
  VARCHAR (single-line; explicit size)
  TEXT (multi-lines; max size=65535)
  BLOB (binary; max size=65535)
  ENUM ('value1', 'value2', ...) -- (default NULL, or '' if NOT NULL)
```