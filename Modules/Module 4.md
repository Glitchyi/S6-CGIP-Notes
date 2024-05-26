## Image Processing

>[!def] Image
>An image is defined as a two-dimensional function, $F( x , y )$ where $x$ and $y$ are spatial coordinates, and the amplitude of F at any pair of coordinates $( x, y )$ is called the intensity of that image at that point.

Images can be represented in many forms, generally they are represented as a matrix with the indices specifying the spatial coordinate and the value being the intensity of the pixel at that point. Usually each point in the image is called a **` pixel `**  

Some ways of representing images:
- **Binary Image**: The values of the pixels range from 0 to 1.
- **8 Bit Color Format (Gray Image)**: The values of pixels range from 0 to 255, also sometimes referred to as PGM (Portable Gray Map).
- **16 Bit Color Format**: It is a color image format, with 65,536 different colors in it. 
### Application of Image Processing
Image processing is a very important field of study and has implication in a lot of fields, like: 

**Gamma Ray Imaging**
In nuclear medicine injecting a patient with a radioactive isotope emits gamma rays as its decays. Images of this sort are used to locate sites of bone pathology such as infections or tumors

**Astronomical Observations**
The output images from satellites and observatories need further processing to extract details and also image processing is needed to visualize data from IR imaging, heatmap data and many more.

**X-ray Imaging**
This is used in processes  like medical diagnostics,  Computerized axial Tomography (CT scan) and also in a magnitude of Industrial applications.

**Ultraviolet Imaging**
Ultraviolet imaging is used in lithography, industrial inspection, microscopy, lasers, biological imaging, and astronomical observations.

**Visible and Infrared band Imaging**
Imaging in the visible and infrared bands is utilized in light microscopy, astronomy, remote sensing, industry, and law enforcement (biometrics).

>[!bug] Note
>There are more application and use cases for image processing, like **Forensics & Investigation**, **Machine Learning**, **Entertainment**
### Fundamental Steps of Image Processing
![[Images/Pasted image 20240526112037.png]]

#### **Image Acquisition** 
This is the first step of the fundamental steps of image processing. In this stage, an image is given in digital form. Generally, in this stage, pre-processing such as scaling is done.
#### Image Enhancement 
This is the process of manipulating an image so that the result is more suitable than the original for a specific application. Interesting features of an image is highlighted such as brightness, contrast, removal of noise, sharpening of an image etc. Subjective in nature – vary from application to application.
#### Image Restoration 
This is the stage in which the appearance of an image is improved. Recovering an image that has been degraded. 
#### Color Image Processing 
Color image processing is a famous area because it has increased the use of digital images on the internet. This includes color modeling, processing in a digital domain, etc.
#### Wavelets and Multi-Resolution Processing
Wavelets facilitate wavelet transforms, providing time and frequency information of an image and enabling multi-resolution processing where the image is represented at various degrees of resolution.
#### Compression
Compression is a crucial technique for reducing the storage requirements of an image, especially important for efficient data transmission over the internet.
#### Morphological Processing
Morphological processing in image processing involves a set of non-linear operations that analyze and manipulate image structures based on their shapes, primarily applied to binary images but also extendable to grayscale images.
#### Segmentation
Segmentation is one of the most challenging tasks in digital image processing, requiring significant time to successfully identify and isolate individual objects within an image. ` Ref Module 5 for more info. `
#### Representation and Description
Converting raw pixel data representing the regions or their boundaries. Representation and description stages are crucial for transforming this raw data into a suitable form for computer processing, facilitating further analysis and interpretation.
#### Object Detection
In this stage, the label is assigned to the object, which is based on descriptors.

>[!flask] Points
>- Acquisition
>- Enhancement
>- Restoration
>- Color Processing
>- Wavelets and Multi-Resolution Processing
>- Compression
>- Morphological Processing
>- Segmentation
>- Representation
>- Object Detection

### Components of An image processing System
![[Images/Pasted image 20240526173927.png]]
#### Image Sensors
To acquire digital images, two components are essential: a physical sensor sensitive to the energy emitted by the object being imaged and a digitizer, which converts the sensor's output into digital data.
#### Image Processing Hardware
Specialized image processing hardware includes the digitizer along with additional hardware capable of performing primitive operations such as arithmetic and logic functions in parallel on entire images, enhancing processing efficiency. ( A good example would be dedicated chips on smartphones to enhance images ).
#### Computer
The computer utilized in an image processing system can be a general-purpose one commonly used in daily life, ranging from personal computers to supercomputers. Occasionally, custom computers are employed to attain specific performance levels as needed.
#### Image Processing Software
Image processing software encompasses all mechanisms and algorithms utilized within an image processing system to manipulate and analyze images.
#### Mass Storage
Mass storage in image processing systems, which accommodates the pixels of images during processing and after processing, this is done by providing sufficient capacity for images depending on the some parameters like quality, file size, with digital storage typically categorized into short-term storage for processing, online storage for quick retrieval, and archival storage for less frequent access, all with different formats such as `png`, `jpg` etc.
#### Image Display
Image display in image processing systems primarily utilizes color TVs, monitors, mobile phone displays occasionally incorporating stereo displays, which can be in the form of headgear or normal desktop monitors.
#### Physical Copy Devices
After processing, the image is transferred to a hard copy device, which could be a pen drive or any external ROM device, utilizing laser printers, film cameras, as well as optical and CD-ROM disks for storage.
### Sampling and Quantization
Sampling and Quantization are the processes used in converting analog signals of the light that we can see into digital representations which can than be used for image processing

> Quantization is a lossy compression technique in image processing that reduces the amount of data in an image by compressing a range of values into a single discrete value
 
 >Sampling is the process of converting an analog signal into discrete values, or pixels, at regular intervals of time.
 
 >[!snail] Simply Put
 > - Quantization is dividing the analog in the `y-axis` into specific levels rather than continuous
 > - Sampling is dividing the analog input in the `x-axis` the analog signal into specific time intervals (this doesn't have a big visual difference on the graph)
 
 ---
**Normal Analog Image Input**
 ```dataviewjs
	let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var y1 = [];
var x1 = [];

for (var i = 0; i <= 255; i++) {
    x1.push(i);
    y1.push(2 * Math.sin(i * Math.PI / 180)); // Sine wave 1
}

var trace1 = {
    x: x1,
    y: y1,
    mode: 'lines',
    type: 'scatter',
    name: 'Sine Wave 1',
    line: { color: '#1f77b4' } // Set line color
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
        font: { family: 'inherit' }, // Use the same font as the rest of Obsidian
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [-2, 2], // Adjusted range for sine wave
        tickvals: [-2, -1, 0, 1, 2],
    },
    showlegend: false, // Hide the legend
};

window.renderPlotly(this.container, data, layout, config);
```
**Digitized Image** 
```dataviewjs
let path = app.vault.adapter.basePath; // absolute path to your vault
var d3 = require(path + "\\.obsidian\\d3.v7.min.js");

var y = [];
var x = [];
var quantizedY = [];

for (var i = 0; i <= 255; i++) {
    let sineValue = 2 * Math.sin(i * Math.PI / 180);
    y.push(sineValue);
    x.push(i);
    quantizedY.push(Math.round(sineValue / 0.5) * 0.5); // Quantize the sine value by 0.5
}


var traceQuantized = {
    x: x,
    y: quantizedY,
    mode: 'lines',
    type: 'scatter',
    name: 'Quantized Sine Wave',
    line: { color: '#ff7f0e' } // Set line color for quantized sine wave
};

var data = [ traceQuantized];
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
        font: { family: 'inherit' }, // Use the same font as the rest of Obsidian
        range: [0, 255],
        tickvals: [0, 64, 128, 192, 255],
    },
    yaxis: {
        range: [-2, 2], // Adjusted range for sine wave
        tickvals: [-2, -1, 0, 1, 2],
    },
};

window.renderPlotly(this.container, data, layout, config);
```

Usually the number of quantas (levels) is equal to the number of gray levels in the image.

### Spatial and Gray Level Resolution
>[!def] Spatial Resolution
>Spatial resolution can be defined as the number of independent pixels values per inch.

Some spatial resolution measurements are:

**Dots Per Inch**
DPI measures image clarity and detail in printing, digital displays, and scanning, with higher DPI yielding sharper prints, more vibrant screen images, and higher quality scans.

**Lines Per Inch**
LPI is a printing resolution measurement used in commercial offset printing, indicating how closely spaced the lines in a halftone grid of ink dots are, with a higher LPI signifying greater detail and sharpness.

**Pixels Per Inch**
Pixels per inch (PPI) measures the number of pixels in a digital image or on a screen, indicating the resolution of digital images, videos, displays, and the resolution capacity of cameras and scanners.

>[!def] Gray Level Resolution
>Gray level resolution refers to the predictable or deterministic change in the shades or levels of gray in an image.

Gray level resolution is usual represented as $L$  which can be calculated by $$L = 2^k$$
where $k$ is the number of **Bits Per Pixel** (BPP).

>[!prob] Sample problem 
>**Q**: The spatial resolution of an image is given by 128 X 128. What is its storage requirements if it is represented by 64 gray levels?
>
>**A**: $64=2^6$ 6-bit representation for each grey level. 
>Image size = $128 x128$ 
>*ie* Storage requirements = $128 x128 x6$ bits

### Relationship Between Pixels

The basic relationship between pixels are - neighborhood, adjacency, connectivity

#### **Neighbors of a Pixel**
A pixel p at coordinates $(x,y)$ has four horizontal and vertical neighbors whose coordinates are given by: $(x+1,y)$, $(x-1,y)$, $(x,y+1)$, $(x,y-1)$. This set is called the 4-neighbors of $P$, is denoted by $N_4(P)$.

For the set of coordinates: $(x+1,y+1)$, $(x-1,y+1)$, $(x+1,y-1)$, $(x-1,y-1)$, these are called the four diagonal neighbors of $P$ usually denoted as $N_D(P)$.  

$N_4$ and $N_D$ together are called 8-neighbour of P denoted as $N_8(P)$
$$N_8 N_4 \cup  N_D$$
#### **Adjacency**
Two pixels are connected if they are neighbors, and their gray levels satisfy some specified criterion of similarity.
Types of adjacency/connectivity
1. **4-adjacency**: Two pixels $p$ and $q$ with values from v are 4-adjacent if q is in the set $N_4 (p)$.
2. **8-adjacency**: Two pixels $p$ and $q$ with values from v are 8-adjacent if q is in the set $N_8 (p)$.
3. **M-adjacency (mixed)**: Two pixels $p$ and $q$ with values from $V$ are m-adjacent if $q$ is in $N_4 (p)$ or 
   $q$ is in $N_D (p)$ and the set $N_4 (p)$ ∩ $N_4 (q)$ has no pixel whose values are from $V$.

>[!def] V is the set of all the possible values that can form a connection if they are adjacent

![[Images/Pasted image 20240526173707.png]]
> Here $V = \{1\}$ 

**Mixed adjacency** is a modification of 8-adjacency is introduced to eliminate the ambiguities that often arise when 8-adjacency is used. (eliminate multiple path connection)
#### **Connectivity**
A subset \( S \) of pixels in an image forms a connected set if it comprises only one connected component. Two pixels \( p \) and \( q \) in \( S \) are considered connected if there is a path between them consisting entirely of pixels in \( S \). The set of all pixels connected to a pixel \( p \) in \( S \) is called a connected component of \( S \).

Types of connectivity based on adjacency:
1. **4-connectivity**: Two or more pixels are 4-connected if they are 4-adjacent to each other.
2. **8-connectivity**: Two or more pixels are 8-connected if they are 8-adjacent to each other.
3. **m-connectivity**: Two or more pixels are m-connected if they are m-adjacent to each other.

![[Images/Pasted image 20240526174753.png]]
#### Region
Let R to be a subset of pixels in an image, we call $R$ a region of the image. If $R$ is a connected set. Two regions $R_i$, $R_j$ are said to be adjacent if their union forms a connected set. Regions that are not adjacent are said to be disjoint. Two regions (of 1s) in the figure, are adjacent only if 8-adjacency is used.
#### **Boundary**
The boundary of a region is defined as the set of pixels within the region that have one or more neighbors outside the region. Consider an image with $K$ distinct regions, denoted as $R_k$ where $k$ = 1, 2, 3, $\ldots$, $K$. None of these regions touch the image border. Let ($R_u$ ) represent the union of all ($K$) regions, and let $(R_u)^c$ denote the complement of 
($R_u$) (the complement of a set ( $S$) is the set of points that are not in ( $S$).

We define all the points in ( $R_u$ ) as the foreground and all the points in $(R_u)^c$ as the background of the image. The boundary of a region $( R )$ consists of the pixels in $( R )$ that have at least one neighbor in the background.

>[!snail] Basically..
>The Region and Boundary defined here are very similar to the general senses of those words, and can be written in your own words, just remember to keep the key points.

>[!bug] Spatial Filtering is explained in a bit more detail in Module 5, so explanation skipped here.
### Spatial Domain Operations

**Correlation and Convolution**
These are functions of displacement.
- Correlation: the process of moving a filter mask over the image and computing the sum of products at each location.
- Convolution: the same process as correlation, except that the filter is first rotated by 180 degrees.



>[!note] If the filter mask is symmetric, correlation and convolution yield the same result.
>

Correlation and convolution with images with a filter of size m $\cdot$ n, we pad the image with a minimum of m-1 rows of 0s at the top and the bottom, and n-1 columns of 0s on the left and right. 