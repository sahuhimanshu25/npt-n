## **art 1: Advanced Study Notes (Deep Dive)**

### **1. The Token Exchange Architecture**

- **The "Why":** Standard User Access Tokens are "Short-Lived" (valid for ~1-2 hours). For large-scale data collection, you cannot manually refresh tokens.
    
- **The "How":** You perform an **Exchange**. You send a `GET` request to the `/oauth/access_token` endpoint.
    
- **Required Parameters for Extension:**
    
    1. `grant_type`: Must be set to `fb_exchange_token`.
        
    2. `client_id`: Your App ID.
        
    3. `client_secret`: Your App Secret.
        
    4. `fb_exchange_token`: The short-lived token you currently have.
        
- **Result:** A "Long-Lived" token valid for ~60 days.
    

### **2. Programmatic Workflow (Python)**

- **The `requests` library:** Used to simulate browser behavior. `requests.get(url)` returns a Response Object.
    
- **The `json` library:** Crucial for **Deserialization**. The API sends a string; `json.loads(response.text)` converts that string into a **Python Dictionary**, allowing you to access data via keys (e.g., `data['paging']`).
    
- **The "While" Loop Logic:** Since social media data is too large for one request, the API uses a "Cursor-based" approach.
    
    - _Step A:_ Fetch Page 1.
        
    - _Step B:_ Check if `['paging']['next']` exists.
        
    - _Step C:_ If yes, update the URL and repeat. If no, break.
        

### **3. API Versioning & Backward Compatibility**

- **Version Pinning:** Facebook uses versioning (e.g., v18.0) to ensure code doesn't break when they update their platform.
    
- **Availability:** An app can only access versions that were "active" when the app was created. You cannot "downgrade" a new app to an old, deprecated API version (like v2.0).
    

---

## **Part 2: The "Master" MCQ Bank (High-Volume)**

**1. Which HTTP method is used to fetch data from the Graph API?**

A. POST

B. GET

C. DELETE

D. PUT

**2. What is the standard duration of a "Long-Lived" User Access Token?**

A. 24 Hours

B. 7 Days

C. 60 Days

D. 1 Year

**3. If you want to access a user's posts, which permission (scope) must be requested?**

A. public_profile

B. user_posts

C. publish_actions

D. read_stream

**4. What does the `json.loads()` function do in the context of data collection?**

A. It sends data to the Facebook server.

B. It converts a JSON string into a Python object (Dictionary/List).

C. It deletes the access token for security.

D. It formats the data into a PDF.

**5. In a pagination loop, what is the 'Terminal Condition' (when the loop stops)?**

A. When the status code is 404.

B. When the 'next' key is missing from the 'paging' object.

C. When the 'data' list is empty.

D. When the access token expires.

**6. Which of these is a sensitive credential that should NEVER be exposed in client-side code?**

A. App ID

B. User ID

C. App Secret

D. Object ID

**7. Why is a 'While' loop preferred over a 'For' loop for API pagination?**

A. While loops are faster in Python.

B. The total number of pages is unknown at the start.

C. For loops cannot handle JSON data.

D. While loops automatically refresh the access token.

**8. What is the significance of the `grant_type=fb_exchange_token` parameter?**

A. It is used to delete an account.

B. It signals the API to upgrade a short-lived token to a long-lived one.

C. It is used to change the app's name.

D. It allows the app to bypass rate limits.

**9. If your application was created in 2024, can it use Graph API v2.0?**

A. Yes, all versions are backward compatible.

B. No, apps are restricted to versions active during or after their creation.

C. Yes, if you have the App Secret.

D. No, unless you are a Facebook employee.

**10. What is the relationship between 'Nodes' and 'Edges' in the Graph API?**

A. Nodes are interactions, Edges are users.

B. Nodes are objects (User, Post, Photo), Edges are connections (Likes, Comments).

C. Nodes and Edges are the same thing.

D. Nodes are the API keys, Edges are the data values.

**11. When using the `requests` library, how do you extract the JSON payload if the response is stored in a variable `r`?**

A. r.to_json()

B. r.json()

C. r.get_data()

D. r.parse()

**12. What does a "403 Forbidden" error typically mean in the Graph API?**

A. The server is under maintenance.

B. Your internet is disconnected.

C. Your token lacks the necessary permissions (scope) for that specific data.

D. You have typed the URL incorrectly.

**13. In the URL `[https://graph.facebook.com/v12.0/me/posts?access_token=](https://graph.facebook.com/v12.0/me/posts?access_token=)...`, what does `me` represent?**

A. The Facebook CEO's profile.

B. A reserved keyword for the user identified by the access token.

C. The name of the application.

D. The system administrator.

**14. What happens if you try to use an "App Secret" as an "Access Token"?**

A. It works but is slower.

B. The request will fail because they serve different cryptographic purposes.

C. It only works for public data.

D. It bypasses all privacy settings.

**15. Why does Facebook use Pagination?**

A. To make coding more difficult for developers.

B. To reduce server load and optimize response time by sending data in chunks.

C. To hide data from the users.

D. To force developers to buy premium plans.

---

### **Answer Key & Rationale**

| **Q**  | **Ans** | **Rationale**                                                                              |
| ------ | ------- | ------------------------------------------------------------------------------------------ |
| **1**  | **B**   | GET is used for retrieving resources; POST is for creating them.                           |
| **2**  | **C**   | 60 days (approx. 2 months) is the standard for extended tokens.                            |
| **3**  | **B**   | `user_posts` is the specific permission required to read a user's timeline.                |
| **4**  | **B**   | It stands for "Load String"—deserializing text into a Python dict.                         |
| **5**  | **B**   | The absence of the 'next' URL confirms there is no more data to fetch.                     |
| **6**  | **C**   | The App Secret is like a password; exposing it allows others to spoof your app.            |
| **7**  | **B**   | Since you don't know if there are 5 or 500 pages, a conditional 'while' loop is necessary. |
| **8**  | **B**   | This is the specific flag that triggers the token extension logic.                         |
| **9**  | **B**   | Facebook "sunsets" old versions; new apps cannot access legacy versions.                   |
| **10** | **B**   | Nodes = Nouns (entities), Edges = Verbs (actions/connections).                             |
| **11** | **B**   | `r.json()` is a built-in method in the `requests` library to parse JSON.                   |
| **12** | **C**   | 403 means "I know who you are, but you don't have permission for this."                    |
| **13** | **B**   | `/me` is a convenient alias for the current authenticated user's ID.                       |
| **14** | **B**   | The App Secret identifies the _app_; the Token identifies the _session/user_.              |
| **15** | **B**   | Sending 10,000 posts in one JSON would crash most browsers/scripts.                        |