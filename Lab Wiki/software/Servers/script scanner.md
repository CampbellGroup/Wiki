Script scanner is a [[LabRAD]] server that is a part of [[the core LabRAD paradigm]], along with the [[data vault]] and the [[parameter vault]]. Script scanner is responsible for executing experiment scripts and processing the resultant data. 

## The Script Scanner Interface

In the [[Qsim GUI]], there is a tab devoted to the Script Scanner and parameter vault. On the left side are five elements: 
#### Script selector
Select the experiment file to load. The experiment files that are available here are configured in `config/scriptscannerconfig.py`. An example config entry is `('Qsim.scripts.experiments.Fidelity_Tweak_Up.fidelity_tweak_up', 'FidelityTweakUp')`
In other words `(path_to_experiment_subclass, name_of_experiment_subclass)`

In addition, you can Run, Repeat, or Schedule experiments (Scan doesn't work very well). Usually you'll just run experiments one time, bit sometimes it can be useful to schedule things at regular intervals, such as interleaved line scans, for instance. 
If you tell a script to run while another script is already running, it will be queued to run immediately afterwards. 
#### Docstring viewer

Shows the docstring of the script. When writing a script, the docstring should include the following:
- a brief description of what the script does
- ideally at least one example pulse sequence diagram

this will get a better write up in the [[codebase style guide]]
#### The other three
The other three panels show lists of the scheduled, queued, and running scripts. 

To make a script cancelable, the script's main `run` loop should contain some variation of the following block of code:
```python
should_break = self.update_progress(self.progress)
if should_break:
	break
```
The `update_progress()` function is defined in the [[QsimExperiment]] class. It both updates the progress bar in the GUI, and checks whether the experiment has received a signal to stop running. 
## Experiment Files

Experiment files are the highest level of the hierarchy of scripts that make up an experiment. Each experiment file should define at least one class that subclasses [[QsimExperiment]].

Experiment files a few methods that should be implemented: 
#### initialize()
Initialize the experiment. Open any connections with other servers, set up local variables, and potentially set up data logging. 
#### run()
The core experimental code. Generally this is where the [[data vault]] might get set up, where the [[pulser]] night get programmed, and where the experimental data gets processed. 
## Pulse Sequences

Pulse sequences represent sequences of pulses sent to the pulser. These are generally compositions of multiple sub-sequences, possibly with some basic logic about which sequences to compose. They tend to be short, so here's an example in full: 
```python
# [various import statements]

class MicrowavePoint(pulse_sequence):

    required_subsequences = [TurnOffAll, DopplerCooling,
                             MicrowaveInterrogation,
                             StandardStateDetection, ShelvingStateDetection, Deshelving,
                             OpticalPumping, Shelving, ShelvingDopplerCooling, ]

    required_parameters = [
        ('Modes', 'state_detection_mode'),
        ('MicrowaveInterrogation', 'repetitions')
        ]

    def sequence(self):
        p = self.parameters
        mode = p.Modes.state_detection_mode

        self.addSequence(TurnOffAll)

        if mode == 'Standard' or mode == 'StandardFiberEOM':
            self.addSequence(DopplerCooling)
            self.addSequence(OpticalPumping)
            for i in range(int(p.MicrowaveInterrogation.repetitions)):
                self.addSequence(MicrowaveInterrogation)
            self.addSequence(StandardStateDetection)
        elif mode == 'Shelving':
            self.addSequence(ShelvingDopplerCooling)
            self.addSequence(OpticalPumping)
            for i in range(int(p.MicrowaveInterrogation.repetitions)):
                self.addSequence(MicrowaveInterrogation)
            self.addSequence(Shelving)
            self.addSequence(ShelvingStateDetection)
            self.addSequence(Deshelving)
```
In summary, a pulse sequence should generally contain mostly a string of `self.addSequence()` calls, with the sequences themselves stored in the sub-sequences directory. 
***Remember to put any parameters referenced in the pulse sequence into the `required_parameters` list, and ant sub-sequences used into the `required_subsequences` list. both are defined at the top of the class declaration. ***
## Sub-Sequences
Sub-sequences are where the code actually talks to the [[Pulser]]. Here's a snippet of example code: 

```python
from common.lib.servers.Pulser2.pulse_sequences.pulse_sequence import pulse_sequence
from labrad.units import WithUnit as U

class OpticalPumping(pulse_sequence):

    required_parameters = [
        ('OpticalPumping', 'duration'),
        ('OpticalPumping', 'power'),
        ('OpticalPumping', 'detuning'),
        ('OpticalPumping', 'repump_power'),
        ('OpticalPumping', 'method'),
        ('OpticalPumping', 'quadrupole_op_duration'),
        ('OpticalPumping', 'quadrupole_op_detuning'),
        ('OpticalPumping', 'extra_repump_time'),
        ('Transitions', 'main_cooling_369'),
        ('ddsDefaults', 'optical_pumping_freq'),
        ('ddsDefaults', 'optical_pumping_power'),
        ('ddsDefaults', 'repump_935_freq'),
        ('ddsDefaults', 'repump_760_1_freq'),
        ('ddsDefaults', 'repump_760_1_power'),
        ('ddsDefaults', 'repump_760_2_freq'),
        ('ddsDefaults', 'repump_760_2_power'),
        ('ddsDefaults', 'DP369_freq'),
        ('ddsDefaults', 'DP2_411_power'),
        ('ddsDefaults', 'DP2_411_freq'),
        ('ddsDefaults', 'repump_976_freq'),
        ('ddsDefaults', 'repump_976_power'),
        ('Modes', 'laser_369')
    ]

    def sequence(self):
        p = self.parameters

        mode = p.Modes.laser_369

		if mode == 'standard':
			#  other cases omitted for brevity in this example snippet
			pass
        elif mode == 'FiberEOM':
            self.addTTL('WindfreakSynthNVTTL',
                        self.start,
                        p.OpticalPumping.duration)
            self.addTTL('WindfreakSynthHDTTL',
                        self.start,
                        p.OpticalPumping.duration)
            self.addDDS('369DP',
                        self.start,
                        p.OpticalPumping.duration,
                        p.Transitions.main_cooling_369/2.0 + p.ddsDefaults.DP369_freq + p.OpticalPumping.detuning/2.0,
                        p.OpticalPumping.power)
            self.addDDS('935SP',
                        self.start,
                        p.OpticalPumping.duration + p.OpticalPumping.extra_repump_time,
                        p.ddsDefaults.repump_935_freq,
                        p.OpticalPumping.repump_power)
            self.addDDS('760SP',
                        self.start,
                        p.OpticalPumping.duration + p.OpticalPumping.extra_repump_time,
                        p.ddsDefaults.repump_760_1_freq,
                        p.ddsDefaults.repump_760_1_power)
            self.addDDS('760SP2',
                        self.start,
                        p.OpticalPumping.duration + p.OpticalPumping.extra_repump_time,
                        p.ddsDefaults.repump_760_2_freq,
                        p.ddsDefaults.repump_760_2_power)
            self.end = self.start + p.OpticalPumping.duration + p.OpticalPumping.extra_repump_time
```
***Remember to put any parameters referenced in the pulse sequence into the `required_parameters` list, and ant sub-sequences used into the `required_subsequences` list. both are defined at the top of the class declaration. ***