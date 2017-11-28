---
title: "클래식 웹 서비스 재학습 | Microsoft Docs"
description: "Azure 기계 학습에서 프로그래밍 방식으로 모델을 다시 학습하고 새로 학습된 모델을 사용하도록 웹 서비스를 업데이트하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="8aeea-103">기존 웹 서비스 재학습</span><span class="sxs-lookup"><span data-stu-id="8aeea-103">Retrain a Classic web service</span></span>
<span data-ttu-id="8aeea-104">배포한 예측 웹 서비스는 기본 점수 매기기 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="8aeea-105">기본 끝점은 원래 학습 및 점수 매기기 실험과 동기화 상태를 유지하므로 기본 끝점에 대한 학습된 모델을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="8aeea-106">웹 서비스를 다시 학습하려면 웹 서비스에 새 끝점을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8aeea-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8aeea-107">Prerequisites</span></span>
<span data-ttu-id="8aeea-108">학습 실험 및 예측 실험을 [프로그래밍 방식으로 Machine Learning 모델 재학습](machine-learning-retrain-models-programmatically.md)에서 보듯이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8aeea-109">예측 실험을 기존 Machine Learning 웹 서비스로 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="8aeea-110">웹 서비스 배포에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8aeea-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="8aeea-111">새 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="8aeea-111">Add a new Endpoint</span></span>
<span data-ttu-id="8aeea-112">배포한 예측 웹 서비스는 원래의 학습 및 점수 매기기 실험 학습된 모델과 동기화를 유지하는 기본 점수 매기기 끝점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="8aeea-113">새로 학습된 모델을 사용하여 웹 서비스를 업데이트하려면 새 점수 매기기 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="8aeea-114">학습된 모델과 함께 업데이트될 수 있는 예측 웹 서비스에서 새 점수 매기기 끝점을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="8aeea-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="8aeea-115">끝점을 학습 웹 서비스가 아닌 예측 웹 서비스에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="8aeea-116">학습 및 예측 웹 서비스를 모두 올바르게 배포한 경우 나열된 두 개의 별도 웹 서비스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="8aeea-117">예측 웹 서비스는 "[예측 exp.]"로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="8aeea-118">웹 서비스에 새로 끝점을 추가할 수 있는 세 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="8aeea-119">프로그래밍 방식</span><span class="sxs-lookup"><span data-stu-id="8aeea-119">Programmatically</span></span>
2. <span data-ttu-id="8aeea-120">Microsoft Azure 웹 서비스 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="8aeea-121">Azure 클래식 포털 사용</span><span class="sxs-lookup"><span data-stu-id="8aeea-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="8aeea-122">프로그래밍 방식으로 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="8aeea-123">이 [GitHub 리포지토리](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)에서 제공된 샘플 코드를 사용하여 점수 매기기 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="8aeea-124">Microsoft Azure 웹 서비스 포털을 사용하여 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="8aeea-125">Machine Learning Studio의 왼쪽 탐색 열에서 Web Services를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="8aeea-126">웹 서비스 대시보드 아래쪽에서 **끝점 관리 미리 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="8aeea-127">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-127">Click **Add**.</span></span>
4. <span data-ttu-id="8aeea-128">새 끝점에 대한 이름 및 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="8aeea-129">로깅 수준 및 예제 데이터 사용 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="8aeea-130">자세한 내용은 [Machine Learning 웹 서비스에 대해 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8aeea-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="8aeea-131">Azure 클래식 포털을 사용하여 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="8aeea-132">[기존 Azure Portal](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8aeea-133">왼쪽 메뉴에서 **기계 학습**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="8aeea-134">이름 아래에서 작업 영역을 클릭한 다음 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="8aeea-135">이름 아래에서 **Census Model[예측 exp.]**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="8aeea-136">페이지 맨 아래에 있는 **끝점 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="8aeea-137">끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8aeea-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="8aeea-138">추가된 끝점의 학습된 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="8aeea-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="8aeea-139">재학습 프로세스를 완료하려면 추가한 새 끝점의 학습된 모델을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="8aeea-140">기존 Azure Portal을 사용하여 새 끝점을 추가한 경우 포털에서 새 끝점의 이름을 클릭한 다음 **UpdateResource** 링크를 클릭하여 끝점의 모델을 업데이트하는 데 필요한 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="8aeea-141">샘플 코드를 사용하여 끝점을 추가한 경우 출력에서 *HelpLocationURL* 값으로 식별되는 도움말 URL의 위치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="8aeea-142">경로 URL을 검색하려면:</span><span class="sxs-lookup"><span data-stu-id="8aeea-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="8aeea-143">URL을 복사하여 브라우저에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="8aeea-144">업데이트 리소스 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="8aeea-145">PATCH 요청의 POST URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="8aeea-146">예:</span><span class="sxs-lookup"><span data-stu-id="8aeea-146">For example:</span></span>
   
     <span data-ttu-id="8aeea-147">패치 URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="8aeea-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="8aeea-148">이제 학습된 모델을 사용하여 이전에 만든 점수 매기기 끝점을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="8aeea-149">다음 샘플 코드는 *BaseLocation*, *RelativeLocation*, *SasBlobToken* 및 PATCH URL을 사용하여 끝점을 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="8aeea-150">호출에 대한 *apiKey* 및 *endpointUrl*은 끝점 대시보드에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="8aeea-151">*리소스*의 *Name* 매개 변수의 값은 예측 실험의 저장된 학습된 모델의 리소스 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="8aeea-152">리소스 이름을 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="8aeea-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="8aeea-153">[기존 Azure Portal](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8aeea-154">왼쪽 메뉴에서 **기계 학습**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="8aeea-155">이름 아래에서 작업 영역을 클릭한 다음 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="8aeea-156">이름 아래에서 **Census Model[예측 exp.]**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="8aeea-157">추가한 새 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="8aeea-158">끝점 대시보드에서 **업데이트 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="8aeea-159">웹 서비스에 대한 업데이트 리소스 API 설명서 페이지에서 **업데이트할 수 있는 리소스** 아래에 **리소스 이름**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="8aeea-160">끝점 업데이트를 완료하기 전에 SAS 토큰이 만료되는 경우 작업 ID로 GET을 수행하여 새 토큰을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="8aeea-161">코드가 성공적으로 실행된 경우 새 끝점은 다시 학습된 모델을 사용하여 약 30초 내에 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="8aeea-162">요약</span><span class="sxs-lookup"><span data-stu-id="8aeea-162">Summary</span></span>
<span data-ttu-id="8aeea-163">재학습 API를 사용하여 다음과 같은 시나리오를 활성화하는 예측 웹 서비스의 학습된 모델을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8aeea-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="8aeea-164">새 데이터를 사용하는 주기적 모델 재학습.</span><span class="sxs-lookup"><span data-stu-id="8aeea-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="8aeea-165">자신의 데이터를 사용하여 모델을 다시 학습할 수 있도록 하는 것을 목표로 고객에게 모델 배포.</span><span class="sxs-lookup"><span data-stu-id="8aeea-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8aeea-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8aeea-166">Next steps</span></span>
[<span data-ttu-id="8aeea-167">Azure 기계 학습 기존 웹 서비스의 재학습 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8aeea-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

