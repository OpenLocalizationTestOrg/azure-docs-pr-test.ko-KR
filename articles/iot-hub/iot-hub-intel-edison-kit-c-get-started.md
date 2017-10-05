---
title: "Intel Edison - 클라우드(C) - Azure IoT Hub에 Intel Edison 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure 클라우드 플랫폼으로 데이터를 보내기 위해 Intel Edison을 설정하고 Intel Edison용 Azure IoT Hub에 연결하는 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot intel edison, intel edison iot hub, intel edison에서 클라우드로 데이터 보내기, intel edison - 클라우드"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: edbdbe0230f742cd7228f04a4a83c9bd567527e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-c"></a><span data-ttu-id="9ff3d-104">Azure IoT Hub에 Intel Edison 연결(C)</span><span class="sxs-lookup"><span data-stu-id="9ff3d-104">Connect Intel Edison to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="9ff3d-105">이 자습서에서는 Intel Edison을 실행하는 작업의 기초부터 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="9ff3d-106">그런 다음 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)를 사용하여 장치를 클라우드에 원활하게 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="9ff3d-107">아직 키트가 없으세요?</span><span class="sxs-lookup"><span data-stu-id="9ff3d-107">Don't have a kit yet?</span></span> <span data-ttu-id="9ff3d-108">[여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9ff3d-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="9ff3d-109">What you do</span></span>

* <span data-ttu-id="9ff3d-110">Intel Edison 및 Grove 모듈을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="9ff3d-111">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-111">Create an IoT hub.</span></span>
* <span data-ttu-id="9ff3d-112">IoT Hub에 Edison용 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="9ff3d-113">Edison에서 샘플 응용 프로그램을 실행하여 IoT Hub로 센서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="9ff3d-114">앞에서 만든 IoT Hub에 Intel Edison을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="9ff3d-115">그런 다음 Edison에서 샘플 응용 프로그램을 실행하여 Grove 온도 센서에서 온도 및 습도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="9ff3d-116">마지막으로 센서 데이터를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9ff3d-117">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9ff3d-117">What you learn</span></span>

* <span data-ttu-id="9ff3d-118">Azure IoT Hub를 만들고 새 장치 연결 문자열을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="9ff3d-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="9ff3d-119">Edison을 Grove 온도 센서에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="9ff3d-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="9ff3d-120">Edison에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법</span><span class="sxs-lookup"><span data-stu-id="9ff3d-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="9ff3d-121">IoT Hub로 센서 데이터를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="9ff3d-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9ff3d-122">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="9ff3d-122">What you need</span></span>

![필요한 항목](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="9ff3d-124">Intel Edison 보드</span><span class="sxs-lookup"><span data-stu-id="9ff3d-124">The Intel Edison board</span></span>
* <span data-ttu-id="9ff3d-125">Arduino 확장 보드</span><span class="sxs-lookup"><span data-stu-id="9ff3d-125">Arduino expansion board</span></span>
* <span data-ttu-id="9ff3d-126">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-126">An active Azure subscription.</span></span> <span data-ttu-id="9ff3d-127">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="9ff3d-128">Windows 또는 Linux를 실행하는 Mac 또는 PC</span><span class="sxs-lookup"><span data-stu-id="9ff3d-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="9ff3d-129">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="9ff3d-129">An Internet connection.</span></span>
* <span data-ttu-id="9ff3d-130">Micro B-A형 USB 케이블</span><span class="sxs-lookup"><span data-stu-id="9ff3d-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="9ff3d-131">DC(직류) 전원 공급 장치</span><span class="sxs-lookup"><span data-stu-id="9ff3d-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="9ff3d-132">전원 공급 장치 정격은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="9ff3d-133">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="9ff3d-133">7-15V DC</span></span>
  - <span data-ttu-id="9ff3d-134">1500mA 이상</span><span class="sxs-lookup"><span data-stu-id="9ff3d-134">At least 1500mA</span></span>
  - <span data-ttu-id="9ff3d-135">중앙/내부 핀은 전원 공급 장치의 양극이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="9ff3d-136">다음 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-136">The following items are optional:</span></span>

* <span data-ttu-id="9ff3d-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="9ff3d-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="9ff3d-138">Grove - 온도 센서</span><span class="sxs-lookup"><span data-stu-id="9ff3d-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="9ff3d-139">Grove 케이블</span><span class="sxs-lookup"><span data-stu-id="9ff3d-139">Grove Cable</span></span>
* <span data-ttu-id="9ff3d-140">포장에 포함된 스페이서 바 또는 나사(모듈을 확장 보드에 고정하기 위한 2개의 나사와 4개의 나사 세트 및 플라스틱 스페이서 포함)</span><span class="sxs-lookup"><span data-stu-id="9ff3d-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="9ff3d-141">코드 샘플이 시뮬레이션된 센서 데이터를 지원하므로 이러한 항목은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="9ff3d-142">Intel Edison 설정</span><span class="sxs-lookup"><span data-stu-id="9ff3d-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="9ff3d-143">보드 조립</span><span class="sxs-lookup"><span data-stu-id="9ff3d-143">Assemble your board</span></span>

<span data-ttu-id="9ff3d-144">이 섹션에는 Intel® Edison 모듈을 확장 보드를 연결하는 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="9ff3d-145">확장 보드의 흰색 윤곽 안에 Intel® Edison 모듈을 놓고 모듈의 구멍과 확장 보드의 나사를 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="9ff3d-146">딸깍 소리가 느껴질 때까지 `What will you make?` 아래에서 모듈을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![보드 2 조립](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="9ff3d-148">2개의 육각 너트(포장에 포함)를 사용하여 모듈을 확장 보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![보드 3 조립](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="9ff3d-150">확장 보드의 구석에 있는 4개 구멍 중 하나에 나사를 끼웁니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="9ff3d-151">흰색 플라스틱 스페너 중 하나를 돌려 나사를 조입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![보드 4 조립](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="9ff3d-153">나머지 3개 구석의 스페이서에 대해 같은 작업을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-153">Repeat for the other three corner spacers.</span></span>

   ![보드 5 조립](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="9ff3d-155">이제 보드가 조립됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-155">Now your board is assembled.</span></span>

   ![조립된 보드](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="9ff3d-157">Grove Base Shield 및 온도 센서 연결</span><span class="sxs-lookup"><span data-stu-id="9ff3d-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="9ff3d-158">보드에 Grove Base Shield를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="9ff3d-159">모든 핀이 보드에 꽂혀 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="9ff3d-161">Grove 케이블을 사용하여 Grove 온도 센서를 Grove Base Shield **A0** 포트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![온도 센서에 연결](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison 및 센서 연결](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="9ff3d-164">이제 센서가 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="9ff3d-165">Edison 전원 켜기</span><span class="sxs-lookup"><span data-stu-id="9ff3d-165">Power up Edison</span></span>

1. <span data-ttu-id="9ff3d-166">전원 공급 장치를 꽂습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-166">Plug in the power supply.</span></span>

   ![전원 공급 장치 꽂기](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="9ff3d-168">녹색 LED(Arduino* 확장 보드에 DS1으로 레이블 지정)가 켜진 후 계속 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="9ff3d-169">보드가 부팅을 마칠 때까지 1분 정도 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9ff3d-170">DC 전원 공급 장치가 없으면 USB 포트를 통해 여전히 보드의 전원을 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="9ff3d-171">자세한 내용은 `Connect Edison to your computer` 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="9ff3d-172">이러한 방식으로 보드를 켜면 보드에서 예기치 않은 동작이 나타날 수 있습니다. 이러한 현상은 Wi-Fi 또는 구동 모터를 사용할 때 더욱 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="9ff3d-173">Edison을 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="9ff3d-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="9ff3d-174">Edison이 장치 모드가 되도록 2개의 마이크로 USB 포트 쪽으로 마이크로 스위치를 내립니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="9ff3d-175">장치 모드와 호스트 모드 간 차이점에 대해서는 [여기](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![마이크로 스위치 내리기](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="9ff3d-177">마이크로 USB 포트를 위쪽 마이크로 USB 케이블에 꽂습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![위쪽 마이크로 USB 포트](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="9ff3d-179">USB 케이블의 다른 쪽을 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-179">Plug the other end of USB cable into your computer.</span></span>

   ![컴퓨터 USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="9ff3d-181">컴퓨터에 새 장치를 탑재(컴퓨터에 SD 카드를 꽂는 것과 매우 유사함)할 때 보드가 완전히 초기화된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="9ff3d-182">구성 도구 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="9ff3d-182">Download and run the configuration tool</span></span>
<span data-ttu-id="9ff3d-183">`Installers` 제목 아래 나열된 [이 링크](https://software.intel.com/en-us/iot/hardware/edison/downloads)에서 최신 구성 도구를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="9ff3d-184">도구를 실행하고 화면 지시를 따른 다음 필요할 때 다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="9ff3d-185">펌웨어 플래시</span><span class="sxs-lookup"><span data-stu-id="9ff3d-185">Flash firmware</span></span>
1. <span data-ttu-id="9ff3d-186">`Set up options` 페이지에서 `Flash Firmware`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="9ff3d-187">다음 중 하나를 수행하여 보드에서 플래시할 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="9ff3d-188">Intel에서 사용 가능한 최신 펌웨어 이미지를 다운로드한 후 이 이미지로 보드를 플래시하려면 `Download the latest image version xxxx`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="9ff3d-189">컴퓨터에 이미 저장한 이미지로 보드를 플래시하려면 `Select the local image`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="9ff3d-190">보드에 플래시할 이미지를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="9ff3d-191">설치 도구는 보드를 플래시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="9ff3d-192">전체 플래시 프로세스는 10분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="9ff3d-193">암호 설정</span><span class="sxs-lookup"><span data-stu-id="9ff3d-193">Set password</span></span>
1. <span data-ttu-id="9ff3d-194">`Set up options` 페이지에서 `Enable Security`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="9ff3d-195">Intel® Edison 보드에 대한 사용자 지정 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="9ff3d-196">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-196">This is optional.</span></span>
3. <span data-ttu-id="9ff3d-197">보드에 대한 암호를 입력한 후 `Set password`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="9ff3d-198">나중에 사용되는 암호에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="9ff3d-199">Wi-Fi 연결</span><span class="sxs-lookup"><span data-stu-id="9ff3d-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="9ff3d-200">`Set up options` 페이지에서 `Connect Wi-Fi`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="9ff3d-201">컴퓨터가 사용할 수 있는 Wi-Fi 네트워크를 검색하므로 최대 1분 정도 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="9ff3d-202">`Detected Networks` 드롭다운 목록에서 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="9ff3d-203">`Security` 드롭다운 목록에서 네트워크의 보안 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="9ff3d-204">로그인 및 암호 정보를 입력한 다음 `Configure Wi-Fi`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="9ff3d-205">나중에 사용되는 IP 주소에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="9ff3d-206">Edison이 컴퓨터와 같은 네트워크에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="9ff3d-207">해당 IP 주소를 사용하여 컴퓨터가 Edison에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![온도 센서에 연결](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="9ff3d-209">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-209">Congratulations!</span></span> <span data-ttu-id="9ff3d-210">Edison 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="9ff3d-211">Intel Edison에 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9ff3d-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="9ff3d-212">Azure IoT 장치 SDK 준비</span><span class="sxs-lookup"><span data-stu-id="9ff3d-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="9ff3d-213">호스트 컴퓨터에서 다음 SSH 클라이언트 중 하나를 사용하여 Intel Edison에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="9ff3d-214">IP 주소는 구성 도구에서 가져오며, 암호는 해당 도구에서 설정한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="9ff3d-215">Windows용 [PuTTY](http://www.putty.org/)</span><span class="sxs-lookup"><span data-stu-id="9ff3d-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="9ff3d-216">Ubuntu 또는 macOS에 있는 기본 제공 SSH 클라이언트(`ssh root@"the IP address"` 실행)</span><span class="sxs-lookup"><span data-stu-id="9ff3d-216">The built-in SSH client on Ubuntu or macOS (run `ssh root@"the IP address"`).</span></span>

2. <span data-ttu-id="9ff3d-217">장치에 샘플 클라이언트 앱을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="9ff3d-218">그런 후 repo 폴더로 이동한 후 다음 명령을 실행하여 Azure IoT SDK를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-the-sample-application"></a><span data-ttu-id="9ff3d-219">샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="9ff3d-219">Configure the sample application</span></span>

1. <span data-ttu-id="9ff3d-220">다음 명령을 실행하여 config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Config 파일](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="9ff3d-222">이 파일에는 사용자가 구성할 수 있는 두 개의 매크로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="9ff3d-223">첫 번째는 클라우드로 전송되는 두 메시지 사이의 간격을 정의하는 `INTERVAL`입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="9ff3d-224">두 번째는 시뮬레이션된 센서 데이터의 사용 여부에 대한 부울 값인 `SIMULATED_DATA`입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="9ff3d-225">**센서가 없는 경우** `SIMULATED_DATA` 값을 `1`로 설정하여 샘플 응용 프로그램에서 시뮬레이션된 센서 데이터를 만들어서 사용하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="9ff3d-226">Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="9ff3d-227">응용 프로그램 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="9ff3d-227">Build and run the sample application</span></span>

1. <span data-ttu-id="9ff3d-228">다음 명령을 실행하여 샘플 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![빌드 출력](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="9ff3d-230">다음 명령을 실행하여 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="9ff3d-231">장치 연결 문자열을 복사하여 작은따옴표 안에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="9ff3d-232">IoT Hub로 전송되는 센서 데이터와 메시지를 보여 주는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![출력 - Intel Edison에서 IoT Hub로 전송된 센서 데이터](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="9ff3d-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ff3d-234">Next steps</span></span>

<span data-ttu-id="9ff3d-235">샘플 응용 프로그램을 실행하여 센서 데이터를 수집하고 IoT Hub로 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3d-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
