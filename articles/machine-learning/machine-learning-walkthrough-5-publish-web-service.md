---
title: "5단계: Machine Learning 웹 서비스 배포 | Microsoft Docs"
description: "예측 솔루션 개발 연습 5단계: Azure 기계 학습 스튜디오에서 예측 실험을 웹 서비스로 배포합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="394fe-103">연습 5단계: Azure 기계 학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="394fe-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="394fe-104">[Azure 기계 학습에서 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="394fe-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="394fe-105">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="394fe-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="394fe-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="394fe-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="394fe-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="394fe-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="394fe-108">모델 학습 및 평가</span><span class="sxs-lookup"><span data-stu-id="394fe-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="394fe-109">**웹 서비스 배포**</span><span class="sxs-lookup"><span data-stu-id="394fe-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="394fe-110">웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="394fe-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="394fe-111">다른 사용자가 이 연습에서 개발한 예측 모델을 사용할 수 있도록 Azure의 웹 서비스로 배포할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="394fe-112">지금까지는 모델을 학습하는 실험을 진행했습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="394fe-113">하지만 배포된 서비스는 더 이상 학습을 수행하지 않고 모델에 따라 사용자 입력의 점수를 매겨서 새 예측을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="394fe-114">그러므로 몇 가지 예측을 수행하여 ***학습*** 실험을 ***예측*** 실험으로 변환하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="394fe-115">이 작업은 세 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="394fe-116">모델 중 하나 제거</span><span class="sxs-lookup"><span data-stu-id="394fe-116">Remove one of the models</span></span>
2. <span data-ttu-id="394fe-117">만든 *학습 실험*을 *예측 실험*으로 변환</span><span class="sxs-lookup"><span data-stu-id="394fe-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="394fe-118">예측 실험을 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="394fe-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="394fe-119">모델 중 하나 제거</span><span class="sxs-lookup"><span data-stu-id="394fe-119">Remove one of the models</span></span>

<span data-ttu-id="394fe-120">먼저 이 실험을 약간 간단히 줄여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="394fe-121">현재 실험에는 두 개의 다른 모델이 있지만 웹 서비스로 배포할 때는 하나의 모델만을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="394fe-122">우리는 향상된 트리 모델이 SVM 모델보다 더 효율적으로 수행되었다는 결론을 내리게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="394fe-123">가장 먼저 수행할 작업은 [2클래스 Support Vector Machine][two-class-support-vector-machine] 모듈과 학습에 사용된 모듈을 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="394fe-124">먼저 실험 캔버스 아래쪽에 있는 **다른 이름으로 저장**을 클릭하여 실험 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="394fe-125">다음 모듈을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="394fe-126">[2클래스 Support Vector Machine][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="394fe-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="394fe-127">연결된 [모델 학습][train-model] 및 [모델 점수 매기기][score-model] 모듈</span><span class="sxs-lookup"><span data-stu-id="394fe-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="394fe-128">[데이터 표준화][normalize-data](둘 다)</span><span class="sxs-lookup"><span data-stu-id="394fe-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="394fe-129">[모델 평가][evaluate-model](모델 평가를 완료했으므로)</span><span class="sxs-lookup"><span data-stu-id="394fe-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="394fe-130">각 모듈을 선택하고 Delete 키를 누르거나 모듈을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![SVM 모델 제거됨][3a]

<span data-ttu-id="394fe-132">모델은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-132">Our model should now look something like this:</span></span>

![SVM 모델 제거됨][3]

<span data-ttu-id="394fe-134">이제 [2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree]를 사용하여 이 모듈을 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="394fe-135">학습 실험에서 예측 실험으로 변환</span><span class="sxs-lookup"><span data-stu-id="394fe-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="394fe-136">이 모델을 배포하도록 준비하려면 이 학습 실험을 예측 실험으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="394fe-137">이는 세 가지 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-137">This involves three steps:</span></span>

1. <span data-ttu-id="394fe-138">학습한 모델을 저장한 다음 학습 모듈 바꾸기</span><span class="sxs-lookup"><span data-stu-id="394fe-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="394fe-139">학습에만 필요한 모듈을 제거하여 실험 축소</span><span class="sxs-lookup"><span data-stu-id="394fe-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="394fe-140">웹 서비스에서 입력을 수락할 위치 및 출력을 생성할 위치 정의</span><span class="sxs-lookup"><span data-stu-id="394fe-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="394fe-141">이 작업을 수동으로 수행할 수 있으나 다행히도 실험 캔버스의 맨 아래에 있는 **웹 서비스 설정**을 클릭하여 세 단계를 모두 수행할 수 있습니다(및 **예측 웹 서비스** 옵션 선택).</span><span class="sxs-lookup"><span data-stu-id="394fe-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="394fe-142">학습 실험을 예측 실험으로 변환할 때 발생하는 결과를 자세히 알아보려면 [Azure Machine Learning Studio에서 배포 모델을 준비하는 방법](machine-learning-convert-training-experiment-to-scoring-experiment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="394fe-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="394fe-143">**웹 서비스 설정**을 클릭하면 다음과 같은 결과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="394fe-144">학습한 모델이 단일 **학습된 모델** 모듈로 변환된 후 실험 캔버스 왼쪽의 모듈 팔레트에 저장됩니다(**학습된 모델** 아래에서 찾을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="394fe-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="394fe-145">다음을 비롯하여 학습에 사용된 모듈은 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="394fe-146">[2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="394fe-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="394fe-147">[모델 학습][train-model]</span><span class="sxs-lookup"><span data-stu-id="394fe-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="394fe-148">[데이터 분할][split]</span><span class="sxs-lookup"><span data-stu-id="394fe-148">[Split Data][split]</span></span>
  * <span data-ttu-id="394fe-149">테스트 데이터에 사용된 두 번째 [R 스크립트 실행][execute-r-script] 모듈</span><span class="sxs-lookup"><span data-stu-id="394fe-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="394fe-150">저장된 학습된 모델이 실험에 다시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="394fe-151">**웹 서비스 입력** 및 **웹 서비스 출력** 모듈이 추가됩니다(이러한 모듈은 사용자 데이터가 모델에 입력되는 위치, 반환된 데이터, 웹 서비스가 액세스되는 경우를 식별함).</span><span class="sxs-lookup"><span data-stu-id="394fe-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="394fe-152">실험이 탭 아래에 두 부분으로 저장되고 실험 캔버스 위쪽에 추가되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="394fe-153">원래 학습 실험은 **학습 실험** 탭 아래에 표시되고, 새로 만든 예측 실험은 **예측 실험** 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="394fe-154">예측 실험은 웹 서비스로 배포하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="394fe-155">이 특정 실험과 함께 하나의 추가 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="394fe-156">두 개의 [R 스크립트 실행][execute-r-script] 모듈을 추가하여 데이터에 가중치 기능을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="394fe-157">이 모듈은 학습 및 테스트에만 필요하므로 최종 모델에서는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="394fe-158">Machine Learning Studio는 [분할][split] 모듈을 제거할 때 [R 스크립트 실행][execute-r-script] 모듈을 하나 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="394fe-159">이제 다른 모듈을 제거하고 [메타데이터 편집기][metadata-editor]를 [모델 점수 매기기][score-model]에 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="394fe-160">이제 실험은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-160">Our experiment should now look like this:</span></span>  

![학습된 모델 점수 매기기][4]  

> [!NOTE]
> <span data-ttu-id="394fe-162">예측 실험에서 UCI 독일어 신용 카드 데이터의 데이터 집합을 남겨둔 이유가 궁금할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="394fe-163">서비스에서는 원래 데이터 집합이 아니라 사용자 데이터를 사용하려고 하는데 모델에 원래 데이터 집합으로 두는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="394fe-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="394fe-164">서비스에 원래 신용 카드 데이터가 필요하지 않은 것은 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="394fe-165">하지만 열 수 및 숫자인 열 같은 정보가 포함된 해당 데이터에 대한 스키마는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="394fe-166">이 스키마 정보는 사용자 데이터를 해석하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="394fe-167">서비스가 실행 중일 때 점수 매기기 모듈에 데이터 집합 스키마가 포함되도록 이러한 구성 요소를 연결된 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="394fe-168">데이터는 사용되지 않고 스키마만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="394fe-169">마지막으로 실험을 한 번 실행합니다(**실행** 클릭). 모델이 계속 작동 중인지 확인하려면 [모델 점수 매기기][score-model] 모듈의 출력을 클릭하고 **결과 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="394fe-170">원래 데이터가 신용 위험 값("점수를 매긴 레이블") 및 점수 매기기 확률 값("점수를 매긴 확률")과 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="394fe-171">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="394fe-171">Deploy the web service</span></span>
<span data-ttu-id="394fe-172">실험을 Azure Resource Manager에 기반하는 기존 웹 서비스 또는 새 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="394fe-173">기존 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="394fe-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="394fe-174">실험에서 파생된 기존 웹 서비스를 배포하려면 캔버스에서 **웹 서비스 배포**를 클릭하고 **웹 서비스 배포[기존]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="394fe-175">기계 학습 스튜디오에서 실험을 웹 서비스로 배포하고 웹 서비스에 대한 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="394fe-176">이 페이지에서 실험으로 돌아가서(**스냅숏 보기** 또는 **최신 항목 보기**) 간단한 웹 서비스 테스트를 실행할 수 있습니다(아래 **웹 서비스 테스트** 참조).</span><span class="sxs-lookup"><span data-stu-id="394fe-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="394fe-177">여기에는 웹 서비스에 액세스할 수 있는 응용 프로그램을 만들기 위한 정보도 있습니다. 자세한 내용은 이 연습의 다음 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="394fe-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![웹 서비스 대시보드][6]

<span data-ttu-id="394fe-179">**구성** 탭을 클릭하여 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="394fe-180">여기서 서비스 이름(기본적으로 실험 이름이 지정됨)을 수정하고 설명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="394fe-181">입력 및 출력 데이터에 대해 더 친숙한 레이블을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-181">You can also give more friendly labels for the input and output data.</span></span>  

![웹 서비스 구성][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="394fe-183">새 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="394fe-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="394fe-184">새 웹 서비스를 배포하려면 웹 서비스를 배포하는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="394fe-185">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="394fe-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="394fe-186">실험에서 파생된 새 웹 서비스를 배포하려면:</span><span class="sxs-lookup"><span data-stu-id="394fe-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="394fe-187">캔버스 아래에서 **웹 서비스 배포**를 클릭하고 **웹 서비스 배포[신규]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="394fe-188">Machine Learning Studio를 통해 Azure Machine Learning 웹 서비스 **배포 실험** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="394fe-189">웹 서비스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="394fe-190">**가격 책정 계획**의 경우 기존 가격 책정 계획을 선택하거나 "새로 만들기"를 선택하고 새 계획 이름을 지정한 후 월별 계획 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="394fe-191">계획 계층이 기본적으로 기본 하위 지역에 대한 계획으로 설정되고 웹 서비스는 해당 하위 지역에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="394fe-192">**배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-192">Click **Deploy**.</span></span>

<span data-ttu-id="394fe-193">몇 분 후에 웹 서비스에 대한 **빠른 시작** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="394fe-194">**구성** 탭을 클릭하여 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="394fe-195">여기에서 서비스를 수정하고 설명을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="394fe-196">웹 서비스를 테스트하려면 **테스트** 탭을 클릭합니다(아래의 **웹 서비스 테스트** 참조).</span><span class="sxs-lookup"><span data-stu-id="394fe-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="394fe-197">웹 서비스에 액세스할 수 있는 응용 프로그램 만들기에 대한 정보는 **사용** 탭을 클릭합니다(자세한 내용은 이 연습의 다음 단계 참조).</span><span class="sxs-lookup"><span data-stu-id="394fe-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="394fe-198">웹 서비스를 배포하고 나서 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="394fe-199">예를 들어 모델을 변경하려면 학습 실험을 편집하고, 모델 매개 변수를 조정하고, **웹 서비스 배포**를 클릭한 후 **웹 서비스 배포[클래식]** 또는 **웹 서비스 배포[신규]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="394fe-200">실험을 다시 배포하면 이 실험이 웹 서비스를 대체하고 이제 업데이트된 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="394fe-201">웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="394fe-201">Test the web service</span></span>

<span data-ttu-id="394fe-202">웹 서비스에 액세스될 때 사용자 데이터는 **웹 서비스 입력** 모듈로 이동됩니다. 여기서 [모델 점수 매기기][score-model] 모듈로 전달되고 점수가 매겨집니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="394fe-203">예측 실험을 설정했던 방법대로, 모델은 원래 신용 위험 데이터 집합과 동일한 형식의 데이터를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="394fe-204">결과가 웹 서비스로부터 **웹 서비스 출력** 모듈을 거쳐 사용자에게 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="394fe-205">예측 실험을 구성한 방법대로 [모델 점수 매기기][score-model] 모듈에서 전체 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="394fe-206">여기에는 모든 입력 데이터와 신용 위험 값 및 점수 매기기 확률이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="394fe-207">하지만 원하는 경우 다른 것을 반환할 수 있습니다. 예를 들어 신용 위험 값만 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="394fe-208">이를 수행하려면 [모델 점수 매기기][score-model] 및 **웹 서비스 출력** 사이에 [프로젝트 열][project-columns] 모듈을 삽입하여 웹 서비스에서 반환하지 않으려는 열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="394fe-209">**Machine Learning Studio** 또는 **Azure Machine Learning 웹 서비스** 포털에서 기존 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="394fe-210">**Machine Learning 웹 서비스** 포털에서만 새 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="394fe-211">Azure Machine Learning 웹 서비스 포털에서 테스트하는 경우 요청-응답 서비스를 테스트하는 데 사용할 수 있는 샘플 데이터가 포털에서 생성되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="394fe-212">**구성** 페이지에서 **샘플 데이터 사용 여부**에 대해 "예"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="394fe-213">**테스트** 페이지에서 요청-응답 탭을 열면 포털은 원래 신용 위험 데이터 집합에서 가져온 샘플 데이터를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="394fe-214">기존 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="394fe-214">Test a Classic web service</span></span>

<span data-ttu-id="394fe-215">Machine Learning Studio 또는 Machine Learning 웹 서비스 포털에서 기존 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="394fe-216">Machine Learning Studio에서 테스트</span><span class="sxs-lookup"><span data-stu-id="394fe-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="394fe-217">웹 서비스에 대한 **대시보드** 페이지에서 **기본 끝점**의 **테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="394fe-218">서비스에 대한 입력 데이터를 요청하는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="394fe-219">이는 원래 신용 위험 데이터 집합에 나타난 열과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="394fe-220">데이터 집합을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="394fe-221">Machine Learning 웹 서비스 포털에서 테스트</span><span class="sxs-lookup"><span data-stu-id="394fe-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="394fe-222">웹 서비스에 대한 **대시보드** 페이지에서 **기본 끝점** 아래의 **테스트 미리 보기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="394fe-223">웹 서비스 끝점에 대한 Azure Machine Learning 웹 서비스 포털의 테스트 페이지가 열리고 서비스에 사용할 입력 데이터를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="394fe-224">이는 원래 신용 위험 데이터 집합에 나타난 열과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="394fe-225">**요청-응답 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="394fe-226">새 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="394fe-226">Test a New web service</span></span>

<span data-ttu-id="394fe-227">Machine Learning 웹 서비스 포털에서만 새 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="394fe-228">[Azure Machine Learning 웹 서비스](https://services.azureml.net/quickstart) 포털에서 페이지의 맨 위에 있는 **테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="394fe-229">**테스트** 페이지가 열리면 서비스에 대한 데이터를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="394fe-230">표시된 입력 필드는 원래 신용 위험 데이터 집합에 나타난 열과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="394fe-231">데이터 집합을 입력하고 **요청-응답 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="394fe-232">테스트의 결과는 출력 열에 있는 페이지의 오른쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="394fe-233">웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="394fe-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="394fe-234">Azure 클래식 포털에서 기존 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="394fe-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="394fe-235">기존 웹 서비스를 배포한 후에는 [Azure 클래식 포털](https://manage.windowsazure.com)에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="394fe-236">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="394fe-237">Microsoft Azure 서비스 패널에서 **Machine Learning**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="394fe-238">작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-238">Click your workspace</span></span>
4. <span data-ttu-id="394fe-239">**웹 서비스** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="394fe-240">만든 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-240">Click the web service we created</span></span>
6. <span data-ttu-id="394fe-241">"기본" 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-241">Click the "default" endpoint</span></span>

<span data-ttu-id="394fe-242">여기에서 웹 서비스를 수행하는 방법을 모니터링하고 서비스에서 처리할 수 있는 동시 호출 수를 변경하여 성능을 조정하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="394fe-243">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="394fe-243">For more details, see:</span></span>

* [<span data-ttu-id="394fe-244">끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="394fe-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="394fe-245">웹 서비스 확장</span><span class="sxs-lookup"><span data-stu-id="394fe-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="394fe-246">Azure Machine Learning 웹 서비스 포털에서 기존 또는 새 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="394fe-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="394fe-247">기존 또는 신규의 웹 서비스를 배포한 후에는 [Microsoft Azure Machine Learning 웹 서비스 포털](https://services.azureml.net/quickstart)에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="394fe-248">웹 서비스의 성능을 모니터링하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="394fe-249">[Microsoft Azure Machine Learning 웹 서비스](https://services.azureml.net/quickstart) 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="394fe-250">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-250">Click **Web services**</span></span>
3. <span data-ttu-id="394fe-251">해당 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-251">Click your web service</span></span>
4. <span data-ttu-id="394fe-252">**대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="394fe-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="394fe-253">**다음: [웹 서비스 액세스](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="394fe-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
