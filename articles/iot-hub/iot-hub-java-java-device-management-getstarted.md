---
title: "Azure IoT Hub 장치 관리 (Java) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub 장치 관리 tooinitiate 원격 장치를 다시 부팅 합니다. Hello Azure IoT 장치 SDK를 사용 하 여 Java tooimplement 직접적인 방법 및 hello Java tooimplement hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK 포함 하는 시뮬레이션 된 장치 앱에 대 한 합니다."
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
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="d6a25-104">장치 관리 시작(Java)</span><span class="sxs-lookup"><span data-stu-id="d6a25-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="d6a25-105">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d6a25-106">Azure 포털 toocreate IoT Hub hello를 사용 하 및 IoT 허브에서 장치 id를 만드는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="d6a25-107">직접적인 방법 tooreboot hello 장치를 구현 하는 시뮬레이션 된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="d6a25-108">Hello 클라우드에서 직접 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="d6a25-109">다시 부팅 hello IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하는 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="d6a25-110">이 응용 프로그램 다음 hello 다시 부팅 작업이 완료 되 면 hello 장치 toosee에서 속성을 보고 된 hello 모니터입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="d6a25-111">이 자습서의 hello 끝에 두 개의 Java 콘솔 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="d6a25-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="d6a25-112">**simulated-device**.</span></span> <span data-ttu-id="d6a25-113">이 앱의 기능:</span><span class="sxs-lookup"><span data-stu-id="d6a25-113">This app:</span></span>

* <span data-ttu-id="d6a25-114">앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="d6a25-115">재부팅 직접 메서드 호출을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="d6a25-116">물리적 재부팅을 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="d6a25-117">보고 속성을 통해 hello 마지막 재부팅 hello 시간을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="d6a25-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="d6a25-118">**trigger-reboot**.</span></span> <span data-ttu-id="d6a25-119">이 앱의 기능:</span><span class="sxs-lookup"><span data-stu-id="d6a25-119">This app:</span></span>

* <span data-ttu-id="d6a25-120">Hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="d6a25-121">Hello 시뮬레이션 된 장치에서 전송 하는 hello 응답 toohello 직접 메서드 호출을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="d6a25-122">업데이트 표시 hello 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="d6a25-123">장치 및 백 엔드 솔루션에서 응용 프로그램 toorun toobuild를 사용할 수 있는 Sdk hello에 대 한 정보를 참조 하십시오. [Azure IoT Sdk][lnk-hub-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="d6a25-124">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="d6a25-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="d6a25-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="d6a25-125">Java SE 8.</span></span> <br/> <span data-ttu-id="d6a25-126">[개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 Java tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d6a25-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="d6a25-127">Maven 3.</span></span>  <br/> <span data-ttu-id="d6a25-128">[개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 tooinstall [Maven] [ lnk-maven] Windows 또는 Linux에서이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d6a25-129">[Node.js 버전 0.10.0 이상](http://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="d6a25-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="d6a25-130">트리거는 직접 메서드를 사용 하 여 hello 장치에 원격 컴퓨터를 다시 부팅</span><span class="sxs-lookup"><span data-stu-id="d6a25-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="d6a25-131">이 섹션에서는 다음을 수행하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="d6a25-132">Hello hello 시뮬레이션 된 장치 응용 프로그램에서 다시 부팅 직접 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="d6a25-133">Hello 응답을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-133">Displays hello response.</span></span>
1. <span data-ttu-id="d6a25-134">설문 hello hello 다시 부팅이 완료 되 면 hello 장치 toodetermine에서 전송 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="d6a25-135">이 콘솔 응용 프로그램 연결 tooyour IoT Hub tooinvoke hello 직접적인 방법 및 읽기 hello 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="d6a25-136">dm-get-started라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="d6a25-137">Hello dm get 시작 폴더에서 라는 Maven 프로젝트를 만듭니다 **트리거를 다시 부팅** hello 다음 명령 프롬프트에서 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="d6a25-138">hello 다음에는 단일, 긴 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="d6a25-139">명령 프롬프트 toohello 트리거를 다시 부팅 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="d6a25-140">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 트리거를 다시 부팅 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d6a25-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="d6a25-141">이 종속성 있습니다 toouse hello iot 서비스 클라이언트에서에서 패키지를 IoT hub와 사용자 응용 프로그램 toocommunicate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d6a25-142">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-service-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="d6a25-143">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d6a25-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="d6a25-144">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="d6a25-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="d6a25-145">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="d6a25-146">텍스트 편집기를 사용 하 여 hello trigger-reboot\src\main\java\com\mycompany\app\App.java 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="d6a25-147">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="d6a25-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="d6a25-148">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="d6a25-149">대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:</span><span class="sxs-lookup"><span data-stu-id="d6a25-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="d6a25-150">tooimplement hello를 읽을 수 있는 스레드 속성을 보고 hello 장치로 이중 10 초 마다 추가 hello 다음 중첩 클래스 toohello **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="d6a25-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="d6a25-151">tooinvoke hello 재부팅 hello 시뮬레이션 된 장치에서 직접 메서드 추가 코드 toohello 다음 hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d6a25-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="d6a25-152">toostart hello 스레드 toopoll hello hello 시뮬레이션 된 장치에서 보고 된 속성, 다음 코드 toohello hello 추가 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d6a25-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="d6a25-153">tooenable 하면 toostop hello 응용 프로그램, 코드 toohello 다음 hello 추가 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d6a25-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="d6a25-154">저장 하 고 hello trigger-reboot\src\main\java\com\mycompany\app\App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="d6a25-155">Hello 빌드 **트리거를 다시 부팅** 백 엔드 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d6a25-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="d6a25-156">명령 프롬프트 toohello 트리거를 다시 부팅 폴더 및 다음 명령이 실행된 hello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d6a25-157">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d6a25-157">Create a simulated device app</span></span>

<span data-ttu-id="d6a25-158">이 섹션에서는 장치를 시뮬레이트하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="d6a25-159">hello 앱 IoT 허브에서 hello 재부팅 직접 메서드 호출에 대 한 수신 하 고 즉시 toothat 호출 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="d6a25-160">앱 다음 잠시 동안 대기한 hello toosimulate hello 다시 부팅 프로세스 보고 속성 toonotify hello를 사용 하기 전에 **트리거를 다시 부팅** hello 다시 부팅 하는 백 엔드 앱이 완성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="d6a25-161">Hello dm get 시작 폴더에서 라는 Maven 프로젝트를 만듭니다 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="d6a25-162">hello 다음은 단일, 긴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="d6a25-163">명령 프롬프트 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="d6a25-164">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 시뮬레이션 된 장치 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d6a25-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="d6a25-165">이 종속성 있습니다 toouse hello iot 서비스 클라이언트에서에서 패키지를 IoT hub와 사용자 응용 프로그램 toocommunicate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d6a25-166">최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-device-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="d6a25-167">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d6a25-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="d6a25-168">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="d6a25-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="d6a25-169">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="d6a25-170">텍스트 편집기를 사용 하 여 hello simulated-device\src\main\java\com\mycompany\app\App.java 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="d6a25-171">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="d6a25-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="d6a25-172">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="d6a25-173">대체 `{yourdeviceconnectionstring}` hello에서 기록한 hello 장치 연결 문자열과 함께 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="d6a25-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="d6a25-174">직접적인 방법 상태 이벤트에 대 한 콜백 처리기 tooimplement hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="d6a25-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="d6a25-175">장치로 이중 상태 이벤트에 대 한 콜백 처리기 tooimplement hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="d6a25-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="d6a25-176">속성 이벤트에 대 한 콜백 처리기 tooimplement hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="d6a25-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="d6a25-177">스레드 toosimulate hello 장치를 다시 부팅, tooimplement hello 다음 추가 클래스 toohello 중첩 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="d6a25-178">5 초 동안 대기 하 고 다음 hello를 설정 하는 hello 스레드 **lastReboot** 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="d6a25-179">hello 장치에서 tooimplement hello 직접적인 방법 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="d6a25-180">Hello 시뮬레이트된 응용 프로그램 호출 toohello를 받을 때 **재부팅** 직접적인 방법 승인을 toohello 발신자를 반환 하 고 다음 시작 스레드 tooprocess hello를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="d6a25-181">Hello의 hello 서명을 수정 **주** 메서드 toothrow hello 다음 예외:</span><span class="sxs-lookup"><span data-stu-id="d6a25-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="d6a25-182">tooinstantiate는 **DeviceClient**, 다음 코드 toohello hello 추가 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d6a25-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="d6a25-183">직접 메서드 호출을 수신 대기 toostart 추가 코드 toohello 다음 hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d6a25-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="d6a25-184">hello 장치 시뮬레이터 아래로 tooshut 추가 코드 toohello 다음 hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d6a25-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="d6a25-185">저장 하 고 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="d6a25-186">Hello 빌드 **시뮬레이션 된 장치** 백 엔드 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d6a25-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="d6a25-187">명령 프롬프트에서 다음 명령이 실행된 hello 및 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="d6a25-188">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="d6a25-188">Run hello apps</span></span>

<span data-ttu-id="d6a25-189">준비 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d6a25-190">Hello 시뮬레이션 된 장치 폴더에서 명령 프롬프트에서 다음 명령을 toobegin IoT 허브에서 다시 부팅 메서드 호출을 수신 대기 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![다시 부팅 직접 메서드 호출에 대 한 시뮬레이션 된 Java IoT Hub 장치 앱 toolisten][1]

1. <span data-ttu-id="d6a25-192">Hello 트리거를 다시 부팅 폴더에서 명령 프롬프트에서 hello IoT 허브에서 명령 toocall hello 재부팅 메서드 시뮬레이션 된 장치에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 toocall hello 직접 메서드를 다시 부팅][2]

1. <span data-ttu-id="d6a25-194">시뮬레이션 된 장치 hello toohello 재부팅 직접 메서드 호출을 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a25-194">hello simulated device responds toohello reboot direct method call:</span></span>

    ![Java IoT Hub 시뮬레이션 된 장치 응용 프로그램 응답 toohello 직접 메서드 호출][3]

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