---
title: "Active Directory Id 보호 aaaAzure | Microsoft Docs"
description: "Azure AD Identity Protection을 통해 방법을 공격자가 tooexploit 노출된 된 id의 toolimit hello 능력 또는 장치와 toosecure id 또는 장치 의심 되는 또는 알려진 toobe를 이전에 손상에 대해 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory ID 보호

Azure Active Directory Id 보호는 수 있도록 Azure AD Premium P2 hello 버전의 기능:

- 조직의 ID에 영향을 미치는 잠재적인 취약점을 검색

- 자동화 된 응답이 toodetected 의심 스러운 동작을 관련된 tooyour 조직의 identities 구성  

- 의심 스러운 문제를 조사 하 고 적절 한 조치 tooresolve 수행을   


## <a name="getting-started"></a>시작

Microsoft는 10년 넘게 클라우드 기반 ID를 보호하고 있습니다. Azure Active Directory Id 보호 사용자 환경에서 사용할 수 있습니다 hello 동일한 보호 시스템 Microsoft toosecure identities를 사용 합니다.

공격자는 사용자의 id를 도용 하 여 액세스 tooan 환경 수 hello 포함 된 대부분의 보안 위반 걸릴 놓습니다. Hello 년간 공격자가 되 고 제 3 자 위반을 활용 하 고 정교한 피싱 공격을 사용 하는 효과적인 점점 더 있습니다. 공격자 액세스 tooeven 낮은 권한이 가진된 사용자 계정에는 즉시 해당 측면 확대를 통해 toogain tooimportant 회사 리소스에 액세스에 대 한 비교적 쉽습니다.

이에 따라 다음을 수행해야 합니다.

- 해당 권한 수준에 관계 없이 모든 ID 보호

- 손상된 ID가 남용되지 않도록 사전에 방지

손상된 ID를 검색하는 것은 쉬운 작업이 아닙니다. 적응 기계 학습 알고리즘을 사용 하 여 azure Active Directory 및 추론 toodetect 비정상 보고서 및 잠재적으로 나타내는 의심 스러운 인시던트 손상 identities 합니다. 이 데이터를 사용 하 여 Id 보호는 보고서를 생성 tooevaluate hello를 사용할 수 있는 경고 문제를 발견 했습니다 및 적절 한 완화 또는 재구성 작업을 수행 합니다.

Azure Active Directory ID 보호는 모니터링 및 보고 도구 이상입니다. tooprotect 조직의 id를 지정 된 위험 수준에 도달 했을 때 toodetected 문제를 자동으로 응답 하는 위험 기반 정책을 구성할 수 있습니다. 이러한 정책에서는 또한 tooother 조건부 Azure Active Directory 및 EMS에서 제공 하는 컨트롤에 액세스할 자동으로 차단 하거나 암호 재설정 및 다단계 인증 적용을 포함 한 적응 업데이트 관리 작업을 시작 합니다.


#### <a name="identity-protection-capabilities"></a>ID 보호 기능

**취약점 및 위험 계정 검색:**  

* 사용자 지정 권장 사항을 tooimprove 제공 취약점을 강조 표시 하 여 전반적인 보안 상태
* 로그인 위험 수준 계산
* 사용자 위험 수준 계산


**위험 이벤트 조사:**

* 위험 이벤트에 대한 알림 보내기
* 관련된 컨텍스트 정보를 사용하여 위험 이벤트 조사
* Tootrack 조사 기본 워크플로 제공합니다.
* 쉽게 액세스할 수 tooremediation 암호 다시 설정 하는 등의 작업

**위험 기준 조건부 액세스 정책:**

* 정책 toomitigate 위험한 로그인 하 여 로그인을 차단 하거나 다단계 인증 챌린지를 요구 합니다.
* 정책 tooblock 또는 보안 위험 사용자 계정
* Multi-factor authentication에 대해 정책 toorequire 사용자 tooregister



## <a name="identity-protection-roles"></a>ID 보호 역할

tooload 균형 hello 관리 활동 Id 보호 구현 주위 몇 가지 역할을 할당할 수 있습니다. Azure AD ID 보호는 3가지 디렉터리 역할을 지원합니다.

| 역할                         | 가능한 작업                          | 불가능한 작업
| :--                          | ---                                |  ---   |
| 전역 관리자         | 전체 액세스 tooIdentity 보호, 등록 Id 보호| |
| 보안 관리자       | 전체 액세스 tooIdentity 보호 | ID 보호 등록, 사용자의 암호 재설정 |
| 보안 판독기              | 읽기 전용 액세스 tooIdentity 보호 | ID 보호 등록, 사용자 수정, 정책 구성, 암호 재설정 |




자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)을 참조하세요.



## <a name="detection"></a>감지

### <a name="vulnerabilities"></a>취약점

Azure Active Directory ID 보호는 구성을 분석하고 사용자의 ID에 영향을 줄 수 있는 취약점을 검색합니다. 자세한 내용은 [Azure Active Directory ID 보호에서 검색되는 취약성](active-directory-identityprotection-vulnerabilities.md)을 참조하세요.

### <a name="risk-events"></a>위험 이벤트

Azure Active Directory 적응 컴퓨터 학습 알고리즘 및 추론 toodetect 의심 스러운 동작을 관련된 tooyour 사용자 id를 사용 합니다. hello 시스템이 각 검색 된 의심 스러운 동작에 대 한 레코드를 만듭니다. 이러한 레코드를 위험 이벤트라고도 합니다.  
자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.


## <a name="investigation"></a>조사
일반적으로 시간이 되 셨 Id 보호 hello Identity Protection 대시보드 붙습니다.

![수정](./media/active-directory-identityprotection/1000.png "수정")

hello 대시보드에 액세스할을 수 있습니다.

* **위험 플래그가 지정된 사용자**, **위험 이벤트** 및 **취약성**과 같은 보고서
* 설정의 hello 구성 예: 프로그램 **보안 정책**, **알림** 및 **다단계 인증 등록**

일반적으로 조사는 hello 프로세스 hello 활동, 로그 및 관련된 tooa 위험 이벤트 toodecide 업데이트 관리 또는 완화 단계는 필요 여부는 기타 관련 정보를 검토 하 고, hello identity 어 떠 시작 합니다. hello identity를 노출 하는 방법을 이해 하 고 손상 되 면 사용 되었습니다.

조사 활동 toohello에 연결할 수 있습니다 [알림](active-directory-identityprotection-notifications.md) 전자 메일 당 전송 되는 Azure Active Directory 보호 합니다.

hello 다음 섹션에서는 제공 자세한 내용 및 관련된 tooan 조사 중인 hello 단계.  


## <a name="risky-sign-ins"></a>위험한 로그인

Azure Active Directory는 [위험 이벤트 유형](active-directory-reporting-risk-events.md#risk-event-types)을 실시간 및 오프라인으로 검색합니다. 사용자의 로그인 기능에 대해 검색 된 각 위험 이벤트 위험한 로그인 라는 tooa 논리적 개념을 적용 합니다. 위험한 로그인이 없습니다 수행 되었을 수도 사용자 계정의 hello 정당한 소유자가 로그인 시도에 대 한 표시기입니다.


### <a name="sign-in-risk-level"></a>로그인 위험 수준

로그인 위험 수준을 나타냅니다 (높음, 중간 또는 낮음) hello 가능성의 로그인 시도 하는 사용자 계정의 hello 합법적인 소유자에 의해 수행 되지 않았습니다.

### <a name="mitigating-sign-in-risk-events"></a>로그인 위험 이벤트 완화

완화는 hello id 또는 장치 tooa 안전 상태를 복원 하지 않고 장치나 공격자가 tooexploit 노출된 된 id의 작업 toolimit hello 기능입니다. 한 완화 수단 hello id 또는 장치와 관련 된 이전 로그인 위험 이벤트 확인 되지 않습니다.

toomitigate 위험한 로그인 로그인 위험 보안 policicies 자동으로 구성할 수 있습니다. Hello 사용자 또는 로그인 tooblock hello의 hello 위험 수준을 로그인 위험한 고려 하거나 hello 사용자 tooperform multi-factor authentication 요구 이러한 정책을 사용 하 여, 있습니다. 이러한 작업 하면 공격자가 도난된 identity toocause 손상 악용 하지 않을 수 있으며 시간 toosecure hello id를 제공할 수 있습니다.

### <a name="sign-in-risk-security-policy"></a>로그인 위험 보안 정책
로그인 위험 정책은 hello 위험 tooa 특정 로그인 평가 하 고 미리 정의 된 조건 및 규칙에 따라 완화 기능이 적용 되는 조건부 액세스 정책이입니다.

![로그인 위험 정책](./media/active-directory-identityprotection/1014.png "로그인 위험 정책")

Azure AD Identity Protection 위험한 로그인의 hello 완화 하 여 관리할 수 있습니다.

* Hello 사용자 및 그룹 hello 정책 설정에 적용 됩니다.

    ![로그인 위험 정책](./media/active-directory-identityprotection/1015.png "로그인 위험 정책")
* Hello 로그인 위험 수준 임계값 (낮음, 보통 또는 높음) hello 정책 트리거하는 설정 합니다.

    ![로그인 위험 정책](./media/active-directory-identityprotection/1016.png "로그인 위험 정책")
* 집합 hello 컨트롤 toobe hello 정책을 트리거하면 적용:  

    ![로그인 위험 정책](./media/active-directory-identityprotection/1017.png "로그인 위험 정책")
* 정책 hello 상태 전환:

    ![MFA 등록](./media/active-directory-identityprotection/403.png "MFA 등록")
* 검토 하 고 변경 하기를 활성화 하기 전에 hello 영향을 평가 합니다.

    ![로그인 위험 정책](./media/active-directory-identityprotection/1018.png "로그인 위험 정책")

#### <a name="what-you-need-tooknow"></a>필요한 tooknow
로그인 위험 보안 정책 toorequire multi-factor authentication을 구성할 수 있습니다.

![로그인 위험 정책](./media/active-directory-identityprotection/1017.png "로그인 위험 정책")

그러나 보안상의 이유로 이 설정은 다단계 인증에 이미 등록된 사용자에게만 적용됩니다. Hello 조건 toorequire multi-factor authentication 사용자에 게 multi-factor authentication에 아직 등록 되지 않았습니다 충족 하는 hello 사용자가 차단 됩니다.

모범 사례로, 로그인을 위한 위험한, toorequire 다단계 인증을 사용 하려는 경우 해야 합니다.

1. Hello를 사용 하도록 설정 [다단계 인증 등록 정책](#multi-factor-authentication-registration-policy) hello에 대 한 영향을 받는 사용자입니다.
2. Hello 영향을 받는 사용자 toologin 위험한 비 세션 tooperform에 MFA 등록 필요

이러한 단계를 완료하면 위험한 로그인에 대해 다단계 인증이 요구됩니다.

#### <a name="best-practices"></a>모범 사례
선택는 **높은** 임계값 정책이 트리거되고 hello 영향 toousers 최소화 횟수 hello 수를 줄일 수 있습니다.  

그러나이 메서드를 제외 **낮은** 및 **보통** 공격자가 악용 노출된 된 id를 차단할 수 있는 hello 정책에서 위험에 대 한 플래그가 지정 된 로그인.

설정이 정책을 hello 하는 경우

* 다단계 인증이 없는/있을 수 없는 사용자 제외
* 로캘에서 여기서 hello 정책 사용 불가능 한 사용자를 제외 (예를 들어 없는 액세스 toohelpdesk)
* 가능성이 높은 toogenerate 많이 거짓 긍정 (개발자, 보안 분석가) 인 사용자를 제외 합니다.
* 초기 정책이 롤아웃하는 동안 또는 최종 사용자가 확인하는 과제를 최소화해야 하는 경우 **높음** 임계값을 사용합니다.
* 조직에서 보안을 강화해야 하는 경우 **낮음** 임계값을 사용합니다. **낮은** 임계값을 선택하면 추가 사용자 로그인 과제가 발생하지만 보안이 강화됩니다.

기본 권장 대부분의 조직에 대 한 규칙 tooconfigure을는 hello는 **보통** 임계값 toostrike 보안과 유용성 간의 균형입니다.

hello 로그인 위험 정책은 됩니다.

* 적용 된 tooall 브라우저 트래픽과 최신 인증을 사용 하 여 로그인 합니다.
* ADFS와 같은 페더레이션 hello IDP에서 hello WS-트러스트 끝점을 사용 하지 않도록 설정 하 여 이전 보안 프로토콜을 사용 하 여 적용된 되지 않았습니다. tooapplications 합니다.

hello **위험 이벤트** hello Id 보호 콘솔 페이지에서에서 모든 이벤트를 나열 합니다.

* 이 정책은 다음에 적용되었습니다.
* Hello 활동을 검토 하 고 hello 작업이 적절 한 되었는지 여부를 확인할 수 있습니다.

사용자 환경 관련 hello에 대 한 개요를 참조 합니다.

* [위험한 로그인 복구](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [위험한 로그인 차단됨](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Azure AD ID 보호를 사용하는 로그인 환경](active-directory-identityprotection-flows.md)  

**tooopen hello 관련된 구성 대화 상자**:

- Hello에 **Azure AD Identity Protection** 블레이드 hello **구성** 섹션에서 클릭 **위험 정책을 로그인**합니다.

    ![사용자 위험 정책](./media/active-directory-identityprotection/1014.png "사용자 위험 정책")



## <a name="users-flagged-for-risk"></a>위험에 대한 플래그가 지정된 사용자

모든 활성 [이벤트 위험](active-directory-identity-protection-risk-events.md) 사용자 기여 사용자 위험 라는 tooa 논리적 개념에 대 한 Azure Active Directory에서 검색 되었습니다. 위험 플래그가 지정된 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.

![위험에 대한 플래그가 지정된 사용자](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>사용자 위험 수준

위험 수준의 사용자는 나타냅니다 (높음, 중간 또는 낮음) hello 유사도 hello 사용자의 id가 손상 되었습니다. 사용자의 id와 연결 된 hello 사용자 위험 이벤트로 따라 계산 됩니다.

hello 상태 위험 이벤트는 **활성** 또는 **닫힘**합니다. 만 있는 이벤트의 위험 **활성** 기여 toohello 사용자 위험 수준 계산 합니다.

hello 사용자 위험 수준은 입력 다음 hello를 사용 하 여 계산 됩니다.

* Hello 사용자 영향을 미치는 활성 위험 이벤트
* 이러한 이벤트의 위험 수준
* 수정 작업이 수행되었는지 여부

![사용자 위험](./media/active-directory-identityprotection/1031.png "사용자 위험")

Hello 사용자 위험 수준 toocreate 조건부 액세스 정책의 위험한 사용자 로그인을 차단할 사용 하거나 강제로 할 수 있습니다 toosecurely가 암호를 변경 합니다.

### <a name="closing-risk-events-manually"></a>수동으로 위험 이벤트 닫기

대부분의 경우 보안 암호를 재설정 tooautomatically 닫기 위험 이벤트와 같은 수정 작업을 맡은 것입니다. 그러나 불가능할 수 있습니다.  
이 경우, 예를 들어 hello 경우:

* 활성 위험 이벤트가 있는 사용자가 삭제된 경우
* 조사는 hello 합법적인 사용자가 보고 된 위험 상황을 수행 된 보여 줍니다.

위험 이벤트를는 **활성** toohello 사용자 위험 계산 참가, toomanually 위험 이벤트를 수동으로 닫고 위험 수준을 낮출 수 있습니다.  
조사 hello 과정을 선택할 수 있습니다 tootake 위험 이벤트의 이러한 동작 toochange hello 상태 중 하나:

![작업](./media/active-directory-identityprotection/34.png "작업")

* **해결** -Identity Protection 외부 적절 한 업데이트 관리 작업을 수행한 위험 이벤트를 검토 하 고 해당 hello 위험 이벤트 고려할 닫힌 경우 "해결 됨"로 표시 hello 이벤트 판단 되는 경우. 확인할된 이벤트는 상태 tooClosed hello 위험 이벤트를 설정 하 고 hello 위험 이벤트 toouser 위험 주지 더 이상.
* **가양성으로 표시** - 경우에 따라 위험 이벤트를 조사하여 플래그 지정이 위험으로 잘못 지정되었음을 발견할 수 있습니다. 거짓 긍정으로 hello 위험 이벤트를 표시 하 여 hello 이러한 발생 수를 줄일 수 있습니다. 이 hello 기계 hello 향후의 비슷한 이벤트가 알고리즘 tooimprove hello 분류 학습 도움이 됩니다. hello 거짓 긍정 이벤트 상태가 너무**닫힘** 및 toouser 위험을 더 이상 제공 됩니다.
* **Ignore** -업데이트 관리 작업을 되지 않았을 hello 활성 목록에서 제거 하는 위험 이벤트 toobe hello, 무시 하는 위험 이벤트를 표시할 수 있습니다 및 hello 이벤트 상태 종료 됩니다. 무시 이벤트 toouser 위험을 기여 하지 않습니다. 이 옵션은 이례적인 상황에서만 사용해야 합니다.
* **다시 활성화** -수동으로 종료 된 이벤트를 위험 (선택 하 여 **해결**, **거짓 긍정**, 또는 **무시**) 활성화할 수 hello 설정 이벤트 상태 너무 다시**활성**합니다. 다시 활성화 된 위험 이벤트 toohello 사용자 위험 수준 계산을 영향을 줍니다. 수정(예: 보안 암호를 다시 설정)을 통해 닫힌 위험 이벤트를 다시 활성화할 수 없습니다.

**tooopen hello 관련된 구성 대화 상자**:

1. Hello에 **Azure AD Identity Protection** 블레이드 아래 **조사**, 클릭 **이벤트 위험**합니다.

    ![암호 수동 다시 설정](./media/active-directory-identityprotection/1002.png "암호 수동 다시 설정")
2. Hello에 **이벤트 위험** 목록에서 위험을 클릭 합니다.

    ![암호 수동 다시 설정](./media/active-directory-identityprotection/1003.png "암호 수동 다시 설정")
3. Hello 위험 블레이드에서 사용자를 마우스 오른쪽 단추로 클릭 합니다.

    ![암호 수동 다시 설정](./media/active-directory-identityprotection/1004.png "암호 수동 다시 설정")

### <a name="closing-all-risk-events-for-a-user-manually"></a>사용자에 대한 모든 위험 이벤트를 수동으로 닫기
수동으로 사용자에 대 한 위험 이벤트를 개별적으로 종료, 하는 대신 Azure Active Directory Id 보호도 하면 메서드 tooclose 이벤트를 모두 한 번의 클릭으로 사용자에 대 한 있습니다.

![작업](./media/active-directory-identityprotection/2222.png "작업")

클릭할 때 **이벤트를 모두 해제**, 이벤트를 모두 닫혀 있고 hello 영향을 받는 사용자가 더 이상 위험에 노출 합니다.

### <a name="remediating-user-risk-events"></a>사용자 위험 이벤트 수정

업데이트 관리 작업은 id 또는 이전에 의심 하거나 toobe 알려진 장치를 손상 하는 작업 toosecure입니다. 수정 작업 hello id 또는 장치 tooa 안전 상태를 복원 하 고 hello id 또는 장치와 관련 된 이전 위험 이벤트를 해결 합니다.

tooremediate 사용자 위험 이벤트를 수행할 수 있습니다.

* 보안 된 암호 재설정 tooremediate 사용자 위험 이벤트를 수동으로 수행 합니다.
* 사용자 위험 보안 정책 toomitigate 구성 하거나 사용자 위험 이벤트를 자동으로 재구성
* Hello 감염 된 장치를 이미지로 다시 설치  

#### <a name="manual-secure-password-reset"></a>수동으로 안전한 암호 다시 설정
보안 암호를 재설정 많은 위험 이벤트에 대 한 효과적인 조치가 및 수행 되 면 자동으로 이러한 위험 이벤트를 닫고 hello 사용자 위험 수준 다시 계산 됩니다. Hello Identity Protection 대시보드 tooinitiate 암호 재설정 위험한 사용자에 대해 사용할 수 있습니다.

hello 관련된 대화 상자에서는 두 가지 방법이 tooreset 암호를 제공합니다.

**암호 재설정** -선택 **hello 사용자 tooreset 자신의 암호를 요구** tooallow hello 사용자 tooself 복구 hello 사용자가 multi-factor authentication에 등록 하는 경우. Hello 사용자의 다음에 로그인 하는 동안 hello 사용자는 multi-factor authentication 질문이 성공적으로 필요한 toosolve 및 다음, 강제 toochange hello 암호 됩니다. 이 옵션 hello 사용자 계정이 등록 된 multi-factor authentication이 아닌 경우에 사용할 수 없습니다.

**임시 암호** -선택 **임시 암호가 생성** tooimmediately hello 기존 암호를 무효화 하 고 hello 사용자에 대 한 새 임시 암호를 만듭니다. Hello 새 임시 암호 tooan 대체 전자 메일 주소를 hello 사용자나 toohello 사용자의 관리자에 대 한 보냅니다. Hello 암호 임시 이기 때문에 hello 사용자 로그인 시 증명된 toochange hello 암호가 됩니다.

![정책](./media/active-directory-identityprotection/1005.png "정책")

**tooopen hello 관련된 구성 대화 상자**:

1. Hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **위험에 대 한 플래그가 지정 된 사용자가**합니다.

    ![암호 수동 다시 설정](./media/active-directory-identityprotection/1006.png "암호 수동 다시 설정")
2. 사용자의 hello 목록에서 하나 이상의 위험 이벤트와 사용자를 선택 합니다.

    ![암호 수동 다시 설정](./media/active-directory-identityprotection/1007.png "암호 수동 다시 설정")
3. Hello 사용자 블레이드 클릭 **암호 재설정**합니다.

    ![암호 수동 다시 설정](./media/active-directory-identityprotection/1008.png "암호 수동 다시 설정")

### <a name="user-risk-security-policy"></a>사용자 위험 보안 정책
사용자 위험 보안 정책은 hello 위험 수준 tooa 특정 사용자를 평가 하 고 미리 정의 된 조건 및 규칙에 따라 수정 및 완화 작업을 적용 하는 조건부 액세스 정책을입니다.

![사용자 위험 정책](./media/active-directory-identityprotection/1009.png "사용자 위험 정책")

Azure AD Identity Protection hello 완화 및 수정 하 여 위험에 대 한 플래그가 지정 된 사용자를 관리할 수 있습니다.

* Hello 사용자 및 그룹 hello 정책 설정에 적용 됩니다.

    ![사용자 위험 정책](./media/active-directory-identityprotection/1010.png "사용자 위험 정책")
* Hello 사용자 위험 수준 임계값 (낮음, 보통 또는 높음) hello 정책 트리거하는 설정 합니다.

    ![사용자 위험 정책](./media/active-directory-identityprotection/1011.png "사용자 위험 정책")
* 집합 hello 컨트롤 toobe hello 정책을 트리거하면 적용:

    ![사용자 위험 정책](./media/active-directory-identityprotection/1012.png "사용자 위험 정책")
* 정책 hello 상태 전환:

    ![사용자 위험 정책](./media/active-directory-identityprotection/403.png "MFA 등록")
* 검토 하 고 변경 하기를 활성화 하기 전에 hello 영향을 평가 합니다.

    ![사용자 위험 정책](./media/active-directory-identityprotection/1013.png "사용자 위험 정책")

선택는 **높은** 임계값 정책이 트리거되고 hello 영향 toousers 최소화 횟수 hello 수를 줄일 수 있습니다.
그러나이 메서드를 제외 **낮은** 및 **보통** 수 하지를 보호 하는 id 또는 장치 hello 정책에서 위험에 대 한 플래그가 지정 된 이전에 의심 사용자나 손상 toobe 알려진 합니다.

설정이 정책을 hello 하는 경우

* 가능성이 높은 toogenerate 많이 거짓 긍정 (개발자, 보안 분석가) 인 사용자를 제외 합니다.
* 로캘에서 여기서 hello 정책 사용 불가능 한 사용자를 제외 (예를 들어 없는 액세스 toohelpdesk)
* 초기 정책이 롤아웃하는 동안 또는 최종 사용자가 확인하는 과제를 최소화해야 하는 경우 **높음** 임계값을 사용합니다.
* 조직이 보안을 강화해야 하는 경우 **낮음** 임계값을 사용합니다. **낮은** 임계값을 선택하면 추가 사용자 로그인 과제가 발생하지만 보안이 강화됩니다.

기본 권장 대부분의 조직에 대 한 규칙 tooconfigure을는 hello는 **보통** 임계값 toostrike 보안과 유용성 간의 균형입니다.

사용자 환경 관련 hello에 대 한 개요를 참조 합니다.

* [손상된 계정 복구 흐름](active-directory-identityprotection-flows.md#compromised-account-recovery)  
* [손상된 계정 차단됨 흐름](active-directory-identityprotection-flows.md#compromised-account-blocked)  

**tooopen hello 관련된 구성 대화 상자**:

- Hello에 **Azure AD Identity Protection** 블레이드 hello **구성** 섹션에서 클릭 **사용자 위험 정책**합니다.

    ![사용자 위험 정책](./media/active-directory-identityprotection/1009.png "사용자 위험 정책")

### <a name="mitigating-user-risk-events"></a>사용자 위험 이벤트 완화
관리자는 로그인 시 사용자 위험 보안 정책 tooblock 사용자 hello 위험 수준에 따라 설정할 수 있습니다.

로그인 차단:

* Hello 영향을 받는 사용자에 대 한 새 사용자 위험 이벤트 hello 생성할을 수 없습니다.
* 수 있도록 관리자 toomanually hello 사용자의 id에 영향을 주는 hello 위험 이벤트를 수정 하 고 tooa 보안 상태를 복원



## <a name="multi-factor-authentication-registration-policy"></a>Multi-Factor Authentication 등록 정책
Azure multi-factor authentication은 사용자를 확인 하는 것 이상의 사용자 이름 및 암호 사용 하 여 hello를 해야 하는 방법입니다. 보안 toouser 로그인 및 트랜잭션에 두 번째 계층을 제공합니다.  
다음과 같은 이유로, 사용자 로그인에 Azure Multi-Factor Authentication을 요구하는 것이 좋습니다.

* 다양한 간편한 확인 옵션과 함께 강력한 인증 제공
* 중요 한 역할 조직 tooprotect를 준비 하 고 계정 손상 복구

![사용자 위험 정책](./media/active-directory-identityprotection/1019.png "사용자 위험 정책")

자세한 내용은 [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection 수 있도록 하는 정책을 구성 하 여 hello 롤아웃 multi-factor authentication 등록을 관리할 수 있습니다.

* Hello 사용자 및 그룹 hello 정책 설정에 적용 됩니다.

    ![MFA 정책](./media/active-directory-identityprotection/1020.png "MFA 정책")
* Hello 정책 트리거할 때 적용 하는 집합 hello 컨트롤 toobe::  

    ![MFA 정책](./media/active-directory-identityprotection/1021.png "MFA 정책")
* 정책 hello 상태 전환:

    ![MFA 정책](./media/active-directory-identityprotection/403.png "MFA 정책")
* Hello 현재 등록 상태를 확인 합니다.

    ![MFA 정책](./media/active-directory-identityprotection/1022.png "MFA 정책")

사용자 환경 관련 hello에 대 한 개요를 참조 합니다.

* [Multi-Factor Authentication 등록 흐름](active-directory-identityprotection-flows.md#multi-factor-authentication-registration)  
* [Azure AD ID 보호를 사용하는 로그인 환경](active-directory-identityprotection-flows.md)  

**tooopen hello 관련된 구성 대화 상자**:

- Hello에 **Azure AD Identity Protection** 블레이드 hello **구성** 섹션에서 클릭 **multi-factor authentication 등록**합니다.

    ![MFA 정책](./media/active-directory-identityprotection/1019.png "MFA 정책")

## <a name="next-steps"></a>다음 단계
* [Channel 9: Azure AD 및 ID 표시: ID 보호 미리 보기](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Azure Active Directory ID 보호 활성화](active-directory-identityprotection-enable.md)

* [Azure Active Directory ID 보호에서 검색하는 취약성](active-directory-identityprotection-vulnerabilities.md)

* [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)

* [Azure Active Directory ID 보호 알림](active-directory-identityprotection-notifications.md)

* [Azure Active Directory ID 보호 플레이 북](active-directory-identityprotection-playbook.md)

* [Azure Active Directory ID 보호 용어집](active-directory-identityprotection-glossary.md)

* [Azure AD ID 보호를 사용하는 로그인 환경](active-directory-identityprotection-flows.md)

* [Azure Active Directory Id 보호-어떻게 toounblock 사용자](active-directory-identityprotection-unblock-howto.md)

* [Azure Active Directory ID 보호 및 Microsoft Graph 시작](active-directory-identityprotection-graph-getting-started.md)
