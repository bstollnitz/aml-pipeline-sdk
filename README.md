# How to train using an Azure ML pipeline, using the SDK

This project shows how to train a Fashion MNIST model using an Azure ML pipeline, and how to deploy it using an online managed endpoint. It demonstrates how to create Azure ML resources using the Python SDK, and it uses MLflow for tracking and model representation.


## Blog post

To learn more about the code in this repo, check out the accompanying blog post: https://bea.stollnitz.com/blog/aml-pipeline/


## Setup

* You need to have an Azure subscription. You can get a [free subscription](https://azure.microsoft.com/en-us/free?WT.mc_id=aiml-67316-bstollnitz) to try it out.
* Create a [resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal?WT.mc_id=aiml-67316-bstollnitz).
* Create a new machine learning workspace by following the "Create the workspace" section of the [documentation](https://docs.microsoft.com/en-us/azure/machine-learning/quickstart-create-resources?WT.mc_id=aiml-67316-bstollnitz). Keep in mind that you'll be creating a "machine learning workspace" Azure resource, not a "workspace" Azure resource, which is entirely different!
* If you have access to GitHub Codespaces, click on the "Code" button in this GitHub repo, select the "Codespaces" tab, and then click on "New codespace."
* Alternatively, if you plan to use your local machine:
  * Install the Azure CLI by following the instructions in the [documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?WT.mc_id=aiml-67316-bstollnitz).
  * Install the ML extension to the Azure CLI by following the "Installation" section of the [documentation](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-cli?WT.mc_id=aiml-67316-bstollnitz).
  * Install and activate the conda environment by executing the following commands:
  ```
  conda env create -f environment.yml
  conda activate aml_pipeline_sdk
  ```
* In a terminal window, log in to Azure by executing `az login --use-device-code`. 
* Add a `config.json` file to the root of your project (or somewhere in the parent folder hierarchy) containing your Azure subscription ID, resource group, and workspace:
```
{
    "subscription_id": "<YOUR_SUBSCRIPTION_ID>",
    "resource_group": "<YOUR_RESOURCE_GROUP>",
    "workspace_name": "<YOUR_WORKSPACE>"
}
```
* You can now open the [Azure Machine Learning studio](https://ml.azure.com/?WT.mc_id=aiml-67316-bstollnitz), where you'll be able to see and manage all the machine learning resources we'll be creating.
* Install the [Azure Machine Learning extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vscode-ai), and log in to it by clicking on "Azure" in the left-hand menu, and then clicking on "Sign in to Azure."


## Training and inference on your development machine

* Under "Run and Debug" on VS Code's left navigation, choose the "Train locally" run configuration and press F5.
* Do the same for the "Test locally" run configuration.

* You can analyze the metrics logged in the "mlruns" directory with the following command:

```
mlflow ui
```

* Make a local prediction using the trained mlflow model. You can use either csv or json files:

```
cd aml_pipeline_sdk
mlflow models predict --model-uri "model" --input-path "test_data/images.csv" --content-type csv
mlflow models predict --model-uri "model" --input-path "test_data/images.json" --content-type json
```


## Train and deploy in the cloud

### Create and run the pipeline

Select the run configuration "Train in the cloud" and press F5 to train in the cloud.


### Create and invoke the endpoint

Select the run configuration "Create endpoint" and press F5 to create an endpoint in the cloud and invoke it.


### Clean up the endpoint

Once you're done working with the endpoint, you can clean it up to avoid getting charged by selecting the "Delete endpoint" run configuration and pressing F5.


## Related resources

* [Component YAML schema](https://docs.microsoft.com/en-us/azure/machine-learning/reference-yaml-component-command?WT.mc_id=aiml-42161-bstollnitz)
* [Pipeline YAML schema](https://docs.microsoft.com/en-us/azure/machine-learning/reference-yaml-job-pipeline?WT.mc_id=aiml-42161-bstollnitz)
* [az ml job commands](https://docs.microsoft.com/en-us/cli/azure/ml/job?view=azure-cli-latest#az-ml-job-create?WT.mc_id=aiml-42161-bstollnitz)
* [Output formats for Azure CLI commands](https://docs.microsoft.com/en-us/cli/azure/format-output-azure-cli?WT.mc_id=aiml-42161-bstollnitz)
