Citi Bike Data ETL and Analysis Project – Development Process

For this project, I worked on cleaning, transforming, and structuring Citi Bike trip data into a relational database for analysis. My goal was to take raw CSV files, ensure the data was accurate and consistent, and make it easily accessible for reporting and analytics. Below is an overview of my process, technical decisions, and enhancements.

1. Data Cleaning and Transformation

The raw data required several cleaning steps to ensure accuracy and usability:

Combining multiple CSVs: I used pandas and glob to read and concatenate all trip data files into a single DataFrame for efficient processing.

Standardizing column names: Replaced spaces with underscores and converted all names to lowercase for consistency and to prevent SQL issues later.

Correcting data types: Converted numeric columns to Int64, categorical fields to category, and datetime fields (start_time and stop_time) using pd.to_datetime. This improved memory usage and ensured proper handling in SQL.

Removing duplicates and assigning IDs: Dropped duplicate rows and added unique IDs for trips and users to simplify relational joins.

Filtering anomalous data: Removed trips shorter than 60 seconds and trips with unrealistic birth years (<1936), while retaining extremely long trips, as these could represent long-term users.

Handling missing values:

Missing user_type was inferred based on gender and birth_year, assigning "Customer" or "Subscriber" logically.

Remaining missing birth_year values were filled with the average to maintain data completeness.

These decisions ensured the dataset was clean, reliable, and suitable for analysis while retaining as much meaningful data as possible.

2. Relational Database Design

I designed the database schema with normalization and analytical needs in mind:

stations: Contains all start and end stations with IDs, names, and coordinates.

users: Stores unique users with user type, gender, and birth year.

gender: A small lookup table for gender mapping to keep the users table normalized.

dim_date: A date dimension table, generated programmatically, storing year, month, day, quarter, and names of days and months. This standardizes date attributes for aggregation.

trip_informations: The central fact table linking trips to users, stations, and dates.

This schema supports efficient joins, avoids redundancy, and mirrors a typical star schema used in data warehousing.

3. Views and Analytical Insights

To facilitate analysis and reporting, I created several SQL views:

bike_usage: Aggregates total trips, average trip duration, and total duration per bike. Useful for identifying the most popular bikes and usage patterns.

user_trip_stats: Summarizes trips by user, including user type and gender. Analysts can study usage patterns, identify heavy users, or segment by demographics.

station_usage: Counts trips starting and ending at each station. Supports capacity planning and identifying under- or over-utilized stations.

trip_summary: Provides a detailed trip-level view, combining trip, user, and station information. Useful for exploratory analysis or complex queries.

daily_trip_summary: Aggregates trips by day, with totals, averages, and unique users. Supports trend analysis over time.

These views provide pre-aggregated and easily queryable data, making the dataset much more accessible to analysts without having to write complex joins repeatedly.

4. Automation and Deployment

To enhance workflow efficiency and ensure that the database remains up-to-date:

ETL Automation: Python scripts with pandas and psycopg2 automate data cleaning, transformation, and bulk insertion into PostgreSQL.

Supabase Integration: The relational database is hosted on Supabase, providing a managed, cloud-hosted PostgreSQL environment.

GitHub/GitLab Actions: I implemented a CI/CD workflow that automatically runs the ETL pipeline whenever new data is pushed to the repository. This ensures that Supabase is continuously updated with the latest trip data without manual intervention.

This automation not only saves time but also demonstrates modern DevOps and data engineering practices.

5. Technical Skills and Decisions Highlighted

Efficient use of pandas for ETL tasks, including concatenation, type conversion, and handling missing data.

Data quality checks and logical handling of anomalies and missing values.

Relational database design with normalization and fact/dimension modeling for analytics.

Bulk insertion into PostgreSQL using psycopg2 and execute_values for efficiency.

Creation of SQL views to provide clean, aggregated, and user-friendly representations of the data.

CI/CD workflow using GitHub/GitLab Actions to automate deployment to Supabase.

Conclusion

This project demonstrates my ability to take messy, real-world data, clean and structure it, and build a relational schema optimized for analysis. By integrating automated deployment with Supabase, the database and views are always up-to-date, enabling efficient querying, analytics, and reporting.

The project showcases my expertise in Python ETL pipelines, SQL data modeling, relational database design, and modern deployment workflows, making it a strong portfolio example for data engineering and analytics roles.