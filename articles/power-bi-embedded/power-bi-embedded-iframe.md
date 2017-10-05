---
title: "REST에서 Power BI Embedded를 사용하는 방법 | Microsoft Docs"
description: "REST에서 Power BI Embedded를 사용하는 방법 알아보기  "
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
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="294ac-103">REST에서 Power BI Embedded를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="294ac-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="294ac-104">Power BI Embedded: 정의 및 용도</span><span class="sxs-lookup"><span data-stu-id="294ac-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="294ac-105">Power BI Embedded의 개요는 공식적인 [Power BI Embedded 사이트](https://azure.microsoft.com/services/power-bi-embedded/)에 설명되어 있으나 REST에서 사용하는 방법을 자세히 살펴보기 전에 간단히 확인해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="294ac-106">실제로를 상당히 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-106">It's quite simple, really.</span></span> <span data-ttu-id="294ac-107">응용 프로그램 내에서 [Power BI](https://powerbi.microsoft.com)의 동적 데이터 시각화를 사용하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="294ac-108">대부분의 사용자 지정 응용 프로그램은 반드시 자체 조직의 사용자가 아닌 자신의 고객에게 데이터를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="294ac-109">예를 들어 회사 A와 B 둘 다에게 서비스를 제공하는 경우 회사 A의 사용자에게는 자신의 회사 A의 데이터만 보입니다. 즉, 이러한 전달을 위해서는 다중 테넌트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="294ac-110">사용자 지정 응용 프로그램은 자체 인증 방법(예: 폼 인증, 기본 인증 등)을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="294ac-111">그러면 포함 솔루션은 이러한 기존 인증 방법과 공동으로 안전하게 작동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="294ac-112">또한 사용자들이 Power BI 구독을 추가로 구입하거나 라이선스가 없는 상태로 해당 ISV 응용 프로그램을 사용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="294ac-113">**Power BI Embedded**는 정확하게 이러한 종류의 사용자 지정 시나리오를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="294ac-114">지금까지 방법을 간단히 살펴보았으므로 좀 더 자세한 부분을 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="294ac-115">.NET \(C#) 또는 Node.js SDK를 사용하여 Power BI Embedded로 응용 프로그램을 손쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="294ac-116">그러나 이 문서에서는 SDK 없이 Power BI의 HTTP 흐름\(AuthN 포함)에 대해 설명하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="294ac-117">이 흐름을 이해하면 **프로그래밍 언어를 사용하지 않고** 응용 프로그램을 빌드할 수 있으며 Power BI Embedded의 기본 사항을 깊이 있게 이해할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="294ac-118">Power BI 작업 영역 컬렉션 만들기 및 선택키 가져오기\(프로비전)</span><span class="sxs-lookup"><span data-stu-id="294ac-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="294ac-119">Power BI Embedded는 Azure 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="294ac-120">Azure Portal을 사용하는 ISV에게만 사용 요금이 부과되고\(시간당 사용자 세션), 보고서를 보는 사용자에게는 요금이 부과되지 않고 Azure 구독조차 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="294ac-121">응용 프로그램 개발을 시작하기 전에 Azure 포털을 사용하여 **Power BI 작업 영역 컬렉션** 을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="294ac-122">Power BI Embedded의 각 작업 영역은 각 고객의 작업 영역(테넌트)이며, 각 작업 영역 컬렉션에 여러 작업 영역을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="294ac-123">동일한 선택키가 각 작업 영역 컬렉션에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="294ac-124">실제로 작업 영역 컬렉션은 Power BI Embedded에 대한 보안 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="294ac-125">작업 영역 컬렉션을 다 만들면 Azure 포털에서 선택키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="294ac-126">또한 작업 영역 컬렉션을 프로비전하고 REST API를 통해 선택키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="294ac-127">자세한 내용은 [Power BI 리소스 공급자 API](https://msdn.microsoft.com/library/azure/mt712306.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="294ac-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="294ac-128">Power BI Desktop으로 .pbix 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="294ac-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="294ac-129">다음으로 포함할 데이터 연결 및 보고서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="294ac-130">이 작업의 경우 프로그래밍 또는 코드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="294ac-131">Power BI Desktop만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="294ac-132">이 문서에서 Power BI Desktop을 사용하는 자세한 방법을 다루지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="294ac-133">이에 대한 추가 도움말이 필요한 경우 [Power BI Desktop 시작](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="294ac-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="294ac-134">예제에서는 [소매점 분석 샘플](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/)을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="294ac-135">Power BI 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="294ac-135">Create a Power BI workspace</span></span>

<span data-ttu-id="294ac-136">이제 프로비전 작업이 모두 완료되었으므로 REST API를 통해 작업 영역 컬렉션에서 고객의 작업 영역을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="294ac-137">다음 HTTP POST 요청(REST)은 기존 작업 영역 컬렉션에 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="294ac-138">이것은 [POST 작업 영역 API](https://msdn.microsoft.com/library/azure/mt711503.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="294ac-139">이 예제에서 작업 영역 컬렉션 이름은 **mypbiapp**입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="294ac-140">앞서 복사한 선택키를 **AppKey**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="294ac-141">이 과정은 매우 간단한 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-141">It’s very simple authentication!</span></span>

<span data-ttu-id="294ac-142">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="294ac-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="294ac-143">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="294ac-143">**HTTP Response**</span></span>

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

<span data-ttu-id="294ac-144">반환된 **workspaceId** 는 후속 API 호출에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="294ac-145">응용 프로그램은 이 값을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="294ac-146">작업 영역으로 .pbix 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="294ac-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="294ac-147">작업 영역의 각 보고서는 데이터 집합\(데이터 원본 설정 포함)이 있는 단일 Power BI Desktop 파일과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="294ac-148">아래 코드에 표시된 대로 .pbix 파일을 작업 영역으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="294ac-149">여기에서 볼 수 있듯이 http에서 MIME 다중 파트를 사용하여 .pbix 파일의 이진 내용을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="294ac-150">URI 조각 **32960a09-6366-4208-a8bb-9e0678cdbb9d**는 workspaceId이고 쿼리 매개 변수 **datasetDisplayName**은 만들 데이터 집합 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="294ac-151">만든 데이터 집합에서 가져온 데이터, 데이터 원본에 대한 포인터 등의 모든 데이터 관련 아티팩트는 .pbix 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="294ac-152">이 가져오기 작업은 잠시 동안 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-152">This import task might run for a while.</span></span> <span data-ttu-id="294ac-153">완료되면 응용 프로그램은 가져오기 ID를 사용하여 작업 상태를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="294ac-154">이 예제에서 가져오기 ID는 **4eec64dd-533b-47c3-a72c-6508ad854659**입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="294ac-155">다음은 이 가져오기 ID를 사용하여 상태를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="294ac-156">작업이 완료되지 않으면 HTTP 응답은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-156">If the task isn't complete, the HTTP response could be like this:</span></span>

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

<span data-ttu-id="294ac-157">작업이 완료되면 HTTP 응답은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-157">If the task is complete, the HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="294ac-158">데이터 원본 연결\(및 데이터의 다중 테넌트)</span><span class="sxs-lookup"><span data-stu-id="294ac-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="294ac-159">.pbix 파일의 거의 모든 아티팩트를 작업 영역으로 가져오지만 데이터 원본에 대한 자격 증명은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="294ac-160">결과적으로 **DirectQuery 모드**를 사용할 경우 포함된 보고서가 올바르게 표시될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="294ac-161">하지만 **가져오기 모드**를 사용할 때는 기존에 가져온 데이터를 사용하여 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="294ac-162">이 경우 REST 호출을 통해 다음 단계를 사용하여 자격 증명을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="294ac-163">먼저 게이트웨이 데이터 원본을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="294ac-164">데이터 집합 **ID** 는 이전에 반환된 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="294ac-165">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="294ac-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="294ac-166">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="294ac-166">**HTTP Response**</span></span>

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

<span data-ttu-id="294ac-167">반환된 게이트웨이 ID와 데이터 원본 ID를 사용하여\(반환된 결과의 이전 **gatewayId** 및 **id** 참조) 이 데이터 원본의 자격 증명을 다음과 같이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="294ac-168">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="294ac-168">**HTTP Request**</span></span>

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

<span data-ttu-id="294ac-169">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="294ac-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="294ac-170">프로덕션 환경에서 REST API를 사용하여 작업 영역마다 다른 연결 문자열을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="294ac-171">\(즉, 고객별로 데이터베이스를 분리할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="294ac-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="294ac-172">다음에서는 REST를 통해 데이터 원본의 연결 문자열을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="294ac-173">또는 Power BI Embedded에서 행 수준 보안을 사용하고 한 보고서에서 각 사용자의 데이터를 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="294ac-174">결과적으로 .pbix\(UI 등)는 동일하지만 데이터 원본은 다른 각 고객 보고서를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="294ac-175">**DirectQuery 모드** 대신 **가져오기 모드**를 사용하는 경우 API를 통해 모델을 새로 고칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="294ac-176">또한 Power BI 게이트웨이 통한 온-프레미스 데이터 원본은 아직 Power BI Embedded에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="294ac-177">그러나 [Power BI 블로그](https://powerbi.microsoft.com/blog/) 에서 새로운 기능 및 앞으로 제공될 기능을 확인하는 것도 유용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="294ac-178">웹 페이지의 인증 및 보고서 호스트(포함)</span><span class="sxs-lookup"><span data-stu-id="294ac-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="294ac-179">이전 REST API에서는 선택키 **AppKey** 자체를 권한 부여 헤더로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="294ac-180">이러한 호출은 백 엔드 서버 쪽에서 처리될 수 있으므로 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="294ac-181">그러나 웹 페이지에 보고서를 포함할 경우 이러한 종류의 보안 정보는 JavaScript를 사용하여 처리됩니다\(프런트 엔드).</span><span class="sxs-lookup"><span data-stu-id="294ac-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="294ac-182">그런 다음 권한 부여 헤더 값을 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="294ac-183">악의적인 사용자나 악의적인 코드가 선택키를 찾으면 이 키를 사용하여 모든 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="294ac-184">따라서 웹 페이지에 보고서를 포함할 경우 선택키 **AppKey**대신 계산된 토큰을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="294ac-185">응용 프로그램은 클레임 및 계산된 디지털 서명으로 구성된 OAuth JWT\(JSON Web Token)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="294ac-186">아래와 같이 이 OAuth JWT는 점으로 구분된 인코딩된 문자열 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="294ac-187">먼저 나중에 서명되는 입력 값을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="294ac-188">이 값은 다음 json의 base64 url 인코딩(rfc4648) 문자열이며, 점\(.) 문자로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="294ac-189">나중에 보고서 ID를 가져오는 방법이 설명될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="294ac-190">Power BI Embedded에서 RLS(행 수준 보안)를 사용하려는 경우 클레임에 **사용자 이름** 및 **역할**도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

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

<span data-ttu-id="294ac-191">다음으로, SHA256 알고리즘에 따라 base64로 인코딩된 HMAC\(서명) 문자열을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="294ac-192">이 서명된 입력 값은 이전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="294ac-193">마지막으로, 점\(.) 문자를 사용하여 입력 값 및 서명 문자열을 결합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="294ac-194">완료된 문자열은 보고서 포함을 위한 앱 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="294ac-195">악의적인 사용자가 앱 토큰을 발견해도 원래 선택키를 가져올 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="294ac-196">이 앱 토큰은 신속하게 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-196">This app token will expire quickly.</span></span>

<span data-ttu-id="294ac-197">이러한 단계에 대한 PHP 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-197">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is the apptoken)
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

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="294ac-198">마지막으로 웹 페이지에 보고서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="294ac-199">보고서를 포함하기 위해 다음 REST API를 사용하여 포함 URL과 보고서 **ID** 를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="294ac-200">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="294ac-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="294ac-201">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="294ac-201">**HTTP Response**</span></span>

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

<span data-ttu-id="294ac-202">이전 앱 토큰을 사용하여 웹앱에 보고서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="294ac-203">다음 샘플 코드를 보면 첫 번째 부분은 이전 예제와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="294ac-204">이 샘플의 두 번째 부분에서는 iframe의 **embedUrl**\(이전 결과 참조)를 표시하고 앱 토큰을 iframe에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="294ac-205">보고서 ID 값을 원하는 값으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="294ac-206">또한 콘텐츠 관리 시스템의 버그로 인해 코드 샘플의 iframe 태그는 문자 그대로 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="294ac-207">이 샘플 코드를 복사하여 붙여넣는 경우 태그에서 대문자 텍스트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="294ac-208">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="294ac-209">이번에는 Power BI Embedded에 iframe의 보고서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="294ac-210">그렇지만 [Power BI 블로그](https://powerbi.microsoft.com/blog/)를 잘 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="294ac-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="294ac-211">향후 개선된 기능에서는 정보를 가져올 수 있을 뿐만 아니라 iframe으로 정보를 보낼 수 있도록 하는 새 클라이언트 쪽 API가 사용될 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="294ac-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="294ac-212">기대해 보세요.</span><span class="sxs-lookup"><span data-stu-id="294ac-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="294ac-213">참고 항목</span><span class="sxs-lookup"><span data-stu-id="294ac-213">See also</span></span>
* [<span data-ttu-id="294ac-214">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="294ac-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="294ac-215">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="294ac-215">More questions?</span></span> [<span data-ttu-id="294ac-216">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="294ac-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

