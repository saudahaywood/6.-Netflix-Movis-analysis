
# **Netflix Movies Analysis**

## **Project Overview**
This project analyzes **Netflix’s most popular movies and TV shows** based on **viewership data, genre trends, and regional performance**. The goal is to provide **movie creators** with **data-driven insights** to guide future content development, ensuring alignment with audience preferences.

## **Target Audience**
- **Movie Creators & Content Producers**: To help them identify **high-performing genres** and **regional trends** for better decision-making in future productions.
- **Streaming Analysts**: To understand **viewer behavior** and optimize **content recommendations**.

## **Call to Action**
- **Develop content in high-performing genres** identified in the analysis.
- **Focus on regional audience preferences** to expand Netflix’s global reach.
- **Balance content variety** by offering diverse movie lengths and family-friendly options.

---

## **Dataset Overview**
### **1. Most Popular Netflix Movies & Shows**
- **Source:** Netflix Global Data
- **Columns:**
  - `category`: Film (English/Non-English) or TV Show.
  - `rank`: Rank of the movie/show.
  - `show_title`: Name of the content.
  - `hours_viewed_first_91_days`: Total watch time in the first 91 days.
  - `runtime`: Duration of the movie/show.
  - `views_first_91_days`: Total views in the first 91 days.

### **2. Weekly Global Netflix Rankings**
- **Source:** Netflix Global Weekly Top 10
- **Columns:**
  - `week`: Date of ranking.
  - `category`: Type of content.
  - `weekly_rank`: Position in the weekly top 10.
  - `show_title`: Name of the content.
  - `weekly_hours_viewed`: Total hours watched per week.
  - `runtime`: Duration of the movie/show.
  - `cumulative_weeks_in_top_10`: Number of weeks in the top 10.

### **3. Regional Performance by Country**
- **Source:** Netflix Top 10 by Country
- **Columns:**
  - `country_name`: Country where the ranking applies.
  - `weekly_rank`: Position in the weekly top 10.
  - `show_title`: Name of the content.
  - `cumulative_weeks_in_top_10`: Total weeks in the top 10.

---

## **Methodology**
### **1. Data Exploration & Cleaning**
- **Checked for missing values and duplicate entries.**
- **Formatted date and time columns** for consistency.
- **Converted watch hours to numerical values** for better analysis.

```python
import pandas as pd

# Load the dataset
df = pd.read_excel('most-popular-netflix.xlsx')

# Display dataset preview
print(df.head())

# Check for missing values
print(df.isnull().sum())
```

---

### **2. Key Visualizations & Insights**
#### **Top 10 Most Watched Netflix Movies & Shows**
```python
import matplotlib.pyplot as plt

# Sort dataset by hours viewed
top_10 = df.sort_values(by='hours_viewed_first_91_days', ascending=False).head(10)

# Bar chart visualization
plt.figure(figsize=(10, 6))
plt.barh(top_10['show_title'], top_10['hours_viewed_first_91_days'], color='skyblue')
plt.xlabel('Total Hours Viewed (First 91 Days)')
plt.ylabel('Show Title')
plt.title('Top 10 Netflix Shows/Movies by Total Hours Viewed')
plt.gca().invert_yaxis()
plt.show()
```
#### **Findings:**
- **Thriller, fantasy, and adventure genres dominate** Netflix’s most-watched titles.
- **High engagement films** include *Red Notice*, *Don’t Look Up*, and *Bird Box*.

---

#### **Runtime vs Viewership**
```python
plt.figure(figsize=(12, 4))
plt.scatter(df['runtime'], df['views_first_91_days'], color='green', alpha=0.7)
plt.xlabel('Runtime (in hours)')
plt.ylabel('Views in First 91 Days')
plt.title('Runtime vs Views for Netflix Shows/Movies')
plt.grid(True)
plt.show()
```
#### **Findings:**
- No strong correlation between runtime and views.
- **Both short and long-duration content** perform well.
- **Recommendation:** Focus on **content quality** rather than runtime.

---

#### **Top Shows by Cumulative Weeks in Top 10**
```python
# Rank movies by total weeks in Top 10
ranked_movies = df.groupby('show_title')['cumulative_weeks_in_top_10'].max().sort_values(ascending=False)

# Select the top 10
top_10_ranked = ranked_movies.head(10)

# Plot results
plt.figure(figsize=(10, 6))
top_10_ranked.plot(kind='bar', color='lightblue')
plt.xlabel('Show Title')
plt.ylabel('Cumulative Weeks in Top 10')
plt.title('Top 10 Netflix Shows/Movies by Cumulative Weeks in Top 10')
plt.xticks(rotation=45)
plt.show()
```
#### **Findings:**
- **Long-term hits include *Yo Soy Betty, La Fea* and *Manifest*.**
- **Non-English TV shows maintain steady weekly viewership.**
- **Recommendation:** **Increase investment in international content.**

---

### **3. Regional Performance Analysis**
#### **Top Shows in the U.S.**
```python
# Filter U.S. data
us_data = df[df['country_name'] == 'United States']

# Rank by cumulative weeks in Top 10
us_top_shows = us_data.groupby('show_title')['cumulative_weeks_in_top_10'].max().sort_values(ascending=False).head(10)

# Plot results
plt.figure(figsize=(10, 6))
us_top_shows.plot(kind='bar', color='lightblue')
plt.xlabel('Show Title')
plt.ylabel('Cumulative Weeks in Top 10')
plt.title('Top Shows in the U.S. by Cumulative Weeks in Top 10')
plt.xticks(rotation=45)
plt.show()
```
#### **Findings:**
- **Family-friendly movies like *Sing 2*, *Super Mario Bros.*, and *Despicable Me 2* dominate.**
- **Mature content such as *Stranger Things* and *Squid Game* also performs well.**
- **Recommendation:** Maintain a **balanced mix of family-oriented and mature content.**

---

## **Recommendations**
1. **Invest More in Thriller, Adventure, and Fantasy Genres**  
   - These genres dominate Netflix’s most-watched list.
2. **Increase Focus on International Content**  
   - Non-English shows consistently **maintain long-term popularity**.
3. **Expand Family-Friendly Content**  
   - Animated movies like *Super Mario Bros.* and *Despicable Me 2* attract **long-term viewership**.
4. **Content Variety is Key**  
   - No clear correlation between runtime and views—**focus on story quality.**
5. **Leverage Regional Preferences**  
   - **Optimize content** for specific country-level preferences.

---

## **Challenges & Limitations**
- **Netflix's Algorithm Influence**: Content rankings are affected by **Netflix’s recommendation algorithm**.
- **Data Coverage**: Some weeks and regions **lack complete records**.
- **Viewership Trends Change Rapidly**: Popularity can shift due to **external factors like social media trends**.

---

## **Future Enhancements**
1. **Time-Series Forecasting**  
   - Predict upcoming **high-performing content trends**.
2. **Sentiment Analysis**  
   - Analyze **social media discussions** around Netflix content.
3. **Interactive Dashboard**  
   - Use **Tableau or Power BI** for real-time **data visualization**.

---

## **Required Libraries**
To run this project, install the necessary Python libraries:
```bash
pip install pandas numpy matplotlib seaborn
```

---

## **References**
- [Netflix Top 10](https://top10.netflix.com/)
- [Netflix Global Data](https://www.netflix.com)
