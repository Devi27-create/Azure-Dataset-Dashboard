# Microsoft Azure- Microsoft SQL Server Management Studio- PowerBI:

**Introduction**

In this project of Insigh BI Solutions Pvt. Ltd., I first focused on data cleaning using Azure SQL. I utilized a few functions to remove inconsistencies, and formatted the data for better analysis. Once the data was thoroughly cleaned and structured, I moved on to the visualization phase using Power BI

## Microsoft Azure 

**Step 1: Creating Database & Loading Data**

To begin the process, I logged into my Azure account to create a database filling the basic details of server,  Database name, Authentication method and password and clicked on review+create and then on create. once deployment is completed then going to resource I then setted up a server firewall via selecting a Public network and IPv4 address and saved the same.

After this I opened the Microsoft SQL Server Management Studio and through Database Engine connected the server by providing the User name and Password. Now going back to Azure in Query editor(preview) by providing the same login credentials I used while creating the resource I logged into the Query editor. after this under tables while futher expanding the mentioned data I clicked on the three dots and clicked on the select top 1000 rows with this a query "SELECT TOP (1000) * FROM [dbo].[Men Tshirt]," will get excecuted.

**Step 2: Data Transformations** 
After loading the data and gaining a comprehensive understanding of its structure and content, I proceeded to implement some data transformations after finding the impurities in the 'original price' and 'sales price' columns. It appeared that there were unnecessary question marks preceding both prices, which could potentially lead to inaccuracies in data analysis. To resolve this issue, I updated the table to remove the question marks, ensuring that the values in both the 'original price' and 'sales price' columns were clean and properly formatted.

This was accomplished using the following SQL command:
```sql
update [dbo].[Men Tshirt]
set original_price =trim(replace(cast(original_price as varchar(max)),'?',''))
where original_price like '%?%'

update [dbo].[Men Tshirt]
set sale_price =trim(replace(cast(sale_price as varchar(max)),'?',''))
where sale_price like '%?%'
```


## POWER BI DAX+ Dashboard

Once the data was cleaned, I proceeded to connect the Microsoft Azure Database with Power BI using the get data option and connect it via the server name available in Azure. This process allowed me to create insightful visualizations and reports based on the refined dataset, facilitating deeper analysis and informed decision-making.

**POWER BI DAX:**
By opening the power bi I clicked on the transform data for adding some other columns which I needed to create the dashboard. once the data was visible in the Power BI's Power query I checked for the data types of the available columns and changed the data types of orignal_price and sale_price from text to whole number. later that I Checked fro the NA values and on finding that I cleared the filter from that on all the columns through which I excluded 16 NA records, but other than that because I found other NA values In Original and sales price column where values where avilable I had to add another column to find a fix for this problem. so I created another column and wherever the orignal_price column value was NA and sales_price column values were valid value(a number), I replaced it with 1.5 because we wanted the orignal_price column values to be equal to 50% more than the sale_price column values and for else case I wanted zero to be there in the output so I added that as well.

Now that the Factor column got created now I needed to multiply the factor column with sales column to get the values for the NA in Orignial_price column.

**Structure and Order:**
1. Project Title/ Headline
2. Short Description
3. Tech Stack
4. Data Source
5. Features/Highlights
6. Screenshots

**1. Project Title: Insigh BI Solutions Private Limited**

**2. Short Description:**

Insigh BI Solutions Private Limited Dashboard is a visually engaging analytical Power BI report designed to help the users to explore and compare the different brands insights, the report presents key insights across two distinct pages. The first page highlights the various brands, while the second page provides more detailed breakdowns and visual representations of specific metrics. This approach not only enhances the clarity of the insights but also makes it easier to understand and interpret the findings effectively.


**3. Tech Stack:**

-**Microsoft Azure+ Microsoft SQL Server Management Studio-** Utilized for robust data storage and management and data loading and cleaning.
-**PowerBI-** The primary data visualization platform used to create the dashboard, offering the interactive features that enhance user engagement and comprehension of the data.
-**File Format-** The dashboard is developed in .pbit format with snapshot visualizations saved as .png files for sharing and reporting purposes. 

**4. Data Source:**
Source: https://www.udemy.com/course/complete-data-analyst-bootcamp-from-basics-to-advanced/learn/lecture/50857825#overview

**5. Features/Highlights:**

1. Key Questions
2. Goal of the Dashboard
3. A Walkthrough of Key Visuals


**1. Key Questions:**
1) What are the highest number of varites in the top 5 brands?
2) What is the highest average sales price of the top 5 brands?
3) What is the average of discount % in the top 5 brands?
4) What is the top 5 brands average profit %?
5) What is the bottom 5 brands average profit %?

**2. Goal of the Dashboard:**

The primary objective of this dashboard is to provide users with an interactive and intuitive visual tool that simplifies data exploration and analysis. By allowing users to seamlessly navigate through the dataset. The dashboard helps to uncover intricate details regarding the usage patterns of KWH and CSU. This ultimately facilitates informed decision-making and encourages strategic planning for energy management and sustainability efforts.

**3. A Walkthrough of Key Visuals:**

**1. Text Box (top):**
The text box displays the title of the Dashboard, ***Energy Consumption Dashboard***.

**2. KWH by Country (Bar Chart) (Left Corner):**
This visually engaging bar chart illustrates the electric consumption in kilowatt-hours (KWH) across various countries. Australia leads the pack with an impressive usage of 80,410 KWH, highlighting its high energy demands. In contrast, Chile registers the lowest energy consumption among the listed countries, with a modest usage of 16,556 KWH, reflecting its comparatively lower energy requirements.

**3. CSU by Country (Bar Chart) (Middle):**
The bar chart presented here captures the energy usage in CSU by country. New Zealand stands out as the largest consumer, utilizing 16,862 CSU, indicative of its significant energy needs. Conversely, Nigeria occupies the bottom position with a total of 5,043 CSU, while Kenya follows closely behind at 5,126 CSU, illustrating the varying energy consumption patterns across these nations.

**4. KWH by Region (Column Chart) (Top Right Corner):**
This column chart effectively displays the energy consumption in KWH among the top six regions worldwide. Leading this chart is a region with a staggering total of 163,213 KWH, demonstrating substantial energy requirements. Notably, Australia appears at the lower end of this spectrum, with a usage of 145,825 KWH, indicating its relative energy consumption compared to other regions.

**5. KWH by Energy Source (Column Chart) (Top Second Right Corner):**
In this column chart, the five primary energy sources are analyzed based on their usage in KWH. Wind energy emerges as the most utilized source, with a remarkable consumption of 214,492 KWH, showcasing its growing importance in the energy mix. In contrast, the Geothermal Energy Source represents the smallest share, with a usage of 164,182 KWH, underscoring the need for increased investment in this area.

**6. CSU by Region (Column Chart) (Bottom Second Right Corner):**
This column chart visually represents the consumption in CSU across the top six regions. South America takes the lead with a notable consumption of 34,692 CSU, while Africa closely follows with 34,444 CSU, reflecting a competitive energy landscape. Meanwhile, North America registers the least consumption among these regions, with a total of 30,732 CSU, indicating differing energy usage patterns.

**7. CSU by Energy Source (Column Chart) (Bottom Right Corner):**
Here, the column chart categorizes the top five energy sources based on their usage in CSU. Wind energy again stands out, with a considerable consumption of 47,507 CSU, emphasizing its significance in energy generation. Conversely, the Geothermal Energy Source records the lowest usage in this context, with 32,841 CSU, pointing to potential areas for development in sustainable energy practices.


**6. Screenshots:**
See what the dashboard looks like - ![Alt Text](https://github.com/Devi27-create/AWS-SNOWFLAKE-TABLEAU/blob/main/Energy_Consumption_dashboard.png)







