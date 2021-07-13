## Cleaning & Analyzing Ebay Kleinanzeigan Data

In this project, we will be taking a dataset of 50,000 points from the Ebay Kleinanzeigen classifieds section of German Ebay and cleaning and analyzing the data. We will import the dataset using Pandas to clean and organize it for analysis.

We will ultimately look at the top 6 brands and their mean price and mileage to compare them.


```python
#importing libraries
import pandas as pd
import numpy as np
```


```python
#reading the dataset into a DataFrame
autos = pd.read_csv("autos.csv", encoding='Latin-1')
```


```python
autos
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
      <th>dateCrawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offerType</th>
      <th>price</th>
      <th>abtest</th>
      <th>vehicleType</th>
      <th>yearOfRegistration</th>
      <th>gearbox</th>
      <th>powerPS</th>
      <th>model</th>
      <th>odometer</th>
      <th>monthOfRegistration</th>
      <th>fuelType</th>
      <th>brand</th>
      <th>notRepairedDamage</th>
      <th>dateCreated</th>
      <th>nrOfPictures</th>
      <th>postalCode</th>
      <th>lastSeen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-26 17:47:46</td>
      <td>Peugeot_807_160_NAVTECH_ON_BOARD</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$5,000</td>
      <td>control</td>
      <td>bus</td>
      <td>2004</td>
      <td>manuell</td>
      <td>158</td>
      <td>andere</td>
      <td>150,000km</td>
      <td>3</td>
      <td>lpg</td>
      <td>peugeot</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>79588</td>
      <td>2016-04-06 06:45:54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-04-04 13:38:56</td>
      <td>BMW_740i_4_4_Liter_HAMANN_UMBAU_Mega_Optik</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,500</td>
      <td>control</td>
      <td>limousine</td>
      <td>1997</td>
      <td>automatik</td>
      <td>286</td>
      <td>7er</td>
      <td>150,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>bmw</td>
      <td>nein</td>
      <td>2016-04-04 00:00:00</td>
      <td>0</td>
      <td>71034</td>
      <td>2016-04-06 14:45:08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-26 18:57:24</td>
      <td>Volkswagen_Golf_1.6_United</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,990</td>
      <td>test</td>
      <td>limousine</td>
      <td>2009</td>
      <td>manuell</td>
      <td>102</td>
      <td>golf</td>
      <td>70,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>35394</td>
      <td>2016-04-06 20:15:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-12 16:58:10</td>
      <td>Smart_smart_fortwo_coupe_softouch/F1/Klima/Pan...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$4,350</td>
      <td>control</td>
      <td>kleinwagen</td>
      <td>2007</td>
      <td>automatik</td>
      <td>71</td>
      <td>fortwo</td>
      <td>70,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>smart</td>
      <td>nein</td>
      <td>2016-03-12 00:00:00</td>
      <td>0</td>
      <td>33729</td>
      <td>2016-03-15 03:16:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-04-01 14:38:50</td>
      <td>Ford_Focus_1_6_Benzin_TÜV_neu_ist_sehr_gepfleg...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,350</td>
      <td>test</td>
      <td>kombi</td>
      <td>2003</td>
      <td>manuell</td>
      <td>0</td>
      <td>focus</td>
      <td>150,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-04-01 00:00:00</td>
      <td>0</td>
      <td>39218</td>
      <td>2016-04-01 14:38:50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>2016-03-27 14:38:19</td>
      <td>Audi_Q5_3.0_TDI_qu._S_tr.__Navi__Panorama__Xenon</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$24,900</td>
      <td>control</td>
      <td>limousine</td>
      <td>2011</td>
      <td>automatik</td>
      <td>239</td>
      <td>q5</td>
      <td>100,000km</td>
      <td>1</td>
      <td>diesel</td>
      <td>audi</td>
      <td>nein</td>
      <td>2016-03-27 00:00:00</td>
      <td>0</td>
      <td>82131</td>
      <td>2016-04-01 13:47:40</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>2016-03-28 10:50:25</td>
      <td>Opel_Astra_F_Cabrio_Bertone_Edition___TÜV_neu+...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,980</td>
      <td>control</td>
      <td>cabrio</td>
      <td>1996</td>
      <td>manuell</td>
      <td>75</td>
      <td>astra</td>
      <td>150,000km</td>
      <td>5</td>
      <td>benzin</td>
      <td>opel</td>
      <td>nein</td>
      <td>2016-03-28 00:00:00</td>
      <td>0</td>
      <td>44807</td>
      <td>2016-04-02 14:18:02</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>2016-04-02 14:44:48</td>
      <td>Fiat_500_C_1.2_Dualogic_Lounge</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$13,200</td>
      <td>test</td>
      <td>cabrio</td>
      <td>2014</td>
      <td>automatik</td>
      <td>69</td>
      <td>500</td>
      <td>5,000km</td>
      <td>11</td>
      <td>benzin</td>
      <td>fiat</td>
      <td>nein</td>
      <td>2016-04-02 00:00:00</td>
      <td>0</td>
      <td>73430</td>
      <td>2016-04-04 11:47:27</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>2016-03-08 19:25:42</td>
      <td>Audi_A3_2.0_TDI_Sportback_Ambition</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$22,900</td>
      <td>control</td>
      <td>kombi</td>
      <td>2013</td>
      <td>manuell</td>
      <td>150</td>
      <td>a3</td>
      <td>40,000km</td>
      <td>11</td>
      <td>diesel</td>
      <td>audi</td>
      <td>nein</td>
      <td>2016-03-08 00:00:00</td>
      <td>0</td>
      <td>35683</td>
      <td>2016-04-05 16:45:07</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>2016-03-14 00:42:12</td>
      <td>Opel_Vectra_1.6_16V</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,250</td>
      <td>control</td>
      <td>limousine</td>
      <td>1996</td>
      <td>manuell</td>
      <td>101</td>
      <td>vectra</td>
      <td>150,000km</td>
      <td>1</td>
      <td>benzin</td>
      <td>opel</td>
      <td>nein</td>
      <td>2016-03-13 00:00:00</td>
      <td>0</td>
      <td>45897</td>
      <td>2016-04-06 21:18:48</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 20 columns</p>
</div>




```python
#exploring the DF
autos.info()
autos.head()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 50000 entries, 0 to 49999
    Data columns (total 20 columns):
     #   Column               Non-Null Count  Dtype 
    ---  ------               --------------  ----- 
     0   dateCrawled          50000 non-null  object
     1   name                 50000 non-null  object
     2   seller               50000 non-null  object
     3   offerType            50000 non-null  object
     4   price                50000 non-null  object
     5   abtest               50000 non-null  object
     6   vehicleType          44905 non-null  object
     7   yearOfRegistration   50000 non-null  int64 
     8   gearbox              47320 non-null  object
     9   powerPS              50000 non-null  int64 
     10  model                47242 non-null  object
     11  odometer             50000 non-null  object
     12  monthOfRegistration  50000 non-null  int64 
     13  fuelType             45518 non-null  object
     14  brand                50000 non-null  object
     15  notRepairedDamage    40171 non-null  object
     16  dateCreated          50000 non-null  object
     17  nrOfPictures         50000 non-null  int64 
     18  postalCode           50000 non-null  int64 
     19  lastSeen             50000 non-null  object
    dtypes: int64(5), object(15)
    memory usage: 7.6+ MB





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
      <th>dateCrawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offerType</th>
      <th>price</th>
      <th>abtest</th>
      <th>vehicleType</th>
      <th>yearOfRegistration</th>
      <th>gearbox</th>
      <th>powerPS</th>
      <th>model</th>
      <th>odometer</th>
      <th>monthOfRegistration</th>
      <th>fuelType</th>
      <th>brand</th>
      <th>notRepairedDamage</th>
      <th>dateCreated</th>
      <th>nrOfPictures</th>
      <th>postalCode</th>
      <th>lastSeen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-26 17:47:46</td>
      <td>Peugeot_807_160_NAVTECH_ON_BOARD</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$5,000</td>
      <td>control</td>
      <td>bus</td>
      <td>2004</td>
      <td>manuell</td>
      <td>158</td>
      <td>andere</td>
      <td>150,000km</td>
      <td>3</td>
      <td>lpg</td>
      <td>peugeot</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>79588</td>
      <td>2016-04-06 06:45:54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-04-04 13:38:56</td>
      <td>BMW_740i_4_4_Liter_HAMANN_UMBAU_Mega_Optik</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,500</td>
      <td>control</td>
      <td>limousine</td>
      <td>1997</td>
      <td>automatik</td>
      <td>286</td>
      <td>7er</td>
      <td>150,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>bmw</td>
      <td>nein</td>
      <td>2016-04-04 00:00:00</td>
      <td>0</td>
      <td>71034</td>
      <td>2016-04-06 14:45:08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-26 18:57:24</td>
      <td>Volkswagen_Golf_1.6_United</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,990</td>
      <td>test</td>
      <td>limousine</td>
      <td>2009</td>
      <td>manuell</td>
      <td>102</td>
      <td>golf</td>
      <td>70,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>35394</td>
      <td>2016-04-06 20:15:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-12 16:58:10</td>
      <td>Smart_smart_fortwo_coupe_softouch/F1/Klima/Pan...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$4,350</td>
      <td>control</td>
      <td>kleinwagen</td>
      <td>2007</td>
      <td>automatik</td>
      <td>71</td>
      <td>fortwo</td>
      <td>70,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>smart</td>
      <td>nein</td>
      <td>2016-03-12 00:00:00</td>
      <td>0</td>
      <td>33729</td>
      <td>2016-03-15 03:16:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-04-01 14:38:50</td>
      <td>Ford_Focus_1_6_Benzin_TÜV_neu_ist_sehr_gepfleg...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,350</td>
      <td>test</td>
      <td>kombi</td>
      <td>2003</td>
      <td>manuell</td>
      <td>0</td>
      <td>focus</td>
      <td>150,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-04-01 00:00:00</td>
      <td>0</td>
      <td>39218</td>
      <td>2016-04-01 14:38:50</td>
    </tr>
  </tbody>
</table>
</div>



From the data's info, we can see that there are supposed to be 50,000 rows and 20 columns. In those 20 columns, we can see that 5 have some missing info (null values) because their rows do not equal 50k. We can also see that a couple of the columns that should be int64 dtype have a dtype of object. When looking at the head of the info, we can see why these columns are objects instead of integers and how to convert them. The price column is an object due to it having the '$' symbol in front of each price. The odometer has 'km' after each integer. To convert them, we will need to remove those characters and change the column name to include them. From the head, we can also see there are some null values, but in this German data set they are listed as "nein", the German word for "none." We can also see in the info that the column names are in CamelCase instead of snakecase, meaning we would need to convert them in order to replace whitespace with underscores.

## Exploring and cleaning column names


```python
autos.columns
```




    Index(['dateCrawled', 'name', 'seller', 'offerType', 'price', 'abtest',
           'vehicleType', 'yearOfRegistration', 'gearbox', 'powerPS', 'model',
           'odometer', 'monthOfRegistration', 'fuelType', 'brand',
           'notRepairedDamage', 'dateCreated', 'nrOfPictures', 'postalCode',
           'lastSeen'],
          dtype='object')




```python
autos.columns = ['date_crawled', 'name', 'seller',
            'offer_type', 'price', 'ab_test',
            'vehicle_type', 'registration_year', 'gearbox',
            'power_PS', 'model', 'odometer', 
            'registration_month', 'fuel_type', 'brand',
            'unrepaired_damage', 'ad_created', 'nr_of_pictures',
            'postal_code', 'last_seen',]
```


```python
autos.columns
```




    Index(['date_crawled', 'name', 'seller', 'offer_type', 'price', 'ab_test',
           'vehicle_type', 'registration_year', 'gearbox', 'power_PS', 'model',
           'odometer', 'registration_month', 'fuel_type', 'brand',
           'unrepaired_damage', 'ad_created', 'nr_of_pictures', 'postal_code',
           'last_seen'],
          dtype='object')




```python
autos.head()
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
      <th>date_crawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offer_type</th>
      <th>price</th>
      <th>ab_test</th>
      <th>vehicle_type</th>
      <th>registration_year</th>
      <th>gearbox</th>
      <th>power_PS</th>
      <th>model</th>
      <th>odometer</th>
      <th>registration_month</th>
      <th>fuel_type</th>
      <th>brand</th>
      <th>unrepaired_damage</th>
      <th>ad_created</th>
      <th>nr_of_pictures</th>
      <th>postal_code</th>
      <th>last_seen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-26 17:47:46</td>
      <td>Peugeot_807_160_NAVTECH_ON_BOARD</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$5,000</td>
      <td>control</td>
      <td>bus</td>
      <td>2004</td>
      <td>manuell</td>
      <td>158</td>
      <td>andere</td>
      <td>150,000km</td>
      <td>3</td>
      <td>lpg</td>
      <td>peugeot</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>79588</td>
      <td>2016-04-06 06:45:54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-04-04 13:38:56</td>
      <td>BMW_740i_4_4_Liter_HAMANN_UMBAU_Mega_Optik</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,500</td>
      <td>control</td>
      <td>limousine</td>
      <td>1997</td>
      <td>automatik</td>
      <td>286</td>
      <td>7er</td>
      <td>150,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>bmw</td>
      <td>nein</td>
      <td>2016-04-04 00:00:00</td>
      <td>0</td>
      <td>71034</td>
      <td>2016-04-06 14:45:08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-26 18:57:24</td>
      <td>Volkswagen_Golf_1.6_United</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,990</td>
      <td>test</td>
      <td>limousine</td>
      <td>2009</td>
      <td>manuell</td>
      <td>102</td>
      <td>golf</td>
      <td>70,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>35394</td>
      <td>2016-04-06 20:15:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-12 16:58:10</td>
      <td>Smart_smart_fortwo_coupe_softouch/F1/Klima/Pan...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$4,350</td>
      <td>control</td>
      <td>kleinwagen</td>
      <td>2007</td>
      <td>automatik</td>
      <td>71</td>
      <td>fortwo</td>
      <td>70,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>smart</td>
      <td>nein</td>
      <td>2016-03-12 00:00:00</td>
      <td>0</td>
      <td>33729</td>
      <td>2016-03-15 03:16:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-04-01 14:38:50</td>
      <td>Ford_Focus_1_6_Benzin_TÜV_neu_ist_sehr_gepfleg...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,350</td>
      <td>test</td>
      <td>kombi</td>
      <td>2003</td>
      <td>manuell</td>
      <td>0</td>
      <td>focus</td>
      <td>150,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-04-01 00:00:00</td>
      <td>0</td>
      <td>39218</td>
      <td>2016-04-01 14:38:50</td>
    </tr>
  </tbody>
</table>
</div>



Above, I changed the column names from CamelCase to snakecase in order to be able to change whitespaces to underscores. Snakecase is python's more preferred method of typing column names.

## Exploring and cleaning columns


```python
autos.describe(include='all')
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
      <th>date_crawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offer_type</th>
      <th>price</th>
      <th>ab_test</th>
      <th>vehicle_type</th>
      <th>registration_year</th>
      <th>gearbox</th>
      <th>power_PS</th>
      <th>model</th>
      <th>odometer</th>
      <th>registration_month</th>
      <th>fuel_type</th>
      <th>brand</th>
      <th>unrepaired_damage</th>
      <th>ad_created</th>
      <th>nr_of_pictures</th>
      <th>postal_code</th>
      <th>last_seen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>44905</td>
      <td>50000.000000</td>
      <td>47320</td>
      <td>50000.000000</td>
      <td>47242</td>
      <td>50000</td>
      <td>50000.000000</td>
      <td>45518</td>
      <td>50000</td>
      <td>40171</td>
      <td>50000</td>
      <td>50000.0</td>
      <td>50000.000000</td>
      <td>50000</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>48213</td>
      <td>38754</td>
      <td>2</td>
      <td>2</td>
      <td>2357</td>
      <td>2</td>
      <td>8</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>245</td>
      <td>13</td>
      <td>NaN</td>
      <td>7</td>
      <td>40</td>
      <td>2</td>
      <td>76</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>39481</td>
    </tr>
    <tr>
      <th>top</th>
      <td>2016-04-02 11:37:04</td>
      <td>Ford_Fiesta</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$0</td>
      <td>test</td>
      <td>limousine</td>
      <td>NaN</td>
      <td>manuell</td>
      <td>NaN</td>
      <td>golf</td>
      <td>150,000km</td>
      <td>NaN</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-04-03 00:00:00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-04-07 06:17:27</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>3</td>
      <td>78</td>
      <td>49999</td>
      <td>49999</td>
      <td>1421</td>
      <td>25756</td>
      <td>12859</td>
      <td>NaN</td>
      <td>36993</td>
      <td>NaN</td>
      <td>4024</td>
      <td>32424</td>
      <td>NaN</td>
      <td>30107</td>
      <td>10687</td>
      <td>35232</td>
      <td>1946</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2005.073280</td>
      <td>NaN</td>
      <td>116.355920</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.723360</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50813.627300</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>105.712813</td>
      <td>NaN</td>
      <td>209.216627</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.711984</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>25779.747957</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1000.000000</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1067.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1999.000000</td>
      <td>NaN</td>
      <td>70.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>30451.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2003.000000</td>
      <td>NaN</td>
      <td>105.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>49577.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2008.000000</td>
      <td>NaN</td>
      <td>150.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>71540.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9999.000000</td>
      <td>NaN</td>
      <td>17700.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>99998.000000</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



The columns 'seller,' 'offer_type', 'ab_test,' and 'gearbox' all have only 2 values, which means they could probably be dropped. 'registration_year,' 'power_PS,' 'registration_month,' 'nr_of_pictures,' and 'postal_code' all have NaN values in the 'unique' row, as well as most other rows, meaning they need further investigation. The columns that have numeric values stored as test which need cleaning are 'price' and 'odometer.'


```python
autos['price'].describe()
```




    count     50000
    unique     2357
    top          $0
    freq       1421
    Name: price, dtype: object




```python
#cleaning 'price' column and converting to integer
autos['price'] = autos['price'].str.replace('$', '').str.replace(',', '').astype(int)
```


```python
#cleaning 'odometer' column and converting to integer
autos['odometer'] = autos['odometer'].str.replace('km', '').str.replace(',', '').astype(int)
```


```python
#renaming 'odometer' to 'odometer_km' to clarify it's in kilometers
autos.rename(columns={'odometer': 'odometer_km'}, inplace=True)
```


```python
#exploring unique values for 'price'
autos['price'].unique().shape
```




    (2357,)




```python
#checking cleaned column 'price' stats
autos['price'].describe()
```




    count    5.000000e+04
    mean     9.840044e+03
    std      4.811044e+05
    min      0.000000e+00
    25%      1.100000e+03
    50%      2.950000e+03
    75%      7.200000e+03
    max      1.000000e+08
    Name: price, dtype: float64




```python
#exploring unique value counts of 'price' column to see outliers and most common values
autos['price'].value_counts().sort_index()
```




    0           1421
    1            156
    2              3
    3              1
    5              2
                ... 
    10000000       1
    11111111       2
    12345678       3
    27322222       1
    99999999       1
    Name: price, Length: 2357, dtype: int64




```python
#looking at top of price list in ascending order to remove outliers
autos['price'].value_counts().head(10)
```




    0       1421
    500      781
    1500     734
    2500     643
    1000     639
    1200     639
    600      531
    800      498
    3500     498
    2000     460
    Name: price, dtype: int64




```python
#looking at bottom of price list in descending order to remove outliers
autos['price'].value_counts().sort_index(ascending=False).head(10)
```




    99999999    1
    27322222    1
    12345678    3
    11111111    2
    10000000    1
    3890000     1
    1300000     1
    1234566     1
    999999      2
    999990      1
    Name: price, dtype: int64




```python
#updating list to remove some outliers
autos = autos.loc[autos['price'].between(1,900000)]
```


```python
#exploring cleaned price list
autos['price'].describe()
```




    count     48565.000000
    mean       5888.935591
    std        9059.854754
    min           1.000000
    25%        1200.000000
    50%        3000.000000
    75%        7490.000000
    max      350000.000000
    Name: price, dtype: float64




```python
autos['price'].value_counts().sort_index(ascending=True).head()
```




    1    156
    2      3
    3      1
    5      2
    8      1
    Name: price, dtype: int64



The 'price' column seemed to have some outliers since the highest frequency row was '0' which would mean that either the person didn't enter a price in that field or they're giving their car away for free. Some had prices of $10, some $100 which are highly unlikely to be real, and some had over 1,000,000 which also seems unlikely to be real. To remove these outliers, I reran the column with only the prices between 100 and 900,000.

After removing the outliers in the 'price' column, we can see that the calculations of mean, standard deviation, minimum, maximum, and the percentages all make much more sense and seem to be normal for what you would see on a used car sales forum.


```python
#exploring unique values for 'odometer_km'
autos['odometer_km'].unique().shape
```




    (13,)




```python
#looking at 'odometer_km' column stats
autos['odometer_km'].describe()
```




    count     48565.000000
    mean     125770.101925
    std       39788.636804
    min        5000.000000
    25%      125000.000000
    50%      150000.000000
    75%      150000.000000
    max      150000.000000
    Name: odometer_km, dtype: float64




```python
#exploring value counts for 'odometer_km'
autos['odometer_km'].value_counts()
```




    150000    31414
    125000     5057
    100000     2115
    90000      1734
    80000      1415
    70000      1217
    60000      1155
    50000      1012
    5000        836
    40000       815
    30000       780
    20000       762
    10000       253
    Name: odometer_km, dtype: int64



For the 'odometer_km' column, there doesn't seem to be any outliers, so I left the column as-is. We can see from the values that the most frequent odometer reading is 150,000 31,228 entries. We can also see that the majority of cars listed for sale have more than 100,000 km on the odometer, and that any cars with 40,000 or less km have less than 1000 listings respectively.

## Exploring auto listing and view data


```python
date_crawl = (autos['date_crawled'].str[:10])
print (date_crawl.value_counts(normalize=True, dropna=False).sort_index())
```

    2016-03-05    0.025327
    2016-03-06    0.014043
    2016-03-07    0.036014
    2016-03-08    0.033296
    2016-03-09    0.033090
    2016-03-10    0.032184
    2016-03-11    0.032575
    2016-03-12    0.036920
    2016-03-13    0.015670
    2016-03-14    0.036549
    2016-03-15    0.034284
    2016-03-16    0.029610
    2016-03-17    0.031628
    2016-03-18    0.012911
    2016-03-19    0.034778
    2016-03-20    0.037887
    2016-03-21    0.037373
    2016-03-22    0.032987
    2016-03-23    0.032225
    2016-03-24    0.029342
    2016-03-25    0.031607
    2016-03-26    0.032204
    2016-03-27    0.031092
    2016-03-28    0.034860
    2016-03-29    0.034099
    2016-03-30    0.033687
    2016-03-31    0.031834
    2016-04-01    0.033687
    2016-04-02    0.035478
    2016-04-03    0.038608
    2016-04-04    0.036487
    2016-04-05    0.013096
    2016-04-06    0.003171
    2016-04-07    0.001400
    Name: date_crawled, dtype: float64


The 'date_crawled' column shows the percent of listings that were crawled by the browser on each of the listed dates. We can see it's mostly similar but tapers off towards the last few dates as those are the most recent and would have the least amount of listings crawled.


```python
ad_create = (autos['ad_created'].str[:10])
print (ad_create.value_counts(normalize=True, dropna=False).sort_index())
```

    2015-06-11    0.000021
    2015-08-10    0.000021
    2015-09-09    0.000021
    2015-11-10    0.000021
    2015-12-05    0.000021
                    ...   
    2016-04-03    0.038855
    2016-04-04    0.036858
    2016-04-05    0.011819
    2016-04-06    0.003253
    2016-04-07    0.001256
    Name: ad_created, Length: 76, dtype: float64


From the 'ad_created' column we can see there were far less listings in the beginning of the data (June 2015 - February 2016) than in the latter data in March and April. If this data is what is currently listed, this makes sense as we would expect that most of the earlier listings have been sold/taken down already versus the more current listings. This can also tell us that most listings usually will be taken down in only 2 months, but that there will be some stragglers each month.


```python
last_see = (autos['last_seen'].str[:10])
print (last_see.value_counts(normalize=True, dropna=False).sort_index())
```

By the title of the column, 'last_seen', as well as the data we can assume that this column refers to the last time the listing was seen by a consumer/user of the site. As we would expect, the values ascend as the dates become recent. This would make sense because most listings that are still available on the site should have been seen recently and most of the ones that haven't been seen for months should be taken down already, so again we seem to have some stragglers that need to be taken down from the site.

## Cleaning 'registration_year'


```python
autos['registration_year'].describe()
```

There is clearly some incorrect information in this column since the minimum registration year can't possibly be 1000 and the maximum can't possibly be 9999. This means we will need to clean this column to remove these outliers and analyze these values correctly.


```python
autos = autos.loc[autos['registration_year'].between(1900,2016)]
autos['registration_year'].value_counts(normalize=True).sort_index()
```

By cleaning the data and only looking at the registration years 1900-2016, we can see that the years 1910-2016 seem to be the most accurate.

## Exploring and aggregating 'brand' column


```python
autos['brand'].value_counts(normalize=True)
```

After looking at the 'brand' column values, I've decided to aggregate the data by any brand with over 5% of listings. This gives us the top 6 brands which are: Volkswagon, BMW, Opel, Mercedes Benz, Audi, and Ford.


```python
brands = autos['brand'].value_counts(normalize=True)
#creating the top 6 list of brands by filtering only the brands = or above 0.05
top_6_brands = brands[brands >= .05].index                     
print (top_6_brands)
```


```python
#aggregating mean prices by top 6 brands
brand_mean_prices = {}
for row in top_6_brands:
    selected_rows = autos[autos['brand']==row]
    mean_price = int(selected_rows['price'].mean())
    brand_mean_prices[row] = mean_price
#creating series for top 6 brands and mean prices
bmp_series = pd.Series(brand_mean_prices)
print (bmp_series)
```

From the results of the aggregate brand and mean price data, we can see that Opel brand has the lowest mean value, and Audi has the highest with Mercedes and BMW following closely behind. Volkswagon and Ford have mid-range mean values. 


```python
#aggregating mean mileage by top 6 brands
brand_mean_mileage = {}
for row in top_6_brands:
    selected_rows = autos[autos['brand']==row]
    mean_mileage = int(selected_rows['odometer_km'].mean())
    brand_mean_mileage[row] = mean_mileage
#creating series for top 6 brands and mean mileage
bmm_series = pd.Series(brand_mean_mileage)
print (bmm_series)
```


```python
#creating new DF of top 6 brands with mean price and mean mileage
autos = pd.DataFrame({'mean_price': bmp_series, 'mean_mileage': bmm_series})
print (autos.sort_values('mean_price'))
```

## Analysis & Conclusion

By comparing the mean mileage and the mean price of the top 6 brands, we can see that the mileage does not seem to effect the prices of these brands. The higher priced brands actually have a higher mean mileage than nearly all the lower priced brands. This implies that these brands tend to be higher priced in general, even when they have the same or higher mileage than one of the brands with the lower price means. This makes sense when you consider Audi, Mercedes, and BMW are luxury car brands and they're initial prices are typically much higher than the other brands.
