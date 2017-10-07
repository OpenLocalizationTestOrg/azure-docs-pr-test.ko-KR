---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하는 개발자 정보 | Microsoft Docs"
description: "사용자 지정 정책으로 Azure AD B2C를 구성 및 유지 관리하는 개발자를 위한 정보"
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
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Azure Active Directory B2C 사용자 지정 정책 공개 미리 보기에 대한 릴리스 정보
hello 사용자 지정 정책 기능 집합은 이제 모든 Azure Active Directory B2C에 대 한 공개 미리 보기에서 평가할 수 없습니다 (Azure AD B2C) 고객 합니다. 이 기능 집합은 hello 가장 복잡 한 id 솔루션을 구축 하는 고급 id 개발자를 대상 합니다.  

현재이 기능 집합에는 XML 파일 편집을 통해 직접 개발자 tooconfigure hello Id 경험 프레임 워크 필요합니다. 이 구성 방법은 강력하고 복잡합니다. Hello를 사용 하 여 identity 개발자가 Id 경험 프레임 워크 계획 해야 tooinvest 약간의 시간이 참조 문서를 읽고 연습을 완료 합니다. 

## <a name="features-included-in-this-public-preview"></a>이 공개 미리 보기에 포함된 기능
Hello 공개 미리 보기에 도입 된 새로운 기능 hello 개발자가 작업을 수행 하는 hello를 수행할 수 있습니다.<br>

* 사용자 지정 정책을 사용하여 사용자 지정 인증 사용자 경험을 작성 및 업로드합니다. 
   * 클레임 공급자 간의 교환으로 사용자 경험을 단계별로 설명합니다. 
   * 사용자 경험에서 조건부 분기를 정의합니다. 
* 사용자 지정 인증 사용자 경험에서 REST API 사용 서비스를 통합합니다.  
* Hello OpenIDConnect 표준 준수 하는 id 공급자와 페더레이션을 추가 합니다. <br>
* Toohello SAML 2.0 프로토콜을 준수 하는 id 공급자와의 페더레이션을 추가 합니다. 

## <a name="terms-of-hello-public-preview"></a>Hello 공개 미리 보기 약관

* 사용자 toouse hello 평가 목적 으로만 사용에 대 한 새로운 기능 좋습니다.<br>
* 새 기능은 프로덕션 환경에서는 사용할 수 없습니다.<br>
* 서비스 수준 계약 (Sla) toohello 새로운 기능을 적용 되지 않습니다. <br>
* 정식 지원 채널을 통해 지원 요청을 정리할 수 있습니다. <br>
* 일반 공급에 대해 정해진 날짜는 없습니다.<br>
* 우리의 판단에 따라 및 어떤 이유로 든 Microsoft 플래그 및 거부 하거나 제한할 수 시나리오 및 고객 id 및 액세스 관리 (CIAM) 플랫폼으로 Azure AD B2C hello 제품 기본 문서 tooserve hello 범위를 초과 하는 사용자 여정이 있습니다.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>사용자 지정 정책 기능 집합 개발자의 책임
수동 정책 구성의 Azure AD B2C 플랫폼 기본 하위 수준의 액세스 toohello 부여 및 hello는 완전히 사용자 지정할 수 있는 고유 트러스트 프레임 워크를 사용 하 여 생성 됩니다. 사용자 지정 id 공급자, 트러스트 관계의 가능한 조합은 외부 서비스 및 단계별 워크플로 통합 요구 사항이 보다 고급 개발자 제네릭을 hello에 배치 합니다.

toofully 혜택 hello 공개 미리 보기에서 것이 좋습니다 hello 정책 사용자 지정 기능 집합을 사용 하는 개발자가 toohello 지침을 따릅니다.
* Hello Identity 경험 엔진의 hello 구성 언어 및 키/암호 관리 익숙해져야 합니다.
* 시나리오 및 사용자 지정 통합을 직접 소유합니다.
* 체계적인 시나리오 테스트를 수행합니다.
* 최소 1개의 개발/테스트 환경과 1개의 프로덕션 환경을 구축하여 소프트웨어 개발 및 스테이징 모범 사례를 준수합니다.
* Hello id 공급자와 통합 하면 서비스에서 새로운 개발에 대 한 정보를 유지 합니다. 예를 들어 유지 비밀의 예약 된 경우와 예약 되지 않은 변경 내용 toohello 서비스의 변경의 추적 합니다.
* 현재 모니터링을 설정 하 고 프로덕션 환경의 hello 응답성을 모니터링 합니다.
* 연락처 전자 메일 주소를 최신으로 유지 하 고 응답 toohello Microsoft 라이브 사이트 팀 전자 메일을 유지 합니다.
* 이 권장된 toodo;에서 Microsoft 라이브 사이트 팀을 hello 때 시기 적절 한 조치를 취해야 합니다. 


>[!NOTE]
>이러한 기능은 tooall 개발자가 보다 쉽게 액세스할 수 있도록 Azure AD 기본 제공 정책에 결국 포함 될 수 있습니다.

## <a name="next-steps"></a>다음 단계
[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md)
