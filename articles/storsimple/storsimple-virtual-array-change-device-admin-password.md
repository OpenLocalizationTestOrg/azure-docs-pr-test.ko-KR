---
title: "aaaChange StorSimple 가상 배열 장치 관리자 암호 | Microsoft Docs"
description: "어떻게 toouse 하거나 hello Azure 포털 또는 StorSimple 가상 배열 웹 UI toochange hello 장치 관리자 암호에 설명 합니다."
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
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="2088a-103">Hello StorSimple 가상 배열 장치 관리자 암호를 통해 StorSimple 장치 관리자를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="2088a-104">개요</span><span class="sxs-lookup"><span data-stu-id="2088a-104">Overview</span></span>

<span data-ttu-id="2088a-105">사용 하는 경우 Windows PowerShell 인터페이스 tooaccess hello hello StorSimple 가상 배열, 필요한 tooenter 장치 관리자 암호는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="2088a-106">Hello 기본 암호는 hello StorSimple 장치를 처음 프로 비전 및 시작 하는 경우 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="2088a-107">데이터의 hello 보안용 hello 기본 암호가 만료 된 후 처음으로 로그인 할 hello 하 고 필요한 toochange이이 암호는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="2088a-108">또한 hello 장치 프로덕션 환경에 배포 된 후 언제 든 지 어느 hello 로컬 웹 UI 또는 hello Azure 포털 toochange hello 장치 관리자 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="2088a-109">이 문서에서는 각 절차에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-109">Each of these procedures is described in this article.</span></span>

 ![장치 블레이드](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="2088a-111">Hello Azure 포털 toochange hello 암호 사용</span><span class="sxs-lookup"><span data-stu-id="2088a-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="2088a-112">Hello 단계 toochange hello 장치 관리자 암호 hello Azure 포털을 통해 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="2088a-113">hello Azure 포털을 통해 toochange hello 장치 관리자 암호</span><span class="sxs-lookup"><span data-stu-id="2088a-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="2088a-114">Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **관리** 섹션에서 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="2088a-115">Hello 열립니다 **장치** 블레이드를 모든 StorSimple 가상 배열 장치를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="2088a-116">Hello에 **장치** 블레이드에서 암호의 변경이 필요한 hello 장치를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="2088a-117">Hello에 **설정** 해당 장치용 블레이드 클릭 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="2088a-118">Hello에 **보안 설정** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="2088a-119">Toohello 아래로 스크롤하여 **장치 관리자 암호** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2088a-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="2088a-120">8 too15 15 자 사이 포함 하는 관리자 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="2088a-121">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="2088a-122">클릭 **저장** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="2088a-123">이제 hello 장치 관리자 암호가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="2088a-124">이 수정 된 암호 tooaccess hello 장치를 로컬로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-124">You can use this modified password tooaccess hello device locally.</span></span>

![보안 설정 블레이드](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="2088a-126">Hello 로컬 웹 UI toochange hello 암호 사용</span><span class="sxs-lookup"><span data-stu-id="2088a-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="2088a-127">Hello 단계 toochange hello 장치 관리자 암호 hello 로컬 웹 UI 통해 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="2088a-128">hello 로컬 웹 UI 통해 toochange hello 장치 관리자 암호</span><span class="sxs-lookup"><span data-stu-id="2088a-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="2088a-129">Hello 로컬 웹 UI에서에서 클릭 **유지 관리** > **암호 변경을** 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![password1 변경](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="2088a-131">Hello 입력 **현재 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="2088a-132">**새 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-132">Provide a **New Password**.</span></span> <span data-ttu-id="2088a-133">hello 암호는 길이가 적어도 8 자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="2088a-134">3 / 4 hello 다음을 포함 해야 합니다: 대문자, 소문자, 숫자 및 특수 문자.</span><span class="sxs-lookup"><span data-stu-id="2088a-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="2088a-135">암호를 입력 하는 hello hello 지난 24 개의 암호와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="2088a-136">Hello 암호 tooconfirm 다시 입력 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-136">Reenter hello password tooconfirm it.</span></span>
   
    ![password2 변경](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="2088a-138">Hello hello 페이지의 아래쪽에 있는 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="2088a-139">이제 hello 새 암호가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-139">hello new password is now applied.</span></span> <span data-ttu-id="2088a-140">Hello 암호 변경이 실패할 경우 hello 다음 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![암호 오류](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="2088a-142">Hello 암호를 업데이트 한 후 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="2088a-143">그런 다음이 수정 된 암호 tooaccess hello 장치를 로컬로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2088a-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2088a-144">Next steps</span></span>
<span data-ttu-id="2088a-145">너무 방법에 대해 알아봅니다[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2088a-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

