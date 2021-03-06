# Project Description
In this project, we build an ETL pipeline using Python to load data into a Postgres database. Along the way, we define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

![alt text](https://udacity-reviews-uploads.s3.us-west-2.amazonaws.com/_attachments/38715/1600052919/Song_ERD.png)

## Song Dataset
The first dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.  
`song_data/A/B/C/TRABCEI128F424C983.json`  
`song_data/A/A/B/TRAABJL12903CDCF1A.json`  

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.  
`{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}`

## Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.  

`log_data/2018/11/2018-11-12-events.json`  
`log_data/2018/11/2018-11-13-events.json`  

## Project Files
the project workspace includes six files:

1. test.ipynb displays the first few rows of each table to let you check your database.
2. create_tables.py drops and creates your tables. You run this file to reset your tables before each time you run your ETL scripts.
3. etl.ipynb reads and processes a single file from song_data and log_data and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.
4. etl.py reads and processes files from song_data and log_data and loads them into your tables. You can fill this out based on your work in the ETL notebook.
5. sql_queries.py contains all your sql queries, and is imported into the last three files above.
6. README.md provides discussion on your project.

## Schema for Song Play Analysis
Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

### Fact Table
1. **songplays** - records in log data associated with song plays i.e. records with page `NextSong`  
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent  
### Dimension Tables
2. **users** - users in the app  
user_id, first_name, last_name, gender, level  
3. **songs** - songs in music database  
song_id, title, artist_id, year, duration  
4. **artists** - artists in music database  
artist_id, name, location, latitude, longitude  
5. **time** - timestamps of records in songplays broken down into specific units  
start_time, hour, day, week, month, year, weekday  

## How to Run
1. Run `python create_tables.py` to drop and create all the tables as empty tables with the define schema.
2. Run `python etl.py` to extract the data from the data files and load them into the tables created in step 1.
