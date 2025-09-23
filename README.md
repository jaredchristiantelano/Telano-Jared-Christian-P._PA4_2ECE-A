# Telano-Jared-Christian-P._PA4_2ECE-A

This assignment applies different codes for data wrangling and visualization 

**Problem 1** 

This problem specifies some conditions to filter the dataframe and selects a few columns to be displayed. This problem mainly uses codes from the pandas library, such as df.loc[], to access rows, columns, and labels. 

**a.) Instru** 

First, to import pandas library, the following code below is executed. This gives access to your program to the funcionalities included in the library. Affixing 'pd' allows you to access the functionalities in the pandas library. 

```
import pandas as pd                    # Imports pandas library

```

To obtain the dataframe from an external file, pd.read_excel is used. This reads the uploaded Excel file and loads it into a pandas dataframe. The dataframe is then stored in the variable df. After that, it is displayed to check if it is already loaded. 
```
df = pd.read_excel('board2.xlsx')      # Reads the uploaded file that contains the dataframe
df                                     # Displays the dataframe
```

To create a sub-dataframe with only selected rows and columns through some conditions, the following code is executed. First, '.loc[]' is used to select rows and columns, with conditions enclosed within the brackets, that act like indices. The conditions that should be met are that the 'Track' should be 'Instrumentation', the 'Hometown' should be 'Luzon', and the score in the 'Electronics' subject should be greater than 70. The ampersand (&) indicates that these conditions must all be True to filter the students in the dataframe. After filtering the rows in the dataframe, a few columns are selected to be displayed in the output. These are 'Name', 'GEAS', and 'Electronics'. These sub-dataframe is stores under the variable 'Instru'. 
Code
```
Instru = df.loc[(df['Track'] == 'Instrumentation') & (df['Hometown'] == 'Luzon') & (df['Electronics'] > 70), ['Name', 'GEAS', 'Electronics']]
Instru

# Uses the function df.loc to filter the uploaded dataframe 
# First, it specifies the row conditions. Then, column names are selected, specifying which to display in the output
```

Output
```
	Name	GEAS	Electronics
0	  S1	  75	         89
7	  S8	  64	         81
29	 S30	  57	         81

```



**b.) Mindy** 


To create a sub-dataframe with different set of conditions, the following code is executed. First, a list containing the subject columns are created under the variable named 'score'. This will be used to calculate the student's average score.
```
score = ['Electronics', 'GEAS', 'Math', 'Communication']          # A sub-dataframe is created 
```

As used previously, '.loc[]' is used to filter the dataframe. The following conditions are used to filter rows: the student's average score must be greater than or equal to 55, 'Hometown' is equal to 'Mindanao', and 'Gender' is equal to 'Female'. To calculate the student's average score across 4 subjects, '.mean(axis=1)' is used to calculate the average score of the student row-wise, which is set by the condition enclosed in the parentheses (axis=1). The conditions are then combined using ampersand (&), which indicates that all conditions must be met to be True. After the filtering process, the columns 'Name', 'Track', and 'Electronics' are only displayed in the output. The sub-dataframe is stored under the variable named 'Mindy'. 
```
Mindy = df.loc[(df[subs].mean(axis=1) >= 55) & (df['Hometown'] == 'Mindanao') & (df['Gender'] == 'Female'), ['Name', 'Track', 'Electronics']]
Mindy

# Then, the mean of the sub-dataframe was calculated. The "axis=1" means the mean was calculated across the selected columns
# Then the following conditions are specified, such as the average score should be at least 55, hometown must be Mindanao, and the gender must be female
# Lastly, .loc is used so the selected columns are to be displayed after filtering the dataframe 
```

Output 
```
	Name	         Track	   Electronics
1	  S2	 Communication	            75
2	  S3   Instrumentation	            74
14	 S15  Microelectronics	            41
16	 S17  Microelectronics	            79
19	 S20	 Communication	            60

```


**Problem 2** 

This problem uses the same dataframe as Problem 1. The codes applied here are from matplotlib.plyplot library to visualize the data needed. This program visualizes how certain features such as track, gender, and hometown contributes to average grade. With this visualization, the little discrepancies between the average scores per subgroup imply that these selected attributes do not necessarily contribute to a higher average score. 

First, pyplot library is imported by executing the following code below. Affixing 'plt' allows access to the functionalities in the library. The functionalities under this library are for data visualization.  
```
import matplotlib.pyplot as plt            
# Imports pyplot library for data visualization 
```

After importing the library needed, the excel file containing the dataframe is read using pandas. It is then stored under the variable named 'df'. 
```
df = pd.read_excel('board2.xlsx')
# This reads the uploaded Excel file, loading it into a pandas dataframe
```

To obtain the average score of students across the four subjects, the mean of their scores are calculated and stored under a new column named 'Average'. 
```
df["Average"] = df[["Math","Electronics","GEAS","Communication"]].mean(axis=1)     
# A new column called 'Average' is created to store the mean grade
# Computes the average grade for each student, across the selected columns 
# axis=1 
```

To separate the students according to their attributes, df.groupby() is used to group them accordingly. Then the mean of the average score per student is calculated within that group. 
```
track = df.groupby("Track")["Average"].mean()              # Groups the students by 'Track' and calculates the mean of the averages per track 
gender = df.groupby("Gender")["Average"].mean()            # Groups the students by 'Gender' and calculates the mean of the averages per gender
hometown = df.groupby("Hometown")["Average"].mean()        # Groups the students by 'Hometown' and calculates the mean of the averages per hometown

# df.groupby() groups the rows by track, gender, and hometown
# Then, the average column is called, computing for the mean average per track, the mean average per gender, and the mean average per hometown 
```

A figure is created for plotting. The size of the figure is also indicated, which is 15 inches by 5 inches. 
```
plt.figure(figsize=(15,5))
# This creates the figure for plotting, indicating the size of the figure (15 inches by 5 inches) 
```

To visualize the data, a bar chart is used to see the relationship between the attributes and the average score. This creates the first subplot of the dataframe, showing the relationship between the chosen 'Track' and the average score of the student. In this code, the color of the bar chart, the title, and the labels are indicated. These also follow for the other two subplots, yet with different features of their bar charts. 
```
# Track
plt.subplot(1,3,1)                                                          # Creates the first plot 
track.plot(kind="bar", color="skyblue", edgecolor="black")                  # Creates a bar chart, specifying the colors used
plt.title("Average Grade by Track")                                         # Indicates the title of the chart 
plt.ylabel("Average Score")                                                 # Labels the y-axis 
plt.xticks(rotation=30)                                                     # Tilts the track titles in the x-axis to fit them in 
```

This shows the subplot for the relationship between 'Gender' and the average score. 
```
# Gender
plt.subplot(1,3,2)                                                          # Creates the second plot 
gender.plot(kind="bar", color="lightgreen", edgecolor="black")              # Creates a bar chart, specifying the colors used
plt.title("Average Grade by Gender")                                        # Indicates the title of the chart
plt.ylabel("Average Score")                                                 # Labels the y-axis
```

This shows the subplot for the relationship between 'Hometown' and the average score. 
```
# Hometown
plt.subplot(1,3,3)                                                          # Creates the third plot
hometown.plot(kind="bar", color="salmon", edgecolor="black")                # Creates a bar chart, specifying the colors used
plt.title("Average Grade by Hometown")                                      # Indicates the title of the chart
plt.ylabel("Average Score")                                                 # Labels the y-axis
```

This code displays the 3 subplots side by side. 
```
plt.show()                                                                  # Shows the 3 charts side by side 
```


<img width="967" height="421" alt="Screenshot 2025-09-23 025504" src="https://github.com/user-attachments/assets/000b33e8-e6b7-482b-8171-5b8210bc01b4" />

