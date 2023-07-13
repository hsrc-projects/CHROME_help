# CHROME Schedule

This section provides an overview of the CHROME Scheduling module and its functions

## Overview

CHROME Schedule is a flexible patient journey builder for mapping out key touchpoints in the patient journey and estimating resource requirements using pre-built and custom prediction models.

- Integration with existing prediction models for multiple outputs

- Ability to connect custom user build models

- End-to-end patient journey estimation of resource requirements

## Uses for CHROME Schedule

CHROME Schedule can be used for:

- Estimating future medical resource requirements
- Optimal scheduling and allocation of resources
- Enhance resource management capabilities of  management staff

## Getting Started - Basic Example

```python
import chrome
from chrome.client.config import ChromeClient, Config
import chrome.client.schedule as ch
import chrome.client.prediction as cp
from chrome.client.prediction import PredictionModel
from chrome.client.schedule import Scheduler

my_config = Config(API_KEY='<API KEY>',
                  version='0.1'
                  )

conn = ChromeClient(client_name='firstclient',config=my_config)

conn.connect()


scheduler = Scheduler(client=conn)
prediction_model = PredictionModel(client=conn)

# Define input data

input_data = {'Age':'55',
             'Discipline':'OTO',
             'Procedure Code': 'SB810K',
             'Gender':'M',
             'ASA Status':'II',
             'Priority':'Elective'}

# Specify journey touchpoints and associated models

pt_journey = {'Consultation': prediction_model.register_model('ConsultTimeModelv1'),
             'SurgeryListing': prediction_model.register_model('SurgeryDurationModelv1'),
             'PreopAdmissionTest': prediction_model.register_model('LOSAdmissionModelv2')}

# Set up scheduling model

scheduler.add_input(input_data)
scheduler.add_journey(pt_journey)

# Run scheduler and retrieve report

scheduler.compile()
scheduler.predict()
report = scheduler.report()


```

