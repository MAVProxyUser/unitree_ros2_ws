# Ubuntu 18.04

Install Ubuntu 18.04, this was written using ubuntu-18.04.6-desktop-amd64.iso from https://releases.ubuntu.com/18.04/ubuntu-18.04.6-desktop-amd64.iso

The machine that was used for this document was hardwired to my local LAN with internet connectivity. Additionally it has a WiFi card currently connected to nothing. 

Select the "Minimal installation", "Download updates while installing Ubuntu", and "Install third-party software for graphics and Wi-Fi hardware and additional media formats" options. 

Open a terminal:
```
sudo apt-get install net-tools openssh-server
sudo apt-get update
sudo apt-get dist-upgrade

reboot
```

From another machine:
```
ssh 192.168.1.106 
(once connected)
rm -rf Documents/ Downloads/ Music/ Pictures/ Public/ Templates/ Videos/

sudo apt install software-properties-common
sudo add-apt-repository universe
```
Install ros2 eloquent - https://docs.ros.org/en/eloquent/Installation/Linux-Install-Debians.html
```
sudo apt update && sudo apt install curl gnupg2 lsb-release
```

This key from the original documentation is invalid - https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc 
Install new key per - https://discourse.ros.org/t/ros-gpg-key-expiration-incident/20669
```
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

sudo apt update
sudo apt upgrade

sudo apt-get install ros-eloquent-desktop

sudo apt install -y python3-pip
pip3 install -U argcomplete

source /opt/ros/eloquent/setup.bash

sudo apt install python3-colcon-common-extensions

sudo apt-get install git 
```

Use ssh clone method to obtain the submodules properly
```
git clone git@github.com:MAVProxyUser/unitree_ros2_ws.git --recurse-submodules

git clone https://github.com/lcm-proj/lcm.git
cd lcm 
mkdir build
cd build
cmake ..
make -j4
sudo make install 
```

Build the ros Unitree packages 
```
cd ../../unitree_ros2_ws/
colcon build 
```

Update the library path permanantly
First verify the path to the .so files, then add them to the ldconfig 
You should still be in ~/unitree_ros2_ws

```
find /usr -name liblcm.so
echo `pwd`/src/unitree_legged_sdk/lib/
echo `pwd`/src/unitree_legged_sdk/lib/ > /tmp/unitree.conf
echo /usr/local/lib/ >> /tmp/unitree.conf 

sudo mv /tmp/unitree.conf /etc/ld.so.conf.d/
sudo ldconfig
```

Sanity check the environment with example_walk, it should execute without error
```
source install/setup.sh 
./build/unitree_legged_sdk/example_walk
```


# Ubuntu 20.04

Install Ubuntu 18.04, this was written using ubuntu-20.04.5-desktop-amd64.iso from https://releases.ubuntu.com/focal/ubuntu-20.04.5-desktop-amd64.iso 

Select the "Minimal installation", "Download updates while installing Ubuntu", and "Install third-party software for graphics and Wi-Fi hardware and additional media formats" options. 
Open a terminal:
```
sudo apt-get install net-tools openssh-server
sudo apt-get update
sudo apt-get dist-upgrade

reboot
```

From another machine:
```
ssh 192.168.1.106 
rm -rf Documents/ Downloads/ Music/ Pictures/ Public/ Templates/ Videos/

sudo apt install software-properties-common
sudo add-apt-repository universe
```

Install ros2 foxy (or galactic if you prefer) - https://docs.ros.org/en/foxy/Installation/Linux-Install-Debians.html
```
sudo apt update && sudo apt install curl gnupg2 lsb-release
```

This key from the original documentation is invalid - https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc 
Install new key per - https://discourse.ros.org/t/ros-gpg-key-expiration-incident/20669
```
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

sudo apt update
sudo apt upgrade

sudo apt-get install ros-foxy-desktop
```
alternately you can install Galactic
```
sudo apt-get install ros-galactic-desktop

sudo apt install -y python3-pip
pip3 install -U argcomplete

source /opt/ros/eloquent/setup.bash
```
alternately source the foxy setup.bash
```
source /opt/ros/eloquent/setup.bash

sudo apt install python3-colcon-common-extensions

sudo apt-get install git 
```

Use ssh clone method to obtain the submodules properly
```
git clone git@github.com:MAVProxyUser/unitree_ros2_ws.git --recurse-submodules

git clone https://github.com/lcm-proj/lcm.git
cd lcm 
mkdir build
cd build
cmake ..
make -j4
sudo make install 
```

Build the ros Unitree packages 
```
cd ../../unitree_ros2_ws/
colcon build 
```

Update the library path permanantly
First verify the path to the .so files, then add them to the ldconfig 
You should still be in ~/unitree_ros2_ws
```
find /usr -name liblcm.so
echo `pwd`/src/unitree_legged_sdk/lib/
echo `pwd`/src/unitree_legged_sdk/lib/ > /tmp/unitree.conf
echo /usr/local/lib/ >> /tmp/unitree.conf 

sudo mv /tmp/unitree.conf /etc/ld.so.conf.d/
sudo ldconfig
```

Sanity check the environment with example_walk, it should execute without error
```
source install/setup.sh 
./build/unitree_legged_sdk/example_walk
```
