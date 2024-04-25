The chain of servers that connects the "oven" button on the GUI to the actual power supply running the oven is a finicky one. If it's not working, the best bet is to restart the servers in the correct order:
1. GPIB Bus 
2. GPIB Device Manager 
3. Keithley 2230G Server 
4. Oven Server

The rationale: 
1. GPIB Bus 
	- The server that makes the hardware GPIB bus on the camera computer available to LabRAD
2. GPIB Device Manager 
	-  The server that runs all the GPIB devices connected to the camera computer
1. Keithley 2230G Server 
	- The server that runs the physical power supply that powers the oven
1. Oven Server
	- The server that connects to [[NormalPMTFlow]] and the Keithley 2230G to run the oven until an ion has loaded