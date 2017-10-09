---
title: "장치 tooAzure Java와 함께 IoT 허브에서에서 aaaUpload 파일 | Microsoft Docs"
description: "어떻게 tooupload Java 용 Azure IoT 장치 SDK를 사용 하 여 장치 toohello 클라우드에서 파일입니다. 업로드된 파일은 Azure Storage blob 컨테이너에 저장됩니다."
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
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="71541-104">IoT Hub와 장치 toohello 클라우드에서 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="71541-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="71541-105">Hello에 hello 코드에 기반 하는이 자습서 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-java-java-c2d.md) 자습서 tooshow 있습니다 어떻게 toouse hello [IoT 허브의 업로드 기능 파일](iot-hub-devguide-file-upload.md) tooupload 파일 너무[ Azure blob 저장소](../storage/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="71541-106">표시 하는 hello 자습서에:</span><span class="sxs-lookup"><span data-stu-id="71541-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="71541-107">파일을 업로드하기 위한 Azure blob URI를 장치에 안전하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="71541-108">앱 백 엔드에서 IoT Hub 파일 업로드 알림 tootrigger 처리 hello 파일 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="71541-109">hello [IoT 허브 시작](iot-hub-java-java-getstarted.md) 및 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-java-java-c2d.md) hello 장치-클라우드 및 클라우드-장치 메시징의 기본 기능 IoT Hub를 보여 주는 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="71541-110">hello [프로세스 장치-클라우드 메시지](iot-hub-java-java-process-d2c.md) 자습서에서는 Azure blob 저장소에 양방향 tooreliably 저장소 장치-클라우드 메시지를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="71541-111">그러나 일부 시나리오에서는 장치가 IoT Hub 수락 하는 hello 상대적으로 작은 하는 장치-클라우드 메시지에 보낼 hello 데이터 쉽게 매핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="71541-112">예:</span><span class="sxs-lookup"><span data-stu-id="71541-112">For example:</span></span>

* <span data-ttu-id="71541-113">이미지가 포함된 대형 파일</span><span class="sxs-lookup"><span data-stu-id="71541-113">Large files that contain images</span></span>
* <span data-ttu-id="71541-114">비디오</span><span class="sxs-lookup"><span data-stu-id="71541-114">Videos</span></span>
* <span data-ttu-id="71541-115">자주 샘플링되는 진동 데이터</span><span class="sxs-lookup"><span data-stu-id="71541-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="71541-116">특정 형태의 전처리된 데이터</span><span class="sxs-lookup"><span data-stu-id="71541-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="71541-117">이러한 파일은 일반적으로 일괄 처리와 같은 도구를 사용 하 여 hello 클라우드에서 [Azure Data Factory](../data-factory/index.md) 또는 hello [Hadoop](../hdinsight/index.md) 스택 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="71541-118">장치에서 tooupland 파일 필요할 때 IoT 허브의 안정성 및 보안 hello 여전히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="71541-119">이 자습서의 hello 끝에 두 개의 Java 콘솔 응용 프로그램 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="71541-120">**시뮬레이션 된 장치**, hello [IoT Hub와 송신 클라우드-장치 메시지] 자습서에서 만든 hello 응용 프로그램의 수정된 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="71541-121">이 앱이 IoT 허브에서 제공 하는 SAS URI를 사용 하 여 파일 toostorage를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="71541-122">**read-file-upload-notification** - IoT Hub에서 파일 업로드 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="71541-123">IoT Hub는 Azure IoT 장치 SDK를 통해 많은 장치 플랫폼 및 언어(C, .NET 및 Javascript 포함)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="71541-124">Toohello 참조 [Azure IoT 개발자 센터] 방법에 대 한 단계별 지침에 대 한 tooconnect 프로그램 장치 tooAzure IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="71541-125">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="71541-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="71541-126">최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="71541-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="71541-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="71541-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="71541-128">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="71541-128">An active Azure account.</span></span> <span data-ttu-id="71541-129">계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="71541-130">장치 앱에서 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="71541-130">Upload a file from a device app</span></span>

<span data-ttu-id="71541-131">이 섹션에서는 hello 장치 응용 프로그램에서 만든 수정 하면 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-java-java-c2d.md) tooupload 파일 tooIoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="71541-132">이미지 파일 toohello 복사 `simulated-device` 폴더 이름을 바꿉니다 `myimage.png`합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="71541-133">Hello를 열고 텍스트 편집기를 사용 하 여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="71541-134">Hello 변수 선언 toohello 추가 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="71541-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="71541-135">tooprocess 업로드 상태 콜백 메시지를 파일, hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="71541-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="71541-136">tooupload 이미지 tooIoT 허브 메서드 toohello 다음 hello 추가 **앱** 클래스 tooupload tooIoT 허브 이미지:</span><span class="sxs-lookup"><span data-stu-id="71541-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="71541-137">Hello 수정 **주** 메서드 toocall hello **uploadFile** hello 다음 코드 조각에에서 나와 있는 것 처럼 메서드:</span><span class="sxs-lookup"><span data-stu-id="71541-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
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

1. <span data-ttu-id="71541-138">사용 하 여 hello 다음 명령은 toobuild hello **시뮬레이션 된 장치** 응용 프로그램 및 오류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="71541-139">파일 업로드 알림 수신</span><span class="sxs-lookup"><span data-stu-id="71541-139">Receive a file upload notification</span></span>

<span data-ttu-id="71541-140">이 섹션에서는 IoT Hub에서 파일 업로드 알림 메시지를 수신하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71541-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="71541-141">Hello 필요한 **iothubowner** 이 여기서 IoT Hub toocomplete에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="71541-142">Hello에서 hello 연결 문자열을 찾을 수 있습니다 [Azure 포털](https://portal.azure.com/) hello에 **공유 액세스 정책** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="71541-143">라는 Maven 프로젝트 만들기 **파일 업로드 알림 읽기** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="71541-144">이 명령은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="71541-145">명령 프롬프트에서 새 toohello 이동 `read-file-upload-notification` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="71541-146">Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `read-file-upload-notification` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="71541-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="71541-147">Toouse hello hello 종속성을 추가 하면 **java 서비스 클라이언트 iothub** IoT 허브 서비스와 응용 프로그램 toocommunicate 프로그램에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="71541-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="71541-148">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="71541-149">저장 후 닫기 hello `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="71541-150">Hello를 열고 텍스트 편집기를 사용 하 여 `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="71541-151">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="71541-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="71541-152">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="71541-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="71541-153">hello 파일 업로드 toohello 콘솔에 대 한 정보 tooprint hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="71541-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
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

1. <span data-ttu-id="71541-154">파일 업로드 알림을 수신 하는 toostart hello 스레드 추가 코드 toohello 다음 hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="71541-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="71541-155">저장 후 닫기 hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="71541-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="71541-156">사용 하 여 hello 다음 명령은 toobuild hello **파일 업로드 알림 읽기** 응용 프로그램 및 오류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="71541-157">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="71541-157">Run hello applications</span></span>

<span data-ttu-id="71541-158">이제 준비 toorun hello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71541-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="71541-159">Hello에서 명령 프롬프트에서 `read-file-upload-notification` 폴더를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="71541-160">Hello에서 명령 프롬프트에서 `simulated-device` 폴더를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71541-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="71541-161">hello 다음 스크린 샷에서 hello 출력을에서 보여 줍니다 hello **시뮬레이션 된 장치** 앱:</span><span class="sxs-lookup"><span data-stu-id="71541-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![simulated-device 앱의 출력](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="71541-163">hello 다음 스크린 샷에서 hello 출력을에서 보여 줍니다 hello **파일 업로드 알림 읽기** 앱:</span><span class="sxs-lookup"><span data-stu-id="71541-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![read-file-upload-notification 앱의 출력](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="71541-165">구성한 hello 저장소 컨테이너에서 hello 포털 tooview hello 업로드 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![업로드된 파일](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="71541-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71541-167">Next steps</span></span>

<span data-ttu-id="71541-168">이 자습서에서는 toouse hello 파일에서 IoT Hub toosimplify 파일 업로드 장치에서의 기능을 업로드 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="71541-169">다음 문서는 hello로 tooexplore IoT 허브 기능 및 시나리오를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71541-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="71541-170">[프로그래밍 방식으로 IoT Hub 만들기][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="71541-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="71541-171">[소개 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="71541-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="71541-172">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="71541-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="71541-173">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="71541-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="71541-174">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="71541-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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


