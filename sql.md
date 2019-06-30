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
* **Note**: The difference between a UNIQUE and primary key is that PK is both NOT NULL and UNIQUE.

```sql
\c learning
DROP TABLE student; /* To delete a Table */

CREATE TABLE student (
    student_id INTEGER,
    name VARCHAR(30) NOT NULL,  /* Demonstration of NOT NULL*/
    major VARCHAR(30) UNIQUE,   /* Demonstration of UNIQUE*/
    PRIMARY KEY (student_id)
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


## Get unique values with `DISTINCT`
```sql
/* Show me the unique appearances of country_of_birth */
SELECT DISTINCT country_of_birth FROM person;
```

# `WHERE`, `OR` and `AND` clause
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
```


# The `BETWEEN` Keyword
*  `BETWEEN` is used to select data in a range. See example.
```sql
/* Get id and emails of Russian Males with id between 100 and 500 */
SELECT id, email  FROM person WHERE gender = 'Male' AND country_of_birth = 'Russia' AND id BETWEEN 100 AND 500;
```


# Like and iLike
























# Updation and Deletion

* Now we play around with the update statement. We'll continue with the database from the last section.

```sql
USE learning;

SELECT * FROM student;

UPDATE student SET major = 'Bio' WHERE major = 'Biology';
UPDATE student SET major = 'Comp. Sci.' WHERE major = 'Computer Science';
UPDATE student SET major = 'Sociology' WHERE student_id = '2';
UPDATE student SET major = 'Biochemistry' WHERE major = 'Bio' OR major = 'Chemistry';
UPDATE student SET name = 'Tom', major = 'undecided' WHERE student_id = 1;

SELECT * FROM student;

/* Now we try some deletion */
DELETE FROM student WHERE student_id = 5;
DELETE FROM student WHERE major = 'Biochemistry' AND name = 'Claire';
```
**Note**: We can drop the `WHERE` and the conditions will be applied to every student */



# Droping columns from a table.

```sql
/*Add another column to the table*/
ALTER TABLE student ADD gpa DECIMAL(3, 2); /* 3 total digits and 2 are after decimal point*/
DESCRIBE student;

/*Drop a specific column*/
ALTER TABLE student DROP COLUMN gpa;
DESCRIBE student;
```
