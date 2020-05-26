# AUTOMATION OF MACHINE LEARNING MODEL WITH JENKINS

I have automated machine learning model with jenkins. Using my own docker image in which all the required libraries are installed.I have used linux operating system for this.

# DOCKER IMAGE 

For creating my own docker image I have used two "images" one is centos and second is "tensorflow/tensorflow"
~~~
FROM centos:latest
RUN yum install python3 -y
FROM tensorflow/tensorflow
RUN pip install keras
RUN pip install sklearn
RUN pip install numpy
RUN pip install pandas

COPY <file name> .
~~~

# JENKINS

For doing this task first their should be jenkins installed in linux operating system. Then launch jenkins in your browser.Then install github plugins.This plugins help you into automatically downloading the git repository. After installing create different jobs.


## JOB1
JOB1 is for only pulling github repository we provide url of git repository to jenkins(in job1).Give name according to you my job1 name is "git_upload".

![job1 1](https://user-images.githubusercontent.com/62477381/82884631-9776a280-9f61-11ea-8bed-4708c6adc5f6.PNG)

Set "GitHub hook trigger for GITScm polling" 

![job 1 2](https://user-images.githubusercontent.com/62477381/82884731-c0973300-9f61-11ea-8b40-e3c5aea00d5d.PNG)

For copy file use copy command

![job1 3](https://user-images.githubusercontent.com/62477381/82884864-f9370c80-9f61-11ea-8f94-007185dcef96.PNG)

## JOB2
In job2 I have done the image building part after building image we have to run the container.This job will run after job1 when it will successfull.

For this go to BUILD TRIGGERS and click on "Build after other projects are built" and select job and click "Trigger only if build is stable"

![job2 1](https://user-images.githubusercontent.com/62477381/82887422-99dafb80-9f65-11ea-8105-b9e7801c05bb.PNG)

Now write some code for running the container

![job2 2](https://user-images.githubusercontent.com/62477381/82887614-e6bed200-9f65-11ea-97a9-3647ea4658ab.PNG)

Now for email configuration go to Manage pluggins install Email-ext plugins and to configure it. Go to System configuration and the go to Extended Email notification and set SMTQ sever

SMTP server name : 
User name: (provide your email-id)
Password: "give your password"
Use SSL : Checked
SMTP Port: 895

![job2 3](https://user-images.githubusercontent.com/62477381/82888951-a52f2680-9f67-11ea-8475-a2922cf64f9a.PNG)

## JOB3 
This is for executing the python file which is copied in that
This will run after when job two is successfully build

![job3](https://user-images.githubusercontent.com/62477381/82889577-939a4e80-9f68-11ea-8758-086a8bccfe7a.PNG)

I have stored the accuracy in folder for retreiving it.

## JOB4
It will check the accuracy if accuracy is less then 95% then it wil again run the and execute the code.

For this i have created an other code in another folder.If accuracy is less this file will run and increase the accuracy.
~~~
from keras.models import Sequential
from keras.layers import Conv2D
from keras.layers import MaxPooling2D
from keras.layers import Dense
from keras.layers import Flatten
from keras.optimizers import SGD

def define_model():
	model = Sequential()
	model.add(Conv2D(32, (3, 3), activation='relu', kernel_initializer='he_uniform', input_shape=(28, 28, 1)))
	model.add(MaxPooling2D((2, 2)))
	model.add(Flatten())
	model.add(Dense(100, activation='relu', kernel_initializer='he_uniform'))
	model.add(Dense(10, activation='softmax'))
	# compile model
	opt = SGD(lr=0.01, momentum=0.9)
	model.compile(optimizer=opt, loss='categorical_crossentropy', metrics=['accuracy'])
	return model
  ~~~

![job4](https://user-images.githubusercontent.com/62477381/82891699-cf82e300-9f6b-11ea-80f4-9e630d2da340.PNG)

# VISUALISATION
For visualisation I have use two things one is "Build Pipeline View" and second is "Build Monitor View"

![ml5](https://user-images.githubusercontent.com/62477381/82892516-3b198000-9f6d-11ea-8887-ea5fb8b88e16.PNG)

![ml6](https://user-images.githubusercontent.com/62477381/82892529-410f6100-9f6d-11ea-931f-6bcc358c7003.PNG)

# MONITORING 
For monitoring of jenkins I have used Prometheus . For using it first u have to install Prometheus than you have to provide target.
and install "prometheus metrics " in jenkins also for monitoring

~~~
prometheus-2.18.1.linux-amd64.tar.gz
~~~
For installing
~~~
tar -xzf prometheus-2.18.1.linux-amd64.tar.gz
~~~

Then go to that that directory and edit yml file
~~~
cd <name>
vim prometheus.yml
~~~

![prom](https://user-images.githubusercontent.com/62477381/82893383-897b4e80-9f6e-11ea-9e4c-e12b97bedd4d.PNG)

Now run IP address of prometheus and monitor your jenkins job

![prom2](https://user-images.githubusercontent.com/62477381/82893402-8da76c00-9f6e-11ea-9faa-f3212bad5678.PNG)

![ml3](https://user-images.githubusercontent.com/62477381/82893558-ce9f8080-9f6e-11ea-9b5e-acf735aa5406.PNG)

![ms2](https://user-images.githubusercontent.com/62477381/82893760-263dec00-9f6f-11ea-8a5b-86ec409daa6e.PNG)



