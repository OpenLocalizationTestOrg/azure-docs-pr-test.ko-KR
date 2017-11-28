---
title: "hello 컴퓨터 학습 권장 사항을 API에서에서 aaaCommon 작업 | Microsoft Docs"
description: "Azure ML 권장 사항 샘플 응용 프로그램"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
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
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a><span data-ttu-id="c32d2-103">권장 사항 API 응용 프로그램 예제 연습</span><span class="sxs-lookup"><span data-stu-id="c32d2-103">Recommendations API Sample Application Walkthrough</span></span>
> [!NOTE]
> <span data-ttu-id="c32d2-104">이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="c32d2-105">hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="c32d2-106">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="c32d2-107">에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="c32d2-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

## <a name="purpose"></a><span data-ttu-id="c32d2-108">목적</span><span class="sxs-lookup"><span data-stu-id="c32d2-108">Purpose</span></span>
<span data-ttu-id="c32d2-109">이 문서에서는 Azure 시스템 학습 권장 사항 API를 통해 hello의 hello 사용 표시는 [샘플 응용 프로그램](https://code.msdn.microsoft.com/Recommendations-144df403)합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-109">This document shows hello usage of hello Azure Machine Learning Recommendations API via a [sample application](https://code.msdn.microsoft.com/Recommendations-144df403).</span></span>

<span data-ttu-id="c32d2-110">이 응용 프로그램은 의도 한 tooinclude 전체 기능을 하지도 모든 hello Api 사용.</span><span class="sxs-lookup"><span data-stu-id="c32d2-110">This application is not intended tooinclude full functionality, nor does it use all hello APIs.</span></span> <span data-ttu-id="c32d2-111">기계 학습 권장 서비스가 hello로 tooplay 먼저 하려는 경우 몇 가지 일반적인 작업 tooperform를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-111">It demonstrates some common operations tooperform when you first want tooplay with hello Machine Learning recommendation service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a><span data-ttu-id="c32d2-112">소개 tooMachine 학습 권장 구성 서비스</span><span class="sxs-lookup"><span data-stu-id="c32d2-112">Introduction tooMachine Learning recommendation service</span></span>
<span data-ttu-id="c32d2-113">Hello 기계 학습 권장 서비스를 통해 권장 사항 hello 다음 데이터를 기반으로 추천 모델을 빌드할 때 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-113">Recommendations via hello Machine Learning recommendation service are enabled when you build a recommendation model based on hello following data:</span></span>

* <span data-ttu-id="c32d2-114">카탈로그 라고도 toorecommend hello 항목의 저장소</span><span class="sxs-lookup"><span data-stu-id="c32d2-114">A repository of hello items you want toorecommend, also known as a catalog</span></span>
* <span data-ttu-id="c32d2-115">사용자 또는 세션 (이 얻을 수 hello 샘플 응용 프로그램의 일부가 아니라 데이터 취득 통해 시간이 지남에 따라) 당 항목 hello 사용을 나타내는 데이터</span><span class="sxs-lookup"><span data-stu-id="c32d2-115">Data representing hello usage of items per user or session (this can be acquired over time via data acquisition, not as part of hello sample app)</span></span>

<span data-ttu-id="c32d2-116">추천 모델을 작성 한 후 사용할 수 있습니다는 사용자에 관심을 가질 수 있는 toopredict 항목 따라 tooa 일련의 항목 (또는 단일 항목) hello 사용자가 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-116">After a recommendation model is built, you can use it toopredict items that a user might be interested in, according tooa set of items (or a single item) hello user selects.</span></span>

<span data-ttu-id="c32d2-117">tooenable hello 이전 시나리오에서 hello 다음 기계 학습 권장 서비스가 hello:</span><span class="sxs-lookup"><span data-stu-id="c32d2-117">tooenable hello previous scenario, do hello following in hello Machine Learning recommendation service:</span></span>

* <span data-ttu-id="c32d2-118">모델을 만듭니다:이 hello 데이터 (카탈로그 및 사용) 및 hello 예측 모델을 보관 하는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-118">Create a model: This is a logical container that holds hello data (catalog and usage) and hello prediction model(s).</span></span> <span data-ttu-id="c32d2-119">각 모델 컨테이너는 생성 시 할당되는 고유 ID를 통해 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-119">Each model container is identified via a unique ID, which is allocated when it is created.</span></span> <span data-ttu-id="c32d2-120">이 ID는 hello 모델 ID 라고 하 고 대부분의 hello Api에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-120">This ID is called hello model ID, and it is used by most of hello APIs.</span></span> 
* <span data-ttu-id="c32d2-121">Toocatalog 업로드: 모델 컨테이너를 만들면 tooit 카탈로그를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-121">Upload toocatalog: When a model container is created, you can associate tooit a catalog.</span></span>

<span data-ttu-id="c32d2-122">**참고**: 모델 만들기 및 업로드 tooa 카탈로그는 일반적으로 한 번 수행 hello 모델 수명 주기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-122">**Note**: Creating a model and uploading tooa catalog are usually performed once for hello model lifecycle.</span></span>

* <span data-ttu-id="c32d2-123">사용 현황 업로드: 이렇게 하면 사용 현황 데이터 toohello 모델 컨테이너를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-123">Upload usage: This adds usage data toohello model container.</span></span>
* <span data-ttu-id="c32d2-124">추천 모델을 빌드: 충분 한 데이터를 설정한 후에 hello 추천 모델을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-124">Build a recommendation model: After you have enough data, you can build hello recommendation model.</span></span> <span data-ttu-id="c32d2-125">이 작업 hello 상위 기계 학습 알고리즘 toocreate 추천 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-125">This operation uses hello top Machine Learning algorithms toocreate a recommendation model.</span></span> <span data-ttu-id="c32d2-126">각 빌드는 고유 ID와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-126">Each build is associated with a unique ID.</span></span> <span data-ttu-id="c32d2-127">일부 Api의 hello 기능에 필요한 있기 때문에이 ID에 대 한 기록을 tookeep을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-127">You need tookeep a record of this ID because it is necessary for hello functionality of some APIs.</span></span>
* <span data-ttu-id="c32d2-128">빌드 프로세스 모니터 hello: 추천 모델 빌드는 비동기 작업을 하 고 hello 양의 데이터 (카탈로그 및 사용)에 따라 몇 분 tooseveral 시간에서 수행 하 고 hello 빌드 매개 변수 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-128">Monitor hello building process: A recommendation model build is an asynchronous operation, and it can take from several minutes tooseveral hours, depending on hello amount of data (catalog and usage) and hello build parameters.</span></span> <span data-ttu-id="c32d2-129">따라서 toomonitor hello 빌드를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-129">Therefore, you need toomonitor hello build.</span></span> <span data-ttu-id="c32d2-130">연결된 해당 빌드가 성공적으로 완료되는 경우에만 권장 사항 모델이 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-130">A recommendation model is created only if its associated build completes successfully.</span></span>
* <span data-ttu-id="c32d2-131">(선택 사항) 활성 권장 사항 모델 빌드 선택: 이 단계는 모델 컨테이너에서 권장 사항 모델이 두 개 이상 빌드된 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-131">(Optional) Choose an active recommendation model build: This step is only necessary if you have more than one recommendation model built in your model container.</span></span> <span data-ttu-id="c32d2-132">Hello 활성 추천 모델을 표시 하지 않고 요청 tooget 권장 사항을 hello 시스템 toohello 기본 현재 빌드에 의해 자동으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-132">Any request tooget recommendations without indicating hello active recommendation model is redirected automatically by hello system toohello default active build.</span></span> 

<span data-ttu-id="c32d2-133">**참고**: 활성 권장 사항 모델은 프로덕션 환경에서 바로 사용할 수 있으며 프로덕션 작업을 위해 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-133">**Note**: An active recommendation model is production ready and it is built for production workload.</span></span> <span data-ttu-id="c32d2-134">테스트와 비슷한 환경(스테이징 환경이라고도 함)에 머무르는 비활성 권장 사항 모델과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-134">This differs from a non-active recommendation model, which stays in a test-like environment (sometimes called staging).</span></span>

* <span data-ttu-id="c32d2-135">권장 사항 가져오기: 권장 사항 모델이 있으면 선택한 단일 항목 또는 항목 목록에 대한 권장 사항을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-135">Get recommendations: After you have a recommendation model, you can trigger recommendations for a single item or a list of items that you select.</span></span> 

<span data-ttu-id="c32d2-136">일반적으로 특정 기간에 대해 Get Recommendation을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-136">You will usually invoke Get Recommendation for a certain period of time.</span></span> <span data-ttu-id="c32d2-137">해당 시간 기간 동안 사용 현황 데이터 toohello이 데이터 toohello 지정된 모델 컨테이너를 추가 하는 기계 학습 추천 시스템을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-137">During that period of time, you can redirect usage data toohello Machine Learning recommendation system, which adds this data toohello specified model container.</span></span> <span data-ttu-id="c32d2-138">충분 한 사용 현황 데이터를 있으면 hello 추가 사용 현황 데이터를 통합 하는 새 추천 모델을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-138">When you have enough usage data, you can build a new recommendation model that incorporates hello additional usage data.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c32d2-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c32d2-139">Prerequisites</span></span>
* <span data-ttu-id="c32d2-140">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="c32d2-140">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="c32d2-141">인터넷 액세스</span><span class="sxs-lookup"><span data-stu-id="c32d2-141">Internet access</span></span> 
* <span data-ttu-id="c32d2-142">구독 toohello 권장 사항을 API (https://datamarket.azure.com/dataset/amla/recommendations)입니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-142">Subscription toohello Recommendations API (https://datamarket.azure.com/dataset/amla/recommendations).</span></span>

## <a name="azure-machine-learning-sample-app-solution"></a><span data-ttu-id="c32d2-143">Azure 기계 학습 샘플 앱 솔루션</span><span class="sxs-lookup"><span data-stu-id="c32d2-143">Azure Machine Learning sample app solution</span></span>
<span data-ttu-id="c32d2-144">이 솔루션 hello 소스 코드, 사용법 예제, 카탈로그 파일 및 컴파일에 필요한 지시문 toodownload hello 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-144">This solution contains hello source code, sample usage, catalog file, and directives toodownload hello packages that are required for compilation.</span></span>

## <a name="hello-apis-used"></a><span data-ttu-id="c32d2-145">hello 사용 되는 Api</span><span class="sxs-lookup"><span data-stu-id="c32d2-145">hello APIs used</span></span>
<span data-ttu-id="c32d2-146">hello 응용 프로그램에서는 사용 가능한 Api의 하위 집합을 통해 기계 학습 권장 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-146">hello application uses Machine Learning recommendation functionality via a subset of available APIs.</span></span> <span data-ttu-id="c32d2-147">다음 Api hello 응용 프로그램에서 보여지는 hello:</span><span class="sxs-lookup"><span data-stu-id="c32d2-147">hello following APIs are demonstrated in hello application:</span></span>

* <span data-ttu-id="c32d2-148">모델을 만들: 논리적 컨테이너 toohold 데이터와 권장 사항 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-148">Create model: Create a logical container toohold data and recommendation models.</span></span> <span data-ttu-id="c32d2-149">모델은 한 이름으로 식별 되 고 hello로 하나 이상의 모델을 만들 수 없습니다 동일한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-149">A model is identified by a name, and you  cannot create more than one model with hello same name.</span></span>
* <span data-ttu-id="c32d2-150">카탈로그 파일을 업로드: tooupload 카탈로그 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-150">Upload catalog file: Use tooupload catalog data.</span></span>
* <span data-ttu-id="c32d2-151">사용 현황 파일 업로드: tooupload 사용 현황 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-151">Upload usage file: Use tooupload usage data.</span></span>
* <span data-ttu-id="c32d2-152">빌드를 트리거: toocreate 추천 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-152">Trigger build: Use toocreate a recommendation model.</span></span>
* <span data-ttu-id="c32d2-153">빌드 실행을 모니터링할: toomonitor hello에서는 추천 모델 빌드 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-153">Monitor build execution: Use toomonitor hello status of a recommendation model build.</span></span>
* <span data-ttu-id="c32d2-154">권장 사항이 작성 된 모델 선택: tooindicate는 추천 모델 toouse를 기본적으로 사용 특정 모델 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-154">Choose a built model for recommendation: Use tooindicate which recommendation model toouse by default for a certain model container.</span></span> <span data-ttu-id="c32d2-155">이 단계는 추천 모델을 여러 개 있고 tooactivate 활성이 아닌 hello 활성 추천 모델을 빌드 하려는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-155">This step is necessary only if you have more than one recommendation model and you want tooactivate a non-active build as hello active recommendation model.</span></span>
* <span data-ttu-id="c32d2-156">권장 메시지가: tooretrieve 추천 tooa 지정 된 단일 항목 또는 항목 집합에 따라 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-156">Get recommendation: Use tooretrieve recommended items according tooa given single item or a set of items.</span></span> 

<span data-ttu-id="c32d2-157">에 대 한 전체 설명은 hello Api, hello Microsoft Azure Marketplace 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c32d2-157">For a complete description of hello APIs, please see hello Microsoft Azure Marketplace documentation.</span></span> 

<span data-ttu-id="c32d2-158">**참고**: 시간이 지나면(동시는 아님) 모델 빌드가 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-158">**Note**: A model can have several builds over time (not simultaneously).</span></span> <span data-ttu-id="c32d2-159">각 빌드를 동일한 또는 업데이트 된 hello로 만든 카탈로그 및 추가 사용 현황 데이터.</span><span class="sxs-lookup"><span data-stu-id="c32d2-159">Each build is created with hello same or an updated catalog and additional usage data.</span></span>

## <a name="common-pitfalls"></a><span data-ttu-id="c32d2-160">공통 문제</span><span class="sxs-lookup"><span data-stu-id="c32d2-160">Common pitfalls</span></span>
* <span data-ttu-id="c32d2-161">사용자 이름 및 Microsoft Azure Marketplace 기본 계정 키 toorun hello 샘플 앱 tooprovide 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-161">You need tooprovide your user name and your Microsoft Azure Marketplace primary account key toorun hello sample app.</span></span>
* <span data-ttu-id="c32d2-162">연속적으로 실행 중인 hello에 대 한 샘플 응용 프로그램 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-162">Running hello sample app consecutively will fail.</span></span> <span data-ttu-id="c32d2-163">hello 응용 프로그램 흐름 만들고 업로드 hello 모니터를 구축 하 고, 미리 정의 된 모델에서 권장 구성을 가져오는 포함 됩니다. 따라서 호출 사이의 hello 모델 이름을 변경 하지 않는 경우 연속 실행에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-163">hello application flow includes creating, uploading, building hello monitor, and getting recommendations from a predefined model; therefore, it will fail on consecutive execution if you do not change hello model name between invocations.</span></span>
* <span data-ttu-id="c32d2-164">데이터 없이 권장 사항이 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-164">Recommendations might return without data.</span></span> <span data-ttu-id="c32d2-165">hello 샘플 응용 프로그램에는 매우 작은 카탈로그 및 사용 현황 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-165">hello sample app uses a very small catalog and usage file.</span></span> <span data-ttu-id="c32d2-166">따라서 hello 카탈로그에서 일부 항목 권장된 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-166">Therefore, some items from hello catalog will have no recommended items.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="c32d2-167">고지 사항</span><span class="sxs-lookup"><span data-stu-id="c32d2-167">Disclaimer</span></span>
<span data-ttu-id="c32d2-168">hello 샘플 응용 프로그램을 프로덕션 환경에서 실행 되는 의도 된 toobe 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-168">hello sample app is not intended toobe run in a production environment.</span></span> <span data-ttu-id="c32d2-169">매우 작은 hello 카탈로그에서 제공 하는 hello 데이터 이며 의미 있는 추천 모델을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-169">hello data provided in hello catalog is very small, and it will not provide a meaningful recommendation model.</span></span> <span data-ttu-id="c32d2-170">hello 데이터 데모로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c32d2-170">hello data is provided as a demonstration.</span></span> 

