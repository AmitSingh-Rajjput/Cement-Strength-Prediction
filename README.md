# Cement-Strength-Prediction

## Problem Description 
To build a regression model to predict the concrete compressive strength of cement based on the different features in the training data.

## Language Used - Python
## Deployed on - Heroku
## Framework - Flask
## Tools - PyCharm
## Algorihtms - K-Mean Clustring, Random Forest Regressor and Linear Regression
## Accuracy Metric - R Squared , Adj R squared

## Data Description 

Given is the variable name, variable type, the measurement unit and a brief description.  
The concrete compressive strength is the regression problem.

1: Cement (component 1) quantitative, kg in a m3 mixture.It is an Input Variable. 

2: Blast Furnace Slag (component 2) quantitative ,kg in a m3 mixture. Input Variable-- Blast furnace slag is a nonmetallic coproduct produced in the process. It consists primarily of silicates, aluminosilicates, and calcium-alumina-silicates 

3: Fly Ash (component 3) quantitative ,kg in a m3 mixture . Input Variable- it is a coal combustion product that is composed of the particulates (fine particles of burned fuel) that are driven out of coal-fired boilers together with the flue gases.  

4: Water (component 4) quantitative ,kg in a m3 mixture . Input Variable 

5: Superplasticizer (component 5) ,quantitative ,kg in a m3 mixture . Input Variable--Superplasticizers (SP's), also known as high range water reducers, are additives used in making high strength concrete. 

6: Coarse Aggregate (component 6) ,quantitative kg in a m3 mixture . Input Variable-- construction aggregate, or simply "aggregate", is a broad category of coarse to medium grained particulate material used in construction, including sand, gravel, crushed stone, slag, recycled concrete and geosynthetic aggregates 

7: Fine Aggregate (component 7) ,quantitative ,kg in a m3 mixture . Input Variable—Similar to coarse aggregate, the constitution is much finer. 

8:Age ,quantitative ,Day (1~365) . Input Variable 

9:Concrete compressive strength ,quantitative ,MPa . Output Variable 

## Data Validation  

In this step, we perform different sets of validation on the given set of training files.   

1:Name Validation- We validate the name of the files based on the given name in the schema file. We have created a regex pattern as per the name given in the schema file to use for validation. After validating the pattern in the name, we check for the length of date in the file name as well as the length of time in the file name. If all the values are as per requirement, we move such files to "Good_Data_Folder" else we move such files to "Bad_Data_Folder." 

 

2:Number of Columns - We validate the number of columns present in the files, and if it doesn't match with the value given in the schema file, then the file is moved to "Bad_Data_Folder." 

 

 

3:Name of Columns - The name of the columns is validated and should be the same as given in the schema file. If not, then the file is moved to "Bad_Data_Folder". 

 

4:The datatype of columns - The datatype of columns is given in the schema file. This is validated when we insert the files into Database. If the datatype is wrong, then the file is moved to "Bad_Data_Folder". 

 

 

5:Null values in columns - If any of the columns in a file have all the values as NULL or missing, we discard such a file and move it to "Bad_Data_Folder". 


## Data Insertion in Database 

  

1) Database Creation and connection - Create a database with the given name passed. If the database is already created, open the connection to the database.  

2) Table creation in the database - Table with name - "Good_Data", is created in the database for inserting the files in the "Good_Data_Folder" based on given column names and datatype in the schema file. If the table is already present, then the new table is not created and new files are inserted in the already present table as we want training to be done on new as well as old training files.      

3) Insertion of files in the table - All the files in the "Good_Data_Folder" are inserted in the above-created table. If any file has invalid data type in any of the columns, the file is not loaded in the table and is moved to "Bad_Data_Folder". 


## Model Training  

1) Data Export from Db - The data in a stored database is exported as a CSV file to be used for model training. 

2) Data Preprocessing   

   a) Check for null values in the columns. If present, impute the null values using the KNN imputer 

   b) transform the features using log transformation 

   c) Scale the training and test data separately  

3) Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. 

   To train data in different clusters. The Kmeans model is trained over preprocessed data and the model is saved for further use in prediction. 

4) Model Selection - After clusters are created, we find the best model for each cluster. We are using two algorithms, "Random forest Regressor" and “Linear Regression”. For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the Rsquared scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. 

## Prediction

Data Export from Db - The data in the stored database is exported as a CSV file to be used for prediction.
Data Preprocessing

a) Check for null values in the columns. If present, impute the null values using the KNN imputer.

b) Check if any column has zero standard deviation, remove such columns as we did in training.

Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.

Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.

Once the prediction is made for all the clusters, the predictions along with the Wafer names are saved in a CSV file at a given location and the location is returned to the client.

Deployment
We will be deploying the model to the Heroku Cloud platform.

## Advantage of Heroku:

1: Beginner and start-up-friendly

2: It allows you to create a new server in just 10 seconds by using the interface of Heroku Command Line.

3: This cloud computing platform takes care of patching systems and keeping everything healthy.

4: A range of automated functionalities including the scaling, configuration, setup, and others

5: Easy integration with other AWS products.

## Output:

After compilation you can see this type of interface. Where you can give Custom files path for prediction or Default File prediction.

![ML2](https://user-images.githubusercontent.com/66250589/114582964-baf02c00-9c9e-11eb-94b0-366c3c54bc3b.PNG)







