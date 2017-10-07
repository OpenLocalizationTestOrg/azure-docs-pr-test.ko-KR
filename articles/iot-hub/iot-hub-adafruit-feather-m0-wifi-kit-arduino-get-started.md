---
title: "M0 toocloud: 페더 M0 WiFi tooAzure IoT 허브 연결 | Microsoft Docs"
description: "자세한 내용은 방법 tooset 및이 자습서에서는 Adafruit 페더 M0 WiFi tooAzure IoT Hub toosend 데이터 toohello Azure 클라우드 플랫폼을 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="464d7-103">Adafruit 페더 M0 WiFi tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280, Feather M0 WiFi 및 IoT Hub 간의 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="464d7-105">이 자습서에서는 먼저 Arduino 보드와 작업의 hello 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="464d7-106">그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="464d7-107">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="464d7-107">What you do</span></span>

<span data-ttu-id="464d7-108">만들면 Adafruit 페더 M0 WiFi tooan IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="464d7-109">다음는 BME280에서 M0 WiFi toocollect hello 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="464d7-110">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="464d7-111">학습 내용</span><span class="sxs-lookup"><span data-stu-id="464d7-111">What you learn</span></span>

* <span data-ttu-id="464d7-112">어떻게 toocreate IoT hub 페더 M0 WiFi에 대 한 장치를 등록 하 고</span><span class="sxs-lookup"><span data-stu-id="464d7-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="464d7-113">어떻게 tooconnect 페더 M0 WiFi hello 센서와 사용자의 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="464d7-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="464d7-114">어떻게 페더 M0 WiFi에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터</span><span class="sxs-lookup"><span data-stu-id="464d7-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="464d7-115">Toosend 센서 데이터 tooyour IoT 허브를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="464d7-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="464d7-116">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="464d7-116">What you need</span></span>

![hello 자습서에 필요한 부품](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="464d7-118">toocomplete 페더 M0 WiFi 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="464d7-119">hello 페더 M0 WiFi 보드</span><span class="sxs-lookup"><span data-stu-id="464d7-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="464d7-120">마이크로 USB tooType A USB 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="464d7-121">Hello 개발 환경에 대 한 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="464d7-122">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="464d7-122">An active Azure subscription.</span></span> <span data-ttu-id="464d7-123">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="464d7-124">Windows 또는 Ubuntu를 실행하는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="464d7-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="464d7-125">페더 M0 WiFi tooconnect에 대 한 무선 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="464d7-126">인터넷 연결 toodownload hello 구성 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="464d7-127">[Arduino IDE](https://www.arduino.cc/en/main/software) 버전 1.6.8 이상</span><span class="sxs-lookup"><span data-stu-id="464d7-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="464d7-128">이전 버전 hello Azure IoT Hub 라이브러리와 함께 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="464d7-129">센서를 설정 하지 않은 경우 hello 다음 항목은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="464d7-130">시뮬레이션 된 센서 데이터를 사용 하 여 hello 옵션도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="464d7-131">BME280 온도 및 습도 센서</span><span class="sxs-lookup"><span data-stu-id="464d7-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="464d7-132">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="464d7-132">A breadboard</span></span>
* <span data-ttu-id="464d7-133">M/M 점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="464d7-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="464d7-134">페더 M0 WiFi hello 센서 및 컴퓨터를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="464d7-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="464d7-135">이 섹션에서는 hello 센서 tooyour 보드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="464d7-136">그런 다음 나중에 사용할 장치 tooyour 컴퓨터에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="464d7-137">DHT22 온도 및 습도 센서 tooFeather M0 WiFi에 연결</span><span class="sxs-lookup"><span data-stu-id="464d7-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="464d7-138">Hello breadboard 및 점퍼 와이어 toomake hello 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="464d7-139">센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![연결 참조](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="464d7-141">센서 핀에 대 한 다음 배선 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="464d7-142">시작(센서)</span><span class="sxs-lookup"><span data-stu-id="464d7-142">Start (sensor)</span></span>           | <span data-ttu-id="464d7-143">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="464d7-143">End (board)</span></span>            | <span data-ttu-id="464d7-144">케이블 색</span><span class="sxs-lookup"><span data-stu-id="464d7-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="464d7-145">VDD(27A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="464d7-146">3V(3A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="464d7-147">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-147">Red cable</span></span>     |
| <span data-ttu-id="464d7-148">GND(29A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="464d7-149">GND(6A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="464d7-150">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-150">Black cable</span></span>   |
| <span data-ttu-id="464d7-151">SCK(30A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="464d7-152">SCK(12A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="464d7-153">노란색 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-153">Yellow cable</span></span>  |
| <span data-ttu-id="464d7-154">SDO(31A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="464d7-155">MI(14A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="464d7-156">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-156">White cable</span></span>   |
| <span data-ttu-id="464d7-157">SDI(32A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="464d7-158">M0(13A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="464d7-159">파란색 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-159">Blue cable</span></span>    |
| <span data-ttu-id="464d7-160">CS(33A 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="464d7-161">GPIO 5(15J 핀)</span><span class="sxs-lookup"><span data-stu-id="464d7-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="464d7-162">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="464d7-162">Orange cable</span></span>  |

<span data-ttu-id="464d7-163">자세한 내용은 [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all)(Adafruit BME280 습도 + 기압 + 온도 센서 혁신 세션) 및 [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts)(Adafruit Feather M0 WiFi 핀 배열)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="464d7-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="464d7-164">이제 Feather M0 WiFi를 작동 센서와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![DHT22를 Feather Huzzah와 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="464d7-166">페더 M0 WiFi tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="464d7-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="464d7-167">표시 된 것 처럼 hello 마이크로 USB tooType USB 케이블 tooconnect 페더 M0 WiFi tooyour 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![페더 Huzzah tooyour 컴퓨터 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="464d7-169">직렬 포트 권한 추가(Ubuntu만 해당)</span><span class="sxs-lookup"><span data-stu-id="464d7-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="464d7-170">Ubuntu를 사용 하는 경우 했는지 확인 hello 권한을 toooperate에 hello USB 포트의 페더 M0 WiFi 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="464d7-171">tooadd 직렬 포트 사용 권한을 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="464d7-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="464d7-172">터미널 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="464d7-173">Hello 다음 출력 중 하나를 가져오는:</span><span class="sxs-lookup"><span data-stu-id="464d7-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="464d7-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="464d7-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="464d7-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="464d7-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="464d7-176">Hello 출력 알 수 있듯이 `uucp` 또는 `dialout` hello USB 포트 hello 그룹 소유자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="464d7-177">tooadd hello 사용자 toohello 그룹, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="464d7-178">Hello 그룹 소유자 이름 hello 이전 단계에서 가져온 `<group-owner-name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="464d7-179">Ubuntu 사용자 이름은 `<username>`입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="464d7-180">Hello 변경 tooappear에 대 한 로그 Ubuntu 아웃 한 다음 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="464d7-181">센서 데이터를 수집 하 고 tooyour IoT hub 보내기</span><span class="sxs-lookup"><span data-stu-id="464d7-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="464d7-182">이 섹션에서는 Feather M0 WiFi에서 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="464d7-183">hello 샘플 응용 프로그램을 사용 하면 hello 페더 M0 WiFi에 led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="464d7-184">그런 다음 hello 온도 보냅니다 및 IoT 허브에서 hello BME280 센서 tooyour 습도 데이터 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="464d7-185">GitHub에서 hello 샘플 응용 프로그램을 가져오고 hello Arduino IDE를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="464d7-186">hello 샘플 응용 프로그램은 GitHub에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="464d7-187">GitHub에서 hello 샘플 응용 프로그램을 포함 하는 hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="464d7-188">tooclone hello 샘플 리포지토리 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="464d7-189">명령 프롬프트 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="464d7-190">저장 된 hello 샘플 응용 프로그램 toobe 저장할 tooa 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="464d7-191">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="464d7-192">Hello Arduino IDE에서에서 페더 M0 WiFi에 대 한 hello 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="464d7-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="464d7-193">Hello 샘플 응용 프로그램 저장 된 hello 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="464d7-194">Hello Arduino IDE의에서 hello 응용 프로그램 폴더에 hello app.ino 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Arduino IDE에서 열린 hello 샘플 응용 프로그램](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="464d7-196">클릭 **파일** > **기본 설정** (Windows/Linux) 또는 **Arduino** > **기본 설정** (Mac) 및 복사 하 고 hello에 아래 hello 링크 붙여넣기 **보드 관리자 Url을 추가로** hello Arduino IDE 기본 설정 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="464d7-197">클릭 **도구** > **보드** > **보드 관리자**, hello를 설치한 다음 `Arduino SAMD Boards` 버전 `1.6.2` 이상.</span><span class="sxs-lookup"><span data-stu-id="464d7-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="464d7-198">그런 다음 같은 창 hello, 설치 `Adafruit SAMD Boards` tooadd hello 보드 파일 정의 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![hello esp8266 패키지가 설치 되어](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="464d7-200">**도구** > **보드** > **Adafruit M0 WiFi**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="464d7-201">드라이버를 설치합니다(Windows만 해당).</span><span class="sxs-lookup"><span data-stu-id="464d7-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="464d7-202">페더 M0 WiFi에 연결 하는 경우에 드라이버 tooinstall을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="464d7-203">클릭 [hello 웹 페이지에서 다운로드 링크 hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello 드라이버 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="464d7-204">원하는 hello 단계 tooinstall hello 드라이버를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="464d7-205">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="464d7-205">Install necessary libraries</span></span>

1. <span data-ttu-id="464d7-206">Hello Arduino IDE, 클릭 **스케치** > **라이브러리 포함** > **관리 라이브러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="464d7-207">다음 라이브러리 이름을 하나씩 hello에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="464d7-208">검색한 각 라이브러리에 대해 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="464d7-209">수동으로 `Adafruit_WINC1500`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="464d7-210">너무 이동[이 웹 사이트](https://github.com/adafruit/Adafruit_WINC1500) 클릭 **클론 또는 다운로드** > **zip 파일 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="464d7-211">프로그램 Arduino IDE에서 이동 하 여 너무**스케치** > **라이브러리 포함** > **.zip 라이브러리 추가** hello zip 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="464d7-212">실제 BME280 센서 없는 경우 hello 샘플 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="464d7-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="464d7-213">실제 BME280 센서를 설정 하지 않은 경우 hello 샘플 응용 프로그램 데이터를 온도 및 습도 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="464d7-214">tooset hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="464d7-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="464d7-215">열기 hello `config.h` hello에 대 한 파일 `app` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="464d7-216">다음 코드 줄을 hello를 찾아 hello 값에서 변경 `false` 너무`true`:</span><span class="sxs-lookup"><span data-stu-id="464d7-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 구성 합니다.](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="464d7-218">Hello 파일을 저장 `Control-s`합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="464d7-219">Hello 샘플 응용 프로그램 tooFeather M0 WiFi 배포</span><span class="sxs-lookup"><span data-stu-id="464d7-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="464d7-220">Hello Arduino IDE, 클릭 **도구** > **포트**, 페더 M0 WiFi에 대 한 hello 직렬 포트를 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="464d7-221">클릭 **스케치** > **업로드** toobuild hello 샘플 응용 프로그램 tooFeather M0 WiFi를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="464d7-222">자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="464d7-222">Enter your credentials</span></span>

<span data-ttu-id="464d7-223">Hello 업로드 성공적으로 완료 되 면 이러한 단계 tooenter 자격 증명를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="464d7-224">Hello Arduino IDE, 클릭 **도구** > **직렬 모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="464d7-225">Hello 직렬 모니터 창의 hello 오른쪽 아래에서 선택 **줄 닫는** hello 왼쪽 hello 드롭 다운 목록에서.</span><span class="sxs-lookup"><span data-stu-id="464d7-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="464d7-226">선택 **115200 보드** hello 드롭 다운 목록에서 오른쪽 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="464d7-227">Hello 위쪽에 hello 입력된 상자에 hello 인 경우 다음 정보를 입력 한 클릭 tooprovide 요청 **보낼**:</span><span class="sxs-lookup"><span data-stu-id="464d7-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="464d7-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="464d7-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="464d7-229">Wi-Fi 암호</span><span class="sxs-lookup"><span data-stu-id="464d7-229">Wi-Fi password</span></span>
   * <span data-ttu-id="464d7-230">장치 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="464d7-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="464d7-231">hello 자격 증명 정보는 hello 페더 M0 WiFi EEPROM에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="464d7-232">Hello 페더 M0 WiFi 보드에 hello reset 단추를 누르면 hello 샘플 응용 프로그램 묻는 tooerase hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="464d7-233">입력 `Y` tooerase hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="464d7-234">Tooprovide hello 정보를 두 번째로 묻는 합니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="464d7-235">Hello 예제 응용 프로그램이 성공적으로 실행 되 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="464d7-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="464d7-236">표시 되 면 hello 다음 hello 직렬 모니터 창에서 출력 hello 페더 M0 WiFi hello 샘플 응용 프로그램의 led가 깜박입니다.이 성공적으로 실행 되 고:</span><span class="sxs-lookup"><span data-stu-id="464d7-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Arduino IDE의 최종 출력](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="464d7-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="464d7-238">Next steps</span></span>

<span data-ttu-id="464d7-239">페더 M0 WiFi tooyour IoT 허브를 연결 하 고 캡처한 hello 센서 데이터 tooyour IoT 허브를 전송 했습니다.</span><span class="sxs-lookup"><span data-stu-id="464d7-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

