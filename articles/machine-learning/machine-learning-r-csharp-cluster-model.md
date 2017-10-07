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
# <a name="deprecated-cluster-model"></a>(사용되지 않음) 클러스터 모델

> [!NOTE]
> hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며 
> 
> Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다. Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

그룹의 순서 tooreduce hello 충전 오프 위험을 신용 카드 발급자 신용 cardholders 동작을 예측할 수 있습니다 어떻게 우리? 수 정의 하는 직원의 개성 특성의 그룹 순서 tooimprove에 직장 성능을? 의사 들에 게는 어떻게 자신의 질병의 hello 특성에 따라 그룹으로 환자 분류할 수 있습니까? 원칙적으로 클러스터 분석을 통해 이러한 모든 질문에 대답할 수 있습니다.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

클러스터 분석에서는 변수 조합을 기반으로 하여 관찰 집합을 둘 이상의 상호 배타적인 알 수 없는 그룹으로 분류합니다. hello 클러스터 분석의 목적은 toodiscover 관찰, 일반적으로 사람 또는 해당 특성 그룹으로 구성 하는 시스템 여기서 hello 그룹의 멤버 속성을 공유 공통입니다. 이 [서비스](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) 사용 하 여 hello K-means 방법은 방법, 자주 사용 되는 클러스터링 기술 toocluster 임의의 데이터를 그룹으로 합니다. 이 웹 서비스는 hello 데이터를 가져와 및 k hello 수를 입력으로 클러스터 및 각 관찰 속한 hello k 그룹 toowhich 중의 예측을 생성 합니다. 

> 사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다. 하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다. Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다. hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.  
> 
> 

## <a name="consumption-of-web-service"></a>웹 서비스 사용
이 웹 서비스의 각 행에 대 한 k 그룹 및 출력 hello 그룹 할당 집합으로 hello 데이터를 그룹화 합니다. 여기서 행은 쉼표 (,)로 구분 되 고 열은 세미콜론 (;)으로 구분 문자열 hello 최종 사용자 tooinput 데이터를 필요로 하는 hello 웹 서비스입니다. hello 웹 서비스에는 한 번에 1 개 행이 필요합니다. 예제 데이터 집합은 다음과 같습니다.

![샘플 데이터][1]

3 개의 상호 배타적인 그룹으로 hello 원하는 사용자 tooseparate이이 데이터를 가정 합니다. 데이터 입력을 데이터 집합 위에 hello hello 다음 hello: 값 = "10; 5; 2,18, 1; 6,7; 5; 5,22; 3; 4,12 않으면 2; 1,10; 3; 4"; k = "3"입니다. hello 출력 각 hello 행에 대 한 예측된 그룹 구성원 자격을 hello 됩니다.

> 이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다. 
> 
> 

여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>웹 서비스 사용의 C# 코드 시작:
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




## <a name="creation-of-web-service"></a>웹 서비스 만들기
> 이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다. 무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요. 다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.
> 
> 

Azure 기계 학습에서는 내에서 새로운 빈 실험을 만들 때와 그 두 [R 스크립트 실행] [ execute-r-script] 모듈 hello 작업 영역으로 끌어옵니다. hello 데이터 스키마가 생성 하는 간단한 [R 스크립트 실행][execute-r-script]합니다. 그런 다음 hello 데이터 스키마가 연결 된 toohello 모델 섹션을 사용 하 여 다시 만든 클러스터는 [R 스크립트 실행][execute-r-script]합니다. Hello에 [R 스크립트 실행] [ execute-r-script] hello 클러스터 모델의 사용, hello 웹 서비스가 다음 사용 "k 수단" hello 함수 hello에 미리 작성 된를 [R 스크립트 실행] [ execute-r-script] Azure 기계 학습의 합니다.    

![실험 흐름][3]

#### <a name="module-1"></a>모듈 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>모듈 2:
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


## <a name="limitations"></a>제한 사항
이 예제는 매우 간단한 클러스터링 웹 서비스 예제입니다. 위의 hello 예제 코드에서 볼 수 있듯이 없음 오류 찾기는 구현 하 여 hello 서비스 가정 모든 항목은 연속 변수 (범주 기능이 없습니다 허용), hello 서비스 지 원하는 유일한 입력 숫자 값으로이 웹 hello 생성 hello 시 서비스입니다. 또한 hello 서비스가 현재 처리 하는 제한 된 데이터 크기를 hello 웹 서비스의 요청/응답 특성 toohello 인해 호출과 hello 사실을 hello 모델은 되 고 적합 hello 웹 서비스를 호출할 때마다 합니다. 

## <a name="faq"></a>FAQ
Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

