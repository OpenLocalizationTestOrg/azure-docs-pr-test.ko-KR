---
title: "Azure AD 응용 프로그램 프록시 aaaSingle 로그온 tooapps | Microsoft Docs"
description: "Single sign on hello Azure 포털에서에서 Azure AD 응용 프로그램 프록시 게시 된 온-프레미스 응용 프로그램에 설정 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정

Azure Active Directory 응용 프로그램 프록시는 원격 직원들이 안전하게 액세스할 수 있도록 온-프레미스 응용 프로그램을 게시하여 생산성을 개선하는 데 도움을 줍니다. Hello Azure 포털에서에서 single sign-on (SSO) toothese 앱을 설정할 수 있습니다. 사용자가 Azure AD와 tooauthenticate 하기만 하 고 다시 toosign 필요 없이 엔터프라이즈 응용 프로그램에 액세스할 수 있습니다.

응용프로그램 프록시에서는 여러 [Single Sign-On 모드](application-proxy-sso-overview.md)를 지원합니다. 암호 기반 로그인은 인증에 사용자 이름/암호 조합을 사용하는 응용 프로그램을 위한 것입니다. 응용 프로그램에 대 한 암호 기반 로그온 구성 하면 사용자가 toohello 온-프레미스 응용 프로그램에서 한 번 toosign 하 게 합니다. 그 후 Azure Active Directory hello 로그인 정보를 저장 하 고 자동으로 제공 toohello 응용 프로그램 사용자가 원격으로 액세스 하는 경우. 

이미 응용 프로그램 프록시를 사용하여 앱을 게시하고 테스트했을 것입니다. 그렇지 않은 경우 hello 단계에 따라 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](application-proxy-publish-azure-portal.md) 여기로 돌아와 야 합니다. 

## <a name="set-up-password-vaulting-for-your-application"></a>응용 프로그램에 대한 암호 보관 설정

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. **Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.
3. Hello 목록에서 sso를 tooset hello 앱을 선택 합니다.  
4. **Single Sign-On**을 선택합니다.

   ![Single Sign-On 선택](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Hello SSO 모드 선택 **암호 기반 로그온**합니다.
6. Hello 로그온 URL에 대 한 URL을 입력 hello hello 페이지에 대 한 사용자가 tooyour 앱 hello 회사 네트워크 외부에서 자신의 사용자 이름 및 암호 toosign를 입력 합니다. 이 응용 프로그램 프록시를 통해 hello 앱을 게시할 때 만들어진 외부 URL hello 수 있습니다. 

   ![암호 기반 로그온 선택 및 URL 입력](./media/application-proxy-sso-azure-portal/password-sso.png)

7. **저장**을 선택합니다.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>앱 테스트

원격 액세스 tooyour 응용 프로그램에 대해 구성 된 tooexternal URL로 이동 합니다. 이러한 앱에 대 한 자격 증명 (또는 액세스로 설정 하는 테스트 계정의 자격 증명 hello)를 사용 하 여 로그인 합니다. 성공적으로 로그인 하면 있습니다 수 tooleave hello 앱와 자격 증명을 다시 입력 하지 않고 다시 시도 합니다. 

## <a name="next-steps"></a>다음 단계

- 다른 방법으로 tooimplement에 대해 알아보세요 [Single sign on 응용 프로그램 프록시](application-proxy-sso-overview.md)
- [Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항](application-proxy-security-considerations.md)을 알아봅니다