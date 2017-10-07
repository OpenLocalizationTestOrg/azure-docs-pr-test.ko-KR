---
title: "Azure AD 응용 프로그램 프록시에 대 한 aaaHeader 기반 인증 PingAccess 사용 | Microsoft Docs"
description: "PingAccess 및 응용 프로그램 프록시 toosupport 헤더 기반 인증으로 응용 프로그램을 게시 합니다."
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
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>응용 프로그램 프록시 및 PingAccess를 사용하여 Single Sign-On에 대한 헤더 기반 인증

Azure Active Directory 응용 프로그램 프록시 및 PingAccess 관계를 맺고 함께 tooprovide 액세스 tooeven 사용 하는 Azure Active Directory 고객 더 많은 응용 프로그램입니다. PingAccess 확장 hello [기존의 응용 프로그램 프록시 서비스](active-directory-application-proxy-get-started.md) tooinclude single sign-on 액세스 tooapplications 인증에 대 한 헤더를 사용 하는 합니다.

## <a name="what-is-pingaccess-for-azure-ad"></a>Azure AD용 PingAccess는 무엇입니까?

Azure Active Directory에 대 한 PingAccess toogive 사용자가 액세스할 수 있도록 하는 PingAccess 및 single sign on tooapplications 인증에 대 한 헤더를 사용 하는 제품입니다. 응용 프로그램 프록시는 Azure AD tooauthenticate 액세스를 사용 하 여와 hello 커넥터 서비스를 통해 트래픽을 전달 요, 이러한 앱을 처리 합니다. PingAccess는 hello 앱 앞에 배치 하 고 hello 응용 프로그램을 읽을 수는 hello 형태로 hello 인증을 받을 수 있도록 Azure AD에서 액세스 토큰 hello 헤더로 변환 합니다.

회사 앱 toouse에 로그인 할 때 사용자가 다른 있어서는 합니다. 여전히 어디에서든지 모든 장치에서 작업할 수 있습니다. 

Hello 응용 프로그램 프록시 커넥터의 인증 유형에 관계 없이 원격 트래픽을 tooall 앱을 지시 하는 경우 이후 자동으로 tooload 균형을 계속 합니다.

## <a name="how-do-i-get-access"></a>액세스 권한은 어떻게 얻을 수 있나요?

이 시나리오는 Azure Active Directory 및 PingAccess 간의 파트너 관계를 통해 제공되므로 두 서비스에 대한 라이선스가 필요합니다. 그러나 Azure Active Directory Premium 구독에 too20 응용 프로그램을 검사 하는 기본 PingAccess 라이선스가 포함 되어 있습니다. 20 개 이상의 헤더 기반 응용 프로그램 toopublish 해야 할 경우 PingAccess에서 추가 라이센스를 구입할 수 있습니다. 

자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.

## <a name="publish-your-application-in-azure"></a>Azure에 응용 프로그램 게시

이 문서는 사용자에 게 게시 하는 hello에 대 한이 시나리오를 사용 하 여 앱 처음으로 사용 됩니다. Tooget를 어떻게 시작 응용 프로그램과 PingAccess, 또한 toohello 게시 단계 안내 합니다. 두 서비스를 이미 구성한 해도 hello 게시 단계 세부 정보를 원하는 경우 hello 커넥터 설치를 건너뛰고 너무 이동[응용 프로그램 프록시는 AD에 앱 tooAzure 추가](#add-your-app-to-Azure-AD-with-Application-Proxy)합니다.

>[!NOTE]
>이 시나리오는 Azure AD 간의 파트너 관계 이므로 hello Ping Id 사이트에 있는 hello 명령 중 일부는 PingAccess, 및입니다.

### <a name="install-an-application-proxy-connector"></a>응용 프로그램 프록시 커넥터 설치

응용 프로그램 프록시를 사용 하 고, 이미 있고는 커넥터가 설치 되어 있는 경우이 섹션을 건너뛰고 너무 이동[응용 프로그램 프록시는 AD에 앱 tooAzure 추가](#add-your-app-to-azure-ad-with-application-proxy)합니다.

hello 응용 프로그램 프록시 커넥터는 Windows 서버에서 원격 직원 tooyour hello 트래픽을 전송 하는 서비스에 게시 된 앱입니다. 설치 지침 보다 자세한 참조 [hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 전역 관리자입니다.
2. **Azure Active Directory** > **응용 프로그램 프록시**를 선택합니다.
3. 선택 **커넥터 다운로드** toostart hello 응용 프로그램 프록시 커넥터 다운로드 합니다. Hello 설치 지침을 따릅니다.

   ![응용 프로그램 프록시를 사용 하도록 설정 하 고 hello 커넥터를 다운로드 합니다.](./media/application-proxy-ping-access/install-connector.png)

4. Hello connector 다운로드 자동으로 사용 하도록 설정 해야 응용 프로그램 프록시 본인이 아니신가요 선택할 수 있지만 디렉터리에 대 한 **응용 프로그램 프록시를 사용 하도록 설정**합니다.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>사용자 응용 프로그램 tooAzure AD 응용 프로그램 프록시를 추가 합니다.

Tootake hello Azure 포털에에서 필요한 두 가지 작업이 있습니다. 먼저 toopublish 응용 프로그램 프록시 응용 프로그램입니다. 그런 다음 해야 toocollect hello PingAccess 단계 중에 사용할 수 있는 hello 앱에 대 한 정보.

이러한 단계 toopublish 응용 프로그램을 따릅니다. 1 ~ 8 단계에 대한 자세한 연습은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](application-proxy-publish-azure-portal.md)를 참조하세요.

1. Toohello hello 마지막 섹션에서 그렇지 않은 경우 로그인 [Azure 포털](https://portal.azure.com) 전역 관리자입니다.
2. **Azure Active Directory** > **Enterprise 응용 프로그램**을 선택합니다.
3. 선택 **추가** hello hello 블레이드 위쪽에 있습니다.
4. **온-프레미스 응용 프로그램**을 선택합니다.
5. 새 응용 프로그램에 대 한 정보가 필요한 hello 필드를 작성 합니다. Hello hello 설정에 대 한 지침을 사용 합니다.
   - **내부 URL**: 작업을 수행 해야 toohello 응용 프로그램의 로그인 페이지에 hello 회사 네트워크에 있는 경우 hello URL을 제공 하는 일반적으로 합니다. 이 시나리오에 대 한 hello 커넥터는 tootreat hello PingAccess 프록시 (hello) 프런트 페이지 hello 응용 프로그램에 필요합니다. `https://<host name of your PA server>:<port>` 형식을 사용합니다. hello 포트는 기본적으로 3000 있지만 PingAccess에서 구성할 수 있습니다.
   - **사전 인증 방법**: Azure Active Directory
   - **헤더에서 URL 변환**: 아니요

   >[!NOTE]
   >첫 번째 응용 프로그램의 경우 포트 3000 toostart를 사용 하 여 방문 하 여 tooupdate이이 설정을 PingAccess 구성을 변경 하는 경우. 이 두 번째 이상 앱을이 수신기 PingAccess에 구성한 toomatch hello를 할 수 있습니다. [PingAccess의 수신기](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html)에 대해 자세히 알아봅니다.

6. 선택 **추가** hello hello 블레이드 맨 아래에 있습니다. 응용 프로그램은 추가 되 고 hello 빠른 시작 메뉴가 열립니다.
7. Hello 빠른 시작 메뉴에서 선택 **테스트 하기 위한 사용자 지정**, 적어도 한 명의 사용자 toohello 응용 프로그램을 추가 합니다. 이 테스트 계정 액세스 toohello 온-프레미스 응용 프로그램에 있는지 확인 합니다.
8. 선택 **할당** toosave hello 테스트 사용자 할당 합니다.
9. Hello 응용 프로그램 관리 블레이드의 선택 **Single sign on**합니다.
10. 선택 **헤더 기반 로그온** hello 드롭 다운 메뉴에서 합니다. **저장**을 선택합니다.

   >[!TIP]
   >헤더 기반 single sign on을 사용 하 여 처음으로 이면 tooinstall PingAccess 해야 합니다. toomake Azure 구독이 확실 PingAccess 설치 프로그램에서이 single sign-on 페이지 toodownload PingAccess hello 연결을 사용 하 여 자동으로 연결 합니다. 이제 hello 다운로드 사이트를 열 수도 있고 나중에 다시 toothis 페이지 수 있습니다. 

   ![헤더 기반 로그온 선택](./media/application-proxy-ping-access/sso-header.PNG)

11. Hello 엔터프라이즈 응용 프로그램 블레이드를 닫거나 모든 hello 방식으로 toohello 왼쪽된 tooreturn toohello Azure Active Directory 메뉴 스크롤하십시오.
12. **앱 등록**을 선택합니다.

   ![앱 등록 선택](./media/application-proxy-ping-access/app-registrations.png)

13. 방금 추가한 다음 선택 hello 앱 **회신 Url**합니다.

   ![회신 URL 선택](./media/application-proxy-ping-access/reply-urls.png)

14. Hello 외부 URL이 할당 된 tooyour 앱 5 단계에서 목록에 있으면 hello 회신 Url toosee를 확인 합니다. 그렇지 않은 경우 지금 추가합니다.
15. Hello 응용 프로그램 설정 블레이드에서 선택 **필요한 권한**합니다.

  ![필요한 권한 선택](./media/application-proxy-ping-access/required-permissions.png)

16. **추가**를 선택합니다. Hello API에 대 한 선택 **Windows Azure Active Directory**, 다음 **선택**합니다. Hello 사용 권한에 대 한 선택 **읽기 및 모든 응용 프로그램 쓰기** 및 **로그인 및 사용자 프로필 읽기**, 다음 **선택** 및 **수행**합니다.  

  ![권한 선택](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Hello PingAccess 단계에 대 한 정보를 수집 합니다.

1. 앱 설정 블레이드에서 **속성**을 선택합니다. 

  ![속성 선택](./media/application-proxy-ping-access/properties.png)

2. Hello 저장 **응용 프로그램 Id** 값입니다. 이 값은 PingAccess를 구성할 때 hello 클라이언트 ID에 사용 됩니다.
3. Hello 응용 프로그램 설정 블레이드에서 선택 **키**합니다.

  ![키 선택](./media/application-proxy-ping-access/Keys.png)

4. 키 설명을 입력 하 고 hello 드롭 다운 메뉴에서 만료 날짜를 선택 하 여 키를 만듭니다.
5. **저장**을 선택합니다. Hello에 표시 되는 GUID **값** 필드입니다.

  이 값을 저장 이제 수 toosee 수 없을 것으로 그 후에 다시이 창을 닫으십시오.

  ![새 키 만들기](./media/application-proxy-ping-access/create-keys.png)

6. Hello 앱 등록 블레이드를 닫거나 모든 hello 방식으로 toohello 왼쪽된 tooreturn toohello Azure Active Directory 메뉴 스크롤하십시오.
7. **속성**을 선택합니다.
8. Hello 저장 **디렉터리 ID** GUID입니다.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>선택 사항-업데이트 GraphAPI toosend 사용자 지정 필드

Azure AD에서 인증에 대해 전송하는 보안 토큰의 목록은 [Azure AD 토큰 참조](./develop/active-directory-token-and-claims.md)를 참조하세요. GraphAPI tooset hello 응용 프로그램 필드를 사용 하 여 기타 토큰을 전송 하는 사용자 지정 클레임을 해야 할 경우 *acceptMappedClaims* 너무**True**합니다. Azure AD 그래프 탐색기 또는 MS 그래프 toomake이이 구성을 사용할 수 있습니다. 

이 예에서는 Graph Explorer를 사용합니다.

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>PingAccess 다운로드 및 앱 구성

모든 hello Azure Active Directory 설정 단계를 완료 하면 했으므로 tooconfiguring PingAccess에 이동할 수 있습니다. 

hello hello PingAccess 부분에서는이 시나리오에 대 한 자세한 단계에서에서 계속 Ping Identity 설명서 hello [Azure AD에 대 한 구성 PingAccess](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)합니다.

이러한 단계 PingAccess 계정이 아직 없는 경우, hello PingAccess 서버를 설치 하 고 hello hello Azure 포털에서에서 복사한 디렉터리 ID가 있는 Azure AD OIDC 공급자 연결을 만드는 hello 프로세스를 안내 합니다. 그런 다음 PingAccess에 hello 응용 프로그램 ID 및 키 값 toocreate 웹 세션을 사용 합니다. 그런 다음 ID 매핑을 설정하고 가상 호스트, 사이트 및 응용 프로그램을 만들 수 있습니다.

### <a name="test-your-app"></a>앱 테스트

이러한 모든 단계를 완료하면 앱이 준비되고 실행되어야 합니다. tootest, 브라우저를 열고 Azure의 hello 앱을 게시할 때 만든 toohello 외부 URL을 탐색 합니다. 해당 할당된 toohello 앱 hello 테스트 계정으로 로그인 합니다.

## <a name="next-steps"></a>다음 단계

- [Azure AD에 대한 PingAccess 구성(영문)](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Azure AD 응용 프로그램 프록시에서 Single Sign-On을 제공하는 방법](application-proxy-sso-overview.md)
- [응용 프로그램 프록시 문제 해결](active-directory-application-proxy-troubleshoot.md)
