These notes bridge the gap between manually exploring data and building a robust backend system for automated collection. As you are currently interning at **Skypoint Cloud**, you will recognize this process as a standard **OAuth 2.0 flow**, which is essential for multi-tenant SaaS architectures that need persistent access to third-party data.

### **Comprehensive Study Notes**

- **Access Token Management (0:12 - 7:51):**
    - **Concept:** Access tokens provide the authorization needed to make API calls. Short-lived tokens expire quickly (e.g., 1-2 hours), making them unsuitable for long-term programmatic data collection.
    - **Solution:** Developers must create a Facebook App to gain an `App ID` and `App Secret`. These credentials allow the exchange of a short-lived token for a long-lived one (valid for 60 days) via a `GET` request to the `oauth/access_token` endpoint.
- **Programmatic Data Collection with Python (8:00 - 13:00):**
    - **Tools:** The `requests` library is used to handle HTTP operations. Data returned by the Facebook Graph API is in `JSON` format.
    - **Parsing:** The `json` library is used to convert the raw response text into a dictionary/list structure, allowing for programmatic access to specific fields like `data` or `message`.
- **Handling API Responses (17:27 - 23:36):**
    - **Pagination:** When data exceeds a set `limit`, the API returns a `paging` object containing a `next` URL.
    - **Architecture:** A `while` loop is required to iterate through the results, checking for the existence of the `next` key in each subsequent response to fetch the remaining records.

---

### **Key Terminology**

- **Graph API:** A RESTful API that allows developers to query data from the Facebook social graph (nodes like users, pages, posts; edges like likes, comments).
- **Access Token:** An opaque string that identifies the user, app, and permissions associated with a request.
- **JSON (JavaScript Object Notation):** A lightweight data-interchange format consisting of key-value pairs.
- **Endpoint:** A specific URL where the API provides access to resources (e.g., `/{page-id}/feed`).
- **Indentation (Python):** Unlike C/C++ which uses curly braces, Python defines code blocks (functions, loops) through whitespace indentation.

---

### **NPTEL-Style MCQs**

1. **Why is it necessary to exchange a short-lived token for a long-lived one?** A) To increase the API response speed. B) To bypass authentication entirely. C) To enable persistent data collection without frequent manual re-authentication. D) To access restricted premium data fields. _Rationale:_ Short-lived tokens expire in ~1 hour; automating collection requires a stable token that lasts for 60 days.
    
2. **How does Python handle the structure of a JSON response compared to manual string manipulation?** A) Python treats JSON as a single long string. B) The `json` library converts JSON into native dictionaries and lists, allowing access via keys and indices. C) Python ignores JSON structure and maps it to a database automatically. D) Python requires a separate C++ module to parse JSON. _Rationale:_ `json.loads()` translates the JSON object into standard Python data types (dicts/lists), enabling easy navigation.
    
3. **In the context of the `while` loop for pagination, what is the primary indicator that no more data exists?** A) The API returns an HTTP 404 error. B) The `data` list contains more than 100 items. C) The `paging` key is missing, or the `next` field is null. D) The access token becomes invalid. _Rationale:_ The API provides a `next` URL for pagination; if this field is null or absent, it signals the end of the dataset.
    
4. **What does the `grant_type=fb_exchange_token` signify in the API request?** A) It tells Facebook to reset the user's password. B) It indicates the intent to swap a valid short-lived token for a long-lived one. C) It grants the developer permanent administrative access to the page. D) It is an obsolete parameter that is no longer used. _Rationale:_ This specific parameter is the mechanism used in the OAuth flow to request the 60-day token.
    
5. **Why might a developer receive no additional information when querying an older version of the Graph API (e.g., v2.0) with a newly created app?** A) Older versions are locked by default. B) New apps are only provisioned to work with the versions of the API available at the time of their creation or later. C) The query syntax is different for older versions. D) Facebook deletes data from older versions. _Rationale:_ Access to legacy API versions is typically restricted to apps created while those versions were current.
    
6. **Which library is essential for managing HTTP headers and connection persistence in the demonstration?** A) `json` B) `os` C) `requests` D) `sys` _Rationale:_ The `requests` library is the standard Python tool for executing HTTP GET/POST calls to web APIs.
    
7. **If the `paging` dictionary exists in the response, is it safe to assume there is always a `next` page?** A) Yes, if `paging` is present, `next` is guaranteed. B) No, the `paging` object might only contain a `previous` page. C) No, `paging` only appears when the data is empty. D) Yes, `paging` is synonymous with `next`. _Rationale:_ One must explicitly check for the `next` key within the `paging` object, as sometimes only `previous` exists (e.g., if you are already at the end of the feed).
    
8. **What is the significance of the `App Secret`?** A) It is public information displayed on the user's profile. B) It is used to cryptographically verify that the request is coming from your specific application. C) It allows anyone with the ID to access your personal Facebook account. D) It is used to generate the CSS for the app's website. _Rationale:_ The secret is a security credential meant to pair with the App ID to authenticate the app's identity during the token exchange.
    
9. **What happens if you fail to convert the response object to `.text` in the `requests.get()` call?** A) The program prints the full HTTP response object (metadata included), which is harder to parse. B) The program will crash immediately. C) The API will return an error. D) It makes no difference; Python handles it automatically. _Rationale:_ The `response` object is an object containing metadata; `.text` (or `.json()`) is required to extract the actual payload body.
    
10. **In Python, what does `response['data']` imply if `response` is a parsed JSON object?** A) It is accessing the file named 'data' on the hard drive. B) It is a function call to fetch new data. C) It is accessing the value associated with the 'data' key in a dictionary. D) It is selecting all data fields from the server. _Rationale:_ Once loaded into Python, JSON objects are dictionary-like structures, and `['data']` is the key lookup syntax.
    

[

### [Get a Long-Lived Us](https://developers.facebook.com/documentation/facebook-login/guides/access-tokens/get-long-lived)

---

## **I. Technical Study Notes: Persistent Collection**

### **1. Access Token Lifecycles**

- **The Problem**: Tokens generated via the Graph API Explorer are **Short-Lived**, typically expiring in 1–2 hours.
    
- **The Solution**: To collect data for prolonged periods (e.g., tracking sentiment over weeks), you must exchange the short-lived token for a **Long-Lived Access Token**, which is valid for approximately **60 days**.
    

### **2. The App Framework**

To get a 60-day token, you must register a **Facebook App** to obtain two critical credentials:

- **App ID (Client ID)**: The public identifier for your application.
    
- **App Secret (Client Secret)**: A private key used to prove the application's identity to Facebook.
    
- **Version Pinning**: New apps are restricted to the version of the API available at their creation (e.g., v2.6+). Unlike the default Explorer app, a new app cannot access "Legacy" data structures from older versions like v2.0.
    

### **3. Programmatic Implementation (Python)**

- **`requests` Library**: The standard tool for making `GET` requests to the Graph API URL.
    
- **`json` Library**: Crucial for parsing the response. Use `json.loads(data.text)` to convert the raw string into a Python **Dictionary** or **List**.
    
- **Indentation Control**: In Python, code blocks (functions, loops) are defined by whitespace (tabs/spaces) rather than curly braces `{}`.
    

### **4. Handling Large Datasets (Pagination)**

- **Logic**: Facebook rarely returns all data at once. It provides a `paging` key.
    
- **The While Loop**: A robust script must check `if 'next' in response['paging']`. If true, the script should update the URL to the "next" link and continue the loop until the key is missing or the list is empty.
    

---

## **II. NPTEL-Standard MCQ Practice (Set 7)**

**1. Why does the API return a "400 Bad Request" if you attempt to use an expired short-lived token?**

A. The server is under maintenance.

B. The token is an authentication string that must be valid for the Resource Server to respond.

C. The App ID was entered incorrectly.

D. You are using the wrong version of Python.

**2. In the Python code `next_page = response['paging']['next']`, what does the second set of square brackets represent?**

A. A new list being created.

B. A multi-dimensional array index.

C. Accessing a nested key within the 'paging' dictionary.

D. A syntax error in Python.

**3. Which parameter is required in the GET request to specifically exchange a token for a 60-day version?**

A. `grant_type=fb_exchange_token`

B. `token_type=permanent`

C. `extend=true`

D. `client_auth=long_lived`

**4. If a loop is fetching posts from a Page feed, what is the best indicator that you have reached the very first post ever made?**

A. The `id` becomes 0.

B. The `paging` key is either absent or does not contain a `next` field.

C. The `access_token` expires.

D. The API returns a 404 error.

**5. Why was the "App Secret" required to extend the token validity?**

A. To verify the user's password.

B. To cryptographically prove the request is coming from a registered application.

C. To encrypt the data being downloaded.

D. To increase the limit of posts per page from 25 to 100.

---

### **Answer Key**

| **Q1** | **Q2** | **Q3** | **Q4** | **Q5** |
| ------ | ------ | ------ | ------ | ------ |
| **B**  | **C**  | **A**  | **B**  | **B**  |