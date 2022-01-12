# Vehicle_insurance_fraud_detection-data-Exploration
Vehicle_insurance_fraud_detection data exploration and analysis using SQL server management studio
The file was downloaded from kaggle https://www.kaggle.com/brcsnt/fraud-data-analysis-with-plotly for exploratory analysis using sql server.
/****** Script for SelectTopNRows command from SSMS  ******/
SELECT TOP (1000) [Month]
      ,[Make]
      ,[AccidentArea]
      ,[MonthClaimed]
      ,[Sex]
      ,[MaritalStatus]
      ,[Age]
      ,[Fault]
      ,[PolicyType]
      ,[VehiclePrice]
      ,[FraudFound_P]
      ,[PolicyNumber]
      ,[RepNumber]
      ,[Deductible]
      ,[DriverRating]
      ,[Days_Policy_Accident]
      ,[Days_Policy_Claim]
      ,[PastNumberOfClaims]
      ,[AgeOfVehicle]
      ,[AgeOfPolicyHolder]
      ,[PoliceReportFiled]
      ,[AddressChange_Claim]
      ,[Year]
      ,[BasePolicy]
  FROM [PortfolioProject1].[dbo].[fraud_vehicle]

--Drop table not required
Alter table fraud_vehicle
drop column [WeekOfMonth], [DayOfWeek], [DayOfWeekClaimed], [WeekOfMonthClaimed], [VehicleCategory], [WitnessPresent],[AgentType],
[NumberOfSuppliments], [NumberOfCars]

Select * 
from dbo.fraud_vehicle

--Counting no. of fraud found
Select count(FraudFound_P)
from dbo.fraud_vehicle
where FraudFound_P=1
group by FraudFound_P

Select count(*) as Fault_count ,Max(MonthClaimed) as max_month, Fault
from dbo.fraud_vehicle
group by Fault

Select count(*) as Count_Report,PoliceReportFiled
From dbo.fraud_vehicle
group by PoliceReportFiled

Select count(FraudFound_P), PoliceReportFiled
from dbo.fraud_vehicle
where FraudFound_P=1
and PoliceReportFiled='No'
group by PoliceReportFiled

Select count(FraudFound_P), PoliceReportFiled
from dbo.fraud_vehicle
where FraudFound_P=0
and PoliceReportFiled='Yes'
group by PoliceReportFiled

Select count(*) as Area_count, AccidentArea
From dbo.fraud_vehicle
group by AccidentArea

Select YEAR, count(*)
from dbo.fraud_vehicle
group by year

Select Month, count(*), Year
from dbo.fraud_vehicle
group by Month, YEAR
order by Year Asc

--No. of Frauds found in 3 years and report has been filed to police
select Year, count(FraudFound_P), PoliceReportFiled
from dbo.fraud_vehicle
where FraudFound_P=1
and PoliceReportFiled='Yes'
Group by Year, FraudFound_P, PoliceReportFiled

select Month , Year, count(FraudFound_P), PoliceReportFiled
from dbo.fraud_vehicle
where FraudFound_P=1
and PoliceReportFiled='Yes'
Group by Year, FraudFound_P, PoliceReportFiled, Month

--Total no. of frauds found in 3 years
select sum (FraudFound_P) as Total_FraudFound, Year
from dbo.fraud_vehicle
group by year

--Average no. of frauds reported in three years
select Avg(FraudFound_P) as avg_FraudFound_P, Year
from dbo.fraud_vehicle
group by year

