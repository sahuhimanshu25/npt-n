Complete Study Notes: MySQL Integration for Storing OSN Data (Twitter API)
Provided Study Notes / AI Summary (As Requested):
Study Notes: MySQL Integration for OSN Data
This video outlines the process of installing MySQL, integrating it with Python, and using it to store real-time data from social media APIs.
1. Installation & Configuration (0:15 - 2:54)

MySQL Server Installation: Uses sudo apt-get install mysql-server. The system prompts for a root password.
Security Configuration: Executing sudo mysql_secure_installation is a crucial step to remove anonymous users, disable remote root login, and delete test databases.
Version Check: Use mysql --version.

2. Python-MySQL Integration (2:58 - 4:16)

Dependencies: The video suggests installing build dependencies via apt-get build-dep followed by the library MySQL-python.
Verification: Import MySQLdb in the Python CLI to ensure connectivity.

3. Database & Table Management (4:19 - 5:26)

Creating Database: CREATE DATABASE OSN_data;.
Table Schema: Tables are defined with specific fields and a Primary Key (e.g., tweet_id) to ensure unique indexing.

4. Real-time Data Storage (5:29 - 7:27)

Script Logic: The script establishes a connection to localhost. It utilizes create_connection and close_connection functions.
Insertion: Uses INSERT IGNORE (7:12) to handle duplicate entries, preventing errors when a primary key (Tweet ID) already exists.

5. Querying Stored Data (7:50 - 9:38)

Verification: SELECT * FROM tweets; retrieves all entries.
Aggregations: SELECT COUNT(*) FROM tweets; is used to verify the total number of collected records.

Key Terminology

Relational Database, Primary Key, SQL, API.


My Enhanced Detailed Notes for NPTEL Exam
This tutorial teaches how to store Twitter data (collected via REST or Streaming API) persistently in MySQL, a relational database. This completes the data collection pipeline: API → Python (Twython) → MySQL.
1. MySQL Installation & Setup
Commands:
Bashsudo apt-get install mysql-server
sudo mysql_secure_installation
mysql --version
During mysql_secure_installation:

Set root password (remember it).
Remove anonymous users.
Disallow remote root login.
Remove test database.
Reload privilege tables.

Login to MySQL:
Bashmysql -u root -p
2. Python Integration with MySQL
Installation:
Bashsudo apt-get build-dep python-mysqldb
sudo pip install MySQL-python
Verification:
Pythonimport MySQLdb   # No error = successful installation
Note (Modern Context): MySQL-python (MySQLdb) is older. Modern alternatives are PyMySQL or mysql-connector-python, but NPTEL expects the library shown in the video.
3. Database and Table Creation
SQLCREATE DATABASE OSN_data;
USE OSN_data;

CREATE TABLE tweets (
    tweet_id VARCHAR(255) PRIMARY KEY,
    text TEXT
);

Primary Key (tweet_id): Ensures uniqueness and prevents duplicate entries. Very important for streaming data.

4. Python Script for Storing Streaming Data
Key components of the integrated script:
Pythonimport MySQLdb
from twython import TwythonStreamer

# Database credentials
db_config = {
    'host': 'localhost',
    'user': 'root',
    'passwd': 'your_password',
    'db': 'OSN_data'
}

def create_connection():
    return MySQLdb.connect(**db_config)

def close_connection(conn):
    conn.close()

# In on_success() of streamer
def on_success(self, data):
    if 'text' in data:
        tweet_text = data['text']
        tweet_id = data['id_str']
        
        conn = create_connection()
        cursor = conn.cursor()
        
        # INSERT IGNORE prevents duplicate key errors
        sql = "INSERT IGNORE INTO tweets (tweet_id, text) VALUES (%s, %s)"
        cursor.execute(sql, (tweet_id, tweet_text))
        conn.commit()
        close_connection(conn)
Why INSERT IGNORE?
Streaming data can contain duplicates. This command silently skips insertion if the tweet_id (Primary Key) already exists.
5. Querying the Database
SQLUSE OSN_data;
SHOW TABLES;
SELECT * FROM tweets;
SELECT COUNT(*) FROM tweets;

Key Takeaways for NPTEL

MySQL is a relational database → Data stored in tables with rows & columns.
Primary Key is mandatory for unique identification and efficient querying.
Connection is made to localhost because both Python script and MySQL run on the same machine.
Always handle connections properly (open → execute → commit → close).
This pipeline (Twitter Streaming → MySQL) is the foundation for later analysis (trust, credibility, misinformation detection).


NPTEL-Style MCQs (High Yield)
Conceptual

MySQL is an example of a:
A) NoSQL database B) Relational database Correct: B
What is the purpose of INSERT IGNORE?
A) Delete duplicate rows
B) Skip insertion if Primary Key already exists
C) Update existing records
Correct: B
mysql_secure_installation is used for:
A) Installing MySQL
B) Hardening database security
C) Creating tables
Correct: B

Practical / Code-based
4. Command to create a database:
Ans: CREATE DATABASE OSN_data;

The Primary Key in the tweets table is:
Ans: tweet_id
In Python, the library used to connect to MySQL in this tutorial is:
Ans: MySQLdb
SELECT COUNT(*) FROM tweets; returns:
Ans: Total number of rows in the table
localhost in the connection string refers to:
Ans: The same machine where the script and MySQL are running
Why do we use commit() after execute()?
Ans: To permanently save changes to the database
SHOW TABLES; command does what?
Ans: Lists all tables in the current database

More Expected Questions
11. True/False: Primary Key prevents duplicate tweet insertion. (True)
12. The command to login to MySQL as root is: mysql -u root -p
13. apt-get build-dep is used for installing ________. (Build dependencies)
14. In streaming data collection, why is a database preferred over just printing? (Persistent storage, indexing, easy querying)
15. SELECT * FROM tweets; without WHERE clause returns ________. (All rows)

These notes, when combined with previous Week 3 notes (Twitter API setup, Trust & Credibility, Privacy, Alan Westin, Facebook Inspector), give you full coverage of Week 3.
Would you like me to create one mega consolidated Week 3 Revision PDF-style document with all lectures + tutorials + 100+ MCQs? Or shall we move to Week 4? Just paste the next transcript whenever ready.