Complete & Detailed Study Notes: Twitter API Tutorial (Week 3)
Course: Privacy and Security in Online Social Media
These notes are prepared exclusively for NPTEL exam preparation. They are comprehensive, structured, and contain all important steps, concepts, code logic, and expected MCQ points.

1. Objective of the Tutorial
To teach students how to create a Twitter developer account, generate API credentials, and collect data programmatically using Python (Twython library) via both REST API and Streaming API.

2. Step-by-Step Account & App Setup
Step 1: Twitter Account Creation

Go to www.twitter.com → Sign Up.
Enter full name, email, password, and choose a unique username.
Skip phone number during signup (add later).
Skip importing contacts and following suggestions.
Email Verification is mandatory (click “Confirm Now” in email).

Step 2: Phone Number Verification (Critical)

Go to Settings → Mobile → Add phone number → Verify with OTP received via SMS.
Reason: Required to create a developer app. Without it, app creation fails.

Step 3: Create Twitter Application

Go to apps.twitter.com → “Create New App”.
Fill: App Name, Description, Website (any URL e.g. http://www.google.com).
Callback URL → Leave blank.
Agree to terms → Create.
Go to Keys and Access Tokens tab.

Four Essential Credentials Generated:

Consumer Key (also called API Key)
Consumer Secret (also called API Secret)
Access Token (generate by clicking “Create My Access Token”)
Access Token Secret

Security Note: Never share these four keys publicly (forum, GitHub, etc.). They allow full access to your account’s data collection capabilities.

3. Twitter API Types























API TypePurposeUse CaseNatureREST APIPull / request specific dataTimelines, Search, User infoOn-demandStreaming APIReal-time continuous data pushLive keyword or user monitoringPersistent connection

4. Python Implementation using Twython
Installation:
Bashsudo pip install twython
(Verify: python → import twython)
Basic Authentication:
Pythonfrom twython import Twython

twitter = Twython(
    APP_KEY, 
    APP_SECRET, 
    OAUTH_TOKEN, 
    OAUTH_TOKEN_SECRET
)

5. Major Code Examples Covered
Example 1: Get Home Timeline (REST)

twitter.get_home_timeline()
Returns list of tweet objects (JSON).
Use json.dumps(data, indent=4) for readable output.
Visualize using jsonviewer.stack.hu.
Each tweet is a dictionary with keys: text, id, user, entities, etc.

Improved Version (Print only tweet text):
Pythonfor tweet in timeline:
    print(tweet['text'])
Example 2: Search API
Pythondata = twitter.search(q="election 2016", 
                      result_type="mixed", 
                      count=100)

result_type: mixed / popular / recent
Access tweets via data['statuses']

Example 3: Streaming API (Real-time)

Uses TwythonStreamer class.
Create custom class MyStreamer.
Override two functions:
on_success(self, data) → Print tweet text (with UTF-8 encoding).
on_error(self, status_code) → Handle errors.

Filter options:
Keywords (e.g., #elections2016)
User ID (track specific user’s tweets in real time)


How to get User ID: From JSON output of timeline → user['id_str'].

6. Important Observations from Tutorial

Fresh account → 0 followers & 0 friends.
New tweets appear instantly in get_home_timeline() and streaming.
Data is rich: contains text, user info, location, entities (hashtags, URLs), timestamps, etc.
Next tutorial → Saving this JSON data into MySQL / MongoDB.


7. Key Terminology (High Weightage)

Consumer Key/Secret: Application-level credentials.
Access Token/Secret: User-level authorization (OAuth).
Endpoint: Specific API function (e.g., /statuses/home_timeline).
Wrapper: Twython simplifies HTTP requests and OAuth handling.
JSON: Standard response format from Twitter API.
Streaming Listener: Event-driven code that reacts when new data arrives.


NPTEL-Style MCQs (Very High Probability)
Easy Level

How many credentials are required for Twitter API authentication in this tutorial?
Ans: 4
Phone number verification is ________ for creating a developer application.
Ans: Mandatory
Which API is used for real-time data collection?
A) REST API B) Streaming API
Correct: B
Twython is a:
Ans: Python wrapper for Twitter API
The website for creating Twitter apps is:
Ans: apps.twitter.com

Medium / Application Level
6. get_home_timeline() returns tweets from:
Ans: Your home feed (tweets from people you follow)

In Search API, count=100 limits:
Ans: Number of tweets returned in one request
result_type="mixed" returns:
Ans: Both popular and recent tweets
In Streaming API, real-time tracking of a user is done using:
Ans: User ID (id_str)
Raw API output is converted into readable format using:
Ans: json.dumps() + jsonviewer.stack.hu

Advanced / Conceptual
11. Each tweet object returned by API is a ________ in Python.
Ans: Dictionary

Why is on_success() function important in streaming?
Ans: It handles incoming real-time data
True/False: The same four keys work for both REST and Streaming APIs. (True)
What is the main difference between REST and Streaming API?
Ans: REST = pull (on demand), Streaming = push (continuous)
If you get authentication error, the first thing to check is:
Ans: Correctness of all four keys/tokens

More Expected Questions (16-30)
16. Command to install Twython → sudo pip install twython
17. JSON viewer website → jsonviewer.stack.hu
18. Callback URL while creating app → Can be left blank
19. Purpose of Access Token → Grants permission on behalf of user
20. In streaming, data comes in real time only if ________. (Keyword is trending / user is active)
21–25. True/False statements on setup steps, JSON structure, etc.
26–30. Sequence/order of steps (account → email verify → phone → app → keys).

Exam Tips for This Tutorial

Memorize the exact 4 credentials and their names.
Clearly differentiate REST vs Streaming.
Remember practical tools: json.dumps(), jsonviewer.stack.hu, Twython installation command.
Understand OAuth flow conceptually (App credentials + User token).
Questions on debugging (wrong keys, missing phone verification) are very common.
Link this with previous weeks: This data will later be stored in MongoDB/MySQL for analysis (trust, credibility, privacy studies).