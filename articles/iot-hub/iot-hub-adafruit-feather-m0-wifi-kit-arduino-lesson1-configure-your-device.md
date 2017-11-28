---
title: "Connect Arduino (C) tooAzure IoT-1 단원: 장치 구성 | Microsoft Docs"
description: "처음 사용 시 Adafruit Feather M0 WiFi를 구성합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "설정, arduino arduino toopc, 설치 arduino, arduino 보드 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="a6f9d-104">장치 구성</span><span class="sxs-lookup"><span data-stu-id="a6f9d-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a6f9d-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="a6f9d-105">What you will do</span></span>
<span data-ttu-id="a6f9d-106">처음 사용 하기 위해 Adafruit 페더 M0 WiFi Arduino 보드를 구동 하는 hello 보드 어셈블하는 방법으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="a6f9d-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6f9d-108">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="a6f9d-108">What you need</span></span>
<span data-ttu-id="a6f9d-109">toocomplete hello Adafruit 페더 M0 WiFi 시작 키트에 대 한 부분을 다음 해야이 작업의 경우:</span><span class="sxs-lookup"><span data-stu-id="a6f9d-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="a6f9d-110">hello Adafruit 페더 M0 WiFi 보드</span><span class="sxs-lookup"><span data-stu-id="a6f9d-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="a6f9d-111">마이크로 B tooType A USB 케이블</span><span class="sxs-lookup"><span data-stu-id="a6f9d-111">A Micro B tooType A USB cable</span></span>

![키트][kit]

<span data-ttu-id="a6f9d-113">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-113">You also need:</span></span>

* <span data-ttu-id="a6f9d-114">Windows, Mac 또는 Linux를 실행하는 컴퓨터 </span><span class="sxs-lookup"><span data-stu-id="a6f9d-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="a6f9d-115">Arduino 보드 tooconnect 프로그램에 대 한 무선 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="a6f9d-116">인터넷 연결 toodownload 구성 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a6f9d-117">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="a6f9d-117">What you will learn</span></span>
<span data-ttu-id="a6f9d-118">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-118">In this article, you will learn:</span></span>

* <span data-ttu-id="a6f9d-119">어떻게 tooassemble Arduino 보드 및 전원 것 다음 hello에 대해 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="a6f9d-120">어떻게 ubuntu tooadd 직렬 포트 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="a6f9d-121">Arduino 보드 tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="a6f9d-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="a6f9d-122">Hello 상위 마이크로 USB 포트에 hello 마이크로 USB 케이블을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![위쪽 마이크로 USB 포트][top-micro-usb-port]

2. <span data-ttu-id="a6f9d-124">플러그를 컴퓨터에 USB 케이블의 다른 쪽 끝을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-124">Plug hello other end of USB cable into your computer.</span></span>

   ![컴퓨터 USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="a6f9d-126">Ubuntu에서 직렬 포트 권한 추가</span><span class="sxs-lookup"><span data-stu-id="a6f9d-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="a6f9d-127">Windows 또는 macOS를 사용하는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="a6f9d-128">Ubuntu, hello hello 일반 linux 사용자에 게 Arduino 보드의 hello USB 포트에 사용 권한을 toooperate hello 있는지 단계 toomake 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="a6f9d-129">이제 터미널에서 일반 사용자로 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="a6f9d-130">다음과 비슷한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="a6f9d-131">다른 숫자를 "0" hello 없거나 항목이 여러 개 반환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="a6f9d-132">필요한 hello 첫 번째 사례 hello 데이터는 `uucp`, 둘째는 hello에 `dialout`, hello 파일의 hello 그룹 소유자 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="a6f9d-133">사용자 toohello toohello 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="a6f9d-134">여기서 `group-name` 는 hello 첫 번째 단계에서 찾은 hello 데이터 및 `username` 은 linux 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="a6f9d-135">이 변경 tootake 효과 및 전체 hello 설정에 대 한 다시 toolog에 및를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="a6f9d-136">요약</span><span class="sxs-lookup"><span data-stu-id="a6f9d-136">Summary</span></span>
<span data-ttu-id="a6f9d-137">이 문서에서 배운 어떻게 tooconfigure Arduino 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="a6f9d-138">hello 다음 작업은 tooinstall hello 필요한 도구 및 Arduino 보드에는 예제 응용 프로그램을 실행 하기 위한 준비 과정에서 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="a6f9d-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![하드웨어는 준비되었습니다.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="a6f9d-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6f9d-140">Next steps</span></span>
<span data-ttu-id="a6f9d-141">[Hello 도구 가져오기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="a6f9d-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md