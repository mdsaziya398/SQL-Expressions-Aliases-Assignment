# SQL Expressions and Aliases

## 📌 Assignment Overview

This assignment demonstrates the use of Expressions and Aliases in SQL using the Oracle `EMP` table.

The main objective is to understand how SQL can perform calculations directly inside a `SELECT` statement and how **aliases** can be used to give meaningful names to calculated columns.

The assignment includes practical examples of:

- Arithmetic expressions
- Salary calculations
- Annual salary calculation
- Bonus calculation
- Percentage increase and decrease
- Salary deductions
- Multiple-column expressions
- `EMP.*` for selecting all columns
- Column aliases using `AS`

---

# 1. What is an SQL Expression?

An **expression** is a combination of one or more values, column names, operators, and functions that produces a result.

Expressions are commonly used in the `SELECT` statement to perform calculations on table data.

### Basic Syntax

```sql
SELECT column_name, expression
FROM table_name;
```

### Example

```sql
SELECT ENAME, SAL * 12
FROM EMP;
```

Here:

- `ENAME` displays the employee name.
- `SAL` represents the employee's salary.
- `*` is the multiplication operator.
- `12` represents the number of months.
- `SAL * 12` calculates the annual salary.

The result displays the employee's name along with the calculated annual salary.

Example from this assignment:

```text
ENAME       SAL*12
SMITH        9600
ALLEN       19200
WARD        15000
JONES       35700
```

---

# 2. Types of Arithmetic Operators

SQL supports arithmetic operators that can be used in expressions.

| Operator | Meaning | Example |
|----------|---------|---------|
| `+` | Addition | `SAL + 2000` |
| `-` | Subtraction | `SAL - 100` |
| `*` | Multiplication | `SAL * 12` |
| `/` | Division | `SAL / 2` |

These operators allow us to perform calculations directly on table columns.

---

# 3. Addition Expression

The `+` operator is used to add values.

### Example

```sql
SELECT ENAME, SAL + 50
FROM EMP;
```

This adds `50` to every employee's salary.

Another example:

```sql
SELECT EMP.*, SAL + 2000
FROM EMP;
```

This displays all employee details and an additional calculated column containing salary plus 2000.

For example:

```text
SMITH   SAL = 800    SAL+2000 = 2800
ALLEN   SAL = 1600   SAL+2000 = 3600
```

---

# 4. Subtraction Expression

The `-` operator is used to subtract a value.

### Example

```sql
SELECT ENAME, SAL - 100
FROM EMP;
```

This subtracts `100` from each employee's salary.

Example:

```text
SMITH     800 - 100 = 700
ALLEN    1600 - 100 = 1500
```

---

# 5. Multiplication Expression

The `*` operator is used for multiplication.

### Example

```sql
SELECT ENAME, SAL * 6
FROM EMP;
```

This calculates six months of salary.

Another example:

```sql
SELECT ENAME, SAL * 12
FROM EMP;
```

This calculates the annual salary.

### Annual Salary Formula

```text
Annual Salary = Monthly Salary × 12
```

For example:

```text
SMITH
Monthly Salary = 800

Annual Salary = 800 × 12
              = 9600
```

---

# 6. Percentage Calculation

Expressions can also be used to calculate percentages.

### Example

```sql
SELECT ENAME, SAL + (SAL * 0.10)
FROM EMP;
```

This calculates the salary after a **10% increase**.

### Formula

```text
New Salary = Salary + (Salary × 10 / 100)
```

For example:

```text
SMITH
Salary = 800

10% of Salary = 800 × 0.10
              = 80

New Salary = 800 + 80
           = 880
```

---

# 7. Salary Deduction

An expression can also be used to calculate a reduced salary.

### Example

```sql
SELECT ENAME, SAL - (SAL * 0.25)
FROM EMP;
```

This calculates the salary after a **25% deduction**.

### Formula

```text
Remaining Salary = Salary - (Salary × 25 / 100)
```

For example:

```text
SMITH
Salary = 800

25% of Salary = 800 × 0.25
              = 200

Remaining Salary = 800 - 200
                 = 600
```

---

# 8. Ten Percent Deduction from Annual Salary

Expressions can also be combined to perform multiple calculations.

### Example

```sql
SELECT ENAME, SAL * 12 - (SAL * 12 * 0.10)
FROM EMP;
```

First, the monthly salary is converted into annual salary:

```text
SAL × 12
```

Then 10% is deducted:

```text
Annual Salary - (Annual Salary × 0.10)
```

### Formula

```text
Final Amount = (SAL × 12) - ((SAL × 12) × 0.10)
```

For example, for SMITH:

```text
SAL = 800

Annual Salary = 800 × 12
              = 9600

10% Deduction = 9600 × 0.10
              = 960

Final Amount = 9600 - 960
             = 8640
```

---

# 9. Combining Multiple Expressions

Multiple arithmetic operators can be combined in one SQL expression.

### Example

```sql
SELECT EMP.*, SAL * 6 + (SAL * 6 * 0.25)
FROM EMP;
```

This first calculates six months of salary and then adds 25% of that amount.

### Formula

```text
Result = (SAL × 6) + ((SAL × 6) × 0.25)
```

For SMITH:

```text
SAL = 800

Six Month Salary = 800 × 6
                 = 4800

25% = 4800 × 0.25
    = 1200

Result = 4800 + 1200
       = 6000
```

---

# 10. Parentheses in SQL Expressions

Parentheses are important when we want to control the order in which calculations are performed.

### Example

```sql
SELECT ENAME, (SAL + SAL * 0.10)
FROM EMP;
```

The expression calculates:

```text
SAL + (SAL × 10%)
```

Parentheses make complex calculations easier to understand and help control the order of calculation.



# 11. What is an Alias?

An **alias** is a temporary alternative name given to a column or table in a SQL query.

Aliases are especially useful for calculated columns because SQL normally displays the expression itself as the column heading.

For example:

```sql
SELECT ENAME, SAL * 12
FROM EMP;
```

The output column heading will normally appear as:

```text
SAL*12
```

Instead, we can give the calculated column a meaningful name.

```sql
SELECT ENAME, SAL * 12 AS ANNUAL_SALARY
FROM EMP;
```

Now the output becomes easier to understand:

```text
ENAME       ANNUAL_SALARY
SMITH            9600
ALLEN           19200
WARD            15000
```

---

# 12. Alias Using AS

The `AS` keyword can be used to assign an alias.

### Syntax

```sql
SELECT column_name AS alias_name
FROM table_name;
```

### Example

```sql
SELECT SAL AS SALARY
FROM EMP;
```

Here:

- `SAL` is the original column.
- `SALARY` is the alias.

For expressions:

```sql
SELECT SAL * 12 AS ANNUAL_SALARY
FROM EMP;
```

The calculated result is displayed under the heading `ANNUAL_SALARY`.

---

# 13. Alias Without AS

In Oracle SQL, an alias can also be written without using `AS`.

### Example

```sql
SELECT SAL * 12 ANNUAL_SALARY
FROM EMP;
```

This produces the same type of column alias:

```text
ANNUAL_SALARY
```

However, using `AS` can make the query easier to read.



# 14. Alias for a Bonus Calculation

A calculated column can be given a meaningful alias.

### Example

```sql
SELECT EMP.*, SAL + 2000 AS ANNUAL_BONUS
FROM EMP;
```

This query displays all columns from the `EMP` table and creates an additional calculated column called `ANNUAL_BONUS`.

Example:

```text
ENAME       SAL      ANNUAL_BONUS
SMITH       800          2800
ALLEN      1600          3600
WARD       1250          3250
```

The alias makes the purpose of the calculated column immediately clear.

---

# 15. Using EMP.*

The `*` symbol is used to select all columns from a table.

### Example

```sql
SELECT *
FROM EMP;
```

This displays every column of the `EMP` table.

We can also write:

```sql
SELECT EMP.*
FROM EMP;
```

Here, `EMP.*` means:

> Select all columns belonging to the EMP table.

We can combine `EMP.*` with an expression:

```sql
SELECT EMP.*, SAL + 2000 AS BONUS
FROM EMP;
```

This displays all employee information plus the calculated bonus column.

---

# 16. Expression with Multiple Columns

Expressions can use more than one column.

### Example

```sql
SELECT ENAME, SAL + COMM
FROM EMP;
```

This attempts to calculate the total of salary and commission.

```text
Total = Salary + Commission
```

An important point in the assignment is that some employees have no commission value. In Oracle, a `NULL` commission results in a `NULL` result when directly added to salary.

For example:

```text
ALLEN
SAL  = 1600
COMM = 300

SAL + COMM = 1900
```

For employees whose `COMM` is `NULL`, the expression produces `NULL`.

---

# 17. Date Column with an Expression

Expressions can also be used alongside other types of columns.

### Example

```sql
SELECT HIREDATE, SAL * 6 + 450
FROM EMP;
```

Here:

- `HIREDATE` displays the employee's joining date.
- `SAL * 6 + 450` performs an arithmetic calculation.

Example:

```text
HIREDATE       SAL*6+450
17-DEC-80         5250
20-FEB-81        10050
22-FEB-81         7950
```


# 18. Correct SQL Syntax

The assignment also demonstrates some common syntax mistakes.

### Incorrect

```sql
SELECT*.SAL+2000
FROM EMP;
```

This is incorrect because `*` cannot be followed by `.SAL` in this way.

### Correct

```sql
SELECT EMP.*, SAL + 2000
FROM EMP;
```

Here:

- `EMP.*` selects all columns.
- `SAL + 2000` calculates the additional amount.

---

# 19. Decimal Values in Expressions

Decimal values can be used for percentage calculations.

### Correct

```sql
SELECT ENAME, SAL + (SAL * 0.10)
FROM EMP;
```

Here `0.10` represents 10%.

### Common Mistake

```sql
SAL + SAL * O.10
```

The character `O` was used instead of the number `0`.

The correct expression is:

```sql
SAL + SAL * 0.10
```

This distinction is important because `0` is a number, while `O` is a letter.

---

# 20. Importance of Aliases

Aliases are useful because they:

1. Make column headings meaningful.
2. Improve query readability.
3. Make calculated results easier to understand.
4. Make reports more professional.
5. Help users understand what a calculated value represents.

### Without Alias

```sql
SELECT ENAME, SAL * 12
FROM EMP;
```

Output heading:

```text
SAL*12
```

### With Alias

```sql
SELECT ENAME, SAL * 12 AS ANNUAL_SALARY
FROM EMP;
```

Output heading:

```text
ANNUAL_SALARY
```

The second query is easier to understand.



# 21. Important Concepts Learned

Through this assignment, the following SQL concepts were practiced:

### Expressions

Expressions allow calculations to be performed directly in SQL.

Examples:

```sql
SAL * 12
SAL + 2000
SAL - 100
SAL * 6
SAL + (SAL * 0.10)
SAL - (SAL * 0.25)
```

### Arithmetic Operators

```text
+    Addition
-    Subtraction
*    Multiplication
/    Division
```

### Aliases

Aliases provide meaningful names to columns.

Example:

```sql
SAL * 12 AS ANNUAL_SALARY
```

### `EMP.*`

Used to select all columns from the `EMP` table.

Example:

```sql
SELECT EMP.*
FROM EMP;
```

### Parentheses

Parentheses help organize calculations and control the order of operations.

Example:

```sql
SAL + (SAL * 0.10)
```

---

# 22. Summary

SQL expressions are useful for performing calculations directly on database values without changing the original data stored in the table.

Using expressions, we can calculate:

- Annual salary
- Six-month salary
- Salary increases
- Salary deductions
- Bonuses
- Other calculated amounts

Aliases make these calculated columns easier to understand by replacing expressions such as `SAL*12` with meaningful names such as `ANNUAL_SALARY`.

This assignment provides practical understanding of how **SQL Expressions and Aliases** can be used to create clear and meaningful query results.

---

## 🛠️ Technologies Used

- Oracle SQL
- SQL*Plus
- `EMP` sample table

---

## 📚 Key SQL Syntax

```sql
-- Arithmetic Expression
SELECT ENAME, SAL * 12
FROM EMP;

-- Expression with Alias
SELECT ENAME, SAL * 12 AS ANNUAL_SALARY
FROM EMP;

-- Addition
SELECT ENAME, SAL + 2000 AS BONUS
FROM EMP;

-- Subtraction
SELECT ENAME, SAL - 100 AS REDUCED_SALARY
FROM EMP;

-- Percentage Increase
SELECT ENAME, SAL + (SAL * 0.10) AS INCREASED_SALARY
FROM EMP;

-- Percentage Deduction
SELECT ENAME, SAL - (SAL * 0.25) AS REDUCED_SALARY
FROM EMP;

-- All Columns with an Expression
SELECT EMP.*, SAL + 2000 AS BONUS
FROM EMP;
```

---

## 👨‍💻 Assignment

**Topic:** SQL Expressions and Aliases

**Database:** Oracle SQL

**Table Used:** EMP

**Purpose:** To understand and practice arithmetic expressions, calculated columns, aliases, and different SQL calculation techniques.
