# install-robotics-tools
Install basic Robotics tools in Ubuntu

## Basic tools
Some editors and tools:
```
sudo apt update
sudo apt install -y curl nano gedit ssh vim git
```

Set up Git:
```
git config --global user.name "your-github-username"
git config --global user.email "your-email@address.com"
```

Python: some useful libraries:
```
sudo apt install -y ipython3 python3-pip python3-dev python3-numpy python3-scipy
```
if you have multiple Python versions in global environment, here's how to set the default:
(not needed if using virtual environment or conda)
```
# for example, you have python 3.12 and 2.7
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.12 1
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2 
sudo update-alternatives --config python
# then type `1` to choose python3.12
```

Jupyter notebook: 
```
pip3 install jupyterlab notebook ipympl ipywidgets
```
or
```
conda install jupyterlab notebook ipympl ipywidgets
```

ROS: follow ROS installation instructions, and install some useful packages for catkin and ROS
```
sudo apt install python3-catkin-pkg python3-rospkg  python3-wstool
```


## Install some Robotics packages using Conda:
Install [mim-solvers](https://github.com/machines-in-motion/mim_solvers) 
which will install [Pinocchio](https://stack-of-tasks.github.io/pinocchio/download.html) 
and [Crocoddyl](https://github.com/loco-3d/crocoddyl) as dependences:
```
conda install mim-solvers -c conda-forge
```
Some useful packages:
```
conda install mujoco matplotlib meshcat-python -c conda-forge
```


## (Not recommended) Install Pinocchio and Crocoddyl manually:
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
install Pinocchio, Crocoddyl and related packages:
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
configure environment variables: add the following lines to `~/.bashrc` (this may conflict with conda)
```
export PATH=/opt/openrobots/bin:$PATH
export PKG_CONFIG_PATH=/opt/openrobots/lib/pkgconfig:$PKG_CONFIG_PATH
export LD_LIBRARY_PATH=/opt/openrobots/lib:$LD_LIBRARY_PATH
export PYTHONPATH=/opt/openrobots/lib/python3.10/site-packages:$PYTHONPATH # Adapt your desired python version here
export CMAKE_PREFIX_PATH=/opt/openrobots:$CMAKE_PREFIX_PATH
```
then `source ~/.bashrc`.
