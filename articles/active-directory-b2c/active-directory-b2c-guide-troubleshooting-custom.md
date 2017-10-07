---
title: "Azure Active Directory B2C: 사용자 지정 정책 문제 해결 | Microsoft Docs"
description: "방법에 알아봅니다 toosolving 오류 Azure Active Directory에서 사용자 지정 정책을 사용 하 여 작업 하는 경우."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Azure AD B2C 사용자 지정 정책 및 Identity Experience Framework 문제 해결

Azure Active Directory B2C를 사용 하는 경우 (Azure AD B2C) 사용자 지정 정책을 정책 언어 XML 형식으로 hello Id 발생할 프레임 워크를 설정 하는 문제를 발생할 수 있습니다.  새로운 언어와 같은 학습 toowrite 사용자 지정 정책을 수 있습니다. 이 문서에서는 문제를 신속하게 검색하고 해결하는 데 유용한 도구와 팁을 설명합니다. 

> [!NOTE]
> 이 문서에서는 Azure AD B2C 사용자 지정 정책 구성의 문제 해결을 중점적으로 다룹니다. 해당 신뢰 당사자 응용 프로그램 또는 identity 라이브러리 hello를 해결 되지 않습니다.

## <a name="xml-editing"></a>XML 편집

hello 가장 일반적인 오류 사용자 지정 정책 설정에 부적절 하 게 XML 서식이 지정 합니다. 좋은 XML 편집기가 거의 필수입니다. 좋은 XML 편집기는 XML을 기본적으로 표시하고, 콘텐츠를 색상으로 구분하며, 일반적인 용어를 미리 채우고, XML 요소를 인덱싱된 상태로 유지하며, 스키마로 유효성을 검사할 수 있습니다. 다음은 권장되는 두 XML 편집기입니다.

* [Contact.java](https://code.visualstudio.com/)
* [메모장++](https://notepad-plus-plus.org/)

XML 파일을 업로드하기 전에 XML 스키마 유효성 검사가 오류를 식별합니다. Hello 스타터 팩 hello 루트 폴더에서 TrustFrameworkPolicy_0.3.0.0.xsd hello XML 스키마 정의 가져옵니다. XML 편집기의 hello 설명서에서 자세한 정보에 대 한 참조 *XML 도구* 및 *XML 유효성 검사*합니다.

XML 규칙 검토가 도움이 될 수도 있습니다. Azure AD B2C는 검색된 XML 형식 오류를 거부합니다. 경우에 따라 형식이 잘못된 XML로 인해 잘못된 오류 메시지가 발생할 수 있습니다.

## <a name="upload-policies-and-policy-validation"></a>정책 업로드 및 정책 유효성 검사

 XML 파일 업로드 유효성 검사는 자동으로 수행됩니다. 대부분의 오류 hello 업로드 toofail을 발생 합니다. 유효성 검사에 업로드 하는 hello 정책 파일에 포함 됩니다. Hello 업로드 파일이 너무 참조 하는 파일의 hello 체인이 포함 됩니다 (신뢰 당사자의 정책 파일, 확장 파일 hello 및 hello 기본 파일 hello). 
 
 일반적인 유효성 검사 오류 hello 다음과를 같습니다.

오류 코드 조각: `... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* hello ClaimType 값, 삭제 또는 hello 스키마에 존재 하지 않습니다.
* ClaimType 값 hello 정책에 hello 파일 중 하나 이상에 정의 되어야 합니다. 
    예: ` <ClaimType Id="socialIdpUserId">`
* ClaimType hello 확장 파일에 정의 된 hello 기본 파일의 TechnicalProfile 값에 사용 되는 표시 되지만 hello 기본 파일을 업로드 하면 오류가 발생 합니다.

오류 코드 조각: `...makes a reference tooa ClaimsTransformation with id...`
* hello 오류 수 수 hello 동일 구문과 hello ClaimType 오류에 대 한 원인을 hello 합니다.

오류 코드 조각: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* 해당 hello hello의 TenantId 값 확인  **\<TrustFrameworkPolicy\>**  및  **\<BasePolicy\>**  요소가 대상 Azure AD B2C 일치 테 넌 트입니다.  

## <a name="troubleshoot-hello-runtime"></a>Hello 런타임 문제 해결

* 사용 하 여 `Run Now` 및 `https://jwt.io` tootest 독립적으로 웹 이나 모바일 응용 프로그램 정책입니다. 이 웹 사이트는 신뢰 당사자 응용 프로그램처럼 작동합니다. JSON 웹 토큰 (JWT) Azure AD B2C 정책에 의해 생성 되는 hello의 hello 내용을 표시 합니다. toocreate 다음 값에 사용 하 여 hello Id 경험 프레임 워크에서 테스트 응용 프로그램:
    * 이름: TestApp
    * 웹앱/Web API: 아니요
    * 네이티브 클라이언트: 아니요

* 클라이언트 브라우저와 Azure AD B2C 사용 간의 메시지 tootrace hello 교환을 [Fiddler](http://www.telerik.com/fiddler)합니다. 오케스트레이션 단계에서 사용자 환경이 실패한 위치를 확인하는 데 도움이 될 수 있습니다.

* **개발 모드**를 사용 하 여 **Application Insights** Id 경험 프레임 워크 사용자 여행의 tootrace hello 활동입니다. **개발 모드**, hello 교환 Id 경험 프레임 워크 hello 포리스트 간에 클레임을 확인할 수 있습니다 및 hello 다양 한 클레임 공급자 API 기반 서비스를 id 공급자와 같은 기술 프로필에 정의 된 Azure AD B2C hello 사용자 디렉터리 및 기타 서비스를 같은 Azure 다중-Factor 인증입니다.  

## <a name="recommended-practices"></a>권장 사례

**여러 버전의 시나리오를 유지하고 응용 프로그램과 함께 프로젝트에 그룹화합니다.** hello 자료, 확장 및 신뢰 당사자 파일 서로에 직접적으로 종속 됩니다. 그룹으로 저장합니다. 새로운 기능 tooyour 정책 추가 되 면 별도 작업 버전을 유지 합니다. 직접 단계 작업 버전 파일 시스템과 상호 작용 하는 hello 응용 프로그램 코드입니다.  응용 프로그램은 테넌트의 여러 다른 신뢰 당사자 정책을 호출할 수 있습니다. Azure AD B2C 정책에서 기대 하는 hello 클레임에 종속 될 수 있습니다.

**알려진 사용자 환경으로 기술 프로필을 개발 및 테스트합니다.** 테스트 거친된 스타터 팩 정책 tooset 기술 프로 파일을 사용 합니다. 고유한 사용자 환경에 통합하기 전에 개별적으로 테스트합니다.

**테스트된 기술 프로필을 통해 사용자 환경을 개발 및 테스트합니다.** 사용자 작업의 hello 오케스트레이션 단계를 증분 방식으로 변경 합니다. 의도한 시나리오를 점진적으로 작성합니다.

## <a name="next-steps"></a>다음 단계

* Github를 hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip).zip 파일을 다운로드 합니다.
