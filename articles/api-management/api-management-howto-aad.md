---
title: "Azure Active Directory-Azure API 관리를 사용 하 여 aaaAuthorize 개발자 계정을 | Microsoft Docs"
description: "자세한 내용은 방법 tooauthorize 사용자가 Azure Active Directory를 사용 하 여 API 관리에서 합니다."
services: api-management
documentationcenter: API Management
author: steved0x
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
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Tooauthorize 개발자 어떻게 사용 하 여 계정을 Azure Active Directory를 Azure API 관리에서
## <a name="overview"></a>개요
이 가이드에서는 tooenable Azure Active Directory에서 사용자에 대 한 toohello 개발자 포털에 액세스 하는 방법을 알아봅니다. 이 가이드 또한 보면 방법을 포함 하는 외부 그룹을 추가 하 여 Azure Active Directory 사용자 그룹이 toomanage hello Azure Active Directory의 사용자가 있습니다.

> 이 가이드의 단계를 toocomplete hello 있어야 Azure Active Directory는 toocreate에 응용 프로그램입니다.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Tooauthorize 개발자 어떻게 사용 하 여 계정을 Azure Active Directory
시작 tooget 클릭 **게시자 포털** hello API 관리 서비스에 대 한 Azure 포털의에서. API 관리 게시자 포털 toohello 이동합니다.

![게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

클릭 **보안** hello에서 **API 관리** 메뉴를 클릭 한 hello 왼쪽 **외부 Id**합니다.

![외부 ID][api-management-security-external-identities]

**Azure Active Directory**를 클릭합니다. Hello 메모 **리디렉션 URL** hello Azure 클래식 포털에서에서 Azure Active Directory tooyour 전환 하 고 있습니다.

![외부 ID][api-management-security-aad-new]

Hello 클릭 **추가** toocreate 새 Azure Active Directory 응용 프로그램 단추 선택한 **조직에서 개발 중인 응용 프로그램 추가**합니다.

![새 Azure Active Directory 응용 프로그램 추가][api-management-new-aad-application-menu]

Hello 응용 프로그램에 대 한 이름을 입력 **웹 응용 프로그램 및/또는 Web API**, hello 다음 단추를 클릭 합니다.

![새 Azure Active Directory 응용 프로그램][api-management-new-aad-application-1]

에 대 한 **로그온 URL**, 개발자 포털을 가리키도록의 hello 로그온 URL을 입력 합니다. 이 예제에서는 hello **로그온 URL** 은 `https://aad03.portal.current.int-azure-api.net/signin`합니다. 

Hello에 대 한 **앱 ID URL**hello Azure Active Directory에 대 한 hello 기본 도메인 또는 사용자 지정 도메인을 입력 하 고 고유한 문자열 tooit를 추가 합니다. 이 예제에서는 기본 도메인의 hello **https://contoso5api.onmicrosoft.com** 의 hello 접미사와 함께 사용 되 **/api** 지정 합니다.

![새 Azure Active Directory 응용 프로그램 속성][api-management-new-aad-application-2]

Hello 확인 단추 toosave 클릭 하 고 hello 응용 프로그램을 만들어 toohello 전환 **구성** tooconfigure hello 새 응용 프로그램을 탭 합니다.

![새 Azure Active Directory 응용 프로그램 만들어짐][api-management-new-aad-app-created]

여러 Azure Active 디렉터리 하는 경우이 응용 프로그램에 사용 되는 toobe 클릭 **예** 에 대 한 **응용 프로그램은 다중 테 넌 트**합니다. hello 기본값은 **아니요**합니다.

![예][api-management-aad-app-multi-tenant]

복사 hello **리디렉션 URL** hello에서 **Azure Active Directory** hello 섹션 **외부 Id** 탭 hello 게시자 포털에서 하 고 hello 에붙여**회신 URL** 입력란. 

![회신 URL][api-management-aad-reply-url]

스크롤 toohello 맨 hello 구성 탭을 선택 하는 hello **응용 프로그램 사용 권한** 드롭 다운 확인 **디렉터리 데이터 읽기**합니다.

![응용 프로그램 권한][api-management-aad-app-permissions]

선택 hello **권한 위임** 드롭 다운 확인 **로그온을 사용 하도록 설정 하 고 사용자의 프로필 읽기**합니다.

![위임된 권한][api-management-aad-delegated-permissions]

> 응용 프로그램 및 권한이 위임된 하는 방법에 대 한 자세한 내용은 참조 [Graph API 액세스 hello][Accessing hello Graph API]합니다.
> 
> 

복사 hello **클라이언트 Id** toohello 클립보드 합니다.

![클라이언트 ID][api-management-aad-app-client-id]

뒤로 toohello 게시자 포털을 전환 하 고 hello에 붙여 **클라이언트 Id** hello Azure Active Directory 응용 프로그램 구성에서 복사 합니다.

![클라이언트 ID][api-management-client-id]

뒤로 toohello Azure Active Directory 구성을 전환 하 고 hello 클릭 **기간 선택** 드롭 다운 hello **키** 섹션 고 간격을 지정 합니다. 이 예제에서는 **1년**을 사용합니다.

![키][api-management-aad-key-before-save]

클릭 **저장** toosave hello 구성 및 표시 hello 키입니다. Hello 키 toohello 클립보드에 복사 합니다.

> 이 키를 기록해 둡니다. Hello Azure Active Directory 구성 창을 닫으면 되 면 hello 키를 다시 표시할 수 없습니다.
> 
> 

![키][api-management-aad-key-after-save]

스위치 백 toohello 게시자 포털 및 붙여넣기 hello 키 hello에 **클라이언트 암호** 입력란.

![클라이언트 암호][api-management-client-secret]

**테 넌 트 허용** 하는 디렉터리 액세스 toohello hello API 관리 서비스 인스턴스에의 Api를 포함 하도록 지정 합니다. Hello toogrant에 액세스 하는 Azure Active Directory 인스턴스 toowhich의 hello 도메인을 지정 합니다. 줄바꿈, 공백 또는 쉼표로 여러 도메인을 구분할 수 있습니다.

![허용된 테넌트][api-management-client-allowed-tenants]


Hello 원하는 구성이 지정 되어 있는 경우 클릭 **저장**합니다.

![저장][api-management-client-allowed-tenants-save]

지정 된는 Azure Active Directory의 hello 단계를 수행 하 여 toohello 개발자 포털에 서명할 수 hello에 hello 사용자 hello 변경 내용이 저장 되 면 [Azure Active Directory 계정을 사용 하 여 toohello 개발자 포털에 로그인] [Log in toohello Developer portal using an Azure Active Directory account].

여러 도메인 hello에 지정할 수 있습니다 **허용 테 넌 트** 섹션. 모든 사용자는 hello 원래 도메인 hello 응용 프로그램 등록 된 다른 도메인에서 로그인 할 수, 전에 hello 서로 다른 도메인의 글로벌 관리자 권한을 부여 해야 응용 프로그램 tooaccess hello에 대 한 디렉터리 데이터. toogrant 권한, 전역 관리자에 게 너무 이동 해야`https://<URL of your developer portal>/aadadminconsent` (예를 들어 https://contoso.portal.azure-api.net/aadadminconsent) hello toogive 액세스 tooand 원하는 Active Directory 테 넌 트의 hello 도메인 이름 입력 제출을 클릭 합니다. Hello 다음의 예를 들어의 전역 관리자 `miaoaad.onmicrosoft.com` toogive 권한 toothis 특정 개발자 포털에서이 하려고 시도 합니다. 

![권한][api-management-aad-consent]

Hello 다음 화면에서 전역 관리자에 게 증명된 tooconfirm hello 권한을 부여 됩니다. 

![권한][api-management-permissions-form]

> 비전역 관리자가 권한 전에 toolog에 전역 관리자가 부여, hello 로그인 시도 실패 및 오류 화면이 표시 됩니다.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>어떻게 tooadd 외부 Azure Active Directory 그룹
Azure Active Directory의 사용자에 대 한 액세스를 설정한 후 쉽게 관리할 수 원하는 hello 제품 hello 그룹에서 hello 개발자의 hello 연결 API 관리 toomore에 Azure Active Directory 그룹을 추가할 수 있습니다.

> 먼저 외부 Azure Active Directory 그룹에서 Azure Active Directory hello tooconfigure hello hello 이전 섹션 절차에에서 따라 hello Identities 탭에서 구성 되어야 합니다. 
> 
> 

외부 Azure Active Directory 그룹 hello에서 추가 된 **가시성** toogrant 액세스 toohello 그룹 원하는 hello 제품의 탭 합니다. 클릭 **제품**, hello 원하는 제품의 hello 이름을 클릭 하 고 있습니다.

![제품 구성][api-management-configure-product]

Toohello 전환 **가시성** 탭을 클릭 **Azure Active Directory에서 그룹 추가**합니다.

![그룹 추가][api-management-add-groups]

선택 hello **Azure Active Directory 테 넌 트** hello 드롭 다운 목록 및 hello hello에서 원하는 그룹의 다음 유형 hello 이름에서 **그룹** toobe 입력란을 추가 합니다.

![그룹 선택][api-management-select-group]

이 그룹 이름은 hello에 있습니다 **그룹** hello 다음 예제에에서 표시 된 대로 Azure Active Directory에 대 한 나열 합니다.

![Azure Active Directory 그룹 목록][api-management-aad-groups-list]

클릭 **추가** toovalidate hello 그룹 이름 및 hello 그룹을 추가 합니다. 이 예제에서는 hello **Contoso 5 개발자** 외부 그룹이 추가 됩니다. 

![그룹 추가됨][api-management-aad-group-added]

클릭 **저장** toosave hello 새 그룹을 선택 합니다.

제품 중 하나에서 Azure Active Directory 그룹에 구성 된 사용 가능한 toobe hello에 확인 표시가 되어 **가시성** 탭에 대 한 hello API 관리 서비스 인스턴스의 다른 제품 hello 합니다.

tooreview hello 속성 hello hello 그룹의 hello 이름을 클릭 하는 추가 되 면 외부 그룹을 구성 하 고 **그룹** 탭 합니다.

![그룹 관리][api-management-groups]

여기에서 hello를 편집할 수 있습니다 **이름** 및 hello **설명** hello 그룹의 합니다.

![그룹 편집][api-management-edit-group]

사용자 hello에서 구성 된 Azure Active Directory 수 뷰와 toohello 개발자 포털에 로그인 및 hello 지침 hello 섹션 다음에 따라 표시 여부를 가지는 tooany 그룹을 구독 합니다.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>어떻게 toolog Azure Active Directory 계정을 사용 하 여 toohello 개발자 포털에서
hello 이전 섹션에 구성 된 Azure Active Directory 계정을 사용 하는 hello 개발자 포털에 toolog hello를 사용 하 여 새 브라우저 창을 열고 **로그온 URL** hello Active Directory 응용 프로그램 구성 및 클릭 **Azure Active Directory**합니다.

![개발자 포털][api-management-dev-portal-signin]

Azure Active Directory에 hello 사용자 중 하나의 hello 자격 증명을 입력 하 고 클릭 **로그인**합니다.

![로그인][api-management-aad-signin]

추가 정보가 필요한 경우 등록 양식과 함께 메시지가 표시될 수 있습니다. Hello 등록 양식을 완성 하 고 클릭 **등록**합니다.

![등록][api-management-complete-registration]

사용자는 이제 API 관리 서비스 인스턴스에 대 한 hello 개발자 포털에 기록 됩니다.

![등록 완료][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
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
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

