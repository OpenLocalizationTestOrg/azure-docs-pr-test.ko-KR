---
title: "Microsoft Azure StorSimple 가상 배열 iSCSI 서버 설정 | Microsoft Docs"
description: "초기 설정을 수행하고, StorSimple iSCSI 서버를 등록하고, 장치 설정을 완료하는 방법을 설명합니다."
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
ms.openlocfilehash: 076df176d7cd40c009aea27004fe0f4415999c80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a><span data-ttu-id="f7a71-103">StorSimple 가상 배열 배포 – Azure Portal을 통해 iSCSI 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="f7a71-103">Deploy StorSimple Virtual Array – Set up as an iSCSI server via Azure portal</span></span>

![iscsi 설정 프로세스 흐름](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a><span data-ttu-id="f7a71-105">개요</span><span class="sxs-lookup"><span data-stu-id="f7a71-105">Overview</span></span>

<span data-ttu-id="f7a71-106">이 배포 자습서는 Microsoft Azure StorSimple 가상 배열에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-106">This deployment tutorial applies to the Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="f7a71-107">이 자습서는 iSCSI 서버에서 구성된 StorSimple 가상 배열에서 초기 설정을 수행하고, StorSimple iSCSI 서버를 등록하고, 장치 설정을 완료하고, StorSimple 가상 장치 iSCSI 서버에서 볼륨을 만들고, 탑재하고, 초기화하고, 포맷하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-107">This tutorial describes how to perform the initial setup, register your StorSimple iSCSI server, complete the device setup, and then create, mount, initialize, and format volumes on your StorSimple Virtual Array configured as an iSCSI server.</span></span> 

<span data-ttu-id="f7a71-108">여기서 설명된 프로시저를 완료하려면 30분에서 1시간 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-108">The procedures described here take approximately 30 minutes to 1 hour to complete.</span></span> <span data-ttu-id="f7a71-109">이 문서에 게시된 정보는 StorSimple 가상 배열에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-109">The information published in this article applies to StorSimple Virtual Arrays only.</span></span>

## <a name="setup-prerequisites"></a><span data-ttu-id="f7a71-110">설정 필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7a71-110">Setup prerequisites</span></span>

<span data-ttu-id="f7a71-111">StorSimple 가상 배열을 구성하고 설정하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-111">Before you configure and set up your StorSimple Virtual Array, make sure that:</span></span>

* <span data-ttu-id="f7a71-112">[StorSimple 가상 배열 배포 - Hyper-V에서 가상 배열 프로비전](storsimple-ova-deploy2-provision-hyperv.md) 또는 [StorSimple 가상 배열 배포 - VMware에서 가상 배열 프로비전](storsimple-virtual-array-deploy2-provision-vmware.md)에 설명된 대로 가상 배열을 프로비전하고 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-112">You have provisioned a virtual array and connected to it as described in [Deploy StorSimple Virtual Array - Provision a virtual array in Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array  - Provision a virtual array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
* <span data-ttu-id="f7a71-113">StorSimple 가상 배열을 관리하려고 만든 StorSimple 장치 관리자 서비스의 서비스 등록 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-113">You have the service registration key from the StorSimple Device Manager service that you created to manage your StorSimple Virtual Arrays.</span></span> <span data-ttu-id="f7a71-114">자세한 내용은 **StorSimple 가상 배열 배포 – 포털 준비** 의 [2단계: 서비스 등록 키 받기](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a71-114">For more information, see **Step 2: Get the service registration key** in [Deploy StorSimple Virtual Array - Prepare the portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
* <span data-ttu-id="f7a71-115">기존 StorSimple 장치 관리자 서비스에 가상 배열을 두 번째 또는 후속으로 등록하는 경우에는 서비스 데이터 암호화 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-115">If this is the second or subsequent virtual array that you are registering with an existing StorSimple Device Manager service, you should have the service data encryption key.</span></span> <span data-ttu-id="f7a71-116">이 키는 서비스에 첫 번째 장치가 등록될 때 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-116">This key was generated when the first device was successfully registered with this service.</span></span> <span data-ttu-id="f7a71-117">이 키를 잃어버린 경우에는 **웹 UI를 사용하여 StorSimple 가상 배열 관리** 의 [서비스 데이터 암호화 키 가져오기](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a71-117">If you have lost this key, see **Get the service data encryption key** in [Use the Web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).</span></span>

## <a name="step-by-step-setup"></a><span data-ttu-id="f7a71-118">단계별 설정</span><span class="sxs-lookup"><span data-stu-id="f7a71-118">Step-by-step setup</span></span>

<span data-ttu-id="f7a71-119">다음 단계별 지침을 사용하여 StorSimple 가상 배열을 설정 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-119">Use the following step-by-step instructions to set up and configure your StorSimple Virtual Array:</span></span>

* [<span data-ttu-id="f7a71-120">1단계: 로컬 웹 UI 설정을 완료하고 장치를 등록</span><span class="sxs-lookup"><span data-stu-id="f7a71-120">Step 1: Complete the local web UI setup and register your device</span></span>](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [<span data-ttu-id="f7a71-121">2단계: 필요한 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="f7a71-121">Step 2: Complete the required device setup</span></span>](#step-2-complete-the-required-device-setup)
* [<span data-ttu-id="f7a71-122">3단계: 볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="f7a71-122">Step 3: Add a volume</span></span>](#step-3-add-a-volume)
* [<span data-ttu-id="f7a71-123">4단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="f7a71-123">Step 4: Mount, initialize, and format a volume</span></span>](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-the-local-web-ui-setup-and-register-your-device"></a><span data-ttu-id="f7a71-124">1단계: 로컬 웹 UI 설정을 완료하고 장치를 등록</span><span class="sxs-lookup"><span data-stu-id="f7a71-124">Step 1: Complete the local web UI setup and register your device</span></span>

#### <a name="to-complete-the-setup-and-register-the-device"></a><span data-ttu-id="f7a71-125">설정을 완료하고 장치를 등록하려면</span><span class="sxs-lookup"><span data-stu-id="f7a71-125">To complete the setup and register the device</span></span>

1. <span data-ttu-id="f7a71-126">브라우저 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-126">Open a browser window.</span></span> <span data-ttu-id="f7a71-127">웹 UI 유형에 연결하려면:</span><span class="sxs-lookup"><span data-stu-id="f7a71-127">To connect to the web UI type:</span></span>
   
    `https://<ip-address of network interface>`
   
    <span data-ttu-id="f7a71-128">이전 단계에서 언급한 연결 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-128">Use the connection URL noted in the previous step.</span></span> <span data-ttu-id="f7a71-129">웹 사이트의 보안 인증서에 문제가 있음을 알려주는 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-129">You will see an error notifying you that there is a problem with the website’s security certificate.</span></span> <span data-ttu-id="f7a71-130">**이 웹 페이지에서 계속 진행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-130">Click **Continue to this web page**.</span></span>
   
    ![보안 인증서 오류](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. <span data-ttu-id="f7a71-132">가상 장치의 웹 UI에 **StorSimpleAdmin**으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-132">Sign in to the web UI of your virtual device as **StorSimpleAdmin**.</span></span> <span data-ttu-id="f7a71-133">[StorSimple 가상 배열 배포 - Hyper-V에서 가상 장치 프로비전](storsimple-virtual-array-deploy2-provision-hyperv.md) 또는 [StorSimple 가상 배열 배포 - VMware에서 가상 장치 프로비전](storsimple-virtual-array-deploy2-provision-vmware.md)의 3단계: 가상 장치 시작에서 변경한 장치 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-133">Enter the device administrator password that you changed in Step 3: Start the virtual device in [Deploy StorSimple Virtual Array - Provision a virtual device in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array - Provision a virtual device in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
   
    ![로그인 페이지](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. <span data-ttu-id="f7a71-135">**홈** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-135">You will be taken to the **Home** page.</span></span> <span data-ttu-id="f7a71-136">이 페이지는 StorSimple 장치 관리자 서비스에 가상 장치를 구성하고 등록하는 데 필요한 다양한 설정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-136">This page describes the various settings required to configure and register the virtual device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="f7a71-137">**네트워크 설정**, **웹 프록시 설정**, **시간 설정**은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-137">Note that the **Network settings**, **Web proxy settings**, and **Time settings** are optional.</span></span> <span data-ttu-id="f7a71-138">필요한 설정은 **장치 설정** 및 **클라우드 설정**입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-138">The only required settings are **Device settings** and **Cloud settings**.</span></span>
   
    ![홈 페이지](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. <span data-ttu-id="f7a71-140">**네트워크 설정** 페이지의 **네트워크 인터페이스**에서 DATA 0이 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-140">On the **Network settings** page under **Network interfaces**, DATA 0 will be automatically configured for you.</span></span> <span data-ttu-id="f7a71-141">각 네트워크 인터페이스는 IP 주소를 자동으로 가져오도록(DHCP) 기본 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-141">Each network interface is set by default to get an IP address automatically (DHCP).</span></span> <span data-ttu-id="f7a71-142">따라서 IP 주소, 서브넷 및 게이트웨이가 자동으로 할당됩니다(IPv4 및 IPv6 모두에 대해).</span><span class="sxs-lookup"><span data-stu-id="f7a71-142">Therefore, an IP address, subnet, and gateway will be automatically assigned (for both IPv4 and IPv6).</span></span>
   
    <span data-ttu-id="f7a71-143">장치를 iSCSI 서버(블록 저장소를 프로비전하기 위해)로 배포할 계획이므로, **자동으로 IP 주소 받기** 옵션을 사용하지 않도록 설정하고 고정 IP 주소를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-143">As you plan to deploy your device as an iSCSI server (to provision block storage), we recommend that you disable the **Get IP address automatically** option and configure static IP addresses.</span></span>
   
    ![네트워크 설정 페이지](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    <span data-ttu-id="f7a71-145">장치를 프로비전하는 동안 네트워크 인터페이스를 둘 이상 추가한 경우에는 여기에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-145">If you added more than one network interface during the provisioning of the device, you can configure them here.</span></span> <span data-ttu-id="f7a71-146">네트워크 인터페이스를 IPv4로만 구성하거나 IPv4와 IPv6 둘 다로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-146">Note you can configure your network interface as IPv4 only or as both IPv4 and IPv6.</span></span> <span data-ttu-id="f7a71-147">IPv6 전용 구성은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-147">IPv6 only configurations are not supported.</span></span>
5. <span data-ttu-id="f7a71-148">장치가 클라우드 저장소 서비스 공급자와 통신하려고 시도하거나 파일 서버로 구성된 경우 이름으로 장치를 확인하려고 시도하는 경우에 DNS 서버가 사용되기 때문에 DNS 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-148">DNS servers are required because they are used when your device attempts to communicate with your cloud storage service providers or to resolve your device by name if it is configured as a file server.</span></span> <span data-ttu-id="f7a71-149">**네트워크 설정** 페이지의 **DNS 서버** 아래에서:</span><span class="sxs-lookup"><span data-stu-id="f7a71-149">On the **Network settings** page under the **DNS servers**:</span></span>
   
   1. <span data-ttu-id="f7a71-150">기본 및 보조 DNS 서버는 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-150">A primary and secondary DNS server will be automatically configured.</span></span> <span data-ttu-id="f7a71-151">고정 IP 주소를 구성하도록 선택하면 DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-151">If you choose to configure static IP addresses, you can specify DNS servers.</span></span> <span data-ttu-id="f7a71-152">고가용성을 위해 기본 및 보조 DNS 서버를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-152">For high availability, we recommend that you configure a primary and a secondary DNS server.</span></span>
   2. <span data-ttu-id="f7a71-153">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-153">Click **Apply**.</span></span> <span data-ttu-id="f7a71-154">네트워크 설정이 적용되고 유효성 검사가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-154">This will apply and validate the network settings.</span></span>
6. <span data-ttu-id="f7a71-155">**장치 설정** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="f7a71-155">On the **Device settings** page:</span></span>
   
   1. <span data-ttu-id="f7a71-156">장치에 고유한 **이름** 을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-156">Assign a unique **Name** to your device.</span></span> <span data-ttu-id="f7a71-157">이름에는 1-15자를 사용할 수 있으며 문자, 숫자 및 하이픈을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-157">This name can be 1-15 characters and can contain letter, numbers and hyphens.</span></span>
   2. <span data-ttu-id="f7a71-158">만드는 장치의 **유형**에 대해 **iSCSI 서버** 아이콘 ![iSCSI 서버 아이콘](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-158">Click the **iSCSI server** icon ![iSCSI server icon](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) for the **Type** of device that you are creating.</span></span> <span data-ttu-id="f7a71-159">iSCSI 서버에서 블록 저장소를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-159">An iSCSI server will allow you to provision block storage.</span></span>
   3. <span data-ttu-id="f7a71-160">이 장치를 도메인에 가입할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-160">Specify if you want this device to be domain-joined.</span></span> <span data-ttu-id="f7a71-161">장치가 iSCSI 서버인 경우, 도메인 가입은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-161">If your device is an iSCSI server, then joining the domain is optional.</span></span> <span data-ttu-id="f7a71-162">iSCSI 서버를 도메인에 가입하지 않으려면, **적용**을 클릭하고 설정이 적용될 때까지 기다린 후에 다음 단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-162">If you decide to not join your iSCSI server to a domain, click **Apply**, wait for the settings to be applied and then skip to the next step.</span></span>
      
       <span data-ttu-id="f7a71-163">장치를 도메인에 가입하려면</span><span class="sxs-lookup"><span data-stu-id="f7a71-163">If you want to join the device to a domain.</span></span> <span data-ttu-id="f7a71-164">**도메인 이름**을 입력하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-164">Enter a **Domain name**, and then click **Apply**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f7a71-165">iSCSI 서버를 도메인에 연결하는 경우 가상 배열이 Microsoft Azure Active Directory용 자체 OU(조직 구성 단위)에 있으며 GPO(그룹 정책 개체)가 적용되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-165">If joining your iSCSI server to a domain, ensure that your virtual  array is in its own organizational unit (OU) for Microsoft Azure Active Directory and no group policy objects (GPO) are applied to it.</span></span>
      > 
      > 
   4. <span data-ttu-id="f7a71-166">대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-166">A dialog box will appear.</span></span> <span data-ttu-id="f7a71-167">지정된 형식으로 도메인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-167">Enter your domain credentials in the specified format.</span></span> <span data-ttu-id="f7a71-168">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="f7a71-168">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png)<span data-ttu-id="f7a71-170">을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-170">.</span></span> <span data-ttu-id="f7a71-171">도메인 자격 증명이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-171">The domain credentials will be verified.</span></span> <span data-ttu-id="f7a71-172">자격 증명이 올바르지 않으면 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-172">You will see an error message if the credentials are incorrect.</span></span>
      
       ![자격 증명](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. <span data-ttu-id="f7a71-174">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-174">Click **Apply**.</span></span> <span data-ttu-id="f7a71-175">장치 설정이 적용되고 유효성 검사가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-175">This will apply and validate the device settings.</span></span>
7. <span data-ttu-id="f7a71-176">(선택 사항) 웹 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-176">(Optionally) configure your web proxy server.</span></span> <span data-ttu-id="f7a71-177">웹 프록시 구성은 선택 사항이지만 웹 프록시를 사용하면 여기서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-177">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span>
   
    ![웹 프록시 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    <span data-ttu-id="f7a71-179">**웹 프록시** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="f7a71-179">On the **Web proxy** page:</span></span>
   
   1. <span data-ttu-id="f7a71-180">*http://host-IP 주소* 또는 *FDQN:포트 번호* 형식으로 **웹 프록시 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-180">Supply the **Web proxy URL** in this format: *http://host-IP address* or *FDQN:Port number*.</span></span> <span data-ttu-id="f7a71-181">HTTPS URL은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-181">Note that HTTPS URLs are not supported.</span></span>
   2. <span data-ttu-id="f7a71-182">**인증**은 **기본** 또는 **없음**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-182">Specify **Authentication** as **Basic** or **None**.</span></span>
   3. <span data-ttu-id="f7a71-183">인증을 사용하는 경우에는 **사용자 이름** 및 **암호**도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-183">If you are using authentication, you will also need to provide a **Username** and **Password**.</span></span>
   4. <span data-ttu-id="f7a71-184">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-184">Click **Apply**.</span></span> <span data-ttu-id="f7a71-185">구성된 웹 프록시 설정의 유효성을 검사하고 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-185">This will validate and apply the configured web proxy settings.</span></span>
8. <span data-ttu-id="f7a71-186">(선택 사항) 장치에 대한 시간 설정(예: 표준 시간대 및 기본 및 보조 NTP 서버)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-186">(Optionally) configure the time settings for your device, such as time zone and the primary and secondary NTP servers.</span></span> <span data-ttu-id="f7a71-187">클라우드 서비스 공급자와 인증할 수 있도록 장치 시간을 동기화해야 하기 때문에 NTP 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-187">NTP servers are required because your device must synchronize time so that it can authenticate with your cloud service providers.</span></span>
   
    ![시간 설정](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    <span data-ttu-id="f7a71-189">**시간 설정** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="f7a71-189">On the **Time settings** page:</span></span>
   
   1. <span data-ttu-id="f7a71-190">드롭다운 목록에서 해당 장치가 배포되는 지리적 위치를 기반으로 **표준 시간대**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-190">From the drop-down list, select the **Time zone** based on the geographic location in which the device is being deployed.</span></span> <span data-ttu-id="f7a71-191">장치의 기본 표준 시간대는 PST입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-191">The default time zone for your device is PST.</span></span> <span data-ttu-id="f7a71-192">장치는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-192">Your device will use this time zone for all scheduled operations.</span></span>
   2. <span data-ttu-id="f7a71-193">장치에 **기본 NTP 서버** 를 지정하거나 time.windows.com의 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-193">Specify a **Primary NTP server** for your device or accept the default value of time.windows.com.</span></span> <span data-ttu-id="f7a71-194">네트워크에서 NTP 트래픽이 데이터 센터에서 인터넷으로 전달되도록 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-194">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span>
   3. <span data-ttu-id="f7a71-195">선택적으로 장치에 대한 **보조 NTP 서버**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-195">Optionally specify a **Secondary NTP server** for your device.</span></span>
   4. <span data-ttu-id="f7a71-196">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-196">Click **Apply**.</span></span> <span data-ttu-id="f7a71-197">구성된 시간 설정의 유효성을 검사하고 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-197">This will validate and apply the configured time settings.</span></span>
9. <span data-ttu-id="f7a71-198">장치에 대한 클라우드 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-198">Configure the cloud settings for your device.</span></span> <span data-ttu-id="f7a71-199">이 단계에서는 로컬 장치 구성을 완료한 다음 StorSimple 장치 관리자 서비스에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-199">In this step, you will complete the local device configuration and then register the device with your StorSimple Device Manager service.</span></span>
   
   1. <span data-ttu-id="f7a71-200">[StorSimple 가상 배열 배포 - 포털 준비](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)에서 **2단계:서비스 등록 키 얻기**에서 얻은 **서비스 등록 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-200">Enter the **Service registration key** that you got in **Step 2: Get the service registration key** in [Deploy StorSimple Virtual Array - Prepare the Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
   2. <span data-ttu-id="f7a71-201">서비스에 장치를 처음으로 등록하는 경우가 아니라면 **서비스 데이터 암호화 키**를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-201">If this is not the first device that you are registering with this service, you will need to provide the **Service data encryption key**.</span></span> <span data-ttu-id="f7a71-202">이 키는 StorSimple 장치 관리자 서비스에 추가 장치를 등록하기 위한 서비스 등록 키에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-202">This key is required with the service registration key to register additional devices with the StorSimple Device Manager service.</span></span> <span data-ttu-id="f7a71-203">자세한 내용은 로컬 웹 UI의 [서비스 데이터 암호화 키 받기](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a71-203">For more information, refer to [Get the service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) on your local web UI.</span></span>
   3. <span data-ttu-id="f7a71-204">**등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-204">Click **Register**.</span></span> <span data-ttu-id="f7a71-205">장치가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-205">This will restart the device.</span></span> <span data-ttu-id="f7a71-206">장치 등록이 완료되기까지 2-3분 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-206">You may need to wait for 2-3 minutes before the device is successfully registered.</span></span> <span data-ttu-id="f7a71-207">장치가 다시 시작된 후 로그인 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-207">After the device has restarted, you will be taken to the sign in page.</span></span>
      
      ![장치 등록](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. <span data-ttu-id="f7a71-209">Azure Portal로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-209">Return to the Azure portal.</span></span>
11. <span data-ttu-id="f7a71-210">서비스의 **장치** 블레이드를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-210">Navigate to the **Devices** blade of your service.</span></span> <span data-ttu-id="f7a71-211">리소스가 많이 있는 경우 **모든 리소스**를 클릭하고 서비스 이름(필요한 경우 검색)을 클릭한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-211">If you have a lot of resources, click **All resources**, click your service name (search for it if necessary), and then click **Devices**.</span></span>
12. <span data-ttu-id="f7a71-212">**장치** 블레이드에서 상태를 조회하여 장치가 서비스에 성공적으로 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-212">On the **Devices** blade, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="f7a71-213">장치 상태는 **설정할 준비 완료**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-213">The device status should be **Ready to set up**.</span></span>
    
    ![장치 등록](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-the-device-as-iscsi-server"></a><span data-ttu-id="f7a71-215">2단계: iSCSI 서버로 장치 구성</span><span class="sxs-lookup"><span data-stu-id="f7a71-215">Step 2: Configure the device as iSCSI server</span></span>

<span data-ttu-id="f7a71-216">필요한 장치 설정을 완료하려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-216">Perform the following steps in the Azure portal to complete the required device setup.</span></span>

#### <a name="to-configure-the-device-as-iscsi-server"></a><span data-ttu-id="f7a71-217">iSCSI 서버로 장치를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="f7a71-217">To configure the device as iSCSI server</span></span>

1. <span data-ttu-id="f7a71-218">StorSimple 장치 관리자 서비스로 이동한 다음 **관리 > 장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-218">Go to your StorSimple Device Manager service and then go to **Management > Devices**.</span></span> <span data-ttu-id="f7a71-219">**장치** 블레이드에서 방금 만든 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-219">In the **Devices** blade, select the device you just created.</span></span> <span data-ttu-id="f7a71-220">이 장치는 **설정할 준비 완료**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-220">This device would show up as **Ready to set up**.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. <span data-ttu-id="f7a71-222">장치를 클릭하고 장치를 설치할 준비가 되었음을 나타내는 배너 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-222">Click the device and you will see a banner message indicating that the device is ready to setup.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. <span data-ttu-id="f7a71-224">장치 명령 모음에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-224">Click **Configure** on the device command bar.</span></span> <span data-ttu-id="f7a71-225">그러면 **구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-225">This opens up the **Configure** blade.</span></span> <span data-ttu-id="f7a71-226">**구성** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-226">In the **Configure** blade, do the following:</span></span>
   
   * <span data-ttu-id="f7a71-227">iSCSI 서버 이름은 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-227">The iSCSI server name is automatically populated.</span></span>
   * <span data-ttu-id="f7a71-228">클라우드 저장소 암호화가 **사용**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-228">Make sure the cloud storage encryption is set to **Enabled**.</span></span> <span data-ttu-id="f7a71-229">이를 통해 이 장치에서 클라우드로 전송되는 데이터가 암호화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-229">This ensures that the data sent from the device to the cloud is encrypted.</span></span>
   * <span data-ttu-id="f7a71-230">32자 암호화 키를 지정하고 나중에 참조할 수는 키 관리 앱에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-230">Specify a 32-character encryption key and record it in a key management app for future reference.</span></span>
   * <span data-ttu-id="f7a71-231">장치에 사용할 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-231">Select a storage account to be used with your device.</span></span> <span data-ttu-id="f7a71-232">구독에서 기존 저장소 계정을 선택하거나 **추가**를 클릭하여 다른 구독에서 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-232">In this subscription, you can select an existing storage account, or you can click **Add** to choose an account from a different subscription.</span></span>
     
     ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. <span data-ttu-id="f7a71-234">**구성**을 클릭하여 iSCSI 서버 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-234">Click **Configure** to complete setting up the iSCSI server.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. <span data-ttu-id="f7a71-236">iSCSI 서버 만들기가 진행 중이라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-236">You will be notified that the iSCSI server creation is in progress.</span></span> <span data-ttu-id="f7a71-237">iSCSI 서버를 성공적으로 만든 후에 **장치** 블레이드가 업데이트되고 해당 장치가 **온라인** 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-237">After the iSCSI server is successfully created, the **Devices** blade is updated and the corresponding device status is **Online**.</span></span>
   
    ![iSCSI 서버로 장치 구성](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a><span data-ttu-id="f7a71-239">3단계: 볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="f7a71-239">Step 3: Add a volume</span></span>

1. <span data-ttu-id="f7a71-240">**장치** 블레이드에서 iSCSI 서버로 구성한 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-240">In the **Devices** blade, select the device you just configured as an iSCSI server.</span></span> <span data-ttu-id="f7a71-241">또는 행에서 마우스 오른쪽 버튼으로 **...**을 클릭하고 상황에 맞는 메뉴에서 **볼륨 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-241">Click **...** (alternatively right-click in this row) and from the context menu, select **Add volume**.</span></span> <span data-ttu-id="f7a71-242">명령 모음에서 **+볼륨 추가**를 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-242">You can also click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="f7a71-243">그려면 **볼륨 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-243">This opens up the **Add volume** blade.</span></span>
   
    ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. <span data-ttu-id="f7a71-245">**볼륨 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-245">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="f7a71-246">**볼륨 이름** 필드에서 볼륨의 고유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-246">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="f7a71-247">이름은 3~127개의 문자를 포함하는 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-247">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="f7a71-248">**형식** 드롭다운 목록에서 **계층** 또는 **로컬로 고정** 볼륨을 만들지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-248">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="f7a71-249">로컬 보증, 낮은 대기 시간 및 높은 성능을 필요로 하는 워크로드의 경우 **로컬로 고정된** **볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-249">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned** **volume**.</span></span> <span data-ttu-id="f7a71-250">다른 모든 데이터에 대해서는 **계층화된** **볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-250">For all other data, select **Tiered** **volume**.</span></span>
   * <span data-ttu-id="f7a71-251">**용량** 필드에서 볼륨의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-251">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="f7a71-252">계층화된 볼륨은 500GB에서 5TB 사이여야 하고 로컬로 고정된 볼륨은 50GB에서 500GB 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-252">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
     
     <span data-ttu-id="f7a71-253">로컬로 고정된 볼륨은 씩 프로비전되며, 볼륨의 기본 데이터가 장치에 유지되고 클라우드에 유출되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-253">A locally pinned volume is thickly provisioned and ensures that the primary data in the volume stays on the device and does not spill to the cloud.</span></span>
     
     <span data-ttu-id="f7a71-254">반면에 계층화된 본륨은 씬 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-254">A tiered volume on the other hand is thinly provisioned.</span></span> <span data-ttu-id="f7a71-255">계층화된 볼륨을 만들 때 공간의 약 10%는 로컬 계층에 프로비전되고 공간의 90%는 클라우드에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-255">When you create a tiered volume, approximately 10% of the space is provisioned on the local tier and 90% of the space is provisioned in the cloud.</span></span> <span data-ttu-id="f7a71-256">예를 들어, 1TB 볼륨을 프로비전하는 경우 100GB는 로컬 공간에 상주하고 900GB는 데이터가 계층화될 때 클라우드에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-256">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="f7a71-257">이것은 장치의 로컬 공간이 부족하면 계층화된 공유를 프로비전할 수 없다는 것을(10%를 사용할 수 없기 때문에) 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-257">This in turn implies is that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10% will not be available).</span></span>
     
     ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * <span data-ttu-id="f7a71-259">**호스트 연결**을 클릭하고 이 볼륨에 연결하려는 iSCSI 초기자에 해당하는 ACR(액세스 제어 레코드)를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-259">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span> <br><br> 
3. <span data-ttu-id="f7a71-260">새롭게 연결된 호스트를 추가하려면 **새로 추가**를 클릭하고 호스트의 이름 및 해당 IQN(iSCSI 정규화 이름)을 입력한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-260">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span> <span data-ttu-id="f7a71-261">IQN이 없는 경우 [부록 A: Windows Server 호스트의 IQN 가져오기](#appendix-a-get-the-iqn-of-a-windows-server-host)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-261">If you don't have the IQN, go to [Appendix A: Get the IQN of a Windows Server host](#appendix-a-get-the-iqn-of-a-windows-server-host).</span></span>
   
      ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. <span data-ttu-id="f7a71-263">볼륨 구성을 완료했다면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-263">When you're finished configuring your volume, click **OK**.</span></span> <span data-ttu-id="f7a71-264">볼륨이 지정된 설정으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-264">A volume will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="f7a71-265">기본적으로 볼륨에 대한 모니터링 및 백업을 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-265">By default, monitoring and backup will be enabled for the volume.</span></span>
   
     ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. <span data-ttu-id="f7a71-267">볼륨이 성공적으로 만들어졌는지 확인하려면 **볼륨** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-267">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="f7a71-268">볼륨이 목록으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-268">You should see the volume listed.</span></span>
   
   ![볼륨 추가](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a><span data-ttu-id="f7a71-270">4단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="f7a71-270">Step 4: Mount, initialize, and format a volume</span></span>

<span data-ttu-id="f7a71-271">다음 단계를 수행하여 Windows Server 호스트에서 StorSimple 볼륨을 탑재, 초기화 및 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-271">Perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

#### <a name="to-mount-initialize-and-format-a-volume"></a><span data-ttu-id="f7a71-272">볼륨을 탑재, 초기화 및 포맷하려면</span><span class="sxs-lookup"><span data-stu-id="f7a71-272">To mount, initialize, and format a volume</span></span>

1. <span data-ttu-id="f7a71-273">적절한 서버에서 **iSCSI 초기자** 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-273">Open the **iSCSI initiator** app on the appropriate server.</span></span>
2. <span data-ttu-id="f7a71-274">**iSCSI 초기자 속성** 창의 **검색** 탭에서 **포털 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-274">In the **iSCSI Initiator Properties** window, on the **Discovery** tab, click **Discover Portal**.</span></span>
   
    ![포털 검색](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. <span data-ttu-id="f7a71-276">**대상 포털 검색** 대화 상자에서 iSCSI 사용 네트워크 인터페이스의 IP 주소를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-276">In the **Discover Target Portal** dialog box, supply the IP address of your iSCSI-enabled network interface, and then click **OK**.</span></span>
   
    ![IP 주소](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. <span data-ttu-id="f7a71-278">**iSCSI 초기자 속성** 창의 **대상** 탭에서 **검색된 대상**을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-278">In the **iSCSI Initiator Properties** window, on the **Targets** tab, locate the **Discovered targets**.</span></span> <span data-ttu-id="f7a71-279">(각 볼륨은 검색된 대상이 됩니다.) 장치 상태가 **비활성**으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-279">(Each volume will be a discovered target.) The device status should appear as **Inactive**.</span></span>
   
    ![검색된 대상](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. <span data-ttu-id="f7a71-281">대상 장치를 선택하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-281">Select a target device and then click **Connect**.</span></span> <span data-ttu-id="f7a71-282">장치가 연결되면 상태가 **연결됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-282">After the device is connected, the status should change to **Connected**.</span></span> <span data-ttu-id="f7a71-283">Microsoft iSCSI 초기자 사용에 대한 자세한 내용은 [Microsoft iSCSI 초기자 설치 및 구성][1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a71-283">(For more information about using the Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
   
    ![대상 장치 선택](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. <span data-ttu-id="f7a71-285">Windows 호스트에서 Windows 로고 키 + X를 누르고 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-285">On your Windows host, press the Windows Logo key + X, and then click **Run**.</span></span>
7. <span data-ttu-id="f7a71-286">**실행** 대화 상자에 **Diskmgmt.msc**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-286">In the **Run** dialog box, type **Diskmgmt.msc**.</span></span> <span data-ttu-id="f7a71-287">**확인**을 클릭하면 **디스크 관리** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-287">Click **OK**, and the **Disk Management** dialog box will appear.</span></span> <span data-ttu-id="f7a71-288">오른쪽 창에 호스트의 볼륨이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-288">The right pane will show the volumes on your host.</span></span>
8. <span data-ttu-id="f7a71-289">**디스크 관리** 창에 탑재된 볼륨이 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-289">In the **Disk Management** window, the mounted volumes will appear as shown in the following illustration.</span></span> <span data-ttu-id="f7a71-290">검색된 볼륨을 마우스 오른쪽 단추로 클릭(디스크 이름 클릭)한 다음 **온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-290">Right-click the discovered volume (click the disk name), and then click **Online**.</span></span>
   
    ![디스크 관리](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. <span data-ttu-id="f7a71-292">마우스 오른쪽 단추를 클릭한 다음 **디스크 초기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-292">Right-click and select **Initialize Disk**.</span></span>
   
    ![디스크 1 초기화](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. <span data-ttu-id="f7a71-294">대화 상자에서 초기화하려는 디스크를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-294">In the dialog box, select the disk(s) to initialize, and then click **OK**.</span></span>
    
    ![디스크 2 초기화](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. <span data-ttu-id="f7a71-296">새 단순 볼륨 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-296">The New Simple Volume wizard starts.</span></span> <span data-ttu-id="f7a71-297">디스크 크기를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-297">Select a disk size, and then click **Next**.</span></span>
    
    ![새 볼륨 마법사 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. <span data-ttu-id="f7a71-299">볼륨에 드라이브 문자를 할당한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-299">Assign a drive letter to the volume, and then click **Next**.</span></span>
    
    ![새 볼륨 마법사 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. <span data-ttu-id="f7a71-301">볼륨을 포맷하는 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-301">Enter the parameters to format the volume.</span></span> <span data-ttu-id="f7a71-302">**Windows Server에는 NTFS만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="f7a71-302">**On Windows Server, only NTFS is supported.**</span></span> <span data-ttu-id="f7a71-303">할당 단위 크기를 64K로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-303">Set the allocation unit size to 64K.</span></span> <span data-ttu-id="f7a71-304">볼륨의 레이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-304">Provide a label for your volume.</span></span> <span data-ttu-id="f7a71-305">이 이름은 StorSimple 가상 배열에 지정한 볼륨 이름과 동일하게 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-305">It is a recommended best practice for this name to be identical to the volume name you provided on your StorSimple Virtual Array.</span></span> <span data-ttu-id="f7a71-306">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-306">Click **Next**.</span></span>
    
    ![새 볼륨 마법사 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. <span data-ttu-id="f7a71-308">볼륨에 대한 값을 확인한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-308">Check the values for your volume, and then click **Finish**.</span></span>
    
    ![새 볼륨 마법사 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    <span data-ttu-id="f7a71-310">이 볼륨은 **디스크 관리** 페이지에 **온라인**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-310">The volumes will appear as **Online** on the **Disk Management** page.</span></span>
    
    ![온라인 볼륨](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a><span data-ttu-id="f7a71-312">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7a71-312">Next steps</span></span>

<span data-ttu-id="f7a71-313">로컬 웹 UI를 사용하여 [StorSimple 가상 배열을 관리](storsimple-ova-web-ui-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-313">Learn how to use the local web UI to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

## <a name="appendix-a-get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="f7a71-314">부록 A: Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="f7a71-314">Appendix A: Get the IQN of a Windows Server host</span></span>

<span data-ttu-id="f7a71-315">Windows Server 2012를 실행하는 Windows 호스트의 iSCSI 정규화된 이름(IQN)을 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-315">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server 2012.</span></span>

#### <a name="to-get-the-iqn-of-a-windows-host"></a><span data-ttu-id="f7a71-316">Windows 호스트의 IQN을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="f7a71-316">To get the IQN of a Windows host</span></span>

1. <span data-ttu-id="f7a71-317">Windows 호스트에서 Microsoft iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-317">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
2. <span data-ttu-id="f7a71-318">**iSCSI 초기자 속성** 창의 **구성** 탭에서 **초기자 이름** 필드의 문자열을 선택하고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-318">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   
    ![iSCSI 초기자 속성](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. <span data-ttu-id="f7a71-320">이 문자열을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a71-320">Save this string.</span></span>

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



