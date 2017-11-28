---
title: "aaaMachine 학습 권장 사항을 API 설명서 | Microsoft Docs"
description: "Hello Microsoft Azure Marketplace에서에서 제공 하는 권장 엔진에 대 한 azure 컴퓨터 학습 권장 사항을 API 설명서입니다."
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
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="a8ea1-103">Azure 기계 학습 권장 사항 API 설명서</span><span class="sxs-lookup"><span data-stu-id="a8ea1-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="a8ea1-104">이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="a8ea1-105">hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="a8ea1-106">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="a8ea1-107">에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="a8ea1-108">이 문서에서는 Microsoft Azure 기계 학습 권장 사항 API에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="a8ea1-109">1. 일반 개요</span><span class="sxs-lookup"><span data-stu-id="a8ea1-109">1. General overview</span></span>
<span data-ttu-id="a8ea1-110">이 문서는 API 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-110">This document is an API reference.</span></span> <span data-ttu-id="a8ea1-111">"Azure 기계 학습 권장-빠른 시작" 문서 hello로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="a8ea1-112">hello Azure 컴퓨터 학습 권장 사항을 API hello 논리 그룹을 다음으로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="a8ea1-113"><ins>제한 사항</ins> - 추천 API 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="a8ea1-114"><ins>일반 정보</ins> - 인증, 서비스 URI 및 버전 관리에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="a8ea1-115"><ins>Basic 모델</ins> -toodo hello 대 한 기본 작업 모델을 사용 하는 Api (예: 만들기, 업데이트 및 삭제는 모델).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="a8ea1-116"><ins>고급 모델링</ins> -hello 모델에 대 한 고급 tooget 데이터 통찰력을 사용 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="a8ea1-117"><ins>모델 비즈니스 규칙</ins> -hello 모델 권장 구성 결과에 toomanage 비즈니스 규칙을 사용 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="a8ea1-118"><ins>카탈로그</ins> -toodo 모델 카탈로그에 대 한 기본 작업을 사용 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="a8ea1-119">카탈로그는 hello 사용 현황 데이터의 hello 항목에 대 한 메타 데이터 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="a8ea1-120"><ins>기능</ins> -hello 카탈로그로 tooget 항목에 대 한 통찰력을 사용 하도록 설정 하는 Api와 방법을 toouse이 정보 toobuild 더 나은 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="a8ea1-121"><ins>사용 현황 데이터</ins> -toodo hello 모델 사용 현황 데이터에 대 한 기본 작업을 사용 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="a8ea1-122">Hello 기본 형태로 사용 현황 데이터의 쌍 &#60; userId &#62; 포함 하는 행으로 이루어진, &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="a8ea1-123"><ins>빌드</ins> -tootrigger 모델을 사용할 수 있는 Api 빌드하고 빌드 관련된 toothis 있는 기본 작업 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="a8ea1-124">유용한 사용 데이터가 있으면 모델 빌드를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="a8ea1-125"><ins>권장 사항</ins> -모델의 hello 빌드가 끝난 후 tooconsume 권장 사항을 수 있는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="a8ea1-126"><ins>사용자 데이터</ins> -hello 사용자 사용 현황 데이터에 toofetch 정보를 사용 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="a8ea1-127"><ins>알림</ins> -Api를 사용 하면 문제에 tooreceive 알림 관련 API tooyour 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="a8ea1-128">(예를 들어 보고 하려는 데이터 취득 및 대부분의 처리 실패 하는 hello 이벤트를 통해 사용 현황 데이터.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="a8ea1-129">오류 알림이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="a8ea1-130">2. 제한 사항</span><span class="sxs-lookup"><span data-stu-id="a8ea1-130">2. Limitations</span></span>
* <span data-ttu-id="a8ea1-131">구독 당 모델의 hello 최대 수는 10입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="a8ea1-132">모델에 대해 빌드의 최대 수 hello은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="a8ea1-133">hello 카탈로그를 보유할 수 있는 항목의 최대 수는 100, 000입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="a8ea1-134">hello 사용 포인트 유지 되는 최대 수에는 ~ 5,000,000는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="a8ea1-135">새로 업로드 되거나 보고 되는 경우 가장 오래 된 hello 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="a8ea1-136">POST (예: 카탈로그 데이터 가져오기 사용 현황 데이터 가져오기)에 보낼 수 있는 데이터의 최대 크기 hello 사항은 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="a8ea1-137">hello 권장 구성을 가져올 때에 대해 질문할 수 있는 항목의 최대 수는 150입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="a8ea1-138">3. API – 일반 정보</span><span class="sxs-lookup"><span data-stu-id="a8ea1-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="a8ea1-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-139">3.1.</span></span> <span data-ttu-id="a8ea1-140">인증</span><span class="sxs-lookup"><span data-stu-id="a8ea1-140">Authentication</span></span>
<span data-ttu-id="a8ea1-141">인증 문제에 관한 hello Microsoft Azure 마켓플레이스 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="a8ea1-142">hello 마켓플레이스 hello Basic 또는 OAuth 인증 방법 중 하나를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="a8ea1-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-143">3.2.</span></span> <span data-ttu-id="a8ea1-144">서비스 URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-144">Service URI</span></span>
<span data-ttu-id="a8ea1-145">hello hello Azure 컴퓨터 학습 권장 사항을 Api에 대 한 서비스 루트 URI는 [여기 합니다.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="a8ea1-146">hello 전체 서비스 URI는 hello OData 사양의 요소를 사용 하 여 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="a8ea1-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-147">3.3.</span></span> <span data-ttu-id="a8ea1-148">API 버전</span><span class="sxs-lookup"><span data-stu-id="a8ea1-148">API version</span></span>
<span data-ttu-id="a8ea1-149">각 API 호출에 hello 끝에 호출 apiVersion too1.0를 설정 해야 하는 쿼리 매개를 변수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="a8ea1-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-150">3.4.</span></span> <span data-ttu-id="a8ea1-151">ID 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="a8ea1-151">IDs are case sensitive</span></span>
<span data-ttu-id="a8ea1-152">Id, hello Api 중 하나에서 반환 된 대/소문자 구분 및 후속 API 호출에 매개 변수로 전달 된 경우 에서처럼 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="a8ea1-153">예를 들어 모델 ID와 카탈로그 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="a8ea1-154">4. 권장 사항 품질 및 콜드 항목</span><span class="sxs-lookup"><span data-stu-id="a8ea1-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="a8ea1-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-155">4.1.</span></span> <span data-ttu-id="a8ea1-156">권장 사항 품질</span><span class="sxs-lookup"><span data-stu-id="a8ea1-156">Recommendation quality</span></span>
<span data-ttu-id="a8ea1-157">추천 모델을 만드는 것이 일반적으로 충분 한 tooallow hello 시스템 tooprovide 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="a8ea1-158">그럼에도 불구 하 고 권장 사항은 정확성이 처리 hello 사용량에 따라 다르며 hello hello 카탈로그의 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="a8ea1-159">예를 들어 hello 시스템 어려움 이러한 항목에 대 한 권장 사항을 제공 하거나 이러한 항목을 사용 하 여 권장 한 최초 항목 (항목 한 사용 하지 않고) 많을 경우 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="a8ea1-160">순서 tooovercome hello 최초 항목 문제가 hello 시스템에는 hello 항목 tooenhance hello 권장 구성의 메타 데이터의 hello 사용할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="a8ea1-161">이 메타 데이터 참조 tooas 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="a8ea1-162">일반적인 기능은 책의 저자 또는 동영상의 배우입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="a8ea1-163">키/값 문자열 hello 형태로 hello 카탈로그를 통해 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="a8ea1-164">Hello hello 카탈로그 파일의 전체 포맷을 toohello를 참조 하십시오 [카탈로그 섹션을 가져올](#81-import-catalog-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="a8ea1-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-165">4.2.</span></span> <span data-ttu-id="a8ea1-166">순위 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-166">Rank build</span></span>
<span data-ttu-id="a8ea1-167">기능 hello 추천 모델을 향상 시킬 수 있지만 toodo 하려면 hello 의미 있는 기능을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="a8ea1-168">이를 위해 순위 빌드라는 새 빌드가 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="a8ea1-169">이 빌드 hello 유용성 기능에 순위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="a8ea1-170">의미 있는 기능은 순위 점수가 2 이상인 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="a8ea1-171">Hello 기능이 있는 의미를 이해 한 후 hello 목록 (또는 하위 목록)의 의미 있는 기능을 사용 하 여 권장 사항 빌드를 트리거하십시오.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="a8ea1-172">것이 가능한 toouse 웜 항목과 최초 항목의 hello 향상 된 기능에 대 한 이러한 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="a8ea1-173">Hello 웜 항목에 대 한 해당 순서 toouse에서 `UseFeatureInModel` 빌드 매개 변수를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="a8ea1-174">최초 항목에 대 한 순서 toouse 기능에서 hello `AllowColdItemPlacement` 빌드 매개 변수를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="a8ea1-175">참고: 것은 가능한 tooenable `AllowColdItemPlacement` 사용 하지 않고 `UseFeatureInModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="a8ea1-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-176">4.3.</span></span> <span data-ttu-id="a8ea1-177">권장 사항 추론</span><span class="sxs-lookup"><span data-stu-id="a8ea1-177">Recommendation reasoning</span></span>
<span data-ttu-id="a8ea1-178">권장 사항 추론은 기능 사용의 또 다른 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="a8ea1-179">실제로, hello Azure 시스템 학습 권장 사항 엔진 צ ְ ײ 기능 tooprovide 권장 사항을 설명 (규칙 하위</span><span class="sxs-lookup"><span data-stu-id="a8ea1-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="a8ea1-180">추론), toomore 신뢰도 hello에 선행 hello 권장 소비자에서 항목을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="a8ea1-181">tooenable 추론을 hello `AllowFeatureCorrelation` 및 `ReasoningFeatureList` 매개 변수는 설치 이전 toorequesting 권장 빌드 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="a8ea1-182">5. 모델 기본</span><span class="sxs-lookup"><span data-stu-id="a8ea1-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="a8ea1-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-183">5.1.</span></span> <span data-ttu-id="a8ea1-184">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-184">Create Model</span></span>
<span data-ttu-id="a8ea1-185">"모델 만들기" 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="a8ea1-186">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-186">HTTP Method</span></span> | <span data-ttu-id="a8ea1-187">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-188">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-189">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-190">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-190">Parameter Name</span></span> | <span data-ttu-id="a8ea1-191">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-192">modelName</span><span class="sxs-lookup"><span data-stu-id="a8ea1-192">modelName</span></span> |<span data-ttu-id="a8ea1-193">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a8ea1-194">최대 길이: 20</span><span class="sxs-lookup"><span data-stu-id="a8ea1-194">Max length: 20</span></span> |
| <span data-ttu-id="a8ea1-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-195">apiVersion</span></span> |<span data-ttu-id="a8ea1-196">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-196">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-197">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-197">Request Body</span></span> |<span data-ttu-id="a8ea1-198">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-198">NONE</span></span> |

<span data-ttu-id="a8ea1-199">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-199">**Response**:</span></span>

<span data-ttu-id="a8ea1-200">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="a8ea1-201">`feed/entry/content/properties/id`--Hello 모델 ID를 포함 하는 중</span><span class="sxs-lookup"><span data-stu-id="a8ea1-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="a8ea1-202">**참고**: 모델 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="a8ea1-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-203">OData XML</span></span>

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

### <a name="52-get-model"></a><span data-ttu-id="a8ea1-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-204">5.2.</span></span> <span data-ttu-id="a8ea1-205">모델 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-205">Get Model</span></span>
<span data-ttu-id="a8ea1-206">"모델 가져오기" 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="a8ea1-207">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-207">HTTP Method</span></span> | <span data-ttu-id="a8ea1-208">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-209">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-210">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-211">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-211">Parameter Name</span></span> | <span data-ttu-id="a8ea1-212">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-213">id</span><span class="sxs-lookup"><span data-stu-id="a8ea1-213">id</span></span> |<span data-ttu-id="a8ea1-214">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="a8ea1-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-215">apiVersion</span></span> |<span data-ttu-id="a8ea1-216">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-216">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-217">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-217">Request Body</span></span> |<span data-ttu-id="a8ea1-218">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-218">NONE</span></span> |

<span data-ttu-id="a8ea1-219">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-219">**Response**:</span></span>

<span data-ttu-id="a8ea1-220">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-220">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-221">요소 다음 hello에서 hello 모델 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="a8ea1-222">`feed/entry/content/properties/Id` – 모델의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="a8ea1-223">`feed/entry/content/properties/Name` – 모델 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="a8ea1-224">`feed/entry/content/properties/Date` - 모델을 만든 날짜</span><span class="sxs-lookup"><span data-stu-id="a8ea1-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="a8ea1-225">`feed/entry/content/properties/Status` – 모델 상태</span><span class="sxs-lookup"><span data-stu-id="a8ea1-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="a8ea1-226">Hello 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-226">One of hello following:</span></span>
  * <span data-ttu-id="a8ea1-227">Created - 모델이 생성되었으며 카탈로그 및 사용 현황을 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="a8ea1-228">ReadyForBuild – 모델이 생성되었으며 카탈로그 및 사용 현황을 포함함</span><span class="sxs-lookup"><span data-stu-id="a8ea1-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="a8ea1-229">`feed/entry/content/properties/HasActiveBuild`-Hello 모델이 성공적으로 빌드된 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="a8ea1-230">`feed/entry/content/properties/BuildId` – 모델 활성 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="a8ea1-231">`feed/entry/content/properties/Mpr` – 모델 평균 백분위수 순위(MPR - 자세한 내용은 ModelInsight 참조)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="a8ea1-232">`feed/entry/content/properties/UserName` – 모델 내부 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="a8ea1-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-233">OData XML</span></span>

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

### <a name="53----get-all-models"></a><span data-ttu-id="a8ea1-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-234">5.3.</span></span>    <span data-ttu-id="a8ea1-235">모든 모델 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-235">Get All Models</span></span>
<span data-ttu-id="a8ea1-236">Hello 현재 사용자의 모든 모델을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="a8ea1-237">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-237">HTTP Method</span></span> | <span data-ttu-id="a8ea1-238">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-239">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-240">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-241">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-241">Parameter Name</span></span> | <span data-ttu-id="a8ea1-242">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-243">apiVersion</span></span> |<span data-ttu-id="a8ea1-244">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-244">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-245">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-245">Request Body</span></span> |<span data-ttu-id="a8ea1-246">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-246">NONE</span></span> |

<span data-ttu-id="a8ea1-247">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-247">**Response**:</span></span>

<span data-ttu-id="a8ea1-248">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="a8ea1-249">`feed/entry/content/properties/Id` – 모델의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="a8ea1-250">`feed/entry/content/properties/Name` – 모델 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="a8ea1-251">`feed/entry/content/properties/Date` - 모델을 만든 날짜</span><span class="sxs-lookup"><span data-stu-id="a8ea1-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="a8ea1-252">`feed/entry/content/properties/Status` – 모델 상태</span><span class="sxs-lookup"><span data-stu-id="a8ea1-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="a8ea1-253">Hello 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-253">One of hello following:</span></span>
  * <span data-ttu-id="a8ea1-254">Created - 모델이 생성되었으며 카탈로그 및 사용 현황을 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="a8ea1-255">ReadyForBuild – 모델이 생성되었으며 카탈로그 및 사용 현황을 포함함</span><span class="sxs-lookup"><span data-stu-id="a8ea1-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="a8ea1-256">`feed/entry/content/properties/HasActiveBuild`-Hello 모델이 성공적으로 빌드된 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="a8ea1-257">`feed/entry/content/properties/BuildId` – 모델 활성 빌드 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="a8ea1-258">`feed/entry/content/properties/Mpr` – 모델 MPR(자세한 내용은 ModelInsight 참조)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="a8ea1-259">`feed/entry/content/properties/UserName` – 모델 내부 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="a8ea1-260">`feed/entry/content/properties/UsageFileNames` – 쉼표로 구분된 모델 사용 파일 목록</span><span class="sxs-lookup"><span data-stu-id="a8ea1-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="a8ea1-261">`feed/entry/content/properties/CatalogId` – 모델 카탈로그 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="a8ea1-262">`feed/entry/content/properties/Description` – 모델 설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="a8ea1-263">`feed/entry/content/properties/CatalogFileName` – 모델 카탈로그 파일 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="a8ea1-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-264">OData XML</span></span>

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

### <a name="54----update-model"></a><span data-ttu-id="a8ea1-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-265">5.4.</span></span>    <span data-ttu-id="a8ea1-266">모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="a8ea1-266">Update Model</span></span>
<span data-ttu-id="a8ea1-267">Hello 모델 설명을 업데이트 하거나 hello 활성 빌드 id입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="a8ea1-268">
<ins>활성 빌드 ID</ins> – 모든 모델에 대한 모든 빌드에는 빌드 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="a8ea1-269">hello 활성 빌드 ID는 모든 새 모델의 첫 번째 성공한 빌드의 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="a8ea1-270">활성 빌드 ID 있고 hello에 대 한 추가 빌드 작업을 수행한 후 동일한 모델을 해야 tooexplicitly가 hello 기본 빌드 ID 하려면으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="a8ea1-271">사용 하면 권장 사항, toouse, 하나의 자동으로 사용 됩니다 하는 hello 기본 원하는 hello 빌드 ID를 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="a8ea1-272">이 메커니즘을 사용 하면 추천 모델이 프로덕션-toobuild 새 모델에에서 있는 하 고 테스트 하 여 이러한 수준을 올리기 전에 tooproduction-있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="a8ea1-273">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-273">HTTP Method</span></span> | <span data-ttu-id="a8ea1-274">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-275">PUT</span><span class="sxs-lookup"><span data-stu-id="a8ea1-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-276">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-277">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-277">Parameter Name</span></span> | <span data-ttu-id="a8ea1-278">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-279">id</span><span class="sxs-lookup"><span data-stu-id="a8ea1-279">id</span></span> |<span data-ttu-id="a8ea1-280">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="a8ea1-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-281">apiVersion</span></span> |<span data-ttu-id="a8ea1-282">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-282">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-283">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="a8ea1-284">참고 설명과 ActiveBuildId 해당 hello XML 태그는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="a8ea1-285">설명 또는 ActiveBuildId tooset 하지 않으려면 hello 전체 태그를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="a8ea1-286">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-286">**Response**:</span></span>

<span data-ttu-id="a8ea1-287">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="a8ea1-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-288">5.5.</span></span>    <span data-ttu-id="a8ea1-289">모델 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-289">Delete Model</span></span>
<span data-ttu-id="a8ea1-290">ID별로 기존 모델을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="a8ea1-291">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-291">HTTP Method</span></span> | <span data-ttu-id="a8ea1-292">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-293">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-294">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-295">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-295">Parameter Name</span></span> | <span data-ttu-id="a8ea1-296">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-297">id</span><span class="sxs-lookup"><span data-stu-id="a8ea1-297">id</span></span> |<span data-ttu-id="a8ea1-298">(대/소문자 구분) hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="a8ea1-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-299">apiVersion</span></span> |<span data-ttu-id="a8ea1-300">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-300">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-301">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-301">Request Body</span></span> |<span data-ttu-id="a8ea1-302">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-302">NONE</span></span> |

<span data-ttu-id="a8ea1-303">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-303">**Response**:</span></span>

<span data-ttu-id="a8ea1-304">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-304">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-305">OData XML</span></span>

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

## <a name="6-model-advanced"></a><span data-ttu-id="a8ea1-306">6. 모델 고급</span><span class="sxs-lookup"><span data-stu-id="a8ea1-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="a8ea1-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-307">6.1.</span></span>    <span data-ttu-id="a8ea1-308">모델 데이터 정보</span><span class="sxs-lookup"><span data-stu-id="a8ea1-308">Model Data Insight</span></span>
<span data-ttu-id="a8ea1-309">이 모델 빌드된 hello 사용 현황 데이터에 통계 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="a8ea1-310">권장 사항 빌드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="a8ea1-311">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-311">HTTP Method</span></span> | <span data-ttu-id="a8ea1-312">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-313">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-314">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-315">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-315">Parameter Name</span></span> | <span data-ttu-id="a8ea1-316">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-317">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-317">modelId</span></span> |<span data-ttu-id="a8ea1-318">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-319">apiVersion</span></span> |<span data-ttu-id="a8ea1-320">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-320">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-321">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-321">Request Body</span></span> |<span data-ttu-id="a8ea1-322">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-322">NONE</span></span> |

<span data-ttu-id="a8ea1-323">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-323">**Response**:</span></span>

<span data-ttu-id="a8ea1-324">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-324">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-325">hello 데이터 속성의 컬렉션으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="a8ea1-326">`feed/entry/id/content/properties/key`-Hello 속성 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="a8ea1-327">`feed/entry/id/content/properties/value`-Hello 속성 값을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="a8ea1-328">hello 다음 표에서 각 키를 나타내는 hello 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="a8ea1-329">키</span><span class="sxs-lookup"><span data-stu-id="a8ea1-329">Key</span></span> | <span data-ttu-id="a8ea1-330">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="a8ea1-331">AvgItemLength</span></span> |<span data-ttu-id="a8ea1-332">항목당 평균 고유 사용자 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="a8ea1-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="a8ea1-333">AvgUserLength</span></span> |<span data-ttu-id="a8ea1-334">사용자당 평균 고유 항목 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="a8ea1-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a8ea1-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="a8ea1-336">모델링할 수 없는 항목을 정리한 후의 항목 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="a8ea1-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a8ea1-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="a8ea1-338">모델링할 수 없는 사용자 및 항목을 정리한 후의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="a8ea1-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a8ea1-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="a8ea1-340">모델링할 수 없는 사용자 및 항목을 정리한 후의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="a8ea1-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="a8ea1-341">MaxItemLength</span></span> |<span data-ttu-id="a8ea1-342">Hello 가장 인기 있는 항목에 대 한 고유 사용자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="a8ea1-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="a8ea1-343">MaxUserLength</span></span> |<span data-ttu-id="a8ea1-344">사용자의 최대 고유 항목 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="a8ea1-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="a8ea1-345">MinItemLength</span></span> |<span data-ttu-id="a8ea1-346">항목의 최대 고유 사용자 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="a8ea1-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="a8ea1-347">MinUserLength</span></span> |<span data-ttu-id="a8ea1-348">사용자의 최소 고유 항목 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="a8ea1-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a8ea1-349">RawNumberOfItems</span></span> |<span data-ttu-id="a8ea1-350">Hello 사용 파일의 항목 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="a8ea1-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a8ea1-351">RawNumberOfUsers</span></span> |<span data-ttu-id="a8ea1-352">정리하기 전의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="a8ea1-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a8ea1-353">RawNumberOfRecords</span></span> |<span data-ttu-id="a8ea1-354">정리하기 전의 사용 포인트 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="a8ea1-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a8ea1-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="a8ea1-356">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-356">N/A</span></span> |
| <span data-ttu-id="a8ea1-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a8ea1-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="a8ea1-358">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-358">N/A</span></span> |
| <span data-ttu-id="a8ea1-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a8ea1-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="a8ea1-360">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-360">N/A</span></span> |

<span data-ttu-id="a8ea1-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-361">OData XML</span></span>

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

### <a name="62----model-insight"></a><span data-ttu-id="a8ea1-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-362">6.2.</span></span>    <span data-ttu-id="a8ea1-363">모델 정보</span><span class="sxs-lookup"><span data-stu-id="a8ea1-363">Model Insight</span></span>
<span data-ttu-id="a8ea1-364">Hello 현재 빌드에 대 한 정보를 모델링 하는 반환 (제공 된 경우) 또는 특정 빌드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="a8ea1-365">권장 사항 빌드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="a8ea1-366">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-366">HTTP Method</span></span> | <span data-ttu-id="a8ea1-367">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-368">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-368">GET</span></span> |<span data-ttu-id="a8ea1-369">활성 빌드 ID 사용:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-370">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-371">특정 빌드 ID 사용:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-372">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-372">Parameter Name</span></span> | <span data-ttu-id="a8ea1-373">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-374">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-374">modelId</span></span> |<span data-ttu-id="a8ea1-375">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-376">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-376">buildId</span></span> |<span data-ttu-id="a8ea1-377">(선택 사항) - 성공적인 빌드를 식별하는 번호</span><span class="sxs-lookup"><span data-stu-id="a8ea1-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="a8ea1-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-378">apiVersion</span></span> |<span data-ttu-id="a8ea1-379">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-379">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-380">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-380">Request Body</span></span> |<span data-ttu-id="a8ea1-381">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-381">NONE</span></span> |

<span data-ttu-id="a8ea1-382">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-382">**Response**:</span></span>

<span data-ttu-id="a8ea1-383">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-383">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-384">hello 데이터 속성의 컬렉션으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="a8ea1-385">hello 다음 표에서 각 키를 나타내는 hello 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="a8ea1-386">키</span><span class="sxs-lookup"><span data-stu-id="a8ea1-386">Key</span></span> | <span data-ttu-id="a8ea1-387">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="a8ea1-388">CatalogCoverage</span></span> |<span data-ttu-id="a8ea1-389">어떤 부분이 hello 카탈로그의 사용 패턴 모델이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="a8ea1-390">hello rest hello 항목의 콘텐츠 기반 기능 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="a8ea1-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="a8ea1-391">Mpr</span></span> |<span data-ttu-id="a8ea1-392">Hello 모델의 백분위 수 순위를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="a8ea1-393">낮을수록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-393">Lower is better.</span></span> |
| <span data-ttu-id="a8ea1-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="a8ea1-394">NumberOfDimensions</span></span> |<span data-ttu-id="a8ea1-395">Hello 행렬 factorization 알고리즘에서 사용 하는 차원 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="a8ea1-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-396">OData XML</span></span>

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

### <a name="63----get-model-sample"></a><span data-ttu-id="a8ea1-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-397">6.3.</span></span>    <span data-ttu-id="a8ea1-398">모델 샘플 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-398">Get Model Sample</span></span>
<span data-ttu-id="a8ea1-399">Hello 추천 모델의 샘플을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="a8ea1-400">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-400">HTTP Method</span></span> | <span data-ttu-id="a8ea1-401">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-402">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-403">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-404">특정 빌드 ID 사용:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-405">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-406">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-406">Parameter Name</span></span> | <span data-ttu-id="a8ea1-407">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-408">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-408">modelId</span></span> |<span data-ttu-id="a8ea1-409">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-410">apiVersion</span></span> |<span data-ttu-id="a8ea1-411">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-411">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-412">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-412">Request Body</span></span> |<span data-ttu-id="a8ea1-413">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-413">NONE</span></span> |

<span data-ttu-id="a8ea1-414">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-414">**Response**:</span></span>

<span data-ttu-id="a8ea1-415">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-415">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-416">OData XML</span></span>

<span data-ttu-id="a8ea1-417">원시 텍스트 형식으로 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-417">Response is returned in raw text format:</span></span>

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
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="a8ea1-418">7. 모델 비즈니스 규칙</span><span class="sxs-lookup"><span data-stu-id="a8ea1-418">7. Model Business Rules</span></span>
<span data-ttu-id="a8ea1-419">다음은 지원 되는 규칙의 hello 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="a8ea1-420"><strong>차단 목록</strong> -차단 목록 사용 하면 tooprovide hello 권장 구성 결과에서 tooreturn 하지 않을 항목의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="a8ea1-421"><strong>FeatureBlockList</strong> -차단 목록 기능을 사용 하면 있습니다 tooblock 항목 기능 hello 값을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="a8ea1-422">*단일 차단 목록 규칙에 1000개보다 많은 항목을 전송하지 마세요. 호출 시간 제한에 도달할 수 있습니다. 1000 개 이상의 항목 tooblock 해야 할 경우에 여러 개의 차단 목록 호출을 만들 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="a8ea1-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="a8ea1-423"><strong>Upsale</strong> -Upsale hello 권장 구성 결과에서 tooenforce 항목 tooreturn을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="a8ea1-424"><strong>화이트 리스트</strong> -tooonly 있습니다 항목의 목록에서 권장 사항을 제안 허용 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="a8ea1-425"><strong>FeatureWhiteList</strong> -기능 허용 목록을 사용 하면 특정 기능 값을 가진 tooonly 권장 되는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="a8ea1-426"><strong>PerSeedBlockList</strong> -당 시드 차단 목록 당 tooprovide 권장 결과로 반환할 수 없는 항목의 목록 항목을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="a8ea1-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-427">7.1.</span></span>    <span data-ttu-id="a8ea1-428">모델 규칙 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-428">Get Model Rules</span></span>
| <span data-ttu-id="a8ea1-429">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-429">HTTP Method</span></span> | <span data-ttu-id="a8ea1-430">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-431">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a8ea1-432">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-433">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-433">Parameter Name</span></span> | <span data-ttu-id="a8ea1-434">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-435">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-435">modelId</span></span> |<span data-ttu-id="a8ea1-436">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-437">apiVersion</span></span> |<span data-ttu-id="a8ea1-438">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-438">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-439">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-439">Request Body</span></span> |<span data-ttu-id="a8ea1-440">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-440">NONE</span></span> |

<span data-ttu-id="a8ea1-441">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-441">**Response**:</span></span>

<span data-ttu-id="a8ea1-442">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="a8ea1-443">`feed/entry/content/properties/Id` – 이 규칙의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="a8ea1-444">`feed/entry/content/properties/Type`Hello 규칙의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="a8ea1-445">`feed/entry/content/properties/Parameter` – 규칙 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="a8ea1-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-446">OData XML</span></span>

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

### <a name="72----add-rule"></a><span data-ttu-id="a8ea1-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-447">7.2.</span></span>    <span data-ttu-id="a8ea1-448">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="a8ea1-448">Add Rule</span></span>
| <span data-ttu-id="a8ea1-449">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-449">HTTP Method</span></span> | <span data-ttu-id="a8ea1-450">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-451">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="a8ea1-452">HEADER</span><span class="sxs-lookup"><span data-stu-id="a8ea1-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a8ea1-453">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-453">Parameter Name</span></span> | <span data-ttu-id="a8ea1-454">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-455">apiVersion</span></span> |<span data-ttu-id="a8ea1-456">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-456">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-457">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-457">Request Body</span></span> | |

<span data-ttu-id="a8ea1-458"><ins>비즈니스 규칙에 대 한 항목 Id를 제공 될 때마다 toouse hello hello 항목의 외부 Id가 있는지 확인 하십시오 (hello hello 카탈로그 파일에 사용 되는 동일한 Id)</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="a8ea1-459">
<ins>tooadd 차단 목록 규칙:</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a8ea1-460"><ins>
<ins>tooadd FeatureBlockList 규칙:</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a8ea1-461"><ins>tooadd Upsale 규칙:</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="a8ea1-462">
<ins>tooadd 허용 목록 규칙:</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a8ea1-463"><ins>
<ins>tooadd FeatureWhiteList 규칙:</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a8ea1-464"><ins>tooadd PerSeedBlockList 규칙:</ins></span><span class="sxs-lookup"><span data-stu-id="a8ea1-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="a8ea1-465">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-465">**Response**:</span></span>

<span data-ttu-id="a8ea1-466">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-466">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-467">hello API의 세부 정보와 함께 규칙을 새로 만든 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="a8ea1-468">경로 따라 hello에서 hello 규칙 속성을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="a8ea1-469">`feed/entry/content/properties/Id` – 이 규칙의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="a8ea1-470">`feed/entry/content/properties/Type`-Hello 규칙의 유형을: Upsale 또는 차단 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="a8ea1-471">`feed/entry/content/properties/Parameter` – 규칙 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="a8ea1-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-472">OData XML</span></span>

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

### <a name="73----delete-rule"></a><span data-ttu-id="a8ea1-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-473">7.3.</span></span>    <span data-ttu-id="a8ea1-474">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-474">Delete Rule</span></span>
| <span data-ttu-id="a8ea1-475">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-475">HTTP Method</span></span> | <span data-ttu-id="a8ea1-476">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-477">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-478">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-479">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-479">Parameter Name</span></span> | <span data-ttu-id="a8ea1-480">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-481">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-481">modelId</span></span> |<span data-ttu-id="a8ea1-482">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-483">filterId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-483">filterId</span></span> |<span data-ttu-id="a8ea1-484">Hello 필터의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="a8ea1-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-485">apiVersion</span></span> |<span data-ttu-id="a8ea1-486">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-486">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-487">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-487">Request Body</span></span> |<span data-ttu-id="a8ea1-488">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-488">NONE</span></span> |

<span data-ttu-id="a8ea1-489">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-489">**Response**:</span></span>

<span data-ttu-id="a8ea1-490">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="a8ea1-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-491">7.4.</span></span>    <span data-ttu-id="a8ea1-492">모든 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-492">Delete All Rules</span></span>
| <span data-ttu-id="a8ea1-493">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-493">HTTP Method</span></span> | <span data-ttu-id="a8ea1-494">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-495">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-496">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-497">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-497">Parameter Name</span></span> | <span data-ttu-id="a8ea1-498">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-499">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-499">modelId</span></span> |<span data-ttu-id="a8ea1-500">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-501">apiVersion</span></span> |<span data-ttu-id="a8ea1-502">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-502">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-503">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-503">Request Body</span></span> |<span data-ttu-id="a8ea1-504">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-504">NONE</span></span> |

<span data-ttu-id="a8ea1-505">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-505">**Response**:</span></span>

<span data-ttu-id="a8ea1-506">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="a8ea1-507">8. 카탈로그</span><span class="sxs-lookup"><span data-stu-id="a8ea1-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="a8ea1-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-508">8.1.</span></span>    <span data-ttu-id="a8ea1-509">카탈로그 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-509">Import Catalog Data</span></span>
<span data-ttu-id="a8ea1-510">여러 가지 카탈로그 파일 toohello 모델 동일한 여러 호출으로 업로드 하는 경우만 hello 새 카탈로그 항목 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="a8ea1-511">기존 항목 hello 원래 값으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="a8ea1-512">이 메서드를 사용하여 카탈로그 데이터를 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="a8ea1-513">hello 카탈로그 데이터 형식에 따라 hello를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="a8ea1-514">기능 사용 안 함 - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="a8ea1-515">기능 사용 - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="a8ea1-516">참고: hello 최대 파일 크기 사항은 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="a8ea1-517">** 형식 세부 정보 **</span><span class="sxs-lookup"><span data-stu-id="a8ea1-517">** Format details **</span></span>

| <span data-ttu-id="a8ea1-518">이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-518">Name</span></span> | <span data-ttu-id="a8ea1-519">필수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-519">Mandatory</span></span> | <span data-ttu-id="a8ea1-520">형식</span><span class="sxs-lookup"><span data-stu-id="a8ea1-520">Type</span></span> | <span data-ttu-id="a8ea1-521">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a8ea1-522">항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-522">Item Id</span></span> |<span data-ttu-id="a8ea1-523">예</span><span class="sxs-lookup"><span data-stu-id="a8ea1-523">Yes</span></span> |<span data-ttu-id="a8ea1-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="a8ea1-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a8ea1-525">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-525">Max length: 50</span></span> |<span data-ttu-id="a8ea1-526">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="a8ea1-527">Item Name</span><span class="sxs-lookup"><span data-stu-id="a8ea1-527">Item Name</span></span> |<span data-ttu-id="a8ea1-528">예</span><span class="sxs-lookup"><span data-stu-id="a8ea1-528">Yes</span></span> |<span data-ttu-id="a8ea1-529">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="a8ea1-530">최대 길이: 255</span><span class="sxs-lookup"><span data-stu-id="a8ea1-530">Max length: 255</span></span> |<span data-ttu-id="a8ea1-531">항목 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-531">Item name.</span></span> |
| <span data-ttu-id="a8ea1-532">Item Category</span><span class="sxs-lookup"><span data-stu-id="a8ea1-532">Item Category</span></span> |<span data-ttu-id="a8ea1-533">예</span><span class="sxs-lookup"><span data-stu-id="a8ea1-533">Yes</span></span> |<span data-ttu-id="a8ea1-534">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a8ea1-535">최대 길이: 255</span><span class="sxs-lookup"><span data-stu-id="a8ea1-535">Max length: 255</span></span> |<span data-ttu-id="a8ea1-536">범주 toowhich이이 항목이 속하는 (예: 요리 책, 드라마...); 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="a8ea1-537">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-537">Description</span></span> |<span data-ttu-id="a8ea1-538">아니요, 기능이 없는 경우(그러나 비어 있을 수 있음)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="a8ea1-539">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a8ea1-540">최대 길이: 4000</span><span class="sxs-lookup"><span data-stu-id="a8ea1-540">Max length: 4000</span></span> |<span data-ttu-id="a8ea1-541">이 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-541">Description of this item.</span></span> |
| <span data-ttu-id="a8ea1-542">Features list</span><span class="sxs-lookup"><span data-stu-id="a8ea1-542">Features list</span></span> |<span data-ttu-id="a8ea1-543">아니요</span><span class="sxs-lookup"><span data-stu-id="a8ea1-543">No</span></span> |<span data-ttu-id="a8ea1-544">영숫자 문자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a8ea1-545">최대 길이: 4000; 최대 기능 수: 20</span><span class="sxs-lookup"><span data-stu-id="a8ea1-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="a8ea1-546">기능 이름 쉼표로 구분 된 목록을 사용 하는 tooenhance 모델 권장; 일 수 있는 기능 값 = 참조 [고급 항목](#2-advanced-topics) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="a8ea1-547">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-547">HTTP Method</span></span> | <span data-ttu-id="a8ea1-548">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-549">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-550">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a8ea1-551">HEADER</span><span class="sxs-lookup"><span data-stu-id="a8ea1-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a8ea1-552">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-552">Parameter Name</span></span> | <span data-ttu-id="a8ea1-553">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-554">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-554">modelId</span></span> |<span data-ttu-id="a8ea1-555">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-556">filename</span><span class="sxs-lookup"><span data-stu-id="a8ea1-556">filename</span></span> |<span data-ttu-id="a8ea1-557">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="a8ea1-558">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a8ea1-559">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-559">Max length: 50</span></span> |
| <span data-ttu-id="a8ea1-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-560">apiVersion</span></span> |<span data-ttu-id="a8ea1-561">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-561">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-562">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-562">Request Body</span></span> |<span data-ttu-id="a8ea1-563">예(기능 사용):</span><span class="sxs-lookup"><span data-stu-id="a8ea1-563">Example (with features):</span></span><br/><span data-ttu-id="a8ea1-564">2406e770-769 c-4189-89de-1c9283f93a96, 클라라 Callan, 책, hello 책 설명 작성 Richard Wright = 게시자 Harper 홍학 캐나다 = 연도 2001 =</span><span class="sxs-lookup"><span data-stu-id="a8ea1-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="a8ea1-565">21bf8088-b6c0-4509-870 c-e1c7ac78304a, hello Forgetting 룸: A 소설 (비잔티움 책), 책, 작성 Nick Bantock = 게시자 = Harpercollins, 연도 1997 =</span><span class="sxs-lookup"><span data-stu-id="a8ea1-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="a8ea1-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,책,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="a8ea1-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="a8ea1-567">552a1940-21e4-4399-82bb-594b46d7ed54, 짐승 지지대, 책, hello 책 설명 작성 Magnus 충당 = 게시자 = 아케이드 게시 연도 1998 =</span><span class="sxs-lookup"><span data-stu-id="a8ea1-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="a8ea1-568">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-568">**Response**:</span></span>

<span data-ttu-id="a8ea1-569">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-569">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-570">hello API hello 가져오기에 대 한 보고서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="a8ea1-571">`feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="a8ea1-572">`feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="a8ea1-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-573">OData XML</span></span>

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

### <a name="82----get-catalog"></a><span data-ttu-id="a8ea1-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-574">8.2.</span></span>    <span data-ttu-id="a8ea1-575">카탈로그 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-575">Get Catalog</span></span>
<span data-ttu-id="a8ea1-576">모든 카탈로그 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="a8ea1-577">hello 카탈로그 됩니다 한 번에 한 페이지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="a8ea1-578">특정 인덱스에서 tooget 항목을 하려는 경우에 hello $skip odata 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="a8ea1-579">예를 들어 tooget 항목 100 위치에서 시작 하려는 경우 추가 hello 매개 변수 $skip = 100 toohello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="a8ea1-580">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-580">HTTP Method</span></span> | <span data-ttu-id="a8ea1-581">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-582">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-583">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-584">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-584">Parameter Name</span></span> | <span data-ttu-id="a8ea1-585">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-586">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-586">modelId</span></span> |<span data-ttu-id="a8ea1-587">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-588">apiVersion</span></span> |<span data-ttu-id="a8ea1-589">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-589">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-590">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-590">Request Body</span></span> |<span data-ttu-id="a8ea1-591">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-591">NONE</span></span> |

<span data-ttu-id="a8ea1-592">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-592">**Response**:</span></span>

<span data-ttu-id="a8ea1-593">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-593">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-594">hello 응답에는 카탈로그 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="a8ea1-595">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-596">`feed/entry/content/properties/ExternalId`-항목 외부 ID를 카탈로그, hello hello 고객에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="a8ea1-597">`feed/entry/content/properties/InternalId`카탈로그 항목 내부 ID hello Azure 시스템 학습 권장 사항이 생성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="a8ea1-598">`feed/entry/content/properties/Name` – 카탈로그 항목 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="a8ea1-599">`feed/entry/content/properties/Category` – 카탈로그 항목 범주</span><span class="sxs-lookup"><span data-stu-id="a8ea1-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="a8ea1-600">`feed/entry/content/properties/Description` – 카탈로그 항목 설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="a8ea1-601">`feed/entry/content/properties/Metadata` – 카탈로그 항목 메타데이터</span><span class="sxs-lookup"><span data-stu-id="a8ea1-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="a8ea1-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-602">OData XML</span></span>

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
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="a8ea1-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-603">8.3.</span></span>    <span data-ttu-id="a8ea1-604">토큰별 카탈로그 항목 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="a8ea1-605">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-605">HTTP Method</span></span> | <span data-ttu-id="a8ea1-606">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-607">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-608">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-609">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-609">Parameter Name</span></span> | <span data-ttu-id="a8ea1-610">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-611">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-611">modelId</span></span> |<span data-ttu-id="a8ea1-612">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-613">token</span><span class="sxs-lookup"><span data-stu-id="a8ea1-613">token</span></span> |<span data-ttu-id="a8ea1-614">토큰 hello 카탈로그 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="a8ea1-615">3자 이상 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="a8ea1-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-616">apiVersion</span></span> |<span data-ttu-id="a8ea1-617">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-617">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-618">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-618">Request Body</span></span> |<span data-ttu-id="a8ea1-619">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-619">NONE</span></span> |

<span data-ttu-id="a8ea1-620">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-620">**Response**:</span></span>

<span data-ttu-id="a8ea1-621">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-621">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-622">hello 응답에는 카탈로그 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="a8ea1-623">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-624">`feed/entry/content/properties/InternalId`카탈로그 항목 내부 ID hello Azure 시스템 학습 권장 사항이 생성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="a8ea1-625">`feed/entry/content/properties/Name` – 카탈로그 항목 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="a8ea1-626">`feed/entry/content/properties/Rating` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="a8ea1-627">`feed/entry/content/properties/Reasoning` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="a8ea1-628">`feed/entry/content/properties/Metadata` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="a8ea1-629">`feed/entry/content/properties/FormattedRating` - (나중에 사용)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="a8ea1-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-630">OData XML</span></span>

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

## <a name="9-usage-data"></a><span data-ttu-id="a8ea1-631">9. 사용 데이터</span><span class="sxs-lookup"><span data-stu-id="a8ea1-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="a8ea1-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-632">9.1.</span></span>    <span data-ttu-id="a8ea1-633">사용 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="a8ea1-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-634">9.1.1.</span></span> <span data-ttu-id="a8ea1-635">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-635">Uploading File</span></span>
<span data-ttu-id="a8ea1-636">이 섹션에서는 어떻게 tooupload 사용 현황 데이터 파일을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="a8ea1-637">사용 데이터를 사용하여 이 API를 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="a8ea1-638">모든 호출에 대한 모든 사용 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="a8ea1-639">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-639">HTTP Method</span></span> | <span data-ttu-id="a8ea1-640">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-641">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-642">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-643">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-643">Parameter Name</span></span> | <span data-ttu-id="a8ea1-644">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-645">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-645">modelId</span></span> |<span data-ttu-id="a8ea1-646">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-647">filename</span><span class="sxs-lookup"><span data-stu-id="a8ea1-647">filename</span></span> |<span data-ttu-id="a8ea1-648">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="a8ea1-649">문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a8ea1-650">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-650">Max length: 50</span></span> |
| <span data-ttu-id="a8ea1-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-651">apiVersion</span></span> |<span data-ttu-id="a8ea1-652">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-652">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-653">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-653">Request Body</span></span> |<span data-ttu-id="a8ea1-654">사용 데이터.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-654">Usage data.</span></span> <span data-ttu-id="a8ea1-655">형식:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="a8ea1-656">Name</span><span class="sxs-lookup"><span data-stu-id="a8ea1-656">Name</span></span></th><th><span data-ttu-id="a8ea1-657">필수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-657">Mandatory</span></span></th><th><span data-ttu-id="a8ea1-658">형식</span><span class="sxs-lookup"><span data-stu-id="a8ea1-658">Type</span></span></th><th><span data-ttu-id="a8ea1-659">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-659">Description</span></span></th></tr><tr><td><span data-ttu-id="a8ea1-660">User Id</span><span class="sxs-lookup"><span data-stu-id="a8ea1-660">User Id</span></span></td><td><span data-ttu-id="a8ea1-661">예</span><span class="sxs-lookup"><span data-stu-id="a8ea1-661">Yes</span></span></td><td><span data-ttu-id="a8ea1-662">[A-z], [a-z], [0-9], [_] &#40;밑줄&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="a8ea1-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a8ea1-663">최대 길이: 255</span><span class="sxs-lookup"><span data-stu-id="a8ea1-663">Max length: 255</span></span> </td><td><span data-ttu-id="a8ea1-664">사용자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="a8ea1-665">항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-665">Item Id</span></span></td><td><span data-ttu-id="a8ea1-666">예</span><span class="sxs-lookup"><span data-stu-id="a8ea1-666">Yes</span></span></td><td><span data-ttu-id="a8ea1-667">[A-z], [a-z], [0-9], [&#95;] &#40;밑줄&#41;, [-] &#40;대시&#41;</span><span class="sxs-lookup"><span data-stu-id="a8ea1-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a8ea1-668">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-668">Max length: 50</span></span></td><td><span data-ttu-id="a8ea1-669">항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="a8ea1-670">Time</span><span class="sxs-lookup"><span data-stu-id="a8ea1-670">Time</span></span></td><td><span data-ttu-id="a8ea1-671">아니요</span><span class="sxs-lookup"><span data-stu-id="a8ea1-671">No</span></span></td><td><span data-ttu-id="a8ea1-672">날짜(형식): YYYY/MM/DDTHH:MM:SS(예: 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="a8ea1-673">데이터의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="a8ea1-674">이벤트</span><span class="sxs-lookup"><span data-stu-id="a8ea1-674">Event</span></span></td><td><span data-ttu-id="a8ea1-675">아니요. 지정하는 경우 날짜도 입력해야 함</span><span class="sxs-lookup"><span data-stu-id="a8ea1-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="a8ea1-676">Hello 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-676">One of hello following:</span></span><br><span data-ttu-id="a8ea1-677">• Click</span><span class="sxs-lookup"><span data-stu-id="a8ea1-677">• Click</span></span><br><span data-ttu-id="a8ea1-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="a8ea1-678">• RecommendationClick</span></span><br><span data-ttu-id="a8ea1-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="a8ea1-679">•    AddShopCart</span></span><br><span data-ttu-id="a8ea1-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="a8ea1-680">• RemoveShopCart</span></span><br><span data-ttu-id="a8ea1-681">• Purchase</span><span class="sxs-lookup"><span data-stu-id="a8ea1-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="a8ea1-682">최대 파일 크기 200MB</span><span class="sxs-lookup"><span data-stu-id="a8ea1-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="a8ea1-683">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="a8ea1-684">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-684">**Response**:</span></span>

<span data-ttu-id="a8ea1-685">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="a8ea1-686">`Feed\entry\content\properties\LineCount` – 허용되는 줄 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="a8ea1-687">`Feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="a8ea1-688">`Feed\entry\content\properties\FileId` – 파일 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="a8ea1-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-689">OData XML</span></span>

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


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="a8ea1-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-690">9.1.2.</span></span> <span data-ttu-id="a8ea1-691">데이터 취득 사용</span><span class="sxs-lookup"><span data-stu-id="a8ea1-691">Using Data Acquisition</span></span>
<span data-ttu-id="a8ea1-692">이 섹션에서는 real에서 toosend 이벤트 웹 사이트에서 일반적으로 tooAzure 시스템 학습 권장 사항으로 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="a8ea1-693">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-693">HTTP Method</span></span> | <span data-ttu-id="a8ea1-694">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-695">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="a8ea1-696">HEADER</span><span class="sxs-lookup"><span data-stu-id="a8ea1-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a8ea1-697">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-697">Parameter Name</span></span> | <span data-ttu-id="a8ea1-698">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-699">apiVersion</span></span> |<span data-ttu-id="a8ea1-700">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-700">1.0</span></span> |
| <span data-ttu-id="a8ea1-701">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-701">Request body</span></span> |<span data-ttu-id="a8ea1-702">이벤트 데이터 입력 원하는 toosend 각 이벤트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="a8ea1-703">Hello 동일한 사용자 또는 브라우저 세션 hello hello 세션 Id 필드에 동일한 ID에 대 한 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="a8ea1-704">아래 이벤트 본문 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="a8ea1-705">'Click' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="a8ea1-706">'RecommendationClick' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="a8ea1-707">'AddShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="a8ea1-708">'RemoveShopCart' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="a8ea1-709">'Purchase' 이벤트의 예:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-709">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="a8ea1-710">두 개의 이벤트 'Click' 및 'AddShopCart'를 보내는 예:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="a8ea1-711">**응답**: HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="a8ea1-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-712">9.2.</span></span>    <span data-ttu-id="a8ea1-713">모델 사용 파일 나열</span><span class="sxs-lookup"><span data-stu-id="a8ea1-713">List Model Usage Files</span></span>
<span data-ttu-id="a8ea1-714">모든 모델 사용 파일의 메타데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="a8ea1-715">hello 사용 파일 됩니다 한 페이지 한 번에 검색할 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="a8ea1-716">각 페이지는 100개의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-716">Each page containes 100 items.</span></span> <span data-ttu-id="a8ea1-717">특정 인덱스에서 tooget 항목을 하려는 경우에 hello $skip odata 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="a8ea1-718">예를 들어 tooget 항목 100 위치에서 시작 하려는 경우 추가 hello 매개 변수 $skip = 100 toohello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="a8ea1-719">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-719">HTTP Method</span></span> | <span data-ttu-id="a8ea1-720">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-721">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-722">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-723">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-723">Parameter Name</span></span> | <span data-ttu-id="a8ea1-724">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-725">forModelId</span></span> |<span data-ttu-id="a8ea1-726">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-727">apiVersion</span></span> |<span data-ttu-id="a8ea1-728">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-728">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-729">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-729">Request Body</span></span> |<span data-ttu-id="a8ea1-730">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-730">NONE</span></span> |

<span data-ttu-id="a8ea1-731">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-731">**Response**:</span></span>

<span data-ttu-id="a8ea1-732">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-732">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-733">hello 응답에는 사용 현황 파일 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="a8ea1-734">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-735">`feed\entry\content\properties\Id` – 사용 파일 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="a8ea1-736">`feed\entry\content\properties\Length` – 사용 파일 길이(MB)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="a8ea1-737">`feed\entry\content\properties\DateModified`-Hello 사용 현황 파일을 만든 날짜</span><span class="sxs-lookup"><span data-stu-id="a8ea1-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="a8ea1-738">`feed\entry\content\properties\UseInModel`-여부 hello 사용 현황 파일 hello 모델에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="a8ea1-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-739">OData XML</span></span>

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

### <a name="93----get-usage-statistics"></a><span data-ttu-id="a8ea1-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-740">9.3.</span></span>    <span data-ttu-id="a8ea1-741">사용 통계 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-741">Get Usage Statistics</span></span>
<span data-ttu-id="a8ea1-742">사용 통계를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-742">Gets usage statistics.</span></span>

| <span data-ttu-id="a8ea1-743">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-743">HTTP Method</span></span> | <span data-ttu-id="a8ea1-744">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-745">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-746">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-747">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-747">Parameter Name</span></span> | <span data-ttu-id="a8ea1-748">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-749">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-749">modelId</span></span> |<span data-ttu-id="a8ea1-750">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-751">startDate</span><span class="sxs-lookup"><span data-stu-id="a8ea1-751">startDate</span></span> |<span data-ttu-id="a8ea1-752">시작 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-752">Start date.</span></span> <span data-ttu-id="a8ea1-753">형식: yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="a8ea1-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="a8ea1-754">endDate</span><span class="sxs-lookup"><span data-stu-id="a8ea1-754">endDate</span></span> |<span data-ttu-id="a8ea1-755">종료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-755">End date.</span></span> <span data-ttu-id="a8ea1-756">형식: yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="a8ea1-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="a8ea1-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="a8ea1-757">eventTypes</span></span> |<span data-ttu-id="a8ea1-758">이벤트의 쉼표로 구분 된 문자열 또는 null tooget 모든 이벤트</span><span class="sxs-lookup"><span data-stu-id="a8ea1-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="a8ea1-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-759">apiVersion</span></span> |<span data-ttu-id="a8ea1-760">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-760">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-761">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-761">Request Body</span></span> |<span data-ttu-id="a8ea1-762">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-762">NONE</span></span> |

<span data-ttu-id="a8ea1-763">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-763">**Response**:</span></span>

<span data-ttu-id="a8ea1-764">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-764">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-765">키/값 요소의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-765">A collection of key/value elements.</span></span> <span data-ttu-id="a8ea1-766">각각 hello 합계의 시간별 특정 이벤트 유형의 이벤트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="a8ea1-767">`feed\entry[i]\content\properties\Key`-(시간별) hello 시간을 포함 합니다. 및 hello 이벤트 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="a8ea1-768">`feed\entry[i]\content\properties\Value` - 총 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="a8ea1-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-769">OData XML</span></span>

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

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="a8ea1-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-770">9.4.</span></span>    <span data-ttu-id="a8ea1-771">사용 파일 샘플 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-771">Get Usage File Sample</span></span>
<span data-ttu-id="a8ea1-772">검색 사용 파일 콘텐츠의 첫 번째 2KB hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="a8ea1-773">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-773">HTTP Method</span></span> | <span data-ttu-id="a8ea1-774">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-775">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-776">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-777">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-777">Parameter Name</span></span> | <span data-ttu-id="a8ea1-778">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-779">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-779">modelId</span></span> |<span data-ttu-id="a8ea1-780">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-781">fileId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-781">fileId</span></span> |<span data-ttu-id="a8ea1-782">Hello 모델 사용 파일의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="a8ea1-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-783">apiVersion</span></span> |<span data-ttu-id="a8ea1-784">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-784">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-785">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-785">Request Body</span></span> |<span data-ttu-id="a8ea1-786">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-786">NONE</span></span> |

<span data-ttu-id="a8ea1-787">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-787">**Response**:</span></span>

<span data-ttu-id="a8ea1-788">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-788">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-789">원시 텍스트 형식으로 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-789">Response is returned in raw text format:</span></span>

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


### <a name="95----get-model-usage-file"></a><span data-ttu-id="a8ea1-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-790">9.5.</span></span>    <span data-ttu-id="a8ea1-791">모델 사용 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-791">Get Model Usage File</span></span>
<span data-ttu-id="a8ea1-792">Hello hello 사용 파일의 전체 콘텐츠를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="a8ea1-793">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-793">HTTP Method</span></span> | <span data-ttu-id="a8ea1-794">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-795">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-796">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-797">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-797">Parameter Name</span></span> | <span data-ttu-id="a8ea1-798">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-799">mId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-799">mid</span></span> |<span data-ttu-id="a8ea1-800">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-801">fid</span><span class="sxs-lookup"><span data-stu-id="a8ea1-801">fid</span></span> |<span data-ttu-id="a8ea1-802">Hello 모델 사용 파일의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="a8ea1-803">다운로드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-803">download</span></span> |<span data-ttu-id="a8ea1-804">1</span><span class="sxs-lookup"><span data-stu-id="a8ea1-804">1</span></span> |
| <span data-ttu-id="a8ea1-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-805">apiVersion</span></span> |<span data-ttu-id="a8ea1-806">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-806">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-807">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-807">Request Body</span></span> |<span data-ttu-id="a8ea1-808">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-808">NONE</span></span> |

<span data-ttu-id="a8ea1-809">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-809">**Response**:</span></span>

<span data-ttu-id="a8ea1-810">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-810">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-811">원시 텍스트 형식으로 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-811">Response is returned in raw text format:</span></span>

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

### <a name="96----delete-usage-file"></a><span data-ttu-id="a8ea1-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-812">9.6.</span></span>    <span data-ttu-id="a8ea1-813">사용 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-813">Delete Usage File</span></span>
<span data-ttu-id="a8ea1-814">Hello 지정 된 모델 사용 현황 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="a8ea1-815">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-815">HTTP Method</span></span> | <span data-ttu-id="a8ea1-816">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-817">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-818">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-819">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-819">Parameter Name</span></span> | <span data-ttu-id="a8ea1-820">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-821">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-821">modelId</span></span> |<span data-ttu-id="a8ea1-822">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-823">fileId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-823">fileId</span></span> |<span data-ttu-id="a8ea1-824">Hello 파일 toobe 삭제의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="a8ea1-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-825">apiVersion</span></span> |<span data-ttu-id="a8ea1-826">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-826">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-827">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-827">Request Body</span></span> |<span data-ttu-id="a8ea1-828">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-828">NONE</span></span> |

<span data-ttu-id="a8ea1-829">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-829">**Response**:</span></span>

<span data-ttu-id="a8ea1-830">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="a8ea1-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-831">9.7.</span></span>    <span data-ttu-id="a8ea1-832">모든 사용 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-832">Delete All Usage Files</span></span>
<span data-ttu-id="a8ea1-833">모든 모델 사용 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="a8ea1-834">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-834">HTTP Method</span></span> | <span data-ttu-id="a8ea1-835">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-836">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-837">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-838">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-838">Parameter Name</span></span> | <span data-ttu-id="a8ea1-839">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-840">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-840">modelId</span></span> |<span data-ttu-id="a8ea1-841">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-842">apiVersion</span></span> |<span data-ttu-id="a8ea1-843">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-843">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-844">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-844">Request Body</span></span> |<span data-ttu-id="a8ea1-845">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-845">NONE</span></span> |

<span data-ttu-id="a8ea1-846">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-846">**Response**:</span></span>

<span data-ttu-id="a8ea1-847">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="a8ea1-848">10. 기능</span><span class="sxs-lookup"><span data-stu-id="a8ea1-848">10. Features</span></span>
<span data-ttu-id="a8ea1-849">이 섹션에서는 어떻게 tooretrieve 가져온 hello 기능 및 해당 값, 해당 순위 등의 정보 있을 수 있으며이 순위 할당 된 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="a8ea1-850">기능에서 가져온 hello 카탈로그 데이터의 한 다음 차수 관련 순위 빌드가 수행 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="a8ea1-851">기능 순위에 따라 toohello 패턴의 사용량 데이터 및 항목의 형식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="a8ea1-852">하지만 hello 순위 일관 된 사용 현황/항목에 대 한 약간의 변동이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="a8ea1-853">기능의 hello 순위 음수가 아닌 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="a8ea1-854">hello 숫자 0 의미 hello 기능을 순위가 지정 되지 않습니다 (첫 번째 순위 빌드 hello이 API 이전 toohello 완료를 호출 하는 경우 수행 됨).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="a8ea1-855">hello 날짜 hello 순위 특성이 지정 된 점수 freshness hello 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="a8ea1-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-856">10.1.</span></span> <span data-ttu-id="a8ea1-857">기능 정보 가져오기(마지막 순위 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="a8ea1-858">마지막으로 성공한 순위 빌드 hello에 대 한 순위 등의 hello 기능 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="a8ea1-859">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-859">HTTP Method</span></span> | <span data-ttu-id="a8ea1-860">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-861">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-862">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-863">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-863">Parameter Name</span></span> | <span data-ttu-id="a8ea1-864">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-865">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-865">modelId</span></span> |<span data-ttu-id="a8ea1-866">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="a8ea1-867">samplingSize</span></span> |<span data-ttu-id="a8ea1-868">Hello 카탈로그에 있는 toohello 데이터에 따라 각 기능에 대해 tooinclude 값의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="a8ea1-869">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-869">Possible values are:</span></span><br> <span data-ttu-id="a8ea1-870">-1 - 모든 샘플.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-870">-1 - All samples.</span></span> <br><span data-ttu-id="a8ea1-871">0 - 샘플링 없음.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-871">0 - No sampling.</span></span> <br><span data-ttu-id="a8ea1-872">N - 각 기능 이름별로 N개의 샘플 반환.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="a8ea1-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-873">apiVersion</span></span> |<span data-ttu-id="a8ea1-874">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-874">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-875">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-875">Request Body</span></span> |<span data-ttu-id="a8ea1-876">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-876">NONE</span></span> |

<span data-ttu-id="a8ea1-877">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-877">**Response**:</span></span>

<span data-ttu-id="a8ea1-878">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-878">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-879">hello 응답 기능 정보 항목의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="a8ea1-880">각 항목에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-880">Each entry contains:</span></span>

* <span data-ttu-id="a8ea1-881">`feed/entry/content/m:properties/d:Name` - 기능 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="a8ea1-882">`feed/entry/content/m:properties/d:RankUpdateDate`-순위는 hello에 할당 된 toothis 기능 라고도 함 된 날짜</span><span class="sxs-lookup"><span data-stu-id="a8ea1-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="a8ea1-883">점수 유효 시간)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-883">score freshness feature.</span></span> <span data-ttu-id="a8ea1-884">과거 날짜('0001-01-01T00:00:00')는 순위 빌드가 수행되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="a8ea1-885">`feed/entry/content/m:properties/d:Rank` - 기능 순위(부동 소수점).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="a8ea1-886">2.0 이상의 순위가 유용한 기능으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="a8ea1-887">`feed/entry/content/m:properties/d:SampleValues`-쉼표로 구분 된 목록 toohello 샘플링 크기 요청 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="a8ea1-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
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

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="a8ea1-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-889">10.2.</span></span> <span data-ttu-id="a8ea1-890">기능 정보 가져오기(특정 순위 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="a8ea1-891">Hello 특정 순위 빌드에 대 한 순위 등의 hello 기능 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="a8ea1-892">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-892">HTTP Method</span></span> | <span data-ttu-id="a8ea1-893">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-894">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-895">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-896">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-896">Parameter Name</span></span> | <span data-ttu-id="a8ea1-897">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-898">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-898">modelId</span></span> |<span data-ttu-id="a8ea1-899">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="a8ea1-900">samplingSize</span></span> |<span data-ttu-id="a8ea1-901">Hello 카탈로그에 있는 toohello 데이터에 따라 각 기능에 대해 tooinclude 값의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="a8ea1-902">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-902">Possible values are:</span></span><br> <span data-ttu-id="a8ea1-903">-1 - 모든 샘플.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-903">-1 - All samples.</span></span> <br><span data-ttu-id="a8ea1-904">0 - 샘플링 없음.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-904">0 - No sampling.</span></span> <br><span data-ttu-id="a8ea1-905">N - 각 기능 이름별로 N개의 샘플 반환.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="a8ea1-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-906">rankBuildId</span></span> |<span data-ttu-id="a8ea1-907">Hello 순위 빌드 또는 hello 마지막 순위 빌드에 대 한-1의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="a8ea1-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-908">apiVersion</span></span> |<span data-ttu-id="a8ea1-909">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-909">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-910">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-910">Request Body</span></span> |<span data-ttu-id="a8ea1-911">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-911">NONE</span></span> |

<span data-ttu-id="a8ea1-912">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-912">**Response**:</span></span>

<span data-ttu-id="a8ea1-913">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-913">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-914">hello 응답 기능 정보 항목의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="a8ea1-915">각 항목에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-915">Each entry contains:</span></span>

* <span data-ttu-id="a8ea1-916">`feed/entry/content/m:properties/d:Name` - 기능 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="a8ea1-917">`feed/entry/content/m:properties/d:RankUpdateDate`-순위는 hello에 할당 된 toothis 기능 라고도 함 된 날짜</span><span class="sxs-lookup"><span data-stu-id="a8ea1-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="a8ea1-918">점수 유효 시간)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-918">score freshness feature.</span></span> <span data-ttu-id="a8ea1-919">과거 날짜('0001-01-01T00:00:00')는 순위 빌드가 수행되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="a8ea1-920">`feed/entry/content/m:properties/d:Rank` - 기능 순위(부동 소수점).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="a8ea1-921">2.0 이상의 순위가 유용한 기능으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="a8ea1-922">`feed/entry/content/m:properties/d:SampleValues`-쉼표로 구분 된 목록 toohello 샘플링 크기 요청 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="a8ea1-923">OData</span><span class="sxs-lookup"><span data-stu-id="a8ea1-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
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


## <a name="11-build"></a><span data-ttu-id="a8ea1-924">11. 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-924">11. Build</span></span>
  <span data-ttu-id="a8ea1-925">이 섹션에서는 hello toobuilds와 관련 된 다른 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="a8ea1-926">세 가지 유형의 빌드(권장 사항 빌드, 순위 빌드 및 FBT(자주 함께 구매됨) 빌드)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="a8ea1-927">hello 권장 빌드 목적은 toogenerate 예측에 사용 되는 추천 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="a8ea1-928">예측(이 유형의 빌드 관련)은 다음 두 가지 유형으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="a8ea1-929">I2I</span><span class="sxs-lookup"><span data-stu-id="a8ea1-929">I2I - a.k.a.</span></span> <span data-ttu-id="a8ea1-930">항목 목록 또는 항목을 제공 된 tooItem 권장 사항을-항목의이 옵션을 예측 하는 가능성이 toobe 높은 관심 있는 항목의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="a8ea1-931">U2I</span><span class="sxs-lookup"><span data-stu-id="a8ea1-931">U2I - a.k.a.</span></span> <span data-ttu-id="a8ea1-932">사용자 tooItem-제공 된 권장 사항을 사용자 id (및 필요에 따라 항목의 목록)이이 옵션 가능성이 toobe 사용자 (및 추가 선택 항목)을 지정 하는 hello에 대 한 높은 관심 있는 항목의 목록을 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="a8ea1-933">hello U2I 권장 사항은 toohello 시간 hello 모델 작성 된 hello 사용자에 대 한 관심 있는 항목의 hello 기록을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="a8ea1-934">순위 빌드 hello 유용성 기능에 대 한 toolearn 수 있는 기술 빌드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="a8ea1-935">일반적으로 순서 tooget hello 최상의 결과에서 기능을 포함 하는 추천 모델에 대 한 단계를 수행 하는 hello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="a8ea1-936">Hello 기능 점수를 얻을 때까지 기다려 및 ()를 제외 기능 hello 점수 안정적인 순위 빌드를 트리거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="a8ea1-937">Hello 호출 하 여 hello 순위 기능을 검색할 [기능 정보 가져오기](#101-get-features-info-for-last-rank-build) API입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="a8ea1-938">Hello 매개 변수 뒤 권장 빌드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="a8ea1-939">`useFeatureInModel`-TooTrue 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="a8ea1-940">`ModelingFeatureList`2.0 이상의 점수 기능 집합 tooa 쉼표로 구분 된 목록 (따르는 toohello 순위 hello 이전 단계에서 검색)입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="a8ea1-941">`AllowColdItemPlacement`-TooTrue 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="a8ea1-942">필요에 따라 설정할 수 있습니다 `EnableFeatureCorrelation` tooTrue 및 `ReasoningFeatureList` toouse (일반적으로 모델링 또는 하위 목록을 사용 되는 기능 목록은 같은 hello) 설명에 대 한 원하는 기능의 toohello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="a8ea1-943">Hello로 트리거 hello 권장 빌드 매개 변수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="a8ea1-944">참고: 매개 변수를 구성 하지 않으면 (예: 매개 변수 없이 hello 권장 빌드 호출) 또는 hello 사용 기능을 명시적으로 해제 하지 않으면 (예: `UseFeatureInModel` tooFalse 설정), hello 시스템 hello 기능 관련 매개 변수를 설정 합니다 toohello 순위 빌드가 존재 하는 경우 위의 값을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="a8ea1-945">순위 빌드 실행에 제한이 없으며 및 권장 사항을 동시에 빌드할 hello에 대 한 동일한 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="a8ea1-946">그럼에도 불구 하 고 hello hello 동시에 같은 모델에 동일한 입력의 두 빌드를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="a8ea1-947">FBT(자주 함께 구매됨) 빌드는 유형이 다른(같은 유형: 책, 영화, 일부 음식, 패션, 다른 유형: 컴퓨터와 장치, 크로스 도메인, 고도로 다양) 카탈로그에 적합한 “보수적인" 추천이라고도 하는 다른 권장 사항 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="a8ea1-948">참고: hello 사용 파일 경우 업로드 hello 선택적 필드 "이벤트 형식" 다음 FBT "Purchase" 이벤트만 모델링 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="a8ea1-949">이벤트 유형이 제공되지 않은 경우에는 모든 이벤트가 구매로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="a8ea1-950">11.1 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-950">11.1 Build parameters</span></span>
<span data-ttu-id="a8ea1-951">각 빌드 형식은 매개 변수 집합(아래 설명)을 통해 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="a8ea1-952">Hello 매개 변수를 구성 하지 않는 경우 hello 시스템 toohello 정보 hello 시간에 빌드를 트리거에 따라 toohello 매개 변수 값 특성이 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="a8ea1-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-953">11.1.1.</span></span> <span data-ttu-id="a8ea1-954">사용 콘덴서</span><span class="sxs-lookup"><span data-stu-id="a8ea1-954">Usage condenser</span></span>
<span data-ttu-id="a8ea1-955">사용 포인트가 거의 없는 사용자 또는 항목은 정보보다 노이즈를 더 많이 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="a8ea1-956">hello 시스템 toopredict hello 최소한의 모델에 사용 되는 사용자/항목 toobe 당 사용 포인트를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="a8ea1-957">이 번호가 ItemCutoffLowerBound hello 및 항목과 UserCutOffLowerBound hello 및 사용자에 대 한 UserCutoffUpperBound 매개 변수에 의해 정의 된 hello 범위에 대 한 ItemCutoffUpperBound 매개 변수에 의해 정의 된 hello 범위 내에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="a8ea1-958">해당 범위 toozero hello 중 하나 이상을 설정 하 여 항목이 나 사용자가에 hello 콘덴서 영향을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="a8ea1-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-959">11.1.2.</span></span> <span data-ttu-id="a8ea1-960">순위 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-960">Rank build parameters</span></span>
<span data-ttu-id="a8ea1-961">hello 다음 표에서 순위 빌드에 대 한 hello 빌드 매개 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="a8ea1-962">키</span><span class="sxs-lookup"><span data-stu-id="a8ea1-962">Key</span></span> | <span data-ttu-id="a8ea1-963">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-963">Description</span></span> | <span data-ttu-id="a8ea1-964">형식</span><span class="sxs-lookup"><span data-stu-id="a8ea1-964">Type</span></span> | <span data-ttu-id="a8ea1-965">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a8ea1-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a8ea1-966">NumberOfModelIterations</span></span> |<span data-ttu-id="a8ea1-967">hello 수의 반복 hello 모델의 성능을 hello 리플렉션하 전체 시간 및 hello 모델 정확도 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="a8ea1-968">hello hello 크면, hello 더 나은 정확도 받아볼 수 있지만 hello 시간이 오래 걸립니다. 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="a8ea1-969">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-969">Integer</span></span> |<span data-ttu-id="a8ea1-970">10-50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-970">10-50</span></span> |
| <span data-ttu-id="a8ea1-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a8ea1-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="a8ea1-972">차원 수가 hello toohello 수가 '기능' hello 모델 toofind 데이터 내에서 시도 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="a8ea1-973">Hello 차원 수를 늘리면 더 작은 클러스터로 hello 결과의 더 나은 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="a8ea1-974">그러나 차원이 너무 많습니다. 항목 간의 상관 관계를 찾을 hello 모델 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="a8ea1-975">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-975">Integer</span></span> |<span data-ttu-id="a8ea1-976">10-40</span><span class="sxs-lookup"><span data-stu-id="a8ea1-976">10-40</span></span> |
| <span data-ttu-id="a8ea1-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a8ea1-978">Hello 콘덴서에 대 한 hello 항목 하한값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-979">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-979">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-980">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-980">Integer</span></span> |<span data-ttu-id="a8ea1-981">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a8ea1-983">Hello 콘덴서에 대 한 hello 항목 상한 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-984">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-984">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-985">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-985">Integer</span></span> |<span data-ttu-id="a8ea1-986">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="a8ea1-988">Hello 콘덴서에 대 한 hello 사용자 하한값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-989">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-989">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-990">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-990">Integer</span></span> |<span data-ttu-id="a8ea1-991">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="a8ea1-993">Hello 콘덴서에 대 한 hello 사용자 상한 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-994">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-994">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-995">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-995">Integer</span></span> |<span data-ttu-id="a8ea1-996">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="a8ea1-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-997">11.1.3.</span></span> <span data-ttu-id="a8ea1-998">권장 사항 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-998">Recommendation build parameters</span></span>
<span data-ttu-id="a8ea1-999">hello 다음 표에서 권장 사항 빌드에 대 한 hello 빌드 매개 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="a8ea1-1000">키</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1000">Key</span></span> | <span data-ttu-id="a8ea1-1001">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1001">Description</span></span> | <span data-ttu-id="a8ea1-1002">형식</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1002">Type</span></span> | <span data-ttu-id="a8ea1-1003">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a8ea1-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="a8ea1-1005">hello 수의 반복 hello 모델의 성능을 hello 리플렉션하 전체 시간 및 hello 모델 정확도 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="a8ea1-1006">hello hello 크면, hello 더 나은 정확도 받아볼 수 있지만 hello 시간이 오래 걸립니다. 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="a8ea1-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1007">Integer</span></span> |<span data-ttu-id="a8ea1-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1008">10-50</span></span> |
| <span data-ttu-id="a8ea1-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="a8ea1-1010">차원 수가 hello toohello 수가 '기능' hello 모델 toofind 데이터 내에서 시도 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="a8ea1-1011">Hello 차원 수를 늘리면 더 작은 클러스터로 hello 결과의 더 나은 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="a8ea1-1012">그러나 차원이 너무 많습니다. 항목 간의 상관 관계를 찾을 hello 모델 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="a8ea1-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1013">Integer</span></span> |<span data-ttu-id="a8ea1-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1014">10-40</span></span> |
| <span data-ttu-id="a8ea1-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a8ea1-1016">Hello 콘덴서에 대 한 hello 항목 하한값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1017">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1017">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1018">Integer</span></span> |<span data-ttu-id="a8ea1-1019">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a8ea1-1021">Hello 콘덴서에 대 한 hello 항목 상한 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1022">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1022">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1023">Integer</span></span> |<span data-ttu-id="a8ea1-1024">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="a8ea1-1026">Hello 콘덴서에 대 한 hello 사용자 하한값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1027">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1027">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1028">Integer</span></span> |<span data-ttu-id="a8ea1-1029">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="a8ea1-1031">Hello 콘덴서에 대 한 hello 사용자 상한 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1032">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1032">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1033">Integer</span></span> |<span data-ttu-id="a8ea1-1034">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1035">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1035">Description</span></span> |<span data-ttu-id="a8ea1-1036">빌드 설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1036">Build description.</span></span> |<span data-ttu-id="a8ea1-1037">String</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1037">String</span></span> |<span data-ttu-id="a8ea1-1038">모든 텍스트, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="a8ea1-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1039">EnableModelingInsights</span></span> |<span data-ttu-id="a8ea1-1040">있습니다 toocompute 메트릭을 hello 추천 모델에서.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="a8ea1-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1041">Boolean</span></span> |<span data-ttu-id="a8ea1-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1042">True/False</span></span> |
| <span data-ttu-id="a8ea1-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="a8ea1-1044">기능 순서 tooenhance hello 추천 모델에서 사용할 수 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="a8ea1-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1045">Boolean</span></span> |<span data-ttu-id="a8ea1-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1046">True/False</span></span> |
| <span data-ttu-id="a8ea1-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1047">ModelingFeatureList</span></span> |<span data-ttu-id="a8ea1-1048">쉼표로 구분 된 목록 순서 tooenhance hello 권장 구성의 hello 권장 빌드에 사용 하는 기능 이름은 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="a8ea1-1049">문자열</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1049">String</span></span> |<span data-ttu-id="a8ea1-1050">기능 이름, too512 문자를</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="a8ea1-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="a8ea1-1052">Hello 권장 구성 최초 항목 기능 유사성을 통해 푸시하여도 해야 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="a8ea1-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1053">Boolean</span></span> |<span data-ttu-id="a8ea1-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1054">True/False</span></span> |
| <span data-ttu-id="a8ea1-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="a8ea1-1056">추론에서 기능을 사용할 수 있는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="a8ea1-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1057">Boolean</span></span> |<span data-ttu-id="a8ea1-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1058">True/False</span></span> |
| <span data-ttu-id="a8ea1-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="a8ea1-1060">쉼표로 구분 된 목록 (예: 권장 사항 설명) 문장 추론에 사용 되는 기능 이름은 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="a8ea1-1061">문자열</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1061">String</span></span> |<span data-ttu-id="a8ea1-1062">기능 이름, too512 문자를</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="a8ea1-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1063">EnableU2I</span></span> |<span data-ttu-id="a8ea1-1064">개인 설정 된 hello 권장 라고도 함 허용</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="a8ea1-1065">U2I (사용자 tooitem 권장 구성).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="a8ea1-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1066">Boolean</span></span> |<span data-ttu-id="a8ea1-1067">True/False(기본값 true)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="a8ea1-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1068">11.1.4.</span></span> <span data-ttu-id="a8ea1-1069">FBT 빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1069">FBT build parameters</span></span>
<span data-ttu-id="a8ea1-1070">hello 다음 표에서 권장 사항 빌드에 대 한 hello 빌드 매개 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="a8ea1-1071">키</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1071">Key</span></span> | <span data-ttu-id="a8ea1-1072">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1072">Description</span></span> | <span data-ttu-id="a8ea1-1073">형식</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1073">Type</span></span> | <span data-ttu-id="a8ea1-1074">유효한 값(기본값)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a8ea1-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="a8ea1-1076">보수적인 hello 모델은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1076">How conservative hello model is.</span></span> <span data-ttu-id="a8ea1-1077">모델링을 위한 것으로 간주 하는 항목 toobe 공동 일치의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="a8ea1-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1078">Integer</span></span> |<span data-ttu-id="a8ea1-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1079">3-50 (6)</span></span> |
| <span data-ttu-id="a8ea1-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="a8ea1-1081">Hello 수 자주 집합에 있는 항목의 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="a8ea1-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1082">Integer</span></span> |<span data-ttu-id="a8ea1-1083">2-3(2)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1083">2-3 (2)</span></span> |
| <span data-ttu-id="a8ea1-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1084">FbtMinimalScore</span></span> |<span data-ttu-id="a8ea1-1085">최소 점수 집합을 자주 수행 해야 hello에 포함 되는 순서 toobe에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="a8ea1-1086">hello 더 높은 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1086">hello higher hello better.</span></span> |<span data-ttu-id="a8ea1-1087">Double</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1087">Double</span></span> |<span data-ttu-id="a8ea1-1088">0 이상(0)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1088">0 and above (0)</span></span> |
| <span data-ttu-id="a8ea1-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="a8ea1-1090">Hello 유사성 함수 toobe hello 빌드에 의해 사용 되는 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="a8ea1-1091">리프트 serendipity를 우선으로, 예측 가능성을를 우선으로 동시 발생 및 Jaccard hello 2 간 좋은 절충안입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="a8ea1-1092">문자열</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1092">String</span></span> |<span data-ttu-id="a8ea1-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="a8ea1-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1094">11.2.</span></span> <span data-ttu-id="a8ea1-1095">권장 사항 빌드 트리거</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="a8ea1-1096">기본적으로 이 API는 권장 사항 모델 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="a8ea1-1097">순위 tootrigger (순서 tooscore 기능)에서 빌드, hello 빌드 API variant 빌드 형식 매개 변수와 함께 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="a8ea1-1098">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1098">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1099">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1100">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1101">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a8ea1-1102">HEADER</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1102">HEADER</span></span> |<span data-ttu-id="a8ea1-1103">`"Content-Type", "text/xml"` (요청 본문을 보내는 경우)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="a8ea1-1104">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1104">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1105">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1106">modelId</span></span> |<span data-ttu-id="a8ea1-1107">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1108">userDescription</span></span> |<span data-ttu-id="a8ea1-1109">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="a8ea1-1110">공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="a8ea1-1111">위 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1111">See example above.</span></span><br><span data-ttu-id="a8ea1-1112">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1112">Max length: 50</span></span> |
| <span data-ttu-id="a8ea1-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1113">apiVersion</span></span> |<span data-ttu-id="a8ea1-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-1115">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1115">Request Body</span></span> |<span data-ttu-id="a8ea1-1116">비워 두면 hello 빌드 hello 기본 빌드 매개 변수와 함께 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="a8ea1-1117">Tooset hello 빌드 매개 변수를 사용 하도록 하려는 경우 다음 예제는 hello와 같이 hello 본문으로 hello 매개 변수 XML로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="a8ea1-1118">(에 대 한 설명은 hello 매개 변수는 hello "빌드 매개 변수" 섹션 참조).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="a8ea1-1119">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1119">**Response**:</span></span>

<span data-ttu-id="a8ea1-1120">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1121">비동기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1121">This is an asynchronous API.</span></span> <span data-ttu-id="a8ea1-1122">응답으로 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="a8ea1-1123">hello 빌드 끝나면 tooknow, 해야 hello "Get 빌드 상태의 정도 모델" API를 호출 하 고 배치할 있습니다 hello 응답에서이 빌드 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="a8ea1-1124">Note 빌드 hello hello 데이터 크기에 따라 분 toohours에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="a8ea1-1125">Hello 빌드 끝까지 권장 사항을 소비할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="a8ea1-1126">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1126">Valid build status:</span></span>

* <span data-ttu-id="a8ea1-1127">Create - 빌드 요청이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="a8ea1-1128">Queued – 빌드 요청을 보냈으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="a8ea1-1129">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="a8ea1-1130">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a8ea1-1131">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a8ea1-1132">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a8ea1-1133">취소 하 고-hello 빌드에 대 한 취소 요청을 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="a8ea1-1134">Note는 hello 빌드 경로 따라 hello에서 ID를 찾을 수 있습니다.`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="a8ea1-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1135">OData XML</span></span>

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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="a8ea1-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1136">11.3.</span></span> <span data-ttu-id="a8ea1-1137">빌드(권장 사항, 순위 또는 FBT) 트리거</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="a8ea1-1138">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1138">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1139">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1140">POST</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1141">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a8ea1-1142">HEADER</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1142">HEADER</span></span> |<span data-ttu-id="a8ea1-1143">`"Content-Type", "text/xml"` (요청 본문을 보내는 경우)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="a8ea1-1144">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1144">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1145">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1146">modelId</span></span> |<span data-ttu-id="a8ea1-1147">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1148">userDescription</span></span> |<span data-ttu-id="a8ea1-1149">Hello 카탈로그의 텍스트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="a8ea1-1150">공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="a8ea1-1151">위 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1151">See example above.</span></span><br><span data-ttu-id="a8ea1-1152">최대 길이: 50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1152">Max length: 50</span></span> |
| <span data-ttu-id="a8ea1-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1153">buildType</span></span> |<span data-ttu-id="a8ea1-1154">Hello 빌드 tooinvoke 유형:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="a8ea1-1155">- 권장 사항 빌드의 경우 'Recommendation'</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="a8ea1-1156">- 순위 빌드의 경우 'Ranking'</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="a8ea1-1157">- FBT 빌드의 경우 'Fbt'</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="a8ea1-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1158">apiVersion</span></span> |<span data-ttu-id="a8ea1-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-1160">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1160">Request Body</span></span> |<span data-ttu-id="a8ea1-1161">비워 두면 hello 빌드 hello 기본 빌드 매개 변수와 함께 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="a8ea1-1162">원하는 tooset 빌드 매개 변수를 XML로 샘플 다음 hello와 같은 hello 본문으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="a8ea1-1163">(자세한 설명 및 hello 매개 변수의 전체 목록은 hello "빌드 매개 변수" 섹션 참조).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="a8ea1-1164">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1164">**Response**:</span></span>

<span data-ttu-id="a8ea1-1165">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1166">비동기 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1166">This is an asynchronous API.</span></span> <span data-ttu-id="a8ea1-1167">응답으로 빌드 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="a8ea1-1168">hello 빌드 끝나면 tooknow, 해야 hello "Get 빌드 상태의 정도 모델" API를 호출 하 고 배치할 있습니다 hello 응답에서이 빌드 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="a8ea1-1169">Note 빌드 hello hello 데이터 크기에 따라 분 toohours에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="a8ea1-1170">Hello 빌드 끝까지 권장 사항을 소비할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="a8ea1-1171">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1171">Valid build status:</span></span>

* <span data-ttu-id="a8ea1-1172">Create – 모델을 만듦</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1172">Create - Model was created.</span></span>
* <span data-ttu-id="a8ea1-1173">Queued – 모델 빌드가 트리거되고 쿼리됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="a8ea1-1174">Building – 모델을 빌드하는 중</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="a8ea1-1175">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a8ea1-1176">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a8ea1-1177">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a8ea1-1178">Cancelling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a8ea1-1179">Note는 hello 빌드 경로 따라 hello에서 ID를 찾을 수 있습니다.`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="a8ea1-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1180">OData XML</span></span>

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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="a8ea1-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1181">11.4.</span></span> <span data-ttu-id="a8ea1-1182">모델의 빌드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="a8ea1-1183">지정된 모델의 빌드 및 해당 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="a8ea1-1184">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1184">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1185">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1186">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1187">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1188">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1188">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1189">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1190">modelId</span></span> |<span data-ttu-id="a8ea1-1191">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1192">onlyLastBuild</span></span> |<span data-ttu-id="a8ea1-1193">나타냅니다 tooreturn hello 모든 만들 hello 모델의 기록 또는 유일한 hello 상태의 hello 최신 빌드가 있는지 여부를</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="a8ea1-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1194">apiVersion</span></span> |<span data-ttu-id="a8ea1-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1195">1.0</span></span> |

<span data-ttu-id="a8ea1-1196">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1196">**Response**:</span></span>

<span data-ttu-id="a8ea1-1197">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1198">hello 응답 빌드 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="a8ea1-1199">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1200">`feed/entry/content/properties/UserName`-Hello 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="a8ea1-1201">`feed/entry/content/properties/ModelName`-Hello 모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="a8ea1-1202">`feed/entry/content/properties/ModelId` – 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="a8ea1-1203">`feed/entry/content/properties/IsDeployed`-Hello 빌드 (규칙 하위 배포 여부</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="a8ea1-1204">활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1204">active build).</span></span>
* <span data-ttu-id="a8ea1-1205">`feed/entry/content/properties/BuildId` – 빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="a8ea1-1206">`feed/entry/content/properties/BuildType`-Hello 빌드의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="a8ea1-1207">`feed/entry/content/properties/Status` – 빌드 상태</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="a8ea1-1208">Hello 다음 중 하나일 수 있습니다: 오류, 건물, 대기, 취소, 취소 됨, 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="a8ea1-1209">`feed/entry/content/properties/StatusMessage`-자세한 상태 메시지 (toospecific 상태에만 적용 됨).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="a8ea1-1210">`feed/entry/content/properties/Progress` – 빌드 진행률(%)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="a8ea1-1211">`feed/entry/content/properties/StartTime` – 빌드 시작 시간</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="a8ea1-1212">`feed/entry/content/properties/EndTime` – 빌드 종료 시간</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="a8ea1-1213">`feed/entry/content/properties/ExecutionTime` – 빌드 기간</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="a8ea1-1214">`feed/entry/content/properties/ProgressStep`-진행 중인 빌드가의 현재 단계 hello에 대 한 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="a8ea1-1215">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1215">Valid build status:</span></span>

* <span data-ttu-id="a8ea1-1216">Created – 빌드 요청 항목이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="a8ea1-1217">Queued – 빌드 요청이 트리거되었으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="a8ea1-1218">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="a8ea1-1219">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a8ea1-1220">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a8ea1-1221">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a8ea1-1222">Cancelling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a8ea1-1223">유효한 빌드 형식 값:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1223">Valid values for build type:</span></span>

* <span data-ttu-id="a8ea1-1224">Rank - 순위 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="a8ea1-1225">Recommendation - 권장 사항 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="a8ea1-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1226">OData XML</span></span>

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


### <a name="115-get-builds-status"></a><span data-ttu-id="a8ea1-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1227">11.5.</span></span> <span data-ttu-id="a8ea1-1228">빌드 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1228">Get Builds Status</span></span>
<span data-ttu-id="a8ea1-1229">사용자의 모든 모델에 대한 빌드 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="a8ea1-1230">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1230">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1231">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1232">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1233">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1234">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1234">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1235">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1236">onlyLastBuild</span></span> |<span data-ttu-id="a8ea1-1237">나타냅니다 hello 모든 tooreturn hello 모델의 기록 빌드할지 hello 가장 최근 빌드의 유일한 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="a8ea1-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1238">apiVersion</span></span> |<span data-ttu-id="a8ea1-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1239">1.0</span></span> |

<span data-ttu-id="a8ea1-1240">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1240">**Response**:</span></span>

<span data-ttu-id="a8ea1-1241">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1242">hello 응답 빌드 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="a8ea1-1243">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1244">`feed/entry/content/properties/UserName`-Hello 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="a8ea1-1245">`feed/entry/content/properties/ModelName`-Hello 모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="a8ea1-1246">`feed/entry/content/properties/ModelId` – 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="a8ea1-1247">`feed/entry/content/properties/IsDeployed`-여부 hello 빌드가 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="a8ea1-1248">`feed/entry/content/properties/BuildId` – 빌드의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="a8ea1-1249">`feed/entry/content/properties/BuildType`-Hello 빌드의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="a8ea1-1250">`feed/entry/content/properties/Status` – 빌드 상태</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="a8ea1-1251">Hello 다음 중 하나일 수 있습니다: 오류, 건물, 대기, 취소 됨, 취소, 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="a8ea1-1252">`feed/entry/content/properties/StatusMessage`-자세한 상태 메시지 (toospecific 상태에만 적용 됨).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="a8ea1-1253">`feed/entry/content/properties/Progress` – 빌드 진행률(%)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="a8ea1-1254">`feed/entry/content/properties/StartTime` – 빌드 시작 시간</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="a8ea1-1255">`feed/entry/content/properties/EndTime` – 빌드 종료 시간</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="a8ea1-1256">`feed/entry/content/properties/ExecutionTime` – 빌드 기간</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="a8ea1-1257">`feed/entry/content/properties/ProgressStep`-진행 중인 빌드가의 현재 단계 hello에 대 한 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="a8ea1-1258">유효한 빌드 상태:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1258">Valid build status:</span></span>

* <span data-ttu-id="a8ea1-1259">Created – 빌드 요청 항목이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="a8ea1-1260">Queued – 빌드 요청이 트리거되었으며 큐에 대기됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="a8ea1-1261">Building – 빌드가 진행 중임</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="a8ea1-1262">Success – 빌드가 성공적으로 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a8ea1-1263">Error – 오류로 인해 빌드가 종료됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a8ea1-1264">Cancelled – 빌드가 취소됨</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a8ea1-1265">Cancelling – 빌드 취소 중</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a8ea1-1266">유효한 빌드 형식 값:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1266">Valid values for build type:</span></span>

* <span data-ttu-id="a8ea1-1267">Rank - 순위 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="a8ea1-1268">Recommendation - 권장 사항 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="a8ea1-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1269">OData XML</span></span>

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


### <a name="116-delete-build"></a><span data-ttu-id="a8ea1-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1270">11.6.</span></span> <span data-ttu-id="a8ea1-1271">빌드 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1271">Delete Build</span></span>
<span data-ttu-id="a8ea1-1272">빌드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1272">Deletes a build.</span></span>

<span data-ttu-id="a8ea1-1273">참고: </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1273">NOTE:</span></span> <br><span data-ttu-id="a8ea1-1274">활성 빌드는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1274">You cannot delete an active build.</span></span> <span data-ttu-id="a8ea1-1275">hello 모델 해야 tooa 다른 활성 빌드를 삭제 하기 전에 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="a8ea1-1276">진행 중인 빌드는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="a8ea1-1277">호출 하 여 먼저 hello 빌드를 취소 해야 <strong>빌드 취소</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="a8ea1-1278">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1278">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1279">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1280">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1281">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1282">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1282">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1283">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1284">buildId</span></span> |<span data-ttu-id="a8ea1-1285">Hello 빌드의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="a8ea1-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1286">apiVersion</span></span> |<span data-ttu-id="a8ea1-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1287">1.0</span></span> |

<span data-ttu-id="a8ea1-1288">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1288">**Response:**</span></span>

<span data-ttu-id="a8ea1-1289">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="a8ea1-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1290">11.7.</span></span> <span data-ttu-id="a8ea1-1291">빌드 취소</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1291">Cancel Build</span></span>
<span data-ttu-id="a8ea1-1292">빌드 중 상태인 빌드를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="a8ea1-1293">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1293">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1294">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1296">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1297">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1297">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1298">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1299">buildId</span></span> |<span data-ttu-id="a8ea1-1300">Hello 빌드의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="a8ea1-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1301">apiVersion</span></span> |<span data-ttu-id="a8ea1-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1302">1.0</span></span> |

<span data-ttu-id="a8ea1-1303">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1303">**Response:**</span></span>

<span data-ttu-id="a8ea1-1304">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="a8ea1-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1305">11.8.</span></span> <span data-ttu-id="a8ea1-1306">빌드 매개 변수 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1306">Get Build Parameters</span></span>
<span data-ttu-id="a8ea1-1307">빌드 매개 변수를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="a8ea1-1308">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1308">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1309">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1310">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1311">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1312">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1312">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1313">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1314">buildId</span></span> |<span data-ttu-id="a8ea1-1315">Hello 빌드의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="a8ea1-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1316">apiVersion</span></span> |<span data-ttu-id="a8ea1-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1317">1.0</span></span> |

<span data-ttu-id="a8ea1-1318">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1318">**Response:**</span></span>

<span data-ttu-id="a8ea1-1319">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1320">이 API는 키/값 요소의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="a8ea1-1321">각 요소는 매개 변수와 해당 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="a8ea1-1322">`feed/entry/content/properties/Key` - 빌드 매개 변수 이름.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="a8ea1-1323">`feed/entry/content/properties/Value` - 빌드 매개 변수 값.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="a8ea1-1324">hello 다음 표에서 각 키를 나타내는 hello 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="a8ea1-1325">키</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1325">Key</span></span> | <span data-ttu-id="a8ea1-1326">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1326">Description</span></span> | <span data-ttu-id="a8ea1-1327">형식</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1327">Type</span></span> | <span data-ttu-id="a8ea1-1328">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a8ea1-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="a8ea1-1330">hello 수의 반복 hello 모델의 성능을 hello 리플렉션하 전체 시간 및 hello 모델 정확도 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="a8ea1-1331">hello hello 크면, hello 더 나은 정확도 받아볼 수 있지만 hello 시간이 오래 걸립니다. 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="a8ea1-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1332">Integer</span></span> |<span data-ttu-id="a8ea1-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1333">10-50</span></span> |
| <span data-ttu-id="a8ea1-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="a8ea1-1335">차원 수가 hello toohello 수가 '기능' hello 모델 toofind 데이터 내에서 시도 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="a8ea1-1336">Hello 차원 수를 늘리면 더 작은 클러스터로 hello 결과의 더 나은 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="a8ea1-1337">그러나 차원이 너무 많습니다. 항목 간의 상관 관계를 찾을 hello 모델 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="a8ea1-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1338">Integer</span></span> |<span data-ttu-id="a8ea1-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1339">10-40</span></span> |
| <span data-ttu-id="a8ea1-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a8ea1-1341">Hello 콘덴서에 대 한 hello 항목 하한값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1342">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1342">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1343">Integer</span></span> |<span data-ttu-id="a8ea1-1344">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a8ea1-1346">Hello 콘덴서에 대 한 hello 항목 상한 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1347">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1347">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1348">Integer</span></span> |<span data-ttu-id="a8ea1-1349">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="a8ea1-1351">Hello 콘덴서에 대 한 hello 사용자 하한값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1352">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1352">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1353">Integer</span></span> |<span data-ttu-id="a8ea1-1354">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="a8ea1-1356">Hello 콘덴서에 대 한 hello 사용자 상한 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="a8ea1-1357">위의 사용 콘덴서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1357">See usage condenser above.</span></span> |<span data-ttu-id="a8ea1-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1358">Integer</span></span> |<span data-ttu-id="a8ea1-1359">2 이상(0 - 콘덴서 사용 안 함)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a8ea1-1360">설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1360">Description</span></span> |<span data-ttu-id="a8ea1-1361">빌드 설명</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1361">Build description.</span></span> |<span data-ttu-id="a8ea1-1362">String</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1362">String</span></span> |<span data-ttu-id="a8ea1-1363">모든 텍스트, 최대 512자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="a8ea1-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1364">EnableModelingInsights</span></span> |<span data-ttu-id="a8ea1-1365">있습니다 toocompute 메트릭을 hello 추천 모델에서.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="a8ea1-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1366">Boolean</span></span> |<span data-ttu-id="a8ea1-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1367">True/False</span></span> |
| <span data-ttu-id="a8ea1-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="a8ea1-1369">기능 순서 tooenhance hello 추천 모델에서 사용할 수 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="a8ea1-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1370">Boolean</span></span> |<span data-ttu-id="a8ea1-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1371">True/False</span></span> |
| <span data-ttu-id="a8ea1-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1372">ModelingFeatureList</span></span> |<span data-ttu-id="a8ea1-1373">쉼표로 구분 된 목록 순서 tooenhance hello 권장 구성의 hello 권장 빌드에 사용 하는 기능 이름은 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="a8ea1-1374">문자열</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1374">String</span></span> |<span data-ttu-id="a8ea1-1375">기능 이름, too512 문자를</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="a8ea1-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="a8ea1-1377">Hello 권장 구성 최초 항목 기능 유사성을 통해 푸시하여도 해야 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="a8ea1-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1378">Boolean</span></span> |<span data-ttu-id="a8ea1-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1379">True/False</span></span> |
| <span data-ttu-id="a8ea1-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="a8ea1-1381">추론에서 기능을 사용할 수 있는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="a8ea1-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1382">Boolean</span></span> |<span data-ttu-id="a8ea1-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1383">True/False</span></span> |
| <span data-ttu-id="a8ea1-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="a8ea1-1385">쉼표로 구분 된 목록 (예: 권장 사항 설명) 문장 추론에 사용 되는 기능 이름은 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="a8ea1-1386">문자열</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1386">String</span></span> |<span data-ttu-id="a8ea1-1387">기능 이름, too512 문자를</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="a8ea1-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1388">OData XML</span></span>

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

## <a name="12-recommendation"></a><span data-ttu-id="a8ea1-1389">12. 권장 사항</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="a8ea1-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1390">12.1.</span></span> <span data-ttu-id="a8ea1-1391">항목 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="a8ea1-1392">형식의 hello 활성 빌드의 권장 사항을 "권장" 메시지가 "Fbt" 초기값 (입력) 항목의 목록에 따라 또는.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="a8ea1-1393">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1393">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1394">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1395">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1396">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1397">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1397">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1398">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1399">modelId</span></span> |<span data-ttu-id="a8ea1-1400">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1401">itemIds</span></span> |<span data-ttu-id="a8ea1-1402">쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="a8ea1-1403">Hello 활성 빌드의 경우 다음 항목을 하나만 보낼 수 FBT를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="a8ea1-1404">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1404">Max length: 1024</span></span> |
| <span data-ttu-id="a8ea1-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1405">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1406">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1406">Number of required results</span></span> <br> <span data-ttu-id="a8ea1-1407">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1407">Max: 150</span></span> |
| <span data-ttu-id="a8ea1-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1408">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1409">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1409">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1410">apiVersion</span></span> |<span data-ttu-id="a8ea1-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1411">1.0</span></span> |

<span data-ttu-id="a8ea1-1412">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1412">**Response:**</span></span>

<span data-ttu-id="a8ea1-1413">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1414">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1415">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1416">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1417">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1418">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1419">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1420">아래 예제 응답 hello 10 개 권장된 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="a8ea1-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1421">OData XML</span></span>

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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="a8ea1-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1422">12.2.</span></span> <span data-ttu-id="a8ea1-1423">항목 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="a8ea1-1424">특정 빌드 형식 "Recommendation" 또는 "Fbt"의 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="a8ea1-1425">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1425">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1426">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1427">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1428">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1429">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1429">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1430">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1431">modelId</span></span> |<span data-ttu-id="a8ea1-1432">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1433">itemIds</span></span> |<span data-ttu-id="a8ea1-1434">쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="a8ea1-1435">Hello 활성 빌드의 경우 다음 항목을 하나만 보낼 수 FBT를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="a8ea1-1436">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1436">Max length: 1024</span></span> |
| <span data-ttu-id="a8ea1-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1437">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1438">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1438">Number of required results</span></span> <br> <span data-ttu-id="a8ea1-1439">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1439">Max: 150</span></span> |
| <span data-ttu-id="a8ea1-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1440">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1441">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1441">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1442">buildId</span></span> |<span data-ttu-id="a8ea1-1443">hello이 권장 구성 요청에 대 한 id toouse 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a8ea1-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1444">apiVersion</span></span> |<span data-ttu-id="a8ea1-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1445">1.0</span></span> |

<span data-ttu-id="a8ea1-1446">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1446">**Response:**</span></span>

<span data-ttu-id="a8ea1-1447">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1448">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1449">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1450">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1451">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1452">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1453">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1454">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="a8ea1-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1455">12.3.</span></span> <span data-ttu-id="a8ea1-1456">FBT 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="a8ea1-1457">시드 (입력) 항목을 기반으로 하는 "Fbt" 형식의 hello 활성 빌드의 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="a8ea1-1458">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1458">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1459">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1460">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1461">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1462">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1462">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1463">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1464">modelId</span></span> |<span data-ttu-id="a8ea1-1465">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1466">itemId</span></span> |<span data-ttu-id="a8ea1-1467">에 대 한 항목 toorecommend 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="a8ea1-1468">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1468">Max length: 1024</span></span> |
| <span data-ttu-id="a8ea1-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1469">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1470">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1470">Number of required results</span></span> <br><span data-ttu-id="a8ea1-1471">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1471">Max: 150</span></span> |
| <span data-ttu-id="a8ea1-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1472">minimalScore</span></span> |<span data-ttu-id="a8ea1-1473">결과 반환 하는 집합을 자주 있는 hello에 포함 되는 순서 toobe에 최소 점수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="a8ea1-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1474">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1475">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1475">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1476">apiVersion</span></span> |<span data-ttu-id="a8ea1-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1477">1.0</span></span> |

<span data-ttu-id="a8ea1-1478">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1478">**Response:**</span></span>

<span data-ttu-id="a8ea1-1479">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1480">hello 응답에는 권장된 항목 집합 (일반적으로 hello 초기값/입력 항목과 함께 구매 하는 항목 집합) 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="a8ea1-1481">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1482">`Feed\entry\content\properties\Id1` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1483">`Feed\entry\content\properties\Name1`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1484">`Feed\entry\content\properties\Id2` - 두 번째 권장된 항목 ID(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="a8ea1-1485">`Feed\entry\content\properties\Name2`-(선택 사항) hello 두 번째 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="a8ea1-1486">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1487">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1488">아래 예제 응답 hello 세 추천된 항목 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="a8ea1-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1489">OData XML</span></span>

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

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="a8ea1-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1490">12.4.</span></span> <span data-ttu-id="a8ea1-1491">FBT 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="a8ea1-1492">특정 빌드 유형 "Fbt"의 권장 사항 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="a8ea1-1493">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1493">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1494">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1495">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1496">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1497">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1497">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1498">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1499">modelId</span></span> |<span data-ttu-id="a8ea1-1500">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1501">itemId</span></span> |<span data-ttu-id="a8ea1-1502">에 대 한 항목 toorecommend 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="a8ea1-1503">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1503">Max length: 1024</span></span> |
| <span data-ttu-id="a8ea1-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1504">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1505">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1505">Number of required results</span></span> <br><span data-ttu-id="a8ea1-1506">최대: 150</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1506">Max: 150</span></span> |
| <span data-ttu-id="a8ea1-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1507">minimalScore</span></span> |<span data-ttu-id="a8ea1-1508">결과 반환 하는 집합을 자주 있는 hello에 포함 되는 순서 toobe에 최소 점수</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="a8ea1-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1509">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1510">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1510">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1511">buildId</span></span> |<span data-ttu-id="a8ea1-1512">hello이 권장 구성 요청에 대 한 id toouse 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a8ea1-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1513">apiVersion</span></span> |<span data-ttu-id="a8ea1-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1514">1.0</span></span> |

<span data-ttu-id="a8ea1-1515">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1515">**Response:**</span></span>

<span data-ttu-id="a8ea1-1516">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1517">hello 응답에는 권장된 항목 집합 (일반적으로 hello 초기값/입력 항목과 함께 구매 하는 항목 집합) 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="a8ea1-1518">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1519">`Feed\entry\content\properties\Id1` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1520">`Feed\entry\content\properties\Name1`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1521">`Feed\entry\content\properties\Id2` - 두 번째 권장된 항목 ID(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="a8ea1-1522">`Feed\entry\content\properties\Name2`-(선택 사항) hello 두 번째 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="a8ea1-1523">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1524">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1525">12.3의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="a8ea1-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1526">12.5.</span></span> <span data-ttu-id="a8ea1-1527">사용자 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="a8ea1-1528">빌드 형식이 활성 빌드로 표시된 "Recommendation"인 사용자 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="a8ea1-1529">hello API hello 사용자의 사용 현황 toohello에 따라 예측 된 항목의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="a8ea1-1530">참고:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1530">Notes:</span></span> 

1. <span data-ttu-id="a8ea1-1531">FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="a8ea1-1532">활성 hello 빌드 이면 FBT이이 메서드는 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="a8ea1-1533">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1533">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1534">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1535">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1536">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1537">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1537">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1538">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1539">modelId</span></span> |<span data-ttu-id="a8ea1-1540">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1541">userId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1541">userId</span></span> |<span data-ttu-id="a8ea1-1542">Hello 사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a8ea1-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1543">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1544">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1544">Number of required results</span></span> |
| <span data-ttu-id="a8ea1-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1545">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1546">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1546">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1547">apiVersion</span></span> |<span data-ttu-id="a8ea1-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1548">1.0</span></span> |

<span data-ttu-id="a8ea1-1549">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1549">**Response:**</span></span>

<span data-ttu-id="a8ea1-1550">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1551">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1552">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1553">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1554">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1555">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1556">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1557">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="a8ea1-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1558">12.6.</span></span> <span data-ttu-id="a8ea1-1559">항목 목록이 있는 사용자 권장 사항 가져오기(활성 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="a8ea1-1560">추가 항목 목록이 있으며 빌드 형식이 활성 빌드로 표시된 "Recommendation"인 사용자 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="a8ea1-1561">hello API hello 사용자 및 제공 된 항목을 추가로 hello toohello 현황에 따라 예측 된 항목의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="a8ea1-1562">참고:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1562">Notes:</span></span> 

1. <span data-ttu-id="a8ea1-1563">FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="a8ea1-1564">활성 hello 빌드 이면 FBT이이 메서드는 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="a8ea1-1565">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1565">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1566">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1567">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1568">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1569">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1569">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1570">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1571">modelId</span></span> |<span data-ttu-id="a8ea1-1572">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1573">userId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1573">userId</span></span> |<span data-ttu-id="a8ea1-1574">Hello 사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a8ea1-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1575">itemsIds</span></span> |<span data-ttu-id="a8ea1-1576">쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="a8ea1-1577">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1577">Max length: 1024</span></span> |
| <span data-ttu-id="a8ea1-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1578">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1579">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1579">Number of required results</span></span> |
| <span data-ttu-id="a8ea1-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1580">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1581">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1581">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1582">apiVersion</span></span> |<span data-ttu-id="a8ea1-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1583">1.0</span></span> |

<span data-ttu-id="a8ea1-1584">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1584">**Response:**</span></span>

<span data-ttu-id="a8ea1-1585">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1586">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1587">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1588">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1589">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1590">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1591">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1592">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="a8ea1-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1593">12.7.</span></span> <span data-ttu-id="a8ea1-1594">사용자 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="a8ea1-1595">특정 빌드 형식이 "Recommendation"인 사용자 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="a8ea1-1596">hello API hello 사용자 (hello 특정 빌드에 사용 됨)의 toohello 현황에 따라 예측 된 항목의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="a8ea1-1597">참고: FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="a8ea1-1598">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1598">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1599">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1600">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1601">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1602">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1602">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1603">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1604">modelId</span></span> |<span data-ttu-id="a8ea1-1605">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1606">userId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1606">userId</span></span> |<span data-ttu-id="a8ea1-1607">Hello 사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a8ea1-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1608">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1609">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1609">Number of required results</span></span> |
| <span data-ttu-id="a8ea1-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1610">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1611">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1611">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1612">buildId</span></span> |<span data-ttu-id="a8ea1-1613">hello이 권장 구성 요청에 대 한 id toouse 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a8ea1-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1614">apiVersion</span></span> |<span data-ttu-id="a8ea1-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1615">1.0</span></span> |

<span data-ttu-id="a8ea1-1616">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1616">**Response:**</span></span>

<span data-ttu-id="a8ea1-1617">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1618">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1619">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1620">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1621">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1622">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1623">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1624">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="a8ea1-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1625">12.8.</span></span> <span data-ttu-id="a8ea1-1626">항목 목록이 있는 사용자 권장 사항 가져오기(특정 빌드)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="a8ea1-1627">"권장" 형식의 특정 빌드의 사용자 권장 사항 및 추가 항목 hello 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="a8ea1-1628">hello API hello 사용자의 toohello 사용 기록 및 hello 항목의 추가 목록에 따라 예측 된 항목의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="a8ea1-1629">참고: FBT 빌드에 대한 사용자 권장 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="a8ea1-1630">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1630">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1631">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1632">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1633">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1634">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1634">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1635">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1636">modelId</span></span> |<span data-ttu-id="a8ea1-1637">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1638">userId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1638">userId</span></span> |<span data-ttu-id="a8ea1-1639">Hello 사용자의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a8ea1-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1640">itemIds</span></span> |<span data-ttu-id="a8ea1-1641">쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="a8ea1-1642">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1642">Max length: 1024</span></span> |
| <span data-ttu-id="a8ea1-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1643">numberOfResults</span></span> |<span data-ttu-id="a8ea1-1644">필요한 결과 수 </span><span class="sxs-lookup"><span data-stu-id="a8ea1-1644">Number of required results</span></span> |
| <span data-ttu-id="a8ea1-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1645">includeMetatadata</span></span> |<span data-ttu-id="a8ea1-1646">나중에 사용, 항상 false</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1646">Future use, always false</span></span> |
| <span data-ttu-id="a8ea1-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1647">buildId</span></span> |<span data-ttu-id="a8ea1-1648">hello이 권장 구성 요청에 대 한 id toouse 빌드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a8ea1-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1649">apiVersion</span></span> |<span data-ttu-id="a8ea1-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1650">1.0</span></span> |

<span data-ttu-id="a8ea1-1651">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1651">**Response:**</span></span>

<span data-ttu-id="a8ea1-1652">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1653">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1654">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1655">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1656">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1657">`Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a8ea1-1658">`Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a8ea1-1659">12.1의 응답 예제 참조</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="a8ea1-1660">13. 사용자 사용 기록</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1660">13. User Usage History</span></span>
<span data-ttu-id="a8ea1-1661">추천 모델 작성 되 면 hello 시스템 tooretrieve hello 사용자 기록 (항목 관련된 tooa 특정 사용자) hello 빌드에 사용 되는 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="a8ea1-1662">이 API는 tooretrieve hello 사용자 기록 허용</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="a8ea1-1663">참고: hello 사용자 기록은 권장 사항 빌드에 대해서만 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="a8ea1-1664">13.1 사용자 기록 검색</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="a8ea1-1665">활성 hello에 사용 되는 항목 검색 hello 목록을 빌드하거나 hello 지정 된 사용자 id를 지정 하는 hello에 대 한 빌드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="a8ea1-1666">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1666">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1667">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1668">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1668">GET</span></span> |<span data-ttu-id="a8ea1-1669">Hello 현재 빌드에 대 한 hello 사용자 기록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="a8ea1-1670">빌드를 제공 하는 hello에 대 한 hello 사용자 기록 가져오기`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="a8ea1-1671">예:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="a8ea1-1672">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1672">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1673">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1674">modelId</span></span> |<span data-ttu-id="a8ea1-1675">hello hello 모델의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="a8ea1-1676">userId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1676">userId</span></span> |<span data-ttu-id="a8ea1-1677">hello hello 사용자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="a8ea1-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1678">buildId</span></span> |<span data-ttu-id="a8ea1-1679">선택적 매개 변수에서 어떤 빌드에서 hello 사용자 기록 있어야 인출 tooindicate 허용</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="a8ea1-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1680">apiVersion</span></span> |<span data-ttu-id="a8ea1-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1681">1.0</span></span> |

<span data-ttu-id="a8ea1-1682">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1682">**Response:**</span></span>

<span data-ttu-id="a8ea1-1683">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1684">hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a8ea1-1685">각 항목에 같은 데이터가 hello:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="a8ea1-1686">`Feed\entry\content\properties\Id` - 권장된 항목 ID</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a8ea1-1687">`Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a8ea1-1688">`Feed\entry\content\properties\Rating` 해당 없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="a8ea1-1689">`Feed\entry\content\properties\Reasoning` 해당 없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="a8ea1-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1690">OData XML</span></span>

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

## <a name="14-notifications"></a><span data-ttu-id="a8ea1-1691">14. 알림</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1691">14. Notifications</span></span>
<span data-ttu-id="a8ea1-1692">Azure 시스템 학습 권장 사항 hello 시스템에서 영구 오류가 발생 하는 경우 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="a8ea1-1693">다음과 같은 세 가지 유형의 알림이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="a8ea1-1694">빌드 오류 – 이 알림은 모든 빌드 오류에 대해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="a8ea1-1695">오류-이 알림을 처리 하는 데이터 취득은 100 개 이상의 오류에에서 있는 hello hello 처리 모델에 대해 사용 이벤트의 최근 5 분 동안 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="a8ea1-1696">발생 한 경우 100 개 이상의 오류 hello에 모델에 대해 권장 요청의 hello 처리에서 마지막 5 분 권장 소비 실패-이 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="a8ea1-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1697">14.1.</span></span> <span data-ttu-id="a8ea1-1698">알림 가져오기</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1698">Get Notifications</span></span>
<span data-ttu-id="a8ea1-1699">모든 모델에 대 한 또는 단일 모델에 대 한 모든 hello 알림을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="a8ea1-1700">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1700">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1701">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1702">GET</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1703">모든 모델에 대한 모든 알림 가져오기:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1704">특정 모델에 대한 알림을 가져오는 예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="a8ea1-1705">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1705">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1706">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1707">modelId</span></span> |<span data-ttu-id="a8ea1-1708">선택적 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1708">Optional parameter.</span></span> <span data-ttu-id="a8ea1-1709">생략한 경우 모든 모델에 대한 모든 알림을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="a8ea1-1710">유효한 값: hello 모델의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="a8ea1-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1711">apiVersion</span></span> |<span data-ttu-id="a8ea1-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-1713">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1713">Request Body</span></span> |<span data-ttu-id="a8ea1-1714">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1714">NONE</span></span> |

<span data-ttu-id="a8ea1-1715">**응답:**</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1715">**Response:**</span></span>

<span data-ttu-id="a8ea1-1716">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="a8ea1-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
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

### <a name="142-delete-model-notifications"></a><span data-ttu-id="a8ea1-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1718">14.2.</span></span> <span data-ttu-id="a8ea1-1719">모델 알림 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1719">Delete Model Notifications</span></span>
<span data-ttu-id="a8ea1-1720">모델에 대한 읽은 알림을 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="a8ea1-1721">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1721">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1722">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1723">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a8ea1-1724">예제:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1725">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1725">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1726">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1727">modelId</span></span> |<span data-ttu-id="a8ea1-1728">Hello 모델의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a8ea1-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1729">apiVersion</span></span> |<span data-ttu-id="a8ea1-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-1731">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1731">Request Body</span></span> |<span data-ttu-id="a8ea1-1732">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1732">NONE</span></span> |

<span data-ttu-id="a8ea1-1733">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1733">**Response**:</span></span>

<span data-ttu-id="a8ea1-1734">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="a8ea1-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1735">14.3.</span></span> <span data-ttu-id="a8ea1-1736">사용자 알림 삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1736">Delete User Notifications</span></span>
<span data-ttu-id="a8ea1-1737">모든 모델에 대한 모든 알림을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="a8ea1-1738">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1738">HTTP Method</span></span> | <span data-ttu-id="a8ea1-1739">URI</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1740">삭제</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="a8ea1-1741">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1741">Parameter Name</span></span> | <span data-ttu-id="a8ea1-1742">유효한 값</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a8ea1-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1743">apiVersion</span></span> |<span data-ttu-id="a8ea1-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="a8ea1-1745">요청 본문</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1745">Request Body</span></span> |<span data-ttu-id="a8ea1-1746">없음</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1746">NONE</span></span> |

<span data-ttu-id="a8ea1-1747">**응답**:</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1747">**Response**:</span></span>

<span data-ttu-id="a8ea1-1748">HTTP 상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="a8ea1-1749">15. 법적 정보</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1749">15. Legal</span></span>
<span data-ttu-id="a8ea1-1750">이 문서는 "있는 그대로" 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="a8ea1-1751">URL 및 기타 인터넷 웹 사이트 참조를 포함하여 본 문서에 명시된 정보 및 보기는 통지 없이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="a8ea1-1752">여기에서 설명하는 일부 예는 설명 목적으로만 제공되는 가상의 예이며,</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="a8ea1-1753">어떠한 실제 사례와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="a8ea1-1754">이 문서에서는 있습니다 법적 권리도 tooany Microsoft 제품의 지적 재산입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="a8ea1-1755">이 문서는 내부 참조용으로만 복사 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="a8ea1-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="a8ea1-1757">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="a8ea1-1757">All rights reserved.</span></span>

