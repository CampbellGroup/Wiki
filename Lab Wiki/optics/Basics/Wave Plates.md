# Theory
Waveplates change the polarization of a beam. There are two main types: half and quarter waveplates. Half waveplates take linear polarization to linear polarization while quarter waveplates change the polarization ellipticity, taking linear polarization to circular polarization and vice-versa. They are made of a birefringent material such that the wavenumber $k$ is different along the orthogonal ``fast'' and ``slow'' axes of the waveplate. This difference introduces a phase difference that changes the polarization of the light. Before the waveplate we may write the propagating light as

$\vec{E} = Ee^{i(kz-wt)}\hat{p} = Ee^{i(kz-wt)}e^{i\Phi}[cos(\theta)\hat{f} + e^{i\phi}sin(\theta)\hat{s}]$

where we have projected the polarization vector $\hat{p}$ onto the fast and slow axes $\hat{f}$ and $\hat{s}$. For the sake of generality we have chosen $\hat{p}=e^{i\Phi}[cos(\theta)\hat{f} + e^{i\phi}sin(\theta)\hat{s}]$ such that we do not assume the incident light to be polarized linearly or circularly. Now after the light propagates through the waveplate of thickness $L$

$\vec{E}_{waveplate} = Ee^{i[k(z-L)-wt]}e^{i\Phi}[e^{ik_fL}cos(\theta)\hat{f} + e^{i\phi+ik_sL}sin(\theta)\hat{s}]$

and if we let $\Delta k = k_s-k_f$ and $\Phi_L = \Phi+k_fL-kL$ we have

$\vec{E}_{waveplate} = Ee^{i[kz-wt]}e^{i\Phi_L}[cos(\theta)\hat{f} + e^{i[\phi+(\Delta k)L]}sin(\theta)\hat{s}]$

A half waveplate has length $L$ such that $\Delta kL = \pi$, and so

$\vec{E}_{HWP} = Ee^{i[kz-wt]}e^{i\Phi_L}[cos(\theta)\hat{f} + e^{i\phi}sin(\theta)\hat{s}]= Ee^{i[kz-wt]}e^{i\Phi_L}[cos(\theta)\hat{f} + e^{i(\phi+\pi)}sin(\theta)\hat{s}]$

While a quarter waveplate has length $L$ such that $\Delta kL = \pi/2$, and so

$\vec{E}_{QWP} = Ee^{i[kz-wt]}e^{i\Phi_L}[cos(\theta)\hat{f} +i e^{i\phi}sin(\theta)\hat{s}] = Ee^{i[kz-wt]}e^{i\Phi_L}[cos(\theta)\hat{f} +e^{i(\phi+\pi/2)}sin(\theta)\hat{s}]$

Comparing the light after the waveplate ($\vec{E}_{HWP}$ and $\vec{E}_{QWP}$) with our incident light ($\vec{E}$), we see how these waveplates change the polarization of the light. Half waveplates take linear polarization to linear polarization while quarter waveplates change the polarization ellipticity, taking linear polarization to circular polarization and vice-versa. Examples are given in the table below where $\theta$ is chosen to be $\pi/4$.

For $\theta = \pi/4$

|$\phi$ | $e^{i\phi}$ | Polarization Before | Polarization After HWP | Polarization After QWP|
|:-:|:--:|:------------------:|:----------------------:|:------------------:|
|0 | 1 | Linear | Linear, flipped about $\hat{f}$ | RHC|
|$\pi/2$ | $i$ | RHC | LHC | Linear|
|$\pi$ | -1 | Linear | Linear, flipped about $\hat{f}$ | LHC|
|$3\pi/2$ | $-i$ | LHC | RHC | Linear|

As partially explained in the above table, half wave plates flip linear polarization about the fast axis $\hat{f}$. Therefore with input linear polarization we may get any desired output linear polarizaiton by rotating the waveplate orientation (thereby rotating the orientation of the fast axis $\hat{f}$ over which the input polarization will be flipped). By rotating the waveplate we change $\theta$ in equations for $\vec{E}_{HWP}$ and $\vec{E}_{QWP}$, and this allows us to achieve any orientation or ellipticity of polarization using half or quarter waveplates.

# Mounting Wave Plates
The waveplates are placed in the circular mounts with 360 degrees of rotation. Adjusting this degree of rotation will send different amounts of power through the ends of a [[Polarizing Beam Splitter]]. They are held in place with a ring which can be screwed in with a spanner wrench. 