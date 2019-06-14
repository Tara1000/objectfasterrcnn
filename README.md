# objectfasterrcnn
### Faster-RCNN adaption based on tf-faster-rcnn by [endernewton](https://github.com/endernewton/tf-faster-rcnn) built partly on files by Ross Girshick. Modified by me [Tara1000](https://github.com/Tara1000/) to implement two new network models, ResNet-41 and Deeper MobileNet with the purpose of testing performance and accuracy of these modifications. Pre-trained ImageNet weights added from TensorFlow or [endernewton](https://github.com/endernewton). Objectfasterrcnn is tested only on Ubuntu 18-04 on NVidia GTX 1080 Ti.

More details: [https://github.com/endernewton/tf-faster-rcnn](https://github.com/endernewton/tf-faster-rcnn)

COCO 2014 data set can be downloaded from [http://cocodataset.org/#download](http://cocodataset.org/#download)

If you lack pip or conda packages in Anaconda-3 to run the code, see `packagelist.txt` at the google drive for package versions, or setup a virtual environment with the yaml file included in this repository:
`> conda env create -f tfgpuenv.yaml`

`> conda activate tensorflow\_gpuenv`

### Build:

`> cd lib`

If your GPU is not a NVidia 1080 (Ti) change the architecture accordingly

`> vim setup.py`

Change sm\_61 in line 130 to the best fit as shown in [tf-faster-rcnn](https://github.com/endernewton/tf-faster-rcnn)

In lib folder, proceed to build the project:

`> make clean`

`> make`

`> cd ..`

### Configure code base:
Download ImageNet weights (data) and pre-trained COCO models (output) from Faster-RCNN folder at [https://drive.google.com/open?id=1qlXjT-P6vgZk6NylAo7JeJREKY3jccNV](https://drive.google.com/open?id=1qlXjT-P6vgZk6NylAo7JeJREKY3jccNV) into project root, and clone + build coco API:

`> cd data`
`> git clone https://github.com/pdollar/coco.git`
`> cd coco/PythonAPI`
`> make`
`> cd ..`

In `coco` create symlinks of 'images' and 'annotations' folders from your data set folder to here:

`> ln -s your/path/to/coco2014/annotations ./annotations`

`> ln -s your/path/to/coco2014/images ./images`

`> cd ../..`

### Run

To run validation run the test\_faster\_rcnn.sh script with parameter 0 for default GPU 0 and e.g mobile for MobileNet v.1 or res41 for ResNet-41:

`> ./experiments/scripts/test\_faster\_rcnn.sh 0 coco mobile`

To train a network on GPU 0, move or remove its COCO pretrained weights folder from output, e.g. res41 for ResNet-41, and run:

`> ./experiments/scripts/train\_faster\_rcnn.sh 0 coco res41`

