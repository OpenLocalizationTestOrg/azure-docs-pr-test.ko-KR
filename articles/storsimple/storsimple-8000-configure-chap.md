---
title: "StorSimple 8000 시리즈 장치에 대 한 CHAP aaaConfigure | Microsoft Docs"
description: "StorSimple 장치에 tooconfigure Challenge Handshake 인증 프로토콜 CHAP () hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="91289-103">StorSimple 장치에 대한 CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="91289-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="91289-104">이 자습서에서는 tooconfigure StorSimple 장치에 대 한 CHAP 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="91289-105">이 문서에 자세히 설명 하는 hello 프로시저는 tooStorSimple 8000 시리즈 장치에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91289-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="91289-106">CHAP는 Challenge Handshake Authentication Protocol의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="91289-107">원격 클라이언트의 서버 toovalidate hello id에서 사용 하는 인증 체계 이며</span><span class="sxs-lookup"><span data-stu-id="91289-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="91289-108">hello 확인 공유 암호를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="91289-109">CHAP는 일방(단방향)이거나 상호적(양방향)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="91289-110">단방향 CHAP는 hello 대상은 초기자를 인증 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="91289-111">상호 / 역방향 CHAP의 hello 대상 hello 초기자를 인증 한 hello 초기자 인증 hello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="91289-112">대상 인증 없이 초기자 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="91289-113">그러나 초기자 인증도 구현하는 경우 대상 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="91289-114">모범 사례로, CHAP tooenhance iSCSI 보안을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="91289-115">IPSEC는 StorSimple 장치에서 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="91289-116">다음 방법으로 hello에 hello StorSimple 장치에서 CHAP 설정은 hello를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="91289-117">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="91289-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="91289-118">양방향 또는 상호 또는 역방향 인증</span><span class="sxs-lookup"><span data-stu-id="91289-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="91289-119">각각의이 경우 hello 장치와 hello 서버 iSCSI 초기자 소프트웨어에 대 한 hello 포털 구성 toobe 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="91289-120">hello이 구성에 대 한 자세한 단계는 hello 자습서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="91289-121">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="91289-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="91289-122">단방향 인증 hello 대상 hello 초기자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="91289-123">이 인증 하려면 hello StorSimple 장치와 hello iSCSI 초기자 소프트웨어 hello 호스트에서 hello CHAP 초기자 설정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="91289-124">StorSimple 장치에 대 한 자세한 절차 hello 및 Windows 호스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="91289-125">tooconfigure 단방향 인증을 위해 장치</span><span class="sxs-lookup"><span data-stu-id="91289-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="91289-126">Azure 포털 hello tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="91289-127">클릭 **장치** 선택 하 고 클릭 tooconfigure CHAP는 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="91289-128">너무 이동**장치 설정 > 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="91289-129">Hello에 **보안 설정** 블레이드에서 클릭 **CHAP**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="91289-131">Hello에 **CHAP** 블레이드 및 hello **CHAP 초기자** 섹션:</span><span class="sxs-lookup"><span data-stu-id="91289-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="91289-132">CHAP 초기자에 대한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="91289-133">CHAP 초기자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="91289-134">hello CHAP 사용자 이름에 보다 적은 233 자 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="91289-135">hello CHAP 암호는 12 ~ 16 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="91289-136">더 긴 사용자 이름이 나 암호가 hello Windows 호스트에서 인증 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="91289-137">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-137">Confirm hello password.</span></span>

       ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="91289-139">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-139">Click **Save**.</span></span> <span data-ttu-id="91289-140">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91289-140">A confirmation message is displayed.</span></span> <span data-ttu-id="91289-141">클릭 **확인** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="91289-142">Windows hello에서 tooconfigure 단방향 인증 서버를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="91289-143">Hello Windows 호스트 서버에서 hello iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="91289-144">Hello에 **iSCSI 초기자 속성** 창의 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="91289-145">Hello 클릭 **검색** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-145">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI 초기자 속성](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="91289-147">**포털 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="91289-148">Hello에 **대상 포털 검색** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="91289-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="91289-149">장치의 hello IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="91289-150">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-150">Click **Advanced**.</span></span>
      
       ![대상 포털 검색](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="91289-152">Hello에 **고급 설정** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="91289-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="91289-153">선택 hello **사용 CHAP 로그온 정보** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="91289-154">Hello에 **이름** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="91289-155">Hello에 **대상 암호** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="91289-156">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-156">Click **OK**.</span></span>
      
       ![고급 설정 일반](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="91289-158">Hello에 **대상** hello 탭 **iSCSI 초기자 속성** 창으로 hello 장치 상태를 표시 해야 **연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="91289-159">StorSimple 1200 장치를 사용하는 경우 각 볼륨은 iSCSI 대상으로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="91289-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="91289-160">따라서 3-4 단계 toobe 각 볼륨에 대해 반복 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![별도 대상으로 탑재된 볼륨](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="91289-162">Hello iSCSI 이름을 변경 하면 새 iSCSI 세션에 대 한 hello 새 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91289-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="91289-163">새 설정은 로그오프하고 다시 로그온할 때까지 기존 세션에 대해 다시 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="91289-164">너무 hello Windows 호스트 서버에서 CHAP를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[추가 고려 사항](#additional-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="91289-165">양방향 또는 상호 인증</span><span class="sxs-lookup"><span data-stu-id="91289-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="91289-166">양방향 인증에서는 hello 대상 hello 초기자를 인증 한 hello 초기자 인증 hello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="91289-167">이 절차를 수행 하려면 hello 사용자 tooconfigure hello CHAP 초기자 설정을, hello 장치와 iSCSI 초기자 소프트웨어 hello 호스트에서 CHAP 설정을 반대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="91289-168">hello 다음 절차에서는 설명 hello 단계 tooconfigure 상호 인증 hello Windows 호스트와 hello 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="91289-169">tooconfigure 상호 인증을 위해 장치</span><span class="sxs-lookup"><span data-stu-id="91289-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="91289-170">Azure 포털 hello tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="91289-171">클릭 **장치** 선택 하 고 클릭 tooconfigure CHAP는 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="91289-172">너무 이동**장치 설정 > 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="91289-173">Hello에 **보안 설정** 블레이드에서 클릭 **CHAP**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 대상](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="91289-175">Hello 및이 페이지에서 아래로 스크롤하여 **CHAP 대상** 섹션:</span><span class="sxs-lookup"><span data-stu-id="91289-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="91289-176">장치에 대한 **역방향 CHAP 사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="91289-177">장치에 대한 **역방향 CHAP 암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="91289-178">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-178">Confirm hello password.</span></span>
3. <span data-ttu-id="91289-179">Hello에 **CHAP 초기자** 섹션:</span><span class="sxs-lookup"><span data-stu-id="91289-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="91289-180">장치에 대한 **사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="91289-181">장치에 대한 **암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="91289-182">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-182">Confirm hello password.</span></span>

       ![CHAP 초기자](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="91289-184">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-184">Click **Save**.</span></span> <span data-ttu-id="91289-185">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91289-185">A confirmation message is displayed.</span></span> <span data-ttu-id="91289-186">클릭 **확인** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="91289-187">Windows hello에서 tooconfigure 양방향 인증 서버를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="91289-188">Hello Windows 호스트 서버에서 hello iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="91289-189">Hello에 **iSCSI 초기자 속성** 창의 hello 클릭 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="91289-190">**CHAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="91289-191">Hello에 **iSCSI 초기자 상호 CHAP 암호** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="91289-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="91289-192">형식 hello **역방향 CHAP 암호** hello Azure 포털에에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="91289-193">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-193">Click **OK**.</span></span>
      
       ![iSCSI 초기자 상호 CHAP 암호](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="91289-195">Hello 클릭 **대상** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="91289-196">Hello 클릭 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="91289-197">Hello에 **tooTarget 연결** 대화 상자를 클릭 **고급**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="91289-198">Hello에 **고급 속성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="91289-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="91289-199">선택 hello **사용 CHAP 로그온 정보** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="91289-200">Hello에 **이름** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="91289-201">Hello에 **대상 암호** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="91289-202">선택 hello **상호 인증 수행** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![고급 설정 상호 인증](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="91289-204">클릭 **확인** toocomplete hello CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="91289-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="91289-205">너무 hello Windows 호스트 서버에서 CHAP를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[추가 고려 사항](#additional-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="91289-206">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="91289-206">Additional considerations</span></span>

<span data-ttu-id="91289-207">hello **빠른 연결** 기능은 CHAP를 사용할 수 있는 연결을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="91289-208">CHAP를 사용 하는 hello를 사용 하는지 확인 **연결** hello에서 사용할 수 있는 단추 **대상** 탭 tooconnect tooa 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Tootarget 연결](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="91289-210">Hello에 **tooTarget 연결** 대화 상자는 선택에 나타난 hello **즐겨 찾는 대상의 연결 toohello 목록이 추가** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="91289-211">이 옵션을이 선택 하 hello 컴퓨터를 다시 시작 될 때마다 하려고 toorestore hello 연결 toohello iSCSI 즐겨찾기 대상 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="91289-212">구성 중 오류</span><span class="sxs-lookup"><span data-stu-id="91289-212">Errors during configuration</span></span>

<span data-ttu-id="91289-213">CHAP 구성이 올바르지 않을 경우 가능성이 toosee 됩니다는 **인증 실패** 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="91289-214">CHAP 구성 확인</span><span class="sxs-lookup"><span data-stu-id="91289-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="91289-215">CHAP hello 다음 단계를 완료 하 여 사용 되 고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91289-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="91289-216">tooverify CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="91289-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="91289-217">**즐겨찾는 대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="91289-218">인증 사용 하도록 설정한 hello 대상을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="91289-219">**세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-219">Click **Details**.</span></span>
   
    ![iSCSI 초기자 속성 즐겨찾는 대상](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="91289-221">Hello에 **즐겨 찾는 대상 세부 정보** 대화 상자, hello에 메모 hello 항목 **인증** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="91289-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="91289-222">경우 hello 구성에 성공 했는지를 필드 **CHAP**합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![즐겨찾는 대상 세부 정보](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="91289-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91289-224">Next steps</span></span>

* <span data-ttu-id="91289-225">[StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91289-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="91289-226">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91289-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

