---
title: "aaaRaspberry Pi toocloud (C)-라스베리 Pi 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 방법을 toosetup 하 고이 자습서에서는 라스베리 Pi toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 라스베리 Pi tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot 라즈베리 라즈베리 pi pi iot 허브 라즈베리 pi 송신 데이터 toocloud 라즈베리 pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a><span data-ttu-id="5bfd8-104">라스베리 Pi tooAzure IoT Hub (C) 연결</span><span class="sxs-lookup"><span data-stu-id="5bfd8-104">Connect Raspberry Pi tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="5bfd8-105">이 자습서에서는 먼저 라스베리 Pi Raspbian를 실행 하는 작업의 hello 기본 사항 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="5bfd8-106">그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="5bfd8-107">Windows 10 IoT Core 샘플에 대 한 이동 toohello [Windows 개발자 센터](http://www.windowsondevices.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="5bfd8-108">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="5bfd8-108">Don't have a kit yet?</span></span> <span data-ttu-id="5bfd8-109">[Raspberry Pi 온라인 시뮬레이터](iot-hub-raspberry-pi-web-simulator-get-started.md)를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="5bfd8-110">또는 새 키트를 [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="5bfd8-111">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="5bfd8-111">What you do</span></span>

* <span data-ttu-id="5bfd8-112">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-112">Create an IoT hub.</span></span>
* <span data-ttu-id="5bfd8-113">IoT Hub에 Pi용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="5bfd8-114">Raspberry Pi를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="5bfd8-115">Pi toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="5bfd8-116">만들면 라스베리 Pi tooan IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="5bfd8-117">다음 BME280 센서에서 Pi toocollect 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="5bfd8-118">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="5bfd8-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="5bfd8-119">What you learn</span></span>

* <span data-ttu-id="5bfd8-120">어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="5bfd8-121">어떻게 tooconnect BME280 센서와 Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="5bfd8-122">어떻게 Pi에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="5bfd8-123">어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5bfd8-124">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="5bfd8-124">What you need</span></span>

![필요한 항목](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="5bfd8-126">hello 라스베리 Pi 2 또는 라스베리 Pi 3 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="5bfd8-127">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-127">An active Azure subscription.</span></span> <span data-ttu-id="5bfd8-128">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="5bfd8-129">모니터, USB 키보드 및 마우스 tooPi 연결 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="5bfd8-130">Windows 또는 Linux를 실행하는 Mac 또는 PC.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="5bfd8-131">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-131">An Internet connection.</span></span>
* <span data-ttu-id="5bfd8-132">16GB 이상의 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="5bfd8-133">USB SD 어댑터 또는 microSD 카드 tooburn hello에 운영 체제 이미지 hello microSD 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="5bfd8-134">Hello 6 피트 마이크로 USB 케이블을 5 v 2 amp 전원 공급 장치.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="5bfd8-135">hello 다음 항목은 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="5bfd8-135">hello following items are optional:</span></span>

* <span data-ttu-id="5bfd8-136">조립된 Adafruit BME280 온도, 압력 및 습도 센서.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="5bfd8-137">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="5bfd8-137">A breadboard.</span></span>
* <span data-ttu-id="5bfd8-138">F/M 점퍼 와이어 6개.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="5bfd8-139">확산형 10mm LED.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="5bfd8-140">Hello 코드 샘플 지원 센서 데이터를 시뮬레이션 하기 때문에 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="5bfd8-141">Raspberry Pi 설치</span><span class="sxs-lookup"><span data-stu-id="5bfd8-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="5bfd8-142">Pi에 대 한 hello Raspbian 운영 체제를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="5bfd8-143">Hello microSD 카드 hello Raspbian 이미지의 설치를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="5bfd8-144">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="5bfd8-145">[Desktop Raspbian 제시 다운로드](https://www.raspberrypi.org/downloads/raspbian/) (hello.zip 파일).</span><span class="sxs-lookup"><span data-stu-id="5bfd8-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="5bfd8-146">Hello Raspbian 이미지 tooa 컴퓨터의 폴더에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="5bfd8-147">Raspbian toohello microSD 카드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="5bfd8-148">[다운로드 및 설치 hello Etcher SD 카드 버너 유틸리티](https://etcher.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="5bfd8-149">Etcher를 실행 하 고 1 단계에서 압축을 푼 hello Raspbian 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="5bfd8-150">Hello microSD 카드 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-150">Select hello microSD card drive.</span></span> <span data-ttu-id="5bfd8-151">Etcher 선택 했을 수 이미 hello 올바른 드라이브 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="5bfd8-152">플래시 tooinstall Raspbian toohello microSD 카드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="5bfd8-153">설치가 완료 되 면 hello microSD 카드를 컴퓨터에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="5bfd8-154">되므로 안전 tooremove hello microSD 카드 직접 Etcher를 꺼냅니다. 자동으로 또는 완료 되 면 hello microSD 카드 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="5bfd8-155">Pi에 hello microSD 카드를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="5bfd8-156">SSH 및 SPI를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5bfd8-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="5bfd8-157">Pi toohello 모니터, 키보드 및 마우스 연결 Pi 시작한 다음 Raspbian 사용 하 여 로그인 `pi` hello. 사용자 이름 및 `raspberry` hello 암호와 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="5bfd8-158">Hello 라즈베리 아이콘 클릭 > **기본 설정** > **라스베리 Pi 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![hello Raspbian 기본 설정 메뉴](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="5bfd8-160">Hello에 **인터페이스** 탭, 설정 **SPI** 및 **SSH** 너무**사용**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-160">On hello **Interfaces** tab, set **SPI** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="5bfd8-161">없습니다 실제 센서 고 시뮬레이션 toouse 센서 데이터를 하는 경우이 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Raspberry Pi에서 SPI 및 SSH를 사용하도록 설정](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="5bfd8-163">tooenable SSH 및 SPI에서 더 많은 참조 문서를 찾을 수 있습니다 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 및 [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-163">tooenable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="5bfd8-164">Hello 센서 tooPi 연결</span><span class="sxs-lookup"><span data-stu-id="5bfd8-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="5bfd8-165">사용 하 여 hello breadboard 및 점퍼 와이어 tooconnect LED 및 BME280 tooPi 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="5bfd8-166">Hello 센서가 없는 경우 [이 섹션을 건너뛸](#connect-pi-to-the-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![hello 라스베리 Pi 및 센서 연결](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="5bfd8-168">hello BME280 센서 온도 및 습도 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="5bfd8-169">및 장치 및 hello 클라우드 간의 통신 이면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="5bfd8-170">센서 핀에 대 한 다음 배선 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="5bfd8-171">시작(센서 및 LED)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="5bfd8-172">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-172">End (Board)</span></span>            | <span data-ttu-id="5bfd8-173">케이블 색</span><span class="sxs-lookup"><span data-stu-id="5bfd8-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="5bfd8-174">LED VDD(5G 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="5bfd8-175">GPIO 4(7 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="5bfd8-176">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-176">White cable</span></span>   |
| <span data-ttu-id="5bfd8-177">LED GND(6G 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="5bfd8-178">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-178">GND (Pin 6)</span></span>            | <span data-ttu-id="5bfd8-179">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-179">Black cable</span></span>   |
| <span data-ttu-id="5bfd8-180">VDD(18F 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="5bfd8-181">3.3V PWR(17 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="5bfd8-182">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-182">White cable</span></span>   |
| <span data-ttu-id="5bfd8-183">GND(20F 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="5bfd8-184">GND(20 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-184">GND (Pin 20)</span></span>           | <span data-ttu-id="5bfd8-185">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-185">Black cable</span></span>   |
| <span data-ttu-id="5bfd8-186">SCK(21F 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="5bfd8-187">SPI0 SCLK(23 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="5bfd8-188">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-188">Orange cable</span></span>  |
| <span data-ttu-id="5bfd8-189">SDO(22F 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="5bfd8-190">SPI0 MISO(21 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="5bfd8-191">노란색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-191">Yellow cable</span></span>  |
| <span data-ttu-id="5bfd8-192">SDI(23F 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="5bfd8-193">SPI0 MOSI(19 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="5bfd8-194">녹색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-194">Green cable</span></span>   |
| <span data-ttu-id="5bfd8-195">CS(24F 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="5bfd8-196">SPI0 CS(24 핀)</span><span class="sxs-lookup"><span data-stu-id="5bfd8-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="5bfd8-197">파란색 케이블</span><span class="sxs-lookup"><span data-stu-id="5bfd8-197">Blue cable</span></span>    |

<span data-ttu-id="5bfd8-198">Tooview 클릭 [라스베리 Pi 2 & 3 Pin 매핑](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) 참조할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-198">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="5bfd8-199">성공적으로 연결한 후 BME280 tooyour 라스베리 Pi와 같은 이미지 아래 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-199">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi와 BME280 연결](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="5bfd8-201">Pi toohello 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="5bfd8-201">Connect Pi toohello network</span></span>

<span data-ttu-id="5bfd8-202">Pi hello 마이크로 USB 케이블 및 hello 전원 공급 장치를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-202">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="5bfd8-203">사용 하 여 hello 이더넷 케이블 tooconnect Pi tooyour 유선 네트워크 또는 hello에 따라 [hello 라스베리 Pi Foundation의에서 지침에 따라](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 무선 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-203">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="5bfd8-204">Tootake hello 메모 필요 하면 Pi에 대 한 toohello 성공적으로 연결 된 네트워크를 수행한 후 [프로그램 Pi의 IP 주소](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-204">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![연결 된 toowired 네트워크](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="5bfd8-206">Pi에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="5bfd8-206">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="5bfd8-207">Hello 필수 구성 요소 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-207">Install hello prerequisite packages</span></span>

1. <span data-ttu-id="5bfd8-208">Hello 호스트 컴퓨터 tooconnect tooyour 라스베리 Pi에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-208">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="5bfd8-209">**Windows 사용자**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-209">**Windows Users**</span></span>
   1. <span data-ttu-id="5bfd8-210">Windows용 [PuTTY](http://www.putty.org/)를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="5bfd8-211">Hello 호스트 이름 (또는 IP 주소)에 Pi 섹션의 hello IP 주소를 복사 하 고 SSH hello 연결 유형으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-211">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="5bfd8-213">**Mac 및 Ubuntu 사용자**</span><span class="sxs-lookup"><span data-stu-id="5bfd8-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="5bfd8-214">Ubuntu 또는 macOS에 SSH 클라이언트를 기본 제공 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-214">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="5bfd8-215">Toorun 해야 `ssh pi@<ip address of pi>` tooconnect SSH 통해 Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-215">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="5bfd8-216">hello 기본 사용자 이름은 `pi` , hello 암호도 `raspberry`합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-216">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="5bfd8-217">C 및 Cmake hello 다음 명령을 실행 하 여 hello hello Microsoft Azure IoT 장치 SDK에 대 한 필수 구성 요소 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-217">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C and Cmake by running hello following commands:</span></span>

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


### <a name="configure-hello-sample-application"></a><span data-ttu-id="5bfd8-218">Hello 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="5bfd8-218">Configure hello sample application</span></span>

1. <span data-ttu-id="5bfd8-219">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-219">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="5bfd8-220">Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Config 파일](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="5bfd8-222">이 파일에는 사용자가 구성할 수 있는 두 개의 매크로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="5bfd8-223">hello 먼저 하나는 `INTERVAL`, toocloud 전송 하는 두 개의 메시지 간의 hello 시간 간격 (밀리초)을 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-223">hello first one is `INTERVAL`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="5bfd8-224">두 번째 식 hello `SIMULATED_DATA`, 값은 부울 값 여부 toouse 센서 데이터를 시뮬레이션 하는 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="5bfd8-225">경우 있습니다 **hello 센서 없는**설정 hello `SIMULATED_DATA` 너무 값`1` toomake hello 샘플 응용 프로그램을 만들고 시뮬레이션된 센서 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="5bfd8-226">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="5bfd8-227">빌드 및 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="5bfd8-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="5bfd8-228">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![빌드 출력](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="5bfd8-230">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="5bfd8-231">하면 복사-붙여넣기 hello 장치 연결 문자열 hello 작은따옴표에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="5bfd8-232">Hello 다음 출력에서는 hello 센서 데이터와 hello 전송 된 메시지를 tooyour IoT 허브는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![출력-라스베리 Pi tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="5bfd8-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5bfd8-234">Next steps</span></span>

<span data-ttu-id="5bfd8-235">샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="5bfd8-236">라스베리 Pi가 보냈음을 tooyour IoT 허브 또는 송신 메시지 tooyour 라스베리 Pi는 명령줄 인터페이스에서 toosee hello 메시지 참조 hello [iothub 탐색기 자습서와 함께 메시징 관리 클라우드 장치](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)합니다.</span><span class="sxs-lookup"><span data-stu-id="5bfd8-236">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
