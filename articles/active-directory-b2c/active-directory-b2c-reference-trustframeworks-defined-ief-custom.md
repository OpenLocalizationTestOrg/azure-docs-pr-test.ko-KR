---
title: "Azure Active Directory B2C: 참조 - 보안 프레임워크 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책 및 hello Id 경험 프레임 워크에 대 한 항목"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Azure AD B2C ID 경험 프레임워크에서 보안 프레임워크 정의

Azure Active Directory B2C hello Id 경험 프레임 워크를 사용 하는 (Azure AD B2C) 사용자 지정 정책은 사용자 조직에 중앙 집중화 된 서비스를 제공 합니다. 이 서비스는 hello 복잡 한 id 페더레이션이 큰 커뮤니티에 관심을 줄입니다. hello 복잡성 감소 tooa 단일 트러스트 관계 및 단일 메타 데이터 교환 됩니다.

Id 경험 프레임 워크 tooenable hello를 사용 하는 azure AD B2C 사용자 지정 정책 있습니다 tooanswer hello 다음 관련 질문:

- Hello 법률, 보안, 개인 정보 및 데이터 보호 정책을 준수 해야 하는 것이 무엇입니까?
- Hello 연락처 란 무엇 이며 공인된 참가자 지정할 hello 프로세스는 누구 인가요?
- Id 정보 공급자 라고도 "클레임 공급자 (")를 공인 hello는 누구 이며 무엇 주기?
- 신뢰 당사자 accredited hello는 (및 필요에 따라 작업 필요)?
- ""Hello 통신 중에 기술 hello 이란 상호 운용성 요구 사항에 대 한 참가자?
- 디지털 id 정보를 교환 하기 위해 수행 해야 하는 hello operational "runtime" 규칙 이란?

tooanswer 이러한 질문 모두를 hello Id 경험 프레임 워크 사용 하 여 hello 신뢰 프레임 워크 (TF)를 사용 하는 Azure AD B2C 사용자 지정 정책을 구성 합니다. 이 구문과 및 제공되는 관련 항목에 대해 살펴보겠습니다.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Hello 신뢰 프레임 워크 및 페더레이션 관리 foundation 이해

hello 신뢰 프레임 워크는 hello id, 보안, 개인 정보 및 데이터 보호 정책 toowhich 관심 있는 커뮤니티 참가자가 따라야의 서 면된 사양입니다.

페더레이션된 ID는 인터넷 규모에서 최종 사용자 ID 보증을 달성하기 위한 기초를 제공합니다. Identity management toothird 파티를 위임 하 여 여러 신뢰 당사자와 최종 사용자에 대 한 단일 디지털 id는 재사용할 수 있습니다.  

Identity 보증 id 공급자 (IdPs)와 특성 공급자 (AtPs) 준수 toospecific 보안, 개인 정보 및 운영 정책 및 사례 필요 합니다.  직접 검사를 수행할 수 없는 경우 신뢰 당사자 (Rp)를 개발 해야 IdPs hello 및 AtPs toowork와 선택한 트러스트 관계.  

이러한 트러스트 관계를 어려운 toocontinue 쌍이 들어 있는 관리 또는 쌍이 들어 있는 네트워크에 연결 하는 데 필요한 hello 기술 메타 데이터 교환을 hello 소비자와 디지털 id 정보는 공급자의 hello 수 증가 .  페더레이션 허브에서는 이러한 문제를 해결하는 데 있어 제한된 성공만 달성했습니다.

### <a name="what-a-trust-framework-specification-defines"></a>보안 프레임워크 사양에서 정의하는 항목
TFs는 각 커뮤니티의 지원을 받고 관심 있는 특정 TF 사양은 준하여 hello Open Identity Exchange (OIX) 신뢰 프레임 워크 모델의 hello linchpins 합니다. 이러한 TF 사양은 다음을 정의합니다.

- **정의 hello 관심 있는 hello 커뮤니티에 대 한 보안 및 개인 정보 메트릭을 hello:**
    - hello 수준의 보증 (부하 분산) 참가자; 제공/필요 예를 들어 정렬된 된 집합의 디지털 id 정보의 hello 신뢰성에 대 한 신뢰도 등급입니다.
    - hello 수준의 보호 (LOP) 참가자; 제공/필요 예를 들어 정렬된 된 집합의 hello 참가자 관심 있는 hello 커뮤니티에 의해 처리 되는 디지털 id 정보 보호에 대 한 신뢰도 등급입니다.

- **참가자가 제공 되 는/필요 여부를 지정 하는 hello 디지털 id 정보 설명은 hello**합니다.

- **hello 기술 정책 생성 및의 디지털 id 정보를 사용 하므로 대 한 부하 분산 및 LOP 측정입니다. 일반적으로 정책 기록 여기에 정책의 범주를 수행 하는 hello 포함 됩니다.**
    - ID 교정 정책(예: *사람의 ID 정보를 얼마나 강력하게 검사하는가?*)
    - 보안 정책(예: *정보 무결성 및 기밀성을 얼마나 강력하게 보호하는가?*)
    - 개인 정보 보호 정책(예: *PII(개인 식별 정보)에 대해 어떤 제어 권한이 사용자에게 있는가?*)
    - 존속성 정책(예: *공급자가 운영을 중단하는 경우 PII 기능의 연속성 및 보호는 어떻게 작동하는가?*)

- **생성 및 사용 디지털 id 정보에 대 한 프로필을 기술 하는 hello 합니다. 이러한 프로필에 포함되는 항목은 다음과 같습니다.**
    - 지정된 LOA에서 디지털 ID 정보를 사용할 수 있는 범위 인터페이스
    - 실시간 상호 운용성에 대한 기술 요구 사항

- **hello 설명은 hello 다양 한 역할 hello 커뮤니티 참가자가 수행 하 고 이러한 역할은 필요한 toofulfill 자격 hello 수 있습니다.**

따라서 TF 사양 제어 관심 있는 hello 커뮤니티의 hello 참가자 간에 id 정보 교환 방법: 신뢰 당사자, id 및 특성 공급자 및 특성 확인자입니다.

TF 사양은 hello 거 버 넌 스 hello 어설션 규제 하는 관심 있는 hello 커뮤니티 및 소비 hello 커뮤니티 내 디지털 id 정보에 대 한 참조로 사용 될 하나 이상의 문서입니다. 문서화 된 정책 집합이 되며 이러한 절차에서 관심 있는 커뮤니티의 구성원 간에 온라인 거래에 사용 되는 hello 디지털 id tooestablish 신뢰 설계 되었습니다.  

즉, TF 사양 커뮤니티에 대 한 실행 가능한 페더레이션된 id 에코 시스템을 만들기 위한 hello 규칙을 정의 합니다.

현재 이러한 접근 방식은의 hello 혜택에 광범위 한 계약이입니다. 없이 스팸은 하는 프레임 워크 사양을 안정형 보증 보안과 개인 정보 보호 특성이 여러 커뮤니티에서 다시 사용할 의미 디지털 id 에코 시스템의 hello 개발을 용이 하 게 신뢰 합니다.

이런 이유로 hello Id 경험 프레임 워크를 사용 하는 Azure AD B2C 사용자 지정 정책 hello 기준의 해당 데이터 표현으로 hello 사양 TF toofacilitate 상호 운용성을 위해 사용 합니다.  

Hello Id 경험 프레임 워크를 활용 하는 azure AD B2C 사용자 지정 정책의 사람 및 컴퓨터가 읽을 수 있는 데이터의 혼합으로 TF 사양을 나타냅니다. 이 모델 (일반적으로 더 중심된 거 버 넌 스도 섹션)의 일부 섹션은 hello 함께 toopublished 보안과 개인 정보 보호 정책 설명서를 참조로 표시 됩니다 (있는 경우)에 관련 절차입니다. 세부 hello 구성 메타 데이터와 런타임 규칙에서 작업 자동화를 쉽게 수행할 수 있는 다른 섹션에 설명 합니다.

## <a name="understand-trust-framework-policies"></a>보안 프레임워크 정책 이해

Hello TF 사양을 구현 측면에서 완벽 하 게 identity 동작 및 환경 제어를 허용 하는 정책 집합을 구성 됩니다.  Hello Id 경험 프레임 워크를 활용 하는 azure AD B2C 사용자 지정 정책 tooauthor 있습니다를 사용 하도록 설정 하 고 정의 하 고 구성할 수 있는 선언적 이러한 정책을 통해 직접 TF을 만듭니다.

- hello 문서 참조 또는 TF toohello 관련 된 hello 커뮤니티의 hello 페더레이션된 id 에코 시스템을 정의 하는 참조 합니다. 이들은 toohello TF 설명서 링크입니다. (미리 정의 된) operational "runtime" 규칙 또는 자동화 및/또는 hello exchange 및 hello 클레임의 사용을 제어 하는 hello 사용자 여정이 hello 합니다. 이러한 사용자 경험은 LOA(및 LOP)와 연결됩니다. 따라서 정책은 다양한 LOA(및 LOP)의 사용자 경험을 포함할 수 있습니다.

- hello id 및 특성 공급자 또는 hello에 대 한 클레임 공급자, 지원 toothem 관련 된 hello (대역) 부하 분산/LOP 인정 함께 이자 및 hello 기술 프로필 hello 커뮤니티에서입니다.

- hello 통합 특성 검증 도구 또는 클레임 공급자입니다.

- 신뢰 당사자 (유추)에 의해 hello 커뮤니티의 hello 합니다.

- 참가자 간 네트워크 통신을 설정 하기 위한 hello 메타 데이터입니다. Hello 기술 프로필과 함께이 메타 데이터는 트랜잭션 tooplumb 중 사용 되는 ""hello 통신 중에 간에 상호 운용이 가능 hello 신뢰 당사자 및 기타 커뮤니티 참가자입니다.

- 있는 경우 프로토콜 변환 hello (예: SAML, OAuth2 WS-페더레이션 및 OpenID Connect).

- hello 인증 요구 사항입니다.

- hello 다단계 오케스트레이션이 있는 경우입니다.

- 모든 hello 클레임을 사용할 수 및 관심 있는 커뮤니티의 매핑 tooparticipants 공유 스키마입니다.

- 모든 hello 클레임이이 컨텍스트, toosustain hello exchange 및 hello 클레임의 사용 가능한 데이터 최소화 hello와 함께 변환 합니다.

- hello 바인딩 및 암호화 합니다.

- hello 클레임 저장소입니다.

### <a name="understand-claims"></a>클레임 이해

> [!NOTE]
> Tooall hello 가능한 유형의 "클레임"으로 교환할 수 있는 id 정보를 집합적으로 언급할: 개인적으로 식별 하는 최종 사용자의 인증 자격 증명, identity 심사, 통신 장치, 물리적 위치에 대 한 클레임 특성 및 등입니다.  
>
> 온라인 트랜잭션을에서 이러한 데이터 아티팩트 되지 않으므로 hello 신뢰 당사자에서 직접 확인할 수 있는 팩트 "hello 용어"클레임"-특성이 아닌"-사용 합니다. 대신 어설션 또는 클레임을 신뢰 당사자는 hello에 대 한 충분 한 신뢰도 toogrant hello 최종 사용자의 요청 된 트랜잭션 개발 해야 하는 팩트에 대 한 일입니다.  
>
> 또한 "클레임" hello Id 경험 프레임 워크를 사용 하는 사용자 지정 정책은 Azure AD B2C 일관 된 방식에 관계 없이 모든 종류의 디지털 id 정보 toosimplify hello exchange 설계 되었기 때문에 여부 hello 기본 hello 용어를 사용 사용자 인증 또는 특성 검색을 위해 프로토콜 정의 됩니다.  마찬가지로, 특정 함수 간의 toodistinguish 원치 않으므로 때 tooidentity 공급자, 특성 공급자 및 특성 확인자 toocollectively "클레임 공급자" 참조 hello 용어를 사용 합니다.   

따라서 이에 따라 신뢰 당사자, ID 및 특성 공급자 및 특성 검증자 간에 ID 정보를 교환하는 방법이 달라집니다. 신뢰 당사자 인증에 어떤 ID 및 특성 공급자가 필요한지를 제어합니다. 상속, *if* 문, 다형성이 있는 특정 응용 프로그램 도메인에 특화된 컴퓨터 언어인 DSL(Domain-Specific Language)로 간주되어야 합니다.

이러한 정책은 TF hello Id 경험 프레임 워크를 활용 하 여 Azure AD B2C 사용자 지정 정책에서 생성 하는 hello의 hello 컴퓨터가 읽을 수 있는 부분으로 구성 됩니다. 모든 hello operational 포함 한 정보를 클레임 공급자의 메타 데이터 및 프로필 기술, 클레임 스키마 정의 클레임 변환 함수 및 채워진 사용자 친구 toofacilitate operational 오케스트레이션에 서를 포함 하 고 자동화 됩니다.  

Toobe 가정 됩니다 *주거 문서* 이므로 가능성이 내용이 hello 정책에 선언 된 hello 적극적인 참여자로 관한 시간이 지남에 따라 변경 됩니다. Hello 약관 참여 하지에 대 한 변경 될 수 있는 hello 가능성이 이기도 합니다.  

페더레이션 설치 및 유지 관리 하 여 다양 한 클레임 공급자/검증 도구에 참여 하거나 (나타내는 hello 커뮤니티)을 그대로 둡니다 대로 신뢰 당사자 트러스트 및 연결 재구성 진행 중인에서 실딩 크게 간소화 hello 정책 집합입니다.

상호 운용성은 또 다른 중요한 문제입니다. 추가 클레임 공급자/검증 도구를 통합 합니다, 그리고 필요한 프로토콜 hello 모든 신뢰 당사자으 나 가능성이 toosupport 때문에 있습니다. 업계 표준 프로토콜을 지원 하 여이 문제를 해결 하는 azure AD B2C 사용자 지정 정책 및 특정 사용자 친구를 적용 하 여 신뢰 당사자 및 속성 공급자를 지원 하지 않는 경우에 요청을 tootranspose hello 동일한 프로토콜입니다.  

사용자 친구 등이 프로토콜 프로필 사용된 tooplumb는 메타 데이터 "에"hello 통신 간에 상호 운용이 가능 hello 신뢰 당사자와 다른 참가자입니다. Operational 런타임 규칙을 적용된 tooidentity 정보 요청/응답 메시지를 교환 hello TF 사양의 일부분으로 게시 된 정책 사용 하 여 준수를 강제 적용에 대 한도 있습니다. 사용자 친구의 hello 아이디어는 주요 toohello 사용자 지정한 hello 사용자 환경 개선. 또한 hello 시스템 hello 프로토콜 수준에서 작동 하는 방법에 대 한 light를 통해.

이것을 토대로에서 신뢰 당사자 응용 프로그램 및 포털과 수은 컨텍스트에 따라 Azure AD B2C 사용자 지정 정책을 호출할 Id 경험 프레임 워크의 특정 정책 hello 이름을 전달 hello 및 활용 정확 하 게 hello 동작 및 정보를 가져옵니다. exchange muss, 난리, 일부 또는 위험 없이 원합니다.
