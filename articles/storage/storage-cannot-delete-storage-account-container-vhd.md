---
title: "클래식 배포에서 Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 문제 해결 | Microsoft Docs"
description: "클래식 배포에서 Azure 저장소 계정, 컨테이너 또는 VHD를 삭제하는 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="40c1f-103">클래식 배포에서 Azure 저장소 계정, 컨테이너 또는 VHD를 삭제하는 문제 해결</span><span class="sxs-lookup"><span data-stu-id="40c1f-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="40c1f-104">[Azure Portal](https://portal.azure.com/)이나 [Azure 클래식 포털](https://manage.windowsazure.com/)에서 Azure 저장소 계정, 컨테이너 또는 VHD를 삭제하려고 하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="40c1f-105">다음과 같은 상황으로 인해 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="40c1f-106">VM을 삭제할 때 디스크와 VHD는 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="40c1f-107">따라서 저장소 계정 삭제 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="40c1f-108">다른 VM을 마운트할 수 있도록 디스크는 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="40c1f-109">즉, 디스크에 대한 임대 또는 디스크와 연결된 blob가 계속 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="40c1f-110">Blob, 컨테이너 또는 저장소 계정을 사용하는 VM 이미지는 여전히 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="40c1f-111">Azure 문제와 관련된 정보가 이 문서에 없을 경우 [MSDN 및 Stack Overflow](https://azure.microsoft.com/support/forums/)에서 Azure 포럼을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="40c1f-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="40c1f-112">이러한 포럼이나 Twitter의 @AzureSupport에 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="40c1f-113">또한 **Azure 지원** 사이트에서 [지원 받기](https://azure.microsoft.com/support/options/) 를 선택하여 Azure 지원 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="40c1f-114">증상</span><span class="sxs-lookup"><span data-stu-id="40c1f-114">Symptoms</span></span>
<span data-ttu-id="40c1f-115">다음 섹션에서는 Azure 저장소 계정, 컨테이너 또는 VHD를 삭제하려고 할 때 발생할 수 있는 일반적인 오류에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="40c1f-116">시나리오 1: 저장소 계정을 삭제할 수 없음</span><span class="sxs-lookup"><span data-stu-id="40c1f-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="40c1f-117">[Azure Portal](https://portal.azure.com/)에서 클래식 저장소 계정으로 이동하여 **삭제**를 선택하면 저장소 계정을 삭제할 수 없는 개체의 목록이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![저장소 계정 삭제 시 오류 이미지](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="40c1f-119">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 저장소 계정으로 이동하여 **삭제**를 선택하면 다음 오류 중 하나가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="40c1f-120">*저장소 계정 StorageAccountName에는 VM 이미지가 들어 있습니다. 이 저장소 계정을 삭제하려면 이러한 VM 이미지를 제거해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="40c1f-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="40c1f-121">*저장소 계정 <vm-storage-account-name>을(를) 삭제하지 못했습니다. <vm-storage-account-name> 저장소 계정을 삭제할 수 없습니다. '저장소 계정 <vm-storage-account-name>에 일부 활성 이미지 및/또는 디스크가 있습니다. 이 저장소 계정을 삭제하려면 이러한 이미지 및/또는 디스크를 제거해야 합니다.'.*</span><span class="sxs-lookup"><span data-stu-id="40c1f-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="40c1f-122">*저장소 계정 <vm-storage-account-name>에 xxxxxxxxx- xxxxxxxxx-O-209490240936090599과(와) 같은 일부 활성 이미지 및/또는 디스크가 있습니다. 이 저장소 계정을 삭제하려면 이러한 이미지 및/또는 디스크를 제거해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="40c1f-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="40c1f-123">*저장소 계정 <vm-storage-account-name>에 활성 이미지 및/또는 디스크 아티팩트를 포함하는 1 컨테이너가 있습니다. 이 저장소 계정을 삭제하려면 이미지 리포지토리에서 이러한 아티팩트를 제거해야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="40c1f-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="40c1f-124">*제출 실패 저장소 계정 <vm-storage-account-name>에 활성 이미지 및/또는 디스크 아티팩트를 포함하는 1 컨테이너가 있습니다. 이 저장소 계정을 삭제하려면 이미지 리포지토리에서 이러한 아티팩트를 제거해야 합니다. 저장소 계정을 삭제하려고 하는데 해당 저장소 계정과 연결된 활성 디스크가 남아 있는 경우에는 남아 있는 활성 디스크를 삭제해야 한다는 내용의 메시지가 표시됩니다*.</span><span class="sxs-lookup"><span data-stu-id="40c1f-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="40c1f-125">시나리오 2: 컨테이너를 삭제할 수 없음</span><span class="sxs-lookup"><span data-stu-id="40c1f-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="40c1f-126">저장소 컨테이너를 삭제하려고 할 때 다음 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="40c1f-127">*저장소 컨테이너를 삭제하지 못했습니다<container name>. 오류: '현재 컨테이너에 임대가 있는데 요청에서 임대 ID가 지정되지 않았습니다*.</span><span class="sxs-lookup"><span data-stu-id="40c1f-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="40c1f-128">또는</span><span class="sxs-lookup"><span data-stu-id="40c1f-128">Or</span></span>

<span data-ttu-id="40c1f-129">*VirtualMachineDiskName1, VirtualMachineDiskName2, ... 등의 가상 컴퓨터 디스크에서 컨테이너의 Blob을 사용 하므로 이 컨테이너를 삭제할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="40c1f-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="40c1f-130">시나리오 3: VHD를 삭제할 수 없음</span><span class="sxs-lookup"><span data-stu-id="40c1f-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="40c1f-131">VM을 삭제한후 연결된 VHD의 blob를 삭제하려고 하면 다음 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="40c1f-132">*'path/XXXXXX-XXXXXX-os-1447379084699.vhd' Blob을 삭제하지 못했습니다. 오류: '현재 Blob에 임대가 있는데 요청에서 임대 ID가 지정되지 않았습니다.*</span><span class="sxs-lookup"><span data-stu-id="40c1f-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="40c1f-133">또는</span><span class="sxs-lookup"><span data-stu-id="40c1f-133">Or</span></span>

<span data-ttu-id="40c1f-134">*'BlobName.vhd' Blob에서 'VirtualMachineDiskName' 가상 컴퓨터 디스크로 사용 중이므로 Blob을 삭제할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="40c1f-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="40c1f-135">해결 방법</span><span class="sxs-lookup"><span data-stu-id="40c1f-135">Solution</span></span>
<span data-ttu-id="40c1f-136">가장 일반적인 문제는 다음과 같은 방법으로 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="40c1f-137">1단계: 저장소 계정, 컨테이너 또는 VHD의 삭제를 방지하는 모든 디스크 삭제</span><span class="sxs-lookup"><span data-stu-id="40c1f-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="40c1f-138">[Azure 클래식 포털](https://manage.windowsazure.com/)로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="40c1f-139">**가상 컴퓨터** > **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Azure 클래식 포털에 표시된 가상 컴퓨터의 디스크 이미지입니다.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="40c1f-141">삭제하려는 저장소 계정, 컨테이너 또는 VHD와 연결된 디스크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="40c1f-142">디스크 위치를 확인하면 연결된 저장소 계정, 컨테이너 또는 VHD를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Azure 클래식 포털에서 디스크의 위치 정보를 보여주는 이미지](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="40c1f-144">다음 방법 중 하나를 사용하여 디스크를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="40c1f-145">VM이 디스크의 **연결된 항목** 필드에 나열되지 않은 경우 디스크를 직접 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="40c1f-146">디스크가 데이터 디스크인 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="40c1f-147">디스크가 연결된 VM의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="40c1f-148">**Virtual Machines** > **인스턴스**로 이동한 다음 해당 VM을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="40c1f-149">디스크를 사용하고 있는 VM이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="40c1f-150">포털 아래쪽에서 **디스크 분리**를 선택하여 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="40c1f-151">**Virtual Machines** > **디스크**로 이동하고 **연결된 항목** 필드가 빈 상태로 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="40c1f-152">이는 디스크가 VM에서 성공적으로 분리되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="40c1f-153">**Virtual Machines** > **디스크**의 아래쪽에 있는 **삭제**를 선택하여 디스크를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="40c1f-154">디스크가 OS 디스크(**OS 2 포함** 필드에 Windows와 같은 값이 있음)이고 VM에 연결되어 있는 경우 다음 단계에 따라 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="40c1f-155">OS 디스크는 분리할 수 없으므로 VM을 삭제하여 연결 상태를 끊어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="40c1f-156">[데이터 디스크]에 연결된 Virtual Machine의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="40c1f-157">**Virtual Machines** > **인스턴스**로 이동한 다음 디스크가 연결된 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="40c1f-158">실제로 가상 컴퓨터를 사용 중인 항목이 없고 가상 컴퓨터가 더 이상 필요하지 않음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="40c1f-159">디스크가 연결된 VM을 선택하고 **삭제** > **연결된 디스크 삭제**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="40c1f-160">**Virtual Machines** > **디스크**로 이동하고 디스크가 없어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="40c1f-161">이 상태가 될 때까지 몇 분이 걸릴 수 있으며 페이지를 새로 고쳐야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="40c1f-162">디스크가 없어지지 않으면 **연결된 항목** 필드가 빈 상태로 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="40c1f-163">이는 디스크가 VM에서 완전히 분리되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="40c1f-164">그런 다음 디스크를 선택하고 페이지의 아래쪽에 있는 **삭제**를 선택하여 디스크를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="40c1f-165">VM에 연결되어 있는 디스크는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="40c1f-166">디스크는 삭제된 VM에서 비동기적으로 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="40c1f-167">따라서 VM을 삭제한 후 이 필드가 지워질 때까지 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="40c1f-168">2단계: 저장소 계정 또는 컨테이너의 삭제를 방지하는 모든 VM 이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="40c1f-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="40c1f-169">[Azure 클래식 포털](https://manage.windowsazure.com/)로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="40c1f-170">**가상 컴퓨터** > **이미지**를 선택한 다음 저장소 계정, 컨테이너 또는 VHD에 연결된 이미지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="40c1f-171">그런 다음 저장소 계정, 컨테이너 또는 VHD를 다시 삭제해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="40c1f-172">계정을 삭제하기 전에 저장할 내용을 백업했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="40c1f-173">VHD, BLOB, 테이블, 큐 또는 파일을 삭제하면 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="40c1f-174">리소스가 사용되고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="40c1f-175">중지됨(할당 취소됨) 상태 관련 정보</span><span class="sxs-lookup"><span data-stu-id="40c1f-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="40c1f-176">클래식 배포 모델에서 만든 후 보존된 VM은 [Azure Portal](https://portal.azure.com/) 또는 [Azure 클래식 포털](https://manage.windowsazure.com/)에서 **중지됨(할당 취소됨)** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="40c1f-177">**Azure 클래식 포털**:</span><span class="sxs-lookup"><span data-stu-id="40c1f-177">**Azure classic portal**:</span></span>

![Azure 포털에 표시된 VM의 중지됨(할당 취소됨) 상태입니다.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="40c1f-179">**Azure 포털**:</span><span class="sxs-lookup"><span data-stu-id="40c1f-179">**Azure portal**:</span></span>

![Azure 클래식 포털에 표시된 VM의 중지됨(할당 취소됨) 상태입니다.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="40c1f-181">"중지됨(할당 취소됨)" 상태에서는 CPU, 메모리, 네트워크 등의 컴퓨터 리소스가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="40c1f-182">그러나 사용자가 필요 시 빠르게 VM을 다시 만들 수 있도록 디스크는 계속 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="40c1f-183">이러한 디스크는 Azure 저장소에서 지원하는 VHD를 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="40c1f-184">저장소 계정에 이러한 VHD가 포함되어 있으며 디스크에는 이러한 VHD의 임대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c1f-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40c1f-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40c1f-185">Next steps</span></span>
* [<span data-ttu-id="40c1f-186">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="40c1f-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
