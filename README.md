# Normalization
A large database defined as a single relation may result in data duplication. This repetition of data may result in:

- Making relations very large.
- It isn't easy to maintain and update data as it would involve searching many records in relation.
- Wastage and poor utilization of disk space and resources.
- The likelihood of errors and inconsistencies increases.

So to handle these problems, we should analyze and decompose the relations with redundant data into smaller, simpler and well-structured relations that are satisfy desirable properties. Normalization is a process of decomposing the relations into relations with fewer attributes.

### What is Normalization?

- Normalization is the process of organizing the data in the database.
- Normalization is used to minimize the redundancy from a relation or set of relations. It is also used to eliminate undesirable characteristics like Insertion, Update, and Deletion Anomalies.
- Normalization divides the larger table into smaller and links them using relationships.
- The normal form is used to reduce redundancy from the database table.

### Types of Normal Forms:

![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20200804110751/normalizationedited.jpg)

| Normal Form | Description                                                                                                  |
|-------------|--------------------------------------------------------------------------------------------------------------|
| 1NF         | A relation is in 1NF if it contains an atomic value.                                                         |
| 2NF         | A relation will be in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the primary key. |
| 3NF         | A relation will be in 3NF if it is in 2NF and no transitive dependency exists.                               |

### First Normal Form (1NF)

- A relation will be 1NF if it contains an atomic value.
- It states that an attribute of a table cannot hold multiple values. It must hold only single-valued attribute.
- First normal form disallows the multi-valued attribute, composite attribute and their combinations.

Here's how you can represent the example of the **EMPLOYEE** table and its decomposition into **1NF** using Markdown:

### Original EMPLOYEE Table (Not in 1NF):


| EMP_ID | EMP_NAME | EMP_PHONE             | EMP_STATE |
|--------|----------|-----------------------|-----------|
| 14     | John     | 7272826385, 9064738238 | UP        |
| 20     | Harry    | 8574783832             | Bihar     |
| 12     | Sam      | 7390372389, 8589830302 | Punjab    |


### Decomposed EMPLOYEE Table (In 1NF):


| EMP_ID | EMP_NAME | EMP_PHONE   | EMP_STATE |
|--------|----------|-------------|-----------|
| 14     | John     | 7272826385  | UP        |
| 14     | John     | 9064738238  | UP        |
| 20     | Harry    | 8574783832  | Bihar     |
| 12     | Sam      | 7390372389  | Punjab    |
| 12     | Sam      | 8589830302  | Punjab    |
