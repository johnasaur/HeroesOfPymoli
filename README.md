

```python
# Dependencies and file read
import pandas as pd
import numpy as np
import os
```


```python
# read file
json_path = "../Lesson-Plans/purchase_data.json"

# Import the file as a DataFrame
pymoli_df = pd.read_json(json_path)
pymoli_df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# player count: number of players
number_of_players = len(pymoli_df["SN"].unique()) 
all_players_df = pd.DataFrame([{"Total number of Players": number_of_players}]) 
all_players_df
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
      <th>Total number of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
# purchasing analysis: delete duplicates from the list & find unique items
remove_duplicates = pymoli_df.drop_duplicates(["Item ID"], keep = "last")
unique = len(remove_duplicates)
unique
```




    183




```python
# find average using purchases and revenue
avg_price = (pymoli_df["Price"].mean(), 2)
avg_price
```




    (2.931192307692303, 2)




```python
# find all purchases (total number of purchases)
all_purchases = pymoli_df["Price"].count()
all_purchases
```




    780




```python
# find all revenue (total number of revenue)
revenue = round(pymoli_df["Price"].sum(),2)
revenue
```




    2286.33




```python
# gender demogr. - no duplicates again
remove_duplicates = pymoli_df.drop_duplicates(["SN"], keep = "last")
remove_duplicates.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
    </tr>
  </tbody>
</table>
</div>




```python
# remove duplicates
gender_count = remove_duplicates["Gender"].value_counts().reset_index()
gender_count
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
      <th>index</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>465</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# gender percentage & count
gender_count = gender_count["Gender"]/number_of_players * 100
gender_count.round(2)
```




    0    81.15
    1    17.45
    2     1.40
    Name: Gender, dtype: float64




```python
# purchasing analysis by gender
purchase_gender = pd.DataFrame(pymoli_df.groupby("Gender")["Gender"].count())
purchase_gender
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
      <th>Gender</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
# purchase count by gender
purchase_count = pd.DataFrame(pymoli_df.groupby("Gender")["Price"].sum())
purchase_count
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
# avg purchase price, need to merge to calculate
avg_purchase = pd.merge(purchase_gender, purchase_count, left_index = True, right_index = True)
# avg_purchase
```


```python
# average purchase price and total purchase value (price) by gender
avg_purchase["Avg Price"] = avg_purchase["Price"] / avg_purchase ["Gender"]
avg_purchase.round(2)
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
      <th>Gender</th>
      <th>Price</th>
      <th>Avg Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>382.91</td>
      <td>2.82</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>1867.68</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>35.74</td>
      <td>3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# normalise by dividing all by sum of values
avg_purchase["Normalised Totals"] = round(avg_purchase["Price"]/ avg_purchase["Gender"], 2)
avg_purchase
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
      <th>Gender</th>
      <th>Price</th>
      <th>Avg Price</th>
      <th>Normalised Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>382.91</td>
      <td>2.815515</td>
      <td>2.82</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>1867.68</td>
      <td>2.950521</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>35.74</td>
      <td>3.249091</td>
      <td>3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# age demogr (bins of 4 yrs)
bins = [0, 9.99, 14.99, 19.99, 24.99, 29.99, 34.99, 39.99, 99.99]
groups = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]
pymoli_df["All Ages"] = pd.cut(pymoli_df["Age"], bins, labels=groups)
pymoli_df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>All Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# total
age_totals = pymoli_df["All Ages"].value_counts()
age_totals
```




    20-24    336
    15-19    133
    25-29    125
    30-34     64
    35-39     42
    10-14     35
    <10       28
    40+       17
    Name: All Ages, dtype: int64




```python
# percent
age_percent = age_totals / number_of_players * 100
age_percent.round(2)
```




    20-24    58.64
    15-19    23.21
    25-29    21.82
    30-34    11.17
    35-39     7.33
    10-14     6.11
    <10       4.89
    40+       2.97
    Name: All Ages, dtype: float64




```python
demogr = pd.DataFrame({"Player percentage": gender_count})
demogr.round(2)
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
      <th>Player percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>81.15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17.45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
# avg purchase price
avg_price = pd.DataFrame(pymoli_df.groupby("All Ages")["Price"].mean())
avg_price.head().round(2)
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
      <th>Price</th>
    </tr>
    <tr>
      <th>All Ages</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>2.98</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>2.77</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>2.91</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>2.91</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2.96</td>
    </tr>
  </tbody>
</table>
</div>




```python
# total purchase price
total_price2 = pd.DataFrame(pymoli_df.groupby("All Ages")["Price"].sum())
total_price2.head()
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
      <th>Price</th>
    </tr>
    <tr>
      <th>All Ages</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>370.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge all above bin data
age_merge = pd.merge(age_count, avg_price, left_index=True, right_index=True).merge(total_price2, left_index=True, right_index=True)
age_merge.head().round(2)
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
      <th>SN</th>
      <th>Price_x</th>
      <th>Price_y</th>
    </tr>
    <tr>
      <th>All Ages</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>0</td>
      <td>2.98</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>0</td>
      <td>2.77</td>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>0</td>
      <td>2.91</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>3</td>
      <td>2.91</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>0</td>
      <td>2.96</td>
      <td>370.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename columns
age_merge = age_merge.rename(columns={"Price_x": "Average Price", "Price_y": "Total Purchases"})
age_merge.head().round(2)
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
      <th>SN</th>
      <th>Average Price</th>
      <th>Total Purchases</th>
    </tr>
    <tr>
      <th>All Ages</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>0</td>
      <td>2.98</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>0</td>
      <td>2.77</td>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>0</td>
      <td>2.91</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>3</td>
      <td>2.91</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>0</td>
      <td>2.96</td>
      <td>370.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# normalise all
age_merge_norm = total_price2 ["Price"] / age_merge ["Total Purchases"]
age_merge_norm
```




    All Ages
    <10      1.0
    10-14    1.0
    15-19    1.0
    20-24    1.0
    25-29    1.0
    30-34    1.0
    35-39    1.0
    40+      1.0
    dtype: float64




```python
# top spenders
spender_total = pd.DataFrame(pymoli_df.groupby("SN")["Price"].sum())
spender_total.head()                     
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
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# purchase count
spender_count = pd.DataFrame(pymoli_df.groupby("SN")["Price"].count())
spender_count.head()
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
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# avg purchase
spender_average = pd.DataFrame(pymoli_df.groupby("SN")["Price"].mean())
spender_average.head().round(2)
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
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>2.23</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>1.93</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge all
merge_all2 = pd.merge(spender_total, spender_count, left_index=True, right_index=True).merge(spender_average, left_index=True, right_index=True)
merge_all2.head()
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
      <th>Price_x</th>
      <th>Price_y</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
      <td>3</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
      <td>3</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
      <td>1</td>
      <td>1.270000</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_all2 = merge_all2.rename(columns={"Price_x": "Total Purchases", "Price_y": "Purchase Counts", "Price": "Average Price"})
merge_all2.head().round(2)
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
      <th>Total Purchases</th>
      <th>Purchase Counts</th>
      <th>Average Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
      <td>3</td>
      <td>2.23</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
      <td>3</td>
      <td>1.93</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
      <td>1</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# top 5 spenders
merge_all2.sort_values("Total Purchases", ascending=False, inplace=True)
merge_all2.head().round(2)
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
      <th>Total Purchases</th>
      <th>Purchase Counts</th>
      <th>Average Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>17.06</td>
      <td>5</td>
      <td>3.41</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>13.56</td>
      <td>4</td>
      <td>3.39</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>12.74</td>
      <td>4</td>
      <td>3.18</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>12.73</td>
      <td>3</td>
      <td>4.24</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>11.58</td>
      <td>3</td>
      <td>3.86</td>
    </tr>
  </tbody>
</table>
</div>




```python
# most popular items
most_popular_items = pd.DataFrame(pymoli_df.groupby("Item ID")["Item ID"].count())
most_popular_items.head()
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
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# sort asc
most_popular_items.sort_values("Item ID", ascending = False, inplace = True)
most_popular_items.head()
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
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>11</td>
    </tr>
    <tr>
      <th>84</th>
      <td>11</td>
    </tr>
    <tr>
      <th>31</th>
      <td>9</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# total purchase
total_most_popular = pd.DataFrame(pymoli_df.groupby("Item ID")["Price"].sum())
total_most_popular.head()
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge total count and total purchase
merge_most_popular = pd.merge(most_popular_items, total_most_popular, left_index=True, right_index=True)
merge_most_popular.head()
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
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>11</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <td>11</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <td>9</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <td>9</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
# no duplicates, add the rest
duplicates = pymoli_df.drop_duplicates(["Item ID"], keep="last")
duplicates.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>All Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>21</th>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>59</th>
      <td>15</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>63</th>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>88</th>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_all = pd.merge(merge_most_popular, duplicates, left_index=True, right_index=True)
merge_all.head()
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
      <th>Item ID_x</th>
      <th>Price_x</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID_y</th>
      <th>Item Name</th>
      <th>Price_y</th>
      <th>SN</th>
      <th>All Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>173</th>
      <td>5</td>
      <td>24.15</td>
      <td>30</td>
      <td>Male</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.82</td>
      <td>Chadadarya31</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>129</th>
      <td>4</td>
      <td>6.20</td>
      <td>23</td>
      <td>Female</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>3.25</td>
      <td>Eurinu48</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>177</th>
      <td>4</td>
      <td>19.56</td>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>63</th>
      <td>4</td>
      <td>5.08</td>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
      <td>9.81</td>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15-19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# drop the columns not needed for the assignment 
merge_all = merge_all[["Item ID_y", "Item Name", "Item ID_x", "Price_x", "Price_y"]]
merge_all.head()
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
      <th>Item ID_y</th>
      <th>Item Name</th>
      <th>Item ID_x</th>
      <th>Price_x</th>
      <th>Price_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>173</th>
      <td>0</td>
      <td>Splinter</td>
      <td>5</td>
      <td>24.15</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>129</th>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>4</td>
      <td>6.20</td>
      <td>3.25</td>
    </tr>
    <tr>
      <th>177</th>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>4</td>
      <td>19.56</td>
      <td>3.73</td>
    </tr>
    <tr>
      <th>63</th>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>4</td>
      <td>5.08</td>
      <td>3.04</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
      <td>Phantomlight</td>
      <td>3</td>
      <td>9.81</td>
      <td>1.79</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename columns
merge_all = merge_all.rename(columns={"Item ID_y": "Item ID", "Item ID_x": "Purchase Count", "Price_x": "Total Purchase Value", "Price_y": "Item Price"})
merge_all
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
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
      <th>Item Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>173</th>
      <td>0</td>
      <td>Splinter</td>
      <td>5</td>
      <td>24.15</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>129</th>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>4</td>
      <td>6.20</td>
      <td>3.25</td>
    </tr>
    <tr>
      <th>177</th>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>4</td>
      <td>19.56</td>
      <td>3.73</td>
    </tr>
    <tr>
      <th>63</th>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>4</td>
      <td>5.08</td>
      <td>3.04</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
      <td>Phantomlight</td>
      <td>3</td>
      <td>9.81</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>17</th>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>3</td>
      <td>10.41</td>
      <td>1.65</td>
    </tr>
    <tr>
      <th>88</th>
      <td>132</td>
      <td>Persuasion</td>
      <td>2</td>
      <td>8.20</td>
      <td>3.90</td>
    </tr>
    <tr>
      <th>59</th>
      <td>2</td>
      <td>Verdict</td>
      <td>1</td>
      <td>1.65</td>
      <td>3.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
# most profitable items
most_profit = pd.DataFrame(pymoli_df.groupby("Item ID")["Price"].sum())
most_profit.head()
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# asc order
most_profit.sort_values("Price", ascending=False, inplace=True)
most_profit.head()
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
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
# purchase count
profit_count = pd.DataFrame(pymoli_df.groupby("Item ID")["Item ID"].count())
profit_count.head()
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
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge above tables
profit_merge = pd.merge(most_profit, profit_count, left_index=True, right_index=True, how="left")
profit_merge.head()
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
      <th>Price</th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>37.26</td>
      <td>9</td>
    </tr>
    <tr>
      <th>115</th>
      <td>29.75</td>
      <td>7</td>
    </tr>
    <tr>
      <th>32</th>
      <td>29.70</td>
      <td>6</td>
    </tr>
    <tr>
      <th>103</th>
      <td>29.22</td>
      <td>6</td>
    </tr>
    <tr>
      <th>107</th>
      <td>28.88</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# drop duplicates
duplicates1 = pymoli_df.drop_duplicates(["Item ID"], keep="last")
duplicates1.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>All Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>21</th>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>59</th>
      <td>15</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>63</th>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>88</th>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge in non duplicates
merge_nondup = pd.merge(most_profit, duplicates1, left_index=True, right_index=True)
merge_nondup.head()
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
      <th>Price_x</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price_y</th>
      <th>SN</th>
      <th>All Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>173</th>
      <td>24.15</td>
      <td>30</td>
      <td>Male</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.82</td>
      <td>Chadadarya31</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>177</th>
      <td>19.56</td>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10.41</td>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>21</th>
      <td>9.81</td>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>88</th>
      <td>8.20</td>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# add item ID in merge
merge_more = pd.merge(most_profit,merge_nondup, left_index = True, right_on = 'Item ID')
merge_more.head()
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
      <th>Price</th>
      <th>Price_x</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price_y</th>
      <th>SN</th>
      <th>All Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>177</th>
      <td>11.19</td>
      <td>19.56</td>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>88</th>
      <td>7.80</td>
      <td>8.20</td>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>59</th>
      <td>3.40</td>
      <td>1.65</td>
      <td>15</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>129</th>
      <td>3.25</td>
      <td>6.20</td>
      <td>23</td>
      <td>Female</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>3.25</td>
      <td>Eurinu48</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>63</th>
      <td>3.04</td>
      <td>5.08</td>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge in profit count
merge_again = pd.merge(merge_more, profit_count, left_index=True, right_index=True)
merge_again
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
      <th>Price</th>
      <th>Price_x</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID_x</th>
      <th>Item Name</th>
      <th>Price_y</th>
      <th>SN</th>
      <th>All Ages</th>
      <th>Item ID_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>177</th>
      <td>11.19</td>
      <td>19.56</td>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
      <td>30-34</td>
      <td>4</td>
    </tr>
    <tr>
      <th>88</th>
      <td>7.80</td>
      <td>8.20</td>
      <td>23</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>Undotesta33</td>
      <td>20-24</td>
      <td>2</td>
    </tr>
    <tr>
      <th>59</th>
      <td>3.40</td>
      <td>1.65</td>
      <td>15</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.40</td>
      <td>Ila44</td>
      <td>15-19</td>
      <td>1</td>
    </tr>
    <tr>
      <th>129</th>
      <td>3.25</td>
      <td>6.20</td>
      <td>23</td>
      <td>Female</td>
      <td>126</td>
      <td>Exiled Mithril Longsword</td>
      <td>3.25</td>
      <td>Eurinu48</td>
      <td>20-24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>63</th>
      <td>3.04</td>
      <td>5.08</td>
      <td>23</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>3.04</td>
      <td>Ryanara76</td>
      <td>20-24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>173</th>
      <td>1.82</td>
      <td>24.15</td>
      <td>30</td>
      <td>Male</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.82</td>
      <td>Chadadarya31</td>
      <td>30-34</td>
      <td>5</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1.79</td>
      <td>9.81</td>
      <td>15</td>
      <td>Male</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>Iaralrgue74</td>
      <td>15-19</td>
      <td>3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1.65</td>
      <td>10.41</td>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
      <td>20-24</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_again = merge_again[["Item ID_x", "Item ID_y","Item Name" ,"Price_x", "Price_y"]]
merge_again
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
      <th>Item ID_x</th>
      <th>Item ID_y</th>
      <th>Item Name</th>
      <th>Price_x</th>
      <th>Price_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>177</th>
      <td>155</td>
      <td>4</td>
      <td>War-Forged Gold Deflector</td>
      <td>19.56</td>
      <td>3.73</td>
    </tr>
    <tr>
      <th>88</th>
      <td>132</td>
      <td>2</td>
      <td>Persuasion</td>
      <td>8.20</td>
      <td>3.90</td>
    </tr>
    <tr>
      <th>59</th>
      <td>2</td>
      <td>1</td>
      <td>Verdict</td>
      <td>1.65</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>129</th>
      <td>126</td>
      <td>4</td>
      <td>Exiled Mithril Longsword</td>
      <td>6.20</td>
      <td>3.25</td>
    </tr>
    <tr>
      <th>63</th>
      <td>28</td>
      <td>4</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>5.08</td>
      <td>3.04</td>
    </tr>
    <tr>
      <th>173</th>
      <td>0</td>
      <td>5</td>
      <td>Splinter</td>
      <td>24.15</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>9.81</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>17</th>
      <td>59</td>
      <td>3</td>
      <td>Lightning, Etcher of the King</td>
      <td>10.41</td>
      <td>1.65</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename columns
merge_again = merge_again.rename(columns= {"Item ID_x": "Item ID", "Item ID_y": "Purchase Count", "Price_x": "Total Purchase Value", "Price_y": "Item Price"})
merge_again
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
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Item Name</th>
      <th>Total Purchase Value</th>
      <th>Item Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>177</th>
      <td>155</td>
      <td>4</td>
      <td>War-Forged Gold Deflector</td>
      <td>19.56</td>
      <td>3.73</td>
    </tr>
    <tr>
      <th>88</th>
      <td>132</td>
      <td>2</td>
      <td>Persuasion</td>
      <td>8.20</td>
      <td>3.90</td>
    </tr>
    <tr>
      <th>59</th>
      <td>2</td>
      <td>1</td>
      <td>Verdict</td>
      <td>1.65</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>129</th>
      <td>126</td>
      <td>4</td>
      <td>Exiled Mithril Longsword</td>
      <td>6.20</td>
      <td>3.25</td>
    </tr>
    <tr>
      <th>63</th>
      <td>28</td>
      <td>4</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>5.08</td>
      <td>3.04</td>
    </tr>
    <tr>
      <th>173</th>
      <td>0</td>
      <td>5</td>
      <td>Splinter</td>
      <td>24.15</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
      <td>3</td>
      <td>Phantomlight</td>
      <td>9.81</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>17</th>
      <td>59</td>
      <td>3</td>
      <td>Lightning, Etcher of the King</td>
      <td>10.41</td>
      <td>1.65</td>
    </tr>
  </tbody>
</table>
</div>


