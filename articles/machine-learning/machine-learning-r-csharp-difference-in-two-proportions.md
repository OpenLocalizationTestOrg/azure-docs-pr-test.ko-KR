---
title: "aaa(deprecated) 비율 테스트-Azure에서에서 차이 | Microsoft Docs"
description: "(사용되지 않음) 비율 차이 테스트"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="5504b-103">(사용되지 않음) 비율 차이 테스트</span><span class="sxs-lookup"><span data-stu-id="5504b-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="5504b-104">hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며</span><span class="sxs-lookup"><span data-stu-id="5504b-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="5504b-105">Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5504b-106">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="5504b-107">두 비율이 통계적으로 다른가요?</span><span class="sxs-lookup"><span data-stu-id="5504b-107">Are two proportions statistically different?</span></span> <span data-ttu-id="5504b-108">사용자가 한 동영상에 더 높은 비율의 경우 두 toocompare 동영상 toodetermine '배치할 수' 때 가정 toohello 다른 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="5504b-109">큰 샘플에는 통계적으로 중요 한 차이가 hello 비율 0.50 및 0.51 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="5504b-110">작은 샘플에 있을 수 있습니다 하지 충분 한 데이터 toodetermine 이러한 비율 실제로 다른 경우.</span><span class="sxs-lookup"><span data-stu-id="5504b-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="5504b-111">이 [웹 서비스](https://datamarket.azure.com/dataset/aml_labs/prop_test) hello 성공 횟수 및 hello 평가판 hello 2 비교 그룹에 대 한 총 수의 사용자 입력에 따라 두 비율로 hello 차이의 가설 테스트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="5504b-112">한 가지 가능한 시나리오에서 알리는 hello 사용자 여부 hello 동영상 중 하나 실제로 '연결' 영화 등급에 따라 다른 hello 보다 더 자주 동영상 비교 앱 내에서이 웹 서비스에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="5504b-113">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="5504b-114">하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="5504b-115">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="5504b-116">hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="5504b-117">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="5504b-117">Consumption of web service</span></span>
<span data-ttu-id="5504b-118">이 서비스는 4개의 인수를 받아들여 비율의 가설 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="5504b-119">hello 입력된 인수는.</span><span class="sxs-lookup"><span data-stu-id="5504b-119">hello input arguments are:</span></span>

* <span data-ttu-id="5504b-120">Successes1 - 샘플 1의 성공 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="5504b-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="5504b-121">Successes2 - 샘플 2의 성공 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="5504b-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="5504b-122">Total1 - 샘플 1의 크기</span><span class="sxs-lookup"><span data-stu-id="5504b-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="5504b-123">Total2 - 샘플 2의 크기</span><span class="sxs-lookup"><span data-stu-id="5504b-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="5504b-124">hello 서비스의 hello 출력은 hello 가설의 hello 결과 hello chi-square 통계, df, p-값을 테스트 하 고 샘플 1/2 및 신뢰 경계 내에 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="5504b-125">이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="5504b-126">여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="5504b-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="5504b-127">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="5504b-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="5504b-128">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5504b-128">Creation of web service</span></span>
> <span data-ttu-id="5504b-129">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="5504b-130">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5504b-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="5504b-131">다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="5504b-132">Azure 기계 학습 내에서 두 개의 [R 스크립트 실행][execute-r-script] 모듈을 사용하여 새로운 빈 실험을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="5504b-133">첫 번째 모듈 hello hello 두 번째 모듈 R tooperform hello 가설 테스트 내에서 prop.test 명령 hello를 사용 하 여 2 비율에 대 한 hello 데이터 스키마 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="5504b-134">실험 흐름:</span><span class="sxs-lookup"><span data-stu-id="5504b-134">Experiment flow:</span></span>
![실험 흐름][2]

#### <a name="module-1"></a><span data-ttu-id="5504b-136">모듈 1:</span><span class="sxs-lookup"><span data-stu-id="5504b-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="5504b-137">모듈 2:</span><span class="sxs-lookup"><span data-stu-id="5504b-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="5504b-138">제한 사항</span><span class="sxs-lookup"><span data-stu-id="5504b-138">Limitations</span></span>
<span data-ttu-id="5504b-139">이 예제는 두 비율 간의 차이를 테스트하는 매우 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="5504b-140">위의 hello 예제 코드에서 볼 수 있듯이 없음 오류 찾기 구현 되 고 hello 서비스 모든 hello 변수는 연속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="5504b-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="5504b-141">FAQ</span></span>
<span data-ttu-id="5504b-142">Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5504b-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

