## Detecting Algal Blooms 
<br/><br/>
### Problem Statement/Background
There are many different kinds of algae. Algae plays an important role in ecosystems. Most significantly for us humans, algae provides much of Earth’s oxygen. Sometimes natural conditions occur that cause a big algal bloom, like warm spots in water. Even iron deposited in the ocean from a big sandstorm can seed an algal bloom. Agricultural run-off can cause algae blooms by adding an injection of fertilizer to waterways. Some algae produce toxic by-products that can have serious negative impacts on human foodsystems and marine life. Blooms of these algae are dubbed Harmful Algal Blooms or “HABs” and are responsible for millions of dollars in health costs, lost crops of shellfish, and lost business in the hospitality/tourism industry. 
<br/><br/>
Because these algal blooms can be so severely toxic, public agencies (NOAA) have developed hardcore monitoring systems with regular water testing so that people can be warned when it is not safe to eat seafood or go in the water. This has been working fairly well for to protect people’s health, but aside from averting recalls and liability,  it doesn’t do much to help the shellfish farmers because by the time they know there is harmful algae in the water, it’s often too late to do anything about it. With an earlier warning, they may be able to take measures to minimize or plan for losses, like for example, harvesting their crop a bit early before the bloom hits.
<br/><br/>
### Solution
Remote sensing data has become much more accessible in the past couple of decades, enabling exciting new uses. This project focuses on using satellite imagery and machine learning to scan waters from above and identify algae blooms in real time, without having to manually sample and lab test on a micro level. A great model for algae detection paired with other conditions like ocean currents and temperatures (some of which can also be measured by remote sensing) can forecast when and where algae blooms will occur.
<br/><br/>
### Methods
This project is a case study in building a classification model with satellite imagery data to detect algae in the ocean off the coast of Florida where there are reliably seasonal algal blooms of K. brevis, also known as red tide, a toxic and costly occurance.  A dataset was obtained from NOAA (https://habsos.noaa.gov/) which includes the geographical coordinates, dates and counts of K. brevis from ~17,000 ocean samples during 2016 and 2017.
<br/><br/>
To the data was added the feature of a small geometry centered at each geographical point, from which to sample pixels from a satellite image with dates corresponding. For each unique date in the data, there should also be a unique satellite image composite (google earth engine ImageCollection) from which to sample pixels to use as features in a classification model. Latitude and Longitude from the original dataset were used to create columns of Google Earth Engine (GEE) shape and point objects to add compatibility with GEE built-in methods.
<br/><br/>
The data was narrowed down to only include observations of 0 cells/ml and those above 100,000 cells/ml to represent the negative and positive classes respectively.
<br/><br/>
Due to time constraints, a proof of concept model with a simpler set of training data was developed. A narrowed-down dataset including just three consecutive months of data were chosen, October through December of 2016, when there were many high counts of K. brevis. A composite NDVI image from the Sentinel 2 satellite over those dates was obtained and visualized in GEE. That one image was used as the source of pixel feature collection instead of unique images for all dates. Points were used for sampling instead of polygons. A CART model was constructed in GEE and trained with 70% of the narrowed down data and tested with the remainder, yielding an accuracy score of 87.5%. The CART model seems like it could be a good fit for this problem, however the model was not tuned and not much significance can be given to it, as the dataset used only consisted of 619 points with unbalanced classes (with the great majority being in the positive class.) The classification was then mapped over the area of interest to visualize how the model predicts on a continuous image!
<br/><br/>
Future steps should include using Chlor_a, NDVI, and possibly other wavelength bands or calculations as features in the same model, and feature collection should be conducted as initially outlined. Also, other models such as Random Forest, CNNs and methods such as PCA could be tested for their effectiveness at algae classification/detection.
<br/><br/>
This project was completed using Google Earth Engine’s Python API accessed through a Google Colab Notebook (a Google cloud-based Jupyter Notebook type of thing).


