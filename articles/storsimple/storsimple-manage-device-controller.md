---
title: "StorSimple 장치 컨트롤러 관리 | Microsoft Docs"
description: "StorSimple 장치 컨트롤러를 중지, 다시 시작, 종료 또는 다시 설정하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 67dbb0c4066002256efbab6061157c641527e441
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-storsimple-device-controllers"></a><span data-ttu-id="1aa06-103">StorSimple 장치 컨트롤러 관리</span><span class="sxs-lookup"><span data-stu-id="1aa06-103">Manage your StorSimple device controllers</span></span>
## <a name="overview"></a><span data-ttu-id="1aa06-104">개요</span><span class="sxs-lookup"><span data-stu-id="1aa06-104">Overview</span></span>
<span data-ttu-id="1aa06-105">이 자습서에서는 StorSimple 장치 컨트롤러에서 수행할 수 있는 다양한 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-105">This tutorial describes the different operations that can be performed on your StorSimple device controllers.</span></span> <span data-ttu-id="1aa06-106">StorSimple 장치의 컨트롤러는 능동-수동 구성에서 중복(피어) 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-106">The controllers in your StorSimple device are redundant (peer) controllers in an active-passive configuration.</span></span> <span data-ttu-id="1aa06-107">지정된 시간에 컨트롤러는 하나만 활성화되어 모든 디스크 및 네트워크 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-107">At a given time, only one controller is active and is processing all the disk and network operations.</span></span> <span data-ttu-id="1aa06-108">다른 컨트롤러는 수동 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-108">The other controller is in a passive mode.</span></span> <span data-ttu-id="1aa06-109">활성 컨트롤러에 실패하면 수동 컨트롤러가 자동으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-109">If the active controller fails, the passive controller becomes active automatically.</span></span>

<span data-ttu-id="1aa06-110">이 자습서는 다음을 사용하여 장치 컨트롤러를 관리하도록 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-110">This tutorial includes step-by-step instructions to manage the device controllers by using the:</span></span>

* <span data-ttu-id="1aa06-111">StorSimple Manager 서비스에서 **유지 관리** 페이지의 **컨트롤러** 섹션</span><span class="sxs-lookup"><span data-stu-id="1aa06-111">**Controllers** section of the **Maintenance** page in the StorSimple Manager service</span></span>
* <span data-ttu-id="1aa06-112">StorSimple용 Windows PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-112">Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="1aa06-113">사용자가 StorSimple Manager 서비스를 통해 장치 컨트롤러를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-113">We recommend that you manage the device controllers via the StorSimple Manager service.</span></span> <span data-ttu-id="1aa06-114">StorSimple용 Windows PowerShell을 사용해야 동작을 수행할 수 있는 경우에는 자습서에 관련 메모가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-114">If an action can only be performed by using Windows PowerShell for StorSimple, the tutorial makes a note of it.</span></span>

<span data-ttu-id="1aa06-115">이 자습서를 읽은 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-115">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="1aa06-116">StorSimple 장치 컨트롤러를 다시 시작 또는 종료</span><span class="sxs-lookup"><span data-stu-id="1aa06-116">Restart or shut down a StorSimple device controller</span></span>
* <span data-ttu-id="1aa06-117">StorSimple 장치 종료</span><span class="sxs-lookup"><span data-stu-id="1aa06-117">Shut down a StorSimple device</span></span>
* <span data-ttu-id="1aa06-118">StorSimple 장치를 공장 기본값으로 재설정</span><span class="sxs-lookup"><span data-stu-id="1aa06-118">Reset your StorSimple device to factory defaults</span></span>

## <a name="restart-or-shut-down-a-single-controller"></a><span data-ttu-id="1aa06-119">단일 컨트롤러 다시 시작 또는 종료</span><span class="sxs-lookup"><span data-stu-id="1aa06-119">Restart or shut down a single controller</span></span>
<span data-ttu-id="1aa06-120">컨트롤러 다시 시작 또는 종료는 정상적인 시스템 작업의 일환으로 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-120">A controller restart or shutdown is not required as a part of normal system operation.</span></span> <span data-ttu-id="1aa06-121">단일 장치 컨트롤러에 대한 종료 작업은 실패한 장치 하드웨어 구성 요소가 교체를 필요로 하는 경우에 흔하게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-121">Shutdown operations for a single device controller are common only in cases in which a failed device hardware component requires replacement.</span></span> <span data-ttu-id="1aa06-122">과도한 메모리 사용 또는 작동하지 않는 컨트롤러 때문에 성능이 영향을 받는 경우에도 컨트롤러를 다시 시작할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-122">A controller restart may also be required in a situation in which performance is affected by excessive memory usage or a malfunctioning controller.</span></span> <span data-ttu-id="1aa06-123">또한 대체 컨트롤러를 사용하도록 설정하고 테스트하려면 컨트롤러를 성공적으로 교체한 후에 컨트롤러를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-123">You may also need to restart a controller after a successful controller replacement, if you wish to enable and test the replaced controller.</span></span>

<span data-ttu-id="1aa06-124">수동 컨트롤러를 사용할 수 있다면 장치를 다시 시작해도 연결된 개시 장치를 중단하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-124">Restarting a device is not disruptive to connected initiators, assuming the passive controller is available.</span></span> <span data-ttu-id="1aa06-125">수동 컨트롤러를 사용할 수 없거나 꺼져있는 경우 활성 컨트롤러를 다시 시작하면 서비스 및 가동 중지 시간이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-125">If a passive controller is not available or turned off, then restarting the active controller may result in the disruption of service and downtime.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1aa06-126">**이렇게 하면 중복 손실과 가동 중지 시간 위험 가능성이 높아져서 실행 중인 컨트롤러를 물리적으로 제거하지 말아야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-126">**A running controller should never be physically removed as this would result in a loss of redundancy and an increased risk of downtime.**</span></span>
> * <span data-ttu-id="1aa06-127">다음 절차는 물리적 StorSimple 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-127">The following procedure applies only to the StorSimple physical device.</span></span> <span data-ttu-id="1aa06-128">가상 장치를 시작, 중지 및 다시 시작하는 방법에 대한 자세한 내용은 [가상 장치로 작업](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-128">For information about how to start, stop, and restart the virtual device, see [Work with the virtual device](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).</span></span>
> 
> 

<span data-ttu-id="1aa06-129">StorSimple용 Windows PowerShell 또는 StorSimple Manager 서비스의 Azure 클래식 포털을 사용하여 단일 장치 컨트롤러를 다시 시작하거나 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-129">You can restart or shut down a single device controller by using the Azure classic portal of the StorSimple Manager service or Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="1aa06-130">Azure 클래식 포털에서 장치 컨트롤러를 관리 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-130">To manage your device controllers from the Azure classic portal, perform the following steps.</span></span>

#### <a name="to-restart-or-shut-down-a-controller-in-classic-portal"></a><span data-ttu-id="1aa06-131">클래식 포털에서 컨트롤러를 다시 시작 하거나 종료하려면</span><span class="sxs-lookup"><span data-stu-id="1aa06-131">To restart or shut down a controller in classic portal</span></span>
1. <span data-ttu-id="1aa06-132">**장치 > 유지 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-132">Navigate to **Devices > Maintenance**.</span></span>
2. <span data-ttu-id="1aa06-133">**하드웨어 상태**로 이동하여 장치에서 컨트롤러의 상태가 **정상**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-133">Go to **Hardware Status** and verify that the status of both the controllers on your device is **Healthy**.</span></span>
   
    ![StorSimple 장치 컨트롤러가 정상임을 확인](./media/storsimple-manage-device-controller/IC766017.png)
3. <span data-ttu-id="1aa06-135">**유지 관리** 페이지 아래쪽에서 **컨트롤러 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-135">From the bottom of the **Maintenance** page, click **Manage Controllers**.</span></span>
   
    ![StorSimple 장치 컨트롤러 관리](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > <span data-ttu-id="1aa06-137">**컨트롤러 관리**가 표시되지 않는 경우 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-137">If you cannot see **Manage Controllers**, then you need to install updates.</span></span> <span data-ttu-id="1aa06-138">자세한 내용은 [StorSimple 장치 업데이트](storsimple-update-device.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-138">For more information, see [Update your StorSimple device](storsimple-update-device.md).</span></span>
   > 
   > 
4. <span data-ttu-id="1aa06-139">**컨트롤러 설정 변경** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-139">In the **Change Controller Settings** dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="1aa06-140">**컨트롤러 선택** 드롭다운 목록에서 관리하려는 컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-140">From the **Select Controller** drop-down list, select the controller that you want to manage.</span></span> <span data-ttu-id="1aa06-141">옵션은 컨트롤러 0과 컨트롤러 1입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-141">The options are Controller 0 and Controller 1.</span></span> <span data-ttu-id="1aa06-142">이러한 컨트롤러는 활성 또는 수동으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-142">These controllers are also identified as active or passive.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="1aa06-143">컨트롤러를 사용할 수 없거나 꺼져있으면 관리할 수 없으며 드롭다운 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-143">A controller cannot be managed if it is unavailable or turned off, and it will not appear in the drop-down list.</span></span>
      > 
      > 
   2. <span data-ttu-id="1aa06-144">**작업 선택** 드롭다운 목록에서 **컨트롤러 다시 시작** 또는 **컨트롤러 종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-144">From the **Select Action** drop-down list, choose **Restart controller** or **Shut down controller**.</span></span>
      
       ![StorSimple 장치 수동 컨트롤러 다시 시작](./media/storsimple-manage-device-controller/IC766020.png)
   3. <span data-ttu-id="1aa06-146">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="1aa06-146">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-device-controller/IC740895.png)<span data-ttu-id="1aa06-148">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-148">.</span></span>

<span data-ttu-id="1aa06-149">컨트롤러 종료하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-149">This will restart or shut down the controller.</span></span> <span data-ttu-id="1aa06-150">**컨트롤러 설정 변경** 대화 상자에서 사용자의 선택에 따라 발생한 일의 세부 정보를 아래 테이블에서 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-150">The table below summarizes the details of what happens depending on the selections you have made in the **Change Controller Settings** dialog box.</span></span>  

| <span data-ttu-id="1aa06-151">선택 번호</span><span class="sxs-lookup"><span data-stu-id="1aa06-151">Selection #</span></span> | <span data-ttu-id="1aa06-152">선택한 경우...</span><span class="sxs-lookup"><span data-stu-id="1aa06-152">If you choose to...</span></span> | <span data-ttu-id="1aa06-153">발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-153">This will happen.</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1aa06-154">1.</span><span class="sxs-lookup"><span data-stu-id="1aa06-154">1.</span></span> |<span data-ttu-id="1aa06-155">수동 컨트롤러를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-155">Restart the passive controller.</span></span> |<span data-ttu-id="1aa06-156">작업을 만들어서 작업 컨트롤러를 다시 시작하고 작업이 성공적으로 만들어진 후에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-156">A job will be created to restart the controller, and you will be notified after the job is successfully created.</span></span> <span data-ttu-id="1aa06-157">이 컨트롤러를 다시 시작하도록 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-157">This will initiate the controller restart.</span></span> <span data-ttu-id="1aa06-158">**서비스 > 대시보드 > 작업 로그 보기**에 액세스하여 프로세스 다시 시작을 모니터링하고 서비스에 특정된 매개 변수로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-158">You can monitor the restart process by accessing **Service > Dashboard > View operation logs** and then filtering by parameters specific to your service.</span></span> |
| <span data-ttu-id="1aa06-159">2.</span><span class="sxs-lookup"><span data-stu-id="1aa06-159">2.</span></span> |<span data-ttu-id="1aa06-160">활성 컨트롤러를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-160">Restart the active controller.</span></span> |<span data-ttu-id="1aa06-161">다음과 같은 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-161">You will see the following warning: "If you restart the active controller, the device will fail over to the passive controller.</span></span> <span data-ttu-id="1aa06-162">"활성 컨트롤러를 다시 시작하면 장치는 수동 컨트롤러에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-162">Do you want to continue?"</span></span> </br><span data-ttu-id="1aa06-163">이 작업을 계속하려는 경우 다음 단계는 수동 컨트롤러를 다시 시작하는 데 사용되는 것과 동일합니다(선택 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1aa06-163">If you choose to proceed with this operation, the next steps will be identical to those used to restart the passive controller (see selection 1).</span></span> |
| <span data-ttu-id="1aa06-164">3.</span><span class="sxs-lookup"><span data-stu-id="1aa06-164">3.</span></span> |<span data-ttu-id="1aa06-165">수동 컨트롤러를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-165">Shut down the passive controller.</span></span> |<span data-ttu-id="1aa06-166">다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-166">You will see the following message: "After shutdown is complete, you will need to push the power button on your controller to turn it on.</span></span> <span data-ttu-id="1aa06-167">"종료가 완료된 후에 컨트롤러를 켜기 위해서 전원 단추를 눌러야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-167">Are you sure you want to shut down this controller?"</span></span> </br><span data-ttu-id="1aa06-168">이 작업을 계속하려는 경우 다음 단계는 수동 컨트롤러를 다시 시작하는 데 사용되는 것과 동일합니다(선택 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1aa06-168">If you choose to proceed with this operation, the next steps will be identical to those used to restart the passive controller (see selection 1).</span></span> |
| <span data-ttu-id="1aa06-169">4.</span><span class="sxs-lookup"><span data-stu-id="1aa06-169">4.</span></span> |<span data-ttu-id="1aa06-170">활성 컨트롤러를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-170">Shut down the active controller.</span></span> |<span data-ttu-id="1aa06-171">다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-171">You will see the following message: "After shutdown is complete, you will need to push the power button on your controller to turn it on.</span></span> <span data-ttu-id="1aa06-172">"종료가 완료된 후에 컨트롤러를 켜기 위해서 전원 단추를 눌러야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-172">Are you sure you want to shut down this controller?"</span></span> </br><span data-ttu-id="1aa06-173">이 작업을 계속하려는 경우 다음 단계는 수동 컨트롤러를 다시 시작하는 데 사용되는 것과 동일합니다(선택 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1aa06-173">If you choose to proceed with this operation, the next steps will be identical to those used to restart the passive controller (see selection 1).</span></span> |

#### <a name="to-restart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a><span data-ttu-id="1aa06-174">StorSimple용 Windows PowerShell에서 컨트롤러를 다시 시작하거나 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-174">To restart or shut down a controller in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="1aa06-175">다음 단계를 수행하여 Azure 클래식 포털에서 StorSimple 장치에 단일 컨트롤러를 종료 하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-175">Perform the following steps to shut down or restart a single controller on your StorSimple device from the Azure classic portal.</span></span>

1. <span data-ttu-id="1aa06-176">직렬 콘솔 또는 원격 컴퓨터에서 텔넷 세션을 사용하여 장치에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-176">Access the device by using the serial console or a telnet session from a remote computer.</span></span> <span data-ttu-id="1aa06-177">[장치 직렬 콘솔 연결에 PuTTY 사용](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)단계를 수행하여 컨트롤러 0 또는 컨트롤러 1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-177">Connect to Controller 0 or Controller 1 by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="1aa06-178">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-178">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="1aa06-179">배너 메시지에서 연결된 컨트롤러(컨트롤러 0 또는 컨트롤러 1)와 활성 또는 수동(대기) 컨트롤러 여부를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-179">In the banner message, make a note of the controller you are connected to (Controller 0 or Controller 1) and whether it is the active or the passive (standby) controller.</span></span>
   
   * <span data-ttu-id="1aa06-180">프롬프트에서 단일 컨트롤러를 종료하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-180">To shut down a single controller, at the prompt, type:</span></span>
     
       `Stop-HcsController`
     
       <span data-ttu-id="1aa06-181">연결된 컨트롤러를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-181">This will shut down the controller that you are connected to.</span></span> <span data-ttu-id="1aa06-182">활성 컨트롤러를 중지하면 수동 컨트롤러를 종료하기 전에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-182">If you stop the active controller, then it will fail over to the passive controller before it shuts down.</span></span>
   * <span data-ttu-id="1aa06-183">컨트롤러를 다시 시작하려면 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-183">To restart a controller, at the prompt, type:</span></span>
     
       `Restart-HcsController`
     
       <span data-ttu-id="1aa06-184">연결된 컨트롤러를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-184">This will restart the controller that you are connected to.</span></span> <span data-ttu-id="1aa06-185">활성 컨트롤러를 다시 시작하면 수동 컨트롤러를 다시 시작하기 전에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-185">If you restart the active controller, it will fail over to the passive controller before the restart.</span></span>

## <a name="shut-down-a-storsimple-device"></a><span data-ttu-id="1aa06-186">StorSimple 장치 종료</span><span class="sxs-lookup"><span data-stu-id="1aa06-186">Shut down a StorSimple device</span></span>
<span data-ttu-id="1aa06-187">이 섹션에서는 원격 컴퓨터에서 실행 중이거나 실패한 StorSimple 장치를 종료하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-187">This section explains how to shut down a running or a failed StorSimple device from a remote computer.</span></span> <span data-ttu-id="1aa06-188">장치는 장치 컨트롤러를 종료한 후에 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-188">A device is turned off after shutting down both the device controllers.</span></span> <span data-ttu-id="1aa06-189">장치를 물리적으로 이동하는 경우 장치가 종료되거나 서비스에서 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-189">A device shutdown is done when the device is being physically moved, or is taken out of service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1aa06-190">장치를 종료하기 전에 장치 구성 요소의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-190">Before you shut down the device, check the health of the device components.</span></span> <span data-ttu-id="1aa06-191">**장치 > 유지 관리 > 하드웨어 상태**로 이동하고 모든 구성 요소의 LED 상태가 녹색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-191">Navigate to **Devices > Maintenance > Hardware Status** and verify that the LED status of all the components is green.</span></span> <span data-ttu-id="1aa06-192">정상 장치만이 녹색 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-192">Only a healthy device will have a green status.</span></span> <span data-ttu-id="1aa06-193">장치가 종료되어 작동하지 않는 구성 요소를 교체하는 경우 해당 구성 요소에 실패(빨간색) 또는 성능 저하(노란색) 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-193">If your device is being shut down to replace a malfunctioning component, you will see a failed (red) or a degraded (yellow) status for the respective component(s).</span></span>
> 
> 

#### <a name="to-shut-down-a-storsimple-device"></a><span data-ttu-id="1aa06-194">StorSimple 장치 종료하려면</span><span class="sxs-lookup"><span data-stu-id="1aa06-194">To shut down a StorSimple device</span></span>
1. <span data-ttu-id="1aa06-195">[컨트롤러 다시 시작 또는 종료](#restart-or-shut-down-a-single-controller) 프로시저를 사용하여 장치에서 수동 컨트롤러를 식별하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-195">Use the [restart or shut down a controller](#restart-or-shut-down-a-single-controller) procedure to identify and shut down the passive controller on your device.</span></span> <span data-ttu-id="1aa06-196">Azure 클래식 포털 또는 StorSimple용 Windows PowerShell에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-196">You can perform this operation in the Azure classic portal or in Windows PowerShell for StorSimple.</span></span>
2. <span data-ttu-id="1aa06-197">활성 컨트롤러를 종료하려면 위의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-197">Repeat the above step to shut down the active controller.</span></span>
3. <span data-ttu-id="1aa06-198">이제 장치 뒤쪽 평면을 살펴봐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-198">You will now need to look at the back plane of the device.</span></span> <span data-ttu-id="1aa06-199">두 컨트롤러를 완전히 종료한 후에 두 컨트롤러에서 상태 LED가 빨간색으로 깜박여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-199">After the two controllers are completely shut down, the status LEDs on both the controllers should be blinking red.</span></span> <span data-ttu-id="1aa06-200">이번에 장치를 완전히 해제해야 하면 전원 및 냉각 모듈(PCM) 모두에서 전원 스위치를 끄기 위치에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-200">If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.</span></span> <span data-ttu-id="1aa06-201">이 장치를 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-201">This should turn off the device.</span></span>

<!--#### To shut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect to the serial console of the StorSimple device by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In the serial console menu, verify from the banner message that the controller you are connected to is the passive controller. If you are connected to the active controller, disconnect from this controller and connect to the other controller.

1. In the serial console menu, choose option 1, **log in with full access**.

1. At the prompt, type:

    `Stop-HCSController`

    This should shut down the current controller. To verify whether the shutdown has finished, check the back of the device. The controller status LED should be solid red.

1. Repeat steps 1 through 4 to connect to the active controller and then shut it down.

1. After both the controllers are completely shut down, the status LEDs on both should be blinking red. If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.-->

## <a name="reset-the-device-to-factory-default-settings"></a><span data-ttu-id="1aa06-202">장치를 공장 기본 설정으로 재설정</span><span class="sxs-lookup"><span data-stu-id="1aa06-202">Reset the device to factory default settings</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1aa06-203">장치를 공장 기본 설정으로 재설정해야 할 경우 Microsoft 지원 서비스에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-203">If you need to reset your device to factory default settings, contact Microsoft Support.</span></span> <span data-ttu-id="1aa06-204">아래에 설명된 절차는 Microsoft 기술 지원 서비스에 따라서만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-204">The procedure described below should be used only in conjunction with Microsoft Support.</span></span>
> 
> 

<span data-ttu-id="1aa06-205">이 절차는 StorSimple용 Windows PowerShell을 사용하여 Microsoft Azure StorSimple 장치를 공장 기본 설정으로 다시 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-205">This procedure describes how to reset your Microsoft Azure StorSimple device to factory default settings using Windows PowerShell for StorSimple.</span></span>
<span data-ttu-id="1aa06-206">장치를 다시 설정하면 기본적으로 전체 클러스터에서 모든 데이터 및 설정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-206">Resetting a device removes all data and settings from the entire cluster by default.</span></span>

<span data-ttu-id="1aa06-207">Microsoft Azure StorSimple 장치를 공장 기본 설정으로 다시 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-207">Perform the following steps to reset your Microsoft Azure StorSimple device to factory default settings:</span></span>

### <a name="to-reset-the-device-to-default-settings-in-windows-powershell-for-storsimple"></a><span data-ttu-id="1aa06-208">StorSimple용 Windows PowerShell의 기본 설정으로 장치를 재설정하려면</span><span class="sxs-lookup"><span data-stu-id="1aa06-208">To reset the device to default settings in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="1aa06-209">직렬 콘솔을 통해 장치에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-209">Access the device through its serial console.</span></span> <span data-ttu-id="1aa06-210">활성 컨트롤러에 연결하려면 배너 메시지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-210">Check the banner message to ensure that you are connected to the Active controller.</span></span>
2. <span data-ttu-id="1aa06-211">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-211">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="1aa06-212">프롬프트에서 전체 클러스터를 다시 설정하는 다음 명령을 입력하면 모든 데이터, 메타데이터 및 컨트롤러 설정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-212">At the prompt, type the following command to reset the entire cluster, removing all data, metadata, and controller settings:</span></span>
   
    `Reset-HcsFactoryDefault`
   
    <span data-ttu-id="1aa06-213">대신 단일 컨트롤러를 재설정하려면 `-scope` 매개 변수가 있는 [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-213">To instead reset a single controller, use the  [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet with the `-scope` parameter.)</span></span>
   
    <span data-ttu-id="1aa06-214">시스템을 여러 번 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-214">The system will reboot multiple times.</span></span> <span data-ttu-id="1aa06-215">재설정이 성공적으로 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-215">You will be notified when the reset has successfully completed.</span></span> <span data-ttu-id="1aa06-216">시스템 모델에 따라 이 프로세스를 완료 하는 데 8100 장치로 45-60분이 걸리고 8600 장치로 60-90분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-216">Depending on the system model, it can take 45-60 minutes for an 8100 device and 60-90 minutes for an 8600 to finish this process.</span></span>
   
   > [!TIP]
   > * <span data-ttu-id="1aa06-217">업데이트 1.2 이상을 사용하는 경우 `–SkipFirmwareVersionCheck` 매개 변수를 사용하여 펌웨어 버전 확인을 건너뜁니다(아니면 펌웨어 불일치 에러가 표시되며 펌웨어 버전의 불일치로 인해 펌웨어 버전의 불일치 때문에 공장 재설정을 계속할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="1aa06-217">If you're using Update 1.2 or earlier use the `–SkipFirmwareVersionCheck` parameter to skip the firmware version check (otherwise you'll see a firmware mismatch error: Factory reset cannot continue due to a mismatch in the firmware versions.</span></span> <span data-ttu-id="1aa06-218">)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-218">).</span></span>
   > * <span data-ttu-id="1aa06-219">정부 포털에서 업데이트 1 또는 1.1을 실행하고, 단일 또는 이중 컨트롤러 교체(업데이트 1 이전 소프트웨어와 함께 제공된 교체 컨트롤러)를 성공적으로 수행한 StorSimple 장치에서는 공장 재설정 절차에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-219">The factory reset procedure may fail for StorSimple devices that are running Update 1 or 1.1 in the Government portal and have performed a successful single or dual controller replacement (with replacement controllers that were shipped with pre-Update 1 software).</span></span> <span data-ttu-id="1aa06-220">이는 공장 재설정 이미지가 업데이트 1 이전 소프트웨어에 대해 존재하지 않는 컨트롤러의 SHA1 파일 존재에 대해 유효성이 검사된 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-220">This happens when the factory reset image is validated for the presence of a SHA1 file on the controller that does not exist for pre-Update 1 software.</span></span> <span data-ttu-id="1aa06-221">이 공장 재설정 오류가 표시되면 Microsoft 지원에 문의하여 다음 단계에 대한 지원을 받으세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-221">If you see this factory reset failure, contact Microsoft Support to assist you with the next steps.</span></span> <span data-ttu-id="1aa06-222">업데이트 1 이상 소프트웨어와 함께 공장에서 배송된 교체 컨트롤러에는 이 문제가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-222">This issue is not seen with replacement controllers that were shipped from the factory with Update 1 or later software.</span></span>
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a><span data-ttu-id="1aa06-223">장치 컨트롤러를 관리하는 방법에 대한 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="1aa06-223">Questions and answers about managing device controllers</span></span>
<span data-ttu-id="1aa06-224">이 섹션에서는 StorSimple 장치 컨트롤러의 관리와 관련하여 자주 묻는 질문 중 일부를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-224">In this section, we have summarized some of the frequently asked questions regarding managing StorSimple device controllers.</span></span>

<span data-ttu-id="1aa06-225">**Q.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-225">**Q.**</span></span> <span data-ttu-id="1aa06-226">장치에서 컨트롤러가 모두 정상이고 켜져 있으며 활성 컨트롤러를 다시 시작 또는 종료하는 경우 무엇이 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="1aa06-226">What happens if both the controllers on my device are healthy and turned on and I restart or shut down the active controller?</span></span>

<span data-ttu-id="1aa06-227">**A.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-227">**A.**</span></span> <span data-ttu-id="1aa06-228">장치에서 컨트롤러가 모두 정상이고 켜져 있는 경우 확인을 위한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-228">If both the controllers on your device are healthy and turned on, you will be prompted for confirmation.</span></span> <span data-ttu-id="1aa06-229">선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-229">You may choose to:</span></span>

* <span data-ttu-id="1aa06-230">**활성 컨트롤러 다시 시작** – 활성 컨트롤러를 다시 시작하면 장치가 수동 컨트롤러로 장애 조치(failover)된다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-230">**Restart the active controller** – You will be notified that restarting an active controller will cause the device to fail over to the passive controller.</span></span> <span data-ttu-id="1aa06-231">컨트롤러가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-231">The controller will restart.</span></span>
* <span data-ttu-id="1aa06-232">**활성 컨트롤러 종료** – 활성 컨트롤러를 종료하면 가동이 중지된다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-232">**Shut down an active controller** – You will be notified that shutting down an active controller will result in downtime.</span></span> <span data-ttu-id="1aa06-233">컨트롤러를 켜기 위해 장치에서 전원 단추를 눌러야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-233">You will also need to push the power button on the device to turn on the controller.</span></span>

<span data-ttu-id="1aa06-234">**Q.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-234">**Q.**</span></span> <span data-ttu-id="1aa06-235">장치에서 수동 컨트롤러가 모두 정상이고 켜져 있으며 활성 컨트롤러를 다시 시작 또는 종료하는 경우 무엇이 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="1aa06-235">What happens if the passive controller on my device is unavailable or turned off and I restart or shut down the active controller?</span></span>

<span data-ttu-id="1aa06-236">**A.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-236">**A.**</span></span> <span data-ttu-id="1aa06-237">장치에서 수동 컨트롤러를 사용할 수 없거나 해제된 경우 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-237">If the passive controller on your device is unavailable or turned off, and you choose to:</span></span>

* <span data-ttu-id="1aa06-238">**활성 컨트롤러 다시 시작** – 작업을 계속하면 서비스의 임시 중단이 발생하고 확인 메시지가 표시된다는 내용의 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-238">**Restart the active controller** – You will be notified that continuing the operation will result in a temporary disruption of the service, and you will be prompted for confirmation.</span></span>
* <span data-ttu-id="1aa06-239">**활성 컨트롤러 종료** – 작업을 계속하면 가동 중지 시간이 발생하고 장치를 켜기 위해 하나 또는 두 컨트롤러 모두에서 전원 단추를 눌러야 한다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-239">**Shut down an active controller** – You will be notified that continuing the operation will result in downtime, and that you will need to push the power button on one or both controllers to turn on the device.</span></span> <span data-ttu-id="1aa06-240">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-240">You will be prompted for confirmation.</span></span>

<span data-ttu-id="1aa06-241">**Q.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-241">**Q.**</span></span> <span data-ttu-id="1aa06-242">어떤 경우에 컨트롤러를 다시 시작 또는 종료를 진행하는 데 실패합니까?</span><span class="sxs-lookup"><span data-stu-id="1aa06-242">When does the controller restart or shutdown fails to progress?</span></span>

<span data-ttu-id="1aa06-243">**A.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-243">**A.**</span></span> <span data-ttu-id="1aa06-244">다음 경우 롤러를 다시 시작하거나 종료하는 데 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-244">Restarting or shutting down a controller may fail if:</span></span>

* <span data-ttu-id="1aa06-245">장치 업데이트를 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-245">A device update is in progress.</span></span>
* <span data-ttu-id="1aa06-246">컨트롤러 다시 시작이 이미 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-246">A controller restart is already in progress.</span></span>
* <span data-ttu-id="1aa06-247">컨트롤러 종료가 이미 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-247">A controller shutdown is already in progress.</span></span>

<span data-ttu-id="1aa06-248">**Q.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-248">**Q.**</span></span> <span data-ttu-id="1aa06-249">컨트롤러를 다시 시작하거나 종료하는 경우 어떻게 확인합니까?</span><span class="sxs-lookup"><span data-stu-id="1aa06-249">How can you figure out if a controller was restarted or shut down?</span></span>

<span data-ttu-id="1aa06-250">**A.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-250">**A.**</span></span> <span data-ttu-id="1aa06-251">유지 관리 페이지에서 컨트롤러의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-251">You can check the controller status on the Maintenance page.</span></span> <span data-ttu-id="1aa06-252">컨트롤러의 상태는 컨트롤러가 다시 시작하거나 종료되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-252">The controller status will indicate whether a controller has been restarted or shut down.</span></span> <span data-ttu-id="1aa06-253">또한 컨트롤러가 다시 시작하거나 종료된 경우 경고 페이지는 정보 경고를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-253">Additionally, the Alerts page will contain an informational alert if the controller was restarted or shut down.</span></span> <span data-ttu-id="1aa06-254">컨트롤러 다시 시작 및 종료 작업은 작업 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-254">The controller restart and shutdown operations are also recorded in the operation logs.</span></span> <span data-ttu-id="1aa06-255">작업 로그에 대한 자세한 내용을 보려면 [작업 로그 보기](storsimple-service-dashboard.md#view-the-operations-logs)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-255">For more information about operation logs, go to [View the operation logs](storsimple-service-dashboard.md#view-the-operations-logs).</span></span>

<span data-ttu-id="1aa06-256">**Q.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-256">**Q.**</span></span> <span data-ttu-id="1aa06-257">컨트롤러 장애 조치의 결과로써 I/O에 영향이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="1aa06-257">Is there any impact to the I/Os as a result of controller failover?</span></span>

<span data-ttu-id="1aa06-258">**A.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-258">**A.**</span></span> <span data-ttu-id="1aa06-259">초기자 및 활성 컨트롤러 간의 TCP 연결은 컨트롤러 장애 조치의 결과로 재설정되지만 수동 컨트롤러가 작업을 가정하는 경우 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-259">The TCP connections between initiators and active controller will be reset as a result of controller failover, but will be reestablished when the passive controller assumes operation.</span></span> <span data-ttu-id="1aa06-260">이 작업의 과정에서 초기자와 장치 간의 I/O 작업에서 임시(30초 미만) 일시 정지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa06-260">There may be a temporary (less than 30 seconds) pause in I/O activity between initiators and the device during the course of this operation.</span></span>

<span data-ttu-id="1aa06-261">**Q.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-261">**Q.**</span></span> <span data-ttu-id="1aa06-262">컨트롤러를 서비스에서 종료하고 제거한 후에 서비스에 반환하는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="1aa06-262">How do I return my controller to service after it has been shut down and removed?</span></span>

<span data-ttu-id="1aa06-263">**A.**</span><span class="sxs-lookup"><span data-stu-id="1aa06-263">**A.**</span></span> <span data-ttu-id="1aa06-264">컨트롤러를 서비스에 반환하려면 [StorSimple 장치의 컨트롤러 모듈 교체](storsimple-controller-replacement.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-264">To return a controller to service, you must insert it into the chassis as described in [Replace a controller module on your StorSimple device](storsimple-controller-replacement.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa06-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1aa06-265">Next steps</span></span>
* <span data-ttu-id="1aa06-266">StorSimple 장치 컨트롤러에서 이 자습서에 나열된 절차를 사용하여 해결할 수 없는 문제가 발생할 경우 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-266">If you encounter any issues with your StorSimple device controllers that you cannot resolve by using the procedures listed in this tutorial, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="1aa06-267">StorSimple Manager 서비스를 사용하는 방법을 자세히 알아보려면 [StorSimple Manager 서비스를 사용하여 StorSimple 장치 관리](storsimple-manager-service-administration.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa06-267">To learn more about using the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

