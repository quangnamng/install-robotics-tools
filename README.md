# install-robotics-tools
Install basic tools for Robotics in Ubuntu systems

## Basic tools
Some editors and tools:
```
sudo apt update
sudo apt install -y curl nano gedit ssh vim git terminator
```

Set up Git:
```
git config --global user.name "your-github-username"
git config --global user.email "your-email@address.com"
```

Some python3 libruaries (some may be already installed in fresh Ubuntu):
```
sudo apt install -y ipython3 python3-pip python3-dev python3-numpy python3-scipy python3-wstool
```
Set python3 as default:
```
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2 
sudo update-alternatives --config python   # then type `2` to choose python3
```

OpenCV and PCL:
```
sudo apt install -y libopencv-dev python3-opencv
sudo apt install -y libpcl-dev pcl-tools
```

## Install [robotpkg](http://robotpkg.openrobots.org/) by LAAS lab
Add the robotpkg ppa:
```
sudo sh -c 'echo "deb [arch=amd64] http://robotpkg.openrobots.org/wip/packages/debian/pub $(lsb_release -sc) robotpkg" > /etc/apt/sources.list.d/robotpkg-openrobots.list'
sudo sh -c 'echo "deb [arch=amd64] http://robotpkg.openrobots.org/packages/debian/pub $(lsb_release -sc) robotpkg" >> /etc/apt/sources.list.d/robotpkg-openrobots.list'
curl -s http://robotpkg.openrobots.org/packages/debian/robotpkg.key | sudo apt-key add -
```

Pinocchio:
```
sudo apt install -y robotpkg-hpp-fcl
sudo apt install -y robotpkg-libccd
sudo apt install -y robotpkg-octomap
sudo apt install -y robotpkg-pinocchio
sudo apt install -y robotpkg-eigen-quadprog
# test data
sudo apt install -y robotpkg-example-robot-data
sudo apt install -y robotpkg-py310-eigenpy robotpkg-py310-pinocchio robotpkg-py310-quadprog robotpkg-py310-crocoddyl robotpkg-py310-hpp-fcl
```

## ROS2
Follow the official instruction for [Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html). 
Finally, to auto-source the setup file, add it into `.bashrc`:
```
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
