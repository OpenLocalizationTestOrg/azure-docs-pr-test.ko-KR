---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 문제 해결 | Microsoft Docs"
description: "Intel NUC 게이트웨이 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 문제, 사물 인터넷 문제"
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="9c4d5-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="9c4d5-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="9c4d5-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="9c4d5-106">TI SensorTag는 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="9c4d5-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="9c4d5-107">tootroubleshoot SensorTag 연결 문제를 사용 하 여 hello [SensorTag 앱](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="9c4d5-108">Intel NUC에 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="9c4d5-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="9c4d5-109">tootroubleshoot 부팅 문제 참조 너무[Intel NUC의 No 부팅 문제 해결](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="9c4d5-110">tootroubleshoot 운영 체제 문제 참조 너무[Intel NUC에 운영 체제 문제 해결](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="9c4d5-111">tootroubleshoot의 다른 문제가 너무 참조[Blink 코드 및 Intel NUC에 대 한 코드 경고음을 발생시킬지](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="9c4d5-112">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="9c4d5-113">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="9c4d5-113">No response during gulp tasks</span></span>

<span data-ttu-id="9c4d5-114">Gulp 작업 실행 중에 문제가 발생 하면 hello를 추가할 수 있습니다 `--verbose` 디버깅에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="9c4d5-115">사용 하 여 tooterminate 현재 gulp 작업 시도 `Ctrl + C`, 누른 실행된 hello 다음 콘솔 창 toosee 디버그 메시지에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="9c4d5-116">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="9c4d5-117">장치 검색 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-117">Device discovery issues</span></span>

<span data-ttu-id="9c4d5-118">Hello 된 일반적인 문제 해결에 대 한 도움말 `discover-sensortag` 명령에서 확인 hello [wiki 페이지](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="9c4d5-119">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-119">npm issues</span></span>

<span data-ttu-id="9c4d5-120">Tooupdate npm 패키지를 hello 다음 명령을 실행 하 여 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="9c4d5-121">Hello 문제가 여전히 지속 되는 경우이 문서의 끝 hello에 의견을 남겨 만들거나에 GitHub 문제 우리의 [샘플 리포지토리](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="9c4d5-122">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="9c4d5-122">Remote Debugging</span></span>
> <span data-ttu-id="9c4d5-123">아래 지침은 이 자습서에서 사용된 node.js 스크립트를 디버깅하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="9c4d5-124">Hello 샘플 응용 프로그램을 디버그 모드에서 실행</span><span class="sxs-lookup"><span data-stu-id="9c4d5-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="9c4d5-125">Hello 다음 명령을 실행 하 여 디버그 모드에서 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="9c4d5-126">Hello 디버그 엔진 준비 되 면 표시 되어야 `Debugger listening on port 5858` hello 콘솔 출력에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="9c4d5-127">Visual Studio Code tooconnect toohello 원격 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="9c4d5-128">열기 hello **디버그** hello 왼쪽 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="9c4d5-129">녹색 hello 클릭 **디버깅 시작** 단추 (F5).</span><span class="sxs-lookup"><span data-stu-id="9c4d5-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="9c4d5-130">Visual Studio Code에 `launch.json` 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="9c4d5-131">업데이트 hello `launch.json` hello 콘텐츠를 다음으로 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="9c4d5-132">대체 `[device hostname or IP address]` hello 실제 장치 IP 주소 또는 호스트 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![원격 디버깅 구성](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="9c4d5-134">Toohello 원격 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="9c4d5-134">Attach toohello remote application</span></span>

<span data-ttu-id="9c4d5-135">녹색 hello 클릭 **디버깅 시작** 단추 toostart 디버깅 (F5).</span><span class="sxs-lookup"><span data-stu-id="9c4d5-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="9c4d5-136">읽기 [VS Code에서 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 디버거 hello에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![디버깅 BLE 샘플](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="9c4d5-138">Azure CLI 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-138">Azure CLI issues</span></span>

<span data-ttu-id="9c4d5-139">hello Azure CLI (명령줄 인터페이스 Azure) 미리 보기 빌드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="9c4d5-140">tooseek 솔루션 hello를 사용할 수 있습니다 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="9c4d5-141">파일 hello 도구를 사용 하 여 모든 버그를 발생 하는 경우는 [문제](https://github.com/Azure/azure-cli/issues) hello에 **문제** hello GitHub 리포지토리의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="9c4d5-142">일반적인 문제 해결에 도움이 필요 하면 확인 hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="9c4d5-143">충족 하는 경우 "을 찾을 수 없는 hello 요구 사항을 만족 하는 버전" 하십시오 실행된 hello 다음 명령은 tooupgrade pip toolastest 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="9c4d5-144">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="9c4d5-145">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="9c4d5-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="9c4d5-146">pip를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="9c4d5-147">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="9c4d5-148">이전 설치의 일부 pip 패키지가 hello 사용 권한 오류를 일으키는 루트에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="9c4d5-149">솔루션을 hello tooremove 루트에 의해 설치 된 해당 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="9c4d5-150">이 작업 단계 toocomplete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="9c4d5-151">너무 이동`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="9c4d5-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="9c4d5-152">root에 의해 생성된 패키지 나열: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="9c4d5-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="9c4d5-153">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="9c4d5-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="9c4d5-154">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="9c4d5-155">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="9c4d5-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="9c4d5-156">Hello Azure CLI로 Azure IoT 허브 성공적으로 프로 비전 한 tooyour IoT 허브를 연결 하는 도구 toomanage hello 장치 해야 하는 경우 도구 다음 hello 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="9c4d5-157">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="9c4d5-157">Device Explorer</span></span>

<span data-ttu-id="9c4d5-158">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows 로컬 컴퓨터에서 실행 되며 Azure에서 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="9c4d5-159">Hello 다음 통신할 [IoT Hub 끝점](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="9c4d5-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="9c4d5-160">장치 identity management tooprovision IoT hub와 등록 된 장치를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="9c4d5-161">장치 tooyour IoT 허브에서 보낸 메시지를 모니터링할 수 있도록 장치-클라우드를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="9c4d5-162">IoT 허브에서 tooyour 장치 메시지를 보낼 수 있도록 클라우드-장치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="9c4d5-163">이 도구 toouse 내에서 IoT 허브 연결 문자열의 모든 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="9c4d5-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="9c4d5-164">iothub-explorer</span></span>

<span data-ttu-id="9c4d5-165">[iothub 탐색기](https://github.com/Azure/iothub-explorer) 샘플 다중 플랫폼 CLI 도구 toomanage 장치 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="9c4d5-166">Hello id 레지스트리에의 hello 도구 toomanage hello 장치를 사용 하 고, 장치-클라우드 메시지를 모니터링 하 고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="9c4d5-167">tooinstall hello 최신 (시험판) 버전의 hello iothub 탐색기 도구를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="9c4d5-168">모든에 대 한 추가 도움말 tooget hello iothub 탐색기 명령 및 매개 변수, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="9c4d5-169">hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9c4d5-169">hello Azure portal</span></span>

<span data-ttu-id="9c4d5-170">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="9c4d5-171">Toouse hello 수도 [Azure 포털](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp 프로 비전, 관리 및 Azure 리소스를 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="9c4d5-172">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c4d5-172">Azure Storage issues</span></span>

<span data-ttu-id="9c4d5-173">[Microsoft Azure 저장소 탐색기 (미리 보기)](http://storageexplorer.com/) toowork Windows, macOS 등 및 Linux에서 Azure 저장소 데이터와 함께 사용할 수 있는 Microsoft에서 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="9c4d5-174">이 도구를 사용 하 여 tooyour 테이블을 연결 하 고 그 안에 hello 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="9c4d5-175">이 도구 tootroubleshoot Azure 저장소 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4d5-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
