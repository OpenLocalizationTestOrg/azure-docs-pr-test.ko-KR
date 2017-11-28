---
title: "StorSimple 8000 시리즈 장치에 대한 CHAP 구성 | Microsoft Docs"
description: "StorSimple 장치에 CHAP(Challenge Handshake 인증 프로토콜)를 구성하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 36b4e73d0336deb9560d44163fc5330d1c9d775c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="6a9cb-103">StorSimple 장치에 대한 CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="6a9cb-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="6a9cb-104">이 자습서에서는 StorSimple 장치에 대한 CHAP를 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="6a9cb-105">이 문서에서 설명하는 절차는 StorSimple 1200 장치 뿐만 아니라 StorSimple 8000 시리즈에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="6a9cb-106">CHAP는 Challenge Handshake Authentication Protocol의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="6a9cb-107">CHAP는 서버에서 원격 클라이언트의 ID를 확인하는데 사용하는 인증 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="6a9cb-108">확인은 공유 암호 또는 암호를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="6a9cb-109">CHAP는 일방(단방향)이거나 상호적(양방향)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="6a9cb-110">단방향 CHAP는 대상이 초기자를 인증하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="6a9cb-111">반면에 상호 또는 역방향 CHAP는 대상이 초기자를 인증한 다음 초기자에서 대상을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="6a9cb-112">대상 인증 없이 초기자 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="6a9cb-113">그러나 초기자 인증도 구현하는 경우 대상 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="6a9cb-114">모범 사례로 CHAP를 사용하여 iSCSI 보안을 강화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="6a9cb-115">IPSEC는 StorSimple 장치에서 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="6a9cb-116">StorSimple 장치에서 CHAP 설정은 다음과 같은 방법으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="6a9cb-117">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="6a9cb-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="6a9cb-118">양방향 또는 상호 또는 역방향 인증</span><span class="sxs-lookup"><span data-stu-id="6a9cb-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="6a9cb-119">각 경우에서 장치 포털 및 서버 iSCSI 초기자 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="6a9cb-120">이 구성에 대한 자세한 단계는 다음 자습서에 설명되어있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="6a9cb-121">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="6a9cb-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="6a9cb-122">단방향 인증에서 대상이 초기자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="6a9cb-123">이 인증은 StorSimple 장치의 CHAP 초기자 설정 및 호스트의 iSCSI 초기자 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="6a9cb-124">StorSimple 장치 및 Windows 호스트에 대한 자세한 절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="6a9cb-125">단방향 인증에 대한 장치를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6a9cb-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="6a9cb-126">Azure 클래식 포털의 **장치** 페이지에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP 초기자](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="6a9cb-128">이 페이지에서 아래로 스크롤하고 **CHAP 초기자** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="6a9cb-129">CHAP 초기자에 대한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="6a9cb-130">CHAP 초기자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="6a9cb-131">CHAP 사용자 이름은 233 미만의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="6a9cb-132">CHAP 암호는 12 ~ 16 자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="6a9cb-133">더 긴 사용자 이름이나 암호를 사용하면 Windows 호스트에서 인증 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="6a9cb-134">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-134">Confirm the password.</span></span>
3. <span data-ttu-id="6a9cb-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-135">Click **Save**.</span></span> <span data-ttu-id="6a9cb-136">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="6a9cb-137">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="6a9cb-138">Windows 호스트 서버에서 일방 인증을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6a9cb-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="6a9cb-139">Windows 호스트 서버에서 iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="6a9cb-140">**iSCSI 초기자 속성** 창에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="6a9cb-141">**검색** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-141">Click the **Discovery** tab.</span></span>
      
       ![iSCSI 초기자 속성](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="6a9cb-143">**포털 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="6a9cb-144">**대상 포털 검색** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="6a9cb-145">장치의 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="6a9cb-146">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-146">Click **Advanced**.</span></span>
      
       ![대상 포털 검색](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="6a9cb-148">**고급 설정** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="6a9cb-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="6a9cb-149">**CHAP 로그온 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="6a9cb-150">**이름** 필드에 클래식 포털에서 CHAP 초기자에 지정한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="6a9cb-151">**대상 암호** 필드에 클래식 포털에서 CHAP 초기자에 지정한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="6a9cb-152">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-152">Click **OK**.</span></span>
      
       ![고급 설정 일반](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="6a9cb-154">**iSCSI 초기자 속성** 창의 **대상** 탭에서 장치 상태는 **Connected**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="6a9cb-155">StorSimple 1200 장치를 사용하는 경우 각 볼륨은 아래와 같이 iSCSI 대상으로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="6a9cb-156">따라서 3-4단계는 각 볼륨에 대해 반복해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![별도 대상으로 탑재된 볼륨](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="6a9cb-158">iSCSI 이름을 변경하는 경우 새 iSCSI 세션에 대한 새 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="6a9cb-159">새 설정은 로그오프하고 다시 로그온할 때까지 기존 세션에 대해 다시 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="6a9cb-160">Windows 호스트 서버에서 CHAP를 구성하는 방법에 대한 자세한 내용을 보려면 [추가 고려 사항](#additional-considerations)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="6a9cb-161">양방향 또는 상호 인증</span><span class="sxs-lookup"><span data-stu-id="6a9cb-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="6a9cb-162">양방향 인증에서 대상은 초기자를 인증한 다음 초기자는 대상을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="6a9cb-163">사용자가 CHAP 초기자 설정과 장치의 역방향 CHAP 설정 및 호스트의 iSCSI 초기자 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="6a9cb-164">다음 절차는 장치와 Windows 호스트에서 상호 인증을 구성하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="6a9cb-165">상호 인증에 대한 장치를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6a9cb-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="6a9cb-166">Azure 클래식 포털의 **장치** 페이지에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP 대상](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="6a9cb-168">이 페이지에서 아래로 스크롤하고 **CHAP 대상** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="6a9cb-169">장치에 대한 **역방향 CHAP 사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="6a9cb-170">장치에 대한 **역방향 CHAP 암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="6a9cb-171">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-171">Confirm the password.</span></span>
3. <span data-ttu-id="6a9cb-172">**CHAP 초기자** 섹션에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="6a9cb-173">장치에 대한 **사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="6a9cb-174">장치에 대한 **암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="6a9cb-175">암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-175">Confirm the password.</span></span>
4. <span data-ttu-id="6a9cb-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-176">Click **Save**.</span></span> <span data-ttu-id="6a9cb-177">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="6a9cb-178">**확인** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="6a9cb-179">Windows 호스트 서버에서 양방향 인증을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6a9cb-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="6a9cb-180">Windows 호스트 서버에서 iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="6a9cb-181">**iSCSI 초기자 속성** 창에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="6a9cb-182">**CHAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="6a9cb-183">**iSCSI 초기자 상호 CHAP 암호** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="6a9cb-184">Azure 클래식 포털에서 구성한 **역방향 CHAP 암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="6a9cb-185">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-185">Click **OK**.</span></span>
      
       ![iSCSI 초기자 상호 CHAP 암호](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="6a9cb-187">**대상** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="6a9cb-188">**연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="6a9cb-189">**대상에 연결** 대화 상자에서 **고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="6a9cb-190">**고급 속성** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="6a9cb-191">**CHAP 로그온 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="6a9cb-192">**이름** 필드에 클래식 포털에서 CHAP 초기자에 지정한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="6a9cb-193">**대상 암호** 필드에 클래식 포털에서 CHAP 초기자에 지정한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="6a9cb-194">**상호 인증 수행** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![고급 설정 상호 인증](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="6a9cb-196">**확인** 을 클릭하여 CHAP 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="6a9cb-197">Windows 호스트 서버에서 CHAP를 구성하는 방법에 대한 자세한 내용을 보려면 [추가 고려 사항](#additional-considerations)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="6a9cb-198">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6a9cb-198">Additional considerations</span></span>
<span data-ttu-id="6a9cb-199">**빠른 연결** 기능은 CHAP를 사용할 수 있는 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="6a9cb-200">CHAP를 사용하도록 설정한 경우 **대상** 탭에 있는 **연결** 단추를 사용하여 대상에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![대상에 연결](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="6a9cb-202">표시되는 **대상에 연결** 대화 상자에서 **즐겨찾는 대상 목록에 이 연결 추가** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="6a9cb-203">이렇게 하면 컴퓨터를 다시 시작할 때마다 iSCSI 즐겨찾는 대상에 연결을 복원하는 시도가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="6a9cb-204">구성 중 오류</span><span class="sxs-lookup"><span data-stu-id="6a9cb-204">Errors during configuration</span></span>
<span data-ttu-id="6a9cb-205">CHAP 구성이 올바르지 않은 경우 **인증 실패** 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="6a9cb-206">CHAP 구성 확인</span><span class="sxs-lookup"><span data-stu-id="6a9cb-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="6a9cb-207">다음 단계를 완료하여 CHAP가 사용되고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="6a9cb-208">CHAP 구성을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="6a9cb-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="6a9cb-209">**즐겨찾는 대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="6a9cb-210">인증을 사용하도록 설정한 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="6a9cb-211">**세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-211">Click **Details**.</span></span>
   
    ![iSCSI 초기자 속성 즐겨찾는 대상](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="6a9cb-213">**즐겨찾는 대상 세부 정보** 대화 상자에서 **인증** 필드에 항목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="6a9cb-214">구성이 성공하면 **CHAP**라는 텍스트가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![즐겨찾는 대상 세부 정보](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="6a9cb-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a9cb-216">Next steps</span></span>
* <span data-ttu-id="6a9cb-217">[StorSimple 보안](storsimple-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="6a9cb-218">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6a9cb-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

