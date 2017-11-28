---
title: "aaa(deprecated) 정규 분포 웹 서비스 도구 모음-Azure | Microsoft Docs"
description: "(사용되지 않음) 정규 분포 웹 서비스 제품군"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="465ad-103">(사용되지 않음) 정규 분포 제품군</span><span class="sxs-lookup"><span data-stu-id="465ad-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="465ad-104">hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며</span><span class="sxs-lookup"><span data-stu-id="465ad-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="465ad-105">Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="465ad-106">Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="465ad-107">hello 정규 분포 Suite는 샘플 웹 서비스 집합 ([생성기](https://datamarket.azure.com/dataset/aml_labs/ndg7), [변 위치 계산기](https://datamarket.azure.com/dataset/aml_labs/ndq5), [확률 계산기](https://datamarket.azure.com/dataset/aml_labs/ndp5)) 생성 하 고 처리 하는 데 도움이 정규 분포입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="465ad-108">hello 서비스 길이, 변 위치에서 지정 된 확률을 계산 하 고 지정한 변 위치에서 확률을 계산 하는 정규 분포 시퀀스 생성을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="465ad-109">Hello 선택한 서비스에 따라 서로 다른 출력을 내보내는 각 hello 서비스 (아래 설명 참조).</span><span class="sxs-lookup"><span data-stu-id="465ad-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="465ad-110">정규 분포 Suite hello R 통계 패키지에 포함 된 hello R 함수 qnorm, rnorm, 및 pnorm를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="465ad-111">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="465ad-112">하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="465ad-113">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="465ad-114">hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="465ad-115">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="465ad-115">Consumption of web service</span></span>
<span data-ttu-id="465ad-116">hello 정규 분포 제품군 3 서비스를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="465ad-117">정규 분포 분위수 계산기</span><span class="sxs-lookup"><span data-stu-id="465ad-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="465ad-118">이 서비스는 정규 분포의 4 개 인수를 수락 하 고 연결 된 hello 변 위치를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="465ad-119">hello 입력된 인수는.</span><span class="sxs-lookup"><span data-stu-id="465ad-119">hello input arguments are:</span></span>

* <span data-ttu-id="465ad-120">p - 정규 분포를 통한 이벤트의 단일 확률</span><span class="sxs-lookup"><span data-stu-id="465ad-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="465ad-121">평균-hello 정규 분포 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="465ad-122">SD-hello 정규 분포 표준 편차입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="465ad-123">쪽-L hello 배포의 낮은 쪽 hello에 대 한 잠금과 U hello 분포의 상한 면 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="465ad-124">hello 서비스의 hello 출력은 확률을 지정 하는 hello와 연결 된 계산 hello 변 위치.</span><span class="sxs-lookup"><span data-stu-id="465ad-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="465ad-125">정규 분포 확률 계산기</span><span class="sxs-lookup"><span data-stu-id="465ad-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="465ad-126">이 서비스는 정규 분포의 4 개 인수를 받아들이고 hello 관련 된 확률을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="465ad-127">hello 입력된 인수는.</span><span class="sxs-lookup"><span data-stu-id="465ad-127">hello input arguments are:</span></span>

* <span data-ttu-id="465ad-128">q – 정규 분포를 통한 이벤트의 단일 분위수</span><span class="sxs-lookup"><span data-stu-id="465ad-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="465ad-129">평균-hello 정규 분포 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="465ad-130">SD-hello 정규 분포 표준 편차입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="465ad-131">쪽-L hello 배포의 낮은 쪽 hello에 대 한 잠금과 U hello 분포의 상한 면 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="465ad-132">hello 서비스의 hello 출력은 변 위치를 지정 하는 hello와 연결 된 계산 hello 확률.</span><span class="sxs-lookup"><span data-stu-id="465ad-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="465ad-133">정규 분포 생성기</span><span class="sxs-lookup"><span data-stu-id="465ad-133">Normal Distribution Generator</span></span>
<span data-ttu-id="465ad-134">이 서비스는 정규 분포의 3개 인수를 수락하고 정규적으로 분포되는 숫자의 임의 시퀀스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="465ad-135">hello 다음 인수도 제공 해야 tooit hello 요청 내:</span><span class="sxs-lookup"><span data-stu-id="465ad-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="465ad-136">n-hello 수가 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="465ad-137">평균-hello 정규 분포 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="465ad-138">sd-hello 정규 분포 표준 편차입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="465ad-139">hello 서비스의 hello 출력은 정규 분포 hello 평균과 sd 인수에 따라 길이가 n의 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="465ad-140">이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="465ad-141">여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 여기: [생성기](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [확률 계산기](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [변 위치 계산기](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="465ad-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="465ad-142">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="465ad-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="465ad-143">정규 분포 분위수 계산기</span><span class="sxs-lookup"><span data-stu-id="465ad-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="465ad-144">정규 분포 확률 계산기</span><span class="sxs-lookup"><span data-stu-id="465ad-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="465ad-145">정규 분포 생성기</span><span class="sxs-lookup"><span data-stu-id="465ad-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="465ad-146">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="465ad-146">Creation of web service</span></span>
> <span data-ttu-id="465ad-147">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="465ad-148">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="465ad-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="465ad-149">다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="465ad-150">정규 분포 분위수 계산기</span><span class="sxs-lookup"><span data-stu-id="465ad-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="465ad-151">실험 흐름:</span><span class="sxs-lookup"><span data-stu-id="465ad-151">Experiment flow:</span></span>

![실험 흐름][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="465ad-153">정규 분포 확률 계산기</span><span class="sxs-lookup"><span data-stu-id="465ad-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="465ad-154">실험 흐름:</span><span class="sxs-lookup"><span data-stu-id="465ad-154">Experiment flow:</span></span>

![실험 흐름][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="465ad-156">정규 분포 생성기</span><span class="sxs-lookup"><span data-stu-id="465ad-156">Normal Distribution Generator</span></span>
<span data-ttu-id="465ad-157">실험 흐름:</span><span class="sxs-lookup"><span data-stu-id="465ad-157">Experiment flow:</span></span>

![실험 흐름][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="465ad-159">제한 사항</span><span class="sxs-lookup"><span data-stu-id="465ad-159">Limitations</span></span>
<span data-ttu-id="465ad-160">이들은 hello 정규 분포를 둘러싼 매우 간단한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="465ad-161">위의 hello 예제 코드에서 볼 수 있듯이 거의 오류 찾기 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="465ad-162">FAQ</span><span class="sxs-lookup"><span data-stu-id="465ad-162">FAQ</span></span>
<span data-ttu-id="465ad-163">Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="465ad-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

