---
title: "Connect Raspberry Pi (C) tooAzure IoT-1 단원: 장치 구성 | Microsoft Docs"
description: "처음 사용 하기 위해 라스베리 Pi 3 구성 하 고 hello Raspbian OS, hello 라스베리 Pi 하드웨어에 최적화 된 무료 운영 체제를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspbian 다운로드, 설치 raspbian은 tooinstall raspbian raspbian 설치 라즈베리 pi 설치 raspbian 라즈베리 pi 설치 라즈베리 os pi sd 카드 라즈베리 설치 pi 연결 연결 tooraspberry pi 라즈베리 pi 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="20d16-104">장치 구성</span><span class="sxs-lookup"><span data-stu-id="20d16-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="20d16-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="20d16-105">What you will do</span></span>
<span data-ttu-id="20d16-106">Pi를 처음 사용 하기 위해 구성 하 고 hello Raspbian 운영 체제를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="20d16-107">Raspbian는 가능한 운영 체제 hello 라스베리 Pi 하드웨어에 대해 최적화 된입니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="20d16-108">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="20d16-109">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="20d16-109">What you will learn</span></span>
<span data-ttu-id="20d16-110">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-110">In this article, you will learn:</span></span>

* <span data-ttu-id="20d16-111">어떻게 tooinstall 원주율 Raspbian 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="20d16-112">어떻게 USB 케이블을 사용 하 여 toopower Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="20d16-113">어떻게 tooconnect Pi toohello 이더넷 케이블 또는 무선 네트워크를 사용 하 여 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="20d16-114">Tooadd LED toohello breadboard 어떻게 tooPi 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="20d16-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="20d16-115">What you need</span></span>
<span data-ttu-id="20d16-116">toocomplete 라스베리 Pi 3 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="20d16-117">hello 라스베리 Pi 3 보드</span><span class="sxs-lookup"><span data-stu-id="20d16-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="20d16-118">hello 16GB microSD 카드</span><span class="sxs-lookup"><span data-stu-id="20d16-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="20d16-119">hello 6 피트 마이크로 USB 케이블 hello 5 v 2 amp 전원 공급 장치</span><span class="sxs-lookup"><span data-stu-id="20d16-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="20d16-120">hello breadboard</span><span class="sxs-lookup"><span data-stu-id="20d16-120">hello breadboard</span></span>
* <span data-ttu-id="20d16-121">커넥터 와이어</span><span class="sxs-lookup"><span data-stu-id="20d16-121">Connector wires</span></span>
* <span data-ttu-id="20d16-122">560옴 저항기</span><span class="sxs-lookup"><span data-stu-id="20d16-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="20d16-123">확산형 10mm LED</span><span class="sxs-lookup"><span data-stu-id="20d16-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="20d16-124">hello 이더넷 케이블</span><span class="sxs-lookup"><span data-stu-id="20d16-124">hello Ethernet cable</span></span>

![시작 키트의 항목](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="20d16-126">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-126">You also need:</span></span>

* <span data-ttu-id="20d16-127">에 Pi tooconnect에 대 한 유선 또는 무선 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="20d16-128">USB SD 어댑터 또는 미니 SD 카드 tooburn hello OS에 이미지를 hello microSD 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-128">A USB-SD adapter or mini-SD card tooburn hello OS image onto hello microSD card.</span></span>
* <span data-ttu-id="20d16-129">Windows, Mac 또는 Linux를 실행하는 컴퓨터 </span><span class="sxs-lookup"><span data-stu-id="20d16-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="20d16-130">hello 컴퓨터가 hello microSD 카드에 사용 되는 tooinstall Raspbian 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="20d16-131">인터넷 연결 toodownload 필요한 도구와 소프트웨어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="20d16-132">Raspbian hello MicroSD 카드에 설치</span><span class="sxs-lookup"><span data-stu-id="20d16-132">Install Raspbian on hello MicroSD card</span></span>
<span data-ttu-id="20d16-133">Hello microSD 카드 hello Raspbian 이미지의 설치를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="20d16-134">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="20d16-135">[다운로드](https://www.raspberrypi.org/downloads/raspbian/) hello.zip 파일에 대 한 픽셀을 Raspbian 제시 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="20d16-136">Hello Raspbian 이미지 tooa 컴퓨터의 폴더에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="20d16-137">Raspbian toohello microSD 카드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="20d16-138">[다운로드](https://www.etcher.io) hello Etcher SD 카드 버너 유틸리티 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="20d16-139">Etcher를 실행 하 고 1 단계에서 압축을 푼 hello Raspbian 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="20d16-140">Hello microSD 카드 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="20d16-141">Etcher 선택 했을 수 이미 hello 올바른 드라이브 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="20d16-142">클릭 **플래시** tooinstall Raspbian toohello microSD 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="20d16-143">설치가 완료 되 면 hello microSD 카드를 컴퓨터에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="20d16-144">되므로 안전 tooremove hello microSD 카드 직접 Etcher를 꺼냅니다. 자동으로 또는 완료 되 면 hello microSD 카드 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-144">It is safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="20d16-145">프로그램 Pi에 hello microSD 카드를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-145">Insert hello microSD card into your Pi.</span></span>

![Hello SD 카드를 삽입 합니다.](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="20d16-147">Pi 켜기</span><span class="sxs-lookup"><span data-stu-id="20d16-147">Turn on Pi</span></span>
<span data-ttu-id="20d16-148">Pi hello 마이크로 USB 케이블 및 hello 전원 공급 장치를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![켜기](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="20d16-150">최소 hello 키트의 중요 한 toouse hello 전원 공급 장치는 프로그램 라스베리에 충분 한 전력 toowork 올바르게 있는지 2A toomake 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="20d16-151">SSH 사용</span><span class="sxs-lookup"><span data-stu-id="20d16-151">Enable SSH</span></span>
<span data-ttu-id="20d16-152">Hello 2016 년 11 월 릴리스를 기준으로 Raspbian 기본적으로 사용 하지 않도록 설정 하는 hello SSH 서버를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="20d16-153">Tooenable 필요한 것 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-153">You need tooenable it manually.</span></span> <span data-ttu-id="20d16-154">Toohello 참조할 수 있습니다 [공식 지침](https://www.raspberrypi.org/documentation/remote-access/ssh/) 하거나 모니터를 연결 하 고 이동 너무**기본 설정-> 라스베리 Pi 구성** tooenable SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="20d16-155">라스베리 Pi 3 toohello 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="20d16-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="20d16-156">Pi tooa 유선 네트워크 또는 tooa 무선 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="20d16-157">Pi 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="20d16-158">예를 들어 컴퓨터에 연결 되어 있는지를 전환 동일한는 Pi toohello를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="20d16-159">Tooa 유선 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="20d16-159">Connect tooa wired network</span></span>
<span data-ttu-id="20d16-160">Hello 이더넷 케이블 tooconnect Pi tooyour 유선 네트워크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="20d16-161">hello Pi에서 두 개의 Led 설정 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![이더넷 케이블을 사용하여 연결](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="20d16-163">Tooa 무선 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="20d16-163">Connect tooa wireless network</span></span>
<span data-ttu-id="20d16-164">Hello에 따라 [지침](https://www.raspberrypi.org/learning/software-guide/wifi/) hello 라스베리 Pi Foundation tooconnect Pi tooyour 무선 네트워크에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="20d16-165">이러한 지침을 사용 해야 하는 모니터 및 키보드 tooPi toofirst 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="20d16-166">Hello LED tooPi 연결</span><span class="sxs-lookup"><span data-stu-id="20d16-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="20d16-167">toocomplete이 작업을 사용 하 여 hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)및 LED, hello 저항기 hello 커넥터 와이어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="20d16-168">Toohello 연결 [범용 입/출력](https://www.raspberrypi.org/documentation/usage/gpio/) Pi의 포트 (GPIO).</span><span class="sxs-lookup"><span data-stu-id="20d16-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![실험용 회로판, LED 및 저항기](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="20d16-170">Hello 짧은 다리 hello LED의 너무 연결**GPIO GND (Pin 6)**합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="20d16-171">Hello hello 저항기의 LED tooone 레그의 긴 레그 hello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="20d16-172">연결의 hello 저항기 다른 레그 너무 hello**GPIO 4 (Pin 7)**합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="20d16-173">Note는 hello LED 극성이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="20d16-174">이 극성 설정은 일반적으로 활성(낮음)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-174">This polarity setting is commonly known as Active Low.</span></span>

![핀아웃](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="20d16-176">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-176">Congratulations!</span></span> <span data-ttu-id="20d16-177">Pi 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="20d16-178">요약</span><span class="sxs-lookup"><span data-stu-id="20d16-178">Summary</span></span>
<span data-ttu-id="20d16-179">이 문서에서 배운 Raspbian, Pi tooa 네트워크 연결을 설치 하 고 연결 하는 LED tooPi tooconfigure Pi 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="20d16-180">Note 해당 hello LED가 켜 아직 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20d16-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="20d16-181">hello 다음 작업은 tooinstall hello 필요한 도구 및 Pi에서 샘플 응용 프로그램을 실행 하는 준비 과정에서 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="20d16-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![하드웨어는 준비되었습니다.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="20d16-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20d16-183">Next steps</span></span>
[<span data-ttu-id="20d16-184">Hello 도구 가져오기</span><span class="sxs-lookup"><span data-stu-id="20d16-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

