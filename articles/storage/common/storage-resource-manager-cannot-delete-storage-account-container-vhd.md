---
title: "Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결 | Microsoft Docs"
description: "Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="a4617-103">Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a4617-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="a4617-104">[Azure 포털](https://portal.azure.com)에서 Azure 저장소 계정, 컨테이너 또는 VHD(가상 하드 디스크)를 삭제하려고 하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a4617-105">이 문서에서는 Azure Resource Manager 배포의 문제 해결에 유용한 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="a4617-106">이 문서에 Azure 문제와 관련된 정보가 없는 경우 [MSDN 및 Stack Overflow](https://azure.microsoft.com/support/forums/)에서 Azure 포럼을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="a4617-107">이러한 포럼이나 Twitter의 @AzureSupport에 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="a4617-108">또한 **Azure 지원** 사이트에서 [지원 받기](https://azure.microsoft.com/support/options/) 를 선택하여 Azure 지원 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="a4617-109">증상</span><span class="sxs-lookup"><span data-stu-id="a4617-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="a4617-110">시나리오 1</span><span class="sxs-lookup"><span data-stu-id="a4617-110">Scenario 1</span></span>
<span data-ttu-id="a4617-111">Resource Manager 배포의 저장소 계정에서 VHD를 삭제하려고 할 때 다음 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="a4617-112">**Blob 'vhds/BlobName.vhd'를 삭제하지 못했습니다. 오류: 현재 Blob에 임대가 있는데 요청에서 임대 ID가 지정되지 않았습니다.**</span><span class="sxs-lookup"><span data-stu-id="a4617-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="a4617-113">이 문제는 가상 컴퓨터(VM)에 삭제하려는 VHD에 대한 임대가 있으므로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="a4617-114">시나리오 2</span><span class="sxs-lookup"><span data-stu-id="a4617-114">Scenario 2</span></span>
<span data-ttu-id="a4617-115">Resource Manager 배포의 저장소 계정에서 컨테이너를 삭제하려고 할 때 다음 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="a4617-116">**저장소 컨테이너 'vhds'를 삭제하지 못했습니다. 오류: 현재 컨테이너에 임대가 있는데 요청에서 임대 ID가 지정되지 않았습니다**.</span><span class="sxs-lookup"><span data-stu-id="a4617-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="a4617-117">이 문제는 컨테이너에 임대 상태에서 잠겨 있는 VHD가 있기 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="a4617-118">시나리오 3</span><span class="sxs-lookup"><span data-stu-id="a4617-118">Scenario 3</span></span>
<span data-ttu-id="a4617-119">Resource Manager 배포의 저장소 계정을 삭제하려고 할 때 다음 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="a4617-120">**저장소 계정 'StorageAccountName'을 삭제하지 못했습니다. 오류: 저장소 계정의 아티팩트가 사용 중이므로 저장소 계정을 삭제할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="a4617-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="a4617-121">이 문제는 저장소 계정에 임대 상태에 있는 VHD가 포함되어 있기 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="a4617-122">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a4617-122">Solution</span></span> 
<span data-ttu-id="a4617-123">이러한 문제를 해결하려면 오류를 일으키는 VHD와 연결된 VM을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="a4617-124">그런 다음 VM(데이터 디스크에 대한)에서 VHD를 분리하거나 VHD(OS 디스크에 대한)를 사용 중인 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="a4617-125">그러면 VHD에서 임대가 제거되어 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="a4617-126">이 작업을 수행하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="a4617-127">방법 1 - Azure Storage 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="a4617-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="a4617-128">1단계 저장소 계정 삭제를 방지하는 VHD 식별</span><span class="sxs-lookup"><span data-stu-id="a4617-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="a4617-129">저장소 계정을 삭제하는 경우 다음과 같은 메시지 대화 상자를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![저장소 계정을 삭제하는 경우의 메시지](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="a4617-131">**디스크 URL**을 확인하여 저장소 계정과 저장소 계정 삭제를 방지하는 VHD를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="a4617-132">다음 예제에서는 ".blob.core.windows.net" 앞의 문자열이 저장소 계정 이름이고, "SCCM2012-2015-08-28.vhd"가 VHD 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="a4617-133">2단계 Azure Storage 탐색기를 사용하여 VHD 삭제</span><span class="sxs-lookup"><span data-stu-id="a4617-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="a4617-134">[Azure Storage 탐색기](http://storageexplorer.com/)의 최신 버전을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="a4617-135">이 도구는 Windows, macOS 및 Linux에서 Azure Storage 데이터로 쉽게 작업할 수 있도록 해주는 Microsoft의 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="a4617-136">Azure Storage 탐색기를 열고 왼쪽 막대에서</span><span class="sxs-lookup"><span data-stu-id="a4617-136">Open Azure Storage Explorer, select</span></span> ![계정 아이콘](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="a4617-138">및 Azure 환경을 차례로 선택한 다음 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="a4617-139">모든 구독을 선택하거나 삭제하려는 저장소 계정이 포함된 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![구독 추가](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="a4617-141">앞의 디스크 URL에서 얻은 저장소 계정으로 이동하여 **BLOB 컨테이너** > **vhd**를 선택하고 저장소 계정 삭제를 방지하는 VHD를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="a4617-142">VHD가 있으면 **VM 이름** 열에서 이 VHD를 사용하는 VM을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![VM 확인](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="a4617-144">Azure Portal을 사용하여 VHD에서 임대를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="a4617-145">자세한 내용은 [VHD에서 임대 제거](#remove-the-lease-from-the-vhd)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4617-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="a4617-146">Azure Storage 탐색기로 이동하여 VHD를 마우스 오른쪽 단추로 클릭하고 삭제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="a4617-147">저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="a4617-148">방법 2 - Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="a4617-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="a4617-149">1단계: 저장소 계정 삭제를 방지하는 VHD 식별</span><span class="sxs-lookup"><span data-stu-id="a4617-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="a4617-150">저장소 계정을 삭제하는 경우 다음과 같은 메시지 대화 상자를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![저장소 계정을 삭제하는 경우의 메시지](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="a4617-152">**디스크 URL**을 확인하여 저장소 계정과 저장소 계정 삭제를 방지하는 VHD를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="a4617-153">다음 예제에서는 ".blob.core.windows.net" 앞의 문자열이 저장소 계정 이름이고, "SCCM2012-2015-08-28.vhd"가 VHD 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="a4617-154">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="a4617-155">허브 메뉴에서 **모든 리소스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="a4617-156">저장소 계정으로 이동한 다음 **Blobs** > **vhds**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![저장소 계정 및 "vhds" 컨테이너가 강조 표시된 포털의 스크린샷](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="a4617-158">앞의 디스크 URL에서 가져온 VHD를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="a4617-159">그런 다음 VHD를 사용 중인 VM을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="a4617-160">일반적으로 VHD의 이름을 확인하여 VHD를 유지하는 VM를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="a4617-161">Resource Manager 개발 모델의 VM</span><span class="sxs-lookup"><span data-stu-id="a4617-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="a4617-162">OS 디스크는 일반적으로 VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="a4617-163">데이터 디스크는 일반적으로 VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="a4617-164">Classic 개발 모델의 VM</span><span class="sxs-lookup"><span data-stu-id="a4617-164">VM in Classic development model</span></span>

   * <span data-ttu-id="a4617-165">OS 디스크는 일반적으로 CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="a4617-166">데이터 디스크는 일반적으로 CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="a4617-167">2단계: VHD에서 임대 제거</span><span class="sxs-lookup"><span data-stu-id="a4617-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="a4617-168">[VHD에서 임대를 제거](#remove-the-lease-from-the-vhd)하고 저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="a4617-169">임대란?</span><span class="sxs-lookup"><span data-stu-id="a4617-169">What is a lease?</span></span>
<span data-ttu-id="a4617-170">임대는 Blob(예를 들어, VHD)에 대한 액세스를 제어하는 데 사용할 수 있는 잠금입니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="a4617-171">Blob가 임대되면 임대 소유자만 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="a4617-172">다음과 같은 이유로 임대가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="a4617-173">여러 소유자가 Blob의 같은 부분에 동시에 쓰려고 하는 경우 데이터 손상이 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="a4617-174">실제로 어떤 항목이 Blob를 사용 중인 경우(예를 들어, VM) Blob가 삭제되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="a4617-175">실제로 어떤 항목이 저장소 계정을 사용 중인 경우(예를 들어, VM) 저장소 계정이 삭제되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="a4617-176">VHD에서 임대 제거</span><span class="sxs-lookup"><span data-stu-id="a4617-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="a4617-177">VHD가 OS 디스크인 경우 VM을 삭제하여 임대를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="a4617-178">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a4617-179">**허브** 메뉴에서 **Virtual Machines**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="a4617-180">VHD에서 임대를 유지하는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="a4617-181">실제로 가상 컴퓨터를 사용 중인 항목이 없고 가상 컴퓨터가 더 이상 필요하지 않음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="a4617-182">**VM 세부 정보** 블레이드 맨 위에서 **삭제**를 선택한 후 **예**를 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="a4617-183">VM은 삭제되지만 VHD는 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="a4617-184">그러나 VHD는 더 이상 임대를 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="a4617-185">임대를 해제하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="a4617-186">임대가 해제되었는지 확인하려면 **모든 리소스** > **저장소 계정 이름** > **Blobs** > **vhds**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="a4617-187">**Blob 속성** 창에서 **임대 상태** 값이 **잠금 해제됨**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="a4617-188">VHD가 데이터 디스크인 경우 VM에서 VHD를 분리하여 임대를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="a4617-189">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a4617-190">**허브** 메뉴에서 **Virtual Machines**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="a4617-191">VHD에서 임대를 유지하는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="a4617-192">**VM 세부 정보** 블레이드에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="a4617-193">VHD에서 임대를 유지하는 데이터 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="a4617-194">VHD의 URL을 확인하여 디스크에 연결된 VHD를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="a4617-195">확실히 데이터 디스크를 사용 중인 항목이 없는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="a4617-196">**디스크 세부 정보** 블레이드에서 **분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="a4617-197">이제 VM에서 디스크가 분리되며 VHD는 더 이상 임대를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="a4617-198">임대를 해제하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="a4617-199">임대가 해제되었는지 확인하려면 **모든 리소스** > **저장소 계정 이름** > **Blobs** > **vhds**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="a4617-200">**Blob 속성** 창에서 **임대 상태** 값이 **잠금 해제됨**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4617-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4617-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4617-201">Next steps</span></span>
* [<span data-ttu-id="a4617-202">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="a4617-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="a4617-203">Microsoft Azure(PowerShell)에서 Blob 저장소의 임대 잠금을 해제하는 방법</span><span class="sxs-lookup"><span data-stu-id="a4617-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
