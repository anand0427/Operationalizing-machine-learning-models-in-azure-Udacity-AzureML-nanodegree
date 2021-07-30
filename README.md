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

* Experiment Completed
![Diagram](./screenshots/3.PNG?raw=true "Running experiment")
* Best Models with Voting Ensemble achieving an accuracy of 0.9168
![Diagram](./screenshots/4.PNG?raw=true "Best Models")
![Diagram](./screenshots/5.PNG?raw=true "Best Models")

* Running logs script to enable Application insights
![Diagram](./screenshots/6.PNG?raw=true "Logs") 
![Diagram](./screenshots/7.PNG?raw=true "Logs")
![Diagram](./screenshots/8.PNG?raw=true "Best Models")

We also create a pipeline to train the model and publish the pipeline and consume the pipeline as an endpoint. 

![Diagram](./screenshots/9.PNG?raw=true "Endpoint")

## Deployment and Results

After creating the AutoML model and Pipeline, we get the best model and have to deploy the pipeline using Azure SDK. 

![Diagram](./screenshots/9.PNG?raw=true "Endpoint")

* Pipeline being shown active

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

* Benchmarking the API 

![Diagram](./screenshots/14.PNG?raw=true "bench mark")
![Diagram](./screenshots/15.PNG?raw=true "bench mark")
![Diagram](./screenshots/16.PNG?raw=true "bench mark")
![Diagram](./screenshots/17.PNG?raw=true "bench mark")

## Screen Recording

Look at the screenshots folder for more images. This screen recording gives a short overview of the project in action.

https://www.youtube.com/watch?v=TTyaFGE1Jq8

## Standout Suggestions

1. Creating newer features with existing features. 
2. Training hyperdrive experiment for more parameters.
3. Automl model can run for longer to get better models and more options with higher accuracy. 
4. Having better computing power for decreasing latency. 