---
title: "Connect Intel Edison (C) tooAzure IoT-문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="3f4f3-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3f4f3-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="3f4f3-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-105">Hardware issues</span></span>
<span data-ttu-id="3f4f3-106">Intel Edison에서 일반적인 문제를 해결 하는 방법에 대 한 정보를 참조 hello [공식 문제 해결 페이지](https://software.intel.com/en-us/node/637974)합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="3f4f3-107">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="3f4f3-108">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="3f4f3-108">No response during gulp tasks</span></span>
<span data-ttu-id="3f4f3-109">Gulp 작업을 실행 하는 문제가 발생 하면 hello를 추가할 수 있습니다 `--verbose` 디버깅에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="3f4f3-110">사용 하 여 tooterminate 현재 gulp 작업 시도 `Ctrl + C`, 누른 실행된 hello 다음 콘솔 창 toosee 디버그 메시지에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="3f4f3-111">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="3f4f3-112">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-112">NPM issues</span></span>
<span data-ttu-id="3f4f3-113">다음 명령을 hello로 tooupdate NPM 패키지를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="3f4f3-114">Hello 문제가 여전히 지속 되는 경우이 문서의 끝 hello에 의견을 남겨 만들거나에 GitHub 문제 우리의 [샘플 리포지토리][sample-repository]합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="3f4f3-115">Azure-CLI 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-115">Azure-CLI issues</span></span>
<span data-ttu-id="3f4f3-116">hello Azure CLI (명령줄 인터페이스 Azure) 미리 보기 빌드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="3f4f3-117">Hello에서 솔루션을 찾고 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="3f4f3-118">명령을 예상 대로 작동 하지 않는 경우 tooupgrade Azure cli toolatest 버전을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="3f4f3-119">파일 hello 도구를 사용 하 여 모든 버그를 발생 하는 경우는 [문제](https://github.com/Azure/azure-cli/issues) hello에 **문제** hello GitHub 리포지토리의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="3f4f3-120">일반적인 문제 해결 도움말에 대 한 확인 hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="3f4f3-121">충족 하는 경우 "을 찾을 수 없는 hello 요구 사항을 만족 하는 버전" 하십시오 실행된 hello 다음 명령은 tooupgrade pip toolastest 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="3f4f3-122">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="3f4f3-123">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="3f4f3-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="3f4f3-124">**pip**를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="3f4f3-125">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="3f4f3-126">일부 **pip** 이전 설치에서 패키지는 hello 사용 권한 오류를 생성 하는 루트에 의해 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="3f4f3-127">솔루션을 hello tooremove 루트에 의해 설치 된 해당 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="3f4f3-128">이 작업 단계 toocomplete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="3f4f3-129">/usr/local/lib/python2.7/site-packages로 이동</span><span class="sxs-lookup"><span data-stu-id="3f4f3-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="3f4f3-130">root에 의해 생성된 패키지를 나열입니다. `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="3f4f3-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="3f4f3-131">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="3f4f3-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="3f4f3-132">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="3f4f3-133">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="3f4f3-134">Azure IoT 허브를 구축 했습니다 했습니다 `azure-cli`, 도구 다음 시도 hello tooyour IoT 허브를 연결 하는 도구 toomanage hello 장치 필요:</span><span class="sxs-lookup"><span data-stu-id="3f4f3-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="3f4f3-135">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="3f4f3-135">Device Explorer</span></span>
<span data-ttu-id="3f4f3-136">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows 로컬 컴퓨터에서 실행 되며 Azure에서 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="3f4f3-137">Hello 다음 통신할 [IoT Hub 끝점](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="3f4f3-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="3f4f3-138">_장치 id 관리_ tooprovision IoT hub와 등록 된 장치를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="3f4f3-139">_장치-클라우드 수신_ 장치 tooyour IoT 허브에서 보낸 메시지를 모니터링할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="3f4f3-140">_클라우드-장치 보내기_ IoT 허브에서 tooyour 장치 메시지를 보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="3f4f3-141">구성 프로그램 `IoT hub connection string` 이 도구 toouse 내에서 모든 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="3f4f3-142">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="3f4f3-142">IoT hub Explorer</span></span>
<span data-ttu-id="3f4f3-143">[IoT 허브 탐색기](https://github.com/Azure/iothub-explorer) 샘플 다중 플랫폼 CLI 도구 toomanage 장치 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="3f4f3-144">Hello id 레지스트리에의 hello 도구 toomanage hello 장치를 사용 하 고, 장치-클라우드 메시지를 모니터링 하 고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="3f4f3-145">tooinstall hello (시험판) 최신 버전의 hello iothub 탐색기 도구를 hello 다음 명령줄 환경에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="3f4f3-146">다음 명령을 iothub 탐색기 명령 및 매개 변수 모두에 대 한 추가 도움말 tooget hello hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="3f4f3-147">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3f4f3-147">Azure portal</span></span>
<span data-ttu-id="3f4f3-148">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="3f4f3-149">Toouse hello 수도 [Azure 포털](../azure-portal-overview.md) toohelp 프로 비전, 관리 및 Azure 리소스를 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="3f4f3-150">Azure Storage 문제</span><span class="sxs-lookup"><span data-stu-id="3f4f3-150">Azure storage issues</span></span>
<span data-ttu-id="3f4f3-151">[Microsoft Azure 저장소 탐색기 (미리 보기)](http://storageexplorer.com) toowork와 사용할 수 있는 Microsoft에서 독립 실행형 응용 프로그램은 [Azure 저장소](https://azure.microsoft.com/en-us/services/storage/) 창, macOS 등 및 Linux에 대 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="3f4f3-152">이 도구를 사용 하 여 tooyour 테이블을 연결 하 고 그 안에 hello 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="3f4f3-153">이 도구 tootroubleshoot Azure 저장소 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f4f3-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f4f3-154">Next steps</span></span>
<span data-ttu-id="3f4f3-155">이 페이지에는 Intel Edison 키트의 가장 일반적인 문제 hello만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="3f4f3-156">또한 자세한 문제 해결에 대 한 tooreport 문제 아래쪽 메모를 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="3f4f3-157">너무 돌아가서[Intel Edison (C) 시작](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3f4f3-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started