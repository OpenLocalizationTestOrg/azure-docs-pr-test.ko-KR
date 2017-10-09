---
title: "StorSimple 장치 관리자를 통해 aaaChange 암호 | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 관리자 서비스 toochange StorSimple 스냅숏 관리자 및 장치 관리자 암호에 설명 합니다."
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
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="a2ffd-103">StorSimple Manager 서비스 toochange hello StorSimple 암호 사용</span><span class="sxs-lookup"><span data-stu-id="a2ffd-103">Use hello StorSimple Manager service toochange your StorSimple passwords</span></span>
## <a name="overview"></a><span data-ttu-id="a2ffd-104">개요</span><span class="sxs-lookup"><span data-stu-id="a2ffd-104">Overview</span></span>
<span data-ttu-id="a2ffd-105">Azure 클래식 포털 hello **구성** 페이지 StorSimple Manager 서비스에서 관리 되는 StorSimple 장치에는 다시 구성할 수 있는 모든 hello 장치 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-105">hello Azure classic portal **Configure** page contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Manager service.</span></span> <span data-ttu-id="a2ffd-106">이 자습서에서는 hello를 사용 하는 방법에 대해 설명 **구성** toochange 페이지 장치 관리자 또는 StorSimple 스냅숏 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-106">This tutorial explains how you can use hello **Configure** page toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="a2ffd-107">Hello 장치 관리자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="a2ffd-107">Change hello device administrator password</span></span>
<span data-ttu-id="a2ffd-108">Windows PowerShell 인터페이스 tooaccess hello StorSimple 장치를 사용 하 여 필요한 tooenter 장치 관리자 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="a2ffd-109">이 인터페이스에 대 한 hello 기본 암호는 서비스와 hello 첫 번째 StorSimple 장치를 등록 하는 경우 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="a2ffd-110">데이터의 hello 보안, 사용자가 필요한 toochange 때이 암호를 hello hello 등록 프로세스 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="a2ffd-111">이 암호를 변경 하지 않고 hello 등록 프로세스를 종료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="a2ffd-112">자세한 내용은 참조 [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="a2ffd-113">hello 설정 된 암호를 먼저 hello Windows PowerShell 인터페이스를 통해 등록 하는 동안 hello Azure 클래식 포털을 통해 다음 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-113">hello password that was first set through hello Windows PowerShell interface during registration can then be changed via hello Azure classic portal.</span></span> <span data-ttu-id="a2ffd-114">Hello 단계 toochange hello 장치 관리자 암호를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="a2ffd-115">toochange hello 장치 관리자 암호</span><span class="sxs-lookup"><span data-stu-id="a2ffd-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="a2ffd-116">Hello 클래식 포털에서 클릭 **장치** > **구성** 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-116">In hello classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="a2ffd-117">Toohello 아래로 스크롤하여 **장치 관리자 암호** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-117">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="a2ffd-118">8 too15 15 자 사이 포함 하는 관리자 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-118">Provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="a2ffd-119">hello 암호의 3 개 이상의 대문자, 소문자, 숫자 및 특수 문자 조합을 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-119">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="a2ffd-120">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-120">Confirm hello password.</span></span>
4. <span data-ttu-id="a2ffd-121">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-121">Click **Save** at hello bottom of hello page.</span></span>

<span data-ttu-id="a2ffd-122">이제 hello 장치 관리자 암호를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-122">hello device administrator password should now be updated.</span></span> <span data-ttu-id="a2ffd-123">이 수정 된 암호 tooaccess hello Windows PowerShell 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-123">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="change-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="a2ffd-124">Hello StorSimple 스냅숏 관리자 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-124">Change hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="a2ffd-125">StorSimple 스냅숏 관리자 소프트웨어는 Windows 호스트에 상주 하며 관리자 hello 형태의 로컬 및 클라우드 스냅숏 StorSimple 장치의 toomanage 백업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-125">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="a2ffd-126">장치를 StorSimple 스냅숏 관리자를 구성할 때 메시지가 표시 됩니다 tooprovide hello 장치 IP 주소와 암호 tooauthenticate 저장 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-126">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span> <span data-ttu-id="a2ffd-127">이 암호는 hello Windows PowerShell 인터페이스를 통해 처음 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-127">This password is first configured through hello Windows PowerShell interface.</span></span> <span data-ttu-id="a2ffd-128">자세한 내용은 참조 [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-128">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="a2ffd-129">hello 설정 된 암호를 먼저 hello Windows PowerShell 인터페이스를 통해 등록 하는 동안 hello 클래식 포털을 통해 다음 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-129">hello password that was first set through hello Windows PowerShell interface during registration can then be changed via hello classic portal.</span></span> <span data-ttu-id="a2ffd-130">Hello 단계 toochange hello StorSimple 스냅숏 관리자 암호를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-130">Perform hello following steps toochange hello StorSimple Snapshot Manager password.</span></span>

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="a2ffd-131">toochange hello StorSimple 스냅숏 관리자 암호</span><span class="sxs-lookup"><span data-stu-id="a2ffd-131">toochange hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="a2ffd-132">Hello 클래식 포털에서 클릭 **장치** > **구성** 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-132">In hello classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="a2ffd-133">Toohello 아래로 스크롤하여 **StorSimple 스냅숏 관리자** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-133">Scroll down toohello **StorSimple Snapshot Manager** section.</span></span> <span data-ttu-id="a2ffd-134">14자 또는 15자인 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-134">Enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="a2ffd-135">Hello 암호의 3 개 이상의 대문자, 소문자, 숫자 및 특수 문자의 조합이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-135">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="a2ffd-136">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-136">Confirm hello password.</span></span>
4. <span data-ttu-id="a2ffd-137">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-137">Click **Save** at hello bottom of hello page.</span></span>

<span data-ttu-id="a2ffd-138">이제 hello StorSimple 스냅숏 관리자 암호를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-138">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2ffd-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2ffd-139">Next steps</span></span>
* <span data-ttu-id="a2ffd-140">[StorSimple 보안](storsimple-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-140">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="a2ffd-141">[장치 구성을 수정](storsimple-modify-device-config.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-141">Learn more about [modifying your device configuration](storsimple-modify-device-config.md).</span></span>
* <span data-ttu-id="a2ffd-142">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ffd-142">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

