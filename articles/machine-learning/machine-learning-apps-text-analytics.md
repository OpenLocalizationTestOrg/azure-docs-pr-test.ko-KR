---
title: "Machine Learning API: 텍스트 분석 | Microsoft Docs"
description: "Microsoft의 시스템 학습 텍스트 분석 Api 사용된 tooanalyze 수 감성 분석, 키 구 추출, 언어 검색 및 항목 검색에 대 한 구조화 되지 않은 텍스트입니다."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>기계 학습 API: 정서, 핵심 구문 추출, 언어 검색 및 토픽 검색을 위한 텍스트 분석
> [!NOTE]
> 이 가이드는 hello API의 버전 1에 대 한 합니다. 버전 2, [ **toothis 문서 참조**](../cognitive-services/cognitive-services-text-analytics-quick-start.md)합니다. 버전 2이이 API의 기본 버전 hello 되었습니다.
> 
> 

## <a name="overview"></a>개요
hello 텍스트 분석 API는 텍스트 분석의 제품군 [웹 서비스](https://datamarket.azure.com/dataset/amla/text-analytics) Azure 기계 학습을 사용 하 여 작성 합니다. hello API 사용된 tooanalyze 수 감성 분석, 키 구 추출, 언어 검색 및 항목 검색 등의 작업에 대 한 구조화 되지 않은 텍스트입니다. 데이터는 교육 없습니다 필요한 toouse이이 API: 방금 텍스트 데이터를 표시 합니다. 이 API는 고급 언어 처리 기술 toodeliver 가장 클래스 예측에 사용 합니다.

텍스트 분석 작업에서에서 확인할 수 있습니다이 [데모 사이트](https://text-analytics-demo.azurewebsites.net/)또한을 찾을 수 있는, [샘플](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) 방법에 C# 및 Python tooimplement 텍스트 분석 합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>정서 분석
hello API는 0 및 1 사이의 점수를 반환합니다. 점수 닫기 too1 점수 닫기 too0 음수 인지를 나타내는 반면 긍정적인 인지를 나타냅니다. 정서 점수는 분류 기술을 사용하여 생성됩니다. hello 입력된 기능 toohello 분류자 n 그램, 음성 부분 태그 및 포함 된 word에서 생성 된 기능을 포함 합니다. 현재 영어는 hello 언어 에서만 지원 됩니다.

## <a name="key-phrase-extraction"></a>핵심 문구 추출
hello API hello 제안에서에서 요점 hello 입력된 텍스트를 나타내는 문자열 목록을 반환 합니다. Microsoft Office의 정교한 자연어 처리 도구 키트에서 제공되는 기술을 사용합니다. 현재 영어는 hello 언어 에서만 지원 됩니다.

## <a name="language-detection"></a>언어 검색
hello API hello 검색 언어 및 0 및 1 사이의 점수를 반환 합니다. 점수 닫기 too1 100% 확신도 식별 하는 hello 언어 true 인지를 나타냅니다. 총 120개의 언어가 지원됩니다.

## <a name="topic-detection"></a>토픽 검색
제출 된 텍스트 레코드 목록에 대 한 hello 최상위 검색 된 항목을 반환 하는 새로 출시 된 API입니다. 토픽은 핵심 문구로 식별되며 하나 이상의 관련 단어를 가질 수 있습니다. 이 API에서는 100 텍스트의 최소 제출 toobe를 기록 하는 수백 디자인 된 toodetect 항목은 레코드의 toothousands 합니다. 이 API는 제출된 텍스트 레코드당 하나의 트랜잭션을 사용합니다. hello API는 검토와 사용자에 게 피드백 등의 텍스트를 작성 하는 short, 인적에 대 한 잘 설계 된 toowork입니다.

- - -
## <a name="api-definition"></a>API 정의
### <a name="headers"></a>헤더
Hello 올바른 헤더, 다음과 같이 있어야 하 고 요청에 포함 하 고 확인 해야 합니다.

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Hello에서 계정에서 계정 키를 찾을 수 있습니다 [Azure 데이터 마켓](https://datamarket.azure.com/account/keys)합니다. 현재는 JSON의 경우에만 입력 및 출력 형식이 허용됩니다. XML은 지원되지 않습니다.

- - -
## <a name="single-response-apis"></a>단일 응답 API
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**예제 요청**

아래 hello 호출 감성 분석 hello 구 "Hello World"에 대 한 요청:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

그러면 다음과 같이 응답을 반환합니다.

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**예제 요청**

Hello 호출 아래에서 키 구를 hello 문제를 발견 hello 텍스트에 ", 고유 장식 및 친숙 한 직원 훌륭한 호텔 toostay" 요청 하는 했습니다.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

그러면 다음과 같이 응답을 반환합니다.

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**예제 요청**

아래 hello GET 호출에서 hello 텍스트에서 키 구 hello에 대 한 hello 의미에 대 한 요청 하는 것 *Hello World*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

그러면 다음과 같이 응답을 반환합니다.

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**선택적 매개 변수**

`NumberOfLanguagesToDetect` 는 선택적 매개 변수입니다. hello 기본값은 1입니다.

- - -
## <a name="batch-apis"></a>배치 API
hello 텍스트 분석 서비스 toodo 감성 및 키 구 추출 일괄 처리 모드에 있습니다. 하나의 트랜잭션으로 점수가 매겨진 각 hello 레코드 개수를 확인 합니다. 예를 들어 단일 호출에서 1000개의 레코드에 대한 정서를 요청하면 1000개의 트랜잭션이 공제됩니다.

Hello Id hello 시스템에 입력 하는 hello Id hello 시스템에 의해 반환 됩니다. hello 웹 서비스는 이러한 Id는 고유한 것을 확인 하지 않습니다. hello hello 호출자 tooverify 고유 합니다. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**예제 요청**

hello POST 호출 아래 hello 표현의 hello 구 "Hello World", "Foo World Hello" 및 "내의 Hello World" hello hello 요청 본문에 대 한 요청 했습니다.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

본문 요청:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

아래 hello 응답에서 텍스트 Id와 연결 된 점수 hello 목록이 나타날 수 있습니다.

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**예제 요청**

이 예제에서는 텍스트를 다음 hello에서 키 구 hello에 대 한 표현의 목록은 hello에 대 한 요청 하는 것: 

* ", 고유 장식 및 친숙 한 직원 훌륭한 호텔 toostay 했습니다"
* "It was an amazing build conference, with very interesting talks"
* "hello 트래픽 찍 했, toohello 공항 라인으로 전환 하는 3 시간을 투자"

이 요청은 POST 호출 toohello 끝점으로 구성 됩니다.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

본문 요청:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

아래 hello 응답에서 텍스트 Id와 연결 된 키 구 hello 목록이 나타날 수 있습니다.

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

Hello POST 호출 아래에 두 개의 텍스트 입력에 대 한 언어 검색 요청:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

본문 요청:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Hello 다음 응답으로 hello 두 번째 입력의 첫 번째 입력이 hello 및 프랑스어에서 영어 발견 되는 위치를 반환 합니다.

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>토픽 검색 API
제출 된 텍스트 레코드 목록에 대 한 hello 최상위 검색 된 항목을 반환 하는 새로 출시 된 API입니다. 토픽은 핵심 문구로 식별되며 하나 이상의 관련 단어를 가질 수 있습니다. 이 API는 제출된 텍스트 레코드당 하나의 트랜잭션을 사용합니다.

이 API에서는 100 텍스트의 최소 제출 toobe를 기록 하는 수백 디자인 된 toodetect 항목은 레코드의 toothousands 합니다.

### <a name="topics--submit-job"></a>토픽 - 작업 제출
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**예제 요청**

아래 hello POST 호출에서 여러 여기서 hello 이름과 성을 입력가 표시 되는 문서 및 두 StopPhrases 포함 하는 100 문서에 대 한 항목이 요청 합니다.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

본문 요청:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

아래 hello 응답에서 hello 제출 된 작업에 대 한 hello를 JobId를 얻습니다.

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

토픽으로 반환할 수 없는 한 단어 또는 여러 단어 문구의 목록입니다. 매우 일반적인 항목을 사용 하는 toofilter 될 수 있습니다. 예를 들어 호텔 리뷰에 대한 데이터 집합에서 "호텔" 및 "호스텔"은 합리적인 중지 문구가 될 수 있습니다.  

### <a name="topics--poll-for-job-results"></a>토픽 - 작업 결과에 대한 설문 조사
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**예제 요청**

JobId hello '전송 작업' 단계 toofetch hello 결과에서 반환 된 hello를 전달 합니다. 호출 하는이 끝점 상태가 될 때까지 1 분 마다 권장 = hello 응답에 '완료'입니다. 작업 toocomplete 이상 동안 수천 개의 레코드를 사용 하 여 작업에 대 한 약 10 분이 걸립니다.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


처리 하는 동안 hello 응답은 다음과 같이 됩니다.

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


hello API 형식에 따라 hello에 대 한 JSON 형식으로 출력을 반환 합니다.

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


hello 응답의 각 부분에 대 한 hello 속성은 다음과 같습니다.

**TopicInfo 속성**

| 키 | 설명 |
|:--- |:--- |
| TopicId |각 토픽에 대한 고유 식별자입니다. |
| Score |레코드의 수가 tootopic를 할당 합니다. |
| KeyPhrase |요약 단어 또는 구를 hello 항목에 대 한 합니다. 한 단어 또는 여러 단어가 될 수 있습니다. |

**TopicAssignment 속성**

| 키 | 설명 |
|:--- |:--- |
| Id |Hello 레코드에 대 한 식별자입니다. Hello 입력에 포함 된 toohello ID를 같습니다. |
| TopicId |hello 항목 ID는 hello 레코드에 할당 되었습니다. |
| Distance |신뢰도 hello 레코드 속해 toohello 항목입니다. 거리 자세히 toozero에 더 높은 신뢰 수준을 나타냅니다. |

