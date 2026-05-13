omplete Study Notes: MongoDB for Storing OSN Data (Week 3 Tutorial)
Provided Comprehensive Study Notes / AI Summary (As Requested):
Comprehensive Study Notes
Introduction to MongoDB (0:13 - 0:29)

MongoDB: An open-source, non-relational, document-based database. Unlike relational databases (SQL) that use fixed-schema tables, MongoDB uses flexible, JSON-like documents, making it ideal for hierarchical or rapidly evolving data structures.

Installation Process (0:33 - 1:52)

Environment: The tutorial demonstrates installation on an Ubuntu/Linux-based system using apt-get package management.
Steps:
Import the MongoDB GPG public key for package verification.
Add the MongoDB repository to the system file list.
Update the local package index (sudo apt-get update).
Install the package using sudo apt-get install -y mongodb.

Verification: Access the shell by typing mongo in the terminal.

Basic Database Management (2:14 - 2:58)

show dbs: Lists existing databases.
use: Switches to a specific database. Note: A database is not physically created until data is inserted into it.

Connecting Python to MongoDB (3:00 - 4:19)

Tool: pymongo is the official Python driver acting as a connector between Python applications and MongoDB.
Installation: sudo pip install pymongo.
Usage: Import MongoClient from pymongo to establish a connection object, which is used to define the specific database and collection to access.

Data Insertion and Storage (4:34 - 5:15)

Mechanism: Collected data (e.g., from a Twitter stream) is converted into a JSON object.
_id key: Every record in MongoDB requires a unique identifier. Manually setting _id to the tweet_id is a best practice for deduplication.

Data Exploration & Querying (6:07 - 7:30)

show collections: Lists collections within the active database.
db..count(): Returns the number of documents in a collection.
db..find(): Retrieves data.
db..findOne(): Fetches a single record, typically used for inspecting document structure without cluttering the console.

Key Terminology

NoSQL (Non-Relational), BSON/JSON, Collection, Document, Sharding.


My Enhanced Detailed Notes for NPTEL Exam
This tutorial introduces MongoDB as a NoSQL/document-oriented database alternative to MySQL for storing social media data (especially Twitter/ Facebook data collected via APIs). It is more suitable for semi-structured, high-velocity, and evolving data like tweets.
Why MongoDB for OSN Data?

Flexible schema (no fixed columns).
Stores data in JSON-like documents (BSON internally).
Excellent for hierarchical data (nested objects, arrays).
Horizontal scaling (sharding) capability.

Installation Steps (Ubuntu/Linux)
Bash# 1. Import GPG key
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

# 2. Add repository
echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list

# 3. Update & Install
sudo apt-get update
sudo apt-get install -y mongodb-org
Verification:
Bashmongo          # Opens MongoDB shell
show dbs
Important Note: A database only appears in show dbs after inserting data (lazy creation).
Basic MongoDB Commands
Bashuse osndata                    # Switch to database (creates on first insert)
show dbs
show collections
db.tweets.count()              # Count documents
db.tweets.find()               # Show all documents
db.tweets.findOne()            # Show one formatted document
Python Integration using PyMongo
Installation:
Bashsudo pip install pymongo
Verification:
Pythonimport pymongo
Example Script for Storing Twitter Streaming Data:
Pythonfrom pymongo import MongoClient
from twython import TwythonStreamer

# Connection
client = MongoClient()                    # Connects to localhost:27017
db = client.osndata                       # Database
collection = db.tweets                    # Collection (like table)

class MyStreamer(TwythonStreamer):
    def on_success(self, data):
        if 'text' in data:
            # Set _id for uniqueness
            data['_id'] = data['id_str']
            collection.insert_one(data)   # Insert entire tweet JSON
            print("Stored:", data['text'][:50])
Key Points:

Entire tweet object (JSON) is stored — no need to flatten fields.
_id field acts as primary key (unique identifier). Must be set manually to avoid duplicates.

Comparison: MySQL vs MongoDB (Very Important for Exam)


| Feature         | MySQL (Relational)             | MongoDB (NoSQL)                |
| --------------- | ------------------------------ | ------------------------------ |
| Data Model      | Tables + Rows + Columns        | Collections + Documents (JSON) |
| Schema          | Fixed / Rigid                  | Flexible / Dynamic             |
| Best For        | Structured data                | Semi-structured, nested data   |
| Query Language  | SQL                            | MongoDB Query Language         |
| Primary Key     | `tweet_id` (defined in CREATE) | `_id` field                    |
| Use Case in OSN | Clean tabular analytics        | Storing full raw tweets easily |







































FeatureMySQL (Relational)MongoDB (NoSQL)Data ModelTables + Rows + ColumnsCollections + Documents (JSON)SchemaFixed / RigidFlexible / DynamicBest ForStructured dataSemi-structured, nested dataQuery LanguageSQLMongoDB Query LanguagePrimary Keytweet_id (defined in CREATE)_id fieldUse Case in OSNClean tabular analyticsStoring full raw tweets easily

NPTEL-Style MCQs
Easy Level

MongoDB is a ________ database.
Ans: Non-relational / Document-oriented / NoSQL
In MongoDB, a database is physically created when:
Ans: First document is inserted into it
The Python library used to connect to MongoDB is:
Ans: pymongo

Medium / Application Level
4. The command to list all databases in MongoDB shell is:
Ans: show dbs

The command to list all collections in the current database is:
Ans: show collections
Which field is used as unique identifier in MongoDB documents?
Ans: _id
db.tweets.findOne() is used to:
Ans: Retrieve and display a single well-formatted document
Why is MongoDB preferred for Twitter data?
Ans: Because tweet data is semi-structured and contains nested fields

Advanced / Conceptual
9. True/False: MongoDB requires a fixed schema like MySQL. (False)

INSERT IGNORE in MySQL is conceptually similar to setting ________ in MongoDB.
Ans: Unique _id
What does MongoClient() connect to by default?
Ans: localhost:27017
In the tutorial, the collection name used for storing tweets was:
Ans: tweets
True/False: You can store the entire JSON tweet object directly in MongoDB. (True)
db.tweets.count() returns:
Ans: Number of documents in the collection
Major advantage of MongoDB over MySQL for OSN data:
Ans: Flexible schema and easy storage of nested JSON data


These notes, along with all previous Week 3 materials (Twitter API setup, MySQL integration, Trust & Credibility, Privacy, Alan Westin, Facebook Inspector), give you complete coverage of Week 3.
Would you like a full Week 3 Mega Revision document (all lectures + tutorials combined with 100+ MCQs) or shall we proceed to Week 4? Just send the next transcript.
Keep going — you're building a very strong foundation! Good luck for