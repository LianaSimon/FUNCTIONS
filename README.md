# FUNCTIONS

This repository contains SQL scripts to perform various operations on a Persons table and a Country table. The operations include adding a new column, creating a user-defined function, fetching data using the function, and performing string manipulations on country names.

## Features

Add DOB Column: Adds a new DOB column to the Persons table.

Calculate Age Function: A user-defined function CalculateAge() to compute age from the date of birth.

Fetch Age of Persons: A SELECT query to retrieve the age of all persons using the function.

String Operations on Country Names:

Find the length of each country name.

Extract the first three characters of each country name.

Convert country names to uppercase and lowercase.

## Usage

To execute these queries, run them in a MySQL environment.

Run each query sequentially.

Observe the results for data transformations.

## SQL Scripts

 -- SQL ASSIGNMENT 7- (FUNCTION)
USE ENTRICLASSES;

-- Create and populate the COUNTRY2 table

CREATE TABLE COUNTRY(
    ID INT PRIMARY KEY,
    COUNTRY_NAME VARCHAR(50),
    POPULATION INT,
    AREA FLOAT
);

INSERT INTO COUNTRY(ID, COUNTRY_NAME, POPULATION, AREA)
VALUES 
(1, 'USA', 331000000, 9834000),
(2, 'India', 1400000000, 3287000),
(3, 'China', 1440000000, 9597000),
(4, 'Brazil', 213000000, 8516000),
(5, 'Russia', 146000000, 17098200),
(6, 'Japan', 126000000, 377975),
(7, 'Germany', 83000000, 357386),
(8, 'UK', 67000000, 242495),
(9, 'France', 67000000, 551695),
(10, 'Australia', 25600000, 7692024);

SELECT * FROM COUNTRY;

![image](https://github.com/user-attachments/assets/45f57977-8309-4aaa-8069-c05c31e366f0)

-- Create and populate the PERSONS table

CREATE TABLE PERSONS(
    ID INT PRIMARY KEY,
    F_NAME VARCHAR(50),
    L_NAME VARCHAR(50),
    POPULATION INT,
    RATING FLOAT,
    COUNTRY_ID INT,
    COUNTRY_NAME VARCHAR(50),
    FOREIGN KEY (COUNTRY_ID) REFERENCES COUNTRY(ID)
);

INSERT INTO PERSONS(ID, F_NAME, L_NAME, POPULATION, RATING, COUNTRY_ID, COUNTRY_NAME)
VALUES
(1, 'John', 'Doe', 5000, 4.5, 1, 'USA'),
(2, 'Jane', 'Smith', 6000, 4.7, 1, 'USA'),
(3, 'Raj', 'Kumar', 7000, 4.9, 2, 'India'),
(4, 'Wei', 'Zhang', 5500, 4.6, 3, 'China'),
(5, 'Ana', 'Silva', 5000, 4.8, 4, 'Brazil'),
(6, 'Olga', 'Ivanova', 3000, 4.3, 5, 'Russia'),
(7, 'Taro', 'Yamamoto', 2000, 4.4, 6, 'Japan'),
(8, 'Hans', 'Müller', 2500, 4.2, 7, 'Germany'),
(9, 'Emma', 'Brown', 4000, 4.5, 8, 'UK'),
(10, 'Jean', 'Dupont', 3000, 4.1, 9, 'France');

SELECT * FROM PERSONS;

![image](https://github.com/user-attachments/assets/06b19b8d-6b69-4e07-9c9f-c1a6d40efa56)


# QUERIES

## 1. Add a new column called DOB in Persons table with data type as Date.

ALTER TABLE PERSONS ADD COLUMN DOB DATE;
DESC  PERSONS;

![image](https://github.com/user-attachments/assets/0987e026-a64b-4e66-91f1-75ef914f5b7a)

## 2. Write a user-defined function to calculate age using DOB.

UPDATE PERSONS SET DOB='1998-02-02' WHERE ID=1;
UPDATE PERSONS SET DOB='2000-04-05' WHERE ID=2;
UPDATE PERSONS SET DOB='1999-04-05' WHERE ID=3;
UPDATE PERSONS SET DOB='2001-07-05' WHERE ID=4;
UPDATE PERSONS SET DOB='2006-08-08' WHERE ID=5;
UPDATE PERSONS SET DOB='2001-06-09' WHERE ID=6;
UPDATE PERSONS SET DOB='1994-07-11' WHERE ID=7;
UPDATE PERSONS SET DOB='2000-12-05' WHERE ID=8;
UPDATE PERSONS SET DOB='2005-9-10' WHERE ID=9;
UPDATE PERSONS SET DOB='1996-05-03' WHERE ID=10;

SELECT * FROM PERSONS;

![image](https://github.com/user-attachments/assets/d1ac92d6-625d-4672-9ff3-6b0757163d4f)

DELIMITER //
CREATE FUNCTION CalculateAge(dob DATE) RETURNS INT DETERMINISTIC
BEGIN
    DECLARE age INT;
    SET age = TIMESTAMPDIFF(YEAR, dob, CURDATE());
    RETURN age;
END //
DELIMITER ;

SHOW FUNCTION STATUS WHERE NAME='CALCULATEAGE';

![image](https://github.com/user-attachments/assets/6fc774a4-e1a0-4ca8-82f1-2f1e727448cd)

## 3. Write a select query to fetch the Age of all persons using the function that has been created.

SELECT ID,F_NAME,DOB,CALCULATEAGE(DOB) AS AGE FROM PERSONS;

![image](https://github.com/user-attachments/assets/5c3b8b92-3ade-42b7-9eab-ee84381b7859)

## 4. Find the length of each country name in the Country table.

SELECT ID,COUNTRY_NAME,LENGTH(COUNTRY_NAME) AS "COUNTRY-NAME LENGTH" FROM COUNTRY;

![image](https://github.com/user-attachments/assets/1bb948dc-e3f5-4963-84e2-36e905348c30)

## 5. Extract the first three characters of each country's name in the Country table.

SELECT ID,COUNTRY_NAME,LEFT(COUNTRY_NAME,3) AS "FIRST 3 CHARACTERS OF COUNTRY-NAME" FROM COUNTRY;

![image](https://github.com/user-attachments/assets/0ff00841-14ed-49bb-b6d1-e9b1c6fcca23)

## 6. Convert all country names to uppercase and lowercase in the Country table.

SELECT ID,COUNTRY_NAME,UPPER(COUNTRY_NAME) AS "COUNTRY-NAME IN UPPERCASE",LOWER(COUNTRY_NAME) AS "COUNTRY-NAME IN LOWER CASE" FROM COUNTRY;

![image](https://github.com/user-attachments/assets/5a3333e9-c79e-42a4-9455-40b5fad0ded4)



# Author

Developed by Liana Simon.













