---
title: "aaaHow tooconfigure single sign on tooan 응용 프로그램 프록시 응용 프로그램 | Microsoft Docs"
description: "신속 하 게 single sign on tooyour 응용 프로그램 프록시 응용 프로그램을 구성 하는 방법"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>어떻게 tooconfigure single sign on tooan 응용 프로그램 프록시 응용 프로그램

Single sign on (SSO)를 통해 사용자가 tooaccess 응용 프로그램 여러 번을 인증 하지 않아도 됩니다. Azure Active Directory에 대해 hello 클라우드에서 hello 단일 인증 toooccur 있으며 hello 서비스나 커넥터 tooimpersonate hello 사용자 toocomplete hello 응용 프로그램에서 추가 인증 챌린지에 모든을 허용 합니다.

## <a name="how-tooconfigure-single-sign-on"></a>어떻게 tooconfigure single sign-on
먼저 tooconfigure SSO, 응용 프로그램은 Azure Active Directory를 통해 사전 인증에 대해 구성 되어 있는지 확인 합니다. toodo이 이동, 너무**Azure Active Directory**  - &gt; **엔터프라이즈 응용 프로그램**  - &gt; **모든 응용 프로그램**  - &gt; 응용 프로그램  **- &gt; 응용 프로그램 프록시**합니다. 이 페이지에서 "사전 인증" hello 표시는 너무 설정 되어 있는지 확인 하 고 필드를 "Azure Active Directory. 

Hello 사전 인증 방법에 대 한 자세한 내용은 hello의 4 단계를 참조 하십시오. [앱 게시 문서](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)합니다.

   ![Azure Portal의 사전 인증 방법](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>응용 프로그램 프록시 응용 프로그램에 대한 Single Sign-On 모드 구성
다음에서 single sign-on의 hello 종류로 구성합니다. hello 로그온 메서드는 사용 하는 어떤 유형의 인증 hello 백 엔드 응용 프로그램에 따라 분류 됩니다. 앱 프록시 응용 프로그램은 세 가지 유형의 로그온을 지원합니다.

-   **암호 기반 로그온**: 암호 기반 로그온 toosign에 사용자 이름 및 암호 필드를 사용 하는 모든 응용 프로그램에 사용할 수 있습니다. 구성 단계는 [암호-SSO 구성 설명서](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications)를 참조하세요.

-   **Windows 통합 인증**: IWA(Windows 통합 인증)를 사용하는 응용 프로그램의 경우 KDC(Kerberos 제한 위임)를 통해 Single Sign-On을 사용할 수 있습니다. Active Directory tooimpersonate 사용자 및 toosend에서 응용 프로그램 프록시 커넥터 사용 권한을 부여 하 고 사용자 대신 토큰을 수신 합니다. Hello에서 KCD를 구성 하는 방법에 대 한 세부 정보를 확인할 수 있습니다 [Single Sign-on KCD 설명서](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)합니다.

-   **헤더 기반 로그온**: 헤더 기반 로그온은 파트너 관계를 통해 활성화되며 몇 가지 추가 구성이 필요합니다. 에 대 한 내용은 hello partnership 및 인증에 대 한 헤더를 사용 하는 single sign on tooan 응용 프로그램을 구성 하기 위한 단계별 지침을 참조 hello [Azure AD 설명서에 대 한 PingAccess](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)합니다.

이러한 각 옵션에 "엔터프라이즈 응용 프로그램" 및 opening hello tooyour 응용 프로그램을 이동 하 여 155633 **Single Sign On** hello 왼쪽된 메뉴에는 페이지입니다. 응용 프로그램을 만들어진 경우 hello 이전 포털에 나타나지 않을 수 있습니다 이러한 옵션을 모두 확인 합니다.

이 페이지에는 추가 로그온 옵션인 연결된 로그온이 있습니다. 응용 프로그램 프록시에서도 지원됩니다. 그러나이 옵션 single sign on toohello 응용 프로그램을 추가 하지 않는 note 합니다. 즉, hello 응용 프로그램에 single sign-on Active Directory Federation Services와 같은 다른 서비스를 사용 하 여 구현 이미 있을 수 있습니다. 

이 옵션을 사용 하면 관리자 toocreate 사용자에 hello 응용 프로그램에 액세스할 때 먼저 도착 하는 링크 tooan 응용 프로그램입니다. 예를 들어 응용 프로그램을 Active Directory Federation Services 2.0을 사용 하 여 tooauthenticate 사용자가 구성을 있으면는 관리자는 hello 액세스 패널에 hello "연결 된 로그온" 옵션 toocreate 링크 tooit을 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.](active-directory-application-proxy-sso-using-kcd.md)
