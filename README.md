Name- Riya Khandelwal
Roll number- 2337049

This assignment uses an inbuilt data set available on Big Query Public Data.
Dataset- fdic_banks: bigquery-public-data.fdic_banks
Tables- Institutions: bigquery-public-data.fdic_banks.institutions
        Locations:  bigquery-public-data.fdic_banks.locations

1. Find the total number of active and inactive institutions.

SELECT active, COUNT(*) AS institution_count
FROM `bigquery-public-data.fdic_banks.institutions`
GROUP BY active;

2. List the top 10 states with the most bank branches.

SELECT state, COUNT(*) AS branch_count
FROM `bigquery-public-data.fdic_banks.locations`
GROUP BY state
ORDER BY branch_count DESC
LIMIT 10;

3. Identify institutions with a total asset value exceeding $100 billion.

SELECT fdic_certificate_number, institution_name, total_assets
FROM `bigquery-public-data.fdic_banks.institution`
WHERE total_assets > 100000000000;

4. Compare the average total assets of national and state-chartered banks.

SELECT bank_charter_class, AVG(total_assets) AS avg_total_assets
FROM `bigquery-public-data.fdic_banks.institution`
GROUP BY bank_charter_class;

5. Find institutions that have undergone at least three structural changes based on change codes.

SELECT fdic_certificate_number, institution_name
FROM `bigquery-public-data.fdic_banks.institution`
WHERE (change_code_1 IS NOT NULL AND change_code_1 != "")
  AND (change_code_2 IS NOT NULL AND change_code_2 != "")
  AND (change_code_3 IS NOT NULL AND change_code_3 != "");

6. List the types of FDIC-insured institutions and the number of branches each type has.

SELECT service_type, COUNT(*) AS branch_count
FROM `bigquery-public-data.fdic_banks.locations`
GROUP BY service_type;

7.  Find the oldest and newest bank branches based on their establishment dates.

SELECT MIN(date_established) AS oldest_date, MAX(date_established) AS newest_date
FROM `bigquery-public-data.fdic_banks.locations`;

8. Compare the distribution of total assets for commercial and savings institutions.

SELECT institution_class, SUM(total_assets) AS total_assets
FROM `bigquery-public-data.fdic_banks.institution`
GROUP BY institution_class;

9. Which states have the highest concentration of branches operated by institutions with over $10,000 in assets?

SELECT l.state, COUNT(*) AS branch_count
FROM `bigquery-public-data.fdic_banks.locations` AS l
INNER JOIN `bigquery-public-data.fdic_banks.institution` AS i
ON l.fdic_certificate_number = i.fdic_certificate_number
WHERE i.total_assets > 10000
GROUP BY l.state
ORDER BY branch_count DESC;

10. Which types of FDIC-insured institutions have the highest average number of branches per state they operate in?

SELECT i.institution_name, COUNT(l.state) AS avg_branches_per_state
FROM `bigquery-public-data.fdic_banks.locations` AS l
INNER JOIN `bigquery-public-data.fdic_banks.institutions` AS i
ON l.fdic_certificate_number = i.fdic_certificate_number
GROUP BY i.institution_name
ORDER BY avg_branches_per_state DESC;

The results of all these 10 SQL queries have been uploaded in this google link.

https://drive.google.com/drive/folders/1OBsgNbaYPUujvErxHtbsdVTs1QT-x8ks?usp=sharing


