---
title: "aaaRaspberry Pi toocloud (Python)-라스베리 Pi 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 방법을 toosetup 하 고이 자습서에서는 라스베리 Pi toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 라스베리 Pi tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot 라즈베리 라즈베리 pi pi iot 허브 라즈베리 pi 송신 데이터 toocloud 라즈베리 pi toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="2662e-104">연결 라스베리 Pi tooAzure IoT 허브 (Python)</span><span class="sxs-lookup"><span data-stu-id="2662e-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="2662e-105">이 자습서에서는 먼저 라스베리 Pi Raspbian를 실행 하는 작업의 hello 기본 사항 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="2662e-106">그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="2662e-107">Windows 10 IoT Core 샘플에 대 한 이동 toohello [Windows 개발자 센터](http://www.windowsondevices.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="2662e-108">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="2662e-108">Don't have a kit yet?</span></span> <span data-ttu-id="2662e-109">[Raspberry Pi 온라인 시뮬레이터](iot-hub-raspberry-pi-web-simulator-get-started.md)를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2662e-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="2662e-110">또는 새 키트를 [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2662e-111">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="2662e-111">What you do</span></span>

* <span data-ttu-id="2662e-112">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-112">Create an IoT hub.</span></span>
* <span data-ttu-id="2662e-113">IoT Hub에 Pi용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="2662e-114">Raspberry Pi를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="2662e-115">Pi toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="2662e-116">만들면 라스베리 Pi tooan IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="2662e-117">다음 BME280 센서에서 Pi toocollect 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="2662e-118">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2662e-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="2662e-119">What you learn</span></span>

* <span data-ttu-id="2662e-120">어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="2662e-121">어떻게 tooconnect BME280 센서와 Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="2662e-122">어떻게 Pi에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="2662e-123">어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2662e-124">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="2662e-124">What you need</span></span>

![필요한 항목](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="2662e-126">hello 라스베리 Pi 2 또는 라스베리 Pi 3 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="2662e-127">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="2662e-127">An active Azure subscription.</span></span> <span data-ttu-id="2662e-128">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2662e-129">모니터, USB 키보드 및 마우스 tooPi 연결 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="2662e-130">Windows 또는 Linux를 실행하는 Mac 또는 PC.</span><span class="sxs-lookup"><span data-stu-id="2662e-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="2662e-131">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="2662e-131">An Internet connection.</span></span>
* <span data-ttu-id="2662e-132">16GB 이상의 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="2662e-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="2662e-133">USB SD 어댑터 또는 microSD 카드 tooburn hello에 운영 체제 이미지 hello microSD 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="2662e-134">Hello 6 피트 마이크로 USB 케이블을 5 v 2 amp 전원 공급 장치.</span><span class="sxs-lookup"><span data-stu-id="2662e-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="2662e-135">hello 다음 항목은 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="2662e-135">hello following items are optional:</span></span>

* <span data-ttu-id="2662e-136">조립된 Adafruit BME280 온도, 압력 및 습도 센서.</span><span class="sxs-lookup"><span data-stu-id="2662e-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="2662e-137">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="2662e-137">A breadboard.</span></span>
* <span data-ttu-id="2662e-138">F/M 점퍼 와이어 6개.</span><span class="sxs-lookup"><span data-stu-id="2662e-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="2662e-139">확산형 10mm LED.</span><span class="sxs-lookup"><span data-stu-id="2662e-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="2662e-140">Hello 코드 샘플 지원 센서 데이터를 시뮬레이션 하기 때문에 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="2662e-141">Raspberry Pi 설정</span><span class="sxs-lookup"><span data-stu-id="2662e-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="2662e-142">Pi에 대 한 hello Raspbian 운영 체제를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="2662e-143">Hello microSD 카드 hello Raspbian 이미지의 설치를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="2662e-144">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="2662e-145">[Desktop Raspbian 제시 다운로드](https://www.raspberrypi.org/downloads/raspbian/) (hello.zip 파일).</span><span class="sxs-lookup"><span data-stu-id="2662e-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="2662e-146">Hello Raspbian 이미지 tooa 컴퓨터의 폴더에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="2662e-147">Raspbian toohello microSD 카드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="2662e-148">[다운로드 및 설치 hello Etcher SD 카드 버너 유틸리티](https://etcher.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="2662e-149">Etcher를 실행 하 고 1 단계에서 압축을 푼 hello Raspbian 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="2662e-150">Hello microSD 카드 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-150">Select hello microSD card drive.</span></span> <span data-ttu-id="2662e-151">Etcher 선택 했을 수 이미 hello 올바른 드라이브 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="2662e-152">플래시 tooinstall Raspbian toohello microSD 카드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="2662e-153">설치가 완료 되 면 hello microSD 카드를 컴퓨터에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="2662e-154">되므로 안전 tooremove hello microSD 카드 직접 Etcher를 꺼냅니다. 자동으로 또는 완료 되 면 hello microSD 카드 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="2662e-155">Pi에 hello microSD 카드를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="2662e-156">SSH 및 I2C를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2662e-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="2662e-157">Pi toohello 모니터, 키보드 및 마우스 연결 Pi 시작한 다음 Raspbian 사용 하 여 로그인 `pi` hello. 사용자 이름 및 `raspberry` hello 암호와 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="2662e-158">Hello 라즈베리 아이콘 클릭 > **기본 설정** > **라스베리 Pi 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![hello Raspbian 기본 설정 메뉴](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="2662e-160">Hello에 **인터페이스** 탭, 설정 **I2C** 및 **SSH** 너무**사용**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="2662e-161">없습니다 실제 센서 고 시뮬레이션 toouse 센서 데이터를 하는 경우이 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Raspberry Pi에서 I2C 및 SSH를 사용하도록 설정](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="2662e-163">tooenable SSH 및 I2C에서 더 많은 참조 문서를 찾을 수 있습니다 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 및 [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="2662e-164">Hello 센서 tooPi 연결</span><span class="sxs-lookup"><span data-stu-id="2662e-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="2662e-165">사용 하 여 hello breadboard 및 점퍼 와이어 tooconnect LED 및 BME280 tooPi 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="2662e-166">Hello 센서가 없는 경우 [이 섹션을 건너뛸](#connect-pi-to-the-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![hello 라스베리 Pi 및 센서 연결](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="2662e-168">hello BME280 센서 온도 및 습도 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="2662e-169">및 장치 및 hello 클라우드 간의 통신 이면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="2662e-170">센서 핀에 대 한 다음 배선 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="2662e-171">시작(센서 및 LED)</span><span class="sxs-lookup"><span data-stu-id="2662e-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="2662e-172">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="2662e-172">End (Board)</span></span>            | <span data-ttu-id="2662e-173">케이블 색</span><span class="sxs-lookup"><span data-stu-id="2662e-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2662e-174">VDD(5G 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="2662e-175">3.3V PWR(1 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="2662e-176">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="2662e-176">White cable</span></span>   |
| <span data-ttu-id="2662e-177">GND(7G 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="2662e-178">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-178">GND (Pin 6)</span></span>            | <span data-ttu-id="2662e-179">갈색 케이블</span><span class="sxs-lookup"><span data-stu-id="2662e-179">Brown cable</span></span>   |
| <span data-ttu-id="2662e-180">SDI(10G 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="2662e-181">I2C1 SDA(3 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="2662e-182">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="2662e-182">Red cable</span></span>     |
| <span data-ttu-id="2662e-183">SCK(8G 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="2662e-184">I2C1 SCL(5 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="2662e-185">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="2662e-185">Orange cable</span></span>  |
| <span data-ttu-id="2662e-186">LED VDD(18F 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="2662e-187">GPIO 24(18 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="2662e-188">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="2662e-188">White cable</span></span>   |
| <span data-ttu-id="2662e-189">LED GND(17F 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="2662e-190">GND(20 핀)</span><span class="sxs-lookup"><span data-stu-id="2662e-190">GND (Pin 20)</span></span>           | <span data-ttu-id="2662e-191">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="2662e-191">Black cable</span></span>   |

<span data-ttu-id="2662e-192">Tooview 클릭 [라스베리 Pi 2 & 3 Pin 매핑](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) 참조할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="2662e-193">성공적으로 연결한 후 BME280 tooyour 라스베리 Pi와 같은 이미지 아래 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi와 BME280 연결](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="2662e-195">Pi toohello 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="2662e-195">Connect Pi toohello network</span></span>

<span data-ttu-id="2662e-196">Pi hello 마이크로 USB 케이블 및 hello 전원 공급 장치를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="2662e-197">사용 하 여 hello 이더넷 케이블 tooconnect Pi tooyour 유선 네트워크 또는 hello에 따라 [hello 라스베리 Pi Foundation의에서 지침에 따라](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 무선 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="2662e-198">Tootake hello 메모 필요 하면 Pi에 대 한 toohello 성공적으로 연결 된 네트워크를 수행한 후 [프로그램 Pi의 IP 주소](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![연결 된 toowired 네트워크](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="2662e-200">Pi 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="2662e-201">예를 들어 컴퓨터는 연결 된 tooa 무선 네트워크 Pi는 유선 네트워크 연결된 tooa를 동안 표시 될 수 없습니다 hello IP hello devdisco 출력에는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="2662e-202">Pi에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2662e-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="2662e-203">Hello 필수 구성 요소 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="2662e-204">Hello 호스트 컴퓨터 tooconnect tooyour 라스베리 Pi에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="2662e-205">**Windows 사용자**</span><span class="sxs-lookup"><span data-stu-id="2662e-205">**Windows Users**</span></span>
   1. <span data-ttu-id="2662e-206">Windows용 [PuTTY](http://www.putty.org/)를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="2662e-207">Hello 호스트 이름 (또는 IP 주소)에 Pi 섹션의 hello IP 주소를 복사 하 고 SSH hello 연결 유형으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="2662e-208">**Mac 및 Ubuntu 사용자**</span><span class="sxs-lookup"><span data-stu-id="2662e-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="2662e-209">Ubuntu 또는 macOS에 SSH 클라이언트를 기본 제공 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="2662e-210">Toorun 해야 `ssh pi@<ip address of pi>` tooconnect SSH 통해 Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="2662e-211">hello 기본 사용자 이름은 `pi` , hello 암호도 `raspberry`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="2662e-212">Hello 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="2662e-212">Configure hello sample application</span></span>

1. <span data-ttu-id="2662e-213">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="2662e-214">Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="2662e-215">이 파일에는 사용자가 구성할 수 있는 5개의 매크로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="2662e-216">hello 먼저 하나는 `MESSAGE_TIMESPAN`, toocloud 전송 하는 두 개의 메시지 간의 hello 시간 간격 (밀리초)을 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="2662e-217">두 번째 식 hello `SIMULATED_DATA`, 값은 부울 값 여부 toouse 센서 데이터를 시뮬레이션 하는 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="2662e-218">`I2C_ADDRESS`BME280 센서 연결 된 hello I2C 주소가입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="2662e-219">`GPIO_PIN_ADDRESS`에 대 한 프로그램 LED는 hello GPIO 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="2662e-220">hello 마지막 하나는 `BLINK_TIMESPAN`, hello timespan (밀리초) 여 LED 상태에서 정의 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="2662e-221">경우 있습니다 **hello 센서 없는**설정 hello `SIMULATED_DATA` 너무 값`True` toomake hello 샘플 응용 프로그램을 만들고 시뮬레이션된 센서 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="2662e-222">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="2662e-223">빌드 및 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2662e-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="2662e-224">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="2662e-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="2662e-225">Python 용 Azure IoT Sdk hello hello Azure IoT 장치 C SDK 위에 래퍼 이기 때문에 toocompile hello C 라이브러리를 원 하거나 소스 코드에서 toogenerate hello Python 라이브러리를 필요로 하는 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="2662e-226">실행 하 여 원하는 hello 버전을 지정할 수도 있습니다 `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="2662e-227">Hello 스크립트에서는 python 설치의 hello 버전을 자동으로 검색 매개 변수 없이 스크립트를 실행 하는 경우 (검색 시퀀스 2.7 3.4-> 3.5->).</span><span class="sxs-lookup"><span data-stu-id="2662e-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="2662e-228">Python 버전을 빌드하고 실행하는 동안 일관성 있게 유지하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="2662e-229">Hello Python 클라이언트 라이브러리 (iothub_client.so) 보다 작거나 1 g B RAM이 있는 Linux 장치에 구축에 표시 될 수 있습니다 98% 아래와 같이 iothub_client_python.cpp를 작성 하는 동안 전송 되지 않는 빌드 `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="2662e-230">이 문제를 실행 하면 hello 장치를 사용 하 여 hello 메모리 사용량 확인 `free -m command` 이 시간 동안 다른 터미널 창에서.</span><span class="sxs-lookup"><span data-stu-id="2662e-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="2662e-231">Hello 스왑 공간 tooget 증가 tootemporarily 있을 iothub_client_python.cpp 파일을 컴파일하는 동안 메모리 부족 실행 하는 경우 보다 많은 가용 메모리 toosuccessfully hello Python 클라이언트 쪽 장치 SDK 라이브러리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="2662e-232">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="2662e-233">하면 복사-붙여넣기 hello 장치 연결 문자열 hello 작은따옴표에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="2662e-234">Hello python 3을 사용할 경우 사용할 수 있습니다 및 hello 명령 `python3 app.py '<your Azure IoT hub device connection string>'`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="2662e-235">Hello 다음 출력에서는 hello 센서 데이터와 hello 전송 된 메시지를 tooyour IoT 허브는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![출력-라스베리 Pi tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="2662e-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2662e-237">Next steps</span></span>

<span data-ttu-id="2662e-238">샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="2662e-239">라스베리 Pi가 보냈음을 tooyour IoT 허브 또는 송신 메시지 tooyour 라스베리 Pi는 명령줄 인터페이스에서 toosee hello 메시지 참조 hello [iothub 탐색기 자습서와 함께 메시징 관리 클라우드 장치](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662e-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
