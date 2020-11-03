
# CHARLS Urbanicity Scale

## Authors
* **Shozen Dan**: Keio University Environmental and Information Studies, University of California Davis Statistics, Stanford Center for Asian Research and Education
* **Nicholas Ortega**: University of California Los Angeles Statistics, Stanford Center for Asian Research and Education

## Introduction
In this document we record our attempt to implement an urbanicity scale for the [China Health and Retirement Longitudinal Survey](http://charls.pku.edu.cn). Our work is mostly based off of the [urbanicity scale](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3869031/) construction done for the [China Health and Nutrition Survey](https://www.cpc.unc.edu/projects/china). 

We hope that our work will be of use to other researchers using CHALRS to conduct research on the Aging population in China. If you have any questions please feel free to contact us: [Shozen Dan](shozendn@stanford.edu), [Nicholas Ortega](nmo97@stanford.edu).

## Documentation Guidelines
In this section we outline the principles to follow when documenting the implementation of the scale. (*This section will be removed once all implementations are completed*)

1. A list of the names and description of all the variables used for construction. Variable names need to be highlighted `ja001`.
2. All equations must be written in LaTex format. Currently GitHub markdown doesn't render LaTeX -> Use [this website](https://www.codecogs.com/latex/eqneditor.php) to create gifs of equations and insert the links to the images as a work-around.
3. All cut off points need to be justified.
4. A histogram of each implemented criterion must be provided. 
5. All sources must be cited. 
6. A discription of the limitations should be included when possible.

## Table of Contents
1. Population Density
2. Economic
3. Markets
4. Supermarket and Food Vendors
5. Education
6. Diversity
7. Health
8. Transportation
9. Housing
10. Sanitation
11. Communication
12. Social Services

## 1. Population Density

### Variables
* `jc001`: Population in the village/community at the end of 2010
* `jc003`: Indicator of whether the area is recorded under `jc003_1` or `jc003_2` 
* `ja003_1`: Area of the village/community in <a href="https://www.codecogs.com/eqnedit.php?latex=km^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?km^2" title="km^2" /></a>
* `ja003_2`: Area of the village/community in <a href="https://www.codecogs.com/eqnedit.php?latex=mu=1500km^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?mu=1500km^2" title="mu=1500km^2" /></a>
### Equation and Cutoff points
The measurements in $mu$ were converted to <a href="https://www.codecogs.com/eqnedit.php?latex=km^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?km^2" title="km^2" /></a> and the population density was computed using the following equation.

<a href="https://www.codecogs.com/eqnedit.php?latex=PopulationDensity=Population/Area" target="_blank"><img src="https://latex.codecogs.com/gif.latex?PopulationDensity=Population/Area" title="PopulationDensity=Population/Area" /></a>

The cutoff points are adopted from the CHNS Urbanicity Index. 
<table style="text-align:center">
  <tr>
    <th>Points</th>
    <th>Log Poulation Range</th>
    <th>Population Range</th>
  </tr>
  <tr>
    <td>0</td>
    <td>0 ~ 0.58</td>
    <td>0 ~ 1</td>
  </tr>
  <tr>
    <td>0.5</td>
    <td>0.58 ~ 1.16</td>
    <td>1 ~ 3</td>
  </tr>
  <tr>
    <td>1</td>
    <td>1.16 ~ 1.74</td>
    <td>3 ~ 5</td>
  </tr>
  <tr>
    <td>1.5</td>
    <td>1.74 ~ 2.32</td>
    <td>5 ~ 10</td>
  </tr>
  <tr>
    <td>2</td>
    <td>2.32 ~ 2.9</td>
    <td>10 ~ 18</td>
  </tr>
  <tr>
    <td>2.5</td>
    <td>2.9 ~ 3.48</td>
    <td>18 ~ 32</td>
  </tr>
  <tr>
    <td>3</td>
    <td>3.48 ~ 4.06</td>
    <td>32 ~ 57</td>
  </tr>
  <tr>
    <td>3.5</td>
    <td>4.06 ~ 4.64</td>
    <td>57 ~ 103</td>
  </tr>
  <tr>
    <td>4</td>
    <td>4.64 ~ 5.22</td>
    <td>103 ~ 184</td>
  </tr>
  <tr>
    <td>4.5</td>
    <td>5.22 ~ 5.8</td>
    <td>184 ~ 330</td>
  </tr>
  <tr>
    <td>5</td>
    <td>5.8 ~ 6.38</td>
    <td>330 ~ 589</td>
  </tr>
  <tr>
    <td>5.5</td>
    <td>6.38 ~ 6.96</td>
    <td>589 ~ 1053</td>
  </tr>
  <tr>
    <td>6</td>
    <td>6.96 ~ 7.54</td>
    <td>1053 ~ 1881</td>
  </tr>
  <tr>
    <td>6.5</td>
    <td>7.54 ~ 8.12</td>
    <td>1881 ~ 3361</td>
  </tr>
  <tr>
    <td>7</td>
    <td>8.12 ~ 8.7</td>
    <td>3361 ~ 6002</td>
  </tr>
  <tr>
    <td>7.5</td>
    <td>8.7 ~ 9.28</td>
    <td>6002 ~ 10721</td>
  </tr>
  <tr>
    <td>8</td>
    <td>9.28 ~ 9.86</td>
    <td>10721 ~ 19148</td>
  </tr>
  <tr>
    <td>8.5</td>
    <td>9.86 ~ 10.44</td>
    <td>19148 ~ 34200</td>
  </tr>
  <tr>
    <td>9</td>
    <td>10.44 ~ 11.02</td>
    <td>34200 ~ 61083</td>
  </tr>
  <tr>
    <td>9.5</td>
    <td>11.02 ~ 11.6</td>
    <td>61083 ~ 109097</td>
  </tr>
  <tr>
    <td>10</td>
    <td>11.6 ~ 12.18</td>
    <td>109097 ~ 194852</td>
  </tr>
</table>

### Imputation
For villages/communites where population density information cannot be computed, the data was imputed using the average county population density. There were a total of 27(5%) entries that were imputed. 

### Distribution
![Population Density Score Distribution](urban-scale-figures/population-density-score-dist.png)
The plot shows the distribution of the population density score disaggregated by the urban/rural distinction variable within CHARLS. Generally, urban areas have a higher population density score compared to rural areas. However, there are a few exceptions that might be due to errors in the implementation process. 

### Limitations
The cutoff points are adopted from the CHNS Urbanicity Index which uses a different sample from CHARLS. It might be a better approach to define the cutoff points using the data from CHARLS. 

## 2. Economic

### Variables
* `fa001`: Did you engage in agricultural work (including farming, forestry, fishing, and husbandry for your own family or others) for more than 10 days in the past year?
* `PCE1`: Per Capita Expenditure (Non-Durable + Service Flow)

### Construction
<ol>
  <li>The proportion of people who engaged in agricultural work was calculated.
  <li>The community PCE by taking the average of individual level PCE for each community.
  <li>
    <ul>
      <li>If *CommunityPCE* < *median(CommunityPCE)* than: <img src="https://latex.codecogs.com/gif.latex?\inline&space;EconScore&space;=&space;100(1&space;-&space;PropAgriculture)/20" title="EconScore = 100(1 - PropAgriculture)/20" />
      <li>If *CommunityPCE* >= *median(CommunityPCE)* than: <img src="https://latex.codecogs.com/gif.latex?\inline&space;EconScore&space;=&space;200(1&space;-&space;PropAgriculture)/20" title="EconScore = 200(1 - PropAgriculture)/20" /></li>
    </ul>
  </li>
</ol>

### Imputation
For villages/communites where economic score cannot be computed, the data was imputed using the average county economic score. A total of 2(0.4%) of the entries were imputed.

### Distribution
![Economic Score Distribution](urban-scale-figures/economic-score-dist.png)
The plot shows the distribution of the economic score disaggregated by the urban/rural distinction variable within CHARLS. Generally, this criterion is able to separate urban and rural areas well. 

### Limitations
Although the implementation is able to separate the distribution of urban and rural areas, we can see that the distribution for urban communities has a long left tail. Also, we can see that it is cut off at 10. Ideally we want to evenly distribute the data. 

## 3. Markets
### Variables
* `jb028_1_11_` ~ `jb028_1_13_`: How many convenience stores/farmers' markets/super markets are in your village/community?
* `jb028_2_11_` ~ `jb028_2_13_`: What is the distance from the village/community office to the most commonly used convenience store/farmers' market/super market(0 if facility is located in the village/community)
### Construction
### Distribution
### Limitation

## 4. Education
### Variables
* `jc020` ~ `jc024`: The percentage of adult population in the community that is illiterate/semi-literate. The percentage of adult population in the community that completed primary/middle/senior high/college/graduate school.

* `bd001`: The highest level of education attained (Individual).

### Construction
1. Calculate the average community education level using the formula: <img src="https://latex.codecogs.com/gif.latex?AvgCommunityEdu_1&space;=&space;(0*%Illiterate&space;&plus;&space;1*%Primary&plus;2*%Middle&plus;3*%High&plus;5*%College&plus;6*%Graduate)/100" title="AvgCommunityEdu = (0*%Illiterate + 1*%Primary+2*%Middle+3*%High+5*%College+6*%Graduate)/100" />

2. Obtain *EducationScore1* by scaling *AvgCommunityEdu1* by 10/5 such that it is from 0 ~ 10: <img src="https://latex.codecogs.com/gif.latex?EducationScore_1&space;=&space;\frac{10*AvgCommunityEdu}{5}" title="EducationScore_1 = \frac{10*AvgCommunityEdu}{5}" />

3. Calculate the average community education level by aggregating the individual level data within each community. The CHARLS data was grouped and scored in the following way to match the scoring scheme in the CHNS Urbanicity Scale. <img src="https://latex.codecogs.com/gif.latex?AvgCommunityEdu_2&space;=&space;\frac{\sum&space;Scoring*%Grouping}{100}" title="AvgCommunityEdu_2 = \frac{\sum Scoring*%Grouping}{100}" />
<table>
  <tr>
    <th>Grouping</th>
    <th>Scoring</th>
  </tr>
  <tr>
    <td>
      <table>
    <tr>
      <th>Variable BD001</th>
      <th>Grouping</th>
    </tr>
    <tr>
      <td>No Formal Education (bd001 = 1)</td>
      <td>None</td>
    </tr>
    <tr>
      <td>Did not finish primary school by capable of reading and/or writing (bd001 = 2)</td>
      <td>None</td>
    </tr>
    <tr>
      <td>Shishu/home school (bd001 = 3)</td>
      <td>None</td>
    </tr>
    <tr>
      <td>Elementary School (bd001 = 4)</td>
      <td>Primary School</td>
    </tr>
    <tr>
      <td>Middle School (bd001 = 5)</td>
      <td>Middle School</td>
    </tr>
    <tr>
      <td>High School (bd001 = 6)</td>
      <td>High School</td>
    </tr>
    <tr>
      <td>Vocational School (bd001 = 7)</td>
      <td>Technical or Vocational</td>
    </tr>
    <tr>
      <td>Two/Three Year College/Associate Degree (bd001 = 8)</td>
      <td>College Degree</td>
    </tr>
    <tr>
      <td>Four-Year College/Bachelor's Degree (bd001 = 9)</td>
      <td>College Degree</td>
    </tr>
    <tr>
      <td>Master's Degree (bd001 = 10)</td>
      <td>Master's Degree or Higher</td>
    </tr>
    <tr>
      <td>Doctoral Degree/Ph.D. (bd001 = 11)</td>
      <td>Master's Degree or Higher</td>
    </tr>
  </table>
    </td>
    <td>
      <table>
        <tr>
          <th>Grouping</th>
          <th>Scoring</th>
        </tr>
        <tr>
          <td>None</td>
          <td>0</td>
        </tr>
        <tr>
          <td>Primary School</td>
          <td>1</td>
        </tr>
        <tr>
          <td>Middle School</td>
          <td>2</td>
        </tr>
        <tr>
          <td>High School</td>
          <td>3</td>
        </tr>
        <tr>
          <td>Technical or Vocational</td>
          <td>4</td>
        </tr>
        <tr>
          <td>College Degree</td>
          <td>5</td>
        </tr>
        <tr>
          <td>Master's Degree or Higher</td>
          <td>6</td>
        </tr>
      </table>
    </td>
  </tr>
</table>

4. Obtain *EducationScore2* by scaling *AvgCommunityEdu2* using the formula below. The reason we this way is because we want the score to be distributed between 0 ~ 10. <img src="https://latex.codecogs.com/gif.latex?EducationScore_2&space;=&space;\frac{10(1.25AvgCommunityEdu_2)}{5}" title="EducationScore_2 = \frac{10(1.25AvgCommunityEdu_2)}{5}" />

5. Obtain the final score by taking the average of *EducationScore1* and *EducationScore2*: <img src="https://latex.codecogs.com/gif.latex?EducationScore_{final}&space;=&space;\frac{EducationScore_1&space;&plus;&space;EducationScore_2}{2}" title="EducationScore_{final} = \frac{EducationScore_1 + EducationScore_2}{2}" />

### Imputation
Missing values for *EducationScore1* was imputed with the average county score or the average province score (if county score was not available). A total of 67(14.7%) entries were imputed. Data for XinJiang could not be computed therefore the score for communities within that province is the value of *EducationScore2*.

### Distribution
![Education Score Distribution](urban-scale-figures/education-score-dist.png)

### Limitations

## 5. Diversity
### Variables
* `jc020` ~ `jc024`: The percentage of adult population in the community that is illiterate/semi-literate. The percentage of adult population in the community that completed primary/middle/senior high/college/graduate school.
* `INCOME_PC`: Household per capita income.

### Construction
1. The educational variance was calculated for each community and points were given based on the scoring table below, which was adapted from the CHNS urbanicity scale. 
  
2. The income variance for each community was calculated by aggregating the individual per capita income for each community. The numbers were than divided by 1000 in order to make them more managable. The points were given based on the scoring table below, which was adapted from the CHNS urbanicity scale. 

3. The total score was comupted by taking the average of the Education Diversity and Income Diversity scores. If one of them was NA, then the other one was used. 

<table>
  <tr>
    <th>Education Variance Scoring Table</th>
    <th>Income Variance Scoring Table</th>
  </tr>
  <tr>
    <td>
      <table style="text-align:center">
        <tr>
          <th>Points</th>
          <th>Education Variance</th>
        </tr>
        <tr>
          <td>0</td>
          <td>0 ~ 0.50</td>
        </tr>
        <tr>
          <td>1</td>
          <td>0.50 ~ 0.75</td>
        </tr>
        <tr>
          <td>2</td>
          <td>0.75 ~ 1.0</td>
        </tr>
        <tr>
          <td>3</td>
          <td>1.0 ~ 1.25</td>
        </tr>
        <tr>
          <td>4</td>
          <td>1.25 ~ 1.5</td>
        </tr>
        <tr>
          <td>4.5</td>
          <td>1.5 ~ 1.75</td>
        </tr>
        <tr>
          <td>5</td>
          <td>1.75 ~ 2.0</td>
        </tr>
        <tr>
          <td>6</td>
          <td>2 ~ 2.25</td>
        </tr>
        <tr>
          <td>7</td>
          <td>2.25 ~ 2.50</td>
        </tr>
        <tr>
          <td>8</td>
          <td>2.50 ~ 2.75</td>
        </tr>
        <tr>
          <td>9</td>
          <td>2.75 ~ 3.00</td>
        </tr>
        <tr>
          <td>10</td>
          <td>3.00 ~ </td>
        </tr>
      </table>
    </td>
    <td>
      <table>
        <tr>
          <th>Points</th>
          <th>Income Variance</th>
        </tr>
        <tr>
          <td>1</td>
          <td>0 ~ 20</td>
        </tr>
        <tr>
          <td>2</td>
          <td>20 ~ 90</td>
        </tr>
        <tr>
          <td>3</td>
          <td>90 ~ 400</td>
        </tr>
        <tr>
          <td>4</td>
          <td>400 ~ 1800</td>
        </tr>
        <tr>
          <td>5</td>
          <td>1800 ~ 8100</td>
        </tr>
        <tr>
          <td>6</td>
          <td>8100 ~ 36300</td>
        </tr>
        <tr>
          <td>7</td>
          <td>36300 ~ 162750</td>
        </tr>
        <tr>
          <td>8</td>
          <td>162750 ~ 729400</td>
        </tr>
        <tr>
          <td>9</td>
          <td>729400 ~ 3269000</td>
        </tr>
        <tr>
          <td>10</td>
          <td>3269000 ~ </td>
        </tr>
      </table>
    </td>
  </tr>
</table>

### Imputation
For villages/communites where the Education Diversity score cannot be computed, the data was imputed using the average county Education Diversity score. A total of 61(15%) of the entries were imputed.

### Distribution
![Diversity Score Distribution](urban-scale-figures/diversity-score-dist.png)

### Limitations
* There were a considerable amount of imputations done for the Education Variance Score which may make it unreliable. 

* The CHNS Urbanicity Scale uses individual per capita income to calculate the Income Variance score. The Per Capita Expenditure(PCE) in CHARLS is considered a better measure for economic status. Thus, we should consider using it instead of per capita income.   

## 6. Health Infrastructure

### Variables

* `jf002_1_ ~ jf002_8_`: Whether a community/village has a specific type of medical facility
* `jf002_1_1_ ~ jf002_1_8_`: How many of that type of medical facility are located in the village
* `jf006_1_ ~ jf006_8_`: Distance to the medical facility from the village in km if not located within it

### Construction

<ol>
  <li>The presence of village clinics, township clinics, community health centers, hospitals, and pharmacies was determined using the above variables.
  <li>The health score was calculated with the following formula, where all variables are binary variables indicating the availability of that medical facility: <img src="https://latex.codecogs.com/gif.latex?HelathScore_{1}=1*VillageClinic&plus;2*TownshipClinic&plus;3*HealthCenter&plus;4*Hospital&plus;Pharmacy" title="HelathScore_{1}=1*VillageClinic+2*TownshipClinic+3*HealthCenter+4*Hospital+Pharmacy" />
  <li>Restricting the above score to be no greater than 8, the final score was calculated one of two ways
    <ul>
      <li>If there are multiple health faciltiies present in a community then: <img src="https://latex.codecogs.com/gif.latex?HealthScore_{Final}&space;=&space;1.25*HealthScore_{1}" title="HealthScore_{Final} = 1.25*HealthScore_{1}" />
      <li>If there are no facilities in a community or they are all greater than 12km away then: <img src="https://latex.codecogs.com/gif.latex?HealthScore_{Final}&space;=&space;0.5*HealthScore_{1}" title="HealthScore_{Final} = 0.5*HealthScore_{1}" />
    </ul>   
  </li>
</ol>

### Imputation

### Distribution
![Diversity Score Distribution](urban-scale-figures/health-infrastructure-graph.png)

### Limitations
* Some of the health facility types present in the CHNS dataset are not present in the CHARLS dataset, and vice versa.

## 7. Transportation

### Variables

* `jb001`: Main road type present in the village
* `jb003`: How many bus lines are accessible in this village
* `jb004`: How far away the nearest bus stop is from the village in km
* `jb005`: How far away the nearest train station is from the village in km


### Construction

<ol>
  <li>The primary road type, the distance to the nearest bus stop, and the distance to the nearest train station were determined.
    <ul>
      <li>Road = 0 is the main road type is dirt, Road= 1 if the main road type is stone/gravel/mixed, Road = 2 if the main road type is paved
      <li>Bus = 0 if there is no close bus stop, Bus = 1 if the bus stop is close to but not in the community, Bus = 2 if the bus stop is in the community
      <li>Train = 0 if there is no close train station, Train = 1 if the train station is close to but not in the community, Train = 2 if the train station is in the community  
    </ul>  
  <li>The final score was calculated with the following: <img src="https://latex.codecogs.com/gif.latex?TransportationScore=1.6666*(Road&plus;Bus&plus;Train)" title="TransportationScore=1.6666*(Road+Bus+Train)" />
  </li>
</ol>


### Imputation

### Distribution
![Diversity Score Distribution](urban-scale-figures/transportation-score-graph.png)

### Limitations

## 8. Housing

### Variables

* `jb020`: Number of days electricity is supplied in the village throughout the year
* `jb021`: Average daily electrical supply throughout the year
* `jb006_1 ~ jb006_8`: Main water source in village
* `i012_3`: Number of bathrooms in household
* `i013`: Distance to the nearest toilet
* `i015`: Whether toilet is flushable
* `jb013`: Main toilet type in village


### Construction

<ol>
  <li>Electricity timing was calculated with: <img src="https://latex.codecogs.com/gif.latex?ElectricityTiming=Hours_{Electricity}PerDay/24&space;&plus;&space;Days_{Electricity}PerYear/366" title="ElectricityTiming=Hours_{Electricity}PerDay/24 + Days_{Electricity}PerYear/366" />
  <li>In house tapwater score was calculated with: <img src="https://latex.codecogs.com/gif.latex?TapWaterScore=(TapWater/AllWater)*10" title="TapWaterScore=(TapWater/AllWater)*10" />
  <li>Toilet score was calculated with: <img src="https://latex.codecogs.com/gif.latex?FlushToiletScore=(IndoorFlush/AllToilets)*10" title="FlushToiletScore=(IndoorFlush/AllToilets)*10" />
  <li>Gas score was calculated with: <img src="https://latex.codecogs.com/gif.latex?GasScore=(NaturalGas/AllCookingFuel)" title="GasScore=(NaturalGas/AllCookingFuel)" />
  <li>The housing score was calculated by taking the mean of the above scores:<img src="https://latex.codecogs.com/gif.latex?HousingScore=(ElectricityTiming&plus;TapWaterScore&plus;FlushToiletScore&plus;GasScore)/4" title="HousingScore=(ElectricityTiming+TapWaterScore+FlushToiletScore+GasScore)/4" />
  </li>
</ol>


### Imputation

### Distribution
![Diversity Score Distribution](urban-scale-figures/housing-score-graph.png)

### Limitations

## 9. Sanitation

### Variables

* `i012_3`: Number of bathrooms in household
* `i013`: Distance to the nearest toilet
* `i015`: Whether toilet is flushable
* `jb013`: Main toilet type in village


### Construction

<ol>
  <li>The proportion of households with indoor flush toilets was calculated and multipied by 10: <img src="https://latex.codecogs.com/gif.latex?IndoorFlushScore&space;=&space;(IndoorFlush/AllToilets)*10" title="IndoorFlushScore = (IndoorFlush/AllToilets)*10" />
  <li>The proportion of households without excreta present outside was calculated and multiplied by 10: <img src="https://latex.codecogs.com/gif.latex?ExcretaAbsentOutside&space;=&space;[(IndoorFlush&plus;IndoorNoFlush)/AllToilets]&space;*&space;10" title="ExcretaAbsentOutside = [(IndoorFlush+IndoorNoFlush)/AllToilets] * 10" />
  <li>The final score was calculated by taking the average of the two scores above: <img src="https://latex.codecogs.com/gif.latex?SanitationScore&space;=&space;(IndoorFlushScore&plus;ExcretaAbsentOutside)/2" title="SanitationScore = (IndoorFlushScore+ExcretaAbsentOutside)/2" />
  </li>
</ol>

### Imputation

### Distribution
![Diversity Score Distribution](urban-scale-figures/sanitation-score-graph.png)

### Limitations
* CHARLS dataset does not contain a variable indicating whether a village has treated water
## 10. Communications

### Variables

* `jb028_1_9_`: Number of cinemas in village
* `jb028_1_5_`: Number of post offices in village
* `jb023`: Percentage of households with telephones
* `jb024`: Percentage of households with at least one cell phone 
* `jb025`: Percentage of households with a television
* `jb026`: Percentage of households with a refrigerator

### Construction

<ol>
  <li>The proportion of households with television, a refrigerator, and at least one cell phone were extracted from the variables given above.
  <li>The communication score was first calculated by dividing each proportion by 10 and taking their mean: <img src="https://latex.codecogs.com/gif.latex?CommunicationScore_{1}=(TelevisionProp/10&plus;CellPhoneProp/10&plus;RefrigeratorProp/10)/3" title="CommunicationScore_{1}=(TelevisionProp/10+CellPhoneProp/10+RefrigeratorProp/10)/3" />
  <li>This score was then divided by 10/6: <img src="https://latex.codecogs.com/gif.latex?CommunicationScore_{2}=CommunicationScore_{1}/(10/6)" title="CommunicationScore_{2}=CommunicationScore_{1}/(10/6)" />
  <li>The final score was then calculated with the addition of binary variables indicating the availability of cinema, news, post office, and telephone service: <img src="https://latex.codecogs.com/gif.latex?CommunicationScore_{Final}=CommunicationScore_{2}&plus;Cinema&plus;News&plus;PostOffice&plus;Telephone" title="CommunicationScore_{Final}=CommunicationScore_{2}+Cinema+News+PostOffice+Telephone" />
  </li>
</ol>

### Imputation

### Distribution
![Diversity Score Distribution](urban-scale-figures/communication-score-graph.png)

### Limitations
* The CHARLS dataset does not contain variables indicating the percent of households with computer, availability of newspaper, and availability of telephone service.

## 11. Social Services

### Variables

* `jb028_1_1_`: Number of kindergartens in community
* `jf010s1`: Urban insurance is offered in this community
* `jf010s2`: Rural insurance is offered in this community
* `jb028_2_1_`: Distance to nearest kindergarten


### Construction

<ol>
  <li>The availability of kindergartens, the distance to the nearest kindergarten, and the availability of urban and rural insurance were determined.
  <li>The social service score was first calculated with the following formula, where all variables are binary variables indicating the availability of that service: <img src="https://latex.codecogs.com/gif.latex?SocialScore_{1}=3.3*Kinder&plus;3.3*UrbanInsurance&plus;3.3*RuralInsurance" title="SocialScore_{1}=3.3*Kinder+3.3*UrbanInsurance+3.3*RuralInsurance" />
  <li>The final score was then calculated by adding 1.65 if the nearest kindergarten was not in the community but still less than 25 km away: <img src="https://latex.codecogs.com/gif.latex?SocialScore_{Final}=SocialScore_{1}&plus;1.65*OutsideKinder" title="SocialScore_{Final}=SocialScore_{1}+1.65*OutsideKinder" />
  </li>
</ol>


### Imputation

### Distribution
![Diversity Score Distribution](urban-scale-figures/social-services-graph.png)

### Limitations
* The CHARLS dataset does not contain a variable indicating the availability of care for children under 3

