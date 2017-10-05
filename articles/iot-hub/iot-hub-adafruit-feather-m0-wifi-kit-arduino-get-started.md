---
title: "M0에서 클라우드로: Feather M0 WiFi를 Azure IoT Hub에 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure 클라우드 플랫폼으로 데이터를 보내기 위해 Adafruit Feather M0 WiFi를 설정하고 Azure IoT Hub에 연결하는 방법을 알아봅니다."
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
ms.openlocfilehash: 0dcf6b46a4c6c743c713d24ce7844e801b278dcf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="ded36-103">Adafruit Feather M0 WiFi를 클라우드의 Azure IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="ded36-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280, Feather M0 WiFi 및 IoT Hub 간의 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="ded36-105">이 자습서에서는 Arduino 보드를 실행하는 작업의 기초부터 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="ded36-106">그런 다음 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)를 사용하여 장치를 클라우드에 원활하게 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ded36-107">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="ded36-107">What you do</span></span>

<span data-ttu-id="ded36-108">사용자가 만든 IoT Hub에 Adafruit Feather M0 WiFi를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="ded36-109">그런 다음 M0 WiFi에서 샘플 응용 프로그램을 실행하여 BME280에서 온도 및 습도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="ded36-110">마지막으로 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-110">Finally, you send the sensor data to your IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="ded36-111">학습 내용</span><span class="sxs-lookup"><span data-stu-id="ded36-111">What you learn</span></span>

* <span data-ttu-id="ded36-112">IoT Hub를 만들고 Feather M0 WiFi용 장치를 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="ded36-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="ded36-113">Feather M0 WiFi를 센서와 컴퓨터에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="ded36-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="ded36-114">Feather M0 WiFi에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법</span><span class="sxs-lookup"><span data-stu-id="ded36-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="ded36-115">IoT Hub로 센서 데이터를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="ded36-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ded36-116">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="ded36-116">What you need</span></span>

![이 자습서에 필요한 부품](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="ded36-118">이 작업을 완료하려면 Feather M0 WiFi 시작 키트에서 다음 부품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="ded36-119">Feather M0 WiFi 보드</span><span class="sxs-lookup"><span data-stu-id="ded36-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="ded36-120">Micro USB - A형 USB 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="ded36-121">또한 개발 환경에는 다음 사항도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="ded36-122">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="ded36-122">An active Azure subscription.</span></span> <span data-ttu-id="ded36-123">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ded36-124">Windows 또는 Ubuntu를 실행하는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="ded36-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="ded36-125">Feather M0 WiFi를 연결할 무선 네트워크</span><span class="sxs-lookup"><span data-stu-id="ded36-125">A wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="ded36-126">구성 도구를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="ded36-126">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="ded36-127">[Arduino IDE](https://www.arduino.cc/en/main/software) 버전 1.6.8 이상</span><span class="sxs-lookup"><span data-stu-id="ded36-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="ded36-128">이전 버전은 Azure IoT Hub 라이브러리와 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-128">Earlier versions don't work with the Azure IoT Hub library.</span></span>

<span data-ttu-id="ded36-129">센서가 없는 경우 다음 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-129">If you don’t have a sensor, the following items are optional.</span></span> <span data-ttu-id="ded36-130">시뮬레이트된 센서 데이터를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-130">You also have the option of using simulated sensor data:</span></span>

* <span data-ttu-id="ded36-131">BME280 온도 및 습도 센서</span><span class="sxs-lookup"><span data-stu-id="ded36-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="ded36-132">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="ded36-132">A breadboard</span></span>
* <span data-ttu-id="ded36-133">M/M 점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="ded36-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="ded36-134">Feather M0 WiFi를 센서와 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="ded36-134">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="ded36-135">이 섹션에서는 센서를 보드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-135">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="ded36-136">그런 다음 장치를 나중에 사용할 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-136">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="ded36-137">Feather M0 WiFi에 DHT22 온도 및 습도 센서 연결</span><span class="sxs-lookup"><span data-stu-id="ded36-137">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="ded36-138">브레드보드와 점퍼 와이어를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-138">Use the breadboard and jumper wires to make the connection.</span></span> <span data-ttu-id="ded36-139">센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![연결 참조](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="ded36-141">센서 핀의 경우 다음 배선을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-141">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="ded36-142">시작(센서)</span><span class="sxs-lookup"><span data-stu-id="ded36-142">Start (sensor)</span></span>           | <span data-ttu-id="ded36-143">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="ded36-143">End (board)</span></span>            | <span data-ttu-id="ded36-144">케이블 색</span><span class="sxs-lookup"><span data-stu-id="ded36-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="ded36-145">VDD(27A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="ded36-146">3V(3A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="ded36-147">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-147">Red cable</span></span>     |
| <span data-ttu-id="ded36-148">GND(29A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="ded36-149">GND(6A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="ded36-150">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-150">Black cable</span></span>   |
| <span data-ttu-id="ded36-151">SCK(30A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="ded36-152">SCK(12A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="ded36-153">노란색 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-153">Yellow cable</span></span>  |
| <span data-ttu-id="ded36-154">SDO(31A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="ded36-155">MI(14A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="ded36-156">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-156">White cable</span></span>   |
| <span data-ttu-id="ded36-157">SDI(32A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="ded36-158">M0(13A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="ded36-159">파란색 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-159">Blue cable</span></span>    |
| <span data-ttu-id="ded36-160">CS(33A 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="ded36-161">GPIO 5(15J 핀)</span><span class="sxs-lookup"><span data-stu-id="ded36-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="ded36-162">주황색 케이블</span><span class="sxs-lookup"><span data-stu-id="ded36-162">Orange cable</span></span>  |

<span data-ttu-id="ded36-163">자세한 내용은 [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all)(Adafruit BME280 습도 + 기압 + 온도 센서 혁신 세션) 및 [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts)(Adafruit Feather M0 WiFi 핀 배열)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ded36-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="ded36-164">이제 Feather M0 WiFi를 작동 센서와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![DHT22를 Feather Huzzah와 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="ded36-166">Feather M0 WiFi를 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="ded36-166">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="ded36-167">다음과 같이 Micro USB - A형 USB 케이블을 사용하여 Feather M0 WiFi를 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-167">Use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer, as shown:</span></span>

![Feather Huzzah를 컴퓨터에 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="ded36-169">직렬 포트 권한 추가(Ubuntu만 해당)</span><span class="sxs-lookup"><span data-stu-id="ded36-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="ded36-170">Ubuntu를 사용하는 경우 Feather M0 WiFi의 USB 포트에서 작동할 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-170">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="ded36-171">직렬 포트 권한을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-171">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="ded36-172">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-172">At a terminal, run the following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="ded36-173">다음 출력 중 하나가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-173">You get one of the following outputs:</span></span>

   * <span data-ttu-id="ded36-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="ded36-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="ded36-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="ded36-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="ded36-176">출력에서 `uucp` 또는 `dialout`이 USB 포트의 그룹 소유자 이름인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-176">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="ded36-177">그룹에 사용자를 추가하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-177">To add the user to the group, run the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="ded36-178">이전 단계에서 그룹 소유자 이름 `<group-owner-name>`을 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-178">In the previous step, you obtained the group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="ded36-179">Ubuntu 사용자 이름은 `<username>`입니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="ded36-180">변경 내용이 표시되도록 Ubuntu에서 로그아웃한 다음 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-180">For the change to appear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="ded36-181">센서 데이터를 수집하여 IoT Hub에 보내기</span><span class="sxs-lookup"><span data-stu-id="ded36-181">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="ded36-182">이 섹션에서는 Feather M0 WiFi에서 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="ded36-183">응용 프로그램 예제는 Feather M0 WiFi에서 LED가 깜박이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-183">The sample application makes the LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="ded36-184">그런 다음 BME280 센서에서 수집된 온도 및 습도 데이터를 IoT Hub에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-184">It then sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-the-arduino-ide"></a><span data-ttu-id="ded36-185">GitHub에서 응용 프로그램 예제를 가져오고 Arduino IDE 준비</span><span class="sxs-lookup"><span data-stu-id="ded36-185">Get the sample application from GitHub and prepare the Arduino IDE</span></span>

<span data-ttu-id="ded36-186">샘플 응용 프로그램은 GitHub에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-186">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="ded36-187">GitHub에서 응용 프로그램 예제가 포함된 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-187">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="ded36-188">샘플 리포지토리를 복제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-188">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="ded36-189">명령 프롬프트 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="ded36-190">응용 프로그램 예제를 저장하려는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-190">Go to a folder where you want the sample application to be stored.</span></span>
3. <span data-ttu-id="ded36-191">다음 명령 실행:</span><span class="sxs-lookup"><span data-stu-id="ded36-191">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-the-package-for-feather-m0-wifi-in-the-arduino-ide"></a><span data-ttu-id="ded36-192">Arduino IDE에 Feather M0 WiFi 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="ded36-192">Install the package for Feather M0 WiFi in the Arduino IDE</span></span>

1. <span data-ttu-id="ded36-193">응용 프로그램 예제가 저장된 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-193">Open the folder where the sample application is stored.</span></span>

2. <span data-ttu-id="ded36-194">Arduino IDE의 앱 폴더에서 app.ino 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-194">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Arduino IDE에서 샘플 응용 프로그램 열기](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="ded36-196">**파일** > **기본 설정**(Windows/Linux) 또는 **Arduino** > **환경설정**(Mac)을 클릭하고 아래 링크를 복사하여 Arduino IDE 기본 설정의 **Additional Boards Manager URLs**(추가 보드 관리자 URL) 옵션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste the link below into the **Additional Boards Manager URLs** option in the Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="ded36-197">**도구** > **보드** > **보드 관리자**를 클릭한 다음 `Arduino SAMD Boards` 버전 `1.6.2` 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-197">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="ded36-198">그런 다음 같은 창에서 `Adafruit SAMD Boards` 패키지를 설치하여 보드 파일 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-198">Then in the same window, install `Adafruit SAMD Boards` package to add the board file definitions.</span></span>

   ![esp8266 패키지가 설치됨](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="ded36-200">**도구** > **보드** > **Adafruit M0 WiFi**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="ded36-201">드라이버를 설치합니다(Windows만 해당).</span><span class="sxs-lookup"><span data-stu-id="ded36-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="ded36-202">Feather M0 WiFi를 연결하면 드라이버를 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-202">When you plug in Feather M0 WiFi, you might need to install a driver.</span></span> <span data-ttu-id="ded36-203">[웹 페이지의 다운로드 링크](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe)를 클릭하여 드라이버 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-203">Click [the download link on the webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the driver installer.</span></span> <span data-ttu-id="ded36-204">단계에 따라 원하는 드라이버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-204">Follow the steps to install the drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="ded36-205">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="ded36-205">Install necessary libraries</span></span>

1. <span data-ttu-id="ded36-206">Arduino IDE에서 **스케치** > **라이브러리 포함** > **라이브러리 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-206">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="ded36-207">다음 라이브러리 이름을 하나씩 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-207">Search for the following library names one by one.</span></span> <span data-ttu-id="ded36-208">검색한 각 라이브러리에 대해 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="ded36-209">수동으로 `Adafruit_WINC1500`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="ded36-210">[이 웹 사이트](https://github.com/adafruit/Adafruit_WINC1500)로 이동하고 **Clone or download**(복제 또는 다운로드) > **Download ZIP**(ZIP 다운로드)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-210">Go to [this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="ded36-211">그런 다음 Arduino IDE에서 **Sketch**(스케치) > **Include Library**(라이브러리 포함) > **Add .zip Library**(.zip 라이브러리 추가)로 이동하고 zip 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-211">Then in your Arduino IDE, go to **Sketch** > **Include Library** > **Add .zip Library** and add the zip file.</span></span>

### <a name="use-the-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="ded36-212">실제 BME280 센서가 없는 경우 응용 프로그램 예제 사용</span><span class="sxs-lookup"><span data-stu-id="ded36-212">Use the sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="ded36-213">실제 BME280 센서가 없는 경우 응용 프로그램 예제에서 온도 및 습도 데이터를 시뮬레이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-213">If you don’t have a real BME280 sensor, the sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="ded36-214">시뮬레이션된 데이터를 사용하도록 샘플 응용 프로그램을 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-214">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="ded36-215">`app` 폴더에서 `config.h` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-215">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="ded36-216">다음 코드 줄을 찾아 값을 `false`에서 `true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-216">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![시뮬레이션된 데이터를 사용하도록 샘플 응용 프로그램 구성](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="ded36-218">`Control-s`로 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-218">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="ded36-219">Feather M0 WiFi에 샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="ded36-219">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="ded36-220">Arduino IDE에서 **도구** > **포트**를 클릭한 후 Feather M0 WiFi에 대한 직렬 포트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-220">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="ded36-221">**스케치** > **업로드**를 클릭하여 샘플 응용 프로그램을 빌드하고 Feather M0 WiFi에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-221">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="ded36-222">자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="ded36-222">Enter your credentials</span></span>

<span data-ttu-id="ded36-223">업로드를 성공적으로 완료했으면 다음 단계에 따라 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-223">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="ded36-224">Arduino IDE에서 **도구** > **직렬 모니터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-224">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="ded36-225">직렬 모니터 창의 오른쪽 아래 모서리에서 왼쪽에 있는 드롭다운 목록에서 **No line ending**(줄 끝 없음)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-225">In the lower-right corner of the serial monitor window, select **No line ending** in the drop-down list on the left.</span></span>
3. <span data-ttu-id="ded36-226">오른쪽에 있는 드롭다운 목록에서 **115200 baud**(115200보드)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-226">Select **115200 baud** in the drop-down list on the right.</span></span>
4. <span data-ttu-id="ded36-227">위쪽에 있는 입력 상자에 다음 정보를 입력하고(제공하라는 메시지가 표시되는 경우) **Send**(보내기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-227">In the input box at the top, enter the following information if you're asked to provide it, and click **Send**:</span></span>

   * <span data-ttu-id="ded36-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="ded36-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="ded36-229">Wi-Fi 암호</span><span class="sxs-lookup"><span data-stu-id="ded36-229">Wi-Fi password</span></span>
   * <span data-ttu-id="ded36-230">장치 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="ded36-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="ded36-231">자격 증명 정보는 Feather M0 WiFi의 EEPROM에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-231">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="ded36-232">Feather M0 WiFi 보드의 리셋 단추를 클릭하면 샘플 응용 프로그램에서 정보를 지울 것인지 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-232">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="ded36-233">`Y`를 입력하여 정보를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-233">Enter `Y` to erase the information.</span></span> <span data-ttu-id="ded36-234">정보를 다시 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-234">You're asked to provide the information a second time.</span></span>

### <a name="verify-that-the-sample-application-is-running-successfully"></a><span data-ttu-id="ded36-235">응용 프로그램 예제가 실행되고 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="ded36-235">Verify that the sample application is running successfully</span></span>

<span data-ttu-id="ded36-236">직렬 모니터 창에 다음 출력이 표시되고 Feather M0 WiFi의 LED가 깜박이면 응용 프로그램 예제가 실행되고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-236">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully:</span></span>

![Arduino IDE의 최종 출력](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="ded36-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ded36-238">Next steps</span></span>

<span data-ttu-id="ded36-239">IoT Hub에 Feather M0 WiFi를 연결하고 캡처된 센서 데이터를 IoT Hub로 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="ded36-239">You have successfully connected Feather M0 WiFi to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

