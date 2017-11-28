---
title: "Azure 기계 학습에서 새 웹 서비스 aaaDeploying | Microsoft Docs"
description: "ARM 배포 hello 워크플로 기반 웹 서비스"
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
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="d7df6-103">새 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="d7df6-103">Deploy a new web service</span></span>
<span data-ttu-id="d7df6-104">기반으로 하는 웹 서비스를 제공 하는 Microsoft Azure 기계 이제 학습 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 새 청구 계획 옵션 및 배포 하 여 웹 서비스 toomultiple 영역에 대 한 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="d7df6-105">다음은 hello 일반 워크플로 toodeploy Microsoft Azure 컴퓨터 학습 웹 서비스를 사용 하는 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="d7df6-106">예측 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="d7df6-106">Create a predictive experiment</span></span>
* <span data-ttu-id="d7df6-107">배포</span><span class="sxs-lookup"><span data-stu-id="d7df6-107">deploy it</span></span>
* <span data-ttu-id="d7df6-108">해당 이름 구성</span><span class="sxs-lookup"><span data-stu-id="d7df6-108">configure its name</span></span>
* <span data-ttu-id="d7df6-109">요금제</span><span class="sxs-lookup"><span data-stu-id="d7df6-109">billing plan</span></span>
* <span data-ttu-id="d7df6-110">테스트</span><span class="sxs-lookup"><span data-stu-id="d7df6-110">test it</span></span>
* <span data-ttu-id="d7df6-111">사용</span><span class="sxs-lookup"><span data-stu-id="d7df6-111">consume it.</span></span>

<span data-ttu-id="d7df6-112">다음 그래픽 hello hello 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-112">hello following graphic illustrates hello workflow.</span></span>

![웹 서비스 배포 워크플로][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="d7df6-114">Studio에서 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="d7df6-114">Deploy web service from Studio</span></span>
<span data-ttu-id="d7df6-115">새 웹 서비스 실험 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="d7df6-116">Hello 기계 학습 스튜디오에 로그인 하 고 새 예측 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="d7df6-117">**참고**: 실험을 기존 웹 서비스로 이미 배포한 경우 새 웹 서비스로 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="d7df6-118">클릭 **실행** hello hello 맨 아래에 캔버스를 실험 하 고 클릭 **웹 서비스 배포** 및 **웹 서비스 배포 [New]**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="d7df6-119">hello 기계 학습 웹 서비스 관리자의 hello 배포 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="d7df6-120">기계 학습 웹 서비스 관리자 배포 실험 페이지</span><span class="sxs-lookup"><span data-stu-id="d7df6-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="d7df6-121">Hello 실험 배포 페이지에서 hello 웹 서비스에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="d7df6-122">가격 책정 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-122">Select a pricing plan.</span></span> <span data-ttu-id="d7df6-123">기존 가격 책정 계획 선택할 수 있는 경우에 hello 서비스에 대 한 새 가격 계획을 만들어야 그렇지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="d7df6-124">Hello에 **가격 계획** 드롭 다운를 기존 계획을 선택 하거나 선택 hello **선택 새 계획** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="d7df6-125">**계획 이름**, 청구서에 hello 계획을 식별 하는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="d7df6-126">Hello 중 하나를 선택 **월별 계획 계층**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="d7df6-127">참고 hello 계획 계층 기본 기본 지역 및 웹 서비스에 대 한 toohello 계획 하는 배포 된 toothat 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="d7df6-128">클릭 **배포** 웹 서비스에 대 한 hello 빠른 시작 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="d7df6-129">빠른 시작 페이지</span><span class="sxs-lookup"><span data-stu-id="d7df6-129">Quickstart page</span></span>
<span data-ttu-id="d7df6-130">hello 웹 서비스 빠른 시작 페이지 하면 액세스 및 지침 hello 새 웹 서비스를 만든 후 수행할 수는 가장 일반적인 작업에.</span><span class="sxs-lookup"><span data-stu-id="d7df6-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="d7df6-131">여기에서 쉽게 액세스할 수 있습니다 두 hello **테스트** 페이지 및 **사용** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d7df6-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="d7df6-132">웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="d7df6-132">Testing your web service</span></span>
<span data-ttu-id="d7df6-133">Hello 빠른 시작 페이지에서 일반적인 작업에서 테스트 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="d7df6-134">tootest hello 웹 서비스 요청 응답 서비스 (RR)로:</span><span class="sxs-lookup"><span data-stu-id="d7df6-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="d7df6-135">클릭 **테스트** hello 메뉴 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="d7df6-136">**요청-응답**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="d7df6-137">Hello 실험의 입력된 열에 대 한 적절 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="d7df6-138">**요청-응답**테스트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="d7df6-139">결과 있습니다 hello의 오른쪽 hello 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="d7df6-140">일괄 처리 실행 서비스 (BES) 웹 서비스 tootest CSV 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="d7df6-141">클릭 **테스트** hello 메뉴 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="d7df6-142">**배치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-142">Click **Batch**.</span></span>
* <span data-ttu-id="d7df6-143">입력을 찾아보기를 클릭 하 고 tooyour 예제 데이터 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="d7df6-144">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-144">Click **Test**.</span></span>

<span data-ttu-id="d7df6-145">테스트의 hello 상태 표시 됩니다 **테스트 일괄 처리 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="d7df6-146">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="d7df6-146">Consuming your Web Service</span></span>
<span data-ttu-id="d7df6-147">웹 서비스로 배포된 경우 Azure 기계 학습 실험에서는 광범위한 장치 및 플랫폼에서 사용할 수 있는 REST API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="d7df6-148">간단한 REST API를 받아들이고 JSON을 사용 하 여 응답 hello 형식의 메시지 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="d7df6-149">hello Azure 기계 학습 포털에서는 사용할 수 있는 코드에서 R, C#, 및 Python toocall hello 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="d7df6-150">Hello Consuming 페이지에서 다음을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="d7df6-151">hello API 키와 앱에서 웹 서비스 사용에 대 한 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="d7df6-152">Excel 및 웹 응용 프로그램 템플릿 tookick 소비 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="d7df6-153">샘플 코드에 C#, python 및 R tooget 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="d7df6-154">웹 서비스 사용에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7df6-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7df6-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7df6-155">Next Steps</span></span>
<span data-ttu-id="d7df6-156">웹 서비스 사용에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7df6-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="d7df6-157">어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="d7df6-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="d7df6-158">Azure 기계 학습 웹 서비스: 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="d7df6-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
