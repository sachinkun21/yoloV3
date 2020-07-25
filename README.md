Yolo Darknet installation and Custom training Steps
 
Official Website: - https://pjreddie.com/darknet/yolo/
 
We will be working with Tiny Yolo
 
Tiny Yolo Config File:- https://github.com/pjreddie/darknet/blob/master/cfg/yolov3-tiny.cfg
 
Changes to be done in Yolo COnfig File
 
1. Uncomment the lines 5,6, and 7 and change the training batch to 64 and subdivisions to 2.
 
2. Change the number of filters for convolutional layer "[convolution]" just before every yolo output "[yolo]" such that the number of filters= 3 x (5 + #ofclasses)= 3x(5+1)= 18. The number 5 is the count of parameters center_x, center_y, width, height, and objectness Score. So, change the lines 127 and 171 to "filters=18".
 
3. For every yolo layer [yolo] change the number of classes to 1 as in lines 135 and 177.
 
Files Needed :-
 
1. Create a file object.names
 
Insert the class name
 
Rubiks Cube
 
2. trainer.data
 
Contents:-
 
1. Number of classes.
2. Locations of train.txt and test.txt files relative to the darknet main directory.
3. Location of objects.names file relative to the darknet main directory.
4. Location of the backup folder for saving the weights of training process, it is also relative to the darknet main directory
 
Looks like:-
 
classes= 1  
train  = custom/train.txt  
valid  = custom/test.txt  
names = custom/objects.names  
backup = backup/
 
3. yolov3-tiny.cfg 
It contains the training parameters as batch size, learning rate, etc., and also the architecture of the network as number of layer, filters, type of activation function, etc.
 
Weights File Download Link :- https://pjreddie.com/media/files/darknet53.conv.74
 
Start Training:-
 
Create a folder called "training" in the darknet directory
 
Then we copy the files train.txt, test.txt, objects.names, yolov3-tiny.cfg, and trainer.data inside the "training" folder .
 
Training Command :- ./darknet detector train custom/trainer.data custom/yolov3-tiny.cfg darknet53.conv.74
 
Notes :-
Weights will be saved in the backup folder every 100 iterations till 900 and then every 10000.
Kill the training process once the average loss is less than 0.06, or once the avg value no longer increases.
 
Once training is done
 
Do the prediction/testing via live cam
conda create --name yolo python=3.6.10
conda activate opencv
#install the opencv package
conda install -c conda-forge opencv
or
pip install opencv-python
 
cd to project_directory
 
python yolo_opencv.py -c /path/to/yolov3-tiny.cfg -w /path/to/yolov3-tiny_finally.weights -cl /path/to/objects.names
 
 
 
 
 
