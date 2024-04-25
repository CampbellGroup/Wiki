### Saturated Absorption Spectra and Desired Error Signal
The goal is to lock our laser to a narrow frequency, generally either a cavity reflection or in this case a peak of a saturated absorption spectra. We send a low frequency O(100Hz) signal (our "sweep" frequency) to our laser to sweep the frequency so that we may trace out a spectrum. 

![[Pasted image 20231207102506.png]]
Above is an image of [[Saturated Absorption Spectroscopy]] (taken from Thorlabs). The time scale will vary depending on sweep frequency, and the signal is given by the probe beam of saturated absorption spectroscopy on a photodiode. While the horizontal axis is time in this graph (as you would see on an oscilloscope), this sweep signal is being sent to sweep the laser frequency, and so for a triangle wave sweep signal there will be a linear mapping of this time axis to frequency. With that being said, be sure to use a triangle wave on the sweep so that the time and frequency are related linearly remain directly proportional to one another for the entire sweep. In your head you can essentially replace time with frequency on the graph, just know there is some proportionality constant between them that depends on the sweep frequency. 

The goal is to lock our laser frequency to one of the Lorentzian-like Doppler-free transmission peaks. To do this we need to generate an error signal that will push us forward (backward) if we are past (before) the resonance peak, with magnitude of this push back proportional to how far off resonance we have become. See [[Rubidium Saturated Absorption Spectroscopy PDH Lock]] for a description of how this is done in our lab. The graph below models the feature we want to lock to as a Lorentzian and we wish to generate an error signal as described above, which looks like the derivative of the peak.
![[Pasted image 20231207103652.png]]
This image is a model/sketch of the spectra peak (red) that we wish to lock to and the desired corresponding error signal (blue). In this image the horizontal axis is frequency and the vertical axis is voltage. 

### Generating an Error Signal from a Resonance Feature( Theory and Math)
With a working saturated absorption system we will see a feature that looks like the red trace in the above image, and we must now generate something that looks like the blue error signal. Imagine we stop our sweep frequency and remain at one frequency $f$ such that our photodiode voltage is $V(f)$. If we know the peak voltage value $V(f_0)$ we can get an idea of how far from resonance we are, but we do not know if we are above or below resonance. What we do to fix this is use an AOM to modulate the saturated absorption pump laser at a higher frequency dither (our dither is 50 kHz). This dither on the AOM creates a modulation on the frequency $\Delta f(t)=(\delta_f) sin(\omega_dt)$ (where $\delta_f$ is the amplitude of frequency oscillation and $\omega_d$ is the dither frequency), such that our frequency is now $f(t)= f + \Delta f(t)$. The photodiode voltage is subsequently modulated, reading $V(f+\Delta f(t))$ where $\Delta f$ is small, so Taylor approximating we find $V(f+\Delta f(t)) = V(f) + \frac{dV}{df}|_f\Delta f$
such that 
$V(t) = V(f) + \frac{dV}{df}|_f(\delta_f) sin(\omega_dt)$
If we pass this photo diode signal into a mixer with the original dither signal $V_d(t) = V_0sin(\omega_dt)$, we get 
$V_{mix}(t)=V_0V(f)sin(\omega_dt)+ V_0\frac{dV}{df}|_f(\delta_f) sin^2(\omega_dt)$ 
(note the voltage of the dither $V_d(t)$ is proportional to the frequency modulation it creates but not identical). Using a trig identity we may rewrite this signal as $V_{mix}(t)=V_0V(f)sin(\omega_dt)+ V_0\frac{dV}{df}|_f(\delta_f)(1/2) + V_0\frac{dV}{df}|_f(\delta_f) cos(2\omega_dt)$. If we then low pass this signal with cutoff below $\omega_d$ the only remaining term will be 
$V_{LP}=V_0\frac{dV}{df}|_f(\delta_f)(1/2)$

Imagine now that the laser frequency we stopped at ($f$) is to the left (right) of our resonance peak, then $\frac{dV}{df}|_f$ will be positive (negative) and our low pass signal will be a positive (negative) voltage $V_{LP} = +(-)V_0\abs{\frac{dV}{df}|_f}(\delta_f)(1/2)$. This signal now provides an indication of which way we need to move our frequency, and by how much as the signal is proportional to the slope (which is steeper further off resonance).  If our sweep frequency is much slower than our dither frequency, it is fair to think of the laser at stopping at each frequency in its span momentarily, the signal from the photodiode is mixed and low passed, and it moves to the next frequency over. In this case we trace out a signal in frequency space across our resonance feature we trace out $V_{LP} = V_0\frac{dV}{df}(\delta_f)(1/2)$, which is proportional to the derivative of our resonance peak and provides the desired error signal. Again one should note here that while the oscilloscope reads in the time domain, the laser frequency is being swept in that time such that frequency changes proportional to time. In other words $V_{LP}(t) = V_0\frac{dV}{df}(\delta_f)(1/2)$ but $V_{LP}(f) \propto V_0\frac{dV}{df}(\delta_f)(1/2)$. 

Alternatively if we keep the sweep signal in for the math:
$V(f+\Delta_ssin(\omega_st))$
The dither makes the frequency $f(t)= f + \Delta_ssin(\omega_st)+\Delta_d sin(\omega_dt)$
and the photodiode voltage is subsequently modulated, reading 
$V(f + \Delta_ssin(\omega_st)+\Delta_d sin(\omega_dt))=V(f+\Delta_s(t)+\Delta_d(t))$
where $\Delta_d(t)$ is small (much smaller than $\Delta_s$, so Taylor approximating we find 
$V(t) = V(f+\Delta_ssin(\omega_st)) + \frac{dV}{df}|_{[f+\Delta_ssin(\omega_st)]}(\Delta_d) sin(\omega_dt)$
If we pass this photo diode signal into a mixer with the original dither signal $V_d(t) = V_0sin(\omega_dt)$, we get 
$V_{mix}(t)=V_0V(f+\Delta_ssin(\omega_st))sin(\omega_dt)+ V_0\frac{dV}{df}|_{[f+\Delta_ssin(\omega_st)]}(\delta_f) sin^2(\omega_dt)$ 
which we may write as
$V_{mix}(t)=V_0V(f+\Delta_ssin(\omega_st))sin(\omega_dt)+ V_0\frac{dV}{df}|_{[f+\Delta_ssin(\omega_st)]}(\Delta_d)(1/2) + V_0\frac{dV}{df}|_{[f+\Delta_ssin(\omega_st)]}(\Delta_d) cos(2\omega_dt)$
If we then low pass this signal with cutoff below $\omega_d$ the only remaining term will be 
$V_{LP}=V_0\frac{dV}{df}|_{[f+\Delta_ssin(\omega_st)]}(\Delta_d)(1/2)$


