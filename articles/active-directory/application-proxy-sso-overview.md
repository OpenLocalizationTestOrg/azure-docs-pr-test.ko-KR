---
title: "Azure AD 응용 프로그램 프록시에 대 한 SSO aaaManage | Microsoft Docs"
description: "Single sign-on의 응용 프로그램 프록시 hello 기본 사항에 알아보기"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Azure AD 응용 프로그램 프록시에서 Single Sign-On을 제공하는 방법

Single Sign-On은 Azure AD 응용 프로그램 프록시의 핵심 요소입니다.  사용자가 하나만 있으므로 toosign tooAzure hello 클라우드에 Active Directory에에서 hello 최상의 사용자 환경을 제공 합니다. TooAzure Active Directory 인증 되 면 hello 응용 프로그램 프록시 커넥터는 온-프레미스 응용 프로그램을 toohello hello 인증을 처리 합니다. hello 백 엔드 응용 프로그램 도메인에 가입 된 장치에 정상적인 사용 및 응용 프로그램 프록시를 통해 로그인 하는 원격 사용자의 hello 차이 구별할 수 없습니다. 

single sign on tooyour 응용 프로그램에 대 한 Azure Active Directory를 toouse, 해야 tooselect **Azure Active Directory** hello 사전 인증 방법으로 합니다. 선택 하는 경우 **통과** 사용자에 게 전혀 tooAzure Active Directory를 인증 하지 않고 되지만 직선 toohello 방향이 지정 된 응용 프로그램입니다. 먼저 응용 프로그램을 게시 또는 hello Azure 포털에서에서 tooyour 응용 프로그램을 이동 하 고 hello 응용 프로그램 프록시 설정을 편집이 설정을 구성할 수 있습니다. 

toosee single sign on 옵션을 다음이 단계를 수행 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 너무 이동**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**합니다.
3. 해당에서 single sign-on 옵션을 선택 hello 앱 toomanage를 합니다.
4. **Single Sign-On**을 선택합니다.

   ![SSO 드롭다운 메뉴](./media/application-proxy-sso-overview/single-sign-on-mode.png)

hello 드롭다운 메뉴에는 single sign on tooyour 응용 프로그램에 대 한 다섯 가지 옵션이 나와 있습니다.

* Azure AD Single Sign-On 사용 안 함
* 암호 기반 로그온
* 연결된 로그온
* Windows 통합 인증
* 헤더 기반 로그온

## <a name="azure-ad-single-sign-on-disabled"></a>Azure AD Single Sign-On 사용 안 함

Single sign on tooyour 응용 프로그램에 대 한 toouse Azure Active Directory 통합을 사용 하지 않으려는 경우 선택 **Azure AD에서 single sign-on 사용 하지 않도록 설정**합니다. 이 옵션을 선택하면 사용자가 두 번 인증할 수 있습니다. 첫째, tooAzure Active Directory 인증 하 고 toohello 응용 프로그램 자체에 로그인 합니다. 

이 옵션은 온-프레미스 응용 프로그램 사용자 tooauthenticate 필요 하지 않습니다 있지만 원격 액세스에 대 한 보안 계층으로 tooadd Azure Active Directory를 수행 하는 경우에 적합 한 선택 합니다. 

## <a name="password-based-sign-on"></a>암호 기반 로그온

온-프레미스 응용 프로그램에 대 한 Azure Active Directory toouse 암호 자격 증명 모음으로 하려는 경우 선택 **암호 기반 로그온**합니다. 이 옵션은 응용 프로그램에서 액세스 토큰 또는 헤더 대신 사용자 이름/암호 조합을 사용하여 인증하는 경우에 적합한 선택입니다. 암호 기반 로그온 사용자에 게 필요 toosign toohello 응용 프로그램 hello에 처음으로 액세스 하는 날짜입니다. 그 후 Azure Active Directory hello 사용자를 대신 하 여 hello 사용자 이름 및 암호 제공합니다. 

암호 기반 로그온 설정에 대한 내용은 [응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정](application-proxy-sso-azure-portal.md)을 참조하세요.

## <a name="linked-sign-on"></a>연결된 로그온

온-프레미스 ID에 대한 Single Sign-On 솔루션이 이미 설치된 경우 **연결된 로그온**을 선택합니다. 이 옵션을 통해 Azure Active Directory tooleverage 기존 SSO 솔루션 하지만 원격 액세스 toohello 응용 프로그램 사용자가 제공 합니다. 

연결된 로그온(공식적으로 기존 Single Sign-On으로 알려짐)에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)를 참조하세요.

## <a name="integrated-windows-authentication"></a>Windows 통합 인증

온-프레미스 응용 프로그램에서 통합 Windows Authentication(IWA) 사용 또는 single sign on toouse KCD Kerberos 제한 위임 ()를 사용 하려는 경우 선택 **Windows 통합 인증**합니다. 이 옵션을 사용 사용자 권한만 tooauthenticate tooAzure Active Directory 및 그런 다음 응용 프로그램 프록시 커넥터 hello 가장 hello 사용자 tooget Kerberos 토큰 및 toohello 응용 프로그램에 로그인 합니다. 

Windows 통합 인증 설정에 대한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 Kerberos 제한된 위임](active-directory-application-proxy-sso-using-kcd.md)을 참조하세요.

## <a name="header-based-sign-on"></a>헤더 기반 로그온 

응용 프로그램에서 인증에 헤더를 사용하는 경우 **헤더 기반 로그온**을 선택합니다. 이 옵션을 사용 하면 사용자는 Azure Active Directory tooauthentication hello가 필요합니다. 타사 인증 서비스와 Microsoft 파트너 PingAccess hello 응용 프로그램에 대 한 헤더 형식을으로 hello Azure Active Directory 액세스 토큰을 변환 하는 호출 됩니다. 

헤더 기반 인증 설정에 대한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 헤더 기반 인증](application-proxy-ping-access.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

- [응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정](application-proxy-sso-azure-portal.md)
- [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 Kerberos 제한된 위임](active-directory-application-proxy-sso-using-kcd.md)
- [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 헤더 기반 인증](application-proxy-ping-access.md) 
