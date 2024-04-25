The original Pi beam profiler is documented on the lab wiki. This project was a failed attempt to update it to a Raspberry pi 4 and python 3. I'm documenting it in the hopes that we're able to get it working later. 

## Bill of materials
- Raspberry pi 4
- Raspberry pi touch display
- Raspberry pi camera v. 2.3
- Case for pi + touch display
- Extra long ribbon cable
- 32GB microSD card

## Software
- I tried two different softwares, but both were quite heavily edited. 
	- The first was Tony Ransford's PiBeamProfiler.py. 
		- PyQt4 had to be upgraded to PyQt5, replacing many elements that had previously been located in QtGui with QtWidgets
		- The matplotlib backend needed to be changes
		- The Scipy API had to be changed to reflect changes in PIL
	- The second was a github project named Beam-GUI. This ran fine on the pi, but the GUI didn't fit on the touch display and was generally very poorly designed, with the position of every element hardcoded into the window size. 
		- This required a full GUI rework to make the window rescalable. 


## Installation
- The beam profiler softwares both use the legacy camera stack. This means that when flashing the OS onto the SD card, you *MUST* select "Raspberry Pi OS (Legacy)" to make the legacy camera stack avaliable. 
- Once the pi has booted and been set up, enable the legacy camera stack:
	- `sudo raspi config`
	- navigate to "interface"
	- select "Enable Legacy Camera"
	- reboot
- Install the python packages
	- `sudo apt-get install python3-matplotlib`
	- `sudo apt-get install python3-opencv`
	- `sudo apt-get install python3-scipy`
	- Numpy and PyQT5 should be pre-installed on the pi, or installed as dependencies by the above packages
- Run the software. 

## Issues
It seems that running either of the two programs I tried encounters a `Segmentation Fault` error. This is bad and I don't really know how to fix it. 