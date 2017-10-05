---
title: "Azure Cosmos DB 자동화 - Powershell로 관리 | Microsoft Docs"
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
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="357e8-103">PowerShell을 사용하여 Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="357e8-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="357e8-104">이 문서에서는 Azure Powershell을 사용하여 Azure Cosmos DB 데이터베이스 계정 관리를 자동화하는 명령에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="357e8-105">[다중 하위 지역 데이터베이스 계정][scaling-globally]에서 계정 키 및 장애 조치 우선 순위를 관리하는 명령도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="357e8-106">데이터베이스 계정을 업데이트하면 일관성 정책을 수정하고 하위 지역을 추가/제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="357e8-107">Azure Cosmos DB 계정의 플랫폼 간 관리를 위해 [Azure CLI](cli-samples.md), [리소스 공급자 REST API][rp-rest-api] 또는 [Azure Portal](create-documentdb-dotnet.md#create-account)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="357e8-108">시작하기</span><span class="sxs-lookup"><span data-stu-id="357e8-108">Getting Started</span></span>

<span data-ttu-id="357e8-109">[Azure PowerShell을 설치 및 구성하는 방법][powershell-install-configure]의 지침에 따라 Powershell에서 Azure Resource Manager 계정을 설치하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="357e8-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="357e8-110">Notes</span></span>

* <span data-ttu-id="357e8-111">사용자에게 확인을 요구하지 않고 다음 명령을 실행하려면 명령에 `-Force` 플래그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="357e8-112">다음 명령은 모두 동기식입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="357e8-113"><a id="create-documentdb-account-powershell"></a> Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="357e8-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="357e8-114">이 명령을 사용하면 Azure Cosmos DB 데이터베이스 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="357e8-115">새 데이터베이스 계정을 특정 [일관성 정책](consistency-levels.md)을 사용하여 단일 하위 지역 또는 [다중 하위 지역][scaling-globally]으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="357e8-116">`<write-region-location>` - 데이터베이스 계정의 쓰기 하위 지역의 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="357e8-117">이 위치에는 0인 장애 조치 우선 순위 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="357e8-118">데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="357e8-119">`<read-region-location>` - 데이터베이스 계정의 읽기 하위 지역의 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="357e8-120">이 위치에는 0보다 큰 장애 조치 우선 순위 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="357e8-121">데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="357e8-122">`<ip-range-filter>` 지정된 데이터베이스 계정에 대해 허용된 클라이언트 IP 목록으로 포함할 IP 주소 집합 또는 IP 주소 범위를 CIDR 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="357e8-123">IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="357e8-124">자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="357e8-125">`<default-consistency-level>`Azure Cosmos DB 계정의 기본 일관성 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="357e8-126">자세한 내용은 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="357e8-127">`<max-interval>` - 제한된 부실(Bounded Staleness) 일관성과 함께 사용되는 경우 이 값은 부실 허용 시간(초)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="357e8-128">값의 허용 범위는 1-100입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="357e8-129">`<max-staleness-prefix>` - 제한된 부실 일관성과 함께 사용되는 경우 이 값은 허용된 부실 요청 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="357e8-130">이 값의 허용 범위는 1-2,147,483,647입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="357e8-131">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-132">`<resource-group-location>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 Azure 리소스 그룹의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-133">`<database-account-name>` - 만들어질 Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="357e8-134">소문자, 숫자, '-'(대시) 문자만 사용할 수 있으며, 3-50자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="357e8-135">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="357e8-136">참고 사항</span><span class="sxs-lookup"><span data-stu-id="357e8-136">Notes</span></span>
* <span data-ttu-id="357e8-137">앞의 예제에서는 두 개의 하위 지역이 있는 데이터베이스 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="357e8-138">하나의 하위 지역(쓰기 하위 지역으로 지정되고 장애 조치 우선 순위 값이 0임) 또는 세 개 이상의 하위 지역이 있는 데이터베이스 계정도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="357e8-139">자세한 내용은 [다중 하위 지역 데이터베이스 계정][scaling-globally]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="357e8-140">위치는 Azure Cosmos DB를 일반적으로 사용할 수 있는 하위 지역이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="357e8-141">현재 하위 지역 목록은 [Azure 지역 페이지](https://azure.microsoft.com/regions/#services)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="357e8-142"><a id="update-documentdb-account-powershell"></a> DocumentDB 데이터베이스 계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="357e8-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="357e8-143">이 명령을 사용하면 Azure Cosmos DB 데이터베이스 계정 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="357e8-144">여기에는 일관성 정책과 데이터베이스 계정이 있는 위치가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="357e8-145">이 명령을 사용하면 하위 지역을 추가/제거할 수 있지만 장애 조치 우선 순위는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="357e8-146">장애 조치 우선 순위를 수정하려면 [아래 예제](#modify-failover-priority-powershell)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="357e8-147">`<write-region-location>` - 데이터베이스 계정의 쓰기 하위 지역의 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="357e8-148">이 위치에는 0인 장애 조치 우선 순위 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="357e8-149">데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="357e8-150">`<read-region-location>` - 데이터베이스 계정의 읽기 하위 지역의 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="357e8-151">이 위치에는 0보다 큰 장애 조치 우선 순위 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="357e8-152">데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="357e8-153">`<default-consistency-level>`Azure Cosmos DB 계정의 기본 일관성 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="357e8-154">자세한 내용은 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="357e8-155">`<ip-range-filter>` 지정된 데이터베이스 계정에 대해 허용된 클라이언트 IP 목록으로 포함할 IP 주소 집합 또는 IP 주소 범위를 CIDR 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="357e8-156">IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="357e8-157">자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="357e8-158">`<max-interval>` - 제한된 부실(Bounded Staleness) 일관성과 함께 사용되는 경우 이 값은 부실 허용 시간(초)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="357e8-159">값의 허용 범위는 1-100입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="357e8-160">`<max-staleness-prefix>` - 제한된 부실 일관성과 함께 사용되는 경우 이 값은 허용된 부실 요청 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="357e8-161">이 값의 허용 범위는 1-2,147,483,647입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="357e8-162">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-163">`<resource-group-location>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 Azure 리소스 그룹의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-164">`<database-account-name>` - 업데이트할 Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="357e8-165">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="357e8-166"><a id="delete-documentdb-account-powershell"></a> DocumentDB 데이터베이스 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="357e8-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="357e8-167">이 명령을 사용하면 기존 Azure Cosmos DB 데이터베이스 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="357e8-168">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-169">`<database-account-name>` - 삭제할 Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="357e8-170">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="357e8-171"><a id="get-documentdb-properties-powershell"></a> DocumentDB 데이터베이스 계정 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="357e8-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="357e8-172">이 명령을 사용하면 기존 Azure Cosmos DB 데이터베이스 계정의 속성을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="357e8-173">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-174">`<database-account-name>` - Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="357e8-175">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="357e8-176"><a id="update-tags-powershell"></a> - Azure Cosmos DB 데이터베이스 계정의 업데이트 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="357e8-177">다음 예제에서는 Azure Cosmos DB 데이터베이스 계정에 대해 [Azure 리소스 태그][azure-resource-tags]를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="357e8-178">이 명령은 `-Tags` 플래그에 해당 매개 변수를 추가하여 만들기 또는 업데이트 명령과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="357e8-179">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="357e8-180"><a id="list-account-keys-powershell"></a> 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="357e8-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="357e8-181">Azure Cosmos DB 계정을 만들면 해당 서비스에서 Azure Cosmos DB 계정에 액세스할 때 인증에 사용할 수 있는 2개의 마스터 액세스 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="357e8-182">Azure Cosmos DB에서는 2개의 액세스 키를 제공해서 사용자가 Azure Cosmos DB 계정에 대한 중단 없이 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="357e8-183">읽기 전용 작업을 인증하기 위한 읽기 전용 키도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="357e8-184">두 개의 읽기-쓰기 키(기본 및 보조) 및 두 개의 읽기 전용 키(기본 및 보조)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="357e8-185">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-186">`<database-account-name>` - Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="357e8-187">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="357e8-188"><a id="list-connection-strings-powershell"></a> 연결 문자열 나열</span><span class="sxs-lookup"><span data-stu-id="357e8-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="357e8-189">MongoDB 계정의 경우 MongoDB 앱을 데이터베이스 계정에 연결하기 위한 연결 문자열은 다음 명령을 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="357e8-190">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-191">`<database-account-name>` - Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="357e8-192">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="357e8-193"><a id="regenerate-account-key-powershell"></a> 계정 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="357e8-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="357e8-194">저장소 연결을 더욱 안전하게 유지할 수 있도록 정기적으로 Azure Cosmos DB 계정의 액세스 키를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="357e8-195">두 개의 액세스 키가 할당되므로 액세스 키 하나를 다시 생성하는 동안 다른 액세스 키를 사용하여 Azure Cosmos DB 계정에 대한 연결을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="357e8-196">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-197">`<database-account-name>` - Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="357e8-198">`<key-kind>` - 다시 생성할 네 가지 유형의 키, 즉 ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="357e8-199">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="357e8-200"><a id="modify-failover-priority-powershell"></a> Azure Cosmos DB 데이터베이스 계정의 장애 조치(Failover) 우선 순위 수정</span><span class="sxs-lookup"><span data-stu-id="357e8-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="357e8-201">다중 하위 지역 데이터베이스 계정의 경우 Azure Cosmos DB 데이터베이스 계정이 있는 다양한 하위 지역의 장애 조치(Failover) 우선 순위를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="357e8-202">Azure Cosmos DB 데이터베이스 계정의 장애 조치(Failover)에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포][distribute-data-globally]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="357e8-203">`<write-region-location>` - 데이터베이스 계정의 쓰기 하위 지역의 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="357e8-204">이 위치에는 0인 장애 조치 우선 순위 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="357e8-205">데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="357e8-206">`<read-region-location>` - 데이터베이스 계정의 읽기 하위 지역의 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="357e8-207">이 위치에는 0보다 큰 장애 조치 우선 순위 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="357e8-208">데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="357e8-209">`<resource-group-name>` - 새 Azure Cosmos DB 데이터베이스 계정이 속하는 [Azure 리소스 그룹][azure-resource-groups]의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="357e8-210">`<database-account-name>` - Azure Cosmos DB 데이터베이스 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="357e8-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="357e8-211">예제:</span><span class="sxs-lookup"><span data-stu-id="357e8-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="357e8-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="357e8-212">Next steps</span></span>

* <span data-ttu-id="357e8-213">.NET을 사용하여 연결하려면 [.NET을 사용하여 연결 및 쿼리](create-documentdb-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="357e8-214">.NET Core를 사용하여 연결하려면 [.NET Core를 사용하여 연결 및 쿼리](create-documentdb-dotnet-core.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="357e8-215">Node.js를 사용하여 연결하려면 [Node.js 및 MongoDB 앱을 사용하여 연결 및 쿼리](create-mongodb-nodejs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="357e8-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
