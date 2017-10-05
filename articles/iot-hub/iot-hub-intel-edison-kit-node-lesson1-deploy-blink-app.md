---
title: "Azure IoT에 Intel Edison(노드) 연결 - 단원 1: 앱 배포 | Microsoft Docs"
description: "GitHub에서 샘플 C 응용 프로그램을 복제하고 gulp를 실행하여 이 응용 프로그램을 Intel Edison 보드에 배포합니다. 이 샘플 응용 프로그램은 보드에 연결된 LED를 2초마다 깜박이게 합니다."
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
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="30d77-105">깜박임 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="30d77-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="30d77-106">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="30d77-106">What you will do</span></span>
<span data-ttu-id="30d77-107">GitHub에서 샘플 C 응용 프로그램을 복제하고 gulp 도구를 사용하여 Intel Edison에 샘플 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="30d77-108">샘플 응용 프로그램은 보드에 연결된 LED를 2초마다 깜박이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="30d77-109">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="30d77-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="30d77-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="30d77-110">What you will learn</span></span>
* <span data-ttu-id="30d77-111">Edison에서 샘플 응용 프로그램을 배포하고 실행하는 방법.</span><span class="sxs-lookup"><span data-stu-id="30d77-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="30d77-112">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="30d77-112">What you need</span></span>
<span data-ttu-id="30d77-113">다음 작업을 성공적으로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="30d77-114">[장치 구성][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="30d77-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="30d77-115">[도구 얻기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="30d77-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="30d77-116">샘플 응용 프로그램 열기</span><span class="sxs-lookup"><span data-stu-id="30d77-116">Open the sample application</span></span>
<span data-ttu-id="30d77-117">샘플 응용 프로그램을 열려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="30d77-118">다음 명령을 실행하여 GitHub에서 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="30d77-119">다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Repo 구조][repo-structure]

<span data-ttu-id="30d77-121">`app` 하위 폴더의 파일은 LED 제어 코드가 있는 핵심 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="30d77-122">응용 프로그램 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="30d77-122">Install application dependencies</span></span>
<span data-ttu-id="30d77-123">다음 명령을 실행하여 샘플 응용 프로그램에 필요한 라이브러리 및 기타 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="30d77-124">장치 연결 구성</span><span class="sxs-lookup"><span data-stu-id="30d77-124">Configure the device connection</span></span>
<span data-ttu-id="30d77-125">장치 연결을 구성하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="30d77-126">다음 명령을 실행하여 장치 구성 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="30d77-127">구성 파일 `config-edison.json`에는 Edison에 로그인하는 데 사용하는 사용자 자격 증명이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="30d77-128">사용자 자격 증명의 유출을 방지하기 위해 구성 파일은 컴퓨터 홈 폴더의 `.iot-hub-getting-started` 하위 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="30d77-129">다음 명령을 실행하여 Visual Studio Code에서 장치 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="30d77-130">자리 표시자 `[device hostname or IP address]` 및 `[device password]`를 이전 단원에서 적어 둔 IP 주소 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="30d77-132">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-132">Congratulations!</span></span> <span data-ttu-id="30d77-133">Edison의 첫 번째 샘플 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="30d77-134">샘플 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="30d77-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="30d77-135">샘플 앱 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="30d77-135">Deploy and run the sample app</span></span>
<span data-ttu-id="30d77-136">다음 명령을 실행하여 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="30d77-137">앱 작동 확인</span><span class="sxs-lookup"><span data-stu-id="30d77-137">Verify the app works</span></span>
<span data-ttu-id="30d77-138">샘플 응용 프로그램은 LED를 20번 깜박인 후 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="30d77-139">LED가 깜박이지 않으면 [문제 해결 가이드][troubleshooting]에서 일반적인 문제에 대한 솔루션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d77-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED 깜박임][led-blinking]

## <a name="summary"></a><span data-ttu-id="30d77-141">요약</span><span class="sxs-lookup"><span data-stu-id="30d77-141">Summary</span></span>
<span data-ttu-id="30d77-142">Edison 작동에 필요한 도구를 설치했으며 LED를 깜박이게 하는 샘플 응용 프로그램을 Edison에 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="30d77-143">이제 메시지 송수신을 위해 Azure IoT Hub에 Edison을 연결하는 다른 샘플 응용 프로그램을 만들고, 배포하고, 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d77-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30d77-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30d77-144">Next steps</span></span>
<span data-ttu-id="30d77-145">[Azure 도구 얻기][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="30d77-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
