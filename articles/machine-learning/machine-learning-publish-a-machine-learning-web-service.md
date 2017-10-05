---
title: "Machine Learning 웹 서비스 배포 | Microsoft Docs"
description: "학습 실험을 예측 실험으로 변환하고 배포할 준비를 한 다음 Azure 기계 학습 웹 서비스로 배포하는 방법입니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 39761f94efc530452a41ef9f2130976803cff711
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a><span data-ttu-id="09f04-103">Azure 기계 학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="09f04-103">Deploy an Azure Machine Learning web service</span></span>
<span data-ttu-id="09f04-104">Azure Machine Learning을 사용하면 예측 분석 솔루션을 빌드, 테스트 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-104">Azure Machine Learning enables you to build, test, and deploy predictive analytic solutions.</span></span>

<span data-ttu-id="09f04-105">대략적인 관점에서 이 작업은 다음 세 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-105">From a high-level point-of-view, this is done in three steps:</span></span>

* <span data-ttu-id="09f04-106">**[학습 실험 만들기]** - Azure 기계 학습 스튜디오는 사용자가 제공하는 학습 데이터를 사용하여 예측 분석 모델을 학습하고 테스트하는 데 사용하는 시각적 공동 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-106">**[Create a training experiment]** - Azure Machine Learning Studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data that you supply.</span></span>
* <span data-ttu-id="09f04-107">**[예측 실험으로 변환]** - 기존 데이터로 모델을 학습시키고 새 데이터의 점수를 매기는 데 사용할 준비가 되면, 예측을 위해 실험을 준비하고 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-107">**[Convert it to a predictive experiment]** - Once your model has been trained with existing data and you're ready to use it to score new data, you prepare and streamline your experiment for predictions.</span></span>
* <span data-ttu-id="09f04-108">**[앱 서비스로 배포]** - 예측 실험을 [신규] 또는 [기존] Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-108">**[Deploy it as a web service]** - You can deploy your predictive experiment as a [new] or [classic] Azure web service.</span></span> <span data-ttu-id="09f04-109">사용자 모델에 데이터를 보내고 모델의 예측을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-109">Users can send data to your model and receive your model's predictions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a><span data-ttu-id="09f04-110">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="09f04-110">Create a training experiment</span></span>
<span data-ttu-id="09f04-111">예측 분석 모델을 학습시키려면 Azure 기계 학습 스튜디오에서 학습 데이터를 로드하고, 필요한 대로 데이터를 준비하며, 기계 학습 알고리즘을 적용하고 결과를 평가하는 다양한 모듈을 포함하는 학습 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-111">To train a predictive analytics model, you use Azure Machine Learning Studio to create a training experiment where you include various modules to load training data, prepare the data as necessary, apply machine learning algorithms, and evaluate the results.</span></span> <span data-ttu-id="09f04-112">실험은 반복할 수 있으며 여러 다른 기계 학습 알고리즘을 시도하여 결과를 비교하고 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-112">You can iterate on an experiment and try different machine learning algorithms to compare and evaluate the results.</span></span>

<span data-ttu-id="09f04-113">학습 실험을 만들고 관리하는 프로세스는 다른 부분에서 더욱 철저히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-113">The process of creating and managing training experiments is covered more thoroughly elsewhere.</span></span> <span data-ttu-id="09f04-114">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-114">For more information, see these articles:</span></span>

* [<span data-ttu-id="09f04-115">Azure 기계 학습 스튜디오에서 간단한 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="09f04-115">Create a simple experiment in Azure Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="09f04-116">Azure 기계 학습을 사용하여 예측 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="09f04-116">Develop a predictive solution with Azure Machine Learning</span></span>](machine-learning-walkthrough-develop-predictive-solution.md)
* [<span data-ttu-id="09f04-117">Azure 기계 학습 스튜디오에 학습 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="09f04-117">Import your training data into Azure Machine Learning Studio</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="09f04-118">Azure 기계 학습 스튜디오에서 반복 실험 관리</span><span class="sxs-lookup"><span data-stu-id="09f04-118">Manage experiment iterations in Azure Machine Learning Studio</span></span>](machine-learning-manage-experiment-iterations.md)

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="09f04-119">학습 실험에서 예측 실험으로 변환</span><span class="sxs-lookup"><span data-stu-id="09f04-119">Convert the training experiment to a predictive experiment</span></span>
<span data-ttu-id="09f04-120">모델을 학습했으면 학습 실험을 예측 실험으로 변환하여 새 데이터의 점수를 매길 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-120">Once you've trained your model, you're ready to convert your training experiment into a predictive experiment to score new data.</span></span>

<span data-ttu-id="09f04-121">예측 실험으로 변환하면 학습된 모델을 점수 매기기 웹 서비스로 배포할 준비가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-121">By converting to a predictive experiment, you're getting your trained model ready to be deployed as a scoring web service.</span></span> <span data-ttu-id="09f04-122">웹 서비스 사용자가 입력 데이터를 모델로 보내면 모델에서 예측 결과를 다시 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-122">Users of the web service can send input data to your model and your model will send back the prediction results.</span></span> <span data-ttu-id="09f04-123">따라서 예측 실험을 변환할 때 다른 사람이 사용할 모델을 어떻게 예측할 것인지를 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-123">As you convert to a predictive experiment, keep in mind how you expect your model to be used by others.</span></span>

<span data-ttu-id="09f04-124">학습 실험을 예측 실험으로 변환하려면 실험 캔버스의 맨 아래에서 **실행**을 클릭한 다음 **웹 서비스 설정**을 클릭한 다음 **예측 웹 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-124">To convert your training experiment to a predictive experiment, click **Run** at the bottom of the experiment canvas, click **Set Up Web Service**, then select **Predictive Web Service**.</span></span>

![점수 매기기 실험으로 변환](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

<span data-ttu-id="09f04-126">이 변환을 수행하는 방법에 대한 자세한 내용은 [Azure Machine Learning Studio에서 배포하기 위한 모델을 준비하는 방법](machine-learning-convert-training-experiment-to-scoring-experiment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-126">For more information on how to perform this conversion, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="09f04-127">다음 단계에서는 예측 실험을 새 웹 서비스로 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-127">The following steps describe deploying a predictive experiment as a New web service.</span></span> <span data-ttu-id="09f04-128">실험을 기존 웹 서비스로 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-128">You can also deploy the experiment as Classic web service.</span></span>

## <a name="deploy-it-as-a-web-service"></a><span data-ttu-id="09f04-129">웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="09f04-129">Deploy it as a web service</span></span>

<span data-ttu-id="09f04-130">예측 실험을 새 웹 서비스 또는 기존 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-130">You can deploy the predictive experiment as a New web service or as a Classic web service.</span></span>

### <a name="deploy-the-predictive-experiment-as-a-new-web-service"></a><span data-ttu-id="09f04-131">예측 실험을 새 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="09f04-131">Deploy the predictive experiment as a New web service</span></span>
<span data-ttu-id="09f04-132">이제 예측 실험이 준비되었으므로 이를 새 Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-132">Now that the predictive experiment has been prepared, you can deploy it as a new Azure web service.</span></span> <span data-ttu-id="09f04-133">웹 서비스를 사용하면 사용자가 모델에 데이터를 보낼 수 있으며, 이 경우 모델에서 해당 예측을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-133">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="09f04-134">예측 실험을 배포하려면 실험 캔버스의 맨 아래에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-134">To deploy your predictive experiment, click **Run** at the bottom of the experiment canvas.</span></span> <span data-ttu-id="09f04-135">실험 실행이 완료되면 **웹 서비스 배포**를 클릭하고 **웹 서비스 배포[신규]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-135">Once the experiment has finished running, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>  <span data-ttu-id="09f04-136">Machine Learning 웹 서비스 포털의 배포 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-136">The deployment page of the Machine Learning Web Service portal opens.</span></span>

> [!NOTE] 
> <span data-ttu-id="09f04-137">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-137">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="09f04-138">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-138">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a><span data-ttu-id="09f04-139">Machine Learning 웹 서비스 포털 배포 실험 페이지</span><span class="sxs-lookup"><span data-stu-id="09f04-139">Machine Learning Web Service portal Deploy Experiment Page</span></span>
<span data-ttu-id="09f04-140">실험 배포 페이지에서 웹 서비스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-140">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="09f04-141">가격 책정 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-141">Select a pricing plan.</span></span> <span data-ttu-id="09f04-142">기존 가격 책정 계획이 있는 경우 해당 계획을 선택하고 그렇지 않으면 서비스에 대한 새 가격 계획을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-142">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span>

1. <span data-ttu-id="09f04-143">**가격 계획** 드롭다운에서 기존 계획을 선택하거나 **새 계획 선택** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-143">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="09f04-144">**계획 이름**에 청구서의 계획을 식별하는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-144">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="09f04-145">**월별 계획 계층**중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-145">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="09f04-146">계획 계층이 기본적으로 기본 하위 지역에 대한 계획으로 설정되고 웹 서비스는 해당 하위 지역에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-146">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="09f04-147">**배포** 를 클릭하면 웹 서비스에 대한 **빠른 시작** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-147">Click **Deploy** and the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="09f04-148">웹 서비스 빠른 시작 페이지를 사용하면 웹 서비스를 만든 후 수행할 가장 일반적인 작업에 대한 액세스 권한 및 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-148">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a web service.</span></span> <span data-ttu-id="09f04-149">여기에서 테스트 페이지 및 사용 페이지에 모두 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-149">From here, you can easily access both the Test page and Consume page.</span></span>

<!-- ![Deploy the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a><span data-ttu-id="09f04-150">새 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="09f04-150">Test your New web service</span></span>
<span data-ttu-id="09f04-151">새 웹 서비스를 테스트하려면 일반적인 작업에서 **웹 서비스 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-151">To test your new web service, click **Test web service** under common tasks.</span></span> <span data-ttu-id="09f04-152">테스트 페이지에서 웹 서비스를 RRS(요청-응답 서비스) 또는 BES(일괄 처리 실행 서비스)로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-152">On the Test page, you can test your web service as a Request-Response Service (RRS) or a Batch Execution service (BES).</span></span>

<span data-ttu-id="09f04-153">RRS 테스트 페이지에서는 실험에 대해 정의된 입력, 출력 및 모든 전역 매개 변수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-153">The RRS test page displays the inputs, outputs, and any global parameters that you have defined for the experiment.</span></span> <span data-ttu-id="09f04-154">웹 서비스를 테스트하려면 입력에 적절한 값을 수동으로 입력하거나 테스트 값을 포함하는 CSV(쉼표로 구분된 값) 형식의 파일을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-154">To test the web service, you can manually enter appropriate values for the inputs or supply a comma separated value (CSV) formatted file containing the test values.</span></span>

<span data-ttu-id="09f04-155">RRS를 테스트하려면 목록 보기 모드에서 입력에 적절한 값을 입력하고 **요청-응답 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-155">To test using RRS, from the list view mode, enter appropriate values for the inputs and click **Test Request-Response**.</span></span> <span data-ttu-id="09f04-156">예측 결과는 왼쪽의 출력 열에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-156">Your prediction results  display in the output column to the left.</span></span>

![웹 서비스 배포](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

<span data-ttu-id="09f04-158">BES를 테스트하려면 **배치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-158">To test your BES, click **Batch**.</span></span> <span data-ttu-id="09f04-159">배치 테스트 페이지의 입력에서 찾아보기를 클릭하고 적절한 샘플 값이 포함된 CSV 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-159">On the Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="09f04-160">CSV 파일이 없고 Machine Learning Studio를 사용하여 예측 실험을 만든 경우 예측 실험에 대한 데이터 집합을 다운로드하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-160">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download the data set for your predictive experiment and use it.</span></span>

<span data-ttu-id="09f04-161">데이터 집합을 다운로드하려면 기계 학습 스튜디오를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-161">To download the data set, open Machine Learning Studio.</span></span> <span data-ttu-id="09f04-162">예측 실험을 열고 실험에 대한 입력을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-162">Open your predictive experiment and right click the input for your experiment.</span></span> <span data-ttu-id="09f04-163">상황에 맞는 메뉴에서 **데이터 집합**을 선택한 다음 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-163">From the context menu, select **dataset** and then select **Download**.</span></span>

![웹 서비스 배포](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

<span data-ttu-id="09f04-165">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-165">Click **Test**.</span></span> <span data-ttu-id="09f04-166">Batch 실행 작업의 상태는 **Batch 작업 테스트**의 오른쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-166">The status of your Batch Execution job displays to the right under **Test Batch Jobs**.</span></span>

![웹 서비스 배포](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

<span data-ttu-id="09f04-168">**구성** 페이지에서 설명, 제목을 변경하고 저장소 계정 키를 업데이트하며 웹 서비스에 대한 샘플 데이터를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-168">On the **CONFIGURATION** page, you can change the description, title, update the storage account key, and enable sample data for your web service.</span></span>

![웹 서비스 구성](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

<span data-ttu-id="09f04-170">웹 서비스를 배포한 후 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-170">Once you've deployed the web service, you can:</span></span>

* <span data-ttu-id="09f04-171">**액세스** </span><span class="sxs-lookup"><span data-stu-id="09f04-171">**Access** it through the web service API.</span></span>
* <span data-ttu-id="09f04-172">**관리** </span><span class="sxs-lookup"><span data-stu-id="09f04-172">**Manage** it through Azure Machine Learning web services portal or the Azure classic portal.</span></span>
* <span data-ttu-id="09f04-173">**업데이트** </span><span class="sxs-lookup"><span data-stu-id="09f04-173">**Update** it if your model changes.</span></span>

#### <a name="access-your-new-web-service"></a><span data-ttu-id="09f04-174">새 웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="09f04-174">Access your New web service</span></span>
<span data-ttu-id="09f04-175">기계 학습 스튜디오에서 웹 서비스를 배포하면 서비스에 데이터를 보내고 프로그래밍 방식으로 응답을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-175">Once you deploy your web service from Machine Learning Studio, you can send data to the service and receive responses programmatically.</span></span>

<span data-ttu-id="09f04-176">**사용** 페이지에서는 웹 서비스에 액세스하는 데 필요한 모든 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-176">The **Consume** page provides all the information you need to access your web service.</span></span> <span data-ttu-id="09f04-177">예를 들어, 서비스에 대한 권한이 부여된 액세스를 허용하도록 API 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-177">For example, the API key is provided to allow authorized access to the service.</span></span>

<span data-ttu-id="09f04-178">Machine Learning 웹 서비스 액세스에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스를 사용하는 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-178">For more information about accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-new-web-service"></a><span data-ttu-id="09f04-179">새 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="09f04-179">Manage your New web service</span></span>
<span data-ttu-id="09f04-180">새 웹 서비스 Machine Learning 웹 서비스 포털을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-180">You can manage your New web services Machine Learning Web Services portal.</span></span> <span data-ttu-id="09f04-181">[기본 포털 페이지](https://services.azureml-test.net/)에서 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-181">From the [main portal page](https://services.azureml-test.net/), click **Web Services**.</span></span> <span data-ttu-id="09f04-182">웹 서비스 페이지에서 서비스를 삭제하거나 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-182">From the web services page, you can delete or copy a service.</span></span> <span data-ttu-id="09f04-183">특정 서비스를 모니터링하려면 서비스를 클릭한 다음 **대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-183">To monitor a specific service, click the service and then click **Dashboard**.</span></span> <span data-ttu-id="09f04-184">웹 서비스와 연결된 배치 작업을 모니터링하려면 **배치 요청 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-184">To monitor batch jobs associated with the web service, click **Batch Request Log**.</span></span>

### <a name="deploy-the-predictive-experiment-as-a-classic-web-service"></a><span data-ttu-id="09f04-185">예측 실험을 기존 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="09f04-185">Deploy the predictive experiment as a Classic web service</span></span>

<span data-ttu-id="09f04-186">이제 예측 실험이 충분히 준비되었으므로 이를 기존 Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-186">Now that the predictive experiment has been sufficiently prepared, you can deploy it as a Classic Azure web service.</span></span> <span data-ttu-id="09f04-187">웹 서비스를 사용하면 사용자가 모델에 데이터를 보낼 수 있으며, 이 경우 모델에서 해당 예측을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-187">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="09f04-188">예측 실험을 배포하려면 실험 캔버스의 맨 아래에서 **실행**을 클릭한 다음 **웹 서비스 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-188">To deploy your predictive experiment, click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service**.</span></span> <span data-ttu-id="09f04-189">웹 서비스가 설정되고 웹 서비스 대시보드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-189">The web service is set up and you are placed in the web service dashboard.</span></span>

![웹 서비스 배포](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a><span data-ttu-id="09f04-191">기존 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="09f04-191">Test your Classic web service</span></span>

<span data-ttu-id="09f04-192">Machine Learning 웹 서비스 포털 또는 Machine Learning Studio에서 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-192">You can test the web service in either the Machine Learning Web Services portal or Machine Learning Studio.</span></span>

<span data-ttu-id="09f04-193">리소스 요청 웹 서비스를 테스트하려면 웹 서비스 대시보드에서 **테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-193">To test the Request Response web service, click the **Test** button in the web service dashboard.</span></span> <span data-ttu-id="09f04-194">서비스에 대한 입력 데이터를 요청하는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-194">A dialog pops up to ask you for the input data for the service.</span></span> <span data-ttu-id="09f04-195">이러한 열이 점수 매기기 실험에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-195">These are the columns expected by the scoring experiment.</span></span> <span data-ttu-id="09f04-196">데이터 집합을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-196">Enter a set of data and then click **OK**.</span></span> <span data-ttu-id="09f04-197">웹 서비스에서 생성된 결과가 대시보드 아래쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-197">The results generated by the web service are displayed at the bottom of the dashboard.</span></span>

<span data-ttu-id="09f04-198">**테스트** 미리 보기 링크를 클릭하면 앞서 새 웹 서비스 섹션에 나온 것처럼 Azure Machine Learning 웹 서비스에서 해당 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-198">You can click the **Test** preview link to test your service in the Azure Machine Learning Web Services portal as shown previously in the New web service section.</span></span>

<span data-ttu-id="09f04-199">일괄 처리 실행 서비스를 테스트하려면 **테스트** 미리 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-199">To test the Batch Execution Service, click **Test** preview link .</span></span> <span data-ttu-id="09f04-200">배치 테스트 페이지의 입력에서 찾아보기를 클릭하고 적절한 샘플 값이 포함된 CSV 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-200">On the Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="09f04-201">CSV 파일이 없고 Machine Learning Studio를 사용하여 예측 실험을 만든 경우 예측 실험에 대한 데이터 집합을 다운로드하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-201">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download the data set for your predictive experiment and use it.</span></span>

![웹 서비스 테스트](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

<span data-ttu-id="09f04-203">**구성** 페이지에서 서비스의 표시 이름을 변경하고 설명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-203">On the **CONFIGURATION** page, you can change the display name of the service and give it a description.</span></span> <span data-ttu-id="09f04-204">웹 서비스를 관리하는 [Azure 클래식 포털](http://manage.windowsazure.com/) 에 이름과 설명이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-204">The name and description is displayed in the [Azure classic portal](http://manage.windowsazure.com/) where you manage your web services.</span></span>

<span data-ttu-id="09f04-205">**입력 스키마**, **출력 스키마** 및 **웹 서비스 매개 변수**의 각 열에 문자열을 입력하여 입력 데이터, 출력 데이터 및 웹 서비스 매개 변수에 대한 설명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-205">You can provide a description for your input data, output data, and web service parameters by entering a string for each column under **INPUT SCHEMA**, **OUTPUT SCHEMA**, and **Web SERVICE PARAMETER**.</span></span> <span data-ttu-id="09f04-206">이러한 설명은 웹 서비스에 제공된 샘플 코드 설명서에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-206">These descriptions are used in the sample code documentation provided for the web service.</span></span>

<span data-ttu-id="09f04-207">로깅을 사용하도록 설정하면 웹 서비스에 액세스할 때 나타나는 실패를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-207">You can enable logging to diagnose any failures that you're seeing when your web service is accessed.</span></span> <span data-ttu-id="09f04-208">자세한 내용은 [기계 학습 웹 서비스에 대해 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-208">For more information, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

![웹 서비스 구성](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

<span data-ttu-id="09f04-210">또한 앞서 새 웹 서비스 섹션에 나온 절차와 유사하게 Azure Machine Learning 웹 서비스 포털에서 웹 서비스에 대한 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-210">You can also configure the endpoints for the web service in the Azure Machine Learning Web Services portal similar to the procedure shown previously in the New web service section.</span></span> <span data-ttu-id="09f04-211">옵션은 여러 가지가 있습니다. 서비스 설명을 추가하거나 변경하고, 로깅을 사용하도록 설정하고, 테스트에 사용할 샘플 데이터를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-211">The options are different, you can add or change the service description, enable logging, and enable sample data for testing.</span></span>

#### <a name="access-your-classic-web-service"></a><span data-ttu-id="09f04-212">기존 웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="09f04-212">Access your Classic web service</span></span>
<span data-ttu-id="09f04-213">기계 학습 스튜디오에서 웹 서비스를 배포하면 서비스에 데이터를 보내고 프로그래밍 방식으로 응답을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-213">Once you deploy your web service from Machine Learning Studio, you can send data to the service and receive responses programmatically.</span></span>

<span data-ttu-id="09f04-214">대시보드에서는 웹 서비스에 액세스하는 데 필요한 모든 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-214">The dashboard provides all the information you need to access your web service.</span></span> <span data-ttu-id="09f04-215">예를 들어, 서비스에 대해 권한 부여된 액세스가 가능하도록 API 키가 제공되고, 코드 작성을 시작하는 데 도움이 되도록 API 도움말 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-215">For example, the API key is provided to allow authorized access to the service, and API help pages are provided to help you get started writing your code.</span></span>

<span data-ttu-id="09f04-216">Machine Learning 웹 서비스 액세스에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스를 사용하는 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-216">For more information about accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-classic-web-service"></a><span data-ttu-id="09f04-217">기존 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="09f04-217">Manage your Classic web service</span></span>
<span data-ttu-id="09f04-218">다양한 작업을 통해 웹 서비스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-218">There are various of actions you can perform to monitor a web service.</span></span> <span data-ttu-id="09f04-219">업데이트 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-219">You can update it, and delete it.</span></span> <span data-ttu-id="09f04-220">배포할 때 생성되는 기본 끝점 외에, 기존 웹 서비스에 추가 끝점도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-220">You can also add additional endpoints to a Classic web service in addition to the default endpoint that is created when you deploy it.</span></span>

<span data-ttu-id="09f04-221">자세한 내용은 [Azure Machine Learning 작업 영역 관리](machine-learning-manage-workspace.md) 및 [Azure Machine Learning 웹 서비스 포털을 사용하여 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-221">For more information, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md) and [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>

<!-- When this article gets published, fix the link and uncomment
For more information on how to manage Azure Machine Learning web service endpoints using the REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-the-web-service"></a><span data-ttu-id="09f04-222">웹 서비스 업데이트</span><span class="sxs-lookup"><span data-stu-id="09f04-222">Update the web service</span></span>
<span data-ttu-id="09f04-223">추가 학습 데이터로 모델 업데이트와 같은 방식으로 웹 서비스를 변경하고 다시 배포하여 원래 웹 서비스를 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-223">You can make changes to your web service, such as updating the model with additional training data, and deploy it again, overwriting the original web service.</span></span>

<span data-ttu-id="09f04-224">웹 서비스를 업데이트하려면 웹 서비스를 배포하는 데 사용한 원래 예측 실험을 열고 **다른 이름으로 저장**을 클릭하여 편집 가능한 사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-224">To update the web service, open the original predictive experiment you used to deploy the web service and make an editable copy by clicking **SAVE AS**.</span></span> <span data-ttu-id="09f04-225">변경한 다음 **웹 서비스 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-225">Make your changes and then click **Deploy Web Service**.</span></span>

<span data-ttu-id="09f04-226">이 실험을 이전에 배포했기 때문에 기존 서비스를 덮어쓰거나(기존 웹 서비스) 업데이트(새 웹 서비스)할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-226">Because you've deployed this experiment before, you are asked if you want to overwrite (Classic Web Service) or update (New web service) the existing service.</span></span> <span data-ttu-id="09f04-227">**예** 또는 **업데이트**를 클릭하여 기존 웹 서비스를 중지하고 대신 새 예측 실험을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-227">Clicking **YES** or **Update** stops the existing web service and deploys the new predictive experiment is deployed in its place.</span></span>

> [!NOTE]
> <span data-ttu-id="09f04-228">예를 들어, 새 표시 이름 또는 설명을 입력하여 원래 웹 서비스의 구성을 변경한 경우 해당 값을 다시 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-228">If you made configuration changes in the original web service, for example, entering a new display name or description, you will need to enter those values again.</span></span>
> 
> 

<span data-ttu-id="09f04-229">웹 서비스를 업데이트하기 위한 한 가지 옵션은 프로그래밍 방식으로 모델을 다시 학습하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09f04-229">One option for updating your web service is to retrain the model programmatically.</span></span> <span data-ttu-id="09f04-230">자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f04-230">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

<!-- internal links -->
<span data-ttu-id="09f04-231">[학습 실험 만들기]: #create-a-training-experiment</span><span class="sxs-lookup"><span data-stu-id="09f04-231">[Create a training experiment]: #create-a-training-experiment</span></span>
<span data-ttu-id="09f04-232">[예측 실험으로 변환]: #convert-the-training-experiment-to-a-predictive-experiment</span><span class="sxs-lookup"><span data-stu-id="09f04-232">[Convert it to a predictive experiment]: #convert-the-training-experiment-to-a-predictive-experiment</span></span>
<span data-ttu-id="09f04-233">[앱 서비스로 배포]: #deploy-it-as-a-web-service</span><span class="sxs-lookup"><span data-stu-id="09f04-233">[Deploy it as a web service]: #deploy-it-as-a-web-service</span></span>
<span data-ttu-id="09f04-234">[신규]: #deploy-the-predictive-experiment-as-a-new-Web-service</span><span class="sxs-lookup"><span data-stu-id="09f04-234">[new]: #deploy-the-predictive-experiment-as-a-new-Web-service</span></span>
<span data-ttu-id="09f04-235">[기존]: #deploy-the-predictive-experiment-as-a-new-Web-service</span><span class="sxs-lookup"><span data-stu-id="09f04-235">[classic]: #deploy-the-predictive-experiment-as-a-new-Web-service</span></span>
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
