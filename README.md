# nosql-challenge

## Project Aim
This project focuses on using noSQL database through MongoDB. The raw data that is used to be studied is stored in JSON files.

## Project Description
This project is the work under a food magazine company. Data given in Json file contains information of food evaluation of various establishments across the United Kingdom. The ratings data provided would be analysed and used by food critics and journalists for their future work. 

This project would be divided into 3 parts:

Part 1: Set up and Part 2: Update would be in "NOSQL_setup.ipynb" file.

Part 3: Analysis would be in "NOSQL_analysis.ipynb"

## Project Method
### Part 1: Database and Jupyter Notebook Set Up in "NOSQL_setup.ipynb"
1. First is to open Visual Studio Code (VSC) page, direct to path where "establishment.json" file is stored
2. Import dataset by enter this code: mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json
3. Once imported, enter conda environement workspace, and open Jupyter notebook
4. Import dependencies from pandas. pymongo library and pprint for Json file
5. Create an instance of MongoClient with specific local port connection 
(Check MongoDB app installed in the local computer for port number)
6. Check if database from VSC is imported by run the code (.list_databse_names())
7. From database, check the available collections by run the code (.list_collection_names())
8. Assign a variable name for collection to be used for subsequent analysis
9. To review the content of a document, run the code: pprint(.find_one())

### Part 2: Update Database in "NOSQL_setup.ipynb"
1. Copy and Paste provided dictionary restaurant data for "Penang Flavours"
2. Insert data into collectin using the code (.insert_one()) and check if data inserted by run a query and (.find())
3. Using provided field "Business Type" to find the correspondent "BusinessTypeID" from other documents and insert into "Penang Flavours" document
4. This magazine company does not want documents from Dover Local Authority, hence all related documents need to get deleted using (.delete_many())
5. Changing data type for longitude and latitude to decimal using ($toDouble)
6. When re-run the code, insert data into document (this is the case for "Penang Flavours) might get duplicated, hence need to delete duplicated documents using the last code (.delete_many())
7. When re-run the code, deleted documents (this is "Dover") cannot be retrieved, hence database has to be deleted using (.drop_database()) and re-import database from PART 1 again. 
