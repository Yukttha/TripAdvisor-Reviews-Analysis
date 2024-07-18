# TripAdvisor-Reviews-Analysis

Project Focus: Text Processing and Representation Analysis
<p>Dataset Source: https://www.kaggle.com/datasets/andrewmvd/trip-advisor-hotel-reviews

<!DOCTYPE html>
<html lang="en">
  
  <head>

  </head>
  
  <body>

  <h3>Libraries</h3>
  <li>Pandas</li>
  <li>Matplotlib</li>
  <li>Wordcloud</li>
  <li>Spacy</li>


  <h3>I. Overview of Dataset</h3>
  <p>The dataset focuses on hotel reviews from TripAdvisor. TripAdvisor operates in the hospitality and tourism industry, where travellers (i.e., users) typically rely on the reviews made on TripAdvisor to book hotels. 

The dataset is stored in a csv file, with two variables: Review and Rating. The dataset consists of 20k reviews. The ‘Review’ variable is a string variable, and the ‘Rating’ variable is an integer variable. These variables are important to be identified and understand what they represent, as they will be used to create the following objectives, which will guide this report.</p>

<h5>Objectives</h5>
<li>To identify how are consumers’ expressions different between high-ranked reviews and low-ranked reviews.</li>
<li>To identify what are the key factors of high-ranked hotels and low-ranked hotels.</li>
<li>To identify why there may be significant differences in high-ranked reviews compared to low-ranked reviews.</li>

  <h3>II. Text Processing & Representation</h3>
  <h5>Text Cleaning</h5>
<p>Text cleaning is done to remove punction, numbers, and special characters that do not hold meaning. This allows to focus on the actual content’s meaning. This procedure also ensures we have consistency across the dataset, which would be useful for the subsequent steps of the analysis.

After the text cleaning process, to fully understand and analyze this dataset, we must subset the dataset in two datasets: 1) High Ranking Rating Reviews and 2) Low Ranking Rating Reviews. This is done to focus on high versus low ratings, due to the reason, that there are a total of 20,491 reviews. The ratings range from 1 to 5. High ranking ratings reviews are defined as ratings with a score of 4 or 5. Whereas, low ranking ratings are defined as ratings with a score of 1 or 2. Below is a table that summarizes the number of reviews made, according to the rating scores. From the table, we found that the low rating score of 1 have the least number of reviews (1,421) and the high rating score of 5 had the highest rating of reviews (9,054). It is important to note that quantitatively, the low-ranking dataset is a smaller dataset (3,214), compared to the high-ranking dataset (15,093). Additionally, a rating of 3 was not categorized in either the low rating or high-ranking dataset, this is due to the nature that the review, may hold neutrality, and may make it difficult in analyzing. Since, we have created two subsets of data, we are now working with 18,307 reviews, as we omitted reviews with a rating of 3.

<table>
  <tr>
    <th>Ratings</th>
    <th>Count</th>
  </tr>
  <tr>
    <td>1</td>
    <td>1,421</td>
  </tr>
  <tr>
    <td>2</td>
    <td>1,793</td>
  </tr>
  <tr>
    <td>3</td>
    <td>2,184</td>
  </tr>
  <tr>
    <td>4</td>
    <td>6,039</td>
  </tr>
  <tr>
    <td>5</td>
    <td>9,054</td>
  </tr>
  <tr>
    <th>Total</th>
    <th>20,491</th>
  </tr>
</table>

To understand why there were a significant difference in higher ratings versus lower rating reviews, external research was done. It was found out that nearly 80% of TripAdvisor users are more likely to book a hotel with a higher rating when choosing between two otherwise identical properties (TripAdvisor, 2019). Therefore, it creates a cyclical cycle, where higher ratings mean more people are likely to book that hotel, and if the individual had a positive experience, then they are more inclined to leave a higher rating. This creates a cycle in which the next user would read that review and be influenced to book at the same hotel. On the other hand, if there are negative reviews, then individuals would more likely avoid booking at the hotel, leading to lower review ratings in total. </p>

<h5>Tokenization</h5>
<p>For the Tokenization process, we have chosen to conduct Word Tokenization, which involves splitting the text into individual words. This would be more useful, compared to doing sentence tokenization, where we would split the text into sentences. 

Word Tokenization can reveal words that have negative or positive sentiments. Below is the summary of the polarity and subjectivity for each dataset: </p>
<table>
  <tr>
    <th></th>
    <th>High Rating Review</th>
    <th>Low Rating Review</th>
  </tr>
  <tr>
    <th>Average Polarity</th>
    <td>~0.34</td>
    <td>~0.03</td>
  </tr>
  <tr>
    <th>Average Subjectivity</th>
    <td>~0.60</td>
    <td>~0.54</td>
  </tr>
</table>

<p>Interestingly, the average polarity for high rating review is approximately 0.34, which is far from 1 (1 being positive). This insight shows that even with high rating reviews of 4 and 5, the average polarity is on the lower side. The average polarity for the low rating reviews is about 0.03, which is close to 0 and it is approaching negative. This makes sense, as the dataset for low ratings contain ratings of 1 and 2. Another reason, maybe is that the low rating dataset is very small when compared to the high rating dataset. If the dataset had been smaller for high rating review, such as focusing on ratings of 5, then the average polarity may have been higher.

The average subjectivity is higher for the high rating dataset, this makes sense as the average polarity was on the lower side. As for the low rating dataset, the average subjectivity was about 0.5, which is somewhat neutral, by placing itself in the middle between 0 (objectivity) and 1 (subjectivity). 

We also conducted the sentiment analyses with VADER (Valence Aware Dictionary and sEntiment Reasoner), which the below table summarizes the results.</p>

<table>
  <tr>
    <th></th>
    <th>High Ranked Reviews</th>
    <th>Low Ranked Reviews</th>
  </tr>
  <tr>
    <th>Negative</th>
    <td>9.3%</td>
    <td>7.2%</td>
  </tr>
  <tr>
    <th>Neutral</th>
    <td>64.6%</td>
    <td>64.3%</td>
  </tr>
  <tr>
    <th>Positive</th>
    <td>26.1%</td>
    <td>28.5%</td>
  </tr>
  <tr>
    <th>Compound</th>
    <td>96.3%</td>
    <td>97.5%</td>
  </tr>
</table>

<p>Based on the results above, high ranked reviews hold more negative sentiment than low ranked reviews, additionally, high ranked reviews are less positive compared to low ranked reviews. What this shows is that both types of reviews hold strong neutrality, with both averaging in the 60% range. Customers are providing balanced reviews, pointing out both positives and areas of improvement.</p>

  <h5>Text Representation</h5>
<p><b>BoW Model</b> was created in representing text data as a collection of word counts. We can represent the collection of words as a graph to visualize the frequency of each word appearance. Based on Figure 6, for high rating review dataset, we found that the top 5 highest frequency words were hotel, room, great, good, and n’t. The top 5 highest frequency words in the low rating review dataset was room, hotel, n’t, stay, and night. This shows that both datasets hold very similar words when it comes to the top 5 highest frequency words.</p>

<p>The <b>TF-IDF</b> measure is used to measure the importance of a word. Based on the high rating reviews dataset, we found that words such as nt, service, and staff had high TF-IDF scores (Figure 8). For low rating review datasets, we found that hotel, room, nt, and staff, had high TF-IDF scores (Figure 9). Interestingly, both show similarity that they contain the same words and have high TF-IDF scores for those words.</p>

<p><b>Word Embeddings</b>
  
Based on the word cloud, the top 10 words were chosen for high rating reviews:
1. Room
2. Hotel
3. Great
4. Nice
5. People
6. Restaurant
7. Resort
8. Day
9. Time
10. Beach

Based on the word cloud, the top 10 words were chosen for low rating reviews:
1.	Day
2.	Time
3.	Room
4.	Hotel
5.	Night
6.	People
7.	Stay
8.	Food
9.	Nice
10.	Service

When you compare the list between high and low rankings, they list of words are very similar to a point where you can not differentiate which words typically belong in the high versus low rating reviews. Due to this, I rendered a second list where the list of words chosen are biased, where some words like ‘nice’ and ‘great’ would be selected for high-ranking reviews, to look at the dataset with filtered lens. We acknowledge that this is more of a biased approach, but this allows us to have deeper and more differentiated analysis, than we were to use the above list of words.

Filtered top 10 words for high rating reviews:
1.	Nice
2.	Loved
3.	Great
4.	Perfect
5.	Amazing
6.	Level
7.	Better
8.	Beautiful
9.	Pretty
10.	Friendly
 
Filtered top 10 words for low rating reviews:
1.	Bad
2.	Problem
3.	Expect
4.	Poor
5.	Pay
6.	Noise
7.	Little
8.	Broken
9.	Dirty
10.	Nothing
 
As you can see from the second list, the list is more differentiated, and it can easily be identified which list of words belongs to high versus low rating reviews.</p>

  <h3>III. Insights & Managerial Implications</h3>
  <p>Hotels should understand the power of reviews left by their customers. If customers left a negative review, then they should seek ways in improving the customer’s experience through the feedback. It is evident that negative ratings scare customers away, which shows why there was a significant difference in low ratings reviews compared to the total number of high rating reviews.

When looking at the top 5 frequency of words for both datasets, there words that belonged in both datasets, and many of those words were nouns, such as hotel, night, and room. We can infer from this that many of the reviews focus on their experience with the hotel, night, and room stay. </p>

<h5>Similarities & Differences Among Low and High Ranked Reviews</h5>
<p>Interestingly, when looking at the word cloud, both word clouds for high and low ranked reviews looked very similar. It was difficult to differentiate between both word clouds, of which dataset it belonged to. However, upon closer examination, when looking at the word cloud, if you look at the words that are smaller in font size, then it creates more differentiation between high and low ranked reviews.</p> 

  <h3>IV. Summary & Conclusion</h3>
<p>From our analysis, we found that there were greater number of high ranked reviews than low ranked reviews. The reason being that high ranked reviews attract more customers to that hotel, creating a cyclical cycle, whereas low ranked reviews typically avoid making bookings. A suggestion for further areas for research is to focus on high ranked reviews with a rating of 5 and low ranked reviews with a rating of 1. In addition, both datasets should be somewhat equal in size, so it reduces inconsistencies when analyzing both datasets simultaneously. Furthermore, the dataset itself, only contained two columns of reviews and ratings, this makes it difficult in understanding the demographic and geographic reviews of the users. Upon further research of the TripAdvisor site, there are various features that contribute to a user’s reviews, this includes property amenities, room features, room types, etc. (Exhibit 5). These details are important to be identified to further understand the review. This may have contributed to the average polarity for high ranked reviews to be on the lower side, because individuals may have had overall positive experience at the hotel, but if the hotel lacked certain amenities or room features, then this would contribute to a less positive review, creating a balanced review of positive and negative sentiment–neutral review.</p>
