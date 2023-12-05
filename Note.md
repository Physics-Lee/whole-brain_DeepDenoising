原理：暂时跳过

功能：recovering high SNR calcium traces from low SNR videos

想要应用它需要的步骤

* step1: 配一模一样的环境
  * python: 3.5
    * ok
  * tensorflow 1.6.0
    * ok
  * **CUDA v9.0**
    * 我的老电脑的显卡和驱动版本是可以的
    * 我的新电脑在2022春装过一个v11的CUDA
  * **cudnn-9.0-windows10-x64-v7.6.4.38**
    * 同上
* step2: 跑例子
* step3: 跑lrh的数据

# Train on new dataset

* To train network on new data, pairs of **noisy** i.e. low SNR images (acquired at low laser power or small exposure time conditions) and **clean** i.e. high SNR images (acquired at high laser power or long exposure time conditions) are needed.
* size: 512 x 512 x d
  * d is number of images in stack
  * For other image sizes, either resize images first or channel dimensions need to be changed in architecture files in `cnn_archs` folder.
* organise the folder
* Run `python train.py -h` to see usage and input arguments.
* Once training is finished a folder named `run_unet_fixed_l1_mp0_m2D_d1_1_[tsize]` will be created in `Results` folder. 

# Denoise calcium activity recordings

* organise the folder
* Run `python inference.py -h` to see usage and input arguments.
* Once denoising is finished, output folders `/vid1/pred_run_unet_fixed_l1_mp0_m2D_d1_1_[tsize]` and `/vid2/pred_run_unet_fixed_l1_mp0_m2D_d1_1_[tsize]` will be created.

# Denoise independent images

~

# paper

带着问题去看

他们的high SNR怎么获得的？

* 同时用low SNR和high SNR拍摄的

tradeoff指什么？

* exposure time大，SNR大，但是会有motion artifacts。
  * 现在通常用的exposure time对应3–6 volumes/s
* laser power大，SNR大，但是会导致光漂白、光毒性
  * 光漂白：激发光的光强超过某一阈值后，荧光蛋白不会发射发射光。背后的原理：可能是过强的激发光改变了荧光蛋白的结构。

* 若要对整个动物拍照，需要FOV大，从而需要放大率小、laser power大，后者会加剧光漂白。

**PS：咱们实验室用的应该是high SNR？？？**
