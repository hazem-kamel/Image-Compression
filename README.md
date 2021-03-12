# Image-Compression
## Introduction
A fast Fourier transform (FFT) is an algorithm that computes the discrete Fourier
transform (DFT) of a sequence, or its inverse (IDFT). Fourier analysis converts a
signal from its original domain (often time or space) to a representation in the
frequency domain and vice versa.

<img src="https://www.researchgate.net/profile/Nuwan_Kuruwitaarachchi/publication/323281289/figure/fig6/AS:701217198059529@1544194616847/Fast-Fourier-Transformation-2-Fast-Fourier-Transformation-To-increase-the-performance.ppm">

## Project Description
As most of the signal processing application, our showcase project implements something kind of simple although very impressive: image compression using FFT.
If we consider, for instance, a 10 by 10 pixels picture we know that all the possible black & white images obtainable are 2^100 (each pixel can, independently from the others, be black or white). Among this huge amount of possible states of our picture (something like 10^30) only a very tiny portion of them is something that makes sense for human eyes. In other words, by picking a random image among all those images there is a very high probability that the picture looks like random noise. One important point to describe before explaining the application, is that it is true, for “real world” images, that the most of the frequency values of a 2-D Fourier transform of an image are very close to zero. The two facts explained above are described by the so-called sparsity representation principle for images.
Image compression saves storage memory in our PCs by exploiting the sparse representation principle.
The steps done in our implementation of image compression through FFT are explained:
* The image that will be compressed is loaded into the program
* The size of the image is shown just to compare it with what will be the compressed image size
* The image is converted to a grayscale image (compressing a colour image would need to work on the 3 RGB layers instead)
* The 2-D FFT algorithm is applied to the gray scale image in order to have the possibility to take a close look to each frequency of the image
* The amplitudes of the frequencies are stored into a vector and sorted descendingly to determine the highest frequencies that affects and creates our image hence which frequencies are essential for the image to be reconstructed again removing the least frequencies to save size and in the same time have the same image.
* Four different percentages of the frequencies to be kept in our new generated image are defined (10%,5%,1%,0.3%) as parameters upon which the size and quality of the new compressed image will depend on and for each of those the following operations are applied:
    1. The corresponding threshold value is computed.
    2. We use the threshold to truncate all the frequencies which have an amplitude value below it so we only keep the highest values needed
        to display the image with the required percantage.
    3. By multiplying the transformed image with the small indices
    4. The resulting image is inverse-fast-Fourier transformed and displayed
    5. A new folder for the compressed images are created in the same directory of the code file , images are then saved there with the percantage used as a name.



The final result is that we got different images really close to the old one that are actually
lighter since some of the frequencies have been truncated. \
Unfortunately, this technique doesn’t work very well for every kind of picture: for example, 
we experience bad performance in “fine grained” textures like grass, human hair, animal fur and all this kind of patterns which actually require an high number of pixels to be well represented.

## Original image (4,7 MB)
![mountain](/uploads/77ff187f4f3b2320c7be23e9bdbdc7f1/mountain.jpg)

## Compressed image [10%] (1,9 MB)
![compressed_10.0_](/uploads/b97fc013c4314b79e17113fd199ac400/compressed_10.0_.jpg)
