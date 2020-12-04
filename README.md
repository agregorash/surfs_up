# Surfs Up Analysis
![hawaii-surfing-mecca-blog.jpg](https://github.com/agregorash/surfs_up/blob/main/Resources/hawaii-surfing-mecca-blog.jpg)
## Project Overview

After vacationing to Hawaii and discovering a newfound passion of surfing, I have come up with a plan to open a surf and shack that will allow me to not only pursue this passion but also live in beautiful Hawaii.  In order to turn this dream into reality I have constructed a business plan and have reached out to a local investor, W.Avy, who shares my passion for surfing.   I have been tasked with performing historical weather analysis on several different locations to ensure that we open the surf and shake shack in the most ideal location.
## Resources
- Data Sources: [hawaii.sqlite](https://github.com/agregorash/surfs_up/blob/main/hawaii.sqlite)
               
 - Software: Python 3.8.3, Jupyter Notebooks, Anaconda 3,  

## Results

I have performed a statistical analyses on the temperature during the months of June and December, to provide a quick glimse at the minimum, maximum and average temperatures at opposite times of the year.  The results of these statistical analyses (seen below) show:

-  June temperatures averaged around 75 degrees, with a maximum temperature of 85 degrees and a minimum temperature of 64 degrees
-  December temperatures averaged around 71 degrees, with a maximum temperature of 83 degrees and a minimum temperature of 56 degrees
-  Both month's temperature statistics contained tightly grouped data, with standard deviations of 3.26 degrees for the month of June and 3.75 degrees for December

### June Temperatures

![June_temps.PNG](https://github.com/agregorash/surfs_up/blob/main/Resources/June_temps.PNG)


### December Temperatures

![dec_temps.PNG](https://github.com/agregorash/surfs_up/blob/main/Resources/dec_temps.PNG)

## Summary

In summary, it can be concluded that Hawaii is an excellent place to open up a surf and shake shack based on the temperature data.  Temperatures are mild and warm year round with averages of about 75 degrees at the height of Summer and about 71 degrees at the depths of Winter.  This means that locals and tourists will be at the beaches surfing and relaxing year-round, providing a consistent customer base for our business.

Temperature, however, is not the only weather factor that I need to keep in mind while performing weather analysis on our potential vendor location.  Excessive rain can prevent people from heading out to the beach.  I have executed queries for the months of June and December that plot the precipitation recordings at our target location (station USC00519281) in order to ensure we are indeed making the correct data-based decision for our venture location.

### June Precipitation Histogram

```
# Additional query to gather more weather data for the month of June
june_prcp = session.query(Measurement.prcp).filter(extract('month', Measurement.date)==6).\
filter(Measurement.station =='USC00519281')
june_prcp_list = [precip.prcp for precip in june_prcp]
juneprcp_df = pd.DataFrame(june_prcp_list, columns=["June Precipitation"])
juneprcp_df.plot.hist(bins=5)
```
![june_prcp.PNG](https://github.com/agregorash/surfs_up/blob/main/Resources/june_prcp.PNG)

### December Precipitation Histogram

```
# Additional query to gather more weather data for the month of December
dec_prcp = session.query(Measurement.prcp).filter(extract('month', Measurement.date)==12).\
filter(Measurement.station =='USC00519281')
dec_prcp_list = [precip.prcp for precip in dec_prcp]
decprcp_df = pd.DataFrame(dec_prcp_list, columns=["December Precipitation (in inches)"])
decprcp_df.plot.hist(bins=5)
```
![dec_prcp.PNG](https://github.com/agregorash/surfs_up/blob/main/Resources/dec_prcp.PNG)

### Conclusion

The precipitation histogram for the month of June shows 120 instances of no precipitation with only a few occurances of more than 1 inch of rain.  The December histogram shows similar results with over 140 instances of no precipitation, but more instances of precipitation exceeding 1 inch of rain.  Nonetheless, these precipitation charts support our original temperature-based conclusion that Hawaii, and in particular our target location, is an ideal location for our venture.
