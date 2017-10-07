---
title: "aaaHow tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델 | Microsoft Docs"
description: "변환 하 여 tooprepare 웹 배포에 대 한 학습 된 모델 서비스 방법 기계 학습 스튜디오 학습 tooa 예측 실험을 시험 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a><span data-ttu-id="89a9f-103">어떻게 tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델</span><span class="sxs-lookup"><span data-stu-id="89a9f-103">How tooprepare your model for deployment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="89a9f-104">Azure 기계 학습 스튜디오에서는 도구는 예측 분석 모델 toodevelop 필요 하 고 다음 Azure 웹 서비스로 배포 하 여 운영 화 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-104">Azure Machine Learning Studio gives you hello tools you need toodevelop a predictive analytics model and then operationalize it by deploying it as an Azure web service.</span></span>

<span data-ttu-id="89a9f-105">toodo이 Studio toocreate 실험-호출을 사용 하 여 한 *학습 실험* -학습, 점수를 매길 하 고 있는 모델을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-105">toodo this, you use Studio toocreate an experiment - called a *training experiment* - where you train, score, and edit your model.</span></span> <span data-ttu-id="89a9f-106">학습 실험 tooa 변환 하 여 모델 준비 toodeploy 얻게를 마치면 *예측 실험* 가 tooscore 사용자 데이터를 구성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-106">Once you're satisfied, you get your model ready toodeploy by converting your training experiment tooa *predictive experiment* that's configured tooscore user data.</span></span>

<span data-ttu-id="89a9f-107">이 프로세스의 예는 [연습: Azure Machine Learning의 신용 위험 평가에 대한 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-107">You can see an example of this process in [Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

<span data-ttu-id="89a9f-108">이 문서에서는 해당 예측 실험 배포 방법으로 학습 실험 예측 실험으로 변환 방법의 hello 세부 정보를 심층 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-108">This article takes a deep dive into hello details of how a training experiment gets converted into a predictive experiment, and how that predictive experiment is deployed.</span></span> <span data-ttu-id="89a9f-109">이러한 세부 정보를 이해 하면 학습할 수 있는 방법을 tooconfigure 배포 된 모델 toomake 것이 더 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-109">By understanding these details, you can learn how tooconfigure your deployed model toomake it more effective.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="89a9f-110">개요</span><span class="sxs-lookup"><span data-stu-id="89a9f-110">Overview</span></span> 

<span data-ttu-id="89a9f-111">hello 변환 프로세스를 학습의 실험 tooa 예측 실험에는 세 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-111">hello process of converting a training experiment tooa predictive experiment involves three steps:</span></span>

1. <span data-ttu-id="89a9f-112">Hello 컴퓨터 학습 알고리즘 모듈 학습 된 모델을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-112">Replace hello machine learning algorithm modules with your trained model.</span></span>
2. <span data-ttu-id="89a9f-113">Hello 실험 tooonly 점수 매기기에 필요한 모듈을 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-113">Trim hello experiment tooonly those modules that are needed for scoring.</span></span> <span data-ttu-id="89a9f-114">학습 실험에는 다양 한 모듈 학습 시에 필요 하지만 hello 모델을 학습 한 후에 필요 하지 않은 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-114">A training experiment includes a number of modules that are necessary for training but are not needed once hello model is trained.</span></span>
3. <span data-ttu-id="89a9f-115">어떤 데이터를 반환할 인트라넷과 모델을 hello 웹 서비스 사용자의 데이터를 수락 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-115">Define how your model will accept data from hello web service user, and what data will be returned.</span></span>

> [!TIP]
> <span data-ttu-id="89a9f-116">학습 실험에서는 사용자 고유의 데이터를 사용하여 모델을 학습하고 점수를 매기는 데 관심이 있지만,</span><span class="sxs-lookup"><span data-stu-id="89a9f-116">In your training experiment, you've been concerned with training and scoring your model using your own data.</span></span> <span data-ttu-id="89a9f-117">하지만 배포 된 후 사용자는 새 데이터 tooyour 모델 보냅니다 하 고 예측 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-117">But once deployed, users will send new data tooyour model and it will return prediction results.</span></span> <span data-ttu-id="89a9f-118">따라서 배포에 대 한 준비 프로그램 학습 실험 tooa 예측 실험 tooget을 변환할 때 염두에서에 둬야 hello 모델의 용도 다른 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-118">So, as you convert your training experiment tooa predictive experiment tooget it ready for deployment, keep in mind how hello model will be used by others.</span></span>
> 
> 

## <a name="set-up-web-service-button"></a><span data-ttu-id="89a9f-119">웹 서비스 설정 단추</span><span class="sxs-lookup"><span data-stu-id="89a9f-119">Set Up Web Service button</span></span>
<span data-ttu-id="89a9f-120">실험을 실행 한 후 (클릭 **실행** hello hello 실험 캔버스 맨 아래에), hello 클릭 **웹 서비스 설정** 단추 (선택 hello **예측 웹 서비스** 옵션)입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-120">After you run your experiment (click **RUN** at hello bottom of hello experiment canvas), click hello **Set Up Web Service** button (select hello **Predictive Web Service** option).</span></span> <span data-ttu-id="89a9f-121">**웹 서비스 설정** 는 학습 실험 tooa 예측 실험으로 변환의 세 단계 hello에 대해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-121">**Set Up Web Service** performs for you hello three steps of converting your training experiment tooa predictive experiment:</span></span>

1. <span data-ttu-id="89a9f-122">학습 된 모델 hello 저장 **학습 된 모델** hello 모듈 색상표 (hello 실험 캔버스의 왼쪽 toohello)의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-122">It saves your trained model in hello **Trained Models** section of hello module palette (toohello left of hello experiment canvas).</span></span> <span data-ttu-id="89a9f-123">다음 hello 기계 학습 알고리즘을 대체 하 고 [모델 학습] [ train-model] 여러 모듈을 저장 하는 hello 학습 된 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-123">It then replaces hello machine learning algorithm and [Train Model][train-model] modules with hello saved trained model.</span></span>
2. <span data-ttu-id="89a9f-124">실험을 분석하고, 분명히 학습에만 사용되었지만 더 이상 필요하지 않은 모듈을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-124">It analyzes your experiment and removes modules that were clearly used only for training and are no longer needed.</span></span>
3. <span data-ttu-id="89a9f-125">_웹 서비스 입력_ 및 _출력_ 모듈을 실험의 기본 위치에 삽입합니다(이러한 모듈은 사용자 데이터를 수락하고 반환합니다).</span><span class="sxs-lookup"><span data-stu-id="89a9f-125">It inserts _Web service input_ and _output_ modules into default locations in your experiment (these modules accept and return user data).</span></span>

<span data-ttu-id="89a9f-126">예를 들어 hello 다음 샘플 인구 조사 데이터를 사용 하 여 2 클래스 승격 된 의사 결정 트리 모델 기차를 실험:</span><span class="sxs-lookup"><span data-stu-id="89a9f-126">For example, hello following experiment trains a two-class boosted decision tree model using sample census data:</span></span>

![학습 실험][figure1]

<span data-ttu-id="89a9f-128">기본적으로 4 개의 다른 기능을 수행 하는이 실험에서 모듈 hello:</span><span class="sxs-lookup"><span data-stu-id="89a9f-128">hello modules in this experiment perform basically four different functions:</span></span>

![모듈 함수][figure2]

<span data-ttu-id="89a9f-130">이 학습 실험 tooa 예측 실험으로 변환 하면 더 이상 필요 없는 이러한 모듈 중 일부를 또는 다른 목적을 이제 사용:</span><span class="sxs-lookup"><span data-stu-id="89a9f-130">When you convert this training experiment tooa predictive experiment, some of these modules are no longer needed, or they now serve a different purpose:</span></span>

* <span data-ttu-id="89a9f-131">**데이터** -hello 데이터가이 예제 데이터 집합에 점수 매기기 하는 동안 사용 되지 않는-hello 웹 서비스의 hello 사용자 hello 데이터 toobe 점수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-131">**Data** - hello data in this sample dataset is not used during scoring - hello user of hello web service will supply hello data toobe scored.</span></span> <span data-ttu-id="89a9f-132">그러나 데이터 형식과 같은이 데이터 집합에서 메타 데이터를 hello hello 학습 된 모델에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-132">However, hello metadata from this dataset, such as data types, is used by hello trained model.</span></span> <span data-ttu-id="89a9f-133">이 메타 데이터를 제공할 수 있도록 hello 예측 실험에서 tookeep hello 데이터 집합을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-133">So you need tookeep hello dataset in hello predictive experiment so that it can provide this metadata.</span></span>

* <span data-ttu-id="89a9f-134">**필수 구성 요소** -이러한 모듈 되거나 되지 않을 수 있습니다 필요한 tooprocess hello 들어오는 데이터, 점수를 매기기 위해 제출할 hello 사용자 데이터에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-134">**Prep** - Depending on hello user data that will be submitted for scoring, these modules may or may not be necessary tooprocess hello incoming data.</span></span> <span data-ttu-id="89a9f-135">hello **웹 서비스 설정** 이러한 단추 터치 하지 않는-toodecide 해야 원하는 toohandle 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-135">hello **Set Up Web Service** button doesn't touch these - you need toodecide how you want toohandle them.</span></span>
  
    <span data-ttu-id="89a9f-136">예를 들어,이 예에서 hello 샘플 데이터 집합 개일 수 누락 값 있으므로 [누락 데이터 정리] [ clean-missing-data] 모듈을 포함된 toodeal 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-136">For instance, in this example hello sample dataset may have missing values, so a [Clean Missing Data][clean-missing-data] module was included toodeal with them.</span></span> <span data-ttu-id="89a9f-137">또한 hello 샘플 데이터 집합은 필요한 tootrain hello 모델 열에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-137">Also, hello sample dataset includes columns that are not needed tootrain hello model.</span></span> <span data-ttu-id="89a9f-138">따라서 한 [데이터 집합의 열 선택] [ select-columns] 에서 이러한 추가 열 포함된 tooexclude 된 모듈이 데이터 흐름 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-138">So a [Select Columns in Dataset][select-columns] module was included tooexclude those extra columns from hello data flow.</span></span> <span data-ttu-id="89a9f-139">점수를 매기기 위해 제출할 hello 데이터를 알고 있는 경우 hello를 통해 웹 서비스에 포함 되지 누락 값을 다음 hello를 제거할 수 있습니다 [누락 데이터 정리] [ clean-missing-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-139">If you know that hello data that will be submitted for scoring through hello web service will not have missing values, then you can remove hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="89a9f-140">그러나 hello 이후 [데이터 집합의 열을 선택] [ select-columns] 모듈을 사용 하면 hello 열 정의 데이터의 해당 hello 학습 된 모델에는 해당 모듈 tooremain 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-140">However, since hello [Select Columns in Dataset][select-columns] module helps define hello columns of data that hello trained model expects, that module needs tooremain.</span></span>

* <span data-ttu-id="89a9f-141">**학습** -이러한 모듈은 사용 되는 tootrain hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-141">**Train** - These modules are used tootrain hello model.</span></span> <span data-ttu-id="89a9f-142">클릭할 때 **웹 서비스 설정**, 이러한 모듈을 학습할 hello 모델이 포함 된 단일 모듈으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-142">When you click **Set Up Web Service**, these modules are replaced with a single module that contains hello model you trained.</span></span> <span data-ttu-id="89a9f-143">이 새 모듈 hello에 저장 된 **학습 된 모델** hello 모듈 색상표의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-143">This new module is saved in hello **Trained Models** section of hello module palette.</span></span>

* <span data-ttu-id="89a9f-144">**점수** -이 예제에서는 hello [분할 데이터] [ split] 모듈에는 테스트 데이터 및 학습 데이터에 사용 되는 toodivide hello 데이터 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-144">**Score** - In this example, hello [Split Data][split] module is used toodivide hello data stream into test data and training data.</span></span> <span data-ttu-id="89a9f-145">Hello 예측 실험에서 우리는 하지 교육 더 이상 그렇게 [분할 데이터] [ split] 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-145">In hello predictive experiment, we're not training anymore, so [Split Data][split] can be removed.</span></span> <span data-ttu-id="89a9f-146">마찬가지로, 두 번째 hello [모델 점수 매기기] [ score-model] 모듈과 hello [모델 평가] [ evaluate-model] 모듈은 hello 테스트에서 사용 되는 toocompare 결과 데이터를 이러한 모듈은 필요한 hello 예측에 시험 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-146">Similarly, hello second [Score Model][score-model] module and hello [Evaluate Model][evaluate-model] module are used toocompare results from hello test data, so these modules are not needed in hello predictive experiment.</span></span> <span data-ttu-id="89a9f-147">hello 남은 [모델 점수 매기기] [ score-model] 모듈 인데 필요한 tooreturn hello 웹 서비스를 통해 점수 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-147">hello remaining [Score Model][score-model] module, however, is needed tooreturn a score result through hello web service.</span></span>

<span data-ttu-id="89a9f-148">다음은 **웹 서비스 설정**을 클릭한 후 이 예제의 변화된 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-148">Here is how our example looks after clicking **Set Up Web Service**:</span></span>

![변환된 예측 실험][figure3]

<span data-ttu-id="89a9f-150">수행 된 작업 hello **웹 서비스 설정** 충분 한 tooprepare 웹 서비스로 배포 하 여 실험 toobe 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-150">hello work done by **Set Up Web Service** may be sufficient tooprepare your experiment toobe deployed as a web service.</span></span> <span data-ttu-id="89a9f-151">그러나, 몇 가지 추가 작업 특정 tooyour 실험 toodo를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-151">However, you may want toodo some additional work specific tooyour experiment.</span></span>

### <a name="adjust-input-and-output-modules"></a><span data-ttu-id="89a9f-152">입력 및 출력 모듈 조정</span><span class="sxs-lookup"><span data-stu-id="89a9f-152">Adjust input and output modules</span></span>
<span data-ttu-id="89a9f-153">학습 실험에서 학습 데이터 집합을 사용 하 고 일부 처리 tooget 않은 기계 학습 알고리즘 필요한 hello는 폼의 데이터를 hello 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-153">In your training experiment, you used a set of training data and then did some processing tooget hello data in a form that hello machine learning algorithm needed.</span></span> <span data-ttu-id="89a9f-154">Tooreceive hello 웹 서비스를 통해 원하는 hello 데이터에서이 처리를 필요로 하는 경우 파일을 무시할 수: hello hello 출력에 연결 **웹 서비스에 대 한 입력된 모듈** tooa 실험의 다른 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-154">If hello data you expect tooreceive through hello web service will not need this processing, you can bypass it: connect hello output of hello **Web service input module** tooa different module in your experiment.</span></span> <span data-ttu-id="89a9f-155">hello 사용자의 데이터는 이제 hello 모델이이 위치에 도착 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-155">hello user's data will now arrive in hello model at this location.</span></span>

<span data-ttu-id="89a9f-156">예를 들어 기본적으로 **웹 서비스 설정** 넣습니다 hello **웹 서비스 입력** hello 맨 위의 hello 그림에 나와 있는 것 처럼, 데이터 흐름에 있는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-156">For example, by default **Set Up Web Service** puts hello **Web service input** module at hello top of your data flow, as shown in hello figure above.</span></span> <span data-ttu-id="89a9f-157">Hello을 수동으로 배치할 수 있습니다 하지만 **웹 서비스 입력** hello 데이터 처리 모듈을 지 나:</span><span class="sxs-lookup"><span data-stu-id="89a9f-157">But we can manually position hello **Web service input** past hello data processing modules:</span></span>

![이동 hello 웹 서비스 입력][figure4]

<span data-ttu-id="89a9f-159">hello는 hello를 통해 웹 서비스는 이제 전달 hello 모델 점수 매기기 모듈에 직접 전처리 없이 제공 된 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-159">hello input data provided through hello web service will now pass directly into hello Score Model module without any preprocessing.</span></span>

<span data-ttu-id="89a9f-160">마찬가지로, 기본적으로 **웹 서비스 설정** 넣습니다 hello 데이터 흐름의 hello 맨 아래에 웹 서비스 출력 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-160">Similarly, by default **Set Up Web Service** puts hello Web service output module at hello bottom of your data flow.</span></span> <span data-ttu-id="89a9f-161">Hello 웹 서비스는 hello의 toohello 사용자 hello 출력을 반환 하는 데이 예제에서는 [모델 점수 매기기] [ score-model] hello 전체 입력된 데이터 벡터를 더한 결과 점수 매기기 hello를 포함 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-161">In this example, hello web service will return toohello user hello output of hello [Score Model][score-model] module, which includes hello complete input data vector plus hello scoring results.</span></span>
<span data-ttu-id="89a9f-162">그러나 사용 하려는 tooreturn 사항이 서로 다른 경우 다음 추가할 수 있습니다 hello 하기 전에 추가 모듈 **웹 서비스 출력** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-162">However, if you would prefer tooreturn something different, then you can add additional modules before hello **Web service output** module.</span></span> 

<span data-ttu-id="89a9f-163">Tooreturn만 hello 점수 매기기 결과 전체 벡터 입력된 데이터의 hello 추가 하는 예를 들어 한 [데이터 집합의 열 선택] [ select-columns] 를 제외한 모든 열 hello 결과 점수 매기기 모듈 tooexclude 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-163">For example, tooreturn only hello scoring results and not hello entire vector of input data, add a [Select Columns in Dataset][select-columns] module tooexclude all columns except hello scoring results.</span></span> <span data-ttu-id="89a9f-164">다음 hello 이동 **웹 서비스 출력** 모듈 toohello 출력의 hello [데이터 집합의 열을 선택] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-164">Then move hello **Web service output** module toohello output of hello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="89a9f-165">hello 실험은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-165">hello experiment looks like this:</span></span>

![Hello 웹 서비스 출력 이동][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a><span data-ttu-id="89a9f-167">추가 데이터 처리 모듈 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="89a9f-167">Add or remove additional data processing modules</span></span>
<span data-ttu-id="89a9f-168">점수를 매기는 동안 필요 없다는 것을 알고 있는 추가 모듈이 실험에 있는 경우 이러한 모듈을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-168">If there are more modules in your experiment that you know will not be needed during scoring, these can be removed.</span></span> <span data-ttu-id="89a9f-169">예를 들어 hello를 이동 하기 때문에 **웹 서비스 입력** hello 모듈을 처리 하는 데이터를 제거할 수 있습니다 hello 가리킨 다음 모듈 tooa [누락 데이터 정리] [ clean-missing-data] 에서 모듈 실험을 예측 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-169">For example, because we moved hello **Web service input** module tooa point after hello data processing modules, we can remove hello [Clean Missing Data][clean-missing-data] module from hello predictive experiment.</span></span>

<span data-ttu-id="89a9f-170">이제 예측 실험은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-170">Our predictive experiment now looks like this:</span></span>

![추가 모듈 제거][figure6]


### <a name="add-optional-web-service-parameters"></a><span data-ttu-id="89a9f-172">선택적 웹 서비스 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="89a9f-172">Add optional Web Service Parameters</span></span>
<span data-ttu-id="89a9f-173">일부 경우에 hello 서비스에 액세스할 때 모듈의 웹 서비스 toochange hello 동작의 tooallow hello 사용자를 있습니다 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-173">In some cases, you may want tooallow hello user of your web service toochange hello behavior of modules when hello service is accessed.</span></span> <span data-ttu-id="89a9f-174">*웹 서비스 매개 변수* toodo 사용 하면이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-174">*Web Service Parameters* allow you toodo this.</span></span>

<span data-ttu-id="89a9f-175">일반적인 예로를 설정 하 고는 [데이터 가져오기] [ import-data] 모듈의 hello hello 사용자는 웹 서비스를 배포 하도록 hello 웹 서비스에 액세스할 때 다른 데이터 원본을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-175">A common example is setting up an [Import Data][import-data] module so hello user of hello deployed web service can specify a different data source when hello web service is accessed.</span></span> <span data-ttu-id="89a9f-176">또는 다른 대상을 지정할 수 있도록 [데이터 내보내기][export-data] 모듈을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-176">Or configuring an [Export Data][export-data] module so that a different destination can be specified.</span></span>

<span data-ttu-id="89a9f-177">웹 서비스 매개 변수를 정의하여 하나 이상의 모듈 매개 변수와 연결하고 이러한 매개 변수가 필수인지 또는 선택 사항인지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-177">You can define Web Service Parameters and associate them with one or more module parameters, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="89a9f-178">hello 웹 서비스의 hello 사용자 hello 서비스에 액세스 하는 hello 모듈 동작을 적절 하 게 수정 되 고 이러한 매개 변수에 대해 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-178">hello user of hello web service provides values for these parameters when hello service is accessed, and hello module actions are modified accordingly.</span></span>

<span data-ttu-id="89a9f-179">어떤 웹 서비스 매개 변수에 대 한 자세한 정보는 어떻게 toouse, 참조에 대 한 [를 사용 하 여 Azure 컴퓨터 학습 웹 서비스 매개 변수가][webserviceparameters]합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-179">For more information about what Web Service Parameters are and how toouse them, see [Using Azure Machine Learning Web Service Parameters][webserviceparameters].</span></span>

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a><span data-ttu-id="89a9f-180">Hello 예측 실험을 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="89a9f-180">Deploy hello predictive experiment as a web service</span></span>
<span data-ttu-id="89a9f-181">Hello 예측 실험 충분히 준비 하는 Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-181">Now that hello predictive experiment has been sufficiently prepared, you can deploy it as an Azure web service.</span></span> <span data-ttu-id="89a9f-182">Hello 웹 서비스를 사용 하면 데이터 tooyour 모델을 보낼 수 있습니다 및 hello 모델의 예측이 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a9f-182">Using hello web service, users can send data tooyour model and hello model will return its predictions.</span></span>

<span data-ttu-id="89a9f-183">Hello 완전 한 배포 프로세스에 대 한 자세한 내용은 참조 하세요. [Azure 기계 학습 웹 서비스 배포][deploy]</span><span class="sxs-lookup"><span data-stu-id="89a9f-183">For more information on hello complete deployment process, see [Deploy an Azure Machine Learning web service][deploy]</span></span>

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
