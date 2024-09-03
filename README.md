Normalization
A large database defined as a single relation may result in data duplication. This repetition of data may result in:

Making relations very large.
It isn't easy to maintain and update data as it would involve searching many records in relation.
Wastage and poor utilization of disk space and resources.
The likelihood of errors and inconsistencies increases.
So to handle these problems, we should analyze and decompose the relations with redundant data into smaller, simpler and well-structured relations that are satisfy desirable properties. Normalization is a process of decomposing the relations into relations with fewer attributes.

Insertion, Update, and Deletion Anomalies
In relational databases, anomalies are problems that can arise when tables are not properly normalized. These anomalies can lead to data inconsistencies, redundant data and inefficiency in managing the data. The three main types of anomalies are Insertion Anomalies, Update Anomalies and Deletion Anomalies.

1. Insertion Anomaly
An Insertion Anomaly occurs when the design of a database schema makes it difficult to insert data into a table without introducing inconsistency or redundancy.

Example: Suppose we have a table that stores information about students and the courses they are enrolled in:

StudentID	StudentName	CourseID	CourseName	Instructor
1	John	101	Math	Dr. Smith
Problem: If we want to insert a new course (say "Physics" with CourseID 102) that currently has no students enrolled, we can't do so without either:

Entering NULL values for the StudentID and StudentName (which violates the integrity of the table).
Repeating data, which could lead to redundancy.
2. Update Anomaly
An Update Anomaly occurs when we need to update the same piece of data in multiple places because it is duplicated in multiple rows. This can lead to data inconsistencies if all instances are not updated correctly.

Example: Using the same table as above, if Dr. Smith changes his name to Dr. Johnson, we would need to update all rows where Dr. Smith is listed as the instructor. If we forget to update one of those rows, your database will have inconsistent data:

StudentID	StudentName	CourseID	CourseName	Instructor
1	John	101	Math	Dr. Johnson
2	Alice	101	Math	Dr. Smith
Problem: The instructor's name is inconsistent for the same course because it was not updated in all rows, leading to inaccurate data.

3. Deletion Anomaly
A Deletion Anomaly occurs when deleting data inadvertently causes other useful data to be lost. This often happens when all data is stored in a single table and related data is not properly normalized.

Example: Suppose a student drops out of a course, and we delete their record from the table:

StudentID	StudentName	CourseID	CourseName	Instructor
1	John	101	Math	Dr. Smith
If John is the only student enrolled in the "Math" course, deleting John's record would also remove the course information (CourseID, CourseName, and Instructor) from the table, even though this information is still needed.

Problem: By deleting John's record, we also lose the information about the "Math" course, which may still be relevant.

What is Normalization?
Normalization is the process of organizing the data in the database.
Normalization is used to minimize the redundancy from a relation or set of relations. It is also used to eliminate undesirable characteristics like Insertion, Update, and Deletion Anomalies.
Normalization divides the larger table into smaller and links them using relationships.
The normal form is used to reduce redundancy from the database table.
Types of Normal Forms:
alt text

Normal Form	Description
1NF	A relation is in 1NF if it contains an atomic value.
2NF	A relation will be in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the primary key.
3NF	A relation will be in 3NF if it is in 2NF and no transitive dependency exists.
First Normal Form (1NF)
A relation will be 1NF if it contains an atomic value.
It states that an attribute of a table cannot hold multiple values. It must hold only single-valued attribute.
First normal form disallows the multi-valued attribute, composite attribute and their combinations.
Here's how we can represent the example of the EMPLOYEE table and its decomposition into 1NF using Markdown:

Original EMPLOYEE Table (Not in 1NF):
EMP_ID	EMP_NAME	EMP_PHONE	EMP_STATE
14	John	7272826385, 9064738238	UP
20	Harry	8574783832	Bihar
12	Sam	7390372389, 8589830302	Punjab
Decomposed EMPLOYEE Table (In 1NF):
EMP_ID	EMP_NAME	EMP_PHONE	EMP_STATE
14	John	7272826385	UP
14	John	9064738238	UP
20	Harry	8574783832	Bihar
12	Sam	7390372389	Punjab
12	Sam	8589830302	Punjab
Second Normal Form (2NF)
Second Normal Form (2NF) is a higher level of database normalization that builds upon First Normal Form (1NF). A relation (or table) is in 2NF if:

It is already in 1NF.
All non-key attributes are fully functionally dependent on the primary key. This means that there are no partial dependencies, where a non-key attribute depends on part of a composite primary key rather than on the entire key.
Example of 2NF
Step 1: Original Table (In 1NF, but not in 2NF)
Consider the following STUDENT_COURSE table, which records the courses that students are enrolled in, along with the marks they obtained in the courses:

StudentID	CourseID	StudentName	CourseName	Marks
1	101	John	Math	85
1	102	John	English	90
2	101	Alice	Math	88
2	103	Alice	Science	92
Primary Key: {StudentID, CourseID} (composite key)
Non-Key Attributes: StudentName, CourseName, Marks
In this table, the attributes StudentName and CourseName are partially dependent on the composite primary key:

StudentName depends only on StudentID, not on the full key {StudentID, CourseID}.
CourseName depends only on CourseID, not on the full key {StudentID, CourseID}.
Thus, this table is not in 2NF because it contains partial dependencies.

Step 2: Decomposition into 2NF
To remove partial dependencies, we decompose the table into two smaller tables: one for student information and another for course information.

Student Table (2NF):

StudentID	StudentName
1	John
2	Alice
Course Table (2NF):

CourseID	CourseName
101	Math
102	English
103	Science
Enrollment Table (2NF):

StudentID	CourseID	Marks
1	101	85
1	102	90
2	101	88
2	103	92
Now:

StudentName is fully dependent on StudentID (in the Student table).
CourseName is fully dependent on CourseID (in the Course table).
The Marks attribute depends on the full composite key {StudentID, CourseID} in the Enrollment table.
Thus, all tables are now in 2NF, with no partial dependencies remaining.

Third Normal Form (3NF)
Third Normal Form (3NF) is a stage of database normalization designed to reduce redundancy and improve data integrity. A relation (or table) is in 3NF if it satisfies the following conditions:

It is in Second Normal Form (2NF): This means it is already in First Normal Form (1NF) and there are no partial dependencies (i.e., all non-key attributes are fully dependent on the entire primary key).

No Transitive Dependencies: In addition to being in 2NF, a table is in 3NF if every non-key attribute is non-transitively dependent on the primary key. In other words, a non-key attribute should not depend on another non-key attribute.

Example of 3NF
Step 1: Table Not in 3NF
Consider the following EMPLOYEE table:

EmpID	EmpName	EmpDept	DeptLocation
1	John	Sales	New York
2	Alice	HR	Chicago
3	Bob	Sales	New York
Primary Key: EmpID
Non-Key Attributes: EmpName, EmpDept, DeptLocation
Here:

EmpDept (non-key attribute) determines DeptLocation (another non-key attribute). So, DeptLocation is transitively dependent on EmpID through EmpDept.
Step 2: Decomposition into 3NF
To bring this table into 3NF, you must eliminate the transitive dependency by creating separate tables.

Employee Table (3NF):

EmpID	EmpName	EmpDept
1	John	Sales
2	Alice	HR
3	Bob	Sales
Department Table (3NF):

EmpDept	DeptLocation
Sales	New York
HR	Chicago
In this decomposition:

The Employee table stores employee-specific information.
The Department table stores department-specific information, including the location.
Explanation:

In the Employee table, EmpDept is the foreign key that references the Department table.
In the Department table, DeptLocation is dependent only on EmpDept, and there are no transitive dependencies.
SQL TRANSACTIONS
Transactions group a set of tasks into a single execution unit. Each transaction begins with a specific job and ends when all the tasks in the group successfully completed. If any of the tasks fail, the transaction fails. Therefore, a transaction has only two results: success or failure.

Example of a transaction to transfer $150 from account A to account B:

1. read(A)  
2. A:= A – 150  
3. write(A)  
4. read(B)  
5. B:= B + 150  
6. write(B)
Incomplete steps result in the failure of the transaction. A database transaction, by definition, must be atomic, consistent, isolated, and durable.
These are popularly known as ACID properties. These properties can ensure the concurrent execution of multiple transactions without conflict.

ACID Properties
ACID stands for Atomicity, Consistency, Isolation, and Durability. These are essential properties in databases to ensure that transactions are processed reliably.

ACID Properties in DBMS

1) Atomicity
Atomicity means that a transaction is "all or nothing." If any part of the transaction fails, the whole transaction should fail, and the system should return to its previous state. It ensures that transactions do not end up partially completed.

Example: Imagine Remo wants to transfer $10 from his account (A) to Sheero's account (B). After the transaction, Remo's balance should decrease by $10, and Sheero's balance should increase by $10. If the money is deducted from Remo's account but not added to Sheero's account, the transaction is not atomic. Atomicity ensures that either both actions (debit and credit) happen, or neither does.

ACID Properties in DBMS

In the above diagram, it can be seen that after crediting $10, the amount is still $100 in account B. So, it is not an atomic transaction.

The below image shows that both debit and credit operations are done successfully. Thus the transaction is atomic.

ACID Properties in DBMS

Thus, when the amount loses atomicity, then in the bank systems, this becomes a huge issue, and so the atomicity is the main focus in the bank systems.

2) Consistency
Consistency ensures that a transaction brings the database from one valid state to another. After a transaction, the data should follow all the rules and constraints set on the database.

Example:

ACID Properties in DBMS

In the above figure, there are three accounts, A, B, and C, where A is making a transaction T one by one to both B & C. There are two operations that take place, i.e., Debit and Credit. Account A firstly debits $50 to account B, and the amount in account A is read $300 by B before the transaction. After the successful transaction T, the available amount in B becomes $150. Now, A debits $20 to account C, and that time, the value read by C is $250 (that is correct as a debit of $50 has been successfully done to B). The debit and credit operation from account A to C has been done successfully. We can see that the transaction is done successfully, and the value is also read correctly. Thus, the data is consistent. In case the value read by B and C is $300, which means that data is inconsistent because when the debit operation executes, it will not be consistent.

3) Isolation
Isolation ensures that transactions occur independently of each other. Even if multiple transactions happen at the same time, each transaction should be isolated so that they don’t interfere with each other.

Example: If two operations are concurrently running on two different accounts, then the value of both accounts should not get affected. The value should remain persistent. As you can see in the below diagram, account A is making T1 and T2 transactions to account B and C, but both are executing independently without affecting each other. It is known as Isolation.

ACID Properties in DBMS

4) Durability
Durability ensures the permanency of something. In DBMS, the term durability ensures that the data after the successful execution of the operation becomes permanent in the database. The durability of the data should be so perfect that even if the system fails or leads to a crash, the database still survives. However, if gets lost, it becomes the responsibility of the recovery manager for ensuring the durability of the database. For committing the values, the COMMIT command must be used every time we make changes.
