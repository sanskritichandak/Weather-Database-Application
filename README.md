# Weather-Database-Application

**MiniWorld Description: Weather Database** 

Consider a weather database in which information about

*   The weather event types are identified by a unique event number, description of the type of weather event, and its severity
*   The fs.files are identified by their filename(consists of images relevent to each type of weather event), and respective weatherID
*   The locations are identified by a unique location number, the name of the city, county, state, and zipcode
*   The airport-based weather stations record the weather reports which are identified by their unique airport number, aiport code, time zone the weather station is located in, and the location it reports weather for
*  The daily weather reports are created when the airport-based weather stations record the weather report which is identified by a unique report number, date of the report, weatherID, type of weather, serverity of the weather, location number, airport number, and the precipiation that was recorded

**Description of entities and attributes** 

The baseline conceptual model should contain the following <entity;attributes>;

1. <WeatherEvents; WeatherID (PK), Weather_Type, Severity>
2. <WeatherLocations; Location ID (PK), City, County, State, ZipCode>
3. <Airports; AirportID (PK), AirportCode, TimeZone, LocationID (FK)>
4. <DailyWeather; DailyWeatherID (PK), Date, WeatherID (FK), WeatherType (FK), Severity (FK), LocationID (FK), AirportID (FK), Precipitation>
5. <fs.files; filename (PK), WeatherID (FK)>

**Description and correct mapping of all relationships**

The minimum conceptual model should have the following relationships and cardinalities

1. Each weather location has one and only one (1, 1) airport-based weather station 
2. Each airport-based weather station has one and only one (1, 1) weather location
3. Each daily weather report can have one and only one (1, 1) weather ID
4. Each weather ID can have zero or many (0, N) daily weather reports 
5. Each daily weather report can have one and only one (1, 1) weather type 
6. Each weather type can have zero or many (0, N) daily weather reports
7. Each daily weather report can have one and only one (1, 1) severity level 
8. Each severity level can have zero or many (0, N) daily weather reports 
9. Each daily weather report can have one and only one (1, 1) airport ID
10. Each airport ID can have zero or many (0, N) daily weather reports 
11. Each file can one only and only one (1, 1) weather ID 
12. Each weather ID can have one and only one (1, 1) file

**Description and correct mapping of constraints related to business rules**

The state of the weather database corresponds to the statuses of all its relations in a particular point in time 

The constraints are derived from the rules in the miniworld that the database represents 

Examples of constraints related to business rules 

1. The weather database is a NoSQL document-based databse: data is stored in the form of documents, described in JSON and accessed by their document ID or other indexes 

2. The CAP theorum is applicable to the Weather database. The CAP theory consists of three desirable properties of distributed systems with replicated data of which two are application to NoSQL databases:

*   availability of the system to read and write operations: the documents from this databse can be used to create views, triggers, and indexes and run general queries, filter for documents, aggregate data from documents, update and delete data from documents 
*   partition tolerance: the data can be partitioned and used in accordance with the constraints of the database

3. The document stores resemble complex or XML documents and are self-describing. The documents have different data elements (attributes) even if they belong to the same colelction. New documents can have data elements that do not exist in any current document in the collection. 

4. MongoDB documents are stored in BSON (binary JSON) format, which is a variation of JSON with additional data types and is more efficient for storage than JSON

5. All write operations are replicated on the primary copy and all read operations are replicated by any copy

**Choice of database application and library**

MongoDB is a document database used to build highly available and scalable internet applications. MongoDB accomodates large amounts of data and is an open source NoSQL database. MongoDB is compatible with the large amounts of data that the Weather dataset has. Furthermore, it is able to process structured, semi-structured, and unstructured data from the Weather data set as it uses a non-relational document-oriented data model and a non-structured query language. It allows the user to combine and store multiple types of data which is applicable to the Weather data set since it consists of various types of data such as strings, integers, dates, etc. Furthermore, MongoDB allows the user to connect their application through a driver or Atlas Data API in any programming language including Python. It allows you to access the data through MongoDB's GUI or Javascript interface and is compatible with various operating softwares.

Google Collab allows the user to write and execute arbitray python code through the browser. In addition, Google is cloud-based which allows it to be connected to MongoDB.

PyMongo is a Python distribution containing tool for working with MongoDB. It is the official MongoDB driver for synchronous Python applications. It servers as the connector between Google Colab and MongoDB. Using the PyMongo library allows you to connect to MongoDB Atlas and develop open source NoSQL databases and carry out non-structured queries in Python.

There are many benefits to utilizing a NoSQL database than a relational database such as flexible data models, horizontal scaling, faster queries and its easy to use for developers.  NoSQL databases usually have flexible schemas which allow you to easily make changes to your database as requirements are changed and updated.  Furthermore, horizontal scaling is a major advantage of NoSQL databases because most of them allow you to scale out horizontally which means you can add cheaper commodity servers when needed.  Moreover, NoSQL databases query faster than SQL databases because data in NoSQL databases is stored in a way that is optimized for queries.  Lastly, NoSQL databases are advantageous because they map their data structures to those of popular programming languages like MongoDB has.  Thus, developers can store and code their data in the ways they are used to and it makes it easier for more programmers to use. Given these advantages of NoSQL and MongoDB, we have chosen to use it to create our database application for the weather database as it proves to be the most efficient and effective way to store and query data. Thus, the Weather database is created by connecting the Atlas Data API using Pymongo.

**Collection and document creation, including relational constraints (PK, FK, NOT NULL)**

The data for the Weather database was sourced from 

https://www.kaggle.com/datasets/sobhanmoosavi/us-weather-events/versions/3?resource=download

Description of the dataset: This is a countrywide weather events dataset that includes 7.5 million events, and covers 49 states of the United States. Examples of weather events are rain, snow, storm, and freezing condition. The data is collected from January 2016 to December 2021, using historical weather reports that were collected from 2,071 airport-based weather stations across the nation.

Description of Weather Events

Weather event is a spatiotemporal entity, where such an entity is associated with location and time. Following is the description of available weather event types in this dataset:

Severe-Cold: The case of having extremely low temperature, with temperature below -23.7 degrees of Celsius.
Fog: The case where there is low visibility condition as a result of fog or haze.
Hail: The case of having solid precipitation including ice pellets and hail.
Rain: The case of having rain, ranging from light to heavy.
Snow: The case of having snow, ranging from light to heavy.
Storm: The extremely windy condition, where the wind speed is at least 60 km/h.
Other Precipitation: Any other type of precipitation which cannot be assigned to previously described event types.

Since the dataset contains 7.5 million datapoints, it was filtered in Excel based on WeatherType, City, and State for the purpose of simulating a database application using MongoDB. 

The filtered data was saved as a new Excel workbook for each collection. Each Excel file for each collection is saved as a CSV file with the collection name. 

Following which, in Google Colab using pymongo the data insert commands are used to insert the data into the database on Cloud.MongoDB.
Since the documents is being created in the manner described above, the constraints related to business rules are not directly displayed in the Database Structure Schema. However, for each collection schema assume the following constraints:

1. WeatherEvents 

WeatherID: PK, NOT NULL 

WeatherType: NOT NULL

Severity: NOT NULL 

2. fs.files 

filename: PK, NOT NULL 

WeatherID: FK, NOT NULL

3. WeatherLocations

LocationID: PK, NOT NULL 

City: NOT NULL 

County: NOT NULL 

State: NOT NULL 

ZipCode: NOT NULL 

4. Airports 

AirportID: PK, NOT NULL 

AirportCode: NOT NULL 

TimeZone: NOT NULL 

LocationID: FK, NOT NULL

5. DailyWeather

DailyWeatherID: PK, NOT NULL 

Date: NOT NULL 

WeatherID: FK, NOT NULL 

WeatherType: FK, NOT NULL 

Severity: FK, NOT NULL 

LocationID: FK, NOT NULL 

AirportID: FK, NOT NULL 

Precipitaion: NOT NULL

Indexes

Indexes support the efficient execution of queries in MongoDB. If an appropriate index exits for a query, MongoDB uses the index to limit the number of documents it must inspect. 

The index stores the value of a specific field or set of fields, ordered by the value of the field. 

The ordering of the index entries supports efficient equlity matches and range-based query operations. MongoDB can return sorted results by using the ordering in the index.

Triggers

Triggers allow for executing server-side logic whenever a document is added, updated, or removed in a linked MongoDB Atlas cluster. The triggers run on a serverless compute layer that scales independently of the database server.

Database triggers are implemented for event-driven data interactions. They use MongoDB change streams to watch for real-time changes in a collection. A change stream is a series of 
database events that each describe an operation on a document in the collection. 

There are four types of database change events: 

INSERT: Represents a new document added to the collection

UPDATE: Represents a change to an existing document in the collection 

DELETE: Represents a document deleted from the collection

Views 

MongoDB views are read-only queryable objects whose contents are defined by an aggregation pipeline on other collections or views. 
There are two types of views: 
1. Standard views: computed as read views, not stored to disk
2. On-demand materalized views: stored on and read from disk using "merge" and "out" stage to update the saved data 

Data Usage:

Main operation (use cases):

1. Retrieving general information from a collection
2. Filtering objects by specific filters/conditions
3. Aggregating/summarising data based on aggregation operators
4. Joining entities/objects to address more complex queries
5. Update or delete operations
