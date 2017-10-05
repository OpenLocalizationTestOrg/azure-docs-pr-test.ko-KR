---
title: "저장소 액세스 키 롤링 후 Media Services 업데이트 | Microsoft Docs"
description: "이 문서에서는 저장소 액세스 키를 롤링한 후 미디어 서비스를 업데이트하는 방법에 대한 지침을 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 304e72e0d2d4a7e95df513e6d5481def9eae3f68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="adafa-103">저장소 액세스 키 롤링 후 Media Services 업데이트</span><span class="sxs-lookup"><span data-stu-id="adafa-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="adafa-104">새 AMS(Azure Media Services) 계정을 만들 때 미디어 콘텐츠를 저장하는 데 사용되는 Azure Storage 계정을 선택하도록 요청받습니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="adafa-105">Media Services 계정에 저장소 계정을 둘 이상 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="adafa-106">이 항목에서는 저장소 키를 회전하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-106">This topic shows how to rotate storage keys.</span></span> <span data-ttu-id="adafa-107">또한 미디어 계정에 저장소 계정을 추가하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="adafa-108">이 항목에서 설명하는 작업을 수행하려면 [ARM API](https://docs.microsoft.com/rest/api/media/mediaservice) 및 [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-108">To perform the actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="adafa-109">자세한 내용은 [PowerShell 및 Resource Manager로 Azure 리소스를 관리하는 방법](../azure-resource-manager/powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adafa-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="adafa-110">개요</span><span class="sxs-lookup"><span data-stu-id="adafa-110">Overview</span></span>

<span data-ttu-id="adafa-111">새 저장소 계정이 만들어지면 Azure는 2개의 512비트 저장소 액세스 키를 만들며, 이는 저장소 계정에 대한 액세스를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="adafa-112">저장소 연결을 보다 안전하게 유지하려면 저장소 액세스 키를 주기적으로 다시 생성하고 회전하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="adafa-113">2개의 액세스 키(기본 및 보조)는 다른 액세스 키를 다시 생성하는 동안 하나의 액세스 키를 사용하여 저장소 계정에 대한 연결을 유지할 수 있도록 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="adafa-114">이 과정은 "액세스 키 롤링"이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="adafa-115">미디어 서비스는 제공되는 저장소 키에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="adafa-116">특히, 자산을 스트림 또는 다운로드하는 데 사용되는 로케이터는 지정된 저장소 액세스 키에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="adafa-117">AMS 계정을 만들 때 기본적으로 기본 저장소 액세스 키에 종속되지만 사용자는 AMS의 저장소 키를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-117">When an AMS account is created it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="adafa-118">이 토픽에 설명된 다음과 같은 절차에 따라 사용할 키를 Media Services에 알려 주어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-118">You must make sure to let Media Services know which key to use by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="adafa-119">여러 저장소 계정이 있는 경우 각각의 저장소 계정마다 이 과정을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="adafa-120">저장 키를 회전하는 순서는 고정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="adafa-121">보조 키를 먼저 회전시킨 다음 기본 키를 회전하거나 그 반대로 회전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="adafa-122">이 토픽에서 설명한 단계를 프로덕션 계정에서 실행하기 전에 사전 프로덕션 계정에서 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-122">Before executing steps described in this topic on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="adafa-123">저장 키를 회전하는 단계</span><span class="sxs-lookup"><span data-stu-id="adafa-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="adafa-124">PowerShell cmdlet 또는 [Azure](https://portal.azure.com/) 포털을 통해 저장소 계정 기본 키를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="adafa-125">적절한 매개 변수로 Sync-AzureRmMediaServiceStorageKeys cmdlet을 호출하여 미디어 계정에서 저장소 계정 키를 가져오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="adafa-126">다음 예제에서는 키를 저장소 계정에 동기화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="adafa-127">1 시간 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-127">Wait an hour or so.</span></span> <span data-ttu-id="adafa-128">스트리밍 시나리오가 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="adafa-129">PowerShell cmdlet 또는 Azure Portal을 통해 저장소 계정 보조 키를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="adafa-130">적절한 매개 변수로 Sync-AzureRmMediaServiceStorageKeys PowerShell cmdlet을 호출하여 미디어 계정에서 새 저장소 계정 키를 가져오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="adafa-131">1 시간 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-131">Wait an hour or so.</span></span> <span data-ttu-id="adafa-132">스트리밍 시나리오가 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="adafa-133">PowerShell cmdlet 예제</span><span class="sxs-lookup"><span data-stu-id="adafa-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="adafa-134">다음 예제에서는 저장소 계정을 가져와서 AMS 계정과 동기화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="adafa-135">AMS 계정에 저장소 계정을 추가하는 단계</span><span class="sxs-lookup"><span data-stu-id="adafa-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="adafa-136">[Media Services 계정에 여러 저장소 계정 연결](meda-services-managing-multiple-storage-accounts.md) 문서에서 AMS 계정에 저장소 계정을 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adafa-136">The following topic shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="adafa-137">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="adafa-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="adafa-138">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="adafa-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="adafa-139">승인</span><span class="sxs-lookup"><span data-stu-id="adafa-139">Acknowledgments</span></span>
<span data-ttu-id="adafa-140">이 문서를 만들 때 기여한 다음 사람들에게 감사 드리고자 합니다. Cenk Dingiloglu, Milan Gada, Seva Titov</span><span class="sxs-lookup"><span data-stu-id="adafa-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
