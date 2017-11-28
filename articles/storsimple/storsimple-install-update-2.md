---
title: "StorSimple 장치에 업데이트 2 설치 | Microsoft Docs"
description: "StorSimple 8000 시리즈 장치에서 StorSimple 8000 시리즈 업데이트 2를 설치하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: e788439608b7122f2bca6b99b832baa5258e472d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a><span data-ttu-id="eb236-103">StorSimple 장치에 업데이트 2 설치</span><span class="sxs-lookup"><span data-stu-id="eb236-103">Install Update 2 on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="eb236-104">개요</span><span class="sxs-lookup"><span data-stu-id="eb236-104">Overview</span></span>
<span data-ttu-id="eb236-105">이 자습서에서는 Azure 클래식 포털을 통해 이전 소프트웨어 버전을 실행하는 StorSimple 장치에 업데이트 2를 설치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-105">This tutorial explains how to install Update 2 on a StorSimple device running an earlier software version via the Azure classic portal.</span></span> <span data-ttu-id="eb236-106">또한 이 자습서는 StorSimple 장치의 DATA 0 이외의 다른 네트워크 인터페이스에서 게이트웨이를 구성하고 업데이트 1 이전 소프트웨어 버전에서 업데이트를 시도하는 경우 업데이트에 필요한 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-106">The tutorial also covers the steps required for the update when a gateway is configured on a network interface other than DATA 0 of the StorSimple device and you are trying to update from a pre-Update 1 software version.</span></span>

<span data-ttu-id="eb236-107">업데이트 2는 장치 소프트웨어 업데이트, LSI 드라이버 업데이트 및 디스크 펌웨어 업데이트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-107">Update 2 includes device software updates, LSI driver updates, and disk firmware updates.</span></span> <span data-ttu-id="eb236-108">장치 소프트웨어 및 LSI 업데이트는 무중단 업데이트이며 Azure 클래식 포털을 통해 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-108">The device software and LSI updates are non-disruptive updates and can be applied via the Azure classic portal.</span></span> <span data-ttu-id="eb236-109">디스크 펌웨어 업데이트는 작업 중단 업데이트이며 장치의 Windows PowerShell 인터페이스를 통해서만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-109">The disk firmware updates are disruptive updates and can only be applied via the Windows PowerShell interface of the device.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="eb236-110">업데이트의 단계적 롤아웃을 수행하기 때문에 즉시 업데이트 2를 볼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-110">You may not see Update 2 immediately because we do a phased rollout of the updates.</span></span> <span data-ttu-id="eb236-111">해당 업데이트를 곧 사용할 수 있게 되므로 몇 일 후에 업데이트를 스캔합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-111">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="eb236-112">설치하기 전에 일련의 수동 및 자동 전 검사를 수행하며 하드웨어 상태 및 네트워크 연결 측면에서 장치 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-112">A set of manual and automatic pre-checks are done prior to the install to determine the device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="eb236-113">Azure 클래식 포털에서 업데이트를 적용하는 경우 이러한 사전 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-113">These pre-checks are performed only if you apply the updates from the Azure classic portal.</span></span>
> * <span data-ttu-id="eb236-114">Azure 클래식 포털을 통해 소프트웨어 및 드라이버 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-114">We recommend that you install the software and driver updates via the Azure  classic portal.</span></span> <span data-ttu-id="eb236-115">포털에서 사전 업데이트 게이트웨이 검사가 실패한 경우 (업데이트를 설치하려면) 장치의 Windows PowerShell 인터페이스로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-115">You should only go to the Windows PowerShell interface of the device (to install updates) if the pre-update gateway check fails in the portal.</span></span> <span data-ttu-id="eb236-116">업데이트를 설치하는 데 4-7시간이 걸릴 수 있습니다(Windows 업데이트 포함).</span><span class="sxs-lookup"><span data-stu-id="eb236-116">The updates may take 4-7 hours to install (including the Windows Updates).</span></span> <span data-ttu-id="eb236-117">장치의 Windows PowerShell 인터페이스를 통해 유지 관리 모드 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-117">The maintenance mode updates must be installed via the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="eb236-118">유지 관리 모드 업데이트는 중단 업데이트입니다. 이는 장치에 중단 시간을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-118">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> * <span data-ttu-id="eb236-119">선택적 StorSimple Snapshot Manager를 실행하는 경우 장치를 업데이트하기 전에 Snapshot Manager 버전을 업데이트 2로 업그레이드했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-119">If running the optional StorSimple Snapshot Manager, ensure that you have upgraded your Snapshot Manager version to Update 2 prior to updating the device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-the-azure-classic-portal"></a><span data-ttu-id="eb236-120">Azure 클래식 포털을 통해 업데이트 2 설치</span><span class="sxs-lookup"><span data-stu-id="eb236-120">Install Update 2 via the Azure classic portal</span></span>
<span data-ttu-id="eb236-121">다음 단계를 수행하여 장치를 [업데이트 2](storsimple-update2-release-notes.md)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-121">Perform the following steps to update your device to [Update 2](storsimple-update2-release-notes.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eb236-122">업데이트 2를 통해 Microsoft는 장치로부터 추가적인 진단 정보를 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-122">Update 2 enables Microsoft to pull additional diagnostic information from the device.</span></span> <span data-ttu-id="eb236-123">따라서 운영 팀에서 문제가 있는 장치를 확인하는 경우, 장치로부터 정보를 수집하고 문제를 진단할 준비가 더욱 잘 갖추어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-123">As a result, when our operations team identifies devices that are having problems, we are better equipped to collect information from the device and diagnose issues.</span></span> <span data-ttu-id="eb236-124">업데이트 2를 수락하면, 이러한 주도적 지원을 제공해도 된다고 허락하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-124">By accepting Update 2, you allow us to provide this proactive support.</span></span>
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="eb236-125">장치가 **StorSimple 8000 시리즈 업데이트 2(6.3.9600.17673)**를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-125">Verify that your device is running **StorSimple 8000 Series Update 2 (6.3.9600.17673)**.</span></span> <span data-ttu-id="eb236-126">**마지막 업데이트 날짜** 도 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-126">The **Last updated date** should also be modified.</span></span> <span data-ttu-id="eb236-127">또한 유지 관리 모드 업데이트가 사용 가능하다고 표시됩니다(이 메시지는 업데이트를 설치한 후 최대 24시간 동안 계속 표시될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="eb236-127">You'll also see that Maintenance mode updates are available (this message might continue to be displayed for up to 24 hours after you install the updates).</span></span>
   
   <span data-ttu-id="eb236-128">유지 관리 모드 업데이트는 작업 중단 업데이트이므로 장치 가동 중지 시간이 발생할 수 있으며, 장치의 Windows PowerShell 인터페이스를 통해서만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-128">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via the Windows PowerShell interface of your device.</span></span> <span data-ttu-id="eb236-129">일부 경우에 업데이트 1.2를 실행할 때 디스크 펌웨어가 이미 있을 최신 버전일 수 있습니다. 이 경우 모든 유지 관리 모드 업데이트를 설치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-129">In some cases when you are running Update 1.2, your disk firmware might already be up-to-date, in which case you don't need to install any maintenance mode updates.</span></span>
2. <span data-ttu-id="eb236-130">[핫픽스를 다운로드하려면](#to-download-hotfixes)에 나열된 단계를 사용하여 유지 관리 모드 업데이트를 다운로드한 후 KB3121899를 검색한 후 다운로드합니다. 이 KB는 디스크 펌웨어 업데이트를 설치합니다(다른 업데이트가 이미 설치되어 있어야 함).</span><span class="sxs-lookup"><span data-stu-id="eb236-130">Download the maintenance mode updates by using the steps listed in [To download hotfixes](#to-download-hotfixes) to search for and download KB3121899, which installs disk firmware updates (the other updates should already be installed by now).</span></span>
3. <span data-ttu-id="eb236-131">[유지 관리 모드 핫픽스 설치 및 확인](#to-install-and-verify-maintenance-mode-hotfixes) 에 나열된 단계를 따라 유지 관리 모드 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-131">Follow the steps listed in [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) to install the maintenance mode updates.</span></span>

## <a name="install-update-2-as-a-hotfix"></a><span data-ttu-id="eb236-132">핫픽스로 업데이트 2 설치</span><span class="sxs-lookup"><span data-stu-id="eb236-132">Install Update 2 as a hotfix</span></span>
<span data-ttu-id="eb236-133">Azure 클래식 포털을 통해 업데이트를 설치하려고 할 때 게이트웨이 검사에 실패하는 경우 이 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-133">Use this procedure if you fail the gateway check when trying to install the updates through the Azure classic portal.</span></span> <span data-ttu-id="eb236-134">비데이터 0 네트워크 인터페이스에 할당된 게이트웨이가 있고 장치가 업데이트 1 이전의 소프트웨어 버전을 실행하는 경우 확인이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-134">The check fails as you have a gateway assigned to a non-DATA 0 network interface and your device is running a software version prior to Update 1.</span></span>

<span data-ttu-id="eb236-135">핫픽스 메서드를 사용하여 업그레이드할 수 있는 소프트웨어 버전은 업데이트 0.1, 업데이트 0.2, 업데이트 0.3, 업데이트 1, 업데이트 1.1, 업데이트 1.2입니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-135">The software versions that can be upgraded using the hotfix method are Update 0.1, Update 0.2, and Update 0.3, Update 1, Update 1.1, and Update 1.2.</span></span> <span data-ttu-id="eb236-136">핫픽스 메서드에는 다음 세 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-136">The hotfix method involves the following three steps:</span></span>

* <span data-ttu-id="eb236-137">Microsoft Update 카탈로그에서 핫픽스를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-137">Download the hotfixes from the Microsoft Update Catalog.</span></span>
* <span data-ttu-id="eb236-138">일반 모드 핫픽스를 설치 및 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-138">Install and verify the regular mode hotfixes.</span></span>
* <span data-ttu-id="eb236-139">유지 관리 모드 핫픽스를 설치 및 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-139">Install and verify the maintenance mode hotfix.</span></span>

<span data-ttu-id="eb236-140">업데이트 2를 핫픽스로 설치하려면 다음 핫픽스를 다운로드한 후 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-140">To install Update 2 as a hotfix, you must download and install the following hotfixes:</span></span>

| <span data-ttu-id="eb236-141">순서</span><span class="sxs-lookup"><span data-stu-id="eb236-141">Order</span></span> | <span data-ttu-id="eb236-142">KB</span><span class="sxs-lookup"><span data-stu-id="eb236-142">KB</span></span> | <span data-ttu-id="eb236-143">설명</span><span class="sxs-lookup"><span data-stu-id="eb236-143">Description</span></span> | <span data-ttu-id="eb236-144">업데이트 유형</span><span class="sxs-lookup"><span data-stu-id="eb236-144">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eb236-145">1</span><span class="sxs-lookup"><span data-stu-id="eb236-145">1</span></span> |<span data-ttu-id="eb236-146">KB3121901</span><span class="sxs-lookup"><span data-stu-id="eb236-146">KB3121901</span></span> |<span data-ttu-id="eb236-147">소프트웨어 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb236-147">Software update</span></span> |<span data-ttu-id="eb236-148">일반</span><span class="sxs-lookup"><span data-stu-id="eb236-148">Regular</span></span> |
| <span data-ttu-id="eb236-149">2</span><span class="sxs-lookup"><span data-stu-id="eb236-149">2</span></span> |<span data-ttu-id="eb236-150">KB3121900</span><span class="sxs-lookup"><span data-stu-id="eb236-150">KB3121900</span></span> |<span data-ttu-id="eb236-151">LSI 드라이버</span><span class="sxs-lookup"><span data-stu-id="eb236-151">LSI driver</span></span> |<span data-ttu-id="eb236-152">일반</span><span class="sxs-lookup"><span data-stu-id="eb236-152">Regular</span></span> |
| <span data-ttu-id="eb236-153">3</span><span class="sxs-lookup"><span data-stu-id="eb236-153">3</span></span> |<span data-ttu-id="eb236-154">KB3080728</span><span class="sxs-lookup"><span data-stu-id="eb236-154">KB3080728</span></span> |<span data-ttu-id="eb236-155">Storport 픽스 </span><span class="sxs-lookup"><span data-stu-id="eb236-155">Storport fix</span></span> </br> <span data-ttu-id="eb236-156">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="eb236-156">Windows Server 2012 R2</span></span> |<span data-ttu-id="eb236-157">일반</span><span class="sxs-lookup"><span data-stu-id="eb236-157">Regular</span></span> |
| <span data-ttu-id="eb236-158">4</span><span class="sxs-lookup"><span data-stu-id="eb236-158">4</span></span> |<span data-ttu-id="eb236-159">KB3090322</span><span class="sxs-lookup"><span data-stu-id="eb236-159">KB3090322</span></span> |<span data-ttu-id="eb236-160">Spaceport 픽스 </span><span class="sxs-lookup"><span data-stu-id="eb236-160">Spaceport fix</span></span> </br> <span data-ttu-id="eb236-161">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="eb236-161">Windows Server 2012 R2</span></span> |<span data-ttu-id="eb236-162">일반</span><span class="sxs-lookup"><span data-stu-id="eb236-162">Regular</span></span> |
| <span data-ttu-id="eb236-163">5</span><span class="sxs-lookup"><span data-stu-id="eb236-163">5</span></span> |<span data-ttu-id="eb236-164">KB3121899</span><span class="sxs-lookup"><span data-stu-id="eb236-164">KB3121899</span></span> |<span data-ttu-id="eb236-165">디스크 펌웨어</span><span class="sxs-lookup"><span data-stu-id="eb236-165">Disk firmware</span></span> |<span data-ttu-id="eb236-166">유지 관리</span><span class="sxs-lookup"><span data-stu-id="eb236-166">Maintenance</span></span> |

> [!IMPORTANT]
> * <span data-ttu-id="eb236-167">장치가 릴리스(GA) 버전을 실행하는 경우 이 업데이트 설치를 위한 지원을 받으려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="eb236-167">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) to assist you with the update.</span></span>
> * <span data-ttu-id="eb236-168">이 절차는 업데이트 2에만 적용하도록 한 번만 수행해야 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-168">This procedure needs to be performed only once to apply Update 2.</span></span> <span data-ttu-id="eb236-169">Azure 클래식 포털을 사용하여 후속 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-169">You can use the Azure classic portal to apply subsequent updates.</span></span>
> * <span data-ttu-id="eb236-170">각 핫픽스 설치를 완료하려면 약 20분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-170">Each hotfix installation can take about 20 minutes to complete.</span></span> <span data-ttu-id="eb236-171">총 설치 시간은 2시간에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-171">Total install time is close to 2 hours.</span></span>
> * <span data-ttu-id="eb236-172">이 절차에 따라 업데이트를 적용하기 전에 두 장치 컨트롤러가 온라인 상태이고 모든 하드웨어 구성 요소가 정상 상태에 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-172">Before using this procedure to apply the update, make sure that both device controllers are online and all the hardware components are healthy.</span></span>
> 
> 

<span data-ttu-id="eb236-173">다음 단계를 수행하여 이 업데이트를 핫픽스로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-173">Perform the following steps to apply this update as a hotfix.</span></span>

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="eb236-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb236-174">Next steps</span></span>
<span data-ttu-id="eb236-175">[업데이트 2 릴리스](storsimple-update2-release-notes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb236-175">Learn more about the [Update 2 release](storsimple-update2-release-notes.md).</span></span>

