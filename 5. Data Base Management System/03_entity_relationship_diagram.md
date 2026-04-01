# Entity-Relationship (ER) Diagram

An Entity-Relationship (ER) Diagram is a visual representation of the entities within a system and the relationships between those entities. It is commonly used in database design to illustrate the structure of a database and how different entities interact with each other.

## Components of an ER Diagram

There are few components in an ER Diagram, and we will discuss each of them in detail.

### Entities

An entity is a real-world object, concept or a thing about which the data can be stored. The tables in a database represent entities. For example, in a university database, entities could be "Student", "Course", "Book" etc.
An entity is represented by a rectangle in an ER diagram.

![Entity Representation](images/entity.png)

An Entity Set is a collection of similar types of entities. For example, all the students in a university can be considered as an entity set.

There are two types of entities:

1. **Strong Entity:** A strong entity is an entity that can exist independently of other entities. It has a primary key that uniquely identifies each instance of the entity. For example, a "Student" entity can be considered a strong entity because it can exist independently and has a unique identifier (e.g., student ID).

2. **Weak Entity:** A weak entity is an entity that cannot exist independently and relies on a strong entity for its existence. It does not have a primary key of its own and is identified by a combination of its attributes and the primary key of the strong entity it depends on. For example, a "Course Enrollment" entity can be considered a weak entity because it cannot exist without the "Student" entity and is identified by the combination of the student ID and course ID.

In order to differentiate between strong and weak entities in an ER diagram, we use different notations. A strong entity is represented by a rectangle with a single border, while a weak entity is represented by a rectangle with a double border.

![Entity Types Representation](images/entity_types.png)

### Attributes

Attributes are the properties or characteristics of an entity. They provide more information about the entity and help to describe it in more detail. For example, for a "Student" entity, attributes could include "Student ID", "Name", "Roll No", "Age", "Major" etc. An attribute is represented by an oval in an ER diagram.

![Attribute Representation](images/attribute.png)

There are four types of attributes:

1. **Simple Attribute:** A simple attribute is an attribute that cannot be further divided into smaller parts. For example, "Email" is a simple attribute because it cannot be broken down into smaller components.
2. **Composite Attribute:** A composite attribute is an attribute that can be divided into smaller sub-parts. For example, "Name" can be considered a composite attribute because it can be broken down into "First Name" and "Last Name".
3. **Derived Attribute:** A derived attribute is an attribute that can be derived from other attributes. For example, "Age" can be considered a derived attribute because it can be calculated from the "Date of Birth" attribute.
4. **Multivalued Attribute:** A multivalued attribute is an attribute that can have multiple values for a single entity. For example, "Phone Number" can be considered a multivalued attribute because a person can have multiple phone numbers.
5. **Key Attribute:** A key attribute is an attribute that uniquely identifies an entity within an entity set. For example, "Student ID" can be considered a key attribute because it uniquely identifies each student in the "Student" entity set.

In order to differentiate between simple, composite, derived, and multivalued attributes in an ER diagram, we use different notations. A simple attribute is represented by a single oval, a composite attribute is represented by an oval with sub-ovals, a derived attribute is represented by a dashed oval, and a multivalued attribute is represented by a double oval, while a key attribute is represented by an oval with an underline.

![Attribute Types Representation](images/attribute_types.png)

### Relationships

A relationship is an association between two or more entities. It represents how entities are related to each other in the real world. For example, in a university database, a "Student" entity may have a relationship with a "Course" entity through an "Enrollment" relationship, which indicates that a student is enrolled in a course. A relationship is represented by a diamond shape in an ER diagram.

![Relationship Representation](images/relationship.png)

A relationship set is a collection of similar types of relationships. For example, all the enrollments between students and courses can be considered as a relationship set.

Okay, there are two concepts related to relationships that we need to understand i.e., Degree and Cardinality.

#### Degree of a Relationship

The degree of a relationship refers to the number of entities that are involved in the relationship. There are four types of relationships based on their degree:

1. **Unary Relationship:** A unary relationship is a relationship that involves only one entity. For example, in a university database, a "Student" entity may have a unary relationship with itself to represent the "Advises" relationship, where a student can advise other students.
2. **Binary Relationship:** A binary relationship is a relationship that involves two entities. For example, in a university database, a "Student" entity may have a binary relationship with a "Course" entity through an "Enrollment" relationship, which indicates that a student is enrolled in a course.
3. **Ternary Relationship:** A ternary relationship is a relationship that involves three entities. For example, in a university database, a "Student" entity may have a ternary relationship with a "Course" entity and a "Professor" entity through a "Teaches" relationship, which indicates that a professor teaches a course to students.
4. **N-ary Relationship:** An n-ary relationship is a relationship that involves more than three entities. For example, in a university database, a "Student" entity may have an n-ary relationship with a "Course" entity, a "Professor" entity, and a "Department" entity through a "Teaches" relationship, which indicates that a professor teaches a course to students in a specific department.

![Relationship Degree Representation](images/relationship_degree.png)

#### Cardinality of a Relationship

The cardinality of a relationship refers to the number of instances of one entity that can be associated with instances of another entity in a relationship. There are three types of cardinality:

1. **One-to-One (1:1):** In a one-to-one relationship, each instance of one entity is associated with at most one instance of another entity, and vice versa. For example, in a government database, a "Citizen" entity may have a one-to-one relationship with a "Passport" entity, where each citizen can have at most one passport, and each passport can be associated with at most one citizen.
2. **One-to-Many (1:N):** In a one-to-many relationship, each instance of one entity can be associated with multiple instances of another entity, but each instance of the other entity can be associated with at most one instance of the first entity. For example, in a library database, an "Author" entity may have a one-to-many relationship with a "Book" entity, where each author can write multiple books, but each book can be written by at most one author.
3. **Many-to-Many (M:N):** In a many-to-many relationship, each instance of one entity can be associated with multiple instances of another entity, and vice versa. For example, in a hospital database, a "Doctor" entity may have a many-to-many relationship with a "Patient" entity through a "Treats" relationship, where each doctor can treat multiple patients, and each patient can be treated by multiple doctors.

In order to differentiate between one-to-one, one-to-many, and many-to-many relationships in an ER diagram, we use different notations. A one-to-one relationship is represented by a single line connecting the entities, a one-to-many relationship is represented by a line with a crow's foot at the end of the entity that can have multiple instances, and a many-to-many relationship is represented by a line with crow's feet at both ends.

![Relationship Cardinality Representation](images/relationship_cardinality.png)

#### Participation of an Entity in a Relationship

The participation of an entity in a relationship refers to whether all instances of the entity are involved in the relationship or only some instances. There are two types of participation:

1. **Total Participation:** In total participation, all instances of an entity are involved in the relationship. For example, in a university database, a "Student" entity may have total participation in an "Enrollment" relationship with a "Course" entity, where every student must be enrolled in at least one course.
2. **Partial Participation:** In partial participation, only some instances of an entity are involved in the relationship. For example, in a company database, an "Employee" entity may have partial participation in a "Works On" relationship with a "Project" entity, where only some employees work on projects.

In order to differentiate between total and partial participation in an ER diagram, we use different notations. Total participation is represented by a double line connecting the entity to the relationship, while partial participation is represented by a single line.

![Participation Representation](images/participation.png)

## Crow's Foot Notation

Crow's Foot Notation is a popular notation used in ER diagrams to represent the cardinality of relationships. It uses symbols to indicate the number of instances of one entity that can be associated with instances of another entity in a relationship. Following are the symbols used in Crow's Foot Notation:

| Symbol | Meaning |
| -------- | --------- |
| o\| | Zero-or-one |
| o{ | Zero-or-many |
| \|\| | One and only one |
| \|{ | One or many |

## A real-world example of an ER Diagram

```mermaid
erDiagram

    UNIVERSITY ||--|{ DEPARTMENT : "has"
    DEPARTMENT ||--o| DEPARTMENT_HEAD : "led by"
    PROFESSOR ||--|| DEPARTMENT_HEAD : "appointed as"
    DEPARTMENT ||--|{ COURSE : "offers"
    PROFESSOR ||--o{ COURSE : "teaches"
    STUDENT }o--o{ COURSE : "enrolls in"
    COURSE ||--|{ COURSE_SECTION : "divided into"
    COURSE_SECTION ||--o{ ENROLLMENT : "has"
    STUDENT ||--o{ ENROLLMENT : "registers for"
    COURSE ||--o{ ASSIGNMENT : "has"
    STUDENT ||--o{ SUBMISSION : "submits"
    ASSIGNMENT ||--|{ SUBMISSION : "receives"
    STUDENT o|--|| STUDENT_PROFILE : "has"

    UNIVERSITY {
        int id PK
        string name
        string location
        int founded_year
    }

    DEPARTMENT {
        int id PK
        int university_id FK
        string name
        string building
    }

    DEPARTMENT_HEAD {
        int id PK
        int department_id FK
        int professor_id FK
        date start_date
    }

    PROFESSOR {
        int id PK
        int department_id FK
        string name
        string email
        string rank
    }

    STUDENT {
        int id PK
        string name
        string email
        date enrolled_on
    }

    STUDENT_PROFILE {
        int id PK
        int student_id FK
        string address
        string phone
        string gpa
    }

    COURSE {
        int id PK
        int department_id FK
        int professor_id FK
        string title
        int credits
    }

    COURSE_SECTION {
        int id PK
        int course_id FK
        string semester
        string room
        int capacity
    }

    ENROLLMENT {
        int id PK
        int student_id FK
        int section_id FK
        string grade
    }

    ASSIGNMENT {
        int id PK
        int course_id FK
        string title
        date due_date
        int max_score
    }

    SUBMISSION {
        int id PK
        int assignment_id FK
        int student_id FK
        date submitted_at
        int score
    }
```

The diagram above seems complex, but it is very easy to understand.
First thing to notice is that there are 11 entities in the diagram i.e., UNIVERSITY, DEPARTMENT, DEPARTMENT_HEAD, PROFESSOR, STUDENT, STUDENT_PROFILE, COURSE, COURSE_SECTION, ENROLLMENT, ASSIGNMENT and SUBMISSION. Each entity has its own attributes, primary keys (PK), and foreign keys (FK). I will explain you about PK and FK later but for now let's focus on the relationships and their cardinality:

1. UNIVERSITY has a one-to-many relationship with DEPARTMENT (`||--|{`), which means that one university must have at least one department, and each department belongs to exactly one university.
2. DEPARTMENT has a one-to-zero-or-one relationship with DEPARTMENT_HEAD (`||--o|`), which means that each department may or may not have a department head at a given time, but each department head leads exactly one department.
3. DEPARTMENT has a one-to-many relationship with COURSE (`||--|{`), which means that one department can offer multiple courses, but each course is offered by exactly one department.
4. DEPARTMENT_HEAD has a one-to-one relationship with PROFESSOR (`||--||`), which means that each department head is appointed as exactly one professor, and each professor can be appointed as a department head for only one department.
5. PROFESSOR has a one-to-zero-or-many relationship with COURSE (`||--o{`), which means that a professor may teach zero or more courses (e.g., a newly hired professor may not yet be assigned any course), but each course is taught by exactly one professor.
6. COURSE has a zero-or-many-to-zero-or-many relationship with STUDENT (`}o--o{`), which means that a course can have zero or more students enrolled, and a student can be enrolled in zero or more courses (e.g., a student who has just registered but not yet enrolled in any course).
7. COURSE has a one-to-many relationship with COURSE_SECTION (`||--|{`), which means that one course must have at least one section, and each section belongs to exactly one course.
8. COURSE has a one-to-zero-or-many relationship with ASSIGNMENT (`||--o{`), which means that a course can have zero or more assignments, but each assignment belongs to exactly one course.
9. STUDENT has a zero-or-one-to-one relationship with STUDENT_PROFILE (`o|--||`), which means that a student may or may not have a profile yet, but each student profile belongs to exactly one student.
10. STUDENT has a one-to-zero-or-many relationship with ENROLLMENT (`||--o{`), which means that one student can have zero or more enrollments, but each enrollment record belongs to exactly one student.
11. STUDENT has a one-to-zero-or-many relationship with SUBMISSION (`||--o{`), which means that one student can make zero or more submissions, but each submission belongs to exactly one student.
12. COURSE_SECTION has a one-to-zero-or-many relationship with ENROLLMENT (`||--o{`), which means that one course section can have zero or more enrollments (e.g., a newly created section with no students yet), but each enrollment belongs to exactly one course section.
13. ASSIGNMENT has a one-to-many relationship with SUBMISSION (`||--|{`), which means that one assignment must have at least one submission, and each submission belongs to exactly one assignment.
