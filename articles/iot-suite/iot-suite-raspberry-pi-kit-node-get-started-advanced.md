---
title: "aaaConnect 라스베리 Pi tooAzure Node.js toosupport 펌웨어를 사용 하 여 IoT Suite 업데이트 | Microsoft Docs"
description: "Hello 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트 hello와, Azure IoT Suite를 사용 합니다. 프로그램 라스베리 Pi toohello 모니터링 솔루션 원격 Node.js tooconnect를 사용 하 여, toohello 클라우드 센서에서 원격 분석을 전송 하 고 원격 펌웨어 업데이트를 수행 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="ffa5a-104">원격 모니터링 솔루션 라스베리 Pi 3 toohello 사용자를 연결 하 고 Node.js를 사용 하 여 원격 펌웨어 업데이트를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ffa5a-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="ffa5a-105">이 자습서 toouse 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="ffa5a-106">Hello 클라우드와 통신할 수 있는 온도 및 습도 판독기를 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="ffa5a-107">사용 하도록 설정 하 고 hello 라스베리 Pi에서 원격 펌웨어 업데이트 tooupdate hello 클라이언트 응용 프로그램을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="ffa5a-108">hello 자습서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-108">hello tutorial uses:</span></span>

- <span data-ttu-id="ffa5a-109">Raspbian OS 프로그래밍 언어를 Node.js hello 및 Node.js tooimplement 샘플 장치에 대 한 Microsoft Azure IoT SDK hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-109">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="ffa5a-110">hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="ffa5a-111">개요</span><span class="sxs-lookup"><span data-stu-id="ffa5a-111">Overview</span></span>

<span data-ttu-id="ffa5a-112">이 자습서의 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-112">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="ffa5a-113">Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="ffa5a-114">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="ffa5a-115">설정 하면 장치 및 센서 toocommunicate 컴퓨터 및 hello와 원격 솔루션 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="ffa5a-116">Hello 샘플 장치 코드 tooconnect toohello 원격 모니터링 솔루션을 업데이트 하 고 hello 솔루션 대시보드에서 볼 수 있는 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
- <span data-ttu-id="ffa5a-117">Hello 샘플 장치 코드 tooupdate hello 클라이언트 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="ffa5a-118">원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="ffa5a-119">hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="ffa5a-120">종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="ffa5a-121">미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="ffa5a-122">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="ffa5a-123">다운로드 하 고 hello 샘플 구성</span><span class="sxs-lookup"><span data-stu-id="ffa5a-123">Download and configure hello sample</span></span>

<span data-ttu-id="ffa5a-124">이제 다운로드 하 고 라스베리 원주율 hello 원격 모니터링 클라이언트 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="ffa5a-125">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="ffa5a-125">Install Node.js</span></span>

<span data-ttu-id="ffa5a-126">아직 그렇게 하지 않은 경우 Raspberry Pi에 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="ffa5a-127">Node.js 용 IoT SDK hello 0.11.5 이상 버전의 Node.js 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-127">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="ffa5a-128">hello 다음 단계 방법을 보여 줍니다 라스베리 원주율 tooinstall Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="ffa5a-128">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="ffa5a-129">다음 명령은 tooupdate hello 라스베리 Pi를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-129">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="ffa5a-130">다음 명령은 toodownload hello Node.js 바이너리 tooyour 라스베리 Pi hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-130">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="ffa5a-131">사용 하 여 hello 다음 명령 tooinstall hello 이진 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-131">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="ffa5a-132">Node.js v6.10.2를 성공적으로 설치한 명령 tooverify 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-132">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="ffa5a-133">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="ffa5a-133">Clone hello repositories</span></span>

<span data-ttu-id="ffa5a-134">아직 수행 하지 않은 경우 복제 hello를 실행 하 여 저장소 hello 나오는 명령에 Pi에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-134">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="ffa5a-135">Hello 장치 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="ffa5a-135">Update hello device connection string</span></span>

<span data-ttu-id="ffa5a-136">Hello에 샘플 구성 파일을 열고 hello **nano** hello 다음 명령을 사용 하 여 편집기:</span><span class="sxs-lookup"><span data-stu-id="ffa5a-136">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="ffa5a-137">Hello 장치 id와 만들고이 자습서의 시작 부분 hello에 저장 된 IoT 허브 정보 hello 자리 표시자 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-137">Replace hello placeholder values with hello device id and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="ffa5a-138">완료 되 면 다음 예제는 hello 같이 hello hello deviceinfo 파일 내용의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-138">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="ffa5a-139">변경 내용을 저장 (**Ctrl-O**, **Enter**) 및 exit hello 편집기 (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="ffa5a-139">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="ffa5a-140">Hello 예제 실행</span><span class="sxs-lookup"><span data-stu-id="ffa5a-140">Run hello sample</span></span>

<span data-ttu-id="ffa5a-141">실행된 hello 다음 tooinstall hello hello 샘플에 대 한 필수 구성 요소 패키지가 명령:</span><span class="sxs-lookup"><span data-stu-id="ffa5a-141">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="ffa5a-142">이제 라스베리 Pi hello에 hello 샘플 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-142">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="ffa5a-143">Hello 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-143">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="ffa5a-144">hello 다음 샘플 출력은 hello 라스베리 Pi hello 명령 프롬프트에서 참조 하는 hello 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-144">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Raspberry Pi 앱의 출력][img-raspberry-output]

<span data-ttu-id="ffa5a-146">키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-146">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="ffa5a-147">Hello 솔루션 대시보드 클릭 **장치** toovisit hello **장치** 페이지.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-147">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="ffa5a-148">Hello에 라스베리 Pi 선택 **장치 목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-148">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="ffa5a-149">그런 다음 **메서드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-149">Then choose **Methods**:</span></span>

    ![대시보드에서 장치 나열][img-list-devices]

1. <span data-ttu-id="ffa5a-151">Hello에 **메서드 호출** 페이지에서 선택 **InitiateFirmwareUpdate** hello에 **메서드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-151">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="ffa5a-152">Hello에 **FWPackageURI** 필드에, 입력 **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-152">In hello **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="ffa5a-153">이 파일에는 hello 펌웨어 버전 2.0의 hello 구현을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-153">This file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="ffa5a-154">**InvokeMethod**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="ffa5a-155">hello 응용 프로그램에 액세스 hello 라스베리 Pi 승인 백 toohello 솔루션 대시보드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-155">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="ffa5a-156">다음 hello 펌웨어 hello 새 버전을 다운로드 하 여 hello 펌웨어 업데이트 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-156">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![메서드 기록 표시][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="ffa5a-158">Hello 펌웨어 업데이트 프로세스를 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-158">Observe hello firmware update process</span></span>

<span data-ttu-id="ffa5a-159">Hello 장치에서 실행 되는 때에 hello 펌웨어 업데이트 프로세스를 확인할 수 및 hello를 확인 하 여 hello 솔루션 대시보드에 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-159">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="ffa5a-160">Hello 라스베리 Pi에 hello 업데이트 프로세스에서 hello 진행 상황을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-160">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![업데이트 진행률 표시][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="ffa5a-162">hello 업데이트가 완료 되 면 hello 원격 모니터링 응용 프로그램 다시 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-162">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="ffa5a-163">Hello 명령을 사용 하 여 `ps -ef` tooverify 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-163">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="ffa5a-164">Hello를 사용 하 여 tooterminate hello 프로세스를 사용 하도록 하려는 경우 `kill` 명령을 hello 프로세스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-164">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="ffa5a-165">Hello 솔루션 포털에서 hello 장치에서 보고 hello 펌웨어 업데이트의 hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-165">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="ffa5a-166">hello 다음 스크린샷은 hello 상태 및 기간이 hello 새로운 펌웨어 버전 및 hello 업데이트 프로세스의 각 단계:</span><span class="sxs-lookup"><span data-stu-id="ffa5a-166">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![작업 상태 보기][img-job-status]

    <span data-ttu-id="ffa5a-168">뒤로 toohello 대시보드를 탐색 하면 hello 장치에서 여전히 hello 펌웨어 업데이트를 수행 하는 원격 분석을 보내는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-168">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="ffa5a-169">Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-169">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="ffa5a-170">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-170">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="ffa5a-171">사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-171">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa5a-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffa5a-172">Next steps</span></span>

<span data-ttu-id="ffa5a-173">Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa5a-173">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
