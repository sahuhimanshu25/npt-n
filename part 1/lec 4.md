![[Pasted image 20260513204926.png]]![[Pasted image 20260513205330.png]]
![[Pasted image 20260513211008.png]]
![[Pasted image 20260513211114.png]]![[Pasted image 20260513211131.png]]
![[Pasted image 20260513211207.png]]
**Comprehensive Study Notes**

- **0:54 - 3:51: Misinformation Propagation Analysis:** Data from the _Boston Blast_ event shows that rumors peak faster than legitimate news. The study highlights the need to reduce the propagation time of true information and mitigate the spread of false claims.
- **6:16 - 12:05: Methodology & Characterization:** The course adopts a standard data science pipeline: Data Collection (API) -> Characterization -> Ground Truth Generation (human annotation) -> Model Training -> Evaluation. An example case study, _Hurricane Sandy_, utilized 1.7 million tweets, with ground truth annotated by _The Guardian_.
- **13:05 - 15:43: Network Analysis:** Visualizing social networks reveals how information diffuses. The instructor emphasizes that the original source (the root) may not always be the most influential node in the subsequent propagation network.
- **15:44 - 22:30: Classification Features:** Features extracted from social media include:
    - **User Features:** Account age, verification status, friend/follower ratio, and list membership.
    - **Tweet Features:** Length, presence of URLs, question/exclamation marks, and sentiment (emoticons).
    - **Models:** Naive Bayes and Decision Trees are highlighted as effective classification techniques, with Decision Trees achieving high accuracy (~97%).
- **34:33 - 35:16: Evaluation Metrics:** The instructor introduces **NDC G (Normalized Discounted Cumulative Gain)** to measure the quality of rankings/classification and **Cronbach's Alpha** (target > 0.7) to ensure inter-annotator agreement.
- **41:00 - 45:15: TweetCred & Real-time Implementation:** _TweetCred_ is presented as a Chrome browser extension that provides a credibility score (1-7) for tweets in a user's timeline. It uses 45 features, including sentiment (swear words, positive/negative emotion) and URL-based credibility scores (WOT - Web of Trust).

**Key Terminology**

- **Rate Limiting:** A control mechanism to restrict the number of API requests a user can make within a specific timeframe to prevent service abuse.
- **JSON Parsing:** Converting _JavaScript Object Notation_ (the standard data format returned by social media APIs) into usable objects in programming languages like Python.
- **OAuth:** An industry-standard protocol for authorization, allowing users to grant third-party applications access to their social media accounts without sharing passwords.
- **Ground Truth:** The verified, real-world data used to train and test machine learning models (often created via human annotation).
- **Inter-annotator Agreement:** A metric (e.g., Cronbach’s Alpha) used to ensure that different human raters are evaluating data consistently.

**NPTEL-Style MCQs**

1. **Why does the instructor emphasize calculating Cronbach's Alpha during human annotation?** A) To reduce the number of annotators needed. B) To measure the reliability and consistency of human labels. C) To speed up the API collection process. D) To predict the virality of a tweet. _Rationale: B; It ensures that multiple annotators agree on labels like 'credible' vs 'incredible', validating the ground truth._ (33:48-34:22)
    
2. **In the context of the Boston Blast, why is network analysis critical?** A) To see which server the tweet originated from. B) To identify the central influential nodes in information diffusion. C) To increase the tweet length limit. D) To bypass rate limits. _Rationale: B; It reveals that the person who initiates a tweet isn't always the one who drives its viral spread._ (13:05-15:43)
    
3. **Which model is specifically highlighted for achieving ~97% accuracy in identifying fake posts?** A) Neural Networks B) Logistic Regression C) Decision Trees D) Support Vector Machines _Rationale: C; The lecture specifically mentions Decision Trees outperforming other methods in this classification task._ (22:07-22:20)
    
4. **Why is the 'account age' a useful feature for credibility classification?** A) Older accounts are always more accurate. B) It mimics traditional security practices where newer, short-lived domains are often malicious. C) It allows the API to bypass rate limits. D) It is required for the user to be a developer. _Rationale: B; Malicious actors often create 'burner' accounts that lack a historical record._ (19:38-20:05)
    
5. **What is the purpose of NDCG in this research?** A) To count the number of retweets. B) To measure the quality of the classification ranking system. C) To normalize the length of tweets. D) To store data in MySQL. _Rationale: B; NDCG evaluates how well the system ranks items based on their true relevance (credibility)._ (38:47-39:15)
    
6. **How does 'TweetCred' maintain its learning model?** A) It uses external news databases only. B) It accepts user feedback (agree/disagree) to refine the credibility score. C) It automatically deletes fake tweets. D) It blocks accounts that post rumors. _Rationale: B; The demo shows that collecting user feedback directly helps update the model's accuracy._ (42:25-43:05)
    
7. **Why is 'Rate Limiting' a major concern for developers in this course?** A) It slows down Python scripts. B) It prevents unauthorized access. C) APIs restrict how much data you can fetch in a specific window. D) It increases the accuracy of machine learning models. _Rationale: C; API providers impose quotas to prevent excessive usage, forcing developers to manage their data collection rate._ (47:23-47:25)
    
8. **What was the primary difference between 'user features' and 'tweet features' mentioned?** A) User features represent the profile/history; tweet features represent the specific content of the post. B) Tweet features are more accurate than user features. C) User features are stored in JSON; tweet features are not. D) There is no difference. _Rationale: A; This categorization is fundamental to the classification pipeline used in the course._ (16:15-18:00)
    
9. **Why might researchers use 5-fold cross-validation?** A) To handle large JSON files. B) To ensure the classification model's performance is robust and not just lucky on one data subset. C) To increase the speed of the API requests. D) To calculate the sentiment of an emoticon. _Rationale: B; It increases confidence in model results by testing against different data splits._ (21:02-21:15)
    
10. **In the context of the video, why is 'WOT' score used for URLs?** A) To check for spelling errors. B) To determine if the linked site is reputable/trusted. C) To calculate the length of the URL. D) To see if the URL is active. _Rationale: B; The Web of Trust (WOT) score assesses the domain's reputation._ (44:00-44:15)
    

**Verification Check: Outdated Content**

- **API Access (X/Twitter):** The video implies relatively open/free access to Twitter data via APIs. As of 2026, the academic research track has been discontinued. Most large-scale data collection as described in the video is now prohibitively expensive or gated behind high-tier enterprise paid plans.
- **Platform Names:** The video refers to the platform consistently as _Twitter_. It is now _X_.
- **Tooling/Infrastructure:** While Python and MySQL/MongoDB remain standard, the specific API endpoints and authentication flows discussed are likely obsolete due to the platform's transition to a strictly commercialized model.





## **Lecture 5: Detailed Study Notes**

### **1. The Misinformation Lifecycle**

- **Propagation Patterns:** Rumors and fake news often have a "sharper" peak. They spread faster than verified news because they often exploit high-arousal emotions (fear, anger).
    
- **Goal of Analysis:** To minimize the "Lead Time"—the gap between a rumor starting and the truth being propagated.
    

### **2. The Social Media Data Science Pipeline**

To build a system like TweetCred, researchers follow these steps:

1. **Data Collection:** Using APIs (Twitter/X, Facebook).
    
2. **Characterization:** Identifying patterns in the raw data.
    
3. **Ground Truth Generation:** Human annotators label data (e.g., "Credible" or "Not Credible").
    
4. **Feature Extraction:** Converting text and profiles into numbers.
    
5. **Model Training:** Using algorithms like **Decision Trees** or **Naive Bayes**.
    
6. **Evaluation:** Checking accuracy and ranking quality.
    

### **3. Feature Engineering for Credibility**

Researchers split features into distinct categories:

- **User-Based Features:**
    
    - _Account Age:_ New accounts are "riskier" (potential bots).
        
    - _Verification:_ Blue-check status.
        
    - _Follower/Friend Ratio:_ A high number of "following" with zero "followers" is a classic bot sign.
        
- **Tweet-Based Features:**
    
    - _Linguistic:_ Use of exclamation marks (!!!), question marks, or "swear words."
        
    - _Metadata:_ Presence of a URL or an image.
        
    - _Sentiment:_ Positive vs. negative emotion in the text.
        

### **4. Statistical Rigor in Research**

- **Cronbach's Alpha ($\alpha$):** A coefficient used to check **Internal Consistency**. In social media research, if three humans label a tweet, $\alpha > 0.7$ means they agree well enough for the data to be used as "Ground Truth."
    
- **NDCG (Normalized Discounted Cumulative Gain):** A measure of ranking quality. It ensures that the most credible tweets appear at the top of a search result.
    

---

## **NPTEL-Standard MCQ Practice (Set 4)**

**1. Which of the following best describes 'Ground Truth' in the context of rumor detection?**

A. The most retweeted post on a topic.

B. Data that has been verified or labeled by human experts/annotators.

C. The very first tweet ever posted about an event.

D. Data that is automatically generated by the API.

**2. In the credibility classification pipeline, what is the significance of a Decision Tree reaching ~97% accuracy?**

A. It means the model never makes a mistake.

B. It indicates that the extracted features (User + Tweet) are highly discriminative for the task.

C. It suggests the model is too slow for real-time use.

D. It proves that human annotators are no longer needed.

**3. If two human annotators disagree on whether a tweet is a rumor, which metric is used to evaluate their consistency?**

A. NDCG

B. Cronbach's Alpha

C. Root Mean Square Error

D. TF-IDF

**4. Why is the 'Follower-to-Friend' ratio considered a User-based feature?**

A. Because it describes the content of the tweet.

B. Because it describes the social behavior and history of the account holder.

C. Because it is only available for verified users.

D. Because it determines the rate limit of the API.

**5. TweetCred assigns a score from 1 to 7. If a tweet contains many 'Swear Words' and 'Negative Sentiment,' how is its score likely to be affected?**

A. The score will increase toward 7.

B. The score will decrease toward 1.

C. The score will remain unchanged.

D. The score will become a negative number.

**6. What is the primary purpose of the 'Web of Trust' (WOT) score in the TweetCred system?**

A. To measure the speed of the internet connection.

B. To evaluate the reputation and safety of URLs shared within a tweet.

C. To verify the user's home address.

D. To encrypt the tweet content.

**7. In a propagation network, the 'Root Node' represents:**

A. The most influential person in the network.

B. The original source or first person to post the information.

C. The person with the most followers.

D. The last person to retweet the information.

**8. Which of these is a 'Tweet-based' linguistic feature?**

A. The number of lists the user belongs to.

B. The presence of multiple exclamation marks in the post.

C. The date the account was created.

D. The geolocation of the user's profile.

**9. Why do rumors often peak faster than legitimate news in social media analysis?**

A. Rumors are usually longer in length.

B. Legitimate news sources are always blocked by APIs.

C. Rumors often utilize emotional triggers that encourage rapid sharing.

D. Legitimate news is only posted in JSON format.

**10. What does NDCG primarily evaluate in a credibility system?**

A. The speed of data collection.

B. The effectiveness of the system in ranking highly credible information at the top.

C. The total number of users in the social graph.

D. The amount of storage space used by MySQL.