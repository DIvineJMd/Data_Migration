# University Database Migration Project

This project involves migrating a university database from a relational model (PostgreSQL) to a non-relational model (MongoDB) while ensuring efficient data transformation, optimization, and analysis.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Data Migration Process](#data-migration-process)
  - [1. Extract](#1-extract)
  - [2. Transform](#2-transform)
  - [3. Load](#3-load)
- [MongoDB Schema Design](#mongodb-schema-design)
- [Queries in MongoDB](#queries-in-mongodb)
- [Optimization Strategies](#optimization-strategies)
- [Performance Analysis](#performance-analysis)
- [Observations](#observations)
- [How to Run](#how-to-run)
- [Future Improvements](#future-improvements)

---

## Project Overview

The primary goal of this project was to migrate and optimize a university database for performance. Data from the PostgreSQL database was transformed into a document-based schema in MongoDB. The project focuses on optimizing for read-heavy workloads, improving performance, and conducting meaningful analytics.

---

## Technologies Used
- **PostgreSQL**: Source relational database.
- **MongoDB**: Target non-relational database.
- **Python**: For data extraction, transformation, and loading.
- **Apache Spark**: For large-scale query processing and performance optimization.
- **PyMongo**: MongoDB integration with Python.

---

## Data Migration Process

### 1. Extract
- Connected to PostgreSQL and retrieved data from the following tables:
  - Departments
  - Students
  - Instructors
  - Courses
  - Enrollments
- SQL queries were used to fetch data into Python for processing.

### 2. Transform
- Data transformations were performed to align with the MongoDB schema:
  - **Departments**: Minimal changes, mainly field renaming.
  - **Students**: Embedded enrollments within each student document.
  - **Instructors**: Embedded courses within each instructor document.
  - **Courses**: Embedded enrollments within each course document.
- Ensured proper data types, especially for dates.
- Applied custom transformation functions for data restructuring.

### 3. Load
- Established a connection to MongoDB and inserted the transformed data.
- Used `replace_one` with `upsert=True` for seamless inserts and updates.
- Ensured compatibility for date objects by converting them to MongoDB's `datetime` format.

---

## MongoDB Schema Design

The schema was restructured for read-heavy workloads:

- **Students Collection**:  
  Embedded enrollment details for efficient querying.  

- **Instructors Collection**:  
  Embedded courses taught by instructors for quick lookups.  

- **Courses Collection**:  
  Embedded student enrollment details for seamless course analysis.  

- **Departments Collection**:  
  Maintained as a static collection for department metadata.  

---
## Performance Analysis
# Query Description	Before Optimization (s)	After Optimization (s)
Fetch students enrolled in courseId=1	5.2	3.1
Calculate average enrollment per instructor	4.8	3.0
List courses by department	5.5	3.4
Total students per department	6.1	3.7
Instructors teaching core CSE courses	5.9	3.8
Top 10 courses by enrollment count	6.4	3.5
## Observations
- **Enrollment Trends** : Courses like Introduction to Programming had the highest enrollments.
- **Instructor Engagement** : Some instructors showed limited course participation, prompting deeper investigation.
- **Department Insights** : Computer Science had the highest student enrollment, reflecting its popularity.

##Future Improvements
Automate updates for embedded data to avoid redundancy.
Explore horizontal scaling of MongoDB for larger datasets.
Integrate real-time analytics for dynamic course engagement tracking.
