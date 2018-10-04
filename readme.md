felipe@Felipe:~$ pwd
/home/felipe
felipe@Felipe:~$ cd Escritorio/fullstack_1
bash: cd: Escritorio/fullstack_1: No existe el archivo o el directorio
felipe@Felipe:~$ cd Escritorio/fullstack_14/
felipe@Felipe:~/Escritorio/fullstack_14$ ls
'Prueba HTML y CSS'   Semana10   Semana14   Semana3   Semana7
'Prueba RoR 1'        Semana11   semana15   Semana4   Semana8
'Pueba Ruby'          Semana12   semana16   Semana5   Semana9
 Semana1              Semana13   Semana2    Semana6
felipe@Felipe:~/Escritorio/fullstack_14$ cd semana16
felipe@Felipe:~/Escritorio/fullstack_14/semana16$ ls
E16CP1A1  E16CP1A2
felipe@Felipe:~/Escritorio/fullstack_14/semana16$ cd E16CP1A2
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2$ ls
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2$ git init
Inicializado repositorio Git vacío en /home/felipe/Escritorio/fullstack_14/semana16/E16CP1A2/.git/
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2$ git clone git@github.com:felipin1992/E16CP2A1.git
Clonando en 'E16CP2A1'...
remote: Counting objects: 14, done.
remote: Total 14 (delta 0), reused 0 (delta 0), pack-reused 14
Recibiendo objetos: 100% (14/14), 32.85 KiB | 5.47 MiB/s, listo.
Resolviendo deltas: 100% (3/3), listo.
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2$ ls
E16CP2A1
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2$ cd E16CP2A1
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2/E16CP2A1$ ls
readme.md  readme.pdf
felipe@Felipe:~/Escritorio/fullstack_14/semana16/E16CP1A2/E16CP2A1$ psql
psql (10.5 (Ubuntu 10.5-0ubuntu0.18.04))
Type "help" for help.

felipe=# create database pintagram;
CREATE DATABASE
felipe=# \dt
Did not find any relations.
felipe=# \l
felipe=# \c pintagram
You are now connected to database "pintagram" as user "felipe".
pintagram=# create table users (
pintagram(# id serial primary key,
pintagram(# name text
pintagram(# );
CREATE TABLE
pintagram=# select * from users;
 id | name 
----+------
(0 rows)

pintagram=# create table likes (
pintagram(# id integer primary key,
pintagram(# user_id integer references users (id),
pintagram(# );
ERROR:  syntax error at or near ")"
LINE 4: );
        ^
pintagram=# create table images (
pintagram(# id integer primary key,
pintagram(# user_id integer references users (id),
pintagram(# name text,
pintagram(# url text
pintagram(# );
CREATE TABLE
pintagram=# create table likes(
pintagram(# id integer primary key,
pintagram(# user_id integer references user (id),
pintagram(# image_id integer references images (id)
pintagram(# );
ERROR:  syntax error at or near "user"
LINE 3: user_id integer references user (id),
                                   ^
pintagram=# create table likes(
id integer primary key,
user_id integer references users (id),
image_id integer references images (id)
);
CREATE TABLE
pintagram=# \l
pintagram=# \dt
        List of relations
 Schema |  Name  | Type  | Owner  
--------+--------+-------+--------
 public | images | table | felipe
 public | likes  | table | felipe
 public | users  | table | felipe
(3 rows)

pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
(0 rows)

pintagram=# alter table images add constraint imagesfk foreign key (like_id) references likes (id);
ERROR:  column "like_id" referenced in foreign key constraint does not exist
pintagram=# alter table images add column like_id integer;
ALTER TABLE
pintagram=# alter table images add constraint imagesfk foreign key (like_id) references likes (id);
ALTER TABLE
pintagram=# select * from likes
pintagram-# ;
 id | user_id | image_id 
----+---------+----------
(0 rows)

pintagram=# select * from images
pintagram-# ;
 id | user_id | name | url | like_id 
----+---------+------+-----+---------
(0 rows)

pintagram=# create table tags (
pintagram(# id serial primary key,
pintagram(# image_id integer references images (id)
pintagram(# );
CREATE TABLE
pintagram=# create table images_tags (
pintagram(# image_id integer references images (id),
pintagram(# tag_id integer references tags (id)
pintagram(# );
CREATE TABLE
pintagram=# \l
pintagram=# \l
pintagram=# \
Invalid command \. Try \? for help.
pintagram=# \l
pintagram=# \dt
           List of relations
 Schema |    Name     | Type  | Owner  
--------+-------------+-------+--------
 public | images      | table | felipe
 public | images_tags | table | felipe
 public | likes       | table | felipe
 public | tags        | table | felipe
 public | users       | table | felipe
(5 rows)

pintagram=# insert into users (name) values ('felipe'), ('shakira');
INSERT 0 2
pintagram=# select * from users;
 id |  name   
----+---------
  1 | felipe
  2 | shakira
(2 rows)

pintagram=# selest
pintagram-# ;
ERROR:  syntax error at or near "selest"
LINE 1: selest
        ^
pintagram=# select * from images;
 id | user_id | name | url | like_id 
----+---------+------+-----+---------
(0 rows)

pintagram=# insert into images (user_id, name, url) values (1, 'image1', 'hhh'),(1, 'image2', 'hhhh'), (2, 'image1', 'hhh'),(2, 'image2', 'hhhh');
ERROR:  null value in column "id" violates not-null constraint
DETAIL:  Failing row contains (null, 1, image1, hhh, null).
pintagram=# insert into images (id, user_id, name, url) values (1, 1, 'image1', 'hhh'), (2, 1, 'image2', 'hhh'), (3, 2, 'image1', 'hhh'), (4, 1, 'image1', 'hhh');
INSERT 0 4
pintagram=# select * from images;
 id | user_id |  name  | url | like_id 
----+---------+--------+-----+---------
  1 |       1 | image1 | hhh |        
  2 |       1 | image2 | hhh |        
  3 |       2 | image1 | hhh |        
  4 |       1 | image1 | hhh |        
(4 rows)

pintagram=# update images set user_id = 2 where id = 4;
UPDATE 1
pintagram=# select * from images;
 id | user_id |  name  | url | like_id 
----+---------+--------+-----+---------
  1 |       1 | image1 | hhh |        
  2 |       1 | image2 | hhh |        
  3 |       2 | image1 | hhh |        
  4 |       2 | image1 | hhh |        
(4 rows)

pintagram=# update images set name = 'image2' where id = 4;
UPDATE 1
pintagram=# select * from images;
 id | user_id |  name  | url | like_id 
----+---------+--------+-----+---------
  1 |       1 | image1 | hhh |        
  2 |       1 | image2 | hhh |        
  3 |       2 | image1 | hhh |        
  4 |       2 | image2 | hhh |        
(4 rows)

pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
(0 rows)

pintagram=# alter table likes drop column id;
ERROR:  cannot drop table likes column id because other objects depend on it
DETAIL:  constraint imagesfk on table images depends on table likes column id
HINT:  Use DROP ... CASCADE to drop the dependent objects too.
pintagram=# insert into likes (1,1);
ERROR:  syntax error at or near "1"
LINE 1: insert into likes (1,1);
                           ^
pintagram=# insert into likes values (1,1);
INSERT 0 1
pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  1 |       1 |         
(1 row)

pintagram=# insert into likes values (2,1,1);
INSERT 0 1
pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  1 |       1 |         
  2 |       1 |        1
(2 rows)

pintagram=# insert into likes values (image_id = 1) where (id = 1);
ERROR:  syntax error at or near "where"
LINE 1: insert into likes values (image_id = 1) where (id = 1);
                                                ^
pintagram=# insert into likes values (image_id = 1) where id = 1;
ERROR:  syntax error at or near "where"
LINE 1: insert into likes values (image_id = 1) where id = 1;
                                                ^
pintagram=# insert into likes values (3, 1, 1);
INSERT 0 1
pintagram=# insert into likes values (image_id = 1) select * from likes where id= 1;
ERROR:  syntax error at or near "select"
LINE 1: insert into likes values (image_id = 1) select * from likes ...
                                                ^
pintagram=# update likes set image_id = 1 where id = 1;
UPDATE 1
pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  2 |       1 |        1
  3 |       1 |        1
  1 |       1 |        1
(3 rows)

pintagram=# insert into likes values (4,2,1), (5,2,1), (6,2,1);
INSERT 0 3
pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  2 |       1 |        1
  3 |       1 |        1
  1 |       1 |        1
  4 |       2 |        1
  5 |       2 |        1
  6 |       2 |        1
(6 rows)

pintagram=# insert into likes values (7,1,2), (8,1,2), (9,1,2);
INSERT 0 3
pintagram=# insert into likes values (10,1,3), (11,1,3), (12,1,3);
INSERT 0 3
pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  2 |       1 |        1
  3 |       1 |        1
  1 |       1 |        1
  4 |       2 |        1
  5 |       2 |        1
  6 |       2 |        1
  7 |       1 |        2
  8 |       1 |        2
  9 |       1 |        2
 10 |       1 |        3
 11 |       1 |        3
 12 |       1 |        3
(12 rows)

pintagram=# insert into likes values (13,2,3), (14,2,3), (15,2,3);
INSERT 0 3
pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  2 |       1 |        1
  3 |       1 |        1
  1 |       1 |        1
  4 |       2 |        1
  5 |       2 |        1
  6 |       2 |        1
  7 |       1 |        2
  8 |       1 |        2
  9 |       1 |        2
 10 |       1 |        3
 11 |       1 |        3
 12 |       1 |        3
 13 |       2 |        3
 14 |       2 |        3
 15 |       2 |        3
(15 rows)

pintagram=# select * from likes;
 id | user_id | image_id 
----+---------+----------
  2 |       1 |        1
  3 |       1 |        1
  1 |       1 |        1
  4 |       2 |        1
  5 |       2 |        1
  6 |       2 |        1
  7 |       1 |        2
  8 |       1 |        2
  9 |       1 |        2
 10 |       1 |        3
 11 |       1 |        3
 12 |       1 |        3
 13 |       2 |        3
 14 |       2 |        3
 15 |       2 |        3
(15 rows)

pintagram=# select * from tags;
 id | image_id 
----+----------
(0 rows)

pintagram=# insert into tags values (image_id) values (1), (1), (1), (1), (2), (2), (2), (2);
ERROR:  syntax error at or near "values"
LINE 1: insert into tags values (image_id) values (1), (1), (1), (1)...
                                           ^
pintagram=# insert into tags values (image_id) values (1);
ERROR:  syntax error at or near "values"
LINE 1: insert into tags values (image_id) values (1);
                                           ^
pintagram=# insert into tags (image_id) values (1), (1), (1), (1), (2), (2), (2), (2);
INSERT 0 8
pintagram=# select * from tags;
 id | image_id 
----+----------
  1 |        1
  2 |        1
  3 |        1
  4 |        1
  5 |        2
  6 |        2
  7 |        2
  8 |        2
(8 rows)

pintagram=# insert into likes values (16,2,4), (17,2,4), (15,2,4);
ERROR:  duplicate key value violates unique constraint "likes_pkey"
DETAIL:  Key (id)=(15) already exists.
pintagram=# insert into likes values (16,2,4), (17,2,4), (16,2,4);
ERROR:  duplicate key value violates unique constraint "likes_pkey"
DETAIL:  Key (id)=(16) already exists.
pintagram=# insert into likes values (16,2,4), (17,2,4), (18,2,4);
INSERT 0 3
pintagram=# insert into tags (image_id) values (3), (3), (3), (4), (4), (4);
INSERT 0 6
pintagram=# select * from tags;
 id | image_id 
----+----------
  1 |        1
  2 |        1
  3 |        1
  4 |        1
  5 |        2
  6 |        2
  7 |        2
  8 |        2
  9 |        3
 10 |        3
 11 |        3
 12 |        4
 13 |        4
 14 |        4
(14 rows)

pintagram=# select * from images inner join likes on (id = image_id);
ERROR:  column reference "id" is ambiguous
LINE 1: select * from images inner join likes on (id = image_id);
                                                  ^
pintagram=# select * from images inner join likes on (images.id = likes.image_id);
 id | user_id |  name  | url | like_id | id | user_id | image_id 
----+---------+--------+-----+---------+----+---------+----------
  1 |       1 | image1 | hhh |         |  2 |       1 |        1
  1 |       1 | image1 | hhh |         |  3 |       1 |        1
  1 |       1 | image1 | hhh |         |  1 |       1 |        1
  1 |       1 | image1 | hhh |         |  4 |       2 |        1
  1 |       1 | image1 | hhh |         |  5 |       2 |        1
  1 |       1 | image1 | hhh |         |  6 |       2 |        1
  2 |       1 | image2 | hhh |         |  7 |       1 |        2
  2 |       1 | image2 | hhh |         |  8 |       1 |        2
  2 |       1 | image2 | hhh |         |  9 |       1 |        2
  3 |       2 | image1 | hhh |         | 10 |       1 |        3
  3 |       2 | image1 | hhh |         | 11 |       1 |        3
  3 |       2 | image1 | hhh |         | 12 |       1 |        3
  3 |       2 | image1 | hhh |         | 13 |       2 |        3
  3 |       2 | image1 | hhh |         | 14 |       2 |        3
  3 |       2 | image1 | hhh |         | 15 |       2 |        3
  4 |       2 | image2 | hhh |         | 16 |       2 |        4
  4 |       2 | image2 | hhh |         | 17 |       2 |        4
  4 |       2 | image2 | hhh |         | 18 |       2 |        4
(18 rows)

pintagram=# select name.count(image_id) from users full join images (users.id = images.user_id) group by name;
ERROR:  syntax error at or near "group"
LINE 1: ...sers full join images (users.id = images.user_id) group by n...
                                                             ^
pintagram=# select name, count(images.id) from users inner join images on (user.id = images.user_id) group by name;
ERROR:  syntax error at or near "."
LINE 1: ...t(images.id) from users inner join images on (user.id = imag...
                                                             ^
pintagram=# select name, count(id) from users inner join images on (user.id = images.user_id) group by name;
ERROR:  syntax error at or near "."
LINE 1: ...e, count(id) from users inner join images on (user.id = imag...
                                                             ^
pintagram=# 

