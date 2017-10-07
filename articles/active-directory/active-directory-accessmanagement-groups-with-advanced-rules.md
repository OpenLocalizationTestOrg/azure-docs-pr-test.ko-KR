---
title: "Azure Active Directory에서 개체 특성에 따라 동적으로 aaaPopulate 그룹 | Microsoft Docs"
description: "방법-를 toocreate 규칙에 대 한 고급 식 규칙 연산자와 매개 변수 지원 되는 그룹 멤버 자격을 포함 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: fe22829118ed8f5137a619d93fa6f9bf80835863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>개체 특성에 따른 동적 그룹 채우기
Azure 클래식 포털 hello Azure Active Directory (Azure AD) 그룹에 대해 보다 복잡 한 특성 기반 동적 구성원을 hello 기능 tooenable 제공합니다.  

사용자 또는 장치 변경의 특성을 hello 시스템 평가 되 면 디렉터리 toosee의 모든 동적 그룹 규칙 hello 변경을 트리거하는 경우 모든 그룹에 추가 하거나 지웁니다. 사용자 또는 장치가 그룹에 대한 규칙을 만족하면 해당 그룹의 멤버로 추가됩니다. Hello 규칙을 더 이상 만족 하는 경우 제거 됩니다.

> [!NOTE]
> - 보안 그룹 또는 Office 365 그룹에서 동적 멤버 자격에 대한 규칙을 설정할 수 있습니다.
>
> - 이 기능은 각 사용자 멤버 중 하나 이상이 추가 tooat 동적 그룹에 대 한 Azure AD Premium P1 라이선스가 필요 합니다.
>
> - 장치 또는 사용자에 대한 동적 그룹을 만들 수 있지만 사용자 및 장치 개체를 모두 포함하는 규칙을 만들 수는 없습니다.

> - Hello 순간에 아닙니다 장치 그룹 소유 사용자의 특성에 따라 가능한 toocreate. 장치 멤버 자격 규칙 hello 디렉터리에 장치 개체의 직계 특성을 참조만 할 수 있습니다.

## <a name="toocreate-an-advanced-rule"></a>toocreate 고급 규칙
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 한 다음 조직의 디렉터리를 엽니다.
2. 선택 hello **그룹** 탭을 선택한 tooedit 연 다음 hello 그룹입니다.
3. 선택 hello **구성** 탭, 선택 hello **고급 규칙** 옵션을 선택한 다음 규칙 hello 텍스트 상자에 고급 hello를 입력 합니다.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Hello 고급 규칙 본문 구성
hello hello 그룹에 대 한 동적 멤버 자격에 대해 만들 수 있는 고급 규칙은 기본적으로 이진 식의 세 부분으로 구성 되어 있고 true 또는 false의 결과로입니다. hello 세 개의 부분은 다음과 같습니다.

* 왼쪽 매개 변수
* 이항 연산자
* 오른쪽 상수

전체 고급 규칙은 유사한 toothis: (leftParameter binaryOperator "RightConstant") 중괄호와 닫는 괄호 hello hello 전체 이진 식에 필요한 경우 큰따옴표는 hello 오른쪽 상수 및 hello 구문에 필요 hello 왼쪽된 매개 변수는 user.property. 고급 규칙 hello로 구분 된 이진 식 하나 이상 구성할 수 있습니다-및,-, 및-하지 논리 연산자입니다.
hello 다음은 제대로 구성 된 고급 규칙의 예입니다.

* (user.department -eq "Sales") -or (user.department -eq "Marketing")
* (user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")

지원 되는 매개 변수 및 식 규칙 연산자의 전체 목록은 hello, 아래 섹션을 참조 하세요.


hello 속성 ज ा य hello 올바른 개체 유형을 참고: 사용자 또는 장치입니다.
규칙 아래 hello hello 유효성 검사가 실패 합니다.-ne null 메일

hello 올바른 규칙 것입니다.

user.mail-ne null

hello hello 고급 규칙 본문의 총 길이 2048 자를 초과할 수 없습니다.

> [!NOTE]
> 문자열 및 regex 연산은 대/소문자를 구분합니다.
> 따옴표(")를 포함하는 문자열은 ' 문자를 사용하여 이스케이프해야 합니다(예: user.department -eq \`"Sales").
> 문자열 형식 값에 대해서만 따옴표를 사용하고, 영어 따옴표만 사용합니다.
>
>

## <a name="supported-expression-rule-operators"></a>지원되는 식 규칙 연산자
hello 다음 표에 나타난 모든 지원 되는 hello 식 규칙 연산자와 해당 구문 toobe hello hello 고급 규칙 본문에 사용 되는.

| 연산자 | 구문 |
| --- | --- |
| 같지 않음 |-ne |
| 같음 |-eq |
| 다음으로 시작 안 함 |-notStartsWith |
| 시작 |-startsWith |
| 포함하지 않음 |-notContains |
| 포함 |-contains |
| 일치하지 않음 |-notMatch |
| 일치 |-match |
| 내용 | -in |
| 속하지 않음 | -notIn |

## <a name="operator-precedence"></a>연산자 우선 순위

모든 연산자는 우선 순위가 낮은 toohigher에서 당 아래 나열 된 경우 같은 줄에서 연산자 같은 우선 순위에는-모든-all-또는-및-하지-eq-ne-startsWith-notStartsWith--notContains 포함-– 문자열이 일치--notIn에서

모든 연산자는 하이픈(-) 접두사를 사용하거나 사용하지 않을 수 있습니다.

Note 항상 괄호가 필요 하지 않은, 우선 순위 요구 사항을 예를 들어 충족 하지 않는 경우 tooadd 괄호에만 필요 합니다.

   user.department –eq "Marketing" –and user.country –eq "US"

이는 다음과 동등합니다.

   (user.department –eq "Marketing") –and (user.country –eq "US")

## <a name="using-hello--in-and--notin-operators"></a>사용 하 여 hello-에-notIn 연산자

서로 다른 값의 수와 사용자 특성 toocompare hello 값을 원하는 경우 사용할 수 있습니다 hello-에-notIn 연산자입니다. 다음은 예제를 사용 하 여 hello-In 연산자:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

Hello hello 사용 "[" 및 "]" hello의 시작과 끝 값 hello 목록에 있습니다. 이 조건이 tooTrue hello 목록의 hello 값 user.department equals 하나 hello 값의 평가 됩니다.

## <a name="query-error-remediation"></a>쿼리 오류 수정
hello 다음 표에 나와 잠재적인 오류 방법과 toocorrect 발생 한 경우

| 쿼리 구문 분석 오류 | 잘못된 사용법 | 수정된 사용법 |
| --- | --- | --- |
| 오류: 특성이 지원되지 않습니다. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/>속성 중 hello 하 나와 일치 해야 [속성 목록 지원](#supported-properties)합니다. |
| 오류: 특성에서는 연산자가 지원되지 않습니다. |(user.accountEnabled -contains true) |(user.accountEnabled -eq true)<br/>속성은 부울 형식입니다. 지원 되는 hello 연산자를 사용 하 여 (-eq 또는-ne) 목록 위의 hello 부울 형식에 있습니다. |
| 오류: 쿼리 컴파일 오류입니다. |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>논리 연산자는 위의 지원 hello 속성 목록 중 하 나와 일치 해야 합니다. (user.userPrincipalName-일치 ". *@domain.ext") 또는 (user.userPrincipalName-일치 "@domain.ext$") 정규식에 오류가 있습니다. |
| 오류: 이진 식 형식이 올바르지 않습니다. |(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>쿼리에 오류가 여러 개 있습니다. 괄호 위치가 적절하지 않습니다. |
| 오류: 동적 멤버 자격을 설정하는 동안 알 수 없는 오류가 발생했습니다. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>쿼리에 오류가 여러 개 있습니다. 괄호 위치가 적절하지 않습니다. |

## <a name="supported-properties"></a>지원되는 속성
hello 다음은 고급 규칙에서 사용할 수 있는 모든 hello 사용자 속성입니다.

### <a name="properties-of-type-boolean"></a>부울 형식의 속성
허용되는 연산자

* -eq
* -ne

| 속성 | 허용되는 값 | 사용 현황 |
| --- | --- | --- |
| accountEnabled |true false |user.accountEnabled -eq true |
| dirSyncEnabled |true false |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>문자열 형식의 속성
허용되는 연산자

* -eq
* -ne
* -notStartsWith
* -startsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| 속성 | 허용되는 값 | 사용 현황 |
| --- | --- | --- |
| city |임의의 문자열 값 또는 $null입니다. |(user.city -eq "value") |
| country |임의의 문자열 값 또는 $null입니다. |(user.country -eq "value") |
| companyName | 임의의 문자열 값 또는 $null입니다. | (user.companyName -eq "value") |
| department |임의의 문자열 값 또는 $null입니다. |(user.department -eq "value") |
| displayName |임의의 문자열 값입니다. |(user.displayName -eq "value") |
| facsimileTelephoneNumber |임의의 문자열 값 또는 $null입니다. |(user.facsimileTelephoneNumber -eq "value") |
| givenName |임의의 문자열 값 또는 $null입니다. |(user.givenName -eq "value") |
| jobTitle |임의의 문자열 값 또는 $null입니다. |(user.jobTitle -eq "value") |
| mail |문자열 값 또는 $null (hello 사용자의 SMTP 주소) |(user.mail -eq "value") |
| mailNickName |임의의 문자열 값 (hello 사용자의 메일 별칭) |(user.mailNickName -eq "value") |
| mobile |임의의 문자열 값 또는 $null입니다. |(user.mobile -eq "value") |
| objectId |Hello 사용자 개체의 GUID |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | 온-프레미스 SID (보안 식별자)에서 동기화 된 사용자에 대 한 온-프레미스 toohello 클라우드입니다. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |임의의 문자열 값 또는 $null입니다. |(user.physicalDeliveryOfficeName -eq "value") |
| postalCode |임의의 문자열 값 또는 $null입니다. |(user.postalCode -eq "value") |
| preferredLanguage |ISO 639-1 코드 |(user.preferredLanguage -eq "en-US") |
| sipProxyAddress |임의의 문자열 값 또는 $null입니다. |(user.sipProxyAddress -eq "value") |
| state |임의의 문자열 값 또는 $null입니다. |(user.state -eq "value") |
| streetAddress |임의의 문자열 값 또는 $null입니다. |(user.streetAddress -eq "value") |
| surname |임의의 문자열 값 또는 $null입니다. |(user.surname-eq "value") |
| telephoneNumber |임의의 문자열 값 또는 $null입니다. |(user.telephoneNumber -eq "value") |
| usageLocation |두 자로 된 국가 코드 |(user.usageLocation -eq "US") |
| userPrincipalName |임의의 문자열 값입니다. |(user.userPrincipalName -eq "alias@domain") |
| userType |member guest $null |(user.userType -eq "Member") |

### <a name="properties-of-type-string-collection"></a>문자열 컬렉션 형식의 속성
허용되는 연산자

* -contains
* -notContains

| 속성 | 허용되는 값 | 사용 현황 |
| --- | --- | --- |
| otherMails |임의의 문자열 값입니다. |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp: alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>다중 값 속성
허용되는 연산자

* -모든 (만족 hello 컬렉션에 항목을 하나 이상 hello 조건과 일치 하는 경우)
* -모든 (충족 hello 컬렉션의 모든 항목이 hello 조건과 일치 하는 경우)

| properties | 값 | 사용 현황 |
| --- | --- | --- |
| assignedPlans |Hello 다음과 같은 문자열 속성을 노출 하는 hello 컬렉션의 각 개체: capabilityStatus, 서비스, servicePlanId |user.assignedPlans -any(assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

다중 값 속성 hello 개체의 컬렉션은 같은 형식입니다. -같이 사용할 수 있습니다. 모든 매개 변수와-모든 연산자 tooapply 조건 tooone 또는 hello의 모든 컬렉션의 항목을 hello, 각각. 예:

assignedPlans은 toohello 사용자를 할당 하는 모든 서비스 계획을 나열 하는 다중 값 속성입니다. 식 아래 hello 사용 상태에 있는 hello Exchange Online 계획 2 개 서비스 계획을 설치한 사용자를 선택 합니다.

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(hello Guid 식별자 hello Exchange Online 계획 2 개 서비스 계획을 식별 합니다.)

> [!NOTE]
> 대상 tooidentify 모든 사용자가 원하는 경우에 유용 Office 365 (또는 기타 Microsoft 온라인 서비스) 기능이 활성화 되어 있는 예제 tootarget에 대 한 일련의 정책 사용 하 여 합니다.

hello 다음 식은 선택 합니다 ("SCO" 서비스 이름으로 식별 됨)는 Intune 서비스 hello와 연결 된 모든 서비스 계획에 있는 모든 사용자.
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Null 값 사용

규칙에 null 값이 toospecify, "null" 또는 $null 사용할 수 있습니다. 예제:

   user.mail -ne null은 user.mail –ne $null과 동등합니다.

## <a name="extension-attributes-and-custom-attributes"></a>확장 특성 및 사용자 지정 특성
확장 특성 및 사용자 지정 특성은 동적 멤버 자격 규칙에서 지원됩니다.

확장 특성 온-프레미스 Windows Server AD에서에서 동기화 되 고 여기서 X은 1-15 "ExtensionAttributeX" hello 형식의 수행 합니다.
확장 특성을 사용하는 규칙의 예는 다음과 같습니다.

(user.extensionAttribute15 -eq "Marketing")

사용자 지정 특성 또는 연결 된 SaaS 응용 프로그램 및 hello hello 형식에서의 온-프레미스 Windows Server AD에서에서 동기화 된 "user.extension_[GUID]\__ [Attribute]", 여기서 [GUID]는 hello 응용 프로그램에 대 한 AAD에서 hello 고유 식별자를 AAD와 [Attribute]에서 생성된 된 hello 특성은은 만들어지지 hello 특성의 hello 이름입니다.
사용자 지정 특성을 사용하는 규칙의 예는 다음과 같습니다.

user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

hello 사용자 지정 특성 이름 있습니다 hello 디렉터리에 사용자를 쿼리하여의 그래프 탐색기를 사용 하 여 특성과 hello 특성 이름을 검색 합니다.

## <a name="direct-reports-rule"></a>"직접 보고" 규칙
관리자의 직접 보고서를 모두 포함하는 그룹을 만들 수 있습니다. Hello 관리자의 부하 직원 hello 이후 바뀌면 hello 그룹의 구성원 자격은 자동으로 조정 됩니다.

> [!NOTE]
> 1. Hello 규칙 toowork 확인 되었는지 hello **관리자 ID** 테 넌 트의 사용자에 대해 속성이 올바르게 설정 되어 있습니다. 사용자에 대 한 hello 현재 값을 확인할 수 있습니다 자신의 **프로필 탭**합니다.
> 2. 이 규칙은 **직접** 보고서만을 지원합니다. 이 현재 가능한 toocreate 부하 직원 및 보고서를 포함 하는 그룹 예를 들어 중첩된 된 계층에 대 한 그룹이 없습니다.

**tooconfigure hello 그룹**

1. 섹션에서 1-5 단계를 수행 [toocreate hello 고급 규칙](#to-create-the-advanced-rule), 선택는 **멤버 자격 유형** 의 **동적 사용자**합니다.
2. Hello에 **동적 멤버 자격 규칙** 블레이드에서 구문 다음 hello로 hello 규칙을 입력 합니다.

    *"{obectID_of_manager}"의 직접 보고서*

    올바른 규칙의 예제:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Hello 규칙을 저장 한 후 hello 있는 모든 사용자가 관리자 ID 값이 toohello 그룹 추가 되 지정 합니다.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>장치 개체에 대 한 특성 toocreate 규칙을 사용 하 여
또한 그룹의 멤버 자격에 대한 장치 개체를 선택하는 규칙을 만들 수 있습니다. hello 다음 장치 특성을 사용할 수 있습니다.

| properties              | 허용되는 값                  | 사용 현황                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| accountEnabled          | true false                      | (device.accountEnabled -eq true)                            |
| displayName             | 임의의 문자열 값입니다.                | (device.displayName -eq "Rob Iphone”)                       |
| deviceOSType            | 임의의 문자열 값입니다.                | (device.deviceOSType -eq "IOS")                             |
| deviceOSVersion         | 임의의 문자열 값입니다.                | (device.OSVersion -eq "9.1")                                |
| deviceCategory          | 임의의 문자열 값입니다.                | (device.deviceCategory -eq "")                              |
| deviceManufacturer      | 임의의 문자열 값입니다.                | (device.deviceManufacturer -eq "Microsoft")                 |
| deviceModel             | 임의의 문자열 값입니다.                | (device.deviceModel -eq "IPhone 7+")                        |
| deviceOwnership         | 임의의 문자열 값입니다.                | (device.deviceOwnership -eq "")                             |
| domainName              | 임의의 문자열 값입니다.                | (device.domainName -eq "contoso.com")                       |
| enrollmentProfileName   | 임의의 문자열 값입니다.                | (device.enrollmentProfileName -eq "")                       |
| isRooted                | true false                      | (device.deviceOSType -eq true)                              |
| managementType          | 임의의 문자열 값입니다.                | (device.managementType -eq "")                              |
| organizationalUnit      | 임의의 문자열 값입니다.                | (device.organizationalUnit -eq "")                          |
| deviceId                | 유효한 deviceId                | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| objectId                | 유효한 AAD objectId            | (device.objectId -eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> Hello "간단한 규칙" 드롭다운을 사용 하 여 hello Azure 클래식 포털에서에서 해당 장치 규칙을 만들 수 없습니다.
>
>

## <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [그룹의 동적 멤버 자격 문제 해결](active-directory-accessmanagement-troubleshooting.md)
* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [그룹 설정을 구성하는 Azure Active Directory cmdlets](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
