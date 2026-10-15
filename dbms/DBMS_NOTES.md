# 4 U By U &bull; Complete DBMS Masterclass & Placement Blueprint
> **Source Material:** CodeHelp DBMS Master Notes (49 Pages &bull; 21 Core Lectures & Scaling Patterns)  
> **Target Audience:** Engineering Students, System Architects & Placement Candidates  
> **Status:** Verified 100% Complete Transcription & Conceptual Guide  

---

## Table of Contents
1. [LEC-1: Introduction to DBMS & Data Foundations](#lec-1-introduction-to-dbms--data-foundations) (Pages 1–2)
2. [LEC-2: DBMS Architecture & Three-Schema Framework](#lec-2-dbms-architecture--three-schema-framework) (Pages 3–5)
3. [LEC-3: Entity-Relationship (ER) Model](#lec-3-entity-relationship-er-model) (Pages 6–8)
4. [LEC-4: Extended ER Features (EER)](#lec-4-extended-er-features-eer) (Page 9)
5. [LEC-7: Relational Model & Keys](#lec-7-relational-model--keys) (Pages 10–11)
6. [LEC-8: Transformation: ER Model to Relational Model](#lec-8-transformation-er-model-to-relational-model) (Pages 12–13)
7. [LEC-9: Complete SQL Masterclass](#lec-9-complete-sql-masterclass) (Pages 14–21)
8. [LEC-11: Functional Dependencies & Normalisation](#lec-11-functional-dependencies--normalisation) (Pages 22–23)
9. [LEC-12: Transactions & ACID Properties](#lec-12-transactions--acid-properties) (Pages 24–25)
10. [LEC-13: Implementing Atomicity & Durability](#lec-13-implementing-atomicity--durability) (Page 26)
11. [LEC-14: Indexing in DBMS](#lec-14-indexing-in-dbms) (Pages 27–28)
12. [LEC-15: NoSQL Databases](#lec-15-nosql-databases) (Pages 29–31)
13. [LEC-16: Taxonomy of Database Models](#lec-16-taxonomy-of-database-models) (Pages 32–33)
14. [LEC-17: Database Clustering](#lec-17-database-clustering) (Page 34)
15. [LEC-18: Partitioning & Sharding](#lec-18-partitioning--sharding) (Page 35)
16. [Scaling Case Study: Step-by-Step Scaling Patterns](#scaling-case-study-step-by-step-scaling-patterns) (Pages 36–47)
17. [LEC-20: CAP Theorem in Distributed Databases](#lec-20-cap-theorem-in-distributed-databases) (Page 48)
18. [LEC-21: The Master-Slave Architecture](#lec-21-the-master-slave-architecture) (Page 49)

---

## LEC-1: Introduction to DBMS & Data Foundations
*PDF Reference: Pages 1–2*

### 1. What is Data?
- **Definition:** Data is a collection of raw, unorganized facts and details like text, observations, figures, symbols, and descriptions of things.
- Data does not carry any specific purpose and has no significance by itself.
- Data is measured in terms of **bits and bytes** &mdash; the basic units of information in computer storage and processing.
- Data can be recorded and doesn’t have any meaning unless processed.

### 2. Types of Data
1. **Quantitative:**
   - Numerical form.
   - Examples: Weight, volume, cost of an item.
2. **Qualitative:**
   - Descriptive, non-numerical form.
   - Examples: Name, gender, hair color of a person.

### 3. What is Information?
- Information is **processed, organized, and structured data**.
- It provides context to data and enables decision making.
- Information is processed data that makes sense to humans.
- It is extracted by analyzing and interpreting pieces of data.
- *Example:* If you collect raw census data from a locality, that is Data. When analyzed to find:
  - 100 senior citizens
  - Sex ratio is 1.1
  - 100 newborn babies  
  These conclusions represent **Information**.

### 4. Data vs Information Matrix
| Dimension | Data | Information |
|---|---|---|
| **Nature** | Raw, unorganized facts | Processed, organized, structured |
| **Context** | Lacks context; isolated points | Places facts into context; big-picture view |
| **Meaning** | Meaningless on its own | Meaningful after interpretation |
| **Dependency** | Independent of information | Heavily dependent on underlying data |
| **Representation** | Numbers, graphs, figures, statistics | Words, language, ideas, thoughts |
| **Decision Making**| Insufficient for decisions | Directly enables sound decision making |

### 5. What is a Database?
- An electronic system/place where data is stored systematically so that it can be **easily accessed, managed, and updated**.
- To make real operational use of data, we require Database Management Systems (DBMS).

### 6. What is a DBMS?
- A Database Management System is a collection of **interrelated data** and a **set of programs to access those data**.
- The collection of data is referred to as the database, containing enterprise-relevant information.
- **Primary Goal:** Provide a convenient and efficient way to store and retrieve database information.
- A DBMS encompasses the database itself along with all software and functionality to perform operations: addition, access, updating, and deletion.

### 7. DBMS vs File Systems (Why Use DBMS?)
File-processing systems suffer from major disadvantages, which correspond directly to the **advantages of DBMS**:
1. **Data Redundancy and Inconsistency:** Multiple file formats and duplicate data lead to higher storage and inconsistent records. DBMS ensures centralized single-point storage.
2. **Difficulty in Accessing Data:** File systems require custom ad-hoc programs to extract data. DBMS provides structured query capabilities.
3. **Data Isolation:** Data scattered in different files and formats makes retrieval hard.
4. **Integrity Problems:** Enforcement of consistency constraints across isolated files is cumbersome.
5. **Atomicity Problems:** Systems may crash mid-operation in file systems leaving partial state. DBMS guarantees all-or-nothing transactions.
6. **Concurrent-Access Anomalies:** Multiple users updating files simultaneously cause race conditions. DBMS implements robust concurrency control.
7. **Security Problems:** Granular authorization is difficult in OS files. DBMS enforces role-based and view-based security.

---

## LEC-2: DBMS Architecture & Three-Schema Framework
*PDF Reference: Pages 3–5*

### 1. Three-Schema Architecture (View of Data)
DBMS achieves data abstraction by hiding low-level storage details across three distinct levels:
1. **Physical Level (Internal Level):**
   - Lowest level of abstraction; describes *how* data are physically stored.
   - Low-level data structures (e.g., B+ trees, N-ary trees, hashing).
   - Manages storage allocation, data compression, encryption, and block layouts.
   - *Goal:* Define algorithms for efficient physical access.
2. **Logical Level (Conceptual Level):**
   - Describes *what* data are stored in the database and what relationships exist among them.
   - Programmers and DBAs operate at this level.
   - Hides physical storage complexity.
   - *Goal:* Ease of use and structural design.
3. **View Level (External Level):**
   - Highest level of abstraction; provides customized, role-tailored views of the database for different user groups.
   - Each view schema (subschema) hides the rest of the database.
   - Provides security barriers preventing unauthorized access to sensitive fields.

```
+-------------------------------------------------------+
|  View 1 (External)   View 2 (External)   View N ...   |
+-------------------------------------------------------+
                           |
            [ External / Conceptual Mapping ]
                           v
+-------------------------------------------------------+
|              Conceptual / Logical Level               |
+-------------------------------------------------------+
                           |
            [ Conceptual / Internal Mapping ]
                           v
+-------------------------------------------------------+
|             Internal / Physical Level                 |
+-------------------------------------------------------+
                           v
                     [ Database ]
```

### 2. Instances and Schemas
- **Instance:** The collection of information stored in the database at a specific moment in time. Dynamic and changes frequently.
- **Schema:** The overall logical design/structure of the database. Analogous to variable types and class definitions in programming. Static and rarely modified.
- **Physical Data Independence:** The capacity to alter the physical schema (e.g., storage hardware, file organization, indexes) without requiring changes to the logical schema or application programs.

### 3. Data Models
- Conceptual tools for describing data, data relationships, data semantics, and consistency constraints.
- Prominent models: Relational Model, Entity-Relationship (ER) Model, Object-Oriented Model, Object-Relational Model.

### 4. Database Languages
- **DDL (Data Definition Language):** Specifies database schema, constraints, and authorization.
- **DML (Data Manipulation Language):** Expresses data queries and modifications (insert, update, delete). Includes Query Languages.
- Practically, both features are unified in SQL.

### 5. Application Access Interfaces
- Applications in host languages (C/C++, Java, Python) interact with the DBMS via APIs:
  - **ODBC (Open Database Connectivity):** Microsoft C-based standard.
  - **JDBC (Java Database Connectivity):** Java enterprise standard.

### 6. Functions of the Database Administrator (DBA)
- Central controller of data and access programs:
  1. Schema definition
  2. Storage structure and access-method definition
  3. Schema and physical-organization modifications
  4. Granting authorization for data access
  5. Routine maintenance (periodic backups, security patches, system upgrades)

### 7. Application Architectures
- **1-Tier (T1):** Client, Server, and Database all reside on the exact same physical machine.
- **2-Tier (T2):** Direct client-to-server architecture. Client issues query language statements directly to the database engine via ODBC/JDBC.
- **3-Tier (T3):** Client (frontend) communicates with an Application Server, which processes business logic and communicates with the Database Server.
  - *Advantages:* High scalability via distributed app servers, superior data integrity (logic separated from storage), robust security (client has zero direct database connectivity). Ideal for WWW applications.

---

## LEC-3: Entity-Relationship (ER) Model
*PDF Reference: Pages 6–8*

### 1. Fundamental ER Concepts
- **ER Model:** High-level conceptual data model perceiving the real world as a collection of basic objects (entities) and relationships among them.
- **Entity:** A real-world "thing" or "object" distinguishable from all other objects (e.g., a specific student, bank customer).
- **Strong Entity:** Can be uniquely identified on its own via a Primary Key.
- **Weak Entity:** Cannot be uniquely identified by its own attributes alone; depends on the existence of an identifying strong entity (e.g., `Payment` depends on `Loan`).
  - Lacks a primary key; identified via **Partial Discriminator Key + Strong Entity's Primary Key**.

### 2. Entity Sets & Attributes
- **Entity Set:** A set of entities of the same type sharing identical properties/attributes (e.g., all Students in a university).
- **Attribute:** Descriptive property possessed by each member of an entity set.
- **Domain:** Permitted set of values for an attribute.

### 3. Attribute Classification
1. **Simple:** Cannot be divided further (e.g., `Roll_No`, `Account_Number`).
2. **Composite:** Can be divided into subparts (e.g., `Name` into `First_Name`, `Middle_Name`, `Last_Name`; `Address` into `Street`, `City`, `State`, `PIN`).
3. **Single-Valued:** Takes a single value for an entity (e.g., `Student_ID`).
4. **Multi-Valued:** Can hold multiple values simultaneously (e.g., `Phone_Numbers`, `Degrees`).
5. **Derived:** Value computed dynamically from other attributes (e.g., `Age` derived from `Date_of_Birth`).
6. **NULL Values:** Represents "not applicable" (e.g., no middle name) or "unknown" (missing value or unassigned salary).

### 4. Relationships & Constraints
- **Relationship:** Association among two or more entities (e.g., `Student enrolls in Course`).
- **Degree of Relationship:**
  - **Unary (Recursive):** 1 entity set participating (e.g., `Employee manages Employee`).
  - **Binary:** 2 entity sets participating (most common; e.g., `Student takes Course`).
  - **Ternary:** 3 entity sets participating (e.g., `Employee works on Branch for Job`).
- **Mapping Cardinalities (Cardinality Ratios):**
  - **One-to-One (1:1):** Citizen &harr; Aadhar Card.
  - **One-to-Many (1:N):** Citizen &harr; Vehicles.
  - **Many-to-One (N:1):** Course &harr; Professor.
  - **Many-to-Many (M:N):** Customer &harr; Products; Student &harr; Courses.
- **Participation Constraints (Minimum Cardinality):**
  - **Partial Participation:** Not every entity in the set is required to participate in the relationship.
  - **Total Participation (Existence Dependency):** Every entity must participate in at least one relationship instance (e.g., `Loan` cannot exist without `Customer`). Represented by double lines. Weak entities always exhibit total participation.

### 5. ER Diagram Standard Notations
- **Rectangle:** Strong Entity
- **Double Rectangle:** Weak Entity
- **Ellipse:** Attribute
- **Double Ellipse:** Multi-valued Attribute
- **Dashed Ellipse:** Derived Attribute
- **Underlined Text inside Ellipse:** Primary Key Attribute
- **Dashed Underline inside Ellipse:** Weak Key / Partial Discriminator Attribute
- **Diamond:** Relationship
- **Double Diamond:** Identifying Relationship for Weak Entity
- **Double Line:** Total Participation

---

## LEC-4: Extended ER Features (EER)
*PDF Reference: Page 9*

### 1. Specialisation (Top-Down Approach)
- Subgrouping an entity set into distinctive sub-entity sets based on specific functionalities, specialities, and features.
- *Example:* `Person` (Superclass) specialized into `Customer`, `Student`, `Employee` (Subclasses).
- Uses "is-a" relationship represented by a triangle component pointing to the superclass.
- *Rationale:* Allows defining attributes and relationships that apply only to specific subgroups without polluting the generic superclass.

### 2. Generalisation (Bottom-Up Approach)
- Exact reverse of Specialisation.
- Identifies common attributes across multiple existing entity sets and synthesizes a generalized superclass.
- *Example:* `Car`, `Jeep`, and `Bus` generalized into `Vehicle`.
- *Rationale:* Eliminates data redundancy and streamlines database schema design.

### 3. Inheritance Principles
- **Attribute Inheritance:** Subclasses automatically inherit all attributes of their parent superclass.
- **Participation Inheritance:** If a parent entity set participates in an external relationship, all its specialized child entity sets automatically participate in that relationship.

### 4. Aggregation
- Technique used when a relationship needs to be treated as a higher-level abstract entity and enter into a relationship with another entity.
- Solves the problem of "relationships among relationships" and prevents redundant multi-way relationships.

---

## LEC-7: Relational Model & Keys
*PDF Reference: Pages 10–11*

### 1. Relational Model Fundamentals
- Organizes data into **relations (tables)**, each identified by a unique name.
- **Tuple:** A single row representing a distinct real-world record.
- **Column / Attribute:** Named property with a specified domain.
- **Relation Schema:** Denoted as $R(A_1, A_2, \dots, A_n)$; defines table structure and attribute domains.
- **Degree:** Number of columns/attributes in a relation.
- **Cardinality:** Total number of tuples/rows in a relation.

### 2. Properties of Relations
1. Unique relation names within the database.
2. **Atomic values:** Values cannot be divided into multi-valued lists (First Normal Form requirement).
3. Unique column names within a relation.
4. Unique tuples (no duplicate rows).
5. The ordering of rows and columns has no semantic significance.
6. Must strictly adhere to defined integrity constraints.

### 3. Hierarchy of Relational Keys
```
+-------------------------------------------------------+
|                     SUPER KEYS                        |
|  (Any combination of attributes uniquely identifying) |
|   +-----------------------------------------------+   |
|   |                CANDIDATE KEYS                 |   |
|   |         (Minimal Super Keys, No Redundancy)   |   |
|   |   +-------------------+  +----------------+   |   |
|   |   |    PRIMARY KEY    |  | ALTERNATE KEYS |   |   |
|   |   | (Chosen Minimal)  |  |  (Remaining)   |   |   |
|   |   +-------------------+  +----------------+   |   |
|   +-----------------------------------------------+   |
+-------------------------------------------------------+
```
- **Super Key (SK):** Any superset of attributes that can uniquely identify each tuple in a relation.
- **Candidate Key (CK):** A minimal super key with zero redundant attributes. CK values cannot be NULL.
- **Primary Key (PK):** The candidate key selected by the DBA to uniquely identify tuples. Must be unique and `NOT NULL`.
- **Alternate Key (AK):** All candidate keys that were not chosen as the Primary Key ($AK = CK \setminus \{PK\}$).
- **Foreign Key (FK):** An attribute in relation $R_1$ (referencing/child) that references the Primary Key of relation $R_2$ (referenced/parent). Enables referential integrity.
- **Composite Key:** A primary key constructed from two or more attributes.
- **Compound Key:** A key composed of at least two foreign keys.
- **Surrogate Key:** An artificially generated synthetic primary key (usually an auto-incrementing integer or UUID) with no business meaning.

### 4. Integrity Constraints
1. **Domain Constraints:** Enforce data types, valid ranges, and value sets for each attribute.
2. **Entity Integrity Constraints:** Every relation must have a primary key, and no primary key attribute can be `NULL`.
3. **Referential Integrity Constraints:** If a foreign key exists in a referencing table, each value must either match an existing primary key value in the referenced table or be explicitly `NULL`.
4. **Key Constraints:**
   - `NOT NULL`: Attribute must always contain a value.
   - `UNIQUE`: Prevents duplicate entries in a column (permits NULLs unless restricted).
   - `DEFAULT`: Supplies fallback value when none is provided during insertion.
   - `CHECK`: Evaluates a boolean condition before allowing CRUD operations.
   - `PRIMARY KEY`: Combines `NOT NULL` and `UNIQUE`.
   - `FOREIGN KEY`: Establishes parent-child cross-table linkages.

---

## LEC-8: Transformation: ER Model to Relational Model
*PDF Reference: Pages 12–13*

### Rule-by-Rule Mapping Specification
1. **Strong Entity Set:**
   - Becomes an independent table.
   - Attributes become columns.
   - Entity's Primary Key becomes the table's Primary Key.
2. **Weak Entity Set:**
   - Becomes a separate table.
   - Contains all attributes of the weak entity.
   - Includes the Primary Key of the owner Strong Entity as a Foreign Key.
   - **Composite Primary Key:** $\{ \text{Owner FK} + \text{Partial Discriminator Key} \}$.
3. **Single-Valued Attributes:**
   - Mapped directly as columns in the corresponding relation.
4. **Composite Attributes:**
   - Flattened out: Flatten composite components into distinct individual columns in the relation (e.g., `Address` becomes `address_street`, `address_city`, `address_pin`). The parent attribute is discarded.
5. **Multi-Valued Attributes:**
   - Must be mapped to an **independent new table**.
   - Columns: Primary Key of the owner entity (as Foreign Key) + the multivalued attribute value.
   - **Composite Primary Key:** $\{ \text{Owner FK} + \text{Attribute Value} \}$.
   - *Example:* For `Employee(emp_id)` with multivalued `dependent_name`, create `Dependent(emp_id, dname)` with PK $\{ \text{emp\_id}, \text{dname} \}$ and FK `emp_id`.
6. **Derived Attributes:**
   - **Omitted from tables** to prevent storage waste and sync anomalies. Calculated on-the-fly via SQL views or application queries.
7. **Generalisation / Specialisation:**
   - **Method 1 (Higher + Lower Tables):**
     - Table for superclass: `Account(acc_no, balance)`.
     - Tables for subclasses containing subclass attributes + superclass PK:  
       `Savings_Account(acc_no, interest_rate, daily_limit)`  
       `Current_Account(acc_no, overdraft_amount, transaction_charge)`.
   - **Method 2 (Lower Tables Only - Disjoint & Complete):**
     - Discard superclass table; lower tables store all inherited attributes:  
       `Savings_Account(acc_no, balance, interest_rate, daily_limit)`  
       `Current_Account(acc_no, balance, overdraft_amount, transaction_charge)`.
     - *Drawback:* Redundant column definitions; invalid if generalisation is overlapping or incomplete.
8. **Aggregation Mapping:**
   - Create a dedicated table for the relationship set containing primary keys of participating entity sets and aggregated relationships, plus any descriptive attributes.

---

## LEC-9: Complete SQL Masterclass
*PDF Reference: Pages 14–21*

### 1. SQL Overview & Data Types
- **SQL (Structured Query Language):** Non-procedural query language for executing CRUD operations on Relational Databases.
- **RDBMS vs SQL:** SQL is the language specification; MySQL, PostgreSQL, Oracle, and MS SQL Server are software implementations (RDBMS).

#### SQL Data Types Quick Reference Table
| Category | Data Type | Specification / Storage Range |
|---|---|---|
| **Exact String** | `CHAR(n)` | Fixed-length string: $0 \le n \le 255$ bytes |
| **Variable String** | `VARCHAR(n)` | Variable-length string: $0 \le n \le 65,535$ bytes |
| **Long Text** | `TEXT` | $0 \le \text{length} \le 65,535$ characters |
| **Binary Objects** | `BLOB` | Binary large object up to 65,535 bytes |
| **Integer Types** | `TINYINT` | $-128 \text{ to } 127$ (or $0 \text{ to } 255$ UNSIGNED) |
| | `SMALLINT` | $-32,768 \text{ to } 32,767$ |
| | `MEDIUMINT` | $-8,388,608 \text{ to } 8,388,607$ |
| | `INT` | $-2,147,483,648 \text{ to } 2,147,483,647$ |
| | `BIGINT` | $\approx -9.22 \times 10^{18} \text{ to } 9.22 \times 10^{18}$ |
| **Floating Point** | `FLOAT` / `DOUBLE` | Single precision (23 digits) / Double precision (53 digits) |
| **Exact Decimal** | `DECIMAL(p,s)` | Exact fixed-point numeric stored as packed string |
| **Temporal Types** | `DATE` | `YYYY-MM-DD` |
| | `DATETIME` | `YYYY-MM-DD HH:MM:SS` |
| | `TIMESTAMP` | `YYYYMMDDHHMMSS` (timezone aware) |
| **Enums & Bits** | `ENUM` / `BOOLEAN` | Set of predefined string literals / `0` or `1` |

### 2. Five Sub-Languages of SQL
1. **DDL (Data Definition Language):** `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.
2. **DRL / DQL (Data Retrieval / Query Language):** `SELECT`.
3. **DML (Data Manipulation Language):** `INSERT`, `UPDATE`, `DELETE`.
4. **DCL (Data Control Language):** `GRANT`, `REVOKE`.
5. **TCL (Transaction Control Language):** `START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

### 3. DDL Syntax & Database Operations
```sql
-- Database Management
CREATE DATABASE IF NOT EXISTS company_db;
USE company_db;
DROP DATABASE IF EXISTS company_db;
SHOW DATABASES;
SHOW TABLES;

-- Table Creation with Full Constraints
CREATE TABLE customer (
    cust_id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(1024) UNIQUE,
    age INT,
    balance DOUBLE NOT NULL DEFAULT 0.0,
    CONSTRAINT age_check CHECK (age >= 18)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    delivery_date DATE,
    order_placed_date DATE,
    cust_id INT,
    FOREIGN KEY (cust_id) REFERENCES customer(cust_id) 
        ON UPDATE CASCADE 
        ON DELETE SET NULL
);

-- Alter Operations
ALTER TABLE customer ADD phone VARCHAR(20) NOT NULL;
ALTER TABLE customer MODIFY name VARCHAR(500);
ALTER TABLE customer CHANGE COLUMN phone contact_number VARCHAR(25);
ALTER TABLE customer DROP COLUMN contact_number;
ALTER TABLE customer RENAME TO customer_details;
```

### 4. DRL / DQL: Querying Data
- **Syntax:** `SELECT columns FROM table_name WHERE condition;`
- **Execution Order:** Evaluated from Right to Left (`FROM` &rarr; `WHERE` &rarr; `GROUP BY` &rarr; `HAVING` &rarr; `SELECT` &rarr; `ORDER BY`).
- **Dual Table:** Dummy table in MySQL for evaluating constants and functions:
  ```sql
  SELECT 55 + 11;
  SELECT NOW();
  SELECT UCASE('codehelp');
  ```
- **Clauses & Operators:**
  - `WHERE`: Filter rows based on conditions (`age > 18`).
  - `BETWEEN`: Inclusive boundary check (`age BETWEEN 20 AND 30`).
  - `IN`: Reduces chained OR conditions (`city IN ('Delhi', 'Mumbai', 'Bangalore')`).
  - Wildcards (`LIKE`): `%` (0 to n characters), `_` (exactly 1 character).
  - `ORDER BY col ASC/DESC`: Sort result sets.
  - `DISTINCT`: Eliminates duplicate tuples.
  - `GROUP BY`: Collects data across multiple records and groups them by categorical columns. All non-aggregated columns in `SELECT` must appear in `GROUP BY`.
  - `HAVING`: Filters aggregated groups. `WHERE` filters rows *before* grouping; `HAVING` filters groups *after* aggregation.

### 5. Table Joins
```
        INNER JOIN                    LEFT OUTER JOIN                   RIGHT OUTER JOIN
     +-----+-----+-----+            +-----+-----+-----+               +-----+-----+-----+
     |  A  | A∩B |  B  |            |#####|#####|  B  |               |  A  |#####|#####|
     |     |#####|     |            |#####|#####|     |               |     |#####|#####|
     +-----+-----+-----+            +-----+-----+-----+               +-----+-----+-----+
```
1. **INNER JOIN:** Returns matching records present in both relations.
2. **LEFT JOIN:** Returns all records from left relation and matched records from right relation (unmatched right filled with NULL).
3. **RIGHT JOIN:** Returns all records from right relation and matched records from left relation.
4. **FULL JOIN:** Emulated in MySQL using `LEFT JOIN UNION RIGHT JOIN`.
5. **CROSS JOIN:** Cartesian product ($m \times n$ tuples).
6. **SELF JOIN:** Joining a table to itself using aliases to resolve hierarchical or sequential links.

### 6. Set Operations & Subqueries
- `UNION` (removes duplicates) vs `UNION ALL` (retains duplicates).
- `INTERSECT` & `MINUS` (emulated in MySQL using `INNER JOIN` and `LEFT JOIN ... WHERE right.id IS NULL`).
- **Subqueries:** Nested queries inside `WHERE`, `FROM`, or `SELECT` clauses.
- **Correlated Subquery:** Subquery executed once per candidate row of the outer query (driven by the outer query).

---

## LEC-11: Functional Dependencies & Normalisation
*PDF Reference: Pages 22–23*

### 1. Functional Dependency (FD)
- Denoted as $X \rightarrow Y$, meaning attribute set $X$ uniquely determines attribute set $Y$.
- $X$ is the **Determinant**, $Y$ is the **Dependent**.
- **Trivial FD:** $X \rightarrow Y$ is trivial if $Y \subseteq X$ (e.g., $A \rightarrow A$ or $AB \rightarrow A$).
- **Non-Trivial FD:** $X \rightarrow Y$ is non-trivial if $X \cap Y = \emptyset$.

### 2. Armstrong's Axioms (Inference Rules)
1. **Reflexivity:** If $Y \subseteq X$, then $X \rightarrow Y$.
2. **Augmentation:** If $X \rightarrow Y$, then $XZ \rightarrow YZ$ for any attribute set $Z$.
3. **Transitivity:** If $X \rightarrow Y$ and $Y \rightarrow Z$, then $X \rightarrow Z$.

### 3. Why Normalise? Database Anomalies
Data redundancy causes severe anomalies:
1. **Insertion Anomaly:** Inability to insert legitimate data without the presence of unrelated attributes.
2. **Deletion Anomaly:** Deleting one record inadvertently erases unrelated, essential data.
3. **Updation (Modification) Anomaly:** Updating a value requires changes across multiple duplicate rows; missing one results in data inconsistency.

### 4. Normal Forms Hierarchy
```
    +-------------------------------------------------------+
    |                     1NF (Atomic)                      |
    |   +-----------------------------------------------+   |
    |   |         2NF (1NF + No Partial Dependency)     |   |
    |   |   +---------------------------------------+   |   |
    |   |   |    3NF (2NF + No Transitive Dep)      |   |   |
    |   |   |   +-------------------------------+   |   |   |
    |   |   |   |   BCNF (Strict Super Key Det) |   |   |   |
    |   |   |   +-------------------------------+   |   |   |
    |   |   +---------------------------------------+   |   |
    |   +-----------------------------------------------+   |
    +-------------------------------------------------------+
```
- **1NF (First Normal Form):** Every cell must contain atomic (indivisible) values. No multi-valued attributes or repeating groups.
- **2NF (Second Normal Form):** Must be in 1NF and have **no partial dependency**. All non-prime attributes must be fully functionally dependent on the entire Primary Key, not a proper subset of it.
- **3NF (Third Normal Form):** Must be in 2NF and have **no transitive dependency**. If $X \rightarrow Y$, then either $X$ is a Super Key or $Y$ is a prime attribute.
- **BCNF (Boyce-Codd Normal Form):** Stricter version of 3NF. For every non-trivial functional dependency $X \rightarrow Y$, **$X$ must be a Super Key**. Eliminates anomalies where a prime attribute is determined by a non-super-key.

---

## LEC-12: Transactions & ACID Properties
*PDF Reference: Pages 24–25*

### 1. Transaction Definition
- A logical unit of database work containing one or more SQL statements executed in sequential order.
- Must execute completely or be rolled back cleanly if failure occurs.

### 2. ACID Properties
- **Atomicity:** All-or-nothing principle. All operations succeed and reflect in the DB, or all operations are undone.
- **Consistency:** Transactions must transition the database from one valid consistent state (satisfying all integrity constraints) to another.
- **Isolation:** Concurrent transactions execute without interfering with each other. It appears to each transaction that it is running alone.
- **Durability:** Once committed, transaction updates persist permanently, surviving system crashes, reboots, and power failures.

### 3. Transaction State Transition Lifecycle
```
       [Active State]
         /         \
   (Failure)    (R/W Success)
       v             v
  [Failed]    [Partially Committed]
      |          /           \
  (Rollback) (Failure)   (Permanent Store)
      v         v             v
  [Aborted] <---+         [Committed]
      \                       /
       v                     v
            [Terminated]
```
1. **Active:** Initial state; executing read and write operations.
2. **Partially Committed:** Final statement executed; updates buffered in volatile memory, not yet flushed to disk.
3. **Committed:** Updates permanently written to non-volatile disk. No rollback possible.
4. **Failed:** Error encountered during active execution or buffer flushing.
5. **Aborted:** Buffer modifications reversed; database rolled back to prior consistent state.
6. **Terminated:** Final state after either committing or aborting.

---

## LEC-13: Implementing Atomicity & Durability
*PDF Reference: Page 26*

### 1. Shadow-Copy Scheme
- Operates on the premise that only one transaction is active at a time.
- A disk pointer `db-pointer` points to the current active database copy.
- The transaction clones the entire database, applies updates exclusively to the new copy, and leaves the shadow copy untouched.
- **Commit:** System writes all modified pages to disk, then atomically updates `db-pointer` to the new copy.
- **Abort:** System simply deletes the modified copy; old copy is completely unaffected.
- *Limitation:* Extremely inefficient; copying the entire database per transaction is prohibitive for real-world workloads.

### 2. Log-Based Recovery Schemes
- Uses append-only logs stored in stable storage (robust against power and hardware failures) written using **Write-Ahead Logging (WAL)**: log records must reach disk before actual database modifications are applied.
- **Deferred Database Modifications:**
  - Database writes are deferred until the transaction reaches committed state.
  - If crash occurs before commit, log records are discarded (no undo needed).
  - If crash occurs during write execution after commit, system runs `REDO` using commit logs.
- **Immediate Database Modifications:**
  - Active transactions write uncommitted modifications directly to the database.
  - In event of crash:
    - Transactions with active/uncommitted log entries use old-value fields to `UNDO`.
    - Transactions with commit logs use new-value fields to `REDO`.

---

## LEC-14: Indexing in DBMS
*PDF Reference: Pages 27–28*

### 1. Indexing Fundamentals
- Data structure that minimizes disk block I/O accesses when searching records.
- **Search Key:** Copy of primary/candidate key or non-key attribute used for lookup.
- **Data Reference:** Pointer to disk block containing the corresponding record.
- Index files are always stored in sorted order.

### 2. Index Classifications
1. **Primary Index (Clustering Index):**
   - Built on a data file that is already **sequentially ordered**.
   - If sorted on Key attribute: Forms a **Sparse Index** (one entry per disk block).
   - If sorted on Non-Key attribute: Forms a **Dense Index** (one entry per unique non-key value).
2. **Secondary Index (Non-Clustering Index):**
   - Built on **unsorted data files**.
   - Always a **Dense Index** (one entry per record in the data file).
   - Uses more storage, but allows fast queries on non-primary fields.
3. **Dense vs Sparse Indexes:**
   - **Dense:** Contains an index record for *every single search key value* in the file.
   - **Sparse:** Contains index records for only a subset of search key values (typically block pointers). Uses far less memory.
4. **Multi-Level Indexing:**
   - When the primary index itself exceeds main memory, a higher-level sparse index is built on top of the inner index.

---

## LEC-15: NoSQL Databases
*PDF Reference: Pages 29–31*

### 1. Core Paradigm & Drivers
- "Not Only SQL": Non-tabular databases providing flexible schemas, horizontal scaling, and high availability.
- Driven by exponential data growth (Big Data), cloud computing, microservices, and agile iteration where pre-defined schemas are restrictive.

### 2. Four Primary NoSQL Data Models
1. **Key-Value Stores:**
   - Schema: Minimalistic dictionary of unique keys mapped to arbitrary value blobs.
   - Ideal for: User session data, caching, gaming leaderboards, shopping carts.
   - Examples: Redis, Amazon DynamoDB, Oracle NoSQL.
2. **Column-Oriented (Wide-Column / C-Store):**
   - Data stored column by column rather than row by row.
   - Ideal for: High-speed analytics, aggregations, data warehousing.
   - Examples: Apache Cassandra, HBase, Google Bigtable, Snowflake, Redshift.
3. **Document-Based Stores:**
   - Stores semi-structured JSON/BSON documents with embedded hierarchical data.
   - Ideal for: E-commerce catalogs, mobile backends, content management. Supports ACID transactions in modern versions.
   - Examples: MongoDB, CouchDB.
4. **Graph-Based Stores:**
   - Data modeled as Nodes (entities), Edges (relationships), and Properties.
   - Eliminates expensive JOIN operations by traversing physical pointers.
   - Ideal for: Social networks, fraud detection engines, recommendation graphs.
   - Examples: Neo4j, Amazon Neptune.

### 3. Comprehensive Comparison: SQL vs NoSQL
| Feature | SQL Databases (RDBMS) | NoSQL Databases |
|---|---|---|
| **Data Storage Model** | Fixed tables with rows & columns | Documents, Key-Value, Columnar, Graphs |
| **Development History** | 1970s; focused on eliminating data duplication | Late 2000s; focused on scale & developer agility |
| **Examples** | Oracle, MySQL, PostgreSQL, SQL Server | MongoDB, Redis, Cassandra, Neo4j |
| **Schema** | Rigid, pre-defined | Dynamic, schema-free / flexible |
| **Scaling** | Vertical scaling (Scale-Up) | Horizontal scaling (Scale-Out across clusters) |
| **Transactions & ACID**| ACID compliance standard | BASE (Basically Available, Soft-state, Eventual consistency) |
| **Joins** | Heavily required & supported | Rarely required (denormalized / embedded) |
| **Object Mapping** | Requires ORM (Hibernate, Prisma) | Native JSON/document data structure mappings |

---

## LEC-16: Taxonomy of Database Models
*PDF Reference: Pages 32–33*

1. **Relational Databases (RDBMS):**
   - Ubiquitous since 1970s; discrete tables joined by foreign keys; normalized; ACID-compliant.
2. **Object-Oriented Databases (OODBMS):**
   - Data stored as objects incorporating OOP encapsulation, inheritance, and methods.
   - Examples: ObjectDB, GemStone. Limited community adoption compared to RDBMS.
3. **Hierarchical Databases:**
   - Tree-like structure where each parent has multiple children, but each child has **exactly one parent** (1:N).
   - Traversals start at root. Very fast for tree hierarchies, but rigid and inflexible for M:N links. Example: IBM IMS.
4. **Network Databases:**
   - Extension of hierarchical model; records organized in graph structures allowing children to have **multiple parent records** (M:N).
   - Flexible but schema maintenance is complex. Examples: Integrated Data Store (IDS), IDMS.

---

## LEC-17: Database Clustering
*PDF Reference: Page 34*

- **Clustering:** Combining multiple database servers/instances into a unified cluster connecting to a shared dataset.
- **Core Advantages:**
  1. **Data Redundancy:** Replicating identical datasets across nodes prevents data loss during server failures.
  2. **Load Balancing:** Workload distributed across nodes prevents bottlenecking and handles sudden traffic spikes.
  3. **High Availability:** System remains operational and accessible even if individual nodes collapse.

---

## LEC-18: Partitioning & Sharding
*PDF Reference: Page 35*

### 1. Partitioning Concepts
- Dividing massive database objects into smaller, manageable slices called partitions.
- **Vertical Partitioning:** Slicing tables vertically (column-wise). Frequently accessed columns separated from rarely accessed blobs.
- **Horizontal Partitioning:** Slicing tables horizontally (row-wise). Distinct rows stored across different partitions or nodes.

### 2. Sharding (Horizontal Partitioning across Nodes)
- Splitting data across independent database servers with a **Routing Layer** that forwards queries to the correct shard.
- **Pros:** Massive horizontal scalability and high availability.
- **Cons:** High complexity in partition mapping, cross-shard joins are difficult, re-sharding overhead, and the **Scatter-Gather Problem** (analytical queries must query every shard and aggregate results).

---

## Scaling Case Study: Step-by-Step Scaling Patterns
*PDF Reference: Pages 36–47*

### The Problem: Cab Booking Startup
- Starts with ~10 users on a tiny single machine DB handling 1 booking every 5 minutes.
- Grows to 30 bookings/minute &rarr; API latency spikes, deadlocks, starvation, app becomes sluggish.

### The 7 Scaling Patterns
```
Pattern 1: Query Optimisation & Connection Pool (Cache + Conn Pool)
     |
     v
Pattern 2: Vertical Scaling (Scale-Up: upgrade CPU/RAM/SSD)
     |
     v
Pattern 3: CQRS (Command Query Responsibility Segregation: Primary Write, Replicas Read)
     |
     v
Pattern 4: Multi-Primary Replication (Circular ring of writable masters)
     |
     v
Pattern 5: Partitioning by Functionality (Decouple Location, User, Billing DBs)
     |
     v
Pattern 6: Horizontal Scaling / Sharding (Split data by Shard Key across 50 nodes)
     |
     v
Pattern 7: Data Centre Wise Partitioning (Geo-distributed across continents + IPO ready)
```

1. **Pattern 1 &mdash; Query Optimisation & Connection Pooling:**
   - Cache non-dynamic data (user profiles, history) in memory (Redis).
   - Implement connection pool libraries so threads reuse established connections instead of incurring TCP handshake overhead.
2. **Pattern 2 &mdash; Vertical Scaling (Scale-Up):**
   - Upgrade hardware (double RAM, SSD 3x, higher CPU cores).
   - Pocket-friendly initially, but cost increases exponentially and reaches a hardware ceiling.
3. **Pattern 3 &mdash; CQRS (Command Query Responsibility Segregation):**
   - Segregate read and write traffic physically: 1 Primary machine handles all Writes; 2+ Replicas handle all Reads.
   - Challenge: Replication lag between primary and replicas can impact user experience.
4. **Pattern 4 &mdash; Multi-Primary Replication:**
   - Distribute writes across multiple master nodes arranged in a logical circular ring.
   - Any node accepts writes; reads served by whichever node answers broadcast first.
5. **Pattern 5 &mdash; Partitioning of Data by Functionality:**
   - Isolate databases by domain: separate location tables, user tables, and billing tables into distinct DB clusters.
   - Application layer takes responsibility for cross-domain joins.
6. **Pattern 6 &mdash; Horizontal Scaling / Sharding (Scale-Out):**
   - Deploy 50+ nodes sharing the identical schema, each holding a fraction of data based on hash/range sharding key.
   - Requires strong data locality and replica sets per shard.
7. **Pattern 7 &mdash; Data Centre Wise Partitioning:**
   - Multi-continent distribution: Route users to local regional datacenters to minimize intercontinental latency.
   - Enable asynchronous cross-datacenter replication for disaster recovery.

---

## LEC-20: CAP Theorem in Distributed Databases
*PDF Reference: Page 48*

- Formulated by Eric Brewer: A distributed data store can guarantee at most **two out of three** properties simultaneously in the presence of a network partition:
  1. **Consistency (C):** Every read receives the most recent write or an error. All nodes see identical data simultaneously.
  2. **Availability (A):** Every non-failing node returns a non-error response for every request, without guarantee that it contains the latest write.
  3. **Partition Tolerance (P):** The system continues operating despite dropped or delayed messages between nodes.

### Three CAP Database Classifications
- **CA Databases:** Prioritize Consistency and Availability. Cannot tolerate network partitions. Unrealistic in real distributed networks (MySQL / PostgreSQL single-cluster setups).
- **CP Databases:** Prioritize Consistency and Partition Tolerance. When a network partition occurs, inconsistent nodes are shut down until resolved. Essential for banking and financial transactions. Example: **MongoDB**, Spanner.
- **AP Databases:** Prioritize Availability and Partition Tolerance. Nodes remain responsive during partitions and achieve **Eventual Consistency** after reconciliation. Essential for high-uptime platforms like social feeds. Examples: **Apache Cassandra**, Amazon DynamoDB.

---

## LEC-21: The Master-Slave Architecture
*PDF Reference: Page 49*

- Core mechanism to optimize I/O bottlenecks when query volume surges:
  - **Master Database:** Authoritative source for all Write operations (`INSERT`, `UPDATE`, `DELETE`).
  - **Slave Databases:** Replicas that serve all Read queries (`SELECT`).
- Safeguards site reliability, reduces latency, and prevents write contention.
- **Replication Options:**
  - **Synchronous:** Master waits for confirmation from slave before committing. High consistency, higher write latency.
  - **Asynchronous:** Master commits immediately and updates slaves in background. Fast writes, potential replication lag.
