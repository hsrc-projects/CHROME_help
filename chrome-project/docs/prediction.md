# CHROME Predict

This section provides an overview of the CHROME Predict module and its functions

## Overview

CHROME Predict is a prediction model building framework for designing, building and deploying custom prediction models. It includes:

- GUI-based prediction model pipeline builder

- Allows access to pre-built prediction models with defined inputs

## Uses for CHROME Predict

CHROME Simulation can be used for:

- Predict service duration more accurately
- Enhance the patient journey experience
- Allow quick retrieval of information and estimates for reporting

## Getting Started - Basic Example

```python
import pandas as pd
import chrome
from chrome.client.config import ChromeClient, Config
from chrome.client.prediction import PredictionModel
from chrome.client.simulation import SimulationModel
import chrome.client.prediction as cp

my_config = Config(API_KEY='<API KEY>',
                  version='0.1'
                  )

conn = ChromeClient(client_name='firstclient',config=my_config)

conn.connect()

prediction_model = PredictionModel(client=conn)
# Work on prediction model here

# Creating a basic prediction pipeline

pipeline = cp.Pipeline()

# Specify training, test dataset and features

df = pd.read_csv('test_dataset.csv')
X_train, y_train, X_test, y_test = train_test_split(df,split = 0.2)
input_features = ['Procedure Code','OT Code','Age']
target_feature = 'Actual Duration'

pipeline.input_dataset(train=[X_train,y_train],test=[X_test,y_test])
pipeline.model_features(input=input_features,target=target_feature)

# Specify model type and training parameters
pipeline.model_type('XGBoost')
pipeline.fit()

# Access pre-built models

prediction_model.register_model('LOS-Admission-Modelv1')
predictions = prediction_model.predict(X_test)


```

