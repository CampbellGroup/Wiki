
## PDH Lock Set Up 
- Rigol function generator creates 1Vpp saw tooth wave 250 Hz sweep signal
- Sweep signal is split and sent to laser and oscilloscope (for triggering)
- Another channel of the same Rigol function generator creates a 4 Vpp 50 kHz sine wave dither
- The dither signal is split and one sent to RF input of a Bias-Tee (Mini-Circuits MN:ZFBT-4R2G+)
- 11.6 V from a DC power supply goes to the DC of the Bias-Tee 
- Bias-Tee output is sent to VCO (Mini-Circuits MN: ZX95-200-S+) with another 12 V DC for power on the VCC port
- VCO signal is amplified (Mini-Circuits MN: ZHL-1-2W+) and attenuated to be below 31.76 dBM AOM power rating
- AOM (Gooch and Housego MN: 46200-.4-.78-LTD) double passes SadAbs pump and applies dither frequency
- SadAbs probe photodiode signal sent to the RF channel of the mixer (Mini-Circuits MN: ZAD-8+)
- The other dither signal is sent to the local oscillator channel of the mixer
- Mixer output is sent to SRS low pass filter and amplifier (MN: SR560) to output the error signal
## Problems Encountered and Not Obvious Considerations to be Made
### Dither Frequency Higher than Modulation Bandwidth
You should be able to see sinusoidal like wiggles on your saturated absorption photo-diode signal from your dither frequency. For a long time we did not see this and as a consequence did not see an error signal as the photo-diode signal was not being modulated. When lowering our dither from 500 kHz to 50 kHz, we noticed the dither appear in our photo-diode signal (cut off around 100 kHz). We believe that while the AOM has a driving bandwidth fo 150 to 200 MHz, it has a smaller frequency modulation bandwidth that cuts off around 100 kHz. We think the AOM modulation limit to be the problem as the 500 kHz dither is present in the signal going into the AOM, but not on the photo-diode. The photo-diode also has a bandwidth greater than our 500 kHz dither frequency. In any case, the take away is to run your dither much higher than your sweep with the caveat that some electronics may be frequency modulation bandwidth limited.
### AOM Shift of Doppler Free Line Centers and General Expected Results
As calculations in [[Saturated Absorption Spectroscopy]] show, the Doppler free atomic line centers will be one single pass AOM shift behind where the true value is, and the Doppler broadened signals will not appear shifted. When generating a theory graph of expected SadAbs results, one must account for this shift. Additionally we only see transitions associated with the highest transition strength (In Rb 87 this is F=2 to F=3), and so we see good agreement between our theory and data when we lower the effective strengths of the transitions we do not see. 
### Dither Frequency Must be an Integer Multiple of the Sweep Frequency
The dither frequency should sample the same part of the spectrum with each sweep, such that the frequency of the dither must be such that it has the same phase at the start of each sweep. To do this the dither frequency must be an integer multiple of the sweep frequency. If the dither is far from an integer multiple of the sweep frequency the error signal will oscillate rapidly. If very close to an integer multiple but off by less than a hertz (this happened when we used two different function generators with different references) the error signal will appear to have a phase slipping issue at around a Hertz or so.
### Too Many AOM Orders in Saturated Absorption
By the time the double passed pump beam light got to the Rubidium sample the beams had diverged to the point where they overlapped, and multiple AOM modes interacted with the probe beam. This means we saw our saturated absorption features once for every AOM mode, shifted up by a frequency equal to the AOM frequency. For example with Rubidium 87 we should see three peaks, but instead we saw 6 as we had 2 orders of the AOM interacting with the probe. We fixed the problem by forking down a beam block to select the correct order. 

