---
title: "Azure Active Directory B2C: 사용자 지정 정책 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C: 사용자 지정 정책

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>사용자 지정 정책이란?

사용자 지정 정책은 Azure AD B2C 테 넌 트의 hello 동작을 정의 하는 구성 파일입니다. 반면 **기본 제공 정책** hello 가장 일반적인 identity, 사용자 지정 정책을 수 작업에 대 한 Azure AD B2C hello 포털에서 미리 정의 된 작업의 거의 무제한을 identity 개발자 toocomplete가 완벽 하 게 편집 합니다. 사용자 지정 정책으로는 사용자에 대 한 오른쪽 및 id 시나리오 toodetermine 계속 읽어 보십시오.

**사용자 지정 정책 편집은 일부 사용자에게만 해당됩니다.** hello 배워야 할 필요성이 요구 하는 hello 시작 시간이 깁니다 하 고 나중에 변경 내용 toocustom 정책을 비슷한 전문 지식을 toomaintain를 해야 합니다. 사용자 지정 정책을 사용하기 전에 먼저 시나리오에 대한 기본 제공 정책을 신중하게 고려해야 합니다.

## <a name="comparing-built-in-policies-and-custom-policies"></a>기본 제공 정책과 사용자 지정 정책 비교

| | 기본 제공 정책 | 사용자 지정 정책 |
|-|-------------------|-----------------|
|대상 사용자 | ID 전문 지식이 있거나 없는 모든 앱 개발자 | ID 전문가: 시스템 통합 서비스, 컨설턴트 및 사내 ID 팀입니다. OpenIDConnect 흐름에 만족하고 ID 공급자와 클레임 기반 인증을 이해합니다. |
|구성 방법 | 사용자에게 친숙한 UI를 사용하는 Azure Portal | XML 파일을 직접 편집 하 고 toohello Azure 포털을 업로드 |
|UI 사용자 지정 | HTML, CSS 및 JScript 지원을 비롯한 전체 UI 사용자 지정(사용자 지정 도메인 필요)<br><br>사용자 지정 문자열을 사용하여 다국어 지원 | 동일 |
| 특성 사용자 지정 | 표준 및 사용자 지정 특성 | 동일 |
|토큰 및 세션 관리 | 사용자 지정 토큰 및 다중 세션 옵션 | 동일 |
|ID 공급자| **현재**: 미리 정의된 로컬, 소셜 공급자<br><br>**이후**: 표준 기반 OIDC, SAML, OAuth | **현재**: 표준 기반 OIDC, OAUTH, SAML<br><br>**이후**: WsFed |
|ID 작업(예제) | 로컬 및 많은 소셜 계정을 사용하여 등록 또는 로그인<br><br>셀프 서비스 암호 재설정<br><br>프로필 편집<br><br>Multi-Factor Auth 시나리오<br><br>토큰 및 세션 사용자 지정<br><br>액세스 토큰 흐름 | Hello 사용자 지정 id 공급자를 사용 하 여 기본 제공 정책으로 동일한 작업을 완료 하거나 사용자 지정 범위를 사용 합니다.<br><br>등록의 hello 시 다른 시스템에서 사용자 프로 비전<br><br>고유한 전자 메일 서비스 공급자를 사용하여 환영 전자 메일 보내기<br><br>B2C 외부 사용자 저장소 사용<br><br>API를 통해 신뢰할 수 있는 시스템을 사용하여 사용자 제공 정보의 유효성 검사 |

## <a name="policy-files"></a>정책 파일

사용자 지정 정책은 하나 또는 여러 XML 형식 파일을 계층적 체인의 다른 tooeach 참조로 표시 됩니다. hello XML 요소 정의: 클레임 스키마를 변환, 콘텐츠 정의 클레임 공급자/기술 프로필 및 다른 요소 중 Userjourney 오케스트레이션 단계를 클레임 합니다.

Hello를 사용 하 여를 세 가지 유형의 정책 파일의 사용 하는 것이 좋습니다.

- **기본 파일**, 대부분의 hello 정의 및 제공 하는 Azure 전체 샘플에 대 한 포함 된 합니다.  최소한의 toothis 파일 toohelp 문제를 쉽게 해결 하는 변경 하 고 정책 장기적인 유지 관리 하는 것이 좋습니다.
- **확장 파일** 테 넌 트에 대 한 고유한 구성 변경 내용을 hello를 보유 하는
- **RP (신뢰 당사자) 파일** hello 단일 작업 중심 파일인 hello 응용 프로그램이 나 서비스 (즉, 신뢰 당사자)에서 직접입니다.  자세한 내용은 정책 파일 정의 hello 문서를 읽어 보세요.  고유한 각 태스크에는 자체 RP 필요 하며 브랜딩 요구 사항에 따라 hello 수 "사용 사례 수가 총 x 응용 프로그램의 총" 수 있습니다.


Azure AD B2C에 대 한 기본 제공 정책 hello 포털 hello 배경 toohello EXTenstions 파일에서 변경 하는 동안에 게 표시 hello RP (신뢰 당사자) 파일에만 hello 개발자 하지만 위에서 설명 하는 hello 3 파일 패턴을 따릅니다.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>사용자 지정 정책을 사용하는 경우 알아야 할 핵심 개념

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Azure의 CIAM(고객 ID 및 액세스 관리) 서비스입니다. hello 서비스에는 다음이 포함 됩니다.

1. 특수 한 용도의 Azure Active Directory의 Microsoft Graph 및 로컬 계정과 페더레이션된 계정에 대 한 사용자 데이터가 들어 있는 통해 액세스할 수 있는 hello 형태로 사용자 디렉터리 
2. Toohello 액세스 **Id 경험 프레임 워크** 사용자 및 엔터티 간의 트러스트를 조정 하 고 identity/액세스 관리 작업 toocomplete 이들 간에 클레임을 전달 
3. 보안 토큰 서비스 (STS) id 토큰, 새로 고침 토큰 및 액세스 토큰 (및 해당 하는 SAML 어설션에)를 발급 하 고 tooprotect 리소스 그 유효성을 검사 합니다.

Azure AD B2C 및 상호 작용 하 id 공급자, 사용자, 다른 시스템 hello 로컬 사용자 디렉터리 시퀀스 tooachieve에 identity 작업 (예: 로그인 사용자를 새 사용자 등록, 암호 재설정). hello 다자간 트러스트를 설정 하 고 다음이 단계를 실행 하는 기본 플랫폼 라고 hello Id 경험 프레임 워크 및 (사용자 여행 또는 트러스트 프레임 워크 정책) 정책을 명시적으로 정의 hello 행위자 hello 동작 hello 프로토콜 및 단계 toocomplete hello 시퀀스입니다.

### <a name="identity-experience-framework"></a>ID 경험 프레임워크

OpenIDConnect, OAuth, SAML, WSFed 및 일부 비표준 형식(예: REST API 기반 시스템 간 클레임 교환)과 같은 표준 프로토콜 형식인 엔터티(광범위하게 클레임 공급자) 간의 신뢰를 조정하는 완전히 구성 가능한 정책 기반이며 클라우드 기반인 Azure 플랫폼입니다. 사용자에 게 친숙 hello I2E 만듭니다, whitelabelled 발생 하는 HTML, CSS 및 jscript를 지원 합니다.  오늘날 hello Id 경험 프레임 워크의 Azure AD B2C 서비스 hello hello 컨텍스트에서만에서 사용할 수 및 관련된 tooCIAM 작업에 대 한 우선 순위를 지정 합니다.

### <a name="built-in-policies"></a>기본 제공 정책

Azure AD B2C tooperform hello 가장 일반적으로 사용 되는 id의 직접 hello 동작 (즉, 사용자 등록, 로그인, 암호 재설정) 작업 및 해당 관계 (Azure AD B2C 미리 정의 하는 신뢰할 수 있는 당사자와 상호 작용 구성 파일을 미리 정의 된 예를 들어 Facebook id 공급자, LinkedIn, Microsoft 계정에서 Google 계정)입니다.  Hello 이후, 일반적으로 Azure Active Directory Premium, ADFS Active Directory와 Salesforce ID 공급자와 같은 hello 엔터프라이즈 영역에 있는 id 공급자의 사용자 지정에 대 한 기본 제공 정책 제공할 수도 있습니다.


### <a name="custom-policies"></a>사용자 지정 정책

Azure AD B2C 테 넌 트의 Id 경험 프레임 워크의 hello 동작을 정의 하는 구성 파일입니다. 사용자 지정 정책은 하나 이상의 XML 파일 (정책 파일 정의 참조) hello Id 경험 프레임 워크는 신뢰 당사자 (예: 응용 프로그램)에 의해 호출 될 때 실행 하는 액세스 가능성입니다. 사용자 지정 정책을 수 작업의 거의 무제한을 identity 개발자 toocomplete로 직접 편집 합니다. 사용자 지정 정책 구성 정의 해야 하는 개발자가 hello 신중 하 게 세부 tooinclude 메타 데이터 끝점에서 신뢰할 수 있는 관계, 정확한 클레임 정의 교환 하 고 각 id 공급자가 필요에 따라 암호, 키 및 인증서를 구성 합니다.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Trustframeworks ID 경험 프레임워크에 대한 정책 파일 정의

### <a name="policy-files"></a>정책 파일

사용자 지정 정책은 하나 또는 여러 XML 형식 파일을 계층적 체인의 다른 tooeach 참조로 표시 됩니다. hello XML 요소 정의: 클레임 스키마를 변환, 콘텐츠 정의 클레임 공급자/기술 프로필 및 다른 요소 중 Userjourney 오케스트레이션 단계를 클레임 합니다.  Hello를 사용 하 여를 세 가지 유형의 정책 파일의 사용 하는 것이 좋습니다.

- **기본 파일**, 대부분의 hello 정의 및 제공 하는 Azure 전체 샘플에 대 한 포함 된 합니다.  최소한의 toothis 파일 toohelp 문제를 쉽게 해결 하는 변경 하 고 정책 장기적인 유지 관리 하는 것이 좋습니다.
- **확장 파일** 테 넌 트에 대 한 고유한 구성 변경 내용을 hello를 보유 하는
- **RP (신뢰 당사자) 파일** hello 단일 작업 중심 파일인 hello 응용 프로그램이 나 서비스 (즉, 신뢰 당사자)에서 직접입니다.  자세한 내용은 정책 파일 정의 hello 문서를 읽어 보세요.  고유한 각 태스크에는 자체 RP 필요 하며 브랜딩 요구 사항에 따라 hello 수 "사용 사례 수가 총 x 응용 프로그램의 총" 수 있습니다.

![정책 파일 형식](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| 정책 파일의 종류 | 예제 파일 이름 | 권장되는 사용 | 상속 원본 |
|---------------------|--------------------|-----------------|---------------|
| 기본 |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Hello 핵심 클레임 스키마, 클레임 변환을, 클레임 공급자 및 Microsoft에서 구성 된 사용자 친구 포함 됩니다.<br><br>최소한의 변경 toothis 파일 만들기 | 없음 |
| 확장(EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | 프로그램 변경 내용을 toohello 기본 파일 형식의 통합<br><br>수정된 클레임 공급자<br><br>수정된 사용자 경험<br><br>사용자 고유의 사용자 지정 스키마 정의 | 기본 파일 |
| 신뢰 당사자(RP) | B2C_1A_sign_up_sign_in.xml| 여기에서 토큰 셰이프 및 세션 설정 변경| Extensions(EXT) 파일 |

### <a name="inheritance-model"></a>상속 모델

응용 프로그램 hello RP 정책 파일을 호출 하는 경우 hello B2C에 Id 경험 프레임 워크 자료에서 다음 확장에서 모든 hello 요소를 추가 하 고 마지막으로 hello RP 정책 파일 tooassemble에서 현재 정책을 실제로 hello.  동일 형식 및 hello RP 파일 이름을 hello 요소 확장을 hello 및 확장 재정의 자료에 우선 합니다.

**기본 제공 정책** Azure AD B2C에 hello 포털 hello 배경 toohello EXTenstions 파일에서 변경 하는 동안에 게 표시 hello RP (신뢰 당사자) 파일에만 hello 개발자 하지만 위에서 설명 하는 hello 3 파일 패턴을 따릅니다.  모든 Azure AD B2C hello Azure B2C 팀의 hello 제어에서 사용 되 고 자주 업데이트 되는 기본 정책 파일을 공유 합니다.
