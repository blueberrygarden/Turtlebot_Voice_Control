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
test1
  
### Download 
Create a new APP, and download the SDK voice packet with the function: Speech dictation and online speech synthesis.  
`Remeber your APPID, it is very important and will be used in later work`   
extract the packet Linux_iat1227_tts_online1227_600b81a1 to your home directory  
find the file "iat_online_record_sample" at ~/Linux_iat1227_tts_online1227_600b81a1/samples/   
change the file path in Makefile and 64bit_make.sh  
picture1  
picture2  
$ cd ~/Linux_iat1227_tts_online1227_600b81a1/samples/iat_online_record_sample  
$ source 64bit_make.sh   
$ make  
picture3  

$ cd ~/Linux_iat1227_tts_online1227_600b81a1/libs/x64   
$ sudo cp libmsc.so /usr/lib/  
$ sudo ldconfig  
  
Now we can run the test demo    
$ cd ~/Linux_iat1227_tts_online1227_600b81a1/bin  
$ ./iat_online_record_sample  
picture4  


### speech recognition and voice control

add “robot_voice” package to your work space ~/catkin_ws/src  
change the APPID in .c and .cpp code to your own APPID, at ~/catkin_ws/src/robot_voice/src/  
ctrl + f can help you to search the key word  
$ cd ~/catkin_ws && catkin_make  
  
let's start to recognise our voice  
$ roscore
$ rosrun robot_voice iat_publish  
$ rostopic pub /voiceWakeup  std_msgs/String  "data: 'anny string'"  
we have changed iat_pubish.py, so you don't need to wake it up, iat_publish will keep recording 
$ rostopic echo /voiceWords  
picture5

I have written a simple voice_teleop node, subscribe the topic "voiceWords". which is published by iat_publish. Than publish control commands '/turtle1/cmd_vel' recording to the Text information.  
Now we can control the turtlesim node  
$ roscore    
$ rosrun robot_voice iat_publish    
$ rosrun robot_voice voice_teleop.py  
$ rosrun turtlesim turtlesim_node  
