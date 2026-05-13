
[PSOSM Tutorial 2](https://www.youtube.com/watch?v=Xm8AlGflXzE&t=1345s)
This tutorial shifts from the theoretical "what" of social media data to the practical "how" of extracting it using the **Facebook Graph API**. As a software engineering intern focused on backend systems and SaaS, you will find this particularly relevant for understanding how multi-tenant platforms interact with external data providers.


# Study Notes: Facebook Graph API Tutorial

## 1. Comprehensive Study Notes (Organized by Timestamp)

- **(0:30 - 3:00) Setting up a Development Environment:** To interface with the Facebook API, one must register at `developers.facebook.com`. The process requires creating an **App**, which functions as the programmatic "doorway" to Facebook’s data. This app is the entity that will be authorized by users to access their information.
    
- **(3:30 - 5:00) Authentication & Access Tokens:** The **Access Token** acts as a security key. It is an authorization string that validates both the user and the application's permission scope.
    
- **(7:50 - 8:50) Data Representation (JSON):** The API returns data in **JSON** (JavaScript Object Notation). The video recommends tools like `JSON Viewer` to parse and format these deeply nested, large structures into human-readable hierarchical data.
    
- **(9:50 - 12:00) Graph API Queries & Edge Cases:** Every node (a user, a post) has specific "edges" (connections like reactions, likes, comments). These are queried as sub-resources. Accessing these requires specific granular permissions (e.g., `user_posts`, `email`).
    
- **(12:15 - 14:40) Search & Geolocation:** The API supports searching for "places." This involves passing query parameters like `q` (the search term) and coordinates. The video highlights how the API returns verified status, which is critical for developers ensuring data authenticity.
    
- **(17:00 - 20:30) Programmatic Integration (Python):** The session demonstrates using the `requests` library in Python to perform RESTful HTTP `GET` requests.
    

## 2. Key Terminology

- **Graph API:** The primary way for apps to read and write to the Facebook social graph. It is structured as a network of "nodes" (objects like users, photos) and "edges" (connections between objects).
- **Access Token:** An opaque string that identifies a user, app, or page. It is passed with API requests to prove authorization.
- **JSON (JavaScript Object Notation):** A lightweight data-interchange format, standard for web API responses.
- **API Endpoint:** A specific URL where an API can be accessed. For example, `graph.facebook.com` is the base URL for the Graph API.
- **Scope:** A list of permissions an app requests from a user (e.g., `email`, `public_profile`).

## 3. NPTEL-Style MCQs

**1. Why is an "App" required to use the Facebook Graph API?** A) To generate revenue for the developer. B) To create a unique identifier for the connection between the user's data and the third-party client. C) To bypass the login page for users. D) It is a legacy requirement that is no longer strictly enforced. _Rationale: B. In the Facebook architecture, an App serves as the intermediary entity that secures authorization tokens to access specific user-permitted data._

**2. How does the Graph API handle spaces in query parameters (e.g., in a place search)?** A) By using an underscore (_). B) By using a plus sign (+). C) By encoding them as `%20`. D) By ignoring the space entirely. _Rationale: C. Standard URL encoding rules apply to REST API requests; `%20` is the standard encoding for a literal space character._

**3. What does an "Edge" represent in the Facebook Graph?** A) The user profile itself. B) The hardware running the Facebook server. C) The connection or relationship between two nodes (e.g., a comment on a post). D) The security firewall of the Facebook platform. _Rationale: C. The Graph API model defines "nodes" as objects and "edges" as the paths or relationships between them._

**4. If an API request returns a 403 Forbidden error, what is the most likely cause?** A) The server is down. B) The requested data is missing. C) The access token does not have the necessary scope/permissions. D) The request URL is malformed. _Rationale: C. Permissions are scope-based; if an app asks for `email` but tries to access `posts`, it will be blocked._

**5. Why are access tokens typically short-lived?** A) To save server memory. B) To limit the window of opportunity for an attacker if a token is intercepted. C) To force users to log in every 2 hours. D) Because Facebook servers cannot store long-term keys. _Rationale: B. Security best practice for OAuth mandates periodic rotation to minimize risk._

**6. What is the primary function of the `requests` library in the Python implementation shown?** A) To create the user interface. B) To encrypt the API data. C) To send HTTP requests and handle responses. D) To store the user's password. _Rationale: C. The `requests` library is the standard Python tool for interacting with HTTP-based REST APIs._

**7. Why is JSON the standard format for Facebook API responses?** A) It is the only format supported by Python. B) It is human-readable and easily parsed by virtually every modern programming language. C) It is more secure than XML. D) It is a proprietary format owned by Facebook. _Rationale: B. JSON's lightweight, key-value structure makes it the industry standard for REST API data exchange._

**8. What does a "User Access Token" verify?** A) The identity of the Facebook server. B) The specific user who has authorized the app and the permissions they have granted. C) The MAC address of the developer's computer. D) The total number of likes the user has. _Rationale: B. It provides a delegated authorization, allowing the app to act on behalf of the user within defined limits._

**9. If you want to perform a search that is NOT limited to a specific radius, what is a necessary condition?** A) You must provide a global variable. B) You must provide at least a query string (`q`). C) You must use a deprecated version of the API. D) The API does not allow searches without a radius. _Rationale: B. For place searches, a search term or location-based query is required to narrow down the result set._

**10. How has the Facebook API changed, according to the tutorial, in response to "scandals"?** A) It has become entirely open to the public. B) It has moved to a paid-only model. C) It has introduced a stricter, manual review process for app permissions. D) It has disabled all API access for independent developers. _Rationale: C. Facebook increased scrutiny on app data access to prevent mass data harvesting (as noted in the video explanation at 15:00)._

## 4. Verification Check: Outdated Information

- **API Versions:** The video uses an older version of the Graph API. As of May 2026, **v22.0+** is the standard. Older versions (v18.0 and lower) are officially deprecated.
- **Review Process:** The "manual review" process for permissions is significantly more rigorous than implied in the video. Features like `user_posts` now often require business verification and strict compliance checks.
- **Access Token Expiration:** The video mentions a manual process to extend tokens. Modern practice prefers using the **Refresh Token** flow (for offline access) rather than manually re-generating keys through the Debug Tool.
- **Search Limitations:** The video notes that searching is restricted to "places." This remains accurate; the broader Search API endpoints were heavily throttled/restricted years ago.

---

## **I. Technical Study Notes**

### **1. Entry Points: The App and the Door**

- **The Developer Perspective**: To interact with Facebook as a developer, you must use **developers.facebook.com**.
    
- **The "App" Concept**: You cannot access the API directly as a user; you must create an **App**. Think of the App as the "door" and the **Access Token** as the "key".
    
- **Access Tokens & OAuth**: Tokens are authentication strings generated via the **OAuth protocol**. They verify your identity and the specific permissions (scopes) you have been granted.
    
- **Token Lifespan**: Initial tokens are often short-lived (expiring in ~2 hours) to minimize security risks if intercepted.
    

### **2. The Graph Model in Practice**

- **Nodes**: Objects like Users, Pages, and Groups.
    
- **Edges**: Connections like `/posts`, `/friends`, or `/photos`.
    
- **Permissions (Scopes)**: Accessing specific edges requires explicit user permission (e.g., `user_posts`, `user_birthday`). If a field returns an error or is empty, it is usually due to a missing permission or a privacy setting.
    

### **3. Data Extraction & Versioning**

- **JSON Format**: The API returns data in **JavaScript Object Notation**. Because raw JSON can be a "block" of text, tools like **JSON Viewer** are used to expand/collapse the data hierarchy.
    
- **API Versioning**: Facebook updates the API frequently (e.g., v2.0 vs. v2.6 in the video). Older versions often returned more data by default, whereas newer versions require you to **explicitly request fields** (e.g., `me?fields=id,name,email`).
    
- **Paging**: When a result set exceeds a limit (default is usually 25), the API provides a `paging` object with "next" and "previous" URLs.
    

---

## **II. NPTEL-Style MCQ Practice (Set 6)**

**1. In the Facebook Graph API, what is the specific format used for a Post ID?** A. A single 16-digit random number. B. `post_id_username` C. `user_id_post_id` D. `app_id_user_id` **Rationale:** A post ID is a combination of the creator's ID and the specific post's unique number, separated by an underscore.

**2. Why might the API return a "Total Count" of 6 friends, but only display 1 name in the data list?** A. The other 5 friends have deleted their accounts. B. The API only returns friends who have also authorized the specific App you are using. C. The Access Token has expired mid-request. D. You are using an outdated version of JSON Viewer. **Rationale:** Due to privacy changes, you can typically only "see" friends via the API if they have also used/authorized the same developer app.

**3. Which parameter is used to change the number of results returned in a single API page?** A. `count` B. `size` C. `limit` D. `offset` **Rationale:** The `limit` parameter (e.g., `limit=100`) allows the developer to manually override the default pagination size.

**4. What happens if you try to query a user's `birthday` field without the `user_birthday` permission in your access token?** A. The API will return a random date. B. The API will throw a debug error or return an empty field. C. The App will be automatically deleted. D. Facebook will send a notification to the user's email. **Rationale:** Accessing specific sensitive nodes or edges requires the corresponding permission checkmark during token generation.

**5. How does the Graph API handle "Reactions" compared to "Likes"?** A. Reactions cannot be accessed via API. B. Reactions are queried using the `/reactions` edge and can be filtered by type (e.g., `LOVE`, `HAHA`). C. Reactions are only available in version 2.0. D. Reactions are automatically converted into "Likes" in the JSON response. **Rationale:** Version 2.6 and above allow granular filtering of reactions by type using the `type` parameter.