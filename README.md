# Module 12 - nosql-challenge - READMe

## Eat Safe, Love

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine,  *Eat Safe, Love* , to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

**Requirements:**

* PyMongo
* PPrint
* Pandas

## NoSQL Setup Starter Notebook (1 of 2 Notebooks)

### Part 1: Database and Jupyter Notebook Set Up

Import the data provided in the `establishments.json` file from your Terminal. Name the database `uk_food` and the collection `establishments`.

Import the dataset with "mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json"

This notebook will create an instance of the Mongo Clinet, confirm the database is created and loaded properly and assigns the establishments collection to a variable (establishments).

### Part 2: Update the Database

The notebook continues on to update the database with an exciting new halal restaurant in Greenwich called Penang Flavours. 

The BusinessType "Restaurant/Cafe/Canteen" ID is located and then Penang Flavours BusinessTypeID is updated with this using update_one().

The establlishments in Dover are then removed using delete_many() and the notebook checks to ensure they were deleted while keeping other values using count_documents().

Finally, the latitude and longitudes for the establishments is converted from strings to decimal numbers using update_many() along with 'set' and 'toDouble'.

## NoSQL Setup Analysis Notebook (2 of 2 Notebooks)

### Part 3: Exploratory Analysis

This notebook answers four questions by searching the 'establishments' collection in the 'uk_food' database. 

1. Which establishments have a hygiene score equal to 20?
   This is answered by using count_documents(), finding the first document with find_one()), and displaying this using pprint. The results are converted to a Pandas DF, the number of rows is printed and then the first 10 rows are displayed.
2. Which establishments in London have a RatingValue greater than or equal to 4?
   This is answered by using regex to match documents with "London" in the LocalAuthorityName field and then using $in to match documents with a RatingValue of 4 or 5. Count_documents()) is then used to find the number of matching documents and find_one() is used to find the first document. The results are converted to a Pandas DF, the number of rows is printed and then the first 10 rows are displayed.
3. What are the top 5 establishments with a RatingValue of '5', sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
   This is answered by using aggregate() with a pipeline to match the documents within 0.01 degree of Penang Flavours latitude and longitude, a RatingValue of 5, sorted by hygiene scores, and limited to 5 results. The results are then pprinted and stored, which is then convereted to a Pandas DF and the results are displayed.
4. How many establishments in each Local Authority area have a hygiene score of 0?
   This is answered by using aggregate() with a pipeline that matches a hygiene score of 0, grouped by LocalAuthorityName, and sorted from the highest to lowest which is then pprinted. The results are converted to a Pandas DF, the number of rows is printed and then the first 10 rows are displayed.
