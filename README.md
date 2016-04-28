# An Analysis of Well-Being in San Francisco

This is a one-day project completed as part of the Bayes Impact hackathon.

Prompt
------

Housing inequality is present in cities across the United States, rendering low
income families unable to obtain affordable housing. Lack of fair housing
opportunities is just one of the problems communities face: many people also
lack access to transportation and services within the community. Both
communities and residents suffer when specific populations cannot utilize all
the resources communities have to offer. National and local data sets have been
created by initiatives that are addressing the gaps between residents in
communities.

Help cities enhance their use of data and evidence to uncover new ways to
revitalize neighborhoods and improve the lives of residents. Leverage federal
and local open data to identify disparities in access to resource, services,
and housing that communities need to thrive. Interactive informative tools that
show current trends, or tools to illustrate federal and local spending or
regulatory changes, have the potential to reinvent the way communities come
together and grow.

[Original Brief for The Project](http://bayeshack.org/housing-and-urban-development.html)

Goals
-----
This project aims at characterizing the livability of San Francisco
neighborhoods, and does so in 2 ways:
- By providing meaningful metrics for each neighborhood, related to crime,
  transportation, access to restaurants, together with tools to visuzalize
  them
- It investigates the relation between those features and the
  satisfaction of neighborhood residents.

Examples
--------

Visualizing features of neighborhoods using chloropleths.

![Chloropleth](./screencast-chloropleth.gif)

Eploring the relationship between the features and the general level of
satisfaction of inhabitants.

![Screencast](./screencast-factors.gif)

Data and Methodology
--------------------
### Survey Data

We used the survey data set - [San Francisco City Survey Data 1996-2015](https://data.sfgov.org/City-Management-and-Ethics/San-Francisco-City-Survey-Data-1996-2015/89tc-4uwi) for computing the satisfaction index of San Francisco city inhabitants as follows - 
* Each field in the survey data set represents a numerical categorical response to a survey question (except for a few columns related to survey and demographic information like year, zipcode, district etc)
* Only the questions with graded responses (from F-Very Bad to A-Excellent) were considered
* Responses that had values of 6 (Have Not Used) and 7 (Don't know) were ignored
* All the responses were weighted by the 'finweigh' column as stipulated in the survey data notes
* Only data from 2009-2015 was considered
* Finally all the responses were aggregated across zipcodes and a final **Satisfaction Score** was computed by taking a weighted average of all the scores across categories

### Neighborhood Features

The neighborhood features include:
- a <b>crime</b> index, calculated from the crime density of the area.
- access to <b>schools</b>, both public and private.
- access to <b>restauration</b> services, i.e. number of close restaurants and their respective ratings.
- <b>transportation costs</b>, <b>affordability</b>, <b>poverty</b>, <b>ethnicity</b> indices taken directly from census data.

The crime, schools and restauration indices were created in the following way:
* The index for every tract is a weighted average (by distance) of the tract to the individual instances (school, restaurant or crime): *I(t) ~ &#931; K(d(t, x_i))* where the *x_i* are the coordinates of the instances, *t* the coordinates of the tract, *d* a distance function and *K* a smoothing kernel.
* The indices are then normalized to be between 0 and 100.

### Feature Importances:

* We select a list of features like, Job Prospects, Crime Index, Environment Score, Housing and Transportation prices etc., which can be affected by the government. 

* We aim to find the features which are most important for predicting the satisfaction scores across San Francisco. We do this by using `Random Forests`.

* Random Forests fit a bunch of trees to bootstrapped versions of the sample data and a better fit is obtained by making  successive trees independent of each other. This is done by randomly selecting a subset of features at each node of the tree.

* To compute the `Feature Importances`, the reduction of the error due to each of the features is calculated and the importance of each feature is inferred.

### Conclusions:
* We have compiled data from various sources to understand what drives the well-being of residents in San Francisco. We observed that Housing Costs and Job Prospects are the most important predictors of well-being.

* We also observed that there are certain neighborhoods which perform badly across various types of amenities. But, we also observe that all kinds of amenities do not have the same impact on the well-being and the government can be intelligent in choosing what facilites to improve.

Tools
-----

The project was developed with the Python and JavaScript programming languages.
The deliverable is an interactive document provided in the form of a Jupyter
notebook with advanced interactive visualizations based on leafletjs, bqplot,
d3.js.

Directions for improvement
--------------------------
- Incorporating historical feature and response data will allow building a neighborhood specific model that may better predict the impact of changing a feature of that neighborhood on its well-being.
- Building a GUI using `bqplot` to allow the features to be adjusted visually and which displays the predicted change in well-being for the neighborhood.
- Incorporating Yelp reviews to gauge neighborhood well-being.

Requirements
------------

To be able to run the project the following software is required:

 - Python Scientific Stack
   - [numpy](https://github.com/numpy/numpy)
   - [pandas](https://github.com/pydata/pandas) `>= 0.17.1`
   - [matplotlib](https://github.com/matplotlib/matplotlib) `>= 1.5.1`

 - Jupyter notebook and Interactive Widget Libraries
   - [Jupyter Notebook](https://github.com/jupyter/notebook) `>= 4.2`
   - [ipywidgets](https://github.com/ipython/ipywidgets) `>= 5.0.0`
   - [ipyleaflet](https://github.com/ellisonbg/ipyleaflet) `>= 0.2.0b5`
   - [bqplot](https://github.com/bloomberg/bqplot) `>= 0.6.1`

 - GIS library
   - [geopy](https://github.com/geopy/geopy) `>=1.10`

Geographical Data
-----------------

- `sf_zipcodes.geojson`:

    A GeoJSON file that contains San Francisco zip code level topographical data. Each feature contains an attitude `id` which is the zip code associated with the `Polygon`.

Getting Started
---------------

The main notebook of the study is [Main.ipynb](/notebooks/Main.ipynb).
