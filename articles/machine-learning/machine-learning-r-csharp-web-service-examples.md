---
title: "(사용되지 않음) R을 사용하여 작성한 Machine Learning 웹 서비스 예제 - Azure | Microsoft Docs"
description: "(사용되지 않음) R 코드와 Machine Learning을 사용하여 만든 후 Azure Marketplace에 게시한 유용한 웹 서비스 예제 집합을 찾아보세요."
keywords: "csharp, r 코드, 웹 서비스 예제"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="f57e5-104">(사용되지 않음) Azure Machine Learning의 R 코드를 사용하고 Microsoft Azure Marketplace에 게시된 웹 서비스 예제</span><span class="sxs-lookup"><span data-stu-id="f57e5-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="f57e5-105">Microsoft DataMarket은 종료되고 있는 중이며 이 API는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="f57e5-106">[Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com)에서 많은 유용한 예제 실험과 API를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f57e5-107">갤러리에 대한 자세한 내용은 [Cortana Intelligence 갤러리의 리소스 공유 및 검색](machine-learning-gallery-how-to-use-contribute-publish.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f57e5-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f57e5-108">이 문서에는 Azure 기계 학습을 사용하여 만든 다음 Azure 마켓플레이스에 게시된 예제 웹 서비스가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="f57e5-109">각 웹 서비스 예제에는 서비스를 테스트하고 사용자가 비슷한 서비스를 직접 만들 수 있는 방법을 설명하는 샘플 데이터 집합이 포함된 광범위한 문서가 첨부되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="f57e5-110">Azure 기계 학습 스튜디오에서 사용자는 R 코드를 작성한 후 몇 번의 클릭만으로 전 세계의 응용 프로그램과 장치에서 사용될 수 있는 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="f57e5-111">통계 기능을 제공하는 단순 계산 생성부터 사용자 지정 텍스트 마이닝 정서 분석 예측 변수 생성까지, 초보 사용자와 숙련된 사용자가 둘 다 Azure 기계 학습 사용자로서 간편하게 R 코드를 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="f57e5-112">이 웹 서비스를 사용자가 모바일 앱이나 웹 사이트를 통해 소비할 수 있지만 이 웹 서비스의 목적은 기계 학습에서 분석용으로 R 스크립트를 운영하고 R 코드 기반의 웹 서비스를 만드는 데 기계 학습을 사용하는 방법의 예로 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="f57e5-113">각 예제에는 웹 서비스 소비를 위한 C# 예제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-113">Each example includes a C# example for web service consumption.</span></span>

![Azure 기계 학습의 R 코드 다이어그램: 독자적으로 사용하거나 Azure 마켓플레이스에 게시하는 R 솔루션][1]

<span data-ttu-id="f57e5-115">다음과 같은 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f57e5-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="f57e5-116">시나리오 1: 일반 모델</span><span class="sxs-lookup"><span data-stu-id="f57e5-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="f57e5-117">사용자는 시계열 데이터의 기본 예측 또는 고급 분석을 통한 사용자 지정으로 작성된 R 메서드와 같이 새 사용자의 데이터에 적용할 수 있는 일반 모델을 사용하여 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="f57e5-118">이 사용자는 다른 사용자가 해당 데이터와 함께 소비하도록 모델을 웹 서비스로 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="f57e5-119">이진 분류자</span><span class="sxs-lookup"><span data-stu-id="f57e5-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="f57e5-120">클러스터 모델</span><span class="sxs-lookup"><span data-stu-id="f57e5-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="f57e5-121">다변량 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="f57e5-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="f57e5-122">예측 - 지수 평활법</span><span class="sxs-lookup"><span data-stu-id="f57e5-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="f57e5-123">EETS + STL 예측</span><span class="sxs-lookup"><span data-stu-id="f57e5-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="f57e5-124">예측 - ARIMA(자동 회귀 통합 이동 평균)</span><span class="sxs-lookup"><span data-stu-id="f57e5-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="f57e5-125">생존 분석</span><span class="sxs-lookup"><span data-stu-id="f57e5-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="f57e5-126">시나리오 2: 학습된 모델 – 특정 데이터</span><span class="sxs-lookup"><span data-stu-id="f57e5-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="f57e5-127">사용자의 성격 유형을 예측하기 위한 k-means 알고리즘을 통해 클러스터된 성격 질문서의 큰 샘플 또는 생존 분석 R 패키지를 통해 개인의 위암에 대한 위험을 예측하는 데 사용할 수 있는 건강 설문 데이터와 같이 R 코드를 통해 유용한 예측을 제공하는 데이터가 사용자에게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="f57e5-128">사용자는 새 사용자의 결과를 예측하는 웹 서비스를 통해 데이터를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="f57e5-129">시나리오 3: 학습된 모델 – 일반 데이터</span><span class="sxs-lookup"><span data-stu-id="f57e5-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="f57e5-130">일반적으로 웹 서비스를 작성한 후 다양한 유형의 사용 사례와 시나리오에서 적용할 수 있는 일반 데이터(예: 텍스트 모음)가 사용자에게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="f57e5-131">어휘집 기반 감정 분석</span><span class="sxs-lookup"><span data-stu-id="f57e5-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="f57e5-132">시나리오 4: 고급 계산기</span><span class="sxs-lookup"><span data-stu-id="f57e5-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="f57e5-133">사용자는 고급 계산 또는 시뮬레이션을 제공하므로 학습된 모델이 필요하지 않고 모델을 사용자 데이터에 맞출 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f57e5-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="f57e5-134">비율 차이 테스트</span><span class="sxs-lookup"><span data-stu-id="f57e5-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="f57e5-135">정규 분포 제품군</span><span class="sxs-lookup"><span data-stu-id="f57e5-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="f57e5-136">이항 분포 패키지</span><span class="sxs-lookup"><span data-stu-id="f57e5-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="f57e5-137">FAQ</span><span class="sxs-lookup"><span data-stu-id="f57e5-137">FAQ</span></span>
<span data-ttu-id="f57e5-138">웹 서비스 사용 또는 마켓플레이스 게시 방법과 관련한 질문과 대답은 [여기](machine-learning-marketplace-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f57e5-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



