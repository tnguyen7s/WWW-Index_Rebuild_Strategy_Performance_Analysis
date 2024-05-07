# Context
At W.W.Wood Products, the company uses SQL Server database to store internal data serving their applications. The company set up different processes and settings in the past to improve the server's performance, one of which is the index rebuild jobs. By schedule, these jobs run every night, and they are intensive processes. Currently, we have been reassessing the need to balance between the frequency/the amount of work spent on index maintenance and the server's performance. We learned that the extra workload on index rebuild might not yield better performance.
In theory, index maintenance every once a week is more appropriate than the daily approach that we are taking. However, we need empirical analysis to come to any conclusion for decision-making.
This project aims to use the collected data and compare the server's performance under two different conditions: when index maintenance was enabled (allow index rebuild every night during weekdays) and when it was disabled (no index rebuild during weekdays at all). Given we would attempt to control other variables on the server to be the same (workload, and other settings).

# Data
The project will use the workload and performance data for the following days:
| Condition A - Index maintenance Enabled  | Condition B - Index maintenance Disabled | 
| ---------------------------------------- | ---------------------------------------- | 
| 1st_day_A.xlsx                           | 1st_day_B.xlsx                           |       
| 2nd_day_A.xlsx                           | 2nd_day_B.xlsx                           |           
| 3th_day_A.xlsx                           | 3th_day_B.xlsx                           |         
| 4th_day_A.xlsx                           | 4th_day_B.xlsx                           |            
| 5th_day_A.xlsx                           | 5th_day_B.xlsx                           | 

1st_day_B.xlsx contains data on the first day since the index maintenance was DISABLED. 1st_day_A.xlsx contains the corresponding data when index maintenance was ENABLED to compare with. Apply the same logic to other days.

Each excel file contains these data metrics:
| Supercategory by Workload or Performance | Supercategory by Resource                | Metric                           |
| ---------------------------------------- | ---------------------------------------- | -------------------------------- | 
| Workload                                 |                                          | Batch requests/sec               |     
| Workload                                 |                                          | User connections                 |         
| Performance                              | CPU                                      | SQL Server: Processor time       |         
| Performance                              | Memory                                   | SQL Server: Free memory          |          
| Performance                              | Memory                                   | Page reads/sec                   |        
| Performance                              | IO                                       | Disk avg read time               |        
| Performance                              | IO                                       | Disk avg write time              |        
| Performance                              | Latch                                    | Latch Wait time                  |        
| Performance                              | Compilations                             | Compilations per batch           |        


# Project milestones
We have foreseen the necessary steps to accomplish the projects (outlined below). As we move on, we may add changes to these steps or other parts in this document. In data analytics, it is also possible to come back to the previous step, such as data exploration can lead to some insights that take us back to the data processing step.
## 1. Data processing
To assist the data analytics, it is important to clean and transform the data to an appropriate format. Use a programming language (Python recommended) to process each file mentioned above as follows:
- For each sheet, averaging the values to the minute granularity.
- Join the metrics from all sheets in the file by the `Date (UTC)` column.
- Converts the `Date (UTC)` to `Date (Central Standard Time)`.
- Convert the `Free Memory` metric from Bytes to GB
- Multiply the `Compilations/batch` by 100
- Combine `Disk avg read time sql data 1` and `Disk avg read time sql data 2` into one column `Disk avg read time sql data` using a SUM
  
After finished processing all files in folder A:
- Concat the resulted data frames, export the concat dataframe to a CSV file, and name it as `A.csv`
- Load the data from the `A.csv` to a dataframe and filter the data on the dataframe to include only records between the timeframe 5 am to 4 pm. Export the result dataframe to a CSV file, and name it as `[Daytime]A.csv`

After finished processing all files in folder B:
- Concat the resulted data frames, export the concat dataframe to a CSV file, and name it as `B.csv`
- Load the data from the `B.csv` to a dataframe and filter the data on the dataframe to include only records between the timeframe 5 am to 4 pm. Export the result dataframe to a CSV file, and name it as `[Daytime]B.csv`

## 2. Data exploration
This step is necessary for further analysis and future choices of the types of hypothesis testing that best fit the data. For each variable:
-	Understand distribution (using histogram, box plots, or violins)
-	Identify unusual values during the day (very high/low values)
-	Identify any special relationships among the metrics
-	Others

## 3. Hypothesis testing
- From the data exploration above, determine an appropriate statistical test to test if there is a significant difference between the means of the two groups (with index rebuild jobs and without index rebuild jobs). For example, if data qualifies all assumptions of independent T-tests, we will use that type of test on the metric.
- There are 11 metrics and 5 days, thus we need a total of 55 tests.

Some useful references:
- Two means Difference Test Assumptions and Alternatives [https://www.mas.ncl.ac.uk/~njnsm/medfac/docs/skewness]
- GeeksForGeek is an exellent reference (brief concepts and examples with code illustration): [https://www.geeksforgeeks.org/mann-and-whitney-u-test/]

## 4. Data visualization
- To communicate the result to other stakeholders, we need a beautiful Tableau dashboard to display insights from data explorations and results from hypothesis testing. We will discuss the details as we move on to this step.

# Timeline and meetings
- Thursday 05/09/2024: hand the first version of the code for the 1st step Data Preprocessing. We will meet to review and clean up the code.
- Friday 05/06/2024: the company will upload the remaining datasets
- Monday 05/12/2024: deliver some of your findings on the 2nd step Data Exploration
- Thursday 05/16/2024: deliver other findings on the 2nd step Data Exploration and determine the types of tests for the 3rd step Hypothesis testing
- Sunday 05/19/2024: deliver your results on the 3rd step Hypothesis testing. Review and clean up the code.
- Monday 05/20/2024: discuss on the requirements of the 4th step Data visualization
- Friday 05/24/2024: deliver your first attempt on the dashboard. Receive feedback to fix
- Monday 05/27/2024: finalize the dashboard

# Objectives
You will help the company answer the question mentioned in the Context. In addition, you will gain experience on pandas (1. Data processing), matplotlib (2. Data exploration), hypothesis testing, and Tableau (4. Data visualization)


