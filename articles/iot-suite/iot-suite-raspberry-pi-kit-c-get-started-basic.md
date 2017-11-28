---
title: "aaaConnect 라스베리 Pi tooAzure IoT Suite C를 사용 하 여 실제 센서와 | Microsoft Docs"
description: "Hello 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트 hello와, Azure IoT Suite를 사용 합니다. C tooconnect 프로그램 라스베리 Pi toohello 원격 모니터링 솔루션을 사용 하 고 toohello 클라우드 센서에서 원격 분석을 전송 toomethods hello 솔루션 대시보드에서 호출에 응답 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="e02af-104">원격 모니터링 솔루션 라스베리 Pi 3 toohello 사용자를 연결 하 고 C를 사용 하 여 실제 센서에서 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="e02af-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="e02af-105">이 자습서에서는 어떻게 toouse hello Microsoft Azure IoT 시작 키트 toodevelop 라스베리 Pi 3에 대 한 hello 클라우드와 통신할 수 있는 온도 및 습도 판독기입니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="e02af-106">hello 자습서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-106">hello tutorial uses:</span></span>

- <span data-ttu-id="e02af-107">Raspbian OS, hello C 프로그래밍 언어 및 C tooimplement 샘플 장치에 대 한 Microsoft Azure IoT SDK hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="e02af-108">hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="e02af-109">개요</span><span class="sxs-lookup"><span data-stu-id="e02af-109">Overview</span></span>

<span data-ttu-id="e02af-110">이 자습서의 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="e02af-111">Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="e02af-112">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="e02af-113">설정 하면 장치 및 센서 toocommunicate 컴퓨터 및 hello와 원격 솔루션 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="e02af-114">Hello 샘플 장치 코드 tooconnect toohello 원격 모니터링 솔루션을 업데이트 하 고 hello 솔루션 대시보드에서 볼 수 있는 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="e02af-115">원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="e02af-116">hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="e02af-117">종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="e02af-118">미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="e02af-119">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="e02af-120">다운로드 하 고 hello 샘플 구성</span><span class="sxs-lookup"><span data-stu-id="e02af-120">Download and configure hello sample</span></span>

<span data-ttu-id="e02af-121">이제 다운로드 하 고 라스베리 원주율 hello 원격 모니터링 클라이언트 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="e02af-122">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="e02af-122">Clone hello repositories</span></span>

<span data-ttu-id="e02af-123">아직 이미 하지 않은 경우 복제 hello 나오는 프로그램 Pi에 따라 종료에서 명령을 실행 하 여 저장소 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="e02af-124">Hello 장치 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="e02af-124">Update hello device connection string</span></span>

<span data-ttu-id="e02af-125">Hello open hello 샘플 소스 파일 **nano** hello 다음 명령을 사용 하 여 편집기:</span><span class="sxs-lookup"><span data-stu-id="e02af-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="e02af-126">Hello를 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="e02af-127">Hello 장치와 IoT 허브 정보를 만들고이 자습서의 시작 부분 hello에 저장 된 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="e02af-128">변경 내용을 저장 (**Ctrl-O**, **Enter**) 및 exit hello 편집기 (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="e02af-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="e02af-129">Hello 예제 빌드</span><span class="sxs-lookup"><span data-stu-id="e02af-129">Build hello sample</span></span>

<span data-ttu-id="e02af-130">Hello 나오는 라스베리 Pi hello에 따라 종료에서 명령을 실행 하 여 C에 대 한 Microsoft Azure IoT 장치 SDK hello에 대 한 hello 필수 구성 요소 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="e02af-131">이제 hello 라스베리 Pi에서 업데이트 하는 hello 샘플 솔루션을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="e02af-132">이제 라스베리 Pi hello에 hello 샘플 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="e02af-133">Hello 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="e02af-134">hello 다음 샘플 출력은 hello 라스베리 Pi hello 명령 프롬프트에서 참조 하는 hello 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Raspberry Pi 앱의 출력][img-raspberry-output]

<span data-ttu-id="e02af-136">키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="e02af-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e02af-137">Next steps</span></span>

<span data-ttu-id="e02af-138">Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="e02af-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
