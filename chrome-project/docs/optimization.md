# CHROME Optimize

This section provides an overview of the CHROME optimization module and its functions

## Overview

CHROME Optimize is a generic optimization framework for solving optimization models involving healthcare resources, such as operating theatres, beds and medical equipment. It includes:

- High level APIs for easily defining optimization models based in the healthcare context

- Integration with external frameworks such as RSOME, pyatom

- Support for strategic and tactical decision-making for scheduling medical resources

## Uses for CHROME Optimize

CHROME Optimize can be used for:

- Estimating future medical resource requirements
- Optimal scheduling and allocation of resources
- Enhance resource management capabilities of  management staff

## Getting Started - Basic Example

```
import chrome
from chrome.client.config import ChromeClient, Config
from chrome.client.optimization import OptimizationModel
import chrome.client.optimization as co 

my_config = Config(API_KEY='<API KEY>',
                   version='0.1')

conn = ChromeClient(client_name='firstclient',config=my_config)

conn.connect()

optimization_model = OptimizationModel(client=conn)

# Define model variables and parameters

X = co.DecisionVariable()
A = co.Parameter()
B = co.Parameter()
C = co.CostParameter()

# Define constraint and objective formulas

constraint_1 = co.Constraint(A*X > B)
objective_1 = co.Objective(C*X)

# Set up optimization model

optimization_model.add_variable(X)
optimization_model.add_constraint(constraint_1)
optimization_model.add_objective(objective_1)

# Compile and solve model

optimization_model.compile()
optimization_model.solve()
report = optimization_model.report()
```

