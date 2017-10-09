---
title: "기본 웹 서비스 aaaRetrain | Microsoft Docs"
description: "어떻게 tooprogrammatically 모델을 다시 학습 모델 및 업데이트 hello 웹 서비스 toouse hello 새로 학습 된 Azure 기계 학습에서에 대해 알아봅니다."
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
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="30792-103">기존 웹 서비스 재학습</span><span class="sxs-lookup"><span data-stu-id="30792-103">Retrain a Classic web service</span></span>
<span data-ttu-id="30792-104">hello 배포한 예측 웹 서비스는 hello 기본 점수 매기기 끝점용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="30792-105">기본 끝점은 계속 동기화 hello 원래 학습 및 테스트를 평가 하 고 따라서 hello hello 기본 끝점에 대 한 학습 된 모델을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="30792-106">tooretrain hello 웹 서비스를 새 끝점 toohello 웹 서비스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="30792-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30792-107">Prerequisites</span></span>
<span data-ttu-id="30792-108">학습 실험 및 예측 실험을 [프로그래밍 방식으로 Machine Learning 모델 재학습](machine-learning-retrain-models-programmatically.md)에서 보듯이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="30792-109">hello 예측 실험 클래식 기계 학습 웹 서비스도 배포 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="30792-110">웹 서비스 배포에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30792-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="30792-111">새 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="30792-111">Add a new Endpoint</span></span>
<span data-ttu-id="30792-112">hello 배포한 예측 웹 서비스에는 점수 매기기 끝점용 hello 원래 학습 및 점수 매기기 실험 학습 된 모델와 동기화 유지 되는 기본 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="30792-113">tooupdate 프로그램 웹 서비스 toowith 새 학습 된 모델 점수 매기기 새 끝점을 만들 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="30792-114">toocreate hello hello 학습 된 모델을 업데이트할 수 있는 예측 웹 서비스에 새 점수 매기기 끝점:</span><span class="sxs-lookup"><span data-stu-id="30792-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="30792-115">Hello 끝점 toohello 예측 웹 서비스, 하지 hello 학습 웹 서비스를 추가 하는 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="30792-116">학습 및 예측 웹 서비스를 모두 올바르게 배포한 경우 나열된 두 개의 별도 웹 서비스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30792-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="30792-117">hello 예측 웹 서비스 "[예측 내선 번호]"로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="30792-118">세 가지 방법으로 새 끝점 tooa 웹 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="30792-119">프로그래밍 방식</span><span class="sxs-lookup"><span data-stu-id="30792-119">Programmatically</span></span>
2. <span data-ttu-id="30792-120">Hello Microsoft Azure 웹 서비스 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="30792-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="30792-121">Hello Azure 클래식 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="30792-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="30792-122">프로그래밍 방식으로 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="30792-123">이 제공 된 hello 샘플 코드를 사용 하 여 점수 매기기 끝점을 추가할 수 있습니다 [github 리포지토리](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="30792-124">Hello Microsoft Azure 웹 서비스 포털 tooadd 끝점을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="30792-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="30792-125">기계 학습 스튜디오에서는 hello 왼쪽된 탐색 열 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="30792-126">Hello 웹 서비스 대시보드 hello 아래쪽 클릭 **관리 끝점 미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="30792-127">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-127">Click **Add**.</span></span>
4. <span data-ttu-id="30792-128">이름 및 hello 새 끝점에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="30792-129">Hello 로깅 수준 및 예제 데이터가 활성화 되어 있는지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="30792-130">자세한 내용은 [Machine Learning 웹 서비스에 대해 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30792-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="30792-131">Azure 클래식 포털 tooadd 끝점 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="30792-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="30792-132">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="30792-133">Hello 왼쪽된 메뉴에서 클릭 **기계 학습**합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="30792-134">이름 아래에서 작업 영역을 클릭한 다음 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="30792-135">이름 아래에서 **Census Model[예측 exp.]**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="30792-136">Hello hello 페이지의 아래쪽에 있는 클릭 **끝점 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="30792-137">끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30792-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="30792-138">업데이트 hello 끝점의 학습 된 모델 추가</span><span class="sxs-lookup"><span data-stu-id="30792-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="30792-139">toocomplete hello 재교육 프로세스를 사용자가 추가한 hello 새 끝점의 hello 학습 된 모델을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="30792-140">Hello 포털에서 hello 새 끝점의 이름을 클릭 다음 hello 수 hello 클래식 Azure 포털을 사용 하 여 hello 새 끝점을 추가한 경우 **UpdateResource** tooupdate hello 끝점의 모델 해야 tooget hello URL에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="30792-141">Hello 샘플 코드를 사용 하 여 hello 끝점을 추가한 경우 여기에 hello로 식별 되는 hello 도움말 URL의 위치 *HelpLocationURL* hello 출력에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30792-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="30792-142">tooretrieve hello 경로 URL:</span><span class="sxs-lookup"><span data-stu-id="30792-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="30792-143">복사 하 여 브라우저에 hello URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="30792-144">Hello 업데이트 리소스 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="30792-145">Hello hello PATCH 요청의 게시 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="30792-146">예:</span><span class="sxs-lookup"><span data-stu-id="30792-146">For example:</span></span>
   
     <span data-ttu-id="30792-147">패치 URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="30792-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="30792-148">이제 점수 매기기 끝점용 이전에 만든 hello 학습 된 모델 tooupdate hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="30792-149">표시 하는 샘플 코드 다음 hello toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, 및 패치 URL tooupdate hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="30792-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="30792-150">hello *apiKey* 및 hello *endpointUrl* 에 hello 호출 끝점 대시보드에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="30792-151">값의 hello hello *이름* 매개 변수에서 *리소스* 은 일치 hello hello의 리소스 이름은 학습 된 모델에에서 저장 hello 예측 실험 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="30792-152">tooget hello 리소스 이름:</span><span class="sxs-lookup"><span data-stu-id="30792-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="30792-153">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="30792-154">Hello 왼쪽된 메뉴에서 클릭 **기계 학습**합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="30792-155">이름 아래에서 작업 영역을 클릭한 다음 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="30792-156">이름 아래에서 **Census Model[예측 exp.]**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="30792-157">추가한 hello 새 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="30792-158">Hello 끝점 대시보드에서 **업데이트 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="30792-159">Hello hello hello 웹 서비스에 대 한 업데이트 리소스 API 설명서 페이지를 찾을 수 있습니다 **리소스 이름** 아래 **업데이트할 수 있는 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="30792-160">Hello 끝점을 업데이트를 완료 하기 전에 SAS 토큰에 만료 되 면 hello 작업 Id tooobtain 새로 토큰 상태로 GET을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="30792-161">Hello 코드 성공적으로 실행 하는 경우 새 끝점의 hello 약 30 초 내에 다시 학습 되도록 hello 모델을 사용 하 여 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="30792-162">요약</span><span class="sxs-lookup"><span data-stu-id="30792-162">Summary</span></span>
<span data-ttu-id="30792-163">Api 재교육 hello를 사용 하 여, 예측 웹 서비스와 같은 시나리오를 지원의 hello 학습 된 모델을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30792-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="30792-164">새 데이터를 사용하는 주기적 모델 재학습.</span><span class="sxs-lookup"><span data-stu-id="30792-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="30792-165">자신의 데이터를 사용 하 여 hello 모델을 보존 하기 위해 이러한의 hello 목표 모델 toocustomers의 분포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30792-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30792-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30792-166">Next steps</span></span>
[<span data-ttu-id="30792-167">Azure 기계 학습 클래식 웹 서비스의 hello 재교육 문제 해결</span><span class="sxs-lookup"><span data-stu-id="30792-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

