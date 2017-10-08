---
title: "StorSimple 가상 배열에 대 한 필수 구성 요소 aaaPortal | Microsoft Docs"
description: "첫 번째 자습서 toodeploy StorSimple 가상 배열 hello Azure 포털을 준비가 포함"
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
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a><span data-ttu-id="7c759-103">StorSimple 가상 배열 배포-hello Azure 포털 준비</span><span class="sxs-lookup"><span data-stu-id="7c759-103">Deploy StorSimple Virtual Array - Prepare hello Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="7c759-104">개요</span><span class="sxs-lookup"><span data-stu-id="7c759-104">Overview</span></span>

<span data-ttu-id="7c759-105">이 hello 첫 번째 문서 hello 시리즈의 필요한 배포 자습서 toocompletely hello 리소스 관리자 모델을 사용 하는 iSCSI 서버나 파일 서버와 가상 배열을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-105">This is hello first article in hello series of deployment tutorials required toocompletely deploy your virtual array as a file server or an iSCSI server using hello Resource Manager model.</span></span> <span data-ttu-id="7c759-106">이 문서는 hello 요구 하는 toocreate에 설명 하 고 실행 하 여 StorSimple 장치 관리자 서비스 이전 tooprovisioning 가상 배열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-106">This article describes hello preparation required toocreate and configure your StorSimple Device Manager service prior tooprovisioning a virtual array.</span></span> <span data-ttu-id="7c759-107">이 문서는 때도 tooa 배포 필수 구성 검사 목록 및 구성 요소 out 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-107">This article also links out tooa deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="7c759-108">관리자는 권한이 toocomplete hello 설정 및 구성 프로세스를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-108">You need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="7c759-109">시작 하기 전에 hello 배포 구성 검사 목록 검토 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-109">We recommend that you review hello deployment configuration checklist before you begin.</span></span> <span data-ttu-id="7c759-110">hello 포털 준비 보다 작은 10 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-110">hello portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="7c759-111">이 문서에 게시 된 hello 정보 toohello hello Azure 포털에서에서 StorSimple 가상 배열 및 Microsoft Azure Government 클라우드 배포를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-111">hello information published in this article applies toohello deployment of StorSimple Virtual Arrays in hello Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="7c759-112">시작</span><span class="sxs-lookup"><span data-stu-id="7c759-112">Get started</span></span>
<span data-ttu-id="7c759-113">hello 배포 워크플로 hello 포털을 준비 하 고, 가상화 된 환경의 가상 배열 프로 비전, hello 설치 완료 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-113">hello deployment workflow consists of preparing hello portal, provisioning a virtual array in your virtualized environment, and completing hello setup.</span></span> <span data-ttu-id="7c759-114">파일 서버 또는 iSCSI 서버로 hello StorSimple 가상 배열 배포 시작 tooget, 벡터 리소스 다음 toorefer toohello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-114">tooget started with hello StorSimple Virtual Array deployment as a file server or an iSCSI server, you need toorefer toohello following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="7c759-115">배포 문서</span><span class="sxs-lookup"><span data-stu-id="7c759-115">Deployment articles</span></span>

<span data-ttu-id="7c759-116">toodeploy StorSimple 가상 배열 toohello 문서 미리 시퀀스를 지정 하는 hello에서는 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7c759-116">toodeploy your StorSimple Virtual Array, refer toohello following articles in hello prescribed sequence.</span></span>

| **#** | <span data-ttu-id="7c759-117">**단계**</span><span class="sxs-lookup"><span data-stu-id="7c759-117">**In this step**</span></span> | <span data-ttu-id="7c759-118">**이 작업을 수행합니다…**</span><span class="sxs-lookup"><span data-stu-id="7c759-118">**You do this …**</span></span> | <span data-ttu-id="7c759-119">**그리고 이러한 문서를 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="7c759-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7c759-120">1.</span><span class="sxs-lookup"><span data-stu-id="7c759-120">1.</span></span> |<span data-ttu-id="7c759-121">**Azure 포털 hello 설정**</span><span class="sxs-lookup"><span data-stu-id="7c759-121">**Set up hello Azure portal**</span></span> |<span data-ttu-id="7c759-122">만들기 및 실행 하 여 StorSimple 장치 관리자 서비스 이전 tooprovisioning StorSimple 가상 배열 구성.</span><span class="sxs-lookup"><span data-stu-id="7c759-122">Create and configure your StorSimple Device Manager service prior tooprovisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="7c759-123">Hello 포털 준비</span><span class="sxs-lookup"><span data-stu-id="7c759-123">Prepare hello portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="7c759-124">2.</span><span class="sxs-lookup"><span data-stu-id="7c759-124">2.</span></span> |<span data-ttu-id="7c759-125">**가상 배열 hello를 프로 비전**</span><span class="sxs-lookup"><span data-stu-id="7c759-125">**Provision hello Virtual Array**</span></span> |<span data-ttu-id="7c759-126">Hyper-v에 대 한 프로 비전 하 고 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2에서 Hyper-v를 실행 중인 호스트 시스템에서 StorSimple 가상 배열 tooa를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-126">For Hyper-V, provision and connect tooa StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="7c759-127">VMware에 대 한 프로 비전 및 tooa StorSimple 가상 배열 이상 VMware ESXi 5.5를 실행 하는 호스트 시스템에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-127">For VMware, provision and connect tooa StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="7c759-128">Hyper-V에서 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="7c759-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="7c759-129">VMware에서 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="7c759-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="7c759-130">3.</span><span class="sxs-lookup"><span data-stu-id="7c759-130">3.</span></span> |<span data-ttu-id="7c759-131">**가상 배열 hello 설정**</span><span class="sxs-lookup"><span data-stu-id="7c759-131">**Set up hello Virtual Array**</span></span> |<span data-ttu-id="7c759-132">파일 서버에 대 한 초기 설치를 수행 하 고 StorSimple 파일 서버를 등록 hello 장치 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-132">For your file server, perform initial setup, register your StorSimple file server, and complete hello device setup.</span></span> <span data-ttu-id="7c759-133">그런 다음 SMB 공유를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="7c759-134">ISCSI 서버에 대 한 초기 설치를 수행 하 고 StorSimple iSCSI 서버를 등록 hello 장치 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete hello device setup.</span></span> <span data-ttu-id="7c759-135">그런 다음 iSCSI 볼륨을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="7c759-136">파일 서버로 가상 배열 설정</span><span class="sxs-lookup"><span data-stu-id="7c759-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="7c759-137">iSCSI 서버로 가상 배열 설정</span><span class="sxs-lookup"><span data-stu-id="7c759-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="7c759-138">이제 tooset hello Azure 포털을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-138">You can now begin tooset up hello Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="7c759-139">구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="7c759-139">Configuration checklist</span></span>

<span data-ttu-id="7c759-140">hello 필요한 정보를 toocollect StorSimple 가상 배열에 hello 소프트웨어를 구성 하기 전에 hello 구성 검사 목록에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-140">hello configuration checklist describes hello information that you need toocollect before you configure hello software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="7c759-141">이 정보를 사용 하면 시간 미리 약식 hello 프로세스의 사용자 환경에서 hello StorSimple 장치 배포를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-141">Preparing this information ahead of time helps streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="7c759-142">StorSimple 가상 배열 하는 파일 서버 또는 iSCSI 서버로 배포 되었는지 여부에 따라 필요 하면 다음 검사 목록을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of hello following checklists.</span></span>

* <span data-ttu-id="7c759-143">Hello 다운로드 [StorSimple 가상 배열 파일 서버 구성 검사 목록](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-143">Download hello [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="7c759-144">Hello 다운로드 [StorSimple 가상 배열 iSCSI 서버 구성 검사 목록](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-144">Download hello [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c759-145">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c759-145">Prerequisites</span></span>

<span data-ttu-id="7c759-146">여기에 StorSimple 장치 관리자 서비스, StorSimple 가상 배열 및 hello 데이터 센터 네트워크 hello 구성 필수 구성 요소를 찾을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-146">Here you find hello configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and hello datacenter network.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="7c759-147">Hello StorSimple 장치 관리자 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="7c759-147">For hello StorSimple Device Manager service</span></span>

<span data-ttu-id="7c759-148">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="7c759-149">액세스 자격 증명이 있는 Microsoft 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="7c759-150">액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="7c759-151">사용자의 Microsoft Azure 구독을 StorSimple 장치 관리자 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="7c759-152">StorSimple 가상 배열 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="7c759-152">For hello StorSimple Virtual Array</span></span>

<span data-ttu-id="7c759-153">가상 배열을 배포하기 전에 다음 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="7c759-154">이상 버전에서 Windows Server 2008 R2 Hyper-v를 실행 하는 액세스 tooa 호스트 시스템이 준비 또는 VMware (ESXi 5.5) tooa 사용된 될 수 있는 장치를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-154">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used tooa provision a device.</span></span>
* <span data-ttu-id="7c759-155">hello 호스트 시스템은 수 toodedicate 가상 배열 리소스 tooprovision 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="7c759-155">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>
  
  * <span data-ttu-id="7c759-156">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="7c759-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="7c759-157">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="7c759-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="7c759-158">파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-158">If you plan tooconfigure hello virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="7c759-159">16GB RAM toosupport 2-4 백만 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-159">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="7c759-160">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="7c759-160">One network interface.</span></span>
  * <span data-ttu-id="7c759-161">시스템 데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="7c759-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-hello-datacenter-network"></a><span data-ttu-id="7c759-162">Hello 데이터 센터 네트워크에 대 한</span><span class="sxs-lookup"><span data-stu-id="7c759-162">For hello datacenter network</span></span>

<span data-ttu-id="7c759-163">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="7c759-164">데이터 센터에서 hello 네트워크 hello StorSimple 장치의 네트워킹 요구 사항을 기준으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-164">hello network in your datacenter is configured as per hello networking requirements for your StorSimple device.</span></span> <span data-ttu-id="7c759-165">자세한 내용은 참조 hello [StorSimple 가상 배열 시스템 요구 사항](storsimple-ova-system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-165">For more information, see hello [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="7c759-166">StorSimple 가상 배열에는 전용 5Mbps 인터넷 대역폭(또는 그 이상)을 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="7c759-167">이 대역폭은 다른 응용 프로그램과 공유하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="7c759-168">단계별 준비</span><span class="sxs-lookup"><span data-stu-id="7c759-168">Step-by-step preparation</span></span>

<span data-ttu-id="7c759-169">Hello StorSimple 장치 관리자 서비스에 대 한 단계별 지침 tooprepare 다음 hello 귀하의 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-169">Use hello following step-by-step instructions tooprepare your portal for hello StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="7c759-170">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7c759-170">Step 1: Create a new service</span></span>

<span data-ttu-id="7c759-171">Hello StorSimple 장치 관리자 서비스의 단일 인스턴스에 여러 개의 StorSimple 가상 배열을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-171">A single instance of hello StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="7c759-172">Hello 단계 toocreate hello StorSimple 장치 관리자 서비스의 인스턴스를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-172">Perform hello following steps toocreate an instance of hello StorSimple Device Manager service.</span></span> <span data-ttu-id="7c759-173">가상 배열에서는 기존 StorSimple 장치 관리자 서비스 toomanage을 설정한 경우이 단계를 건너뜁니다 고 너무 이동[2 단계: Get hello 서비스 등록 키](#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-173">If you have an existing StorSimple Device Manager service toomanage your virtual arrays, skip this step and go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="7c759-174">Toocreate 할 서비스와 저장소 계정의 hello 자동 생성을 설정 하지 않은 경우 저장소 계정을 하나 이상 후 서비스를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-174">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="7c759-175">저장소 계정을 자동으로 만들 하지 않은 경우 너무 이동[hello 서비스에 대 한 새 저장소 계정 구성](#optional-step-configure-a-new-storage-account-for-the-service) 자세한 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-175">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="7c759-176">저장소 계정의 hello 자동 생성을 사용 하도록 설정한 경우 너무 이동[2 단계: Get hello 서비스 등록 키](#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-176">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="7c759-177">2 단계: hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="7c759-177">Step 2: Get hello service registration key</span></span>

<span data-ttu-id="7c759-178">Hello StorSimple 장치 관리자 서비스가 실행 되 고, tooget hello 서비스 등록 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-178">After hello StorSimple Device Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="7c759-179">이 키가 사용 되는 tooregister를 hello 서비스와 StorSimple 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-179">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="7c759-180">Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-180">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="7c759-181">hello 서비스 등록 키를 사용 하는 tooregister 모든 hello tooregister StorSimple 장치 관리자 서비스에 문의 해야 하는 StorSimple 장치 관리자 장치.</span><span class="sxs-lookup"><span data-stu-id="7c759-181">hello service registration key is used tooregister all hello StorSimple Device Manager devices that need tooregister with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a><span data-ttu-id="7c759-182">3 단계: hello 가상 배열 이미지 다운로드</span><span class="sxs-lookup"><span data-stu-id="7c759-182">Step 3: Download hello virtual array image</span></span>

<span data-ttu-id="7c759-183">Hello 서비스 등록 키를 사용 하는 다음 toodownload hello 적절 한 가상 배열 이미지 tooprovision 가상 배열 호스트 시스템에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-183">After you have hello service registration key, you will need toodownload hello appropriate virtual array image tooprovision a virtual array on your host system.</span></span> <span data-ttu-id="7c759-184">hello 가상 배열 이미지는 특정 운영 체제 및 hello hello Azure 포털의에서 빠른 시작 페이지에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-184">hello virtual array images are operating system specific and can be downloaded from hello Quick Start page in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c759-185">hello StorSimple 가상 배열에서 실행 중인 hello 소프트웨어 hello StorSimple 장치 관리자 서비스와만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-185">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="7c759-186">Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-186">Perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="tooget-hello-virtual-array-image"></a><span data-ttu-id="7c759-187">tooget hello 가상 배열 이미지</span><span class="sxs-lookup"><span data-stu-id="7c759-187">tooget hello virtual array image</span></span>

1. <span data-ttu-id="7c759-188">Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-188">Sign into hello [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="7c759-189">Hello Azure 포털에서에서 클릭 **찾아보기 > StorSimple 장치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-189">In hello Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="7c759-190">기존 StorSimple 장치 관리자 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="7c759-191">Hello에 **StorSimple 장치 관리자** 블레이드에서 클릭 **빠른 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-191">In hello **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="7c759-192">Hello 링크 해당 toohello 이미지 hello Microsoft 다운로드 센터에서에서 toodownload 한다는 것을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-192">Click hello link corresponding toohello image that you want toodownload from hello Microsoft Download Center.</span></span> <span data-ttu-id="7c759-193">hello 이미지 파일은 약 4.8 g B입니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-193">hello image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="7c759-194">Windows Server 2012 이상의 Hyper-V용 VHDX</span><span class="sxs-lookup"><span data-stu-id="7c759-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="7c759-195">Windows Server 2008 R2 이상의 Hyper-V용 VHD</span><span class="sxs-lookup"><span data-stu-id="7c759-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="7c759-196">VMWare ESXi 5.5 이상용 VMDK</span><span class="sxs-lookup"><span data-stu-id="7c759-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="7c759-197">다운로드 하 고 hello 파일 tooa 로컬 드라이브를 한 노트는 hello 압축 푼된 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-197">Download and unzip hello file tooa local drive, making a note of where hello unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="7c759-198">선택적 단계: hello 서비스에 대 한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="7c759-198">Optional step: Configure a new storage account for hello service</span></span>

<span data-ttu-id="7c759-199">이 단계는 선택 사항이 며 서비스와 저장소 계정의 hello 자동 만들기를 활성화 하지 않은 경우에 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-199">This step is optional and should be performed only if you did not enable hello automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="7c759-200">Toocreate Azure 저장소 계정을 다른 지역에 필요한 경우 참조 [어떻게 toocreate 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계별 지침.</span><span class="sxs-lookup"><span data-stu-id="7c759-200">If you need toocreate an Azure storage account in a different region, see [How toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="7c759-201">Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://ms.portal.azure.com/) hello StorSimple 장치 관리자 서비스 페이지 tooadd 기존 Microsoft Azure 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-201">Perform hello following steps in hello [Azure portal](https://ms.portal.azure.com/) on hello StorSimple Device Manager service page tooadd an existing Microsoft Azure storage account.</span></span>

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a><span data-ttu-id="7c759-202">저장소 계정 자격 증명 tooadd hello hello 장치 관리자 서비스와 동일한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="7c759-202">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>

1. <span data-ttu-id="7c759-203">Tooyour 장치 관리자 서비스를 찾아 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-203">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="7c759-204">Hello 열립니다 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-204">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="7c759-205">선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="7c759-205">Select **Storage account credentials** within hello **Configuration** section.</span></span>
3. <span data-ttu-id="7c759-206">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-206">Click **Add**.</span></span>
4. <span data-ttu-id="7c759-207">Hello에 **저장소 계정 추가** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-207">In hello **Add a storage account** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="7c759-208">**구독**에 **현재**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="7c759-209">Azure 저장소 계정의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-209">Provide hello name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="7c759-210">선택 **사용** toocreate StorSimple 장치 및 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-210">Select **Enable** toocreate a secure channel for network communication between your StorSimple device and hello cloud.</span></span> <span data-ttu-id="7c759-211">사설 클라우드 내에서 작동하는 경우에만 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="7c759-212">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-212">Click **Add**.</span></span> <span data-ttu-id="7c759-213">Hello 저장소 계정이 정상적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c759-213">You are notified after hello storage account is successfully created.</span></span><br></br>
   
     ![기존 저장소 계정 자격 증명 추가](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="7c759-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c759-215">Next step</span></span>

<span data-ttu-id="7c759-216">hello 다음 단계는 tooprovision StorSimple 가상 배열에 대 한 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="7c759-216">hello next step is tooprovision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="7c759-217">호스트 운영 체제에 따라 참조 hello에 필요한 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="7c759-217">Depending on your host operating system, see hello detailed instructions in:</span></span>

* [<span data-ttu-id="7c759-218">Hyper-V에서 StorSimple 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="7c759-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="7c759-219">VMware에서 StorSimple 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="7c759-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

