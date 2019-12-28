# Creating the Database

Now we are ready to flush out the DAO Layer and Database layers.  Remember are architecture diagram?

![](12-backend-layers.png)


So far we have built out a Product Controller, and a Product Service (Business Logic). 

We are going to "jump" over the DAO and go ahead and flush out the basic Postgres database, then work backwards toward the DAO, ultimatly connecting the Service (Business Logic) layer to the DAO. 

## Setup Postgres

Lets get Postgres installed and up and running:

I ~~stole~~ borrowed these steps from an awesome [Medium writeup by Martin Lasek](https://medium.com/@martinlasek/tutorial-how-to-use-postgresql-88cddc858d9f)


1. Install Postgres.

If working on a mac, then just use homebrew to install postgres. Otherwise, just google around. 

[https://wiki.postgresql.org/wiki/Homebrew](https://wiki.postgresql.org/wiki/Homebrew)


2. Create a database called `retaildb`

```
createdb retaildb;
```

3. Connect to `retaildb`
```
$ psql retaildb
psql (10.10)
Type "help" for help.

retaildb=# 
```

4. Create a user for our project 

thanks to [Arnav Gupta](https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e)

```
# please pick a different password :D 
retaildb=# create user svc_retail with encrypted password 'RetailRules123';
CREATE ROLE
retaildb=# grant all privileges on database retaildb to svc_retail;
GRANT
```

5. Quick Cheatsheet of commands:

[More detailed cheatsheet here](http://www.postgresqltutorial.com/postgresql-cheat-sheet/)

```
# exit psql shell
\q

# start psql shell from terminal
psql -U svc_retail -d retaildb

# see all the database in postgres
\l

# show all tables in database
\dt
```

## Create our first Table




1. Start the psql shell 

```
psql -U svc_retail -d retaildb
```

2. Create the products table


```
retaildb=> CREATE TABLE products
(
  id UUID PRIMARY KEY,
  name character varying(50),
  price NUMERIC(8,2)
);
```

3. Now lets see what happened:

```
# show the table
retaildb=> \dt products

           List of relations
 Schema |   Name   | Type  |   Owner    
--------+----------+-------+------------
 public | products | table | svc_retail
(1 row)

# describe the details of the table
retaildb=> \d products


                     Table "public.products"
 Column |         Type          | Collation | Nullable | Default 
--------+-----------------------+-----------+----------+---------
 id     | uuid                  |           | not null | 
 name   | character varying(50) |           |          | 
 price  | numeric(8,2)          |           |          | 
Indexes:
    "products_pkey" PRIMARY KEY, btree (id)

```

## Import our data

If you have tabular data, meaning data, that can fit in a set of rows and columns, then it can be exported as [Comma Seperated Values (CSV)](https://en.wikipedia.org/wiki/Comma-separated_values).  CSV has been around forever and is very useful and supported. 

Postgres has a specific method for importing CSV diretly into a table. 

[http://www.postgresqltutorial.com/import-csv-file-into-posgresql-table/](http://www.postgresqltutorial.com/import-csv-file-into-posgresql-table/)

copy the below data into a file in the root of your project. 
or you can [download it](products-data.csv)

```
id,name,price
cb76350a-e3ff-44ad-bd2f-0abeda30340b,Hammer,5.98
9e3554a8-f98b-4d66-80f1-72fe8e96b826,Screwdriver,3.99
e78a6b2d-760e-42e4-a51c-66abdac4e0fb,Nail Gun,29.98
9ba7d210-7ee8-477e-b01e-069198c6fca0,Gas Grill,499.98
a99675a1-a127-4bbc-bf97-13e169793000,Christmas Inflatiable,19.99
9a4bcf11-02ee-4971-a736-81cfab5b1053,Trash Can,49.98
b730e391-68bb-4e45-8fc7-6b2ce75b3c53,Celing Fan,119.98
9c9ffd03-707d-4e2f-ab5c-ac0e7ffca3b4,Light Blub,2.98
cb41c784-4faa-440a-82ca-ea564eb22b74,Box Fan,17.49
04339838-cd0b-4b29-8307-db0fc1ec1797,Doorbell,49.49
ba3f9263-e104-4d89-bfc7-f1cf726478d4,Front Door,649.98
2d014c5a-5570-4ee7-8501-103d01251c01,Window,299.98
36923213-68e9-4a94-9e7c-f0389dbbd2a4,Toilet,120.49
0db62db3-b799-4e4e-9a86-a38b62bf38df,Sink,149.49
8d789158-27a9-4304-b0ed-864db490b6ed,Rope 120ft,19.49
f9847a80-6c27-4cd7-98fe-ad34510a2781,Toilet Plunger,2.98
06df04e7-75df-44ad-8474-6ac51caa50c7,2x4 10ft,3.49
```

Then run the below command, changing out the path to the file for your laptop:

```
retaildb=> \copy products FROM '/Users/cade/path/to/products-data.csv' DELIMITER ',' CSV HEADER
COPY 17
retaildb=> select count(*) from products;
 count 
-------
    17
(1 row)
```

SUCCESS!!! We now have data in postgres! 


## Query the Data

Lets run a copy of quick query commands just to see what the data looks like:

```
select * from products where price > 200.00;

select * from products order by price;

select * from products order by price desc;

select * from products where name = 'Sink';

select * from products where name like '%Toilet%';

select count(*) from products;

select avg(price) from products;

select sum(price) from products;

```


## Further Reading:

* https://www.mkyong.com/spring-boot/spring-boot-jdbc-examples/

## [NEXT -->](17-flush-out-dao.md)