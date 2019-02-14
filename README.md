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

### Visual comparison of ridership on maintenance days and regular days

### Impact of maintenance on network of stations
In essence, the MTA subway system is a network in which stations are nodes which connects to other nodes through subway lines which are the edges in the network. A maintenance activity impacts the ridership of a station by suspending its edges with other stations thus in turn impacting its connectivity with the network. The more the edges of a node are perturbed, the severe will be the impact. The stations which are in the middle of these sections lose more riders in comparison to those at the corners. Rather the riders of the intermediate stations, access the corner stations on maintenance day to avail the subway service. Thus, these corner stations although having maintenance, experience the normal or in some cases increased ridership. Therefore, the maintenance sample has further bifurcations as, station date combinations with general maintenance, and station date combinations with maintenance and entry gain(corner nodes).

### Independent samples T-test to compare different samples

### Quantifying the loss in ridership due to maintenance activities:

### Modelling the Data
The ridership of a subway system can be considered as function of trend and periodicity, regular features, and maintenance features.
$$Ridership = f(Trend,Periodicity) + f(Regular Features) + f(Maintenance Features)$$
By standardizing the ridership data with moving mean and standard deviation we have already removed trend and periodicity. Thus,
Standardized z-score = f(Regular Features) + f(Maintenance Features)
Now, a possible method to calculate impact of maintenance is to learn the normal behavior of ridership through regular day data points and use its prediction for maintenance days as counterfact. But as we do not know all the features which affect the normal behavior of subway ridership, this will be difficult for us to perform. Another method can be to pick a mixed sample of regular and maintenance days, and then using the maintenance feature attempt to explain maximum variation in the standardized z-score without overfitting. For a regular day data point, the impact of maintenance features will be 0. Thus,
Standardized z-score = f(Regular Features)
This is shown in the figure 5 by the distribution  colored in blue. This distribution has mean ~0 and shape almost similar to random distribution. As we know, the residual of  a ML model is randomly distributed, if we subtract the modelled variation using maintenance features from standardized z-score, we will get a random distribution which will be similar to the distribution of  z-score on regular days. Thus, we can use this modelled variation as the impact of maintenance on subway ridership.
This can also be understood using figure 5 and table 1, as the distribution is almost normal with mean 0 on regular days(blue distribution) which is pulled down to negative on maintenance days. Using the maintenance feature we are trying to model this effect by which the scores are pulled down and use it as impact of maintenance on ridership.


## Results

## Future Works

