--NormalPMTFlow is the [[LabRAD]] server that handles [[the PMT]] counts coming into the [[pulser]]. The main command it implements is `get_next_counts()`, which returns the next n measurements from the PMT. 

It generally shouldn't be used in experiments, where pulser's `readoutCount` TTL should be used instead.
