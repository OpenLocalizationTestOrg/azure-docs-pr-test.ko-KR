---
title: "Azure 기계 학습 스튜디오란? | Microsoft Docs"
description: "Azure ML Studio의 개요로, 알고리즘 및 모듈의 사용할 준비가 되어 있는 라이브러리에서 신속하게 모델을 빌드하기 위한 끌어서 놓기 도구입니다."
keywords: "azure 기계 학습, azure ml, 기계 학습 스튜디오"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 70a1d0acb8ec9bbb591f696281ea5e975b443a15
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-machine-learning-studio"></a><span data-ttu-id="db5ec-105">Azure 기계 학습 스튜디오란?</span><span class="sxs-lookup"><span data-stu-id="db5ec-105">What is Azure Machine Learning Studio?</span></span>
<span data-ttu-id="db5ec-106">Microsoft Azure 기계 학습 스튜디오는 데이터에 대한 예측 분석 솔루션을 빌드, 테스트, 배포할 수 있는 공동 끌어서 놓기 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-106">Microsoft Azure Machine Learning Studio is a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="db5ec-107">기계 학습 스튜디오는 Excel과 같은 BI 도구 또는 사용자 지정 앱에서 쉽게 사용할 수 있는 웹 서비스로 모델을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-107">Machine Learning Studio publishes models as web services that can easily be consumed by custom apps or BI tools such as Excel.</span></span>

<span data-ttu-id="db5ec-108">기계 학습 스튜디오는 데이터 과학, 예측 분석, 클라우드 리소스 및 데이터가 만나는 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-108">Machine Learning Studio is where data science, predictive analytics, cloud resources, and your data meet.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-machine-learning-studio-interactive-workspace"></a><span data-ttu-id="db5ec-109">기계 학습 스튜디오 대화형 작업 영역</span><span class="sxs-lookup"><span data-stu-id="db5ec-109">The Machine Learning Studio interactive workspace</span></span>
<span data-ttu-id="db5ec-110">예측 분석 모델을 개발하려면 일반적으로 원본 하나 이상의 데이터를 사용하고, 다양한 데이터 조작과 통계 함수를 통해 해당 데이터를 변환 및 분석하고, 결과 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-110">To develop a predictive analysis model, you typically use data from one or more sources, transform and analyze that data through various data manipulation and statistical functions, and generate a set of results.</span></span> <span data-ttu-id="db5ec-111">이와 같은 모델을 개발하는 과정은 반복 프로세스이며,</span><span class="sxs-lookup"><span data-stu-id="db5ec-111">Developing a model like this is an iterative process.</span></span> <span data-ttu-id="db5ec-112">다양한 함수와 해당 매개 변수를 수정할 때 학습된 효과적인 모델을 마련했다고 만족할 때까지 결과가 수렴됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-112">As you modify the various functions and their parameters, your results converge until you are satisfied that you have a trained, effective model.</span></span>

<span data-ttu-id="db5ec-113">**Azure 기계 학습 스튜디오**에서는 예측 분석 모델을 간편하게 빌드, 테스트, 반복할 수 있는 대화형 시각적 작업 영역을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-113">**Azure Machine Learning Studio** gives you an interactive, visual workspace to easily build, test, and iterate on a predictive analysis model.</span></span> <span data-ttu-id="db5ec-114">***데이터 집합***과 분석 ***모듈***을 대화형 캔버스로 끌어서 놓고 함께 연결하여 ***실험***을 생성하고 Machine Learning 스튜디오에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-114">You drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas, connecting them together to form an ***experiment***, which you run in Machine Learning Studio.</span></span> <span data-ttu-id="db5ec-115">모델 디자인을 반복하려면 실험을 편집하고 필요에 따라 복사본을 저장하고 실험을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-115">To iterate on your model design, you edit the experiment, save a copy if desired, and run it again.</span></span> <span data-ttu-id="db5ec-116">준비가 되면 ***학습 실험***을 ***예측 실험***으로 변환한 다음 다른 사용자가 모델에 액세스할 수 있도록 ***웹 서비스***로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-116">When you're ready, you can convert your ***training experiment*** to a ***predictive experiment***, and then publish it as a ***web service*** so that your model can be accessed by others.</span></span>

<span data-ttu-id="db5ec-117">프로그래밍이 필요하지 않고 데이터 집합과 모듈을 시각적으로 연결하면 예측 분석 모델을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-117">There is no programming required, just visually connecting datasets and modules to construct your predictive analysis model.</span></span>

> [!TIP]
> <span data-ttu-id="db5ec-118">기계 학습 스튜디오의 기능을 개략적으로 제공하는 다이어그램을 다운로드하고 인쇄하려면 [Azure 기계 학습 스튜디오 기능 개요](machine-learning-studio-overview-diagram.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-118">To download and print a diagram that gives an overview of the capabilities of Machine Learning Studio, see [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
> 
> 

![Azure ML Studio 다이어그램: 실험을 만들고, 여러 원본에 대한 데이터 읽고, 점수 데이터를 쓰고, 모델을 작성합니다.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a><span data-ttu-id="db5ec-120">기계 학습 스튜디오 시작</span><span class="sxs-lookup"><span data-stu-id="db5ec-120">Get started with Machine Learning Studio</span></span>
<span data-ttu-id="db5ec-121">[기계 학습 스튜디오](https://studio.azureml.net)를 처음 시작하면 **홈** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-121">When you first enter [Machine Learning Studio](https://studio.azureml.net) you see the **Home** page.</span></span> <span data-ttu-id="db5ec-122">여기에서 설명서, 동영상, 웹 세미나를 보고 다른 유용한 리소스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-122">From here you can view documentation, videos, webinars, and find other valuable resources.</span></span>

<span data-ttu-id="db5ec-123">왼쪽 위 메뉴를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-123">Click the upper-left menu</span></span> ![메뉴](media/machine-learning-what-is-ml-studio/menu.png) <span data-ttu-id="db5ec-125">몇 가지 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-125">and you'll see several options.</span></span>

### <a name="cortana-intelligence"></a><span data-ttu-id="db5ec-126">Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="db5ec-126">Cortana Intelligence</span></span>
<span data-ttu-id="db5ec-127">**Cortana Intelligence**를 클릭하면 [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite)의 홈페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-127">Click **Cortana Intelligence** and you'll be taken to the home page of the [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite).</span></span> <span data-ttu-id="db5ec-128">Cortana Intelligence Suite은 데이터를 지능형 작업으로 변환할 수 있는 완전히 관리되는 빅 데이터 및 고급 분석 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-128">The Cortana Intelligence Suite is a fully managed big data and advanced analytics suite to transform your data into intelligent action.</span></span> <span data-ttu-id="db5ec-129">고객 사례를 포함한 전체 설명서에 대한 Suite 홈 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-129">See the Suite home page for full documentation, including customer stories.</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="db5ec-130">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="db5ec-130">Azure Machine Learning</span></span>
<span data-ttu-id="db5ec-131">여기에 시작한 페이지인 **홈**과 **Studio**, 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-131">There are two options here, **Home**, the page where you started, and **Studio**.</span></span>

<span data-ttu-id="db5ec-132">**Studio**를 클릭하여 **Azure Machine Learning Studio**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-132">Click **Studio** and you'll be taken to the **Azure Machine Learning Studio**.</span></span> <span data-ttu-id="db5ec-133">먼저 Microsoft 계정이나 회사 또는 학교 계정을 사용하여 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-133">First you'll be asked to sign in using your Microsoft account, or your work or school account.</span></span> <span data-ttu-id="db5ec-134">로그인하면 왼쪽에 다음과 같은 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-134">Once signed in, you'll see the following tabs on the left:</span></span>

* <span data-ttu-id="db5ec-135">**프로젝트** - 단일 프로젝트를 나타내는 실험, 데이터 집합, notebooks 및 기타 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-135">**PROJECTS** - Collections of experiments, datasets, notebooks, and other resources representing a single project</span></span>
* <span data-ttu-id="db5ec-136">**실험** - 만들고 실행하거나 초안으로 저장한 실험입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-136">**EXPERIMENTS** - Experiments that you have created and run or saved as drafts</span></span>
* <span data-ttu-id="db5ec-137">**웹 서비스** - 실험에서 배포한 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-137">**WEB SERVICES** - Web services that you have deployed from your experiments</span></span>
* <span data-ttu-id="db5ec-138">**노트북** - 사용자가 만든 Jupyter 노트북입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-138">**NOTEBOOKS** - Jupyter notebooks that you have created</span></span>
* <span data-ttu-id="db5ec-139">**데이터 집합** - 스튜디오로 업로드한 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-139">**DATASETS** - Datasets that you have uploaded into Studio</span></span>
* <span data-ttu-id="db5ec-140">**학습된 모델** - 실험에서 학습하고 스튜디오에 저장한 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-140">**TRAINED MODELS** - Models that you have trained in experiments and saved in Studio</span></span>
* <span data-ttu-id="db5ec-141">**설정** - 계정과 리소스를 구성하는 데 사용할 수 있는 설정 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-141">**SETTINGS** - A collection of settings that you can use to configure your account and resources.</span></span>

### <a name="gallery"></a><span data-ttu-id="db5ec-142">갤러리</span><span class="sxs-lookup"><span data-stu-id="db5ec-142">Gallery</span></span>
<span data-ttu-id="db5ec-143">**갤러리** 탭을 클릭하면 **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**로 이동하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-143">Click **Gallery** and you'll be taken to the **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**.</span></span> <span data-ttu-id="db5ec-144">갤러리는 데이터 과학자 및 개발자 커뮤니티가 Cortana Intelligence Suite의 구성 요소를 사용하여 만든 솔루션을 공유하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-144">The Gallery is a place where a community of data scientists and developers share solutions created using components of the Cortana Intelligence Suite.</span></span>

<span data-ttu-id="db5ec-145">갤러리에 대한 자세한 내용은 [Cortana Intelligence 갤러리의 솔루션 공유 및 검색](machine-learning-gallery-how-to-use-contribute-publish.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-145">For more information about the Gallery, see [Share and discover solutions in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

## <a name="components-of-an-experiment"></a><span data-ttu-id="db5ec-146">실험 구성 요소</span><span class="sxs-lookup"><span data-stu-id="db5ec-146">Components of an experiment</span></span>
<span data-ttu-id="db5ec-147">실험은 함께 연결하여 예측 분석 모델을 구성하는 분석 모듈에 데이터를 제공하는 데이터 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-147">An experiment consists of datasets that provide data to analytical modules, which you connect together to construct a predictive analysis model.</span></span> <span data-ttu-id="db5ec-148">특히 유효한 실험에는 다음 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-148">Specifically, a valid experiment has these characteristics:</span></span>

* <span data-ttu-id="db5ec-149">실험에는 하나 이상의 데이터 집합과 하나의 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-149">The experiment has at least one dataset and one module</span></span>
* <span data-ttu-id="db5ec-150">데이터 집합은 모듈에만 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-150">Datasets may be connected only to modules</span></span>
* <span data-ttu-id="db5ec-151">모듈은 데이터 집합 또는 다른 모듈에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-151">Modules may be connected to either datasets or other modules</span></span>
* <span data-ttu-id="db5ec-152">모듈에 대한 모든 입력 포트에는 데이터 흐름에 대한 연결이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-152">All input ports for modules must have some connection to the data flow</span></span>
* <span data-ttu-id="db5ec-153">각 모듈에 대한 모든 필수 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-153">All required parameters for each module must be set</span></span>

<span data-ttu-id="db5ec-154">실험을 처음부터 만들거나 기존 샘플 실험을 템플릿으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-154">You can create an experiment from scratch, or you can use an existing sample experiment as a template.</span></span> <span data-ttu-id="db5ec-155">자세한 내용은 [샘플 실험을 복사하여 새로운 기계 학습 실험 만들기](machine-learning-sample-experiments.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-155">For more information, see [Copy example experiments to create new machine learning experiments](machine-learning-sample-experiments.md).</span></span>

<span data-ttu-id="db5ec-156">간단한 실험을 만드는 예는 [Azure 기계 학습 스튜디오에서 간단한 실험 만들기](machine-learning-create-experiment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-156">For an example of creating a simple experiment, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span>

<span data-ttu-id="db5ec-157">예측 분석 솔루션을 만드는 자세한 연습 과정은 [Azure 기계 학습을 사용한 예측 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-157">For a more complete walkthrough of creating a predictive analytics solution, see [Develop a predictive solution with Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

### <a name="datasets"></a><span data-ttu-id="db5ec-158">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="db5ec-158">Datasets</span></span>
<span data-ttu-id="db5ec-159">데이터 집합은 모델링 프로세스에서 사용할 수 있도록 기계 학습 스튜디오에 업로드된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-159">A dataset is data that has been uploaded to Machine Learning Studio so that it can be used in the modeling process.</span></span> <span data-ttu-id="db5ec-160">기계 학습 스튜디오에는 실험에 사용할 다양한 샘플 데이터 집합이 포함되고, 필요할 때 추가 데이터 집합을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-160">A number of sample datasets are included with Machine Learning Studio for you to experiment with, and you can upload more datasets as you need them.</span></span> <span data-ttu-id="db5ec-161">포함된 데이터 집합의 몇 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-161">Here are some examples of included datasets:</span></span>

* <span data-ttu-id="db5ec-162">**다양한 자동차에 대한 MPG 데이터** - 실린더 수, 마력 등으로 식별되는 자동차에 대한 MPG 값</span><span class="sxs-lookup"><span data-stu-id="db5ec-162">**MPG data for various automobiles** - Miles per gallon (MPG) values for automobiles identified by number of cylinders, horsepower, etc.</span></span>
* <span data-ttu-id="db5ec-163">**유방암 데이터** - 유방암 진단 데이터</span><span class="sxs-lookup"><span data-stu-id="db5ec-163">**Breast cancer data** - Breast cancer diagnosis data.</span></span>
* <span data-ttu-id="db5ec-164">**산불 데이터** - 포르투갈 북동부에서 발생한 산불 규모</span><span class="sxs-lookup"><span data-stu-id="db5ec-164">**Forest fires data** - Forest fire sizes in northeast Portugal.</span></span>

<span data-ttu-id="db5ec-165">실험을 빌드할 때 캔버스의 왼쪽에서 사용할 수 있는 데이터 집합의 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-165">As you build an experiment you can choose from the list of datasets available to the left of the canvas.</span></span>

<span data-ttu-id="db5ec-166">기계 학습 스튜디오에 포함된 샘플 데이터 집합의 목록은 [Azure 기계 학습 스튜디오에서 예제 데이터 집합 사용](machine-learning-use-sample-datasets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-166">For a list of sample datasets included in Machine Learning Studio, see [Use the sample data sets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span></span>

### <a name="modules"></a><span data-ttu-id="db5ec-167">모듈</span><span class="sxs-lookup"><span data-stu-id="db5ec-167">Modules</span></span>
<span data-ttu-id="db5ec-168">모듈은 데이터에 대해 수행할 수 있는 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-168">A module is an algorithm that you can perform on your data.</span></span> <span data-ttu-id="db5ec-169">기계 학습 스튜디오에는 데이터 가져오기 함수부터 학습, 점수 매기기 및 유효성 검사 프로세스에 이르는 다양한 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-169">Machine Learning Studio has a number of modules ranging from data ingress functions to training, scoring, and validation processes.</span></span> <span data-ttu-id="db5ec-170">포함된 모듈의 몇 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-170">Here are some examples of included modules:</span></span>

* <span data-ttu-id="db5ec-171">[ARFF로 변환][convert-to-arff] - .NET 직렬화된 데이터 집합을 ARFF(Attribute-Relation File Format) 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-171">[Convert to ARFF][convert-to-arff] - Converts a .NET serialized dataset to Attribute-Relation File Format (ARFF).</span></span>
* <span data-ttu-id="db5ec-172">[기본 통계 계산][elementary-statistics] - 평균, 표준 편차 등의 기본 통계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-172">[Compute Elementary Statistics][elementary-statistics] - Calculates elementary statistics such as mean, standard deviation, etc.</span></span>
* <span data-ttu-id="db5ec-173">[선형 회귀][linear-regression] - 온라인 기울기 하강 기반 선형 회귀 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-173">[Linear Regression][linear-regression] - Creates an online gradient descent-based linear regression model.</span></span>
* <span data-ttu-id="db5ec-174">[모델 점수 매기기][score-model] - 학습된 분류 또는 회귀 모델의 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-174">[Score Model][score-model] - Scores a trained classification or regression model.</span></span>

<span data-ttu-id="db5ec-175">실험을 빌드할 때 캔버스의 왼쪽에서 사용할 수 있는 모듈의 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-175">As you build an experiment you can choose from the list of modules available to the left of the canvas.</span></span>  

<span data-ttu-id="db5ec-176">모듈에는 모듈 내부 알고리즘을 구성하는 데 사용할 수 있는 매개 변수 집합이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-176">A module may have a set of parameters that you can use to configure the module's internal algorithms.</span></span> <span data-ttu-id="db5ec-177">캔버스에서 모듈을 선택할 때 모듈 매개 변수가 캔버스 오른쪽의 **속성** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-177">When you select a module on the canvas, the module's parameters are displayed in the **Properties** pane to the right of the canvas.</span></span> <span data-ttu-id="db5ec-178">해당 창에서 매개 변수를 수정하여 모델을 튜닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-178">You can modify the parameters in that pane to tune your model.</span></span>

<span data-ttu-id="db5ec-179">사용 가능한 기계 학습 알고리즘의 대규모 라이브러리를 탐색하는 방법에 대한 도움말은 [Microsoft Azure 기계 학습을 위한 알고리즘 선택 방법](machine-learning-algorithm-choice.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-179">For some help navigating through the large library of machine learning algorithms available, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>

## <a name="deploying-a-predictive-analytics-web-service"></a><span data-ttu-id="db5ec-180">예측 분석 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="db5ec-180">Deploying a predictive analytics web service</span></span>
<span data-ttu-id="db5ec-181">예측 분석 모델이 준비되면 기계 학습 스튜디오에서 곧바로 해당 모델을 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db5ec-181">Once your predictive analytics model is ready, you can deploy it as a web service right from Machine Learning Studio.</span></span> <span data-ttu-id="db5ec-182">이 프로세스에 대한 자세한 내용은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5ec-182">For more details on this process, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
