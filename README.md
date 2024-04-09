# Botulism-project
select * from botulism

The questions we are going to answer:
    1. what state has the highest number of cases of botulism
    2. Of the state how many cases were there
    3. What state has  the lowest number of botulism
    4. Of that state how many cases were there
    5. What year was there the highest cases of botulism
    6. What state had the highest case that year 
    

(Select STATE, SUM(COUNT) AS "NUMBER OF CASES" from Botulism
Group by STATE
ORDER BY "NUMBER OF CASES") 

Here we can see the California has the highest amount of cases at 2598 and Vermont/New Hampshire 
    are tied for the lowest at 3 cases 

To confirm we indeed have the highest and lowest cases we can do a subquery as shown

Select min ("Number of cases") as "Minimum number of cases" from (select STATE, SUM (COUNT) AS "Number of cases" FROM Botulism
Group by State)  

Select max ("Number of cases") as "Maximum number of cases" from (select STATE, SUM (count) as "Number of cases" from botulism
Group by STATE)

Next we will query the number of cases per year

Select Year, SUM(COUNT) AS "Number of Cases" from botulism
Group by Year
ORDER BY "Number of Cases"

Here it shows that the lowest amount of cases occured in 1911 with 1 cases noted nation wide
    and highest amount of cases occured in 2016 with 206 cases

Select State, Sum(Count) AS "Number of Cases" from botulism
Where Year = 2016
Group by STATE
ORDER BY "Number of Cases" 

Here we see California had the most cases this year at 66 cases being....

Select (ROUND ((Select SUM(COUNT) AS "Number of Cases" from botulism Where STATE = 'California' AND Year = 2016) / 
(Select Sum(Count) AS "Number of Cases" from botulism Where Year = 2016) * 100)) || '%' as "Ratio" from botulism where state = 'California'
Group by STATE

...32% of all cases in 2016
