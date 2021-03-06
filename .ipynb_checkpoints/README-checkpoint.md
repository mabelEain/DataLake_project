# PROJECT: Data Lake

## Quick start

First, dl.cfg and fill in the open fields. Fill in AWS acces key (KEY) and secret (SECRET).

Example data is in data folder. To run the script to use that data, do the wfollowing:

* Create an AWS S3 bucket.
* Edit dl.cfg: add your S3 bucket name.
* Copy **log_data** and **song_data** folders to your own S3 bucket.
* Create **output_data** folder in your S3 bucket.
* NOTE: You can also run script locally and use local input files. Also run before SparkSession import findspark and findspark.init()
* run on terminal `python3 etl.py` 


## ETL Pipeline
    
1.  Read data from S3
    
    -   Song data:  `s3://udacity-dend/song_data`
    -   Log data:  `s3://udacity-dend/log_data`
    
    The script reads song_data and load_data from S3.
    
3.  Process data using spark
    
    Transforms them to create five different tables listed below : 
    #### Fact Table
    **songplays**  - records in log data associated with song plays i.e. records with page  `NextSong`
    -   _songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent_

    #### Dimension Tables
    **users**  - users in the app
    Fields -   _user_id, first_name, last_name, gender, level_

    **songs**  - songs in music database
    Fields - _song_id, title, artist_id, year, duration_
    
    **artists**  - artists in music database
    Fields -   _artist_id, name, location, lattitude, longitude_
    
    **time**  - timestamps of records in  **songplays**  broken down into specific units
    Fields -   _start_time, hour, day, week, month, year, weekday_
    
4.  Load it back to S3
    
    Writes them to partitioned parquet files in table directories on S3.
