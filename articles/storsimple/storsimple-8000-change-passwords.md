---
title: "StorSimple 암호 변경 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스를 사용하여 StorSimple 스냅숏 관리자 및 장치 관리자 암호를 변경하는 방법에 대해 설명합니다."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="8edef-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 암호 변경</span><span class="sxs-lookup"><span data-stu-id="8edef-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="8edef-104">개요</span><span class="sxs-lookup"><span data-stu-id="8edef-104">Overview</span></span>
<span data-ttu-id="8edef-105">Azure Portal의 **장치 관리자** 옵션에는 StorSimple 장치 관리자 서비스로 관리되는 StorSimple 장치에서 다시 구성할 수 있는 모든 장치 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="8edef-106">이 자습서에서는 **장치 설정**에서 **보안** 옵션을 사용하여 장치 관리자 또는 StorSimple Snapshot Manager 암호를 변경하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="8edef-107">장치 관리자 암호 구성</span><span class="sxs-lookup"><span data-stu-id="8edef-107">Change the device administrator password</span></span>
<span data-ttu-id="8edef-108">Windows PowerShell 인터페이스를 사용하여 StorSimple 장치에 액세스할 때 장치 관리자 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="8edef-109">StorSimple 장치를 서비스에 처음으로 등록할 때 이 인터페이스의 기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="8edef-110">데이터 보안을 위해 등록 과정 마지막에 이 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="8edef-111">이 암호를 변경하지 않고 등록 과정을 종료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="8edef-112">자세한 내용은 [3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8edef-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="8edef-113">등록하는 동안 먼저 Windows PowerShell 인터페이스를 통해 설정된 암호는 나중에 Azure Portal을 통해 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="8edef-114">장치 관리자 암호를 변경하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="8edef-115">장치 관리자 암호 변경 방법</span><span class="sxs-lookup"><span data-stu-id="8edef-115">To change the device administrator password</span></span>
1. <span data-ttu-id="8edef-116">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="8edef-117">장치를 나열하는 테이블에서 해당 암호를 변경하려는 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="8edef-118">**설정** 블레이드에서 **장치 설정 > 보안**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="8edef-119">**보안 설정** 블레이드에서 **암호**를 클릭하여 장치 관리자 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="8edef-120">**암호** 블레이드에서 8자에서 15자를 포함하는 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="8edef-121">암호는 대문자, 소문자, 숫자 및 특수 문자 중 3가지 이상의 조합이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="8edef-122">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="8edef-123">**저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="8edef-124">이제 장치 관리자 암호를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="8edef-125">이 수정된 암호를 사용하여 Windows PowerShell 인터페이스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="8edef-126">StorSimple 스냅숏 관리자 암호 설정</span><span class="sxs-lookup"><span data-stu-id="8edef-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="8edef-127">StorSimple 스냅숏 관리자 소프트웨어는 Windows 호스트에 상주하며 관리자가 로컬 및 클라우드 스냅숏의 형태로 StorSimple 장치의 백업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="8edef-128">StorSimple 스냅숏 관리자에서 장치를 구성하면, 장치 IP 주소 및 암호를 입력하여 저장소 장치를 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="8edef-129">Azure Portal을 통해 StorSimple Snapshot Manager에 대한 암호를 설정하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="8edef-130">다음 단계를 수행하여 StorSimple Snapshot Manager 암호를 설정하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="8edef-131">StorSimple Snapshot Manager 암호를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="8edef-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="8edef-132">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="8edef-133">장치를 나열하는 테이블에서 해당 StorSimple Snapshot Manager 암호를 설정하거나 변경하려는 장치를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="8edef-134">**설정** 블레이드에서 **장치 설정 > 보안**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="8edef-135">**보안 설정** 블레이드에서 **암호**를 클릭하여 StorSimple Snapshot Manager 암호를 설정하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="8edef-136">**암호** 블레이드에서 14자 또는 15자인 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="8edef-137">암호에 대문자, 소문자, 숫자 및 특수 문자 중 3가지 이상의 조합이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="8edef-138">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="8edef-139">**저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="8edef-140">이제 StorSimple 스냅숏 관리자 암호가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8edef-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8edef-141">Next steps</span></span>
* <span data-ttu-id="8edef-142">[StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="8edef-143">[장치 구성을 수정](storsimple-8000-modify-device-config.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="8edef-144">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8edef-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

