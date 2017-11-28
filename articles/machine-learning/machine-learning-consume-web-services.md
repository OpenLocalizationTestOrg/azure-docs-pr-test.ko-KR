---
title: "aaaHow tooconsume Azure 컴퓨터 학습 웹 서비스 | Microsoft Docs"
description: "기계 학습 서비스가 배포 된 후 실시간 요청-응답 서비스 또는 일괄 처리 실행 서비스 hello 사용할 수 있는 RESTFul 웹 서비스를 이용할 수 있습니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a><span data-ttu-id="57ddf-103">어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="57ddf-103">How tooconsume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="57ddf-104">웹 서비스로 Azure 기계 학습 예측 모델을 배포를 사용 하 여 REST API toosend 것 데이터 및 get 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API toosend it data and get predictions.</span></span> <span data-ttu-id="57ddf-105">실시간으로 또는 일괄 처리 모드로 hello 데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-105">You can send hello data in real-time or in batch mode.</span></span>

<span data-ttu-id="57ddf-106">방법에 대 한 자세한 정보를 찾을 수 toocreate 여기 기계 학습 스튜디오를 사용 하 여 컴퓨터 학습 웹 서비스 및 배포:</span><span class="sxs-lookup"><span data-stu-id="57ddf-106">You can find more information about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="57ddf-107">기계 학습 스튜디오에서 실험 참조 하는 toocreate 방법에 대 한 자습서 [첫 번째 실험 만들기](machine-learning-create-experiment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="57ddf-108">방법에 대 한 자세한 내용은 toodeploy 웹 서비스 참조 [컴퓨터 학습 웹 서비스를 배포](machine-learning-publish-a-machine-learning-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="57ddf-109">기계 학습에 대 한 자세한 내용은 일반적으로 hello 방문 [기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="57ddf-110">개요</span><span class="sxs-lookup"><span data-stu-id="57ddf-110">Overview</span></span>
<span data-ttu-id="57ddf-111">Hello Azure 컴퓨터 학습 웹 서비스와 외부 응용 프로그램은 실시간으로 기계 학습 워크플로 점수 매기기 모델와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="57ddf-112">컴퓨터 학습 웹 서비스 호출 tooan 외부 응용 프로그램 예측 결과 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="57ddf-113">컴퓨터 학습 웹 서비스 호출 toomake 예측을 배포할 때 생성 되는 API 키를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="57ddf-114">hello 컴퓨터 학습 웹 서비스 나머지 부분에서는 웹 프로그래밍 프로젝트에 대 한 인기 있는 아키텍처 선택권을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="57ddf-115">Azure 기계 학습에는 다음 두 가지 유형의 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="57ddf-116">서비스 요청-응답 (RR)-짧은 대기 시간, toohello 상태 비저장 모델을 만들고 배포한 hello 기계 학습 스튜디오에서에서 인터페이스를 제공 하는 확장성이 높은 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="57ddf-117">BES(일괄 처리 실행 서비스) – 데이터 레코드의 점수를 일괄적으로 매기는 비동기 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="57ddf-118">Machine Learning 웹 서비스에 대한 자세한 내용은 [Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57ddf-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="57ddf-119">Azure 기계 학습 권한 부여 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="57ddf-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="57ddf-120">실험을 배포 하면 hello 웹 서비스에 대 한 API 키가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="57ddf-121">여러 위치에서 hello 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="57ddf-122">Hello Microsoft Azure 컴퓨터 학습 웹 서비스 포털에서</span><span class="sxs-lookup"><span data-stu-id="57ddf-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="57ddf-123">Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net) 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="57ddf-124">새 컴퓨터 학습 웹 서비스에 대 한 tooretrieve hello API 키:</span><span class="sxs-lookup"><span data-stu-id="57ddf-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="57ddf-125">Hello Azure 컴퓨터 학습 웹 서비스 포털에서 클릭 **웹 서비스** hello 상단 메뉴.</span><span class="sxs-lookup"><span data-stu-id="57ddf-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="57ddf-126">Tooretrieve hello 키 원하는 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="57ddf-127">Hello 상단 메뉴에서 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="57ddf-128">복사 하 고 hello 저장 **기본 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="57ddf-129">클래식 컴퓨터 학습 웹 서비스에 대 한 tooretrieve hello API 키:</span><span class="sxs-lookup"><span data-stu-id="57ddf-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="57ddf-130">Hello Azure 컴퓨터 학습 웹 서비스 포털에서 클릭 **웹 서비스를 클래식** hello 상단 메뉴.</span><span class="sxs-lookup"><span data-stu-id="57ddf-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="57ddf-131">작업 중인 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="57ddf-132">Tooretrieve hello 키 원하는 hello 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="57ddf-133">Hello 상단 메뉴에서 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="57ddf-134">복사 하 고 hello 저장 **기본 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="57ddf-135">기존 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="57ddf-135">Classic Web service</span></span>
 <span data-ttu-id="57ddf-136">기계 학습 스튜디오 또는 hello Azure 클래식 포털에서 기존 웹 서비스에 대 한 키를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="57ddf-137">Machine Learning 스튜디오</span><span class="sxs-lookup"><span data-stu-id="57ddf-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="57ddf-138">기계 학습 스튜디오에서 클릭 **웹 서비스** hello 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="57ddf-139">웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-139">Click a Web service.</span></span> <span data-ttu-id="57ddf-140">hello **API 키** hello에 **대시보드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="57ddf-141">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="57ddf-141">Azure classic portal</span></span>
1. <span data-ttu-id="57ddf-142">클릭 **기계 학습** hello 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="57ddf-143">웹 서비스의 위치를 가리키는 hello 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="57ddf-144">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="57ddf-145">웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-145">Click a Web service.</span></span>
5. <span data-ttu-id="57ddf-146">끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-146">Click an endpoint.</span></span> <span data-ttu-id="57ddf-147">hello "API 키" hello 오른쪽 아래에서 다운 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="57ddf-148"><a id="connect"></a>Tooa 컴퓨터 학습 웹 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="57ddf-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="57ddf-149">Tooa HTTP 요청 및 응답을 지 원하는 모든 프로그래밍 언어를 사용 하 여 컴퓨터 학습 웹 서비스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="57ddf-150">Machine Learning 웹 서비스 도움말 페이지에서 C#, Python 및 R로 작성된 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="57ddf-151">**Machine Learning API 도움말** 웹 서비스를 배포하면 Machine Learning API 도움말이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="57ddf-152">[Azure 기계 학습 연습 - 웹 서비스 배포](machine-learning-walkthrough-5-publish-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57ddf-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="57ddf-153">hello 컴퓨터 학습 API 도움말 예측 웹 서비스에 대 한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="57ddf-154">작업 중인 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="57ddf-155">Hello 끝점 원하는 tooview hello API 도움말 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="57ddf-156">Hello 상단 메뉴에서 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="57ddf-157">클릭 **API 도움말 페이지** hello 요청-응답 또는 일괄 처리 실행 끝점 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="57ddf-158">**새 웹 서비스에 대 한 tooview 컴퓨터 학습 API 도움말**</span><span class="sxs-lookup"><span data-stu-id="57ddf-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="57ddf-159">hello Azure 컴퓨터 학습 웹 서비스 포털:</span><span class="sxs-lookup"><span data-stu-id="57ddf-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="57ddf-160">클릭 **웹 서비스** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="57ddf-161">Tooretrieve hello 키 원하는 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="57ddf-162">클릭 **사용** tooget 요청 Reposonse hello 및 C#, R, 및 Python에서 일괄 처리 실행 서비스 및 샘플 코드에 대 한 Uri를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="57ddf-163">클릭 **Swagger API** tooget hello에서 호출 Api hello에 대 한 설명서를 기반으로 하는 Swagger Uri를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="57ddf-164">C# 샘플</span><span class="sxs-lookup"><span data-stu-id="57ddf-164">C# Sample</span></span>
<span data-ttu-id="57ddf-165">tooconnect tooa 컴퓨터 학습 웹 서비스를 사용 하 여 프로그램 **HttpClient** ScoreData 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="57ddf-166">ScoreData FeatureVector를 숫자 기능 ScoreData hello를 나타내는 경우 n 차원 벡터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="57ddf-167">API 키를 가진 toohello 기계 학습 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="57ddf-168">tooconnect tooa 컴퓨터 학습 웹 서비스 hello **Microsoft.AspNet.WebApi.Client** NuGet 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="57ddf-169">**Visual Studio에서 Microsoft.AspNet.WebApi.Client NuGet 설치**</span><span class="sxs-lookup"><span data-stu-id="57ddf-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="57ddf-170">UCI에서 hello 다운로드 데이터 집합 게시: 성인 2 클래스 dataset 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="57ddf-171">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="57ddf-172">**Install-Package Microsoft.AspNet.WebApi.Client**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="57ddf-173">**toorun hello 코드 샘플**</span><span class="sxs-lookup"><span data-stu-id="57ddf-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="57ddf-174">게시 "예제 1: UCI에서 데이터 집합 다운로드: 성인 2 클래스의 데이터 집합" 실험, hello 기계 학습 예제 컬렉션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="57ddf-175">웹 서비스에서 hello 키를 가진 apiKey를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="57ddf-176">위의 **Azure 기계 학습 권한 부여 키 가져오기** 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57ddf-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="57ddf-177">ServiceUri hello 요청 URI로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="57ddf-178">Python 샘플</span><span class="sxs-lookup"><span data-stu-id="57ddf-178">Python Sample</span></span>
<span data-ttu-id="57ddf-179">tooconnect tooa 컴퓨터 학습 웹 서비스를 사용 하 여 hello **urllib2** 라이브러리 ScoreData 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="57ddf-180">ScoreData FeatureVector를 숫자 기능 ScoreData hello를 나타내는 경우 n 차원 벡터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="57ddf-181">API 키를 가진 toohello 기계 학습 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="57ddf-182">**toorun hello 코드 샘플**</span><span class="sxs-lookup"><span data-stu-id="57ddf-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="57ddf-183">배포 "예제 1: UCI에서 데이터 집합 다운로드: 성인 2 클래스의 데이터 집합" 실험, hello 기계 학습 예제 컬렉션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="57ddf-184">웹 서비스에서 hello 키를 가진 apiKey를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="57ddf-185">Hello 참조 **Azure 기계 학습 권한 부여 키 가져오기** hello 시작 부분 근처이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="57ddf-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="57ddf-186">ServiceUri hello 요청 URI로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ddf-186">Assign serviceUri with hello Request URI.</span></span>

