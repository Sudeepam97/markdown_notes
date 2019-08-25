# DBMS Basics
* Database Management Systems are used to interact with a database.
* The DBMS can create, read, update, and delete (C.R.U.D.) the contents of a database.
* Relational databases use SQL and organize the data into one or more tables. Each table has columns and 
  rows, and a unique key identifies each row.
* Non Relational databases (NoSQL or Not just SQL) organize data in anything but a traditional table.
  Examples are: Graphs, documents like JSON, Key-Valie Pairs etc.
* SQL or Structured Query Language is a **standardized** language for interacting with Relational DBMS (RDBMS).
  So for example, PostgreSQL, SQLite, and MySQL are different RDBMS and to interact with either of them, we use this
  standardized language called SQL. However, not all RDBMS follow SQL in an exactly similar fashion.
* Primary Key is an attribute that uniquely defines a row in a database.
* Primary Key can be natural or surrogate. Surrogate Key has no mapping to the real world.
* A primary key may consist of a combination of 2 or more column values, in such a case it is called a Composite Key.
* Individual columns of a Composite Key may be same across rows but the combinations would be different for each row. 
* A Foreign Key in a database table, stores the Primary Key of a row of another table.
* We can create relations between various tables using Foreign Keys.


# Running PostgreSQL
* We will be using postgreSQL (called postgres) for this tutorial. Using Postgres inside a docker container is recommended during the learning phase. Install docker and pull the image of postgres.
```sh
# Create a postgres container
docker run --name sudeepam-postgres -e POSTGRES_PASSWORD=some_pass -d -p 5432:5432 postgres

# Bash into this container
docker exec -it sudeepam-postgres bash
# With the above command, we actually have opened up a terminal
# inside this docker container. This is similar to how we select
# the python virtual environment. Try running some commands like
# `ls` and `pwd` to get a feel of it.

# Now, we can enter postgres with the command.
psql -U postgres
```


# Creating a Database
```sql
/*Create a database*/
CREATE DATABASE learning;

\l            /* Check all available databases*/
\l learning   /* Info about the database specified */

/*Remove a database (use carefully)*/
DROP DATABASE learning;
```
* **Pro Tip:** Press `Ctrl + L` to clear screen from within postgres in a Linux setting.


# Connecting to a Database
After we have created a database, we need to connect to it to perform CRUD operations.
```sh
# Method 1 (directly from shell)
psql - h localhost -p 5432 -U postgres database_name
```
OR

```sql
/* from within postgres. My preference */
\l              /*list databases*/
\c learning     /*connect to one*/
```


# Creating a Table
```sql
/*Creating a Table*/
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY,
    name VARCHAR(30),
    major VARCHAR(30)
);

\d          /* To check the state of the curent database */
\d student  /* To check the state of the table specified */
```


# Inserting Data into a Table
* Now that we have our student table we will start inserting some data into it.
* Our table is of the form ...

| student_id |   name   | major |
| :--------: |   :--:   | :---: |
|     1      |  name_1  |  ECE  |
|     2      |  name_2  |  CSE  |

```sql
/* We can either insert in the exact same order of columns like...*/
INSERT INTO student VALUES(1, 'Jack', 'Biology');
INSERT INTO student VALUES(2, 'Kate', 'Sociology');

/* OR, we can define the order of insertion...*/
INSERT INTO student(name, major, student_id) VALUES('Claire', 'English', 3);
```

* The second format is more error resistant, and can also be used to insert data even if certain values, like, say the major of a student is unknown, in such a case, the unknown field would automatically assume a value of `NULL`.

* Now, the entire database can be viewed with the following statement.
```sql
SELECT * FROM student;
```
* This `SELECT` command will be described in detail, later.


# Constraints
* Now, we define the table again, by using some `constraints`.
* Constraints allow us to make the table more error proof and makes it easier for us to insert data correctly into the table.
* Say, some columns of our table should not have an empty value. We can impose this restriction on our tables with `NOT NULL`.
* We can also use a constraint like `UNIQUE` to make sure some columns have different value for each row.
* Another constraint is `CHECK` which makes sure that only the allowed values can be entered in a column
* **Note**: The difference between a UNIQUE and primary key is that PK is both NOT NULL and UNIQUE.

```sql
\c learning
DROP TABLE student; /* To delete a Table */

CREATE TABLE student (
    student_id INTEGER,
    name VARCHAR(30) NOT NULL,  /* Demonstration of NOT NULL*/
    major VARCHAR(30) UNIQUE,   /* Demonstration of UNIQUE*/
    PRIMARY KEY (student_id)
    gender VARCHAR(10) CHECK (gender == 'MALE' OR gender == 'FEMALE') /* Demonstration of CHECK */
);

/* Inserts fine*/
INSERT INTO student VALUES(1, 'Jack', 'Biology');

/* Error occours since name is null*/
INSERT INTO student(student_id, major) VALUES(3, 'English');
INSERT INTO student VALUES(3, NULL, 'Chemistry');

/* Error since major is not unique*/
INSERT INTO student VALUES(4, 'Kate', 'Biology');
```

* The `DEFAULT` constraint lets us set a default value for a column.
* `SERIAL` is useful when working with primary keys, if primary keys are simple serial numbers (say), we won't need to manually pass them if we are using this command. Obviously this constraint can be used for non PRIMARY_KEY columns as well.

```sql
\c learning;
DROP TABLE student;

/* SERIAL is an auto increment INTEGER and BIGSERIAL is an auto increment BIGINTEGER */
CREATE TABLE student (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(30),
    major VARCHAR(30) DEFAULT 'undecided'
);

INSERT INTO student(name, major) VALUES('Jack', 'Biology');
INSERT INTO student(name) VALUES('Kate');
INSERT INTO student(name, major) VALUES('Claire', 'Chemistry');
INSERT INTO student(name, major) VALUES('Jack', 'Biology');
INSERT INTO student(name, major) VALUES('Mike', 'Computer Science');

SELECT * FROM student;
```


# Mockaroo and Running SQL scripts
* Mockaroo is a website which can be used to generate large amounts of randomn data.
* We will use it to generate 1000 entry points as explained [here](https://youtu.be/hMPptslDjsQ).
* This will give us a `.sql` file containing the table definition and appropriate `INSERT` statements.
* Within psql enter: `\i /path/to/file` to execute SQL commands from this `.sql` file.
* If psql is running on docker. Attach a volume to the container and proceed as above.
```sh
# Note that we would have to either create a new container from the psql image, or we can commit the
# current state of our psql container as an image, then create a new container from this image, with
# the desired mount, remove the old container, and then re-name the new container to the old name.

# For now, we will simply create a new container. First remove the old container. Then... 
docker run --name sudeepam-postgres -v /home/sudeepam/Desktop/SQL:/usr/src/learn_sql -e POSTGRES_PASSWORD=some_pass -d -p 5432:5432 postgres
# /home/sudeepam/Desktop/SQL : is the host directory that we want to mount.
# /usr/src/learn_sql : is the location within the container where we want to mount.

# Then open bash inside container...
docker exec -it sudeepam-postgres bash

# Start postgres
psql -U postgres

# Run from within postgres
\i /usr/src/learn_sql/filename.sql
```


# Selection
* Let us look at a few examples of `SELECT` statement and understand them.

## BASICS
```sql
/* Select everything from the `person` table. */
SELECT * FROM person;

/* List all the `first_names` in the `person` table. */
SELECT first_name FROM person;

/* List all the last names along with the first names. */
SELECT first_name, last_name FROM person;
```

## Get sorted results with `ORDER BY`
```sql
/* Order the results by date_of_birth. Default is Ascending. */
SELECT * FROM person ORDER BY date_of_birth;

/* Order by Lexiographically descending order of country_of_birth
   Note: We can use `ASC` for Ascending but that is default anyway.*/
SELECT * FROM person ORDER BY country_of_birth DESC;

/* Sort by multipl entries. Here, the first priority would be 
   country_of_birth and the next priority would be date_of_birth. */
SELECT * FROM person ORDER BY country_of_birth, date_of_birth;
```

## LENGTH()
* length is a function that is used to get the length of a `VARCHAR`.
```sql
/* https://www.hackerrank.com/challenges/weather-observation-station-5/problem */
SELECT city, LENGTH(city) FROM station ORDER BY LENGTH(city), city LIMIT 1;
SELECT city, LENGTH(city) FROM station ORDER BY LENGTH(city) DESC, city LIMIT 1;
```

## Get unique values with `DISTINCT`
```sql
/* Show me the unique appearances of country_of_birth */
SELECT DISTINCT country_of_birth FROM person;
```

# `WHERE`, `OR`, `AND` clause
* The `WHERE` clause allows us to select data based on conditions.
```sql
/* List all Females */
SELECT * FROM person WHERE gender = 'Female';
```

* The `AND` and `OR` clause allows us to add multiple condditions.
```sql
/* List males of China and Russia */
SELECT * FROM person WHERE gender = 'Male' AND (country_of_birth = 'China' OR country_of_birth = 'Russia');
```

# Comparision Operators
* Try the following commands. Output would be `t` or `f` for either `true` or `false`.
```sql
SELECT 1 = 1;           /* Logical equals to */
SELECT 1 < 2;           /* Logical less than */
SELECT 1 >= 1;          /* Logical greater than equals to */
SELECT 1 <> 1;          /* Logical not equals to */

/* Consitions work on all data types. Example of Strings. */
SELECT 'Sam' = 'Jhon';
SELECT 'Sam = 'Sam;
```


# `LIMIT`, `OFFSET`, and `FETCH`.
* The `LIMIT` keyword allows us to limit the number of appearences to a certain number.
```sql
/* A query get the information about the first 10 males in our database*/
SELECT * FROM person WHERE gender = 'Male' LIMIT 10;
```

* `OFFSET` allows us to choose the starting point from where the data would be retrieved.
```sql
/* Get info about the first 10 males, but skip the first 7 males*/
SELECT * FROM person WHERE gender = 'Male' OFFSET 7 LIMIT 10;
```

* Now, `LIMIT` is not an SQL keyword by legacy standards. It was used a lot and became a thing.
* Actual keyword is `FETCH` and is used as shown below...
```sql
/* One can see why LIMIT became more popular */
SELECT * FROM person WHERE gender = 'Male' FETCH FIRST 10 ROW ONLY;
```


# The `IN` Keyword
* Take a look at this query...
```sql
SELECT * FROM person WHERE country_of_birth = 'China' OR country_of_birth = 'Brazil' or country_of_birth = 'France';
```
* This line contains a lot of boilerplate (redundant) code. Can we improve?
* The answer is yes, and the solution is the `IN` keyword.
* `IN` takes in an array of values and executes the query with each of those values.
```sql
SELECT * FROM person WHERE country_of_birth IN ('China', 'Brazil', 'France');

/* We can also use `NOT IN` to get details of people of all countries except these countries*/
SELECT * FROM person WHERE country_of_birth NOT IN ('China', 'Brazil', 'France');
```


# The `BETWEEN` Keyword
*  `BETWEEN` is used to select data in a range. See example.
```sql
/* Get id and emails of Russian Males with id between 100 and 500 */
SELECT id, email  FROM person WHERE gender = 'Male' AND country_of_birth = 'Russia' AND id BETWEEN 100 AND 500;
```


# `LIKE` and `ILIKE`
* Like is used for pattern matching with wildcards. Examples below...
```sql
/* Get the details of people whose email is of the form "some_characters + .com" */
SELECT * FROM person WHERE email LIKE '%.com';

/* Get details of people whose email is of the form "some_characters + google + some_characters" */
SELECT * FROM person WHERE email LIKE '%google%';

/* Get details of people with 4th char 's', 5th char 't', and any values of first three characters. */ 
SELECT * FROM person WHERE email LIKE '___st%';
```

* `LIKE` is case sensitive. `ILIKE` ignores case.
```sql
/* No results cuz all names start with capital letters */
SELECT * FROM person WHERE country_of_birth LIKE 'p%'; 

/* But after ignorning case with `ILIKE` we get results */
SELECT * FROM person WHERE country_of_birth ILIKE 'p%'; 
```


# Aggregate Functions
* Aggregate functions compute a single result from a set of input values.
* Let us create a new Database called `car` with mockaroo.
* Connect to the `learning` database and then run the `.sql` script from above.
```sql
/* MAX (Finding the most expensive car) */
SELECT MAX(price) FROM car;

/* MIN (Finding the lease expensive car) */
SELECT MIN(price) FROM car;

/* AVG (average) */
SELECT AVG(price) FROM car;

/* ROUND (Round off a number to 2 decimal places) */
SELECT ROUND(AVG(price), 2) FROM car;

/* sum (get sum of prices of all cars*/
SELECT SUM(price) FROM car;

/* COUNT (This function returns the number of Non NULL enteries) */
SELECT COUNT(price) FROM car WHERE make = 'Audi';

/* An example query to print the (number of cities - number of distict cities) in a DB */
SELECT COUNT(city) - COUNT(DISTINCT city) FROM station_db;
```
* Some more functions are `FLOOR()`, `CEIL()`, `ABS()`.


# REPLACE
* This attribute can be used to replace all occourances of a substring with a different string.
```sql
/* Outputs `HTML Tutorial` */
SELECT REPLACE("SQL Tutorial", "SQL", "HTML");

/* https://www.hackerrank.com/challenges/the-blunder/problem */
```

# GROUP BY
* `GROUP BY` is a clause in SQL that is only used with aggregate functions.
* It is used in collaboration with the `SELECT` statement to arrange identical data into groups.
```sql
/* list number of people in each country */
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth;

/* Order these by country */
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth ORDER BY country_of_birth;

/* Here's a test query to list the minimum price car by each company*/
SELECT make, MIN(price) FROM car GROUP BY make;
```


# HAVING
* `HAVING` works with `GROUP BY` and allows us to add an extra filter after we perform aggrigation.
* `HAVING` should always be just after `GROUP BY`.
```sql
/* list number of people in each all country where population sample > 5 people */
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) > 5 ORDER BY country_of_birth;
```


# Operators
* SQL also allows basic mathematical operations.
* Some operations are `+`, `-`, `/`, `*`, `^` (power), `!` (Factorial), `%` (modulo).
```sql
/* Run a query to return original price + 10% discounted price */
SELECT price, ROUND(0.1 * price, 2), ROUND(price - (0.1 * price), 2) FROM car;
```


# AS
* In the last query, column names for calculations are `round`.
* By default postgres gives us the function name or `?column?`.
* `AS` is used to overwrite a name.
```sql
/* Run a query to return original price + 10% discounted price */
SELECT price AS original_price, ROUND(0.1 * price, 2) AS discount, ROUND(price - (0.1 * price), 2) AS final_price FROM car;
```


# COALESCE
* `COALESCE` allows us to have a default value in-case a value is not present.
```sql
SELECT COALESCE(email, 'EMAIL NOT PROVIDED') FROM person;
```


# NULLIF
* This keyword takes in two arguments and returns `NULL` if the first argument is the same as the second argument, else it returns the first argument.
* This can be used to tackle division by zero in postgres, to avoid an error throw.
```sql
/* POSTGRES throws an error for something like `10 / 0` but does not
throw an error for `10 / NULL`. This is simply equal to `NULL` itself. 

Thus we can do something like... */
SELECT 10 / NULLIF(num, 0);             /* where `num` is the number we actually care about */
```


# Timestamps and dates
```sql
/* Setting the timezone */
SET timezone = 'Asia/Kolkata';

/* A complete timestamp with timezone */
SELECT NOW();

/* Selecting date from timestamp */
SELECT NOW()::DATE;

/* Selecting time from timestamp */
SELECT NOW()::TIME;
```


# Date arithmetic
```sql
SELECT NOW() + INTERVAL '10 years'; /* or '10 year' works as well */
SELECT NOW() - INTERVAL '10 months';
SELECT NOW() - INTERVAL '10 days';
SELECT NOW() + INTERVAL '10 hours';
SELECT NOW() - INTERVAL '10 minutes';
SELECT NOW() - INTERVAL '10 second';
SELECT NOW() - INTERVAL '10 millisecond';

(SELECT NOW() + INTERVAL '10 months')::DATE; /* To get the date only */
```


# Extracting fields
* This keyword can be used to extract certain
```sql
SELECT EXTRACT (YEAR FROM NOW());
/* fields allowed...
YEAR, MONTH, DOW (day of the week), CENTURY, etc. */
```


# AGE
* `AGE` is a function that, as the name suggests, can be used to calculate the age of something or someone.
```sql
SELECT first_name, last_name, AGE(NOW(), date_of_birth) FROM person;
```


# ALTERING a table.
```sql
/* let us drop the `PRIMARY KEY` constraint from `id`*/
ALTER TABLE person DROP CONSTRAINT person_pkey;

/* Re-insert the constraint. */
ALTER TABLE person ADD PRIMARY KEY (id); /* Accepts multiple column names if composite key is required*/

/* Another exaple of adding constraint */
ALTER TABLE person ADD CONSTRAINT gender_constraint CHECK (gender = 'Female' OR gender = 'Male');

/*Add another column to the table*/
ALTER TABLE person ADD age INTEGER;

/*Drop a specific column*/
ALTER TABLE person DROP age;
```


# Deleting records (rows of database)
* The best parameter to delete by is the primary key because it is unique for each row.
```sql
DELETE FROM person WHERE id = 23
DELETE FROM person WHERE gender = 'Male' and country_of_birth = 'China'; 
```


# Updating records
```sql
UPDATE person SET email = 'sudeepam@gmail.com' WHERE first_name = 'Sudeepam';
UPDATE person SET last_name = 'P', email = 'sudeepam.pandey@gmail.com' WHERE first_name = 'Sudeepam';
```


# Table Relations
* Let us first take a quick look at the two tables that we had created...
```sql
CREATE TABLE person (
	id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	gender VARCHAR(50) NOT NULL,
	date_of_birth DATE NOT NULL,
	country_of_birth VARCHAR(50) NOT NULL,
	email VARCHAR(50)
);

CREATE TABLE car (
	id SERIAL PRIMARY KEY,
	make VARCHAR(50) NOT NULL,
	model VARCHAR(50) NOT NULL,
	price NUMERIC(10, 2) NOT NULL
);
```
* Say we want to link a car to a person, such that 'a car could belong to one person only'
* To do this, we can write something like this...
```sql
/* `UNIQUE` makes sure that the car could belong to only one person */
/* `NOT NULL` constraint has not been applied, hence a person may or may not have a car */
car_id INTEGER REFERENCES car(id) UNIQUE
```

# Updating Foreign Key Columns
* For further exercises execute `joins.sql`. Do take a look at the file.
* Try running `SELECT * FROM person` and `SELCT * FROM table`.
```sql
/* Now let us assign the two cars to two of the three people */
UPDATE person SET car_id = 2 WHERE id = 1;
UPDATE person SET car_id = 1 WHERE id = 3;
```


# JOINS
* Joins are used to combine two tables.
* We specify a condition on which the tables have to be joined, and depending upon the type of join, certain records are returned.

## Inner Join
* The inner join retrieves the records that have matching values in both the tables involved in the join.
* Inner Join is essentially equal to (A intersection B).
```sql
/* breaking down the query for redability */
SELECT * FROM
person INNER JOIN car             /* Select from the 'Join' or combined `person` and `car` table */
ON person.car_id = car.id;        /* The columns for which the values must match */

/* We can also write JOIN instead of INNER JOIN
```

## Left Join
* The left join retrieves all records from the first (or the left) table but only the matching records from the second (or the right table).
```sql
SELECT * FROM person LEFT JOIN car ON person.car_id = car.id;
```

## Right Join
* The Right join retrieves all records from the second (or the right) table but only the matching records from the first (or the left table).
```sql
SELECT * FROM person LEFT JOIN car ON person.car_id = car.id;
```

## IS NULL
* Used to get missing values in a column.
* We also have a `IS NOT NULL`.
```sql
SELECT first_name, last_name FROM person WHERE email IS NULL;
SELECT first_name, last_name FROM person WHERE email IS NOT NULL;
```

## CASE
* If-else in SQL.
```sql
/* General */
SELECT column_name,
  CASE
    WHEN condition THEN 'Result_1'
    WHEN condition THEN 'Result_2'
    ELSE 'Result_3'
  END
FROM table_name;

/* https://www.hackerrank.com/challenges/what-type-of-triangle/problem */
SELECT
    CASE
        WHEN A + B <= C OR B + C <= A OR A + C <= B THEN 'Not A Triangle' /* ideally we should remove `=` but cases are wrong */
        WHEN A != B AND B != C AND C != A THEN 'Scalene'
        WHEN A = B AND B = C THEN 'Equilateral'
        WHEN A = B OR B = C OR C = A THEN 'Isosceles'
    END
FROM TRIANGLES;
```

## Arithmetic
```sql
/* returns the cities whose id is an even number */
SELECT DISTINCT city FROM station_db WHERE ID % 2 = 0;
```

## SUBSTRING 
* Can be used to extract a substring from a varchar entry.
* Note that SQL strings are 1 indexed.
* SUBSTRING and SUBSTR work the same way.
```sql
/* get all distinct cities whose names start with vowels*/
SELECT DISTINCT city FROM station WHERE SUBSTRING(LOWER(city), 1, 1) IN ('a', 'e', 'i', 'o', 'u');

/* get all distinct cities whose names end in vowels */
SELECT DISTINCT city FROM station WHERE SUBSTRING(LOWER(city), -1, 1) IN ('a', 'e', 'i', 'o', 'u');
```

## Regular Expressions
* An article on how to write regular expressions can be found [here](https://www.geeksforgeeks.org/write-regular-expressions/). 
```sql
/* get all distinct cities whose names start with vowels using regex*/
SELECT DISTINCT city FROM station WHERE city REGEXP "^[aeiou].*";

/* ends with */
SELECT DISTINCT city FROM station WHERE city REGEXP "[aeiou]$";
```
