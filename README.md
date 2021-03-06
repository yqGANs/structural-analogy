# Structural-analogy from a Single Image Pair

Pytorch implementation for the paper "Structural-analogy from a Single Image Pair".

Abstract: The task of unsupervised image-to-image translation has seen substantial advancements in recent years through the use of deep neural networks.
Typically, the proposed solutions learn the characterizing distribution of two large,
unpaired collections of images, and are able to alter the appearance of a given
image, while keeping its geometry intact. In this paper, we explore the capabilities of neural networks to understand image structure given only a single pair
of images, A and B. We seek to generate images that are structurally aligned:
that is, to generate an image that keeps the appearance and style of B, but has
a structural arrangement that corresponds to A. The key idea is to map between
image patches at different scales. This enables controlling the granularity at which
analogies are produced, which determines the conceptual distinction between
style and content. In addition to structural alignment, our method can be used
to generate high quality imagery in other conditional generation tasks utilizing
images A and B only: guided image synthesis, style and texture transfer, text translation as well as video translation.

For more details, please refer to the [Project Webpage](https://sagiebenaim.github.io/structural-analogy/).

<img src="readme_imgs/teaser.jpg" width="500px">

### Applications
<img src="readme_imgs/results.jpg" width="1500px">

### Video Translation
<img src="readme_imgs/volcano.gif" width="400px">
<img src="readme_imgs/birds.gif" width="400px">

## Code:

### Prerequisites:
Python 3.7, Pytorch 1.4.0, argparse, Pillow 7.0.0, Scipy 1.4.1, skimage 0.16.2, numpy

### Structural Analogy:
You can train using the following command:
```
python train.py --input_a ./images/208.jpg --input_b ./images/209.jpg --gpu_id 0 --out ./output0/ --beta 10.0 --alpha 1.0
```
For other images, just replace input_a and input_b.

In many cases it is possible to improve results quality using the one of the following hyperparameter change:
```
--beta 10.0
```
```
--min_size 25
```

### Refinement
In some cases, the quality of the result can be improved using refinement. You can refine your results using [SinGAN](https://webee.technion.ac.il/people/tomermic/SinGAN/SinGAN.htm) in the following way:
Let "ab.png" the image that we want to refine using the original image "b.png" (i.e. "ab.png" should have the same patch distribution as "b.png").
First clone SinGAN repository
```
git clone https://github.com/tamarott/SinGAN
```
Then train a SinGAN network with "b.png" as input
```
python main_train.py --input_dir ./ --input_name b.png
```
You can refine using the command:
```
python paint2image.py --input_dir ./ --input_name b.png --ref_dir ./ --ref_name ab.png --paint_start_scale 4
```
Where paint_start_scale is a hyperparameter, and it is recommended to try several values.

More details about SinGAN implementation can be found at the [repository](https://github.com/tamarott/SinGAN).

### Sketch to Image:
Soon

### Text Transfer:
```
python train.py --input_a ./images/108.png --input_b ./images/109.png --gpu_id 0 --out ./output3/ --beta 10.0 --alpha 1.0 --min_size 25
```
### Style Transfer:
Soon

### Texture Transfer:
```
python train.py --input_a ./images/8.png --input_b ./images/9.png --gpu_id 0 --out ./output2/ --beta 10.0 --alpha 1.0
```

### Video Translation:


## Citation
If you found this work useful, please cite.

## Contact
For further questions, ron.mokady@gmail.com or sagiebenaim@gmail.com.

## Acknowledgements
This implementation is heavily based on https://github.com/tamarott/SinGAN.




