---
title: "Intel Edison (노드) tooAzure IoT-1과 연결: 앱 배포 | Microsoft Docs"
description: "GitHub에서 hello C 샘플 응용 프로그램을 복제 하 고이 응용 프로그램 tooyour Intel Edison 보드 gulp toodeploy를 실행 합니다. 이 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 프로젝트, arduino led 깜박임, arduino led 깜박임 코드, arduino 깜박임 프로그램, arduino 깜박임 예제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="e3943-105">만들기 및 hello 깜박임 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e3943-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e3943-106">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="e3943-106">What you will do</span></span>
<span data-ttu-id="e3943-107">GitHub에서 hello C 샘플 응용 프로그램을 복제 하 고 hello gulp 도구 toodeploy hello 샘플 응용 프로그램 tooIntel Edison를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="e3943-108">hello 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="e3943-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e3943-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="e3943-110">What you will learn</span></span>
* <span data-ttu-id="e3943-111">어떻게 toodeploy 및 실행된 hello 샘플 Edison에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e3943-112">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e3943-112">What you need</span></span>
<span data-ttu-id="e3943-113">성공적으로 완료 해야 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="e3943-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="e3943-114">[장치 구성][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="e3943-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="e3943-115">[Hello 도구 가져오기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="e3943-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="e3943-116">열기 hello 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e3943-116">Open hello sample application</span></span>
<span data-ttu-id="e3943-117">tooopen hello 샘플 응용 프로그램, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="e3943-118">Hello 다음 명령을 실행 하 여 GitHub에서 hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="e3943-119">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Repo 구조][repo-structure]

<span data-ttu-id="e3943-121">hello에 hello 파일 `app` 하위 폴더는 hello 코드 toocontrol hello LED가 있는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="e3943-122">응용 프로그램 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="e3943-122">Install application dependencies</span></span>
<span data-ttu-id="e3943-123">Hello 라이브러리 및 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램에 필요한 다른 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="e3943-124">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="e3943-124">Configure hello device connection</span></span>
<span data-ttu-id="e3943-125">tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="e3943-126">Hello 다음 명령을 실행 하 여 hello 장치 구성 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="e3943-127">hello 구성 파일 `config-edison.json` toolog tooEdison에서 사용 하 여 hello 사용자 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="e3943-128">tooavoid hello 누수 hello 하위 폴더에 사용자 자격 증명의 hello 구성 파일이 생성 됩니다 `.iot-hub-getting-started` hello 컴퓨터에서 홈 폴더의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="e3943-129">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 장치 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="e3943-130">Hello 자리 표시자 대체 `[device hostname or IP address]` 및 `[device password]` hello IP 주소 및 암호를 이전 단원에서 가격 인하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="e3943-132">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-132">Congratulations!</span></span> <span data-ttu-id="e3943-133">Hello 첫 번째 Edison에 대 한 샘플 응용 프로그램을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="e3943-134">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e3943-134">Deploy and run hello sample application</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="e3943-135">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e3943-135">Deploy and run hello sample app</span></span>
<span data-ttu-id="e3943-136">배포 하 고 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-136">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="e3943-137">Hello 앱 작동 확인</span><span class="sxs-lookup"><span data-stu-id="e3943-137">Verify hello app works</span></span>
<span data-ttu-id="e3943-138">hello 샘플 응용 프로그램 hello led가 깜박입니다 20 배에 대 한 후 자동으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-138">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="e3943-139">Hello led가 깜박입니다.이 표시 되지 않으면 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-139">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED 깜박임][led-blinking]

## <a name="summary"></a><span data-ttu-id="e3943-141">요약</span><span class="sxs-lookup"><span data-stu-id="e3943-141">Summary</span></span>
<span data-ttu-id="e3943-142">Edison와 필요한 hello 도구 toowork를 설치 하 고 샘플 응용 프로그램 tooEdison tooblink hello LED를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-142">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="e3943-143">있습니다 수 이제 만들고, 배포, 및 Edison tooAzure toosend IoT 허브를 연결 하는 또 다른 샘플 응용 프로그램을 실행 하 고 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3943-143">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3943-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3943-144">Next steps</span></span>
<span data-ttu-id="e3943-145">[Hello Azure 도구 가져오기][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="e3943-145">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
