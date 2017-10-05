---
title: "StorSimple 장치에 업데이트 1.2 설치 | Microsoft Docs"
description: "StorSimple 8000 시리즈 장치에서 StorSimple 8000 시리즈 업데이트 1.2를 설치하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 80ff35cc47dfc38089f4c392ef4c90baf9ccc03e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a><span data-ttu-id="59bda-103">StorSimple 8000 시리즈 장치에 업데이트 1.2 설치</span><span class="sxs-lookup"><span data-stu-id="59bda-103">Install Update 1.2 on your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="59bda-104">개요</span><span class="sxs-lookup"><span data-stu-id="59bda-104">Overview</span></span>
<span data-ttu-id="59bda-105">이 자습서에서는 업데이트 1 이전 소프트웨어 버전을 실행하는 StorSimple 장치에 업데이트 1.2를 설치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-105">This tutorial explains how to install Update 1.2 on a StorSimple device that is running a software version prior to Update 1.</span></span> <span data-ttu-id="59bda-106">또한 이 자습서는 StorSimple 장치의 DATA 0 이외의 다른 네트워크 인터페이스에서 게이트웨이를 구성하는 경우 업데이트에 필요한 추가 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-106">The tutorial also covers the additional steps required for the update when a gateway is configured on a network interface other than DATA 0 of the StorSimple device.</span></span>

<span data-ttu-id="59bda-107">업데이트 1.2는 장치 소프트웨어 업데이트, LSI 드라이버 업데이트 및 디스크 펌웨어 업데이트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-107">Update 1.2 includes device software updates, LSI driver updates and disk firmware updates.</span></span> <span data-ttu-id="59bda-108">소프트웨어 및 LSI 드라이버 업데이트는 무중단 업데이트이며 Azure 클래식 포털을 통해 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-108">The software and LSI driver updates are non-disruptive updates and can be applied via the Azure classic portal.</span></span> <span data-ttu-id="59bda-109">디스크 펌웨어 업데이트는 작업 중단 업데이트이며 장치의 Windows PowerShell 인터페이스를 통해서만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-109">The disk firmware updates are disruptive updates and can only be applied via the Windows PowerShell interface of the device.</span></span>

<span data-ttu-id="59bda-110">장치가 실행되는 버전에 따라 업데이트 1.2를 적용할지 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-110">Depending upon which version your device is running, you can determine if Update 1.2 will be applied.</span></span> <span data-ttu-id="59bda-111">장치 **대시보드**의 **빠른 보기** 섹션으로 이동하여 장치의 소프트웨어 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-111">You can check the software version of your device by navigating to the **quick glance** section of your device **Dashboard**.</span></span>

</br>

| <span data-ttu-id="59bda-112">소프트웨어 버전을 실행하는 경우...</span><span class="sxs-lookup"><span data-stu-id="59bda-112">If running software version …</span></span> | <span data-ttu-id="59bda-113">포털에서 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="59bda-113">What happens in the portal?</span></span> |
| --- | --- |
| <span data-ttu-id="59bda-114">릴리스 - GA</span><span class="sxs-lookup"><span data-stu-id="59bda-114">Release - GA</span></span> |<span data-ttu-id="59bda-115">릴리스 버전(GA)을 실행하는 경우 이 업데이트를 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-115">If you are running Release version (GA), do not apply this update.</span></span> <span data-ttu-id="59bda-116">[Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 하여 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-116">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) to update your device.</span></span> |
| <span data-ttu-id="59bda-117">업데이트 0.1</span><span class="sxs-lookup"><span data-stu-id="59bda-117">Update 0.1</span></span> |<span data-ttu-id="59bda-118">포털은 업데이트 1.2를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-118">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="59bda-119">업데이트 0.2</span><span class="sxs-lookup"><span data-stu-id="59bda-119">Update 0.2</span></span> |<span data-ttu-id="59bda-120">포털은 업데이트 1.2를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-120">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="59bda-121">업데이트 0.3</span><span class="sxs-lookup"><span data-stu-id="59bda-121">Update 0.3</span></span> |<span data-ttu-id="59bda-122">포털은 업데이트 1.2를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-122">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="59bda-123">업데이트 1</span><span class="sxs-lookup"><span data-stu-id="59bda-123">Update 1</span></span> |<span data-ttu-id="59bda-124">이 업데이트는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-124">This update will not be available.</span></span> |
| <span data-ttu-id="59bda-125">업데이트 1.1</span><span class="sxs-lookup"><span data-stu-id="59bda-125">Update 1.1</span></span> |<span data-ttu-id="59bda-126">이 업데이트는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-126">This update will not be available.</span></span> |

</br>

> [!IMPORTANT]
> * <span data-ttu-id="59bda-127">업데이트의 단계적 롤아웃을 수행하기 때문에 즉시 업데이트 1.2를 볼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-127">You may not see Update 1.2 immediately because we do a phased rollout of the updates.</span></span> <span data-ttu-id="59bda-128">해당 업데이트를 곧 사용할 수 있게 되므로 몇 일 후에 업데이트를 스캔합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-128">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="59bda-129">이 업데이트는 일련의 수동 및 자동 전 검사를 포함하여 하드웨어 상태 및 네트워크 연결 측면에서 장치 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-129">This update includes a set of manual and automatic pre-checks to determine the device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="59bda-130">Azure 클래식 포털에서 업데이트를 적용하는 경우 이러한 사전 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-130">These pre-checks are performed only if you apply the updates from the Azure classic portal.</span></span>
> * <span data-ttu-id="59bda-131">Azure 클래식 포털을 통해 소프트웨어 및 드라이버 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-131">We recommend that you install the software and driver updates via the Azure classic portal.</span></span> <span data-ttu-id="59bda-132">포털에서 사전 업데이트 게이트웨이 검사가 실패한 경우 (업데이트를 설치하려면) 장치의 Windows PowerShell 인터페이스로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-132">You should only go to the Windows PowerShell interface of the device (to install updates) if the pre-update gateway check fails in the portal.</span></span> <span data-ttu-id="59bda-133">업데이트를 설치하는 데 5-10시간이 걸릴 수 있습니다.(Windows 업데이트 포함) 장치의 Windows PowerShell 인터페이스를 통해 유지 관리 모드 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-133">The updates may take 5-10 hours to install (including the Windows Updates).</span></span> <span data-ttu-id="59bda-134">유지 관리 모드 업데이트는 중단 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-134">The maintenance mode updates must be installed via the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="59bda-135">이는 장치에 중단 시간을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-135">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-the-azure-classic-portal"></a><span data-ttu-id="59bda-136">Azure 클래식 포털을 사용하여 업데이트 1.2 설치</span><span class="sxs-lookup"><span data-stu-id="59bda-136">Install Update 1.2 via the Azure classic portal</span></span>
<span data-ttu-id="59bda-137">다음 단계를 수행하여 장치를 [업데이트 1.2](storsimple-update1-release-notes.md)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-137">Perform the following steps to update your device to [Update 1.2](storsimple-update1-release-notes.md).</span></span> <span data-ttu-id="59bda-138">장치에서 데이터 0 네트워크 인터페이스에 구성된 게이트웨이가 있는 경우 이 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-138">Use this procedure only if you have a gateway configured on DATA 0 network interface on your device.</span></span>

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="59bda-139">장치가 **StorSimple 8000 시리즈 업데이트 1.2(6.3.9600.17584)**를 실행하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-139">Verify that your device is running **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**.</span></span> <span data-ttu-id="59bda-140">**마지막 업데이트 날짜** 도 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-140">The **Last updated date** should also be modified.</span></span> <span data-ttu-id="59bda-141">또한 유지 관리 모드 업데이트가 사용 가능하다고 표시됩니다(이 메시지는 업데이트를 설치한 후 최대 24시간 동안 계속 표시될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="59bda-141">You'll also see that Maintenance mode updates are available (this message might continue to be displayed for up to 24 hours after you install the updates).</span></span>
   
   <span data-ttu-id="59bda-142">유지 관리 모드 업데이트는 작업 중단 업데이트이므로 장치 가동 중지 시간이 발생할 수 있으며, 장치의 Windows PowerShell 인터페이스를 통해서만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-142">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via the Windows PowerShell interface of your device.</span></span>
   
   <span data-ttu-id="59bda-143">![유지 관리 페이지](./media/storsimple-install-update-1/InstallUpdate12_10M.png "유지 관리 페이지")</span><span class="sxs-lookup"><span data-stu-id="59bda-143">![Maintenance page](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Maintenance page")</span></span>
2. <span data-ttu-id="59bda-144">[핫픽스를 다운로드하려면](#to-download-hotfixes)에 나열된 단계를 사용하여 유지 관리 모드 업데이트를 다운로드한 후 KB3063416을 검색한 후 다운로드합니다. 이 KB는 디스크 펌웨어 업데이트를 설치합니다(다른 업데이트가 이미 설치되어 있어야 함).</span><span class="sxs-lookup"><span data-stu-id="59bda-144">Download the maintenance mode updates by using the steps listed in [To download hotfixes](#to-download-hotfixes) to search for and download KB3063416, which installs disk firmware updates (the other updates should already be installed by now).</span></span>
3. <span data-ttu-id="59bda-145">[유지 관리 모드 핫픽스 설치 및 확인](#to-install-and-verify-maintenance-mode-hotfixes) 에 나열된 단계를 따라 유지 관리 모드 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-145">Follow the steps listed in [Install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) to install the maintenance mode updates.</span></span>
4. <span data-ttu-id="59bda-146">Azure 클래식 포털에서 **유지 관리** 페이지로 이동한 후 페이지 아래쪽에서 **업데이트 검색**을 클릭하여 Windows 업데이트를 확인한 다음 **업데이트 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-146">In the Azure classic portal, navigate to the **Maintenance** page and at the bottom of the page, click **Scan Updates** to check for any Windows Updates and then click **Install Updates**.</span></span> <span data-ttu-id="59bda-147">모든 업데이트가 정상적으로 설치되면 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-147">You're finished after all of the updates are successfully installed.</span></span>

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a><span data-ttu-id="59bda-148">비데이터 0 네트워크 인터페이스에 구성된 게이트웨이가 있는 장치에 업데이트 1.2 설치</span><span class="sxs-lookup"><span data-stu-id="59bda-148">Install Update 1.2 on a device that has a gateway configured for a non-DATA 0 network interface</span></span>
<span data-ttu-id="59bda-149">Azure 클래식 포털을 통해 업데이트를 설치하려고 할 때 게이트웨이 검사에 실패하는 경우 이 절차를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-149">You should use this procedure only if you fail the gateway check when trying to install the updates through the Azure classic portal.</span></span> <span data-ttu-id="59bda-150">비데이터 0 네트워크 인터페이스에 할당된 게이트웨이가 있고 장치가 업데이트 1 이전의 소프트웨어 버전을 실행하는 경우 확인이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-150">The check fails as you have a gateway assigned to a non-DATA 0 network interface and your device is running a software version prior to Update 1.</span></span> <span data-ttu-id="59bda-151">장치에 비데이터 0 네트워크 인터페이스에 대한 게이트웨이가 없는 경우, Azure 클래식 포털에서 직접 장치를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-151">If your device does not have a gateway on a non-DATA 0 network interface, you can update your device directly from the Azure classic portal.</span></span> <span data-ttu-id="59bda-152">[Azure 클래식 포털을 사용하여 업데이트 1.2 설치](#install-update-1.2-via-the-azure-classic-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59bda-152">See [Install update 1.2 via the Azure classic portal](#install-update-1.2-via-the-azure-classic-portal).</span></span>

<span data-ttu-id="59bda-153">이 메서드를 사용하여 업그레이드할 수 있는 소프트웨어 버전 업데이트 0.1, 0.2 및 0.3 도 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-153">The software versions that can be upgraded using this method are Update 0.1, Update 0.2, and Update 0.3.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="59bda-154">장치가 릴리스(GA) 버전을 실행하는 경우 이 업데이트 설치를 위한 지원을 받으려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="59bda-154">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) to assist you with the update.</span></span>
> * <span data-ttu-id="59bda-155">이 절차는 업데이트 1.2에만 적용하도록 한 번만 수행해야 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-155">This procedure needs to be performed only once to apply Update 1.2.</span></span> <span data-ttu-id="59bda-156">Azure 클래식 포털을 사용하여 후속 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-156">You can use the Azure classic portal to apply subsequent updates.</span></span>
> 
> 

<span data-ttu-id="59bda-157">장치가 업데이트 1 이전 소프트웨어를 실행하고 데이터 0 이외의 다른 네트워크 인터페이스에 대해 게이트웨이가 설정된 경우, 다음 두 가지 방법으로 업데이트 1.2를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-157">If your device is running pre-Update 1 software and it has a gateway set for a network interface other than DATA 0, you can apply Update 1.2 in the following two ways:</span></span>

* <span data-ttu-id="59bda-158">**옵션 1**: 업데이트를 다운로드하고 장치의 Windows PowerShell 인터페이스에서 `Start-HcsHotfix` cmdlet를 사용하여 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-158">**Option 1**: Download the update and apply it by using the `Start-HcsHotfix` cmdlet from the Windows PowerShell interface of the device.</span></span> <span data-ttu-id="59bda-159">이것이 권장된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-159">This is the recommended method.</span></span> <span data-ttu-id="59bda-160">**장치가 업데이트 1.0 또는 1.1 업데이트를 실행 중인 경우 이 메서드를 사용하여 업데이트 1.2를 적용하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="59bda-160">**Do not use this method to apply Update 1.2 if your device is running Update 1.0 or Update 1.1.**</span></span>
* <span data-ttu-id="59bda-161">**옵션 2**: 게이트웨이 구성을 제거하고 Azure 클래식 포털에서 직접 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-161">**Option 2**: Remove the gateway configuration and install the update directly from the Azure classic portal.</span></span>

<span data-ttu-id="59bda-162">각각에 대한 자세한 지침은 다음 섹션에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-162">Detailed instructions for each of these are provided in the following sections.</span></span>

## <a name="option-1-use-windows-powershell-for-storsimple-to-apply-update-12-as-a-hotfix"></a><span data-ttu-id="59bda-163">옵션 1: StorSimple용 Windows PowerShell을 사용하여 업데이트 1.2를 핫픽스로 적용</span><span class="sxs-lookup"><span data-stu-id="59bda-163">Option 1: Use Windows PowerShell for StorSimple to apply Update 1.2 as a hotfix</span></span>
<span data-ttu-id="59bda-164">업데이트 0.1, 0.2, 0.3을 실행하고 Azure 클래식 포털에서 업데이트를 설치할 때 게이트웨이 검사에 실패한 경우 이 절차를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-164">You should use this procedure only if you are running Update 0.1, 0.2, 0.3 and if your gateway check has failed when trying to install updates from the Azure classic portal.</span></span> <span data-ttu-id="59bda-165">릴리스(GA) 소프트웨어를 실행하는 경우 [Microsoft 지원](storsimple-contact-microsoft-support.md) 에 문의하여 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-165">If you are running Release (GA) software, please [Microsoft Support](storsimple-contact-microsoft-support.md) to update your device.</span></span>

<span data-ttu-id="59bda-166">업데이트 1.2를 핫픽스로 설치하려면 다음 핫픽스를 다운로드한 후 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-166">To install Update 1.2 as a hotfix, you must download and install the following hotfixes:</span></span>

| <span data-ttu-id="59bda-167">순서</span><span class="sxs-lookup"><span data-stu-id="59bda-167">Order</span></span> | <span data-ttu-id="59bda-168">KB</span><span class="sxs-lookup"><span data-stu-id="59bda-168">KB</span></span> | <span data-ttu-id="59bda-169">설명</span><span class="sxs-lookup"><span data-stu-id="59bda-169">Description</span></span> | <span data-ttu-id="59bda-170">업데이트 유형</span><span class="sxs-lookup"><span data-stu-id="59bda-170">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="59bda-171">1</span><span class="sxs-lookup"><span data-stu-id="59bda-171">1</span></span> |<span data-ttu-id="59bda-172">KB3063418</span><span class="sxs-lookup"><span data-stu-id="59bda-172">KB3063418</span></span> |<span data-ttu-id="59bda-173">소프트웨어 업데이트</span><span class="sxs-lookup"><span data-stu-id="59bda-173">Software update</span></span> |<span data-ttu-id="59bda-174">일반</span><span class="sxs-lookup"><span data-stu-id="59bda-174">Regular</span></span> |
| <span data-ttu-id="59bda-175">2</span><span class="sxs-lookup"><span data-stu-id="59bda-175">2</span></span> |<span data-ttu-id="59bda-176">KB3043005</span><span class="sxs-lookup"><span data-stu-id="59bda-176">KB3043005</span></span> |<span data-ttu-id="59bda-177">LSI SAS 컨트롤러 업데이트</span><span class="sxs-lookup"><span data-stu-id="59bda-177">LSI SAS controller update</span></span> |<span data-ttu-id="59bda-178">일반</span><span class="sxs-lookup"><span data-stu-id="59bda-178">Regular</span></span> |
| <span data-ttu-id="59bda-179">3</span><span class="sxs-lookup"><span data-stu-id="59bda-179">3</span></span> |<span data-ttu-id="59bda-180">KB3063416</span><span class="sxs-lookup"><span data-stu-id="59bda-180">KB3063416</span></span> |<span data-ttu-id="59bda-181">디스크 펌웨어</span><span class="sxs-lookup"><span data-stu-id="59bda-181">Disk firmware</span></span> |<span data-ttu-id="59bda-182">유지 관리</span><span class="sxs-lookup"><span data-stu-id="59bda-182">Maintenance</span></span> |

<span data-ttu-id="59bda-183">이 절차를 사용하기 전에 업데이트를 적용하려면 다음을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="59bda-183">Before using this procedure to apply the update, make sure that:</span></span>

* <span data-ttu-id="59bda-184">두 장치 컨트롤러가 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-184">Both device controllers are online.</span></span>

<span data-ttu-id="59bda-185">다음 단계를 수행하여 업데이트 1.2를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-185">Perform the following steps to apply Update 1.2.</span></span> <span data-ttu-id="59bda-186">**업데이트를 완료하는 데 2시간 정도가 걸릴 수 있습니다.(소프트웨어에 약 30분, 드라이버에 30분, 디스크 펌웨어에 45분)**</span><span class="sxs-lookup"><span data-stu-id="59bda-186">**The updates could take around 2 hours to complete (approximately 30 minutes for software, 30 minutes for driver, 45 minutes for disk firmware).**</span></span>

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-the-azure-classic-portal-to-apply-update-12-after-removing-the-gateway-configuration"></a><span data-ttu-id="59bda-187">옵션 2: Azure 클래식 포털을 사용하여 게이트웨이 구성을 제거한 후에 업데이트 1.2를 적용하려면</span><span class="sxs-lookup"><span data-stu-id="59bda-187">Option 2: Use the Azure classic portal to apply Update 1.2 after removing the gateway configuration</span></span>
<span data-ttu-id="59bda-188">이 절차는 업데이트 1 이전의 소프트웨어 버전을 실행 중이고 데이터 0 이외의 다른 네트워크 인터페이스에 게이트웨이가 설정된 StorSimple 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-188">This procedure applies only to StorSimple devices that are running a software version prior to Update 1 and have a gateway set on a network interface other than DATA 0.</span></span> <span data-ttu-id="59bda-189">업데이트를 적용하기 전에 게이트웨이 설정의 선택을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-189">You will need to clear the gateway setting prior to applying the update.</span></span>

<span data-ttu-id="59bda-190">업데이트를 완료하는데 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-190">The update may take a few hours to complete.</span></span> <span data-ttu-id="59bda-191">호스트가 서로 다른 서브넷에 있는 경우 iSCSI 인터페이스에서 게이트웨이 구성을 제거하면 가동 중지 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-191">If your hosts are in different subnets, removing the gateway configuration on the iSCSI interfaces could result in downtime.</span></span> <span data-ttu-id="59bda-192">작동 중지 시간을 줄이려면 iSCSI 트래픽에 대해 데이터 0을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-192">We recommend that you configure DATA 0 for iSCSI traffic to reduce the downtime.</span></span>

<span data-ttu-id="59bda-193">다음 단계를 수행하여 게이트웨이로 네트워크 인터페이스를 사용하지 않도록 설정하고 업데이트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-193">Perform the following steps to disable the network interface with the gateway and then apply the update.</span></span>

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="59bda-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59bda-194">Next steps</span></span>
<span data-ttu-id="59bda-195">[업데이트 1.2 릴리스](storsimple-update1-release-notes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59bda-195">Learn more about the [Update 1.2 release](storsimple-update1-release-notes.md).</span></span>

