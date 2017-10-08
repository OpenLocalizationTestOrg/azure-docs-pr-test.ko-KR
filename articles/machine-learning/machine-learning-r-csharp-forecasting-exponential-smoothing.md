---
title: "-지 수 다듬기-Forecasting Azure aaa(deprecated) | Microsoft Docs"
description: "(사용되지 않음) 웹 서비스: 지수 평활법"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: ebc732d3a47943405b0cb26a373f529a50de9005
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a>(사용되지 않음) 예측 - 지수 평활법

> [!NOTE]
> hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며 
> 
> Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다. Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

이 [웹 서비스](https://datamarket.azure.com/dataset/aml_labs/ets) 구현 hello hello 사용자가 제공한 hello 기록 데이터에 따라 지 수 다듬기 모델 (ETS) tooproduce 예측 합니다. 올해 게 증가 하는 특정 제품에 대 한 수요가 hello? 있습니까 예측할 수 hello에 대 한 제품 판매 크리스마스 시즌을 효과적으로 내 인벤토리를 계획할 수 있습니까? 예측 모델은 apt tooaddress 이러한 질문 합니다. Hello 제공 이전의 데이터를 이러한 모델 숨겨진된 추세 및 계절성 toopredict 향후 추세를 검사 합니다.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> 사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다. 하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다. Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다. hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.
> 
> 

## <a name="consumption-of-web-service"></a>웹 서비스 사용
이 서비스는 4 개 인수를 수락 하 고 hello ETS 예측을 계산 합니다.
hello 입력된 인수는.

* 빈도-hello 원시 데이터 (매일/매주/매월/분기별/연도별)의 hello 빈도 표시 합니다.
* 출시가 임박한 시점 - 미래 예측 시간 프레임입니다.
* 날짜-시간에 대 한 데이터를 hello 새 시계열에 추가 합니다.
* 값 하-hello 새 시계열 데이터 값에 추가 합니다.

hello 서비스의 hello 출력 hello 예측된 값을 계산 됩니다.

샘플 입력은 다음과 같을 수 있습니다. 

* 빈도 - 12
* 출시가 임박한 시점 - 12
* 날짜 - 1/15/2012, 2/15/2012, 3/15/2012, 4/15/2012, 5/15/2012, 6/15/2012, 7/15/2012, 8/15/2012, 9/15/2012, 10/15/2012, 11/15/2012, 12/15/2012, 1/15/2013, 2/15/2013, 3/15/2013, 4/15/2013, 5/15/2013, 6/15/2013, 7/15/2013, 8/15/2013, 9/15/2013, 10/15/2013, 11/15/2013, 12/15/2013, 1/15/2014, 2/15/2014, 3/15/2014, 4/15/2014, 5/15/2014, 6/15/2014, 7/15/2014, 8/15/2014, 9/15/2014
* 값 - 3.479, 3.68, 3.832, 3.941, 3.797, 3.586, 3.508, 3.731, 3.915, 3.844, 3.634, 3.549, 3.557, 3.785, 3.782, 3.601, 3.544, 3.556, 3.65, 3.709, 3.682, 3.511, 3.429, 3.51, 3.523, 3.525, 3.626, 3.695, 3.711, 3.711, 3.693, 3.571, 3.509

> 이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다. 
> 
> 

여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>웹 서비스 사용의 C# 코드 시작:
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
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

Azure 기계 학습 내에서 새로운 빈 실험이 만들어졌습니다. 샘플 입력 데이터는 미리 정의된 데이터 스키마로 업로드되었습니다. 연결 된 toohello 데이터 스키마가 있는 [R 스크립트 실행] [ execute-r-script] 모듈 생성 하는 hello ETS 오른쪽에서 'ets' 및 '예측' 함수를 사용 하 여 모델을 예측 

![실험 흐름][2]

#### <a name="module-1"></a>모듈 1:
    # Add in hello CSV file with hello data in hello format shown below 
![데이터 샘플][3]    

#### <a name="module-2"></a>모듈 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a>제한 사항
이 예제는 매우 간단한 ETS 예측 예제입니다. 위의 hello 예제 코드에서 볼 수 있듯이 없음 오류 찾기는 구현 되 고 hello 서비스 모든 hello 변수는 연속/양수 값 및 hello 빈도 1 보다 큰 정수 여야 합니다 합니다. hello 날짜와 값 벡터의 hello 길이 동일한 hello 해야 합니다. hello 날짜 변수 toohello ' mm/dd/yyyy 형식의 ' 준수 해야 합니다.

## <a name="faq"></a>FAQ
Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

