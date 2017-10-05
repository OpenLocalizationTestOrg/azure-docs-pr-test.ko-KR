---
title: "Machine Learning 권장 사항 API 설명서 | Microsoft Docs"
description: "Microsoft Azure 마켓플레이스에서 사용할 수 있는 권장 사항 엔진에 대한 Azure 기계 학습 권장 사항 API 설명서입니다."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 1fba64d78d779344e2895b0d54419186b7584865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="a779e-103">Azure 기계 학습 권장 사항 API 설명서</span><span class="sxs-lookup"><span data-stu-id="a779e-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="a779e-104">이 버전 대신 Recommendations API Cognitive 서비스를 사용하기 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="a779e-105">Recommendations Cognitive 서비스가 이 서비스를 대체하게 되며, 모든 새로운 기능이 여기에서 개발됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="a779e-106">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="a779e-107">[새로운 Cognitive 서비스로 마이그레이션](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="a779e-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="a779e-108">이 문서에서는 Microsoft Azure 기계 학습 권장 사항 API에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="a779e-109">1. 일반 개요</span><span class="sxs-lookup"><span data-stu-id="a779e-109">1. General overview</span></span>
<span data-ttu-id="a779e-110">이 문서는 API 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-110">This document is an API reference.</span></span> <span data-ttu-id="a779e-111">“Azure Machine Learning 권장 사항 – 빠른 시작” 문서로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="a779e-112">Azure 기계 학습 추천 API는 다음 논리 그룹으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span></span>

* <span data-ttu-id="a779e-113"><ins>제한 사항</ins> - 추천 API 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="a779e-114"><ins>일반 정보</ins> - 인증, 서비스 URI 및 버전 관리에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="a779e-115"><ins>모델 기본</ins> - 모델에 대한 기본 작업(예: 모델 만들기, 업데이트 및 삭제)을 수행할 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="a779e-116"><ins>모델 고급</ins> – 모델에 대한 고급 데이터 정보를 얻을 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span></span>
* <span data-ttu-id="a779e-117"><ins>모델 비즈니스 규칙</ins> – 모델 권장 사항 결과에서 비즈니스 규칙을 관리할 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span></span>
* <span data-ttu-id="a779e-118"><ins>카탈로그</ins> – 모델 카탈로그에 대한 기본 작업을 수행할 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span></span> <span data-ttu-id="a779e-119">카탈로그에는 사용 데이터의 항목에 대한 메타데이터 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-119">A catalog contains metadata information on the items of the usage data.</span></span>
* <span data-ttu-id="a779e-120"><ins>기능</ins> - 항목에 대한 정보를 카탈로그로 작성하고 이 정보를 사용하여 더 나은 권장 사항을 작성하는 방법을 알 수 있도록 하는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span></span>
* <span data-ttu-id="a779e-121"><ins>사용 데이터</ins> - 모델 사용 데이터에 대한 기본 작업을 수행할 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span></span> <span data-ttu-id="a779e-122">기본 형식의 사용 데이터는 &#60;userId&#62;,&#60;itemId&#62; 쌍을 포함하는 행으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="a779e-123"><ins>빌드</ins> – 모델 빌드를 트리거하고 이 빌드와 관련된 기본 작업을 수행할 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span></span> <span data-ttu-id="a779e-124">유용한 사용 데이터가 있으면 모델 빌드를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="a779e-125"><ins>권장 사항</ins> – 모델 빌드가 종료되면 권장 사항을 사용할 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span></span>
* <span data-ttu-id="a779e-126"><ins>사용자 데이터</ins> - 사용자의 사용 현황 데이터 관련 정보를 가져올 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span></span>
* <span data-ttu-id="a779e-127"><ins>알림</ins> - API 작업과 관련된 문제에 대한 알림을 받을 수 있는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span></span> <span data-ttu-id="a779e-128">예를 들어 데이터 취득을 통해 사용 데이터를 보고하고 대부분의 이벤트 처리에 실패한 경우</span><span class="sxs-lookup"><span data-stu-id="a779e-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span></span> <span data-ttu-id="a779e-129">오류 알림이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="a779e-130">2. 제한 사항</span><span class="sxs-lookup"><span data-stu-id="a779e-130">2. Limitations</span></span>
* <span data-ttu-id="a779e-131">구독당 최대 모델 수는 10개입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-131">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="a779e-132">모델당 최대 빌드 수는 20입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-132">The maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="a779e-133">카탈로그에 포함할 수 있는 최대 항목 수는 100,000개입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-133">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="a779e-134">유지되는 사용 포인트의 최대 수는 5,000,000개입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-134">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="a779e-135">새 포인트가 업로드되거나 보고되면 가장 오래된 포인트가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-135">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="a779e-136">POST로 전송할 수 있는 최대 데이터 크기(예: 카탈로그 데이터 가져오기, 사용 데이터 가져오기)는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="a779e-137">권장 사항을 가져올 때 질문할 수 있는 최대 항목 수는 150입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-137">The maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="a779e-138">3. API – 일반 정보</span><span class="sxs-lookup"><span data-stu-id="a779e-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="a779e-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-139">3.1.</span></span> <span data-ttu-id="a779e-140">인증</span><span class="sxs-lookup"><span data-stu-id="a779e-140">Authentication</span></span>
<span data-ttu-id="a779e-141">인증과 관련된 Microsoft Azure 마켓플레이스 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="a779e-142">마켓플레이스에서는 기본 또는 OAuth 인증 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-142">The marketplace supports either the Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="a779e-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-143">3.2.</span></span> <span data-ttu-id="a779e-144">서비스 URI</span><span class="sxs-lookup"><span data-stu-id="a779e-144">Service URI</span></span>
<span data-ttu-id="a779e-145">Azure 기계 학습 권장 사항 API에 대한 서비스 루트 URI는 [여기](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="a779e-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="a779e-146">전체 서비스 URI는 OData 사양의 요소를 사용하여 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-146">The full service URI is expressed using elements of the OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="a779e-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-147">3.3.</span></span> <span data-ttu-id="a779e-148">API 버전</span><span class="sxs-lookup"><span data-stu-id="a779e-148">API version</span></span>
<span data-ttu-id="a779e-149">각 API 호출은 1.0으로 설정해야 하는 apiVersion이라는 쿼리 매개 변수 종료 시 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="a779e-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-150">3.4.</span></span> <span data-ttu-id="a779e-151">ID 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="a779e-151">IDs are case sensitive</span></span>
<span data-ttu-id="a779e-152">API에서 반환되는 ID는 대/소문자를 구분하며, 후속 API 호출에서 매개 변수로 전달될 때에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="a779e-153">예를 들어 모델 ID와 카탈로그 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="a779e-154">4. 권장 사항 품질 및 콜드 항목</span><span class="sxs-lookup"><span data-stu-id="a779e-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="a779e-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-155">4.1.</span></span> <span data-ttu-id="a779e-156">권장 사항 품질</span><span class="sxs-lookup"><span data-stu-id="a779e-156">Recommendation quality</span></span>
<span data-ttu-id="a779e-157">권장 사항 모델 만들기는 일반적으로 시스템에서 권장 사항을 제공하도록 하는 데 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span></span> <span data-ttu-id="a779e-158">그러나 권장 사항 품질은 처리한 사용 현황 및 카탈로그의 적용 범위에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span></span> <span data-ttu-id="a779e-159">예를 들어 콜드 항목(중요한 사용 현황이 없는 항목)이 많은 경우에는 시스템에서 해당 항목에 대한 권장 사항을 제공하거나 해당 항목을 권장 항목으로 사용하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="a779e-160">콜드 항목 문제를 해결하기 위해 시스템에서는 항목의 메타데이터를 사용하여 권장 사항을 개선할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span></span> <span data-ttu-id="a779e-161">이 메타데이터를 기능이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-161">This metadata is referred to as features.</span></span> <span data-ttu-id="a779e-162">일반적인 기능은 책의 저자 또는 동영상의 배우입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="a779e-163">기능은 키/값 문자열 형식으로 카탈로그를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-163">Features are provided via the catalog in the form of key/value strings.</span></span> <span data-ttu-id="a779e-164">카탈로그 파일의 전체 형식은 [카탈로그 가져오기 섹션](#81-import-catalog-data)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="a779e-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-165">4.2.</span></span> <span data-ttu-id="a779e-166">순위 빌드</span><span class="sxs-lookup"><span data-stu-id="a779e-166">Rank build</span></span>
<span data-ttu-id="a779e-167">기능은 권장 사항 모델을 개선할 수 있지만 그러려면 의미 있는 기능을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span></span> <span data-ttu-id="a779e-168">이를 위해 순위 빌드라는 새 빌드가 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="a779e-169">이 빌드는 기능의 유용성 순위를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-169">This build will rank the usefulness of features.</span></span> <span data-ttu-id="a779e-170">의미 있는 기능은 순위 점수가 2 이상인 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="a779e-171">의미 있는 기능을 이해한 후에는 의미 있는 기능 목록(또는 하위 목록)으로 권장 사항 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span></span> <span data-ttu-id="a779e-172">이러한 기능을 사용하여 웜 항목과 콜드 항목 모두를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span></span> <span data-ttu-id="a779e-173">웜 항목에 사용하려면 `UseFeatureInModel` 빌드 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="a779e-174">콜드 항목에 사용하려면 `AllowColdItemPlacement` 빌드 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="a779e-175">참고: `UseFeatureInModel`을 설정하지 않고 `AllowColdItemPlacement`를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="a779e-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-176">4.3.</span></span> <span data-ttu-id="a779e-177">권장 사항 추론</span><span class="sxs-lookup"><span data-stu-id="a779e-177">Recommendation reasoning</span></span>
<span data-ttu-id="a779e-178">권장 사항 추론은 기능 사용의 또 다른 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="a779e-179">실제로 Azure Machine Learning 권장 사항 엔진은 기능을 사용하여 권장 사항 설명(즉,</span><span class="sxs-lookup"><span data-stu-id="a779e-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="a779e-180">추론)을 제공하여 권장 사항 소비자가 권장된 항목에 대해 더 많은 확신을 가지도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span></span>
<span data-ttu-id="a779e-181">추론을 사용하려면 권장 사항 빌드를 요청하기 전에 `AllowFeatureCorrelation` 및 `ReasoningFeatureList` 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="a779e-182">5. 모델 기본</span><span class="sxs-lookup"><span data-stu-id="a779e-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="a779e-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-183">5.1.</span></span> <span data-ttu-id="a779e-184">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="a779e-184">Create Model</span></span>
<span data-ttu-id="a779e-185">"모델 만들기" 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="a779e-186">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-186">HTTP Method</span></span> | <span data-ttu-id="a779e-187">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-188">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-189">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-190">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-190">Parameter Name</span></span> | <span data-ttu-id="a779e-191">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-192">modelName</span><span class="sxs-lookup"><span data-stu-id="a779e-192">modelName</span></span> |<span data-ttu-id="a779e-193">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a779e-194">최대 길이: 20</span><span class="sxs-lookup"><span data-stu-id="a779e-194">Max length: 20</span></span> |
| <span data-ttu-id="a779e-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-195">apiVersion</span></span> |<span data-ttu-id="a779e-196">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-196">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-197">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-197">Request Body</span></span> |<span data-ttu-id="a779e-198">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-198">NONE</span></span> |

<span data-ttu-id="a779e-199">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-199">**Response**:</span></span>

<span data-ttu-id="a779e-200">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="a779e-201">`feed/entry/content/properties/id` - 모델 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-201">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="a779e-202">**참고**: 모델 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="a779e-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="a779e-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-204">5.2.</span></span> <span data-ttu-id="a779e-205">모델 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-205">Get Model</span></span>
<span data-ttu-id="a779e-206">"모델 가져오기" 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="a779e-207">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-207">HTTP Method</span></span> | <span data-ttu-id="a779e-208">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-209">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-210">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-211">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-211">Parameter Name</span></span> | <span data-ttu-id="a779e-212">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-213">id</span><span class="sxs-lookup"><span data-stu-id="a779e-213">id</span></span> |<span data-ttu-id="a779e-214">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="a779e-214">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="a779e-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-215">apiVersion</span></span> |<span data-ttu-id="a779e-216">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-216">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-217">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-217">Request Body</span></span> |<span data-ttu-id="a779e-218">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-218">NONE</span></span> |

<span data-ttu-id="a779e-219">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-219">**Response**:</span></span>

<span data-ttu-id="a779e-220">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-220">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-221">다음 요소 아래에서 모델 데이터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-221">The model data can be found under the following elements:</span></span>

* <span data-ttu-id="a779e-222">`feed/entry/content/properties/Id` – 모델의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="a779e-223">`feed/entry/content/properties/Name` – 모델 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="a779e-224">`feed/entry/content/properties/Date` - 모델을 만든 날짜</span><span class="sxs-lookup"><span data-stu-id="a779e-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="a779e-225">`feed/entry/content/properties/Status` – 모델 상태</span><span class="sxs-lookup"><span data-stu-id="a779e-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="a779e-226">다음 중 하나</span><span class="sxs-lookup"><span data-stu-id="a779e-226">One of the following:</span></span>
  * <span data-ttu-id="a779e-227">Created - 모델이 생성되었으며 카탈로그 및 사용 현황을 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="a779e-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="a779e-228">ReadyForBuild – 모델이 생성되었으며 카탈로그 및 사용 현황을 포함함</span><span class="sxs-lookup"><span data-stu-id="a779e-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="a779e-229">`feed/entry/content/properties/HasActiveBuild` – 모델이 성공적으로 빌드된 경우를 나타냄</span><span class="sxs-lookup"><span data-stu-id="a779e-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="a779e-230">`feed/entry/content/properties/BuildId` – 모델 활성 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="a779e-231">`feed/entry/content/properties/Mpr` – 모델 평균 백분위수 순위(MPR - 자세한 내용은 ModelInsight 참조)</span><span class="sxs-lookup"><span data-stu-id="a779e-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="a779e-232">`feed/entry/content/properties/UserName` – 모델 내부 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="a779e-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="a779e-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-234">5.3.</span></span>    <span data-ttu-id="a779e-235">모든 모델 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-235">Get All Models</span></span>
<span data-ttu-id="a779e-236">현재 사용자의 모든 모델을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-236">Retrieves all models of the current user.</span></span>

| <span data-ttu-id="a779e-237">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-237">HTTP Method</span></span> | <span data-ttu-id="a779e-238">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-239">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="a779e-240">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-241">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-241">Parameter Name</span></span> | <span data-ttu-id="a779e-242">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-243">apiVersion</span></span> |<span data-ttu-id="a779e-244">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-244">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-245">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-245">Request Body</span></span> |<span data-ttu-id="a779e-246">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-246">NONE</span></span> |

<span data-ttu-id="a779e-247">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-247">**Response**:</span></span>

<span data-ttu-id="a779e-248">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="a779e-249">`feed/entry/content/properties/Id` – 모델의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="a779e-250">`feed/entry/content/properties/Name` – 모델 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="a779e-251">`feed/entry/content/properties/Date` - 모델을 만든 날짜</span><span class="sxs-lookup"><span data-stu-id="a779e-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="a779e-252">`feed/entry/content/properties/Status` – 모델 상태</span><span class="sxs-lookup"><span data-stu-id="a779e-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="a779e-253">다음 중 하나</span><span class="sxs-lookup"><span data-stu-id="a779e-253">One of the following:</span></span>
  * <span data-ttu-id="a779e-254">Created - 모델이 생성되었으며 카탈로그 및 사용 현황을 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="a779e-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="a779e-255">ReadyForBuild – 모델이 생성되었으며 카탈로그 및 사용 현황을 포함함</span><span class="sxs-lookup"><span data-stu-id="a779e-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="a779e-256">`feed/entry/content/properties/HasActiveBuild` – 모델이 성공적으로 빌드된 경우를 나타냄</span><span class="sxs-lookup"><span data-stu-id="a779e-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="a779e-257">`feed/entry/content/properties/BuildId` – 모델 활성 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="a779e-258">`feed/entry/content/properties/Mpr` – 모델 MPR(자세한 내용은 ModelInsight 참조)</span><span class="sxs-lookup"><span data-stu-id="a779e-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="a779e-259">`feed/entry/content/properties/UserName` – 모델 내부 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="a779e-260">`feed/entry/content/properties/UsageFileNames` – 쉼표로 구분된 모델 사용 파일 목록</span><span class="sxs-lookup"><span data-stu-id="a779e-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="a779e-261">`feed/entry/content/properties/CatalogId` – 모델 카탈로그 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="a779e-262">`feed/entry/content/properties/Description` – 모델 설명</span><span class="sxs-lookup"><span data-stu-id="a779e-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="a779e-263">`feed/entry/content/properties/CatalogFileName` – 모델 카탈로그 파일 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="a779e-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="a779e-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-265">5.4.</span></span>    <span data-ttu-id="a779e-266">모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="a779e-266">Update Model</span></span>
<span data-ttu-id="a779e-267">모델 설명 또는 활성 빌드 ID를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-267">You can update the model description or the active build ID.</span></span><br><span data-ttu-id="a779e-268">
<ins>활성 빌드 ID</ins> – 모든 모델에 대한 모든 빌드에는 빌드 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="a779e-269">활성 빌드 ID는 모든 새 모델 중 처음 성공한 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-269">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="a779e-270">활성 빌드 ID가 있는데 같은 모델에 대한 추가 빌드를 수행하려면 이 활성 빌드 ID를 기본 빌드 ID로 명시적으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="a779e-271">권장 사항을 소비할 때 사용할 빌드 ID를 지정하지 않으면 자동으로 기본 빌드 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span><br>
<span data-ttu-id="a779e-272">이 메커니즘을 사용하면 프로덕션에 권장 사항 모델을 포함하고 나서 새 모델을 빌드하고 프로덕션으로 수준을 올리기 전에 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="a779e-273">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-273">HTTP Method</span></span> | <span data-ttu-id="a779e-274">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-275">PUT</span><span class="sxs-lookup"><span data-stu-id="a779e-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-276">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-277">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-277">Parameter Name</span></span> | <span data-ttu-id="a779e-278">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-279">id</span><span class="sxs-lookup"><span data-stu-id="a779e-279">id</span></span> |<span data-ttu-id="a779e-280">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="a779e-280">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="a779e-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-281">apiVersion</span></span> |<span data-ttu-id="a779e-282">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-282">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-283">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="a779e-284">XML 태그 Description 및 ActiveBuildId는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-284">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="a779e-285">Description 또는 ActiveBuildId를 설정하지 않으려면 전체 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="a779e-286">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-286">**Response**:</span></span>

<span data-ttu-id="a779e-287">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="a779e-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="a779e-288">5.5.</span></span>    <span data-ttu-id="a779e-289">모델 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-289">Delete Model</span></span>
<span data-ttu-id="a779e-290">ID별로 기존 모델을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="a779e-291">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-291">HTTP Method</span></span> | <span data-ttu-id="a779e-292">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-293">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-294">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-295">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-295">Parameter Name</span></span> | <span data-ttu-id="a779e-296">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-297">id</span><span class="sxs-lookup"><span data-stu-id="a779e-297">id</span></span> |<span data-ttu-id="a779e-298">모델의 고유 식별자(대/소문자 구분)</span><span class="sxs-lookup"><span data-stu-id="a779e-298">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="a779e-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-299">apiVersion</span></span> |<span data-ttu-id="a779e-300">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-300">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-301">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-301">Request Body</span></span> |<span data-ttu-id="a779e-302">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-302">NONE</span></span> |

<span data-ttu-id="a779e-303">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-303">**Response**:</span></span>

<span data-ttu-id="a779e-304">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-304">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="a779e-306">6. 모델 고급</span><span class="sxs-lookup"><span data-stu-id="a779e-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="a779e-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-307">6.1.</span></span>    <span data-ttu-id="a779e-308">모델 데이터 정보</span><span class="sxs-lookup"><span data-stu-id="a779e-308">Model Data Insight</span></span>
<span data-ttu-id="a779e-309">이 모델을 빌드할 때 사용된 사용 데이터에 대한 통계 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-309">Returns statistical data on the usage data that this model was built with.</span></span>

<span data-ttu-id="a779e-310">권장 사항 빌드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="a779e-311">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-311">HTTP Method</span></span> | <span data-ttu-id="a779e-312">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-313">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-314">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-315">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-315">Parameter Name</span></span> | <span data-ttu-id="a779e-316">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-317">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-317">modelId</span></span> |<span data-ttu-id="a779e-318">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-318">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-319">apiVersion</span></span> |<span data-ttu-id="a779e-320">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-320">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-321">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-321">Request Body</span></span> |<span data-ttu-id="a779e-322">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-322">NONE</span></span> |

<span data-ttu-id="a779e-323">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-323">**Response**:</span></span>

<span data-ttu-id="a779e-324">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-324">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-325">데이터는 속성 컬렉션으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-325">The data is returned as a collection of properties.</span></span>

* <span data-ttu-id="a779e-326">`feed/entry/id/content/properties/key` - 속성 이름 유지</span><span class="sxs-lookup"><span data-stu-id="a779e-326">`feed/entry/id/content/properties/key` - Holds the property name.</span></span>
* <span data-ttu-id="a779e-327">`feed/entry/id/content/properties/value` - 속성 값 유지</span><span class="sxs-lookup"><span data-stu-id="a779e-327">`feed/entry/id/content/properties/value` - Holds the property value.</span></span>

<span data-ttu-id="a779e-328">아래 표에서는 각 키가 나타내는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-328">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="a779e-329">키</span><span class="sxs-lookup"><span data-stu-id="a779e-329">Key</span></span> | <span data-ttu-id="a779e-330">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="a779e-331">AvgItemLength</span></span> |<span data-ttu-id="a779e-332">항목당 평균 고유 사용자 수</span><span class="sxs-lookup"><span data-stu-id="a779e-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="a779e-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="a779e-333">AvgUserLength</span></span> |<span data-ttu-id="a779e-334">사용자당 평균 고유 항목 수</span><span class="sxs-lookup"><span data-stu-id="a779e-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="a779e-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a779e-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="a779e-336">모델링할 수 없는 항목을 정리한 후의 항목 수</span><span class="sxs-lookup"><span data-stu-id="a779e-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="a779e-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a779e-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="a779e-338">모델링할 수 없는 사용자 및 항목을 정리한 후의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a779e-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="a779e-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a779e-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="a779e-340">모델링할 수 없는 사용자 및 항목을 정리한 후의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a779e-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="a779e-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="a779e-341">MaxItemLength</span></span> |<span data-ttu-id="a779e-342">가장 널리 사용되는 항목의 고유 사용자 수</span><span class="sxs-lookup"><span data-stu-id="a779e-342">Number of distinct users for the most popular item.</span></span> |
| <span data-ttu-id="a779e-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="a779e-343">MaxUserLength</span></span> |<span data-ttu-id="a779e-344">사용자의 최대 고유 항목 수</span><span class="sxs-lookup"><span data-stu-id="a779e-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="a779e-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="a779e-345">MinItemLength</span></span> |<span data-ttu-id="a779e-346">항목의 최대 고유 사용자 수</span><span class="sxs-lookup"><span data-stu-id="a779e-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="a779e-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="a779e-347">MinUserLength</span></span> |<span data-ttu-id="a779e-348">사용자의 최소 고유 항목 수</span><span class="sxs-lookup"><span data-stu-id="a779e-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="a779e-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a779e-349">RawNumberOfItems</span></span> |<span data-ttu-id="a779e-350">사용 파일에 있는 항목 수</span><span class="sxs-lookup"><span data-stu-id="a779e-350">Number of items in the usage files.</span></span> |
| <span data-ttu-id="a779e-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a779e-351">RawNumberOfUsers</span></span> |<span data-ttu-id="a779e-352">정리하기 전의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a779e-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="a779e-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a779e-353">RawNumberOfRecords</span></span> |<span data-ttu-id="a779e-354">정리하기 전의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a779e-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="a779e-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a779e-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="a779e-356">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a779e-356">N/A</span></span> |
| <span data-ttu-id="a779e-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a779e-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="a779e-358">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a779e-358">N/A</span></span> |
| <span data-ttu-id="a779e-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a779e-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="a779e-360">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a779e-360">N/A</span></span> |

<span data-ttu-id="a779e-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="a779e-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-362">6.2.</span></span>    <span data-ttu-id="a779e-363">모델 정보</span><span class="sxs-lookup"><span data-stu-id="a779e-363">Model Insight</span></span>
<span data-ttu-id="a779e-364">활성 빌드 또는 특정 빌드(지정된 경우)에 대한 모델 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-364">Returns model insight on the active build or (if given) on a specific build.</span></span>

<span data-ttu-id="a779e-365">권장 사항 빌드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="a779e-366">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-366">HTTP Method</span></span> | <span data-ttu-id="a779e-367">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-368">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-368">GET</span></span> |<span data-ttu-id="a779e-369">활성 빌드 ID 사용:</span><span class="sxs-lookup"><span data-stu-id="a779e-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-370">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-371">특정 빌드 ID 사용:</span><span class="sxs-lookup"><span data-stu-id="a779e-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-372">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-372">Parameter Name</span></span> | <span data-ttu-id="a779e-373">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-374">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-374">modelId</span></span> |<span data-ttu-id="a779e-375">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-375">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-376">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-376">buildId</span></span> |<span data-ttu-id="a779e-377">(선택 사항) - 성공적인 빌드를 식별하는 번호</span><span class="sxs-lookup"><span data-stu-id="a779e-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="a779e-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-378">apiVersion</span></span> |<span data-ttu-id="a779e-379">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-379">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-380">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-380">Request Body</span></span> |<span data-ttu-id="a779e-381">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-381">NONE</span></span> |

<span data-ttu-id="a779e-382">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-382">**Response**:</span></span>

<span data-ttu-id="a779e-383">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-383">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-384">데이터는 속성 컬렉션으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-384">The data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="a779e-385">아래 표에서는 각 키가 나타내는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-385">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="a779e-386">키</span><span class="sxs-lookup"><span data-stu-id="a779e-386">Key</span></span> | <span data-ttu-id="a779e-387">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="a779e-388">CatalogCoverage</span></span> |<span data-ttu-id="a779e-389">사용 패턴으로 모델링할 수 있는 카탈로그의 부분.</span><span class="sxs-lookup"><span data-stu-id="a779e-389">What part of the catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="a779e-390">나머지 항목에는 콘텐츠 기반 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-390">The rest of the items will need content-based features.</span></span> |
| <span data-ttu-id="a779e-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="a779e-391">Mpr</span></span> |<span data-ttu-id="a779e-392">모델의 평균 백분위수 순위.</span><span class="sxs-lookup"><span data-stu-id="a779e-392">Mean percentile ranking of the model.</span></span> <span data-ttu-id="a779e-393">낮을수록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-393">Lower is better.</span></span> |
| <span data-ttu-id="a779e-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="a779e-394">NumberOfDimensions</span></span> |<span data-ttu-id="a779e-395">행렬 인수 분해 알고리즘에서 사용된 차원 수</span><span class="sxs-lookup"><span data-stu-id="a779e-395">Number of dimensions used by the matrix factorization algorithm.</span></span> |

<span data-ttu-id="a779e-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="a779e-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-397">6.3.</span></span>    <span data-ttu-id="a779e-398">모델 샘플 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-398">Get Model Sample</span></span>
<span data-ttu-id="a779e-399">권장 사항 모델의 샘플을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-399">Gets a sample of the recommendation model.</span></span>

| <span data-ttu-id="a779e-400">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-400">HTTP Method</span></span> | <span data-ttu-id="a779e-401">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-402">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-403">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-404">특정 빌드 ID 사용:</span><span class="sxs-lookup"><span data-stu-id="a779e-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-405">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-406">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-406">Parameter Name</span></span> | <span data-ttu-id="a779e-407">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-408">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-408">modelId</span></span> |<span data-ttu-id="a779e-409">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-409">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-410">apiVersion</span></span> |<span data-ttu-id="a779e-411">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-411">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-412">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-412">Request Body</span></span> |<span data-ttu-id="a779e-413">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-413">NONE</span></span> |

<span data-ttu-id="a779e-414">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-414">**Response**:</span></span>

<span data-ttu-id="a779e-415">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-415">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-416">OData XML</span></span>

<span data-ttu-id="a779e-417">원시 텍스트 형식으로 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If the Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of the Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on the Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in the Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, The Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On the Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, The Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories to Tell in the Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, The Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic the Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in the Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, The Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, The X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell the President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In the Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, The Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of the Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, The Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in the Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (The Official Guide to the X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, The Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, The Truth Is Out There (The Official Guide to the X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, The Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of the Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where the Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, The God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (The Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in the Time of Cholera (Penguin Great Books of the 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, The Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories To Tell In The Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from the Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="a779e-418">7. 모델 비즈니스 규칙</span><span class="sxs-lookup"><span data-stu-id="a779e-418">7. Model Business Rules</span></span>
<span data-ttu-id="a779e-419">지원되는 규칙 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-419">These are the types of rules supported:</span></span>

* <span data-ttu-id="a779e-420"><strong>BlockList</strong> - 권장 사항 결과에서 반환하지 않을 항목 목록을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span></span> 
* <span data-ttu-id="a779e-421"><strong>FeatureBlockList</strong> - 해당 기능의 값을 기반으로 항목을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span></span>

<span data-ttu-id="a779e-422">*단일 차단 목록 규칙에 1000개보다 많은 항목을 전송하지 마세요. 호출 시간 제한에 도달할 수 있습니다. 1000개보다 많은 항목을 차단할 해야 할 경우 여러 개의 차단 목록을 호출하면 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="a779e-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="a779e-423"><strong>Upsale</strong> - 권장 사항 결과에서 항목을 강제로 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span></span>
* <span data-ttu-id="a779e-424"><strong>WhiteList</strong> - 허용 목록은 항목의 목록에서 권장 사항만 제안할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="a779e-425"><strong>FeatureWhiteList</strong> - 기능 허용 목록은 특정 기능 값을 가진 항목만 추천할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span></span>
* <span data-ttu-id="a779e-426"><strong>PerSeedBlockList</strong> - 권장 사항 결과로 반환할 수 없는 항목 목록을 항목별로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="a779e-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-427">7.1.</span></span>    <span data-ttu-id="a779e-428">모델 규칙 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-428">Get Model Rules</span></span>
| <span data-ttu-id="a779e-429">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-429">HTTP Method</span></span> | <span data-ttu-id="a779e-430">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-431">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a779e-432">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-433">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-433">Parameter Name</span></span> | <span data-ttu-id="a779e-434">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-435">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-435">modelId</span></span> |<span data-ttu-id="a779e-436">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-436">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-437">apiVersion</span></span> |<span data-ttu-id="a779e-438">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-438">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-439">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-439">Request Body</span></span> |<span data-ttu-id="a779e-440">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-440">NONE</span></span> |

<span data-ttu-id="a779e-441">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-441">**Response**:</span></span>

<span data-ttu-id="a779e-442">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="a779e-443">`feed/entry/content/properties/Id` – 이 규칙의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="a779e-444">`feed/entry/content/properties/Type` – 규칙 유형</span><span class="sxs-lookup"><span data-stu-id="a779e-444">`feed/entry/content/properties/Type` - Type of the rule.</span></span>
* <span data-ttu-id="a779e-445">`feed/entry/content/properties/Parameter` – 규칙 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a779e-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="a779e-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="a779e-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-447">7.2.</span></span>    <span data-ttu-id="a779e-448">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="a779e-448">Add Rule</span></span>
| <span data-ttu-id="a779e-449">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-449">HTTP Method</span></span> | <span data-ttu-id="a779e-450">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-451">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="a779e-452">HEADER</span><span class="sxs-lookup"><span data-stu-id="a779e-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a779e-453">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-453">Parameter Name</span></span> | <span data-ttu-id="a779e-454">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-455">apiVersion</span></span> |<span data-ttu-id="a779e-456">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-456">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-457">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-457">Request Body</span></span> | |

<span data-ttu-id="a779e-458"><ins>비즈니스 규칙에 대한 항목 ID를 제공할 때마다 항목의 외부 ID(카탈로그 파일에서 사용한 것과 동일한 ID)를 사용하도록 합니다</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span></span><br><span data-ttu-id="a779e-459">
<ins>BlockList 규칙을 추가하려면:</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-459">
<ins>To add a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a779e-460"><ins>
<ins>FeatureBlockList 규칙을 추가하려면:</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a779e-461"><ins>Upsale 규칙을 추가하려면:</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-461"><ins> To add an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="a779e-462">
<ins>WhiteList 규칙을 추가하려면:</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-462">
<ins>To add a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a779e-463"><ins>
<ins>FeatureWhiteList 규칙을 추가하려면:</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a779e-464"><ins>PerSeedBlockList 규칙을 추가하려면:</ins></span><span class="sxs-lookup"><span data-stu-id="a779e-464"><ins> To add a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="a779e-465">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-465">**Response**:</span></span>

<span data-ttu-id="a779e-466">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-466">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-467">이 API는 새로 만든 규칙을 해당 세부 정보와 함께 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-467">The API returns the newly created rule with its details.</span></span> <span data-ttu-id="a779e-468">다음 경로에서 규칙 속성을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-468">The rules property can be retrieved from the following paths:</span></span>

* <span data-ttu-id="a779e-469">`feed/entry/content/properties/Id` – 이 규칙의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="a779e-470">`feed/entry/content/properties/Type` – 규칙 유형: BlockList 또는 Upsale</span><span class="sxs-lookup"><span data-stu-id="a779e-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="a779e-471">`feed/entry/content/properties/Parameter` – 규칙 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a779e-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="a779e-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="a779e-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-473">7.3.</span></span>    <span data-ttu-id="a779e-474">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-474">Delete Rule</span></span>
| <span data-ttu-id="a779e-475">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-475">HTTP Method</span></span> | <span data-ttu-id="a779e-476">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-477">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-478">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-479">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-479">Parameter Name</span></span> | <span data-ttu-id="a779e-480">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-481">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-481">modelId</span></span> |<span data-ttu-id="a779e-482">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-482">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-483">filterId</span><span class="sxs-lookup"><span data-stu-id="a779e-483">filterId</span></span> |<span data-ttu-id="a779e-484">필터의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-484">Unique identifier of the filter</span></span> |
| <span data-ttu-id="a779e-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-485">apiVersion</span></span> |<span data-ttu-id="a779e-486">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-486">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-487">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-487">Request Body</span></span> |<span data-ttu-id="a779e-488">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-488">NONE</span></span> |

<span data-ttu-id="a779e-489">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-489">**Response**:</span></span>

<span data-ttu-id="a779e-490">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="a779e-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-491">7.4.</span></span>    <span data-ttu-id="a779e-492">모든 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-492">Delete All Rules</span></span>
| <span data-ttu-id="a779e-493">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-493">HTTP Method</span></span> | <span data-ttu-id="a779e-494">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-495">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-496">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-497">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-497">Parameter Name</span></span> | <span data-ttu-id="a779e-498">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-499">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-499">modelId</span></span> |<span data-ttu-id="a779e-500">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-500">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-501">apiVersion</span></span> |<span data-ttu-id="a779e-502">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-502">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-503">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-503">Request Body</span></span> |<span data-ttu-id="a779e-504">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-504">NONE</span></span> |

<span data-ttu-id="a779e-505">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-505">**Response**:</span></span>

<span data-ttu-id="a779e-506">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="a779e-507">8. 카탈로그</span><span class="sxs-lookup"><span data-stu-id="a779e-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="a779e-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-508">8.1.</span></span>    <span data-ttu-id="a779e-509">카탈로그 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-509">Import Catalog Data</span></span>
<span data-ttu-id="a779e-510">여러 번 호출하여 여러 카탈로그 파일을 같은 모델에 업로드하면 새 카탈로그 항목만 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="a779e-511">기존 항목은 원래 값으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-511">Existing items will remain with the original values.</span></span> <span data-ttu-id="a779e-512">이 메서드를 사용하여 카탈로그 데이터를 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="a779e-513">카탈로그 데이터는 다음 형식을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-513">The catalog data should follow the following format:</span></span>

* <span data-ttu-id="a779e-514">기능 사용 안 함 - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="a779e-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="a779e-515">기능 사용 - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="a779e-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="a779e-516">참고: 최대 파일 크기는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-516">Note: The maximum file size is 200MB.</span></span>

<span data-ttu-id="a779e-517">** 형식 세부 정보 **</span><span class="sxs-lookup"><span data-stu-id="a779e-517">** Format details **</span></span>

| <span data-ttu-id="a779e-518">이름</span><span class="sxs-lookup"><span data-stu-id="a779e-518">Name</span></span> | <span data-ttu-id="a779e-519">필수</span><span class="sxs-lookup"><span data-stu-id="a779e-519">Mandatory</span></span> | <span data-ttu-id="a779e-520">형식</span><span class="sxs-lookup"><span data-stu-id="a779e-520">Type</span></span> | <span data-ttu-id="a779e-521">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a779e-522">항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-522">Item Id</span></span> |<span data-ttu-id="a779e-523">예</span><span class="sxs-lookup"><span data-stu-id="a779e-523">Yes</span></span> |<span data-ttu-id="a779e-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="a779e-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a779e-525">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a779e-525">Max length: 50</span></span> |<span data-ttu-id="a779e-526">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="a779e-527">Item Name</span><span class="sxs-lookup"><span data-stu-id="a779e-527">Item Name</span></span> |<span data-ttu-id="a779e-528">예</span><span class="sxs-lookup"><span data-stu-id="a779e-528">Yes</span></span> |<span data-ttu-id="a779e-529">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a779e-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="a779e-530">최대 길이: 255</span><span class="sxs-lookup"><span data-stu-id="a779e-530">Max length: 255</span></span> |<span data-ttu-id="a779e-531">항목 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-531">Item name.</span></span> |
| <span data-ttu-id="a779e-532">Item Category</span><span class="sxs-lookup"><span data-stu-id="a779e-532">Item Category</span></span> |<span data-ttu-id="a779e-533">예</span><span class="sxs-lookup"><span data-stu-id="a779e-533">Yes</span></span> |<span data-ttu-id="a779e-534">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a779e-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a779e-535">최대 길이: 255</span><span class="sxs-lookup"><span data-stu-id="a779e-535">Max length: 255</span></span> |<span data-ttu-id="a779e-536">이 항목이 속하는 범주(예: 요리책, 드라마...). 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="a779e-537">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-537">Description</span></span> |<span data-ttu-id="a779e-538">아니요, 기능이 없는 경우(그러나 비어 있을 수 있음)</span><span class="sxs-lookup"><span data-stu-id="a779e-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="a779e-539">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a779e-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a779e-540">최대 길이: 4000</span><span class="sxs-lookup"><span data-stu-id="a779e-540">Max length: 4000</span></span> |<span data-ttu-id="a779e-541">이 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="a779e-541">Description of this item.</span></span> |
| <span data-ttu-id="a779e-542">Features list</span><span class="sxs-lookup"><span data-stu-id="a779e-542">Features list</span></span> |<span data-ttu-id="a779e-543">아니요</span><span class="sxs-lookup"><span data-stu-id="a779e-543">No</span></span> |<span data-ttu-id="a779e-544">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a779e-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a779e-545">최대 길이: 4000; 최대 기능 수: 20</span><span class="sxs-lookup"><span data-stu-id="a779e-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="a779e-546">쉼표로 구분된 기능 이름 목록 = 모델 권장 사항을 향상 시키기는 데 사용할 수 있는 기능 값; [고급 항목](#2-advanced-topics) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="a779e-547">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-547">HTTP Method</span></span> | <span data-ttu-id="a779e-548">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-549">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-550">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a779e-551">HEADER</span><span class="sxs-lookup"><span data-stu-id="a779e-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a779e-552">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-552">Parameter Name</span></span> | <span data-ttu-id="a779e-553">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-554">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-554">modelId</span></span> |<span data-ttu-id="a779e-555">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-555">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-556">filename</span><span class="sxs-lookup"><span data-stu-id="a779e-556">filename</span></span> |<span data-ttu-id="a779e-557">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="a779e-557">Textual identifier of the catalog.</span></span><br><span data-ttu-id="a779e-558">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a779e-559">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a779e-559">Max length: 50</span></span> |
| <span data-ttu-id="a779e-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-560">apiVersion</span></span> |<span data-ttu-id="a779e-561">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-561">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-562">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-562">Request Body</span></span> |<span data-ttu-id="a779e-563">예(기능 사용):</span><span class="sxs-lookup"><span data-stu-id="a779e-563">Example (with features):</span></span><br/><span data-ttu-id="a779e-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,책, 책 설명,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span><span class="sxs-lookup"><span data-stu-id="a779e-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="a779e-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),책,,author=Nick Bantock,publisher=Harpercollins,year=1997</span><span class="sxs-lookup"><span data-stu-id="a779e-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="a779e-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,책,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="a779e-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="a779e-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,책,책 설명,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span><span class="sxs-lookup"><span data-stu-id="a779e-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="a779e-568">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-568">**Response**:</span></span>

<span data-ttu-id="a779e-569">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-569">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-570">API는 가져오기 보고서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-570">The API returns a report of the import.</span></span>

* <span data-ttu-id="a779e-571">`feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="a779e-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="a779e-572">`feed\entry\content\properties\ErrorCount` – 오류로 인해 삽입되지 않은 줄 수</span><span class="sxs-lookup"><span data-stu-id="a779e-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="a779e-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="a779e-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-574">8.2.</span></span>    <span data-ttu-id="a779e-575">카탈로그 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-575">Get Catalog</span></span>
<span data-ttu-id="a779e-576">모든 카탈로그 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="a779e-577">한 번에 한 페이지씩 카탈로그가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-577">The catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="a779e-578">특정 인덱스에서 항목을 가져오려는 경우 $skip odata 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="a779e-579">예를 들어 100 위치에서 시작하는 항목을 가져오려면 $skip=100 매개 변수를 요청에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="a779e-580">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-580">HTTP Method</span></span> | <span data-ttu-id="a779e-581">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-582">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-583">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-584">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-584">Parameter Name</span></span> | <span data-ttu-id="a779e-585">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-586">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-586">modelId</span></span> |<span data-ttu-id="a779e-587">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-587">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-588">apiVersion</span></span> |<span data-ttu-id="a779e-589">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-589">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-590">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-590">Request Body</span></span> |<span data-ttu-id="a779e-591">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-591">NONE</span></span> |

<span data-ttu-id="a779e-592">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-592">**Response**:</span></span>

<span data-ttu-id="a779e-593">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-593">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-594">응답은 카탈로그 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-594">The response includes one entry per catalog item.</span></span> <span data-ttu-id="a779e-595">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-595">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-596">`feed/entry/content/properties/ExternalId` – 카탈로그 항목 외부 ID, 고객이 제공</span><span class="sxs-lookup"><span data-stu-id="a779e-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span></span>
* <span data-ttu-id="a779e-597">`feed/entry/content/properties/InternalId` – 카탈로그 항목 내부 ID, Azure Machine Learning 권장 사항에서 생성</span><span class="sxs-lookup"><span data-stu-id="a779e-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="a779e-598">`feed/entry/content/properties/Name` – 카탈로그 항목 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="a779e-599">`feed/entry/content/properties/Category` – 카탈로그 항목 범주</span><span class="sxs-lookup"><span data-stu-id="a779e-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="a779e-600">`feed/entry/content/properties/Description` – 카탈로그 항목 설명</span><span class="sxs-lookup"><span data-stu-id="a779e-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="a779e-601">`feed/entry/content/properties/Metadata` – 카탈로그 항목 메타데이터</span><span class="sxs-lookup"><span data-stu-id="a779e-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="a779e-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">The Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="a779e-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-603">8.3.</span></span>    <span data-ttu-id="a779e-604">토큰별 카탈로그 항목 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="a779e-605">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-605">HTTP Method</span></span> | <span data-ttu-id="a779e-606">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-607">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-608">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-609">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-609">Parameter Name</span></span> | <span data-ttu-id="a779e-610">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-611">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-611">modelId</span></span> |<span data-ttu-id="a779e-612">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-612">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-613">token</span><span class="sxs-lookup"><span data-stu-id="a779e-613">token</span></span> |<span data-ttu-id="a779e-614">카탈로그 항목 이름의 토큰</span><span class="sxs-lookup"><span data-stu-id="a779e-614">Token of the catalog item’s name.</span></span> <span data-ttu-id="a779e-615">3자 이상 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="a779e-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-616">apiVersion</span></span> |<span data-ttu-id="a779e-617">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-617">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-618">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-618">Request Body</span></span> |<span data-ttu-id="a779e-619">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-619">NONE</span></span> |

<span data-ttu-id="a779e-620">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-620">**Response**:</span></span>

<span data-ttu-id="a779e-621">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-621">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-622">응답은 카탈로그 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-622">The response includes one entry per catalog item.</span></span> <span data-ttu-id="a779e-623">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-623">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-624">`feed/entry/content/properties/InternalId` – 카탈로그 항목 내부 ID, Azure Machine Learning 권장 사항에서 생성</span><span class="sxs-lookup"><span data-stu-id="a779e-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="a779e-625">`feed/entry/content/properties/Name` – 카탈로그 항목 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="a779e-626">`feed/entry/content/properties/Rating` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a779e-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="a779e-627">`feed/entry/content/properties/Reasoning` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a779e-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="a779e-628">`feed/entry/content/properties/Metadata` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a779e-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="a779e-629">`feed/entry/content/properties/FormattedRating` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a779e-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="a779e-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="a779e-631">9. 사용 데이터</span><span class="sxs-lookup"><span data-stu-id="a779e-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="a779e-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-632">9.1.</span></span>    <span data-ttu-id="a779e-633">사용 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="a779e-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-634">9.1.1.</span></span> <span data-ttu-id="a779e-635">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="a779e-635">Uploading File</span></span>
<span data-ttu-id="a779e-636">이 섹션에서는 파일을 사용하여 사용 데이터를 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-636">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="a779e-637">사용 데이터를 사용하여 이 API를 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="a779e-638">모든 호출에 대한 모든 사용 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="a779e-639">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-639">HTTP Method</span></span> | <span data-ttu-id="a779e-640">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-641">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-642">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-643">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-643">Parameter Name</span></span> | <span data-ttu-id="a779e-644">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-645">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-645">modelId</span></span> |<span data-ttu-id="a779e-646">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-646">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-647">filename</span><span class="sxs-lookup"><span data-stu-id="a779e-647">filename</span></span> |<span data-ttu-id="a779e-648">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="a779e-648">Textual identifier of the catalog.</span></span><br><span data-ttu-id="a779e-649">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a779e-650">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a779e-650">Max length: 50</span></span> |
| <span data-ttu-id="a779e-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-651">apiVersion</span></span> |<span data-ttu-id="a779e-652">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-652">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-653">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-653">Request Body</span></span> |<span data-ttu-id="a779e-654">사용 데이터.</span><span class="sxs-lookup"><span data-stu-id="a779e-654">Usage data.</span></span> <span data-ttu-id="a779e-655">형식:</span><span class="sxs-lookup"><span data-stu-id="a779e-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="a779e-656">Name</span><span class="sxs-lookup"><span data-stu-id="a779e-656">Name</span></span></th><th><span data-ttu-id="a779e-657">필수</span><span class="sxs-lookup"><span data-stu-id="a779e-657">Mandatory</span></span></th><th><span data-ttu-id="a779e-658">형식</span><span class="sxs-lookup"><span data-stu-id="a779e-658">Type</span></span></th><th><span data-ttu-id="a779e-659">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-659">Description</span></span></th></tr><tr><td><span data-ttu-id="a779e-660">User Id</span><span class="sxs-lookup"><span data-stu-id="a779e-660">User Id</span></span></td><td><span data-ttu-id="a779e-661">예</span><span class="sxs-lookup"><span data-stu-id="a779e-661">Yes</span></span></td><td><span data-ttu-id="a779e-662">[A-z], [a-z], [0-9], [_] &#40;밑줄&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="a779e-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a779e-663">최대 길이: 255</span><span class="sxs-lookup"><span data-stu-id="a779e-663">Max length: 255</span></span> </td><td><span data-ttu-id="a779e-664">사용자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="a779e-665">항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-665">Item Id</span></span></td><td><span data-ttu-id="a779e-666">예</span><span class="sxs-lookup"><span data-stu-id="a779e-666">Yes</span></span></td><td><span data-ttu-id="a779e-667">[A-z], [a-z], [0-9], [&#95;] &#40;밑줄&#41;, [-] &#40;대시&#41;</span><span class="sxs-lookup"><span data-stu-id="a779e-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a779e-668">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a779e-668">Max length: 50</span></span></td><td><span data-ttu-id="a779e-669">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="a779e-670">Time</span><span class="sxs-lookup"><span data-stu-id="a779e-670">Time</span></span></td><td><span data-ttu-id="a779e-671">아니요</span><span class="sxs-lookup"><span data-stu-id="a779e-671">No</span></span></td><td><span data-ttu-id="a779e-672">날짜(형식): YYYY/MM/DDTHH:MM:SS(예: 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="a779e-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="a779e-673">데이터의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="a779e-674">이벤트</span><span class="sxs-lookup"><span data-stu-id="a779e-674">Event</span></span></td><td><span data-ttu-id="a779e-675">아니요. 지정하는 경우 날짜도 입력해야 함</span><span class="sxs-lookup"><span data-stu-id="a779e-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="a779e-676">다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-676">One of the following:</span></span><br><span data-ttu-id="a779e-677">• Click</span><span class="sxs-lookup"><span data-stu-id="a779e-677">• Click</span></span><br><span data-ttu-id="a779e-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="a779e-678">• RecommendationClick</span></span><br><span data-ttu-id="a779e-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="a779e-679">•    AddShopCart</span></span><br><span data-ttu-id="a779e-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="a779e-680">• RemoveShopCart</span></span><br><span data-ttu-id="a779e-681">• Purchase</span><span class="sxs-lookup"><span data-stu-id="a779e-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="a779e-682">최대 파일 크기 200MB</span><span class="sxs-lookup"><span data-stu-id="a779e-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="a779e-683">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="a779e-684">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-684">**Response**:</span></span>

<span data-ttu-id="a779e-685">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="a779e-686">`Feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="a779e-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="a779e-687">`Feed\entry\content\properties\ErrorCount` – 오류로 인해 삽입되지 않은 줄 수</span><span class="sxs-lookup"><span data-stu-id="a779e-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="a779e-688">`Feed\entry\content\properties\FileId` – 파일 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="a779e-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="a779e-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-690">9.1.2.</span></span> <span data-ttu-id="a779e-691">데이터 취득 사용</span><span class="sxs-lookup"><span data-stu-id="a779e-691">Using Data Acquisition</span></span>
<span data-ttu-id="a779e-692">이 섹션에서는 일반적으로 웹 사이트에서 Azure 기계 학습 권장 사항에 실시간으로 이벤트를 전송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="a779e-693">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-693">HTTP Method</span></span> | <span data-ttu-id="a779e-694">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-695">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="a779e-696">HEADER</span><span class="sxs-lookup"><span data-stu-id="a779e-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a779e-697">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-697">Parameter Name</span></span> | <span data-ttu-id="a779e-698">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-699">apiVersion</span></span> |<span data-ttu-id="a779e-700">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-700">1.0</span></span> |
| <span data-ttu-id="a779e-701">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-701">Request body</span></span> |<span data-ttu-id="a779e-702">Event data entry for each event you want to send.</span><span class="sxs-lookup"><span data-stu-id="a779e-702">Event data entry for each event you want to send.</span></span> <span data-ttu-id="a779e-703">SessionId 필드에서 같은 사용자 또는 브라우저 세션에 대해 같은 ID를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-703">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="a779e-704">아래 이벤트 본문 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="a779e-705">'Click' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a779e-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="a779e-706">'RecommendationClick' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a779e-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="a779e-707">'AddShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a779e-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="a779e-708">'RemoveShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a779e-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="a779e-709">'Purchase' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a779e-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="a779e-710">두 개의 이벤트 'Click' 및 'AddShopCart'를 보내는 예:</span><span class="sxs-lookup"><span data-stu-id="a779e-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="a779e-711">**응답**: HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="a779e-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-712">9.2.</span></span>    <span data-ttu-id="a779e-713">모델 사용 파일 나열</span><span class="sxs-lookup"><span data-stu-id="a779e-713">List Model Usage Files</span></span>
<span data-ttu-id="a779e-714">모든 모델 사용 파일의 메타데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="a779e-715">한 번에 한 페이지씩 사용 파일이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-715">The usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="a779e-716">각 페이지는 100개의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-716">Each page containes 100 items.</span></span> <span data-ttu-id="a779e-717">특정 인덱스에서 항목을 가져오려는 경우 $skip odata 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="a779e-718">예를 들어 100 위치에서 시작하는 항목을 가져오려면 $skip=100 매개 변수를 요청에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="a779e-719">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-719">HTTP Method</span></span> | <span data-ttu-id="a779e-720">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-721">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-722">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-723">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-723">Parameter Name</span></span> | <span data-ttu-id="a779e-724">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="a779e-725">forModelId</span></span> |<span data-ttu-id="a779e-726">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-726">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-727">apiVersion</span></span> |<span data-ttu-id="a779e-728">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-728">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-729">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-729">Request Body</span></span> |<span data-ttu-id="a779e-730">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-730">NONE</span></span> |

<span data-ttu-id="a779e-731">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-731">**Response**:</span></span>

<span data-ttu-id="a779e-732">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-732">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-733">응답은 사용 파일당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-733">The response includes one entry per usage file.</span></span> <span data-ttu-id="a779e-734">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-734">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-735">`feed\entry\content\properties\Id` – 사용 파일 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="a779e-736">`feed\entry\content\properties\Length` – 사용 파일 길이(MB)</span><span class="sxs-lookup"><span data-stu-id="a779e-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="a779e-737">`feed\entry\content\properties\DateModified` – 사용 파일이 만들어진 날짜</span><span class="sxs-lookup"><span data-stu-id="a779e-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span></span>
* <span data-ttu-id="a779e-738">`feed\entry\content\properties\UseInModel` – 사용 파일이 모델에서 사용되는지 여부</span><span class="sxs-lookup"><span data-stu-id="a779e-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span></span>

<span data-ttu-id="a779e-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="a779e-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-740">9.3.</span></span>    <span data-ttu-id="a779e-741">사용 통계 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-741">Get Usage Statistics</span></span>
<span data-ttu-id="a779e-742">사용 통계를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-742">Gets usage statistics.</span></span>

| <span data-ttu-id="a779e-743">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-743">HTTP Method</span></span> | <span data-ttu-id="a779e-744">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-745">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-746">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-747">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-747">Parameter Name</span></span> | <span data-ttu-id="a779e-748">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-749">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-749">modelId</span></span> |<span data-ttu-id="a779e-750">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-750">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-751">startDate</span><span class="sxs-lookup"><span data-stu-id="a779e-751">startDate</span></span> |<span data-ttu-id="a779e-752">시작 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-752">Start date.</span></span> <span data-ttu-id="a779e-753">형식: yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="a779e-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="a779e-754">endDate</span><span class="sxs-lookup"><span data-stu-id="a779e-754">endDate</span></span> |<span data-ttu-id="a779e-755">종료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-755">End date.</span></span> <span data-ttu-id="a779e-756">형식: yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="a779e-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="a779e-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="a779e-757">eventTypes</span></span> |<span data-ttu-id="a779e-758">쉼표로 구분된 이벤트 유형 문자열이거나 null(모든 이벤트를 가져오려는 경우)</span><span class="sxs-lookup"><span data-stu-id="a779e-758">Comma-separated string of event types or null to get all events</span></span> |
| <span data-ttu-id="a779e-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-759">apiVersion</span></span> |<span data-ttu-id="a779e-760">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-760">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-761">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-761">Request Body</span></span> |<span data-ttu-id="a779e-762">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-762">NONE</span></span> |

<span data-ttu-id="a779e-763">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-763">**Response**:</span></span>

<span data-ttu-id="a779e-764">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-764">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-765">키/값 요소의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-765">A collection of key/value elements.</span></span> <span data-ttu-id="a779e-766">각 컬렉션은 시간별로 그룹화된 특정 이벤트 유형에 대한 이벤트 합계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-766">Each one contains the sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="a779e-767">`feed\entry[i]\content\properties\Key` – 시간(시간별로 그룹화) 및 이벤트 유형 포함</span><span class="sxs-lookup"><span data-stu-id="a779e-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span></span>
* <span data-ttu-id="a779e-768">`feed\entry[i]\content\properties\Value` - 총 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="a779e-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="a779e-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="a779e-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-770">9.4.</span></span>    <span data-ttu-id="a779e-771">사용 파일 샘플 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-771">Get Usage File Sample</span></span>
<span data-ttu-id="a779e-772">사용 파일 내용의 처음 2KB를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-772">Retrieves the first 2KB of usage file content.</span></span>

| <span data-ttu-id="a779e-773">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-773">HTTP Method</span></span> | <span data-ttu-id="a779e-774">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-775">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-776">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-777">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-777">Parameter Name</span></span> | <span data-ttu-id="a779e-778">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-779">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-779">modelId</span></span> |<span data-ttu-id="a779e-780">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-780">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-781">fileId</span><span class="sxs-lookup"><span data-stu-id="a779e-781">fileId</span></span> |<span data-ttu-id="a779e-782">모델 사용 파일의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-782">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="a779e-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-783">apiVersion</span></span> |<span data-ttu-id="a779e-784">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-784">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-785">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-785">Request Body</span></span> |<span data-ttu-id="a779e-786">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-786">NONE</span></span> |

<span data-ttu-id="a779e-787">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-787">**Response**:</span></span>

<span data-ttu-id="a779e-788">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-788">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-789">원시 텍스트 형식으로 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="a779e-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="a779e-790">9.5.</span></span>    <span data-ttu-id="a779e-791">모델 사용 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-791">Get Model Usage File</span></span>
<span data-ttu-id="a779e-792">사용 파일의 전체 내용을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-792">Retrieves the full content of the usage file.</span></span>

| <span data-ttu-id="a779e-793">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-793">HTTP Method</span></span> | <span data-ttu-id="a779e-794">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-795">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-796">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-797">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-797">Parameter Name</span></span> | <span data-ttu-id="a779e-798">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-799">mId</span><span class="sxs-lookup"><span data-stu-id="a779e-799">mid</span></span> |<span data-ttu-id="a779e-800">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-800">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-801">fid</span><span class="sxs-lookup"><span data-stu-id="a779e-801">fid</span></span> |<span data-ttu-id="a779e-802">모델 사용 파일의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-802">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="a779e-803">다운로드</span><span class="sxs-lookup"><span data-stu-id="a779e-803">download</span></span> |<span data-ttu-id="a779e-804">1</span><span class="sxs-lookup"><span data-stu-id="a779e-804">1</span></span> |
| <span data-ttu-id="a779e-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-805">apiVersion</span></span> |<span data-ttu-id="a779e-806">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-806">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-807">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-807">Request Body</span></span> |<span data-ttu-id="a779e-808">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-808">NONE</span></span> |

<span data-ttu-id="a779e-809">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-809">**Response**:</span></span>

<span data-ttu-id="a779e-810">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-810">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-811">원시 텍스트 형식으로 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="a779e-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="a779e-812">9.6.</span></span>    <span data-ttu-id="a779e-813">사용 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-813">Delete Usage File</span></span>
<span data-ttu-id="a779e-814">지정한 모델 사용 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-814">Deletes the specified model usage file.</span></span>

| <span data-ttu-id="a779e-815">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-815">HTTP Method</span></span> | <span data-ttu-id="a779e-816">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-817">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-818">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-819">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-819">Parameter Name</span></span> | <span data-ttu-id="a779e-820">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-821">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-821">modelId</span></span> |<span data-ttu-id="a779e-822">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-822">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-823">fileId</span><span class="sxs-lookup"><span data-stu-id="a779e-823">fileId</span></span> |<span data-ttu-id="a779e-824">삭제할 파일의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-824">Unique identifier of the file to be deleted</span></span> |
| <span data-ttu-id="a779e-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-825">apiVersion</span></span> |<span data-ttu-id="a779e-826">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-826">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-827">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-827">Request Body</span></span> |<span data-ttu-id="a779e-828">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-828">NONE</span></span> |

<span data-ttu-id="a779e-829">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-829">**Response**:</span></span>

<span data-ttu-id="a779e-830">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="a779e-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="a779e-831">9.7.</span></span>    <span data-ttu-id="a779e-832">모든 사용 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-832">Delete All Usage Files</span></span>
<span data-ttu-id="a779e-833">모든 모델 사용 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="a779e-834">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-834">HTTP Method</span></span> | <span data-ttu-id="a779e-835">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-836">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-837">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-838">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-838">Parameter Name</span></span> | <span data-ttu-id="a779e-839">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-840">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-840">modelId</span></span> |<span data-ttu-id="a779e-841">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-841">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-842">apiVersion</span></span> |<span data-ttu-id="a779e-843">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-843">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-844">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-844">Request Body</span></span> |<span data-ttu-id="a779e-845">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-845">NONE</span></span> |

<span data-ttu-id="a779e-846">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-846">**Response**:</span></span>

<span data-ttu-id="a779e-847">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="a779e-848">10. 기능</span><span class="sxs-lookup"><span data-stu-id="a779e-848">10. Features</span></span>
<span data-ttu-id="a779e-849">이 섹션에서는 가져온 기능과 해당 값, 해당 순위 및 이 순위가 할당된 시점 등 기능 정보를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="a779e-850">기능은 카탈로그 데이터의 일부로 가져오며, 순위 빌드가 완료되면 해당 순위가 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="a779e-851">기능 순위는 사용 데이터의 패턴 및 항목 유형에 따라 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-851">Feature rank can change according to the pattern of usage data and type of items.</span></span> <span data-ttu-id="a779e-852">그러나 일관된 사용/항목을 위해 순위는 조금만 변동되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-852">But for consistent usage/items, the rank should have only small fluctuations.</span></span>
<span data-ttu-id="a779e-853">기능의 순위는 음수가 아닌 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-853">The rank of features is a non-negative number.</span></span> <span data-ttu-id="a779e-854">숫자 0은 기능의 순위가 매겨지지 않았음을 의미합니다(첫 번째 순위 빌드가 완료되기 전에 이 API를 호출한 경우에 발생).</span><span class="sxs-lookup"><span data-stu-id="a779e-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span></span> <span data-ttu-id="a779e-855">순위가 지정된 날짜를 점수 유효 시간이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-855">The date at which the rank was attributed is called the score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="a779e-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-856">10.1.</span></span> <span data-ttu-id="a779e-857">기능 정보 가져오기(마지막 순위 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="a779e-858">마지막으로 성공한 순위 빌드에 대해 순위를 포함한 기능 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-858">Retrieves the feature information, including ranking, for the last successful rank build.</span></span>

| <span data-ttu-id="a779e-859">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-859">HTTP Method</span></span> | <span data-ttu-id="a779e-860">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-861">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-862">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-863">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-863">Parameter Name</span></span> | <span data-ttu-id="a779e-864">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-865">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-865">modelId</span></span> |<span data-ttu-id="a779e-866">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-866">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="a779e-867">samplingSize</span></span> |<span data-ttu-id="a779e-868">카탈로그에 있는 데이터에 따라 각 기능에 대해 포함할 값 수</span><span class="sxs-lookup"><span data-stu-id="a779e-868">Number of values to include for each feature according to the data present in the catalog.</span></span> <br/><span data-ttu-id="a779e-869">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-869">Possible values are:</span></span><br> <span data-ttu-id="a779e-870">-1 - 모든 샘플.</span><span class="sxs-lookup"><span data-stu-id="a779e-870">-1 - All samples.</span></span> <br><span data-ttu-id="a779e-871">0 - 샘플링 없음.</span><span class="sxs-lookup"><span data-stu-id="a779e-871">0 - No sampling.</span></span> <br><span data-ttu-id="a779e-872">N - 각 기능 이름별로 N개의 샘플 반환.</span><span class="sxs-lookup"><span data-stu-id="a779e-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="a779e-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-873">apiVersion</span></span> |<span data-ttu-id="a779e-874">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-874">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-875">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-875">Request Body</span></span> |<span data-ttu-id="a779e-876">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-876">NONE</span></span> |

<span data-ttu-id="a779e-877">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-877">**Response**:</span></span>

<span data-ttu-id="a779e-878">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-878">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-879">응답은 기능 정보 항목의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-879">The response contains a list of feature info entries.</span></span> <span data-ttu-id="a779e-880">각 항목에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-880">Each entry contains:</span></span>

* <span data-ttu-id="a779e-881">`feed/entry/content/m:properties/d:Name` - 기능 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="a779e-882">`feed/entry/content/m:properties/d:RankUpdateDate` - 이 기능에 순위가 할당된 날짜(즉,</span><span class="sxs-lookup"><span data-stu-id="a779e-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="a779e-883">점수 유효 시간)</span><span class="sxs-lookup"><span data-stu-id="a779e-883">score freshness feature.</span></span> <span data-ttu-id="a779e-884">과거 날짜('0001-01-01T00:00:00')는 순위 빌드가 수행되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="a779e-885">`feed/entry/content/m:properties/d:Rank` - 기능 순위(부동 소수점).</span><span class="sxs-lookup"><span data-stu-id="a779e-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="a779e-886">2.0 이상의 순위가 유용한 기능으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="a779e-887">`feed/entry/content/m:properties/d:SampleValues` - 요청한 샘플링 크기까지의 쉼표로 구분된 값 목록</span><span class="sxs-lookup"><span data-stu-id="a779e-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="a779e-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get the features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="a779e-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-889">10.2.</span></span> <span data-ttu-id="a779e-890">기능 정보 가져오기(특정 순위 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="a779e-891">특정 순위 빌드에 대해 순위를 포함한 기능 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-891">Retrieves the feature information, including the ranking for a specific rank build.</span></span>

| <span data-ttu-id="a779e-892">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-892">HTTP Method</span></span> | <span data-ttu-id="a779e-893">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-894">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-895">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-896">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-896">Parameter Name</span></span> | <span data-ttu-id="a779e-897">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-898">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-898">modelId</span></span> |<span data-ttu-id="a779e-899">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-899">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="a779e-900">samplingSize</span></span> |<span data-ttu-id="a779e-901">카탈로그에 있는 데이터에 따라 각 기능에 대해 포함할 값 수</span><span class="sxs-lookup"><span data-stu-id="a779e-901">Number of values to include for each feature according to the data present in the catalog.</span></span><br/> <span data-ttu-id="a779e-902">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-902">Possible values are:</span></span><br> <span data-ttu-id="a779e-903">-1 - 모든 샘플.</span><span class="sxs-lookup"><span data-stu-id="a779e-903">-1 - All samples.</span></span> <br><span data-ttu-id="a779e-904">0 - 샘플링 없음.</span><span class="sxs-lookup"><span data-stu-id="a779e-904">0 - No sampling.</span></span> <br><span data-ttu-id="a779e-905">N - 각 기능 이름별로 N개의 샘플 반환.</span><span class="sxs-lookup"><span data-stu-id="a779e-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="a779e-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="a779e-906">rankBuildId</span></span> |<span data-ttu-id="a779e-907">순위 빌드의 고유 식별자 또는 마지막 순위 빌드의 경우 -1</span><span class="sxs-lookup"><span data-stu-id="a779e-907">Unique identifier of the rank build or -1 for the last rank build</span></span> |
| <span data-ttu-id="a779e-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-908">apiVersion</span></span> |<span data-ttu-id="a779e-909">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-909">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-910">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-910">Request Body</span></span> |<span data-ttu-id="a779e-911">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-911">NONE</span></span> |

<span data-ttu-id="a779e-912">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-912">**Response**:</span></span>

<span data-ttu-id="a779e-913">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-913">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-914">응답은 기능 정보 항목의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-914">The response contains a list of feature info entries.</span></span> <span data-ttu-id="a779e-915">각 항목에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-915">Each entry contains:</span></span>

* <span data-ttu-id="a779e-916">`feed/entry/content/m:properties/d:Name` - 기능 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="a779e-917">`feed/entry/content/m:properties/d:RankUpdateDate` - 이 기능에 순위가 할당된 날짜(즉,</span><span class="sxs-lookup"><span data-stu-id="a779e-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="a779e-918">점수 유효 시간)</span><span class="sxs-lookup"><span data-stu-id="a779e-918">score freshness feature.</span></span> <span data-ttu-id="a779e-919">과거 날짜('0001-01-01T00:00:00')는 순위 빌드가 수행되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="a779e-920">`feed/entry/content/m:properties/d:Rank` - 기능 순위(부동 소수점).</span><span class="sxs-lookup"><span data-stu-id="a779e-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="a779e-921">2.0 이상의 순위가 유용한 기능으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="a779e-922">`feed/entry/content/m:properties/d:SampleValues` - 요청한 샘플링 크기까지의 쉼표로 구분된 값 목록</span><span class="sxs-lookup"><span data-stu-id="a779e-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="a779e-923">OData</span><span class="sxs-lookup"><span data-stu-id="a779e-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get the features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="a779e-924">11. 빌드</span><span class="sxs-lookup"><span data-stu-id="a779e-924">11. Build</span></span>
  <span data-ttu-id="a779e-925">이 섹션에서는 빌드와 관련된 다른 API를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-925">This section explains the different APIs related to builds.</span></span> <span data-ttu-id="a779e-926">세 가지 유형의 빌드(권장 사항 빌드, 순위 빌드 및 FBT(자주 함께 구매됨) 빌드)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="a779e-927">권장 빌드는 예측에 사용되는 권장 사항 모델을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span></span> <span data-ttu-id="a779e-928">예측(이 유형의 빌드 관련)은 다음 두 가지 유형으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="a779e-929">I2I</span><span class="sxs-lookup"><span data-stu-id="a779e-929">I2I - a.k.a.</span></span> <span data-ttu-id="a779e-930">(항목-항목 권장 사항) - 항목 또는 항목 목록이 제공될 경우 이 옵션은 가장 높은 관심을 받을 항목 목록을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span></span>
* <span data-ttu-id="a779e-931">U2I</span><span class="sxs-lookup"><span data-stu-id="a779e-931">U2I - a.k.a.</span></span> <span data-ttu-id="a779e-932">(사용자-항목 권장 사항) - 사용자 ID(필요에 따라 항목 목록)가 제공될 경우 이 옵션은 지정된 사용자(및 추가 선택 항목)에 대해 가장 높은 관심을 받을 항목 목록을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span></span> <span data-ttu-id="a779e-933">U2I 권장 사항은 모델이 작성되었을 때까지 사용자에 대해 관심을 받은 항목의 기록을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span></span>

<span data-ttu-id="a779e-934">순위 빌드는 기능의 유용성에 대해 알아볼 수 있는 기술 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span></span> <span data-ttu-id="a779e-935">일반적으로 기능과 관련된 권장 사항 모델에 대한 최상의 결과를 얻으려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span></span>

* <span data-ttu-id="a779e-936">순위 빌드를 트리거(기능 점수가 안정적이지 않은 경우)하고 기능 점수를 얻을 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span></span>
* <span data-ttu-id="a779e-937">[Get Features Info](#101-get-features-info-for-last-rank-build) API를 호출하여 기능의 순위를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="a779e-938">다음 매개 변수를 사용하여 권장 사항 빌드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-938">Configure a recommendation build with the following parameters:</span></span>
  * <span data-ttu-id="a779e-939">`useFeatureInModel` - True로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-939">`useFeatureInModel` - Set to True.</span></span>
  * <span data-ttu-id="a779e-940">`ModelingFeatureList` - 이전 단계에서 검색한 순위에 따라 점수가 2.0 이상인 기능의 쉼표로 구분된 목록으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span></span>
  * <span data-ttu-id="a779e-941">`AllowColdItemPlacement` - True로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-941">`AllowColdItemPlacement` - Set to True.</span></span>
  * <span data-ttu-id="a779e-942">필요한 경우 `EnableFeatureCorrelation`을 True로 설정하고, `ReasoningFeatureList`을(를) 설명에 사용할 기능 목록(일반적으로 모델링 또는 하위 목록에 사용되는 동일한 기능 목록)으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="a779e-943">구성된 매개 변수를 사용하여 권장 사항 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-943">Trigger the recommendation build with the configured parameters.</span></span>

<span data-ttu-id="a779e-944">참고: 매개 변수를 구성하지 않은 경우(예: 매개 변수 없이 권장 사항 빌드를 호출한 경우) 또는 기능 사용을 명시적으로 해제하지 않은 경우(예: `UseFeatureInModel` 을 False로 설정) 순위 빌드가 있으면 기능 관련 매개 변수가 위에 설명된 값으로 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span></span>

<span data-ttu-id="a779e-945">같은 모델에 대해 순위 빌드와 권장 사항 빌드를 동시에 실행하는 것에 대한 제한 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span></span> <span data-ttu-id="a779e-946">그러나 같은 모델에서 동일한 유형의 두 빌드를 동시에 실행할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span></span>

<span data-ttu-id="a779e-947">FBT(자주 함께 구매됨) 빌드는 유형이 다른(같은 유형: 책, 영화, 일부 음식, 패션, 다른 유형: 컴퓨터와 장치, 크로스 도메인, 고도로 다양) 카탈로그에 적합한 “보수적인" 추천이라고도 하는 다른 권장 사항 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="a779e-948">참고: 업로드한 사용 파일에 선택적 필드 "event type"이 포함된 경우에는 FBT 모델링에 "Purchase" 이벤트만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="a779e-949">이벤트 유형이 제공되지 않은 경우에는 모든 이벤트가 구매로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="a779e-950">11.1 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a779e-950">11.1 Build parameters</span></span>
<span data-ttu-id="a779e-951">각 빌드 형식은 매개 변수 집합(아래 설명)을 통해 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="a779e-952">매개 변수를 구성하지 않으면 빌드를 트리거할 때 존재한 정보에 따라 매개 변수 값이 자동으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="a779e-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-953">11.1.1.</span></span> <span data-ttu-id="a779e-954">사용 콘덴서</span><span class="sxs-lookup"><span data-stu-id="a779e-954">Usage condenser</span></span>
<span data-ttu-id="a779e-955">사용 포인트가 거의 없는 사용자 또는 항목은 정보보다 노이즈를 더 많이 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="a779e-956">시스템에서는 모델에서 사용할 사용자/항목당 최소 사용 포인트 수를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span></span> <span data-ttu-id="a779e-957">이 수는 항목의 경우 ItemCutoffLowerBound 및 ItemCutoffUpperBound 매개 변수로 정의되는 범위 내에 속하며, 사용자의 경우 UserCutOffLowerBound 및 UserCutoffUpperBound 매개 변수로 정의되는 범위 내에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="a779e-958">항목 또는 사용자에 대한 콘덴서 효과는 해당 경계 중 하나 이상을 0으로 설정하여 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="a779e-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-959">11.1.2.</span></span> <span data-ttu-id="a779e-960">순위 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a779e-960">Rank build parameters</span></span>
<span data-ttu-id="a779e-961">아래 표에서는 순위 빌드에 대한 빌드 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-961">The table below depicts the build parameters for a rank build.</span></span>

| <span data-ttu-id="a779e-962">키</span><span class="sxs-lookup"><span data-stu-id="a779e-962">Key</span></span> | <span data-ttu-id="a779e-963">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-963">Description</span></span> | <span data-ttu-id="a779e-964">형식</span><span class="sxs-lookup"><span data-stu-id="a779e-964">Type</span></span> | <span data-ttu-id="a779e-965">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a779e-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a779e-966">NumberOfModelIterations</span></span> |<span data-ttu-id="a779e-967">모델에서 수행하는 반복 횟수는 전체 계산 시간과 모델 정확도로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="a779e-968">숫자가 높을수록 정확도는 높지만 계산 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="a779e-969">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-969">Integer</span></span> |<span data-ttu-id="a779e-970">10-50</span><span class="sxs-lookup"><span data-stu-id="a779e-970">10-50</span></span> |
| <span data-ttu-id="a779e-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a779e-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="a779e-972">차원 수는 모델이 데이터 내에서 찾으려는 '기능' 수와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="a779e-973">차원 수를 늘리면 결과를 더 작은 클러스터로 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="a779e-974">그러나 차원 수가 너무 많으면 모델이 항목 간의 상관 관계를 찾지 못하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-974">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="a779e-975">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-975">Integer</span></span> |<span data-ttu-id="a779e-976">10-40</span><span class="sxs-lookup"><span data-stu-id="a779e-976">10-40</span></span> |
| <span data-ttu-id="a779e-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a779e-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a779e-978">콘덴서의 항목 하한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-978">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="a779e-979">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-979">See usage condenser above.</span></span> |<span data-ttu-id="a779e-980">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-980">Integer</span></span> |<span data-ttu-id="a779e-981">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a779e-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a779e-983">콘덴서의 항목 상한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-983">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="a779e-984">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-984">See usage condenser above.</span></span> |<span data-ttu-id="a779e-985">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-985">Integer</span></span> |<span data-ttu-id="a779e-986">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a779e-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="a779e-988">콘덴서의 사용자 하한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-988">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="a779e-989">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-989">See usage condenser above.</span></span> |<span data-ttu-id="a779e-990">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-990">Integer</span></span> |<span data-ttu-id="a779e-991">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a779e-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="a779e-993">콘덴서의 사용자 상한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-993">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="a779e-994">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-994">See usage condenser above.</span></span> |<span data-ttu-id="a779e-995">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-995">Integer</span></span> |<span data-ttu-id="a779e-996">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="a779e-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-997">11.1.3.</span></span> <span data-ttu-id="a779e-998">권장 사항 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a779e-998">Recommendation build parameters</span></span>
<span data-ttu-id="a779e-999">아래 표에서는 권장 사항 빌드에 대한 빌드 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-999">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="a779e-1000">키</span><span class="sxs-lookup"><span data-stu-id="a779e-1000">Key</span></span> | <span data-ttu-id="a779e-1001">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1001">Description</span></span> | <span data-ttu-id="a779e-1002">형식</span><span class="sxs-lookup"><span data-stu-id="a779e-1002">Type</span></span> | <span data-ttu-id="a779e-1003">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a779e-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a779e-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="a779e-1005">모델에서 수행하는 반복 횟수는 전체 계산 시간과 모델 정확도로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="a779e-1006">숫자가 높을수록 정확도는 높지만 계산 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="a779e-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1007">Integer</span></span> |<span data-ttu-id="a779e-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="a779e-1008">10-50</span></span> |
| <span data-ttu-id="a779e-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a779e-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="a779e-1010">차원 수는 모델이 데이터 내에서 찾으려는 '기능' 수와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="a779e-1011">차원 수를 늘리면 결과를 더 작은 클러스터로 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="a779e-1012">그러나 차원 수가 너무 많으면 모델이 항목 간의 상관 관계를 찾지 못하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1012">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="a779e-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1013">Integer</span></span> |<span data-ttu-id="a779e-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="a779e-1014">10-40</span></span> |
| <span data-ttu-id="a779e-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a779e-1016">콘덴서의 항목 하한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1016">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="a779e-1017">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1017">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1018">Integer</span></span> |<span data-ttu-id="a779e-1019">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a779e-1021">콘덴서의 항목 상한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1021">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="a779e-1022">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1022">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1023">Integer</span></span> |<span data-ttu-id="a779e-1024">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="a779e-1026">콘덴서의 사용자 하한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1026">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="a779e-1027">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1027">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1028">Integer</span></span> |<span data-ttu-id="a779e-1029">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="a779e-1031">콘덴서의 사용자 상한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1031">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="a779e-1032">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1032">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1033">Integer</span></span> |<span data-ttu-id="a779e-1034">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1035">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1035">Description</span></span> |<span data-ttu-id="a779e-1036">빌드 설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1036">Build description.</span></span> |<span data-ttu-id="a779e-1037">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1037">String</span></span> |<span data-ttu-id="a779e-1038">모든 텍스트, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a779e-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="a779e-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="a779e-1039">EnableModelingInsights</span></span> |<span data-ttu-id="a779e-1040">권장 사항 모델에 대한 메트릭을 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1040">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="a779e-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1041">Boolean</span></span> |<span data-ttu-id="a779e-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1042">True/False</span></span> |
| <span data-ttu-id="a779e-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="a779e-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="a779e-1044">기능을 사용하여 권장 사항 모델을 개선할 수 있는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1044">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="a779e-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1045">Boolean</span></span> |<span data-ttu-id="a779e-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1046">True/False</span></span> |
| <span data-ttu-id="a779e-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="a779e-1047">ModelingFeatureList</span></span> |<span data-ttu-id="a779e-1048">권장 사항을 개선하기 위해 권장 사항 빌드에서 사용할 기능 이름의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="a779e-1049">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1049">String</span></span> |<span data-ttu-id="a779e-1050">기능 이름, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a779e-1050">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="a779e-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="a779e-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="a779e-1052">권장 사항에서 기능 유사성을 통해 콜드 항목을 푸시해야 하는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1052">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="a779e-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1053">Boolean</span></span> |<span data-ttu-id="a779e-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1054">True/False</span></span> |
| <span data-ttu-id="a779e-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="a779e-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="a779e-1056">추론에서 기능을 사용할 수 있는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="a779e-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1057">Boolean</span></span> |<span data-ttu-id="a779e-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1058">True/False</span></span> |
| <span data-ttu-id="a779e-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="a779e-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="a779e-1060">추론 문장(예: 권장 사항 설명)에 사용할 기능 이름의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="a779e-1061">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1061">String</span></span> |<span data-ttu-id="a779e-1062">기능 이름, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a779e-1062">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="a779e-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="a779e-1063">EnableU2I</span></span> |<span data-ttu-id="a779e-1064">U2I(사용자-항목 권장 사항)라고도 하는</span><span class="sxs-lookup"><span data-stu-id="a779e-1064">Allow the personalized recommendation a.k.a.</span></span> <span data-ttu-id="a779e-1065">개인 설정된 권장 구성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1065">U2I (user to item recommendations).</span></span> |<span data-ttu-id="a779e-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1066">Boolean</span></span> |<span data-ttu-id="a779e-1067">True/False(기본값 true)</span><span class="sxs-lookup"><span data-stu-id="a779e-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="a779e-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-1068">11.1.4.</span></span> <span data-ttu-id="a779e-1069">FBT 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a779e-1069">FBT build parameters</span></span>
<span data-ttu-id="a779e-1070">아래 표에서는 권장 사항 빌드에 대한 빌드 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1070">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="a779e-1071">키</span><span class="sxs-lookup"><span data-stu-id="a779e-1071">Key</span></span> | <span data-ttu-id="a779e-1072">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1072">Description</span></span> | <span data-ttu-id="a779e-1073">형식</span><span class="sxs-lookup"><span data-stu-id="a779e-1073">Type</span></span> | <span data-ttu-id="a779e-1074">유효한 값(기본값)</span><span class="sxs-lookup"><span data-stu-id="a779e-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a779e-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="a779e-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="a779e-1076">모델의 보수적인 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1076">How conservative the model is.</span></span> <span data-ttu-id="a779e-1077">모델링 시 고려할 항목의 공동 발생 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1077">Number of co-occurrences of items to be considered for modeling.</span></span> |<span data-ttu-id="a779e-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1078">Integer</span></span> |<span data-ttu-id="a779e-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="a779e-1079">3-50 (6)</span></span> |
| <span data-ttu-id="a779e-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="a779e-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="a779e-1081">FBT 집합의 항목 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1081">Bounds the number of items in a frequent set.</span></span> |<span data-ttu-id="a779e-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1082">Integer</span></span> |<span data-ttu-id="a779e-1083">2-3(2)</span><span class="sxs-lookup"><span data-stu-id="a779e-1083">2-3 (2)</span></span> |
| <span data-ttu-id="a779e-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="a779e-1084">FbtMinimalScore</span></span> |<span data-ttu-id="a779e-1085">반환된 결과에 포함하기 위해 필요한 FBT 집합의 최소 점수입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span></span> <span data-ttu-id="a779e-1086">높을수록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1086">The higher the better.</span></span> |<span data-ttu-id="a779e-1087">Double</span><span class="sxs-lookup"><span data-stu-id="a779e-1087">Double</span></span> |<span data-ttu-id="a779e-1088">0 이상(0)</span><span class="sxs-lookup"><span data-stu-id="a779e-1088">0 and above (0)</span></span> |
| <span data-ttu-id="a779e-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="a779e-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="a779e-1090">빌드에서 사용할 유사성 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1090">Defines the similarity function to be used by the build.</span></span> <span data-ttu-id="a779e-1091">Lift는 우연성을 우위에 두고, Co-occurrence는 예측 가능성을 우위에 두며, Jaccard는 이 둘을 적절히 절충합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span></span> |<span data-ttu-id="a779e-1092">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1092">String</span></span> |<span data-ttu-id="a779e-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="a779e-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="a779e-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-1094">11.2.</span></span> <span data-ttu-id="a779e-1095">권장 사항 빌드 트리거</span><span class="sxs-lookup"><span data-stu-id="a779e-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="a779e-1096">기본적으로 이 API는 권장 사항 모델 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="a779e-1097">기능의 점수를 매기기 위해 순위 빌드를 트리거하려면 빌드 형식 매개 변수가 있는 빌드 API 변형을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="a779e-1098">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1098">HTTP Method</span></span> | <span data-ttu-id="a779e-1099">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1100">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1101">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a779e-1102">HEADER</span><span class="sxs-lookup"><span data-stu-id="a779e-1102">HEADER</span></span> |<span data-ttu-id="a779e-1103">`"Content-Type", "text/xml"` (요청 본문을 보내는 경우)</span><span class="sxs-lookup"><span data-stu-id="a779e-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="a779e-1104">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1104">Parameter Name</span></span> | <span data-ttu-id="a779e-1105">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1106">modelId</span></span> |<span data-ttu-id="a779e-1107">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1107">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="a779e-1108">userDescription</span></span> |<span data-ttu-id="a779e-1109">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="a779e-1109">Textual identifier of the catalog.</span></span> <span data-ttu-id="a779e-1110">공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="a779e-1111">위 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1111">See example above.</span></span><br><span data-ttu-id="a779e-1112">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a779e-1112">Max length: 50</span></span> |
| <span data-ttu-id="a779e-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1113">apiVersion</span></span> |<span data-ttu-id="a779e-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-1115">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-1115">Request Body</span></span> |<span data-ttu-id="a779e-1116">왼쪽이 비어 있으면 빌드가 기본 빌드 매개 변수로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1116">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="a779e-1117">빌드 매개 변수를 설정하려면 다음 샘플과 같이 매개 변수를 본문에 XML로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span></span> <span data-ttu-id="a779e-1118">매개 변수에 대한 설명은 "빌드 매개 변수" 섹션을 참조하세요.`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="a779e-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="a779e-1119">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-1119">**Response**:</span></span>

<span data-ttu-id="a779e-1120">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1121">비동기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1121">This is an asynchronous API.</span></span> <span data-ttu-id="a779e-1122">응답으로 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="a779e-1123">빌드가 종료된 시점을 알려면 "모델의 빌드 상태 가져오기" API를 호출하여 응답에서 이 빌드 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="a779e-1124">데이터 크기에 따라 빌드를 가져오는 데 몇 분에서 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1124">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="a779e-1125">빌드가 종료될 때까지 권장 사항을 소비할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1125">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="a779e-1126">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a779e-1126">Valid build status:</span></span>

* <span data-ttu-id="a779e-1127">Create - 빌드 요청이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="a779e-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="a779e-1128">Queued – 빌드 요청을 보냈으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="a779e-1129">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="a779e-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="a779e-1130">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a779e-1131">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a779e-1132">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a779e-1133">Cancelling – 빌드에 대한 취소 요청을 보냄</span><span class="sxs-lookup"><span data-stu-id="a779e-1133">Cancelling - A cancel request for the build was sent.</span></span>

<span data-ttu-id="a779e-1134">다음 경로에서 빌드 ID를 찾을 수 있습니다. `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="a779e-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="a779e-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="a779e-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-1136">11.3.</span></span> <span data-ttu-id="a779e-1137">빌드(권장 사항, 순위 또는 FBT) 트리거</span><span class="sxs-lookup"><span data-stu-id="a779e-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="a779e-1138">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1138">HTTP Method</span></span> | <span data-ttu-id="a779e-1139">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1140">POST</span><span class="sxs-lookup"><span data-stu-id="a779e-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1141">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a779e-1142">HEADER</span><span class="sxs-lookup"><span data-stu-id="a779e-1142">HEADER</span></span> |<span data-ttu-id="a779e-1143">`"Content-Type", "text/xml"` (요청 본문을 보내는 경우)</span><span class="sxs-lookup"><span data-stu-id="a779e-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="a779e-1144">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1144">Parameter Name</span></span> | <span data-ttu-id="a779e-1145">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1146">modelId</span></span> |<span data-ttu-id="a779e-1147">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1147">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="a779e-1148">userDescription</span></span> |<span data-ttu-id="a779e-1149">카탈로그의 텍스트 식별자.</span><span class="sxs-lookup"><span data-stu-id="a779e-1149">Textual identifier of the catalog.</span></span> <span data-ttu-id="a779e-1150">공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="a779e-1151">위 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1151">See example above.</span></span><br><span data-ttu-id="a779e-1152">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a779e-1152">Max length: 50</span></span> |
| <span data-ttu-id="a779e-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="a779e-1153">buildType</span></span> |<span data-ttu-id="a779e-1154">호출할 빌드의 형식: </span><span class="sxs-lookup"><span data-stu-id="a779e-1154">Type of the build to invoke:</span></span> <br/> <span data-ttu-id="a779e-1155">- 권장 사항 빌드의 경우 'Recommendation'</span><span class="sxs-lookup"><span data-stu-id="a779e-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="a779e-1156">- 순위 빌드의 경우 'Ranking'</span><span class="sxs-lookup"><span data-stu-id="a779e-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="a779e-1157">- FBT 빌드의 경우 'Fbt'</span><span class="sxs-lookup"><span data-stu-id="a779e-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="a779e-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1158">apiVersion</span></span> |<span data-ttu-id="a779e-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-1160">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-1160">Request Body</span></span> |<span data-ttu-id="a779e-1161">왼쪽이 비어 있으면 빌드가 기본 빌드 매개 변수로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1161">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="a779e-1162">빌드 매개 변수를 설정하려면 다음 샘플과 같이 매개 변수를 본문에 XML로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span></span> <span data-ttu-id="a779e-1163">매개 변수에 대한 설명 및 매개 변수 전체 목록을 보려면 "빌드 매개 변수" 섹션을 참조하세요.`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="a779e-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="a779e-1164">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-1164">**Response**:</span></span>

<span data-ttu-id="a779e-1165">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1166">비동기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1166">This is an asynchronous API.</span></span> <span data-ttu-id="a779e-1167">응답으로 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="a779e-1168">빌드가 종료된 시점을 알려면 "모델의 빌드 상태 가져오기" API를 호출하여 응답에서 이 빌드 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="a779e-1169">데이터 크기에 따라 빌드를 가져오는 데 몇 분에서 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1169">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="a779e-1170">빌드가 종료될 때까지 권장 사항을 소비할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1170">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="a779e-1171">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a779e-1171">Valid build status:</span></span>

* <span data-ttu-id="a779e-1172">Create – 모델을 만듦</span><span class="sxs-lookup"><span data-stu-id="a779e-1172">Create - Model was created.</span></span>
* <span data-ttu-id="a779e-1173">Queued – 모델 빌드가 트리거되고 쿼리됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="a779e-1174">Building – 모델을 빌드하는 중</span><span class="sxs-lookup"><span data-stu-id="a779e-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="a779e-1175">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a779e-1176">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a779e-1177">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a779e-1178">Cancelling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="a779e-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a779e-1179">다음 경로에서 빌드 ID를 찾을 수 있습니다. `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="a779e-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="a779e-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="a779e-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-1181">11.4.</span></span> <span data-ttu-id="a779e-1182">모델의 빌드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="a779e-1183">지정된 모델의 빌드 및 해당 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="a779e-1184">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1184">HTTP Method</span></span> | <span data-ttu-id="a779e-1185">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1186">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1187">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1188">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1188">Parameter Name</span></span> | <span data-ttu-id="a779e-1189">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1190">modelId</span></span> |<span data-ttu-id="a779e-1191">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1191">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="a779e-1192">onlyLastBuild</span></span> |<span data-ttu-id="a779e-1193">모델의 빌드 기록을 모두 반환할지 또는 최신 빌드의 상태만 반환할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span></span> |
| <span data-ttu-id="a779e-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1194">apiVersion</span></span> |<span data-ttu-id="a779e-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1195">1.0</span></span> |

<span data-ttu-id="a779e-1196">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-1196">**Response**:</span></span>

<span data-ttu-id="a779e-1197">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1198">응답은 빌드당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1198">The response includes one entry per build.</span></span> <span data-ttu-id="a779e-1199">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1199">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1200">`feed/entry/content/properties/UserName` - 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1200">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="a779e-1201">`feed/entry/content/properties/ModelName` - 모델의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="a779e-1202">`feed/entry/content/properties/ModelId` – 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="a779e-1203">`feed/entry/content/properties/IsDeployed` – 빌드 배포 여부(즉,</span><span class="sxs-lookup"><span data-stu-id="a779e-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="a779e-1204">활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1204">active build).</span></span>
* <span data-ttu-id="a779e-1205">`feed/entry/content/properties/BuildId` – 빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="a779e-1206">`feed/entry/content/properties/BuildType` - 빌드의 형식</span><span class="sxs-lookup"><span data-stu-id="a779e-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="a779e-1207">`feed/entry/content/properties/Status` – 빌드 상태</span><span class="sxs-lookup"><span data-stu-id="a779e-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="a779e-1208">다음 중 하나일 수 있음: Error, Building, Queued, Cancelling, Cancelled, Success</span><span class="sxs-lookup"><span data-stu-id="a779e-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="a779e-1209">`feed/entry/content/properties/StatusMessage` – 자세한 상태 메시지(특정 상태에만 적용)</span><span class="sxs-lookup"><span data-stu-id="a779e-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="a779e-1210">`feed/entry/content/properties/Progress` – 빌드 진행률(%)</span><span class="sxs-lookup"><span data-stu-id="a779e-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="a779e-1211">`feed/entry/content/properties/StartTime` – 빌드 시작 시간</span><span class="sxs-lookup"><span data-stu-id="a779e-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="a779e-1212">`feed/entry/content/properties/EndTime` – 빌드 종료 시간</span><span class="sxs-lookup"><span data-stu-id="a779e-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="a779e-1213">`feed/entry/content/properties/ExecutionTime` – 빌드 기간</span><span class="sxs-lookup"><span data-stu-id="a779e-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="a779e-1214">`feed/entry/content/properties/ProgressStep` – 진행 중인 빌드의 현재 단계에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a779e-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="a779e-1215">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a779e-1215">Valid build status:</span></span>

* <span data-ttu-id="a779e-1216">Created – 빌드 요청 항목이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="a779e-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="a779e-1217">Queued – 빌드 요청이 트리거되었으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="a779e-1218">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="a779e-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="a779e-1219">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a779e-1220">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a779e-1221">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a779e-1222">Cancelling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="a779e-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a779e-1223">유효한 빌드 형식 값:</span><span class="sxs-lookup"><span data-stu-id="a779e-1223">Valid values for build type:</span></span>

* <span data-ttu-id="a779e-1224">Rank - 순위 빌드</span><span class="sxs-lookup"><span data-stu-id="a779e-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="a779e-1225">Recommendation - 권장 사항 빌드</span><span class="sxs-lookup"><span data-stu-id="a779e-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="a779e-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="a779e-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="a779e-1227">11.5.</span></span> <span data-ttu-id="a779e-1228">빌드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-1228">Get Builds Status</span></span>
<span data-ttu-id="a779e-1229">사용자의 모든 모델에 대한 빌드 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="a779e-1230">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1230">HTTP Method</span></span> | <span data-ttu-id="a779e-1231">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1232">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1233">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1234">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1234">Parameter Name</span></span> | <span data-ttu-id="a779e-1235">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="a779e-1236">onlyLastBuild</span></span> |<span data-ttu-id="a779e-1237">모델의 빌드 기록을 모두 반환할지 또는 최신 빌드의 상태만 반환할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="a779e-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1238">apiVersion</span></span> |<span data-ttu-id="a779e-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1239">1.0</span></span> |

<span data-ttu-id="a779e-1240">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-1240">**Response**:</span></span>

<span data-ttu-id="a779e-1241">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1242">응답은 빌드당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1242">The response includes one entry per build.</span></span> <span data-ttu-id="a779e-1243">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1243">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1244">`feed/entry/content/properties/UserName` - 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1244">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="a779e-1245">`feed/entry/content/properties/ModelName` - 모델의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="a779e-1246">`feed/entry/content/properties/ModelId` – 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="a779e-1247">`feed/entry/content/properties/IsDeployed` – 빌드 배포 여부</span><span class="sxs-lookup"><span data-stu-id="a779e-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span></span>
* <span data-ttu-id="a779e-1248">`feed/entry/content/properties/BuildId` – 빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="a779e-1249">`feed/entry/content/properties/BuildType` - 빌드의 형식</span><span class="sxs-lookup"><span data-stu-id="a779e-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="a779e-1250">`feed/entry/content/properties/Status` – 빌드 상태</span><span class="sxs-lookup"><span data-stu-id="a779e-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="a779e-1251">다음 중 하나일 수 있음: Error, Building, Queued, Cancelled, Cancelling, Success</span><span class="sxs-lookup"><span data-stu-id="a779e-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="a779e-1252">`feed/entry/content/properties/StatusMessage` – 자세한 상태 메시지(특정 상태에만 적용)</span><span class="sxs-lookup"><span data-stu-id="a779e-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="a779e-1253">`feed/entry/content/properties/Progress` – 빌드 진행률(%)</span><span class="sxs-lookup"><span data-stu-id="a779e-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="a779e-1254">`feed/entry/content/properties/StartTime` – 빌드 시작 시간</span><span class="sxs-lookup"><span data-stu-id="a779e-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="a779e-1255">`feed/entry/content/properties/EndTime` – 빌드 종료 시간</span><span class="sxs-lookup"><span data-stu-id="a779e-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="a779e-1256">`feed/entry/content/properties/ExecutionTime` – 빌드 기간</span><span class="sxs-lookup"><span data-stu-id="a779e-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="a779e-1257">`feed/entry/content/properties/ProgressStep` – 진행 중인 빌드의 현재 단계에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a779e-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="a779e-1258">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a779e-1258">Valid build status:</span></span>

* <span data-ttu-id="a779e-1259">Created – 빌드 요청 항목이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="a779e-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="a779e-1260">Queued – 빌드 요청이 트리거되었으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="a779e-1261">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="a779e-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="a779e-1262">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a779e-1263">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a779e-1264">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a779e-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a779e-1265">Cancelling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="a779e-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a779e-1266">유효한 빌드 형식 값:</span><span class="sxs-lookup"><span data-stu-id="a779e-1266">Valid values for build type:</span></span>

* <span data-ttu-id="a779e-1267">Rank - 순위 빌드</span><span class="sxs-lookup"><span data-stu-id="a779e-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="a779e-1268">Recommendation - 권장 사항 빌드</span><span class="sxs-lookup"><span data-stu-id="a779e-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="a779e-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="a779e-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="a779e-1270">11.6.</span></span> <span data-ttu-id="a779e-1271">빌드 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-1271">Delete Build</span></span>
<span data-ttu-id="a779e-1272">빌드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1272">Deletes a build.</span></span>

<span data-ttu-id="a779e-1273">참고: </span><span class="sxs-lookup"><span data-stu-id="a779e-1273">NOTE:</span></span> <br><span data-ttu-id="a779e-1274">활성 빌드는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1274">You cannot delete an active build.</span></span> <span data-ttu-id="a779e-1275">활성 빌드를 삭제하려면 먼저 모델을 다른 활성 빌드로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1275">The model should be updated to a different active build before you delete it.</span></span><br><span data-ttu-id="a779e-1276">진행 중인 빌드는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="a779e-1277">먼저 <strong>빌드 취소</strong>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="a779e-1278">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1278">HTTP Method</span></span> | <span data-ttu-id="a779e-1279">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1280">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1281">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1282">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1282">Parameter Name</span></span> | <span data-ttu-id="a779e-1283">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1284">buildId</span></span> |<span data-ttu-id="a779e-1285">빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1285">Unique identifier of the build.</span></span> |
| <span data-ttu-id="a779e-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1286">apiVersion</span></span> |<span data-ttu-id="a779e-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1287">1.0</span></span> |

<span data-ttu-id="a779e-1288">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1288">**Response:**</span></span>

<span data-ttu-id="a779e-1289">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="a779e-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="a779e-1290">11.7.</span></span> <span data-ttu-id="a779e-1291">빌드 취소</span><span class="sxs-lookup"><span data-stu-id="a779e-1291">Cancel Build</span></span>
<span data-ttu-id="a779e-1292">빌드 중 상태인 빌드를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="a779e-1293">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1293">HTTP Method</span></span> | <span data-ttu-id="a779e-1294">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="a779e-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1296">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1297">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1297">Parameter Name</span></span> | <span data-ttu-id="a779e-1298">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1299">buildId</span></span> |<span data-ttu-id="a779e-1300">빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1300">Unique identifier of the build.</span></span> |
| <span data-ttu-id="a779e-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1301">apiVersion</span></span> |<span data-ttu-id="a779e-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1302">1.0</span></span> |

<span data-ttu-id="a779e-1303">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1303">**Response:**</span></span>

<span data-ttu-id="a779e-1304">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="a779e-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="a779e-1305">11.8.</span></span> <span data-ttu-id="a779e-1306">빌드 매개 변수 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-1306">Get Build Parameters</span></span>
<span data-ttu-id="a779e-1307">빌드 매개 변수를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="a779e-1308">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1308">HTTP Method</span></span> | <span data-ttu-id="a779e-1309">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1310">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1311">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1312">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1312">Parameter Name</span></span> | <span data-ttu-id="a779e-1313">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1314">buildId</span></span> |<span data-ttu-id="a779e-1315">빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1315">Unique identifier of the build.</span></span> |
| <span data-ttu-id="a779e-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1316">apiVersion</span></span> |<span data-ttu-id="a779e-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1317">1.0</span></span> |

<span data-ttu-id="a779e-1318">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1318">**Response:**</span></span>

<span data-ttu-id="a779e-1319">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1320">이 API는 키/값 요소의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="a779e-1321">각 요소는 매개 변수와 해당 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="a779e-1322">`feed/entry/content/properties/Key` - 빌드 매개 변수 이름.</span><span class="sxs-lookup"><span data-stu-id="a779e-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="a779e-1323">`feed/entry/content/properties/Value` - 빌드 매개 변수 값.</span><span class="sxs-lookup"><span data-stu-id="a779e-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="a779e-1324">아래 표에서는 각 키가 나타내는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1324">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="a779e-1325">키</span><span class="sxs-lookup"><span data-stu-id="a779e-1325">Key</span></span> | <span data-ttu-id="a779e-1326">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1326">Description</span></span> | <span data-ttu-id="a779e-1327">형식</span><span class="sxs-lookup"><span data-stu-id="a779e-1327">Type</span></span> | <span data-ttu-id="a779e-1328">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a779e-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a779e-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="a779e-1330">모델에서 수행하는 반복 횟수는 전체 계산 시간과 모델 정확도로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="a779e-1331">숫자가 높을수록 정확도는 높지만 계산 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="a779e-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1332">Integer</span></span> |<span data-ttu-id="a779e-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="a779e-1333">10-50</span></span> |
| <span data-ttu-id="a779e-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a779e-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="a779e-1335">차원 수는 모델이 데이터 내에서 찾으려는 '기능' 수와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="a779e-1336">차원 수를 늘리면 결과를 더 작은 클러스터로 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="a779e-1337">그러나 차원 수가 너무 많으면 모델이 항목 간의 상관 관계를 찾지 못하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1337">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="a779e-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1338">Integer</span></span> |<span data-ttu-id="a779e-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="a779e-1339">10-40</span></span> |
| <span data-ttu-id="a779e-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a779e-1341">콘덴서의 항목 하한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1341">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="a779e-1342">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1342">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1343">Integer</span></span> |<span data-ttu-id="a779e-1344">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a779e-1346">콘덴서의 항목 상한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1346">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="a779e-1347">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1347">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1348">Integer</span></span> |<span data-ttu-id="a779e-1349">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="a779e-1351">콘덴서의 사용자 하한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1351">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="a779e-1352">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1352">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1353">Integer</span></span> |<span data-ttu-id="a779e-1354">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a779e-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="a779e-1356">콘덴서의 사용자 상한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1356">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="a779e-1357">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a779e-1357">See usage condenser above.</span></span> |<span data-ttu-id="a779e-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="a779e-1358">Integer</span></span> |<span data-ttu-id="a779e-1359">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a779e-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a779e-1360">설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1360">Description</span></span> |<span data-ttu-id="a779e-1361">빌드 설명</span><span class="sxs-lookup"><span data-stu-id="a779e-1361">Build description.</span></span> |<span data-ttu-id="a779e-1362">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1362">String</span></span> |<span data-ttu-id="a779e-1363">모든 텍스트, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a779e-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="a779e-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="a779e-1364">EnableModelingInsights</span></span> |<span data-ttu-id="a779e-1365">권장 사항 모델에 대한 메트릭을 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1365">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="a779e-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1366">Boolean</span></span> |<span data-ttu-id="a779e-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1367">True/False</span></span> |
| <span data-ttu-id="a779e-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="a779e-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="a779e-1369">기능을 사용하여 권장 사항 모델을 개선할 수 있는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1369">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="a779e-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1370">Boolean</span></span> |<span data-ttu-id="a779e-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1371">True/False</span></span> |
| <span data-ttu-id="a779e-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="a779e-1372">ModelingFeatureList</span></span> |<span data-ttu-id="a779e-1373">권장 사항을 개선하기 위해 권장 사항 빌드에서 사용할 기능 이름의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="a779e-1374">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1374">String</span></span> |<span data-ttu-id="a779e-1375">기능 이름, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a779e-1375">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="a779e-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="a779e-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="a779e-1377">권장 사항에서 기능 유사성을 통해 콜드 항목을 푸시해야 하는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1377">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="a779e-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1378">Boolean</span></span> |<span data-ttu-id="a779e-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1379">True/False</span></span> |
| <span data-ttu-id="a779e-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="a779e-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="a779e-1381">추론에서 기능을 사용할 수 있는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="a779e-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="a779e-1382">Boolean</span></span> |<span data-ttu-id="a779e-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="a779e-1383">True/False</span></span> |
| <span data-ttu-id="a779e-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="a779e-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="a779e-1385">추론 문장(예: 권장 사항 설명)에 사용할 기능 이름의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="a779e-1386">String</span><span class="sxs-lookup"><span data-stu-id="a779e-1386">String</span></span> |<span data-ttu-id="a779e-1387">기능 이름, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a779e-1387">Feature names, up to 512 chars</span></span> |

<span data-ttu-id="a779e-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="a779e-1389">12. 권장 사항</span><span class="sxs-lookup"><span data-stu-id="a779e-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="a779e-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-1390">12.1.</span></span> <span data-ttu-id="a779e-1391">항목 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="a779e-1392">활성 빌드 형식이 "Recommendation" 또는 시드(입력) 항목 목록을 기반으로 하는 "Fbt"인 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="a779e-1393">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1393">HTTP Method</span></span> | <span data-ttu-id="a779e-1394">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1395">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1396">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1397">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1397">Parameter Name</span></span> | <span data-ttu-id="a779e-1398">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1399">modelId</span></span> |<span data-ttu-id="a779e-1400">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1400">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="a779e-1401">itemIds</span></span> |<span data-ttu-id="a779e-1402">권장할 항목의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1402">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="a779e-1403">활성 빌드가 FBT 형식인 경우에는 항목을 하나만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1403">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="a779e-1404">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a779e-1404">Max length: 1024</span></span> |
| <span data-ttu-id="a779e-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1405">numberOfResults</span></span> |<span data-ttu-id="a779e-1406">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1406">Number of required results</span></span> <br> <span data-ttu-id="a779e-1407">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a779e-1407">Max: 150</span></span> |
| <span data-ttu-id="a779e-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1408">includeMetatadata</span></span> |<span data-ttu-id="a779e-1409">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1409">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1410">apiVersion</span></span> |<span data-ttu-id="a779e-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1411">1.0</span></span> |

<span data-ttu-id="a779e-1412">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1412">**Response:**</span></span>

<span data-ttu-id="a779e-1413">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1414">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1414">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1415">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1415">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1416">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1417">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1417">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1418">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1419">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1420">아래 예제 응답은 10개의 권장 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1420">The example response below includes 10 recommended items.</span></span>

<span data-ttu-id="a779e-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="a779e-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-1422">12.2.</span></span> <span data-ttu-id="a779e-1423">항목 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="a779e-1424">특정 빌드 형식 "Recommendation" 또는 "Fbt"의 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="a779e-1425">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1425">HTTP Method</span></span> | <span data-ttu-id="a779e-1426">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1427">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1428">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1429">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1429">Parameter Name</span></span> | <span data-ttu-id="a779e-1430">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1431">modelId</span></span> |<span data-ttu-id="a779e-1432">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1432">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="a779e-1433">itemIds</span></span> |<span data-ttu-id="a779e-1434">권장할 항목의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1434">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="a779e-1435">활성 빌드가 FBT 형식인 경우에는 항목을 하나만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1435">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="a779e-1436">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a779e-1436">Max length: 1024</span></span> |
| <span data-ttu-id="a779e-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1437">numberOfResults</span></span> |<span data-ttu-id="a779e-1438">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1438">Number of required results</span></span> <br> <span data-ttu-id="a779e-1439">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a779e-1439">Max: 150</span></span> |
| <span data-ttu-id="a779e-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1440">includeMetatadata</span></span> |<span data-ttu-id="a779e-1441">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1441">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1442">buildId</span></span> |<span data-ttu-id="a779e-1443">이 권장 사항 요청에 사용할 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1443">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="a779e-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1444">apiVersion</span></span> |<span data-ttu-id="a779e-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1445">1.0</span></span> |

<span data-ttu-id="a779e-1446">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1446">**Response:**</span></span>

<span data-ttu-id="a779e-1447">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1448">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1448">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1449">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1449">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1450">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1451">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1451">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1452">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1453">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1454">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a779e-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="a779e-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-1455">12.3.</span></span> <span data-ttu-id="a779e-1456">FBT 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="a779e-1457">활성 빌드 형식이 시드(입력) 항목 목록을 기반으로 하는 "Fbt"인 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="a779e-1458">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1458">HTTP Method</span></span> | <span data-ttu-id="a779e-1459">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1460">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1461">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1462">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1462">Parameter Name</span></span> | <span data-ttu-id="a779e-1463">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1464">modelId</span></span> |<span data-ttu-id="a779e-1465">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1465">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="a779e-1466">itemId</span></span> |<span data-ttu-id="a779e-1467">권장할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1467">Item to recommend for.</span></span> <br><span data-ttu-id="a779e-1468">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a779e-1468">Max length: 1024</span></span> |
| <span data-ttu-id="a779e-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1469">numberOfResults</span></span> |<span data-ttu-id="a779e-1470">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1470">Number of required results</span></span> <br><span data-ttu-id="a779e-1471">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a779e-1471">Max: 150</span></span> |
| <span data-ttu-id="a779e-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="a779e-1472">minimalScore</span></span> |<span data-ttu-id="a779e-1473">반환된 결과에 포함하기 위해 필요한 FBT 집합의 최소 점수입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1473">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="a779e-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1474">includeMetatadata</span></span> |<span data-ttu-id="a779e-1475">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1475">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1476">apiVersion</span></span> |<span data-ttu-id="a779e-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1477">1.0</span></span> |

<span data-ttu-id="a779e-1478">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1478">**Response:**</span></span>

<span data-ttu-id="a779e-1479">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1480">응답은 권장 항목 집합(일반적으로 시드/입력 항목과 함께 구매하는 항목 집합)당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="a779e-1481">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1481">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1482">`Feed\entry\content\properties\Id1` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1483">`Feed\entry\content\properties\Name1` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1484">`Feed\entry\content\properties\Id2` - 두 번째 권장된 항목 ID(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a779e-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="a779e-1485">`Feed\entry\content\properties\Name2` – 두 번째 항목의 이름(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a779e-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="a779e-1486">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1487">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1488">아래 예제 응답은 3개의 권장 항목 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1488">The example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="a779e-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="a779e-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="a779e-1490">12.4.</span></span> <span data-ttu-id="a779e-1491">FBT 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="a779e-1492">특정 빌드 유형 "Fbt"의 권장 사항 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="a779e-1493">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1493">HTTP Method</span></span> | <span data-ttu-id="a779e-1494">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1495">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1496">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1497">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1497">Parameter Name</span></span> | <span data-ttu-id="a779e-1498">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1499">modelId</span></span> |<span data-ttu-id="a779e-1500">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1500">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="a779e-1501">itemId</span></span> |<span data-ttu-id="a779e-1502">권장할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1502">Item to recommend for.</span></span> <br><span data-ttu-id="a779e-1503">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a779e-1503">Max length: 1024</span></span> |
| <span data-ttu-id="a779e-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1504">numberOfResults</span></span> |<span data-ttu-id="a779e-1505">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1505">Number of required results</span></span> <br><span data-ttu-id="a779e-1506">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a779e-1506">Max: 150</span></span> |
| <span data-ttu-id="a779e-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="a779e-1507">minimalScore</span></span> |<span data-ttu-id="a779e-1508">반환된 결과에 포함하기 위해 필요한 FBT 집합의 최소 점수입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1508">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="a779e-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1509">includeMetatadata</span></span> |<span data-ttu-id="a779e-1510">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1510">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1511">buildId</span></span> |<span data-ttu-id="a779e-1512">이 권장 사항 요청에 사용할 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1512">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="a779e-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1513">apiVersion</span></span> |<span data-ttu-id="a779e-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1514">1.0</span></span> |

<span data-ttu-id="a779e-1515">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1515">**Response:**</span></span>

<span data-ttu-id="a779e-1516">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1517">응답은 권장 항목 집합(일반적으로 시드/입력 항목과 함께 구매하는 항목 집합)당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="a779e-1518">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1518">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1519">`Feed\entry\content\properties\Id1` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1520">`Feed\entry\content\properties\Name1` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1521">`Feed\entry\content\properties\Id2` - 두 번째 권장된 항목 ID(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a779e-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="a779e-1522">`Feed\entry\content\properties\Name2` – 두 번째 항목의 이름(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a779e-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="a779e-1523">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1524">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1525">12.3의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a779e-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="a779e-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="a779e-1526">12.5.</span></span> <span data-ttu-id="a779e-1527">사용자 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="a779e-1528">빌드 형식이 활성 빌드로 표시된 "Recommendation"인 사용자 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="a779e-1529">API는 사용자의 사용 기록에 따라 예측된 항목의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1529">The API will return a list of predicted item according to the usage history of the user.</span></span>

<span data-ttu-id="a779e-1530">참고:</span><span class="sxs-lookup"><span data-stu-id="a779e-1530">Notes:</span></span> 

1. <span data-ttu-id="a779e-1531">FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="a779e-1532">활성 빌드가 FBT이면 이 메서드는 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1532">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="a779e-1533">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1533">HTTP Method</span></span> | <span data-ttu-id="a779e-1534">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1535">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1536">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1537">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1537">Parameter Name</span></span> | <span data-ttu-id="a779e-1538">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1539">modelId</span></span> |<span data-ttu-id="a779e-1540">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1540">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1541">userId</span><span class="sxs-lookup"><span data-stu-id="a779e-1541">userId</span></span> |<span data-ttu-id="a779e-1542">사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1542">Unique identifier of the user</span></span> |
| <span data-ttu-id="a779e-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1543">numberOfResults</span></span> |<span data-ttu-id="a779e-1544">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1544">Number of required results</span></span> |
| <span data-ttu-id="a779e-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1545">includeMetatadata</span></span> |<span data-ttu-id="a779e-1546">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1546">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1547">apiVersion</span></span> |<span data-ttu-id="a779e-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1548">1.0</span></span> |

<span data-ttu-id="a779e-1549">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1549">**Response:**</span></span>

<span data-ttu-id="a779e-1550">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1551">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1551">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1552">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1552">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1553">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1554">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1554">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1555">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1556">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1557">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a779e-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="a779e-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="a779e-1558">12.6.</span></span> <span data-ttu-id="a779e-1559">항목 목록이 있는 사용자 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="a779e-1560">추가 항목 목록이 있으며 빌드 형식이 활성 빌드로 표시된 "Recommendation"인 사용자 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="a779e-1561">API는 사용자의 사용 기록에 따른 예측된 항목의 목록과 제공된 추가 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span></span>

<span data-ttu-id="a779e-1562">참고:</span><span class="sxs-lookup"><span data-stu-id="a779e-1562">Notes:</span></span> 

1. <span data-ttu-id="a779e-1563">FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="a779e-1564">활성 빌드가 FBT이면 이 메서드는 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1564">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="a779e-1565">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1565">HTTP Method</span></span> | <span data-ttu-id="a779e-1566">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1567">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1568">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1569">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1569">Parameter Name</span></span> | <span data-ttu-id="a779e-1570">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1571">modelId</span></span> |<span data-ttu-id="a779e-1572">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1572">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1573">userId</span><span class="sxs-lookup"><span data-stu-id="a779e-1573">userId</span></span> |<span data-ttu-id="a779e-1574">사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1574">Unique identifier of the user</span></span> |
| <span data-ttu-id="a779e-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="a779e-1575">itemsIds</span></span> |<span data-ttu-id="a779e-1576">권장할 항목의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1576">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="a779e-1577">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a779e-1577">Max length: 1024</span></span> |
| <span data-ttu-id="a779e-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1578">numberOfResults</span></span> |<span data-ttu-id="a779e-1579">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1579">Number of required results</span></span> |
| <span data-ttu-id="a779e-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1580">includeMetatadata</span></span> |<span data-ttu-id="a779e-1581">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1581">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1582">apiVersion</span></span> |<span data-ttu-id="a779e-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1583">1.0</span></span> |

<span data-ttu-id="a779e-1584">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1584">**Response:**</span></span>

<span data-ttu-id="a779e-1585">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1586">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1586">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1587">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1587">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1588">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1589">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1589">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1590">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1591">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1592">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a779e-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="a779e-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="a779e-1593">12.7.</span></span> <span data-ttu-id="a779e-1594">사용자 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="a779e-1595">특정 빌드 형식이 "Recommendation"인 사용자 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="a779e-1596">API는 사용자의 사용 기록에 따라 예측된 항목의 목록을 반환합니다(특정 빌드에 사용).</span><span class="sxs-lookup"><span data-stu-id="a779e-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span></span>

<span data-ttu-id="a779e-1597">참고: FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="a779e-1598">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1598">HTTP Method</span></span> | <span data-ttu-id="a779e-1599">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1600">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1601">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1602">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1602">Parameter Name</span></span> | <span data-ttu-id="a779e-1603">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1604">modelId</span></span> |<span data-ttu-id="a779e-1605">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1605">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1606">userId</span><span class="sxs-lookup"><span data-stu-id="a779e-1606">userId</span></span> |<span data-ttu-id="a779e-1607">사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1607">Unique identifier of the user</span></span> |
| <span data-ttu-id="a779e-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1608">numberOfResults</span></span> |<span data-ttu-id="a779e-1609">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1609">Number of required results</span></span> |
| <span data-ttu-id="a779e-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1610">includeMetatadata</span></span> |<span data-ttu-id="a779e-1611">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1611">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1612">buildId</span></span> |<span data-ttu-id="a779e-1613">이 권장 사항 요청에 사용할 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1613">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="a779e-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1614">apiVersion</span></span> |<span data-ttu-id="a779e-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1615">1.0</span></span> |

<span data-ttu-id="a779e-1616">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1616">**Response:**</span></span>

<span data-ttu-id="a779e-1617">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1618">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1618">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1619">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1619">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1620">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1621">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1621">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1622">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1623">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1624">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a779e-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="a779e-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="a779e-1625">12.8.</span></span> <span data-ttu-id="a779e-1626">항목 목록이 있는 사용자 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a779e-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="a779e-1627">특정 빌드 형식이 "Recommendation"인 사용자 권장 사항과 추가 항목 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span></span>

<span data-ttu-id="a779e-1628">API는 사용자의 사용 기록에 따른 예측된 항목 목록과 추가 항목 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span></span>

<span data-ttu-id="a779e-1629">참고: FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="a779e-1630">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1630">HTTP Method</span></span> | <span data-ttu-id="a779e-1631">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1632">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1633">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1634">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1634">Parameter Name</span></span> | <span data-ttu-id="a779e-1635">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1636">modelId</span></span> |<span data-ttu-id="a779e-1637">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1637">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1638">userId</span><span class="sxs-lookup"><span data-stu-id="a779e-1638">userId</span></span> |<span data-ttu-id="a779e-1639">사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1639">Unique identifier of the user</span></span> |
| <span data-ttu-id="a779e-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="a779e-1640">itemIds</span></span> |<span data-ttu-id="a779e-1641">권장할 항목의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1641">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="a779e-1642">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a779e-1642">Max length: 1024</span></span> |
| <span data-ttu-id="a779e-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a779e-1643">numberOfResults</span></span> |<span data-ttu-id="a779e-1644">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a779e-1644">Number of required results</span></span> |
| <span data-ttu-id="a779e-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a779e-1645">includeMetatadata</span></span> |<span data-ttu-id="a779e-1646">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a779e-1646">Future use, always false</span></span> |
| <span data-ttu-id="a779e-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1647">buildId</span></span> |<span data-ttu-id="a779e-1648">이 권장 사항 요청에 사용할 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1648">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="a779e-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1649">apiVersion</span></span> |<span data-ttu-id="a779e-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1650">1.0</span></span> |

<span data-ttu-id="a779e-1651">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1651">**Response:**</span></span>

<span data-ttu-id="a779e-1652">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1653">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1653">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1654">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1654">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1655">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1656">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1656">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1657">`Feed\entry\content\properties\Rating` - 권장 사항의 등급(숫자가 클수록 신뢰도가 높음)</span><span class="sxs-lookup"><span data-stu-id="a779e-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a779e-1658">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a779e-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a779e-1659">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a779e-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="a779e-1660">13. 사용자 사용 기록</span><span class="sxs-lookup"><span data-stu-id="a779e-1660">13. User Usage History</span></span>
<span data-ttu-id="a779e-1661">권장 모델이 작성되면 시스템은 작성에 사용된 사용자 기록(특정 사용자와 관련된 항목)을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span></span>
<span data-ttu-id="a779e-1662">이 API를 통해 사용자 기록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1662">This API allow to retrieve the user history</span></span>

<span data-ttu-id="a779e-1663">참고: 이 사용자 기록은 현재 권장 사항 작성에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1663">Note: the user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="a779e-1664">13.1 사용자 기록 검색</span><span class="sxs-lookup"><span data-stu-id="a779e-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="a779e-1665">활성 빌드 또는 지정된 사용자 ID에 대해 지정된 빌드에 사용되는 항목 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span></span>

| <span data-ttu-id="a779e-1666">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1666">HTTP Method</span></span> | <span data-ttu-id="a779e-1667">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1668">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1668">GET</span></span> |<span data-ttu-id="a779e-1669">활성 빌드에 대한 사용자 기록을 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-1669">Get the user history for the active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="a779e-1670">지정된 빌드에 대한 사용자 기록을 가져오기`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="a779e-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="a779e-1671">예:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="a779e-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="a779e-1672">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1672">Parameter Name</span></span> | <span data-ttu-id="a779e-1673">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1674">modelId</span></span> |<span data-ttu-id="a779e-1675">모델의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1675">the unique identifier of the model.</span></span> |
| <span data-ttu-id="a779e-1676">userId</span><span class="sxs-lookup"><span data-stu-id="a779e-1676">userId</span></span> |<span data-ttu-id="a779e-1677">사용자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1677">the unique identifier of the user.</span></span> |
| <span data-ttu-id="a779e-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="a779e-1678">buildId</span></span> |<span data-ttu-id="a779e-1679">사용자 기록을 가져올 원본 빌드를 나타내기 위한 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1679">optional parameter, allow to indicate from which build the user history should be fetch</span></span> |
| <span data-ttu-id="a779e-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1680">apiVersion</span></span> |<span data-ttu-id="a779e-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1681">1.0</span></span> |

<span data-ttu-id="a779e-1682">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1682">**Response:**</span></span>

<span data-ttu-id="a779e-1683">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1684">응답은 권장 항목당 하나의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1684">The response includes one entry per recommended item.</span></span> <span data-ttu-id="a779e-1685">각 항목에는 다음과 같은 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1685">Each entry has the following data:</span></span>

* <span data-ttu-id="a779e-1686">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a779e-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a779e-1687">`Feed\entry\content\properties\Name` - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1687">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="a779e-1688">`Feed\entry\content\properties\Rating` 해당 없음</span><span class="sxs-lookup"><span data-stu-id="a779e-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="a779e-1689">`Feed\entry\content\properties\Reasoning` 해당 없음</span><span class="sxs-lookup"><span data-stu-id="a779e-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="a779e-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="a779e-1691">14. 알림</span><span class="sxs-lookup"><span data-stu-id="a779e-1691">14. Notifications</span></span>
<span data-ttu-id="a779e-1692">Azure 기계 학습 권장 사항에서는 시스템에서 영구적 오류가 발생한 경우 알림을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span></span> <span data-ttu-id="a779e-1693">다음과 같은 세 가지 유형의 알림이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="a779e-1694">빌드 오류 – 이 알림은 모든 빌드 오류에 대해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="a779e-1695">데이터 취득 처리 오류 - 이 알림은 지난 5분간의 사용 이벤트 처리에서 모델당 오류가 100개가 넘는 경우 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span></span>
3. <span data-ttu-id="a779e-1696">권장 사항 소비 오류 - 이 알림은 지난 5분간의 권장 사항 요청 처리에서 모델당 오류가 100개가 넘는 경우 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="a779e-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="a779e-1697">14.1.</span></span> <span data-ttu-id="a779e-1698">알림 가져오기</span><span class="sxs-lookup"><span data-stu-id="a779e-1698">Get Notifications</span></span>
<span data-ttu-id="a779e-1699">모든 모델 또는 단일 모델에 대한 모든 알림을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1699">Retrieves all the notifications for all models or for a single model.</span></span>

| <span data-ttu-id="a779e-1700">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1700">HTTP Method</span></span> | <span data-ttu-id="a779e-1701">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1702">GET</span><span class="sxs-lookup"><span data-stu-id="a779e-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1703">모든 모델에 대한 모든 알림 가져오기:</span><span class="sxs-lookup"><span data-stu-id="a779e-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1704">특정 모델에 대한 알림을 가져오는 예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="a779e-1705">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1705">Parameter Name</span></span> | <span data-ttu-id="a779e-1706">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1707">modelId</span></span> |<span data-ttu-id="a779e-1708">선택적 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="a779e-1708">Optional parameter.</span></span> <span data-ttu-id="a779e-1709">생략한 경우 모든 모델에 대한 모든 알림을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="a779e-1710">유효한 값: 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1710">Valid value: unique identifier of the model.</span></span> |
| <span data-ttu-id="a779e-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1711">apiVersion</span></span> |<span data-ttu-id="a779e-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-1713">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-1713">Request Body</span></span> |<span data-ttu-id="a779e-1714">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-1714">NONE</span></span> |

<span data-ttu-id="a779e-1715">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a779e-1715">**Response:**</span></span>

<span data-ttu-id="a779e-1716">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="a779e-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="a779e-1717">OData XML</span></span>

    The response includes one entry per notification. Each entry has the following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="a779e-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="a779e-1718">14.2.</span></span> <span data-ttu-id="a779e-1719">모델 알림 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-1719">Delete Model Notifications</span></span>
<span data-ttu-id="a779e-1720">모델에 대한 읽은 알림을 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="a779e-1721">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1721">HTTP Method</span></span> | <span data-ttu-id="a779e-1722">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1723">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a779e-1724">예제:</span><span class="sxs-lookup"><span data-stu-id="a779e-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1725">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1725">Parameter Name</span></span> | <span data-ttu-id="a779e-1726">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="a779e-1727">modelId</span></span> |<span data-ttu-id="a779e-1728">모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a779e-1728">Unique identifier of the model</span></span> |
| <span data-ttu-id="a779e-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1729">apiVersion</span></span> |<span data-ttu-id="a779e-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-1731">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-1731">Request Body</span></span> |<span data-ttu-id="a779e-1732">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-1732">NONE</span></span> |

<span data-ttu-id="a779e-1733">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-1733">**Response**:</span></span>

<span data-ttu-id="a779e-1734">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="a779e-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="a779e-1735">14.3.</span></span> <span data-ttu-id="a779e-1736">사용자 알림 삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-1736">Delete User Notifications</span></span>
<span data-ttu-id="a779e-1737">모든 모델에 대한 모든 알림을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="a779e-1738">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a779e-1738">HTTP Method</span></span> | <span data-ttu-id="a779e-1739">URI</span><span class="sxs-lookup"><span data-stu-id="a779e-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1740">삭제</span><span class="sxs-lookup"><span data-stu-id="a779e-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="a779e-1741">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a779e-1741">Parameter Name</span></span> | <span data-ttu-id="a779e-1742">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a779e-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a779e-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a779e-1743">apiVersion</span></span> |<span data-ttu-id="a779e-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="a779e-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="a779e-1745">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a779e-1745">Request Body</span></span> |<span data-ttu-id="a779e-1746">없음</span><span class="sxs-lookup"><span data-stu-id="a779e-1746">NONE</span></span> |

<span data-ttu-id="a779e-1747">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a779e-1747">**Response**:</span></span>

<span data-ttu-id="a779e-1748">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a779e-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="a779e-1749">15. 법적 정보</span><span class="sxs-lookup"><span data-stu-id="a779e-1749">15. Legal</span></span>
<span data-ttu-id="a779e-1750">이 문서는 "있는 그대로" 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="a779e-1751">URL 및 기타 인터넷 웹 사이트 참조를 포함하여 본 문서에 명시된 정보 및 보기는 통지 없이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="a779e-1752">여기에서 설명하는 일부 예는 설명 목적으로만 제공되는 가상의 예이며,</span><span class="sxs-lookup"><span data-stu-id="a779e-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="a779e-1753">어떠한 실제 사례와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="a779e-1754">이 문서는 Microsoft 제품의 지적 소유권에 대한 법적 권한을 사용자에게 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="a779e-1755">이 문서는 내부 참조용으로만 복사 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a779e-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="a779e-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a779e-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="a779e-1757">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="a779e-1757">All rights reserved.</span></span>

