---
title: "Raspberry Pi-클라우드(Node.js) - Raspberry Pi를 Azure IoT Hub에 연결 | Microsoft Docs"
description: "Raspberry Pi가 Azure 클라우드에 데이터를 보내도록 Raspberry Pi를 Azure IoT Hub에 연결합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi에서 클라우드로 데이터 전송, raspberry pi-클라우드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="3a007-104">Raspberry Pi를 Azure IoT Hub에 연결(Node.js)</span><span class="sxs-lookup"><span data-stu-id="3a007-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="3a007-105">이 자습서에서는 Raspbian을 실행하는 Raspberry Pi 작업의 기초부터 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="3a007-106">그런 다음 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)를 사용하여 장치를 클라우드에 원활하게 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="3a007-107">Windows 10 IoT Core 샘플이 필요하면 [Windows 개발자 센터](http://www.windowsondevices.com/)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3a007-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="3a007-108">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="3a007-108">Don't have a kit yet?</span></span> <span data-ttu-id="3a007-109">[Raspberry Pi 3 에뮬레이터](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="3a007-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="3a007-110">또는 새 키트를 [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3a007-111">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="3a007-111">What you do</span></span>

* <span data-ttu-id="3a007-112">Raspberry Pi를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="3a007-113">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-113">Create an IoT hub.</span></span>
* <span data-ttu-id="3a007-114">IoT Hub에 Pi용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="3a007-115">Pi에서 샘플 응용 프로그램을 실행하여 IoT Hub로 센서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="3a007-116">앞에서 만든 IoT Hub에 Raspberry Pi를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="3a007-117">그런 다음 Pi에서 샘플 응용 프로그램을 실행하여 BME280에서 온도 및 습도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="3a007-118">마지막으로 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3a007-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="3a007-119">What you learn</span></span>

* <span data-ttu-id="3a007-120">Azure IoT Hub를 만들고 새 장치 연결 문자열을 가져오는 방법.</span><span class="sxs-lookup"><span data-stu-id="3a007-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="3a007-121">Pi를 BME280 센서와 연결하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3a007-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="3a007-122">Pi에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3a007-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="3a007-123">IoT Hub로 센서 데이터를 보내는 방법.</span><span class="sxs-lookup"><span data-stu-id="3a007-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3a007-124">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="3a007-124">What you need</span></span>

![필요한 항목](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="3a007-126">Raspberry Pi 2 또는 Raspberry Pi 3 보드.</span><span class="sxs-lookup"><span data-stu-id="3a007-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="3a007-127">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3a007-127">An active Azure subscription.</span></span> <span data-ttu-id="3a007-128">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3a007-129">Pi에 연결할 모니터, USB 키보드 및 마우스.</span><span class="sxs-lookup"><span data-stu-id="3a007-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="3a007-130">Windows 또는 Linux를 실행하는 Mac 또는 PC.</span><span class="sxs-lookup"><span data-stu-id="3a007-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="3a007-131">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="3a007-131">An Internet connection.</span></span>
* <span data-ttu-id="3a007-132">16GB 이상의 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="3a007-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="3a007-133">운영 체제 이미지를 microSD 카드에 굽기 위한 USB-SD 어댑터 또는 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="3a007-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="3a007-134">6피트 마이크로 USB 케이블과 5볼트 2암페어 전원 공급 장치.</span><span class="sxs-lookup"><span data-stu-id="3a007-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="3a007-135">다음 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-135">The following items are optional:</span></span>

* <span data-ttu-id="3a007-136">조립된 Adafruit BME280 온도, 압력 및 습도 센서.</span><span class="sxs-lookup"><span data-stu-id="3a007-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="3a007-137">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="3a007-137">A breadboard.</span></span>
* <span data-ttu-id="3a007-138">F/M 점퍼 와이어 6개.</span><span class="sxs-lookup"><span data-stu-id="3a007-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="3a007-139">확산형 10mm LED.</span><span class="sxs-lookup"><span data-stu-id="3a007-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="3a007-140">코드 샘플이 시뮬레이션된 센서 데이터를 지원하므로 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="3a007-141">Raspberry Pi 설치</span><span class="sxs-lookup"><span data-stu-id="3a007-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="3a007-142">Pi용 Raspbian 운영 체제 설치</span><span class="sxs-lookup"><span data-stu-id="3a007-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="3a007-143">Raspbian 이미지를 설치를 위해 microSD 카드를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="3a007-144">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="3a007-145">[Raspbian Jessie with Pixel 다운로드](https://www.raspberrypi.org/downloads/raspbian/)(.zip 파일).</span><span class="sxs-lookup"><span data-stu-id="3a007-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="3a007-146">컴퓨터의 폴더에 Raspbian 이미지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="3a007-147">microSD 카드에 Raspbian을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="3a007-148">[Etcher SD 카드 버너 유틸리티를 다운로드하여 설치합니다](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="3a007-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="3a007-149">Etcher를 실행하고 1단계에서 압축을 푼 Raspbian 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="3a007-150">microSD 카드 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-150">Select the microSD card drive.</span></span> <span data-ttu-id="3a007-151">Etcher가 이미 올바른 드라이브를 선택했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="3a007-152">Flash를 클릭하여 microSD 카드에 Raspbian을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="3a007-153">설치가 완료되면 컴퓨터에서 microSD 카드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="3a007-154">완료되면 Etcher가 microSD 카드를 자동으로 배출하거나 탑재를 해제하므로 microSD 카드를 바로 제거하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="3a007-155">Pi에 microSD 카드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="3a007-156">SSH 및 I2C를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3a007-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="3a007-157">사용자 이름으로 `pi`, 암호로 `raspberry`를 사용하여 Pi를 모니터, 키보드, 마우스에 연결하고, Pi를 시작한 다음 Raspbian에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="3a007-158">Raspberry 아이콘 > **기본 설정** > **Raspberry Pi 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Raspbian 기본 설정 메뉴](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="3a007-160">**인터페이스** 탭에서 **I2C** 및 **SSH**를 **사용**으로 설정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="3a007-161">실제 센서가 없고 시뮬레이트된 센서 데이터를 사용하려는 경우 이 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Raspberry Pi에서 I2C 및 SSH를 사용하도록 설정](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="3a007-163">SSH 및 I2C를 사용하려는 경우 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 및 [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)에서 더 많은 참조 문서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="3a007-164">Pi에 센서 연결</span><span class="sxs-lookup"><span data-stu-id="3a007-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="3a007-165">실험용 회로판과 점퍼 와이어를 사용하여 LED 및 BME280 Pi를 다음과 같이 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="3a007-166">센서가 없는 경우 이 섹션을 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="3a007-166">If you don’t have the sensor, skip this section.</span></span>

![Raspberry Pi와 센서 연결](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="3a007-168">BME280 센서는 온도 및 습도 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="3a007-169">그리고 장치와 클라우드 간에 통신이 있으면 LED가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="3a007-170">센서 핀의 경우 다음 배선을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="3a007-171">시작(센서 및 LED)</span><span class="sxs-lookup"><span data-stu-id="3a007-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="3a007-172">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="3a007-172">End (Board)</span></span>            | <span data-ttu-id="3a007-173">케이블 색</span><span class="sxs-lookup"><span data-stu-id="3a007-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="3a007-174">VDD(5G 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="3a007-175">3.3V PWR(1 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="3a007-176">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="3a007-176">White cable</span></span>   |
| <span data-ttu-id="3a007-177">GND(7G 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="3a007-178">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-178">GND (Pin 6)</span></span>            | <span data-ttu-id="3a007-179">갈색 케이블</span><span class="sxs-lookup"><span data-stu-id="3a007-179">Brown cable</span></span>   |
| <span data-ttu-id="3a007-180">SCK(8G 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="3a007-181">I2C1 SDA(3 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="3a007-182">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="3a007-182">Orange cable</span></span>  |
| <span data-ttu-id="3a007-183">SDI(10G 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="3a007-184">I2C1 SCL(5 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="3a007-185">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="3a007-185">Red cable</span></span>     |
| <span data-ttu-id="3a007-186">LED VDD(18F 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="3a007-187">GPIO 24(18 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="3a007-188">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="3a007-188">White cable</span></span>   |
| <span data-ttu-id="3a007-189">LED GND(17F 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="3a007-190">GND(20 핀)</span><span class="sxs-lookup"><span data-stu-id="3a007-190">GND (Pin 20)</span></span>           | <span data-ttu-id="3a007-191">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="3a007-191">Black cable</span></span>   |

<span data-ttu-id="3a007-192">참조용으로 [Raspberry Pi 2 및 3 핀 매핑](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)을 보려면 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="3a007-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="3a007-193">BME280이 Raspberry Pi에 성공적으로 연결되면 아래 이미지처럼 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi와 BME280 연결](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="3a007-195">네트워크에 Pi 연결</span><span class="sxs-lookup"><span data-stu-id="3a007-195">Connect Pi to the network</span></span>

<span data-ttu-id="3a007-196">마이크로 USB 케이블 및 전원 공급 장치를 사용하여 Pi를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="3a007-197">이더넷 케이블을 사용하여 Pi를 유선 네트워크에 연결하거나 [Raspberry Pi Foundation의 지침](https://www.raspberrypi.org/learning/software-guide/wifi/)에 따라 Pi를 무선 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="3a007-198">Pi가 네트워크에 성공적으로 연결된 후 [Pi의 IP 주소](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)를 적어 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![유선 네트워크에 연결](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="3a007-200">Pi가 컴퓨터와 같은 네트워크에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="3a007-201">예를 들어 컴퓨터는 무선 네트워크, Pi는 유선 네트워크에 연결되었다면 devdisco 출력에 IP 주소가 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="3a007-202">Pi에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3a007-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="3a007-203">샘플 응용 프로그램을 복제하고 필수 구성 요소 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="3a007-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="3a007-204">호스트 컴퓨터에서 다음 SSH 클라이언트 중 하나를 사용하여 Raspberry Pi에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="3a007-205">Windows용 [PuTTY](http://www.putty.org/)</span><span class="sxs-lookup"><span data-stu-id="3a007-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="3a007-206">SSH를 통해 연결하려면 Pi의 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="3a007-207">Ubuntu 또는 macOS에 있는 기본 제공 SSH 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3a007-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="3a007-208">SSH를 통해 Pi를 연결하려면 `ssh pi@<ip address of pi>`를 실행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="3a007-209">기본 사용자 이름은 `pi`이며 암호는 `raspberry`입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="3a007-210">Node.js 및 NPM을 Pi에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="3a007-211">먼저 다음 명령을 사용하여 Node.js 버전을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="3a007-212">버전이 4.x보다 낮거나 Pi에 Node.js가 없는 경우 다음 명령을 실행하여 Node.js를 설치 또는 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="3a007-213">다음 명령을 실행하여 샘플 응용 프로그램을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="3a007-214">다음 명령을 사용하여 모든 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-214">Install all packages by the following command.</span></span> <span data-ttu-id="3a007-215">Azure IoT 장치 SDK, BME280 센서 라이브러리 및 배선 Pi 라이브러리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="3a007-216">네트워크 연결에 따라 이 설치 프로세스를 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="3a007-217">샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="3a007-217">Configure the sample application</span></span>

1. <span data-ttu-id="3a007-218">다음 명령을 실행하여 config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Config 파일](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="3a007-220">이 파일에는 사용자가 구성할 수 있는 두 개 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="3a007-221">첫 번째는 클라우드로 전송되는 두 메시지 사이의 간격을 정의하는 `interval`입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="3a007-222">두 번째는 시뮬레이션된 센서 데이터의 사용 여부에 대한 부울 값인 `simulatedData`입니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="3a007-223">**센서가 없는 경우** `simulatedData` 값을 `true`로 설정하여 샘플 응용 프로그램에서 시뮬레이션된 센서 데이터를 만들어서 사용하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="3a007-224">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="3a007-225">샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3a007-225">Run the sample application</span></span>

1. <span data-ttu-id="3a007-226">다음 명령을 실행하여 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="3a007-227">장치 연결 문자열을 복사하여 작은따옴표 안에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="3a007-228">IoT Hub로 전송되는 센서 데이터와 메시지를 보여 주는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![출력 - Raspberry Pi에서 IoT Hub로 전송된 센서 데이터](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="3a007-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a007-230">Next steps</span></span>

<span data-ttu-id="3a007-231">샘플 응용 프로그램을 실행하여 센서 데이터를 수집하고 IoT Hub로 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="3a007-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]