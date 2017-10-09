---
title: "Powershell 스크립트와 Azure 검색 aaaManage | Microsoft Docs"
description: "PowerShell 스크립트를 사용하여 Azure 검색 서비스를 관리합니다. Azure 검색 서비스 만들기 또는 업데이트 및 Azure 검색 관리자 키 관리"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="56e17-104">PowerShell을 사용한 Azure 검색 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="56e17-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56e17-105">포털</span><span class="sxs-lookup"><span data-stu-id="56e17-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="56e17-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56e17-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="56e17-107">이 항목에서는 다양 한 Azure 검색 서비스에 대 한 관리 작업 hello hello PowerShell 명령을 tooperform 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="56e17-108">검색 서비스 만들기, 확장 및 해당 API 키 관리 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="56e17-109">이 명령은 hello 관리 옵션 hello에서 사용할 수 있는 병렬 [Azure 검색 관리 REST API](http://msdn.microsoft.com/library/dn832684.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56e17-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="56e17-110">Prerequisites</span></span>
* <span data-ttu-id="56e17-111">Azure PowerShell 1.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="56e17-112">자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56e17-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="56e17-113">Tooyour 아래 설명 된 대로 PowerShell에서 Azure 구독에에서 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="56e17-114">먼저 수행 해야이 명령 사용 하 여 로그인 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="56e17-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="56e17-115">Hello Microsoft Azure 로그인 대화 상자에서 Azure 계정 및 암호의 hello 전자 메일 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="56e17-116">또는 [비대화형으로 서비스 주체를 사용하여 로그인](../azure-resource-manager/resource-group-authenticate-service-principal.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="56e17-117">여러 Azure 구독이 있는 경우 tooset 프로그램 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="56e17-118">현재 구독 목록이 toosee이이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="56e17-119">toospecify hello 구독을 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="56e17-120">다음 예제는 hello, hello 구독 이름은 `ContosoSubscription`합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="56e17-121">시작 하려면 명령 toohelp</span><span class="sxs-lookup"><span data-stu-id="56e17-121">Commands toohelp you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="56e17-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56e17-122">Next Steps</span></span>
<span data-ttu-id="56e17-123">서비스를 만든 했으므로 hello 다음 단계를 수행할 수 있습니다: 빌드는 [인덱스](search-what-is-an-index.md), [인덱스를 쿼리하여](search-query-overview.md), 및 마지막으로 만들기 및 Azure 검색을 사용 하는 사용자의 검색 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="56e17-124">Hello Azure 포털에서에서 Azure 검색 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="56e17-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="56e17-125">쿼리 검색 탐색기를 사용 하 여 hello Azure 포털에서에서 Azure 검색 인덱스</span><span class="sxs-lookup"><span data-stu-id="56e17-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="56e17-126">인덱서 tooload 데이터를 사용 하 여 다른 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e17-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="56e17-127">.NET에서 toouse Azure 검색 하는 방법</span><span class="sxs-lookup"><span data-stu-id="56e17-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="56e17-128">Azure 검색 트래픽 분석</span><span class="sxs-lookup"><span data-stu-id="56e17-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

