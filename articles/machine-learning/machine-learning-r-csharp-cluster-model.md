---
title: "클러스터 모델-aaa(deprecated) Azure | Microsoft Docs"
description: "(사용되지 않음) 클러스터 모델"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="28936-103">(사용되지 않음) 클러스터 모델</span><span class="sxs-lookup"><span data-stu-id="28936-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="28936-104">hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며</span><span class="sxs-lookup"><span data-stu-id="28936-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="28936-105">Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="28936-106">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="28936-107">그룹의 순서 tooreduce hello 충전 오프 위험을 신용 카드 발급자 신용 cardholders 동작을 예측할 수 있습니다 어떻게 우리?</span><span class="sxs-lookup"><span data-stu-id="28936-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="28936-108">수 정의 하는 직원의 개성 특성의 그룹 순서 tooimprove에 직장 성능을?</span><span class="sxs-lookup"><span data-stu-id="28936-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="28936-109">의사 들에 게는 어떻게 자신의 질병의 hello 특성에 따라 그룹으로 환자 분류할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="28936-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="28936-110">원칙적으로 클러스터 분석을 통해 이러한 모든 질문에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28936-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="28936-111">클러스터 분석에서는 변수 조합을 기반으로 하여 관찰 집합을 둘 이상의 상호 배타적인 알 수 없는 그룹으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="28936-112">hello 클러스터 분석의 목적은 toodiscover 관찰, 일반적으로 사람 또는 해당 특성 그룹으로 구성 하는 시스템 여기서 hello 그룹의 멤버 속성을 공유 공통입니다.</span><span class="sxs-lookup"><span data-stu-id="28936-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="28936-113">이 [서비스](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) 사용 하 여 hello K-means 방법은 방법, 자주 사용 되는 클러스터링 기술 toocluster 임의의 데이터를 그룹으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="28936-114">이 웹 서비스는 hello 데이터를 가져와 및 k hello 수를 입력으로 클러스터 및 각 관찰 속한 hello k 그룹 toowhich 중의 예측을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="28936-115">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28936-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="28936-116">하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="28936-117">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28936-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="28936-118">hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="28936-119">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="28936-119">Consumption of web service</span></span>
<span data-ttu-id="28936-120">이 웹 서비스의 각 행에 대 한 k 그룹 및 출력 hello 그룹 할당 집합으로 hello 데이터를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="28936-121">여기서 행은 쉼표 (,)로 구분 되 고 열은 세미콜론 (;)으로 구분 문자열 hello 최종 사용자 tooinput 데이터를 필요로 하는 hello 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="28936-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="28936-122">hello 웹 서비스에는 한 번에 1 개 행이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="28936-123">예제 데이터 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28936-123">An example dataset could look like this:</span></span>

![샘플 데이터][1]

<span data-ttu-id="28936-125">3 개의 상호 배타적인 그룹으로 hello 원하는 사용자 tooseparate이이 데이터를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="28936-126">데이터 입력을 데이터 집합 위에 hello hello 다음 hello: 값 = "10; 5; 2,18, 1; 6,7; 5; 5,22; 3; 4,12 않으면 2; 1,10; 3; 4"; k = "3"입니다.</span><span class="sxs-lookup"><span data-stu-id="28936-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="28936-127">hello 출력 각 hello 행에 대 한 예측된 그룹 구성원 자격을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28936-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="28936-128">이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28936-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="28936-129">여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="28936-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="28936-130">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="28936-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="28936-131">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="28936-131">Creation of web service</span></span>
> <span data-ttu-id="28936-132">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="28936-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="28936-133">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28936-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="28936-134">다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="28936-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="28936-135">Azure 기계 학습에서는 내에서 새로운 빈 실험을 만들 때와 그 두 [R 스크립트 실행] [ execute-r-script] 모듈 hello 작업 영역으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="28936-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="28936-136">hello 데이터 스키마가 생성 하는 간단한 [R 스크립트 실행][execute-r-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="28936-137">그런 다음 hello 데이터 스키마가 연결 된 toohello 모델 섹션을 사용 하 여 다시 만든 클러스터는 [R 스크립트 실행][execute-r-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="28936-138">Hello에 [R 스크립트 실행] [ execute-r-script] hello 클러스터 모델의 사용, hello 웹 서비스가 다음 사용 "k 수단" hello 함수 hello에 미리 작성 된를 [R 스크립트 실행] [ execute-r-script] Azure 기계 학습의 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![실험 흐름][3]

#### <a name="module-1"></a><span data-ttu-id="28936-140">모듈 1:</span><span class="sxs-lookup"><span data-stu-id="28936-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="28936-141">모듈 2:</span><span class="sxs-lookup"><span data-stu-id="28936-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="28936-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="28936-142">Limitations</span></span>
<span data-ttu-id="28936-143">이 예제는 매우 간단한 클러스터링 웹 서비스 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="28936-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="28936-144">위의 hello 예제 코드에서 볼 수 있듯이 없음 오류 찾기는 구현 하 여 hello 서비스 가정 모든 항목은 연속 변수 (범주 기능이 없습니다 허용), hello 서비스 지 원하는 유일한 입력 숫자 값으로이 웹 hello 생성 hello 시 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="28936-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="28936-145">또한 hello 서비스가 현재 처리 하는 제한 된 데이터 크기를 hello 웹 서비스의 요청/응답 특성 toohello 인해 호출과 hello 사실을 hello 모델은 되 고 적합 hello 웹 서비스를 호출할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="28936-146">FAQ</span><span class="sxs-lookup"><span data-stu-id="28936-146">FAQ</span></span>
<span data-ttu-id="28936-147">Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28936-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

