---
title: "StorSimple 장치 모드 변경 | Microsoft Docs"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: dd160ede1189b0de544c8cf5db3b13228d212419
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="c647e-103">StorSimple 장치에서 장치 모드 변경</span><span class="sxs-lookup"><span data-stu-id="c647e-103">Change the device mode on your StorSimple device</span></span>

<span data-ttu-id="c647e-104">이 문서에서는 StorSimple 장치에서 작동할 수 있는 다양한 모드에 대한 간략한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="c647e-105">StorSimple 장치는 표준, 유지 관리 및 복구의 세 가지 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="c647e-106">이 문서를 읽은 후 다음에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="c647e-107">StorSimple 장치 모드 정의</span><span class="sxs-lookup"><span data-stu-id="c647e-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="c647e-108">StorSimple 장치의 현재 모드를 파악하는 방법</span><span class="sxs-lookup"><span data-stu-id="c647e-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="c647e-109">표준에서 유지 관리 모드로, 그리고 *그 반대로*</span><span class="sxs-lookup"><span data-stu-id="c647e-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="c647e-110">위의 관리 작업은 StorSimple 장치의 Windows PowerShell 인터페이스를 통해만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="c647e-111">StorSimple 장치 모드</span><span class="sxs-lookup"><span data-stu-id="c647e-111">About StorSimple device modes</span></span>

<span data-ttu-id="c647e-112">StorSimple 장치는 표준, 유지 관리 또는 복구 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="c647e-113">각 모드는 아래에 간단하게 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="c647e-114">표준 모드</span><span class="sxs-lookup"><span data-stu-id="c647e-114">Normal mode</span></span>

<span data-ttu-id="c647e-115">완전히 구성된 StorSimple 장치에 대한 표준 작동 모드로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="c647e-116">기본적으로 장치는 표준 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="c647e-117">유지 관리 모드</span><span class="sxs-lookup"><span data-stu-id="c647e-117">Maintenance mode</span></span>

<span data-ttu-id="c647e-118">때로는 StorSimple 장치가 유지 관리 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="c647e-119">이 모드를 사용하면 장치에서 유지 관리를 수행하고 디스크 펌웨어 관련 업데이트와 같은 중단 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="c647e-120">StorSimple용 Windows PowerShell을 통해서만 시스템을 유지 관리 모드로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="c647e-121">모든 I/O 요청은 이 모드에서 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="c647e-122">비휘발성 임의 액세스 메모리 (NVRAM) 등의 서비스 또는 클러스터링 서비스도 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="c647e-123">이 모드로 들어가거나 종료하면 두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="c647e-124">유지 관리 모드를 종료하면 모든 서비스가 다시 시작되고 정상 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="c647e-125">몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="c647e-126">**유지 관리 모드는 정상적으로 작동하는 장치에만 지원됩니다. 하나 또는 모든 컨트롤러가 작동하지 않는 장치에서 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="c647e-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="c647e-127">복구 모드</span><span class="sxs-lookup"><span data-stu-id="c647e-127">Recovery mode</span></span>

<span data-ttu-id="c647e-128">복구 모드는 "네트워크를 지원하는 Windows 안전 모드"로 설명될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="c647e-129">복구 모드는 Microsoft 기술 지원 서비스 팀을 통해 시스템에서 진단을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="c647e-130">복구 모드의 기본 목표는 시스템 로그를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="c647e-131">시스템이 복구 모드로 전환되는 경우 Microsoft 지원에 다음 단계를 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="c647e-132">자세한 내용은 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="c647e-132">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c647e-133">**장치를 복구 모드로 유지할 수 없습니다. 장치가 잘못된 상태에 있으면 복구 모드는 Microsoft 고객 지원 담당자가 검사할 수 있는 상태로 장치를 전환하려고 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c647e-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="c647e-134">StorSimple 장치 모드 확인</span><span class="sxs-lookup"><span data-stu-id="c647e-134">Determine StorSimple device mode</span></span>

#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="c647e-135">현재 장치 모드를 확인하려면</span><span class="sxs-lookup"><span data-stu-id="c647e-135">To determine the current device mode</span></span>

1. <span data-ttu-id="c647e-136">[장치 직렬 콘솔 연결에 PuTTY 사용](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)단계를 수행하여 장치 직렬 콘솔에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="c647e-137">장치의 직렬 콘솔 메뉴에 있는 배너 메시지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="c647e-138">이 메시지는 장치가 유지 관리 또는 복구 모드에 있는지를 명시적으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="c647e-139">메시지에 시스템 모드에 대한 특정 정보가 없는 경우 장치가 표준 모드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="c647e-140">StorSimple 장치 모드 변경</span><span class="sxs-lookup"><span data-stu-id="c647e-140">Change the StorSimple device mode</span></span>

<span data-ttu-id="c647e-141">StorSimple 장치를 유지 관리 모드(표준 모드에서)에 배치하여 유지 관리를 수행하거나 유지 관리 모드 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="c647e-142">유지 관리 모드로 들어가거나 종료하려면 다음 절차를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="c647e-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c647e-143">유지 관리 모드에 들어가기 전에 Azure Portal에서 장치에 대한 **장치 설정 > 하드웨어 상태**에 액세스하여 두 장치 컨트롤러 모두가 정상 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Device settings > Hardware health** for your device in the Azure portal.</span></span> <span data-ttu-id="c647e-144">하나 또는 모든 컨트롤러가 정상 상태가 아니면 다음 단계는 Microsoft 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c647e-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="c647e-145">자세한 내용은 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="c647e-145">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="c647e-146">유지 관리 모드로 전환하려면</span><span class="sxs-lookup"><span data-stu-id="c647e-146">To enter maintenance mode</span></span>

1. <span data-ttu-id="c647e-147">[장치 직렬 콘솔 연결에 PuTTY 사용](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)단계를 수행하여 장치 직렬 콘솔에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="c647e-148">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="c647e-149">메시지가 표시되면 **장치 관리자 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="c647e-150">기본 암호는 `Password1`입니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="c647e-151">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="c647e-152">유지 관리 모드에서는 모든 I/O 요청이 중단되며 Azure Portal에 대한 연결이 끊어짐을 알리는 경고 메시지와 확인 요청 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="c647e-153">**Y** 를 입력하여 유지 관리 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="c647e-154">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-154">Both controllers will restart.</span></span> <span data-ttu-id="c647e-155">다시 시작이 완료되면 장치가 유지 관리 모드임을 나타내는 직렬 콘솔 배너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-155">When the restart is complete, the serial console banner will indicate that the device is in maintenance mode.</span></span> <span data-ttu-id="c647e-156">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="c647e-157">유지 관리 모드를 종료하려면</span><span class="sxs-lookup"><span data-stu-id="c647e-157">To exit maintenance mode</span></span>

1. <span data-ttu-id="c647e-158">장치 직렬 콘솔에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-158">Log on to the device serial console.</span></span> <span data-ttu-id="c647e-159">배너 메시지에서 장치가 유지 관리 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-159">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="c647e-160">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-160">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="c647e-161">경고 메시지와 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="c647e-162">**Y** 를 입력하여 유지 관리 모드를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-162">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="c647e-163">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-163">Both controllers will restart.</span></span> <span data-ttu-id="c647e-164">다시 시작이 완료되면 장치가 정상 모드임을 나타내는 직렬 콘솔 배너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-164">When the restart is complete, the serial console banner indicates that the device is in normal mode.</span></span> <span data-ttu-id="c647e-165">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure to install on each controller could result in data corruption. Exiting maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to exit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="c647e-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c647e-166">Next steps</span></span>

<span data-ttu-id="c647e-167">StorSimple 장치에서 [표준 및 유지 관리 모드 업데이트를 적용](storsimple-update-device.md) 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c647e-167">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

