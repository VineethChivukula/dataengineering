# Keys in Database Management Systems

In DBMS, a key is a field or a set of fields that uniquely identifies a record in a table. Keys are essential for maintaining the integrity of the database and for establishing relationships between tables.

## Types of Keys

There are several types of keys in DBMS. Some of the most common types include:

1. **Primary Key:** A primary key is a field that uniquely identifies each record in a table. It must contain unique values and cannot contain null values. A table can have only one primary key. For example, in a Student table, the student ID can be a primary key.

    ```mermaid
    erDiagram
    STUDENT {
            int student_id PK
            string student_name
            string student_email
            date enrolled_on
        }
    ```

2. **Foreign Key:** A foreign key is a field that is used to establish a link between two tables. It is a field in one table that refers to the primary key in another table. For example, a Student table may have a foreign key that references the primary key of a Course table to indicate which course a student is enrolled in.

    ```mermaid
    erDiagram
    STUDENT {
            int student_id PK
            int course_id FK
            string student_name
            string student_email
            date enrolled_on
        }
    COURSE {
            int course_id PK
            string course_name
            string course_code
        }

    STUDENT ||--|{ COURSE : "enrolled in"
    ```

3. **Composite Key:** A composite key is a combination of two or more fields that together uniquely identify a record in a table. For example, in the Student table above, if we want to ensure that a student can only enroll in a course once, we can use a composite key consisting of the student_id and course_id.

4. **Candidate Key:** The minimal set of fields that can uniquely identify a record in a table is called a candidate key. A table can have multiple candidate keys, but only one of them can be chosen as the primary key. For example, in the Student table above, both student_id and student_email could be candidate keys, but only one of them can be selected as the primary key.

5. **Alternate Key:** An alternate key is a candidate key that is not selected as the primary key. It can still be used to uniquely identify records in the table. For example, if student_id is chosen as the primary key, then student_email can be considered an alternate key.

6. **Super Key:** A super key is a set of one or more fields that can uniquely identify a record in a table. It may contain additional fields that are not necessary for unique identification. For example, in the Student table, a super key could be the combination of student_id and student_name, even though student_id alone is sufficient to uniquely identify a record.
