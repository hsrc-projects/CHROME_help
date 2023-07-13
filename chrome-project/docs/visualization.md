# CHROME Visualize

This section provides an overview of the CHROME Visualization module and its functions

## Overview

CHROME Visualization is a flexible visualization framework for displaying results from CHROME modules in an interactive manner. It includes:

- GUI-based dashboard builder for plotting model results

- Supports custom functions and methods for defining input parameters and interactions


## Uses for CHROME Visualize

CHROME Visualize can be used for:

- Estimating future medical resource requirements
- Optimal scheduling and allocation of resources
- Enhancing resource management capabilities of  management staff

## Getting Started - Basic Example

```python
import chrome
from chrome.client.config import ChromeClient, Config
import chrome.client.schedule as ch
import chrome.client.prediction as cp
from chrome.client.prediction import PredictionModel
from chrome.client.simulation import SimulationModel
from chrome.client.visualization import Visualizer
import chrome.client.visualization as cv

my_config = Config(API_KEY='<API KEY>',
                  version='0.1')

conn = ChromeClient(client_name='firstclient',config=my_config)

conn.connect()

visualizer = Visualizer(client=conn)
scheduler = Scheduler(client=conn)
prediction_model = PredictionModel(client=conn)

# Load previous prediction and simulation model results
duration_model_results = prediction_model.load_results('SurgeryDuration-190120-2030')
simulation_results = simulation_model.load_results('OTSimulation-190120-2030')

# Generate plots from results
duration_errors = cv.Histogram(x=duration_model_results['Error'].bins,
                               y=duration_model_results['Error'])
utilization_rate = cv.Plot(x=simulation_results['Date'],
                           x=simulation_results['Utilization'])

visualizer.add_plot(duration_errors)
visualizer.add_plot(utilization_rate)
visualzier.update()
```

