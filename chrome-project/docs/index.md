# CHROME Overview

This section provides an overview of the Centralized Healthcare Resource Optimization Management (CHROME) Platform.

## About CHROME

CHROME is a flexible and holistic platform for managing medical resources to make life better for healthcare professionals. It includes:

- Integrated micro-service ecosystem for easy deployment and use

- Ubiquitous tools that can be accessed anytime, anywhere

- Support strategic and tactical decision-making for scheduling medical resources

## Uses for CHROME

CHROME can be used for:

- Estimating future medical resource requirements
- Optimal scheduling and allocation of resources
- Enhance resource management capabilities of  management staff
- Predict service duration more accurately
- Enhance the patient journey experience
- Allow quick retrieval of information and estimates for reporting
- Enable cross-institutional collaboration and research
- Flexible framework for quick deployment and integration

## Commands

* `chrome start ` - Starts the CHROME server
* `chrome list-sessions` - List all active sessions
* `chrome status` - Print CHROME server status
* `chrome -h` - Print help message and exit.

## Getting Started

```python
import chrome
from chrome.client.config import ChromeClient, Config
from chrome.client.prediction import PredictionModel
from chrome.client.simulation import SimulationModel

my_config = Config(API_KEY='<API KEY>',
                  version='0.1'
                  )

conn = ChromeClient(client_name='firstclient',config=my_config)

conn.connect()

simulation_model = SimulationModel(client=conn)
# Work on simulation model here

prediction_model = PredictionModel(client=conn)
# Work on prediction model here


```
