### Linear Contrast Stretching
Before the stretching can be performed it is necessary to specify the upper and lower pixel value limits over which the image is to be normalized. 
Often these limits will just be the minimum and maximum pixel values that the image type concerned allows. 
For example for 8-bit graylevel images the lower and upper limits might be 0 and 255. Call the lower and the upper limits a and b respectively.
The simplest sort of normalization then scans the image to find the lowest and highest pixel values currently present in the image.
Call these c and d. Then each pixel P is scaled using the following function:
<br><br>
$P_{out} = (P_{out} - c) × \frac{b - a}{d - c}$ + a
<br>
Values below 0 are set to 0 and values about 255 are set to 255.

