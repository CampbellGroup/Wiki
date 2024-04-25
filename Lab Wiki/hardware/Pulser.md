The pulser is the beating heart of our experiment. There is a page about it on the Campbell lab wiki, which is replicated and expanded upon here: 

# FPGA Pulser 2

Built by Hong in Riken. The paper is [here](http://arxiv.org/pdf/1507.03122v1.pdf).

Powered by the opal kelly 6010 see [here](http://10.97.112.13:4567/opal-kelly-6010) for more information

There is also a Github wiki on the pulser with lots useful information found [here](https://github.com/thetorque/pulse_sequencer/wiki).

## Environment and installation
 - Notes about the environment and installation
    * Use 64-bit py2 environment
    * Install Opal Kelly. Download the file under `Group_Share\software\Opal Kelly` and run FrontPanelUSB-Win-x64-4.5.0.exe
    * Copy the ok file under Group_Share\software to the correct file under your environment. For me it's `C:\Users\scientist\AppData\Local\conda\conda\envs\py2\Lib\site-packages`
    * Go to pulser config (`C:\Users\scientist\code\config\pulser\hardwareConfiguration.py`) and make sure everything is good(described by the following paragraph).

## Hardware Config File

This file determines many of the boards settings and needs to be correctly written for the pulser to operate. Starting with a working [file] (https://github.com/CampbellGroup/qsim_config/blob/master/pulser/hardwareConfiguration.py) from one of the other experiments is the best way to start.
  - Important notes about the hardware config file
    * Make sure the okDeviceID is correct. I run into errors with 'pulser 2' and I changed it to 'Pulser2' and it worked.
    * Not every TTL channel can be switched manaully. See the breakout board section below
    * The variable "self.boardfreqrange" is the DDSs clock frequency you need to supply to the DDSs. We default this to 2GHz.
    * There is a dictionary at the bottom of the file for labeling the available DDSs. The address in the dictionary for each DDS corresponds to the address physically set on the DDS with a jumper. See DDS below.

### Reserved internal channels
You cannot use all channels as TTL outputs since some are reserved for internal triggers or specific outputs. The breakout board was not designed with this knowledge so some BNC's just act as references to internal triggers. The reserved channels I know about are 0,1 and 16-20:

                   'Internal866':channelConfiguration(0, False, False, False, False), ## camera
                   '866DP':channelConfiguration(1, False, False, True, False),
                   'TimeResolvedCount':channelConfiguration(17, False, False, False, False),
                   'DiffCountTrigger':channelConfiguration(16, False, False, False, False),
                   'AdvanceDDS':channelConfiguration(18, False, False, False, False),
                   'ResetDDS':channelConfiguration(19, False, False, False, False),
                   'ReadoutCount':channelConfiguration(20, False, False, False, False), ### triggering for analog board

## Power Requirements
The pulser board needs two 5V and one 8V power supplies. The 5V digital input is all you need for TTL pulsing while the 5V and 8V analog are required for using the DDSs. The main Opal Kelly FPGA also requires a 5V power supply (barrel connector)  in addition to the USB connection to the computer. 
**IMPORTANT: plug the 5V barrel connector into the FPGA adapter board not the FPGA itself**, we have noticed grounding problems causing the pulser to freeze in the wrong configuration.

Currently, the pulser is powered by two power supplies: 
- an HP 6033A provides the 5V DC required by the pulser. It should be configured to provide 5V, and at least 15 A. For details on how to turn it on, see [[Full Lab Startup guide#Pulser]]
- an Acopian Gold Box that's pretty much always on supplies the 8V rail. 
## Breakout Board

The breakout board was designed by Youna Park to allow access to the pulser I/Os. The pulser is 3.3V and the breakout board converts these to TTL. The connection from pulser to the breakout board is shown in the pictures below.

![[Pasted image 20230804154820.png]]{width=50%}]]
![[Pasted image 20230804154839.png]]
## TTL Out

Channels 2-11 on the pulser are configurable to manual mode. These correspond to channels 5-14 on Youna's breakout board. 

Channels 0,1 are used for differential mode with [[the PMT]]. These are channels 3,4 on the breakout board. It looks like the state is inverted when counting in differential mode. This can be changed in the hardwareconfiguration file. 

## DDS
Each DDS plugs into the PCI slot on the pulser board and requires both 5V power supplies, and the 8V power supply be connected (DDS boards light up without 5V and 8V analog voltages). They require an input clock defined by the "boardfreqrange" in the hardware config file. Each board address is defined using the address pins (4 bits total (see paper for picture)). Jumpers are used to change each vertical pair of pins from a 0 to a 1, with the LSB being the far right pair when referencing the picture in the paper. 