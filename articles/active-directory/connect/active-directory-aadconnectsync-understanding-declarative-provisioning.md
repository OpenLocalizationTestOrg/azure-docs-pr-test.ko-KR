---
title: "Azure AD Connect: 선언적 프로비전 이해 | Microsoft Docs"
description: "Hello 선언적 프로비저닝 구성 모델 Azure AD Connect에 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Azure AD Connect 동기화: 선언적 프로비전 이해
이 항목에서는 Azure AD Connect hello 구성 모델을 설명 합니다. 선언적 프로비저닝이 hello 모델 이라고 하 고 toomake를 쉽게 구성 변경 허용 합니다. 이 항목에서 설명하는 여러 가지 항목은 고급이며 대부분의 고객 시나리오에 필요하지 않습니다.

## <a name="overview"></a>개요
선언적 프로비저닝이에 방문 하 여 연결 하는 원본 디렉터리에서 개체를 처리 하 고 원본 tooa 대상에서 hello 개체 및 특성은 변환 하는 방식을 결정 합니다. 개체 동기화 파이프라인에서 처리 하 고 hello 파이프라인은 동일 인바운드 및 아웃 바운드 규칙에 대 한 hello 합니다. 커넥터 공간 toohello 메타 버스에서 인바운드 규칙은 and 아웃 바운드 규칙 hello 메타 버스 tooa 커넥터 공간입니다.

![파이프라인 동기화](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

hello 파이프라인에는 여러 가지 서로 다른 모듈에 있습니다. 각 모듈은 동기화 개체에서 한 가지 개념을 담당합니다.

![파이프라인 동기화](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* 소스, hello 소스 개체
* [범위](#scope), 범위에 있는 모든 동기화 규칙을 찾습니다.
* [조인](#join), 커넥터 공간과 메타버스 간의 관계를 결정합니다.
* [변환](#transform), 특성을 변환하는 방법 및 흐름을 계산합니다.
* [우선 순위](#precedence), 특성 기여의 충돌을 해결합니다.
* 대상, hello 대상 개체

## <a name="scope"></a>범위
hello 범위 모듈 개체를 평가 하 고 범위에 있으며 hello 처리에 포함 되어야 하는 hello 규칙을 결정 합니다. Hello 개체에 hello 특성 값에 따라 서로 다른 동기화 규칙은 범위에서 평가 toobe 됩니다. 예를 들어 사서함이 없는 비활성화된 사용자에게는 사서함이 있는 활성화된 사용자보다 다양한 규칙이 적용됩니다.  
![범위](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

hello 범위 그룹 및 절으로 정의 됩니다. 그룹 내부의 hello 절은 합니다. 논리적 AND는 그룹의 모든 절 간에 사용됩니다. 예를 들어 (부서 = IT AND 국가 = 덴마크). 논리 OR은 그룹 간에 사용됩니다.

![범위](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
이 그림의 hello 범위도 읽어야 (부서 = IT 및 국가 = 덴마크) 또는 (국가 스웨덴 =) 합니다. 그룹 1 또는 2 그룹 계산된 tootrue 이면 hello 규칙은 범위에 있습니다.

hello 범위 모듈 hello 다음 작업을 지원 합니다.

| 작업 | 설명 |
| --- | --- |
| EQUAL, NOTEQUAL |값이 같으면 toohello 값 hello 특성에서 계산 되는 문자열 비교 합니다. 다중값 특성의 경우 ISIN 및 ISNOTIN를 확인합니다. |
| LESSTHAN, LESSTHAN_OR_EQUAL |값이 계산 되는 문자열 비교를 hello hello 특성 값 보다 작은지 합니다. |
| CONTAINS, NOTCONTAINS |문자열 비교를 값을 찾을 수 어딘가에 값 내 hello 특성의 경우를 계산 합니다. |
| STARTSWITH, NOTSTARTSWITH |Hello 시작 하는 hello व hello 특성의에서 값이 계산 되는 문자열 비교 합니다. |
| ENDSWITH, NOTENDSWITH |Hello 특성에 hello 값의 hello 끝에 값이 계산 되는 문자열 비교 합니다. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |문자열 비교를 값 보다 크면 hello 특성에 hello 값의 경우를 계산 합니다. |
| ISNULL, ISNOTNULL |Hello 특성이 없는 경우 계산에서 hello 개체입니다. Hello 특성이 존재 하지 않으며 따라서 null, 경우 hello 규칙은 범위에 있습니다. |
| ISIN, ISNOTIN |Hello 값이 정의 된 hello 특성에 있는 경우 평가 합니다. 이 작업은 등호 및 NOTEQUAL의 hello 다중값된 변형 합니다. hello 특성은 toobe 다중값된 특성 및 hello 특성 값 중 하나에 hello 값을 찾을 수, 하는 경우 다음 hello 규칙은 범위에 합니다. |
| ISBITSET, ISNOTBITSET |특정 비트가 설정되었는지 평가합니다. 예를 들어 수 사용된 tooevaluate toosee userAccountControl의에서 비트를 hello 사용자 활성화 하거나 비활성화 하는 경우. |
| ISMEMBEROF, ISNOTMEMBEROF |hello 값 DN tooa 그룹 hello 커넥터 공간에 포함 되어야 합니다. Hello 개체에 지정한 hello 그룹의 멤버인 경우 hello 규칙이 범위입니다. |

## <a name="join"></a>Join
hello 동기화 파이프라인 hello 조인 모듈은 hello 대상에서 hello hello 원본에서 hello 개체와 개체 관계를 찾는 작업을 담당 합니다. 인바운드 규칙에서이 관계는 관계 tooan 개체 hello 메타 버스에서 발견 하 고 커넥터 공간에서 개체 것입니다.  
![cs와 mv 간의 조인](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
개체가 없는 경우는 이미 다른 커넥터에서 만든 hello 메타 버스의 hello 목표는 toosee을 연결 해야 합니다. 예를 들어는 계정-리소스 포리스트 hello 사용자 hello 계정 포리스트에서 해야 hello 리소스 포리스트에서 hello 사용자와 조인 됩니다.

인바운드 규칙 toojoin 커넥터 공간 개체 함께 toohello에 주로 조인은 동일한 메타 버스 개체입니다.

hello 조인이 하나 이상의 그룹으로 정의 됩니다. 그룹 내에 절이 있습니다. 논리적 AND는 그룹의 모든 절 간에 사용됩니다. 논리 OR은 그룹 간에 사용됩니다. hello 그룹은 상위 toobottom에서 순서 대로 처리 됩니다. 한 그룹 hello 대상에서 개체와 정확히 하나의 일치 항목이 발견 되는, 다음 다른 조인 규칙이 평가 됩니다. 0 개 이상의 한 개체가 보다, 처리 toohello 다음 규칙 그룹을 계속 합니다. 이러한 이유로 hello 규칙이 만들어집니다 가장 명시적인의 hello 순서에서 첫 번째 더 hello 끝에 유사 항목입니다.  
![조인 정의](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
이 그림에서 hello 조인은 상위 toobottom에서 처리 됩니다. 첫 번째 hello 동기화 파이프라인 employeeID에 대 한 일치가 있는지 볼 수 있습니다. 그렇지 않은 경우 두 번째 규칙의 hello 볼 경우 hello 계정 이름을 사용 하는 toojoin hello 개체를 결합 될 수 있습니다. 그렇지 않은 경우 일치 하는 중 하나를 hello 세 번째이자 마지막 규칙이 더 유사 항목 일치 하는 사용자의 hello 이름을 사용 하 여 되었습니다.

모든 조인 규칙이 평가 되었고 일치는 정확 하 게 하는 경우 hello **링크 형식** hello에 **설명** 페이지를 사용 합니다. 이 옵션은 너무 설정 하는 경우**프로 비전**, hello 대상에 새 개체가 만들어집니다.  
![프로비전 또는 조인](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

개체에는 범위 내에 조인 규칙이 포함된 하나의 단일 동기화 규칙이 있어야 합니다. 조인이 정의되는 여러 동기화 규칙이 있는 경우 오류가 발생합니다. 우선 순위 사용된 tooresolve 조인 충돌 않습니다. 개체는 hello로 tooflow 특성에 대 한 범위에는 조인 규칙 있어야 같은 인바운드/아웃 바운드 방향입니다. Tooflow 해야 할 경우 인바운드 및 아웃 바운드 toohello 특성 동일한 개체를 인바운드 및 연결을 사용 하는 아웃 바운드 동기화 규칙에 있어야 합니다.

개체 tooa 대상 커넥터 공간 tooprovision를 읽으려고 할 때 특별 한 동작을 포함 하는 아웃 바운드 조인 합니다. hello DN 특성은 사용 되는 toofirst 시도 역방향 조인입니다. 이미 있는 경우 개체에서 사용 하 여 hello 대상 커넥터 공간 hello 동일한 DN hello 개체가 조인 됩니다.

hello 조인 모듈은 범위에 새 동기화 규칙을 제공 하는 경우 한 번만 계산 됩니다. 을 개체에 연결 면 hello 조인 조건을 더 이상 충족 하는 경우에 가입 되지 됩니다. Toodisjoin 개체를 원하는 경우 hello 개체 가입 hello 동기화 규칙 범위에서 이동 해야 합니다.

### <a name="metaverse-delete"></a>메타버스 삭제
메타 버스 개체를 사용 하 여 범위에서 하나의 동기화 규칙은으로 유지 됩니다 **링크 형식** 도**프로 비전** 또는 **스 티 키 조인**합니다. 커넥터 새 tooprovision 허용 되지 않습니다는 스 티 키 조인 사용할 toohello 메타 버스 개체 이지만에 가입 된 경우 삭제 한 hello 원본의 hello 메타 버스 개체를 삭제 하기 전에.

메타버스 개체가 삭제되면 **프로비전** 되도록 표시된 아웃바운드 동기화 규칙과 연결된 모든 개체는 삭제되도록 표시됩니다.

## <a name="transformations"></a>변환
hello 변환은 hello 소스 toohello 대상에서 흐름 특성이 어떻게 사용 되는 toodefine 합니다. hello 흐름 중 하나일 수 있습니다 hello 다음 **형식 흐름**: Direct, 상수 또는 식입니다. 직접 흐름은 추가 변환 없이 그대로 특성 값을 사용합니다. 상수 값 집합 hello 값을 지정 합니다. Hello 선언적 프로비저닝 식 언어 tooexpress hello 변환 해야 방법을 사용 합니다. hello에 hello 식 언어를 찾을 수에 대 한 세부 정보를 hello [선언적 프로비저닝 표현 언어 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) 항목입니다.

![프로비전 또는 조인](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

hello **한 번 적용** 확인란 정의 해당 hello hello 개체를 처음 만들 때만 특성을 설정 해야 합니다. 예를 들어이 구성을 사용 하는 새 사용자 개체에 대 한 초기 암호 tooset 수 있습니다.

### <a name="merging-attribute-values"></a>특성 값 병합
Hello 특성 흐름에 있으면 설정 toodetermine 다중 값된 특성에서 일부의 커넥터 병합할 수 있습니다. hello 기본값은 **업데이트**, 우선 순위가 hello 동기화 규칙 우선 순위가 높은 나타냅니다.

![형식 병합](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

또한 **병합** 및 **MergeCaseInsensitive**가 있습니다. 이러한 옵션을 사용 하면 서로 다른 원본의 toomerge 값입니다. 예를 들어 서로 다른 여러 포리스트의 사용된 toomerge hello 멤버나 proxyAddresses 특성 수 있습니다. 이 옵션을 사용 하는 경우 모든 동기화 규칙 범위에서 개체 hello를 사용 해야 형식 병합 동일 합니다. 한 커넥터의 **업데이트** 및 다른 커넥터의 **병합**을 정의할 수는 없습니다. 시도하면 오류가 발생합니다.

차이 hello **병합** 및 **MergeCaseInsensitive** 는 tooprocess 특성 값을 복제 하는 방법입니다. hello 동기화 엔진이 중복 값이 hello 대상 특성에 삽입 되지 않았는지 확인 합니다. 와 **MergeCaseInsensitive**, toobe 존재 하지 않을 경우 중복 차이가 포함 된 값이 발생 합니다. 예를 들어 나타나지 않습니다 둘 다 "SMTP:bob@contoso.com"및"smtp:bob@contoso.com" hello 대상 특성에서입니다. **병합** hello 정확한 값과 다중값 확인은 대/소문자만 달라는 있을 수 있습니다.

옵션 hello **대체** 동일 hello는 **업데이트**, 사용 되지 않습니다.

### <a name="control-hello-attribute-flow-process"></a>제어 hello 특성 흐름 프로세스
여러 인바운드 동기화 규칙에서 구성 된 toocontribute toohello를가 하는 경우 동일한 메타 버스 특성 다음 우선 순위 사용 되는 toodetermine hello 변경 내용이 적용 됩니다. 가장 높은 우선 순위 (가장 낮은 숫자 값)으로 hello 동기화 규칙 toocontribute hello 값을 하려고 합니다. hello 아웃 바운드 규칙에 대해서도 동일 합니다. 우선 순위가 높은 동기화 규칙 hello wins 있으며 hello 값 toohello 연결된 디렉터리 합니다.

일부 경우에는 값을 제공 하지 않고 hello 동기화 규칙 결정 해야 다른 규칙 동작 방식입니다. 그러한 경우에 사용되는 특수한 리터럴이 몇 가지 있습니다.

인바운드 동기화 규칙에 대 한 리터럴 hello **NULL** 없는 값 toocontribute hello 흐름에 사용 되는 tooindicate 될 수 있습니다. 우선 순위가 낮은 다른 규칙이 값을 적용할 수 있습니다. 규칙이 없습니다. 제공한 값을 hello 메타 버스 특성이 제거 됩니다. 아웃 바운드 규칙에 대 한 경우 **NULL** hello 값 hello 연결 된 디렉터리에서 제거 된 다음 모든 동기화 규칙을 처리 한 후 hello 최종 값은입니다.

리터럴 hello **AuthoritativeNull** 너무 비슷합니다**NULL** 하면서도 더 낮은 우선 순위 규칙이 값에 발생할 수 있음을 hello 차이입니다.

특성 흐름은 또한 **IgnoreThisFlow**를 사용할 수 있습니다. Hello 의미 없는 표시 되는지에서 비슷한 tooNULL는 toocontribute 합니다. hello 차이가 hello 대상에 이미 기존 값 제거 되지 않습니다. 이 hello 특성 흐름 적이 없는 것입니다.

다음은 예제입니다.

*tooAD-사용자 Exchange 하이브리드 아웃* 흐름 hello를 찾을 수 있습니다.  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
이 식으로 읽어야: hello 특성 tooAD Azure AD에서에서 들어오는 hello 사용자 사서함을 Azure AD에 있는 경우. 그렇지 않은 경우에 모두 백 tooActive 디렉터리를 전달 되지 않습니다. 이 경우 ad에서 hello 기존 값을 보관할 때 것입니다.

### <a name="importedvalue"></a>ImportedValue
hello 함수 ImportedValue 다른 모든 함수와 다른 이므로 hello 특성 이름을 대괄호가 아닌 따옴표로 묶어야 합니다.  
`ImportedValue("proxyAddresses")`

일반적으로 동기화 중 특성 아직 내보내지 또는 내보내기 ("맨 위 hello tower") 하는 동안 오류가 수신 되었습니다 하는 경우에 hello 예상 값을 사용 합니다. 인바운드 동기화는 연결된 디렉터리에 아직 도달하지 않은 특성도 결국 도달할 것으로 가정합니다. 경우에 따라 반드시 tooonly hello 연결 된 디렉터리 ("홀로그램 및 델타 import tower")가 확인 하는 값을 동기화 합니다.

Hello 기본적으로이 함수의 예제를 확인할 수 있습니다 동기화 규칙 *에서 from AD – User Common Exchange에서*합니다. 하이브리드 Exchange에서 exchange online 추가 하는 hello 값만 동기화 해야 hello 값 성공적으로 내보냈음을 확인 된 경우:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>우선 순위
여러 동기화 규칙이 시도 하면 toocontribute hello 같은 특성 값 toohello 대상, hello 우선 순위 값이 사용 되는 toodetermine hello 내용을 적용 했습니다. 우선 순위가 가장 낮은 숫자 값을 사용 하는 hello 규칙 충돌이 toocontribute hello 특성을 하려고 합니다.

![형식 병합](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

순서 지정이 사용 되는 toodefine 보다 정확 하 게 될 수 있습니다 흐름 개체의 작은 하위 집합에 대 한 특성입니다. 예를 들어, hello 부족--상자-규칙의 활성화 된 계정에서 특성이 있는지 확인 (**User AccountEnabled**) 다른 계정에서 우선 순위가 있습니다.

커넥터 간에 우선 순위를 정의할 수 있습니다. 있도록 커넥터 더 나은 데이터 toocontribute 값으로 먼저 합니다.

### <a name="multiple-objects-from-hello-same-connector-space"></a>여러 개체에서 동일한 커넥터 공간 hello
여러 개체가 있는 경우 hello에 같은 커넥터 공간의 조인 된 toohello 동일한 메타 버스 개체 우선 순위를 조정 해야 합니다. 범위에 있는 여러 개체의 hello 동일 동기화 규칙을 다음 hello 동기화 엔진을 사용할 수 없을 수 toodetermine 우선 합니다. 그가 소스 개체가 hello 값 toohello 메타 버스에 기여 해야 모호 합니다. Hello 원본의 hello 특성 hello 하는 경우에이 구성은 모호한 것으로 보고 됩니다 동일한 값입니다.  
![여러 개체가 조인 toohello 동일한 mv 개체](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

이 시나리오에서는 hello 동기화 규칙의 toochange hello 범위 hello 소스 개체는 서로 다른 동기화 규칙 범위에 포함 되어 있으므로 필요 합니다. 다른 우선 순위 toodefine 있도록합니다.  
![여러 개체가 조인 toohello 동일한 mv 개체](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>다음 단계
* Hello 식 언어에 대 한 자세한 설명 [선언적 프로비저닝 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)합니다.
* 참조 방식을 선언적 사용된의 기본의 프로 비전은 [hello 기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md)합니다.
* 선언적 프로비저닝을 사용 하 여 실제 toomake을 변경 하는 방법을 확인할 [어떻게 변경 toohello toomake 기본 구성을](active-directory-aadconnectsync-change-the-configuration.md)합니다.
* 사용자 및 연락처에서 함께 작동 방법을 tooread 계속 [사용자 및 연락처 이해](active-directory-aadconnectsync-understanding-users-and-contacts.md)합니다.

**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

**참조 항목**

* [Azure AD 동기화 연결: 함수 참조](active-directory-aadconnectsync-functions-reference.md)
