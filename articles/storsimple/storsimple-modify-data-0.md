---
title: "StorSimple 장치에서 DATA 0 설정 수정 | Microsoft Docs"
description: "StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치에서 DATA 0 네트워크 인터페이스를 다시 구성하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 3a47ff1eed220cede820e8698c3384300e94688d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="7d2cd-103">StorSimple 장치에서 DATA 0 네트워크 인터페이스 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d2cd-103">Modify the DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="7d2cd-104">개요</span><span class="sxs-lookup"><span data-stu-id="7d2cd-104">Overview</span></span>
<span data-ttu-id="7d2cd-105">Microsoft Azure StorSimple 장치에 DATA 0에서 DATA 5까지 6개의 네트워크 인터페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="7d2cd-106">DATA 0 인터페이스는 항상 Windows PowerShell 인터페이스 또는 직렬 콘솔을 통해 구성되며 자동으로 클라우드가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="7d2cd-107">Azure 클래식 포털을 통해 DATA 0 네트워크 인터페이스를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-107">Note that you cannot configure DATA 0 network interface through the Azure classic portal.</span></span> 

<span data-ttu-id="7d2cd-108">StorSimple 장치의 초기 배포 중 설치 마법사를 통해 DATA 0 인터페이스가 처음 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="7d2cd-109">장치가 운영 모드에 있을 때 DATA 0를 다시 구성해야할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="7d2cd-110">이 자습서에서는 StorSimple용 Windows PowerShell을 통해 DATA 0 네트워크 설정을 수정하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="7d2cd-111">이 자습서를 읽은 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="7d2cd-112">설정 마법사를 통해 DATA 0 네트워크 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d2cd-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="7d2cd-113">`Set-HcsNetInterface` cmdlet을 통해 DATA 0 네트워크 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d2cd-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="7d2cd-114">설정 마법사를 통해 DATA 0 네트워크 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d2cd-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="7d2cd-115">StorSimple 장치의 Windows PowerShell 인터페이스에 연결하고 설치 마법사 세션을 실행하여 DATA 0 네트워크 설정을 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="7d2cd-116">DATA 0 설정을 수정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="7d2cd-117">설정 마법사를 통해 DATA 0 네트워크 설정을 수정하려면</span><span class="sxs-lookup"><span data-stu-id="7d2cd-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="7d2cd-118">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="7d2cd-119">메시지가 표시되면 **장치 관리자 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="7d2cd-120">기본 암호는 `Password1`입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="7d2cd-121">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="7d2cd-122">장치의 DATA 0 인터페이스 구성을 도와주는 설치 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-122">A setup wizard will appear to help you configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="7d2cd-123">IP 주소, 게이트웨이 및 네트워크 마스크에 대한 새 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="7d2cd-124">Azure 클래식 포털에서 StorSimple 장치 **구성** 페이지를 통해 고정된 컨트롤러 IP를 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-124">The fixed controllers IPs will need to be reconfigured through the **Configure** page of the StorSimple device in the Azure classic portal.</span></span> <span data-ttu-id="7d2cd-125">자세한 내용은 [네트워크 인터페이스 수정](storsimple-modify-device-config.md#modify-network-interfaces)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-125">For more information, go to [Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="7d2cd-126">Set-HcsNetInterface cmdlet을 통해 DATA 0 네트워크 설정 수정</span><span class="sxs-lookup"><span data-stu-id="7d2cd-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="7d2cd-127">다른 방법은 `Set-HcsNetInterface` cmdlet을 사용하여 DATA 0 네트워크 인터페이스를 다시 구성하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-127">An alternate way to reconfigure DATA 0 network interface is through the use of  the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="7d2cd-128">StorSimple 장치의 Windows PowerShell 인터페이스에서 cmdlet이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="7d2cd-129">이 절차를 사용하면 컨트롤러가 고정된 IP를 여기서 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="7d2cd-130">DATA 0 설정을 수정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="7d2cd-131">Set-HcsNetInterface cmdlet을 통해 DATA 0 네트워크 설정을 수정하려면</span><span class="sxs-lookup"><span data-stu-id="7d2cd-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="7d2cd-132">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="7d2cd-133">메시지가 표시되면 장치 관리자 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="7d2cd-134">기본 암호는 `Password1`입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="7d2cd-135">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="7d2cd-136">각괄호에 DATA 0에 대해 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="7d2cd-137">IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="7d2cd-137">IPv4 address</span></span>
   * <span data-ttu-id="7d2cd-138">IPv4 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="7d2cd-138">IPv4 gateway</span></span>
   * <span data-ttu-id="7d2cd-139">IPv4 서브넷 마스크</span><span class="sxs-lookup"><span data-stu-id="7d2cd-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="7d2cd-140">컨트롤러 0에 대한 고정 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="7d2cd-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="7d2cd-141">컨트롤러 1에 대한 고정 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="7d2cd-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="7d2cd-142">이 cmdlet을 사용하는 방법에 대한 자세한 내용은 [StorSimple용 Windows PowerShell cmdlet 참조](https://technet.microsoft.com/library/dn688161.aspx)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d2cd-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d2cd-143">Next steps</span></span>
* <span data-ttu-id="7d2cd-144">DATA 0 이외의 네트워크 인터페이스를 구성하려면 [Azure 클래식 포털에서 페이지 구성](storsimple-modify-device-config.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-144">To configure network interfaces other than DATA 0, you can use the [Configure page in the Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="7d2cd-145">네트워크 인터페이스를 구성할 때 문제가 발생하는 경우 [배포 문제 해결](storsimple-troubleshoot-deployment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d2cd-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

