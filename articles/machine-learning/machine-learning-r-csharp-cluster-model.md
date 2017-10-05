---
title: "(사용되지 않음) 클러스터 모델 - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="b1b96-103">(사용되지 않음) 클러스터 모델</span><span class="sxs-lookup"><span data-stu-id="b1b96-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="b1b96-104">Microsoft DataMarket은 종료되고 있는 중이며 이 API는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="b1b96-105">[Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com)에서 많은 유용한 예제 실험과 API를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="b1b96-106">갤러리에 대한 자세한 내용은 [Cortana Intelligence 갤러리의 리소스 공유 및 검색](machine-learning-gallery-how-to-use-contribute-publish.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b96-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="b1b96-107">신용 카드 발급자의 결손 공제 위험을 줄이기 위해 신용 카드 소유자의 행동 그룹을 어떻게 예측할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="b1b96-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="b1b96-108">회사에서 직원의 성과를 향상시키기 위해 직원의 성격 특성 그룹을 어떻게 정의할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="b1b96-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="b1b96-109">의사는 환자의 질병 특성을 기반으로 하여 환자를 어떻게 그룹으로 분류할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="b1b96-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="b1b96-110">원칙적으로 클러스터 분석을 통해 이러한 모든 질문에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="b1b96-111">클러스터 분석에서는 변수 조합을 기반으로 하여 관찰 집합을 둘 이상의 상호 배타적인 알 수 없는 그룹으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="b1b96-112">클러스터 분석의 목적은 관찰(일반적으로 사람 또는 해당 특성)을 그룹으로 구성하는 체계를 발견하는 것입니다. 여기서 그룹의 구성원은 속성을 공통적으로 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="b1b96-113">이 [서비스](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model)에서는 일반적으로 사용되는 클러스터링 기법인 K-Means 방법론을 사용하여 임의 데이터를 그룹으로 클러스터합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="b1b96-114">이 웹 서비스는 데이터 및 k 클러스터 수를 입력으로 사용하여 각 관찰이 속하는 k 그룹에 대한 예측을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="b1b96-115">사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="b1b96-116">하지만 이 웹 서비스는 Azure 기계 학습을 사용하여 R 코드 기반의 웹 서비스를 만드는 방법을 보여 주는 예로 제공되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="b1b96-117">Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="b1b96-118">그런 다음 웹 서비스를 Azure 마켓플레이스에 게시하면 웹 서비스 작성자가 인프라를 설정하지 않고도 전 세계의 사용자와 장치에서 이러한 웹 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="b1b96-119">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="b1b96-119">Consumption of web service</span></span>
<span data-ttu-id="b1b96-120">이 웹 서비스는 데이터를 k 그룹 집합으로 그룹화하고 각 행의 그룹 할당을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="b1b96-121">이 웹 서비스는 최종 사용자가 데이터를 행은 쉼표(,)로 구분되고 열은 세미콜론(;)으로 구분된 문자열로 입력할 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="b1b96-122">이 웹 서비스는 한 번에 1개의 행을 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="b1b96-123">예제 데이터 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-123">An example dataset could look like this:</span></span>

![샘플 데이터][1]

<span data-ttu-id="b1b96-125">사용자가 이 데이터를 상호 배타적인 세 개의 그룹으로 구분하려 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="b1b96-126">위 데이터 집합의 데이터 입력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="b1b96-127">value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3” 출력은 각 행의 예측된 그룹 멤버 자격입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="b1b96-128">Azure 마켓플레이스에서 호스트되는 이 서비스는 OData 서비스이고 POST 또는 GET 메서드를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="b1b96-129">다양한 자동화된 방식으로 서비스를 사용할 수 있습니다(예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="b1b96-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="b1b96-130">웹 서비스 사용의 C# 코드 시작:</span><span class="sxs-lookup"><span data-stu-id="b1b96-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="b1b96-131">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b1b96-131">Creation of web service</span></span>
> <span data-ttu-id="b1b96-132">이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="b1b96-133">무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b96-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="b1b96-134">다음은 웹 서비스를 만든 실험과 실험 내 각 모듈의 예제 코드의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="b1b96-135">Azure Machine Learning 내에서 새로운 빈 실험이 만들어졌으며 두 개의 [R 스크립트 실행][execute-r-script] 모듈을 작업 영역으로 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="b1b96-136">데이터 스키마는 간단한 [R 스크립트 실행][execute-r-script]으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="b1b96-137">데이터 스키마를 클러스터 모델 섹션에 연결하고 다시 [R 스크립트 실행][execute-r-script]을 사용하여 데이터 스키마를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="b1b96-138">그런 다음 클러스터 모델에 사용된 [R 스크립트 실행][execute-r-script]에서 웹 서비스는 Azure Machine Learning의 [R 스크립트 실행][execute-r-script]에 미리 빌드된 “k-means” 함수를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![실험 흐름][3]

#### <a name="module-1"></a><span data-ttu-id="b1b96-140">모듈 1:</span><span class="sxs-lookup"><span data-stu-id="b1b96-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="b1b96-141">모듈 2:</span><span class="sxs-lookup"><span data-stu-id="b1b96-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="b1b96-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="b1b96-142">Limitations</span></span>
<span data-ttu-id="b1b96-143">이 예제는 매우 간단한 클러스터링 웹 서비스 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="b1b96-144">위의 예제 코드에서 알 수 있듯이 오류 catch는 구현되지 않고 서비스에서는 이 웹 서비스를 만들 때 숫자 값만 입력하므로 모든 항목이 연속 변수인 것으로 가정합니다(범주 기능이 허용되지 않음).</span><span class="sxs-lookup"><span data-stu-id="b1b96-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="b1b96-145">또한 웹 서비스가 호출될 때마다 모델이 맞춰진다는 사실과 웹 서비스 호출의 요청/응답 속성 때문에 서비스에서는 현재 제한된 데이터 크기를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b96-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="b1b96-146">FAQ</span><span class="sxs-lookup"><span data-stu-id="b1b96-146">FAQ</span></span>
<span data-ttu-id="b1b96-147">웹 서비스 사용 또는 Azure 마켓플레이스 게시 방법과 관련한 질문과 대답은 [여기](machine-learning-marketplace-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1b96-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

