# Normalization

Normalization is the process of organizing data in a database in such a way that it reduces redundancy and dependency. This is such an **important** concept in database design that it definitely requires a high IQ to understand it. Like seriously, if you don't understand normalization, you might as well just give up on databases altogether. I gave up during my college days, and I haven't looked back since. But, I think it is time to face my fears and defeat normalization once and for all.

Now, there are different levels of normalization, each with its own set of rules and requirements. We call these levels "normal forms". The most common normal forms are:

1. First Normal Form (1NF)
2. Second Normal Form (2NF)
3. Third Normal Form (3NF)
4. Boyce-Codd Normal Form (BCNF)

Apart from these, there are also higher normal forms like Fourth Normal Form (4NF) and Fifth Normal Form (5NF), but their usage is so rare that we won't even bother to discuss them. Nah! I'm kidding, of course I will cover them as well :(. One interesting thing to note is that as we go up the normal forms, the requirements become more stringent, and the design becomes more complex. Brace yourselves, because the path will get tougher as we move forward.

## First Normal Form (1NF)

A table is in First Normal Form (1NF) if it meets the following criteria:

1. Every column must contain atomic (indivisible) values i.e., each cell in a table should contain only one value.
2. Each record/row must be unique, which means that there should be a primary key to identify each record.
3. Each column should have a unique name.
4. The order in which data is stored does not matter.

For example, consider the following table that contains information about students and their courses:

| StudentID | StudentName | Course          |
|-----------|-------------|-----------------|
| 1         | Alice       | Math            |
| 2         | Bob         | Literature      |
| 3         | Charlie     | History         |

Let us do some checks to see if this table is in 1NF:

1. Are all values atomic? Yes, each cell contains only one value.
2. Is each record unique? Yes, each student has a unique StudentID so obviously entire record becomes unique.
3. Do all columns have unique names? Yes, each column has a unique name.

Consider another table that contains information about students and their courses:

| StudentID | StudentName | Courses         |
|-----------|-------------|-----------------|
| 1         | Alice       | Math, Science   |
| 2         | Bob         | Literature      |
| 3         | Charlie     | History, Art    |

Let us do our usual checks again:

1. Are all values atomic? No, the "Courses" column contains multiple values (e.g., "Math, Science").

We stop here because the table fails the first criterion for 1NF. Hmm, so what should we do now? Alright, tell me what does the first criterion say?
Each cell should contain only one value. So, to achieve it, we can split the "Courses" column into multiple rows, like this:

| StudentID | StudentName | Course          |
|-----------|-------------|-----------------|
| 1         | Alice       | Math            |
| 1         | Alice       | Science         |
| 2         | Bob         | Literature      |
| 3         | Charlie     | History         |
| 3         | Charlie     | Art             |

Now, let's do the checks again:

1. Are all values atomic? Yes, each cell contains only one value.
2. Is each record unique? Yes, but how? Isn't the StudentID repeated? Yes, but the combination of StudentID and Course is unique for each record.

    But why do we have to look at the combination of StudentID and Course? Why not StudentID and StudentName? Because, if we take StudentID and StudentName, we will find that they are not unique — (1, "Alice") appears twice, so that fails immediately. More importantly, even if it were unique in some dataset, StudentName is entirely determined by StudentID (every row with StudentID 1 will always have "Alice"), so it adds no identifying power. A primary key must be the *minimal* set of columns that uniquely identifies a row — and (StudentID, Course) is exactly that.

3. Do all columns have unique names? Yes, each column has a unique name.

Hence, the table is now in First Normal Form (1NF).

## Second Normal Form (2NF)

A table is in Second Normal Form (2NF) if it meets the following criteria:

1. It is in First Normal Form (1NF).
2. It does not have any partial dependency, which means that no non-prime attribute should depend on a part of the primary key. Bro what? Okay, so basically if we have a composite key, then all the non-key columns should depend on the complete composite key, not just a part of it.

For example, consider the following table that contains information about students, their courses, and their grades:

| StudentID | Course          | Grade |
|-----------|-----------------|-------|
| 1         | Math            | A     |
| 1         | Science         | B     |
| 2         | Literature      | A     |
| 2         | Art             | A     |
| 3         | History         | C     |
| 3         | Math            | A     |
| 3         | Art             | B     |

Let us do some checks to see if this table is in 2NF:

1. Is the table in 1NF? Yes, there are atomic values, unique records, and unique column names.
2. Does it have any partial dependency?

    Before we can check for partial dependency, we need to identify the primary key of this table. Hmm, so is StudentID the primary key? No, because it is not unique (e.g., StudentID 1 appears twice). Is Course the primary key? No, because it is not unique (e.g., Course "Math" appears twice). Is Grade the primary key? No, because it is not unique (e.g., Grade "A" appears multiple times). So, this indicates that we have to look for a composite key. Okay, so what about StudentID and Course together? Yes, that works because the combination of StudentID and Course is unique for each record. Let's check for other combinations as well. StudentID and Grade? No, (e.g., StudentID 2 and Grade "A" appears twice). Course and Grade? No, (e.g., Course "Math" and Grade "A" appears twice). Hence, the primary key for this table will be a composite key consisting of StudentID and Course.
Now, we need to check if there is any partial dependency. Okay, so what are the non-prime attributes in this table? Grade. Good, now we need to check if Grade depends on a part of the primary key. Does Grade depend on StudentID alone? No, because the same StudentID can have different grades for different courses (e.g., StudentID 1 has Grade "A" for Math and Grade "B" for Science). Does Grade depend on Course alone? No, because the same Course can have different grades for different students (e.g., Course "Art" has Grade "A" for StudentID 2 and Grade "B" for StudentID 3). Hence, there is no partial dependency in this table.

Consider another table that contains information about students, their courses, and their grades:

| StudentID | Course          | Grade | StudentName |
|-----------|-----------------|-------|-------------|
| 1         | Math            | A     | Alice       |
| 1         | Science         | B     | Alice       |
| 2         | Literature      | A     | Bob         |
| 2         | Art             | A     | Bob         |
| 3         | History         | C     | Charlie     |
| 3         | Math            | A     | Charlie     |
| 3         | Art             | B     | Charlie     |

Let us do our usual checks again:

1. Is the table in 1NF? Yes, there are atomic values, unique records, and unique column names.
2. Does it have any partial dependency?

    The primary key for this table is still a composite key consisting of StudentID and Course. Now, we need to check if there is any partial dependency. The non-prime attributes in this table are Grade and StudentName. From the huge explanation we had earlier, we already know that Grade does not depend on a part of the primary key alone. Now, let's check for StudentName. Does StudentName depend on StudentID alone? Yes, because the same StudentID will always have the same StudentName (e.g., StudentID 1 is always "Alice"). Does StudentName depend on Course alone? No, because the same Course can have different StudentNames for different students (e.g., Course "Math" has StudentName "Alice" for StudentID 1 and StudentName "Charlie" for StudentID 3). Hence, there is a partial dependency.

We stop here because the table fails the second criterion for 2NF. So, what should we do now? Alright, tell me what does the second criterion say?
No non-prime attribute should depend on a part of the primary key. The problematic non-prime attribute here is StudentName, which depends on StudentID alone. To remove this partial dependency, we can create a new table for students that contains StudentID and StudentName, and then remove the StudentName column from the original table. The new tables will look like this:

**Students Table:**

| StudentID | StudentName |
|-----------|-------------|
| 1         | Alice       |
| 2         | Bob         |
| 3         | Charlie     |

**Enrollments Table:**

| StudentID | Course          | Grade |
|-----------|-----------------|-------|
| 1         | Math            | A     |
| 1         | Science         | B     |
| 2         | Literature      | A     |
| 2         | Art             | A     |
| 3         | History         | C     |
| 3         | Math            | A     |
| 3         | Art             | B     |

Well if you remember, this is the same table we had before in the earlier 2NF example! So, we have successfully removed the partial dependency and hence, the Enrollments table is now in Second Normal Form (2NF).

**Note:** A table that has a single attribute primary key is automatically in 2NF if it is in 1NF, because there cannot be any partial dependency when there is only one attribute in the primary key. Hence, we can say that the Students table is in 2NF without even checking for partial dependency.

## Third Normal Form (3NF)

A table is in Third Normal Form (3NF) if it meets the following criteria:

1. It is in Second Normal Form (2NF).
2. It does not have any transitive dependency, which means that no non-prime attribute should depend on another non-prime attribute. If say there is a table which contains columns prim, col1, and col2, where prim is the primary key and col1 and col2 are non-prime attributes, then there should not be any dependency between col1 and col2. In other words, if col1 depends on prim and col2 depends on col1, then there is a transitive dependency and the table is not in 3NF. But if col2 depends on prim directly, then there is no transitive dependency and the table is in 3NF.

For example, consider the following table that contains information about students, their names, and their ages:

| StudentID | Name            | Age |
|-----------|-----------------|-----|
| 1         | Alice           | 20  |
| 2         | Bob             | 22  |
| 3         | Charlie         | 21  |
| 4         | Dave            | 20  |
| 5         | Alice           | 22  |

Let us do some checks to see if this table is in 3NF:

1. Is the table in 2NF? Yes, since there is no partial dependency (the primary key is StudentID, which is a single attribute, so there cannot be any partial dependency).
2. Does it have any transitive dependency?

    The non-prime attributes in this table are Name and Age. Does Name depend on StudentID? Yes, because each student has a specific name. Does Age depend on StudentID? Yes, because each student has a specific age. Now, we need to check if there is any dependency between Name and Age. Does Age depend on Name? No, because the same name can have different ages (e.g., StudentID 1 and 5 both have the name "Alice" but different ages). Hence, there is no transitive dependency in this table.

Consider another table that contains information about students, their names, their ages, and Birth Year:

| StudentID | Name            | Age | BirthYear |
|-----------|-----------------|-----|-----------|
| 1         | Alice           | 20  | 2004      |
| 2         | Bob             | 22  | 2002      |
| 3         | Charlie         | 21  | 2003      |
| 4         | Dave            | 20  | 2004      |
| 5         | Alice           | 22  | 2002      |

Let us do our usual checks again:

1. Is the table in 2NF? Yes, since there is no partial dependency (the primary key is StudentID, which is a single attribute, so there cannot be any partial dependency).

2. Does it have any transitive dependency?

    The non-prime attributes in this table are Name, Age, and BirthYear. We already know that Name and Age depend on StudentID. Now, we need to check if there is any dependency between Name, Age, and BirthYear. Does BirthYear depend on Name? No, because the same name can have different birth years (e.g., StudentID 1 and 5 both have the name "Alice" but different birth years). Does BirthYear depend on Age? Yes, because the same age can have different birth years (e.g., StudentID 1 and 4 both have the age "20" but different birth years). Hence, there is a transitive dependency between Age and BirthYear.

We stop here because the table fails the second criterion for 3NF. Again, what does the second criterion say? No non-prime attribute should depend on another non-prime attribute. The problematic non-prime attribute here is BirthYear, which depends on Age. To remove this transitive dependency, we can create a new table for ages that contains Age and BirthYear, and then remove the BirthYear column from the original table. The new tables will look like this:

**Students Table:**

| StudentID | Name            | Age |
|-----------|-----------------|-----|
| 1         | Alice           | 20  |
| 2         | Bob             | 22  |
| 3         | Charlie         | 21  |
| 4         | Dave            | 20  |
| 5         | Alice           | 22  |

**Ages Table:**

| Age | BirthYear |
|-----|-----------|
| 20  | 2004      |
| 22  | 2002      |
| 21  | 2003      |

Well, if you remember, this is the same table we had before in the earlier 3NF example! So, we have successfully removed the transitive dependency and hence, the Students table is now in Third Normal Form (3NF).

## Boyce-Codd Normal Form (BCNF)

A table is in Boyce-Codd Normal Form (BCNF) if it meets the following criteria:

1. It is in Third Normal Form (3NF).
2. For every functional dependency X -> Y, X should be a super key. Hmm, some gibberish right? To put simply, every column must depend on the primary key, including the columns that are part of the primary key. This is a stronger version of 3NF because in 3NF, we only require that non-prime attributes should not depend on other non-prime attributes, but in BCNF, we require that every attribute should depend on the primary key and nothing else.

For example, consider the following table that contains information about students, subjects, and their teachers. An assumption here is that each teacher teaches only one subject, but a subject can be taught by multiple teachers (e.g., different sections of the same course):

| StudentID | Subject         | Teacher     |
|-----------|-----------------|-------------|
| 1         | Math            | Mr. Smith   |
| 1         | Science         | Mrs. Johnson|
| 2         | Math            | Mr. Jones   |
| 2         | Science         | Mrs. Johnson|

Let us do some checks to see if this table is in BCNF:

1. Is the table in 3NF? Yes, since there is no transitive dependency (the primary key is a composite key consisting of StudentID and Subject, and there are no non-prime attributes that depend on other non-prime attributes).

2. For every functional dependency X -> Y, is X a super key?

    First things first, we need to identify the functional dependencies in this table. But what the heck is a functional dependency? A functional dependency is a relationship between two sets of attributes in a table, where one set of attributes (the determinant) uniquely determines another set of attributes (the dependent). In this table, we have the following functional dependencies:

    - StudentID, Subject -> Teacher (because the combination of StudentID and Subject uniquely determines the Teacher)
    - Teacher -> Subject (because each teacher teaches only one subject)

    Now, we need to check if the determinant in each functional dependency is a super key. Is StudentID, Subject a super key? Yes, because it is the primary key of the table. Is Teacher a super key? No, because it does not uniquely identify each record in the table (e.g., Mrs. Johnson teaches both Science for StudentID 1 and StudentID 2). Hence, there is a functional dependency where the determinant is not a super key.

We stop here because the table fails the second criterion for BCNF. The problematic functional dependency here is Teacher -> Subject, where Teacher is not a super key. To remove this dependency, we can create a new table for teachers that contains Teacher and Subject, and then remove the Subject column from the original table. The new tables will look like this:

**Students Table:**

| StudentID | Teacher         |
|-----------|-----------------|
| 1         | Mr. Smith       |
| 1         | Mrs. Johnson    |
| 2         | Mr. Jones       |
| 2         | Mrs. Johnson    |

**Teachers Table:**

| Teacher     | Subject         |
|-------------|-----------------|
| Mr. Smith   | Math            |
| Mrs. Johnson| Science         |
| Mr. Jones   | Math            |

In most of the cases, if a table is in 3NF, then it will also be in BCNF except for some rare cases where there are overlapping candidate keys.

## Fourth Normal Form (4NF)

A table is in Fourth Normal Form (4NF) if it meets the following criteria:

1. It is in Boyce-Codd Normal Form (BCNF).
2. It does not have any non-trivial multivalued dependency in the table. A multivalued dependency occurs when one attribute in a table uniquely determines another attribute, but there can be multiple values of the second attribute for each value of the first attribute. For example, if we have a table with attributes A, B, and C, and there is a multivalued dependency A ->> B, it means that for each value of A, there can be multiple values of B, and these values of B are independent of each other.

I know this is too much to handle, but let's try to understand it with an example.

Consider the following table that contains information about students, their hobbies, and their skills:

| StudentID | Hobby           | Skill          |
|-----------|-----------------|----------------|
| 1         | Painting        | Programming    |
| 1         | Painting        | Cooking        |
| 1         | Music           | Programming    |
| 1         | Music           | Cooking        |
| 2         | Painting        | Programming    |
| 2         | Painting        | Cooking        |
| 2         | Music           | Programming    |
| 2         | Music           | Cooking        |

Let us do some checks to see if this table is in 4NF:

1. Is the table in BCNF? Yes, since there are no functional dependencies where the determinant is not a super key (the primary key is a composite key consisting of StudentID, Hobby, and Skill, and there are no non-prime attributes that depend on other non-prime attributes).

2. Does it have any non-trivial multi-valued dependency?

    The multi-valued dependencies in this table are:

    - StudentID ->> Hobby (because for each StudentID, there can be multiple Hobbies)
    - StudentID ->> Skill (because for each StudentID, there can be multiple Skills)

    Now, we need to check if these multivalued dependencies are trivial or non-trivial. A multivalued dependency is trivial if the dependent attribute is a subset of the determinant attribute or if the determinant attribute is a super key. Gibberish again right? Okay, every student has multiple hobbies and multiple skills, but the hobbies and skills are independent of each other. For example, StudentID 1 has the hobby "Painting" and the skill "Programming", but there is no dependency between the hobby and the skill. Hence, these multivalued dependencies are non-trivial.

We stop here because the table fails the second criterion for 4NF. The problematic multivalued dependencies here are StudentID ->> Hobby and StudentID ->> Skill, which are non-trivial. To remove these multivalued dependencies, we can split the original table into two tables, one for hobbies and one for skills. The new tables will look like this:

**Hobbies Table:**

| StudentID | Hobby           |
|-----------|-----------------|
| 1         | Painting        |
| 1         | Music           |
| 2         | Painting        |
| 2         | Music           |

**Skills Table:**

| StudentID | Skill          |
|-----------|----------------|
| 1         | Programming    |
| 1         | Cooking        |
| 2         | Programming    |
| 2         | Cooking        |

So, we have successfully removed the non-trivial multivalued dependencies and hence, both the Hobbies table and the Skills table are now in Fourth Normal Form (4NF).
