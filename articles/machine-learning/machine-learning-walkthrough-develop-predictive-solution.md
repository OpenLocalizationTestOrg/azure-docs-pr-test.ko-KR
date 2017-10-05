---
title: "기계 학습을 사용한 신용 위험에 대 한 예측 솔루션 | Microsoft Docs"
description: "Azure 기계 학습 스튜디오의 신용 위험 평가에 대한 예측 분석 솔루션을 만드는 방법을 보여주는 자세한 연습."
keywords: "신용 위험, 예측 분석 솔루션, 위험 평가"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="df691-104">연습: Azure 기계 학습의 신용 위험 평가에 대한 예측 분석 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="df691-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="df691-105">이 연습에서는 Machine Learning Studio에서 예측 분석 솔루션을 개발하는 과정을 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="df691-106">Machine Learning Studio에서 간단한 모델을 개발한 다음 이 모델에서 새로운 데이터를 사용하여 예측할 수 있는 Azure Machine Learning 웹 서비스로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="df691-107">이 연습에서는 이전에 Machine Learning Studio를 사용해 본 경험이 한 번 이상 있으며 기계 학습 개념에 대해 어느 정도 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="df691-108">그러나 어느 쪽이든 전문가는 아니라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="df691-109">**Azure Machine Learning Studio**를 사용한 경험이 없는 경우 [Azure Machine Learning Studio에서 첫 번째 데이터 과학 실험 만들기](machine-learning-create-experiment.md) 자습서를 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="df691-110">해당 자습서에서는 처음으로 Machine Learning Studio를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="df691-111">이 자습서는 실험에 모듈을 끌어 놓고 서로 연결하고 실험을 실행하고 결과를 확인하는 방법의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df691-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="df691-112">시작하는 데 도움이 될 수 있는 다른 도구는 Machine Learning Studio의 기능에 대한 개요를 제공하는 다이어그램입니다.</span><span class="sxs-lookup"><span data-stu-id="df691-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="df691-113">[Azure Machine Learning Studio 기능 개요 다이어그램](machine-learning-studio-overview-diagram.md)에서 다운로드하고 인쇄할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="df691-114">일반적으로 기계 학습 분야를 처음 접하는 경우 도움이 될 수 있는 비디오 시리즈가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="df691-115">[초급자를 위한 데이터 과학](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)이라고 하며 일상적인 언어 및 개념을 사용하여 기계 학습에 대한 훌륭한 소개를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="df691-116">문제</span><span class="sxs-lookup"><span data-stu-id="df691-116">The problem</span></span>

<span data-ttu-id="df691-117">신용대출 지원 시 제공한 정보를 기반으로 개인의 신용 위험을 예측해야 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="df691-118">신용 위험 평가는 복잡한 문제이지만 이 연습에서는 다소 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="df691-119">Microsoft Azure Machine Learning을 사용하여 예측 분석 솔루션을 만들 수 있는 방법의 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="df691-120">이 작업을 수행하기 위해 Azure Machine Learning Studio 및 Machine Learning 웹 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="df691-121">솔루션</span><span class="sxs-lookup"><span data-stu-id="df691-121">The solution</span></span>

<span data-ttu-id="df691-122">이 자세한 연습에서는 공개적으로 사용 가능한 신용 위험 데이터와 함께 시작하고 개발하고 해당 데이터를 기반으로 예측 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="df691-123">그런 다음 다른 사용자가 신용 위험 평가를 위해 사용할 수 있도록 웹 서비스로 모델을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="df691-124">이 신용 위험 평가 솔루션을 만들려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="df691-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="df691-125">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="df691-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="df691-126">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="df691-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="df691-127">실험 만들기</span><span class="sxs-lookup"><span data-stu-id="df691-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="df691-128">모델 학습 및 평가</span><span class="sxs-lookup"><span data-stu-id="df691-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="df691-129">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="df691-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="df691-130">웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="df691-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="df691-131">[Cortana Intelligence 갤러리](https://gallery.cortanaintelligence.com)의 이 연습에서 개발하는 실험의 작업 복사본을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df691-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="df691-132">**[연습 - 신용 위험 예측](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**으로 이동하고 **Studio에서 열기**를 클릭하여 Machine Learning Studio 작업 영역으로 실험의 복사본을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="df691-133">이 연습은 [이진 분류: 신용 위험 예측](http://go.microsoft.com/fwlink/?LinkID=525270) 샘플 실험의 간소화된 버전을 기반으로 하며 [갤러리](http://gallery.cortanaintelligence.com/)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="df691-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
