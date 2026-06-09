## 📌 Database Notes: Numeric Data Types & Variations

### 1. PostgreSQL Numeric Data Types

#### Exact Numbers (নিখুঁত সংখ্যা)

<br>

| Data Type | Storage | Range | Use Case |
|------------|----------|---------|----------|
| **SMALLINT** | 2 Bytes | -32,768 to 32,767 | ছোট সংখ্যা, Status Code, Flags |
| **INTEGER (INT)** | 4 Bytes | -2,147,483,648 to 2,147,483,647 | IDs, বয়স, Count, সাধারণ সংখ্যার জন্য সবচেয়ে বেশি ব্যবহৃত |
| **BIGINT** | 8 Bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | বিশাল বড় ID, Large Counters, Timestamps |
| **DECIMAL / NUMERIC** | Variable | Up to 131,072 digits before decimal point | Money, Financial Calculations, Precise Decimal Values |

<br>

### Floating-Point Numbers (আনুমানিক / Approximate Numbers)

| Data Type | Storage | Precision | Use Case |
|------------|----------|-----------|----------|
| **REAL** | 4 Bytes | ~6 Decimal Digits | Scientific Data, Sensor Values |
| **DOUBLE PRECISION** | 8 Bytes | ~15 Decimal Digits | High Precision Mathematical Calculations |

<br>

### 2. Exact Numbers vs Floating-Point Numbers

### Exact Numbers

✅ Stored exactly as entered.

✅ No rounding errors.

✅ Best choice for:

- Money
- Financial calculations
- Inventory quantities
- Business-critical data

Example:

```sql
price NUMERIC(10,2)
```

```sql
10.25 + 20.10 = 30.35
```

Result is always accurate.

---

### Floating-Point Numbers

⚠️ Stored approximately using IEEE-754 format.

⚠️ Small rounding errors may occur.

✅ Best choice for:

- Scientific calculations
- Physics simulations
- Sensor measurements
- Graphics processing

Example:

```sql
0.1 + 0.2
```

May internally become:

```sql
0.30000000000000004
```

❌ Avoid `REAL` and `DOUBLE PRECISION` for financial calculations.

---

## 3. SQL Ecosystem Comparison

| PostgreSQL | MySQL | SQL Server |
|------------|--------|------------|
| SMALLINT | SMALLINT | SMALLINT |
| INTEGER / INT | INT / INTEGER | INT |
| BIGINT | BIGINT | BIGINT |
| REAL | FLOAT | FLOAT(24) |
| DOUBLE PRECISION | DOUBLE | FLOAT(53) |
| NUMERIC / DECIMAL | DECIMAL | DECIMAL |

---

### 4. Important Notes

### INT vs INTEGER

- `INT` এবং `INTEGER` একই Data Type।
- শুধু নামের পার্থক্য।
- PostgreSQL এবং MySQL-এ দুটোই ব্যবহার করা যায়।

Example:

```sql
age INT;
```

```sql
age INTEGER;
```

উভয়ই একই Data Type।

---

### DECIMAL vs NUMERIC

PostgreSQL-এ:

```sql
DECIMAL(10,2)
```

এবং

```sql
NUMERIC(10,2)
```

সম্পূর্ণ একই।

✅ Financial Data-এর জন্য Recommended।

---

### 5. Interview Tips

### Q: Money Store করতে কোন Data Type ব্যবহার করবে?

✅ `NUMERIC`

✅ `DECIMAL`

❌ `REAL`

❌ `DOUBLE PRECISION`

---

### Q: User ID-এর জন্য কোন Data Type?

| System Size | Recommended Type |
|------------|------------------|
| Small System | INTEGER |
| Large Scale System | BIGINT |

---

### Q: REAL এবং DOUBLE PRECISION-এর মধ্যে পার্থক্য?

| Type | Storage | Precision |
|--------|----------|-----------|
| REAL | 4 Bytes | ~6 Digits |
| DOUBLE PRECISION | 8 Bytes | ~15 Digits |

---

### 📌 Quick Summary

| Requirement | Recommended Data Type |
|-------------|-----------------------|
| Small Integer | SMALLINT |
| General Integer | INTEGER / INT |
| Very Large Integer | BIGINT |
| Money / Financial Data | NUMERIC / DECIMAL |
| Scientific Data | REAL |
| High Precision Scientific Data | DOUBLE PRECISION |

### Golden Rule

> Use **NUMERIC / DECIMAL** for money and financial calculations.
>
> Use **REAL / DOUBLE PRECISION** only when small rounding errors are acceptable.

<br>


## 📌 Character String Data Types (PostgreSQL)

### 1. CHAR(n) — Fixed-Length String

### Features

- নির্দিষ্ট দৈর্ঘ্যের (Fixed Length) String Store করে।
- ইনপুট ছোট হলে বাকি অংশ Space (` `) দিয়ে Padding করা হয়।
- Storage সবসময় `n` Character-এর সমান থাকে।

### Example

```sql
CREATE TABLE users (
    country_code CHAR(2)
);
```

```sql
INSERT INTO users VALUES ('BD');
```

Stored Value:

```text
'BD'
```

(যদি Length কম হয়, PostgreSQL Internalভাবে Space Padding করতে পারে।)

### Use Cases

- Country Code (`BD`, `US`, `UK`)
- Gender (`M`, `F`)
- Fixed-Length Identification Codes

<br>

### 2. VARCHAR(n) — Variable-Length String

### Features

- Variable-Length String Store করে।
- সর্বোচ্চ `n` Characters পর্যন্ত Store করা যায়।
- প্রয়োজনের অতিরিক্ত Space ব্যবহার করে না।
- PostgreSQL-এ সবচেয়ে বেশি ব্যবহৃত String Data Type।

### Example

```sql
CREATE TABLE users (
    username VARCHAR(50)
);
```

```sql
INSERT INTO users VALUES ('arfan');
```

### Use Cases

- Username
- Email Address
- Full Name
- Address
- Title

<br>

### 3. TEXT — Large Variable-Length String

### Features

- Length Specify করার প্রয়োজন নেই।
- বিশাল পরিমাণ Text Store করা যায়।
- PostgreSQL-এ `TEXT` এবং `VARCHAR`-এর Performance প্রায় একই।
- Length Restriction না থাকলে এটি ব্যবহার করা সুবিধাজনক।

### Example

```sql
CREATE TABLE blogs (
    content TEXT
);
```

### Use Cases

- Blog Posts
- Comments
- Articles
- Product Descriptions
- Documentation Content



## 4. Quick Comparison

| Data Type | Fixed Length | Maximum Length |
|------------|-------------|----------------|
| CHAR(n) | ✅ Yes | n Characters |
| VARCHAR(n) | ❌ No | n Characters |
| TEXT | ❌ No | ~1 GB |



## 5. Interview Tips

### Q: Fixed-Size Data-এর জন্য কোন Type ব্যবহার করবে?

✅ `CHAR(n)`

Examples:

- Country Code
- Gender
- Fixed-Length Codes

---

### Q: Most Commonly Used String Data Type কোনটি?

✅ `VARCHAR(n)`

কারণ:

- Flexible
- Space Efficient
- Length Restriction দেওয়া যায়

---

### Q: Blog Content বা Large Description Store করতে কোন Type ব্যবহার করবে?

✅ `TEXT`

কারণ:

- Length Restriction নেই
- Large Text Store করতে পারে



## 📌 Best Practice

| Scenario | Recommended Type |
|-----------|------------------|
| Country Code | CHAR(2) |
| Gender | CHAR(1) |
| Username | VARCHAR(50) |
| Email | VARCHAR(255) |
| Address | VARCHAR(255) |
| Blog Content | TEXT |
| Product Description | TEXT |


<br>

## 📌 Date & Time Data Types (PostgreSQL)

### 1. DATE

### Features

- শুধু তারিখ store করে (time থাকে না)
- Format: `YYYY-MM-DD`

### Use Case

- DOB (Date of Birth)
- Event date



### 2. TIME

### Features

- শুধু সময় store করে (date থাকে না)
- Format: `HH:MM:SS`

### Use Case

- Office hours
- Class schedule


### 3. TIMESTAMP

### Features

- Date + Time একসাথে store করে
- Timezone থাকে না
- Format: `YYYY-MM-DD HH:MM:SS`

### Use Case

- created_at
- logs


### 4. TIMESTAMPTZ

### Features

- Date + Time + Timezone store করে
- Best for global applications
- Format: `YYYY-MM-DD HH:MM:SS+TZ`

### Use Case

- Global apps
- Meetings
- Distributed systems



### 5. INTERVAL

### Features

- Time duration / difference store করে
- Format: `2 years 3 months`

### Use Case

- Subscription period
- Age difference



## 📊 Quick Comparison

| Data Type   | Stores      | Timezone | Use Case |
|-------------|------------|----------|----------|
| DATE        | Date only   | ❌       | DOB, Events |
| TIME        | Time only   | ❌       | Schedule |
| TIMESTAMP   | Date + Time | ❌       | Logs, created_at |
| TIMESTAMPTZ | Date + Time | ✅       | Global apps |
| INTERVAL    | Duration    | ❌       | Subscription, age |

---


# 📌 Database Constraints

Database Constraints ব্যবহার করা হয় Data Integrity বজায় রাখার জন্য। এগুলো নিশ্চিত করে যে Database-এ শুধুমাত্র Valid Data Insert বা Update করা যাবে।

---

## 🔑 PRIMARY KEY

### Features

- Unique হতে হবে
- NULL allowed নয়
- প্রতি টেবিলে মাত্র ১টি Primary Key থাকে
- Automatically Unique Index তৈরি হয়
- Composite Primary Key হতে পারে

### Use Cases

- `user_id`
- `order_id`
- `product_id`

### Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

## 💎 UNIQUE

### Features

- Duplicate Value allowed নয়
- NULL রাখা যায়
- একাধিক UNIQUE Constraint ব্যবহার করা যায়
- Automatically Unique Index তৈরি হয়
- Composite UNIQUE হতে পারে

### Use Cases

- `email`
- `username`
- `phone`

### Example

```sql
CREATE TABLE users (
    email VARCHAR(255) UNIQUE
);
```

---

## 🛑 NOT NULL

### Features

- NULL Value allowed নয়
- Duplicate Value allowed
- Index তৈরি করে না
- একাধিক Column-এ ব্যবহার করা যায়

### Use Cases

- `name`
- `password`
- `email`

### Example

```sql
CREATE TABLE users (
    name VARCHAR(100) NOT NULL
);
```

---

## 📊 Quick Comparison

| Feature | PRIMARY KEY | UNIQUE | NOT NULL |
|----------|------------|---------|----------|
| Unique Values | ✅ | ✅ | ❌ |
| NULL Allowed | ❌ | ✅ | ❌ |
| Per Table | 1 | Many | Many |
| Auto Index | ✅ | ✅ | ❌ |
| Composite Possible | ✅ | ✅ | ❌ |

---

## 💡 Important Concept

### PRIMARY KEY = UNIQUE + NOT NULL

Primary Key মূলত:

- Unique হতে হবে
- NULL হতে পারবে না

অর্থাৎ:

```text
PRIMARY KEY = UNIQUE + NOT NULL
```

---

## 💡 UNIQUE ≠ NOT NULL

অনেকেই মনে করে `UNIQUE` মানেই `NOT NULL`।

এটা ভুল।

`UNIQUE` শুধু Duplicate Value বন্ধ করে।

কিন্তু `NULL` Value রাখা যেতে পারে।

PostgreSQL-এ একাধিক `NULL` Value-ও রাখা যায়, কারণ `NULL` কে কোনো নির্দিষ্ট Value হিসেবে ধরা হয় না।

### Example

```sql
CREATE TABLE users (
    email VARCHAR(255) UNIQUE
);
```

Valid Values:

```text
abc@gmail.com
xyz@gmail.com
NULL
NULL
```

এগুলো Valid কারণ Duplicate Email নেই।

---

## 💡 UNIQUE + NOT NULL

যদি কোনো Field:

- Required হয়
- এবং Unique হয়

তাহলে `UNIQUE` এবং `NOT NULL` একসাথে ব্যবহার করতে হবে।

### Example

```sql
email VARCHAR(255) UNIQUE NOT NULL
```

### Valid & Invalid Values

| Value | Result |
|---------|---------|
| abc@gmail.com | ✅ Valid |
| xyz@gmail.com | ✅ Valid |
| abc@gmail.com | ❌ Duplicate |
| NULL | ❌ NOT NULL Violation |

---

## 🎯 Interview Tips

### Q: PRIMARY KEY এবং UNIQUE-এর মধ্যে পার্থক্য কী?

| PRIMARY KEY | UNIQUE |
|------------|---------|
| NULL Allowed নয় | NULL Allowed |
| Table-এ মাত্র ১টি | একাধিক ব্যবহার করা যায় |
| Unique + NOT NULL | শুধুমাত্র Unique |

---

### Q: PRIMARY KEY = ?

✅ `UNIQUE + NOT NULL`

---

### Q: Email Field-এর জন্য কোন Constraint ব্যবহার করবে?

```sql
email VARCHAR(255) UNIQUE NOT NULL
```

কারণ:

- Duplicate Email Allowed নয়
- Email Required

---

## 📌 Quick Summary

| Constraint | Purpose |
|------------|---------|
| PRIMARY KEY | Record Uniquely Identify করে |
| UNIQUE | Duplicate Value Prevent করে |
| NOT NULL | Empty Value Prevent করে |

### Golden Rule

> PRIMARY KEY = UNIQUE + NOT NULL

> UNIQUE Duplicate Value বন্ধ করে

> NOT NULL Empty Value বন্ধ করে

# 📌 Primary Key Best Practices

---

## 🔑 Primary Key Essentials

- প্রতিটি Row-কে Unique ভাবে Identify করে।
- অবশ্যই `UNIQUE` এবং `NOT NULL` হতে হবে।
- প্রতি Table-এ মাত্র ১টি Primary Key থাকে।
- PostgreSQL Automatically Index তৈরি করে।

---

## 🚀 Primary Key Generation

### 1. SERIAL

- Auto Increment Number (1, 2, 3...)
- Small & Medium Projects-এর জন্য ভালো।
- Fast এবং সহজ।

---

### 2. UUID

- Globally Unique Identifier।
- Distributed Systems ও Large Scale Applications-এর জন্য ভালো।
- Predict করা কঠিন, Security বেশি।

---

### 3. Composite Primary Key

- একাধিক Column মিলে Primary Key।
- Junction / Mapping Table-এ বেশি ব্যবহৃত হয়।

### Example

```sql
PRIMARY KEY (student_id, course_id)
```
## ❌ Common Mistakes

---

### 1. Using Email as Primary Key

- Email পরিবর্তন হতে পারে।
- PK ideally immutable হওয়া উচিত।

### ✅ Solution

```sql
id SERIAL PRIMARY KEY,
email VARCHAR(255) UNIQUE
```

### 2. No Primary Key
- Row uniquely identify করা যায় না।
- UPDATE / DELETE risky হয়ে যায়।
### ✅ Rule

Every table should have a Primary Key.

### 3. Using Large VARCHAR / TEXT as PK
- Index বড় হয়।
- Comparison এবং JOIN slow হতে পারে।
### ❌ Avoid
```sql
PRIMARY KEY (email)
```
### ✅ Prefer
```sql
 id SERIAL PRIMARY KEY
```

### 4. Unnecessary Composite PK
- Complex Foreign Key relationships তৈরি করে।
- JOIN queries জটিল হয়ে যায়।

### ✅ Solution

Use Surrogate Key + UNIQUE Constraint when appropriate.

### 💡 Interview Tips
- PRIMARY KEY = UNIQUE + NOT NULL

- Email / Username → UNIQUE, not Primary Key
- Most common PK → SERIAL / BIGSERIAL
- Large-scale systems → UUID
- Every table should have a Primary Key

<br>

### 📌 VARCHAR as Primary Key?

VARCHAR কে PK হিসেবে ব্যবহার করা ভুল নয়, তবে বেশিরভাগ ক্ষেত্রে recommended নয়।

### ✅ When it is OK
- ISO country code (BD, US)
- Small stable identifiers
- Natural short keys
### ❌ When to Avoid
- Large strings (email, username, description)
- High-frequency JOIN operations
- Large-scale systems

### 📌 Final Rule

- ❌ Avoid large VARCHAR / TEXT as Primary Key
- ✅ Prefer INTEGER, BIGINT, SERIAL, UUID
- ⚠️ Use VARCHAR only when it is small, stable, and naturally a key

----
# 📌 Relational & Logical Operators

## Definition

Operators হলো Symbols বা Keywords যা `WHERE` clause-এ Data Filter, Compare এবং Combine করতে ব্যবহৃত হয়।

---

## 🔹 Relational Operators

Relational Operators ব্যবহার করা হয় দুইটি Value Compare করার জন্য।

| Operator | Meaning |
|----------|---------|
| `=` | Equal |
| `!=` | Not Equal |
| `<>` | Not Equal |
| `>` | Greater Than |
| `<` | Less Than |
| `>=` | Greater Than or Equal |
| `<=` | Less Than or Equal |

### Example

```sql
SELECT *
FROM students
WHERE age > 15;
```

---

## 🔹 Logical Operators

Logical Operators ব্যবহার করা হয় একাধিক Condition Combine করার জন্য।

| Operator | Meaning |
|----------|----------|
| `AND` | সব Condition TRUE হতে হবে |
| `OR` | যেকোনো একটি Condition TRUE হলেই হবে |
| `NOT` | Condition-এর বিপরীত ফলাফল দেয় |

### Example (AND)

```sql
SELECT *
FROM students
WHERE course = 'Django'
AND gpa > 3.80;
```

### Example (OR)

```sql
SELECT *
FROM students
WHERE course = 'Django'
OR course = 'ML';
```

### Example (NOT)

```sql
SELECT *
FROM students
WHERE NOT course = 'Django';
```

---

## 🔹 Special Operators

Special Operators Data Filtering আরও সহজ করে।

| Operator | Purpose |
|-----------|----------|
| `BETWEEN` | Range Check |
| `IN` | List Check |
| `LIKE` | Pattern Matching |
| `IS NULL` | NULL Value Check |
| `IS NOT NULL` | Non-NULL Value Check |

---

### BETWEEN Example

```sql
SELECT *
FROM students
WHERE age BETWEEN 18 AND 25;
```

Equivalent to:

```sql
WHERE age >= 18
AND age <= 25;
```

---

### IN Example

```sql
SELECT *
FROM students
WHERE course IN ('ML', 'Agentic AI');
```

Equivalent to:

```sql
WHERE course = 'ML'
OR course = 'Agentic AI';
```

---

### LIKE Example

```sql
SELECT *
FROM students
WHERE name LIKE 'A%';
```

Meaning:

- `A%` → Starts with A

More Patterns:

| Pattern | Meaning |
|----------|----------|
| `'A%'` | Starts with A |
| `'%A'` | Ends with A |
| `'%A%'` | Contains A |
| `'A_'` | A + One Character |

---

### IS NULL Example

```sql
SELECT *
FROM students
WHERE phone IS NULL;
```

Returns rows where phone number is missing.

---

### IS NOT NULL Example

```sql
SELECT *
FROM students
WHERE phone IS NOT NULL;
```

Returns rows where phone number exists.

---

## 📊 Quick Summary

| Category | Operators |
|-----------|-----------|
| Relational | `=`, `!=`, `<>`, `>`, `<`, `>=`, `<=` |
| Logical | `AND`, `OR`, `NOT` |
| Special | `BETWEEN`, `IN`, `LIKE`, `IS NULL`, `IS NOT NULL` |

---

## 💡 Interview Tips

- Relational Operators → Compare values
- Logical Operators → Combine conditions
- `BETWEEN` → Range filtering
- `IN` → Multiple values filtering
- `LIKE` → Pattern matching
- `IS NULL` → Check missing values
- `IS NOT NULL` → Check existing values

---

## 📌 Common Interview Questions

### Q: Difference between `=` and `IN`?

```sql
WHERE course = 'ML'
```

Checks a single value.

```sql
WHERE course IN ('ML', 'AI', 'Django')
```

Checks multiple values.

---

### Q: Why use `BETWEEN`?

Instead of:

```sql
WHERE age >= 18
AND age <= 25
```

You can write:

```sql
WHERE age BETWEEN 18 AND 25
```

Cleaner and easier to read.

---

### Q: Can we use `= NULL`?

❌ Wrong

```sql
WHERE phone = NULL
```

✅ Correct

```sql
WHERE phone IS NULL
```

### Golden Rule

> Use Relational Operators to compare values.
>
> Use Logical Operators to combine conditions.
>
> Use Special Operators to write cleaner and more readable queries.


<br>

## 📌 SQL Special Operators



### 💛 BETWEEN — Range Check

### Features

- নির্দিষ্ট রেঞ্জের মধ্যে value আছে কিনা চেক করে
- **Inclusive** (start এবং end দুইটাই অন্তর্ভুক্ত)



### Example

```sql
SELECT *
FROM students
WHERE age BETWEEN 12 AND 16;
Equivalent Query
WHERE age >= 12
AND age <= 16;
```

### 💙 IN — List Match
Features
- একাধিক value-এর মধ্যে match চেক করে
- Multiple OR condition-এর shortcut

### Example
```sql
SELECT *
FROM students
WHERE course IN ('Django', 'ML', 'DL');
Equivalent Query
WHERE course = 'Django'
   OR course = 'ML'
   OR course = 'DL';
``` 
### 💡 Key Takeaways
- BETWEEN → Range filtering (inclusive)
- IN → Multiple value matching
- দুটোই query আরও clean এবং readable করে
- Complex OR conditions সহজ করে দেয়

