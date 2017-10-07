---
title: "aaaAzure Active Directory 감사 API 참조 | Microsoft Docs"
description: "Tooget은 hello Azure Active Directory 감사 API로 시작 하는 방법"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Azure Active Directory 감사 API 참조
이 항목은 Azure Active Directory hello에 대 한 항목 컬렉션의 일부 API를 보고 합니다.  
Azure AD 보고 하면 있도록 API 코드 또는 관련된 도구를 사용 하 여 tooaccess 감사 데이터 있습니다.
이 항목의 hello 범위는 tooprovide hello에 대 한 참조 정보는 **API 감사**합니다.

다음을 참조하세요.

* 자세한 개념 정보는 [감사 로그](active-directory-reporting-azure-portal.md#activity-reports)를 참조하세요.

* [Hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md) hello 보고 API에 대 한 자세한 내용은 합니다.


관련 작업:

- 질문과 대답(FAQ)은 [FAQ](active-directory-reporting-faq.md)를 읽어보세요. 

- 문제는 [지원 티켓을 파일로 저장하세요](active-directory-troubleshooting-support-howto.md). 


## <a name="who-can-access-hello-data"></a>Hello 데이터에 액세스할 수 있는 사용자?
* Hello 보안 판독기 또는 보안 관리자 역할의 사용자
* 전역 관리자
* 권한 부여 tooaccess hello API를 모든 앱 (앱 권한 부여 가능 설치 전역 관리자의 사용 권한을 기반만)

## <a name="prerequisites"></a>필수 조건
Hello Reporting API를 통해 보고이 순서 tooaccess에 있어야 합니다.

* [Azure Active Directory 무료 이상 버전](active-directory-editions.md)
* 완료 된 hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites.md)합니다. 

## <a name="accessing-hello-api"></a>Hello API 액세스
Hello를 통해이 API를 액세스 하거나 [그래프 탐색기](https://graphexplorer2.cloudapp.net) 프로그래밍 방식으로 사용 하거나, 예를 들어 PowerShell. 순서 대로 PowerShell toocorrectly 해석 AAD Graph REST 호출에 사용 된 hello OData 필터 구문에 대 한 사용 해야 hello 억음 악센트 기호 (즉,: 억음 악센트 기호) 문자 너무 "문자는 이스케이프 처리할" hello $. hello 억음 악센트 문자 역할을 [PowerShell의 이스케이프 문자](https://technet.microsoft.com/library/hh847755.aspx), PowerShell toodo hello $ 문자를 해석 하는 리터럴 허용 하 고 PowerShell 변수 이름으로 혼동 하지 않도록 (예: $filter).

이 항목의 포커스를 hello hello 그래프 탐색기 켜져 있습니다. PowerShell 예제는 이 [PowerShell 스크립트](active-directory-reporting-api-audit-samples.md#powershell-script)를 참조하세요.

## <a name="api-endpoint"></a>API 끝점
다음 URI는 hello를 사용 하 여이 API에 액세스할 수 있습니다.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Hello hello Azure AD 감사 API (OData 페이지 매김을 사용)에서 반환 된 레코드 수에 제한이 있습니다.
데이터 보고에서 보존 제한은 [보존 정책 보고](active-directory-reporting-retention.md)를 확인하세요.

이 호출 일괄 처리로 hello 데이터를 반환합니다. 각 배치에는 최대 1000개 레코드가 있습니다.  
tooget hello의 다음 일괄 처리 레코드를 사용 하 여 hello 다음 링크 합니다. 반환 된 레코드의 첫 번째 집합 hello hello skiptoken 정보를 가져옵니다. hello skip 토큰 hello 결과 집합의 hello 끝에 됩니다.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>지원되는 필터
Hello API에 의해 반환 된 레코드 수를 좁힐 수 있는 필터의 양식에서.  
로그인 API에 대 한 관련된 데이터를 필터에 따라 hello 지원 됩니다.

* **$top =\<반환 된 레코드 toobe 수가\>**  -toolimit hello 반환 된 레코드 수입니다. 이 작업은 비용이 많이 드는 작업입니다. 개체의 tooreturn 수천을 원하는 경우이 필터를 사용 하지 않아야 합니다.     
* **$filter =\<필터 문을\>**  -toospecify hello 별로 지원 되는 필터 필드, 중요 한 레코드의 hello 종류

## <a name="supported-filter-fields-and-operators"></a>지원되는 필터 필드 및 연산자
toospecify hello 유형 중요 한 레코드를 하나 또는 hello 필터 필드를 다음의 조합을 포함할 수 있는 필터 문을 작성할 수 있습니다.

* [activityDate](#activitydate) - 날짜 또는 날짜 범위를 정의합니다.
* [범주](#category) -toofilter에서 원하는 hello 범주를 정의 합니다.
* [activityStatus](#activitystatus) -작업의 hello 상태 정의
* [activityType](#activitytype) -hello 유형의 활동을 정의 합니다.
* [활동](#activity) -문자열로 hello 활동을 정의 합니다.  
* [행위자/이름](#actorname) -hello 행위자의 이름 형식으로의 hello 행위자를 정의 합니다.
* [행위자/objectid](#actorobjectid) -hello 행위자 ID의 형태로 hello 행위자를 정의 합니다.   
* [행위자/upn](#actorupn) -hello 행위자의 사용자 계정 이름 (UPN)의 형태로 hello 행위자를 정의 합니다. 
* [대상/이름](#targetname) -hello 행위자의 이름 형식으로의 hello 대상 정의
* [대상/objectid](#targetobjectid) -hello 대상 ID의 형태로 hello 대상을 정의  
* [대상/upn](#targetupn) -hello 행위자의 사용자 계정 이름 (UPN)의 형태로 hello 행위자를 정의 합니다.   

- - -
### <a name="activitydate"></a>activityDate
**지원되는 연산자**: eq, ge, le, gt, lt

**예제**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**참고**:

datetime는 UTC 형식이어야 합니다.

- - -
### <a name="category"></a>카테고리

**지원되는 값**:

| Category                         | 값     |
| :--                              | ---       |
| 핵심 디렉터리                   | 디렉터리 |
| 셀프 서비스 암호 관리 | SSPR      |
| 셀프 서비스 그룹 관리    | SSGM      |
| 계정 프로비전             | 동기화      |
| 자동화된 암호 롤오버      | 자동화된 암호 롤오버 |
| ID 보호              | IdentityProtection |
| 사용자 초대                    | 사용자 초대 |
| MIM 서비스                      | MIM 서비스 |



**지원되는 연산자**: eq

**예제**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**지원되는 값**:

| 활동 상태 | 값 |
| :--             | ---   |
| 성공         | 0     |
| 실패         | - 1   |

**지원되는 연산자**: eq

**예제**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**지원되는 연산자**: eq

**예제**:

    $filter=activityType eq 'User'    

**참고**:

대/소문자 구분

- - -
### <a name="activity"></a>활동
**연산자 지원**: eq, contains, startsWith

**예제**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**참고**:

대/소문자 구분

- - -
### <a name="actorname"></a>행위자/이름
**연산자 지원**: eq, contains, startsWith

**예제**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**참고**:

대/소문자 구분하지 않음

- - -
### <a name="actorobjectid"></a>행위자/objectid
**지원되는 연산자**: eq

**예제**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>대상/이름
**연산자 지원**: eq, contains, startsWith

**예제**:

    $filter=targets/any(t: t/name eq 'some name')    

**참고**:

대/소문자 구분하지 않음

- - -
### <a name="targetupn"></a>대상/upn
**연산자 지원**: eq, startsWith

**예제**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**참고**:

* 대/소문자 구분하지 않음
* Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity 쿼리할 때 필요한 tooadd hello 전체 네임 스페이스

- - -
### <a name="targetobjectid"></a>대상/objectid
**지원되는 연산자**: eq

**예제**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>행위자/upn
**연산자 지원**: eq, startsWith

**예제**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**참고**:

* 대/소문자 구분하지 않음 
* Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity 쿼리할 때 필요한 tooadd hello 전체 네임 스페이스

- - -
## <a name="next-steps"></a>다음 단계
* 필터링 된 시스템 작업에 대 한 toosee 예제 시겠습니까? 체크 아웃 hello [Azure Active Directory 감사 API 예제](active-directory-reporting-api-audit-samples.md)합니다.
* Tooknow hello Azure AD 보고 API에 대 한 자세한 하 시겠습니까? 참조 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.

