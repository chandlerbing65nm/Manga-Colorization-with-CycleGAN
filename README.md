<p align="center">
  <img 
    src="https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/docs/banner.png?raw=true"
  >
</p>

<div align="center">

  <a href="">![last commit](https://img.shields.io/github/last-commit/chandlerbing65nm/Manga-Colorization-with-CycleGAN)</a>
  <a href="">![repo size](https://img.shields.io/github/repo-size/chandlerbing65nm/Manga-Colorization-with-CycleGAN)</a>
  <a href="">![watchers](https://img.shields.io/github/watchers/chandlerbing65nm/Manga-Colorization-with-CycleGAN?style=social)</a>

</div>

<h4 align="center">Colorizing Black&White Japanese Manga using Generative Adversarial Network.</h4>

<p align="center">
  <img 
    src="https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/docs/demo-gif.gif?raw=true"
  >
</p>

---

# About the Project
![personal](https://img.shields.io/badge/project-chandlertimmdoloriel-red?style=for-the-badge&logo=appveyor)

Japanese manga is popular in all ages and all countries. Anime like One Piece, Naruto, Bleach are products of great authors who write manga as their career. However, japanese manga are released as black-and-white and for someone new to reading manga, it may be difficult to imagine or follow the story along the pages. Most of the time, these manga are remained black-and-white by the authors until anime debut with just few pages colored. It is also time-consuming to manually color because every single page contains many panels along with different scenes, acts, and characters. Inspired with this problem, I created an automatic colorization program using artificial intelligence to automate the coloring processes of japanese manga.

## Dataset
There is no readily availble dataset for manga colorization, so I have to scrap manga pages as PNG images from fan-made websites containing colored and black-and-white chapters. I choose three manga titles to gather data, these are [One Piece](https://ww9.readonepiece.com), [Black Clover](https://ww7.readblackclover.com), and [My Hero Academia](https://ww7.readmha.com/). I used these noteboks to scrap the manga pages each chapter: [Notebook-1](https://www.kaggle.com/code/chandlertimm/web-scrapping-black-clover-manga) for Black Clover and [Notebook-2](https://www.kaggle.com/code/chandlertimm/web-scrapping-manga) for One Piece and My Hero Academia. The total file size of the dataset is 5 GB. Note that my dataset is private to prevent copyright issues with the official owners. 

Below is the tree of my manga dataset distribution.

```python
Black Clover
│ └───Colored         : **1066**
│ └───Black-and-White : **1068**
│
My Hero Academia
│ └───Colored         : **1050**
│ └───Black-and-White : **1094**
│
One Piece
│ └───Colored         : **1461**
│ └───Black-and-White : **2679**
```

## Model

For training and inference, I used [MmGeneration](https://github.com/open-mmlab/mmgeneration) codebase. This is a great toolbox because I can easily change the hyperparameters for training. I used model [CycleGAN](https://openaccess.thecvf.com/content_iccv_2017/html/Zhu_Unpaired_Image-To-Image_Translation_ICCV_2017_paper.html) since my dataset is unpaired, meaning a black-and-white image does not necessary have a colored counterpart. Also, one-to-one paired image in manga is difficult to obtain because usually the colored images are just fan-made while the black-and-white are official release.

For the [configuration](https://github.com/open-mmlab/mmgeneration/tree/master/configs/cyclegan), I set the image size `(width, height) = (512, 732)`, `num_iters = 250k`, and `optimizer = Adam`. I actually rented a GPU from [Vast.ai](https://vast.ai/console/instances/), thankfully is was just cheap at $0.260 per hour for RTX A5000. The training lasted for ~2 days but the result was super good. 

The inference was done in kaggle notebook since it was just not computationally expensive unlike in training. The `FID and IS scores` are shown here.
```
|-----------------------------------------------------+-----------------+------+----------------------------+-------------------------|
|                Training configuration               |    Checkpoint   | Eval |            FID             |            IS           |
|-----------------------------------------------------+-----------------+------+----------------------------+-------------------------|
| cyclegan_lsgan_resnet_in_summer2winter_b1x1_250k.py | iter_250000.pth | orig | 52.7144(4.72190/47.99250)  | mean: 1.746, std: 0.141 |
|-----------------------------------------------------+-----------------+------+----------------------------+-------------------------|
```
You can access the [Training.ipynb](https://www.kaggle.com/code/chandlertimm/manga-colorization-training) and [Inference.ipynb](https://www.kaggle.com/code/chandlertimm/manga-colorization-inference) here. Both can be edited in kaggle.

## Demo

To show the results, I present samples below.

<p align="center">
  <img 
    src="https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/docs/6.png?raw=true"
  >
</p>
<p align="center">
  <img 
    src="https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/docs/7.png?raw=true"
  >
</p>
<p align="center">
  <img 
    src="https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/docs/8.png?raw=true"
  >
</p>
<p align="center">
  <img 
    src="https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/docs/9.png?raw=true"
  >
</p>


# License

This repo is licensed under [MIT License](https://github.com/chandlerbing65nm/Manga-Colorization-with-CycleGAN/blob/main/LICENSE)
