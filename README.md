# Show, Attend and Tell 
<b> Update (December 2, 2016)</b> TensorFlow implementation of [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](http://arxiv.org/abs/1502.03044) which introduces an attention based image caption generator. The model changes its attention to the relevant part of the image while it generates each word.


## References

This is based on Yunjey's [show-attend-and-tell](https://github.com/yunjey/show-attend-and-tell) repository.

<br/>

## Getting Started

### Prerequisites

First, clone this repo and [pycocoevalcap](https://github.com/tylin/coco-caption.git) in same directory.

```bash
$ git clone https://github.com/yunjey/show-attend-and-tell-tensorflow.git
$ git clone https://github.com/tylin/coco-caption.git
```

Replace <b>captions_val2014.json</b> in `coco-caption/annotations/`, and <b>captions_val2014_fakecap_results.json</b> in `coco-caption/results/` when needed to change dataset.

### Preparation

This code is written in Python2.7 and requires [TensorFlow 1.2](https://www.tensorflow.org/versions/r1.2/install/install_linux). In addition, you need to install a few more packages to process [MSCOCO data set](http://mscoco.org/home/). I have provided a script to download the <i>MSCOCO image dataset</i> and [VGGNet19 model](http://www.vlfeat.org/matconvnet/pretrained/). 

Run commands below then the images will be downloaded in `image/` directory (ensure that `train2014/` and `val2014/` exist) and <i>VGGNet19 model</i> (<b>imagenet-vgg-verydeep-19.mat</b>) will be downloaded in `data/` directory. 

In addition, ensure that caption files <b>captions_train2014.json</b> and <b>captions_val2014.json</b> are stored in `data/annotations/` folder.


```bash
$ cd show-attend-and-tell-tensorflow
$ pip install -r requirements.txt
$ chmod +x ./download.sh
$ ./download.sh
```

For feeding the image to the <i>VGGNet</i>, you should resize the <i>MSCOCO image dataset</i> to the fixed size of 224x224. Run command below then resized images will be stored in `image/train2014_resized/` and `image/val2014_resized/` directory.

```bash
$ python resize.py
```

Before training the model, you have to preprocess the <i>MSCOCO caption dataset</i>.

### Train the model 

To generate caption dataset and image feature vectors, run command below.

```bash
$ python prepro.py
```

Adjust <b>max_length</b> to truncate words length, <b>word_count_threshold</b> to filter word frequencies.
<br>

To train the image captioning model, run command below. 

```bash
$ python train.py
```

Adjust <b>n_time_step</b> to fit various sentence length.
<br>


### Evaluate the model 

To generate captions, visualize attention weights and evaluate the model, please see `evaluate_model.ipynb`.


<br/>

## Results
 
<br/>

#### Training data

##### (1) Generated caption: A plane flying in the sky with a landing gear down.
![alt text](jpg/train2.jpg "train image")

#### Validation data

##### (1) Generated caption: A large elephant standing in a dry grass field.
![alt text](jpg/val.jpg "val image")

#### Test data

##### (1) Generated caption: A plane flying over a body of water.
![alt text](jpg/test.jpg "test image")


