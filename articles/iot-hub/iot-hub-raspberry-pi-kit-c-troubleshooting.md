---
title: "Azure IoT에 Raspberry Pi(C) 연결 - 문제 해결 | Microsoft Docs"
description: "Raspberry Pi Node.js 환경 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IoT 문제, 사물 인터넷 문제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="5d3ea-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5d3ea-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="5d3ea-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="5d3ea-106">응용 프로그램은 잘 실행되는데 LED가 깜빡이지 않음</span><span class="sxs-lookup"><span data-stu-id="5d3ea-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="5d3ea-107">이 문제는 항상 하드웨어 회로 연결과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="5d3ea-108">다음 단계를 사용하여 문제를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="5d3ea-109">보드에서 올바른 **GPIO**를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="5d3ea-110">두 포트는 **GPIO GND(핀 6)** 및 **GPIO 04(핀 7)**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="5d3ea-111">LED의 극성이 올바른지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="5d3ea-112">다리가 긴 쪽이 **양극** 즉, 양극 핀을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="5d3ea-113">Raspberry Pi 3에서 **3.3V 핀**과 **GND 핀**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="5d3ea-114">Pi를 DC 전원으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="5d3ea-115">LED가 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-115">Check that the LED works fine.</span></span>

![LED 사양](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="5d3ea-117">다른 하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-117">Other hardware issues</span></span>
<span data-ttu-id="5d3ea-118">Raspberry Pi 3의 일반적인 문제 해결에 대한 내용은 [공식 문제 해결 페이지](http://elinux.org/R-Pi_Troubleshooting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="5d3ea-119">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="5d3ea-120">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="5d3ea-120">No response during gulp tasks</span></span>
<span data-ttu-id="5d3ea-121">gulp 작업을 실행하다가 문제가 발생하면 디버깅을 위해 `--verbose` 옵션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="5d3ea-122">`Ctrl + C`를 사용하여 현재 gulp 작업의 종료를 시도한 다음 콘솔 창에서 다음 명령을 실행하여 디버그 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="5d3ea-123">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="5d3ea-124">장치 검색 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-124">Device discovery issues</span></span>
<span data-ttu-id="5d3ea-125">`devdisco` 명령에 대한 일반적인 문제 해결에 도움이 필요하면 [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)(추가 정보)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="5d3ea-126">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-126">NPM issues</span></span>
<span data-ttu-id="5d3ea-127">다음 명령을 실행하여 NPM 패키지를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="5d3ea-128">문제가 지속되면 이 문서의 끝에 의견을 남기거나 [샘플 리포지토리](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)에서 GitHub 문제를 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="5d3ea-129">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="5d3ea-129">Remote debugging</span></span>

<span data-ttu-id="5d3ea-130">원격 디버깅 지원은 Visual Studio Code C/C++ 확장에서 곧 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="5d3ea-131">한편 좋아하는 SSH 터미널을 통해 GDB를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="5d3ea-132">Azure CLI 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-132">Azure-CLI issues</span></span>
<span data-ttu-id="5d3ea-133">Azure 명령줄 인터페이스(Azure CLI)는 미리 보기 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="5d3ea-134">솔루션을 찾으려면 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)에서 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="5d3ea-135">예상대로 명령이 작동하지 않으면 Azure-cli를 최신 버전으로 업그레이드하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="5d3ea-136">도구에서 버그가 발견되면 GitHub 리포지토리의 **문제** 섹션에 [문제](https://github.com/Azure/azure-cli/issues)를 기록해 주세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="5d3ea-137">일반적인 문제 해결에 도움이 필요하면 [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)(추가 정보)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="5d3ea-138">"요구 사항을 만족하는 버전을 찾을 수 없습니다"라는 메시지가 나타나면 다음 명령을 실행하여 pip를 최신 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="5d3ea-139">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="5d3ea-140">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="5d3ea-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="5d3ea-141">**pip**를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="5d3ea-142">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="5d3ea-143">이전 설치의 일부 **pip** 패키지가 root에 의해 생성되었고 이로 인해 사용 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="5d3ea-144">해결책은 root에 의해 설치된 해당 패키지를 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="5d3ea-145">다음 단계를 수행하여 이 작업을 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="5d3ea-146">/usr/local/lib/python2.7/site-packages로 이동</span><span class="sxs-lookup"><span data-stu-id="5d3ea-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="5d3ea-147">root에 의해 생성된 패키지를 나열입니다. `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="5d3ea-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="5d3ea-148">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="5d3ea-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="5d3ea-149">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="5d3ea-150">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="5d3ea-151">`azure-cli`를 사용하여 Azure IoT Hub 프로비저닝을 완료했고 IoT Hub에 연결하는 장치를 관리할 도구가 필요하다면 다음 도구를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="5d3ea-152">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="5d3ea-152">Device Explorer</span></span>
<span data-ttu-id="5d3ea-153">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)는 Windows 로컬 컴퓨터에서 실행되며 Azure의 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="5d3ea-154">다음과 같은 [IoT Hub 끝점](iot-hub-devguide.md)과 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="5d3ea-155">*장치 ID 관리*: IoT Hub에 등록된 장치를 프로비전하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="5d3ea-156">*장치-클라우드 받기*: 장치에서 IoT Hub로 보내는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="5d3ea-157">*클라우드-장치 보내기*: IoT Hub에서 장치로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="5d3ea-158">모든 기능을 사용하도록 이 도구에서 `IoT hub connection string`을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="5d3ea-159">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="5d3ea-159">IoT hub Explorer</span></span>
<span data-ttu-id="5d3ea-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer)는 장치 클라이언트를 관리하기 위한 샘플 다중 플랫폼 CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="5d3ea-161">이 도구를 사용하여 ID 레지스트리에서 장치를 관리하고, 장치-클라우드 메시지를 모니터링하고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="5d3ea-162">iothub-explorer 도구의 최신(시험판) 버전을 설치하려면 명령줄 환경에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="5d3ea-163">다음 명령을 사용하면 모든 iothub-explorer 명령 및 매개 변수에 대한 추가 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="5d3ea-164">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5d3ea-164">Azure portal</span></span>
<span data-ttu-id="5d3ea-165">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="5d3ea-166">[Azure Portal](../azure-portal-overview.md)을 사용하여 Azure 리소스에 대한 프로비전, 관리, 디버깅을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="5d3ea-167">Azure Storage 문제</span><span class="sxs-lookup"><span data-stu-id="5d3ea-167">Azure storage issues</span></span>
<span data-ttu-id="5d3ea-168">[Microsoft Azure Storage 탐색기(미기 보기)](http://storageexplorer.com)는 Windows, macOS 및 Linux에서 Azure Storage 데이터 작업에 사용할 수 있는 Microsoft의 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="5d3ea-169">이 도구를 사용하면 테이블에 연결하여 그 안에 있는 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="5d3ea-170">Azure Storage 문제를 해결하는 데 이 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d3ea-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
