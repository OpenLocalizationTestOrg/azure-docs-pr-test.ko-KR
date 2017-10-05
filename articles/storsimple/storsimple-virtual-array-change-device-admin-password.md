---
title: "StorSimple Virtual Array 장치 관리자 암호 변경 | Microsoft Docs"
description: "Azure Portal 또는 StorSimple 가상 배열 웹 UI를 사용하여 장치 관리자 암호를 변경하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="c77a0-103">StorSimple 장치 관리자를 통해 StorSimple 가상 배열 장치 관리자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="c77a0-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="c77a0-104">개요</span><span class="sxs-lookup"><span data-stu-id="c77a0-104">Overview</span></span>

<span data-ttu-id="c77a0-105">Windows PowerShell 인터페이스를 사용하여 StorSimple 가상 배열에 액세스할 때 장치 관리자 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="c77a0-106">StorSimple 장치를 처음으로 프로비저닝하고 시작할 때 기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="c77a0-107">데이터 보안을 위해 처음 로그인하면 기본 암호가 만료되며, 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="c77a0-108">프로덕션 환경에 장치가 배포된 후에는 언제든지 로컬 웹 UI 또는 Azure Portal을 사용하여 장치 관리자 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="c77a0-109">이 문서에서는 각 절차에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-109">Each of these procedures is described in this article.</span></span>

 ![장치 블레이드](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="c77a0-111">Azure Portal을 사용하여 암호 변경</span><span class="sxs-lookup"><span data-stu-id="c77a0-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="c77a0-112">Azure Portal을 통해 장치 관리자 암호를 변경하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="c77a0-113">Azure Portal을 통해 장치 관리자 암호를 변경하려면</span><span class="sxs-lookup"><span data-stu-id="c77a0-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="c77a0-114">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **관리** 섹션 내에서 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="c77a0-115">그러면 모든 StorSimple 가상 배열 장치를 나열하는 **장치** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="c77a0-116">**장치** 블레이드에서 암호를 변경해야 하는 장치를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="c77a0-117">장치의 **설정** 블레이드에서 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="c77a0-118">**보안 설정** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="c77a0-119">**장치 관리자 암호** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="c77a0-120">8자에서 15자를 포함하는 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="c77a0-121">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-121">Confirm the password.</span></span>
   3. <span data-ttu-id="c77a0-122">블레이드 위쪽에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="c77a0-123">장치 관리자 암호가 이제 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-123">The device administrator password is now updated.</span></span> <span data-ttu-id="c77a0-124">수정된 암호를 사용하여 로컬에서 장치에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-124">You can use this modified password to access the device locally.</span></span>

![보안 설정 블레이드](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="c77a0-126">로컬 웹 UI를 사용하여 암호 변경</span><span class="sxs-lookup"><span data-stu-id="c77a0-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="c77a0-127">로컬 웹 UI를 통해 장치 관리자 암호를 변경하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="c77a0-128">로컬 웹 UI를 통해 장치 관리자 암호를 변경하려면</span><span class="sxs-lookup"><span data-stu-id="c77a0-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="c77a0-129">로컬 웹 UI에서 장치에 대한 **유지 관리** > **암호 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![password1 변경](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="c77a0-131">**현재 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="c77a0-132">**새 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-132">Provide a **New Password**.</span></span> <span data-ttu-id="c77a0-133">암호의 길이는 8자 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="c77a0-134">대문자, 소문자, 숫자 및 특수 문자 이렇게 4가지 중 3가지가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="c77a0-135">암호는 마지막 24개의 암호와 동일할 수 없으니 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="c77a0-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="c77a0-136">확인을 위해 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-136">Reenter the password to confirm it.</span></span>
   
    ![password2 변경](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="c77a0-138">페이지 아래쪽에서 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="c77a0-139">이제 새 암호가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-139">The new password is now applied.</span></span> <span data-ttu-id="c77a0-140">암호 변경이 실패하면 다음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-140">If the password change is not successful, you see the following error:</span></span>
   
    ![암호 오류](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="c77a0-142">암호가 성공적으로 업데이트되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="c77a0-143">그런 다음 수정된 암호를 사용하여 로컬에서 장치에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c77a0-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c77a0-144">Next steps</span></span>
<span data-ttu-id="c77a0-145">[StorSimple 가상 배열을 관리](storsimple-ova-web-ui-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c77a0-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

