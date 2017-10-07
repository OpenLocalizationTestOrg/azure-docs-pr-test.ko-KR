---
title: "aaaAzure 모니터링 REST API 연습 | Microsoft Docs"
description: "Tooauthenticate는 tooand 사용 하 여 hello Azure 모니터링 REST API 요청 하는 방식입니다."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Azure Monitoring REST API 연습
이 문서에서는 어떻게 tooperform 인증 코드 hello를 사용할 수 있도록 [Microsoft Azure REST API 참조 모니터](https://msdn.microsoft.com/library/azure/dn931943.aspx)합니다.         

hello Azure 모니터 API를 사용 하면 가능한 tooprogrammatically 검색 hello 사용 가능한 기본 메트릭 정의 (예: CPU 시간, 요청 등 메트릭의 hello 유형), 세분성, 및 메트릭 값입니다. 검색 되 면 hello 데이터는 Azure SQL 데이터베이스, Azure Cosmos DB 또는 Azure 데이터 레이크 같은 별도 데이터 저장소에 저장할 수 있습니다. 여기에서 필요에 따라 추가적인 분석을 수행할 수 있습니다.

다양 한 메트릭 데이터 요소를 사용할 것 외에도이 문서에서 보여 주듯이, hello 모니터 API 하면 가능한 toolist 경고 규칙, 보기 작업 로그 등에 있습니다. 사용 가능한 작업의 전체 목록을 참조 hello [Microsoft Azure REST API 참조 모니터](https://msdn.microsoft.com/library/azure/dn931943.aspx)합니다.

## <a name="authenticating-azure-monitor-requests"></a>Azure Monitor 요청 인증
hello 첫 번째 단계는 tooauthenticate hello 요청입니다.

모든 hello 작업 hello Azure 모니터 API 사용 하 여 hello Azure 리소스 관리자 인증 모델에 대해 실행 합니다. 따라서 모든 요청은 Azure AD(Azure Active Directory)로 인증되어야 합니다. 한 접근 방식 tooauthenticate hello 클라이언트 응용 프로그램이 toocreate Azure AD 서비스 사용자 이므로 hello (JWT) 인증 토큰을 검색 합니다. hello 다음 예제 스크립트에서는 Azure AD PowerShell 통해 서비스 사용자 만들기 더 자세한 연습에 toohello 문서를 참조 하십시오 [서비스 보안 주체 tooaccess 리소스 toocreate Azure PowerShell을 사용 하 여](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password)합니다. 것도 가능 너무[hello Azure 포털을 통해 서비스 사용자를 만들](../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다.

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

tooquery hello Azure 모니터 API hello 클라이언트 응용 프로그램이 이전에 만든 서비스 보안 주체 tooauthenticate hello를 사용 해야 합니다. 다음 PowerShell 스크립트 예에서는 hello hello를 사용 하는 한 가지 방법은 [Active Directory 인증 라이브러리](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp hello JWT 인증 토큰을 가져옵니다. hello JWT 토큰 요청 toohello Azure 모니터 REST API에에서는 HTTP 권한 부여 매개 변수의 일환으로 전달 됩니다.

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

Hello 인증 설치 단계 완료 되 면 쿼리 hello Azure 모니터 REST API에 대해 실행할 수 있습니다. 다음과 같이 두 가지 유용한 쿼리 가지가 있습니다.

1. 리소스에 대 한 hello 메트릭 정의 나열
2. Hello 메트릭 값 검색

## <a name="retrieve-metric-definitions"></a>메트릭 정의 검색 
> [!NOTE]
> hello Azure 모니터 REST API를 사용 하 여 tooretrieve 메트릭 정의 API 버전 hello 대로 "2016-03-01"을 사용 합니다.
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
Azure 논리 앱의 경우 메트릭 정의 hello 스크린 샷 다음 유사한 toohello 표시:

![Alt "메트릭 정의 응답의 JSON 보기"](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

자세한 내용은 참조 hello [hello Azure 모니터 REST API에서 리소스에 대 한 메트릭 정의 나열](https://msdn.microsoft.com/library/azure/mt743621.aspx) 설명서입니다.

## <a name="retrieve-metric-values"></a>메트릭 값 검색 
Hello 사용 가능한 메트릭 정의 알고 있는 경우 다음 가능한 tooretrieve hello 관련된 메트릭 값이 있습니다. 모든 필터링 요청 (예를 들어 검색 hello '요청' 및 'CpuTime' 메트릭 데이터 요소)에 대 한 hello 메트릭 이름 'value' (하지 'localizedValue' hello)를 사용 합니다. 필터가 지정 된 hello 기본 메트릭을 반환 됩니다.

> [!NOTE]
> API 버전 hello로 "2016-06-01"를 사용 하는 hello Azure 모니터 REST API를 사용 하 여 tooretrieve 메트릭 값 합니다.
>
>

**메서드**: GET

**요청 URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*

예를 들어 1 시간, hello 요청의 시간 세분화 및 시간 범위를 지정 하는 hello에 대 한 tooretrieve hello RunsSucceeded 메트릭 데이터 요소가 다음과 같이 합니다.

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

hello 결과 표시 비슷한 toohello 뒷부분의 예제 스크린 샷:

![Alt "평균 응답 시간 메트릭 값을 나타내는 JSON 응답"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

다음 예제는 hello와 같이 hello 메트릭 정의 이름이 및 집계 유형 toohello 필터 tooretrieve 여러 데이터 또는 집계를 가리킵니다. 추가 됩니다.

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>ARMClient 사용
대체 toousing PowerShell (위와 같이)은 toouse [ARMClient](https://github.com/projectkudu/ARMClient) Windows 컴퓨터에 있습니다. ARMClient은 hello Azure AD 인증 (및 결과 JWT 토큰)를 자동으로 처리합니다. hello 다음 단계 설명 메트릭 데이터를 검색 하기 위한 ARMClient 사용 합니다.

1. [Chocolatey](https://chocolatey.org/) 및 [ARMClient](https://github.com/projectkudu/ARMClient)를 설치합니다.
2. 터미널 창에서 *armclient.exe login*을 입력합니다. Toolog tooAzure에 표시 됩니다.
3. *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*을 입력합니다.
4. *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*을 입력합니다.

!["Hello Azure 모니터링 REST API 사용 하 여 ARMClient toowork" alt](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Hello 리소스 ID를 검색 합니다.
Hello REST API를 사용 하 여 toounderstand hello 사용 가능한 메트릭 정의 세분성, 및 관련된 값을 실제로 수 있습니다. 해당 정보는 hello를 사용 하는 경우에 유용 [Azure 관리 라이브러리](https://msdn.microsoft.com/library/azure/mt417623.aspx)합니다.

코드 앞에 오는 hello에 대 한 hello 리소스 ID toouse가 전체 경로 toohello hello Azure 리소스 합니다. 예를 들어 Azure 웹 앱에 대해 tooquery, hello 리소스 ID 합니다.

*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*

hello 다음 목록은 몇 가지 다양 한 Azure 리소스에 대 한 리소스 ID 형식.

* **IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*
* **탄력적인 SQL 풀** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*
* **SQL Database(v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*
* **Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*
* **VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*
* **VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*
* **Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*

다른 방법 tooretrieving hello 리소스 ID를 Azure 리소스 탐색기, hello Azure 포털 및 hello Azure CLI 또는 PowerShell을 통해 원하는 hello 리소스 보기를 사용 하는 등 있습니다.

### <a name="azure-resource-explorer"></a>Azure 리소스 탐색기
한 가지 유용한 방법은 원하는 리소스용 toofind hello 리소스 ID는 toouse hello [Azure 리소스 탐색기](https://resources.azure.com) 도구입니다. 원하는 toohello 리소스 이동한 다음 hello 다음 스크린 샷에서 같이 표시 된 hello ID를 확인 합니다.

![Alt "Azure Resource Explorer"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure portal
hello Azure 포털에서에서 hello 리소스 ID는 가져올 수도 있습니다. 따라서 toodo toohello 필요한 리소스를 이동 하 고 속성을 선택 합니다. 리소스 ID hello hello 다음 스크린 샷에서 같이 hello 속성 블레이드에 표시 됩니다.

![Alt "리소스 ID에 hello 속성 블레이드 hello Azure 포털에에서 표시 된"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell cmdlet도를 사용 하 여 hello 리소스 ID는 검색할 수 있습니다. 예를 들어 tooobtain hello 리소스 ID는 Azure 웹 앱에 대 한 hello 다음 스크린 샷에서 같이 hello AzureRmWebApp Get cmdlet을 실행 합니다.

![Alt "PowerShell을 통해 구한 리소스 ID”](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Azure CLI
tooretrieve hello hello Azure CLI를 사용 하 여 리소스 ID, hello를 지정 하는 hello 'azure webapp 쇼' 명령을 실행 '-json' hello 스크린 샷 뒤에 표시 된 대로 옵션:

![Alt "PowerShell을 통해 구한 리소스 ID”](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>활동 로그 데이터 검색
메트릭 정 및 관련된 값과 함께 추가 tooworking는 것도 가능 tooretrieve 추가 하려는 insights 관련된 tooAzure 리소스입니다. 예를 들어, 것이 가능한 tooquery [활동 로그](https://msdn.microsoft.com/library/azure/dn931934.aspx) 데이터입니다. hello 다음 샘플에서는 Azure 구독에 대 한 특정 날짜 범위 내에서 hello Azure 모니터 REST API tooquery 활동 로그 데이터를 사용 하 여 수행 합니다.

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>다음 단계
* 검토 hello [모니터링 개요](monitoring-overview.md)합니다.
* 보기 hello [지원 되는 Azure 모니터로 메트릭](monitoring-supported-metrics.md)합니다.
* 검토 hello [Microsoft Azure REST API 참조 모니터](https://msdn.microsoft.com/library/azure/dn931943.aspx)합니다.
* 검토 hello [Azure 관리 라이브러리](https://msdn.microsoft.com/library/azure/mt417623.aspx)합니다.
