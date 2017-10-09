---
title: "aaaWhat은 Azure 기계 학습 스튜디오는? | Microsoft Docs"
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
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a><span data-ttu-id="81339-105">Azure 기계 학습 스튜디오란?</span><span class="sxs-lookup"><span data-stu-id="81339-105">What is Azure Machine Learning Studio?</span></span>
<span data-ttu-id="81339-106">Microsoft Azure 기계 학습 스튜디오 toobuild, 사용할 수 있는 공동 작업, 끌어서 놓기 도구는 테스트 및 사용자 데이터에 대 한 예측 분석 솔루션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-106">Microsoft Azure Machine Learning Studio is a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="81339-107">기계 학습 스튜디오는 Excel과 같은 BI 도구 또는 사용자 지정 앱에서 쉽게 사용할 수 있는 웹 서비스로 모델을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-107">Machine Learning Studio publishes models as web services that can easily be consumed by custom apps or BI tools such as Excel.</span></span>

<span data-ttu-id="81339-108">기계 학습 스튜디오는 데이터 과학, 예측 분석, 클라우드 리소스 및 데이터가 만나는 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-108">Machine Learning Studio is where data science, predictive analytics, cloud resources, and your data meet.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a><span data-ttu-id="81339-109">대화형 hello 기계 학습 스튜디오 작업 영역</span><span class="sxs-lookup"><span data-stu-id="81339-109">hello Machine Learning Studio interactive workspace</span></span>
<span data-ttu-id="81339-110">예측 분석 모델 toodevelop 일반적으로 사용 데이터 하나 이상의 소스에서 변환 및 다양 한 데이터 조작 및 통계 함수를 통해 해당 데이터를 분석 하 고 결과 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-110">toodevelop a predictive analysis model, you typically use data from one or more sources, transform and analyze that data through various data manipulation and statistical functions, and generate a set of results.</span></span> <span data-ttu-id="81339-111">이와 같은 모델을 개발하는 과정은 반복 프로세스이며,</span><span class="sxs-lookup"><span data-stu-id="81339-111">Developing a model like this is an iterative process.</span></span> <span data-ttu-id="81339-112">다양 한 기능 및 해당 매개 변수에 hello, 결과 수렴 만족할 때까지 수정 하면 효과적인 모델을 학습된 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-112">As you modify hello various functions and their parameters, your results converge until you are satisfied that you have a trained, effective model.</span></span>

<span data-ttu-id="81339-113">**Azure 기계 학습 스튜디오** 대화형, 시각적 작업 영역 tooeasily 프로젝트를 빌드하면 제공 테스트 및 예측 분석 모델을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-113">**Azure Machine Learning Studio** gives you an interactive, visual workspace tooeasily build, test, and iterate on a predictive analysis model.</span></span> <span data-ttu-id="81339-114">끌어서 놓기 있습니다 ***데이터 집합*** 및 분석 ***모듈*** 는 대화형 캔버스로 연결 함께 tooform는 ***실험***, 기계 학습에서 실행 Studio 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-114">You drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas, connecting them together tooform an ***experiment***, which you run in Machine Learning Studio.</span></span> <span data-ttu-id="81339-115">모델 디자인에 대해 tooiterate, 원하는 경우 복사본을 저장 hello 실험 편집한 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-115">tooiterate on your model design, you edit hello experiment, save a copy if desired, and run it again.</span></span> <span data-ttu-id="81339-116">준비 되 면 경우 변환할 수 있습니다 프로그램 ***학습 실험*** tooa ***예측 실험***,으로 다음 게시는 ***웹 서비스*** 모델에 액세스할 수 있도록 다른 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-116">When you're ready, you can convert your ***training experiment*** tooa ***predictive experiment***, and then publish it as a ***web service*** so that your model can be accessed by others.</span></span>

<span data-ttu-id="81339-117">필수, 예측 분석 모델 데이터 집합 및 모듈 tooconstruct를 시각적으로 바로 연결 없는 프로그래밍 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-117">There is no programming required, just visually connecting datasets and modules tooconstruct your predictive analysis model.</span></span>

> [!TIP]
> <span data-ttu-id="81339-118">기계 학습 스튜디오의 hello 기능의 개요 다이어그램 참조 toodownload 및 인쇄 [Azure 기계 학습 스튜디오 기능의 개요 다이어그램](machine-learning-studio-overview-diagram.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-118">toodownload and print a diagram that gives an overview of hello capabilities of Machine Learning Studio, see [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
> 
> 

![Azure ML Studio 다이어그램: 실험을 만들고, 여러 원본에 대한 데이터 읽고, 점수 데이터를 쓰고, 모델을 작성합니다.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a><span data-ttu-id="81339-120">기계 학습 스튜디오 시작</span><span class="sxs-lookup"><span data-stu-id="81339-120">Get started with Machine Learning Studio</span></span>
<span data-ttu-id="81339-121">처음 입력할 때 [기계 학습 스튜디오](https://studio.azureml.net) hello 참조 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="81339-121">When you first enter [Machine Learning Studio](https://studio.azureml.net) you see hello **Home** page.</span></span> <span data-ttu-id="81339-122">여기에서 설명서, 동영상, 웹 세미나를 보고 다른 유용한 리소스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-122">From here you can view documentation, videos, webinars, and find other valuable resources.</span></span>

<span data-ttu-id="81339-123">Hello 왼쪽 위 메뉴를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-123">Click hello upper-left menu</span></span> ![메뉴](media/machine-learning-what-is-ml-studio/menu.png) <span data-ttu-id="81339-125">몇 가지 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81339-125">and you'll see several options.</span></span>

### <a name="cortana-intelligence"></a><span data-ttu-id="81339-126">Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="81339-126">Cortana Intelligence</span></span>
<span data-ttu-id="81339-127">클릭 **Cortana 인텔리전스** hello의 toohello 홈 페이지로 이동 됩니다 및 [Cortana 인텔리전스 Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite)합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-127">Click **Cortana Intelligence** and you'll be taken toohello home page of hello [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite).</span></span> <span data-ttu-id="81339-128">hello Cortana Intelligence Suite는 완전히 관리 되는 큰 데이터 및 분석 suite tootransform 데이터 지능형 동작으로 고급 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-128">hello Cortana Intelligence Suite is a fully managed big data and advanced analytics suite tootransform your data into intelligent action.</span></span> <span data-ttu-id="81339-129">Hello Suite 홈 페이지를 고객의 이야기를 포함 한 전체 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="81339-129">See hello Suite home page for full documentation, including customer stories.</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="81339-130">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="81339-130">Azure Machine Learning</span></span>
<span data-ttu-id="81339-131">두 가지 옵션이 여기에서 **홈**, 시작 위치, hello 페이지 및 **Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-131">There are two options here, **Home**, hello page where you started, and **Studio**.</span></span>

<span data-ttu-id="81339-132">클릭 **Studio** toohello 이동 됩니다 및 **Azure 기계 학습 스튜디오**합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-132">Click **Studio** and you'll be taken toohello **Azure Machine Learning Studio**.</span></span> <span data-ttu-id="81339-133">먼저 만들라는 메시지가 Microsoft 계정 또는 회사 또는 학교 계정을 사용 하 여 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-133">First you'll be asked toosign in using your Microsoft account, or your work or school account.</span></span> <span data-ttu-id="81339-134">로그인 한 후에 hello 탭에 나오는 hello 왼쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81339-134">Once signed in, you'll see hello following tabs on hello left:</span></span>

* <span data-ttu-id="81339-135">**프로젝트** - 단일 프로젝트를 나타내는 실험, 데이터 집합, notebooks 및 기타 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-135">**PROJECTS** - Collections of experiments, datasets, notebooks, and other resources representing a single project</span></span>
* <span data-ttu-id="81339-136">**실험** - 만들고 실행하거나 초안으로 저장한 실험입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-136">**EXPERIMENTS** - Experiments that you have created and run or saved as drafts</span></span>
* <span data-ttu-id="81339-137">**웹 서비스** - 실험에서 배포한 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-137">**WEB SERVICES** - Web services that you have deployed from your experiments</span></span>
* <span data-ttu-id="81339-138">**노트북** - 사용자가 만든 Jupyter 노트북입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-138">**NOTEBOOKS** - Jupyter notebooks that you have created</span></span>
* <span data-ttu-id="81339-139">**데이터 집합** - 스튜디오로 업로드한 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-139">**DATASETS** - Datasets that you have uploaded into Studio</span></span>
* <span data-ttu-id="81339-140">**학습된 모델** - 실험에서 학습하고 스튜디오에 저장한 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-140">**TRAINED MODELS** - Models that you have trained in experiments and saved in Studio</span></span>
* <span data-ttu-id="81339-141">**설정** -계정 및 리소스 tooconfigure를 사용할 수 있는 설정의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-141">**SETTINGS** - A collection of settings that you can use tooconfigure your account and resources.</span></span>

### <a name="gallery"></a><span data-ttu-id="81339-142">갤러리</span><span class="sxs-lookup"><span data-stu-id="81339-142">Gallery</span></span>
<span data-ttu-id="81339-143">클릭 **갤러리** toohello 이동 됩니다 및  **[Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/)**합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-143">Click **Gallery** and you'll be taken toohello **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**.</span></span> <span data-ttu-id="81339-144">hello 갤러리에는 데이터 과학자 및 개발자의 커뮤니티 hello Cortana Intelligence 제품군의 구성 요소를 사용 하 여 만든 솔루션을 공유 하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-144">hello Gallery is a place where a community of data scientists and developers share solutions created using components of hello Cortana Intelligence Suite.</span></span>

<span data-ttu-id="81339-145">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리에서에서 솔루션을 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-145">For more information about hello Gallery, see [Share and discover solutions in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

## <a name="components-of-an-experiment"></a><span data-ttu-id="81339-146">실험 구성 요소</span><span class="sxs-lookup"><span data-stu-id="81339-146">Components of an experiment</span></span>
<span data-ttu-id="81339-147">실험 서로 연결 하는 데이터 tooanalytical 모듈을 제공 하는 데이터 집합으로 이루어져 tooconstruct 예측 분석 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-147">An experiment consists of datasets that provide data tooanalytical modules, which you connect together tooconstruct a predictive analysis model.</span></span> <span data-ttu-id="81339-148">특히 유효한 실험에는 다음 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81339-148">Specifically, a valid experiment has these characteristics:</span></span>

* <span data-ttu-id="81339-149">hello 실험에 하나 이상의 데이터 집합 및 하나의 모듈</span><span class="sxs-lookup"><span data-stu-id="81339-149">hello experiment has at least one dataset and one module</span></span>
* <span data-ttu-id="81339-150">데이터 집합에 연결 된 유일한 toomodules 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-150">Datasets may be connected only toomodules</span></span>
* <span data-ttu-id="81339-151">연결 된 tooeither 데이터 집합 또는 다른 모듈 모듈 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-151">Modules may be connected tooeither datasets or other modules</span></span>
* <span data-ttu-id="81339-152">모듈에 대 한 모든 입력된 포트에는 일부 연결 toohello 데이터를 사용 해야 합니다. 흐름</span><span class="sxs-lookup"><span data-stu-id="81339-152">All input ports for modules must have some connection toohello data flow</span></span>
* <span data-ttu-id="81339-153">각 모듈에 대한 모든 필수 매개 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-153">All required parameters for each module must be set</span></span>

<span data-ttu-id="81339-154">실험을 처음부터 만들거나 기존 샘플 실험을 템플릿으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-154">You can create an experiment from scratch, or you can use an existing sample experiment as a template.</span></span> <span data-ttu-id="81339-155">자세한 내용은 참조 [코드 예제에서는 실험 toocreate 새 기계 학습 실험](machine-learning-sample-experiments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-155">For more information, see [Copy example experiments toocreate new machine learning experiments](machine-learning-sample-experiments.md).</span></span>

<span data-ttu-id="81339-156">간단한 실험을 만드는 예는 [Azure 기계 학습 스튜디오에서 간단한 실험 만들기](machine-learning-create-experiment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81339-156">For an example of creating a simple experiment, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span>

<span data-ttu-id="81339-157">예측 분석 솔루션을 만드는 자세한 연습 과정은 [Azure 기계 학습을 사용한 예측 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81339-157">For a more complete walkthrough of creating a predictive analytics solution, see [Develop a predictive solution with Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

### <a name="datasets"></a><span data-ttu-id="81339-158">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="81339-158">Datasets</span></span>
<span data-ttu-id="81339-159">데이터 집합은 모델링 프로세스 hello에 사용할 수 있도록 된 데이터 tooMachine 학습 스튜디오를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-159">A dataset is data that has been uploaded tooMachine Learning Studio so that it can be used in hello modeling process.</span></span> <span data-ttu-id="81339-160">다양 한 예제 데이터 집합, tooexperiment에 대 한 기계 학습 스튜디오에 포함 되며 필요에 따라 더 많은 데이터 집합을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-160">A number of sample datasets are included with Machine Learning Studio for you tooexperiment with, and you can upload more datasets as you need them.</span></span> <span data-ttu-id="81339-161">포함된 데이터 집합의 몇 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-161">Here are some examples of included datasets:</span></span>

* <span data-ttu-id="81339-162">**다양한 자동차에 대한 MPG 데이터** - 실린더 수, 마력 등으로 식별되는 자동차에 대한 MPG 값</span><span class="sxs-lookup"><span data-stu-id="81339-162">**MPG data for various automobiles** - Miles per gallon (MPG) values for automobiles identified by number of cylinders, horsepower, etc.</span></span>
* <span data-ttu-id="81339-163">**유방암 데이터** - 유방암 진단 데이터</span><span class="sxs-lookup"><span data-stu-id="81339-163">**Breast cancer data** - Breast cancer diagnosis data.</span></span>
* <span data-ttu-id="81339-164">**산불 데이터** - 포르투갈 북동부에서 발생한 산불 규모</span><span class="sxs-lookup"><span data-stu-id="81339-164">**Forest fires data** - Forest fire sizes in northeast Portugal.</span></span>

<span data-ttu-id="81339-165">실험을 만들 때 선택할 수 있습니다 사용할 수 있는 데이터 집합의 hello 목록에서 toohello hello 캔버스의 왼쪽.</span><span class="sxs-lookup"><span data-stu-id="81339-165">As you build an experiment you can choose from hello list of datasets available toohello left of hello canvas.</span></span>

<span data-ttu-id="81339-166">목록이 기계 학습 스튜디오에 포함 된 샘플 데이터 집합에 대 한 참조 [hello 예제 데이터 집합을 사용 하 여 Azure 기계 학습 스튜디오에서](machine-learning-use-sample-datasets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-166">For a list of sample datasets included in Machine Learning Studio, see [Use hello sample data sets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span></span>

### <a name="modules"></a><span data-ttu-id="81339-167">모듈</span><span class="sxs-lookup"><span data-stu-id="81339-167">Modules</span></span>
<span data-ttu-id="81339-168">모듈은 데이터에 대해 수행할 수 있는 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-168">A module is an algorithm that you can perform on your data.</span></span> <span data-ttu-id="81339-169">기계 학습 스튜디오에 데이터 유입 함수 tootraining, 상태 평가 및 유효성 검사 프로세스에서 사이의 모듈의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="81339-169">Machine Learning Studio has a number of modules ranging from data ingress functions tootraining, scoring, and validation processes.</span></span> <span data-ttu-id="81339-170">포함된 모듈의 몇 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-170">Here are some examples of included modules:</span></span>

* <span data-ttu-id="81339-171">[TooARFF 변환] [ convert-to-arff] -변환 직렬화 된.NET dataset tooAttribute 관계 파일 형식 (ARFF).</span><span class="sxs-lookup"><span data-stu-id="81339-171">[Convert tooARFF][convert-to-arff] - Converts a .NET serialized dataset tooAttribute-Relation File Format (ARFF).</span></span>
* <span data-ttu-id="81339-172">[기본 통계 계산][elementary-statistics] - 평균, 표준 편차 등의 기본 통계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-172">[Compute Elementary Statistics][elementary-statistics] - Calculates elementary statistics such as mean, standard deviation, etc.</span></span>
* <span data-ttu-id="81339-173">[선형 회귀][linear-regression] - 온라인 기울기 하강 기반 선형 회귀 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81339-173">[Linear Regression][linear-regression] - Creates an online gradient descent-based linear regression model.</span></span>
* <span data-ttu-id="81339-174">[모델 점수 매기기][score-model] - 학습된 분류 또는 회귀 모델의 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="81339-174">[Score Model][score-model] - Scores a trained classification or regression model.</span></span>

<span data-ttu-id="81339-175">실험을 만들 때 선택할 수 있습니다 사용할 수 있는 모듈의 hello 목록에서 toohello hello 캔버스의 왼쪽.</span><span class="sxs-lookup"><span data-stu-id="81339-175">As you build an experiment you can choose from hello list of modules available toohello left of hello canvas.</span></span>  

<span data-ttu-id="81339-176">모듈은 tooconfigure hello 모듈의 내부 알고리즘을 사용할 수 있는 매개 변수 집합이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-176">A module may have a set of parameters that you can use tooconfigure hello module's internal algorithms.</span></span> <span data-ttu-id="81339-177">Hello에 hello 모듈의 매개 변수가 표시 됩니다 hello 캔버스에 모듈을 선택 하면 **속성** hello 캔버스의 오른쪽 창 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-177">When you select a module on hello canvas, hello module's parameters are displayed in hello **Properties** pane toohello right of hello canvas.</span></span> <span data-ttu-id="81339-178">모델의 해당 창 tootune hello 매개 변수를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-178">You can modify hello parameters in that pane tootune your model.</span></span>

<span data-ttu-id="81339-179">일부 도움말 탐색 하는 데 사용할 수 있는 기계 학습 알고리즘의 대규모 라이브러리 hello 참조 하세요. [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81339-179">For some help navigating through hello large library of machine learning algorithms available, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>

## <a name="deploying-a-predictive-analytics-web-service"></a><span data-ttu-id="81339-180">예측 분석 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="81339-180">Deploying a predictive analytics web service</span></span>
<span data-ttu-id="81339-181">예측 분석 모델이 준비되면 기계 학습 스튜디오에서 곧바로 해당 모델을 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81339-181">Once your predictive analytics model is ready, you can deploy it as a web service right from Machine Learning Studio.</span></span> <span data-ttu-id="81339-182">이 프로세스에 대한 자세한 내용은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81339-182">For more details on this process, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
