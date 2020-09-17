---
title: The Azure development flow
description: An overview of the cloud development cycle on Azure, which involves provisioning, coding, testing, deployment, and management.
ms.date: 06/04/2020
ms.topic: conceptual
ms.custom: devx-track-python
---

# The Azure development flow: provision, code, test, deploy, and manage

[Previous article: provisioning, accessing, and managing resources](cloud-development-provisioning.md)

Now that you understand Azure's model of services and resources, you can understand the overall flow of developing cloud applications with Azure: **provision**, **code**, **test**, **deploy**, and **manage**.

| Step | Primary tools | Activities |
| --- | --- | --- |
| Provision | Azure CLI, Azure Portal, Cloud Shell, Python scripts using Azure management libraries | Provision resource groups; provision specific resources in those groups; configure resources to be ready for use from app code and/or ready to receive Python code in deployments. |
| Code | Code editor (such as Visual Studio Code), Azure libraries, reference documentation | Write Python code using the Azure client libraries to interact with provisioned resources. |
| Test | Python runtime, debugger | Run Python code locally against active cloud resources (typically dev or test resources rather than production resources). The code itself is not yet hosted on Azure, which helps you debug and iterate quickly. |
| Deploy | Azure CLI, GitHub, DevOps | Once code has been tested locally, deploy it to an appropriate Azure hosting service where the code itself can run in the cloud. Deployed code typically runs against staging or production resources. |
| Manage | Azure CLI, Azure Portal, Python scripts, Azure Monitor | Monitor app performance and responsiveness, make adjustments in production environment, migrate improvements back to dev environment for the next round of provisioning and development. |

## Step 1: Provision and configure resources

As described in the [previous article of this series](cloud-development-provisioning.md), the first step in developing any application is to provision and configure the resources that make up the target environment for your application.

Provisioning begins by creating a resource group in a suitable Azure region. You can create a resource group through the Azure portal, through the Azure CLI, or with a custom script that uses the Azure libraries (or REST API).

Within that resource group, you then provision and configure the individual resources you need, again using the portal, the CLI, or the Azure libraries. Configuration includes setting access policies that control what identities (service principals and/or application IDs) are able to access those resources.

For most application scenarios, you'll likely create provisioning scripts with the Azure CLI and/or Python code using the Azure libraries. Such scripts describe the totality of your application's resource needs. A script enables you to easily recreate the same set of resources within different development, test, staging, and production environments, rather than manually performing many repeated steps in the Azure portal. Such scripts also make it easy to provision an environment in a different region, or to use different resource groups. You can also maintain these scripts in source control repositories so that you have full auditing and change history.

## Step 2: Write your app code to use resources

Once you've provisioned the resources you need for your application, you write the application code to work with those resources (excepting the resources to which you deploy the code itself).

For example, in the provisioning step you might have created an Azure storage account, created a blob container within that account, and set access policies for the application on that container. From your code, now, you can authenticate with that storage account and then create, update, or delete blobs within that container. (This process is demonstrated in [Example - Use Azure Storage](azure-sdk-example-storage.md)) Similarly, you might have provisioned a database with a schema and appropriate permissions, so that your application code can connect to the database and perform the usual create-read-update-delete operations.

App code typically uses environment variables to identify the names and URLs of the resources to use. Environment variables allow you to easily switch between cloud environments (dev, test, staging, and production) without any changes to the code.

As a Python developer, you'll likely write your application code in Python using the Azure libraries for Python. That said, any independent part of a cloud application can be written in any supported language. If you're working in a team with a variety of language expertise, for instance, it's entirely possible that some parts of the application are written in Python, some in JavaScript, some in Java, and others in C#.

Note that application code can use the Azure libraries to perform provisioning and management operations as needed. Provisioning scripts, similarly, can use the libraries to initialize resources with specific data, or perform housekeeping tasks on cloud resources even when those scripts are run locally.

## Step 3: Test and debug your app code locally

Developers typically like to test app code on their local workstations before deploying that code to the cloud Testing app code locally means that you're typically accessing other resources that you've already provisioned in the cloud, such as storage, databases, and so forth. The difference is that you're not yet running the app code itself within a cloud service.

By running the code locally, you can also take full advantage of debugging features offered by tools such as Visual Studio Code and manage your code in a source control repository.

You don't need to modify your code at all for local testing: Azure fully supports local development and debugging using the same code you deploy to the cloud. Environment variables are again the key: on the cloud, your code can access the hosting resource's settings as environment variables. By creating those same environment variables locally, the same code runs without modification. This pattern works for authentication credentials, resource URLs, connection strings, and any number of other settings, making it easy to use resources in a development environment when running code locally and production resources once the code is deployed to the cloud.

## Step 4: Deploy your app code to Azure

Once you've tested your code locally, you're ready to deploy the code to the Azure resource that you've provisioned to host it. For example, if you're writing a Django web application, you either deploy that code to a virtual machine (where you provide your own web server) or to Azure App Service (which provides the web server for you). Once deployed, that code is running on the server rather than on your local machine, and can access all the Azure resources for which it's authorized.

As noted in the previous section, in typical development processes you first deploy your code to the resources you've provisioned in a development environment. After a round of testing, you deploy your code to resources in a staging environment, making the application available to your test team and perhaps preview customers. Once you're satisfied with the application's performance, you can deploy the code to your production environment. All of these deployments can also be automated through continuous integration and continuous deployment using Azure DevOps.

However you do it, once the code is deployed to the cloud, it truly becomes a cloud application, running entirely on the server computers in Azure's data centers.

## Step 5: Manage, monitor, and revise

After deployment, you want to make sure the application is performing as it should, responding to customer requests and using resources efficiently (and at the lowest cost). You can manage how Azure automatically scales your deployment as needed, and you can collect and monitor performance data through the Azure portal, the Azure CLI, or custom scripts written with the Azure libraries. You can then make real-time adjustments to your provisioned resources to optimize performance, again using any of the same tools.

Monitoring gives you insight about how you might restructure your cloud application. For example, you may find that certain portions of a web app (such as a group of API endpoints) are used only occasionally in comparison to the primary parts. You could then choose to deploy those APIs separately as serverless Azure Functions, where they have their own backing compute resources that don't compete with the main application but cost only pennies per month. Your main application then becomes more responsive to more customers without having to scale up to a higher-cost tier.

## Next steps

You're now familiar with the basic structure of Azure and the overall development flow: provision resources, write and test code, deploy the code to Azure, and then monitor and manage those resources.

The next step is to get familiar with the Azure libraries for Python, which you'll be using in many parts of the flow.

> [!div class="nextstepaction"]
> [Learn to use the Azure libraries for Python >>>](azure-sdk-overview.md)
