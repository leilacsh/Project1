### Background
According to the [Meteorological Services Singapore](http://www.weather.gov.sg/climate-climate-of-singapore/#:~:text=Singapore%20is%20situated%20near%20the,month%2Dto%2Dmonth%20variation.), Singapore has typical tropical climate with adundant rainfall, high and uniform temperatures and high humidity all year round, since its situated near the equator. There are many factors that help us understand the climate of a country and in this project we are going to look into a few, especially rainfall.

Singapore’s climate is characterised by two main monsoon seasons separated by inter-monsoonal periods.  The **Northeast Monsoon** occurs from December to early March, and the **Southwest Monsoon** from June to September.

The major weather systems affecting Singapore that can lead to heavy rainfall are:
- Monsoon surges, or strong wind episodes in the Northeast Monsoon flow bringing about major rainfall events;
- Sumatra squalls, an organised line of thunderstorms travelling eastward across Singapore, having developed over the island of Sumatra or Straits of Malacca west of us;
- Afternoon and evening thunderstorms caused by strong surface heating and by the sea breeze circulation that develops in the afternoon.

Singapore’s climate station has been located at several different sites in the past 140 years. The station had been decommissioned at various points in the past due to changes to local land use in the site’s vicinity, and had to be relocated. Since 1984, the climate station has been located at **Changi**.

There are other metrics of climate such as temperature, humidity, sun shine duration, wind speed, cloud cover etc. All the dataset used in the project comes from [data.gov.sg](data.gov.sg), as recorded at the Changi climate station 

### Introduction
<font size=3>Daily weather are important in influencing consumer purchasing behavior. Rose and Dolega study indicates that with rising temperature, retail sales tend to increase in each of the four seasons: spring, summer, autumn and winter. This is supported by Tony articles, which states that warm temperature tends to increase consumer moods and lead to higher consumer spending, while cold and rainy weather more likely will hinder retail sales.

Sources:\
Rose, N., Dolega, L. It’s the Weather: Quantifying the Impact of Weather on Retail Sales. *Appl. Spatial Analysis* 15, 189–214 (2022). https://doi.org/10.1007/s12061-021-09397-0 \
Tony, 2019. How does the weather affect retail performance & sales? Retrieved from https://www.anthonygregg.com/insights/how-does-the-weather-affect-retail-performance/

### Problem Statement
I am a foreign businessman who is not familiar with Singapore climate. I am planning to set up my first business in Singapore retail sector. However, before deciding on the category/sector of my first retail business, I would like to have a more comprehensive understanding of Singapore climate, and find out how the retail business is dependent on the regional weather. It is expected that rainy season will affect the retail sales unfavourably. The purpose of this project is to analyse the climate change in Singapore and the effect on retail sales.

### Datasets

1) Number of rain days in a month from 1982 to 2022\
*The number of rain days (day with rainfall amount of 0.2mm or more) in a month recorded at the Changi Climate Station.*

2) Total rain in a month from 1982 to 2022\
*The total monthly rainfall recorded at the Changi Climate Station.*

3) Surface air temperature in a month from 1982 to 2022\
*The monthly mean air temperature recorded at the Changi Climate Station.*

4) Sunshine duration in a month from 1982 to 2022\
*The monthly mean sunshine hours in a day recorded at the Changi Climate Station.*

5) Relative humidity from 1982 to 2022\
*The monthly mean relative humidity recorded at the Changi Climate Station.*

6) Monthly maximum daily rainfall from 1982 to 2022\
*The highest daily total rainfall for the month recorded at the Changi Climate Station.*

7) Hourly wet bulb temperature from 1982 to 2022\
*The hourly wet bulb temperature recorded at the Changi Climate Station.*

8) Monthly retail sales from 1985 to 2019\
*The Retail Sales Index (RSI) measures the short-term performance of retail industries based on the sales records of retail establishments.*
*The RSI is presented at both current prices and constant prices. The indices at current prices measure the changes of sales values which can result from changes in both price and quantity. By removing the price effect, the indices at constant prices measure the changes in the volume of economic activity.*
*The base year is 2017. (2017 = 100)*

*All data retrieved from Data.gov.sg*

### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**period**|*period[M]*| - |Datetime (Month)"YYYY-MM"| - |
|**year**|*period[Y]*| - |Datetime (Year)"YYYY"| - |
|**month**|*period[M]*| - |Datetime (Month)"M"| 1 to 12 represent Jan to Dec respectively. |
|**total_rainfall**|*float*|1982 to 2022|The total monthly rainfall recorded at the Changi Climate Station.|
|**number_rainyday**|*int*|1982 to 2022|The number of rain days (day with rainfall amount of 0.2mm or more) in a month recorded at the Changi Climate Station.|
|**surface_air_temp**|*float*|1982 to 2022|The monthly mean air temperature recorded in degree celsius at the Changi Climate Station.|
|**sunshine_duration**|*float*|1982 to 2022|The monthly mean sunshine hours in a day recorded at the Changi Climate Station.|
|**relative_humidity**|*float*|1982 to 2022|The monthly mean relative humidity recorded at the Changi Climate Station. Percentages are expressed as a value over 100, i.e. "100" represents 100%.|
|**max_daily_rainfall**|*float*|1982 to 2022|The highest daily total rainfall for the month recorded at the Changi Climate Station.|
|**monthly_wet_bulb_temp**|*float*|1982 to 2022|The monthly mean wet bulb temperature recorded at the Changi Climate Station|
|**retail_sales**|*float*|1985 to 2019|The short term performance of retail industries (Retail Sales Index (RSI)) with base year 2017 to remove the price effect over the period |

### Findings

 1) total rainfall

    - Total rainfall in Singapore is within a fixed and large range 0.2mm to 765.9mm, there is no significant upward or downward trend. To highlight, it has the largest standard deviation among all the variables. 
    
    - Generally, total rainfall will start to increase from October (150mm) to December (300mm) and fall towards February (100mm), with large variability and dispersion appears in months of November to January. Other months have a consistent total rainfall of around 150mm. 
 
2) number of rainy days
 
   - Number of rainy days has a wide dispersion from 5 to 22 days in most of the years, it has no obvious upward and downward trends.
    
   - Number of rainy days typically will increase from October (15 days) to December (20 days).
    
3) mean surface air temperature
 
   - Mean surface air temperature has displayed several big fluctuations in between with median temperature of 27.75 degree celsius, but overall has a slow upward trend.
     
   - Monthly analysis suggests that the mean temperature will rise from January (26.7 degree celsius) towards May or June by 2 degree celsius and then decline until December to 26.5 degree celcius, with a steady bell shaped pattern observed.
   
4) mean sunshine hours
 
   - The graph pattern suggest that Singapore has a mean sunshine hours trend at 5.7 hours, varying from 3 to 9 hours over the period.
     
   - Monthly graph shows that in general, Singapore sunshne hours will start to climb from December (4.5 hours) to January (7 hours), and then decline to 6hours and level off from March to August. September to November will fall steadyly to 4.5hours.
 
5) mean relative humidity
 
   - Mean relative humidity has a constant trend from 1985 at 83%, but plummet from 2011 to 2016. Overrall, the downward trend started in 2010s to 75%.
     
   - Monthly plot describes a high relative humidity from November to January at 85%, and stabilise in between February to October at 82%.
    
6) maximum rainfall in a day
 
   - The plot illustrates that the maximum rainfall in a day is quite consistent over years, with a median point at 43.5mm. 
    
   - However, the monthly plot highlighted a variation in the month of January, from 10mm to 210mm.

7) wet bulb temperature
 
   - Wet bulb temperature is a basic indicator of heat stress, which relates to the heat loss from damp skin. it is fatal if it exceeds 35°C when temperature and humidity are too high to remove heat from the inner body.
   
   - Wet bulb temperature generally are 3°C temperature lower than surface air temperature, with mean of 25.3°C. The highest wet bulb temperature is 26.6°C, but it has no obvious upward trend observed as compared to the mean surface air temperature.  
     
   - The temperature usually increase from January to May (24.7 to 25.7°C), and fall slowly towards December till 25°C.

8) RSI (sales value)

   - RSI displayed a strong upward trend over the year but remains steady from 2010s. 
    
   - Monthly graph in contrast shows a stable sales value in each month of the year, showing a constant growth in retail sales every month.
  

#### +ve correlated
- The total rainfall, number of rainy day, mean relative humidity, maximum rainfall in a day are positively strongly correlated.

- The mean surface air temperature, wet bulb temperature and mean sunshine hours are positively strongly correlated.

#### -ve correlated
- The total rainfall, number of rainy day are negatively strongly related with mean surface air temperature and mean sunshine hours.

- The mean surface air temperature is negatively strongly correlated with maximum rainfall in a day, mean relative humidity.

- The mean sunshine hours is negatively strongly correlated with mean relative humidty and maximum rainfall in a day.

### Conclusion

 According to the analysis, December usually has the highest total rainfall in a year, followed by November and January. Historical record shows that total rainfall has the greatest variation from month of November to January, which make it unpredictable how heavy the rain will be during these three months. While the mean of maximum rainfall is 52.33mm, the highest can be up to 216.2mm a day, as happened in Jan 2011. As total rainfall is strongly positively correlated with the number of rainy day and relative humidity, we can expect higher number of rainy days and relative humidity during these period. The highest number of rainy days has been 27days out of 30days, which was happened in Nov 2018; The relative humidity has been up to 90.7%, as in Dec 1991. 

Due to the these factors, December is generally the wetest month of a year, followed by January and November. While these are negatively correlated with mean surface air temperature, we expect these three months are cooler comparing to the remaining. This is correspond to our study that January happened to be the coolest month of a year with mean 26.7&deg;C, followed by December and November. 

Singapore temperature has a mean of 27.7&deg;C. Our analysis shows that May is usually the warmest month of a year with mean of 28.5&deg;C, followd by June and July. The maximum surface air temperature in the record was 29.5&deg;C and for wet bulb temperature was 26.6&deg;C, which is far lesser than the threshold of 35&deg;C that can be fatal. Although the temperatues are positively correlated with mean sunshine hours, February (which has the lowest total rainfall and number of rainy days) instead of May (the warmest month) appeared to have the longest sunshine hours with mean of 7 hours. This could be explained by the stronger correlation with total rainfall and number of rainy days. 

There is no upward or downward trend to the total rainfall and number of rainy day observed. Instead, the relative humidity displays a slow downward trend started in 2010s. Additionally, although there is no obvious upward trend observed in the wet bulb temperature for now, it has a clear increasing trend for surface air temperature. Since these two temperature are positively correlated with 3&deg;C difference typically, it is worth noting that the future surface air and wet bulb temperature could be higher. 

In the analysis of RSI, January generally has the lowest RSI and February has the highest RSI over the year. Also, RSI itself displayed a strong upward trend till 2010 and then a constant growth. However, we have found out the RSI (retail sales index) has little to no correlation with all the weather variables. A multimodal distribution in the RSI could possibly mean that there are underlying independent groups of subpopulation in the data, which required further and deeper study to analyse individually the correlation with weather.  

In conclusion, Singapore has uniform temperature, high humidity and abundant rainfall. Singapore Northeast Monsoon Season happen in end of every year to the subsequent month of early March. In the early phase, Monsoon Surges cause widespread continuous moderate to heavy rain, usually from December to early January. In the later phase, Singapore will be relatively dry with more sunshine exposure from late January to early March. It is presented that Singapore climate has no material effect on the retail sales overall, it might be due to the multimodal distribution found in the dataset. Hence, it is recommended to conduct additional research.

 According to the analysis, December usually has the highest total rainfall in a year, followed by November and January. Historical record shows that total rainfall has the greatest variation from month of November to January, which make it unpredictable how heavy the rain will be during these three months. While the mean of maximum rainfall is 52.33mm, the highest can be up to 216.2mm a day, as happened in Jan 2011. As total rainfall is strongly positively correlated with the number of rainy day and relative humidity, we can expect higher number of rainy days and relative humidity during these period. The highest number of rainy days has been 27days out of 30days, which was happened in Nov 2018; The relative humidity has been up to 90.7%, as in Dec 1991. 

Due to the these factors, December is generally the wetest month of a year, followed by January and November. While these are negatively correlated with mean surface air temperature, we expect these three months are cooler comparing to the remaining. This is correspond to our study that January happened to be the coolest month of a year with mean 26.7&deg;C, followed by December and November. 

Singapore temperature has a mean of 27.7&deg;C. Our analysis shows that May is usually the warmest month of a year with mean of 28.5&deg;C, followd by June and July. The maximum surface air temperature in the record was 29.5&deg;C and for wet bulb temperature was 26.6&deg;C, which is far lesser than the threshold of 35&deg;C that can be fatal. Although the temperatues are positively correlated with mean sunshine hours, February (which has the lowest total rainfall and number of rainy days) instead of May (the warmest month) appeared to have the longest sunshine hours with mean of 7 hours. This could be explained by the stronger correlation with total rainfall and number of rainy days. 

There is no upward or downward trend to the total rainfall and number of rainy day observed. Instead, the relative humidity displays a slow downward trend started in 2010s. Additionally, although there is no obvious upward trend observed in the wet bulb temperature for now, it has a clear increasing trend for surface air temperature. Since these two temperature are positively correlated with 3&deg;C difference typically, it is worth noting that the future surface air and wet bulb temperature could be higher. 

In the analysis of RSI, January generally has the lowest RSI and February has the highest RSI over the year. Also, RSI itself displayed a strong upward trend till 2010 and then a constant growth. However, we have found out the RSI (retail sales index) has little to no correlation with all the weather variables. A multimodal distribution in the RSI could possibly mean that there are underlying independent groups of subpopulation in the data, which required further and deeper study to analyse individually the correlation with weather.  


### Recommendation and Limitation
There is no correlation found between retail sales index and climate change in this analysis. However, the data revealed that the retail sales index has a multimodal distribution, which means that there are different underlying independent groups in the dataset as explained earlier. Further analysis should be done to look at the cluster of the modes separately. Additional study could focus on different retail sectors as the cluster could be due to the inclusion of different independent sectors in the data. There is a study provided significant result based on analysis for different product categories, as it proves that demands for sporting goods and apparel products are more weather sensitive than other goods (Tron, 2022). It could also be an offsetting effect present by different industries that causes the insignificant result. It is proved by Starr-McCluer study that monthly effect in retail sales tend to be offsetting, and largely cancel out at a quarterly frequency (Starr-McCluer, 2000). Additional data and research required to verify this possibility.


This analysis has some limitations in the coverage and depth of data available. Additionally, this analysis has not able to capture any product pricing or price promotional activities that may be influential in consumer purchasing behaviours. This unplanned or spontaneous purchasing decisions, particularly promotions, are less likely to be linked with weather conditions.

Tron, B.R. (2022). The Impact of Weather on Retail Sales. Retrieved from https://www.frbsf.org/economic-research/publications/economic-letter/2022/august/impact-of-weather-on-retail-sales/
    
Starr-McCluer, M. (2000). The Effects of Weather on Retail Sales. Retrieved from https://www.federalreserve.gov/pubs/feds/2000/200008/200008pap.pdf
