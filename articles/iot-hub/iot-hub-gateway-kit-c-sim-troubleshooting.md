---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 문제 해결 | Microsoft Docs"
description: "Intel NUC 게이트웨이 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 문제, 사물 인터넷 문제"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="82ff4-104">문제 해결</span><span class="sxs-lookup"><span data-stu-id="82ff4-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="82ff4-105">하드웨어 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="82ff4-106">TI SensorTag는 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="82ff4-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="82ff4-107">SensorTag 연결 문제를 해결하려면 [SensorTag 앱](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="82ff4-108">Intel NUC에 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="82ff4-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="82ff4-109">부팅 문제를 해결하려면 [문제 해결 Intel® NUC 제품에서 부트되지 않는 문제](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="82ff4-110">운영 체제 문제를 해결하려면 [Intel NUC의 운영 체제 문제 해결](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="82ff4-111">다른 문제를 해결하려면 [Intel NUC에 대한 깜박임 코드 및 경고음 코드](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="82ff4-112">Node.js 패키지 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="82ff4-113">gulp 작업 중 응답 없음</span><span class="sxs-lookup"><span data-stu-id="82ff4-113">No response during gulp tasks</span></span>

<span data-ttu-id="82ff4-114">gulp 작업을 실행하다가 문제가 발생하면 디버깅을 위해 `--verbose` 옵션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="82ff4-115">`Ctrl + C`를 사용하여 현재 gulp 작업의 종료를 시도한 다음 콘솔 창에서 다음 명령을 실행하여 디버그 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="82ff4-116">콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="82ff4-117">장치 검색 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-117">Device discovery issues</span></span>

<span data-ttu-id="82ff4-118">`discover-sensortag` 명령에 대한 일반적인 문제 해결에 도움이 필요하면 [wiki 페이지](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="82ff4-119">NPM 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-119">npm issues</span></span>

<span data-ttu-id="82ff4-120">다음 명령을 실행하여 NPM 패키지를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="82ff4-121">문제가 지속되면 이 문서의 끝에 의견을 남기거나 [샘플 리포지토리](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started)에서 GitHub 문제를 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="82ff4-122">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="82ff4-122">Remote Debugging</span></span>
> <span data-ttu-id="82ff4-123">아래 지침은 이 자습서에서 사용된 node.js 스크립트를 디버깅하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="82ff4-124">디버그 모드에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="82ff4-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="82ff4-125">다음 명령을 실행하여 디버그 모드에서 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="82ff4-126">디버그 엔진이 준비되면 콘솔 출력에 `Debugger listening on port 5858`이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="82ff4-127">원격 장치에 연결하도록 Visual Studio Code 구성</span><span class="sxs-lookup"><span data-stu-id="82ff4-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="82ff4-128">왼쪽의 **디버그** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="82ff4-129">녹색 **디버깅 시작**(F5) 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="82ff4-130">Visual Studio Code에 `launch.json` 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="82ff4-131">다음 내용이 포함된 `launch.json` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="82ff4-132">`[device hostname or IP address]`를 실제 장치 IP 주소 또는 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="82ff4-134">원격 응용 프로그램에 연결</span><span class="sxs-lookup"><span data-stu-id="82ff4-134">Attach to the remote application</span></span>

<span data-ttu-id="82ff4-135">녹색 **디버깅 시작**(F5) 단추를 클릭하여 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="82ff4-136">디버거에 대해 자세히 알아보려면 [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging)(VS Code의 JavaScript)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![디버깅 BLE 샘플](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="82ff4-138">Azure CLI 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-138">Azure CLI issues</span></span>

<span data-ttu-id="82ff4-139">Azure 명령줄 인터페이스(Azure CLI)는 미리 보기 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="82ff4-140">해결책을 검색하려면 [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)(미리 보기 설치 가이드)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="82ff4-141">도구에서 버그가 발견되면 GitHub 리포지토리의 **문제** 섹션에 [문제](https://github.com/Azure/azure-cli/issues)를 기록해 주세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="82ff4-142">일반적인 문제 해결에 도움이 필요하면 [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)(추가 정보)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="82ff4-143">"요구 사항을 만족하는 버전을 찾을 수 없습니다"라는 메시지가 나타나면 다음 명령을 실행하여 pip를 최신 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="82ff4-144">Python 설치 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="82ff4-145">레거시 설치 문제(macOS)</span><span class="sxs-lookup"><span data-stu-id="82ff4-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="82ff4-146">pip를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="82ff4-147">이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="82ff4-148">이전 설치의 일부 pip 패키지가 root에 의해 생성되었고 이로 인해 권한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="82ff4-149">해결책은 root에 의해 설치된 해당 패키지를 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="82ff4-150">다음 단계를 수행하여 이 작업을 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="82ff4-151">`/usr/local/lib/python2.7/site-packages`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="82ff4-152">root에 의해 생성된 패키지 나열: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="82ff4-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="82ff4-153">2단계의 패키지 제거: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="82ff4-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="82ff4-154">Python을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="82ff4-155">Azure IoT Hub 문제</span><span class="sxs-lookup"><span data-stu-id="82ff4-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="82ff4-156">Azure CLI를 사용하여 Azure IoT Hub 프로비저닝을 완료했고 IoT Hub에 연결하는 장치를 관리할 도구가 필요하다면 다음 도구를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="82ff4-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="82ff4-157">장치 탐색기</span><span class="sxs-lookup"><span data-stu-id="82ff4-157">Device Explorer</span></span>

<span data-ttu-id="82ff4-158">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)는 Windows 로컬 컴퓨터에서 실행되며 Azure의 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="82ff4-159">다음과 같은 [IoT Hub 끝점](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/)과 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="82ff4-160">장치 ID 관리: IoT Hub에 등록된 장치를 프로비전하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="82ff4-161">장치-클라우드 받기: 장치에서 IoT Hub로 보내는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="82ff4-162">클라우드-장치 보내기: IoT Hub에서 장치로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="82ff4-163">모든 기능을 사용하도록 이 도구에서 IoT Hub 연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="82ff4-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="82ff4-164">iothub-explorer</span></span>

<span data-ttu-id="82ff4-165">[iothub-explorer](https://github.com/Azure/iothub-explorer)는 장치 클라이언트를 관리하기 위한 샘플 다중 플랫폼 CLI 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="82ff4-166">이 도구를 사용하여 ID 레지스트리에서 장치를 관리하고, 장치-클라우드 메시지를 모니터링하고, 클라우드-장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="82ff4-167">iothub-explorer 도구의 최신(시험판) 버전을 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="82ff4-168">모든 iothub-explorer 명령 및 매개 변수에 대한 추가 도움말을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="82ff4-169">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="82ff4-169">The Azure portal</span></span>

<span data-ttu-id="82ff4-170">전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="82ff4-171">[Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/)을 사용하여 Azure 리소스에 대한 프로비전, 관리, 디버깅을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="82ff4-172">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="82ff4-172">Azure Storage issues</span></span>

<span data-ttu-id="82ff4-173">[Microsoft Azure Storage 탐색기(미기 보기)](http://storageexplorer.com/)는 Windows, macOS 및 Linux에서 Azure Storage 데이터 작업에 사용할 수 있는 Microsoft의 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="82ff4-174">이 도구를 사용하면 테이블에 연결하여 그 안에 있는 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="82ff4-175">Azure Storage 문제를 해결하는 데 이 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82ff4-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
