---
title: "aaaCopy 기계 학습 예제에서는 실험-Azure | Microsoft Docs"
description: "Toouse 예제 기계 학습 toocreate 새 실험 Cortana 인텔리전스 갤러리 및 Microsoft Azure 기계 학습 실험 하는 방법에 대해 알아봅니다."
keywords: "기계 학습 예제, 샘플 실험, 기계 학습 샘플"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a><span data-ttu-id="64019-104">예제에서는 실험 toocreate 새 기계 학습 실험 복사</span><span class="sxs-lookup"><span data-stu-id="64019-104">Copy example experiments toocreate new machine learning experiments</span></span>
<span data-ttu-id="64019-105">toostart 예제로 실험 하는 방법에 대해 알아봅니다 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/) 기계 학습 실험 처음부터 새로 만드는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-105">Learn how toostart with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="64019-106">사용자 고유의 기계 학습 솔루션 hello 예제 toobuild를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-106">You can use hello examples toobuild your own machine learning solution.</span></span>

<span data-ttu-id="64019-107">hello 갤러리 hello Microsoft Azure 기계 학습 팀과 hello 기계 학습 커뮤니티에서 공유 하 여 예제에서는 실험에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-107">hello gallery has example experiments by hello Microsoft Azure Machine Learning team as well as examples shared by hello Machine Learning community.</span></span> <span data-ttu-id="64019-108">실험에 대한 질문을 하거나 의견을 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="64019-109">hello 3 분 비디오를 시청 하세요 toouse hello 갤러리, 방법 toosee [타인의 작업 toodo 데이터 과학 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) hello 계열에서 [초보자를 위한 데이터 과학](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-109">toosee how toouse hello gallery, watch hello 3-minute video [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from hello series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a><span data-ttu-id="64019-110">실험 toocopy Cortana 인텔리전스 갤러리에서 찾기</span><span class="sxs-lookup"><span data-stu-id="64019-110">Find an experiment toocopy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="64019-111">toosee 어떤 실험은 사용할 수 있는, 이동 toohello [갤러리](https://gallery.cortanaintelligence.com/) 클릭 **실험** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-111">toosee what experiments are available, go toohello [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at hello top of hello page.</span></span>

### <a name="find-hello-newest-or-most-popular-experiments"></a><span data-ttu-id="64019-112">최신 또는 가장 인기 있는 실험 hello 찾기</span><span class="sxs-lookup"><span data-stu-id="64019-112">Find hello newest or most popular experiments</span></span>
<span data-ttu-id="64019-113">이 페이지에서 확인할 수 있습니다 **최근에 추가 된** 실험, 또는 toolook에서 아래로 스크롤하여 **인기 있는 이란** 또는 hello 최신 **인기 있는 Microsoft 실험**합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-113">On this page, you can see **Recently added** experiments, or scroll down toolook at **What's popular** or hello latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="64019-114">특정 요구 사항을 충족하는 실험 찾기</span><span class="sxs-lookup"><span data-stu-id="64019-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="64019-115">모든 toobrowse 실험:</span><span class="sxs-lookup"><span data-stu-id="64019-115">toobrowse all experiments:</span></span>

1. <span data-ttu-id="64019-116">클릭 **모두 찾아보기** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-116">Click **Browse all** at hello top of hello page.</span></span>
2. <span data-ttu-id="64019-117">Hello 왼쪽에 아래 **지정 하 여 구체화** hello에 **범주** 섹션에서 **실험** 의 실험 hello 모든 toosee hello 갤러리입니다.</span><span class="sxs-lookup"><span data-stu-id="64019-117">On hello left-hand side, under **Refine by** in hello **Categories** section, select **Experiment** toosee all hello experiments in hello Gallery.</span></span>
3. <span data-ttu-id="64019-118">두 가지 방법으로 요구 사항을 충족하는 실험을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="64019-119">**Hello 왼쪽에 필터를 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64019-119">**Select filters on hello left.**</span></span> <span data-ttu-id="64019-120">PCA 기반 비정상 검색 알고리즘을 사용 하는 toobrowse 실험 예를 들어:와 **실험** 아래에서 선택한 **범주**, 클릭 **모두 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-120">For example, toobrowse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="64019-121">그런 다음 **사용된 알고리즘**에서 **PCA 기반 변칙 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="64019-122">
     ![필터 선택](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="64019-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="64019-123">**Hello 검색 상자를 사용 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64019-123">**Use hello search box.**</span></span> <span data-ttu-id="64019-124">Toofind 실험 관련 Microsoft가 제공 하는 예를 들어 2 클래스 지원 벡터 컴퓨터 알고리즘을 사용 하는 toodigit 인식 hello 검색 상자에 "자리 인식"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-124">For example, toofind experiments contributed by Microsoft related toodigit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in hello search box.</span></span> <span data-ttu-id="64019-125">그런 다음 선택 hello 필터 **실험**, **Microsoft 콘텐츠만**, 및 **2 클래스 지원 벡터 컴퓨터**:</span><span class="sxs-lookup"><span data-stu-id="64019-125">Then, select hello filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="64019-126">
     ![Hello 검색 상자를 사용 하 여](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="64019-126">
![Use hello search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="64019-127">항목에 대 한 자세한는 실험 toolearn를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-127">Click an experiment toolearn more about it.</span></span>
5. <span data-ttu-id="64019-128">toorun hello 실험을 수정, 클릭 하 여 및/또는 **Studio에서 열기** hello 실험 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-128">toorun and/or modify hello experiment, click **Open in Studio** on hello experiment's page.</span></span> <br></br>

    ![예제 실험](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="64019-130">을 열 때 실험 기계 학습 스튜디오에서 hello에 대 한 처음으로 무료로 시도 또는 Azure 구독을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-130">When you open an experiment in Machine Learning Studio for hello first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="64019-131">Hello 기계 학습 스튜디오 무료 평가판 및 유료 서비스에 알아보기</span><span class="sxs-lookup"><span data-stu-id="64019-131">Learn about hello Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="64019-132">예제를 템플릿으로 사용하여 새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="64019-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="64019-133">갤러리 예제를 템플릿으로 사용하여 Machine Learning Studio에서 새 실험을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64019-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="64019-134">Microsoft 계정 자격 증명 toohello 프로그램 इ न क [Studio](https://studio.azureml.net), 클릭 하 고 **새로** toocreate 실험 합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-134">Sign in with your Microsoft account credentials toohello [Studio](https://studio.azureml.net), and then click **New** toocreate an experiment.</span></span>
2. <span data-ttu-id="64019-135">Hello 예제 콘텐츠 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64019-135">Browse through hello example content and click one.</span></span>

<span data-ttu-id="64019-136">새 실험 hello 예제에서는 실험을 템플릿으로 사용 하 여 기계 학습 스튜디오 작업 영역에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="64019-136">A new experiment is created in your Machine Learning Studio workspace using hello example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64019-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64019-137">Next steps</span></span>
* [<span data-ttu-id="64019-138">다양한 소스에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="64019-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="64019-139">기계 학습에서 hello R 언어에 대 한 빠른 시작 자습서</span><span class="sxs-lookup"><span data-stu-id="64019-139">Quickstart tutorial for hello R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="64019-140">Machine Learning 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="64019-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
