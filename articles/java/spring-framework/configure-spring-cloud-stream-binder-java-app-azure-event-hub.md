---
title: How to create a Spring Cloud Stream Binder application with Azure Event Hubs
description: Learn how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializr with Azure Event Hubs.
services: event-hubs
documentationcenter: java
ms.date: 12/19/2018
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.custom: devx-track-java
---

# How to create a Spring Cloud Stream Binder application with Azure Event Hubs

This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.

## Prerequisites

The following prerequisites are required in order to follow the steps in this article:

* An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].
* A supported Java Development Kit (JDK). For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 or later.

> [!IMPORTANT]
>
> Spring Boot version 2.0 or greater is required to complete the steps in this article.
>

## Create an Azure Event Hub using the Azure portal

The following procedure creates an Azure event hub.

### Create an Azure Event Hub Namespace

1. Browse to the Azure portal at <https://portal.azure.com/> and sign in.

1. Click **+ Create a resource**, then search for *Event Hubs**.

1. Click **Create**.

   ![Create Azure Event Hub Namespace][IMG01]

1. On the **Create Namespace** page, enter the following information:

   * Enter a unique **Name**, which will become part of the URI for your event hub namespace. For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.
   * Pricing tier.
   * Choose the **Subscription** you want to use for your namespace.
   * Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.
   * Specify the **Location** for your event hub namespace.
   * You can also specify the **Throughput units** for the namespace.

   ![Specify Azure Event Hub Namespace options][IMG02]

1. When you have specified the options listed above, click **Create** to create your namespace.

## Create an Azure Event Hub in your namespace

After your namespace is deployed, you can create an event hub in the namespace.

1. Navigate to the namespace created in the previous step.

1. Click **+ Event Hub** in top menu bar.

1. Name the event hub.

1. Click **Create**.

   ![Create Event Hub][IMG05]

### Create an Azure Storage Account for your Event Hub checkpoints

The following procedure creates a storage account for event hub checkpoints.

1. Browse to the Azure portal at <https://portal.azure.com/>.

1. Click **+Create**, then **Storage**, and then click **Storage Account**.

1. On the **Create storage account** page, enter the following information:

   * Choose the **Subscription** you want to use for your storage account.
   * Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.
   * Enter a unique **Name** for the storage account.
   * Specify the **Location** for your storage account.

   ![Specify Azure Storage Account options][IMG08]

1. When you have specified the options listed above, click **Review + create** to create your storage account.

1. Review the specifications and click **Create**.  The deployment will take several minutes.

## Create a simple Spring Boot application with the Spring Initializr

The following procedure creates a Spring boot application.

1. Browse to <https://start.spring.io/>.

1. Specify the following options:

   * Generate a **Maven** project with **Java**.
   * Specify a **Spring Boot** version that is equal to or greater than 2.0.
   * Specify the **Group** and **Artifact** names for your application.
   * Add the **Web** dependency.

      ![Basic Spring Initializr options][SI01]

   > [!NOTE]
   >
   > The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.
   >

1. When you have specified the options listed above, click **Generate Project**.

1. When prompted, download the project to a path on your local computer.

1. After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.

## Configure your Spring Boot app to use the Azure Event Hub starter

1. Locate the *pom.xml* file in the root directory of your app; for example:

   `C:\SpringBoot\eventhub\pom.xml`

   -or-

   `/users/example/home/eventhub/pom.xml`

1. Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhubs-stream-binder</artifactId>
      <version>1.2.7</version>
   </dependency>
   ```

1. Save and close the *pom.xml* file.

## Create an Azure Credential File

1. Open a command prompt.

1. Navigate to the *resources* directory of your Spring Boot app; for example:

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   -or-

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. Sign in to your Azure account:

   ```azurecli
   az login
   ```

1. List your subscriptions:

   ```azurecli
   az account list
   ```
   Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
   
1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Create your Azure Credential file:

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## Configure your Spring Boot app to use your Azure Event Hub

1. Locate the *application.properties* in the *resources* directory of your app; for example:

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   -or-

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   Where:

   |                          Field                           |                                                                                   Description                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    Specifies Azure credential file that you created earlier in this tutorial.                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      Specifies the Azure Resource Group that contains your Azure Event Hub.                                                      |
   |               `spring.cloud.azure.region`                |                                           Specifies the geographical region that you specified when you created your Azure Event Hub.                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          Specifies the unique name that you specified when you created your Azure Event Hub Namespace.                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    Specifies Azure Storage Account that you created earlier in this tutorial.                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.                            |
   |       `spring.cloud.stream.bindings.input.group `        | Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub. |
   |    `spring.cloud.stream.bindings.output.destination`     |                               Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.                               |

3. Save and close the *application.properties* file.

## Add sample code to implement basic event hub functionality

In this section, you create the necessary Java classes for sending events to your event hub.

### Modify the main application class

1. Locate the main application Java file in the package directory of your app; for example:

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   -or-

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. Open the main application Java file in a text editor, and add the following lines to the file:

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. Save and close the main application Java file.

### Create a new class for the source connector

1. Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. Save and close the *EventhubSource.java* file.

### Create a new class for the sink connector

1. Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
        LOGGER.info("New message received: '{}'", message);
        checkpointer.success()
                .doOnSuccess(s -> LOGGER.info("Message '{}' successfully checkpointed", message))
                .doOnError((msg) -> {
                    LOGGER.error(String.valueOf(msg));
                })
                .subscribe();
      }
   }
   ```

1. Save and close the *EventhubSink.java* file.

## Build and test your application

Use the following procedures to build and test your application.

1. Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:

   `cd C:\SpringBoot\eventhub`

   -or-

   `cd /users/example/home/eventhub`

1. Build your Spring Boot application with Maven and run it; for example:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Once your application is running, you can use *curl* to test your application; for example:

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   You should see "hello" posted to your application's logs. For example:

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## Next steps

To learn more about Spring and Azure, continue to the Spring on Azure documentation center.

> [!div class="nextstepaction"]
> [Spring on Azure](/azure/developer/java/spring-framework)

### Additional Resources

For more information about Azure support for Event Hub Stream Binder, see the following articles:

* [What is Azure Event Hubs?](/azure/event-hubs/event-hubs-about)

* [Create an Event Hubs namespace and an event hub using the Azure portal](/azure/event-hubs/event-hubs-create)

* [How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].

The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications. One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications. To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>. In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.

<!-- URL List -->

[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure for Java Developers]: /azure/developer/java/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
