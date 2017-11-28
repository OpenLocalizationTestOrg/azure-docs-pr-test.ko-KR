---
title: "aaaESP8266 toocloud-페더 HUZZAH ESP8266 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 방법을 toosetup 하 고이 자습서에서는 Adafruit 페더 HUZZAH ESP8266 tooAzure IoT 허브에 대 한 toosend 데이터 toohello Azure 클라우드 플랫폼을 연결 합니다."
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
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="e6c79-103">Adafruit 페더 HUZZAH ESP8266 tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, Feather HUZZAH ESP8266 및 IoT Hub 간 연결](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="e6c79-105">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="e6c79-105">What you do</span></span>


<span data-ttu-id="e6c79-106">만들면 Adafruit 페더 HUZZAH ESP8266 tooan IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="e6c79-107">다음 DHT22 센서에서 ESP8266 toocollect hello 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="e6c79-108">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e6c79-109">이러한 단계 tooconnect 다른 ESP8266 보드를 사용 하는 경우 여전히 따라 수 것 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="e6c79-110">Hello ESP8266 보드를 사용 하는, 따라 tooreconfigure hello를 할 수 있습니다 `LED_PIN`합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="e6c79-111">예를 들어 ESP8266 AI Thinker에서를 사용 하 여 변경할 수 있습니다에서 `0` 너무`2`합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="e6c79-112">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="e6c79-112">Don't have a kit yet?</span></span> <span data-ttu-id="e6c79-113">Hello에서 가져올 [Azure 웹 사이트](http://azure.com/iotstarterkits)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="e6c79-114">학습 내용</span><span class="sxs-lookup"><span data-stu-id="e6c79-114">What you learn</span></span>

* <span data-ttu-id="e6c79-115">어떻게 toocreate IoT hub 페더 HUZZAH ESP8266에 대 한 장치를 등록 하 고</span><span class="sxs-lookup"><span data-stu-id="e6c79-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="e6c79-116">어떻게 tooconnect 페더 HUZZAH ESP8266 hello 센서와 사용자의 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="e6c79-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="e6c79-117">어떻게 페더 HUZZAH ESP8266에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터</span><span class="sxs-lookup"><span data-stu-id="e6c79-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="e6c79-118">Toosend 센서 데이터 tooyour IoT 허브를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e6c79-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e6c79-119">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e6c79-119">What you need</span></span>

![hello 자습서에 필요한 부품](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="e6c79-121">toocomplete 페더 HUZZAH ESP8266 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="e6c79-122">hello 페더 HUZZAH ESP8266 보드</span><span class="sxs-lookup"><span data-stu-id="e6c79-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="e6c79-123">마이크로 USB tooType A USB 케이블</span><span class="sxs-lookup"><span data-stu-id="e6c79-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="e6c79-124">Hello 개발 환경에 대 한 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="e6c79-125">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e6c79-125">An active Azure subscription.</span></span> <span data-ttu-id="e6c79-126">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="e6c79-127">Windows 또는 Ubuntu가 실행되는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="e6c79-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="e6c79-128">무선 네트워크를 페더 HUZZAH ESP8266 tooconnect에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="e6c79-129">인터넷 연결 toodownload hello 구성 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="e6c79-130">[Arduino IDE](https://www.arduino.cc/en/main/software) 버전 1.6.8 이상</span><span class="sxs-lookup"><span data-stu-id="e6c79-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="e6c79-131">이전 버전 hello AzureIoT 라이브러리와 함께 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="e6c79-132">hello 다음 항목은 선택적 요소는 센서 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="e6c79-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="e6c79-133">시뮬레이션 된 센서 데이터를 사용 하 여 hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="e6c79-134">Adafruit DHT22 온도 및 습도 센서</span><span class="sxs-lookup"><span data-stu-id="e6c79-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="e6c79-135">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="e6c79-135">A breadboard</span></span>
* <span data-ttu-id="e6c79-136">M/M 점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="e6c79-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="e6c79-137">페더 HUZZAH ESP8266 hello 센서 및 컴퓨터를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="e6c79-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="e6c79-138">이 섹션에서는 hello 센서 tooyour 보드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="e6c79-139">그런 다음 나중에 사용할 장치 tooyour 컴퓨터에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="e6c79-140">DHT22 온도 및 습도 센서 tooFeather HUZZAH ESP8266 연결</span><span class="sxs-lookup"><span data-stu-id="e6c79-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="e6c79-141">다음과 같이 hello breadboard 및 점퍼 와이어 toomake hello 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="e6c79-142">센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![연결 참조](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="e6c79-144">센서 핀에 대 한 다음 배선 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="e6c79-145">시작(센서)</span><span class="sxs-lookup"><span data-stu-id="e6c79-145">Start (Sensor)</span></span>           | <span data-ttu-id="e6c79-146">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="e6c79-146">End (Board)</span></span>           | <span data-ttu-id="e6c79-147">케이블 색</span><span class="sxs-lookup"><span data-stu-id="e6c79-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="e6c79-148">VDD(핀 31F)</span><span class="sxs-lookup"><span data-stu-id="e6c79-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="e6c79-149">3V(핀 58H)</span><span class="sxs-lookup"><span data-stu-id="e6c79-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="e6c79-150">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="e6c79-150">Red cable</span></span>     |
| <span data-ttu-id="e6c79-151">데이터(핀 32F)</span><span class="sxs-lookup"><span data-stu-id="e6c79-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="e6c79-152">GPIO 2(핀 46A)</span><span class="sxs-lookup"><span data-stu-id="e6c79-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="e6c79-153">파란색 케이블</span><span class="sxs-lookup"><span data-stu-id="e6c79-153">Blue cable</span></span>    |
| <span data-ttu-id="e6c79-154">GND(핀 34F)</span><span class="sxs-lookup"><span data-stu-id="e6c79-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="e6c79-155">GND(핀 56I)</span><span class="sxs-lookup"><span data-stu-id="e6c79-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="e6c79-156">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="e6c79-156">Black cable</span></span>   |

<span data-ttu-id="e6c79-157">자세한 내용은 [Adafruit DHT22 센서 설치](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor)(영문) 및 [Adafruit Feather HUZZAH Esp8266 핀 배열](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6c79-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="e6c79-158">이제 Feather Huzzah ESP8266을 작동 센서와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![DHT22를 Feather Huzzah와 연결](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="e6c79-160">페더 HUZZAH ESP8266 tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="e6c79-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="e6c79-161">다음과 같이 hello 마이크로 USB tooType USB 케이블 tooconnect 페더 HUZZAH ESP8266 tooyour 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![페더 Huzzah tooyour 컴퓨터 연결](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="e6c79-163">직렬 포트 권한 추가(Ubuntu만 해당)</span><span class="sxs-lookup"><span data-stu-id="e6c79-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="e6c79-164">Ubuntu를 사용 하는 경우 했는지 확인 hello 권한을 toooperate에 hello USB 포트의 페더 HUZZAH ESP8266 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="e6c79-165">tooadd 직렬 포트 사용 권한을 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e6c79-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="e6c79-166">Hello 다음 터미널에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="e6c79-167">Hello 다음 출력 중 하나를 가져오는:</span><span class="sxs-lookup"><span data-stu-id="e6c79-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="e6c79-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e6c79-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="e6c79-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e6c79-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="e6c79-170">Hello 출력 알 수 있듯이 `uucp` 또는 `dialout` hello USB 포트 hello 그룹 소유자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="e6c79-171">Hello 다음 명령을 실행 하 여 hello 사용자 toohello 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="e6c79-172">`<group-owner-name>`hello 이전 단계에서는 가져온 hello 그룹 소유자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="e6c79-173">`<username>`은 Ubuntu 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="e6c79-174">Ubuntu에서 서명 하 고 변경 tooappear hello에 대 한 다음 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="e6c79-175">센서 데이터를 수집 하 고 tooyour IoT hub 보내기</span><span class="sxs-lookup"><span data-stu-id="e6c79-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="e6c79-176">이 섹션에서는 Feather HUZZAH ESP8266에 대한 응용 프로그램 예제를 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="e6c79-177">hello 샘플 응용 프로그램 hello 페더 HUZZAH ESP8266 led가 깜박입니다 hello 온도 보냅니다 및 IoT 허브에서 hello DHT22 센서 tooyour 습도 데이터 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="e6c79-178">GitHub에서 hello 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6c79-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="e6c79-179">hello 샘플 응용 프로그램은 GitHub에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="e6c79-180">GitHub에서 hello 샘플 응용 프로그램을 포함 하는 hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="e6c79-181">tooclone hello 샘플 리포지토리 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="e6c79-182">명령 프롬프트 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="e6c79-183">저장 된 hello 샘플 응용 프로그램 toobe 저장할 tooa 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="e6c79-184">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="e6c79-185">Hello Arduino IDE에서에서 페더 HUZZAH ESP8266에 대 한 hello 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="e6c79-186">Hello 샘플 응용 프로그램 저장 된 hello 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="e6c79-187">Hello Arduino IDE의에서 hello 응용 프로그램 폴더에 hello app.ino 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Arduino IDE에서 열린 hello 샘플 응용 프로그램](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="e6c79-189">Hello Arduino IDE, 클릭 **파일** > **기본 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="e6c79-190">Hello에 **기본 설정** 대화 상자에서 hello 아이콘 다음 toohello 클릭 **보드 관리자 Url을 추가로** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="e6c79-191">Hello 팝업 창에 hello url을 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Arduino IDE tooa 패키지 url 지정](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="e6c79-193">Hello에 **Preference** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="e6c79-194">**도구** > **보드** > **보드 관리자**를 클릭한 후 esp8266을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="e6c79-195">[보드 관리자]에서 ESP8266 2.2.0 이상 버전으로 설치되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![hello esp8266 패키지가 설치 되어](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="e6c79-197">**도구** > **보드** > **Adafruit HUZZAH ESP8266**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="e6c79-198">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="e6c79-198">Install necessary libraries</span></span>

1. <span data-ttu-id="e6c79-199">Hello Arduino IDE, 클릭 **스케치** > **라이브러리 포함** > **관리 라이브러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="e6c79-200">다음 라이브러리 이름을 하나씩 hello에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="e6c79-201">찾은 각 라이브러리에 대해 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="e6c79-202">실제 DHT22 센서가 없나요?</span><span class="sxs-lookup"><span data-stu-id="e6c79-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="e6c79-203">실제 DHT22 센서 없는 경우 hello 샘플 응용 프로그램 데이터를 온도 및 습도 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="e6c79-204">tooset hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e6c79-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="e6c79-205">열기 hello `config.h` hello에 대 한 파일 `app` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="e6c79-206">다음 코드 줄을 hello를 찾아 hello 값에서 변경 `false` 너무`true`:</span><span class="sxs-lookup"><span data-stu-id="e6c79-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 구성 합니다.](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="e6c79-208">Hello 파일을 저장 `Control-s`합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="e6c79-209">Hello 샘플 응용 프로그램 tooFeather HUZZAH ESP8266 배포</span><span class="sxs-lookup"><span data-stu-id="e6c79-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="e6c79-210">Hello Arduino IDE, 클릭 **도구** > **포트**, 페더 HUZZAH ESP8266에 대 한 hello 직렬 포트를 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="e6c79-211">클릭 **스케치** > **업로드** toobuild hello 샘플 응용 프로그램 tooFeather HUZZAH ESP8266를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="e6c79-212">자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="e6c79-212">Enter your credentials</span></span>

<span data-ttu-id="e6c79-213">Hello 업로드 성공적으로 완료 되 면 이러한 단계 tooenter 자격 증명를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="e6c79-214">Hello Arduino IDE, 클릭 **도구** > **직렬 모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="e6c79-215">Hello 직렬 모니터 창에서 hello 오른쪽 아래 모서리에 hello 두 드롭 다운 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="e6c79-216">선택 **줄 닫는** hello 왼쪽된 드롭다운 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="e6c79-217">선택 **115200 보드** hello 오른쪽 드롭다운 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="e6c79-218">Hello 직렬 모니터 창의 hello 위쪽에 있는 입력된 상자 hello에에서 hello tooprovide 요청 하는 경우 다음 정보를 입력, 클릭 하 고 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="e6c79-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="e6c79-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="e6c79-220">Wi-Fi 암호</span><span class="sxs-lookup"><span data-stu-id="e6c79-220">Wi-Fi password</span></span>
   * <span data-ttu-id="e6c79-221">장치 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="e6c79-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="e6c79-222">hello 자격 증명 정보는 hello 페더 HUZZAH ESP8266 EEPROM에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="e6c79-223">Hello 페더 HUZZAH ESP8266 보드에 hello reset 단추를 누르면 hello 샘플 응용 프로그램 묻는 tooerase hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="e6c79-224">입력 `Y` toohave hello 정보를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="e6c79-225">Tooprovide hello 정보를 두 번째로 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="e6c79-226">Hello 샘플 응용 프로그램을 성공적으로 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="e6c79-227">표시 되 면 hello 다음 hello 직렬 모니터 창에서 출력 및 hello 페더 HUZZAH ESP8266 hello 샘플 응용 프로그램의 led가 깜박입니다.이 성공적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Arduino IDE의 최종 출력](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="e6c79-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6c79-229">Next steps</span></span>

<span data-ttu-id="e6c79-230">페더 HUZZAH ESP8266 tooyour IoT 허브를 연결 하 고 캡처한 hello 센서 데이터 tooyour IoT 허브를 전송 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6c79-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

