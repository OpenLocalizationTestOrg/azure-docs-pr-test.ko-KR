---
title: "Machine Learning 권장 사항 API의 공통 작업 | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 8d8efa93e820f4a745ed93c0f4d13b2438dfa1eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a><span data-ttu-id="a7484-103">권장 사항 API 응용 프로그램 예제 연습</span><span class="sxs-lookup"><span data-stu-id="a7484-103">Recommendations API Sample Application Walkthrough</span></span>
> [!NOTE]
> <span data-ttu-id="a7484-104">이 버전 대신 Recommendations API Cognitive 서비스를 사용하기 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="a7484-105">Recommendations Cognitive 서비스가 이 서비스를 대체하게 되며, 모든 새로운 기능이 여기에서 개발됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="a7484-106">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="a7484-107">[새로운 Cognitive 서비스로 마이그레이션](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="a7484-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

## <a name="purpose"></a><span data-ttu-id="a7484-108">목적</span><span class="sxs-lookup"><span data-stu-id="a7484-108">Purpose</span></span>
<span data-ttu-id="a7484-109">이 문서에서는 [샘플 응용 프로그램](https://code.msdn.microsoft.com/Recommendations-144df403)을 통해 Azure 기계 학습 권장 사항 API의 사용법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-109">This document shows the usage of the Azure Machine Learning Recommendations API via a [sample application](https://code.msdn.microsoft.com/Recommendations-144df403).</span></span>

<span data-ttu-id="a7484-110">이 응용 프로그램은 일부 기능만 포함하고 있으며 일부 API만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-110">This application is not intended to include full functionality, nor does it use all the APIs.</span></span> <span data-ttu-id="a7484-111">기계 학습 권장 서비스를 처음 시작할 때 수행할 일반적인 작업 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-111">It demonstrates some common operations to perform when you first want to play with the Machine Learning recommendation service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-to-machine-learning-recommendation-service"></a><span data-ttu-id="a7484-112">기계 학습 권장 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="a7484-112">Introduction to Machine Learning recommendation service</span></span>
<span data-ttu-id="a7484-113">다음 데이터를 기반으로 권장 사항 모델을 빌드할 때 기계 학습 권장 사항 서비스를 통해 권장 사항이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-113">Recommendations via the Machine Learning recommendation service are enabled when you build a recommendation model based on the following data:</span></span>

* <span data-ttu-id="a7484-114">권장하려는 항목의 리포지토리(카탈로그라고도 함)</span><span class="sxs-lookup"><span data-stu-id="a7484-114">A repository of the items you want to recommend, also known as a catalog</span></span>
* <span data-ttu-id="a7484-115">사용자 또는 세션당 항목 사용을 나타내는 데이터(샘플 앱의 일부가 아니라 데이터 취득을 통해 시간이 지남에 따라 취득 가능)</span><span class="sxs-lookup"><span data-stu-id="a7484-115">Data representing the usage of items per user or session (this can be acquired over time via data acquisition, not as part of the sample app)</span></span>

<span data-ttu-id="a7484-116">권장 사항 모델이 작성되면 이 모델을 사용하여 선택한 항목 집합(또는 단일 항목)에 따라 사용자가 관심을 가질 만한 항목을 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-116">After a recommendation model is built, you can use it to predict items that a user might be interested in, according to a set of items (or a single item) the user selects.</span></span>

<span data-ttu-id="a7484-117">이전 시나리오를 지원하려면 기계 학습 권장 서비스에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-117">To enable the previous scenario, do the following in the Machine Learning recommendation service:</span></span>

* <span data-ttu-id="a7484-118">모델 만들기: 데이터(카탈로그 및 사용 현황) 및 예측 모델을 보관하는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-118">Create a model: This is a logical container that holds the data (catalog and usage) and the prediction model(s).</span></span> <span data-ttu-id="a7484-119">각 모델 컨테이너는 생성 시 할당되는 고유 ID를 통해 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-119">Each model container is identified via a unique ID, which is allocated when it is created.</span></span> <span data-ttu-id="a7484-120">이 ID를 모델 ID라고 하며 대부분의 API에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-120">This ID is called the model ID, and it is used by most of the APIs.</span></span> 
* <span data-ttu-id="a7484-121">카탈로그 업로드: 모델 컨테이너를 만든 후에 카탈로그에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-121">Upload to catalog: When a model container is created, you can associate to it a catalog.</span></span>

<span data-ttu-id="a7484-122">**참고**: 모델 만들기 및 카탈로그 업로드는 일반적으로 모델 수명 주기 동안 한 번 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-122">**Note**: Creating a model and uploading to a catalog are usually performed once for the model lifecycle.</span></span>

* <span data-ttu-id="a7484-123">사용 현황 업로드: 모델 컨테이너에 사용 현황 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-123">Upload usage: This adds usage data to the model container.</span></span>
* <span data-ttu-id="a7484-124">권장 사항 모델 작성: 데이터가 충분히 모이면 권장 사항 모델을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-124">Build a recommendation model: After you have enough data, you can build the recommendation model.</span></span> <span data-ttu-id="a7484-125">이 작업에서는 최신 기계 학습 알고리즘을 사용하여 권장 사항 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-125">This operation uses the top Machine Learning algorithms to create a recommendation model.</span></span> <span data-ttu-id="a7484-126">각 빌드는 고유 ID와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-126">Each build is associated with a unique ID.</span></span> <span data-ttu-id="a7484-127">일부 API 기능을 사용하려면 이 ID가 필요하므로 이 ID를 기록해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-127">You need to keep a record of this ID because it is necessary for the functionality of some APIs.</span></span>
* <span data-ttu-id="a7484-128">빌드 프로세스 모니터링: 권장 사항 모델 빌드는 비동기 작업이고 데이터(카탈로그 및 사용) 크기 및 빌드 매개 변수에 따라 몇 분에서 몇 시간까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-128">Monitor the building process: A recommendation model build is an asynchronous operation, and it can take from several minutes to several hours, depending on the amount of data (catalog and usage) and the build parameters.</span></span> <span data-ttu-id="a7484-129">따라서 빌드를 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-129">Therefore, you need to monitor the build.</span></span> <span data-ttu-id="a7484-130">연결된 해당 빌드가 성공적으로 완료되는 경우에만 권장 사항 모델이 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-130">A recommendation model is created only if its associated build completes successfully.</span></span>
* <span data-ttu-id="a7484-131">(선택 사항) 활성 권장 사항 모델 빌드 선택: 이 단계는 모델 컨테이너에서 권장 사항 모델이 두 개 이상 빌드된 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-131">(Optional) Choose an active recommendation model build: This step is only necessary if you have more than one recommendation model built in your model container.</span></span> <span data-ttu-id="a7484-132">활성 권장 사항 모델을 지정하지 않고 권장 사항을 가져오는 모든 요청은 자동으로 기본 활성 빌드로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-132">Any request to get recommendations without indicating the active recommendation model is redirected automatically by the system to the default active build.</span></span> 

<span data-ttu-id="a7484-133">**참고**: 활성 권장 사항 모델은 프로덕션 환경에서 바로 사용할 수 있으며 프로덕션 작업을 위해 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-133">**Note**: An active recommendation model is production ready and it is built for production workload.</span></span> <span data-ttu-id="a7484-134">테스트와 비슷한 환경(스테이징 환경이라고도 함)에 머무르는 비활성 권장 사항 모델과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-134">This differs from a non-active recommendation model, which stays in a test-like environment (sometimes called staging).</span></span>

* <span data-ttu-id="a7484-135">권장 사항 가져오기: 권장 사항 모델이 있으면 선택한 단일 항목 또는 항목 목록에 대한 권장 사항을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-135">Get recommendations: After you have a recommendation model, you can trigger recommendations for a single item or a list of items that you select.</span></span> 

<span data-ttu-id="a7484-136">일반적으로 특정 기간에 대해 Get Recommendation을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-136">You will usually invoke Get Recommendation for a certain period of time.</span></span> <span data-ttu-id="a7484-137">해당 기간 동안 사용 현황 데이터를 기계 학습 권장 시스템으로 리디렉션할 수 있으며, 이 경우 지정된 모델 컨테이너에 이 데이터가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-137">During that period of time, you can redirect usage data to the Machine Learning recommendation system, which adds this data to the specified model container.</span></span> <span data-ttu-id="a7484-138">사용 현황 데이터가 충분히 모였으면 추가 사용 현황 데이터를 통합하는 새 권장 사항 모델을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-138">When you have enough usage data, you can build a new recommendation model that incorporates the additional usage data.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a7484-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a7484-139">Prerequisites</span></span>
* <span data-ttu-id="a7484-140">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="a7484-140">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="a7484-141">인터넷 액세스</span><span class="sxs-lookup"><span data-stu-id="a7484-141">Internet access</span></span> 
* <span data-ttu-id="a7484-142">권장 사항 API에 대한 구독입니다(https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="a7484-142">Subscription to the Recommendations API (https://datamarket.azure.com/dataset/amla/recommendations).</span></span>

## <a name="azure-machine-learning-sample-app-solution"></a><span data-ttu-id="a7484-143">Azure 기계 학습 샘플 앱 솔루션</span><span class="sxs-lookup"><span data-stu-id="a7484-143">Azure Machine Learning sample app solution</span></span>
<span data-ttu-id="a7484-144">이 솔루션에는 소스 코드, 샘플 사용법, 카탈로그 파일 및 컴파일에 필요한 Nuget 패키지를 다운로드하는 지시문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-144">This solution contains the source code, sample usage, catalog file, and directives to download the packages that are required for compilation.</span></span>

## <a name="the-apis-used"></a><span data-ttu-id="a7484-145">사용되는 API</span><span class="sxs-lookup"><span data-stu-id="a7484-145">The APIs used</span></span>
<span data-ttu-id="a7484-146">응용 프로그램에서는 사용 가능한 API의 하위 집합을 통해 기계 학습 권장 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-146">The application uses Machine Learning recommendation functionality via a subset of available APIs.</span></span> <span data-ttu-id="a7484-147">다음 API는 응용 프로그램으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-147">The following APIs are demonstrated in the application:</span></span>

* <span data-ttu-id="a7484-148">모델 만들기: 데이터 및 권장 사항 모델을 포함하는 논리 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-148">Create model: Create a logical container to hold data and recommendation models.</span></span> <span data-ttu-id="a7484-149">모델은 이름으로 식별되고, 이름이 같은 모델을 여러 개 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-149">A model is identified by a name, and you  cannot create more than one model with the same name.</span></span>
* <span data-ttu-id="a7484-150">카탈로그 파일 업로드: 카탈로그 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-150">Upload catalog file: Use to upload catalog data.</span></span>
* <span data-ttu-id="a7484-151">사용 현황 파일 업로드: 사용 현황 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-151">Upload usage file: Use to upload usage data.</span></span>
* <span data-ttu-id="a7484-152">빌드 트리거: 권장 사항 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-152">Trigger build: Use to create a recommendation model.</span></span>
* <span data-ttu-id="a7484-153">빌드 실행 모니터링: 권장 사항 모델 빌드의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-153">Monitor build execution: Use to monitor the status of a recommendation model build.</span></span>
* <span data-ttu-id="a7484-154">빌드된 권장 사항 모델 선택: 특정 모델 컨테이너에 대해 기본적으로 사용할 권장 사항 모델을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-154">Choose a built model for recommendation: Use to indicate which recommendation model to use by default for a certain model container.</span></span> <span data-ttu-id="a7484-155">이 단계는 둘 이상의 권장 사항 모델이 있고 비활성 빌드를 활성 권장 사항 모델로 활성화하려는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-155">This step is necessary only if you have more than one recommendation model and you want to activate a non-active build as the active recommendation model.</span></span>
* <span data-ttu-id="a7484-156">권장 사항 가져오기: 제공된 단일 항목 또는 항목 집합에 따라 권장 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-156">Get recommendation: Use to retrieve recommended items according to a given single item or a set of items.</span></span> 

<span data-ttu-id="a7484-157">API에 대한 자세한 내용은 Microsoft Azure 마켓플레이스 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7484-157">For a complete description of the APIs, please see the Microsoft Azure Marketplace documentation.</span></span> 

<span data-ttu-id="a7484-158">**참고**: 시간이 지나면(동시는 아님) 모델 빌드가 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-158">**Note**: A model can have several builds over time (not simultaneously).</span></span> <span data-ttu-id="a7484-159">각 빌드는 기존과 동일한 또는 업데이트된 카탈로그 및 추가 사용 현황 데이터를 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-159">Each build is created with the same or an updated catalog and additional usage data.</span></span>

## <a name="common-pitfalls"></a><span data-ttu-id="a7484-160">공통 문제</span><span class="sxs-lookup"><span data-stu-id="a7484-160">Common pitfalls</span></span>
* <span data-ttu-id="a7484-161">샘플 앱을 실행하려면 사용자 이름 및 Microsoft Azure 마켓플레이스 기본 계정 키를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-161">You need to provide your user name and your Microsoft Azure Marketplace primary account key to run the sample app.</span></span>
* <span data-ttu-id="a7484-162">샘플 앱을 연속해서 실행하면 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-162">Running the sample app consecutively will fail.</span></span> <span data-ttu-id="a7484-163">응용 프로그램은 모니터 생성, 모니터 업로드, 모니터 빌드, 미리 정의된 모델에서 권장 사항 가져오기로 진행되므로 호출 간에 모델 이름을 변경하지 않으면 연속으로 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-163">The application flow includes creating, uploading, building the monitor, and getting recommendations from a predefined model; therefore, it will fail on consecutive execution if you do not change the model name between invocations.</span></span>
* <span data-ttu-id="a7484-164">데이터 없이 권장 사항이 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-164">Recommendations might return without data.</span></span> <span data-ttu-id="a7484-165">샘플 앱에서는 아주 작은 카탈로그 및 사용 현황 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-165">The sample app uses a very small catalog and usage file.</span></span> <span data-ttu-id="a7484-166">따라서, 카탈로그의 일부 항목에는 권장 항목이 없을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-166">Therefore, some items from the catalog will have no recommended items.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="a7484-167">고지 사항</span><span class="sxs-lookup"><span data-stu-id="a7484-167">Disclaimer</span></span>
<span data-ttu-id="a7484-168">샘플 앱은 프로덕션 환경에서 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-168">The sample app is not intended to be run in a production environment.</span></span> <span data-ttu-id="a7484-169">카탈로그에 제공되는 데이터가 매우 작기 때문에 의미 있는 권장 사항 모델을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-169">The data provided in the catalog is very small, and it will not provide a meaningful recommendation model.</span></span> <span data-ttu-id="a7484-170">제공되는 데이터는 시연용입니다.</span><span class="sxs-lookup"><span data-stu-id="a7484-170">The data is provided as a demonstration.</span></span> 

