# Smooth Cycling- CP 255 Final Project
**Project by Josh Berman**

I bike to UC Berkeley campus every day. One of the most annoying parts of my commute is dodging potholes. I would like to find a safe and convenient route to campus while riding on the smoothest streets. My solution is to come up with a new bikeability index that takes into account pavement condition to come up with a method for finding the optimal route from my house in Oakland to Bauer Wurster hall on campus. I also accounted for the presence of existing bike facilities and elevation change in creating my personal bikeability index.

I decided to focus this project on the portion of the East Bay that I mostly bike around (Berkeley, Emeryville, Oakland and Piedmont), but the method that I put together could be extended to the whole bay area.



## Data Sources

#### MTC
The pavement condition data that I have gathered comes from an MTC data set that lists the condition and coordinates of all streets within the nine county bay area. The most recent data is from 2018.

#### USGS
Elevation data was calculated using raster data from the US Geological Survey. 

#### Open Street Maps
I opted to use street data from Open Street Maps, which provided me with accurate data on the street locations as well as information on whether there are bike facilities present on a given street. 

<h1><u>Process</u></h1>

### Gathering Data
The first order of business was importing my data. I wanted to make sure that I was only pulling Open Street Map data from the cities that I was interested in 

I used OSMNX to fix elevation data to nodes and from there used the add_edge_grades function to create a new column that shows the absolute value of the grade for each street segment. To visualize the grades within the project area I made a plot using matplotlib to show the prelance of different grades in the project area. Not surprisingly the bulk of streets are relatively flat (between 0 and 3%) but the data also includes hilly areas that can be found in Eastern parts of Oakland and Berkeley.

I also made a map using osmnx to visualize where the the steep grades. This was helpful just to spot check using my own knowledge of the area. In this map, the the brighter the color the steeper the grade.
