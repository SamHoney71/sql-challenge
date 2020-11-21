SQL Challenge Notes & Content Description


Data Modeling

1.  I used the Quick Database Design website (http://www.quickdatabasediagrams.com/) to model and design the data tables.
Andrew Perez helped me with understanding how to use the site's syntax to connect tables using Foreign Keys.

	a. quickdatabasescript_Jeter.txt: contains the text that was entered into the website to create the visual tables.
	b. QuickDBD-export_Design_Jeter.png: contains the data table design image from the Website.

2. QuickDBD-export.sql: Quick Database Design provides the capability to export to PostgreSQL to create the tables.
When I imported the data from the CSV files into the tables, all worked except the dep_emp table.  
I manually created this table, and then imported the successfully. 


4. Data_Analysis.sql: Contains the 8 assignments. Below is the Syntax:

--1. List the following details of each employee: 
--employee number, last name, first name, sex, and salary.
-- Works
SELECT e.emp_no, last_name, first_name, sex, salary 
FROM employees e 
JOIN salaries s ON (e.emp_no = s.emp_no)

--2. List first name, last name, and hire date for employees who were hired in 1986.
--- Slack:Ask the Class & Andrew Perez helped me with the Syntax "EXTRACT (YEAR FROM ...)".

SELECT first_name, last_name, hire_date FROM employees e
WHERE EXTRACT(YEAR FROM e.hire_date) = 1986

--3. List the manager of each department with the following information: 
--department number, department name, the manager's employee number, last name, first name.
-- Works
SELECT
	dm.dept_no AS department_number, 
	dnam.dept_name AS department_name,
	e.emp_no AS manager_employee_number,
	last_name AS manager_last_name,
	first_name AS manager_first_name 

FROM
	employees e
	INNER JOIN dept_manager dm ON (e.emp_no = dm.emp_no)
	INNER JOIN departments dnam ON (dnam.dept_no = dm.dept_no)

--4. List the department of each employee with the following information: 
--employee number, last name, first name, and department name.
--Works
SELECT
	e.emp_no AS employee_number,
	last_name,
	first_name,
	dept_name AS department_name

FROM 
	employees e
	JOIN dept_emp de ON (e.emp_no = de.emp_no)
	JOIN departments dnam ON (dnam.dept_no = de.dept_no)

--5. List first name, last name, and sex for employees whose first name
--is "Hercules" and last names begin with "B."
-- Works
SELECT
	first_name AS first_name_Hercules,
	last_name AS last_name_start_with_B,
	sex
FROM employees
WHERE first_name = 'Hercules' AND last_name LIKE 'B%'

--6. List all employees in the Sales department, 
--including their employee number, last name, first name, and department name.
--Works
SELECT
	e.emp_no AS employee_number,
	last_name,
	first_name,
	dept_name AS department_name

FROM 
	employees e
	JOIN dept_emp de ON (e.emp_no = de.emp_no)
	JOIN departments dnam ON (dnam.dept_no = de.dept_no)

WHERE dept_name = 'Sales'

--7. List all employees in the Sales and Development departments, 
--including their employee number, last name, first name, and department name.
--Works

SELECT
	e.emp_no AS employee_number,
	last_name,
	first_name,
	dept_name AS department_name

FROM 
	employees e
	JOIN dept_emp de ON (e.emp_no = de.emp_no)
	JOIN departments dnam ON (dnam.dept_no = de.dept_no)

WHERE dept_name = 'Development' OR dept_name = 'Sales' 

--8. In descending order, list the frequency count of employee last names,
--i.e., how many employees share each last name.
--Works

SELECT last_name, COUNT(last_name) AS "Count of Last Name"
FROM employees
GROUP BY last_name 
ORDER BY COUNT(last_name) DESC


5. Folder-data:  contains the csv files: