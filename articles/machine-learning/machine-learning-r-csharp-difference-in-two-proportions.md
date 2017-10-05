---
title: "(사용되지 않음) 비율 차이 테스트 - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="26311-103">(사용되지 않음) 비율 차이 테스트</span><span class="sxs-lookup"><span data-stu-id="26311-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="26311-104">Microsoft DataMarket은 종료되고 있는 중이며 이 API는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="26311-105">[Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com)에서 많은 유용한 예제 실험과 API를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="26311-106">갤러리에 대한 자세한 내용은 [Cortana Intelligence 갤러리의 리소스 공유 및 검색](machine-learning-gallery-how-to-use-contribute-publish.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26311-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="26311-107">두 비율이 통계적으로 다른가요?</span><span class="sxs-lookup"><span data-stu-id="26311-107">Are two proportions statistically different?</span></span> <span data-ttu-id="26311-108">사용자가 두 개의 동영상을 비교하여 한 동영상의 '좋아요' 비율이 다른 동영상에 비해 상당히 더 높은지 확인하려 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="26311-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="26311-109">큰 샘플을 사용할 경우 비율 0.50과 0.51 간에는 통계적으로 상당한 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="26311-110">작은 샘플을 사용할 경우 이러한 비율이 실제로 다른지를 확인하기 위한 데이터가 충분하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="26311-111">이 [웹 서비스](https://datamarket.azure.com/dataset/aml_labs/prop_test) 는 두 비교 그룹에 대한 성공 횟수와 총 시도 횟수의 사용자 입력을 기반으로 하여 두 비율 간의 차이에 대한 가설 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26311-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="26311-112">가능한 한 가지 시나리오에서, 동영상 비교 앱 내에서 이 웹 서비스를 호출하여 사용자에게 동영상 등급을 기반으로 하여 동영상 중 하나가 다른 동영상보다 실제로 '좋아요'를 더 자주 받았는지 여부를 알려줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="26311-113">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="26311-114">하지만 이 웹 서비스는 Azure 기계 학습을 사용하여 R 코드 기반의 웹 서비스를 만드는 방법을 보여 주는 예로 제공되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="26311-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="26311-115">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="26311-116">그런 다음 웹 서비스를 Azure 마켓플레이스에 게시하면 웹 서비스 작성자가 인프라를 설정하지 않고도 전 세계의 사용자와 장치에서 이러한 웹 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="26311-117">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="26311-117">Consumption of web service</span></span>
<span data-ttu-id="26311-118">이 서비스는 4개의 인수를 받아들여 비율의 가설 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26311-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="26311-119">입력 인수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-119">The input arguments are:</span></span>

* <span data-ttu-id="26311-120">Successes1 - 샘플 1의 성공 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="26311-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="26311-121">Successes2 - 샘플 2의 성공 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="26311-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="26311-122">Total1 - 샘플 1의 크기</span><span class="sxs-lookup"><span data-stu-id="26311-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="26311-123">Total2 - 샘플 2의 크기</span><span class="sxs-lookup"><span data-stu-id="26311-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="26311-124">이 서비스의 출력은 가설 테스트를 카이제곱 통계, df, p 값, 샘플-1/2의 비율 및 신뢰 구간 경계와 함께 사용한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="26311-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="26311-125">Azure 마켓플레이스에서 호스트되는 이 서비스는 OData 서비스이고 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="26311-126">다양한 자동화된 방식으로 서비스를 사용할 수 있습니다(예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="26311-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="26311-127">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="26311-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="26311-128">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="26311-128">Creation of web service</span></span>
> <span data-ttu-id="26311-129">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="26311-130">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26311-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="26311-131">다음은 웹 서비스를 만든 실험과 실험 내 각 모듈의 예제 코드의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="26311-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="26311-132">Azure 기계 학습 내에서 두 개의 [R 스크립트 실행][execute-r-script] 모듈을 사용하여 새로운 빈 실험을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="26311-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="26311-133">첫 번째 모듈에서는 데이터 스키마가 정의된 반면, 두 번째 모듈에서는 R 내에 prop.test 명령을 사용하여 두 비율에 대한 가설 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26311-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="26311-134">실험 흐름:</span><span class="sxs-lookup"><span data-stu-id="26311-134">Experiment flow:</span></span>
![실험 흐름][2]

#### <a name="module-1"></a><span data-ttu-id="26311-136">모듈 1:</span><span class="sxs-lookup"><span data-stu-id="26311-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="26311-137">모듈 2:</span><span class="sxs-lookup"><span data-stu-id="26311-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="26311-138">제한 사항</span><span class="sxs-lookup"><span data-stu-id="26311-138">Limitations</span></span>
<span data-ttu-id="26311-139">이 예제는 두 비율 간의 차이를 테스트하는 매우 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="26311-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="26311-140">위의 예제 코드에서 볼 수 있듯이 오류 catch가 구현되어 있지 않으며, 이 서비스에서는 모든 변수가 연속 변수라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="26311-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="26311-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="26311-141">FAQ</span></span>
<span data-ttu-id="26311-142">웹 서비스 사용 또는 Azure 마켓플레이스 게시 방법과 관련한 질문과 대답은 [여기](machine-learning-marketplace-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26311-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

