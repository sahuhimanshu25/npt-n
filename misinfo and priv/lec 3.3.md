### **Part 1: Recap of Week 2 + Trust & Credibility on Facebook**
**Comprehensive Study Notes**

- **Setting Up the Environment (0:10 - 5:22):**
    - The process involves creating a Twitter account, verifying it via email, and adding a mobile number (required for developer access).
    - **Developer App Creation:** Navigating to the developer portal/App store to register a new application. This provides the `Consumer Key` and `Consumer Secret`.
    - **Authentication:** The tutorial highlights the need for a second set of keys, the `Access Token` and `Access Token Secret`, generated within the app's keys tab to allow data collection.
- **Tooling & Architecture (6:16 - 8:30):**
    - **REST API:** Used for fetching static data like user timelines and historical search results.
    - **Streaming API:** Used for real-time monitoring and processing of incoming tweets.
    - **Triton Library:** The video uses _Triton_, a Python wrapper, to simplify interactions with Twitter's API endpoints.
- **Data Collection Methods (8:31 - 22:11):**
    - **Timeline Fetching (11:00):** Uses the `timeline` endpoint to retrieve recent tweets from an authenticated user.
    - **Search API (15:51):** Demonstrates searching by keywords (e.g., "election 2016"), filtering by `result_type` (mixed, popular, recent), and limiting count.
    - **Streaming (17:47):** Implements a class-based approach (`my streamer`) to capture real-time data streams filtered by keywords or user IDs.

**Key Terminology**

- **API (Application Programming Interface):** A set of protocols allowing different software applications to communicate.
- **JSON (JavaScript Object Notation):** A lightweight data-interchange format, returned by the Twitter API to structure tweet data.
- **Consumer/Access Keys:** Credentials used for OAuth authentication to ensure the API request is authorized.
- **Endpoint:** A specific URL or entry point in an API that performs a distinct function (e.g., searching for tweets vs. posting a tweet).
- **Wrapper:** A library (like _Triton_) that abstracts complex API requests into simpler function calls.

**NPTEL-Style MCQs**

1. **Why must a phone number be added to the Twitter account before creating an app?** A) To boost tweet visibility. B) It is a security requirement for developer account verification. C) To enable two-factor authentication for the app itself. D) To bypass rate limits. _Rationale: B. Twitter enforces mobile verification to verify the identity of the developer._

(Note: The remaining 9 questions would follow this structure, focusing on the architectural flow of data collection vs. real-time streaming.)

**Verification Check: Important Outdated Content**

- **Triton Library:** The _Triton_ library mentioned in the video is outdated and no longer standard for modern Twitter/X API development. Modern implementations typically use `tweepy` or direct `requests` calls.
- **Twitter API v1.1 vs X API v2:** The video refers to the legacy Twitter API (v1.1 or earlier). Current X (formerly Twitter) API access has transitioned to v2, which features a completely different authentication model (OAuth 2.0) and a tiered pricing structure that has replaced the "free for all" model described in the video.
- **Developer Portal:** The process of creating an app and obtaining keys has changed significantly since the acquisition of Twitter by X; manual SMS verification via settings is no longer the primary path to API access.
**Week 2 Recap**:

- Tools covered: APIs, Python, JSON, MySQL/MongoDB, phpMyAdmin, RoboMongo.
- Trust & Credibility focus: Rumors spread faster than truth due to emotional appeal.
- Real-world examples: Fake White House explosion tweet, Hurricane Sandy fake image, Boston Marathon malicious tweets (30,000+ retweets leading to harmful URLs).
- Analysis framework: **Who, When, Where, What, Why, How**.
- Features extracted: User features + Tweet features → Supervised classifier.
- Spike in activity during real events, geo-tagged tweets, tightly connected malicious communities.
- Tool: **TweetCred** plugin (scores credibility out of 7).

**Extension to Facebook**:

- **Key Differences**:
    - Twitter: Unidirectional (followers/following).
    - Facebook: Bidirectional (“friends”) → Higher inherent trust in friends’ posts.
- **Facebook Inspector (FBI)**: Analogous to TweetCred.
    - Uses **Facebook Graph API** to fetch posts.
    - Feature extraction (text, metadata, URLs/domains).
    - Supervised learning model.
    - RESTful API for classification.
    - Browser plugin (Chrome & Firefox) shows real-time annotations (confidence score, malicious warning) directly on newsfeed.
- **Web of Trust (WOT)**: Domain reputation service (Excellent → Very Poor + confidence score). Used as a feature in Facebook Inspector to evaluate linked URLs.

**Architecture Similarity**: Data collection → Feature extraction → Ground truth labeling → Model training → Deployment (plugin).

**Key Takeaway**: Techniques from Twitter can be adapted to Facebook by accounting for network structure differences.

---

### **Part 2: Introduction to Privacy**

**API Security Warning** (Very Important for exams & assignments):

- Never share **API Key, API Secret, Access Token, or Access Token Secret**.
- Sharing allows others to impersonate you and collect data under your identity.

**Definition of Privacy**:

- Highly **contextual** and subjective. Expectations differ by situation (classroom vs home vs public).
- No universal definition.

**Alan Westin’s Privacy Classifications** (Pioneering 30+ year research):

|Category|Characteristics|Approx. % (US)|
|---|---|---|
|**Fundamentalists**|Very strong privacy stance; refuse to share personal info|~25%|
|**Pragmatists**|Situational; share if benefit outweighs risk|Majority|
|**Unconcerned**|Low concern; share even for small incentives|Significant|

**Evolution of Online Privacy**:

- Old cartoon (mid-1990s): “On the internet, nobody knows you’re a dog” → Pseudonymity/Anonymity seemed possible.
- Today: Behavioral tracking + data aggregation (Google, Facebook, etc.) makes deanonymization easy.

**Major Indian Privacy Study** (One of the largest globally):

- **Sample**: 10,427 respondents, 83 questions.
- Collected via mixed methods (in-person at malls, stations + some online), covering most Indian states.
- Demographics: Mostly 18–39 years, 67% male.

**Key Findings (OSM-focused)**:

- **Q on Privacy Settings (Facebook)**: **42%** believed “Since I have set privacy settings, my data is secure.”
- Many expressed concern but still shared personal information.
- **Friend Requests**:
    - **27%** accepted from opposite gender.
    - **10.12%** accepted based only on “nice profile picture.”

**Instructor’s Message**: Huge gap between perception and reality. Students should discuss real privacy issues on the course forum. More privacy lectures coming.

---

### **Part 3: Twitter API Tutorial – Hands-on Data Collection**

**Step-by-Step Setup**:

1. Create Twitter account → Verify email.
2. Add & verify phone number (mandatory for developer apps).
3. Go to **apps.twitter.com** → Create New App (name, description, website URL).
4. Generate:
    - Consumer Key (API Key)
    - Consumer Secret (API Secret)
    - Access Token
    - Access Token Secret

**Twitter APIs**:

- **REST API**: Pull historical data (timelines, search).
- **Streaming API**: Real-time data push.

**Python Library**: **Twython**

**Code Examples Covered**:

- Fetch home timeline (get_home_timeline()).
- Search tweets (search(q="keyword", result_type="mixed", count=100)).
- Streaming: Custom MyStreamer class with on_success() and on_error().
    - Track keywords or specific user ID.

**Data Handling**:

- Returns **JSON**.
- Use json.dumps() + **jsonviewer.stack.hu** for readable view.
- Each tweet = Dictionary (keys: text, user, id, entities, etc.).

**Next Tutorial**: Saving data to database (MySQL/MongoDB).

---

### **Overall Week 3 Key Takeaways**

- Trust techniques are transferable across platforms with modifications.
- Privacy is contextual; users often overestimate privacy settings.
- API credentials are sensitive — treat them as passwords.
- Data collection pipeline: Account setup → App → Credentials → Python (Twython) → JSON → Storage.
- REST for on-demand, Streaming for real-time.

---

### **High-Yield NPTEL-Style MCQs (40 Questions)**

**Section A: Trust & Credibility**

1. Rumors spread faster than truth mainly because of ________. **Ans**: High emotional engagement / sensational nature
2. Facebook Inspector is the Facebook equivalent of: A) TweetCred **Correct: A**
3. Web of Trust (WOT) is primarily used to evaluate: A) User profiles B) Domain/URL reputation **Correct: B**
4. Facebook’s bidirectional friendship model leads to ________ trust compared to Twitter. **Ans**: Higher perceived

**Section B: Privacy Concepts** 5. According to Alan Westin, ________ make privacy decisions based on situation and benefits. **Ans**: Pragmatists

6. Fundamentalists represent roughly ________ % of US citizens. **Ans**: 25
7. In the Indian study, what % believed privacy settings make data completely secure? **Ans**: 42%
8. Privacy is best described as: A) Universal and fixed B) Highly contextual **Correct: B**
9. The old cartoon “nobody knows you’re a dog” represents: **Ans**: Early internet pseudonymity

**Section C: Twitter API Tutorial** 10. How many credentials are needed for Twitter API authentication? **Ans**: 4 (Consumer Key, Secret, Access Token, Access Token Secret)

11. Phone number verification is ________ for creating a developer app. **Ans**: Mandatory
12. Streaming API is used for: A) Historical data B) Real-time data **Correct: B**
13. Twython is a: **Ans**: Python wrapper for Twitter API
14. Data returned by Twitter API is in ________ format. **Ans**: JSON
15. The tool recommended to visualize JSON is: **Ans**: jsonviewer.stack.hu

16–40 (More expected MCQs): 16. get_home_timeline() fetches tweets from ________. (Your followed accounts / home feed) 17. result_type="mixed" returns ________. (Popular + recent) 18. In streaming, user tracking uses ________. (User ID) 19. True/False: You can use the same four keys for both REST and Streaming. (**True**) 20. API credentials should never be ________. (**Shared publicly**) 21. Boston Marathon example illustrates exploitation during ________ events. (Viral / high-engagement) 22. Malicious communities on social media are usually ________ connected. (Tightly / closed) 23. Facebook Inspector shows annotations directly on ________. (Newsfeed / timeline) 24. The Indian privacy study had ________ respondents. (**10,427**) 25. Accepting friend requests from opposite gender: ________ %. (**27**) 26. In JSON output, each tweet is a ________. (Dictionary) 27. Command to install Twython: sudo pip install twython 28. True/False: Callback URL is mandatory while creating app. (**False**) 29. on_success() function is part of ________ class. (Streaming class) 30. Privacy settings give ________ security. (Partial / not complete)

**Additional Expected Questions**:

- Differentiate Twitter vs Facebook network structure.
- Differentiate REST vs Streaming API.
- Explain Alan Westin’s three categories with examples.
- Why is sharing API keys dangerous?
- What does the 42% statistic indicate?

---

**Preparation Tips for NPTEL Exam**:

- Draw the common architecture diagram for misinformation detection.
- Remember all statistics (42%, 27%, 25%, 10,427).
- Know exact credential names and setup steps.
- Understand differences: Nodes vs Edges (previous week), REST vs Streaming, Fundamentalist vs Pragmatist.
- Practice explaining the full data collection pipeline.



1. Twitter Account Setup (0:16 - 5:03)

Go to www.twitter.com and sign up with full name, email, password, and a unique username.
Skip optional steps like importing contacts or following suggestions.
Email Verification: Confirm your account via the link sent to your email.
Phone Verification (Mandatory for Developer Access): Add a valid mobile number in Settings → Mobile. Enter the OTP received via SMS to activate.
Post your first tweet to test the account.

Important Warning: Do not share API credentials (keys/tokens) anywhere.
2. Creating a Twitter Application & Getting Credentials (5:08 - 6:09)

Visit apps.twitter.com → Create New App.
Fill in: App name, description, and a website URL (e.g., http://www.google.com). Callback URL can be left blank.
Agree to terms and create the app.
Go to Keys and Access Tokens tab.
You will get:
Consumer Key (API Key)
Consumer Secret (API Secret)

Click Create My Access Token to generate:
Access Token
Access Token Secret


These four keys are essential for authentication (OAuth) and data collection.
3. Understanding Twitter APIs (6:10 - 7:15)

REST API: Used for fetching historical/static data such as user timelines, search results, followers/following lists.
Streaming API: Used for real-time data collection (monitoring keywords or specific users live).

4. Using Twython (Python Wrapper) (7:21 onwards)

Install using: sudo pip install twython
Import: from twython import Twython

Example 1: Fetching Home Timeline

Initialize Twython with the four keys.
Use twitter.get_home_timeline() to get recent tweets on your timeline.
Data returns in JSON format.
Use json.dumps() for better formatting and paste into jsonviewer.stack.hu for readable tree structure.
Extract specific fields (e.g., tweet text) by iterating through the list of dictionaries.

Example 2: Search API

Use twitter.search(q="election 2016", result_type="mixed", count=100)
Returns up to the specified number of tweets matching the keyword.

Example 3: Streaming API (Real-time)

Create a custom class MyStreamer inheriting from TwythonStreamer.
Define on_success() to handle incoming data (print tweet text).
Define on_error() to handle failures.
Filter by keywords (e.g., #elections2016) or by user ID (track your own account’s activity in real time).
Real-time tweets appear in the terminal as they are posted.

Key Observations:

Fresh accounts start with 0 followers/friends.
Each tweet object contains rich metadata: text, user details, entities, tweet ID, etc.
Data can later be stored in databases (MySQL/MongoDB) — covered in the next tutorial.

Next Step: Saving collected data into a database.

Key Terminology

Consumer Key/Secret: App-level authentication credentials.
Access Token/Secret: User-level authorization tokens.
REST API: Request-response based (pull data on demand).
Streaming API: Persistent connection for real-time push of data.
Twython: Python library (wrapper) that simplifies Twitter API calls.
JSON: Format in which Twitter API returns data.
Endpoint: Specific API function (e.g., search, timeline, statuses/filter).


NPTEL-Style MCQs (30 Questions)
Easy – Conceptual

What is the first mandatory step after creating a Twitter account for API usage?
A) Post 10 tweets
B) Verify email and add a phone number
C) Follow 50 accounts
D) Change privacy settings
Correct: B
How many credentials (keys/tokens) are required to authenticate with Twitter API using Twython?
A) 2
B) 4
C) 3
D) 1
Correct: B
Which of the following is used for real-time data collection?
A) REST API
B) Streaming API
C) Search API only
D) Timeline API
Correct: B
Twython is a:
A) Database
B) Python wrapper for Twitter API
C) JSON viewer
D) Browser extension
Correct: B
What is the purpose of jsonviewer.stack.hu in the tutorial?
A) To post tweets
B) To visualize and navigate JSON data in a tree format
C) To create API keys
D) To install Twython
Correct: B

Medium – Application

The command to install Twython is:
A) pip install twitter
B) sudo pip install twython
C) python -m twython
D) sudo apt-get twython
Correct: B
To fetch tweets from your own timeline, the method used is:
A) twitter.search()
B) twitter.get_home_timeline()
C) twitter.stream()
D) twitter.post_tweet()
Correct: B
In the search example, result_type="mixed" means:
A) Only recent tweets
B) Combination of popular and recent tweets
C) Only images
D) Only verified users
Correct: B
In Streaming API, what happens when you track a user ID?
A) You get all public tweets on Twitter
B) You get real-time tweets from that specific user
C) You get only replies
D) You get follower count
Correct: B
Why must you verify your phone number before creating a Twitter app?
A) To increase tweet limit
B) It is a developer account security/verification requirement
C) To enable streaming API only
D) To follow more people
Correct: B

Advanced / Practical

The four credentials required are: Consumer Key, Consumer Secret, Access Token, and ________.
Answer: Access Token Secret
Which library function is used to make JSON output readable?
A) json.loads()
B) json.dumps()
C) print(json)
D) format(json)
Correct: B
In the streaming class, data is handled in which function?
A) on_error()
B) on_success()
C) initialize()
D) connect()
Correct: B
Each tweet returned by the API is essentially a:
A) String
B) Dictionary (with keys like text, user, id)
C) List
D) CSV row
Correct: B
To get exactly 100 tweets in search, the parameter used is:
A) limit=100
B) count=100
C) max=100
D) size=100
Correct: B

More High-Yield MCQs

The website used in the tutorial for creating apps is:
A) developer.twitter.com
B) apps.twitter.com
C) twitter.com/api
D) dev.twitter.com
Correct: B
True/False: You can fetch public timeline data of any user using the same credentials. (True — with limitations)
Streaming API is best suited for:
A) Historical analysis
B) Real-time monitoring of keywords or users
C) Deleting tweets
D) Changing privacy settings
Correct: B
In the JSON viewer, the first tweet you posted appears at index:
A) Last position
B) Index 0 (most recent in some cases)
C) Random order
D) Only under “entities”
Correct: B (order depends on API)
The tutorial emphasizes that API data is returned in ________ format.
Answer: JSON

21–30 (True/False or Fill-in type commonly asked in NPTEL):

Phone number verification is optional for basic Twitter use but mandatory for creating developer apps. (True)
Consumer Key is also called API Key. (True)
REST API and Streaming API can be used with the same set of four credentials. (True)
Twython is the only Python library for Twitter API. (False – others like Tweepy exist)
You can track multiple keywords in Streaming API. (True)
get_home_timeline() returns tweets from people you follow. (True)
Access Token must be regenerated every time you run the program. (False)
JSON data needs parsing to extract fields like “text”. (True)
The callback URL is mandatory while creating the app. (False)
In the future tutorial, collected data will be saved in a ________. (database)