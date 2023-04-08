# Data Cleaning

![image](https://user-images.githubusercontent.com/86930309/230744142-d22c7cbc-4dcc-4d63-8839-ee65f4951f02.png)

## In this case study I will learn to clean the data to prepare it for modeling and machine learning. The two datsets are from information about grade and ascents of climbing places in Europe and the U.S.A. The idea behind this project is to create recomendations on where to climb based upon a climbers information/criteria.

## 1. Import Libraries

## 2. Import the two CSV files

## 3. Brief Feature Analysis

## 4. Dropping Columns

## 5. Dropping the Unrated Routes

## 6. Removing Null Values & Converting Data Types

- Why delete nulls now? the ratings and grade_id columns are float64 data types, but they should be int64 (example: 1.0, 2.0, 3.0). The only reason they are floats is because they have null values in their columns.

## 7. Detailed Feature Analysis

### - Ratings

a. 1-3 stars of how much the route was enjoyed

b. 0 means not rated. Does NOT MEAN given 0 stars

c. Ascent Rating

![image](https://user-images.githubusercontent.com/86930309/230744336-c358f879-92a0-4c98-81ac-8f4bf3a40ac2.png)

Negatively skewed distribution

### - Name & Crag Column

We need to:

- a. Normalize

-b.  Drop NaN values

- c. Filter out names with less than 3 characters

- d. Fix spelling Problems:

I. Phonetic Techniques: Soundex. This was too aggresive and reduced our data drastically. 

II. Phonetic Techniques: Double Metaphone. Drops the number of groups from around 400,000 to 12,736. Still too aggresive.

III. Filtering Out Lower Frequency Names. I tested four different filters (route names occuring <2, <3, <6, & <10). After analyzing the algorithm performance and accuracy with each of these filters, I discovered the 6x filter performs the best. This can also be viewed below where after the 5x the bar graph starts to level out.
Thus, I will filter the dataset to only include routes that occur more than 5 times
 
 
 ### - Climb Type
 
0 = rope climbing

1 = bouldering

![image](https://user-images.githubusercontent.com/86930309/230744747-48c04bd5-426e-4148-bcdf-a73dc164fa99.png)

Many more roup climbs than bouldering ascents. May want to think about segmenting these different climbs into different groups because typically boulderers are just wanting boulder routes and vice versa with rope climbs.

### - Grade ID

![image](https://user-images.githubusercontent.com/86930309/230744898-91ae67b3-fa0f-427b-bd12-ec0fd03a2378.png)

a. The grade of the climb is on a scale from 1-86, with 1 being the easiest. Many of the logged climbs where 49.

### - Country

Country Normalization :

a. Make column capital letters.

b. Use the country_converter to check if country values are valid, if not, I will turn them into null values.

c. Will use the mode aggregation per route name to populate null values of the country column.

![image](https://user-images.githubusercontent.com/86930309/230745099-6060ec4d-c642-45ba-9499-a5b7960bfed7.png)

d. Most of the climbing logs were from Spain.

### - Grade Table

a. Numbered 1-86.
b. Corresponds to the ascent table & it gives each climb a number 1-86 that corresponds to different rating systems in the US and France.
c. This column is correctly coded as an int64 data type, no work needs to be done on this column.

### - Routes & Boulders

a. Need to forward fill all the USA columns so they correspond to the more numerous French Columns.

## 8. Exporting Data Frames to CSV

### Step 1: Copy the ascent table, and delete all rows except the three rows for the recommendation system, (user_id, name_id, rating).

### Step 2: Merge the grade table with the reference table so all reference items are in one table.

### Step 3: Drop unneccary columns in both data frames and re-arrange columns.

### Step 4: Export files to google drive.
