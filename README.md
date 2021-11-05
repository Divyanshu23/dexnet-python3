# Dex-Net : Neural Network architecture for learning Robotic Grasping

### Original Package [Berkley AUTOLAB Dexnet](https://github.com/BerkeleyAutomation/dex-net)
---
**NOTE**
Please clone this current repository to setup dexnet on Ubuntu 16.04 with Python3. We have modified the source code at certain places to resolve installation errors without changing the functionality of the repo. If cloning the original repo from UC Berkeley, you are prone to get errors.
---


### Prerequisites
This packages (not the original one from UC Berkeley) has been tested on Ubuntu 16.04 with Python3.6 installation in a conda environment. To start going forward, we require the following installations beforehand.
1. Anaconda - Refer [this](https://docs.anaconda.com/anaconda/install/linux/) to install on Ubuntu.
2. Python3 - Python shall be automatically installed when you create an Anaconda evironment (talked about it in the next section). So let the things be the way they are for the case of Python.

### Installation ###

1. Create an Anaconda environment (referred to as env from now) and then activate it.
    ```
    $ conda create --name gqcnn python=3.6
    $ conda activate gqcnn
    ```  
    Here "gqcnn" is the name of the env (can give yours). We have specified to install Python3.6 in this env (you can refer any higher version available but for consistency, I will recomment to stick to 3.6). 

2. Install Boost-Python.  
Booost Python must be probably installed (but a wrong version) in your Ubuntu. I will fist recomment to jump to next step and try running those. If they run without errors, well and good. However, if you encounter something like "Boost Not found" or similar, then follow this step correctly.  
   - Remove old boost installation if any.
        ```
        $ sudo apt-get -y --purge remove libboost-all-dev libboost-doc  libboost-dev
        $ sudo rm -r /usr/local/lib/libboost*
        $ sudo rm -r /usr/local/include/boost
        $ sudo rm -f /usr/lib/libboost_*
        $ sudo rm -r /usr/include/boost
        ```
   - Download the source tarball boost_1_58_0.tr.bz2 from [here](https://www.boost.org/users/history/version_1_58_0.html)
   - In the directory where you want to put the Boost installation, execute
        ```
        $ tar --bzip2 -xf /path/to/boost_1_58_0.tar.bz2
        ```
        If not sure about directory, run this command from your home directory in ubntu. You shall see a new folder "boost_1_58_0". Enter this directory from your shell.
    - Bootstrap boost
        ```
        $ ./bootstrap.sh --prefix=/usr/local
        ```
        If the previous step gives permission denied error, run the command with sudo privelages.
    - Edit user-config.jam
        ```
        $ cp /path/to/boost_1_64_0/tools/build/example/user-config.jam $HOME
        ```
        Open the copied user-config.jam in any text editor and go to the bottom. Uncomment the line "using python" and change it to using python : 3.5 : /usr/bin/python3 : /usr/include/python3.5m : /usr/lib; Change "3.5" to your default global python3 installation.
    - Build Boost
        ```
        $ ./b2
        ```
    - Install Boost
        ```
        $ sudo ./b2 install
        ```
        Just to confirm that the required dynamic libraries have been installed, do
        ```
        $ ls /usr/local/lib/ | grep libboost_python
        ```
        If you see some library listings in your bash shell, then you are good to go forward.
3. Run the installation script.
    ```
    $ sudo sh install.sh {cpu|gpu} {python|ros}
    ```
    If you encounter some linking and/or "boost not found" erros, make sure to complete step-2 now.
4. Test your installation
    ```
    $ python setup.py test
    ```
    This shall run 15 tests to verify that your installation is working correctly. It may take upto 5 mins to complete.