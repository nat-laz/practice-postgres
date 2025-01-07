## Exercises
### Basic Queries

```sql
-- 1. List all employees in the IT department
SELECT *
FROM employees
WHERE department = 'IT';

-- 2. Find employees with salaries greater than 70000
SELECT *
FROM employees
WHERE salary > 70000
ORDER BY salary DESC;

-- 3. List all active employees ordered by hire date
SELECT *
FROM employees
WHERE is_active
ORDER BY hire_date;

-- 4. Find all employees hired between 2019 and 2020
SELECT *
FROM employees
WHERE hire_date BETWEEN '2019-01-01' AND '2020-01-01';
```

### Logical Expressions

```sql
-- 1. Find all employees who are either in IT department OR earn more than 70000
SELECT *
FROM employees
WHERE department = 'IT'
   OR salary > 70000
ORDER BY salary DESC;

-- 2. List employees who are both active AND hired after 2019
SELECT *
FROM employees
WHERE is_active
  AND hire_date >= '2019-01-01'::date
ORDER BY hire_date;


-- 3. Find employees who are NOT in the Marketing department
SELECT *
FROM employees
WHERE department != 'Marketing';

-- 4. Create a column showing TRUE if employee salary is above department average, FALSE otherwise
WIP
```


### Aggregation

```sql
-- 1. Calculate the average salary by department
SELECT department,
       ROUND(AVG(salary)::numeric, 2) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;


-- 2. Find the department with the highest total salary
SELECT department,
       ROUND(SUM(salary)::numeric, 0) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC;

-- 3. Count the number of projects per department
SELECT d.dept_name,
       count(pr.dept_id) AS nr_of_projects
FROM departments d
         JOIN projects pr ON d.dept_id = pr.dept_id
GROUP BY d.dept_name
ORDER BY nr_of_projects DESC;

-- 4. Calculate the total hours allocated per project
SELECT pr.project_name,
       sum(hours_allocated) AS hr_allocated
FROM projects pr
         JOIN employee_projects em_pr ON pr.project_id = em_pr.project_id
GROUP BY pr.project_name
ORDER BY hr_allocated DESC;

-- 5. Find departments where the average salary is above 70000
SELECT department,
       ROUND(AVG(salary)::numeric, 2) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) < 70000;
```