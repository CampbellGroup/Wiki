The data vault is a server that handles saving and loading data and parameters to [[LabRAD]]. It's one of the three parts of our "[[the core LabRAD paradigm]]". Every time you save data to the data vault, it creates 2 files:
- A .csv file that stores the experimental data in multiple columns
- A .ini file that stores the experimental parameters (from [[parameter vault]])

[[QsimExperiment]] will always connect to datavault when initialized. you can access it with `self.dv`

## methods
datavault has a few methods that you'll mostly use:
- `cd(path: str, create: bool)`: cd into a given directory, optionally creating it if it doesn't exist
- `context()`: tbh i don't understand the [[context manager]]
- `new(name: str, independents: List[Tuple[str, str]], dependents: List[Tuple[str, str, str]], dtype='f', context=None)`: creates a new dataset. 
	- independents is a list of 2-element tuples: `([label, units], ...)`
	- dependents is a list of 2- or 3-element tuples: `([label, (legend), units], ...)`
- `add_parameter(parameter, value, context=None)`: Adds a parameter to the dataset that will get saved to the .ini file. 

## setup_datavault()
In most practical cases, you won't need to move beyond the `setup_datavault` method defined in [[QsimExperiment]] to make your experiment save. Here's a brief outline of what that looks like: 

```python
def run(self, cxn, context):
	self.setup_datavault('frequency', 'photons') # tells the datavault to initialize a datset with two columns: "frequency" and "photons"

	for i, freq in self.get_scan_list(self.p.test_experiment.scan, "MHz"):
	
		'''experiment loop code'''
	
		self.dv.add(returned_frequency, returned_photons)
```

So what does `setup_datavault` do under the hood? Here it is! Annotated!
```python
def setup_datavault(self, x_axis, y_axis):
	"""
	Adds parameters to datavault and parameter vault
	"""
	# cd into the directory with the same name of the experiment, creating one if it doesn't exist
	self.dv.cd(['', self.name], True) 
	# create a new dataset in the directory with the appropriate columns
	self.dataset = self.dv.new(self.name, [(x_axis, 'num')], [(y_axis, 'num')])
	# add each expeerimental paramter to the .ini file that will be made
	for parameter in self.p:
		self.dv.add_parameter(parameter, self.p[parameter])
	# return the data in case it's needed
	return self.dataset
```

If you want to do something more complicated than a simple xy scan, for instance something with multiple columns, you'll have to implement a modified version of the above logic in your experiment instead of using `setup_datavault`. For an example of this, you can look at the `setup_prob_datavault` method of the `dark_state_detection.py` experiment file. 