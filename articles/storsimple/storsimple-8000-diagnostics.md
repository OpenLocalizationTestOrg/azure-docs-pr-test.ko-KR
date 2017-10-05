---
title: "StorSimple 8000 장치 문제 해결을 위한 진단 도구 | Microsoft Docs"
description: "StorSimple 장치 모드 및 StorSimple용 Windows PowerShell을 사용하여 장치 모드를 변경하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="47050-103">StorSimple 진단 도구를 사용하여 8000 시리즈 장치 문제 해결</span><span class="sxs-lookup"><span data-stu-id="47050-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="47050-104">개요</span><span class="sxs-lookup"><span data-stu-id="47050-104">Overview</span></span>

<span data-ttu-id="47050-105">StorSimple 진단 도구는 StorSimple 장치에 대한 시스템, 성능, 네트워크 및 하드웨어 구성 요소 상태와 관련된 문제를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="47050-106">진단 도구는 다양한 시나리오에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="47050-107">이러한 시나리오에는 워크로드 계획, StorSimple 장치 배포, 네트워크 환경 평가 및 작동 가능 장치의 성능을 결정하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="47050-108">이 문서에서는 진단 도구에 대한 개요와 도구를 StorSimple 장치와 함께 사용할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="47050-109">진단 도구는 주로 StorSimple 8000 시리즈 온-프레미스 장치(8100 및 8600)에 사용하도록 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="47050-110">진단 도구 실행</span><span class="sxs-lookup"><span data-stu-id="47050-110">Run diagnostics tool</span></span>

<span data-ttu-id="47050-111">이 도구는 사용자의 StorSimple 장치의 Windows PowerShell 인터페이스를 통해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="47050-112">사용자 장치의 로컬 인터페이스에 액세스하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="47050-113">[PuTTY를 사용하여 장치 직렬 콘솔에 연결합니다](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="47050-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="47050-114">[StorSimple용 Windows PowerShell을 통해 도구에 원격으로 액세스합니다](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="47050-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="47050-115">이 문서에서는 PuTTY를 통해 장치 직렬 콘솔에 연결한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="47050-116">진단 도구를 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-116">To run the diagnostics tool</span></span>

<span data-ttu-id="47050-117">장치의 Windows PowerShell 인터페이스에 연결한 후 다음 단계를 수행하여 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="47050-118">[장치 직렬 콘솔 연결에 PuTTY 사용](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)단계를 수행하여 장치 직렬 콘솔에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="47050-119">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="47050-120">범위 매개 변수를 지정하지 않으면 cmdlet은 모든 진단 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="47050-121">이러한 테스트에는 시스템, 하드웨어 구성 요소 상태, 네트워크 및 성능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="47050-122">특정 테스트만 실행하려면 범위 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="47050-123">예를 들어,네트워크 테스트만 실행하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="47050-124">PuTTY 창에서 출력을 선택하여 추가 분석을 위해 텍스트 파일로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="47050-125">진단 도구를 사용하기 위한 시나리오</span><span class="sxs-lookup"><span data-stu-id="47050-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="47050-126">진단 도구를 사용하여 시스템의 네트워크, 성능, 시스템 및 하드웨어 상태 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="47050-127">몇 가지 가능한 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="47050-128">**장치 오프라인** - 사용자의 StorSimple 8000 시리즈 장치가 오프라인 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="47050-129">단, Windows PowerShell 인터페이스에서 두 컨트롤러가 모두 켜져 있고 실행 중인 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="47050-130">이 도구를 사용하여 네트워크 상태를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="47050-131">등록(또는 설치 마법사를 통해 구성)하기 전에는 이 도구를 사용하여 장치의 성능 및 네트워크 설정을 평가하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="47050-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="47050-132">설치 마법사 및 등록하는 과정에서 유효한 IP가 장치에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="47050-133">등록되지 않은 장치에서 하드웨어 상태 및 시스템에 대해 이 cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="47050-134">다음과 같이 범위 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="47050-135">**영구 장치 문제** - 영구적으로 보이는 장치 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="47050-136">예를 들어 등록에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-136">For instance, registration is failing.</span></span> <span data-ttu-id="47050-137">장치를 성공적으로 등록하고 잠시 동안 작동하다가도 장치 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="47050-138">이 경우 Microsoft 지원에 서비스 요청을 로그하기 전에 임시 문제 해결에 대한 이 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="47050-139">이 도구를 실행하고 이 도구의 출력을 캡처하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="47050-140">그런 다음, 문제 해결을 더 신속하게 처리하기 위해 이 출력을 지원에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="47050-141">하드웨어 구성 요소 또는 클러스터 오류가 발생하는 경우 지원 요청에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="47050-142">**낮은 장치 성능** - 사용자의 StorSimple 장치 속도가 느립니다.</span><span class="sxs-lookup"><span data-stu-id="47050-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="47050-143">이 경우 성능으로 설정된 범위 매개 변수로 이 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="47050-144">출력을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-144">Analyze the output.</span></span> <span data-ttu-id="47050-145">클라우드 읽기-쓰기 대기 시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47050-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="47050-146">보고된 대기 시간을 최대 달성 가능한 대상으로 사용하고, 내부 데이터 처리에 일부 오버헤드를 고려한 다음, 시스템에 워크로드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="47050-147">자세한 정보는 [네트워크 테스트를 사용하여 장치 성능 문제 해결](#network-test)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47050-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="47050-148">진단 테스트 및 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="47050-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="47050-149">하드웨어 테스트</span><span class="sxs-lookup"><span data-stu-id="47050-149">Hardware test</span></span>

<span data-ttu-id="47050-150">이 테스트는 하드웨어 구성 요소, USM 펌웨어 및 시스템에서 실행되는 디스크 펌웨어의 상태를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="47050-151">보고된 하드웨어 구성 요소는 테스트에 실패하였거나 시스템에 존재하지 않는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="47050-152">USM 펌웨어 및 디스크 펌웨어 버전은 사용자의 시스템에서 Controller 0, Controller 1 및 공유 구성 요소에 대해 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="47050-153">하드웨어 구성 요소의 전체 목록은 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="47050-154">기본 인클로저의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="47050-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="47050-155">EBOD 인클로저의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="47050-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="47050-156">하드웨어 테스트에서 실패한 구성 요소를 보고하는 경우 [Microsoft 지원으로 서비스 요청에 로그인](storsimple-contact-microsoft-support.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="47050-157">8100 장치에서 실행되는 하드웨어 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="47050-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="47050-158">다음은 StorSimple 8100 장치의 샘플 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="47050-159">8100 모델 장치에 EBOD 인클로저는 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="47050-160">따라서 EBOD 컨트롤러 구성 요소는 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-160">Hence, the EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="47050-161">시스템 테스트</span><span class="sxs-lookup"><span data-stu-id="47050-161">System test</span></span>

<span data-ttu-id="47050-162">이 테스트는 사용자 장치에 대한 시스템 정보, 사용 가능한 업데이트, 클러스터 정보 및 서비스 정보를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="47050-163">시스템 정보에는 시스템에서 실행되는 모델, 장치 일련 번호, 표준 시간대, 컨트롤러 상태 및 자세한 소프트웨어 버전이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="47050-164">출력으로 보고된 다양한 시스템 매개 변수를 이해하려면 [시스템 정보 해석](#appendix-interpreting-system-information)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="47050-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="47050-165">업데이트 가용성은 일반 및 유지 관리 모드를 사용할 수 있는지 여부와 연결된 패키지 이름을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="47050-166">`RegularUpdates` 및 `MaintenanceModeUpdates`가 `false`인 경우 이는 업데이트를 사용할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="47050-167">사용자 장치가 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="47050-168">클러스터 정보에는 모든 HCS 클러스터 그룹 및 해당 상태의 여러 논리 구성 요소에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="47050-169">보고서의 이 섹션에 오프라인 클러스터 그룹이 있는 경우 [Microsoft 지원으로 문의하세요](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="47050-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="47050-170">서비스 정보에는 사용자 장치에서 실행 중인 모든 HCS 및 CiS 서비스의 이름 및 상태가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="47050-171">이 정보는 장치 문제 해결 시 Microsoft 지원에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="47050-172">8100 장치에서 실행되는 시스템 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="47050-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="47050-173">다음은 8100 장치에서 실행되는 시스템 테스트의 샘플 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-173">Here is a sample output of the system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="47050-174">네트워크 테스트</span><span class="sxs-lookup"><span data-stu-id="47050-174">Network test</span></span>

<span data-ttu-id="47050-175">이 테스트는 사용자 StorSimple 장치의 네트워크 인터페이스, 포트, DNS 및 NTP 서버 연결, SSL 인증서, 저장소 계정 자격 증명, 업데이트 서버에 대한 연결 및 웹 프록시 연결 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="47050-176">DATA0만 사용하는 경우 네트워크 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="47050-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="47050-177">다음은 8100 장치의 샘플 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="47050-178">출력에서 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-178">You can see in the output that:</span></span>
* <span data-ttu-id="47050-179">DATA 0 및 DATA 1 네트워크 인터페이스만 사용하도록 설정 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="47050-180">DATA 2 - 5는 포털에서 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="47050-181">DNS 서버 구성은 유효하며 장치는 DNS 서버를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="47050-182">NTP 서버 연결도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="47050-183">포트 80 및 443이 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="47050-184">그러나 포트 9354는 차단되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="47050-185">[시스템 네트워크 요구 사항](storsimple-system-requirements.md)에 따라 Service Bus 통신에 대한 이 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="47050-186">SSL 인증이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="47050-187">장치를 저장소 계정인 _myss8000storageacct_에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="47050-188">업데이트 서버에 대한 연결이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="47050-189">이 장치에 대한 웹 프록시가 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="47050-190">DATA0 및 DATA1을 사용하는 경우 네트워크 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="47050-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="47050-191">성능 테스트</span><span class="sxs-lookup"><span data-stu-id="47050-191">Performance test</span></span>

<span data-ttu-id="47050-192">이 테스트는 사용자 장치에 대한 클라우드 읽기-쓰기 대기 시간을 통해 클라우드 성능을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="47050-193">이 도구는 StorSimple과 함께 얻을 수 있는 클라우드 성능 기준을 설정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="47050-194">도구는 사용자의 연결에서 얻을 수 있는 최대 성능(읽기-쓰기 대기 시간의 모범 사례 시나리오)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="47050-195">도구에서 달성 가능한 최대 성능을 보고하므로 작업 부하를 배포할 때 보고된 읽기-쓰기 대기 시간을 대상으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="47050-196">테스트는 장치의 다양한 볼륨 형식과 연결된 Blob 크기를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="47050-197">일반 계층화되고 로컬로 고정된 일반 볼륨의 백업은 64KB Blob 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="47050-198">선택된 보관 옵션을 사용하는 계층화된 볼륨은 512KB Blob 데이터 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="47050-199">사용자의 장치에 계층화되고 로컬로 고정된 볼륨이 구성되어 있는 경우 64KB Blob 데이터 크기에 해당하는 테스트만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="47050-200">이 도구를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="47050-201">첫째, 계층화된 볼륨과 선택된 보관 옵션을 사용하는 계층화된 볼륨의 조합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47050-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="47050-202">이 작업은 도구에서 64KB와 512KB Blob 크기 모두에 대한 테스트를 실행하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="47050-203">볼륨을 만들고 구성한 후 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="47050-204">형식:</span><span class="sxs-lookup"><span data-stu-id="47050-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="47050-205">도구에서 보고된 읽기-쓰기 대기 시간을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="47050-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="47050-206">이 테스트는 결과를 보고하기 전에 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="47050-207">연결 대기 시간이 모두 예상된 범위 내인 경우 작업 부하를 배포할 때 도구에서 보고된 대기 시간을 달성 가능한 최대 대상으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="47050-208">내부 데이터 처리를 위해 약간의 오버헤드를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="47050-209">진단 도구에서 보고된 읽기-쓰기 대기 시간이 너무 높은 경우:</span><span class="sxs-lookup"><span data-stu-id="47050-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="47050-210">Azure Storage 계정에 대한 대기 시간을 이해하기 위해 Blob services에 대한 저장소 분석을 구성하고 출력을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="47050-211">자세한 지침은 [저장소 분석 설정 및 구성](../storage/common/storage-enable-and-view-metrics.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="47050-212">그러한 대기 시간이 높고 StorSimple 진단 도구에서 수신한 숫자와 비교 가능한 경우 Azure Storage로 서비스 요청을 로그해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="47050-213">저장소 계정 대기 시간이 너무 낮은 경우 사용자 네트워크의 대기 시간 문제 조사를 위해 네트워크 관리자에게 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="47050-214">8100 장치에서 실행되는 성능 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="47050-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="47050-215">부록: 시스템 정보 해석</span><span class="sxs-lookup"><span data-stu-id="47050-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="47050-216">다음은 매핑할 시스템 정보의 다양한 Windows PowerShell 매개 변수를 설명하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="47050-217">PowerShell 매개 변수</span><span class="sxs-lookup"><span data-stu-id="47050-217">PowerShell Parameter</span></span>    | <span data-ttu-id="47050-218">설명</span><span class="sxs-lookup"><span data-stu-id="47050-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="47050-219">인스턴스 ID</span><span class="sxs-lookup"><span data-stu-id="47050-219">Instance ID</span></span>             | <span data-ttu-id="47050-220">모든 컨트롤러에는 고유 식별자 또는 연결된 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="47050-221">이름</span><span class="sxs-lookup"><span data-stu-id="47050-221">Name</span></span>                    | <span data-ttu-id="47050-222">장치를 배포하는 동안 Azure Portal을 통해 구성된 장치의 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="47050-223">기본 친숙한 이름은 장치 일련 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="47050-224">모델</span><span class="sxs-lookup"><span data-stu-id="47050-224">Model</span></span>                   | <span data-ttu-id="47050-225">사용자 StorSimple 8000 시리즈 장치의 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="47050-226">모델은 8100 또는 8600일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="47050-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="47050-227">SerialNumber</span></span>            | <span data-ttu-id="47050-228">장치 일련 번호는 공장에서 할당되고 길이가 15자입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="47050-229">예를 들어, 8600-SHX0991003G44HT는 다음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="47050-230">8600 – 장치 모델을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-230">8600 – Is the device model.</span></span><br><span data-ttu-id="47050-231">SHX – 제조 사이트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="47050-232">0991003 - 특정 제품을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="47050-233">G44HT - 마지막 5자리 숫자는 고유한 일련 번호를 만들기 위해 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="47050-234">순차적인 집합이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="47050-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="47050-235">TimeZone</span></span>                | <span data-ttu-id="47050-236">장치를 배포하는 동안 Azure Portal에서 구성된 장치 표준 시간대입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="47050-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="47050-237">CurrentController</span></span>       | <span data-ttu-id="47050-238">사용자 StorSimple 장치의 Windows PowerShell 인터페이스를 통해 연결한 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="47050-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="47050-239">ActiveController</span></span>        | <span data-ttu-id="47050-240">사용자 장치에서 활성 상태이며 모든 네트워크 및 디스크 작업을 제어하는 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="47050-241">이는 컨트롤러 0 또는 컨트롤러 1일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="47050-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="47050-242">Controller0Status</span></span>       | <span data-ttu-id="47050-243">사용자 장치에서 컨트롤러 0의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="47050-244">컨트롤러 상태는 일반, 복구 모드 또는 연결할 수 없는 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="47050-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="47050-245">Controller1Status</span></span>       | <span data-ttu-id="47050-246">사용자 장치에서 컨트롤러 1의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="47050-247">컨트롤러 상태는 일반, 복구 모드 또는 연결할 수 없는 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="47050-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="47050-248">SystemMode</span></span>              | <span data-ttu-id="47050-249">StorSimple 장치의 전반적인 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="47050-250">장치 상태는 일반, 유지 관리 또는 서비스 해제됨(Azure Portal에서 비활성화에 해당) 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="47050-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="47050-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="47050-252">장치 소프트웨어 버전에 해당하는 친숙한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="47050-253">업데이트 4를 실행하는 시스템의 경우 친숙한 소프트웨어 버전은 StorSimple 8000 시리즈 업데이트 4.0입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="47050-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="47050-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="47050-255">사용자 장치에서 실행되는 HCS 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-255">The HCS software version running on your device.</span></span> <span data-ttu-id="47050-256">예를 들어, StorSimple 8000 시리즈 업데이트 4.0에 해당하는 HCS 소프트웨어 버전은 6.3.9600.17820입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="47050-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="47050-257">ApiVersion</span></span>              | <span data-ttu-id="47050-258">HCS 장치의 Windows PowerShell API의 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="47050-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="47050-259">VhdVersion</span></span>              | <span data-ttu-id="47050-260">장치와 함께 제공된 출하 시 이미지의 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="47050-261">사용자 장치를 공장 기본값으로 다시 설정한 경우 이 소프트웨어 버전을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="47050-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="47050-262">OSVersion</span></span>               | <span data-ttu-id="47050-263">장치에서 실행 중인 Windows Server 운영 체제의 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="47050-264">StorSimple 장치는 6.3.9600에 해당하는 Windows Server 2012 R2를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="47050-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="47050-265">CisAgentVersion</span></span>         | <span data-ttu-id="47050-266">사용자의 StorSimple 장치에서 실행되는 사용자의 Cis 에이전트에 대한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="47050-267">이 에이전트는 Azure에서 실행되는 StorSimple Manager 서비스와 통신하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47050-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="47050-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="47050-268">MdsAgentVersion</span></span>         | <span data-ttu-id="47050-269">사용자의 StorSimple 장치에서 실행되는 사용자의 Mds 에이전트에 해당하는 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="47050-270">이 에이전트는 MDS(모니터링 및 진단 서비스)로 데이터를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="47050-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="47050-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="47050-271">Lsisas2Version</span></span>          | <span data-ttu-id="47050-272">사용자의 StorSimple 장치에서 LSI 드라이버에 해당하는 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="47050-273">용량</span><span class="sxs-lookup"><span data-stu-id="47050-273">Capacity</span></span>                | <span data-ttu-id="47050-274">장치의 총 용량(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="47050-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="47050-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="47050-275">RemoteManagementMode</span></span>    | <span data-ttu-id="47050-276">Windows PowerShell 인터페이스를 통해 장치를 원격으로 관리할 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="47050-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="47050-277">FipsMode</span></span>                | <span data-ttu-id="47050-278">사용자의 장치에서 미국 FIPS(Federal Information Processing Standard) 모드를 사용할 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47050-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="47050-279">FIPS 140 표준은 중요한 데이터의 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인된 암호화 알고리즘을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="47050-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="47050-280">업데이트 4 이상을 실행하는 장치의 경우 FIPS 모드는 기본적으로 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47050-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47050-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47050-281">Next steps</span></span>

* <span data-ttu-id="47050-282">[Invoke-HcsDiagnostics cmdlet의 구문](https://technet.microsoft.com/library/mt795371.aspx)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="47050-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="47050-283">사용자의 StorSimple 장치에서 [배포 문제 해결](storsimple-troubleshoot-deployment.md) 방법에 대한 자세한 정보를 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="47050-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
