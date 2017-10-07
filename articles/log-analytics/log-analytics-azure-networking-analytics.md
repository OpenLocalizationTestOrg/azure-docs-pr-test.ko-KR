---
title: "로그 분석에서 네트워킹 분석 솔루션 aaaAzure | Microsoft Docs"
description: "Hello 로그 분석 tooreview Azure 네트워크 보안 그룹 로그 및 Azure 응용 프로그램 게이트웨이 로그에서 Azure 네트워킹 분석 솔루션을 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Log Analytics의 Azure 네트워킹 모니터링 솔루션

로그 분석은 hello 다음 실제 네트워크 모니터링을 위해 솔루션을 제공 합니다.
* NPM(네트워크 성능 모니터)
 * 네트워크의 hello 상태 모니터
* Azure 응용 프로그램 게이트웨이 분석 tooreview
 * Azure Application Gateway 로그
 * Azure Application Gateway 메트릭
* Azure 네트워크 보안 그룹 분석 tooreview
 * Azure 네트워크 보안 그룹 로그

## <a name="network-performance-monitor-npm"></a>NPM(네트워크 성능 모니터)

hello [네트워크 성능 모니터](log-analytics-network-performance-monitor.md) 관리 솔루션은 모니터링 솔루션 hello 상태, 가용성 및 네트워크 연결 가능성을 모니터링 하는 네트워크입니다.  간의 toomonitor 사용 되는 연결입니다.

* 공용 클라우드 및 온-프레미스
* 데이터 센터 및 사용자 위치(지점)
* 다중 계층 응용 프로그램의 다양한 계층을 호스팅하는 서브넷

자세한 내용은 [네트워크 성능 모니터](log-analytics-network-performance-monitor.md)를 참조하세요.

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure Application Gateway 및 네트워크 보안 그룹 분석
toouse hello 솔루션:
1. Hello 관리 솔루션 tooLog 분석을 추가 하 고
2. 진단 toodirect hello 진단 tooa 로그 분석 작업 영역을 사용 하도록 설정 합니다. 필요한 toowrite hello 로그 tooAzure Blob 저장소는 없습니다.

하나 또는 둘 다 응용 프로그램 게이트웨이 및 네트워크 보안 그룹에 대 한 진단 및 hello 해당 솔루션을 사용할 수 있습니다.

특정 리소스 종류에 대 한 진단 로깅을 사용 하지 않는 hello 솔루션을 설치, 해당 리소스에 대 한 hello 대시보드 블레이드 비어 있는 하 고 오류 메시지를 표시 합니다.

> [!NOTE]
> 2017 년 1 월 hello 분석 변경 하는 응용 프로그램 게이트웨이 및 네트워크 보안 그룹 tooLog에서 로그를 보내는 방식으로 지원 합니다. Hello 표시 되 면 **Azure 네트워킹 분석 (사용 되지 않음)** 솔루션을 너무 참조[hello 이전 네트워킹 분석 솔루션에서 마이그레이션](#migrating-from-the-old-networking-analytics-solution) toofollow 단계에 대 한 필요 합니다.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Azure 네트워킹 데이터 수집 세부 정보 검토
hello Azure 응용 프로그램 게이트웨이 분석 및 네트워크 보안 그룹을 분석 관리 솔루션 hello Azure 응용 프로그램 게이트웨이 및 네트워크 보안 그룹에서 직접 진단 로그를 수집합니다. 필요한 toowrite hello 로그 tooAzure Blob 저장소 않습니다 되며 에이전트가 없습니다. 데이터 수집을 위해 필요 합니다.

hello 다음 표에 Azure 응용 프로그램 게이트웨이 분석 워크 로드와 hello 네트워크 보안 그룹을 분석에 대 한 데이터 수집 방법에 대 한 기타 세부 정보 및 데이터 수집 방법과 있습니다.

| 플랫폼 | 직접 에이전트 | Systems Center Operations Manager 에이전트 | Azure | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |기록될 때 |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Log Analytics의 Azure Application Gateway 분석 솔루션

![Azure Application Gateway 분석 기호](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

응용 프로그램 게이트웨이 로그 다음 hello 지원 됩니다.

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

응용 프로그램 게이트웨이 hello 다음 메트릭을 지원 됩니다.

* 5분 처리량

### <a name="install-and-configure-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 지침 tooinstall hello를 사용 하 고 hello Azure 응용 프로그램 게이트웨이 분석 솔루션을 구성 합니다.

1. Hello 분석 솔루션에서 Azure 응용 프로그램 게이트웨이 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. Hello에 대 한 진단 로깅 사용 [응용 프로그램 게이트웨이](../application-gateway/application-gateway-diagnostics.md) toomonitor 원하는 합니다.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Hello 포털에서 Azure 응용 프로그램 게이트웨이 진단을 사용 하도록 설정

1. Hello Azure 포털에서에서 응용 프로그램 게이트웨이 리소스 toomonitor toohello 이동
2. 선택 *진단 로그* tooopen hello 다음 페이지

   ![Azure Application Gateway 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. 클릭 *진단을 설정* tooopen hello 다음 페이지

   ![Azure Application Gateway 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. 진단, tooturn 클릭 *에* 아래 *상태*
5. 에 대 한 hello 확인란 클릭 *tooLog 분석 보내기*
6. 기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.
7. Hello 확인란 아래에서 클릭 하 여 **로그** 각 로그 형식 toocollect hello에 대 한
8. 클릭 *저장* 진단 tooLog 분석의 tooenable hello 로깅

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>PowerShell을 사용하여 Azure 네트워크 진단 사용 설정

PowerShell 스크립트 뒤 hello 방법의 예를 제공 합니다. 응용 프로그램 게이트웨이에 대 한 진단 로깅을 tooenable 합니다.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Azure Application Gateway 분석 사용
![Azure Application Gateway 분석 타일 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Hello를 클릭 한 후 **Azure 응용 프로그램 게이트웨이 분석** 타일 개요 hello에 요약의 로그를 확인 하 고 다음 드릴 수 hello 다음 범주에 대 한 toodetails에서:

* Application Gateway 액세스 로그
  * Application Gateway 액세스 로그에 대한 클라이언트 및 서버 오류
  * 각 Application Gateway의 시간당 요청
  * 각 Application Gateway의 시간당 실패한 요청
  * Application Gateway에 대한 사용자 에이전트별 오류
* Application Gateway 성능 
  * Application Gateway에 대한 호스트 상태
  * Application Gateway 실패한 요청에 대해 최대값 및 95번째 백분위수

![Azure Application Gateway 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure Application Gateway 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

Hello에 **Azure 응용 프로그램 게이트웨이 분석** 대시보드를 hello hello 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello 로그 검색 페이지에 대 한 정보를 자세히 설명 합니다.

Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다. 패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Log Analytics의 Azure 네트워크 보안 그룹 분석 솔루션

![Azure 네트워크 보안 그룹 분석 기호](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

다음 로그 hello 네트워크 보안 그룹에 대해 지원 됩니다.

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 지침 tooinstall hello를 사용 하 여 하 고 hello Azure 네트워킹 분석 솔루션을 구성 합니다.

1. Hello 분석 솔루션에서 Azure 네트워크 보안 그룹을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. Hello에 대 한 진단 로깅 사용 [네트워크 보안 그룹](../virtual-network/virtual-network-nsg-manage-log.md) toomonitor 원하는 리소스입니다.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Hello 포털에서 Azure 네트워크 보안 그룹 진단 사용

1. Hello Azure 포털에서에서 네트워크 보안 그룹 리소스 toomonitor toohello 이동
2. 선택 *진단 로그* tooopen hello 다음 페이지

   ![Azure 네트워크 보안 그룹 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. 클릭 *진단을 설정* tooopen hello 다음 페이지

   ![Azure 네트워크 보안 그룹 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. 진단, tooturn 클릭 *에* 아래 *상태*
5. 에 대 한 hello 확인란 클릭 *tooLog 분석 보내기*
6. 기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.
7. Hello 확인란 아래에서 클릭 하 여 **로그** 각 로그 형식 toocollect hello에 대 한
8. 클릭 *저장* 진단 tooLog 분석의 tooenable hello 로깅

### <a name="enable-azure-network-diagnostics-using-powershell"></a>PowerShell을 사용하여 Azure 네트워크 진단 사용 설정

방법의 예를 제공 하는 PowerShell 스크립트 뒤 hello tooenable 네트워크 보안 그룹에 진단 로깅
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Azure 네트워크 보안 그룹 분석 사용
Hello를 클릭 한 후 **Azure 네트워크 보안 그룹 분석** 타일 개요 hello에 요약의 로그를 확인 하 고 다음 드릴 수 hello 다음 범주에 대 한 toodetails에서:

* 네트워크 보안 그룹 차단 흐름
  * 차단된 흐름이 있는 네트워크 보안 그룹 규칙
  * 차단된 흐름이 있는 MAC 주소 
* 네트워크 보안 그룹 허용 흐름
  * 허용된 흐름이 있는 네트워크 보안 그룹 규칙
  * 허용된 흐름이 있는 MAC 주소 

![Azure 네트워크 보안 그룹 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure 네트워크 보안 그룹 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

Hello에 **Azure 네트워크 보안 그룹을 분석** 대시보드를 hello hello 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello 로그 검색 페이지에 대 한 정보를 자세히 설명 합니다.

Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다. 패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Hello 이전 네트워킹 분석 솔루션에서 마이그레이션
2017 년 1 월 hello 분석 변경 하는 Azure 응용 프로그램 게이트웨이 및 Azure 네트워크 보안 그룹 tooLog에서 로그를 보내는 방식으로 지원 합니다. 이러한 변경 내용은 다음 장점 hello를 제공 합니다.
+ 직접 hello 없이 tooLog 분석 필요 toouse 저장소 계정 로그가 기록
+ 로그가 hello 시간에서 대기 시간이 짧습니다 생성 toothem 로그 분석에 사용할 수 있습니다.
+ 구성 단계 감소
+ 모든 유형의 Azure 진단을 위한 공통 형식

toouse hello 솔루션을 업데이트 했습니다.

1. [Azure 응용 프로그램 게이트웨이에서 tooLog 분석을 직접 전송 하는 진단 toobe 구성](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [진단 toobe Azure 네트워크 보안 그룹의 직접 tooLog 분석 전송 구성](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Hello를 사용 하도록 설정 *Azure 응용 프로그램 게이트웨이 분석* 및 hello *Azure 네트워크 보안 그룹 분석* hello 프로세스를 사용 하 여 솔루션에 설명 된 [의 추가 로그 분석 솔루션 hello 솔루션 갤러리](log-analytics-add-solutions.md)
3. 모든 저장 된 쿼리, 대시보드, 또는 경고 toouse hello 새 데이터 형식 업데이트
  + 형식은 tooAzureDiagnostics 합니다. Hello ResourceType toofilter tooAzure 네트워킹 로그를 사용할 수 있습니다.

    | 다음 위치 대신 | 사용: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + 접미사가 있는 모든 필드에 대 한 \_s, \_d, 또는 \_g hello 이름 hello 첫 번째 문자 toolower 대/소문자 변경
   + 접미사가 있는 모든 필드에 대 한 \_o hello 데이터 이름에는 중첩 된 hello 필드 이름을 기반으로 하는 개별 필드도 나누어집니다.
4. Hello 제거 *Azure 네트워킹 분석 (사용 되지 않음)* 솔루션입니다.
  + PowerShell을 사용하는 경우 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`를 사용합니다.

데이터는 수집 전에 hello 변경이 hello 새 솔루션에 표시 되지 않습니다. 기존 형식 및 필드 이름을 hello 사용 하 여이 데이터에 대 한 tooquery를 계속할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview Azure 진단 데이터를 자세히 설명 합니다.
