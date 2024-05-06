# Context
At W.W.Wood Products, the company uses SQL Server database to store internal data serving their applications. The company set up different processes and settings in the past to improve the server's performance, one of which is the index rebuild jobs. By schedule, these jobs run every night, and they are intensive processes. Currently, we have been reassessing the need to balance between the frequency/the amount of work spent on index maintenance and the server's performance. We learned that more workload on index rebuild might not yield better performance.
In theory, index maintenance every once a week is more appropriate than the daily approach that we are taking. However, we need empirical analysis to come to any conclusion for decision-making.
This project aims to use the collected data and compare the server's performance under two different conditions: when index maintenance was enabled (allow index rebuild every night during weekdays) and when it was disabled (no index rebuild during weekdays at all). Given we would control other variables on the server to be the same (workload, and other settings).

# Data
The project will use the workload and performance data for the following days:
| Condition A - Index maintenance Enabled  | Condition B - Index maintenance Disabled | Workload Same?                   | Performance Different? How much? |
| ---------------------------------------- | ---------------------------------------- | -------------------------------- | -------------------------------- |
| 1st_day_A.xlsx                           | 1st_day_B.xlsx                           |              ?                   |              ?                   |
| 2nd_day_A.xlsx                           | 2nd_day_B.xlsx                           |              ?                   |              ?                   |
| 3th_day_A.xlsx                           | 3th_day_B.xlsx                           |              ?                   |              ?                   |
| 4th_day_A.xlsx                           | 4th_day_B.xlsx                           |              ?                   |              ?                   |
| 5th_day_A.xlsx                           | 5th_day_B.xlsx                           |              ?                   |              ?                   |

1st_day_B.xlsx contains data on the first day since the index maintenance was disabled. 1st_day_A.xlsx contains the corresponding data when index maintenance was enabled to compare with. Apply the same logic to other days.

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
| Performance                              | Latch Wait                               | Latch Wait time                  |        
| Performance                              | Compilations                             | Compilations per batch           |        


# Project steps

# Objectives

# Timeline
