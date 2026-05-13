## **Lecture 1: Detailed Study Notes**

### **1. The API Gateway**

- **Definition:** An Application Programming Interface (API) is a set of rules that allow two applications to talk to each other. In OSM, it acts as a regulated "tunnel" to fetch data without scraping the entire website.
    
- **The "Rate Limit" Constraint:** Platforms like Twitter and Facebook limit the number of requests you can make in a specific window (e.g., 15 minutes).
    
    - _Why?_ To prevent server overload and protect data privacy.
        
    - _Strategy:_ Developers must implement "sleep" functions in their code to wait out these limits.
        
- **Tooling:** **Python** is the industry standard here due to libraries like `Requests`, `Tweepy` (for Twitter), and `facebook-sdk`.
    

### **2. JSON: The Language of Data**

- **JSON (JavaScript Object Notation):** A lightweight, text-based data-interchange format.
    
- **Structure:** It uses key-value pairs (e.g., `"name": "Gemini"`).
    
- **Utility:** It is language-independent but very easy for Python to parse into "Dictionaries."
    
- **Graph API Explorer:** A sandbox tool provided by Meta (Facebook) to test queries and see the JSON output in real-time before writing actual code.
    

### **3. Storage Philosophies**

- **Relational (SQL):** Best for structured data.
    
    - _Tools:_ **MySQL** is the primary example. Data is stored in fixed tables.
        
    - _Management:_ **phpMyAdmin** (a web-based GUI).
        
- **Non-Relational (NoSQL):** Best for unstructured or rapidly changing data (like social media posts with varying fields).
    
    - _Management:_ **Propel** or similar Object-Relational Mapping (ORM) tools.
        

### **4. The Graph Model**

Social media isn't just a list; it’s a web of relationships.

- **Nodes (Vertices):** The "entities"—Users, Pages, Photos, Posts.
    
- **Edges (Links):** The "interactions"—Likes, Shares, Tags, Friends, Comments.
    
- **Graph API:** Facebook uses this name specifically because their data structure is a massive Social Graph.
    

---

## **Comprehensive MCQ Practice Set**

### **Category: APIs and Collection**

1. **What is the primary purpose of an API in the context of Social Media Analysis?**
    
    A. To design the user interface of the platform.
    
    B. To provide a programmatic "tunnel" for data collection.
    
    C. To increase the speed of the website.
    
    D. To block third-party developers.
    
2. **Which of the following is a direct consequence of "Rate Limiting"?**
    
    A. Data is returned in XML instead of JSON.
    
    B. The API key becomes permanently invalid.
    
    C. A developer must pause data collection after a certain number of requests.
    
    D. The data collected becomes encrypted.
    
3. **Which language is most recommended in the lecture for handling API objects and parsing?**
    
    A. C++
    
    B. HTML
    
    C. Python
    
    D. Java
    

### **Category: Data Formats and Tools**

4. **JSON stands for:**
    
    A. Java System Object Notation
    
    B. JavaScript Object Notation
    
    C. Joint Social Network
    
    D. Just-in-time Serialized Objects
    
5. **The "Graph API Explorer" is primarily used for:**
    
    A. Storing data in a MySQL database.
    
    B. Visually inspecting JSON objects and testing queries.
    
    C. Managing PHP configurations.
    
    D. Visualizing the final research paper graphs.
    
6. **In a JSON object, data is typically represented as:**
    
    A. Rows and Columns
    
    B. Key-Value pairs
    
    C. Linked Lists
    
    D. Binary Code
    

### **Category: Storage and Structure**

7. **Which tool is specifically mentioned for managing MySQL databases via a web interface?**
    
    A. Propel
    
    B. phpMyAdmin
    
    C. JSONLint
    
    D. OAuth
    
8. **In the Facebook Graph Model, a "Like" on a photo is represented as:**
    
    A. A Node
    
    B. An Edge
    
    C. A Table
    
    D. A Rate Limit
    
9. **If you are storing data in a traditional row-and-column format, you are likely using:**
    
    A. NoSQL
    
    B. A Graph Database
    
    C. MySQL (Relational)
    
    D. A JSON file only
    
10. **Which of these is considered a "Node" in a social graph?**
    
    A. A user’s friend request.
    
    B. A comment on a post.
    
    C. A user’s profile.
    
    D. The "share" action.
    

---

### **Answer Key**

|**Q**|**Ans**|**Q**|**Ans**|**Q**|**Ans**|
|---|---|---|---|---|---|
|**1**|B|**5**|B|**9**|C|
|**2**|C|**6**|B|**10**|C|
|**3**|C|**7**|B|||
|**4**|B|**8**|B|||