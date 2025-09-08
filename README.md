Citi Bike ETL Project

This project demonstrates a complete ETL pipeline for Citi Bike trip data. Raw CSV files are cleaned, transformed, and loaded into a PostgreSQL database hosted on Supabase, with analytical views for reporting and analysis.

Key Features

Data Cleaning & Transformation: Handled duplicates, missing values, anomalous trip durations, and standardized column names. Converted data types and created derived columns like trip duration in minutes and hours.

Database Design: Designed a relational schema with stations, users, gender, dim_date, and trip_informations tables. Implemented proper primary and foreign keys to maintain referential integrity.

Analytical Views: SQL views were created to support reporting and analytics:

bike_usage – Bike-level usage statistics

user_trip_stats – User behavior by type and gender

station_usage – Trips started and ended per station

trip_summary – Detailed trip-level data

daily_trip_summary – Summarized daily metrics

ETL Automation: Python scripts with pandas and psycopg2 automate data cleaning, transformation, and bulk insertion into the database.

Automated Deployment with GitHub Actions: A GitHub Actions workflow ensures that the ETL pipeline runs automatically on push to the main branch, keeping the Supabase database up-to-date.

Skills Demonstrated

Python & pandas for data transformation

SQL & PostgreSQL for database modeling and querying

Data cleaning and ETL pipeline development

Analytical reporting with SQL views

Workflow automation with GitHub Actions