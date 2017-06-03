# Week 10

### Question 1

Comparing video compression with image compression, the former utilizes which of the following types of signal redundancy that is not available in the latter

- [ ] spatial redundancy
- [x] temporal redundancy
- [ ] spectral redundancy
- [ ] All of the above

### Question 2

The MPEG video coding standards specify the operations of both the encoder and the decoder.

- [ ] True
- [x] False

### Question 3 

Among the following statements about the H.264 video coding standard, which is (are) correct? Check all that apply.

- [x] H.264 allows prediction from spatial neighbors for intra macroblocks.
- [ ] 16×16 macroblocks are the smallest units for motion estimation in H.264
- [x] The purpose of deblocking filters in H.264 is to remove blocking artifacts introduced in quantization
- [ ] Arithmetic coding is an option for encoding the syntax elements in H.264

### Question 4

A digitized video is to be encoded using the MPEG-1 video coding standard. Assume a frame sequence of IBBPBBPBBPBBI⋯ and that the compression ratio for I, P, and B frames is 0.1, 0.05 and 0.02, respectively. Assume that the video sequence is much longer than 12 frames. What is the approximate average compression ratio for the video? Enter the result to 4 decimal points.

#### Solution

```matlab
(1 * 0.1 + 8 * 0.02 + 3 * 0.05) / 12;

ans = 

      0.0341 % <- Answer
```

### Question 5
 
Consider a video of spatial resolution 1280×720 and frame rate 30 frames per second. Assume 4:2:0 color subsampling, i.e., for every four luma samples there are two corresponding chroma samples. Also assume each sample (being a luma pixel or a chroma pixel) is a 8-bit integer. Without any form of compression, what will be the minimum bit rate required to transmit this video in real time, i.e., without pauses and buffering? (1Mbits/s = 1,024 Kbits/s, and 1 Kbits/s = 1,024 bits/s)

- [x] Around 316.4 Mbits/s
- [ ] Around 31.6 Mbits/s
- [ ] Around 39.6 Mbits/s
- [ ] Around 3.96 Mbits/s

### Question 6

P-frames in an H.264-encoded bit stream may contain both I-macroblocks and P-macroblocks.

- [x] True
- [ ] False

### Question 7

Among the following statements regarding HEVC, which is (are) correct? Check all that apply.

- [x] HEVC is also known as ITU-T H.265.
- [ ] The maximum resolution HEVC can encode is 4096×2160.
- [ ] Motion estimation on 1/4-pixel precision is first introduced in HEVC.
- [ ] Both Variable Length Coding (VLC) and Arithmetic Coding are options for lossless encoding syntax elements in HEVC.

### Question 8

In this problem you will get hands-on experience with encoding video frames. We have created a "mini encoder" in MATLAB that has all (but simplified) components that appear in a modern video encoder.

Download the file directory from here and unzip it into a folder. The file named "week10_main.m" is the entry file, and the file named "block_match.m" performs block-based motion compensation. The two images named "frame_0.jpg" and "frame_1.jpg" represent the reference frame and the target frame, respectively. The target frame is the one that is to be encoded, and the reference frame is where you look for matching blocks. The code is well commented, and it has a clear block-based structure. For each block, the code performs the following operations in order: motion search, DCT of residual, quantization/dequantization, inverse DCT, and reconstruction by motion compensation.

We highly encourage you to go over the code and play around with it. There are several things you can play with, for example, the size of the encoding blocks, and the quantization step size. If interested, you can also look into "block_match.m" and change the error metric (by default the code uses the mean-squared error metric). When you are comfortable with the code, do the encoding with the following parameters: 16*16 blocks and quantization step at 10. Enter below the PSNR value between the reconstructed frame and the original file. Make sure you enter the number to at least 2 decimal points.

#### Solution

```matlab


ans =

  41.44
```
