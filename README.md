# Microsoft Azure - Microsoft SQL Server Management Studio - Power BI

**Introduction**

In my project at Insigh BI Solutions Pvt. Ltd., I embarked on a journey of data analysis that began with meticulous data cleaning using Azure SQL. This initial phase was crucial as I aimed to identify and remove inconsistencies while formatting the data for enhanced clarity and readiness for analysis. Once the data was thoroughly refined and structured, I transitioned into the visualization phase, utilizing Power BI to bring the insights to life.

## Microsoft Azure

**Step 1: Creating Database & Loading Data**

To kick off the process, I logged into my Azure account, navigating to the database creation interface. After filling in the essential details such as the server name, database name, authentication method, and password, I clicked on the review + create button. Following the creation process, I patiently waited for the deployment to complete. Once it was finished, I accessed the database resource and set up a server firewall, opting for a public network and specifying my IPv4 address to ensure secure access.

With the database in place, I opened Microsoft SQL Server Management Studio (SSMS) and connected to the server through the Database Engine, entering the username and password I had set earlier. I then returned to Azure to access the Query Editor (preview), using the same login credentials to establish a connection. To familiarize myself with the data, I expanded the tables and navigated to the relevant dataset. By clicking on the three dots, I selected the option to "Select Top 1000 Rows," which executed the query: 

```sql
SELECT TOP (1000) * FROM [dbo].[Men Tshirt]
```

**Step 2: Data Transformations**

After successfully loading the data and immersing myself in its structure and intricacies, I proceeded with essential data transformations. During my examination, I identified impurities within the 'original price' and 'sales price' columns, where unnecessary question marks had been inserted before these values. This inconsistency could lead to potential inaccuracies in subsequent data analysis, so I knew I needed to take corrective action.

To resolve this issue, I executed a series of SQL commands designed to cleanse the data. My aim was to remove the question marks and ensure the values from both the 'original price' and 'sales price' columns were not only accurate but also properly formatted for analysis. The following SQL commands facilitated this transformation:

```sql
UPDATE [dbo].[Men Tshirt]
SET original_price = TRIM(REPLACE(CAST(original_price AS varchar(max)), '?', ''))
WHERE original_price LIKE '%?%'

UPDATE [dbo].[Men Tshirt]
SET sale_price = TRIM(REPLACE(CAST(sale_price AS varchar(max)), '?', ''))
WHERE sale_price LIKE '%?%'
```

By applying these commands, I effectively stripped the 'original price' and 'sales price' columns of any unwanted characters, paving the way for accurate data analysis and meaningful insights.



## POWER BI DAX+ Dashboard

After meticulously cleaning the dataset, I took the next step of connecting the Microsoft Azure Database to Power BI. Utilizing the "Get Data" option, I entered the server name provided by Azure, which enabled me to seamlessly import the refined data into Power BI. This integration laid the groundwork for creating insightful visualizations and comprehensive reports, empowering me to conduct deeper analyses and make informed decisions based on the cleaned dataset.

**POWER BI DAX:**
Once I opened the data in Power BI, I immediately clicked on the "Transform Data" option to add additional columns necessary for building the dashboard. In the Power Query interface, I began by reviewing the data types of the existing columns. Noticing that both the `original_price` and `sale_price` fields were set as text, I promptly changed their data types to whole numbers to facilitate accurate calculations.

Next, I addressed the presence of NA values in the dataset. I filtered these values from all relevant columns, successfully excluding 16 records. However, I discovered more NA values specifically in the `original_price` and `sale_price` columns that needed to be resolved. To tackle this issue, I created an additional column designed to compensate for the missing data. In this new column, whenever the `original_price` value was NA but the `sale_price` contained a valid number, I replaced the NA with 1.5, reflecting that the original price should be set to 50% above the sale price. For all other scenarios, I ensured that zero was returned as the output.

After successfully creating the Factor column, my next task was to address the missing values in the `original_price` column. To do this, I utilized the Factor column to derive the necessary values by multiplying it with the corresponding `sale_price`. This operation was facilitated by introducing a new conditional column that I designated as the `Sale*Factor` column.

Once I calculated these values, I moved on to create a 'Marked Price' column. This column was designed specifically to replace the Original Price values where they were absent. To ensure data consistency throughout the dataset, I adjusted the data type of the Marked Price column from text to whole number. Finally, I cleansed the dataset by removing any extra and unnecessary columns that were no longer needed, streamlining the data for future analysis.

Having finalized these transformations, I closed the Power Query and applied all changes. With the data now properly structured, I proceeded to implement DAX formulas to incorporate additional analytical columns into my dataset.

To calculate the Discount % column, I employed the following DAX formula: 
```plaintext
Discount % = DIVIDE('Men Tshirt'[Marked Price] - 'Men Tshirt'[Sales Price], 'Men Tshirt'[Marked Price]) * 100
```

For the Profit % column, I utilized this DAX formula:
```plaintext
Profit % = RANDBETWEEN(2, 17)
```

To derive the Cost Price column, I applied the following DAX formula: 
```plaintext
Cost Price = DIVIDE(100 * 'Men Tshirt'[Sales Price], 100 + 'Men Tshirt'[Profit %])
```
With these calculations in place, I proceeded to dive into the dashboard creation, setting the stage for a robust and interactive data visualization experience.

**Structure and Order:**
1. Project Title/ Headline
2. Short Description
3. Tech Stack
4. Data Source
5. Features/Highlights
6. Screenshots

**1. Project Title: Insigh BI Solutions Private Limited**

**2. Short Description:**

The Insigh BI Solutions Private Limited Dashboard is a captivating analytical report crafted using Power BI, designed to empower users to delve deep into brand comparisons and insights. This report spans two distinct pages, each tailored to different analytical needs. The first page showcases a comprehensive overview of the various brands, Meanwhile, the second page offers an in-depth analysis, featuring detailed breakdowns and visually striking representations of specific metrics. This dual-page layout not only elevates the clarity of insights but also facilitates a more straightforward understanding and interpretation of the data findings, ensuring users can make informed decisions with ease.

**3. Tech Stack:**

- **Microsoft Azure + Microsoft SQL Server Management Studio:** These powerful tools are utilized for efficient data storage, management, and the essential processes of data loading and cleaning.
- **Power BI:** This leading data visualization platform serves as the cornerstone for the dashboard, providing interactive features that significantly enhance user engagement and comprehension of complex datasets.
- **File Format:** The dashboard is professionally developed in the .pbit format, with snapshot visualizations conveniently saved as .png files for streamlined sharing and reporting.

**4. Data Source:**
Source: https://www.udemy.com/course/complete-data-analyst-bootcamp-from-basics-to-advanced/learn/lecture/50857825#overview

**5. Features/Highlights:**

1. Key Questions
2. Goal of the Dashboard
3. A Walkthrough of Key Visuals


**1. Key Questions:**
1) What is the highest number of varieties among the top 5 brands?
2) What brand records the highest average sales price in the top 5?
3) What is the average discount percentage across the top 5 brands?
4) What is the average profit percentage for the top 5 brands?
5) How does the average profit percentage of the bottom 5 brands compare?

**2. Goal of the Dashboard:**

The overarching goal of this dashboard is to provide users with an interactive and user-friendly visual tool that simplifies the exploration and analysis of complex datasets. By enabling users to effortlessly navigate through the data, the dashboard uncovers intricate details regarding different brands. This functionality ultimately aids in informed decision-making and promotes strategic planning focused on energy management and sustainability initiatives.

**3. A Walkthrough of Key Visuals:**

**1. Header Text Box:**  
Prominently displayed at the top, the text box features the title of the Dashboard, ***Insigh BI Solutions Private Limited***, establishing a clear identity for the report.

**2. Top 5 Brands by Average Discount Percentage (Bar Chart, Top Left Corner):**  
This engaging bar chart portrays the average discount percentage for the top 5 brands, with The Indian Garage Co leading the chart at an impressive 72%. In contrast, Netplay holds the lowest position among the top 5 at 32%. The average discount percentage across all five brands ranges between 31.81% and 72.37%, providing a comprehensive view of pricing strategies.

**3. Top 5 Brands by Average Profit Percentage (Area Chart, Top Right Corner):**  
The area chart visualizes the average profit percentages of the top 5 brands, illustrating that Be Active, Valen Clun, and VAN HEUSEN brands top the chart with a average of 17% Profit percentage. While the rest of the brands had 16% average profit percentage. (Note: These data can vary everytime when we open the file as I had choosen random in the DAX for Profit Percentage).

**4. Top 5 Brands by Highest Number of Varieties (Donut Chart, Bottom Right Corner):**  
In this donut chart, the focus shifts to the highest number of varieties offered by the top 5 brands. The Indian Garage Co once again tops the list, boasting an impressive 51 varieties (22.87% of the total). Meanwhile, The Bear House and GAP present the lowest count among the top 5, each offering 27 varieties (12.11%).

**5. Top 5 Brands by Highest Average Sales Price (Ribbon Chart, Bottom Middle):**  
The ribbon chart analyzes the brands based on their average sales prices, revealing Armani Exchange as the leader with a remarkable average sales price of 6.1K. Conversely, the Kingdom of Whites registers the lowest average sales price among the top 5 at 3.6K, highlighting pricing diversity within the market.

**6. Bottom 5 Brands by Average Profit Percentage (Pie Chart, Bottom Left Corner):**  
Finally, this pie chart visually represents the average profit percentages of the bottom 5 brands. Notably, each of these brands reflects a uniform average profit percentage of 3.00, indicating potential challenges regarding profitability among these lesser-performing brands.(Note: These data can vary everytime when we open the file as I had choosen random in the DAX for Profit Percentage).

**6. Screenshots:**
See what the dashboard 1 looks like - ![Alt Text](https://github.com/Devi27-create/Azure-Dataset-Dashboard/blob/main/Insigh%20BI%20Brands.png)

See what the dashboard 2 looks like - ![Alt Text](https://github.com/Devi27-create/Azure-Dataset-Dashboard/blob/main/Insigh%20BI%20Details.png)







