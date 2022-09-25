# Pyber_analysis ---

### Import required dependencies
from pandas import DataFrame
import pandas as pd
import os


## Deliverable 1: Collect the Data

To collect the data that you’ll need, complete the following steps:

1. Using the Pandas `read_csv` function and the `os` module, import the data from the `new_full_student_data.csv` file, and create a DataFrame called student_df. 

2. Use the head function to confirm that Pandas properly imported the data.

# Create the path and import the data
full_student_data = os.path.join('../Resources/new_full_student_data.csv')
student_df = pd.read_csv(full_student_data)
# Verify that the data was properly imported
student_df.head()
## Deliverable 2: Prepare the Data

To prepare and clean your data for analysis, complete the following steps:
    
1. Check for and remove all rows with `NaN`, or missing, values in the student DataFrame. 

2. Check for and remove all duplicate rows in the student DataFrame.

3. Use the `str.replace` function to remove the "th" from the grade levels in the grade column.

4. Check data types using the `dtypes` property.

5. Remove the "th" suffix from every value in the grade column using `str` and `replace`.

6. Change the grade colum to the `int` type and verify column types.

7. Use the head (and/or the tail) function to preview the DataFrame.
# Check for null values
student_df.isna().sum()
# Drop rows with null values and verify removal
student_df = student_df.dropna()
student_df.isna().sum()
# Check for duplicated rows
student_df.duplicated().sum()
# Drop duplicated rows and verify removal
student_df = student_df.drop_duplicates()
student_df.duplicated().sum()
# Check data types
student_df.dtypes
# Examine the grade column to understand why it is not an int
student_df['grade']
# Remove the non-numeric characters and verify the contents of the column
student_df['grade'] = student_df['grade'].str.replace('th', '')
student_df['grade']
# Change the grade column to the int type and verify column types
student_df['grade'] = student_df['grade'].astype(int)
student_df.dtypes
student_df.head()
## Deliverable 3: Summarize the Data

Describe the data using summary statistics on the data as a whole and on individual columns.

1. Generate the summary statistics for each DataFrame by using the `describe` function.

2. Display the mean math score using the `mean` function. 

2. Store the minimum reading score as `min_reading_score`.
# Display summary statistics for the DataFrame
student_df.describe()
# Display the mean math score using the mean function
student_df['math_score'].mean()

# Store the minimum reading score as min_reading_score
min_math_score = student_df['math_score'].min()
min_math_score
## Deliverable 4: Drill Down into the Data

Drill down to specific rows, columns, and subsets of the data.

To drill down into the data, complete the following steps:

1. Use `loc` to display the grade column.

2. Use `iloc` to display the first 3 rows and columns 3, 4, and 5.

3. Show the rows for grade nine using `loc`.

4. Store the row with the minimum overall reading score as `min_reading_row` using `loc` and the `min_reading_score` found in Deliverable 3.

5. Find the reading scores for the school and grade from the output of step three using `loc` with multiple conditional statements.

6. Using conditional statements and `loc` or `iloc`, find the mean reading score for all students in grades 11 and 12 combined.
# Use loc to display the grade column
student_df.loc[:,'grade']
# Use `iloc` to display the first 3 rows and columns 3, 4, and 5.
student_df.iloc[0:3,3:6]
# Select the rows for grade nine and display their summary statistics using `loc` and `describe`.
student_df.loc[student_df.grade == 9,:].describe()
# Store the row with the minimum overall reading score as `min_reading_row`
# using `loc` and the `min_reading_score` found in Deliverable 3.
min_reading_score = student_df["reading_score"].min()
min_reading_row = student_df.loc[student_df["reading_score"] == min_reading_score]
min_reading_row



# Use loc with conditionals to select all reading scores from 10th graders at Dixon High School.
student_df.loc[(student_df["grade"] == 10) & (student_df["school_name"] == "Dixon High School"),(["reading_score","school_name"])]


# Find the mean reading score for all students in grades 11 and 12 combined.
student_df.loc[student_df["grade"] > 10,["reading_score"]].mean()





## Deliverable 5: Make Comparisons Between District and Charter Schools

Compare district vs charter schools for budget, size, and scores.

Make comparisons within your data by completing the following steps:

1. Using the `groupby` and `mean` functions, look at the average reading and math scores per school type.

1. Using the `groupby` and `count` functions, find the total number of students at each school.

2. Using the `groupby` and `mean` functions, find the average budget per grade for each school type.
# Use groupby and mean to find the average reading and math scores for each school type.
school_type = student_df.groupby(["school_type"])["school_budget"].mean()
DataFrame(school_type)




# Use the `groupby`, `count`, and `sort_values` functions to find the
# total number of students at each school and sort from most students to least students.

student_count_df = student_df.groupby("school_name").count().sort_values(by = ["student_id"], ascending =[False])

student_count = student_count_df['student_id']



DataFrame(student_count)
    
                                      
#Find the average math score by grade for each school type by using the groupby and mean functions, as the following image shows:
math_score_average =  student_df.groupby(["school_type","grade"]).mean()
math_score_average_type = math_score_average['math_score']

DataFrame(math_score_average_type) 
# Deliverable 6: Summarize Your Findings
In the cell below, write a few sentences to describe any discoveries you made while performing your analysis along with any additional analysis you believe would be worthwhile.
*From the analysis, we have go through steps by steps analysis using all the following functions: read.csv, dtypes,replace, str, replace, sum, describe, mean, loc, iloc, groupby, count, mean, sort_values. It appears that the functions helps us manipulate the data such as summarizing the data, drilldown the data and comparing between the data.  
