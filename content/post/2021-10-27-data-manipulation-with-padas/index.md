---
title: Data manipulation with padas
author: ''
date: '2021-10-27'
slug: data-manipulation-with-padas
categories:
  - Python
tags:
  - DataCamp
---


```python
##Inspecting a DataFrame
```


```python
import pandas as pd
```


```python
## Load dataset homelessness
homelessness = pd.read_csv('homelessness.csv')  
```


```python
# Print the head of the homelessness data
print(homelessness.head())
```

       Unnamed: 0              region       state  individuals  family_members  \
    0           0  East South Central     Alabama       2570.0           864.0   
    1           1             Pacific      Alaska       1434.0           582.0   
    2           2            Mountain     Arizona       7259.0          2606.0   
    3           3  West South Central    Arkansas       2280.0           432.0   
    4           4             Pacific  California     109008.0         20964.0   
    
       state_pop  
    0    4887681  
    1     735139  
    2    7158024  
    3    3009733  
    4   39461588  
    


```python
# Print information about homelessness
print(homelessness.info())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 51 entries, 0 to 50
    Data columns (total 6 columns):
    Unnamed: 0        51 non-null int64
    region            51 non-null object
    state             51 non-null object
    individuals       51 non-null float64
    family_members    51 non-null float64
    state_pop         51 non-null int64
    dtypes: float64(2), int64(2), object(2)
    memory usage: 2.5+ KB
    None
    


```python
# Print the shape of homelessness
print(homelessness.shape)
```

    (51, 6)
    


```python
# Print a description of homelessness
print(homelessness.describe())
```

           Unnamed: 0    individuals  family_members     state_pop
    count   51.000000      51.000000       51.000000  5.100000e+01
    mean    25.000000    7225.784314     3504.882353  6.405637e+06
    std     14.866069   15991.025083     7805.411811  7.327258e+06
    min      0.000000     434.000000       75.000000  5.776010e+05
    25%     12.500000    1446.500000      592.000000  1.777414e+06
    50%     25.000000    3082.000000     1482.000000  4.461153e+06
    75%     37.500000    6781.500000     3196.000000  7.340946e+06
    max     50.000000  109008.000000    52070.000000  3.946159e+07
    


```python
# Print the values of homelessness
print(homelessness.values)

# Print the column index of homelessness
print(homelessness.columns)

# Print the row index of homelessness
print(homelessness.index)
```

    [[0 'East South Central' 'Alabama' 2570.0 864.0 4887681]
     [1 'Pacific' 'Alaska' 1434.0 582.0 735139]
     [2 'Mountain' 'Arizona' 7259.0 2606.0 7158024]
     [3 'West South Central' 'Arkansas' 2280.0 432.0 3009733]
     [4 'Pacific' 'California' 109008.0 20964.0 39461588]
     [5 'Mountain' 'Colorado' 7607.0 3250.0 5691287]
     [6 'New England' 'Connecticut' 2280.0 1696.0 3571520]
     [7 'South Atlantic' 'Delaware' 708.0 374.0 965479]
     [8 'South Atlantic' 'District of Columbia' 3770.0 3134.0 701547]
     [9 'South Atlantic' 'Florida' 21443.0 9587.0 21244317]
     [10 'South Atlantic' 'Georgia' 6943.0 2556.0 10511131]
     [11 'Pacific' 'Hawaii' 4131.0 2399.0 1420593]
     [12 'Mountain' 'Idaho' 1297.0 715.0 1750536]
     [13 'East North Central' 'Illinois' 6752.0 3891.0 12723071]
     [14 'East North Central' 'Indiana' 3776.0 1482.0 6695497]
     [15 'West North Central' 'Iowa' 1711.0 1038.0 3148618]
     [16 'West North Central' 'Kansas' 1443.0 773.0 2911359]
     [17 'East South Central' 'Kentucky' 2735.0 953.0 4461153]
     [18 'West South Central' 'Louisiana' 2540.0 519.0 4659690]
     [19 'New England' 'Maine' 1450.0 1066.0 1339057]
     [20 'South Atlantic' 'Maryland' 4914.0 2230.0 6035802]
     [21 'New England' 'Massachusetts' 6811.0 13257.0 6882635]
     [22 'East North Central' 'Michigan' 5209.0 3142.0 9984072]
     [23 'West North Central' 'Minnesota' 3993.0 3250.0 5606249]
     [24 'East South Central' 'Mississippi' 1024.0 328.0 2981020]
     [25 'West North Central' 'Missouri' 3776.0 2107.0 6121623]
     [26 'Mountain' 'Montana' 983.0 422.0 1060665]
     [27 'West North Central' 'Nebraska' 1745.0 676.0 1925614]
     [28 'Mountain' 'Nevada' 7058.0 486.0 3027341]
     [29 'New England' 'New Hampshire' 835.0 615.0 1353465]
     [30 'Mid-Atlantic' 'New Jersey' 6048.0 3350.0 8886025]
     [31 'Mountain' 'New Mexico' 1949.0 602.0 2092741]
     [32 'Mid-Atlantic' 'New York' 39827.0 52070.0 19530351]
     [33 'South Atlantic' 'North Carolina' 6451.0 2817.0 10381615]
     [34 'West North Central' 'North Dakota' 467.0 75.0 758080]
     [35 'East North Central' 'Ohio' 6929.0 3320.0 11676341]
     [36 'West South Central' 'Oklahoma' 2823.0 1048.0 3940235]
     [37 'Pacific' 'Oregon' 11139.0 3337.0 4181886]
     [38 'Mid-Atlantic' 'Pennsylvania' 8163.0 5349.0 12800922]
     [39 'New England' 'Rhode Island' 747.0 354.0 1058287]
     [40 'South Atlantic' 'South Carolina' 3082.0 851.0 5084156]
     [41 'West North Central' 'South Dakota' 836.0 323.0 878698]
     [42 'East South Central' 'Tennessee' 6139.0 1744.0 6771631]
     [43 'West South Central' 'Texas' 19199.0 6111.0 28628666]
     [44 'Mountain' 'Utah' 1904.0 972.0 3153550]
     [45 'New England' 'Vermont' 780.0 511.0 624358]
     [46 'South Atlantic' 'Virginia' 3928.0 2047.0 8501286]
     [47 'Pacific' 'Washington' 16424.0 5880.0 7523869]
     [48 'South Atlantic' 'West Virginia' 1021.0 222.0 1804291]
     [49 'East North Central' 'Wisconsin' 2740.0 2167.0 5807406]
     [50 'Mountain' 'Wyoming' 434.0 205.0 577601]]
    Index(['Unnamed: 0', 'region', 'state', 'individuals', 'family_members',
           'state_pop'],
          dtype='object')
    RangeIndex(start=0, stop=51, step=1)
    


```python
# Sort homelessness by individual
homelessness_ind = homelessness.sort_values('individuals')

# Print the top few rows
print(homelessness_ind.head())
```

        Unnamed: 0              region         state  individuals  family_members  \
    50          50            Mountain       Wyoming        434.0           205.0   
    34          34  West North Central  North Dakota        467.0            75.0   
    7            7      South Atlantic      Delaware        708.0           374.0   
    39          39         New England  Rhode Island        747.0           354.0   
    45          45         New England       Vermont        780.0           511.0   
    
        state_pop  
    50     577601  
    34     758080  
    7      965479  
    39    1058287  
    45     624358  
    


```python
# Sort homelessness by descending family members
homelessness_fam = homelessness.sort_values('family_members', ascending=False)

# Print the top few rows
print(homelessness_fam.head())
```

        Unnamed: 0              region          state  individuals  \
    32          32        Mid-Atlantic       New York      39827.0   
    4            4             Pacific     California     109008.0   
    21          21         New England  Massachusetts       6811.0   
    9            9      South Atlantic        Florida      21443.0   
    43          43  West South Central          Texas      19199.0   
    
        family_members  state_pop  
    32         52070.0   19530351  
    4          20964.0   39461588  
    21         13257.0    6882635  
    9           9587.0   21244317  
    43          6111.0   28628666  
    


```python
# Sort homelessness by region, then descending family members
homelessness_reg_fam = homelessness.sort_values(['region','family_members'],ascending=[True,False])

# Print the top few rows
print(homelessness_reg_fam.head())
```

        Unnamed: 0              region      state  individuals  family_members  \
    13          13  East North Central   Illinois       6752.0          3891.0   
    35          35  East North Central       Ohio       6929.0          3320.0   
    22          22  East North Central   Michigan       5209.0          3142.0   
    49          49  East North Central  Wisconsin       2740.0          2167.0   
    14          14  East North Central    Indiana       3776.0          1482.0   
    
        state_pop  
    13   12723071  
    35   11676341  
    22    9984072  
    49    5807406  
    14    6695497  
    


```python
##Subsetting columns
# Select the individuals column
individuals = homelessness["individuals"]

# Print the head of the result
print(individuals.head())
```

    0      2570.0
    1      1434.0
    2      7259.0
    3      2280.0
    4    109008.0
    Name: individuals, dtype: float64
    


```python
# Select the state and family_members columns
state_fam = homelessness[['state','family_members']]

# Print the head of the result
print(state_fam.head())
```

            state  family_members
    0     Alabama           864.0
    1      Alaska           582.0
    2     Arizona          2606.0
    3    Arkansas           432.0
    4  California         20964.0
    


```python
# Select only the individuals and state columns, in that order
ind_state = homelessness[["individuals", "state"]]

# Print the head of the result
print(ind_state.head())
```

       individuals       state
    0       2570.0     Alabama
    1       1434.0      Alaska
    2       7259.0     Arizona
    3       2280.0    Arkansas
    4     109008.0  California
    


```python
# Filter for rows where individuals is greater than 10000
ind_gt_10k = homelessness[homelessness["individuals"] > 10000]

# See the result
print(ind_gt_10k)
```

        Unnamed: 0              region       state  individuals  family_members  \
    4            4             Pacific  California     109008.0         20964.0   
    9            9      South Atlantic     Florida      21443.0          9587.0   
    32          32        Mid-Atlantic    New York      39827.0         52070.0   
    37          37             Pacific      Oregon      11139.0          3337.0   
    43          43  West South Central       Texas      19199.0          6111.0   
    47          47             Pacific  Washington      16424.0          5880.0   
    
        state_pop  
    4    39461588  
    9    21244317  
    32   19530351  
    37    4181886  
    43   28628666  
    47    7523869  
    


```python
# Filter for rows where region is Mountain
mountain_reg = homelessness[homelessness["region"] == "Mountain"]

# See the result
print(mountain_reg)
```

        Unnamed: 0    region       state  individuals  family_members  state_pop
    2            2  Mountain     Arizona       7259.0          2606.0    7158024
    5            5  Mountain    Colorado       7607.0          3250.0    5691287
    12          12  Mountain       Idaho       1297.0           715.0    1750536
    26          26  Mountain     Montana        983.0           422.0    1060665
    28          28  Mountain      Nevada       7058.0           486.0    3027341
    31          31  Mountain  New Mexico       1949.0           602.0    2092741
    44          44  Mountain        Utah       1904.0           972.0    3153550
    50          50  Mountain     Wyoming        434.0           205.0     577601
    


```python
# Filter for rows where family_members is less than 1000 
# and region is Pacific
fam_lt_1k_pac = homelessness[(homelessness["family_members"] < 1000) & (homelessness["region"] == "Pacific")]

# See the result
print(fam_lt_1k_pac)
```

       Unnamed: 0   region   state  individuals  family_members  state_pop
    1           1  Pacific  Alaska       1434.0           582.0     735139
    


```python
#Subsetting rows by categorical variables
```


```python
# Subset for rows in South Atlantic or Mid-Atlantic regions
A = homelessness["region"].isin(["South Atlantic", "Mid-Atlantic"])
south_mid_atlantic = homelessness[A]
# See the result
print(south_mid_atlantic)
```

        Unnamed: 0          region                 state  individuals  \
    7            7  South Atlantic              Delaware        708.0   
    8            8  South Atlantic  District of Columbia       3770.0   
    9            9  South Atlantic               Florida      21443.0   
    10          10  South Atlantic               Georgia       6943.0   
    20          20  South Atlantic              Maryland       4914.0   
    30          30    Mid-Atlantic            New Jersey       6048.0   
    32          32    Mid-Atlantic              New York      39827.0   
    33          33  South Atlantic        North Carolina       6451.0   
    38          38    Mid-Atlantic          Pennsylvania       8163.0   
    40          40  South Atlantic        South Carolina       3082.0   
    46          46  South Atlantic              Virginia       3928.0   
    48          48  South Atlantic         West Virginia       1021.0   
    
        family_members  state_pop  
    7            374.0     965479  
    8           3134.0     701547  
    9           9587.0   21244317  
    10          2556.0   10511131  
    20          2230.0    6035802  
    30          3350.0    8886025  
    32         52070.0   19530351  
    33          2817.0   10381615  
    38          5349.0   12800922  
    40           851.0    5084156  
    46          2047.0    8501286  
    48           222.0    1804291  
    


```python

```
