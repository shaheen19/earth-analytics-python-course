---
layout: single
title: "Learn to Use NAIP Multiband Remote Sensing Images in Python"
excerpt: "Learn how to open up a multi-band raster layer or image stored in .tiff format in Python using Rasterio. Learn how to plot histograms of raster values and how to plot 3 band RGB and color infrared or false color images."
authors: ['Leah Wasser']
modified: 2018-10-30
category: [courses]
class-lesson: ['multispectral-remote-sensing-data-python']
permalink: /courses/earth-analytics-python/multispectral-remote-sensing-in-python/naip-imagery-raster-stacks-in-python/
week: 7
nav-title: 'Open NAIP Python'
sidebar:
  nav:
author_profile: false
comments: true
course: "earth-analytics-python"
order: 2
topics:
  remote-sensing: ['naip']
  earth-science: ['fire']
  reproducible-science-and-programming:
  spatial-data-and-gis: ['raster-data']
---



{% include toc title="In This Lesson" icon="file-text" %}

<div class='notice--success' markdown="1">

## <i class="fa fa-graduation-cap" aria-hidden="true"></i> Learning Objectives

After completing this tutorial you will be able to:

* Open an RGB image with 3-4 bands in `Python` using `Rasterio`.
<!--* Export an RGB image as a Geotiff using `writeRaster()`.-->
* Identify the number of bands stored in a multi-band raster in `Python`.
* Plot various band composites in `Python` including True Color (RGB), and Color Infrared (CIR) color images.

## <i class="fa fa-check-square-o fa-2" aria-hidden="true"></i> What You Need

You will need a computer with internet access to complete this lesson and the Cold Springs Fire
data.

{% include/data_subsets/course_earth_analytics/_data-cold-springs-fire.md %}
</div>

## Multispectral Imagery in Python

### Introduction to Multi-Band Raster Data

Earlier in this course, you worked with raster data derived from lidar remote sensing
instruments. These rasters consisted of one layer or band and contained 
height values derived from lidar data. In this lesson, you will
learn how to work with rasters containing multispectral imagery data stored within
multiple bands (or layers).

Just like you did with single band rasters, you will use the `rasterio.open()` function to open multi band raster data in `Python`.  

* To import multi-band raster data you will use the `stack()` function.
* If your multi-band data are imagery that you wish to composite into a color image, you can use the `earthpy`
`plotRGB()` function to plot a 3 band raster image.

<figure>
    <a href="{{ site.url }}/images/courses/earth-analytics/raster-data/single-vs-multi-band-raster-data.png">
    <img src="{{ site.url }}/images/courses/earth-analytics/raster-data/single-vs-multi-band-raster-data.png" alt="A raster can contain one or more bands. You can use the
    raster function to import one single band from a single OR multi-band
    raster.">
    </a>
    <figcaption>A raster can contain one or more bands. You can use the
    raster function to import one single band from a single OR multi-band
    raster. Source: Colin Williams, NEON.</figcaption>
</figure>

## What is Multispectral Imagery?

One type of multispectral imagery that is familiar to many of us is a color
image. A color image consists of three bands: red, green, and blue. Each
band represents light reflected from the red, green or blue portions of the
electromagnetic spectrum. The pixel brightness for each band, when composited
creates the colors that you see in an image. These colors are the ones your eyes
can see within the visible portion of the electromagnetic spectrum.

<figure>
    <a href="{{ site.url }}/images/courses/earth-analytics/raster-data/RGB-bands-raster-stack.jpg">
    <img src="{{ site.url }}/images/courses/earth-analytics/raster-data/RGB-bands-raster-stack.jpg" alt="A color image consists of 3 bands - red, green and blue. When
    rendered together in a GIS, or even a tool like Photoshop or any other
    image software, the 3 bands create a color image."></a>
    <figcaption>A color image consists of 3 bands - red, green and blue. When
    rendered together in a GIS, or even a tool like Photoshop or any other
    image software, the 3 bands create a color image.
	Source: Colin Williams, NEON.
    </figcaption>
</figure>

You can plot each band of a multi-band image individually using a grayscale
color gradient. Remember from the videos that you watched in class that the
LIGHTER colors represent a stronger reflection
in that band. DARKER colors represent a weaker reflection.



{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_2_0.png" alt = "A multiband image has more than one layer. You can plot bands individually just like you plotted lidar height rasters earlier in this course.">
<figcaption>A multiband image has more than one layer. You can plot bands individually just like you plotted lidar height rasters earlier in this course.</figcaption>

</figure>





{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_3_0.png" alt = "A color image is just a composite of the red, green and blue bands of the data. Here NAIP data are used to plot a color RGB composite image.">
<figcaption>A color image is just a composite of the red, green and blue bands of the data. Here NAIP data are used to plot a color RGB composite image.</figcaption>

</figure>




#### Each band plotted separately

Note there are four bands below. You are looking at the red, green, blue and Near
infrared bands of a NAIP image. What do you notice about the relative darkness /
lightness of each image? Is one image brighter than the other?



{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_5_0.png" alt = "You can plot each band individually to better look at reflectance values. In python you would usually create this plot using a loop. However the plot_bands function in earthpy will plot all bands for you automatically.">
<figcaption>You can plot each band individually to better look at reflectance values. In python you would usually create this plot using a loop. However the plot_bands function in earthpy will plot all bands for you automatically.</figcaption>

</figure>




You can plot the red, green and blue bands together to create an RGB image. This is
what you would see with our eyes if you were in the airplane looking down at the earth.


## CIR Image

If the image has a 4th NIR band, you can create a CIR (sometimes called false color)
image. In a color infrared image, the NIR band is plotted on the "red" band. Thus vegetation, which reflects strongly in the NIR part of the spectrum, is colored "red". CIR images are often used to better understand vegetation cover and health in an area.


{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_8_0.png" alt = "Near infrared light reflects strongly off of vegetation. When you plot a near infrared band from remote sensing images on the red channel, vegetation is emphasized.">
<figcaption>Near infrared light reflects strongly off of vegetation. When you plot a near infrared band from remote sensing images on the red channel, vegetation is emphasized.</figcaption>

</figure>




## Other Types of Multi-band Raster Data

Multi-band raster data might also contain:

1. **Time series:** the same variable, over the same area, over time.
2. **Multi or hyperspectral imagery:** image rasters that have 4 or more (multi-spectral) or more than 10-15 (hyperspectral) bands.

We will work with time series data later in the semester.

## Work with NAIP data in Python

Now, we have learned that basic concepts associated with a multi-band raster. Next,
let's explore some spectral imagery in `Python` to better understand our study site -
which is the cold springs fire scare in Colorado near Nederland.



### About NAIP:

In this lesson, you will work with NAIP data.

>The National Agriculture Imagery Program (NAIP) acquires aerial imagery during the agricultural growing seasons in the continental U.S. A primary goal of the NAIP program is to make digital ortho photography available to governmental agencies and the public within a year of acquisition.

> NAIP is administered by the USDA's Farm Service Agency (FSA) through the Aerial Photography Field Office in Salt Lake City. This "leaf-on" imagery is used as a base layer for GIS programs in FSA's County Service Centers, and is used to maintain the Common Land Unit (CLU) boundaries. -- USDA NAIP Program

<a href="https://www.fsa.usda.gov/programs-and-services/aerial-photography/imagery-programs/naip-imagery/" target="_blank">Read more about NAIP</a>

NAIP is a great source of high resolution imagery across the United States.
NAIP imagery is often collected with just a red, green and Blue band. However,
some flights include a near infrared band which is very useful for quantifying
vegetation cover and health.

NAIP data access: The data used in this lesson were downloaded from the <a href="https://earthexplorer.usgs.gov/" target="_blank">USGS Earth explorer website. </a>

## Open NAIP Data in Python

Next, you will use NAIP imagery for the Coldsprings fire study area in
Colorado. To work with multi-band raster data you will use the `rasterio` and `geopandas`
packages. You will also use the `spatial` module from the `earthpy` package for raster plotting.

Before you get started, make sure that your working directory is set.


{:.input}
```python
import os
import numpy as np

import matplotlib.pyplot as plt
import matplotlib as mpl

import rasterio as rio
import geopandas as gpd
import earthpy as et
import earthpy.spatial as es

# set working directory
os.chdir(os.path.join(et.io.HOME, 'earth-analytics'))

mpl.rcParams['figure.figsize'] = (10, 10)
mpl.rcParams['axes.titlesize'] = 20
```

To begin, you will use the rasterio open function to open the multi-band NAIP image

`rio.open("path-to-tif-file-here")`

Remember that it is ideal to use a context manager to open raster data in Python.
This ensures that the data connection is properly closed. 

`with rio.open("path-here") as src:`

Where `src` can be whatever variable name you select to store the raster object.

{:.input}
```python
with rio.open("data/cold-springs-fire/naip/m_3910505_nw_13_1_20150919/crop/m_3910505_nw_13_1_20150919_crop.tif") as src:
    naip_csf = src.read()
    naip_csf_meta = src.meta
```

Above you imported a geotiff like you've done before. But this file is different. Notice the shape of the resulting numpy array. How many layers (known as bands) does it have?

{:.input}
```python
naip_csf.shape
```

{:.output}
{:.execute_result}



    (4, 2312, 4377)





Just like you've done before, you can plot a single band in the NAIP raster using `imshow()`. However, now that you have multiple layers or bands, you need to tell `imshow()` what layer you wish to plot. use `arrayname[0]` to plot the first band of the image.


{:.input}
```python
fig, ax = plt.subplots()
ax.imshow(naip_csf[0], cmap='Greys')
ax.set(title="NAIP RGB Imagery - Band 1-Red\nCold Springs Fire Scar",
       xticks=[], yticks=[])
plt.show()
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_17_0.png" alt = "Plot showing band one (red) of the NAIP data from 2015.">
<figcaption>Plot showing band one (red) of the NAIP data from 2015.</figcaption>

</figure>




Or you can use the earthpy function `plot_bands()`. Note that in this lesson, you will first be shown how to use earthpy to plot multiband rasters. The `earthpy` package was developed to make it easier to work with spatial data in `Python`. 

{:.input}
```python
es.plot_bands(naip_csf[0],
              title="NAIP RGB Imagery - Band 1-Red\nCold Springs Fire Scar")
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_19_0.png" alt = "Plot showing band one (red) of the NAIP data from 2015 using the plot_bands() function.">
<figcaption>Plot showing band one (red) of the NAIP data from 2015 using the plot_bands() function.</figcaption>

</figure>




Look closely at the count element in the metadata for your raster. Note that now, the count is 4 rather than 1. This is because you have multiple bands in your raster, one for each 'color' or type of light collected by the camera. For NAIP data you have red, green, blue and near infrared bands. When you worked with the lidar rasters in week 2 your count was 1 as a DSM or DTM is only composed of one band. 


{:.input}
```python
naip_csf_meta
```

{:.output}
{:.execute_result}



    {'driver': 'GTiff',
     'dtype': 'int16',
     'nodata': -32768.0,
     'width': 4377,
     'height': 2312,
     'count': 4,
     'crs': CRS({'proj': 'utm', 'zone': 13, 'ellps': 'GRS80', 'towgs84': '0,0,0,0,0,0,0', 'units': 'm', 'no_defs': True}),
     'transform': Affine(1.0, 0.0, 457163.0,
            0.0, -1.0, 4426952.0)}






<i class="fa fa-star"></i> **Data Tip:** Remember that a tiff can store 1 or more bands. It's unusual to find tif files with more than 4 bands.
{: .notice--success}

### Image Raster Data Values
Next, examine the raster's min and max values. What is the value range?


{:.input}
```python
# view min and max value
print(naip_csf.min())
print(naip_csf.max())
```

{:.output}
    17
    242



This raster contains values between 0 and 255. These values represent degrees of brightness associated with the image band. In the case of a RGB image (red, green and blue), band 1 is the red band. When we plot the red band, larger numbers (towards 255) represent pixels with more red in them (a strong red reflection). Smaller numbers (towards 0) represent pixels with less red in them (less red was reflected). 

To plot an RGB image, we mix red + green + blue values, using the ratio of each. The ratio of each color is determined by how much light was recorded (the reflectance value) in each band. This mixture creates one single color that, in turn, makes up the full color image - similar to the color image that your camera phone creates.

## 8 vs 16 Bit Images

It's important to note that this image is an 8 bit image. This means that all values in the raster are stored within a range of 0:255. This differs from a 16-bit image, in which values can be stored within a range of 0:65,535. 

In these lessons, you will work with 8-bit images. For 8-bit images, the brightest whites will be at or close to 255. The darkest values in each band will be closer to 0.

### Import A Specific Band

You can plot a single band of your choice using numpy indexing. `naip_csf[1]` will access just the second band - which is the green band when using NAIP data. 

{:.input}
```python
# Plot band 2 - green
fig, ax = plt.subplots()
ax.imshow(naip_csf[1], cmap='Greys')
ax.set(title="RGB Imagery - Band 2 - Green\nCold Springs Fire Scar",
       xticks=[], yticks=[])
plt.show()

```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_25_0.png" alt = "Plot showing band two (green) of the NAIP data from 2015.">
<figcaption>Plot showing band two (green) of the NAIP data from 2015.</figcaption>

</figure>




## Rasters and Numpy Arrays - A Review 

Remember that when you import a raster dataset into Python, the data are converted to a numpy array. A numpy array has no inherent spatial information attached to it and is just a matrix of values. This makes processing the data fast.

The spatial information for the raster is stored in a `.meta` attribute. This metadata allows you to export the data as a geotiff or other spatial format. 



### Plot Raster Band Images

Next plot each band in the raster. This is another intermediate step (like plotting histograms) that you might want to do when you first explore and open your data. You will not need this for your homework but you might want to do it to explore other data that you use in your career. Earthpy contains a plot_bands() function that allows you to quickly plot each band individually. 

Similar to plotting a single band, in each band "color", the brightest pixels are lighter in color or white representing a stronger reflectance for that color on that pixel. The darkest pixels are darker to black in color representing less reflectance of that color in that pixel. 

#### Plot Bands Using Earthpy

You can use the earthpy package to plot a single or all bands in your array. 
To use earthpy call:

`es.plot_bands()`

plot_bands() takes the following arguments:

* title: A single title for one band or a list of x titles for x bands in your array
* figsize: a tutple of 2 values representing the x and y dimensions of the image.
* cmap: the colormap that you'd like to use to plot the raster. Default is greyscale
* cols: if you are plotting more than one band you can specify the number of columns in the grid that you'd like to plot. 

{:.input}
```python
titles = ["Red Band", "Green Band", "Blue Band", "Near Infrared (NIR) Band"]

# plot all bands using the earthpy function
es.plot_bands(naip_csf, 
              title=titles,
              figsize=(12, 5), 
              cols=2)
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_28_0.png" alt = "Plot showing all NAIP data bands from 2015.">
<figcaption>Plot showing all NAIP data bands from 2015.</figcaption>

</figure>




<div class="notice--info" markdown="1">
## Optional - How The plot_bands Function is Built


```python

fig, axs = plt.subplots(2, 2, figsize=(20, 10))
for ax, band, the_title in zip(axs.ravel(), naip_csf, titles):
    ax.imshow(band, cmap='Greys')
    ax.set(xticks=[], yticks=[])
    ax.set_title(the_title)
plt.tight_layout()
```
</div>

## Plot RGB Data in Python


Previously you have plotted individual bands using a greyscale color ramp in Python. Next, you will learn how to plot an RGB composite image. This type of image is similar in appearance to one you capture using a cell phone or digital camera. 

<figure>
    <a href="{{ site.url }}/images/courses/earth-analytics/raster-data/RGB-bands-raster-stack.jpg">
    <img src="{{ site.url }}/images/courses/earth-analytics/raster-data/RGB-bands-raster-stack.jpg" alt="A true color image consists of 3 bands - red, green and blue.
    When composited or rendered together in a GIS, or even a image-editor like
    Photoshop the bands create a color image."></a>
    <figcaption>A "true" color image consists of 3 bands - red, green and blue.
    When composited or rendered together in a GIS, or even a image-editor like
    Photoshop the bands create a color image.
	Source: Colin Williams, NEON.
    </figcaption>
</figure>




You can use the Earthpy function called `plot_rgb()` to quickly plot 3 band composite images.
This function has several key arguments including

1. arr: a numpy array in rasterio band order (bands first)
2. rgb: the three bands that you wish to plot on the red, green and blue channels respectively
3. title: OPTIONAL - if you want to add a title to your plot.

Similar to plotting with geopandas, you can provide an `ax=` argument as well to plot your data on a particular matplotlib axis.

{:.input}
```python
es.plot_rgb(naip_csf,
           rgb=[0, 1, 2],
           title="RGB Composite image - NAIP")
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_32_0.png" alt = "RGB plot NAIP data from 2015.">
<figcaption>RGB plot NAIP data from 2015.</figcaption>

</figure>




Optionally, you can also provide the bands that you wish to plot, the title and the figure size.



{:.input}
```python
es.plot_rgb(naip_csf, title="CIR NAIP image",
            rgb=[3, 0, 1],
            figsize=(10, 8))
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_34_0.png" alt = "CIR (Color Infrared) plot of NAIP data from 2015.">
<figcaption>CIR (Color Infrared) plot of NAIP data from 2015.</figcaption>

</figure>




<div class="notice--info" markdown="1">


## <i class="fa fa-pencil-square-o" aria-hidden="true"></i> Optional : How plot_rgb() Works

To render a 3 band, color image in `Python`, you can use the `imshow()` function. 
`Imshow` allows you to identify what bands you want to render in the red, green and blue regions. 

To ensure that the image plots and is scalled correctly, you will use the `bytescale()` function which used to be a part of sci-py / sci-image. Scipy deprecated this function so we've added it to the `earthpy` package for you to use in this course

The code will look something like this:

`ax.imshow(es.bytescale(naip_csf.read())[:3].transpose([1, 2, 0]))`

where

* `ax.imshow()` is the call to plot the image
* `es.bytescale()` ensures that the values in the image are stretched between 0 and 255 which is the range that our monitor can recognize. 

IMPORTANT: when plotting in python, it is important that you TRANSPOSE the data.
The data are read in with the bands FIRST and then the rows and columns. however imshow expects to find the individual bands last. We adjust the dimensions of the data using:

`transpose([])`

Your final code will look like this:

```python
# plot the first 3 bands of the raster (r,g,b bands)
fig, ax = plt.subplots()
ax.imshow(es.bytescale(naip_csf)[:3].transpose([1, 2, 0]))
plt.show()

```

</div>

<div class="notice--warning" markdown="1">


## <i class="fa fa-pencil-square-o" aria-hidden="true"></i> Optional Challenge: Making Sense of Single Band Images

Plot all of the bands in the NAIP image using python, following the code examples above. Compare grayscale plots of band 1 (red), band 2 (green) and band 4 (near infrared). Is the forested area darker or lighter in band 2 (the green band) compared to band 1 (the red band)?

</div>

<!-- We'd expect a *brighter* value for the forest in band 2 (green) than in band 1 (red) because the leaves on trees of most often appear "green" -
healthy leaves reflect MORE green light compared to red light however the brightest values should be in the NIR band.-->



{:.input}
```python
titles = ['red', 'green', 'near\ninfrared']
es.plot_bands(naip_csf[[0, 1, 3]],
              figsize=(10,  5),
              title=titles)
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_37_0.png" alt = "Plot showing the red vs green vs near infrared bands of the NAIP data. Do you notice a difference in brightness between the 3 images?">
<figcaption>Plot showing the red vs green vs near infrared bands of the NAIP data. Do you notice a difference in brightness between the 3 images?</figcaption>

</figure>




## Image Stretch To Increase Contrast

The image above looks pretty good. You can explore whether applying a stretch to
the image improves clarity and contrast.

<figure>
    <a href="{{ site.url }}/images/courses/earth-analytics/raster-data/raster-image-stretch-dark.jpg">
    <img src="{{ site.url }}/images/courses/earth-analytics/raster-data/raster-image-stretch-dark.jpg" alt="When the range of pixel brightness values is closer to 0, a
    darker image is rendered by default. You can stretch the values to extend to
    the full 0-255 range of potential values to increase the visual contrast of
    the image.">
    </a>
    <figcaption>When the range of pixel brightness values is closer to 0, a
    darker image is rendered by default. You can stretch the values to extend to
    the full 0-255 range of potential values to increase the visual contrast of
    the image.
    </figcaption>
</figure>

<figure>
    <a href="{{ site.url }}/images/courses/earth-analytics/raster-data/raster-image-stretch-light.jpg">
    <img src="{{ site.url }}/images/courses/earth-analytics/raster-data/raster-image-stretch-light.jpg" alt="When the range of pixel brightness values is closer to 255, a
    lighter image is rendered by default. You can stretch the values to extend to
    the full 0-255 range of potential values to increase the visual contrast of
    the image.">
    </a>
    <figcaption>When the range of pixel brightness values is closer to 255, a
    lighter image is rendered by default. You can stretch the values to extend to
    the full 0-255 range of potential values to increase the visual contrast of
    the image.
    </figcaption>
</figure>

Below you use the skimage package to contrast stretch each band in your data to make the whites more bright and the blacks more dark. 

In the example below you only stretch bands 0,1 and 2 which are the RGB bands. To begin you

1. preallocate and array of zeros that is the same shape as your numpy array
2. then you look through each band in the image and rescale it

<i class="fa fa-star"></i> **Data Tip:** Read more about image stretch on the <a href="http://scikit-image.org/docs/dev/auto_examples/color_exposure/plot_equalize.html" target = "_blank">scikit-image website</a>.
{: .notice--success }

For convenience we have also built a stretch feature into `earthpy`. You can call it using the stretch argument.

{:.input}
```python
band_indices = [0, 1, 2]

# apply stretch using the earthpy plot_rgb function
es.plot_rgb(naip_csf,
            rgb=band_indices,
            title="RGB NAIP image\n Stretch Applied",
            figsize=(10, 8),
            stretch=True)
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_40_0.png" alt = "Plot showing RGB image of NAIP data with a stretch applied to increase contrast.">
<figcaption>Plot showing RGB image of NAIP data with a stretch applied to increase contrast.</figcaption>

</figure>




What does the image look like using a different stretch? Any better? worse?

In this case, the stretch does increase the contrast in our image. 
However visually it may or may not be what you want to plot. 


## Multiband Raster Histograms

Just like you did with single band rasters, you can view a histogram of each band in your data using matplotlib. Below, you loop through each band or layer in the number array and plot the distribution of reflectance values. 


You can use the `es.hist()` function in earthpy to plot histograms for all bands in your raster. Hist() accepts several arguments including

* `colors=`: a list of colors to use for each histogram
* `title=`: plot titles to use for each histogram

{:.input}
```python
# Create a colors and titles list to use in the histogram, then plot
colors = ['r', 'g', 'b', 'k']
titles = ['red band', 'green band', 'blue band', 'nir band']
es.hist(naip_csf, 
        colors=colors, 
        title=titles, 
        cols=2)
```

{:.output}
{:.display_data}

<figure>

<img src = "{{ site.url }}//images/courses/earth-analytics-python/07-multispectral-remote-sensing-in-python/01-multi-spectral-remote-sensing-python/2018-04-14-multispectral02-open-NAIP-imagery-in-python_44_0.png" alt = "Histogram for each band in the NAIP data from 2015.">
<figcaption>Histogram for each band in the NAIP data from 2015.</figcaption>

</figure>




<div class="notice--info" markdown="1">
## Optional - How The Hist Function is Built

If you want to understand how the hist function works, have a look at the code below. Here you can loop through all of the bands and plot the histogram for each one. 

```python
colors = ['r', 'g', 'b', 'k']
titles = ['red band', 'green band', 'blue band', 'nir band']
fig, axs = plt.subplots(2, 2, figsize=(10, 10), sharex=True, sharey=True)
for band, color, the_title, ax in zip(naip_csf, colors, titles, axs.ravel()):
    ax.hist(band.ravel(), bins=20, color=color, alpha=.8)
    ax.set_title(the_title)
```    
</div>
