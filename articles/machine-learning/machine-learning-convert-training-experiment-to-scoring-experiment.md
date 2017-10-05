---
title: "Azure Machine Learning Studio에서 배포하기 위한 모델을 준비하는 방법 | Microsoft Docs"
description: "Machine Learning Studio 학습 실험을 예측 실험으로 변환하여 학습된 모델을 웹 서비스로 배포하기 위해 준비하는 방법"
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
ms.openlocfilehash: 716a9a9b723df7ff6eb111fa40f2b5941d57d67a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-prepare-your-model-for-deployment-in-azure-machine-learning-studio"></a><span data-ttu-id="f67bd-103">Azure Machine Learning Studio에서 배포하기 위한 모델을 준비하는 방법</span><span class="sxs-lookup"><span data-stu-id="f67bd-103">How to prepare your model for deployment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="f67bd-104">Azure Machine Learning Studio는 예측 분석 모델을 개발한 다음 Azure 웹 서비스로 배포하여 운영하는 데 필요한 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-104">Azure Machine Learning Studio gives you the tools you need to develop a predictive analytics model and then operationalize it by deploying it as an Azure web service.</span></span>

<span data-ttu-id="f67bd-105">이를 위해 Studio를 사용하여 모델을 학습하고, 점수를 매기고, 편집하는 *학습 실험*이라는 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-105">To do this, you use Studio to create an experiment - called a *training experiment* - where you train, score, and edit your model.</span></span> <span data-ttu-id="f67bd-106">이 학습 실험에 만족하면 사용자 데이터에 대한 점수를 매기도록 구성된 *예측 실험*으로 변환함으로써 모델을 배포할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-106">Once you're satisfied, you get your model ready to deploy by converting your training experiment to a *predictive experiment* that's configured to score user data.</span></span>

<span data-ttu-id="f67bd-107">이 프로세스의 예는 [연습: Azure Machine Learning의 신용 위험 평가에 대한 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-107">You can see an example of this process in [Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

<span data-ttu-id="f67bd-108">이 문서에서는 학습 실험을 예측 실험으로 변환하는 방법과 예측 실험을 배포하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-108">This article takes a deep dive into the details of how a training experiment gets converted into a predictive experiment, and how that predictive experiment is deployed.</span></span> <span data-ttu-id="f67bd-109">이러한 세부 정보를 이해하면 배포된 모델을 더 효과적으로 구성하는 방법을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-109">By understanding these details, you can learn how to configure your deployed model to make it more effective.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="f67bd-110">개요</span><span class="sxs-lookup"><span data-stu-id="f67bd-110">Overview</span></span> 

<span data-ttu-id="f67bd-111">학습 실험을 예측 실험으로 변환하는 프로세스는 세 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-111">The process of converting a training experiment to a predictive experiment involves three steps:</span></span>

1. <span data-ttu-id="f67bd-112">기계 학습 알고리즘 모듈을 학습된 모델로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-112">Replace the machine learning algorithm modules with your trained model.</span></span>
2. <span data-ttu-id="f67bd-113">점수 매기기에 필요한 모듈로만 실험을 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-113">Trim the experiment to only those modules that are needed for scoring.</span></span> <span data-ttu-id="f67bd-114">학습 실험에는 학습에 필요하지만, 모델을 학습한 후에는 필요 없는 여러 모듈이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-114">A training experiment includes a number of modules that are necessary for training but are not needed once the model is trained.</span></span>
3. <span data-ttu-id="f67bd-115">모델에서 웹 서비스 사용자의 데이터를 받아들이는 방법과 반환할 데이터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-115">Define how your model will accept data from the web service user, and what data will be returned.</span></span>

> [!TIP]
> <span data-ttu-id="f67bd-116">학습 실험에서는 사용자 고유의 데이터를 사용하여 모델을 학습하고 점수를 매기는 데 관심이 있지만,</span><span class="sxs-lookup"><span data-stu-id="f67bd-116">In your training experiment, you've been concerned with training and scoring your model using your own data.</span></span> <span data-ttu-id="f67bd-117">일단 배포되면 사용자는 모델에 새 데이터를 보내고, 모델에서는 예측 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-117">But once deployed, users will send new data to your model and it will return prediction results.</span></span> <span data-ttu-id="f67bd-118">따라서 학습 실험을 예측 실험으로 변환하여 배포할 준비가 되면 다른 사용자가 이 모델을 어떻게 사용할지를 명심해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-118">So, as you convert your training experiment to a predictive experiment to get it ready for deployment, keep in mind how the model will be used by others.</span></span>
> 
> 

## <a name="set-up-web-service-button"></a><span data-ttu-id="f67bd-119">웹 서비스 설정 단추</span><span class="sxs-lookup"><span data-stu-id="f67bd-119">Set Up Web Service button</span></span>
<span data-ttu-id="f67bd-120">실험 캔버스 아래쪽의 **실행**을 클릭하여 실험을 실행한 후, **웹 서비스 설정** 단추를 클릭하여 **예측 웹 서비스** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-120">After you run your experiment (click **RUN** at the bottom of the experiment canvas), click the **Set Up Web Service** button (select the **Predictive Web Service** option).</span></span> <span data-ttu-id="f67bd-121">**웹 서비스 설정**에서는 학습 실험을 예측 실험으로 변환하는 세 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-121">**Set Up Web Service** performs for you the three steps of converting your training experiment to a predictive experiment:</span></span>

1. <span data-ttu-id="f67bd-122">모듈 팔레트의 **학습된 모델** 섹션(실험 캔버스의 왼쪽)에 학습된 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-122">It saves your trained model in the **Trained Models** section of the module palette (to the left of the experiment canvas).</span></span> <span data-ttu-id="f67bd-123">그런 다음 기계 학습 알고리즘과 [모델 학습][train-model] 모듈을 저장된 학습 모델로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-123">It then replaces the machine learning algorithm and [Train Model][train-model] modules with the saved trained model.</span></span>
2. <span data-ttu-id="f67bd-124">실험을 분석하고, 분명히 학습에만 사용되었지만 더 이상 필요하지 않은 모듈을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-124">It analyzes your experiment and removes modules that were clearly used only for training and are no longer needed.</span></span>
3. <span data-ttu-id="f67bd-125">_웹 서비스 입력_ 및 _출력_ 모듈을 실험의 기본 위치에 삽입합니다(이러한 모듈은 사용자 데이터를 수락하고 반환합니다).</span><span class="sxs-lookup"><span data-stu-id="f67bd-125">It inserts _Web service input_ and _output_ modules into default locations in your experiment (these modules accept and return user data).</span></span>

<span data-ttu-id="f67bd-126">예를 들어 다음 실험은 샘플 인구 조사 데이터를 사용하여 2클래스 향상된 의사 결정 트리 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-126">For example, the following experiment trains a two-class boosted decision tree model using sample census data:</span></span>

![학습 실험][figure1]

<span data-ttu-id="f67bd-128">이 실험의 모듈은 기본적으로 네 가지 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-128">The modules in this experiment perform basically four different functions:</span></span>

![모듈 함수][figure2]

<span data-ttu-id="f67bd-130">이 학습 실험을 예측 실험으로 변환하면 이러한 모듈 중 일부는 다음과 같이 더 이상 필요하지 않거나 다른 용도로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-130">When you convert this training experiment to a predictive experiment, some of these modules are no longer needed, or they now serve a different purpose:</span></span>

* <span data-ttu-id="f67bd-131">**데이터** - 이 샘플 데이터 집합의 데이터는 점수를 매기는 동안 사용되지 않습니다. 웹 서비스 사용자가 점수를 매길 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-131">**Data** - The data in this sample dataset is not used during scoring - the user of the web service will supply the data to be scored.</span></span> <span data-ttu-id="f67bd-132">그러나 데이터 형식과 같은 이 데이터 집합의 메타데이터는 학습된 모델에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-132">However, the metadata from this dataset, such as data types, is used by the trained model.</span></span> <span data-ttu-id="f67bd-133">따라서 이 메타데이터를 제공할 수 있도록 예측 실험에서 데이터 집합을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-133">So you need to keep the dataset in the predictive experiment so that it can provide this metadata.</span></span>

* <span data-ttu-id="f67bd-134">**준비** - 점수 매기기를 위해 제출할 사용자 데이터에 따라 이러한 모듈이 들어오는 데이터를 처리하는 데 필요할 수도 있고 그렇지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-134">**Prep** - Depending on the user data that will be submitted for scoring, these modules may or may not be necessary to process the incoming data.</span></span> <span data-ttu-id="f67bd-135">**웹 서비스 설정** 단추는 이러한 모듈을 수정하지 않지만, 이들을 처리할 방법은 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-135">The **Set Up Web Service** button doesn't touch these - you need to decide how you want to handle them.</span></span>
  
    <span data-ttu-id="f67bd-136">예를 들어 이 예제에서 샘플 데이터 집합에는 누락된 값이 있을 수 있으므로 이를 처리하기 위해 [누락된 데이터 정리][clean-missing-data] 모듈이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-136">For instance, in this example the sample dataset may have missing values, so a [Clean Missing Data][clean-missing-data] module was included to deal with them.</span></span> <span data-ttu-id="f67bd-137">또한 샘플 데이터 집합에는 모델을 학습하는 데 필요하지 않은 열도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-137">Also, the sample dataset includes columns that are not needed to train the model.</span></span> <span data-ttu-id="f67bd-138">따라서 [데이터 집합의 열 선택][select-columns] 모듈이 데이터 흐름에서 이러한 여분의 열을 제외하기 위해 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-138">So a [Select Columns in Dataset][select-columns] module was included to exclude those extra columns from the data flow.</span></span> <span data-ttu-id="f67bd-139">점수 매기기를 위해 웹 서비스를 통해 제출할 데이터에 누락된 값이 있다는 것을 아는 경우 [누락된 데이터 정리][clean-missing-data] 모듈을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-139">If you know that the data that will be submitted for scoring through the web service will not have missing values, then you can remove the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="f67bd-140">그러나 [데이터 집합의 열 선택][select-columns] 모듈은 학습된 모델에 필요한 데이터 열을 정의하는 데 유용하므로 해당 모듈을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-140">However, since the [Select Columns in Dataset][select-columns] module helps define the columns of data that the trained model expects, that module needs to remain.</span></span>

* <span data-ttu-id="f67bd-141">**학습** - 이러한 모듈은 모델 학습에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-141">**Train** - These modules are used to train the model.</span></span> <span data-ttu-id="f67bd-142">**웹 서비스 설정**을 클릭하면 이러한 모듈이 학습한 모델을 포함하는 단일 모듈로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-142">When you click **Set Up Web Service**, these modules are replaced with a single module that contains the model you trained.</span></span> <span data-ttu-id="f67bd-143">이 새 모듈은 모듈 팔레트의 **학습한 모델** 섹션에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-143">This new module is saved in the **Trained Models** section of the module palette.</span></span>

* <span data-ttu-id="f67bd-144">**점수** - 이 예제에서는 [분할 데이터][split] 모듈을 사용하여 데이터 스트림을 테스트 데이터와 학습 데이터로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-144">**Score** - In this example, the [Split Data][split] module is used to divide the data stream into test data and training data.</span></span> <span data-ttu-id="f67bd-145">예측 실험에서는 더 이상 학습하지 않으므로 [분할 데이터][split]를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-145">In the predictive experiment, we're not training anymore, so [Split Data][split] can be removed.</span></span> <span data-ttu-id="f67bd-146">마찬가지로 두 번째 [모델 점수 매기기][score-model] 모듈 및 [모델 평가][evaluate-model] 모듈을 사용하여 테스트 데이터의 결과를 비교하므로 예측 실험에는 이러한 모듈도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-146">Similarly, the second [Score Model][score-model] module and the [Evaluate Model][evaluate-model] module are used to compare results from the test data, so these modules are not needed in the predictive experiment.</span></span> <span data-ttu-id="f67bd-147">그러나 나머지 [모델 점수 매기기][score-model] 모듈은 웹 서비스를 통해 점수 결과를 반환하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-147">The remaining [Score Model][score-model] module, however, is needed to return a score result through the web service.</span></span>

<span data-ttu-id="f67bd-148">다음은 **웹 서비스 설정**을 클릭한 후 이 예제의 변화된 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-148">Here is how our example looks after clicking **Set Up Web Service**:</span></span>

![변환된 예측 실험][figure3]

<span data-ttu-id="f67bd-150">**웹 서비스 설정**에서 수행한 작업으로 실험을 웹 서비스로 배포하도록 준비하는 데 충분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-150">The work done by **Set Up Web Service** may be sufficient to prepare your experiment to be deployed as a web service.</span></span> <span data-ttu-id="f67bd-151">그러나 실험에 특정한 몇 가지 추가 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-151">However, you may want to do some additional work specific to your experiment.</span></span>

### <a name="adjust-input-and-output-modules"></a><span data-ttu-id="f67bd-152">입력 및 출력 모듈 조정</span><span class="sxs-lookup"><span data-stu-id="f67bd-152">Adjust input and output modules</span></span>
<span data-ttu-id="f67bd-153">학습 실험에서는 학습 데이터 집합을 사용한 다음 일부 처리를 수행하여 기계 학습 알고리즘에 필요한 형식의 데이터를 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-153">In your training experiment, you used a set of training data and then did some processing to get the data in a form that the machine learning algorithm needed.</span></span> <span data-ttu-id="f67bd-154">웹 서비스를 통해 받아야 하는 데이터에 이 처리가 필요하지 않으면 무시할 수 있으며, **웹 서비스 입력 모듈**의 출력을 실험의 다른 모듈에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-154">If the data you expect to receive through the web service will not need this processing, you can bypass it: connect the output of the **Web service input module** to a different module in your experiment.</span></span> <span data-ttu-id="f67bd-155">이제 사용자의 데이터가 이 위치의 모델에 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-155">The user's data will now arrive in the model at this location.</span></span>

<span data-ttu-id="f67bd-156">예를 들어 기본적으로 **웹 서비스 설정**은 위 그림과 같이 **웹 서비스 입력** 모듈을 데이터 흐름의 맨 위에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-156">For example, by default **Set Up Web Service** puts the **Web service input** module at the top of your data flow, as shown in the figure above.</span></span> <span data-ttu-id="f67bd-157">그러나 다음과 같이 **웹 서비스 입력**을 데이터 처리 모듈 뒤에 수동으로 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-157">But we can manually position the **Web service input** past the data processing modules:</span></span>

![웹 서비스 입력 이동][figure4]

<span data-ttu-id="f67bd-159">이제 웹 서비스를 통해 제공되는 입력 데이터가 전처리 없이 모델 점수 매기기 모듈로 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-159">The input data provided through the web service will now pass directly into the Score Model module without any preprocessing.</span></span>

<span data-ttu-id="f67bd-160">마찬가지로 기본적으로 **웹 서비스 설정** 은 웹 서비스 출력 모듈을 데이터 흐름의 맨 아래에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-160">Similarly, by default **Set Up Web Service** puts the Web service output module at the bottom of your data flow.</span></span> <span data-ttu-id="f67bd-161">이 예제에서 웹 서비스는 사용자에게 전체 입력 데이터 벡터와 점수 매기기 결과가 포함된 [모델 점수 매기기][score-model] 모듈을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-161">In this example, the web service will return to the user the output of the [Score Model][score-model] module, which includes the complete input data vector plus the scoring results.</span></span>
<span data-ttu-id="f67bd-162">그러나 다른 모듈을 반환하고 싶은 경우에는 **웹 서비스 출력** 모듈 앞에 모듈을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-162">However, if you would prefer to return something different, then you can add additional modules before the **Web service output** module.</span></span> 

<span data-ttu-id="f67bd-163">예를 들어 입력 데이터의 전체 벡터가 아닌 점수 매기기 결과만 반환하려면 [데이터 집합의 열 선택][select-columns] 모듈을 추가하여 점수 매기기 결과를 제외한 모든 열을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-163">For example, to return only the scoring results and not the entire vector of input data, add a [Select Columns in Dataset][select-columns] module to exclude all columns except the scoring results.</span></span> <span data-ttu-id="f67bd-164">그런 다음 **웹 서비스 출력** 모듈을 [데이터 집합의 열 선택][select-columns] 모듈의 출력으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-164">Then move the **Web service output** module to the output of the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="f67bd-165">실험은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-165">The experiment looks like this:</span></span>

![웹 서비스 출력 이동][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a><span data-ttu-id="f67bd-167">추가 데이터 처리 모듈 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="f67bd-167">Add or remove additional data processing modules</span></span>
<span data-ttu-id="f67bd-168">점수를 매기는 동안 필요 없다는 것을 알고 있는 추가 모듈이 실험에 있는 경우 이러한 모듈을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-168">If there are more modules in your experiment that you know will not be needed during scoring, these can be removed.</span></span> <span data-ttu-id="f67bd-169">예를 들어 **웹 서비스 입력** 모듈을 데이터 처리 모듈 이후의 시점으로 이동했기 때문에 예측 실험에서 [누락된 데이터 정리][clean-missing-data] 모듈을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-169">For example, because we moved the **Web service input** module to a point after the data processing modules, we can remove the [Clean Missing Data][clean-missing-data] module from the predictive experiment.</span></span>

<span data-ttu-id="f67bd-170">이제 예측 실험은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-170">Our predictive experiment now looks like this:</span></span>

![추가 모듈 제거][figure6]


### <a name="add-optional-web-service-parameters"></a><span data-ttu-id="f67bd-172">선택적 웹 서비스 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="f67bd-172">Add optional Web Service Parameters</span></span>
<span data-ttu-id="f67bd-173">경우에 따라 서비스에 액세스할 때 웹 서비스 사용자가 모듈의 동작을 변경하도록 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-173">In some cases, you may want to allow the user of your web service to change the behavior of modules when the service is accessed.</span></span> <span data-ttu-id="f67bd-174">*웹 서비스 매개 변수* 를 통해 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-174">*Web Service Parameters* allow you to do this.</span></span>

<span data-ttu-id="f67bd-175">일반적인 예는 배포된 웹 서비스에 액세스할 때 해당 웹 서비스의 사용자가 다른 데이터 원본을 지정할 수 있도록 [데이터 가져오기][import-data] 모듈을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-175">A common example is setting up an [Import Data][import-data] module so the user of the deployed web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="f67bd-176">또는 다른 대상을 지정할 수 있도록 [데이터 내보내기][export-data] 모듈을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-176">Or configuring an [Export Data][export-data] module so that a different destination can be specified.</span></span>

<span data-ttu-id="f67bd-177">웹 서비스 매개 변수를 정의하여 하나 이상의 모듈 매개 변수와 연결하고 이러한 매개 변수가 필수인지 또는 선택 사항인지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-177">You can define Web Service Parameters and associate them with one or more module parameters, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="f67bd-178">웹 서비스의 사용자는 서비스에 액세스할 때 이러한 매개 변수의 값을 제공하며, 이에 따라 모듈 작업이 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-178">The user of the web service provides values for these parameters when the service is accessed, and the module actions are modified accordingly.</span></span>

<span data-ttu-id="f67bd-179">웹 서비스 매개 변수 및 사용 방법에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 매개 변수 사용][webserviceparameters]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f67bd-179">For more information about what Web Service Parameters are and how to use them, see [Using Azure Machine Learning Web Service Parameters][webserviceparameters].</span></span>

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-the-predictive-experiment-as-a-web-service"></a><span data-ttu-id="f67bd-180">예측 실험을 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="f67bd-180">Deploy the predictive experiment as a web service</span></span>
<span data-ttu-id="f67bd-181">이제 예측 실험이 충분히 준비되었으므로 이를 Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-181">Now that the predictive experiment has been sufficiently prepared, you can deploy it as an Azure web service.</span></span> <span data-ttu-id="f67bd-182">웹 서비스를 사용하면 사용자가 모델에 데이터를 보낼 수 있으며, 이 경우 모델에서 해당 예측을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f67bd-182">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="f67bd-183">전체 배포 프로세스에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포][deploy]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f67bd-183">For more information on the complete deployment process, see [Deploy an Azure Machine Learning web service][deploy]</span></span>

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
