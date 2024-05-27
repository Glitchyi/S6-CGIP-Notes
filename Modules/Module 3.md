### Windows to Viewport Transformations
This is the process of transforming 2D world-coordinate objects to device coordinates. Objects inside the world or clipping window are mapped to the viewport which is the area on the screen where world coordinates are mapped to be displayed.

> [!bug] Important Terminology
> - World Coordinates: This is the cartesian coordinate w.r.t which we define the diagram.
> - Device coordinate: It is the screen coordinate where the objects are to be displayed. 
> - Window: It is the area on the world coordinate selected for display
> - Viewport: It is  the area on the device coordinate where graphics is to be displayed.

In some case the viewport may not be the same size as the windows coordinate, this is where we need to perform windows to viewport transformation.

There are two main steps for this transformation: 
#### Steps
**1:  Window coordinate to normalized coordinate translation.** 
This can be done by the following method

$$
X_{normalised},Y_{normalised} = \dfrac{X_w - X_{wmin}}{X_{wmax} - X_{wmin}}, \dfrac{Y_w - Y_{wmin}}{Y_{wmax} - Y_{wmin}} $$


### Clipping 
When we have to display a large portion of the picture, then not only scaling & translation is necessary, the visible part of picture is also identified. This process is not easy. Certain parts of the image are inside, while others are partially inside. The lines or elements which are partially visible will be omitted.

>[!flask] Applications of clipping:
>- It will extract part we desire.
>- For identifying the visible and invisible area in the 3D or 2D object.
>- For drawing operations.
>- For deleting, copying, moving part of an object.

#### Cohen Sutherland Line Clipping
This is the most popular clipping algorithm

All lines come under any one of the following categories
- Visible: If a line lies within the window, i.e., both endpoints of the line lie within the window. A line is visible and will be displayed as it is.
- Not Visible: If a line lies outside the window, it will be invisible and rejected.
- Clipping Case: If the line is neither visible case nor invisible case. It is considered to be the clipped case. Reject the portion of line that are outside the clipping window and accept portion that are inside the clipping window.

In case of clipping, we need to find the intersecting point of line with window boundary this can be done by finding the point of intersection between the windows boundary lines and the line to be displayed.

This can be done using the formula 
$$X = \dfrac{Y_{wmin}-Y_1}{m}+X_1$$
$$Y = (X_{wmin}-X_1)\cdot{m}+Y_1$$

where $m$ is the slope of the line in question 

Every line endpoint in a picture is assigned a four-digit binary code, called a region code that identifies the location of the point relative to the boundaries of the clipping window. Regions are set up in reference to the boundaries of the clipping window.

--- start-multi-column: ExampleRegion1  
```column-settings  
number of columns: 2  
Border: disabled
shadow:off
Overflow: Hidden
column spacing:0px
```

![[Images/Pasted image 20240527083746.png | 300]]  



--- end-column ---

Every line endpoint in a picture is assigned a four-digit binary code, called a region code that identifies the location of the point relative to the boundaries of the clipping window. Regions are set up in reference to the boundaries of the clipping window.

| Bit 4 | Bit 3 | Bit 2 | Bit 1 |
| ----- | ----- | ----- | ----- |
| Above | Below | Right | Left  |


--- end-multi-column
>[!bug] Steps to Follow
>**Step 1** : Assign a region code for two endpoints of given line.
>
>**Step 2** : If both endpoints have a region code 0000 then given line is completely inside.
>
>**Step 3** : Else, perform the logical AND operation for the region codes of those end points.
>
>⠀⠀⠀**Step 3.1** : If the result is not 0000, then given line is completely outside.
>
>⠀⠀⠀**Step 3.2** : Else line is partially inside.
>
>⠀⠀⠀⠀⠀⠀**Step 3.2.1** : Choose an endpoint of the line that is outside the given rectangle
>
>⠀⠀⠀⠀⠀⠀**Step 3.2.2** : Find the intersection point of the rectangular boundary .
>
>⠀⠀⠀⠀⠀⠀**Step 3.2.3** : Replace endpoint with the intersection point and update the region code.
>
>⠀⠀⠀⠀⠀⠀**Step 3.2.4** : Repeat step 2 until we find a clipped line either trivially accepted or trivially rejected.
>
>**Step 4** : Repeat step 1 for other lines .

#### Sutherland-Hodgeman Polygon Clipping
When clipping a polygon to a window using the Sutherland-Hodgeman algorithm, the following rules apply: if the first vertex is outside and the second is inside, the intersection point with the window boundary and the second vertex are added to the output list (outside to inside). If both vertices are inside, only the second vertex is added (inside to inside). If the first vertex is inside and the second is outside, the intersection point is added (inside to outside). If both vertices are outside, nothing is added.

>[!snail] TLDR
>Just common sense should be fine

![[Images/Pasted image 20240527114817.png]]

