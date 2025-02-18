# Beer Restaurant Success

## Project Outline

### Topic
The topic of interest for this project is using beer permit data to create a machine learning model that can predict the success of beer business locations in the Nashville area. This was chosen as the topic because we would like to know what the best locations would be for opening a bar that serves beer.

### Dataset description
The dataset, [Beer_Permit_Locations.csv](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/main/Beer_Permit_Locations.csv), was obtained from the [Data.Nashville.gov](https://data.nashville.gov/) website. Each row of this dataset displays permit information for various beer-serving businesses in the Nashville area.

#### Variables of Interest
- permit_number
- permit_subtype
- date_entered
- date_issued
- business_name
- zip
- latitude
- longitude
- permit_duration

#### Demographics Dataset
[all_demographic_data_merged.csv](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/main/Resources/all_demographic_data_merged.csv) shows various demographic, education, and income information for people living in Davidson county. This data was obtained from [Census.gov](https://www.census.gov/).

#### Variables of Interest
- zip code
- total population
    - split into male and female
- 18+ population
    - split into male and female
- 18-24 education level
    - split into not high school graduate, high school graduate, and Bachelor's degree or higher
- 25-34 education level
    - split into not high school graduate, high school graduate, and Bachelor's degree or higher
- 35-44 education level
    - split into not high school graduate, high school graduate, and Bachelor's degree or higher
- 65 and up education level
    - split into not high school graduate, high school graduate, and Bachelor's degree or higher
- average household income     

### Question to Answer
Based off of Beer Permit and demographic data, in which zip code will one be more successful when opening a beer serving establishment in Davidson County?

### Technologies Used

#### Data Cleaning and Analysis
Pandas will be used to clean the data and perform an exploratory analysis. Further analysis will be completed using Python.

#### Database Storage
pgAdmin is the database we intend to use, and we will integrate Flask to display the data.  A sample of the initial cleaned dataset was taken to upload to the created database in PostgresSQL.  This database will be used to feed data into the initial machine learning algorithm.  Additional updates will follow pending this initial test. 

#### Machine Learning
Scikit-Learn is the ML library we'll be using to create a classifier. We first used an unsupervised ML model, but after working through the model we discovered a supervised, Random Forest model, would be better suited for this project.

#### Dashboard
In addition to using a Flask template, we will also integrate D3.js for a fully functioning and interactive dashboard. The dashboard will be hosted on Tableau.  

### Database Creation
    • Import data using PGAdmin server instance on AWS.  
    • Use S3 bucketing to house datasets for public use
    • Data is joined using a inner join on zip codes

AWS is being used with S3 bucket to house the dataset.  PGAdmin is used to create the table structure, primary keys, set up foreign key and joins on zip_code for each of two tables.  The table names are beer_permit_locations and demographics.  beer_permit_locations data is obtained from data.nashville.gov included the beer permit locations.  The data set is called with an API and transformed into a usable form using Jupyter Notebook.  Demographics data was obtained from census.gov.  This data is static, without the ability to update automatically due to limitations of the website.  A separate dataset was obtained for each of three areas of interest for Nashville area zip codes.  The datasets were cleaned and transformed using Jupyter Notebook.  All three were merged on zip code from each dataset.  This gave the project two datasets for continued use.  The datasets have been set up with a foreign key relationship on zip code in PGAdmin and joined on this same column.

ERD
![ERD](https://user-images.githubusercontent.com/79231355/128651591-c4f0c780-0c70-4a2a-b7c9-aec99b44e341.png)

### Machine Learning Model

#### Description of preliminary data preprocessing: 
Data preprocessing was performed using Jupyter Notebook and Pandas.   Data was then scaled by importing StandardScaler from sklearn.preprocessing. 

#### Description of feature engineering and feature selection, including their decision-making process:
For the feature engineering, we wanted to look at factors that attribute to the success of business serving beer.  Various data points were considered and analyzed to determine a correlation.  The group decided that population, zip code, average household income and permit duration are the major factors of consideration.  
Feature selection was done through data analysis and visualizations.  Preliminary assumptions were made that needed to be proven accurate with the selected supervised model.  This required a binary data set for the model, which was created and added to the dataframe.  

#### Explanation of model choice, including limitations and benefits:
We utilized an Unsupervised Machine Learning Model. We used this model to transform the data to create an intuitive representation for the analysis. We also used the unsupervised Machine Learning Model to determine patterns in our data by clustering. A benefit to using the Unsupervised Machine Learning model is that it looks at the data, rather than taking in pairing of inputs and outputs from the data, which would not have been possible with our data set. 

#### Explanation of changes in model choice
After careful consideration of this model, the team determined a supervised model would be of better utilization for this project.  Assumptions were made through data analysis and visualizations that needed to be proven correct using supervised learning.  The model used is Random Forest.  This model allows for multiple features and large datasets by randomly sampling each feature.  These samples are weak learners, but become strong learners when combined.  These models resist overfitting and can rank the importance of input variables.  Disadvantages include limitation to the selection of parameters, but can be offset by boosting/bootstrapping. 

#### Description of how data was split into training and testing sets:
Data was split into training and testing sets using train_test_split at the default rate 

#### Description of current accuracy score. Additionally, the model obviously addresses the question or problem the team is solving.
The current accuracy of the model is 74%.  Further tuning may be needed to improve this number, if possible.  However, trial and error in feature selection has been performed to achieve the current result.  For the purposes of business success probability, this model should be sufficiently accurate.  The model accurately supports the question the team is solving. 

### Dashboard

The Dashboard is interactive and fully functioning. Visualizations can be altered by filtering out selected data, such as permit type and zip code.

![Dashboard](https://user-images.githubusercontent.com/79758494/129497690-13d7de8b-3df7-4a1e-9974-7c46823ec6ea.PNG)

https://public.tableau.com/views/Beer_Restaurant_Success_Visualizations_16288178489470/BeerSuccess?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link

#### Initial Visualizations
4 starting visualizations were created in Tableau using the [beer_permit_data_V1.csv](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/Visualizations/beer_permit_data_V1.csv) dataset. These visualizations can be seen in the screenshots below and in this [Tableau workbook](https://public.tableau.com/views/Beer_Restaurant_Success_Visualizations/PermitSubtypeBreakdown?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link):
![](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/Visualizations/Viz%20Screenshots/image%201.png)
![](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/Visualizations/Viz%20Screenshots/image%202.png)
![](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/Visualizations/Viz%20Screenshots/image%203.png)
![](https://github.com/HannaKim4673/Beer_Restaurant_Success/blob/Visualizations/Viz%20Screenshots/image%204.png)

#### Tools Used
* Visualizations from Tableau
* Dashboard will be hosted on Tableau

### Analysis Results
We found that the further away from downtown Nashville a beer-serving business is located, the longer that business has a permit. It should be noted that data is limited to current active permits in Davidson county. Also, our results showed that a person interested in establishing a beer-serving business away from downtown Nashville needs to consider the desires of local populations, since different demographic groups have different desires.

### Further Analysis Recommendations
When measuring “success”, there are many different ways to measure that. In our analysis, we used active permit duration (by days) to measure success. For future analysis, we recommended using multiple different measures of success. On top of active permit duration, using other datasets such as review data (from Yelp or Google) and revenue data could help a model better predict whether or not a beer-serving business will end up being successful.

### Things We Would've Done Differently
Looking back at our project, there are a few things that we would have done differently. First, we would have found and added rent data by zip code. Another thing we could've done in addition to our current data use hotel and short term rental datasets and map them. According to visitmusiccity.com, in 2019 there were 16.1 million visitors to Nashville. If an establishment were looking for a new location to open and be successful, having this data available could be impactful. Also, we could have taken time experimenting with additional machine learning models. 

## Presentation
Here is a link to our presentation: https://docs.google.com/presentation/d/1ncMNHN-_4Yj5ERpOJf3xiXUV8s-9Rn6viUx6BdiPeBo/edit?usp=sharing

It can also be accessed as a powerpoint in the main branch.
