# Answers
1 - Look at the `departments` table in the `school` database provided to you. How many columns does it have and what are the column names?
```sql
// TWO Columns
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL
```
2 -   Which column in the  `departments`  table is intended to be uniquely identifying?
```sql
  id INTEGER PRIMARY KEY
```
3 - Look at the `teachers` schema. Which column is being used as a foreign key? Why might we be using a foreign key here rather than storing the data directly in this table? Review the last paragraph if you are unclear.
```sql
  department INTEGER
  // We don't want to have data redudency or **inconsistency**
```
4 - Look at the remaining table schemas in this database. Whiteboard each of the 5 tables, representing them as simple spreadsheet like grids, using arrows to indicate where a particular column is referring to data stored in another table.

5 - Display the `name` column for every row in the `students` table
```sql
  sqlite> SELECT * FROM STUDENTS;
    lauren
    dan
    naomi
    kim
    sam
    chris
```
6 - Display every column for the `teachers` table. The `department` column just contains numbers, what are these numbers referencing? (Look at the `teachers` schema if you need to).

 ```sql
  sqlite> SELECT * FROM TEACHERS ;
    1|fred|1
    2|pamela|2
    3|beth|1
    4|sunny|2
```
it refers to the department ID

7 - Display every column for the `teachers` table and then every column for the `departments` table. Just by looking at the tables, what is the name of the department that the teacher `beth` is a part of?

    CS

8 - Display just the name column for all the students whose names are not naomi. (Note, `naomi` being text, should be placed in single quotes)

```sql
  sqlite> SELECT NAME  FROM STUDENTS WHERE NAME != 'naomi';
   lauren
   dan
   kim
   sam
   chris
```

9 - Display the name and department id of teachers whose own id is greater than 2 or whose name is 'fred'
```SQL
sqlite> SELECT NAME, DEPARTMENT FROM TEACHERS WHERE ID > 2 OR NAME = 'fred';
fred|1
beth|1
sunny|2
```
10 -   Display the id and name of all the students whose names end in 'm'?
```sql
sqlite> SELECT ID, NAME FROM STUDENTS WHERE NAME LIKE '%m';
4|kim
5|sam
```
11 -   Display all columns for students whose names do not contain the letter 'a'.
**HINT**: a more long-winded way to say "includes the letter 'a'" is "includes 0 or more of any letter followed by an 'a' followed by 0 or more of any letter."

```sql
sqlite> SELECT NAME FROM STUDENTS WHERE NAME NOT LIKE '%a%';
kim
chris
sqlite>
```
12 -   Display just the names of all the teachers whose id is  `NOT`  either 1, 2, or 4.
```sql
sqlite> SELECT NAME FROM TEACHERS WHERE ID NOT IN (1,2,4);
beth
```
13 -   Display just the names of all the teachers whose department is either 1 or 4.
```SQL
sqlite> SELECT NAME FROM TEACHERS WHERE DEPARTMENT IN (1,4);
fred
beth
```
14 - Display the name and id of all the teachers in the 'psy' department (should be pamela and sunny, with their respective ids).
```sQL
sqlite> SELECT NAME, ID FROM TEACHERS WHERE DEPARTMENT = (SELECT ID FROM DEPARTMENTS WHERE NAME = 'psy');
pamela|2
sunny|4
```
15 - Display the name of the department that 'sunny' teaches for (should be 'psy').
```SQL
sqlite> SELECT NAME FROM DEPARTMENTS  WHERE ID = (SELECT DEPARTMENT FROM  TEACHERS WHERE NAME = 'sunny');
psy
```
16 - Use the same thought process from above to make a prediction about what the following queries will return. How many columns will there be? How many rows will there be? Run each of the queries to check your work.

-   `SELECT departments.id, classes.id FROM departments, classes;`
-   `SELECT students.*, teachers.name FROM students, teachers;`

17 - Display the name and id of all the teachers in the 'psy' department (should be pamela and sunny, with their respective ids).
```SQL
sqlite> SELECT TEACHERS.NAME, TEACHERS.ID FROM TEACHERS, DEPARTMENTS AS D WHERE TEACHERS.DEPARTMENT = D.ID AND D.NAME = 'psy';
pamela|2
sunny|4
```
18 -   Display the name of the department that 'sunny' teaches for (should be 'psy').
```SQL
sqlite> SELECT D.NAME FROM DEPARTMENTS AS D, TEACHERS AS T WHERE T.NAME = 'sunny' AND D.ID = T.DEPARTMENT;
psy
```
19 - What is the difference between the return from the following two statements:

```SQL
  SELECT * FROM students, teachers;
  SELECT * FROM students INNER JOIN teachers;
 // NADA
```
20 - Display the name and id of all the teachers in the 'psy' department (should be pamela and sunny, with their respective ids).
```sql
sqlite> SELECT TEACHERS.NAME, TEACHERS.ID FROM TEACHERS INNER JOIN DEPARTMENTS ON DEPARTMENTS.ID = TEACHERS.department AND DEPARTMENTS.name = 'psy';
pamela|2
sunny|4
```
21 - Display the name of the department that 'sunny' teaches for (should be 'psy').
```SQL
sqlite> SELECT D.NAME FROM DEPARTMENTS AS D INNER JOIN TEACHERS AS T ON T.DEPARTMENT = D.ID AND T.NAME = 'sunny';
psy
```
22 - Take a look at the  `classes_students`  schema and answer the following:
-   Which classes is 'sam' taking? (confirm your answer below)
```SQL
sqlite>
SELECT C.NAME FROM CLASSES AS C INNER JOIN classes_students AS CS ON C.ID = CS.CLASSES_ID AND CS.student_id  WHERE CS.STUDENT_ID = (SELECT ID FROM STUDENTS WHERE NAME = 'sam');
communication
```
-  What are the names of the students in the 'compromise' class?
```SQL
sqlite> SELECT S.NAME FROM STUDENTS AS S INNER JOIN CLASSES_STUDENTS AS CS ON S.ID = CS.STUDENT_ID WHERE CS.CLASSES_ID = (SELECT ID FROM CLASSES WHERE NAME = 'compromise');
naomi
chris
kim
```
-  What are the names of the students taking any class in the 'cs' department?
```sql
sqlite>
SELECT DISTINCT S.NAME FROM STUDENTS AS S INNER JOIN CLASSES_STUDENTS AS CS INNER JOIN CLASSES AS C ON S.ID = CS.STUDENT_ID WHERE C.DEPARTMENT = (SELECT ID FROM DEPARTMENTS WHERE NAME = 'cs');
lauren
dan
sam
naomi
kim
chris
```