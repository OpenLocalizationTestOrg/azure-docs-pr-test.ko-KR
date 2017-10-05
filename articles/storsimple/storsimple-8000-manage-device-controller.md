---
title: "StorSimple 8000 시리즈 장치 컨트롤러 관리 | Microsoft Docs"
description: "StorSimple 장치 컨트롤러를 중지, 다시 시작, 종료 또는 다시 설정하는 방법을 알아봅니다."
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
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 75c1bdb570967b6d1902697597f0b5bf3f4ffb7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-storsimple-device-controllers"></a><span data-ttu-id="4d560-103">StorSimple 장치 컨트롤러 관리</span><span class="sxs-lookup"><span data-stu-id="4d560-103">Manage your StorSimple device controllers</span></span>

## <a name="overview"></a><span data-ttu-id="4d560-104">개요</span><span class="sxs-lookup"><span data-stu-id="4d560-104">Overview</span></span>

<span data-ttu-id="4d560-105">이 자습서에서는 StorSimple 장치 컨트롤러에서 수행할 수 있는 다양한 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-105">This tutorial describes the different operations that can be performed on your StorSimple device controllers.</span></span> <span data-ttu-id="4d560-106">StorSimple 장치의 컨트롤러는 능동-수동 구성에서 중복(피어) 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-106">The controllers in your StorSimple device are redundant (peer) controllers in an active-passive configuration.</span></span> <span data-ttu-id="4d560-107">지정된 시간에 컨트롤러는 하나만 활성화되어 모든 디스크 및 네트워크 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-107">At a given time, only one controller is active and is processing all the disk and network operations.</span></span> <span data-ttu-id="4d560-108">다른 컨트롤러는 수동 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-108">The other controller is in a passive mode.</span></span> <span data-ttu-id="4d560-109">활성 컨트롤러에 실패하면 수동 컨트롤러가 자동으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-109">If the active controller fails, the passive controller automatically becomes active.</span></span>

<span data-ttu-id="4d560-110">이 자습서는 다음을 사용하여 장치 컨트롤러를 관리하도록 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-110">This tutorial includes step-by-step instructions to manage the device controllers by using the:</span></span>

* <span data-ttu-id="4d560-111">StorSimple 장치 관리자 서비스에서 장치의 **컨트롤러** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-111">**Controllers** blade for your device in the  StorSimple Device Manager service.</span></span>
* <span data-ttu-id="4d560-112">StorSimple용 Windows PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-112">Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="4d560-113">사용자가 StorSimple 장치 관리자 서비스를 통해 장치 컨트롤러를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-113">We recommend that you manage the device controllers via the  StorSimple Device Manager service.</span></span> <span data-ttu-id="4d560-114">StorSimple용 Windows PowerShell을 사용해야 동작을 수행할 수 있는 경우에는 자습서에 관련 메모가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-114">If an action can only be performed by using Windows PowerShell for StorSimple, the tutorial makes a note of it.</span></span>

<span data-ttu-id="4d560-115">이 자습서를 읽은 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-115">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="4d560-116">StorSimple 장치 컨트롤러를 다시 시작 또는 종료</span><span class="sxs-lookup"><span data-stu-id="4d560-116">Restart or shut down a StorSimple device controller</span></span>
* <span data-ttu-id="4d560-117">StorSimple 장치 종료</span><span class="sxs-lookup"><span data-stu-id="4d560-117">Shut down a StorSimple device</span></span>
* <span data-ttu-id="4d560-118">StorSimple 장치를 공장 기본값으로 재설정</span><span class="sxs-lookup"><span data-stu-id="4d560-118">Reset your StorSimple device to factory defaults</span></span>

## <a name="restart-or-shut-down-a-single-controller"></a><span data-ttu-id="4d560-119">단일 컨트롤러 다시 시작 또는 종료</span><span class="sxs-lookup"><span data-stu-id="4d560-119">Restart or shut down a single controller</span></span>
<span data-ttu-id="4d560-120">컨트롤러 다시 시작 또는 종료는 정상적인 시스템 작업의 일환으로 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-120">A controller restart or shutdown is not required as a part of normal system operation.</span></span> <span data-ttu-id="4d560-121">단일 장치 컨트롤러에 대한 종료 작업은 실패한 장치 하드웨어 구성 요소가 교체를 필요로 하는 경우에 흔하게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-121">Shutdown operations for a single device controller are common only in cases in which a failed device hardware component requires replacement.</span></span> <span data-ttu-id="4d560-122">과도한 메모리 사용 또는 작동하지 않는 컨트롤러 때문에 성능이 영향을 받는 경우에도 컨트롤러를 다시 시작할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-122">A controller restart may also be required in a situation in which performance is affected by excessive memory usage or a malfunctioning controller.</span></span> <span data-ttu-id="4d560-123">또한 대체 컨트롤러를 사용하도록 설정하고 테스트하려면 컨트롤러를 성공적으로 교체한 후에 컨트롤러를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-123">You may also need to restart a controller after a successful controller replacement, if you wish to enable and test the replaced controller.</span></span>

<span data-ttu-id="4d560-124">수동 컨트롤러를 사용할 수 있다면 장치를 다시 시작해도 연결된 개시 장치를 중단하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-124">Restarting a device is not disruptive to connected initiators, assuming the passive controller is available.</span></span> <span data-ttu-id="4d560-125">수동 컨트롤러를 사용할 수 없거나 꺼져있는 경우 활성 컨트롤러를 다시 시작하면 서비스 및 가동 중지 시간이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-125">If a passive controller is not available or turned off, then restarting the active controller may result in the disruption of service and downtime.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="4d560-126">**이렇게 하면 중복 손실과 가동 중지 시간 위험 가능성이 높아져서 실행 중인 컨트롤러를 물리적으로 제거하지 말아야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4d560-126">**A running controller should never be physically removed as this would result in a loss of redundancy and an increased risk of downtime.**</span></span>
> * <span data-ttu-id="4d560-127">다음 절차는 물리적 StorSimple 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-127">The following procedure applies only to the StorSimple physical device.</span></span> <span data-ttu-id="4d560-128">StorSimple Cloud Appliance를 시작, 중지 및 다시 시작하는 방법에 대한 자세한 내용은 [클라우드 어플라이언스로 작업](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d560-128">For information about how to start, stop, and restart the StorSimple Cloud Appliance, see [Work with the cloud appliance](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).</span></span>

<span data-ttu-id="4d560-129">StorSimple용 Windows PowerShell 또는 StorSimple 장치 관리자 서비스의 Azure Portal을 통해 단일 장치 컨트롤러를 다시 시작하거나 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-129">You can restart or shut down a single device controller via the Azure portal of the  StorSimple Device Manager service or Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="4d560-130">Azure Portal에서 장치 컨트롤러를 관리하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-130">To manage your device controllers from the Azure portal, perform the following steps.</span></span>

#### <a name="to-restart-or-shut-down-a-controller-in-azure-portal"></a><span data-ttu-id="4d560-131">Azure Portal에서 컨트롤러를 다시 시작하거나 종료하려면</span><span class="sxs-lookup"><span data-stu-id="4d560-131">To restart or shut down a controller in Azure portal</span></span>
1. <span data-ttu-id="4d560-132">StorSimple 장치 관리자 서비스에서 **장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-132">In your StorSimple Device Manager service, go to **Devices**.</span></span> <span data-ttu-id="4d560-133">장치 목록에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-133">Select your device from the list of devices.</span></span> 

    ![장치 선택](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. <span data-ttu-id="4d560-135">**설정 > 컨트롤러**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-135">Go to **Settings > Controllers**.</span></span>
   
    ![StorSimple 장치 컨트롤러가 정상임을 확인](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. <span data-ttu-id="4d560-137">**컨트롤러** 블레이드에서 장치에 대한 컨트롤러의 상태가 **정상**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-137">In the **Controllers** blade, verify that the status of both the controllers on your device is **Healthy**.</span></span> <span data-ttu-id="4d560-138">컨트롤러를 선택하고 마우스 오른쪽 단추로 클릭한 다음 **다시 시작** 또는 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-138">Select a controller, right-click and then select **Restart** or **Shut down**.</span></span>

    ![StorSimple 장치 컨트롤러를 다시 시작 또는 종료 선택](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. <span data-ttu-id="4d560-140">컨트롤러를 다시 시작하거나 종료하기 위해 작업을 만들고 적용 가능한 경고가 있는 경우 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-140">A job is created to restart or shut down the controller and you are presented with applicable warnings, if any.</span></span> <span data-ttu-id="4d560-141">다시 시작 또는 종료를 모니터링하려면 **서비스 > 활동 로그**로 이동한 다음 서비스에 지정된 매개 변수에서 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-141">To monitor the restart or shutdown, go to **Service > Activity logs** and then filter by parameters specific to your service.</span></span> <span data-ttu-id="4d560-142">컨트롤러를 종료하는 경우 전원 단추를 눌러서 설정하려는 컨트롤러를 켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-142">If a controller was shut down, then you will need to push the power button to turn on the controller to turn it on.</span></span>

#### <a name="to-restart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a><span data-ttu-id="4d560-143">StorSimple용 Windows PowerShell에서 컨트롤러를 다시 시작하거나 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-143">To restart or shut down a controller in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="4d560-144">다음 단계를 수행하여 StorSimple용 Windows PowerShell에서 StorSimple 장치에 단일 컨트롤러를 종료하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-144">Perform the following steps to shut down or restart a single controller on your StorSimple device from the Windows PowerShell for StorSimple.</span></span>

1. <span data-ttu-id="4d560-145">직렬 콘솔 또는 원격 컴퓨터에서 텔넷 세션을 통해 장치에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-145">Access the device via the serial console or a telnet session from a remote computer.</span></span> <span data-ttu-id="4d560-146">컨트롤러 0 또는 컨트롤러 1에 연결하려면 [장치 직렬 콘솔 연결에 PuTTY 사용](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-146">To connect to Controller 0 or Controller 1, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="4d560-147">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-147">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="4d560-148">배너 메시지에서 연결된 컨트롤러(컨트롤러 0 또는 컨트롤러 1)와 활성 또는 수동(대기) 컨트롤러 여부를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-148">In the banner message, make a note of the controller you are connected to (Controller 0 or Controller 1) and whether it is the active or the passive (standby) controller.</span></span>
   
   * <span data-ttu-id="4d560-149">프롬프트에서 단일 컨트롤러를 종료하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-149">To shut down a single controller, at the prompt, type:</span></span>
     
       `Stop-HcsController`
     
       <span data-ttu-id="4d560-150">연결된 컨트롤러를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-150">This shuts down the controller that you are connected to.</span></span> <span data-ttu-id="4d560-151">활성 컨트롤러를 중지하면 장치를 수동 컨트롤러에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-151">If you stop the active controller, then the device fails over to the passive controller.</span></span>

   * <span data-ttu-id="4d560-152">컨트롤러를 다시 시작하려면 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-152">To restart a controller, at the prompt, type:</span></span>
     
       `Restart-HcsController`
     
       <span data-ttu-id="4d560-153">연결된 컨트롤러를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-153">This restarts the controller that you are connected to.</span></span> <span data-ttu-id="4d560-154">활성 컨트롤러를 다시 시작하면 수동 컨트롤러를 다시 시작하기 전에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-154">If you restart the active controller, it fails over to the passive controller before the restart.</span></span>

## <a name="shut-down-a-storsimple-device"></a><span data-ttu-id="4d560-155">StorSimple 장치 종료</span><span class="sxs-lookup"><span data-stu-id="4d560-155">Shut down a StorSimple device</span></span>

<span data-ttu-id="4d560-156">이 섹션에서는 원격 컴퓨터에서 실행 중이거나 실패한 StorSimple 장치를 종료하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-156">This section explains how to shut down a running or a failed StorSimple device from a remote computer.</span></span> <span data-ttu-id="4d560-157">장치 컨트롤러를 모두 종료한 후에 장치는 꺼집니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-157">A device is turned off after both the device controllers are shut down.</span></span> <span data-ttu-id="4d560-158">장치를 물리적으로 이동하는 경우 장치가 종료되거나 서비스에서 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-158">A device shutdown is done when the device is physically moved, or is taken out of service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d560-159">장치를 종료하기 전에 장치 구성 요소의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-159">Before you shut down the device, check the health of the device components.</span></span> <span data-ttu-id="4d560-160">사용자의 장치로 이동한 다음 **설정 > 하드웨어 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-160">Navigate to your device and then click **Settings > Hardware health**.</span></span> <span data-ttu-id="4d560-161">**상태 및 하드웨어 상태** 블레이드에서 모든 구성 요소의 LED 상태가 녹색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-161">In the **Status and hardware health** blade, verify that the LED status of all the components is green.</span></span> <span data-ttu-id="4d560-162">정상 장치만이 녹색 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-162">Only a healthy device has a green status.</span></span> <span data-ttu-id="4d560-163">장치가 종료되어 작동하지 않는 구성 요소를 교체하는 경우 해당 구성 요소에 실패(빨간색) 또는 성능 저하(노란색) 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-163">If your device is being shut down to replace a malfunctioning component, you will see a failed (red) or a degraded (yellow) status for the respective component(s).</span></span>


#### <a name="to-shut-down-a-storsimple-device"></a><span data-ttu-id="4d560-164">StorSimple 장치 종료하려면</span><span class="sxs-lookup"><span data-stu-id="4d560-164">To shut down a StorSimple device</span></span>

1. <span data-ttu-id="4d560-165">[컨트롤러 다시 시작 또는 종료](#restart-or-shut-down-a-single-controller) 프로시저를 사용하여 장치에서 수동 컨트롤러를 식별하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-165">Use the [restart or shut down a controller](#restart-or-shut-down-a-single-controller) procedure to identify and shut down the passive controller on your device.</span></span> <span data-ttu-id="4d560-166">Azure Portal 또는 StorSimple용 Windows PowerShell에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-166">You can perform this operation in the Azure portal or in Windows PowerShell for StorSimple.</span></span>
2. <span data-ttu-id="4d560-167">활성 컨트롤러를 종료하려면 위의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-167">Repeat the above step to shut down the active controller.</span></span>
3. <span data-ttu-id="4d560-168">이제 장치의 뒤쪽 평면을 살펴봐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-168">You must now look at the back plane of the device.</span></span> <span data-ttu-id="4d560-169">두 컨트롤러를 완전히 종료한 후에 두 컨트롤러에서 상태 LED가 빨간색으로 깜박여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-169">After the two controllers are completely shut down, the status LEDs on both the controllers should be blinking red.</span></span> <span data-ttu-id="4d560-170">이번에 장치를 완전히 해제해야 하면 전원 및 냉각 모듈(PCM) 모두에서 전원 스위치를 끄기 위치에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-170">If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.</span></span> <span data-ttu-id="4d560-171">이 장치를 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-171">This should turn off the device.</span></span>

## <a name="reset-the-device-to-factory-default-settings"></a><span data-ttu-id="4d560-172">장치를 공장 기본 설정으로 재설정</span><span class="sxs-lookup"><span data-stu-id="4d560-172">Reset the device to factory default settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d560-173">장치를 공장 기본 설정으로 재설정해야 할 경우 Microsoft 지원 서비스에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-173">If you need to reset your device to factory default settings, contact Microsoft Support.</span></span> <span data-ttu-id="4d560-174">아래에 설명된 절차는 Microsoft 기술 지원 서비스에 따라서만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-174">The procedure described below should be used only in conjunction with Microsoft Support.</span></span>

<span data-ttu-id="4d560-175">이 절차는 StorSimple용 Windows PowerShell을 사용하여 Microsoft Azure StorSimple 장치를 공장 기본 설정으로 다시 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-175">This procedure describes how to reset your Microsoft Azure StorSimple device to factory default settings using Windows PowerShell for StorSimple.</span></span>
<span data-ttu-id="4d560-176">장치를 다시 설정하면 기본적으로 전체 클러스터에서 모든 데이터 및 설정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-176">Resetting a device removes all data and settings from the entire cluster by default.</span></span>

<span data-ttu-id="4d560-177">Microsoft Azure StorSimple 장치를 공장 기본 설정으로 다시 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-177">Perform the following steps to reset your Microsoft Azure StorSimple device to factory default settings:</span></span>

### <a name="to-reset-the-device-to-default-settings-in-windows-powershell-for-storsimple"></a><span data-ttu-id="4d560-178">StorSimple용 Windows PowerShell의 기본 설정으로 장치를 재설정하려면</span><span class="sxs-lookup"><span data-stu-id="4d560-178">To reset the device to default settings in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="4d560-179">직렬 콘솔을 통해 장치에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-179">Access the device through its serial console.</span></span> <span data-ttu-id="4d560-180">**활성** 컨트롤러에 연결하려면 배너 메시지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4d560-180">Check the banner message to ensure that you are connected to the **Active** controller.</span></span>
2. <span data-ttu-id="4d560-181">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-181">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="4d560-182">프롬프트에서 전체 클러스터를 다시 설정하는 다음 명령을 입력하면 모든 데이터, 메타데이터 및 컨트롤러 설정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-182">At the prompt, type the following command to reset the entire cluster, removing all data, metadata, and controller settings:</span></span>
   
    `Reset-HcsFactoryDefault`
   
    <span data-ttu-id="4d560-183">대신 단일 컨트롤러를 재설정하려면 `-scope` 매개 변수가 있는 [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-183">To instead reset a single controller, use the  [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet with the `-scope` parameter.)</span></span>
   
    <span data-ttu-id="4d560-184">시스템을 여러 번 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-184">The system will reboot multiple times.</span></span> <span data-ttu-id="4d560-185">재설정이 성공적으로 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-185">You will be notified when the reset has successfully completed.</span></span> <span data-ttu-id="4d560-186">시스템 모델에 따라 이 프로세스를 완료 하는 데 8100 장치로 45-60분이 걸리고 8600 장치로 60-90분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-186">Depending on the system model, it can take 45-60 minutes for an 8100 device and 60-90 minutes for an 8600 to finish this process.</span></span>
   
## <a name="questions-and-answers-about-managing-device-controllers"></a><span data-ttu-id="4d560-187">장치 컨트롤러를 관리하는 방법에 대한 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="4d560-187">Questions and answers about managing device controllers</span></span>
<span data-ttu-id="4d560-188">이 섹션에서는 StorSimple 장치 컨트롤러의 관리와 관련하여 자주 묻는 질문 중 일부를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-188">In this section, we have summarized some of the frequently asked questions regarding managing StorSimple device controllers.</span></span>

<span data-ttu-id="4d560-189">**Q.**</span><span class="sxs-lookup"><span data-stu-id="4d560-189">**Q.**</span></span> <span data-ttu-id="4d560-190">장치에서 컨트롤러가 모두 정상이고 켜져 있으며 활성 컨트롤러를 다시 시작 또는 종료하는 경우 무엇이 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="4d560-190">What happens if both the controllers on my device are healthy and turned on and I restart or shut down the active controller?</span></span>

<span data-ttu-id="4d560-191">**A.**</span><span class="sxs-lookup"><span data-stu-id="4d560-191">**A.**</span></span> <span data-ttu-id="4d560-192">장치의 컨트롤러가 모두 정상이고 켜져 있는 경우 확인을 위한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-192">If both the controllers on your device are healthy and turned on, you are prompted for confirmation.</span></span> <span data-ttu-id="4d560-193">선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-193">You may choose to:</span></span>

* <span data-ttu-id="4d560-194">**활성 컨트롤러 다시 시작** – 활성 컨트롤러를 다시 시작하면 장치가 수동 컨트롤러로 장애 조치(failover)된다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-194">**Restart the active controller** – You are notified that restarting an active controller caused the device to fail over to the passive controller.</span></span> <span data-ttu-id="4d560-195">컨트롤러가 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-195">The controller restarts.</span></span>
* <span data-ttu-id="4d560-196">**활성 컨트롤러 종료** – 활성 컨트롤러를 종료하면 가동이 중지된다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-196">**Shut down an active controller** – You are notified that shutting down an active controller results in downtime.</span></span> <span data-ttu-id="4d560-197">컨트롤러를 켜기 위해 장치에서 전원 단추를 눌러야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-197">You also need to push the power button on the device to turn on the controller.</span></span>

<span data-ttu-id="4d560-198">**Q.**</span><span class="sxs-lookup"><span data-stu-id="4d560-198">**Q.**</span></span> <span data-ttu-id="4d560-199">장치에서 수동 컨트롤러가 모두 정상이고 켜져 있으며 활성 컨트롤러를 다시 시작 또는 종료하는 경우 무엇이 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="4d560-199">What happens if the passive controller on my device is unavailable or turned off and I restart or shut down the active controller?</span></span>

<span data-ttu-id="4d560-200">**A.**</span><span class="sxs-lookup"><span data-stu-id="4d560-200">**A.**</span></span> <span data-ttu-id="4d560-201">장치에서 수동 컨트롤러를 사용할 수 없거나 해제된 경우 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-201">If the passive controller on your device is unavailable or turned off, and you choose to:</span></span>

* <span data-ttu-id="4d560-202">**활성 컨트롤러 다시 시작** – 작업을 계속하면 서비스의 임시 중단이 발생하고 확인 메시지가 표시된다는 내용의 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-202">**Restart the active controller** – You are notified that continuing the operation will result in a temporary disruption of the service, and you are prompted for confirmation.</span></span>
* <span data-ttu-id="4d560-203">**활성 컨트롤러 종료** – 작업을 계속하면 가동 중지 시간이 발생한다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-203">**Shut down an active controller** – You are notified that continuing the operation results in downtime.</span></span> <span data-ttu-id="4d560-204">하나 또는 두 컨트롤러에서 전원 단추를 눌러서 장치를 켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-204">You also need to push the power button on one or both controllers to turn on the device.</span></span> <span data-ttu-id="4d560-205">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-205">You are prompted for confirmation.</span></span>

<span data-ttu-id="4d560-206">**Q.**</span><span class="sxs-lookup"><span data-stu-id="4d560-206">**Q.**</span></span> <span data-ttu-id="4d560-207">어떤 경우에 컨트롤러를 다시 시작 또는 종료를 진행하는 데 실패합니까?</span><span class="sxs-lookup"><span data-stu-id="4d560-207">When does the controller restart or shutdown fails to progress?</span></span>

<span data-ttu-id="4d560-208">**A.**</span><span class="sxs-lookup"><span data-stu-id="4d560-208">**A.**</span></span> <span data-ttu-id="4d560-209">다음 경우 롤러를 다시 시작하거나 종료하는 데 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-209">Restarting or shutting down a controller may fail if:</span></span>

* <span data-ttu-id="4d560-210">장치 업데이트를 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-210">A device update is in progress.</span></span>
* <span data-ttu-id="4d560-211">컨트롤러 다시 시작이 이미 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-211">A controller restart is already in progress.</span></span>
* <span data-ttu-id="4d560-212">컨트롤러 종료가 이미 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-212">A controller shutdown is already in progress.</span></span>

<span data-ttu-id="4d560-213">**Q.**</span><span class="sxs-lookup"><span data-stu-id="4d560-213">**Q.**</span></span> <span data-ttu-id="4d560-214">컨트롤러를 다시 시작하거나 종료하는 경우 어떻게 확인합니까?</span><span class="sxs-lookup"><span data-stu-id="4d560-214">How can you figure out if a controller was restarted or shut down?</span></span>

<span data-ttu-id="4d560-215">**A.**</span><span class="sxs-lookup"><span data-stu-id="4d560-215">**A.**</span></span> <span data-ttu-id="4d560-216">컨트롤러 블레이드에서 컨트롤러의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-216">You can check the controller status on Controller blade.</span></span> <span data-ttu-id="4d560-217">컨트롤러 상태는 컨트롤러를 다시 시작하는 과정인지, 아니면 종료하는 과정인지를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-217">The controller status will indicate whether a controller is in the process of restarting or shutting down.</span></span> <span data-ttu-id="4d560-218">또한 컨트롤러가 다시 시작하거나 종료된 경우 **경고** 블레이드는 정보 경고를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-218">Additionally, the **Alerts** blade contain an informational alert if the controller is restarted or shut down.</span></span> <span data-ttu-id="4d560-219">컨트롤러 다시 시작 및 종료 작업은 활동 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-219">The controller restart and shutdown operations are also recorded in the acitivity logs.</span></span> <span data-ttu-id="4d560-220">활동 로그에 대한 자세한 내용을 보려면 [활동 로그 보기](storsimple-8000-service-dashboard.md#view-the-activity-logs)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-220">For more information about acitivity logs, go to [View the activity logs](storsimple-8000-service-dashboard.md#view-the-activity-logs).</span></span>

<span data-ttu-id="4d560-221">**Q.**</span><span class="sxs-lookup"><span data-stu-id="4d560-221">**Q.**</span></span> <span data-ttu-id="4d560-222">컨트롤러 장애 조치의 결과로써 I/O에 영향이 있나요?</span><span class="sxs-lookup"><span data-stu-id="4d560-222">Is there any impact to the I/O as a result of controller failover?</span></span>

<span data-ttu-id="4d560-223">**A.**</span><span class="sxs-lookup"><span data-stu-id="4d560-223">**A.**</span></span> <span data-ttu-id="4d560-224">초기자 및 활성 컨트롤러 간의 TCP 연결은 컨트롤러 장애 조치의 결과로 재설정되지만 수동 컨트롤러가 작업을 가정하는 경우 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-224">The TCP connections between initiators and active controller will be reset as a result of controller failover, but will be reestablished when the passive controller assumes operation.</span></span> <span data-ttu-id="4d560-225">이 작업의 과정에서 초기자와 장치 간의 I/O 작업에서 임시(30초 미만) 일시 정지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d560-225">There may be a temporary (less than 30 seconds) pause in I/O activity between initiators and the device during the course of this operation.</span></span>

<span data-ttu-id="4d560-226">**Q.**</span><span class="sxs-lookup"><span data-stu-id="4d560-226">**Q.**</span></span> <span data-ttu-id="4d560-227">컨트롤러를 서비스에서 종료하고 제거한 후에 서비스에 반환하는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="4d560-227">How do I return my controller to service after it has been shut down and removed?</span></span>

<span data-ttu-id="4d560-228">**A.**</span><span class="sxs-lookup"><span data-stu-id="4d560-228">**A.**</span></span> <span data-ttu-id="4d560-229">컨트롤러를 서비스에 반환하려면 [StorSimple 장치의 컨트롤러 모듈 교체](storsimple-8000-controller-replacement.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d560-229">To return a controller to service, you must insert it into the chassis as described in [Replace a controller module on your StorSimple device](storsimple-8000-controller-replacement.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d560-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d560-230">Next steps</span></span>
* <span data-ttu-id="4d560-231">StorSimple 장치 컨트롤러에서 이 자습서에 나열된 절차를 사용하여 해결할 수 없는 문제가 발생할 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="4d560-231">If you encounter any issues with your StorSimple device controllers that you cannot resolve by using the procedures listed in this tutorial, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="4d560-232">StorSimple 장치 관리자 서비스를 사용하는 방법을 자세히 알아보려면 [StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 관리](storsimple-8000-manager-service-administration.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="4d560-232">To learn more about using the  StorSimple Device Manager service, go to [Use the  StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

