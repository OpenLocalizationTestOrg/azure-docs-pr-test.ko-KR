---
title: "StorSimple 8000 시리즈 업데이트 5 릴리스 정보 | Microsoft Docs"
description: "StorSimple 8000 시리즈 업데이트 5의 새로운 기능, 문제 및 해결 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: e68dce72d648171faab930bbb4af9fd61816b19b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a><span data-ttu-id="ceee1-103">StorSimple 8000 시리즈 업데이트 5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="ceee1-103">StorSimple 8000 Series Update 5 release notes</span></span>

## <a name="overview"></a><span data-ttu-id="ceee1-104">개요</span><span class="sxs-lookup"><span data-stu-id="ceee1-104">Overview</span></span>

<span data-ttu-id="ceee1-105">다음 릴리스 정보는 새로운 기능에 대해 설명하고 StorSimple 8000 시리즈 업데이트 5에 대한 중요한 미해결 문제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-105">The following release notes describe the new features and identify the critical open issues for StorSimple 8000 Series Update 5.</span></span> <span data-ttu-id="ceee1-106">또한 이 릴리스에 포함된 StorSimple 소프트웨어 업데이트 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-106">They also contain a list of the StorSimple software updates included in this release.</span></span>

<span data-ttu-id="ceee1-107">업데이트 5는 업데이트 0.1~업데이트 4를 실행하는 모든 StorSimple 장치에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-107">Update 5 can be applied to any StorSimple device running Update 0.1 through Update 4.</span></span> <span data-ttu-id="ceee1-108">업데이트 5에 연결된 장치 버전은 6.3.9600.17845입니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-108">The device version associated with Update 5 is 6.3.9600.17845.</span></span>

<span data-ttu-id="ceee1-109">StorSimple 솔루션에 업데이트를 배포하기 전에 릴리스 정보에 포함된 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="ceee1-109">Review the information contained in the release notes before you deploy the update in your StorSimple solution.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="ceee1-110">업데이트 5에는 장치 소프트웨어, 디스크 펌웨어, OS 보안 및 기타 OS 업데이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-110">Update 5 has device software, disk firmware, OS security, and other OS updates.</span></span> <span data-ttu-id="ceee1-111">이 업데이트를 설치하는 데는 4시간 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-111">It takes approximately 4 hours to install this update.</span></span> <span data-ttu-id="ceee1-112">디스크 펌웨어 업데이트는 중단 업데이트이며 사용자 장치에 대한 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-112">Disk firmware update is a disruptive update and results in a downtime for your device.</span></span> <span data-ttu-id="ceee1-113">장치를 최신 상태로 유지하려면 업데이트 5를 적용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-113">We recommend that you apply Update 5 to keep your device up-to-date.</span></span>
> * <span data-ttu-id="ceee1-114">새 릴리스의 경우, 업데이트의 단계적 롤아웃을 수행하기 때문에 즉시 업데이트를 볼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-114">For new releases, you may not see updates immediately because we do a phased rollout of the updates.</span></span> <span data-ttu-id="ceee1-115">이러한 업데이트가 곧 제공될 예정이니 몇 일 후에 업데이트를 다시 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="ceee1-115">Wait a few days, and then scan for updates again as these updates will become available soon.</span></span>

## <a name="whats-new-in-update-5"></a><span data-ttu-id="ceee1-116">업데이트 5의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="ceee1-116">What's new in Update 5</span></span>

<span data-ttu-id="ceee1-117">업데이트 5에는 다음과 같은 주요 향상 기능 및 버그 수정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-117">The following key improvements and bug fixes have been made in Update 5.</span></span>

* <span data-ttu-id="ceee1-118">**AAD(Azure Active Directory)를 사용하여 StorSimple Device Manager 서비스에서 인증 받기** – 업데이트 5부터 StorSimple Device Manager 서비스에서 인증을 받는 데 Azure Active Directory가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-118">**Use of Azure Active Directory (AAD) to authenticate with StorSimple Device Manager service** – From Update 5 onwards, Azure Active Directory is used to authenticate with the StorSimple Device Manager service.</span></span> <span data-ttu-id="ceee1-119">기존 인증 메커니즘은 2017년 12월부터 지원이 중지될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-119">The old authentication mechanism will be deprecated by December 2017.</span></span> <span data-ttu-id="ceee1-120">모든 사용자는 방화벽 규칙에 새 인증 URL을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-120">All the users must include the new authentication URLs in their firewall rules.</span></span> <span data-ttu-id="ceee1-121">자세한 내용은 [StorSimple 장치에 대한 네트워킹 요구 사항에 나열된 인증 URL](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="ceee1-121">For more information, go to [authentication URLs listed in the networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).</span></span>

    <span data-ttu-id="ceee1-122">인증 URL이 방화벽 규칙에 포함되지 않은 경우 StorSimple 장치가 서비스에서 인증을 받을 수 없다는 중요한 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-122">If the authentication URL is not included in the firewall rules, the users will see a critical alert that their StorSimple device could not authenticate with the service.</span></span> <span data-ttu-id="ceee1-123">이 경고가 표시되면 새 인증 URL을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-123">If the users see this alert, they need to include the new authentication URL.</span></span> <span data-ttu-id="ceee1-124">자세한 내용은 [StorSimple 네트워킹 경고](storsimple-8000-manage-alerts.md#networking-alerts)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-124">For more information, go to [StorSimple networking alerts](storsimple-8000-manage-alerts.md#networking-alerts).</span></span>

* <span data-ttu-id="ceee1-125">**새 버전의 StorSimple Snapshot Manager** - 새 버전의 StorSimple Snapshot Manager가 업데이트 5와 함께 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-125">**New version of StorSimple Snapshot Manager** - A new version of StorSimple Snapshot Manager is released with Update 5.</span></span> <span data-ttu-id="ceee1-126">이 버전으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-126">We recommend that you update to this version.</span></span> <span data-ttu-id="ceee1-127">이 버전은 업데이트 3 이상을 실행하는 모든 StorSimple 장치와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-127">This version is compatible with all the StorSimple devices that are running Update 3 or later.</span></span> <span data-ttu-id="ceee1-128">자세한 내용은 [StorSimple Snapshot Manager 배포](storsimple-snapshot-manager-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceee1-128">For more information, go to [deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>


## <a name="issues-fixed-in-update-5"></a><span data-ttu-id="ceee1-129">업데이트 5에서 해결된 문제</span><span class="sxs-lookup"><span data-stu-id="ceee1-129">Issues fixed in Update 5</span></span>

<span data-ttu-id="ceee1-130">다음 표에는 업데이트 5에서 해결된 문제가 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-130">The following table provides a summary of issues that were fixed in Update 5.</span></span>

| <span data-ttu-id="ceee1-131">아니요</span><span class="sxs-lookup"><span data-stu-id="ceee1-131">No</span></span> | <span data-ttu-id="ceee1-132">기능</span><span class="sxs-lookup"><span data-stu-id="ceee1-132">Feature</span></span> | <span data-ttu-id="ceee1-133">문제</span><span class="sxs-lookup"><span data-stu-id="ceee1-133">Issue</span></span> | <span data-ttu-id="ceee1-134">실제 장치에 적용</span><span class="sxs-lookup"><span data-stu-id="ceee1-134">Applies to physical device</span></span> | <span data-ttu-id="ceee1-135">가상 장치에 적용</span><span class="sxs-lookup"><span data-stu-id="ceee1-135">Applies to virtual device</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ceee1-136">1</span><span class="sxs-lookup"><span data-stu-id="ceee1-136">1</span></span> |<span data-ttu-id="ceee1-137">Windows PowerShell 원격 기능</span><span class="sxs-lookup"><span data-stu-id="ceee1-137">Windows PowerShell remoting</span></span> |<span data-ttu-id="ceee1-138">이전 릴리스에서는 Windows PowerShell을 통해 StorSimple Cloud Appliance에 대해 원격 연결을 설정하는 동안 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-138">In the previous release, a user would receive an error while trying to establish a remote connection to the StorSimple Cloud Appliance via Windows PowerShell.</span></span> <span data-ttu-id="ceee1-139">이 문제는 근본 원인이 파악되었고 이 릴리스에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-139">This issue was root-caused and fixed in this release.</span></span> |<span data-ttu-id="ceee1-140">아니요</span><span class="sxs-lookup"><span data-stu-id="ceee1-140">No</span></span> |<span data-ttu-id="ceee1-141">예</span><span class="sxs-lookup"><span data-stu-id="ceee1-141">Yes</span></span> |
| <span data-ttu-id="ceee1-142">2</span><span class="sxs-lookup"><span data-stu-id="ceee1-142">2</span></span> |<span data-ttu-id="ceee1-143">대역폭 템플릿</span><span class="sxs-lookup"><span data-stu-id="ceee1-143">Bandwidth templates</span></span> |<span data-ttu-id="ceee1-144">이전 릴리스에서는 대역폭 템플릿에 문제가 있어서 장치가 구성된 것보다 더 낮은 대역폭을 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-144">In earlier release, there was an issue with bandwidth templates that resulted in lower bandwidth than what the device was configured for.</span></span> <span data-ttu-id="ceee1-145">이 문제는 이 릴리스에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-145">This issue is resolved in this release.</span></span> |<span data-ttu-id="ceee1-146">예</span><span class="sxs-lookup"><span data-stu-id="ceee1-146">Yes</span></span> |<span data-ttu-id="ceee1-147">예</span><span class="sxs-lookup"><span data-stu-id="ceee1-147">Yes</span></span> |
| <span data-ttu-id="ceee1-148">3</span><span class="sxs-lookup"><span data-stu-id="ceee1-148">3</span></span> |<span data-ttu-id="ceee1-149">장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="ceee1-149">Failover</span></span> |<span data-ttu-id="ceee1-150">이전 릴리스에서는 대량의 볼륨이 있는 장치가 업데이트 4를 실행하는 다른 장치로 장애 조치(failover)되면 액세스 제어 레코드를 적용하려고 할 때 프로세스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-150">In previous release, when a device with a large number of volumes was failed over to another device running Update 4, the process would fail when trying to apply the access control records.</span></span> <span data-ttu-id="ceee1-151">이 문제는 이 릴리스에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-151">This issue is fixed in this release.</span></span> |<span data-ttu-id="ceee1-152">예</span><span class="sxs-lookup"><span data-stu-id="ceee1-152">Yes</span></span> |<span data-ttu-id="ceee1-153">예</span><span class="sxs-lookup"><span data-stu-id="ceee1-153">Yes</span></span> |



## <a name="known-issues-in-update-5-from-previous-releases"></a><span data-ttu-id="ceee1-154">업데이트 5의 알려진 이전 릴리스 문제</span><span class="sxs-lookup"><span data-stu-id="ceee1-154">Known issues in Update 5 from previous releases</span></span>

<span data-ttu-id="ceee1-155">업데이트 5에 알려진 새로운 문제는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-155">There are no new known issues in Update 5.</span></span> <span data-ttu-id="ceee1-156">이전 릴리스에서 업데이트 5로 이어지는 문제 목록은 [업데이트 3 릴리스 정보](storsimple-update3-release-notes.md#known-issues-in-update-3)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-156">For a list of issues carried over to Update 5 from previous releases, go to [Update 3 release notes](storsimple-update3-release-notes.md#known-issues-in-update-3).</span></span>

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a><span data-ttu-id="ceee1-157">업데이트 5의 SAS(Serial attached SCSI) 컨트롤러 및 펌웨어 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceee1-157">Serial-attached SCSI (SAS) controller and firmware updates in Update 5</span></span>

<span data-ttu-id="ceee1-158">이 릴리스에는 SAS 컨트롤러, LSI 드라이버 및 펌웨어 업데이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-158">This release has SAS controller and LSI driver and firmware updates.</span></span> <span data-ttu-id="ceee1-159">이러한 업데이트를 설치하는 방법에 대한 자세한 내용은 StorSimple 장치의 [업데이트 5 설치](storsimple-8000-install-update-5.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceee1-159">For more information on how to install these updates, see [install Update 5](storsimple-8000-install-update-5.md) on your StorSimple device.</span></span>

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a><span data-ttu-id="ceee1-160">업데이트 5의 StorSimple Cloud Appliance 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceee1-160">StorSimple Cloud Appliance updates in Update 5</span></span>

<span data-ttu-id="ceee1-161">이 업데이트는 StorSimple 클라우드 어플라이언스에 적용할 수 없습니다(가상 장치라고도 함).</span><span class="sxs-lookup"><span data-stu-id="ceee1-161">This update cannot be applied to the StorSimple Cloud Appliance (also known as the virtual device).</span></span> <span data-ttu-id="ceee1-162">새 클라우드 어플라이언스는 업데이트 5 이미지를 사용하여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-162">New cloud appliances need to be created using the Update 5 image.</span></span> <span data-ttu-id="ceee1-163">StorSimple Cloud Appliance를 만드는 방법에 대한 자세한 내용은 [StorSimple Cloud Appliance 배포 및 관리](storsimple-8000-cloud-appliance-u2.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-163">For information on how to create a StorSimple Cloud Appliance, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="ceee1-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ceee1-164">Next step</span></span>

<span data-ttu-id="ceee1-165">StorSimple 장치에 [업데이트 5를 설치](storsimple-8000-install-update-5.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ceee1-165">Learn how to [install Update 5](storsimple-8000-install-update-5.md) on your StorSimple device.</span></span>

