# COVID-19-Real-Time-Face-Mask-Detector-using-CNN

	•	Topic: COVID-19 Real-Time Face Mask Detector (using computer vision and deep learning)

	•	Libraries & Frameworks: Keras, TensorFlow, MobileNetV2 architecture, opencv

To train our custom face mask detector, we need to separate our project into two phases/levels:

	•	Phase 1: Training (code1.py)
	•	Phase 2: Deployment (code2.py)

## Phase 1 – Training:
	
	i.	Pre – Training:
	    a.	load face mask detection dataset from disk
	    b.	preprocess our dataset
	    c.	encode our labels – from text to binary value
	    d.	partition the data into training (80%) and testing (20%)
	    e.	construct the training image generator for data augmentation
    
	ii.	Prepare MobileNetV2 for fine-tuning:
	    a.	load MobileNetV2 with pre-trained ImageNet weights, leaving off head of network 
	    b.	construct a new fully connected head, and append it to the base in place of the old head
	    c.	freeze the base layers of the network. The weights of these base layers will not be updated during the process of backpropagation, whereas the head layer weights will be tuned.
    
	iii.	Compile and train our face mask detector network:
	    a.	compile our model with Adam optimizer
	    b.	fit our Model (adding early stopping to overfit our Model & adding the Data Augmentation object we create before)

	iv.	Once training is complete, we’ll evaluate the resulting model on the test set:
	    a.	make predictions on the test set, grabbing the highest probability class label indices
	    b.	print classification report in the terminal for inspection
	    c.	serializes our face mask classifier
	    d.	plot our accuracy and loss curves
    
## Phase 2 – Deployment:

    i.	load face mask classifier from disk
    ii.	detect & extract face from the video streaming (using OpenCV and FaceNet)
    iii.	apply face mask classifier to each face to determine "mask" or "no mask"
    iv.	show the results

### Dataset:

	i.	This dataset consists Approx. 4000 images belonging to two classes:
	    -	faces with mask: 1951 images
	    -	faces without mask: 1948 images
	   link to dataset in OneDrive: https://1drv.ms/u/s!Au-Ss_WjDdP7lKxcu_LCCLYg9jCh6g?e=vCuAR0
	   
	ii.	To strengthen our model in terms of data set size, we can increase our training data in 2 ways:
	    1. Take regular face photos and then create a custom Python script for computer vision to add face masks to them.
	    2. Data augmentation - Applying a (small) amount of the transformations (translations, rotations, scale changes, shear, and horizontal inversion) to an input image will change its appearance slightly, but it does not change the class label.

### Results:
i.	COVID-19 face mask detector training accuracy/loss curves demonstrate high accuracy and little signs of overfitting on the data:

![image](https://user-images.githubusercontent.com/35423788/113988989-abb14e80-9858-11eb-9fbc-613f4598b0c1.png)

ii.	Model Demonstration:

![ezgif com-gif-maker](https://user-images.githubusercontent.com/35423788/113990852-90dfd980-985a-11eb-8ae0-10fcbfeeb316.gif)
