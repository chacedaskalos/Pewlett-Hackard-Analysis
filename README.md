# Pewlett-Hackard-Analysis

##**Overview**
###Purpose The purpose of this analysis was to use PostgreSQL to create new tables of Pewlett-Hackard employee data that is stored in CSV files. Queries were used to group employees that are eligible for retirement to provide insight into how Hewlett-Packard can handle the incoming "silver tsunami"

##**Results**
### - There are duplicate entries for some employees because they have switched titles over the years, so this query was used to create to create unique_titles.csv

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

### - 
