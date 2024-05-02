# sql-challenge

Drop table if exists departments;
Drop table if exists dept_emp;
Drop table if exists dept_manager;
Drop table if exists employees;
Drop table if exists salaries;
Drop table if exists titles;

create table departments(
	dept_no varchar primary key,
	dept_name varchar NOT NULL
);

create table dept_emp(
	emp_no int,
	dept_no varchar
);


create table dept_manager(
	dept_no varchar,
	emp_no int
);

create table employees(
	emp_no int,
	emp_title_id varchar,
	birth_date varchar NOT NULL,
	first_name varchar NOT NULL,
	last_name varchar NOT NULL,
	sex varchar NOT NULL,
	hire_date varchar NOT NULL	
);

create table salaries(
	emp_no int,
	salary int
);



create table titles(
	title_id varchar NOT NULL,
	title varchar NOT NULL
);

select *
from departments;

select *
from dept_emp;

select *
from employees;

select *
from salaries;

select *
from titles;

select *
from dept_manager;

-- 1 List id last name first name sex salary
select de.emp_no,employees.last_name,employees.first_name,employees.sex,salaries.salary
from dept_emp as de
inner join employees on
employees.emp_no = de.emp_no
inner join salaries on
salaries.emp_no = de.emp_no;

-- 2 List first name last name hire date = 1986
select first_name,last_name,hire_date
from employees
where hire_date like '%1986';

-- 3 List Mgr of dept w/ dep no dep nam emp no last name and first name
select departments.dept_no,departments.dept_name,dept_manager.emp_no,employees.last_name,employees.first_name
from departments
inner join dept_manager on
departments.dept_no = dept_manager.dept_no
inner join employees on
dept_manager.emp_no = employees.emp_no
where employees.emp_title_id = 'm0001';

-- 4 List the depatment number for each employee along with that employee's employee number, last name, first name and department name
select dept.dept_no, dept.dept_name,dept_emp.emp_no,employees.last_name,employees.first_name
from departments as dept
inner join dept_emp on
dept.dept_no = dept_emp.dept_no
inner join employees on 
dept_emp.emp_no = employees.emp_no;

-- 5 List first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B.
select first_name,last_name,sex
from employees
where first_name = 'Hercules'
and last_name like 'B%';

-- 6  List each employee in the Sales department, including their employee number, last name and first name.
select dept.dept_name,employees.emp_no,employees.last_name,employees.first_name
from departments as dept
inner join dept_emp on
dept.dept_no = dept_emp.dept_no
inner join employees on
dept_emp.emp_no = employees.emp_no
where dept.dept_no = 'd007';

-- 7  List each employee in the Sales and Development departments, including their employee number, last name, first name and department name.
select dept.dept_name,employees.emp_no,employees.last_name,employees.first_name
from departments as dept
inner join dept_emp on
dept.dept_no = dept_emp.dept_no
inner join employees on
dept_emp.emp_no = employees.emp_no
where dept.dept_no = 'd007'
or dept.dept_no = 'd005';

--8 List the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name).
select last_name,count(last_name) as "Duplicate Name"
from employees
group by last_name
order by "Duplicate Name" desc;
