---
title: "aaa(deprecated) 연쇄 선형 회귀-Azure | Microsoft Docs"
description: "(사용 되지 않음) 다변량 선형 회귀"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="95fb0-103">(사용 되지 않음) 다변량 선형 회귀</span><span class="sxs-lookup"><span data-stu-id="95fb0-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="95fb0-104">hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며</span><span class="sxs-lookup"><span data-stu-id="95fb0-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="95fb0-105">Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="95fb0-106">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="95fb0-107">데이터 집합이 있어야 하 고 예측 tooquickly 같은 종속 변수 (y) 독립 변수에 따라 각 개인 (i)에 대 한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="95fb0-108">선형 회귀는 이러한 예측에 사용되는 널리 사용되는 통계 기법입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="95fb0-109">여기 hello 종속 변수에 y toobe 연속 값으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="95fb0-110">간단한 시나리오는 hello 연구원 toopredict hello 가중치는 높이 (x)에 따라 개인 (y)를 시도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="95fb0-111">좀 더 고급 시나리오에는 여기서 hello 연구원 (예: weight, 성별, 경쟁) 개별 hello에 대 한 정보를 추가 하 고 hello 개별 toopredict hello 가중치를 시도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="95fb0-112">이 [웹 서비스](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) 알맞은 hello 선형 회귀 모델 toohello 데이터 및 출력의 hello 데이터 hello 관측 각각에 대해 예측 된 값 (y) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="95fb0-113">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="95fb0-114">하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="95fb0-115">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="95fb0-116">hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="95fb0-117">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="95fb0-117">Consumption of web service</span></span>
<span data-ttu-id="95fb0-118">이 웹 서비스 제공 hello 모든 hello 관측 치에 대 한 hello 독립 변수를 기반으로 hello 종속 변수의 값을 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="95fb0-119">여기서 행은 쉼표 (,)로 구분 되 고 열은 세미콜론 (;)으로 구분 문자열 hello 최종 사용자 tooinput 데이터를 필요로 하는 hello 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="95fb0-120">한 번에 1 개 행을 요구 하 고 hello 첫 번째 열 toobe hello 종속 변수를 예상 하는 hello 웹 서비스.</span><span class="sxs-lookup"><span data-stu-id="95fb0-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="95fb0-121">예제 데이터 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-121">An example dataset could look like this:</span></span>

![샘플 데이터][1]

<span data-ttu-id="95fb0-123">종속 변수가 없는 관찰은 y에 대해 “NA”로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="95fb0-124">hello 데이터 입력 데이터 집합 위에 hello에 대 한는 hello 다음과 같은 사용 될 문자열: "10; 5; 2,18, 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, NA, 3, 4"입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="95fb0-125">hello는 hello 각 hello 행에 대 한 예측된 값에 따라 hello 독립 변수를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="95fb0-126">이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="95fb0-127">여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="95fb0-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="95fb0-128">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="95fb0-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="95fb0-129">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="95fb0-129">Creation of web service</span></span>
> <span data-ttu-id="95fb0-130">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="95fb0-131">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95fb0-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="95fb0-132">다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="95fb0-133">Azure 기계 학습에서는 내에서 새로운 빈 실험을 만들 때와 그 두 [R 스크립트 실행] [ execute-r-script] 모듈 hello 작업 영역으로 끌어온 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="95fb0-134">이 웹 서비스에서는 기본 R 스크립트를 사용하여 Azure 기계 학습 실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="95fb0-135">2 부 toothis 실험는: 스키마 정의 및 학습 모델을 + 점수 매기기입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="95fb0-136">첫 번째 모듈 hello hello 입력된 데이터 집합, hello 첫 번째 변수는 hello 종속 가변적이 고 hello 나머지 변수는 별개의 예상 hello 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="95fb0-137">hello 두 번째 모듈 hello 입력된 데이터에 대 한 일반 선형 회귀 모델을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![실험 흐름][3]

#### <a name="module-1"></a><span data-ttu-id="95fb0-139">모듈 1:</span><span class="sxs-lookup"><span data-stu-id="95fb0-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="95fb0-140">스키마 정의</span><span class="sxs-lookup"><span data-stu-id="95fb0-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="95fb0-141">모듈 2:</span><span class="sxs-lookup"><span data-stu-id="95fb0-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="95fb0-142">LM 모델링</span><span class="sxs-lookup"><span data-stu-id="95fb0-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="95fb0-143">제한 사항</span><span class="sxs-lookup"><span data-stu-id="95fb0-143">Limitations</span></span>
<span data-ttu-id="95fb0-144">이는 다중 선형 회귀 웹 서비스의 매우 단순한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="95fb0-145">위의 hello 예제 코드에서 볼 수 있듯이 없음 오류 찾기는 구현 하 여 hello 서비스 가정 모든 항목은 연속 변수 (범주 기능이 없습니다 허용), hello 서비스 지 원하는 유일한 입력 숫자 값으로이 웹 hello 생성 hello 시 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="95fb0-146">또한 hello 서비스가 현재 처리 하는 제한 된 데이터 크기를 hello 웹 서비스의 요청/응답 특성 toohello 인해 호출과 hello 사실을 hello 모델은 되 고 적합 hello 웹 서비스를 호출할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="95fb0-147">FAQ</span><span class="sxs-lookup"><span data-stu-id="95fb0-147">FAQ</span></span>
<span data-ttu-id="95fb0-148">Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95fb0-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

