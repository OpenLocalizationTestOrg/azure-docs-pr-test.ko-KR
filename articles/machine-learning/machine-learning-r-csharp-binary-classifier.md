---
title: "이진 분류자-aaa(deprecated) Azure | Microsoft Docs"
description: "(사용되지 않음) 이진 분류자"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="2901d-103">(사용되지 않음) 이진 분류자</span><span class="sxs-lookup"><span data-stu-id="2901d-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="2901d-104">hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며</span><span class="sxs-lookup"><span data-stu-id="2901d-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2901d-105">Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2901d-106">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2901d-107">데이터 집합이 있어야 하 고 원하는 toopredict hello 독립 변수에 따라 이진 종속 변수를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="2901d-108">'로지스틱 회귀 분석'은 이러한 예측에 널리 사용되는 통계 기법입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="2901d-109">여기 hello 종속 변수는 이진 또는 이분법, 및 p 관심 있는 hello 특징의 존재 hello 가능성이 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2901d-110">간단한 시나리오는 연구원 잠재 학생 가능성이 tooaccept (고등학교, 패밀리 수입, 상주 상태 GPA 성별) 정보에 따라는 진입 제품 tooa 대학 인지 toopredict를 시도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="2901d-111">hello 예측 된 결과 hello 진입 제안을 수락 hello 잠재 학생의 hello 확률입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="2901d-112">이 [웹 서비스](https://datamarket.azure.com/dataset/aml_labs/log_regression) 알맞은 hello 로지스틱 회귀 모델 toohello 데이터 및 출력의 hello 데이터 hello 관측 각각에 대 한 확률 값 (y) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="2901d-113">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2901d-114">하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="2901d-115">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2901d-116">hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2901d-117">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="2901d-117">Consumption of web service</span></span>
<span data-ttu-id="2901d-118">이 웹 서비스 제공 hello 모든 hello 관측 치에 대 한 hello 독립 변수를 기반으로 hello 종속 변수의 값을 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="2901d-119">hello 웹 서비스에 있는 행은 쉼표 (,)로 구분 되 고 열이 세미콜론 (;)으로 구분 된 문자열로 hello 최종 사용자 tooinput 데이터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="2901d-120">한 번에 1 개 행을 요구 하 고 hello 첫 번째 열 toobe hello 종속 변수를 예상 하는 hello 웹 서비스.</span><span class="sxs-lookup"><span data-stu-id="2901d-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="2901d-121">예제 데이터 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-121">An example dataset could look like this:</span></span>

![샘플 데이터][1]

<span data-ttu-id="2901d-123">종속 변수가 없는 관찰은 y에 대해 “NA”로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="2901d-124">hello 데이터 입력 데이터 집합 위에 hello에 대 한는 hello 다음과 같은 사용 될 문자열: "1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2, 1, NA; 3; 4"입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="2901d-125">hello는 hello 각 hello 행에 대 한 예측된 값에 따라 hello 독립 변수를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="2901d-126">이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2901d-127">여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2901d-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2901d-128">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="2901d-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="2901d-129">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2901d-129">Creation of web service</span></span>
> <span data-ttu-id="2901d-130">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2901d-131">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2901d-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2901d-132">다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="2901d-133">Azure 기계 학습에서는 내에서 새로운 빈 실험을 만들 때와 그 두 [R 스크립트 실행] [ execute-r-script] 모듈 hello 작업 영역으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="2901d-134">이 웹 서비스에서는 기본 R 스크립트를 사용하여 Azure 기계 학습 실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="2901d-135">2 부 toothis 실험는: 스키마 정의 및 학습 모델을 + 점수 매기기입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="2901d-136">첫 번째 모듈 hello hello 입력된 데이터 집합, hello 첫 번째 변수는 hello 종속 가변적이 고 hello 나머지 변수는 별개의 예상 hello 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="2901d-137">hello 두 번째 모듈 hello 입력된 데이터에 대 한 일반 로지스틱 회귀 모델을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![실험 흐름][2]

#### <a name="module-1"></a><span data-ttu-id="2901d-139">모듈 1:</span><span class="sxs-lookup"><span data-stu-id="2901d-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="2901d-140">모듈 2:</span><span class="sxs-lookup"><span data-stu-id="2901d-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="2901d-141">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2901d-141">Limitations</span></span>
<span data-ttu-id="2901d-142">이 예제는 매우 간단한 이진 분류 웹 서비스 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="2901d-143">없음 오류 찾기 구현 하 고 위의 hello 예제 코드에서 볼 수 있듯이 고 hello 서비스 이진/연속 변수 (범주 기능이 없습니다 허용), 모든 항목은 hello 서비스 지 원하는 유일한 입력 숫자 값으로이 hello 생성 hello 시 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="2901d-144">또한 hello 서비스가 현재 처리 하는 제한 된 데이터 크기를 hello 웹 서비스의 요청/응답 특성 toohello 인해 호출과 hello 사실을 hello 모델은 되 고 적합 hello 웹 서비스를 호출할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="2901d-145">FAQ</span><span class="sxs-lookup"><span data-stu-id="2901d-145">FAQ</span></span>
<span data-ttu-id="2901d-146">Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2901d-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

