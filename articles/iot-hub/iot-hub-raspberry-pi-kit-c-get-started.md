---
title: "Raspberry Pi-클라우드(C) - Raspberry Pi를 Azure IoT Hub에 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure 클라우드 플랫폼으로 데이터를 보내기 위해 Raspberry Pi을 설정하고 Raspberry Pi용 Azure IoT Hub에 연결하는 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi에서 클라우드로 데이터 전송, raspberry pi-클라우드"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b8fda17a8d1d1796d5299e3aba4b0fd5e719a4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a><span data-ttu-id="2703a-104">Raspberry Pi를 Azure IoT Hub에 연결(C)</span><span class="sxs-lookup"><span data-stu-id="2703a-104">Connect Raspberry Pi to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="2703a-105">이 자습서에서는 Raspbian을 실행하는 Raspberry Pi 작업의 기초부터 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="2703a-106">그런 다음 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)를 사용하여 장치를 클라우드에 원활하게 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="2703a-107">Windows 10 IoT Core 샘플이 필요하면 [Windows 개발자 센터](http://www.windowsondevices.com/)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="2703a-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="2703a-108">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="2703a-108">Don't have a kit yet?</span></span> <span data-ttu-id="2703a-109">[Raspberry Pi 온라인 시뮬레이터](iot-hub-raspberry-pi-web-simulator-get-started.md)를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2703a-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="2703a-110">또는 새 키트를 [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2703a-111">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="2703a-111">What you do</span></span>

* <span data-ttu-id="2703a-112">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-112">Create an IoT hub.</span></span>
* <span data-ttu-id="2703a-113">IoT Hub에 Pi용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="2703a-114">Raspberry Pi를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="2703a-115">Pi에서 샘플 응용 프로그램을 실행하여 IoT Hub로 센서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="2703a-116">앞에서 만든 IoT Hub에 Raspberry Pi를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="2703a-117">그런 다음 Pi에서 샘플 응용 프로그램을 실행하여 BME280에서 온도 및 습도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="2703a-118">마지막으로 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2703a-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="2703a-119">What you learn</span></span>

* <span data-ttu-id="2703a-120">Azure IoT Hub를 만들고 새 장치 연결 문자열을 가져오는 방법.</span><span class="sxs-lookup"><span data-stu-id="2703a-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="2703a-121">Pi를 BME280 센서와 연결하는 방법.</span><span class="sxs-lookup"><span data-stu-id="2703a-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="2703a-122">Pi에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법.</span><span class="sxs-lookup"><span data-stu-id="2703a-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="2703a-123">IoT Hub로 센서 데이터를 보내는 방법.</span><span class="sxs-lookup"><span data-stu-id="2703a-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2703a-124">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="2703a-124">What you need</span></span>

![필요한 항목](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="2703a-126">Raspberry Pi 2 또는 Raspberry Pi 3 보드.</span><span class="sxs-lookup"><span data-stu-id="2703a-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="2703a-127">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="2703a-127">An active Azure subscription.</span></span> <span data-ttu-id="2703a-128">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2703a-129">Pi에 연결할 모니터, USB 키보드 및 마우스.</span><span class="sxs-lookup"><span data-stu-id="2703a-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="2703a-130">Windows 또는 Linux를 실행하는 Mac 또는 PC.</span><span class="sxs-lookup"><span data-stu-id="2703a-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="2703a-131">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="2703a-131">An Internet connection.</span></span>
* <span data-ttu-id="2703a-132">16GB 이상의 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="2703a-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="2703a-133">운영 체제 이미지를 microSD 카드에 굽기 위한 USB-SD 어댑터 또는 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="2703a-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="2703a-134">6피트 마이크로 USB 케이블과 5볼트 2암페어 전원 공급 장치.</span><span class="sxs-lookup"><span data-stu-id="2703a-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="2703a-135">다음 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-135">The following items are optional:</span></span>

* <span data-ttu-id="2703a-136">조립된 Adafruit BME280 온도, 압력 및 습도 센서.</span><span class="sxs-lookup"><span data-stu-id="2703a-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="2703a-137">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="2703a-137">A breadboard.</span></span>
* <span data-ttu-id="2703a-138">F/M 점퍼 와이어 6개.</span><span class="sxs-lookup"><span data-stu-id="2703a-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="2703a-139">확산형 10mm LED.</span><span class="sxs-lookup"><span data-stu-id="2703a-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="2703a-140">코드 샘플이 시뮬레이션된 센서 데이터를 지원하므로 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="2703a-141">Raspberry Pi 설치</span><span class="sxs-lookup"><span data-stu-id="2703a-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="2703a-142">Pi용 Raspbian 운영 체제 설치</span><span class="sxs-lookup"><span data-stu-id="2703a-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="2703a-143">Raspbian 이미지를 설치를 위해 microSD 카드를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="2703a-144">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="2703a-145">[Raspbian Jessie with Desktop을 다운로드합니다](https://www.raspberrypi.org/downloads/raspbian/)(.zip 파일).</span><span class="sxs-lookup"><span data-stu-id="2703a-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="2703a-146">컴퓨터의 폴더에 Raspbian 이미지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="2703a-147">microSD 카드에 Raspbian을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="2703a-148">[Etcher SD 카드 버너 유틸리티를 다운로드하여 설치합니다](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="2703a-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="2703a-149">Etcher를 실행하고 1단계에서 압축을 푼 Raspbian 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="2703a-150">microSD 카드 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-150">Select the microSD card drive.</span></span> <span data-ttu-id="2703a-151">Etcher가 이미 올바른 드라이브를 선택했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="2703a-152">Flash를 클릭하여 microSD 카드에 Raspbian을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="2703a-153">설치가 완료되면 컴퓨터에서 microSD 카드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="2703a-154">완료되면 Etcher가 microSD 카드를 자동으로 배출하거나 탑재를 해제하므로 microSD 카드를 바로 제거하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="2703a-155">Pi에 microSD 카드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="2703a-156">SSH 및 SPI를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2703a-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="2703a-157">사용자 이름으로 `pi`, 암호로 `raspberry`를 사용하여 Pi를 모니터, 키보드, 마우스에 연결하고, Pi를 시작한 다음 Raspbian에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="2703a-158">Raspberry 아이콘 > **기본 설정** > **Raspberry Pi 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Raspbian 기본 설정 메뉴](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="2703a-160">**인터페이스** 탭에서 **SPI** 및 **SSH**를 **사용**으로 설정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-160">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="2703a-161">실제 센서가 없고 시뮬레이트된 센서 데이터를 사용하려는 경우 이 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Raspberry Pi에서 SPI 및 SSH를 사용하도록 설정](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="2703a-163">SSH 및 SPI를 사용하려는 경우 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 및 [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)에서 더 많은 참조 문서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-163">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="2703a-164">Pi에 센서 연결</span><span class="sxs-lookup"><span data-stu-id="2703a-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="2703a-165">실험용 회로판과 점퍼 와이어를 사용하여 LED 및 BME280 Pi를 다음과 같이 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="2703a-166">센서가 없는 경우 [이 섹션을 건너뛰세요](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="2703a-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Raspberry Pi와 센서 연결](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="2703a-168">BME280 센서는 온도 및 습도 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="2703a-169">그리고 장치와 클라우드 간에 통신이 있으면 LED가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="2703a-170">센서 핀의 경우 다음 배선을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="2703a-171">시작(센서 및 LED)</span><span class="sxs-lookup"><span data-stu-id="2703a-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="2703a-172">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="2703a-172">End (Board)</span></span>            | <span data-ttu-id="2703a-173">케이블 색</span><span class="sxs-lookup"><span data-stu-id="2703a-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2703a-174">LED VDD(5G 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="2703a-175">GPIO 4(7 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="2703a-176">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-176">White cable</span></span>   |
| <span data-ttu-id="2703a-177">LED GND(6G 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="2703a-178">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-178">GND (Pin 6)</span></span>            | <span data-ttu-id="2703a-179">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-179">Black cable</span></span>   |
| <span data-ttu-id="2703a-180">VDD(18F 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="2703a-181">3.3V PWR(17 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="2703a-182">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-182">White cable</span></span>   |
| <span data-ttu-id="2703a-183">GND(20F 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="2703a-184">GND(20 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-184">GND (Pin 20)</span></span>           | <span data-ttu-id="2703a-185">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-185">Black cable</span></span>   |
| <span data-ttu-id="2703a-186">SCK(21F 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="2703a-187">SPI0 SCLK(23 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="2703a-188">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-188">Orange cable</span></span>  |
| <span data-ttu-id="2703a-189">SDO(22F 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="2703a-190">SPI0 MISO(21 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="2703a-191">노란색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-191">Yellow cable</span></span>  |
| <span data-ttu-id="2703a-192">SDI(23F 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="2703a-193">SPI0 MOSI(19 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="2703a-194">녹색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-194">Green cable</span></span>   |
| <span data-ttu-id="2703a-195">CS(24F 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="2703a-196">SPI0 CS(24 핀)</span><span class="sxs-lookup"><span data-stu-id="2703a-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="2703a-197">파란색 케이블</span><span class="sxs-lookup"><span data-stu-id="2703a-197">Blue cable</span></span>    |

<span data-ttu-id="2703a-198">참조용으로 [Raspberry Pi 2 및 3 핀 매핑](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)을 보려면 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2703a-198">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="2703a-199">BME280이 Raspberry Pi에 성공적으로 연결되면 아래 이미지처럼 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-199">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi와 BME280 연결](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="2703a-201">네트워크에 Pi 연결</span><span class="sxs-lookup"><span data-stu-id="2703a-201">Connect Pi to the network</span></span>

<span data-ttu-id="2703a-202">마이크로 USB 케이블 및 전원 공급 장치를 사용하여 Pi를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-202">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="2703a-203">이더넷 케이블을 사용하여 Pi를 유선 네트워크에 연결하거나 [Raspberry Pi Foundation의 지침](https://www.raspberrypi.org/learning/software-guide/wifi/)에 따라 Pi를 무선 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-203">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="2703a-204">Pi가 네트워크에 성공적으로 연결된 후 [Pi의 IP 주소](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)를 적어 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-204">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![유선 네트워크에 연결](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="2703a-206">Pi에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2703a-206">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="2703a-207">필수 구성 요소 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="2703a-207">Install the prerequisite packages</span></span>

1. <span data-ttu-id="2703a-208">호스트 컴퓨터에서 다음 SSH 클라이언트 중 하나를 사용하여 Raspberry Pi에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-208">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="2703a-209">**Windows 사용자**</span><span class="sxs-lookup"><span data-stu-id="2703a-209">**Windows Users**</span></span>
   1. <span data-ttu-id="2703a-210">Windows용 [PuTTY](http://www.putty.org/)를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="2703a-211">호스트 이름(또는 IP 주소) 섹션에 Pi의 IP 주소를 복사하고 연결 형식으로 SSH를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-211">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="2703a-213">**Mac 및 Ubuntu 사용자**</span><span class="sxs-lookup"><span data-stu-id="2703a-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="2703a-214">Ubuntu 또는 macOS에서 기본 제공되는 SSH 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-214">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="2703a-215">SSH를 통해 Pi를 연결하려면 `ssh pi@<ip address of pi>`를 실행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-215">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="2703a-216">기본 사용자 이름은 `pi`이며 암호는 `raspberry`입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-216">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="2703a-217">다음 명령을 실행하여 C와 Cmake에 대한 Microsoft Azure IoT 장치 SDK의 필수 구성 요소 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-217">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-the-sample-application"></a><span data-ttu-id="2703a-218">샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="2703a-218">Configure the sample application</span></span>

1. <span data-ttu-id="2703a-219">다음 명령을 실행하여 샘플 응용 프로그램을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-219">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="2703a-220">다음 명령을 실행하여 config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-220">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Config 파일](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="2703a-222">이 파일에는 사용자가 구성할 수 있는 두 개의 매크로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="2703a-223">첫 번째는 클라우드로 전송되는 두 메시지 사이의 시간 간격(밀리초)을 정의하는 `INTERVAL`입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-223">The first one is `INTERVAL`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="2703a-224">두 번째는 시뮬레이션된 센서 데이터의 사용 여부에 대한 부울 값인 `SIMULATED_DATA`입니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="2703a-225">**센서가 없는 경우** `SIMULATED_DATA` 값을 `1`로 설정하여 샘플 응용 프로그램에서 시뮬레이션된 센서 데이터를 만들어서 사용하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="2703a-226">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="2703a-227">응용 프로그램 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="2703a-227">Build and run the sample application</span></span>

1. <span data-ttu-id="2703a-228">다음 명령을 실행하여 샘플 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![빌드 출력](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="2703a-230">다음 명령을 실행하여 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="2703a-231">장치 연결 문자열을 복사하여 작은따옴표 안에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="2703a-232">IoT Hub로 전송되는 센서 데이터와 메시지를 보여 주는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![출력 - Raspberry Pi에서 IoT Hub로 전송된 센서 데이터](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="2703a-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2703a-234">Next steps</span></span>

<span data-ttu-id="2703a-235">샘플 응용 프로그램을 실행하여 센서 데이터를 수집하고 IoT Hub로 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="2703a-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="2703a-236">Raspberry Pi가 사용자 IoT Hub로 보낸 메시지 또는 명령줄 인터페이스에서 Raspberry Pi로 보낸 송신 메시지를 보려면 [iothub-explorer를 사용한 클라우드 장치 메시징 관리 자습서](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2703a-236">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
