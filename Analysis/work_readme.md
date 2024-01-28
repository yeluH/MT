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
   
## Issue
- Images and masks are found not matched! (2024.01.09)
