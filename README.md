# Data retriever benchmark

A simple test aims to finds bottlenecks of data retriever


### Notes
- This test use `nyc-tree-count`__(226M)__ for large test and `phytoplankton-size` __(83MB)__ for small
- In further progress this test should use vertnet dataset

## Experiment

Note
> both stats are sorted by [time per call in total time](https://jiffyclub.github.io/snakeviz/#interpreting-results)


## Conclusion/Results

__Time for installing the dataset__

| Engine        | phytoplankton-size dataset    | nyc-tree-count dataset  |
| ------------- |:-------------:| -----:|
| csv      | 494 s| 563 s|
| json      | 528 s  |  615 s |
| xml | 591 s |    677 s |
| sqlite | 432 s  | 586 s |
| mysql |  586 s |  880 s |
| postgres | 559 s |  724 s|



----------------------------------
__Bottelnecks methods__

|# | method   | file  |
| ------------- |:-------------:| -----:|
|1 | format_insert_value | csvengine.py |
|2 | format_insert_value | engine.py |
|3 | correct_invalid_value | cleanup.py |
|4 | load_data | engine.py |
|5 | format_insert_value   | jsonengine.py |
|7 | add_to_table  | engine.py|
|8 | get_insert_columns  | table.py|
|9 | auto_get_datatypes  | engine.py|
|10 | format_insert_value  | xmlengine.py|
|11 | format_single_row  | xmlengine.py|
|12 | < listcomp:104 > | engine.py|
|13 | values_from_line | table.py|
|14 | < listcomp:734 >  | engine.py|
|15 | executemany | engine.py|
|16 | format_insert_value | postgres.py|



----------------------------------
__Engines sorted by performance(best-to-worst)__

|#  | Engine  |
|---|:-------:|
| 1 | CSV     |
| 2 | SQLITE  |
| 3 | JSON    |
| 4 | XML     |
| 5 | POSTGRES|
| 6 | MYSQL   |

#### CSV Engine


__phytoplankton-size__ dataset 

![Figure1.1](screenshots/csv_small_1.png)

![Figure1.2](screenshots/csv_small_2.png)

![Figure1.3](screenshots/csv_small_3.png)

![Figure1.4](screenshots/csv_small_4.png)


__nyc-tree-count__  dataset 


![Figure2.1](screenshots/csv_large_1.png)


![Figure2.1](screenshots/csv_large_2.png)
 

![Figure2.1](screenshots/csv_small_stats.png)

![Figure2.1](screenshots/csv_large_stats.png)


-----------------------------------------------------

#### JSON Engine

__phytoplankton-size__ dataset 

![Figure1.1](screenshots/json_small_1.png)

![Figure1.2](screenshots/json_small_2.png)

![Figure3.3](screenshots/json_small_3.png)

![Figure3.4](screenshots/json_small_4.png)

__nyc-tree-count__  dataset 

![Figure3.5](screenshots/json_large_1.png)

![Figure3.6](screenshots/json_large_2.png)

![Figure3.7](screenshots/json_large_3.png)

![Figure3.8](screenshots/json_large_4.png)

![Figure3.9](screenshots/json_small_stats.png)

![Figure3.9.1](screenshots/json_small_stats_2.png)

![Figure3.9.2](screenshots/json_large_stats_1.png)


--------------------------------------------------------


#### XML Engine

__phytoplankton-size__ dataset 

![Figure4.1](screenshots/xml_small_1.png)

![Figure4.2](screenshots/xml_small_2.png)

![Figure4.3](screenshots/xml_small3.png)

![Figure4.4](screenshots/xml_small_4.png)

![Figure4.5](screenshots/xml_small_5.png)

__nyc-tree-count__  dataset 

![Figure4.6](screenshots/xml_large_1.png)

![Figure4.7](screenshots/xml_large_2.png)

![Figure4.8](screenshots/xml_large_3.png)

![Figure4.9.1](screenshots/xml_stats_small.png)

![Figure4.9.2](screenshots/xml_stats_small2.png)

![Figure4.9.3](screenshots/xml_large_stats1.png)

![Figure4.9.4](screenshots/xml_large_stats2.png)



------------------------------------


### SQLITE engine

__phytoplankton-size__ dataset 

![Figure5.1](screenshots/sqlite_small_1.png)

![Figure5.2](screenshots/sqlite_small_2.png)

![Figure5.3](screenshots/sqlite_small_3.png)

![Figure5.4](screenshots/sqlite_small_4.png)

__nyc-tree-count__  dataset 

![Figure5.6.1](screenshots/sqlite_large_1.png)

![Figure5.6.2](screenshots/sqlite_large_2.png)

![Figure5.6.3](screenshots/sqlite_large_3.png)

![Figure5.6.4](screenshots/sqlite_large_4.png)

![Figure5.7.1](screenshots/sqlite_stats_1.png)

![Figure5.7.1](screenshots/sqlite_stats_2.png)

![Figure5.7.1](screenshots/sqlite_stats_3.png)

![Figure5.7.1](screenshots/sqlite_stats_4.png)


--------------------------------------

### MYSQL engine

__phytoplankton-size__ dataset 

![Figure5.1](screenshots/mysql_small_1.png)

![Figure5.2](screenshots/mysql_small_2.png)

![Figure5.3](screenshots/mysql_small_3.png)


__nyc-tree-count__  dataset 

![Figure5.6.1](screenshots/mysql_large_1.png)

![Figure5.6.2](screenshots/mysql_large_2.png)

![Figure5.6.3](screenshots/mysql_large_3.png)

![Figure5.6.4](screenshots/mysql_large_4.png)

![Figure5.7.1](screenshots/mysql_stats_1.png)

![Figure5.7.2](screenshots/mysql_stats_2.png)

![Figure5.7.3](screenshots/mysql_stats_3.png)

![Figure5.7.4](screenshots/mysql_stats_4.png)


--------------------------------------



### POSTGRESQL engine

__phytoplankton-size__ dataset 

![Figure5.1](screenshots/postgres_small_1.png)

![Figure5.2](screenshots/postgres_small_2.png)

![Figure5.3](screenshots/postgres_small_3.png)

![Figure5.4](screenshots/postgres_small_4.png)

![Figure5.4](screenshots/postgres_small_5.png)


__nyc-tree-count__  dataset 

![Figure 7.6.1](screenshots/postgres_large_1.png)

![Figure 7.6.2](screenshots/postgres_large_2.png)

![Figure 7.6.3](screenshots/postgres_large_3.png)

![Figure 7.7.1](screenshots/postgres_stats_1.png)

![Figure5.7.1](screenshots/postgres_stats_2.png)

![Figure5.7.1](screenshots/postgres_stats_3.png)

![Figure5.7.1](screenshots/postgres_stats_4.png)

-------------------------------------


TODO:

- Add instalation guide to readme

- Improve design and workflow

- Add dynamic datasetnames 

- Live preview depolyment

- Add conclusion