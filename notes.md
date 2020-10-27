cd demos/
✔ ~/dev/craftacademy/demos 
11:49 $ brew services list
Name       Status  User     Plist
postgresql started emiliano /Users/emiliano/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
unbound    stopped          
✔ ~/dev/craftacademy/demos 
11:50 $ psql postgres
psql (12.4)
Type "help" for help.

postgres=# CREATE ROLE api_user WITH LOGIN PASSWORD 'password';
CREATE ROLE
postgres=# ALTER ROLE api_user CREATEDB;
ALTER ROLE
postgres=# \q
✔ ~/dev/craftacademy/demos 
11:57 $ psql - postgres -U api_user
psql: warning: extra command-line argument "postgres" ignored
psql: error: could not connect to server: FATAL:  database "-" does not exist
✘-2 ~/dev/craftacademy/demos 
11:57 $ psql -d postgres -U api_user
psql (12.4)
Type "help" for help.

postgres=> \
invalid command \
Try \? for help.
postgres=> \q
✔ ~/dev/craftacademy/demos 
12:03 $ ls /usr/local/var/postgres/
PG_VERSION		pg_multixact		pg_tblspc
base			pg_notify		pg_twophase
global			pg_replslot		pg_wal
pg_commit_ts		pg_serial		pg_xact
pg_dynshmem		pg_snapshots		postgresql.auto.conf
pg_hba.conf		pg_stat			postgresql.conf
pg_ident.conf		pg_stat_tmp		postmaster.opts
pg_logical		pg_subtrans		postmaster.pid
✔ ~/dev/craftacademy/demos 
12:03 $ psql -d postgres -U api_user
psql (12.4)
Type "help" for help.

postgres=> CREATE DATABASE books_api;
CREATE DATABASE
postgres=> \c books_api 
You are now connected to database "books_api" as user "api_user".
books_api=> CREATE TABLE books (
books_api(> ID SERIAL PRIMARY KEY,
books_api(> author VARCHAR(255) NOT NULL,
books_api(> title VARCHAR(255) NOT NULL
books_api(> );
CREATE TABLE
books_api=> \DT
invalid command \DT
Try \? for help.
books_api=> \dt
         List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | books | table | api_user
(1 row)

books_api=> SELECT * FROM books
books_api-> ;
 id | author | title 
----+--------+-------
(0 rows)

books_api=> INSERT INTO books (author, title)
books_api-> VALUES ('J.K. Rowling', 'Harry Potter');
INSERT 0 1
books_api=> SELECT * FROM books
books_api-> ;
 id |    author    |    title     
----+--------------+--------------
  1 | J.K. Rowling | Harry Potter
(1 row)

books_api=> INSERT INTO books (author, title)
VALUES ('A. Lindgren', 'The adventures of Pippi Longstocking');
INSERT 0 1
books_api=> SELECT * FROM books
;
 id |    author    |                title                 
----+--------------+--------------------------------------
  1 | J.K. Rowling | Harry Potter
  2 | A. Lindgren  | The adventures of Pippi Longstocking
(2 rows)

books_api=> \q
✔ ~/dev/craftacademy/demos 
14:30 $ mkdir books_api
✔ ~/dev/craftacademy/demos 
14:31 $ cd books_api/
✔ ~/dev/craftacademy/demos/books_api 
14:32 $ yarn init
yarn init v1.22.5
question name (books_api): 
question version (1.0.0): 
question description: 
question entry point (index.js): app.js
question repository url: 
question author: Emiliano
question license (MIT): 
question private: 
success Saved package.json
✨  Done in 34.10s.
✔ ~/dev/craftacademy/demos/books_api 
14:33 $ ls 
package.json
✔ ~/dev/craftacademy/demos/books_api 
14:33 $ touch .env
✔ ~/dev/craftacademy/demos/books_api 
14:33 $ code .
✔ ~/dev/craftacademy/demos/books_api 
14:34 $ git st
fatal: not a git repository (or any of the parent directories): .git
✘-128 ~/dev/craftacademy/demos/books_api 
14:38 $ git init
Initialized empty Git repository in /Users/emiliano/dev/craftacademy/demos/books_api/.git/
✔ ~/dev/craftacademy/demos/books_api [master L|…2] 
14:38 $ git add .
✔ ~/dev/craftacademy/demos/books_api [master L|●2] 
14:38 $ git ci -m 'Initializing yarn, creating .env with DB settings and .gitignore'
[master (root-commit) 2e529ca] Initializing yarn, creating .env with DB settings and .gitignore
 2 files changed, 10 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 package.json
✔ ~/dev/craftacademy/demos/books_api [master L|✔] 