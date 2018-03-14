# Data retriever benchmark

a simple test aims to finds slow parts in all data retriever engines




### Notes
- This test use `nyc-tree-count`__(226M)__ for large test and `phytoplankton-size` __(83MB)__ for small
- In further progress this test should use vertnet dataset
 

### Specifications


#### CSV Engine

##### The pipeline 

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
> both stats are sorted by [time per call in total time](https://jiffyclub.github.io/snakeviz/#interpreting-results)


from the performance charts and according to the stats of both the datasets

`auto_get_datatypes` at `engine.py` line : 217

`add_to_table` at `engine.py` line : 77

are the heavy parts in the csv engine pipeline

also despite `format_insert_value` at `csvengine.py` line :56 and `format_insert_value` at `engine.py` line :545

have short percall time, but they have 31.26s and 58.99 total time for 10947193  call which implies that it would make a huge different optimize them.

-----------------------------------------------------

#### JSON Engine

__phytoplankton-size__ dataset 

![Figure1.1](screenshots/json_small_1.png)

![Figure1.1](screenshots/json_small_2.png)

![Figure3.1](screenshots/json_small_3.png)

![Figure3.2](screenshots/json_small_4.png)

![Figure3.3](screenshots/json_large_1.png)

![Figure3.4](screenshots/json_large_2.png)

![Figure3.5](screenshots/json_large_3.png)

![Figure3.6](screenshots/json_large_4.png)

![Figure3.7](screenshots/json_small_stats.png)

![Figure3.8](screenshots/json_small_stats_2.png)

![Figure3.8](screenshots/json_large_stats_1.png)

from the above charts we can point to 

`format_insert_value` at `engine.py` line : 545 

`format_insert_value` at `jsonengine.py` line :73

`add_to_table` at `engine.py` line : 77

`get_insert_columns` at `table.py` line : 222

which are the main time consumers in the json engine

also json encoder and decoder takes about 18.97 and 7.532

--------------------------------------------------------

