# Impact of Subway Maintenance on Subway and Taxi Ridership

## Introduction:
MTA has to carry out periodical maintenance which causes a complete or partial shutdown of the subway services at various stations. Due to these frequent maintenance, commuters face inconvenience, and they have to switch to other modes for transportation. Although MTA attempts, to minimize inconvenience to commuters by conducting these activities in night or weekends, it has never been analyzed whether these activities in actual affect subway ridership or not and if yes by how much? A study of this kind will help to estimate the loss of potential ridership, understand avenues where this loss is maximum, identify the causes which are leading to significant loss, loopholes in current maintenance schedule planning and how it could be optimized. Besides, this can also help to study whether the loss in subway ridership creates demand for other modes of transportation. It can be beneficial for the management of taxi fleets as for management of Taxi, and For Hired Vehicles, resource allocations are the top priority and thus, an understanding about potential events which can lead to increase in demand and will help to maximize profits better.

## Research Objectives:
1. To examine whether the ridership on days with maintenance activities is different and lower than the regular days.
2. If the answer to 1 is yes, what are the leading causes of loss in ridership due to maintenance on different subway lines?
3. To examine whether taxi ridership in taxi zones where maintenance was present is higher than regular days.
4.  If the answer to 3 is yes, how to quantify the increase in customer demand?

## Datasets:
1. MTA Turnstile Data: The data shows the entry/exit register values for all turnstiles at all subway stations for any given date. The turnstiles have readings at 4 hours intervals. As each subunit has different traffic counters, first we allotted a unique id code to each. After calculating counts in the unique id level, we aggregated them on a daily basis by station.
We used the data from 27 August 2017 to 31 October 2018.
Url : http://web.mta.info/developers/turnstile.html
  
2. My MTA Alert: My MTA Alert carries the information regarding the scheduled maintenance carried out by the Metropolitan Transportation Authority (MTA) for NYC Subway Stations. The maintenance data is present in text format without a structure which can be parsed using machines thus, the maintenance data was manually interpreted and processed to obtain its effect on station+date combination level.
The data was collected for all weekends from October 2017 to September 2018 along F, N and R lines. 

Url: https://www.mymtaalerts.com/messagearchive.aspx

3. NYC Subway GTFS static: This data provided the network of subway stations and routes. Trains make stop at any given station on their route based on the type of service. Different types of services are full-time service, late night service, part-time service, express service and local service. We have restricted the scope of the study and picked 106 stations which are served on F, N and R lines. The reasons for this selection were, all these lines run between Brooklyn and Queens, for large sections of their routes they run parallel to each other, and 40% of maintenance activities in the past one year were conducted on these lines.


3. TLC Trip Data: The yellow and green taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off  locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.
Url: http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml


## 

## Methodology:

