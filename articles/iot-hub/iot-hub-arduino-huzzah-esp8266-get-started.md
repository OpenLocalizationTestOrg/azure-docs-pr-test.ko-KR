---
title: "ESP8266에서 클라우드로 - Feather HUZZAH ESP8266을 Azure IoT Hub에 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure 클라우드 플랫폼으로 데이터를 보내기 위해 Adafruit Feather HUZZAH ESP8266를 설정하고 해당 Azure IoT Hub에 연결하는 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="53d2e-103">Adafruit Feather HUZZAH ESP8266을 클라우드의 Azure IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="53d2e-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, Feather HUZZAH ESP8266 및 IoT Hub 간 연결](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="53d2e-105">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="53d2e-105">What you do</span></span>


<span data-ttu-id="53d2e-106">사용자가 만든 IoT Hub에 Adafruit Feather HUZZAH ESP8266을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="53d2e-107">그런 다음 ESP8266에서 샘플 응용 프로그램을 실행하여 DHT22 센서로부터 온도 및 습도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="53d2e-108">마지막으로 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="53d2e-109">다른 ESP8266 보드를 사용하는 경우에도 이러한 단계에 따라 IoT Hub에 계속 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="53d2e-110">사용하는 ESP8266 보드에 따라 `LED_PIN`을 다시 구성해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="53d2e-111">예를 들어 AI-Thinker의 ESP8266을 사용하는 경우 `0`을 `2`로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="53d2e-112">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="53d2e-112">Don't have a kit yet?</span></span> <span data-ttu-id="53d2e-113">[Azure 웹 사이트에서 가져오기](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="53d2e-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="53d2e-114">학습 내용</span><span class="sxs-lookup"><span data-stu-id="53d2e-114">What you learn</span></span>

* <span data-ttu-id="53d2e-115">IoT Hub를 만들고 장치를 Feather HUZZAH ESP8266으로 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="53d2e-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="53d2e-116">센서와 컴퓨터에 Feather HUZZAH ESP8266을 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="53d2e-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="53d2e-117">Feather HUZZAH ESP8266에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법</span><span class="sxs-lookup"><span data-stu-id="53d2e-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="53d2e-118">센서 데이터를 IoT Hub로 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="53d2e-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="53d2e-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="53d2e-119">What you need</span></span>

![이 자습서에 필요한 부품](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="53d2e-121">이 작업을 완료하려면 Feather HUZZAH ESP8266 시작 키트에서 다음 부품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="53d2e-122">Feather HUZZAH ESP8266 보드</span><span class="sxs-lookup"><span data-stu-id="53d2e-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="53d2e-123">Micro USB - A형 USB 케이블</span><span class="sxs-lookup"><span data-stu-id="53d2e-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="53d2e-124">또한 개발 환경에는 다음 사항도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="53d2e-125">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="53d2e-125">An active Azure subscription.</span></span> <span data-ttu-id="53d2e-126">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="53d2e-127">Windows 또는 Ubuntu가 실행되는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="53d2e-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="53d2e-128">Feather HUZZAH ESP8266을 연결할 무선 네트워크</span><span class="sxs-lookup"><span data-stu-id="53d2e-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="53d2e-129">구성 도구를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="53d2e-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="53d2e-130">[Arduino IDE](https://www.arduino.cc/en/main/software) 버전 1.6.8 이상</span><span class="sxs-lookup"><span data-stu-id="53d2e-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="53d2e-131">이전 버전은 Azure IoT 라이브러리에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="53d2e-132">센서가 없는 경우 다음 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="53d2e-133">시뮬레이션된 센서 데이터를 사용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="53d2e-134">Adafruit DHT22 온도 및 습도 센서</span><span class="sxs-lookup"><span data-stu-id="53d2e-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="53d2e-135">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="53d2e-135">A breadboard</span></span>
* <span data-ttu-id="53d2e-136">M/M 점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="53d2e-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="53d2e-137">Feather HUZZAH ESP8266을 센서와 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="53d2e-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="53d2e-138">이 섹션에서는 센서를 보드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="53d2e-139">그런 다음 장치를 나중에 사용할 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="53d2e-140">Feather HUZZAH ESP8266에 DHT22 온도 및 습도 센서 연결</span><span class="sxs-lookup"><span data-stu-id="53d2e-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="53d2e-141">다음과 같이 실험용 회로판과 점퍼 와이어를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="53d2e-142">센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![연결 참조](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="53d2e-144">센서 핀의 경우 다음 배선을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="53d2e-145">시작(센서)</span><span class="sxs-lookup"><span data-stu-id="53d2e-145">Start (Sensor)</span></span>           | <span data-ttu-id="53d2e-146">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="53d2e-146">End (Board)</span></span>           | <span data-ttu-id="53d2e-147">케이블 색</span><span class="sxs-lookup"><span data-stu-id="53d2e-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="53d2e-148">VDD(핀 31F)</span><span class="sxs-lookup"><span data-stu-id="53d2e-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="53d2e-149">3V(핀 58H)</span><span class="sxs-lookup"><span data-stu-id="53d2e-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="53d2e-150">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="53d2e-150">Red cable</span></span>     |
| <span data-ttu-id="53d2e-151">데이터(핀 32F)</span><span class="sxs-lookup"><span data-stu-id="53d2e-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="53d2e-152">GPIO 2(핀 46A)</span><span class="sxs-lookup"><span data-stu-id="53d2e-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="53d2e-153">파란색 케이블</span><span class="sxs-lookup"><span data-stu-id="53d2e-153">Blue cable</span></span>    |
| <span data-ttu-id="53d2e-154">GND(핀 34F)</span><span class="sxs-lookup"><span data-stu-id="53d2e-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="53d2e-155">GND(핀 56I)</span><span class="sxs-lookup"><span data-stu-id="53d2e-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="53d2e-156">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="53d2e-156">Black cable</span></span>   |

<span data-ttu-id="53d2e-157">자세한 내용은 [Adafruit DHT22 센서 설치](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor)(영문) 및 [Adafruit Feather HUZZAH Esp8266 핀 배열](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53d2e-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="53d2e-158">이제 Feather Huzzah ESP8266을 작동 센서와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![DHT22를 Feather Huzzah에 연결](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="53d2e-160">Feather HUZZAH ESP8266을 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="53d2e-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="53d2e-161">다음과 같이 Micro USB - A형 USB 케이블을 사용하여 Feather HUZZAH ESP8266을 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Feather Huzzah를 컴퓨터에 연결](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="53d2e-163">직렬 포트 권한 추가 – Ubuntu만</span><span class="sxs-lookup"><span data-stu-id="53d2e-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="53d2e-164">Ubuntu를 사용하는 경우 Feather HUZZAH ESP8266의 USB 포트에서 작동할 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="53d2e-165">직렬 포트 권한을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="53d2e-166">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="53d2e-167">다음 출력 중 하나가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="53d2e-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="53d2e-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="53d2e-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="53d2e-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="53d2e-170">출력에서 `uucp` 또는 `dialout`이 USB 포트의 그룹 소유자 이름인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="53d2e-171">다음 명령을 실행하여 그룹에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="53d2e-172">`<group-owner-name>`은 이전 단계에서 얻은 그룹 소유자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="53d2e-173">`<username>`은 Ubuntu 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="53d2e-174">Ubuntu에서 로그아웃한 다음 다시 로그인하면 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="53d2e-175">센서 데이터를 수집하여 IoT Hub에 보내기</span><span class="sxs-lookup"><span data-stu-id="53d2e-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="53d2e-176">이 섹션에서는 Feather HUZZAH ESP8266에 대한 응용 프로그램 예제를 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="53d2e-177">샘플 응용 프로그램은 Feather HUZZAH ESP8266의 LED를 깜박이고 DHT22 센서에서 수집된 온도 및 습도 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="53d2e-178">GitHub에서 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="53d2e-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="53d2e-179">샘플 응용 프로그램은 GitHub에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="53d2e-180">GitHub에서 응용 프로그램 예제가 포함된 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="53d2e-181">샘플 리포지토리를 복제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="53d2e-182">명령 프롬프트 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="53d2e-183">응용 프로그램 예제를 저장하려는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="53d2e-184">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="53d2e-185">Arduino IDE에 Feather HUZZAH ESP8266 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="53d2e-186">응용 프로그램 예제가 저장된 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="53d2e-187">Arduino IDE의 앱 폴더에서 app.ino 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Arduino IDE에서 샘플 응용 프로그램 열기](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="53d2e-189">Arduino IDE에서 **파일** > **기본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="53d2e-190">**기본 설정** 대화 상자에서 **Additional Boards Manager URLs**(추가 보드 관리자 URL) 상자 옆에 있는 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="53d2e-191">팝업 창에 다음 URL을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Arduino IDE에서 패키지 URL 가리키기](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="53d2e-193">**기본 설정** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="53d2e-194">**도구** > **보드** > **보드 관리자**를 클릭한 후 esp8266을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="53d2e-195">[보드 관리자]에서 ESP8266 2.2.0 이상 버전으로 설치되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![esp8266 패키지 설치됨](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="53d2e-197">**도구** > **보드** > **Adafruit HUZZAH ESP8266**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="53d2e-198">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="53d2e-198">Install necessary libraries</span></span>

1. <span data-ttu-id="53d2e-199">Arduino IDE에서 **스케치** > **라이브러리 포함** > **라이브러리 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="53d2e-200">다음 라이브러리 이름을 하나씩 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-200">Search for the following library names one by one.</span></span> <span data-ttu-id="53d2e-201">찾은 각 라이브러리에 대해 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="53d2e-202">실제 DHT22 센서가 없나요?</span><span class="sxs-lookup"><span data-stu-id="53d2e-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="53d2e-203">실제 DHT22 센서가 없는 경우 응용 프로그램 예제에서 온도 및 습도 데이터를 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="53d2e-204">시뮬레이션된 데이터를 사용하도록 샘플 응용 프로그램을 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="53d2e-205">`app` 폴더에서 `config.h` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="53d2e-206">다음 코드 줄을 찾아 값을 `false`에서 `true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![시뮬레이션된 데이터를 사용하도록 샘플 응용 프로그램 구성](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="53d2e-208">`Control-s`로 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="53d2e-209">Feather HUZZAH ESP8266에 응용 프로그램 예제 배포</span><span class="sxs-lookup"><span data-stu-id="53d2e-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="53d2e-210">Arduino IDE에서 **도구** > **포트**를 클릭한 후 Feather HUZZAH ESP8266에 대한 직렬 포트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="53d2e-211">**스케치** > **업로드**를 클릭하여 응용 프로그램 예제를 빌드하여 Feather HUZZAH ESP8266에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="53d2e-212">자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="53d2e-212">Enter your credentials</span></span>

<span data-ttu-id="53d2e-213">업로드를 성공적으로 완료했으면 다음 단계에 따라 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="53d2e-214">Arduino IDE에서 **도구** > **직렬 모니터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="53d2e-215">직렬 모니터 창의 오른쪽 아래 모서리에 있는 두 개의 드롭다운 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="53d2e-216">왼쪽 드롭다운 목록에서 **No line ending**(줄 끝 없음)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="53d2e-217">오른쪽 드롭다운 목록에서 **115200 baud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="53d2e-218">직렬 모니터 창 맨 위에 있는 입력 상자에 정보를 입력하라는 메시지가 표시되면 다음 정보를 입력한 후 **보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="53d2e-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="53d2e-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="53d2e-220">Wi-Fi 암호</span><span class="sxs-lookup"><span data-stu-id="53d2e-220">Wi-Fi password</span></span>
   * <span data-ttu-id="53d2e-221">장치 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="53d2e-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="53d2e-222">자격 증명 정보는 Feather HUZZAH ESP8266의 EEPROM에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="53d2e-223">Feather HUZZAH ESP8266 보드에서 리셋 단추를 클릭하면 샘플 응용 프로그램에서 정보를 지울 것인지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="53d2e-224">정보를 지우려면 `Y`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="53d2e-225">정보를 다시 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="53d2e-226">응용 프로그램 예제가 성공적으로 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="53d2e-227">직렬 모니터 창에 다음 출력이 표시되고 Feather HUZZAH ESP8266의 LED가 깜박이면 응용 프로그램 예제가 성공적으로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Arduino IDE의 최종 출력](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="53d2e-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53d2e-229">Next steps</span></span>

<span data-ttu-id="53d2e-230">IoT Hub에 Feather HUZZAH ESP8266를 성공적으로 연결하고 캡처한 센서 데이터를 IoT Hub로 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="53d2e-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

