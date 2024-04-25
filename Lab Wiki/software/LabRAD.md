LabRAD is the core of our experiment's software base. Fundamentally, it provides an *asynchronous* communication protocol between all the devices in the lab.

## [[Installing LabRAD]]
Installing LabRAD is a huge pain. Avoid if possible. For now, use [this link](http://10.97.112.13:4567/LabRAD) to the CampbellGroup Wiki. 

## Running LabRAD
On the experimental control computer, you can start labrad by typing 
```bash
python -m labrad.node 
```
into a fresh terminal window. Preferably, you can open Tabby and open a terminal window with the LabRAD profile, which will cause it to run automatically.

On other devices, LabRAD will be started in different ways, usually with a .bat script that's easily accessible. 
## Opening the LabRAD control panel

LabRAD has a graphical control panel in-browser. To access it, go to [http://localhost:7667](http://localhost:7667/). UNFORTUNATELY, LabRAD only supports chromium versions <= 80, so on the experimental control computer, we maintain a legacy build of the vivaldi browser specifically for running the control panel. 

For more details on the control panel, see [[the LabRAD control page]]

# LabRAD concepts

## Servers
Servers are python scripts that add functions to LabRAD. These can be as complex as interfacing with a device, or as simple as multiplying two numbers together. A LabRAD server is a subclass of the `LabradServer` class. 

A server should always implement the following functions (unless they would be empty): 
- `initServer`: should contain any code that should run once at server startup
- `stopServer`: should contain any code that needs to run before the server shuts down

In addition to these functions, the server can expose any number of other functions to the LabRAD interface using the `@setting` decorator. (For reasons that are beyond me, functions that are exposed to LabRAD are called "settings"). For example (from NormalPMTFlow):
```python
@setting(2, "Set Mode", mode='s', returns='')  
def setMode(self, c, mode):  
    """  
    Start recording Time Resolved Counts into Data Vault
    """    
    if mode not in self.modes:  
        raise Exception('Incorrect Mode')  
    if not self.recording.running:  
        self.currentMode = mode  
        yield self.pulser.set_mode(mode)  
    else:  
        yield self.dostopRecording()  
        self.currentMode = mode  
        yield self.dorecordData()  
    otherListeners = self.getOtherListeners(c)  
    self.onNewSetting(('mode', mode), otherListeners)
```
The `@setting` decorator takes the following arguments:
- positional arguments:
	- ID: a unique integer ID for the setting
	- name: a name for the setting
- keyword arguments:
	- One keyword argument is required for each parameter of the function being decorated. It should be assigned a string with the LabRAD type of the parameter. 
	- returns: If the function returns, the LabRAD type of the value being returned. 
One more thing to note: Instead of the function having the signature `func(self, arg1, arg2)`, it has the signature `func(self, c, arg1, arg2)`. This `c` value is used by the LabRAD context manager somehow. 
For clarity on what the `yield` statements are doing in the above expression, see [[asynchronous programming concepts]]. 
## Clients
A LabRAD client is essentially what we call any program that isn't a LabRAD server but that still talks to LabRAD. Practically speaking, these are mostly GUIs and other user-facing programs that connect LabRAD functions to interfaces that are easier to use. 
# Navigating LabRAD via the command line
## Opening a LabRAD connection
When LabRAD is running, you can connect to LabRAD through python using the `conect()` function. This will return a labRAD connection that you can use to access all running labRAD servers:  
```python
>>> import labrad
>>> cxn = labrad.connect()
```
for all future code snippets, these two lines will be implied. 
## Accessing servers
In LabRAD, a *server* is a script that LabRAD runs that exposes some set of functions to the LabRAD interface. Typing the name of your LabRAD connection into iPython without arguments will simply list all active LabRAD servers: 
```python
>>> cxn
'''LabRAD Client: 'Python Client (mj)' on localhost:7682

Available servers:
    andor_server
    arduinottl
    auth
    bristol_521
    dac_ad660_server
    data_vault
    dg1022_rigol_server
    evpump
    gpib_device_manager
    grapher
    keithley_2230g_server
    keithley_server
    manager
    mj_serial_server
    multiplexerserver
    multipole_server
    node_mj
    node_qsim_camera
    normalpmtflow
    ovenserver
    parametervault
    piezo_server
    pulser
    qsim_camera_gpib_bus
    registry
    scriptscanner
    windfreak
```
Accessing a specific server without arguments lists its functions: 
```python
>>> pmt = cxn.normalpmtflow
>>> pmt
'''LabRAD Server: NormalPMTFlow (ID=15)

Settings:
    currentdataset
    debug
    echo
    get_next_counts
    get_time_length
    get_time_length_range
    getcurrentmode
    isrunning
    record_data
    set_mode
    set_save_folder
    set_time_length
    signal__log
    signal__new_count
    signal__new_setting
    start_new_dataset
    stoprecording
```
and accessing a server function without arguments gives its documentation (if any):
```python 
>>> pmt.get_next_counts
'''LabRAD Setting: "NormalPMTFlow" >> "Get Next Counts" (ID=9)

Acquires next number of counts, where type can be 'ON' or 'OFF' or 'DIFF' Average is optionally True if the counts should be averaged

Note in differential mode, Diff counts get updates every time, but ON and OFF get updated every 2 times.

Accepts:
    (sw)
    (swb)

Returns:
    *v
    v
```

Regardless of whether a docstring is provided or not, the `Accepts` and `Returns` sections will always be given. These tell you the argument types that the function accepts and returns, using the [LabRAD type notation](https://sourceforge.net/p/labrad/wiki/DataTypes/), reproduced in brief at  [[LabRAD#LabRAD Types]].

# Important LabRAD servers

![[LabRAD Server Map]]
## [[the core LabRAD paradigm]]
There are several server that are integrated deeply into our LabRAD workflow. They are explained briefly here, and their interactions are expanded upon in the page linked above:

| server | role| 
|---|---|
| [[script scanner]] | reads and executes experiment files. This includes sending signals and processing the data they produce
| [[data vault]] | takes data from script scanner and maintains a filesystem of .csv files containing data and .ini files containing experimental parameters
| [[parameter vault]] | stores experimental parameters in the LabRAD registry and makes them available to experiments
## Other important servers
| server | role| 
|---|---|
| [[serial server]] | exposes USB ports to LabRAD for interfacing with USB devices
| [[ GPIB device manager]] | exposes GPIB devices to LabRAD
| [[RealSimpleGrapher]] | plots data from the [[data vault]] in real time, provides fitting and other functionality
| [[Pulser]] | executes pulse sequences for controlling the ion, operates all of our DDS's and most of our TTL's
| [[DAC ad660 server]] | Controls the DC trap electrodes

# LabRAD Types
#### Basic Types
|**Tag**|**Name**|**Description**|**Example Data**|
|---|---|---|---|
|**b**|Boolean|Flag|True|
|**i**|Integer|Signed whole number|-1,500,000,000|
|**w**|Word|Unsigned whole number|3,750,000,000|
|**s**|String|Text|"Hello World"|
|**v**|Value|Real number|-1.637e23|
|**c**|Complex|Complex number|3.2 + 1.6i|
|**t**|TimeStamp|Time and date|1/15/2006 12:53pm|
|**?**|Any|Placeholder for any type|_N/A_|
|**\_**|Empty|Unspecified array type|_N/A_|
#### Composite Types
|**Tag**|**Name**|**Description**|**Example Type Tag and Data**|
|---|---|---|---|
|\***?** or \***n?**|Array|List of data with n dimensions|\***s**: "Karl", "Peter", "Tom"|
|**(**...**)**|Cluster|Collection of data|**(sw)**: "Karl", 27|
|**E** or **E?**|Error|Error message|**E**: 15: "Can't divide by 0!"|
#### Type Modifiers
|**Tag**|**Name**|**Description**|**Example Type Tag**|
|---|---|---|---|
|**\[**...**\]**|Units|[Units](https://sourceforge.net/p/labrad/wiki/Units/) of a Value or Complex||**v\[GHz\]**|
|**_{_**...**_}_**|Comment|Type tag annotation|**s\_{Name}\_**|
|**:**...|End|Marks the end of the type tag|**b_: Turn instrument on(T)/off(F)_**|

# LabRAD Units

Often in LabRAD servers, you'll need to use unitful values. LabRAD provides a library to do this called `Units`, and therefore you'll often see the following import at the top of LabRAD servers: 
```python
from labrad.Unit import WithUnit as U
```
This allows you to use LabRAD unit syntax, and conversions and compatibility will be handled for you. 
```python
>>> freq1 = U(100.0, "MHz")
>>> freq2 = U(1000.0, "kHz")
>>> freq1 + freq2
"Value(101000.0, 'kHz')"
>>> mass1 = U(1, "kg")
>>> freq1 + mass1
"TypeError: Incompatible units: MHz, kg"
```
Complete documentation of the Labrad units can be found [here](https://sourceforge.net/p/labrad/wiki/Units/). 