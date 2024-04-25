The PMT is a Hamamatsu \[insert model number here]. It's mounted to a lens tube suspended above the trap chamber, on  a three-axis translation stage. It is connected to a reserved TTL input on the [[pulser]], which accumulates the PMT counts. 

PMT counts can be requested from the pulser via the [[NormalPMTFlow]] server using the `get_next_counts()` function. 

We also have a PMT on the bottom beampath, and we used to be able to combine both PMT signals on an SRS DG535 box. This feature currently isn't in use. 