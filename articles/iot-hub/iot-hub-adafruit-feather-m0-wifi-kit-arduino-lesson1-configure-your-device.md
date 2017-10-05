---
title: "Azure IoT에 Arduino(C) 연결 - 단원 1: 장치 구성 | Microsoft Docs"
description: "처음 사용 시 Adafruit Feather M0 WiFi를 구성합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 설정, pc에 arduino 연결, arduino 설치, arduino 보드"
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="785b7-104">장치 구성</span><span class="sxs-lookup"><span data-stu-id="785b7-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="785b7-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="785b7-105">What you will do</span></span>
<span data-ttu-id="785b7-106">보드를 조립하여 전원을 켜서 Adafruit Feather M0 WiFi Arduino 보드를 처음 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="785b7-107">문제가 있으면 [문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="785b7-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="785b7-108">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="785b7-108">What you need</span></span>
<span data-ttu-id="785b7-109">이 작업을 완료하려면 Adafruit Feather M0 WiFi 시작 키트에서 다음 부품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="785b7-110">Adafruit Feather M0 WiFi 보드</span><span class="sxs-lookup"><span data-stu-id="785b7-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="785b7-111">Micro B-A형 USB 케이블</span><span class="sxs-lookup"><span data-stu-id="785b7-111">A Micro B to Type A USB cable</span></span>

![키트][kit]

<span data-ttu-id="785b7-113">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-113">You also need:</span></span>

* <span data-ttu-id="785b7-114">Windows, Mac 또는 Linux를 실행하는 컴퓨터 </span><span class="sxs-lookup"><span data-stu-id="785b7-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="785b7-115">무선으로 Arduino 보드 연결</span><span class="sxs-lookup"><span data-stu-id="785b7-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="785b7-116">구성 도구를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="785b7-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="785b7-117">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="785b7-117">What you will learn</span></span>
<span data-ttu-id="785b7-118">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-118">In this article, you will learn:</span></span>

* <span data-ttu-id="785b7-119">다음 단원을 위해 Arduino 보드를 조립하고 전원을 켜는 방법</span><span class="sxs-lookup"><span data-stu-id="785b7-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="785b7-120">Ubuntu에서 직렬 포트 권한을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="785b7-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="785b7-121">컴퓨터에 Arduino 보드 연결</span><span class="sxs-lookup"><span data-stu-id="785b7-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="785b7-122">마이크로 USB 케이블을 위쪽 마이크로 USB 포트에 꽂습니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![위쪽 마이크로 USB 포트][top-micro-usb-port]

2. <span data-ttu-id="785b7-124">USB 케이블의 다른 쪽을 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-124">Plug the other end of USB cable into your computer.</span></span>

   ![컴퓨터 USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="785b7-126">Ubuntu에서 직렬 포트 권한 추가</span><span class="sxs-lookup"><span data-stu-id="785b7-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="785b7-127">Windows 또는 macOS를 사용하는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="785b7-128">Ubuntu의 경우 일반적인 Linux 사용자가 Arduino 보드의 USB 포트에서 작동할 수 있는 권한을 가지고 있는지 확인하려면 다음 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="785b7-129">이제 터미널에서 일반 사용자로 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="785b7-130">다음과 비슷한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="785b7-131">"0" 대신 다른 숫자가 될 수도 있고 여러 항목이 반환될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="785b7-132">첫 번째 경우 필요한 데이터는 `uucp`이고 두 번째의 경우 `dialout`인데 이는 파일의 그룹 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="785b7-133">그룹에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="785b7-134">여기서 `group-name`은 첫 번째 단계에 있는 데이터이고 `username`은 Linux 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="785b7-135">이 변경 내용을 적용하고 설치를 완료하려면 로그아웃한 후 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="785b7-136">요약</span><span class="sxs-lookup"><span data-stu-id="785b7-136">Summary</span></span>
<span data-ttu-id="785b7-137">이 문서에서는 Arduino 보드를 구성하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="785b7-138">다음 작업은 Arduino 보드에서 샘플 응용 프로그램 실행을 위한 준비로 필요한 도구 및 소프트웨어를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="785b7-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![하드웨어는 준비되었습니다.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="785b7-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="785b7-140">Next steps</span></span>
<span data-ttu-id="785b7-141">[도구 얻기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="785b7-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md