# Marvel Image Classifier 

This project was an image classifier to identify Marvel charecters. I have used Googles Inception model and retrained it to classify Marvel charecters. 

## Dependencies

> 1. [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/)
> 2. Tensorflow docker image

## Procedures

### 1. Installing Docker Toolbox

Follow the procedures to install the Docker Toolbox from this [link](https://docs.docker.com/toolbox/toolbox_install_windows/). When everything is set open the Docker Toolbox Quickstart terminal.

### 2. Installing the Tensorflow image.

In the docker terminal run the below code.

`$ docker run -it -p 8888:8888 tensorflow/tensorflow:latest-devel`

this download all the dependencies necessary to successfully execute the project. Your terminal will change something like

`root@f39c242dd78a:~#`

Now all the dependencies have been succefully installed in your instance. Now press ctrl+D if you are on a windows or cmd+D on a mac. Your command line will exit the instance.

`root@f39c242dd78a:~# exit`

### 3. Cloning this Repository

Change your directory to desktop
`$ cd ~/Desktop`

clone the repository
`$ git clone https://github.com/bkumar080/Marvel-Image-Classifier.git`

I already have trained the model with my dataset, to test the model skip to step 7. To retrain the model again with your data, delete all the files in this folder except imageClassifier.py and make new folders containing images of the class you want to classify, and follow the steps below.

> Note: Please make sure to have atleast 100 images of each variant

### 4. Link the TF Image with our repository 
 
Now all we need is to connect our image set with the TF Image.

`$ docker run -it -v ~/Desktop/Marvel-Image-Classifier/tf_files:/tf_files -p 8888:8888 tensorflow/tensorflow:latest-devel`

Your terminal will change something like

`root@f39c242dd78a:~# `

To check for successful integration of the folder.
`:~# ls /tf_files `

This will give you the folder you created for your classes. Now we know that we have our files integrated with the TF Image.

### 5. Pulling in the Inception Model

To get the Googles Inception Model.

`:~# cd /tensorflow`

`:tensorflow# `

### 6. Retrain the Inception Model

Lets start retraining the Inception model. 

`:tensorflow# python tensorflow/examples/image_retraining/retrain.py  --bottleneck_dir=tf_files/bottlenecks   --how_many_training_steps=500   --model_dir=/tf_files/inception   --output_graph=/tf_files/retrained_graph.pb  --output_labels=/tf_files/retrained_labels.txt   --image_dir=/tf_files/`

This will take approximately about 15 to 30 minutes to run depending on your data. At the end it will give an Final Test accuracy between 85% and 99%. This is the testing accuracy of your model.

### 7. Testing our Model

Here comes the interesting part. To test download a image and save it in the tf_files directory, replace the name of the file in the below code and run.

`:tensorflow# python /tf_files/imageClassifier.py /tf_files/{filename}`

This gives out the scores of the class.