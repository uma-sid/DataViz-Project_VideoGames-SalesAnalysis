# DataViz-Project_VideoGamesSales-Analysis
This is a Data Visualization Project using Tableau on Video Games Sales


1. Introduction
The dataset ‘Video Game Sales with Ratings’ is used for this coursework. It is taken from Kaggle.com and is available at https://www.kaggle.com/datasets/rush4ratio/video-game-sales-with-ratings?select=Video_Games_Sales_as_at_22_Dec_2016.csv. This dataset is originally web scraped from Metacritic website which maintains aggregated reviews of films, TV shows, music albums and video games.

The dataset consists of data related to sales (in millions of units) of different videogames released from 1996 to 2017. It also contains the score and ratins given by the Metacritic review team and the subscribers of Metacritic. 

1.1. Data
The dataset consists of the following columns. The columns highlighted in bold are the ones created using the existing columns. The original dataset consists of 16719 rows with 16 columns. 

Column Name	Description	Domain
Name	Name of the game	Nominal
Platform	Console on which the game is running	Nominal
Year_of_Release	Year of the game released	Date
Genre	Game’s category	Nominal
Publisher	Publisher	Nominal
NA_Sales	Game sales in North America (in millions of units)	Float [0-100]
EU_Sales	Game sales in the European Union (in millions of units)	Float [0-100]
JP_Sales	Game sales in Japan (in millions of units)	Float [0-100]
Other_Sales	Game sales in in the rest of the world (in millions of units)	Float [0-100]
Global_Sales	Total sales in the world (in millions of units)	Float [0-100]
Critic_Score	Aggregate score compiled by Metacritic staff	Float [0-100]
Critic_Count	The number of critics used in coming up with the critic score	Integer
User_Score	Score by Metacritic’s subscribers	Float [0-100]
User_Count	Number of users who gave the user score	Integer
Developer	Party responsible for creating the game	Nominal
Rating	The ESRB ratings (Eg. Everyone, Teen, Adults, etc)	Nominal
Measure1	Placeholder for dynamic aggregated measure value	Float [0-100]
Measure2	Placeholder for dynamic aggregated measure value	Float [0-100]
Region	Placeholder for dynamic aggregated measure value	Float [0-100]
Cluster	Cluster Number obtained from clustering implementation	Nominal

1.2. Persona and questions
XYZ is a mobile game development company looking for expanding their horizon to the pc and other gaming platforms. The Product development head of the company wanted to analyse the data answer the following questions. 

1.	Is there a correlation between the different performance metrics(eg. Critic Score,  User count etc) with respect to the available dimensions(eg. Genre, platform etc)?
2.	Who leads the development of the most preferred platform based games with in the last 10 years across different regions of the world?
Answering the question-1 gives the user a general idea of what metrics contribute to the success of a game. This analysis also gives the user, an understanding of the correlation of sales across different regions of the world. 
Answer the question-2, makes the user understand who their competitors are and what platform or genre they should target for the development of their initial launch in to video games industry. 

1.3. Requirements

Q1. Is there a correlation between the different performance metrics(eg. Critic Score,  User count etc) with respect to the available dimensions(eg. Cluster, Genre, platform etc)?

R1. To answer Q1, the user needs to visualize the variables critic count, user count, critic score, user score, sales across regions in a way that they convey the correlation between them. The user also needs to have an option to change the dimension variable to view the correlation with respect to different dimensions. For this, a correlation plot along with the trend line will be a good view with the options to select the necessary measures and dimensions. 
Q2. Who leads the development of the most preferred platform based games with in the last 10 years across different regions of the world?
R2. Answering Q2 needs, few visual charts that satisfies the requirements. First the user must have the option to select the regions, platform and genres of his choice. There must be the option to select the years of his interest, which is provided using the R3. Then the user must have the visualization of the sales according to the platform wise and then be able to select a particular platform from that plot. There needs a one more plot which then displays the top developers and their share in the total sales. To achieve this, we need a pie chart with the platform-based sales and then selecting a pie would then display the developers with highest sales in a tree map. 

R3.  An additional view of the video games lifetime sales and their year of release is a good choice to serve the purpose of displaying the sales of video games and also using this as a filter for the user to select the years of his choice. A bar plot with the years on the x-axis and the number of millions of units sold on the y-axis would be a very good visualization.  

R4. The developed dashboard should fit in to any screen resolution without any additional steps by the user.

R5. The user must have a have a basic understanding of correlation plots and the statistical aspects of the correlation plots like the R-squared and p-values. 

R6. The user must have the basic knowledge of using tableau dashboards including the presentation mode. 

R7. The user should have the basic understanding of how the drill down works when working with different interlinked charts.


















2. Design
A paper landscape is designed to illustrate how the intended solution will look and function. 

 


The paper landscape is designed to complain with the Jacques Bertin’s image theory, so that only one aspect of the data is concentrated at each step while designing the solution for question 2. So that the user can drill down the data step by step. Keeping in mind about the importance of the planar variables, the pie chart and the tree map are designed in the final dashboard so that they display the sales number first and then the percentage of total, which is a secondary information. The filters related to the correlation plot are situated along with it as they are specific to that plot. While rest of the filters are situated as universal as they belong to all the three remaining plots.

 

The important difference between the landscape and the final dashboard is the addition of an extra hover chart to answer relevant additional questions, which was initially never thought of. Also the addition of ‘cluster’ field in the Dimensions Param of the correlation plot was never in the plan during the prototype design. 

3. Implementation

The implementation of this dashboard involves three steps. 
1.	Cleaning the data and clustering using python.
2.	Creating the Tableau Dashboard
3.	Creating the same dashboard in Power BI.

3.1 Data cleaning and Clustering:
The original dataset consists of 16719 rows and 16 columns. But there are many missing values. So, to clean them, python is chosen. After cleaning, the dataset is left with 6825 rows without any missing values. Clustering the dataset is done to identify if there are any correlations between the performance metrics with respective to the similar clusters. 
First the dataset is loaded into a python dataframe and then the rows with missing values are dropped. Then, the dataframe is left with 6825 rows. All the numerical columns are scaled using MinMaxScaler()




 


As the dataset has categorical and numerical variables for clustering, KPrototypes clustering is the algorithm used for clustering the dataset. A range of clusters from 1 to 10 are tried to find the optimal number of clusters. The optimal number of clusters is found at 3 clusters. So, the clustering is done using the 3 as number of clusters. A new column names ‘cluster’ is added to the data and then the whole dataset is exported in to a CSV file which will be used for the Tableau and Power BI Dashboard preparation 
        


3.2. Tableau Dashboard Implementation:
The cleaned dataset without any missing values and with the new ‘cluster’ column, which is now in csv format, is imported to the Tableau. The year is displayed as number(decimal) format. So, a new calculated field is created by using the original field to create a date column. 

All the datatypes of the fields are cross-checked to make sure all the fields are having correct datatypes. 

The column ‘Other Sales’ is renamed to ‘Rest of the World Sales’. The field ‘Name’ is renamed to ‘Game Name’.

3.2.1 Correlation Plot Development:
1.	First 2 parameters are created and named them as ‘Measure-1’ & ‘Measure-2’ and the values in these parameters are manually entered as lists. These are nothing but the names of the measure columns entered as the values for these parameters. 
2.	Two calculated measure columns are created and named as ‘Measure1’ & ‘Measure2’. These are created to dynamically hold the measure column that is selected in the above created parameters. Both of these variables consists of case statements.
3.	Next, ‘Dimension Param’ is created to give the user an option to visualize the correlation based on a particular dimension. The values in this parameter are also created by manually entering the different dimension names. A calculated column, ‘Dimension Selector’ is created for the purpose of dynamically holding the selected dimension from the ‘Dimension Param’.
4.	Measure1 and Measure2 columns are selected in to rows and columns and the aggregation is changed to Avg. The Dimension Selector variable is dragged and dropped at the ‘Detail’ level of the Marks pane and also in to the filters pane. 
 
3.2.2. Lifetime Sales in Millions of Units Plot:
1.	A parameter ‘Region Param’ is created and the region column names are manually entered as list. A calculated field ‘Region’ is created using a case statement to dynamically switch to the selected region from the ‘Region Param’. 
2.	Year of Release and Region pills are selected in to the columns and rows pane respectively. The view is changed to bar plot from the Show Me pane.
3.	Two filters are created based on the Genre and platform variables. 
4.	The Region pill is dragged in to the Labels pane of the Marks shelf, to display the sales number on the corresponding bars. 
 

3.2.3. Platform based Share Chart:
1.	First the fields ‘Platform’ and ‘Region’ are selected at a time by using the control key and the from the Show Me pane, the pie chart option is selected. Then the view is changed from ‘Standard’ to .Entire View’.
2.	As the platform needs to be displayed, the platform field is then dragged and dropped on to the ‘Label’ option of the ‘Marks’ Shelf. The region column is dragged and dropped on to the ‘Label’ option of the ‘Marks’ Shelf.
3.	To display the percentage of total sales, region column is again dropped on to the Label pane and then the down arrow  available with the pill is selected. Then, Quick Table Calculation->Percentage of Total are selected.
 

3.2.4. Sales in Millions of Units by Developer chart:
1.	First the ‘Developer’ and ‘Region’ are selected simultaneously using the control key and then ‘Tree Map’ is chosen from the ‘Show Me’ pane.
2.	Developer and region are dragged on to the ‘Label’ option of the ‘Marks’ Shelf.
3.	To display the percentage of total sales, step number-3 from 3.2.3 is repeated.

 

3.2.5. Dashboard Development:
1.	All the plots are dragged and dropped on to the dashboard and adjusted. 
2.	The Size option of the dashboard is changed from ‘Fixed’ to ‘Automatic’. Requirement R4 is achieved through this.
3.	The filters are rearranged as required. As we need the bar plot to be acting as a filter for selecting years for the remaining 2 plots, the barplot is selected and the option ‘Use as Filter’ is selected from the dropdown options as shown below.
 
4.	Step-3 is repeated for the Platform based share pie plot.
5.	As the correlation plot and the bar plot needs to be stable irrespective of the selections made on the other two plots, ‘Ignore Actions from the drop down menu of the plots is selected as shown in the below image. 
 

 




3.2.6. Additional Hover Chart:
The current dashboard is having the forward drill down. For example, if the user is looking for the top developers in Action and Adventure genres in the last 10 years, then he selects the 10 years bars in the bar plot and then select a particular platform in the pie chart. Then the top developers are displayed. But, if the user wanted to know how are the sales of the particular developer are scattered in other platforms, then our dashboard doesn’t answer that vital information. So, to overcome this, an additional hover chart is created and linked to the tree map to show up the pie chart consisting of developer sales based on platforms when the user hovers over the tree map.
1.	A pie chart is created with same steps as of platform based pie chart creation. 
2.	This chart is linked using the Tooltip of the tree map sheet using the sheet name parameter. 
 


3.3. Power BI Dashboard Development:
Unlike in Tableau, Power BI gives the option of creating all the plots directly on the single report editor. During the Data model creation in the Power BI the dynamic measure columns Measure-1 and Measure-2 are created. After that the calculated fields Measure1 and Measure2 are created and linked to the previously created dynamic models by using a ‘switch’ statement. Then the correlation plot is created using these calculated columns just by dragging and dropping on to the report editor. Filters are added by using the available slicer option in the visualizations window. 
The bar plot, pie chart and the tree map are created by dragging and dropping the necessary columns on the report editor and then the filters are implemented using the slicer options available in the visualizations pane. Adjusted all the plots as necessary. All the charts are linked together using the ‘Edit interactions’ option under the ‘Format’ tab. In Tableau setting filters for each worksheet level and making a chart to ignore actions on the other charts are involved a lot of learning about how these options work. Whereas in Power BI all these options were neatly packaged under a single option called ‘Edit Interactions’ under format tab. 
 

4. Walkthrough
Answering Q1:
To answer Q1 the user needs to make use of the correlation plot by following the below mentioned steps.
a.	Select the Dimension param with which the user is looking to analyse the data
b.	Select the measure-1 and measure-2 from the dropdowns 
 
c.	selecting the necessary measures in both the measure-1 and measure-2 drop downs, so that they are selected on the y and x axis respectively.
d.	Hover over the trend line to see the R-squred and p values to identify the correlation between the measures. 
 
e.	R-squred value near to 1 indicates a strong correlation. But, the p-value indicates whether the R-squared value is significant or not. When the p-value is less than 0.05, then the R-squared value is considered to be significant. 

Answering Q2:
a.	Select the region, Genre and Platform of interest from the right side filters.
 

b.	Select the bars in the bar chart from 2006 to 2016 simply by using the mouse at a stretch with a single click select the 10 bars and release. Then the pie chart (platform based share plot) displays the values corresponding to the selection made here. Requirement R3 is met with this step.
 

c.	Thus the pie chart gives the most preferred platforms details.
d.	Now, click on the platforms (pies) needed. Then the Tree map displays the top developers for this selection. The user gets all the information here like the top developers and their sales and their percentage share of the total sales. This answers our Q2 and the R2 is also achieved successfully.
 
e.	Additionally we can hover over the tree map to see the particular developers total sales for the selected 10 years across different platforms. 

 


4.1. Observations:
While answering Q1 it is observed that there is weak to no correlation between the performance metrics user count vs critic count and user score vs critics score across different dimensions except ratings. However region wise sales are correlated with good R-squared values across different dimensions, which is expected. 

While answering Q2, it is found that across the globe (global region) and all the genres, with in the last 10 years, X360 emerged as most preferred platform. Developer ‘Treyarch’ is leading the development of different games in this platform with a share of 5% of industry sales within these years.


5. Reflective Discussion

The need for data cleaning is inevitable for any data related projects. Although tableau provides an advanced software solution in terms of a product called tableau prep, it would have been more elegant if the tableau prep is integrated with the tableau desktop. The learning curve involved is much steeper in tableau when compared to the Power BI. On the other hand Power BI is restricted only for windows, which make the mac users a herculean job to work on the Power BI. Indeed this course work is majorly done using a mac and a secondary windows laptop is used to implement the dashboard in power BI. The paper landscape is completely implemented without skipping any parts of it. However, upgrade to the prototype has become unavoidable to make the dashboard more elegant.

The implementation of variable selection dynamically has been a major learning during the implementation of this dashboard, without which the project would have been a mere static visualisation. Overall, the module provided great insights about the various principles of data visualization like the need for maximising the data ink ratio,  consistency between views, optimal use of different charts etc. In the near future, the skill of implementing visualisations using different data sources and also from multiple sources at the same time is taken as a personal learning objective. 







6. References
Data modelling in Power BI: Helpful tips & best practices (2021) Powerbi.com. Available at: https://community.powerbi.com/t5/Community-Blog/Data-Modelling-In-Power-BI-Helpful-Tips-amp-Best-Practices/ba-p/1977956 (Accessed: March 20, 2022).
Tutorial Gateway. (2018). Tableau Case Function. [online] Available at: https://www.tutorialgateway.org/tableau-case-function/ [Accessed 12 March. 2022].
Lymperopoulos, F. (2020) Keep up with dynamic data changes using dynamic parameters, Tableau. Available at: https://www.tableau.com/about/blog/2020/2/say-hello-dynamic-parameters (Accessed: April 20, 2022).
Docs.microsoft.com(2022) Change how visuals interact in a report - Power BI. [online] Available at: https://docs.microsoft.com/en-us/power-bi/create-reports/service-reports-visual-interactions?tabs=powerbi-desktop [Accessed 12 April 2022].
McKay, S. and CFA (2019). How To Control The Interactions Of Your Visuals In Power BI. [online] Enterprise DNA. Available at: https://blog.enterprisedna.co/how-to-control-the-interactions-of-your-visuals-in-power-bi/ [Accessed 12 Apr. 2022].
 www.youtube.com. (n.d.). How to add a Viz. in Tooltip? | Tooltip Tips & Tricks | Tableau Interview Question. [online] Available at: https://www.youtube.com/watch?v=Y-sDN20il8E [Accessed 12 Apr. 2022].
Data modelling in Power BI: Helpful tips & best practices (2021) Powerbi.com. Available at: https://community.powerbi.com/t5/Community-Blog/Data-Modelling-In-Power-BI-Helpful-Tips-amp-Best-Practices/ba-p/1977956 (Accessed: April 20, 2022).
![image](https://user-images.githubusercontent.com/98278525/193476137-aa59234a-043e-42fd-bdd4-e1414f917ce8.png)


