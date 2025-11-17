# hospital-management-sql-project
SQL project analyzing hospital data: patients, doctors, stays, and medical expenses.
#Overview
#Objectives
#Schema
```sql
create table hospital(
 hospital_name varchar(100),
 location varchar(100),
 department varchar(100),
 doctor_count int,
 patient_count int,
 addmission_date date,
 discharge_date date,
 medical_expenses numeric(10,2)
 );```

## Problems And solutions

### 1. average on of doctors per hospital

```sql
select
hospital_name, avg(doctor_count) as avg_doctors
from hospital
group by hospital_name ```


### 2.top 3 department with the highest no of patient 

```sql
select
department, count(patient_count) as patientcount
from hospital 
group by department
order by patientcount
desc limit 3```

### 3.hospital with the maximum medcal expenses

```sql
select
hospital_name, medical_expenses
from hospital
order by medical_expenses
desc limit 1;
```

### 4.daily average medical expense

```sql
SELECT 
    addmission_date,
    ROUND(AVG(medical_expenses), 2) AS daily_avg_expense
FROM hospital
GROUP BY addmission_date
ORDER BY addmission_date;```

### 5.longest hospital stay

```sql
SELECT 
    hospital_name,
    location,
    department,
    addmission_date,
    discharge_date,
    (discharge_date - addmission_date) AS stay_duration_days
FROM hospital
ORDER BY stay_duration_days DESC
LIMIT 1;
```



### 6.total patient treated per city

```sql
select
location, sum(patient_count) as total_patient_pr_city
from hospital
group by location
```
### 7.average  lenght of stay per department

```sql
select
 addmission_date-coalesce(sum(discharge_date),0) as stay
from hospital group by department```


### 8.identify the department with the lowest number of patients 

```sql
select
 department, patient_count
from hospital
order by patient_count
asc limit 1```
