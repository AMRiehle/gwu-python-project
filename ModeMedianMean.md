

```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats
from matplotlib.ticker import  FuncFormatter, MaxNLocator


house_df = pd.read_csv("Arlington_County_Sales_2017.csv")
house_df.head()
pd.set_option("display.max_columns", 500)
counter = 0
for column in house_df:

    if house_df[column].isnull().sum()>= 1000:
        house_df.drop(column, axis=1, inplace = True)
house_df.to_csv("Trimmed")
```


```python
majorLocator = MultipleLocator(20)
majorFormatter = FormatStrFormatter('%d')
minorLocator = MultipleLocator(5)
```


```python
house_df
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
      <th>FullStreetAddress</th>
      <th>Amenities</th>
      <th>Appliances</th>
      <th>AssessmentYear</th>
      <th>Attic</th>
      <th>Baths</th>
      <th>BathsFull</th>
      <th>BathsHalf</th>
      <th>Beds</th>
      <th>CityName</th>
      <th>CloseDate</th>
      <th>ClosePrice</th>
      <th>ContractDate</th>
      <th>County</th>
      <th>CountyTax</th>
      <th>CountyTaxPaymentFreq</th>
      <th>DaysOnMarket</th>
      <th>DomProperty</th>
      <th>Fireplaces</th>
      <th>Foreclosure</th>
      <th>Heating</th>
      <th>HOA</th>
      <th>HotWater</th>
      <th>ImprovementAssessmentAmount</th>
      <th>ImprovementAssessmentPaymentFreq</th>
      <th>InteriorFeatures</th>
      <th>LandAssessmentAmount</th>
      <th>LandAssessmentPaymentFreq</th>
      <th>Stories</th>
      <th>ListDate</th>
      <th>ListPrice</th>
      <th>ListingLowPrice</th>
      <th>ListingType</th>
      <th>Longitude</th>
      <th>ListingID</th>
      <th>OriginalListPrice</th>
      <th>Ownership</th>
      <th>Parking</th>
      <th>PropertyType</th>
      <th>Remarks</th>
      <th>ShowDays</th>
      <th>StreetName</th>
      <th>StreetNumber</th>
      <th>Style</th>
      <th>ListingTaxID</th>
      <th>TotalAssessment</th>
      <th>TotalOpenHouses</th>
      <th>TotalShowings</th>
      <th>LivingArea</th>
      <th>TotalTaxes</th>
      <th>TotalTours</th>
      <th>Type</th>
      <th>YearBuilt</th>
      <th>Zip4</th>
      <th>PostalCode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3601 5TH ST S #504</td>
      <td>NaN</td>
      <td>Dishwasher, Disposal, Refrigerator, Range Hood...</td>
      <td>2014.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-02-22</td>
      <td>185000.0</td>
      <td>2017-01-15</td>
      <td>ARLINGTON</td>
      <td>1872.62</td>
      <td>Annually</td>
      <td>688</td>
      <td>688</td>
      <td>0</td>
      <td>False</td>
      <td>Summer / Winter Changeover</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>154100.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>36400.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2015-02-27</td>
      <td>192500.0</td>
      <td>192500.0</td>
      <td>Excl. Right</td>
      <td>-77.096760</td>
      <td>AR8563022</td>
      <td>229000.0</td>
      <td>Condo</td>
      <td>Unassigned</td>
      <td>Residential</td>
      <td>This condo has been thoroughly renovated just ...</td>
      <td>NaN</td>
      <td>5TH</td>
      <td>3601.0</td>
      <td>Contemporary</td>
      <td>23-015-111</td>
      <td>190500</td>
      <td>0</td>
      <td>0</td>
      <td>1011</td>
      <td>1897.38</td>
      <td>1</td>
      <td>Mid-Rise 5-8 Floors</td>
      <td>1958</td>
      <td>1636.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1600 OAK ST #1915/1914</td>
      <td>Built-in Bookcases, Chair Railing, Crown Moldi...</td>
      <td>Cooktop, Dishwasher, Disposal, Dryer, Exhaust ...</td>
      <td>2015.0</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-02-21</td>
      <td>1700000.0</td>
      <td>2016-11-16</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>514</td>
      <td>514</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>1648000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>122000.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2015-06-22</td>
      <td>1850000.0</td>
      <td>1850000.0</td>
      <td>Excl. Right</td>
      <td>-77.073770</td>
      <td>AR8673996</td>
      <td>2800000.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>A blend of two homes-3,390 interior sqft. w/mu...</td>
      <td>All Days</td>
      <td>OAK</td>
      <td>1600.0</td>
      <td>Contemporary</td>
      <td>17-003-291</td>
      <td>1770000</td>
      <td>0</td>
      <td>0</td>
      <td>3390</td>
      <td>17629.00</td>
      <td>1</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1986</td>
      <td>2760.0</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1719 GREENBRIER ST</td>
      <td>Attic - Finished, Automatic Garage Door Opener...</td>
      <td>ENERGY STAR Dishwasher, ENERGY STAR Refrigerat...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>8</td>
      <td>7</td>
      <td>1</td>
      <td>7</td>
      <td>ARLINGTON</td>
      <td>2017-03-03</td>
      <td>1625000.0</td>
      <td>2017-01-08</td>
      <td>ARLINGTON</td>
      <td>7353.82</td>
      <td>Annually</td>
      <td>489</td>
      <td>489</td>
      <td>1</td>
      <td>False</td>
      <td>ENERGY STAR Heating System, Forced Air, Heat P...</td>
      <td>False</td>
      <td>Natural Gas, 60 or More Gallon Tank</td>
      <td>173100.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>575000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2015-09-08</td>
      <td>1695000.0</td>
      <td>1695000.0</td>
      <td>Excl. Right</td>
      <td>-77.130370</td>
      <td>AR8742330</td>
      <td>1751000.0</td>
      <td>Fee Simple</td>
      <td>Garage, Basement Garage, Drvwy/Off Str, Paved ...</td>
      <td>Residential</td>
      <td>New Custom Arts and Crafts home by Calvert Hom...</td>
      <td>NaN</td>
      <td>GREENBRIER</td>
      <td>1719.0</td>
      <td>Arts &amp; Crafts</td>
      <td>09-016-016</td>
      <td>748100</td>
      <td>0</td>
      <td>0</td>
      <td>5994</td>
      <td>7451.08</td>
      <td>1</td>
      <td>Detached</td>
      <td>2016</td>
      <td>3629.0</td>
      <td>22205</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3723 FOUR MILE RUN DR</td>
      <td>NaN</td>
      <td>Dishwasher, Disposal, Oven / Range - Gas, Refr...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-01-17</td>
      <td>430000.0</td>
      <td>2016-12-03</td>
      <td>ARLINGTON</td>
      <td>3361.86</td>
      <td>Annually</td>
      <td>121</td>
      <td>121</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>152000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>190000.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2015-09-20</td>
      <td>475000.0</td>
      <td>475000.0</td>
      <td>Excl. Right</td>
      <td>-77.090230</td>
      <td>AR8747453</td>
      <td>450000.0</td>
      <td>Fee Simple</td>
      <td>Street</td>
      <td>Residential</td>
      <td>Perfect location!  This is your client's oppor...</td>
      <td>All Days</td>
      <td>FOUR MILE RUN</td>
      <td>3723.0</td>
      <td>Federal</td>
      <td>31-030-066</td>
      <td>342000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3406.32</td>
      <td>1</td>
      <td>Semi-Detached</td>
      <td>1945</td>
      <td>2332.0</td>
      <td>22206</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2005 KEY BLVD #11579</td>
      <td>Bathroom(s) - Ceramic Tile, Countertop(s) - Gr...</td>
      <td>Dishwasher, Disposal, Exhaust Fan, Microwave, ...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-04-07</td>
      <td>362000.0</td>
      <td>2017-03-06</td>
      <td>ARLINGTON</td>
      <td>3386.81</td>
      <td>Annually</td>
      <td>81</td>
      <td>81</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s), Forced Air</td>
      <td>True</td>
      <td>Electric</td>
      <td>309700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>36600.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-12-10</td>
      <td>365000.0</td>
      <td>365000.0</td>
      <td>Excl. Right</td>
      <td>-77.083800</td>
      <td>AR9823220</td>
      <td>369000.0</td>
      <td>Condo</td>
      <td>Street</td>
      <td>Residential</td>
      <td>Fully updated 2BR/1BA corner unit in Colonial ...</td>
      <td>NaN</td>
      <td>KEY</td>
      <td>2005.0</td>
      <td>Rambler</td>
      <td>16-026-213</td>
      <td>346300</td>
      <td>0</td>
      <td>0</td>
      <td>852</td>
      <td>3431.80</td>
      <td>0</td>
      <td>Garden 1-4 Floors</td>
      <td>1940</td>
      <td>NaN</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1719 GLEBE RD N</td>
      <td>Fireplace Mantel(s), Countertop(s) - Granite, ...</td>
      <td>Dishwasher, Disposal, Dryer, Exhaust Fan, Icem...</td>
      <td>2016.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-04-28</td>
      <td>760000.0</td>
      <td>2017-03-25</td>
      <td>ARLINGTON</td>
      <td>7480.72</td>
      <td>Annually</td>
      <td>12</td>
      <td>12</td>
      <td>1</td>
      <td>False</td>
      <td>Radiator</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>288700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>476200.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-03-09</td>
      <td>765000.0</td>
      <td>765000.0</td>
      <td>Excl. Right</td>
      <td>-77.119080</td>
      <td>AR9882001</td>
      <td>765000.0</td>
      <td>Fee Simple</td>
      <td>Garage, Drvwy/Off Str</td>
      <td>Residential</td>
      <td>Stylish, high end renovations of Georgetown st...</td>
      <td>All Days</td>
      <td>GLEBE</td>
      <td>1719.0</td>
      <td>Colonial</td>
      <td>07-025-004</td>
      <td>764900</td>
      <td>0</td>
      <td>0</td>
      <td>1854</td>
      <td>7580.14</td>
      <td>1</td>
      <td>Detached</td>
      <td>1937</td>
      <td>2037.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1400 KENMORE ST</td>
      <td>Attic - Floored, Attic - Stairs Fixed, Attic -...</td>
      <td>Dishwasher, Disposal, Dryer, Extra Refrigerato...</td>
      <td>2016.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>4</td>
      <td>ARLINGTON</td>
      <td>2017-04-07</td>
      <td>930000.0</td>
      <td>2017-03-15</td>
      <td>ARLINGTON</td>
      <td>7869.97</td>
      <td>Annually</td>
      <td>7</td>
      <td>7</td>
      <td>1</td>
      <td>False</td>
      <td>Wall Unit, Radiator</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>192700.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>612000.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-03-07</td>
      <td>899000.0</td>
      <td>899000.0</td>
      <td>Excl. Right</td>
      <td>-77.102050</td>
      <td>AR9881038</td>
      <td>899000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str, Garage, Paved Driveway, Asphalt...</td>
      <td>Residential</td>
      <td>Fabulous location! Near Clarendon, Vir. Sq. &amp; ...</td>
      <td>All Days</td>
      <td>KENMORE</td>
      <td>1400.0</td>
      <td>Traditional</td>
      <td>15-039-029</td>
      <td>804700</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>7974.56</td>
      <td>2</td>
      <td>Detached</td>
      <td>1942</td>
      <td>4912.0</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1800 WILSON BLVD #222</td>
      <td>Automatic Garage Door Opener, Elevator, Closet...</td>
      <td>Dishwasher, Disposal, Exhaust Fan, Icemaker, M...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>ARLINGTON</td>
      <td>2017-05-10</td>
      <td>392000.0</td>
      <td>2017-04-03</td>
      <td>ARLINGTON</td>
      <td>3576.55</td>
      <td>Annually</td>
      <td>10</td>
      <td>10</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>326200.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>39500.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-03-24</td>
      <td>399900.0</td>
      <td>399900.0</td>
      <td>Excl. Right</td>
      <td>-77.079100</td>
      <td>AR9895940</td>
      <td>399900.0</td>
      <td>Condo</td>
      <td>Assigned, Covered Parking, Garage, Prk Space C...</td>
      <td>Residential</td>
      <td>When this condo was built, AHC purchased sever...</td>
      <td>All Days</td>
      <td>WILSON</td>
      <td>1800.0</td>
      <td>Contemporary</td>
      <td>17-010-138</td>
      <td>365700</td>
      <td>0</td>
      <td>1</td>
      <td>718</td>
      <td>3624.08</td>
      <td>3</td>
      <td>Garden 1-4 Floors</td>
      <td>2007</td>
      <td>6604.0</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4195 FOUR MILE RUN DR S #201</td>
      <td>Closet - Master Bedroom Walk-in, Countertop(s)...</td>
      <td>Dishwasher, Disposal, Dryer, Refrigerator, Ice...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>ARLINGTON</td>
      <td>2017-06-29</td>
      <td>313000.0</td>
      <td>2017-05-26</td>
      <td>ARLINGTON</td>
      <td>3009.31</td>
      <td>Annually</td>
      <td>17</td>
      <td>17</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Electric</td>
      <td>273700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>34000.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-05-09</td>
      <td>313000.0</td>
      <td>313000.0</td>
      <td>Excl. Right</td>
      <td>-77.097465</td>
      <td>AR9941117</td>
      <td>316000.0</td>
      <td>Condo</td>
      <td>Unassigned, Surface</td>
      <td>Residential</td>
      <td>Sunny, pristine condo at West Village of Shirl...</td>
      <td>All Days</td>
      <td>FOUR MILE RUN</td>
      <td>4195.0</td>
      <td>Contemporary</td>
      <td>27-007-579</td>
      <td>307700</td>
      <td>0</td>
      <td>0</td>
      <td>851</td>
      <td>3049.30</td>
      <td>2</td>
      <td>Garden 1-4 Floors</td>
      <td>1966</td>
      <td>3986.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6961 FAIRFAX DR</td>
      <td>Bathroom(s) - Ceramic Tile, Closet - Master Be...</td>
      <td>Central Vacuum, Dishwasher, Disposal, Dryer, M...</td>
      <td>2016.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-08-04</td>
      <td>639000.0</td>
      <td>2017-07-12</td>
      <td>ARLINGTON</td>
      <td>5522.77</td>
      <td>Annually</td>
      <td>7</td>
      <td>7</td>
      <td>1</td>
      <td>False</td>
      <td>Programmable Thermostat, Zoned</td>
      <td>False</td>
      <td>Electric</td>
      <td>204700.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>360000.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-07-05</td>
      <td>642144.0</td>
      <td>642144.0</td>
      <td>Excl. Right</td>
      <td>-77.167080</td>
      <td>AR9988772</td>
      <td>642144.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Beautiful 3 BR, 3 BA End unit townhouse in Bro...</td>
      <td>All Days</td>
      <td>FAIRFAX</td>
      <td>6961.0</td>
      <td>Traditional</td>
      <td>01-010-041</td>
      <td>564700</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5596.16</td>
      <td>1</td>
      <td>Townhouse</td>
      <td>1988</td>
      <td>1008.0</td>
      <td>22213</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2200 WESTMORELAND ST N #420</td>
      <td>Attached Master Bathroom, Closet - Master Bedr...</td>
      <td>Dishwasher, Dryer - Front Loading, Icemaker, M...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-10-09</td>
      <td>565000.0</td>
      <td>2017-09-27</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>42</td>
      <td>42</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>440100.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>52700.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-08-16</td>
      <td>565000.0</td>
      <td>565000.0</td>
      <td>Excl. Right</td>
      <td>-77.162653</td>
      <td>AR9010756</td>
      <td>574900.0</td>
      <td>Condo</td>
      <td>Assigned</td>
      <td>Residential</td>
      <td>Spectacular 2 BR &amp; DEN /2 BA in sought after W...</td>
      <td>All Days</td>
      <td>WESTMORELAND</td>
      <td>2200.0</td>
      <td>Contemporary</td>
      <td>11-011-118</td>
      <td>492800</td>
      <td>0</td>
      <td>1</td>
      <td>1172</td>
      <td>4883.64</td>
      <td>2</td>
      <td>Mid-Rise 5-8 Floors</td>
      <td>2006</td>
      <td>1051.0</td>
      <td>22213</td>
    </tr>
    <tr>
      <th>11</th>
      <td>832 GREENBRIER ST S #1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-03-23</td>
      <td>140000.0</td>
      <td>2017-02-23</td>
      <td>ARLINGTON</td>
      <td>1138.31</td>
      <td>Annually</td>
      <td>407</td>
      <td>407</td>
      <td>0</td>
      <td>False</td>
      <td>Radiator</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>91500.0</td>
      <td>Annually</td>
      <td>Flat</td>
      <td>24300.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2015-10-20</td>
      <td>150000.0</td>
      <td>150000.0</td>
      <td>Excl. Right</td>
      <td>-77.119080</td>
      <td>AR9501967</td>
      <td>180000.0</td>
      <td>Condo</td>
      <td>Assigned, Surface</td>
      <td>Residential</td>
      <td>Price reduced for quick sell.Contract failed d...</td>
      <td>All Days</td>
      <td>GREENBRIER</td>
      <td>832.0</td>
      <td>Other</td>
      <td>22-011-212</td>
      <td>115800</td>
      <td>0</td>
      <td>0</td>
      <td>695</td>
      <td>1153.37</td>
      <td>1</td>
      <td>Garden 1-4 Floors</td>
      <td>1948</td>
      <td>2712.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2704 BUCHANAN ST N</td>
      <td>Attached Master Bathroom, Attic - Stairs Pull ...</td>
      <td>Dishwasher, Disposal, Humidifier, Icemaker, Mi...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>7</td>
      <td>ARLINGTON</td>
      <td>2017-07-21</td>
      <td>1999900.0</td>
      <td>2016-01-06</td>
      <td>ARLINGTON</td>
      <td>6494.68</td>
      <td>Annually</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas, 60 or More Gallon Tank</td>
      <td>142000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>518700.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2016-01-05</td>
      <td>1999900.0</td>
      <td>1999900.0</td>
      <td>Excl. Right</td>
      <td>-77.129570</td>
      <td>AR9546034</td>
      <td>1999900.0</td>
      <td>Fee Simple</td>
      <td>Garage, Drvwy/Off Str</td>
      <td>Residential</td>
      <td>Fabulous new design by Arlington's premier bui...</td>
      <td>All Days</td>
      <td>BUCHANAN</td>
      <td>2704.0</td>
      <td>Colonial</td>
      <td>02-088-046</td>
      <td>660700</td>
      <td>0</td>
      <td>0</td>
      <td>6305</td>
      <td>6580.57</td>
      <td>0</td>
      <td>Detached</td>
      <td>2017</td>
      <td>2725.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>13</th>
      <td>28 S PERSHING DR</td>
      <td>Attic - Stairs Pull Down, Automatic Garage Doo...</td>
      <td>Dishwasher, Disposal, Dryer, Exhaust Fan, Icem...</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-02-17</td>
      <td>487500.0</td>
      <td>2016-08-01</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>413</td>
      <td>632</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air, Heat Pump(s), Zoned</td>
      <td>False</td>
      <td>60 or More Gallon Tank, Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2</td>
      <td>2016-01-18</td>
      <td>979000.0</td>
      <td>979000.0</td>
      <td>Excl. Agency</td>
      <td>-77.110890</td>
      <td>AR9555136</td>
      <td>999000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str, Garage</td>
      <td>Residential</td>
      <td>This is an MLS Placement Limited Service Listi...</td>
      <td>All Days</td>
      <td>S PERSHING</td>
      <td>28.0</td>
      <td>Craftsman</td>
      <td>23-004-026</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3200</td>
      <td>NaN</td>
      <td>1</td>
      <td>Detached</td>
      <td>2016</td>
      <td>1356.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1001 VERMONT ST #614</td>
      <td>NaN</td>
      <td>Dishwasher, Disposal, Microwave, Oven / Range ...</td>
      <td>2015.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-01-30</td>
      <td>410000.0</td>
      <td>2016-12-21</td>
      <td>ARLINGTON</td>
      <td>4141.38</td>
      <td>Annually</td>
      <td>300</td>
      <td>300</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>False</td>
      <td>Electric</td>
      <td>388700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>32600.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-02-24</td>
      <td>419999.0</td>
      <td>419999.0</td>
      <td>Excl. Agency</td>
      <td>-77.114370</td>
      <td>AR9578263</td>
      <td>435000.0</td>
      <td>Condo</td>
      <td>Underground</td>
      <td>Residential</td>
      <td>LUXURY 2 BR condo in the heart of Ballston!  F...</td>
      <td>All Days</td>
      <td>VERMONT</td>
      <td>1001.0</td>
      <td>Traditional</td>
      <td>14-017-152</td>
      <td>421300</td>
      <td>0</td>
      <td>0</td>
      <td>814</td>
      <td>4196.15</td>
      <td>1</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>2005</td>
      <td>4766.0</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6318 31ST ST N</td>
      <td>Attic - Finished, Automatic Garage Door Opener...</td>
      <td>Dishwasher, Disposal, Exhaust Fan, Icemaker, M...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-08-08</td>
      <td>1729000.0</td>
      <td>2016-05-10</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>69</td>
      <td>145</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air, Wood Burning Stove, Zoned</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>105200.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>545000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2016-03-03</td>
      <td>1749000.0</td>
      <td>1749000.0</td>
      <td>Modified/Excl</td>
      <td>-77.155344</td>
      <td>AR9585142</td>
      <td>1749000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Looking for new construction but tired of the ...</td>
      <td>All Days</td>
      <td>31ST</td>
      <td>6318.0</td>
      <td>Farm House</td>
      <td>01-021-002</td>
      <td>650200</td>
      <td>0</td>
      <td>0</td>
      <td>5500</td>
      <td>6475.99</td>
      <td>1</td>
      <td>Detached</td>
      <td>2015</td>
      <td>1123.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>16</th>
      <td>664 29TH RD S</td>
      <td>Attic - Access Only, Automatic Garage Door Ope...</td>
      <td>Cooktop, Dishwasher, Disposal, Dryer - Front L...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>4</td>
      <td>3</td>
      <td>1</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-02-16</td>
      <td>1149000.0</td>
      <td>2017-01-11</td>
      <td>ARLINGTON</td>
      <td>9551.81</td>
      <td>Annually</td>
      <td>202</td>
      <td>202</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air, Heat Pump(s)</td>
      <td>False</td>
      <td>60 or More Gallon Tank, Natural Gas</td>
      <td>595800.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>427500.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2016-03-24</td>
      <td>1149900.0</td>
      <td>1149900.0</td>
      <td>Excl. Right</td>
      <td>-77.056092</td>
      <td>AR9605099</td>
      <td>1269000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str, Garage, Paved Driveway, Street,...</td>
      <td>Residential</td>
      <td>MASSIVE PRICE DROP ~ This hard-to-find Arlingt...</td>
      <td>All Days</td>
      <td>29TH</td>
      <td>664.0</td>
      <td>Contemporary</td>
      <td>37-027-040</td>
      <td>1023300</td>
      <td>0</td>
      <td>0</td>
      <td>3493</td>
      <td>9678.13</td>
      <td>1</td>
      <td>Detached</td>
      <td>1990</td>
      <td>2315.0</td>
      <td>22202</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2004 CULPEPER ST N</td>
      <td>Automatic Garage Door Opener, Bathroom(s) - Ce...</td>
      <td>Dishwasher, Cooktop, Disposal, Dryer, Dryer - ...</td>
      <td>2015.0</td>
      <td>No</td>
      <td>7</td>
      <td>5</td>
      <td>2</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-01-05</td>
      <td>1050000.0</td>
      <td>2016-11-16</td>
      <td>ARLINGTON</td>
      <td>10517.12</td>
      <td>Annually</td>
      <td>224</td>
      <td>224</td>
      <td>3</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Electric, Natural Gas</td>
      <td>609900.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>460000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2016-04-03</td>
      <td>1099000.0</td>
      <td>1099000.0</td>
      <td>Excl. Right</td>
      <td>-77.126214</td>
      <td>AR9615310</td>
      <td>1199888.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>***OWNER SAYS SELL***BRING ALL OFFERS***1 Mile...</td>
      <td>All Days</td>
      <td>CULPEPER</td>
      <td>2004.0</td>
      <td>Arts &amp; Crafts</td>
      <td>08-011-032</td>
      <td>1069900</td>
      <td>0</td>
      <td>1</td>
      <td>6550</td>
      <td>10656.20</td>
      <td>2</td>
      <td>Detached</td>
      <td>2008</td>
      <td>2005.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1309 S. QUINN ST</td>
      <td>NaN</td>
      <td>ENERGY STAR Dishwasher, ENERGY STAR Refrigerat...</td>
      <td>NaN</td>
      <td>No</td>
      <td>4</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-02-24</td>
      <td>740285.0</td>
      <td>2016-06-10</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44</td>
      <td>44</td>
      <td>0</td>
      <td>False</td>
      <td>ENERGY STAR Heating System</td>
      <td>True</td>
      <td>Instant Hot Water, Tankless Water Heater</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2016-04-06</td>
      <td>740285.0</td>
      <td>740285.0</td>
      <td>Excl. Agency</td>
      <td>-77.073900</td>
      <td>AR9618603</td>
      <td>724900.0</td>
      <td>Fee Simple</td>
      <td>Garage, Garage Door Opener, Paved Driveway</td>
      <td>Residential</td>
      <td>Introducing Carver Place, an exciting new cons...</td>
      <td>All Days</td>
      <td>S. QUINN</td>
      <td>1309.0</td>
      <td>Craftsman</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2080</td>
      <td>NaN</td>
      <td>1</td>
      <td>Townhouse</td>
      <td>2016</td>
      <td>NaN</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2834 SOMERSET ST N</td>
      <td>Attached Master Bathroom, Attic - Stairs Pull ...</td>
      <td>Dishwasher, Disposal</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-05-23</td>
      <td>1635000.0</td>
      <td>2017-04-03</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>355</td>
      <td>355</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>770700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>688800.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2016-04-13</td>
      <td>1649900.0</td>
      <td>1649900.0</td>
      <td>Excl. Right</td>
      <td>-77.158123</td>
      <td>AR9625262</td>
      <td>1699000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Move in ready! Modern Craftsman on 1/3 acre at...</td>
      <td>NaN</td>
      <td>SOMERSET</td>
      <td>2834.0</td>
      <td>Craftsman</td>
      <td>01-019-030</td>
      <td>1459500</td>
      <td>0</td>
      <td>1</td>
      <td>5035</td>
      <td>7662.38</td>
      <td>3</td>
      <td>Detached</td>
      <td>2016</td>
      <td>1219.0</td>
      <td>22213</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2408 1ST RD S</td>
      <td>Closet(s) - Walk-in, Countertop(s) - Granite, ...</td>
      <td>Central Vacuum, Dishwasher, Disposal, Dryer, I...</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>6</td>
      <td>ARLINGTON</td>
      <td>2017-02-06</td>
      <td>1187000.0</td>
      <td>2016-12-29</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>261</td>
      <td>261</td>
      <td>1</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2016-04-12</td>
      <td>1249888.0</td>
      <td>1249888.0</td>
      <td>Excl. Right</td>
      <td>-77.085140</td>
      <td>AR9624755</td>
      <td>1349888.0</td>
      <td>Fee Simple</td>
      <td>Paved Driveway</td>
      <td>Residential</td>
      <td>Ultra Luxurious custom home in the heart of Ar...</td>
      <td>NaN</td>
      <td>1ST</td>
      <td>2408.0</td>
      <td>Craftsman</td>
      <td>24-005-007</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3977</td>
      <td>NaN</td>
      <td>2</td>
      <td>Detached</td>
      <td>2016</td>
      <td>1823.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>21</th>
      <td>4141 HENDERSON RD #814</td>
      <td>Closet(s) - Walk-in, Countertop(s) - Granite, ...</td>
      <td>Dishwasher, Refrigerator, Oven / Range - Gas</td>
      <td>2015.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>ARLINGTON</td>
      <td>2017-01-31</td>
      <td>244000.0</td>
      <td>2016-12-17</td>
      <td>ARLINGTON</td>
      <td>2407.37</td>
      <td>Annually</td>
      <td>249</td>
      <td>249</td>
      <td>0</td>
      <td>False</td>
      <td>Central</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>223200.0</td>
      <td>Annually</td>
      <td>Efficiency</td>
      <td>21700.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-04-13</td>
      <td>249900.0</td>
      <td>249900.0</td>
      <td>Excl. Right</td>
      <td>-77.109480</td>
      <td>AR9625903</td>
      <td>249900.0</td>
      <td>Condo</td>
      <td>On-site Prk/Rent</td>
      <td>Residential</td>
      <td>Enjoy Beautiful Sunset from your balcony,Or wa...</td>
      <td>All Days</td>
      <td>HENDERSON</td>
      <td>4141.0</td>
      <td>Contemporary</td>
      <td>20-012-223</td>
      <td>244900</td>
      <td>0</td>
      <td>0</td>
      <td>542</td>
      <td>2439.20</td>
      <td>1</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1973</td>
      <td>2467.0</td>
      <td>22203</td>
    </tr>
    <tr>
      <th>22</th>
      <td>4118 27TH RD N</td>
      <td>Attached Master Bathroom, Automatic Garage Doo...</td>
      <td>Dishwasher, Disposal, Dryer, Microwave, Oven -...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>ARLINGTON</td>
      <td>2017-02-10</td>
      <td>950000.0</td>
      <td>2017-01-10</td>
      <td>ARLINGTON</td>
      <td>8340.76</td>
      <td>Annually</td>
      <td>229</td>
      <td>229</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>258500.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>590000.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2016-04-16</td>
      <td>929000.0</td>
      <td>929000.0</td>
      <td>Excl. Right</td>
      <td>-77.112880</td>
      <td>AR9629124</td>
      <td>995000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str, Garage</td>
      <td>Residential</td>
      <td>Schedule showings online through showingtime. ...</td>
      <td>All Days</td>
      <td>27TH</td>
      <td>4118.0</td>
      <td>Split Foyer</td>
      <td>05-001-027</td>
      <td>848500</td>
      <td>0</td>
      <td>1</td>
      <td>2349</td>
      <td>8451.06</td>
      <td>3</td>
      <td>Detached</td>
      <td>1965</td>
      <td>5116.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>23</th>
      <td>412 GARFIELD ST N</td>
      <td>Automatic Garage Door Opener, Chair Railing, C...</td>
      <td>Cooktop, Dishwasher, Disposal, Dryer, Microwav...</td>
      <td>NaN</td>
      <td>No</td>
      <td>5</td>
      <td>5</td>
      <td>0</td>
      <td>7</td>
      <td>ARLINGTON</td>
      <td>2017-03-31</td>
      <td>1735000.0</td>
      <td>2017-01-23</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>262</td>
      <td>262</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3</td>
      <td>2016-05-06</td>
      <td>1888000.0</td>
      <td>1888000.0</td>
      <td>Excl. Right</td>
      <td>-77.093210</td>
      <td>AR9631923</td>
      <td>2000000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Exotic-European Flair &amp; Noble Ambiance! Luxury...</td>
      <td>NaN</td>
      <td>GARFIELD</td>
      <td>412.0</td>
      <td>Colonial</td>
      <td>18-049-013</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5750</td>
      <td>NaN</td>
      <td>2</td>
      <td>Detached</td>
      <td>2005</td>
      <td>1610.0</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1319 S. QUINN</td>
      <td>NaN</td>
      <td>ENERGY STAR Dishwasher, ENERGY STAR Refrigerat...</td>
      <td>NaN</td>
      <td>No</td>
      <td>4</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-02-27</td>
      <td>877015.0</td>
      <td>2016-05-19</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11</td>
      <td>11</td>
      <td>0</td>
      <td>False</td>
      <td>ENERGY STAR Heating System</td>
      <td>True</td>
      <td>Instant Hot Water, Tankless Water Heater</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2016-04-21</td>
      <td>829900.0</td>
      <td>829900.0</td>
      <td>Excl. Agency</td>
      <td>-77.072590</td>
      <td>AR9634927</td>
      <td>819900.0</td>
      <td>Fee Simple</td>
      <td>Garage, Garage Door Opener, Paved Driveway</td>
      <td>Residential</td>
      <td>Home is currently under construction. End Unit...</td>
      <td>All Days</td>
      <td>S. QUINN</td>
      <td>1319.0</td>
      <td>Craftsman</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2580</td>
      <td>NaN</td>
      <td>1</td>
      <td>Townhouse</td>
      <td>2016</td>
      <td>NaN</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>25</th>
      <td>900 TAYLOR ST #1527</td>
      <td>Master Bedroom - Full Bathroom, Attached Maste...</td>
      <td>Dishwasher, Disposal, Dryer, Dryer - Front Loa...</td>
      <td>2015.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-04-28</td>
      <td>195000.0</td>
      <td>2017-04-10</td>
      <td>ARLINGTON</td>
      <td>1311.32</td>
      <td>Annually</td>
      <td>350</td>
      <td>350</td>
      <td>0</td>
      <td>False</td>
      <td>Central</td>
      <td>False</td>
      <td>Electric</td>
      <td>95000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>38400.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-04-26</td>
      <td>240000.0</td>
      <td>240000.0</td>
      <td>Excl. Right</td>
      <td>-77.112836</td>
      <td>AR9639067</td>
      <td>270000.0</td>
      <td>Condo</td>
      <td>Parking Fee</td>
      <td>Residential</td>
      <td>Please notice this is a Retirement Community. ...</td>
      <td>NaN</td>
      <td>TAYLOR</td>
      <td>900.0</td>
      <td>Traditional</td>
      <td>14-051-227</td>
      <td>133400</td>
      <td>0</td>
      <td>0</td>
      <td>960</td>
      <td>1328.66</td>
      <td>2</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1992</td>
      <td>1890.0</td>
      <td>22203</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1715 13TH ROAD S.</td>
      <td>NaN</td>
      <td>ENERGY STAR Dishwasher, ENERGY STAR Refrigerat...</td>
      <td>NaN</td>
      <td>No</td>
      <td>5</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-03-28</td>
      <td>835970.0</td>
      <td>2016-05-25</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19</td>
      <td>19</td>
      <td>0</td>
      <td>False</td>
      <td>ENERGY STAR Heating System</td>
      <td>True</td>
      <td>Instant Hot Water, Tankless Water Heater</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2016-05-03</td>
      <td>809900.0</td>
      <td>809900.0</td>
      <td>Excl. Agency</td>
      <td>-77.073290</td>
      <td>AR9646368</td>
      <td>809900.0</td>
      <td>Fee Simple</td>
      <td>Garage, Garage Door Opener, Paved Driveway</td>
      <td>Residential</td>
      <td>Home is currently under construction. 2580 sq ...</td>
      <td>All Days</td>
      <td>13TH ROAD S.</td>
      <td>1715.0</td>
      <td>Craftsman</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2580</td>
      <td>NaN</td>
      <td>1</td>
      <td>Townhouse</td>
      <td>2016</td>
      <td>NaN</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>27</th>
      <td>4366 PERSHING DR #43662</td>
      <td>Wood Floors</td>
      <td>Dishwasher, Disposal, Microwave, Refrigerator,...</td>
      <td>2015.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-02-17</td>
      <td>260000.0</td>
      <td>2017-01-29</td>
      <td>ARLINGTON</td>
      <td>2588.24</td>
      <td>Annually</td>
      <td>263</td>
      <td>263</td>
      <td>0</td>
      <td>False</td>
      <td>Radiator</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>210900.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>52400.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-05-11</td>
      <td>274900.0</td>
      <td>274900.0</td>
      <td>Excl. Right</td>
      <td>-77.108866</td>
      <td>AR9654407</td>
      <td>315000.0</td>
      <td>Condo</td>
      <td>Permit Required, Unassigned, Surface</td>
      <td>Residential</td>
      <td>Please see documents for disclosures &amp; conveya...</td>
      <td>NaN</td>
      <td>PERSHING</td>
      <td>4366.0</td>
      <td>Colonial</td>
      <td>20-026-360</td>
      <td>263300</td>
      <td>0</td>
      <td>0</td>
      <td>936</td>
      <td>2622.47</td>
      <td>1</td>
      <td>Garden 1-4 Floors</td>
      <td>1940</td>
      <td>NaN</td>
      <td>22203</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2907 KENSINGTON ST N</td>
      <td>Attic - Finished, Closet - Master Bedroom Walk...</td>
      <td>Dishwasher, Disposal, Dryer, Exhaust Fan, Icem...</td>
      <td>NaN</td>
      <td>Yes</td>
      <td>8</td>
      <td>6</td>
      <td>2</td>
      <td>7</td>
      <td>ARLINGTON</td>
      <td>2017-03-31</td>
      <td>2186500.0</td>
      <td>2017-02-04</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>263</td>
      <td>263</td>
      <td>2</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2016-05-18</td>
      <td>2295000.0</td>
      <td>2295000.0</td>
      <td>Excl. Right</td>
      <td>-77.145620</td>
      <td>AR9661083</td>
      <td>2295000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Completed in March '17. A frame design on one ...</td>
      <td>All Days</td>
      <td>KENSINGTON</td>
      <td>2907.0</td>
      <td>A-Frame</td>
      <td>000000</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7078</td>
      <td>NaN</td>
      <td>1</td>
      <td>Detached</td>
      <td>2016</td>
      <td>NaN</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>29</th>
      <td>900 TAYLOR ST #1420</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-02-28</td>
      <td>249000.0</td>
      <td>2016-12-22</td>
      <td>ARLINGTON</td>
      <td>1586.56</td>
      <td>Annually</td>
      <td>172</td>
      <td>264</td>
      <td>0</td>
      <td>False</td>
      <td>Central</td>
      <td>False</td>
      <td>Electric</td>
      <td>122200.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>39200.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-06-02</td>
      <td>249999.0</td>
      <td>249999.0</td>
      <td>Excl. Right</td>
      <td>-77.112643</td>
      <td>AR9675673</td>
      <td>275000.0</td>
      <td>Condo</td>
      <td>Parking Fee</td>
      <td>Residential</td>
      <td>Monthly Service Fee of $3,170.00 is not option...</td>
      <td>NaN</td>
      <td>TAYLOR</td>
      <td>900.0</td>
      <td>Traditional</td>
      <td>14-051-201</td>
      <td>161400</td>
      <td>0</td>
      <td>0</td>
      <td>981</td>
      <td>1607.54</td>
      <td>1</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1992</td>
      <td>1873.0</td>
      <td>22203</td>
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
      <th>3054</th>
      <td>1311 Quinn ST S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>4</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-02-23</td>
      <td>751955.0</td>
      <td>2016-12-30</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Central</td>
      <td>True</td>
      <td>Electric</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2016-12-30</td>
      <td>751955.0</td>
      <td>751955.0</td>
      <td>Excl. Right</td>
      <td>-77.072630</td>
      <td>AR10117538</td>
      <td>751955.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Comp purposes only</td>
      <td>NaN</td>
      <td>QUINN</td>
      <td>1311.0</td>
      <td>Arts &amp; Crafts</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>Townhouse</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3055</th>
      <td>4360 LEE HWY #203</td>
      <td>Bathroom(s) - Ceramic Tile, Built-in Bookcases...</td>
      <td>Dishwasher, Disposal, Exhaust Fan, Oven / Rang...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-12-29</td>
      <td>330000.0</td>
      <td>2017-12-17</td>
      <td>ARLINGTON</td>
      <td>2677.76</td>
      <td>Annually</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>240000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>33800.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-12-14</td>
      <td>324900.0</td>
      <td>324900.0</td>
      <td>Excl. Right</td>
      <td>-77.115720</td>
      <td>AR10118991</td>
      <td>324900.0</td>
      <td>Condo</td>
      <td>Assigned</td>
      <td>Residential</td>
      <td>MULTIPLE OFFERS RECEIVED - SUNDAY OPEN HOUSE C...</td>
      <td>All Days</td>
      <td>LEE</td>
      <td>4360.0</td>
      <td>Other</td>
      <td>07-012-048</td>
      <td>273800</td>
      <td>0</td>
      <td>0</td>
      <td>938</td>
      <td>2713.34</td>
      <td>2</td>
      <td>Garden 1-4 Floors</td>
      <td>1964</td>
      <td>3231.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>3056</th>
      <td>117 FILLMORE ST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016.0</td>
      <td>No</td>
      <td>5</td>
      <td>5</td>
      <td>0</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-12-12</td>
      <td>960000.0</td>
      <td>2017-12-12</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>220</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>688700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>410800.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-12-12</td>
      <td>1000000.0</td>
      <td>1000000.0</td>
      <td>Excl. Right</td>
      <td>-77.088390</td>
      <td>AR10119050</td>
      <td>1000000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>**Sun Filled Custom Built Home**Minutes to Was...</td>
      <td>All Days</td>
      <td>FILLMORE</td>
      <td>117.0</td>
      <td>Colonial</td>
      <td>24-001-131</td>
      <td>1099500</td>
      <td>0</td>
      <td>0</td>
      <td>4326</td>
      <td>10896.02</td>
      <td>1</td>
      <td>Detached</td>
      <td>2006</td>
      <td>1838.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3057</th>
      <td>1633 BARTON ST #12</td>
      <td>Bathroom(s) - Ceramic Tile, Bedroom - Entry Le...</td>
      <td>Dishwasher, Microwave, Oven / Range - Electric...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-12-30</td>
      <td>379900.0</td>
      <td>2017-12-29</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16</td>
      <td>29</td>
      <td>1</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>True</td>
      <td>Electric</td>
      <td>362000.0</td>
      <td>Annually</td>
      <td>Other</td>
      <td>44800.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-12-14</td>
      <td>389900.0</td>
      <td>389900.0</td>
      <td>Excl. Right</td>
      <td>-77.081490</td>
      <td>AR10120026</td>
      <td>409900.0</td>
      <td>Condo</td>
      <td>Assigned</td>
      <td>Residential</td>
      <td>Contact ShowingTime at 800-746-9464. Direct al...</td>
      <td>NaN</td>
      <td>BARTON</td>
      <td>1633.0</td>
      <td>Other</td>
      <td>32-001-618</td>
      <td>406800</td>
      <td>0</td>
      <td>0</td>
      <td>1120</td>
      <td>4031.38</td>
      <td>1</td>
      <td>Garden 1-4 Floors</td>
      <td>1985</td>
      <td>4856.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3058</th>
      <td>1418 RHODES ST #B412</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-12-15</td>
      <td>950000.0</td>
      <td>2017-12-15</td>
      <td>ARLINGTON</td>
      <td>7921.80</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>716100.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>93900.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2017-12-15</td>
      <td>950000.0</td>
      <td>950000.0</td>
      <td>Excl. Right</td>
      <td>-77.079370</td>
      <td>AR10120801</td>
      <td>950000.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Bright 2 bed 2.5 bath Unit Only blocks to shop...</td>
      <td>NaN</td>
      <td>RHODES</td>
      <td>1418.0</td>
      <td>Contemporary</td>
      <td>17-023-090</td>
      <td>810000</td>
      <td>0</td>
      <td>0</td>
      <td>1878</td>
      <td>8027.10</td>
      <td>0</td>
      <td>Garden 1-4 Floors</td>
      <td>2010</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3059</th>
      <td>3600 GLEBE RD S #621W</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016.0</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-02-24</td>
      <td>473000.0</td>
      <td>2017-02-14</td>
      <td>ARLINGTON</td>
      <td>4465.55</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Central</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>389200.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>67400.0</td>
      <td>Annually</td>
      <td>0</td>
      <td>2017-02-14</td>
      <td>485000.0</td>
      <td>485000.0</td>
      <td>Excl. Right</td>
      <td>-77.051547</td>
      <td>AR10121715</td>
      <td>485000.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Comp Purposes Only.</td>
      <td>NaN</td>
      <td>GLEBE</td>
      <td>3600.0</td>
      <td>Contemporary</td>
      <td>34-027-243</td>
      <td>456600</td>
      <td>0</td>
      <td>0</td>
      <td>1123</td>
      <td>4524.88</td>
      <td>0</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>2006</td>
      <td>NaN</td>
      <td>22202</td>
    </tr>
    <tr>
      <th>3060</th>
      <td>3546 UTAH ST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016.0</td>
      <td>Yes</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>ARLINGTON</td>
      <td>2017-12-18</td>
      <td>865000.0</td>
      <td>2017-12-18</td>
      <td>ARLINGTON</td>
      <td>7236.22</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Central</td>
      <td>False</td>
      <td>Electric</td>
      <td>129900.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>610000.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2017-12-18</td>
      <td>865000.0</td>
      <td>865000.0</td>
      <td>Excl. Right</td>
      <td>-77.123850</td>
      <td>AR10122043</td>
      <td>865000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str</td>
      <td>Residential</td>
      <td>Sold to builder before going on the market. So...</td>
      <td>NaN</td>
      <td>UTAH</td>
      <td>3546.0</td>
      <td>Rambler</td>
      <td>03-036-108</td>
      <td>739900</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7332.40</td>
      <td>0</td>
      <td>Detached</td>
      <td>1953</td>
      <td>4444.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>3061</th>
      <td>3650 38TH ST N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>ARLINGTON</td>
      <td>2017-12-19</td>
      <td>862000.0</td>
      <td>2017-10-31</td>
      <td>ARLINGTON</td>
      <td>8402.76</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>237300.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>608900.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2017-10-31</td>
      <td>872000.0</td>
      <td>872000.0</td>
      <td>Excl. Right</td>
      <td>-77.118920</td>
      <td>AR10122381</td>
      <td>872000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Sold privately "as is."   Entered for comp pur...</td>
      <td>NaN</td>
      <td>38TH</td>
      <td>3650.0</td>
      <td>Split Foyer</td>
      <td>04-036-010</td>
      <td>846200</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8512.76</td>
      <td>0</td>
      <td>Detached</td>
      <td>1959</td>
      <td>4824.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>3062</th>
      <td>3450 14TH ST N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-12-12</td>
      <td>980000.0</td>
      <td>2017-11-10</td>
      <td>ARLINGTON</td>
      <td>7529.90</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>122300.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>636000.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-11-10</td>
      <td>980000.0</td>
      <td>980000.0</td>
      <td>Excl. Right</td>
      <td>-77.102840</td>
      <td>AR10122669</td>
      <td>980000.0</td>
      <td>Fee Simple</td>
      <td>Other</td>
      <td>Residential</td>
      <td>Comp purposes only. Purchased from builder pri...</td>
      <td>NaN</td>
      <td>14TH</td>
      <td>3450.0</td>
      <td>Cape Cod</td>
      <td>15-081-028</td>
      <td>758300</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7628.46</td>
      <td>0</td>
      <td>Detached</td>
      <td>1949</td>
      <td>4910.0</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>3063</th>
      <td>1307 HUDSON ST N</td>
      <td>Attached Master Bathroom, Attic - Finished, Au...</td>
      <td>Dishwasher, Disposal, Dryer - Front Loading, E...</td>
      <td>2016.0</td>
      <td>Yes</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-12-20</td>
      <td>1905000.0</td>
      <td>2017-11-21</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>27</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air, Programmable Thermostat</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>1059500.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>725000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2017-11-21</td>
      <td>1949900.0</td>
      <td>1949900.0</td>
      <td>Excl. Right</td>
      <td>-77.097540</td>
      <td>AR10123038</td>
      <td>1949900.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str, Garage, Detached, Garage Door O...</td>
      <td>Residential</td>
      <td>Contact Alt Listing Agent  Bridget Hodge @ 703...</td>
      <td>All Days</td>
      <td>HUDSON</td>
      <td>1307.0</td>
      <td>Craftsman</td>
      <td>15-073-001</td>
      <td>1784500</td>
      <td>0</td>
      <td>0</td>
      <td>4894</td>
      <td>17684.38</td>
      <td>1</td>
      <td>Detached</td>
      <td>2007</td>
      <td>5015.0</td>
      <td>22201</td>
    </tr>
    <tr>
      <th>3064</th>
      <td>2616 KENMORE CT</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>4</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-11-07</td>
      <td>755000.0</td>
      <td>2017-10-05</td>
      <td>ARLINGTON</td>
      <td>6386.96</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Central, Forced Air</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>356200.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>287000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2017-10-05</td>
      <td>755000.0</td>
      <td>755000.0</td>
      <td>Excl. Right</td>
      <td>-77.086220</td>
      <td>AR10123175</td>
      <td>755000.0</td>
      <td>Fee Simple</td>
      <td>Garage, Street</td>
      <td>Residential</td>
      <td>immaculate home in Shirlington Crest</td>
      <td>NaN</td>
      <td>KENMORE</td>
      <td>2616.0</td>
      <td>Federal</td>
      <td>31-033-205</td>
      <td>643200</td>
      <td>0</td>
      <td>0</td>
      <td>2049</td>
      <td>6470.56</td>
      <td>0</td>
      <td>Townhouse</td>
      <td>2008</td>
      <td>2365.0</td>
      <td>22206</td>
    </tr>
    <tr>
      <th>3065</th>
      <td>5212 32ND ST N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-12-21</td>
      <td>795000.0</td>
      <td>2017-12-21</td>
      <td>ARLINGTON</td>
      <td>7426.64</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>147900.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>600000.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2017-12-21</td>
      <td>795000.0</td>
      <td>795000.0</td>
      <td>Excl. Right</td>
      <td>-77.142310</td>
      <td>AR10123182</td>
      <td>795000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str</td>
      <td>Residential</td>
      <td>For comp purposes only. Off market sale. Buyer...</td>
      <td>NaN</td>
      <td>32ND</td>
      <td>5212.0</td>
      <td>Rambler</td>
      <td>02-025-011</td>
      <td>747900</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7523.86</td>
      <td>0</td>
      <td>Detached</td>
      <td>1955</td>
      <td>1503.0</td>
      <td>22207</td>
    </tr>
    <tr>
      <th>3066</th>
      <td>1338 ROLFE ST S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-08-11</td>
      <td>726275.0</td>
      <td>2017-03-09</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>0.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>60800.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-03-09</td>
      <td>726275.0</td>
      <td>726275.0</td>
      <td>Modified/Excl</td>
      <td>-77.074336</td>
      <td>AR10125276</td>
      <td>726275.0</td>
      <td>Condo</td>
      <td>Drvwy/Off Str</td>
      <td>Residential</td>
      <td>Settled on 8/11/2017</td>
      <td>All Days</td>
      <td>ROLFE</td>
      <td>1338.0</td>
      <td>Colonial</td>
      <td>33-007-074</td>
      <td>60800</td>
      <td>0</td>
      <td>0</td>
      <td>2202</td>
      <td>611.64</td>
      <td>0</td>
      <td>Townhouse</td>
      <td>2017</td>
      <td>4750.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3067</th>
      <td>1530 KEY BLVD #1216</td>
      <td>NaN</td>
      <td>Dishwasher, Disposal, Dryer, Exhaust Fan, Icem...</td>
      <td>2017.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>ARLINGTON</td>
      <td>2017-12-29</td>
      <td>650000.0</td>
      <td>2017-11-10</td>
      <td>ARLINGTON</td>
      <td>5828.90</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>False</td>
      <td>Electric</td>
      <td>546500.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>40500.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-11-10</td>
      <td>650000.0</td>
      <td>650000.0</td>
      <td>Excl. Right</td>
      <td>-77.076060</td>
      <td>AR10125734</td>
      <td>650000.0</td>
      <td>Condo</td>
      <td>Garage, Assigned, Underground</td>
      <td>Residential</td>
      <td>Stunning 12th floor condo with sweeping views ...</td>
      <td>NaN</td>
      <td>KEY</td>
      <td>1530.0</td>
      <td>Contemporary</td>
      <td>16-034-343</td>
      <td>587000</td>
      <td>0</td>
      <td>0</td>
      <td>1125</td>
      <td>5905.20</td>
      <td>0</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1986</td>
      <td>1543.0</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3068</th>
      <td>5225 11TH ST S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-12-29</td>
      <td>466625.0</td>
      <td>2017-12-29</td>
      <td>ARLINGTON</td>
      <td>4871.64</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>136500.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>354100.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2017-12-29</td>
      <td>466625.0</td>
      <td>466625.0</td>
      <td>Excl. Right</td>
      <td>-77.116090</td>
      <td>AR10125794</td>
      <td>466625.0</td>
      <td>Fee Simple</td>
      <td>None</td>
      <td>Residential</td>
      <td>.</td>
      <td>NaN</td>
      <td>11TH</td>
      <td>5225.0</td>
      <td>Colonial</td>
      <td>28-005-024</td>
      <td>490600</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4935.40</td>
      <td>0</td>
      <td>Detached</td>
      <td>1947</td>
      <td>3216.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3069</th>
      <td>1701 16th ST N #318</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-08-10</td>
      <td>1499900.0</td>
      <td>2017-03-01</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>2017-03-01</td>
      <td>1499900.0</td>
      <td>1499900.0</td>
      <td>Excl. Right</td>
      <td>-77.077760</td>
      <td>AR10125930</td>
      <td>1499900.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Entered for Comparative Purposes.  Selling Age...</td>
      <td>NaN</td>
      <td>16TH</td>
      <td>1701.0</td>
      <td>Contemporary</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1880</td>
      <td>NaN</td>
      <td>0</td>
      <td>Garden 1-4 Floors</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3070</th>
      <td>1709 13TH RD S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>No</td>
      <td>5</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-12-31</td>
      <td>854755.0</td>
      <td>2017-12-31</td>
      <td>ARLINGTON</td>
      <td>4488.36</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>182000.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>270000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2017-12-31</td>
      <td>854755.0</td>
      <td>854755.0</td>
      <td>Excl. Right</td>
      <td>-77.073142</td>
      <td>AR10126594</td>
      <td>854755.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>None</td>
      <td>NaN</td>
      <td>13TH</td>
      <td>1709.0</td>
      <td>Colonial</td>
      <td>33-007-043</td>
      <td>452000</td>
      <td>0</td>
      <td>0</td>
      <td>2496</td>
      <td>4547.12</td>
      <td>0</td>
      <td>Townhouse</td>
      <td>2016</td>
      <td>4720.0</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3071</th>
      <td>5130 16TH ST N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-12-27</td>
      <td>645000.0</td>
      <td>2017-10-13</td>
      <td>ARLINGTON</td>
      <td>7533.88</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>143400.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>615300.0</td>
      <td>Annually</td>
      <td>2</td>
      <td>2017-10-13</td>
      <td>650000.0</td>
      <td>650000.0</td>
      <td>Excl. Right</td>
      <td>-77.126380</td>
      <td>AR10126669</td>
      <td>650000.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Entered for comp purposes only.  Home needed u...</td>
      <td>NaN</td>
      <td>16TH</td>
      <td>5130.0</td>
      <td>Rambler</td>
      <td>09-031-011</td>
      <td>758700</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7632.50</td>
      <td>0</td>
      <td>Detached</td>
      <td>1952</td>
      <td>2644.0</td>
      <td>22205</td>
    </tr>
    <tr>
      <th>3072</th>
      <td>4312 2ND RD N #2</td>
      <td>Bathroom(s) - Ceramic Tile, Shades / Blinds, W...</td>
      <td>Disposal, Microwave, Oven / Range - Gas, Refri...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-12-29</td>
      <td>246100.0</td>
      <td>2017-11-21</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>98</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>180400.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>49000.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-11-21</td>
      <td>234900.0</td>
      <td>234900.0</td>
      <td>Excl. Right</td>
      <td>-77.106470</td>
      <td>AR10127109</td>
      <td>234900.0</td>
      <td>Condo</td>
      <td>Gen Comm Elem, Permit Required, Prk Space Cnvys</td>
      <td>Residential</td>
      <td>Call Alt Agent Sarah Noel with questions. SCHE...</td>
      <td>All Days</td>
      <td>2ND</td>
      <td>4312.0</td>
      <td>Colonial</td>
      <td>20-028-044</td>
      <td>229400</td>
      <td>0</td>
      <td>0</td>
      <td>875</td>
      <td>2273.34</td>
      <td>1</td>
      <td>Garden 1-4 Floors</td>
      <td>1940</td>
      <td>2970.0</td>
      <td>22203</td>
    </tr>
    <tr>
      <th>3073</th>
      <td>1336 S. Quinn ST</td>
      <td>Home Warranty, Vanities - Double, Countertop(s...</td>
      <td>ENERGY STAR Dishwasher, ENERGY STAR Refrigerat...</td>
      <td>NaN</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-11-21</td>
      <td>809990.0</td>
      <td>2017-05-17</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>ENERGY STAR Heating System</td>
      <td>True</td>
      <td>Instant Hot Water, Tankless Water Heater</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3</td>
      <td>2017-05-17</td>
      <td>719900.0</td>
      <td>719900.0</td>
      <td>Excl. Agency</td>
      <td>-77.073900</td>
      <td>AR10130028</td>
      <td>719900.0</td>
      <td>Condo</td>
      <td>Garage, Garage Door Opener, Paved Driveway</td>
      <td>Residential</td>
      <td>Arlington's fastest selling community.  Conven...</td>
      <td>All Days</td>
      <td>S. QUINN</td>
      <td>1336.0</td>
      <td>Craftsman</td>
      <td>0.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2879</td>
      <td>NaN</td>
      <td>1</td>
      <td>Townhouse</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22204</td>
    </tr>
    <tr>
      <th>3074</th>
      <td>3458 S WAKEFIELD ST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-12-18</td>
      <td>604000.0</td>
      <td>2017-11-27</td>
      <td>ARLINGTON</td>
      <td>5168.56</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>False</td>
      <td>Electric</td>
      <td>461900.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>58600.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-11-27</td>
      <td>585000.0</td>
      <td>585000.0</td>
      <td>Excl. Right</td>
      <td>-77.091601</td>
      <td>AR10132615</td>
      <td>594000.0</td>
      <td>Condo</td>
      <td>Assigned</td>
      <td>Residential</td>
      <td>For comp purposes, sold off-market.</td>
      <td>NaN</td>
      <td>S WAKEFIELD</td>
      <td>3458.0</td>
      <td>Colonial</td>
      <td>30-021-642</td>
      <td>520500</td>
      <td>0</td>
      <td>0</td>
      <td>1830</td>
      <td>5236.22</td>
      <td>1</td>
      <td>Townhouse</td>
      <td>1940</td>
      <td>1706.0</td>
      <td>22206</td>
    </tr>
    <tr>
      <th>3075</th>
      <td>1701 16th Street N #311</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-07-05</td>
      <td>1250724.0</td>
      <td>2017-02-10</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Loft</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2</td>
      <td>2017-02-10</td>
      <td>1250724.0</td>
      <td>1250724.0</td>
      <td>Excl. Right</td>
      <td>-77.077760</td>
      <td>AR10132004</td>
      <td>1250724.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>Gaslight Select.... New Construction by Abdo.....</td>
      <td>NaN</td>
      <td>16TH STREET</td>
      <td>1701.0</td>
      <td>Contemporary</td>
      <td>17-008-091</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1650</td>
      <td>NaN</td>
      <td>0</td>
      <td>Duplex</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3076</th>
      <td>1701 16th St #353</td>
      <td>Countertop(s) - Silestone, Elevator, Master Be...</td>
      <td>Dishwasher, Disposal, Dryer - Front Loading, I...</td>
      <td>NaN</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-06-28</td>
      <td>939900.0</td>
      <td>2017-01-20</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>2017-01-20</td>
      <td>939900.0</td>
      <td>939900.0</td>
      <td>Excl. Right</td>
      <td>-77.077760</td>
      <td>AR10138138</td>
      <td>939900.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>2 Bedroom Flat for comparable purposes only.</td>
      <td>NaN</td>
      <td>16TH ST</td>
      <td>1701.0</td>
      <td>Contemporary</td>
      <td>17-008-122</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1337</td>
      <td>NaN</td>
      <td>0</td>
      <td>Garden 1-4 Floors</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3077</th>
      <td>1701 16th ST #334</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-07-11</td>
      <td>1205900.0</td>
      <td>2017-01-22</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Traditional, Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2</td>
      <td>2017-01-22</td>
      <td>1205900.0</td>
      <td>1205900.0</td>
      <td>Excl. Right</td>
      <td>-77.077760</td>
      <td>AR10138178</td>
      <td>1205900.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>For Comp purposes only. 2 bedroom loft unit, n...</td>
      <td>NaN</td>
      <td>16TH</td>
      <td>1701.0</td>
      <td>Contemporary</td>
      <td>17-008-109</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1875</td>
      <td>NaN</td>
      <td>0</td>
      <td>Mid-Rise 5-8 Floors</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3078</th>
      <td>1701 16th #351</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-09-22</td>
      <td>971900.0</td>
      <td>2017-09-01</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Floor Plan-Open</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>2017-09-01</td>
      <td>971900.0</td>
      <td>971900.0</td>
      <td>Excl. Right</td>
      <td>-77.077760</td>
      <td>AR10138196</td>
      <td>971900.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>For Comp Purposes.  1st level 2 bedroom flat w...</td>
      <td>NaN</td>
      <td>16TH</td>
      <td>1701.0</td>
      <td>Contemporary</td>
      <td>17-008-120</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1337</td>
      <td>NaN</td>
      <td>0</td>
      <td>Mid-Rise 5-8 Floors</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3079</th>
      <td>1701 16th St. N ST #322</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>ARLINGTON</td>
      <td>2017-06-30</td>
      <td>849900.0</td>
      <td>2017-03-01</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Hot Water</td>
      <td>False</td>
      <td>60 or More Gallon Tank</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Loft</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2</td>
      <td>2017-03-01</td>
      <td>849900.0</td>
      <td>849900.0</td>
      <td>Excl. Right</td>
      <td>-77.077760</td>
      <td>AR10149248</td>
      <td>849900.0</td>
      <td>Condo</td>
      <td>Assigned</td>
      <td>Residential</td>
      <td>Listing for comp purposes</td>
      <td>NaN</td>
      <td>16TH ST. N</td>
      <td>1701.0</td>
      <td>Contemporary</td>
      <td>125356</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1024</td>
      <td>NaN</td>
      <td>0</td>
      <td>Attach/Row Hse</td>
      <td>2017</td>
      <td>NaN</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3080</th>
      <td>5709 11TH ST N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-09-22</td>
      <td>867604.0</td>
      <td>2017-04-14</td>
      <td>ARLINGTON</td>
      <td>3972.00</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>True</td>
      <td>Natural Gas, Tankless Water Heater</td>
      <td>0.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>400000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2017-04-14</td>
      <td>867604.0</td>
      <td>867604.0</td>
      <td>Modified/Excl</td>
      <td>-77.134070</td>
      <td>AR10150737</td>
      <td>867604.0</td>
      <td>Fee Simple</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>New Construction. Arlington Row.  For Comp Pur...</td>
      <td>NaN</td>
      <td>11TH</td>
      <td>5709.0</td>
      <td>Other</td>
      <td>09-064-022</td>
      <td>400000</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4024.00</td>
      <td>0</td>
      <td>Townhouse</td>
      <td>2017</td>
      <td>2303.0</td>
      <td>22205</td>
    </tr>
    <tr>
      <th>3081</th>
      <td>1121 ARLINGTON BLVD #505</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>ARLINGTON</td>
      <td>2017-07-24</td>
      <td>159000.0</td>
      <td>2017-06-20</td>
      <td>ARLINGTON</td>
      <td>1651.34</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Summer / Winter Changeover</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>143900.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>22400.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2017-06-20</td>
      <td>159000.0</td>
      <td>159000.0</td>
      <td>Excl. Right</td>
      <td>-77.069365</td>
      <td>AR10153179</td>
      <td>159000.0</td>
      <td>Coop</td>
      <td>On-site Prk/Rent</td>
      <td>Residential</td>
      <td>Great Rental Return</td>
      <td>NaN</td>
      <td>ARLINGTON</td>
      <td>1121.0</td>
      <td>Transitional</td>
      <td>17-039-181</td>
      <td>166300</td>
      <td>0</td>
      <td>0</td>
      <td>559</td>
      <td>1672.94</td>
      <td>0</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1955</td>
      <td>3226.0</td>
      <td>22209</td>
    </tr>
    <tr>
      <th>3082</th>
      <td>1120 KENSINGTON ST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>No</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>5</td>
      <td>ARLINGTON</td>
      <td>2017-12-12</td>
      <td>1041943.0</td>
      <td>2017-05-27</td>
      <td>ARLINGTON</td>
      <td>3972.00</td>
      <td>Annually</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>True</td>
      <td>Tankless Water Heater</td>
      <td>0.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>400000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2017-05-27</td>
      <td>949990.0</td>
      <td>949990.0</td>
      <td>Excl. Agency</td>
      <td>-77.133797</td>
      <td>AR10155430</td>
      <td>949990.0</td>
      <td>Fee Simple</td>
      <td>Basement Garage</td>
      <td>Residential</td>
      <td>New Construction</td>
      <td>NaN</td>
      <td>KENSINGTON</td>
      <td>1120.0</td>
      <td>Contemporary</td>
      <td>09-064-034</td>
      <td>400000</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4024.00</td>
      <td>0</td>
      <td>Townhouse</td>
      <td>2017</td>
      <td>3532.0</td>
      <td>22205</td>
    </tr>
    <tr>
      <th>3083</th>
      <td>1401 GLEBE RD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-03-24</td>
      <td>668000.0</td>
      <td>2017-02-24</td>
      <td>ARLINGTON</td>
      <td>6951.98</td>
      <td>Annually</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>False</td>
      <td>Hot Water, Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>148100.0</td>
      <td>Annually</td>
      <td>NaN</td>
      <td>552000.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2017-02-24</td>
      <td>656000.0</td>
      <td>656000.0</td>
      <td>Excl. Right</td>
      <td>-77.118140</td>
      <td>AR10157944</td>
      <td>656000.0</td>
      <td>Fee Simple</td>
      <td>Drvwy/Off Str</td>
      <td>Residential</td>
      <td>Entered for comps purposes</td>
      <td>NaN</td>
      <td>GLEBE</td>
      <td>1401.0</td>
      <td>Tudor</td>
      <td>07-042-005</td>
      <td>700100</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7042.98</td>
      <td>0</td>
      <td>Detached</td>
      <td>1926</td>
      <td>2119.0</td>
      <td>22207</td>
    </tr>
  </tbody>
</table>
<p>3084 rows × 55 columns</p>
</div>




```python
for ix,row in house_df.iterrows():
    house_df.at[ix,"CloseMonth"] = row['CloseDate'].split('-')[1]

#str.split('-')
```


```python

#house_df["CloseDate"]=
#house_df['CloseMonth_2'] = house_df["CloseDate"].str.split('-',expand=True)[1]
house_df.head(5)
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
      <th>FullStreetAddress</th>
      <th>Amenities</th>
      <th>Appliances</th>
      <th>AssessmentYear</th>
      <th>Attic</th>
      <th>Baths</th>
      <th>BathsFull</th>
      <th>BathsHalf</th>
      <th>Beds</th>
      <th>CityName</th>
      <th>CloseDate</th>
      <th>ClosePrice</th>
      <th>ContractDate</th>
      <th>County</th>
      <th>CountyTax</th>
      <th>CountyTaxPaymentFreq</th>
      <th>DaysOnMarket</th>
      <th>DomProperty</th>
      <th>Fireplaces</th>
      <th>Foreclosure</th>
      <th>Heating</th>
      <th>HOA</th>
      <th>HotWater</th>
      <th>ImprovementAssessmentAmount</th>
      <th>ImprovementAssessmentPaymentFreq</th>
      <th>InteriorFeatures</th>
      <th>LandAssessmentAmount</th>
      <th>LandAssessmentPaymentFreq</th>
      <th>Stories</th>
      <th>ListDate</th>
      <th>ListPrice</th>
      <th>ListingLowPrice</th>
      <th>ListingType</th>
      <th>Longitude</th>
      <th>ListingID</th>
      <th>OriginalListPrice</th>
      <th>Ownership</th>
      <th>Parking</th>
      <th>PropertyType</th>
      <th>Remarks</th>
      <th>ShowDays</th>
      <th>StreetName</th>
      <th>StreetNumber</th>
      <th>Style</th>
      <th>ListingTaxID</th>
      <th>TotalAssessment</th>
      <th>TotalOpenHouses</th>
      <th>TotalShowings</th>
      <th>LivingArea</th>
      <th>TotalTaxes</th>
      <th>TotalTours</th>
      <th>Type</th>
      <th>YearBuilt</th>
      <th>Zip4</th>
      <th>PostalCode</th>
      <th>CloseMonth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3601 5TH ST S #504</td>
      <td>NaN</td>
      <td>Dishwasher, Disposal, Refrigerator, Range Hood...</td>
      <td>2014.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-02-22</td>
      <td>185000.0</td>
      <td>2017-01-15</td>
      <td>ARLINGTON</td>
      <td>1872.62</td>
      <td>Annually</td>
      <td>688</td>
      <td>688</td>
      <td>0</td>
      <td>False</td>
      <td>Summer / Winter Changeover</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>154100.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>36400.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2015-02-27</td>
      <td>192500.0</td>
      <td>192500.0</td>
      <td>Excl. Right</td>
      <td>-77.09676</td>
      <td>AR8563022</td>
      <td>229000.0</td>
      <td>Condo</td>
      <td>Unassigned</td>
      <td>Residential</td>
      <td>This condo has been thoroughly renovated just ...</td>
      <td>NaN</td>
      <td>5TH</td>
      <td>3601.0</td>
      <td>Contemporary</td>
      <td>23-015-111</td>
      <td>190500</td>
      <td>0</td>
      <td>0</td>
      <td>1011</td>
      <td>1897.38</td>
      <td>1</td>
      <td>Mid-Rise 5-8 Floors</td>
      <td>1958</td>
      <td>1636.0</td>
      <td>22204</td>
      <td>02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1600 OAK ST #1915/1914</td>
      <td>Built-in Bookcases, Chair Railing, Crown Moldi...</td>
      <td>Cooktop, Dishwasher, Disposal, Dryer, Exhaust ...</td>
      <td>2015.0</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>ARLINGTON</td>
      <td>2017-02-21</td>
      <td>1700000.0</td>
      <td>2016-11-16</td>
      <td>ARLINGTON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>514</td>
      <td>514</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s)</td>
      <td>True</td>
      <td>Natural Gas</td>
      <td>1648000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>122000.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2015-06-22</td>
      <td>1850000.0</td>
      <td>1850000.0</td>
      <td>Excl. Right</td>
      <td>-77.07377</td>
      <td>AR8673996</td>
      <td>2800000.0</td>
      <td>Condo</td>
      <td>Garage</td>
      <td>Residential</td>
      <td>A blend of two homes-3,390 interior sqft. w/mu...</td>
      <td>All Days</td>
      <td>OAK</td>
      <td>1600.0</td>
      <td>Contemporary</td>
      <td>17-003-291</td>
      <td>1770000</td>
      <td>0</td>
      <td>0</td>
      <td>3390</td>
      <td>17629.00</td>
      <td>1</td>
      <td>Hi-Rise 9+ Floors</td>
      <td>1986</td>
      <td>2760.0</td>
      <td>22209</td>
      <td>02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1719 GREENBRIER ST</td>
      <td>Attic - Finished, Automatic Garage Door Opener...</td>
      <td>ENERGY STAR Dishwasher, ENERGY STAR Refrigerat...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>8</td>
      <td>7</td>
      <td>1</td>
      <td>7</td>
      <td>ARLINGTON</td>
      <td>2017-03-03</td>
      <td>1625000.0</td>
      <td>2017-01-08</td>
      <td>ARLINGTON</td>
      <td>7353.82</td>
      <td>Annually</td>
      <td>489</td>
      <td>489</td>
      <td>1</td>
      <td>False</td>
      <td>ENERGY STAR Heating System, Forced Air, Heat P...</td>
      <td>False</td>
      <td>Natural Gas, 60 or More Gallon Tank</td>
      <td>173100.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>575000.0</td>
      <td>Annually</td>
      <td>4</td>
      <td>2015-09-08</td>
      <td>1695000.0</td>
      <td>1695000.0</td>
      <td>Excl. Right</td>
      <td>-77.13037</td>
      <td>AR8742330</td>
      <td>1751000.0</td>
      <td>Fee Simple</td>
      <td>Garage, Basement Garage, Drvwy/Off Str, Paved ...</td>
      <td>Residential</td>
      <td>New Custom Arts and Crafts home by Calvert Hom...</td>
      <td>NaN</td>
      <td>GREENBRIER</td>
      <td>1719.0</td>
      <td>Arts &amp; Crafts</td>
      <td>09-016-016</td>
      <td>748100</td>
      <td>0</td>
      <td>0</td>
      <td>5994</td>
      <td>7451.08</td>
      <td>1</td>
      <td>Detached</td>
      <td>2016</td>
      <td>3629.0</td>
      <td>22205</td>
      <td>03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3723 FOUR MILE RUN DR</td>
      <td>NaN</td>
      <td>Dishwasher, Disposal, Oven / Range - Gas, Refr...</td>
      <td>2015.0</td>
      <td>Yes</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-01-17</td>
      <td>430000.0</td>
      <td>2016-12-03</td>
      <td>ARLINGTON</td>
      <td>3361.86</td>
      <td>Annually</td>
      <td>121</td>
      <td>121</td>
      <td>0</td>
      <td>False</td>
      <td>Forced Air</td>
      <td>False</td>
      <td>Natural Gas</td>
      <td>152000.0</td>
      <td>Annually</td>
      <td>Floor Plan-Open</td>
      <td>190000.0</td>
      <td>Annually</td>
      <td>3</td>
      <td>2015-09-20</td>
      <td>475000.0</td>
      <td>475000.0</td>
      <td>Excl. Right</td>
      <td>-77.09023</td>
      <td>AR8747453</td>
      <td>450000.0</td>
      <td>Fee Simple</td>
      <td>Street</td>
      <td>Residential</td>
      <td>Perfect location!  This is your client's oppor...</td>
      <td>All Days</td>
      <td>FOUR MILE RUN</td>
      <td>3723.0</td>
      <td>Federal</td>
      <td>31-030-066</td>
      <td>342000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3406.32</td>
      <td>1</td>
      <td>Semi-Detached</td>
      <td>1945</td>
      <td>2332.0</td>
      <td>22206</td>
      <td>01</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2005 KEY BLVD #11579</td>
      <td>Bathroom(s) - Ceramic Tile, Countertop(s) - Gr...</td>
      <td>Dishwasher, Disposal, Exhaust Fan, Microwave, ...</td>
      <td>2016.0</td>
      <td>No</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>ARLINGTON</td>
      <td>2017-04-07</td>
      <td>362000.0</td>
      <td>2017-03-06</td>
      <td>ARLINGTON</td>
      <td>3386.81</td>
      <td>Annually</td>
      <td>81</td>
      <td>81</td>
      <td>0</td>
      <td>False</td>
      <td>Heat Pump(s), Forced Air</td>
      <td>True</td>
      <td>Electric</td>
      <td>309700.0</td>
      <td>Annually</td>
      <td>Floor Plan-Traditional</td>
      <td>36600.0</td>
      <td>Annually</td>
      <td>1</td>
      <td>2016-12-10</td>
      <td>365000.0</td>
      <td>365000.0</td>
      <td>Excl. Right</td>
      <td>-77.08380</td>
      <td>AR9823220</td>
      <td>369000.0</td>
      <td>Condo</td>
      <td>Street</td>
      <td>Residential</td>
      <td>Fully updated 2BR/1BA corner unit in Colonial ...</td>
      <td>NaN</td>
      <td>KEY</td>
      <td>2005.0</td>
      <td>Rambler</td>
      <td>16-026-213</td>
      <td>346300</td>
      <td>0</td>
      <td>0</td>
      <td>852</td>
      <td>3431.80</td>
      <td>0</td>
      <td>Garden 1-4 Floors</td>
      <td>1940</td>
      <td>NaN</td>
      <td>22201</td>
      <td>04</td>
    </tr>
  </tbody>
</table>
</div>




```python
mean=house_df.groupby("CloseMonth").mean()
mean_org=mean[["ClosePrice"]]
#mean_org=mean["ClosePrice"]=mean_org=mean["ClosePrice"].map("${:,.2f}".format)
mean_org.head()    
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
      <th>ClosePrice</th>
    </tr>
    <tr>
      <th>CloseMonth</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>01</th>
      <td>621377.368750</td>
    </tr>
    <tr>
      <th>02</th>
      <td>659519.503030</td>
    </tr>
    <tr>
      <th>03</th>
      <td>640787.904000</td>
    </tr>
    <tr>
      <th>04</th>
      <td>682190.573705</td>
    </tr>
    <tr>
      <th>05</th>
      <td>696128.954605</td>
    </tr>
  </tbody>
</table>
</div>




```python
median_df=house_df.groupby("CloseMonth").median()
median_df=median_df[["ClosePrice"]]
mean_org.head()  
median_df["ClosePrice"]
```




    CloseMonth
    01    552450.0
    02    542000.0
    03    517500.0
    04    625000.0
    05    620000.0
    06    630950.0
    07    585000.0
    08    545000.0
    09    523300.0
    10    599900.0
    11    582000.0
    12    575000.0
    Name: ClosePrice, dtype: float64




```python
#mod = house_df.groupby("CloseMonth").ClosePrice.apply(lambda x: x.mode())
#mod
```


```python
plt.clf()
```


    <matplotlib.figure.Figure at 0x1f0b7d90c88>



```python
mode=house_df.groupby("CloseMonth").agg({'ClosePrice': lambda x:stats.mode(x)[0]})

```


```python

mean_gr,=plt.plot(mean_org,color="red", label="Mean Price")
median_line,=plt.plot(median_df,color="green", label="Median Price")
mode_line,=plt.plot(mode,color="blue", label="Mode Price")
plt.legend(loc="best")
labels=("January","February","March","April","May","June","July","August","September","October","November","December")
loc = range(0,len(mean_org))
plt.xticks(loc,labels, rotation='vertical')
plt.title("Arlington: Properties sold in 2017 \n  Mean,Median and Mode Price")
plt.xlabel("Months")
plt.ylabel("Property Price($)")
plt.show()
plt.savefig('real_estate.png')

```


![png](output_10_0.png)



    <matplotlib.figure.Figure at 0x1f0b7d93a58>

