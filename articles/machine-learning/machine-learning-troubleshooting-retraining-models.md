---
title: "Azure Machine Learning 클래식 웹 서비스의 재학습 문제 해결 | Microsoft Docs"
description: "Azure Machine Learning 웹 서비스에 대한 모델을 재학습하는 경우에 발생하는 일반적인 문제를 파악하고 바로 잡습니다."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="2238e-103">Azure Machine Learning 기존 웹 서비스의 재학습 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2238e-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="2238e-104">재학습 개요</span><span class="sxs-lookup"><span data-stu-id="2238e-104">Retraining overview</span></span>
<span data-ttu-id="2238e-105">예측 실험을 점수 매기기 웹 서비스로 배포하는 경우 정적 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="2238e-106">새 데이터를 사용할 수 있는 경우 또는 API 소비자가 자체적인 데이터를 가진 경우 모델을 재학습해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="2238e-107">기존 웹 서비스 재학습 프로세스의 자세한 연습은 [프로그래밍 방식으로 Machine Learning 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2238e-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="2238e-108">재학습 프로세스</span><span class="sxs-lookup"><span data-stu-id="2238e-108">Retraining process</span></span>
<span data-ttu-id="2238e-109">웹 서비스를 다시 학습해야 할 경우, 몇 가지 추가 요소를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="2238e-110">학습 실험에서 배포된 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="2238e-111">실험에는 **모델 학습** 모듈의 출력에 연결된 **웹 서비스 출력** 모듈이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![모델 학습에 웹 서비스 출력을 연결합니다.][image1]
* <span data-ttu-id="2238e-113">점수 매기기 웹 서비스에 추가된 새 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="2238e-114">프로그래밍 방식으로 항목 또는 Azure 클래식 포털을 통해 Machine Learning 재학습 모델에서 참조한 샘플 코드를 사용하여 프로그래밍 방식으로 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="2238e-115">그런 다음 학습 웹 서비스 API 도움말 페이지에서 샘플 C# 코드를 사용하여 모델을 재학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="2238e-116">결과를 평가했고 만족한다면 추가한 새 끝점을 사용하여 학습된 모델 점수 매기기 웹 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="2238e-117">모든 준비가 된 경우 모델을 재학습하기 위해 취해야 할 주요 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="2238e-118">학습 웹 서비스 호출: RRS(요청 응답 서비스)가 아닌 BES(일괄 처리 실행 서비스)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="2238e-119">API 도움말 페이지에 나오는 샘플 C# 코드를 사용하여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="2238e-120">*BaseLocation*, *RelativeLocation* 및 *SasBlobToken*에 대한 값 찾기: 학습 웹 서비스에 대한 호출에서 이러한 값을 출력에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="2238e-121">![재학습 샘플의 출력 및 BaseLocation, RelativeLocation 및 SasBlobToken 값을 표시합니다.][image6]</span><span class="sxs-lookup"><span data-stu-id="2238e-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="2238e-122">새 학습된 모델을 사용하여 점수 매기기 웹 서비스에서 추가된 끝점 업데이트하기: 프로그래밍 방식으로 기계 학습 모델 재학습에서 제공된 샘플 코드를 사용하여 학습 웹 서비스에서 새로 학습된 모델로 점수 매기기 모델에 추가한 새 끝점을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="2238e-123">일반적인 장애물</span><span class="sxs-lookup"><span data-stu-id="2238e-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="2238e-124">PATCH URL이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="2238e-125">사용 중인 PATCH URL은 점수 매기기 웹 서비스에 추가한 새 점수 매기기 끝점과 연결된 것이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="2238e-126">PATCH URL을 얻는 데는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="2238e-127">**옵션 1: 프로그래밍 방식으로**</span><span class="sxs-lookup"><span data-stu-id="2238e-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="2238e-128">올바른 PATCH URL을 가지려면:</span><span class="sxs-lookup"><span data-stu-id="2238e-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="2238e-129">[AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 샘플 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="2238e-130">AddEndpoint의 출력에서 *HelpLocation* 값을 찾아 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![addEndpoint 샘플의 출력에 있는 HelpLocation.][image2]
3. <span data-ttu-id="2238e-132">브라우저에 URL을 붙여넣어 웹 서비스에 대한 도움말 링크를 제공하는 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="2238e-133">**리소스 업데이트** 링크를 클릭하여 패치 도움말 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="2238e-134">**옵션 2: Azure 클래식 포털 사용**</span><span class="sxs-lookup"><span data-stu-id="2238e-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="2238e-135">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2238e-136">기계 학습 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="2238e-137">![Machine Leaning 탭.][image4]</span><span class="sxs-lookup"><span data-stu-id="2238e-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="2238e-138">작업 영역 이름을 클릭한 후 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="2238e-139">현재 작업 중인 점수 매기기 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="2238e-140">(웹 서비스의 기본 이름을 수정하지 않은 경우 결국 [Scoring Exp.]이 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="2238e-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="2238e-141">**끝점 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="2238e-142">끝점이 추가된 후 끝점 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="2238e-143">그런 후에 패치하려는 도움말 페이지를 열려면 **리소스 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="2238e-144">예측 웹 서비스 대신 학습 웹 서비스에 끝점을 추가한 경우 **업데이트 리소스** 링크를 클릭하면 다음과 같은 오류가 발생합니다. 죄송합니다. 이 기능은 지원되지 않거나 이 컨텍스트에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="2238e-145">이 웹 서비스에 업데이트할 수 있는 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="2238e-146">불편을 끼쳐 드려 죄송합니다. 이 워크플로를 개선하도록 작업 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![새 끝점 대시보드.][image3]

<span data-ttu-id="2238e-148">PATCH 도움말 페이지에는 사용해야 하는 PATCH URL이 들어 있으며 호출하는 데 사용할 수 있는 샘플 코드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![패치 URL.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="2238e-150">올바른 점수 매기기 끝점을 업데이트하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="2238e-151">학습 웹 서비스를 패치하지 마십시오. 패치 작업은 점수 매기기 웹 서비스에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="2238e-152">기본 끝점을 웹 서비스에서 패치하지 마십시오. 패치 작업은 추가한 새 점수 매기기 웹 서비스 끝점에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="2238e-153">Azure 클래식 포털을 방문하여 끝점이 어떤 웹 서비스에 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="2238e-154">끝점을 학습 웹 서비스가 아닌 예측 웹 서비스에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="2238e-155">학습 및 예측 웹 서비스를 모두 올바르게 배포한 경우 나열된 두 개의 별도 웹 서비스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="2238e-156">예측 웹 서비스는 "[예측 exp.]"로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="2238e-157">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2238e-158">기계 학습 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="2238e-159">![Machine Learning 작업 영역 UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="2238e-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="2238e-160">작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-160">Select your workspace.</span></span>
4. <span data-ttu-id="2238e-161">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="2238e-162">예측 웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="2238e-163">웹 서비스에 새 끝점이 추가되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="2238e-164">웹 서비스가 있는 작업 영역을 확인하여 올바른 영역에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="2238e-165">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2238e-166">메뉴에서 기계 학습을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="2238e-167">![Machine Learning 하위 지역 UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="2238e-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="2238e-168">작업 영역의 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2238e-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
