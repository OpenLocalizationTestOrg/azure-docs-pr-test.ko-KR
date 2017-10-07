---
title: "로그 분석에서 주요 자격 증명 모음 솔루션 aaaAzure | Microsoft Docs"
description: "로그 분석 tooreview Azure 키 자격 증명 모음 로그에서 hello Azure 키 자격 증명 모음 솔루션을 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Log Analytics의 Azure Key Vault Analytics 솔루션

![Key Vault 기호](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

로그 분석 tooreview Azure 키 자격 증명 모음 AuditEvent 로그에서 hello Azure 키 자격 증명 모음 솔루션을 사용할 수 있습니다.

toouse hello 솔루션을 직접 hello 진단 tooa 로그 분석 작업 영역 및 Azure 키 자격 증명 모음 진단 tooenable 로깅이 필요합니다. 필요한 toowrite hello 로그 tooAzure Blob 저장소는 없습니다.

> [!NOTE]
> 2017 년 1 월 hello 분석 변경 하는 주요 자격 증명 모음 tooLog에서 로그를 보내는 방식으로 지원 합니다. Hello 키 자격 증명 모음 솔루션 사용 하는 경우 표시 *(사용 되지 않음)* hello 제목에 참조 너무[hello 이전 키 자격 증명 모음 솔루션에서 마이그레이션](#migrating-from-the-old-key-vault-solution) toofollow 필요한 단계에 대 한 합니다.
>
>

## <a name="install-and-configure-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 지침 tooinstall hello를 사용 하 여 하 고 hello Azure 키 자격 증명 모음 솔루션을 구성 합니다.

1. 솔루션을 hello Azure 키 자격 증명 모음을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. 키 자격 증명 모음 리소스 toomonitor hello에 대 한 로깅, 어느 hello를 사용 하 여 진단을 사용 하도록 설정 [포털](#enable-key-vault-diagnostics-in-the-portal) 또는 [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Hello 포털에서 주요 자격 증명 모음 진단을 사용 하도록 설정

1. Hello Azure 포털에서에서 toohello 주요 자격 증명 모음 리소스 toomonitor 이동
2. 선택 *진단 로그* tooopen hello 다음 페이지

   ![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. 클릭 *진단을 설정* tooopen hello 다음 페이지

   ![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. 진단, tooturn 클릭 *에* 아래 *상태*
5. 에 대 한 hello 확인란 클릭 *tooLog 분석 보내기*
6. 기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.
7. tooenable *AuditEvent* 로그 hello 확인란을 클릭 하 여 로그에서
8. 클릭 *저장* 진단 tooLog 분석의 tooenable hello 로깅

### <a name="enable-key-vault-diagnostics-using-powershell"></a>PowerShell을 사용하여 Key Vault 진단 사용 설정
방법의 예를 제공 하는 PowerShell 스크립트 뒤 hello toouse `Set-AzureRmDiagnosticSetting` tooenable 주요 자격 증명 모음에 진단 로깅:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Azure Key Vault 데이터 수집 상세 정보를 검토합니다.
Azure 키 자격 증명 모음 솔루션 hello 주요 자격 증명 모음에서 직접 진단 로그를 수집합니다.
필요한 toowrite hello 로그 tooAzure Blob 저장소 않습니다 되며 에이전트가 없습니다. 데이터 수집을 위해 필요 합니다.

hello 다음 표에 Azure 키 자격 증명 모음에 대 한 데이터 수집 방법에 대 한 기타 세부 정보 및 데이터 수집 방법과 있습니다.

| 플랫폼 | 직접 에이전트 | Systems Center Operations Manager 에이전트 | Azure | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | 도착 시 |

## <a name="use-azure-key-vault"></a>Azure Key Vault 사용
후 [hello 솔루션 설치](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), hello를 클릭 하 여 hello 주요 자격 증명 모음 데이터를 볼 **Azure 키 자격 증명 모음** hello에서 타일 **개요** 로그 분석의 페이지입니다.

![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Hello를 클릭 한 후 **개요** 타일 toodetails hello 다음 범주에 대 한에서 로그와 다음 드릴의 요약을 볼 수 있습니다.

* 시간 경과에 따른 모든 Key Vault 작업 크기
* 시간 경과에 따른 실패 작업
* 작업별 평균 작업 대기 시간
* 1000 밀리초 이상 하는 작업의 목록과 hello 수가 1000 밀리초 이상 하는 작업을 사용 하 여 작업에 대 한 서비스 품질

![Azure Key Vault 대시보드 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure Key Vault 대시보드 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>모든 작업에 대 한 tooview 세부 정보
1. Hello에 **개요** 페이지에서 hello **Azure 키 자격 증명 모음** 바둑판식으로 배열입니다.
2. Hello에 **Azure 키 자격 증명 모음** 대시보드를 hello hello 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello 로그 검색 페이지의 항목에 대 한 정보를 자세히 설명 합니다.

    Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다. 패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.

## <a name="log-analytics-records"></a>Log Analytics 레코드
형식을 갖는 레코드를 분석 하는 hello Azure 키 자격 증명 모음 솔루션 **KeyVaults** 에서 수집한 [AuditEvent 로그](../key-vault/key-vault-logging.md) Azure 진단에서 합니다.  이러한 레코드에 대 한 속성은 다음 표에 hello에:  

| 속성 | 설명 |
|:--- |:--- |
| 형식 |*AzureDiagnostics* |
| SourceSystem |*Azure* |
| callerIpAddress |Hello 요청을 수행한 hello 클라이언트의 IP 주소 |
| Category | *AuditEvent* |
| CorrelationId |클라이언트 hello 선택적 GUID가 toocorrelate 서비스 측 (키 자격 증명 모음) 로그를 사용 하 여 클라이언트 쪽 로그를 전달할 수 있습니다. |
| DurationMs |밀리초 단위로 tooservice hello REST API 요청에 소요 된 시간입니다. 이 시간 hello 클라이언트 쪽에서 측정 하는 hello 시간이 이번 일치 하지 않을 수 있으므로 네트워크 대기 시간, 포함 되지 않습니다. |
| httpStatusCode_d |Hello 요청에서 반환 된 HTTP 상태 코드 (예를 들어 *200*) |
| id_s |Hello 요청의 고유 ID |
| identity_claim_appid_g | Hello 응용 프로그램 id에 대 한 GUID |
| OperationName |에 설명 된 대로 hello 작업의 이름 [Azure 키 자격 증명 모음 로깅](../key-vault/key-vault-logging.md) |
| OperationVersion |Hello 클라이언트에서 요청 된 REST API 버전 (예를 들어 *2015-06-01*) |
| requestUri_s |Hello 요청의 Uri |
| 리소스 |Hello 키 자격 증명 모음의 이름 |
| ResourceGroup |Hello 키 자격 증명 모음의 리소스 그룹 |
| ResourceId |Azure 리소스 관리자 리소스 ID. 주요 자격 증명 모음 로그의 경우이 hello 주요 자격 증명 모음 리소스 id입니다. |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *VAULTS* |
| ResultSignature |HTTP 상태(예: *확인*) |
| ResultType |REST API 요청의 결과(예: *성공*) |
| SubscriptionId |Hello 주요 자격 증명 모음을 포함 하는 hello 구독의 azure 구독 ID |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Hello 이전 키 자격 증명 모음 솔루션에서 마이그레이션
2017 년 1 월 hello 분석 변경 하는 주요 자격 증명 모음 tooLog에서 로그를 보내는 방식으로 지원 합니다. 이러한 변경 내용은 다음 장점 hello를 제공 합니다.
+ 직접 hello 없이 tooLog 분석 필요 toouse 저장소 계정 로그가 기록
+ 로그가 hello 시간에서 대기 시간이 짧습니다 생성 toothem 로그 분석에 사용할 수 있습니다.
+ 구성 단계 감소
+ 모든 유형의 Azure 진단을 위한 공통 형식

toouse hello 솔루션을 업데이트 했습니다.

1. [주요 자격 증명 모음에서 tooLog 분석을 직접 전송 하는 진단 toobe 구성](#enable-key-vault-diagnostics-in-the-portal)  
2. 에 설명 된 hello 프로세스를 사용 하 여 hello Azure 키 자격 증명 모음 솔루션을 사용 하도록 설정 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)
3. 모든 저장 된 쿼리, 대시보드, 또는 경고 toouse hello 새 데이터 형식 업데이트
  + 형식이 변경: KeyVaults tooAzureDiagnostics 합니다. Hello ResourceType toofilter tooKey 자격 증명 모음 로그를 사용할 수 있습니다.
  - `Type=KeyVaults` 대신 `Type=AzureDiagnostics ResourceType=VAULTS`를 사용합니다.
  + 필드: (필드 이름은 대/소문자를 구분함)
  - 접미사가 있는 모든 필드에 대 한 \_s, \_d, 또는 \_g hello 이름 hello 첫 번째 문자 toolower 대/소문자 변경
  - 접미사가 있는 모든 필드에 대 한 \_o hello 데이터 이름에는 중첩 된 hello 필드 이름을 기반으로 하는 개별 필드도 나누어집니다. Hello hello 호출자의 UPN 필드에 저장 되는 예를 들어`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - 변경 된 필드 CallerIpAddress tooCallerIPAddress
   - RemoteIPCountry 필드는 더 이상 존재하지 않습니다.
4. Hello 제거 *키 자격 증명 모음 분석 (사용 되지 않음)* 솔루션입니다. PowerShell을 사용하는 경우 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`를 사용합니다.

데이터는 수집 전에 hello 변경이 hello 새 솔루션에 표시 되지 않습니다. 기존 형식 및 필드 이름을 hello 사용 하 여이 데이터에 대 한 tooquery를 계속할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview Azure 키 자격 증명 모음 데이터를 자세히 설명 합니다.
