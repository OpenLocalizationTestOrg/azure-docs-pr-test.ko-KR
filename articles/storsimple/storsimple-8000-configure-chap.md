---
title: "StorSimple 8000 시리즈 장치에 대한 CHAP 구성 | Microsoft Docs"
description: "StorSimple 장치에 CHAP(Challenge Handshake 인증 프로토콜)를 구성하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 61e0877187759d76b6f7efcef0a5ed8bec8500fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="97e24-103">StorSimple 장치에 대한 CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="97e24-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="97e24-104">이 자습서에서는 StorSimple 장치에 대한 CHAP를 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="97e24-105">이 문서에서 설명하는 절차는 StorSimple 8000 시리즈 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-105">The procedure detailed in this article applies to StorSimple 8000 series devices.</span></span>

<span data-ttu-id="97e24-106">CHAP는 Challenge Handshake Authentication Protocol의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="97e24-107">CHAP는 서버에서 원격 클라이언트의 ID를 확인하는데 사용하는 인증 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="97e24-108">확인은 공유 암호 또는 암호를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="97e24-109">CHAP는 일방(단방향)이거나 상호적(양방향)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="97e24-110">단방향 CHAP는 대상이 초기자를 인증하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-110">One way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="97e24-111">상호 또는 역방향 CHAP는 대상이 초기자를 인증한 다음 초기자가 대상을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-111">In mutual or reverse CHAP, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="97e24-112">대상 인증 없이 초기자 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="97e24-113">그러나 초기자 인증도 구현하는 경우 대상 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="97e24-114">모범 사례로 CHAP를 사용하여 iSCSI 보안을 강화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="97e24-115">IPSEC는 StorSimple 장치에서 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="97e24-116">StorSimple 장치에서 CHAP 설정은 다음과 같은 방법으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="97e24-117">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="97e24-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="97e24-118">양방향 또는 상호 또는 역방향 인증</span><span class="sxs-lookup"><span data-stu-id="97e24-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="97e24-119">각 경우에서 장치 포털 및 서버 iSCSI 초기자 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="97e24-120">이 구성에 대한 자세한 단계는 다음 자습서에 설명되어있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="97e24-121">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="97e24-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="97e24-122">단방향 인증에서 대상이 초기자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="97e24-123">이 인증은 StorSimple 장치의 CHAP 초기자 설정 및 호스트의 iSCSI 초기자 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="97e24-124">StorSimple 장치 및 Windows 호스트에 대한 자세한 절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="97e24-125">단방향 인증에 대한 장치를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="97e24-125">To configure your device for one-way authentication</span></span>

1. <span data-ttu-id="97e24-126">Azure Portal에서 StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-126">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="97e24-127">**장치**를 클릭하고 CHAP를 구성하려는 장치를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-127">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="97e24-128">**장치 설정 > 보안**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-128">Go to **Device settings > Security**.</span></span> <span data-ttu-id="97e24-129">**보안 설정** 블레이드에서 **CHAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-129">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="97e24-131">**CHAP** 블레이드의 **CHAP 초기자** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-131">In the **CHAP** blade, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="97e24-132">CHAP 초기자에 대한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="97e24-133">CHAP 초기자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="97e24-134">CHAP 사용자 이름은 233 미만의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-134">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="97e24-135">CHAP 암호는 12 ~ 16 자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-135">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="97e24-136">더 긴 사용자 이름이나 암호를 사용하면 Windows 호스트에서 인증 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-136">A longer user name or password results in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="97e24-137">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-137">Confirm the password.</span></span>

       ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="97e24-139">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-139">Click **Save**.</span></span> <span data-ttu-id="97e24-140">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-140">A confirmation message is displayed.</span></span> <span data-ttu-id="97e24-141">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-141">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="97e24-142">Windows 호스트 서버에서 일방 인증을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="97e24-142">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="97e24-143">Windows 호스트 서버에서 iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-143">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="97e24-144">**iSCSI 초기자 속성** 창에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-144">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="97e24-145">**검색** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-145">Click the **Discovery** tab.</span></span>
      
       ![iSCSI 초기자 속성](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="97e24-147">**포털 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="97e24-148">**대상 포털 검색** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-148">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="97e24-149">장치의 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-149">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="97e24-150">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-150">Click **Advanced**.</span></span>
      
       ![대상 포털 검색](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="97e24-152">**고급 설정** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="97e24-152">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="97e24-153">**CHAP 로그온 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-153">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="97e24-154">**이름** 필드에 클래식 포털에서 CHAP 초기자에 지정한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-154">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="97e24-155">**대상 암호** 필드에 클래식 포털에서 CHAP 초기자에 지정한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-155">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="97e24-156">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-156">Click **OK**.</span></span>
      
       ![고급 설정 일반](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="97e24-158">**iSCSI 초기자 속성** 창의 **대상** 탭에서 장치 상태는 **Connected**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-158">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="97e24-159">StorSimple 1200 장치를 사용하는 경우 각 볼륨은 iSCSI 대상으로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="97e24-160">따라서 3-4단계는 각 볼륨에 대해 반복해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-160">Hence, steps 3-4 will need to be repeated for each volume.</span></span>
   
    ![별도 대상으로 탑재된 볼륨](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="97e24-162">iSCSI 이름을 변경하는 경우 새 iSCSI 세션에 대한 새 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-162">If you change the iSCSI name, the new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="97e24-163">새 설정은 로그오프하고 다시 로그온할 때까지 기존 세션에 대해 다시 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="97e24-164">Windows 호스트 서버에서 CHAP를 구성하는 방법에 대한 자세한 내용을 보려면 [추가 고려 사항](#additional-considerations)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="97e24-164">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="97e24-165">양방향 또는 상호 인증</span><span class="sxs-lookup"><span data-stu-id="97e24-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="97e24-166">양방향 인증에서 대상은 초기자를 인증한 다음 초기자는 대상을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-166">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="97e24-167">이 절차를 수행하려면 사용자가 CHAP 초기자 설정과 장치의 역방향 CHAP 설정 및 호스트의 iSCSI 초기자 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-167">This procedure requires the user to configure the CHAP initiator settings, reverse CHAP settings on the device, and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="97e24-168">다음 절차는 장치와 Windows 호스트에서 상호 인증을 구성하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-168">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="97e24-169">상호 인증에 대한 장치를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="97e24-169">To configure your device for mutual authentication</span></span>

1. <span data-ttu-id="97e24-170">Azure Portal에서 StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-170">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="97e24-171">**장치**를 클릭하고 CHAP를 구성하려는 장치를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-171">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="97e24-172">**장치 설정 > 보안**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-172">Go to **Device settings > Security**.</span></span> <span data-ttu-id="97e24-173">**보안 설정** 블레이드에서 **CHAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-173">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 대상](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="97e24-175">이 페이지에서 아래로 스크롤하고 **CHAP 대상** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-175">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="97e24-176">장치에 대한 **역방향 CHAP 사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="97e24-177">장치에 대한 **역방향 CHAP 암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="97e24-178">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-178">Confirm the password.</span></span>
3. <span data-ttu-id="97e24-179">**CHAP 초기자** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-179">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="97e24-180">장치에 대한 **사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="97e24-181">장치에 대한 **암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="97e24-182">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-182">Confirm the password.</span></span>

       ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="97e24-184">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-184">Click **Save**.</span></span> <span data-ttu-id="97e24-185">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-185">A confirmation message is displayed.</span></span> <span data-ttu-id="97e24-186">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-186">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="97e24-187">Windows 호스트 서버에서 양방향 인증을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="97e24-187">To configure bidirectional authentication on the Windows host server</span></span>

1. <span data-ttu-id="97e24-188">Windows 호스트 서버에서 iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-188">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="97e24-189">**iSCSI 초기자 속성** 창에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-189">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="97e24-190">**CHAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="97e24-191">**iSCSI 초기자 상호 CHAP 암호** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-191">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="97e24-192">Azure Portal에서 구성한 **역방향 CHAP 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-192">Type the **Reverse CHAP Password** that you configured in the Azure portal.</span></span>
   2. <span data-ttu-id="97e24-193">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-193">Click **OK**.</span></span>
      
       ![iSCSI 초기자 상호 CHAP 암호](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="97e24-195">**대상** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-195">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="97e24-196">**연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-196">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="97e24-197">**대상에 연결** 대화 상자에서 **고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-197">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="97e24-198">**고급 속성** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-198">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="97e24-199">**CHAP 로그온 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-199">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="97e24-200">**이름** 필드에 클래식 포털에서 CHAP 초기자에 지정한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-200">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="97e24-201">**대상 암호** 필드에 클래식 포털에서 CHAP 초기자에 지정한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-201">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="97e24-202">**상호 인증 수행** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-202">Select the **Perform mutual authentication** check box.</span></span>
      
       ![고급 설정 상호 인증](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="97e24-204">**확인** 을 클릭하여 CHAP 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-204">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="97e24-205">Windows 호스트 서버에서 CHAP를 구성하는 방법에 대한 자세한 내용을 보려면 [추가 고려 사항](#additional-considerations)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="97e24-205">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="97e24-206">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="97e24-206">Additional considerations</span></span>

<span data-ttu-id="97e24-207">**빠른 연결** 기능은 CHAP를 사용할 수 있는 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-207">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="97e24-208">CHAP를 사용하도록 설정한 경우 **대상** 탭에 있는 **연결** 단추를 사용하여 대상에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-208">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![대상에 연결](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="97e24-210">표시되는 **대상에 연결** 대화 상자에서 **즐겨찾는 대상 목록에 이 연결 추가** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-210">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="97e24-211">이렇게 선택하면 컴퓨터를 다시 시작할 때마다 iSCSI 즐겨찾는 대상에 연결을 복원하는 시도가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-211">This selection ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="97e24-212">구성 중 오류</span><span class="sxs-lookup"><span data-stu-id="97e24-212">Errors during configuration</span></span>

<span data-ttu-id="97e24-213">CHAP 구성이 올바르지 않은 경우 **인증 실패** 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-213">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="97e24-214">CHAP 구성 확인</span><span class="sxs-lookup"><span data-stu-id="97e24-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="97e24-215">다음 단계를 완료하여 CHAP가 사용되고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-215">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="97e24-216">CHAP 구성을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="97e24-216">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="97e24-217">**즐겨찾는 대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="97e24-218">인증을 사용하도록 설정한 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-218">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="97e24-219">**세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-219">Click **Details**.</span></span>
   
    ![iSCSI 초기자 속성 즐겨찾는 대상](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="97e24-221">**즐겨찾는 대상 세부 정보** 대화 상자에서 **인증** 필드에 항목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-221">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="97e24-222">구성이 성공하면 **CHAP**라는 텍스트가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-222">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![즐겨찾는 대상 세부 정보](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="97e24-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97e24-224">Next steps</span></span>

* <span data-ttu-id="97e24-225">[StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="97e24-226">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="97e24-226">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

