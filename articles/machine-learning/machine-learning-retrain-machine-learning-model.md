---
title: "기계 학습 모델 aaaRetrain | Microsoft Docs"
description: "Tooretrain 모델 및 update hello 웹 서비스 toouse hello 새로 학습 된 모델에 Azure 기계 학습 방법에 대해 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="ee5c4-103">Machine Learning 모델 재학습</span><span class="sxs-lookup"><span data-stu-id="ee5c4-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="ee5c4-104">Azure 기계 학습에서 기계 학습 모델의 해결해줍니다 hello 과정의 일환으로, 모델을 교육 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="ee5c4-105">그런 다음 사용할 있습니다 toocreate predicative 웹 서비스.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="ee5c4-106">hello 웹 서비스는 다음 웹 사이트, 대시보드 및 모바일 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="ee5c4-107">기계 학습을 사용하여 만드는 모델은 일반적으로 정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="ee5c4-108">때나 hello API의 hello 소비자가 새 데이터를 사용할 수 있게 됨 자신의 데이터 hello 모델에 다시 학습 되도록 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="ee5c4-109">재학습은 자주 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-109">Retraining may occur frequently.</span></span> <span data-ttu-id="ee5c4-110">Hello 프로그래밍 재교육 API 기능 hello 모델 hello Api 재교육 및 업데이트 hello 웹 서비스를 사용 하 여 hello 새로 학습 된 모델을 다시 학습 프로그래밍 방식으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="ee5c4-111">이 문서는 hello 재교육 프로세스를 설명 하 고 toouse 재교육 Api hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="ee5c4-112">다시 학습 이유: hello 문제 정의</span><span class="sxs-lookup"><span data-stu-id="ee5c4-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="ee5c4-113">학습 프로세스 hello 기계 학습의 일환으로, 데이터 집합을 사용 하 여 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="ee5c4-114">기계 학습을 사용하여 만드는 모델은 일반적으로 정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="ee5c4-115">때나 hello API의 hello 소비자가 새 데이터를 사용할 수 있게 됨 자신의 데이터 hello 모델에 다시 학습 되도록 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="ee5c4-116">이러한 시나리오에서 프로그래밍 방식으로 API를 제공 편리 tooallow 또는 hello 프로그램 Api toocreate 수, 일회성 또는 정기적으로 보존 하기 위해 자신의 데이터를 사용 하 여 hello 모델 클라이언트의 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="ee5c4-117">그런 다음, 재교육 hello 결과 평가 수 있으며 hello 웹 서비스 API toouse hello 새로 학습 된 모델 업데이트.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="ee5c4-118">기존 학습 실험 및 새 웹 서비스를 설정한 경우 다음 hello 연습 hello 다음 섹션에서에서 설명 하는 대신 기존 예측 웹 서비스 재 아웃 toocheck을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="ee5c4-119">종단 간 워크플로</span><span class="sxs-lookup"><span data-stu-id="ee5c4-119">End-to-end workflow</span></span>
<span data-ttu-id="ee5c4-120">hello 프로세스에서는 다음과 같은 구성 요소가 hello: A 학습 실험과 예측 실험을 웹 서비스로 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="ee5c4-121">학습된 된 모델을 학습 실험 hello tooenable 간섭할 학습된 된 모델의 hello 출력을 사용 하 여 웹 서비스로 게시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="ee5c4-122">따라서 API 액세스 toohello 모델을 학습을 다시 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="ee5c4-123">단계를 수행 하는 hello tooboth 새로 추가 되거나 기존의 웹 서비스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="ee5c4-124">Hello 초기 예측 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="ee5c4-125">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-125">Create a training experiment</span></span>
* <span data-ttu-id="ee5c4-126">예측 웹 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="ee5c4-127">예측 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="ee5c4-127">Deploy a predictive web service</span></span>

<span data-ttu-id="ee5c4-128">Hello 웹 서비스를 다시 학습:</span><span class="sxs-lookup"><span data-stu-id="ee5c4-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="ee5c4-129">학습 실험 tooallow 재교육에 대 한 업데이트</span><span class="sxs-lookup"><span data-stu-id="ee5c4-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="ee5c4-130">Hello 재교육 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="ee5c4-131">Hello 배치 실행 서비스 코드 tooretrain hello 모델을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ee5c4-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="ee5c4-132">Hello 이전 단계를 연습에 대 한 참조 [기계 학습을 다시 학습을 프로그래밍 방식으로 모델링](machine-learning-retrain-models-programmatically.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="ee5c4-133">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="ee5c4-134">자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="ee5c4-135">기존 웹 서비스를 배포한 경우:</span><span class="sxs-lookup"><span data-stu-id="ee5c4-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="ee5c4-136">Hello 예측 웹 서비스에 새 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="ee5c4-137">Hello 패치 URL 및 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="ee5c4-138">사용 하 여 hello 패치 URL toopoint hello hello에서 새 끝점에 모델을 다시 학습 되도록</span><span class="sxs-lookup"><span data-stu-id="ee5c4-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="ee5c4-139">Hello 이전 단계를 연습에 대 한 참조 [클래식 웹 서비스를 다시 학습](machine-learning-retrain-a-classic-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="ee5c4-140">문제가 재교육 클래식 웹 서비스를 실행 하면 참조 [hello 재교육 Azure 컴퓨터 학습 클래식 웹 서비스의 문제 해결](machine-learning-troubleshooting-retraining-models.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="ee5c4-141">새 웹 서비스를 배포한 경우:</span><span class="sxs-lookup"><span data-stu-id="ee5c4-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="ee5c4-142">Tooyour Azure 리소스 관리자 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="ee5c4-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="ee5c4-143">Hello 웹 서비스 정의 가져오기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-143">Get hello Web service definition</span></span>
* <span data-ttu-id="ee5c4-144">JSON으로 hello 웹 서비스 정의 내보내기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="ee5c4-145">Hello 참조 toohello 업데이트 `ilearner` hello JSON에에서 blob</span><span class="sxs-lookup"><span data-stu-id="ee5c4-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="ee5c4-146">웹 서비스 정의 hello JSON 가져오기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="ee5c4-147">새 웹 서비스 정의 된 hello 웹 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="ee5c4-148">Hello 이전 단계를 연습에 대 한 참조 [hello 컴퓨터 학습 관리 PowerShell cmdlet을 사용 하 여 새 웹 서비스를 다시 학습](machine-learning-retrain-new-web-service-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="ee5c4-149">hello 프로세스는 기존의 웹 서비스에 대 한 재교육를 설정 하기 위한 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![재학습 프로세스 개요][1]

<span data-ttu-id="ee5c4-151">새 웹 서비스에 대 한 재교육를 설정 하기 위한 hello 프로세스 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![재학습 프로세스 개요][7]

## <a name="other-resources"></a><span data-ttu-id="ee5c4-153">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="ee5c4-153">Other Resources</span></span>
* [<span data-ttu-id="ee5c4-154">Azure Data Factory를 사용하여 Azure Machine Learning 모델 재학습 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="ee5c4-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="ee5c4-155">PowerShell을 사용하여 한 실험에서 여러 Machine Learning 모델 및 웹 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="ee5c4-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="ee5c4-156">hello [AML 재교육 모델 사용 하 여 Api](https://www.youtube.com/watch?v=wwjglA8xllg) 동영상에서는 재교육 Api 및 PowerShell tooretrain 기계 학습 모델 hello를 사용 하 여 Azure 기계 학습에서 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="ee5c4-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

