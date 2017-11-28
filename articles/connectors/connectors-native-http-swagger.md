---
title: "HTTP + Swagger aaaCall REST 끝점에 대 한 Azure 논리 앱 커넥터 | Microsoft Docs"
description: "Swagger 통해 안녕하세요 HTTP + Swagger 커넥터를 사용 하 여 논리 앱에서 tooREST 끝점 연결"
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
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="b34c1-103">안녕하세요 HTTP + Swagger 작업 시작</span><span class="sxs-lookup"><span data-stu-id="b34c1-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="b34c1-104">통해 첫 번째 클래스 커넥터 tooany REST 끝점을 만들 수는 [Swagger 문서](https://swagger.io) 때 논리 앱 워크플로 hello HTTP + Swagger 동작을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="b34c1-105">또한 논리 앱 toocall 모든 REST 끝점은 첫 번째 클래스 논리가 응용 프로그램 디자이너 환경을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="b34c1-106">커넥터를 사용 하 여 논리 앱 toocreate 참조 toolearn [새 논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="b34c1-107">HTTP + Swagger를 트리거 또는 동작으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="b34c1-108">안녕하세요 HTTP + Swagger 트리거와 작업이 바뀐 작업 hello 동일 hello로 [HTTP 동작](connectors-native-http.md) hello API 구조 및 hello의 출력을 노출 하 여 논리 앱 디자이너에서 향상 된 환경을 제공 하지만 [Swagger 메타 데이터](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="b34c1-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="b34c1-109">또한 트리거로 안녕하세요 HTTP + Swagger 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="b34c1-110">폴링 트리거 tooimplement 하려는 경우에 설명 된 hello 폴링 패턴을 따를 [논리 앱에서 사용자 지정 Api toocall 다른 Api, 서비스 및 시스템 만들](../logic-apps/logic-apps-create-api-app.md#polling-triggers)합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="b34c1-111">[논리 앱 트리거 및 동작](connectors-overview.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="b34c1-112">HTTP + Swagger toouse hello 하는 방법의 예로 워크플로에서 논리 앱의 동작으로 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="b34c1-113">선택 hello **새 단계** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="b34c1-114">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="b34c1-115">Hello 동작 검색 상자에 입력 **swagger** toolist 안녕하세요 HTTP + Swagger 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![HTTP + Swagger 동작 선택](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="b34c1-117">Swagger 문서에 대 한 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="b34c1-118">toowork hello 논리가 응용 프로그램 디자이너 hello URL에서에서 HTTPS 끝점 및 CORS 사용.</span><span class="sxs-lookup"><span data-stu-id="b34c1-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="b34c1-119">Hello Swagger 문서가 요구이 사항을 충족 하지 않는 경우 사용할 수 있습니다 [Azure 저장소 사용 하도록 설정 하는 CORS와](#hosting-swagger-from-storage) toostore hello 문서.</span><span class="sxs-lookup"><span data-stu-id="b34c1-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="b34c1-120">클릭 **다음** tooread 및에서 렌더링 hello Swagger 문서.</span><span class="sxs-lookup"><span data-stu-id="b34c1-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="b34c1-121">Hello HTTP 호출에 필요한 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![HTTP 작업 완료](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="b34c1-123">toosave 논리 앱 게시를 클릭 하 고 **저장** 디자이너 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="b34c1-124">Azure Storage에서 Swagger 호스트</span><span class="sxs-lookup"><span data-stu-id="b34c1-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="b34c1-125">Tooreference Swagger 문서 호스트 되지 않는 또는 hello 디자이너에 대 한 hello 보안 및 크로스-원본 요구 사항에 맞지 않는 하지 않는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="b34c1-126">tooresolve이 문제를 Azure 저장소의 hello Swagger 문서를 저장할 수 있으며 CORS tooreference hello 문서를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="b34c1-127">다음은 hello 단계 toocreate, 구성 및 Azure 저장소에 Swagger 문서를 저장할:</span><span class="sxs-lookup"><span data-stu-id="b34c1-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="b34c1-128">[Azure Blob 저장소를 사용하여 Azure Storage 계정을 만듭니다](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b34c1-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="b34c1-129">tooperform이 단계 사용 권한 설정 너무**공용 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="b34c1-130">Hello blob에서 CORS를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="b34c1-131">tooautomatically이 설정을 사용할 수 있습니다, [이 PowerShell 스크립트](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="b34c1-132">Hello Swagger 파일 toohello blob을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="b34c1-133">Hello에서이 단계를 수행할 수 있습니다 [Azure 포털](https://portal.azure.com) 또는 같은 도구에서 [Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="b34c1-134">Azure Blob 저장소에는 HTTPS 링크 toohello 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="b34c1-135">hello 링크에는이 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="b34c1-136">기술 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b34c1-136">Technical details</span></span>
<span data-ttu-id="b34c1-137">다음은이 hello 트리거 및 작업에 대 한 hello 정보 HTTP + Swagger 커넥터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="b34c1-138">HTTP + Swagger 트리거</span><span class="sxs-lookup"><span data-stu-id="b34c1-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="b34c1-139">트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="b34c1-140">트리거에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b34c1-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="b34c1-141">HTTP + Swagger hello 커넥터에 하나의 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="b34c1-142">트리거</span><span class="sxs-lookup"><span data-stu-id="b34c1-142">Trigger</span></span> | <span data-ttu-id="b34c1-143">설명</span><span class="sxs-lookup"><span data-stu-id="b34c1-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b34c1-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="b34c1-144">HTTP + Swagger</span></span> |<span data-ttu-id="b34c1-145">HTTP 호출을 수행 하 고 hello 응답 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="b34c1-146">HTTP + Swagger 동작</span><span class="sxs-lookup"><span data-stu-id="b34c1-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="b34c1-147">동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="b34c1-148">작업에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="b34c1-149">HTTP + Swagger hello 연결선의 한 가지 가능한 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="b34c1-150">동작</span><span class="sxs-lookup"><span data-stu-id="b34c1-150">Action</span></span> | <span data-ttu-id="b34c1-151">설명</span><span class="sxs-lookup"><span data-stu-id="b34c1-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b34c1-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="b34c1-152">HTTP + Swagger</span></span> |<span data-ttu-id="b34c1-153">HTTP 호출을 수행 하 고 hello 응답 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="b34c1-154">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b34c1-154">Action details</span></span>
<span data-ttu-id="b34c1-155">HTTP + Swagger hello 커넥터 작업을 사용할와 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="b34c1-156">다음은 각 hello 작업, 필수 및 선택적 입력된 필드 및 용도와 연결 된 출력 세부 사항에 해당 하는 hello에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="b34c1-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="b34c1-157">HTTP + Swagger</span></span>
<span data-ttu-id="b34c1-158">Swagger 메타데이터를 지원하는 HTTP 아웃바운드 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="b34c1-159">별표(*)는 필수 필드를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="b34c1-160">표시 이름</span><span class="sxs-lookup"><span data-stu-id="b34c1-160">Display name</span></span> | <span data-ttu-id="b34c1-161">속성 이름</span><span class="sxs-lookup"><span data-stu-id="b34c1-161">Property name</span></span> | <span data-ttu-id="b34c1-162">설명</span><span class="sxs-lookup"><span data-stu-id="b34c1-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b34c1-163">Method*</span><span class="sxs-lookup"><span data-stu-id="b34c1-163">Method*</span></span> |<span data-ttu-id="b34c1-164">메서드</span><span class="sxs-lookup"><span data-stu-id="b34c1-164">method</span></span> |<span data-ttu-id="b34c1-165">HTTP 동사 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="b34c1-166">URI*</span><span class="sxs-lookup"><span data-stu-id="b34c1-166">URI*</span></span> |<span data-ttu-id="b34c1-167">uri</span><span class="sxs-lookup"><span data-stu-id="b34c1-167">uri</span></span> |<span data-ttu-id="b34c1-168">Hello HTTP 요청에 대 한 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="b34c1-169">헤더</span><span class="sxs-lookup"><span data-stu-id="b34c1-169">Headers</span></span> |<span data-ttu-id="b34c1-170">headers</span><span class="sxs-lookup"><span data-stu-id="b34c1-170">headers</span></span> |<span data-ttu-id="b34c1-171">HTTP 헤더 tooinclude의 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="b34c1-172">body</span><span class="sxs-lookup"><span data-stu-id="b34c1-172">Body</span></span> |<span data-ttu-id="b34c1-173">body</span><span class="sxs-lookup"><span data-stu-id="b34c1-173">body</span></span> |<span data-ttu-id="b34c1-174">hello HTTP 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="b34c1-175">인증</span><span class="sxs-lookup"><span data-stu-id="b34c1-175">Authentication</span></span> |<span data-ttu-id="b34c1-176">인증</span><span class="sxs-lookup"><span data-stu-id="b34c1-176">authentication</span></span> |<span data-ttu-id="b34c1-177">요청에 대 한 인증 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-177">Authentication toouse for request.</span></span> <span data-ttu-id="b34c1-178">자세한 내용은 참조 hello [HTTP 커넥터](connectors-native-http.md#authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="b34c1-179">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="b34c1-179">**Output details**</span></span>

<span data-ttu-id="b34c1-180">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="b34c1-180">HTTP response</span></span>

| <span data-ttu-id="b34c1-181">속성 이름</span><span class="sxs-lookup"><span data-stu-id="b34c1-181">Property Name</span></span> | <span data-ttu-id="b34c1-182">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="b34c1-182">Data type</span></span> | <span data-ttu-id="b34c1-183">설명</span><span class="sxs-lookup"><span data-stu-id="b34c1-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b34c1-184">headers</span><span class="sxs-lookup"><span data-stu-id="b34c1-184">Headers</span></span> |<span data-ttu-id="b34c1-185">object</span><span class="sxs-lookup"><span data-stu-id="b34c1-185">object</span></span> |<span data-ttu-id="b34c1-186">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="b34c1-186">Response headers</span></span> |
| <span data-ttu-id="b34c1-187">본문</span><span class="sxs-lookup"><span data-stu-id="b34c1-187">Body</span></span> |<span data-ttu-id="b34c1-188">object</span><span class="sxs-lookup"><span data-stu-id="b34c1-188">object</span></span> |<span data-ttu-id="b34c1-189">응답 개체</span><span class="sxs-lookup"><span data-stu-id="b34c1-189">Response object</span></span> |
| <span data-ttu-id="b34c1-190">상태 코드</span><span class="sxs-lookup"><span data-stu-id="b34c1-190">Status Code</span></span> |<span data-ttu-id="b34c1-191">int</span><span class="sxs-lookup"><span data-stu-id="b34c1-191">int</span></span> |<span data-ttu-id="b34c1-192">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="b34c1-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="b34c1-193">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="b34c1-193">HTTP responses</span></span>
<span data-ttu-id="b34c1-194">호출 toovarious 작업을 만들 때 특정 응답 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="b34c1-195">다음 표에서는 해당 응답 및 설명을 대략적으로 요약해서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b34c1-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="b34c1-196">Name</span><span class="sxs-lookup"><span data-stu-id="b34c1-196">Name</span></span> | <span data-ttu-id="b34c1-197">설명</span><span class="sxs-lookup"><span data-stu-id="b34c1-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b34c1-198">200</span><span class="sxs-lookup"><span data-stu-id="b34c1-198">200</span></span> |<span data-ttu-id="b34c1-199">확인</span><span class="sxs-lookup"><span data-stu-id="b34c1-199">OK</span></span> |
| <span data-ttu-id="b34c1-200">202</span><span class="sxs-lookup"><span data-stu-id="b34c1-200">202</span></span> |<span data-ttu-id="b34c1-201">수락됨</span><span class="sxs-lookup"><span data-stu-id="b34c1-201">Accepted</span></span> |
| <span data-ttu-id="b34c1-202">400</span><span class="sxs-lookup"><span data-stu-id="b34c1-202">400</span></span> |<span data-ttu-id="b34c1-203">잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="b34c1-203">Bad request</span></span> |
| <span data-ttu-id="b34c1-204">401</span><span class="sxs-lookup"><span data-stu-id="b34c1-204">401</span></span> |<span data-ttu-id="b34c1-205">권한 없음</span><span class="sxs-lookup"><span data-stu-id="b34c1-205">Unauthorized</span></span> |
| <span data-ttu-id="b34c1-206">403</span><span class="sxs-lookup"><span data-stu-id="b34c1-206">403</span></span> |<span data-ttu-id="b34c1-207">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="b34c1-207">Forbidden</span></span> |
| <span data-ttu-id="b34c1-208">404</span><span class="sxs-lookup"><span data-stu-id="b34c1-208">404</span></span> |<span data-ttu-id="b34c1-209">찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="b34c1-209">Not Found</span></span> |
| <span data-ttu-id="b34c1-210">500</span><span class="sxs-lookup"><span data-stu-id="b34c1-210">500</span></span> |<span data-ttu-id="b34c1-211">내부 서버 오류.</span><span class="sxs-lookup"><span data-stu-id="b34c1-211">Internal server error.</span></span> <span data-ttu-id="b34c1-212">알 수 없는 오류 발생.</span><span class="sxs-lookup"><span data-stu-id="b34c1-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="b34c1-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b34c1-213">Next steps</span></span>

* [<span data-ttu-id="b34c1-214">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b34c1-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="b34c1-215">다른 커넥터 찾기</span><span class="sxs-lookup"><span data-stu-id="b34c1-215">Find other connectors</span></span>](apis-list.md)