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
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>PowerShell을 사용하여 Azure Cosmos DB 계정 만들기

hello 다음 가이드에서는 설명 Azure Powershell을 사용 하 여 Azure Cosmos DB 데이터베이스 계정 명령 tooautomate 관리. 에 포함 되어 명령 toomanage 계정 키 및 장애 조치 우선 순위에서 [다중 지역 데이터베이스 계정][scaling-globally]합니다. 데이터베이스 계정을 업데이트 하는 사용 하면 toomodify 일관성 정책 및 영역 추가/제거 합니다. Azure Cosmos DB 계정의 플랫폼 간 관리를 위해 사용할 수 있습니다 [Azure CLI](cli-samples.md), hello [리소스 공급자 REST API][rp-rest-api], 또는 hello [Azure 포털](create-documentdb-dotnet.md#create-account)합니다.

## <a name="getting-started"></a>시작하기

Hello 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고] [ powershell-install-configure] tooinstall tooyour Azure 리소스 관리자 로그인 계정에 Powershell 합니다.

### <a name="notes"></a>참고 사항

* Tooexecute hello 사용자에 게 확인 하지 않고도 명령 뒤, 원하는 경우 추가 hello `-Force` toohello 명령 플래그를 지정 합니다.
* 다음 명령은 모든 hello는 동기적입니다.

## <a id="create-documentdb-account-powershell"></a> Azure Cosmos DB 계정 만들기

이 명령은 Azure Cosmos DB 데이터베이스 계정 toocreate가 있습니다. 새 데이터베이스 계정을 특정 [일관성 정책](consistency-levels.md)을 사용하여 단일 하위 지역 또는 [다중 하위 지역][scaling-globally]으로 구성합니다.

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`hello의 hello 위치 이름 hello 데이터베이스 계정의 지역을 작성 합니다. 이 위치는 필수 toohave 장애 조치 우선 순위 값이 0입니다. 데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.
* `<read-region-location>`hello 데이터베이스 계정의 지역 대 한 읽기의 hello hello 위치 이름입니다. 이 위치는 필수 toohave 장애 조치 우선 순위 값이 0 보다 큰 값입니다. 데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.
* `<ip-range-filter>`Hello 허용 지정된 데이터베이스 계정에 대 한 클라이언트 Ip의 목록으로 포함 하는 CIDR 형식 toobe hello 집합이 IP 주소 또는 IP 주소 범위를 지정 합니다. IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다. 자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.
* `<default-consistency-level>`hello Azure Cosmos DB 계정 hello 기본 일관성 수준입니다. 자세한 내용은 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하세요.
* `<max-interval>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 시간 양을 (초)의 부실 허용할 것인지를 나타냅니다. 값의 허용 범위는 1-100입니다.
* `<max-staleness-prefix>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 허용 하는 오래 된 요청 수를 나타냅니다. 이 값의 허용 범위는 1-2,147,483,647입니다.
* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<resource-group-location>`hello 위치의 hello Azure 리소스 그룹 toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello Azure Cosmos DB 데이터베이스 계정 toobe 생성의 hello 이름입니다. 사용할 수 있습니다만 소문자, 숫자, hello '-' 문자, 있으며 3 ~ 50 자 사이 여야 합니다.

예제: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>참고 사항
* hello 앞의 예제 데이터베이스 계정을 만듭니다 두 영역. 가능한 toocreate 하나의 지역 (hello 쓰기 영역으로 지정 하 고 장애 조치 우선 순위 값이 0) 또는 두 개 이상의 영역과 함께 데이터베이스 계정 이기도 합니다. 자세한 내용은 [다중 하위 지역 데이터베이스 계정][scaling-globally]을 참조하세요.
* hello 위치 Azure Cosmos DB는 일반적으로 사용할 수 있는 영역 이어야 합니다. hello hello 현재 지역 목록이 제공 됩니다 [Azure 지역 페이지](https://azure.microsoft.com/regions/#services)합니다.

## <a id="update-documentdb-account-powershell"></a> DocumentDB 데이터베이스 계정 업데이트

이 명령을 사용 하면 tooupdate Azure Cosmos DB 데이터베이스 계정 속성입니다. Hello 일관성 정책 및 hello 위치는 hello 데이터베이스 계정이에 있는이 포함 됩니다.

> [!NOTE]
> 이 명령은 tooadd 및 제거 하는 영역 사용 하면 하지만 toomodify 장애 조치 우선 순위 수 하지 않습니다. toomodify 장애 조치 우선 순위 참조 [아래](#modify-failover-priority-powershell)합니다.

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`hello의 hello 위치 이름 hello 데이터베이스 계정의 지역을 작성 합니다. 이 위치는 필수 toohave 장애 조치 우선 순위 값이 0입니다. 데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.
* `<read-region-location>`hello 데이터베이스 계정의 지역 대 한 읽기의 hello hello 위치 이름입니다. 이 위치는 필수 toohave 장애 조치 우선 순위 값이 0 보다 큰 값입니다. 데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.
* `<default-consistency-level>`hello Azure Cosmos DB 계정 hello 기본 일관성 수준입니다. 자세한 내용은 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하세요.
* `<ip-range-filter>`Hello 허용 지정된 데이터베이스 계정에 대 한 클라이언트 Ip의 목록으로 포함 하는 CIDR 형식 toobe hello 집합이 IP 주소 또는 IP 주소 범위를 지정 합니다. IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다. 자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.
* `<max-interval>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 시간 양을 (초)의 부실 허용할 것인지를 나타냅니다. 값의 허용 범위는 1-100입니다.
* `<max-staleness-prefix>`Bounded Staleness 일관성을 사용 하는 경우이 값 hello 허용 하는 오래 된 요청 수를 나타냅니다. 이 값의 허용 범위는 1-2,147,483,647입니다.
* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<resource-group-location>`hello 위치의 hello Azure 리소스 그룹 toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello Azure Cosmos DB 데이터베이스 계정 toobe 업데이트의 hello 이름입니다.

예제: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> DocumentDB 데이터베이스 계정 삭제

이 명령은 toodelete를 기존 Azure Cosmos DB 데이터베이스 계정이 있습니다.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello Azure Cosmos DB 데이터베이스 계정 toobe 삭제의 hello 이름입니다.

예제:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> DocumentDB 데이터베이스 계정 속성 가져오기

이 명령은 기존 Azure Cosmos DB 데이터베이스 계정의 tooget hello 속성이 있습니다.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.

예제:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> - Azure Cosmos DB 데이터베이스 계정의 업데이트 태그입니다.

hello 다음 예에서는 설명 방법을 tooset [Azure 리소스 태그] [ azure-resource-tags] 데이터베이스 계정을 Azure Cosmos DB에 대 한 합니다.

> [!NOTE]
> 이 명령은 hello와 결합할 수 있습니다 만들거나 hello를 추가 하 여 업데이트 명령을 `-Tags` hello 해당 매개 변수를 사용 하는 플래그입니다.

예제:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> 계정 키 나열

Azure Cosmos DB 계정을 만들 때 hello 서비스는 hello Azure Cosmos DB 계정에 액세스할 때 인증에 사용할 수 있는 두 개의 마스터 액세스 키를 생성 합니다. 두 개의 액세스 키를 제공 함으로써 Azure Cosmos DB 하면 없는 중단 tooyour Azure Cosmos DB 계정 사용 하 여 tooregenerate hello 키. 읽기 전용 작업을 인증하기 위한 읽기 전용 키도 사용할 수 있습니다. 두 개의 읽기-쓰기 키(기본 및 보조) 및 두 개의 읽기 전용 키(기본 및 보조)가 있습니다.

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.

예제:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> 연결 문자열 나열

MongoDB 계정에 대 한 hello 연결 문자열 tooconnect MongoDB 앱 toohello 데이터베이스 계정 hello 다음 명령을 사용 하 여 검색할 수 있습니다.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.

예제:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> 계정 키 다시 생성

Hello 액세스 키 tooyour Azure Cosmos DB 계정을 변경 해야 주기적으로 toohelp 유지 되며 연결 더 안전 합니다. 두 개의 액세스 키 tooenable 할당 하면 toomaintain 연결 toohello 다시 생성 하는 동안에 한 선택 키를 사용 하 여 Azure Cosmos DB 계정을 hello 다른 선택 키입니다.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.
* `<key-kind>`Hello 4 유형의 키 중 하나: ["Primary" | " 보조 "|" PrimaryReadonly "|" SecondaryReadonly "] 싶다는 의사를 tooregenerate 합니다.

예제:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> Azure Cosmos DB 데이터베이스 계정의 장애 조치(Failover) 우선 순위 수정

다중 영역 데이터베이스 계정에 대 한 Azure Cosmos DB 데이터베이스 계정 hello는 다양 한 지역에 있는 hello의 hello 장애 조치 우선 순위를 변경할 수 있습니다. Azure Cosmos DB 데이터베이스 계정의 장애 조치(Failover)에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포][distribute-data-globally]를 참조하세요.

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`hello의 hello 위치 이름 hello 데이터베이스 계정의 지역을 작성 합니다. 이 위치는 필수 toohave 장애 조치 우선 순위 값이 0입니다. 데이터베이스 계정마다 정확히 쓰기 하위 지역 하나만 있어야 합니다.
* `<read-region-location>`hello 데이터베이스 계정의 지역 대 한 읽기의 hello hello 위치 이름입니다. 이 위치는 필수 toohave 장애 조치 우선 순위 값이 0 보다 큰 값입니다. 데이터베이스 계정마다 읽기 하위 지역이 둘 이상 있을 수 있습니다.
* `<resource-group-name>`hello의 hello 이름 [Azure 리소스 그룹] [ azure-resource-groups] toowhich hello 새 Azure Cosmos DB 데이터베이스 계정에 속해 있습니다.
* `<database-account-name>`hello 이름 hello Azure Cosmos DB 데이터베이스 계정입니다.

예제:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>다음 단계

* .NET을 사용 하 여 tooconnect 참조 [연결 및 쿼리.net](create-documentdb-dotnet.md)합니다.
* .NET Core를 사용 하 여 tooconnect 참조 [연결 및.NET Core를 사용 하 여 쿼리](create-documentdb-dotnet-core.md)합니다.
* Node.js를 사용 하 여 tooconnect 참조 [연결 및 Node.js 및 MongoDB 앱으로 쿼리](create-mongodb-nodejs.md)합니다.

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
