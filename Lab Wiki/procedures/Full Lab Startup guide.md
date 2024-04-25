## Computers 
### Experimental Control 
1) When restarting the computer, select Ubuntu 18 from the start up menu.
2) Start [[Barrier]] and make sure it's running. This will allow you to control all three computers with the same mouse and keyboard.
3) Open a terminal: 
	- Unlock the /dev permissions:
		- `sudo chmod –R 777 /dev `
	- Start [[LabRAD]]: 
		- `python –m labrad.node`
	- Start the [[RealSimpleGrapher]]: 
		- ```cd LabRAD/RealSimpleGrapher
		   python rsg.py``` 
	- Start [[script scanner]]: 
		- ```cd LabRAD/common/lib/servers/script_scanner/ 
		   python script_scanner.py``` 
	- Start the [[Qsim GUI]]: 
		- ```cd LabRAD/Qsim/clients/QsimGUI/ 
		   python QsimGUI.py```
3) If you launch Tabby, the 1st, 3rd, 4th, and 5th bullet points have shortcuts configured. If you click on the "window"-looking icon in the far right of the tab bar, you should be able to launch these programs without typing
4) Open the Vivaldi browser to [[the LabRAD control page]] (localhost:7667/nodes) 
We will return here soon, there's other computers to start and hardware to restart now 
### [[Camera computer]] 
1) Start the labRAD node on the computer, there's a shortcut on the desktop.  
2) Start the [[Andor camera software]], there's a shortcut and then run the python module (press F5) 
### [[Wavemeter computer]] 
1) Shortcut on the computer restarts the labRAD node 
2) Another shortcut starts the multiplexer server 
3) Start wavemeter software  
## [[Pulser]] 
1) The power supply that powers the 8V is probably on and fine, it restarts with a power failure. The one that is probably off is the big HP supply. The safe way to restart this is to increase the current limit above 15A, and then bring the voltage up slowly to 5V. 
	- Make sure the output adjust light is on "current", and then press and hold 'Display settings' button while you increase the possible output current up to ~16A. 
	- Then switch the output setting to volts and slowly increase the voltage to 5V.  
2) The reference clock also probably failed. Simply flip the switch off and on. The green light should come back on, and all the DDS's in the pulser will flash briefly.  
## Lasers 
1) [[369]]: 
	- Make sure lock switches are off. Toggle on/off switch, current should come up to ~80mA 
2) [[399]]: 
	- There's a "Module On' button all the way to the right on the controller. Press this 
3) [[935]]: 
	- There's a TEC and Current button. Press TEC and then the current so that both show blue lights 
4) [[411]]: 
	- Make sure lock switches are off. Toggle on/off switch, current should start
5) [[760s]], [[935]]/976dbr: 
	- TEC on, then current.
	- For the 760s, you may need to play with the current and temperature to get them to the correct frequencies
## Software 
1) Probably just restart the gui real quick to see if you get the wavemeter and camera widgets 
2) May have to restart pulser server and the normal pmt flow server 
## Try to load!
- For day to day loading, check the [[Startup Checklist]]
