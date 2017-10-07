---
title: "aaaListing hello Azure Active Directory 응용 프로그램 갤러리에서 응용 프로그램"
description: "Toolist single sign on에서 지 원하는 응용 프로그램의 Azure Active Directory 갤러리 hello 어떻게 | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Hello Azure Active Directory 응용 프로그램 갤러리에서 응용 프로그램 나열
toolist 지 hello에서 single sign on Azure Active Directory와 원하는 응용 프로그램 [Azure AD 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/), hello 응용 프로그램에는 먼저 hello 통합 모드를 다음 중 하나를 tooimplement 필요:

* **OpenID Connect** -OpenID Connect를 사용 하 여 인증을 위해 Azure AD와 직접 통합 하 고 구성에 대 한 Azure AD 동의 API hello 합니다. 통합 시작 하는 경우 응용 프로그램 SAML을 지원 하지 않는 hello 권장 되는 모드입니다.
* **SAML** – 응용 프로그램에 이미 hello SAML 프로토콜을 사용 하 여 hello 기능 tooconfigure 타사 id 공급자가 있습니다.

각 모드에 대한 요구 사항을 나열하면 다음과 같습니다.

## <a name="openid-connect-integration"></a>OpenID Connect 통합
toointegrate 다음 hello Azure AD와 응용 프로그램 [개발자 지침](active-directory-authentication-scenarios.md)합니다. 그런 다음 아래 hello 질문을 완료 하 고 보낼 toowaadpartners@microsoft.com합니다.

* Hello Azure AD 팀 tootest hello 통합 하 여 사용할 수 있는 응용 프로그램과 함께 테스트 테 넌 트 또는 계정에 대 한 자격 증명을 제공 합니다.  
* Azure AD hello 팀 수에 로그인 하 고 hello를 사용 하 여 Azure AD tooyour 응용 프로그램의 인스턴스를 연결 하는 방법에 대 한 지침을 제공 [Azure AD의 승인 프레임 워크](active-directory-integrating-applications.md#overview-of-the-consent-framework)합니다. 
* Tootest single sign on 응용 프로그램과 함께 팀 hello Azure AD에 필요한 추가 지침을 제공 합니다. 
* 아래 hello 정보를 제공 합니다.

> 회사 이름:
> 
> 회사 웹 사이트:
> 
> 응용 프로그램 이름:
> 
> 응용 프로그램 설명(200자 제한):
> 
> 응용 프로그램 웹 사이트 (정보):
> 
> 응용 프로그램 기술 지원 웹 사이트 또는 연락처 정보:
> 
> Https://portal.azure.com hello 응용 프로그램 세부 정보에 나와 있는 것 처럼 같은 hello 응용 프로그램의 응용 프로그램 ID:
> 
> 응용 프로그램 등록 URL을 고객에 toosign 어디로 및/또는 구매 hello 응용 프로그램:
> 
> (에 대 한 사용 가능한 범주 참조 hello Azure Active Directory Marketplace) 아래 나열 된 응용 프로그램 toobe 프로그램에 대 한 toothree 범주를 선택 합니다.
> 
> 응용 프로그램 연결 작은 아이콘(PNG 파일, 45x45px, 단색 배경):
> 
> 응용 프로그램 연결 큰 아이콘(PNG 파일, 215x215px, 단색 배경):
> 
> 응용 프로그램 연결 로고(PNG 파일, 150x122px, 투명 배경색):
> 
> 

## <a name="saml-integration"></a>SAML 통합
SAML 2.0을 지 원하는 모든 앱을 사용 하 여 Azure AD 테 넌 트와 직접 통합 될 수 있습니다 [이러한 지침 tooadd 사용자 지정 응용 프로그램](../active-directory-saas-custom-apps.md)합니다. Azure AD와 응용 프로그램 통합을 작동 하는지 테스트 되 면 다음 정보를 너무 hello 전송할<mailto:waadpartners@microsoft.com>합니다.

* Hello Azure AD 팀 tootest hello 통합 하 여 사용할 수 있는 응용 프로그램과 함께 테스트 테 넌 트 또는 계정에 대 한 자격 증명을 제공 합니다.  
* 설명 된 대로 SAML 로그온 URL, 발급자 URL (엔터티 ID), hello 및 회신 URL (어설션 소비자 서비스) 응용 프로그램에 대 한 값을 제공 [여기](../active-directory-saas-custom-apps.md)합니다. 일반적으로 SAML 메타데이터 파일의 일부로 이러한 값을 제공하는 경우 또한 해당 파일을 보냅니다.
* 방법에 대 한 간략 한 설명을 제공 Azure AD SAML 2.0을 사용 하 여 응용 프로그램에 대 한 id 공급자로 tooconfigure 합니다. 응용 프로그램에서 셀프 서비스 관리 포털을 통해를 id 공급자로 구성 Azure AD를 지 원하는 경우 다음 하십시오 위에 제공 된 hello 자격 증명 포함 확인 hello 기능 tooset를이 합니다.
* 아래 hello 정보를 제공 합니다.

> 회사 이름:
> 
> 회사 웹 사이트:
> 
> 응용 프로그램 이름:
> 
> 응용 프로그램 설명(200자 제한):
> 
> 응용 프로그램 웹 사이트 (정보):
> 
> 응용 프로그램 기술 지원 웹 사이트 또는 연락처 정보:
> 
> 응용 프로그램 등록 URL을 고객에 toosign 어디로 및/또는 구매 hello 응용 프로그램:
> 
> 아래 나열 된 응용 프로그램 toobe 프로그램에 대 한 toothree 범주를 선택 (사용 가능한 범주 참조 hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> 응용 프로그램 연결 작은 아이콘(PNG 파일, 45x45px, 단색 배경):
> 
> 응용 프로그램 연결 큰 아이콘(PNG 파일, 215x215px, 단색 배경):
> 
> 응용 프로그램 연결 로고(PNG 파일, 150x122px, 투명 배경색):
> 
> 

