# Land Cover Classification and Change Detection with NASA HLS Imagery in R

# Project Overview

This project uses **R/RStudio** and **NASA Harmonized Landsat and Sentinel-2 (HLS)** satellite imagery to classify land cover and analyze **land cover and land use change (LCLUC)** over time. The workflow follows methods introduced through **NASA ARSET (Applied Remote Sensing Training)**, which focuses on practical remote sensing techniques for environmental analysis using Earth observation data.

A major part of this project was learning **R** for the first time. Early challenges included understanding RStudio project structure, package setup, file paths, and working with large raster datasets. Over time, this became easier by connecting R workflows to concepts already familiar from Git Bash and repository-based organization. Using structured scripts and version-controlled project workflows helped build confidence while working with geospatial data.

## Tools and Packages

This project was built in **R/RStudio** using the following main packages:

- `randomForest`
- `randomForestExplainer`
- `tidyverse`
- `terra`
- `tidyterra`
- `patchwork`

A fixed seed was also used for reproducibility:

```r
set.seed(20260226)
```

## Raster Data Structure

The HLS imagery was loaded as a SpatRasterCollection containing two raster datasets, representing two years of imagery for the same study area.

The raster collection summary shows:

```r
- Class: SpatRasterCollection
- Length: 2
- Rows: 3660, 3660
- Columns: 3660, 3660
- Layers: 13, 13
- Extent: 799980, 909780, -309780, -199980
- CRS: WGS 84 / UTM zone 21N (EPSG:32621)
```

The important things to notice are:

- The collection has a length of 2, corresponding to our two years of data
- Both years have the same number of rows and columns
- Both years have the same number of layers or bands

This consistency is important because it allows the rasters to be compared more directly across time for classification and change detection. We can also create RGB maps of the data for both years and plot them side by side using the patchwork syntax.

## RGB Visualization

Because both raster datasets share the same structure, RGB maps can be created for each year and displayed side by side. This provides a quick visual comparison of the study area before classification begins.

##  RGB preview of both years:

<img width="771" height="416" alt="arset1" src="https://github.com/user-attachments/assets/2f46080a-b641-434d-86f4-3f682c7fe6e4" />

Example plotting section:

# Example placeholder for RGB plotting
# plotRGB(hls[[1]], r = 4, g = 3, b = 2, stretch = "lin")
# plotRGB(hls[[2]], r = 4, g = 3, b = 2, stretch = "lin")

# Part 1: Unsupervised Classification

## K-Means Clustering

It is very simple to implement K-means clustering on our HLS data. Since this is an unsupervised classification method, we do not need to provide any training data. Instead, we only need to specify the number of cluster centers.

Testing different values for centers helps show how the landscape can be split into broader or more detailed spectral groups depending on the classification goal.

 K-means clustering will attempt to make any arbitrary number of class splits
 
```r
- km2 <- k_means(hls[1], centers = 2)
- km3 <- k_means(hls[1], centers = 3)
- km4 <- k_means(hls[1], centers = 4)
- km5 <- k_means(hls[1], centers = 5)
```
## Interpreting the K-Means Results

Running K-means with different values for centers helps build understanding of:

- how unsupervised classification works in remote sensing
- how spectral similarity drives grouping
- how the number of clusters affects map interpretation
- how multiple classification outputs can be compared visually

This step provides a useful foundation before moving into supervised classification methods.


# Part 2: Supervised Classification and Change Detection

The second stage of the project expanded into supervised classification and change detection.

This part included:

- reviewing classification methods in more depth
- learning how training data is used in supervised models
- building and interpreting a K-Nearest Neighbor (KNN) model
- building and interpreting a Random Forest model
- applying classification models across different dates
- comparing classified outputs over time
- creating a change matrix
- mapping land cover and land use changes

These steps helped show where land cover changed and how classification results can support environmental monitoring and geospatial decision-making.


Learning Outcomes

This project strengthened practical skills in:

- R and RStudio
-  Git-connected workflows
- remote sensing
- geospatial raster handling
- unsupervised classification
- supervised classification
- land cover mapping
- change detection
- interpreting classification model outputs
- translating technical analysis into environmental insights

Overall, this project provided hands-on experience with NASA satellite imagery and demonstrated how remote sensing workflows can be used to study land cover patterns and changes over time.

# Conclusion

This notebook documents a practical remote sensing workflow for working with HLS imagery in R. It combines raster handling, classification methods, and temporal comparison to support land cover analysis and land use change assessment.
