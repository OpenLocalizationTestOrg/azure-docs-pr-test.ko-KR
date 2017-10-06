---
title: "SAML 기반 single sign on tooapplications Azure Active Directory에서 aaaHow toodebug | Microsoft Docs"
description: "자세한 내용은 방법 toodebug SAML 기반 single sign on tooapplications Azure Active Directory에 "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>어떻게 toodebug SAML 기반 single sign on tooapplications Azure Active Directory에
SAML 기반 응용 프로그램 통합을 디버깅할 때 종종 유용한 toouse 도구 이므로 같은 [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML 요청, hello SAML 응답 및 toohello 응용 프로그램에 발급 된 hello 실제 SAML 토큰입니다. Hello SAML 토큰을 검사 하 여 hello의 모든 필수 특성 확인, hello hello SAML 주체에 대 한 사용자 이름 및 발급자 예상 대로 URI를 통해 들어오는 hello 수 있습니다.

![][1]

hello hello SAML 토큰을 포함 하는 Azure AD의 응답은 일반적으로 hello https://login.windows.net에서 HTTP 302 리디렉션 후 발생 하 고 보낸된 toohello 구성 **회신 URL** hello 응용 프로그램입니다. 

이 줄을 선택 하 고 hello를 선택 하 여 hello SAML 토큰을 볼 수 있습니다 **검사자 > WebForms** hello 오른쪽 패널의 탭 합니다. 여기에서 마우스 오른쪽 단추로 클릭 hello **SAMLResponse** 값 및 선택 **tooTextWizard 보낼**합니다. 다음 선택 **에서 Base64** hello에서 **변환** 메뉴 toodecode hello 토큰 및 해당 내용을 확인 합니다.

**참고**: toosee hello 내용의이 HTTP 요청, Fiddler 묻는 메시지를 tooconfigure 암호 해독 해야 HTTPS 트래픽의 toodo 합니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](../active-directory-apps-index.md)
* [Single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성](../active-directory-saas-custom-apps.md)
* [tooCustomize 클레임 발급 방식 hello Pre-Integrated 앱에 대 한 SAML 토큰](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png