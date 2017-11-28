---
featureFlags: usabilla
title: "라스베리 Pi (노드) tooAzure IoT-1과 연결: 앱 배포 | Microsoft Docs"
description: "GitHub에서 hello 샘플 Node.js 응용 프로그램을 복제 하 고이 응용 프로그램 tooyour 라스베리 Pi 3 보드 toodeploy gulp 합니다. 이 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다."
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
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="cb0a6-105">만들기 및 hello 깜박임 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="cb0a6-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cb0a6-106">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="cb0a6-106">What you will do</span></span>
<span data-ttu-id="cb0a6-107">GitHub에서 hello 샘플 Node.js 응용 프로그램을 복제 하 고 hello gulp 도구 toodeploy hello 샘플 응용 프로그램 tooyour 라스베리 Pi 3을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-107">Clone hello sample Node.js application from GitHub and use hello gulp tool toodeploy hello sample application tooyour Raspberry Pi 3.</span></span> <span data-ttu-id="cb0a6-108">hello 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="cb0a6-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cb0a6-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="cb0a6-110">What you will learn</span></span>
<span data-ttu-id="cb0a6-111">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-111">In this article, you will learn:</span></span>

* <span data-ttu-id="cb0a6-112">어떻게 toouse hello `device-discover-cli` 도구 tooretrieve 네트워킹 Pi에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="cb0a6-113">어떻게 toodeploy 및 실행된 hello 샘플 원주율 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="cb0a6-114">어떻게 toodeploy 및 디버그 응용 프로그램 플랫폼에서 원격으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cb0a6-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="cb0a6-115">What you need</span></span>
<span data-ttu-id="cb0a6-116">성공적으로 완료 해야 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="cb0a6-117">장치 구성</span><span class="sxs-lookup"><span data-stu-id="cb0a6-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="cb0a6-118">Hello 도구 가져오기</span><span class="sxs-lookup"><span data-stu-id="cb0a6-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="cb0a6-119">Pi의 hello IP 주소 및 호스트 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="cb0a6-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="cb0a6-120">Windows 또는 macOS 또는 Ubuntu, 터미널 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="cb0a6-121">Toohello 다음과 유사한 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-121">You should see an output that is similar toohello following:</span></span>

![장치 검색](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="cb0a6-123">Hello를 메모해 `IP address` 및 `hostname` Pi의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="cb0a6-124">이 정보는 이 문서의 뒤 부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="cb0a6-125">Pi 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="cb0a6-126">예를 들어 컴퓨터는 연결 된 tooa 무선 네트워크 Pi는 유선 네트워크 연결된 tooa를 동안 표시 될 수 없습니다 hello IP hello devdisco 출력에는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="cb0a6-127">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="cb0a6-127">Clone hello sample application</span></span>
<span data-ttu-id="cb0a6-128">tooopen hello 샘플 코드, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-128">tooopen hello sample code, follow these steps:</span></span>

1. <span data-ttu-id="cb0a6-129">Hello 다음 명령을 실행 하 여 GitHub에서 hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="cb0a6-130">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Repo 구조](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="cb0a6-132">hello `app.js` hello에 대 한 파일 `app` 하위 폴더는 hello 코드 toocontrol hello LED가 있는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-132">hello `app.js` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="cb0a6-133">응용 프로그램 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="cb0a6-133">Install application dependencies</span></span>
<span data-ttu-id="cb0a6-134">Hello 라이브러리 및 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램에 필요한 다른 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="cb0a6-135">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="cb0a6-135">Configure hello device connection</span></span>
<span data-ttu-id="cb0a6-136">tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="cb0a6-137">Hello 다음 명령을 실행 하 여 hello 장치 구성 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="cb0a6-138">hello 구성 파일 `config-raspberrypi.json` toolog tooPi에서 사용 하 여 hello 사용자 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="cb0a6-139">tooavoid hello 누수 hello 하위 폴더에 사용자 자격 증명의 hello 구성 파일이 생성 됩니다 `.iot-hub-getting-started` hello 컴퓨터에서 홈 폴더의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="cb0a6-140">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 장치 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="cb0a6-141">Hello 자리 표시자 대체 `[device hostname or IP address]` hello IP 주소 또는 "얻기 hello IP 주소 및 호스트 이름 Pi의"에서 이전에 가져온 hello 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="cb0a6-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="cb0a6-143">Pi tooRaspberry 연결할 때 사용자 이름 및 암호 대신 SSH 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="cb0a6-144">순서로 toodo toogenerate hello 사용 하 여 키 해야이 **붙여넣으세요** 및 **@ ssh-복사-id pi\<장치 주소\>**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="cb0a6-145">Windows의 경우 이러한 명령은 **Git Bash**에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="cb0a6-146">Toorun MacOS에서 필요한 **brew 설치 ssh-복사-id**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="cb0a6-147">Hello 키 toohello 라스베리 Pi을 성공적으로 업로드 한 후 교체 **device_password** 와 **device_key_path** 속성 **config raspberrypi.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="cb0a6-148">업데이트된 줄은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="cb0a6-149">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-149">Congratulations!</span></span> <span data-ttu-id="cb0a6-150">Hello 첫 번째 Pi에 대 한 샘플 응용 프로그램을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="cb0a6-151">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="cb0a6-151">Deploy and run hello sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="cb0a6-152">Pi에 Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="cb0a6-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="cb0a6-153">Node.js 및 NPM 원주율 hello 다음 명령을 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-153">Install Node.js and NPM on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="cb0a6-154">이 태스크는 처음 실행 하면 10 분 toocomplete hello를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-154">This task might take 10 minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="cb0a6-155">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="cb0a6-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="cb0a6-156">배포 하 고 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="cb0a6-157">Hello 앱 작동 확인</span><span class="sxs-lookup"><span data-stu-id="cb0a6-157">Verify hello app works</span></span>
<span data-ttu-id="cb0a6-158">이제 2 초 마다 깜박입니다.이 Pi에 hello LED 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-158">You should now see hello LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="cb0a6-159">Hello led가 깜박입니다.이 표시 되지 않으면 참조 hello [문제 해결 가이드](iot-hub-raspberry-pi-kit-node-troubleshooting.md) toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="cb0a6-160">![LED 깜박임](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="cb0a6-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="cb0a6-161">요약</span><span class="sxs-lookup"><span data-stu-id="cb0a6-161">Summary</span></span>
<span data-ttu-id="cb0a6-162">필요한 hello 도구 toowork Pi와 함께 설치 하 고 샘플 응용 프로그램 tooPi tooblink hello LED를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="cb0a6-163">있습니다 수 이제 만들고, 배포, 및 Pi tooAzure toosend IoT 허브를 연결 하는 또 다른 샘플 응용 프로그램을 실행 하 고 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb0a6-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb0a6-164">Next steps</span></span>
[<span data-ttu-id="cb0a6-165">Hello Azure 도구 가져오기</span><span class="sxs-lookup"><span data-stu-id="cb0a6-165">Get hello Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

