# Heathcare-Analytics-PowerBI-DAX-Queries

1) Load the Data. Open the PowerQuery Editor to change the name of the tables and columns, according to your ease. Make sure the data is accurate with the correct Datatypes.
2) Open the table view, you can create a new table to accomodate new Measures and Columns.
3) Measure 1 - **"Total Patients"** - `Total Patients = COUNTROWS('Hospital ER')`
4) 4) Measure 2 - **"%Non-Administrative Privelege"** - `DIVIDE(COUNTROWS(FILTER('Hospital ER','Hospital ER'[patient_admin_flag]=FALSE())),[Total Patients])`  (Format to **Percentage**)
5) Measure 3 - **"%Administrative Privelege"** -  `DIVIDE(COUNTROWS(FILTER('Hospital ER','Hospital ER'[patient_admin_flag]=TRUE())),[Total Patients])` (Format to **Percentage**)
6) Measure 4 - **"Average Patient Satisfaction Score"** - `CALCULATE(AVERAGE('Hospital ER'[patient_sat_score]),'Hospital ER'[patient_sat_score]<>BLANK())` (Calculate function will help us filter out all BLANK values)
7) Measure 5 - **"No Rating"** -
   `VAR _noRatings = 
   CALCULATE(
    [Total Patients],
    'Hospital ER'[patient_sat_score]=BLANK()
   )
   RETURN
   DIVIDE(
    _noRatings,
    [Total Patients]
   )`
8) Measure 6 - **"Average Wait Time"** = `AVERAGE('Hospital ER'[patient_waittime])`
9) Add Column 1 - **"Age Buckets"** -
   `SWITCH(TRUE(),'Hospital ER'[patient_age]<=10,"0-10",'Hospital ER'[patient_age]<=20,"11-20",'Hospital ER'[patient_age]<=30,"21-30",'Hospital ER'[patient_age]<=40,"31-40",'Hospital ER'[patient_age]<=50,"41-50",'Hospital ER'[patient_age]<=60,"51-60",'Hospital ER'[patient_age]<=70,"61-70","70+")`
   ** Add a Parameter to switch between "Average Wait time" and "Average Patient Satisfaction Score"** Use it in the form of a slicer
10) Add Column 2 - **"Age Group"** -
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
11) Add Table - **"Date"** -  `ADDCOLUMNS(CALENDARAUTO(),"Year",YEAR([Date]),"Month",FORMAT([Date],"mmm"),"Weektype",IF(WEEKDAY([DATE])=1,"Weekend",IF(WEEKDAY([Date])=7,"Weekend","Weekday")),"Weekday",FORMAT([Date],"ddd"),"MonthNum",MONTH([Date]))` Set to "Mark as Date Table" to replace the default table, format the table
12) Go to the Model View to connect the "Date" Columns from "date" table and "Hospital ER" table
13) Measure 7 - **"% Un-Referred"** - 
`VAR _filterpatients =
    CALCULATE([Total Patients],'Hospital ER'[department_referral]="none")
    RETURN DIVIDE(_filterpatients,[Total Patients])` (Format to **Percentage**)
14) Measure 8 - **"% Referred"** -
 `VAR _filterpatients =
    CALCULATE([Total Patients],'Hospital ER'[department_referral]<>"none")
    RETURN DIVIDE(_filterpatients,[Total Patients])` (Format to **Percentage**)
15) Measure 9 - **"Heatmap Caption"** -
`VAR _selectedmeasure =
    SELECTEDVALUE(Parameter[Parameter Order])
    RETURN
    IF(_selectedmeasure=0,
    "The Darkest Green indicates Low Wait time on the Age Group","Patients are most satisfied when Dark Green is shown on Age Group")`
16) Measure 10 - **"% Male Patients"** - `DIVIDE(CALCULATE([Total Patients],'Hospital ER'[patient_gender]="M"),[Total Patients])` (Format to **Percentage**)
17) Measure 11 - **"%Female Patients**" -  `DIVIDE(CALCULATE([Total Patients],'Hospital ER'[patient_gender]="F"),[Total Patients])` (Format to **Percentage**)
18) You can design the report in your own ways through the Measures above. Thank you.
19) Final Result -


    ![2024-06-09 (3)](https://github.com/viskypapi/Heathcare-Analytics-PowerBI-DAX-Queries/assets/164670302/9bc605f1-9a9b-4fee-aef7-6ab08ae11884)













          ![2024-06-09 (3)](https://github.com/viskypapi/Heathcare-Analytics-PowerBI-DAX-Queries/assets/164670302/7585544f-05df-40dd-b164-c72627ecfa6d)
