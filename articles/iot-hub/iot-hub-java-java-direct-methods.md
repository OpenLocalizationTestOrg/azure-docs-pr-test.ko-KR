---
title: "Azure IoT Hub 직접 메서드 사용 (Java) | Microsoft Docs"
description: "Azure IoT Hub 직접 메서드를 사용하는 방법입니다. Java용 Azure IoT 장치 SDK를 사용하여 직접 메서드를 포함한 시뮬레이션된 장치 앱을 구현하며 Java용 Azure IoT service SDK를 사용하여 직접 메서드를 호출하는 서비스 앱을 구현합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6243a1a8cc971c53c797182b2beb6f594d2ac5f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="7454e-104">직접 메서드 사용(Java)</span><span class="sxs-lookup"><span data-stu-id="7454e-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="7454e-105">이 자습서에서는 다음 두 개의 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="7454e-106">**invoke-direct-method**: 시뮬레이트된 장치 앱에서 메서드를 호출하고 응답을 표시하는 Java 백엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-106">**invoke-direct-method**, a Java back-end app that calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="7454e-107">**simulated-device**: IoT Hub를 사용자가 만드는 장치 ID에 연결하는 장치를 시뮬레이트하는 Java 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-107">**simulated-device**, a Java app that simulates a device connecting to your IoT hub with the device identity you create.</span></span> <span data-ttu-id="7454e-108">이 앱은 백 엔드의 직접 호출에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-108">This app responds to the direct invoked from the back end.</span></span>

> [!NOTE]
> <span data-ttu-id="7454e-109">장치와 솔루션 백 엔드에서 실행하기 위해 응용 프로그램을 빌드하는 데 사용할 수 있는 SDK에 관한 정보는 [Azure IoT SDK][lnk-hub-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7454e-109">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="7454e-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="7454e-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="7454e-111">Java SE 8.</span></span> <br/> <span data-ttu-id="7454e-112">[개발 환경 준비][lnk-dev-setup]는 Windows 또는 Linux에서 이 자습서에 대한 Java를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="7454e-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="7454e-113">Maven 3.</span></span>  <br/> <span data-ttu-id="7454e-114">[개발 환경 준비][lnk-dev-setup]는 Windows 또는 Linux에서 이 자습서에 대한 [Maven][lnk-maven]을 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="7454e-115">[Node.js 버전 0.10.0 이상](http://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="7454e-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7454e-116">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7454e-116">Create a simulated device app</span></span>

<span data-ttu-id="7454e-117">이 섹션에서는 솔루션 백 엔드에서 호출한 메서드에 응답하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-117">In this section, you create a Java console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="7454e-118">iot-java-direct-method라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="7454e-119">명령 프롬프트에서 다음 명령을 사용하여 iot-java-direct-method 폴더에 **simulated-device**라는 새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-119">In the iot-java-direct-method folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="7454e-120">다음 명령은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-120">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="7454e-121">명령 프롬프트에서 simulated-device 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-121">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="7454e-122">텍스트 편집기를 사용하여 simulated-device 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-122">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="7454e-123">이러한 종속성을 통해 IoT Hub와 통신하도록 앱에서 iot-device-client 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-123">This dependency enables you to use the iot-device-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7454e-124">[Maven 검색][lnk-maven-device-search]을 사용하여 **iot-device-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-124">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="7454e-125">**종속성** 노드 뒤에 다음 **빌드** 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="7454e-126">이 구성에서는 Maven에 Java 1.8을 사용하여 앱을 빌드하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="7454e-127">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-127">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="7454e-128">텍스트 편집기를 사용하여 simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="7454e-129">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="7454e-130">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="7454e-131">`{youriothubname}`을 IoT 허브 이름으로 바꾸고 `{yourdevicekey}`를 *장치 ID 만들기* 섹션에서 만든 장치 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="7454e-132">이 샘플 앱은 **DeviceClient** 개체를 인스턴스화할 때 **프로토콜** 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-132">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="7454e-133">현재, 직접 메서드를 사용하려면 MQTT 프로토콜을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-133">Currently, to use direct methods you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="7454e-134">상태 코드를 IoT Hub로 반환하려면 중첩된 다음 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-134">To return a status code to your IoT hub, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="7454e-135">솔루션 백 엔드의 직접 메서드 호출을 처리하려면 중첩된 다음 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-135">To handle the direct method invocations from the solution back end, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="7454e-136">**DeviceClient**를 만들고 직접 메서드 호출을 수신 대기하려면 **main** 메서드를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-136">To create a **DeviceClient** and listen for direct method invocations, add a **main** method to the **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed to direct methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key to exit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="7454e-137">simulated-device\src\main\java\com\mycompany\app\App.java 파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-137">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="7454e-138">**simulated-device** 앱을 빌드하고 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-138">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="7454e-139">명령 프롬프트에서 simulated-device 폴더로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-139">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="7454e-140">장치에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="7454e-140">Call a direct method on a device</span></span>

<span data-ttu-id="7454e-141">이 섹션에서는 직접 메서드를 호출하고 응답을 표시하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-141">In this section, you create a Java console app that invokes a direct method and then displays the response.</span></span> <span data-ttu-id="7454e-142">이 콘솔 앱은 IoT Hub에 연결하여 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-142">This console app connects to your IoT Hub to invoke the direct method.</span></span>

1. <span data-ttu-id="7454e-143">명령 프롬프트에서 다음 명령을 사용하여 iot-java-direct-method 폴더에 **invoke-direct-method**라는 새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-143">In the iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using the following command at your command prompt.</span></span> <span data-ttu-id="7454e-144">다음 명령은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-144">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="7454e-145">명령 프롬프트에서 invoke-direct-method 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-145">At your command prompt, navigate to the invoke-direct-method folder.</span></span>

1. <span data-ttu-id="7454e-146">텍스트 편집기를 사용하여 invoke-direct-method 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-146">Using a text editor, open the pom.xml file in the invoke-direct-method folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="7454e-147">이러한 종속성을 통해 IoT Hub와 통신하도록 앱에서 iot-service-client 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-147">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7454e-148">[Maven 검색][lnk-maven-service-search]을 사용하여 **iot-service-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-148">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="7454e-149">**종속성** 노드 뒤에 다음 **빌드** 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-149">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="7454e-150">이 구성에서는 Maven에 Java 1.8을 사용하여 앱을 빌드하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-150">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="7454e-151">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-151">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="7454e-152">텍스트 편집기를 사용하여 invoke-direct-method\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-152">Using a text editor, open the invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="7454e-153">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-153">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="7454e-154">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-154">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="7454e-155">`{youriothubconnectionstring}`은 *IoT Hub 만들기* 섹션에서 기록한 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line to be written";
    ```

1. <span data-ttu-id="7454e-156">시뮬레이트된 장치에서 메서드를 호출하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-156">To invoke the method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="7454e-157">invoke-direct-method\src\main\java\com\mycompany\app\App.java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-157">Save and close the invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="7454e-158">**invoke-direct-method** 앱을 빌드하고 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-158">Build the **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="7454e-159">명령 프롬프트에서 invoke-direct-method 폴더로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-159">At your command prompt, navigate to the invoke-direct-method folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="7454e-160">앱 실행</span><span class="sxs-lookup"><span data-stu-id="7454e-160">Run the apps</span></span>

<span data-ttu-id="7454e-161">이제 콘솔 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-161">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="7454e-162">simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub의 메서드 호출에 대한 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-162">At a command prompt in the simulated-device folder, run the following command to begin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![직접 메서드 호출을 수신 대기할 Java IoT Hub 시뮬레이트된 장치 앱][8]

1. <span data-ttu-id="7454e-164">invoke-direct-method 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub의 시뮬레이트된 장치에 대해 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-164">At a command prompt in the invoke-direct-method folder, run the following command to call a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![직접 메서드 호출을 수행할 Java IoT Hub 서비스 앱][7]

1. <span data-ttu-id="7454e-166">시뮬레이트된 장치는 직접 메서드 호출에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-166">The simulated device responds to the direct method call:</span></span>

    ![Java IoT Hub 시뮬레이트된 장치 앱은 직접 메서드 호출에 응답합니다.][9]

## <a name="next-steps"></a><span data-ttu-id="7454e-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7454e-168">Next steps</span></span>

<span data-ttu-id="7454e-169">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-169">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="7454e-170">시뮬레이션된 장치 앱이 클라우드에서 호출한 메서드에 반응할 수 있도록 장치 ID를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-170">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="7454e-171">장치에서 메서드를 호출하고 장치의 응답을 표시하는 앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7454e-171">You also created an app that invokes methods on the device and displays the response from the device.</span></span>

<span data-ttu-id="7454e-172">다른 IoT 시나리오를 탐색하려면 [여러 장치에서 작업 예약][lnk-devguide-jobs]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7454e-172">To explore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="7454e-173">IoT 솔루션을 확장하고 여러 장치에서 메서드 호출을 예약하는 방법을 알아보려면 [jobs 예약 및 브로드캐스트][lnk-tutorial-jobs] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7454e-173">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
