---
title: "aaaUpdate StorSimple 장치 | Microsoft Docs"
description: "일반 기능 tooinstall 및 유지 관리 모드 업데이트 및 핫픽스 toouse hello StorSimple 업데이트 하는 방법에 대해 설명 합니다."
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
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="7568f-103">StorSimple 8000 시리즈 장치 업데이트</span><span class="sxs-lookup"><span data-stu-id="7568f-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="7568f-104">개요</span><span class="sxs-lookup"><span data-stu-id="7568f-104">Overview</span></span>
<span data-ttu-id="7568f-105">hello StorSimple 업데이트 기능을 사용 하면 tooeasily StorSimple 장치를 최신 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="7568f-106">Hello 업데이트 종류에 따라 업데이트 toohello 장치 hello Azure 클래식 포털을 통해 또는 hello Windows PowerShell 인터페이스를 통해 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="7568f-107">이 자습서에서는 hello 업데이트 유형을 설명 방법과 각 tooinstall 그 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="7568f-108">두 종류의 장치 업데이트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="7568f-109">일반(또는 표준 모드) 업데이트</span><span class="sxs-lookup"><span data-stu-id="7568f-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="7568f-110">유지 관리 모드 업데이트</span><span class="sxs-lookup"><span data-stu-id="7568f-110">Maintenance mode updates</span></span>

<span data-ttu-id="7568f-111">Hello Azure 클래식 포털 또는 Windows PowerShell;를 통해 정기적으로 업데이트를 설치할 수 있습니다. 그러나 Windows PowerShell tooinstall 유지 관리 모드 업데이트를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="7568f-112">각 업데이트 유형은 아래에 별도로 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="7568f-113">일반 업데이트</span><span class="sxs-lookup"><span data-stu-id="7568f-113">Regular updates</span></span>
<span data-ttu-id="7568f-114">정기적인 업데이트는 hello 장치가 표준 모드일 때 설치할 수 있도록 정기적인 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="7568f-115">이러한 업데이트는 hello Microsoft Update 웹 사이트 tooeach 장치 컨트롤러를 통해 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7568f-116">컨트롤러 장애 조치 hello 업데이트 프로세스 중 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="7568f-117">그러나 시스템 가용성 또는 작업에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="7568f-118">Tooinstall regular 업데이트 하는 방법을 통해 hello Azure 클래식 포털에 대 한 세부 정보를 참조 하십시오. [hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치](#install-regular-updates-via-the-azure-classic-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="7568f-119">StorSimple용 Windows PowerShell을 통해 일반 업데이트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7568f-120">자세한 내용은 [StorSimple용 Windows PowerShell을 통해 일반 업데이트 설치](#install-regular-updates-via-windows-powershell-for-storsimple)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7568f-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="7568f-121">유지 관리 모드 업데이트</span><span class="sxs-lookup"><span data-stu-id="7568f-121">Maintenance mode updates</span></span>
<span data-ttu-id="7568f-122">유지 관리 모드 업데이트는 디스크 펌웨어 업그레이드 등의 강제 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="7568f-123">이러한 업데이트는 hello 장치 toobe 유지 관리 모드로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="7568f-124">자세한 내용은 [2단계: 입력 유지 관리 모드](#step2)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7568f-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="7568f-125">Hello Azure 클래식 포털 tooinstall 유지 관리 모드 업데이트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="7568f-126">대신 StorSimple용 Windows PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="7568f-127">Tooinstall 유지 관리 모드 업데이트 하는 방식에 대 한 세부 정보를 참조 하십시오. [StorSimple 용 Windows PowerShell을 통해 설치 유지 관리 모드 업데이트](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple)합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7568f-128">유지 관리 모드 업데이트 해야 tooeach 컨트롤러 개별적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="7568f-129">Hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="7568f-130">Hello Azure 클래식 포털 tooapply 업데이트 tooyour StorSimple 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7568f-131">StorSimple용 Windows PowerShell을 통해 일반 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="7568f-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7568f-132">또는 StorSimple tooapply (기본 모드) 일반 업데이트에 대 한 Windows PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7568f-133">StorSimple 용 Windows PowerShell을 사용 하 여 정기적인 업데이트를 설치할 수 있지만 hello Azure 클래식 포털을 통해 정기적인 업데이트를 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="7568f-134">업데이트 1 부터는 사전 검사 hello 포털에서 수행된 된 이전 tooinstalling 업데이트를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="7568f-135">이러한 검사는 오류의 사전 파악과 더 원활한 환경을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7568f-136">StorSimple용 Windows PowerShell을 통해 유지 관리 모드 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="7568f-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7568f-137">StorSimple tooapply 유지 관리 모드 업데이트 tooyour StorSimple 장치에 대 한 Windows PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="7568f-138">모든 I/O 요청은 이 모드에서 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="7568f-139">비휘발성 메모리 (NVRAM) 또는 서비스를 클러스터링 하는 hello와 같은 서비스 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="7568f-140">이 모드를 종료하거나 입력하면 두 컨트롤러 모두 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="7568f-141">이 모드를 종료 하면 모든 hello 서비스 다시 시작 됩니다 하 고 정상 상태 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="7568f-142">(몇 분이 걸릴 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="7568f-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="7568f-143">Tooapply 유지 관리 모드 업데이트 해야 할 경우 설치 해야 하는 업데이트가 있는지 hello Azure 클래식 포털을 통해 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="7568f-144">이 경고에는 StorSimple tooinstall hello 업데이트에 대 한 Windows PowerShell을 사용 하기 위한 지침이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="7568f-145">장치를 업데이트 한 후 사용 하 여 hello 동일한 프로시저 toochange hello 장치 tooRegular 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="7568f-146">단계별 지침은 [4단계: 유지 관리 모드를 종료](#step4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7568f-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7568f-147">유지 관리 모드를 설정 하기 전에 hello를 확인 하 여 두 장치 컨트롤러가 모두의 상태가 정상 인지 확인 **하드웨어 상태** hello에 **유지 관리** hello Azure 클래식 포털에서에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="7568f-148">Hello 컨트롤러 상태가 정상이 아닌 경우 hello 다음 단계에 대 한 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="7568f-149">자세한 내용은 Microsoft 기술 지원 서비스 tooContact 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="7568f-150">Tooapply 유지 관리 모드에 있는 경우 해야 컨트롤러 하나에 업데이트를 먼저 hello 및 다음에 다른 컨트롤러를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="7568f-151">1 단계: toohello 직렬 콘솔에 연결<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="7568f-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="7568f-152">PuTTY tooaccess 직렬 콘솔 hello와 같은 응용 프로그램을 먼저 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="7568f-153">hello 다음 절차에 설명 방법을 toouse PuTTY tooconnect toohello 직렬 콘솔.</span><span class="sxs-lookup"><span data-stu-id="7568f-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="7568f-154">2단계: 유지 관리 모드 시작 <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="7568f-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="7568f-155">업데이트 tooinstall 있는지 여부를 결정 하 고 유지 관리 모드 tooinstall 입력 toohello 콘솔을 연결 하면 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="7568f-156">3단계: 프로그램 업데이트 설치 <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="7568f-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="7568f-157">다음으로 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="7568f-158">4단계: 유지 관리 모드 종료 <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="7568f-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="7568f-159">마지막으로, 유지 관리 모드를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7568f-160">StorSimple용 Windows PowerShell을 통해 핫픽스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7568f-161">Microsoft Azure StorSimple에 대한 업데이트와 달리 핫픽스는 공유 폴더에서 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="7568f-162">업데이트와 마찬가지로 두 종류의 핫픽스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="7568f-163">일반 핫픽스</span><span class="sxs-lookup"><span data-stu-id="7568f-163">Regular hotfixes</span></span> 
* <span data-ttu-id="7568f-164">유지 관리 모드 핫픽스</span><span class="sxs-lookup"><span data-stu-id="7568f-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="7568f-165">hello 다음 절차에서는 설명 어떻게 StorSimple tooinstall 일반 및 유지 관리 모드 핫픽스를 Windows PowerShell toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="7568f-166">Hello 장치의 재설정 tooupdates 팩터리를 수행 하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="7568f-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="7568f-167">장치 재설정 toofactory 설정 이면 모든 hello 업데이트가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="7568f-168">Hello 공장 재설정 한 장치를 등록 및 구성한 후 StorSimple에 대 한 toomanually hello Azure 클래식 포털 및/또는 Windows PowerShell을 통해 업데이트를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7568f-169">공장 기본 설정에 대 한 자세한 내용은 참조 [hello 장치 toofactory 기본 설정으로 초기화](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7568f-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7568f-170">Next steps</span></span>
* <span data-ttu-id="7568f-171">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple tooadminister 용 Windows PowerShell을 사용한](storsimple-windows-powershell-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="7568f-172">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7568f-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

