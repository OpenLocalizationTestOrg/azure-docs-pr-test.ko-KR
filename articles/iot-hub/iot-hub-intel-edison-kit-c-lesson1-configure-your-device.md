---
title: "Connect Intel Edison (C) tooAzure IoT-1 단원: 장치 구성 | Microsoft Docs"
description: "처음 사용을 위한 Intel Edison을 구성합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "설정, arduino arduino toopc, 설치 arduino, arduino 보드 연결"
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
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="67694-104">Intel Edison 구성</span><span class="sxs-lookup"><span data-stu-id="67694-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="67694-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="67694-105">What you will do</span></span>
<span data-ttu-id="67694-106">Hello 보드, 위로 전원을 어셈블하는 방법으로 처음에 대 한 Intel Edison를 구성 하 고 구성 도구 tooyour 데스크톱 OS tooflash 설치 Edison의 펌웨어 해당 암호를 설정 하 고 연결 tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="67694-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="67694-107">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="67694-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="67694-108">What you will learn</span></span>
<span data-ttu-id="67694-109">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67694-109">In this article, you will learn:</span></span>

* <span data-ttu-id="67694-110">Tooassemble Edison 보드 어떻게을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="67694-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="67694-111">Tooflash Edison 펌웨어 암호를 설정 하 고 Wi-fi 연결 방법</span><span class="sxs-lookup"><span data-stu-id="67694-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="67694-112">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="67694-112">What you need</span></span>
<span data-ttu-id="67694-113">toocomplete Intel Edison 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="67694-114">Intel® Edison 모듈</span><span class="sxs-lookup"><span data-stu-id="67694-114">Intel® Edison module</span></span>
* <span data-ttu-id="67694-115">Arduino 확장 보드</span><span class="sxs-lookup"><span data-stu-id="67694-115">Arduino expansion board</span></span>
* <span data-ttu-id="67694-116">모든 공백 막대 또는 나사 hello 패키징, 나사 두 toofasten hello 모듈 toohello 확장 보드 등의 나사와 플라스틱 스페이서 4 집합에에서 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="67694-117">마이크로 B tooType A USB 케이블</span><span class="sxs-lookup"><span data-stu-id="67694-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="67694-118">DC(직류) 전원 공급 장치</span><span class="sxs-lookup"><span data-stu-id="67694-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="67694-119">전원 공급 장치 정격은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="67694-120">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="67694-120">7-15V DC</span></span>
  - <span data-ttu-id="67694-121">1500mA 이상</span><span class="sxs-lookup"><span data-stu-id="67694-121">At least 1500mA</span></span>
  - <span data-ttu-id="67694-122">hello 센터/내부 pin hello 양수 극의 hello 전원 공급 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![시작 키트의 항목](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="67694-124">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-124">You also need:</span></span>

* <span data-ttu-id="67694-125">Windows, Mac 또는 Linux를 실행하는 컴퓨터 </span><span class="sxs-lookup"><span data-stu-id="67694-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="67694-126">Edison tooconnect에 대 한 무선 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="67694-127">인터넷 연결 toodownload 구성 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="67694-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="67694-128">보드 조립</span><span class="sxs-lookup"><span data-stu-id="67694-128">Assemble your board</span></span>

<span data-ttu-id="67694-129">이 섹션 단계 tooattach Intel® Edison 모듈 tooyour 확장 보드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="67694-130">Hello 확장 보드에 hello 나사 hello 모듈에 hello 허점 만나려고 프로그램 확장 보드에 흰색 hello 개요 내의 hello Intel® Edison 모듈을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="67694-131">Hello 단어 바로 아래 hello 모듈을 누르면 `What will you make?` 간단히 생각 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![보드 2 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="67694-133">Hello 두 (hello 패키지에 포함 됨) 하는 16 진수 너트 toosecure hello 모듈 toohello 확장 보드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![보드 3 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="67694-135">Hello 확장 보드에 네 개의 모퉁이 구멍 hello 중 하나에 나사를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="67694-136">비틀 및 hello 나사에 흰색 hello 플라스틱 스페이서 중 하나를 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![보드 4 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="67694-138">반복에 대 한 다른 3 개의 모퉁이 스페이서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-138">Repeat for hello other three corner spacers.</span></span>

   ![보드 5 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="67694-140">이제 보드가 조립됩니다.</span><span class="sxs-lookup"><span data-stu-id="67694-140">Now your board is assembled.</span></span>

   ![조립된 보드](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="67694-142">Edison 전원 켜기</span><span class="sxs-lookup"><span data-stu-id="67694-142">Power up Edison</span></span>

1. <span data-ttu-id="67694-143">Hello 전원 공급 장치에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-143">Plug in hello power supply.</span></span>

   ![전원 공급 장치 꽂기](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="67694-145">(DS1 hello Arduino * 확장 보드에 표시) 녹색 led가 켜지 고 켜져 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="67694-146">Hello 보드 toofinish 부팅에 대 일 분 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="67694-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="67694-147">DC 전원 공급 장치가 하면 전원 hello 보드 USB 포트를 통해 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67694-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="67694-148">자세한 내용은 `Connect Edison tooyour computer` 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67694-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="67694-149">이러한 방식으로 보드를 켜면 보드에서 예기치 않은 동작이 나타날 수 있습니다. 이러한 현상은 Wi-Fi 또는 구동 모터를 사용할 때 더욱 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="67694-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="67694-150">Edison tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="67694-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="67694-151">Edison 장치 모드는 hello 두 마이크로 USB 포트에 대 한 hello 마이크로 스위치를 설정/해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="67694-152">장치 모드와 호스트 모드 간 차이점에 대해서는 [여기](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67694-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Hello 마이크로 스위치를 설정/해제](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="67694-154">Hello 상위 마이크로 USB 포트에 hello 마이크로 USB 케이블을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![위쪽 마이크로 USB 포트](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="67694-156">플러그를 컴퓨터에 USB 케이블의 다른 쪽 끝을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-156">Plug hello other end of USB cable into your computer.</span></span>

   ![컴퓨터 USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="67694-158">컴퓨터에 새 장치를 탑재(컴퓨터에 SD 카드를 꽂는 것과 매우 유사함)할 때 보드가 완전히 초기화된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="67694-159">다운로드 하 고 hello 구성 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="67694-160">Hello 최신 구성 도구에서 가져올 [이 링크](https://software.intel.com/en-us/iot/hardware/edison/downloads) hello 아래에 나열 `Installers` 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="67694-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="67694-161">Hello 도구를 실행 하 고에 따라 해당 화면에 나타나는 지침, 필요한 경우 다음을 클릭</span><span class="sxs-lookup"><span data-stu-id="67694-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="67694-162">펌웨어 플래시</span><span class="sxs-lookup"><span data-stu-id="67694-162">Flash firmware</span></span>
1. <span data-ttu-id="67694-163">Hello에 `Set up options` 페이지 `Flash Firmware`합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="67694-164">보드에 hello 이미지 tooflash hello 다음 중 하나를 수행 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="67694-165">보드 hello 최신 펌웨어 이미지와 Intel에서 사용할 수 있는 선택 toodownload 및 플래시 `Download hello latest image version xxxx`합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="67694-166">tooflash 이미 컴퓨터에 저장 한 이미지와 함께 보드 선택 `Select hello local image`합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="67694-167">Tooflash tooyour 게시판 tooand 선택 hello 이미지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="67694-168">hello 설치 도구 tooflash 보드를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="67694-169">hello 전체 깜박이 프로세스는 too10 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="67694-170">암호 설정</span><span class="sxs-lookup"><span data-stu-id="67694-170">Set password</span></span>
1. <span data-ttu-id="67694-171">Hello에 `Set up options` 페이지 `Enable Security`합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="67694-172">Intel® Edison 보드에 대한 사용자 지정 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="67694-173">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="67694-173">This is optional.</span></span>
3. <span data-ttu-id="67694-174">보드에 대한 암호를 입력한 후 `Set password`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="67694-175">나중에 사용 되는 hello 암호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="67694-176">Wi-Fi 연결</span><span class="sxs-lookup"><span data-stu-id="67694-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="67694-177">Hello에 `Set up options` 페이지 `Connect Wi-Fi`합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="67694-178">사용 가능한 Wi-fi 네트워크에 대 한 컴퓨터 검색으로 tooone 분을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="67694-179">Hello에서 `Detected Networks` 드롭 다운 목록에서 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="67694-180">Hello에서 `Security` 드롭 다운 목록, 선택 hello 네트워크의 보안 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="67694-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="67694-181">로그인 및 암호 정보를 입력한 다음 `Configure Wi-Fi`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="67694-182">Hello 아래로 나중에 사용 되는 IP 주소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="67694-183">Edison 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="67694-184">Edison tooyour hello IP 주소를 사용 하 여 연결 하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="67694-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="67694-185">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="67694-185">Congratulations!</span></span> <span data-ttu-id="67694-186">Edison 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="67694-187">요약</span><span class="sxs-lookup"><span data-stu-id="67694-187">Summary</span></span>
<span data-ttu-id="67694-188">이 문서에서는 tooassemble를 Edison 보드 hello, 해당 펌웨어, 설정 암호 플래시 및 구성 도구를 사용 하 여 tooWi-Fi 연결 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="67694-189">Note 해당 hello LED가 켜 아직 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67694-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="67694-190">hello 다음 작업은 tooinstall hello 필요한 도구 및 Edison에서 샘플 응용 프로그램을 실행 하는 준비 과정에서 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="67694-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67694-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67694-191">Next steps</span></span>
<span data-ttu-id="67694-192">[Hello 도구 가져오기][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="67694-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md