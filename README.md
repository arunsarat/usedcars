## **Price prediction of Used Cars**

This project explores original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing. The goal of this project is to understand what factors make a car more or less expensive. After the model(s) built and trained, we should be provide clear recommendations to your  used car dealership -- as to what consumers value in a used car.

First step in this project is Data enrichment.

## **Data Enrichment**

Used car data set contains huge amounts of NaN values within 'VIN' column. And features like 'manufacturer', 'condition', 'cylinders' and 'VIN' have almost one-third NaN values.

Most strategies to fill the Null Value columns involve filling in with mean/median or mode if the features are of numerical types. We can also use interpolation techniques for numerical type columns. Since almost all the features with large Null values are categorical type features, we could use the following strategies

* Drop if the column is not significant for inference.
* Use K-Nearest Neighbors Imputation
* Fill with dominant category type.
* Introduce a new 'Default/Unknown' category and fill in Null values with it.

One of these strategies is used for a given feature based on the categorical value distribution. Based on the data values distribution for each column, here're the set of strategies selected to enrich the data.
| Column | Strategy|
| --- | --- |
| VIN | Drop |
| condition | Most Frequest Value Imputation |
| drive | Fill Unknown |
| size | Fill Unknonwn |
| cylinders | Interpolation |
| paint_color | Interpolation |
| Manufacturer | Interpolation with Feature Mapping |

***After data enrichment, we drop rest of the items with NaN values. We keep almost 80% of the data for data analysis after the data enrichment and clean up.***

### **Data Development and Validation split**
Using 'train_test_split' method provided by scikit-learn package, data is split into training and validatationd data sets in a 70-30 split.

### **Data Transformation**
Data Transformation phase within data analysis is a critical step in preparing the data data analysic. The data trasformation stratgies depend on the type of the feature. Numerical type features can be just scaled without any encoding. Binary features can be encoded in one-hot encoder or label encoder, while categorical features can transformed with Ordinal Encoder. 

Used cars dataset comprises of a large number of categorical type features. Hence Ordinal Encoder is used to transform the following features.
* model
* manufacturer
* region
* state
* cylinders
* drive
* size
* type
* transmission
* condition
* title_status
* paint_color

### **Dimensionality Reduction**
Feature selection is the process of reducing dimensionality so as to achieve
* Improved Model Performance
* Addressing curse of Dimensionality
* Cost & Efficiency

The cost of training increases exponentially with higher dimensionality of the data. Hence one of the important step in data analysis stage of M/L projects is to identify and remove less significant features with respect to prediction. In this project, we use and compare 3 methods for feature selection, followed by regression to train the model.
* Polynomial Feature Selection
* Sequential Feature Selection with Ridge Estimator
* Model Selection with Ridge Estimator

With each 'Feature Selection' strategy, we identify the most prominent features for predicting the price.

| Feature Selection Strategy | Prominent Features |
| --- | --- |
| Polynomial Feature Selection | condition^2, year state, manufacturer state, paint_color, state |
| Sequential Feature Selection | year, manufacturer, odometer, title_status, drive, state |
| Model Selection | region, year, condition, model, type. paint_color |

### **Model Training, Regression & Validation**

With each model, we do the following ot compare the models.
* Train the model with development data set, validate the model with validation data set.
* Use model to predict the 'price' of the used cars.
* Compare and visually represent validation data set with predicted data set.
* Compute the varation between validation pricing data and predicted 'price'

***Based on the data set used to train the models, Sequential Feature Selection followed by Ridge regression as estimator gave the best (least) Mean Squared Error between validation data set and predicted data set.***

