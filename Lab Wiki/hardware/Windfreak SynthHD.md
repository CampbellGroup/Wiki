The Windfreak SynthHD is a pretty reliable RF oscillator with some pretty annoying quirks. 

For historical reasons, this is the device generally referred to as the "windfreak" in our codebase, not the [[Windfreak SynthNV]]. 

The Windfreak SynthHD currently feeds into the [[ADVR EOM]] via a diplexer and a low-noise amplifier, in order to apply sidebands for 171Yb and 173Yb doppler cooling. 
## Directions for use
- The SynthHD can be controlled via the "windfreak" LabRAD server, or via the windows "SynthHD" program on the camera computer. Just make sure that whichever you pick, the USB is plugged into the appropriate computer. 
- The synthHD has an annoying tendency to lose its reference. This leads to a weird line shape and inaccurate frequencies. Every day (or at least every few days), the internal reference should be reset. To do this, run `ipython` in a terminal window and type the following:
	```python
	import labrad
	cxn = labrad.connect()
	w = cxn.windfreak
	w.set_reference_mode("external")
	w.set_reference_mode("internal 27mhz")
	```
	Doing this should reset the reference of the windfreak and solve any issues if they exist
- In [[normal qubit operation]], the SynthHD should be set to trigger externally. This should already be the case, but just in case, here's how you do it in iPython: 
	```python
	import labrad
	cxn = labrad.connect()
	w = cxn.windfreak
	w.set_trigger_mode("rf enable")
	```
	The SynthHD is controlled via a TTL on the [[Pulser]] called "WindfreakSynthHDTTL". This TTL is configured strangely:
	- When being manually controlled, the TTL buttons in the GUI turn the tone on and off like you'd expect, with the "Auto" state having the RF on.
	- When being controlled in a pulse sequence, the `addTTL` command is inverted: **it should be inserted where you *don't* want there to be RF**. This is very annoying, but it has to do with the limitations of the Pulser's auto mode. 