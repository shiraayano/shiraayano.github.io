### MySQL
1. **SQL语言四大类别**：
    - **DDL**：用于定义数据库结构，如创建、修改、删除表。
    - **DML**：用于操作数据，如插入、更新、删除记录。
    - **DQL**：用于查询数据，如`SELECT`。
    - **DCL**：用于控制访问权限，如授予、撤销权限。
2. **字符集选择、数据类型转换、字段操作**：
    - 字符集选择影响数据存储与显示，常用的有UTF-8。
    - 数据类型转换用于在不同类型之间转换。
    - 字段操作包括修改字段类型、默认值和约束等。
3. **数据库函数**：
    - **字符串函数**：处理字符串，如`CONCAT`、`SUBSTRING`。
    - **数值函数**：处理数值，如`ROUND`、`ABS`。
    - **日期函数**：处理日期时间，如`NOW`、`DATE_ADD`。
    - **流程函数**：控制流程，如`IF`、`CASE`。
4. **约束**：
    - **非空约束**：保证字段不为空。
    - **唯一约束**：保证字段值唯一。
    - **主键约束**：确保唯一标识每条记录。
5. **多表查询**：
    - **一对多**、**多对多**、**一对一**：表之间的常见关系。
    - **连接查询**：内连接、外连接、自连接。
    - **联合查询**：合并多个查询结果。
    - **子查询**：在查询中嵌套另一个查询。
6. **事务**：
    - **基本操作**：包括`START TRANSACTION`、`COMMIT`、`ROLLBACK`。
    - **ACID特性**：保证事务的原子性、一致性、隔离性和持久性。
    - **并发事务问题和隔离级别**：解决脏读、不可重复读、幻读问题，常见隔离级别有`READ COMMITTED`、`REPEATABLE READ`、`SERIALIZABLE`。



[建议阅读](https://jimhackking.github.io/%E8%BF%90%E7%BB%B4/MySQL%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/#%E6%9D%83%E9%99%90%E4%B8%80%E8%A7%88%E8%A1%A8)



### MySQL数据库的SQL语言四大类别
在MySQL数据库管理中，SQL（Structured Query Language）被划分为四大类别，每个类别包含不同的功能，旨在管理和操作数据库中的数据和结构。

+ 数据定义语言（DDL）
+ 数据操作语言（DML）
+ 数据查询语言（DQL）
+ 控制语言（DCL）

#### 1. 数据定义语言（DDL）
DDL用于定义和管理数据库对象的结构，包括表、视图、索引等。主要命令包括：

+ **CREATE**：用于创建数据库和表等对象。
+ **ALTER**：用于修改现有数据库对象的结构。
+ **DROP**：用于删除数据库对象。

示例：

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50)
);
```

#### 2. 数据操作语言（DML）
DML用于操作数据库中的数据。主要命令包括：

+ **INSERT**：用于向表中插入数据。
+ **UPDATE**：用于更新表中的现有数据。
+ **DELETE**：用于删除表中的数据。

示例：

```sql
INSERT INTO employees (id, name, department) VALUES (1, 'John Doe', 'HR');
```

#### 3. 数据查询语言（DQL）
DQL主要用于查询数据，核心命令是**SELECT**，用于从数据库中检索数据。通过结合WHERE、GROUP BY、HAVING等子句，可以构建复杂的查询。

示例：

```sql
SELECT name, department FROM employees WHERE department = 'HR';
```

#### 4. 数据控制语言（DCL）
DCL用于定义数据库的权限和安全设置，确保数据访问和使用的安全性。主要命令包括：

+ **GRANT**：用于授予用户特定的权限。
+ **REVOKE**：用于撤销用户的权限。

示例：

```sql
GRANT SELECT, INSERT ON employees TO 'user1'@'localhost';
```





### MySQL数据库中的字符集选择、数据类型转换与字段操作
#### 1. 字符集选择
字符集决定了数据库中存储的字符的编码方式，不同的字符集支持不同的语言和符号。常用的字符集包括`utf8mb4`（支持多种语言和符号）和`latin1`（支持西欧语言）。

+ **设置字符集**：可以在创建数据库或表时指定字符集，也可以在连接时设置。
+ **更改字符集**：使用`ALTER`命令可以更改现有表的字符集。

示例：

```sql
CREATE DATABASE mydb CHARACTER SET utf8mb4;
ALTER TABLE employees CONVERT TO CHARACTER SET utf8mb4;
```

#### 2. 数据类型转换
数据类型转换是指将一种数据类型转换为另一种数据类型。MySQL支持隐式和显式的数据类型转换。

+ **隐式转换**：当操作符或函数需要某种特定的数据类型时，MySQL会自动进行类型转换。
+ **显式转换**：使用`CAST`或`CONVERT`函数可以明确地将数据转换为指定的数据类型。

示例：

```sql
SELECT CAST('123' AS UNSIGNED); -- 将字符串转换为无符号整数
SELECT CONVERT('2025-01-09', DATE); -- 将字符串转换为日期
```

#### 3. 字段操作
字段操作涉及表中的列（字段）的增删改等操作，确保表结构的灵活性和扩展性。

+ **添加字段**：使用`ALTER TABLE`命令添加新列。
+ **修改字段**：可以更改字段的数据类型、默认值或其他属性。
+ **删除字段**：删除不需要的字段。

示例：

```sql
ALTER TABLE employees ADD COLUMN email VARCHAR(100); -- 添加新字段
ALTER TABLE employees MODIFY COLUMN name VARCHAR(100); -- 修改字段类型
ALTER TABLE employees DROP COLUMN department; -- 删除字段
```



### 函数
MySQL提供了丰富的内置函数，帮助用户在数据库操作中进行字符串处理、数值运算、日期计算以及流程控制等多种任务。根据功能的不同，这些函数可分为四大类：字符串函数、数值函数、日期函数和流程函数。

#### 1. 字符串函数
字符串函数用于对字符串进行处理和操作，例如提取子字符串、查找字符串长度、转换大小写等。

常用的字符串函数包括：

+ `**CONCAT()**`：连接两个或多个字符串。
+ `**LENGTH()**`：返回字符串的长度（字符数）。
+ `**SUBSTRING()**`：返回字符串的子串。
+ `**UPPER()**`：将字符串转换为大写字母。
+ `**LOWER()**`：将字符串转换为小写字母。
+ `**TRIM()**`：去除字符串两端的空白字符。
+ `**REPLACE()**`：替换字符串中的指定子字符串。

示例：

```sql
SELECT CONCAT('Hello', ' ', 'World');  -- 输出：Hello World
SELECT LENGTH('MySQL');  -- 输出：5
SELECT SUBSTRING('MySQL', 2, 3);  -- 输出：ySQL
SELECT UPPER('mysql');  -- 输出：MYSQL
```

#### 2. 数值函数
数值函数用于执行数值计算，如四则运算、取整、随机数生成等。

常用的数值函数包括：

+ `**ROUND()**`：对数值进行四舍五入。
+ `**FLOOR()**`：返回小于或等于指定数值的最大整数。
+ `**CEIL()**`：返回大于或等于指定数值的最小整数。
+ `**RAND()**`：生成一个随机浮动值，通常用于生成随机数。
+ `**ABS()**`：返回数值的绝对值。

示例：

```sql
SELECT ROUND(123.456, 2);  -- 输出：123.46
SELECT FLOOR(123.456);  -- 输出：123
SELECT CEIL(123.456);  -- 输出：124
SELECT RAND();  -- 输出：随机值，例如：0.487156
SELECT ABS(-100);  -- 输出：100
```

#### 3. 日期函数
日期函数用于处理和操作日期和时间数据，常见的功能包括获取当前时间、日期加减、格式化日期等。

常用的日期函数包括：

+ `**NOW()**`：返回当前的日期和时间。
+ `**CURDATE()**`：返回当前的日期。
+ `**DATE_ADD()**`：向日期添加指定的时间间隔。
+ `**DATE_SUB()**`：从日期中减去指定的时间间隔。
+ `**YEAR()**`、`**MONTH()**`、`**DAY()**`：分别提取日期中的年、月、日部分。
+ `**DATE_FORMAT()**`：格式化日期为指定的字符串格式。

示例：

```sql
SELECT NOW();  -- 返回当前日期和时间，例如：2025-01-09 12:34:56
SELECT CURDATE();  -- 返回当前日期，例如：2025-01-09
SELECT DATE_ADD('2025-01-09', INTERVAL 1 DAY);  -- 输出：2025-01-10
SELECT DATE_SUB('2025-01-09', INTERVAL 2 MONTH);  -- 输出：2024-11-09
SELECT YEAR('2025-01-09');  -- 输出：2025
SELECT DATE_FORMAT('2025-01-09', '%Y-%m-%d');  -- 输出：2025-01-09
```

#### 4. 流程函数
流程控制函数用于在SQL查询中实现条件判断和流程控制，如判断语句、条件表达式等。

常用的流程函数包括：

+ `**IF()**`：用于根据条件执行不同的操作。
+ `**CASE**`：根据不同的条件返回不同的结果（类似于`switch`语句）。
+ `**COALESCE()**`：返回参数中第一个非空的值。
+ `**NULLIF()**`：如果两个表达式相等，返回`NULL`，否则返回第一个表达式的值。

示例：

```sql
SELECT IF(1 > 0, 'True', 'False');  -- 输出：True
SELECT CASE WHEN age >= 18 THEN 'Adult' ELSE 'Minor' END FROM users;  -- 根据age字段判断
SELECT COALESCE(NULL, 'Default', 'Value');  -- 输出：Default
SELECT NULLIF(10, 10);  -- 输出：NULL
```

### 
### MySQL数据库中的约束
在MySQL中，约束（Constraints）是用于限定表中数据的规则，确保数据的完整性和一致性。约束可以在创建表时定义，也可以在表创建后使用`ALTER TABLE`命令添加或修改。常见的约束有非空约束（`NOT NULL`）、唯一约束（`UNIQUE`）和主键约束（`PRIMARY KEY`）。

#### 1. 非空约束（`NOT NULL`）
非空约束确保表中的某个字段在插入数据时不能为`NULL`。这意味着该字段必须包含有效的数据，不能为空。

+ **作用**：保证字段有值，避免出现无效或缺失的数据。
+ **应用场景**：例如，要求每个员工必须有姓名、每个订单必须有订单号等。

**示例**：

```sql
CREATE TABLE employees (
    id INT NOT NULL,  -- 非空约束，id不能为空
    name VARCHAR(50) NOT NULL,  -- 非空约束，name不能为空
    department VARCHAR(50)
);
```

如果尝试插入`NULL`值，系统会报错：

```sql
INSERT INTO employees (id, name) VALUES (1, NULL);  -- 报错，name不能为空
```

#### 2. 唯一约束（`UNIQUE`）
唯一约束确保字段中的所有值都是唯一的，即该字段中的每个数据值不能重复。唯一约束允许字段中的值为`NULL`，但如果字段不为空，则每个值都必须是唯一的。

+ **作用**：确保数据表中某一字段的数据不重复，避免出现重复记录。
+ **应用场景**：例如，要求每个电子邮件地址必须是唯一的，或者每个身份证号不能重复。

**示例**：

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE  -- 唯一约束，email不能重复
);
```

在插入数据时，如果试图插入重复的`email`值，系统会报错：

```sql
INSERT INTO employees (id, email) VALUES (1, 'john.doe@example.com');
INSERT INTO employees (id, email) VALUES (2, 'john.doe@example.com');  -- 报错，email值重复
```

#### 3. 主键约束（`PRIMARY KEY`）
主键约束是唯一约束的特殊形式。主键是表中用来唯一标识每一条记录的字段或字段组合。主键约束要求字段值必须唯一，并且不能为空。每个表只能有一个主键。

+ **作用**：主键确保表中的每一行数据都有唯一标识，并且不允许为`NULL`。
+ **应用场景**：例如，要求每个员工必须有唯一的员工编号，或者每个订单必须有唯一的订单号。

**示例**：

```sql
CREATE TABLE employees (
    id INT NOT NULL,
    name VARCHAR(50),
    department VARCHAR(50),
    PRIMARY KEY (id)  -- id列是主键，不能重复并且不能为NULL
);
```

在插入数据时，如果试图插入重复的主键值或`NULL`值，系统会报错：

```sql
INSERT INTO employees (id, name, department) VALUES (1, 'John Doe', 'HR');
INSERT INTO employees (id, name, department) VALUES (1, 'Jane Doe', 'Finance');  -- 报错，主键冲突
```

### 总结
+ **非空约束**：确保字段不能有`NULL`值，保证数据的完整性。
+ **唯一约束**：确保字段中的值唯一，防止重复记录。
+ **主键约束**：不仅保证字段值唯一，而且字段值不能为空，通常用于唯一标识记录。



### MySQL数据库中的多表查询
在实际应用中，数据库表之间的关系非常常见，MySQL提供了丰富的多表查询功能，用于处理表与表之间的各种关系。常见的多表查询类型包括一对多关系、多对多关系、一对一关系，以及各种连接查询（内连接、外连接、自连接）和联合查询、子查询等。以下是这些查询的详细介绍：

#### 1. 一对多关系（One-to-Many）
一对多关系指的是一个表中的一条记录可以与另一个表中的多条记录相关联。通常在一对多关系中，"一"的一方是主表，"多"的一方是从表。

例如，假设有两个表：`departments`（部门表）和`employees`（员工表）。每个部门有多个员工，但每个员工只属于一个部门。

**表结构**：

+ `departments`表：存储部门信息（`department_id`、`department_name`）。
+ `employees`表：存储员工信息（`employee_id`、`employee_name`、`department_id`）。

**查询示例**：

```sql
SELECT e.employee_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

这个查询返回所有员工及其所属部门的信息，其中每个部门可以有多个员工。

#### 2. 多对多关系（Many-to-Many）
多对多关系指的是表与表之间的关系非常复杂，一条记录可以与另一表中的多条记录关联，反之亦然。通常，需要通过一个中间表来表示这种关系。

例如，假设有三个表：`students`（学生表）、`courses`（课程表）和`student_courses`（学生选课表）。一个学生可以选修多门课程，而每门课程可以被多个学生选修。

**表结构**：

+ `students`表：存储学生信息（`student_id`、`student_name`）。
+ `courses`表：存储课程信息（`course_id`、`course_name`）。
+ `student_courses`表：存储学生和课程之间的关系（`student_id`、`course_id`）。

**查询示例**：

```sql
SELECT s.student_name, c.course_name
FROM students s
JOIN student_courses sc ON s.student_id = sc.student_id
JOIN courses c ON sc.course_id = c.course_id;
```

该查询返回每个学生选修的课程信息，其中每个学生可以选修多门课程，且每门课程也可以有多个学生。

#### 3. 一对一关系（One-to-One）
一对一关系指的是两个表中的一条记录只能与另一个表中的一条记录关联。例如，假设有`employees`（员工表）和`employee_details`（员工详细信息表），每个员工在`employee_details`表中只有一条记录，反之亦然。

**表结构**：

+ `employees`表：存储员工信息（`employee_id`、`employee_name`）。
+ `employee_details`表：存储员工详细信息（`employee_id`、`address`、`phone_number`）。

**查询示例**：

```sql
SELECT e.employee_name, ed.address, ed.phone_number
FROM employees e
JOIN employee_details ed ON e.employee_id = ed.employee_id;
```

该查询返回每个员工及其详细信息，其中每个员工只有一个对应的详细信息记录。

#### 4. 内连接查询（INNER JOIN）
内连接查询用于返回两个表中符合连接条件的记录。如果两个表中的记录没有匹配项，则该记录不会出现在查询结果中。

**查询示例**：

```sql
SELECT e.employee_name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id;
```

这个查询只会返回那些员工与部门匹配的记录（即`employee_id`与`department_id`匹配的记录）。

#### 5. 外连接查询（OUTER JOIN）
外连接查询返回两个表中的所有记录，即使某些记录在一个表中没有匹配项。外连接分为左外连接（`LEFT JOIN`）、右外连接（`RIGHT JOIN`）和完全外连接（`FULL OUTER JOIN`，在MySQL中需要用`UNION`模拟）。

+ **左外连接（**`**LEFT JOIN**`**）**：返回左表中的所有记录，以及右表中匹配的记录。如果右表中没有匹配项，结果中右表的列将显示`NULL`。
+ **右外连接（**`**RIGHT JOIN**`**）**：返回右表中的所有记录，以及左表中匹配的记录。如果左表中没有匹配项，结果中左表的列将显示`NULL`。

**查询示例**：

```sql
-- 左外连接
SELECT e.employee_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;

-- 右外连接
SELECT e.employee_name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.department_id;
```

#### 6. 自连接查询（Self Join）
自连接查询是指同一表与其自身进行连接。这种查询通常用于查找表中记录之间的关系，比如员工表中的经理与员工之间的关系。

**查询示例**：

```sql
SELECT e1.employee_name AS Employee, e2.employee_name AS Manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.employee_id;
```

这个查询返回所有员工及其经理的名称，其中`e1`是员工表的别名，`e2`是经理表的别名，`manager_id`表示经理的`employee_id`。

#### 7. 联合查询（UNION）
联合查询用于将多个`SELECT`查询的结果合并为一个结果集。使用`UNION`时，所有的查询列数和列类型必须一致。`UNION`会去除重复的记录，若需要包括重复记录，可以使用`UNION ALL`。

**查询示例**：

```sql
SELECT employee_name FROM employees
UNION
SELECT department_name FROM departments;
```

该查询将返回员工名称和部门名称的并集。

#### 8. 子查询（Subquery）
子查询是在一个查询中嵌套另一个查询，子查询可以出现在`SELECT`、`FROM`、`WHERE`等子句中。子查询可以是单行子查询、多行子查询或相关子查询。

**查询示例**：

```sql
-- 单行子查询
SELECT employee_name
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'HR');

-- 多行子查询
SELECT employee_name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE department_name = 'HR');
```

上面的查询会返回所有在`HR`部门的员工。

### 总结
+ **一对多关系**：通过连接表和外键关系来查询一个表与另一个表之间的多对多关系。
+ **多对多关系**：通过中间表来实现，通常用于处理涉及多个实体的复杂关联。
+ **一对一关系**：通常通过共享主键来建立一对一关系，适用于存储一对一相关的数据。
+ **内连接（INNER JOIN）**：返回两个表中匹配的记录。
+ **外连接（OUTER JOIN）**：返回一个表中的所有记录及另一个表中匹配的记录，包括没有匹配项的记录。
+ **自连接（SELF JOIN）**：同一表与自身进行连接，适用于处理表中记录之间的关联。
+ **联合查询（UNION）**：将多个查询结果合并为一个结果集，默认去除重复记录。
+ **子查询（SUBQUERY）**：将一个查询嵌套在另一个查询中，用于复杂的查询逻辑。



### MySQL数据库中的事务
事务（Transaction）是一个逻辑上的工作单位，由一系列的数据库操作组成，这些操作要么全部成功执行，要么全部回滚。事务的主要目的是确保数据的一致性、完整性和可靠性。MySQL支持事务处理，它可以让用户在多个操作之间实现原子性、持久性等特性，从而保证数据的准确性和一致性。

#### 1. 基本操作
MySQL的事务操作包括`START TRANSACTION`、`COMMIT`、`ROLLBACK`等。通过这些操作，用户可以启动一个事务、提交事务或回滚事务。

+ `**START TRANSACTION**`：启动一个新的事务。
+ `**COMMIT**`：提交事务，意味着将事务中的所有更改永久保存到数据库。
+ `**ROLLBACK**`：回滚事务，意味着撤销事务中的所有更改，恢复到事务开始之前的状态。

**示例**：

```sql
START TRANSACTION;  -- 开始事务

UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;  -- 从账户1扣款
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;  -- 向账户2存款

COMMIT;  -- 提交事务
```

如果在执行过程中出现错误，需要回滚事务：

```sql
START TRANSACTION;  -- 开始事务

UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;  -- 从账户1扣款
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;  -- 向账户2存款

ROLLBACK;  -- 回滚事务，撤销所有更改
```

#### 2. ACID特性
事务的四个基本特性被称为ACID特性，它们是保证事务可靠性的核心标准。ACID是以下四个英文单词的缩写：

+ **原子性（Atomicity）**：事务中的操作要么全部成功，要么全部失败。事务不可分割，不能出现部分提交的情况。即使在操作过程中发生故障，系统也会恢复到事务开始之前的状态。
+ **一致性（Consistency）**：事务执行前后，数据库必须保持一致的状态。每个事务在执行时必须从一个一致的数据库状态转移到另一个一致的数据库状态。
+ **隔离性（Isolation）**：每个事务的执行不应受到其他事务的干扰。即使多个事务并发执行，每个事务也应像是独立执行一样，互不影响。
+ **持久性（Durability）**：事务一旦提交，其结果就会永久保存到数据库中，不会因为系统崩溃或故障而丢失。

**ACID特性示例**：

+ **原子性**：假设某个事务涉及到两次操作（扣款和存款）。如果其中一次操作失败（比如扣款失败），整个事务会回滚，恢复到原始状态（即没有执行扣款和存款操作）。
+ **一致性**：如果银行账户操作符合一定规则（如账户余额不能为负），事务执行后，系统仍然满足这些规则。
+ **隔离性**：即使两个用户同时操作相同的数据（如转账），每个用户的操作都不会干扰到另一个用户的事务。
+ **持久性**：即使系统崩溃，已提交的转账记录仍然能够被保存并恢复。

#### 3. 并发事务问题和隔离级别
在数据库中，当多个事务并发执行时，可能会出现并发事务问题，例如脏读、不可重复读和幻读。为了避免这些问题，数据库提供了隔离级别（Isolation Levels）来控制并发事务的行为。

**并发事务问题**：

+ **脏读（Dirty Read）**：一个事务读取了另一个事务未提交的数据。
+ **不可重复读（Non-repeatable Read）**：一个事务在执行过程中，另一个事务修改了正在读取的数据，导致数据不一致。
+ **幻读（Phantom Read）**：一个事务在读取数据集时，另一个事务插入了新的数据，导致查询结果发生变化。

**事务隔离级别**： MySQL支持四种事务隔离级别，每种隔离级别提供不同程度的并发控制，从而影响事务的执行效率和数据一致性。

1. **READ UNCOMMITTED（读未提交）**：
    - 在这个隔离级别，事务可以读取其他事务未提交的数据（脏读）。这是最不严格的隔离级别。
    - 可能出现脏读、不可重复读和幻读问题。

**示例**：

```sql
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

2. **READ COMMITTED（读已提交）**：
    - 在这个隔离级别，事务只能读取已提交的数据（防止脏读）。但是，仍然可能出现不可重复读。
    - 这种隔离级别避免了脏读，但无法避免不可重复读和幻读问题。

**示例**：

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

3. **REPEATABLE READ（可重复读）**：
    - 在这个隔离级别，事务中读取的数据在整个事务期间都是一致的（防止不可重复读）。但是，可能会出现幻读问题。
    - 这是MySQL的默认隔离级别，能够防止脏读和不可重复读，但幻读问题仍然存在。

**示例**：

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

4. **SERIALIZABLE（可串行化）**：
    - 在这个隔离级别，事务强制按照顺序执行，完全避免了脏读、不可重复读和幻读问题。每个事务的执行会被其他事务完全隔离。
    - 这是最严格的隔离级别，能够提供完全的数据一致性，但性能较低。

**示例**：

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

**隔离级别的选择**：

+ **性能与一致性的权衡**：越高的隔离级别通常会带来更强的数据一致性保障，但也会导致更低的并发性能。因此，选择合适的隔离级别需要权衡性能和数据一致性。
+ **默认隔离级别**：在MySQL中，默认的隔离级别是`REPEATABLE READ`，它能够防止脏读和不可重复读。

### 总结
+ **基本操作**：通过`START TRANSACTION`、`COMMIT`和`ROLLBACK`控制事务的开始、提交和回滚。
+ **ACID特性**：确保事务具备原子性、一致性、隔离性和持久性，从而保证数据的可靠性和一致性。
+ **并发事务问题**：可能出现脏读、不可重复读和幻读等问题，通过合理选择事务隔离级别可以解决这些问题。
+ **事务隔离级别**：包括`READ UNCOMMITTED`、`READ COMMITTED`、`REPEATABLE READ`和`SERIALIZABLE`四种，隔离级别越高，数据一致性越强，但性能可能降低。


MySQL中SQL语句的书写顺序和执行顺序：
书写顺序
SELECT：选择要返回的列。
FROM：指定查询的表。
JOIN：表连接操作。
WHERE：过滤条件。
GROUP BY：分组条件。
HAVING：分组后的过滤条件。
ORDER BY：排序条件。
LIMIT：限制返回的行数。
执行顺序
FROM：确定查询的表。
JOIN：表连接操作。
WHERE：过滤条件。
GROUP BY：分组条件。
HAVING：分组后的过滤条件。
SELECT：选择要返回的列。
ORDER BY：排序条件。
LIMIT：限制返回的行数。
为什么不同
性能优化：先处理FROM、JOIN和WHERE可以减少需要处理的数据量，提高查询效率。
逻辑依赖：GROUP BY和HAVING需要在数据已经过滤和连接之后才能生效。

