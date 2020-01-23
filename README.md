# Data Modeling with Postgres

## Purpose of Project
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis.

## Project Description
In this Project, fact and dimension tables will be designed for a star schema for this particular purpose. An ETL pipeline will also be designed to transfer data from files in two local directories into these tables in Postgres using Python and SQL.

## Source Data
Song data:

```
{"num_songs": 1, "artist_id": "ARD7TVE1187B99BFB1", "artist_latitude": null, "artist_longitude": null, "artist_location": "California - LA", "artist_name": "Casual", "song_id": "SOMZWCG12A8C13C480", "title": "I Didn't Mean To", "duration": 218.93179, "year": 0}
```

Log data:

```
{"artist":null,"auth":"Logged In","firstName":"Walter","gender":"M","itemInSession":0,"lastName":"Frye","length":null,"level":"free","location":"San Francisco-Oakland-Hayward, CA","method":"GET","page":"Home","registration":1540919166796.0,"sessionId":38,"song":null,"status":200,"ts":1541105830796,"userAgent":"\"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/36.0.1985.143 Safari\/537.36\"","userId":"39"}
```

## Database schema

This database uses the star schema: One Fact Table and Four Dimension Tables.

#### Fact Table
**songplays** 
- songplay_id (INT) PRIMARY KEY
- start_time (TIMESTAMP) NOT NULL
- user_id (VARCHAR) NOT NULL
- level (VARCHAR)
- song_id (VARCHAR) 
- artist_id (VARCHAR)
- session_id (INT)
- location (VARCHAR)
- user_agent (VARCHAR)

#### Dimension Tables
**users** 
- user_id (INT) NOT NULL PRIMARY KEY
- first_name (VARCHAR) NOT NULL
- last_name (VARCHAR) NOT NULL
- gender (VARCHAR)
- level (VARCHAR) NOT NULL

**songs** 
- song_id (VARCHAR) PRIMARY KEY
- title (VARCHAR) NOT NULL
- artist_id (VARCHAR) NOT NULL
- year (INT) NOT NULL
- duration (INT) NOT NULL

**artists** 
- artist_id (VARCHAR) PRIMARY KEY
- name (VARCHAR) NOT NULL
- location (VARCHAR)
- lattitude (FLOAT)
- longitude (FLOAT)

**time** 
- start_time (TIMESTAMP) NOT NULL PRIMARY KEY
- hour (INT) NOT NULL
- day (INT) NOT NULL
- week (INT) NOT NULL
- month (INT) NOT NULL
- year (INT) NOT NULL
- weekday (INT) NOT NULL

![ERD] (ERD.PNG)

## File Structure

- `sql_queries.py` - contains all the sql queries, and is imported into the following files
- `create_tables.py` - drops and creates tables in postgres database.
- `etl.ipynb` - reads and processes the single file from song_data and log_data and loads the data into the postgres database.
- `etl.py` - reads and processes all the files from song_data and log_data and loads the data into the postgres database.
- `test.ipynb` - displays the rows of each table to validate the data.

## ETL pipeline

- ETL.py will first connect to the sparkify datase. And it will drop and create all the tables.
- Json files will be parsed and get loaded into dataframe.
- Song_data and Log_data will be loaded into the fact and dimension tables.

Files will be excuted in the following orders:

1.create_tables.py
2.etl.py
3.test.ipynb
