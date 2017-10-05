---
title: "StorSimple 장치 업데이트 | Microsoft Docs"
description: "StorSimple 업데이트 기능을 사용하여 일반 및 유지 관리 모드 업데이트 및 핫픽스를 설치하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="d785f-103">StorSimple 8000 시리즈 장치 업데이트</span><span class="sxs-lookup"><span data-stu-id="d785f-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="d785f-104">개요</span><span class="sxs-lookup"><span data-stu-id="d785f-104">Overview</span></span>
<span data-ttu-id="d785f-105">StorSimple 업데이트 기능을 사용하면 쉽게 StorSimple 장치를 최신 상태로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="d785f-106">업데이트 유형에 따라 Windows PowerShell 인터페이스 또는 Azure 클래식 포털을 통해 장치에 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="d785f-107">이 자습서에는 업데이트 유형 및 각 항목을 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="d785f-108">두 종류의 장치 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="d785f-109">일반(또는 표준 모드) 업데이트</span><span class="sxs-lookup"><span data-stu-id="d785f-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="d785f-110">유지 관리 모드 업데이트</span><span class="sxs-lookup"><span data-stu-id="d785f-110">Maintenance mode updates</span></span>

<span data-ttu-id="d785f-111">Azure 클래식 포털 또는 Windows PowerShell을 통해 정기적으로 업데이트를 설치할 수 있습니다. 그러나 Windows PowerShell을 사용하여 유지 관리 모드 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="d785f-112">각 업데이트 유형은 아래에 별도로 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="d785f-113">일반 업데이트</span><span class="sxs-lookup"><span data-stu-id="d785f-113">Regular updates</span></span>
<span data-ttu-id="d785f-114">일반 업데이트는 장치가 표준 모드에 있을 때 설치할 수 있는 무중단 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="d785f-115">이 업데이트는 Microsoft Update 웹사이트를 통해 각 장치 컨트롤러에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d785f-116">컨트롤러 장애 조치는 업데이트 과정에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="d785f-117">그러나 시스템 가용성 또는 작업에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="d785f-118">Azure 클래식 포털을 통해 일반 업데이트를 설치하는 방법에 대한 자세한 내용은 [Azure 클래식 포털을 통해 일반 업데이트 설치](#install-regular-updates-via-the-azure-classic-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="d785f-119">StorSimple용 Windows PowerShell을 통해 일반 업데이트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d785f-120">자세한 내용은 [StorSimple용 Windows PowerShell을 통해 일반 업데이트 설치](#install-regular-updates-via-windows-powershell-for-storsimple)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="d785f-121">유지 관리 모드 업데이트</span><span class="sxs-lookup"><span data-stu-id="d785f-121">Maintenance mode updates</span></span>
<span data-ttu-id="d785f-122">유지 관리 모드 업데이트는 디스크 펌웨어 업그레이드 등의 강제 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="d785f-123">이 업데이트를 사용하려면 장치가 유지 관리 모드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="d785f-124">자세한 내용은 [2단계: 입력 유지 관리 모드](#step2)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="d785f-125">Azure 클래식 포털을 사용하여 유지 관리 모드 업데이트를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="d785f-126">대신 StorSimple용 Windows PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="d785f-127">유지 관리 모드 업데이트를 설치하는 방법에 대한 세부 정보는 [StorSimple용 Windows PowerShell을 통해 유지 관리 모드 업데이트 설치](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d785f-128">유지 관리 모드 업데이트는 각 컨트롤러에 개별적으로 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="d785f-129">Azure 클래식 포털을 통해 일반 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="d785f-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="d785f-130">Azure 클래식 포털을 사용하여 StorSimple 장치에 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d785f-131">StorSimple용 Windows PowerShell을 통해 일반 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="d785f-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d785f-132">또는, StorSimple 용 Windows PowerShell을 사용하여 일반(표준 모드) 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d785f-133">StorSimple용 Windows PowerShell을 사용하여 정기적으로 업데이트를 설치할 수 있지만 Azure 클래식 포털을 통해 정기적으로 업데이트를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="d785f-134">업데이트 1부터, 포털에서 업데이트를 설치하기 전에 사전 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="d785f-135">이러한 검사는 오류의 사전 파악과 더 원활한 환경을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d785f-136">StorSimple용 Windows PowerShell을 통해 유지 관리 모드 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="d785f-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d785f-137">StorSimple용 Windows PowerShell을 사용하여 유지 관리 모드 업데이트를 StorSimple 장치에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="d785f-138">모든 I/O 요청은 이 모드에서 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="d785f-139">비휘발성 임의 액세스 메모리 (NVRAM) 등의 서비스 또는 클러스터링 서비스도 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="d785f-140">이 모드를 종료하거나 입력하면 두 컨트롤러 모두 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="d785f-141">이 모드를 종료하면 모든 서비스가 다시 시작되고 정상 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="d785f-142">(몇 분이 걸릴 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d785f-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="d785f-143">유지 관리 모드 업데이트를 적용해야 하는 경우  설치해야 하는 업데이트가 있다는 경고를 Azure 클래식 포털을 통해 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="d785f-144">이 경고는 StorSimple용 Windows PowerShell을 사용하여 업데이트를 설치하기 위한 지침을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="d785f-145">장치를 업데이트한 후, 동일한 절차에 따라 장치를 일반 모드로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="d785f-146">단계별 지침은 [4단계: 유지 관리 모드를 종료](#step4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d785f-147">유지 관리 모드에 들어가기 전에 Azure 클래식 포털의 **유지 관리** 페이지에서 **하드웨어 상태**를 확인하여 두 장치 컨트롤러 모두가 정상 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="d785f-148">컨트롤러가 정상 상태가 아니면 다음 단계는 Microsoft 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="d785f-149">자세한 내용은 Microsoft 지원에 문의로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="d785f-150">유지 관리 모드에 있는 경우, 업데이트를 먼저 하나의 컨트롤러에 적용한 다음 다른 컨트롤러에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="d785f-151">1단계: 직렬 콘솔에 연결 <a name="step1"></span><span class="sxs-lookup"><span data-stu-id="d785f-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="d785f-152">먼저,  PuTTY와 같은 응용 프로그램을 사용하여 직렬 콘솔에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="d785f-153">다음 절차는 PuTTY를 사용하여 직렬 콘솔에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="d785f-154">2단계: 유지 관리 모드 시작 <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="d785f-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="d785f-155">콘솔에 연결한 후, 설치할 업데이트가 있는지 여부를 결정하고 유지 관리 모드로 전환하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="d785f-156">3단계: 프로그램 업데이트 설치 <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="d785f-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="d785f-157">다음으로 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="d785f-158">4단계: 유지 관리 모드 종료 <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="d785f-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="d785f-159">마지막으로, 유지 관리 모드를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d785f-160">StorSimple용 Windows PowerShell을 통해 핫픽스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d785f-161">Microsoft Azure StorSimple에 대한 업데이트와 달리 핫픽스는 공유 폴더에서 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="d785f-162">업데이트와 마찬가지로 두 종류의 핫픽스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="d785f-163">일반 핫픽스</span><span class="sxs-lookup"><span data-stu-id="d785f-163">Regular hotfixes</span></span> 
* <span data-ttu-id="d785f-164">유지 관리 모드 핫픽스</span><span class="sxs-lookup"><span data-stu-id="d785f-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="d785f-165">다음 절차에서는 StorSimple 용 Windows PowerShell을 사용하여 일반 및 유지 관리 모드 핫픽스를 설치 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="d785f-166">장치를 공장 재설정하는 경우 업데이트에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="d785f-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="d785f-167">장치를 공장 기본 설정으로 다시 설정하는 경우 업데이트가 모두 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="d785f-168">공장 재설정 장치를 등록하고 구성한 후, StorSimple용 Windows PowerShell 및/또는 Azure 클래식 포털을 통해 수동으로 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d785f-169">공장 재설정에 대한 자세한 내용은 [장치를 공장 기본 설정으로 재설정](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d785f-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d785f-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d785f-170">Next steps</span></span>
* <span data-ttu-id="d785f-171">[StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치를 관리](storsimple-windows-powershell-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="d785f-172">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d785f-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

