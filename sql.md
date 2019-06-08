# DBMS
* Database Management Systems are used to interact with a database.
* The DBMS can create, read, update, and delete (C.R.U.D.) the contents of a database.
* Relational databases use SQL and organize the data into one or more tables. Each table has columns and 
  rows, and a unique key identifies each row.
* Non Relational databases (NoSQL or Not just SQL) organize data in anything but a traditional table.
  Examples are: Graphs, documents like JSON, Key-Valie Pairs etc.
* SQL or Structured Query Language is a **standardized** language for interacting with Relational DBMS (RDBMS).
  So for example, SQLite and MySQL are two different RDBMS and to interact with either of them, we use this
  standardized language called SQL. However, not all RDBMS follow SQL in an exactly similar fashion.
* Primary Key is an attribute that uniquely defines a row in a database.
* Primary Key can be natural or surrogate. Surrogate Key has no mapping to the real world.
* A primary key may consist of a combination of 2 or more column values, in such a case it is called a Composite Key.
* Individual columns of a Composite Key may be same across rows but the combinations would be different for each row. 
* A Foreign Key in a database table, stores the Primary Key of a row of another table.
* We can create relations between various tables using Foreign Keys.

# Creating a Database

```sql
/*Create a database*/
CREATE DATABASE learning;

/*Check all available databases*/
SHOW DATABASES;

/*Select our new database*/
USE learning;
```

# Creating a Table

```sql
/*Creating a Table*/
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY,
    name VARCHAR(30),
    major VARCHAR(30)
);

/*To check if the table is created (or altered) correctly*/
DESCRIBE student;
```

# Inserting Data into a Table
* Now that we have our student table we will start inserting some data into it.
* Our table is of the form ...

| student_id |  name  | major |
| :--------: |  :--:  | :---: |
| Roll_num_1 |  name1 |  ECE  |
| Roll_num_1 |  name2 |  CSE  |

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

# Droping columns from a table.

```sql
/*Add another column to the table*/
ALTER TABLE student ADD gpa DECIMAL(3, 2); /* 3 total digits and 2 are after decimal point*/
DESCRIBE student;

/*Drop a specific column*/
ALTER TABLE student DROP COLUMN gpa;
DESCRIBE student;
```

# Constraints

* Now, we define the table again, by using some `constraints`.
* Constraints allow us to make the table more error proof and makes it easier for us to insert data correctly into the table.
* Say, some columns of our table should not have an empty value. We can impose this restriction on our tables with `NOT NULL`.
* We can also use a constraint like `UNIQUE` to make sure some columns have different value for each row.
* The difference between a UNIQUE and primary key is that PK is both NOT NULL and UNIQUE.


```sql
USE learning;
DROP TABLE student;

CREATE TABLE student (
    student_id INTEGER,
    name VARCHAR(30) NOT NULL,  /* Demonstration of NOT NULL*/
    major VARCHAR(30) UNIQUE    /* Demonstration of UNIQUE*/
    PRIMARY KEY (student_id)
);

/* Inserts fine*/
INSERT INTO student VALUES(1, 'Jack', 'Biology');

/* Error occours since name is null*/
INSERT INTO student(student_id, major) VALUES(3, 'English');
INSERT INTO student VALUES(3, NULL, 'Chemistry');

/* Error since major is not unique*/
INSERT INTO student VALUES(4, 'Jack', 'Biology');
```

* The `DEFAULT` constraint lets us set a default value for a column.
* `AUTO_INCREMENT is useful when working with primary keys, if primary keys are simple serial numbers (say), we won't need to manually pass them if we are using this command. Obviously this constraint can be used for non PRIMARY_KEY columns as well.

```sql
USE learning;
DROP TABLE student;

CREATE TABLE student (
    student_id INTEGER PRIMARY KEY AUTO_INCREMENT,
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
