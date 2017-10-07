---
title: "Azure StorSimple 가상 배열 iSCSI 서버 설치 프로그램 aaaMicrosoft | Microsoft Docs"
description: "초기 설정 tooperform StorSimple iSCSI 서버를 등록 하 고 장치 설치를 완료 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a><span data-ttu-id="e21dc-103">StorSimple 가상 배열 배포 – Azure Portal을 통해 iSCSI 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="e21dc-103">Deploy StorSimple Virtual Array – Set up as an iSCSI server via Azure portal</span></span>

![iscsi 설정 프로세스 흐름](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a><span data-ttu-id="e21dc-105">개요</span><span class="sxs-lookup"><span data-stu-id="e21dc-105">Overview</span></span>

<span data-ttu-id="e21dc-106">이 배포 자습서에는 Microsoft Azure StorSimple 가상 배열 toohello 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-106">This deployment tutorial applies toohello Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="e21dc-107">이 자습서에서는 방법 tooperform hello 초기 설정 완료 hello 장치 설치 StorSimple iSCSI 서버를 등록 하 고 다음 만들기, 탑재, 초기화 및 포맷 iSCSI 서버로 구성 된 StorSimple 가상 배열에 있는 볼륨을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-107">This tutorial describes how tooperform hello initial setup, register your StorSimple iSCSI server, complete hello device setup, and then create, mount, initialize, and format volumes on your StorSimple Virtual Array configured as an iSCSI server.</span></span> 

<span data-ttu-id="e21dc-108">여기 설명 된 hello 절차 too1 시간 toocomplete 약 30 분을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-108">hello procedures described here take approximately 30 minutes too1 hour toocomplete.</span></span> <span data-ttu-id="e21dc-109">이 문서에서 게시 하는 hello 정보에는 가상 배열 tooStorSimple 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-109">hello information published in this article applies tooStorSimple Virtual Arrays only.</span></span>

## <a name="setup-prerequisites"></a><span data-ttu-id="e21dc-110">설정 필수 조건</span><span class="sxs-lookup"><span data-stu-id="e21dc-110">Setup prerequisites</span></span>

<span data-ttu-id="e21dc-111">StorSimple 가상 배열을 구성하고 설정하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-111">Before you configure and set up your StorSimple Virtual Array, make sure that:</span></span>

* <span data-ttu-id="e21dc-112">가상 배열 사용자를 프로 비전 하 고에 설명 된 대로 tooit 연결 [배포 StorSimple 가상 배열-프로 비전 Hyper-v에서 가상 배열](storsimple-ova-deploy2-provision-hyperv.md) 또는 [배포 StorSimple 가상 배열-VMware에 가상 배열 프로 비전 ](storsimple-virtual-array-deploy2-provision-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="e21dc-112">You have provisioned a virtual array and connected tooit as described in [Deploy StorSimple Virtual Array - Provision a virtual array in Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array  - Provision a virtual array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
* <span data-ttu-id="e21dc-113">Hello 하 여 만든 toomanage StorSimple 가상 배열 StorSimple 장치 관리자 서비스에서에서 서비스 등록 키 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-113">You have hello service registration key from hello StorSimple Device Manager service that you created toomanage your StorSimple Virtual Arrays.</span></span> <span data-ttu-id="e21dc-114">자세한 내용은 참조 **2 단계: Get hello 서비스 등록 키** 에 [배포 StorSimple 가상 배열-hello 포털 준비](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-114">For more information, see **Step 2: Get hello service registration key** in [Deploy StorSimple Virtual Array - Prepare hello portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
* <span data-ttu-id="e21dc-115">Hello 두 번째 또는 그 가상 배열 기존 StorSimple 장치 관리자 서비스를 사용 하 여 등록 된 경우에 hello 서비스 데이터 암호화 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-115">If this is hello second or subsequent virtual array that you are registering with an existing StorSimple Device Manager service, you should have hello service data encryption key.</span></span> <span data-ttu-id="e21dc-116">첫 번째 장치 hello가이 서비스와 성공적으로 등록 될 때이 키가 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-116">This key was generated when hello first device was successfully registered with this service.</span></span> <span data-ttu-id="e21dc-117">이 키를 잃어버린 경우 참조 **Get hello 서비스 데이터 암호화 키** 에 [사용 하 여 hello 웹 UI tooadminister StorSimple 가상 배열](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-117">If you have lost this key, see **Get hello service data encryption key** in [Use hello Web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).</span></span>

## <a name="step-by-step-setup"></a><span data-ttu-id="e21dc-118">단계별 설정</span><span class="sxs-lookup"><span data-stu-id="e21dc-118">Step-by-step setup</span></span>

<span data-ttu-id="e21dc-119">단계별 지침은 tooset 이후의 hello를 사용 하 고 StorSimple 가상 배열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-119">Use hello following step-by-step instructions tooset up and configure your StorSimple Virtual Array:</span></span>

* [<span data-ttu-id="e21dc-120">1 단계: hello 로컬 웹 UI 설치를 완료 하 고 장치 등록</span><span class="sxs-lookup"><span data-stu-id="e21dc-120">Step 1: Complete hello local web UI setup and register your device</span></span>](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [<span data-ttu-id="e21dc-121">2 단계: 전체 hello 필요한 장치 설치</span><span class="sxs-lookup"><span data-stu-id="e21dc-121">Step 2: Complete hello required device setup</span></span>](#step-2-complete-the-required-device-setup)
* [<span data-ttu-id="e21dc-122">3단계: 볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="e21dc-122">Step 3: Add a volume</span></span>](#step-3-add-a-volume)
* [<span data-ttu-id="e21dc-123">4단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="e21dc-123">Step 4: Mount, initialize, and format a volume</span></span>](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a><span data-ttu-id="e21dc-124">1 단계: hello 로컬 웹 UI 설치를 완료 하 고 장치 등록</span><span class="sxs-lookup"><span data-stu-id="e21dc-124">Step 1: Complete hello local web UI setup and register your device</span></span>

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a><span data-ttu-id="e21dc-125">toocomplete 설치 hello 및 hello 장치 등록</span><span class="sxs-lookup"><span data-stu-id="e21dc-125">toocomplete hello setup and register hello device</span></span>

1. <span data-ttu-id="e21dc-126">브라우저 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-126">Open a browser window.</span></span> <span data-ttu-id="e21dc-127">tooconnect toohello 웹 UI 형식:</span><span class="sxs-lookup"><span data-stu-id="e21dc-127">tooconnect toohello web UI type:</span></span>
   
    `https://<ip-address of network interface>`
   
    <span data-ttu-id="e21dc-128">Hello 이전 단계에서 설명 하는 hello 연결 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-128">Use hello connection URL noted in hello previous step.</span></span> <span data-ttu-id="e21dc-129">Hello 웹 사이트의 보안 인증서에 문제가 있다는 것을 알리는 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-129">You will see an error notifying you that there is a problem with hello website’s security certificate.</span></span> <span data-ttu-id="e21dc-130">클릭 **계속 toothis 웹 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-130">Click **Continue toothis web page**.</span></span>
   
    ![보안 인증서 오류](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. <span data-ttu-id="e21dc-132">Toohello 로그인 웹 UI로 하려면 가상 장치의 **StorSimpleAdmin**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-132">Sign in toohello web UI of your virtual device as **StorSimpleAdmin**.</span></span> <span data-ttu-id="e21dc-133">3 단계에서에서 사용자가 변경한 hello 장치 관리자 암호를 입력: 시작 hello 가상 장치에서 [배포 StorSimple 가상 배열-Hyper-v에서 가상 장치 프로 비전](storsimple-virtual-array-deploy2-provision-hyperv.md) 또는 [배포 StorSimple 가상 배열- VMware에 가상 장치를 프로 비전](storsimple-virtual-array-deploy2-provision-vmware.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-133">Enter hello device administrator password that you changed in Step 3: Start hello virtual device in [Deploy StorSimple Virtual Array - Provision a virtual device in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array - Provision a virtual device in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
   
    ![로그인 페이지](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. <span data-ttu-id="e21dc-135">Toohello 수행할 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e21dc-135">You will be taken toohello **Home** page.</span></span> <span data-ttu-id="e21dc-136">이 페이지에서는 hello tooconfigure와 레지스터 hello hello StorSimple 장치 관리자 서비스를 사용 하 여 가상 장치 다양 한 설정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-136">This page describes hello various settings required tooconfigure and register hello virtual device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="e21dc-137">해당 hello 참고 **네트워크 설정**, **웹 프록시 설정**, 및 **시간 설정** 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-137">Note that hello **Network settings**, **Web proxy settings**, and **Time settings** are optional.</span></span> <span data-ttu-id="e21dc-138">필요한 설정은 hello **장치 설정** 및 **클라우드 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-138">hello only required settings are **Device settings** and **Cloud settings**.</span></span>
   
    ![홈 페이지](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. <span data-ttu-id="e21dc-140">Hello에 **네트워크 설정** 페이지 **네트워크 인터페이스**, 데이터 0을 자동으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-140">On hello **Network settings** page under **Network interfaces**, DATA 0 will be automatically configured for you.</span></span> <span data-ttu-id="e21dc-141">각 네트워크 인터페이스 기본 tooget으로 IP 주소는 자동으로 설정 됩니다 (DHCP).</span><span class="sxs-lookup"><span data-stu-id="e21dc-141">Each network interface is set by default tooget an IP address automatically (DHCP).</span></span> <span data-ttu-id="e21dc-142">따라서 IP 주소, 서브넷 및 게이트웨이가 자동으로 할당됩니다(IPv4 및 IPv6 모두에 대해).</span><span class="sxs-lookup"><span data-stu-id="e21dc-142">Therefore, an IP address, subnet, and gateway will be automatically assigned (for both IPv4 and IPv6).</span></span>
   
    <span data-ttu-id="e21dc-143">ISCSI 서버 (tooprovision 블록 저장소)로 장치 toodeploy 계획할 때는 hello를 사용 하지 않도록 설정 하는 것이 좋습니다 **IP 주소를 자동으로 가져오기** 옵션 및 고정 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-143">As you plan toodeploy your device as an iSCSI server (tooprovision block storage), we recommend that you disable hello **Get IP address automatically** option and configure static IP addresses.</span></span>
   
    ![네트워크 설정 페이지](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    <span data-ttu-id="e21dc-145">Hello hello 장치의 프로 비전 중 둘 이상의 네트워크 인터페이스를 추가한 경우에 여기 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-145">If you added more than one network interface during hello provisioning of hello device, you can configure them here.</span></span> <span data-ttu-id="e21dc-146">네트워크 인터페이스를 IPv4로만 구성하거나 IPv4와 IPv6 둘 다로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-146">Note you can configure your network interface as IPv4 only or as both IPv4 and IPv6.</span></span> <span data-ttu-id="e21dc-147">IPv6 전용 구성은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-147">IPv6 only configurations are not supported.</span></span>
5. <span data-ttu-id="e21dc-148">에 사용 되므로 장치 시도 클라우드 저장소 서비스 공급자 또는 tooresolve toocommunicate 장치 이름으로 파일 서버로 구성 된 경우에 DNS 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-148">DNS servers are required because they are used when your device attempts toocommunicate with your cloud storage service providers or tooresolve your device by name if it is configured as a file server.</span></span> <span data-ttu-id="e21dc-149">Hello에 **네트워크 설정** hello 페이지 **DNS 서버**:</span><span class="sxs-lookup"><span data-stu-id="e21dc-149">On hello **Network settings** page under hello **DNS servers**:</span></span>
   
   1. <span data-ttu-id="e21dc-150">기본 및 보조 DNS 서버는 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-150">A primary and secondary DNS server will be automatically configured.</span></span> <span data-ttu-id="e21dc-151">Tooconfigure 고정 IP 주소를 선택한 경우에 DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-151">If you choose tooconfigure static IP addresses, you can specify DNS servers.</span></span> <span data-ttu-id="e21dc-152">고가용성을 위해 기본 및 보조 DNS 서버를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-152">For high availability, we recommend that you configure a primary and a secondary DNS server.</span></span>
   2. <span data-ttu-id="e21dc-153">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-153">Click **Apply**.</span></span> <span data-ttu-id="e21dc-154">적용 되 고 hello 네트워크 설정의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-154">This will apply and validate hello network settings.</span></span>
6. <span data-ttu-id="e21dc-155">Hello에 **장치 설정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e21dc-155">On hello **Device settings** page:</span></span>
   
   1. <span data-ttu-id="e21dc-156">고유한 할당 **이름** tooyour 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-156">Assign a unique **Name** tooyour device.</span></span> <span data-ttu-id="e21dc-157">이름에는 1-15자를 사용할 수 있으며 문자, 숫자 및 하이픈을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-157">This name can be 1-15 characters and can contain letter, numbers and hyphens.</span></span>
   2. <span data-ttu-id="e21dc-158">Hello 클릭 **iSCSI 서버** 아이콘 ![iSCSI 서버 아이콘](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) hello에 대 한 **형식** 만들고 있는 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-158">Click hello **iSCSI server** icon ![iSCSI server icon](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) for hello **Type** of device that you are creating.</span></span> <span data-ttu-id="e21dc-159">ISCSI 서버 tooprovision 한 블록 저장소를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-159">An iSCSI server will allow you tooprovision block storage.</span></span>
   3. <span data-ttu-id="e21dc-160">지정 하는 경우이 장치 toobe 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-160">Specify if you want this device toobe domain-joined.</span></span> <span data-ttu-id="e21dc-161">장치 iSCSI 서버를 사용 하는 경우에 다음 hello 도메인에 가입 하는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-161">If your device is an iSCSI server, then joining hello domain is optional.</span></span> <span data-ttu-id="e21dc-162">Toonot 조인 iSCSI 서버 tooa 도메인을 결정 한 경우 클릭 **적용**, hello 설정 toobe 적용 될 때까지 기다리는 및 toohello 다음 단계를 건너 뛰 세요.</span><span class="sxs-lookup"><span data-stu-id="e21dc-162">If you decide toonot join your iSCSI server tooa domain, click **Apply**, wait for hello settings toobe applied and then skip toohello next step.</span></span>
      
       <span data-ttu-id="e21dc-163">Toojoin hello 장치 tooa 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-163">If you want toojoin hello device tooa domain.</span></span> <span data-ttu-id="e21dc-164">**도메인 이름**을 입력하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-164">Enter a **Domain name**, and then click **Apply**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e21dc-165">가상 배열 자체 Microsoft Azure Active Directory 및 그룹 정책 개체 (GPO)에 대 한 조직 구성 단위 (OU) 인지 확인 iSCSI 서버 tooa 도메인에 가입 하는 경우에 적용 된 tooit이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-165">If joining your iSCSI server tooa domain, ensure that your virtual  array is in its own organizational unit (OU) for Microsoft Azure Active Directory and no group policy objects (GPO) are applied tooit.</span></span>
      > 
      > 
   4. <span data-ttu-id="e21dc-166">대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-166">A dialog box will appear.</span></span> <span data-ttu-id="e21dc-167">지정 된 형식의 hello 도메인 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-167">Enter your domain credentials in hello specified format.</span></span> <span data-ttu-id="e21dc-168">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-168">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png)<span data-ttu-id="e21dc-170">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-170">.</span></span> <span data-ttu-id="e21dc-171">hello 도메인 자격 증명 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-171">hello domain credentials will be verified.</span></span> <span data-ttu-id="e21dc-172">Hello 자격 증명이 올바르지 않을 경우 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-172">You will see an error message if hello credentials are incorrect.</span></span>
      
       ![자격 증명](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. <span data-ttu-id="e21dc-174">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-174">Click **Apply**.</span></span> <span data-ttu-id="e21dc-175">적용 되 고 hello 장치 설정의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-175">This will apply and validate hello device settings.</span></span>
7. <span data-ttu-id="e21dc-176">선택적으로 웹 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-176">(Optionally) configure your web proxy server.</span></span> <span data-ttu-id="e21dc-177">웹 프록시 구성은 선택 사항이지만 웹 프록시를 사용하면 여기서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-177">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span>
   
    ![웹 프록시 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    <span data-ttu-id="e21dc-179">Hello에 **웹 프록시** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e21dc-179">On hello **Web proxy** page:</span></span>
   
   1. <span data-ttu-id="e21dc-180">공급 hello **웹 프록시 URL** 형식에서: *http://host-IP 주소* 또는 *FDQN:Port 번호*합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-180">Supply hello **Web proxy URL** in this format: *http://host-IP address* or *FDQN:Port number*.</span></span> <span data-ttu-id="e21dc-181">HTTPS URL은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-181">Note that HTTPS URLs are not supported.</span></span>
   2. <span data-ttu-id="e21dc-182">**인증**은 **기본** 또는 **없음**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-182">Specify **Authentication** as **Basic** or **None**.</span></span>
   3. <span data-ttu-id="e21dc-183">인증을 사용 하는 또한 경우 tooprovide는 **Username** 및 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-183">If you are using authentication, you will also need tooprovide a **Username** and **Password**.</span></span>
   4. <span data-ttu-id="e21dc-184">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-184">Click **Apply**.</span></span> <span data-ttu-id="e21dc-185">유효성 검사 되 고 구성 하는 hello 웹 프록시 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-185">This will validate and apply hello configured web proxy settings.</span></span>
8. <span data-ttu-id="e21dc-186">표준 시간대 등 장치에 대 한 hello 시간 설정을 구성 하 고 기본 및 보조 NTP 서버 hello (선택 사항).</span><span class="sxs-lookup"><span data-stu-id="e21dc-186">(Optionally) configure hello time settings for your device, such as time zone and hello primary and secondary NTP servers.</span></span> <span data-ttu-id="e21dc-187">클라우드 서비스 공급자와 인증할 수 있도록 장치 시간을 동기화해야 하기 때문에 NTP 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-187">NTP servers are required because your device must synchronize time so that it can authenticate with your cloud service providers.</span></span>
   
    ![시간 설정](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    <span data-ttu-id="e21dc-189">Hello에 **시간 설정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e21dc-189">On hello **Time settings** page:</span></span>
   
   1. <span data-ttu-id="e21dc-190">Hello 드롭 다운 목록에서 선택 hello **시간대** hello 지리적 위치 장치 배포 되 고 있는 hello에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-190">From hello drop-down list, select hello **Time zone** based on hello geographic location in which hello device is being deployed.</span></span> <span data-ttu-id="e21dc-191">장치에 대 한 hello 기본 표준 시간대 PST입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-191">hello default time zone for your device is PST.</span></span> <span data-ttu-id="e21dc-192">장치는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-192">Your device will use this time zone for all scheduled operations.</span></span>
   2. <span data-ttu-id="e21dc-193">지정 된 **주 NTP 서버** 장치에 대 한 하거나 time.windows.com의 hello 기본값을 적용 합니다. 네트워크 사용자 데이터 센터 toohello 인터넷에서에서 NTP 트래픽이 toopass 허용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-193">Specify a **Primary NTP server** for your device or accept hello default value of time.windows.com. Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span>
   3. <span data-ttu-id="e21dc-194">선택적으로 장치에 대한 **보조 NTP 서버**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-194">Optionally specify a **Secondary NTP server** for your device.</span></span>
   4. <span data-ttu-id="e21dc-195">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-195">Click **Apply**.</span></span> <span data-ttu-id="e21dc-196">유효성 검사 되 고 구성 하는 hello 시간 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-196">This will validate and apply hello configured time settings.</span></span>
9. <span data-ttu-id="e21dc-197">장치에 대 한 hello 클라우드 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-197">Configure hello cloud settings for your device.</span></span> <span data-ttu-id="e21dc-198">이 단계에서는 hello 로컬 장치 구성을 완료 한 후 StorSimple 장치 관리자 서비스와 hello 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-198">In this step, you will complete hello local device configuration and then register hello device with your StorSimple Device Manager service.</span></span>
   
   1. <span data-ttu-id="e21dc-199">Hello 입력 **서비스 등록 키** 가져온 **2 단계: Get hello 서비스 등록 키** 에 [배포 StorSimple 가상 배열-포털 hello 준비](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-199">Enter hello **Service registration key** that you got in **Step 2: Get hello service registration key** in [Deploy StorSimple Virtual Array - Prepare hello Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
   2. <span data-ttu-id="e21dc-200">Tooprovide hello 할 경우이 정보가이 서비스에 등록 하는 hello 첫 번째 장치를 **서비스 데이터 암호화 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-200">If this is not hello first device that you are registering with this service, you will need tooprovide hello **Service data encryption key**.</span></span> <span data-ttu-id="e21dc-201">이 키는 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple 장치 관리자 서비스 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-201">This key is required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="e21dc-202">자세한 내용은 참조 너무[Get hello 서비스 데이터 암호화 키](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) 에 로컬 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-202">For more information, refer too[Get hello service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) on your local web UI.</span></span>
   3. <span data-ttu-id="e21dc-203">**Register**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-203">Click **Register**.</span></span> <span data-ttu-id="e21dc-204">Hello 장치 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-204">This will restart hello device.</span></span> <span data-ttu-id="e21dc-205">Hello 장치를 등록 하기 전에 2-3 분 동안 toowait을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-205">You may need toowait for 2-3 minutes before hello device is successfully registered.</span></span> <span data-ttu-id="e21dc-206">Hello 장치를 다시 시작한 후 이동 됩니다 toohello 로그인 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-206">After hello device has restarted, you will be taken toohello sign in page.</span></span>
      
      ![장치 등록](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. <span data-ttu-id="e21dc-208">Azure 포털 toohello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-208">Return toohello Azure portal.</span></span>
11. <span data-ttu-id="e21dc-209">Toohello 이동 **장치** 서비스의 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-209">Navigate toohello **Devices** blade of your service.</span></span> <span data-ttu-id="e21dc-210">리소스가 많이 있는 경우 **모든 리소스**를 클릭하고 서비스 이름(필요한 경우 검색)을 클릭한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-210">If you have a lot of resources, click **All resources**, click your service name (search for it if necessary), and then click **Devices**.</span></span>
12. <span data-ttu-id="e21dc-211">Hello에 **장치** 블레이드에서 hello 장치 성공적으로 hello 상태를 조회 하 여 toohello 서비스 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-211">On hello **Devices** blade, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="e21dc-212">hello 장치 상태가 **를 tooset 준비**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-212">hello device status should be **Ready tooset up**.</span></span>
    
    ![장치 등록](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a><span data-ttu-id="e21dc-214">2 단계: iSCSI 서버로 hello 장치 구성</span><span class="sxs-lookup"><span data-stu-id="e21dc-214">Step 2: Configure hello device as iSCSI server</span></span>

<span data-ttu-id="e21dc-215">Hello Azure 포털 toocomplete hello 필요한 장치 설치 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-215">Perform hello following steps in hello Azure portal toocomplete hello required device setup.</span></span>

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a><span data-ttu-id="e21dc-216">iSCSI 서버로 tooconfigure hello 장치</span><span class="sxs-lookup"><span data-stu-id="e21dc-216">tooconfigure hello device as iSCSI server</span></span>

1. <span data-ttu-id="e21dc-217">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 이동 하 여 너무**관리 > 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-217">Go tooyour StorSimple Device Manager service and then go too**Management > Devices**.</span></span> <span data-ttu-id="e21dc-218">Hello에 **장치** 블레이드, 방금 만든 선택 hello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-218">In hello **Devices** blade, select hello device you just created.</span></span> <span data-ttu-id="e21dc-219">이 장치도 표시 됩니다 **를 tooset 준비**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-219">This device would show up as **Ready tooset up**.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. <span data-ttu-id="e21dc-221">클릭 하 여 hello 장치의 hello 장치 준비 toosetup 인지 나타내는 배너 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-221">Click hello device and you will see a banner message indicating that hello device is ready toosetup.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. <span data-ttu-id="e21dc-223">클릭 **구성** hello 장치 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-223">Click **Configure** on hello device command bar.</span></span> <span data-ttu-id="e21dc-224">Hello를 열어서이 **구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-224">This opens up hello **Configure** blade.</span></span> <span data-ttu-id="e21dc-225">Hello에 **구성** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-225">In hello **Configure** blade, do hello following:</span></span>
   
   * <span data-ttu-id="e21dc-226">hello iSCSI 서버 이름이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-226">hello iSCSI server name is automatically populated.</span></span>
   * <span data-ttu-id="e21dc-227">Hello 클라우드 저장소 암호화 너무 설정 되어 있는지 확인**Enabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-227">Make sure hello cloud storage encryption is set too**Enabled**.</span></span> <span data-ttu-id="e21dc-228">이렇게 하면 hello 장치 toohello 클라우드에서 전송 된 hello 데이터 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-228">This ensures that hello data sent from hello device toohello cloud is encrypted.</span></span>
   * <span data-ttu-id="e21dc-229">32자 암호화 키를 지정하고 나중에 참조할 수는 키 관리 앱에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-229">Specify a 32-character encryption key and record it in a key management app for future reference.</span></span>
   * <span data-ttu-id="e21dc-230">장치와 함께 사용 되는 저장소 계정 toobe를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-230">Select a storage account toobe used with your device.</span></span> <span data-ttu-id="e21dc-231">이 구독에서 기존 저장소 계정을 선택 하거나 클릭할 수 있는 **추가** toochoose 다른 구독에서 계정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-231">In this subscription, you can select an existing storage account, or you can click **Add** toochoose an account from a different subscription.</span></span>
     
     ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. <span data-ttu-id="e21dc-233">클릭 **구성** toocomplete hello iSCSI 서버 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-233">Click **Configure** toocomplete setting up hello iSCSI server.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. <span data-ttu-id="e21dc-235">알려 hello iSCSI 서버 만들기 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-235">You will be notified that hello iSCSI server creation is in progress.</span></span> <span data-ttu-id="e21dc-236">Hello iSCSI 서버를 성공적으로 만든 후 hello **장치** 블레이드 업데이트 되 고 해당 장치 상태가 hello **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-236">After hello iSCSI server is successfully created, hello **Devices** blade is updated and hello corresponding device status is **Online**.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a><span data-ttu-id="e21dc-238">3단계: 볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="e21dc-238">Step 3: Add a volume</span></span>

1. <span data-ttu-id="e21dc-239">Hello에 **장치** 블레이드, 선택 hello 장치를 방금 iSCSI 서버로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-239">In hello **Devices** blade, select hello device you just configured as an iSCSI server.</span></span> <span data-ttu-id="e21dc-240">클릭 **중...**  (이 행에 또는 마우스 오른쪽 단추로) hello 상황에 맞는 메뉴에서 선택 하 고 **볼륨 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-240">Click **...** (alternatively right-click in this row) and from hello context menu, select **Add volume**.</span></span> <span data-ttu-id="e21dc-241">클릭할 수도 있습니다 **+ 볼륨 추가** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-241">You can also click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="e21dc-242">Hello를 열어서이 **볼륨 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-242">This opens up hello **Add volume** blade.</span></span>
   
    ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. <span data-ttu-id="e21dc-244">Hello에 **볼륨 추가** 블레이드에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="e21dc-244">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="e21dc-245">Hello에 **볼륨 이름을** 필드에서 볼륨에 대 한 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-245">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="e21dc-246">hello 이름에는 3 too127 문자를 포함 하는 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-246">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="e21dc-247">Hello에 **형식** 드롭다운 목록에서 지정 하는지 여부를 toocreate는 **계층화 됨** 또는 **로컬로 고정** 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-247">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="e21dc-248">로컬 보증, 낮은 대기 시간 및 높은 성능을 필요로 하는 워크로드의 경우 **로컬로 고정된** **볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-248">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned** **volume**.</span></span> <span data-ttu-id="e21dc-249">다른 모든 데이터에 대해서는 **계층화된** **볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-249">For all other data, select **Tiered** **volume**.</span></span>
   * <span data-ttu-id="e21dc-250">Hello에 **용량** 필드 hello hello 볼륨 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-250">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="e21dc-251">계층화된 볼륨은 500GB에서 5TB 사이여야 하고 로컬로 고정된 볼륨은 50GB에서 500GB 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-251">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
     
     <span data-ttu-id="e21dc-252">로컬 고정된 볼륨 씩 프로 비전 하 고 hello hello 볼륨의 기본 데이터를 hello 장치에 유지 되 고 toohello 클라우드를 분산 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-252">A locally pinned volume is thickly provisioned and ensures that hello primary data in hello volume stays on hello device and does not spill toohello cloud.</span></span>
     
     <span data-ttu-id="e21dc-253">계층화 된 볼륨 hello에 다른 손 씬 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-253">A tiered volume on hello other hand is thinly provisioned.</span></span> <span data-ttu-id="e21dc-254">계층화 된 볼륨을 만들 때 hello 공간의 약 10 %hello 로컬 계층에서 프로 비전 하 고 hello 공간을 90 %hello 클라우드 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-254">When you create a tiered volume, approximately 10% of hello space is provisioned on hello local tier and 90% of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="e21dc-255">예를 들어 1 t B 볼륨을 프로 비전, 100GB hello 로컬 공간에 있게 및 900GB hello 클라우드에서 사용할 수 있도록 하는 경우 데이터 계층이 때 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-255">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="e21dc-256">이 차례로 것을 의미 하는 hello 장치에서 모든 hello 로컬 공간이 부족 하면 있습니다 (하기 때문에 hello 10%를 사용할 수 있습니다)를 계층화 된 공유에 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-256">This in turn implies is that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10% will not be available).</span></span>
     
     ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * <span data-ttu-id="e21dc-258">클릭 **호스트 연결**, 액세스 제어 레코드 (ACR) 해당 toohello iSCSI 초기자는 tooconnect toothis 볼륨을 클릭 한 다음 선택 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-258">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span> <br><br> 
3. <span data-ttu-id="e21dc-259">tooadd 새 연결 된 호스트를 클릭 **새로 추가**, hello 호스트와 해당 iSCSI에 대 한 이름을 입력 하 고 클릭 한 다음 정규화 된 이름 (IQN) **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-259">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span> <span data-ttu-id="e21dc-260">IQN hello를 설정 하지 않은 경우 너무 이동[부록 a: 가져오기 hello Windows Server 호스트의 IQN](#appendix-a-get-the-iqn-of-a-windows-server-host)합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-260">If you don't have hello IQN, go too[Appendix A: Get hello IQN of a Windows Server host](#appendix-a-get-the-iqn-of-a-windows-server-host).</span></span>
   
      ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. <span data-ttu-id="e21dc-262">볼륨 구성을 완료했다면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-262">When you're finished configuring your volume, click **OK**.</span></span> <span data-ttu-id="e21dc-263">지정 된 hello로 볼륨을 만들 수는 설정 하 고 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-263">A volume will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="e21dc-264">기본적으로 모니터링 및 백업을 반드시 hello 볼륨에 대해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-264">By default, monitoring and backup will be enabled for hello volume.</span></span>
   
     ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. <span data-ttu-id="e21dc-266">볼륨 hello tooconfirm를 만드는 방법, 이동 toohello **볼륨** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-266">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="e21dc-267">Hello 볼륨이 나열 되어 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-267">You should see hello volume listed.</span></span>
   
   ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a><span data-ttu-id="e21dc-269">4단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="e21dc-269">Step 4: Mount, initialize, and format a volume</span></span>

<span data-ttu-id="e21dc-270">Hello 수행 단계 toomount 다음 초기화 및 Windows Server 호스트에 StorSimple 볼륨을 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-270">Perform hello following steps toomount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

#### <a name="toomount-initialize-and-format-a-volume"></a><span data-ttu-id="e21dc-271">toomount, 초기화 및 볼륨 포맷</span><span class="sxs-lookup"><span data-stu-id="e21dc-271">toomount, initialize, and format a volume</span></span>

1. <span data-ttu-id="e21dc-272">열기 hello **iSCSI 초기자** hello 적절 한 서버에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-272">Open hello **iSCSI initiator** app on hello appropriate server.</span></span>
2. <span data-ttu-id="e21dc-273">Hello에 **iSCSI 초기자 속성** 창의 hello에 **검색** 탭을 클릭 **포털 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-273">In hello **iSCSI Initiator Properties** window, on hello **Discovery** tab, click **Discover Portal**.</span></span>
   
    ![포털 검색](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. <span data-ttu-id="e21dc-275">Hello에 **대상 포털 검색** 대화 상자에서 사용할 수 있는 iSCSI 네트워크 인터페이스의 hello IP 주소를 제공 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-275">In hello **Discover Target Portal** dialog box, supply hello IP address of your iSCSI-enabled network interface, and then click **OK**.</span></span>
   
    ![IP 주소](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. <span data-ttu-id="e21dc-277">Hello에 **iSCSI 초기자 속성** 창의 hello에 **대상** 탭, 찾기 hello **대상 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-277">In hello **iSCSI Initiator Properties** window, on hello **Targets** tab, locate hello **Discovered targets**.</span></span> <span data-ttu-id="e21dc-278">(각 볼륨이 검색 된 대상 됩니다.) hello 장치 상태에 표시 되어야 **비활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-278">(Each volume will be a discovered target.) hello device status should appear as **Inactive**.</span></span>
   
    ![검색된 대상](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. <span data-ttu-id="e21dc-280">대상 장치를 선택하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-280">Select a target device and then click **Connect**.</span></span> <span data-ttu-id="e21dc-281">Hello 상태도 변경 해야 hello 장치가 연결 된 후**연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-281">After hello device is connected, hello status should change too**Connected**.</span></span> <span data-ttu-id="e21dc-282">(Hello Microsoft iSCSI 초기자를 사용 하는 방법에 대 한 자세한 내용은 참조 [iSCSI 초기자 설치 및 구성 하는 Microsoft][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-282">(For more information about using hello Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
   
    ![대상 장치 선택](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. <span data-ttu-id="e21dc-284">Windows 호스트에서 hello Windows 로고 키 + X를 클릭 한 다음 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-284">On your Windows host, press hello Windows Logo key + X, and then click **Run**.</span></span>
7. <span data-ttu-id="e21dc-285">Hello에 **실행** 대화 상자에서 **Diskmgmt.msc**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-285">In hello **Run** dialog box, type **Diskmgmt.msc**.</span></span> <span data-ttu-id="e21dc-286">클릭 **확인**, 및 hello **디스크 관리** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-286">Click **OK**, and hello **Disk Management** dialog box will appear.</span></span> <span data-ttu-id="e21dc-287">hello 오른쪽 창에는 호스트에서 hello 볼륨이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-287">hello right pane will show hello volumes on your host.</span></span>
8. <span data-ttu-id="e21dc-288">Hello에 **디스크 관리** 창의 hello 탑재 된 볼륨이 표시 됩니다 hello 다음 그림에에서 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-288">In hello **Disk Management** window, hello mounted volumes will appear as shown in hello following illustration.</span></span> <span data-ttu-id="e21dc-289">발견 된 hello 볼륨을 마우스 오른쪽 단추로 클릭 (hello 디스크 이름 클릭)를 클릭 하 고 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-289">Right-click hello discovered volume (click hello disk name), and then click **Online**.</span></span>
   
    ![디스크 관리](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. <span data-ttu-id="e21dc-291">마우스 오른쪽 단추를 클릭한 다음 **디스크 초기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-291">Right-click and select **Initialize Disk**.</span></span>
   
    ![디스크 1 초기화](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. <span data-ttu-id="e21dc-293">Hello 대화 상자에서 디스크 tooinitialize hello를 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-293">In hello dialog box, select hello disk(s) tooinitialize, and then click **OK**.</span></span>
    
    ![디스크 2 초기화](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. <span data-ttu-id="e21dc-295">hello 새 단순 볼륨 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-295">hello New Simple Volume wizard starts.</span></span> <span data-ttu-id="e21dc-296">디스크 크기를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-296">Select a disk size, and then click **Next**.</span></span>
    
    ![새 볼륨 마법사 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. <span data-ttu-id="e21dc-298">드라이브 문자 toohello 볼륨을 할당 한 후 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-298">Assign a drive letter toohello volume, and then click **Next**.</span></span>
    
    ![새 볼륨 마법사 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. <span data-ttu-id="e21dc-300">Hello 매개 변수 tooformat hello 볼륨을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-300">Enter hello parameters tooformat hello volume.</span></span> <span data-ttu-id="e21dc-301">**Windows Server에는 NTFS만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="e21dc-301">**On Windows Server, only NTFS is supported.**</span></span> <span data-ttu-id="e21dc-302">할당 단위 크기 too64K hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-302">Set hello allocation unit size too64K.</span></span> <span data-ttu-id="e21dc-303">볼륨의 레이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-303">Provide a label for your volume.</span></span> <span data-ttu-id="e21dc-304">StorSimple 가상 배열에 제공 된이 이름 toobe 동일한 toohello 볼륨 이름에 대 한 권장된 모범 사례는 경우</span><span class="sxs-lookup"><span data-stu-id="e21dc-304">It is a recommended best practice for this name toobe identical toohello volume name you provided on your StorSimple Virtual Array.</span></span> <span data-ttu-id="e21dc-305">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-305">Click **Next**.</span></span>
    
    ![새 볼륨 마법사 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. <span data-ttu-id="e21dc-307">서 볼륨에 대 한 hello 값을 확인 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-307">Check hello values for your volume, and then click **Finish**.</span></span>
    
    ![새 볼륨 마법사 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    <span data-ttu-id="e21dc-309">hello 볼륨으로 표시 됩니다 **온라인** hello에 **디스크 관리** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e21dc-309">hello volumes will appear as **Online** on hello **Disk Management** page.</span></span>
    
    ![온라인 볼륨](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a><span data-ttu-id="e21dc-311">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e21dc-311">Next steps</span></span>

<span data-ttu-id="e21dc-312">어떻게 toouse hello 로컬 웹 UI 너무 자세한[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-312">Learn how toouse hello local web UI too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a><span data-ttu-id="e21dc-313">부록 a: Get hello Windows Server 호스트의 IQN</span><span class="sxs-lookup"><span data-stu-id="e21dc-313">Appendix A: Get hello IQN of a Windows Server host</span></span>

<span data-ttu-id="e21dc-314">다음 단계 tooget hello iSCSI hello 수행 정규화 된 이름 (IQN) Windows Server 2012를 실행 중인 Windows 호스트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-314">Perform hello following steps tooget hello iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server 2012.</span></span>

#### <a name="tooget-hello-iqn-of-a-windows-host"></a><span data-ttu-id="e21dc-315">tooget hello Windows 호스트의 IQN</span><span class="sxs-lookup"><span data-stu-id="e21dc-315">tooget hello IQN of a Windows host</span></span>

1. <span data-ttu-id="e21dc-316">Windows 호스트에 hello Microsoft iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-316">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
2. <span data-ttu-id="e21dc-317">Hello에 **iSCSI 초기자 속성** 창의 hello에 **구성** 탭 선택 하 고 hello에서 hello 문자열을 복사 **초기자 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-317">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   
    ![iSCSI 초기자 속성](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. <span data-ttu-id="e21dc-319">이 문자열을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e21dc-319">Save this string.</span></span>

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



