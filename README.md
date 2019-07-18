# Train your own data for detectiong your custom objects using YOLOv2/v3 on Ubuntu 16.04

1)Install darknet and Yolo_mark
* git clone darkent at https://github.com/AlexeyAB/darknet
   (or refer to: https://pjreddie.com/darknet/install/)   
*  git clone Yolo_mark at https://github.com/AlexeyAB/Yolo_mark

2) compile 
a) To compile in directory: /darknet 
make
b)To compile in directory: /Yolo_mark
cmake .
make
./linux_mark.sh [for testing a GUI open for manual labelling] 


3) Prpapre your own images
* delete all files from directory x64/Release/data/img
* put your .jpg-images to this directory x64/Release/data/img
* run file in Linux: ./linux_mark.sh, perform manual labeling (drawing a block to each object to be detected using mouse) on each image in the directory: x64/Release/data/img.
   more details refer to the bottom part at https://github.com/AlexeyAB/Yolo_mark.
* copy all .jpg and .txt files to directory: darknet/data/img.

once you finished the draw over all objects of all images on GUI, your own dataset is prepared for YOLO training.
Note: you should check the generated .txt at directory: x64/Release/data/img for each object in images and ensure it is right.

4) Change parameters in configuration 
a) Change parameter in files with obj.data nad obj.names
* change numer of classes (objects for detection) in file x64/Release/data/obj.data: 
   refer to: https://github.com/AlexeyAB/Yolo_mark/blob/master/x64/Release/data/obj.data#L1
* put names of objects, one for each line in file x64/Release/data/obj.names: 
   refer to: https://github.com/AlexeyAB/Yolo_mark/blob/master/x64/Release/data/obj.names

b) Change 2 lines in file x64/Release/yolo-obj.cfg for training your custom objects:
* set number of classes (objects): https://github.com/AlexeyAB/Yolo_mark/blob/master/x64/Release/yolo-obj.cfg#L230
* set filter-value: 
For Yolov2 (classes + 5)*5: https://github.com/AlexeyAB/Yolo_mark/blob/master/x64/Release/yolo-obj.cfg#L224
For Yolov3 (classes + 5)*3

5) Download pre-trained weights for the convolutional layers (76 MB): 
 * at  http://pjreddie.com/media/files/darknet19_448.conv.23

6) Prepare train files
   * Put files: yolo-obj.cfg, data/train.txt, data/obj.names, data/obj.data, darknet19_448.conv.23 and directory data/img near with executable darknet-file
   for example, all these files are placed in directory: /darknet, in my computer.
   * Change the path in data/train.txt and save it. 
    for example, change "x64/Release/data/img/sample.jpg"--> "data/img/sample.jpg"
 
7) Train on your own data
  ./darknet detector train data/obj.data yolo-obj.cfg darknet19_448.conv.23

8) Test your own images
