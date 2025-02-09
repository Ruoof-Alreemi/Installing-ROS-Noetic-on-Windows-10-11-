# Installing-ROS-Noetic-on-Windows-10-11-
## **Prerequisites**  
- Windows 10 (Version 2004 or later) or Windows 11  
- WSL 2 (Windows Subsystem for Linux)  
- Ubuntu 20.04 (Running inside WSL 2)  
- Basic knowledge of the command line  

---

## **Step 1: Install WSL 2 and Ubuntu 20.04**  

### **1.1 Enable WSL 2 on Windows**  
Open **PowerShell as Administrator** and run the following command:  

```powershell
wsl --install
```

This command will install WSL with Ubuntu by default. **Restart your computer** after the installation.  

---

### **1.2 Check if WSL 2 is Installed**  
After restarting, open **PowerShell** and check if Ubuntu is installed:  

```powershell
wsl --list --verbose
```

If Ubuntu is not installed, you can install it manually using:  

```powershell
wsl --install -d Ubuntu-20.04
```

After installation, open **Ubuntu** from the **Start Menu** and set up your username and password.  

---

## **Step 2: Update and Upgrade Ubuntu**  

Inside the **Ubuntu terminal**, update the package list:  

```bash
sudo apt update && sudo apt upgrade -y
```

---

## **Step 3: Setup ROS Noetic Repository**  

### **3.1 Add the ROS Package Repository**  
First, install some necessary tools:  

```bash
sudo apt install curl gnupg lsb-release -y
```

Now, add the ROS repository and keys:  

```bash
echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/ros-latest.list
curl -sSL 'http://repo.ros2.org/repos.key' | sudo apt-key add -
```

Update the package list:  

```bash
sudo apt update
```

---

## **Step 4: Install ROS Noetic**  

### **4.1 Install the Full Desktop Version**  
The full version includes ROS tools like **Rviz, Gazebo, and rqt**:  

```bash
sudo apt install ros-noetic-desktop-full -y
```

If you want a minimal installation, you can install only the ROS core:  

```bash
sudo apt install ros-noetic-ros-base -y
```

---

## **Step 5: Set Up the ROS Environment**  

After installation, set up your ROS environment automatically:  

```bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

For **Zsh users**, use:  

```bash
echo "source /opt/ros/noetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
```

---

## **Step 6: Install Additional ROS Tools**  

Install `rosdep`, `rosinstall`, and other useful tools:  

```bash
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential -y
```

Initialize `rosdep`:  

```bash
sudo rosdep init
rosdep update
```

---

## **Step 7: Verify Installation**  

### **7.1 Run roscore**  
To check if ROS is working, open **Ubuntu WSL** and run:  

```bash
roscore
```

If it runs without errors, ROS is installed correctly.  

### **7.2 Run a Test Node**  
Open another **Ubuntu WSL terminal** and run:  

```bash
rosrun turtlesim turtlesim_node
```

If a window with a turtle appears, then ROS is working fine!  

---

## **Step 8: Enable GUI Applications (Optional for Rviz/Gazebo)**  

Since WSL 2 does not support native GUI applications, you need to install **VcXsrv X Server** for Windows.  

### **8.1 Install X Server for Windows**  
- Download **VcXsrv** from: [https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/)  
- Install and launch **XLaunch**, then select **Multiple Windows** and **Start No Client**.  

### **8.2 Configure Display Settings in WSL**  
Run the following command inside **Ubuntu WSL**:  

```bash
echo "export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0" >> ~/.bashrc
source ~/.bashrc
```

Now, you can run ROS GUI tools like **Rviz** and **Gazebo**:  

```bash
rviz
```

or  

```bash
gazebo
```

---

## **Troubleshooting**  

### **Issue 1: "roscore not found"**  
Run:  
```bash
source /opt/ros/noetic/setup.bash
```
If this fixes the issue, add the command to `.bashrc` as shown in **Step 5**.  

### **Issue 2: "Could not connect to display" (GUI issues)**  
Ensure that **VcXsrv** is running and that `DISPLAY` is set correctly.  

---

## **Conclusion**  
You have successfully installed **ROS Noetic** on **Windows 10/11** using **WSL 2**. You can now start developing ROS applications on Windows! 🚀  
