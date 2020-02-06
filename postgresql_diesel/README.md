# Usage

[When you make a full stack Rust app, your workflow will be similar to this.](https://github.com/steadylearner/Rust-Full-Stack)

1. Install Postgresql or another databases. 
2. Test first with its CLI commands(psql). 
3. Use ORM(Diesel etc) instead of them and integrate R2D2 for connection reuse.
4. Make Rust web server with routes.
5. Use a template engine such as Tera to show visual results. 
6. Substitue it with Yew or another single page app if necessary.

## Rust Diesel

1. [Starter for CRUD Structure](http://diesel.rs/guides/getting-started/)
2. [Documentation](http://docs.diesel.rs/diesel/index.html)
3. [Blog Example with Rocket Rust](https://notryanb.github.io/rust-blog-series-1.html)
4. [Refer to the example with Warp](https://github.com/steadylearner/Rust-Full-Stack/blob/master/warp/database/2.%20with_db_pool/src/models/post.rs) 

## Postgresql 

1. [Official Documentation](https://www.postgresql.org/docs/current/static/tutorial-sql.html)
2. [Install it in your machine](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04)
3. [You can also Use Docker or AWS etc instead to deploy or test locally.](https://www.steadylearner.com/blog/read/Docker)

## Connect to Postgesql


```console
// 1. Install Postgresql on Linux.
$sudo apt update && $sudo apt install postgresql postgresql-contrib
// 2. Login to psqL.
$sudo -i -u postgres 
// 3. Use it to connect to postgresql.
$psql
// 4. Create another user if you want.
$sudo -u postgres createuser --interactive
```

## Use it with SQL commands

You have to almost always use ; at the end you use it.

```sql
CREATE USER owner1 WITH PASSWORD 'password1';
ALTER USER my_user_name WITH PASSWORD 'my_secure_password';
CREATE DATABASE demo_db1 OWNER owner1; 
```

Refer to these commands from psql console.

```md
**\h** to show SQL 
**\?** for psql commands
**\password**
**\du** to list user 
**\l** to show databases
**\c db_name;** to connect to db_name made by the ORM or You
```

You can use Diesel at this point. But, you can also test it manually.

```console
CREATE TABLE demo_t(something int); // make table, CREATE TABLE demo_c(anychar char);
INSERT INTO demo_t (something) values (1); // Insert title and field to the table, edit table, or (anything) values ('$char')
DROP DATABASE demo_t // drop database
\dt // show table
\l // show database lists
SELECT * from demo_t;
\q
$DROP DATABASE IF EXISTS db_name; 
```
 
## Setup Diesel with Cargo

```console
// I had a problem using Cargo with "linking with cc failed exit code 1"
// and could solve it with this comamnd. 
$sudo apt install libpq-dev libmysqlclient-dev
 
$cargo install diesel_cli --no-default-features --features postgres or $cargo install diesel_cli
$cargo doc -p diesel --open 

// 1. Set up Diesl in your project.
// 2. Create migration "create_posts" 
// 3. Write SQL for migration 
// 4. Run it 
// 5. Redo if you want after you edit SQL you made before.

$diesel setup
$diesel migration create_post
// Move to migrations/ folder and use SQL similar to this.
CREATE TABLE posts (
   id SERIAL PRIMARY KEY,
   title VARCHAR NOT NULL,
   body TEXT NOT NULL
)
$diesel migration run
$diesel migraiton redo
---

You can use **$cargo run --bin [filename] [argument]** to use the CLI for this example.

You can use **$history** for commands you used before.

