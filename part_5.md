# 📌 Aggregate Functions

### Definition

Aggregate Function একাধিক Row-এর Data নিয়ে একটি Single Result Return করে।

### Formula

```text
Multiple Rows → Single Value
```

### Example

```sql
AVG(gpa)
```

Input:

```text
3.95, 3.60, 3.90, 3.45, 3.75, 3.95, 3.80
```

Output:

```text
3.77
```



### 📊 Common Aggregate Functions

| Function | Purpose |
|-----------|---------|
| `COUNT()` | Row Count |
| `SUM()` | Total Sum |
| `AVG()` | Average Value |
| `MIN()` | Smallest Value |
| `MAX()` | Largest Value |



### 🔢 COUNT()

### Purpose

Table-এ কতগুলো Row আছে তা Count করে।

### Example

```sql
SELECT COUNT(*)
FROM students;
```

### Result

```text
7
```



### ➕ SUM()

### Purpose

Numeric Values-এর Total Sum বের করে।

### Example

```sql
SELECT SUM(marks)
FROM students;
```



### 📈 AVG()

### Purpose

Numeric Values-এর Average বের করে।

### Example

```sql
SELECT AVG(gpa)
FROM students;
```



### 🔽 MIN()

### Purpose

সবচেয়ে ছোট Value Return করে।

### Example

```sql
SELECT MIN(gpa)
FROM students;
```



### 🔼 MAX()

### Purpose

সবচেয়ে বড় Value Return করে।

### Example

```sql
SELECT MAX(gpa)
FROM students;
```

<br>


### 📌 ROUND() Function

<br>

⚠️ `ROUND()` Aggregate Function নয়।

এটি একটি **Numeric Function (Scalar Function)**।

সাধারণত Aggregate Function-এর Result Format করার জন্য ব্যবহার করা হয়।

### Example

```sql
SELECT ROUND(AVG(gpa), 2)
FROM students;
```

### Explanation

- `AVG(gpa)` → Average GPA বের করে
- `ROUND(..., 2)` → Result-কে ২ দশমিক ঘর পর্যন্ত দেখায়

Example:

```text
3.77142857
```

Becomes:

```text
3.77
```


### 📊 Aggregate Function vs Scalar Function

| Type | Works On | Returns |
|--------|----------|----------|
| Aggregate Function | Multiple Rows | Single Value |
| Scalar Function | Single Value | Single Value |

### Example

Aggregate Function:

```sql
AVG(gpa)
```

Scalar Function:

```sql
ROUND(3.77142857, 2)
```



### 📌 Quick Summary

| Function | Category | Purpose |
|----------|----------|----------|
| COUNT() | Aggregate | Count Rows |
| SUM() | Aggregate | Calculate Total |
| AVG() | Aggregate | Calculate Average |
| MIN() | Aggregate | Smallest Value |
| MAX() | Aggregate | Largest Value |
| ROUND() | Scalar | Format Numeric Values |



### 💡 Interview Tips

- Aggregate Functions summarize data.
- Multiple Rows → Single Result.
- Most Common Aggregate Functions:
  - `COUNT()`
  - `SUM()`
  - `AVG()`
  - `MIN()`
  - `MAX()`
- Often used with `GROUP BY`.
- `ROUND()` is **not** an Aggregate Function.
- `ROUND()` is commonly used to format the output of Aggregate Functions.



### 🔥 Golden Rule

> Aggregate Functions take multiple rows and return a single value.

> `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()` are Aggregate Functions.

> `ROUND()` is a Scalar Function used to format numeric results.

<br>


## 📌 GROUP BY

### Definition

`GROUP BY` একটি Column-এর ভিত্তিতে Data-কে Group করে এবং প্রতিটি Group-এর উপর Aggregate Function চালায়।

### Concept

Without `GROUP BY`

```text
Whole Table → 1 Result
```

With `GROUP BY`

```text
Each Group → 1 Result
```



### Example

### Without GROUP BY

```sql
SELECT COUNT(*) AS total
FROM students;
```

### Result

```text
7
```

এখানে পুরো Table-এর জন্য একটি Summary Result পাওয়া যায়।


### With GROUP BY

```sql
SELECT course,
       COUNT(*) AS students_count,
       ROUND(AVG(gpa), 2) AS avg_gpa
FROM students
GROUP BY course;
```

### Result

```text
Django        → 2 Students
Python        → 1 Student
ML            → 1 Student
DL            → 1 Student
Data Analysis → 1 Student
Agentic AI    → 1 Student
```

এখানে প্রতিটি Course আলাদা Group হিসেবে বিবেচিত হয়েছে।



### 📊 Common Aggregate Functions with GROUP BY

নিচের Aggregate Functions-গুলো সাধারণত `GROUP BY`-এর সাথে ব্যবহার করা হয়:

| Function | Purpose |
|----------|----------|
| `COUNT()` | Row Count |
| `SUM()` | Total Sum |
| `AVG()` | Average Value |
| `MIN()` | Smallest Value |
| `MAX()` | Largest Value |


### 🔹 COUNT() with GROUP BY

```sql
SELECT course,
       COUNT(*) AS total_students
FROM students
GROUP BY course;
```

প্রতিটি Course-এ কতজন Student আছে তা দেখাবে।


### 🔹 AVG() with GROUP BY

```sql
SELECT course,
       AVG(gpa) AS avg_gpa
FROM students
GROUP BY course;
```

প্রতিটি Course-এর Average GPA দেখাবে।



### 🔹 MAX() with GROUP BY

```sql
SELECT course,
       MAX(gpa) AS highest_gpa
FROM students
GROUP BY course;
```

প্রতিটি Course-এর Highest GPA দেখাবে।


### 💡 Important Rule

`SELECT`-এ থাকা প্রতিটি Column অবশ্যই:

- `GROUP BY`-তে থাকতে হবে, অথবা
- Aggregate Function-এর ভিতরে থাকতে হবে।



### ✅ Correct

```sql
SELECT course,
       COUNT(*)
FROM students
GROUP BY course;
```

কারণ:

- `course` → GROUP BY-তে আছে
- `COUNT(*)` → Aggregate Function



### ❌ Wrong

```sql
SELECT course,
       name,
       COUNT(*)
FROM students
GROUP BY course;
```

কারণ:

- `course` → GROUP BY-তে আছে
- `COUNT(*)` → Aggregate Function
- `name` → Neither grouped nor aggregated

PostgreSQL Error দিবে।


<br>

### 📌 GROUP BY vs Aggregate Function

Without GROUP BY:

```sql
SELECT AVG(gpa)
FROM students;
```

Result:

```text
Whole Table Average GPA
```

With GROUP BY:

```sql
SELECT course,
       AVG(gpa)
FROM students
GROUP BY course;
```

Result:

```text
Average GPA for each course
```



### 📌 Quick Comparison

| Without GROUP BY | With GROUP BY |
|------------------|---------------|
| Whole Table Summary | Group-wise Summary |
| Single Result | Multiple Results |
| One Aggregate Value | One Aggregate Value per Group |



### 🧠 Quick Memory Trick

```text
No GROUP BY → Whole Table Summary

GROUP BY → Group-wise Summary
```



### 💡 Interview Tips

- `GROUP BY` Data-কে Group করে।
- প্রতিটি Group-এর উপর Aggregate Function চালানো হয়।
- `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()` সবচেয়ে বেশি ব্যবহৃত হয়।
- `SELECT`-এর Non-Aggregated Column অবশ্যই `GROUP BY`-তে থাকতে হবে।
- `GROUP BY` ছাড়া Aggregate Function পুরো Table-এর উপর কাজ করে।


### 🔥 Golden Rule

> Without `GROUP BY` → Aggregate Function works on the entire table.

> With `GROUP BY` → Aggregate Function works on each group separately.

> Every non-aggregated column in `SELECT` must appear in the `GROUP BY` clause.

<br>

## 📌 HAVING Clause

### Definition

`HAVING` Grouped Data Filter করতে ব্যবহৃত হয়।

- `WHERE` → Rows Filter করে  
- `HAVING` → Groups Filter করে  



### 🔄 WHERE vs HAVING

#### ✅ WHERE

Aggregation-এর আগে Row Filter করে।

```sql
SELECT *
FROM students
WHERE gpa > 3.80;
```



#### ✅ HAVING

Aggregation-এর পরে Group Filter করে।

```sql
SELECT course,
       ROUND(AVG(gpa), 2) AS avg_gpa
FROM students
GROUP BY course
HAVING AVG(gpa) > 3.80;
```



### 📊 Common Usage

### 🔹 Groups with more than 2 students

```sql
SELECT course, COUNT(*)
FROM students
GROUP BY course
HAVING COUNT(*) > 2;
```


### 🔹 Groups with average GPA above 3.80

```sql
SELECT course, AVG(gpa)
FROM students
GROUP BY course
HAVING AVG(gpa) > 3.80;
```



### ❌ Common Mistake

### Wrong

```sql
SELECT course, AVG(gpa)
FROM students
WHERE AVG(gpa) > 3.80
GROUP BY course;
```

### ❗ Why wrong?

- `WHERE` aggregate function handle করতে পারে না
- Aggregation এর পর filter করতে হয়


### ✅ Correct

```sql
SELECT course, AVG(gpa)
FROM students
GROUP BY course
HAVING AVG(gpa) > 3.80;
```



### ⚙️ Query Execution Order

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
SELECT
 ↓
ORDER BY
 ↓
LIMIT
```



### 🧠 Quick Memory Trick

```text
WHERE  → Filter Rows
HAVING → Filter Groups
```



### 💡 Interview Tips

- `WHERE` aggregation-এর আগে কাজ করে
- `HAVING` aggregation-এর পরে কাজ করে
- `WHERE`-এ `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` ব্যবহার করা যায় না
- Aggregate Result filter করতে সবসময় `HAVING` ব্যবহার করতে হবে
- `HAVING` সাধারণত `GROUP BY`-এর সাথে ব্যবহার করা হয়



### 🔥 Golden Rule

> WHERE filters individual rows  
> HAVING filters grouped results  

> Aggregation-based filtering = HAVING


## 📌 Common SQL Mistakes to Avoid



### ❌ Mistake 1: WHERE with Aggregates

`WHERE` দিয়ে aggregate function ব্যবহার করা।

#### ❌ Wrong

```sql
WHERE AVG(gpa) > 3.80;
```

#### ✅ Correct

```sql
HAVING AVG(gpa) > 3.80;
```

### 💡 Reason

- `WHERE` কাজ করে **GROUP BY-এর আগে**
- Aggregate value তখনো তৈরি হয় না



### ❌ Mistake 2: Non-grouped column without aggregate

#### ❌ Wrong

```sql
SELECT course, name, COUNT(*)
FROM students
GROUP BY course;
```

#### ✅ Correct

```sql
SELECT course, COUNT(*)
FROM students
GROUP BY course;
```

### 💡 Reason

- `name` না `GROUP BY`-তে আছে
- না কোনো aggregate function-এর ভিতরে আছে
→ তাই SQL error দেয়


### ❌ Mistake 3: Aggregate on Text Column

#### ❌ Wrong

```sql
SELECT AVG(course)
FROM students;
```

#### ✅ Correct

```sql
SELECT AVG(gpa)
FROM students;
```

#### 💡 Reason

- `AVG(), SUM(), MIN(), MAX()` শুধু **numeric column**-এ কাজ করে
- Text data-এর উপর কাজ করে না



### ❌ Mistake 4: Not Using ROUND()

#### ❌ Ugly Output

```sql
SELECT AVG(gpa)
FROM students;
-- 3.771428571428571
```

#### ✅ Clean Output

```sql
SELECT ROUND(AVG(gpa), 2)
FROM students;
-- 3.77
```

#### 💡 Reason

- Default output অনেক বেশি decimal দেয়
- `ROUND()` ব্যবহার করলে result clean ও readable হয়


### 📊 Quick Summary

- WHERE ❌ aggregates → HAVING ✅
- GROUP BY rule always follow করতে হবে
- Aggregates only work on numeric data
- `ROUND()` ব্যবহার করলে output clean হয়



### 🔥 Golden Rules

> WHERE = row-level filtering (before aggregation)

> HAVING = group-level filtering (after aggregation)

> Aggregates always need correct column type (numeric)

<br>

## 📌 SQL String Functions: TRIM() & REPLACE()

### ✂️ TRIM()

### Definition

`TRIM()` String-এর শুরু এবং শেষের অতিরিক্ত Space অথবা নির্দিষ্ট Character Remove করে।



### Syntax

```sql
TRIM(string)
```



### Example

```sql
SELECT TRIM('   Hello World   ');
```

### Output

```text
Hello World
```



### Remove Specific Character

```sql
SELECT TRIM('x' FROM 'xxxHelloxxx');
```

### Output

```text
Hello
```



### Use Cases

- User Input Clean করা
- Extra Spaces Remove করা
- Data Validation
- Imported Data Cleanup



### 🔄 REPLACE()

### Definition

`REPLACE()` String-এর নির্দিষ্ট অংশ খুঁজে অন্য Value দিয়ে Replace করে।


### Syntax

```sql
REPLACE(string, old_value, new_value)
```



### Example

```sql
SELECT REPLACE('I love Java', 'Java', 'PostgreSQL');
```

### Output

```text
I love PostgreSQL
```



### Multiple Occurrences

```sql
SELECT REPLACE('aaa-bbb-aaa', 'aaa', 'xxx');
```

### Output

```text
xxx-bbb-xxx
```



### Use Cases

- Text Correction
- Data Cleaning
- URL Modification
- String Formatting
- Updating Old Values



### 📊 Quick Comparison

| Function | Purpose |
|----------|---------|
| `TRIM()` | Remove Spaces / Characters |
| `REPLACE()` | Replace Text |



### 💡 Interview Tips

### TRIM Example

```sql
SELECT TRIM('   Arfan   ');
```

### Result

```text
Arfan
```



### REPLACE Example

```sql
SELECT REPLACE('Hello Java', 'Java', 'SQL');
```

### Result

```text
Hello SQL
```



### 📌 TRIM vs REPLACE

| Feature | TRIM() | REPLACE() |
|----------|---------|-----------|
| Removes Spaces | ✅ | ❌ |
| Removes Specific Character | ✅ | ❌ |
| Replaces Text | ❌ | ✅ |
| Data Cleaning | ✅ | ✅ |


### 🧠 Memory Trick

```text
TRIM    → Remove
REPLACE → Change
```



### 📌 Quick Summary

- `TRIM()` → String-এর শুরু ও শেষ থেকে Space বা Character Remove করে
- `REPLACE()` → String-এর নির্দিষ্ট অংশ Replace করে
- দুটোই Data Cleaning এবং Text Processing-এর জন্য খুব গুরুত্বপূর্ণ



### 🔥 Golden Rule

> Use `TRIM()` when you need to remove unwanted spaces or characters.

> Use `REPLACE()` when you need to change one text value into another.


## 📌 ALTER TABLE & CHECK Constraint



### 🔧 ALTER TABLE

### Definition

`ALTER TABLE` Existing Table-এর Structure Modify করতে ব্যবহৃত হয়।



### Common Operations

- Rename Column
- Add Column
- Drop Column
- Add Constraint
- Remove Constraint



### 🔄 Rename Column

### Syntax

```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```



### Example

```sql
ALTER TABLE student
RENAME COLUMN name TO full_name;
```


### Verify

```sql
SELECT * FROM student;
```

### Result

```text
name → full_name
```



### ➕ Add Column

```sql
ALTER TABLE student
ADD COLUMN email VARCHAR(255);
```



### ❌ Drop Column

```sql
ALTER TABLE student
DROP COLUMN email;
```



## 🔐 CHECK Constraint

### Definition

`CHECK` Constraint নির্দিষ্ট Condition অনুযায়ী Data Validation করে।

- Condition TRUE হলে → Data Insert/Update হবে  
- Condition FALSE হলে → Error দেখাবে  



### Syntax

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
CHECK (condition);
```



### Example

```sql
ALTER TABLE student
ADD CONSTRAINT chk_age
CHECK (age >= 5 AND age <= 25);
```



### ✅ Valid Data

```sql
INSERT INTO student(age)
VALUES (20);
```

### Result

```text
Success
```



### ❌ Invalid Data

```sql
INSERT INTO student(age)
VALUES (30);
```

### Result

```text
ERROR: CHECK constraint violation
```


### 📊 Quick Summary

| Command | Purpose |
|---------|----------|
| ALTER TABLE | Modify table structure |
| RENAME COLUMN | Change column name |
| ADD COLUMN | Add new column |
| DROP COLUMN | Remove column |
| CHECK | Validate data rules |



### 💡 Interview Tips

- `ALTER TABLE` → Existing table modify করার জন্য
- `RENAME COLUMN` → Column name change
- `CHECK` → Business rules enforce করে
- Constraint name দেওয়া best practice



### 🧠 Memory Trick

```text
ALTER TABLE → Modify Structure
CHECK       → Validate Data
```



### 🔥 Golden Rule

> Use `ALTER TABLE` when you need to change table structure.

> Use `CHECK` when you need to enforce data validation rules.