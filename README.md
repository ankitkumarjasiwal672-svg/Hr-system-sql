# HR Employee Database — SQL Project

**Author:** Ankit Kumar  
**Tool:** MySQL  
**Type:** Portfolio Project  
**Domain:** Human Resources / People Analytics

---

## about this project

i built this project to practice sql and show how i think about data — specifically around HR operations, payroll tracking, and performance reporting. a lot of the logic here is inspired by the kind of MIS reporting and exception handling i do at work daily.

the database tracks employees across departments, monitors attendance, stores performance reviews (KPI, quality, CSAT), manages payroll, and handles leave requests.

---

## database structure

6 tables in total:

| table | what it stores |
|---|---|
| departments | team names, locations, manager |
| employees | all employee info — role, salary, status |
| attendance | daily check-in / check-out log |
| perf_reviews | quarterly KPI, quality, CSAT scores |
| payroll | monthly salary, bonus, deductions, net pay |
| leaves | leave requests and approval status |

---

## what the queries do

| # | query | purpose |
|---|---|---|
| 1 | employee directory | full list with department info |
| 2 | dept headcount & salary | group by aggregation report |
| 3 | performance ranking | overall score + rating band |
| 4 | payroll MIS report | with exception flagging for unpaid |
| 5 | attendance report | late arrival and absence flags |
| 6 | leave report | who is on leave and why |
| 7 | missing review check | data gap detection using LEFT JOIN |
| 8 | dept payroll total | sum of payout per department |
| 9 | salary vs KPI analysis | cross-check high pay vs performance |
| 10 | stored procedure | full employee profile in one call |

---

## views created

- `active_employees` — only shows currently active staff
- `pending_payments` — payroll exceptions (Pending / On Hold)
- `perf_summary` — average performance score per employee

---

## sql concepts used

- DDL: `CREATE TABLE`, `PRIMARY KEY`, `FOREIGN KEY`
- DML: `INSERT INTO`, `SELECT`
- Joins: `INNER JOIN`, `LEFT JOIN`
- Aggregation: `GROUP BY`, `COUNT`, `SUM`, `AVG`, `ROUND`
- Conditional logic: `CASE WHEN`
- Null handling: `IS NULL` for gap detection
- Stored Procedure: `DELIMITER`, `CREATE PROCEDURE`
- Views: `CREATE VIEW`

---

## how to run

1. open mysql workbench or any mysql client
2. run the full `.sql` file from top to bottom
3. use the queries section to test individual reports
4. to get a specific employee's full profile run:

```sql
call get_emp_details(1);
```

replace `1` with any emp_id

---

## skills this project demonstrates

- sql query writing for reporting and analytics
- MIS-style exception flagging in sql (same logic as excel)
- performance tracking with KPI / CSAT / quality scores
- payroll data management
- data gap identification using LEFT JOIN + IS NULL
- stored procedures and views for reusable reporting

---

## other projects

- [Blinkit Sales & Operations Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZmI1...) — Power BI
- [Floww Budget Tracker](https://ankitkumarjasiwal672-svg.github.io/budget-tracker) — HTML/CSS/JS

---

*open to MIS Analyst, Reporting Analyst, and Data Analyst roles in Delhi NCR*  
*reach me at ankit.kumarjasiwal672@gmail.com*
