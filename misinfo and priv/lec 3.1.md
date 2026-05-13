
# Study Notes: Misinformation on Social Media (Week 3.1)

### 1. Recap of Previous Concepts (0:10 - 4:40)

- **Data Collection & APIs:** Introduction to Python, MongoDB for storage, and PHPMyAdmin for visualization. Emphasis on using Twitter and Facebook APIs for research.
- **Trust & Credibility:** Discussion on how rumors spread faster than truthful information. Malicious users exploit viral events (e.g., Boston Marathon) to propagate malicious URLs.
- **Analysis Techniques:** Categorization of analysis by _who, when, where, what, why, and how_. Users and tweet features are extracted to train classifiers that distinguish between legitimate and fake content.
- **Data Representation:** Mention of geotagging (spikes in tweets corresponding to real-world events) and identifying communities of malicious actors.

### 2. Twitter vs. Facebook Structural Differences (5:00 - 6:30)

- **Network Topology:**
    - _Twitter:_ Unidirectional platform (followers/following).
    - _Facebook:_ Bi-directional network (friends).
- **Social Trust:** Facebook's personal connections make posts from friends inherently more credible to users than those from random accounts.

### 3. Architectural Model for Misinformation Detection (6:30 - 8:00)

- **Tool:** _Facebook Inspector (FBI)_.
- **Workflow:**
    1. **Data Acquisition:** Fetch posts via _Facebook Graph API_.
    2. **Feature Extraction:** Analyze text, metadata, and embedded domains.
    3. **Supervised Learning:** Use pre-trained models to classify posts as credible or malicious.
    4. **Output:** RESTful API serves the classification result to the user.

### 4. Domain Trust Verification: Web of Trust (WOT) (8:00 - 9:00)

- **Function:** Analyzes domains to provide reputation scores (Excellent, Good, Satisfactory, Poor, Very Poor).
- **Usage:** Used as a feature within _Facebook Inspector_ to evaluate the trustworthiness of URLs shared in posts.

### 5. Plugin Implementation (9:00 - 11:58)

- **Tooling:** Browser extensions (Chrome/Firefox) provide real-time annotations on social media feeds.
- **Functionality:** Annotates posts with "Confidence" scores or "Malicious" warnings, allowing users to verify content before interacting.

---

## Key Terminology

- **Graph API:** The primary way for apps to read and write to the Facebook social graph.
- **Geotagging:** Adding geographical identification metadata to media, useful for mapping events.
- **Supervised Learning:** A machine learning approach where a model is trained on labeled data to make predictions on new, unseen data.
- **RESTful API:** An architectural style for providing standards between computer systems on the web.
- **WOT (Web of Trust):** A community-based rating system for websites.

---

## NPTEL-Style MCQs

1. **Why do rumors often spread faster than truthful information on social media?** A) Truthful information is censored. B) Rumors are often sensational and elicit high emotional engagement. C) Twitter algorithms prioritize fake news. D) Truthful news requires more data. _Rationale: Rumors often exploit emotional triggers, which increases the likelihood of viral sharing compared to neutral factual updates._ (Correct: B)
    
2. **What is a fundamental difference between Twitter and Facebook regarding social trust?** A) Twitter has more users. B) Facebook's bi-directional "friends" model implies a higher inherent trust than Twitter's unidirectional follow model. C) Twitter is more secure. D) Facebook does not use an API. _Rationale: The personal, bi-directional nature of Facebook connections naturally impacts perceived credibility._ (Correct: B)
    
3. **How does the 'Facebook Inspector' tool utilize the Web of Trust (WOT)?** A) It replaces the browser's DNS. B) It acts as a feature for evaluating the safety of external domains found in posts. C) It forces users to log into Facebook. D) It verifies the user's identity. _Rationale: WOT serves as an external reputation service integrated to filter malicious links._ (Correct: B)
    
4. **In the context of the architecture, what is the role of the Supervised Learning model?** A) To store user passwords. B) To automate the posting process. C) To classify a post as credible or malicious based on extracted features. D) To visualize the network. _Rationale: Machine learning models use training data to classify new inputs._ (Correct: C)
    
5. **What does a 'spike' in geotagged social media content typically represent?** A) A server error. B) A significant real-world event occurring at that location. C) A bot attack. D) High internet speeds. _Rationale: Social media volume correlates with real-world activity._ (Correct: B)
    
6. **Why is feature extraction critical in misinformation detection?** A) It makes the data look better. B) It converts raw text into numerical vectors that models can process. C) It deletes duplicate tweets. D) It increases the API rate limit. _Rationale: Models require structured numerical inputs derived from raw data._ (Correct: B)
    
7. **What is the primary function of the Graph API?** A) Designing the Facebook UI. B) Facilitating programmatic access to Facebook social graph data. C) Managing user advertising budgets. D) encrypting browser cookies. _Rationale: The Graph API is the official bridge between apps and Facebook's data._ (Correct: B)
    
8. **What does a 'low confidence' annotation on a post indicate?** A) The system is very sure it is fake. B) The system cannot definitively classify the post as fake or real. C) The internet connection is slow. D) The author is anonymous. _Rationale: Low confidence indicates the model lacks sufficient indicators for a high-accuracy prediction._ (Correct: B)
    
9. **Why are browser plugins used for Facebook/Twitter inspection instead of just server-side analysis?** A) They are easier to hack. B) They provide real-time, in-context warnings to the user on their actual timeline. C) They are faster to develop. D) They don't require internet. _Rationale: Plugins enable immediate, visual feedback where the user is actually interacting with content._ (Correct: B)
    
10. **What is the main risk of malicious actors exploiting viral events?** A) They increase website traffic for the media. B) They trick users into sharing personal information or clicking malicious links. C) They cause the server to crash. D) They fix fake news. _Rationale: Malicious actors use the high engagement of events to execute phishing or malware campaigns._ (Correct: B)
    

---

## Verification Check

- **API Versions:** The video mentions the "Facebook Graph API." Note that Facebook frequently updates their Graph API versions (e.g., v18.0+). Older code examples using very old API versions may fail due to deprecation.
- **Web of Trust (WOT):** While the concept remains valid, the specific browser extensions or service reputation may have changed. It is highly recommended to check the current [official WOT website](https://mywot.com/) to ensure compatibility with modern browser security standards.
- **Techniques:** While the core logic of feature-based classification remains standard in academic research, modern detection now relies heavily on Large Language Models (LLMs) rather than just manual feature extraction. Cross-reference these notes with modern "Deepfake" and "LLM-based detection" literature.
Recap of Week 2 and Core Concepts in Trust & Credibility
The instructor begins by reviewing data collection tools (APIs, Python, MongoDB, phpMyAdmin, RoboMongo) and hands-on practice with Facebook and Twitter APIs. The core discussion revolves around Trust and Credibility on social media.
Rumors and fake content spread much faster than truthful information because they are often sensational and trigger strong emotional responses. Several real-world examples were discussed: fake tweets impacting stock markets, a viral fake image during Hurricane Sandy, and malicious exploitation during the Boston Marathon bombing (where a tweet about an 8-year-old victim was retweeted over 30,000 times to lure users to malicious URLs).
A key analytical framework emphasized is answering Who, When, Where, What, Why, and How when studying social media content. Researchers extract user features and tweet/post features to build classifiers that can automatically label content as legitimate or fake. Analysis often reveals:

Spikes in tweet volume during major real-world events.
Geo-tagged tweets helping map where information originates.
Malicious users forming tightly connected, closed communities.

The overall architecture for such systems includes data collection via APIs, annotation for ground truth, feature engineering, model building (usually supervised learning), and evaluation using standard metrics. TweetCred plugin was highlighted as a practical tool that assigns credibility scores (e.g., x/7) to tweets in real time.
Extending Twitter Techniques to Facebook
Facebook and Twitter differ significantly in structure and trust dynamics:

Twitter is unidirectional (followers/following).
Facebook is bidirectional (“friends” relationship), making it more personal. Users tend to trust posts from friends more than random accounts.

Despite these differences, the overall architecture for misinformation detection remains similar. The course introduces Facebook Inspector (FBI) — a tool analogous to TweetCred. It works as follows:

Fetches posts using Facebook Graph API.
Performs feature extraction (text, metadata, embedded URLs/domains).
Uses a supervised learning model trained on labeled data.
Provides classification (credible vs. malicious) through a RESTful API.
Browser plugin (Chrome/Firefox) overlays warnings or confidence scores directly on the user’s Facebook newsfeed.

Web of Trust (WOT) Integration
Facebook Inspector also uses the Web of Trust (WOT) service as a feature. WOT takes a domain as input and returns a reputation rating: Excellent, Good, Satisfactory, Poor, or Very Poor, along with a confidence score. This helps evaluate the safety of links shared in Facebook posts. The same idea was mentioned earlier for domain analysis (age of domain, registrar information, etc.).
The lecture demonstrates the Facebook Inspector plugin in action on real posts (e.g., Bollywood gossip or iPhone rumors), showing red flags for low-confidence or malicious content.
Key Takeaway: Techniques developed for Twitter (feature-based classification) can be successfully adapted to Facebook and other platforms by accounting for network-specific structures and features. Browser plugins make these solutions practical for everyday users by giving real-time, in-context warnings.

Key Terminology

Bidirectional vs Unidirectional Network: Facebook (mutual friends) vs Twitter (one-way follow).
Feature Extraction: Converting raw posts into numerical vectors for ML models.
Supervised Learning: Training models on labeled (ground truth) data.
RESTful API: Standard web service interface for delivering model predictions.
Web of Trust (WOT): Community-driven domain reputation system.
Geotagging: Location metadata attached to posts, useful for event mapping.


NPTEL-Style MCQs (25 Questions)
Conceptual (Easy-Medium)

Why do rumors spread faster than truthful information on social media?
A) Truthful information is always censored
B) Rumors are sensational and create high emotional engagement
C) Algorithms only promote fake news
D) Truthful posts have lower character limits
Correct: B
Which is a major structural difference between Facebook and Twitter?
A) Facebook is unidirectional, Twitter is bidirectional
B) Facebook has bidirectional “friends”, Twitter has unidirectional follower model
C) Only Twitter has an API
D) Facebook does not allow posts
Correct: B
What does “Facebook Inspector (FBI)” primarily do?
A) Delete malicious posts automatically
B) Analyze Facebook posts in real-time and annotate credibility/maliciousness
C) Block all URLs
D) Change user privacy settings
Correct: B
Web of Trust (WOT) is mainly used as a feature to evaluate:
A) User age
B) Reputation of domains/URLs shared in posts
C) Number of friends
D) Post length
Correct: B
The analytical questions emphasized for social media content study are:
A) Only What and When
B) Who, When, Where, What, Why, How
C) Only How and Why
D) Only Where and Who
Correct: B

Application-Oriented (Medium-Hard)

In misinformation detection architecture, the role of supervised learning is to:
A) Collect data from API
B) Classify posts as credible or malicious using trained models
C) Store data in MongoDB
D) Create browser plugins
Correct: B
A spike in the volume of tweets usually indicates:
A) Server downtime
B) Occurrence of a major real-world event
C) Decrease in user activity
D) API rate limit reached
Correct: B
Why are browser plugins like TweetCred and Facebook Inspector useful?
A) They run faster than server-side models
B) They provide real-time annotations directly on the user’s timeline
C) They bypass all privacy settings
D) They replace the need for APIs
Correct: B
Malicious users often exploit events like Boston Marathon because:
A) They can spread malicious URLs to a highly engaged audience
B) Events reduce API rate limits
C) Platforms allow only fake posts during crises
D) Users are offline during events
Correct: A
Geo-tagged tweets are particularly useful for:
A) Increasing follower count
B) Mapping the geographical origin and spread of information
C) Improving image quality
D) Reducing character limit
Correct: B

More MCQs (11-25)

Facebook Inspector uses Facebook ________ to fetch posts.
Answer: Graph API
In Facebook, posts from “friends” are generally perceived as more ________ than random posts.
Answer: Trustworthy / Credible
WOT gives ratings such as Excellent, Good, Satisfactory, Poor, and ________.
Answer: Very Poor
The community of malicious account creators is usually ________ connected.
Answer: Tightly / Closely
TweetCred assigns a credibility score out of ___.
Answer: 7
Feature extraction converts raw social media data into ________ for machine learning models.
Answer: Numerical feature vectors
True/False: The architecture for trust analysis is completely different for Facebook and Twitter. (False)
Which plugin is for Twitter?
A) Facebook Inspector
B) TweetCred
Correct: B
Low confidence score in Facebook Inspector means:
A) The model is very sure it is fake
B) The model lacks enough signals for high-certainty prediction
Correct: B
RESTful API in the architecture is used to:
A) Store data
B) Deliver classification results to the browser plugin
Correct: B