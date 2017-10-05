---
title: "시뮬레이트된 원격 분석에서 Node.js를 사용하여 Azure IoT Suite에 Raspberry Pi 연결 | Microsoft Docs"
description: "Raspberry Pi 3 및 Azure IoT Suite에 Microsoft Azure IoT 스타터 키트를 사용합니다. Node.js를 사용하여 Raspberry Pi를 원격 모니터링 솔루션에 연결하고, 시뮬레이트된 원격 분석을 클라우드로 전송하고, 솔루션 대시보드에서 호출된 메서드에 응답합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="d3e35-104">Raspberry Pi 3를 원격 모니터링 솔루션에 연결하고 Node.js를 사용하여 시뮬레이트된 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="d3e35-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="d3e35-105">이 자습서에서는 Raspberry Pi 3를 사용하여 클라우드로 전송할 온도 및 습도 데이터를 시뮬레이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="d3e35-106">이 자습서에서는 다음을 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-106">The tutorial uses:</span></span>

- <span data-ttu-id="d3e35-107">Raspbian OS, Node.js 프로그래밍 언어 및 Node.js용 Microsoft Azure IoT SDK를 사용하여 샘플 장치를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="d3e35-108">클라우드 기반 백 엔드로 미리 구성된 IoT Suite 원격 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="d3e35-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="d3e35-109">원격 모니터링 솔루션은 Azure 구독에서 Azure 서비스 집합을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="d3e35-110">배포는 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="d3e35-111">불필요한 Azure 사용료가 부과되지 않도록 하려면 배포가 완료된 후 azureiotsuite.com에서 미리 구성된 솔루션 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="d3e35-112">미리 구성된 솔루션이 다시 필요하면 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="d3e35-113">원격 모니터링 솔루션이 실행되는 동안 소비를 감소하는 방법에 대한 자세한 내용은 [데모 목적으로 미리 구성된 Azure IoT Suite 솔루션 구성][lnk-demo-config]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3e35-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="d3e35-114">샘플 다운로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="d3e35-114">Download and configure the sample</span></span>

<span data-ttu-id="d3e35-115">이제 Raspberry Pi에서 원격 모니터링 클라이언트 응용 프로그램을 다운로드하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="d3e35-116">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="d3e35-116">Install Node.js</span></span>

<span data-ttu-id="d3e35-117">아직 그렇게 하지 않은 경우 Raspberry Pi에 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="d3e35-118">Node.js용 IoT SDK에는 Node.js 0.11.5 이상 버전의 Node.js가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="d3e35-119">다음 단계에서는 Raspberry Pi에 Node.js v6.10.2를 설치하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="d3e35-120">다음 명령을 사용하여 Raspberry Pi를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="d3e35-121">다음 명령을 사용하여 Raspberry Pi에 Node.js 이진 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="d3e35-122">다음 명령을 사용하여 이진 파일을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="d3e35-123">다음 명령을 사용하여 Node.js v6.10.2를 성공적으로 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="d3e35-124">리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="d3e35-124">Clone the repositories</span></span>

<span data-ttu-id="d3e35-125">아직 해당 작업을 수행하지 않은 경우 Pi의 터미널에서 다음 명령을 실행하여 필요한 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="d3e35-126">장치 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="d3e35-126">Update the device connection string</span></span>

<span data-ttu-id="d3e35-127">다음 명령을 사용하여 **nano** 편집기에서 샘플 원본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="d3e35-128">다음과 같은 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="d3e35-129">자리 표시자 값을 이 자습서를 시작할 때 만들어 저장한 장치 및 IoT Hub 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="d3e35-130">변경 내용을 저장하고(**Ctrl-O**, **Enter**) 편집기를 종료합니다(**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="d3e35-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="d3e35-131">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="d3e35-131">Run the sample</span></span>

<span data-ttu-id="d3e35-132">다음 명령을 실행하여 이 샘플에 대한 필수 구성 요소 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="d3e35-133">이제 Raspberry Pi에서 샘플 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="d3e35-134">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="d3e35-135">다음 샘플 출력은 Raspberry Pi의 명령 프롬프트에 표시되는 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Raspberry Pi 앱의 출력][img-raspberry-output]

<span data-ttu-id="d3e35-137">**Ctrl+C**를 눌러 언제든지 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e35-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="d3e35-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3e35-138">Next steps</span></span>

<span data-ttu-id="d3e35-139">Azure IoT에 대한 추가 샘플 및 설명서를 보려면 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="d3e35-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
