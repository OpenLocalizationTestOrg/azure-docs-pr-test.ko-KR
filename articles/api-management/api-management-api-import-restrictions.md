---
title: "Azure API 관리 API의 알려진 문제와 aaaRestrictions 가져오기 | Microsoft Docs"
description: "정보 가져오기 hello Open API, WSDL 또는 WADL 형식을 사용 하 여 Azure API 관리에 대 한 제한 사항 및 알려진된 문제입니다."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>API 가져오기 제한 사항 및 알려진 문제
## <a name="about-this-list"></a>다음 목록 정보
동안 대처 하는 Azure API 관리 API 가져오기는 안전 tooensure 이루어집니다 문제 없이 최대한,에서는 경우에 따라 제한 사항이 적용 않거나 toobe 성공적으로 가져오기 전에 수정 해야 하는 문제를 식별 합니다. 이 문서에서는 이러한 문서 hello API의 hello 가져오기 형식에 따라 organised 합니다.

## <a name="open-api"> </a>Open API/Swagger
일반적으로 개방형 API 문서를 가져오는 과정에서 오류가 발생 하는 경우 확인 하십시오 것-검사 한 hello 디자이너를 사용 하 여 hello 새 Azure 포털 (디자인-프런트 엔드-API 사양 편집기 열기)에서 또는 세 번째와 자가 도구와 같은 중 <a href="http://www.swagger.io"> 편집기 swagger</a>합니다.

* **호스트 이름** 호스트 이름 특성이 필요합니다.
* **기본 경로** 기본 경로 특성이 필요합니다.
* **스키마** 스키마 배열이 필요합니다. 

## <a name="wsdl"> </a>WSDL
WSDL 파일 SOAP 통과 Api를 사용 하는 toogenerate 있거나 SOAP-REST API의 백 엔드 hello으로 제공 합니다.

* **WSDL:Import** 현재 이 특성을 사용한 API는 지원하지 않습니다. 고객은 하나의 문서로 가져온 hello 요소를 병합 해야 합니다.
* **여러 부분으로 된 메시지**는 현재 지원되지 않습니다.
* **WCF wsHttpBinding** Windows Communication Foundation으로 생성된 SOAP 서비스는 basicHttpBinding을 사용해야 합니다. wsHttpBinding은 지원되지 않습니다.
* **MTOM** MTOM을 사용한 서비스는 <em>작동할 수 있습니다</em>. 현재는 공식적으로 지원되지 않습니다.
* **재귀** 않은 형식 정의 재귀적으로 (예: tooan 배열 자체 참조)는 지원 되지 않습니다.

## <a name="wadl"> </a>WADL
현재는 알려진 WADL 가져오기 문제가 없습니다.


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
