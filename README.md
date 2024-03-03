# SQL CRUD

## Restaurant Finder

### Code to create the tables
1) **Restaurnat table**
- CREATE TABLE restaurants ( res_id INTEGER PRIMARY KEY, name TEXT, neighbourhood TEXT, category TEXT, price TEXT, good_for_kids BOOLEAN, otime TEXT, ctime TEXT, star_rating INTEGER);

 2) **Reviews table**
 - CREATE TABLE reviews ( rev_id INTEGER PRIMARY KEY, res_id INTEGER, review TEXT);
### Code to import the csv file into the restaurant table
- before importin use this code- 
```sql
.separator ","
```
- .import 'C:\Spring 2024\database\4-sql-crud-Vighnesh2822000\data\restaurants.csv' restaurants --skip 1

### Link to the restaurants data file 
- [Mock restaurant data file](https://github.com/dbdesign-students-spring2024/4-sql-crud-Vighnesh2822000/blob/main/data/restaurants.csv)

### Answer Queries
Answer number corresponds to the question number on instructions page
```sql
- 1) select name from restaurants where price = 'cheap' and neighbourhood ='bronx';

```
```sql
- 2) select name, star_rating from restaurants where category = 'french' and star_rating >= 3 order by star_rating desc;
```
```sql
- 3) select * from restaurants where otime < strftime('%H:%M', 'now', 'localtime') and ctime > strftime('%H:%M', 'now', 'localtime');
```
```sql
- 4) insert into reviews (res_id, reviews) select res_id, 'The worst place' from restaurants where restaurants.name = 'Senger LLC';

```
```sql
- 5) delete from restaurants where good_for_kids = false;
```
```sql
- 6) select neighbourhood, count(name) as number_of_restaurants from restaurants group by neighbourhood; 
```
## Social Media A.db

### Code to create the tables
1) **Users table**
- create table users ( user_id INTEGER, username TEXT PRIMARY KEY, password TEXT, email TEXT);

2) **Posts table**
- CREATE TABLE posts( post_id INTEGER PRIMARY KEY, post_type TEXT, sender TEXT, receiver TEXT, date_time_posted DATETIME, visibility TEXT);

### Link to the mock data file
- [Users file](https://github.com/dbdesign-students-spring2024/4-sql-crud-Vighnesh2822000/blob/main/data/users.csv)
- [Posts file](https://github.com/dbdesign-students-spring2024/4-sql-crud-Vighnesh2822000/blob/main/data/posts.csv)

### code to imort the csv files
- before import use this code-
```sql
.separator ","
```
- .import 'C:\Spring 2024\database\4-sql-crud-Vighnesh2822000\users.csv' users --skip 1
- .import 'C:\Spring 2024\database\4-sql-crud-Vighnesh2822000\data\posts.csv' posts --skip 1

### Answer queries
Answer number corresponds to the question number on instructions page
```sql
1) insert into users (username, password, email) values ('vighnesh28','happyhappy', 'vd2058@nyu.edu');
```
```sql
2) insert into posts (post_type, sender, receiver, post_text, date_time_posted, visibility) values ('message', 'dbail0','tovise1', 'How is it going mate?', strftime('%Y-%m-%d %H:%M:%S', 'now', 'localtime'), 'Visible');
```
```sql
3) insert into posts(post_type, sender, receiver, post_text, date_time_posted, visibility) values ('story', 'vighnesh28', 'everyone', 'Party over here!!!!!', strftime('%Y-%m-%d %H:%M:%S', 'now', 'localtime'), 'Visible');
```
```sql
4) select * from posts where visibility = 'Visible' order by date_time_posted desc limit 10;
```
```sql
5) select * from posts where sender ='kchristophe0' and receiver = 'lmcettrick0' and visibility = 'Visible' and post_type = 'message' order by date_time_posted desc limit 10;
```
```sql
6) update posts set visibility = 'Invisible' where post_type = 'story' and julianday('now','localtime') - julianday(strftime(date_time_posted)) > 1;
```
```sql
7) select * from posts where visibility = 'Invisible' order by date_time_posted desc;
```
```sql
8) select users.username, count(post_id) from users inner join posts where users.username = posts.sender group by username;
```
```sql
9) select posts.post_text, users.email, username from users inner join posts on users.username = posts.sender where julianday('now','localtime') - julianday(date_time_posted) < 1; 
```
```sql
10) select username, email from users left join posts on users.username = posts.sender where posts.sender is null;
```
