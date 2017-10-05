---
title: "Azure IoT에 Intel Edison(C) 연결 - 단원 1: 장치 구성 | Microsoft Docs"
description: "처음 사용을 위한 Intel Edison을 구성합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 설정, PC에 arduino 연결, arduino 설정, arduino 보드"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="dd6f6-104">Intel Edison 구성</span><span class="sxs-lookup"><span data-stu-id="dd6f6-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="dd6f6-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="dd6f6-105">What you will do</span></span>
<span data-ttu-id="dd6f6-106">보드를 조립하고, 전원을 켜고, 데스크톱 OS에 구성 도구를 설치하여 Edison 펌웨어를 플래시하고, 해당 암호를 설정한 후 Wi-Fi에 연결하여 처음 사용할 수 있게 Intel Edison을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="dd6f6-107">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dd6f6-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="dd6f6-108">What you will learn</span></span>
<span data-ttu-id="dd6f6-109">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-109">In this article, you will learn:</span></span>

* <span data-ttu-id="dd6f6-110">Edison 보드를 조립하고 전원을 켜는 방법</span><span class="sxs-lookup"><span data-stu-id="dd6f6-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="dd6f6-111">Edison 펌웨어를 플래시하고, 암호를 설정하고, Wi-Fi를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="dd6f6-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dd6f6-112">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="dd6f6-112">What you need</span></span>
<span data-ttu-id="dd6f6-113">이 작업을 완료하려면 Intel Edison 시작 키트에서 다음 부품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="dd6f6-114">Intel® Edison 모듈</span><span class="sxs-lookup"><span data-stu-id="dd6f6-114">Intel® Edison module</span></span>
* <span data-ttu-id="dd6f6-115">Arduino 확장 보드</span><span class="sxs-lookup"><span data-stu-id="dd6f6-115">Arduino expansion board</span></span>
* <span data-ttu-id="dd6f6-116">포장에 포함된 스페이서 바 또는 나사(모듈을 확장 보드에 고정하기 위한 2개의 나사와 4개의 나사 세트 및 플라스틱 스페이서 포함)</span><span class="sxs-lookup"><span data-stu-id="dd6f6-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="dd6f6-117">Micro B-A형 USB 케이블</span><span class="sxs-lookup"><span data-stu-id="dd6f6-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="dd6f6-118">DC(직류) 전원 공급 장치</span><span class="sxs-lookup"><span data-stu-id="dd6f6-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="dd6f6-119">전원 공급 장치 정격은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="dd6f6-120">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="dd6f6-120">7-15V DC</span></span>
  - <span data-ttu-id="dd6f6-121">1500mA 이상</span><span class="sxs-lookup"><span data-stu-id="dd6f6-121">At least 1500mA</span></span>
  - <span data-ttu-id="dd6f6-122">중앙/내부 핀은 전원 공급 장치의 양극이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![시작 키트의 항목](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="dd6f6-124">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-124">You also need:</span></span>

* <span data-ttu-id="dd6f6-125">Windows, Mac 또는 Linux를 실행하는 컴퓨터 </span><span class="sxs-lookup"><span data-stu-id="dd6f6-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="dd6f6-126">Edison을 연결할 무선 연결</span><span class="sxs-lookup"><span data-stu-id="dd6f6-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="dd6f6-127">구성 도구를 다운로드하기 위한 인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="dd6f6-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="dd6f6-128">보드 조립</span><span class="sxs-lookup"><span data-stu-id="dd6f6-128">Assemble your board</span></span>

<span data-ttu-id="dd6f6-129">이 섹션에는 Intel® Edison 모듈을 확장 보드를 연결하는 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="dd6f6-130">확장 보드의 흰색 윤곽 안에 Intel® Edison 모듈을 놓고 모듈의 구멍과 확장 보드의 나사를 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="dd6f6-131">딸깍 소리가 느껴질 때까지 `What will you make?` 아래에서 모듈을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![보드 2 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="dd6f6-133">2개의 육각 너트(포장에 포함)를 사용하여 모듈을 확장 보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![보드 3 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="dd6f6-135">확장 보드의 구석에 있는 4개 구멍 중 하나에 나사를 끼웁니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="dd6f6-136">흰색 플라스틱 스페너 중 하나를 돌려 나사를 조입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![보드 4 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="dd6f6-138">나머지 3개 구석의 스페이서에 대해 같은 작업을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-138">Repeat for the other three corner spacers.</span></span>

   ![보드 5 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="dd6f6-140">이제 보드가 조립됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-140">Now your board is assembled.</span></span>

   ![조립된 보드](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="dd6f6-142">Edison 전원 켜기</span><span class="sxs-lookup"><span data-stu-id="dd6f6-142">Power up Edison</span></span>

1. <span data-ttu-id="dd6f6-143">전원 공급 장치를 꽂습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-143">Plug in the power supply.</span></span>

   ![전원 공급 장치 꽂기](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="dd6f6-145">녹색 LED(Arduino* 확장 보드에 DS1으로 레이블 지정)가 켜진 후 계속 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="dd6f6-146">보드가 부팅을 마칠 때까지 1분 정도 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd6f6-147">DC 전원 공급 장치가 없으면 USB 포트를 통해 여전히 보드의 전원을 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="dd6f6-148">자세한 내용은 `Connect Edison to your computer` 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="dd6f6-149">이러한 방식으로 보드를 켜면 보드에서 예기치 않은 동작이 나타날 수 있습니다. 이러한 현상은 Wi-Fi 또는 구동 모터를 사용할 때 더욱 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="dd6f6-150">Edison을 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="dd6f6-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="dd6f6-151">Edison이 장치 모드가 되도록 2개의 마이크로 USB 포트 쪽으로 마이크로 스위치를 내립니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="dd6f6-152">장치 모드와 호스트 모드 간 차이점에 대해서는 [여기](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![마이크로 스위치 내리기](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="dd6f6-154">마이크로 USB 포트를 위쪽 마이크로 USB 케이블에 꽂습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![위쪽 마이크로 USB 포트](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="dd6f6-156">USB 케이블의 다른 쪽을 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-156">Plug the other end of USB cable into your computer.</span></span>

   ![컴퓨터 USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="dd6f6-158">컴퓨터에 새 장치를 탑재(컴퓨터에 SD 카드를 꽂는 것과 매우 유사함)할 때 보드가 완전히 초기화된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="dd6f6-159">구성 도구 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="dd6f6-159">Download and run the configuration tool</span></span>
<span data-ttu-id="dd6f6-160">`Installers` 제목 아래 나열된 [이 링크](https://software.intel.com/en-us/iot/hardware/edison/downloads)에서 최신 구성 도구를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="dd6f6-161">도구를 실행하고 화면 지시를 따른 다음 필요할 때 다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="dd6f6-162">펌웨어 플래시</span><span class="sxs-lookup"><span data-stu-id="dd6f6-162">Flash firmware</span></span>
1. <span data-ttu-id="dd6f6-163">`Set up options` 페이지에서 `Flash Firmware`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="dd6f6-164">다음 중 하나를 수행하여 보드에서 플래시할 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="dd6f6-165">Intel에서 사용 가능한 최신 펌웨어 이미지를 다운로드한 후 이 이미지로 보드를 플래시하려면 `Download the latest image version xxxx`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="dd6f6-166">컴퓨터에 이미 저장한 이미지로 보드를 플래시하려면 `Select the local image`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="dd6f6-167">보드에 플래시할 이미지를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="dd6f6-168">설치 도구는 보드를 플래시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="dd6f6-169">전체 플래시 프로세스는 10분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="dd6f6-170">암호 설정</span><span class="sxs-lookup"><span data-stu-id="dd6f6-170">Set password</span></span>
1. <span data-ttu-id="dd6f6-171">`Set up options` 페이지에서 `Enable Security`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="dd6f6-172">Intel® Edison 보드에 대한 사용자 지정 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="dd6f6-173">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-173">This is optional.</span></span>
3. <span data-ttu-id="dd6f6-174">보드에 대한 암호를 입력한 후 `Set password`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="dd6f6-175">나중에 사용되는 암호에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="dd6f6-176">Wi-Fi 연결</span><span class="sxs-lookup"><span data-stu-id="dd6f6-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="dd6f6-177">`Set up options` 페이지에서 `Connect Wi-Fi`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="dd6f6-178">컴퓨터가 사용할 수 있는 Wi-Fi 네트워크를 검색하므로 최대 1분 정도 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="dd6f6-179">`Detected Networks` 드롭다운 목록에서 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="dd6f6-180">`Security` 드롭다운 목록에서 네트워크의 보안 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="dd6f6-181">로그인 및 암호 정보를 입력한 다음 `Configure Wi-Fi`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="dd6f6-182">나중에 사용되는 IP 주소에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="dd6f6-183">Edison이 컴퓨터와 같은 네트워크에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="dd6f6-184">해당 IP 주소를 사용하여 컴퓨터가 Edison에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="dd6f6-185">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-185">Congratulations!</span></span> <span data-ttu-id="dd6f6-186">Edison 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="dd6f6-187">요약</span><span class="sxs-lookup"><span data-stu-id="dd6f6-187">Summary</span></span>
<span data-ttu-id="dd6f6-188">이 문서에서는 구성 도구를 사용하여 Edison 보드를 조립하고, 펌웨어를 플래시하고, 암호를 설정하고, Wi-Fi에 연결하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="dd6f6-189">아직 LED에는 불이 들어오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="dd6f6-190">다음 작업은 Edision에서 샘플 응용 프로그램 실행을 위한 준비로 필요한 도구 및 소프트웨어를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dd6f6-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd6f6-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd6f6-191">Next steps</span></span>
<span data-ttu-id="dd6f6-192">[도구 얻기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="dd6f6-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md