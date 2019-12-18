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
