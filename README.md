# Demos: speech recognition and voice control of Turtlebot3_waffle_pi
`Remind:make sure your PC or robot has been equipped with Microphone, and working well.`
### Usage

### Preparation

important deb and lib  
$ sudo apt-get install ros-kinetic-audio-common  
$ sudo apt-get install libasound2  
$ sudo apt-get install gstreamer0.10-*  

http://packages.debian.org/jessie/libsphinxbase1  
http://packages.debian.org/jessie/libpocketsphinx1  
http://packages.ubuntu.com/xenial/libgstreamer-plugins-base0.10-0  
http://packages.debian.org/jessie/gstreamer0.10-pocketsphinx  

$ sudo dpkg -i libsphinxbase1_0.8-6_amd64.deb  
$ sudo dpkg -i libpocketsphinx1_0.8-5_amd64.deb  
$ sudo dpkg -i libgstreamer-plugins-base0.10-0_0.10.36-2ubuntu0.1_amd64.deb  
$ sudo dpkg -i gstreamer0.10-pocketsphinx_0.8-5_amd64.deb  

Download the pocketsphinx package from github and buid    
$ cd ~/catkin_ws/src/    
$ git clone http://github.com/mikeferguson/pocketsphinx  
$ cd ..  
$ catkin_make  

Link the speech engine  
download the CMU Sphinx speech engine from:  
http://packages.debian.org/jessie/pocketsphinx-hmm-en-tidigits  
Than, unzip the CMU Sphinx and copy the model file to pocketsphinx package  

I have modified these two important files, recognizer.py and robocup.launch, include adding load configuration of hmm parameters in recognizer.py, and setting the link path of lm, dic and hmm parameters in  robocup.launch.  
  
Now we can launch the test node  
$ roslaunch pocketsphinx robocup.launch  

### speech recognition and voice control

Create “robot_voice” package
$ cd ~/catkin_ws/src/
$ catkin_create_pkg robot_ voice std_ msgs roscpp rospy

$ cd ..
$ catkin_make
$ source ~/catkin_ws/devel/setup.bash



