---
title: "Azure IoT Hub aaaUse 직접 메서드 (Java) | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub는 메서드를 전달 합니다. Hello Azure IoT 장치 SDK를 사용 하 여 Java tooimplement 직접적인 방법 및 hello Java tooimplement hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK 포함 하는 시뮬레이션 된 장치 앱에 대 한 합니다."
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
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="c0a67-104">직접 메서드 사용(Java)</span><span class="sxs-lookup"><span data-stu-id="c0a67-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="c0a67-105">이 자습서에서는 다음 두 개의 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="c0a67-106">**직접-메서드 호출**, hello 시뮬레이션 된 장치 응용 프로그램의 메서드를 호출 하 고 hello 응답을 표시 하는 Java 백 엔드 앱.</span><span class="sxs-lookup"><span data-stu-id="c0a67-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="c0a67-107">**시뮬레이션 된 장치**, tooyour IoT hub를 만들면 hello 장치 id를 사용 하 여 연결 하는 장치를 시뮬레이션 하는 Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="c0a67-108">이 응용 프로그램 응답 toohello hello 백 엔드에서 직접 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="c0a67-109">장치 및 백 엔드 솔루션에서 응용 프로그램 toorun toobuild를 사용할 수 있는 Sdk hello에 대 한 정보를 참조 하십시오. [Azure IoT Sdk][lnk-hub-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="c0a67-110">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="c0a67-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c0a67-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="c0a67-111">Java SE 8.</span></span> <br/> <span data-ttu-id="c0a67-112">[개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 Java tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c0a67-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="c0a67-113">Maven 3.</span></span>  <br/> <span data-ttu-id="c0a67-114">[개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 tooinstall [Maven] [ lnk-maven] Windows 또는 Linux에서이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c0a67-115">[Node.js 버전 0.10.0 이상](http://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="c0a67-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c0a67-116">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c0a67-116">Create a simulated device app</span></span>

<span data-ttu-id="c0a67-117">이 섹션에서는 응답 tooa 메서드 끝 hello 솔루션 다시에서 호출 하 여 Java 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="c0a67-118">iot-java-direct-method라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="c0a67-119">Hello java 직접 메서드 iot 폴더에서 만들 라는 Maven 프로젝트 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="c0a67-120">다음 명령을 hello은 단일, 긴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c0a67-121">명령 프롬프트 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="c0a67-122">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 시뮬레이션 된 장치 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="c0a67-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="c0a67-123">이 종속성 있습니다 toouse hello iot 장치 클라이언트에서에서 패키지를 IoT hub와 사용자 응용 프로그램 toocommunicate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c0a67-124">최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-device-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="c0a67-125">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="c0a67-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c0a67-126">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="c0a67-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c0a67-127">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="c0a67-128">텍스트 편집기를 사용 하 여 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c0a67-129">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="c0a67-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="c0a67-130">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c0a67-131">교체 `{youriothubname}` 을 IoT 허브 이름으로, 및 `{yourdevicekey}` hello에 생성 된 hello 장치 키 값을 가진 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="c0a67-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="c0a67-132">이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="c0a67-133">현재 toouse 직접 hello MQTT 프로토콜을 사용 해야 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="c0a67-134">상태 코드 tooyour IoT 허브를 tooreturn hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="c0a67-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c0a67-135">hello 솔루션 백 엔드 toohandle hello 직접 메서드 호출 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="c0a67-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="c0a67-136">toocreate는 **DeviceClient** 직접 메서드 호출에 대 한 수신 대기 하 고, 추가 **주** 메서드 toohello **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="c0a67-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="c0a67-137">저장 후 닫기 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일</span><span class="sxs-lookup"><span data-stu-id="c0a67-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="c0a67-138">Hello 빌드 **시뮬레이션 된 장치** 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c0a67-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="c0a67-139">명령 프롬프트에서 다음 명령이 실행된 hello 및 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="c0a67-140">장치에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="c0a67-140">Call a direct method on a device</span></span>

<span data-ttu-id="c0a67-141">이 섹션에서는 직접 메서드를 호출 하 고 다음 hello 응답을 표시 하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="c0a67-142">이 콘솔 응용 프로그램 tooyour IoT Hub tooinvoke hello에 대 한 직접 메서드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="c0a67-143">Hello java 직접 메서드 iot 폴더에서 만들 라는 Maven 프로젝트 **-직접-메서드 호출** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="c0a67-144">다음 명령을 hello은 단일, 긴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c0a67-145">명령 프롬프트 toohello-직접-메서드 호출 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="c0a67-146">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello-직접-메서드 호출 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="c0a67-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c0a67-147">이 종속성 있습니다 toouse hello iot 서비스 클라이언트에서에서 패키지를 IoT hub와 사용자 응용 프로그램 toocommunicate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c0a67-148">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-service-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="c0a67-149">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="c0a67-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c0a67-150">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="c0a67-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c0a67-151">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="c0a67-152">텍스트 편집기를 사용 하 여 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c0a67-153">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="c0a67-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="c0a67-154">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c0a67-155">대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:</span><span class="sxs-lookup"><span data-stu-id="c0a67-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="c0a67-156">hello 시뮬레이션 된 장치에서 tooinvoke hello 메서드 추가 코드 toohello 다음 hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="c0a67-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="c0a67-157">저장 후 닫기 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 파일</span><span class="sxs-lookup"><span data-stu-id="c0a67-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="c0a67-158">Hello 빌드 **-직접-메서드 호출** 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c0a67-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="c0a67-159">명령 프롬프트 toohello-직접-메서드 호출 폴더 및 다음 명령이 실행된 hello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="c0a67-160">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="c0a67-160">Run hello apps</span></span>

<span data-ttu-id="c0a67-161">준비 toorun hello 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="c0a67-162">Hello 시뮬레이션 된 장치 폴더에서 명령 프롬프트에서 다음 명령을 toobegin IoT 허브에서 메서드 호출을 수신 대기 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub에 장치 앱 toolisten 직접 메서드 호출에 대 한 시뮬레이션 된][8]

1. <span data-ttu-id="c0a67-164">Hello-직접-메서드 호출 폴더에 명령 프롬프트에서 다음 명령을 toocall hello 메서드가 장치에서 실행 시뮬레이션 IoT 허브에서:</span><span class="sxs-lookup"><span data-stu-id="c0a67-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 toocall 직접적인 방법][7]

1. <span data-ttu-id="c0a67-166">hello 시뮬레이션 된 장치 응답 toohello 직접 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-166">hello simulated device responds toohello direct method call:</span></span>

    ![Java IoT Hub 시뮬레이션 된 장치 응용 프로그램 응답 toohello 직접 메서드 호출][9]

## <a name="next-steps"></a><span data-ttu-id="c0a67-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0a67-168">Next steps</span></span>

<span data-ttu-id="c0a67-169">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="c0a67-170">이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 tooreact toomethods hello 클라우드 호출한 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="c0a67-171">또한 hello 장치에 대 한 메서드를 호출 하 고 hello 장치에서 hello 응답을 표시 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="c0a67-172">tooexplore IoT 시나리오도 참조 [여러 장치에서 작업을 예약][lnk-devguide-jobs]합니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="c0a67-173">toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c0a67-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
