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
     6. When re-run the code, insert data into document (this is the case for "Penang Flavours) might get duplicated, 
     hence need to delete duplicated documents using the last code (.delete_many())
     7. When re-run the code, deleted documents (this is "Dover") cannot be retrieved, 
     hence database has to be deleted using (.drop_database()) and re-import database from PART 1 again. 

### Part 1: Database and Jupyter Notebook Set Up in "NOSQL_analysis.ipynb"
     1. Import dependencies, and create variable for collection from database (same as Part 1)
     2. Exploring data by running through analysis using query, and find(). The output using pprint(), and count documents number using (.count_documents())
     3. The output is then converted to pandas Dataframe using pd.DataFrame(), and number of results using len() function. 
     4. Fist analysis: To find establishments that have a hygiene score equal to 20, using $eq
     5. Second analysis: To find establishments in London have a RatingValue greater than or equal to 4, using $regex, and $gte
     
     6.Third analysis: To find top 5 establishments with a rating value of '5', sorted by lowest hygiene score, nearest to the restaurant "Penang Flavours".
       - To locate nearby restaurants, need to define the geocoordinates of "Penang Flavours" by using query, and find()
       - Nearby restaurant search is within the given value degree_search =0.01, 
       add and subtract this to both latitude and longitude to get the area defined within the degree_search
       - Using $lte and $gte of the geocoordinates defined after degree_search to get a range of geocoordinates near 'Penang Flavours"
       - Input rating value and both geocoordinates into query, sort by Hygiene score (1 for ascending), 
       and limit results to 5, then pprint the output using for loop
      
     7. Fourth analysis: To create a pipeline aggregate with following conditions:
       - Matches establishments with a hygiene score of 0, using $match and $eq
       - Groups the matches by Local Authority, and count number of documents, 
       using $group, specified '-id' for the group field, and count documents using $sum
       - Sorts the matches from highest to lowest, this is to sort by count of documents using $sort and -1 value for descending order
       - create variable for the pipiline and input into (.aggregate()),, and print the output

### References
 - $toDecimal (aggregation).(2023). Retrieved on:21/05/2023, from:<MongoDB.https://www.mongodb.com/docs/manual/reference/operator/aggregation/toDecimal/>
 - How to use $gte and $lte between date with `$filter`.(14/05/2018). StackOverflow. Retrieved on:22/05/2023, from:<https://stackoverflow.com/questions/50331232/how-to-use-gte-and-lte-between-date-with-filter>
 - C# Convert.ToDouble loses decimal points when converting string to double.(15/1/2013).StackOverflow. Retrieved on:22/05/2023, from:<https://stackoverflow.com/questions/14343622/c-sharp-convert-todouble-loses-decimal-points-when-converting-string-to-double>
 -  Module 12: NoSQL Databases(15/5/2023). Monash University Data Analytics Bootcamp. Retrieved on: 22/5/2023
