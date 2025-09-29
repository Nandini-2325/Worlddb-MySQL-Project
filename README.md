# Worlddb-MySQL-Project

## 📌 1. Project Overview
This project involves designing and populating a **relational database** that models global information such as **countries, cities, continents, and languages**.  
It serves as a foundation for developing **SQL querying skills**, analyzing real-world data, and simulating international reporting systems.

The database was built using **MySQL Workbench** for data modeling and **MySQL** for schema creation and data management.

---

## 🛠 2. Tools Used
| Tool                 | Purpose                                      |
|---------------------|----------------------------------------------|
| MySQL Workbench      | ER modeling and schema design (.mwb file)    |
| MySQL                | Query execution and database interaction     |
| SQL                  | Writing and testing relational queries       |
| Excel / CSV (optional)| Importing or exporting sample data           |

---

## 🌐 3. Dataset Overview
The World database includes structured data on:  

- 🌎 **Countries** – name, population, region, surface area, etc.  
- 🏙️ **Cities** – cities linked to countries with population and location  
- 🗺️ **Continents** – global continent reference  
- 🗣️ **Languages** – languages spoken in each country and whether they are official  
- 💹 **Economy** – GDP and economic indicators (optional expansion)  

This dataset simulates a **geopolitical and socio-economic model** used in global data analysis scenarios.

---

## 🧱 4. Schema Overview
The schema includes the following **normalized tables**:

| Table       | Description                                                |
|------------|------------------------------------------------------------|
| **continent** | List of continents (e.g., Europe, Asia)                 |
| **country**   | Information about countries including population, area, continent reference |
| **city**      | Cities with foreign key link to country                  |
| **language**  | Languages spoken in countries, indicating if official   |
| **gdp_data** (optional) | Economic indicators like GDP, inflation           |

### 🔗 Relationships
- `country.continent_id → continent.continent_id`  
- `city.country_id → country.country_id`  
- `language.country_id → country.country_id`  

🖼️ <img width="955" height="532" alt="image" src="https://github.com/user-attachments/assets/617b5c75-c2ac-4423-8a68-026ffb2e1f08" />


---

## 📚 5. Key Learnings
- 🔧 Modeled **real-world entities** in a normalized relational schema.  
- 📊 Practiced **JOINs, aggregations, and filtering** across multiple tables.  
- 🧩 Applied **foreign keys** to maintain referential integrity.  
- 📥 Gained experience with **data modeling tools** (MySQL Workbench .mwb).  
- 🧠 Simulated a practical dataset useful for **analysis, reporting, and dashboard projects**.  

---

## 🧪 6. Sample SQL Queries

## 🧪 Sample SQL Queries – World Database

```sql
-- Count Cities in USA
SELECT COUNT(DISTINCT Name) AS CityName
FROM City
WHERE countrycode = 'USA';

-- Country with Highest Life Expectancy
SELECT Name, LifeExpectancy
FROM country
ORDER BY LifeExpectancy DESC
LIMIT 1;

-- Cities with 'New' in Name
SELECT Name
FROM city
WHERE Name LIKE '%New%';

-- Display First 10 Cities by Population
SELECT *
FROM city
ORDER BY population DESC
LIMIT 10;

-- Cities with Population Larger than 2,000,000
SELECT Name, Population
FROM city
WHERE Population > 2000000;

-- Cities Beginning with 'Be'
SELECT Name
FROM city
WHERE Name LIKE 'Be%';

-- Cities with Population Between 500,000 and 1,000,000
SELECT Name, Population
FROM city
WHERE Population BETWEEN 500000 AND 1000000;

-- Display Cities Sorted by Name
SELECT Name
FROM city
ORDER BY Name;

-- Most Populated City
SELECT Name, Population
FROM city
ORDER BY Population DESC
LIMIT 1;

-- City Name Frequency Analysis
SELECT DISTINCT Name, COUNT(Name)
FROM city
GROUP BY Name
ORDER BY COUNT(Name) DESC;

-- City with Lowest Population
SELECT Name, Population
FROM city
ORDER BY Population
LIMIT 1;

-- Country with Largest Population
SELECT Name, Population
FROM country
ORDER BY Population DESC
LIMIT 1;

-- Capital of Spain
SELECT co.Name, ci.Name, ci.District
FROM city AS ci
JOIN country AS co
ON co.code = ci.CountryCode
WHERE co.Name = 'Spain';

-- Cities in Europe
SELECT ci.Name, co.Continent
FROM city AS ci
JOIN country AS co
ON co.code = ci.CountryCode
WHERE co.Continent = 'Europe';

-- Average Population by Country
SELECT Name, AVG(Population) AS avg_population
FROM country
GROUP BY Name
ORDER BY avg_population DESC;

-- Capital Cities Population Comparison
SELECT ci.Name, co.Name, ci.Population AS population
FROM country AS co
JOIN city AS ci
ON co.Capital = ci.ID
ORDER BY ci.Population DESC;

-- Countries with Low Population Density
SELECT country.Name, (country.Population / country.SurfaceArea) AS Population_density
FROM country
ORDER BY Population_density;

-- Cities with High GDP per Capita
SELECT co.Name, ci.Name, co.Population, co.GNP, (co.GNP / co.Population) AS GDP_per_capita
FROM city AS ci
JOIN country AS co
ON co.code = ci.CountryCode
ORDER BY GDP_per_capita DESC;

-- Display Rows 31-40 by Population
SELECT *
FROM city
ORDER BY Population DESC
LIMIT 10 OFFSET 30;
