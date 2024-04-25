See Atomic Physics, Foot, pages 155-163 for a more detailed description. 
Note that this technique is used in our [[Rubidium Saturated Absorption Spectroscopy PDH Lock]].
## Doppler Broadening
Atoms in a gas have a gaussian velocity distribution about zero given by the maxwell velocity distribution. To an atom moving at velocity $v$, a laser of frequency $\omega$ will have an apparent frequency of $\omega-kv$ (where $k$ is the laser wavenumber and the positive direction is that of the laser propagation) due to the Doppler effect. Suppose we scan frequency over a transition that has natural resonance $\omega_0$; because of the Doppler shift, the condition on $\omega$ for resonance is $\omega-kv=\omega_0$, such that $\omega=\omega_0+kv$ and we see that different different velocities will resonate at different laser frequencies. Because resonance is dependent on velocity and the atoms follow a gaussian distribution of velocities, the transition linewidth will have inhomogeneous broadening referred to as "Doppler broadening." Saturation Absorption Spectroscopy aims to get rid of this Doppler broadening and leave just the more narrow, natural homogenous broadened linewidth. 
## SadAbs Basic Principle
Set a laser to pass through a sample cell (such as Rubidium) and into a photo-diode and one will observe the signal to decrease and trace out a Doppler broadened spectrum as they scan the laser frequency about an atomic transition. As the resonance condition is $\omega -kv=\omega_0$, we see that a given frequency $\omega$ will excite a certain velocity class $v=(\omega-\omega_0)/k$. 
The idea of SadAbs is to have a second, more powerful laser also incident on the sample that will saturate the transition for the $v=0$ velocity class, such that the weaker laser will not drive the transition for the $v=0$ class and instead pass through the sample and into the photo-diode to create a narrow peak inside the Doppler broadened spectrum. 

The weak beam is referred to as the probe and the strong beam is called the pump, and they are set to counter propagate through the sample. Because the pump counter propagates, the atoms see it with an apparent frequency of $\omega +kv$, such that for laser frequency $\omega$ the pump beam excites $v_{pump}=-(\omega-\omega_0)/k$ while the probe excites $v_{probe}=(\omega-\omega_0)/k$. The pump and probe excite different velocity classes of atoms, and so the photo diode signal is not effected except when $v_{pump}=v_{probe}$, such that $-(\omega-\omega_0)/k=(\omega-\omega_0)/k$, which simplifies to $\omega=\omega_0$ and $v_{pump}=v_{probe}=0$. 
## Cross Over Resonances
Now imagine a more realistic atom with multiple transitions possible, and take for example two natural resonances $\omega_{01}$ and $\omega_{02}$. Now we see the velocity classes that will be excited by the pump and probe are:
$v_{pump,1}=-(\omega-\omega_{01})/k$ and $v_{pump,2}=-(\omega-\omega_{02})/k$
$v_{probe,1}=(\omega-\omega_{01})/k$ and $v_{probe,2}=(\omega-\omega_{02})/k$
We will still see peaks at $\omega=\omega_{01}$ and $\omega=\omega_{02}$, however there will be a point at which the pump excites the $\omega_{02}$ transition while the probe tries to drive the $\omega_{01}$ transition on the same velocity class. In this case probe power passes through the sample and creates a peak on the photo-diode signal as the pump has excited the velocity class of atoms that the weak probe tried to excite. This condition is met when $v_{probe,1}=v_{pump,2}$, such that $(\omega-\omega_{01})/k=-(\omega-\omega_{02})/k$ which occurs when $\omega = (\omega_{01}+\omega_{02})/2$. These "cross over resonances" are not true resonances of the atom, but rather appear midway between true resonances. 
## AOM Shift to Saturated Absorption Peaks
In our system the pump beam is double passed by an AOM. This means that the probe beam has frequency $\omega_{probe}$ and the pump $\omega_{pump}=\omega_{probe}+2\Delta_{AOM}+2\delta_{mod}sin(\omega_dt)$, where $\Delta_{AOM}$ is the single pass first order frequency shift that the AOM imparts on the beam, $\delta_{mod}$ is the modulation depth, and $\omega_d$ is the dither frequency. The modulation is centered on zero and much smaller than the AOM shift, so we may neglect this term. As explained above, we have saturated absorption features when the pump and probe excite atoms in the same velocity class, and the atoms will see the light Doppler shifted such that the resonance condition becomes:
$\omega_{pump}+k_{pump}v_{pump} = \omega_{0,j}$ => $(\omega_{probe}+2\Delta_{AOM} +2\delta_{mod}sin(\omega_dt))+k_{pump}v_{pump}= \omega_{0,j}$ or approximately
$(\omega_{probe}+2\Delta_{AOM})+k_{pump}v_{pump}= \omega_{0,j}$ and
$\omega_{probe}-k_{probe}v_{probe} = \omega_{0,i}$
The condition for a feature is $v_{pump}=v_{probe}$, so solving each of the above for velocity:
$v_{probe}=\frac{\omega_{probe}-\omega_{0,i}}{k_{probe}}$ and
$v_{pump}=-\frac{\omega_{probe}+2\Delta_{AOM}-\omega_{0,j}}{k_{pump}}$
Now as $k_{pump} = \omega_{pump}/c = \left(\omega_{probe}+2\Delta_{AOM}+2\delta_{mod}sin(\omega_dt)\right)/c \approx \left(\omega_{probe}+2\Delta_{AOM}\right)/c$
$1/k_{pump} \approx 1/k_{probe}$ since $\omega_{probe}/c$ $O(10^8)$ Hz and $2\Delta_{AOM}/c$ is $O(1)$. Now setting $v_{pump}=v_{probe}$ and using this approximation:
$\omega_{probe}-\omega_{0,i} = -\omega_{probe}-2\Delta_{AOM}+\omega_{0,j}$
such that
$\omega_{probe} = \frac{\omega_{0,i}+\omega{0,j}}{2}-\Delta_{AOM}$

