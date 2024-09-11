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

Set python3 as default:
```
sudo apt install -y python3 python2
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 2 
sudo update-alternatives --config python
# then type `1` to choose python3
```

Some python3 libraries (some may be already installed in fresh Ubuntu):
```
sudo apt install -y ipython3 python3-pip python3-dev python3-numpy python3-scipy python3-wstool
pip3 install --upgrade pip
# dependencies for catkin and ROS
sudo apt install -y python3-catkin-pkg-modules python3-rospkg-modules
# jupyter
pip3 install jupyterlab notebook
echo "alias jupyter-lab="~/.local/bin/jupyter-lab --no-browser"" >> ~/.bashrc
echo "alias jupyter-notebook="~/.local/bin/jupyter-notebook --no-browser"" >> ~/.bashrc
source ~/.bashrc
```

OpenCV and PCL:
```
sudo apt install -y libopencv-dev python3-opencv
sudo apt install -y libpcl-dev pcl-tools
```

## ROS2
Follow the official instructions for [Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html). 
Finally, to auto-source the setup file, add it into `.bashrc`:
```
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## Install some [robotpkg](http://robotpkg.openrobots.org/) packages:
Add `robotpkg` software repository to apt:
```
sudo apt install -qqy lsb-release curl
sudo mkdir -p /etc/apt/keyrings
curl http://robotpkg.openrobots.org/packages/debian/robotpkg.asc \
     | sudo tee /etc/apt/keyrings/robotpkg.asc
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/robotpkg.asc] http://robotpkg.openrobots.org/packages/debian/pub $(lsb_release -cs) robotpkg" \
     | sudo tee /etc/apt/sources.list.d/robotpkg.list
sudo apt update
```

Install [Pinocchio](https://stack-of-tasks.github.io/pinocchio/download.html), 
[Crocoddyl](https://github.com/loco-3d/crocoddyl), and related packages:
```
sudo apt install -y robotpkg-hpp-fcl
sudo apt install -y robotpkg-libccd
sudo apt install -y robotpkg-octomap
sudo apt install -y robotpkg-eigen-quadprog
# pinoocchio
sudo apt install -qqy robotpkg-py3*-pinocchio
# crocoddyl
sudo apt install -y robotpkg-py3\*-crocoddyl
# test data
sudo apt install -y robotpkg-example-robot-data
sudo apt install -y robotpkg-py310-eigenpy robotpkg-py310-pinocchio robotpkg-py310-quadprog robotpkg-py310-crocoddyl robotpkg-py310-hpp-fcl
```

Configure environment variables: add the following lines to `~/.bashrc`
```
export PATH=/opt/openrobots/bin:$PATH
export PKG_CONFIG_PATH=/opt/openrobots/lib/pkgconfig:$PKG_CONFIG_PATH
export LD_LIBRARY_PATH=/opt/openrobots/lib:$LD_LIBRARY_PATH
export PYTHONPATH=/opt/openrobots/lib/python3.10/site-packages:$PYTHONPATH # Adapt your desired python version here
export CMAKE_PREFIX_PATH=/opt/openrobots:$CMAKE_PREFIX_PATH
```
Then `source ~/.bashrc`

## TODO: testing pinocchio and crocoddyl installation
