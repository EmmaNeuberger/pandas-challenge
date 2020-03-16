## Pandas Data Manipulation Project

### In this project, Pandas library is used to manipulate and analyze clinical data. 

```python
 # Dependencies and Setup
import pandas as pd

# File to Load
file_to_load = "purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)
purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Player Count
player_unique = purchase_data["SN"].unique()
player_count = len(player_unique)

total_players = pd.DataFrame({"Total Players": [player_count]})

total_players
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing Analysis Total
unique_items = purchase_data["Item ID"].unique()
unique_count = len(unique_items)

total_purchases = len(purchase_data["Purchase ID"])

average_price = purchase_data["Price"].sum() / total_purchases
total_revenue = purchase_data["Price"].sum()
purchase_analysis = pd.DataFrame({"Number of Unique Items":[unique_count], "Average Price":[average_price], "Number of Purchases":[total_purchases], "Total Revenue":[total_revenue]})

purchase_analysis
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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>3.050987</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Gender Demographics
gender_demographics = purchase_data.groupby("Gender")
gender_dem_df = pd.DataFrame(gender_demographics.count())

total_purchase = gender_dem_df["Purchase ID"].sum()


female_purchase = gender_dem_df.iloc[0, 0]
male_purchase =  gender_dem_df.iloc[1, 0]
other_purchase = gender_dem_df.iloc[2, 0]
male_percentage = male_purchase / total_purchase
female_percentage = female_purchase / total_purchase
other_percentage = other_purchase / total_purchase


gender_dem = pd.DataFrame({"Male": {"Total": male_purchase, "Percentage": male_percentage}, 
                               "Female": {"Total": female_purchase, "Percentage": female_percentage}, 
                               "Other": {"Total": other_purchase, "Percentage": other_percentage}})
gender_dem
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
      <th>Male</th>
      <th>Female</th>
      <th>Other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Percentage</th>
      <td>0.835897</td>
      <td>0.144872</td>
      <td>0.019231</td>
    </tr>
    <tr>
      <th>Total</th>
      <td>652.000000</td>
      <td>113.000000</td>
      <td>15.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing Analysis Gender
gender_demographics_index = purchase_data.set_index("Gender")
gender_demographics_index

female_purchasetotal = gender_demographics_index.loc["Female", "Price"].sum()
female_averageprice = gender_demographics_index.loc["Female", "Price"].mean()
female_purchasecount = gender_demographics_index.loc["Female", "Price"].count()

male_purchasetotal = gender_demographics_index.loc["Male", "Price"].sum()
male_averageprice = gender_demographics_index.loc["Male", "Price"].mean()
male_purchasecount = gender_demographics_index.loc["Male", "Price"].count()

other_purchasetotal = gender_demographics_index.loc["Other / Non-Disclosed", "Price"].sum()
other_averageprice = gender_demographics_index.loc["Other / Non-Disclosed", "Price"].mean()
other_purchasecount = gender_demographics_index.loc["Other / Non-Disclosed", "Price"].count()

gender_analysis = pd.DataFrame({"Male": {"Purchase Total Value": male_purchasetotal, "Average Purchase Price": male_averageprice, "Number of Purchases": male_purchasecount}, 
                                "Female": {"Purchase Total Value": female_purchasetotal, "Average Purchase Price": female_averageprice, "Number of Purchases": female_purchasecount}, 
                                "Other": {"Purchase Total Value": other_purchasetotal, "Average Purchase Price": other_averageprice, "Number of Purchases": other_purchasecount}})
gender_analysis
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
      <th>Male</th>
      <th>Female</th>
      <th>Other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Average Purchase Price</th>
      <td>3.017853</td>
      <td>3.203009</td>
      <td>3.346</td>
    </tr>
    <tr>
      <th>Number of Purchases</th>
      <td>652.000000</td>
      <td>113.000000</td>
      <td>15.000</td>
    </tr>
    <tr>
      <th>Purchase Total Value</th>
      <td>1967.640000</td>
      <td>361.940000</td>
      <td>50.190</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Age Demographics
purchase_data

bins = (0, 10, 14, 19, 24, 29, 34, 39, 100)

bin_labels = ("<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+")

purchase_data["Age Group"] = pd.cut(purchase_data["Age"], bins=bins, labels=bin_labels)
age_index = purchase_data.groupby("Age Group")

age_sum = pd.DataFrame(age_index.sum())
age_count = pd.DataFrame(age_index.count())
age_average = pd.DataFrame(age_index.mean())

# total purchases in each group
purchases_bygroup = age_count.iloc[:, 0]

# percent of total purchases by group
percent_totalpurchases = age_count.iloc[:, 0] / 780


age_dem = pd.merge(purchases_bygroup, percent_totalpurchases, on="Age Group")
age_dem = age_dem.rename(columns={"Purchase ID_x":"Total Purchases", "Purchase ID_y":"Percentage of Total"})

age_dem
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
      <th>Percentage of Total</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>32</td>
      <td>0.041026</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>19</td>
      <td>0.024359</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>0.174359</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>0.467949</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>0.129487</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>0.093590</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>0.052564</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>0.016667</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing Analysis Age
bins = (0, 10, 14, 19, 24, 29, 34, 39, 100)

bin_labels = ("<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+")

purchase_data["Age Group"] = pd.cut(purchase_data["Age"], bins=bins, labels=bin_labels)

age_index = purchase_data.groupby("Age Group")

age_sum = pd.DataFrame(age_index.sum())
age_count = pd.DataFrame(age_index.count())
age_average = pd.DataFrame(age_index.mean())

# total purchases in each group
purchases_bygroup = age_count.iloc[:, 0]

# average price by group
purchases_av = age_sum.iloc[:, 3] / age_count.iloc[:, 0]

# total purchase value
purchases_total = age_sum.iloc[:, 3]

age_analysis = pd.DataFrame({"Purchase Count": purchases_bygroup, "Average Purchase Price": purchases_av, "Total Purchase Value": purchases_total})
age_analysis
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>32</td>
      <td>3.405000</td>
      <td>108.96</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>19</td>
      <td>2.681579</td>
      <td>50.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>3.035956</td>
      <td>412.89</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>3.052219</td>
      <td>1114.06</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>2.900990</td>
      <td>293.00</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>2.931507</td>
      <td>214.00</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>3.601707</td>
      <td>147.67</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>2.941538</td>
      <td>38.24</td>
    </tr>
  </tbody>
</table>
</div>




```python

# Top Spenders

indexed_spender = purchase_data.groupby("SN")

spender_sum = indexed_spender["Price"].sum()
spender_count = indexed_spender["Item ID"].count()
spender_mean = indexed_spender["Price"].mean()


# Sort by Total Purchase Value
spender_df = pd.DataFrame({"Total Purchase Value": spender_sum, "Purchase Count": spender_count, "Average Purchase Price": spender_mean})
spender_sorted = spender_df.sort_values("Total Purchase Value", ascending=False).head()

spender_sorted
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
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
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
      <th>Lisosia93</th>
      <td>18.96</td>
      <td>5</td>
      <td>3.792000</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>15.45</td>
      <td>4</td>
      <td>3.862500</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>13.83</td>
      <td>3</td>
      <td>4.610000</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>13.62</td>
      <td>4</td>
      <td>3.405000</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>13.10</td>
      <td>3</td>
      <td>4.366667</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Most Popular Items

indexed_item = purchase_data.groupby("Item Name")

item_sum = indexed_item["Price"].sum()
item_count = indexed_item["Item ID"].count()
item_mean = indexed_item["Price"].mean()


# Sort by Total Sold
popular_itemdf = pd.DataFrame({"Total Purchase Value": item_sum, "Total Sold": item_count, "Average Purchase Price": item_mean})
popular_sorteddf = popular_itemdf.sort_values("Total Sold", ascending=False).head()

popular_sorteddf
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
      <th>Total Purchase Value</th>
      <th>Total Sold</th>
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Final Critic</th>
      <td>59.99</td>
      <td>13</td>
      <td>4.614615</td>
    </tr>
    <tr>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>50.76</td>
      <td>12</td>
      <td>4.230000</td>
    </tr>
    <tr>
      <th>Persuasion</th>
      <td>28.99</td>
      <td>9</td>
      <td>3.221111</td>
    </tr>
    <tr>
      <th>Nirvana</th>
      <td>44.10</td>
      <td>9</td>
      <td>4.900000</td>
    </tr>
    <tr>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>31.77</td>
      <td>9</td>
      <td>3.530000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Most Profitable Items
indexed_item = purchase_data.groupby("Item Name")

item_sum = indexed_item["Price"].sum()
item_count = indexed_item["Item ID"].count()
item_mean = indexed_item["Price"].mean()

# Sort by Total Purchase Value
profitable_itemdf = pd.DataFrame({"Total Purchase Value": item_sum, "Purchase Count": item_count, "Item Price": item_mean})
profitable_sorteddf = profitable_itemdf.sort_values("Total Purchase Value", ascending=False).head()

profitable_sorteddf
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
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Final Critic</th>
      <td>59.99</td>
      <td>13</td>
      <td>4.614615</td>
    </tr>
    <tr>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>50.76</td>
      <td>12</td>
      <td>4.230000</td>
    </tr>
    <tr>
      <th>Nirvana</th>
      <td>44.10</td>
      <td>9</td>
      <td>4.900000</td>
    </tr>
    <tr>
      <th>Fiery Glass Crusader</th>
      <td>41.22</td>
      <td>9</td>
      <td>4.580000</td>
    </tr>
    <tr>
      <th>Singed Scalpel</th>
      <td>34.80</td>
      <td>8</td>
      <td>4.350000</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
