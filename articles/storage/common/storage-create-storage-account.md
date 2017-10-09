---
title: "aaaHow toocreate 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 | Microsoft Docs"
description: "새 저장소 계정 만들기, 계정 액세스 키를 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 합니다. 표준 및 프리미엄 저장소 계정에 대해 알아봅니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a><span data-ttu-id="21683-104">Azure 저장소 계정 정보</span><span class="sxs-lookup"><span data-stu-id="21683-104">About Azure storage accounts</span></span>
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="21683-105">개요</span><span class="sxs-lookup"><span data-stu-id="21683-105">Overview</span></span>
<span data-ttu-id="21683-106">Azure 저장소 계정을 고유한 네임 스페이스 toostore 제공 및 Azure 저장소 데이터 개체에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-106">An Azure storage account provides a unique namespace toostore and access your Azure Storage data objects.</span></span> <span data-ttu-id="21683-107">저장소 계정의 모든 개체는 그룹으로 합산 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-107">All objects in a storage account are billed together as a group.</span></span> <span data-ttu-id="21683-108">Hello 계정의 데이터는 기본적으로 사용할 수 있는 유일한 tooyou hello 계정 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-108">By default, hello data in your account is available only tooyou, hello account owner.</span></span>

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a><span data-ttu-id="21683-109">저장소 계정 사용 비용</span><span class="sxs-lookup"><span data-stu-id="21683-109">Storage account billing</span></span>
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> <span data-ttu-id="21683-110">Azure 가상 컴퓨터를 만들 때 저장소 계정 수에 대 한 경우 자동으로 만들어집니다 hello 배포 위치에서 해당 위치에 저장소 계정을 아직 없는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-110">When you create an Azure virtual machine, a storage account is created for you automatically in hello deployment location if you do not already have a storage account in that location.</span></span> <span data-ttu-id="21683-111">따라서 가상 컴퓨터 디스크에 대 한 저장소 계정 toocreate 아래 필요한 toofollow hello 단계는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-111">So it's not necessary toofollow hello steps below toocreate a storage account for your virtual machine disks.</span></span> <span data-ttu-id="21683-112">hello 저장소 계정 이름은 hello 가상 컴퓨터 이름 기반 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-112">hello storage account name will be based on hello virtual machine name.</span></span> <span data-ttu-id="21683-113">Hello 참조 [Azure 가상 컴퓨터 설명서](https://azure.microsoft.com/documentation/services/virtual-machines/) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-113">See hello [Azure Virtual Machines documentation](https://azure.microsoft.com/documentation/services/virtual-machines/) for more details.</span></span>
> 
> 

## <a name="storage-account-endpoints"></a><span data-ttu-id="21683-114">저장소 계정 끝점</span><span class="sxs-lookup"><span data-stu-id="21683-114">Storage account endpoints</span></span>
<span data-ttu-id="21683-115">Azure 저장소에 저장되는 모든 개체에는 고유한 URL 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-115">Every object that you store in Azure Storage has a unique URL address.</span></span> <span data-ttu-id="21683-116">hello 저장소 계정 이름 형식은 hello 해당 주소의 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-116">hello storage account name forms hello subdomain of that address.</span></span> <span data-ttu-id="21683-117">hello는 특정 tooeach 서비스 하위 도메인 및 도메인 이름 조합이 형성 된 *끝점* 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-117">hello combination of subdomain and domain name, which is specific tooeach service, forms an *endpoint* for your storage account.</span></span>

<span data-ttu-id="21683-118">예를 들어 저장소 계정의 이름이 *mystorageaccount*, 저장소 계정에 대 한 hello 기본 끝점은 다음:</span><span class="sxs-lookup"><span data-stu-id="21683-118">For example, if your storage account is named *mystorageaccount*, then hello default endpoints for your storage account are:</span></span>

* <span data-ttu-id="21683-119">Blob 서비스: http://*mystorageaccount*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="21683-119">Blob service: http://*mystorageaccount*.blob.core.windows.net</span></span>
* <span data-ttu-id="21683-120">Table service: http://*mystorageaccount*.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="21683-120">Table service: http://*mystorageaccount*.table.core.windows.net</span></span>
* <span data-ttu-id="21683-121">큐 서비스: http://*mystorageaccount*.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="21683-121">Queue service: http://*mystorageaccount*.queue.core.windows.net</span></span>
* <span data-ttu-id="21683-122">파일 서비스: http://*mystorageaccount*.file.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="21683-122">File service: http://*mystorageaccount*.file.core.windows.net</span></span>

> [!NOTE]
> <span data-ttu-id="21683-123">Blob 저장소 계정 hello Blob 서비스 끝점을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-123">A Blob storage account only exposes hello Blob service endpoint.</span></span>
> 
> 

<span data-ttu-id="21683-124">저장소 계정에는 개체에 액세스 하기 위한 hello URL hello 저장소 계정 toohello 끝점에서 hello 개체의 위치를 추가 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="21683-124">hello URL for accessing an object in a storage account is built by appending hello object's location in hello storage account toohello endpoint.</span></span> <span data-ttu-id="21683-125">예를 들어 Blob 주소의 형식은 다음과 같습니다. http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*</span><span class="sxs-lookup"><span data-stu-id="21683-125">For example, a blob address might have this format: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.</span></span>

<span data-ttu-id="21683-126">사용자 지정 도메인 이름을 toouse 스토리지 계정으로 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-126">You can also configure a custom domain name toouse with your storage account.</span></span> <span data-ttu-id="21683-127">자세한 내용은 [Blob Storage 끝점에 대한 사용자 지정 도메인 이름 구성](../blobs/storage-custom-domain-name.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-127">For more information, see [Configure a custom domain Name for your Blob Storage Endpoint](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="21683-128">PowerShell에서도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-128">You can also configure it with PowerShell.</span></span> <span data-ttu-id="21683-129">자세한 내용은 참조 hello [집합 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="21683-129">For more information, see hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.</span></span>  


## <a name="create-a-storage-account"></a><span data-ttu-id="21683-130">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="21683-130">Create a storage account</span></span>
1. <span data-ttu-id="21683-131">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-131">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="21683-132">Hello 허브 메뉴에서 선택 **새로** -> **저장소** -> **저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-132">On hello Hub menu, select **New** -> **Storage** -> **Storage account**.</span></span>
3. <span data-ttu-id="21683-133">저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-133">Enter a name for your storage account.</span></span> <span data-ttu-id="21683-134">참조 [저장소 계정 끝점](#storage-account-endpoints) 에 대 한 자세한 내용을 hello 저장소 계정 이름을 사용 하는 tooaddress 되는 방식을 Azure 저장소의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-134">See [Storage account endpoints](#storage-account-endpoints) for details about how hello storage account name will be used tooaddress your objects in Azure Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="21683-135">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-135">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>
   > 
   > <span data-ttu-id="21683-136">저장소 계정 이름은 Azure 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-136">Your storage account name must be unique within Azure.</span></span> <span data-ttu-id="21683-137">Azure 포털 hello 선택한 hello 저장소 계정 이름은 이미 사용 중인지 여부 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-137">hello Azure portal will indicate if hello storage account name you select is already in use.</span></span>
   > 
   > 
4. <span data-ttu-id="21683-138">Hello 배포 모델 toobe 사용 지정: **리소스 관리자** 또는 **클래식**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-138">Specify hello deployment model toobe used: **Resource Manager** or **Classic**.</span></span> <span data-ttu-id="21683-139">**리소스 관리자** hello 배포 모델 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-139">**Resource Manager** is hello recommended deployment model.</span></span> <span data-ttu-id="21683-140">자세한 내용은 [리소스 관리자 배포 및 클래식 배포 이해](../../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-140">For more information, see [Understanding Resource Manager deployment and classic deployment](../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="21683-141">Blob 저장소 계정은 hello 리소스 관리자 배포 모델을 사용 하 여 서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-141">Blob storage accounts can only be created using hello Resource Manager deployment model.</span></span>

5. <span data-ttu-id="21683-142">Hello 유형의 저장소 계정 선택: **범용** 또는 **Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-142">Select hello type of storage account: **General purpose** or **Blob storage**.</span></span> <span data-ttu-id="21683-143">**일반 용도의** hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-143">**General purpose** is hello default.</span></span>
   
    <span data-ttu-id="21683-144">경우 **범용** 을 선택한 다음 hello 성능 계층을 지정: **표준** 또는 **프리미엄**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-144">If **General purpose** was selected, then specify hello performance tier: **Standard** or **Premium**.</span></span> <span data-ttu-id="21683-145">hello 기본값은 **표준**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-145">hello default is **Standard**.</span></span> <span data-ttu-id="21683-146">표준 및 프리미엄 저장소 계정에 대 한 자세한 내용은 참조 하십시오. [Azure 저장소 소개 tooMicrosoft](storage-introduction.md) 및 [프리미엄 저장소: Azure 가상 컴퓨터 워크 로드 용 고성능 저장소](storage-premium-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-146">For more details on standard and premium storage accounts, see [Introduction tooMicrosoft Azure Storage](storage-introduction.md) and [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span>
   
    <span data-ttu-id="21683-147">경우 **Blob 저장소** 을 선택한 다음 hello 액세스 계층을 지정: **핫** 또는 **쿨**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-147">If **Blob Storage** was selected, then specify hello access tier: **Hot** or **Cool**.</span></span> <span data-ttu-id="21683-148">hello 기본값은 **핫**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-148">hello default is **Hot**.</span></span> <span data-ttu-id="21683-149">자세한 내용은 [Azure Blob 저장소: 쿨 및 핫 계층](../blobs/storage-blob-storage-tiers.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-149">See [Azure Blob Storage: Cool and Hot tiers](../blobs/storage-blob-storage-tiers.md) for more details.</span></span>
6. <span data-ttu-id="21683-150">Hello 저장소 계정에 대 한 hello 복제 옵션을 선택: **LRS**, **GRS**, **RA-GRS**, 또는 **ZRS**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-150">Select hello replication option for hello storage account: **LRS**, **GRS**, **RA-GRS**, or **ZRS**.</span></span> <span data-ttu-id="21683-151">hello 기본값은 **RA-GRS**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-151">hello default is **RA-GRS**.</span></span> <span data-ttu-id="21683-152">Azure 저장소 복제 옵션에 대한 자세한 내용은 아래의 [Azure 저장소 복제](storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-152">For more details on Azure Storage replication options, see [Azure Storage replication](storage-redundancy.md).</span></span>
7. <span data-ttu-id="21683-153">Hello 구독 하려는 toocreate hello 새 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-153">Select hello subscription in which you want toocreate hello new storage account.</span></span>
8. <span data-ttu-id="21683-154">새 리소스 그룹을 지정하거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-154">Specify a new resource group or select an existing resource group.</span></span> <span data-ttu-id="21683-155">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-155">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>
9. <span data-ttu-id="21683-156">저장소 계정에 대 한 hello 지리적 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-156">Select hello geographic location for your storage account.</span></span> <span data-ttu-id="21683-157">각 지역에서 어떤 서비스가 가능한지에 대한 자세한 정보는 [Azure 지역](https://azure.microsoft.com/regions/#services) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-157">See [Azure Regions](https://azure.microsoft.com/regions/#services) for more information about what services are available in which region.</span></span>
10. <span data-ttu-id="21683-158">클릭 **만들기** toocreate hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-158">Click **Create** toocreate hello storage account.</span></span>

## <a name="manage-your-storage-account"></a><span data-ttu-id="21683-159">저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="21683-159">Manage your storage account</span></span>
### <a name="change-your-account-configuration"></a><span data-ttu-id="21683-160">계정 구성 변경</span><span class="sxs-lookup"><span data-stu-id="21683-160">Change your account configuration</span></span>
<span data-ttu-id="21683-161">저장소 계정을 만든 후에 hello 계정 또는 Blob 저장소 계정에 대 한 변경 hello 액세스 계층에 사용 되는 hello 복제 옵션을 변경 하는 등의 구성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-161">After you create your storage account, you can modify its configuration, such as changing hello replication option used for hello account or changing hello access tier for a Blob storage account.</span></span> <span data-ttu-id="21683-162">Hello에 [Azure 포털](https://portal.azure.com), tooyour 저장소 계정, 찾기 및 클릭 탐색 **구성** 아래 **설정을** hello 계정 구성을 tooview 및/또는 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-162">In hello [Azure portal](https://portal.azure.com), navigate tooyour storage account, find and click **Configuration** under **SETTINGS** tooview and/or change hello account configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="21683-163">Hello 저장소 계정을 만들 때 선택한 hello 성능 계층에 따라 일부 복제 옵션을 사용 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-163">Depending on hello performance tier you chose when creating hello storage account, some replication options may not be available.</span></span>
> 
> 

<span data-ttu-id="21683-164">Hello 복제 옵션을 변경 하면 가격 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-164">Changing hello replication option will change your pricing.</span></span> <span data-ttu-id="21683-165">자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-165">For more details, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) page.</span></span>

<span data-ttu-id="21683-166">Hello 액세스 계층을 변경 하는 저장소 계정, 청구할 수 Blob에 대 한 hello에 대 한 요금이 변경 또한 toochanging 가격 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-166">For Blob storage accounts, changing hello access tier may incur charges for hello change in addition toochanging your pricing.</span></span> <span data-ttu-id="21683-167">Hello를 참조 하십시오 [Blob 저장소 계정-가격 및 요금 청구](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-167">Please see hello [Blob storage accounts - Pricing and Billing](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) for more details.</span></span>

### <a name="manage-your-storage-access-keys"></a><span data-ttu-id="21683-168">저장소 액세스 키 다시 관리</span><span class="sxs-lookup"><span data-stu-id="21683-168">Manage your storage access keys</span></span>
<span data-ttu-id="21683-169">저장소 계정을 만들 때 Azure hello 저장소 계정에 액세스할 때 인증에 사용 되는 두 개의 512 비트 저장소 액세스 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-169">When you create a storage account, Azure generates two 512-bit storage access keys, which are used for authentication when hello storage account is accessed.</span></span> <span data-ttu-id="21683-170">두 개의 저장소 액세스 키를 제공 함으로써 Azure를 사용 하면 중단 tooyour 저장소 서비스와 액세스 toothat 서비스 없는 tooregenerate hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-170">By providing two storage access keys, Azure enables you tooregenerate hello keys with no interruption tooyour storage service or access toothat service.</span></span>

> [!NOTE]
> <span data-ttu-id="21683-171">저장소 액세스 키를 다른 사람과 공유하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-171">We recommend that you avoid sharing your storage access keys with anyone else.</span></span> <span data-ttu-id="21683-172">사용할 수 있습니다 toopermit toostorage 리소스 액세스 키를 정지 하지 않고도 액세스 한 *공유 액세스 서명을*합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-172">toopermit access toostorage resources without giving out your access keys, you can use a *shared access signature*.</span></span> <span data-ttu-id="21683-173">공유 액세스 서명을 지정 하는 hello 사용 권한 및 사용자가 정의한 간격에 대 한 계정에 대 한 액세스 tooa 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-173">A shared access signature provides access tooa resource in your account for an interval that you define and with hello permissions that you specify.</span></span> <span data-ttu-id="21683-174">자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-174">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a><span data-ttu-id="21683-175">저장소 액세스 키 보기 및 복사</span><span class="sxs-lookup"><span data-stu-id="21683-175">View and copy storage access keys</span></span>
<span data-ttu-id="21683-176">Hello에 [Azure 포털](https://portal.azure.com), tooyour 저장소 계정을 탐색, 클릭 **모든 설정을** 클릭 하 고 **액세스 키** tooview, 복사 및 계정 액세스 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-176">In hello [Azure portal](https://portal.azure.com), navigate tooyour storage account, click **All settings** and then click **Access keys** tooview, copy, and regenerate your account access keys.</span></span> <span data-ttu-id="21683-177">hello **선택 키** 블레이드에 toouse 응용 프로그램에서 복사할 수 있음을 기본 및 보조 키를 사용 하 여 미리 구성 된 연결 문자열도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-177">hello **Access Keys** blade also includes pre-configured connection strings using your primary and secondary keys that you can copy toouse in your applications.</span></span>

#### <a name="regenerate-storage-access-keys"></a><span data-ttu-id="21683-178">저장소 액세스 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="21683-178">Regenerate storage access keys</span></span>
<span data-ttu-id="21683-179">Tooyour 저장소 계정을 정기적으로 저장소 연결 보안 toohelp 유지 hello 선택 키를 변경 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-179">We recommend that you change hello access keys tooyour storage account periodically toohelp keep your storage connections secure.</span></span> <span data-ttu-id="21683-180">두 개의 액세스 키에는 다른 선택 키 hello를 다시 생성 하는 동안에 하나의 선택 키를 사용 하 여 연결 toohello 저장소 계정을 유지 관리할 수 있도록 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-180">Two access keys are assigned so that you can maintain connections toohello storage account by using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="21683-181">액세스 키 다시 생성 하는 hello 저장소 계정에 의존 하는 응용 프로그램 뿐만 아니라 Azure에서 서비스 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-181">Regenerating your access keys can affect services in Azure as well as your own applications that are dependent on hello storage account.</span></span> <span data-ttu-id="21683-182">Hello 액세스 키 tooaccess hello 저장소 계정을 사용 하는 모든 클라이언트에 업데이트 된 toouse hello에 대 한 새 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-182">All clients that use hello access key tooaccess hello storage account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="21683-183">**미디어 서비스** -저장소 계정에 의존 하는 미디어 서비스를 사용 하도록 설정한 경우 다시 동기화 해야 hello 선택 키를 미디어 서비스 hello 키를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-183">**Media services** - If you have media services that are dependent on your storage account, you must re-sync hello access keys with your media service after you regenerate hello keys.</span></span>

<span data-ttu-id="21683-184">**응용 프로그램** -웹 응용 프로그램 또는 클라우드 서비스를 사용 하 여 hello 저장소 계정 손실 됩니다 hello 연결 키를 다시 생성 하는 경우 키 롤 하지 않는 한 경우.</span><span class="sxs-lookup"><span data-stu-id="21683-184">**Applications** - If you have web applications or cloud services that use hello storage account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span>

<span data-ttu-id="21683-185">**저장소 탐색기** -를 사용 하는 경우 [저장소 탐색기 응용 프로그램](storage-explorers.md), 해당 응용 프로그램에서 사용 되는 tooupdate hello 저장소 키를 시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-185">**Storage Explorers** - If you are using any [storage explorer applications](storage-explorers.md), you will probably need tooupdate hello storage key used by those applications.</span></span>

<span data-ttu-id="21683-186">저장소 액세스 키를 회전 하기 위한 hello 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-186">Here is hello process for rotating your storage access keys:</span></span>

1. <span data-ttu-id="21683-187">Hello 저장소 계정의 프로그램 응용 프로그램 코드 tooreference hello 보조 액세스 키의 hello 연결 문자열을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-187">Update hello connection strings in your application code tooreference hello secondary access key of hello storage account.</span></span>
2. <span data-ttu-id="21683-188">저장소 계정에 대 한 hello 기본 액세스 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-188">Regenerate hello primary access key for your storage account.</span></span> <span data-ttu-id="21683-189">Hello에 **선택 키** 블레이드에서 클릭 **Key1 다시 생성**, 클릭 하 고 **예** tooconfirm toogenerate 새 키를 지정 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-189">On hello **Access Keys** blade, click **Regenerate Key1**, and then click **Yes** tooconfirm that you want toogenerate a new key.</span></span>
3. <span data-ttu-id="21683-190">코드 tooreference hello 새 기본 액세스 키의 hello 연결 문자열을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-190">Update hello connection strings in your code tooreference hello new primary access key.</span></span>
4. <span data-ttu-id="21683-191">Regenerate hello 보조 액세스 키를 hello 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-191">Regenerate hello secondary access key in hello same manner.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="21683-192">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="21683-192">Delete a storage account</span></span>
<span data-ttu-id="21683-193">tooremove 더 이상 사용 하는 저장소 계정을 탐색 hello toohello 저장소 계정의 [Azure 포털](https://portal.azure.com)를 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-193">tooremove a storage account that you are no longer using, navigate toohello storage account in hello [Azure portal](https://portal.azure.com), and click **Delete**.</span></span> <span data-ttu-id="21683-194">저장소 계정 삭제 hello 전체 계정, 모든 데이터를 포함 하 여 hello 계정에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-194">Deleting a storage account deletes hello entire account, including all data in hello account.</span></span>

> [!WARNING]
> <span data-ttu-id="21683-195">불가능 toorestore 삭제 된 저장소 계정 또는 hello 콘텐츠를 삭제 하기 전에 목록에 포함 된 모든 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-195">It's not possible toorestore a deleted storage account or retrieve any of hello content that it contained before deletion.</span></span> <span data-ttu-id="21683-196">Hello 계정을 삭제 하기 전에 toosave를 원하는 있는지 tooback 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-196">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="21683-197">이 모든 리소스에 대 한 true hello 계정에서-blob, 테이블, 큐 또는 파일을 삭제 하면 영구적으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21683-197">This also holds true for any resources in hello account—once you delete a blob, table, queue, or file, it is permanently deleted.</span></span>
> 

<span data-ttu-id="21683-198">Azure 가상 컴퓨터와 연결 된 저장소 계정을 toodelete 시도 하면 아직 사용 중인 hello 저장소 계정에 대 한 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21683-198">If you try toodelete a storage account associated with an Azure virtual machine, you may get an error about hello storage account still being in use.</span></span> <span data-ttu-id="21683-199">이 오류의 문제를 해결하는 도움말은 [저장소 계정을 삭제할 때 오류 문제 해결](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21683-199">For help troubleshooting this error, please see [Troubleshoot errors when you delete storage accounts](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21683-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21683-200">Next steps</span></span>
* <span data-ttu-id="21683-201">[Microsoft Azure 저장소 탐색기](../../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="21683-201">[Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="21683-202">Azure Blob 저장소: 쿨 및 핫 계층</span><span class="sxs-lookup"><span data-stu-id="21683-202">Azure Blob Storage: Cool and Hot tiers</span></span>](../blobs/storage-blob-storage-tiers.md)
* [<span data-ttu-id="21683-203">Azure 저장소 복제</span><span class="sxs-lookup"><span data-stu-id="21683-203">Azure Storage replication</span></span>](storage-redundancy.md)
* [<span data-ttu-id="21683-204">Azure 저장소 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="21683-204">Configure Azure Storage Connection Strings</span></span>](../storage-configure-connection-string.md)
* [<span data-ttu-id="21683-205">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-205">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
* <span data-ttu-id="21683-206">Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="21683-206">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

