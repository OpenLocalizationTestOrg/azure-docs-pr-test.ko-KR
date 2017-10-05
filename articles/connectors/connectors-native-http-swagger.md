---
title: "Azure Logic Apps용 HTTP + Swagger 커넥터를 사용하여 REST 끝점 호출 | Microsoft Docs"
description: "HTTP + Swagger 커넥터를 통해 Logic Apps에서 REST 끝점에 연결"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="b482d-103">HTTP + Swagger 동작 시작</span><span class="sxs-lookup"><span data-stu-id="b482d-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="b482d-104">논리 앱 워크플로에서 HTTP + Swagger 동작을 사용할 경우 [Swagger 문서](https://swagger.io)를 통해 REST 끝점에 대한 최고급 커넥터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="b482d-105">최고급 논리 앱 디자이너 환경이 있는 모든 REST 끝점을 호출하도록 Logic Apps를 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="b482d-106">커넥터로 Logic Apps를 만드는 방법을 알아보려면 [새 논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b482d-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="b482d-107">HTTP + Swagger를 트리거 또는 동작으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="b482d-108">HTTP + Swagger 트리거 및 동작은 [HTTP 동작](connectors-native-http.md)과 동일하게 작동하지만 [swagger 메타데이터](https://swagger.io)의 API 구조 및 출력을 노출하여 논리 앱 디자이너에 더 나은 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="b482d-109">HTTP + Swagger 커넥터를 트리거로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="b482d-110">폴링 트리거를 구현하려면 [Logic Apps에서 다른 API, 서비스 및 시스템을 호출하기 위한 사용자 지정 API 만들기](../logic-apps/logic-apps-create-api-app.md#polling-triggers)에 설명된 폴링 패턴을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="b482d-111">[논리 앱 트리거 및 동작](connectors-overview.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="b482d-112">다음은 논리 앱에서 HTTP + Swagger 작업을 워크플로의 동작으로 사용하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="b482d-113">**새 단계** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="b482d-114">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="b482d-115">동작 검색 상자에 **swagger** 를 입력하여 HTTP + Swagger 동작을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![HTTP + Swagger 동작 선택](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="b482d-117">Swagger 문서에 대한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="b482d-118">논리 앱 디자이너에서 작동하려면 URL이 HTTPS 끝점이어야 하고 CORS를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="b482d-119">Swagger 문서가 이 요구 사항을 충족하지 않는 경우 [CORS가 설정된 Azure Storage를 사용](#hosting-swagger-from-storage) 하여 문서를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="b482d-120">**다음** 을 클릭하여 Swagger 문서를 읽고 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="b482d-121">HTTP 호출에 필요한 모든 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![HTTP 작업 완료](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="b482d-123">논리 앱을 저장하고 게시하려면 디자이너 도구 모음에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="b482d-124">Azure Storage에서 Swagger 호스트</span><span class="sxs-lookup"><span data-stu-id="b482d-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="b482d-125">호스트되지 않거나 디자이너에 대한 보안 및 원본 간 요구 사항을 충족하지 않는 Swagger 문서를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="b482d-126">이 문제를 해결하기 위해 Azure Storage에서 Swagger 문서를 저장하고 CORS를 사용하도록 설정하여 문서를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="b482d-127">Azure Storage에서 Swagger를 생성, 구성 및 저장하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="b482d-128">[Azure Blob 저장소를 사용하여 Azure Storage 계정을 만듭니다](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b482d-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="b482d-129">이 단계를 수행하려면 **공용 액세스**에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="b482d-130">Blob에 대해 CORS를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="b482d-131">이 설정을 자동으로 구성하려면 [이 PowerShell 스크립트](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="b482d-132">Blob에 Swagger 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="b482d-133">[Azure Portal](https://portal.azure.com) 또는 [Azure Storage 탐색기](http://storageexplorer.com/)와 같은 도구에서 이 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="b482d-134">Azure Blob 저장소의 문서에 대한 HTTPS 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="b482d-135">이 링크에서는 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="b482d-136">기술 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b482d-136">Technical details</span></span>
<span data-ttu-id="b482d-137">이 HTTP + Swagger 커넥터가 지원하는 트리거 및 동작에 대한 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="b482d-138">HTTP + Swagger 트리거</span><span class="sxs-lookup"><span data-stu-id="b482d-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="b482d-139">트리거는 논리 앱에서 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="b482d-140">트리거에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b482d-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="b482d-141">HTTP + Swagger 커넥터에는 1개의 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="b482d-142">트리거</span><span class="sxs-lookup"><span data-stu-id="b482d-142">Trigger</span></span> | <span data-ttu-id="b482d-143">설명</span><span class="sxs-lookup"><span data-stu-id="b482d-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b482d-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="b482d-144">HTTP + Swagger</span></span> |<span data-ttu-id="b482d-145">HTTP 호출을 수행하고 응답 콘텐츠를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="b482d-146">HTTP + Swagger 동작</span><span class="sxs-lookup"><span data-stu-id="b482d-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="b482d-147">동작은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="b482d-148">작업에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="b482d-149">HTTP + Swagger 커넥터에는 1개의 가능한 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="b482d-150">작업</span><span class="sxs-lookup"><span data-stu-id="b482d-150">Action</span></span> | <span data-ttu-id="b482d-151">설명</span><span class="sxs-lookup"><span data-stu-id="b482d-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b482d-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="b482d-152">HTTP + Swagger</span></span> |<span data-ttu-id="b482d-153">HTTP 호출을 수행하고 응답 콘텐츠를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="b482d-154">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b482d-154">Action details</span></span>
<span data-ttu-id="b482d-155">HTTP + Swagger 커넥터에는 1개의 가능한 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="b482d-156">다음은 각 동작, 해당 필수 및 옵션 입력 필드, 사용과 관련된 해당 출력 세부 정보에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="b482d-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="b482d-157">HTTP + Swagger</span></span>
<span data-ttu-id="b482d-158">Swagger 메타데이터를 지원하는 HTTP 아웃바운드 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="b482d-159">별표(*)는 필수 필드를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="b482d-160">표시 이름</span><span class="sxs-lookup"><span data-stu-id="b482d-160">Display name</span></span> | <span data-ttu-id="b482d-161">속성 이름</span><span class="sxs-lookup"><span data-stu-id="b482d-161">Property name</span></span> | <span data-ttu-id="b482d-162">설명</span><span class="sxs-lookup"><span data-stu-id="b482d-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b482d-163">Method*</span><span class="sxs-lookup"><span data-stu-id="b482d-163">Method*</span></span> |<span data-ttu-id="b482d-164">메서드</span><span class="sxs-lookup"><span data-stu-id="b482d-164">method</span></span> |<span data-ttu-id="b482d-165">사용할 HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="b482d-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="b482d-166">URI*</span><span class="sxs-lookup"><span data-stu-id="b482d-166">URI*</span></span> |<span data-ttu-id="b482d-167">uri</span><span class="sxs-lookup"><span data-stu-id="b482d-167">uri</span></span> |<span data-ttu-id="b482d-168">HTTP 요청에 대한 URI</span><span class="sxs-lookup"><span data-stu-id="b482d-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="b482d-169">헤더</span><span class="sxs-lookup"><span data-stu-id="b482d-169">Headers</span></span> |<span data-ttu-id="b482d-170">헤더</span><span class="sxs-lookup"><span data-stu-id="b482d-170">headers</span></span> |<span data-ttu-id="b482d-171">포함할 HTTP 헤더의 JSON 개체</span><span class="sxs-lookup"><span data-stu-id="b482d-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="b482d-172">본문</span><span class="sxs-lookup"><span data-stu-id="b482d-172">Body</span></span> |<span data-ttu-id="b482d-173">본문</span><span class="sxs-lookup"><span data-stu-id="b482d-173">body</span></span> |<span data-ttu-id="b482d-174">HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="b482d-174">The HTTP request body.</span></span> |
| <span data-ttu-id="b482d-175">인증</span><span class="sxs-lookup"><span data-stu-id="b482d-175">Authentication</span></span> |<span data-ttu-id="b482d-176">authentication</span><span class="sxs-lookup"><span data-stu-id="b482d-176">authentication</span></span> |<span data-ttu-id="b482d-177">요청에 사용할 인증</span><span class="sxs-lookup"><span data-stu-id="b482d-177">Authentication to use for request.</span></span> <span data-ttu-id="b482d-178">자세한 내용은 [HTTP 커넥터](connectors-native-http.md#authentication)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b482d-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="b482d-179">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="b482d-179">**Output details**</span></span>

<span data-ttu-id="b482d-180">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="b482d-180">HTTP response</span></span>

| <span data-ttu-id="b482d-181">속성 이름</span><span class="sxs-lookup"><span data-stu-id="b482d-181">Property Name</span></span> | <span data-ttu-id="b482d-182">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="b482d-182">Data type</span></span> | <span data-ttu-id="b482d-183">설명</span><span class="sxs-lookup"><span data-stu-id="b482d-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b482d-184">headers</span><span class="sxs-lookup"><span data-stu-id="b482d-184">Headers</span></span> |<span data-ttu-id="b482d-185">object</span><span class="sxs-lookup"><span data-stu-id="b482d-185">object</span></span> |<span data-ttu-id="b482d-186">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="b482d-186">Response headers</span></span> |
| <span data-ttu-id="b482d-187">본문</span><span class="sxs-lookup"><span data-stu-id="b482d-187">Body</span></span> |<span data-ttu-id="b482d-188">object</span><span class="sxs-lookup"><span data-stu-id="b482d-188">object</span></span> |<span data-ttu-id="b482d-189">응답 개체</span><span class="sxs-lookup"><span data-stu-id="b482d-189">Response object</span></span> |
| <span data-ttu-id="b482d-190">상태 코드</span><span class="sxs-lookup"><span data-stu-id="b482d-190">Status Code</span></span> |<span data-ttu-id="b482d-191">int</span><span class="sxs-lookup"><span data-stu-id="b482d-191">int</span></span> |<span data-ttu-id="b482d-192">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="b482d-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="b482d-193">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="b482d-193">HTTP responses</span></span>
<span data-ttu-id="b482d-194">다양한 작업을 호출할 때 특정 응답이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="b482d-195">다음 표에서는 해당 응답 및 설명을 대략적으로 요약해서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b482d-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="b482d-196">Name</span><span class="sxs-lookup"><span data-stu-id="b482d-196">Name</span></span> | <span data-ttu-id="b482d-197">설명</span><span class="sxs-lookup"><span data-stu-id="b482d-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b482d-198">200</span><span class="sxs-lookup"><span data-stu-id="b482d-198">200</span></span> |<span data-ttu-id="b482d-199">확인</span><span class="sxs-lookup"><span data-stu-id="b482d-199">OK</span></span> |
| <span data-ttu-id="b482d-200">202</span><span class="sxs-lookup"><span data-stu-id="b482d-200">202</span></span> |<span data-ttu-id="b482d-201">수락됨</span><span class="sxs-lookup"><span data-stu-id="b482d-201">Accepted</span></span> |
| <span data-ttu-id="b482d-202">400</span><span class="sxs-lookup"><span data-stu-id="b482d-202">400</span></span> |<span data-ttu-id="b482d-203">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="b482d-203">Bad request</span></span> |
| <span data-ttu-id="b482d-204">401</span><span class="sxs-lookup"><span data-stu-id="b482d-204">401</span></span> |<span data-ttu-id="b482d-205">권한 없음</span><span class="sxs-lookup"><span data-stu-id="b482d-205">Unauthorized</span></span> |
| <span data-ttu-id="b482d-206">403</span><span class="sxs-lookup"><span data-stu-id="b482d-206">403</span></span> |<span data-ttu-id="b482d-207">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="b482d-207">Forbidden</span></span> |
| <span data-ttu-id="b482d-208">404</span><span class="sxs-lookup"><span data-stu-id="b482d-208">404</span></span> |<span data-ttu-id="b482d-209">찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="b482d-209">Not Found</span></span> |
| <span data-ttu-id="b482d-210">500</span><span class="sxs-lookup"><span data-stu-id="b482d-210">500</span></span> |<span data-ttu-id="b482d-211">내부 서버 오류.</span><span class="sxs-lookup"><span data-stu-id="b482d-211">Internal server error.</span></span> <span data-ttu-id="b482d-212">알 수 없는 오류 발생.</span><span class="sxs-lookup"><span data-stu-id="b482d-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="b482d-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b482d-213">Next steps</span></span>

* [<span data-ttu-id="b482d-214">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b482d-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="b482d-215">다른 커넥터 찾기</span><span class="sxs-lookup"><span data-stu-id="b482d-215">Find other connectors</span></span>](apis-list.md)