---
title: "웹앱 템플릿에서 Machine Learning 웹 서비스 사용 | Microsoft Docs"
description: "Azure Marketplace에서 웹 앱을 사용하여 Azure 기계 학습의 예측 웹 서비스를 사용합니다."
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
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="30860-104">웹 앱 템플릿을 사용한 Azure 기계 학습 웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="30860-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="30860-105">예측 모델을 개발하고 기계 학습 스튜디오를 사용하거나 R 또는 Python을 사용하여 Azure 웹으로 배포하면 REST API를 사용하여 운영할 수 있게 된 모델에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="30860-106">REST API를 사용하고 웹 서비스에 액세스하는 방법은 많습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="30860-107">예를 들어, 웹 서비스를 배포할 때 생성된 샘플 코드를 사용하여 C#, R 또는 Python에서 응용 프로그램을 작성할 수 있습니다([Machine Learning 웹 서비스 포털](https://services.azureml.net/quickstart) 또는 Machine Learning 스튜디오의 웹 서비스 대시보드에서 사용 가능).</span><span class="sxs-lookup"><span data-stu-id="30860-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="30860-108">또는 동시에 생성된 샘플 Microsoft Excel 통합 문서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="30860-109">그러나 웹 서비스를 액세스하는 가장 빠르고 쉬운 방법은 [Azure 웹 앱 마켓플레이스](https://azure.microsoft.com/marketplace/web-applications/all/)에서 사용 가능한 웹 앱 템플릿을 통한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30860-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="30860-110">Azure 기계 학습 웹 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="30860-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="30860-111">Azure Marketplace에서 사용할 수 있는 웹 앱 템플릿은 웹 서비스의 입력 데이터 및 예상 결과를 알고 있는 사용자 지정 웹 앱을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="30860-112">따라서 웹 앱이 웹 서비스 및 데이터에 액세스하도록 하기만 하면 나머지 작업은 템플릿이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="30860-113">두 가지 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-113">Two templates are available:</span></span>

* [<span data-ttu-id="30860-114">Azure ML 요청-응답 서비스 웹 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="30860-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="30860-115">Azure ML 일괄 처리 실행 서비스 웹 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="30860-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="30860-116">각 템플릿은 웹 서비스용 API URI 및 키를 사용하여 샘플 ASP.NET 응용 프로그램을 만들고 Azure에 웹 사이트에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="30860-117">요청-응답 서비스(RRS) 템플릿은 단일 결과를 가져오기 위해 데이터의 단일 행을 웹 서비스에 보낼 수 있도록 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30860-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="30860-118">일괄 처리 실행 서비스(BES) 템플릿은 여러 결과를 가져오기 위해 많은 데이터의 행을 보낼 수 있도록 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30860-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="30860-119">이러한 템플릿을 사용하기 위해 코딩 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-119">No coding is required to use these templates.</span></span> <span data-ttu-id="30860-120">API 키 및 URI를 제공하면 템플릿이 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="30860-121">웹 서비스에 대한 API 키 및 요청 URI를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="30860-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="30860-122">[웹 서비스 포털](https://services.azureml.net/quickstart)에서 새 웹 서비스의 경우 위쪽의 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="30860-123">또는 기존 웹 서비스의 경우 **기존 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="30860-124">액세스하려는 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="30860-125">기존 웹 서비스의 경우 액세스하려는 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="30860-126">위쪽의 **소비자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="30860-127">**기본** 또는 **보조 키**를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="30860-128">RRS(요청-응답 서비스) 템플릿을 만드는 경우 **요청-응답** URI를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="30860-129">BES(일괄 처리 실행 서비스) 템플릿을 만드는 경우 **일괄 처리 요청** URI를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="30860-130">요청-응답 서비스(RRS) 템플릿을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="30860-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="30860-131">다음 다이어그램에 표시된 것처럼 이 단계를 따라 RRS 웹앱 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![RRS 웹 템플릿을 사용하는 프로세스][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="30860-133">[Azure Portal](https://portal.azure.com), **로그인**으로 이동하여 **새로 만들기**를 클릭하고 **Azure ML 요청-응답 서비스 웹앱**을 검색하고 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="30860-134">웹 앱에 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-134">Give your web app a unique name.</span></span> <span data-ttu-id="30860-135">웹앱의 URL이 이름 뒤에 됩니다 `.azurewebsites.net.` 예: `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="30860-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="30860-136">Azure 구독과 웹 서비스가 실행되는 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="30860-137">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-137">Click **Create**.</span></span>
     
     ![웹앱 만들기][image5]

4. <span data-ttu-id="30860-139">Azure가 웹앱 배포를 완료하면 Azure의 웹앱 설정 페이지의 **URL**을 클릭하거나 웹 브라우저에 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="30860-140">위치(예:`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="30860-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="30860-141">웹앱을 처음 실행할 때 **API 게시 URL** 및 **API 키**를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="30860-142">이전에 저장한 값을 입력합니다(**요청 URI** 및 **API 키** 각각).</span><span class="sxs-lookup"><span data-stu-id="30860-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="30860-143">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-143">Click **Submit**.</span></span>
     
     ![Post URI 및 API 키 입력][image6]

6. <span data-ttu-id="30860-145">웹앱은 현재 웹 서비스 설정과 함께 **웹앱 구성** 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="30860-146">여기서 웹 앱에서 사용되는 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="30860-147">여기서 설정을 변경하면 이 웹 앱에 대한 설정만 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="30860-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="30860-148">웹 서비스의 기본 설정을 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="30860-149">예를 들어, 여기에서 **설명**을 변경하면 기계 학습 스튜디오의 웹 서비스 대시보드에 표시되는 설명은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="30860-150">완료되면 **변경 내용 저장**을 클릭한 다음 **홈페이지로 이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="30860-151">홈 페이지에서 웹 서비스에 전송하는 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="30860-152">완료되면 **전송**을 클릭하고 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="30860-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="30860-153">**구성** 페이지로 반환하려는 경우, 웹앱의 `setting.aspx` 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="30860-154">예를 들어, `http://carprediction.azurewebsites.net/setting.aspx.` API 키를 다시 입력하라는 메시지가 표시됩니다. 이 키는 해당 페이지에 액세스하고 설정을 업데이트하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="30860-155">웹앱처럼 Azure 포털에서 웹앱을 중지하거나, 다시 시작하거나, 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="30860-156">실행되는 동안, 홈 웹 주소로 이동하여 새 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="30860-157">일괄 처리 실행 서비스(BES) 템플릿을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="30860-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="30860-158">만든 웹 앱을 통해 여러 데이터 행을 제출하고 여러 결과를 수신하는 것을 제외하고, RRS 템플릿과 동일한 방식으로 BES 웹 앱 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="30860-159">일괄 처리 실행 웹 서비스에 대한 입력 값은 Azure 저장소 또는 로컬 파일에서 가져올 수 있으며 결과는 Azure 저장소 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="30860-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="30860-160">따라서 웹 앱에 의해 반환된 결과를 저장할 Azure 저장소 컨테이너가 필요하고 입력된 데이터를 준비시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![BES 웹 템플릿을 사용하는 프로세스][image2]

1. <span data-ttu-id="30860-162">RRS 템플릿에 대한 것과 동일한 절차를 [Azure ML 일괄 처리 실행 서비스 웹앱 템플릿](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)으로 이동하여 Azure Marketplace의 BES 템플릿을 열고 **웹앱 만들기**를 클릭을 제외하고 수행하여 BES 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30860-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="30860-163">결과를 저장하려는 위치를 지정하려면 웹 앱 홈페이지에 대상 컨테이너 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="30860-164">또한 웹 앱이 로컬 파일 또는 Azure 저장소 컨테이너에 있는 입력 값을 가져올 수 있는 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="30860-165">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-165">Click **Submit**.</span></span>
   
    ![저장소 정보][image7]

<span data-ttu-id="30860-167">웹 앱은 작업 상태와 함께 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="30860-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="30860-168">작업이 완료되면 Azure Blob 저장소에서 결과의 위치를 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30860-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="30860-169">또한 결과를 로컬 파일에 다운로드할 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30860-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="30860-170">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="30860-170">For more information</span></span>
<span data-ttu-id="30860-171">다음에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="30860-171">To learn more about...</span></span>

* <span data-ttu-id="30860-172">기계 학습 스튜디오로 기계 학습 실험 만들기는 [Azure 기계 학습 스튜디오에서 첫 번째 실험 만들기](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="30860-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="30860-173">웹 서비스로서 기계 학습 실험을 배포하는 방법은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="30860-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="30860-174">웹 서비스에 액세스하는 다른 방법은 [Azure Machine Learning 웹 서비스](machine-learning-consume-web-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30860-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
