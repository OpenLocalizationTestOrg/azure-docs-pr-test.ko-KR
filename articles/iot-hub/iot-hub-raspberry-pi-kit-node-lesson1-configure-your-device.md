---
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 1: 장치 구성 | Microsoft Docs"
description: Configure Raspberry Pi 3 for first-time use and install the Raspbian OS, a free operating system that is optimized for the Raspberry Pi hardware.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Raspbian 설치, Raspbian 다운로드, Raspbian 설치 방법, Raspbian 설정, Raspberry Pi 설치 Raspbian, Raspberry Pi 설치 OS, Raspberry Pi SD 카드 설치, Raspberry Pi 연결, Raspberry Pi에 연결, Raspberry Pi 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b848c48157a2310f0eb1d6398f8b9aaa4395d47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="5ffd3-104">장치 구성</span><span class="sxs-lookup"><span data-stu-id="5ffd3-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5ffd3-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="5ffd3-105">What you will do</span></span>
<span data-ttu-id="5ffd3-106">최초 사용을 위해 Pi를 구성하고 Raspbian 운영 체제를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="5ffd3-107">Raspbian은 Raspberry Pi 하드웨어에 최적화된 무료 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="5ffd3-108">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-108">If you have any problems, you can seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5ffd3-109">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="5ffd3-109">What you will learn</span></span>
<span data-ttu-id="5ffd3-110">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-110">In this article, you will learn:</span></span>

* <span data-ttu-id="5ffd3-111">Pi에 Raspbian을 설치하는 방법.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="5ffd3-112">USB 케이블을 사용하여 Pi에 전원을 공급하는 방법.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="5ffd3-113">이더넷 케이블이나 무선 네트워크를 사용하여 Pi를 네트워크에 연결하는 방법.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="5ffd3-114">LED를 실험용 회로판에 추가하고 Pi에 연결하는 방법.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="5ffd3-115">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="5ffd3-115">What you will need</span></span>
<span data-ttu-id="5ffd3-116">이 작업을 완료하려면 Raspberry Pi 3 시작 키트에서 다음 부품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="5ffd3-117">Raspberry Pi 3 보드</span><span class="sxs-lookup"><span data-stu-id="5ffd3-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="5ffd3-118">16GB microSD 카드</span><span class="sxs-lookup"><span data-stu-id="5ffd3-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="5ffd3-119">6피트 마이크로 USB 케이블과 5볼트 2암페어 전원 공급 장치</span><span class="sxs-lookup"><span data-stu-id="5ffd3-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="5ffd3-120">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="5ffd3-120">The breadboard</span></span>
* <span data-ttu-id="5ffd3-121">커넥터 와이어</span><span class="sxs-lookup"><span data-stu-id="5ffd3-121">Connector wires</span></span>
* <span data-ttu-id="5ffd3-122">560옴 저항기</span><span class="sxs-lookup"><span data-stu-id="5ffd3-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="5ffd3-123">확산형 10mm LED</span><span class="sxs-lookup"><span data-stu-id="5ffd3-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="5ffd3-124">이더넷 케이블 </span><span class="sxs-lookup"><span data-stu-id="5ffd3-124">The Ethernet cable</span></span>

![시작 키트의 항목](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="5ffd3-126">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-126">You also need:</span></span>

* <span data-ttu-id="5ffd3-127">Pi를 연결할 유선 또는 무선 연결.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="5ffd3-128">운영 체제 이미지를 microSD 카드에 굽기 위한 USB-SD 어댑터 또는 miniSD 카드.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-128">A USB-SD adapter or miniSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="5ffd3-129">Windows, Mac 또는 Linux를 실행하는 컴퓨터 </span><span class="sxs-lookup"><span data-stu-id="5ffd3-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="5ffd3-130">컴퓨터는 microSD 카드에 Raspbian을 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="5ffd3-131">필요한 도구 및 소프트웨어를 다운로드하기 위한 인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="5ffd3-132">microSD 카드에 Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="5ffd3-132">Install Raspbian on the microSD card</span></span>
<span data-ttu-id="5ffd3-133">Raspbian 이미지를 설치를 위해 microSD 카드를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="5ffd3-134">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="5ffd3-135">Raspbian Jessie with Pixel의 zip 파일을 [다운로드](https://www.raspberrypi.org/downloads/raspbian/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="5ffd3-136">컴퓨터의 폴더에 Raspbian 이미지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="5ffd3-137">microSD 카드에 Raspbian을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="5ffd3-138">Etcher SD 카드 버너 유틸리티를 [다운로드](https://www.etcher.io)하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="5ffd3-139">Etcher를 실행하고 1단계에서 압축을 푼 Raspbian 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="5ffd3-140">microSD 카드 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="5ffd3-141">Etcher가 이미 올바른 드라이브를 선택했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="5ffd3-142">**Flash**를 클릭하여 microSD 카드에 Raspbian을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="5ffd3-143">설치가 완료되면 컴퓨터에서 microSD 카드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="5ffd3-144">완료되면 Etcher가 microSD 카드를 자동으로 배출하거나 탑재를 해제하므로 microSD 카드를 바로 제거하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-144">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="5ffd3-145">Pi에 microSD 카드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-145">Insert the microSD card into Pi.</span></span>

![SD 카드 삽입](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="5ffd3-147">Pi 켜기</span><span class="sxs-lookup"><span data-stu-id="5ffd3-147">Turn on Pi</span></span>
<span data-ttu-id="5ffd3-148">마이크로 USB 케이블 및 전원 공급 장치를 사용하여 Pi를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![켜기](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="5ffd3-150">Raspberry가 정상 작동하는 데 충분한 전원이 공급되도록 2A 이상인 키트의 전원 공급 장치를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="5ffd3-151">SSH 사용</span><span class="sxs-lookup"><span data-stu-id="5ffd3-151">Enable SSH</span></span>
<span data-ttu-id="5ffd3-152">2016년 11월 릴리스를 기준으로 Raspbian은 기본적으로 SSH 서버를 비활성화했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="5ffd3-153">수동으로 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-153">You need to enable it manually.</span></span> <span data-ttu-id="5ffd3-154">[공식 지침](https://www.raspberrypi.org/documentation/remote-access/ssh/)을 참조하거나 모니터를 연결하고 **기본 설정 -> Raspberry Pi 구성**으로 이동하여 SSH를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="5ffd3-155">Raspberry Pi 3을 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="5ffd3-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="5ffd3-156">Pi를 유선 네트워크 또는 무선 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="5ffd3-157">Pi가 컴퓨터와 같은 네트워크에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="5ffd3-158">예를 들어 Pi를 컴퓨터가 연결된 스위치와 같은 스위치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="5ffd3-159">유선 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="5ffd3-159">Connect to a wired network</span></span>
<span data-ttu-id="5ffd3-160">이더넷 케이블을 사용하여 Pi를 유선 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="5ffd3-161">연결이 수립되면 Pi의 LED 두 개가 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![이더넷 케이블을 사용하여 연결](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="5ffd3-163">무선 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="5ffd3-163">Connect to a wireless network</span></span>
<span data-ttu-id="5ffd3-164">Raspberry Pi Foundation의 [지침](https://www.raspberrypi.org/learning/software-guide/wifi/)에 따라 Pi를 무선 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="5ffd3-165">이 지침에 따르면 먼저 모니터와 키보드를 Pi에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="5ffd3-166">LED를 Pi에 연결</span><span class="sxs-lookup"><span data-stu-id="5ffd3-166">Connect the LED to Pi</span></span>
<span data-ttu-id="5ffd3-167">이 작업을 완료하려면 [실험용 회로판](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), 커넥터 와이어, LED 및 저항기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="5ffd3-168">이러한 항목을 Pi의 [범용 입출력](https://www.raspberrypi.org/documentation/usage/gpio/)(GPIO) 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![실험용 회로판, LED 및 저항기](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="5ffd3-170">LED의 더 짧은 다리를 **GPIO GND(Pin 6)**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="5ffd3-171">저항기의 한 쪽 다리에 더 긴 LED 다리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="5ffd3-172">LED의 다른 다리를 **GPIO 4(Pin 7)**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="5ffd3-173">LED 극성이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="5ffd3-174">이 극성 설정은 일반적으로 활성(낮음)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-174">This polarity setting is commonly known as Active Low.</span></span>

![핀아웃](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="5ffd3-176">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-176">Congratulations!</span></span> <span data-ttu-id="5ffd3-177">Pi 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="5ffd3-178">요약</span><span class="sxs-lookup"><span data-stu-id="5ffd3-178">Summary</span></span>
<span data-ttu-id="5ffd3-179">이 문서에서는 Raspbian을 설치하고, Pi를 네트워크에 연결하고, LED를 Pi에 연결하여 Pi를 구성하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="5ffd3-180">아직 LED에는 불이 들어오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="5ffd3-181">다음 작업은 Pi에서 샘플 응용 프로그램 실행을 위한 준비로 필요한 도구 및 소프트웨어를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd3-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![하드웨어는 준비되었습니다.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="5ffd3-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ffd3-183">Next steps</span></span>
[<span data-ttu-id="5ffd3-184">도구 얻기</span><span class="sxs-lookup"><span data-stu-id="5ffd3-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

