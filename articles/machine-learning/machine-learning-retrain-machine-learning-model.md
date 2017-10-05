---
title: "Machine Learning 모델 재학습 | Microsoft Docs"
description: "Azure Machine Learning에서 모델을 다시 학습하고 새로 학습된 모델을 사용하도록 웹 서비스를 업데이트하는 방법을 알아봅니다."
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
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="5ff31-103">Machine Learning 모델 재학습</span><span class="sxs-lookup"><span data-stu-id="5ff31-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="5ff31-104">Azure 기계 학습에서 기계 학습 모델 운영 프로세스의 일부로 모델은 학습 및 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="5ff31-105">그런 다음 이를 서술적 웹 서비스를 만드는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="5ff31-106">그러면 웹 사이트, 대시보드 및 모바일 앱에서 웹 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="5ff31-107">기계 학습을 사용하여 만드는 모델은 일반적으로 정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="5ff31-108">새 데이터를 사용할 수 있는 경우 또는 API 소비자가 자체적인 데이터를 가진 경우 모델을 재학습해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="5ff31-109">재학습은 자주 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-109">Retraining may occur frequently.</span></span> <span data-ttu-id="5ff31-110">프로그래밍 방식의 재학습 API 기능을 사용하면 재학습 API를 통해 프로그래밍 방식으로 모델을 다시 학습하고 새로 학습된 모델과 함께 웹 서비스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="5ff31-111">이 문서에서는 재학습 프로세스를 설명하고 재학습 API를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="5ff31-112">다시 학습 이유: 문제 정의</span><span class="sxs-lookup"><span data-stu-id="5ff31-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="5ff31-113">기계 학습 훈련 프로세스의 일부로, 데이터 집합을 사용하여 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="5ff31-114">기계 학습을 사용하여 만드는 모델은 일반적으로 정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="5ff31-115">새 데이터를 사용할 수 있는 경우 또는 API 소비자가 자체적인 데이터를 가진 경우 모델을 재학습해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="5ff31-116">이러한 시나리오에서 개발자나 API 소비자는 프로그래밍 방식의 API를 통해 일회성이나 주기적으로 고유한 데이터를 사용하여 모델을 다시 학습할 수 있는 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="5ff31-117">그런 후에 다시 학습의 결과를 평가하고 새로 학습된 모델을 사용하도록 웹 서비스 API를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff31-118">기존 학습 실험 및 새 웹 서비스가 있다면 다음 섹션에서 언급된 연습을 수행하는 대신에 기존 예측 웹 서비스 재학습을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="5ff31-119">종단 간 워크플로</span><span class="sxs-lookup"><span data-stu-id="5ff31-119">End-to-end workflow</span></span>
<span data-ttu-id="5ff31-120">프로세스에 학습 실험 및 웹 서비스로 게시된 서술적 실험이 구성 요소로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="5ff31-121">학습된 모델을 다시 학습할 수 있으려면 학습 실험은 학습된 모델의 출력을 사용하여 웹 서비스로 게시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="5ff31-122">그러면 API가 다시 학습을 위해 모델에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="5ff31-123">다음 단계는 신규 및 기존 웹 서비스에 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="5ff31-124">초기 예측 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="5ff31-125">학습 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="5ff31-125">Create a training experiment</span></span>
* <span data-ttu-id="5ff31-126">예측 웹 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="5ff31-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="5ff31-127">예측 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5ff31-127">Deploy a predictive web service</span></span>

<span data-ttu-id="5ff31-128">웹 서비스 재학습:</span><span class="sxs-lookup"><span data-stu-id="5ff31-128">Retrain the Web service:</span></span>

* <span data-ttu-id="5ff31-129">재학습을 감안하여 학습 실험 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ff31-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="5ff31-130">재학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5ff31-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="5ff31-131">학습 실험의 일괄 처리 실행 서비스 코드를 사용하여 모델 재학습</span><span class="sxs-lookup"><span data-stu-id="5ff31-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="5ff31-132">이전 단계에 대한 연습은 [프로그래밍 방식으로 Machine Learning 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ff31-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="5ff31-133">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="5ff31-134">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ff31-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="5ff31-135">기존 웹 서비스를 배포한 경우:</span><span class="sxs-lookup"><span data-stu-id="5ff31-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="5ff31-136">예측 웹 서비스에 새 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="5ff31-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="5ff31-137">PATCH URL 및 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ff31-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="5ff31-138">PATCH URL을 사용하여 다시 학습된 모델의 새 끝점을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="5ff31-139">이전 단계에 대한 연습은 [기존 웹 서비스 재학습](machine-learning-retrain-a-classic-web-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ff31-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="5ff31-140">기존 웹 서비스를 다시 학습하는 데 있어 난관에 봉착한 경우 [Azure Machine Learning Classic Web 서비스 재학습 문제 해결](machine-learning-troubleshooting-retraining-models.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ff31-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="5ff31-141">새 웹 서비스를 배포한 경우:</span><span class="sxs-lookup"><span data-stu-id="5ff31-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="5ff31-142">Azure Resource Manager 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="5ff31-143">웹 서비스 정의 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ff31-143">Get the Web service definition</span></span>
* <span data-ttu-id="5ff31-144">JSON으로 웹 서비스 정의 내보내기</span><span class="sxs-lookup"><span data-stu-id="5ff31-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="5ff31-145">JSON에서 `ilearner` blob에 대한 참조 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ff31-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="5ff31-146">JSON을 웹 서비스 정의로 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ff31-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="5ff31-147">웹 서비스를 새 웹 서비스 정의로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="5ff31-148">이전 단계에 대한 연습은 [Machine Learning Management PowerShell cmdlets를 사용하여 새 웹 서비스 재학습](machine-learning-retrain-new-web-service-using-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ff31-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="5ff31-149">Classic Web 서비스에 대한 재학습을 설정하는 프로세스에는 다음 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![재학습 프로세스 개요][1]

<span data-ttu-id="5ff31-151">New Web 서비스에 대한 재학습을 설정하는 프로세스에는 다음 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![재학습 프로세스 개요][7]

## <a name="other-resources"></a><span data-ttu-id="5ff31-153">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="5ff31-153">Other Resources</span></span>
* [<span data-ttu-id="5ff31-154">Azure Data Factory를 사용하여 Azure Machine Learning 모델 재학습 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ff31-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="5ff31-155">PowerShell을 사용하여 한 실험에서 여러 Machine Learning 모델 및 웹 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="5ff31-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="5ff31-156">[API를 사용한 AML 재학습 모델](https://www.youtube.com/watch?v=wwjglA8xllg) 비디오는 Retraining API 및 PowerShell을 사용하여 Azure Machine Learning에서 만들어진 Machine Learning 모델을 재학습하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ff31-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

