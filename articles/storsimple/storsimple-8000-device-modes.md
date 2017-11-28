---
title: "StorSimple 장치 모드 aaaChange | Microsoft Docs"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="2c614-103">StorSimple 장치에 사용 되는 hello 장치 모드 변경</span><span class="sxs-lookup"><span data-stu-id="2c614-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="2c614-104">이 문서에서는 hello에 대 한 간략 한 설명을 StorSimple 장치 작동할 수 있는 다양 한 모드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="2c614-105">StorSimple 장치는 표준, 유지 관리 및 복구의 세 가지 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="2c614-106">이 문서를 읽은 후 다음에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="2c614-107">Hello StorSimple 장치 모드 이란</span><span class="sxs-lookup"><span data-stu-id="2c614-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="2c614-108">에 어떻게 모드 아웃 toofigure hello StorSimple 장치</span><span class="sxs-lookup"><span data-stu-id="2c614-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="2c614-109">어떻게 일반 toomaintenance 모드에서 toochange 및 *반대의*</span><span class="sxs-lookup"><span data-stu-id="2c614-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="2c614-110">관리 작업 위에 hello StorSimple 장치의 Windows PowerShell 인터페이스 hello 통해 수행할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="2c614-111">StorSimple 장치 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-111">About StorSimple device modes</span></span>

<span data-ttu-id="2c614-112">StorSimple 장치는 표준, 유지 관리 또는 복구 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="2c614-113">각 모드는 아래에 간단하게 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="2c614-114">표준 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-114">Normal mode</span></span>

<span data-ttu-id="2c614-115">완전히 구성 된 StorSimple 장치에 대 한 hello 표준 작동 모드로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="2c614-116">기본적으로 장치는 표준 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="2c614-117">유지 관리 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-117">Maintenance mode</span></span>

<span data-ttu-id="2c614-118">경우에 따라 hello StorSimple 장치 해야 toobe 유지 관리 모드로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="2c614-119">이 모드 hello 장치에서 tooperform 유지 관리를 허용 하 고 관련 toodisk 펌웨어 같은 중단 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="2c614-120">StorSimple 용 Windows PowerShell hello 통해서만 유지 관리 모드로 hello 시스템을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="2c614-121">모든 I/O 요청은 이 모드에서 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="2c614-122">비휘발성 메모리 (NVRAM) 또는 서비스를 클러스터링 하는 hello와 같은 서비스 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="2c614-123">이 모드를 종료 하거나 입력 하면 두 hello 컨트롤러 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="2c614-124">Hello 유지 관리 모드를 종료 하면 모든 hello 서비스 다시 시작 됩니다 하 고 정상 상태 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="2c614-125">몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="2c614-126">**유지 관리 모드는 정상적으로 작동하는 장치에만 지원됩니다. hello 컨트롤러 중 하나 이상이 작동 하지 않는 장치에서 지원 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="2c614-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="2c614-127">복구 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-127">Recovery mode</span></span>

<span data-ttu-id="2c614-128">복구 모드는 "네트워크를 지원하는 Windows 안전 모드"로 설명될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="2c614-129">복구 모드 hello Microsoft 지원 팀 있으며 hello 시스템에 tooperform 진단 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="2c614-130">복구 모드의 기본 목표는 hello tooretrieve hello 시스템 로그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="2c614-131">시스템이 복구 모드로 전환되는 경우 Microsoft 지원에 다음 단계를 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="2c614-132">자세한 내용은 이동 너무[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2c614-133">**복구 모드에서 hello 장치를 추가할 수 없습니다. Hello 장치가 비정상적인 상태 이면 복구 모드는 Microsoft 기술 지원 담당자가 검사할 수 상태로 tooget hello 장치를 시도 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2c614-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="2c614-134">StorSimple 장치 모드 확인</span><span class="sxs-lookup"><span data-stu-id="2c614-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="2c614-135">toodetermine hello 현재 장치 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="2c614-136">Hello 단계를 수행 하 여 toohello 장치 직렬 콘솔에 로그온 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="2c614-137">Hello 장치의 hello 직렬 콘솔 메뉴에서 hello 배너 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="2c614-138">이 메시지는 명시적으로 hello 장치 유지 관리 나 복구 모드 인지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="2c614-139">Hello 메시지 toohello 시스템 모드와 관련 된 특정 정보 없으면 hello 장치가 표준 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="2c614-140">Hello StorSimple 장치 모드 변경</span><span class="sxs-lookup"><span data-stu-id="2c614-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="2c614-141">유지 관리 모드 업데이트를 설치 하거나 hello StorSimple 장치가 유지 관리 모드 (기본 모드)에서 tooperform 유지 관리에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="2c614-142">Hello 프로시저 tooenter 또는 끝내기 유지 관리 모드를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c614-143">유지 관리 모드를 설정 하기 전에 hello에 액세스 하 여 두 장치 컨트롤러가 모두의 상태가 정상 인지 확인 **장치 설정 > 하드웨어 상태가** hello Azure 포털에서에서 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="2c614-144">하나 또는 두 개의 hello 컨트롤러 요소가 비정상적인 경우 hello 다음 단계에 대 한 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="2c614-145">자세한 내용은 이동 너무[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="2c614-146">tooenter 유지 관리 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="2c614-147">Hello 단계를 수행 하 여 toohello 장치 직렬 콘솔에 로그온 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="2c614-148">Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="2c614-149">메시지가 표시 되 면 제공 hello **장치 관리자 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="2c614-150">hello 기본 암호는: `Password1`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="2c614-151">Hello 명령 프롬프트에 입력</span><span class="sxs-lookup"><span data-stu-id="2c614-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="2c614-152">유지 관리 모드를 사용 하는 알려 주는 경고 메시지가 모든 I/O 요청이 중단 되며 서버 hello 연결 toohello Azure 포털 및 확인을 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="2c614-153">형식 **Y** tooenter 유지 관리 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="2c614-154">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-154">Both controllers will restart.</span></span> <span data-ttu-id="2c614-155">Hello를 다시 시작이 완료 되 면 hello 직렬 콘솔 배너 hello 장치가 유지 관리 모드에서 해당 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="2c614-156">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="2c614-157">tooexit 유지 관리 모드</span><span class="sxs-lookup"><span data-stu-id="2c614-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="2c614-158">Toohello 장치 직렬 콘솔에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-158">Log on toohello device serial console.</span></span> <span data-ttu-id="2c614-159">장치가 유지 관리 모드에 있는 hello 배너 메시지에서 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2c614-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="2c614-160">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="2c614-161">경고 메시지와 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="2c614-162">형식 **Y** tooexit 유지 관리 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="2c614-163">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-163">Both controllers will restart.</span></span> <span data-ttu-id="2c614-164">Hello를 다시 시작이 완료 되 면 hello 직렬 콘솔 배너 해당 hello 장치가 표준 모드일에서 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="2c614-165">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="2c614-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c614-166">Next steps</span></span>

<span data-ttu-id="2c614-167">너무 방법에 대해 알아봅니다[normal 및 유지 관리 모드 업데이트를 적용](storsimple-update-device.md) StorSimple 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c614-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

