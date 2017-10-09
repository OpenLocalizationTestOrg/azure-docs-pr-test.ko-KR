---
title: "aaaChange StorSimple 암호 | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 장치 관리자 서비스 toochange StorSimple 스냅숏 관리자 및 장치 관리자 암호에 설명 합니다."
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
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="fdff2-103">Hello StorSimple 장치 관리자 서비스 toochange StorSimple 암호 사용</span><span class="sxs-lookup"><span data-stu-id="fdff2-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="fdff2-104">개요</span><span class="sxs-lookup"><span data-stu-id="fdff2-104">Overview</span></span>
<span data-ttu-id="fdff2-105">Azure 포털 hello **장치 설정** 옵션 StorSimple 장치 관리자 서비스에서 관리 되는 StorSimple 장치에는 다시 구성할 수 있는 모든 hello 장치 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="fdff2-106">이 자습서에서는 hello를 사용 하는 방법에 대해 설명 **보안** 옵션에서 **장치 설정** toochange 장치 관리자 또는 StorSimple 스냅숏 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="fdff2-107">Hello 장치 관리자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="fdff2-107">Change hello device administrator password</span></span>
<span data-ttu-id="fdff2-108">Windows PowerShell 인터페이스 tooaccess hello StorSimple 장치를 사용 하 여 필요한 tooenter 장치 관리자 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="fdff2-109">이 인터페이스에 대 한 hello 기본 암호는 서비스와 hello 첫 번째 StorSimple 장치를 등록 하는 경우 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="fdff2-110">데이터의 hello 보안, 사용자가 필요한 toochange 때이 암호를 hello hello 등록 프로세스 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="fdff2-111">이 암호를 변경 하지 않고 hello 등록 프로세스를 종료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="fdff2-112">자세한 내용은 참조 [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="fdff2-113">hello 설정 된 암호를 먼저 hello Windows PowerShell 인터페이스를 통해 등록 하는 동안 hello Azure 포털을 통해 나중에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="fdff2-114">Hello 단계 toochange hello 장치 관리자 암호를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="fdff2-115">toochange hello 장치 관리자 암호</span><span class="sxs-lookup"><span data-stu-id="fdff2-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="fdff2-116">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="fdff2-117">장치의 hello 테이블 형식 목록에서 선택 하 고 hello 장치 암호를 클릭 하려는 toochange 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="fdff2-118">Hello에 **설정** 블레이드에서 너무 이동**장치 설정 > 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="fdff2-119">Hello에 **보안 설정** 블레이드에서 클릭 **암호** toochange hello 장치 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="fdff2-120">Hello에 **암호** 블레이드에서 8 too15 문자를 포함 하는 관리자 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="fdff2-121">hello 암호의 3 개 이상의 대문자, 소문자, 숫자 및 특수 문자 조합을 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="fdff2-122">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="fdff2-123">**저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="fdff2-124">이제 hello 장치 관리자 암호를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="fdff2-125">이 수정 된 암호 tooaccess hello Windows PowerShell 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="fdff2-126">Hello StorSimple 스냅숏 관리자 암호 설정</span><span class="sxs-lookup"><span data-stu-id="fdff2-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="fdff2-127">StorSimple 스냅숏 관리자 소프트웨어는 Windows 호스트에 상주 하며 관리자 hello 형태의 로컬 및 클라우드 스냅숏 StorSimple 장치의 toomanage 백업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="fdff2-128">장치를 StorSimple 스냅숏 관리자를 구성할 때 메시지가 표시 됩니다 tooprovide hello 장치 IP 주소와 암호 tooauthenticate 저장 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="fdff2-129">설정 하거나 hello Azure 포털을 통해 StorSimple 스냅숏 관리자에 대 한 hello 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="fdff2-130">다음 단계 tooset hello 하거나 hello StorSimple 스냅숏 관리자 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="fdff2-131">tooset hello StorSimple 스냅숏 관리자 암호</span><span class="sxs-lookup"><span data-stu-id="fdff2-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="fdff2-132">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="fdff2-133">장치의 hello 테이블 형식 목록에서 선택 하 고 hello 장치를 클릭 합니다. StorSimple 스냅숏 관리자 암호 tooset 또는 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="fdff2-134">Hello에 **설정** 블레이드에서 너무 이동**장치 설정 > 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="fdff2-135">Hello에 **보안 설정** 블레이드에서 클릭 **암호** tooset 또는 변경 hello StorSimple 스냅숏 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="fdff2-136">Hello에 **암호** 블레이드에서 암호는 14 자 또는 15 자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="fdff2-137">Hello 암호의 3 개 이상의 대문자, 소문자, 숫자 및 특수 문자의 조합이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="fdff2-138">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="fdff2-139">**저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="fdff2-140">이제 hello StorSimple 스냅숏 관리자 암호를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdff2-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fdff2-141">Next steps</span></span>
* <span data-ttu-id="fdff2-142">[StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="fdff2-143">[장치 구성을 수정](storsimple-8000-modify-device-config.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="fdff2-144">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fdff2-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

