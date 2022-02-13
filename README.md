# Pewlett-Hackard-Analysis

##Overview
###Purpose The purpose of this analysis was to use PostgreSQL to create new tables of Pewlett-Hackard employee data that is stored in CSV files. Queries were used to group employees that are eligible for retirement to provide insight into how Hewlett-Packard can handle the incoming "silver tsunami"

##Results
### - Retirement Title table that holds all the titles of employees who were born between January 1, 1952 and December 31, 1955 returned 133,776 employees.

### - There are duplicate entries for some employees because they have switched titles over the years, so this query was used to create to create unique_titles.csv. This unique list trimmed the results down to 72,458.

```
SELECT DISTINCT ON (rt.emp_no) rt.emp_no,
rt.first_name,
rt.last_name,
rt.title
INTO unique_titles
FROM retirement_titles AS rt
WHERE (rt.to_date = '9999-01-01')
ORDER BY rt.emp_no, rt.to_date DESC;

SELECT * FROM unique_titles LIMIT 10;
```

### - 72,458 employees are eligible for retirement, and this table shows those 72,458 employees grouped by title.
![retirement_eligible_titles](https://user-images.githubusercontent.com/96211484/153728896-5b4abfc3-8e41-402c-ac6d-2664116ddc73.png)

### - Deliverable 2 looks at employees eligible for mentorship, which is only 1,549.
![mentorship_eligibility](https://user-images.githubusercontent.com/96211484/153729321-c84b8efa-e4aa-4b9f-a013-8896b93489a6.png)

##Summary
As mentioned above, 72,458 roles will need to be filled as the "silver tsunami" begins to make an impact. Unfortunately for Pewlitt-Hackard only 1549 employees fit the criteria for the mentorship program.

A new query and a quick change to the parameters to increase the amount of employees eligible for the program would be to expand the birth_date window 3 years from between 1965-1965 to between 1962-1965.

The query 

```
SELECT DISTINCT ON(e.emp_no) e.emp_no,
    e.first_name,
    e.last_name,
    e.birth_date,
    de.to_date,
    de.from_date,
    t.title

INTO mentorship_eligibility_II
FROM employees as e
INNER JOIN titles as t
    ON (e.emp_no = t.emp_no)
INNER JOIN dept_employees as de
    ON (e.emp_no = de.emp_no)
WHERE (de.to_date = '9999-01-01')
    AND (e.birth_date BETWEEN '1965-01-01' AND '1962-12-31')
ORDER BY e.emp_no;

SELECT * FROM mentorship_eligibility_II; 
```

returns 73,851 employees. But since not every single employee would enroll in the mentorship program it would be safer to expand the birth_date window to 5 years, i.e (birth_date BETWEEN '1960-01-01' AND '1965-12-31')
