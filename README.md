# SDL-Optical-Detectors-Assignment
Calibration and analysis of Hubble Space Telescope (WFPC2) and Sentinel-2 imaging data.

## Repository structure

    ├── exercise-1-calibration/             
    │   ├── hst-data/                       
    │   ├── hst-processed/                  
    │   └── hst-calibration-final.ipynb
    ├── exercise-2-sentinel/                 
    │   ├── sentinel-data/                 
    │   ├── sentinel-processed/              
    │   └── sentinel-2-images.ipynb
    └── README.md
    
Each notebook runs from its own folder without changes

## Requirements 
Python with 'numpy', 'matplotlib' , 'astropy`, `pandas` and `rasterio`

## Part 1: HST Calibration 
Calibrates the raw WFPC2 exposures `ubai2505m`, `ubai2507m` and `ubai2508m`:
Follows the following steps :
1. Masking bad pixels 
2. Bias level correction
3. Bias, dark (scaled by exp. time) and flatfield correction
4. Sky subtraction using the median of each chip
5. Photometric calibration to flux and magnitude

Calibrated images are saved to `hst-processed/` as FITS files with pixel, flux and magnitude extensions.
Compared with the science-ready `_c0m_aligned` files, the calibrated images agree with a Pearson correlation of r ≈ 0.99999, with a small systematic offset (~0.8) attributed to differences in sky subtraction.

## Part 2 : Honga-Tonga Analysis 
Analyses Google Earth and Sentinel-2 images to investigate changes in the land area and vegetation cover of Hunga Tonga-Hunga over time.

Google Earth: Land Area 
1. Estimates pixel dimensions using scale bars in the google earth images
2. Converts RGB images to HSV colour space to get land and sea seperate
3. Uses hue histograms to create threshold to define land mask
4. Estimates pixel dimensions using scale bars in the google earth images
5. Calculates land area from the number of pixels classified as land and plots land area as a function of time

Sentinel 2 : Vegetation Cover 
1. Reads in the pixel resolution and image bounds (in degrees)
2. Converts the pixel size to metres using arc length ( s = Rθ), giving 9.36 m × 9.35 m and 87.55 m² per pixel
3. Calculates NDVI = (B8-B4)/(B8+B4) from the NIR (B8) an red (B4) bands
4. Defines vegetation as NDVI > 0.3 and checks the vegetation mask against the NDVI maps
5. Calculates vegetated area from the number of vegetation pixels
6. PLots the vegetated area against time

Vegetated area increases from 0.564 km² (2017) to 0.633 km² (2018) and 0.708 km² (2019), consistent with vegetation spreading onto the new land.

## Outputs
- `exercise-1-calibration/hst-processed/*_calibrated.fits`
- `exercise-2-sentinel/sentinel-processed/google_land_area_vs_time.png`
- `exercise-2-sentinel/sentinel-processed/sentinel_vegetated_area_vs_time.png`
