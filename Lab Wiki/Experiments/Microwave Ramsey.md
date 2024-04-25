The microwave Ramsey experiment consists of a $\pi/2$ pulse followed by a delay time, followed by another $\pi/2$ pulse.

For each point on the graph (plotting probability to be in excited state on the vertical axis and delay time on the horizontal) the probability is obtained from several trials. Each trial consists of the following sequence:

1. [Optical pumping](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/Experiments/normal%20qubit%20operation.md#optical-pumping) initializes the ion to the $\ket{^2S_{1/2}, F=0}$ ground state.
2. Microwaves are applied to the ion for the duration needed for a $\pi/2$ pulse (running a [Rabi Flopping](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/Experiments/Rabi%20Flopping.md) experiment beforehand to get an accurate $\pi$ time is a good idea).
3. No pulses trigger as the system evolves freely in time for some given delay time $\tau$.
4. Microwaves are applied to the ion for the duration needed for a $\pi/2$ pulse.
5. [Standard state detection](https://github.com/CampbellGroup/Wiki/blob/main/Lab%20Wiki/Experiments/normal%20qubit%20operation.md#standard-state-detection) is used to determine if we are in our bright ($\ket{^2S_{1/2}, F=1}$) or dark ($\ket{^2S_{1/2}, F=0}$) state.

This process is repeated for some "N'' trials at each point of an array of different delay times $\tau$. This iteration over multiple different delay times produces the Ramsey experiment graph.
# Purpose

Microwave Ramsey experiments give us a more accurate measure qubit frequency than typical microwave line scans. After the $\pi/2$ pulse takes the qubit from $\ket{\uparrow}$ to $\ket{+x} = \frac{1}{\sqrt{2}}\left(\ket{\uparrow}+\ket{\downarrow}\right)$, it rotates around the Bloch sphere in the x-y plane. In the rotating frame of the atomic transition being driven, the state will rotate the rate of the detuning $\Delta\omega=\omega_{atomic} - \omega_{laser}$. After rotating in the x-y plane for some time $t$ the state has swept out an angle $\Delta\omega t$. Now after the second $\pi/2$ pulse (about the same axis as the first $\pi/2$ pulse) the projection onto the $\ket{\downarrow}$ state is $cos(\Delta\omega t)$. This means that the probability will trace out a cosine: 
$$|\braket{\downarrow}{\psi(t)}|^2 = cos^2(\Delta wt) = 1/2 + (1/2)cos(2\Delta w t)$$ We may then fit this cosine trace for a more accurate measure of $\Delta w$ than we could obtain via a normal microwave line scan.
