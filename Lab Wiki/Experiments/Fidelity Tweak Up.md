This program creates a histogram for dark and bright state preparation, where the horizontal axis is photon counts. 

The dark state is prepared N times via [[Optical pumping]], and is followed by [[Standard state detection]] each time to create the photon count histogram of the dark states. 

The bright state can be prepared in two ways:
- via [[Optical pumping]] followed by a Rabi flop
- via straight doppler cooling (which tends to populate the F=1 state more often than the F=0)
Usually the Rabi flop method is used, unless microwaves aren't operational. 

Each experiment is followed by state detection each time to create the photon count histogram of the bright state. 

To have good fidelity we need the states to be as distinguishable as possible, such that we aim to minimize the overlap of the bright and dark state histograms. We do this by adjusting state preparation parameters such as laser power, optical pumping duration, and standard state detection duration. **These parameters can be changed as the experiment is running.** If the bright state is prepared via a microwave pi-pulse, running a [[Rabi Flopping]] experiment to get a more accurate pi time can also help improve fidelity.