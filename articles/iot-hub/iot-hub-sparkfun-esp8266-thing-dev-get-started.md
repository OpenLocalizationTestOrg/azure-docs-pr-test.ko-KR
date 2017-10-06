---
title: "aaaESP8266 toocloud-연결 Sparkfun ESP8266 일 Dev tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup이 자습서에서에 대 한 IoT Hub Sparkfun ESP8266 일 Dev tooAzure toosend 데이터 toohello Azure 클라우드 플랫폼을 연결 하 고 있습니다."
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
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="76577-103">Sparkfun ESP8266 일 Dev tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, Thing Dev 및 IoT Hub 간 연결](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="76577-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="76577-105">What you will do</span></span>

<span data-ttu-id="76577-106">만들려는 Sparkfun ESP8266 일 Dev tooan IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="76577-107">다음 DHT22 센서에서 샘플 응용 프로그램 ESP8266 toocollect 온도 및 습도 데이터에 대해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="76577-108">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76577-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="76577-109">이러한 단계 tooconnect 다른 ESP8266 보드를 사용 하는 경우 여전히 따라 수 것 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="76577-110">Hello ESP8266 보드를 사용 하는, 따라 tooreconfigure hello를 할 수 있습니다 `LED_PIN`합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="76577-111">예를 들어 ESP8266 AI Thinker에서를 사용 하는 경우 변경할 수 있습니다에서 `0` 너무`2`합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="76577-112">아직 키트가 없나요? [여기](http://azure.com/iotstarterkits)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="76577-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="76577-113">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="76577-113">What you will learn</span></span>

* <span data-ttu-id="76577-114">어떻게 toocreate IoT hub 일 개발에 대 한 장치를 등록 하 고</span><span class="sxs-lookup"><span data-stu-id="76577-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="76577-115">어떻게 tooconnect 일 Dev hello 센서와 사용자의 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="76577-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="76577-116">방법 항목 개발에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터</span><span class="sxs-lookup"><span data-stu-id="76577-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="76577-117">어떻게 toosend hello 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="76577-118">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="76577-118">What you will need</span></span>

![hello 자습서에 필요한 부품](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="76577-120">toocomplete 일 개발자 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="76577-121">hello Sparkfun ESP8266 일 Dev 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="76577-122">마이크로 USB tooType A USB 케이블</span><span class="sxs-lookup"><span data-stu-id="76577-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="76577-123">개발 환경에 대 한 hello 다음 구성 요소도 필요.</span><span class="sxs-lookup"><span data-stu-id="76577-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="76577-124">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="76577-124">An active Azure subscription.</span></span> <span data-ttu-id="76577-125">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76577-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="76577-126">Windows 또는 Ubuntu가 실행되는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="76577-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="76577-127">무선 네트워크에 Sparkfun ESP8266 일 Dev tooconnect에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="76577-128">인터넷 연결 toodownload hello 구성 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="76577-129">[Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 버전 이상, 이전 버전 hello AzureIoT 라이브러리와 함께 작동 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="76577-130">hello 다음 항목은 선택적 요소는 센서 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="76577-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="76577-131">시뮬레이션 된 센서 데이터를 사용 하 여 hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76577-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="76577-132">Adafruit DHT22 온도 및 습도 센서</span><span class="sxs-lookup"><span data-stu-id="76577-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="76577-133">실험용 회로판</span><span class="sxs-lookup"><span data-stu-id="76577-133">A breadboard.</span></span>
* <span data-ttu-id="76577-134">M/M 점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="76577-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="76577-135">ESP8266 일 Dev hello 센서 및 컴퓨터를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="76577-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="76577-136">DHT22 온도 및 습도 센서 연결 tooESP8266 일 개발</span><span class="sxs-lookup"><span data-stu-id="76577-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="76577-137">다음과 같이 hello breadboard 및 점퍼 와이어 toomake hello 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="76577-138">센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="76577-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![연결 참조](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="76577-140">센서 핀에 대 한 hello 배선 다음 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="76577-141">시작(센서)</span><span class="sxs-lookup"><span data-stu-id="76577-141">Start (Sensor)</span></span>           | <span data-ttu-id="76577-142">끝(보드)</span><span class="sxs-lookup"><span data-stu-id="76577-142">End (Board)</span></span>           | <span data-ttu-id="76577-143">케이블 색</span><span class="sxs-lookup"><span data-stu-id="76577-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="76577-144">VDD(27F 핀)</span><span class="sxs-lookup"><span data-stu-id="76577-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="76577-145">3V(8A 핀)</span><span class="sxs-lookup"><span data-stu-id="76577-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="76577-146">빨간색 케이블</span><span class="sxs-lookup"><span data-stu-id="76577-146">Red cable</span></span>     |
| <span data-ttu-id="76577-147">데이터(28F 핀)</span><span class="sxs-lookup"><span data-stu-id="76577-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="76577-148">GPIO 2(9A 핀)</span><span class="sxs-lookup"><span data-stu-id="76577-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="76577-149">흰색 케이블</span><span class="sxs-lookup"><span data-stu-id="76577-149">White cable</span></span>    |
| <span data-ttu-id="76577-150">GND(30F 핀)</span><span class="sxs-lookup"><span data-stu-id="76577-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="76577-151">GND(7J 핀)</span><span class="sxs-lookup"><span data-stu-id="76577-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="76577-152">검은색 케이블</span><span class="sxs-lookup"><span data-stu-id="76577-152">Black cable</span></span>   |


- <span data-ttu-id="76577-153">자세한 내용은 [DHT22 센서 설정](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf)(영문) 및 [Sparkfun ESP8266 Thing Dev 사양](https://www.sparkfun.com/products/13711)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76577-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="76577-154">이제 Sparkfun ESP8266 Thing Dev를 작동 센서와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![dht22와 ESP8266 Thing Dev 연결](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="76577-156">Sparkfun ESP8266 일 Dev tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="76577-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="76577-157">다음과 같이 hello 마이크로 USB tooType USB 케이블 tooconnect Sparkfun ESP8266 일 Dev tooyour 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![페더 huzzah tooyour 컴퓨터 연결](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="76577-159">직렬 포트 권한 추가 – Ubuntu만</span><span class="sxs-lookup"><span data-stu-id="76577-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="76577-160">Ubuntu를 사용 하는 경우 일반 사용자에 hello 권한을 toooperate에 hello USB 포트의 Sparkfun ESP8266 일 개발 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="76577-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="76577-161">다음이 단계를 수행 하는 일반 사용자에 대 한 tooadd 직렬 포트 사용 권한:</span><span class="sxs-lookup"><span data-stu-id="76577-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="76577-162">Hello 다음 터미널에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="76577-163">Hello 다음 출력 중 하나를 가져오는:</span><span class="sxs-lookup"><span data-stu-id="76577-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="76577-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="76577-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="76577-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="76577-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="76577-166">Hello 출력 `uucp` 또는 `dialout` 즉 hello 소유자의 그룹 이름을 hello USB 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="76577-167">Hello 다음 명령을 실행 하 여 hello 사용자 toohello 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="76577-168">`<group-owner-name>`hello 이전 단계에서는 가져온 hello 그룹 소유자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="76577-169">`<username>`은 Ubuntu 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="76577-170">로그 아웃 Ubuntu 하 한이 다시 로그인 tootake 효과 변경 하는 hello에 대 한 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="76577-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="76577-171">센서 데이터를 수집 하 고 tooyour IoT hub 보내기</span><span class="sxs-lookup"><span data-stu-id="76577-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="76577-172">이 섹션에서는 Sparkfun ESP8266 Thing Dev에 대한 샘플 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="76577-173">hello 샘플 응용 프로그램 hello Sparkfun ESP8266 작업 개발자의 led가 깜박입니다 hello 온도 보냅니다 및 IoT 허브에서 hello DHT22 센서 tooyour 습도 데이터 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="76577-174">GitHub에서 hello 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="76577-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="76577-175">hello 샘플 응용 프로그램은 GitHub에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76577-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="76577-176">GitHub에서 hello 샘플 응용 프로그램을 포함 하는 hello 샘플 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="76577-177">tooclone hello 샘플 리포지토리 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="76577-178">명령 프롬프트 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76577-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="76577-179">저장 된 hello 샘플 응용 프로그램 toobe 저장할 tooa 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="76577-180">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="76577-181">Arduino IDE에서 Sparkfun ESP8266 일 dev hello 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="76577-182">Hello 샘플 응용 프로그램 저장 된 hello 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76577-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="76577-183">Arduino IDE에서 hello 응용 프로그램 폴더에서 hello app.ino 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76577-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![arduino ide에서 열린 hello 샘플 응용 프로그램](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="76577-185">Hello Arduino IDE, 클릭 **파일** > **기본 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="76577-186">Hello에 **기본 설정** 대화 상자에서 hello 아이콘 다음 toohello 클릭 **보드 관리자 Url을 추가로** 입력란.</span><span class="sxs-lookup"><span data-stu-id="76577-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="76577-187">Hello 팝업 창에 hello url을 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![arduino ide tooa 패키지 url 지정](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="76577-189">Hello에 **Preference** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="76577-190">**도구** > **보드** > **보드 관리자**를 클릭한 후 esp8266을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="76577-191">ESP8266 버전 2.2.0 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![hello esp8266 패키지가 설치 되어](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="76577-193">**도구** > **보드** > **Sparkfun ESP8266 Thing Dev**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="76577-194">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="76577-194">Install necessary libraries</span></span>

1. <span data-ttu-id="76577-195">Hello Arduino IDE, 클릭 **스케치** > **라이브러리 포함** > **관리 라이브러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="76577-196">다음 라이브러리 이름을 하나씩 hello에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="76577-197">각 찾았으면 hello 라이브러리에 대 한 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="76577-198">실제 DHT22 센서가 없나요?</span><span class="sxs-lookup"><span data-stu-id="76577-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="76577-199">실제 DHT22 센서 없는 경우 hello 샘플 응용 프로그램 데이터를 온도 및 습도 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76577-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="76577-200">tooenable hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="76577-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="76577-201">열기 hello `config.h` hello에 대 한 파일 `app` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="76577-202">다음 코드 줄을 hello를 찾아 hello 값에서 변경 `false` 너무`true`:</span><span class="sxs-lookup"><span data-stu-id="76577-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 구성 합니다.](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="76577-204">`Control-s`로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="76577-205">Hello 샘플 응용 프로그램 tooSparkfun ESP8266 일 개발 배포</span><span class="sxs-lookup"><span data-stu-id="76577-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="76577-206">Hello Arduino IDE, 클릭 **도구** > **포트**, Sparkfun ESP8266 일 개발 hello 직렬 포트를 클릭 한 다음</span><span class="sxs-lookup"><span data-stu-id="76577-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="76577-207">클릭 **스케치** > **업로드** toobuild hello 샘플 응용 프로그램 tooSparkfun ESP8266 일 장치 배포</span><span class="sxs-lookup"><span data-stu-id="76577-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="76577-208">MacOS를 사용 하는 경우 아마도 hello 메시지를 업로드 하는 동안 다음을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76577-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="76577-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="76577-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="76577-210">Ternimal 창을 열고이 문제를 작업 toosolve 아래 완료 하십시오.</span><span class="sxs-lookup"><span data-stu-id="76577-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="76577-211">자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="76577-211">Enter your credentials</span></span>

<span data-ttu-id="76577-212">Hello 업로드 성공적으로 완료 되 면 hello 단계 tooenter 자격 증명를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="76577-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="76577-213">Hello Arduino IDE, 클릭 **도구** > **직렬 모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="76577-214">Hello 직렬 모니터 창에서 hello 오른쪽 아래 모서리에 hello 두 드롭 다운 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="76577-215">선택 **줄 닫는** hello 왼쪽된 드롭다운 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="76577-216">선택 **115200 보드** hello 오른쪽 드롭다운 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="76577-217">Hello 직렬 모니터 창의 hello 위쪽에 있는 입력된 상자 hello에에서 hello tooprovide 요청 하는 경우 다음 정보를 입력, 클릭 하 고 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="76577-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="76577-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="76577-219">Wi-Fi 암호</span><span class="sxs-lookup"><span data-stu-id="76577-219">Wi-Fi password</span></span>
   * <span data-ttu-id="76577-220">장치 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="76577-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="76577-221">hello 자격 증명 정보는 hello EEPROM의 Sparkfun ESP8266 일 장치에 저장</span><span class="sxs-lookup"><span data-stu-id="76577-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="76577-222">Hello Sparkfun ESP8266 일 Dev 보드에 hello reset 단추를 누르면 hello 샘플 응용 프로그램 묻는 경우 tooerase hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76577-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="76577-223">입력 `Y` toohave hello 정보를 삭제 하 고 라는 tooprovide hello 정보를 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76577-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="76577-224">Hello 샘플 응용 프로그램을 성공적으로 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76577-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="76577-225">표시 되 면 hello 다음 hello 직렬 모니터 창에서 출력 및 hello Sparkfun ESP8266 일 개발, hello 샘플 응용 프로그램의 led가 깜박입니다.이 성공적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76577-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![arduino ide에서 최종 출력](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="76577-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76577-227">Next steps</span></span>

<span data-ttu-id="76577-228">Sparkfun ESP8266 일 Dev tooyour IoT 허브를 연결 하 고 캡처한 hello 센서 데이터 tooyour IoT 허브를 전송 했습니다.</span><span class="sxs-lookup"><span data-stu-id="76577-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
