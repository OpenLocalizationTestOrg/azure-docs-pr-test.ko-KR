---
title: "Azure API 관리에는 API aaaImport | Microsoft Docs"
description: "자세한 방법을 tooimport API 및 Azure API 관리에 해당 작업이 있습니다."
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="585b3-103">어떻게 tooimport hello Azure API 관리에서 작업을 사용 하는 API의 정의</span><span class="sxs-lookup"><span data-stu-id="585b3-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="585b3-104">API 관리에서 새로운 Api 만들 수 있으며 한 번에 hello 작업과 함께 hello 작업을 수동으로 추가할 또는 hello API 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="585b3-105">Api 및 해당 작업 형식에 따라 hello를 사용 하 여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="585b3-106">WADL</span><span class="sxs-lookup"><span data-stu-id="585b3-106">WADL</span></span>
* <span data-ttu-id="585b3-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="585b3-107">Swagger</span></span>

<span data-ttu-id="585b3-108">이 가이드에서는 새로운 API를 만들고 그 작업과 함께 한번에 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="585b3-109">수동으로 API를 만들고 추가 작업에 대 한 자세한 내용은 참조 하십시오. [어떻게 toocreate Api] [ How toocreate APIs] 및 [어떻게 tooadd 작업 tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="585b3-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="585b3-110"><a name="import-api"> </a>API 가져오기</span><span class="sxs-lookup"><span data-stu-id="585b3-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="585b3-111">Api 생성 및 hello 게시자 포털에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="585b3-112">tooaccess 게시자 포털을 클릭 하 여 hello **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="585b3-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="585b3-113">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="585b3-115">클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **API 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![API 가져오기][api-management-import-apis]

<span data-ttu-id="585b3-117">hello **가져오기 API** 창에 toohello 세 가지 방법 tooprovide hello API 사양에 해당 하는 세 가지 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="585b3-118">**클립보드에서** hello 지정 된 텍스트 상자에 toopaste hello API 지정을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="585b3-119">**파일에서** hello API 사양을 포함 하는 toobrowse tooand 선택 hello 파일 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="585b3-120">**URL에서** hello API에 대 한 toosupply hello URL toohello 사양이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![API 가져오기 형식][api-management-import-api-clipboard]

<span data-ttu-id="585b3-122">Hello API 사양을 제공한 후 hello 라디오 단추를 사용 하 여 hello 오른쪽 tooindicate hello 사양 형식을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="585b3-123">hello 다음 형식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-123">hello following formats are supported.</span></span>

* <span data-ttu-id="585b3-124">WADL</span><span class="sxs-lookup"><span data-stu-id="585b3-124">WADL</span></span>
* <span data-ttu-id="585b3-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="585b3-125">Swagger</span></span>

<span data-ttu-id="585b3-126">이제 **Web API URL 접미사**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="585b3-127">API 관리 서비스에 대 한 추가 toohello 기준 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="585b3-128">hello 기본 URL은 API 관리 서비스의 각 인스턴스에서 호스트 되는 모든 Api에 대 한 일반적인입니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="585b3-129">API 관리의 접미사로 Api를 구별 하 고 따라서 hello 접미사는 특정 API 관리 서비스 인스턴스에 모든 API에 대 한 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="585b3-130">모든 값을 입력 한 후 클릭 **저장** toocreate hello API 및 hello 작업에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="585b3-131">Swagger 형식의 기본 계산기 API의 자습서는 [Azure API 관리에서 첫 번째 API 관리](api-management-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="585b3-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="585b3-132"><a name="export-api"> </a> API 내보내기</span><span class="sxs-lookup"><span data-stu-id="585b3-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="585b3-133">또한 tooimporting에서 새로운 Api hello 게시자 포털에서 Api의 hello 정의 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="585b3-134">toodo 이므로, 클릭 **내보내기 API** hello에서 **요약 탭** 의 프로그램 **API**합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![API 내보내기][api-management-export-api]

<span data-ttu-id="585b3-136">API는 WADL 또는 Swagger를 사용하여 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="585b3-137">Hello 원하는 형식 선택를 클릭 **저장**, toosave hello 파일에서 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![API 내보내기 형식][api-management-export-api-format]

## <span data-ttu-id="585b3-139"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="585b3-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="585b3-140">API 만들어집니다 가져온 hello 작업을 검토 하 고 구성할 수 추가 설정을 hello API tooa 제품을 추가 하 고 개발자를 위해 사용할 수 있도록 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b3-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="585b3-141">자세한 내용은 hello 가이드를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="585b3-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="585b3-142">[어떻게 tooconfigure API 설정][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="585b3-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="585b3-143">[어떻게 toocreate 및 제품 게시][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="585b3-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
