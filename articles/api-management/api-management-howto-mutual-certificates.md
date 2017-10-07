---
title: "클라이언트 인증서 인증-Azure API 관리를 사용 하 여 aaaSecure 백 엔드 서비스 | Microsoft Docs"
description: "클라이언트를 사용 하 여 toosecure 백 엔드 서비스의 Azure API 관리에서 인증 인증서 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>클라이언트를 사용 하 여 toosecure 백 엔드 서비스의 Azure API 관리에서 인증 인증서 방법
API 관리 클라이언트 인증서를 사용 하 여 hello 기능 toosecure 액세스 toohello 백 엔드 서비스의 API 제공 합니다. 이 가이드에서는 toomanage hello API 게시자 포털에서 인증서 방법 등에 tooconfigure API toouse 인증서 tooaccess 백 엔드 서비스에 해당 합니다.

Hello API 관리 REST API를 사용 하 여 인증서를 관리 하는 방법에 대 한 정보를 참조 하십시오. [Azure API 관리 REST API 인증서 엔터티][Azure API Management REST API Certificate entity]합니다.

## <a name="prerequisites"> </a>필수 조건
이 가이드를 보면 어떻게 tooconfigure 프로그램 API 관리 서비스 인스턴스 toouse 클라이언트 인증서 인증 tooaccess hello에 대 한 백 엔드 서비스는 API입니다. 이 항목의 단계를 다음 hello, 전에 클라이언트 인증서 인증에 대해 구성 된 백 엔드 서비스 있어야 ([toothis 문서를 참조 하는 Azure 웹 사이트에서 인증 tooconfigure 인증서] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), 액세스 hello API 관리 게시자 포털에 업로드 하기 위한 hello 인증서에 대 한 인증서와 hello 암호 toohello 하 고 있습니다.

## <a name="step1"> </a>클라이언트 인증서 업로드
시작 tooget 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서. API 관리 게시자 포털 toohello 이동합니다.

![API 게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

클릭 **보안** hello에서 **API 관리** 메뉴를 클릭 한 hello 왼쪽 **클라이언트 인증서**합니다.

![클라이언트 인증서][api-management-security-client-certificates]

새 인증서를 tooupload 클릭 **인증서 업로드**합니다.

![인증서 업로드][api-management-upload-certificate]

Tooyour 인증서를 찾은 다음 hello 인증서에 대 한 hello 암호를 입력 합니다.

> hello 인증서에 있어야 **.pfx** 형식입니다. 자체 서명된 인증서도 사용할 수 있습니다.
> 
> 

![인증서 업로드][api-management-upload-certificate-form]

클릭 **업로드** tooupload hello 인증서입니다.

> hello 인증서 암호는이 이번에 유효성이 검사 됩니다. 암호가 잘못된 경우 오류 메시지가 표시됩니다.
> 
> 

![업로드된 인증서][api-management-certificate-uploaded]

Hello에 나타나는 hello 인증서를 업로드 한 후 **클라이언트 인증서** 탭 합니다. 인증서가 여러 개 있는 경우 hello 주체의 적어 두거나 hello 다음에서 살펴본 것 처럼 인증서 API toouse를 구성할 때 사용 되는 tooselect hello 인증서는는 hello 손도장의 마지막 네 문자가 hello [구성 프로그램 API toouse 게이트웨이 인증을 위해 클라이언트 인증서] [ Configure an API toouse a client certificate for gateway authentication] 섹션.

> 이 FAQ에 설명 된 hello 단계를 수행 하는 예를 들어 자체 서명 된 인증서를 사용 하면 인증서 체인 유효성 검사 해제 tooturn [항목](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)합니다.
> 
> 

## <a name="step1a"> </a>클라이언트 인증서 삭제
toodelete 인증서를 클릭 하 여 **삭제** hello 원하는 인증서 옆에 있는 합니다.

![인증서 삭제][api-management-certificate-delete]

클릭 **예, 삭제할** tooconfirm 합니다.

![삭제 확인][api-management-confirm-delete]

Hello 인증서는 API에서 사용 중인 경우 경고 화면이 표시 됩니다. hello를 먼저 제거 해야 toodelete hello 인증서 것 구성된 toouse 있는 모든 Api에서 인증서입니다.

![삭제 확인][api-management-confirm-delete-policy]

## <a name="step2"></a>API toouse 게이트웨이 인증을 위해 클라이언트 인증서를 구성 합니다.
클릭 **Api** hello에서 **API 관리** 메뉴 hello에 남아 있는 원하는 hello API의 hello 이름을 클릭 하 고 hello 클릭 **보안** 탭 합니다.

![API 보안][api-management-api-security]

선택 **클라이언트 인증서** hello에서 **자격 증명으로** 드롭 다운 목록입니다.

![클라이언트 인증서][api-management-mutual-certificates]

선택 hello hello에서 원하는 인증서 **클라이언트 인증서** 드롭 다운 목록입니다. 여러 인증서가 있는 경우 hello 주체를 살펴볼 수도 있고 hello hello 지문 안녕하세요 이전 섹션 toodetermine hello 올바른 인증서에 설명 된 대로 마지막 4 자를 수 있습니다.

![인증서 선택][api-management-select-certificate]

클릭 **저장** toosave hello 구성 변경 toohello API입니다.

> 이 변경 내용이 즉시 적용 됩니다 및 해당 API의 toooperations ´ ֲ 호출 hello hello 백 엔드 서버에서 인증서 tooauthenticate 합니다.
> 
> 

![API 변경 내용 저장][api-management-save-api]

> API의 hello 백 엔드 서비스에 대 한 게이트웨이 인증용 인증서를 지정 하면 해당 API에 대 한 hello 정책의 일부가 됩니다 하 고 hello 정책 편집기에서 볼 수 있습니다.
> 
> 

![인증서 정책][api-management-certificate-policy]

## <a name="next-steps"></a>다음 단계
다른 방법으로 toosecure 대 한 자세한 내용은 기본 또는 공유 암호 인증 HTTP와 같은 백 엔드 서비스에 hello 다음 비디오를 참조 합니다.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



