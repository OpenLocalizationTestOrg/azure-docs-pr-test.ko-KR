---
title: "기계 학습 aaaRetrain를 프로그래밍 방식으로 모델링 | Microsoft Docs"
description: "어떻게 tooprogrammatically 모델을 다시 학습 모델 및 업데이트 hello 웹 서비스 toouse hello 새로 학습 된 Azure 기계 학습에서에 대해 알아봅니다."
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
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="77c7a-103">프로그래밍 방식으로 기계 학습 모델 다시 학습</span><span class="sxs-lookup"><span data-stu-id="77c7a-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="77c7a-104">이 연습에서는 tooprogrammatically 다시 C# 및 hello 기계 학습 일괄 처리 실행 서비스를 사용 하는 Azure 기계 학습 웹 서비스를 학습 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="77c7a-105">일단 hello 모델을 유지 하는 연습을 수행 하는 hello tooupdate 예측 웹 서비스에서 모델을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="77c7a-106">Hello 컴퓨터 학습 웹 서비스 포털의 기본 웹 서비스를 배포한 경우 참조 [클래식 웹 서비스를 다시 학습](machine-learning-retrain-a-classic-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="77c7a-107">새 웹 서비스를 배포한 경우 참조 [hello 컴퓨터 학습 관리 cmdlet을 사용 하 여 새 웹 서비스를 다시 학습](machine-learning-retrain-new-web-service-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="77c7a-108">Hello 재교육 프로세스의 개요를 참조 하십시오. [기계 학습 모델을 다시 학습](machine-learning-retrain-machine-learning-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="77c7a-109">새 Azure 리소스 관리자 기반 웹 서비스는 기존 toostart 하려는 경우, 참조 [기존 예측 웹 서비스를 다시 학습](machine-learning-retrain-existing-resource-manager-based-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="77c7a-110">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="77c7a-110">Create a training experiment</span></span>
<span data-ttu-id="77c7a-111">이 예제에서는 사용 합니다 "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합" hello Microsoft Azure 기계 학습 샘플에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="77c7a-112">toocreate hello 실험:</span><span class="sxs-lookup"><span data-stu-id="77c7a-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="77c7a-113">TooMicrosoft Azure 기계 학습 스튜디오에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="77c7a-114">Hello의 오른쪽 아래 모서리 hello 대시보드, 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="77c7a-115">Microsoft 샘플 hello에서 샘플 5를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="77c7a-116">hello 실험 캔버스의 hello 위쪽 toorename hello 실험 hello 실험 이름을 선택 "샘플 5: 학습, 테스트 평가 이진 분류에 대 한: 성인 데이터 집합"입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="77c7a-117">Census Model을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-117">Type Census Model.</span></span>
6. <span data-ttu-id="77c7a-118">Hello 실험 캔버스의 hello 아래쪽 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="77c7a-119">**웹 서비스 설정**을 클릭하고 **재학습 웹 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="77c7a-120">hello 다음 hello 초기 실험을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-120">hello following shows hello initial experiment.</span></span>
   
   ![초기 실험.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="77c7a-122">예측 실험을 만들고 웹 서비스로 게시</span><span class="sxs-lookup"><span data-stu-id="77c7a-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="77c7a-123">다음으로 서술적 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="77c7a-124">Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **예측 웹 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="77c7a-125">Hello 모델을 학습 된 모델로 저장 웹 서비스 입력 및 출력 모듈을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="77c7a-126">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-126">Click **Run**.</span></span> 
3. <span data-ttu-id="77c7a-127">Hello 실험 실행이 종료 된 후 클릭 **웹 서비스 배포 [기본]** 또는 **웹 서비스 배포 [New]**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="77c7a-128">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="77c7a-129">자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="77c7a-130">Hello 학습 실험을 교육 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="77c7a-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="77c7a-131">tooretrain hello 학습 된 모델 Retraining 웹 서비스로 작성 하는 hello 학습 실험을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="77c7a-132">이 웹 서비스는 *웹 서비스 출력* 모듈 연결 toohello  *[모델 학습] [ train-model]*  모듈, 새로운 toobe 수 tooproduce 학습 된 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="77c7a-133">tooreturn toohello 학습 실험 hello 왼쪽된 창에서 hello 실험 아이콘 클릭 Census 모델 이라는 hello 실험을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="77c7a-134">Hello 검색 실험 항목 검색 상자에 웹 서비스를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="77c7a-135">끌어서는 *웹 서비스 입력* hello에 모듈 캔버스를 실험 하 고 해당 출력 toohello 연결 *누락 데이터 정리* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="77c7a-136">이렇게 하면 재교육 데이터 처리는 hello 동일한 방식으로 원래 학습 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="77c7a-137">두 개 *웹 서비스 출력* hello에 모듈 실험 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="77c7a-138">Hello hello 출력에 연결 *모델 학습* 모듈 tooone 및 hello 출력의 hello *모델 평가* 다른 모듈 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="77c7a-139">에 대 한 웹 서비스 출력 hello **모델 학습** hello 새 학습 된 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="77c7a-140">너무 연결 된 출력 hello**모델 평가** hello 성능 결과 해당 모듈의 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="77c7a-141">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-141">Click **Run**.</span></span> 

<span data-ttu-id="77c7a-142">그런 다음 학습된 된 모델 및 모델 평가 결과 생성 하는 웹 서비스는 hello 학습 실험을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="77c7a-143">기본 웹 서비스 또는 새 웹 서비스를 사용 하 여 작업할 여부에 종속 되어이 작업의 다음 집합 tooaccomplish 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="77c7a-144">**기존 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="77c7a-144">**Classic web service**</span></span>

<span data-ttu-id="77c7a-145">Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **웹 서비스 배포 [기본]**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="77c7a-146">웹 서비스 hello **대시보드** 일괄 처리 실행에 대 한 API 키와 hello API hello 도움말 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="77c7a-147">학습 된 모델을 만들기 위한 hello 일괄 처리 실행 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="77c7a-148">**새 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="77c7a-148">**New web service**</span></span>

<span data-ttu-id="77c7a-149">Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정** 선택 **웹 서비스 배포 [New]**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="77c7a-150">hello 웹 서비스 Azure 컴퓨터 학습 웹 서비스 포털 toohello 배포 웹 서비스 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="77c7a-151">웹 서비스의 이름을 입력하고 결제 방식을 선택한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="77c7a-152">Hello 일괄 처리 실행 방법 학습 된 모델을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="77c7a-153">두 경우 모두 실험의 실행을 완료 한 후 hello 결과 워크플로가 표시 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![실행 후 결과 워크플로.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="77c7a-155">Hello 모델 BES를 사용 하 여 새 데이터를 보존 하기 위해</span><span class="sxs-lookup"><span data-stu-id="77c7a-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="77c7a-156">이 예제에서는 C# toocreate hello 재교육 응용 프로그램에 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="77c7a-157">사용할 수도 있습니다 hello Python 또는 R 샘플 코드 tooaccomplish이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="77c7a-158">toocall hello 재교육 Api:</span><span class="sxs-lookup"><span data-stu-id="77c7a-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="77c7a-159">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="77c7a-160">기계 학습 웹 서비스 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="77c7a-161">기존 웹 서비스를 사용하여 작업하는 경우 **Classic Web Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="77c7a-162">사용 하는 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="77c7a-163">Hello 기본 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="77c7a-164">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="77c7a-165">Hello hello 맨 아래에 **사용** 페이지 hello **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="77c7a-166">이 절차의 5 toostep를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="77c7a-167">새 웹 서비스를 사용하여 작업하는 경우 **Web Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="77c7a-168">사용 하는 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="77c7a-169">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="77c7a-170">Hello hello에서 hello 사용 페이지 맨 아래에 **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="77c7a-171">일괄 처리 실행에 대 한 hello 샘플 C# 코드를 복사 하 고 hello Program.cs 파일에 붙여넣습니다 이때 hello 네임 스페이스를 그대로 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="77c7a-172">Hello 설명에 지정 된 대로 Microsoft.AspNet.WebApi.Client hello Nuget 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="77c7a-173">tooadd hello 참조 tooMicrosoft.WindowsAzure.Storage.dll Microsoft Azure 저장소 서비스에 대 한 tooinstall hello 클라이언트 라이브러리를 먼저 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="77c7a-174">자세한 내용은 [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77c7a-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="77c7a-175">Hello apikey 선언 업데이트</span><span class="sxs-lookup"><span data-stu-id="77c7a-175">Update hello apikey declaration</span></span>
<span data-ttu-id="77c7a-176">Hello 찾을 **apikey** 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="77c7a-177">Hello에 **기본 소비 정보** hello 섹션 **사용** 페이지 hello 기본 키 찾아 toohello 복사 **apikey** 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="77c7a-178">Hello Azure 저장소 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="77c7a-179">hello BES 샘플 코드는 로컬 드라이브 (예: "C:\temp\CensusIpnput.csv") tooAzure 저장소에서에서 파일을 업로드 하 고 처리 한 hello 결과 백 tooAzure 저장소를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="77c7a-180">tooaccomplish이이 태스크에서는 hello 코드의 값에 해당 하는 hello 업데이트 및 hello 클래식 Azure 포털에서 저장소 계정에 대 한 hello 저장소 계정 이름, 키 및 컨테이너 정보를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="77c7a-181">Toohello 클래식 Azure 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="77c7a-182">Hello 왼쪽된 탐색 열에서 클릭 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="77c7a-183">Hello 저장소 계정 목록에서 선택 하나 toostore hello 모델을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="77c7a-184">Hello hello 페이지의 아래쪽에 있는 클릭 **액세스 키 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="77c7a-185">복사 하 고 hello 저장 **기본 액세스 키** 및 닫기 hello 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="77c7a-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="77c7a-186">Hello hello 페이지의 위쪽에 클릭 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="77c7a-187">기존 컨테이너를 선택 하거나 새 만들고 hello 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="77c7a-188">Hello 찾을 *StorageAccountName*, *StorageAccountKey*, 및 *StorageContainerName* 선언 및에서 저장 하는 hello 값 업데이트 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="77c7a-189">또한 hello 코드에서 지정 하는 hello 위치의 hello 입력된 파일을 사용할 수 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="77c7a-190">Hello 출력 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-190">Specify hello output location</span></span>
<span data-ttu-id="77c7a-191">Hello 요청 페이로드를 hello 출력 위치를 지정할 때는 hello에 지정 된 hello 파일의 확장명 *RelativeLocation* ilearner로 지정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="77c7a-192">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="77c7a-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="77c7a-193">출력 위치 hello 형태의 hello 웹 서비스 출력 모듈 추가한 hello 순서에 따라이 연습에서 hello에서 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="77c7a-194">이 두 개의 출력을 사용 하 여 학습 실험을 설정한 이후 hello 결과 둘 모두에 대 한 저장소 위치 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![재학습 출력][6]

<span data-ttu-id="77c7a-196">다이어그램 4: 재학습 출력.</span><span class="sxs-lookup"><span data-stu-id="77c7a-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="77c7a-197">Hello 재교육 결과 평가</span><span class="sxs-lookup"><span data-stu-id="77c7a-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="77c7a-198">Hello 응용 프로그램을 실행 하면 hello 출력 hello URL이 포함 하 고 SAS 토큰 필요한 tooaccess hello 평가 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="77c7a-199">Hello를 결합 하 여 hello 다시 학습 되도록 모델의 hello 성능 결과 볼 수 있습니다 *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과에서 에 대 한 *output2* (에서처럼 hello 재교육 출력 이미지 이전) 및 hello 브라우저 주소 표시줄에 hello 전체 URL 붙여넣기 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="77c7a-200">Hello 새로 학습 된 모델 하나 기존 tooreplace hello 충분히 잘 수행 하는지 여부 hello 결과 toodetermine를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="77c7a-201">복사 hello *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과 통해 사용할 것 hello 재교육 프로세스 중입니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77c7a-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77c7a-202">Next steps</span></span>
<span data-ttu-id="77c7a-203">클릭 하 여 hello 예측 웹 서비스를 배포한 경우 **웹 서비스 배포 [기본]**, 참조 [클래식 웹 서비스를 다시 학습](machine-learning-retrain-a-classic-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="77c7a-204">클릭 하 여 hello 예측 웹 서비스를 배포한 경우 **웹 서비스 배포 [New]**, 참조 [hello 컴퓨터 학습 관리 cmdlet을 사용 하 여 새 웹 서비스를 다시 학습](machine-learning-retrain-new-web-service-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77c7a-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
