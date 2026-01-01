## 🧠 What are “default databases” in MySQL?

👉 When MySQL is installed, it **automatically creates some databases**.
These databases are **not for your application data**.
They are used by **MySQL itself** to work properly.

***

## 📦 Default Databases You Will See

When you run:

```
SHOW DATABASES;

```

You usually see something like:

```
information_schema
mysql
performance_schema
sys

```

Let’s understand **each one clearly**.

***

## 1️⃣ `information_schema`

### 🔹 What is it?

👉 A **read-only system database** that stores **metadata**
(Data *about* your databases)

***

### 🔹 What kind of information does it contain?

* List of databases
* List of tables
* List of columns
* Index information
* Constraints

📌 Example:

```
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'sakila';

```

***

### 🔹 Important beginner notes

* ❌ You cannot insert data
* ❌ You cannot delete tables
* ✅ You only **query** it

🧠 **Think of it as MySQL’s “dictionary”**

***

## 2️⃣ `mysql`

### 🔹 What is it?

👉 The **most critical internal database**
It stores **user accounts and permissions**.

***

### 🔹 What does it contain?

* Users and passwords
* Privileges
* Roles
* Authentication info

📌 Example:

```
SELECT user, host FROM mysql.user;

```

***

### 🔹 Important beginner notes

* ⚠️ **Do NOT modify tables manually**
* ❌ Do not store application data here
* 🔐 Used by MySQL for security

🧠 **Think of it as MySQL’s “security office”**

***

## 3️⃣ `performance_schema`

### 🔹 What is it?

👉 A database used to **monitor MySQL performance**.

***

### 🔹 What does it track?

* Slow queries
* Locks
* Threads
* Memory usage
* Query execution stats

📌 Example:

```
SELECT * FROM performance_schema.events_statements_summary_by_digest;

```

***

### 🔹 Important beginner notes

* Used by DBAs
* Helps tune performance
* Not required for daily app work

🧠 **Think of it as MySQL’s “monitoring dashboard”**

***

## 4️⃣ `sys`

### 🔹 What is it?

👉 A **helper database built on top of `performance_schema`**
Provides **easy-to-read views**.

***

### 🔹 Why does it exist?

`performance_schema` tables are:

* Large
* Complex
* Hard to query

`sys` simplifies them.

***

### 🔹 Example

```
SELECT * FROM sys.user_summary;

```

This gives human-readable performance info.

***

### 🔹 Important beginner notes

* Contains **views**, not real tables
* Safe to query
* Meant for diagnostics

🧠 **Think of it as MySQL’s “report generator”**

***

## 🧩 Summary Table (Very Important)

| Database            | Purpose                      | Can You Store Data? |
| ------------------- | ---------------------------- | ------------------- |
| information\_schema | Metadata                     | ❌ No                |
| mysql               | Users & permissions          | ❌ No                |
| performance\_schema | Performance metrics          | ❌ No                |
| sys                 | Simplified performance views | ❌ No                |

***

## 🚫 Where should YOU store your data?

👉 **In your own database**

Example:

```
CREATE DATABASE app_db;
USE app_db;

```

Then create tables there.

***

## 🧠 Common Beginner Mistakes ❌

❌ Creating tables in `mysql`
❌ Deleting `sys` database
❌ Trying to insert rows into `information_schema`
❌ Treating system databases like normal databases

***

## 🧠 Final Mental Model (Remember This)

> **System databases are for MySQL**
> **User databases are for YOU**
