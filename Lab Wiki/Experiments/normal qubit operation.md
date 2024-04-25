Normal qubit operation refers to the way we run our experiment for quantum computing. That is, we prepare our hyperfine qubit in the ground state, and do essentially all of our operations with 369nm light. This is in contrast with [[shelved qubit operation]], in which we shelve one of the qubit states to the $^2 F_{7/2}$ state. This is often called "standard" in the codebase. 

It should also be noted that this only applies for 171Yb. For 173Yb see [173Yb operation]()

Here, I'll describe the scheme for normal operation in the case of our [ADVR EOM](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/hardware/ADVR%20EOM.md) system. For how the system historically worked, click the links for elaboration. 
## [Doppler cooling](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/ytterbium/Doppler%20cooling.md)

> [!TODO] Insert an image of the doppler cooling scheme here

Doppler cooling with the fiber EOM involves driving two sets of transitions: One from F=0 -> F=1, and one from F=1 -> F=0. These two tones are separated by the sum of the hyperfine splittings of the S and P states: 12.642 GHz + 2.105 GHz = 14.74... GHz. 

We achieve this with a 7.374GHz tone on the [Windfreak SynthHD](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/hardware/Windfreak%20SynthHD.md) oscillator at about -10 dBm, which drives a second-order sideband on the EOM. 

## [Optical pumping](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/ytterbium/Optical%20pumping.md)

> [!TODO] Insert an image of the optical pumping scheme here

Optical pumping with the fiber EOM involves driving the F=1 -> F=1 transitions. Since the P state F=1 manifold can decay to both the F=1 and the F=0, this pumps the ion into the F=0 state. Population transfer usually takes less than 50 us. 

This requires moving the frequency of our light by the P-state splitting of 2.105 GHz. We do this using the [Windfreak SynthNV](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/hardware/Windfreak%20SynthNV.md), operating at -4 dBm (or whatever power best depletes the carrier).
## [Standard state detection](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/ytterbium/Standard%20state%20detection.md)

> [!TODO] Insert an image of the state detection scheme here

State detection involves a closed cycle between the S-state F=1 manifold, and the P-state F=0 manifold. Since the decay from F=0 to F=0 is forbidden, we can cycle on this transition many times before decohering the qubit. The main decoherence mechanism is off-resonant scattering the P=state F=1 manifold. 

The carrier is parked on this transition, so during state detection, all EOM tones are **off**. 
