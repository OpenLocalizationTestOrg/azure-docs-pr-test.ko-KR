---
title: "Azure API Management 가져오기에서 제한 사항 및 알려진 문제 | Microsoft Docs"
description: "Open API, WSDL 또는 WADL 형식을 사용하여 Azure API Management로 가져오기 시 알려진 문제 및 제한 사항입니다."
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
ms.openlocfilehash: ac799d66b5038c207413086b0fa71239ff2a332f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="673be-103">API 가져오기 제한 사항 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="673be-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="673be-104">다음 목록 정보</span><span class="sxs-lookup"><span data-stu-id="673be-104">About this list</span></span>
<span data-ttu-id="673be-105">API를 Azure API Management로 가능한 완벽하고 문제 없이 가져올 수 있도록 최선의 노력을 하고 있지만 간혹 제한 사항이 적용되거나 성공적으로 가져오기 위해 수정이 필요한 문제가 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="673be-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span></span> <span data-ttu-id="673be-106">이 문서에서는 이러한 내용을 API의 가져오기 형식별로 구성하여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="673be-106">This article documents these, organised by the import format of the API.</span></span>

## <span data-ttu-id="673be-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="673be-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="673be-108">일반적으로 Open API 문서를 가져오는 중 오류를 수신하면 새 Azure Portal에서 디자이너를 사용하거나(Design - Front End - Open API Specification Editor) <a href="http://www.swagger.io">Swagger Editor</a>와 같은 타사 도구를 사용하여 유효성을 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="673be-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="673be-109">**호스트 이름** 호스트 이름 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="673be-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="673be-110">**기본 경로** 기본 경로 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="673be-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="673be-111">**스키마** 스키마 배열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="673be-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="673be-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="673be-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="673be-113">SOAP 통과 API를 생성하는 데 WSDL 파일이 사용되며 SOAP-to-REST API의 백 엔드로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="673be-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="673be-114">**WSDL:Import** 현재 이 특성을 사용한 API는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="673be-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="673be-115">고객은 가져온 요소를 문서 하나로 병합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="673be-115">Customers should merge the imported elements into one document.</span></span>
* <span data-ttu-id="673be-116">**여러 부분으로 된 메시지**는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="673be-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="673be-117">**WCF wsHttpBinding** Windows Communication Foundation으로 생성된 SOAP 서비스는 basicHttpBinding을 사용해야 합니다. wsHttpBinding은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="673be-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="673be-118">**MTOM** MTOM을 사용한 서비스는 <em>작동할 수 있습니다</em>.</span><span class="sxs-lookup"><span data-stu-id="673be-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="673be-119">현재는 공식적으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="673be-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="673be-120">재귀적으로 정의된(예: 자체의 배열을 참조) **재귀** 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="673be-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span></span>

## <span data-ttu-id="673be-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="673be-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="673be-122">현재는 알려진 WADL 가져오기 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="673be-122">There are no known WADL import issues currently.</span></span>


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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
