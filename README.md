#### This is a Data Visualization Project on Video Games Sales Analysis using Tableau & Power BI

## 1. Introduction
The dataset ‘Video Game Sales with Ratings’ is used for this project. It is taken from Kaggle.com and is available at https://www.kaggle.com/datasets/rush4ratio/video-game-sales-with-ratings?select=Video_Games_Sales_as_at_22_Dec_2016.csv. This dataset is originally web scraped from Metacritic website which maintains aggregated reviews of films, TV shows, music albums and video games.

## 2. Persona and questions
XYZ is a mobile game development company looking for expanding their horizon to the pc and other gaming platforms. The Product development head of the company wanted to analyse the data answer the following questions. 

1.	Is there a correlation between the different performance metrics(eg. Critic Score,  User count etc) with respect to the available dimensions(eg. Genre, platform etc)?
2.	Who leads the development of the most preferred platform based games with in the last 10 years across different regions of the world?

Answering the question-1 gives the user a general idea of what metrics contribute to the success of a game. This analysis also gives the user, an understanding of the correlation of sales across different regions of the world. 
Answer the question-2, makes the user understand who their competitors are and what platform or genre they should target for the development of their initial launch in to video games industry. 

## 3. Paper Landscape

A paper landscape is designed to illustrate how the intended solution will look and function.

<img width="529" alt="image" src="https://user-images.githubusercontent.com/98278525/193476638-0f26f348-7874-4c65-8409-9e6e30ed8ae0.png">


## 4. Implementation

The implementation of this dashboard involves three steps. 
1.	Cleaning the data and clustering using python.
2.	Creating the Tableau Dashboard
3.	Creating the same dashboard in Power BI.

### 4.1 Data cleaning and Clustering:
The original dataset consists of 16719 rows and 16 columns. But there are many missing values. So, to clean them, python is chosen. After cleaning, the dataset is left with 6825 rows without any missing values. Clustering the dataset is done to identify if there are any correlations between the performance metrics with respective to the similar clusters. 
First the dataset is loaded into a python dataframe and then the rows with missing values are dropped. Then, the dataframe is left with 6825 rows. All the numerical columns are scaled using MinMaxScaler()

<img width="452" alt="image" src="https://user-images.githubusercontent.com/98278525/193476726-b269394d-b159-4321-b981-8f0599da0317.png">

As the dataset has categorical and numerical variables for clustering, KPrototypes clustering is the algorithm used for clustering the dataset. A range of clusters from 1 to 10 are tried to find the optimal number of clusters. The optimal number of clusters is found at 3 clusters. So, the clustering is done using the 3 as number of clusters. A new column names ‘cluster’ is added to the data and then the whole dataset is exported in to a CSV file which will be used for the Tableau and Power BI Dashboard preparation.

<img width="231" alt="image" src="https://user-images.githubusercontent.com/98278525/193476764-165cd4e6-13e0-455e-9fdb-26636a2694f6.png">
<img width="140" alt="image" src="https://user-images.githubusercontent.com/98278525/193476766-d99a164f-8ab9-4f81-ba4c-3e766860ce4d.png">

### 4.2. Tableau Dashboard Implementation:
The cleaned dataset without any missing values and with the new ‘cluster’ column, which is now in csv format, is imported to the Tableau. The year is displayed as number(decimal) format. So, a new calculated field is created by using the original field to create a date column. 

All the datatypes of the fields are cross-checked to make sure all the fields are having correct datatypes. 

The column ‘Other Sales’ is renamed to ‘Rest of the World Sales’. The field ‘Name’ is renamed to ‘Game Name’.

#### 4.2.1 Correlation Plot Development:
  -	First 2 parameters are created and named them as ‘Measure-1’ & ‘Measure-2’ and the values in these parameters are manually entered as lists. These are nothing but the names of the measure columns entered as the values for these parameters. 
  -	Two calculated measure columns are created and named as ‘Measure1’ & ‘Measure2’. These are created to dynamically hold the measure column that is selected in the above created parameters. Both of these variables consists of case statements.
  -	Next, ‘Dimension Param’ is created to give the user an option to visualize the correlation based on a particular dimension. The values in this parameter are also created by manually entering the different dimension names. A calculated column, ‘Dimension Selector’ is created for the purpose of dynamically holding the selected dimension from the ‘Dimension Param’.
  -	Measure1 and Measure2 columns are selected in to rows and columns and the aggregation is changed to Avg. The Dimension Selector variable is dragged and dropped at the ‘Detail’ level of the Marks pane and also in to the filters pane. 

<img width="655" alt="image" src="https://user-images.githubusercontent.com/98278525/193476854-6308a16a-5018-41ee-9252-724f71c74690.png">

#### 4.2.2. Lifetime Sales in Millions of Units Plot:
-	A parameter ‘Region Param’ is created and the region column names are manually entered as list. A calculated field ‘Region’ is created using a case statement to dynamically switch to the selected region from the ‘Region Param’. 
-	Year of Release and Region pills are selected in to the columns and rows pane respectively. The view is changed to bar plot from the Show Me pane.
-	Two filters are created based on the Genre and platform variables. 
-	The Region pill is dragged in to the Labels pane of the Marks shelf, to display the sales number on the corresponding bars. 

<img width="725" alt="image" src="https://user-images.githubusercontent.com/98278525/193476905-3a508ee8-5242-45d6-8416-732eeb930c8e.png">

#### 4.2.3. Platform based Share Chart:
-	First the fields ‘Platform’ and ‘Region’ are selected at a time by using the control key and the from the Show Me pane, the pie chart option is selected. Then the view is changed from ‘Standard’ to .Entire View’.
-	As the platform needs to be displayed, the platform field is then dragged and dropped on to the ‘Label’ option of the ‘Marks’ Shelf. The region column is dragged and dropped on to the ‘Label’ option of the ‘Marks’ Shelf.
-	To display the percentage of total sales, region column is again dropped on to the Label pane and then the down arrow  available with the pill is selected. Then, Quick Table Calculation->Percentage of Total are selected.

<img width="562" alt="image" src="https://user-images.githubusercontent.com/98278525/193476968-6273de37-d083-4a2a-8749-83fc0119bade.png">

#### 4.2.4. Sales in Millions of Units by Developer chart:
-	First the ‘Developer’ and ‘Region’ are selected simultaneously using the control key and then ‘Tree Map’ is chosen from the ‘Show Me’ pane.
-	Developer and region are dragged on to the ‘Label’ option of the ‘Marks’ Shelf.
-	To display the percentage of total sales, step number-3 from 3.2.3 is repeated.

<img width="664" alt="image" src="https://user-images.githubusercontent.com/98278525/193477024-f6ddd2f5-3ddf-4729-8a3b-2a158d001801.png">

#### 4.2.5. Dashboard Development:
-	All the plots are dragged and dropped on to the dashboard and adjusted. 
-	The Size option of the dashboard is changed from ‘Fixed’ to ‘Automatic’. Requirement R4 is achieved through this.
-	The filters are rearranged as required. As we need the bar plot to be acting as a filter for selecting years for the remaining 2 plots, the barplot is selected and the option ‘Use as Filter’ is selected from the dropdown options as shown below.

<img width="131" alt="image" src="https://user-images.githubusercontent.com/98278525/193477059-1d9fb5a2-613c-4467-934b-7f5d4633ad92.png">
-	Step-3 is repeated for the Platform based share pie plot.
-	As the correlation plot and the bar plot needs to be stable irrespective of the selections made on the other two plots, ‘Ignore Actions from the drop down menu of the plots is selected as shown in the below image. 
<img width="109" alt="image" src="https://user-images.githubusercontent.com/98278525/193477073-905f2b4c-e7f8-443e-9c5b-f41aa1eb7994.png">

<img width="452" alt="image" src="https://user-images.githubusercontent.com/98278525/193477084-c54306ce-2b1f-47a5-ae57-bd74f95f07c6.png">

#### 4.2.6. Additional Hover Chart:
The current dashboard is having the forward drill down. For example, if the user is looking for the top developers in Action and Adventure genres in the last 10 years, then he selects the 10 years bars in the bar plot and then select a particular platform in the pie chart. Then the top developers are displayed. But, if the user wanted to know how are the sales of the particular developer are scattered in other platforms, then our dashboard doesn’t answer that vital information. So, to overcome this, an additional hover chart is created and linked to the tree map to show up the pie chart consisting of developer sales based on platforms when the user hovers over the tree map.
-	A pie chart is created with same steps as of platform based pie chart creation. 
-	This chart is linked using the Tooltip of the tree map sheet using the sheet name parameter. 
<img width="495" alt="image" src="https://user-images.githubusercontent.com/98278525/193477335-22eec73c-4f16-4e7c-8c85-151a4bb584c5.png">

## 5. Power BI Dashboard Development:
Unlike in Tableau, Power BI gives the option of creating all the plots directly on the single report editor. During the Data model creation in the Power BI the dynamic measure columns Measure-1 and Measure-2 are created. After that the calculated fields Measure1 and Measure2 are created and linked to the previously created dynamic models by using a ‘switch’ statement. Then the correlation plot is created using these calculated columns just by dragging and dropping on to the report editor. Filters are added by using the available slicer option in the visualizations window. 

The bar plot, pie chart and the tree map are created by dragging and dropping the necessary columns on the report editor and then the filters are implemented using the slicer options available in the visualizations pane. Adjusted all the plots as necessary. All the charts are linked together using the ‘Edit interactions’ option under the ‘Format’ tab. In Tableau setting filters for each worksheet level and making a chart to ignore actions on the other charts are involved a lot of learning about how these options work. Whereas in Power BI all these options were neatly packaged under a single option called ‘Edit Interactions’ under format tab. 

<img width="506" alt="image" src="https://user-images.githubusercontent.com/98278525/193477385-3557b6c9-2063-412f-95b3-6dbf1936f3e1.png">

## 6. Observations:
While answering Q1 it is observed that there is weak to no correlation between the performance metrics user count vs critic count and user score vs critics score across different dimensions except ratings. However region wise sales are correlated with good R-squared values across different dimensions, which is expected. 

While answering Q2, it is found that across the globe (global region) and all the genres, with in the last 10 years, X360 emerged as most preferred platform. Developer ‘Treyarch’ is leading the development of different games in this platform with a share of 5% of industry sales within these years.


## 7. References
Data modelling in Power BI: Helpful tips & best practices (2021) Powerbi.com. Available at: https://community.powerbi.com/t5/Community-Blog/Data-Modelling-In-Power-BI-Helpful-Tips-amp-Best-Practices/ba-p/1977956 (Accessed: March 20, 2022).

Tutorial Gateway. (2018). Tableau Case Function. [online] Available at: https://www.tutorialgateway.org/tableau-case-function/ [Accessed 12 March. 2022].

Lymperopoulos, F. (2020) Keep up with dynamic data changes using dynamic parameters, Tableau. Available at: https://www.tableau.com/about/blog/2020/2/say-hello-dynamic-parameters (Accessed: April 20, 2022).

Docs.microsoft.com(2022) Change how visuals interact in a report - Power BI. [online] Available at: https://docs.microsoft.com/en-us/power-bi/create-reports/service-reports-visual-interactions?tabs=powerbi-desktop [Accessed 12 April 2022].

McKay, S. and CFA (2019). How To Control The Interactions Of Your Visuals In Power BI. [online] Enterprise DNA. Available at: https://blog.enterprisedna.co/how-to-control-the-interactions-of-your-visuals-in-power-bi/ [Accessed 12 Apr. 2022].

www.youtube.com. (n.d.). How to add a Viz. in Tooltip? | Tooltip Tips & Tricks | Tableau Interview Question. [online] Available at: https://www.youtube.com/watch?v=Y-sDN20il8E [Accessed 12 Apr. 2022].

Data modelling in Power BI: Helpful tips & best practices (2021) Powerbi.com. Available at: https://community.powerbi.com/t5/Community-Blog/Data-Modelling-In-Power-BI-Helpful-Tips-amp-Best-Practices/ba-p/1977956 (Accessed: April 20, 2022).
