Here's the skinny on how [[LabRAD]], and specifically the [[data vault]] manages contexts. 

## What is a context?
A context is essentially a session that can be opened by a program. In the context (no pun intended) of the data vault, it solves a pretty simple problem. Say I have two routines: A and B, each of which wants to access a different directory in the datavault. These routines can even be in the same program. If process A uses the `context=context_A`  parameter, and process B uses the `context=context_B` flag, then each context can be `cd`'ed into a different directory, and can have different files open without conflict. Here's an example from the `dark_state_detection` experiment: 
```python
class DarkStateDetection(QsimExperiment):
	def initialize(self, cxn, context, ident):  
	    self.ident = ident  
	    self.pulser = self.cxn.pulser  
	    self.rsg = self.cxn.grapher  
	    self.pzt_server = cxn.piezo_server  
	    self.prob_ctx = self.dv.context()  
	    self.hist_ctx = self.dv.context()  
	    self.mean_doppler_counts = 0.0  
	    self.cavity_chan = 1  
	    self.cavity_voltage = 0.0  
	    self.hist_mean = 0.0  
	    self.hist_std_dev = 0.0
	
	...
	
	def setup_prob_datavault(self):  
	    self.dv.cd(['', 'Dark_State_Probability'], True, context=self.prob_ctx)  
	    self.dataset_prob = self.dv.new('fidelity_dark_state_prep',  
	                                    [('run', 'arb u')],  
	                                    [('Counts', 'Counts', 'num')],  
	                                    context=self.prob_ctx)  
	  
	    self.rsg.plot(self.dataset_prob, 'Fidelity', False)  
	    for parameter in self.p:  
	        self.dv.add_parameter(parameter, self.p[parameter], context=self.prob_ctx)  
	  
	    self.dark_state_counts = self.dv.context()  
	    self.dv.cd(['', 'Dark_State_Counts'], True, context=self.dark_state_counts)  
	    self.dark_state_counts_dataset = self.dv.new('dark_state_counts', [('run', 'arb')],  
	                                                 [('counts', 'detection_counts', 'num'),  
	                                                  ('counts', 'doppler_counts', 'num')],  
	                                                 context=self.dark_state_counts)  
	    for parameter in self.p:  
	        self.dv.add_parameter(parameter, self.p[parameter],  
	                              context=self.dark_state_counts)
	
	...
```
In the `initialize` method in the above snippet, the experiment opens two different contexts in the datavault. Then in the `setup_prob_datavault` method, it `cd`'s into two different filenames and initializes a dataset for each. Any actions that touch the datavault can now select either of the two contexts, without having to `cd` into the relevant file every time. 