---
title: "Azure IoT Hub 장치 관리 시작(Java) | Microsoft Docs"
description: "Azure IoT Hub 장치 관리를 사용하여 원격 장치 재부팅을 시작하는 방법입니다. Java용 Azure IoT 장치 SDK를 사용하여 직접 메서드를 포함한 시뮬레이션된 장치 앱을 구현하며 Java용 Azure IoT service SDK를 사용하여 직접 메서드를 호출하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: c75635f366f5ced4bf91792d1a905dd6aab8ed79
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="41874-104">장치 관리 시작(Java)</span><span class="sxs-lookup"><span data-stu-id="41874-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="41874-105">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="41874-106">Azure Portal을 사용하여 IoT Hub를 만들고 IoT Hub에 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="41874-107">장치를 다시 부팅하는 직접 메서드를 구현하는 시뮬레이트된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="41874-108">직접 메서드는 클라우드에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="41874-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="41874-109">IoT Hub를 통해 시뮬레이트된 장치 앱에서 재부팅 직접 메서드를 호출하는 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="41874-110">그러면 이 앱이 장치에서 보고된 속성을 모니터링하여 재부팅 작업이 완료되는 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="41874-111">이 자습서를 마치면 다음 두 가지 Java 콘솔 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="41874-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="41874-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="41874-112">**simulated-device**.</span></span> <span data-ttu-id="41874-113">이 앱의 기능:</span><span class="sxs-lookup"><span data-stu-id="41874-113">This app:</span></span>

* <span data-ttu-id="41874-114">IoT Hub를 앞에서 만든 장치 ID에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="41874-115">재부팅 직접 메서드 호출을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="41874-116">물리적 재부팅을 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="41874-117">보고된 속성을 통해 마지막 재부팅 시간을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="41874-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="41874-118">**trigger-reboot**.</span></span> <span data-ttu-id="41874-119">이 앱의 기능:</span><span class="sxs-lookup"><span data-stu-id="41874-119">This app:</span></span>

* <span data-ttu-id="41874-120">시뮬레이트된 장치 앱에서 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="41874-121">시뮬레이트된 장치에서 보낸 직접 메서드 호출에 대한 응답을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="41874-122">업데이트된 보고된 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="41874-123">장치와 솔루션 백 엔드에서 실행하기 위해 응용 프로그램을 빌드하는 데 사용할 수 있는 SDK에 관한 정보는 [Azure IoT SDK][lnk-hub-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41874-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="41874-124">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="41874-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="41874-125">Java SE 8.</span></span> <br/> <span data-ttu-id="41874-126">[개발 환경 준비][lnk-dev-setup]는 Windows 또는 Linux에서 이 자습서에 대한 Java를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="41874-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="41874-127">Maven 3.</span></span>  <br/> <span data-ttu-id="41874-128">[개발 환경 준비][lnk-dev-setup]는 Windows 또는 Linux에서 이 자습서에 대한 [Maven][lnk-maven]을 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="41874-129">[Node.js 버전 0.10.0 이상](http://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="41874-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="41874-130">직접 메서드를 사용하여 장치에서 원격 재부팅 트리거</span><span class="sxs-lookup"><span data-stu-id="41874-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="41874-131">이 섹션에서는 다음을 수행하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="41874-132">시뮬레이트된 장치 앱에서 재부팅 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="41874-133">응답을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-133">Displays the response.</span></span>
1. <span data-ttu-id="41874-134">장치에서 보낸 보고된 속성을 폴링하여 재부팅이 완료되는 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="41874-135">이 콘솔 앱은 IoT Hub에 연결하여 직접 메서드를 호출하고 보고된 속성을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="41874-136">dm-get-started라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="41874-137">명령 프롬프트에서 다음 명령을 사용하여 dm-get-started folder 폴더에 **trigger-reboot**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="41874-138">다음은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="41874-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="41874-139">명령 프롬프트에서 trigger-reboot 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="41874-140">텍스트 편집기를 사용하여 trigger-reboot 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="41874-141">이러한 종속성을 통해 IoT Hub와 통신하도록 앱에서 iot-service-client 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="41874-142">[Maven 검색][lnk-maven-service-search]을 사용하여 **iot-service-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="41874-143">**종속성** 노드 뒤에 다음 **빌드** 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="41874-144">이 구성에서는 Maven에 Java 1.8을 사용하여 앱을 빌드하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="41874-145">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="41874-146">텍스트 편집기를 사용하여 trigger-reboot\src\main\java\com\mycompany\app\App.java 원본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41874-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="41874-147">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-147">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="41874-148">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="41874-149">`{youriothubconnectionstring}`은 *IoT Hub 만들기* 섹션에서 기록한 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41874-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="41874-150">장치 쌍에서 10초마다 보고되는 속성을 읽는 스레드를 구현하려면 **App** 클래스에 다음 중첩 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="41874-151">시뮬레이트된 장치에서 재부팅 직접 메서드를 호출하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-151">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="41874-152">시뮬레이트된 장치에서 보고된 속성을 스레드가 폴링을 시작하도록 하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-152">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="41874-153">앱을 중지할 수 있도록 하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-153">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="41874-154">trigger-reboot\src\main\java\com\mycompany\app\App.java 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-154">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="41874-155">**trigger-reboot** 백 엔드 앱을 빌드하고 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-155">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="41874-156">명령 프롬프트에서 trigger-reboot 폴더로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-156">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="41874-157">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="41874-157">Create a simulated device app</span></span>

<span data-ttu-id="41874-158">이 섹션에서는 장치를 시뮬레이트하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="41874-159">이 앱은 IoT Hub의 재부팅 직접 메서드 호출을 수신하고 그 즉시 해당 호출에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-159">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="41874-160">그런 다음 잠시 유휴 상태로 전환하여 재부팅 프로세스를 시뮬레이트한 후 보고된 속성을 사용하여 **trigger-reboot** 백 엔드 앱에 재부팅이 완료되었음을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="41874-160">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="41874-161">명령 프롬프트에서 다음 명령을 사용하여 dm-get-started 폴더에 **simulated-device**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41874-161">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="41874-162">다음은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="41874-162">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="41874-163">명령 프롬프트에서 simulated-device 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-163">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="41874-164">텍스트 편집기를 사용하여 simulated-device 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-164">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="41874-165">이러한 종속성을 통해 IoT Hub와 통신하도록 앱에서 iot-service-client 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-165">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="41874-166">[Maven 검색][lnk-maven-device-search]을 사용하여 **iot-device-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-166">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="41874-167">**종속성** 노드 뒤에 다음 **빌드** 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-167">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="41874-168">이 구성에서는 Maven에 Java 1.8을 사용하여 앱을 빌드하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-168">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="41874-169">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-169">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="41874-170">텍스트 편집기를 사용하여 simulated-device\src\main\java\com\mycompany\app\App.java 원본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41874-170">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="41874-171">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-171">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="41874-172">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-172">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="41874-173">`{yourdeviceconnectionstring}`을 *장치 ID 만들기* 섹션에서 기록해 둔 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41874-173">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="41874-174">직접 메서드 상태 이벤트에 대한 콜백 처리기를 구현하려면 **App** 클래스에 다음 중첩 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-174">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="41874-175">장치 쌍 상태 이벤트에 대한 콜백 처리기를 구현하려면 **App** 클래스에 다음 중첩 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-175">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="41874-176">속성 이벤트에 대한 콜백 처리기를 구현하려면 **App** 클래스에 다음 중첩 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-176">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="41874-177">장치 재부팅을 시뮬레이트하는 스레드를 구현하려면 **App** 클래스에 다음 중첩 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-177">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="41874-178">이 스레드는 5초 동안 유휴 상태를 유지한 후 **lastReboot** 보고된 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-178">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="41874-179">장치에서 직접 메서드를 구현하려면 **App** 클래스에 다음 중첩 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-179">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="41874-180">시뮬레이트된 앱은 **재부팅** 직접 메서드에 대한 호출을 수신하면 호출자에게 수신 확인을 반환한 후 재부팅을 처리하기 위한 스레드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-180">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="41874-181">다음 예외를 throw하도록 **main** 메서드의 서명을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-181">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="41874-182">**DeviceClient**를 인스턴스화하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-182">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="41874-183">직접 메서드 호출 수신을 시작하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-183">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="41874-184">장치 시뮬레이터를 종료하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-184">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="41874-185">simulated-device\src\main\java\com\mycompany\app\App.java 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-185">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="41874-186">**simulated-device** 백 엔드 앱을 빌드하고 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-186">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="41874-187">명령 프롬프트에서 simulated-device 폴더로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-187">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="41874-188">앱 실행</span><span class="sxs-lookup"><span data-stu-id="41874-188">Run the apps</span></span>

<span data-ttu-id="41874-189">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41874-189">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="41874-190">simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub의 재부팅 메서드 호출에 대한 수신 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-190">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![재부팅 직접 메서드 호출을 수신 대기할 Java IoT Hub 시뮬레이트된 장치 앱][1]

1. <span data-ttu-id="41874-192">trigger-reboot 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub의 시뮬레이트된 장치에 대해 재부팅 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-192">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![재부팅 직접 메서드를 호출할 Java IoT Hub 서비스 앱][2]

1. <span data-ttu-id="41874-194">시뮬레이트된 장치는 재부팅 직접 메서드 호출에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="41874-194">The simulated device responds to the reboot direct method call:</span></span>

    ![Java IoT Hub 시뮬레이트된 장치 앱은 직접 메서드 호출에 응답합니다.][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22