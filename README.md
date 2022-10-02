## 1. Introduction
The dataset ‘Video Game Sales with Ratings’ is used for this coursework. It is taken from Kaggle.com and is available at https://www.kaggle.com/datasets/rush4ratio/video-game-sales-with-ratings?select=Video_Games_Sales_as_at_22_Dec_2016.csv. This dataset is originally web scraped from Metacritic website which maintains aggregated reviews of films, TV shows, music albums and video games.

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

4.2. Tableau Dashboard Implementation:
The cleaned dataset without any missing values and with the new ‘cluster’ column, which is now in csv format, is imported to the Tableau. The year is displayed as number(decimal) format. So, a new calculated field is created by using the original field to create a date column. 

All the datatypes of the fields are cross-checked to make sure all the fields are having correct datatypes. 

The column ‘Other Sales’ is renamed to ‘Rest of the World Sales’. The field ‘Name’ is renamed to ‘Game Name’.

4.2.1 Correlation Plot Development:
1.	First 2 parameters are created and named them as ‘Measure-1’ & ‘Measure-2’ and the values in these parameters are manually entered as lists. These are nothing but the names of the measure columns entered as the values for these parameters. 
2.	Two calculated measure columns are created and named as ‘Measure1’ & ‘Measure2’. These are created to dynamically hold the measure column that is selected in the above created parameters. Both of these variables consists of case statements.
3.	Next, ‘Dimension Param’ is created to give the user an option to visualize the correlation based on a particular dimension. The values in this parameter are also created by manually entering the different dimension names. A calculated column, ‘Dimension Selector’ is created for the purpose of dynamically holding the selected dimension from the ‘Dimension Param’.
4.	Measure1 and Measure2 columns are selected in to rows and columns and the aggregation is changed to Avg. The Dimension Selector variable is dragged and dropped at the ‘Detail’ level of the Marks pane and also in to the filters pane. 

<img width="655" alt="image" src="https://user-images.githubusercontent.com/98278525/193476854-6308a16a-5018-41ee-9252-724f71c74690.png">








