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

## Gathering Data
The first order of business was importing my data. I wanted to make sure that I was only pulling Open Street Map data from the cities that I was interested in 

I used OSMNX to fix elevation data to nodes and from there used the add_edge_grades function to create a new column that shows the absolute value of the grade for each street segment. To visualize the grades within the project area I made a plot using matplotlib to show the prelance of different grades in the project area. Not surprisingly the bulk of streets are relatively flat (between 0 and 3%) but the data also includes hilly areas that can be found in Eastern parts of Oakland and Berkeley.

I also made a map using osmnx to visualize where the the steep grades. This was helpful just to spot check using my own knowledge of the area. In this map, the the brighter the color the steeper the grade.

<p align="center">
  <img src="https://user-images.githubusercontent.com/98047774/166982225-d2c6d3ce-2e69-4009-88a5-ac56b76792eb.png" />
</p>
<p alig<img width="903" alt="Screenshot 2022-05-05 111305" src="https://user-images.githubusercontent.com/98047774/166987256-637ee88a-49f7-4ecc-9d3f-ba7d2bdf1f0c.png">
  <img src="https://user-images.githubusercontent.com/98047774/166983071-e291dcda-faa0-47f3-9433-cf897ee66d9a.png" />


I also wanted to investigate the quality of the roads by themselves. I found that the marjority of roads in the project area were rated poor/failing. I mapped the streets onto an interactive folium map.


<p align = "center"><img src="https://github.com/jgberman/CP255/blob/main/images/pavement_condition_graph.png"></p>
<img width="903" alt="Screenshot 2022-05-05 111305" src="https://user-images.githubusercontent.com/98047774/166987326-0d154096-ba40-44ff-888c-899c42e9c7ae.png">
Side note: I couldn't get the folium map to work because the html file was too large, so here is just a screen shot to give you an idea. The Reds are streets in poor or failing condition, yellows are streets in fair condition and greens are streets in good condition.

The next step was to merge all of the data together into on geodataframe. I did this using a geopandas spatial join between the MTC and OSM geodata. Together I had one data set that I could use to create an index.

## Bike Index Methodology
To create my personal bike index, I started by looking at other methodologies that have tried to do the same thing. In my research I came accross a <a href="https://essay.utwente.nl/83741/1/hartanto.pdf">paper</a> looking to establish a bikeability index to enable assessment of Transit Oriented Development. Using this as inspiration, I made my own index to help show the best streets to bike on using pavement condition, street steepness, presence of bike infrastructure and types of roads. By rating these characteristics I was able to develop a method of determining the streets with the most ideal biking characteristics.

<p align="center">
  <img src="https://user-images.githubusercontent.com/98047774/167023572-fd253fde-e320-467d-841b-5bdf3cd546ba.png"
       width="400"/>
</p>

## Results
Based on the index I can show where the best streets for biking are. The lower the index number, the better the biking conditions:

![bikeind_map](https://user-images.githubusercontent.com/98047774/167026750-54396b0d-4f9c-4d86-bf7c-a61c3206494a.png)

With this information, I was able to use the index to weight the distance of each street segment. I used this weighted distance to find the optimal route between my house and Bauer Wurster Hall using OSMNX's shortest_path function. 

![OSMNX_Shortest Route](https://user-images.githubusercontent.com/98047774/167028148-f01c80aa-c6c8-4da9-b47b-4d93be72cd44.png)

To get a better view I made a folium map, but again the file was too large for me to show here so here is a screenshot:

<img width="848" alt="image" src="https://user-images.githubusercontent.com/98047774/167029201-287c8970-5fd4-42fe-b0b2-faaedbc4fd22.png">

## Reflections
The route that was created may be the optimal based on the conditions dictated, but does not match the optimal route that I have found for myself. There are a few reasons for the discrepancy.

1) The methodology does not differentiate between different levels of bicycle infrastructure. A road with a protected bikelane is shown as equivalent as a road with sharrow markings, despite the fact that protected bikelands greatly affects the quality of my ride whereas sharrows have a negligible effect on the quality of my ride.
2) The methodology does not differentiate between the different types of roads except for motorways (I excluded limited access highways from the data set). I prefer riding on residential streets with a maximum of two lanes, rather than 4 lane arterials.
3) The pavement condition index was from 2018. Some roads have been repaved since then, which would change the scores and potentially alter the route.

With time and energy all of these issues could be addressed, but for now I'm just happy to know that it is possible to make this map.

