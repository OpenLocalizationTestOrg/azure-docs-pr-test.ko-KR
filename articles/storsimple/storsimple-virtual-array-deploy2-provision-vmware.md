---
title: "VMware에서 StorSimple 가상 배열 aaaProvision | Microsoft Docs"
description: "StorSimple 가상 배열 배포 시리즈의 두 번째 자습서에는 VMware에서 가상 장치를 프로비전하는 내용이 포함됩니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a><span data-ttu-id="492e3-103">StorSimple 가상 배열 배포 - VMware에서 프로비전</span><span class="sxs-lookup"><span data-stu-id="492e3-103">Deploy StorSimple Virtual Array - Provision in VMware</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a><span data-ttu-id="492e3-104">개요</span><span class="sxs-lookup"><span data-stu-id="492e3-104">Overview</span></span>
<span data-ttu-id="492e3-105">이 자습서에서는 설명 방법을 tooprovision tooa StorSimple 가상 배열 이상 VMware ESXi 5.5를 실행 하는 호스트 시스템에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-105">This tutorial describes how tooprovision and connect tooa StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span> <span data-ttu-id="492e3-106">이 문서에는 Azure 포털 및 Microsoft Azure Government 클라우드 hello toohello 배포를 StorSimple 가상 배열에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-106">This article applies toohello deployment of StorSimple Virtual Arrays in Azure portal and hello Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="492e3-107">관리자 권한 tooprovision 필요 하 고이 정보를 tooa 가상 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-107">You need administrator privileges tooprovision and connect tooa virtual device.</span></span> <span data-ttu-id="492e3-108">hello 프로 비전 하 고 초기 설치에는 약 10 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-108">hello provisioning and initial setup can take around 10 minutes toocomplete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="492e3-109">프로비전 필수 조건</span><span class="sxs-lookup"><span data-stu-id="492e3-109">Provisioning prerequisites</span></span>
<span data-ttu-id="492e3-110">필수 구성 요소 tooprovision VMware ESXi 5.5를 실행 하는 호스트 시스템에서 가상 장치 hello 및 위에서 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-110">hello prerequisites tooprovision a virtual device on a host system running VMware ESXi 5.5 and above, are as follows.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="492e3-111">Hello StorSimple 장치 관리자 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="492e3-111">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="492e3-112">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="492e3-113">모든 hello 단계를 완료 [StorSimple 가상 배열에 대 한 준비 hello 포털](storsimple-virtual-array-deploy1-portal-prep.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-113">You have completed all hello steps in [Prepare hello portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="492e3-114">Hello Azure 포털에서에서 VMware에 대 한 hello 가상 장치 이미지를 다운로드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-114">You have downloaded hello virtual device image for VMware from hello Azure portal.</span></span> <span data-ttu-id="492e3-115">자세한 내용은 참조 **3 단계: 다운로드 hello 가상 장치 이미지** 의 [StorSimple 가상 배열 가이드에 대 한 준비 hello 포털](storsimple-virtual-array-deploy1-portal-prep.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-115">For more information, see **Step 3: Download hello virtual device image** of [Prepare hello portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

### <a name="for-hello-storsimple-virtual-device"></a><span data-ttu-id="492e3-116">Hello StorSimple 가상 장치에 대 한</span><span class="sxs-lookup"><span data-stu-id="492e3-116">For hello StorSimple virtual device</span></span>
<span data-ttu-id="492e3-117">가상 장치를 배포하기 전에 다음 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-117">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="492e3-118">Hyper-v를 실행 하는 액세스 tooa 호스트 시스템이 준비 (2008 R2 이상 버전)는 수 사용된 tooa 프로 비전 할 수는 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-118">You have access tooa host system running Hyper-V (2008 R2 or later) that can be used tooa provision a device.</span></span>
* <span data-ttu-id="492e3-119">hello 호스트 시스템은 수 toodedicate 가상 장치 리소스 tooprovision 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="492e3-119">hello host system is able toodedicate hello following resources tooprovision your virtual device:</span></span>

  * <span data-ttu-id="492e3-120">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="492e3-120">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="492e3-121">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="492e3-121">At least 8 GB of RAM.</span></span> <span data-ttu-id="492e3-122">파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 보다 작은 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-122">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="492e3-123">16GB RAM toosupport 2-4 백만 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-123">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="492e3-124">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="492e3-124">One network interface.</span></span>
  * <span data-ttu-id="492e3-125">시스템 데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="492e3-125">A 500 GB virtual disk for system data.</span></span>

### <a name="for-hello-network-in-datacenter"></a><span data-ttu-id="492e3-126">Hello 네트워크 데이터 센터에 대 한</span><span class="sxs-lookup"><span data-stu-id="492e3-126">For hello network in datacenter</span></span>
<span data-ttu-id="492e3-127">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-127">Before you begin, make sure that:</span></span>

* <span data-ttu-id="492e3-128">Hello 네트워킹 요구 사항 toodeploy StorSimple 가상 장치 하 고 hello 요구 사항에 따른 구성 된 hello 데이터 센터 네트워크를 검토 했습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-128">You have reviewed hello networking requirements toodeploy a StorSimple virtual device and configured hello datacenter network as per hello requirements.</span></span> 

## <a name="step-by-step-provisioning"></a><span data-ttu-id="492e3-129">단계별 프로비전</span><span class="sxs-lookup"><span data-stu-id="492e3-129">Step-by-step provisioning</span></span>
<span data-ttu-id="492e3-130">tooprovision tooa 가상 장치를 연결 하 고, tooperform hello 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-130">tooprovision and connect tooa virtual device, you need tooperform hello following steps:</span></span>

1. <span data-ttu-id="492e3-131">Hello 호스트 시스템에 충분 한 리소스 toomeet hello 최소 가상 장치 요구 사항에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-131">Ensure that hello host system has sufficient resources toomeet hello minimum virtual device requirements.</span></span>
2. <span data-ttu-id="492e3-132">하이퍼바이저에서 가상 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="492e3-133">Hello 가상 장치를 시작 하 고 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-133">Start hello virtual device and get hello IP address.</span></span>

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="492e3-134">1단계: 호스트 시스템이 최소 가상 장치 요구 사항을 충족하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-134">Step 1: Ensure host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="492e3-135">가상 장치 toocreate이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-135">toocreate a virtual device, you will need:</span></span>

* <span data-ttu-id="492e3-136">VMware ESXi Server 5.5를 실행 하는 액세스 tooa 호스트 시스템 이상.</span><span class="sxs-lookup"><span data-stu-id="492e3-136">Access tooa host system running VMware ESXi Server 5.5 and above.</span></span>
* <span data-ttu-id="492e3-137">시스템 toomanage hello ESXi 호스트에 VMware vSphere 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-137">VMware vSphere client on your system toomanage hello ESXi host.</span></span>

  * <span data-ttu-id="492e3-138">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="492e3-138">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="492e3-139">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="492e3-139">At least 8 GB of RAM.</span></span> <span data-ttu-id="492e3-140">파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 보다 작은 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-140">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="492e3-141">16GB RAM toosupport 2-4 백만 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-141">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="492e3-142">하나 이상의 네트워크 인터페이스 연결 toohello 네트워크 라우팅 트래픽 tooInternet 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-142">One network interface connected toohello network capable of routing traffic tooInternet.</span></span> <span data-ttu-id="492e3-143">hello 최소 인터넷 대역폭 hello 장치의 최적의 작업에 대 한 5 Mbps tooallow 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-143">hello minimum Internet bandwidth should be 5 Mbps tooallow for optimal working of hello device.</span></span>
  * <span data-ttu-id="492e3-144">데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="492e3-144">A 500 GB virtual disk for data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="492e3-145">2단계: 하이퍼바이저에서 가상 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-145">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="492e3-146">Hello 단계 tooprovision 프로그램 하이퍼바이저에서 가상 장치를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-146">Perform hello following steps tooprovision a virtual device in your hypervisor.</span></span>

1. <span data-ttu-id="492e3-147">시스템에 hello 가상 장치 이미지를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-147">Copy hello virtual device image on your system.</span></span> <span data-ttu-id="492e3-148">이 가상 이미지가 hello Azure 포털을 통해 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-148">You downloaded this virtual image through hello Azure portal.</span></span>

   1. <span data-ttu-id="492e3-149">Hello 최신 이미지 파일을 다운로드 한 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-149">Ensure that you have downloaded hello latest image file.</span></span> <span data-ttu-id="492e3-150">이전에 hello 이미지 다운로드 하는 경우 다운로드 다시 tooensure hello 최신 이미지가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-150">If you downloaded hello image earlier, download it again tooensure you have hello latest image.</span></span> <span data-ttu-id="492e3-151">hello 최신 이미지에는 두 개의 파일 (대신 하나)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-151">hello latest image has two files (instead of one).</span></span>
   2. <span data-ttu-id="492e3-152">이 이미지를 사용 하 여 hello 절차의 뒷부분에 나오는 hello 이미지를 복사 했던 hello 위치를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-152">Make a note of hello location where you copied hello image as you are using this image later in hello procedure.</span></span>

2. <span data-ttu-id="492e3-153">Hello vSphere 클라이언트를 사용 하 여 ESXi 서버 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-153">Log in toohello ESXi server using hello vSphere client.</span></span> <span data-ttu-id="492e3-154">Toohave 관리자 권한을 toocreate 가상 컴퓨터 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-154">You need toohave administrator privileges toocreate a virtual machine.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. <span data-ttu-id="492e3-155">Hello 왼쪽된 창에 표시 되는 hello 인벤토리 단원의 hello vSphere 클라이언트 hello ESXi 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-155">In hello vSphere client, in hello inventory section in hello left pane, select hello ESXi Server.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. <span data-ttu-id="492e3-156">Hello VMDK toohello ESXi 서버를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-156">Upload hello VMDK toohello ESXi server.</span></span> <span data-ttu-id="492e3-157">Toohello 이동 **구성** hello 오른쪽 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-157">Navigate toohello **Configuration** tab in hello right pane.</span></span> <span data-ttu-id="492e3-158">**하드웨어** 아래에서 **저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-158">Under **Hardware**, select **Storage**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. <span data-ttu-id="492e3-159">Hello에서 마우스 오른쪽 단추로 창 아래에서 **데이터 저장소**, 선택 hello tooupload hello VMDK를 원하는 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-159">In hello right pane, under **Datastores**, select hello datastore where you want tooupload hello VMDK.</span></span> <span data-ttu-id="492e3-160">hello 데이터 저장소는 충분 한 hello OS에 대비한 여유 공간 및 데이터 디스크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-160">hello datastore must have enough free space for hello OS and data disks.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. <span data-ttu-id="492e3-161">**데이터 저장소 찾아보기**를 마우스 오른쪽 단추를 클릭하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-161">Right-click and select **Browse Datastore**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. <span data-ttu-id="492e3-162">**데이터 저장소 브라우저** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-162">A **Datastore Browser** window appears.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. <span data-ttu-id="492e3-163">Hello 도구 모음에서 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) 아이콘 toocreate 새 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-163">In hello tool bar, click ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icon toocreate a new folder.</span></span> <span data-ttu-id="492e3-164">Hello 폴더 이름을 지정 하 고는 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-164">Specify hello folder name and make a note of it.</span></span> <span data-ttu-id="492e3-165">나중에 가상 컴퓨터를 만들 때 이 폴더 이름을 사용합니다(권장 모범 사례).</span><span class="sxs-lookup"><span data-stu-id="492e3-165">You will use this folder name later when creating a virtual machine (recommended best practice).</span></span> <span data-ttu-id="492e3-166">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-166">Click **OK**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. <span data-ttu-id="492e3-167">hello hello의 왼쪽된 창에 새 폴더가 hello 표시 **데이터 저장소 브라우저**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-167">hello new folder appears in hello left pane of hello **Datastore Browser**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. <span data-ttu-id="492e3-168">Hello 업로드 아이콘 클릭 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) 선택 **파일 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-168">Click hello Upload icon ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) and select **Upload File**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. <span data-ttu-id="492e3-169">탐색 하 고 다운로드 한 toohello VMDK 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-169">Browse and point toohello VMDK files that you downloaded.</span></span> <span data-ttu-id="492e3-170">두 가지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-170">There are two files.</span></span> <span data-ttu-id="492e3-171">파일 tooupload를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-171">Select a file tooupload.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. <span data-ttu-id="492e3-172">**열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-172">Click **Open**.</span></span> <span data-ttu-id="492e3-173">hello VMDK 파일 toohello의 hello 업로드 데이터 저장소 시작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-173">hello upload of hello VMDK file toohello specified datastore starts.</span></span> <span data-ttu-id="492e3-174">파일 tooupload hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-174">It may take several minutes for hello file tooupload.</span></span>
13. <span data-ttu-id="492e3-175">Hello 업로드가 완료 되 면 hello 파일을 hello 데이터 저장소에서 사용자가 만든 hello 폴더에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-175">After hello upload is complete, you see hello file in hello datastore in hello folder you created.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    <span data-ttu-id="492e3-176">이제 두 번째 VMDK 파일 toohello hello 업로드 같은 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-176">Now upload hello second VMDK file toohello same datastore.</span></span>
14. <span data-ttu-id="492e3-177">Toohello vSphere 클라이언트 창을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-177">Return toohello vSphere client window.</span></span> <span data-ttu-id="492e3-178">ESXi 서버를 선택한 상태에서 마우스 오른쪽 단추를 클릭하고 **새 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-178">With ESXi server selected, right-click and select **New Virtual Machine**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. <span data-ttu-id="492e3-179">**새 가상 컴퓨터 만들기** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-179">A **Create New Virtual Machine** window will appear.</span></span> <span data-ttu-id="492e3-180">Hello에 **구성** 페이지, 선택 hello **사용자 지정** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-180">On hello **Configuration** page, select hello **Custom** option.</span></span> <span data-ttu-id="492e3-181">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-181">Click **Next**.</span></span>
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. <span data-ttu-id="492e3-182">Hello에 **이름 및 위치** 페이지에서 가상 컴퓨터의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-182">On hello **Name and Location** page, specify hello name of your virtual machine.</span></span> <span data-ttu-id="492e3-183">이 이름은 8 단계 앞부분에서 지정한 hello 폴더 이름이 (권장된 모범 사례) 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-183">This name should match hello folder name (recommended best practice) you specified earlier in Step 8.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. <span data-ttu-id="492e3-184">Hello에 **저장소** 페이지 toouse tooprovision VM를 원하는 데이터 저장소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-184">On hello **Storage** page, select a datastore you want toouse tooprovision your VM.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. <span data-ttu-id="492e3-185">Hello에 **가상 컴퓨터 버전** 페이지에서 **가상 컴퓨터 버전: 8**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-185">On hello **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span></span> <span data-ttu-id="492e3-186">버전 8 too11 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-186">Versions 8 too11 are all supported.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. <span data-ttu-id="492e3-187">Hello에 **게스트 운영 체제** 페이지, 선택 hello **게스트 운영 체제** 으로 **Windows**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-187">On hello **Guest Operating System** page, select hello **Guest Operating System** as **Windows**.</span></span> <span data-ttu-id="492e3-188">에 대 한 **버전**, hello 드롭다운 목록에서 선택 **Microsoft Windows Server 2012 (64 비트)**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-188">For **Version**, from hello dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. <span data-ttu-id="492e3-189">Hello에 **Cpu** 페이지, hello 조정 **가상 소켓 수** 및 **가상 소켓 당 코어 수가** hello를 하므로 **코어의총수**4 (또는 그 이상)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-189">On hello **CPUs** page, adjust hello **Number of virtual sockets** and **Number of cores per virtual socket** so that hello **Total number of cores** is 4 (or more).</span></span> <span data-ttu-id="492e3-190">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-190">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. <span data-ttu-id="492e3-191">Hello에 **메모리** 페이지 8GB 이상의 ram을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-191">On hello **Memory** page, specify 8 GB (or more) of RAM.</span></span> <span data-ttu-id="492e3-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. <span data-ttu-id="492e3-193">Hello에 **네트워크** 페이지 hello 네트워크 인터페이스의 hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-193">On hello **Network** page, specify hello number of hello network interfaces.</span></span> <span data-ttu-id="492e3-194">최소 요구 사항을 hello는 하나의 네트워크 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-194">hello minimum requirement is one network interface.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. <span data-ttu-id="492e3-195">Hello에 **SCSI 컨트롤러** 페이지에서 기본값을 사용한 hello **LSI 논리 SAS 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-195">On hello **SCSI Controller** page, accept hello default **LSI Logic SAS controller**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. <span data-ttu-id="492e3-196">Hello에 **디스크를 선택** 페이지에서 선택 **기존 가상 디스크를 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-196">On hello **Select a Disk** page, choose **Use an existing virtual disk**.</span></span> <span data-ttu-id="492e3-197">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. <span data-ttu-id="492e3-198">Hello에 **기존 디스크 선택** 페이지의 **디스크 파일 경로**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-198">On hello **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span></span> <span data-ttu-id="492e3-199">**Browse Datastores** (데이터 저장소 찾아보기) 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-199">This opens a **Browse Datastores** dialog.</span></span> <span data-ttu-id="492e3-200">Toohello 위치 hello VMDK 업로드 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-200">Navigate toohello location where you uploaded hello VMDK.</span></span> <span data-ttu-id="492e3-201">Hello 두 개의 파일을 처음 업로드 병합 된 hello 데이터 저장소의 파일 하나만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-201">You now see only one file in hello datastore as hello two files that you initially uploaded have been merged.</span></span> <span data-ttu-id="492e3-202">Hello 파일을 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-202">Select hello file and click **OK**.</span></span> <span data-ttu-id="492e3-203">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-203">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. <span data-ttu-id="492e3-204">Hello에 **고급 옵션** 페이지 hello 기본값을 적용 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-204">On hello **Advanced Options** page, accept hello default and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. <span data-ttu-id="492e3-205">Hello에 **준비 tooComplete** 페이지 hello 새 가상 컴퓨터와 관련 된 모든 hello 설정을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-205">On hello **Ready tooComplete** page, review all hello settings associated with hello new virtual machine.</span></span> <span data-ttu-id="492e3-206">확인 **완료 되기 전에 hello 가상 컴퓨터 설정을 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-206">Check **Edit hello virtual machine settings before completion**.</span></span> <span data-ttu-id="492e3-207">**계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-207">Click **Continue**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. <span data-ttu-id="492e3-208">Hello에 **가상 컴퓨터 속성** 페이지 hello **하드웨어** 탭에서 hello 장치 하드웨어를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-208">On hello **Virtual Machines Properties** page, in hello **Hardware** tab, locate hello device hardware.</span></span> <span data-ttu-id="492e3-209">**새 하드 디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-209">Select **New Hard Disk**.</span></span> <span data-ttu-id="492e3-210">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-210">Click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. <span data-ttu-id="492e3-211">**하드웨어 추가** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-211">You see a **Add Hardware** window.</span></span> <span data-ttu-id="492e3-212">Hello에 **장치 유형** 페이지의 **tooadd 원하는 선택 hello 유형의 장치**선택, **하드 디스크**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-212">On hello **Device Type** page, under **Choose hello type of device you wish tooadd**, select **Hard Disk**, and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. <span data-ttu-id="492e3-213">Hello에 **디스크를 선택** 페이지에서 선택 **새 가상 디스크 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-213">On hello **Select a Disk** page, choose **Create a new virtual disk**.</span></span> <span data-ttu-id="492e3-214">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-214">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. <span data-ttu-id="492e3-215">Hello에 **디스크를 만들** 페이지, hello 변경 **디스크 크기** too500 GB (이상).</span><span class="sxs-lookup"><span data-stu-id="492e3-215">On hello **Create a Disk** page, change hello **Disk Size** too500 GB (or more).</span></span> <span data-ttu-id="492e3-216">500GB hello 최소 요구 사항을 상태인 동안 항상 가장 큰 디스크를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-216">While 500 GB is hello minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="492e3-217">참고 확장 하거나 프로 비전 한 번 hello 디스크를 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-217">Note that you cannot expand or shrink hello disk once provisioned.</span></span> <span data-ttu-id="492e3-218">디스크 tooprovision hello 크기에 자세한 내용은 hello hello 크기 조정 섹션을 검토 [모범 사례 문서](storsimple-ova-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-218">For more information on hello size of disk tooprovision, review hello sizing section in hello [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="492e3-219">**디스크 프로비전**에서 **씬 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-219">Under **Disk Provisioning**, select **Thin Provision**.</span></span> <span data-ttu-id="492e3-220">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-220">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. <span data-ttu-id="492e3-221">Hello에 **고급 옵션** 페이지 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-221">On hello **Advanced Options** page, accept hello default.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. <span data-ttu-id="492e3-222">Hello에 **준비 tooComplete** 페이지 hello 디스크 옵션을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-222">On hello **Ready tooComplete** page, review hello disk options.</span></span> <span data-ttu-id="492e3-223">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-223">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. <span data-ttu-id="492e3-224">Toohello 가상 컴퓨터 속성 페이지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-224">Return toohello Virtual Machine Properties page.</span></span> <span data-ttu-id="492e3-225">새 하드 디스크 tooyour 가상 컴퓨터에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-225">A new hard disk is added tooyour virtual machine.</span></span> <span data-ttu-id="492e3-226">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-226">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. <span data-ttu-id="492e3-227">Hello 오른쪽 창에서 선택한 가상 컴퓨터와 toohello 이동 **요약** 탭 합니다. 가상 컴퓨터에 대 한 hello 설정을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-227">With your virtual machine selected in hello right pane, navigate toohello **Summary** tab. Review hello settings for your virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

<span data-ttu-id="492e3-228">가상 컴퓨터가 프로비전되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-228">Your virtual machine is now provisioned.</span></span> <span data-ttu-id="492e3-229">hello 다음 단계 toopower이이 컴퓨터에 이며 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-229">hello next step is toopower on this machine and get hello IP address.</span></span>

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a><span data-ttu-id="492e3-230">3 단계: hello 가상 장치 시작 및 hello IP 가져오기</span><span class="sxs-lookup"><span data-stu-id="492e3-230">Step 3: Start hello virtual device and get hello IP</span></span>
<span data-ttu-id="492e3-231">가상 장치 hello 단계 toostart 다음을 수행 하 고 tooit를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-231">Perform hello following steps toostart your virtual device and connect tooit.</span></span>

#### <a name="toostart-hello-virtual-device"></a><span data-ttu-id="492e3-232">toostart hello 가상 장치</span><span class="sxs-lookup"><span data-stu-id="492e3-232">toostart hello virtual device</span></span>
1. <span data-ttu-id="492e3-233">Hello 가상 장치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-233">Start hello virtual device.</span></span> <span data-ttu-id="492e3-234">Hello 왼쪽된 창에서 hello vSphere Configuration Manager에서에서 장치를 선택 하 고 toobring hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-234">In hello vSphere Configuration Manager, in hello left pane, select your device and right-click toobring up hello context menu.</span></span> <span data-ttu-id="492e3-235">**전원**을 선택한 후 **전원 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-235">Select **Power** and then select **Power on**.</span></span> <span data-ttu-id="492e3-236">이렇게 하면 가상 컴퓨터의 전원이 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-236">This should power on your virtual machine.</span></span> <span data-ttu-id="492e3-237">Hello 아래쪽에서 hello 상태를 볼 수 **최근 작업** hello vSphere 클라이언트의 창.</span><span class="sxs-lookup"><span data-stu-id="492e3-237">You can view hello status in hello bottom **Recent Tasks** pane of hello vSphere client.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. <span data-ttu-id="492e3-238">hello 설정 작업은 몇 분 toocomplete를 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-238">hello setup tasks will take a few minutes toocomplete.</span></span> <span data-ttu-id="492e3-239">Hello 장치가 실행 되 면 이동 toohello **콘솔** 탭 합니다. Ctrl + Alt + Delete toolog을 toohello 장치에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-239">Once hello device is running, navigate toohello **Console** tab. Send Ctrl+Alt+Delete toolog in toohello device.</span></span> <span data-ttu-id="492e3-240">또는 지점 hello 콘솔 창에 hello 커서 수 있으며 Ctrl + Alt + Insert 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-240">Alternatively, you can point hello cursor on hello console window and press Ctrl+Alt+Insert.</span></span> <span data-ttu-id="492e3-241">hello 기본 사용자가 *StorSimpleAdmin* hello 기본 암호는 및 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-241">hello default user is *StorSimpleAdmin* and hello default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. <span data-ttu-id="492e3-242">보안상의 이유로 hello 처음 로그온 할 때 hello 장치 관리자 암호가 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-242">For security reasons, hello device administrator password expires at hello first logon.</span></span> <span data-ttu-id="492e3-243">입력 정보 요청된 toochange hello 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-243">You are prompted toochange hello password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. <span data-ttu-id="492e3-244">8자 이상을 포함하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-244">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="492e3-245">hello 암호 3 4 가지 항목 중 이러한 요구 사항 포함 해야 합니다: 대문자, 소문자, 숫자 및 특수 문자.</span><span class="sxs-lookup"><span data-stu-id="492e3-245">hello password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="492e3-246">Hello 암호 tooconfirm 다시 입력 것입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-246">Reenter hello password tooconfirm it.</span></span> <span data-ttu-id="492e3-247">알려 hello 암호가 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-247">You will be notified that hello password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. <span data-ttu-id="492e3-248">Hello 암호를 성공적으로 변경 한 후 hello 가상 장치를 다시 부팅 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-248">After hello password is successfully changed, hello virtual device may reboot.</span></span> <span data-ttu-id="492e3-249">Hello 재부팅 toocomplete 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-249">Wait for hello reboot toocomplete.</span></span> <span data-ttu-id="492e3-250">hello 장치의 Windows PowerShell 콘솔 hello 진행률 표시줄을 함께 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-250">hello Windows PowerShell console of hello device may be displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. <span data-ttu-id="492e3-251">6-8단계는 DHCP 환경이 아닌 곳에서 부팅하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-251">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="492e3-252">DHCP 환경에 있는 다음 이러한 단계를 생략 하 고 toostep 9를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-252">If you are in a DHCP environment, then skip these steps and go toostep 9.</span></span> <span data-ttu-id="492e3-253">비 DHCP 환경에서 장치를 부팅 하는 경우 다음 화면 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-253">If you booted up your device in non-DHCP environment, you will see hello following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   <span data-ttu-id="492e3-254">다음으로 hello 네트워크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-254">Next, configure hello network.</span></span>
7. <span data-ttu-id="492e3-255">사용 하 여 hello `Get-HcsIpAddress` 명령 toolist hello 네트워크 인터페이스가 가상 장치에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-255">Use hello `Get-HcsIpAddress` command toolist hello network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="492e3-256">장치에 사용 하도록 설정 하는 단일 네트워크 인터페이스, hello 기본 이름이 할당 toothis 인터페이스 인지 `Ethernet`합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-256">If your device has a single network interface enabled, hello default name assigned toothis interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. <span data-ttu-id="492e3-257">사용 하 여 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-257">Use hello `Set-HcsIpAddress` cmdlet tooconfigure hello network.</span></span> <span data-ttu-id="492e3-258">아래에 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-258">An example is shown below:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. <span data-ttu-id="492e3-259">Hello 초기 설치가 완료 된 후 hello 장치에 부팅 hello 장치 배너 텍스트를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-259">After hello initial setup is complete and hello device has booted up, you will see hello device banner text.</span></span> <span data-ttu-id="492e3-260">Hello IP 주소와 hello 배너 텍스트 toomanage hello 장치에 표시 된 hello URL의 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-260">Make a note of hello IP address and hello URL displayed in hello banner text toomanage hello device.</span></span> <span data-ttu-id="492e3-261">이 IP 주소 tooconnect toohello 웹 가상 장치 하 고 전체 hello 로컬 설치 및 등록의 UI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-261">You will use this IP address tooconnect toohello web UI of your virtual device and complete hello local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. <span data-ttu-id="492e3-262">(선택 사항) 정부 클라우드 hello에 장치를 배포 하는 경우에이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-262">(Optional) Perform this step only if you are deploying your device in hello Government Cloud.</span></span> <span data-ttu-id="492e3-263">장치에서 이제 hello 미국 연방 정보 FIPS (Processing Standard) 모드를 하면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-263">You will now enable hello United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="492e3-264">hello FIPS 140 표준은 hello 중요 한 데이터 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인 하는 암호화 알고리즘을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-264">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span>

    1. <span data-ttu-id="492e3-265">tooenable hello FIPS 모드에서는 hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-265">tooenable hello FIPS mode, run hello following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="492e3-266">암호화 유효성 검사 hello 내용이 적용 되도록 hello FIPS 모드를 활성화 한 후에 장치를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-266">Reboot your device after you have enabled hello FIPS mode so that hello cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="492e3-267">장치에서 FIPS 모드를 사용 또는 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-267">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="492e3-268">FIPS 및 비 FIPS 모드 사이 교대로 반복 되 hello 장치가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-268">Alternating hello device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="492e3-269">장치 hello 최소 구성 요구를 충족 하지 않으면 hello 배너 텍스트 (아래 참조)에 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-269">If your device does not meet hello minimum configuration requirements, you will see an error in hello banner text (shown below).</span></span> <span data-ttu-id="492e3-270">적절 한 리소스 toomeet hello 최소 요구 사항을 갖도록 toomodify hello 장치 구성을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-270">You will need toomodify hello device configuration so that it has adequate resources toomeet hello minimum requirements.</span></span> <span data-ttu-id="492e3-271">그런 다음 다시 시작 하 고 toohello 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-271">You can then restart and connect toohello device.</span></span> <span data-ttu-id="492e3-272">toohello 최소 구성 요구 사항을 참조 [1 단계: hello 호스트 시스템이 최소 가상 장치 요구 사항을 충족 하는지 확인](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-272">Refer toohello minimum configuration requirements in [Step 1: Ensure that hello host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

<span data-ttu-id="492e3-273">Hello 로컬 웹 UI를 사용 하 여 hello 초기 구성 중 다른 오류가 발생 하면 다음 워크플로가 toohello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="492e3-273">If you face any other error during hello initial configuration using hello local web UI, refer toohello following workflows:</span></span>

* <span data-ttu-id="492e3-274">진단 테스트를 너무 실행[웹 UI 설정 문제 해결](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)합니다.</span><span class="sxs-lookup"><span data-stu-id="492e3-274">Run diagnostic tests too[troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="492e3-275">[로그 패키지를 생성하고 로그 파일을 살펴봅니다](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="492e3-275">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="492e3-276">다음 단계</span><span class="sxs-lookup"><span data-stu-id="492e3-276">Next steps</span></span>
* [<span data-ttu-id="492e3-277">StorSimple 가상 배열을 파일 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="492e3-277">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="492e3-278">StorSimple 가상 배열을 iSCSI 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="492e3-278">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
