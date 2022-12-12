# My-Google-Capestone-Project
Bellabeat Fitness Analysis Project
THIS IS MY CAPESTONE PROJECT DONE AFTER COMPLETING GOOGLE DATA ANALYTICS CERTIFICATION PROGRAM 

-- I used Google sheets for cleaning my data files, Google Bigquery for analysing it and Tableau for visualization.
-- I used three csv files: sleepDay_merged and DailyActivity_merged (which contained Total Steps, Distance, Calories and Amount of Activity)
-- Google Sheets was used for removing duplicates, filtering and sorting the data.


-- I did some data analysis in Google Bigquery after uploading the cleaned datasets to the console. 

-- Firstly I added a new column named "Dayname" in both sleepDay_merged and DailyActivity_merged using Spreadsheet TEXT function.


--I found number of participants in the Dailyactivity table by running a simple SQL query. The result was 33 users(its a very small sample)

SELECT 
COUNT(DISTINCT(Id)) 
FROM `nimishaprojects.Google_Capestone1.Dailyactivity_cleaned`

-- Then I run the same query with sleepDay_merged file which returned 24 users

SELECT 
 COUNT(DISTINCT(Id)) 
  FROM `nimishaprojects.Google_Capestone1.Seepdayupdated` 
  
  -- For finding Actvity level percentage of participants
  
  SELECT 
 
 SUM(VeryActiveMinutes)/ SUM(VeryActiveMinutes+FairlyActiveMinutes+LightlyActiveMinutes+SedentaryMinutes) *100 AS VeryActiveperc,
  SUM(FairlyActiveMinutes)/ SUM(VeryActiveMinutes+FairlyActiveMinutes+LightlyActiveMinutes+SedentaryMinutes) *100 AS FairyActiveperc,
  SUM(LightlyActiveMinutes)/ SUM(VeryActiveMinutes+FairlyActiveMinutes+LightlyActiveMinutes+SedentaryMinutes) *100 AS LightlyActiveperc,
SUM(SedentaryMinutes)/ SUM(VeryActiveMinutes+FairlyActiveMinutes+LightlyActiveMinutes+SedentaryMinutes) *100 AS Sedentaryperc,
 FROM `nimishaprojects.Google_Capestone1.Dailyactivity_cleaned` 
 
 -- Finding the most active day in a week
 
 SELECT
 AVG(VeryActiveMinutes) AS VeryActiveMinutes, 
 AVG(FairlyActiveMinutes) AS FairlyActiveMinutes, 
 AVG(LightlyActiveMinutes) AS LightActiveMinutes, 
 AVG(SedentaryMinutes) AS SedentaryMinutes,  DayName
  FROM  `nimishaprojects.Google_Capestone1.Dailyactivity_cleaned`
WHERE  (VeryActiveMinutes+FairlyActiveMinutes+LightlyActiveMinutes+SedentaryMinutes) <> 0
GROUP BY DayName
 
 
 -- Average number of Steps per week day

SELECT  
AVG(TotalSteps) as total_steps,
AVG(TotalDistance) as total_dist,
AVG(Calories) as total_calories,DayName
FROM `nimishaprojects.Google_Capestone1.Dailyactivity_cleaned`
Group By  DayName




-- Relation Between Steps and Calories Burned:

SELECT Id, AVG(TotalSteps) AS Total_Steps, AVG(Calories) AS Total_Calories
FROM  `nimishaprojects.Google_Capestone1.Dailyactivity_cleaned`
  GROUP BY Id

-- Sleeping time per day of week

SELECT AVG(TotalMinutesAsleep) , DayName
FROM `nimishaprojects.Google_Capestone1.Seepdayupdated` 
group by DayName




