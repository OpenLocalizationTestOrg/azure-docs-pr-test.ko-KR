---
title: "Machine Learning API: 텍스트 분석 | Microsoft Docs"
description: "Microsoft의 기계 학습 텍스트 분석 API를 사용하여 정서 분석, 핵심 문구 추출, 언어 검색 및 토픽 검색에 대해 구조화되지 않은 텍스트를 분석할 수 있습니다."
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
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="58584-103">기계 학습 API: 정서, 핵심 구문 추출, 언어 검색 및 토픽 검색을 위한 텍스트 분석</span><span class="sxs-lookup"><span data-stu-id="58584-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="58584-104">이 가이드는 API의 버전 1용입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="58584-105">버전 2의 경우 [**이 문서를 참조하세요**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="58584-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="58584-106">현재 버전 2가 기본 설정된 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="58584-107">개요</span><span class="sxs-lookup"><span data-stu-id="58584-107">Overview</span></span>
<span data-ttu-id="58584-108">텍스트 분석 API는 Azure 기계 학습을 사용하여 빌드한 텍스트 분석 [웹 서비스](https://datamarket.azure.com/dataset/amla/text-analytics) 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="58584-109">이 API를 사용하여 정서 분석, 핵심 문구 추출, 언어 검색 및 토픽 검색과 같은 작업에 대한 구조화되지 않은 텍스트를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="58584-110">학습 데이터 없이 이 API를 사용할 수 있으며, 텍스트 데이터를 가져오기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="58584-111">이 API는 고급 자연어 처리 기술을 사용하여 클래스 예측을 가장 잘 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="58584-112">[데모 사이트](https://text-analytics-demo.azurewebsites.net/)에서 작업에 대한 텍스트 분석을 볼 수 있으며 이 사이트에는 C# 및 Python에서 텍스트 분석을 구현하는 방법에 대한 [샘플](https://text-analytics-demo.azurewebsites.net/Home/SampleCode)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="58584-113">정서 분석</span><span class="sxs-lookup"><span data-stu-id="58584-113">Sentiment analysis</span></span>
<span data-ttu-id="58584-114">이 API는 0에서 1 사이의 숫자 점수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="58584-115">1에 가까운 점수는 긍정적인 정서를 나타내고, 0에 가까운 점수는 부정적인 정서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58584-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="58584-116">정서 점수는 분류 기술을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="58584-117">분류자의 입력 기능에는 N-그램, 음성 부분 태그에서 생성된 기능 및 단어 포함이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="58584-118">현재 지원되는 언어는 영어뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="58584-119">핵심 문구 추출</span><span class="sxs-lookup"><span data-stu-id="58584-119">Key phrase extraction</span></span>
<span data-ttu-id="58584-120">이 API는 입력 텍스트의 핵심 요지를 나타내는 문자열 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="58584-121">Microsoft Office의 정교한 자연어 처리 도구 키트에서 제공되는 기술을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="58584-122">현재 지원되는 언어는 영어뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="58584-123">언어 검색</span><span class="sxs-lookup"><span data-stu-id="58584-123">Language detection</span></span>
<span data-ttu-id="58584-124">API는 검색된 언어 및 0에서 1 사이의 숫자 점수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="58584-125">점수가 1에 가까울수록 식별된 언어가 true라는 100% 확실성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58584-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="58584-126">총 120개의 언어가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="58584-127">토픽 검색</span><span class="sxs-lookup"><span data-stu-id="58584-127">Topic detection</span></span>
<span data-ttu-id="58584-128">새로 발표된 API이며 제출된 텍스트 레코드 목록에 대해 검색된 상위 토픽을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="58584-129">토픽은 핵심 문구로 식별되며 하나 이상의 관련 단어를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="58584-130">이 API는 제출되는 텍스트 레코드 수가 100개 이상 필요하지만 수백 개에서 수천 개의 레코드에서 토픽을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="58584-131">이 API는 제출된 텍스트 레코드당 하나의 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="58584-132">이 API는 리뷰와 사용자 피드백 등 짧고 직접 작성한 텍스트 사용 시 더 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="58584-133">API 정의</span><span class="sxs-lookup"><span data-stu-id="58584-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="58584-134">헤더</span><span class="sxs-lookup"><span data-stu-id="58584-134">Headers</span></span>
<span data-ttu-id="58584-135">다음과 같이 요청에 올바른 헤더가 포함되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="58584-136">[Azure 데이터 마켓](https://datamarket.azure.com/account/keys)에서 계정의 계정 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="58584-137">현재는 JSON의 경우에만 입력 및 출력 형식이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="58584-138">XML은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="58584-139">단일 응답 API</span><span class="sxs-lookup"><span data-stu-id="58584-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="58584-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="58584-140">GetSentiment</span></span>
<span data-ttu-id="58584-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="58584-142">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-142">**Example request**</span></span>

<span data-ttu-id="58584-143">아래 호출에서는 "Hello World"라는 문구에 대한 정서 분석을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="58584-144">그러면 다음과 같이 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="58584-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="58584-145">GetKeyPhrases</span></span>
<span data-ttu-id="58584-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="58584-147">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-147">**Example request**</span></span>

<span data-ttu-id="58584-148">아래 호출에서는 "It was a wonderful hotel to stay at, with unique decor and friendly staff" 텍스트에 있는 핵심 문구를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="58584-149">그러면 다음과 같이 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="58584-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="58584-150">GetLanguage</span></span>
<span data-ttu-id="58584-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="58584-152">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-152">**Example request**</span></span>

<span data-ttu-id="58584-153">아래 호출에서는 *Hello World*</span><span class="sxs-lookup"><span data-stu-id="58584-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="58584-154">그러면 다음과 같이 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="58584-155">**선택적 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="58584-155">**Optional parameters**</span></span>

<span data-ttu-id="58584-156">`NumberOfLanguagesToDetect` 는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="58584-157">기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="58584-158">배치 API</span><span class="sxs-lookup"><span data-stu-id="58584-158">Batch APIs</span></span>
<span data-ttu-id="58584-159">텍스트 분석 서비스를 통해 배치 모드에서 정서 및 키 구문 추출 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="58584-160">점수가 매겨진 각 레코드는 하나의 트랜잭션으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="58584-161">예를 들어 단일 호출에서 1000개의 레코드에 대한 정서를 요청하면 1000개의 트랜잭션이 공제됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="58584-162">시스템에 입력한 ID가 시스템에서 반환한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="58584-163">웹 서비스는 이러한 ID가 고유한지 검사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="58584-164">호출자가 고유성을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="58584-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="58584-165">GetSentimentBatch</span></span>
<span data-ttu-id="58584-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="58584-167">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-167">**Example request**</span></span>

<span data-ttu-id="58584-168">아래 POST 호출에서는 요청 본문에 있는 "Hello World", "Hello Foo World", "Hello My World" 문구에 대한 정서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="58584-169">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="58584-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="58584-170">아래 응답에서 텍스트 ID와 연결된 점수 목록을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="58584-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="58584-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="58584-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="58584-173">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-173">**Example request**</span></span>

<span data-ttu-id="58584-174">이 예제에서는 다음 텍스트의 핵심 문구에 대한 정서 목록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="58584-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span><span class="sxs-lookup"><span data-stu-id="58584-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="58584-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="58584-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="58584-177">"The traffic was terrible, I spent three hours going to the airport"</span><span class="sxs-lookup"><span data-stu-id="58584-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="58584-178">다음 요청은 끝점에 대한 POST 호출로 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="58584-179">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="58584-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="58584-180">아래 응답에서 텍스트 ID와 연결된 핵심 문구 목록을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="58584-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="58584-181">GetLanguageBatch</span></span>

<span data-ttu-id="58584-182">아래의 POST 호출에서는 두 텍스트 입력에 대한 언어 검색을 요청하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="58584-183">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="58584-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="58584-184">그러면 다음 응답이 반환되는데 첫 번째 입력에서 영어가 검색되고 두 번째 입력에서 프랑스어가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="58584-185">토픽 검색 API</span><span class="sxs-lookup"><span data-stu-id="58584-185">Topic Detection APIs</span></span>
<span data-ttu-id="58584-186">새로 발표된 API이며 제출된 텍스트 레코드 목록에 대해 검색된 상위 토픽을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="58584-187">토픽은 핵심 문구로 식별되며 하나 이상의 관련 단어를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="58584-188">이 API는 제출된 텍스트 레코드당 하나의 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="58584-189">이 API는 제출되는 텍스트 레코드 수가 100개 이상 필요하지만 수백 개에서 수천 개의 레코드에서 토픽을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="58584-190">토픽 - 작업 제출</span><span class="sxs-lookup"><span data-stu-id="58584-190">Topics – Submit job</span></span>
<span data-ttu-id="58584-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="58584-192">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-192">**Example request**</span></span>

<span data-ttu-id="58584-193">아래 POST 호출에서는 100개 문서 집합에 대해 토픽을 요청하여 첫 번째 및 마지막 입력 문서를 표시하고 두 개의 StopPhrases를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="58584-194">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="58584-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="58584-195">아래 응답에서 제출된 작업에 대한 JobId를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="58584-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="58584-196">토픽으로 반환할 수 없는 한 단어 또는 여러 단어 문구의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="58584-197">매우 일반적인 토픽을 필터링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="58584-198">예를 들어 호텔 리뷰에 대한 데이터 집합에서 "호텔" 및 "호스텔"은 합리적인 중지 문구가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="58584-199">토픽 - 작업 결과에 대한 설문 조사</span><span class="sxs-lookup"><span data-stu-id="58584-199">Topics – Poll for job results</span></span>
<span data-ttu-id="58584-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="58584-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="58584-201">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="58584-201">**Example request**</span></span>

<span data-ttu-id="58584-202">'작업 제출' 단계에서 반환된 JobId를 전달하여 결과를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="58584-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="58584-203">응답에 Status='Complete'가 표시될 때까지 1분마다 이 끝점을 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="58584-204">한 작업을 완료하는 데 약 10분의 시간이 소요되며 레코드 수가 수천 개인 작업의 경우 더 오랜 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="58584-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="58584-205">처리하는 동안 다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58584-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="58584-206">API는 다음과 같은 형식의 JSON 형식으로 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="58584-206">The API returns output in JSON format in the following format:</span></span>

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


<span data-ttu-id="58584-207">응답의 각 부분에 대한 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="58584-208">**TopicInfo 속성**</span><span class="sxs-lookup"><span data-stu-id="58584-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="58584-209">키</span><span class="sxs-lookup"><span data-stu-id="58584-209">Key</span></span> | <span data-ttu-id="58584-210">설명</span><span class="sxs-lookup"><span data-stu-id="58584-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="58584-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="58584-211">TopicId</span></span> |<span data-ttu-id="58584-212">각 토픽에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="58584-213">Score</span><span class="sxs-lookup"><span data-stu-id="58584-213">Score</span></span> |<span data-ttu-id="58584-214">토픽에 할당된 레코드 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="58584-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="58584-215">KeyPhrase</span></span> |<span data-ttu-id="58584-216">토픽에 대한 요약 단어 또는 구입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="58584-217">한 단어 또는 여러 단어가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="58584-218">**TopicAssignment 속성**</span><span class="sxs-lookup"><span data-stu-id="58584-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="58584-219">키</span><span class="sxs-lookup"><span data-stu-id="58584-219">Key</span></span> | <span data-ttu-id="58584-220">설명</span><span class="sxs-lookup"><span data-stu-id="58584-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="58584-221">Id</span><span class="sxs-lookup"><span data-stu-id="58584-221">Id</span></span> |<span data-ttu-id="58584-222">레코드에 대한 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-222">Identifier for the record.</span></span> <span data-ttu-id="58584-223">입력에 포함된 ID와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58584-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="58584-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="58584-224">TopicId</span></span> |<span data-ttu-id="58584-225">레코드가 할당된 토픽 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="58584-226">Distance</span><span class="sxs-lookup"><span data-stu-id="58584-226">Distance</span></span> |<span data-ttu-id="58584-227">레코드가 토픽에 속할 신뢰도입니다.</span><span class="sxs-lookup"><span data-stu-id="58584-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="58584-228">Distance가 0에 가까울수록 신뢰도가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="58584-228">Distance closer to zero indicates higher confidence.</span></span> |

