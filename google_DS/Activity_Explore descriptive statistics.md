# Activity: Explore descriptive statistics

## **Introduction**

Data professionals often use descriptive statistics to understand the data they are working with and provide collaborators with a summary of the relative location of values in the data, as well an information about its spread. 

For this activity, you are a member of an analytics team for the United States Environmental Protection Agency (EPA). You are assigned to analyze data on air quality with respect to carbon monoxide, a major air pollutant. The data includes information from more than 200 sites, identified by state, county, city, and local site names. You will use Python functions to gather statistics about air quality, then share insights with stakeholders.

## **Step 1: Imports** 


Import the relevant Python libraries `pandas` and `numpy`.


```python
# Import relevant Python libraries.
import numpy as np 
import pandas as pd 
### YOUR CODE HERE ###


```

The dataset provided is in the form of a .csv file named `c4_epa_air_quality.csv`. It contains a subset of data from the U.S. EPA. As shown in this cell, the dataset has been automatically loaded in for you. You do not need to download the .csv file, or provide more code, in order to access the dataset and proceed with this lab. Please continue with this activity by completing the following instructions.


```python
# RUN THIS CELL TO IMPORT YOUR DATA.

### YOUR CODE HERE
epa_data = pd.read_csv("c4_epa_air_quality.csv", index_col = 0)
```

<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about loading data in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `pandas` library that allows you to read in data from a .csv file and load it into a DataFrame. 

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `read_csv` function from the pandas `library`. The `index_col` parameter can be set to `0` to read in the first column as an index (and to avoid `"Unnamed: 0"` appearing as a column in the resulting DataFrame).

</details>

## **Step 2: Data exploration** 

To understand how the dataset is structured, display the first 10 rows of the data.


```python
# Display first 10 rows of the data.

### YOUR CODE HERE
epa_data.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date_local</th>
      <th>state_name</th>
      <th>county_name</th>
      <th>city_name</th>
      <th>local_site_name</th>
      <th>parameter_name</th>
      <th>units_of_measure</th>
      <th>arithmetic_mean</th>
      <th>aqi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-01-01</td>
      <td>Arizona</td>
      <td>Maricopa</td>
      <td>Buckeye</td>
      <td>BUCKEYE</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.473684</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-01-01</td>
      <td>Ohio</td>
      <td>Belmont</td>
      <td>Shadyside</td>
      <td>Shadyside</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.263158</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-01-01</td>
      <td>Wyoming</td>
      <td>Teton</td>
      <td>Not in a city</td>
      <td>Yellowstone National Park - Old Faithful Snow ...</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.111111</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-01</td>
      <td>Pennsylvania</td>
      <td>Philadelphia</td>
      <td>Philadelphia</td>
      <td>North East Waste (NEW)</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.300000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-01-01</td>
      <td>Iowa</td>
      <td>Polk</td>
      <td>Des Moines</td>
      <td>CARPENTER</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.215789</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018-01-01</td>
      <td>Hawaii</td>
      <td>Honolulu</td>
      <td>Not in a city</td>
      <td>Kapolei</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.994737</td>
      <td>14</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2018-01-01</td>
      <td>Hawaii</td>
      <td>Honolulu</td>
      <td>Not in a city</td>
      <td>Kapolei</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.200000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2018-01-01</td>
      <td>Pennsylvania</td>
      <td>Erie</td>
      <td>Erie</td>
      <td>NaN</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.200000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018-01-01</td>
      <td>Hawaii</td>
      <td>Honolulu</td>
      <td>Honolulu</td>
      <td>Honolulu</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.400000</td>
      <td>5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018-01-01</td>
      <td>Colorado</td>
      <td>Larimer</td>
      <td>Fort Collins</td>
      <td>Fort Collins - CSU - S. Mason</td>
      <td>Carbon monoxide</td>
      <td>Parts per million</td>
      <td>0.300000</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about exploratory data analysis in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `pandas` library that allows you to get a specific number of rows from the top of a DataFrame. 

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `head()` function from the `pandas` library.

</details>

**Question:** What does the `aqi` column represent?

Aqi is the EPA air quality indec or 'aqi'

Now, get a table that contains some descriptive statistics about the data.


```python
# Get descriptive stats.

### YOUR CODE HERE
epa_data.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>arithmetic_mean</th>
      <th>aqi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>260.000000</td>
      <td>260.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.403169</td>
      <td>6.757692</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.317902</td>
      <td>7.061707</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.200000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.276315</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.516009</td>
      <td>9.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.921053</td>
      <td>50.000000</td>
    </tr>
  </tbody>
</table>
</div>



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `pandas` library that allows you to generate a table of basic descriptive statistics about the numeric columns in a DataFrame.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `describe()` function from the `pandas` library.

</details>

**Question:** Based on the table of descriptive statistics, what do you notice about the count value for the `aqi` column?

th mean and the aqi are 260.0000, they are the same 

**Question:** What do you notice about the 25th percentile for the `aqi` column?

This is an important measure for understanding where the aqi values lie. 

Within the 25h percentile aqiis 2.000 this demonstarates 25% of the values are below or less than 2

**Question:** What do you notice about the 75th percentile for the `aqi` column?

This is another important measure for understanding where the aqi values lie. 

The 75h percentile aqi value is 9.000 so for the higher values, 25 percent of them are above 9 and the rest 75% are below 9, the 50th percentile lie between 2 and 9 

## **Step 3: Statistical tests** 

Next, get some descriptive statistics about the states in the data.


```python
# Get descriptive stats about the states in the data.

### YOUR CODE HERE
epa_data["state_name"].describe()
```




    count            260
    unique            52
    top       California
    freq              66
    Name: state_name, dtype: object



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `pandas` library that allows you to generate basic descriptive statistics about a DataFrame or a column you are interested in.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

 Use the `describe()` function from the `pandas` library. Note that this function can be used:
- "on a DataFrame (to find descriptive statistics about the numeric columns)" 
- "directly on a column containing categorical data (to find pertinent descriptive statistics)"

</details>

**Question:** What do you notice while reviewing the descriptive statistics about the states in the data? 

Note: Sometimes you have to individually calculate statistics. To review to that approach, use the `numpy` library to calculate each of the main statistics in the preceding table for the `aqi` column.

We have a count of 260 states, and 52 unique names, california is the state that occurs the most with a frequency of 66 

## **Step 4. Results and evaluation**

Now, compute the mean value from the `aqi` column.


```python
# Compute the mean value from the aqi column.

### YOUR CODE HERE
np.mean(epa_data["aqi"])
```




    6.757692307692308



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `numpy` library that allows you to get the mean value from an array or a Series of values.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `mean()` function from the `numpy` library.

</details>

**Question:** What do you notice about the mean value from the `aqi` column?

This is an important measure, as it tells you what the average air quality is based on the data.

the aqi mean is 6.76, the average aqi within the data in 6.76

Next, compute the median value from the aqi column.


```python
# Compute the median value from the aqi column.

### YOUR CODE HERE
np.median(epa_data['aqi'])

```




    5.0



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `numpy` library that allows you to get the median value from an array or a series of values.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `median()` function from the `numpy` library.

</details>

**Question:** What do you notice about the median value from the `aqi` column?

This is an important measure for understanding the central location of the data.

the median of the aqui value is 5.0, the other half of the values are below 5 

Next, identify the minimum value from the `aqi` column.


```python
# Identify the minimum value from the aqi column.

### YOUR CODE HERE
np.min(epa_data['aqi'])
```




    0



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `numpy` library that allows you to get the minimum value from an array or a Series of values.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `min()` function from the `numpy` library.

</details>

**Question:** What do you notice about the minimum value from the `aqi` column?

This is an important measure, as it tell you the best air quality observed in the data.

The smallest value we have is 0. 

Now, identify the maximum value from the `aqi` column.


```python
# Identify the maximum value from the aqi column.

### YOUR CODE HERE
np.max(epa_data['aqi'])

```




    50



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `numpy` library that allows you to get the maximum value from an array or a Series of values.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

  Use the `max()` function from the `numpy` library.

</details>

**Question:** What do you notice about the maximum value from the `aqi` column?

This is an important measure, as it tells you which value in the data corresponds to the worst air quality observed in the data.

the maximum aqi vlaue is 50, so within the states, one of them is out of the std at a high vlaue of 50, we can check if it is an outlier or the context of the data .

Now, compute the standard deviation for the `aqi` column.

By default, the `numpy` library uses 0 as the Delta Degrees of Freedom, while `pandas` library uses 1. To get the same value for standard deviation using either library, specify the `ddof` parameter to 1 when calculating standard deviation.


```python
# Compute the standard deviation for the aqi column.

### YOUR CODE HERE
np.std(epa_data['aqi'], ddof=1)
```




    7.0617066788207215



<details>
  <summary><h4><strong>Hint 1</strong></h4></summary>

Refer to the video section about descriptive statistics in Python.

</details>

<details>
  <summary><h4><strong>Hint 2</strong></h4></summary>

  There is a function in the `numpy` library that allows you to get the standard deviation from an array or a series of values.

</details>

<details>
  <summary><h4><strong>Hint 3</strong></h4></summary>

Use the `std()` function from the `numpy` library. Make sure to specify the `ddof` parameter as 1. To read more about this function,  refer to its documentation in the references section of this lab.

</details>

**Question:** What do you notice about the standard deviation for the `aqi` column? 

This is an important measure of how spread out the aqi values are.

The standard deviation is 7.06,t he vlaues are apread by this range 

## **Considerations**


**What are some key takeaways that you learned during this lab?**

[Write your response here. Double-click (or enter) to edit.]

**How would you present your findings from this lab to others? Consider the following relevant points noted by AirNow.gov as you respond:**
- "AQI values at or below 100 are generally thought of as satisfactory. When AQI values are above 100, air quality is considered to be unhealthy—at first for certain sensitive groups of people, then for everyone as AQI values increase."
- "An AQI of 100 for carbon monoxide corresponds to a level of 9.4 parts per million."

[Write your response here. Double-click (or enter) to edit.]

**What summary would you provide to stakeholders? Use the same information provided previously from AirNow.gov as you respond.**

[Write your response here. Double-click (or enter) to edit.]

**References**

[Air Quality Index - A Guide to Air Quality and Your Health](https://www.airnow.gov/sites/default/files/2018-04/aqi_brochure_02_14_0.pdf). (2014,February)

[Numpy.Std — NumPy v1.23 Manual](https://numpy.org/doc/stable/reference/generated/numpy.std.html)

US EPA, OAR. (2014, 8 July).[*Air Data: Air Quality Data Collected at Outdoor Monitors Across the US*](https://www.epa.gov/outdoor-air-quality-data). 

**Congratulations!** You've completed this lab. However, you may not notice a green check mark next to this item on Coursera's platform. Please continue your progress regardless of the check mark. Just click on the "save" icon at the top of this notebook to ensure your work has been logged.
