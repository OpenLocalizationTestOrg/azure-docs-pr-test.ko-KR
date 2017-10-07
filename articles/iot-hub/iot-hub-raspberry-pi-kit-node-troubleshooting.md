---
title: "Connect Raspberry Pi (C) tooAzure IoT-문제 해결 | Microsoft Docs"
description: "Hello 라스베리 Pi Node.js 경험에 대 한 페이지 문제 해결"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 문제, 사물 인터넷 문제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="c4a31-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c4a31-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="c4a31-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="c4a31-106">hello 응용 프로그램 실행 외에 있지만 hello LED가 깜박이고 하지</span><span class="sxs-lookup"><span data-stu-id="c4a31-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="c4a31-107">이 문제는 항상 관련된 toohardware 회로 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="c4a31-108">다음 단계 tooidentify 문제 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="c4a31-109">올바른 hello 선택 했음을 확인 **GPIO** 보드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="c4a31-110">hello 두 포트 해야 **GPIO GND (Pin 6)** 및 **GPIO 04 (Pin 7)**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="c4a31-111">프로그램 led hello 극성이 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="c4a31-112">hello 긴 레그 hello 나타내야 **양의**, anode pin입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="c4a31-113">사용 하 여 hello **3.3 v 고정** 및 **GND Pin** 라스베리 Pi 3에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="c4a31-114">Pi hello DC 전원 취급 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="c4a31-115">해당 hello LED는 정상 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-115">Check that hello LED works fine.</span></span>

![LED 사양](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="c4a31-117">다른 하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-117">Other hardware issues</span></span>
<span data-ttu-id="c4a31-118">라스베리 Pi 3에 대 한 일반적인 문제를 해결 하는 방법에 대 한 정보를 참조 hello [공식 문제 해결 페이지](http://elinux.org/R-Pi_Troubleshooting)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="c4a31-119">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="c4a31-120">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="c4a31-120">No response during gulp tasks</span></span>
<span data-ttu-id="c4a31-121">Gulp 작업 실행 중에 문제가 발생 하면 hello를 추가할 수 있습니다 `--verbose` 디버깅에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="c4a31-122">Ctrl + C를 사용 하 여 tooterminate 현재 gulp 작업을 시도 하 고 다음 콘솔 창 toosee 디버그 메시지에 명령을 hello를 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4a31-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="c4a31-123">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="c4a31-124">장치 검색 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-124">Device discovery issues</span></span>
<span data-ttu-id="c4a31-125">Hello 된 일반적인 문제 해결에 대 한 도움말 `devdisco` 명령에서 확인 hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="c4a31-126">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-126">npm issues</span></span>
<span data-ttu-id="c4a31-127">Tooupdate npm 패키지를 hello 다음 명령을 사용 하 여 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="c4a31-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="c4a31-128">Hello 문제가 여전히 지속 되는 경우이 문서의 끝 hello에 의견을 남겨 만들거나에 GitHub 문제 우리의 [샘플 리포지토리](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="c4a31-129">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="c4a31-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="c4a31-130">Hello 샘플 응용 프로그램을 디버그 모드에서 실행</span><span class="sxs-lookup"><span data-stu-id="c4a31-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="c4a31-131">Hello 디버그 엔진 준비 되 면 표시 되어야 ```Debugger listening on port 5858``` hello 콘솔 출력에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="c4a31-132">Visual Studio Code tooconnect toohello 원격 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="c4a31-133">열기 hello **디버그** hello 왼쪽 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="c4a31-134">녹색 hello 클릭 **디버깅 시작** 단추 (F5).</span><span class="sxs-lookup"><span data-stu-id="c4a31-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="c4a31-135">Visual Studio Code에 launch.json 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="c4a31-136">콘텐츠를 다음 hello로 hello launch.json 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="c4a31-137">대체 `[device hostname or IP address]` hello 실제 장치 IP 주소 또는 호스트 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="c4a31-138">Visual Studio 디버깅 hello에 대 한 자세한 toolearn 너무 참조 하십시오[Visual Studio 코드에서 디버깅](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

![원격 디버깅 구성](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="c4a31-140">Toohello 원격 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="c4a31-140">Attach toohello remote application</span></span>
<span data-ttu-id="c4a31-141">녹색 hello 클릭 **디버깅 시작** 단추 toostart 디버깅 (F5).</span><span class="sxs-lookup"><span data-stu-id="c4a31-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="c4a31-142">읽기 [VS Code에서 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 디버거 hello에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![대화형 원격 디버깅](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="c4a31-144">Azure CLI 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-144">Azure CLI issues</span></span>
<span data-ttu-id="c4a31-145">hello Azure CLI (명령줄 인터페이스 Azure) 미리 보기 빌드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="c4a31-146">tooseek 솔루션 hello를 사용할 수 있습니다 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="c4a31-147">파일 hello 도구를 사용 하 여 모든 버그를 발생 하는 경우는 [문제](https://github.com/Azure/azure-cli/issues) hello에 **문제** hello GitHub 리포지토리의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="c4a31-148">일반적인 문제 해결에 도움이 필요 하면 확인 hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="c4a31-149">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="c4a31-150">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="c4a31-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="c4a31-151">pip를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="c4a31-152">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="c4a31-153">이전 설치의 일부 pip 패키지가 hello 사용 권한 오류를 일으키는 루트에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="c4a31-154">솔루션을 hello tooremove 루트에 의해 설치 된 해당 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="c4a31-155">이 작업 단계 toocomplete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="c4a31-156">/usr/local/lib/python2.7/site-packages로 이동</span><span class="sxs-lookup"><span data-stu-id="c4a31-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="c4a31-157">root에 의해 생성된 패키지 나열: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="c4a31-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="c4a31-158">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="c4a31-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="c4a31-159">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="c4a31-160">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="c4a31-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="c4a31-161">Azure CLI 있는 Azure IoT 허브를 사용 하 여 성공적으로 프로 비전 한 tooyour IoT 허브를 연결 하는 도구 toomanage hello 장치 해야 하는 경우 도구 다음 hello 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="c4a31-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="c4a31-162">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="c4a31-162">Device explorer</span></span>
<span data-ttu-id="c4a31-163">hello [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 도구 Windows 로컬 컴퓨터에서 실행 되며 Azure에서 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="c4a31-164">Hello 다음 통신할 [IoT Hub 끝점](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="c4a31-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="c4a31-165">*장치 id 관리* tooprovision IoT hub와 등록 된 장치를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="c4a31-166">*장치-클라우드 수신* 장치 tooyour IoT 허브에서 보낸 메시지를 모니터링할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="c4a31-167">*클라우드-장치 보내기* IoT 허브에서 tooyour 장치 메시지를 보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="c4a31-168">이 도구 toouse 내에서 IoT 허브 연결 문자열의 모든 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="c4a31-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="c4a31-169">iothub-explorer</span></span>
<span data-ttu-id="c4a31-170">[iothub 탐색기](https://github.com/Azure/iothub-explorer) 샘플 다중 플랫폼 CLI 도구 toomanage 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="c4a31-171">Hello id 레지스트리에의 hello 도구 toomanage hello 장치를 사용 하 고, 장치-클라우드 메시지를 모니터링 하 고, 클라우드-장치 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="c4a31-172">tooinstall hello (시험판) 최신 버전의 hello iothub 탐색기 도구를 hello 다음 명령줄 환경에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="c4a31-173">다음 명령을 iothub 탐색기 명령 및 매개 변수 모두에 대 한 추가 도움말 tooget hello hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="c4a31-174">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c4a31-174">Azure portal</span></span>
<span data-ttu-id="c4a31-175">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="c4a31-176">Toouse hello 수도 [Azure 포털](../azure-portal-overview.md) toohelp 프로 비전, 관리 및 Azure 리소스를 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="c4a31-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c4a31-177">Azure Storage issues</span></span>
<span data-ttu-id="c4a31-178">[Microsoft Azure 저장소 탐색기 (미리 보기)](http://storageexplorer.com) toowork Windows, macOS 등 및 Linux에서 Azure 저장소 데이터와 함께 사용할 수 있는 Microsoft에서 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="c4a31-179">이 도구를 사용 하 여 tooyour 테이블을 연결 하 고 그 안에 hello 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="c4a31-180">이 도구 tootroubleshoot Azure 저장소 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4a31-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

