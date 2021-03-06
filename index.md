<center><img src="{{ https://github.com/EdDataScienceEES/tutorial-lynseythomson/blob/master/Blue_Marker_map.png }}/Blue_Marker_map.png" alt="Img"></center>

# Intro to Making Study Site Maps
### Tutorial Aims

#### <a href="#section1"> 1. Using the leaflet package.</a>

#### <a href="#section2"> 2. Creating the site map.</a>

#### <a href="#section3"> 3. Editing the colours!</a>

Ever struggled creating a map for you study sites? Fear not! Intro to making Study Site Maps is here to save you trouble and heartache, by using the leaflet package!
---------------------------

Study site maps are important for field studies. They allow a visual aid to sample sites, transparancy, and can help with future replication.

This tutorial will look at creating a study site map with code, using R Studio and the <a href="https://rstudio.github.io/leaflet/" target="_blank">leaflet</a> package.

You can get all of the resources for this tutorial from <a href="https://github.com/EdDataScienceEES/tutorial-lynseythomson" target="_blank">this GitHub repository</a>. Clone and download the repo as a zip file, then unzip it.

<a name="#section1"></a>

## 1. Using the leaflet package.
### Introduction to leaflet.
The first, and more simple method of creating a study site map is using the **leaflet** package. This package is useful as it allows you to create the maps in R Studio, by simply having 'latitude' and 'longitude' columns in your data frame. The maps can have interactive elements, such as pop-ups or markers but can also be static for the use in scientific papers.

We will use the lat/long coordinates collected from a student's field trip to Loch Tay, Scotland for the Ecological Measurement course at the University of Edinburgh.

The leaflet package is useful, as it can work with data frames with lattitude and longitude columns, a lattitude/longitude matrix and also also through the **sp** package through spatial points, lines, polygons and spatial polygons. However, in this tutorial we are just focusing on using **leaflet** through a data frame with lat/long columns.

### Getting Started
Firstly, please open 'R Studio', create a new a new script by clicking on the `File/ New File/ R Script`. Remember to date your script, add your name, and contact details at the start of the script, using hastags to add clear comments.

If you are unsure of how to use <a href="https://ourcodingclub.github.io/2017/02/27/git.html">Github</a> or <a href="https://ourcodingclub.github.io/2016/11/13/intro-to-r.html">R Studio</a>, check out these handy tutorials.




```
# ============  Intro to Map Making  ==============
# ============    Complete script    ==============
# By Lynsey Thomson
# Contact: s1745313@ed.ac.uk
```

Remember to use your own name! Now time to install the packages needed for this tutorial. Copy and paste the code below.

```
# Setting up --

# Install packages
install.packages("tidyverse")
install.packages("leaflet")
install.packages("readr")
install.packages("ggplot2")
install.packages("htmltools")
install.packages("htmlwidgets")

# Load packages
library(tidyverse) # for easy data manipulation
library(leaflet)   # for map making
library(readr)     # for importing the data set
library(ggplot2)    # a different tool for map making
library(htmltools) # to add text one the labels in leaflet
library(htmlwidgets) # to save the interactive maps
```
Remember to run each line of code, by pressing command + enter on Mac, or control + enter on windows. 

Next, we must import the data to work with it. It's good practice to check that that it's loaded properly.

```
Step 1: load site coordinates.
site_coords <- read_csv("Raw_Data/site_coords.csv")

# View data to check it loaded properly
View(site_coords)
# Looks good!
```
Furthermore, when assinging the data frame to an object, it's useful to use informative names. Above, we use 'site_coords' which is easily recognisable, compared to for example naming it 'first_object'.

<a name="section2"></a>
## 2. Creating the site map.
Using the `leaflet()` function, we will create the study site map. Wrapping the whole code snippet in () will make it easier to save/export. Here, we are adding black circles as markers. The leaflet package is highly customisable, notice there are a number of different elements you can add. However, we have left them blank in this example.

A useful element to add is the `addScaleBar()` because this is essential in scientific text.

```
# Step 2: Use the leaflet() function to create the map
(leafletMap <- leaflet(data = site_coords) %>%   # The '%>%' sign is called  pipe, and runs the line onto the next line without retyping the object!
  addTiles() %>% 
  addCircles(lng = ~long,    # Here we are adding circles to mark the study sites.
             lat = ~lat,     # When calling data from the data frame, put '~' 
             radius = 50,
             fillOpacity = 1,
             stroke = FALSE,
             color = 'black',          # Here we are just using black, however other colours can be used!
             label= ~Site_Name) %>%    # The '~' tell it to use the column 'site_Name' from the df to make labels.
  addScaleBar(position = 'bottomleft')) # Adding a scale bar is important for scientific writing!
```

<a href="http://rpubs.com/lynseythomson/556443"> Check out this link to see what your map should look like!</a>


<center><iframe src="{{ https://github.com/lynseythomson/Intro_To_Maps }}//Maps/leafletMap_saved.html" width="100%" height="600px" style="border:none"></iframe></center>


<center><img src="{{ https://github.com/lynseythomson/Intro_To_Maps }}/Maps/leafletMap_saved.html" alt="Img"></center>


<a name="section2"></a>
## 3. Editing the colours!
Now, let's jazz it up a little and add red, opaque markers with the study site names as well. You can play around with the colour outline and fill.

```
# This time we are adding blue, slightly opaque cirlces, and the site name appears too!
leaflet(data = site_coords) %>%   
  addTiles() %>% 
addCircleMarkers(lng = ~long, 
                 lat = ~lat,
                 radius = 8 , color="purple",  
                 fillColor = "blue", 
                 stroke = TRUE, 
                 fillOpacity = 0.5,
                 label= ~Site_Name) %>%   
  addScaleBar(position = 'bottomleft') 
```

<a href="http://rpubs.com/lynseythomson/556442"> Check out this link to see what your map should look like!</a>

<center><iframe src="{{ https://github.com/lynseythomson/Intro_To_Maps }}//Maps/Purple_and_blue_map_leaflet.html" width="100%" height="600px" style="border:none"></iframe></center>



Let's change the shape of the markers now! Instead of adding circles, we will add blue markers!

```
leaflet(data = site_coords) %>%
  addTiles() %>%
  addMarkers(label = ~Site_Name,
             labelOptions = labelOptions(noHide = T)) %>%
  addScaleBar(position='bottomleft')
```

<a href="http://rpubs.com/lynseythomson/556440"> Check out this link to see what your map should look like!</a>


http://rpubs.com/lynseythomson/556440

<center><iframe src="{{ https://github.com/lynseythomson/Intro_To_Maps }}//marker_map_saved.html" width="100%" height="600px" style="border:none"></iframe></center>


### Thank you for taking the time to do this tutorial! Let's recap what we have learned!
- The leaflet package is a super easy and simple way to create a study site map.
- Using the leaflet() function, adding our data frame and creating a map.
- Adding colour markers, and changing the design!

### Useful Links
- To read more about the leaflet package click <a href="https://rstudio.github.io/leaflet/map_widget.html">here</a>, or <a href="https://bookdown.org/yihui/rmarkdown/interactive-documents.html">here</a>.

- For more on `ggplot2`, read the official <a href="https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf" target="_blank">ggplot2 cheatsheet</a>.


<hr>
<hr>

#### Check out our <a href="https://ourcodingclub.github.io/links/" target="_blank">Useful links</a> page where you can find loads of guides and cheatsheets.

#### If you have any questions about completing this tutorial, please contact us on ourcodingclub@gmail.com

#### <a href="INSERT_SURVEY_LINK" target="_blank">We would love to hear your feedback on the tutorial, whether you did it in the classroom or online!</a>

<ul class="social-icons">
	<li>
		<h3>
			<a href="https://twitter.com/our_codingclub" target="_blank">&nbsp;Follow our coding adventures on Twitter! <i class="fa fa-twitter"></i></a>
		</h3>
	</li>
</ul>

### &nbsp;&nbsp;Subscribe to our mailing list:
<div class="container">
	<div class="block">
        <!-- subscribe form start -->
		<div class="form-group">
			<form action="https://getsimpleform.com/messages?form_api_token=de1ba2f2f947822946fb6e835437ec78" method="post">
			<div class="form-group">
				<input type='text' class="form-control" name='Email' placeholder="Email" required/>
			</div>
			<div>
                        	<button class="btn btn-default" type='submit'>Subscribe</button>
                    	</div>
                	</form>
		</div>
	</div>
</div>
