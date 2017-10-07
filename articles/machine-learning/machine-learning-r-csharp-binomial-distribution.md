---
title: "aaa(deprecated) 이항 분포 도구 모음-Azure | Microsoft Docs"
description: "(사용되지 않음) 이항 분포 패키지"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
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
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a>(사용되지 않음) 이항 분포 패키지

> [!NOTE]
> hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며 
> 
> Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다. Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

hello 이항 분포 제품군은 일련의 샘플 웹 서비스 ([이항 생성기](https://datamarket.azure.com/dataset/aml_labs/bdg5), [확률 계산기](https://datamarket.azure.com/dataset/aml_labs/bdp4), [변 위치 계산기](https://datamarket.azure.com/dataset/aml_labs/bdq5))에서 생성 하는 데 도움이 되 고 이항 분포를 처리합니다. hello 서비스를 통해 계산 변 위치 길이, 이항 분포 시퀀스 생성 중에서 제공 된 확률 및 계산 확률 지정된 변 위치입니다. Hello 선택한 서비스에 따라 서로 다른 출력을 내보내는 각 hello 서비스 (아래 설명 참조). 이항 분포 Suite hello hello R 통계 패키지에 포함 된 hello R 함수 qbinom, rbinom, 및 pbinom를 기반으로 합니다. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> 이러한 웹 서비스 소비 될 수 – 사용자가 잠재적으로 hello marketplace 웹 사이트를 통해 또는 로컬 컴퓨터에도 모바일 앱에서 직접 예입니다. 하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다. Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다. hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 되며 hello – 전 세계 사용자 및 장치에 사용 된 hello 웹 서비스의 hello 작성자가 인프라를 설치 하지 않아도 필요 합니다.
> 
> 

## <a name="consumption-of-web-service"></a>웹 서비스 사용
hello 이항 분포 제품군 3 서비스를 수행 하는 hello 포함 됩니다.

### <a name="binomial-distribution-quantile-calculator"></a>이항 분포 변위치 계산기
이 서비스는 정규 분포의 4 개 인수를 수락 하 고 연결 된 hello 변 위치를 계산 합니다.
hello 입력된 인수는.

* p - 여러 시도의 단일 집계 확률  
* 크기-hello 시행 횟수입니다.
* 문제-hello 평가판 성공 확률.
* 측면-L hello 분포의 상한 면 hello에 대 한 U, hello 분포의 더 낮은 쪽 hello에 대 한 합니다. 

hello 서비스의 hello 출력은 확률을 지정 하는 hello와 연결 된 계산 hello 변 위치.

### <a name="binomial-distribution-probability-calculator"></a>이항 분포 확률 계산기
이 서비스는 이항 분포의 4 개 인수를 받아들이고 hello 관련 된 확률을 계산 합니다.
hello 입력된 인수는.

* q – 이항 분포에서 이벤트의 단일 변위치 
* 크기-hello 시행 횟수입니다.
* 문제-hello 평가판 성공 확률.
* 측면-L hello 분포의 상한 면 hello에 대 한 U 또는 같은 tooa 단일 성공 횟수는 E hello 배포의 낮은 쪽 hello에 대 한 합니다.

hello 서비스의 hello 출력은 변 위치를 지정 하는 hello와 연결 된 계산 hello 확률.

### <a name="binomial-distribution-generator"></a>이항 분포 생성기
이 서비스는 이항 분포의 인수 3개를 받아들여 이항 분포된 숫자의 임의 시퀀스를 생성합니다. hello 다음 인수도 제공 해야 tooit hello 요청 내:

* n - 관찰 수 
* size – 시도 횟수
* prob – 성공 확률

hello 서비스의 hello 출력은 이항 분포 hello 크기와 문제 인수에 따라 길이가 n의 시퀀스입니다.

> 이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다. 
> 
> 

여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 여기: [생성기](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [확률 계산기](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [변 위치 계산기](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>웹 서비스 사용의 C# 코드 시작:
### <a name="binomial-distribution-quantile-calculator"></a>이항 분포 변위치 계산기
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a>이항 분포 확률 계산기
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a>이항 분포 생성기
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
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

### <a name="binomial-distribution-quantile-calculator"></a>이항 분포 변위치 계산기
![작업 영역 만들기][4]

#### <a name="module-1"></a>모듈 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a>모듈 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a>이항 분포 확률 계산기
![작업 영역 만들기][5]

#### <a name="module-1"></a>모듈 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a>모듈 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a>이항 분포 생성기
![작업 영역 만들기][6]

#### <a name="module-1"></a>모듈 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a>모듈 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>제한 사항
이들은 hello 이항 분포를 둘러싼 매우 간단한 예입니다. 위의 hello 예제 코드에서 볼 수 있듯이 거의 오류 찾기 구현 됩니다.

## <a name="faq"></a>FAQ
Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

