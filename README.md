-- HR Employee Database
-- created by ankit kumar


create database hr_db;
use hr_db;


-- departments table, keeping it simple
create table departments (
    dept_id int primary key auto_increment,
    dept_name varchar(100),
    location varchar(100),
    head_name varchar(100)
);


-- main employee table
create table employees (
    emp_id int primary key auto_increment,
    name varchar(150),
    email varchar(150),
    phone varchar(15),
    dept_id int,
    role varchar(100),
    emp_type varchar(20) default 'Full-Time',  -- Full-Time / Contract / Part-Time
    joining_date date,
    salary decimal(10,2),
    status varchar(20) default 'Active',       -- Active / Inactive / On Leave
    foreign key (dept_id) references departments(dept_id)
);


-- attendance log
create table attendance (
    id int primary key auto_increment,
    emp_id int,
    att_date date,
    check_in time,
    check_out time,
    att_status varchar(20),   -- Present, Absent, Half Day, WFH
    foreign key (emp_id) references employees(emp_id)
);


-- performance review table
-- added csat and quality score separately because those are tracked differently at my workplace
create table perf_reviews (
    review_id int primary key auto_increment,
    emp_id int,
    quarter varchar(20),
    kpi_score decimal(5,2),
    quality_score decimal(5,2),
    csat_score decimal(5,2),
    reviewed_by varchar(100),
    review_date date,
    comments text,
    foreign key (emp_id) references employees(emp_id)
);


-- payroll / salary table
create table payroll (
    txn_id int primary key auto_increment,
    emp_id int,
    month varchar(20),
    basic decimal(10,2),
    bonus decimal(10,2) default 0,
    deductions decimal(10,2) default 0,
    net_pay decimal(10,2),
    pay_date date,
    pay_status varchar(20) default 'Paid',
    foreign key (emp_id) references employees(emp_id)
);


-- leave table
create table leaves (
    leave_id int primary key auto_increment,
    emp_id int,
    leave_type varchar(30),
    start_date date,
    end_date date,
    days int,
    status varchar(20) default 'Pending',
    applied_on date,
    foreign key (emp_id) references employees(emp_id)
);


-- inserting data

insert into departments (dept_name, location, head_name) values
('Customer Support', 'Delhi', 'Rajesh Sharma'),
('Quality Assurance', 'Delhi', 'Priya Mehta'),
('Operations', 'Noida', 'Amit Verma'),
('MIS & Reporting', 'Gurgaon', 'Sunita Rao'),
('HR & Admin', 'Delhi', 'Kavita Singh');


insert into employees (name, email, phone, dept_id, role, emp_type, joining_date, salary, status) values
('Ankit Kumar', 'ankit.kumar@wipro.com', '8882360235', 1, 'Senior Customer Support & Team Lead', 'Full-Time', '2023-08-01', 55000, 'Active'),
('Sneha Gupta', 'sneha.gupta@wipro.com', '9876543210', 2, 'QA Analyst', 'Full-Time', '2022-03-15', 48000, 'Active'),
('Rahul Singh', 'rahul.singh@wipro.com', '9988776655', 1, 'Customer Support Executive', 'Full-Time', '2023-01-10', 38000, 'Active'),
('Pooja Sharma', 'pooja.sharma@wipro.com', '9123456780', 3, 'Operations Analyst', 'Full-Time', '2021-07-20', 52000, 'Active'),
('Mohit Yadav', 'mohit.yadav@wipro.com', '9001122334', 4, 'MIS Analyst', 'Full-Time', '2020-11-05', 60000, 'Active'),
('Riya Kapoor', 'riya.kapoor@wipro.com', '9871234560', 1, 'Customer Support Executive', 'Contract', '2024-01-15', 32000, 'Active'),
('Deepak Nair', 'deepak.nair@wipro.com', '9654321870', 5, 'HR Executive', 'Full-Time', '2022-09-01', 42000, 'On Leave'),
('Tanvi Bose', 'tanvi.bose@wipro.com', '9765432100', 2, 'Senior QA Lead', 'Full-Time', '2019-06-10', 65000, 'Active'),
('Karan Joshi', 'karan.joshi@wipro.com', '9988001122', 3, 'Process Trainer', 'Full-Time', '2021-04-25', 50000, 'Inactive'),
('Nisha Patel', 'nisha.patel@wipro.com', '9871122334', 1, 'Team Leader', 'Full-Time', '2020-08-18', 58000, 'Active');


insert into perf_reviews (emp_id, quarter, kpi_score, quality_score, csat_score, reviewed_by, review_date, comments) values
(1,  'Q4 2024', 92.5, 95.0, 88.0, 'Rajesh Sharma', '2025-01-10', 'strong team coaching, MIS reports accurate'),
(2,  'Q4 2024', 88.0, 91.0, 85.5, 'Priya Mehta',   '2025-01-12', 'consistent quality, no major issues'),
(3,  'Q4 2024', 76.0, 78.5, 80.0, 'Ankit Kumar',   '2025-01-15', 'needs to work on first call resolution rate'),
(4,  'Q4 2024', 84.5, 82.0, 79.0, 'Amit Verma',    '2025-01-11', 'good ops delivery this quarter'),
(5,  'Q4 2024', 95.0, 93.0, 91.0, 'Sunita Rao',    '2025-01-09', 'best MIS reports in the team, very reliable'),
(6,  'Q4 2024', 70.0, 73.0, 75.0, 'Ankit Kumar',   '2025-01-16', 'ok for contract level, can improve call handling'),
(8,  'Q4 2024', 97.0, 96.5, 94.0, 'Priya Mehta',   '2025-01-13', 'top performer in QA, consistent all year'),
(10, 'Q4 2024', 89.0, 90.0, 87.5, 'Rajesh Sharma', '2025-01-14', 'handles escalations well, good leadership');


insert into payroll (emp_id, month, basic, bonus, deductions, net_pay, pay_date, pay_status) values
(1,  'March 2025', 55000, 5000, 2000, 58000, '2025-03-31', 'Paid'),
(2,  'March 2025', 48000, 2000, 1500, 48500, '2025-03-31', 'Paid'),
(3,  'March 2025', 38000, 0,    1200, 36800, '2025-03-31', 'Paid'),
(4,  'March 2025', 52000, 3000, 1800, 53200, '2025-03-31', 'Paid'),
(5,  'March 2025', 60000, 6000, 2200, 63800, '2025-03-31', 'Paid'),
(6,  'March 2025', 32000, 0,    1000, 31000, '2025-03-31', 'Paid'),
(7,  'March 2025', 42000, 0,    1500, 40500, '2025-03-31', 'Pending'),
(8,  'March 2025', 65000, 8000, 2500, 70500, '2025-03-31', 'Paid'),
(9,  'March 2025', 50000, 0,    0,    50000, '2025-03-31', 'On Hold'),
(10, 'March 2025', 58000, 4000, 2000, 60000, '2025-03-31', 'Paid');


insert into leaves (emp_id, leave_type, start_date, end_date, days, status, applied_on) values
(3,  'Sick',   '2025-03-10', '2025-03-11', 2,  'Approved', '2025-03-09'),
(7,  'Earned', '2025-03-01', '2025-03-15', 15, 'Approved', '2025-02-25'),
(6,  'Casual', '2025-03-20', '2025-03-20', 1,  'Approved', '2025-03-19'),
(10, 'Casual', '2025-03-05', '2025-03-05', 1,  'Pending',  '2025-03-04'),
(2,  'Sick',   '2025-03-22', '2025-03-23', 2,  'Approved', '2025-03-22');


insert into attendance (emp_id, att_date, check_in, check_out, att_status) values
(1,  '2025-03-28', '09:02:00', '18:05:00', 'Present'),
(2,  '2025-03-28', '09:15:00', '18:00:00', 'Present'),
(3,  '2025-03-28', null,       null,       'Absent'),
(4,  '2025-03-28', '09:00:00', '18:10:00', 'Present'),
(5,  '2025-03-28', '08:55:00', '18:00:00', 'Present'),
(6,  '2025-03-28', '10:00:00', '14:00:00', 'Half Day'),
(7,  '2025-03-28', null,       null,       'Absent'),
(8,  '2025-03-28', '09:05:00', '18:00:00', 'Present'),
(9,  '2025-03-28', '09:30:00', '18:00:00', 'WFH'),
(10, '2025-03-28', '09:00:00', '18:00:00', 'Present');


-- queries section
-- these are the ones i use mostly for reporting


-- 1. employee list with dept info
select
    e.emp_id,
    e.name,
    e.role,
    d.dept_name,
    d.location,
    e.salary,
    e.status
from employees e
join departments d on e.dept_id = d.dept_id
order by d.dept_name;


-- 2. headcount and avg salary per department
select
    d.dept_name,
    count(e.emp_id) as total_emp,
    sum(case when e.status = 'Active' then 1 else 0 end) as active,
    round(avg(e.salary), 0) as avg_salary
from departments d
left join employees e on d.dept_id = e.dept_id
group by d.dept_name
order by avg_salary desc;


-- 3. performance ranking for Q4 2024
-- added overall score column manually, easier to read this way
select
    e.name,
    d.dept_name,
    pr.kpi_score,
    pr.quality_score,
    pr.csat_score,
    round((pr.kpi_score + pr.quality_score + pr.csat_score) / 3, 1) as overall_avg,
    case
        when (pr.kpi_score + pr.quality_score + pr.csat_score) / 3 >= 90 then 'Outstanding'
        when (pr.kpi_score + pr.quality_score + pr.csat_score) / 3 >= 80 then 'Good'
        when (pr.kpi_score + pr.quality_score + pr.csat_score) / 3 >= 70 then 'Average'
        else 'Needs Improvement'
    end as rating,
    pr.comments
from perf_reviews pr
join employees e on pr.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id
where pr.quarter = 'Q4 2024'
order by overall_avg desc;


-- 4. payroll report for march 2025
-- flagging unpaid ones as exceptions (same logic i use in excel mis)
select
    e.name,
    d.dept_name,
    p.basic,
    p.bonus,
    p.deductions,
    p.net_pay,
    p.pay_status,
    case
        when p.pay_status != 'Paid' then 'Exception - Check Required'
        else '-'
    end as flag
from payroll p
join employees e on p.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id
where p.month = 'March 2025'
order by p.pay_status;


-- 5. attendance report - 28 march
select
    e.name,
    d.dept_name,
    a.check_in,
    a.check_out,
    a.att_status,
    case
        when a.check_in > '09:30:00' then 'Late'
        when a.att_status = 'Absent' then 'Follow Up Needed'
        else 'OK'
    end as remark
from attendance a
join employees e on a.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id
order by a.att_status;


-- 6. leave report
select
    e.name,
    d.dept_name,
    l.leave_type,
    l.start_date,
    l.end_date,
    l.days,
    l.status
from leaves l
join employees e on l.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id
order by l.start_date desc;


-- 7. who hasnt been reviewed yet
-- useful for identifying data gaps before submitting reports
select
    e.emp_id,
    e.name,
    d.dept_name,
    e.role,
    e.status
from employees e
left join perf_reviews pr on e.emp_id = pr.emp_id
join departments d on e.dept_id = d.dept_id
where pr.review_id is null;


-- 8. dept wise payroll total
select
    d.dept_name,
    count(p.emp_id) as emp_count,
    sum(p.basic) as total_basic,
    sum(p.bonus) as total_bonus,
    sum(p.deductions) as total_deductions,
    sum(p.net_pay) as total_payout
from payroll p
join employees e on p.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id
where p.month = 'March 2025'
group by d.dept_name
order by total_payout desc;


-- 9. salary vs kpi cross check
-- added this to spot if high paid employees are actually performing
select
    e.name,
    e.salary,
    pr.kpi_score,
    case
        when e.salary > 55000 and pr.kpi_score < 80 then 'High Salary, Low KPI - Review Needed'
        when e.salary > 55000 and pr.kpi_score >= 90 then 'High Salary, High KPI - Justified'
        when e.salary <= 55000 and pr.kpi_score >= 90 then 'Good Value Employee'
        else 'Normal'
    end as analysis
from employees e
join perf_reviews pr on e.emp_id = pr.emp_id
order by e.salary desc;


-- 10. stored procedure to pull one employee full details at once
-- helpful when hr asks for a quick summary

delimiter //

create procedure get_emp_details(in p_id int)
begin
    select e.name, e.role, d.dept_name, e.salary, e.status
    from employees e
    join departments d on e.dept_id = d.dept_id
    where e.emp_id = p_id;

    select quarter, kpi_score, quality_score, csat_score, comments
    from perf_reviews
    where emp_id = p_id
    order by review_date desc
    limit 1;

    select month, net_pay, pay_status
    from payroll
    where emp_id = p_id
    order by pay_date desc
    limit 1;

    select leave_type, start_date, end_date, days, status
    from leaves
    where emp_id = p_id
    order by applied_on desc;

end //

delimiter ;

-- to use: call get_emp_details(1);


-- views for quick access

create view active_employees as
select e.emp_id, e.name, e.role, d.dept_name, e.salary
from employees e
join departments d on e.dept_id = d.dept_id
where e.status = 'Active';


create view pending_payments as
select e.name, d.dept_name, p.month, p.net_pay, p.pay_status
from payroll p
join employees e on p.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id
where p.pay_status != 'Paid';


create view perf_summary as
select
    e.name,
    d.dept_name,
    pr.quarter,
    round((pr.kpi_score + pr.quality_score + pr.csat_score) / 3, 1) as avg_score
from perf_reviews pr
join employees e on pr.emp_id = e.emp_id
join departments d on e.dept_id = d.dept_id;
