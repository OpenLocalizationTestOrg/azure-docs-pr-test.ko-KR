---
title: "VMware에서 StorSimple Virtual Array 프로비전 | Microsoft Docs"
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
ms.openlocfilehash: 118521a127b2e4b765efabdbdde71605440d81c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a><span data-ttu-id="40b83-103">StorSimple 가상 배열 배포 - VMware에서 프로비전</span><span class="sxs-lookup"><span data-stu-id="40b83-103">Deploy StorSimple Virtual Array - Provision in VMware</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a><span data-ttu-id="40b83-104">개요</span><span class="sxs-lookup"><span data-stu-id="40b83-104">Overview</span></span>
<span data-ttu-id="40b83-105">이 자습서는 VMware ESXi 5.5 이상을 실행하는 호스트 시스템에 StorSimple 가상 배열을 프로비전하고 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-105">This tutorial describes how to provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span> <span data-ttu-id="40b83-106">이 문서는 Azure Portal 및 Microsoft Azure Government 클라우드에서 StorSimple 가상 배열의 배포에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and the Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="40b83-107">가상 장치를 프로비전하고 연결하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-107">You need administrator privileges to provision and connect to a virtual device.</span></span> <span data-ttu-id="40b83-108">프로비전 및 초기 설정을 완료하는 데 10분 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="40b83-109">프로비전 필수 조건</span><span class="sxs-lookup"><span data-stu-id="40b83-109">Provisioning prerequisites</span></span>
<span data-ttu-id="40b83-110">VMware ESXi 5.5 이상을 실행하는 호스트 시스템에 가상 장치를 프로비전하기 위한 필수 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-110">The prerequisites to provision a virtual device on a host system running VMware ESXi 5.5 and above, are as follows.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="40b83-111">StorSimple 장치 관리자 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="40b83-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="40b83-112">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="40b83-113">[StorSimple 가상 배열용 포털 준비](storsimple-virtual-array-deploy1-portal-prep.md)의 모든 단계를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="40b83-114">Azure 포털에서 VMware용 가상 장치 이미지를 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-114">You have downloaded the virtual device image for VMware from the Azure portal.</span></span> <span data-ttu-id="40b83-115">자세한 내용은 [StorSimple 가상 배열을 위한 포털 준비 가이드](storsimple-virtual-array-deploy1-portal-prep.md)의 **3단계: 가상 장치 이미지 다운로드**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40b83-115">For more information, see **Step 3: Download the virtual device image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

### <a name="for-the-storsimple-virtual-device"></a><span data-ttu-id="40b83-116">StorSimple 가상 장치의 경우</span><span class="sxs-lookup"><span data-stu-id="40b83-116">For the StorSimple virtual device</span></span>
<span data-ttu-id="40b83-117">가상 장치를 배포하기 전에 다음 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-117">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="40b83-118">장치 프로비전에 사용될 수 있는 Hyper-V(2008 R2 이상)를 실행하는 호스트 시스템에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-118">You have access to a host system running Hyper-V (2008 R2 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="40b83-119">가상 디스크 프로비전을 위해 호스트 시스템에서 다음 리소스를 전용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-119">The host system is able to dedicate the following resources to provision your virtual device:</span></span>

  * <span data-ttu-id="40b83-120">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="40b83-120">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="40b83-121">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="40b83-121">At least 8 GB of RAM.</span></span> <span data-ttu-id="40b83-122">가상 배열을 파일 서버로서 구성하려는 경우 8GB는 2백만 개 미만의 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-122">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="40b83-123">2 - 4백만 개의 파일을 지원하려면 16GB RAM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-123">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="40b83-124">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="40b83-124">One network interface.</span></span>
  * <span data-ttu-id="40b83-125">시스템 데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="40b83-125">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-network-in-datacenter"></a><span data-ttu-id="40b83-126">데이터 센터 네트워크의 경우</span><span class="sxs-lookup"><span data-stu-id="40b83-126">For the network in datacenter</span></span>
<span data-ttu-id="40b83-127">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-127">Before you begin, make sure that:</span></span>

* <span data-ttu-id="40b83-128">StorSimple 가상 장치를 배포하기 위한 네트워킹 요구 사항을 검토하고, 요구 사항에 따라 데이터 센터 네트워크를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-128">You have reviewed the networking requirements to deploy a StorSimple virtual device and configured the datacenter network as per the requirements.</span></span> 

## <a name="step-by-step-provisioning"></a><span data-ttu-id="40b83-129">단계별 프로비전</span><span class="sxs-lookup"><span data-stu-id="40b83-129">Step-by-step provisioning</span></span>
<span data-ttu-id="40b83-130">가상 장치를 프로비전하고 연결하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-130">To provision and connect to a virtual device, you need to perform the following steps:</span></span>

1. <span data-ttu-id="40b83-131">호스트 시스템에 최소 가상 장치 요구 사항을 충족하기에 충분한 리소스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span></span>
2. <span data-ttu-id="40b83-132">하이퍼바이저에서 가상 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="40b83-133">가상 장치를 시작하고 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-133">Start the virtual device and get the IP address.</span></span>

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="40b83-134">1단계: 호스트 시스템이 최소 가상 장치 요구 사항을 충족하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-134">Step 1: Ensure host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="40b83-135">가상 장치를 만들려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-135">To create a virtual device, you will need:</span></span>

* <span data-ttu-id="40b83-136">VMware ESXi Server 5.5 이상을 실행하는 호스트 시스템에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="40b83-136">Access to a host system running VMware ESXi Server 5.5 and above.</span></span>
* <span data-ttu-id="40b83-137">ESXi 호스트를 관리하기 위한 시스템의 VMware vSphere 클라이언트</span><span class="sxs-lookup"><span data-stu-id="40b83-137">VMware vSphere client on your system to manage the ESXi host.</span></span>

  * <span data-ttu-id="40b83-138">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="40b83-138">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="40b83-139">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="40b83-139">At least 8 GB of RAM.</span></span> <span data-ttu-id="40b83-140">가상 배열을 파일 서버로서 구성하려는 경우 8GB는 2백만 개 미만의 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-140">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="40b83-141">2 - 4백만 개의 파일을 지원하려면 16GB RAM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-141">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="40b83-142">인터넷으로 트래픽을 라우팅할 수 있는 네트워크에 연결된 네트워크 인터페이스 하나.</span><span class="sxs-lookup"><span data-stu-id="40b83-142">One network interface connected to the network capable of routing traffic to Internet.</span></span> <span data-ttu-id="40b83-143">장치가 최적으로 작동할 수 있도록 허용하는 최소 인터넷 대역폭은 5Mbps입니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-143">The minimum Internet bandwidth should be 5 Mbps to allow for optimal working of the device.</span></span>
  * <span data-ttu-id="40b83-144">데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="40b83-144">A 500 GB virtual disk for data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="40b83-145">2단계: 하이퍼바이저에서 가상 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-145">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="40b83-146">하이퍼바이저에서 가상 장치를 프로비전하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-146">Perform the following steps to provision a virtual device in your hypervisor.</span></span>

1. <span data-ttu-id="40b83-147">시스템에서 가상 장치 이미지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-147">Copy the virtual device image on your system.</span></span> <span data-ttu-id="40b83-148">Azure Portal을 통해 이 가상 이미지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-148">You downloaded this virtual image through the Azure portal.</span></span>

   1. <span data-ttu-id="40b83-149">최신 이미지 파일을 다운로드했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-149">Ensure that you have downloaded the latest image file.</span></span> <span data-ttu-id="40b83-150">이전에 이미지를 다운로드한 경우 최신 이미지인지 확인하기 위해 다시 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-150">If you downloaded the image earlier, download it again to ensure you have the latest image.</span></span> <span data-ttu-id="40b83-151">최신 이미지에는 하나가 아니라 두 개의 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-151">The latest image has two files (instead of one).</span></span>
   2. <span data-ttu-id="40b83-152">나중에 절차에서 이 이미지를 사용하므로 이미지를 복사한 위치를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>

2. <span data-ttu-id="40b83-153">vSphere 클라이언트를 사용하여 ESXi 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-153">Log in to the ESXi server using the vSphere client.</span></span> <span data-ttu-id="40b83-154">가상 컴퓨터를 만들려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-154">You need to have administrator privileges to create a virtual machine.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. <span data-ttu-id="40b83-155">vSphere 클라이언트 왼쪽 창의 인벤토리 섹션에서 ESXi 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-155">In the vSphere client, in the inventory section in the left pane, select the ESXi Server.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. <span data-ttu-id="40b83-156">ESXi 서버에 VMDK를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-156">Upload the VMDK to the ESXi server.</span></span> <span data-ttu-id="40b83-157">오른쪽 창의 **구성** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-157">Navigate to the **Configuration** tab in the right pane.</span></span> <span data-ttu-id="40b83-158">**하드웨어** 아래에서 **저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-158">Under **Hardware**, select **Storage**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. <span data-ttu-id="40b83-159">오른쪽 창의 **데이터 저장소**아래에서 VMDK를 업로드할 데이터 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-159">In the right pane, under **Datastores**, select the datastore where you want to upload the VMDK.</span></span> <span data-ttu-id="40b83-160">데이터 저장소에는 OS 및 데이터 디스크에 충분한 여유 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-160">The datastore must have enough free space for the OS and data disks.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. <span data-ttu-id="40b83-161">**데이터 저장소 찾아보기**를 마우스 오른쪽 단추를 클릭하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-161">Right-click and select **Browse Datastore**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. <span data-ttu-id="40b83-162">**데이터 저장소 브라우저** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-162">A **Datastore Browser** window appears.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. <span data-ttu-id="40b83-163">도구 모음에서 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) 아이콘을 클릭하여 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-163">In the tool bar, click ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icon to create a new folder.</span></span> <span data-ttu-id="40b83-164">폴더 이름을 지정하고 해당 이름을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-164">Specify the folder name and make a note of it.</span></span> <span data-ttu-id="40b83-165">나중에 가상 컴퓨터를 만들 때 이 폴더 이름을 사용합니다(권장 모범 사례).</span><span class="sxs-lookup"><span data-stu-id="40b83-165">You will use this folder name later when creating a virtual machine (recommended best practice).</span></span> <span data-ttu-id="40b83-166">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-166">Click **OK**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. <span data-ttu-id="40b83-167">새 폴더가 **데이터 저장소 브라우저**의 왼쪽 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-167">The new folder appears in the left pane of the **Datastore Browser**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. <span data-ttu-id="40b83-168">업로드 아이콘 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png)을 클릭하고 **파일 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-168">Click the Upload icon ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) and select **Upload File**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. <span data-ttu-id="40b83-169">다운로드한 VMDK 파일을 찾아서 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-169">Browse and point to the VMDK files that you downloaded.</span></span> <span data-ttu-id="40b83-170">두 가지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-170">There are two files.</span></span> <span data-ttu-id="40b83-171">업로드할 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-171">Select a file to upload.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. <span data-ttu-id="40b83-172">**열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-172">Click **Open**.</span></span> <span data-ttu-id="40b83-173">VMDK 파일을 지정된 데이터 저장소에 업로드하는 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-173">The upload of the VMDK file to the specified datastore starts.</span></span> <span data-ttu-id="40b83-174">파일 업로드에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-174">It may take several minutes for the file to upload.</span></span>
13. <span data-ttu-id="40b83-175">업로드가 완료되면 사용자가 만든 폴더의 데이터 저장소에 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-175">After the upload is complete, you see the file in the datastore in the folder you created.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    <span data-ttu-id="40b83-176">두 번째 VMDK 파일을 동일한 데이터 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-176">Now upload the second VMDK file to the same datastore.</span></span>
14. <span data-ttu-id="40b83-177">vSphere 클라이언트 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-177">Return to the vSphere client window.</span></span> <span data-ttu-id="40b83-178">ESXi 서버를 선택한 상태에서 마우스 오른쪽 단추를 클릭하고 **새 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-178">With ESXi server selected, right-click and select **New Virtual Machine**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. <span data-ttu-id="40b83-179">**새 가상 컴퓨터 만들기** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-179">A **Create New Virtual Machine** window will appear.</span></span> <span data-ttu-id="40b83-180">**구성** 페이지에서 **사용자 지정** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-180">On the **Configuration** page, select the **Custom** option.</span></span> <span data-ttu-id="40b83-181">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-181">Click **Next**.</span></span>
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. <span data-ttu-id="40b83-182">**이름 및 위치** 페이지에서 가상 컴퓨터의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-182">On the **Name and Location** page, specify the name of your virtual machine.</span></span> <span data-ttu-id="40b83-183">이 이름은 앞서 8단계에서 지정한 폴더 이름(권장 모범 사례)과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-183">This name should match the folder name (recommended best practice) you specified earlier in Step 8.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. <span data-ttu-id="40b83-184">**저장소** 페이지에서 VM을 프로비전하는 데 사용할 데이터 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-184">On the **Storage** page, select a datastore you want to use to provision your VM.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. <span data-ttu-id="40b83-185">**가상 컴퓨터 버전** 페이지에서 **가상 컴퓨터 버전: 8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-185">On the **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span></span> <span data-ttu-id="40b83-186">버전 8~11이 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-186">Versions 8 to 11 are all supported.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. <span data-ttu-id="40b83-187">**게스트 운영 체제** 페이지에서 **게스트 운영 체제**를 **Windows**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-187">On the **Guest Operating System** page, select the **Guest Operating System** as **Windows**.</span></span> <span data-ttu-id="40b83-188">**버전**은 드롭다운 목록에서 **Microsoft Windows Server 2012(64비트)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-188">For **Version**, from the dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. <span data-ttu-id="40b83-189">**CPU** 페이지에서 **총 코어 수**가 4(또는 그 이상)가 되도록 **가상 소켓의 수** 및 **가상 소켓 당 코어의 수**를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-189">On the **CPUs** page, adjust the **Number of virtual sockets** and **Number of cores per virtual socket** so that the **Total number of cores** is 4 (or more).</span></span> <span data-ttu-id="40b83-190">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-190">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. <span data-ttu-id="40b83-191">**메모리** 페이지에서 RAM을 8GB(또는 그 이상)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-191">On the **Memory** page, specify 8 GB (or more) of RAM.</span></span> <span data-ttu-id="40b83-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. <span data-ttu-id="40b83-193">**네트워크** 페이지에서 네트워크 인터페이스의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-193">On the **Network** page, specify the number of the network interfaces.</span></span> <span data-ttu-id="40b83-194">최소 요구 사항은 네트워크 인터페이스 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-194">The minimum requirement is one network interface.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. <span data-ttu-id="40b83-195">**SCSI 컨트롤러** 페이지에서 기본 **LSI Logic SAS 컨트롤러**를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-195">On the **SCSI Controller** page, accept the default **LSI Logic SAS controller**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. <span data-ttu-id="40b83-196">**디스크 선택** 페이지에서 **기존 가상 디스크 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-196">On the **Select a Disk** page, choose **Use an existing virtual disk**.</span></span> <span data-ttu-id="40b83-197">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. <span data-ttu-id="40b83-198">**기존 디스크 선택** 페이지의 **디스크 파일 경로** 아래에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-198">On the **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span></span> <span data-ttu-id="40b83-199">**Browse Datastores** (데이터 저장소 찾아보기) 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-199">This opens a **Browse Datastores** dialog.</span></span> <span data-ttu-id="40b83-200">VMDK를 업로드한 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-200">Navigate to the location where you uploaded the VMDK.</span></span> <span data-ttu-id="40b83-201">이제 처음에 업로드한 두 개의 파일이 병합되었으므로 데이터 저장소에 하나의 파일만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-201">You now see only one file in the datastore as the two files that you initially uploaded have been merged.</span></span> <span data-ttu-id="40b83-202">파일을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-202">Select the file and click **OK**.</span></span> <span data-ttu-id="40b83-203">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-203">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. <span data-ttu-id="40b83-204">**고급 옵션** 페이지에서 기본값을 적용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-204">On the **Advanced Options** page, accept the default and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. <span data-ttu-id="40b83-205">**Ready to Complete** (완료 준비) 페이지에서 새 가상 컴퓨터와 관련된 모든 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-205">On the **Ready to Complete** page, review all the settings associated with the new virtual machine.</span></span> <span data-ttu-id="40b83-206">**Edit the virtual machine settings before completion**(완료하기 전에 가상 컴퓨터 설정 편집)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-206">Check **Edit the virtual machine settings before completion**.</span></span> <span data-ttu-id="40b83-207">**계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-207">Click **Continue**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. <span data-ttu-id="40b83-208">**가상 컴퓨터 속성** 페이지의 **하드웨어** 탭에서 장치 하드웨어를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-208">On the **Virtual Machines Properties** page, in the **Hardware** tab, locate the device hardware.</span></span> <span data-ttu-id="40b83-209">**새 하드 디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-209">Select **New Hard Disk**.</span></span> <span data-ttu-id="40b83-210">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-210">Click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. <span data-ttu-id="40b83-211">**하드웨어 추가** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-211">You see a **Add Hardware** window.</span></span> <span data-ttu-id="40b83-212">**장치 유형** 페이지의 **추가할 장치 유형 선택**에서 **하드 디스크**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-212">On the **Device Type** page, under **Choose the type of device you wish to add**, select **Hard Disk**, and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. <span data-ttu-id="40b83-213">**디스크 선택** 페이지에서 **새 가상 디스크 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-213">On the **Select a Disk** page, choose **Create a new virtual disk**.</span></span> <span data-ttu-id="40b83-214">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-214">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. <span data-ttu-id="40b83-215">**디스크 만들기** 페이지에서 **디스크 크기**를 500GB(또는 그 이상)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-215">On the **Create a Disk** page, change the **Disk Size** to 500 GB (or more).</span></span> <span data-ttu-id="40b83-216">500GB가 최소 요구 사항이지만 언제나 더 큰 디스크를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-216">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="40b83-217">프로비전된 후에는 디스크를 확장하거나 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-217">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="40b83-218">프로비전할 디스크의 크기에 대한 자세한 정보는 [모범 사례 문서](storsimple-ova-best-practices.md)의 크기 조정 섹션을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="40b83-218">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="40b83-219">**디스크 프로비전**에서 **씬 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-219">Under **Disk Provisioning**, select **Thin Provision**.</span></span> <span data-ttu-id="40b83-220">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-220">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. <span data-ttu-id="40b83-221">**고급 옵션** 페이지에서 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-221">On the **Advanced Options** page, accept the default.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. <span data-ttu-id="40b83-222">**Ready to Complete** (완료 준비) 페이지에서 디스크 옵션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-222">On the **Ready to Complete** page, review the disk options.</span></span> <span data-ttu-id="40b83-223">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-223">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. <span data-ttu-id="40b83-224">가상 컴퓨터 속성 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-224">Return to the Virtual Machine Properties page.</span></span> <span data-ttu-id="40b83-225">새 하드 디스크가 가상 컴퓨터에 추가되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-225">A new hard disk is added to your virtual machine.</span></span> <span data-ttu-id="40b83-226">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-226">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. <span data-ttu-id="40b83-227">오른쪽 창에 가상 컴퓨터가 선택된 상태에서 **요약** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-227">With your virtual machine selected in the right pane, navigate to the **Summary** tab.</span></span> <span data-ttu-id="40b83-228">가상 컴퓨터에 대한 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-228">Review the settings for your virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

<span data-ttu-id="40b83-229">가상 컴퓨터가 프로비전되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-229">Your virtual machine is now provisioned.</span></span> <span data-ttu-id="40b83-230">다음 단계는 이 컴퓨터의 전원을 켜고 IP 주소를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-230">The next step is to power on this machine and get the IP address.</span></span>

## <a name="step-3-start-the-virtual-device-and-get-the-ip"></a><span data-ttu-id="40b83-231">3단계: 가상 장치를 시작하고 IP를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-231">Step 3: Start the virtual device and get the IP</span></span>
<span data-ttu-id="40b83-232">가상 장치를 시작하여 연결하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-232">Perform the following steps to start your virtual device and connect to it.</span></span>

#### <a name="to-start-the-virtual-device"></a><span data-ttu-id="40b83-233">가상 장치를 시작하려면</span><span class="sxs-lookup"><span data-stu-id="40b83-233">To start the virtual device</span></span>
1. <span data-ttu-id="40b83-234">가상 장치를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-234">Start the virtual device.</span></span> <span data-ttu-id="40b83-235">vSphere 구성 관리자의 왼쪽 창에서 장치를 선택하고 마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-235">In the vSphere Configuration Manager, in the left pane, select your device and right-click to bring up the context menu.</span></span> <span data-ttu-id="40b83-236">**전원**을 선택한 후 **전원 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-236">Select **Power** and then select **Power on**.</span></span> <span data-ttu-id="40b83-237">이렇게 하면 가상 컴퓨터의 전원이 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-237">This should power on your virtual machine.</span></span> <span data-ttu-id="40b83-238">vSphere 클라이언트의 아래쪽 **최근 태스크** 창에서 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-238">You can view the status in the bottom **Recent Tasks** pane of the vSphere client.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. <span data-ttu-id="40b83-239">설정 태스크를 완료하려면 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-239">The setup tasks will take a few minutes to complete.</span></span> <span data-ttu-id="40b83-240">장치가 실행되면 **콘솔** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-240">Once the device is running, navigate to the **Console** tab.</span></span> <span data-ttu-id="40b83-241">Ctrl+Alt+Delete 키를 눌러서 장치에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-241">Send Ctrl+Alt+Delete to log in to the device.</span></span> <span data-ttu-id="40b83-242">또는, 콘솔 창의 커서를 가리키고 Ctrl+Alt+Insert 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-242">Alternatively, you can point the cursor on the console window and press Ctrl+Alt+Insert.</span></span> <span data-ttu-id="40b83-243">기본 사용자는 *StorSimpleAdmin*이고 기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-243">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. <span data-ttu-id="40b83-244">보안상의 이유로 장치 관리자 암호는 처음 로그인하면 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-244">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="40b83-245">암호를 변경하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-245">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. <span data-ttu-id="40b83-246">8자 이상을 포함하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-246">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="40b83-247">암호는 4가지 요구 사항(대문자, 소문자, 숫자 및 특수 문자) 중 3가지를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-247">The password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="40b83-248">확인을 위해 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-248">Reenter the password to confirm it.</span></span> <span data-ttu-id="40b83-249">암호가 변경되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-249">You will be notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. <span data-ttu-id="40b83-250">암호 변경이 완료되면 가상 장치가 다시 부팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-250">After the password is successfully changed, the virtual device may reboot.</span></span> <span data-ttu-id="40b83-251">재부팅이 완료될 때가지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-251">Wait for the reboot to complete.</span></span> <span data-ttu-id="40b83-252">장치의 Windows PowerShell 콘솔이 진행률 표시줄과 함께 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-252">The Windows PowerShell console of the device may be displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. <span data-ttu-id="40b83-253">6-8단계는 DHCP 환경이 아닌 곳에서 부팅하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-253">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="40b83-254">DHCP 환경인 경우에는 이 단계를 건너뛰고 9단계로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="40b83-254">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="40b83-255">DHCP 환경이 아닌 곳에서 장치를 부팅하는 경우에는 다음 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-255">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   <span data-ttu-id="40b83-256">다음으로 네트워크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-256">Next, configure the network.</span></span>
7. <span data-ttu-id="40b83-257">`Get-HcsIpAddress` 명령을 사용하여 가상 장치에 사용하도록 설정된 네트워크 인터페이스 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-257">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="40b83-258">장치에 사용하도록 설정된 네트워크 인터페이스가 하나인 경우에는 `Ethernet`이라는 기본 이름이 인터페이스에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-258">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. <span data-ttu-id="40b83-259">`Set-HcsIpAddress` cmdlet을 사용하여 네트워크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-259">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="40b83-260">아래에 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-260">An example is shown below:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. <span data-ttu-id="40b83-261">초기 설정이 완료된 후 장치가 부팅되면 장치 배너 텍스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-261">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="40b83-262">장치 관리를 위해 배너 텍스트에 표시되는 IP 주소와 URL을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-262">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="40b83-263">IP 주소를 사용하여 가상 장치의 웹 UI를 연결하고 로컬 설정 및 등록을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-263">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. <span data-ttu-id="40b83-264">(선택 사항) 이 단계는 정부 클라우드에서 장치를 배포하는 경우에만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-264">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="40b83-265">이제 장치에서 미국 FIPS(Federal Information Processing Standard) 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-265">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="40b83-266">FIPS 140 표준은 중요한 데이터의 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인된 암호화 알고리즘을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-266">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="40b83-267">FIPS 모드를 사용하도록 설정하려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-267">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="40b83-268">암호화 유효성 검사에 적용되도록 FIPS 모드를 사용하도록 설정한 후 장치를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-268">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="40b83-269">장치에서 FIPS 모드를 사용 또는 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-269">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="40b83-270">장치에서 FIPS 모드와 비 FIPS 모드가 교대로 반복되는 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-270">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="40b83-271">장치가 최소 구성 요구 사항을 충족하지 못하면 배너 텍스트에 오류(아래 참고)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-271">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span></span> <span data-ttu-id="40b83-272">최소 요구 사항을 충족하기에 충분한 리소스를 확보하도록 장치 구성을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-272">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="40b83-273">그런 다음 다시 시작하고 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-273">You can then restart and connect to the device.</span></span> <span data-ttu-id="40b83-274">[1단계: 호스트 시스템이 최소 가상 장치 요구 사항을 충족하도록 합니다.](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements)에서 최소 구성 요구 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40b83-274">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

<span data-ttu-id="40b83-275">로컬 웹 UI를 사용하여 초기 구성을 하는 동안 다른 오류가 발생하면 다음 워크플로를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40b83-275">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="40b83-276">진단 테스트를 실행하여 [웹 UI 설정 문제를 해결](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)합니다.</span><span class="sxs-lookup"><span data-stu-id="40b83-276">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="40b83-277">[로그 패키지를 생성하고 로그 파일을 살펴봅니다](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="40b83-277">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40b83-278">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40b83-278">Next steps</span></span>
* [<span data-ttu-id="40b83-279">StorSimple 가상 배열을 파일 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="40b83-279">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="40b83-280">StorSimple 가상 배열을 iSCSI 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="40b83-280">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
