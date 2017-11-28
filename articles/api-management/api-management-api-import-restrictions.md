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
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="4853a-103">API 가져오기 제한 사항 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4853a-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="4853a-104">다음 목록 정보</span><span class="sxs-lookup"><span data-stu-id="4853a-104">About this list</span></span>
<span data-ttu-id="4853a-105">동안 대처 하는 Azure API 관리 API 가져오기는 안전 tooensure 이루어집니다 문제 없이 최대한,에서는 경우에 따라 제한 사항이 적용 않거나 toobe 성공적으로 가져오기 전에 수정 해야 하는 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="4853a-106">이 문서에서는 이러한 문서 hello API의 hello 가져오기 형식에 따라 organised 합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="4853a-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="4853a-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="4853a-108">일반적으로 개방형 API 문서를 가져오는 과정에서 오류가 발생 하는 경우 확인 하십시오 것-검사 한 hello 디자이너를 사용 하 여 hello 새 Azure 포털 (디자인-프런트 엔드-API 사양 편집기 열기)에서 또는 세 번째와 자가 도구와 같은 중 <a href="http://www.swagger.io"> 편집기 swagger</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="4853a-109">**호스트 이름** 호스트 이름 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="4853a-110">**기본 경로** 기본 경로 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="4853a-111">**스키마** 스키마 배열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="4853a-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="4853a-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="4853a-113">WSDL 파일 SOAP 통과 Api를 사용 하는 toogenerate 있거나 SOAP-REST API의 백 엔드 hello으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="4853a-114">**WSDL:Import** 현재 이 특성을 사용한 API는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="4853a-115">고객은 하나의 문서로 가져온 hello 요소를 병합 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="4853a-116">**여러 부분으로 된 메시지**는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="4853a-117">**WCF wsHttpBinding** Windows Communication Foundation으로 생성된 SOAP 서비스는 basicHttpBinding을 사용해야 합니다. wsHttpBinding은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="4853a-118">**MTOM** MTOM을 사용한 서비스는 <em>작동할 수 있습니다</em>.</span><span class="sxs-lookup"><span data-stu-id="4853a-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="4853a-119">현재는 공식적으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="4853a-120">**재귀** 않은 형식 정의 재귀적으로 (예: tooan 배열 자체 참조)는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="4853a-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="4853a-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="4853a-122">현재는 알려진 WADL 가져오기 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4853a-122">There are no known WADL import issues currently.</span></span>


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
