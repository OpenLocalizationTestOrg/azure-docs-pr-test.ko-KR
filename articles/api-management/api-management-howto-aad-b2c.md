---
title: "Azure Active Directory B2C-Azure API 관리를 사용 하 여 개발자 계정을 aaaAuthorize | Microsoft Docs"
description: "자세한 내용은 방법 API 관리에서 Azure Active Directory B2C를 사용 하 여 tooauthorize 사용자입니다."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Azure API 관리에서 Azure Active Directory B2C를 사용 하 여 tooauthorize 개발자 계정을 하는 방법
## <a name="overview"></a>개요
Azure Active Directory B2C는 소비자 지향 웹 및 모바일 응용 프로그램을 위한 클라우드 ID 관리 솔루션입니다. Toomanage 액세스 tooyour 개발자 포털을 사용할 수 있습니다. 이 가이드와 Azure Active Directory B2C API 관리 서비스 toointegrate 프로그램에 필요한 구성 hello를 표시 합니다. 클래식 Azure Active Directory를 사용 하 여 액세스 toohello 개발자 포털을 사용 하는 방법에 대 한 정보를 참조 하십시오. [tooauthorize 개발자 방법을 사용 하 여 계정을 Azure Active Directory]합니다.

> [!NOTE]
> toocomplete hello이이 가이드의에서 단계를 먼저 Azure Active Directory B2C 테 넌 트 toocreate 응용 프로그램의 해야 합니다. 또한 정책이 필요 한가요 toohave 등록 및 signin 준비 합니다. 자세한 내용은 [Azure Active Directory B2C 개요]를 참조하세요.

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Azure Active Directory B2C를 사용하여 개발자 계정에 권한 부여

1. 시작 tooget 클릭 **게시자 포털** hello API 관리 서비스에 대 한 Azure 포털의에서. API 관리 게시자 포털 toohello 이동합니다.

   ![게시자 포털][api-management-management-console]

   > [!NOTE]
   > API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 자습서시작][Get started with Azure API Management].

2. Hello에 **API 관리** 메뉴를 클릭 하 여 **보안**합니다. Hello에 **Identities** 탭에서 선택 **Azure Active Directory B2C**합니다.

  ![외부 ID 1][api-management-howto-aad-b2c-security-tab]

3. Hello 메모 **리디렉션 URL** hello Azure 포털에서에서 Active Directory B2C tooAzure 전환 하 고 있습니다.

  ![외부 ID 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Hello 클릭 **응용 프로그램** 단추입니다.

  ![새 응용 프로그램 1 등록][api-management-howto-aad-b2c-portal-menu]

5. Hello 클릭 **추가** toocreate 새 Azure Active Directory B2C 응용 프로그램 단추입니다.

  ![새 응용 프로그램 2 등록][api-management-howto-aad-b2c-add-button]

6. Hello에 **새 응용 프로그램** 블레이드에서 hello 응용 프로그램에 대 한 이름을 입력 합니다. **Web App/Web API**에서 **예**를 선택하고 **암시적 흐름 허용**에서 **예**를 선택합니다. 그런 다음 복사본 hello **리디렉션 URL** hello에서 **Azure Active Directory B2C** hello 섹션 **Identities** hello 게시자 포털을 탭 하 고 hello 에붙여**회신 URL** 입력란.

  ![새 응용 프로그램 3 등록][api-management-howto-aad-b2c-app-details]

7. Hello 클릭 **만들기** 단추입니다. Hello에 나타나는 hello 응용 프로그램을 만든 경우 **응용 프로그램** 블레이드입니다. Hello 응용 프로그램 이름 toosee 세부 정보를 클릭 합니다.

  ![새 응용 프로그램 4 등록][api-management-howto-aad-b2c-app-created]

8. Hello에서 **속성** 블레이드, 복사 hello **응용 프로그램 ID** toohello 클립보드 합니다.

  ![응용 프로그램 ID 1][api-management-howto-aad-b2c-app-id]

9. 뒤로 toohello 게시자 포털을 전환 하 고 hello ID hello에 붙여 **클라이언트 Id** 입력란.

  ![응용 프로그램 ID 2][api-management-howto-aad-b2c-client-id]

10. 전환 백 toohello Azure 포털을 hello 클릭 **키** 단추를 선택한 다음 클릭 **키 생성**합니다. 클릭 **저장** toosave hello 구성 및 표시 hello **응용 프로그램 키는**합니다. Hello 키 toohello 클립보드에 복사 합니다.

  ![앱 키 1][api-management-howto-aad-b2c-app-key]

11. 스위치 백 toohello 게시자 포털 및 붙여넣기 hello 키 hello에 **클라이언트 암호** 입력란.

  ![앱 키 2][api-management-howto-aad-b2c-client-secret]

12. Hello hello Azure Active Directory B2C 테 넌 트에 도메인 이름을 지정 **허용 테 넌 트**합니다.

  ![허용된 테넌트][api-management-howto-aad-b2c-allowed-tenant]

13. Hello 지정 **등록 정책** 및 **Signin 정책**합니다. 선택적으로 제공할 수도 있습니다 hello **프로필 편집 정책** 및 **암호 재설정 정책**합니다.

  ![정책][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > 정책에 대한 자세한 내용은 [Azure Active Directory B2C: 확장할 수 있는 정책 프레임워크]를 참조하세요.

14. 원하는 구성 hello를 지정한 후 클릭 **저장**합니다.

  Hello 변경 내용이 저장 된 후 개발자 수 toocreate 새 계정이 되며 Azure Active Directory B2C를 사용 하 여 toohello 개발자 포털에 로그인 합니다.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Azure Active Directory B2C를 사용하여 개발자 계정에 등록

1. 에 Azure Active Directory B2C를 사용 하 여 개발자 계정으로 가입할 toosign 새 브라우저 창을 열고 toohello 개발자 포털을 이동 합니다. Hello 클릭 **등록** 단추입니다.

   ![개발자 포털 1][api-management-howto-aad-b2c-dev-portal]

2. 선택 하는 toosign **Azure Active Directory B2C**합니다.

   ![개발자 포털 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. 리디렉션된 toohello 등록 정책 hello 이전 섹션에서 구성 하는 것입니다. 전자 메일 주소 또는 기존 소셜 계정 중 하나를 사용 하 여 위로 toosign를 선택 합니다.

   > [!NOTE]
   > Azure Active Directory B2C hello에 사용 하도록 설정 된 옵션만 hello 이면 **Identities** 탭 hello 게시자 포털에서 수 리디렉션된 toohello 등록 정책을 직접 합니다.

   ![개발자 포털][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Hello 등록 완료 되 면 리디렉션된 백 toohello 개발자 포털 것입니다. API 관리 서비스 인스턴스에 대 한 toohello 개발자 포털을 지금 로그인 되어 있습니다.

    ![등록 완료][api-management-registration-complete]

## <a name="next-steps"></a>다음 단계

*  [Azure Active Directory B2C 개요]
*  [Azure Active Directory B2C: 확장할 수 있는 정책 프레임워크]
*  [Azure Active Directory B2C에서 Microsoft 계정을 ID 공급자로 사용]
*  [Azure Active Directory B2C에서 Google 계정을 ID 공급자로 사용]
*  [Azure Active Directory B2C에서 LinkedIn 계정을 ID 공급자로 사용]
*  [Azure Active Directory B2C에서 Facebook 계정을 ID 공급자로 사용]




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Azure Active Directory B2C 개요]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[tooauthorize 개발자 방법을 사용 하 여 계정을 Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: 확장할 수 있는 정책 프레임워크]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Azure Active Directory B2C에서 Microsoft 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Azure Active Directory B2C에서 Google 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Azure Active Directory B2C에서 Facebook 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Azure Active Directory B2C에서 LinkedIn 계정을 ID 공급자로 사용]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
