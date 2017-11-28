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
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="5f3c5-104">Hello 컴퓨터 학습 권장 사항을 API (버전 1)에 대 한 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="5f3c5-105">Hello를 사용 하 여 시작 해야 [권장 API Cognitive 서비스](https://www.microsoft.com/cognitive-services/recommendations-api) 이 버전 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="5f3c5-106">hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="5f3c5-107">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="5f3c5-108">에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="5f3c5-109">이 문서에서는 설명 방법을 tooonboard 서비스 또는 응용 프로그램 toouse Microsoft Azure 시스템 학습 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="5f3c5-110">Hello에 권장 사항을 API hello에 자세한 내용을 볼 수 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="5f3c5-111">일반 개요</span><span class="sxs-lookup"><span data-stu-id="5f3c5-111">General overview</span></span>
<span data-ttu-id="5f3c5-112">Azure 시스템 학습 권장 사항 toouse tootake hello 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="5f3c5-113">모델 만들기-모델은 사용 현황 데이터, 카탈로그 데이터와 hello 추천 모델의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="5f3c5-114">데이터 카탈로그 가져오기-카탈로그 hello 항목에 대 한 메타 데이터 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="5f3c5-115">사용 데이터 가져오기 - 다음 두 가지 방법 중 하나(또는 둘 다)로 사용 데이터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="5f3c5-116">Hello 사용 현황 데이터를 포함 하는 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="5f3c5-117">데이터 취득 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="5f3c5-118">일반적으로 순서 toobe 수 toocreate (부트스트랩)는 초기 추천 모델의에서 사용 파일을 업로드 한 hello 시스템 hello 데이터 취득 형식을 사용 하 여 충분 한 데이터가 수집 될 때까지 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="5f3c5-119">추천 모델을 작성-이 작업은 비동기 작업은 hello에서 추천 시스템 모든 hello 사용 현황 데이터를 가져와 추천 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="5f3c5-120">이 작업에는 몇 분 정도 걸릴 수 있습니다 또는 hello에 따라 몇 시간이 데이터의 크기 hello와 hello 빌드 구성 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="5f3c5-121">Hello 빌드를 트리거 id가 빌드 ID가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="5f3c5-122">Tooconsume 권장 구성을 시작 하기 전에 hello 빌드 프로세스가 종료 되는 경우 toocheck을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="5f3c5-123">권장 사항 소비 – 특정 항목 또는 항목 목록에 대한 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="5f3c5-124">위의 모든 hello 단계 hello Azure 컴퓨터 학습 권장 사항을 API를 통해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="5f3c5-125">각 hello에서 이러한 단계를 구현 하는 예제 응용 프로그램을 다운로드할 수 있습니다 [갤러리 뿐입니다.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="5f3c5-126">제한 사항</span><span class="sxs-lookup"><span data-stu-id="5f3c5-126">Limitations</span></span>
* <span data-ttu-id="5f3c5-127">구독 당 모델의 hello 최대 수는 10입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="5f3c5-128">hello 카탈로그를 보유할 수 있는 항목의 최대 수는 100, 000입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="5f3c5-129">hello 사용 포인트 유지 되는 최대 수에는 ~ 5,000,000는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="5f3c5-130">새로 업로드 되거나 보고 되는 경우 가장 오래 된 hello 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="5f3c5-131">POST (예를 들어 카탈로그 데이터 가져오기 사용 현황 데이터 가져오기)에 보낼 수 있는 데이터의 최대 크기 hello 사항은 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="5f3c5-132">hello 활성화 되지 않은 추천 모델 빌드에 대 한 초당 트랜잭션 수는 ~ 2TPS 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="5f3c5-133">활성화 된 추천 모델 빌드 too20TPS를 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="5f3c5-134">통합</span><span class="sxs-lookup"><span data-stu-id="5f3c5-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="5f3c5-135">인증</span><span class="sxs-lookup"><span data-stu-id="5f3c5-135">Authentication</span></span>
<span data-ttu-id="5f3c5-136">Microsoft Azure Marketplace hello Basic 또는 OAuth 인증 방법 중 하나를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="5f3c5-137">쉽게 찾을 수 hello 계정 키 toohello 키 아래에서 hello 시장에서 이동 하 여 [계정 설정을](https://datamarket.azure.com/account/keys)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="5f3c5-138">기본 인증</span><span class="sxs-lookup"><span data-stu-id="5f3c5-138">Basic Authentication</span></span>
<span data-ttu-id="5f3c5-139">Hello 권한 부여 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="5f3c5-140">TooBase64 변환 (C#)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="5f3c5-141">TooBase64 변환 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="5f3c5-142">서비스 URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-142">Service URI</span></span>
<span data-ttu-id="5f3c5-143">hello hello Azure 컴퓨터 학습 권장 사항을 Api에 대 한 서비스 루트 URI는 [여기 합니다.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="5f3c5-144">hello 전체 서비스 URI는 hello OData 사양의 요소를 사용 하 여 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="5f3c5-145">API 버전</span><span class="sxs-lookup"><span data-stu-id="5f3c5-145">API version</span></span>
<span data-ttu-id="5f3c5-146">각 API 호출 갖게 될 예정 hello 끝에 쿼리 라는 매개 변수를 설정 해야 하는 apiVersion 너무 "1.0"입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="5f3c5-147">ID 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="5f3c5-147">IDs are case-sensitive</span></span>
<span data-ttu-id="5f3c5-148">Hello, Api 중 하나에서 반환 된 Id, 대/소문자 및 후속 API 호출에 매개 변수로 전달 된 경우 에서처럼 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="5f3c5-149">예를 들어 모델 ID와 카탈로그 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="5f3c5-150">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="5f3c5-150">Create a model</span></span>
<span data-ttu-id="5f3c5-151">"모델 만들기" 요청 만들기:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="5f3c5-152">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-152">HTTP Method</span></span> | <span data-ttu-id="5f3c5-153">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-154">POST</span><span class="sxs-lookup"><span data-stu-id="5f3c5-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-155">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-156">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-156">Parameter Name</span></span> | <span data-ttu-id="5f3c5-157">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-158">modelName</span><span class="sxs-lookup"><span data-stu-id="5f3c5-158">modelName</span></span> |<span data-ttu-id="5f3c5-159">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="5f3c5-160">최대 길이: 20</span><span class="sxs-lookup"><span data-stu-id="5f3c5-160">Max length: 20</span></span> |
| <span data-ttu-id="5f3c5-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-161">apiVersion</span></span> |<span data-ttu-id="5f3c5-162">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-162">1.0</span></span> |
|  | |
| <span data-ttu-id="5f3c5-163">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5f3c5-163">Request Body</span></span> |<span data-ttu-id="5f3c5-164">없음</span><span class="sxs-lookup"><span data-stu-id="5f3c5-164">NONE</span></span> |

<span data-ttu-id="5f3c5-165">**응답**:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-165">**Response**:</span></span>

<span data-ttu-id="5f3c5-166">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="5f3c5-167">`feed/entry/content/properties/id`--Hello 모델 ID를 포함 하는 중</span><span class="sxs-lookup"><span data-stu-id="5f3c5-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="5f3c5-168">Hello 모델 ID가 대/소문자 구분을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="5f3c5-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="5f3c5-170">카탈로그 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="5f3c5-170">Import catalog data</span></span>
<span data-ttu-id="5f3c5-171">여러 가지 카탈로그 파일 toohello 모델 동일한 여러 호출으로 업로드 하는 경우만 hello 새 카탈로그 항목 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="5f3c5-172">기존 항목 hello 원래 값으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="5f3c5-173">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-173">HTTP Method</span></span> | <span data-ttu-id="5f3c5-174">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-175">POST</span><span class="sxs-lookup"><span data-stu-id="5f3c5-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-176">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-177">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-177">Parameter Name</span></span> | <span data-ttu-id="5f3c5-178">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-179">modelId</span><span class="sxs-lookup"><span data-stu-id="5f3c5-179">modelId</span></span> |<span data-ttu-id="5f3c5-180">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="5f3c5-181">filename</span><span class="sxs-lookup"><span data-stu-id="5f3c5-181">filename</span></span> |<span data-ttu-id="5f3c5-182">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="5f3c5-183">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="5f3c5-184">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="5f3c5-184">Max length: 50</span></span> |
| <span data-ttu-id="5f3c5-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-185">apiVersion</span></span> |<span data-ttu-id="5f3c5-186">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-186">1.0</span></span> |
|  | |
| <span data-ttu-id="5f3c5-187">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5f3c5-187">Request Body</span></span> |<span data-ttu-id="5f3c5-188">카탈로그 데이터.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-188">Catalog data.</span></span> <span data-ttu-id="5f3c5-189">형식:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="5f3c5-190">Name</span><span class="sxs-lookup"><span data-stu-id="5f3c5-190">Name</span></span></th><th><span data-ttu-id="5f3c5-191">필수</span><span class="sxs-lookup"><span data-stu-id="5f3c5-191">Mandatory</span></span></th><th><span data-ttu-id="5f3c5-192">형식</span><span class="sxs-lookup"><span data-stu-id="5f3c5-192">Type</span></span></th><th><span data-ttu-id="5f3c5-193">설명</span><span class="sxs-lookup"><span data-stu-id="5f3c5-193">Description</span></span></th></tr><tr><td><span data-ttu-id="5f3c5-194">항목 ID</span><span class="sxs-lookup"><span data-stu-id="5f3c5-194">Item Id</span></span></td><td><span data-ttu-id="5f3c5-195">예</span><span class="sxs-lookup"><span data-stu-id="5f3c5-195">Yes</span></span></td><td><span data-ttu-id="5f3c5-196">영숫자, 최대 길이 50</span><span class="sxs-lookup"><span data-stu-id="5f3c5-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="5f3c5-197">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="5f3c5-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="5f3c5-198">Item Name</span></span></td><td><span data-ttu-id="5f3c5-199">예</span><span class="sxs-lookup"><span data-stu-id="5f3c5-199">Yes</span></span></td><td><span data-ttu-id="5f3c5-200">영숫자, 최대 길이 255</span><span class="sxs-lookup"><span data-stu-id="5f3c5-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="5f3c5-201">항목 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="5f3c5-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="5f3c5-202">Item Category</span></span></td><td><span data-ttu-id="5f3c5-203">예</span><span class="sxs-lookup"><span data-stu-id="5f3c5-203">Yes</span></span></td><td><span data-ttu-id="5f3c5-204">영숫자, 최대 길이 255</span><span class="sxs-lookup"><span data-stu-id="5f3c5-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="5f3c5-205">(예: 요리 책 드라마...)이 항목이 속한 범주 toowhich</span><span class="sxs-lookup"><span data-stu-id="5f3c5-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="5f3c5-206">설명</span><span class="sxs-lookup"><span data-stu-id="5f3c5-206">Description</span></span></td><td><span data-ttu-id="5f3c5-207">아니요</span><span class="sxs-lookup"><span data-stu-id="5f3c5-207">No</span></span></td><td><span data-ttu-id="5f3c5-208">영숫자, 최대 길이 4000</span><span class="sxs-lookup"><span data-stu-id="5f3c5-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="5f3c5-209">이 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="5f3c5-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="5f3c5-210">최대 파일 크기는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="5f3c5-211">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="5f3c5-212">**응답**:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-212">**Response**:</span></span>

<span data-ttu-id="5f3c5-213">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="5f3c5-214">`Feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="5f3c5-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="5f3c5-215">`Feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="5f3c5-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="5f3c5-217">사용 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="5f3c5-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="5f3c5-218">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-218">Uploading a file</span></span>
<span data-ttu-id="5f3c5-219">이 섹션에서는 어떻게 tooupload 사용 현황 데이터 파일을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="5f3c5-220">사용 데이터를 사용하여 이 API를 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="5f3c5-221">모든 호출에 대한 모든 사용 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="5f3c5-222">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-222">HTTP Method</span></span> | <span data-ttu-id="5f3c5-223">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-224">POST</span><span class="sxs-lookup"><span data-stu-id="5f3c5-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-225">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-226">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-226">Parameter Name</span></span> | <span data-ttu-id="5f3c5-227">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-228">modelId</span><span class="sxs-lookup"><span data-stu-id="5f3c5-228">modelId</span></span> |<span data-ttu-id="5f3c5-229">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="5f3c5-230">filename</span><span class="sxs-lookup"><span data-stu-id="5f3c5-230">filename</span></span> |<span data-ttu-id="5f3c5-231">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="5f3c5-232">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="5f3c5-233">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="5f3c5-233">Max length: 50</span></span> |
| <span data-ttu-id="5f3c5-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-234">apiVersion</span></span> |<span data-ttu-id="5f3c5-235">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-235">1.0</span></span> |
|  | |
| <span data-ttu-id="5f3c5-236">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5f3c5-236">Request Body</span></span> |<span data-ttu-id="5f3c5-237">사용 데이터.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-237">Usage data.</span></span> <span data-ttu-id="5f3c5-238">형식:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="5f3c5-239">Name</span><span class="sxs-lookup"><span data-stu-id="5f3c5-239">Name</span></span></th><th><span data-ttu-id="5f3c5-240">필수</span><span class="sxs-lookup"><span data-stu-id="5f3c5-240">Mandatory</span></span></th><th><span data-ttu-id="5f3c5-241">형식</span><span class="sxs-lookup"><span data-stu-id="5f3c5-241">Type</span></span></th><th><span data-ttu-id="5f3c5-242">설명</span><span class="sxs-lookup"><span data-stu-id="5f3c5-242">Description</span></span></th></tr><tr><td><span data-ttu-id="5f3c5-243">User Id</span><span class="sxs-lookup"><span data-stu-id="5f3c5-243">User Id</span></span></td><td><span data-ttu-id="5f3c5-244">예</span><span class="sxs-lookup"><span data-stu-id="5f3c5-244">Yes</span></span></td><td><span data-ttu-id="5f3c5-245">영숫자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-245">Alphanumeric</span></span></td><td><span data-ttu-id="5f3c5-246">사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="5f3c5-247">항목 ID</span><span class="sxs-lookup"><span data-stu-id="5f3c5-247">Item Id</span></span></td><td><span data-ttu-id="5f3c5-248">예</span><span class="sxs-lookup"><span data-stu-id="5f3c5-248">Yes</span></span></td><td><span data-ttu-id="5f3c5-249">영숫자, 최대 길이 50</span><span class="sxs-lookup"><span data-stu-id="5f3c5-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="5f3c5-250">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="5f3c5-251">Time</span><span class="sxs-lookup"><span data-stu-id="5f3c5-251">Time</span></span></td><td><span data-ttu-id="5f3c5-252">아니요</span><span class="sxs-lookup"><span data-stu-id="5f3c5-252">No</span></span></td><td><span data-ttu-id="5f3c5-253">날짜(형식): YYYY/MM/DDTHH:MM:SS(예: 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="5f3c5-254">데이터의 시간</span><span class="sxs-lookup"><span data-stu-id="5f3c5-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="5f3c5-255">이벤트</span><span class="sxs-lookup"><span data-stu-id="5f3c5-255">Event</span></span></td><td><span data-ttu-id="5f3c5-256">아니요. 지정하는 경우 날짜도 입력해야 함</span><span class="sxs-lookup"><span data-stu-id="5f3c5-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="5f3c5-257">Hello 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-257">One of hello following:</span></span><br><span data-ttu-id="5f3c5-258">• Click</span><span class="sxs-lookup"><span data-stu-id="5f3c5-258">• Click</span></span><br><span data-ttu-id="5f3c5-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="5f3c5-259">• RecommendationClick</span></span><br><span data-ttu-id="5f3c5-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="5f3c5-260">•    AddShopCart</span></span><br><span data-ttu-id="5f3c5-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="5f3c5-261">• RemoveShopCart</span></span><br><span data-ttu-id="5f3c5-262">• Purchase</span><span class="sxs-lookup"><span data-stu-id="5f3c5-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="5f3c5-263">최대 파일 크기는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="5f3c5-264">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="5f3c5-265">**응답**:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-265">**Response**:</span></span>

<span data-ttu-id="5f3c5-266">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="5f3c5-267">`Feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="5f3c5-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="5f3c5-268">`Feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="5f3c5-269">`Feed\entry\content\properties\FileId` – 파일 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="5f3c5-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="5f3c5-271">데이터 취득 사용</span><span class="sxs-lookup"><span data-stu-id="5f3c5-271">Using data acquisition</span></span>
<span data-ttu-id="5f3c5-272">이 섹션에서는 real에서 toosend 이벤트 웹 사이트에서 일반적으로 tooAzure 시스템 학습 권장 사항으로 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="5f3c5-273">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-273">HTTP Method</span></span> | <span data-ttu-id="5f3c5-274">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-275">POST</span><span class="sxs-lookup"><span data-stu-id="5f3c5-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-276">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-276">Parameter Name</span></span> | <span data-ttu-id="5f3c5-277">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-278">apiVersion</span></span> |<span data-ttu-id="5f3c5-279">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-279">1.0</span></span> |
|  | |
| <span data-ttu-id="5f3c5-280">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5f3c5-280">Request body</span></span> |<span data-ttu-id="5f3c5-281">이벤트 데이터 입력 원하는 toosend 각 이벤트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="5f3c5-282">Hello 동일한 사용자 또는 브라우저 세션 hello hello 세션 Id 필드에 동일한 ID에 대 한 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="5f3c5-283">아래 이벤트 본문 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="5f3c5-284">'Click' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="5f3c5-285">'RecommendationClick' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="5f3c5-286">'AddShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="5f3c5-287">'RemoveShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="5f3c5-288">'Purchase' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="5f3c5-289">두 개의 이벤트 'Click' 및 'AddShopCart'를 보내는 예:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="5f3c5-290">**응답**: HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="5f3c5-291">권장 사항 모델 작성</span><span class="sxs-lookup"><span data-stu-id="5f3c5-291">Build a recommendation model</span></span>
| <span data-ttu-id="5f3c5-292">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-292">HTTP Method</span></span> | <span data-ttu-id="5f3c5-293">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-294">POST</span><span class="sxs-lookup"><span data-stu-id="5f3c5-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-295">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-296">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-296">Parameter Name</span></span> | <span data-ttu-id="5f3c5-297">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-298">modelId</span><span class="sxs-lookup"><span data-stu-id="5f3c5-298">modelId</span></span> |<span data-ttu-id="5f3c5-299">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="5f3c5-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="5f3c5-300">userDescription</span></span> |<span data-ttu-id="5f3c5-301">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="5f3c5-302">공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="5f3c5-303">위 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-303">See example above.</span></span><br><span data-ttu-id="5f3c5-304">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="5f3c5-304">Max length: 50</span></span> |
| <span data-ttu-id="5f3c5-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-305">apiVersion</span></span> |<span data-ttu-id="5f3c5-306">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-306">1.0</span></span> |
|  | |
| <span data-ttu-id="5f3c5-307">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5f3c5-307">Request Body</span></span> |<span data-ttu-id="5f3c5-308">없음</span><span class="sxs-lookup"><span data-stu-id="5f3c5-308">NONE</span></span> |

<span data-ttu-id="5f3c5-309">**응답**:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-309">**Response**:</span></span>

<span data-ttu-id="5f3c5-310">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-310">HTTP Status code: 200</span></span>

<span data-ttu-id="5f3c5-311">비동기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-311">This is an asynchronous API.</span></span> <span data-ttu-id="5f3c5-312">응답으로 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-312">You will get a build ID as a response.</span></span> <span data-ttu-id="5f3c5-313">hello 빌드 끝나면 tooknow, 해야 hello "Get 빌드 상태의 정도 모델" API를 호출 하 고 배치할 있습니다 hello 응답에서이 빌드 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="5f3c5-314">Note 빌드 hello hello 데이터 크기에 따라 분 toohours에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="5f3c5-315">Hello 빌드 끝까지 권장 사항을 소비할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="5f3c5-316">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-316">Valid build status:</span></span>

* <span data-ttu-id="5f3c5-317">Create – 모델을 만듦</span><span class="sxs-lookup"><span data-stu-id="5f3c5-317">Create – Model was created.</span></span>
* <span data-ttu-id="5f3c5-318">Queued – 모델 빌드가 트리거되고 쿼리됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="5f3c5-319">Building – 모델을 빌드하는 중</span><span class="sxs-lookup"><span data-stu-id="5f3c5-319">Building – Model is being built.</span></span>
* <span data-ttu-id="5f3c5-320">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="5f3c5-321">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="5f3c5-322">Canceled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="5f3c5-323">Canceling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="5f3c5-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="5f3c5-324">Note는 hello 빌드 경로 따라 hello에서 ID를 찾을 수 있습니다.`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="5f3c5-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="5f3c5-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="5f3c5-326">모델의 빌드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="5f3c5-326">Get build status of a model</span></span>
| <span data-ttu-id="5f3c5-327">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-327">HTTP Method</span></span> | <span data-ttu-id="5f3c5-328">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-329">GET</span><span class="sxs-lookup"><span data-stu-id="5f3c5-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-330">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-331">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-331">Parameter Name</span></span> | <span data-ttu-id="5f3c5-332">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-333">modelId</span><span class="sxs-lookup"><span data-stu-id="5f3c5-333">modelId</span></span> |<span data-ttu-id="5f3c5-334">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="5f3c5-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="5f3c5-335">onlyLastBuild</span></span> |<span data-ttu-id="5f3c5-336">나타냅니다 hello 모든 tooreturn hello 모델의 기록 빌드할지 hello 가장 최근 빌드의 유일한 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="5f3c5-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-337">apiVersion</span></span> |<span data-ttu-id="5f3c5-338">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-338">1.0</span></span> |

<span data-ttu-id="5f3c5-339">**응답**:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-339">**Response**:</span></span>

<span data-ttu-id="5f3c5-340">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-340">HTTP Status code: 200</span></span>

<span data-ttu-id="5f3c5-341">hello 응답 빌드 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-341">hello response includes one entry per build.</span></span> <span data-ttu-id="5f3c5-342">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="5f3c5-343">`feed/entry/content/properties/UserName`– Hello 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="5f3c5-344">`feed/entry/content/properties/ModelName`– Hello 모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="5f3c5-345">`feed/entry/content/properties/ModelId` – 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="5f3c5-346">`feed/entry/content/properties/IsDeployed`– Hello 빌드 (규칙 하위 배포 여부</span><span class="sxs-lookup"><span data-stu-id="5f3c5-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="5f3c5-347">활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-347">active build).</span></span>
* <span data-ttu-id="5f3c5-348">`feed/entry/content/properties/BuildId` – 빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="5f3c5-349">`feed/entry/content/properties/BuildType`-Hello 빌드의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="5f3c5-350">`feed/entry/content/properties/Status` – 빌드 상태</span><span class="sxs-lookup"><span data-stu-id="5f3c5-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="5f3c5-351">Hello 다음 중 하나일 수 있습니다: 오류, 건물, 대기, 취소, 취소 됨, 성공</span><span class="sxs-lookup"><span data-stu-id="5f3c5-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="5f3c5-352">`feed/entry/content/properties/StatusMessage`– 자세한 상태 메시지 (toospecific 상태에만 적용 됨).</span><span class="sxs-lookup"><span data-stu-id="5f3c5-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="5f3c5-353">`feed/entry/content/properties/Progress` – 빌드 진행률(%)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="5f3c5-354">`feed/entry/content/properties/StartTime` – 빌드 시작 시간</span><span class="sxs-lookup"><span data-stu-id="5f3c5-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="5f3c5-355">`feed/entry/content/properties/EndTime` – 빌드 종료 시간</span><span class="sxs-lookup"><span data-stu-id="5f3c5-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="5f3c5-356">`feed/entry/content/properties/ExecutionTime` – 빌드 기간</span><span class="sxs-lookup"><span data-stu-id="5f3c5-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="5f3c5-357">`feed/entry/content/properties/ProgressStep`– 빌드가 진행 중인 hello 현재 단계에 대 한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="5f3c5-358">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-358">Valid build status:</span></span>

* <span data-ttu-id="5f3c5-359">Created – 빌드 요청 항목이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="5f3c5-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="5f3c5-360">Queued – 빌드 요청이 트리거되었으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="5f3c5-361">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="5f3c5-361">Building – Build is in process.</span></span>
* <span data-ttu-id="5f3c5-362">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="5f3c5-363">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="5f3c5-364">Canceled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="5f3c5-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="5f3c5-365">Canceling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="5f3c5-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="5f3c5-366">유효한 빌드 형식 값:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-366">Valid values for build type:</span></span>

* <span data-ttu-id="5f3c5-367">Rank - 순위 빌드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-367">Rank - Rank build.</span></span> <span data-ttu-id="5f3c5-368">(순위에 대 한 빌드 정보, toohello "컴퓨터 학습 권장 API 설명서" 문서를 참조 하십시오.)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="5f3c5-369">Recommendation - 권장 사항 빌드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="5f3c5-370">Fbt - 자주 함께 구매됨 빌드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="5f3c5-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="5f3c5-372">권장 사항 가져오기</span><span class="sxs-lookup"><span data-stu-id="5f3c5-372">Get recommendations</span></span>
| <span data-ttu-id="5f3c5-373">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-373">HTTP Method</span></span> | <span data-ttu-id="5f3c5-374">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-375">GET</span><span class="sxs-lookup"><span data-stu-id="5f3c5-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-376">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-377">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-377">Parameter Name</span></span> | <span data-ttu-id="5f3c5-378">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-379">modelId</span><span class="sxs-lookup"><span data-stu-id="5f3c5-379">modelId</span></span> |<span data-ttu-id="5f3c5-380">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="5f3c5-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="5f3c5-381">itemIds</span></span> |<span data-ttu-id="5f3c5-382">쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="5f3c5-383">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="5f3c5-383">Max length: 1024</span></span> |
| <span data-ttu-id="5f3c5-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="5f3c5-384">numberOfResults</span></span> |<span data-ttu-id="5f3c5-385">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="5f3c5-385">Number of required results</span></span> |
| <span data-ttu-id="5f3c5-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="5f3c5-386">includeMetatadata</span></span> |<span data-ttu-id="5f3c5-387">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="5f3c5-387">Future use, always false</span></span> |
| <span data-ttu-id="5f3c5-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-388">apiVersion</span></span> |<span data-ttu-id="5f3c5-389">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-389">1.0</span></span> |

<span data-ttu-id="5f3c5-390">**응답:**</span><span class="sxs-lookup"><span data-stu-id="5f3c5-390">**Response:**</span></span>

<span data-ttu-id="5f3c5-391">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-391">HTTP Status code: 200</span></span>

<span data-ttu-id="5f3c5-392">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="5f3c5-393">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="5f3c5-394">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="5f3c5-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="5f3c5-395">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="5f3c5-396">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="5f3c5-397">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="5f3c5-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="5f3c5-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-398">OData XML</span></span>

<span data-ttu-id="5f3c5-399">아래 예제 응답 hello 10 개 권장된 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-399">hello example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="5f3c5-400">모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="5f3c5-400">Update model</span></span>
<span data-ttu-id="5f3c5-401">Hello 모델 설명을 업데이트 하거나 hello 활성 빌드 id입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="5f3c5-402">*활성 빌드 ID* – 모든 모델에 대한 모든 빌드에는 빌드 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="5f3c5-403">hello 활성 빌드 ID는 모든 새 모델의 첫 번째 성공한 빌드의 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="5f3c5-404">활성 빌드 ID 있고 hello에 대 한 추가 빌드 작업을 수행한 후 동일한 모델을 해야 tooexplicitly가 hello 기본 빌드 ID 하려면으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="5f3c5-405">사용 하면 권장 사항, toouse, 하나의 자동으로 사용 됩니다 하는 hello 기본 원하는 hello 빌드 ID를 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="5f3c5-406">이 메커니즘을 사용 하면 추천 모델이 프로덕션-toobuild 새 모델에에서 있는 하 고 테스트 하 여 이러한 수준을 올리기 전에 tooproduction-있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="5f3c5-407">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5f3c5-407">HTTP Method</span></span> | <span data-ttu-id="5f3c5-408">URI</span><span class="sxs-lookup"><span data-stu-id="5f3c5-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-409">PUT</span><span class="sxs-lookup"><span data-stu-id="5f3c5-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="5f3c5-410">예제:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="5f3c5-411">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5f3c5-411">Parameter Name</span></span> | <span data-ttu-id="5f3c5-412">유효한 값</span><span class="sxs-lookup"><span data-stu-id="5f3c5-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f3c5-413">id</span><span class="sxs-lookup"><span data-stu-id="5f3c5-413">id</span></span> |<span data-ttu-id="5f3c5-414">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="5f3c5-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="5f3c5-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5f3c5-415">apiVersion</span></span> |<span data-ttu-id="5f3c5-416">1.0</span><span class="sxs-lookup"><span data-stu-id="5f3c5-416">1.0</span></span> |
|  | |
| <span data-ttu-id="5f3c5-417">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5f3c5-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="5f3c5-418">참고 설명과 ActiveBuildId 해당 hello XML 태그는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="5f3c5-419">설명 또는 ActiveBuildId tooset 하지 않으려면 hello 전체 태그를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="5f3c5-420">**응답**:</span><span class="sxs-lookup"><span data-stu-id="5f3c5-420">**Response**:</span></span>

<span data-ttu-id="5f3c5-421">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="5f3c5-421">HTTP Status code: 200</span></span>

<span data-ttu-id="5f3c5-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="5f3c5-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="5f3c5-423">법적 정보</span><span class="sxs-lookup"><span data-stu-id="5f3c5-423">Legal</span></span>
<span data-ttu-id="5f3c5-424">이 문서는 "있는 그대로" 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-424">This document is provided "as-is".</span></span> <span data-ttu-id="5f3c5-425">URL 및 기타 인터넷 웹 사이트 참조를 포함하여 본 문서에 명시된 정보 및 보기는 통지 없이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="5f3c5-426">여기에서 설명하는 일부 예는 설명 목적으로만 제공되는 가상의 예이며,</span><span class="sxs-lookup"><span data-stu-id="5f3c5-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="5f3c5-427">어떠한 실제 사례와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="5f3c5-428">이 문서에서는 있습니다 법적 권리도 tooany Microsoft 제품의 지적 재산입니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="5f3c5-429">이 문서는 내부 참조용으로만 복사 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="5f3c5-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-430">© 2014 Microsoft.</span></span> <span data-ttu-id="5f3c5-431">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="5f3c5-431">All rights reserved.</span></span> 

