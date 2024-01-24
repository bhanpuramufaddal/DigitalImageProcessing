## Correlation and Convolution
Correlation is simply taking an elementwise dot product of a kernel with an image (pixel matrix). 

When you filter an impulse image with an arbitrary kernerl, you get the same kernel inverted. Thus the operation of convolution invertes the pixels regionally.
<img align="centre" src="https://github.com/bhanpuramufaddal/DigitalImageProcessing/assets/46320499/60e1aa6e-d386-42a2-b202-c05cedd82dbb">

Therefore, we preinvert the kernel twixce before performing elementwise dot product. This is called cnvolution.
Here, the kernel is flipped twice (horizontally and vertically) , and then we perform elementwise dot - product.<br>
For example, 

```math
Kernel = \begin{bmatrix}a & b & c \\ d & e & f \\ g & h & i\end{bmatrix} \;\;\; 
Fipped\:Kernel = \begin{bmatrix}i & h & g \\ f & e & d \\ c & b & a\end{bmatrix}
```
<img align="centre" src="https://github.com/bhanpuramufaddal/DigitalImageProcessing/assets/46320499/ade02e58-d557-4cf5-80ba-ea27b6da3c92">

## Image Filters (Correlation)
### Box filter
Convolution with a kernal with all values set to 1.  (Average Pooling)
1. Makes the image smoother.
2. Can be used for Noice reduction.

### Gaussian filter
1. Elements nearest to the original pixel have the greatest influence.
2. As you move away from the centre, weights decrease linearly.
3. Distribution of weights approximates 2d Gaussian function.

<p align="center">
  <img src="https://github.com/bhanpuramufaddal/DigitalImageProcessing/assets/46320499/180fc456-af10-469e-a51f-b85c00f9cfe8">
</p>

<br> Example 3 x 3 Gaussian Filter: <br>

```math
\begin{bmatrix}1 & 2 & 1 \\ 2 & 4 & 2 \\ 1 & 2 & 1\end{bmatrix}
```
<br> When multiplying by this kernel, also devide by $\frac{1}{16}$ for smothing.

### Edge filter
Makes the edges prominent.

<p align="center">
  <img src= "https://github.com/bhanpuramufaddal/DigitalImageProcessing/assets/46320499/f658ba66-09fa-43ae-9387-3638c90614ce">
</p>

#### Horizontal Edge Filters
```math
\begin{bmatrix} -1 & -1 & -1 \\ 0 & 0 & 0 \\ 1 & 1 & 1\end{bmatrix}
```
#### Vertical Edge Filters
```math
\begin{bmatrix} -1 & 0 & 1 \\ -1 & 0 & 1 \\ -1 & 0 & 1\end{bmatrix}
```
### General Properties of Correlation and Convolution
Both correlation and convolution have these 2 properties:
#### Linearity (or Superposition principle):
```math
  I◦(h0 + h1)=I◦h0 +I◦h1
```
#### Shift Invariance
```math
  g(i,j)=h(i+k,j+l) ⇐⇒ (f◦g)(i,j)=(f◦h)(i+k,j+l)
```
In simpler terms, if you shift the input signal by a certain amount $t_0$, 
the output of the convolution operation will also be shifted by the same amount $t_0$.
This property is desirable in many applications, especially in image processing, 
where the location of features in an image should not affect the ability of a convolutional neural network (CNN) to detect those features.

### General Properties of Convolution
#### Commutative
```math
  a∗b=b∗a$,
```
Does not really matter which is the image and which is the kernel.
#### Associative: 
``` math
  a∗(b∗c) = (a∗b)∗c$
```
#### Distributive over addition
```math
  a∗(b+c)=(a∗b)+(a∗c)
``` 
#### Scalars factor out:
```math
  ka∗b=a∗kb=k(a∗b)
``` 
#### Identity
Whewn you convolve a kernel with a unit impulse, you get the kernel back.
```math
  e=[...,0,0,1,0,0,...], \; a∗e=a
```

## Kernal Separability into a and y components.
The time complexity of kernel operations is $k^2$ where k is the size of the kernel.
But if we can separate the kernel into its x and y component, and perform convolution separately among the 2 axis, the time complexity reduces to k (2k operations).

$K = vh^T$, where v, h are 1D kernels, and K is the 2D kernel.

<img align="centre" src="https://github.com/bhanpuramufaddal/DigitalImageProcessing/assets/46320499/9c0d4547-3951-49bb-a32f-e23225604d61">

