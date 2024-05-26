# Image Enhancement

> [!def] Image Enhancement
> The process of changing the pixel values of an image in order to get more detail/information, usually enhancing an image provides better contrast and a more detailed image as compared to the original.

### Basic Gray Level Transformation

Transformations on an image can be generalized in the following format $$S = T(r)$$
where $S$ is the corresponding pixel in the output image after the transformation $T$ is applied on the original image pixel $r$.

There are 3 basic gray level transformations, they are:

- Linear Transformation
- Log Transformation
- Power-Law Transformation

#### Linear Transformation

Linear transformations include simple operation that are applied to the input image to produce the output image.

**Identity Transformation**
This is a very simple function that just return the same pixel value without any change.$$ S = r$$

```dataviewjs
let path = app.vault.adapter.basePath;//absolute path to your vault
var d3 = require(path+"\\.obsidian\\d3.v7.min.js");
var y = [0,255];
var x = [0,255];
var trace = {
 x: x,
 y: y,
 mode: 'lines',
 type: 'scatter'
};
var data = [trace];
var config;
var layout = {
 margin: {l: 40,r: 40,t: 40,b: 40},
 width: 350,
 height: 350,
  xaxis: {
   font: { family: 'Product Sans, sans-serif' },
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 },
 yaxis: {
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 }
};

window.renderPlotly(this.container, data, layout, config)
```

**Negative Transformation**
The transformation converts an image to its **"negative"** , which is the flipping of all the pixel values, for example white will become black and black will become white vise-versa.
$$S = (L -1) -r$$
Here $L$ is the maximum number of levels the image has, for an 8-bit image this will be $2^8  = 256$, so for an 8-bit image out equation becomes $$S = 255 -r$$

```dataviewjs
let path = app.vault.adapter.basePath;//absolute path to your vault
var d3 = require(path+"\\.obsidian\\d3.v7.min.js");
var y = [255,0];
var x = [0,255];
var trace = {
 x: x,
 y: y,
 mode: 'lines',
 type: 'scatter'
};
var data = [trace];
var config;
var layout = {
 margin: {l: 40,r: 40,t: 40,b: 40},
 width: 350,
 height: 350,
  xaxis: {
   font: { family: 'Product Sans, sans-serif' },
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 },
 yaxis: {
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 }
};

window.renderPlotly(this.container, data, layout, config)
```

#### Logarithmic Transformation

The log transformation are processes of applying a log function to the input pixels. There are mainly two types of log transformations:

**Log Transformation**
By applying the transformation which can be represented as:
$$ S = c \cdot log(r+1 )$$

 > [!bug] Points To Note
>
> - $c$ is an arbitrary constant
> - The input is $r+1$ rather than just $r$ to avoid issues that may arise due to $r=0$ like $log(0)$

The output image results to be a **high contrast image**, this is because the log transformation enhances image contrast by spreading out darker pixel values to make their differences more noticeable while compressing brighter pixel values to reduce their differences.

```dataviewjs
let path = app.vault.adapter.basePath;//absolute path to your vault
var d3 = require(path+"\\.obsidian\\d3.v7.min.js");
var y = [];
var x = [];
for (var i = 0; i <= 255; i++) {
 x.push(i);
 y.push(46.01838514300634798508718005383*Math.log(i));
}
var trace = {
 x: x,
 y: y,
 mode: 'lines',
 type: 'scatter'
};
var data = [trace];
var config;
var layout = {
margin: {l: 40,r: 40,t: 40,b: 40},
 width: 350,
 height: 350,
  xaxis: {
   font: { family: 'Product Sans, sans-serif' },
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 },
 yaxis: {
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 }
};
window.renderPlotly(this.container, data, layout, config)
```

![[Images/Pasted image 20240524214240.png| 300]] ![[Images/Pasted image 20240524214301.png| 300]]

**Inverse Log Transformation**
This is the inverse of the normal log function here, the higher input pixel value, lower output pixel value and as a result a **low contrast output image** is produced.
$$ S = c \cdot log^{-1}(r+1 )$$

```dataviewjs
let path = app.vault.adapter.basePath;//absolute path to your vault
var d3 = require(path+"\\.obsidian\\d3.v7.min.js");
var y = [];
var x = [];
for (var i = 0; i <= 255; i++) {
 y.push(i);
 x.push(46.01838514300634798508718005383*Math.log(i));
}
var trace = {
 x: x,
 y: y,
 mode: 'lines',
 type: 'scatter'
};
var data = [trace];
var config;
var layout = {
margin: {l: 40,r: 40,t: 40,b: 40},
 width: 350,
 height: 350,
  xaxis: {
   font: { family: 'Product Sans, sans-serif' },
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 },
 yaxis: {
  range: [0, 255],
  tickvals: [0, 64, 128, 192, 255],
 }
};
window.renderPlotly(this.container, data, layout, config)
```

![[Images/Pasted image 20240524214240.png| 300]] ![[Images/Pasted image 20240524214356.png|300]]

#### Power Law Transformation

A technique used in computer graphics to enhance the contrast of an image by applying a non-linear transformation to the pixel values.

The transformation is represented as:
$$ S = c \cdot r^\gamma $$

> [!bug] Points To Note
>
> - The parameter $\gamma$ controls the degree of enhancement.
> - $c$ is a constant that scales the output.

The output image results to be either brighter or darker depending on the value of $\gamma$ . This is because when $\gamma < 1$ , the transformation enhances the brightness of the image, making dark regions lighter. Conversely, when $\gamma > 1$, it enhances the darkness, making bright regions darker.

> [!imp] Gamma Correction
> The power law is similar to the log function, but since the value of $\gamma$ is variable, the power law function is much more versatile and is often used to correct contrast for displays, this process is called gamma correction.

```dataviewjs
let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var y1 = [];
var x1 = [];
var y2 = [];
var x2 = [];
var y3 = [];
var x3 = [];
var y4 = [];
var x4 = [];

for (var i = 0; i <= 255; i++) {
    x1.push(i);
    y1.push(46.01838514300634798508718005383 * Math.log(i));
    x2.push(i);
    y2.push(Math.pow(i,2.7182818284590452353602874713527)/13649.422013022317250591579592092);
    x3.push(i);
    x4.push(i);
	var gamma=1;
	var c=1;
    y3.push(Math.pow(i,gamma)*c);
	var gamma=0.6;
	var c=9.175211248758;
    y4.push(Math.pow(i,gamma)*c);
}

var trace1 = {
    x: x1,
    y: y1,
	name:"log",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#1FB442' }
 
};

var trace2 = {
    x: x2,
    y: y2,
	name:"inv log",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#923FDC' }
};

var trace3 = {
	x: x3,
    y: y3,
	name:"γ = 1",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#1F64B4' }
};
var trace4 = {
    x: x4,
    y: y4,
	name:"γ = 0.6",
    mode: 'lines',
    type: 'scatter',
		line: { color: '#1FB4A7' }

};

var data = [trace1, trace4, trace3,trace2];
var config;
var layout = {
    margin: {
        l: 40,
        r: 40,
        t: 40,
        b: 40
    },
    width: 400,
    height: 350,
    xaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    // showlegend: false,

};

window.renderPlotly(this.container, data, layout, config);

```

---
### Contrast Stretching

>[!imp] Piece-wise Linear Transformation
>Rather than using a well-defined function, we use arbitrary user defined transforms.

Contrast Stretching is a piece-wise linear transformation, it is a process that expands the range of intensity levels in an image so that it spans the full intensity range of the recording medium or display device.

An example for a contrast stretching functions is: 

$S(r) = \begin{cases} x \cdot r & \text{if } 0 \leq r \leq a \\ y \cdot (r - a) + c & \text{if } a < r \leq b \\ z \cdot (r - b) + d & \text{if } b < r \leq L-1 \end{cases}$

```dataviewjs
let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var y1 = [0,45];
var x1 = [0,85];
var y2 = [45,210];
var x2 = [85,160];
var y3 = [210,255];
var x3 = [160,255];

var trace1 = {
    x: x1,
    y: y1,
	name:"log",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#1F64B4' }
 
};

var trace2 = {
    x: x2,
    y: y2,
	name:"inv log",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#0084fb' }
};

var trace3 = {
	x: x3,
    y: y3,
	name:"γ = 1",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#1F64B4' }
};

var data = [trace1, trace2, trace3];
var config;
var layout = {
    margin: {
        l: 40,
        r: 40,
        t: 40,
        b: 40
    },
    width: 350,
    height: 350,
    xaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    showlegend: false,

};

window.renderPlotly(this.container, data, layout, config);

```


>[!flask] Intensity Level slicing
This technique is used to highlight a specific range of gray levels in a given image (thresholding). Other levels can be suppressed or maintained – Useful for highlighting features in an image.
>Two basic themes are: 
>- One approach is to display a high value for all gray levels in the range of interest and a low value for all other gray levels. 
>- The second approach, based on the transformation brightens the desired range of gray levels but preserves gray levels unchanged.

---
Approach 1
```dataviewjs
let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var x = [];
var y = [];

for(let i=0; i<255 ;i++){
	x.push(i);
	if(i>150 && i<200){
		y.push(160);
	}else{
		y.push(40);
	}
}

var trace1 = {
    x: x,
    y: y,
	name:"log",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#1F64B4' }
 
};

var data = [trace1];
var config;
var layout = {
    margin: {
        l: 40,
        r: 40,
        t: 40,
        b: 40
    },
    width: 350,
    height: 350,
    xaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    showlegend: false,

};

window.renderPlotly(this.container, data, layout, config);

```
Approach 2
```dataviewjs
let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var x = [];
var y = [];

for(let i=0; i<255 ;i++){
	x.push(i);
	if(i>70 && i<130){
		y.push(190);
	}else{
		y.push(i);
	}
}

var trace1 = {
    x: x,
    y: y,
	name:"log",
    mode: 'lines',
    type: 'scatter',
	line: { color: '#1F64B4' }
 
};

var data = [trace1];
var config;
var layout = {
    margin: {
        l: 40,
        r: 40,
        t: 40,
        b: 40
    },
    width: 350,
    height: 350,
    xaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    showlegend: false,

};

window.renderPlotly(this.container, data, layout, config);
```


#### Histogram Processing

> [!def] Histogram
> A graphical representation that displays the distribution of numerical data through bins or intervals, showcasing the frequency of data points within those ranges.

>[!flask] Applications of Histogram
>It is used to analyze an image. Properties of an image can be predicted by the detailed study of the histogram. 
>- The brightness of the image can be adjusted by having the details of its histogram. 
>The contrast of the image can be adjusted according to the need by having details of the x-axis of a histogram. It is used for image equalization. Gray level intensities are expanded along the x-axis to produce a high contrast image. Histograms are used in thresholding as it improves the appearance of the image. If we have input and output histogram of an image, we can determine which type of transformation is applied in the algorithm

```dataviewjs
let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var x =[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,136,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,152,153,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,169,170,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,186,187,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,203,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,221,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,238,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,254,255];
var y =[40,145,93,255,113,102,21,88,57,26,26,18,12,11,10,10,12,12,12,10,8,8,8,8,7,8,8,7,8,7,7,8,7,7,7,7,7,6,6,7,6,7,6,6,5,6,6,6,5,5,5,5,5,4,5,4,4,4,4,4,4,4,4,4,4,4,4,4,3,4,3,3,3,3,3,3,3,3,3,3,3,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,1,1,2,1,1,1,1,1,1,1,1,2,1,1,1,2,2,2,2,2,2,2,2,2,2,3,3,3,4,3,0,3,4,4,4,4,5,5,5,5,6,6,6,6,6,6,6,6,5,5,5,5,5,5,5,5,5,5,4,5,5,5,5,5,5,5,5,5,5,6,6,6,6,6,6,6,5,5,5,5,5,4,5,5,4,5,4,4,5,5,5,5,4,5,5,5,5,5,5,5,5,5,5,6,5,6,6,6,6,6,6,7,7,7,7,7,6,7,7,7,7,7,6,6,7,7,7,6,6,6,6,5,5,4,4,3,4,3,3,2,3,3,2,2,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0]

const average = arr => arr.reduce( ( p, c ) => p + c, 0 ) / arr.length;
var avg = average(y)

for(let i =0; i<y.length;i++){
	if(y[i]!=avg){
		y[i]= (avg - y[i] )*10
	}
}

var trace1 = {
    x: x,
    y: y,
    type: 'bar',
	line: { color: '#1F64B4' }
 
};

var data = [trace1];
var config;
var layout = {
    margin: {
        l: 40,
        r: 40,
        t: 40,
        b: 40
    },
    width: 350,
    height: 350,
    xaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    showlegend: false,

};

window.renderPlotly(this.container, data, layout, config);
```

##### Histogram Equalization
Histogram Equalization is a computer image processing technique used to improve contrast in images. Histogram equalization is used for equalizing all the pixel values of an image, so that a uniformly flattened histogram is produced. 
#Todo
#### Spatial Filtering

Spatial filtering is a technique used in image processing to modify or enhance an image by manipulating the pixel values based on the values of neighboring pixels. This process involves the application of a filter mask (also known as a kernel, template, or window) that moves across the image, performing operations at each pixel location. Histogram equalization increases the dynamic range of pixel values and makes an equal count of pixels at each level which produces a flat histogram with high contrast image.

> [!bug] Points To Note
>
> - Spatial filtering can be linear or nonlinear.
> - It is used for various purposes such as noise reduction, blurring, sharpening, and edge detection.

##### Smoothing Linear Filters
$$\newcommand{\bm}[1]{\boldsymbol{#1}}$$
Smoothing filters are used to reduce noise and smooth out rapid intensity variations in an image. They are also known as low-pass filters because they allow low-frequency components to pass through while attenuating high-frequency components.

**Average Filter:**
The average filter, also known as the mean filter, replaces each pixel value with the average of the pixel values in its neighborhood. This filter is effective in reducing random noise. This is also referred to as lowpass filters.

The equation for a 3x3 average filter is:
$$\bm{x} = \begin{bmatrix} 1/9 & 1/9 & 1/9 \\1/9 & 1/9 & 1/9 \\ 1/9 & 1/9 & 1/9 \end{bmatrix}$$
or 
$$ g(x, y) = \frac{1}{9} \sum_{i=-1}^{1} \sum_{j=-1}^{1} f(x+i, y+j) $$


**Median Filter:**
The median filter is a nonlinear filter that replaces each pixel value with the median value of the pixel values in its neighborhood. It is particularly effective in removing salt-and-pepper noise while preserving edges.

The process involves:
1. Sorting the pixel values in the neighborhood.
2. Selecting the median value.
3. Replacing the center pixel with the median value.

**Max/Min Filters:**
Max and Min filters are order-statistics filters that replace each pixel value with the maximum or minimum value in its neighborhood, respectively. These filters are useful for enhancing bright or dark regions in an image.

##### Sharpening Linear Filters

Sharpening filters are used to enhance the edges and fine details in an image. They are also known as high-pass filters because they allow high-frequency components to pass through while attenuating low-frequency components.

**First Derivative:**
The first derivative of an image is used to detect edges by highlighting regions with rapid intensity changes. The gradient magnitude is commonly used to measure the strength of edges.

The gradient magnitude can be computed using the following equation:
$$ \Delta f = |Gx| + |Gy|  $$
$$ \nabla = |Gx| + |Gy|  $$
where $Gx$ and $Gy$ are the gradients in the x and y directions, respectively.

**Second Derivative:**
The second derivative is more sensitive to fine details and is used to enhance edges and other discontinuities. The Laplacian operator is a common second-order derivative used in image sharpening.

The Laplacian operator is defined as:
$$ \nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} $$

In discrete form, the Laplacian can be approximated using a convolution mask:
$$ \nabla^2 f(x, y) = f(x+1, y) + f(x-1, y) + f(x, y+1) + f(x, y-1) - 4f(x, y) $$
By applying the Laplacian to an image and then subtracting the result from the original image, we can enhance the edges and fine details.

**Example of a Laplacian Filter:**
$$ \begin{bmatrix}
0 & 1 & 0 \\
1 & -4 & 1 \\
0 & 1 & 0
\end{bmatrix} $$
### Fundamentals of Image Segmentation

>[!def] Image Segmentation
>Image Segmentation is the process by which a digital image is partitioned into various subgroups (of pixels) called Image Objects, which can reduce the complexity of the image, and thus analyzing the image becomes simpler.

#### Similarity Detection 
This fundamental approach relies on detecting similar pixels in an image – based on a threshold, region growing, region spreading, and region merging so does classification, which detects similarity based on a pre-defined (known) set of features.

#### Discontinuity Detection 
This is a stark opposite of the similarity detection approach where the algorithm rather searches for discontinuity. Image Segmentation Algorithms like Edge Detection, Point Detection, Line Detection follow this approach – where edges get detected based on various metrics of discontinuity like intensity, etc.

#### Thresholding

**Simple thresholding (Binary Thresholding)** 
$$g(x,y) = \begin{cases} 1, \text{ if }  f(x,y)  >T \\ 0, \text{ else } f(x,y)<T\end{cases}$$

this is a simple binary thresholding function which converts the pixels into either black or white depending on the Threshold $T$

**Multiple thresholding** 
$$g(x,y) = \begin{cases} a, \text{ if }  f(x,y)  >T_1 \\ b, \text{ if } T_1 <f(x,y)<T_2\\ c, \text{ if } f(x,y)<T_2\end{cases}$$

Here the function converts the output pixels to either $a,b$  or $c$ depending on the thresholds $T_1$ and $T_2$.

>[!bug] Types of thresholding
>- **Global thresholding**: T is constant and applicable over the whole image
>- **Variable/ Local thresholding**: T changes over an image. T at a point (x,y) is a function of the neighborhood of (x,y)
>- **Dynamic / Adaptic thresholding**: T changes over an image. T at any point(x,y) is a function of spatial coordinate (x,y)



#### Region Growing Technique
In the case of the Region growing method, we start with some pixel as the seed pixel
and then check the adjacent pixels.
If the adjacent pixels abide by the predefined rules, then that pixel is added to the
region of the seed pixel and the following process continues till there is no similarity
left. This method follows the bottom-up approach.
In case of a region growing, the preferred rule can be set as a threshold.


#### Region Splitting and Merging Technique
In Region splitting, the whole image is first taken as a single region. If the region does not follow the predefined rules, then it is further divided into multiple regions (usually 4 quadrants) and then the predefined rules are carried out on those regions in order to decide whether to further subdivide or to classify that as a region. The following process continues till there is no further division of regions required i.e every region follows the predefined rules. In Region merging technique, we consider every pixel as an individual region. We select a region as the seed region to check if adjacent regions are similarly based on predefined rules. If they are similar, we merge them into a single region and move ahead in order to build the segmented regions of the whole image.
### Edge Detection

>[!def] Edge detection
>Edge detection is a technique of image processing used to identify points in a digital
image with discontinuities, simply to say, sharp changes in the image brightness. These
points where the image brightness varies sharply are called the edges (or boundaries)
of the image.

---
#### Sobel Edge Detection
The Sobel edge detection operator extracts all the edges of an image, without worrying about the directions. The main advantage of the Sobel operator is that it provides differencing and smoothing effect.

Sobel edge detection operator is implemented as the sum of two directional edges. And the resulting image is a unidirectional outline in the original image. Sobel Edge detection operator consists of 3x3 convolution kernels. $G_x$ is a simple kernel and $G_y$ is rotated by 90°.
$$ \begin{bmatrix}
-1 & 0 & +1 \\
-5 & 0 & +5 \\
-1 & 0 & +1
\end{bmatrix} \space\space\space \begin{bmatrix}
+1 & +5 & +1 \\
0 & 0 & 0 \\
-1 & -5 & -1
\end{bmatrix} $$
These Kernels are applied separately to the input image

#### Prewitt Edge Detection
The Prewitt edge detection operator extracts all the edges of an image, without worrying about the directions. This is similar to Sobel, just that all the values in the kernel are unit values.
$$ \begin{bmatrix}
-1 & 0 & +1 \\
-1 & 0 & +1 \\
-1 & 0 & +1
\end{bmatrix} \space\space\space \begin{bmatrix}
+1 & +1 & +1 \\
0 & 0 & 0 \\
-1 & -1 & -1
\end{bmatrix} $$

#### Robert's Cross Operator
The Roberts cross operator, a simple and quick differential method for edge detection, approximates the gradient of an image by summing the squares of differences between diagonally adjacent pixels, aiming to produce well-defined edges with minimal background noise and edge intensities that closely match human perception.
$$ \begin{bmatrix}
+1 & 0  \\
0 & -1 \\
\end{bmatrix} \space\space\space \begin{bmatrix}
0 & +1 \\
-1 & 0\\
\end{bmatrix} $$
