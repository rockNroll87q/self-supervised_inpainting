# Encoder decoder architecture for Image Completion

Description of the code used in the paper: 

> Svanera, M., Morgan, A. T., Petro, L. S., & Muckli, L. (2021). A self-supervised deep neural network for image completion resembles early visual cortex fMRI activity patterns for occluded scenes. *Journal of Vision*, 21(7), 5-5. ([link](https://jov.arvojournals.org/article.aspx?articleid=2776469))

Visit the [project website](https://rocknroll87q.github.io/self-supervised_inpainting/) for more.

### Encoder/decoder detail

<p align="center">
<kbd>
<img src="./encDec_details.png" width=500"/>  
</kbd>
</p>

Layer shapes:

~~~
(batch_size, 256, 256, 3) 		# input image
(batch_size, 128, 128, 128)
(batch_size, 64, 64, 256)
(batch_size, 32, 32, 512)
(batch_size, 16, 16, 1024)
(batch_size, 8, 8, 1024)
(batch_size, 4, 4, 1024)
(batch_size, 2, 2, 1024)
(batch_size, 1, 1, 1024)
(batch_size, 2, 2, 1024)
(batch_size, 4, 4, 1024)
(batch_size, 8, 8, 1024)
(batch_size, 16, 16, 1024)
(batch_size, 32, 32, 512)
(batch_size, 64, 64, 256)
(batch_size, 128, 128, 128)
(batch_size, 256, 256, 3) 		# output image
~~~

### Training procedure

<p align="center">
<kbd>
<img src="./training_scheme.png"/>  
</kbd>
</p>

## Models

* grayscale trained model: [link](https://cloud.psy.gla.ac.uk/index.php/s/QNqUBvLDFwWOao7)
* RGB trained model: [link](https://cloud.psy.gla.ac.uk/index.php/s/ou5cmJ20GyqHcFm)


## Requirements

`Tensorflow 1.x`


## Usage

To train the model:

~~~~
python enc_dec_activExtract.py \
  --mode train \
  --output_dir /path/where/model/is/saved/ \
  --max_epochs 10 \
  --ngf=128 --ndf=128 \
  --input_dir /path/to/training/imgs/ \
  --which_direction BtoA \
  --batch_size 10 \
  --out_activations_path /path/to/activations/folder/ \
  --gpu_device 0
~~~~

To test the model and save activations:

~~~~
python enc_dec_activExtract.py \
  --mode test \
  --output_dir /path/to/save/dir/ \
  --input_dir /path/to/testing/imgs/ \
  --out_activations_path /path/to/activations/folder/ \
  --checkpoint /path/where/model/is/saved/ \
  --gpu_device 0
~~~~


## Authors

[Michele Svanera](https://www.michelesvanera.org/)


## Citation

If you find this code useful in your research, please consider citing the original work and our paper:

```
@InProceedings{Isola_2017_CVPR,
author = {Isola, Phillip and Zhu, Jun-Yan and Zhou, Tinghui and Efros, Alexei A.},
title = {Image-To-Image Translation With Conditional Adversarial Networks},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {July},
year = {2017}
}
```

```
@article{svanera2021,
    author = {Svanera, Michele and Morgan, Andrew T. and Petro, Lucy S. and Muckli, Lars},
    title = "{A self-supervised deep neural network for image completion resembles early visual cortex fMRI activity patterns for occluded scenes}",
    journal = {Journal of Vision},
    volume = {21},
    number = {7},
    pages = {5-5},
    year = {2021},
    month = {07},
    issn = {1534-7362},
    doi = {10.1167/jov.21.7.5},
    url = {https://doi.org/10.1167/jov.21.7.5},
    eprint = {https://arvojournals.org/arvo/content\_public/journal/jov/938547/i1534-7362-21-7-5\_1626237272.06066.pdf},
}
```
