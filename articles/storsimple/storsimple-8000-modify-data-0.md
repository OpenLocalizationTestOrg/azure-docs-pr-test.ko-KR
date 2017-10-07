---
title: "데이터 0 aaaModify StorSimple 8000 시리즈 장치에 설정을 | Microsoft Docs"
description: "자세한 내용은 StorSimple tooreconfigure에 대 한 Windows PowerShell toouse StorSimple 장치에서 DATA 0 네트워크 인터페이스를 hello 하는 방법입니다."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="7d94a-103">StorSimple 8000 시리즈 장치에 hello DATA 0 네트워크 인터페이스 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-103">Modify hello DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="7d94a-104">개요</span><span class="sxs-lookup"><span data-stu-id="7d94a-104">Overview</span></span>

<span data-ttu-id="7d94a-105">Microsoft Azure StorSimple 장치에는 DATA 0에서에서 6 개의 네트워크 인터페이스 tooDATA 5입니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="7d94a-106">hello DATA 0 인터페이스는 항상 hello Windows PowerShell 인터페이스 또는 hello 직렬 콘솔을 통해 구성 및 자동으로 클라우드 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="7d94a-107">참고 hello Azure 포털을 통해 DATA 0 네트워크 인터페이스를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-107">Note that you cannot configure DATA 0 network interface through hello Azure portal.</span></span>

<span data-ttu-id="7d94a-108">hello DATA 0 인터페이스는 처음 hello StorSimple 장치의 초기 배포 시 hello 설치 마법사를 통해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="7d94a-109">데이터 0 tooreconfigure hello 장치가 작동 모드에 있을 때 할 수 있습니다 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="7d94a-110">이 자습서는 StorSimple 용 Windows PowerShell을 통해 모두 toomodify DATA 0 네트워크 설정을 두 개의 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="7d94a-111">이 자습서를 읽은 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="7d94a-112">수정 DATA 0 네트워크 hello 설치 마법사를 통해 설정</span><span class="sxs-lookup"><span data-stu-id="7d94a-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="7d94a-113">DATA 0 네트워크 설정을 hello 통해 수정 `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="7d94a-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="7d94a-114">설정 마법사를 통해 DATA 0 네트워크 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d94a-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="7d94a-115">StorSimple 장치의 toohello Windows PowerShell 인터페이스를 연결 하 고 설치 마법사 세션을 시작 하 여 DATA 0 네트워크 설정을 재구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="7d94a-116">다음 단계 toomodify DATA 0 hello 수행 설정:</span><span class="sxs-lookup"><span data-stu-id="7d94a-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="7d94a-117">설치 마법사를 통해 toomodify DATA 0 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="7d94a-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="7d94a-118">Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="7d94a-119">메시지가 표시 되 면 hello 제공 **장치 관리자 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="7d94a-120">hello 기본 암호는 `Password1`합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="7d94a-121">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="7d94a-122">설치 마법사가 toohelp 나타나면 DATA 0 hello 구성 장치의 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-122">A setup wizard appears toohelp configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="7d94a-123">Hello IP 주소, 게이트웨이 및 네트워크 마스크에 대 한 새 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="7d94a-124">고정 컨트롤러 Ip toobe hello를 통해 다시 구성 해야 합니다는 hello **네트워크 설정** hello Azure 포털에에서 표시 되는 hello StorSimple 장치의 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-124">hello fixed controllers IPs will need toobe reconfigured through hello **Network settings** blade of hello StorSimple device in hello Azure portal.</span></span> <span data-ttu-id="7d94a-125">자세한 내용은 이동 너무[네트워크 인터페이스 수정](storsimple-8000-modify-device-config.md#modify-network-interfaces)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-125">For more information, go too[Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="7d94a-126">Set-HcsNetInterface cmdlet을 통해 DATA 0 네트워크 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d94a-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="7d94a-127">대체 방식으로 tooreconfigure DATA 0 네트워크 인터페이스는 hello hello 사용을 통해 `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7d94a-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="7d94a-128">hello cmdlet은 StorSimple 장치의 hello Windows PowerShell 인터페이스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="7d94a-129">이 절차를 사용 하 여 hello 컨트롤러 고정 Ip 여기 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="7d94a-130">다음 단계 toomodify hello DATA 0 hello 수행 설정:</span><span class="sxs-lookup"><span data-stu-id="7d94a-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="7d94a-131">hello Set-hcsnetinterface cmdlet 통해 toomodify DATA 0 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="7d94a-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="7d94a-132">Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="7d94a-133">메시지가 표시 되 면 hello 장치 관리자 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="7d94a-134">hello 기본 암호는 `Password1`합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="7d94a-135">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="7d94a-136">각 진 hello 대괄호로 hello DATA 0에 대 한 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="7d94a-137">IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="7d94a-137">IPv4 address</span></span>
   * <span data-ttu-id="7d94a-138">IPv4 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="7d94a-138">IPv4 gateway</span></span>
   * <span data-ttu-id="7d94a-139">IPv4 서브넷 마스크</span><span class="sxs-lookup"><span data-stu-id="7d94a-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="7d94a-140">컨트롤러 0에 대한 고정 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="7d94a-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="7d94a-141">컨트롤러 1에 대한 고정 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="7d94a-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="7d94a-142">이 cmdlet의 hello 사용에 자세한 내용은 이동 너무[용 Windows PowerShell StorSimple cmdlet 참조](https://technet.microsoft.com/library/dn688161.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d94a-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d94a-143">Next steps</span></span>
* <span data-ttu-id="7d94a-144">데이터 0 이외의 tooconfigure 네트워크 인터페이스, hello를 사용할 수 있습니다 [hello Azure 포털에서에서 네트워크 설정을 구성](storsimple-8000-modify-device-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure network settings in hello Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="7d94a-145">네트워크 인터페이스를 구성할 때 문제가 발생 하면 너무 참조[배포 문제를 해결](storsimple-troubleshoot-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d94a-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

