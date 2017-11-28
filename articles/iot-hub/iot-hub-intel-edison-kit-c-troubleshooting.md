---
title: "Azure IoT에 Intel Edison(C) 연결 - 문제 해결 | Microsoft Docs"
description: "Intel Edison C 환경에 대한 페이지 문제 해결"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 문제 해결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dd6338ad29e0bb858c33e5bb24b8f41d3c22575a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="09501-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="09501-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="09501-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="09501-105">Hardware issues</span></span>
<span data-ttu-id="09501-106">Intel Edison의 일반적인 문제 해결에 대한 내용은 [공식 문제 해결 페이지](https://software.intel.com/en-us/node/637974)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="09501-107">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="09501-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="09501-108">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="09501-108">No response during gulp tasks</span></span>
<span data-ttu-id="09501-109">gulp 작업을 실행하다가 문제가 발생하면 디버깅을 위해 `--verbose` 옵션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="09501-110">`Ctrl + C`를 사용하여 현재 gulp 작업의 종료를 시도한 다음 콘솔 창에서 다음 명령을 실행하여 디버그 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="09501-111">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="09501-112">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="09501-112">NPM issues</span></span>
<span data-ttu-id="09501-113">다음 명령을 실행하여 NPM 패키지를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="09501-114">문제가 지속되면 이 문서의 끝에 의견을 남기거나 [샘플 리포지토리][sample-repository]에서 GitHub 문제를 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="09501-115">Azure CLI 문제</span><span class="sxs-lookup"><span data-stu-id="09501-115">Azure-CLI issues</span></span>
<span data-ttu-id="09501-116">Azure 명령줄 인터페이스(Azure CLI)는 미리 보기 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="09501-116">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="09501-117">솔루션을 찾으려면 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)에서 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-117">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="09501-118">예상대로 명령이 작동하지 않으면 Azure-cli를 최신 버전으로 업그레이드하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-118">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="09501-119">도구에서 버그가 발견되면 GitHub 리포지토리의 **문제** 섹션에 [문제](https://github.com/Azure/azure-cli/issues)를 기록해 주세요.</span><span class="sxs-lookup"><span data-stu-id="09501-119">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="09501-120">일반적인 문제 해결에 도움이 필요하면 [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)(추가 정보)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-120">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="09501-121">"요구 사항을 만족하는 버전을 찾을 수 없습니다"라는 메시지가 나타나면 다음 명령을 실행하여 pip를 최신 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-121">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="09501-122">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="09501-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="09501-123">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="09501-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="09501-124">**pip**를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="09501-125">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="09501-126">이전 설치의 일부 **pip** 패키지가 root에 의해 생성되었고 이로 인해 사용 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-126">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="09501-127">해결책은 root에 의해 설치된 해당 패키지를 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09501-127">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="09501-128">다음 단계를 수행하여 이 작업을 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="09501-128">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="09501-129">/usr/local/lib/python2.7/site-packages로 이동</span><span class="sxs-lookup"><span data-stu-id="09501-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="09501-130">root에 의해 생성된 패키지를 나열입니다. `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="09501-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="09501-131">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="09501-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="09501-132">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="09501-133">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="09501-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="09501-134">`azure-cli`를 사용하여 Azure IoT Hub 프로비저닝을 완료했고 IoT Hub에 연결하는 장치를 관리할 도구가 필요하다면 다음 도구를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="09501-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="09501-135">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="09501-135">Device Explorer</span></span>
<span data-ttu-id="09501-136">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)는 Windows 로컬 컴퓨터에서 실행되며 Azure의 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="09501-137">다음과 같은 [IoT Hub 끝점](iot-hub-devguide.md)과 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-137">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="09501-138">_장치 ID 관리_: IoT Hub에 등록된 장치를 프로비전하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-138">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="09501-139">_장치-클라우드 받기_: 장치에서 IoT Hub로 보내는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-139">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="09501-140">_클라우드-장치 보내기_: IoT Hub에서 장치로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-140">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="09501-141">모든 기능을 사용하도록 이 도구에서 `IoT hub connection string`을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-141">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="09501-142">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="09501-142">IoT hub Explorer</span></span>
<span data-ttu-id="09501-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer)는 장치 클라이언트를 관리하기 위한 샘플 다중 플랫폼 CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="09501-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="09501-144">이 도구를 사용하여 ID 레지스트리에서 장치를 관리하고, 장치-클라우드 메시지를 모니터링하고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-144">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="09501-145">iothub-explorer 도구의 최신(시험판) 버전을 설치하려면 명령줄 환경에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="09501-145">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="09501-146">다음 명령을 사용하면 모든 iothub-explorer 명령 및 매개 변수에 대한 추가 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-146">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="09501-147">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="09501-147">Azure portal</span></span>
<span data-ttu-id="09501-148">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09501-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="09501-149">[Azure Portal](../azure-portal-overview.md)을 사용하여 Azure 리소스에 대한 프로비전, 관리, 디버깅을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-149">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="09501-150">Azure Storage 문제</span><span class="sxs-lookup"><span data-stu-id="09501-150">Azure storage issues</span></span>
<span data-ttu-id="09501-151">[Microsoft Azure Storage 탐색기(미리 보기)](http://storageexplorer.com)는 Windows, macOS 및 Linux에서 [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) 데이터 작업에 사용할 수 있는 Microsoft의 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="09501-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="09501-152">이 도구를 사용하면 테이블에 연결하여 그 안에 있는 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-152">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="09501-153">Azure Storage 문제를 해결하는 데 이 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-153">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09501-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09501-154">Next steps</span></span>
<span data-ttu-id="09501-155">이 페이지에는 Intel Edison 키트의 가장 일반적인 문제만 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-155">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="09501-156">또한 하단에 의견을 남겨 추가 문제 해결에 대한 문제를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09501-156">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="09501-157">[Intel Edison(C) 시작](iot-hub-intel-edison-kit-c-get-started.md)으로 돌아가기</span><span class="sxs-lookup"><span data-stu-id="09501-157">Go back to [Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started