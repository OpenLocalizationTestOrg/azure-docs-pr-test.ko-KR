---
title: "응용 프로그램 게이트웨이에 대 한 로그, 성능 로그, 백 엔드 상태 및 메트릭을 aaaMonitor에 액세스 | Microsoft Docs"
description: "자세한 내용은 방법 tooenable에 응용 프로그램 게이트웨이 액세스 로그와 성능 로그 및 관리"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Application Gateway에 대한 백 엔드 상태, 진단 로그 및 메트릭

Azure 응용 프로그램 게이트웨이 사용 하 여 hello 같은 방법으로 다음의 리소스를 모니터링할 수 있습니다.

* [백 엔드 상태](#back-end-health): 응용 프로그램 게이트웨이 백 엔드 풀 hello Azure 포털을 통해 및 PowerShell을 통해 hello에 대 한 hello 서버 hello 기능 toomonitor hello 상태를 제공 합니다. Hello 성능 진단 로그를 통해 hello 백 엔드 풀의 hello 상태를 찾을 수 있습니다.

* [로그](#diagnostic-logs): 액세스, 성능, 로그를 사용 하 고 다른 데이터 toobe 저장 하거나 모니터링을 위해 리소스에서 사용 합니다.

* [메트릭](#metrics) - Application Gateway에는 현재 메트릭이 하나만 있습니다. 이 메트릭은 초당 바이트 수의 응용 프로그램 게이트웨이 hello hello 처리량을 측정합니다.

## <a name="back-end-health"></a>백 엔드 상태

응용 프로그램 게이트웨이 hello 기능 toomonitor hello hello 포털, PowerShell 및 hello CLI (명령줄 인터페이스)를 통해 hello 백 엔드 풀의 개별 멤버의 상태를 제공합니다. 집계 된 상태를 찾을 수도 있습니다 hello 성능 진단 로그를 통해 백 엔드 풀의 요약 합니다. 

hello 백 엔드 상태 보고서의 hello 응용 프로그램 게이트웨이 상태 프로브 toohello 백 엔드 인스턴스 hello 출력에 반영 됩니다. 검색이 성공 하 고 다시 hello 끝 트래픽을 수신할 수 경우 정상인 상태로 간주 됩니다. 그렇지 않으면 비정상 상태로 간주됩니다.

> [!IMPORTANT]
> 응용 프로그램 게이트웨이 서브넷에 NSG ()는 네트워크 보안 그룹이 있는 경우 인바운드 트래픽의 hello 응용 프로그램 게이트웨이 서브넷에 65503 65534 포트 범위를 엽니다. 이러한 포트는 hello 백 엔드 상태 API toowork 필요 합니다.


### <a name="view-back-end-health-through-hello-portal"></a>Hello 포털을 통해 백 엔드 상태 보기

Hello 포털에서 백 엔드 상태는 자동으로 제공 됩니다. 기존 응용 프로그램 게이트웨이에서 **모니터링** > **백 엔드 상태**를 차례로 선택합니다. 

Hello 백 엔드 풀의 각 멤버는 (인지 NIC, IP 또는 FQDN)이이 페이지에 나열 됩니다. 백 엔드 풀 이름, 포트, 백 엔드 HTTP 설정 이름 및 상태도 표시됩니다. 상태의 유효한 값은 **정상**, **비정상** 및 **알 수 없음**입니다.

> [!NOTE]
> 백 엔드의 상태를 표시 하는 경우 **알 수 없는**, 해당 액세스 toohello 백 엔드 NSG 규칙, 사용자 정의 경로 (UDR) 또는 hello 가상 네트워크에 있는 사용자 지정 DNS에 의해 차단 되지 않도록 합니다.

![백 엔드 상태][10]

### <a name="view-back-end-health-through-powershell"></a>PowerShell을 통해 백 엔드 상태 보기

다음 PowerShell 코드 hello tooview 백 엔드 상태를 사용 하 여 hello 하는 방법을 보여 줍니다. `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Azure CLI 2.0을 통해 백 엔드 상태 보기

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>결과

다음 코드 조각 hello hello 응답의 예를 보여 줍니다.

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>진단 로그

Azure toomanage에 서로 다른 유형의 로그를 사용할 수 있으며 응용 프로그램 게이트웨이 문제 해결. 일부이 로그 hello 포털을 통해 액세스할 수 있습니다. 모든 로그는 Azure Blob 저장소에서 추출하고 다양한 도구(예: [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md),Excel 및 Power BI)에서 볼 수 있습니다. Hello 통한 여러 유형의 로그 hello 목록 다음에 대해 자세히 알아볼 수 있습니다.

* **활동 로그**: 사용할 수 있습니다 [Azure 활동 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) (이전의 작업 로그 및 감사 로그) tooview 중인 모든 작업이 tooyour Azure 구독 및 해당 상태를 전송 합니다. 기본적으로 활동 로그 항목을 수집 하 고 hello Azure 포털에서에서 볼 수 있습니다.
* **액세스 로그**:이 로그 tooview 응용 프로그램 게이트웨이 액세스 패턴을 사용 하 고 중요 한 정보, 포함 하 여 hello 호출자의 IP, 요청된 URL, 응답 대기 시간, 반환 코드 및 바이트를 축소 및 분석할 수 있습니다. 액세스 로그는 300초마다 수집됩니다. 이 로그에는 Application Gateway 인스턴스당 하나의 레코드가 포함됩니다. hello instanceId 속성에 의해 hello 응용 프로그램 게이트웨이 인스턴스를 식별할 수 있습니다.
* **성능 로그**:이 로그 tooview 응용 프로그램 게이트웨이 인스턴스가 수행 하는 방법을 사용할 수 있습니다. 이 로그는 인스턴스 단위로 처리된 총 요청 수, 처리량(바이트), 실패한 요청 수, 정상 및 비정상 백 엔드 인스턴스 수 등의 성능 정보를 캡처합니다. 성능 로그는 60초마다 수집됩니다.
* **방화벽 로그**: 감지 하거나 방지 모드의 웹 응용 프로그램 방화벽 hello로 구성 된 응용 프로그램 게이트웨이 통해 로깅되는이 로그 tooview hello 요청을 사용할 수 있습니다.

> [!NOTE]
> 로그는 hello Azure 리소스 관리자 배포 모델에서 배포 된 리소스에만 사용할 수 있습니다. Hello 클래식 배포 모델의 리소스에 대 한 로그를 사용할 수 없습니다. 더 잘 이해 hello 두 모델의를 참조 hello [이해 리소스 관리자 배포 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md) 문서.

로그 저장에는 세 가지 옵션이 있습니다.

* **저장소 계정** - 로그를 장기간 저장하고 필요할 때 검토하는 경우에 가장 적합합니다.
* **이벤트 허브**: (SEIM)의 이벤트 관리 도구 리소스에 tooget 경고 및 이벤트 허브는 기타 보안 정보를 통합 하기 위한 유용한 옵션입니다.
* **Log Analytics** - 일반적으로 응용 프로그램을 실시간 모니터링하거나 추세를 파악하는 데 가장 적합합니다.

### <a name="enable-logging-through-powershell"></a>PowerShell을 통한 로깅 사용

활동 로깅은 모든 Resource Manager 리소스에 대해 사용하도록 설정됩니다. 액세스 및 이러한 로그를 통해 사용할 수 있는 hello 데이터 수집 성능 로깅 toostart 사용 하도록 설정 해야 합니다. tooenable 로깅에 사용 하 여 hello 단계를 수행 합니다.

1. Note hello 로그 데이터가 저장 되는 저장소 계정의 리소스 ID입니다. 이 값은 hello 폼의: /subscriptions/\<subscriptionId\>/resourceGroups/\<리소스 그룹 이름은\>/providers/Microsoft.Storage/storageAccounts/\<저장소계정이름\>. 구독의 모든 저장소 계정을 사용할 수 있습니다. Azure 포털 toofind hello이이 정보를 사용할 수 있습니다.

    ![포털: 저장소 계정의 리소스 ID](./media/application-gateway-diagnostics/diagnostics1.png)

2. 로깅을 사용할 Application Gateway의 리소스 ID를 적어 둡니다. 이 값은 hello 폼의: /subscriptions/\<subscriptionId\>/resourceGroups/\<리소스 그룹 이름은\>/providers/Microsoft.Network/applicationGateways/\<응용 프로그램 게이트웨이 이름\>합니다. Hello 포털 toofind이이 정보를 사용할 수 있습니다.

    ![포털: 응용 프로그램 게이트웨이의 리소스 ID](./media/application-gateway-diagnostics/diagnostics2.png)

3. Hello 다음 PowerShell cmdlet을 사용 하 여 진단 로깅 사용:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>활동 로그에는 별도의 저장소 계정이 필요하지 않습니다. 저장소 액세스 및 성능 로깅에 대 한 hello 사용할 서비스 요금이 부과 됩니다.

### <a name="enable-logging-through-hello-azure-portal"></a>Azure 포털을 통해 hello 로깅을 사용 하도록 설정

1. 에 Azure 포털 hello, 리소스를 찾 및 클릭 **진단 로그**합니다.

   Application Gateway의 경우 다음 세 가지 로그를 사용할 수 있습니다.

   * 액세스 로그
   * 성능 로그
   * 방화벽 로그

2. 데이터를 수집 하는 toostart 클릭 **진단을 설정**합니다.

   ![진단 켜기][1]

3. hello **진단 설정을** 블레이드는 hello 설정을 hello에 대 한 진단 로그를 제공 합니다. 이 예제에서는 로그 분석 hello 로그를 저장합니다. 클릭 **구성** 아래 **로그 분석** tooconfigure 작업 영역입니다. 이벤트 허브 및는 저장소 계정 toosave hello 진단 로그를 사용할 수도 있습니다.

   ![Hello 구성 프로세스를 시작합니다.][2]

4. 기존 OMS(Operations Management Suite) 작업 영역을 선택하거나 새 작업 영역을 만듭니다. 이 예제에서는 기존 작업 영역을 사용합니다.

   ![OMS 작업 영역에 대한 옵션][3]

5. Hello 설정을 확인 하 고 클릭 **저장**합니다.

   ![선택 항목이 있는 진단 설정 블레이드][4]

### <a name="activity-log"></a>활동 로그

Azure는 기본적으로 hello 활동 로그를 생성합니다. hello 로그 hello 이벤트 로그를 Azure 저장소에서 90 일 동안 유지 됩니다. 에 대 한 자세한이 로그 hello 읽어 [이벤트 및 활동 로그 보기](../monitoring-and-diagnostics/insights-debugging-with-events.md) 문서.

### <a name="access-log"></a>액세스 로그

각 응용 프로그램 게이트웨이 인스턴스에서 hello 이전 단계에에서 설명 된 대로 활성화 한 경우에 hello 액세스 로그가 생성 됩니다. hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다. 각 응용 프로그램 게이트웨이 액세스 hello 다음 예제에에서 나와 있는 것 처럼 JSON 형식으로 기록 됩니다.


|값  |설명  |
|---------|---------|
|instanceId     | 응용 프로그램 게이트웨이 인스턴스는 서비스 제공된 하는 hello 요청입니다.        |
|clientIP     | Hello 요청에 대 한 원래 IP입니다.        |
|clientPort     | Hello 요청에 대 한 포트를 시작 합니다.       |
|httpMethod     | Hello 요청에 의해 사용 되는 HTTP 메서드.       |
|requestUri     | Hello의 URI는 요청을 받았습니다.        |
|RequestQuery     | **서버 라우팅됩니다**: hello 요청 보낸 백 엔드 풀 인스턴스. </br> **AzureApplicationGateway 로그 ID X**: hello 요청에 사용 되는 상관 관계 ID. Hello 백 엔드 서버에 사용 되는 tootroubleshoot 트래픽 문제 수 있습니다. </br>**서버 상태**: 응용 프로그램 게이트웨이 백 엔드 hello에서에서 받은 HTTP 응답 코드입니다.       |
|UserAgent     | Hello HTTP 요청 헤더에서 사용자 에이전트입니다.        |
|httpStatus     | HTTP 상태 코드는 응용 프로그램 게이트웨이에서 toohello 클라이언트를 반환 합니다.       |
|httpVersion     | Hello 요청의 HTTP 버전입니다.        |
|receivedBytes     | 받은 패킷의 크기(바이트)        |
|sentBytes| 보낸 패킷의 크기(바이트)|
|timeTaken| 처리 요청 toobe 및 해당 응답 toobe 전송 하는 데 걸리는 시간 (밀리초)의 길이입니다. 이 응용 프로그램 게이트웨이 hello 응답 송신 작업이 완료 되는 HTTP 요청 toohello 시간의 hello 첫 번째 바이트를 수신 하는 경우 hello 시간부터 hello 간격으로 계산 됩니다. 일반적으로 필드 Time-taken hello toonote hello 요청 및 응답 패킷을 hello 네트워크를 통해 이동 하는 hello 시간을 포함 합니다. |
|sslEnabled| 통신 toohello 백 엔드 풀 SSL 사용 여부. 유효한 값은 on과 off입니다.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>성능 로그

hello 성능 로그가 hello 이전 단계에에서 설명 된 대로 각 응용 프로그램 게이트웨이 인스턴스에서 사용 하는 경우에 생성 됩니다. hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다. hello 성능 로그 데이터는 1 분 간격으로 생성 됩니다. hello 같은 데이터가 기록 됩니다.


|값  |설명  |
|---------|---------|
|instanceId     |  성능 데이터가 생성되는 Application Gateway 인스턴스입니다. 다중 인스턴스 응용 프로그램 게이트웨이의 경우 인스턴스마다 하나의 행이 있습니다.        |
|healthyHostCount     | Hello 백 엔드 풀에서 정상 호스트의 수입니다.        |
|unHealthyHostCount     | Hello 백 엔드 풀에서 비정상 호스트의 수입니다.        |
|requestCount     | 처리된 요청 수        |
|latency | 대기 시간 (밀리초) hello 인스턴스 toohello에서 보낸 요청의 백 엔드 hello 요청을 수용 하는 합니다. |
|failedRequestCount| 실패한 요청 수|
|throughput| 바이트 수 / 초 단위로 측정 된 hello 마지막 로그 이후 평균 처리량입니다.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Hello HTTP 요청의 첫 번째 바이트 hello hello HTTP 응답의 마지막 바이트 hello 전송 된 때 받은 toohello 시간은 언제 인가요 hello 시간에서 대기 시간이 계산 됩니다. hello 총 hello 응용 프로그램 게이트웨이 처리 시간 및 hello 네트워크 비용 toohello 다시 종료, 백 엔드는 tooprocess hello 요청 hello hello 시간 plus입니다.

### <a name="firewall-log"></a>방화벽 로그

방화벽 로그 hello hello 이전 단계에에서 설명 된 대로 각 응용 프로그램 게이트웨이를 사용 하는 경우에 생성 됩니다. 이 로그는 hello 웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이에 구성 되어 있어야 합니다. hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다. hello 같은 데이터가 기록 됩니다.


|값  |설명  |
|---------|---------|
|instanceId     | 방화벽 데이터가 생성되는 Application Gateway 인스턴스입니다. 다중 인스턴스 응용 프로그램 게이트웨이의 경우 인스턴스마다 하나의 행이 있습니다.         |
|clientIp     |   Hello 요청에 대 한 원래 IP입니다.      |
|clientPort     |  Hello 요청에 대 한 포트를 시작 합니다.       |
|requestUri     | Hello의 URL 요청을 받았습니다.       |
|ruleSetType     | 규칙 집합 유형이며, hello 사용 가능한 값은 OWASP입니다.        |
|ruleSetVersion     | 사용된 규칙 집합 버전이며, 사용 가능한 값은 2.2.9 및 3.0입니다.     |
|ruleId     | 이벤트를 트리거하는 hello의 규칙 ID입니다.        |
|Message     | 이벤트를 트리거하는 hello에 대 한 친숙 한 메시지입니다. 자세한 내용은 hello 세부 정보 섹션에서 제공 됩니다.        |
|action     |  Hello 요청에서 수행한 작업입니다. 사용할 수 있는 값은 Blocked 및 Allowed입니다.      |
|site     | 사이트는 hello에 대 한 로그를 생성 합니다. 현재 규칙이 전역이므로 Global만 나열됩니다.|
|세부 정보     | 이벤트를 트리거하는 hello의 세부 정보입니다.        |
|details.message     | Hello 규칙의 설명입니다.        |
|details.data     | 특정 데이터는 일치 하는 hello 규칙을 요청에 있습니다.         |
|details.file     | Hello 규칙을 포함 하는 구성 파일입니다.        |
|details.line     | Hello 이벤트를 트리거한 hello 구성 파일에 줄 번호입니다.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>보기 및 분석 hello 활동 로그

볼 수 있고 hello 메서드를 다음 중 하나를 사용 하 여 활동 로그 데이터를 분석할 수 없습니다.

* **Azure tools**: hello Azure 포털 또는 Azure PowerShell을 hello Azure CLI, hello Azure REST API를 통해 hello 활동 로그에서 정보를 검색 합니다. 각 방법에 대 한 단계별 지침 hello에 자세히 설명 되어 [활동 작업 리소스 관리자와](../azure-resource-manager/resource-group-audit.md) 문서.
* **Power BI** - [Power BI](https://powerbi.microsoft.com/pricing) 계정이 아직 없는 경우 무료로 사용해볼 수 있습니다. Hello를 사용 하 여 [Azure 활동 로그 콘텐츠 팩 Power BI에 대 한](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), 하거나 사용자 지정할 방법으로 사용할 수 있는 미리 구성 된 대시보드를 사용 하 여 데이터를 분석할 수 있습니다.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>보기 및 분석 hello 액세스, 성능 및 방화벽 로그

Azure [로그 분석](../log-analytics/log-analytics-azure-networking-analytics.md) Blob 저장소 계정에서 hello 카운터 및 이벤트 로그 파일을 수집할 수 있습니다. 포함 시각화 및 강력한 검색 기능 tooanalyze 로그 합니다.

Tooyour 저장소 계정을 연결 하 고 액세스 및 성능 로그에 대 한 hello JSON 로그 항목을 검색할 수도 있습니다. Hello JSON 파일을 다운로드 한 후 tooCSV 변환 하 고 Excel, Power BI 또는 다른 데이터 시각화 도구에서 볼 수 있습니다.

> [!TIP]
> Visual Studio 및 C#의 변수 및 상수에 대 한 값 변경의 기본 개념에 잘 알고 있다면 hello를 사용할 수 있습니다 [변환기 도구 로그](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub에서 사용할 수 있습니다.
> 
> 

## <a name="metrics"></a>메트릭

메트릭은 hello 포털에서 성능 카운터를 볼 수 있는 특정 Azure 리소스에 대 한 기능입니다. Application Gateway의 경우 현재 메트릭 하나만 사용할 수 있습니다. 이 메트릭은 처리량, 이며 hello 포털에서 볼 수 있습니다. Tooan 응용 프로그램 게이트웨이 찾아 클릭 **메트릭**합니다. tooview hello 값, 선택 hello 처리량 **사용 가능한 메트릭** 섹션. 다음 이미지는 hello, 다른 시간 범위에서 toodisplay hello 데이터를 사용할 수 있는 hello 필터 인 예제를 볼 수 있습니다.

![필터가 있는 메트릭 보기][5]

toosee 메트릭, 현재 목록을 참조 [지원 되는 Azure 모니터로 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)합니다.

### <a name="alert-rules"></a>경고 규칙

리소스에 대한 메트릭을 기반으로 하는 경고 규칙을 시작할 수 있습니다. 예를 들어 경고는 webhook을 호출 하거나 hello 응용 프로그램 게이트웨이의 hello 처리량 위, 아래 또는 임계값에 대 한 경우 지정된 된 기간 동안 관리자가 전자 메일로 보낼 수 있습니다.

다음 예제는 hello 임계값 a 처리량 위반 후 tooan 관리자 전자 메일을 보내는 경고 규칙을 만드는 과정을 설명 합니다.

1. 클릭 **추가 메트릭 경고** tooopen hello **규칙 추가** 블레이드입니다. 이 블레이드 hello 메트릭 블레이드에서 에서도 볼 수 있습니다.

   !["메트릭 경고 추가" 단추][6]

2. Hello에 **규칙 추가** 블레이드에서 hello 이름, 조건, 작성 및 섹션을 알리고 클릭 **확인**합니다.

   * Hello에 **조건** 선택기, 4 hello 값 중 하나를 선택: **보다 큰**, **보다 크거나 같은**, **미만**, 또는  **보다 작거나**합니다.

   * Hello에 **기간** 선택기에 선택 5에서 기간 too6 시간을 분입니다.

   * 선택 하는 경우 **소유자, 참가자 및 독자를 전자 메일로 보내기**, hello 전자 메일 수 동적 toothat 리소스 액세스 권한이 있는 hello 사용자를 기반으로 합니다. Hello에 있는 사용자의 쉼표로 구분 된 목록을 제공할 수는 그렇지 않은 경우 **추가 관리자 email(s)** 상자입니다.

   ![규칙 추가 블레이드][7]

Hello 임계값 위반 되 면 다음 이미지는 hello에 비슷한 toohello 하나는 전자 메일 도착 하면:

![위반된 임계값에 대한 전자 메일][8]

메트릭 경고를 만들면 경고 목록이 표시됩니다. 모든 hello 경고 규칙에 대 한 개요를 제공합니다.

![경고 및 규칙 목록][9]

경고 알림에 대해 더 toolearn 참조 [경고 알림의 받을](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.

webhook 및 경고에를 사용 하는 방법에 대해 자세히 toounderstand 방문 [Azure 메트릭 경고에는 webhook 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다.

## <a name="next-steps"></a>다음 단계

* [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)를 사용하여 카운터 및 이벤트 로그 시각화
* [Power BI를 사용하여 Azure 활동 로그 시각화](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 블로그 게시물
* [Power BI 등에서 Azure 활동 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 블로그 게시물

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
