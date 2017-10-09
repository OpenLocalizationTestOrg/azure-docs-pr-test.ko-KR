---
title: "기계 학습을 사용 하 여 신용 위험에 대 한 aaaA 예측 솔루션 | Microsoft Docs"
description: "자세한 연습 과정을 보여 주는 방법을 toocreate 신용에 대 한 예측 분석 솔루션의 위험 평가 Azure 기계 학습 스튜디오에서."
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
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="7a013-104">연습: Azure 기계 학습의 신용 위험 평가에 대한 예측 분석 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="7a013-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="7a013-105">이 연습에서는 살펴보면는 확장 된 hello 프로세스의 기계 학습 스튜디오에서 예측 분석 솔루션을 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="7a013-106">기계 학습 스튜디오에서 간단한 모델을 개발 하 고 hello 모델이 새 데이터를 사용 하 여 예측을 만들 수 있는 Azure 기계 학습 웹 서비스로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="7a013-107">이 연습에서는 이전에 Machine Learning Studio를 사용해 본 경험이 한 번 이상 있으며 기계 학습 개념에 대해 어느 정도 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="7a013-108">그러나 어느 쪽이든 전문가는 아니라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="7a013-109">사용한 경험이 없는 경우 **Azure 기계 학습 스튜디오** hello 자습서와 함께 toostart 할 수 전에 [Azure 기계 학습 스튜디오에서 실험 하 여 첫 번째 데이터 과학 만들기](machine-learning-create-experiment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="7a013-110">이 자습서에서는 기계 학습 스튜디오 hello에 대 한 처음으로 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="7a013-111">표시를 사용 하 여 실험에 어떻게 toodrag 놓기 모듈의 기본 사항 hello 이들을 서로 연결 hello 실험을 실행 하 고 hello 결과 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="7a013-112">시작 하는 데 도움이 될 수 있는 다른 도구 기계 학습 스튜디오의 hello 기능의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="7a013-113">[Azure Machine Learning Studio 기능 개요 다이어그램](machine-learning-studio-overview-diagram.md)에서 다운로드하고 인쇄할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="7a013-114">기계 학습 일반적 새로운 toohello 필드를 사용 하는 경우 유용한 tooyou 될 수 있는 비디오 시리즈가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="7a013-115">호출 될 [초보자를 위한 데이터 과학](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) 일상적인 언어 및 개념을 사용 하 여 충분히 소개 toomachine 학습 파악 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="7a013-116">hello 문제</span><span class="sxs-lookup"><span data-stu-id="7a013-116">hello problem</span></span>

<span data-ttu-id="7a013-117">개인의 신용 위험 신용 응용 프로그램에서 제공 받은 hello 정보에 따라 toopredict 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="7a013-118">신용 위험 평가는 복잡한 문제이지만 이 연습에서는 다소 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="7a013-119">Microsoft Azure Machine Learning을 사용하여 예측 분석 솔루션을 만들 수 있는 방법의 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="7a013-120">toodo이를 Azure 기계 학습 스튜디오 고 기계 학습 웹 서비스 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="7a013-121">hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="7a013-121">hello solution</span></span>

<span data-ttu-id="7a013-122">이 자세한 연습에서는 공개적으로 사용 가능한 신용 위험 데이터와 함께 시작하고 개발하고 해당 데이터를 기반으로 예측 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="7a013-123">에서는 모델을 배포 하십시오 hello 웹 서비스로 신용 위험 평가 대 한 다른 사용자가 사용할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="7a013-124">toocreate이 신용 위험 평가 솔루션에서는 다음이 단계를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="7a013-125">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="7a013-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="7a013-126">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="7a013-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="7a013-127">실험 만들기</span><span class="sxs-lookup"><span data-stu-id="7a013-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="7a013-128">학습 하 고 hello 모델 평가</span><span class="sxs-lookup"><span data-stu-id="7a013-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="7a013-129">Hello 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="7a013-130">액세스 hello 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="7a013-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="7a013-131">Hello에서이 연습에서 개발 하는 hello 실험의 작업 복사본을 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="7a013-132">너무 이동**[연습-신용 위험 예측](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  클릭 **Studio에서 열기** toodownload 기계 학습 스튜디오 작업 영역으로 hello 실험의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="7a013-133">이 연습에서는 hello 샘플 실험 인의 단순화 된 버전에 따라은 [이진 분류: 신용 위험 예측](http://go.microsoft.com/fwlink/?LinkID=525270)hello 에서도 사용 가능, [갤러리](http://gallery.cortanaintelligence.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a013-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
