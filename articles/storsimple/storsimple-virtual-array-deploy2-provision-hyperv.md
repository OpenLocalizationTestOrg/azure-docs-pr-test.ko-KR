---
title: "Hyper-V에서 StorSimple Virtual Array 프로비전 | Microsoft Docs"
description: "StorSimple 가상 배열 배포에 대한 두 번째 자습서에는 Hyper-V에서 가상 배열을 프로비전하는 내용이 포함됩니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bad431c8958f7d381bb9c0410caa3a57c6e75c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="6f071-103">StorSimple 가상 배열 배포 - Hyper-V에서 프로비전</span><span class="sxs-lookup"><span data-stu-id="6f071-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="6f071-104">개요</span><span class="sxs-lookup"><span data-stu-id="6f071-104">Overview</span></span>
<span data-ttu-id="6f071-105">이 자습서에서는 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2에서 Hyper-V를 실행하는 호스트 시스템의 StorSimple 가상 배열을 프로비전하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="6f071-106">이 문서는 Azure Portal 및 Microsoft Azure Government 클라우드에서 StorSimple 가상 배열의 배포에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="6f071-107">가상 배열을 프로비전하고 구성하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-107">You need administrator privileges to provision and configure a virtual array.</span></span> <span data-ttu-id="6f071-108">프로비전 및 초기 설정을 완료하는 데 10분 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="6f071-109">프로비전 필수 조건</span><span class="sxs-lookup"><span data-stu-id="6f071-109">Provisioning prerequisites</span></span>
<span data-ttu-id="6f071-110">여기서는 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2에서 Hyper-V를 실행하는 호스트 시스템에서 가상 배열을 프로비전하기 위한 필수 구성 요소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="6f071-111">StorSimple 장치 관리자 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="6f071-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="6f071-112">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="6f071-113">[StorSimple 가상 배열용 포털 준비](storsimple-virtual-array-deploy1-portal-prep.md)의 모든 단계를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="6f071-114">Azure Portal에서 Hyper-V용 가상 배열 이미지를 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="6f071-115">자세한 내용은 [StorSimple 가상 배열을 위한 포털 준비 가이드](storsimple-virtual-array-deploy1-portal-prep.md)의 **3단계: 가상 배열 이미지 다운로드**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6f071-116">StorSimple 가상 배열에서 실행되는 소프트웨어는 StorSimple 장치 관리자 서비스와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="6f071-117">StorSimple 가상 배열의 경우</span><span class="sxs-lookup"><span data-stu-id="6f071-117">For the StorSimple Virtual Array</span></span>
<span data-ttu-id="6f071-118">가상 배열을 배포하기 전에 다음 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="6f071-119">장치 프로비전에 사용될 수 있는 Windows Server 2008 R2 이상에서 Hyper-V를 실행하는 호스트 시스템에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="6f071-120">가상 배열을 프로비전하려면 호스트 시스템에서 다음 리소스를 전용으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-120">The host system is able to dedicate the following resources to provision your virtual array:</span></span>

  * <span data-ttu-id="6f071-121">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="6f071-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="6f071-122">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="6f071-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="6f071-123">가상 배열을 파일 서버로서 구성하려는 경우 8GB는 2백만 개 미만의 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="6f071-124">2 - 4백만 개의 파일을 지원하려면 16GB RAM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-124">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="6f071-125">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="6f071-125">One network interface.</span></span>
  * <span data-ttu-id="6f071-126">데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="6f071-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="6f071-127">데이터 센터에서 네트워크의 경우</span><span class="sxs-lookup"><span data-stu-id="6f071-127">For the network in the datacenter</span></span>
<span data-ttu-id="6f071-128">시작하기 전에 StorSimple 가상 배열을 배포하고 데이터 센터 네트워크를 적절히 구성하기 위한 네트워킹 요구 사항을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span></span> <span data-ttu-id="6f071-129">자세한 내용은 [StorSimple 가상 배열 네트워킹 요구 사항](storsimple-ova-system-requirements.md#networking-requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="6f071-130">단계별 프로비전</span><span class="sxs-lookup"><span data-stu-id="6f071-130">Step-by-step provisioning</span></span>
<span data-ttu-id="6f071-131">가상 배열을 프로비전하고 연결하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-131">To provision and connect to a virtual array, you need to perform the following steps:</span></span>

1. <span data-ttu-id="6f071-132">호스트 시스템에 최소 가상 배열 요구 사항을 충족하기에 충분한 리소스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span></span>
2. <span data-ttu-id="6f071-133">하이퍼바이저에서 가상 배열을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="6f071-134">가상 배열을 시작하고 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-134">Start the virtual array and get the IP address.</span></span>

<span data-ttu-id="6f071-135">각 단계는 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-135">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="6f071-136">1단계: 호스트 시스템이 최소 가상 배열 요구 사항을 충족하는지 확인</span><span class="sxs-lookup"><span data-stu-id="6f071-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="6f071-137">가상 배열을 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-137">To create a virtual array, you need:</span></span>

* <span data-ttu-id="6f071-138">Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 SP1에 설치되어 있는 Hyper-V 역할</span><span class="sxs-lookup"><span data-stu-id="6f071-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="6f071-139">호스트에 연결된 Microsoft Windows 클라이언트의 Microsoft Hyper-V 관리자</span><span class="sxs-lookup"><span data-stu-id="6f071-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="6f071-140">가상 배열을 만드는 기본 하드웨어(호스트 시스템)에서 가상 배열에 대해 다음 리소스를 전용으로 사용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span></span>

* <span data-ttu-id="6f071-141">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="6f071-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="6f071-142">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="6f071-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="6f071-143">가상 배열을 파일 서버로서 구성하려는 경우 8GB는 2백만 개 미만의 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="6f071-144">2 - 4백만 개의 파일을 지원하려면 16GB RAM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-144">You need 16 GB RAM to support 2 - 4 million files.</span></span>
* <span data-ttu-id="6f071-145">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="6f071-145">One network interface.</span></span>
* <span data-ttu-id="6f071-146">시스템 데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="6f071-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="6f071-147">2단계: 하이퍼바이저에서 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="6f071-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="6f071-148">하이퍼바이저에서 장치를 프로비전하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-148">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-array"></a><span data-ttu-id="6f071-149">가상 배열을 프로비전하려면</span><span class="sxs-lookup"><span data-stu-id="6f071-149">To provision a virtual array</span></span>
1. <span data-ttu-id="6f071-150">Windows Server 호스트에서 로컬 드라이브에 가상 배열 이미지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-150">On your Windows Server host, copy the virtual array image to a local drive.</span></span> <span data-ttu-id="6f071-151">이 이미지(VHD 또는 VHDX)를 Azure Portal을 통해 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span></span> <span data-ttu-id="6f071-152">나중에 절차에서 이 이미지를 사용하므로 이미지를 복사한 위치를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>
2. <span data-ttu-id="6f071-153">**서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-153">Open **Server Manager**.</span></span> <span data-ttu-id="6f071-154">오른쪽 위 모서리에서 **도구**를 클릭하고 **Hyper-V 관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="6f071-155">Windows Server 2008 R2를 실행하는 경우에는 Hyper-V 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="6f071-156">서버 관리자에서 **역할 > Hyper-V > Hyper-V 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="6f071-157">**Hyper-V 관리자**의 범위 창에서 시스템 노드를 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 연 다음 **새로 만들기** > **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="6f071-158">새 가상 컴퓨터 마법사의 **시작하기 전에** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="6f071-159">**이름 및 위치 지정** 페이지에서 가상 배열의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="6f071-160">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="6f071-161">**세대 지정** 페이지에서 장치 이미지 유형을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span></span> <span data-ttu-id="6f071-162">Windows Server 2008 R2를 사용하는 경우에는 이 페이지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="6f071-163">Windows Server 2012 이상에 대한 .vhdx 이미지를 다운로드한 경우 **2세대** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="6f071-164">Windows Server 2008 R2 이상에 대한 .vhd 이미지를 다운로드한 경우 **1세대** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="6f071-165">**메모리 할당** 페이지에서 **시작 메모리**를 **8192MB** 이상으로 지정하고, 동적 메모리는 사용하도록 설정하지 않은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="6f071-166">**네트워킹 구성** 페이지에서 인터넷에 연결된 가상 스위치를 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="6f071-167">**가상 하드 디스크 연결** 페이지에서 **기존 가상 하드 디스크 사용**을 선택하고 가상 배열 이미지(.vhdx 또는 .vhd)의 위치를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="6f071-168">**요약**을 검토하고 **마침**을 클릭하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="6f071-169">최소 요구 사항을 충족하려면 코어 4개가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-169">To meet the minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="6f071-170">4개의 가상 프로세서를 추가하려면 **Hyper-V 관리자** 창에서 호스트 시스템을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span></span> <span data-ttu-id="6f071-171">**가상 컴퓨터** 목록의 오른쪽 창에서 방금 만든 가상 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="6f071-172">컴퓨터 이름을 선택하고 마우스 오른쪽 단추로 클릭한 후 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-172">Select and right-click the machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="6f071-173">**설정** 페이지의 왼쪽 창에서 **프로세서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-173">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="6f071-174">오른쪽 창에서 **가상 프로세서 수**를 4(또는 그 이상)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="6f071-175">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="6f071-176">최소 요구 사항을 충족하려면 가상 데이터 디스크를 500GB 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="6f071-177">**설정** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="6f071-177">In the **Settings** page:</span></span>

    1. <span data-ttu-id="6f071-178">왼쪽 창의 **SCSI 컨트롤러**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-178">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="6f071-179">오른쪽 창의 **하드 드라이브**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-179">In the right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="6f071-180">**하드 드라이브** 페이지에서 **가상 하드 디스크** 옵션을 선택하고 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="6f071-181">**새 가상 하드 디스크 마법사**가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-181">The **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="6f071-182">새 가상 하드 디스크 마법사의 **시작하기 전에** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="6f071-183">**디스크 형식 선택** 페이지에서 **VHDX** 형식의 기본 옵션을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="6f071-184">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-184">Click **Next**.</span></span> <span data-ttu-id="6f071-185">Windows Server 2008 R2를 실행하는 경우에는 이 화면이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="6f071-186">**디스크 유형 선택** 페이지에서 가상 하드 디스크 유형을 **동적 확장**(권장)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="6f071-187">**고정 크기** 디스크는 작동은 되지만 오래 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-187">**Fixed size** disk would work but you may need to wait a long time.</span></span> <span data-ttu-id="6f071-188">**차이점 보관용** 옵션은 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-188">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="6f071-189">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-189">Click **Next**.</span></span> <span data-ttu-id="6f071-190">Windows Server 2012 R2 및 Windows Server 2012에서는 **동적 확장**이 기본 옵션이지만 Windows Server 2008 R2에서는 **고정 크기**가 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="6f071-191">**이름 및 위치 지정** 페이지에서 데이터 디스크의 **이름** 및 **위치**(해당 위치로 이동 가능)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="6f071-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="6f071-193">**디스크 구성** 페이지에서 **비어 있는 새 가상 하드 디스크 만들기** 옵션을 선택하고 크기를 **500GB**(또는 그 이상)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="6f071-194">500GB가 최소 요구 사항이지만 언제나 더 큰 디스크를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="6f071-195">프로비전된 후에는 디스크를 확장하거나 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-195">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="6f071-196">프로비전할 디스크의 크기에 대한 자세한 정보는 [모범 사례 문서](storsimple-ova-best-practices.md)의 크기 조정 섹션을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="6f071-197">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="6f071-198">**요약** 페이지에서 가상 데이터 디스크의 세부 정보를 검토한 후 만족스러우면 **마침**을 클릭하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="6f071-199">마법사가 닫히고 가상 하드 디스크가 컴퓨터에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-199">The wizard closes and a virtual hard disk is added to your machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="6f071-200">**설정** 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-200">Return to the **Settings** page.</span></span> <span data-ttu-id="6f071-201">**확인**을 클릭하여 **설정** 페이지를 닫고 Hyper-V 관리자 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-array-and-get-the-ip"></a><span data-ttu-id="6f071-202">3단계: 가상 배열 시작 및 IP 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f071-202">Step 3: Start the virtual array and get the IP</span></span>
<span data-ttu-id="6f071-203">가상 배열을 시작하여 연결하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-203">Perform the following steps to start your virtual array and connect to it.</span></span>

#### <a name="to-start-the-virtual-array"></a><span data-ttu-id="6f071-204">가상 배열을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="6f071-204">To start the virtual array</span></span>
1. <span data-ttu-id="6f071-205">가상 배열을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-205">Start the virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="6f071-206">장치가 실행된 후에 장치를 선택하고 마우스 오른쪽 단추를 클릭하여 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-206">After the device is running, select the device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="6f071-207">장치가 준비되기까지 5-10분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-207">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="6f071-208">콘솔에 진행률을 나타내는 상태 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-208">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="6f071-209">장치가 준비되면 **작업**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-209">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="6f071-210">`Ctrl + Alt + Delete` 키를 눌러서 가상 배열에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span></span> <span data-ttu-id="6f071-211">기본 사용자는 *StorSimpleAdmin*이고 기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="6f071-212">보안상의 이유로 장치 관리자 암호는 처음 로그인하면 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-212">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="6f071-213">암호를 변경하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-213">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="6f071-214">8자 이상을 포함하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="6f071-215">암호는 4가지 요구 사항(소문자, 대문자, 숫자 및 특수 문자) 중 3가지 이상을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="6f071-216">확인을 위해 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-216">Reenter the password to confirm it.</span></span> <span data-ttu-id="6f071-217">암호가 변경되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-217">You are notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="6f071-218">암호 변경이 완료되면 가상 배열이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-218">After the password is successfully changed, the virtual array may restart.</span></span> <span data-ttu-id="6f071-219">장치가 시작할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-219">Wait for the device to start.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="6f071-220">장치의 Windows PowerShell 콘솔이 진행률 표시줄과 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="6f071-221">6-8단계는 DHCP 환경이 아닌 곳에서 부팅하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="6f071-222">DHCP 환경인 경우에는 이 단계를 건너뛰고 9단계로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="6f071-223">DHCP 환경이 아닌 곳에서 장치를 부팅하는 경우에는 다음 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="6f071-224">다음으로 네트워크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-224">Next, configure the network.</span></span>
7. <span data-ttu-id="6f071-225">`Get-HcsIpAddress` 명령을 사용하여 가상 배열에 사용하도록 설정된 네트워크 인터페이스 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="6f071-226">장치에 사용하도록 설정된 네트워크 인터페이스가 하나인 경우에는 `Ethernet`이라는 기본 이름이 인터페이스에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="6f071-227">`Set-HcsIpAddress` cmdlet을 사용하여 네트워크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="6f071-228">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-228">See the following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="6f071-229">초기 설정이 완료된 후 장치가 부팅되면 장치 배너 텍스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="6f071-230">장치 관리를 위해 배너 텍스트에 표시되는 IP 주소와 URL을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="6f071-231">IP 주소를 사용하여 가상 배열의 웹 UI를 연결하고 로컬 설정 및 등록을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="6f071-232">(선택 사항) 이 단계는 정부 클라우드에서 장치를 배포하는 경우에만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="6f071-233">이제 장치에서 미국 FIPS(Federal Information Processing Standard) 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="6f071-234">FIPS 140 표준은 중요한 데이터의 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인된 암호화 알고리즘을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="6f071-235">FIPS 모드를 사용하도록 설정하려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-235">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="6f071-236">암호화 유효성 검사에 적용되도록 FIPS 모드를 사용하도록 설정한 후 장치를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="6f071-237">장치에서 FIPS 모드를 사용 또는 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="6f071-238">장치에서 FIPS 모드와 비 FIPS 모드가 교대로 반복되는 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="6f071-239">장치가 최소 구성 요구 사항을 충족하지 못하면 아래 표시된 배너 텍스트에 다음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span></span> <span data-ttu-id="6f071-240">컴퓨터가 최소 요구 사항을 충족하기에 충분한 리소스를 확보하도록 장치 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="6f071-241">그런 다음 다시 시작하고 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-241">You can then restart and connect to the device.</span></span> <span data-ttu-id="6f071-242">[1단계: 호스트 시스템이 최소 가상 배열 요구 사항을 충족하는지 확인](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements)에서 최소 구성 요구 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="6f071-243">로컬 웹 UI를 사용하여 초기 구성을 하는 동안 다른 오류가 발생하면 다음 워크플로를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f071-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="6f071-244">진단 테스트를 실행하여 [웹 UI 설정 문제를 해결](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f071-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="6f071-245">[로그 패키지를 생성하고 로그 파일을 살펴봅니다](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="6f071-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f071-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f071-246">Next steps</span></span>
* [<span data-ttu-id="6f071-247">StorSimple 가상 배열을 파일 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="6f071-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="6f071-248">StorSimple 가상 배열을 iSCSI 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="6f071-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
