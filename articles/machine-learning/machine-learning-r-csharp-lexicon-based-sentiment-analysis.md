---
title: "aaa(deprecated) 어휘 집 기반 감정 분석-Azure | Microsoft Docs"
description: "(사용되지 않음) 어휘집 기반 감정 분석"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(사용되지 않음) 어휘집 기반 감정 분석

> [!NOTE]
> hello Microsoft DataMarket은 사용 되지 않음이 API는 사용 되지 않으며 
> 
> Hello에서 많은 유용한 예 실험 및 Api를 찾을 수 있습니다 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다. Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

온라인 소셜 네트워크(예: Facebook 게시물, 트윗, 리뷰 등)에서 브랜드나 주제에 대한 사용자의 의견과 태도를 어떻게 측정할 수 있을까요? 감정 분석을 통해 이러한 질문을 분석할 수 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

감정 분석 방법으로는 일반적으로 두 가지 방법이 있습니다. 지도 방식된 학습 알고리즘을 사용 하는 하나 및 다른 hello 자율된 학습으로 처리할 수 있습니다. 감독되는 학습 알고리즘은 일반적으로 주석이 지정된 큰 모음을 기반으로 분류 모델을 작성합니다. 정확성 hello 주석의 hello 품질에 주로 기반 및 일반적으로 hello 학습 프로세스는 시간이 오래 걸립니다. 뿐만 아니라 hello 알고리즘 tooanother 도메인에 적용할 때 hello 결과 일반적으로 바람직하지 않습니다. 어휘 집 기반 감정 사전 큰 데이터 모음을 저장 하지 않아도 사용 하 여 자율된 학습 및 교육-낮추는 전체 프로세스를 훨씬 빠르게 hello toosupervised 학습을 비교 합니다. 

우리의 [서비스](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) 는 hello 가장 일반적으로 사용 하는 hello 주 관성 집을 중 하나인 MPQA 주 관성 사전 (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/)을 기반으로 합니다. MPQA에는 5097개의 부정적인 감정과 2533개의 긍정적인 감정이 있습니다. 또한 이러한 모든 단어에는 강하거나 약한 극성으로 주석이 지정되어 있습니다. GNU General Public License hello 전체 모음이입니다. hello 웹 서비스는 트 윗 및 Facebook 게시물 등 적용된 tooany 짧은 문장 될 수 있습니다. 

> 사용자는 이 웹 서비스를 모바일 앱이나 웹 사이트를 통해 사용하거나 로컬 컴퓨터에서도 사용할 수 있습니다. 하지만 hello 웹 서비스의 목적은 hello Azure 기계 학습 R 코드를 기반으로 웹 서비스를 사용 하는 toocreate을 수 있는 방법의 예를 들어 tooserve 이기도 합니다. Azure 기계 학습 스튜디오 내에서 R 코드 몇 줄을 포함하고 단추를 몇 번 클릭하면 R 코드를 사용하여 실험을 만들고 웹 서비스로 게시할 수 있습니다. hello 웹 서비스 게시 toohello Azure 마켓플레이스 수 및 hello 웹 서비스의 hello 작성자가 인프라 설치 하지 않고도 hello 전 세계 사용자와 장치에서 사용 합니다.
> 
> 

## <a name="consumption-of-web-service"></a>웹 서비스 사용
hello 입력된 데이터에는 모든 텍스트를 가능 하지만 더 짧은 문장은 hello 웹 서비스입니다. hello 출력은-1과 1 사이의 숫자 값입니다. 0 보다 작은 모든 값의 hello 텍스트 hello 감성 음수; 임을 나타내는합니다 0 초과 하는 경우 양수입니다. hello 결과 hello 절대 값은 연결 된 hello 감성의 hello 강도를 나타냅니다. 

> 이 서비스 hello Azure Marketplace에서 호스트는 OData 서비스입니다. 이 POST 또는 GET 메서드를 통해 호출할 수 있습니다. 
> 
> 

여러 가지 방법으로 자동화 된 방식으로 hello 서비스를 사용 하는 (예제 앱은 [여기](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>웹 서비스 사용의 C# 코드 시작:
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



hello 입력은 "오늘 좋은 하루 합니다." hello 출력은 "1" hello 입력된 문장이와 관련 된 긍정적인 인지를 나타냅니다. 

## <a name="creation-of-web-service"></a>웹 서비스 만들기
> 이 웹 서비스는 Azure 기계 학습을 사용하여 만들었습니다. 무료 평가판 및 실험을 만들고 [웹 서비스를 게시](machine-learning-publish-a-machine-learning-web-service.md)하는 방법에 대한 소개 비디오는 [azure.com/ml](http://azure.com/ml)을 참조하세요. 다음은 각 hello 실험 내 hello 모듈에 대 한 hello 웹 서비스와 예제 코드를 생성 하는 hello 실험의 스크린샷입니다.
> 
> 

Azure 기계 학습 내에서 새로운 빈 실험이 만들어졌습니다. 아래 hello 그림 어휘 집 기반 감정 분석의 hello 실험 흐름을 보여 줍니다. hello "sent_dict.csv" hello MPQA 주 관성 lexicon은 파일과의 hello 입력 중 하나로 설정 [R 스크립트 실행][execute-r-script]합니다. 다른 입력이 테스트를 선택, 열 이름 수정 수행 म 및 분할 작업에 대 한 hello Amazon 검토 데이터 집합에서 샘플링 된 검토 합니다. Hello 메모리에 해시 패키지 toostore hello 주 관성 용어를 사용 하 고 hello 점수 계산 프로세스를 가속화할 합니다. hello 전체 텍스트 "tm" 패키지에 의해 토큰화 되며 hello 단어 hello 감성 사전에서 비교 합니다. 마지막으로, 각 주관적인 단어의 hello 가중치 hello 텍스트에 추가 하 여 점수를 계산 됩니다. 

### <a name="experiment-flow"></a>실험 흐름:
![실험 흐름][2]

#### <a name="module-1"></a>모듈 1:
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>해시 패키지 설치
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>제한 사항
알고리즘의 관점에서 어휘 집 기반 감정 분석은 일반 감성 분석 도구 특정 필드에 대 한 hello 분류 방법 보다 더 잘 수행 하지 않을 수 있습니다. hello 부정 문제 되지 잘 처리 됩니다. 여기서는 프로그램에 몇 가지 부정 단어를 하드 코드하지만, 더 좋은 방법은 부정 사전을 사용하고 몇 가지 규칙을 작성하는 것입니다. hello 웹 서비스 보다 잘에 수행 트 윗 및 Facebook 게시물 등 짧고 간단한 문장을 보다 Amazon 리뷰와 같은 길고 복잡 한 문장에 합니다. 

## <a name="faq"></a>FAQ
Hello 웹 서비스 또는 Azure 마켓플레이스에서 게시 toohello의 사용에 대 한 자주 묻는 질문에 대 한 참조 [여기](machine-learning-marketplace-faq.md)합니다.

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


