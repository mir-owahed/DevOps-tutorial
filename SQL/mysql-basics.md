```
sudo apt update
sudo apt install mysql-server -y
sudo systemctl status mysql
sudo mysql
[mysql -u root -h sql.myserver.com -p 3306 -p ]
show databases;
create database test-db;
use test-db;
show tables;
create table table_name (
id int,
name varchar(255),
region varchar(255)
);
describe table table_name;
insert into table_name values (1, "mir", "kol");
show tables;
describe tables;
select * from table_name;
select name from table_name;
select * from table_name where origin = "earth";
select * from table_name where origin = "earth" or origin = "asgard";
select field_name from table_name where age < 30;
select * from table_name where not origin = "earth";
delete from table_name where first_name = "mir";
update table_name set last_name = "ali" where fiest_name = "mir";
alter table table_name add column_name boolean;
```
