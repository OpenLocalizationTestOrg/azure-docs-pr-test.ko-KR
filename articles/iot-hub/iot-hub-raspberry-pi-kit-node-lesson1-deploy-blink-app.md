---
featureFlags: usabilla
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 1: 앱 배포 | Microsoft Docs"
description: "GitHub에서 샘플 Node.js 응용 프로그램과, Raspberry Pi 3 보드에 이 응용 프로그램을 배포하기 위한 gulp를 복제합니다. 이 샘플 응용 프로그램은 보드에 연결된 LED를 2초마다 깜박이게 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Raspberry Pi LED 깜박임, Raspberry Pi를 통한 LED 깜박임"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="e0b2e-105">깜박임 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="e0b2e-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e0b2e-106">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="e0b2e-106">What you will do</span></span>
<span data-ttu-id="e0b2e-107">GitHub에서 샘플 Node.js 응용 프로그램을 복제하고 gulp 도구를 사용하여 Raspberry Pi 3 보드에 이 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="e0b2e-108">샘플 응용 프로그램은 보드에 연결된 LED를 2초마다 깜박이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="e0b2e-109">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e0b2e-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="e0b2e-110">What you will learn</span></span>
<span data-ttu-id="e0b2e-111">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-111">In this article, you will learn:</span></span>

* <span data-ttu-id="e0b2e-112">Pi에 관한 네트워킹 정보를 검색하기 위해 `device-discover-cli` 도구 사용 방법.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="e0b2e-113">Pi에서 샘플 응용 프로그램을 배포하고 실행하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="e0b2e-114">Pi에서 원격으로 실행되는 응용 프로그램을 배포하고 디버깅하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e0b2e-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e0b2e-115">What you need</span></span>
<span data-ttu-id="e0b2e-116">다음 작업을 성공적으로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="e0b2e-117">장치 구성</span><span class="sxs-lookup"><span data-stu-id="e0b2e-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="e0b2e-118">도구 얻기</span><span class="sxs-lookup"><span data-stu-id="e0b2e-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="e0b2e-119">Pi의 IP 주소 및 호스트 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="e0b2e-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="e0b2e-120">macOS 또는 Ubuntu의 터미널이나 Windows에서 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="e0b2e-121">출력은 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-121">You should see an output that is similar to the following:</span></span>

![장치 검색](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="e0b2e-123">Pi의 `IP address` 및 `hostname`을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="e0b2e-124">이 정보는 이 문서의 뒤 부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b2e-125">Pi가 컴퓨터와 같은 네트워크에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="e0b2e-126">예를 들어 컴퓨터는 무선 네트워크, Pi는 유선 네트워크에 연결되었다면 devdisco 출력에 IP 주소가 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="e0b2e-127">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="e0b2e-127">Clone the sample application</span></span>
<span data-ttu-id="e0b2e-128">샘플 코드를 열려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="e0b2e-129">다음 명령을 실행하여 GitHub에서 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="e0b2e-130">다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Repo 구조](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="e0b2e-132">`app` 하위 폴더의 `app.js` 파일은 LED 제어 코드가 담긴 핵심 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="e0b2e-133">응용 프로그램 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="e0b2e-133">Install application dependencies</span></span>
<span data-ttu-id="e0b2e-134">다음 명령을 실행하여 샘플 응용 프로그램에 필요한 라이브러리 및 기타 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="e0b2e-135">장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="e0b2e-135">Configure the device connection</span></span>
<span data-ttu-id="e0b2e-136">장치 연결을 구성하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="e0b2e-137">다음 명령을 실행하여 장치 구성 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="e0b2e-138">구성 파일 `config-raspberrypi.json`에는 Pi에 로그인하는 데 사용하는 사용자 자격 증명이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="e0b2e-139">사용자 자격 증명의 유출을 방지하기 위해 구성 파일은 컴퓨터 홈 폴더의 `.iot-hub-getting-started` 하위 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="e0b2e-140">다음 명령을 실행하여 Visual Studio Code에서 장치 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="e0b2e-141">자리 표시자 `[device hostname or IP address]`를 앞서 "Pi의 IP 주소 및 호스트 이름 가져오기"에서 확보한 IP 주소 또는 호스트 이름과 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="e0b2e-143">Raspberry Pi에 연결할 때 사용자 이름과 암호 대신 SSH 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="e0b2e-144">사용 하 여 키를 생성 해야 하며이 작업을 수행 하기 위해 **붙여넣으세요** 및 **@ ssh-복사-id pi\<장치 주소\>**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="e0b2e-145">Windows의 경우 이러한 명령은 **Git Bash**에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="e0b2e-146">MacOS의 경우 **brew install ssh-copy-id**를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="e0b2e-147">키를 Raspberry Pi에 업로드한 후, **config-raspberrypi.json**에서 **device_password**를 **device_key_path** 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="e0b2e-148">업데이트된 줄은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="e0b2e-149">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-149">Congratulations!</span></span> <span data-ttu-id="e0b2e-150">Pi의 첫 번째 샘플 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="e0b2e-151">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="e0b2e-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="e0b2e-152">Pi에 Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="e0b2e-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="e0b2e-153">다음 명령을 실행하여 Node.js 및 NPM을 Pi에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="e0b2e-154">이 작업의 최초 실행을 완료하려면 10분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="e0b2e-155">샘플 앱 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="e0b2e-155">Deploy and run the sample app</span></span>
<span data-ttu-id="e0b2e-156">다음 명령을 실행하여 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="e0b2e-157">앱 작동 확인</span><span class="sxs-lookup"><span data-stu-id="e0b2e-157">Verify the app works</span></span>
<span data-ttu-id="e0b2e-158">Pi에 연결된 LED가 2초마다 깜빡이는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="e0b2e-159">Led가 깜박이지 않으면 [문제 해결 가이드](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 일반적인 문제에 대한솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="e0b2e-160">![LED 깜박임](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="e0b2e-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="e0b2e-161">요약</span><span class="sxs-lookup"><span data-stu-id="e0b2e-161">Summary</span></span>
<span data-ttu-id="e0b2e-162">Pi 작동에 필요한 도구를 설치했으며 LED를 깜박이게 하는 샘플 응용 프로그램을 Pi에 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="e0b2e-163">이제 메시지 송수신을 위해 Azure IoT Hub에 Pi를 연결하는 다른 샘플 응용 프로그램을 만들고, 배포하고, 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2e-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0b2e-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0b2e-164">Next steps</span></span>
[<span data-ttu-id="e0b2e-165">Azure 도구 얻기</span><span class="sxs-lookup"><span data-stu-id="e0b2e-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

