---
title: "aaaHow toocreate Azure API 관리에서 Api"
description: "자세한 내용은 방법 toocreate 하 고 Azure API 관리에서 Api를 구성 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>어떻게 toocreate Azure API 관리에서 Api
API 관리에서 API는 클라이언트 응용 프로그램이 호출할 수 있는 작업 집합을 나타냅니다. 새 Api hello 게시자 포털에 만들어지며 다음 hello 필요한 작업은 추가 됩니다. Hello 작업 추가 되 면 hello API tooa 제품 추가 및 게시할 수 있습니다. API 게시 되 면 구독 된 tooand 개발자가 사용 가능 합니다.

이 가이드에서는 hello 프로세스 hello 첫 번째 단계: 어떻게 toocreate 및 API 관리에서 새로운 API를 구성 합니다. 작업 추가 및 제품 게시에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooadd 작업 tooan API] [ How tooadd operations tooan API] 및 [어떻게 toocreate 및 제품 게시] [ How toocreate and publish a product].

## <a name="create-new-api"> </a>새 API 만들기
Api 생성 및 hello 게시자 포털에서 구성 됩니다. tooaccess 게시자 포털을 클릭 하 여 hello **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.

![게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **API 추가**합니다.

![API 만들기][api-management-create-api]

사용 하 여 hello **새 API 추가** 창 tooconfigure hello 새로운 API입니다.

![새 API 추가][api-management-add-new-api]

다음 필드는 hello 사용 되는 tooconfigure hello 새 API 사용 됩니다.

* **Web API 이름** hello API에 대 한 고유 하며 구분 가능한 이름을 제공 합니다. Hello 개발자 및 게시자 포털에 표시 됩니다.
* **웹 서비스 URL** 참조 hello HTTP 서비스 hello API를 구현 합니다. API 관리 toothis 주소 요청을 전달합니다.
* **웹 API URL 접미사** 추가 toohello hello API 관리 서비스에 대 한 기본 URL입니다. hello 기본 URL은 API 관리 서비스 인스턴스에 의해 호스트 되는 모든 Api에 대 한 일반적인입니다. API 관리의 접미사로 Api를 구별 하 고 따라서 hello 접미사를 지정된 된 게시자에 대 한 모든 API에 대 한 고유 해야 합니다.
* **웹 API URL 구성표** 프로토콜을 사용 하는 tooaccess hello API 될 수 있는지 결정 합니다. 기본적으로 HTTPS가 지정됩니다.
* toooptionally이 새 API tooa 제품 추가, hello 클릭 **(선택 사항) 제품** 드롭 다운 하 고 제품을 선택 합니다. 이 단계는 반복 된 여러 번 tooadd hello API toomultiple 제품 될 수 있습니다.

Hello 원하는 값이 구성 되어 클릭 **저장**합니다. Hello 새로운 API를 만든 후 hello hello API에 대 한 요약 페이지에에서 표시 됩니다 hello 게시자 포털.

![API 요약][api-management-api-summary]

## <a name="configure-api-settings"> </a>API 설정 구성
Hello를 사용할 수 있습니다 **설정** tooverify 탭 및 API에 대 한 hello 구성을 편집 합니다. **Web API 이름**, **웹 서비스 URL**, 및 **웹 API URL 접미사** 는 처음 여기에서 설정 hello API 만들고 수정할 수 있습니다. **설명** 대 한 선택적 설명을 제공 하 고 **웹 API URL 구성표** 프로토콜을 사용 하는 tooaccess hello API 될 수 있는지 결정 합니다.

![API 설정][api-management-api-settings]

tooconfigure 게이트웨이 인증 hello 백 엔드 서비스 구현 hello API에 대 한 선택 hello **보안** 탭 hello **자격 증명으로** 드롭 다운 사용된 tooconfigure 수 **HTTP 기본** 또는 **클라이언트 인증서** 인증 합니다. toouse HTTP 기본 인증을 간단히 hello 필요한 자격 증명을 입력 합니다. 클라이언트 인증서 인증을 사용 하는 방법은 참조 하십시오. [클라이언트를 사용 하 여 toosecure 백 엔드 서비스의 Azure API 관리에서 인증 인증서 방법을][How toosecure back-end services using client certificate authentication in Azure API Management]합니다.

hello **보안** 탭 사용된 tooconfigure 될 수도 있습니다 **사용자 권한 부여** OAuth 2.0을 사용 합니다. 자세한 내용은 참조 [tooauthorize 개발자 방법을 사용 하 여 계정을 Azure API 관리에서 OAuth 2.0][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]합니다.

![기본 인증 설정][api-management-api-settings-credentials]

클릭 **저장** toosave 변경 사항은 toohello API 설정 합니다.

## <a name="next-steps"> </a>다음 단계
API 만들고 구성 하는 hello 설정을 hello 다음 단계는 tooadd hello operations toohello API hello API tooa 제품을 추가 하 고 개발자에 사용할 수 있도록 게시 합니다. 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [어떻게 tooadd 작업 tooan API][How tooadd operations tooan API]
* [어떻게 toocreate 및 제품 게시][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
