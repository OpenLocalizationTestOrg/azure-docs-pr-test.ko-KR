---
title: "Powershell 사용한 관리 aaaAzure Cosmos DB 자동화-| Microsoft Docs"
description: "Azure Powershell을 사용하여 Azure Cosmos DB 계정을 관리합니다."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="13991-103">PowerShell을 사용하여 Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="13991-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="13991-104">hello 다음 가이드에서는 설명 Azure Powershell을 사용 하 여 Azure Cosmos DB 데이터베이스 계정 명령 tooautomate 관리.</span><span class="sxs-lookup"><span data-stu-id="13991-104">hello following guide describes commands tooautomate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="13991-105">에 포함 되어 명령 toomanage 계정 키 및 장애 조치 우선 순위에서 [다중 지역 데이터베이스 계정][scaling-globally]합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-105">It also includes commands toomanage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="13991-106">데이터베이스 계정을 업데이트 하는 사용 하면 toomodify 일관성 정책 및 영역 추가/제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-106">Updating your database account allows you toomodify consistency policies and add/remove regions.</span></span> <span data-ttu-id="13991-107">Azure Cosmos DB 계정의 플랫폼 간 관리를 위해 사용할 수 있습니다 [Azure CLI](cli-samples.md), hello [리소스 공급자 REST API][rp-rest-api], 또는 hello [Azure 포털](create-documentdb-dotnet.md#create-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), hello [Resource Provider REST API][rp-rest-api], or hello [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="13991-108">시작하기</span><span class="sxs-lookup"><span data-stu-id="13991-108">Getting Started</span></span>

<span data-ttu-id="13991-109">Hello 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고] [ powershell-install-configure] tooinstall tooyour Azure 리소스 관리자 로그인 계정에 Powershell 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-109">Follow hello instructions in [How tooinstall and configure Azure PowerShell][powershell-install-configure] tooinstall and log in tooyour Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="13991-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="13991-110">Notes</span></span>

* <span data-ttu-id="13991-111">Tooexecute hello 사용자에 게 확인 하지 않고도 명령 뒤, 원하는 경우 추가 hello `-Force` toohello 명령 플래그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-111">If you would like tooexecute hello following commands without requiring user confirmation, append hello `-Force` flag toohello command.</span></span>
* <span data-ttu-id="13991-112">다음 명령은 모든 hello는 동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-112">All hello following commands are synchronous.</span></span>

## <span data-ttu-id="13991-113"><a id="create-documentdb-account-powershell"></a> Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="13991-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="13991-114">이 명령은 Azure Cosmos DB 데이터베이스 계정 toocreate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-114">This command allows you toocreate an Azure Cosmos DB database account.</span></span> <span data-ttu-id="13991-115">새 데이터베이스 계정을 특정 [일관성 정책](consistency-levels.md)을 사용하여 단일 하위 지역 또는 [다중 하위 지역][scaling-globally]으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="13991-116">`<write-region-location>`hello의 hello 위치 이름 hello 데이터베이스 계정의 지역을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-116">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="13991-117">이 위치는 필수 toohave 장애 조치 우선 순위 값이 0입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-117">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="13991-118">데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="13991-119">`<read-region-location>`hello 데이터베이스 계정의 지역 대 한 읽기의 hello hello 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-119">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="13991-120">이 위치는 필수 toohave 장애 조치 우선 순위 값이 0 보다 큰 값입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-120">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="13991-121">데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="13991-122">`<ip-range-filter>`Hello 허용 지정된 데이터베이스 계정에 대 한 클라이언트 Ip의 목록으로 포함 하는 CIDR 형식 toobe hello 집합이 IP 주소 또는 IP 주소 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-122">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="13991-123">IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13991-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="13991-124">자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13991-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="13991-125">`<default-consistency-level>`hello Azure Cosmos DB 계정 hello 기본 일관성 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-125">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="13991-126">자세한 내용은 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13991-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="13991-127">`<max-interval>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 시간 양을 (초)의 부실 허용할 것인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="13991-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="13991-128">값의 허용 범위는 1-100입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="13991-129">`<max-staleness-prefix>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 허용 하는 오래 된 요청 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="13991-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="13991-130">이 값의 허용 범위는 1-2,147,483,647입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="13991-131">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-131">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-132">`<resource-group-location>`hello 위치의 hello Azure 리소스 그룹 toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-132">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-133">`<database-account-name>`hello Azure Cosmos DB 데이터베이스 계정 toobe 생성의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-133">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe created.</span></span> <span data-ttu-id="13991-134">사용할 수 있습니다만 소문자, 숫자, hello '-' 문자, 있으며 3 ~ 50 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-134">It can only use lowercase letters, numbers, hello '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="13991-135">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="13991-136">참고 사항</span><span class="sxs-lookup"><span data-stu-id="13991-136">Notes</span></span>
* <span data-ttu-id="13991-137">hello 앞의 예제 데이터베이스 계정을 만듭니다 두 영역.</span><span class="sxs-lookup"><span data-stu-id="13991-137">hello preceding example creates a database account with two regions.</span></span> <span data-ttu-id="13991-138">가능한 toocreate 하나의 지역 (hello 쓰기 영역으로 지정 하 고 장애 조치 우선 순위 값이 0) 또는 두 개 이상의 영역과 함께 데이터베이스 계정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-138">It is also possible toocreate a database account with either one region (which is designated as hello write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="13991-139">자세한 내용은 [다중 하위 지역 데이터베이스 계정][scaling-globally]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13991-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="13991-140">hello 위치 Azure Cosmos DB는 일반적으로 사용할 수 있는 영역 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-140">hello locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="13991-141">hello hello 현재 지역 목록이 제공 됩니다 [Azure 지역 페이지](https://azure.microsoft.com/regions/#services)합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-141">hello current list of regions is provided on hello [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="13991-142"><a id="update-documentdb-account-powershell"></a> DocumentDB 데이터베이스 계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="13991-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="13991-143">이 명령을 사용 하면 tooupdate Azure Cosmos DB 데이터베이스 계정 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-143">This command allows you tooupdate your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="13991-144">Hello 일관성 정책 및 hello 위치는 hello 데이터베이스 계정이에 있는이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13991-144">This includes hello consistency policy and hello locations which hello database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="13991-145">이 명령은 tooadd 및 제거 하는 영역 사용 하면 하지만 toomodify 장애 조치 우선 순위 수 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-145">This command allows you tooadd and remove regions but does not allow you toomodify failover priorities.</span></span> <span data-ttu-id="13991-146">toomodify 장애 조치 우선 순위 참조 [아래](#modify-failover-priority-powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-146">toomodify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="13991-147">`<write-region-location>`hello의 hello 위치 이름 hello 데이터베이스 계정의 지역을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-147">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="13991-148">이 위치는 필수 toohave 장애 조치 우선 순위 값이 0입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-148">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="13991-149">데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="13991-150">`<read-region-location>`hello 데이터베이스 계정의 지역 대 한 읽기의 hello hello 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-150">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="13991-151">이 위치는 필수 toohave 장애 조치 우선 순위 값이 0 보다 큰 값입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-151">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="13991-152">데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="13991-153">`<default-consistency-level>`hello Azure Cosmos DB 계정 hello 기본 일관성 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-153">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="13991-154">자세한 내용은 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13991-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="13991-155">`<ip-range-filter>`Hello 허용 지정된 데이터베이스 계정에 대 한 클라이언트 Ip의 목록으로 포함 하는 CIDR 형식 toobe hello 집합이 IP 주소 또는 IP 주소 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-155">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="13991-156">IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13991-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="13991-157">자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13991-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="13991-158">`<max-interval>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 시간 양을 (초)의 부실 허용할 것인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="13991-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="13991-159">값의 허용 범위는 1-100입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="13991-160">`<max-staleness-prefix>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 허용 하는 오래 된 요청 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="13991-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="13991-161">이 값의 허용 범위는 1-2,147,483,647입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="13991-162">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-162">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-163">`<resource-group-location>`hello 위치의 hello Azure 리소스 그룹 toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-163">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-164">`<database-account-name>`hello Azure Cosmos DB 데이터베이스 계정 toobe 업데이트의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-164">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe updated.</span></span>

<span data-ttu-id="13991-165">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="13991-166"><a id="delete-documentdb-account-powershell"></a> DocumentDB 데이터베이스 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="13991-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="13991-167">이 명령은 toodelete를 기존 Azure Cosmos DB 데이터베이스 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-167">This command allows you toodelete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="13991-168">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-168">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-169">`<database-account-name>`hello Azure Cosmos DB 데이터베이스 계정 toobe 삭제의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-169">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe deleted.</span></span>

<span data-ttu-id="13991-170">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="13991-171"><a id="get-documentdb-properties-powershell"></a> DocumentDB 데이터베이스 계정 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="13991-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="13991-172">이 명령은 기존 Azure Cosmos DB 데이터베이스 계정의 tooget hello 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-172">This command allows you tooget hello properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="13991-173">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-173">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-174">`<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-174">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="13991-175">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="13991-176"><a id="update-tags-powershell"></a> - Azure Cosmos DB 데이터베이스 계정의 업데이트 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="13991-177">hello 다음 예에서는 설명 방법을 tooset [Azure 리소스 태그] [ azure-resource-tags] 데이터베이스 계정을 Azure Cosmos DB에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-177">hello following example describes how tooset [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="13991-178">이 명령은 hello와 결합할 수 있습니다 만들거나 hello를 추가 하 여 업데이트 명령을 `-Tags` hello 해당 매개 변수를 사용 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-178">This command can be combined with hello create or update commands by appending hello `-Tags` flag with hello corresponding parameter.</span></span>

<span data-ttu-id="13991-179">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="13991-180"><a id="list-account-keys-powershell"></a> 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="13991-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="13991-181">Azure Cosmos DB 계정을 만들 때 hello 서비스는 hello Azure Cosmos DB 계정에 액세스할 때 인증에 사용할 수 있는 두 개의 마스터 액세스 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-181">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="13991-182">두 개의 액세스 키를 제공 함으로써 Azure Cosmos DB 하면 없는 중단 tooyour Azure Cosmos DB 계정 사용 하 여 tooregenerate hello 키.</span><span class="sxs-lookup"><span data-stu-id="13991-182">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> <span data-ttu-id="13991-183">읽기 전용 작업을 인증하기 위한 읽기 전용 키도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="13991-184">두 개의 읽기-쓰기 키(기본 및 보조) 및 두 개의 읽기 전용 키(기본 및 보조)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="13991-185">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-185">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-186">`<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-186">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="13991-187">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="13991-188"><a id="list-connection-strings-powershell"></a> 연결 문자열 나열</span><span class="sxs-lookup"><span data-stu-id="13991-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="13991-189">MongoDB 계정에 대 한 hello 연결 문자열 tooconnect MongoDB 앱 toohello 데이터베이스 계정 hello 다음 명령을 사용 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-189">For MongoDB accounts, hello connection string tooconnect your MongoDB app toohello database account can be retrieved using hello following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="13991-190">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-190">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-191">`<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-191">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="13991-192">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="13991-193"><a id="regenerate-account-key-powershell"></a> 계정 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="13991-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="13991-194">Hello 액세스 키 tooyour Azure Cosmos DB 계정을 변경 해야 주기적으로 toohelp 유지 되며 연결 더 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-194">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="13991-195">두 개의 액세스 키 tooenable 할당 하면 toomaintain 연결 toohello 다시 생성 하는 동안에 한 선택 키를 사용 하 여 Azure Cosmos DB 계정을 hello 다른 선택 키입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-195">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="13991-196">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-196">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-197">`<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-197">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="13991-198">`<key-kind>`Hello 4 유형의 키 중 하나: ["Primary" | " 보조 "|" PrimaryReadonly "|" SecondaryReadonly "] 싶다는 의사를 tooregenerate 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-198">`<key-kind>` One of hello four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like tooregenerate.</span></span>

<span data-ttu-id="13991-199">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="13991-200"><a id="modify-failover-priority-powershell"></a> Azure Cosmos DB 데이터베이스 계정의 장애 조치(Failover) 우선 순위 수정</span><span class="sxs-lookup"><span data-stu-id="13991-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="13991-201">다중 영역 데이터베이스 계정에 대 한 Azure Cosmos DB 데이터베이스 계정 hello는 다양 한 지역에 있는 hello의 hello 장애 조치 우선 순위를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-201">For multi-region database accounts, you can change hello failover priority of hello various regions which hello Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="13991-202">Azure Cosmos DB 데이터베이스 계정의 장애 조치(Failover)에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포][distribute-data-globally]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13991-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="13991-203">`<write-region-location>`hello의 hello 위치 이름 hello 데이터베이스 계정의 지역을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-203">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="13991-204">이 위치는 필수 toohave 장애 조치 우선 순위 값이 0입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-204">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="13991-205">데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="13991-206">`<read-region-location>`hello 데이터베이스 계정의 지역 대 한 읽기의 hello hello 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-206">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="13991-207">이 위치는 필수 toohave 장애 조치 우선 순위 값이 0 보다 큰 값입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-207">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="13991-208">데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="13991-209">`<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13991-209">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="13991-210">`<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="13991-210">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="13991-211">예제:</span><span class="sxs-lookup"><span data-stu-id="13991-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="13991-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13991-212">Next steps</span></span>

* <span data-ttu-id="13991-213">.NET을 사용 하 여 tooconnect 참조 [연결 및 쿼리.net](create-documentdb-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-213">tooconnect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="13991-214">.NET Core를 사용 하 여 tooconnect 참조 [연결 및.NET Core를 사용 하 여 쿼리](create-documentdb-dotnet-core.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-214">tooconnect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="13991-215">Node.js를 사용 하 여 tooconnect 참조 [연결 및 Node.js 및 MongoDB 앱으로 쿼리](create-mongodb-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13991-215">tooconnect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
