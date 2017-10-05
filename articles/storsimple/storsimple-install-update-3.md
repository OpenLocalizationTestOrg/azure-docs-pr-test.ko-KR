---
title: "StorSimple 장치에 업데이트 3 설치 | Microsoft Docs"
description: "StorSimple 8000 시리즈 장치에서 StorSimple 8000 시리즈 업데이트 3를 설치하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 72b004a6c2604e0fc20b71b4b69217622f8f9ea0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a><span data-ttu-id="be92e-103">StorSimple 8000 시리즈 장치에 업데이트 3 설치</span><span class="sxs-lookup"><span data-stu-id="be92e-103">Install Update 3 on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="be92e-104">개요</span><span class="sxs-lookup"><span data-stu-id="be92e-104">Overview</span></span>

<span data-ttu-id="be92e-105">이 자습서에서는 Azure 클래식 포털을 통해서와 핫픽스 방법을 사용하여 이전 소프트웨어 버전을 실행하는 StorSimple 장치에 업데이트 3을 설치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-105">This tutorial explains how to install Update 3 on a StorSimple device running an earlier software version via the Azure classic portal and using the hotfix method.</span></span> <span data-ttu-id="be92e-106">핫픽스 방법은 StorSimple 장치의 DATA 0 이외의 네트워크 인터페이스에 게이트웨이가 구성되어 있고 업데이트 1 이전 소프트웨어 버전에서 업데이트하려는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-106">The hotfix method is used when a gateway is configured on a network interface other than DATA 0 of the StorSimple device and you are trying to update from a pre-Update 1 software version.</span></span>

<span data-ttu-id="be92e-107">업데이트 3에는 장치 소프트웨어, LSI 드라이버 및 펌웨어, Storport 및 Spaceport 업데이트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-107">Update 3 includes device software, LSI driver and firmware, Storport and Spaceport updates.</span></span> <span data-ttu-id="be92e-108">업데이트 2 또는 이전 버전에서 업데이트하는 경우 iSCSI, WMI를 적용해야 하며 경우에 따라 디스크 펌웨어 업데이트도 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-108">If updating from Update 2 or an earlier version, you will also be required to apply iSCSI, WMI, and in certain cases, disk firmware updates.</span></span> <span data-ttu-id="be92e-109">장치 소프트웨어, WMI, iSCSI, LSI 드라이버, Spaceport 및 Storport 픽스는 무중단 업데이트이며 Azure 클래식 포털을 통해 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-109">The device software, WMI, iSCSI, LSI driver, Spaceport, and Storport fixes are non-disruptive updates and can be applied via the Azure classic portal.</span></span> <span data-ttu-id="be92e-110">디스크 펌웨어 업데이트는 작업 중단 업데이트이며 장치의 Windows PowerShell 인터페이스를 통해서만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-110">The disk firmware updates are disruptive updates and can only be applied via the Windows PowerShell interface of the device.</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="be92e-111">설치하기 전에 일련의 수동 및 자동 전 검사를 수행하며 하드웨어 상태와 네트워크 연결 측면에서 장치 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-111">A set of manual and automatic pre-checks are done prior to the install to determine the device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="be92e-112">Azure 클래식 포털에서 업데이트를 적용하는 경우 이러한 사전 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-112">These pre-checks are performed only if you apply the updates from the Azure classic portal.</span></span>
> * <span data-ttu-id="be92e-113">Azure 클래식 포털을 통해 소프트웨어 및 드라이버 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-113">We recommend that you install the software and driver updates via the Azure  classic portal.</span></span> <span data-ttu-id="be92e-114">포털에서 사전 업데이트 게이트웨이 검사가 실패한 경우 (업데이트를 설치하려면) 장치의 Windows PowerShell 인터페이스로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-114">You should only go to the Windows PowerShell interface of the device (to install updates) if the pre-update gateway check fails in the portal.</span></span> <span data-ttu-id="be92e-115">업데이트하는 버전에 따라 업데이트 설치에 1.5~2.5시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-115">Depending upon the version you are updating from, the updates may take 1.5-2.5 hours to install.</span></span> <span data-ttu-id="be92e-116">장치의 Windows PowerShell 인터페이스를 통해 유지 관리 모드 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-116">The maintenance mode updates must be installed via the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="be92e-117">유지 관리 모드 업데이트는 중단 업데이트입니다. 이는 장치에 중단 시간을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-117">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> * <span data-ttu-id="be92e-118">선택적 StorSimple Snapshot Manager를 실행하는 경우 장치를 업데이트하기 전에 Snapshot Manager 버전을 업데이트 2로 업그레이드했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-118">If running the optional StorSimple Snapshot Manager, ensure that you have upgraded your Snapshot Manager version to Update 2 prior to updating the device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-the-azure-classic-portal"></a><span data-ttu-id="be92e-119">Azure 클래식 포털을 통해 업데이트 3 설치</span><span class="sxs-lookup"><span data-stu-id="be92e-119">Install Update 3 via the Azure classic portal</span></span>
<span data-ttu-id="be92e-120">다음 단계를 수행하여 장치를 [업데이트 3](storsimple-update3-release-notes.md)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-120">Perform the following steps to update your device to [Update 3](storsimple-update3-release-notes.md).</span></span>

> [!NOTE]
> <span data-ttu-id="be92e-121">업데이트 2 이상(업데이트 2.1 포함)을 적용하는 경우 Microsoft가 장치에서 추가 진단 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-121">If you are applying Update 2 or later (including Update 2.1), Microsoft will be able to pull additional diagnostic information from the device.</span></span> <span data-ttu-id="be92e-122">따라서 운영 팀에서 문제가 있는 장치를 확인하는 경우, 장치로부터 정보를 수집하고 문제를 진단할 준비가 더욱 잘 갖추어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-122">As a result, when our operations team identifies devices that are having problems, we are better equipped to collect information from the device and diagnose issues.</span></span> <span data-ttu-id="be92e-123">업데이트 2 이상을 수락하면, 이러한 주도적 지원을 제공해도 된다고 허락하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-123">By accepting Update 2 or later, you allow us to provide this proactive support.</span></span>
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

<span data-ttu-id="be92e-124">장치가 **StorSimple 8000 시리즈 업데이트 3(6.3.9600.17759)**를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-124">Verify that your device is running **StorSimple 8000 Series Update 3 (6.3.9600.17759)**.</span></span> <span data-ttu-id="be92e-125">**마지막 업데이트 날짜** 도 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-125">The **Last updated date** should also be modified.</span></span> 
   - <span data-ttu-id="be92e-126">업데이트 2 이전 버전에서 업데이트하는 경우 유지 관리 모드 업데이트가 사용 가능하다고도 표시됩니다(이 메시지는 업데이트를 설치한 후 최대 24시간 동안 계속 표시될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="be92e-126">If you are updating from a version prior to Update 2, you will also see that the Maintenance mode updates are available (this message might continue to be displayed for up to 24 hours after you install the updates).</span></span>
     <span data-ttu-id="be92e-127">유지 관리 모드 업데이트는 작업 중단 업데이트이므로 장치 가동 중지 시간이 발생할 수 있으며, 장치의 Windows PowerShell 인터페이스를 통해서만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-127">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via the Windows PowerShell interface of your device.</span></span> <span data-ttu-id="be92e-128">일부 경우에 업데이트 1.2를 실행할 때 디스크 펌웨어가 이미 최신 버전일 수 있습니다. 이 경우 모든 유지 관리 모드 업데이트를 설치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-128">In some cases when you are running Update 1.2, your disk firmware might already be up-to-date, in which case you don't need to install any maintenance mode updates.</span></span>
   - <span data-ttu-id="be92e-129">업데이트 2 이상에서 업데이트하는 경우 이제 장치가 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-129">If you are updating from Update 2 or later, your device should now be up-to-date.</span></span> <span data-ttu-id="be92e-130">다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-130">You can skip the next step.</span></span>

<span data-ttu-id="be92e-131">[핫픽스를 다운로드하려면](#to-download-hotfixes)에 나열된 단계를 사용하여 유지 관리 모드 업데이트를 다운로드한 후 KB3121899를 검색한 후 다운로드합니다. 이 KB는 디스크 펌웨어 업데이트를 설치합니다(다른 업데이트가 이미 설치되어 있어야 함).</span><span class="sxs-lookup"><span data-stu-id="be92e-131">Download the maintenance mode updates by using the steps listed in [to download hotfixes](#to-download-hotfixes) to search for and download KB3121899, which installs disk firmware updates (the other updates should already be installed by now).</span></span> <span data-ttu-id="be92e-132">[유지 관리 모드 핫픽스 설치 및 확인](#to-install-and-verify-maintenance-mode-hotfixes) 에 나열된 단계를 따라 유지 관리 모드 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-132">Follow the steps listed in [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) to install the maintenance mode updates.</span></span> 

## <a name="install-update-3-as-a-hotfix"></a><span data-ttu-id="be92e-133">핫픽스로 업데이트 3 설치</span><span class="sxs-lookup"><span data-stu-id="be92e-133">Install Update 3 as a hotfix</span></span>
<span data-ttu-id="be92e-134">Azure 클래식 포털을 통해 업데이트를 설치하려고 할 때 게이트웨이 검사에 실패하는 경우 이 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-134">Use this procedure if you fail the gateway check when trying to install the updates through the Azure classic portal.</span></span> <span data-ttu-id="be92e-135">비데이터 0 네트워크 인터페이스에 할당된 게이트웨이가 있고 장치가 업데이트 1 이전의 소프트웨어 버전을 실행하는 경우 확인이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-135">The check fails as you have a gateway assigned to a non-DATA 0 network interface and your device is running a software version prior to Update 1.</span></span>

<span data-ttu-id="be92e-136">핫픽스 방법을 사용하여 업그레이드할 수 있는 소프트웨어 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-136">The software versions that can be upgraded using the hotfix method are:</span></span>

* <span data-ttu-id="be92e-137">업데이트 0.1, 0.2, 0.3</span><span class="sxs-lookup"><span data-stu-id="be92e-137">Update 0.1, 0.2, 0.3</span></span>
* <span data-ttu-id="be92e-138">업데이트 1, 1.1, 1.2</span><span class="sxs-lookup"><span data-stu-id="be92e-138">Update 1, 1.1, 1.2</span></span>
* <span data-ttu-id="be92e-139">업데이트 2, 2.1, 2.2</span><span class="sxs-lookup"><span data-stu-id="be92e-139">Update 2, 2.1, 2.2</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="be92e-140">장치가 릴리스(GA) 버전을 실행하는 경우 이 업데이트 설치를 위한 지원을 받으려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="be92e-140">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) to assist you with the update.</span></span>
> 
> 

<span data-ttu-id="be92e-141">핫픽스 메서드에는 다음 세 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-141">The hotfix method involves the following three steps:</span></span>

1. <span data-ttu-id="be92e-142">Microsoft Update 카탈로그에서 핫픽스를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-142">Download the hotfixes from the Microsoft Update Catalog.</span></span>
2. <span data-ttu-id="be92e-143">일반 모드 핫픽스를 설치 및 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-143">Install and verify the regular mode hotfixes.</span></span>
3. <span data-ttu-id="be92e-144">유지 관리 모드 핫픽스를 설치 및 확인합니다(업데이트 2 이전 소프트웨어에서 업데이트하는 경우에만).</span><span class="sxs-lookup"><span data-stu-id="be92e-144">Install and verify the maintenance mode hotfix (only when updating from pre-Update 2 software).</span></span>

#### <a name="download-updates-for-your-device"></a><span data-ttu-id="be92e-145">장치에 대한 업데이트 다운로드</span><span class="sxs-lookup"><span data-stu-id="be92e-145">Download updates for your device</span></span>
<span data-ttu-id="be92e-146">**장치에서 업데이트 2.1 또는 2.2를 실행 중**인 경우 다음 핫픽스를 사전 설정된 순서대로 다운로드하고 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-146">**If your device is running Update 2.1 or 2.2**, you must download and install the following hotfixes in the prescribed order:</span></span>

| <span data-ttu-id="be92e-147">순서</span><span class="sxs-lookup"><span data-stu-id="be92e-147">Order</span></span> | <span data-ttu-id="be92e-148">KB</span><span class="sxs-lookup"><span data-stu-id="be92e-148">KB</span></span> | <span data-ttu-id="be92e-149">설명</span><span class="sxs-lookup"><span data-stu-id="be92e-149">Description</span></span> | <span data-ttu-id="be92e-150">업데이트 유형</span><span class="sxs-lookup"><span data-stu-id="be92e-150">Update type</span></span> | <span data-ttu-id="be92e-151">설치 시간</span><span class="sxs-lookup"><span data-stu-id="be92e-151">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="be92e-152">1.</span><span class="sxs-lookup"><span data-stu-id="be92e-152">1.</span></span> |<span data-ttu-id="be92e-153">KB3186843</span><span class="sxs-lookup"><span data-stu-id="be92e-153">KB3186843</span></span> |<span data-ttu-id="be92e-154">소프트웨어 업데이트 &#42;</span><span class="sxs-lookup"><span data-stu-id="be92e-154">Software update &#42;</span></span> |<span data-ttu-id="be92e-155">일반 </span><span class="sxs-lookup"><span data-stu-id="be92e-155">Regular</span></span> <br></br><span data-ttu-id="be92e-156">중단 없음</span><span class="sxs-lookup"><span data-stu-id="be92e-156">Non-disruptive</span></span> |<span data-ttu-id="be92e-157">~ 45분</span><span class="sxs-lookup"><span data-stu-id="be92e-157">~ 45 mins</span></span> |
| <span data-ttu-id="be92e-158">2.</span><span class="sxs-lookup"><span data-stu-id="be92e-158">2.</span></span> |<span data-ttu-id="be92e-159">KB3186859</span><span class="sxs-lookup"><span data-stu-id="be92e-159">KB3186859</span></span> |<span data-ttu-id="be92e-160">LSI 드라이버 및 펌웨어</span><span class="sxs-lookup"><span data-stu-id="be92e-160">LSI driver and firmware</span></span> |<span data-ttu-id="be92e-161">일반</span><span class="sxs-lookup"><span data-stu-id="be92e-161">Regular</span></span> <br></br><span data-ttu-id="be92e-162">중단 없음</span><span class="sxs-lookup"><span data-stu-id="be92e-162">Non-disruptive</span></span> |<span data-ttu-id="be92e-163">~ 20분</span><span class="sxs-lookup"><span data-stu-id="be92e-163">~ 20 mins</span></span> |
| <span data-ttu-id="be92e-164">3.</span><span class="sxs-lookup"><span data-stu-id="be92e-164">3.</span></span> |<span data-ttu-id="be92e-165">KB3121261</span><span class="sxs-lookup"><span data-stu-id="be92e-165">KB3121261</span></span> |<span data-ttu-id="be92e-166">Storport 및 Spaceport 픽스 </span><span class="sxs-lookup"><span data-stu-id="be92e-166">Storport and Spaceport fix</span></span> </br> <span data-ttu-id="be92e-167">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="be92e-167">Windows Server 2012 R2</span></span> |<span data-ttu-id="be92e-168">일반</span><span class="sxs-lookup"><span data-stu-id="be92e-168">Regular</span></span> <br></br><span data-ttu-id="be92e-169">중단 없음</span><span class="sxs-lookup"><span data-stu-id="be92e-169">Non-disruptive</span></span> |<span data-ttu-id="be92e-170">~ 20분</span><span class="sxs-lookup"><span data-stu-id="be92e-170">~ 20 mins</span></span> |

<span data-ttu-id="be92e-171">&#42; *소프트웨어 업데이트는 `all-hcsmdssoftwareupdate`가 붙은 장치 소프트웨어 업데이트 및 `all-cismdsagentupdatebundle`이 붙은 Cis 및 Mds 에이전트와 같은 두 개의 이진 파일로 구성되어 있음에 유의하세요. 장치 소프트웨어 업데이트는 Cis 및 Mds 에이전트 전에 설치해야 합니다. 또한 Cis 및 Mds 에이전트 업데이트를 적용한 후, 나머지 업데이트를 적용하기 전에 `Restart-HcsController` cmdlet을 통해 활성 컨트롤러를 다시 시작해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="be92e-171">&#42;  *Note that the software update consists of two binary files: device software update prefaced with `all-hcsmdssoftwareupdate` and the Cis and Mds agent prefaced with `all-cismdsagentupdatebundle`. The device software update must be installed before the Cis and Mds agent. You must also restart the active controller via the `Restart-HcsController` cmdlet after you apply the Cis and Mds agent update (and before applying the remaining updates).*</span></span> 

<span data-ttu-id="be92e-172">**장치에서 업데이트 0.1, 0.2, 0.3, 1.0, 1.1, 1.2 또는 2.0을 실행 중**인 경우 해당 소프트웨어, LSI 드라이버 및 펌웨어 업데이트(앞의 표에 나와 있음) 외에도 다음 핫픽스를 사전 설정된 순서대로 다운로드하여 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-172">**If your device is running Update 0.1, 0.2, 0.3, 1.0, 1.1, 1.2, or 2.0**, you must download and install the following hotfixes in addition to the software, LSI driver and firmware updates (shown in the preceding table), in the prescribed order:</span></span>

| <span data-ttu-id="be92e-173">순서</span><span class="sxs-lookup"><span data-stu-id="be92e-173">Order</span></span> | <span data-ttu-id="be92e-174">KB</span><span class="sxs-lookup"><span data-stu-id="be92e-174">KB</span></span> | <span data-ttu-id="be92e-175">설명</span><span class="sxs-lookup"><span data-stu-id="be92e-175">Description</span></span> | <span data-ttu-id="be92e-176">업데이트 유형</span><span class="sxs-lookup"><span data-stu-id="be92e-176">Update type</span></span> | <span data-ttu-id="be92e-177">설치 시간</span><span class="sxs-lookup"><span data-stu-id="be92e-177">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="be92e-178">4.</span><span class="sxs-lookup"><span data-stu-id="be92e-178">4.</span></span> |<span data-ttu-id="be92e-179">KB3146621</span><span class="sxs-lookup"><span data-stu-id="be92e-179">KB3146621</span></span> |<span data-ttu-id="be92e-180">iSCSI 패키지</span><span class="sxs-lookup"><span data-stu-id="be92e-180">iSCSI package</span></span> |<span data-ttu-id="be92e-181">일반</span><span class="sxs-lookup"><span data-stu-id="be92e-181">Regular</span></span> <br></br><span data-ttu-id="be92e-182">중단 없음</span><span class="sxs-lookup"><span data-stu-id="be92e-182">Non-disruptive</span></span> |<span data-ttu-id="be92e-183">~ 20분</span><span class="sxs-lookup"><span data-stu-id="be92e-183">~ 20 mins</span></span> |
| <span data-ttu-id="be92e-184">5.</span><span class="sxs-lookup"><span data-stu-id="be92e-184">5.</span></span> |<span data-ttu-id="be92e-185">KB3103616</span><span class="sxs-lookup"><span data-stu-id="be92e-185">KB3103616</span></span> |<span data-ttu-id="be92e-186">WMI 패키지</span><span class="sxs-lookup"><span data-stu-id="be92e-186">WMI package</span></span> |<span data-ttu-id="be92e-187">일반</span><span class="sxs-lookup"><span data-stu-id="be92e-187">Regular</span></span> <br></br><span data-ttu-id="be92e-188">중단 없음</span><span class="sxs-lookup"><span data-stu-id="be92e-188">Non-disruptive</span></span> |<span data-ttu-id="be92e-189">~ 12분</span><span class="sxs-lookup"><span data-stu-id="be92e-189">~ 12 mins</span></span> |

<br></br>

<span data-ttu-id="be92e-190">**장치에서 버전 0.2, 0.3, 1.0, 1.1 및 1.2를 실행 중**인 경우 앞의 표에 나와 있는 모든 업데이트 맨 위에 디스크 펌웨어 업데이트를 설치해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-190">**If your device is running versions 0.2, 0.3, 1.0, 1.1, and 1.2**, you may also need to install disk firmware updates on top of all the updates shown in the preceding tables.</span></span> <span data-ttu-id="be92e-191">`Get-HcsFirmwareVersion` cmdlet을 실행하여 디스크 펌웨어 업데이트가 필요한지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-191">You can verify whether you need the disk firmware updates by running the `Get-HcsFirmwareVersion` cmdlet.</span></span> <span data-ttu-id="be92e-192">펌웨어 버전 `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`을 실행하는 경우 이러한 업데이트를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-192">If you are running these firmware versions: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, then you do not need to install these updates.</span></span>

| <span data-ttu-id="be92e-193">순서</span><span class="sxs-lookup"><span data-stu-id="be92e-193">Order</span></span> | <span data-ttu-id="be92e-194">KB</span><span class="sxs-lookup"><span data-stu-id="be92e-194">KB</span></span> | <span data-ttu-id="be92e-195">설명</span><span class="sxs-lookup"><span data-stu-id="be92e-195">Description</span></span> | <span data-ttu-id="be92e-196">업데이트 유형</span><span class="sxs-lookup"><span data-stu-id="be92e-196">Update type</span></span> | <span data-ttu-id="be92e-197">설치 시간</span><span class="sxs-lookup"><span data-stu-id="be92e-197">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="be92e-198">6.</span><span class="sxs-lookup"><span data-stu-id="be92e-198">6.</span></span> |<span data-ttu-id="be92e-199">KB3121899</span><span class="sxs-lookup"><span data-stu-id="be92e-199">KB3121899</span></span> |<span data-ttu-id="be92e-200">디스크 펌웨어</span><span class="sxs-lookup"><span data-stu-id="be92e-200">Disk firmware</span></span> |<span data-ttu-id="be92e-201">유지 관리</span><span class="sxs-lookup"><span data-stu-id="be92e-201">Maintenance</span></span> <br></br><span data-ttu-id="be92e-202">중단</span><span class="sxs-lookup"><span data-stu-id="be92e-202">Disruptive</span></span> |<span data-ttu-id="be92e-203">~ 30분</span><span class="sxs-lookup"><span data-stu-id="be92e-203">~ 30 mins</span></span> |

<br></br>

> [!IMPORTANT]
> * <span data-ttu-id="be92e-204">이 절차는 업데이트 3에만 적용하도록 한 번만 수행해야 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-204">This procedure needs to be performed only once to apply Update 3.</span></span> <span data-ttu-id="be92e-205">Azure 클래식 포털을 사용하여 후속 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-205">You can use the Azure classic portal to apply subsequent updates.</span></span>
> * <span data-ttu-id="be92e-206">업데이트 2.2에서 업데이트하는 경우 전체 설치 시간은 1.1시간에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-206">If updating from Update 2.2, the total install time is close to 1.1 hours.</span></span>
> * <span data-ttu-id="be92e-207">이 절차에 따라 업데이트를 적용하기 전에 두 장치 컨트롤러가 온라인 상태이고 모든 하드웨어 구성 요소가 정상 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-207">Before using this procedure to apply the update, make sure that both the device controllers are online and all the hardware components are healthy.</span></span>
> 
> 

<span data-ttu-id="be92e-208">다음 단계에 따라 핫픽스를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-208">Perform the following steps to download and install the hotfixes.</span></span>

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="be92e-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be92e-209">Next steps</span></span>
<span data-ttu-id="be92e-210">[업데이트 3 릴리스](storsimple-update3-release-notes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="be92e-210">Learn more about the [Update 3 release](storsimple-update3-release-notes.md).</span></span>

