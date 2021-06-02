# PX4_Gazebo_setup
## Software requirement
* Gazebo 9
* Ubuntu 18.04
* ROS melodic
### MAVROS installation
```XML
sudo apt install ros-kinetic-mavros ros-melodic-mavros-extras
roscd mavros
wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
sudo chmod a+x ./install_geographiclib_datasets.sh
./install_geographiclib_datasets.sh
```
### PX4 installation
```XML
git clone https://github.com/PX4/Firmware
mv Firmware PX4_Firmware
cd PX4_Firmware
git checkout -b xtdrone/dev v1.11.0-beta1
git submodule update --init --recursive
cd PX4_Firmware
bash
bash ./Tools/setup/ubuntu.sh --no-nuttx --no-sim-tools
make px4_sitl_default gazebo
cd PX4_Firmware
source ~/PX4_Firmware/Tools/setup_gazebo.bash ~/PX4_Firmware/ ~/PX4_Firmware/build/px4_sitl_default
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/PX4_Firmware
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/PX4_Firmware/Tools/sitl_gazebo
cd ~/PX4_Firmware
roslaunch px4 mavros_posix_sitl.launch
```
### Check the PX4 installation
```XML
rostopic echo /mavros/state
```
if PX4 installed successfully, it should show connected:true
