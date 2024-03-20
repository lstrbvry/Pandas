# Code For Merging Dataframes in Pandas
```
#I want to replace the c column of df1 with c column of df2
import pandas as pd

df1= {
  'name': ['a', 'b', 'c'],
  'a': [1, 2, 3],
  'b':[2, 4, 6], 
  'c':['','' ,''], 
}
df2 = {
  'name':['a', 'b', 'c', 'd'],
  'c':[3, '', 9, '']
}
df1['c'] = pd.to_numeric(df1['c'], errors='coerce')
df1 = pd.DataFrame(df1)
df2 = pd.DataFrame(df2)

df1_merged = df1.merge(df2, on=['name'], how='right', suffixes=('_df1', '_df2'))
df1['c'] = df1_merged['c_df2']
print(df1)
print(df1_merged)

output:
  name  a  b  c
0    a  1  2  3
1    b  2  4   
2    c  3  6  9
  name    a    b  c_df1 c_df2
0    a  1.0  2.0    NaN     3
1    b  2.0  4.0    NaN      
2    c  3.0  6.0    NaN     9
3    d  NaN  NaN    NaN      
```
## Challenged encountered
**Unable to merge column due to difference in type:**
* Col c in df1 and Col c in df2 are two different datatypes, one is a str, and the other an integer
* It appeared to be so minor that I initially ignored the warning message. I thought i was doing something wrong with the 'merge' method.(You see I did not read the error message carefully)
* When I learned the issue, the first thing I did was to search how to convert the col c in df1 to int, and with the help of chatgpt, used pd.to_numeric to finally convert it to int. With that, a major roadblock that stumped m for hours was gone.
* I now regained the power to manipulate the data. The rest is basically just merging columns and deleting unwanted columns

*There's really no better way to learn than discovering a problem you are interested in solving* 

