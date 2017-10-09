---
title: "StorSimple 8000 시리즈 장치에 대 한 CHAP aaaConfigure | Microsoft Docs"
description: "StorSimple 장치에 tooconfigure Challenge Handshake 인증 프로토콜 CHAP () hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="1127e-103">StorSimple 장치에 대한 CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="1127e-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="1127e-104">이 자습서에서는 tooconfigure StorSimple 장치에 대 한 CHAP 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="1127e-105">이 문서에 자세히 설명 하는 hello 절차는 StorSimple 1200 장치 뿐만 아니라 tooStorSimple 8000 시리즈 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="1127e-106">CHAP는 Challenge Handshake Authentication Protocol의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="1127e-107">원격 클라이언트의 서버 toovalidate hello id에서 사용 하는 인증 체계 이며</span><span class="sxs-lookup"><span data-stu-id="1127e-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="1127e-108">hello 확인 공유 암호를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="1127e-109">CHAP는 일방(단방향)이거나 상호적(양방향)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="1127e-110">Hello 대상이 초기자를 인증할 때는 단방향 CHAP를 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="1127e-111">상호 / 역방향 CHAP hello에 다른 손 hello 초기자 hello 대상을 인증 하는 다음 한 hello 대상을 hello 초기자 인증을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="1127e-112">대상 인증 없이 초기자 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="1127e-113">그러나 초기자 인증도 구현하는 경우 대상 인증을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="1127e-114">모범 사례로, CHAP tooenhance iSCSI 보안을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="1127e-115">IPSEC는 StorSimple 장치에서 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="1127e-116">다음 방법으로 hello에 hello StorSimple 장치에서 CHAP 설정은 hello를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="1127e-117">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="1127e-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="1127e-118">양방향 또는 상호 또는 역방향 인증</span><span class="sxs-lookup"><span data-stu-id="1127e-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="1127e-119">각각의이 경우 hello 장치와 hello 서버 iSCSI 초기자 소프트웨어에 대 한 hello 포털 구성 toobe 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="1127e-120">hello이 구성에 대 한 자세한 단계는 hello 자습서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="1127e-121">단방향 또는 일방 인증</span><span class="sxs-lookup"><span data-stu-id="1127e-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="1127e-122">단방향 인증 hello 대상 hello 초기자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="1127e-123">이 인증 하려면 hello StorSimple 장치와 hello iSCSI 초기자 소프트웨어 hello 호스트에서 hello CHAP 초기자 설정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="1127e-124">StorSimple 장치에 대 한 자세한 절차 hello 및 Windows 호스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="1127e-125">tooconfigure 단방향 인증을 위해 장치</span><span class="sxs-lookup"><span data-stu-id="1127e-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="1127e-126">Hello hello에 Azure 클래식 포털에서에서 **장치** 페이지에서 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP 초기자](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="1127e-128">Hello 및이 페이지에서 아래로 스크롤하여 **CHAP 초기자** 섹션:</span><span class="sxs-lookup"><span data-stu-id="1127e-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="1127e-129">CHAP 초기자에 대한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="1127e-130">CHAP 초기자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="1127e-131">hello CHAP 사용자 이름에 보다 적은 233 자 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="1127e-132">hello CHAP 암호는 12 ~ 16 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="1127e-133">더 긴 사용자 이름이 나 암호가 hello Windows 호스트에서 인증 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="1127e-134">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-134">Confirm hello password.</span></span>
3. <span data-ttu-id="1127e-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-135">Click **Save**.</span></span> <span data-ttu-id="1127e-136">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="1127e-137">클릭 **확인** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="1127e-138">Windows hello에서 tooconfigure 단방향 인증 서버를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="1127e-139">Hello Windows 호스트 서버에서 hello iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="1127e-140">Hello에 **iSCSI 초기자 속성** 창의 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="1127e-141">Hello 클릭 **검색** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-141">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI 초기자 속성](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="1127e-143">**포털 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="1127e-144">Hello에 **대상 포털 검색** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="1127e-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="1127e-145">장치의 hello IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="1127e-146">**고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-146">Click **Advanced**.</span></span>
      
       ![대상 포털 검색](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="1127e-148">Hello에 **고급 설정** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="1127e-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="1127e-149">선택 hello **사용 CHAP 로그온 정보** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="1127e-150">Hello에 **이름** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="1127e-151">Hello에 **대상 암호** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="1127e-152">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-152">Click **OK**.</span></span>
      
       ![고급 설정 일반](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="1127e-154">Hello에 **대상** hello 탭 **iSCSI 초기자 속성** 창으로 hello 장치 상태를 표시 해야 **연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="1127e-155">StorSimple 1200 장치를 사용하는 경우 각 볼륨은 아래와 같이 iSCSI 대상으로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="1127e-156">따라서 3-4 단계 toobe 각 볼륨에 대해 반복 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![별도 대상으로 탑재된 볼륨](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="1127e-158">Hello iSCSI 이름을 변경 하면 새 iSCSI 세션에 대 한 hello 새 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="1127e-159">새 설정은 로그오프하고 다시 로그온할 때까지 기존 세션에 대해 다시 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="1127e-160">너무 hello Windows 호스트 서버에서 CHAP를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[추가 고려 사항](#additional-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="1127e-161">양방향 또는 상호 인증</span><span class="sxs-lookup"><span data-stu-id="1127e-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="1127e-162">양방향 인증에서는 hello 대상 hello 초기자를 인증 한 hello 초기자 인증 hello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="1127e-163">이 hello 장치와 iSCSI 초기자 소프트웨어 hello 호스트에 대 한 역방향 CHAP 설정은 hello 뿐만 아니라 hello 사용자 tooconfigure hello CHAP 초기자 설정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="1127e-164">hello 다음 절차에서는 설명 hello 단계 tooconfigure 상호 인증 hello Windows 호스트와 hello 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="1127e-165">tooconfigure 상호 인증을 위해 장치</span><span class="sxs-lookup"><span data-stu-id="1127e-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="1127e-166">Hello hello에 Azure 클래식 포털에서에서 **장치** 페이지에서 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP 대상](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="1127e-168">Hello 및이 페이지에서 아래로 스크롤하여 **CHAP 대상** 섹션:</span><span class="sxs-lookup"><span data-stu-id="1127e-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="1127e-169">장치에 대한 **역방향 CHAP 사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="1127e-170">장치에 대한 **역방향 CHAP 암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="1127e-171">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-171">Confirm hello password.</span></span>
3. <span data-ttu-id="1127e-172">Hello에 **CHAP 초기자** 섹션:</span><span class="sxs-lookup"><span data-stu-id="1127e-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="1127e-173">장치에 대한 **사용자 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="1127e-174">장치에 대한 **암호** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="1127e-175">Hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-175">Confirm hello password.</span></span>
4. <span data-ttu-id="1127e-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-176">Click **Save**.</span></span> <span data-ttu-id="1127e-177">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="1127e-178">클릭 **확인** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="1127e-179">Windows hello에서 tooconfigure 양방향 인증 서버를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="1127e-180">Hello Windows 호스트 서버에서 hello iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="1127e-181">Hello에 **iSCSI 초기자 속성** 창의 hello 클릭 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="1127e-182">**CHAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="1127e-183">Hello에 **iSCSI 초기자 상호 CHAP 암호** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="1127e-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="1127e-184">형식 hello **역방향 CHAP 암호** hello Azure 클래식 포털에에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="1127e-185">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-185">Click **OK**.</span></span>
      
       ![iSCSI 초기자 상호 CHAP 암호](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="1127e-187">Hello 클릭 **대상** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="1127e-188">Hello 클릭 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="1127e-189">Hello에 **tooTarget 연결** 대화 상자를 클릭 **고급**합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="1127e-190">Hello에 **고급 속성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="1127e-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="1127e-191">선택 hello **사용 CHAP 로그온 정보** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="1127e-192">Hello에 **이름** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="1127e-193">Hello에 **대상 암호** 필드, hello 클래식 포털의 hello CHAP 초기자에 대해 지정한 공급 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="1127e-194">선택 hello **상호 인증 수행** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![고급 설정 상호 인증](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="1127e-196">클릭 **확인** toocomplete hello CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="1127e-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="1127e-197">너무 hello Windows 호스트 서버에서 CHAP를 구성 하는 방법에 대 한 자세한 내용을 보려면 이동[추가 고려 사항](#additional-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="1127e-198">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="1127e-198">Additional considerations</span></span>
<span data-ttu-id="1127e-199">hello **빠른 연결** 기능은 CHAP를 사용할 수 있는 연결을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="1127e-200">CHAP를 사용 하는 hello를 사용 하는지 확인 **연결** hello에서 사용할 수 있는 단추 **대상** 탭 tooconnect tooa 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Tootarget 연결](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="1127e-202">Hello에 **tooTarget 연결** 대화 상자는 선택에 나타난 hello **즐겨 찾는 대상의 연결 toohello 목록이 추가** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="1127e-203">이렇게 하면는 hello 컴퓨터를 다시 시작 될 때마다 하려고 toorestore hello 연결 toohello iSCSI 즐겨찾기 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="1127e-204">구성 중 오류</span><span class="sxs-lookup"><span data-stu-id="1127e-204">Errors during configuration</span></span>
<span data-ttu-id="1127e-205">CHAP 구성이 올바르지 않을 경우 가능성이 toosee 됩니다는 **인증 실패** 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="1127e-206">CHAP 구성 확인</span><span class="sxs-lookup"><span data-stu-id="1127e-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="1127e-207">CHAP hello 다음 단계를 완료 하 여 사용 되 고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="1127e-208">tooverify CHAP 구성</span><span class="sxs-lookup"><span data-stu-id="1127e-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="1127e-209">**즐겨찾는 대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="1127e-210">인증 사용 하도록 설정한 hello 대상을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="1127e-211">**세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-211">Click **Details**.</span></span>
   
    ![iSCSI 초기자 속성 즐겨찾는 대상](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="1127e-213">Hello에 **즐겨 찾는 대상 세부 정보** 대화 상자, hello에 메모 hello 항목 **인증** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="1127e-214">경우 hello 구성에 성공 했는지를 필드 **CHAP**합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![즐겨찾는 대상 세부 정보](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="1127e-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1127e-216">Next steps</span></span>
* <span data-ttu-id="1127e-217">[StorSimple 보안](storsimple-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="1127e-218">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1127e-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

