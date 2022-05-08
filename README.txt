SQL NOTES

Module 1:

    - history and overview of databases
    - what is a database? 
    - types of databases
    - SQL vs. NoSQL ---> (relational vs. non-relational)
    - RDBMS ---> relational database management system
    - SQL ---> Structured Query Language (uses tables with rows and columns)
    - MongoDB ---> NoSQL (non-relational)
    - GraphQL ---> alternative database technology to REST API
    - Tables: rows and columns or (fields)
        - datatypes for columns
        - common column datatypes ---> integer, charachter, array, varchar, boolean


datatypes:
    - tinyint
    - bigint
    - int
    - varchar
    - character varying (string)




// SQL SHELL COMMANDS

// ***************************
//  DAY 1 CONTENT
// ***************************

// 1. Show a List of Databases
// \l

// 2. Create a New Database
// CREATE DATABASE pet_info;

// 3. Remove a Database
// (use pd Admin 4 to delete a database)

// 4. Connect Into a Specific Database
// \c pet_info;

// 5. Create a Table with Columns
// CREATE TABLE pets(pet_id int, pet_type varchar(25), pet_name varchar(25), pet_age int);

// 6. Check that the table was created
// \d pets

// 7. Delete a Table
// DROP TABLE pets;

// 8. Insert Data into a Database
// *** basic syntax ***
// INSERT INTO table_name (column_1, column_2) VALUES (value_1, value_2);

// *** example ***
// INSERT INTO pets (pet_id, pet_type, pet_name, pet_age) VALUES (1, 'Dog', 'Tuxedo', 8), (2, 'Cat', 'Olivia', 3), (3, 'Bunny', 'Rainbow', 1);

// 9. Read Specific Data in a Database
// *** basic syntax ***
// SELECT column_name FROM table_name;

// *** example ***
// SELECT pet_name FROM pets;

// 10. Read All Data in a Database
// SELECT * FROM pets;

// 11. Filter to Read Specific Data in a Database
// *** the WHERE clause allows us to filter the query to be more specific ***
// SELECT pet_name FROM pets WHERE pet_age = 8;

// 12. Filter to Read Specific Data in a Database with AND, OR, NOT
// SELECT pet_name FROM pets WHERE pet_type = 'Cat' AND pet_id = 2;
// SELECT pet_name FROM pets WHERE pet_type = 'Bunny' OR pet_age = '5';
// SELECT pet_name FROM pets WHERE NOT pet_type = 'Cat';

// 13. Filter to Read Specific Data in a Database with LIKE
// *** The LIKE operator is used in a WHERE clause to search for a pattern in a column. Here is more information about the LIKE operator ***
// SELECT * FROM pets WHERE pet_name LIKE '_o%';
// *** in the above example, this selects records where the pet names have 'o' in the second position ***

// 14. Update data in a Database
// *** basic syntax ***
// UPDATE table_name SET column_1 = value_1 WHERE column_1 = value_2;

// *** example ***
// UPDATE pets SET pet_name='JimmerJam' WHERE pet_name='Tuxedo';

// 15. Delete Data in a Database
// *** basic syntax ***
// DELETE FROM table_name WHERE column_1 = value_1;

// *** example ***
// DELETE FROM pets WHERE pet_name = 'JimmerJam';


SQL Joins
    Data may be needed from several tables

    * A SQL Join is a clause that combines data from multiple tables.
        - left join; returns all records from the left (first) table and the matched records from the right (second) table.
        - right join; returns all rows from the table only matching  rows from the table in the FROM clause.
        - inner join; combines only common tables data;
            (selects records that have matching values in both tables)
        - outer join; combines all tables database  
            (returns unmatched rows from both tables.)

* set theory *

Subquery

Union ---> allows us to combine the results of two or more SELECT queries

Aggregate functions
    - AVG
    - COUNT
    - MAX
    - MIN
    - SUM



Answers to questions of aggregate functions activity: Practice with Aggregate Functions

SELECT COUNT(title) FROM film;
SELECT * FROM film;
Select * from information_schema.columns WHERE TABLE_NAME = 'film'; /* DESC outside of postgres */
Select * from information_schema.columns WHERE TABLE_NAME = 'film_category'; /* DESC outside of postgres */
SELECT * FROM film WHERE rating = 'G';	
SELECT SUM(rental_duration) FROM film;
SELECT SUM(LENGTH) FROM film WHERE rating = 'R';
SELECT AVG(LENGTH) FROM film;
SELECT AVG(replacement_cost) FROM film WHERE rating = 'G';
SELECT MIN(replacement_cost), title FROM film GROUP BY title;
SELECT MIN(LENGTH) FROM film;
SELECT MIN(rental_rate), title FROM film;
SELECT max(LENGTH), title FROM film GROUP BY title;
SELECT MAX(replacement_cost), title FROM film GROUP BY title;

    data outcome answer:
    COUNT
        - 1,000 - SELECT COUNT (title) FROM film;
        - 178 - SELECT COUNT (title) FROM film WHERE rating = 'G';
    SUM
        - 4,985 - SELECT SUM (rental_duration) FROM film; 
        - 931 - SELECT SUM (rental_duration) FROM film WHERE rating = 'R';
    AVG
        - 115.272 - SELECT AVG (length) FROM film;
        - 20.124831 - SELECT AVG (replacement_cost) FROM film WHERE rating = 'G';
    MIN
        - 9.99 (NOTORIUS UNION, WAIT CIDER, LIFE TWISTED...)
            ^ SELECT MIN(replacement_cost), title FROM film GROUP BY title;
        - 46 (IRON MOON)
            ^ SELECT MAX(length), title FROM film GROUP BY title; 
        - $0.99
            ^ SELECT MIN (rental_rate) FROM film WHERE rating = 'R';
    MAX
        - 185 (CHICAGO NORTH, CONTROL ANTHEM, DARN FORRESTER ...)
            ^ SELECT MAX (length), title FROM film GROUP BY title;
            ^ SELECT title FROM film WHERE length = '185';
        - 53 different movies all with $29.99 replacement_cost
            ^ SELECT MAX (replacement_cost) FROM film;
            ^ SELECT title FROM film WHERE replacement_cost = '29.99';



ORM libraries
    - Sequalize;

    npm i
    npm i sequelize
    npm i pg -pg-hstore

Sequelize Models:
    model names should be singular
    table names should be plural of model names

    STRING ---> VARCHAR(25)
    STRING(100) ---> VARCHAR(100)
    TEXT ---> TEXT
    INTEGER ---> INTEGER
    DATE ---> TIMESTAMP WITH TIME ZONE


Syncing Models and Tables

Sequelize CLI and Migrations

    CLI ---> command line interface

    *Sequelize is very similar to Mongoose*

    Sequelize CLI is a npm package that has to be installed


