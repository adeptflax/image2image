I created to this repo to do image2image translation with [CompVis/taming-transformers](https://github.com/CompVis/taming-transformers "CompVis/taming-transformers"). It's to solve my issue [here](https://github.com/CompVis/taming-transformers/issues/51). Based on how I modified the orginal source this repo can only be used for image2image translation. The CompVis/taming-transformers codebase is basically spaghetti code. Someone should rewrite the source code of this repo and CompVis/taming-transformers. This repo is basically a hack. I don't feel like making this repo's code sane. It's too much work. 

This repo should work, If you have any problems or questions, please open an issue and I will try to help you. I don't have any plans of mantaining this repo. If want to make changes please open an issue and I will link to it here. 


### Install the python requirements
I used python 3.8.5 and I used a rtx 3090 to train the model. 
```bash
pip3 install -r requirements.txt

```

### You will need the following directory stucture for training data:

It's transforming "X" data into "Y" data
> ds/x/train/
ds/x/validation/
ds/y/train/
ds/y/validation/

### Creates a list of training data and puts it into text file.

```bash
mkdir -p $HOME/.cache/autoencoders/data/ILSVRC2012_train/
mkdir -p $HOME/.cache/autoencoders/data/ILSVRC2012_validation/

!ls -d $PWD/ds/y/validation/* > $HOME/.cache/autoencoders/data/ILSVRC2012_validation/filelist.txt
!ls -d $PWD/ds/y/train/* > $HOME/.cache/autoencoders/data/ILSVRC2012_train/filelist.txt

### Change the config
The code only supports square input and output data. Someone should probably figure out how to make it support non-sqaure data. You should probably change all instances of "512" with the resolution of your dataset in "configs/imagenet_vqgan.yaml".

```bash
python3 main.py --base configs/imagenet_vqgan.yaml -t True --gpus 0,
```

