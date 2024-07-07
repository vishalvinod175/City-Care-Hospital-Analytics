# Heathcare-Analytics-PowerBI-DAX-Queries   

City Care Hospital is a renowned hospital in Bengaluru. They want to get a better understanding of their patient background and needs so that the hospital can assist them in better ways.

**Problem Statement** -
With plans of improving the hospital's services, the CEO of City Care Hospital has asked Vishal Vinod to analyse the provided sample data and report key findings to the management of City Care Hospital. This analysis is expected to guide them in serving their patients better and make sure their treatments involve lesser hassles. 

Vishal’s task is to focus on implementing suggested metrics, designing an easy-to-understand dashboard, and creatively presenting key insights to City Care Hospital's  top-level management and strategy team.

**Tools Used** - Microsoft PowerBI for Desktop Application   

# Building the Dashboard   
 
 * Load all the Data. Open the PowerQuery Editor to change the name of the tables and columns, according to your ease. Make sure the data is accurate with the correct Datatypes.
* Rename the tables for your ease of work. Check that the headers have been promoted.
* Establish relationships between tables.
* Created custom and quick measures for key metrics and insights.
* Utilized DAX queries for performing BI calculations.
* Designed KPIs to highlight important metrics at a glance.
* Created a dashboard highlighting various insights about Patient Frequencies, Satisfaction scores, etc.
* Made use of different visualizations for various types of data, such as Data Tiles, bar/column charts and Line charts.


# Model View   

![2024-07-07 (8)](https://github.com/vishalvinod175/City-Care-Hospital-Analytics/assets/164670302/788e0e7a-3ab5-4c73-a4ff-b428787d7161)   

* Add a Parameter to switch between "Average Wait time" and "Average Patient Satisfaction Score" to use in the form of a slicer.
* Go to the Model View to connect the "Date" Columns from "date" table and "Hospital ER" table.



# Final Dashboard   

![2024-07-07 (9)](https://github.com/vishalvinod175/City-Care-Hospital-Analytics/assets/164670302/b6fa83e7-2595-42b7-be2b-55676acb84b8)   
![2024-07-07 (10)](https://github.com/vishalvinod175/City-Care-Hospital-Analytics/assets/164670302/56f241b4-9efb-49d1-92e0-f19d01c6dc13)













1) Load the Data. Open the PowerQuery Editor to change the name of the tables and columns, according to your ease. Make sure the data is accurate with the correct Datatypes.
2) Open the table view, you can create a new table to accomodate new Measures and Columns.
3) Measure 1 - **"Total Patients"** -  
`Total Patients = COUNTROWS('Hospital ER')`
4) Measure 2 - **"%Non-Administrative Privelege"** -  
`DIVIDE(COUNTROWS(FILTER('Hospital ER','Hospital ER'[patient_admin_flag]=FALSE())),[Total Patients])`  (Format to **Percentage**)
5) Measure 3 - **"%Administrative Privelege"** -  
 `DIVIDE(COUNTROWS(FILTER('Hospital ER','Hospital ER'[patient_admin_flag]=TRUE())),[Total Patients])` (Format to **Percentage**)
6) Measure 4 - **"Average Patient Satisfaction Score"** -  
 `CALCULATE(AVERAGE('Hospital ER'[patient_sat_score]),'Hospital ER'[patient_sat_score]<>BLANK())` (Calculate function will help us filter out all BLANK values)
7) Measure 5 - **"No Rating"** -  
`VAR _noRatings =   
CALCULATE(
[Total Patients],
'Hospital ER'[patient_sat_score]=BLANK())
RETURN
DIVIDE(
_noRatings,
[Total Patients]
)`  
9) Measure 6 - **"Average Wait Time"** =  
`AVERAGE('Hospital ER'[patient_waittime])`
10) Add Column 1 - **"Age Buckets"** -  
`SWITCH(TRUE(),'Hospital ER'[patient_age]<=10,"0-10",'Hospital ER'[patient_age]<=20,"11-20",'Hospital ER'[patient_age]<=30,"21-30",'Hospital ER'[patient_age]<=40,"31-40",'Hospital ER'[patient_age]<=50,"41-50",'Hospital ER'[patient_age]<=60,"51-60",'Hospital ER'[patient_age]<=70,"61-70","70+")`
   ** Add a Parameter to switch between "Average Wait time" and "Average Patient Satisfaction Score"** Use it in the form of a slicer
11) Add Column 2 - **"Age Group"** -  
`VAR _PatientAge = 'Hospital ER'[patient_age]
RETURN
IF(
     _PatientAge<=2,"Infancy",
    IF(_PatientAge<=6,"Early Childhood",
       IF(_PatientAge<=12,"Midde Childhood",
          IF(_PatientAge<=18,"Teenager",
          "Adult"
          )
       )
    )
)`
12) Add Table - **"Date"** -  
`ADDCOLUMNS(CALENDARAUTO(),"Year",YEAR([Date]),"Month",FORMAT([Date],"mmm"),"Weektype",IF(WEEKDAY([DATE])=1,"Weekend",IF(WEEKDAY([Date])=7,"Weekend","Weekday")),"Weekday",FORMAT([Date],"ddd"),"MonthNum",MONTH([Date]))` Set to "Mark as Date Table" to replace the default table, format the table
13) Go to the Model View to connect the "Date" Columns from "date" table and "Hospital ER" table
14) Measure 7 - **"% Un-Referred"** -   
`VAR _filterpatients =
    CALCULATE([Total Patients],'Hospital ER'[department_referral]="none")
    RETURN DIVIDE(_filterpatients,[Total Patients])` (Format to **Percentage**)
15) Measure 8 - **"% Referred"** -  
 `VAR _filterpatients =
    CALCULATE([Total Patients],'Hospital ER'[department_referral]<>"none")
    RETURN DIVIDE(_filterpatients,[Total Patients])` (Format to **Percentage**)
16) Measure 9 - **"Heatmap Caption"** -  
`VAR _selectedmeasure =
    SELECTEDVALUE(Parameter[Parameter Order])
    RETURN
    IF(_selectedmeasure=0,
    "The Darkest Green indicates Low Wait time on the Age Group","Patients are most satisfied when Dark Green is shown on Age Group")`
17) Measure 10 - **"% Male Patients"** -  
`DIVIDE(CALCULATE([Total Patients],'Hospital ER'[patient_gender]="M"),[Total Patients])` (Format to **Percentage**)
18) Measure 11 - **"%Female Patients**" -  
`DIVIDE(CALCULATE([Total Patients],'Hospital ER'[patient_gender]="F"),[Total Patients])` (Format to **Percentage**)
19) You can design the report in your own ways through the Measures above. Thank you.







