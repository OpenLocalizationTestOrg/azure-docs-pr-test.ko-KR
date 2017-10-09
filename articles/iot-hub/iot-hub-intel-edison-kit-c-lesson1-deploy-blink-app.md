---
title: "Connect Intel Edison (C) tooAzure IoT-1 단원: 응용 프로그램 배포 | Microsoft Docs"
description: "GitHub에서 hello C 샘플 응용 프로그램을 복제 하 고이 응용 프로그램 tooyour Intel Edison 보드 gulp toodeploy를 실행 합니다. 이 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 프로젝트, arduino led 깜박임, arduino led 깜박임 코드, arduino 깜박임 프로그램, arduino 깜박임 예제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="b1b0e-105">만들기 및 hello 깜박임 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="b1b0e-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b1b0e-106">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="b1b0e-106">What you will do</span></span>
<span data-ttu-id="b1b0e-107">GitHub에서 hello C 샘플 응용 프로그램을 복제 하 고 hello gulp 도구 toodeploy hello 샘플 응용 프로그램 tooIntel Edison를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="b1b0e-108">hello 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="b1b0e-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b1b0e-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="b1b0e-110">What you will learn</span></span>
* <span data-ttu-id="b1b0e-111">어떻게 toodeploy 및 실행된 hello 샘플 Edison에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b1b0e-112">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="b1b0e-112">What you need</span></span>
<span data-ttu-id="b1b0e-113">성공적으로 완료 해야 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="b1b0e-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="b1b0e-114">[장치 구성][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="b1b0e-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="b1b0e-115">[Hello 도구 가져오기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="b1b0e-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="b1b0e-116">열기 hello 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b1b0e-116">Open hello sample application</span></span>
<span data-ttu-id="b1b0e-117">tooopen hello 샘플 응용 프로그램, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="b1b0e-118">Hello 다음 명령을 실행 하 여 GitHub에서 hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="b1b0e-119">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Repo 구조][repo-structure]

<span data-ttu-id="b1b0e-121">hello에 hello 파일 `app` 하위 폴더는 hello 코드 toocontrol hello LED가 있는 hello 키 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="b1b0e-122">응용 프로그램 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="b1b0e-122">Install application dependencies</span></span>
<span data-ttu-id="b1b0e-123">Hello 라이브러리 및 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램에 필요한 다른 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="b1b0e-124">Hello 장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="b1b0e-124">Configure hello device connection</span></span>
<span data-ttu-id="b1b0e-125">tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="b1b0e-126">Hello 다음 명령을 실행 하 여 hello 장치 구성 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="b1b0e-127">hello 구성 파일 `config-edison.json` toolog tooEdison에서 사용 하 여 hello 사용자 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="b1b0e-128">tooavoid hello 누수 hello 하위 폴더에 사용자 자격 증명의 hello 구성 파일이 생성 됩니다 `.iot-hub-getting-started` hello 컴퓨터에서 홈 폴더의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="b1b0e-129">Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 장치 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="b1b0e-130">Hello 자리 표시자 대체 `[device hostname or IP address]` 및 `[device password]` hello IP 주소 및 암호를 이전 단원에서 가격 인하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="b1b0e-132">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-132">Congratulations!</span></span> <span data-ttu-id="b1b0e-133">Hello 첫 번째 Edison에 대 한 샘플 응용 프로그램을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="b1b0e-134">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b1b0e-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="b1b0e-135">Edison에 hello Azure IoT 허브 SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="b1b0e-136">Hello 다음 명령을 실행 하 여 Edison에 hello Azure IoT 허브 SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="b1b0e-137">이 작업은 네트워크 연결에 따라 시간이 오래 toocomplete, 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="b1b0e-138">이것 필요 toobe 실행 한 번만 하나의 Edison에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="b1b0e-139">배포 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b1b0e-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="b1b0e-140">배포 하 고 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="b1b0e-141">Hello 앱 작동 확인</span><span class="sxs-lookup"><span data-stu-id="b1b0e-141">Verify hello app works</span></span>
<span data-ttu-id="b1b0e-142">hello 샘플 응용 프로그램 hello led가 깜박입니다 20 배에 대 한 후 자동으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="b1b0e-143">Hello led가 깜박입니다.이 표시 되지 않으면 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED 깜박임][led-blinking]

## <a name="summary"></a><span data-ttu-id="b1b0e-145">요약</span><span class="sxs-lookup"><span data-stu-id="b1b0e-145">Summary</span></span>
<span data-ttu-id="b1b0e-146">Edison와 필요한 hello 도구 toowork를 설치 하 고 샘플 응용 프로그램 tooEdison tooblink hello LED를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="b1b0e-147">있습니다 수 이제 만들고, 배포, 및 Edison tooAzure toosend IoT 허브를 연결 하는 또 다른 샘플 응용 프로그램을 실행 하 고 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b0e-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b0e-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1b0e-148">Next steps</span></span>
<span data-ttu-id="b1b0e-149">[Hello Azure 도구 가져오기][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="b1b0e-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
