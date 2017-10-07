---
title: "Azure 기계 학습을 사용 하 여 생존 분석 aaa(deprecated) | Microsoft Docs"
description: "(사용되지 않음) 생존 분석 이벤트 발생 확률"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a>(사용되지 않음) 생존 분석

> [!NOTE]
> hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며 
> 
> Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다. Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

대부분의 시나리오에서 평가에서 주요 결과 hello은 관심 있는 hello 시간 tooan 이벤트입니다. 즉, hello 질문 "발생 한 경우이 이벤트?" 질문합니다. 예를 들어 hello까지 여기서 hello 데이터 hello 경과 시간 (일, 년, 주행 거리 등)에 대해 설명 하는 경우를 가정해 보십시오 (질병 relapse, 받은 PhD도, 브레이크 패드 실패) 관련 이벤트 발생 합니다. Hello 데이터의 각 인스턴스는 특정 개체를 (환자, 학생, 자동차 등.)을 나타냅니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

이 [웹 서비스](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) hello 질문의 대답을 "이란 관련 이벤트 hello hello 확률에 수행 됩니다 x 개체에 대 한 시간 n?" 생존 분석 모델을 제공 하 여이 웹 서비스 사용자 toosupply 데이터 tootrain hello 모델 있으며이 테스트 합니다. hello 주제 hello 실험은 관심 있는 hello 이벤트가 발생할 때까지 toomodel hello 길이 hello 경과 시간입니다. 

> 사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다. 하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다. Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다. hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.  
> 
> 

## <a name="consumption-of-web-service"></a>웹 서비스 사용
hello 웹 서비스의 hello 입력된 데이터 스키마는 다음 표에 hello에 표시 됩니다. 6 가지 정보 hello 입력으로 필요: 학습 데이터, 테스트 데이터, 원하는 시간, "시간" 차원의 hello 인덱스, "이벤트" 차원과 hello 변수 형식에 대 한 hello 인덱스 (연속 또는 요소). 여기서 hello 행이 쉼표로 구분 되 고 hello 열이 세미콜론으로 구분 됩니다 문자열로 hello 학습 데이터가 표시 됩니다. hello 데이터 기능의 hello 수는 유연 합니다. Hello 입력된 문자열에서 모든 hello 요소는 숫자 여야 합니다. "Hello"시간 차원 hello 학습 데이터의 hello 시간 단위 (일, 년, 주행 거리 등) 이후 경과 hello hello의 시작 지점 (환자와 처리 방법 프로그램, 학생 시작 PhD 연구, toobe 시작 자동차 수신 연구를 나타냅니다. 제어, 등) hello 이벤트가 발생할 때까지 관심 (hello 환자 toodrug 사용, hello 학생 얻으려면 hello PhD도, 브레이크 패드 실패 등 필요 hello 자동차 반환). hello "이벤트" 차원 hello 관련 이벤트의 hello 시간만 hello 끝에서 발생 하는지 여부를 나타냅니다. 값이 "이벤트 = 1" hello "시간" 차원;으로 표시 하는 hello 시간에 관심 이벤트 hello 의미 발생 "이벤트 0 =" hello "시간" 차원에서 지정 된 hello 시간 관련 이벤트 hello 의미를 수행 하지 않은 합니다.

* trainingdata - 문자열입니다. 행은 쉼표로 구분되고 열은 세미콜론으로 구분됩니다. 각 행에는 "시간" 차원, "이벤트" 차원 및 예측 요인 변수가 포함됩니다.
* testingdata - 특정 개체에 대한 예측 요인 변수를 포함하는 데이터의 한 행입니다.
* time_of_interest-관심 있는 n hello 경과 시간입니다.
* index_time-(1부터 시작) hello "시간" 차원의 hello 열 인덱스입니다.
* index_event-(1부터 시작) hello "이벤트" 차원의 hello 열 인덱스입니다.
* variable_types - 세미콜론을 구분 기호로 사용하는 문자열입니다. 0은 연속 변수를 나타내고 1은 요소 변수를 나타냅니다.

hello 출력은 특정 시간으로 발생 하는 이벤트의 hello 확률입니다. 

> 이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다. 
> 
> 

여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>웹 서비스 사용의 C# 코드 시작:
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




이 테스트의 hello 해석은 다음과 같습니다. Hello hello 데이터의 ´ ֲ toomodel hello 경과 된 시간까지 hello 가정 hello 두 처리 프로그램 중 하나를 받은 환자의 hello에 대 한 toodrug 사용량을 반환 합니다. hello 웹 서비스 읽기 출력 hello: 환자 35 세 되 고, 이전 필요 약품 처리 2 배 hello 긴 가계 처리 프로그램 라인으로 전환 하며 heroin와 cocaine 사용법과 hello 확률의 toohello 약품 사용 반환 95.64 %by 500 일입니다.

## <a name="creation-of-web-service"></a>웹 서비스 만들기
> 이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다. 무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요. 다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.
> 
> 

Azure 기계 학습에서는 내에서 새로운 빈 실험을 만들 때와 그 두 [R 스크립트 실행] [ execute-r-script] 모듈 hello 작업 영역으로 끌어온 합니다. hello 데이터 스키마로 만들어진 간단한 [R 스크립트 실행][execute-r-script], hello 웹 서비스에 대 한 hello 입력된 데이터 스키마를 정의 하는 합니다. 이 모듈은 다음 두 번째 toohello 연결 [R 스크립트 실행] [ execute-r-script] 작업 주요지 않습니다는 모듈입니다. 이 모듈은 데이터 전처리, 모델 작성 및 예측을 수행합니다. Hello 데이터 전처리 단계에서 긴 문자열이 나타내는 hello 입력된 데이터 변형 되어 데이터 프레임으로 변환 합니다. Hello 모델 빌드 단계에서 생존 분석을 수행 하기 위한 "survival_2.37 7.zip" 외부 R 패키지를 처음 설치 됩니다. 그런 다음 hello "coxph" 함수는 계열 데이터 처리 작업 후 실행 됩니다. hello R 설명서에서 생존 분석에 대 한 hello "coxph" 함수의 hello 세부 정보를 읽을 수 있습니다. Hello 예측 단계에서 테스트 인스턴스 hello "surfit" 함수로 hello 학습 된 모델을 제공 하 고이 테스트 인스턴스에 대 한 hello 서바이벌 곡선은 "curve" 변수로 발생 했습니다. 마지막으로, hello 확률 관심 있는 hello 시간을 가져옵니다. 

### <a name="experiment-flow"></a>실험 흐름:
![실험 흐름][1]

#### <a name="module-1"></a>모듈 1:
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a>모듈 2:
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a>제한 사항
이 웹 서비스는 기능 변수(열)로 숫자 값만 사용할 수 있습니다. hello "이벤트" 열에는 0 또는 1 값만 사용할 수 있습니다. hello "시간" 열에는 양의 정수 toobe를 해야합니다.

## <a name="faq"></a>FAQ
Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

