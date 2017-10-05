---
title: "프로그래밍 방식으로 Machine Learning 모델 다시 학습 | Microsoft Docs"
description: "Azure 기계 학습에서 프로그래밍 방식으로 모델을 다시 학습하고 새로 학습된 모델을 사용하도록 웹 서비스를 업데이트하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="8a969-103">프로그래밍 방식으로 기계 학습 모델 다시 학습</span><span class="sxs-lookup"><span data-stu-id="8a969-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="8a969-104">이 연습에서는 C# 및 Machine Learning Batch Execution 서비스를 사용하여 Azure Machine Learning 웹 서비스를 프로그래밍 방식으로 다시 학습하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="8a969-105">모델을 다시 학습한 후 다음 연습에서는 예측 웹 서비스에서 모델을 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="8a969-106">Machine Learning 웹 서비스 포털에서 기존 웹 서비스를 배포한 경우 [기존 웹 서비스 재학습](machine-learning-retrain-a-classic-web-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="8a969-107">새 웹 서비스를 배포한 경우 [Machine Learning Management cmdlet을 사용하여 새 웹 서비스 재학습](machine-learning-retrain-new-web-service-using-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="8a969-108">재학습 프로세스의 개요의 경우 [Machine Learning 모델 재학습](machine-learning-retrain-machine-learning-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="8a969-109">기존의 새 Azure Resource Manager 기반 웹 서비스로 시작하려는 경우 [기존 예측 웹 서비스 재학습](machine-learning-retrain-existing-resource-manager-based-web-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="8a969-110">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="8a969-110">Create a training experiment</span></span>
<span data-ttu-id="8a969-111">이 예의 경우 Microsoft Azure 기계 학습 샘플의 "샘플 5: 이진 분류에 대한 학습, 테스트, 평가: 성인 데이터 집합"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="8a969-112">실험을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="8a969-112">To create the experiment:</span></span>

1. <span data-ttu-id="8a969-113">Microsoft Azure 기계 학습 스튜디오에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="8a969-114">대시보드의 오른쪽 아래 모서리에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="8a969-115">Microsoft 샘플에서 샘플 5를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="8a969-116">실험의 이름을 바꾸려면 실험 캔버스의 위쪽에서 실험 이름 "샘플 5: 이진 분류에 대한 학습, 테스트, 평가: 성인 데이터 집합"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="8a969-117">Census Model을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-117">Type Census Model.</span></span>
6. <span data-ttu-id="8a969-118">실험 캔버스 맨 아래에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="8a969-119">**웹 서비스 설정**을 클릭하고 **재학습 웹 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="8a969-120">다음은 초기 실험을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-120">The following shows the initial experiment.</span></span>
   
   ![초기 실험.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="8a969-122">예측 실험을 만들고 웹 서비스로 게시</span><span class="sxs-lookup"><span data-stu-id="8a969-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="8a969-123">다음으로 서술적 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="8a969-124">실험 캔버스 맨 아래에서 **웹 서비스 설정**을 클릭하고 **예측 웹 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="8a969-125">모델을 학습된 모델로 저장한 다음 웹 서비스 입력 및 출력 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="8a969-126">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-126">Click **Run**.</span></span> 
3. <span data-ttu-id="8a969-127">실험 실행이 완료된 후 **웹 서비스 배포[기존]**을 클릭하고 **웹 서비스 배포[신규]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="8a969-128">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="8a969-129">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="8a969-130">학습 실험을 학습 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="8a969-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="8a969-131">학습된 모델을 다시 학습하려면 재학습 웹 서비스로 만든 학습 실험을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="8a969-132">이 웹 서비스가 학습된 모델을 새로 생성할 수 있으려면 *웹 서비스 출력* 모듈이 *[학습 모델][train-model]* 모듈에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="8a969-133">학습 실험으로 돌아가려면 왼쪽 창에서 실험 아이콘을 클릭한 다음 Census Model이라는 실험을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="8a969-134">실험 항목 검색 상자에 웹 서비스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="8a969-135">*웹 서비스 입력* 모듈을 실험 캔버스로 끌어 놓고 해당 출력을 *누락된 데이터 정리* 모듈에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="8a969-136">그러면 이 재학습 데이터가 원래 학습 데이터와 동일한 방식으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="8a969-137">두 *웹 서비스 출력* 모듈을 실험 캔버스로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="8a969-138">하나는 *모델 학습* 모듈의 출력에, 다른 하나는 *모델 평가* 모듈의 출력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="8a969-139">**학습 모델** 에 대한 웹 서비스 출력에서 새로 학습된 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="8a969-140">**모델 평가**에 연결된 출력은 성능 결과인 해당 모듈의 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="8a969-141">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-141">Click **Run**.</span></span> 

<span data-ttu-id="8a969-142">다음으로 학습 실험을 학습된 모델 및 모델 평가 결과를 생성하는 웹 서비스로 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="8a969-143">이를 위해 다음에 할 작업은 기존 웹 서비스 또는 새로운 웹 서비스 중 어떤 것을 사용하여 작업하는지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="8a969-144">**기존 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="8a969-144">**Classic web service**</span></span>

<span data-ttu-id="8a969-145">실험 캔버스 맨 아래에서 **웹 서비스 설정**을 클릭하고 **웹 서비스 배포[기존]**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="8a969-146">웹 서비스 **대시보드**가 배치 실행을 위한 API 키 및 API 도움말 페이지와 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="8a969-147">학습된 모델을 만들 때는 배치 실행 방법만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="8a969-148">**새 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="8a969-148">**New web service**</span></span>

<span data-ttu-id="8a969-149">실험 캔버스 맨 아래에서 **웹 서비스 설정**을 클릭하고 **웹 서비스 배포[신규]**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="8a969-150">Web Service Azure Machine Learning Web Services 포털은 웹 서비스 배포 페이지에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="8a969-151">웹 서비스의 이름을 입력하고 결제 방식을 선택한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="8a969-152">학습된 모델을 만들 때는 배치 실행 방법만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="8a969-153">어느 경우든 실험 실행이 완료된 후 결과 워크플로는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![실행 후 결과 워크플로.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="8a969-155">BES를 사용하여 새 데이터로 모델 다시 학습</span><span class="sxs-lookup"><span data-stu-id="8a969-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="8a969-156">이 예에서는 재학습 응용 프로그램을 만드는 데 C#을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="8a969-157">또한 Python 또는 R 샘플 코드를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="8a969-158">재학습 API를 호출하려면:</span><span class="sxs-lookup"><span data-stu-id="8a969-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="8a969-159">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="8a969-160">Machine Learning 웹 서비스 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="8a969-161">기존 웹 서비스를 사용하여 작업하는 경우 **Classic Web Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="8a969-162">현재 작업 중인 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="8a969-163">"기본" 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="8a969-164">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="8a969-165">**사용** 페이지의 맨 아래에 있는 **샘플 코드** 섹션에서 **Batch**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="8a969-166">이 절차의 5 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="8a969-167">새 웹 서비스를 사용하여 작업하는 경우 **Web Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="8a969-168">현재 작업 중인 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="8a969-169">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="8a969-170">사용 페이지의 맨 아래에 있는 **샘플 코드** 섹션에서 **Batch**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="8a969-171">배치 실행을 위해 샘플 C# 코드를 복사한 다음 네임스페이스를 그대로 유지하여 Program.cs 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="8a969-172">설명에서 지정된 대로 Nuget 패키지인 Microsoft.AspNet.WebApi.Client를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="8a969-173">Microsoft.WindowsAzure.Storage.dll에 참조를 추가하려면 우선 Microsoft Azure Storage 서비스용 클라이언트 라이브러리를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="8a969-174">자세한 내용은 [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="8a969-175">apikey 선언 업데이트</span><span class="sxs-lookup"><span data-stu-id="8a969-175">Update the apikey declaration</span></span>
<span data-ttu-id="8a969-176">**apikey** 선언을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="8a969-177">**사용** 페이지의 **기본 사용량 정보** 섹션에서 기본 키를 찾아 **apikey** 선언으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="8a969-178">Azure 저장소 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="8a969-178">Update the Azure Storage information</span></span>
<span data-ttu-id="8a969-179">BES 샘플 코드는 로컬 드라이브에서(예: "C:\temp\CensusIpnput.csv") Azure 저장소로 파일을 업로드하고 이를 처리하고 결과를 Azure 저장소에 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="8a969-180">이 작업을 수행하려면 Azure 클래식 포털에서 저장소 계정에 대한 저장소 계정 이름, 키 및 컨테이너 정보를 검색한 다음 코드에서 해당 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="8a969-181">클래식 Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="8a969-182">왼쪽 탐색 열에서 **Storage**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="8a969-183">저장소 계정 목록에서 하나를 선택하여 재학습된 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="8a969-184">페이지 맨 아래에 있는 **액세스 키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="8a969-185">**기본 액세스 키**를 복사하여 저장한 후 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="8a969-186">페이지 위쪽에서 **컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="8a969-187">기존 컨테이너를 선택하거나 새 컨테이너를 만들어 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="8a969-188">*StorageAccountName*, *StorageAccountKey* 및 *StorageContainerName* 선언을 찾아 Azure Portal에서 저장한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="8a969-189">또한 코드에 지정한 위치에서 입력 파일을 사용할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="8a969-190">출력 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-190">Specify the output location</span></span>
<span data-ttu-id="8a969-191">요청 페이로드에서 출력 위치를 지정할 때 *RelativeLocation* 에서 지정된 파일의 확장명을 csv에서 ilearner로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="8a969-192">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="8a969-193">출력 위치 이름은 웹 서비스 출력 모듈을 추가한 순서에 따라 이 연습의 출력 위치 이름과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="8a969-194">이 학습 실험을 두 개의 출력으로 설정했으므로 결과는 둘 모두에 대한 저장소 위치 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![재학습 출력][6]

<span data-ttu-id="8a969-196">다이어그램 4: 재학습 출력.</span><span class="sxs-lookup"><span data-stu-id="8a969-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="8a969-197">재학습 결과 평가</span><span class="sxs-lookup"><span data-stu-id="8a969-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="8a969-198">응용 프로그램을 실행할 때 출력은 평가 결과를 액세스하는 데 필요한 URL 및 SAS 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="8a969-199">*output2*에 대한 출력 결과의 *BaseLocation*, *RelativeLocation* 및 *SasBlobToken*을 조합하고(앞서 재학습 출력 이미지에 표시된 것처럼) 브라우저 주소 표시줄에 전체 URL을 붙여넣어 다시 학습된 모델의 성능 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="8a969-200">새로 학습된 모델이 기존 모델을 대체할 만큼 성능이 뛰어난지 여부를 확인하도록 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="8a969-201">출력 결과에서 *BaseLocation*, *RelativeLocation* 및 *SasBlobToken*을 복사합니다. 이는 재학습 프로세스 중에 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a969-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a969-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a969-202">Next steps</span></span>
<span data-ttu-id="8a969-203">**웹 서비스 배포[기존]**를 클릭하여 예측 웹 서비스를 배포한 경우 [기존 웹 서비스 재학습](machine-learning-retrain-a-classic-web-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="8a969-204">**웹 서비스 배포[신규]**를 클릭하여 예측 웹 서비스를 배포한 경우 [Machine Learning Management cmdlet을 사용하여 새 웹 서비스 재학습](machine-learning-retrain-new-web-service-using-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a969-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
