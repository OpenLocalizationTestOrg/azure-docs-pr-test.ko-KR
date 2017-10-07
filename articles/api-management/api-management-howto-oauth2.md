---
title: "Azure API 관리에서 OAuth 2.0을 사용 하 여 aaaAuthorize 개발자 계정을 | Microsoft Docs"
description: "자세한 방법을 tooauthorize 사용자가 API 관리에서 OAuth 2.0을 사용 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Tooauthorize 개발자 어떻게 사용 하 여 계정을 Azure API 관리에서 OAuth 2.0
대부분의 Api 지원 [OAuth 2.0](http://oauth.net/2/) toosecure API hello 및를 유효한 사용자 액세스 권한이 있으며 리소스 toowhich에만 액세스할 수 있는 자격이 있는지 확인 합니다. 순서 toouse Azure API 관리 대화형 개발자 콘솔에서 이러한 Api와 hello 서비스 있습니다 tooconfigure OAuth 2.0을 사용 하면 서비스 인스턴스 toowork API를 사용 하도록 설정 합니다.

## <a name="prerequisites"> </a>필수 조건
이 가이드에서는 어떻게 tooconfigure API 관리 서비스 인스턴스 toouse 개발자에 대 한 OAuth 2.0 권한 부여 계정, 하지만 표시 하지 않는 있습니다 어떻게 알아봅니다 tooconfigure OAuth 2.0 공급자. hello 단계는 유사 하며 필요한 hello 가지 API 관리 서비스 인스턴스에서 OAuth 2.0을 구성에 사용 되는 정보는 공급자가 다른 경우 각 OAuth 2.0에 대 한 hello 구성 hello 동일 합니다. 이 항목에서는 OAuth 2.0 공급자로서 Azure Active Directory를 사용하는 예제를 설명합니다.

> [!NOTE]
> Azure Active Directory를 사용 하 여 OAuth 2.0 구성 방법에 대 한 자세한 내용은 참조 hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] 샘플.
> 
> 

## <a name="step1"> </a>API 관리에서 OAuth 2.0 권한 부여 서버 구성
시작 tooget 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.

![게시자 포털][api-management-management-console]

> [!NOTE]
> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

클릭 **보안** hello에서 **API 관리** hello 마우스 왼쪽된 단추 클릭에 메뉴 **OAuth 2.0**, 클릭 하 고 **추가 권한 부여 서버**합니다.

![OAuth 2.0][api-management-oauth2]

클릭 한 후 **추가 권한 부여 서버**, hello 새 권한 부여 서버 양식이 표시 됩니다.

![새 서버][api-management-oauth2-server-1]

Hello에는 이름 및 선택적 설명을 입력 **이름** 및 **설명** 필드입니다. 

> [!NOTE]
> 이러한 필드는 hello 현재 API 관리 서비스 인스턴스 내에서 사용 되는 tooidentify hello OAuth 2.0 권한 부여 서버 및 OAuth 2.0 hello 서버에서 해당 값이 제공 되지 않습니다.
> 
> 

Hello 입력 **클라이언트 등록 페이지 URL**합니다. 이 페이지는 사용자가 만드는 고의 계정을 관리할 수 있으며 사용 되는 OAuth 2.0 hello 공급자에 따라 달라 집니다. hello **클라이언트 등록 페이지 URL** toohello 페이지가 사용 하는 지점 toocreate를 사용 하 여를 업데이트 하 고 계정의 사용자 관리를 지 원하는 OAuth 2.0 공급자에 대 한 자신의 계정을 구성할 수 있습니다. 일부 조직에서는 구성 하지 않거나 hello OAuth 2.0 공급자가 지 원하는 경우에이 기능을 사용 합니다. OAuth 2.0 공급자에 사용자 계정의 관리를 구성 하는 경우, 회사 hello URL 또는 URL 같은 여기에 자리 표시자 URL 같은 입력 `https://placeholder.contoso.com`합니다.

hello hello hello 폼의 다음 섹션에 포함 되어 **인증 코드 권한 유형**, **권한 부여 끝점 URL**, 및 **권한 부여 요청 메서드가** 설정 합니다.

![새 서버][api-management-oauth2-server-2]

Hello 지정 **인증 코드 권한 유형** hello 원하는 형식을 선택 하 여 합니다. **인증 코드** 가 지정됩니다.

Hello 입력 **권한 부여 끝점 URL**합니다. Azure Active Directory에 대 한이 URL이 url을 비슷한 toohello 됩니다 여기서 `<client_id>` 응용 프로그램 toohello OAuth 2.0 서버를 식별 하는 hello 클라이언트 id로 바뀝니다.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

hello **권한 부여 요청 메서드가** toohello OAuth 2.0 서버 hello 권한 부여 요청을 보내는 하는 방식을 지정 합니다. 기본적으로는 **GET** 이 선택됩니다.

hello 다음 섹션은에 hello **끝점 URL 토큰**, **클라이언트 인증 방법을**, **메서드를 전송 하는 액세스 토큰**, 및 **기본범위** 지정 됩니다.

![새 서버][api-management-oauth2-server-3]

Azure Active Directory OAuth 2.0 서버 hello **끝점 URL 토큰** , 형식에 따라 hello 갖습니다 여기서 `<APPID>` 의 hello 형식이 `yourapp.onmicrosoft.com`합니다.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

hello에 대 한 기본 설정은 **클라이언트 인증 방법을** 은 **기본**, 및 **메서드를 전송 하는 액세스 토큰** 은 **권한 부여 헤더**. 이러한 값은 hello와 함께 hello 폼의이 섹션에 구성 된 **기본 범위**합니다.

hello **클라이언트 자격 증명** 섹션에서는 hello **클라이언트 ID** 및 **클라이언트 암호**, OAuth 2.0의 hello 생성 및 구성 프로세스 중 얻어 서버입니다. 한 번 hello **클라이언트 ID** 및 **클라이언트 암호** 지정 hello **redirect_uri** hello에 대 한 **인증 코드** 생성 됩니다. 이 URI는 OAuth 2.0 서버 구성에 사용 되는 tooconfigure hello 회신 URL입니다.

![새 서버][api-management-oauth2-server-4]

경우 **인증 코드 권한 유형** 너무 설정**리소스 소유자 암호**, hello **리소스 소유자 암호 자격 증명** 섹션은 사용 되는 toospecify;이 자격 증명 그렇지 않으면 있습니다 수 비워 둡니다.

![새 서버][api-management-oauth2-server-5]

Hello 양식을 완료 되 면 클릭 **저장** toosave hello API 관리 OAuth 2.0 권한 부여 서버 구성 합니다. Hello 서버 구성을 저장 되 고 나면 구성할 수 있습니다 Api toouse이이 구성에서는 hello 다음 섹션에 나와 있는 것 처럼 합니다.

## <a name="step2"></a>API toouse OAuth 2.0 사용자 권한 부여 구성
클릭 **Api** hello에서 **API 관리** 메뉴 hello에 남아 있는 원하는 hello API의 hello 이름을 클릭 하 고 **보안**, 한 다음 확인란 hello에 대 한 **OAuth 2.0**합니다.

![사용자 권한 부여][api-management-user-authorization]

원하는 선택 hello **권한 부여 서버** hello 드롭 다운 목록 및 클릭에서 **저장**합니다.

![사용자 권한 부여][api-management-user-authorization-save]

## <a name="step3"></a>Hello 개발자 포털에서에서 hello OAuth 2.0 사용자 권한 부여를 테스트 합니다.
OAuth 2.0 권한 부여 서버를 구성 하 고 API toouse 해당 서버를 구성 했으면 toohello 개발자 포털을 이동 하는 API를 호출 하 여 테스트할 수 있습니다.  클릭 **개발자 포털** hello 맨 위 오른쪽 메뉴에 있습니다.

![개발자 포털][api-management-developer-portal-menu]

클릭 **Api** hello 상단 메뉴 및 선택 **에코 API**합니다.

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> 구성 하는 하나의 API가 있는 경우 표시 tooyour 계정 Api를 클릭 한 다음 이동 직접 해당 API에 대 한 toohello 작업.
> 
> 

선택 hello **리소스 가져오기** 작업을 클릭 하 여 **콘솔을 열고**, 선택한 후 **인증 코드** hello 드롭다운 목록에서 합니다.

![콘솔 시작][api-management-open-console]

때 **인증 코드** 은 선택 하면 팝업 창이 hello OAuth 2.0 공급자의 hello 로그인 폼으로 표시 됩니다. 이 예에서 hello 로그인 폼은 Azure Active Directory에서 제공 됩니다.

> [!NOTE]
> 팝업을 사용 하는 경우 tooenable을 묻는 메시지가 표시 됩니다. 사용 안 함 hello 브라우저에서 합니다. 사용 하도록 설정한 후 선택 **인증 코드** 다시 고 hello 로그인 폼이 표시 됩니다.
> 
> 

![로그인][api-management-oauth2-signin]

로그인 하면 hello **요청 헤더** 채워집니다는 `Authorization : Bearer` hello 요청에 권한을 부여 하는 헤더입니다.

![요청 헤더 토큰][api-management-request-header-token]

이 시점에서 매개 변수를 남은 hello에 대 한 hello 원하는 값을 구성한 hello 요청을 제출 합니다. 

## <a name="next-steps"></a>다음 단계
OAuth 2.0 및 API 관리를 사용 하는 방법에 대 한 자세한 내용은 참조 hello 다음 비디오 및 함께 제공 된 [문서](api-management-howto-protect-backend-with-aad.md)합니다.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

