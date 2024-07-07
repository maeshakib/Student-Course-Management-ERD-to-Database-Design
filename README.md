# Student-Course-Management-ERD-to-Database-Design
## Entity Relationship Diagram (ERD) to Relational Model(RM)
<img align="left" alt="covid 19 vacciantion timeline" width="1000px" src="https://github.com/maeshakib/Student-Course-Management-ERD-to-Database-Design/blob/main/student-course-erd.png" /> <br>
                                  **Fig 1: Entity Relation Conceptual Schema**
                                  
From the above ER diagram, draw the Relational models by explaining each step

***Step One: Step 1: Mapping of Regular Entity Types*** 

Following are all regular entity identified from Fig 1 Entity relation schema. We created the relations Staff, Company, Task, Wife in Figure 2 to correspond to the regular entity types Staff, Company, Task, Wife from Figure 1

1.	STUDENT
   - STUDENT_ID(primary key)
   - DOB
   - STUDENT_NAME
   - DOOR#
   - STREET
   - CITY
2.	Student_Hobby
   - STUDENT_ID_FK
   - Hobby_name

3.	LECTURER
   - LECTURER_ID (primary key)
   - LECTURER_NAME
4.	SUBJECTS
   - LECTURER_ID (primary key)
   - SUBJECT_ID
   - SUBJECT_NAME
   - COURSE_ID_FK_IN_SUBJECT(foreign key related with course table)
5.	COURSE	
   - COURSE_ID (primary key)
   - COURSE_NAME
6.	STUDENT_ATTEND_COURSE
   - STUDENT_ID_FK (foreign key related with STUDENT table)
   - COURSE_ID_FK(foreign key related with course table)
7.	LECTURE_TAKES_COURSE
   - LECTURER_ID_FK
   - COURSE_ID_FK

***Step 2: Mapping of Weak Entity Types:***
There is not  is a week entity in this ER model. 
Step 3: Mapping of Binary 1:1 Relationship Types
   - With foreign key approach we included the primary key(LECTURER_ID) of the LECTURER relation as foreign key in the SUBJECTS relation as name LECTURER_ID in Fig 2.

***Step 4: Mapping of Binary 1 :N Relationship Types:***
   - For  1:N relationship types HAS we included the primary key COURSE_ID of the COURSE relation as foreign key in the SUBJECT relation and call it COURSE_ID_FK_IN_SUBJECT in Fig 2.

***Step 5: Mapping of Binary M:N Relationship Types:***
Attends:
   - we mapped the M:N relationship type Attends from Figure 1 by creating the relation STUDENT_ATTEND_COURSE in Figure 2
   - We also included the primary keys of the STUDENT and COURSE relations as foreign keys in STUDENT_ATTEND_COURSE and STUDENT_ID_FK and COURSE_ID_FK respectively in Fig 2.
Takes:
   - we mapped the M:N relationship type Takes from Figure 1 by creating the relation LECTURER_TAKES_COURSE in Figure 2
   - We also included the primary keys of the STUDENT and COURSE relations as foreign keys in STUDENT_ATTEND_COURSE and LECTURER_ID_FK and COURSE_ID_FK respectively in Fig 2.

***Step 6: Mapping of Multivalued Attributes***
HOBBY is multivalued attribute:
   - we created a relation Student_hobby the attribute HOBBY represents the multivalued attribute of entity STUDENT, 
   - The primary key of Student_hobby  is the combination of { STUDENT_ID, Hobby_name }. A separate tuple will exist in Student_hobby   for each hobby that a STUDENT has.
   - while STUDENT_ID -as foreign key represents the primary key of the STUDENT relation
<img align="left" alt="covid 19 vacciantion timeline" width="1000px" src="https://github.com/maeshakib/Student-Course-Management-ERD-to-Database-Design/blob/main/student-course-RM.png" /> <br>
                                **Fig 2: Result of mapping of the Fig 1 ER schema into a relational Database Schema.**

     ## 3.	Create the tables above and insert 10 row in each table

**Create the STUDENT table**

```sql
CREATE TABLE STUDENT (
    STUDENT_ID VARCHAR(50) PRIMARY KEY,
    STUDENT_NAME VARCHAR(100),
    AGE INT,
    HOBBY VARCHAR(100),
    DOB DATE,
    DOOR_NUM VARCHAR(20),
    STREET VARCHAR(100),
    CITY VARCHAR(100),
    STATE VARCHAR(100),
    PIN VARCHAR(20)
);
```
**Create the LECTURER table**

```sql
CREATE TABLE LECTURER (
    LECTURER_ID VARCHAR(50) PRIMARY KEY,
    LECTURER_NAME VARCHAR(100)
);
```
**Create the COURSE table**
```sql
CREATE TABLE COURSE (
    COURSE_ID VARCHAR(50) PRIMARY KEY,
    COURSE_NAME VARCHAR(100)
);
```
**Create the SUBJECTS table**

```sql
CREATE TABLE SUBJECTS (
    SUBJECT_ID VARCHAR(50) PRIMARY KEY,
    SUBJECT_NAME VARCHAR(100),
    LECTURER_ID VARCHAR(50),
    COURSE_ID_FK VARCHAR(50),
    FOREIGN KEY (LECTURER_ID) REFERENCES LECTURER(LECTURER_ID) ON DELETE CASCADE,
    FOREIGN KEY (COURSE_ID_FK) REFERENCES COURSE(COURSE_ID) ON DELETE CASCADE
);
```
**Create the Student_Hobby table**

```sql
CREATE TABLE Student_Hobby (
    STUDENT_ID VARCHAR(50),
    hobby_name VARCHAR(100),
    PRIMARY KEY (STUDENT_ID, hobby_name),
    FOREIGN KEY (STUDENT_ID) REFERENCES STUDENT(STUDENT_ID)
);
```
**Create the STUDENT_ATTEND_COURSE table**

```sql
CREATE TABLE STUDENT_ATTEND_COURSE (
    STUDENT_ID_FK VARCHAR(50),
    COURSE_ID_FK VARCHAR(50),
    PRIMARY KEY (STUDENT_ID_FK, COURSE_ID_FK),
    FOREIGN KEY (STUDENT_ID_FK) REFERENCES STUDENT(STUDENT_ID) ON DELETE CASCADE,
    FOREIGN KEY (COURSE_ID_FK) REFERENCES COURSE(COURSE_ID) ON DELETE CASCADE
);
```
**Create the LECTURER_TAKES_COURSE table**

```sql
CREATE TABLE LECTURER_TAKES_COURSE (
    LECTURER_ID_FK VARCHAR(50),
    COURSE_ID_FK VARCHAR(50),
    PRIMARY KEY (LECTURER_ID_FK, COURSE_ID_FK),
    FOREIGN KEY (LECTURER_ID_FK) REFERENCES LECTURER(LECTURER_ID) ON DELETE CASCADE,
    FOREIGN KEY (COURSE_ID_FK) REFERENCES COURSE(COURSE_ID) ON DELETE CASCADE
);
```
**Insert rows into the STUDENT table**

```sql
INSERT INTO STUDENT (STUDENT_ID, STUDENT_NAME, AGE, HOBBY, DOB, DOOR_NUM, STREET, CITY, STATE, PIN)
VALUES 
('S001', 'John Doe', 20, 'Reading', '2004-01-15', '123', 'Main St', 'Springfield', 'IL', '62701'),
('S002', 'Jane Smith', 22, 'Swimming', '2002-04-20', '456', 'Elm St', 'Springfield', 'IL', '62701'),
('S003', 'Alice Johnson', 21, 'Cycling', '2003-05-10', '789', 'Oak St', 'Springfield', 'IL', '62701'),
('S004', 'Bob Brown', 19, 'Hiking', '2005-02-25', '321', 'Pine St', 'Springfield', 'IL', '62701'),
('S005', 'Charlie Davis', 23, 'Running', '2001-03-30', '654', 'Maple St', 'Springfield', 'IL', '62701'),
('S006', 'Daisy Miller', 24, 'Painting', '2000-06-15', '987', 'Birch St', 'Springfield', 'IL', '62701'),
('S007', 'Edward Wilson', 20, 'Writing', '2004-08-20', '111', 'Cedar St', 'Springfield', 'IL', '62701'),
('S008', 'Fiona Clark', 22, 'Gardening', '2002-11-10', '222', 'Spruce St', 'Springfield', 'IL', '62701'),
('S009', 'George Lewis', 21, 'Fishing', '2003-09-25', '333', 'Aspen St', 'Springfield', 'IL', '62701'),
('S010', 'Hannah Walker', 19, 'Cooking', '2005-12-30', '444', 'Fir St', 'Springfield', 'IL', '62701');
```
**Insert rows into the LECTURER table**

```sql
INSERT INTO LECTURER (LECTURER_ID, LECTURER_NAME)
VALUES 
('L001', 'Dr. Smith'),
('L002', 'Dr. Johnson'),
('L003', 'Dr. Brown'),
('L004', 'Dr. Davis'),
('L005', 'Dr. Miller'),
('L006', 'Dr. Wilson'),
('L007', 'Dr. Clark'),
('L008', 'Dr. Lewis'),
('L009', 'Dr. Walker'),
('L010', 'Dr. Hall');
```
**Insert rows into the COURSE table**

```sql
INSERT INTO COURSE (COURSE_ID, COURSE_NAME)
VALUES 
('C001', 'Mathematics'),
('C002', 'Physics'),
('C003', 'Chemistry'),
('C004', 'Biology'),
('C005', 'Computer Science'),
('C006', 'English'),
('C007', 'History'),
('C008', 'Geography'),
('C009', 'Art'),
('C010', 'Music'),
('C011', 'Philosophy');
```
**Insert rows into the SUBJECTS table**

```sql
INSERT INTO SUBJECTS (SUBJECT_ID, SUBJECT_NAME, LECTURER_ID, COURSE_ID_FK)
VALUES 
('SUB001', 'Algebra', 'L001', 'C001'),
('SUB002', 'Calculus', 'L001', 'C001'),
('SUB003', 'Mechanics', 'L002', 'C002'),
('SUB004', 'Thermodynamics', 'L002', 'C002'),
('SUB005', 'Organic Chemistry', 'L003', 'C003'),
('SUB006', 'Inorganic Chemistry', 'L003', 'C003'),
('SUB007', 'Botany', 'L004', 'C004'),
('SUB008', 'Zoology', 'L004', 'C004'),
('SUB009', 'Programming', 'L005', 'C005'),
('SUB010', 'Data Structures', 'L005', 'C005'),
('SUB011', 'Literature', 'L006', 'C006');
```
**Insert rows into the Student_Hobby table**

```sql
INSERT INTO Student_Hobby (STUDENT_ID, hobby_name)
VALUES 
('S001', 'Reading'),
('S001', 'Writing'),
('S001', 'Swimming'),
('S001', 'Cycling'),
('S003', 'Hiking'),
('S003', 'Running'),
('S004', 'Hiking'),
('S004', 'Running'),
('S005', 'Running'),
('S006', 'Painting'),
('S006', 'Gardening'),
('S007', 'Writing'),
('S007', 'Cooking'),
('S008', 'Gardening'),
('S008', 'Fishing'),
('S009', 'Fishing'),
('S010', 'Cooking'),
('S010', 'Reading');
```
**Insert rows into the STUDENT_ATTEND_COURSE table**

```sql
INSERT INTO STUDENT_ATTEND_COURSE (STUDENT_ID_FK, COURSE_ID_FK)
VALUES 
('S001', 'C001'),
('S001', 'C005'),
('S001', 'C011'),
('S001', 'C002'),
('S002', 'C003'),
('S003', 'C003'),
('S003', 'C004'),
('S004', 'C004'),
('S004', 'C001'),
('S005', 'C005'),
('S005', 'C006'),
('S006', 'C006'),
('S006', 'C007'),
('S007', 'C007'),
('S007', 'C008'),
('S008', 'C008'),
('S008', 'C009'),
('S009', 'C009'),
('S009', 'C010'),
('S010', 'C010'),
('S010', 'C001'),
('S010', 'C002');
```
**Insert rows into the LECTURER_TAKES_COURSE table**

```sql
INSERT INTO LECTURER_TAKES_COURSE (LECTURER_ID_FK, COURSE_ID_FK)
VALUES 
('L001', 'C001'),
('L001', 'C005'),
('L001', 'C011'),
('L002', 'C002'),
('L002', 'C003'),
('L003', 'C003'),
('L003', 'C004'),
('L004', 'C004'),
('L004', 'C001'),
('L005', 'C005'),
('L005', 'C006'),
('L006', 'C006'),
('L006', 'C007'),
('L007', 'C007'),
('L007', 'C008'),
('L008', 'C008'),
('L008', 'C009'),
('L009', 'C009'),
('L009', 'C010'),
('L010', 'C010'),
('L010', 'C001'),
('L010', 'C011');
```
