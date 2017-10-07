---
title: "aaaAzure Active Directory 로그인 활동 보고서 API 참조 | Microsoft Docs"
description: "Hello Azure Active Directory 로그인 활동 보고서 API에 대 한 참조"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Azure Active Directory 로그인 활동 보고서 API 참조
이 항목은 Azure Active Directory hello에 대 한 항목 컬렉션의 일부 API를 보고 합니다.  
Azure AD 보고 하면 있도록 API 코드 또는 관련된 도구를 사용 하 여 tooaccess 로그인 활동 보고서 데이터 있습니다.
이 항목의 hello 범위는 tooprovide hello에 대 한 참조 정보는 **로그인 활동 보고서 API**합니다.

다음을 참조하세요.

* [로그인 활동](active-directory-reporting-azure-portal.md#activity-reports) 을 참조하세요.
* [Hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md) hello 보고 API에 대 한 자세한 내용은 합니다.


## <a name="who-can-access-hello-api-data"></a>Hello API 데이터에 액세스할 수 있는 사용자?
* 사용자 및 서비스 사용자 역할 hello 보안 판독기 또는 보안 관리자 역할
* 전역 관리자
* 권한 부여 tooaccess hello API를 모든 앱 (앱 권한 부여 가능 설치 전역 관리자의 사용 권한을 기반만)

응용 프로그램 tooaccess 보안 Api signin 이벤트와 같은 PowerShell tooadd hello 응용 프로그램 서비스 사용자 hello 보안 읽기 역할에 따라 사용 하 여 hello에 대 한 tooconfigure 액세스

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>필수 조건
이 통해 보고 tooaccess hello 보고 API 있어야 합니다.

* [Azure Active Directory Premium P1 또는 P2 Edition](active-directory-editions.md)
* 완료 된 hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites.md)합니다. 

## <a name="accessing-hello-api"></a>Hello API 액세스
Hello를 통해이 API를 액세스 하거나 [그래프 탐색기](https://graphexplorer2.cloudapp.net) 프로그래밍 방식으로 사용 하거나, 예를 들어 PowerShell. 순서 대로 PowerShell toocorrectly 해석 AAD Graph REST 호출에 사용 된 hello OData 필터 구문에 대 한 사용 해야 hello 억음 악센트 기호 (즉,: 억음 악센트 기호) 문자 너무 "문자는 이스케이프 처리할" hello $. hello 억음 악센트 문자 역할을 [PowerShell의 이스케이프 문자](https://technet.microsoft.com/library/hh847755.aspx), PowerShell toodo hello $ 문자를 해석 하는 리터럴 허용 하 고 PowerShell 변수 이름으로 혼동 하지 않도록 (예: $filter).

이 항목의 포커스를 hello hello 그래프 탐색기 켜져 있습니다. PowerShell 예제는 이 [PowerShell 스크립트](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script)를 참조하세요.

## <a name="api-endpoint"></a>API 끝점
기본 URI 뒤 hello를 사용 하 여이 API에 액세스할 수 있습니다.  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



이 API는 toohello 양의 데이터가 인해 1 백만 레코드의 제한을 있습니다. 

이 호출 일괄 처리로 hello 데이터를 반환합니다. 각 배치에는 최대 1000개 레코드가 있습니다.  
tooget hello의 다음 일괄 처리 레코드를 사용 하 여 hello 다음 링크 합니다. Hello 가져오기 [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) hello 반환 되는 레코드의 첫 번째 집합의 정보입니다. hello skip 토큰 hello 결과 집합의 hello 끝에 됩니다.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>지원되는 필터
Hello API에 의해 반환 된 레코드 수를 좁힐 수 있는 필터의 양식에서.  
로그인 API에 대 한 관련된 데이터를 필터에 따라 hello 지원 됩니다.

* **$top =\<반환 된 레코드 toobe 수가\>**  -toolimit hello 반환 된 레코드 수입니다. 이 작업은 비용이 많이 드는 작업입니다. 개체의 tooreturn 수천을 원하는 경우이 필터를 사용 하지 않아야 합니다.  
* **$filter =\<필터 문을\>**  -toospecify hello 별로 지원 되는 필터 필드, 중요 한 레코드의 hello 종류

## <a name="supported-filter-fields-and-operators"></a>지원되는 필터 필드 및 연산자
toospecify hello 유형 중요 한 레코드를 하나 또는 hello 필터 필드를 다음의 조합을 포함할 수 있는 필터 문을 작성할 수 있습니다.

* [signinDateTime](#signindatetime) - 날짜 또는 날짜 범위를 정의합니다.
* [userId](#userid) -정의 기반으로 특정 사용자 hello 사용자의 id입니다.
* [userPrincipalName](#userprincipalname) -특정 사용자 기반 hello 사용자의 사용자 계정 이름 (UPN)을 정의 합니다.
* [appId](#appid) -특정 응용 프로그램 기반 hello 앱의 ID를 정의 합니다.
* [appDisplayName](#appdisplayname) -정의 기반으로 하는 특정 앱 hello 응용 프로그램의 표시 이름
* [loginStatus](#loginStatus) -정의 hello 로그인의 hello 상태 (성공 / 실패)

> [!NOTE]
> 그래프 탐색기를 사용할 때는 hello 있습니다 각 문자에 대 한 사례 필터 필드는 올바른 toouse hello가 필요 합니다.
> 
> 

데이터를 반환 하는 hello hello 범위 아래로 toonarrow를 hello 지원 필터 및 필터 필드의 조합을 작성할 수 있습니다. 예를 들어 hello 다음 반환 명령문 hello 1 일부 터 2016 년 7 월 6 일 2016 년 7 월 사이의 상위 10 개의 레코드:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**지원되는 연산자**: eq, ge, le, gt, lt

**예제**:

특정 날짜 사용

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



날짜 범위 사용    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**참고**:

hello datetime 매개 변수는 hello UTC 형식에서 이어야 합니다. 

- - -
### <a name="userid"></a>userId
**지원되는 연산자**: eq

**예제**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**참고**:

사용자 Id의 hello 값은 문자열 값

- - -
### <a name="userprincipalname"></a>userPrincipalName
**지원되는 연산자**: eq

**예제**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**참고**:

userPrincipalName의 hello 값은 문자열 값

- - -
### <a name="appid"></a>appId
**지원되는 연산자**: eq

**예제**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**참고**:

appId의 hello 값은 문자열 값

- - -
### <a name="appdisplayname"></a>appDisplayName
**지원되는 연산자**: eq

**예제**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**참고**:

appDisplayName의 hello 값은 문자열 값

- - -
### <a name="loginstatus"></a>loginStatus
**지원되는 연산자**: eq

**예제**:

    $filter=loginStatus+eq+'1'  


**참고**:

LoginStatus hello에 대 한 두 가지가 있습니다: 0-성공을, 1-실패

- - -
## <a name="next-steps"></a>다음 단계
* 필터링 된 로그인 활동에 대 한 toosee 예제 시겠습니까? 체크 아웃 hello [Azure Active Directory 로그인 활동 보고서 API 예제](active-directory-reporting-api-sign-in-activity-samples.md)합니다.
* Tooknow hello Azure AD 보고 API에 대 한 자세한 하 시겠습니까? 참조 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.

