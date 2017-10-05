---
title: "StorSimple 장치 관리자를 통해 암호 변경 | Microsoft Docs"
description: "StorSimple 관리자 서비스를 사용하여 StorSimple 스냅숏 관리자 및 장치 관리자 암호를 변경하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d890b59595628ca3eeff1df258847c2bb54d29ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="744eb-103">StorSimple 관리자 서비스를 사용하여 StorSimple 암호 변경</span><span class="sxs-lookup"><span data-stu-id="744eb-103">Use the StorSimple Manager service to change your StorSimple passwords</span></span>
## <a name="overview"></a><span data-ttu-id="744eb-104">개요</span><span class="sxs-lookup"><span data-stu-id="744eb-104">Overview</span></span>
<span data-ttu-id="744eb-105">Azure 클래식 포털 **구성** 페이지에는 StorSimple 관리자 서비스로 관리되는 StorSimple 장치에서 다시 구성할 수 있는 모든 장치 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-105">The Azure classic portal **Configure** page contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Manager service.</span></span> <span data-ttu-id="744eb-106">이 자습서에서는 **구성** 페이지를 사용하여 장치 관리자 또는 StorSimple Snapshot Manager 암호를 변경하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-106">This tutorial explains how you can use the **Configure** page to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="744eb-107">장치 관리자 암호 구성</span><span class="sxs-lookup"><span data-stu-id="744eb-107">Change the device administrator password</span></span>
<span data-ttu-id="744eb-108">Windows PowerShell 인터페이스를 사용하여 StorSimple 장치에 액세스할 때 장치 관리자 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="744eb-109">StorSimple 장치를 서비스에 처음으로 등록할 때 이 인터페이스의 기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="744eb-110">데이터 보안을 위해 등록 과정 마지막에 이 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="744eb-111">이 암호를 변경하지 않고 등록 과정을 종료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="744eb-112">자세한 내용은 [3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="744eb-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="744eb-113">등록하는 동안 먼저 Windows PowerShell 인터페이스를 통해 설정된 암호는 Azure 클래식 포털을 통해 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-113">The password that was first set through the Windows PowerShell interface during registration can then be changed via the Azure classic portal.</span></span> <span data-ttu-id="744eb-114">장치 관리자 암호를 변경하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="744eb-115">장치 관리자 암호 변경 방법</span><span class="sxs-lookup"><span data-stu-id="744eb-115">To change the device administrator password</span></span>
1. <span data-ttu-id="744eb-116">클래식 포털에서 사용자의 장치에 대해 **장치** > **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-116">In the classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="744eb-117">**장치 관리자 암호** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-117">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="744eb-118">8자에서 15자를 포함하는 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-118">Provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="744eb-119">암호는 대문자, 소문자, 숫자 및 특수 문자 중 3가지 이상의 조합이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-119">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="744eb-120">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-120">Confirm the password.</span></span>
4. <span data-ttu-id="744eb-121">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-121">Click **Save** at the bottom of the page.</span></span>

<span data-ttu-id="744eb-122">이제 장치 관리자 암호를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-122">The device administrator password should now be updated.</span></span> <span data-ttu-id="744eb-123">이 수정된 암호를 사용하여 Windows PowerShell 인터페이스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-123">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="change-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="744eb-124">StorSimple 스냅숏 관리자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="744eb-124">Change the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="744eb-125">StorSimple 스냅숏 관리자 소프트웨어는 Windows 호스트에 상주하며 관리자가 로컬 및 클라우드 스냅숏의 형태로 StorSimple 장치의 백업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-125">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="744eb-126">StorSimple 스냅숏 관리자에서 장치를 구성하면, 장치 IP 주소 및 암호를 입력하여 저장소 장치를 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-126">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span> <span data-ttu-id="744eb-127">이 암호는 Windows PowerShell 인터페이스를 통해 처음 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-127">This password is first configured through the Windows PowerShell interface.</span></span> <span data-ttu-id="744eb-128">자세한 내용은 [3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="744eb-128">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="744eb-129">등록하는 동안 먼저 Windows PowerShell 인터페이스를 통해 설정된 암호는 클래식 포털을 통해 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-129">The password that was first set through the Windows PowerShell interface during registration can then be changed via the classic portal.</span></span> <span data-ttu-id="744eb-130">다음 단계에서 StorSimple 스냅숏 관리자 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-130">Perform the following steps to change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-change-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="744eb-131">StorSimple 스냅숏 관리자 암호 변경 방법</span><span class="sxs-lookup"><span data-stu-id="744eb-131">To change the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="744eb-132">클래식 포털에서 사용자의 장치에 대해 **장치** > **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-132">In the classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="744eb-133">**StorSimple 스냅숏 관리자** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-133">Scroll down to the **StorSimple Snapshot Manager** section.</span></span> <span data-ttu-id="744eb-134">14자 또는 15자인 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-134">Enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="744eb-135">암호에 대문자, 소문자, 숫자 및 특수 문자 중 3가지 이상의 조합이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-135">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="744eb-136">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-136">Confirm the password.</span></span>
4. <span data-ttu-id="744eb-137">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-137">Click **Save** at the bottom of the page.</span></span>

<span data-ttu-id="744eb-138">이제 StorSimple 스냅숏 관리자 암호가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-138">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="744eb-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="744eb-139">Next steps</span></span>
* <span data-ttu-id="744eb-140">[StorSimple 보안](storsimple-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-140">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="744eb-141">[장치 구성을 수정](storsimple-modify-device-config.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-141">Learn more about [modifying your device configuration](storsimple-modify-device-config.md).</span></span>
* <span data-ttu-id="744eb-142">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="744eb-142">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

