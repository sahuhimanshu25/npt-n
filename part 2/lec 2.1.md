## **. Detailed Study Notes**

### **1. The Big Picture: Summarizing Week 1**

- **The 5 V's of OSM Data**: The fundamental challenges of social media data are **Volume** (amount), **Velocity** (speed of generation), **Veracity** (truthfulness), **Variety** (different types), and **Value** (importance).
    
- **Real-World Impact**: Social media isn't just digital; it has real consequences, such as compromised accounts causing stock market fluctuations or false images (like the 2015 Chennai floods crocodile) causing public panic.
    
- **Infrastructure**: While the course supports Linux for its development environment, Python remains the primary language for writing collection scripts.
    

### **2. Data Collection: The API Tunnel**

- **The Concept**: An **API (Application Programming Interface)** acts as a "tunnel" between your script and the social media service. You send a request, and the server responds with specific data.
    
- **Rate Limits**: This is the most critical constraint. Platforms do not allow unlimited data harvesting; they set limits on how many requests you can make in a specific timeframe to protect their servers.
    

### **3. Data Formats: JSON & XML**

- **JSON (JavaScript Object Notation)**: The industry standard for social media data. It represents data in key-value pairs (e.g., `{"id": "123", "name": "PK"}`).
    
- **Parsing**: Python is used to parse these JSON objects into dictionaries, making the data programmatically accessible.
    
- **Visualization**: Tools like `json.viewer.stack.hu` are recommended to transform dense blocks of API text into a human-readable hierarchy.
    

### **4. Storage and Management**

- **Relational (MySQL)**: Best for structured data stored in rows and columns.
    
    - **Management**: **phpMyAdmin** is used to visually inspect and query MySQL databases.
        
- **Non-Relational (MongoDB)**: Increasingly popular for social media because it handles unstructured data more naturally.
    
    - **Management**: **RoboMongo** (now Studio 3T) is used to browse MongoDB data.
        

### **5. The Graph Model (Facebook focus)**

- **Data Structure**: Facebook views the world as a **Social Graph**.
    
- **Nodes**: Represent objects (Users, Photos, Videos, Status updates).
    
- **Edges**: Represent interactions or connections (Friendships, Likes, Comments).
    
- **Universal ID**: Every node (user, page, or post) is assigned a unique numeric ID.
    

---

## **II. NPTEL-Standard MCQ Practice**

**1. According to the '5 V's' framework, which 'V' deals with the uncertainty or truthfulness of the data generated on social media?** A. Volume B. Velocity C. Veracity D. Variety **Rationale:** Veracity refers to the reliability and accuracy of the information, such as detecting fake news or rumors.

**2. In the context of API interaction, what is the primary purpose of 'Rate Limiting'?** A. To increase the speed of data transfer. B. To prevent programmatic access to the site. C. To prevent server overload and manage fair usage. D. To encrypt the JSON response during transit. **Rationale:** Rate limits ensure platforms can handle traffic without their servers being crashed by too many automated requests.

**3. If you are retrieving a list of "likes" on a specific Facebook post, how is that "like" categorized in the Graph API model?** A. As a Node B. As an Edge C. As a Database Table D. As a Rate Limit **Rationale:** In the graph model, interactions between entities (like a user liking a post) are represented as edges.

**4. Which tool is specifically mentioned as a way to visually inspect data stored in a MongoDB database?** A. phpMyAdmin B. RoboMongo C. Graph API Explorer D. JSON Viewer **Rationale:** While phpMyAdmin is for MySQL, RoboMongo is the specialized tool for NoSQL/MongoDB visualization.

**5. What is the fundamental difference between the 'id' of a user and the 'id' of a post in the Facebook Graph API?** A. User IDs are numeric, while post IDs are alphanumeric. B. Both are unique numeric IDs representing nodes in the graph. C. Only users have IDs; posts are identified by their text. D. Post IDs are temporary, whereas User IDs are permanent. **Rationale:** In the Facebook Graph model, every object (node) has a unique numeric identifier.

**6. Why is Python recommended over other languages in this course for OSM data collection?** A. It is the only language that supports Linux. B. It has extensive libraries for reading URLs, parsing JSON, and interacting with APIs. C. It bypasses the rate limits set by social media platforms. D. It automatically generates the required App Secret keys. **Rationale:** Python's rich ecosystem of libraries (like `requests` and `json`) makes it the most efficient choice for API-based research.

**7. In a JSON object returned by an API, what does the structure typically consist of?** A. Rows and columns separated by commas. B. Key-value pairs organized in a hierarchical structure. C. Binary data that must be decrypted. D. Only unique numeric IDs without text. **Rationale:** JSON uses key-value pairs, making it lightweight and easy to map directly to Python dictionaries.

**8. What HTTP status code is commonly associated with hitting a Rate Limit (Too Many Requests)?** A. 200 OK B. 404 Not Found C. 429 Too Many Requests D. 500 Internal Server Error **Rationale:** 429 is the standard response from an API when a user has exceeded their quota.


### **Comprehensive Study Notes**

- **Introduction to OSM Data (0:00 - 4:45):** The lecture emphasizes the massive scale of social media data, characterized by the '5 Vs' (Volume, Velocity, etc.). Issues such as compromised accounts and misinformation highlight the necessity of data collection for security and privacy research.
- **APIs (Application Programming Interfaces) (4:48 - 7:00):** APIs act as the bridge between your program and social media servers. They facilitate programmatic data retrieval. A critical constraint mentioned is **Rate Limiting**—a mechanism used by platforms to prevent abuse and manage server load by restricting the number of requests per unit of time.
- **Data Formats (7:01 - 9:30):** The primary data format encountered in API responses is **JSON** (JavaScript Object Notation), a lightweight, text-based format. The lecture suggests using tools like 'JSON viewers' to parse and visually inspect the hierarchical structures returned by endpoints.
- **Storage & Databases (9:31 - 11:35):**
    - **MySQL:** A Relational Database Management System (RDBMS) using tables, rows, and columns, suitable for structured data.
    - **NoSQL:** Mentioned as an alternative for storing massive, less structured social data. Tools like _phpMyAdmin_ are used for _MySQL_, while others are used for _NoSQL_ storage.
- **Graph Model (11:36 - 13:12):** Facebook stores data as a 'Social Graph', where users/entities are **Nodes** and their interactions (likes, comments, friendships) are **Edges**. This is why the Facebook API is specifically referred to as the 'Graph API'.

### **Key Terminology**

- **API (Application Programming Interface):** A set of protocols allowing different software applications to communicate.
- **Rate Limiting:** A security and performance constraint that limits the number of API requests a user can make within a specific timeframe.
- **JSON Parsing:** The process of converting a JSON-formatted string into a data structure (like a Python dictionary) that a program can manipulate.
- **OAuth:** While not explicitly detailed, it is the industry-standard authorization framework (often required by APIs) that allows users to grant access to their data without sharing passwords.
- **Nodes & Edges:** Fundamental concepts in Graph Theory. Nodes represent entities (e.g., a User, a Photo), and Edges represent the relationship or interaction between those nodes.

### **Verification & Outdated Content**

- **API Stability:** Many APIs discussed (specifically Facebook's Graph API and Twitter's API) have undergone major version changes. Twitter’s API (now X API) has significantly changed its access tiers and pricing models since this lecture was recorded. Always check the official developer documentation for the latest authentication requirements.
- **Tooling:** While _phpMyAdmin_ remains popular, modern data science stacks often utilize _Pandas_ for data manipulation and _MongoDB_ or _PostgreSQL_ for storage rather than basic _MySQL_ setups.

### **NPTEL-Style MCQs**

1. **Why do platforms enforce rate limiting on their APIs?** A) To reduce the size of the data returned. B) To protect server infrastructure from overload and ensure fair usage. C) To force users to switch to paid subscriptions only. D) To prevent data from being encrypted. _Rationale: B is correct; rate limits are critical for maintaining service availability._
    
2. **In the context of the Facebook Graph API, what does a 'friendship' represent?** A) A Node. B) A Database Table. C) An Edge. D) A JSON Object. _Rationale: C; in graph models, interactions between entities are defined as edges._
    
3. **Which data format is most commonly returned by modern social media APIs?** A) CSV. B) JSON. C) Binary. D) Excel. _Rationale: B; JSON is the standard for web-based API communication due to its lightweight and human-readable nature._
    
4. **Why might a researcher prefer a NoSQL database over SQL for social media data?** A) SQL does not support data storage. B) NoSQL handles unstructured, rapidly changing data schemas more flexibly. C) SQL is too expensive. D) NoSQL is always faster for simple queries. _Rationale: B; NoSQL databases are designed for high-velocity, semi-structured social media content._
    
5. **What is the primary role of an API in data collection?** A) It automates the analysis of data. B) It acts as a secure communication channel between a user's program and the service. C) It encrypts the user's password. D) It replaces the need for a database. _Rationale: B; APIs provide the interface for requested data to pass from the server to the client._
    
6. **What should a developer do when they encounter an 'HTTP 429' error?** A) Retry immediately. B) Stop the program permanently. C) Implement exponential backoff to retry after waiting. D) Change their API key. _Rationale: C; 429 indicates too many requests; waiting allows the rate limit window to reset._
    
7. **If you have a JSON response from an API, how do you typically access a specific 'user_id' field in Python?** A) Using SQL `SELECT`. B) Parsing it as a dictionary/object. C) Converting it to a binary file. D) It cannot be accessed. _Rationale: B; JSON is naturally parsed into native language data types like dictionaries/objects._
    
8. **What characterizes the '5 Vs' of social media data?** A) Variety, Volume, Velocity, Veracity, Value. B) Validity, Volume, Versioning, View, Vector. C) Visibility, Velocity, Voice, Variable, Value. D) Verification, Volume, Velocity, Virtual, View. _Rationale: A; these represent the primary challenges of Big Data._
    
9. **Why is the Facebook API called the 'Graph API'?** A) Because it generates charts automatically. B) Because it models data as nodes and edges. C) Because it is only for photos. D) Because it was built with a graphing calculator. _Rationale: B; it follows a graph-based data architecture._
    
10. **What is the best way to verify if your code is hitting API limits?** A) Checking the file size of the download. B) Inspecting HTTP response headers for limit status. C) Asking the social media platform in an email. D) Counting the number of lines in the code. _Rationale: B; headers like 'X-Rate-Limit-Remaining' provide this information._