## Workflow

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_01
- Input data and save to dataframe
- Save location information and transform to proper coordinates system
- Save Google Street View images according to the locations
  - For each location, four images are saved.
    - Heading are 0, 90, 180, 270 separately.
    - Size are 640*640, fov is 120, pitch is 0.
- Using Unfall-Nr to identify each accident, location as well as images.

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_02
- Save all GSV images (Google Image View) to a list

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_03
- Write functions to automatically generate mask using SAM, and save it into .npy files.
- Run the function to all GSV images and save them with 1/2/3/4 according to heading direction for each locations.

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_04
- Load all generated mask .npy files into list and read.
- Add a filtering function to remove total-overlapping(subset) masks and test.

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_05
- Label more masks and summarize the statistics of curbs
  #### Work_05_0
    - Label images of first 10 accident locations (in the order of latitude) and do histogram of curbs
  #### Work_05_1
    - Label images of random 10 accident locations and do histogram of curbs
      ##### Work_05_1_forthesis
      - For thesis use: generate images of four directions of chosen locations: id 99900060164616, 99900051076121
  #### Work_05_2
    - Combine the two labeled dataframes from above work and generate statistics of 7 labelgroups: sky, infrastructure, vegetation, building, means_of_transportation, other, curb and tram_line. (3934 masks labelled including 49 curbs)
      ##### Work_05_2_original
      - = Work_05_2
      ##### Work_05_2_forthesis
      - For thesis use: generate plots for illustrating color distance 
  #### Work_05_3
    - Update function to only consider masks which are located in the lower part of the images
    - Add index for geometric attributes, coordinate values of extreme points, including topmost, bottommost, leftmost, rightmost
    - Add more index for spectral features like RGB quantile value and color distance
    - Redo the statistics summary of all variables for 7 labelgroups
    - (Local version and science_app version)
    - Add index for orientation (of fitting ellipse) and angle of rotation (of rotated rectangle) to feature summary
      ##### Work_05_3_lo
      - Consider only lower part of the images
  #### Work_05_4
    - Label more images of random accident locations
    - Postponed (because current model is already ok for further analysis)

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$
     
### Work_06
- Mapping the locations of labelled images
- More statistics
- Add maps of generated random pseudo points
  #### Work_06_1
    - Visualize maps of predicted/recogized curbs in both accident and pseudo datasets
  #### Work_06_2
    - Visualize maps of entropy variables(image entropy, whole-scene mask entropy, ground-scene mask entropy)

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_07
- Generate random pseudo points in QGIS using functions:
  - Random points along line (1 per feature)
  - Random extract (6%)
- Load in the generated random pseudo points file (.csv)
- Save Google Street View Images according to locations
  - For each location, four images are saved.
    - Heading are 0, 90, 180, 270 separately.
    - Size are 640*640, fov is 120, pitch is 0.
- Run functions to generate SAM output for gsv_rpf (Google Street View - random pseudo points - filtered).

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_08
- Classification of label groups on the newly updated features summary
  - Unsupervised machine learning
  - Supervised machine learning
- Evaluation of classification by calculating accuracy, precision and recall
- Extraction of curbs
- Find the suitable variables for classification and extraction of curbs
- Three classification models obtained in total:
  - *my_random_forest_1.joblib*: for curb extraction (presence and number)
  - *my_random_forest_2_whole7.joblib*: for entropy calculation of whole scene and pattern index
  - *my_random_forest_3_ground7.joblib*: for entropy calculation of ground scene
  #### Work_08_0
  #### Work_08_1
  #### Work_08_2
    - Update the classification models and generate images for thesis
      ##### Work_08_2_redo0
      ##### Work_08_2_redo1

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_09
- Apply the feature summary functions to images of accident points and pseudo-absence points
  #### Work_09_0_accident
  #### Work_09_1_pseudo
  #### Work_09_2_model
    - Apply the classification model to dataframes of pseudo-absence points
  #### Work_09_3_entropy
    - Write functions to calculate entropy of each direction in each location *(base = default e)*
    - Apply to predicted labelgroup for both accident and pseudo point dataframes
    - Including two entropy indices
      - Entropy for the whole scene
        - 1 curb, 2 infrastructure, 0 building, 3 means_of_transportation, 4 other, 5 sky, 6 vegetation
      - Entropy for the ground scene
        - Using the 1 & 2 label groups from above (just curb and infrastructure)
        - 0 bike lane, 1 curb, 2 ground_sign, 3 manhole, 4 other, 5 pavement, 6 road
      ##### Work_09_3_entropy_redo_correct
      - Correct mistake in chosen test and train sets (choosing new test and train datasets)
  #### Work_09_4_image_entropy
    - Write functions to calculate entropy of images *(base = default e)*
    - Apply to 295×4 images for accident points and 792×4 images for pseudo points
  #### Work_09_5_summary_of_entropy
    - Combine three entropy variables together: image entropy, mask entropy of whole scene, mask entropy of ground scene
      ##### Work_09_5_summary_of_entropy_redo_correct
      - Correct mistake by using corrected classification model to calculate entropy values

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_10
- Preparing for regression analysis
  #### Work_10_0_variable_curb
  - Summarize all the curb-related variables extracted from SAM result
  #### Work_10_1_regression_curb_rp
  - Apply OLS regression model and optimize model and variables
  - For random pseudo points
  #### Work_10_1_regression_curb
  - Apply OLS regression model and optimize model and variables
  - For accident points
  #### Work_10_2_regression_raw 
  - Regression model built with accident data
  - For relationship between accident presence and severity with other conditions:
      - weather/light/road/traffic/drivers/time
  #### Work_10_3_trafficcount
  #### Work_10_3_trafficcount_rp
  #### Work_10_4_variables_tt
  #### Work_10_4_variables_tt_rp
  #### Work_10_5_regression_tt
  - Regression model built with traffic-transport related data
  - For relationship between accident presence and severity with tt variables:
      - Network data: bicycle lanes, bus lanes, motorized vehicles lanes, tram track, road width;
      - Transport data：traffic area, signalized speed limit, right-of-way, red lights, stop signs, pedestrain crossing, junction, complex intersections, public parking spaces
  #### Work_10_5_regression_tt_rp
  #### Work_10_4_regression_comb
  - Regression model built with all variables including curb-infrastructure, raw-condition, traffic-transport.
  #### Work_10_4_regression_comb_rp

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_11 (removed)
(- Build model for accident presence & severity prediction analysis)

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_12
- Result visualization (plot maps)
- Time series analysis
- Build regression model for severity of accident
  - Build OLS regression model for both presence and severity variables
  - Build classification model for presence variables
  - Build prediction model for both presence and severity variables
  #### Work_12_0
  - Prepare koordinates of valid accident points
  #### Work_12_1 & Work_12_1_raster
  - Plot map results
  #### Work_12_2
  - Time series analysis for accident
  #### Work_12_3_crv_rp
  - Merge curb related variables for pseudo points
  #### Work_12_4_regression_allv
  - Among all accident points, build OLS regression model for accident severity, including presence (of person injury, property damage; light injury, severe injury) and value (number of lightly injured person, severely injured person, amount of property damage)
  - Apply random forest classification model for presence variables, presence (of person injury, property damage; light injury, severe injury)
      ##### allv_i
      - Add prediction based on regression model
      - Add evaluation measures for classification model and plot confusion matrix as well as variables' importance
      ##### allv_2
      - Similar to allv_i but reduce number of variables based on their performance in regression model
  #### Work_12_5_regression_allv_gam
  - Build GAM regression model for both presence and severity variables
  - Build prediction model

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

### Work_13
- Build regression model for presence of accident (accident 1, pseudo 0)
  #### Work_13_0_regression_acp
  - Apply OLS regression model
  #### Work_13_1_regression_gam
  - Apply linear gam regression model

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$

## Issues
- Images and masks are found not matched! (2024.01.09)   <Solved>
- Labels for previous classification models (for mask entropy of ground scene) were not all covered in train datasets. (2024.04)  <Solved> 
