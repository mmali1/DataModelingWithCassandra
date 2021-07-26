Introduction:
    A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.
    
Purpose:
    Purpose of this project is to model the data based on queries needed to run in Apache Cassandra and create an ETL pipeline in Python. 
    
Dataset:
    Data resides in event_data directory in the form of csv files. This directory is partitioned by date. 
    Example:
        event_data/2018-11-08-events.csv
        event_data/2018-11-09-events.csv
        
Scripts:
    1. Project_1B_ Project_Template.ipynb
        This jupyter notebook has two components. First is ETL pipeline for preprocessing the files. After running this section of the notebook we get event_datafile_new.csv file. This file contains denormalized data from event_data directory. It has following columns,
        - artist 
        - firstName of user
        - gender of user
        - item number in session
        - last name of user
        - length of the song
        - level (paid or free song)
        - location of the user
        - sessionId
        - song title
        - userId 
        Second component of this notebook is to create Apache Cassandra tables. 
        Based on the queries given, we will need three tables.
        
        1.  Give me the artist, song title and song's length in the music app history that was heard during  sessionId = 338, and itemInSession  = 4
        Table: 
            session_history  
            primary key: sessionid,iteminsession
        columns:
            - sessionid int, 
            - iteminsession int, 
            - artist text, 
            - song_title text, 
            - length float
                
         2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
        Table:
            user_history_by_session
            primary key: userid, sessionid, 
            clustering column: iteminsession
            Since we need to sort by iteminsession we will include iteminsession as clustering column in this key
        Columns:
           - userid int, 
           - first_name text, 
           - last_name text, 
           - sessionid int,
           - iteminsession int, 
           - artist text, 
           - song text 
           
          3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'
        Table:
            song_history
            primary key : song, first_name, last_name, userid
            columns:
            - userid int, 
            - first_name text, 
            - last_name text, 
            - song text
            
 How to run:
     Run each portion of Project_1B_ Project_Template.ipynb 