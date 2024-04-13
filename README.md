# Data Warehouse and Business Inteligence

## Overview
This project was an application implemented for the purpose of the course: **Information Systems - web applications** during my **MSc in Advanced Information Systems**.
The project aims to create a data warehouse (DW), specifically constructing cubes from large databases (DB) and performing detailed analysis of cube data (OLAP). Specifically, for the development of the Data Warehouse, a dataset containing information and data about Covid-19 from the website [source](https://www.ecdc.europa.eu/en/publications-data/data-national-14-day-notification-rate-covid-19) was used. We designed the DB for data entry into a relational Database. Then, we selected the data used for analytical processing and proceeded with the preprocessing process (cleaning, transformation) using Excel. Upon the selected data from the previous step, they were imported into the Database designed, with the data ready for entry into the Data Warehouse. Subsequently, a data warehouse - cube - was defined with appropriate dimensions, hierarchies, and measures. The DW follows the star schema model. Additionally, the queries we posed to the cube, the conclusions we reached, as well as visualized data of the responses we received from the cube for clearer conclusions, are presented. Finally, association rule extraction techniques were applied to the dataset, describing the results and the interesting measures used (support, confidence, lift, etc.) for rule selection.

### Source of Data:
The data source is a basic requirement for the establishment and creation of a Data Warehouse. For the development of the Data Warehouse, a dataset containing information and data about Covid-19 from the website [source](https://www.ecdc.europa.eu/en/publications-data/data-national-14-day-notification-rate-covid-19) was used. The dataset contains information about the percentage of positive cases and deaths on a daily basis, by country and continent. Additionally, the percentage is calculated per 100,000 population, 14-day period for reported cases per million population per day and country.

### 3. Design and Architecture of Data Warehouse
A data warehouse contains many database objects such as tables, views, stored procedures, functions, and so on. It is a decision support DB that is kept separate from an organization's/business's DB. It focuses on data modeling and analysis with the main goal of decision making over time.
The design of the data warehouse with appropriate design techniques supports multidimensional data analysis. Various measures and dimensions have been developed for its modeling, such as:
- Star Schema
- Snowflake Schema

For the development of the data warehouse, the SSDT tool was used. The covidAnalysis project was created and the DB created in the previous step was imported. For the construction of the cube, the dbo.country, dbo.covidDetails, dbo.date tables were selected through which the Fact table and the Dimensions were defined. The structure of the tables necessitated the selection of the Star schema for the architecture of the Data Warehouse and the cube structure.

#### Star Schema:
The Star Schema resembles a star in which the Fact Table acts as the axis as it is located at the center, while multiple dimensions are connected to the Fact table in a star-shaped manner with Foreign Keys. A simple Star Schema usually has one Fact Table and many dimensions, but complex star shapes can consist of more.

#### Fact table:
The Fact table consists of parameters, measures, and foreign keys. Measures consist of numerical values that can be counted or measured, while foreign keys constitute the connection with dimension tables. Measures can be used for query analysis. The Fact table is the covidDetails table.

#### Dimensions:
Dimension tables consist of descriptive values. Each dimension table has its own primary key. Dimension tables are dim.country, dim.date.
- dim.country: The Country dimension consists of the attributes geoId (Primary Key), CountriesAndTerritories, CountryTerritoryCode, popData2019, continent, etc. It consists of descriptive values about countries, their population, and the continent to which they belong.
- dim.date: The date dimension consists of the attributes dateRep (Primary Key), day, month, year. It consists of dates, days, months, and years.

#### Dimension Hierarchies:
Dimensions represent the parameters of the problem to be solved by the cube, describing the axes for modeling the questions of a problem. Therefore, it is necessary to create hierarchies in the dimensions as the levels of detail of the axes we set in the questions can easily be distinguished. Hierarchies were constructed in each dimension.

Hierarchy country: In the hierarchy of the country dimension, the continent (Continent Exp) was first placed and then the country (Country).

Hierarchy date: In the hierarchy of the date dimension, the years (Year) were placed first, then the months (Month), and finally the days (Day).

### 4. Detailed Analysis - OLAP:
The construction of the cube has now been completed. Next, multidimensional representation of the data needs to be performed using Analysis Services (SSAS), as well as visualization of the results for clearer presentation, using Excel. The structure of the cube was designed to serve the queries we want to pose on the dataset, which are informative and can be useful

### 5 Association Rules Extraction and Evaluation

To evaluate the association rules, we selected the Mining Model Viewer tab and then the Rules tab to display the association rules with the highest probability/confidence and importance. Data discretization was applied, and then 80% of the total data was selected for the training set, while 20% for the test set. As shown in Table 18, a table with three columns is displayed.

- **Probability column:** This column displays the confidence/probability level of the rule. All percentages shown are above 0.79, as the selected value of the MINIMUM_PROBABILITY parameter is 0.79.

- **Importance column:** This column displays the importance level of the association rule.

- **Rule column:** The rules produced by the algorithm are displayed here. Each rule consists of the left and right parts and has the following format:

   Set of variables that depend on the variables of the right member     Set of variables that depend on the variables of the left member.

So, the deaths of a country located on the right side of the rule depend on the deaths of the country or countries located on the left side.
