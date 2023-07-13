# CHROME Simulate

This section provides an overview of the CHROME Simulation module and its functions

## Overview

CHROME Simulation is a flexible simulation framework for designing, building and deploying custom simulation models based on medical resource management processes. It includes:

- GUI-based simulation model builder with drag-and-drop functionalities

- Supports custom functions and methods for defining input parameters and interactions


## Uses for CHROME Simulation

CHROME Simulation can be used for:

- Estimating future medical resource requirements
- Optimal scheduling and allocation of resources
- Enhancing resource management capabilities of  management staff

## Getting Started - Basic Example

```python
import chrome
from chrome.client.config import ChromeClient, Config
from chrome.client.simulation import SimulationModel
import chrome.client.simulation as cs

my_config = Config(API_KEY='<API KEY>',
                  version='0.1'
                  )

conn = ChromeClient(client_name='firstclient',config=my_config)

conn.connect()

simulation_model = SimulationModel(client=conn)
# Work on simulation model here

# Creating Patient object
pt = cs.Patient(age=55,
                gender='M',
                primary_discipline='OTO')

# Creating multiple Patient objects with random attributes
N = 100
pt_list = [cs.Patient(random_attr=True) for n in range(len(N))]

# Creating multiple OT objects according to defined attribute lists
ot_names = ['L1','M4','OT22','OT26','M3']
ot_list = [cs.OT(ot_name=n) for n in ot_names]

# Defining interactions between objects with functions

def schedule_function(patient,ot):
    ot.Surgery_List.append(patient)
    return True
    
intr_surgery_scheduling = cs.Interaction(entities=[pt,ot],interaction_function=schedule_function)

# Defining metrics to be collected from simulation model

def get_utilization(ot_list):
    utilization = 0
    for ot in ot_list:
        utilization += ot.Utilized_Duration
    return utilization

metric_utilization = cs.Metrics(entities=[ot_list],metric_function=get_utilization)

# Add objects and interactions to simulation model

simulation_model.add_entities(pt_list)
simulation_model.add_entities(ot_list)
simulation_model.add_interactions(intr_surgery_scheduling)
simulation_model.add_metrics(metric_utilization)

# Compile and run simulation model

simulation_model.compile()
simulation_model.run()

report = simulation_model.get_report()






```