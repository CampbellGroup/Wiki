For each point on the graph (plotting probabilities on the vertical axis and time on the horizontal) the probabilities are obtained from several trials. Each trial consists of the following sequence:

1. [[Optical pumping]] initializes the ion to the $\ket{^2S_{1/2}, F=0}$ ground state.
2. Microwave radiation is applied to the ion for some time $t$ (Rabi flopping theory tells us the probability to flip is proportional to $sin^2(\Omega't/2)$).
3. [[Standard state detection]] is used to determine if we are in our bright ($\ket{^2S_{1/2}, F=1}$) or dark ($\ket{^2S_{1/2}, F=0}$)) state.

This process is repeated for some "N'' trials at each point of an array of times $t$ for which microwave radiation is to be applied. This iteration over multiple different times produces the Rabi flopping graph.

As the trace produces a $sin^2(\Omega't/2)$ curve, we may fit the resulting plot to get an accurate pi time $t_\pi = \pi/\Omega'$. Updating this pi time parameter in [[script scanner]] will improve fidelity in state preparation by microwave pulses.