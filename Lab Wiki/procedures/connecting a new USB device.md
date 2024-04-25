Connecting a new USB device to the experimental control computer so that it's accessible to [[LabRAD]] and other programs is a bit tricky. Here's a walkthrough:

# Setting up a device
### Identifying the new device
- go to the `/dev` directory, where all devices are stored, and list the files in the folder using `ls`
- plug in/unplug the device, and use `ls` again. The list of devices should have changed
- Identify the name of the new device

### Setting permissions
Whenever a new device is added, you should update the permissions of all files in the `/dev` folder with the following command:
- `sudo chmod -R 777 /dev`
Let's break down the command:
- `sudo`: perform this action using admin permissions
- `chmod`: modifies the permissions of a file or folder. Stands for *ch*ange *mod*e
- `-R`: perform this action recursively on all subfolders
	- `777`: give full permissions for the files in question. This is a numerical permissions string:
		- the permissions number contains 3 bits: read (r), write (w), and execute (x). For example:
			- 7 -> 111 -> rwx
			- 5 -> 101 -> r-x
			- 2 -> 010 -> -w-
		- There are three kinds of access: Owner, Group, and Unauthenticated/other, so we use a triplet of numbers:
			- 777 -> 111, 111, 111 -> rwx (Owner), rwx (Group), rwx (Other)
			- 751 -> 111, 101, 100 -> rwx (Owner), r-x (Group), r-- (Other)
- `\dev` the folder to apply the command to

### Make the USB address of a given device permanent
Usually the address assigned to a device is kind of random every time you re-plug it. You'll want to make a permanent link to the device. 

Instructions based on this [website](http://hintshop.ludvig.co.nz/show/persistent-names-usb-serial-devices/):
1. look up the serial ID of the desired device by usb port connects
  ```bash
  ~ # udevadm info -a -n /dev/ttyUSB1 | grep '{serial}' | head -n1
      ATTRS{serial}=="A6008isP"
  ```

2. type `lsusb` and identify the info for the specific device

  >	ex. `ID 0403:6001` , the first number is the idVendor and the second number is the     idProduct
3. open up the `/etc/udev/rules.d/99-usb-serial.rules` file and add a new line with all the info and pick a name for your device's symlink
4.  You may need to add permission to the symlink (chmod +777 symlink)

Now, when you plug in the device, you should see a file with the name you created in `/dev`! This link will always point to the correct device. 

# Reconnecting an already set-up device
When you reconnect an already set-up device to the computer, its permissions may still have been reset. Take the following steps: 
- run `sudo chmod -R 777 /dev` to update the permissions
- restart the [[serial server]]
- restart any server that depends on that device