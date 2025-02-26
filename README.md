# ResShift: Efficient Diffusion Model for Image Super-resolution by Residual Shifting

[Zongsheng Yue](https://zsyoaoa.github.io/), [Jianyi Wang](https://iceclear.github.io/), [Chen Change Loy](https://www.mmlab-ntu.com/person/ccloy/) 

[Paper](https://arxiv.org/abs/2307.12348)

<a href="https://colab.research.google.com/drive/1CL8aJO7a_RA4MetanrCLqQO5H7KWO8KI?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="google colab logo"></a> ![visitors](https://visitor-badge.laobi.icu/badge?page_id=zsyOAOA/ResShift) 
[![Replicate](https://replicate.com/cjwbw/resshift/badge)](https://replicate.com/cjwbw/resshift)

:star: If ResShift is helpful to your images or projects, please help star this repo. Thanks! :hugs: 

---
>Diffusion-based image super-resolution (SR) methods are mainly limited by the low inference speed due to the requirements of hundreds or even thousands of sampling steps. Existing acceleration sampling techniques inevitably sacrifice performance to some extent, leading to over-blurry SR results. To address this issue, we propose a novel and efficient diffusion model for SR that significantly reduces the number of diffusion steps, thereby eliminating the need for post-acceleration during inference and its associated performance deterioration. Our method constructs a Markov chain that transfers between the high-resolution image and the low-resolution image by shifting the residual between them, substantially improving the transition efficiency. Additionally, an elaborate noise schedule is developed to flexibly control the shifting speed and the noise strength during the diffusion process. Extensive experiments demonstrate that the proposed method obtains superior or at least comparable performance to current state-of-the-art methods on both synthetic and real-world datasets, *even only with 15 sampling steps*. 

## Update
- **2023.07.31**: Add Colab demo <a href="https://colab.research.google.com/drive/1CL8aJO7a_RA4MetanrCLqQO5H7KWO8KI?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="google colab logo"></a>.  
- **2023.07.24**: Create this repo.

## Requirements
* Python 3.9.16, Pytorch 1.12.1, [xformers](https://github.com/facebookresearch/xformers) 0.0.20
* More detail (See [environment.yml](environment.yml))
A suitable [conda](https://conda.io/) environment named `ResShift` can be created and activated with:

```
conda env create -f environment.yaml
conda activate ResShift
```

## Applications
### :point_right: Real-world image super-resolution
[<img src="assets/0015.png" height="324px"/>](https://imgsli.com/MTkzNzgz) [<img src="assets/0030.png" height="324px"/>](https://imgsli.com/MTkzNzgx)

[<img src="assets/frog.png" height="324px"/>](https://imgsli.com/MTkzNzg0) [<img src="assets/dog2.png" height="324px">](https://imgsli.com/MTkzNzg3)

[<img src="assets/cat.png" height="252px"/>](https://imgsli.com/MTkzNzkx) [<img src="assets/Lincon.png" height="252px"/>](https://imgsli.com/MTkzNzk5) [<img src="assets/oldphoto6.png" height="252px"/>](https://imgsli.com/MTkzNzk2) 


## Inference
#### :tiger: Real-world image super-resolution
```
CUDA_VISIBLE_DEVICES=gpu_id python inference_resshift.py -i [image folder/image path] -o [result folder] --task realsrx4 --chop_size 512
```
#### :lion: Bicubic image super-resolution
```
CUDA_VISIBLE_DEVICES=gpu_id python inference_resshift.py -i [image folder/image path] -o [result folder] --task bicsrx4 --chop_size 512
```

## Training
#### :turtle: Prepare data
Download the training data and add the data path to the config file (data.train.params.dir_path or data.train.params.txt_file_path). To synthesize the testing dataset utilized in our paper, please refer to these [scripts](./scripts/).
* Real-world and Bicubic image super-resolution: [ImageNet](https://www.image-net.org/) and [FFHQ](https://github.com/NVlabs/ffhq-dataset) (resized to 256x256) 
#### :dolphin: Real-world Image Super-resolution
```
CUDA_VISIBLE_DEVICES=0,1,2,3 torchrun --standalone --nproc_per_node=4 --nnodes=1 main.py --cfg_path configs/realsr_swinunet_realesrgan256.yaml --save_dir [Logging Folder] --steps 15
```
#### :whale: Bicubic Image Super-resolution
```
CUDA_VISIBLE_DEVICES=0,1,2,3 torchrun --standalone --nproc_per_node=4 --nnodes=1 main.py --cfg_path configs/bicubic_swinunet_bicubic256.yaml --save_dir [Logging Folder]  --steps 15
```

## License

This project is licensed under <a rel="license" href="https://github.com/sczhou/CodeFormer/blob/master/LICENSE">NTU S-Lab License 1.0</a>. Redistribution and use should follow this license.

## Acknowledgement

This project is based on [Improved Diffusion Model](https://github.com/openai/improved-diffusion), [LDM](https://github.com/CompVis/latent-diffusion), and [BasicSR](https://github.com/XPixelGroup/BasicSR). We also adopt [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) to synthesize the training data for real-world super-resolution. Thanks for their awesome works.

### Contact
If you have any questions, please feel free to contact me via `zsyzam@gmail.com`.
