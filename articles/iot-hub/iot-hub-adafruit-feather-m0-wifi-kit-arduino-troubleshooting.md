---
title: "Azure IoT에 Arduino(C) 연결 - 문제 해결 | Microsoft Docs"
description: "Adafruit Feather M0 WiFi Arduino 환경에 대한 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 문제 해결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="373f6-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="373f6-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="373f6-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-105">Hardware issues</span></span>
<span data-ttu-id="373f6-106">Adafruit Feather M0 WiFi Arduino 보드의 일반적인 문제 해결에 대한 내용은 [공식 문제 해결 페이지](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="373f6-107">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="373f6-108">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="373f6-108">No response during gulp tasks</span></span>
<span data-ttu-id="373f6-109">gulp 작업을 실행하다가 문제가 발생하면 디버깅을 위해 `--verbose` 옵션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="373f6-110">`Ctrl + C`를 사용하여 현재 gulp 작업의 종료를 시도한 다음 콘솔 창에서 다음 명령을 실행하여 디버그 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="373f6-111">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="373f6-112">또는 `--listen`를 추가하여 장치 로그 정보를 출력하기 위한 직렬 포트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="373f6-113">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-113">NPM issues</span></span>
<span data-ttu-id="373f6-114">다음 명령을 실행하여 NPM 패키지를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="373f6-115">문제가 지속되면 이 문서의 끝에 의견을 남기거나 [샘플 리포지토리][sample-repository]에서 GitHub 문제를 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="373f6-116">Azure CLI 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-116">Azure-CLI issues</span></span>
<span data-ttu-id="373f6-117">Azure 명령줄 인터페이스(Azure CLI)는 미리 보기 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="373f6-118">솔루션을 찾으려면 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)에서 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="373f6-119">예상대로 명령이 작동하지 않으면 Azure-cli를 최신 버전으로 업그레이드하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="373f6-120">도구에서 버그가 발견되면 GitHub 리포지토리의 **문제** 섹션에 [문제](https://github.com/Azure/azure-cli/issues)를 기록해 주세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="373f6-121">일반적인 문제 해결에 도움이 필요하면 [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)(추가 정보)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="373f6-122">"요구 사항을 만족하는 버전을 찾을 수 없습니다"라는 메시지가 나타나면 다음 명령을 실행하여 pip를 최신 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="373f6-123">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="373f6-124">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="373f6-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="373f6-125">**pip**를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="373f6-126">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="373f6-127">이전 설치의 일부 **pip** 패키지가 root에 의해 생성되었고 이로 인해 사용 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="373f6-128">해결책은 root에 의해 설치된 해당 패키지를 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="373f6-129">다음 단계를 수행하여 이 작업을 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="373f6-130">/usr/local/lib/python2.7/site-packages로 이동</span><span class="sxs-lookup"><span data-stu-id="373f6-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="373f6-131">root에 의해 생성된 패키지를 나열입니다. `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="373f6-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="373f6-132">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="373f6-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="373f6-133">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="373f6-134">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="373f6-135">`azure-cli`를 사용하여 Azure IoT Hub 프로비저닝을 완료했고 IoT Hub에 연결하는 장치를 관리할 도구가 필요하다면 다음 도구를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="373f6-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="373f6-136">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="373f6-136">Device Explorer</span></span>
<span data-ttu-id="373f6-137">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)는 Windows 로컬 컴퓨터에서 실행되며 Azure의 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="373f6-138">다음과 같은 [IoT Hub 끝점](iot-hub-devguide.md)과 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="373f6-139">*장치 ID 관리*: IoT Hub에 등록된 장치를 프로비전하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="373f6-140">*장치-클라우드 받기*: 장치에서 IoT Hub로 보내는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="373f6-141">*클라우드-장치 보내기*: IoT Hub에서 장치로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="373f6-142">모든 기능을 사용하도록 이 도구에서 `IoT hub connection string`을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="373f6-143">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="373f6-143">IoT hub Explorer</span></span>
<span data-ttu-id="373f6-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer)는 장치 클라이언트를 관리하기 위한 샘플 다중 플랫폼 CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="373f6-145">이 도구를 사용하여 ID 레지스트리에서 장치를 관리하고, 장치-클라우드 메시지를 모니터링하고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="373f6-146">iothub-explorer 도구의 최신(시험판) 버전을 설치하려면 명령줄 환경에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="373f6-147">다음 명령을 사용하면 모든 iothub-explorer 명령 및 매개 변수에 대한 추가 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="373f6-148">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="373f6-148">Azure portal</span></span>
<span data-ttu-id="373f6-149">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="373f6-150">[Azure Portal](../azure-portal-overview.md)을 사용하여 Azure 리소스에 대한 프로비전, 관리, 디버깅을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="373f6-151">Azure Storage 문제</span><span class="sxs-lookup"><span data-stu-id="373f6-151">Azure storage issues</span></span>
<span data-ttu-id="373f6-152">[Microsoft Azure Storage 탐색기(미기 보기)](http://storageexplorer.com)는 Windows, macOS 및 Linux에서 Azure Storage 데이터 작업에 사용할 수 있는 Microsoft의 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="373f6-153">이 도구를 사용하면 테이블에 연결하여 그 안에 있는 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="373f6-154">Azure Storage 문제를 해결하는 데 이 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="373f6-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md