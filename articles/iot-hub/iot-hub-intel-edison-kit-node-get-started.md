---
title: "aaaIntel Edison toocloud (Node.js)-Intel Edison 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 방법을 toosetup 하 고이 자습서에서는 Intel Edison toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 Intel Edison tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot intel edison, intel edison iot 허브, intel edison 보낼 데이터 toocloud, intel edison toocloud"
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="3272a-104">Intel Edison tooAzure IoT Hub (Node.js) 연결</span><span class="sxs-lookup"><span data-stu-id="3272a-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="3272a-105">이 자습서에서는 먼저 Intel Edison 작업할 hello 기본 사항 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="3272a-106">그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="3272a-107">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="3272a-107">Don't have a kit yet?</span></span> <span data-ttu-id="3272a-108">[여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="3272a-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3272a-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="3272a-109">What you do</span></span>

* <span data-ttu-id="3272a-110">Intel Edison 및 Grove 모듈을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="3272a-111">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-111">Create an IoT hub.</span></span>
* <span data-ttu-id="3272a-112">IoT Hub에 Edison용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="3272a-113">Edison toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="3272a-114">Intel Edison tooan IoT hub를 만들면를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="3272a-115">다음 예제 응용 프로그램에서에서를 실행 Edison toocollect 온도 및 습도 데이터 나무숲을 조성 온도 센서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="3272a-116">마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3272a-117">학습 내용</span><span class="sxs-lookup"><span data-stu-id="3272a-117">What you learn</span></span>

* <span data-ttu-id="3272a-118">어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="3272a-119">어떻게 나무숲을 조성 온도 센서와 Edison tooconnect 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="3272a-120">어떻게 Edison에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="3272a-121">어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3272a-122">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="3272a-122">What you need</span></span>

![필요한 항목](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="3272a-124">hello Intel Edison 보드</span><span class="sxs-lookup"><span data-stu-id="3272a-124">hello Intel Edison board</span></span>
* <span data-ttu-id="3272a-125">Arduino 확장 보드</span><span class="sxs-lookup"><span data-stu-id="3272a-125">Arduino expansion board</span></span>
* <span data-ttu-id="3272a-126">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3272a-126">An active Azure subscription.</span></span> <span data-ttu-id="3272a-127">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3272a-128">Windows 또는 Linux를 실행하는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="3272a-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="3272a-129">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="3272a-129">An Internet connection.</span></span>
* <span data-ttu-id="3272a-130">마이크로 B tooType A USB 케이블</span><span class="sxs-lookup"><span data-stu-id="3272a-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="3272a-131">DC(직류) 전원 공급 장치</span><span class="sxs-lookup"><span data-stu-id="3272a-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="3272a-132">전원 공급 장치 정격은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="3272a-133">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="3272a-133">7-15V DC</span></span>
  - <span data-ttu-id="3272a-134">1500mA 이상</span><span class="sxs-lookup"><span data-stu-id="3272a-134">At least 1500mA</span></span>
  - <span data-ttu-id="3272a-135">hello 센터/내부 pin hello 양수 극의 hello 전원 공급 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="3272a-136">hello 다음 항목은 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="3272a-136">hello following items are optional:</span></span>

* <span data-ttu-id="3272a-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="3272a-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="3272a-138">Grove - 온도 센서</span><span class="sxs-lookup"><span data-stu-id="3272a-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="3272a-139">Grove 케이블</span><span class="sxs-lookup"><span data-stu-id="3272a-139">Grove Cable</span></span>
* <span data-ttu-id="3272a-140">모든 공백 막대 또는 나사 hello 패키징, 나사 두 toofasten hello 모듈 toohello 확장 보드 등의 나사와 플라스틱 스페이서 4 집합에에서 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="3272a-141">Hello 코드 샘플 지원 센서 데이터를 시뮬레이션 하기 때문에 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="3272a-142">Intel Edison 설정</span><span class="sxs-lookup"><span data-stu-id="3272a-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="3272a-143">보드 조립</span><span class="sxs-lookup"><span data-stu-id="3272a-143">Assemble your board</span></span>

<span data-ttu-id="3272a-144">이 섹션 단계 tooattach Intel® Edison 모듈 tooyour 확장 보드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="3272a-145">Hello 확장 보드에 hello 나사 hello 모듈에 hello 허점 만나려고 프로그램 확장 보드에 흰색 hello 개요 내의 hello Intel® Edison 모듈을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="3272a-146">Hello 단어 바로 아래 hello 모듈을 누르면 `What will you make?` 간단히 생각 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![보드 2 조립](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="3272a-148">Hello 두 (hello 패키지에 포함 됨) 하는 16 진수 너트 toosecure hello 모듈 toohello 확장 보드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![보드 3 조립](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="3272a-150">Hello 확장 보드에 네 개의 모퉁이 구멍 hello 중 하나에 나사를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="3272a-151">비틀 및 hello 나사에 흰색 hello 플라스틱 스페이서 중 하나를 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![보드 4 조립](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="3272a-153">반복에 대 한 다른 3 개의 모퉁이 스페이서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-153">Repeat for hello other three corner spacers.</span></span>

   ![보드 5 조립](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="3272a-155">이제 보드가 조립됩니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-155">Now your board is assembled.</span></span>

   ![조립된 보드](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="3272a-157">연결 나무숲을 조성 자료 방패 hello 및 hello 온도 센서</span><span class="sxs-lookup"><span data-stu-id="3272a-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="3272a-158">Hello 나무숲을 조성 자료 방패 tooyour 보드에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="3272a-159">모든 핀이 보드에 꽂혀 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="3272a-161">Hello 나무숲을 조성 자료 방패에 나무숲을 사용 하 여 나무숲을 조성 케이블 tooconnect 조성 온도 센서 **A0** 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Tootemperature 센서 연결](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison 및 센서 연결](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="3272a-164">이제 센서가 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="3272a-165">Edison 전원 켜기</span><span class="sxs-lookup"><span data-stu-id="3272a-165">Power up Edison</span></span>

1. <span data-ttu-id="3272a-166">Hello 전원 공급 장치에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-166">Plug in hello power supply.</span></span>

   ![전원 공급 장치 꽂기](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="3272a-168">(DS1 hello Arduino * 확장 보드에 표시) 녹색 led가 켜지 고 켜져 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="3272a-169">Hello 보드 toofinish 부팅에 대 일 분 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3272a-170">DC 전원 공급 장치가 하면 전원 hello 보드 USB 포트를 통해 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="3272a-171">자세한 내용은 `Connect Edison tooyour computer` 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3272a-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="3272a-172">이러한 방식으로 보드를 켜면 보드에서 예기치 않은 동작이 나타날 수 있습니다. 이러한 현상은 Wi-Fi 또는 구동 모터를 사용할 때 더욱 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="3272a-173">Edison tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="3272a-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="3272a-174">Edison 장치 모드는 hello 두 마이크로 USB 포트에 대 한 hello 마이크로 스위치를 설정/해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="3272a-175">장치 모드와 호스트 모드 간 차이점에 대해서는 [여기](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3272a-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Hello 마이크로 스위치를 설정/해제](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="3272a-177">Hello 상위 마이크로 USB 포트에 hello 마이크로 USB 케이블을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![위쪽 마이크로 USB 포트](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="3272a-179">플러그를 컴퓨터에 USB 케이블의 다른 쪽 끝을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-179">Plug hello other end of USB cable into your computer.</span></span>

   ![컴퓨터 USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="3272a-181">컴퓨터에 새 장치를 탑재(컴퓨터에 SD 카드를 꽂는 것과 매우 유사함)할 때 보드가 완전히 초기화된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="3272a-182">다운로드 하 고 hello 구성 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="3272a-183">Hello 최신 구성 도구에서 가져올 [이 링크](https://software.intel.com/en-us/iot/hardware/edison/downloads) hello 아래에 나열 `Installers` 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="3272a-184">Hello 도구를 실행 하 고에 따라 해당 화면에 나타나는 지침, 필요한 경우 다음을 클릭</span><span class="sxs-lookup"><span data-stu-id="3272a-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="3272a-185">펌웨어 플래시</span><span class="sxs-lookup"><span data-stu-id="3272a-185">Flash firmware</span></span>
1. <span data-ttu-id="3272a-186">Hello에 `Set up options` 페이지 `Flash Firmware`합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="3272a-187">보드에 hello 이미지 tooflash hello 다음 중 하나를 수행 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="3272a-188">보드 hello 최신 펌웨어 이미지와 Intel에서 사용할 수 있는 선택 toodownload 및 플래시 `Download hello latest image version xxxx`합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="3272a-189">tooflash 이미 컴퓨터에 저장 한 이미지와 함께 보드 선택 `Select hello local image`합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="3272a-190">Tooflash tooyour 게시판 tooand 선택 hello 이미지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="3272a-191">hello 설치 도구 tooflash 보드를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="3272a-192">hello 전체 깜박이 프로세스는 too10 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="3272a-193">암호 설정</span><span class="sxs-lookup"><span data-stu-id="3272a-193">Set password</span></span>
1. <span data-ttu-id="3272a-194">Hello에 `Set up options` 페이지 `Enable Security`합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="3272a-195">Intel® Edison 보드에 대한 사용자 지정 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="3272a-196">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-196">This is optional.</span></span>
3. <span data-ttu-id="3272a-197">보드에 대한 암호를 입력한 후 `Set password`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="3272a-198">나중에 사용 되는 hello 암호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="3272a-199">Wi-Fi 연결</span><span class="sxs-lookup"><span data-stu-id="3272a-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="3272a-200">Hello에 `Set up options` 페이지 `Connect Wi-Fi`합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="3272a-201">사용 가능한 Wi-fi 네트워크에 대 한 컴퓨터 검색으로 tooone 분을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="3272a-202">Hello에서 `Detected Networks` 드롭 다운 목록에서 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="3272a-203">Hello에서 `Security` 드롭 다운 목록, 선택 hello 네트워크의 보안 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="3272a-204">로그인 및 암호 정보를 입력한 다음 `Configure Wi-Fi`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="3272a-205">Hello 아래로 나중에 사용 되는 IP 주소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="3272a-206">Edison 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="3272a-207">Edison tooyour hello IP 주소를 사용 하 여 연결 하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Tootemperature 센서 연결](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="3272a-209">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-209">Congratulations!</span></span> <span data-ttu-id="3272a-210">Edison 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="3272a-211">Intel Edison에 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3272a-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="3272a-212">Azure IoT 장치 SDK hello 준비</span><span class="sxs-lookup"><span data-stu-id="3272a-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="3272a-213">Hello 호스트 컴퓨터 tooconnect tooyour Intel Edison에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="3272a-214">hello IP 주소가 hello 구성 도구에서 고 hello 암호는 hello 하나 해당 도구에서 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="3272a-215">Windows용 [PuTTY](http://www.putty.org/)</span><span class="sxs-lookup"><span data-stu-id="3272a-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="3272a-216">hello 기본 제공 SSH 클라이언트 Ubuntu 또는 macOS에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="3272a-217">Hello 샘플 클라이언트 응용 프로그램 tooyour 장치를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="3272a-218">다음 toohello 리포지토리 폴더 toorun hello 명령 tooinstall 다음 모든 패키지를 이동, serval 분 toocomplete 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="3272a-219">구성 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3272a-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="3272a-220">Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Config 파일](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="3272a-222">이 파일에는 사용자가 구성할 수 있는 두 개의 매크로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="3272a-223">hello 먼저 하나는 `INTERVAL`, toocloud 전송 하는 두 개의 메시지 간의 hello 시간 간격을 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="3272a-224">두 번째 식 hello `simulatedData`, 값은 부울 값 여부 toouse 센서 데이터를 시뮬레이션 하는 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="3272a-225">경우 있습니다 **hello 센서 없는**설정 hello `simulatedData` 너무 값`true` toomake hello 샘플 응용 프로그램을 만들고 시뮬레이션된 센서 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="3272a-226">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="3272a-227">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="3272a-228">하면 복사-붙여넣기 hello 장치 연결 문자열 hello 작은따옴표에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="3272a-229">Hello 다음 출력에서는 hello 센서 데이터와 hello 전송 된 메시지를 tooyour IoT 허브는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![출력-Intel Edison tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="3272a-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3272a-231">Next steps</span></span>

<span data-ttu-id="3272a-232">샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3272a-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
