---
title: "Power BI 포함 rest aaaHow toouse | Microsoft Docs"
description: "자세한 내용은 방법 toouse rest Power BI 포함 "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="56651-103">어떻게 toouse rest Power BI 포함</span><span class="sxs-lookup"><span data-stu-id="56651-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="56651-104">Power BI Embedded: 정의 및 용도</span><span class="sxs-lookup"><span data-stu-id="56651-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="56651-105">Power BI 포함에 대 한 개요는 hello 공식에 설명 되어 [Power BI 포함 사이트](https://azure.microsoft.com/services/power-bi-embedded/), 살펴보겠습니다 빠른 REST 사용에 대 한 세부 정보 hello에 들어가기 전에 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="56651-106">실제로를 상당히 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-106">It's quite simple, really.</span></span> <span data-ttu-id="56651-107">toouse hello 동적 데이터 시각화의 경우가 [Power BI](https://powerbi.microsoft.com) 사용자 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="56651-108">가 자신의 조직에서 반드시 사용자가 자신의 고객에 대 한 toodeliver hello 데이터가 있어야 하는 대부분의 사용자 지정 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="56651-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="56651-109">예를 들어, 회사 A와 b에 대 한 몇 가지 서비스를 제공 하 고, 회사 A의에서 사용자가 해야 볼 데이터 자신의 회사 A에 대 한 즉, 다중 테 넌 트 hello hello 배달 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="56651-110">hello 사용자 지정 응용 프로그램은 자체 인증 방법을 폼 인증, 기본 인증 등도 제공 될 수 있습니다...</span><span class="sxs-lookup"><span data-stu-id="56651-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="56651-111">그런 다음 솔루션을 포함 하는 hello 해야 협력이 기존 인증 방법을 안전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="56651-112">사용자가 toobe 수 toouse에 필요한 것도 추가 구매 하거나 Power BI 구독 라이선스는 ISV 응용 프로그램 없이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="56651-113">**Power BI Embedded**는 정확하게 이러한 종류의 사용자 지정 시나리오를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="56651-114">따라서 해당 간략 한 소개 hello 방식을 만들었으므로 이제 해당 보겠습니다가 일부 세부 정보를</span><span class="sxs-lookup"><span data-stu-id="56651-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="56651-115">Hello.NET을 사용할 수 있습니다 \(C#) 또는 Node.js SDK, tooeasily Power BI embedded 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="56651-116">그러나 이 문서에서는 SDK 없이 Power BI의 HTTP 흐름\(AuthN 포함)에 대해 설명하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="56651-117">이 흐름을 이해, 응용 프로그램을 빌드할 수 **프로그래밍 언어와**, Power BI 포함의 hello 핵심 요소 깊이 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="56651-118">Power BI 작업 영역 컬렉션 만들기 및 선택키 가져오기\(프로비전)</span><span class="sxs-lookup"><span data-stu-id="56651-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="56651-119">Power BI 포함 Azure 서비스는 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="56651-120">유일한 hello Azure 포털을 사용 하는 ISV 사용 요금에 대 한 요금이 부과 됩니다 \(사용자 세션당 매시간), hello 사용자에 게 청구 또는 짝수 뷰 hello 보고서 수 없는 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="56651-121">이 응용 프로그램 개발을 시작 하기 전에 hello 만들어야 **Power BI 작업 영역 컬렉션** Azure 포털을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="56651-122">Power BI 포함의 각 작업 영역은 각 고객 (테 넌 트)에 대 한 hello 작업 영역 및 각 작업 영역 컬렉션에서 작업 영역을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="56651-123">각 작업 영역 컬렉션에서 동일한 액세스 키를 사용 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="56651-124">실제로 hello 작업 영역 컬렉션은 Power BI 포함에 대 한 hello 보안 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="56651-125">Hello 작업 영역 컬렉션 만들기를 완료 되 면 Azure 포털에서 hello 액세스 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="56651-126">또한 hello 작업 영역 컬렉션을 프로 비전 하 고 REST API를 통해 액세스 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="56651-127">toolearn 더 참조 [Power BI 리소스 공급자 Api](https://msdn.microsoft.com/library/azure/mt712306.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="56651-128">Power BI Desktop으로 .pbix 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="56651-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="56651-129">다음으로 hello 데이터 연결 및 포함 된 보고서 toobe 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="56651-130">이 작업의 경우 프로그래밍 또는 코드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="56651-131">Power BI Desktop만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="56651-132">방법에 대 한 세부 정보 hello 일일이 다루지는 않겠습니다.에서는이 문서에서는 Power BI Desktop toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="56651-133">이에 대한 추가 도움말이 필요한 경우 [Power BI Desktop 시작](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56651-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="56651-134">이 예에서는 방금에서는 hello [소매 분석 샘플](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/)합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="56651-135">Power BI 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="56651-135">Create a Power BI workspace</span></span>

<span data-ttu-id="56651-136">Hello를 프로 비전 작업이 모두 완료 했으므로 이제 시작 하겠습니다 REST Api를 통해 hello 작업 영역 컬렉션에서 고객의 작업 영역 만들기.</span><span class="sxs-lookup"><span data-stu-id="56651-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="56651-137">hello 다음 HTTP POST 요청 (REST) 만드는 것 hello 새 작업 영역에서 기존 작업 영역 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="56651-138">이 hello [POST 작업 영역 API](https://msdn.microsoft.com/library/azure/mt711503.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="56651-139">예에서 hello 작업 영역 컬렉션 이름이 **mypbiapp**합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="56651-140">에서는 이전에 복사한 hello 액세스 키를 설정으로 **AppKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="56651-141">이 과정은 매우 간단한 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-141">It’s very simple authentication!</span></span>

<span data-ttu-id="56651-142">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="56651-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="56651-143">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="56651-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="56651-144">반환 된 hello **workspaceId** hello 후속 API 호출 다음에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56651-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="56651-145">응용 프로그램은 이 값을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="56651-146">Hello 작업 영역 크기의.pbix 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="56651-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="56651-147">데이터 집합과 tooa 단일 Power BI Desktop 파일을 해당 하는 각 보고서 작업 영역에서 \(데이터 원본 설정 포함).</span><span class="sxs-lookup"><span data-stu-id="56651-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="56651-148">Hello 코드 아래에 나와 있는 것 처럼 취급.pbix 파일 toohello 작업에 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="56651-149">볼 수 있듯이 hello 이진 MIME 다중 파트를 사용 하 여 http에서 하는.pbix 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="56651-150">hello uri 조각 **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello workspaceId 및 쿼리 매개 변수는 **datasetDisplayName** hello 데이터 집합 이름 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56651-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="56651-151">관련 된 모든 데이터를 보유 하는 hello 만든 데이터 집합에서 가져온된 데이터를 같은 크기의.pbix 파일 아티팩트 hello 포인터 toohello 데이터 원본 등...</span><span class="sxs-lookup"><span data-stu-id="56651-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="56651-152">이 가져오기 작업은 잠시 동안 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-152">This import task might run for a while.</span></span> <span data-ttu-id="56651-153">완료 되 면 응용 프로그램 가져오기 id를 사용 하 여 hello 작업 상태를 요청할 수 있습니다. 이 예에서 hello 가져오기 id는 **4eec64dd-533b-47c3-a72c-6508ad854659**합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="56651-154">hello 다음이 가져오기 id를 사용 하 여 상태 요청:</span><span class="sxs-lookup"><span data-stu-id="56651-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="56651-155">Hello 작업 완료 없는 경우 다음과 같이 hello HTTP 응답 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="56651-156">Hello 작업이 완료 되 면 hello HTTP 응답을 다음과 같이 더 많은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="56651-157">데이터 원본 연결\(및 데이터의 다중 테넌트)</span><span class="sxs-lookup"><span data-stu-id="56651-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="56651-158">이 작업 영역으로 가져옵니다.pbix 파일의 hello 아티팩트의 거의 모든 데이터 원본에 대 한 자격 증명 hello는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="56651-159">결과적으로 사용 하는 경우 **DirectQuery 모드**, hello 포함 된 보고서를 표시할 수 없습니다 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="56651-160">하지만 사용 하는 경우 **가져오기 모드**, hello 기존 가져온된 데이터를 사용 하 여 hello 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="56651-161">이 경우 hello REST 호출을 통해 다음 단계를 사용 하 여 hello 자격 증명을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="56651-162">첫째, 우리 hello 게이트웨이 데이터 소스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="56651-163">회원님의 hello dataset **id** 는 hello 이전에 반환 된 id입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="56651-164">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="56651-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="56651-165">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="56651-165">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="56651-166">게이트웨이 id와 데이터 소스 id를 반환 된 hello를 사용 하 여 \(hello 이전 참조 **gatewayId** 및 **id** hello에 결과 반환 했습니다.),이 데이터 원본의 자격 증명 hello 다음과 같이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="56651-167">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="56651-167">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="56651-168">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="56651-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="56651-169">프로덕션 환경에서 REST API를 사용 하 여 각 작업 영역에 대 한 hello 다른 연결 문자열도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="56651-170">\(즉, 우리 구분할 수 hello 데이터베이스 각 고객에 대 한.)</span><span class="sxs-lookup"><span data-stu-id="56651-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="56651-171">hello 다음 REST 통해 데이터 원본의 연결 문자열 hello 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56651-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="56651-172">또는, 행 수준 보안 Power BI 포함에 사용 하 고 한 보고서에서 각 사용자에 대 한 hello 데이터를 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="56651-173">결과적으로 .pbix\(UI 등)는 동일하지만 데이터 원본은 다른 각 고객 보고서를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="56651-174">사용 중인 경우 **가져오기 모드** 대신 **DirectQuery 모드**는 API 통해 방법은 toorefresh 모델이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="56651-175">또한 Power BI 게이트웨이 통한 온-프레미스 데이터 원본은 아직 Power BI Embedded에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="56651-176">그러나 실제로 합니다 tookeep hello [Power BI 블로그](https://powerbi.microsoft.com/blog/) 새로운 기능 및 향후 예정 사항 나중에 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="56651-177">웹 페이지의 인증 및 보고서 호스트(포함)</span><span class="sxs-lookup"><span data-stu-id="56651-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="56651-178">이전 REST API를 hello, hello 액세스 키를 사용할 수 **AppKey** hello authorization 헤더로 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="56651-179">Hello 백 엔드 서버 쪽에서 이러한 호출을 처리할 수 있습니다, 때문에 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="56651-180">하지만 이러한 종류의 보안 정보 JavaScript를 사용 하 여 처리 됩니다 품질 웹 페이지에 hello 보고서를 포함 했습니다 \(프런트 엔드).</span><span class="sxs-lookup"><span data-stu-id="56651-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="56651-181">그런 다음 hello 권한 부여 헤더 값은 보호 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="56651-182">악의적인 사용자나 악의적인 코드가 선택키를 찾으면 이 키를 사용하여 모든 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="56651-183">선택 키 대신 계산된 토큰 hello를 사용 해야 품질 웹 페이지에 hello 보고서를 포함 했습니다 **AppKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="56651-184">응용 프로그램이 OAuth Json 웹 토큰 hello 만들어야 \(JWT) hello 클레임와 계산 된 디지털 서명이 hello 구성 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="56651-185">아래와 같이 이 OAuth JWT는 점으로 구분된 인코딩된 문자열 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="56651-186">첫째, 나중에 서명이 있는 hello 입력된 값을 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="56651-187">이 값은 hello base64 url 인코딩된 (rfc4648) 문자열의 json, 다음 hello 및 hello 점으로 구분 된 이러한 \(.) 문자.</span><span class="sxs-lookup"><span data-stu-id="56651-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="56651-188">이상에서는 tooget 보고서 id hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="56651-189">경우 원하는 toouse Power BI embedded 행 수준 보안 (RLS)도 지정 해야 **username** 및 **역할** hello 클레임에서입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="56651-190">다음으로, HMAC의 base64 인코딩 문자열 hello 만들어야 \(hello 서명) SHA256 알고리즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="56651-191">이 지정 된 입력된 값은 hello 이전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="56651-192">마지막으로, hello 입력된 값과 기간을 사용 하 여 서명 문자열을 결합 해야 우리 \(.) 문자.</span><span class="sxs-lookup"><span data-stu-id="56651-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="56651-193">완료 하는 hello 문자열은 보고서 포함 하는 hello에 hello 앱 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="56651-194">Hello 앱 토큰 악의적인 사용자가 발견 되는 경우에 hello 원래 선택 키를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="56651-195">이 앱 토큰은 신속하게 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="56651-195">This app token will expire quickly.</span></span>

<span data-ttu-id="56651-196">이러한 단계에 대한 PHP 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-196">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="56651-197">마지막으로 hello 보고서 hello 웹 페이지에 포함</span><span class="sxs-lookup"><span data-stu-id="56651-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="56651-198">보고서를 포함 하는 것에 대 한 hello 가져와서 url 및 보고서에 포함할 **id** hello 다음 REST API를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="56651-199">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="56651-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="56651-200">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="56651-200">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="56651-201">Hello 이전 응용 프로그램 토큰을 사용 하 여 웹 앱에 hello 보고서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="56651-202">Hello 다음 샘플 코드를 보면 hello 이전 부분 hello 앞의 예제와 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56651-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="56651-203">Hello 뒷부분에서이 샘플은 hello **embedUrl** \(hello 이전 결과 참조)에 iframe hello 및 hello iframe에 hello 앱 토큰을 게시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="56651-204">자신만의 toochange hello 보고서 id 값 tooone가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="56651-205">또한 콘텐츠 관리 시스템에 tooa 버그 인해 hello iframe 태그 hello 코드 예제에는 읽기 문자 그대로입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="56651-206">이 샘플 코드를 복사한 경우 hello 태그에서 보강 hello 텍스트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="56651-207">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56651-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="56651-208">이때 Power BI 포함만 hello 보고서 hello iframe의입니다.</span><span class="sxs-lookup"><span data-stu-id="56651-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="56651-209">Hello 예의 주시 있지만 [Power BI 블로그](https://powerbi.microsoft.com/blog/)합니다.</span><span class="sxs-lookup"><span data-stu-id="56651-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="56651-210">향후 개선 사항도 새 클라이언트 쪽 됩니다 주세요 hello iframe에 대 한 정보를 보낼 뿐만 아니라 정보를 가져올 수 있는 Api를 사용할 수 있습니다. 기대해 보세요.</span><span class="sxs-lookup"><span data-stu-id="56651-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="56651-211">참고 항목</span><span class="sxs-lookup"><span data-stu-id="56651-211">See also</span></span>
* [<span data-ttu-id="56651-212">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="56651-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="56651-213">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="56651-213">More questions?</span></span> [<span data-ttu-id="56651-214">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="56651-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

