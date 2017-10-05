---
title: "ESP8266에서 클라우드로 - Sparkfun ESP8266 Thing Dev를 Azure IoT Hub에 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure 클라우드 플랫폼으로 데이터를 보내기 위해 Sparkfun ESP8266 Thing Dev를 설정하고 해당 Azure IoT Hub에 연결하는 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="7e855-103">Sparkfun ESP8266 Thing Dev를 클라우드의 Azure IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="7e855-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, Thing Dev 및 IoT Hub 간 연결](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="7e855-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="7e855-105">What you will do</span></span>

<span data-ttu-id="7e855-106">만들게 될 IoT Hub에 Sparkfun ESP8266 Thing Dev를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="7e855-107">그런 다음 ESP8266에서 응용 프로그램 예제를 실행하여 DHT22 센서로부터 온도 및 습도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="7e855-108">마지막으로, 이 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="7e855-109">다른 ESP8266 보드를 사용하는 경우에도 이러한 단계에 따라 IoT Hub에 계속 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="7e855-110">사용하는 ESP8266 보드에 따라 `LED_PIN`을 다시 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="7e855-111">예를 들어, AI-Thinker의 ESP8266을 사용하는 경우 `0`을 `2`로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="7e855-112">아직 키트가 없나요? [여기](http://azure.com/iotstarterkits)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="7e855-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7e855-113">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="7e855-113">What you will learn</span></span>

* <span data-ttu-id="7e855-114">IoT Hub를 만들고 Thing Dev에 대한 장치를 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="7e855-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="7e855-115">Thing Dev를 센서와 컴퓨터에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="7e855-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="7e855-116">Thing Dev에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법</span><span class="sxs-lookup"><span data-stu-id="7e855-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="7e855-117">IoT Hub로 센서 데이터를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="7e855-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="7e855-118">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="7e855-118">What you will need</span></span>

![이 자습서에 필요한 부품](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="7e855-120">이 작업을 완료하려면 Thing Dev 시작 키트에서 다음 부품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="7e855-121">Sparkfun ESP8266 Thing Dev 보드</span><span class="sxs-lookup"><span data-stu-id="7e855-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="7e855-122">Micro USB - A형 USB 케이블</span><span class="sxs-lookup"><span data-stu-id="7e855-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="7e855-123">개발 환경에는 다음 사항도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="7e855-124">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="7e855-124">An active Azure subscription.</span></span> <span data-ttu-id="7e855-125">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="7e855-126">Windows 또는 Ubuntu가 실행되는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="7e855-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="7e855-127">Sparkfun ESP8266 Thing Dev가 연결되는 무선 네트워크</span><span class="sxs-lookup"><span data-stu-id="7e855-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="7e855-128">구성 도구를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="7e855-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="7e855-129">[Arduino IDE](https://www.arduino.cc/en/main/software) 버전 1.6.8(이상) - 이전 버전은 AzureIoT 라이브러리에서 작동하지 않음</span><span class="sxs-lookup"><span data-stu-id="7e855-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="7e855-130">센서가 없는 경우 다음 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="7e855-131">시뮬레이션된 센서 데이터를 사용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="7e855-132">Adafruit DHT22 온도 및 습도 센서</span><span class="sxs-lookup"><span data-stu-id="7e855-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="7e855-133">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="7e855-133">A breadboard.</span></span>
* <span data-ttu-id="7e855-134">M/M 점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="7e855-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="7e855-135">ESP8266 Thing Dev를 센서와 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="7e855-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="7e855-136">DHT22 온도 및 습도 센서를 ESP8266 Thing Dev에 연결</span><span class="sxs-lookup"><span data-stu-id="7e855-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="7e855-137">다음과 같이 실험용 회로판과 점퍼 와이어를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="7e855-138">센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![연결 참조](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="7e855-140">센서 핀의 경우 다음 배선을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="7e855-141">시작(센서)</span><span class="sxs-lookup"><span data-stu-id="7e855-141">Start (Sensor)</span></span>           | <span data-ttu-id="7e855-142">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="7e855-142">End (Board)</span></span>           | <span data-ttu-id="7e855-143">케이블 색</span><span class="sxs-lookup"><span data-stu-id="7e855-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="7e855-144">VDD(27F 핀)</span><span class="sxs-lookup"><span data-stu-id="7e855-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="7e855-145">3V(8A 핀)</span><span class="sxs-lookup"><span data-stu-id="7e855-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="7e855-146">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="7e855-146">Red cable</span></span>     |
| <span data-ttu-id="7e855-147">데이터(28F 핀)</span><span class="sxs-lookup"><span data-stu-id="7e855-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="7e855-148">GPIO 2(9A 핀)</span><span class="sxs-lookup"><span data-stu-id="7e855-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="7e855-149">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="7e855-149">White cable</span></span>    |
| <span data-ttu-id="7e855-150">GND(30F 핀)</span><span class="sxs-lookup"><span data-stu-id="7e855-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="7e855-151">GND(7J 핀)</span><span class="sxs-lookup"><span data-stu-id="7e855-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="7e855-152">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="7e855-152">Black cable</span></span>   |


- <span data-ttu-id="7e855-153">자세한 내용은 [DHT22 센서 설정](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf)(영문) 및 [Sparkfun ESP8266 Thing Dev 사양](https://www.sparkfun.com/products/13711)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e855-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="7e855-154">이제 Sparkfun ESP8266 Thing Dev를 작동 센서와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![dht22와 ESP8266 Thing Dev 연결](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="7e855-156">Sparkfun ESP8266 Thing Dev를 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="7e855-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="7e855-157">다음과 같이 Micro USB - A형 USB 케이블을 사용하여 Sparkfun ESP8266 Thing Dev를 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![feather huzzah를 컴퓨터에 연결](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="7e855-159">직렬 포트 권한 추가 – Ubuntu만</span><span class="sxs-lookup"><span data-stu-id="7e855-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="7e855-160">Ubuntu를 사용하는 경우 일반 사용자에게 Sparkfun ESP8266 Thing Dev의 USB 포트에서 작동할 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="7e855-161">일반 사용자에 대한 직렬 포트 권한을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="7e855-162">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="7e855-163">다음 출력 중 하나가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="7e855-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="7e855-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="7e855-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="7e855-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="7e855-166">출력에서 `uucp` 또는 `dialout`이 USB 포트의 그룹 소유자 이름임을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="7e855-167">다음 명령을 실행하여 그룹에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="7e855-168">`<group-owner-name>`은 이전 단계에서 얻은 그룹 소유자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="7e855-169">`<username>`은 Ubuntu 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="7e855-170">변경 내용을 적용하려면 Ubuntu에서 로그아웃했다가 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="7e855-171">센서 데이터를 수집하여 IoT Hub에 보내기</span><span class="sxs-lookup"><span data-stu-id="7e855-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="7e855-172">이 섹션에서는 Sparkfun ESP8266 Thing Dev에 대한 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="7e855-173">샘플 응용 프로그램은 Sparkfun ESP8266 Thing Dev의 LED를 깜박이고 DHT22 센서에서 수집한 온도 및 습도 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="7e855-174">GitHub에서 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e855-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="7e855-175">샘플 응용 프로그램은 GitHub에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="7e855-176">GitHub에서 응용 프로그램 예제가 포함된 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="7e855-177">샘플 리포지토리를 복제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="7e855-178">명령 프롬프트 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="7e855-179">응용 프로그램 예제를 저장하려는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="7e855-180">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="7e855-181">Arduino IDE에 Sparkfun ESP8266 Thing Dev 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="7e855-182">응용 프로그램 예제가 저장된 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="7e855-183">Arduino IDE의 앱 폴더에서 app.ino 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![arduino ide에서 응용 프로그램 예제 열기](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="7e855-185">Arduino IDE에서 **파일** > **기본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="7e855-186">**기본 설정** 대화 상자에서 **Additional Boards Manager URLs**(추가 보드 관리자 URL) 텍스트 상자 옆에 있는 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="7e855-187">팝업 창에 다음 URL을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![arduino ide에서 패키지 url 가리키기](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="7e855-189">**기본 설정** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="7e855-190">**도구** > **보드** > **보드 관리자**를 클릭한 후 esp8266을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="7e855-191">ESP8266 버전 2.2.0 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![esp8266 패키지 설치됨](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="7e855-193">**도구** > **보드** > **Sparkfun ESP8266 Thing Dev**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="7e855-194">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="7e855-194">Install necessary libraries</span></span>

1. <span data-ttu-id="7e855-195">Arduino IDE에서 **스케치** > **라이브러리 포함** > **라이브러리 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="7e855-196">다음 라이브러리 이름을 하나씩 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-196">Search for the following library names one by one.</span></span> <span data-ttu-id="7e855-197">라이브러리를 찾을 때마다 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="7e855-198">실제 DHT22 센서가 없나요?</span><span class="sxs-lookup"><span data-stu-id="7e855-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="7e855-199">실제 DHT22 센서가 없는 경우 응용 프로그램 예제에서 온도 및 습도 데이터를 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="7e855-200">시뮬레이션된 데이터를 사용하도록 응용 프로그램 예제를 설정하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="7e855-201">`app` 폴더에서 `config.h` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="7e855-202">다음 코드 줄을 찾아 값을 `false`에서 `true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![시뮬레이션된 데이터를 사용하도록 응용 프로그램 예제 구성](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="7e855-204">`Control-s`로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="7e855-205">Sparkfun ESP8266 Thing Dev에 샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7e855-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="7e855-206">Arduino IDE에서 **도구** > **포트**를 차례로 클릭한 다음 Sparkfun ESP8266 Thing Dev에 대한 직렬 포트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="7e855-207">**스케치** > **업로드**를 차례로 클릭하여 샘플 응용 프로그램을 빌드하고 Sparkfun ESP8266 Thing Dev에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="7e855-208">macOS를 사용하는 경우 업로드하는 동안 다음 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="7e855-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="7e855-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="7e855-210">터미널 창을 열고 아래 작업을 완료하여 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="7e855-211">자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="7e855-211">Enter your credentials</span></span>

<span data-ttu-id="7e855-212">업로드를 성공적으로 완료했으면 단계에 따라 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="7e855-213">Arduino IDE에서 **도구** > **직렬 모니터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="7e855-214">직렬 모니터 창의 오른쪽 아래에서 드롭다운 목록 두 개를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="7e855-215">왼쪽 드롭다운 목록에서 **No line ending**(줄 끝 없음)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="7e855-216">오른쪽 드롭다운 목록에서 **115200 baud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="7e855-217">직렬 모니터 창 맨 위에 있는 입력 상자에 정보를 입력하라는 메시지가 표시되면 다음 정보를 입력한 후 **보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="7e855-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="7e855-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="7e855-219">Wi-Fi 암호</span><span class="sxs-lookup"><span data-stu-id="7e855-219">Wi-Fi password</span></span>
   * <span data-ttu-id="7e855-220">장치 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="7e855-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="7e855-221">자격 증명 정보는 Sparkfun ESP8266 Thing Dev의 EEPROM에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="7e855-222">Sparkfun ESP8266 Thing Dev 보드에서 리셋 단추를 클릭하면 샘플 응용 프로그램에서 정보를 지울지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="7e855-223">정보를 지우고 정보를 입력하라는 메시지를 다시 표시하도록 하려면 `Y`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="7e855-224">응용 프로그램 예제가 성공적으로 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="7e855-225">직렬 모니터 창에서 다음 출력이 표시되고 Sparkfun ESP8266 Thing Dev의 LED가 깜박이면 샘플 응용 프로그램이 성공적으로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![arduino ide에서 최종 출력](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="7e855-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e855-227">Next steps</span></span>

<span data-ttu-id="7e855-228">IoT Hub에 Sparkfun ESP8266 Thing Dev를 성공적으로 연결하고 캡처한 센서 데이터를 IoT Hub에 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="7e855-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
