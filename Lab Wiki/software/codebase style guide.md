Please please please abide by the following style conventions when editing code. Some of them are dumb, but if we change them now it only makes things more confusing. 

In general, we outsource to the [Google Style Guide](https://android.googlesource.com/platform/external/google-styleguide/+/refs/tags/android-s-beta-2/pyguide.md) for a great deal of our code style decisions, and the PyCharm linter is mostly configured for this so you won't need to check it much.  

## Directory spelling conventions
The capitalization of things at the same hierarchy level should be consistent. Classes are CamelCase, python files should be snake_case, and folder names should be snake_case. However, the experiment capitalization is inconsistent as of now, so just apply these rules going forward. 

Example hierarchy
```cs
scripts
>>> experiments
>>> >>> Qsim_Experiment
>>> >>> >>> qsim_experiment.py
>>> >>> >>> >>> class QsimExperiment
>>> pulse_sequences
>>> >>> pulse_sequence.py
>>> >>> >>> class PulseSequence
>>> >>> sub_sequences
>>> >>> >>> sub_sequence.py
>>> >>> >>> >>> class SubSequence
```

## Experiment docstrings

**Note that python 2 experiment files that use these characters need to have the following comment at the top of the file to specify the encoding: `# -*- coding: utf-8 -*-`**

When you write an experiment script, I think it's good form to write a docstring that explains in detail what the experiment does. I believe this so strongly that I modified the [[script scanner]] gui to display these docstrings. Here's an example of a docstring for Microwave Ramsey Experiment: 
```
    Scan delay time between microwave pulses with variable pulse area  
    Pulse sequence diagram:  
Standard:  
    369SP            |████████████████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████    
    DopplerCoolingSP |████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁    
    StateDetectionSP |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████    
    OpticalPumpingSP |▁▁▁▁▁▁▁▁▁▁▁▁████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁    
    MicrowaveTTL     |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁█████▁▁▁▁▁▁▁▁▁█████▁▁▁▁▁▁▁▁▁▁▁▁    
    Microwave_qubit  |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▓▓▓▓▓▁▁▁▁▁▁▁▁▁▓▓▓▓▓▁▁▁▁▁▁▁▁▁▁▁▁    
    935SP/976SP      |████████████████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████    
    760SP/760SP2     |████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁    
    ReadoutCount     |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████         
	    (TurnOffAll) DC          OP          RMI    ~~~~~~~~~     StandardSD  
FiberEOM:  
    369SP            |████████████████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████    
    WindfreakSynthHD |▁▁▁▁▁▁▁▁▁▁▁▁████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████    
    WindfreakSynthNV |▁▁▁▁▁▁▁▁▁▁▁▁████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁    
    MicrowaveTTL     |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁█████▁▁▁▁▁▁▁▁▁█████▁▁▁▁▁▁▁▁▁▁▁▁    
    Microwave_qubit  |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▓▓▓▓▓▁▁▁▁▁▁▁▁▁▓▓▓▓▓▁▁▁▁▁▁▁▁▁▁▁▁    
    935SP/976SP      |████████████████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████    
    760SP/760SP2     |████████████▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁    
    ReadoutCount     |▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁████████████         
	    (TurnOffAll) DC          OP          RMI    ~~~~~~~~~     StandardSD
```

As a rule, I like to include a pulse sequence diagram for any pulse sequences that are used for the experiment. Along the bottom are labels for the different sub-sequences being used. DDSes and TTLs are represented by:
- `█████` if on
- `▁▁▁▁▁` if off (note that this isn't an underscore)
- `▓▓▓▓▓` if on, with a parameter (such as frequency) is being varied
- If the duration of one of the sub-sequences is being varied, I like to put tildes under that sub sequence

