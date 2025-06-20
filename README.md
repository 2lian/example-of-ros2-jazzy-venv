# example-of-ros2-jazzy-venv

Lets build the simple [dwm1001 package](https://github.com/the-hive-lab/dwm1001_ros2/tree/integration) with its [python dependencies](https://pypi.org/project/pydwm1001/).

---
Make your workspace:
```bash
cd ~
mkdir myrosws

cd myrosws
mkdir src
cd src
git clone https://github.com/the-hive-lab/dwm1001_ros2.git
cd ..
```

Make your python venv:
```bash
cd ~
mkdir myrosws

. /opt/ros/jazzy/setup.bash
sudo apt install python3-virtualenv python3.12-venv # just in case it's missing
sudo apt install --upgrade python3-wheel
python3 -m venv --system-site-packages ./venv # creates venv with ros2 pkg included and frozen
. venv/bin/activate
python3 -m pip install --upgrade pip wheel # updates wheel that is often outdated
```

Install you dependencies:
```bash
cd ~
mkdir myrosws

. /opt/ros/jazzy/setup.bash
. venv/bin/activate

python3 -m pip install pydwm1001
```

Build your workspace (I would recommand a fresh new terminal):
```bash
cd ~
mkdir myrosws

. venv/bin/activate # I usually activate venv before sourcing ros, but the order should not matter
. /opt/ros/jazzy/setup.bash

python3 -m colcon build
```

You MUST build with the colcon from inside your venv by using `python3 -m colcon`. System level simple `colcon` command is not part of the venv, thus does not include your python dependencies.

Launch your node (sourcing venv and ros not necessary):
```bash
cd ~
mkdir myrosws

. install/setup.bash

ros2 launch dwm1001_launch active_node.launch.py
```

Enabling the venv is not necessary for launching and running ros2 nodes, it is only necessary for building. The venv is included by colcon in your ros workspace when you build.

However, please note that the venv is only available inside a node, it is not available inside a ros2 launcher `launch.py`.
