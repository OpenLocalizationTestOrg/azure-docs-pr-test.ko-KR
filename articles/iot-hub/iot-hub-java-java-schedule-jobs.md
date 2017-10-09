---
title: "Azure IoT Hub (Java)와 aaaSchedule 작업 | Microsoft Docs"
description: "Azure IoT Hub tooschedule tooinvoke 직접적인 방법 작업 방법과 여러 장치에서 원하는 속성을 설정 합니다. Hello Azure IoT 장치 SDK를 사용 하 여 Java tooimplement hello 시뮬레이션 된 장치 앱과 hello Java tooimplement 서비스 응용 프로그램 toorun hello 작업에 대 한 Azure IoT 서비스 SDK에 대 한 합니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="ecd3b-104">작업 예약 및 브로드캐스트(Java)</span><span class="sxs-lookup"><span data-stu-id="ecd3b-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="ecd3b-105">수백만 개의 장치로 업데이트 하는 Azure IoT Hub tooschedule 및 추적 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="ecd3b-106">작업을 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-106">Use jobs to:</span></span>

* <span data-ttu-id="ecd3b-107">desired 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="ecd3b-107">Update desired properties</span></span>
* <span data-ttu-id="ecd3b-108">tags 업데이트</span><span class="sxs-lookup"><span data-stu-id="ecd3b-108">Update tags</span></span>
* <span data-ttu-id="ecd3b-109">직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="ecd3b-109">Invoke direct methods</span></span>

<span data-ttu-id="ecd3b-110">작업이 다음이 작업 중 하나를 래핑하고 트랙 hello 일련의 장치에 대 한 실행.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="ecd3b-111">장치로 이중 쿼리 hello hello 작업에 대해 실행 되는 장치 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="ecd3b-112">예를 들어 백 엔드 응용 프로그램 hello 장치를 다시 부팅 하는 장치 10, 000에서 작업 tooinvoke 직접 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="ecd3b-113">장치로 이중 쿼리로 hello 일련의 장치를 지정 하 고 hello 작업 toorun 이후 시간에 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="ecd3b-114">각 hello 장치로 작업 추적 진행 상황 hello 수신 하 고 hello 재부팅 직접 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="ecd3b-115">이러한 기능의 각각에 대해 자세히 toolearn 참조:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="ecd3b-116">장치 쌍 및 속성: [장치 쌍 시작](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="ecd3b-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="ecd3b-117">직접 메서드: [IoT Hub 개발자 가이드 - 직접 메서드](iot-hub-devguide-direct-methods.md) 및 [자습서: 직접 메서드 사용](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="ecd3b-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="ecd3b-118">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ecd3b-119">**lockDoor**라는 직접 메서드를 구현하는 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="ecd3b-120">hello 장치 앱 hello 백 엔드 응용 프로그램에서 원하는 속성 변경 내용을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="ecd3b-121">백 엔드 앱을 만드는 작업 toocall hello 만들기 **lockDoor** 여러 장치에서 직접적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="ecd3b-122">다른 작업이 toomultiple 장치를 업데이트 하는 원하는 속성을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="ecd3b-123">이 자습서의 hello 끝에 콘솔 장치 java 응용 프로그램 및 java 콘솔 백 엔드 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ecd3b-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="ecd3b-124">**시뮬레이션 된 장치** tooyour IoT 허브를 연결 하는, 구현 hello **lockDoor** 메서드와 핸들 필요한 속성 변경 내용을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="ecd3b-125">**작업 예약** 작업 toocall hello를 사용 하는 **lockDoor** 원하는 여러 장치에서 속성을 직접 메서드와 업데이트 hello 장치로 이중 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="ecd3b-126">hello 문서 [Azure IoT Sdk](iot-hub-devguide-sdks.md) toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecd3b-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ecd3b-127">Prerequisites</span></span>

<span data-ttu-id="ecd3b-128">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="ecd3b-129">최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="ecd3b-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="ecd3b-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="ecd3b-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="ecd3b-131">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-131">An active Azure account.</span></span> <span data-ttu-id="ecd3b-132">계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="ecd3b-133">Toocreate hello 장치 id를 프로그래밍 방식으로 선호 하는 경우 hello의 hello 해당 섹션을 읽어 [Java를 사용 하 여 장치 tooyour IoT 허브 연결](iot-hub-java-java-getstarted.md#create-a-device-identity) 문서.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="ecd3b-134">Hello를 사용할 수도 있습니다 [iothub 탐색기](https://github.com/Azure/iothub-explorer) 도구 tooadd 장치 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="ecd3b-135">Hello 서비스 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ecd3b-135">Create hello service app</span></span>

<span data-ttu-id="ecd3b-136">이 섹션에서는 작업을 통해 다음을 수행하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="ecd3b-137">Hello 호출 **lockDoor** 여러 장치에서 직접적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="ecd3b-138">원하는 속성 toomultiple 장치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="ecd3b-139">toocreate hello 앱:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-139">toocreate hello app:</span></span>

1. <span data-ttu-id="ecd3b-140">개발 컴퓨터에서 `iot-java-schedule-jobs`라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="ecd3b-141">Hello에 `iot-java-schedule-jobs` 폴더 라는 Maven 프로젝트를 만들 **작업 예약** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="ecd3b-142">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ecd3b-143">명령 프롬프트에서 이동 toohello `schedule-jobs` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="ecd3b-144">Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `schedule-jobs` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ecd3b-145">이 종속성 하면 toouse hello **iot 서비스 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ecd3b-146">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="ecd3b-147">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="ecd3b-148">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="ecd3b-149">저장 후 닫기 hello `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="ecd3b-150">Hello를 열고 텍스트 편집기를 사용 하 여 `schedule-jobs\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ecd3b-151">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. <span data-ttu-id="ecd3b-152">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ecd3b-153">대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="ecd3b-154">Hello 메서드 toohello 다음 추가 **앱** 클래스 tooschedule 작업 tooupdate hello **건물** 및 **Floor** 원하는 hello 장치로 이중의 속성:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. <span data-ttu-id="ecd3b-155">작업 toocall hello tooschedule **lockDoor** 메서드를 다음 메서드 toohello hello 추가 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. <span data-ttu-id="ecd3b-156">toomonitor 작업을 추가 메서드 toohello 다음 hello **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. <span data-ttu-id="ecd3b-157">를 실행 하는 hello 작업의 hello 세부 정보에 대 한 tooquery hello 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="ecd3b-158">업데이트 hello **주** 메서드 서명 tooinclude hello 다음 `throws` 절:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="ecd3b-159">toorun 및 모니터 두 가지 작업은 순차적으로 hello 코드 toohello 다음 추가 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="ecd3b-160">저장 후 닫기 hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` 파일</span><span class="sxs-lookup"><span data-stu-id="ecd3b-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="ecd3b-161">Hello 빌드 **작업 예약** 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="ecd3b-162">명령 프롬프트에서 이동 toohello `schedule-jobs` 폴더 및 다음 명령이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="ecd3b-163">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ecd3b-163">Create a device app</span></span>

<span data-ttu-id="ecd3b-164">이 섹션에서는 Java 콘솔 앱을 핸들 hello IoT Hub와 구현 hello 직접 메서드 호출에서 전송 되는 원하는 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="ecd3b-165">Hello에 `iot-java-schedule-jobs` 폴더 라는 Maven 프로젝트를 만들 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="ecd3b-166">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ecd3b-167">명령 프롬프트에서 이동 toohello `simulated-device` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="ecd3b-168">Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `simulated-device` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="ecd3b-169">이 종속성 하면 toouse hello **iot 장치 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ecd3b-170">최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="ecd3b-171">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="ecd3b-172">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="ecd3b-173">저장 후 닫기 hello `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="ecd3b-174">Hello를 열고 텍스트 편집기를 사용 하 여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ecd3b-175">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="ecd3b-176">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ecd3b-177">교체 `{youriothubname}` 을 IoT 허브 이름으로, 및 `{yourdevicekey}` hello에 생성 된 hello 장치 키 값을 가진 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="ecd3b-178">이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="ecd3b-179">현재 toouse 장치로 이중 기능 hello MQTT 프로토콜을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="ecd3b-180">tooprint 장치로 이중 알림 toohello 콘솔에서 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="ecd3b-181">tooprint 메서드 알림 toohello 직접 콘솔에서 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="ecd3b-182">IoT 허브에서 직접 메서드 호출 toohandle hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="ecd3b-183">업데이트 hello **주** 메서드 서명 tooinclude hello 다음 `throws` 절:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="ecd3b-184">다음 코드 toohello hello 추가 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="ecd3b-185">IoT Hub와 장치 클라이언트 toocommunicate를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="ecd3b-186">만들기는 **장치** toostore hello 장치로 이중 속성 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-186">Create a **Device** object toostore hello device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="ecd3b-187">toostart hello 장치 클라이언트 서비스를 추가할 코드 toohello 다음 hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="ecd3b-188">hello 사용자 toopress hello에 대 한 toowait **Enter** 종료 하기 전에 키에 추가 코드 toohello의 끝 다음 hello hello **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="ecd3b-189">저장 후 닫기 hello `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ecd3b-190">Hello 빌드 **시뮬레이션 된 장치** 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="ecd3b-191">명령 프롬프트에서 이동 toohello `simulated-device` 폴더 및 다음 명령이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="ecd3b-192">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="ecd3b-192">Run hello apps</span></span>

<span data-ttu-id="ecd3b-193">준비 toorun hello 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="ecd3b-194">Hello에서 명령 프롬프트에서 `simulated-device` hello 원하는 속성 변경 및 직접 메서드 호출에 대 한 수신 대기 하는 명령 toostart hello 장치 앱을 따라를 실행 하는 폴더:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello 장치 클라이언트 시작](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="ecd3b-196">Hello에 명령 프롬프트에서 `schedule-jobs` hello 명령 toorun hello 다음를 실행 하는 폴더 **작업 예약** 앱 toorun 두 개의 작업 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="ecd3b-197">hello hello 원하는 속성 값을 먼저 설정, 두 번째 호출 hello hello 직접적인 방법:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub 서비스 앱에서 두 개의 작업을 작성함](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="ecd3b-199">hello 장치 앱 hello 원하는 속성을 변경 하 고 hello 직접 메서드 호출을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![장치 클라이언트 hello 응답 toohello 변경 내용](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="ecd3b-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecd3b-201">Next steps</span></span>

<span data-ttu-id="ecd3b-202">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ecd3b-203">두 개의 작업 toorun 백 엔드 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="ecd3b-204">hello ल ी 원하는 속성 값, 직접 메서드를 호출 하는 hello 두 번째 작업을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="ecd3b-205">사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:</span><span class="sxs-lookup"><span data-stu-id="ecd3b-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="ecd3b-206">Hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작](iot-hub-java-java-getstarted.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="ecd3b-207">Hello로 장치를 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬 설정)를 제어할 [직접 메서드를 사용 하 여](iot-hub-java-java-direct-methods.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd3b-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
