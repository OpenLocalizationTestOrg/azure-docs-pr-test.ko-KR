---
title: "Azure AD Connect: 선언적 프로비전 식 | Microsoft Docs"
description: "Hello 선언적 프로비저닝 식에 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Azure AD Connect 동기화: 선언적 프로비전 식 이해
Azure AD Connect 동기화는 Forefront Identity Manager 2010에 처음 도입된 선언적 프로비전을 기반으로 합니다. Tooimplement 허용 hello 필요 toowrite 없이 완전 한 id 통합 비즈니스 논리 컴파일된 코드입니다.

선언적 프로비저닝의 핵심 부분은 특성 흐름에 사용 되는 hello 식 언어입니다. 사용 되는 hello 언어는 Microsoft® Visual Basic®에 대 한 VBA의 일부입니다. 이 언어는 Microsoft Office에서 사용되며, VBScript 경험이 있는 사용자 또한 이 언어를 인식합니다. hello 선언적 프로비저닝 표현 언어는 함수만 사용 및 구조적 언어가 아닙니다. 메서드 또는 문이 없습니다. 함수는 중첩 대신 tooexpress 흐름을 프로그래밍 합니다.

자세한 내용은 참조 하십시오. [toohello Visual Basic for Applications 언어 참조 Office 2013에 대 한 시작](https://msdn.microsoft.com/library/gg264383.aspx)합니다.

hello 특성은 강력한 형식입니다. 함수는 hello 올바른 형식의 특성만 허용 합니다. 대/소문자를 구분하기도 합니다. 함수 이름과 특성 이름은 모두 적절한 대/소문자를 가지고 있어야 하며 그렇지 않으면 오류가 발생합니다.

## <a name="language-definitions-and-identifiers"></a>언어 정의 및 식별자
* 함수는 다음과 같이 이름 뒤에 대괄호로 인수가 붙습니다. FunctionName(인수 1, 인수 N).
* 특성은 다음과 같이 대괄호로 식별됩니다. [attributeName]
* 매개 변수는 다음과 같이 백분율 기호로 식별됩니다. % ParameterName %
* 문자열 상수는 따옴표를 사용합니다(예: "Contoso"). (참고: 둥근 따옴표 “”가 아닌 직선 따옴표 ""를 사용)
* 숫자 값은 10 진수 예상된 toobe 및 따옴표 없이 표시 됩니다. 16진수 값은 접두사 &H가 붙습니다. 예: 98052, &HFF
* 부울 값은 다음과 같은 상수로 표시됩니다. True, False
* 기본 제공 상수 및 리터럴은 자신의 이름으로만 표현됩니다. NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>함수
선언적 프로비저닝이 많은 함수 tooenable hello 가능성 tootransform 특성 값을 사용합니다. 한 함수의 결과 hello tooanother 함수에 전달 되는 하므로 이러한 함수를 중첩할 수 있습니다.

`Function1(Function2(Function3()))`

hello에 hello 전체 함수 목록은 있습니다 [함수 참조](active-directory-aadconnectsync-functions-reference.md)합니다.

### <a name="parameters"></a>매개 변수
매개 변수는 커넥터를 통해 또는 PowerShell을 사용하는 관리자에 의해 정의됩니다. Hello 도메인 hello 사용자의 hello 이름에 있는 예를 들어와 매개 변수는 일반적으로 시스템 toosystem에서 다른 값을 포함 합니다. 이러한 매개 변수를 특성 흐름에서 사용할 수 있습니다.

인바운드 동기화 규칙에 대 한 매개 변수 뒤 Active Directory Connector 제공 된 hello을 hello:

| 매개 변수 이름 | 주석 |
| --- | --- |
| Domain.Netbios |Netbios 형식의 hello 도메인 현재 가져오기 예를 들어 FABRIKAMSALES |
| Domain.FQDN |Hello 도메인 현재 가져오기 예를 들어 sales.fabrikam.com의 FQDN 형식 |
| Domain.LDAP |Hello 도메인 현재 가져오기 예를 들어 DC의 LDAP 형식을 판매, DC = = fabrikam, DC = com |
| Forest.Netbios |Hello 포리스트 이름 현재 가져오기 예를 들어 FABRIKAMCORP Netbios 형식 |
| Forest.FQDN |Hello 포리스트 이름 현재 가져오기 예를 들어 fabrikam.com FQDN 형식 |
| Forest.LDAP |LDAP 이름의 형식이 hello 포리스트 현재 가져오기 예를 들어 DC = fabrikam, DC = com |

hello 시스템 제공 hello 매개 변수를 다음 실행 되는 hello 커넥터의 hello 식별자를 사용 하는 tooget 현재:  
`Connector.ID`

Hello 사용자가 있는 hello 도메인의 netbios 이름 hello 사용 하 여 hello 메타 버스 특성 도메인을 채우는 예는 다음과 같습니다.  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>연산자
hello 다음 연산자를 사용할 수 있습니다.

* **비교**: <, <=, <>, =, >, >=
* **수학**: +, -, \*, -
* **문자열**: &(연결)
* **논리**: &&(및), ||(또는)
* **계산 순서**: ( )

연산자는 왼쪽된 tooright 평가 하며 hello 동일한 평가 우선 순위입니다. 즉, hello \* (승수) 하기 전에-(빼기) 계산 하지 않습니다. 2\*(5 + 3) 하지 2로 동일 hello은\*5 + 3입니다. hello 괄호 () 사용 되 toochange hello 평가 순서 두면 tooright 평가 순서 적절 하지 않습니다.

## <a name="multi-valued-attributes"></a>다중값 특성
hello 함수는 단일 값 및 다중값 특성에서 작동할 수 있습니다. 다중 값된 특성에 대 한 hello 모든 값에 대해 작동 하 고 적용 합니다 hello tooevery 값 함수 동일 합니다.

예:  
`Trim([proxyAddresses])`Hello / / proxyAddress 특성의 각 값의 Trim을 수행 합니다.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`와 모든 값에 대해는 @-sign, 대체 hello 도메인을 @contoso.com합니다.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Hello SIP 주소 찾아서 hello 값에서 제거 합니다.

## <a name="next-steps"></a>다음 단계
* Hello 구성 모델에 대해 자세히 읽어보세요 [이해 선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md)합니다.
* 참조 방식을 선언적 사용된의 기본의 프로 비전은 [hello 기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md)합니다.
* 선언적 프로비저닝을 사용 하 여 실제 toomake을 변경 하는 방법을 확인할 [어떻게 변경 toohello toomake 기본 구성을](active-directory-aadconnectsync-change-the-configuration.md)합니다.

**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

**참조 항목**

* [Azure AD 동기화 연결: 함수 참조](active-directory-aadconnectsync-functions-reference.md)

