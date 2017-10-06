---
title: "Active Directory Identity 보호 용어 aaaAzure | Microsoft Docs"
description: "Azure Active Directory ID 보호 용어집"
services: active-directory
keywords: "Azure Active Directory ID 보호, Cloud App Discovery, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약성, 보안 정책, 용어집"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Azure Active Directory ID 보호 용어집
### <a name="at-risk-user"></a>위험(사용자)
하나 이상의 활성 위험 이벤트가 있는 사용자입니다. 

### <a name="atypical-sign-in-location"></a>비정상적인 로그인 위치
로그인 hello 특정 사용자, 비슷한 사용자 또는 테 넌 트 hello에 대 한 일반적이 지 않습니다는 지리적 위치에서.

### <a name="azure-ad-identity-protection"></a>Azure AD ID 보호
조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공하는 Azure Active Directory의 보안 모듈입니다.

### <a name="conditional-access"></a>조건부 액세스
액세스 tooresources를 보호 하기 위한 정책입니다. 조건부 액세스 규칙 hello Azure Active Directory에에서 저장 되 고 toohello 리소스 액세스 권한을 부여 하기 전에 Azure AD에 의해 평가 됩니다.  예제 규칙은 사용자 위치, 장치 상태 또는 사용자 인증 방법에 따라 액세스를 제한하게 됩니다.

### <a name="credentials"></a>자격 증명
Id 및 사용 되는 toogain toolocal 및 네트워크 리소스에 액세스는 id 증명이 포함 된 정보입니다. 자격 증명의 예는 사용자 이름 및 암호, 스마트 카드 및 인증서가 있습니다.

### <a name="event"></a>이벤트
Azure Active Directory에서 작업의 기록입니다.

### <a name="false-positive-risk-event"></a>가양성(위험 이벤트)
해당 hello 위험 이벤트를 조사 된 셀과 위험 이벤트로 잘못 표시 되었습니다 나타내는 Id 보호 사용자가을 수동으로 설정 하는 위험 이벤트 상태입니다.

### <a name="identity"></a>ID
암호 또는 인증서와 같은 조건에 따라 인증이라는 방법으로 확인되어야 하는 개인 및 엔터티입니다.

### <a name="identity-risk-event"></a>ID 위험 이벤트
ID 보호에서 비정상으로 플래그가 지정되고 ID가 손상되었음을 나타낼 수 있는 AAD 이벤트입니다.

### <a name="ignored-risk-event"></a>무시된(위험 이벤트)
해당 hello 위험 이벤트 한 수정 작업을 수행 하지 않고 닫혀 나타내는 Id 보호 사용자가을 수동으로 설정 하는 위험 이벤트 상태입니다.

### <a name="impossible-travel-from-atypical-locations"></a>비정상적 위치에서 불가능한 이동
Hello 같은 사용자 검색 되 면 그 중 하나 이상 비정상적인 로그인 위치, 여기서는 hello 간격 hello 로그인은 최소 hello 보다 짧은 시간에 대해 2 회의 로그인 toophysically 수행 되는 경우에 발생 하는 위험 이벤트 간의 이러한 통과 위치입니다.  

### <a name="investigation"></a>조사
hello hello 활동, 로그 및 기타 관련 정보를 검토 하는 프로세스 관련 tooa 위험 이벤트 toodecide 업데이트 관리 또는 완화 단계는 필요 여부를 이해와 hello identity 보안이 손상 되 고 이해 하는 방법을 어떻게 hello 손상 된 id가 사용 되었습니다.

### <a name="leaked-credentials"></a>유출된 자격 증명
현재 사용자 자격 증명 (사용자 이름 및 암호)가 발견 된 경우 발생 하는 위험 이벤트 우리의 연구원에 의해 hello 어두운 웹에 공개적으로 게시 합니다.

### <a name="mitigation"></a>해결 방법
동작 toolimit 또는 hello id 또는 장치 tooa 안전 상태를 복원 하지 않고는 공격자가 tooexploit 노출된 된 id 또는 장치의 hello 기능을 제거 합니다. 한 완화 수단 hello id 또는 장치와 관련 된 이전 위험 이벤트 확인 되지 않습니다.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
이러한 인증서; hello 사용자가 항목을 포함할 수 있는 두 개 이상의 인증 방법이 필요로 하는 인증 방법 사용자 이름, 암호 또는 암호 문구; 같은 hello 사용자가 알고 항목 thumbprint; 등의 물리적 특성 개인 같은 및 특성에 서명 합니다.

### <a name="offline-detection"></a>오프라인 검색
비정상 보고서 및 이미 발생 하는 이벤트에 대 한 hello 팩트 후의 로그인 시도 같은 이벤트의 hello 위험 평가 hello 감지 합니다.

### <a name="policy-condition"></a>정책 조건
Hello 엔터티 (그룹, 사용자, 앱, 장치 플랫폼, 장치 상태, IP 범위, 클라이언트 형식)를 정의 하는 보안 정책이의 일부 hello 정책에 포함 되거나 여기에서 제외 합니다.

### <a name="policy-rule"></a>정책 규칙
hello 정책 및 hello 정책 트리거될 때 수행 하는 hello 작업이 트리거하는 hello 상황을 설명 하는 보안 정책의 hello 부분입니다.

### <a name="prevention"></a>방지
Id 또는 장치 남용을 통해 작업 tooprevent 손상 toohello 조직 의심 또는 손상 toobe 알고 있습니다. 방지 동작은 hello 장치 또는 id를 보호 하지 및 이전 위험 이벤트 확인 되지 않습니다.

### <a name="privileged-user"></a>권한 있는(사용자)
입력과 하는 위험 이벤트의 hello 시 영구 또는 임시 관리 권한 tooone 또는 더 많은 리소스 전역 관리자와 같은 Azure Active Directory 사용자 대금 청구 관리자, 서비스 관리자, 사용자 관리자 및 암호 관리자가입니다. 

### <a name="real-time"></a>실시간
실시간 탐지를 참조하세요.

### <a name="real-time-detection"></a>실시간 탐지
hello 변칙 검색 하 고 hello 이벤트 이전에, 로그인 시도 같은 이벤트의 hello 위험 평가 tooproceed를 허용 됩니다.

### <a name="remediated-risk-event"></a>수정된(위험 이벤트)
나타내는 해당 hello 위험 이벤트 hello 표준 수정 작업을 사용 하 여 이러한 유형의 위험 이벤트에 대 한 재구성 하는 Id 보호에서 자동으로 설정 하는 위험 이벤트 상태입니다. 예를 들어 hello 사용자 암호를 다시 설정할 때 hello 이전 암호가 손상 여부를 나타내는 많은 위험 이벤트 자동으로 치료 됩니다.

### <a name="remediation"></a>재구성
동작 toosecure id 또는 이전에 의심 되거나 toobe 알려진 된 장치를 노출 합니다. 수정 작업 hello id 또는 장치 tooa 안전 상태를 복원 하 고 hello id 또는 장치와 관련 된 이전 위험 이벤트를 해결 합니다.

### <a name="resolved-risk-event"></a>확인된(위험 이벤트)
Hello 사용자가 Id 보호 외부 적절 한 업데이트 관리 작업을 수행 하 고 해당 hello 위험 이벤트를 고려할 수를 나타내는 Id 보호 사용자가을 수동으로 설정 하는 위험 이벤트 상태가 닫힙니다.

### <a name="risk-event-status"></a>위험 이벤트 상태
위험 이벤트의 속성, hello 이벤트가 활성 상태 인지 여부를 나타내는 닫혀 닫기에 대 한 hello 이유.

### <a name="risk-event-type"></a>위험 이벤트 유형
Hello에 대 한 범주 위험이 hello 유형의 위험한 것으로 간주 하는 hello 이벤트 toobe를 발생 시킨 예외를 나타내는 이벤트.

### <a name="risk-level-risk-event"></a>위험 수준(위험 이벤트)
Tooreduce hello 위험 tootheir 조직 가지도록 hello 작업 우선 순위를 지정 하는 hello 위험 이벤트 toohelp Identity Protection 사용자의 hello 심각도 (높음, 중간 또는 낮음) 나타냅니다. 

### <a name="risk-level-sign-in"></a>위험 수준(로그인)
(높음, 중간 또는 낮음)의 표시 hello 가능성은 특정 로그인에 대 한 다른 사용자가 시도 하 toouse hello 사용자의 id입니다.

### <a name="risk-level-user-compromise"></a>위험 수준(사용자 손상)
나타냅니다 (높음, 중간 또는 낮음) id가 손상 된 hello 유사도.

### <a name="risk-level-vulnerability"></a>위험 수준(취약점)
Tooreduce hello 위험 tootheir 조직 가지도록 hello 작업 우선 순위를 지정 하는 hello 취약점 toohelp Identity Protection 사용자의 hello 심각도 (높음, 중간 또는 낮음) 나타냅니다.

### <a name="secure-identity"></a>보안(ID)
암호 변경 또는 잠재적으로 손상 된 identity tooan 손상 되지 않은 상태 toorestore를 이미지로 다시 설치 하는 컴퓨터와 같은 업데이트 관리 작업을 수행 합니다.

### <a name="security-policy"></a>보안 정책
정책 규칙 및 조건의 컬렉션입니다. 정책을 같은 사용자, 그룹, 앱, 장치, 장치 플랫폼, 장치 상태, IP 범위 및 Auth2.0 클라이언트 형식에 적용 된 tooentities 될 수 있습니다. 정책을 사용 하는 hello 정책에 포함 된 엔터티를 리소스에 대 한 토큰을 실행할 때마다 계산 됩니다.

### <a name="sign-in-v"></a>로그인(v)
Azure Active Directory에서 tooauthenticate tooan id입니다.

### <a name="sign-in-n"></a>로그인(n)
hello 프로세스 또는이 작업을 캡처하는 hello 이벤트와 Azure Active Directory id를 인증 하는 동작입니다.

### <a name="sign-in-from-anonymous-ip-address"></a>익명 IP 주소에서 로그인
익명 프록시 IP 주소로 식별된 IP 주소에서 성공적인 로그인 후에 트리거된 위험 이벤트입니다.

### <a name="sign-in-from-infected-device"></a>감염된 장치에서 로그인
위험 이벤트 toobe에서 하나 이상의 손상 된 장치, 봇 서버와 toocommunicate 적극적으로 사용 하는 알려진 IP 주소에서 발생 하 여 로그인 하는 경우에 트리거됩니다.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>의심스러운 동작으로 IP 주소에서 로그인
짧은 기간 동안 여러 사용자 계정에서 여러 번 실패한 로그인을 시도한 IP 주소의 성공적인 로그인 후에 트리거된 위험 이벤트입니다.

### <a name="sign-in-from-unfamiliar-location"></a>알 수 없는 위치에서 로그인
사용자가 새 위치(IP, 위도/경도 및 ASN)에서 성공적으로 로그인한 경우 트리거되는 위험 이벤트입니다.

### <a name="sign-in-risk"></a>로그인 위험
위험 수준(로그인)을 참조하세요.

### <a name="sign-in-risk-policy"></a>로그인 위험 정책
Hello 위험 tooa 특정 로그인 평가 하 고 미리 정의 된 조건 및 규칙에 따라 완화를 적용 하는 조건부 액세스 정책입니다.

### <a name="user-compromise-risk"></a>사용자 손상 위험
위험 수준(사용자 손상)을 참조하세요

### <a name="user-risk"></a>사용자 위험
위험 수준(사용자 손상)을 참조하세요.

### <a name="user-risk-policy"></a>사용자 위험 정책
Hello에 대 한 로그인을 고려 하 여 미리 정의 된 조건 및 규칙에 따라 완화를 적용 하는 조건부 액세스 정책입니다.

### <a name="users-flagged-for-risk"></a>위험에 대한 플래그가 지정된 사용자
활성화되거나 수정된 위험 이벤트를 가진 사용자입니다

### <a name="vulnerability"></a>취약점
구성 또는 hello 디렉터리 취약 tooexploits 또는 위험을 낮추는 Azure Active Directory의 조건입니다.

## <a name="see-also"></a>참고 항목
* [Azure Active Directory ID 보호](active-directory-identityprotection.md)

