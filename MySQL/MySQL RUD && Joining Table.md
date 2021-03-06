# TIL-Today-I-Learned- 20200612(Fri).md

Continuing CRUD

### 2. Read with `SELECT`

`SELECT * FROM topic;` shows the table. Limit the number of data when the table contains too much information.

`SELECT id, title, created, author FROM topic;`

`SELECT id, title, created, author FROM topic WHERE author='egoing';`

`SELECT id, title, created, author FROM topic WHERE author='egoing' ORDER BY id DESC;` //descending order

`SELECT id, title, created, author FROM topic WHERE author='egoing' ORDER BY id DESC LIMIT 2;` //show only two data

`SELECT "egoing";`

### 3. Update with `UPDATE SET`, `INSERT INTO` and `RENAME`

| 2  | ORACLE | ORACLE is ... | 2020-06-12 00:54:35 | jehong | developer |
| 2  | Oracle | Oracle is ... | 2020-06-12 00:54:35 | egoing | developer |

`UPDATE topic SET title='Oracle', description='Oracle is ...', author='egoing' WHERE id=2;`
Set values of the columns title, description and author where id is 2, that is, the second row.
Careful not to omit `WHERE ~` because the command will change all the corresponding values in the table.


| id | title | description | created | author | profile |
|----|-------|-------------|---------|--------|---------|
| 1  | MySQL | MySQL is ... | 2020-06-12 00:50:34 | jehong | developer |
| 2  | Oracle | Oracle is ... | 2020-06-12 00:54:35 | jehong | developer |
| 3  | SQL Server | SQL is ... | 2020-06-12 00:55:49 | duru | data administrator |
| 4  | PostgreSQL | PostgreSQL is ... | 2020-06-12 00:58:12 | taeho | data scientist, developer |
| 5  | MongoDB | MongoDB is ... | 2020-06-12 00:58:38 | egoing | developer |

After deleting row 5, I added it back
`INSERT INTO topic(title, description, created, author, profile) VALUES ('MongoDB', 'MongoDB is ...', NOW(), 'egoing', 'developer');
Since I did not specify the id, I got id = 6.
So I added the row again specifying id = 5
`INSERT INTO topic(id, title, description, created, author, profile) VALUES (5, 'MongoDB', 'MongoDB is ...', NOW(), 'egoing', 'developer');
This brought back the row 5 that I had deleted on the first place.
What was interesting was that this row with id = 5 was automatically placed above the row with id = 6.
Because id has the auto_incrementing feature.
I deleted the row with id = 6.

### 4. Delete with `DELETE`

`DELETE FROM topic WHERE id=5;` Must use `FROM` and `WHERE` so that the other data are safe.

## Overlapping data values

### Author column have overlapping data and can be managed like below:

| id | title | description | created | author_id |
|----|-------|-------------|---------|----------:|
| 1  | MySQL | MySQL is ... | 2020-06-12 00:50:34 |1|
| 2  | Oracle | Oracle is ... | 2020-06-12 00:54:35 |1|
| 3  | SQL Server | SQL is ... | 2020-06-12 00:55:49 |2|
| 4  | PostgreSQL | PostgreSQL is ... | 2020-06-12 00:58:12 |3|
| 5  | MongoDB | MongoDB is ... | 2020-06-12 00:58:38 |1|

| id | name | profile |
|----|------|---------|
| 1  | egoing | developer|
| 2  | duru | database administrator|
| 3  | taeho | data scientist, developer|

- This is useful when modifying these overlapping data (imaging there are 10,000 data).

- This is also useful in differentiating data that have the same name.
For example, if two authors named "egoing" existed one being a developer and the other a designer,
we give them two distinct ids to clearly see that they are different.
Otherwise, we have to additionally check profile or even other data on author.

- But this method is slower to get information because we have to check two tables.
Fortunately, MySQL is able to show these tables as if they were one.

### Joining table

`RENAME TABLE topic TO topic_backup;`

`SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.id;` This combines two tables where topic table's author_id equals author table's id.

| id | title | description | created | author_id | id | name | profile |
|----|-------|-------------|---------|----------:|----|------|---------|
| 1  | MySQL | MySQL is ... | 2020-06-12 00:50:34 |1|1  | egoing | developer|
| 2  | Oracle | Oracle is ... | 2020-06-12 00:54:35 |1|1  | egoing | developer|
| 3  | SQL Server | SQL is ... | 2020-06-12 00:55:49 |2| 2  | duru | database administrator|
| 4  | PostgreSQL | PostgreSQL is ... | 2020-06-12 00:58:12 |3| 3  | taeho | data scientist, developer|
| 5  | MongoDB | MongoDB is ... | 2020-06-12 00:58:38 |1|1  | egoing | developer|


Since author_id and author table's id are unnecessary:

`SELECT id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;` But MySQL won't execute this ambinuous command. There are two ids.

`SELECT topic.id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;` Specify which id.

## Internet

Client computer requests information to server computer.
This is called web.
Client computer uses web browser program.
Server computer uses web server program.

Web client, web server
Game client, game server
Chatting client, chatting server
Databse client, database server

Information is saved in server and the client requests it.
Mysql Monitor is one of the database clients provided with Mysql.
It is a CLI (Command Line Interface) where users request information through commands. Wherever MySQL is, there is also MySQL Monitor.
On the other hand, MySQL Workbench is a GUI(Graphical User Interface) client program. 
This is easy to see because it provides graphical information, but cannot be used everywhere.

## Workbench
`mysql -uroot -p -h[addresss of the database server to access through internet]` 
Since mysql server and mysql client are located in the same computer in my case, no need to write -h.
`hlocalhost` and `-h127.0.0.1` equal no `h` tag

