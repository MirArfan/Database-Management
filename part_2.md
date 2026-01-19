### 🔹 Database Normalization


Normalization হলো ডাটাবেস ডিজাইন করার প্রক্রিয়া যাতে:

- Data redundancy কমে  
- Data integrity বজায় থাকে  

**Goal:** Efficient & consistent data storage

<br>

### ✅  Relationships (রিলেশনশিপস)


Relationships define how tables are connected.

### Types
- **One-to-One (1:1)**  
  One row in a table ↔ one row in another table
- **One-to-Many (1:N)**  
  One row ↔ multiple rows
- **Many-to-Many (M:N)**  
  Multiple rows ↔ multiple rows  
  *(Requires a junction/bridge table)*

<br>

### 1️⃣ First Normal Form (1NF)

### Rule
- Table-এ repeating groups বা multiple values in a column থাকবে না  
- Atomic values থাকতে হবে  

### Example

**Before 1NF:**

| StudentID | Name | Courses        |
|----------|------|----------------|
| 1        | Ali  | Math, Physics  |
| 2        | Sara | English        |

**Problem:**  
Courses column এ multiple values আছে

**After 1NF:**

| StudentID | Name | Course   |
|----------|------|----------|
| 1        | Ali  | Math     |
| 1        | Ali  | Physics  |
| 2        | Sara | English  |

✅ Atomic values, no repeating groups


### 2️⃣ Second Normal Form (2NF)

### Rule
- 1NF follow করবে  
- Table-এর সব non-key attributes **fully dependent** হবে primary key এর উপর  
- Partial dependency থাকবে না  

### Example

**Before 2NF:**

| StudentID | Course  | Instructor | Dept    |
|----------|---------|------------|---------|
| 1        | Math    | Mr. Khan   | Science |
| 1        | Physics | Mrs. Roy   | Science |

**Problem:**  
Dept শুধু Course এর উপর নির্ভর করছে, পুরো primary key  
(StudentID + Course) এর উপর নয়

**After 2NF (Split into two tables):**

**StudentCourses**

| StudentID | Course  |
|----------|---------|
| 1        | Math    |
| 1        | Physics |

**Courses**

| Course  | Instructor | Dept    |
|--------|------------|---------|
| Math   | Mr. Khan   | Science |
| Physics| Mrs. Roy   | Science |

✅ No partial dependency



### 3️⃣ Third Normal Form (3NF)

### Rule
- 2NF follow করবে  
- Non-key attribute আরেকটি non-key attribute এর উপর dependent হবে না  
- Transitive dependency থাকবে না  

### Example

**Before 3NF:**

| StudentID | Name | Dept    | DeptHead   |
|----------|------|---------|------------|
| 1        | Ali  | Science | Dr. Ahmed  |
| 2        | Sara | Arts    | Dr. Karim  |

**Problem:**  
DeptHead transitively dependent on Dept

**After 3NF (Split):**

**Students**

| StudentID | Name | Dept    |
|----------|------|---------|
| 1        | Ali  | Science |
| 2        | Sara | Arts    |

**Departments**

| Dept    | DeptHead   |
|--------|------------|
| Science| Dr. Ahmed  |
| Arts   | Dr. Karim  |

✅ No transitive dependency



### 4️⃣ Boyce-Codd Normal Form (BCNF)

### Rule
- 3NF follow করবে  
- Table-এ **every determinant must be a candidate key**

### Example

**Before BCNF:**

| Course  | Instructor | Room |
|--------|------------|------|
| Math   | Mr. Khan   | R101 |
| Physics| Mrs. Roy   | R102 |

**Problem:**  
Suppose: Instructor → Room  
Instructor হলো non-key attribute কিন্তু determinant → violates BCNF

**After BCNF (Split):**

**CourseInstructor**

| Course  | Instructor |
|--------|------------|
| Math   | Mr. Khan   |
| Physics| Mrs. Roy   |

**InstructorRoom**

| Instructor | Room |
|------------|------|
| Mr. Khan   | R101 |
| Mrs. Roy   | R102 |

✅ All determinants are candidate keys

<br>

### 🔹 Quick Summary

| Normal Form | Rule | Key Example |
|------------|------|-------------|
| 1NF | Atomic values, no repeating groups | Split multi-value columns |
| 2NF | Fully dependent on PK, no partial dependency | Split tables if column depends on part of PK |
| 3NF | No transitive dependency | Move dependent column to separate table |
| BCNF | Every determinant = candidate key | Remove non-key determinants |

<br>

### 1️⃣ SQL (Structured Query Language) Databases


- SQL databases are **Relational Databases (RDBMS)**  
- Data is stored in **tables (rows & columns)**  
- Supports relationships using **Primary Key & Foreign Key**  
- Uses **SQL language** to query and manage data  


### Examples
- MySQL  
- PostgreSQL  
- Oracle  
- SQL Server  


### 2️⃣ NoSQL (Not Only SQL) Databases


- NoSQL databases are **non-relational**  
- Data is stored in different formats  
  (document, key-value, column, graph)  
- **Schema-less** (flexible structure)  
- Great for **big data & real-time applications**

 

### Examples
- MongoDB  
- Cassandra  
- Redis  
- Neo4j  


<br>

### 3️⃣ Key Differences Between SQL and NoSQL

| Feature | SQL (RDBMS) | NoSQL |
|------|-----------|-------|
| Data Model | Relational (Tables) | Non-relational (Document, Key-Value, Graph, Column) |
| Schema | Fixed schema | Schema-less / Flexible |
| Query Language | SQL | Varies (JSON, API calls, custom query) |
| Scalability | Vertical scaling (add CPU, RAM) | Horizontal scaling (add servers) |
| Transactions | Strong ACID support | BASE model |
| Best For | Structured data, complex queries, strong consistency | Large-scale, unstructured/semi-structured data, high performance |



### 4️⃣ Use Cases

### SQL
- Banking systems (transactions must be accurate)  
- HR systems  
- E-commerce order management  

### NoSQL
- Social media apps (Instagram, Facebook, Twitter)  
- Real-time chat apps (WhatsApp, Messenger)  
- Big data analytics (Netflix, Spotify recommendations)  



<br>

### ❓ Interview Questions & Answers

### ✅ Q1: What is the main difference between SQL and NoSQL?
**Answer:**  
- **SQL** → Relational, structured, fixed schema, ACID compliance  
- **NoSQL** → Non-relational, flexible schema, highly scalable, BASE model  


### ✅ Q2: When would you choose NoSQL over SQL?
**Answer:**  
- If the application needs **scalability, flexibility**, and handles **unstructured data**  
  (e.g., social media, IoT, real-time apps) → **NoSQL**  
- If the system needs **transactions, strong consistency**, and **structured data** → **SQL**



### ✅ Q4: Which is faster – SQL or NoSQL?
**Answer:**  
Depends on use case:
- Complex queries & transactions → **SQL**  
- Large-scale, high-performance, real-time applications → **NoSQL**



### ✅ Q5: Explain Vertical vs Horizontal Scaling in context of SQL and NoSQL.
**Answer:**  
- **SQL** → Supports **Vertical Scaling** (upgrade hardware: more RAM, CPU)  
- **NoSQL** → Supports **Horizontal Scaling** (add more servers/nodes)

<br>
<br>

### 📌 SQL Database Categories

### 1️⃣ Open Source SQL Databases

 
Free to use, community-supported, widely used for web applications.

>ফ্রি, কমিউনিটি সাপোর্টেড, ওয়েব অ্যাপ্লিকেশনে বহুল ব্যবহৃত।

**Examples:**
- **MySQL** – Popular for web apps, WordPress, e-commerce  
- **PostgreSQL** – Advanced, supports JSON, GIS data, ACID compliant  
- **SQLite** – Lightweight, embedded in mobile apps & browsers, no server needed  
- **MariaDB** – MySQL fork, open-source with extra features  

<br>

### 📊 SQL Databases – Summary Table

| Category | SQL Databases |  |
|--------|---------------|----------------|
| Open Source | MySQL, PostgreSQL, SQLite, MariaDB | ফ্রি, ওয়েব ও ছোট-মাঝারি অ্যাপের জন্য |
| Commercial | Oracle, SQL Server, IBM Db2, SAP HANA | পেইড, বড় কোম্পানি ও ব্যাংকিং সিস্টেমে ব্যবহৃত |
| Cloud | Amazon RDS, Google Cloud SQL, Azure SQL, Amazon Aurora | ক্লাউডে managed service, scalable |
| Special Purpose | SQLite, Teradata, Snowflake | মোবাইল, ডেটা ওয়্যারহাউস, অ্যানালিটিক্সের জন্য |



### ✅ Interview Shortcut (SQL)

- Small apps → **SQLite**  
- Web apps → **MySQL / PostgreSQL**  
- Enterprise → **Oracle / SQL Server / Db2**  
- Cloud-based → **AWS RDS / Aurora / Google Cloud SQL**  
- Data warehouse → **Teradata / Snowflake**

<br>

### 📌 NoSQL Database Categories

NoSQL ডেটাবেসগুলো সাধারণত চারটি বড় ক্যাটাগরিতে ভাগ হয়:  
**Document, Key-Value, Column, Graph**



### 1️⃣ Document-Oriented Databases


- Data stored as documents (JSON, BSON, XML)  
- Schema-less, flexible structure  
- Best for semi-structured data  


**Examples:**
- MongoDB  
- CouchDB  
- RavenDB  
- Firebase Firestore  



### 2️⃣ Key-Value Stores

- Data stored as key-value pairs  
- Very fast for simple queries  
- Best for caching, session storage, real-time apps  

  

**Examples:**
- Redis  
- Amazon DynamoDB  
- Riak  
- Aerospike  



### 3️⃣ Column-Oriented Databases


- Data stored in columns instead of rows  
- Optimized for analytical queries and big data  
- Best for data warehousing  


**Examples:**
- Apache Cassandra  
- HBase  
- Amazon Redshift  
- ScyllaDB  



### 4️⃣ Graph Databases


- Data stored as nodes and edges  
- Best for social networks, recommendation engines, fraud detection  


**Examples:**
- Neo4j  
- Amazon Neptune  
- ArangoDB  
- OrientDB  

<br>

### 📊 NoSQL Databases – Summary Table

| Category | Examples | বাংলা ব্যাখ্যা |
|--------|----------|----------------|
| Document | MongoDB, CouchDB, Firestore | JSON/BSON আকারে ডেটা সংরক্ষণ |
| Key-Value | Redis, DynamoDB, Riak | Key-Value pair আকারে ডেটা |
| Column | Cassandra, HBase, Redshift | Column-wise storage, big data analytics |
| Graph | Neo4j, Neptune, ArangoDB | Node-Edge আকারে ডেটা, relationship heavy apps |



### ✅ Interview Shortcut (NoSQL)

- Document DB → **MongoDB** (flexible schema)  
- Key-Value DB → **Redis** (fast caching, session management)  
- Column DB → **Cassandra / HBase** (big data, analytics)  
- Graph DB → **Neo4j** (social networks, relationships)

### 📌 SQL vs NoSQL – Interview Questions & Answers



### ❓ Q1. What is the main difference between SQL and NoSQL databases?

**Answer:**
- **SQL** → Relational, structured, fixed schema, ACID compliant  
- **NoSQL** → Non-relational, flexible schema, highly scalable, BASE model  



### ❓ Q2. Why would you choose MongoDB over MySQL in a project?

**Answer:**
- If the data is unstructured or semi-structured (JSON-like documents)  
- If you need flexibility in schema (frequent changes)  
- If the application requires horizontal scaling  



### ❓ Q3. When is SQL a better choice than NoSQL?

**Answer:**
- When data is structured and relationships are important  
- When the system needs transactions (banking, finance)  
- When complex queries and ACID compliance are required  



### ❓ Q4. Can we use SQL and NoSQL together in a project?

**Answer:**
- Yes, this is called **Polyglot Persistence**  
- Example:  
  - SQL (MySQL/PostgreSQL) → transactions & structured data  
  - NoSQL (MongoDB/Redis) → caching, logging, real-time analytics  



### ❓ Q5. Which is faster – SQL or NoSQL?

**Answer:**
- SQL → Faster for complex queries & transactions  
- NoSQL → Faster for large-scale, unstructured data & real-time performance  



### ❓ Q6. Example Scenario Question  
**Q:** Suppose you are building an E-commerce website. Which database would you choose and why?

**Answer:**
- Use **SQL (MySQL/PostgreSQL)** for Users, Orders, Payments  
  - Reason: Transactions must be accurate and consistent  
- Use **NoSQL (MongoDB/Redis)** for product catalogs, browsing history, caching  
  - Reason: Fast retrieval and flexible schema  



### ❓ Q7. Explain Vertical vs Horizontal Scaling in context of SQL & NoSQL.

**Answer:**
- **SQL** → Vertical Scaling (increase RAM/CPU in one machine)  
- **NoSQL** → Horizontal Scaling (add more servers/nodes)  


### ❓ Project-Based Interview Question

### ❓ Q: Why did you choose MongoDB for your project?

**Answer (English):**  
I chose MongoDB because it is a NoSQL, document-oriented database that provides flexibility in schema design. My project deals with dynamic and unstructured data, and MongoDB allows storing JSON-like documents without fixed schemas. It also supports horizontal scaling, which helps handle large amounts of data in the future.

>আমি MongoDB ব্যবহার করেছি কারণ এটি একটি NoSQL, document-oriented ডাটাবেস। আমার প্রজেক্টে ডেটা অনেক dynamic ও unstructured, আর MongoDB JSON-like document আকারে flexible ভাবে ডেটা স্টোর করতে দেয়। এছাড়া MongoDB সহজে horizontal scaling সাপোর্ট করে, তাই ভবিষ্যতে ডেটা বাড়লেও সমস্যা হবে না।

