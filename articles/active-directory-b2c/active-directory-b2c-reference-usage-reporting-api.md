---
title: "Azure Active Directory B2C: 사용량 보고 API 샘플 및 정의 | Microsoft Docs"
description: "Azure AD B2C 테넌트 사용자, 인증 및 다단계 인증에 대한 보고서를 얻는 방법에 대한 가이드 및 샘플입니다."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Hello 보고 API를 통해 Azure AD B2C의 사용 현황 보고서에 액세스

Azure AD B2C(Azure Active Directory B2C)는 사용자 로그인 및 Azure Multi-Factor Authentication 기반 인증을 제공합니다. 인증은 ID 공급자를 통해 응용 프로그램 제품군의 최종 사용자에게 제공됩니다. Hello 유형별 hello 테 넌 트, tooregister, 및 인증 hello 수는 데 사용 하는 hello 공급자에에서 등록 된 사용자 수를 알고 있는 경우와 같은 확인할 수 있습니다.
* 각 유형의 id 공급자 (예를 들어 Microsoft 소프트웨어 또는 LinkedIn 계정)에서 얼마나 많은 사용자 최근 10 일 동안 hello에 등록 한?
* Hello 지난 달의에서 Multi-factor Authentication을 사용 하 여 제공할 인증 수를 성공적으로 완료?
* 이번 달에 완료된 로그인 기반 인증은 몇 번인가요? 일일? 응용 프로그램 당?
* Hello 예상 내 Azure AD B2C 테 넌 트 작업의 월별 비용을 예측할 수는 방법

이 문서는 사용자, 기호에 따라 청구 가능한 인증 및 multi-factor authentication의 hello 수를 기반으로 하는 연결 된 보고서 toobilling 활동에 중점을 둡니다.


## <a name="prerequisites"></a>필수 조건
toocomplete hello 단계를 시작 하기 전에 필요한 [필수 구성 요소 tooaccess hello Azure AD reporting Api](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)합니다. 응용 프로그램을 만들고,에 대 한 암호를 가져올 액세스용 grant 권한 tooyour Azure AD B2C 테 넌 트의 보고서입니다. *Bash 스크립트* 및 *Python 스크립트* 예제도 여기에 제공됩니다. 

## <a name="powershell-script"></a>PowerShell 스크립트
이 스크립트는 hello를 사용 하 여 hello 4 개의 사용 현황 보고서 생성을 보여 줍니다. `TimeStamp` 매개 변수 및 hello `ApplicationId` 필터입니다.

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a>사용량 보고서 정의
* **tenantUserCount**: hello 하루 hello에 id 공급자의 형식에 의해 hello 테 넌 트의 사용자 수가 지난 30 일 이내입니다. (필요에 따라 한 `TimeStamp` 필터는 현재 날짜에서 특정된 날짜 toohello 사용자 까지의 제공). hello 보고서 제공합니다.
  * **TotalUserCount**: hello 모든 사용자 개체 수입니다.
  * **OtherUserCount**: hello Azure Active Directory 사용자 (Azure AD B2C 사용자가 아닌)의 수입니다.
  * **LocalUserCount**: hello Azure AD B2C 사용자 계정 자격 증명 로컬 toohello Azure AD B2C 테 넌 트를 사용 하 여 만든 수 있습니다.

* **AlternateIdUserCount**: 외부 id 공급자와 함께 등록 된 Azure AD B2C 사용자 hello 수 (예를 들어, Facebook, Microsoft 계정 또는 다른 Azure Active Directory 테 넌 트, 라고도 tooas는 `OrgId`).

* **b2cAuthenticationCountSummary**: hello 매일 일 및 인증 흐름의 형식에 따라 지난 30 일 hello 통해 청구 가능 인증 수를 요약 합니다.

* **b2cAuthenticationCount**: 시간 간격 내에서 인증 수 hello 합니다. hello 기본값이 hello 지난 30 일 이내입니다.  (선택 사항: hello 시작 및 끝 `TimeStamp` 매개 변수를 정의 특정 시간 기간) hello 출력에는 `StartTimeStamp` (이 테 넌이 트에 대 한 활동의 가장 빠른 날짜) 및 `EndTimeStamp` (최신 업데이트) 합니다.

* **b2cMfaRequestCountSummary**: hello 일일 수 요일과 유형 (음성 또는 SMS) 하 여 multi-factor authentication의 요약입니다.


## <a name="limitations"></a>제한 사항
사용자 수 데이터는 24 too48 시간 마다 새로 고쳐집니다. 인증은 하루에도 여러 번 업데이트됩니다. Hello를 사용 하는 경우 `ApplicationId` 필터에 빈 보고서 응답 때문일 수 있습니다 다음 조건 중 tooone:
  * hello 응용 프로그램 ID hello 테 넌 트에 존재 하지 않습니다. 정확한지 확인하세요.
  * hello 응용 프로그램 ID가 있지만 데이터를 보고 기간 hello에서 찾지 못했습니다. 날짜/시간 매개 변수를 검토하세요.


## <a name="next-steps"></a>다음 단계
### <a name="monthly-bill-estimates-for-azure-ad"></a>Azure AD에 대한 월별 예상 청구 비용 견적
함께 사용 하면 [최신 Azure AD B2C 가격 가능 hello](https://azure.microsoft.com/pricing/details/active-directory-b2c/)를 예측할 수 있습니다 매일, 주별 및 월별 Azure 소비 합니다.  견적은 전체 비용에 영향을 줄 수 있는 테넌트 동작의 변경 내용을 계획할 때 특히 유용합니다. [연결된 Azure 구독](active-directory-b2c-how-to-enable-billing.md)에서 실제 비용을 검토할 수 있습니다.

### <a name="options-for-other-output-formats"></a>다른 출력 형식의 옵션
hello 다음 코드 예를 보여 줍니다 출력 tooJSON, 이름 값 목록 및 XML 보내기:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
