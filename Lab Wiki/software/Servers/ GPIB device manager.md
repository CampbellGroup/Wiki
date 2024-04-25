---
aliases:
  - GPIB bus
  - GPIB device manager
---


The GPIB bus and the GPIB device manager run on the [[Camera computer]] and are used to interact with GPIB devices. The only current server for a GPIB device is the [[keithley 2230G server]], which is one part of the [[oven server]]. Generally, these servers need to be restarted in the order GPIB Bus -> GPIB device manager, as seen in [[Restarting the Oven]]

1. GPIB Bus 
	- The server that makes the hardware GPIB bus on the camera computer available to LabRAD
2. GPIB Device Manager 
	-  The server that runs all the GPIB devices connected to the camera computer