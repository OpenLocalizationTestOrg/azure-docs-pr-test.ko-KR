---
title: "웹 서비스는 Azure 컴퓨터 학습 클래식 재교육 aaaTroubleshoot | Microsoft Docs"
description: "식별 하 고는 Azure 기계 학습 웹 서비스에 대 한 hello 모델 재교육는 일반적인 문제 이름을으로 해결 합니다."
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="37d1f-103">Hello 재교육 Azure 컴퓨터 학습 클래식 웹 서비스의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="37d1f-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="37d1f-104">재학습 개요</span><span class="sxs-lookup"><span data-stu-id="37d1f-104">Retraining overview</span></span>
<span data-ttu-id="37d1f-105">예측 실험을 점수 매기기 웹 서비스로 배포하는 경우 정적 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="37d1f-106">새 데이터를 사용할 수 있게 됨 또는 hello API의 hello 소비자가 데이터에 다시 학습 되도록 toobe hello 모델에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="37d1f-107">Hello 재교육 클래식 웹 서비스의 프로세스는 전체 연습은 참조 [보존 하기 위해 컴퓨터 학습 모델 프로그래밍 방식으로](machine-learning-retrain-models-programmatically.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="37d1f-108">재학습 프로세스</span><span class="sxs-lookup"><span data-stu-id="37d1f-108">Retraining process</span></span>
<span data-ttu-id="37d1f-109">Tooretrain hello 웹 서비스를 해야 하는 경우 일부 추가 항목을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="37d1f-110">Hello 학습 실험에서에서 배포 된 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="37d1f-111">hello 실험 있어야는 **웹 서비스 출력** 모듈이 연결의 hello toohello 출력 **모델 학습** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Hello 웹 서비스 출력 toohello 학습 모델을 연결 합니다.][image1]
* <span data-ttu-id="37d1f-113">새 끝점 tooyour 웹 서비스 점수 매기기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="37d1f-114">Hello 끝점을 프로그래밍 방식으로 추가할 수 있습니다 hello에서 참조 하는 hello 샘플 코드를 사용 하 여 다시 학습 기계 학습 모델 프로그래밍 방식으로 항목 또는 hello Azure 클래식 포털을 통해.</span><span class="sxs-lookup"><span data-stu-id="37d1f-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="37d1f-115">다음 샘플 C# 코드 hello hello 학습 웹 서비스의 API 도움말 페이지 tooretrain 모델에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="37d1f-116">Hello 결과 평가 하 여 만족 되 면, 웹 서비스 사용자가 추가한 hello 새 끝점을 사용 하 여 점수 매기기 hello 학습 된 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="37d1f-117">모든 hello 작업으로 tooretrain hello 모델을 수행 해야 하는 hello 주요 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="37d1f-118">Hello 학습 웹 서비스 호출: 요청 응답 서비스 (RR) 하지 hello, hello 호출은 toohello 일괄 처리 실행 서비스 (BES)입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="37d1f-119">Hello API 도움말 페이지 toomake hello 호출 hello 샘플 C# 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="37d1f-120">Hello에 대 한 hello 값을 찾을 *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken*: hello 출력에 프로그램 호출 toohello 교육 웹에서에서 이러한 값이 반환 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="37d1f-121">![샘플 및 hello BaseLocation, RelativeLocation, 및 SasBlobToken 값 재교육 hello의 hello 출력을 표시 합니다.][image6]</span><span class="sxs-lookup"><span data-stu-id="37d1f-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="37d1f-122">학습 된 모델에서 새 웹 서비스 hello와 점수 매기기 hello 끝점 업데이트 hello 추가: hello 보존 하기 위해 기계 학습에서에서 모델을 프로그래밍 방식으로 hello 새 끝점 업데이트 제공 hello 샘플 코드를 사용 하 여 추가한 toohello 새로 hello 사용 하 여 모델 점수 매기기 hello 학습 웹 서비스에서에서 학습 된 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="37d1f-123">일반적인 장애물</span><span class="sxs-lookup"><span data-stu-id="37d1f-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="37d1f-124">올바른 URL 패치 hello 있으면 toosee 확인</span><span class="sxs-lookup"><span data-stu-id="37d1f-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="37d1f-125">hello 패치 URL을 사용 하는 hello hello에 연결 되어 있어야 합니다. 새 점수 매기기 끝점용 추가한 toohello 웹 서비스를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="37d1f-126">다양 한 방법으로 tooobtain hello 패치 URL에는</span><span class="sxs-lookup"><span data-stu-id="37d1f-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="37d1f-127">**옵션 1: 프로그래밍 방식으로**</span><span class="sxs-lookup"><span data-stu-id="37d1f-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="37d1f-128">tooget hello 패치 URL을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="37d1f-129">Hello 실행 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="37d1f-130">Hello AddEndpoint의 출력에서 찾을 hello *HelpLocation* 값 및 hello URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation hello addEndpoint 샘플의 hello 출력에서 합니다.][image2]
3. <span data-ttu-id="37d1f-132">Hello URL을 hello 웹 서비스에 대 한 도움말 링크를 제공 하는 브라우저 toonavigate tooa 페이지에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="37d1f-133">Hello 클릭 **업데이트 리소스** 링크 tooopen hello 패치 도움말 페이지.</span><span class="sxs-lookup"><span data-stu-id="37d1f-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="37d1f-134">**옵션 2: hello Azure 클래식 포털 사용**</span><span class="sxs-lookup"><span data-stu-id="37d1f-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="37d1f-135">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="37d1f-136">열기 hello 기계 학습 탭 합니다. ![Machine Leaning 탭.][image4]</span><span class="sxs-lookup"><span data-stu-id="37d1f-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="37d1f-137">작업 영역 이름을 클릭한 후 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="37d1f-138">웹 서비스를 사용 하는 점수 매기기 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="37d1f-139">(Hello 웹 서비스의 hello 기본 이름을 수정 하지 않은 경우 끝납니다 [점수 매기기 Exp].의 합니다.)</span><span class="sxs-lookup"><span data-stu-id="37d1f-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="37d1f-140">**끝점 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="37d1f-141">Hello 끝점 추가 되 면 hello 끝점 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="37d1f-142">클릭 **업데이트 리소스** tooopen hello 도움말 페이지를 패치 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="37d1f-143">Hello hello를 클릭할 때 다음 오류가 표시는 hello 예측 웹 서비스 대신 hello 끝점 toohello 학습 웹 서비스를 추가한 경우 **업데이트 리소스** 링크: 죄송 합니다. 하지만이 기능은 지원 되지 않는 또는 이 컨텍스트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="37d1f-144">이 웹 서비스에 업데이트할 수 있는 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="37d1f-145">이 워크플로 개선으로 작업 하 hello 불편을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![새 끝점 대시보드.][image3]

<span data-ttu-id="37d1f-147">hello를 사용 해야 하는 패치 URL을 포함 하 고 예제 코드를 사용할 수 있습니다를 제공 하는 hello 패치 도움말 페이지 toocall 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![패치 URL.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="37d1f-149">Toosee hello 올바른 점수 매기기 끝점을 업데이트 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="37d1f-150">Hello 학습 웹 서비스를 패치 하지 않습니다: 웹 서비스를 평가 하는 hello에서 hello 패치 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="37d1f-151">웹 서비스에 대 한 hello 기본 끝점을 패치 하지 않습니다: hello 패치 작업 hello 새로운 사용자가 추가한 웹 서비스 끝점 점수 매기기에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="37d1f-152">웹 서비스 hello 끝점으로 설정 되어 방문 hello Azure 클래식 포털을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="37d1f-153">Hello 끝점 toohello 예측 웹 서비스, 하지 hello 학습 웹 서비스를 추가 하는 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="37d1f-154">학습 및 예측 웹 서비스를 모두 올바르게 배포한 경우 나열된 두 개의 별도 웹 서비스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="37d1f-155">hello 예측 웹 서비스 "[예측 내선 번호]"로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="37d1f-156">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="37d1f-157">열기 hello 기계 학습 탭 합니다. ![Machine Learning 작업 영역 UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="37d1f-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="37d1f-158">작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-158">Select your workspace.</span></span>
4. <span data-ttu-id="37d1f-159">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="37d1f-160">예측 웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="37d1f-161">새 끝점 추가 toohello 웹 서비스 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="37d1f-162">웹 서비스에 tooensure은 hello 올바른 영역에 있는 hello 작업 영역 확인</span><span class="sxs-lookup"><span data-stu-id="37d1f-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="37d1f-163">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="37d1f-164">기계 학습 hello 메뉴에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="37d1f-165">![Machine Learning 하위 지역 UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="37d1f-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="37d1f-166">작업 영역의 hello 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d1f-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
