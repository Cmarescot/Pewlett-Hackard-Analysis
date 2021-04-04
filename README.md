# Pewlett-Hackard-Analysis

## Overview of Analysis 
### Purpose 
In this analysis we imported csv files and created tables in PgAdmin. 
Using the tables we ceated we queried through them in order to gather information on employees that were due for retirement 

In this challenge specifically  we were tasked with:
- Determining the number of retiring employees for each title
- Identifying employees who are eligible  to participate in the mentorship program 

## Results 
Our analysis found that:
- Senior Engineers had the most amount of retiring employees of 29414
- Senior Staff had the second most amount of retiring employees of 28254
- 2 Managers are retiring 
![title_count]()
- There are 1549 eligible to partcipate in the mentorship program  
![eligibility]()

## Summary 
### Key Takeaways
- 90398 roles will need to be filled as the "silver tsunami" begins to make an impact 
- With only 1549 elegible retireers able to partcipate in the mentorship program, there are not enough mentors for the next generation of Pewlett Hackward employees
### More Queries
- In addition to the queries we've also peformed we can use the querie :
      
      SELECT COUNT(me.title), 
      me.title
      FROM mentorship_eligibililty as me
      GROUP BY me.title 
      ORDER BY count DESC;
      
  In order to find out how many possible mentors are eligible for each title. This can help the company allocate it's resources and figure out which departments are going to need more assistance with the next generation of Pewlett Hackward employees .
  
  Our query above returns a table that looks like this:
  ![mentors_per_title]()
  
  ### Employees Retiring by Departments 
  Lasty, we can perform the same query we performed on titles, but this time with each departments. We can do this by first: 
  - Adding a departments column to our unique titles query and removing the titles column:
           
           --Retiring by Departments  
              SELECT DISTINCT ON (rt.emp_no)
              rt.emp_no,
              rt.first_name,
              rt.last_name,
              rt.title,
              d.dept_name
              INTO unique_managers2
              FROM retirement_titles as rt
              INNER JOIN dept_emp as de
              ON (rt.emp_no = de.emp_no)
              INNER JOIN departments as d
              ON(de.dept_no = d.dept_no);
  - Grouping our retiring employee count table by departments 
              
              SELECT COUNT(um.dept_name), 
              um.dept_name
              --INTO retiring_titles
              FROM unique_managers2 as um
              GROUP BY um.dept_name 
              ORDER BY count DESC;
    Our results look like the following 
    ![count_by_departments]()
    
With these results we can get a better idea of which departments will be needed the most help when it comes to training in the future. 
