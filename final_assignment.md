# Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.

# Part 1: Yelp Dataset Profiling and Understanding

## 1. Profile the data by finding the total number of records for each of the tables below:

```SQL
-- Example for one table
SELECT COUNT (*)
FROM Attribute
-- Manually replace the table name Attribute to others like Business
```

- i. Attribute table = 10000
- ii. Business table = 10000
- iii. Category table = 10000
- iv. Checkin table = 10000
- v. elite_years table = 10000
- vi. friend table = 10000
- vii. hours table = 10000
- viii. photo table = 10000
- ix. review table = 10000
- x. tip table = 10000
- xi. user table = 10000

## 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

```SQL
SELECT COUNT(DISTINCT(id))
FROM Business
```

- i. Business = 10000 for primary key `id`
- ii. Hours = 1562
- iii. Category = 2643
- iv. Attribute = 1115
- v. Review = 10000 for primary key `id`, 8090 for `business_id`, 9581 for `user_id`
- vi. Checkin = 493
- vii. Photo = 10000 for primary key `id`, 6493 for `business_id`
- viii. Tip = 3979 for `business_id`, 537 for `user_id`
- ix. User = 10000 for primary key `id`
- x. Friend = 11 for `user_id`
- xi. Elite_years = 2780 for `user_id`

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.

## 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

Answer: no

SQL code used to arrive at answer:

```SQL
SELECT COUNT (*)
FROM user
WHERE id IS NULL
OR name IS NULL
OR review_count IS NULL
OR yelping_since IS NULL
OR useful IS NULL
OR funny IS NULL
OR cool IS NULL
OR fans IS NULL
OR average_stars IS NULL
OR compliment_hot IS NULL
OR compliment_more IS NULL
OR compliment_profile IS NULL
OR compliment_cute IS NULL
OR compliment_list IS NULL
OR compliment_note IS NULL
OR compliment_plain IS NULL
OR compliment_cool IS NULL
OR compliment_funny IS NULL
OR compliment_writer IS NULL
OR compliment_photos IS NULL
```

## 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

i. Table: Review, Column: Stars

    min: 1		max: 5		avg: 3.7082

ii. Table: Business, Column: Stars

    min: 1 		max: 5		avg: 3.6549

iii. Table: Tip, Column: Likes

    min: 0		max: 2		avg: 0.0144

iv. Table: Checkin, Column: Count

    min: 1		max: 53		avg: 1.9414

v. Table: User, Column: Review_count

    min: 0		max: 2000		avg: 24.2995

## 5. List the cities with the most reviews in descending order:

SQL code used to arrive at answer:

```SQL
SELECT SUM(review_count) as num_reviews, city
FROM business
GROUP BY city
ORDER BY num_reviews DESC
```

Copy and Paste the Result Below:

```
+-------------+-----------------+
| num_reviews | city            |
+-------------+-----------------+
|       82854 | Las Vegas       |
|       34503 | Phoenix         |
|       24113 | Toronto         |
|       20614 | Scottsdale      |
|       12523 | Charlotte       |
|       10871 | Henderson       |
|       10504 | Tempe           |
|        9798 | Pittsburgh      |
|        9448 | Montréal        |
|        8112 | Chandler        |
|        6875 | Mesa            |
|        6380 | Gilbert         |
|        5593 | Cleveland       |
|        5265 | Madison         |
|        4406 | Glendale        |
|        3814 | Mississauga     |
|        2792 | Edinburgh       |
|        2624 | Peoria          |
|        2438 | North Las Vegas |
|        2352 | Markham         |
|        2029 | Champaign       |
|        1849 | Stuttgart       |
|        1520 | Surprise        |
|        1465 | Lakewood        |
|        1155 | Goodyear        |
+-------------+-----------------+
(Output limit exceeded, 25 of 362 total rows shown)
```

## 6. Find the distribution of star ratings to the business in the following cities:

Avon has 10 businesses and Beachwood has 14 businesses, so a similar amount. However, Beachwood has five 5-star-rated businesses, while Avon has only one.

### i. Avon

SQL code used to arrive at answer:

```SQL
SELECT stars AS star_rating, COUNT(stars) as count
FROM business
WHERE city="Avon"
GROUP BY star_rating
```

Copy and Paste the Resulting Table Below (2 columns – star rating and count):

```
+-------------+-------+
| star_rating | count |
+-------------+-------+
|         1.5 |     1 |
|         2.5 |     2 |
|         3.5 |     3 |
|         4.0 |     2 |
|         4.5 |     1 |
|         5.0 |     1 |
+-------------+-------+
```

ii. Beachwood

SQL code used to arrive at answer:

```SQL
SELECT stars AS star_rating, COUNT(stars) as count
FROM business
WHERE city="Beachwood"
GROUP BY star_rating
```

Copy and Paste the Resulting Table Below (2 columns – star rating and count):

```
+-------------+-------+
| star_rating | count |
+-------------+-------+
|         2.0 |     1 |
|         2.5 |     1 |
|         3.0 |     2 |
|         3.5 |     2 |
|         4.0 |     1 |
|         4.5 |     2 |
|         5.0 |     5 |
+-------------+-------+
```

## 7. Find the top 3 users based on their total number of reviews:

SQL code used to arrive at answer:

```SQL
SELECT review_count, name, id
FROM user
ORDER BY review_count DESC
LIMIT 3
```

Copy and Paste the Result Below:

```
+--------------+--------+------------------------+
| review_count | name   | id                     |
+--------------+--------+------------------------+
|         2000 | Gerald | -G7Zkl1wIWBBmD0KRy_sCw |
|         1629 | Sara   | -3s52C4zL_DHRK0ULG6qtg |
|         1339 | Yuri   | -8lbUNlXVSoXqaRRiHiSNg |
+--------------+--------+------------------------+
```

## 8. Does posing more reviews correlate with more fans?

Please explain your findings and interpretation of the results:

```SQL
SELECT review_count, name, id, fans
FROM user
ORDER BY review_count DESC -- also try ASC and sort by fans
```

```
+--------------+-----------+------------------------+------+
| review_count | name      | id                     | fans |
+--------------+-----------+------------------------+------+
|         2000 | Gerald    | -G7Zkl1wIWBBmD0KRy_sCw |  253 |
|         1629 | Sara      | -3s52C4zL_DHRK0ULG6qtg |   50 |
|         1339 | Yuri      | -8lbUNlXVSoXqaRRiHiSNg |   76 |
|         1246 | .Hon      | -K2Tcgh2EKX6e6HqqIrBIQ |  101 |
|         1215 | William   | -FZBTkAZEXoP7CYvRV2ZwQ |  126 |
|         1153 | Harald    | --2vR0DIsmQ6WfcSzKWigw |  311 |
|         1116 | eric      | -gokwePdbXjfS0iF7NsUGA |   16 |
|         1039 | Roanna    | -DFCC64NXgqrxlO8aLU5rg |  104 |
|          968 | Mimi      | -8EnCioUmDygAbsYZmTeRQ |  497 |
|          930 | Christine | -0IiMAZI2SsQ7VmyzJjokQ |  173 |
|          904 | Ed        | -fUARDNuXAfrOn4WLSZLgA |   38 |
|          864 | Nicole    | -hKniZN2OdshWLHYuj21jQ |   43 |
|          862 | Fran      | -9da1xk7zgnnfO1uTVYGkA |  124 |
|          861 | Mark      | -B-QEUESGWHPE_889WJaeg |  115 |
|          842 | Christina | -kLVfaJytOJY2-QdQoCcNQ |   85 |
|          836 | Dominic   | -kO6984fXByyZm3_6z2JYg |   37 |
|          834 | Lissa     | -lh59ko3dxChBSZ9U7LfUw |  120 |
|          813 | Lisa      | -g3XIcCb2b-BD0QBCcq2Sw |  159 |
|          775 | Alison    | -l9giG8TSDBG1jnUBUXp5w |   61 |
|          754 | Sui       | -dw8f7FLaUmWR7bfJ_Yf0w |   78 |
|          702 | Tim       | -AaBjWJYiQxXkCMDlXfPGw |   35 |
|          696 | L         | -jt1ACMiZljnBFvS6RRvnA |   10 |
|          694 | Angela    | -IgKkE8JvYNWeGu8ze4P8Q |  101 |
|          676 | Crissy    | -hxUwfo3cMnLTv-CAaP69A |   25 |
|          675 | Lyn       | -H6cTbVxeIRYR-atxdielQ |   45 |
+--------------+-----------+------------------------+------+
(Output limit exceeded, 25 of 10000 total rows shown)

+--------------+-----------+------------------------+------+
| review_count | name      | id                     | fans |
+--------------+-----------+------------------------+------+
|          609 | Amy       | -9I98YbNQnLdAmcYfb324Q |  503 |
|          968 | Mimi      | -8EnCioUmDygAbsYZmTeRQ |  497 |
|         1153 | Harald    | --2vR0DIsmQ6WfcSzKWigw |  311 |
|         2000 | Gerald    | -G7Zkl1wIWBBmD0KRy_sCw |  253 |
|          930 | Christine | -0IiMAZI2SsQ7VmyzJjokQ |  173 |
|          813 | Lisa      | -g3XIcCb2b-BD0QBCcq2Sw |  159 |
|          377 | Cat       | -9bbDysuiWeo2VShFJJtcw |  133 |
|         1215 | William   | -FZBTkAZEXoP7CYvRV2ZwQ |  126 |
|          862 | Fran      | -9da1xk7zgnnfO1uTVYGkA |  124 |
|          834 | Lissa     | -lh59ko3dxChBSZ9U7LfUw |  120 |
|          861 | Mark      | -B-QEUESGWHPE_889WJaeg |  115 |
|          408 | Tiffany   | -DmqnhW4Omr3YhmnigaqHg |  111 |
|          255 | bernice   | -cv9PPT7IHux7XUc9dOpkg |  105 |
|         1039 | Roanna    | -DFCC64NXgqrxlO8aLU5rg |  104 |
|          694 | Angela    | -IgKkE8JvYNWeGu8ze4P8Q |  101 |
|         1246 | .Hon      | -K2Tcgh2EKX6e6HqqIrBIQ |  101 |
|          307 | Ben       | -4viTt9UC44lWCFJwleMNQ |   96 |
|          584 | Linda     | -3i9bhfvrM3F1wsC9XIB8g |   89 |
|          842 | Christina | -kLVfaJytOJY2-QdQoCcNQ |   85 |
|          220 | Jessica   | -ePh4Prox7ZXnEBNGKyUEA |   84 |
|          408 | Greg      | -4BEUkLvHQntN6qPfKJP2w |   81 |
|          178 | Nieves    | -C-l8EHSLXtZZVfUAUhsPA |   80 |
|          754 | Sui       | -dw8f7FLaUmWR7bfJ_Yf0w |   78 |
|         1339 | Yuri      | -8lbUNlXVSoXqaRRiHiSNg |   76 |
|          161 | Nicole    | -0zEEaDFIjABtPQni0XlHA |   73 |
+--------------+-----------+------------------------+------+
(Output limit exceeded, 25 of 10000 total rows shown)
```

The 25 users with the most reviews have 10-497 fans. The 25 users with the least reviews have 0 fans. So there is some kind of correlation, but to quantify it, we would need to perform some kind of regression.

## 9. Are there more reviews with the word "love" or with the word "hate" in them?

Answer:

- 1780 reviews contain the word "love"
- 232 reviews contain the word "hate"

SQL code used to arrive at answer:

```SQL
SELECT COUNT(id)
FROM review
WHERE text LIKE '%love%' -- switch with hate
```

## 10. Find the top 10 users with the most fans:

SQL code used to arrive at answer:

```SQL
SELECT fans, name, id
FROM user
ORDER BY fans DESC
LIMIT 10
```

Copy and Paste the Result Below:

```
+------+-----------+------------------------+
| fans | name      | id                     |
+------+-----------+------------------------+
|  503 | Amy       | -9I98YbNQnLdAmcYfb324Q |
|  497 | Mimi      | -8EnCioUmDygAbsYZmTeRQ |
|  311 | Harald    | --2vR0DIsmQ6WfcSzKWigw |
|  253 | Gerald    | -G7Zkl1wIWBBmD0KRy_sCw |
|  173 | Christine | -0IiMAZI2SsQ7VmyzJjokQ |
|  159 | Lisa      | -g3XIcCb2b-BD0QBCcq2Sw |
|  133 | Cat       | -9bbDysuiWeo2VShFJJtcw |
|  126 | William   | -FZBTkAZEXoP7CYvRV2ZwQ |
|  124 | Fran      | -9da1xk7zgnnfO1uTVYGkA |
|  120 | Lissa     | -lh59ko3dxChBSZ9U7LfUw |
+------+-----------+------------------------+
```

# Part 2: Inferences and Analysis

## 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

- Chosen city: Las Vegas because has most reviews, see above
- Chosen category: Restaurants, because have most reviews in Las Vegas (namely 4, tied with Health & Medical and Shopping) as well as most reviews from all cities (namely 71).

```SQL
SELECT COUNT(c.category) AS cnt, c.category
FROM business b
LEFT JOIN category c ON c.business_id=b.id
WHERE b.city="Las Vegas" -- optional
GROUP BY c.category
ORDER BY cnt DESC
```

i. Do the two groups you chose to analyze have a different distribution of hours?

The hours are only specified for three out of the four restaurants. The hours aren't that much different and it is difficult to draw a conclusion based on that sample size.

```SQL
SELECT b.name, b.stars, c.category, h.hours
FROM business b
LEFT JOIN category c ON c.business_id=b.id
LEFT JOIN hours h on h.business_id=b.id
WHERE b.city="Las Vegas"
AND c.category="Restaurants"
```

```
+---------------------+-------+-------------+-----------------------+
| name                | stars | category    | hours                 |
+---------------------+-------+-------------+-----------------------+
| Jacques Cafe        |   4.0 | Restaurants | Monday|11:00-20:00    |
| Jacques Cafe        |   4.0 | Restaurants | Tuesday|11:00-20:00   |
| Jacques Cafe        |   4.0 | Restaurants | Friday|11:00-20:00    |
| Jacques Cafe        |   4.0 | Restaurants | Wednesday|11:00-20:00 |
| Jacques Cafe        |   4.0 | Restaurants | Thursday|11:00-20:00  |
| Jacques Cafe        |   4.0 | Restaurants | Sunday|8:00-14:00     |
| Jacques Cafe        |   4.0 | Restaurants | Saturday|11:00-20:00  |
| Wingstop            |   3.0 | Restaurants | Monday|11:00-0:00     |
| Wingstop            |   3.0 | Restaurants | Tuesday|11:00-0:00    |
| Wingstop            |   3.0 | Restaurants | Friday|11:00-0:00     |
| Wingstop            |   3.0 | Restaurants | Wednesday|11:00-0:00  |
| Wingstop            |   3.0 | Restaurants | Thursday|11:00-0:00   |
| Wingstop            |   3.0 | Restaurants | Sunday|11:00-0:00     |
| Wingstop            |   3.0 | Restaurants | Saturday|11:00-0:00   |
| Big Wong Restaurant |   4.0 | Restaurants | Monday|10:00-23:00    |
| Big Wong Restaurant |   4.0 | Restaurants | Tuesday|10:00-23:00   |
| Big Wong Restaurant |   4.0 | Restaurants | Friday|10:00-23:00    |
| Big Wong Restaurant |   4.0 | Restaurants | Wednesday|10:00-23:00 |
| Big Wong Restaurant |   4.0 | Restaurants | Thursday|10:00-23:00  |
| Big Wong Restaurant |   4.0 | Restaurants | Sunday|10:00-23:00    |
| Big Wong Restaurant |   4.0 | Restaurants | Saturday|10:00-23:00  |
| Hibachi-San         |   4.5 | Restaurants | None                  |
+---------------------+-------+-------------+-----------------------+
```

ii. Do the two groups you chose to analyze have a different number of reviews?

Restaurant "Hibachi-San", which is rated the highest with 4.5 stars, has significantly fewer reviews than the other restaurants.

```SQL
SELECT b.name, b.stars, c.category, b.review_count, b.postal_code, b.is_open
FROM business b
LEFT JOIN category c ON c.business_id=b.id
WHERE b.city="Las Vegas"
AND c.category="Restaurants"
```

```
+---------------------+-------+-------------+--------------+-------------+---------+
| name                | stars | category    | review_count | postal_code | is_open |
+---------------------+-------+-------------+--------------+-------------+---------+
| Jacques Cafe        |   4.0 | Restaurants |          168 | 89134       |       0 |
| Wingstop            |   3.0 | Restaurants |          123 | 89103       |       1 |
| Big Wong Restaurant |   4.0 | Restaurants |          768 | 89146       |       1 |
| Hibachi-San         |   4.5 | Restaurants |            3 | 89169       |       0 |
+---------------------+-------+-------------+--------------+-------------+---------+
```

iii. Are you able to infer anything from the location data provided between these two groups? Explain.

Looking at the postal code and using google maps, Jacques Café lies at the edge of Las Vegas, while the other Restaurants are rather central.

SQL code used for analysis: See above

## 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.

i. Difference 1:
The restaurant with the least amount of reviews (3), is closed.
The restaurant with the most amount of reviews (768) is open.

ii. Difference 2:
The restaurant at the edge of the city (Jacques Cafe) is closed.

SQL code used for analysis: see above

## 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:

### i. Indicate the type of analysis you chose to do:

First I wanted to analyze the reviews of users. Questions such as

- Are there users who typically give bad reviews?
- Are there users who review restaurants more than once?
- Do users typically review only once city?
- Do users have friends in the same city or from all over?

However, due the limited tables, the intersection between users and reviews is very low: We can only link 72 of all 10,000 reviews to 69 users. Not much of an analysis here... Likewise, we can only link 62 of the tips to 4 users.

However, there is a decent linkage between businesses and tips: We can link 677 tips to 254 businesses. Also, the tips are from 537 distinct users (although we can only link 4 of them to the user table as mentioned above). So let's analyze the tips table.

### ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

see above

### iii. Output of your finished dataset:

#### What do the tips text contain?

- 382 for Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday
- 59 for `reserv`
- 227 for `park`
- breakfast, lunch, dinner
  - 117 for breakfast
  - 273 for lunch
  - 139 for dinner
- price
  - 49 for expensive
  - 57 for cheap
- 2542 for good, love, great, fantastic, awesome, amazing, delicious, tasty
- 178 bad, hate, poor, terrible, disgust, `not recommend`,
- 324 try

```SQL
SELECT COUNT(*)
FROM tip
WHERE text LIKE '%bad%'
OR text LIKE '%hate%'
OR text LIKE '%poor%'
OR text LIKE '%terrible%'
OR text LIKE '%disgust%'
OR text LIKE '%not recommend%'
ORDER BY business_id ASC
```

#### Are tips for weekdays entered on those weekdays?

Tips containing the text Monday are mostly submitted on Mondays. The same is true for any other weekday.

```
Example output for Monday:
+-----------+----------+
| weekday   | COUNT(*) |
+-----------+----------+
| Friday    |        5 |
| Monday    |       30 |
| Saturday  |        4 |
| Sunday    |        5 |
| Thursday  |        2 |
| Tuesday   |        7 |
| Wednesday |        7 |
+-----------+----------+
```

```SQL
-- https://www.sqlitetutorial.net/sqlite-date-functions/sqlite-strftime-function/
SELECT CASE STRFTIME('%w', date)
WHEN '0' THEN 'Sunday'
WHEN '1' THEN 'Monday'
WHEN '2' THEN 'Tuesday'
WHEN '3' THEN 'Wednesday'
WHEN '4' THEN 'Thursday'
WHEN '5' THEN 'Friday'
WHEN '6' THEN 'Saturday'
ELSE 'error'
END weekday
, COUNT(*)
FROM tip
WHERE TEXT LIKE '%Monday%'
GROUP BY weekday
```

#### Which tips get the most likes?

The tip with the most likes has only two likes - I expected much more. Difficult to draw conclusions based on that. However, the number of likes definitely correlates with the text length:

- for text lenght < 25: 0.004
- for text lenght < 50: 0.006
- for text lenght < 100: 0.009
- for text lenght > 100: 0.036
- for text lenght > 200: 0.066

```SQL
SELECT AVG(likes), AVG(LENGTH(text)),COUNT(*)
from tip
WHERE LENGTH(text)>200
```

#### Tips and users: Do some users tend to give only positive / bad reviews?

In the following we will only consider the 46 users with at least 50 reviews.

About 20 of those users have never submitted a negative tip, but up to 40 positive ones. Similarly, five users have only submitted one negative tip, but up to 80 positive ones. In summary, they have submitted 20x more positive tips than negative ones.

On the flipside, even the most critical user has submitted 1.5x more positive than negative reviews (namely 6 vs 4). There are only four users who have submitted less than 5x as many positive reviews than negative ones. The world is good - at least the tips seem to be.

```
+------------------------+-------------+-------------+-------------+---------------+
| user_id                | num_reviews | is_positive | is_negative |         ratio |
+------------------------+-------------+-------------+-------------+---------------+
| eXC9pqaD21oSet31ZeRG_A |         114 |          40 |           0 |        4000.0 |
| vzAojVzcALJVBXjHOGgeiA |         129 |          32 |           0 |        3200.0 |
| PuCMCx8LvgUWgZhnt2PHJg |          99 |          29 |           0 |        2900.0 |
| fmzIm7RxEdii5Jz44PtO7g |         338 |          28 |           0 |        2800.0 |
| BjtJ3VkMOxV2Lan037AFuw |         186 |          23 |           0 |        2300.0 |
| yqa2qWN6acpmDuDL3U61UA |          67 |          21 |           0 |        2100.0 |
| mm9WYrFhiNqvHCyhQKw3Mg |          53 |          20 |           0 |        2000.0 |
| 5JVY32_bmTBfIGpCCsnAfw |          75 |          18 |           0 |        1800.0 |
| _7zgzdB1Qog-HUWQdbH0pw |          52 |          16 |           0 |        1600.0 |
| H5d_nFqzwrREE-YduK2ABg |          53 |          15 |           0 |        1500.0 |
| KqItBIJXO_UhZ6MktvuI0Q |          52 |          13 |           0 |        1300.0 |
| ca___2Qaf5FFyPCf6T2eZA |          97 |          13 |           0 |        1300.0 |
| PZNMPWCViVX8JLsn10MSnQ |          87 |          11 |           0 |        1100.0 |
| -0x2ov-qcCopv32Imm-TYg |          56 |           9 |           0 |         900.0 |
| Xe-Dlatnkz9A9l8oyDgU9Q |          79 |           7 |           0 |         700.0 |
| UyXqGEKod-veD6m6Hq0EDw |          82 |           5 |           0 |         500.0 |
| JE2qFjL4BaUbiI-cT5MSBw |          86 |           2 |           0 |         200.0 |
| dYEHTYJeDJ4v8AUiExaVsw |          51 |           1 |           0 |         100.0 |
| PAeEkjrXTub0ENa4rZiWvA |         260 |          82 |           1 | 81.1881188119 |
| 2IweYEr1K6vWxx428zZoVg |          98 |          36 |           1 | 35.6435643564 |
| _4Wwqc9CcI8jBPzfxyg6kw |         120 |          34 |           1 | 33.6633663366 |
| rp007n5XVLGJwIOTh9U0-g |         101 |          32 |           1 | 31.6831683168 |
| blrWvPePSv87aU9hV1Zd8Q |         232 |          29 |           1 | 28.7128712871 |
| jlpapIPWURjBUg3V31AjKw |         119 |          24 |           1 | 23.7623762376 |
| 4yG4J05aKzE2zov0Jr37kg |         134 |          45 |           2 | 22.3880597015 |
+------------------------+-------------+-------------+-------------+---------------+
(Output limit exceeded, 25 of 46 total rows shown)

+------------------------+-------------+-------------+-------------+---------------+
| user_id                | num_reviews | is_positive | is_negative |         ratio |
+------------------------+-------------+-------------+-------------+---------------+
| A0Tkq4VV8dD6t8NbBxvBPA |          66 |           6 |           4 | 1.49625935162 |
| uVDJlnPJNx07_jDqI4jgYA |          77 |          17 |           6 | 2.82861896839 |
| CbmNBkKa9QKNxPiN_whFUw |         189 |           8 |           2 | 3.98009950249 |
| QQtoHnP0cP7nzNnUob_1CQ |          78 |          33 |           7 | 4.70756062767 |
| B_4cl4IGRqYb0wQSe-rYjQ |         144 |          26 |           5 | 5.18962075848 |
| benfF2qIwxDz7TCeF1XWIA |         455 |          26 |           5 | 5.18962075848 |
| voTmwjTzaKSq3a9Eiwy3DQ |          97 |          22 |           4 | 5.48628428928 |
| wrUYC0wc987XBBAoskOCHA |         465 |          68 |          12 | 5.66194837635 |
| UsmTxWbobLsI6WR1Db0W7A |         475 |          71 |          11 | 6.44868301544 |
| P3B7FfBpXERa-KdxwIGkHA |          67 |          20 |           3 | 6.64451827243 |
| GMKoemATfrXg1deaXxt2jA |          56 |          15 |           2 | 7.46268656716 |
| M9TjYmTgHayJ22cNkyvW_g |         319 |          82 |           9 | 9.10099889012 |
| 135DbbQnr3BEkQbBzZ9T1A |         365 |          80 |           8 | 9.98751560549 |
| NAZzgDkNIL_DpHg6xu9APQ |         164 |          83 |           7 | 11.8402282454 |
| vI7X_PYnUc5cjd-iPbhARA |         227 |          63 |           5 | 12.5748502994 |
| QYKexxaOJQlseGWmc6soRg |          89 |          14 |           1 | 13.8613861386 |
| nOcP-0PIg4REFX4JeR49aw |         122 |          28 |           2 | 13.9303482587 |
| bDqi-ueISUIJ-Au40_KVnw |         112 |          15 |           1 | 14.8514851485 |
| 1W3_JUSkH5tsrIWdIXoK-w |         214 |          36 |           2 | 17.9104477612 |
| NxtYkOpXHSy7LWRKJf3z0w |          93 |          19 |           1 | 18.8118811881 |
| 3z1EttCePzDn9OZbudD5VA |         101 |          21 |           1 | 20.7920792079 |
| 4yG4J05aKzE2zov0Jr37kg |         134 |          45 |           2 | 22.3880597015 |
| jlpapIPWURjBUg3V31AjKw |         119 |          24 |           1 | 23.7623762376 |
| blrWvPePSv87aU9hV1Zd8Q |         232 |          29 |           1 | 28.7128712871 |
| rp007n5XVLGJwIOTh9U0-g |         101 |          32 |           1 | 31.6831683168 |
+------------------------+-------------+-------------+-------------+---------------+
(Output limit exceeded, 25 of 46 total rows shown)
```

```SQL
-- Creating views is not supported in the coursera interface :/. A complex SQL statement follows...
SELECT t.user_id, num_reviews

, COUNT(CASE
WHEN text LIKE '%good%' THEN 1
WHEN text LIKE '%love%' THEN 1
WHEN text LIKE '%great%' THEN 1
WHEN text LIKE '%love%' THEN 1
WHEN text LIKE '%fantastic%' THEN 1
WHEN text LIKE '%awesome%' THEN 1
WHEN text LIKE '%amazing%' THEN 1
WHEN text LIKE '%delicious%' THEN 1
WHEN text LIKE '%tasty%' THEN 1
END) AS is_positive

, COUNT(CASE
WHEN text LIKE '%bad%' THEN 1
WHEN text LIKE '%hate%' THEN 1
WHEN text LIKE '%poor%' THEN 1
WHEN text LIKE '%terrible%' THEN 1
WHEN text LIKE '%disgust%' THEN 1
WHEN text LIKE '%not recommend%' THEN 1
WHEN text LIKE '%stay away%' THEN 1
END) AS is_negative

,( COUNT(CASE
WHEN text LIKE '%good%' THEN 1
WHEN text LIKE '%love%' THEN 1
WHEN text LIKE '%great%' THEN 1
WHEN text LIKE '%love%' THEN 1
WHEN text LIKE '%fantastic%' THEN 1
WHEN text LIKE '%awesome%' THEN 1
WHEN text LIKE '%amazing%' THEN 1
WHEN text LIKE '%delicious%' THEN 1
WHEN text LIKE '%tasty%' THEN 1
END))
/
(COUNT(CASE
WHEN text LIKE '%bad%' THEN 1
WHEN text LIKE '%hate%' THEN 1
WHEN text LIKE '%poor%' THEN 1
WHEN text LIKE '%terrible%' THEN 1
WHEN text LIKE '%disgust%' THEN 1
WHEN text LIKE '%not recommend%' THEN 1
WHEN text LIKE '%stay away%' THEN 1
END)+0.01) AS ratio

FROM tip t

LEFT JOIN (
  SELECT user_id, COUNT(text) AS num_reviews
  FROM tip
  GROUP BY user_id
  ) AS a ON a.user_id=t.user_id

WHERE num_reviews>=50

GROUP BY t.user_id

ORDER BY ratio DESC -- also check ASC
```

#### Tips and businesses: Which business receive the most tips? Does it correlate with the city or state?

We can link 677 tips to the `business` table using `INNER JOIN`. Among those tips, 58% (396) refer to business in Pittsburgh. The city with the second highest tips only has 23 tips, so Pittsburgh stands out. Moreover, 85% of the tips are linked to businesses in the PA state.

```
+-------+-----+
| state | cnt |
+-------+-----+
| PA    | 579 |
| AZ    |  50 |
| OH    |  26 |
| NV    |  18 |
| NC    |   2 |
| ON    |   1 |
| QC    |   1 |
+-------+-----+

+------------------+-----+
| city             | cnt |
+------------------+-----+
| Pittsburgh       | 396 |
| Homestead        |  23 |
| Las Vegas        |  18 |
| Oakmont          |  17 |
| Tempe            |  16 |
| Bethel Park      |  15 |
| Phoenix          |  14 |
| Bridgeville      |  13 |
| Moon Township    |  13 |
| West Mifflin     |  13 |
| Coraopolis       |  12 |
| Scottsdale       |  12 |
| Wilkinsburg      |  11 |
| Canonsburg       |   9 |
| Monroeville      |   8 |
| Gibsonia         |   7 |
| Murrysville      |   7 |
| Dormont          |   6 |
| Independence     |   5 |
| McMurray         |   5 |
| Chagrin Falls    |   4 |
| Chandler         |   4 |
| Mount Lebanon    |   4 |
| Woodmere Village |   4 |
| Carnegie         |   3 |
+------------------+-----+
(Output limit exceeded, 25 of 54 total rows shown)
```

```SQL
SELECT b.state, COUNT(t.text) as cnt
FROM tip t
INNER JOIN business b ON b.id=t.business_id
GROUP BY b.state
ORDER BY cnt DESC
-- also switch b.state with b.city
```

#### Tips and businesses: Does the tip count correlate with the review count?

There seems to be a slight correlation between tip count and review count. Business with more than 5 tips have typically aso received at least 10 reviews, half of them even 100 reviews. However, there is one business who has received 8 tips but only 6 reviews. On the other side, among the businesses with more than 234 reviews, about half of them have only received one tip.

```SQL
SELECT b.id, c.category, b.review_count, COUNT(t.text) as tip_count
FROM tip t
INNER JOIN business b ON b.id=t.business_id
LEFT JOIN category c ON c.business_id=b.id
GROUP BY b.id
ORDER BY review_count DESC -- also sort by tip_count
```

```
+------------------------+------------+--------------+-----------+
| id                     | category   | review_count | tip_count |
+------------------------+------------+--------------+-----------+
| 1GaooxqCWHzulI2Ub3CXEw | Mexican    |          103 |        51 |
| 08t3_HjbpLyPeuft6eoa5A | None       |          118 |        36 |
| 0PVxodALQu-soL5J8bjerQ | None       |          182 |        21 |
| -igpUhnA1b5iUK6rfAtuPw | None       |          197 |        17 |
| 01I5pFCvJrrGuY3A-KoNIA | None       |           39 |        17 |
| 1hqOjPxgH8IXE4bNq6DFiw | None       |           80 |        13 |
| 0kyhbUW6NkpYjJzFBZ64vQ | Sandwiches |           91 |        12 |
| 1Z4_zSITNVQ_Bt027R0S1g | None       |          126 |        11 |
| 1ZDGpyCKBX-VvuO0Vl2tww | None       |           31 |        11 |
| 0PCBt3JKD6IooicImKNBzA | None       |          429 |        10 |
| 04kZ5CSh6oKhI5huU5bLdg | None       |          242 |         9 |
| 28exW1xiocTHiJIkVY2A9g | None       |          158 |         9 |
| -7H-oXvCxJzuT42ky6Db0g | None       |          436 |         8 |
| 1cGyzWtfOoDiE8V0OR85yA | None       |          124 |         8 |
| 1d-gQ3bl4jy6CH6tpIM6ZQ | None       |            6 |         8 |
| 1dYpffQi3qdh-dkXF4LZBw | None       |          239 |         8 |
| 1oxMj71XiKQjCbRxECzB7w | None       |           89 |         8 |
| 1uvcySLWM75MzlLM12F8dA | None       |          165 |         8 |
| 22u7wqu4vRRDi2zXw_dTRQ | None       |           81 |         8 |
| 1LUaZFVMEjodl1tbAGF3sQ | None       |           55 |         7 |
| 1eJ7yIzSAjwC145fnHD5Xw | None       |           22 |         7 |
| 2eVpkjDioFSgp2C27mSdHQ | None       |           15 |         7 |
| -HeqTxBMPTi3A7QuU5PvgQ | None       |           98 |         6 |
| -httBl6DSZiUtDX4SQWtag | None       |          142 |         6 |
| 0IhSOm9Vm1JkvRO6XyElGg | None       |            9 |         6 |
+------------------------+------------+--------------+-----------+
(Output limit exceeded, 25 of 254 total rows shown)

+------------------------+----------+--------------+-----------+
| id                     | category | review_count | tip_count |
+------------------------+----------+--------------+-----------+
| 0W4lkclzZThpx3V65bVgig |     None |         1757 |         1 |
| 0FUtlsQrJI7LhqDPxLumEw |     None |         1549 |         1 |
| 2iTsRqUsPGRH1li1WVRvKQ |     None |         1410 |         1 |
| -050d_XIor1NpCuWkbIVaQ |     None |          700 |         1 |
| -rhH9sL3XGFpoJXcxUpEWA |     None |          667 |         1 |
| -sAr-LA9TsIdl37UjwBlvg |     None |          534 |         1 |
| 0WoQQlMXVIDEgI0xNdENKA |     None |          503 |         1 |
| 1CR2ddUcjYYwRd5JLtiRrw |     None |          485 |         1 |
| -7H-oXvCxJzuT42ky6Db0g |     None |          436 |         8 |
| 0PCBt3JKD6IooicImKNBzA |     None |          429 |        10 |
| -Dnh48f029YNugtMKkkI-Q |     None |          424 |         1 |
| -6h3K1hj0d4DRcZNUtHDuw |     None |          422 |         1 |
| 2IvrdAb6zdxr3ZqplqJHbg |     None |          414 |         1 |
| -bMZCfTK7fxFaURynKpBMA |     None |          400 |         1 |
| 16Fplxu-OwVmTEFxQAUP4g |     None |          385 |         1 |
| 2aoKv8DjAeVBjTT9O9sx5g |     None |          381 |         2 |
| -BxWyEIQ6wypT-37MzZizQ |     None |          353 |         2 |
| -4TMQnQJW1yd6NqGRDvAeA |     None |          343 |         1 |
| -ITj6Pu8Gdw8MmLf0XBEKQ |     None |          319 |         1 |
| 1HD5iUUfVJDbfEBIn9yVhw |     None |          295 |         1 |
| -R2kwt0qMnzwEdAfXPvkXg |     None |          264 |         2 |
| 04kZ5CSh6oKhI5huU5bLdg |     None |          242 |         9 |
| 1vEBp-YeAvqg1w19GzYg9w |     None |          242 |         4 |
| 1dYpffQi3qdh-dkXF4LZBw |     None |          239 |         8 |
| 1dhPgc7E7IzzpxjHM2LphQ |     None |          234 |         6 |
+------------------------+----------+--------------+-----------+
(Output limit exceeded, 25 of 254 total rows shown)
```

#### Tips and businesses: Does the tip count correlate with the business category?

It is difficult to find any correlation between tip count and business category, since the inner join only produces three businesses.

```
+------------------------+------------+--------------+-----------+
| id                     | category   | review_count | tip_count |
+------------------------+------------+--------------+-----------+
| 1GaooxqCWHzulI2Ub3CXEw | Mexican    |          103 |        51 |
| 0kyhbUW6NkpYjJzFBZ64vQ | Sandwiches |           91 |        12 |
| 2LVuwl-eH-8PYikyFmqcTQ | Pizza      |           28 |         2 |
+------------------------+------------+--------------+-----------+
```
