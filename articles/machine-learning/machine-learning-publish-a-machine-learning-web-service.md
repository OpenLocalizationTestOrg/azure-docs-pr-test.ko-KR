---
title: "기계 학습 웹 서비스 aaaDeploy | Microsoft Docs"
description: "Tooconvert 학습 실험 tooa 예측 실험 하는 방법에 배포를 준비 다음 Azure 기계 학습 웹 서비스로 배포 하기 합니다."
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
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a><span data-ttu-id="8d79c-103">Azure 기계 학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="8d79c-103">Deploy an Azure Machine Learning web service</span></span>
<span data-ttu-id="8d79c-104">Azure 기계 학습 하면 toobuild, 테스트 및 예측 분석 솔루션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-104">Azure Machine Learning enables you toobuild, test, and deploy predictive analytic solutions.</span></span>

<span data-ttu-id="8d79c-105">대략적인 관점에서 이 작업은 다음 세 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-105">From a high-level point-of-view, this is done in three steps:</span></span>

* <span data-ttu-id="8d79c-106">**[학습 실험 만들기]**  -Azure 기계 학습 스튜디오는 tootrain를 사용 하 고 예측 분석을 테스트 하는 시각적 공동 개발 환경을 제공 하는 학습 데이터를 사용 하 여 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-106">**[Create a training experiment]** - Azure Machine Learning Studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data that you supply.</span></span>
* <span data-ttu-id="8d79c-107">**[Tooa 예측 실험으로 변환]**  -기존 데이터와 모델의 학습 및 준비 toouse 하 고 나면 그 tooscore 새 데이터를 준비 하 고 예측에 대 한 실험을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-107">**[Convert it tooa predictive experiment]** - Once your model has been trained with existing data and you're ready toouse it tooscore new data, you prepare and streamline your experiment for predictions.</span></span>
* <span data-ttu-id="8d79c-108">**[앱 서비스로 배포]** - 예측 실험을 [신규] 또는 [기존] Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-108">**[Deploy it as a web service]** - You can deploy your predictive experiment as a [new] or [classic] Azure web service.</span></span> <span data-ttu-id="8d79c-109">사용자가 데이터 tooyour 모델 보내고 모델의 예측을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-109">Users can send data tooyour model and receive your model's predictions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a><span data-ttu-id="8d79c-110">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="8d79c-110">Create a training experiment</span></span>
<span data-ttu-id="8d79c-111">Azure 기계 학습 스튜디오 toocreate 여기서 포함 다양 한 모듈 tooload 학습 데이터, 필요에 따라 hello 데이터 준비, 기계 학습 알고리즘을 적용 한 hello 결과 평가 학습 실험 사용 tootrain 예측 분석 모델 .</span><span class="sxs-lookup"><span data-stu-id="8d79c-111">tootrain a predictive analytics model, you use Azure Machine Learning Studio toocreate a training experiment where you include various modules tooload training data, prepare hello data as necessary, apply machine learning algorithms, and evaluate hello results.</span></span> <span data-ttu-id="8d79c-112">실험을 반복 하 고 다양 한 기계 학습 알고리즘 toocompare 한 hello 결과 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-112">You can iterate on an experiment and try different machine learning algorithms toocompare and evaluate hello results.</span></span>

<span data-ttu-id="8d79c-113">hello 프로세스 만들기 및 관리 학습 실험의 다른 곳에서 완벽 하 게 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-113">hello process of creating and managing training experiments is covered more thoroughly elsewhere.</span></span> <span data-ttu-id="8d79c-114">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d79c-114">For more information, see these articles:</span></span>

* [<span data-ttu-id="8d79c-115">Azure 기계 학습 스튜디오에서 간단한 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="8d79c-115">Create a simple experiment in Azure Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="8d79c-116">Azure 기계 학습을 사용하여 예측 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="8d79c-116">Develop a predictive solution with Azure Machine Learning</span></span>](machine-learning-walkthrough-develop-predictive-solution.md)
* [<span data-ttu-id="8d79c-117">Azure 기계 학습 스튜디오에 학습 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="8d79c-117">Import your training data into Azure Machine Learning Studio</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="8d79c-118">Azure 기계 학습 스튜디오에서 반복 실험 관리</span><span class="sxs-lookup"><span data-stu-id="8d79c-118">Manage experiment iterations in Azure Machine Learning Studio</span></span>](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="8d79c-119">Hello 학습 실험 tooa 예측 실험으로 변환</span><span class="sxs-lookup"><span data-stu-id="8d79c-119">Convert hello training experiment tooa predictive experiment</span></span>
<span data-ttu-id="8d79c-120">모델을 학습할 준비 tooconvert 교육 실험를 예측 실험 tooscore 새 데이터에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-120">Once you've trained your model, you're ready tooconvert your training experiment into a predictive experiment tooscore new data.</span></span>

<span data-ttu-id="8d79c-121">예측 tooa 변환 하 여 실험, 점수 매기기 웹 서비스로 배포 하 여 학습 된 모델을 준비 toobe 가져오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-121">By converting tooa predictive experiment, you're getting your trained model ready toobe deployed as a scoring web service.</span></span> <span data-ttu-id="8d79c-122">입력된 데이터 tooyour 모델 및 모델 백 hello 예측 결과 기준으로 송신할 hello 웹 서비스 사용자를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-122">Users of hello web service can send input data tooyour model and your model will send back hello prediction results.</span></span> <span data-ttu-id="8d79c-123">변환할 때 예측 tooa 실험, 원하는 다른 사용자가 사용 하 여 모델 toobe 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-123">As you convert tooa predictive experiment, keep in mind how you expect your model toobe used by others.</span></span>

<span data-ttu-id="8d79c-124">tooconvert 예측 하 여 학습 실험 tooa 실험, 클릭 **실행** hello 실험 캔버스의 hello 맨 아래에 클릭 **웹 서비스 설정**을 선택한 후 **예측 웹 서비스** .</span><span class="sxs-lookup"><span data-stu-id="8d79c-124">tooconvert your training experiment tooa predictive experiment, click **Run** at hello bottom of hello experiment canvas, click **Set Up Web Service**, then select **Predictive Web Service**.</span></span>

![Tooscoring 실험으로 변환](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

<span data-ttu-id="8d79c-126">방법에 대 한 자세한 내용은 tooperform이이 변환에서는 참조 [어떻게 tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델](machine-learning-convert-training-experiment-to-scoring-experiment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-126">For more information on how tooperform this conversion, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="8d79c-127">hello 다음 단계에서는 새 웹 서비스로 예측 실험 배포.</span><span class="sxs-lookup"><span data-stu-id="8d79c-127">hello following steps describe deploying a predictive experiment as a New web service.</span></span> <span data-ttu-id="8d79c-128">또한 기본 웹 서비스로 hello 실험을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-128">You can also deploy hello experiment as Classic web service.</span></span>

## <a name="deploy-it-as-a-web-service"></a><span data-ttu-id="8d79c-129">웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="8d79c-129">Deploy it as a web service</span></span>

<span data-ttu-id="8d79c-130">새 웹 서비스 또는 기본 웹 서비스로 hello 예측 실험을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-130">You can deploy hello predictive experiment as a New web service or as a Classic web service.</span></span>

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a><span data-ttu-id="8d79c-131">새 웹 서비스로 hello 예측 실험 배포</span><span class="sxs-lookup"><span data-stu-id="8d79c-131">Deploy hello predictive experiment as a New web service</span></span>
<span data-ttu-id="8d79c-132">Hello 예측 실험 준비 했으므로 새 Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-132">Now that hello predictive experiment has been prepared, you can deploy it as a new Azure web service.</span></span> <span data-ttu-id="8d79c-133">Hello 웹 서비스를 사용 하면 데이터 tooyour 모델을 보낼 수 있습니다 및 hello 모델의 예측이 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-133">Using hello web service, users can send data tooyour model and hello model will return its predictions.</span></span>

<span data-ttu-id="8d79c-134">toodeploy 실험을 클릭 하면 예측 **실행** 실험 캔버스 hello hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-134">toodeploy your predictive experiment, click **Run** at hello bottom of hello experiment canvas.</span></span> <span data-ttu-id="8d79c-135">Hello 실험 실행이 완료 되 면 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [새로]**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-135">Once hello experiment has finished running, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>  <span data-ttu-id="8d79c-136">hello 기계 학습 웹 서비스 포털의 hello 배포 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-136">hello deployment page of hello Machine Learning Web Service portal opens.</span></span>

> [!NOTE] 
> <span data-ttu-id="8d79c-137">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-137">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="8d79c-138">자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-138">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a><span data-ttu-id="8d79c-139">Machine Learning 웹 서비스 포털 배포 실험 페이지</span><span class="sxs-lookup"><span data-stu-id="8d79c-139">Machine Learning Web Service portal Deploy Experiment Page</span></span>
<span data-ttu-id="8d79c-140">Hello 실험 배포 페이지에서 hello 웹 서비스에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-140">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="8d79c-141">가격 책정 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-141">Select a pricing plan.</span></span> <span data-ttu-id="8d79c-142">기존 가격 책정 계획 선택할 수 있는 경우에 hello 서비스에 대 한 새 가격 계획을 만들어야 그렇지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-142">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span>

1. <span data-ttu-id="8d79c-143">Hello에 **가격 계획** 드롭 다운를 기존 계획을 선택 하거나 선택 hello **선택 새 계획** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-143">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="8d79c-144">**계획 이름**, 청구서에 hello 계획을 식별 하는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-144">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="8d79c-145">Hello 중 하나를 선택 **월별 계획 계층**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-145">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="8d79c-146">hello 계획 계층 toohello 계획 기본 지역 및 웹 서비스에 대 한 기본 배포 toothat 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-146">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="8d79c-147">클릭 **배포** 및 hello **퀵 스타트** 웹 서비스에 대 한 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-147">Click **Deploy** and hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="8d79c-148">hello 웹 서비스 빠른 시작 페이지 하면 액세스 및 지침 hello 웹 서비스를 만든 후 수행할 수는 가장 일반적인 작업에.</span><span class="sxs-lookup"><span data-stu-id="8d79c-148">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a web service.</span></span> <span data-ttu-id="8d79c-149">여기에서는 hello 테스트 페이지와 페이지 사용을 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-149">From here, you can easily access both hello Test page and Consume page.</span></span>

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a><span data-ttu-id="8d79c-150">새 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="8d79c-150">Test your New web service</span></span>
<span data-ttu-id="8d79c-151">tootest 새 웹 서비스를 클릭 하 여 **웹 서비스를 테스트할** 일반 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-151">tootest your new web service, click **Test web service** under common tasks.</span></span> <span data-ttu-id="8d79c-152">Hello 테스트 페이지에서 서비스 요청-응답 (RR)으로 웹 서비스 또는 일괄 처리 실행 서비스 (BES)을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-152">On hello Test page, you can test your web service as a Request-Response Service (RRS) or a Batch Execution service (BES).</span></span>

<span data-ttu-id="8d79c-153">hello RR 테스트 페이지 hello 입력, 출력 및 hello 실험에 정의 된 모든 전역 매개 변수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-153">hello RRS test page displays hello inputs, outputs, and any global parameters that you have defined for hello experiment.</span></span> <span data-ttu-id="8d79c-154">tootest hello 웹 서비스를 수동으로 입력할 수 있습니다 적절 한 값 hello 입력 또는 공급 장치에 대 한 hello 테스트 값을 포함 하는 쉼표로 구분 된 값 (CSV) 형식이 지정 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-154">tootest hello web service, you can manually enter appropriate values for hello inputs or supply a comma separated value (CSV) formatted file containing hello test values.</span></span>

<span data-ttu-id="8d79c-155">RR을 사용 하 여 tootest hello 목록 뷰 모드에서 hello 입력에 대 한 적절 한 값을 입력 하 고 클릭 **테스트 요청-응답**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-155">tootest using RRS, from hello list view mode, enter appropriate values for hello inputs and click **Test Request-Response**.</span></span> <span data-ttu-id="8d79c-156">예측 결과 hello 출력 열 toohello 왼쪽에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-156">Your prediction results  display in hello output column toohello left.</span></span>

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

<span data-ttu-id="8d79c-158">tootest 프로그램 BES 클릭 **일괄 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-158">tootest your BES, click **Batch**.</span></span> <span data-ttu-id="8d79c-159">Hello 일괄 처리 테스트 페이지를 사용자의 입력에서 찾아보기를 클릭 하 고 적절 한 샘플 값이 포함 된 CSV 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-159">On hello Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="8d79c-160">CSV 파일에 없는 경우 예측 실험 기계 학습 스튜디오를 사용 하 여 만든 예측 하 여 실험에 대 한 hello 데이터 집합을 다운로드 하 고 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-160">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download hello data set for your predictive experiment and use it.</span></span>

<span data-ttu-id="8d79c-161">toodownload hello 데이터 집합, 기계 학습 스튜디오를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-161">toodownload hello data set, open Machine Learning Studio.</span></span> <span data-ttu-id="8d79c-162">예측 하 여 실험을 열고 마우스 오른쪽 단추로 클릭 하 여 실험에 대 한 hello 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-162">Open your predictive experiment and right click hello input for your experiment.</span></span> <span data-ttu-id="8d79c-163">Hello 상황에 맞는 메뉴에서 선택 **dataset** 선택한 후 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-163">From hello context menu, select **dataset** and then select **Download**.</span></span>

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

<span data-ttu-id="8d79c-165">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-165">Click **Test**.</span></span> <span data-ttu-id="8d79c-166">일괄 처리 실행 작업의 hello 상태 표시 toohello 권리도 **테스트 일괄 처리 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-166">hello status of your Batch Execution job displays toohello right under **Test Batch Jobs**.</span></span>

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

<span data-ttu-id="8d79c-168">Hello에 **구성** 페이지 hello 설명, 제목, hello 저장소 계정 키 업데이트를 웹 서비스에 대 한 예제 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-168">On hello **CONFIGURATION** page, you can change hello description, title, update hello storage account key, and enable sample data for your web service.</span></span>

![Hello 웹 서비스 구성](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

<span data-ttu-id="8d79c-170">Hello 웹 서비스를 배포 하 고 나면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-170">Once you've deployed hello web service, you can:</span></span>

* <span data-ttu-id="8d79c-171">**액세스** hello 웹 서비스 API를 통해 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-171">**Access** it through hello web service API.</span></span>
* <span data-ttu-id="8d79c-172">**관리** 웹 서비스 포털 Azure 기계 학습을 통해 또는 Azure 클래식 포털을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-172">**Manage** it through Azure Machine Learning web services portal or hello Azure classic portal.</span></span>
* <span data-ttu-id="8d79c-173">**업데이트** </span><span class="sxs-lookup"><span data-stu-id="8d79c-173">**Update** it if your model changes.</span></span>

#### <a name="access-your-new-web-service"></a><span data-ttu-id="8d79c-174">새 웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="8d79c-174">Access your New web service</span></span>
<span data-ttu-id="8d79c-175">기계 학습 스튜디오에서 웹 서비스를 배포한 후 데이터 toohello 서비스 보내고 프로그래밍 방식으로 응답을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-175">Once you deploy your web service from Machine Learning Studio, you can send data toohello service and receive responses programmatically.</span></span>

<span data-ttu-id="8d79c-176">hello **사용** 페이지 tooaccess 웹 서비스를 해야 하는 모든 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-176">hello **Consume** page provides all hello information you need tooaccess your web service.</span></span> <span data-ttu-id="8d79c-177">예를 들어 hello API 키를 권한이 tooallow 액세스 toohello 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-177">For example, hello API key is provided tooallow authorized access toohello service.</span></span>

<span data-ttu-id="8d79c-178">기계 학습 웹 서비스에 액세스 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-178">For more information about accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-new-web-service"></a><span data-ttu-id="8d79c-179">새 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="8d79c-179">Manage your New web service</span></span>
<span data-ttu-id="8d79c-180">새 웹 서비스 Machine Learning 웹 서비스 포털을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-180">You can manage your New web services Machine Learning Web Services portal.</span></span> <span data-ttu-id="8d79c-181">Hello에서 [포털 기본 페이지](https://services.azureml-test.net/), 클릭 **웹 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-181">From hello [main portal page](https://services.azureml-test.net/), click **Web Services**.</span></span> <span data-ttu-id="8d79c-182">Hello 웹 서비스 페이지에서 삭제 하거나 서비스를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-182">From hello web services page, you can delete or copy a service.</span></span> <span data-ttu-id="8d79c-183">특정 서비스 toomonitor hello 서비스를 클릭 한 다음 클릭 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-183">toomonitor a specific service, click hello service and then click **Dashboard**.</span></span> <span data-ttu-id="8d79c-184">hello 웹 서비스와 관련 된 toomonitor 일괄 처리 작업이 클릭 **일괄 처리 요청 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-184">toomonitor batch jobs associated with hello web service, click **Batch Request Log**.</span></span>

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a><span data-ttu-id="8d79c-185">Hello 예측 실험을 기본 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="8d79c-185">Deploy hello predictive experiment as a Classic web service</span></span>

<span data-ttu-id="8d79c-186">Hello 예측 실험 충분히 준비 했으므로 클래식 Azure 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-186">Now that hello predictive experiment has been sufficiently prepared, you can deploy it as a Classic Azure web service.</span></span> <span data-ttu-id="8d79c-187">Hello 웹 서비스를 사용 하면 데이터 tooyour 모델을 보낼 수 있습니다 및 hello 모델의 예측이 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-187">Using hello web service, users can send data tooyour model and hello model will return its predictions.</span></span>

<span data-ttu-id="8d79c-188">toodeploy 실험을 클릭 하면 예측 **실행** hello hello 맨 아래에 캔버스를 실험 하 고 클릭 **웹 서비스 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-188">toodeploy your predictive experiment, click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service**.</span></span> <span data-ttu-id="8d79c-189">hello 웹 서비스 설정 및 웹 서비스 대시보드 hello에에서 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-189">hello web service is set up and you are placed in hello web service dashboard.</span></span>

![Hello 웹 서비스를 배포 합니다.](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a><span data-ttu-id="8d79c-191">기존 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="8d79c-191">Test your Classic web service</span></span>

<span data-ttu-id="8d79c-192">Hello 컴퓨터 학습 웹 서비스 포털 또는 기계 학습 스튜디오에서 hello 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-192">You can test hello web service in either hello Machine Learning Web Services portal or Machine Learning Studio.</span></span>

<span data-ttu-id="8d79c-193">tootest hello 요청 응답 웹 서비스는 hello 클릭 **테스트** hello 웹 서비스 대시보드에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-193">tootest hello Request Response web service, click hello **Test** button in hello web service dashboard.</span></span> <span data-ttu-id="8d79c-194">대화 상자가 표시 tooask 있습니다 hello hello 서비스에 대 한 입력된 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-194">A dialog pops up tooask you for hello input data for hello service.</span></span> <span data-ttu-id="8d79c-195">이들은 실험 점수 매기기 hello에 필요한 hello 열입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-195">These are hello columns expected by hello scoring experiment.</span></span> <span data-ttu-id="8d79c-196">데이터 집합을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-196">Enter a set of data and then click **OK**.</span></span> <span data-ttu-id="8d79c-197">hello 웹 서비스에 의해 생성 된 hello 결과 hello hello 대시보드 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-197">hello results generated by hello web service are displayed at hello bottom of hello dashboard.</span></span>

<span data-ttu-id="8d79c-198">Hello를 클릭할 수 있는 **테스트** hello 새 웹 서비스 섹션에서에서 이전에 표시 된 것 처럼 링크 tootest hello Azure 컴퓨터 학습 웹 서비스 포털에서 서비스를 미리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-198">You can click hello **Test** preview link tootest your service in hello Azure Machine Learning Web Services portal as shown previously in hello New web service section.</span></span>

<span data-ttu-id="8d79c-199">tootest hello 배치 실행 서비스 클릭 **테스트** 미리 보기 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-199">tootest hello Batch Execution Service, click **Test** preview link .</span></span> <span data-ttu-id="8d79c-200">Hello 일괄 처리 테스트 페이지를 사용자의 입력에서 찾아보기를 클릭 하 고 적절 한 샘플 값이 포함 된 CSV 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-200">On hello Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="8d79c-201">CSV 파일에 없는 경우 예측 실험 기계 학습 스튜디오를 사용 하 여 만든 예측 하 여 실험에 대 한 hello 데이터 집합을 다운로드 하 고 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-201">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download hello data set for your predictive experiment and use it.</span></span>

![Hello 웹 서비스 테스트](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

<span data-ttu-id="8d79c-203">Hello에 **구성** 페이지 hello 서비스의 hello 표시 이름을 변경 하 고 설명을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-203">On hello **CONFIGURATION** page, you can change hello display name of hello service and give it a description.</span></span> <span data-ttu-id="8d79c-204">hello 이름 및 설명을 hello에 표시 됩니다 [Azure 클래식 포털](http://manage.windowsazure.com/) 웹 서비스를 관리 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-204">hello name and description is displayed in hello [Azure classic portal](http://manage.windowsazure.com/) where you manage your web services.</span></span>

<span data-ttu-id="8d79c-205">**입력 스키마**, **출력 스키마** 및 **웹 서비스 매개 변수**의 각 열에 문자열을 입력하여 입력 데이터, 출력 데이터 및 웹 서비스 매개 변수에 대한 설명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-205">You can provide a description for your input data, output data, and web service parameters by entering a string for each column under **INPUT SCHEMA**, **OUTPUT SCHEMA**, and **Web SERVICE PARAMETER**.</span></span> <span data-ttu-id="8d79c-206">이러한 설명은 hello 웹 서비스에 대해 제공 하는 hello 샘플 코드 설명서에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-206">These descriptions are used in hello sample code documentation provided for hello web service.</span></span>

<span data-ttu-id="8d79c-207">웹 서비스에 액세스할 때 표시 되는 모든 오류 로깅 toodiagnose를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-207">You can enable logging toodiagnose any failures that you're seeing when your web service is accessed.</span></span> <span data-ttu-id="8d79c-208">자세한 내용은 [기계 학습 웹 서비스에 대해 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d79c-208">For more information, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

![Hello 웹 서비스 구성](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

<span data-ttu-id="8d79c-210">또한 Azure 컴퓨터 학습 웹 서비스 포털 비슷한 toohello 프로시저 hello 새 웹 서비스 섹션의에서 앞에 표시 된 hello에 hello 웹 서비스에 대 한 hello 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-210">You can also configure hello endpoints for hello web service in hello Azure Machine Learning Web Services portal similar toohello procedure shown previously in hello New web service section.</span></span> <span data-ttu-id="8d79c-211">hello 옵션은 서로 다른, 추가 하거나 hello 서비스 설명, 로깅 사용 및 테스트에 대 한 사용 샘플 데이터를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-211">hello options are different, you can add or change hello service description, enable logging, and enable sample data for testing.</span></span>

#### <a name="access-your-classic-web-service"></a><span data-ttu-id="8d79c-212">기존 웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="8d79c-212">Access your Classic web service</span></span>
<span data-ttu-id="8d79c-213">기계 학습 스튜디오에서 웹 서비스를 배포한 후 데이터 toohello 서비스 보내고 프로그래밍 방식으로 응답을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-213">Once you deploy your web service from Machine Learning Studio, you can send data toohello service and receive responses programmatically.</span></span>

<span data-ttu-id="8d79c-214">hello 대시보드 tooaccess 웹 서비스를 원하는 모든 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-214">hello dashboard provides all hello information you need tooaccess your web service.</span></span> <span data-ttu-id="8d79c-215">예를 들어 hello API 키에는 tooallow 액세스 toohello 서비스에 권한이 있고 API 도움말 페이지 코드 작성을 시작 하려면 toohelp 제공 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-215">For example, hello API key is provided tooallow authorized access toohello service, and API help pages are provided toohelp you get started writing your code.</span></span>

<span data-ttu-id="8d79c-216">기계 학습 웹 서비스에 액세스 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-216">For more information about accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-classic-web-service"></a><span data-ttu-id="8d79c-217">기존 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="8d79c-217">Manage your Classic web service</span></span>
<span data-ttu-id="8d79c-218">다양 한 작업의 toomonitor 웹 서비스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-218">There are various of actions you can perform toomonitor a web service.</span></span> <span data-ttu-id="8d79c-219">업데이트 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-219">You can update it, and delete it.</span></span> <span data-ttu-id="8d79c-220">배포할 때 만들어지는 추가 toohello 기본 끝점에 추가 끝점 tooa 클래식 웹 서비스를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-220">You can also add additional endpoints tooa Classic web service in addition toohello default endpoint that is created when you deploy it.</span></span>

<span data-ttu-id="8d79c-221">자세한 내용은 참조 [는 Azure 기계 학습 작업 영역을 관리](machine-learning-manage-workspace.md) 및 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-221">For more information, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md) and [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a><span data-ttu-id="8d79c-222">Hello 웹 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-222">Update hello web service</span></span>
<span data-ttu-id="8d79c-223">Hello 모델 추가 학습 데이터로 업데이트 하는 등 tooyour 웹 서비스를 변경할 수 있으며 덮어쓰지 hello 원래 웹 서비스를 다시 배포.</span><span class="sxs-lookup"><span data-stu-id="8d79c-223">You can make changes tooyour web service, such as updating hello model with additional training data, and deploy it again, overwriting hello original web service.</span></span>

<span data-ttu-id="8d79c-224">tooupdate hello 웹 서비스 toodeploy hello 웹 서비스를 사용한 예측 실험 원래 hello를 열고 클릭 하 여 편집 가능한 복사본을 만들 **SAVE AS**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-224">tooupdate hello web service, open hello original predictive experiment you used toodeploy hello web service and make an editable copy by clicking **SAVE AS**.</span></span> <span data-ttu-id="8d79c-225">변경한 다음 **웹 서비스 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-225">Make your changes and then click **Deploy Web Service**.</span></span>

<span data-ttu-id="8d79c-226">하기 전에이 실험을 배포한 때문에 toooverwrite (클래식 웹 서비스) 또는 업데이트 (새 웹 서비스) hello 기존 서비스 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-226">Because you've deployed this experiment before, you are asked if you want toooverwrite (Classic Web Service) or update (New web service) hello existing service.</span></span> <span data-ttu-id="8d79c-227">클릭 하면 **예** 또는 **업데이트** hello 기존 웹 서비스를 중지 하 고 배포 hello 새 예측 실험 그 자리에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-227">Clicking **YES** or **Update** stops hello existing web service and deploys hello new predictive experiment is deployed in its place.</span></span>

> [!NOTE]
> <span data-ttu-id="8d79c-228">Hello 원래 웹 서비스의 구성을 변경 하는 경우 예를 들어 새로운 표시 이름이 나 설명, 입력 값이 필요 합니다 tooenter 이러한 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-228">If you made configuration changes in hello original web service, for example, entering a new display name or description, you will need tooenter those values again.</span></span>
> 
> 

<span data-ttu-id="8d79c-229">웹 서비스를 업데이트 하기 위한 한 가지 옵션은 프로그래밍 방식으로 tooretrain hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="8d79c-229">One option for updating your web service is tooretrain hello model programmatically.</span></span> <span data-ttu-id="8d79c-230">자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d79c-230">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

<!-- internal links -->
[학습 실험 만들기]: #create-a-training-experiment
[Tooa 예측 실험으로 변환]: #convert-the-training-experiment-to-a-predictive-experiment
[앱 서비스로 배포]: #deploy-it-as-a-web-service
[신규]: #deploy-the-predictive-experiment-as-a-new-Web-service
[기존]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
