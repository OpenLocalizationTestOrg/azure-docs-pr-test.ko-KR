---
title: "Azure Machine Learning에서 새 웹 서비스 배포 | Microsoft Docs"
description: "ARM 기반 웹 서비스를 배포하는 워크플로"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="93688-103">새 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="93688-103">Deploy a new web service</span></span>
<span data-ttu-id="93688-104">Microsoft Azure Machine Learning은 이제 새 청구 계획 옵션을 허용하고 여러 지역에 웹 서비스를 배포하는 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 를 기반으로 하는 웹 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="93688-105">Microsoft Azure 기계 학습 웹 서비스를 사용하여 웹 서비스를 배포하는 일반적인 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93688-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="93688-106">예측 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="93688-106">Create a predictive experiment</span></span>
* <span data-ttu-id="93688-107">배포</span><span class="sxs-lookup"><span data-stu-id="93688-107">deploy it</span></span>
* <span data-ttu-id="93688-108">해당 이름 구성</span><span class="sxs-lookup"><span data-stu-id="93688-108">configure its name</span></span>
* <span data-ttu-id="93688-109">요금제</span><span class="sxs-lookup"><span data-stu-id="93688-109">billing plan</span></span>
* <span data-ttu-id="93688-110">테스트</span><span class="sxs-lookup"><span data-stu-id="93688-110">test it</span></span>
* <span data-ttu-id="93688-111">사용</span><span class="sxs-lookup"><span data-stu-id="93688-111">consume it.</span></span>

<span data-ttu-id="93688-112">다음 그래픽에서는 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93688-112">The following graphic illustrates the workflow.</span></span>

![웹 서비스 배포 워크플로][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="93688-114">Studio에서 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="93688-114">Deploy web service from Studio</span></span>
<span data-ttu-id="93688-115">실험을 새 웹 서비스로 배포하려면.</span><span class="sxs-lookup"><span data-stu-id="93688-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="93688-116">기계 학습 스튜디오에 로그인하고 새 예측 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93688-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="93688-117">**참고**: 실험을 기존 웹 서비스로 이미 배포한 경우 새 웹 서비스로 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93688-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="93688-118">실험 캔버스의 맨 아래에서 **실행**을 클릭한 다음 **웹 서비스 배포** 및 **웹 서비스 배포[신규]**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="93688-119">기계 학습 웹 서비스 관리자의 배포 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="93688-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="93688-120">기계 학습 웹 서비스 관리자 배포 실험 페이지</span><span class="sxs-lookup"><span data-stu-id="93688-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="93688-121">실험 배포 페이지에서 웹 서비스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="93688-122">가격 책정 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-122">Select a pricing plan.</span></span> <span data-ttu-id="93688-123">기존 가격 책정 계획이 있는 경우 해당 계획을 선택하고 그렇지 않으면 서비스에 대한 새 가격 계획을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="93688-124">**가격 계획** 드롭다운에서 기존 계획을 선택하거나 **새 계획 선택** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="93688-125">**계획 이름**에 청구서의 계획을 식별하는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="93688-126">**월별 계획 계층**중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="93688-127">계획 계층이 기본적으로 기본 영역에 대한 계획으로 설정되고 웹 서비스는 해당 지역에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="93688-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="93688-128">**배포** 를 클릭하면 웹 서비스에 대한 빠른 시작 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93688-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="93688-129">빠른 시작 페이지</span><span class="sxs-lookup"><span data-stu-id="93688-129">Quickstart page</span></span>
<span data-ttu-id="93688-130">웹 서비스 빠른 시작 페이지를 사용하면 새 웹 서비스를 만든 후 수행할 가장 일반적인 작업에 대한 액세스 권한 및 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="93688-131">여기에서 **테스트** 페이지 및 **사용** 페이지에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93688-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="93688-132">웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="93688-132">Testing your web service</span></span>
<span data-ttu-id="93688-133">빠른 시작 페이지에서 일반적인 작업의 웹 서비스 테스트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="93688-134">웹 서비스를 RRS(요청-응답 서비스)로 테스트하려면:</span><span class="sxs-lookup"><span data-stu-id="93688-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="93688-135">메뉴 모음에서 **테스트** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="93688-136">**요청-응답**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="93688-137">실험의 입력 열에 적절한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="93688-138">**요청-응답**테스트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="93688-139">결과는 페이지의 오른쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93688-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="93688-140">BES(배치 실행 서비스) 웹 서비스를 테스트하려면 CSV 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="93688-141">메뉴 모음에서 **테스트** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="93688-142">**배치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-142">Click **Batch**.</span></span>
* <span data-ttu-id="93688-143">입력에서 찾아보기를 클릭하고 샘플 데이터 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="93688-144">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-144">Click **Test**.</span></span>

<span data-ttu-id="93688-145">테스트의 상태는 **배치 작업 테스트**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93688-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="93688-146">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="93688-146">Consuming your Web Service</span></span>
<span data-ttu-id="93688-147">웹 서비스로 배포된 경우 Azure 기계 학습 실험에서는 광범위한 장치 및 플랫폼에서 사용할 수 있는 REST API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="93688-148">이는 단순 REST API는 JSON 형식의 메시지를 허용하고 응답하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="93688-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="93688-149">Azure 기계 학습 포털에서는 웹 서비스를 호출하는 데 사용할 수 있는 R, C# 및 Python 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93688-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="93688-150">사용 페이지에서 다음을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93688-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="93688-151">앱에서 웹 서비스를 사용하기 위해 필요한 API 키 및 URI</span><span class="sxs-lookup"><span data-stu-id="93688-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="93688-152">사용 프로세스를 시작할 Excel 및 웹앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="93688-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="93688-153">시작할 C#, Python 및 R의 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="93688-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="93688-154">웹 서비스 사용에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 사용 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93688-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93688-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93688-155">Next Steps</span></span>
<span data-ttu-id="93688-156">웹 서비스 사용에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93688-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="93688-157">Azure Machine Learning 웹 서비스 사용 방법</span><span class="sxs-lookup"><span data-stu-id="93688-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="93688-158">Azure 기계 학습 웹 서비스: 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="93688-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
