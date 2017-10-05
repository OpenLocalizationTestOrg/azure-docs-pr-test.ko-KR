---
title: "Machine Learning 웹 서비스에 연결 | Microsoft Docs"
description: "C# 또는 Python을 사용하는 경우 권한 부여 키를 사용하여 Azure Machine Learning 웹 서비스에 연결합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="27678-103">Azure 기계 학습 웹 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="27678-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="27678-104">Azure Machine Learning 개발자 환경은 실시간 또는 일괄 처리 모드로 입력 데이터에서 예측하는 웹 서비스 API입니다.</span><span class="sxs-lookup"><span data-stu-id="27678-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="27678-105">Azure Machine Learning 스튜디오를 사용하여 예측을 만들고 Azure Machine Learning 웹 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="27678-106">Machine Learning 스튜디오를 사용하여 Machine Learning 웹 서비스를 만들고 배포하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="27678-107">기계 학습 스튜디오에서 실험을 만드는 방법에 대한 자습서는 [첫 번째 실험 만들기](machine-learning-create-experiment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="27678-108">웹 서비스를 배포하는 방법에 대한 자세한 내용은 [Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="27678-109">기계 학습에 대한 자세한 내용은 [기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="27678-110">Azure Machine Learning 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="27678-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="27678-111">Azure Machine Learning 웹 서비스를 통해 외부 응용 프로그램에서 Machine Learning 워크플로 점수 매기기 모델과 실시간으로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="27678-112">Machine Learning 웹 서비스 호출은 외부 응용 프로그램에 예측 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="27678-113">Machine Learning 웹 서비스를 호출하려면 예측을 배포할 때 만들어진 API 키를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="27678-114">Machine Learning 웹 서비스는 웹 프로그래밍 프로젝트에 일반적으로 사용되는 아키텍처인 REST를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="27678-115">Azure 기계 학습에는 다음 두 가지 유형의 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="27678-116">RRS(요청-응답 서비스) - 대기 시간이 짧고 확장성이 높은 서비스로, 기계 학습 스튜디오에서 생성 및 배포되는 상태 비저장 모델에 대한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="27678-117">BES(일괄 처리 실행 서비스) – 데이터 레코드의 점수를 일괄적으로 매기는 비동기 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="27678-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="27678-118">Machine Learning 웹 서비스에 대한 자세한 내용은 [Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="27678-119">Azure 기계 학습 권한 부여 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="27678-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="27678-120">실험을 배포할 때 웹 서비스에 API 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27678-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="27678-121">여러 위치에서 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="27678-122">Microsoft Azure Machine Learning 웹 서비스 포털에서</span><span class="sxs-lookup"><span data-stu-id="27678-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="27678-123">[Microsoft Azure Machine Learning 웹 서비스](https://services.azureml.net) 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="27678-124">새 Machine Learning 웹 서비스에 대한 API 키를 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="27678-125">Azure Machine Learning 웹 서비스 포털의 최상위 메뉴에서 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="27678-126">키를 검색하려는 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="27678-127">위쪽 메뉴에서 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="27678-128">**기본 키**를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="27678-129">클래식 Machine Learning 웹 서비스에 대한 API 키를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="27678-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="27678-130">Azure Machine Learning 웹 서비스 포털의 최상위 메뉴에서 **클래식 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="27678-131">사용하고 있는 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="27678-132">키를 검색하려는 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="27678-133">위쪽 메뉴에서 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="27678-134">**기본 키**를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="27678-135">기존 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="27678-135">Classic Web service</span></span>
 <span data-ttu-id="27678-136">Machine Learning 스튜디오 또는 Azure Classic Portal에서 클래식 웹 서비스에 대한 키를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="27678-137">Machine Learning 스튜디오</span><span class="sxs-lookup"><span data-stu-id="27678-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="27678-138">Machine Learning Studio의 왼쪽에서 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="27678-139">웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-139">Click a Web service.</span></span> <span data-ttu-id="27678-140">**API 키**는 **대시보드** 탭에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="27678-141">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="27678-141">Azure classic portal</span></span>
1. <span data-ttu-id="27678-142">왼쪽에서 **MACHINE LEARNING**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="27678-143">웹 서비스의 위치에 있는 작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="27678-144">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="27678-145">웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-145">Click a Web service.</span></span>
5. <span data-ttu-id="27678-146">끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-146">Click an endpoint.</span></span> <span data-ttu-id="27678-147">"API 키"는 오른쪽 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="27678-148"><a id="connect"></a>Machine Learning 웹 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="27678-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="27678-149">HTTP 요청 및 응답을 지원하는 모든 프로그래밍 언어를 사용하여 Machine Learning 웹 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="27678-150">Machine Learning 웹 서비스 도움말 페이지에서 C#, Python 및 R로 작성된 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="27678-151">**Machine Learning API 도움말** 웹 서비스를 배포하면 Machine Learning API 도움말이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27678-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="27678-152">[Azure 기계 학습 연습 - 웹 서비스 배포](machine-learning-walkthrough-5-publish-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="27678-153">Machine Learning API 도움말에는 예측 웹 서비스에 대한 세부 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27678-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="27678-154">사용하고 있는 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="27678-155">API 도움말 페이지를 보려는 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="27678-156">위쪽 메뉴에서 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="27678-157">응답 간 또는 Batch 실행 끝점에서 **API 도움말 페이지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="27678-158">**새 웹 서비스에 대한 Machine Learning API 도움말을 보려면**</span><span class="sxs-lookup"><span data-stu-id="27678-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="27678-159">Azure Machine Learning 웹 서비스 포털에서:</span><span class="sxs-lookup"><span data-stu-id="27678-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="27678-160">최상위 메뉴에서 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="27678-161">키를 검색하려는 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="27678-162">**사용**을 클릭하여 C#, R 및 Python으로 요청-응답 및 배치 실행 서비스와 샘플 코드에 대한 URI를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27678-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="27678-163">**Swagger API**를 클릭하여 제공된 URI에서 호출된 API에 대한 Swagger 기반 설명서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27678-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="27678-164">C# 샘플</span><span class="sxs-lookup"><span data-stu-id="27678-164">C# Sample</span></span>
<span data-ttu-id="27678-165">Machine Learning 웹 서비스에 연결하려면 ScoreData를 전달하는 **HttpClient**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="27678-166">ScoreData는 ScoreData를 나타내는 수치의 n 차원 벡터인 FeatureVector를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="27678-167">API 키로 기계 학습 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="27678-168">Machine Learning 웹 서비스에 연결하려면 **Microsoft.AspNet.WebApi.Client** NuGet 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="27678-169">**Visual Studio에서 Microsoft.AspNet.WebApi.Client NuGet 설치**</span><span class="sxs-lookup"><span data-stu-id="27678-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="27678-170">UCI: Adult 2 클래스 데이터 집합에서 데이터 집합 다운로드 웹 서비스를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="27678-171">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="27678-172">**Install-Package Microsoft.AspNet.WebApi.Client**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="27678-173">**코드 샘플을 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="27678-173">**To run the code sample**</span></span>

1. <span data-ttu-id="27678-174">기계 학습 샘플 컬렉션의 “샘플 1: UCI: Adult 2 클래스 데이터 집합에서 데이터 집합 다운로드” 실험 부분을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="27678-175">웹 서비스에서 가져온 키로 apiKey를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="27678-176">위의 **Azure 기계 학습 권한 부여 키 가져오기** 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="27678-177">요청 URI로 serviceUri를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="27678-178">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="27678-178">Python Sample</span></span>
<span data-ttu-id="27678-179">Machine Learning 웹 서비스에 연결하려면 ScoreData를 전달하는 **urllib2** 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="27678-180">ScoreData는 ScoreData를 나타내는 수치의 n 차원 벡터인 FeatureVector를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="27678-181">API 키로 기계 학습 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="27678-182">**코드 샘플을 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="27678-182">**To run the code sample**</span></span>

1. <span data-ttu-id="27678-183">기계 학습 샘플 컬렉션의 “샘플 1: UCI: Adult 2 클래스 데이터 집합에서 데이터 집합 다운로드” 실험 부분을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="27678-184">웹 서비스에서 가져온 키로 apiKey를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="27678-185">이 문서의 시작 부분 가까이에 있는 **Azure Machine Learning 권한 부여 키 가져오기** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27678-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="27678-186">요청 URI로 serviceUri를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27678-186">Assign serviceUri with the Request URI.</span></span>

