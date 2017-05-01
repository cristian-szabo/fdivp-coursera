## Week 3

### Question 1

Fast Fourier Transform (FFT) speeds up the computation of the Discrete Fourier Transform (DFT) of a signal by compromising the accuracy of the result

- [ ] True
- [x] False

### Question 2

The continuous image x(t1,t2) has the following frequency spectrum. What is the minimum number of samples that should be taken from any 10cm by 10cm square region on the image to avoid aliasing?

![ans2](q2_img1.jpg)

- [ ] 5
- [ ] 25
- [x] 50
- [ ] 100

#### Solution

```
Ω1 = 2 * (100π) rad/m = 200π rad/m (origin is in the image center)
Ω2 = 2 * (50π) rad/m = 100π rad/m

Ω = 2π/T 

Ω1 = 2π/T1
200π rad/m = 2π/T1
T1 = 2π rad / 200π rad/m
T1 = 1 / 100 m = 0.01m = 1cm

Ω2 = 2π/T2
100π rad/m = 2π/T2
T2 = 2π rad / 100π rad/m
T2 = 1 / 50 m = 0.02 m = 2 cm

T1, T2 < 10cm
T = T1 * T2 = 2 cm-sq (total sample rate)
Grid area = 10 cm * 10cm = 100 cm-sq / 2 cm-sq = 50 (minimum number of samples)
```

### Question 3

Imagine you want to decrease the resolution of a 1024×1024 pixel image by a factor of 2 in each direction so that you end up with a 512×512 lower resolution image. Which one of the following procedures should you follow?

- [ ] low-pass filtering of the original image followed by discarding half of the pixels in the resulting image
- [x] low-pass filtering of the original image followed by discarding three quarters of the pixels in the resulting image
- [ ] high-pass filtering of the original image followed by discarding half of the pixels in the resulting image
- [ ] high-pass filtering of the original image followed by discarding three quarters of the pixels in the resulting image

#### Solution

```
Take for example a 4x4 image (16 pixel in total)
Discard all the odd rows and columns
The new image will have a size of 2x2 (4 pixel in total)
Observation: 4 = 16 - 12 = 16 - 16 * 3/4 => three quarters of the pixels 
```

### Question 4

Imagine now that you want to display a low resolution image on a high resolution TV screen. Which one of the following statements is true?

- [ ] This can only be done in the spatial domain where the image is taken.
- [ ] This can only be done in the frequency domain.
- [x] This can be done in the spatial domain.
- [ ] Going from low resolution to high resolution is practically not possible.

### Question 5

x(n1,n2) is defined as x(n1,n2)=(−1)n1+n2 when 0≤n1,n2≤2 and zero elsewhere. Denote by X(k1,k2), where 0≤k1,k2≤2, the DFT of x(n1,n2). What is the value of X(1,2)?

- [ ] 1+j3√
- [ ] 1−j3√
- [x] 4
- [ ] (1+j3√)2

#### Solution

```
img = [1,-1,1; -1,1,-1; 1,-1,1];
fft2(img);
ans;

ans =

   1.0000 + 0.0000i   1.0000 + 1.7321i   1.0000 - 1.7321i
   1.0000 + 1.7321i  -2.0000 + 3.4641i   4.0000 + 0.0000i
   1.0000 - 1.7321i   4.0000 + 0.0000i  -2.0000 - 3.4641i
```

### Question 6

A 4×4 pixel image x(n1,n2) is depicted below. Denote by X(k1,k2) the 4×4 point DFT of x(n1,n2). Calculate X(0,0)

![ans6](q6_img1.jpg)

Answer: 136

#### Solution

```
img = [1,2,3,4; 5,6,7,8; 9,10,11,12; 13,14,15,16];
fft2(img);
ans(1, 1);

ans = 

     136
```

### Question 7

Check all statements that are true regarding the 4×3 point DFT of the image x(n1,n2) shown below

![ans7](q7_img1.jpg)

- [x] X(k1,k2) is real
- [ ] X(1,k2)=X(2,k2) for 0≤k2≤2
- [ ] X(k1,0)=X(k1,2) for 0≤k1≤3
- [ ] X(k1,k2)=X(k2,k1) for 0≤k1,k2≤2
- [x] X(0,0)=6

#### Solution

```
img = [2,1,0,1; 1,0,0,0; 1,0,0,0];
fft2(img);
ans;

ans =

     6     4     2     4
     3     1    -1     1
     3     1    -1     1
```

### Question 8

In this problem you will get hands-on experience with changing the resolution of an image, i.e., down-sampling and up-sampling. Follow the instructions below to finish this problem.

1. Download the original image from [here](q8_img1.jpg). The original image is an 8-bit gray-scale image of width 479 and height 359 pixels. Convert the original image from type 'uint8' (8-bit integer) to 'double' (real number).

2. Recall from the lecture that in order to avoid aliasing (e.g., jagged edges) when down-sampling an image, you will need to first perform low-pass filtering of the original image. For this step, create a 3×3 low-pass filter with all coefficients equal to 1/9. Perform low-pass filtering with this filter using the MATLAB function "imfilter" with 'replicate' as the third argument. For more information about low-pass filtering using MATLAB, refer to the programming problem in the homework of module 2.

3. Obtain the down-sampled image by removing every other row and column from the filtered image, that is, removing the 2nd, 4th, all the way to the 358th row, and then removing the 2nd, 4th, all the way to the 478th column. The resulting image should be of width 240 and height 180 pixles. This completes the procedure for image down-sampling. In the next steps, you will up-sample this low-resolution image to the original resolution via spatial domain processing.

4. Create an all-zero MATLAB array of width 479 and height 359. For every odd-valued i∈[1,359] and odd-valued j∈[1,479], set the value of the newly created array at (i,j) equal to the value of the low-resolution image at (i+12,j+12). After this step you have inserted zeros into the low-resolution image.

5. Convolve the result obtained from step (4) with a filter with coefficients [0.25,0.5,0.25;0.5,1,0.5;0.25,0.5,0.25] using the MATLAB function "imfilter". In this step you should only provide "imfilter" with two arguments instead of three, that was the case in step (1). The two arguments are the result from step (4) and the filter specified in this step. This step essentially performs bilinear interpolation to obtain the up-sampled image.

6. Compute the PSNR between the upsampled image obtained from step (5) and the original image. For more information about PSNR, refer to the programming problem in the homework of module 2. Enter the PSNR you have obtained to two decimal points in the box below.

``` matlab
img_original = imread('original_quiz.jpg');
img_cast = im2double(I);
lpf_3x3 = repmat(1/9, 3);
img_result = imfilter(img_cast, lpf_3x3, 'replicate');
img_ds = img_result(1:2:end, 1:2:end);
[rows columns] = size(img_cast);
img_us = zeros(rows, columns);
for i=1:2:rows;
    for j=1:2:columns;     
        img_us(i, j) = img_ds((i+1)/2, (j+1)/2);
    end;
end;
filter = [0.25,0.5,0.25; 0.5,1,0.5; 0.25,0.5,0.25];
img_us = imfilter(img_us, filter);
psnr(img_us, img_cast);
ans;

ans = 

     28.17
```
