---
title: "Azure AD 응용 프로그램 프록시를 사용 하 여 aaaPublish 앱 | Microsoft Docs"
description: "온-프레미스 Azure AD 응용 프로그램 프록시를 사용 하는 응용 프로그램 toohello 클라우드 hello Azure 포털에에서 게시 합니다."
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
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Azure 클래식 포털](active-directory-application-proxy-publish.md)

Azure AD (Active Directory) 응용 프로그램 프록시를 사용 하면 온-프레미스 응용 프로그램 toobe hello를 통해 액세스를 게시 하 여 원격 작업자를 지 원하는 인터넷 합니다. 네트워크 외부의 hello Azure 포털 tooprovide 보안 된 원격 액세스를 통해 이러한 응용 프로그램을 게시할 수 있습니다.

이 문서는 hello 단계 toopublish 응용 프로그램 프록시를 사용 하 여 온-프레미스 앱을 안내합니다. 사용자는이 문서를 완료 한 후 수 tooaccess 응용 프로그램을 원격으로 수 있습니다. 준비 tooconfigure 같은 hello 응용 프로그램에 대 한 추가 기능 수 고 single sign on, 개인된 정보 및 보안 요구 사항입니다.

새 tooApplication 프록시를 사용 하는 경우 자세한 hello 문서와 함께이 기능에 대 한 내용은 [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](active-directory-application-proxy-get-started.md)합니다.


## <a name="publish-an-on-premises-app-for-remote-access"></a>원격 액세스를 위한 온-프레미스 앱 게시

이러한 단계 toopublish 응용 프로그램 프록시를 사용 하 여 앱을 따릅니다. 이미 다운로드 하 고 조직에 대 한 커넥터를 구성 하지 않은, 이동 너무[응용 프로그램 프록시를 시작 하 고 hello 커넥터 설치](active-directory-application-proxy-enable.md) 먼저 다음 응용 프로그램을 게시 합니다.

> [!TIP]
> 테스트 하려는 응용 프로그램 프록시 아웃 hello에 대 한 처음으로 하는 경우 암호 기반 인증을 위해 설정 하는 응용 프로그램을 선택 합니다. 응용 프로그램 프록시 인증에 다른 형식을 지원 하지만 암호 기반 앱이를 가장 쉽게 tooget hello 및 신속 하 게 실행. 

1. Hello에 관리자 권한으로 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. **Azure Active Directory** > **Enterprise 응용 프로그램** > **새로운 응용 프로그램**을 선택합니다.

  ![엔터프라이즈 응용 프로그램 추가](./media/application-proxy-publish-azure-portal/add-app.png)

3. **모두**를 선택한 다음 **온-프레미스 응용 프로그램**을 선택합니다.  

  ![응용 프로그램 직접 추가](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Hello 다음 응용 프로그램에 대 한 정보를 제공 합니다.

   - **이름**: hello Azure 포털 및 hello 액세스 패널에 표시 되는 hello 응용 프로그램의 hello 이름입니다. 

   - **내부 URL**: hello 개인 네트워크 내부에서 tooaccess hello 응용 프로그램을 사용 하는 URL입니다. Hello 서버 hello 나머지 게시 하지 않은 동안 hello 백 엔드 서버 toopublish에 특정 경로 제공할 수 있습니다. 이러한 방식으로 서로 다른 사이트를 게시할 수 있습니다 다른 앱과 동일한 서버 hello 되 고 각각 고유한 이름 및 액세스 규칙을 지정 합니다.

     > [!TIP]
     > 경로 게시 하는 경우 모든 hello 필요한 이미지, 스크립트 및 응용 프로그램에 대 한 스타일 시트를 포함 하는지 확인 합니다. 예를 들어 앱 https://yourapp/app에 https://yourapp/media에 있는 이미지를 사용 하는 경우 다음 게시 해야 https://yourapp/ hello 경로로 합니다. 이 내부 URL toobe hello 방문 페이지를 사용자에 게 표시 되어 있지 않습니다. 자세한 내용은 [게시된 앱에 대해 사용자 지정 홈페이지 설정](application-proxy-office365-app-launcher.md)을 참조하세요.

   - **외부 URL**: hello tooin 순서 tooaccess hello 외부 응용 프로그램에서 네트워크 사용자가 이동 하는 주소입니다. Toouse hello 기본 응용 프로그램 프록시 도메인을 사용 하지 않으려는 경우에 대해 알아보세요 [Azure AD 응용 프로그램 프록시에 사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)합니다.
   - **사전 인증**: 응용 프로그램 프록시에 어떻게 액세스 tooyour 응용 프로그램을 제공 하기 전에 사용자를 확인 합니다. 

     - Azure Active Directory: 응용 프로그램 프록시는 hello 디렉터리와 응용 프로그램에 대 한 사용 권한을 인증 하는 Azure AD 사용 하 여 사용자가 toosign을 리디렉션합니다. 조건부 액세스 및 Multi-factor Authentication과 같은 Azure AD 보안 기능을 이용할 수 있도록 hello 기본적으로이 옵션을 유지 것이 좋습니다.
     - 통과: 사용자가 Azure Active Directory tooaccess hello 응용 프로그램에 대해 tooauthenticate를 않아도 됩니다. Hello 백 엔드에 인증 요구 사항을 설정할 수 있습니다.
   - **커넥터 그룹**: 커넥터 프로세스 hello 원격 액세스 tooyour 응용 프로그램 및 커넥터 그룹을 사용 하면 커넥터와 지역, 네트워크 또는 목적으로 앱을 구성할 수 있습니다. 앱이 너무 할당 된 아직 작성 된 모든 커넥터 그룹에 없으면**기본**합니다.

   ![응용 프로그램 구성](./media/application-proxy-publish-azure-portal/configure-app.png)
5. 필요한 경우 추가 설정을 구성합니다. 대부분의 응용 프로그램에서는 다음과 같은 설정을 기본 상태로 유지해야 합니다. 
   - **백 엔드 응용 프로그램 시간 제한이**:이 값을 너무 설정**긴** tooauthenticate 느린 연결 및 응용 프로그램은 경우에 합니다. 
   - **헤더의 Url 변환**:으로이 값을 유지 **예** 응용 프로그램 hello 인증 요청에 hello 원래 호스트 헤더가 필요한 경우를 제외 합니다.
   - **응용 프로그램 본문에 Url 변환**:으로이 값을 유지 **아니요** 하드 코드 된 HTML 링크 tooother 온-프레미스 응용 프로그램 및 사용자 지정 도메인을 사용 하지 않는 한 합니다. 자세한 내용은 [응용 프로그램 프록시를 사용한 링크 변환](application-proxy-link-translation.md)을 참조하세요.
   
   ![응용 프로그램 구성](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. **추가**를 선택합니다.


## <a name="add-a-test-user"></a>테스트 사용자 추가 

tootest 앱 올바르게 게시 된 테스트 사용자 계정을 추가 합니다. 이 계정이 사용 권한을 tooaccess hello 앱에서 이미 갖고 있는지 확인 hello 회사 네트워크 내부 합니다.

1. Hello 빠른 시작 블레이드를 다시 선택 **테스트 하기 위한 사용자 지정**합니다.

  ![테스트할 사용자 지정](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Hello 사용자 및 그룹 블레이드 선택 **추가**합니다.

  ![사용자 또는 그룹 추가](./media/application-proxy-publish-azure-portal/add-user.png)

3. Hello 추가 할당 블레이드에서 선택 **사용자 및 그룹** tooadd hello 계정을 선택 합니다. 
4. **할당**을 선택합니다.

## <a name="test-your-published-app"></a>게시된 앱 테스트

브라우저에서 hello 중 구성한 toohello 외부 URL을 탐색 단계를 게시 합니다. Hello 시작 화면에서 표시 되어야 하며 수 toosign hello 테스트 계정을 사용 하 여 있습니다 설정 되어야 합니다.

![게시된 앱 테스트](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>다음 단계
- [커넥터를 다운로드](active-directory-application-proxy-enable.md) 및 [커넥터 그룹을 만들](active-directory-application-proxy-connectors-azure-portal.md) 별도 네트워크 위치에 toopublish 응용 프로그램입니다.

- 새로 게시된 앱에 대해 [Single Sign-On을 설정](application-proxy-sso-azure-portal.md)합니다.
