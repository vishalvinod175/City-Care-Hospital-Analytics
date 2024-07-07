# City Care-Hospital-PowerBI-DAX-Queries   

City Care Hospital is a renowned hospital. They want to get a better understanding of their patient background and needs so that the hospital can assist them in better ways.

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

# Key Metrics   
* Total number of patients were 4998.
* Gender Distribution: 51.24% Male, 48.48% Female and 0.28% Unknown.
* ### Age Distribution: Adults constitute the majority at 3832 patients.
*  ### Visit Trends-   
1. Monthly Distribution:   
        Peak in May with 581 patients.   
        Lowest in December with 246 patients.    

2. Weektype Distribution:   
        3576 patients on weekdays.
        1422 patients on weekends.

3. Yearly Distribution:    
        2019: 2351 patients    
        2020: 2647 patients    

* ### Patient Feedback-

    Rating:   
        76% of patients gave no rating.    
    Satisfaction Score:    
        Average satisfaction score is 5.    
    Average Wait Time:    
        35 minutes on average.    
    Referral Status:    
        40.90% of patients were referred.     
        59.10% were not referred.     

* ### Departments and Referrals

    Departments Referred to:    
        General Practice: 986 patients    
        Orthopedics: 504 patients     
        Physiotherapy: 172 patients   
        Cardiology: 132 patients   
        Gastroenterology: 104 patients   
        Neurology: 101 patients    
        Renal: 45 patients    
        None: 2954 patients       

* ### Patient Race and Satisfaction    
Patient satisfaction varies by age and race, with the dark green indicating the highest satisfaction scores. Specific breakdowns by race are not provided but can be deduced from the heatmap.   

# Recommendations   

* ### Improve Patient Feedback Collection   

Increase Feedback Participation:    
Develop a more engaging feedback system, such as user-friendly digital surveys that patients can complete on their mobile devices. Consider follow-up surveys via email or SMS for patients who did not provide feedback during their visit.

* ### Optimize Resource Allocation    

Adjust Staffing Based on Volume Trends:   
1. Increase staffing levels during peak months like May and higher-volume weekdays to handle the increased patient load efficiently.   
2. Implement a flexible staffing schedule to better manage patient influx during off-peak times, such as December and weekends.    

* ### Enhance Operational Efficiency   

Reduce Wait Times:
1. Streamline the triage process to ensure quick and efficient patient assessment and prioritization, potentially reducing the average wait time of 35 minutes.    
2. Introduce an online check-in system to allow patients to register before arriving at the ER, reducing congestion and wait times upon arrival.    

* ### Improve Patient Satisfaction   

Targeted Satisfaction Improvements:
1. Analyze the 24% of patients who provided ratings to identify common issues and address them. This can help improve the overall satisfaction score from the current average of 5.   
2. Enhance patient communication by providing regular updates on wait times and treatment progress.    

* ### Streamline Referral Processes   

Optimize Referral System:
1. Implement an electronic referral system to ensure seamless communication and reduce delays between the ER and referral departments.   
2. Regularly review referral processes to identify bottlenecks and ensure patients are referred to the appropriate departments in a timely manner.    

* ### Address Demographic-Specific Needs    

Tailored Health Programs:
1. Develop specific health programs and services for different age groups, given that adults are the largest patient group but children and teenagers also constitute a significant portion.    
2. Offer culturally competent care and targeted health education to address the needs of diverse racial groups, as indicated by the satisfaction heatmap.    

* ### Leverage Technology    

Implement Digital Health Solutions:
1. Use telemedicine services for non-emergency consultations, which can reduce the number of unnecessary ER visits.   
2. Develop a mobile app for patient scheduling, check-ins, and accessing health information to improve the overall patient experience.    

* ### Continuous Improvement   

Regular Training and Development:
1. Provide continuous training for staff on best practices for patient care and customer service to improve patient interactions and satisfaction.    
2. Encourage staff to participate in quality improvement initiatives and provide feedback on ways to enhance ER operations.    

* ### Monitor and Evaluate Performance

Regular Data Analysis:    
1. Regularly review and analyze performance metrics such as wait times, patient satisfaction scores, and referral outcomes to identify areas for improvement.    
2.  Use predictive analytics to forecast patient volumes and adjust resources and staffing accordingly to ensure optimal patient care.    

By implementing these targeted suggestions, the Emergency Room can enhance its operational efficiency, improve patient satisfaction, and better manage its resources to provide high-quality care to its patients.

# CODE   

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







