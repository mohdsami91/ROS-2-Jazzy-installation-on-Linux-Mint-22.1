# ROS 2 Jazzy Installation on Linux Mint 22.1

This guide explains how to install **ROS 2 Jazzy Jalisco** on **Linux Mint 22.1** (based on Ubuntu 24.04).

---

## 1. Setup Locale

```bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

---

## 2. Add ROS 2 Repository

Install required packages:
```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
```

Add ROS 2 GPG key:
```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

Add repository to sources list:
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## 3. Install ROS 2 Jazzy

Update and install:
```bash
sudo apt update
```

Full Desktop version (recommended):
```bash
sudo apt install ros-jazzy-desktop
```

Bare-bones version (core libraries only):
```bash
sudo apt install ros-jazzy-ros-base
```

Additional development tools:
```bash
sudo apt update && sudo apt install ros-dev-tools
```

---

## 4. Environment Setup

Add ROS 2 to your shell:
```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

For your own workspace (after building with colcon):
```bash
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 5. Install Build Tools (Optional but Recommended)

```bash
sudo apt install python3-colcon-common-extensions python3-rosdep python3-vcstool build-essential
```

Initialize rosdep:
```bash
sudo rosdep init
rosdep update
```

---

## 6. Test Installation

Run a talker in one terminal:
```bash
ros2 run demo_nodes_cpp talker
```

Run a listener in another:
```bash
ros2 run demo_nodes_cpp listener
```

You should see the talker publishing and the listener receiving messages 🎉

## 7. Install xacro and joint_state_publisher

These packages are available via APT for ROS Jazzy:
```bash
sudo apt install -y ros-jazzy-xacro ros-jazzy-joint-state-publisher
```

You can also install other useful packages:
```bash
sudo apt install -y ros-jazzy-joint-state-publisher-gui
```

## 8. Test the Installation

To check if they were installed correctly:
```bash
ros2 run xacro xacro --help
ros2 run joint_state_publisher joint_state_publisher --help
```

---

## Notes

- Always source your environment before running ROS 2 commands:
  ```bash
  source /opt/ros/jazzy/setup.bash
  source ~/ros2_ws/install/setup.bash
  ```
- You can add these lines permanently in your `~/.bashrc` file.

---

✅ ROS 2 Jazzy is now installed and ready to use on Linux Mint 22.1!
