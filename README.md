# Data Science Salary Estimator: Project Overview 
* I developed a tool that estimates data science salaries (MAE ~ $ 11K) to help data scientists negotiate their income during the hiring process.
* Scraped over 1000 job descriptions from Glassdoor using Python and Selenium.
* Engineered features from the text of each job description to quantify the value companies put on Python, Excel, AWS, and Spark. 
* Optimized Linear, Lasso, and Random Forest Regressors using GridSearchCV to reach the best model. 
* Built a client-facing API using Flask.

## Code and Resources Used 
**Python Version:** 3.7  
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, selenium, flask, json, pickle  
**For Web Framework Requirements:** ```pip install -r requirements.txt```  
**Scraper Reference:** https://github.com/arapfaik/scraping-glassdoor-selenium  
**Scraper Article:** https://towardsdatascience.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905  
**Flask Productionization:** https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2

## YouTube Project Walk-Through
https://www.youtube.com/playlist?list=PL2zq7klxX5ASFejJj80ob9ZAnBHdz5O1t

## Web Scraping
I utilized a web scraper to collect 1000 job postings from glassdoor.com. For each job, the following data points were extracted:
* Job title
* Salary Estimate
* Job Description
* Rating
* Company 
* Location
* Company Headquarters 
* Company Size
* Company Founded Date
* Type of Ownership 
* Industry
* Sector
* Revenue
* Competitors 

## Data Cleaning
After scraping the data, I cleaned it to ensure it was usable for the model. I implemented the following changes and created these variables:

* Parsed numeric data out of salary 
* Created columns for employer provided salary and hourly wages 
* Removed rows without salary 
* Parsed rating out of company text 
* Created a new column for company state 
* Added a column for if the job was at the company's headquarters 
* Transformed founded date into age of company 
* Created columns for specific skills listed in the job description:
    * Python  
    * R  
    * Excel  
    * AWS  
    * Spark 
* Created columns for simplified job title and seniority 
* Created a column for description length 

## EDA
I analyzed the distributions of the data and the value counts for various categorical variables. Below are highlights from the pivot tables. 

![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/salary_by_job_title.PNG "Salary by Position")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/positions_by_state.png "Job Opportunities by State")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/correlation_visual.png "Correlations")

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and test sets with a test size of 20%.   

I evaluated three different models using Mean Absolute Error (MAE). I chose MAE because it is easy to interpret and outliers are not particularly detrimental for this type of model.   

The three models tested were:
* Multiple Linear Regression - Baseline for the model
* Lasso Regression - Chosen because the sparse data from categorical variables often benefits from normalized regression.
* Random Forest - Selected due to its effectiveness with the sparsity associated with this dataset. 

## Model Performance
The Random Forest model outperformed the other approaches on the test and validation sets. 
* Random Forest: MAE = 11.22
* Linear Regression: MAE = 18.86
* Ridge Regression: MAE = 19.67

## Productionization 
In this step, I built a Flask API endpoint hosted on a local webserver. The API endpoint takes in a request with a list of values from a job listing and returns an estimated salary.

## Maintainer
**Gunesh Mahajan**  
Product Manager with 4 years of experience delivering customer-centric digital products across healthcare technology and consulting environments. I specialize in driving product strategy, roadmap planning, and data-driven decision-making. My technical background includes hands-on experience with SQL, product analytics, and Generative AI.

* Email: guneshmahajan574@gmail.com
* LinkedIn: https://www.linkedin.com/in/guneshm007/