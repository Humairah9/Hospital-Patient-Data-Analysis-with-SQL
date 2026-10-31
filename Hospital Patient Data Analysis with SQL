USE [TWDP Assignment]
--Import Patients data into SQL server nd ensures it loads successfully
SELECT*
FROM Patients

--1. Retrieve All Patients From Lagos 
SELECT *
FROM Patients 
WHERE [City] = 'Lagos'

--2. Find all patients with a lenght of stay greater than 5 days 
SELECT *
FROM Patients 
WHERE [Length_of_Stay]  > 5

--3. Find patients whose age is between 30 and 50 years
SELECT *
FROM Patients
WHERE Age 
BETWEEN 30 and 50 

--4. Retrieve all female patients from Lagos who where admitted through emergency admission
SELECT *
FROM Patients
WHERE City = 'Lagos' 
AND Gender = 'Female'
AND Admission_Type = 'Emergency'

--5. Retrieve all patients who have diabetes or hypertension 
SELECT *
FROM Patients
WHERE Condition = 'Diabetes' 
OR Condition = 'Hypertension'

--6. Find the 3 patients with the longest hospital stays, 
	--displaying them from longest to shortest stays
SELECT TOP 3 * 
FROM Patients 
ORDER BY Length_of_Stay DESC

--7. List all unique cities represented in the dataset 
SELECT DISTINCT City
FROM Patients
ORDER BY City

--8. Count the total number of patients 
SELECT COUNT (Patient_ID) 
AS Total_patient
FROM Patients;

--9. Calculate the average patient age 
SELECT 
   CAST(
        SUM(Age) * 1.0 / COUNT(*) 
        AS DECIMAL(10,1)
    ) AS Average_age
FROM Patients

--10. Count the number of patients for each medical condition
SELECT Condition, 
COUNT (Patient_ID)
	AS Cond_count
FROM Patients
GROUP BY Condition

--11. Display each patient's full name in uppercase 
SELECT Patient_Name,
UPPER(Patient_Name)
	AS PatientName
FROM Patients

--12. Display each patient's full name in lowercase 
SELECT Patient_Name,
LOWER(Patient_Name)
	AS PatientName
FROM Patients

--13. Create a new column that combines the the Patient_ID and Patient_Name into one value
SELECT
	Patient_ID,
	Patient_Name,
CONCAT(Patient_ID, ' ', Patient_Name) 
	AS Patient_Details
FROM Patients

--14. Find all patients who were admitted after January 15, 2026
SELECT 
	Patient_ID,
	Patient_Name,
	condition, 
	Admission_Type,
	Admission_Date
FROM Patients
WHERE Admission_Date > '2026-01-15'

--15. Display the year and month in which each patients was admitted
SELECT 
	Patient_ID,
	Patient_Name,
	condition, 
	Admission_Type,
	Admission_Date,
YEAR(Admission_Date) 
	AS Admission_Year,
DATENAME(Month, Admission_Date)
	AS Admission_Month
FROM Patients

--16. Calclate the average lenght of stay for each admission type
SELECT
    Admission_Type,
    CAST(
        SUM(Length_of_Stay) * 1.0 / COUNT(*) 
        AS DECIMAL(10,1)
    ) AS Avg_Length_Stay
FROM Patients
GROUP BY Admission_Type;

--17. Find the admission types with an average lenght of stay greater than 4 days 
SELECT
    Admission_Type,
    CAST(
        SUM(Length_of_Stay) * 1.0 / COUNT(*) 
        AS DECIMAL(10,1)
    ) AS Avg_Length_Stay
FROM Patients
GROUP BY Admission_Type
HAVING AVG(Length_of_Stay) > 4; 


--18. Classify patient as Young (under 40), Middle_age (40-59), or Senior (60 and above)
SELECT
	Patient_ID, 
	Patient_Name,
	Gender,
	Age,
CASE
	WHEN Age <40 THEN 'Young' 
	WHEN Age BETWEEN 40 AND 59 THEN 'Middle_age'
	Else 'Senior'
END AS Age_group
FROM Patients

--19. Count the number of patients in each age group
SELECT
   CASE
	 WHEN Age <40 THEN 'Young' 
	 WHEN Age BETWEEN 40 AND 59 THEN 'Middle_age'
	 Else 'Senior'
END AS Age_group,
COUNT(*) AS Patient_qty
FROM Patients
GROUP BY
CASE
	WHEN Age <40 THEN 'Young' 
	WHEN Age BETWEEN 40 AND 59 THEN 'Middle_age'
	Else 'Senior'
END

--20. Classify patients as Short stay (3 days or less) or Long stay (more than 3 days)
SELECT
	Patient_ID, 
	Patient_Name,
	Gender,
	Length_of_Stay,
  CASE
	 WHEN Length_of_Stay <=3 THEN 'Short stay' 
	 Else 'Long stay'
END AS Patient_stay
FROM Patients

--21. Find the medical conditions with more than 1 patient
SELECT
	Condition,
	COUNT(*) AS Patient_cond
FROM Patients
GROUP BY Condition
HAVING COUNT(*) > 1

--Import Doctors data into SQL server nd ensures it loads successfully
SELECT *
FROM Doctors

--22. Join the patients and doctors to displays the patients' name and their doctor's specialization
SELECT 
	Patients.Doctor_ID,
	Patients.Patient_Name,
	Doctors.Doctor_Name,
	Doctors.Specialization
FROM Patients
JOIN Doctors
ON Doctors.Doctor_ID = Patients.Doctor_ID

--23. Find all patients teated by doctors specializing in internal medicine
SELECT 
	Patients.Doctor_ID,
	Patients.Patient_Name,
	Doctors.Doctor_Name,
	Doctors.Specialization
FROM Patients
JOIN Doctors 
ON Doctors.Doctor_ID = Patients.Doctor_ID
WHERE Specialization = 'Internal Medicine'

--24. Calculate the average lenght of stay of patients treated by each doctors
SELECT
	Doctors.Doctor_Name,
     CAST(
        SUM(Patients.Length_of_Stay) * 1.0 / COUNT(*) 
        AS DECIMAL(10,1)
    ) AS Avg_Length_Stay
FROM Patients
JOIN Doctors 
ON Doctors.Doctor_ID = Patients.Doctor_ID
GROUP BY Doctor_Name


--25. Identify the doctor who has treated the highest number of patients
SELECT TOP 1
    Doctors.Doctor_Name,
    COUNT(Patients.Patient_ID) AS Patient_Count
FROM Patients
JOIN Doctors
    ON Doctors.Doctor_ID = Patients.Doctor_ID
GROUP BY Doctors.Doctor_Name
ORDER BY Patient_Count DESC;
