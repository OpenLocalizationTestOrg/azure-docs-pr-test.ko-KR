---
title: "aaaB2B 공동 작업 사용자 클레임에서 Azure Active Directory로의 매핑을 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에 대한 클레임 매핑 참조"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Azure Active Directory의 B2B 공동 작업 사용자 클레임 매핑

Azure Active Directory (Azure AD) 지원 B2B 공동 작업 사용자에 대 한 hello SAML 토큰에서 발급 된 hello 클레임을 사용자 지정 합니다. Toohello 응용 프로그램을 인증 하는 사용자를 Azure AD는 고유 하 게 식별 하는 hello 사용자에 대 한 정보 (또는 클레임)를 포함 하는 SAML 토큰 toohello 앱을 발급 합니다. 기본적으로 여기에 hello 사용자의 사용자 이름, 전자 메일 주소, 이름 및 성입니다. 있습니다 수 보거나 편집 hello 클레임 hello hello 특성 탭에서 SAML 토큰 toohello 응용 프로그램에에서 전송 합니다.

다음 두 가지 가능한 hello SAML 토큰에서 발급 된 tooedit hello 클레임 할 수 있습니다.

1. hello 응용 프로그램을 썼는지 toorequire 다른 클레임 Uri의 설정 또는 클레임 값

2. 응용 프로그램에 Azure Active Directory에 저장 된 hello 사용자 계정 이름 이외의 hello NameIdentifier 클레임 toobe 필요 합니다.

  ![SAML 토큰의 클레임 보기](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

이 문서에 사용자 지정 클레임, 클레임을 tooadd 및 편집 하는 방법에 대 한 내용은 확인해 [Azure Active Directory에 사전 통합된 앱에 대 한 hello SAML 토큰에서 발급 된 클레임을 사용자 지정](develop/active-directory-saml-claims-customization.md)합니다. B2B 공동 작업 사용자의 경우 보안상의 이유로 테넌트 간 NameID 및 UPN 매핑이 금지됩니다.


## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업용 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
