---
title: "aaaDiagnostics 도구 tootroubleshoot StorSimple 8000 장치 | Microsoft Docs"
description: "Hello StorSimple 장치 모드에 설명 하 고 설명 방법을 toochange StorSimple에 대 한 Windows PowerShell toouse hello 장치 모드입니다."
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
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="ffe8e-103">Hello StorSimple 진단 도구 tootroubleshoot 8000 시리즈 장치 문제를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ffe8e-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="ffe8e-104">개요</span><span class="sxs-lookup"><span data-stu-id="ffe8e-104">Overview</span></span>

<span data-ttu-id="ffe8e-105">hello StorSimple 진단 도구는 문제 관련된 toosystem, 성능, 네트워크 및 StorSimple 장치에 대 한 하드웨어 구성 요소 상태를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="ffe8e-106">hello 진단 도구는 다양 한 시나리오에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="ffe8e-107">이러한 시나리오에는 작업 계획, StorSimple 장치 배포, hello 네트워크 환경을 평가 및 작동 하는 장치의 hello 성능을 결정 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="ffe8e-108">이 문서에서는 hello 진단 도구에 대해 간략하게 설명 하 고 StorSimple 장치와 hello 도구를 사용할 수 있는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="ffe8e-109">hello 진단 도구는 주로 (8100 및 8600) StorSimple 8000 시리즈 온-프레미스 장치에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="ffe8e-110">진단 도구 실행</span><span class="sxs-lookup"><span data-stu-id="ffe8e-110">Run diagnostics tool</span></span>

<span data-ttu-id="ffe8e-111">StorSimple 장치의 Windows PowerShell 인터페이스 hello 통해이 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="ffe8e-112">두 가지 방법으로 tooaccess hello 장치의 로컬 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="ffe8e-113">[사용 하 여 장치 직렬 콘솔 PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="ffe8e-114">[StorSimple 용 Windows PowerShell hello 통해 hello 도구에 원격으로 액세스](storsimple-remote-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="ffe8e-115">이 문서에서는 toohello PuTTY 통해 장치 직렬 콘솔 연결을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="ffe8e-116">toorun hello 진단 도구</span><span class="sxs-lookup"><span data-stu-id="ffe8e-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="ffe8e-117">Hello 장치의 toohello Windows PowerShell 인터페이스를 연결 하 고 나면 다음 단계 toorun hello cmdlet hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="ffe8e-118">Hello 단계를 수행 하 여 toohello 장치 직렬 콘솔에 로그온 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="ffe8e-119">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="ffe8e-120">Hello scope 매개 변수를 지정 하지 않으면 hello cmdlet 모든 hello 진단 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="ffe8e-121">이러한 테스트에는 시스템, 하드웨어 구성 요소 상태, 네트워크 및 성능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="ffe8e-122">특정 테스트 toorun hello 범위 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="ffe8e-123">예를 들어, toorun 유일한 hello 네트워크 테스트, 형식</span><span class="sxs-lookup"><span data-stu-id="ffe8e-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="ffe8e-124">선택 하 고 hello 출력 hello PuTTY에서에서 복사 추가 분석을 위해 텍스트 파일에는 창입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="ffe8e-125">시나리오 toouse hello 진단 도구</span><span class="sxs-lookup"><span data-stu-id="ffe8e-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="ffe8e-126">Hello 진단 도구 tootroubleshoot hello 네트워크, 성능, 시스템 및 하드웨어 시스템의 상태 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="ffe8e-127">몇 가지 가능한 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="ffe8e-128">**장치 오프라인** - 사용자의 StorSimple 8000 시리즈 장치가 오프라인 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="ffe8e-129">그러나 hello Windows PowerShell 인터페이스에서 같습니다 hello 두 컨트롤러가 모두 실행 되 고 지.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="ffe8e-130">이 도구를 사용 하면 toothen hello 네트워크 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="ffe8e-131">Hello 등록 (또는 설치 마법사를 통해 구성) 하기 전에 장치에서이 도구 tooassess 성능 및 네트워크 설정을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="ffe8e-132">유효한 IP 설치 마법사 및 등록 하는 동안 toohello 장치를 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="ffe8e-133">등록되지 않은 장치에서 하드웨어 상태 및 시스템에 대해 이 cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="ffe8e-134">예를 들어 hello 범위 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="ffe8e-135">**영구 장치 문제** -toopersist 것 장치 문제가 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="ffe8e-136">예를 들어 등록에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-136">For instance, registration is failing.</span></span> <span data-ttu-id="ffe8e-137">또한 발생할 수 있습니다 장치 문제 hello 장치가 성공적으로 등록 하 고 작업을 잠시 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="ffe8e-138">이 경우 Microsoft 지원에 서비스 요청을 로그하기 전에 임시 문제 해결에 대한 이 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="ffe8e-139">이 도구 및 캡처 hello 출력이 도구를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="ffe8e-140">그런 다음이 출력 tooSupport tooexpedite 문제 해결을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="ffe8e-141">하드웨어 구성 요소 또는 클러스터 오류가 발생하는 경우 지원 요청에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="ffe8e-142">**낮은 장치 성능** - 사용자의 StorSimple 장치 속도가 느립니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="ffe8e-143">이 경우이 cmdlet을 범위 매개 변수 집합 tooperformance 함께 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="ffe8e-144">Hello 출력을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-144">Analyze hello output.</span></span> <span data-ttu-id="ffe8e-145">읽기 / 쓰기 대기 시간이 hello 클라우드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="ffe8e-146">사용 하 여 hello 대기 시간이 최대 달성 가능한 대상으로 hello 내부 데이터 처리에 대 한 약간의 오버 헤드에 모아 놓은 다음 hello 시스템에 hello 워크 로드를 배포를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="ffe8e-147">자세한 내용은 이동 너무[hello 네트워크 tootroubleshoot 장치 성능 테스트를 사용 하 여](#network-test)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="ffe8e-148">진단 테스트 및 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ffe8e-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="ffe8e-149">하드웨어 테스트</span><span class="sxs-lookup"><span data-stu-id="ffe8e-149">Hardware test</span></span>

<span data-ttu-id="ffe8e-150">이 테스트는 hello 하드웨어 구성 요소, hello USM 펌웨어 및 시스템에서 실행 하는 hello 디스크 펌웨어의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="ffe8e-151">보고 hello 하드웨어 구성 요소는 해당 구성 요소 실패 한 hello 테스트 또는 hello 시스템에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="ffe8e-152">hello USM 펌웨어와 디스크 펌웨어 버전 hello 컨트롤러 0, 컨트롤러 1에 대 한 보고 되 고 시스템의 공유 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="ffe8e-153">하드웨어 구성 요소의 전체 목록은 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="ffe8e-154">기본 인클로저의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ffe8e-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="ffe8e-155">EBOD 인클로저의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ffe8e-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="ffe8e-156">Hello 하드웨어 테스트 실패 한 구성 요소를 보고 하는 경우 [Microsoft 지원 인 서비스 요청은 로그인](storsimple-contact-microsoft-support.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="ffe8e-157">8100 장치에서 실행되는 하드웨어 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ffe8e-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="ffe8e-158">다음은 StorSimple 8100 장치의 샘플 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="ffe8e-159">EBOD 인클로저 hello hello 8100 모델 장치에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="ffe8e-160">따라서 hello EBOD 컨트롤러 구성 요소 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-160">Hence, hello EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="ffe8e-161">시스템 테스트</span><span class="sxs-lookup"><span data-stu-id="ffe8e-161">System test</span></span>

<span data-ttu-id="ffe8e-162">이 테스트는 hello 시스템 정보, 사용 가능한 hello 업데이트, hello 클러스터 정보 및 장치에 대 한 hello 서비스 정보를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="ffe8e-163">hello 모델, 장치 일련 번호, 표준 시간대, 컨트롤러의 상태 및 hello 시스템에서 실행 중인 hello 자세한 소프트웨어 버전 hello 시스템 정보에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="ffe8e-164">다양 한 너무 이동 시스템 매개 변수는 hello 출력으로 보고 toounderstand hello[시스템 정보를 해석 하](#appendix-interpreting-system-information)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="ffe8e-165">hello 업데이트 가용성 hello 일반 연결 및 유지 관리 모드를 사용할 수 있는지 여부를 보고 하 고 연결 된 패키지 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="ffe8e-166">경우 `RegularUpdates` 및 `MaintenanceModeUpdates` 는 `false`, hello 업데이트 제공 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="ffe8e-167">사용자 장치가 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="ffe8e-168">hello 클러스터 정보 모든 hello HCS 클러스터 그룹 및 해당 상태의 다양 한 논리적 구성 요소에 hello 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="ffe8e-169">Hello 보고서의이 섹션에 있는 오프 라인 클러스터 그룹에 표시 되 면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="ffe8e-170">hello 이름과 모든 hello HCS의 상태 및 장치에서 실행 되는 Ci 서비스 hello 서비스 정보에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="ffe8e-171">이 정보는 hello 장치 문제 해결에 hello Microsoft 지원에 대 한 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="ffe8e-172">8100 장치에서 실행되는 시스템 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ffe8e-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="ffe8e-173">8100 장치에서 실행 하는 hello 시스템 테스트의 샘플 출력 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="ffe8e-174">네트워크 테스트</span><span class="sxs-lookup"><span data-stu-id="ffe8e-174">Network test</span></span>

<span data-ttu-id="ffe8e-175">이 테스트는 hello 네트워크 인터페이스, 포트, DNS 및 NTP 서버 간의 연결, SSL 인증서, 저장소 계정 자격 증명, 연결 toohello 업데이트 서버 및 StorSimple 장치에서 웹 프록시 연결 hello 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="ffe8e-176">DATA0만 사용하는 경우 네트워크 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ffe8e-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="ffe8e-177">다음은 hello 8100 장치의 샘플 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="ffe8e-178">Hello 출력에서 볼 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-178">You can see in hello output that:</span></span>
* <span data-ttu-id="ffe8e-179">DATA 0 및 DATA 1 네트워크 인터페이스만 사용하도록 설정 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="ffe8e-180">데이터 2-5 hello 포털에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="ffe8e-181">hello DNS 서버 구성이 올바른지와 hello 장치 hello DNS 서버를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="ffe8e-182">hello NTP 서버 연결 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="ffe8e-183">포트 80 및 443이 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="ffe8e-184">그러나 포트 9354는 차단되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="ffe8e-185">Hello에 따라 [시스템 네트워크 요구 사항](storsimple-system-requirements.md), hello 서비스 버스 통신용 tooopen이이 포트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="ffe8e-186">hello SSL 인증 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="ffe8e-187">hello 장치 toohello 저장소 계정에 연결할 수 있습니다: _myss8000storageacct_합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="ffe8e-188">hello 연결 tooUpdate 서버 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="ffe8e-189">이 장치에는 hello 웹 프록시 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="ffe8e-190">DATA0 및 DATA1을 사용하는 경우 네트워크 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ffe8e-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="ffe8e-191">성능 테스트</span><span class="sxs-lookup"><span data-stu-id="ffe8e-191">Performance test</span></span>

<span data-ttu-id="ffe8e-192">이 테스트를 통해 장치에 대 한 hello 클라우드 읽기 / 쓰기 대기 시간이 hello 클라우드 성능을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="ffe8e-193">이 도구에 사용 되는 tooestablish StorSimple에서 얻을 수 있는 hello 클라우드 성능 기준을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="ffe8e-194">hello 도구 보고서 hello 최대 성능을 (읽기 / 쓰기 대기 시간에 대 한 모범 사례 시나리오) 연결을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="ffe8e-195">Hello 도구 hello 최대 달성 가능한 성능을 보고, 여기서 사용 하 여 hello를 배포할 때 대상 hello 작업으로 읽기 / 쓰기 대기 시간을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="ffe8e-196">hello 테스트 hello 장치에서 hello 다른 볼륨 유형과 관련 된 hello blob 크기를 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="ffe8e-197">일반 계층화되고 로컬로 고정된 일반 볼륨의 백업은 64KB Blob 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="ffe8e-198">선택된 보관 옵션을 사용하는 계층화된 볼륨은 512KB Blob 데이터 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="ffe8e-199">장치에는 계층화 된 볼륨과 로컬 고정 볼륨 구성 된 유일한 hello 테스트 해당 too64 KB blob 데이터 크기 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="ffe8e-200">이 도구 toouse를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="ffe8e-201">첫째, 계층화된 볼륨과 선택된 보관 옵션을 사용하는 계층화된 볼륨의 조합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="ffe8e-202">이 작업을 실행 하면 해당 hello 도구 테스트를 실행 hello 64 KB와 512KB에 대 한 blob 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="ffe8e-203">만들고 hello 볼륨 구성 후 hello cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="ffe8e-204">형식:</span><span class="sxs-lookup"><span data-stu-id="ffe8e-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="ffe8e-205">Hello 도구에서 보고 하는 hello 읽기 / 쓰기 대기 시간을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="ffe8e-206">이 테스트는 hello 결과 보고 하기 전에 몇 분 toorun을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="ffe8e-207">Hello 연결 대기 시간이 너무 hello에서 모든 범위를 예상 경우 hello hello 도구에서 보고 하는 대기 시간으로 사용할 수 달성 가능한 최대 대상 hello 작업 부하를 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="ffe8e-208">내부 데이터 처리를 위해 약간의 오버헤드를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="ffe8e-209">보고 된 hello 읽기 / 쓰기 대기 시간이 hello 진단 도구가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="ffe8e-210">Blob 서비스에 대 한 Storage Analytics를 구성 하 고 hello Azure 저장소 계정에 대 한 hello 출력 toounderstand hello 대기를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="ffe8e-211">자세한 지침은 이동 너무[설정 및 구성 저장소 분석](../storage/common/storage-enable-and-view-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="ffe8e-212">이러한 대기는 또한 최고 / 비교 가능한 toohello 숫자 hello StorSimple 진단 도구에서에서 받은, Azure 저장소 인 서비스 요청은 toolog을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="ffe8e-213">Hello 저장소 계정 대기 시간이 부족 한 경우, 대기 시간을 네트워크에서 발급 하 여 네트워크 관리자 tooinvestigate에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="ffe8e-214">8100 장치에서 실행되는 성능 테스트의 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="ffe8e-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="ffe8e-215">부록: 시스템 정보 해석</span><span class="sxs-lookup"><span data-stu-id="ffe8e-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="ffe8e-216">다음은 어떤 hello에 매핑할 hello 시스템 정보에는 다양 한 Windows PowerShell 매개 변수를 설명 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="ffe8e-217">PowerShell 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ffe8e-217">PowerShell Parameter</span></span>    | <span data-ttu-id="ffe8e-218">설명</span><span class="sxs-lookup"><span data-stu-id="ffe8e-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="ffe8e-219">인스턴스 ID</span><span class="sxs-lookup"><span data-stu-id="ffe8e-219">Instance ID</span></span>             | <span data-ttu-id="ffe8e-220">모든 컨트롤러에는 고유 식별자 또는 연결된 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="ffe8e-221">이름</span><span class="sxs-lookup"><span data-stu-id="ffe8e-221">Name</span></span>                    | <span data-ttu-id="ffe8e-222">hello hello Azure 포털을 통해 장치를 배포 하는 동안 구성 된 대로 hello 장치의 식별 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="ffe8e-223">hello 기본 이름은 hello 장치 일련 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="ffe8e-224">모델</span><span class="sxs-lookup"><span data-stu-id="ffe8e-224">Model</span></span>                   | <span data-ttu-id="ffe8e-225">StorSimple 8000 시리즈 장치의 hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="ffe8e-226">hello 모델 8100 또는 8600 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="ffe8e-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="ffe8e-227">SerialNumber</span></span>            | <span data-ttu-id="ffe8e-228">hello 장치 일련 번호 hello 공장에서 할당 되 고 길이가 15 자.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="ffe8e-229">예를 들어, 8600-SHX0991003G44HT는 다음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="ffe8e-230">8600-hello 장치 모델이입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="ffe8e-231">SHX –는 hello 제조 사이트.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="ffe8e-232">0991003 - 특정 제품을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="ffe8e-233">G44HT hello 마지막 5 자리는 toocreate 고유한 일련 번호를 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="ffe8e-234">순차적인 집합이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="ffe8e-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="ffe8e-235">TimeZone</span></span>                | <span data-ttu-id="ffe8e-236">hello 장치 표준 시간대에에서 구성 된 대로 hello Azure 포털 장치 배포 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="ffe8e-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="ffe8e-237">CurrentController</span></span>       | <span data-ttu-id="ffe8e-238">연결 된 toothrough StorSimple 장치의 Windows PowerShell 인터페이스를 hello는 hello 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="ffe8e-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="ffe8e-239">ActiveController</span></span>        | <span data-ttu-id="ffe8e-240">장치에서 활성화 되어 있고 모든 hello 네트워크 및 디스크 작업을 제어 하는 hello 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="ffe8e-241">이는 컨트롤러 0 또는 컨트롤러 1일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="ffe8e-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="ffe8e-242">Controller0Status</span></span>       | <span data-ttu-id="ffe8e-243">장치에서 컨트롤러 0의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="ffe8e-244">복구 모드에서 기본 또는 연결할 수 없습니다. hello 컨트롤러 상태 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="ffe8e-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="ffe8e-245">Controller1Status</span></span>       | <span data-ttu-id="ffe8e-246">컨트롤러 1의 장치에서 상태를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="ffe8e-247">복구 모드에서 기본 또는 연결할 수 없습니다. hello 컨트롤러 상태 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="ffe8e-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="ffe8e-248">SystemMode</span></span>              | <span data-ttu-id="ffe8e-249">StorSimple 장치의 전반적인 상태를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="ffe8e-250">hello 장치 상태는 보통, 수, 유지 관리 또는 폐기 된 (toodeactivated hello Azure 포털에서에서 해당).</span><span class="sxs-lookup"><span data-stu-id="ffe8e-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="ffe8e-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="ffe8e-252">toohello 장치 소프트웨어 버전에 해당 하는 친숙 한 문자열 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="ffe8e-253">업데이트 4를 실행 하는 시스템에 대 한 hello 친숙 한 소프트웨어 버전은 StorSimple 8000 시리즈 업데이트 4.0 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="ffe8e-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="ffe8e-255">장치에서 실행 중인 hello HCS 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="ffe8e-256">예를 들어, HCS 소프트웨어 버전 해당 tooStorSimple 8000 hello 시리즈 업데이트 4.0은 6.3.9600.17820 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="ffe8e-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-257">ApiVersion</span></span>              | <span data-ttu-id="ffe8e-258">hello hello HCS 장치의 Windows PowerShell API의 hello 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="ffe8e-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-259">VhdVersion</span></span>              | <span data-ttu-id="ffe8e-260">장치 hello hello 출하 시 이미지의 hello 소프트웨어 버전과 함께 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="ffe8e-261">장치 toofactory 기본값을 다시 설정 하면이 소프트웨어 버전을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="ffe8e-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-262">OSVersion</span></span>               | <span data-ttu-id="ffe8e-263">hello hello hello 장치에서 실행 되는 Windows Server 운영 체제의 소프트웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="ffe8e-264">hello StorSimple 장치 hello too6.3.9600 해당 하는 Windows Server 2012 r 2를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="ffe8e-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-265">CisAgentVersion</span></span>         | <span data-ttu-id="ffe8e-266">StorSimple 장치에서 실행 하 여 Ci 에이전트에 대 한 hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="ffe8e-267">이 에이전트는 Azure에서 실행 되는 hello StorSimple Manager 서비스와 통신 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="ffe8e-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="ffe8e-268">MdsAgentVersion</span></span>         | <span data-ttu-id="ffe8e-269">hello 버전 해당 toohello Mds 에이전트 StorSimple 장치에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="ffe8e-270">이 에이전트는 데이터 toohello 이동 모니터링 및 진단 서비스 (MDS).</span><span class="sxs-lookup"><span data-stu-id="ffe8e-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="ffe8e-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="ffe8e-271">Lsisas2Version</span></span>          | <span data-ttu-id="ffe8e-272">StorSimple 장치에서 해당 toohello LSI 드라이버 버전 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="ffe8e-273">용량</span><span class="sxs-lookup"><span data-stu-id="ffe8e-273">Capacity</span></span>                | <span data-ttu-id="ffe8e-274">hello hello 장치 바이트에서의 총 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="ffe8e-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="ffe8e-275">RemoteManagementMode</span></span>    | <span data-ttu-id="ffe8e-276">Windows PowerShell 인터페이스를 통해 hello 장치는 원격으로 관리 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="ffe8e-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="ffe8e-277">FipsMode</span></span>                | <span data-ttu-id="ffe8e-278">장치에서 hello 미국 연방 정보 FIPS (Processing Standard) 모드를 사용 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="ffe8e-279">hello FIPS 140 표준은 hello 중요 한 데이터 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인 하는 암호화 알고리즘을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="ffe8e-280">업데이트 4 이상을 실행하는 장치의 경우 FIPS 모드는 기본적으로 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ffe8e-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffe8e-281">Next steps</span></span>

* <span data-ttu-id="ffe8e-282">Hello 자세한 [hello Invoke HcsDiagnostics cmdlet의 구문을](https://technet.microsoft.com/library/mt795371.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="ffe8e-283">너무 방법에 대 한 자세한[배포 문제를 해결](storsimple-troubleshoot-deployment.md) StorSimple 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffe8e-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
