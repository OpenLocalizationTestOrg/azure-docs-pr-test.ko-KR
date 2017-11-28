---
title: "Java를 사용하여 장치에서 Azure IoT Hub로 파일 업로드 | Microsoft Docs"
description: "Java용 Azure IoT 장치 SDK를 사용하여 장치에서 클라우드로 파일을 업로드하는 방법입니다. 업로드된 파일은 Azure Storage blob 컨테이너에 저장됩니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: c917a3b3e16f1e84f202d6c87a04faf642266701
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="52370-104">IoT Hub를 사용하여 장치에서 클라우드로 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="52370-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="52370-105">이 자습서에서는 [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-java-java-c2d.md) 자습서의 코드를 기반으로 작성되었으며 [IoT Hub의 파일 업로드 기능](iot-hub-devguide-file-upload.md)을 사용하여 [Azure Blob Storage](../storage/index.md)에 파일을 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52370-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="52370-106">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="52370-107">파일을 업로드하기 위한 Azure blob URI를 장치에 안전하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="52370-108">IoT Hub 파일 업로드 알림을 사용하여 앱 백 엔드에서 파일 처리를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="52370-109">[IoT Hub 시작](iot-hub-java-java-getstarted.md) 및 [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-java-java-c2d.md) 자습서는 IoT Hub의 기본적인 장치-클라우드 및 클라우드-장치 메시징 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52370-109">The [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="52370-110">[장치-클라우드 메시지 프로세스](iot-hub-java-java-process-d2c.md) 자습서에서는 장치-클라우드 메시지를 Azure Blob 저장소에 안정적으로 저장하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-110">The [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="52370-111">그러나 일부 시나리오에서는 장치에서 전송하는 데이터를 IoT Hub에서 허용하는 비교적 작은 장치-클라우드 메시지에 쉽게 매핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="52370-112">예:</span><span class="sxs-lookup"><span data-stu-id="52370-112">For example:</span></span>

* <span data-ttu-id="52370-113">이미지가 포함된 대형 파일</span><span class="sxs-lookup"><span data-stu-id="52370-113">Large files that contain images</span></span>
* <span data-ttu-id="52370-114">비디오</span><span class="sxs-lookup"><span data-stu-id="52370-114">Videos</span></span>
* <span data-ttu-id="52370-115">자주 샘플링되는 진동 데이터</span><span class="sxs-lookup"><span data-stu-id="52370-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="52370-116">특정 형태의 전처리된 데이터</span><span class="sxs-lookup"><span data-stu-id="52370-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="52370-117">이러한 파일은 일반적으로 [Azure Data Factory](../data-factory/index.md) 또는 [Hadoop](../hdinsight/index.md) 스택과 같은 도구를 사용하여 클라우드에서 배치 방식으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="52370-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="52370-118">장치에서 파일을 업로드해야 할 때 IoT Hub의 보안 및 안정성을 여전히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="52370-119">이 자습서의 끝 부분에서는 다음 두 개의 Java 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-119">At the end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="52370-120">**simulated-device** - [IoT Hub를 사용하여 클라우드-장치 메시지 보내기] 자습서에서 만든 앱의 수정된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="52370-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="52370-121">이 앱은 IoT Hub에서 제공하는 SAS URI를 사용하여 저장소에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="52370-122">**read-file-upload-notification** - IoT Hub에서 파일 업로드 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="52370-123">IoT Hub는 Azure IoT 장치 SDK를 통해 많은 장치 플랫폼 및 언어(C, .NET 및 Javascript 포함)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="52370-124">Azure IoT Hub에 장치를 연결하는 방법에 대한 단계별 지침은 [Azure IoT 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52370-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="52370-125">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="52370-126">최신 [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="52370-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="52370-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="52370-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="52370-128">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="52370-128">An active Azure account.</span></span> <span data-ttu-id="52370-129">계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="52370-130">장치 앱에서 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="52370-130">Upload a file from a device app</span></span>

<span data-ttu-id="52370-131">이 섹션에서는 [IoT Hub를 사용하여 클라우드-장치 메시지 보내기](iot-hub-java-java-c2d.md)에서 만든 장치 앱을 수정하여 IoT Hub에서 파일을 업로드하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52370-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="52370-132">이미지 파일을 `simulated-device` 폴더에 복사하고 파일 이름을 `myimage.png`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52370-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="52370-133">텍스트 편집기를 사용하여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52370-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="52370-134">**App** 클래스에 변수 선언을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-134">Add the variable declaration to the **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="52370-135">파일 업로드 상태 콜백 메시지를 처리하려면 다음 중첩 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-135">To process file upload status callback messages, add the following nested class to the **App** class:</span></span>

    ```java
    // Define a callback method to print status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to file upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="52370-136">이미지를 IoT Hub에 업로드하려면 IoT Hub에 이미지를 업로드하도록 다음 메서드를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span></span>

    ```java
    // Use IoT Hub to upload a file asynchronously to Azure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="52370-137">다음 코드 조각에 나와 있는 것처럼, **uploadFile** 메서드를 호출하도록 **main** 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get the filename and start the upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="52370-138">다음 명령을 사용하여 **simulated-device** 앱을 작성하고 오류가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-138">Use the following command to build the **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="52370-139">파일 업로드 알림 수신</span><span class="sxs-lookup"><span data-stu-id="52370-139">Receive a file upload notification</span></span>

<span data-ttu-id="52370-140">이 섹션에서는 IoT Hub에서 파일 업로드 알림 메시지를 수신하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52370-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="52370-141">IoT Hub가 이 섹션을 완료하려면 **iothubowner** 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span></span> <span data-ttu-id="52370-142">이 연결 문자열은 [Azure Portal](https://portal.azure.com/)에서 찾거나 **공유 액세스 정책** 블레이드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="52370-143">명령 프롬프트에서 다음 명령을 사용하여 **read-file-upload-notification**이라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52370-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span></span> <span data-ttu-id="52370-144">이 명령은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="52370-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="52370-145">명령 프롬프트에서 새 `read-file-upload-notification` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="52370-146">텍스트 편집기를 사용하여 `read-file-upload-notification` 폴더에서 `pom.xml` 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="52370-147">의존성을 추가하면 IoT Hub 서비스와 통신하기 위해 응용 프로그램에서 **iothub-java-service-client** 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="52370-148">[Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)을 사용하여 **iot-service-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="52370-149">`pom.xml` 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="52370-150">텍스트 편집기를 사용하여 `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52370-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="52370-151">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="52370-152">다음 클래스 수준 변수를 **앱** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-152">Add the following class-level variables to the **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="52370-153">콘솔에 파일을 업로드하는 정보를 인쇄하려면 다음 중첩 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Create a thread to receive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="52370-154">파일 업로드 알림을 수신하는 스레드를 시작하려면 다음 코드를 **main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from the ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start the thread to receive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER to exit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="52370-155">`read-file-upload-notification\src\main\java\com\mycompany\app\App.java` 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="52370-156">다음 명령을 사용하여 **read-file-upload-notification** 앱을 작성하고 오류가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="52370-157">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="52370-157">Run the applications</span></span>

<span data-ttu-id="52370-158">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-158">Now you are ready to run the applications.</span></span>

<span data-ttu-id="52370-159">`read-file-upload-notification` 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="52370-160">`simulated-device` 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52370-160">At a command prompt in the `simulated-device` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="52370-161">다음 스크린샷은 **simulated-device** 앱의 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52370-161">The following screenshot shows the output from the **simulated-device** app:</span></span>

![simulated-device 앱의 출력](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="52370-163">다음 스크린샷은 **read-file-upload-notification** 앱의 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52370-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span></span>

![read-file-upload-notification 앱의 출력](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="52370-165">포털을 사용하면 구성한 저장소 컨테이너에 업로드된 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-165">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![업로드된 파일](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="52370-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52370-167">Next steps</span></span>

<span data-ttu-id="52370-168">이 자습서에서는 장치에서 파일 업로드를 단순화하기 위해 IoT Hub의 파일 업로드 기능을 사용하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="52370-169">다음 문서를 사용하여 IoT Hub 기능 및 시나리오를 계속 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52370-169">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="52370-170">[프로그래밍 방식으로 IoT Hub 만들기][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="52370-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="52370-171">[C SDK 소개][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="52370-171">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="52370-172">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="52370-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="52370-173">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52370-173">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="52370-174">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="52370-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


