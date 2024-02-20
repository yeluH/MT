## Workflow

### Work_01
- Input data and save to dataframe
- Save location information and transform to proper coordinates system
- Save Google Street View images according to the locations
  - For each location, four images are saved.
    - Heading are 0, 90, 180, 270 separately.
    - Size are 640*640, fov is 120, pitch is 0.
- Using Unfall-Nr to identify each accident, location as well as images.

### Work_02
- Save all GSV images (Google Image View) to a list

### Work_03
- Write functions to automatically generate mask using SAM, and save it into .npy files.
- Run the function to all GSV images and save them with 1/2/3/4 according to heading direction for each locations.

### Work_04
- Load all generated mask .npy files into list and read.
- Add a filtering function to remove total-overlapping(subset) masks and test.

### Work_05
- Label more masks and summarize the statistics of curbs
  #### Work_05_0
    - Label images of first 10 accident locations (in the order of latitude) and do histogram of curbs
  #### Work_05_1
    - Label images of random 10 accident locations and do histogram of curbs
  #### Work_05_2
    - Combine the two labeled dataframes from above work and generate statistics of 7 labelgroups: sky, infrastructure, vegetation, building, means_of_transportation, other, curb and tram_line. (3934 masks labelled including 49 curbs)
  #### Work_05_3
    - Update function to only consider masks which are located in the lower part of the images
    - Add index for geometric attributes, coordinate values of extreme points, including topmost, bottommost, leftmost, rightmost
    - Add more index for spectral features like RGB quantile value and color distance
    - Redo the statistics summary of all variables for 7 labelgroups
    - (Local version and science_app version)
    - Add index for orientation (of fitting ellipse) and angle of rotation (of rotated rectangle) to feature summary
  #### Work_05_4
    - Label more images of random accident locations
      
### Work_06
- Mapping the locations of labelled images
- More statistics
- Add maps of generated random pseudo points

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

### Work_08
- Classification of label groups on the newly updated features summary
  - Unsupervised machine learning
  - Supervised machine learning
- Evaluation of classification by calculating accuracy, precision and recall
- Extraction of curbs
- Find the suitable variables for classification and extraction of curbs

## Issue
- Images and masks are found not matched! (2024.01.09)   <Solved>
