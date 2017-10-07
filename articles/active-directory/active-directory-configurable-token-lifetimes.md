---
title: "Azure Active Directory에서 토큰 수명 aaaConfigurable | Microsoft Docs"
description: "Tooset 수명 토큰에 대 한 Azure AD에서 발급 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Azure Active Directory에서 구성 가능한 토큰 수명(공개 미리 보기)
Azure Active Directory (Azure AD)에서 발급 한 토큰의 hello 수명을 지정할 수 있습니다. 조직의 모든 앱, 다중 테넌트(다중 조직) 응용 프로그램 또는 조직의 특정 서비스 주체에 대해 토큰 수명을 구성할 수 있습니다.

> [!NOTE]
> 이 기능은 현재 공개 미리 보기로 제공되고 있습니다. Toorevert 준비 하거나 변경 내용을 모두 제거 합니다. hello 기능은 공개 미리 보기 기간 동안 모든 Azure Active Directory 구독에서 사용할 수 있습니다. 그러나 hello 기능이 일반 공급 되 면 일부의 hello 기능이 필요할 수 있습니다는 [Azure Active Directory Premium](active-directory-get-started-premium.md) 구독 합니다.
>
>

Azure AD에서 정책 개체는 개별 응용 프로그램 또는 조직의 모든 응용 프로그램에 적용되는 규칙 집합을 나타냅니다. 각 정책 형식에 적용 된 tooobjects toowhich가 할당 되는 속성 집합으로는 고유한 구조가 있습니다.

조직에 대 한 정책을 hello 기본 정책으로 지정할 수 있습니다. hello 정책은 더 높은 우선 순위를 가진 정책에 의해 재정의 되지 않은 상태로 hello 조직에 적용 된 tooany 응용 프로그램입니다. 또한 할당할 수 있습니다 정책 toospecific 응용 프로그램. 우선 순위에 따라 hello 정책 유형에 따라 달라 집니다.


## <a name="token-types"></a>토큰 형식

새로 고침 토큰, 액세스 토큰, 세션 토큰 및 ID 토큰에 대한 토큰 수명 정책을 구성할 수 있습니다.

### <a name="access-tokens"></a>액세스 토큰
액세스를 사용 하는 클라이언트 tooaccess 보호 된 리소스 토큰입니다. 액세스 토큰은 사용자, 클라이언트 및 리소스의 특정 조합에만 사용할 수 있습니다. 액세스 토큰은 해지될 수 없으며 만료될 때까지 유효합니다. 액세스 토큰을 획득한 악의적인 행위자는 수명 범위 동안 이를 사용할 수 있습니다. Hello 수명을 조정 하는 액세스 토큰은 시스템 성능 향상 사이의 절충 하며 증가 hello 클라이언트 hello는 시간의 양을 보유 액세스 hello 사용자 계정을 사용할 수 없습니다. 향상 된 시스템 성능을 낼 수 클라이언트 tooacquire 새 액세스 토큰을 필요한 시간이 hello 수를 줄입니다.

### <a name="refresh-tokens"></a>새로 고침 토큰
클라이언트가 보호 된 리소스는 액세스 토큰 tooaccess 가져오면 hello 클라이언트가 모두 새로 고침 토큰 및 액세스 토큰을 받습니다. hello 새로 고침 토큰 hello 현재 액세스 토큰이 만료 될 때 사용 되는 tooobtain 새로운 액세스/새로 고침 토큰 쌍은입니다. 새로 고침 토큰은 사용자와 클라이언트의 바인딩된 tooa 조합 합니다. 새로 고침 토큰 이며 해지할 수 및 hello 토큰을 사용할 때마다 hello 토큰의 유효성이 검사 됩니다.

것이 중요 한 toomake 기밀 클라이언트 및 클라이언트에 공용 구별 합니다. 다양한 유형의 클라이언트에 대한 자세한 내용은 [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1)를 참조하세요.

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>비밀 클라이언트 새로 고침 토큰의 토큰 수명
비밀 클라이언트는 클라이언트 암호(비밀)를 안전하게 저장할 수 있는 응용 프로그램입니다. 악의적인 행위자 아닌 hello 클라이언트 응용 프로그램에서 요청이 들어오는지를 증명할 수 있습니다. 예를 들어 웹 응용 프로그램은 기밀 클라이언트 hello 웹 서버에서 클라이언트 암호를 저장할 수 있기 때문입니다. 따라서 노출되지 않습니다. 이러한 흐름에서 보다 안전한 되므로 hello 발급된 toothese 흐름은 새로 고침 토큰의 기본 수명 `until-revoked`, 정책을 사용 하 여 변경할 수 없습니다 및 자발적 암호 재설정에 취소 되지 것입니다.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>공용 클라이언트 새로 고침 토큰의 토큰 수명

공용 클라이언트는 클라이언트 암호(비밀)를 안전하게 저장할 수 없습니다. 예를 들어 iOS/Android 앱 수 없는 난독 처리 hello 리소스 소유자 로부터 암호 공용 클라이언트의 것으로 간주 됩니다. 정책을 설정할 수 있습니다 리소스에 tooprevent 새로 고침 토큰은 새 액세스/새로 고침 토큰 쌍 하지 못하도록 지정 된 기간 보다 오래 된 공용 클라이언트에서. (toodo이를 사용 하 여 hello 토큰 최대 비활성 시간이 새로 고침 속성입니다.) 정책 tooset hello 새로 고침 토큰을 벗어나는 기간 증명이 더 이상 사용할 수도 없습니다. (toodo이를 사용 하 여 hello 속성 새로 고침 토큰 최대 처리 기간입니다.) Hello 수명의 시기와 빈도 hello 사용자가 자동으로 검색, 공용 클라이언트 응용 프로그램을 사용 하는 경우 대신 필요한 tooreenter 자격 증명, 새로 고침 토큰 toocontrol 조정할 수 있습니다.

### <a name="id-tokens"></a>ID 토큰
ID 토큰 toowebsites 및 네이티브 클라이언트에 전달 됩니다. ID 토큰은 사용자에 대한 프로필 정보를 포함합니다. ID 토큰은 사용자와 클라이언트의 바인딩된 tooa 특정 조합 합니다. ID 토큰은 만료될 때까지 유효한 것으로 간주됩니다. 웹 응용 프로그램에서 사용자를 일치 하는 일반적으로 hello ID 토큰의 hello 응용 프로그램 toohello 수명에서 세션 수명의 hello 사용자에 대해 실행 합니다. ID 토큰 toocontrol 얼마나 자주 hello 응용 프로그램 세션 및 (자동으로 또는 대화형)을 Azure AD와 다시 인증할 hello 사용자 toobe 필요 얼마나 자주 hello 웹 응용 프로그램 만료 됨의 hello 수명을 조정할 수 있습니다.

### <a name="single-sign-on-session-tokens"></a>Single Sign-On 세션 토큰
사용자를 Azure AD를 인증 하 고 선택 하는 hello **로그인 상태 유지** 확인란을 hello 사용자의 브라우저와 Azure AD는 single sign-on (SSO) 설정 됩니다. 쿠키의 hello 형태로 hello SSO 토큰이이 세션을 나타냅니다. Note hello SSO 세션 토큰 바인딩된 tooa 특정 리소스/클라이언트 응용 프로그램이 아닙니다. SSO 세션 토큰은 해지 가능하며 사용될 때마다 토큰의 유효성이 검사됩니다.

Azure AD는 두 종류의 SSO 세션 토큰을 사용합니다. 하나는 영구 세션 토큰이고 다른 하나는 비영구 세션 토큰입니다. 영구 세션 토큰 hello 브라우저에서 영구 쿠키로 저장 됩니다. 비영구 세션 토큰은 세션 쿠키로 저장됩니다. (Hello 브라우저를 닫을 때 세션 쿠키 제거 됨 됩니다.)

비영구 세션 토큰의 수명은 24시간입니다. 영구 토큰의 수명은 180일입니다. SSO 세션 토큰의 유효 기간이 내에서 사용 되는 언제 든 지 다른 24 시간 또는 hello 토큰 유형에 따라 180 일 hello 유효 기간 연장 됩니다. 유효 기간 내에 SSO 세션 토큰을 사용하지 않으면 만료된 것으로 간주하여 더 이상 허용되지 않습니다.

정책 tooset hello 시간 초과 hello 세션 토큰은 더 이상 받지 않습니다 hello 첫 번째 세션 토큰 발급 된 후 사용할 수 없습니다. (toodo이를 사용 하 여 hello 세션 토큰의 최대 처리 기간 속성입니다.) 사용자가 필요한 tooreenter 자격 증명을 자동으로 인증을 받은 웹 응용 프로그램을 사용 하는 경우 대신 시기와 빈도 세션 토큰 toocontrol의 hello 수명을 조정할 수 있습니다.

### <a name="token-lifetime-policy-properties"></a>토큰 수명 정책 속성
토큰 수명 정책은 토큰 수명 규칙을 포함하는 정책 개체의 형식입니다. Hello 정책 toocontrol의 hello 속성을 사용 하 여 토큰 수명을 지정 합니다. 설정 된 정책이 hello 시스템 hello 기본 수명 값을 적용 합니다.

### <a name="configurable-token-lifetime-properties"></a>구성 가능한 토큰 수명 속성
| 속성 | 정책 속성 문자열 | 영향 | 기본값 | 최소 | 최대 |
| --- | --- | --- | --- | --- | --- |
| 액세스 토큰 수명 |AccessTokenLifetime |액세스 토큰, ID 토큰, SAML2 토큰 |1시간 |10분 |1일 |
| 새로 고침 토큰 최대 비활성 시간 |MaxInactiveTime |새로 고침 토큰 |14일 |10분 |90일 |
| 단일 단계 새로 고침 토큰 최대 기간 |MaxAgeSingleFactor |새로 고침 토큰(모든 사용자) |Until-revoked |10분 |Until-revoked<sup>1</sup> |
| 다단계 새로 고침 토큰 최대 기간 |MaxAgeMultiFactor |새로 고침 토큰(모든 사용자) |Until-revoked |10분 |Until-revoked<sup>1</sup> |
| 단일 단계 세션 토큰 최대 기간 |MaxAgeSessionSingleFactor<sup>2</sup> |세션 토큰(영구 및 비영구) |Until-revoked |10분 |Until-revoked<sup>1</sup> |
| 다단계 세션 토큰 최대 기간 |MaxAgeSessionMultiFactor<sup>3</sup> |세션 토큰(영구 및 비영구) |Until-revoked |10분 |Until-revoked<sup>1</sup> |

* <sup>1</sup>365 일 hello 길이 제한이 명시적이 특성에 대해 설정할 수 있는 합니다.
* <sup>2</sup>경우 **MaxAgeSessionSingleFactor** hello를 사용 하는이 값을 설정 하지 않으면 **MaxAgeSingleFactor** 값입니다. 두 매개 변수가 설정 된 hello 속성 (까지 해지 된) hello 기본값을 사용 합니다.
* <sup>3</sup>경우 **MaxAgeSessionMultiFactor** hello를 사용 하는이 값을 설정 하지 않으면 **MaxAgeMultiFactor** 값입니다. 두 매개 변수가 설정 된 hello 속성 (까지 해지 된) hello 기본값을 사용 합니다.

### <a name="exceptions"></a>예외
| 속성 | 영향 | 기본값 |
| --- | --- | --- |
| 새로 고침 토큰 최대 기간(해지 정보가 부족한 페더레이션된 사용자에 대해 발급됨<sup>1</sup>) |새로 고침 토큰(해지 정보가 부족한 페더레이션된 사용자에 대해 발급됨<sup>1</sup>) |12시간 |
| 새로 고침 토큰 최대 비활성 시간(비밀 클라이언트에 대해 발급됨) |새로 고침 토큰(비밀 클라이언트에 대해 발급됨) |90일 |
| 새로 고침 토큰 최대 기간(비밀 클라이언트에 대해 발급됨) |새로 고침 토큰(비밀 클라이언트에 대해 발급됨) |Until-revoked |

* <sup>1</sup>없는 경우에 모든 사용자 포함 부족 하 여 해지 정보를 가진 페더레이션 사용자 hello "LastPasswordChangeTimestamp" 특성을 동기화 합니다. 이러한 증명이 사용자가 짧은 최대 처리 기간 AAD toorevoke 토큰을 연결 이전 (예: 변경 된 암호) 자격 증명 길이 해당 hello 사용자 더 자주 tooensure에 다시 확인 해야 tooan 없습니다 tooverify 되어 있기 때문에 계속 해 서 연결 된 토큰 에 좋은 고정 합니다. tooimprove admins 동기화는 확인 해야 하는 테 넌 트가이 환경을 hello "LastPasswordChangeTimestamp" 특성 (설정할 수 있습니다 AADSync 또는 Powershell을 사용 하 여 hello 사용자 개체에).

### <a name="policy-evaluation-and-prioritization"></a>정책 평가 및 우선 순위 지정
수 만들고 토큰 수명 정책 tooa 특정 응용 프로그램, tooyour 조직 및 tooservice 보안 주체를 할당 합니다. 여러 정책을 tooa 특정 응용 프로그램을 적용할 수 있습니다. hello 토큰 수명 정책을 적용 하는 이러한 규칙을 따릅니다.

* 정책을 명시적으로 toohello 서비스 사용자를 할당 하 고, 적용 됩니다.
* 정책이 명시적으로 할당 된 toohello 서비스 사용자 인 경우 hello 서비스 사용자의 toohello 모 조직을 명시적으로 할당 하는 정책이 적용 됩니다.
* 할당 된 정책이 명시적으로 toohello 서비스 사용자 또는 toohello 조직, toohello 응용 프로그램을 할당 하는 hello 정책 적용 됩니다.
* 정책이 없는 toohello 서비스 보안 주체, hello 조직 또는 hello application 개체 hello 기본 값에 할당 된 경우 적용 됩니다. (Hello 표를 참조 [구성 가능한 토큰 수명 속성](#configurable-token-lifetime-properties).)

응용 프로그램 개체 및 서비스 사용자 개체 간의 관계 hello에 대 한 자세한 내용은 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](active-directory-application-objects.md)합니다.

토큰의 유효성은 hello 토큰을 사용 하는 hello 시 계산 됩니다. hello 정책 hello 우선 순위가 가장 높은 액세스 하는 hello 응용 프로그램에 적용이 됩니다.

> [!NOTE]
> 다음은 예제 시나리오입니다.
>
> 사용자가 두 tooaccess 웹 응용 프로그램: 웹 응용 프로그램 A와 웹 응용 프로그램 B
> 
> 요소:
> * 웹 응용 프로그램은 모두 hello에 조직 부모 동일 합니다.
> * 세션 토큰 최대 기간이 8 시간이 토큰 수명 정책 1 hello 모 조직 기본값으로 설정 됩니다.
> * 웹 응용 프로그램 A 일반을 사용 하 여 웹 응용 프로그램 이며 연결 된 tooany 정책을 되지 않습니다.
> * 웹 응용 프로그램 B는 매우 중요한 프로세스에 사용됩니다. 서비스 사용자는 세션 토큰 최대 처리 기간을 30 분에 연결 된 tooToken 수명 정책 2 됩니다.
>
> 오후 12시 hello 사용자가 새 브라우저 세션을 시작할 시도 tooaccess 웹 응용 프로그램 1. hello 사용자 한 리디렉션된 tooAzure AD가 toosign에서 요청 했습니다. Hello 브라우저에서 세션 토큰에 쿠키를 만듭니다. hello 사용자 수 있도록 하는 hello 사용자 tooaccess hello ID 토큰으로 리디렉션된 백 tooWeb 응용 프로그램 A가입니다.
>
> 오후 12 시 15 분 hello 사용자 tooaccess 웹 응용 프로그램 B. hello 브라우저 리디렉션 tooAzure hello 세션 쿠키를 검색 하는 광고를 시도 합니다. 웹 응용 프로그램 B의 서비스 사용자가 연결 된 tooToken 수명 정책 2 하지만 hello 모 조직, 기본값은 토큰 수명 정책 1의 일부 이기도 합니다. 토큰 수명 정책 2 정책 tooservice 연결 된 보안 주체 보다 우선 순위가 더 높은 조직 기본 정책 때문에 적용이 됩니다. hello 세션 토큰이 원래 발급 된 hello 내에서 마지막 30 분 때문에 유효한 간주 됩니다. hello 사용자 액세스 권한을 부여 하는 ID 토큰으로 리디렉션된 백 tooWeb 응용 프로그램 B는입니다.
>
> 오후 1 시에 hello 사용자 시도 tooaccess 웹 응용 프로그램 1. hello 사용자는 리디렉션된 tooAzure AD는입니다. 웹 응용 프로그램 A는 연결 된 tooany 정책 없지만 기본 토큰 수명은 정책 1 있는 조직에서 이기 때문에 해당 정책에 적용 됩니다. 원래 실행 된 hello 내에서 마지막 8 시간 hello 세션 쿠키를 검색 했습니다. hello 사용자가 자동으로 리디렉션된 백 tooWeb 응용 프로그램 A를 새 ID 토큰입니다. hello 사용자가 필요한 tooauthenticate 아닙니다.
>
> Hello 사용자가 나중에 즉시 tooaccess 웹 응용 프로그램 B. hello 사용자는 리디렉션된 tooAzure AD입니다. 이전과 마찬가지로 토큰 수명 정책 2가 적용됩니다. Hello 사용자 프롬프트 tooreenter가 30 분 넘게, hello 토큰이 발급 된 때문에 해당 로그인 자격 증명입니다. 완전히 새로운 세션 토큰 및 ID 토큰이 발급됩니다. hello 사용자 웹 응용 프로그램 2. 액세스할 수 있습니다.
>
>

## <a name="configurable-policy-property-details"></a>구성 가능한 정책 속성 세부 정보
### <a name="access-token-lifetime"></a>액세스 토큰 수명
**문자열:** AccessTokenLifetime

**영향:** 액세스 토큰, ID 토큰

**요약:** 이 정책은 이 리소스에 대한 액세스 및 ID 토큰이 유효한 것으로 간주되는 기간을 제어합니다. 액세스 토큰 또는 오랜 시간에 대 한 악의적인 행위자에서 사용 하 고 ID 토큰의 hello 위험을 완화 시키는 hello 액세스 토큰 수명 속성 감소 합니다. (이러한 토큰을 취소할 수 없습니다.) hello 대신 hello 토큰 교체를 더 자주 toobe 때문에 성능이 나쁜 저하 됩니다.

### <a name="refresh-token-max-inactive-time"></a>새로 고침 토큰 최대 비활성 시간
**문자열:** MaxInactiveTime

**영향:** 새로 고침 토큰

**요약:** 오래 된 새로 고침 토큰 일 수 없습니다 클라이언트가 사용할 수는 더 이상 새 액세스/새로 고침 토큰 쌍 tooretrieve tooaccess이이 리소스를 시도할 때이 정책을 제어 합니다. 새로 고침 토큰이 사용 될 때 새로운 새로 고침 토큰 반환은 일반적으로, 때문에이 정책을 hello 클라이언트 tooaccess 지정 된 기간 동안 hello 동안 hello 현재 새로 고침 토큰을 사용 하 여 모든 리소스를 시도 하는 경우 액세스할 수 없습니다.

이 정책이 사용자에 게 해당 클라이언트 tooreauthenticate tooretrieve 새로운 새로 고침 토큰에서 활성화 되지 않은 요구 합니다.

hello 단일 요소 토큰 최대 처리 기간 보다 더 낮은 값 tooa 및 hello Multi-factor 새로 고침 토큰 최대 처리 기간 속성 hello 토큰 최대 비활성 시간이 새로 고침 속성을 설정 되어야 합니다.

### <a name="single-factor-refresh-token-max-age"></a>단일 단계 새로 고침 토큰 최대 기간
**문자열:** MaxAgeSingleFactor

**영향:** 새로 고침 토큰

**요약:** 이 정책 제어 방법 장기 사용자를 새 새로 고침 토큰 tooget 사용 액세스/새로 고침 토큰 쌍은 마지막 성공적으로 인증 되는 단일 요소에만 사용 하 여 후 합니다. 사용자를 인증 하 고 새로운 새로 고침 토큰도 수신, 후 hello 사용자 지정 하는 hello에 대 한 hello 새로 고침 토큰 흐름을 사용할 수는 시간 기간입니다. (그렇습니다으로 hello 현재 새로 고침 토큰이 해지 되지 않으며 hello 비활성 시간 보다 오래 사용 하지 않는 상태로 있습니다.) 해당 시점에 hello 사용자는 강제 tooreauthenticate tooreceive 새로운 새로 고침 토큰입니다.

Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다. 단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값을 설정 하는 것이 좋습니다 같은 tooor 즉 hello Multi-factor 새로 고침 토큰 최대 처리 기간 속성 보다 낮습니다.

### <a name="multi-factor-refresh-token-max-age"></a>다단계 새로 고침 토큰 최대 기간
**문자열:** MaxAgeMultiFactor

**영향:** 새로 고침 토큰

**요약:** 이 정책 제어 방법 장기 사용자를 새 새로 고침 토큰 tooget 사용 액세스/새로 고침 토큰 쌍은 마지막 인증 된 후 성공적으로 여러 요소를 사용 하 여 합니다. 사용자를 인증 하 고 새로운 새로 고침 토큰도 수신, 후 hello 사용자 지정 하는 hello에 대 한 hello 새로 고침 토큰 흐름을 사용할 수는 시간 기간입니다. (그렇습니다 hello 현재 새로 고침 토큰 해지 되지 않은 고 hello 비활성 시간 보다 오래 사용 되지 않습니다.) 이 시점에서 사용자가 tooreauthenticate tooreceive 새 새로 고침 토큰을 강제 합니다.

Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다. 단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값 같은 tooor hello 단일 요소 새로 고침 토큰 최대 처리 기간 속성 보다 큼을 설정 하는 것이 좋습니다.

### <a name="single-factor-session-token-max-age"></a>단일 단계 세션 토큰 최대 기간
**문자열:** MaxAgeSessionSingleFactor

**영향:** 세션 토큰(영구 및 비영구)

**요약:** 이 정책 기간을 제어 사용자가 새 ID와 세션 토큰은 마지막 성공적으로 인증 되는 단일 요소에만 사용 하 여 후 세션 토큰 tooget를 사용할 수 있습니다. 인증 하 고 새 세션 토큰을 수신 하는 사용자, 후 hello 사용자 지정 하는 hello에 대 한 세션 토큰 흐름 hello를 사용할 수는 시간 기간입니다. (그렇습니다 hello 현재 세션 토큰 해지 되지 않은 하 고 만료 되지 않았습니다.) Hello 기간 동안 지정 후 hello 사용자는 강제 tooreauthenticate tooreceive 새 세션 토큰입니다.

Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다. 단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값 같은 hello 보다 작은 tooor Multi-factor 세션 토큰 최대 처리 기간 속성을 설정 하는 것이 좋습니다.

### <a name="multi-factor-session-token-max-age"></a>다단계 세션 토큰 최대 기간
**문자열:** MaxAgeSessionMultiFactor

**영향:** 세션 토큰(영구 및 비영구)

**요약:** 이 정책 기간을 제어 사용자가 새 ID와 세션 후 토큰 세션 토큰 tooget צ ְ ײ hello 마지막으로 여러 요소를 사용 하 여 성공적으로 인증 합니다. 인증 하 고 새 세션 토큰을 수신 하는 사용자, 후 hello 사용자 지정 하는 hello에 대 한 세션 토큰 흐름 hello를 사용할 수는 시간 기간입니다. (그렇습니다 hello 현재 세션 토큰 해지 되지 않은 하 고 만료 되지 않았습니다.) Hello 기간 동안 지정 후 hello 사용자는 강제 tooreauthenticate tooreceive 새 세션 토큰입니다.

Hello 최대 보존 기간을 줄이면 사용자 tooauthenticate 더 자주 강제로 수행 합니다. 단일 요소 인증 다단계 인증 보다 안전 하지 않은 것 간주 되므로,이 속성 tooa 값 같은 tooor hello 단일 요소 세션 토큰 최대 처리 기간 속성 보다 큼을 설정 하는 것이 좋습니다.

## <a name="example-token-lifetime-policies"></a>토큰 수명 정책 예제
앱, 서비스 주체 및 전체 조직의 토큰 수명을 만들고 관리할 수 있다면 Azure AD에서 다양한 시나리오가 가능합니다. 이 섹션에서는 새 규칙을 적용하는 데 도움이 되는 몇 가지 일반적인 정책 시나리오를 살펴보겠습니다.

* 토큰 수명
* 토큰 최대 비활성 시간
* 토큰 최대 기간

Hello 예제에서 배울 방법:

* 조직의 기본 정책 관리
* 웹 로그인에 대한 정책 만들기
* web API를 호출하는 네이티브 앱에 대한 정책 만들기
* 고급 정책 관리

### <a name="prerequisites"></a>필수 조건
다음 예제는 hello, 업데이트, 링크를 만들고 응용 프로그램, 서비스 사용자 및 조직 전체에 대 한 정책을 삭제 합니다. 새 tooAzure AD 인 경우에 대 한 자세히 배울 것이 좋습니다 [tooget는 Azure AD 테 넌 트](active-directory-howto-tenant.md) 이러한 예제를 진행 하기 전에.  

시작 tooget 단계 hello지 않습니다.

1. Hello를 최신 버전 다운로드 [Azure AD PowerShell 모듈 공개 미리 보기 릴리스에서](https://www.powershellgallery.com/packages/AzureADPreview)합니다.
2. Hello 실행 `Connect` tooyour Azure AD 관리자 계정에에서 toosign 명령입니다. 새 세션을 시작할 때마다 이 명령을 실행합니다.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee 다음 실행된 hello 조직에서 생성 된 모든 정책을 명령입니다. Hello 다음 시나리오에서에서 대부분의 작업 후이 명령을 실행 합니다. Hello 가져오기는 데 도움이 됩니다. 또한 hello 명령을 실행 * * * * 정책입니다.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>예: 조직의 기본 정책 관리
이 예에서는 사용자가 전체 조직에서 로그인하는 빈도를 줄이는 정책을 만듭니다. toodo이 토큰에 대 한 단일 요소 새로 고침을 조직 전체에 적용 되는 토큰 수명 정책을 만듭니다. hello 정책은 조직 및 설정 정책 지문이 아직 없으면 tooeach 서비스 사용자에 적용 된 tooevery 응용 프로그램입니다.

1. 토큰 수명 정책을 만듭니다.

    1.  너무 "까지-해지." hello 단일 요소 새로 고침 토큰 설정 액세스가 취소 될 때까지 hello 토큰 만료 되지 않습니다. 정책 정의 다음 hello를 만듭니다.

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  다음 명령을 hello 실행 toocreate hello 정책:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Hello 정책을 업데이트 합니다.

    이 예제에 설정 된 hello 첫 번째 정책을 서비스에 필요한 만큼 엄격 인지를 결정할 수 있습니다. tooset 프로그램 단일 요소 새로 고침 토큰 tooexpire 2 일 동안에서 실행 다음 명령을 hello:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>예: 웹 로그인에 대한 정책 만들기

이 예제에서는 웹 앱에 더 자주 tooauthenticate 사용자가 요구 하는 정책을 만들 수 있습니다. 이 정책은 hello 수명 hello 액세스/ID 토큰 및 웹 응용 프로그램의 다단계 세션 토큰 toohello 서비스 사용자의 hello 최대 보존 기간을 설정합니다.

1. 토큰 수명 정책을 만듭니다.

    웹 로그인에 대 한이 정책을 hello 액세스/ID 토큰 수명 및 hello 최대 단일 요소 세션 토큰 age tootwo 시간을 설정합니다.

    1.  이 명령을 실행 toocreate hello 정책:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Hello 정책 tooyour 서비스 사용자를 할당 합니다. 또한 tooget hello 해야 **ObjectId** 서비스 사용자의 합니다. 

    1.  toosee 조직의 모든 서비스 사용자를 쿼리할 수 있습니다 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)합니다. 또는 [Azure AD 그래프 탐색기](https://graphexplorer.cloudapp.net/), tooyour Azure AD 계정에에서 로그인 합니다.

    2.  Hello를 보유 하는 경우 **ObjectId** 의 서비스 사용자를 hello 다음 명령을 실행 합니다.

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>예: web API를 호출하는 네이티브 앱에 대한 정책 만들기
이 예제에서는 사용자가 tooauthenticate 덜 자주 요구 하는 정책을 만들 수 있습니다. hello 정책에는 또한 hello 사용자 수 전에 비활성 상태로 유지 hello 사용자 다시 인증 해야 하는 시간의 양을 길어집니다. hello 정책에 적용 된 toohello 웹 API입니다. Hello 네이티브 응용 프로그램 리소스로 hello 웹 API를 요청 하면이 정책이 적용 됩니다.

1. 토큰 수명 정책을 만듭니다.

    1.  웹 API hello 다음 명령을 실행에 대 한 엄격한 정책 toocreate:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Hello 정책 tooyour 웹 API를 할당 합니다. 또한 tooget hello 해야 **ObjectId** 응용 프로그램의 합니다. 앱의 가장 좋은 방법은 toofind hello **ObjectId** 는 toouse hello [Azure 포털](https://portal.azure.com/)합니다.

   Hello를 보유 하는 경우 **ObjectId** hello 다음 명령을 실행 하면 앱의:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>예: 고급 정책 관리
이 예제에서는 몇 가지 정책, toolearn hello 우선 순위 시스템 작동 하는 방법을 만들 수 있습니다. 또한 학습할 수 있는 방법을 toomanage는 적용 된 tooseveral 개체는 여러 정책을 합니다.

1. 토큰 수명 정책을 만듭니다.

    1.  toocreate 설정 하는 단일 요소 새로 고침 토큰 수명 too30 hello 일 전 부터는 hello 다음 명령을 실행 하는 조직 기본 정책:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee 새 정책 및 tooget hello 정책 **ObjectId**실행 hello 다음 명령을:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Hello 정책 tooa 서비스 사용자를 할당 합니다.

    이제 toohello 전체 조직에 적용 되는 정책을 준비 합니다. Toopreserve이 30 일 정책을 특정 서비스 주체에 대 한 원하는 수 있지만 hello 조직 기본 정책 toohello 상한값 "까지-해지."의 변경

    1.  toosee 조직의 모든 서비스 사용자를 쿼리할 수 있습니다 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)합니다. 또는 [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/)에서 Azure AD 계정을 사용하여 로그인합니다.

    2.  Hello를 보유 하는 경우 **ObjectId** 의 서비스 사용자를 hello 다음 명령을 실행 합니다.

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. 집합 hello `IsOrganizationDefault` toofalse 플래그:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. 새로운 조직 기본 정책을 만듭니다.

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    Hello 원래 정책 tooyour 연결 된 서비스 사용자, 있으며 hello 새 정책이 조직의 기본 정책으로 설정 된 수 있습니다. 것이 중요 한 tooremember 정책이 적용 tooservice 주체 조직 기본 정책 보다 우선 순위가 하 합니다.

## <a name="cmdlet-reference"></a>Cmdlet 참조

### <a name="manage-policies"></a>정책 관리

다음 cmdlet toomanage 정책 hello를 사용할 수 있습니다.

#### <a name="new-azureadpolicy"></a>New-AzureADPolicy

새 정책을 만듭니다.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Definition</code> |모든 hello 정책 규칙이 포함 된 화 JSON의 배열입니다. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |문자열 hello 정책 이름입니다. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |True 이면 hello 정책을 hello 조직의 기본 정책으로 설정 합니다. false이면 아무 작업도 수행하지 않습니다. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |정책의 유형입니다. 토큰 수명의 경우 항상 "TokenLifetimePolicy"를 사용합니다. | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[선택 사항] |Hello 정책에 대 한 대체 ID를 설정합니다. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
모든 Azure AD 정책 또는 지정된 정책을 가져옵니다.

```PowerShell
Get-AzureADPolicy
```

| 매개 변수 | 설명 | 예 |
| --- | --- | --- |
| <code>&#8209;Id</code>[선택 사항] |**ObjectId (Id)** 원하는 hello 정책. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
모든 앱과 연결 된 tooa 정책 인 서비스 사용자를 가져옵니다.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** 원하는 hello 정책. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
기존 정책을 업데이트합니다.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** 원하는 hello 정책. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |문자열 hello 정책 이름입니다. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code>[선택 사항] |모든 hello 정책 규칙이 포함 된 화 JSON의 배열입니다. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code>[선택 사항] |True 이면 hello 정책을 hello 조직의 기본 정책으로 설정 합니다. false이면 아무 작업도 수행하지 않습니다. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code>[선택 사항] |정책의 유형입니다. 토큰 수명의 경우 항상 "TokenLifetimePolicy"를 사용합니다. |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[선택 사항] |Hello 정책에 대 한 대체 ID를 설정합니다. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
삭제 hello 정책을 지정 합니다.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** 원하는 hello 정책. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>응용 프로그램 정책
Hello 다음 응용 프로그램 정책에 대 한 cmdlet을 사용할 수 있습니다.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Add-AzureADApplicationPolicy
링크 hello 정책 tooan 응용 프로그램을 지정 합니다.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 응용 프로그램입니다. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** hello 정책입니다. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Tooan 응용 프로그램에 할당 된 hello 정책을 가져옵니다.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 응용 프로그램입니다. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
응용 프로그램에서 정책을 제거합니다.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 응용 프로그램입니다. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** hello 정책입니다. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>서비스 사용자 정책
서비스 주체 정책에 대 한 cmdlet을 다음 hello를 사용할 수 있습니다.

#### <a name="add-azureadserviceprincipalpolicy"></a>Add-AzureADServicePrincipalPolicy
링크 hello 지정한 정책 tooa 서비스 사용자입니다.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 응용 프로그램입니다. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** hello 정책입니다. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
모든 정책 연결 된 toohello 지정된 서비스 보안 주체를 가져옵니다.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 응용 프로그램입니다. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
Hello 정책을 hello 지정된 서비스 보안 주체에서 제거합니다.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 응용 프로그램입니다. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** hello 정책입니다. | `-PolicyId <ObjectId of Policy>` |
