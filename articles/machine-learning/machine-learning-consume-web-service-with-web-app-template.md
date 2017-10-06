---
title: "웹 응용 프로그램 템플릿 사용 하 여 기계 학습 웹 서비스 aaaConsume | Microsoft Docs"
description: "Azure 마켓플레이스 tooconsume Azure 기계 학습에서 예측 웹 서비스에서에서 웹 응용 프로그램 템플릿을 사용 합니다."
keywords: "웹 서비스, 운영, REST API, 기계 학습"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="caf84-104">웹 앱 템플릿을 사용한 Azure 기계 학습 웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="caf84-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="caf84-105">한 번 개발 모델에 예측 하 고 기계 학습 스튜디오를 사용 하 여 Azure 웹 서비스로 배포 또는 Python 또는 R 등의 도구를 사용 하는 REST API를 사용 하 여 hello 가능한 모델 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="caf84-106">Tooconsume hello REST API 및 액세스 hello 웹 서비스는 다양 한 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="caf84-107">예를 들어 C#에서 R을 응용 프로그램을 작성 또는 hello를 사용 하 여 Python 샘플 hello 웹 서비스를 배포할 때 자동으로 생성 된 코드 (hello에서 사용할 수 있는 [컴퓨터 학습 웹 서비스 포털](https://services.azureml.net/quickstart) 또는에서 hello 웹 서비스 대시보드 기계 학습 스튜디오)입니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="caf84-108">Hello 샘플 Microsoft Excel 통합 문서를 hello로 생성을 사용할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="caf84-109">웹 서비스는 hello에서 사용할 수 있는 hello 웹 응용 프로그램 템플릿을 통해 쉽고 빠르게 tooaccess hello 하지만 [Azure 웹 앱 마켓플레이스](https://azure.microsoft.com/marketplace/web-applications/all/)합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="caf84-110">hello Azure 컴퓨터 학습 웹 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="caf84-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="caf84-111">hello 웹 응용 프로그램 템플릿 hello Azure Marketplace에서에서 사용할 수 있는 웹 서비스의 입력된 데이터 및 예상된 결과 알고 있는 사용자 지정 웹 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="caf84-112">하기만 하면 toodo는 hello 웹 응용 프로그램 액세스 tooyour 웹 서비스 및 데이터를 제공할 및 hello 템플릿 rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="caf84-113">두 가지 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-113">Two templates are available:</span></span>

* [<span data-ttu-id="caf84-114">Azure ML 요청-응답 서비스 웹 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="caf84-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="caf84-115">Azure ML 일괄 처리 실행 서비스 웹 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="caf84-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="caf84-116">각 템플릿은 웹 서비스에 대 한 hello API URI 및 키를 사용 하 여 샘플 ASP.NET 응용 프로그램을 만들고 웹 사이트 tooAzure로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="caf84-117">hello 요청 응답 서비스 (RR) 템플릿은 toosend 데이터 toohello 웹 서비스 tooget 단일 결과의 단일 행을 허용 하는 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="caf84-118">hello 일괄 처리 실행 서비스 (BES) 템플릿은 만듭니다 toosend 수 있는 웹 응용 프로그램 데이터 tooget 무수히 많은 행 여러 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="caf84-119">코딩이 필요 toouse 이러한 서식 파일은 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="caf84-120">Hello API 키와 URI를 입력 하 고 hello 템플릿 hello 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="caf84-121">tooget hello API 키와 웹 서비스에 대 한 요청 URI:</span><span class="sxs-lookup"><span data-stu-id="caf84-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="caf84-122">Hello에 [웹 서비스 포털](https://services.azureml.net/quickstart), 새 웹 서비스에 대 한 클릭 **웹 서비스** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="caf84-123">또는 기존 웹 서비스의 경우 **기존 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="caf84-124">Tooaccess 사용할 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="caf84-125">기본 웹 서비스에 대 한 tooaccess hello 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="caf84-126">클릭 **사용** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="caf84-127">복사 hello **기본** 또는 **보조 키** 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="caf84-128">요청 응답 서비스 (RR) 템플릿을 만드는 경우 복사 hello **요청-응답** URI 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="caf84-129">일괄 처리 실행 서비스 (BES) 템플릿을 만드는 경우 복사 hello **일괄 처리 요청** URI 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="caf84-130">어떻게 toouse hello 서식 파일 요청 응답 서비스 (RR)</span><span class="sxs-lookup"><span data-stu-id="caf84-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="caf84-131">Hello 다음 다이어그램에에서 표시 된 대로 이러한 단계 toouse hello RR 웹 응용 프로그램 템플릿을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![프로세스 toouse RR 웹 서식 파일][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="caf84-133">Toohello 이동 [Azure 포털](https://portal.azure.com), **로그인**, 클릭 **새로**검색 하 고 선택 **Azure ML 요청 응답 서비스 웹 앱**, 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="caf84-134">웹 앱에 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-134">Give your web app a unique name.</span></span> <span data-ttu-id="caf84-135">hello 웹 응용 프로그램의 hello URL이이 이름 뒤 됩니다 `.azurewebsites.net.` 예를 들어`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="caf84-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="caf84-136">웹 서비스가 실행 되 고 있는 hello Azure 구독 및 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="caf84-137">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-137">Click **Create**.</span></span>
     
     ![웹앱 만들기][image5]

4. <span data-ttu-id="caf84-139">Azure hello 웹 응용 프로그램 배포 완료 되 면 클릭 hello **URL** hello azure에서 웹 응용 프로그램 설정 페이지 또는 웹 브라우저에서 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="caf84-140">예를 들어 `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="caf84-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="caf84-141">웹 앱 첫 번째 실행 것을 요청 hello에 대 한 경우 hello **API 게시 URL** 및 **API 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="caf84-142">이전에 저장 하는 hello 값을 입력 (**요청 URI** 및 **API 키**각각).</span><span class="sxs-lookup"><span data-stu-id="caf84-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="caf84-143">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-143">Click **Submit**.</span></span>
     
     ![Post URI 및 API 키 입력][image6]

6. <span data-ttu-id="caf84-145">웹 응용 프로그램 표시 hello 해당 **웹 응용 프로그램 구성** hello 현재 웹 서비스 설정으로 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="caf84-146">여기 toohello 설정을 hello 웹 응용 프로그램에서 사용 하는 변경 내용을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="caf84-147">여기에서 hello 설정을 변경에이 웹 응용 프로그램에만 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="caf84-148">웹 서비스의 기본 설정을 hello 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="caf84-149">예를 들어, hello를 변경 하는 경우 **설명** 여기 기계 학습 스튜디오에서 hello 웹 서비스 대시보드에 표시 되는 hello 설명 변경 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="caf84-150">완료 되 면 클릭 **ब ा ळ**, 클릭 하 고 **tooHome 페이지 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="caf84-151">Hello에서 홈 페이지를 입력할 수 있는 값은 toosend tooyour 웹 서비스.</span><span class="sxs-lookup"><span data-stu-id="caf84-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="caf84-152">클릭 **전송** 때 완료 되 고 hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="caf84-153">Tooreturn toohello 하려는 경우 **구성** 페이지에서 이동 toohello `setting.aspx` hello 웹 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="caf84-154">예를 들어: `http://carprediction.azurewebsites.net/setting.aspx.` 다시 증명된 tooenter hello API 키가 될-tooaccess 페이지 hello 및 hello 설정을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="caf84-155">중지, 다시 시작 하거나 hello 다른 웹 앱 처럼 Azure 포털의에서 웹 앱 hello를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="caf84-156">실행 중인 상태로 toohello 홈 웹 주소 찾아 새 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="caf84-157">Toouse 일괄 처리 실행 서비스 (BES) 템플릿 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="caf84-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="caf84-158">Hello BES를 사용할 수 있습니다 hello hello RR 템플릿으로 방식으로 제외 하 고 동일한 만들어진 해당 hello 웹 앱에에서 웹 응용 프로그램 템플릿을 사용 하면 toosubmit 여러 데이터 행을 여러 결과 수신 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="caf84-159">일괄 처리 실행 웹 서비스에 대 한 입력된 값 hello; 로컬 파일 또는 Azure 저장소에서 가져올 수 있습니다. hello 결과 Azure 저장소 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="caf84-160">따라서 살펴볼 필요한 Azure 저장소 컨테이너 toohold hello hello 웹 응용 프로그램에서 반환 된 결과 및 해야 tooget 입력된 데이터 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Toouse BES 처리 웹 서식 파일][image2]

1. <span data-ttu-id="caf84-162">다음과 같은 hello 프로시저 toocreate hello BES 웹 앱 go 제외 하 고 hello RR 서식 파일의 경우와 너무[Azure ML 일괄 처리 실행 서비스 웹 응용 프로그램 템플릿](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Azure 마켓플레이스에서 BES 템플릿을 hello 및 클릭 **웹 앱 만들기** .</span><span class="sxs-lookup"><span data-stu-id="caf84-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="caf84-163">hello 결과 저장 하 고, 원하는 toospecify hello 웹 응용 프로그램 홈 페이지에 hello 대상 컨테이너 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="caf84-164">또한 웹 응용 프로그램 hello hello 입력된 값을 로컬 파일 또는 Azure 저장소 컨테이너에는 어디서 얻을 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="caf84-165">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-165">Click **Submit**.</span></span>
   
    ![저장소 정보][image7]

<span data-ttu-id="caf84-167">hello 웹 응용 프로그램의 작업 상태 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="caf84-168">Hello 작업이 완료 되 면 Azure blob 저장소에 hello 결과의 hello 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="caf84-169">Hello hello 결과 tooa 로컬 파일을 다운로드할 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf84-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="caf84-170">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="caf84-170">For more information</span></span>
<span data-ttu-id="caf84-171">에 대 한 자세한 toolearn 중...</span><span class="sxs-lookup"><span data-stu-id="caf84-171">toolearn more about...</span></span>

* <span data-ttu-id="caf84-172">기계 학습 스튜디오로 기계 학습 실험 만들기는 [Azure 기계 학습 스튜디오에서 첫 번째 실험 만들기](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="caf84-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="caf84-173">기계 학습 웹 서비스 실험 toodeploy 참조 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="caf84-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="caf84-174">다른 방법으로 tooaccess 웹 서비스 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="caf84-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
