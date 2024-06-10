# Extracting-Tables-with-MySQL-Excel
This is a database information from Openemr. 
Here, I want to extract only the table_names and the fields in each table(i.e  column_names). 
Here is the link: https://raw.githubusercontent.com/openemr/openemr/master/sql/database.sql 

# Step by Step Approach
Step 1: Download MySQl workbench if you don't have it yet on your system.
Step 2: Click on the link dataset link and copy the sql code to Notepad. 
Step 3: Save the notepad as db_openemr.sql
Step 4: Open MySQL workbench and connect to database.
Step 5: Open the existing file (db_openemr)
Step 6: Add the code below to the top to create the database
          DROP DATABASE IF EXISTS OPENEMR;
          CREATE DATABASE OPENEMR;
          USE OPENEMR;
Step 7: Run the code
Note: The database will be created and all the tables and fileds will be inputed the their data. However, it will develop an error at the end of the action output. This is because server SQL Mode is on 'NO_ZERO_DATE'. You can change that depending on the workbench you are using. Nevertherless, you can continue and later extract the table name and fields with excel. Now, we will continue and use excel to recover the table name that was nt created
Step 8: Open a new SQL tab and write the code below
          SELECT table_name, GROUP_CONCAT(column_name ORDER BY ordinal_position)
          FROM information_schema.columns
          WHERE table_schema = 'openemr'
          GROUP BY table_name
          ORDER BY table_name
Note: This will generate all the table names and corresponding fields. Click Export to export it a CSV format.
Step 9: Open Microsoft Excel and import the CSV file to load the data. Rename the Header
Step 10: Open a new sheet
Step 11: Return to the link of the original dataset above. Press Ctrl + F (to find the name of the table which was not created in the database 'openemr_postcalendar_events')
Step 12: Copy everthing from `pc_eid` down to `uuid` and paste it to the create excel sheet.
Step 13: On a new cell, add the code below to get only the fields in the table 'openemr_postcalendar_events'
            =MID(A1, SEARCH("`",A1) + 1, SEARCH("`",A1,SEARCH("`",A1)+1) - SEARCH("`",A1) - 1)
Step 14: Copy the result and edit it somewhere to have it in the same line just like the database provided.
Step 15: Insert the table name and paste the result of the fields for the table to macth the format of other tables.
            
