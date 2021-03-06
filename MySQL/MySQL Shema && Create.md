# TIL-Today-I-Learned- 20200611(Thur)

CRUD (Create/Read/Update/Delete)

## MySQL
I downloaded Bitnami WAMP for Windows.
- Open `Bitnami WAMP Stack Manager Tool`
- Windows + R >> enter cmd
- Go to Bitnami WAMP bin directory. In my case, `C:\Bitnami\wampstack-7.4.6-1\mysql\bin`
- Enter `Mysql -uroot -p`
- Choose the database to work on.


### Schema
Database is a group of tables in a Database(Database server)
In Mysql, it is also called a Schema
and a Database server like Mysql contains several Schemas.
table < schema/database < database server(Mysql)

`CREATE DATABASE [name];`

`DROP DATABASE [name];`

`SHOW DATABASES;`

`USE [name];`

*`[name]` is the name of the DATABSE created (name of a Schema)

---
## CRUD (Create/Read/Update/Delete) 
Four major funcions of a Databse.

I made a table like below in my MySQL databse.
| id | title | description | created | author | profile |
|----|-------|-------------|---------|--------|---------|
| 1  | MySQL | MySQL is ... | 2020-06-12 00:50:34 | jehong | developer |
| 2  | ORACLE | ORACLE is ... | 2020-06-12 00:54:35 | egoing | developer |
| 3  | SQL Server | SQL is ... | 2020-06-12 00:55:49 | duru | data administrator |
| 4  | PostgreSQL | PostgreSQL is ... | 2020-06-12 00:58:12 | taeho | data scientist, developer |
| 5  | MongoDB | MongoDB is ... | 2020-06-12 00:58:38 | egoing | developer |

### 1. Create with `CREATE`
It is possible to limit the type of data entered in the table.

- Creating a table

| id | title | description | created | author | profile |
|----|-------|-------------|---------|--------|---------|
```
CREATE TABLE topic(
    id INT(11) NOT NULL AUTO_INCREMENT,   //INT(11) means data type int && show 11 data when searched. 
                                          //NOT NULL because data must exist
                                          //id is an integer increasing by one
    title VARCHAR(100) NOT NULL,          //100 is the max size of title
    description TEXT NULL,                //VARCHAR's max is 255 while TEXT's is 65,535
    created DATETIME NOT NULL,
    author VARCHAR(30) NULL,
    profile VARCHAR(100) NULL,
    PRIMARY KEY(id));                      //shows the main element which cannot have overlapping values.
```

- Inserting values to the table
`SHOW TABLES;`

`DESC topic;` show attributes of the main column(field)

`ALTER TABLE topic MODIFY id INT(11) NOT NULL AUTO_INCREMENT;` modify the attributes of an existing column

`INSERT INTO topic (title, description, created, author, profile) VALUES('MySQL', 'MySQL is ...', NOW(), 'jehong', 'developer');` create row and its value

`SELECT * FROM topic;` read rows from table

