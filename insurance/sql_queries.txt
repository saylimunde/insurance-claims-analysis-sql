use insurance;

select * from insurance_data;

-- What are the top 5 patients who claimed the highest insurance amounts?

select *, dense_rank() over(order by claim desc) from insurance_data limit 5;

-- What is the average insurance claimed by patients based on the number of children they have?

select children,avg_claim,row_num from (select *,
avg(claim) over(partition by children) as avg_claim,
ROW_NUMBER() over(partition by children) as 'row_num'
from insurance_data ) as t
where t.row_num = 1;

-- What is the highest and lowest claimed amount by patients in each region?

SELECT region,max_claim,min_claim FROM (SELECT *, MAX(claim) OVER(PARTITION BY region) as 'max_claim',
MIN(claim) OVER(PARTITION BY region) as 'min_claim',
ROW_NUMBER() OVER(PARTITION BY region) as rn
FROM insurance_data) AS t
where t.rn = 1;

-- What is the difference between the claimed amount of each patient and the first claimed amount of that patient?

SELECT *, claim - first_value(claim) over() as diff from insurance_data;

-- For each patient, calculate the difference between their claimed amount and the average 
-- claimed amount of patients with the same number of children.

select *,claim - avg(claim) over(partition by children) from insurance_data;

--  Show the patient with the highest BMI in each region and their respective rank.

select * from (SELECT *,
rank() over(partition by region order by bmi desc) as 'group_rank',
rank() over(order by bmi desc) as 'overall_rank'
from insurance_data) t 
where t.group_rank = 1;

--  Calculate the difference between the claimed amount of each patient and 
 -- the claimed amount of the patient who has the highest BMI in their region.
 
 SELECT *, 
 claim - first_value(claim) over(partition by region order by bmi desc) 
 from insurance_data;
 
 --  For each patient, calculate the difference in claim amount between the patient and 
 -- the patient with the highest claim amount among patients with the smoker status, 
 -- within the same region. Return the result in descending order difference.
 
SELECT *,
(MAX(claim) OVER(PARTITION BY region,smoker) - claim) as claim_diff
FROM insurance_data
ORDER BY claim_diff DESC;

 -- For each patient, find the maximum BMI value among their next three records (ordered by age).
 
 select *,
 max(bmi) over(order by age ROWS BETWEEN 1 FOLLOWING AND 3 FOLLOWING)
 from insurance_data;
 
 -- For each patient, find the rolling average of the last 2 claims.

SELECT *,
avg(claim) OVER(ROWS BETWEEN 2 PRECEDING AND 1 PRECEDING) 
from insurance_data;

 -- Find the first claimed insurance value for male and female patients, 
 -- within each region order the data by patient age in ascending order, 
 -- and only include patients who are non-diabetic and have a bmi value between 25 and 30.

with filtered_data as (
	select * from insurance_data
    where diabetic = 'No' and bmi between 25 and 30
)

select region,gender,first_claim from (select *,
first_value(claim) over(partition by region,gender order by age) as 'first_claim',
row_number() over(partition by region,gender order by age) as 'row_num'
from filtered_data) t 
where t.row_num = 1


