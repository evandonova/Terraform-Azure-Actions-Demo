# Terraform + Azure + GitHub Actions
Using a **Terraform configuration** and a **GitHub Actions workflow** to create resources and deploy app to **Azure**.
<br></br>
Created for demo for @SoftUni Svetlina exercises.

## Terraform Configuration Files
  - [main.tf](https://github.com/evandonova/Terraform-Azure-Actions-Demo/blob/main/main.tf) - main **Terraform configuration file** that defines resources to be provisioned
  - [variables.tf](https://github.com/evandonova/Terraform-Azure-Actions-Demo/blob/main/variables.tf) - Terraform **variable definitions**
  - [terraform.tfvars](https://github.com/evandonova/Terraform-Azure-Actions-Demo/blob/main/terraform.tfvars) - Terraform **variable values**

## Workflow Files
  - [tf-unit-tests.yml](https://github.com/evandonova/Terraform-Azure-Actions-Demo/blob/main/.github/workflows/tf-unit-tests.yml) - a GitHub Actions workflow to simply **initialize the working directory** and test if the **Terraform configuration** in the repo is **correctly formatted** and **valid**.
  - [tf-plan-apply.yml](https://github.com/evandonova/Terraform-Azure-Actions-Demo/blob/main/.github/workflows/tf-plan-apply.yml) - a GitHub Actions workflow that **provisions resources in Azure** and **deploys an app from a repo**.

## Requirements
To use this configuration, you should:
  - Have an **Azure subscription**
  - Create a **service principal in Azure** to authenticate in GitHub Actions:
      - You can use the following **command** to create the service principal and get the JSON output file with credentials:
      ``az ad sp create-for-rbac --name "Azure-Terraform-GitHub-Actions" --role contributor --scopes /subscriptions/{your subscription id} --sdk-auth``
      - Save the **output JSON** from the command
      - Create the following secrets in GitHub: ``AZURE_CREDENTIALS`` (the whole JSON), ``AZURE_CLIENT_ID``, ``AZURE_CLIENT_SECRET``, ``AZURE_SUBSCRIPTION_ID``, ``AZURE_TENANT_ID``
  - Create a **storage account** and **container** in **Azure** to **store the Terraform state file**. Names should match those in the **backend{} block** in the [main.tf](https://github.com/evandonova/Terraform-Azure-Actions-Demo/blob/main/main.tf) file
      - You can create an **Azure storage account** with the following command or manually through Azure Portal (the resource group should exist):
      ``az storage account create --name taskboardstorageacc --resource-group TaskBoardStorageRG --location northeurope --sku Standard_LRS --kind StorageV2``
      - You can create a **container in the storage account** with this command or manually:
      ``az storage container create -n taskboardcontainer --account-name taskboardstorageacc``

## Results
  - Successful **workflows** in **GitHub Actions**:
<br></br>
<kbd><img src="https://github.com/evandonova/Terraform-Azure-Actions-Demo/assets/69080997/33c0ca03-d1f0-47d8-aa53-f32008a09fbf" width="600"></kbd>
<br></br>
<kbd><img src="https://github.com/evandonova/Terraform-Azure-Actions-Demo/assets/69080997/abe14924-b27e-4362-8a7f-dc706872e040" width="600"></kbd>

  - **Provisioned resources** in Azure:
<br></br>
<kbd><img src="https://github.com/evandonova/Terraform-Azure-Actions-Demo/assets/69080997/e3ed8e48-3354-443e-a018-489d733d237f" width="600"></kbd>

  - Working **deployed app** in Azure:
<br></br>
<kbd><img src="https://github.com/evandonova/Terraform-Azure-Actions-Demo/assets/69080997/4406a8ba-fa98-4b5d-b1a4-4ced98f0bc39" width="600"></kbd>

