# MySQL

## Installation
### Client
```
sudo apt-get install mysql-client
```

## Switching from MySQL’s utf8 to utf8mb4

```
# Database
ALTER DATABASE database_name CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
# Table
ALTER TABLE table_name CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
# Column
ALTER TABLE table_name CHANGE column_name column_name VARCHAR(191) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### Create User
```
CREATE USER 'newuser'@'%' IDENTIFIED BY 'password';
```

```
GRANT ALL PRIVILEGES ON mydatabase. * TO 'newuser'@'%'; or GRANT SELECT, INSERT, DELETE ON mydatabase. * TO 'newuser'@'%';
```

```
FLUSH PRIVILEGES;
```

### Backup and restore

```
mysqldump -h hostname -u username -p database_name > backup.sql
```

```
mysql -h hostname -u username -p database_name < backup.sql
```

### Backup and restore in docker containes

#### Backup

```
docker exec CONTAINER /usr/bin/mysqldump -u root --password=root DATABASE > backup.sql
```

#### Restore

```
cat backup.sql | docker exec -i CONTAINER /usr/bin/mysql -u root --password=root DATABASE
```

### Export and Import

#### Import

```
LOAD DATA LOCAL INFILE '/path/to/data.csv' INTO TABLE table_name FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 ROWS (id, first_name, last_name, email, transactions, @account_creation)SET account_creation  = STR_TO_DATE(@account_creation, '%m/%d/%y');
```
