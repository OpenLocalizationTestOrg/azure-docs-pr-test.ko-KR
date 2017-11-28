---
title: "aaa(deprecated) 컴퓨터 학습 웹 서비스 예제 R-Azure 사용 하 여 빌드한 | Microsoft Docs"
description: "(사용 되지 않음) 웹 서비스 예제에서는 유용한 R 코드 및 기계 학습을 사용 하 여 만든 및 toohello Azure 마켓플레이스에서 게시 찾습니다."
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="de3c3-104">(사용 되지 않음) 웹 서비스는 Azure 기계 학습 및 게시 된 tooMicrosoft Azure Marketplace에서 R 코드를 사용 하는 예제</span><span class="sxs-lookup"><span data-stu-id="de3c3-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="de3c3-105">Microsoft DataMarket hello 사용 중지 됩니다 하 고 이러한 Api가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="de3c3-106">Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="de3c3-107">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="de3c3-108">이 문서에는 예제 웹 서비스는 Azure 기계 학습을 사용 하 여 만든 및 toohello Azure 마켓플레이스에서 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="de3c3-109">각 웹 서비스 예제에는 전체 문서는 연결을 위해 hello 서비스를 테스트 하 고 어떻게 hello 사용자 직접 만들 수 있습니다 유사한 서비스를 설명 하는 샘플 데이터 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="de3c3-110">Azure 기계 학습 스튜디오에서 사용자가 R 코드를 작성 하 고 몇 번의 클릭으로 hello 전 세계 tooconsume 응용 프로그램 및 장치에 대 한 웹 서비스로 게시할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="de3c3-111">사용자 지정 텍스트 마이닝 감성 분석 예측자 toocreating 통계 기능을 제공 하는 간단한 계산기를 생성, 신규 및 경력 전화 R 사용자는 사용자가 Azure 기계 학습의 R을 운용 수 있습니다. hello 용이성에서 얻을 수합니다 있습니다. 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="de3c3-112">모바일 앱 또는 웹 사이트를 통해 잠재적으로 사용자가 해당 웹 서비스를 소비 될 수 하는 동안 예제는 기계 학습 수 운영 화 방법을 tooshow 이러한 웹 서비스의 hello 용도 R 분석 용도로 사용에 대 한 스크립트에 포함할 및 toocreate 사용 되는 웹 서비스 R 코드의 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="de3c3-113">각 예제에는 웹 서비스 소비를 위한 C# 예제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-113">Each example includes a C# example for web service consumption.</span></span>

![Azure 기계 학습의 R 코드의 다이어그램: R 솔루션을 게시 된 toohello Azure 마켓플레이스 또는 독점적인 사용 합니다.][1]

<span data-ttu-id="de3c3-115">다음 시나리오는 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="de3c3-116">시나리오 1: 일반 모델</span><span class="sxs-lookup"><span data-stu-id="de3c3-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="de3c3-117">사용자 기본 예측 시계열 데이터 또는 고급 분석을 사용 하 여 사용자가 작성 한 R 메서드 등과 같은 tooa 적용 된 새 사용자의 데이터 일 수 있는 일반 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="de3c3-118">이 사용자가 hello 게시 tooconsume 하면서 자신의 데이터를 다른 사용자에 대 한 웹 서비스로 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="de3c3-119">이진 분류자</span><span class="sxs-lookup"><span data-stu-id="de3c3-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="de3c3-120">클러스터 모델</span><span class="sxs-lookup"><span data-stu-id="de3c3-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="de3c3-121">다변량 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="de3c3-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="de3c3-122">예측 - 지수 평활법</span><span class="sxs-lookup"><span data-stu-id="de3c3-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="de3c3-123">EETS + STL 예측</span><span class="sxs-lookup"><span data-stu-id="de3c3-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="de3c3-124">예측 - ARIMA(자동 회귀 통합 이동 평균)</span><span class="sxs-lookup"><span data-stu-id="de3c3-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="de3c3-125">생존 분석</span><span class="sxs-lookup"><span data-stu-id="de3c3-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="de3c3-126">시나리오 2: 학습된 모델 – 특정 데이터</span><span class="sxs-lookup"><span data-stu-id="de3c3-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="de3c3-127">사용자의 개성 질문의 큰 샘플 k 알고리즘 toopredict hello 사용자의 개성 형식을 통해 클러스터링 또는 설문 조사 toopredict 사용된 될 수 있는 데이터는 개인의 상태와 같은 R 코드를 통해 유용한 예측을 제공 하는 데이터가 있는 생존 분석 R 패키지와 함께 lung 유방암에 대 한 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="de3c3-128">hello 사용자가 새 사용자의 결과 예측 하는 웹 서비스를 통해 hello 데이터를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="de3c3-129">시나리오 3: 학습된 모델 – 일반 데이터</span><span class="sxs-lookup"><span data-stu-id="de3c3-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="de3c3-130">사용자는 웹 서비스 toobe 빌드되고 다양 한 유형의 사용 사례 및 시나리오에 일반적인 방식으로 적용할 수 있는 일반 데이터 (예: 텍스트 모음)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="de3c3-131">어휘집 기반 감정 분석</span><span class="sxs-lookup"><span data-stu-id="de3c3-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="de3c3-132">시나리오 4: 고급 계산기</span><span class="sxs-lookup"><span data-stu-id="de3c3-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="de3c3-133">사용자는 고급 계산 또는 모든 학습 된 모델 또는 모델 toohello 사용자 데이터의 맞춤 요구 하지 않는 시뮬레이션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="de3c3-134">비율 차이 테스트</span><span class="sxs-lookup"><span data-stu-id="de3c3-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="de3c3-135">정규 분포 제품군</span><span class="sxs-lookup"><span data-stu-id="de3c3-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="de3c3-136">이항 분포 패키지</span><span class="sxs-lookup"><span data-stu-id="de3c3-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="de3c3-137">FAQ</span><span class="sxs-lookup"><span data-stu-id="de3c3-137">FAQ</span></span>
<span data-ttu-id="de3c3-138">Hello 웹 서비스 또는 게시 toohello Marketplace의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de3c3-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



