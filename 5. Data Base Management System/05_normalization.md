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
