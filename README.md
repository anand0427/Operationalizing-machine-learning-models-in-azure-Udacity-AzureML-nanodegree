# Operationalizing Machine Learning Project Udacity NanoDegree

## Table of contents
   * [Project Overview](#Project-Overview)
   * [Project requirements](#Project-requirements)
   * [Architecture and Procedure](#Architecture-and-Procedure)
   * [Deployment and Results](#Deployment-and-Results)
   * [Screen Recording](#Screen-Recording)
   * [Standout Suggestions](#Standout-Suggestions)

## Project Overview

The problem is to create a pipeline with AutoML experiement and deploy one of the models to create an endpoint and consume that endpoint with POST request. 

***
## Project requirements
* An Azure ML workspace
* A compute instance
* Jupyter lab.

***
## Architecture and Procedure

![Diagram](screenshots/architecture.PNG?raw=true "Results of automl")

To train an automl model a few steps need to be executed to setup the experiement. 

1. We setup the workspace.
2. Create an experiment
3. Setup the compute
4. Import the dataset into the workspace and register to datasets using Dataset package
5. Create automl settings with parameters to timeout, concurrent iterations and metric to use
6. Create automl config to use compute, data, target and early stopping
7. Submit the experiment and wait for completion. 

* The experiment will create a few child runs and show completed when the best model is found or when there is no further improvement. The experiment is then marked completed which moves us on to the next step that is deployment. 
![Diagram](./screenshots/3.PNG?raw=true "Running experiment")
* Best Models with Voting Ensemble achieving an accuracy of 0.9168
![Diagram](./screenshots/4.PNG?raw=true "Best Models")
![Diagram](./screenshots/5.PNG?raw=true "Best Models")

* We choose the best model for deployment and enable "Authentication" while deploying the model using Azure Container Instance (ACI). The executed code in logs.py enables Application Insights. "Application Insights enabled" is disabled before executing logs.py.
![Diagram](./screenshots/6.PNG?raw=true "Logs") 
![Diagram](./screenshots/7.PNG?raw=true "Logs")
![Diagram](./screenshots/8.PNG?raw=true "Best Models")

We also create a pipeline to train the model and publish the pipeline and consume the pipeline as an endpoint. 

![Diagram](./screenshots/9.PNG?raw=true "Endpoint")

## Deployment and Results

After creating the AutoML model and Pipeline, we get the best model and have to deploy the pipeline using Azure SDK. 

![Diagram](./screenshots/9.PNG?raw=true "Endpoint")

* When the pipeline is deployed and it goes from a transition phase to a healthy phase the pipeline that is live is marked as active. We can use this endpoint now to make API requests and get our results with the model.

![Diagram](./screenshots/23.PNG?raw=true "pipeline]")
![Diagram](./screenshots/22.PNG?raw=true "pipeline")

We also setup Swagger documentation to understand exactly what the API needs to have a fool proof way of sending requests and removing the guess work. 

![Diagram](./screenshots/9.PNG?raw=true "Swagger")
![Diagram](./screenshots/11.PNG?raw=true "Swagger")
![Diagram](./screenshots/12.PNG?raw=true "Swagger")

we send requests to endpoint as a json object using Python requests library. We also use his endpoint script to benchmark our rest API to get accurate idea of how well the API is performing under many requests per second. 

Input:

```
{
  "data":
    [
        {
            "age": 17,
            "job": "blue-collar",
            "marital": "married",
            "education": "university.degree",
            "default": "no",
            "housing": "yes",
            "loan": "yes",
            "contact": "cellular",
            "month": "may",
            "day_of_week": "mon",
            "duration": 971,
            "campaign": 1,
            "pdays": 999,
            "previous": 1,
            "poutcome": "failure",
            "emp.var.rate": -1.8,
            "cons.price.idx": 92.893,
            "cons.conf.idx": -46.2,
            "euribor3m": 1.299,
            "nr.employed": 5099.1,
        }
    ]
}
```

![Diagram](./screenshots/13.PNG?raw=true "Endpoint")

* We run the benchmark shell file to send multiple requests to the endpoint and log various details. 

![Diagram](./screenshots/14.PNG?raw=true "bench mark")
![Diagram](./screenshots/15.PNG?raw=true "bench mark")
![Diagram](./screenshots/16.PNG?raw=true "bench mark")
![Diagram](./screenshots/17.PNG?raw=true "bench mark")

## Screen Recording

Look at the screenshots folder for more images. This screen recording gives a short overview of the project in action.

https://youtu.be/LhCW3kwu8-A

## Standout Suggestions

1. Creating newer features with existing features. 
2. Training hyperdrive experiment for more parameters.
3. Automl model can run for longer to get better models and more options with higher accuracy. 
4. Having better computing power for decreasing latency. 