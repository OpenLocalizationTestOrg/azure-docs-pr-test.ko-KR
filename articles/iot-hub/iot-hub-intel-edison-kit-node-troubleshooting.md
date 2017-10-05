---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 4: 문제 해결 | Microsoft Docs"
description: "Intel Edison Node.js 환경 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 문제 해결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="71785-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="71785-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="71785-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="71785-105">Hardware issues</span></span>
<span data-ttu-id="71785-106">Intel Edison의 일반적인 문제 해결에 대한 내용은 [공식 문제 해결 페이지](https://software.intel.com/en-us/node/637974)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="71785-107">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="71785-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="71785-108">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="71785-108">No response during gulp tasks</span></span>
<span data-ttu-id="71785-109">gulp 작업을 실행하다가 문제가 발생하면 디버깅을 위해 `--verbose` 옵션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="71785-110">`Ctrl + C`를 사용하여 현재 gulp 작업의 종료를 시도한 다음 콘솔 창에서 다음 명령을 실행하여 디버그 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="71785-111">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="71785-112">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="71785-112">NPM issues</span></span>
<span data-ttu-id="71785-113">다음 명령을 실행하여 NPM 패키지를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="71785-114">문제가 지속되면 이 문서의 끝에 의견을 남기거나 [샘플 리포지토리][sample-repository]에서 GitHub 문제를 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="71785-115">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="71785-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="71785-116">디버그 모드에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="71785-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="71785-117">디버그 엔진이 준비되면 콘솔 출력에서 ```Debugger listening on port 5858```이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="71785-118">원격 장치에 연결하도록 VS Code 구성</span><span class="sxs-lookup"><span data-stu-id="71785-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="71785-119">왼쪽의 **디버그** 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="71785-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="71785-120">녹색 **디버깅 시작**(F5) 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="71785-121">VS Code에 업데이트할 **launch.json** 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="71785-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="71785-122">**launch.json** 파일을 다음 내용으로 업데이트하고 `[device hostname or IP address]`를 실제 장치 IP 주소 또는 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="71785-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![원격 디버깅 구성](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="71785-124">원격 응용 프로그램에 연결</span><span class="sxs-lookup"><span data-stu-id="71785-124">Attach to the remote application</span></span>

<span data-ttu-id="71785-125">녹색 **디버깅 시작**(F5) 단추를 클릭하여 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="71785-126">디버거에 대해 자세히 알아보려면 [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging)(VS Code의 JavaScript)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![대화형 원격 디버깅](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="71785-128">Azure-CLI 문제</span><span class="sxs-lookup"><span data-stu-id="71785-128">Azure-CLI issues</span></span>
<span data-ttu-id="71785-129">Azure 명령줄 인터페이스(Azure CLI)는 미리 보기 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="71785-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="71785-130">솔루션을 찾으려면 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)에서 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="71785-131">예상대로 명령이 작동하지 않으면 Azure-cli를 최신 버전으로 업그레이드하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="71785-132">도구에서 버그가 발견되면 GitHub 리포지토리의 **문제** 섹션에 [문제](https://github.com/Azure/azure-cli/issues)를 기록해 주세요.</span><span class="sxs-lookup"><span data-stu-id="71785-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="71785-133">일반적인 문제 해결에 도움이 필요하면 [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)(추가 정보)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="71785-134">"요구 사항을 만족하는 버전을 찾을 수 없습니다"라는 메시지가 나타나면 다음 명령을 실행하여 pip를 최신 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="71785-135">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="71785-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="71785-136">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="71785-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="71785-137">**pip**를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="71785-138">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="71785-139">이전 설치의 일부 **pip** 패키지가 root에 의해 생성되었고 이로 인해 사용 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="71785-140">해결책은 root에 의해 설치된 해당 패키지를 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="71785-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="71785-141">다음 단계를 수행하여 이 작업을 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="71785-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="71785-142">/usr/local/lib/python2.7/site-packages로 이동</span><span class="sxs-lookup"><span data-stu-id="71785-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="71785-143">root에 의해 생성된 패키지를 나열입니다. `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="71785-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="71785-144">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="71785-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="71785-145">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="71785-146">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="71785-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="71785-147">`azure-cli`를 사용하여 Azure IoT Hub 프로비저닝을 완료했고 IoT Hub에 연결하는 장치를 관리할 도구가 필요하다면 다음 도구를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="71785-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="71785-148">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="71785-148">Device Explorer</span></span>
<span data-ttu-id="71785-149">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)는 Windows 로컬 컴퓨터에서 실행되며 Azure의 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="71785-150">다음과 같은 [IoT Hub 끝점](iot-hub-devguide.md)과 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="71785-151">_장치 ID 관리_: IoT Hub에 등록된 장치를 프로비전하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="71785-152">_장치-클라우드 받기_: 장치에서 IoT Hub로 보내는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="71785-153">_클라우드-장치 보내기_: IoT Hub에서 장치로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="71785-154">모든 기능을 사용하도록 이 도구에서 `IoT hub connection string`을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="71785-155">IoT hub Explorer</span><span class="sxs-lookup"><span data-stu-id="71785-155">IoT hub Explorer</span></span>
<span data-ttu-id="71785-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer)는 장치 클라이언트를 관리하기 위한 샘플 다중 플랫폼 CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="71785-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="71785-157">이 도구를 사용하여 ID 레지스트리에서 장치를 관리하고, 장치-클라우드 메시지를 모니터링하고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="71785-158">iothub-explorer 도구의 최신(시험판) 버전을 설치하려면 명령줄 환경에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71785-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="71785-159">다음 명령을 사용하면 모든 iothub-explorer 명령 및 매개 변수에 대한 추가 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="71785-160">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="71785-160">Azure portal</span></span>
<span data-ttu-id="71785-161">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71785-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="71785-162">[Azure Portal](../azure-portal-overview.md)을 사용하여 Azure 리소스에 대한 프로비전, 관리, 디버깅을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="71785-163">Azure Storage 문제</span><span class="sxs-lookup"><span data-stu-id="71785-163">Azure storage issues</span></span>
<span data-ttu-id="71785-164">[Microsoft Azure Storage 탐색기(미리 보기)](http://storageexplorer.com)는 Windows, macOS 및 Linux에서 [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) 데이터 작업에 사용할 수 있는 Microsoft의 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="71785-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="71785-165">이 도구를 사용하면 테이블에 연결하여 그 안에 있는 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="71785-166">Azure Storage 문제를 해결하는 데 이 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71785-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71785-167">Next steps</span></span>
<span data-ttu-id="71785-168">이 페이지에는 Intel Edison 키트의 가장 일반적인 문제만 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="71785-169">또한 하단에 의견을 남겨 추가 문제 해결에 대한 문제를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71785-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="71785-170">[Intel Edison(Node.js) 시작](iot-hub-intel-edison-kit-node-get-started.md)으로 돌아가기</span><span class="sxs-lookup"><span data-stu-id="71785-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started