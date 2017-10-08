---
title: "저장소 롤링 후 aaaUpdate 미디어 서비스 액세스 키 | Microsoft Docs"
description: "이 문서 저장소 롤링 후 tooupdate 미디어 서비스 키를 액세스 하는 방법에 대 한 지침을 제공 합니다."
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
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="a9b86-103">저장소 액세스 키 롤링 후 Media Services 업데이트</span><span class="sxs-lookup"><span data-stu-id="a9b86-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="a9b86-104">새 Azure 미디어 서비스 (AMS) 계정을 만들 때 ´ â Azure 저장소 계정 즉 tooselect toostore 미디어 콘텐츠를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="a9b86-105">둘 이상의 저장소 계정을 tooyour 미디어 서비스 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="a9b86-106">이 항목에서는 방법을 toorotate 저장소 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="a9b86-107">또한 tooadd 저장소 tooa 미디어 계정을 계정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="a9b86-108">이 항목에 설명 된 tooperform hello 작업을 사용 해야 [ARM Api](https://docs.microsoft.com/rest/api/media/mediaservice) 및 [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="a9b86-109">자세한 내용은 참조 [어떻게 toomanage Azure PowerShell 및 리소스 관리자를 사용 하 여 리소스](../azure-resource-manager/powershell-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a9b86-110">개요</span><span class="sxs-lookup"><span data-stu-id="a9b86-110">Overview</span></span>

<span data-ttu-id="a9b86-111">새 저장소 계정이 만들어질 때 Azure에서는 두 개의 512 비트 저장소 액세스 키를 사용 하는 tooauthenticate을 발생 하는 tooyour 저장소 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="a9b86-112">tookeep 보다 안전한 tooperiodically 좋습니다 저장소 연결을 다시 생성 한 저장소 액세스 키를 회전 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="a9b86-113">두 개의 액세스 키 (기본 및 보조)에 순서 tooenable toomaintain 연결 toohello 저장소 계정 하나를 사용 하 여 액세스 키 hello를 다시 생성 하는 동안 다른 선택 키 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="a9b86-114">이 과정은 "액세스 키 롤링"이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="a9b86-115">미디어 서비스 tooit 제공 된 저장소 키에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="a9b86-116">특히 사용 되는 toostream 또는 자산을 다운로드 하는 hello 로케이터가 hello 지정 된 저장소 액세스 키에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="a9b86-117">AMS 계정이 만들어질 때 기본적으로 hello 기본 저장소 액세스 키에 대 한 종속성 걸리는 하지만 사용자로 AMS을가지고 있는 hello 저장소 키를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="a9b86-118">알아두어야 toolet 미디어 서비스 키 toouse는이 항목에 설명 된 단계를 수행 하 여 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="a9b86-119">여러 저장소 계정이 있는 경우 각각의 저장소 계정마다 이 과정을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="a9b86-120">저장소 키를 회전 하는 hello 순서 고정이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="a9b86-121">먼저 hello 보조 키를 회전 수 있으며 다음 기본 키 만들거나 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="a9b86-122">단계를 실행 하기 전에이 항목에서 설명 확인 되었는지 tootest 프로덕션 계정에서 해당 프로덕션 전 계정에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="a9b86-123">단계 toorotate 저장소 키</span><span class="sxs-lookup"><span data-stu-id="a9b86-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="a9b86-124">변경 hello 저장소 계정 기본 키 hello powershell cmdlet 통해 또는 [Azure](https://portal.azure.com/) 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="a9b86-125">저장소 계정 키를 tooforce 미디어 계정 toopick 적절 한 매개 변수를 사용 하 여 동기화 AzureRmMediaServiceStorageKeys cmdlet을 호출</span><span class="sxs-lookup"><span data-stu-id="a9b86-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="a9b86-126">다음 예제는 hello toosync toostorage 계정 키 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="a9b86-127">1 시간 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-127">Wait an hour or so.</span></span> <span data-ttu-id="a9b86-128">Hello 스트리밍 시나리오 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="a9b86-129">Hello powershell cmdlet 또는 Azure 포털을 통해 저장소 계정 보조 키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="a9b86-130">적절 한 params tooforce 미디어 계정 toopick 새 저장소 계정 키를 사용 하 여 동기화 AzureRmMediaServiceStorageKeys powershell을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="a9b86-131">1 시간 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-131">Wait an hour or so.</span></span> <span data-ttu-id="a9b86-132">Hello 스트리밍 시나리오 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="a9b86-133">PowerShell cmdlet 예제</span><span class="sxs-lookup"><span data-stu-id="a9b86-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="a9b86-134">hello 다음 방법을 보여 주는 예제 tooget 저장소 계정 hello hello AMS 계정과 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="a9b86-135">단계 tooadd 저장소 계정 tooyour AMS 계정</span><span class="sxs-lookup"><span data-stu-id="a9b86-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="a9b86-136">hello 다음 항목에서는 방법을 tooadd 저장소 계정 tooyour AMS 계정: [여러 저장소 계정을 미디어 서비스 계정 tooa 연결](meda-services-managing-multiple-storage-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a9b86-137">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a9b86-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9b86-138">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a9b86-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="a9b86-139">승인</span><span class="sxs-lookup"><span data-stu-id="a9b86-139">Acknowledgments</span></span>
<span data-ttu-id="a9b86-140">이 문서를 만들 때 제공한 사람 다음 tooacknowledge hello 같은: Cenk Dingiloglu, Milan Gada Seva Titov 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9b86-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
