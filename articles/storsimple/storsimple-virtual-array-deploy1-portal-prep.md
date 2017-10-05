---
title: "StorSimple Virtual Array를 위한 포털 준비 | Microsoft Docs"
description: "StorSimple 가상 배열을 배포하는 첫 번째 자습서에는 Azure 포털 준비가 포함됩니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d0801053721f98ce7a2b0fcbe3c65da8dbdd8d3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-the-azure-portal"></a><span data-ttu-id="c5d8f-103">StorSimple 가상 배열 배포 – Azure Portal 준비</span><span class="sxs-lookup"><span data-stu-id="c5d8f-103">Deploy StorSimple Virtual Array - Prepare the Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="c5d8f-104">개요</span><span class="sxs-lookup"><span data-stu-id="c5d8f-104">Overview</span></span>

<span data-ttu-id="c5d8f-105">Resource Manager 모델을 사용하여 가상 배열을 파일 서버 또는 iSCSI 서버로 완전히 배포하는 데 필요한 배포 자습서 시리즈의 첫 번째 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-105">This is the first article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server using the Resource Manager model.</span></span> <span data-ttu-id="c5d8f-106">이 문서는 가상 배열을 프로비전하기 전에 StorSimple 장치 관리자 서비스를 만들고 구성하는 데 필요한 준비 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-106">This article describes the preparation required to create and configure your StorSimple Device Manager service prior to provisioning a virtual array.</span></span> <span data-ttu-id="c5d8f-107">이 문서는 배포 구성 검사 목록 및 필수 조건과도 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-107">This article also links out to a deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="c5d8f-108">설치 및 구성 프로세스를 완료하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-108">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="c5d8f-109">시작하기 전에 배포 구성 검사 목록을 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-109">We recommend that you review the deployment configuration checklist before you begin.</span></span> <span data-ttu-id="c5d8f-110">포털 준비에는 10분 미만이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-110">The portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="c5d8f-111">이 문서에 게시된 정보는 Azure Portal 및 Microsoft Azure Government 클라우드에서 StorSimple 가상 배열의 배포에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-111">The information published in this article applies to the deployment of StorSimple Virtual Arrays in the Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="c5d8f-112">시작</span><span class="sxs-lookup"><span data-stu-id="c5d8f-112">Get started</span></span>
<span data-ttu-id="c5d8f-113">배포 워크플로는 포털 준비, 가상화된 환경에 가상 배열 프로비전, 설치 완료로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-113">The deployment workflow consists of preparing the portal, provisioning a virtual array in your virtualized environment, and completing the setup.</span></span> <span data-ttu-id="c5d8f-114">파일 서버 또는 iSCSI 서버로 StorSimple 가상 배열 배포를 시작하려면 다음 표에 준비된 리소스를 참고해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-114">To get started with the StorSimple Virtual Array deployment as a file server or an iSCSI server, you need to refer to the following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="c5d8f-115">배포 문서</span><span class="sxs-lookup"><span data-stu-id="c5d8f-115">Deployment articles</span></span>

<span data-ttu-id="c5d8f-116">StorSimple 가상 배열을 배포하려면 다음 문서를 지정된 순서대로 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-116">To deploy your StorSimple Virtual Array, refer to the following articles in the prescribed sequence.</span></span>

| **#** | <span data-ttu-id="c5d8f-117">**단계**</span><span class="sxs-lookup"><span data-stu-id="c5d8f-117">**In this step**</span></span> | <span data-ttu-id="c5d8f-118">**이 작업을 수행합니다…**</span><span class="sxs-lookup"><span data-stu-id="c5d8f-118">**You do this …**</span></span> | <span data-ttu-id="c5d8f-119">**그리고 이러한 문서를 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="c5d8f-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c5d8f-120">1.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-120">1.</span></span> |<span data-ttu-id="c5d8f-121">**Azure Portal 설정**</span><span class="sxs-lookup"><span data-stu-id="c5d8f-121">**Set up the Azure portal**</span></span> |<span data-ttu-id="c5d8f-122">StorSimple 가상 배열을 프로비전하기 전에 StorSimple 장치 관리자 서비스를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-122">Create and configure your StorSimple Device Manager service prior to provisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="c5d8f-123">포털 준비</span><span class="sxs-lookup"><span data-stu-id="c5d8f-123">Prepare the portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="c5d8f-124">2.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-124">2.</span></span> |<span data-ttu-id="c5d8f-125">**가상 배열 프로비전**</span><span class="sxs-lookup"><span data-stu-id="c5d8f-125">**Provision the Virtual Array**</span></span> |<span data-ttu-id="c5d8f-126">Hyper-V의 경우 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2에서 Hyper-V를 실행하는 호스트 시스템의 StorSimple 가상 배열을 프로비전하고 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-126">For Hyper-V, provision and connect to a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="c5d8f-127">VMware의 경우, VMware ESXi 5.5 이상을 실행하는 호스트 시스템에서 StorSimple 가상 배열에 프로비전하고 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-127">For VMware, provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="c5d8f-128">Hyper-V에서 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="c5d8f-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="c5d8f-129">VMware에서 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="c5d8f-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="c5d8f-130">3.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-130">3.</span></span> |<span data-ttu-id="c5d8f-131">**가상 배열 설정**</span><span class="sxs-lookup"><span data-stu-id="c5d8f-131">**Set up the Virtual Array**</span></span> |<span data-ttu-id="c5d8f-132">파일 서버에 대해 초기 설정을 수행하고 StorSimple 파일 서버를 등록하고 장치 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-132">For your file server, perform initial setup, register your StorSimple file server, and complete the device setup.</span></span> <span data-ttu-id="c5d8f-133">그런 다음 SMB 공유를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="c5d8f-134">iSCSI 서버에 대해 초기 설정을 수행하고 StorSimple iSCSI 서버를 등록하고 장치 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete the device setup.</span></span> <span data-ttu-id="c5d8f-135">그런 다음 iSCSI 볼륨을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="c5d8f-136">파일 서버로 가상 배열 설정</span><span class="sxs-lookup"><span data-stu-id="c5d8f-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="c5d8f-137">iSCSI 서버로 가상 배열 설정</span><span class="sxs-lookup"><span data-stu-id="c5d8f-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="c5d8f-138">이제 Azure Portal 설치를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-138">You can now begin to set up the Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="c5d8f-139">구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="c5d8f-139">Configuration checklist</span></span>

<span data-ttu-id="c5d8f-140">구성 검사 목록에서는 StorSimple 가상 배열에 소프트웨어를 구성하기 전에 수집해야 하는 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-140">The configuration checklist describes the information that you need to collect before you configure the software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="c5d8f-141">이 정보를 미리 준비하면 사용자 환경에서 StorSimple 장치를 배포하는 과정을 간소화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-141">Preparing this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="c5d8f-142">StorSimple 가상 배열을 파일 서버로 배포할지 iSCSI 서버로 배포할지에 따라서 다음 검사 목록 중 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of the following checklists.</span></span>

* <span data-ttu-id="c5d8f-143">[StorSimple 가상 배열 파일 서버 구성 검사 목록](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-143">Download the [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="c5d8f-144">[StorSimple 가상 배열 iSCSI 서버 구성 검사 목록](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-144">Download the [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5d8f-145">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5d8f-145">Prerequisites</span></span>

<span data-ttu-id="c5d8f-146">여기에는 StorSimple 장치 관리자 서비스, StorSimple 가상 배열, 데이터 센터 네트워크에 대한 필수 조건이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-146">Here you find the configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and the datacenter network.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="c5d8f-147">StorSimple 장치 관리자 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="c5d8f-147">For the StorSimple Device Manager service</span></span>

<span data-ttu-id="c5d8f-148">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="c5d8f-149">액세스 자격 증명이 있는 Microsoft 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="c5d8f-150">액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="c5d8f-151">사용자의 Microsoft Azure 구독을 StorSimple 장치 관리자 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="c5d8f-152">StorSimple 가상 배열의 경우</span><span class="sxs-lookup"><span data-stu-id="c5d8f-152">For the StorSimple Virtual Array</span></span>

<span data-ttu-id="c5d8f-153">가상 배열을 배포하기 전에 다음 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="c5d8f-154">장치 프로비전에 사용될 수 있는 Windows Server 2008 R2 이상 또는 VMware(ESXi 5.5 이상)에서 Hyper-V를 실행하는 호스트 시스템에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-154">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="c5d8f-155">가상 배열을 프로비전하려면 호스트 시스템에서 다음 리소스를 전용으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-155">The host system is able to dedicate the following resources to provision your virtual array:</span></span>
  
  * <span data-ttu-id="c5d8f-156">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="c5d8f-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="c5d8f-157">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="c5d8f-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="c5d8f-158">가상 배열을 파일 서버로서 구성하려는 경우 8GB는 2백만 개의 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-158">If you plan to configure the virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="c5d8f-159">2 - 4백만 개의 파일을 지원하려면 16GB RAM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-159">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="c5d8f-160">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="c5d8f-160">One network interface.</span></span>
  * <span data-ttu-id="c5d8f-161">시스템 데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="c5d8f-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-datacenter-network"></a><span data-ttu-id="c5d8f-162">데이터 센터 네트워크의 경우</span><span class="sxs-lookup"><span data-stu-id="c5d8f-162">For the datacenter network</span></span>

<span data-ttu-id="c5d8f-163">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="c5d8f-164">데이터 센터의 네트워크가 StorSimple 장치에 대한 네트워킹 요구 사항에 따라 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-164">The network in your datacenter is configured as per the networking requirements for your StorSimple device.</span></span> <span data-ttu-id="c5d8f-165">자세한 내용은 [StorSimple 가상 배열 시스템 요구 사항](storsimple-ova-system-requirements.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-165">For more information, see the [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="c5d8f-166">StorSimple 가상 배열에는 전용 5Mbps 인터넷 대역폭(또는 그 이상)을 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="c5d8f-167">이 대역폭은 다른 응용 프로그램과 공유하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="c5d8f-168">단계별 준비</span><span class="sxs-lookup"><span data-stu-id="c5d8f-168">Step-by-step preparation</span></span>

<span data-ttu-id="c5d8f-169">다음 단계별 지침을 사용하여 StorSimple 장치 관리자 서비스용 포털을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-169">Use the following step-by-step instructions to prepare your portal for the StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="c5d8f-170">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c5d8f-170">Step 1: Create a new service</span></span>

<span data-ttu-id="c5d8f-171">StorSimple 장치 관리자 서비스 단일 인스턴스는 여러 StorSimple 가상 배열을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-171">A single instance of the StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="c5d8f-172">StorSimple 장치 관리자 서비스의 인스턴스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-172">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span> <span data-ttu-id="c5d8f-173">가상 배열을 관리하는 기존 StorSimple 장치 관리자 서비스가 있는 경우에는 이 단계를 건너뛰고 [2단계: 서비스 등록 키 가져오기](#step-2-get-the-service-registration-key)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-173">If you have an existing StorSimple Device Manager service to manage your virtual arrays, skip this step and go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="c5d8f-174">서비스와 함께 저장소 계정을 자동으로 만들도록 설정하지 않은 경우, 서비스를 성공적으로 만든 후 하나 이상의 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-174">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="c5d8f-175">저장소 계정을 자동으로 만들지 않은 경우 자세한 지침은 [서비스에 대한 새 저장소 계정 구성](#optional-step-configure-a-new-storage-account-for-the-service) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-175">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="c5d8f-176">저장소 계정을 자동으로 생성하도록 설정한 경우, [2단계: 서비스 등록 키 받기](#step-2-get-the-service-registration-key)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-176">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="c5d8f-177">2단계: 서비스 등록 키 받기</span><span class="sxs-lookup"><span data-stu-id="c5d8f-177">Step 2: Get the service registration key</span></span>

<span data-ttu-id="c5d8f-178">StorSimple 장치 관리자 서비스를 실행한 후에는 서비스 등록 키를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-178">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="c5d8f-179">이 키는 StorSimple 장치를 서비스에 등록 및 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-179">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="c5d8f-180">[Azure Portal](https://portal.azure.com/)에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-180">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="c5d8f-181">서비스 등록 키는 StorSimple 장치 관리자 서비스에 등록해야 하는 모든 StorSimple 장치 관리자 장치를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-181">The service registration key is used to register all the StorSimple Device Manager devices that need to register with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-the-virtual-array-image"></a><span data-ttu-id="c5d8f-182">3단계: 가상 배열 이미지 다운로드</span><span class="sxs-lookup"><span data-stu-id="c5d8f-182">Step 3: Download the virtual array image</span></span>

<span data-ttu-id="c5d8f-183">서비스 등록 키를 확보한 후에는 호스트 시스템에 가상 배열을 프로비전할 적절한 가상 배열 이미지를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-183">After you have the service registration key, you will need to download the appropriate virtual array image to provision a virtual array on your host system.</span></span> <span data-ttu-id="c5d8f-184">가상 배열 이미지는 운영 체제 별로 구분되며 Azure Portal의 빠른 시작 페이지에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-184">The virtual array images are operating system specific and can be downloaded from the Quick Start page in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5d8f-185">StorSimple 가상 배열에서 실행되는 소프트웨어는 StorSimple 장치 관리자 서비스와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-185">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="c5d8f-186">[Azure Portal](https://portal.azure.com/)에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-186">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-get-the-virtual-array-image"></a><span data-ttu-id="c5d8f-187">가상 배열 이미지를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="c5d8f-187">To get the virtual array image</span></span>

1. <span data-ttu-id="c5d8f-188">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-188">Sign into the [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="c5d8f-189">Azure Portal에서 **찾아보기 > StorSimple 장치 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-189">In the Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="c5d8f-190">기존 StorSimple 장치 관리자 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="c5d8f-191">**StorSimple 장치 관리자** 블레이드에서 **빠른 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-191">In the **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="c5d8f-192">Microsoft 다운로드 센터에서 다운로드하려는 이미지에 해당하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-192">Click the link corresponding to the image that you want to download from the Microsoft Download Center.</span></span> <span data-ttu-id="c5d8f-193">이미지 파일은 약 4.8GB입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-193">The image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="c5d8f-194">Windows Server 2012 이상의 Hyper-V용 VHDX</span><span class="sxs-lookup"><span data-stu-id="c5d8f-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="c5d8f-195">Windows Server 2008 R2 이상의 Hyper-V용 VHD</span><span class="sxs-lookup"><span data-stu-id="c5d8f-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="c5d8f-196">VMWare ESXi 5.5 이상용 VMDK</span><span class="sxs-lookup"><span data-stu-id="c5d8f-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="c5d8f-197">파일을 다운로드하고 로컬 드라이브에 압축을 푼 다음 압축을 푼 위치를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-197">Download and unzip the file to a local drive, making a note of where the unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="c5d8f-198">선택적 단계: 서비스에 대한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="c5d8f-198">Optional step: Configure a new storage account for the service</span></span>

<span data-ttu-id="c5d8f-199">이 단계는 선택 사항이며 서비스를 사용하여 저장소 계정을 자동으로 생성하도록 설정하지 않은 경우에만 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-199">This step is optional and should be performed only if you did not enable the automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="c5d8f-200">다른 지역에 Azure Storage 계정을 만들어야 하는 경우 단계별 지침은 [저장소 계정을 만드는 방법](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-200">If you need to create an Azure storage account in a different region, see [How to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="c5d8f-201">기존 Microsoft Azure Storage 계정을 추가하려면 StorSimple 장치 관리자 서비스 페이지의 [Azure Portal](https://ms.portal.azure.com/)에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-201">Perform the following steps in the [Azure portal](https://ms.portal.azure.com/) on the StorSimple Device Manager service page to add an existing Microsoft Azure storage account.</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="c5d8f-202">장치 관리자 서비스와 동일한 Azure 구독에 있는 저장소 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="c5d8f-202">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="c5d8f-203">장치 관리자 서비스를 찾아 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-203">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="c5d8f-204">그러면 **개요** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-204">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="c5d8f-205">**구성** 섹션 내의 **저장소 계정 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-205">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="c5d8f-206">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-206">Click **Add**.</span></span>
4. <span data-ttu-id="c5d8f-207">**저장소 계정 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-207">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="c5d8f-208">**구독**에 **현재**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="c5d8f-209">Azure 저장소 계정의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-209">Provide the name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="c5d8f-210">**사용**을 선택하여 StorSimple 장치와 클라우드 간의 네트워크 통신을 위한 보안 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-210">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="c5d8f-211">사설 클라우드 내에서 작동하는 경우에만 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="c5d8f-212">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-212">Click **Add**.</span></span> <span data-ttu-id="c5d8f-213">저장소 계정이 성공적으로 만들어진 후 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-213">You are notified after the storage account is successfully created.</span></span><br></br>
   
     ![기존 저장소 계정 자격 증명 추가](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="c5d8f-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5d8f-215">Next step</span></span>

<span data-ttu-id="c5d8f-216">다음 단계는 StorSimple 가상 배열에 대한 가상 컴퓨터를 프로비전하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-216">The next step is to provision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="c5d8f-217">호스트 운영 체제에 따라서 다음의 자세한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5d8f-217">Depending on your host operating system, see the detailed instructions in:</span></span>

* [<span data-ttu-id="c5d8f-218">Hyper-V에서 StorSimple 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="c5d8f-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="c5d8f-219">VMware에서 StorSimple 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="c5d8f-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

