---
title: "빠른 시작: Azure Machine Learning Recommendations API(버전 1)| Microsoft Docs"
description: "Azure 기계 학습 권장 사항 - 빠른 시작 가이드"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="22d2f-104">기계 학습 권장 사항 API(버전 1)에 대한 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="22d2f-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="22d2f-105">이 버전 대신 [Recommendations API Cognitive 서비스](https://www.microsoft.com/cognitive-services/recommendations-api)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="22d2f-106">Recommendations Cognitive 서비스가 이 서비스를 대체하게 되며, 모든 새로운 기능이 여기에서 개발됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="22d2f-107">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="22d2f-108">[새로운 Cognitive 서비스로 마이그레이션](http://aka.ms/recomigrate)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="22d2f-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="22d2f-109">이 문서에서는 Microsoft Azure 기계 학습 권장 사항을 사용하도록 서비스나 응용 프로그램을 등록하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="22d2f-110">권장 사항 API에 대한 자세한 내용은 [Cortana Intelligence 갤러리](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="22d2f-111">일반 개요</span><span class="sxs-lookup"><span data-stu-id="22d2f-111">General overview</span></span>
<span data-ttu-id="22d2f-112">Azure 기계 학습 권장 사항을 사용하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="22d2f-113">모델 만들기 - 모델은 사용 데이터, 카탈로그 데이터 및 권장 사항 모델의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="22d2f-114">카탈로그 데이터 가져오기 - 카탈로그에는 항목에 대한 메타데이터 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="22d2f-115">사용 데이터 가져오기 - 다음 두 가지 방법 중 하나(또는 둘 다)로 사용 데이터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="22d2f-116">사용 데이터를 포함하는 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="22d2f-117">데이터 취득 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="22d2f-118">일반적으로 초기 권장 사항 모델(부트스트랩)을 만들고 시스템에서 데이터 취득 형식을 사용하여 충분한 데이터를 수집할 때까지 초기 모델을 사용할 수 있도록 사용 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="22d2f-119">권장 사항 모델 작성 - 이 단계는 권장 사항 시스템이 모든 사용 데이터를 이용하여 권장 사항 모델을 만드는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="22d2f-120">이 작업은 데이터 크기 및 빌드 구성 매개 변수에 따라 몇 분이나 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="22d2f-121">빌드를 트리거하면 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="22d2f-122">이 빌드 ID를 사용하여 권장 사항 소비를 시작하기 전에 빌드 프로세스가 종료된 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="22d2f-123">권장 사항 소비 – 특정 항목 또는 항목 목록에 대한 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="22d2f-124">위의 모든 단계는 Azure 기계 학습 권장 사항 API를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="22d2f-125">이러한 각 단계를 구현하는 응용 프로그램 예제를 [갤러리에서도](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="22d2f-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="22d2f-126">제한 사항</span><span class="sxs-lookup"><span data-stu-id="22d2f-126">Limitations</span></span>
* <span data-ttu-id="22d2f-127">구독당 최대 모델 수는 10개입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="22d2f-128">카탈로그에 포함할 수 있는 최대 항목 수는 100,000개입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="22d2f-129">유지되는 사용 포인트의 최대 수는 5,000,000개입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="22d2f-130">새 포인트가 업로드되거나 보고되면 가장 오래된 포인트가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="22d2f-131">POST로 전송할 수 있는 최대 데이터 크기(예: 카탈로그 데이터 가져오기, 사용 데이터 가져오기)는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="22d2f-132">활성화되지 않은 권장 사항 모델 빌드에 대한 초당 트랜잭션 수는 최대 2TPS입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="22d2f-133">활성화된 권장 사항 모델 빌드는 최대 20TPS를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="22d2f-134">통합</span><span class="sxs-lookup"><span data-stu-id="22d2f-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="22d2f-135">인증</span><span class="sxs-lookup"><span data-stu-id="22d2f-135">Authentication</span></span>
<span data-ttu-id="22d2f-136">Microsoft Azure Marketplace에서는 기본 또는 OAuth 인증 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="22d2f-137">마켓플레이스의 [계정 설정](https://datamarket.azure.com/account/keys)에서 키로 이동하여 계정 키를 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="22d2f-138">기본 인증</span><span class="sxs-lookup"><span data-stu-id="22d2f-138">Basic Authentication</span></span>
<span data-ttu-id="22d2f-139">인증 헤더 추가:</span><span class="sxs-lookup"><span data-stu-id="22d2f-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="22d2f-140">Base64로 변환(C#)</span><span class="sxs-lookup"><span data-stu-id="22d2f-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="22d2f-141">Base64로 변환(JavaScript)</span><span class="sxs-lookup"><span data-stu-id="22d2f-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="22d2f-142">서비스 URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-142">Service URI</span></span>
<span data-ttu-id="22d2f-143">Azure 기계 학습 권장 사항 API에 대한 서비스 루트 URI는 [여기](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="22d2f-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="22d2f-144">전체 서비스 URI는 OData 사양의 요소를 사용하여 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="22d2f-145">API 버전</span><span class="sxs-lookup"><span data-stu-id="22d2f-145">API version</span></span>
<span data-ttu-id="22d2f-146">각 API 호출은 “1.0”으로 설정해야 하는 apiVersion이라는 쿼리 매개 변수 종료 시 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="22d2f-147">ID 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="22d2f-147">IDs are case-sensitive</span></span>
<span data-ttu-id="22d2f-148">API에서 반환되는 ID는 대/소문자를 구분하며, 후속 API 호출에서 매개 변수로 전달될 때에도 마찬가지로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="22d2f-149">예를 들어 모델 ID와 카탈로그 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="22d2f-150">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="22d2f-150">Create a model</span></span>
<span data-ttu-id="22d2f-151">"모델 만들기" 요청 만들기:</span><span class="sxs-lookup"><span data-stu-id="22d2f-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="22d2f-152">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-152">HTTP Method</span></span> | <span data-ttu-id="22d2f-153">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-154">POST</span><span class="sxs-lookup"><span data-stu-id="22d2f-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-155">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-156">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-156">Parameter Name</span></span> | <span data-ttu-id="22d2f-157">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-158">modelName</span><span class="sxs-lookup"><span data-stu-id="22d2f-158">modelName</span></span> |<span data-ttu-id="22d2f-159">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="22d2f-160">최대 길이: 20</span><span class="sxs-lookup"><span data-stu-id="22d2f-160">Max length: 20</span></span> |
| <span data-ttu-id="22d2f-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-161">apiVersion</span></span> |<span data-ttu-id="22d2f-162">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-162">1.0</span></span> |
|  | |
| <span data-ttu-id="22d2f-163">요청 본문</span><span class="sxs-lookup"><span data-stu-id="22d2f-163">Request Body</span></span> |<span data-ttu-id="22d2f-164">없음</span><span class="sxs-lookup"><span data-stu-id="22d2f-164">NONE</span></span> |

<span data-ttu-id="22d2f-165">**응답**:</span><span class="sxs-lookup"><span data-stu-id="22d2f-165">**Response**:</span></span>

<span data-ttu-id="22d2f-166">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="22d2f-167">`feed/entry/content/properties/id` - 모델 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="22d2f-168">모델 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="22d2f-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="22d2f-170">카탈로그 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="22d2f-170">Import catalog data</span></span>
<span data-ttu-id="22d2f-171">여러 번 호출하여 여러 카탈로그 파일을 같은 모델에 업로드하면 새 카탈로그 항목만 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="22d2f-172">기존 항목은 원래 값으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="22d2f-173">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-173">HTTP Method</span></span> | <span data-ttu-id="22d2f-174">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-175">POST</span><span class="sxs-lookup"><span data-stu-id="22d2f-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-176">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-177">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-177">Parameter Name</span></span> | <span data-ttu-id="22d2f-178">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-179">modelId</span><span class="sxs-lookup"><span data-stu-id="22d2f-179">modelId</span></span> |<span data-ttu-id="22d2f-180">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="22d2f-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="22d2f-181">filename</span><span class="sxs-lookup"><span data-stu-id="22d2f-181">filename</span></span> |<span data-ttu-id="22d2f-182">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="22d2f-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="22d2f-183">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="22d2f-184">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="22d2f-184">Max length: 50</span></span> |
| <span data-ttu-id="22d2f-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-185">apiVersion</span></span> |<span data-ttu-id="22d2f-186">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-186">1.0</span></span> |
|  | |
| <span data-ttu-id="22d2f-187">요청 본문</span><span class="sxs-lookup"><span data-stu-id="22d2f-187">Request Body</span></span> |<span data-ttu-id="22d2f-188">카탈로그 데이터.</span><span class="sxs-lookup"><span data-stu-id="22d2f-188">Catalog data.</span></span> <span data-ttu-id="22d2f-189">형식:</span><span class="sxs-lookup"><span data-stu-id="22d2f-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="22d2f-190">Name</span><span class="sxs-lookup"><span data-stu-id="22d2f-190">Name</span></span></th><th><span data-ttu-id="22d2f-191">필수</span><span class="sxs-lookup"><span data-stu-id="22d2f-191">Mandatory</span></span></th><th><span data-ttu-id="22d2f-192">형식</span><span class="sxs-lookup"><span data-stu-id="22d2f-192">Type</span></span></th><th><span data-ttu-id="22d2f-193">설명</span><span class="sxs-lookup"><span data-stu-id="22d2f-193">Description</span></span></th></tr><tr><td><span data-ttu-id="22d2f-194">항목 ID</span><span class="sxs-lookup"><span data-stu-id="22d2f-194">Item Id</span></span></td><td><span data-ttu-id="22d2f-195">예</span><span class="sxs-lookup"><span data-stu-id="22d2f-195">Yes</span></span></td><td><span data-ttu-id="22d2f-196">영숫자, 최대 길이 50</span><span class="sxs-lookup"><span data-stu-id="22d2f-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="22d2f-197">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="22d2f-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="22d2f-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="22d2f-198">Item Name</span></span></td><td><span data-ttu-id="22d2f-199">예</span><span class="sxs-lookup"><span data-stu-id="22d2f-199">Yes</span></span></td><td><span data-ttu-id="22d2f-200">영숫자, 최대 길이 255</span><span class="sxs-lookup"><span data-stu-id="22d2f-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="22d2f-201">항목 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="22d2f-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="22d2f-202">Item Category</span></span></td><td><span data-ttu-id="22d2f-203">예</span><span class="sxs-lookup"><span data-stu-id="22d2f-203">Yes</span></span></td><td><span data-ttu-id="22d2f-204">영숫자, 최대 길이 255</span><span class="sxs-lookup"><span data-stu-id="22d2f-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="22d2f-205">이 항목이 속하는 범주(예: 요리책, 드라마...)</span><span class="sxs-lookup"><span data-stu-id="22d2f-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="22d2f-206">설명</span><span class="sxs-lookup"><span data-stu-id="22d2f-206">Description</span></span></td><td><span data-ttu-id="22d2f-207">아니요</span><span class="sxs-lookup"><span data-stu-id="22d2f-207">No</span></span></td><td><span data-ttu-id="22d2f-208">영숫자, 최대 길이 4000</span><span class="sxs-lookup"><span data-stu-id="22d2f-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="22d2f-209">이 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="22d2f-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="22d2f-210">최대 파일 크기는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="22d2f-211">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="22d2f-212">**응답**:</span><span class="sxs-lookup"><span data-stu-id="22d2f-212">**Response**:</span></span>

<span data-ttu-id="22d2f-213">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="22d2f-214">`Feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="22d2f-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="22d2f-215">`Feed\entry\content\properties\ErrorCount` – 오류로 인해 삽입되지 않은 줄 수</span><span class="sxs-lookup"><span data-stu-id="22d2f-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="22d2f-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="22d2f-217">사용 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="22d2f-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="22d2f-218">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="22d2f-218">Uploading a file</span></span>
<span data-ttu-id="22d2f-219">이 섹션에서는 파일을 사용하여 사용 데이터를 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="22d2f-220">사용 데이터를 사용하여 이 API를 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="22d2f-221">모든 호출에 대한 모든 사용 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="22d2f-222">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-222">HTTP Method</span></span> | <span data-ttu-id="22d2f-223">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-224">POST</span><span class="sxs-lookup"><span data-stu-id="22d2f-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-225">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-226">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-226">Parameter Name</span></span> | <span data-ttu-id="22d2f-227">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-228">modelId</span><span class="sxs-lookup"><span data-stu-id="22d2f-228">modelId</span></span> |<span data-ttu-id="22d2f-229">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="22d2f-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="22d2f-230">filename</span><span class="sxs-lookup"><span data-stu-id="22d2f-230">filename</span></span> |<span data-ttu-id="22d2f-231">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="22d2f-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="22d2f-232">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="22d2f-233">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="22d2f-233">Max length: 50</span></span> |
| <span data-ttu-id="22d2f-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-234">apiVersion</span></span> |<span data-ttu-id="22d2f-235">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-235">1.0</span></span> |
|  | |
| <span data-ttu-id="22d2f-236">요청 본문</span><span class="sxs-lookup"><span data-stu-id="22d2f-236">Request Body</span></span> |<span data-ttu-id="22d2f-237">사용 데이터.</span><span class="sxs-lookup"><span data-stu-id="22d2f-237">Usage data.</span></span> <span data-ttu-id="22d2f-238">형식:</span><span class="sxs-lookup"><span data-stu-id="22d2f-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="22d2f-239">Name</span><span class="sxs-lookup"><span data-stu-id="22d2f-239">Name</span></span></th><th><span data-ttu-id="22d2f-240">필수</span><span class="sxs-lookup"><span data-stu-id="22d2f-240">Mandatory</span></span></th><th><span data-ttu-id="22d2f-241">형식</span><span class="sxs-lookup"><span data-stu-id="22d2f-241">Type</span></span></th><th><span data-ttu-id="22d2f-242">설명</span><span class="sxs-lookup"><span data-stu-id="22d2f-242">Description</span></span></th></tr><tr><td><span data-ttu-id="22d2f-243">User Id</span><span class="sxs-lookup"><span data-stu-id="22d2f-243">User Id</span></span></td><td><span data-ttu-id="22d2f-244">예</span><span class="sxs-lookup"><span data-stu-id="22d2f-244">Yes</span></span></td><td><span data-ttu-id="22d2f-245">영숫자</span><span class="sxs-lookup"><span data-stu-id="22d2f-245">Alphanumeric</span></span></td><td><span data-ttu-id="22d2f-246">사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="22d2f-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="22d2f-247">항목 ID</span><span class="sxs-lookup"><span data-stu-id="22d2f-247">Item Id</span></span></td><td><span data-ttu-id="22d2f-248">예</span><span class="sxs-lookup"><span data-stu-id="22d2f-248">Yes</span></span></td><td><span data-ttu-id="22d2f-249">영숫자, 최대 길이 50</span><span class="sxs-lookup"><span data-stu-id="22d2f-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="22d2f-250">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="22d2f-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="22d2f-251">Time</span><span class="sxs-lookup"><span data-stu-id="22d2f-251">Time</span></span></td><td><span data-ttu-id="22d2f-252">아니요</span><span class="sxs-lookup"><span data-stu-id="22d2f-252">No</span></span></td><td><span data-ttu-id="22d2f-253">날짜(형식): YYYY/MM/DDTHH:MM:SS(예: 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="22d2f-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="22d2f-254">데이터의 시간</span><span class="sxs-lookup"><span data-stu-id="22d2f-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="22d2f-255">이벤트</span><span class="sxs-lookup"><span data-stu-id="22d2f-255">Event</span></span></td><td><span data-ttu-id="22d2f-256">아니요. 지정하는 경우 날짜도 입력해야 함</span><span class="sxs-lookup"><span data-stu-id="22d2f-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="22d2f-257">다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-257">One of the following:</span></span><br><span data-ttu-id="22d2f-258">• Click</span><span class="sxs-lookup"><span data-stu-id="22d2f-258">• Click</span></span><br><span data-ttu-id="22d2f-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="22d2f-259">• RecommendationClick</span></span><br><span data-ttu-id="22d2f-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="22d2f-260">•    AddShopCart</span></span><br><span data-ttu-id="22d2f-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="22d2f-261">• RemoveShopCart</span></span><br><span data-ttu-id="22d2f-262">• Purchase</span><span class="sxs-lookup"><span data-stu-id="22d2f-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="22d2f-263">최대 파일 크기는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="22d2f-264">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="22d2f-265">**응답**:</span><span class="sxs-lookup"><span data-stu-id="22d2f-265">**Response**:</span></span>

<span data-ttu-id="22d2f-266">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="22d2f-267">`Feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="22d2f-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="22d2f-268">`Feed\entry\content\properties\ErrorCount` – 오류로 인해 삽입되지 않은 줄 수</span><span class="sxs-lookup"><span data-stu-id="22d2f-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="22d2f-269">`Feed\entry\content\properties\FileId` – 파일 식별자</span><span class="sxs-lookup"><span data-stu-id="22d2f-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="22d2f-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="22d2f-271">데이터 취득 사용</span><span class="sxs-lookup"><span data-stu-id="22d2f-271">Using data acquisition</span></span>
<span data-ttu-id="22d2f-272">이 섹션에서는 일반적으로 웹 사이트에서 Azure 기계 학습 권장 사항에 실시간으로 이벤트를 전송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="22d2f-273">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-273">HTTP Method</span></span> | <span data-ttu-id="22d2f-274">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-275">POST</span><span class="sxs-lookup"><span data-stu-id="22d2f-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-276">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-276">Parameter Name</span></span> | <span data-ttu-id="22d2f-277">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-278">apiVersion</span></span> |<span data-ttu-id="22d2f-279">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-279">1.0</span></span> |
|  | |
| <span data-ttu-id="22d2f-280">요청 본문</span><span class="sxs-lookup"><span data-stu-id="22d2f-280">Request body</span></span> |<span data-ttu-id="22d2f-281">Event data entry for each event you want to send.</span><span class="sxs-lookup"><span data-stu-id="22d2f-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="22d2f-282">SessionId 필드에서 같은 사용자 또는 브라우저 세션에 대해 같은 ID를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="22d2f-283">아래 이벤트 본문 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22d2f-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="22d2f-284">'Click' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="22d2f-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="22d2f-285">'RecommendationClick' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="22d2f-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="22d2f-286">'AddShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="22d2f-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="22d2f-287">'RemoveShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="22d2f-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="22d2f-288">'Purchase' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="22d2f-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="22d2f-289">두 개의 이벤트 'Click' 및 'AddShopCart'를 보내는 예:</span><span class="sxs-lookup"><span data-stu-id="22d2f-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="22d2f-290">**응답**: HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="22d2f-291">권장 사항 모델 작성</span><span class="sxs-lookup"><span data-stu-id="22d2f-291">Build a recommendation model</span></span>
| <span data-ttu-id="22d2f-292">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-292">HTTP Method</span></span> | <span data-ttu-id="22d2f-293">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-294">POST</span><span class="sxs-lookup"><span data-stu-id="22d2f-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-295">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-296">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-296">Parameter Name</span></span> | <span data-ttu-id="22d2f-297">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-298">modelId</span><span class="sxs-lookup"><span data-stu-id="22d2f-298">modelId</span></span> |<span data-ttu-id="22d2f-299">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="22d2f-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="22d2f-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="22d2f-300">userDescription</span></span> |<span data-ttu-id="22d2f-301">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="22d2f-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="22d2f-302">공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="22d2f-303">위 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22d2f-303">See example above.</span></span><br><span data-ttu-id="22d2f-304">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="22d2f-304">Max length: 50</span></span> |
| <span data-ttu-id="22d2f-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-305">apiVersion</span></span> |<span data-ttu-id="22d2f-306">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-306">1.0</span></span> |
|  | |
| <span data-ttu-id="22d2f-307">요청 본문</span><span class="sxs-lookup"><span data-stu-id="22d2f-307">Request Body</span></span> |<span data-ttu-id="22d2f-308">없음</span><span class="sxs-lookup"><span data-stu-id="22d2f-308">NONE</span></span> |

<span data-ttu-id="22d2f-309">**응답**:</span><span class="sxs-lookup"><span data-stu-id="22d2f-309">**Response**:</span></span>

<span data-ttu-id="22d2f-310">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-310">HTTP Status code: 200</span></span>

<span data-ttu-id="22d2f-311">비동기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-311">This is an asynchronous API.</span></span> <span data-ttu-id="22d2f-312">응답으로 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-312">You will get a build ID as a response.</span></span> <span data-ttu-id="22d2f-313">빌드가 종료된 시점을 알려면 "모델의 빌드 상태 가져오기" API를 호출하여 응답에서 이 빌드 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="22d2f-314">데이터 크기에 따라 빌드를 가져오는 데 몇 분에서 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="22d2f-315">빌드가 종료될 때까지 권장 사항을 소비할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="22d2f-316">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="22d2f-316">Valid build status:</span></span>

* <span data-ttu-id="22d2f-317">Create – 모델을 만듦</span><span class="sxs-lookup"><span data-stu-id="22d2f-317">Create – Model was created.</span></span>
* <span data-ttu-id="22d2f-318">Queued – 모델 빌드가 트리거되고 쿼리됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="22d2f-319">Building – 모델을 빌드하는 중</span><span class="sxs-lookup"><span data-stu-id="22d2f-319">Building – Model is being built.</span></span>
* <span data-ttu-id="22d2f-320">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="22d2f-321">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="22d2f-322">Canceled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="22d2f-323">Canceling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="22d2f-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="22d2f-324">다음 경로에서 빌드 ID를 찾을 수 있습니다. `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="22d2f-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="22d2f-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="22d2f-326">모델의 빌드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="22d2f-326">Get build status of a model</span></span>
| <span data-ttu-id="22d2f-327">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-327">HTTP Method</span></span> | <span data-ttu-id="22d2f-328">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-329">GET</span><span class="sxs-lookup"><span data-stu-id="22d2f-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-330">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-331">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-331">Parameter Name</span></span> | <span data-ttu-id="22d2f-332">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-333">modelId</span><span class="sxs-lookup"><span data-stu-id="22d2f-333">modelId</span></span> |<span data-ttu-id="22d2f-334">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="22d2f-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="22d2f-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="22d2f-335">onlyLastBuild</span></span> |<span data-ttu-id="22d2f-336">모델의 빌드 기록을 모두 반환할지 또는 최신 빌드의 상태만 반환할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="22d2f-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-337">apiVersion</span></span> |<span data-ttu-id="22d2f-338">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-338">1.0</span></span> |

<span data-ttu-id="22d2f-339">**응답**:</span><span class="sxs-lookup"><span data-stu-id="22d2f-339">**Response**:</span></span>

<span data-ttu-id="22d2f-340">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-340">HTTP Status code: 200</span></span>

<span data-ttu-id="22d2f-341">응답은 빌드당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-341">The response includes one entry per build.</span></span> <span data-ttu-id="22d2f-342">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-342">Each entry has the following data:</span></span>

* <span data-ttu-id="22d2f-343">`feed/entry/content/properties/UserName` - 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="22d2f-344">`feed/entry/content/properties/ModelName` - 모델의 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="22d2f-345">`feed/entry/content/properties/ModelId` – 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="22d2f-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="22d2f-346">`feed/entry/content/properties/IsDeployed` – 빌드 배포 여부(즉,</span><span class="sxs-lookup"><span data-stu-id="22d2f-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="22d2f-347">활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="22d2f-347">active build).</span></span>
* <span data-ttu-id="22d2f-348">`feed/entry/content/properties/BuildId` – 빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="22d2f-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="22d2f-349">`feed/entry/content/properties/BuildType` - 빌드의 형식</span><span class="sxs-lookup"><span data-stu-id="22d2f-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="22d2f-350">`feed/entry/content/properties/Status` – 빌드 상태</span><span class="sxs-lookup"><span data-stu-id="22d2f-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="22d2f-351">다음 중 하나일 수 있음: Error, Building, Queued, Canceling, Canceled, Success</span><span class="sxs-lookup"><span data-stu-id="22d2f-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="22d2f-352">`feed/entry/content/properties/StatusMessage` – 자세한 상태 메시지(특정 상태에만 적용)</span><span class="sxs-lookup"><span data-stu-id="22d2f-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="22d2f-353">`feed/entry/content/properties/Progress` – 빌드 진행률(%)</span><span class="sxs-lookup"><span data-stu-id="22d2f-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="22d2f-354">`feed/entry/content/properties/StartTime` – 빌드 시작 시간</span><span class="sxs-lookup"><span data-stu-id="22d2f-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="22d2f-355">`feed/entry/content/properties/EndTime` – 빌드 종료 시간</span><span class="sxs-lookup"><span data-stu-id="22d2f-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="22d2f-356">`feed/entry/content/properties/ExecutionTime` – 빌드 기간</span><span class="sxs-lookup"><span data-stu-id="22d2f-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="22d2f-357">`feed/entry/content/properties/ProgressStep` – 진행 중인 빌드의 현재 단계에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="22d2f-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="22d2f-358">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="22d2f-358">Valid build status:</span></span>

* <span data-ttu-id="22d2f-359">Created – 빌드 요청 항목이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="22d2f-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="22d2f-360">Queued – 빌드 요청이 트리거되었으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="22d2f-361">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="22d2f-361">Building – Build is in process.</span></span>
* <span data-ttu-id="22d2f-362">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="22d2f-363">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="22d2f-364">Canceled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="22d2f-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="22d2f-365">Canceling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="22d2f-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="22d2f-366">유효한 빌드 형식 값:</span><span class="sxs-lookup"><span data-stu-id="22d2f-366">Valid values for build type:</span></span>

* <span data-ttu-id="22d2f-367">Rank - 순위 빌드</span><span class="sxs-lookup"><span data-stu-id="22d2f-367">Rank - Rank build.</span></span> <span data-ttu-id="22d2f-368">(순위 빌드에 대한 자세한 내용은 "기계 학습 권장 사항 API 문서" 설명서를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="22d2f-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="22d2f-369">Recommendation - 권장 사항 빌드</span><span class="sxs-lookup"><span data-stu-id="22d2f-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="22d2f-370">Fbt - 자주 함께 구매됨 빌드</span><span class="sxs-lookup"><span data-stu-id="22d2f-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="22d2f-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="22d2f-372">권장 사항 가져오기</span><span class="sxs-lookup"><span data-stu-id="22d2f-372">Get recommendations</span></span>
| <span data-ttu-id="22d2f-373">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-373">HTTP Method</span></span> | <span data-ttu-id="22d2f-374">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-375">GET</span><span class="sxs-lookup"><span data-stu-id="22d2f-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-376">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-377">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-377">Parameter Name</span></span> | <span data-ttu-id="22d2f-378">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-379">modelId</span><span class="sxs-lookup"><span data-stu-id="22d2f-379">modelId</span></span> |<span data-ttu-id="22d2f-380">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="22d2f-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="22d2f-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="22d2f-381">itemIds</span></span> |<span data-ttu-id="22d2f-382">권장할 항목의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="22d2f-383">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="22d2f-383">Max length: 1024</span></span> |
| <span data-ttu-id="22d2f-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="22d2f-384">numberOfResults</span></span> |<span data-ttu-id="22d2f-385">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="22d2f-385">Number of required results</span></span> |
| <span data-ttu-id="22d2f-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="22d2f-386">includeMetatadata</span></span> |<span data-ttu-id="22d2f-387">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="22d2f-387">Future use, always false</span></span> |
| <span data-ttu-id="22d2f-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-388">apiVersion</span></span> |<span data-ttu-id="22d2f-389">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-389">1.0</span></span> |

<span data-ttu-id="22d2f-390">**응답:**</span><span class="sxs-lookup"><span data-stu-id="22d2f-390">**Response:**</span></span>

<span data-ttu-id="22d2f-391">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-391">HTTP Status code: 200</span></span>

<span data-ttu-id="22d2f-392">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="22d2f-393">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-393">Each entry has the following data:</span></span>

* <span data-ttu-id="22d2f-394">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="22d2f-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="22d2f-395">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="22d2f-396">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="22d2f-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="22d2f-397">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="22d2f-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="22d2f-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-398">OData XML</span></span>

<span data-ttu-id="22d2f-399">아래 예제 응답은 10개의 권장 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-399">The example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="22d2f-400">모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="22d2f-400">Update model</span></span>
<span data-ttu-id="22d2f-401">모델 설명 또는 활성 빌드 ID를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="22d2f-402">*활성 빌드 ID* – 모든 모델에 대한 모든 빌드에는 빌드 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="22d2f-403">활성 빌드 ID는 모든 새 모델 중 처음 성공한 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="22d2f-404">활성 빌드 ID가 있는데 같은 모델에 대한 추가 빌드를 수행하려면 이 활성 빌드 ID를 기본 빌드 ID로 명시적으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="22d2f-405">권장 사항을 소비할 때 사용할 빌드 ID를 지정하지 않으면 자동으로 기본 빌드 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="22d2f-406">이 메커니즘을 사용하면 프로덕션에 권장 사항 모델을 포함하고 나서 새 모델을 빌드하고 프로덕션으로 수준을 올리기 전에 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="22d2f-407">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22d2f-407">HTTP Method</span></span> | <span data-ttu-id="22d2f-408">URI</span><span class="sxs-lookup"><span data-stu-id="22d2f-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-409">PUT</span><span class="sxs-lookup"><span data-stu-id="22d2f-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="22d2f-410">예제:</span><span class="sxs-lookup"><span data-stu-id="22d2f-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="22d2f-411">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="22d2f-411">Parameter Name</span></span> | <span data-ttu-id="22d2f-412">유효한 값</span><span class="sxs-lookup"><span data-stu-id="22d2f-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="22d2f-413">id</span><span class="sxs-lookup"><span data-stu-id="22d2f-413">id</span></span> |<span data-ttu-id="22d2f-414">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="22d2f-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="22d2f-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="22d2f-415">apiVersion</span></span> |<span data-ttu-id="22d2f-416">1.0</span><span class="sxs-lookup"><span data-stu-id="22d2f-416">1.0</span></span> |
|  | |
| <span data-ttu-id="22d2f-417">요청 본문</span><span class="sxs-lookup"><span data-stu-id="22d2f-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="22d2f-418">XML 태그 Description 및 ActiveBuildId는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="22d2f-419">Description 또는 ActiveBuildId를 설정하지 않으려면 전체 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="22d2f-420">**응답**:</span><span class="sxs-lookup"><span data-stu-id="22d2f-420">**Response**:</span></span>

<span data-ttu-id="22d2f-421">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="22d2f-421">HTTP Status code: 200</span></span>

<span data-ttu-id="22d2f-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="22d2f-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="22d2f-423">법적 정보</span><span class="sxs-lookup"><span data-stu-id="22d2f-423">Legal</span></span>
<span data-ttu-id="22d2f-424">이 문서는 "있는 그대로" 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-424">This document is provided "as-is".</span></span> <span data-ttu-id="22d2f-425">URL 및 기타 인터넷 웹 사이트 참조를 포함하여 본 문서에 명시된 정보 및 보기는 통지 없이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="22d2f-426">여기에서 설명하는 일부 예는 설명 목적으로만 제공되는 가상의 예이며,</span><span class="sxs-lookup"><span data-stu-id="22d2f-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="22d2f-427">어떠한 실제 사례와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="22d2f-428">이 문서는 Microsoft 제품의 지적 소유권에 대한 법적 권한을 사용자에게 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="22d2f-429">이 문서는 내부 참조용으로만 복사 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22d2f-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="22d2f-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22d2f-430">© 2014 Microsoft.</span></span> <span data-ttu-id="22d2f-431">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="22d2f-431">All rights reserved.</span></span> 

