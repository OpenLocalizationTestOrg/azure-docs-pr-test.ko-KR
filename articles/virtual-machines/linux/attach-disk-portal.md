---
title: "Linux VM에 데이터 디스크 연결 | Microsoft Docs"
description: "리소스 관리자 배포 모델을 사용하여 Azure 포털의 Linux VM에 신규 및 기존 데이터 디스크를 연결하는 방법."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="0a93c-103">Azure 포털에서 Linux VM에 데이터 디스크를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="0a93c-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="0a93c-104">이 문서에서는 Azure 포털을 통해 신규 및 기존 디스크를 Linux 가상 컴퓨터에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="0a93c-105">또한 [Azure Portal에서 Windows VM에 데이터 디스크를 연결](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0a93c-106">Azure Managed Disks 또는 관리되지 않는 디스크를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="0a93c-107">관리되는 디스크는 Azure 플랫폼을 통해 처리되며 디스크를 저장할 위치나 준비가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="0a93c-108">관리되지 않는 디스크는 저장소 계정이 필요하며 [적용되는 할당량 및 제한](../../azure-subscription-service-limits.md#storage-limits)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="0a93c-109">Azure Managed Disks에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a93c-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="0a93c-110">VM에 디스크를 연결하기 전에 다음 팁을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="0a93c-111">가상 컴퓨터의 크기로 연결할 수 있는 디스크 개수가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="0a93c-112">자세한 내용은 [가상 컴퓨터의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a93c-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="0a93c-113">프리미엄 저장소를 사용하려면 DS 시리즈 또는 GS 시리즈 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="0a93c-114">이러한 가상 컴퓨터와 함께 프리미엄 및 표준 디스크를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="0a93c-115">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="0a93c-116">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a93c-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="0a93c-117">가상 컴퓨터에 연결된 디스크는 실제로 Azure에 저장된 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="0a93c-118">자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a93c-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="0a93c-119">가상 컴퓨터 찾기</span><span class="sxs-lookup"><span data-stu-id="0a93c-119">Find the virtual machine</span></span>
1. <span data-ttu-id="0a93c-120">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0a93c-121">허브 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="0a93c-122">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="0a93c-123">가상 컴퓨터 블레이드의 **Essentials**에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![디스크 설정 열기](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="0a93c-125">[관리되는 디스크](#use-azure-managed-disks) 또는 [관리되지 않는 디스크](#use-unmanaged-disks) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="0a93c-126">Azure Managed Disks 사용</span><span class="sxs-lookup"><span data-stu-id="0a93c-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="0a93c-127">새 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="0a93c-127">Attach a new disk</span></span>

1. <span data-ttu-id="0a93c-128">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="0a93c-129">**이름**에 대한 드롭다운 메뉴를 클릭하고 **디스크 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Azure Managed Disks 만들기](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="0a93c-131">관리되는 디스크에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="0a93c-132">기본 설정을 검토하고 필요에 따라 업데이트한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![디스크 설정 검토](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="0a93c-134">**저장**을 클릭하여 관리되는 디스크를 만들고 VM 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![새 Azure Managed Disk 저장](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="0a93c-136">Azure가 디스크를 만들고 가상 컴퓨터에 연결하면 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 새 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="0a93c-137">관리되는 디스크는 최상위 수준 리소스이므로 디스크는 리소스 그룹의 루트에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![리소스 그룹의 Azure Managed Disk](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="0a93c-139">기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="0a93c-139">Attach an existing disk</span></span>
1. <span data-ttu-id="0a93c-140">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="0a93c-141">**이름**에 대한 드롭다운 메뉴를 클릭하여 Azure 구독에 액세스할 수 있는 기존 관리되는 디스크의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="0a93c-142">연결할 관리되는 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-142">Select the managed disk to attach:</span></span>

   ![기존 Azure Managed Disk 연결](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="0a93c-144">**저장**을 클릭하여 기존 관리되는 디스크를 연결하고 VM 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Azure Managed Disk 업데이트 저장](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="0a93c-146">Azure가 디스크를 가상 컴퓨터에 연결한 후 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 해당 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="0a93c-147">관리되지 않는 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="0a93c-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="0a93c-148">새 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="0a93c-148">Attach a new disk</span></span>

1. <span data-ttu-id="0a93c-149">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="0a93c-150">기본 설정을 검토하고 필요에 따라 업데이트한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![디스크 설정 검토](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="0a93c-152">Azure가 디스크를 만들고 가상 컴퓨터에 연결하면 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 새 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="0a93c-153">기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="0a93c-153">Attach an existing disk</span></span>
1. <span data-ttu-id="0a93c-154">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="0a93c-155">**기존 디스크 연결**에서 **VHD 파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![기존 디스크 연결](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="0a93c-157">**저장소 계정**에서 계정 및 .vhd 파일을 보관하는 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![VHD 위치 찾기](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="0a93c-159">.vhd 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="0a93c-160">**기존 디스크 연결**에서 방금 선택한 파일이 **VHD 파일** 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="0a93c-161">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-161">Click **OK**.</span></span>
6. <span data-ttu-id="0a93c-162">Azure가 디스크를 가상 컴퓨터에 연결한 후 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 해당 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0a93c-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a93c-163">Next steps</span></span>
<span data-ttu-id="0a93c-164">디스크를 추가한 후 해당 디스크를 사용할 수 있도록 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a93c-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="0a93c-165">자세한 내용은 [방법: Linux에서 새 데이터 디스크 초기화](add-disk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a93c-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
