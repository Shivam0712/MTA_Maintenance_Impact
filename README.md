# Impact of Subway Maintenance on Subway and Taxi Ridership

## Introduction:
MTA has to carry out periodical maintenance which causes a complete or partial shutdown of the subway services at various stations. Due to these frequent maintenance, commuters face inconvenience, and they have to switch to other modes for transportation. Although MTA attempts, to minimize inconvenience to commuters by conducting these activities in night or weekends, it has never been analyzed whether these activities in actual affect subway ridership or not and if yes by how much? A study of this kind will help to estimate the loss of potential ridership, understand avenues where this loss is maximum, identify the causes which are leading to significant loss, loopholes in current maintenance schedule planning and how it could be optimized. Besides, this can also help to study whether the loss in subway ridership creates demand for other modes of transportation. It can be beneficial for the management of taxi fleets as for management of Taxi, and For Hired Vehicles, resource allocations are the top priority and thus, an understanding about potential events which can lead to increase in demand and will help to maximize profits better.

## Research Objectives:
1. To examine whether the ridership on days with maintenance activities is different and lower than the regular days.
2. If the answer to 1 is yes, what are the leading causes of loss in ridership due to maintenance on different subway lines?
3. To examine whether taxi ridership in taxi zones where maintenance was present is higher than regular days.
4.  If the answer to 3 is yes, how to quantify the increase in customer demand?

## Datasets:
**1. MTA Turnstile Data: The data shows the entry/exit register values for all turnstiles at all subway stations for any given date.** The turnstiles have readings at 4 hours intervals. As each subunit has different traffic counters, first we allotted a unique id code to each. After calculating counts in the unique id level, we aggregated them on a daily basis by station.
**We used the data from 27 August 2017 to 31 October 2018.**

Url : http://web.mta.info/developers/turnstile.html
  
**2. My MTA Alert: My MTA Alert carries the information regarding the scheduled maintenance carried out by the Metropolitan Transportation Authority (MTA) for NYC Subway Stations.** The maintenance data is present in text format without a structure which can be parsed using machines thus, the maintenance data was manually interpreted and processed to obtain its effect on station+date combination level.
**The data was collected for all weekends from October 2017 to September 2018 along F, N and R lines.**

Url: https://www.mymtaalerts.com/messagearchive.aspx

**3. NYC Subway GTFS static: This data provided the network of subway stations and routes. We have restricted the scope of the study and picked 106 stations which are served on F, N and R lines.** The reasons for this selection were, all these lines run between Brooklyn and Queens, for large sections of their routes they run parallel to each other, and 40% of maintenance activities in the past one year were conducted on these lines.
<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset1.PNG" align="center" border="1"/>


**4. TLC Trip Data:** The yellow and green taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off  locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.
Url: http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml

## Methodology:

The data points in our final processed data are station & dates combination with the maintenance features. Any given maintenance activity impacts a group of stations on its scheduled dates; we can comprehend this impact as the decrease in ridership for the stations from the regular. The apt way to do this is to take the sample of days when maintenance activity was conducted and compare its distribution of ridership with days when maintenance was not present. If ridership in our maintenance sample is significantly lower than the regular days then, we can confirm our hypothesis that maintenance does affect ridership.

### Non-Uniformity and Non-Stationarity in Data
Essentially, as we are trying to study the impact in 106 stations on F, N and R lines, and these stations have different ridership behavior on Saturdays and Sundays, we have 212 time series in our data.
1. Data points comes from different stations which have different average ridership. Thus, all data points are not uniformly comparable.
2. Data points comes from different periods of time which may not be stationary.
To overcome these challenges we standardize the data by deducting the rolling mean and diviing by the rolling standard deviation.
We conduct the Augmented Dickey-Fuller test which is a standard method to test the stationarity in time series data, on all the time series before and after the above standardization.
<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset2.PNG" align="center" border="1"/>

### Visual comparison of ridership on maintenance days and regular days
<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset3.PNG" align="center" border="1"/>

### Impact of maintenance on network of stations
In essence, the MTA subway system is a network in which stations are nodes which connects to other nodes through subway lines which are the edges in the network. A maintenance activity impacts the ridership of a station by suspending its edges with other stations thus in turn impacting its connectivity with the network. The more the edges of a node are perturbed, the severe will be the impact. The stations which are in the middle of these sections lose more riders in comparison to those at the corners. Rather the riders of the intermediate stations, access the corner stations on maintenance day to avail the subway service. Thus, these corner stations although having maintenance, experience the normal or in some cases increased ridership. Therefore, the maintenance sample has further bifurcations as, station date combinations with general maintenance, and station date combinations with maintenance and entry gain(corner nodes).
<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset7.jpg" align="center" border="1"/>


### Independent samples T-test to compare different samples
<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset4.PNG" align="center" border="1"/>

<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset9.PNG" align="center" border="1"/>

From the results of independent samples T-test we can see, indeed sample with maintenance and without maintenance are significantly different, and sample with maintenance & entry gain is not significantly different from without maintenance.
### Quantifying the loss in ridership due to maintenance activities:

### Modelling the Data
The ridership of a subway system can be considered as function of trend and periodicity, regular features, and maintenance features.

 
**Ridership = f(Trend,Periodicity) + f(Regular Features) + f(Maintenance Features)**

By standardizing the ridership data with moving mean and standard deviation we have already removed trend and periodicity. Thus,

**Standardized z-score = f(Regular Features) + f(Maintenance Features)**

For a regular day data point, the impact of maintenance features will be 0. This is shown in the figure 5 by the distribution  colored in blue. This distribution has mean ~0 and shape almost similar to normal distribution.

Thus our modelling objective is to model the maximum possible variation in the z-score using only maintenance features without overfitting. This modelled variation can be used as the impact of maintenance on subway ridership.
We use tree based decision models here:

<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset9.PNG" align="center" border="1"/>

## Results
**1. Overall in October 2017 to September 2018, there was a total loss of 1.45 Million riders on F, N and R lines just for the maintenance that occured on weekends.**

<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset10.PNG" align="center" border="1"/>

**2. Signal and Track maintenance are the leading cause of ridership losses.**

<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset5.PNG" align="center" border="1"/>

**3. On F line Signal is the Major problem, whereas on N & R lines Track is the major problem.**

<img src="https://github.com/Shivam0712/MTA_Maintenance_Impact/blob/master/Assets/Asset6.PNG" align="center" border="1"/>

## Conclusion and Future Work:


Further, this we also need to take into account the taxi ridership data and relate it with the maintenance activities of MTA Subway.

## Conclusion:
From this study we are able to conclude with statistical significance that the scheduled maintenance activities in MTA subway system negatively impacts the ridership. We also uncovered that the maintenance activities affect ridership by impacting the underlying network connections of stations. Stations at the corner of sections where maintenance is conducted show normal or increased ridership on maintenance days. We were able to establish a method through which this loss in ridership can be quantified and found that the loss of ridership was about 1.45 Million riders in the given time frame. Maintenance activities related to signals on F line and related to tracks on N and R lines are sternly leading to loss in riderships. 

## Limitations & Future Works:
Currently this analysis has many limitations:
1. Analysis was only done on 3 Lines; NYC MTA Subway has total 23 operational lines.
2. Only scheduled maintenance for weekends were considered. Weekday maintenance and delay in service are still to be analyzed.
3. We have analyzed only the impact on ridership which originates at affected stations.(only Checkin's)
4. For maintenance data, we have used the self processed publicly available text data. Use of GTFS-Realtime data here will enable us to further improve our analysis.
5. For the network connections, currently we were able to create only the binary features i.e., presence or absence of an edge. With more sophisticated data such as of GTFS-Realtime, we will be able to add weights to these edges too.
6. Lastly, we do not take into account the shifting of ridership to other lines as we focus our analysis on F,N,R lines. 

Future works would be first to quantify the surge in taxi ridership during subway maintenance. Second, to scale this analysis for all subway stations. Third, to incorporate GTFS-realtime data and enrich the network features and ultimately use this new data source to extend the study and include subway delay too. 
