# MongoDB Concept

## Introduction
- MongoDB is a NoSQL database management system used for managing large amounts of data.
-	It stores data in a non-relational format, using documents instead of rows and columns.
-	Data is stored in JSON-like format, specifically BSON (Binary JSON).
## Key Concepts
1. Document: A group of field-value pairs representing an object.
2. Collection: A group of documents.
3. Database: A group of collections.
## Installation Process
1. Go to MongoDB's website and navigate to the installation section.
2. Download and install MongoDB Community Edition based on your operating system (Windows example provided).
3. Install MongoDB Compass, a graphical user interface for MongoDB.
4. Install MongoDB Shell (mongosh) for command-line interaction.
## Using MongoDB Shell
1. Connection: Establish a connection using the mongosh command.
2. Commands:
```bash
show dbs: List all databases.
use <db_name>: Switch to a specific database.
db.createCollection("<collection_name>"): Create a collection.
db.dropDatabase(): Drop the current database.
```
## Using MongoDB Compass
1.	Creating a Database and Collection:
o	Use the GUI to create a new database and add collections.
o	Insert documents into collections manually or by importing JSON/CSV files.
2.	Deleting a Database:
o	Select the database and click the trash icon to delete it.
Inserting Documents
1.	MongoDB Shell:
o	db.<collection>.insertOne({<field>: <value>, ...}): Insert a single document.
o	db.<collection>.insertMany([{...}, {...}, ...]): Insert multiple documents.
2.	MongoDB Compass:
o	Use the GUI to insert single or multiple documents.
Basic Data Types
1.	String: Series of text within quotes.
2.	Integer: Whole numbers.
3.	Double: Numbers with decimal portions.
4.	Boolean: True or False values.
5.	Date: Date objects using the new Date() constructor.
6.	Null: No value.
7.	Array: Lists of values enclosed in square brackets.
8.	Nested Document: Documents within documents.
Sorting and Limiting Documents
1.	Sorting:
   ```bash
Sort in ascending order:
db.<collection>.find().sort({<field>: 1})
Sort in descending order:
db.<collection>.find().sort({<field>: -1})
```
3.	Limiting:
o	db.<collection>.find().limit(<number>): Limit the number of documents returned.
4.	Combining Sort and Limit:
o	db.<collection>.find().sort({<field>: 1}).limit(<number>): Combine sorting and limiting.
Using Compass for Sorting and Limiting
•	Use the GUI options to sort and limit documents within a collection.
Basic Sorting and Limiting
•	Sorting:
o	Use the sort method with {field: 1} for ascending and {field: -1} for descending order.
o	Example: db.students.find().sort({GPA: -1}) will sort students by GPA in descending order.
•	Limiting:
o	Use the limit method to restrict the number of documents returned.
o	Example: db.students.find().limit(1) returns the top student.
The find Method
•	Basic Usage:
o	Retrieve all documents with db.collection.find().
o	Example: db.students.find() returns all students.
•	Query Parameters:
o	The first argument specifies selection filters.
o	Example: db.students.find({name: "SpongeBob"}) returns students named SpongeBob.
o	Multiple filters: {GPA: 4.0, fullTime: true}.
•	Projection Parameters:
o	The second argument specifies which fields to return.
o	Example: db.students.find({}, {name: true, GPA: true, _id: false}) returns only names and GPAs.
Updating Documents
•	Update One Document:
o	db.collection.updateOne(filter, update) with $set to modify fields.
o	Example: db.students.updateOne({name: "SpongeBob"}, {$set: {fullTime: true}}).
•	Update Many Documents:
o	db.collection.updateMany(filter, update).
o	Example: db.students.updateMany({}, {$set: {fullTime: false}}).
•	Unset Fields:
o	Use $unset to remove fields.
o	Example: db.students.updateOne({name: "SpongeBob"}, {$unset: {fullTime: ""}}).
Deleting Documents
•	Delete One Document:
o	db.collection.deleteOne(filter).
o	Example: db.students.deleteOne({name: "Larry"}).
•	Delete Many Documents:
o	db.collection.deleteMany(filter).
o	Example: db.students.deleteMany({fullTime: false}).
Comparison Operators
•	Not Equals:
o	$ne for not equal.
o	Example: db.students.find({name: {$ne: "SpongeBob"}}).
•	Less Than / Less Than Equals:
o	$lt and $lte.
o	Example: db.students.find({age: {$lt: 20}}).
•	Greater Than / Greater Than Equals:
o	$gt and $gte.
o	Example: db.students.find({age: {$gt: 27}}).
•	Range:
o	Combine operators.
o	Example: db.students.find({GPA: {$gte: 3, $lte: 4}}).
•	In / Not In:
o	$in and $nin.
o	Example: db.students.find({name: {$in: ["SpongeBob", "Patrick", "Sandy"]}}).
Logical Operators
•	And:
o	$and to check multiple conditions.
o	Example: db.students.find({$and: [{fullTime: true}, {age: {$lte: 22}}]}).
•	Or:
o	$or to check if at least one condition is true.
o	Example: db.students.find({$or: [{fullTime: true}, {age: {$lte: 22}}]}).
•	Nor:
o	$nor to check if both conditions are false.
o	Example: db.students.find({$nor: [{fullTime: true}, {age: {$lte: 22}}]}).
•	Not:
o	$not to reverse the effect of a query condition.
o	Example: db.students.find({age: {$not: {$gte: 30}}}).
Indexes
•	Creating an Index:
o	db.collection.createIndex({field: 1}) for ascending or -1 for descending.
o	Example: db.students.createIndex({name: 1}).
•	Explain Method:
o	Method chaining explain("executionStats") to view query performance.
o	Example: db.students.find({name: "Larry"}).explain("executionStats").
•	Get Indexes:
o	db.collection.getIndexes().
o	Example: db.students.getIndexes() returns all indexes on the students collection.


Here are the CRUD (Create, Read, Update, Delete) operations in MongoDB, each explained with commands.
Create
1.	Insert a Single Document
db.collection.insertOne({ name: "Alice", age: 30, city: "New York" })
2.	Insert Multiple Documents
db.collection.insertMany([
   { name: "Bob", age: 25, city: "San Francisco" },
   { name: "Charlie", age: 35, city: "Los Angeles" }
])
Read
1.	Find One Document
db.collection.findOne({ name: "Alice" })
2.	Find All Documents
db.collection.find({})
3.	Find with a Query
db.collection.find({ city: "New York" })
4.	Find with a Query and Projection
db.collection.find({ city: "New York" }, { name: 1, age: 1, _id: 0 })
Update
1.	Update a Single Document
db.collection.updateOne(
   { name: "Alice" },
   { $set: { age: 31, city: "Boston" } }
)
2.	Update Multiple Documents
db.collection.updateMany(
   { city: "San Francisco" },
   { $set: { city: "SF" } }
)
3.	Replace a Document
db.collection.replaceOne(
   { name: "Alice" },
   { name: "Alice", age: 32, city: "Chicago" }
)
Delete
1.	Delete a Single Document
db.collection.deleteOne({ name: "Alice" })
2.	Delete Multiple Documents
db.collection.deleteMany({ city: "SF" })
These commands demonstrate how to perform basic CRUD operations in MongoDB. Each operation is essential for managing and interacting with the data stored in your MongoDB collections.

Here are 20 commonly used MongoDB commands along with their descriptions:
1.	Show List of Databases
show dbs
2.	Create/Select a Database
use <database_name>
3.	Show Current Database
db
4.	Show Collections in a Database
show collections
5.	Create a Collection
db.createCollection("<collection_name>")
6.	Insert a Document into a Collection
db.<collection_name>.insertOne({ <document> })
7.	Insert Multiple Documents into a Collection
db.<collection_name>.insertMany([ { <document1> }, { <document2> } ])
8.	Find One Document in a Collection
db.<collection_name>.findOne({ <query> })
9.	Find All Documents in a Collection
db.<collection_name>.find({ <query> })
10.	Update a Document in a Collection
db.<collection_name>.updateOne({ <query> }, { $set: { <field>: <value> } })
11.	Update Multiple Documents in a Collection
db.<collection_name>.updateMany({ <query> }, { $set: { <field>: <value> } })
12.	Delete a Document from a Collection
db.<collection_name>.deleteOne({ <query> })
13.	Delete Multiple Documents from a Collection
db.<collection_name>.deleteMany({ <query> })
14.	Drop a Collection
db.<collection_name>.drop()
15.	Drop a Database
db.dropDatabase()
16.	Count Documents in a Collection
db.<collection_name>.countDocuments({ <query> })
17.	Aggregate Data in a Collection
db.<collection_name>.aggregate([ { <stage> }, { <stage> } ])
18.	Create an Index on a Collection
db.<collection_name>.createIndex({ <field>: <index_type> })
19.	Show Indexes of a Collection
db.<collection_name>.getIndexes()
20.	Explain Query Execution Plan
db.<collection_name>.find({ <query> }).explain("executionStats")

