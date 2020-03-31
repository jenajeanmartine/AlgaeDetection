## Detecting Algal Blooms 
### Problem Statement/Background
Algae is amazing, it provides much of Earth’s oxygen, it is important in ecosystems, and could provide solutions in clean energy and food systems. However, this project is about Harmful Algal Blooms (HABs), which are large, toxic blooms of algae in the ocean or freshwater, caused by natural circumstances or as a result of human activity (e.g. agricultural fertilizer run-off), and they are responsible for millions of dollars per year in health costs, and damage to mariculture and hospitality industries. 
<br/><br/>
Because these algal blooms can be so severely toxic, public agencies (NOAA) have developed hardcore monitoring systems with regular water testing so that people can be warned when it is not safe to eat seafood or go in the water. A need has been identified for real-time monitoring that can speed up detection and help give fisheries and people more time to avoid/plan for the losses that are associated with such blooms.
<br/><br/>
### Solution
Remote sensing data has become much more accessible in the past couple of decades, enabling exciting new uses. This project focuses on using satellite imagery and machine learning to scan waters from above and identify algal blooms in real time, without having to manually sample and lab test on a micro level. A great model for algae detection paired with other models like ocean currents and temperatures (some of which can also be measured by remote sensing) can forecast when and where algal blooms will occur. This project was completed using Google Earth Engine’s Python API accessed through a Google Colab Notebook (a Google cloud-based Jupyter Notebook type of thing).
<br/><br/>
### Methods
#### Data
This project is a case study in building a classification model with satellite imagery data to detect algae in the ocean off the coast of Florida where there are reliably seasonal algal blooms of K. brevis, also known as red tide, a toxic and costly occurance.  A dataset was obtained from NOAA (https://habsos.noaa.gov/) which includes the geographical coordinates, dates and counts of K. brevis from ~17,000 ocean samples during 2016 and 2017.
#### Feature Creation
To the data was added the feature of a small geometry centered at each geographical point, from which to sample pixels from a satellite image with dates corresponding. For each unique date in the data, there should also be a unique satellite image composite (google earth engine ImageCollection) from which to sample pixels to use as features in a classification model. Latitude and Longitude from the original dataset were used to create columns of Google Earth Engine (GEE) shape and point objects to add compatibility with GEE built-in methods.
<br/><br/>
The data was narrowed down to only include observations of 0 cells/ml and those above 100,000 cells/ml to represent the negative and positive classes (no bloom, bloom) respectively.
<br/><br/>
Due to the time constraints in learning the GEE tooling for this (~2wk) project, a proof of concept model with a simpler set of training data was developed. A narrowed-down dataset including just three consecutive months of data were chosen, October through December of 2016, when there were many high counts of K. brevis. A composite NDVI image from the Sentinel 2 satellite over those dates was obtained and visualized in GEE. That one image was used as the source of pixel feature collection instead of unique images for all dates. Points were used for sampling instead of polygons. A CART model was constructed in GEE and trained with 70% of the narrowed down data and tested with the remainder, yielding an accuracy score of 87.5%. The CART model seems like it could be a good fit for this problem, however the model was not tuned and not much significance can be given to it, as the dataset used consisted of only 619 points with unbalanced classes (with the great majority being in the positive class.) The classification was then mapped over the area of interest to visualize how the model predicts on a continuous image!
### Next Steps
Future steps should include using Chlor_a, NDVI, and possibly other wavelength bands or calculations as features in the same model, and feature collection should be conducted as initially outlined. Also, other models such as Random Forest, CNNs and methods such as PCA could be tested for their effectiveness at algae classification/detection. Problems like surface and bottom reflectance of the ocean, especially near shore, and other possible factors that would confuse such a model should be considered and dealt with in future iterations of this project.
<br/><br/>


