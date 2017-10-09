---
title: "aaaRaspberry Pi toocloud (Node.js)-라스베리 Pi 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "Azure 클라우드 라스베리 Pi toosend 데이터 toohello에 대 한 라스베리 Pi tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 라즈베리 라즈베리 pi pi iot 허브 라즈베리 pi 송신 데이터 toocloud 라즈베리 pi toocloud"
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
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="be9fc-104">라스베리 Pi tooAzure IoT Hub (Node.js) 연결</span><span class="sxs-lookup"><span data-stu-id="be9fc-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="be9fc-105">이 자습서에서는 먼저 라스베리 Pi Raspbian를 실행 하는 작업의 hello 기본 사항 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="be9fc-106">그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="be9fc-107">Windows 10 IoT Core 샘플에 대 한 이동 toohello [Windows 개발자 센터](http://www.windowsondevices.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="be9fc-108">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="be9fc-108">Don't have a kit yet?</span></span> <span data-ttu-id="be9fc-109">Hello 시도 [라스베리 Pi 3 에뮬레이터](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-109">Try hello [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="be9fc-110">또는 새 키트를 [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="be9fc-111">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="be9fc-111">What you do</span></span>

* <span data-ttu-id="be9fc-112">Raspberry Pi를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="be9fc-113">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-113">Create an IoT hub.</span></span>
* <span data-ttu-id="be9fc-114">IoT Hub에 Pi용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="be9fc-115">Pi toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="be9fc-116">만들면 라스베리 Pi tooan IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="be9fc-117">다음 BME280 센서에서 Pi toocollect 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="be9fc-118">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="be9fc-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="be9fc-119">What you learn</span></span>

* <span data-ttu-id="be9fc-120">어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="be9fc-121">어떻게 tooconnect BME280 센서와 Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="be9fc-122">어떻게 Pi에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="be9fc-123">어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="be9fc-124">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="be9fc-124">What you need</span></span>

![필요한 항목](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="be9fc-126">hello 라스베리 Pi 2 또는 라스베리 Pi 3 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="be9fc-127">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="be9fc-127">An active Azure subscription.</span></span> <span data-ttu-id="be9fc-128">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="be9fc-129">모니터, USB 키보드 및 마우스 tooPi 연결 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="be9fc-130">Windows 또는 Linux를 실행하는 Mac 또는 PC.</span><span class="sxs-lookup"><span data-stu-id="be9fc-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="be9fc-131">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="be9fc-131">An Internet connection.</span></span>
* <span data-ttu-id="be9fc-132">16GB 이상의 microSD 카드.</span><span class="sxs-lookup"><span data-stu-id="be9fc-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="be9fc-133">USB SD 어댑터 또는 microSD 카드 tooburn hello에 운영 체제 이미지 hello microSD 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="be9fc-134">Hello 6 피트 마이크로 USB 케이블을 5 v 2 amp 전원 공급 장치.</span><span class="sxs-lookup"><span data-stu-id="be9fc-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="be9fc-135">hello 다음 항목은 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="be9fc-135">hello following items are optional:</span></span>

* <span data-ttu-id="be9fc-136">조립된 Adafruit BME280 온도, 압력 및 습도 센서.</span><span class="sxs-lookup"><span data-stu-id="be9fc-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="be9fc-137">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="be9fc-137">A breadboard.</span></span>
* <span data-ttu-id="be9fc-138">F/M 점퍼 와이어 6개.</span><span class="sxs-lookup"><span data-stu-id="be9fc-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="be9fc-139">확산형 10mm LED.</span><span class="sxs-lookup"><span data-stu-id="be9fc-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="be9fc-140">Hello 코드 샘플 지원 센서 데이터를 시뮬레이션 하기 때문에 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="be9fc-141">Raspberry Pi 설치</span><span class="sxs-lookup"><span data-stu-id="be9fc-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="be9fc-142">Pi에 대 한 hello Raspbian 운영 체제를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="be9fc-143">Hello microSD 카드 hello Raspbian 이미지의 설치를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="be9fc-144">Raspbian을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="be9fc-145">[픽셀을 Raspbian 제시 다운로드](https://www.raspberrypi.org/downloads/raspbian/) (hello.zip 파일).</span><span class="sxs-lookup"><span data-stu-id="be9fc-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="be9fc-146">Hello Raspbian 이미지 tooa 컴퓨터의 폴더에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="be9fc-147">Raspbian toohello microSD 카드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="be9fc-148">[다운로드 및 설치 hello Etcher SD 카드 버너 유틸리티](https://etcher.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="be9fc-149">Etcher를 실행 하 고 1 단계에서 압축을 푼 hello Raspbian 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="be9fc-150">Hello microSD 카드 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-150">Select hello microSD card drive.</span></span> <span data-ttu-id="be9fc-151">Etcher 선택 했을 수 이미 hello 올바른 드라이브 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="be9fc-152">플래시 tooinstall Raspbian toohello microSD 카드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="be9fc-153">설치가 완료 되 면 hello microSD 카드를 컴퓨터에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="be9fc-154">되므로 안전 tooremove hello microSD 카드 직접 Etcher를 꺼냅니다. 자동으로 또는 완료 되 면 hello microSD 카드 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="be9fc-155">Pi에 hello microSD 카드를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="be9fc-156">SSH 및 I2C를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="be9fc-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="be9fc-157">Pi toohello 모니터, 키보드 및 마우스 연결 Pi 시작한 다음 Raspbian 사용 하 여 로그인 `pi` hello. 사용자 이름 및 `raspberry` hello 암호와 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="be9fc-158">Hello 라즈베리 아이콘 클릭 > **기본 설정** > **라스베리 Pi 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![hello Raspbian 기본 설정 메뉴](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="be9fc-160">Hello에 **인터페이스** 탭, 설정 **I2C** 및 **SSH** 너무**사용**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="be9fc-161">없습니다 실제 센서 고 시뮬레이션 toouse 센서 데이터를 하는 경우이 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Raspberry Pi에서 I2C 및 SSH를 사용하도록 설정](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="be9fc-163">tooenable SSH 및 I2C에서 더 많은 참조 문서를 찾을 수 있습니다 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 및 [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="be9fc-164">Hello 센서 tooPi 연결</span><span class="sxs-lookup"><span data-stu-id="be9fc-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="be9fc-165">사용 하 여 hello breadboard 및 점퍼 와이어 tooconnect LED 및 BME280 tooPi 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="be9fc-166">Hello 센서를 설정 하지 않은 경우이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-166">If you don’t have hello sensor, skip this section.</span></span>

![hello 라스베리 Pi 및 센서 연결](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="be9fc-168">hello BME280 센서 온도 및 습도 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="be9fc-169">및 장치 및 hello 클라우드 간의 통신 이면 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="be9fc-170">센서 핀에 대 한 다음 배선 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="be9fc-171">시작(센서 및 LED)</span><span class="sxs-lookup"><span data-stu-id="be9fc-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="be9fc-172">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="be9fc-172">End (Board)</span></span>            | <span data-ttu-id="be9fc-173">케이블 색</span><span class="sxs-lookup"><span data-stu-id="be9fc-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="be9fc-174">VDD(5G 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="be9fc-175">3.3V PWR(1 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="be9fc-176">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="be9fc-176">White cable</span></span>   |
| <span data-ttu-id="be9fc-177">GND(7G 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="be9fc-178">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-178">GND (Pin 6)</span></span>            | <span data-ttu-id="be9fc-179">갈색 케이블</span><span class="sxs-lookup"><span data-stu-id="be9fc-179">Brown cable</span></span>   |
| <span data-ttu-id="be9fc-180">SCK(8G 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="be9fc-181">I2C1 SDA(3 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="be9fc-182">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="be9fc-182">Orange cable</span></span>  |
| <span data-ttu-id="be9fc-183">SDI(10G 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="be9fc-184">I2C1 SCL(5 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="be9fc-185">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="be9fc-185">Red cable</span></span>     |
| <span data-ttu-id="be9fc-186">LED VDD(18F 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="be9fc-187">GPIO 24(18 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="be9fc-188">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="be9fc-188">White cable</span></span>   |
| <span data-ttu-id="be9fc-189">LED GND(17F 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="be9fc-190">GND(20 핀)</span><span class="sxs-lookup"><span data-stu-id="be9fc-190">GND (Pin 20)</span></span>           | <span data-ttu-id="be9fc-191">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="be9fc-191">Black cable</span></span>   |

<span data-ttu-id="be9fc-192">Tooview 클릭 [라스베리 Pi 2 & 3 Pin 매핑](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) 참조할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="be9fc-193">성공적으로 연결한 후 BME280 tooyour 라스베리 Pi와 같은 이미지 아래 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi와 BME280 연결](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="be9fc-195">Pi toohello 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="be9fc-195">Connect Pi toohello network</span></span>

<span data-ttu-id="be9fc-196">Pi hello 마이크로 USB 케이블 및 hello 전원 공급 장치를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="be9fc-197">사용 하 여 hello 이더넷 케이블 tooconnect Pi tooyour 유선 네트워크 또는 hello에 따라 [hello 라스베리 Pi Foundation의에서 지침에 따라](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 무선 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="be9fc-198">Tootake hello 메모 필요 하면 Pi에 대 한 toohello 성공적으로 연결 된 네트워크를 수행한 후 [프로그램 Pi의 IP 주소](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![연결 된 toowired 네트워크](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="be9fc-200">Pi 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="be9fc-201">예를 들어 컴퓨터는 연결 된 tooa 무선 네트워크 Pi는 유선 네트워크 연결된 tooa를 동안 표시 될 수 없습니다 hello IP hello devdisco 출력에는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="be9fc-202">Pi에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="be9fc-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="be9fc-203">샘플 응용 프로그램을 복제 하 고 hello 필수 구성 요소 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="be9fc-204">Hello 호스트 컴퓨터 tooconnect tooyour 라스베리 Pi에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
    - <span data-ttu-id="be9fc-205">Windows용 [PuTTY](http://www.putty.org/)</span><span class="sxs-lookup"><span data-stu-id="be9fc-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="be9fc-206">Pi tooconnect의 hello IP 주소가 필요한 SSH를 통해 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-206">You need hello IP address of your Pi tooconnect it via SSH.</span></span>
    - <span data-ttu-id="be9fc-207">hello 기본 제공 SSH 클라이언트 Ubuntu 또는 macOS에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-207">hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="be9fc-208">실행 수 하면 `ssh pi@<ip address of pi>` tooconnect SSH 통해 Pi 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-208">You might need run `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="be9fc-209">hello 기본 사용자 이름은 `pi` , hello 암호도 `raspberry`합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-209">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="be9fc-210">Node.js 및 NPM tooyour Pi를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-210">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="be9fc-211">먼저 다음 명령을 hello로는 Node.js 버전을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-211">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="be9fc-212">Hello 버전 4.x 보다 낮습니다. 하거나 프로그램 원주율 없습니다 Node.js hello 명령 tooinstall 다음 실행 또는 Node.js를 업데이트 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-212">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="be9fc-213">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="be9fc-214">다음 명령을 hello에서 모든 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-214">Install all packages by hello following command.</span></span> <span data-ttu-id="be9fc-215">Azure IoT 장치 SDK, BME280 센서 라이브러리 및 배선 Pi 라이브러리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="be9fc-216">걸릴 수 있습니다 몇 분 toofinish이 설치 프로세스 denpening 네트워크 연결에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-216">It might take several minutes toofinish this installation process denpening on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="be9fc-217">Hello 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="be9fc-217">Configure hello sample application</span></span>

1. <span data-ttu-id="be9fc-218">Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-218">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Config 파일](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="be9fc-220">이 파일에는 사용자가 구성할 수 있는 두 개 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="be9fc-221">hello 먼저 하나는 `interval`, toocloud 전송 하는 두 개의 메시지 간의 hello 시간 간격을 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-221">hello first one is `interval`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="be9fc-222">두 번째 식 hello `simulatedData`, 값은 부울 값 여부 toouse 센서 데이터를 시뮬레이션 하는 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-222">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="be9fc-223">경우 있습니다 **hello 센서 없는**설정 hello `simulatedData` 너무 값`true` toomake hello 샘플 응용 프로그램을 만들고 시뮬레이션된 센서 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-223">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="be9fc-224">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="be9fc-225">Hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="be9fc-225">Run hello sample application</span></span>

1. <span data-ttu-id="be9fc-226">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-226">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="be9fc-227">하면 복사-붙여넣기 hello 장치 연결 문자열 hello 작은따옴표에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-227">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="be9fc-228">Hello 다음 출력에서는 hello 센서 데이터와 hello 전송 된 메시지를 tooyour IoT 허브는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-228">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![출력-라스베리 Pi tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="be9fc-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be9fc-230">Next steps</span></span>

<span data-ttu-id="be9fc-231">샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="be9fc-231">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]