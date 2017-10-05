---
title: "Azure API Management에 API 가져오기 | Microsoft Docs"
description: "Azure API Management에 API 및 해당 작업을 가져오는 방법에 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="897f4-103">Azure API 관리에서 작업과 함께 API의 정의를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="897f4-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="897f4-104">API 관리에서 새 API를 만들고 작업을 수동으로 추가하거나 API를 작업과 함께 한 번에 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="897f4-105">API 및 그 작업은 다음 형식으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="897f4-106">WADL</span><span class="sxs-lookup"><span data-stu-id="897f4-106">WADL</span></span>
* <span data-ttu-id="897f4-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="897f4-107">Swagger</span></span>

<span data-ttu-id="897f4-108">이 가이드에서는 새로운 API를 만들고 그 작업과 함께 한번에 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="897f4-109">API를 수동으로 만들고 작업을 추가하는 방법에 대해서는 [API를 만드는 방법][How to create APIs] 및 [API에 작업을 추가하는 방법][How to add operations to an API]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="897f4-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="897f4-110"><a name="import-api"> </a>API 가져오기</span><span class="sxs-lookup"><span data-stu-id="897f4-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="897f4-111">게시자 포털에서 API를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="897f4-112">게시자 포털에 액세스하려면 API 관리 서비스에 대해 Azure Portal에서 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="897f4-113">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="897f4-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="897f4-115">왼쪽의 **API Management** 메뉴에서 **API**를 클릭한 다음 **API 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![API 가져오기][api-management-import-apis]

<span data-ttu-id="897f4-117">**API 가져오기** 창에는 3개의 탭이 있으며 각기 API 사양을 제공하는 3가지 방법에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="897f4-118">**클립보드에서** 지정된 입력란에 API 사양을 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="897f4-119">**파일에서** API 사양을 포함하는 파일로 이동하여 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="897f4-120">**URL에서** API의 사양에 URL을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![API 가져오기 형식][api-management-import-api-clipboard]

<span data-ttu-id="897f4-122">API 사양을 제공한 후 오른쪽의 라디오 단추를 사용하여 사양 형식을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="897f4-123">다음 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-123">The following formats are supported.</span></span>

* <span data-ttu-id="897f4-124">WADL</span><span class="sxs-lookup"><span data-stu-id="897f4-124">WADL</span></span>
* <span data-ttu-id="897f4-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="897f4-125">Swagger</span></span>

<span data-ttu-id="897f4-126">이제 **Web API URL 접미사**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="897f4-127">이 접미사는 API 관리 서비스의 기본 URL에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="897f4-128">기본 URL은 API 관리 서비스의 각 인스턴스에서 호스트되는 모든 API에 공통으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="897f4-129">API 관리는 접미사를 사용하여 API를 구분하므로, 접미사는 특정 API 관리 서비스 인스턴스의 모든 API에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="897f4-130">모든 값을 입력한 후에는 **저장** 을 클릭하여 API 및 연결된 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="897f4-131">Swagger 형식의 기본 계산기 API의 자습서는 [Azure API 관리에서 첫 번째 API 관리](api-management-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="897f4-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="897f4-132"><a name="export-api"> </a> API 내보내기</span><span class="sxs-lookup"><span data-stu-id="897f4-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="897f4-133">새 API를 가져올 뿐만 아니라 게시자 포털에서 API에 대한 정의를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="897f4-134">그렇게 하려면 **API**의 **요약 탭**에서 **API 내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![API 내보내기][api-management-export-api]

<span data-ttu-id="897f4-136">API는 WADL 또는 Swagger를 사용하여 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="897f4-137">원하는 형식을 선택하고, **저장**을 클릭하고, 파일을 저장할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![API 내보내기 형식][api-management-export-api-format]

## <span data-ttu-id="897f4-139"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="897f4-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="897f4-140">API를 만들고 작업을 가져온 후 추가 설정을 검토 및 구성하고, 제품에 API를 추가하고, 개발자가 사용할 수 있도록 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897f4-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="897f4-141">자세한 내용은 다음 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="897f4-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="897f4-142">[API 설정을 구성하는 방법][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="897f4-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="897f4-143">[제품을 만들고 게시하는 방법][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="897f4-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
