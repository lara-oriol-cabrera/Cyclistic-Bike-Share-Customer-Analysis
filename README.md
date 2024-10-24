# Cyclistic Bike-Share Customer Analysis
This project presents a comprehensive data analysis of Cyclistic, a fictional bike-share company based in Chicago, with the goal of uncovering valuable insights into customer behavior and usage patterns. By thoroughly examining real-world trip data, the analysis aims to identify key trends and opportunities for business growth and service optimization. The primary objective is to provide actionable recommendations that will enable Cyclistic to enhance its user experience, drive customer engagement, and strengthen its impact within the community. Through meticulous data exploration and interpretation, this project aspires to support Cyclistic in making informed data-driven decisions.

## INDEX 
1.- Scenario<br>
2.- Ask <br>
3.- Prepare <br>
4.- Process<br>
5.- Analyze <br>
6.- Share <br>
7.- Act <br>
8.- Reflections on the case study <br>

## 🎭 Scenario:
As a junior data analyst at Cyclistic, I have been tasked with a critical project aimed at uncovering insights into the behavior of two key user segments: Annual Members and Casual Riders. <br>

Cyclistic, a leading bike-sharing company in Chicago, is looking to enhance its business strategies by understanding the patterns and preferences between these two groups.<br>

While Annual Members enjoy the convenience of unlimited access with a subscription model, Casual Riders typically use the service on a pay-per-ride basis. 
The company’s ultimate goal is to increase customer retention and boost membership acquisition, converting more Casual Riders into loyal Annual Members. 
To achieve this, I have been asked to analyze usage trends, identify key factors that influence ride frequency, time of usage, and route preferences, and provide actionable insights. <br>

By revealing these behavioral trends, the company hopes to tailor its marketing and operational strategies, ultimately driving the conversion of more Casual Riders into Annual Members. My analysis will serve as a data-driven foundation for these strategic decisions.<br>

## 💡 ASK:
Business Task: The business task is to analyze the patterns of Members and non-Members to understand their behavior, preferences, and interactions with the company. I will help identify key factors that differentiate Members from Casual Riders in order to develop a strategy to convert non-Members into Members.

## 📚 PREPARE
How is the dataset: This dataset is provided internally by the company, Cyclistic. You can find the data source here: [Source](https://divvy-tripdata.s3.amazonaws.com/index.html)<br> 
In the data source we can find  multiple CSV files, each representing data for one month from January 2020 to August 2024. There are 15 variables included in each file that capture various aspects of bike and scooter rides. <br>

Description of each variable:<br>
- Ride_Id: a unique identifier for each ride. This ID can be used to track specific rides throughout the dataset. <br>
- Rideable_Type: the type of vehicle used for the ride. This can electric bike, standard bike, or electric scooter. <br>
- Date_Started_At: the date when the ride began, recorded in a standard date format (DD-MM-YYYY). <br>
- Time_Started_At: the time when the ride started, recorded in a 24-hour format (HH:MM:SS).<br> 
- Date_Ended_At: the date when the ride ended, recorded in the same format as the start date (DD-MM-YYYY). <br>
- Time_Ended_At: the time when the ride ended, recorded in the same 24-hour format (HH:MM:SS). <br>
- Start_Station_Name: the name of the station where the ride started. This could be the name of a bike station or scooter pickup point. <br>
- Start_Station_Id: a unique identifier for the start station, useful for data analysis and geographic mapping. <br>
- End_Station_Name: the name of the station where the ride ended. This could be the name of a bike station or scooter drop-off point. <br>
- End_Station_Id: a unique identifier for the end station, helping to trace the ride's destination. <br>
- Start_Latitude: the latitude of the starting station, allowing for geographic analysis of the ride's starting location. <br>
- Start_longitude: the longitude of the starting station, used alongside latitude for mapping purposes. <br>
- End_Latitude: the latitude of the ending station, enabling geographic analysis of the ride's destination location. <br>
- End_longitude: the longitude of the ending station, which, combined with latitude, helps in visualizing ride data on a map. <br>
- Member_Casual: indicates the type of rider. It can be either Member (someone with a subscription) or Casual (someone who pays for individual rides). This variable is important for analyzing user demographics and ride patterns.<br>

ROCCC Approach: <br>
(R)eliability: the dataset includes information on both Members and Casual users. This data is provided directly by Cyclistic, ensuring its accuracy and trustworthiness. As an internal dataset, it reflects the company's operations and user interactions, providing a solid foundation for analysis.<br>
(O)riginality: the dataset is original and derived from internal sources within Cyclistic, making it unique to the organization. <br>
(C)omprehensiveness: with 15 variables covering a wide range of data points, the dataset provides a comprehensive view of user interactions with Cyclistic's products. <br>
(C)urrentness: the dataset spans from January 2020 to August 2024, with updates occurring monthly.<br>
(C)ited: this dataset is provided by Cyclistic. <br>

‼️Data Limitations: The dataset lacks demographic variables, limiting user segmentation analysis, and analyzing only one month's data may introduce seasonal biases. <br>

👩🏻‍⚕️ How I dealt with Data Limitations: I would recommend that the company begin collecting demographic variables and used Excel's Power Query tools to merge data into a single spreadsheet encompassing 12 months of information from September 2023 to August 2024.<br>

## ⚒️ PROCESS
I first examined the dataset to understand the context of each variable and gain a comprehensive overview. Next, I used data filters to identify and address null values, followed by removing duplicates. Initially, I had 1,029,750 observations, but after cleaning, I retained 1,016,175 observations, eliminating 13,575 that could skew the analysis!! I then ensured all data was in the correct format. After familiarizing myself with each variable's context, I corrected errors, such as in latitude and longitude values, which may have resulted from data manipulation and downloads. Knowing the type of analysis I intended to perform, I added several new columns to the dataset. I calculated the “day of the week” for each bike ride and computed the “distance” traveled in meters for each observation. Additionally, I calculated the “ride length” in minutes using the time variables previously defined, and created  new columns for the "months" and “season” when the service was used. <br>

🆘 I apologize for the inconvenience, but the database is quite large and cannot be shared directly at this time. We are actively working on a solution to address this issue and appreciate your patience. Thank you for your understanding!

Tools used: Microsoft Excel 

## 📈 ANALYSIS
### DESCRIPTIVE ANALYSIS
In this section, I will conduct a descriptive analysis to provide a comprehensive overview of the data related to Cyclistic's bike usage patterns. This analysis aims to summarize key statistics and trends, helping us understand the characteristics of different user groups, including casual riders and members. 

a) Members and Casuals  
```r
table(DataSet$Member_Casual)
prop.table(table(DataSet$Member_Casual))
pie(prop.table(table(DataSet$Member_Casual)), main = "Distribution for Members and Casuals")
```
<p align="center">
<img width="400" alt="Captura de pantalla 2024-10-24 a las 9 46 42" src="https://github.com/user-attachments/assets/0cd42460-9512-4f6d-91b5-ed686411f508">
</p>
From the analysis of the distribution we can see that the most active user type are the members, being a total of 69,68%, making casuals are a 30,31%. 

b) Rideable type 
```r
table(DataSet$Rideable_Type) 
prop.table(table(DataSet$Rideable_Type)) 
barplot(table(DataSet$Rideable_Type), main="Distribution for Rideable Type", xlab="Categories of Rideable Type", col="lightgreen")
```
<p align="center">
<img width="457" alt="Captura de pantalla 2024-10-11 a las 19 16 55" src="https://github.com/user-attachments/assets/31f21c6d-3cb0-4e89-bb1c-a94538442d85">
</p>
In our analysis of rideable types, we observe that the classic bike is the most utilized option, comprising 65.83% of total rides, while the electric scooter accounts for only 0.63%. It’s important to note that the electric scooter was introduced in August 2024, which may explain its lower usage at this stage.

c) Season
```r
table(DataSet$Season) 
prop.table(table(DataSet$Season)) 
barplot(table(DataSet$Season), main="Distribution for Seasons", xlab="Seasons", col="lightgreen")
```
<p align="center">
<img width="424" alt="Captura de pantalla 2024-10-23 a las 19 31 30" src="https://github.com/user-attachments/assets/0c33804e-c774-45eb-af9b-5c36511a0d85">
</p>
Next, examining seasonal trends, summer emerges as the season with the highest activity, representing 25.96% of rides, closely followed by winter at 25.92%. Conversely, spring sees the least activity, accounting for only 23.69%.

d) Day of the week 
```r
table(DataSet$Day_week) 
prop.table(table(DataSet$Day_week)) 
barplot(table(DataSet$Day_week), main="Distribution for Day of the Week Usage", xlab="Day of the Week", col="lightgreen")
```
<p align="center">
<img width="427" alt="Captura de pantalla 2024-10-23 a las 19 36 47" src="https://github.com/user-attachments/assets/64507cd5-c821-49bc-acdf-16b08abc0b75">
</p>
Analyzing the days of the week, Wednesday is the most active day, with 15.54% of rides, while Sunday is the least active, contributing only 12.74%.

e) Hours
```r
table(DataSet$Hour) 
prop.table(table(DataSet$Hour)) 
barplot(table(DataSet$Hour), main="Distribution for Hours", xlab="Hours", col="lightgreen")
```
<p align="center">
<img width="427" alt="Captura de pantalla 2024-10-23 a las 19 05 04" src="https://github.com/user-attachments/assets/bbfd647a-4014-4918-84a8-312e31cda1f9">
</p>
When we look at the time of day, the peak hour for rides is 5:00 PM, capturing 10.50% of the total, whereas the least activity occurs at 3:00 AM, with just 0.2%.

f) Ride Distance in Meters
```r
mean(DataSet$Distance_Meters)
sd(DataSet$Distance_Meters)
```
Regarding distance, the average ride distance is 2003.4 meters, with a standard deviation of 1817.54 meters, indicating significant variability in ride distances, suggesting diverse usage patterns among riders.

g) Ride Length in Minutes 
```r
mean(DataSet$Minutes_num)
sd(DataSet$Minutes_num)
```
For ride length, the average duration is 15.26 minutes, with a standard deviation of 34,84 minutes,
that shows that ride distances are relatively consistent and clustered around the mean, reflecting a more uniform usage pattern among the customers.

Tools used: R-Studio 

### ANALYSIS 
Now, to analyze the differences between the two user types, I will transition to SQL, as it is more effective for handling large datasets.

a) Now, I will analyze the differences in rideable types between the two user types.
```SQL
SELECT COUNT(Ride_Id) AS CountRides,
Member_Casual,
Rideable_Type
FROM `cyclisticproject-438012-data_analysis.dataset`
GROUP BY Member_Casual,
Rideable_Type
```
 <p align="center">
<img width="306" alt="Captura de pantalla 2024-10-23 a las 20 45 04" src="https://github.com/user-attachments/assets/1070c399-261b-4c8b-ab4c-23267f17f798">
</p>
<p align="center">
<img width="404" alt="Captura de pantalla 2024-10-24 a las 10 16 25" src="https://github.com/user-attachments/assets/e4862fd2-eae1-41e6-8c5e-eadf5bc9ba81">
</p>

The analysis reveals that the classic bike is the most commonly used rideable type for both user groups, indicating a strong preference for this option across the board. Conversely, the electric scooter emerges as the least utilized choice for both groups, suggesting limited adoption at this stage. 

b) In this section, we will explore the duration of rides for both user types. Understanding how long each group spends on their rides can provide valuable insights into their riding habits and preferences. 

```SQL
SELECT AVG(Formatted_Ride_Length) AS Average Ride_Length,
Member_Casual
FROM `cyclisticproject-438012-data_analysis.dataset`
GROUP BY Member_Casual
```
<p align="center">
<img width="213" alt="Captura de pantalla 2024-10-23 a las 20 44 51" src="https://github.com/user-attachments/assets/d15847d7-e2be-4508-963f-05ee35f614b0">
</p> 
<p align="center">
<img width="602" alt="Captura de pantalla 2024-10-23 a las 20 49 26" src="https://github.com/user-attachments/assets/fe8335ed-403a-4e2b-8443-20f2970abc67">
</p>
In conclusion, the data indicates that casual users spend significantly more time on rides, averaging 22 seconds, compared to members, who average only 12 seconds. This difference suggests that casual users may be engaging in longer or more leisurely rides, while members likely prioritize efficiency and quicker trips. 

c) After noting that casual users spend more time on their rides, while members tend to take shorter trips, we will now examine the distances traveled by both groups. 
```SQL
SELECT AVG(Distance_Meters);
Member_Casual
FROM `cyclisticproject-438012-data_analysis.dataset`
GROUP BY Member_Casual
```
<p align="center">
<img width="205" alt="Captura de pantalla 2024-10-23 a las 20 44 40" src="https://github.com/user-attachments/assets/67a65ab3-df69-47d2-989d-7075ed85aecd">
</p>
<p align="center">
<img width="603" alt="Captura de pantalla 2024-10-23 a las 20 49 10" src="https://github.com/user-attachments/assets/7207c517-2edf-4cca-874d-575b7edf099b">
</p>
While the ride meter indicates that both user groups travel similar distances, the observation that casual users spend more time on their rides suggests a potential hypothesis: casual users may be engaging in more leisurely journeys, whereas members could be favoring more point-to-point trips. 

d) Now, I will analyze trip patterns based on seasonal variations. Understanding how ride frequency and duration change with the seasons can provide valuable insights into user behavior and preferences throughout the year. 
```SQL
SELECT COUNT(Ride_Id) AS Rides,
Mmeber_casual,
Season
FROM `cyclisticproject-438012-data_analysis.dataset`
GROUP BY Member_casual,
Season
```
<p align="center">
<img width="305" alt="Captura de pantalla 2024-10-23 a las 20 50 05" src="https://github.com/user-attachments/assets/92886c2b-c00d-47b2-9bf2-feef546259bd">
</p>
<p align="center">
<img width="523" alt="Captura de pantalla 2024-10-23 a las 20 50 21" src="https://github.com/user-attachments/assets/3f8c5988-bcc7-4c33-82a0-627b1253b8d3">
</p>

Data reveals distinct seasonal preferences between user groups: casual users predominantly favor summer for their rides, while members show a preference for winter. This divergence suggests that casual riders may be more inclined to take advantage of favorable weather conditions, while members might engage in riding year-round, possibly for commuting or consistent activity.

e) Moreover, I will explore how trip patterns vary by day of the week. Recognizing that user behavior may fluctuate throughout the week, we aim to analyze the frequency and duration of rides on different days. 
```SQL
SELECT COUNT(Ride_Id),
Member_Casual,
Day_week
FROM `cyclisticproject-438012-data_analysis.dataset`
GROUP BY Member_Casual
Day_week
```
<p align="center">
<img width="306" alt="Captura de pantalla 2024-10-23 a las 20 52 40" src="https://github.com/user-attachments/assets/499899c5-e0c6-4b8c-921e-d7f5a8dcf42d">
</p>
<p align="center">
<img width="603" alt="Captura de pantalla 2024-10-24 a las 10 19 54" src="https://github.com/user-attachments/assets/f335343a-3b21-49b4-9122-675937b4104f">
</p>

My analysis indicates that casual users significantly increase their rides on weekends, with Saturday being their peak day. In contrast, members demonstrate a stronger preference for riding during weekdays, with Wednesdays being the most active day for this group. These patterns highlight the differing motivations and riding behaviors between casual users and members, suggesting that casual riders may be engaging in leisure activities, while members likely use rides for commuting or other weekday purposes.

f) Furthermore, I will also examine how ride patterns vary by hour of the day. Analyzing the timing of rides can provide valuable insights into user behavior, revealing peak usage times and identifying trends related to commuting, leisure, or other activities. 
```SQL
SELECT COUNT(Ride_Id) AS Rides,
Hour_Started,
Member_Casual
FROM `cyclisticproject-438012-data_analysis.dataset`
GROUP BY Member-Casual,
Hour_Started
```
<p align="center">
<img width="304" alt="Captura de pantalla 2024-10-23 a las 20 54 31" src="https://github.com/user-attachments/assets/72d32f34-bf9f-4248-9cc2-63e68531dc81">
</p>
<p align="center">
<img width="603" alt="Captura de pantalla 2024-10-23 a las 20 55 01" src="https://github.com/user-attachments/assets/d93472c6-a00e-4b4a-854b-0a44c2ad3890">
</p>

In conclusion, ride patterns throughout the day reveals that casual users tend to have a more dispersed riding schedule, engaging at various times without distinct peaks. In contrast, member users exhibit two significant spikes in activity, particularly at 8 AM and 5 PM. These times likely correspond to common commuting hours, indicating that members may primarily use rides for practical purposes. 

g) Finally, I will use the starting points of bike journeys to understand where users prefer to begin their rides. By examining the stations chosen by both casual users and members, we can gain insights into travel patterns, popular destinations, and potential factors influencing their choices. 
<p align="center">
<img width="149" alt="Captura de pantalla 2024-10-23 a las 22 04 01" src="https://github.com/user-attachments/assets/b09c438f-d63a-4818-b628-e640c373b348">
</p>
<p align="center">
<img width="427" alt="Captura de pantalla 2024-10-23 a las 22 03 56" src="https://github.com/user-attachments/assets/89aa3099-62a5-462f-b7b8-728415153b55">
</p>

Starting points reveals that both user groups predominantly begin their rides in the beach zone of Chicago. However, a notable distinction emerges in the dispersion of their chosen locations: members exhibit a wider spread of starting points across the map, suggesting a greater diversity in their riding destinations. In contrast, casual users are more concentrated in the beach area, indicating a preference for recreational rides in this specific location. 

Tools used: SQL (Big Query), Microsoft Excel and Tableau. 

### HYPOTHESIS TESTING 
After completing the initial analysis, I decided to conduct some hypothesis testing using contingency tables and ANOVA to assess the significance of the differences in means and the dependency of the variables. Specifically, I utilized the Chi-Square Test for the contingency tables and One-Way ANOVA to analyze the data. The results of all tests indicated significant findings, reinforcing the insights gained from the initial analysis.

This additional step has provided a deeper understanding of the data, and I plan to continue with this analysis to explore the implications further. This rigorous approach adds an extra layer of validity to our conclusions and enhances our overall understanding of user behavior.

Tools used: JMP PRO 17

### CONCLUSION
To sum up, the analysis highlights several key differences between casual users and members. Casual users primarily utilize bikes for leisure activities, favoring weekend rides and specific locations like the beach zone. Their riding patterns are more dispersed throughout the day, reflecting a focus on enjoyment and relaxation. In contrast, members tend to use bikes more for commuting purposes, with significant spikes in activity during weekday mornings and evenings. They demonstrate a greater diversity in starting points, indicating a broader range of destinations.

However, to enhance the depth of this analysis, I would recommend that the company continue to collect data, particularly demographic information that is currently missing. This additional data would allow for a more comprehensive understanding of user behaviors and preferences, ultimately leading to more effective strategies tailored to each group’s needs.

### 🖼️ SHARE
Taking all these insights into account, I have created an interactive dashboard that allows for a comprehensive exploration of the data. This dashboard enables users to visualize key trends and patterns related to both casual users and members, facilitating a deeper understanding of their behaviors and preferences. With features that allow for filtering and drilling down into specific metrics, the dashboard serves as a valuable tool for ongoing analysis and decision-making.<br>
[Tableau](https://prod-uk-a.online.tableau.com/#/site/laraoricab-072e17f9c4/redirect_to_view/7761462)

<p align="center">
<img width="1199" alt="Captura de pantalla 2024-10-23 a las 22 19 13" src="https://github.com/user-attachments/assets/ee755ad1-2edd-41b0-8c96-6d83b28cac8a">
</p>

Tools used: Tableau 

### 👀 ACT 
a) Targeted Promotions for Weekend Riders:<br>
Given the higher bike usage among casual riders during weekends, Cyclistic could implement targeted promotions specifically designed for this audience. For instance, offering discounts on memberships that are exclusively valid for weekend use could incentivize more casual riders to consider membership. Additionally, creating a special "Weekend Rider Membership" could encourage repeat usage by providing unique benefits, such as discounts on weekend rentals or access to special events. This approach not only attracts casual users but also fosters a sense of community among weekend riders.

b) Flexible Membership Options:<br>
To better cater to casual riders, particularly those who may be hesitant to commit to a full annual membership, Cyclistic could introduce short-term or flexible membership plans. Options such as monthly or quarterly memberships would appeal to casual users and tourists who may not be frequent riders but want the convenience of membership during their stay. By reducing the commitment barrier, Cyclistic can attract a broader audience and convert casual users into more regular customers.

c) Emphasizing Cost Savings for Frequent Riders:<br>
To encourage casual riders to transition into membership, Cyclistic could highlight the potential cost savings for those who ride frequently. By demonstrating how much money casual riders could save by becoming members—especially for those with longer ride durations or who ride regularly on weekends—Cyclistic can create a compelling value proposition. This could be achieved through targeted marketing campaigns that showcase real-life examples of savings based on usage patterns. By illustrating the financial benefits, Cyclistic can effectively convert high-usage casual riders into committed members.

d) Feedback Mechanisms: <br>
Implementing feedback systems allows Cyclistic to gather insights directly from casual riders about their experiences and preferences regarding membership options. This could be achieved through surveys, suggestion boxes, or online platforms where users can share their thoughts. By actively seeking input, Cyclistic can identify potential barriers to membership, understand what features or benefits riders value most, and tailor their offerings accordingly. This responsive approach not only enhances user satisfaction but also builds trust and loyalty, as riders feel their opinions are valued and considered in decision-making processes.

e) Seasonal Promotions: <br>
Considering the seasonal preferences observed in ride patterns, Cyclistic could launch targeted seasonal promotions to keep users engaged throughout the year. For example, special discounts or offers during peak riding seasons, like summer, could attract more casual riders, while winter promotions could encourage members to continue riding despite colder weather. By aligning promotions with seasonal trends, Cyclistic can provide timely incentives that encourage more frequent usage, thereby maximizing ridership even during typically slower periods. This strategy not only boosts usage rates but also keeps the brand top-of-mind for users, making them more likely to choose Cyclistic when they are ready to ride.

f) Community Events: <br>
Organizing community events or group rides can significantly enhance user engagement and foster a sense of belonging among riders. These events could include themed rides, bike safety workshops, or social gatherings that bring together both casual and member users. Such initiatives create opportunities for riders to connect, share experiences, and develop a community around cycling. Additionally, community events can serve as a platform for Cyclistic to promote membership benefits and encourage casual riders to consider joining. By cultivating a strong community presence, Cyclistic not only increases user loyalty but also strengthens its brand identity as a welcoming and inclusive cycling service.

Based on the analysis and suggested actions, the initial step is to develop targeted marketing campaigns and strategies designed to convert casual riders into members. Following this, it will be essential to monitor the effectiveness of these initiatives.<br>

The key performance indicators (KPIs) to track for this project include:<br>

- Conversion Rates: This metric will assess the effectiveness of promotions and flexible membership options in converting casual riders into members. <br>
- Ride Frequency Comparison: By comparing the ride frequency of users before and after they become members, we can evaluate whether the conversion leads to an increase in riding activity, particularly on weekends.<br>

This phase will be crucial in determining the uptake of new membership plans and whether the newly converted users maintain or increase their ride frequency over time.<br>

### 🙇‍♀️ REFLECTIONS ON THE CASE STUDY 
Reflecting on this project, I found it to be a highly engaging and insightful experience. It allowed me to delve into various aspects of user behavior and data analysis, which not only heightened my interest but also helped me develop and consolidate valuable skills. Through this process, I enhanced my analytical abilities, learned how to interpret data effectively, and gained practical experience in formulating actionable strategies.

I look forward to engaging in similar projects in the future, as they provide an excellent opportunity for continuous learning and professional growth. Each experience contributes to my understanding of user dynamics and helps me better navigate real-world challenges in the field.










