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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="b05b3-103">기계 학습 API: 정서, 핵심 구문 추출, 언어 검색 및 토픽 검색을 위한 텍스트 분석</span><span class="sxs-lookup"><span data-stu-id="b05b3-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="b05b3-104">이 가이드는 hello API의 버전 1에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="b05b3-105">버전 2, [ **toothis 문서 참조**](../cognitive-services/cognitive-services-text-analytics-quick-start.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="b05b3-106">버전 2이이 API의 기본 버전 hello 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="b05b3-107">개요</span><span class="sxs-lookup"><span data-stu-id="b05b3-107">Overview</span></span>
<span data-ttu-id="b05b3-108">hello 텍스트 분석 API는 텍스트 분석의 제품군 [웹 서비스](https://datamarket.azure.com/dataset/amla/text-analytics) Azure 기계 학습을 사용 하 여 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="b05b3-109">hello API 사용된 tooanalyze 수 감성 분석, 키 구 추출, 언어 검색 및 항목 검색 등의 작업에 대 한 구조화 되지 않은 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="b05b3-110">데이터는 교육 없습니다 필요한 toouse이이 API: 방금 텍스트 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="b05b3-111">이 API는 고급 언어 처리 기술 toodeliver 가장 클래스 예측에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="b05b3-112">텍스트 분석 작업에서에서 확인할 수 있습니다이 [데모 사이트](https://text-analytics-demo.azurewebsites.net/)또한을 찾을 수 있는, [샘플](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) 방법에 C# 및 Python tooimplement 텍스트 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="b05b3-113">정서 분석</span><span class="sxs-lookup"><span data-stu-id="b05b3-113">Sentiment analysis</span></span>
<span data-ttu-id="b05b3-114">hello API는 0 및 1 사이의 점수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="b05b3-115">점수 닫기 too1 점수 닫기 too0 음수 인지를 나타내는 반면 긍정적인 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="b05b3-116">정서 점수는 분류 기술을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="b05b3-117">hello 입력된 기능 toohello 분류자 n 그램, 음성 부분 태그 및 포함 된 word에서 생성 된 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="b05b3-118">현재 영어는 hello 언어 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="b05b3-119">핵심 문구 추출</span><span class="sxs-lookup"><span data-stu-id="b05b3-119">Key phrase extraction</span></span>
<span data-ttu-id="b05b3-120">hello API hello 제안에서에서 요점 hello 입력된 텍스트를 나타내는 문자열 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="b05b3-121">Microsoft Office의 정교한 자연어 처리 도구 키트에서 제공되는 기술을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="b05b3-122">현재 영어는 hello 언어 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="b05b3-123">언어 검색</span><span class="sxs-lookup"><span data-stu-id="b05b3-123">Language detection</span></span>
<span data-ttu-id="b05b3-124">hello API hello 검색 언어 및 0 및 1 사이의 점수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="b05b3-125">점수 닫기 too1 100% 확신도 식별 하는 hello 언어 true 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="b05b3-126">총 120개의 언어가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="b05b3-127">토픽 검색</span><span class="sxs-lookup"><span data-stu-id="b05b3-127">Topic detection</span></span>
<span data-ttu-id="b05b3-128">제출 된 텍스트 레코드 목록에 대 한 hello 최상위 검색 된 항목을 반환 하는 새로 출시 된 API입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="b05b3-129">토픽은 핵심 문구로 식별되며 하나 이상의 관련 단어를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="b05b3-130">이 API에서는 100 텍스트의 최소 제출 toobe를 기록 하는 수백 디자인 된 toodetect 항목은 레코드의 toothousands 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="b05b3-131">이 API는 제출된 텍스트 레코드당 하나의 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="b05b3-132">hello API는 검토와 사용자에 게 피드백 등의 텍스트를 작성 하는 short, 인적에 대 한 잘 설계 된 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="b05b3-133">API 정의</span><span class="sxs-lookup"><span data-stu-id="b05b3-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="b05b3-134">헤더</span><span class="sxs-lookup"><span data-stu-id="b05b3-134">Headers</span></span>
<span data-ttu-id="b05b3-135">Hello 올바른 헤더, 다음과 같이 있어야 하 고 요청에 포함 하 고 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="b05b3-136">Hello에서 계정에서 계정 키를 찾을 수 있습니다 [Azure 데이터 마켓](https://datamarket.azure.com/account/keys)합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="b05b3-137">현재는 JSON의 경우에만 입력 및 출력 형식이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="b05b3-138">XML은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="b05b3-139">단일 응답 API</span><span class="sxs-lookup"><span data-stu-id="b05b3-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="b05b3-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="b05b3-140">GetSentiment</span></span>
<span data-ttu-id="b05b3-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="b05b3-142">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-142">**Example request**</span></span>

<span data-ttu-id="b05b3-143">아래 hello 호출 감성 분석 hello 구 "Hello World"에 대 한 요청:</span><span class="sxs-lookup"><span data-stu-id="b05b3-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="b05b3-144">그러면 다음과 같이 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="b05b3-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="b05b3-145">GetKeyPhrases</span></span>
<span data-ttu-id="b05b3-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="b05b3-147">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-147">**Example request**</span></span>

<span data-ttu-id="b05b3-148">Hello 호출 아래에서 키 구를 hello 문제를 발견 hello 텍스트에 ", 고유 장식 및 친숙 한 직원 훌륭한 호텔 toostay" 요청 하는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="b05b3-149">그러면 다음과 같이 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="b05b3-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="b05b3-150">GetLanguage</span></span>
<span data-ttu-id="b05b3-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="b05b3-152">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-152">**Example request**</span></span>

<span data-ttu-id="b05b3-153">아래 hello GET 호출에서 hello 텍스트에서 키 구 hello에 대 한 hello 의미에 대 한 요청 하는 것 *Hello World*</span><span class="sxs-lookup"><span data-stu-id="b05b3-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="b05b3-154">그러면 다음과 같이 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="b05b3-155">**선택적 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="b05b3-155">**Optional parameters**</span></span>

<span data-ttu-id="b05b3-156">`NumberOfLanguagesToDetect` 는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="b05b3-157">hello 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="b05b3-158">배치 API</span><span class="sxs-lookup"><span data-stu-id="b05b3-158">Batch APIs</span></span>
<span data-ttu-id="b05b3-159">hello 텍스트 분석 서비스 toodo 감성 및 키 구 추출 일괄 처리 모드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="b05b3-160">하나의 트랜잭션으로 점수가 매겨진 각 hello 레코드 개수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="b05b3-161">예를 들어 단일 호출에서 1000개의 레코드에 대한 정서를 요청하면 1000개의 트랜잭션이 공제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="b05b3-162">Hello Id hello 시스템에 입력 하는 hello Id hello 시스템에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="b05b3-163">hello 웹 서비스는 이러한 Id는 고유한 것을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="b05b3-164">hello hello 호출자 tooverify 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="b05b3-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="b05b3-165">GetSentimentBatch</span></span>
<span data-ttu-id="b05b3-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="b05b3-167">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-167">**Example request**</span></span>

<span data-ttu-id="b05b3-168">hello POST 호출 아래 hello 표현의 hello 구 "Hello World", "Foo World Hello" 및 "내의 Hello World" hello hello 요청 본문에 대 한 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="b05b3-169">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="b05b3-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="b05b3-170">아래 hello 응답에서 텍스트 Id와 연결 된 점수 hello 목록이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="b05b3-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="b05b3-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="b05b3-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="b05b3-173">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-173">**Example request**</span></span>

<span data-ttu-id="b05b3-174">이 예제에서는 텍스트를 다음 hello에서 키 구 hello에 대 한 표현의 목록은 hello에 대 한 요청 하는 것:</span><span class="sxs-lookup"><span data-stu-id="b05b3-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="b05b3-175">", 고유 장식 및 친숙 한 직원 훌륭한 호텔 toostay 했습니다"</span><span class="sxs-lookup"><span data-stu-id="b05b3-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="b05b3-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="b05b3-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="b05b3-177">"hello 트래픽 찍 했, toohello 공항 라인으로 전환 하는 3 시간을 투자"</span><span class="sxs-lookup"><span data-stu-id="b05b3-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="b05b3-178">이 요청은 POST 호출 toohello 끝점으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="b05b3-179">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="b05b3-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="b05b3-180">아래 hello 응답에서 텍스트 Id와 연결 된 키 구 hello 목록이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="b05b3-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="b05b3-181">GetLanguageBatch</span></span>

<span data-ttu-id="b05b3-182">Hello POST 호출 아래에 두 개의 텍스트 입력에 대 한 언어 검색 요청:</span><span class="sxs-lookup"><span data-stu-id="b05b3-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="b05b3-183">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="b05b3-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="b05b3-184">Hello 다음 응답으로 hello 두 번째 입력의 첫 번째 입력이 hello 및 프랑스어에서 영어 발견 되는 위치를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="b05b3-185">토픽 검색 API</span><span class="sxs-lookup"><span data-stu-id="b05b3-185">Topic Detection APIs</span></span>
<span data-ttu-id="b05b3-186">제출 된 텍스트 레코드 목록에 대 한 hello 최상위 검색 된 항목을 반환 하는 새로 출시 된 API입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="b05b3-187">토픽은 핵심 문구로 식별되며 하나 이상의 관련 단어를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="b05b3-188">이 API는 제출된 텍스트 레코드당 하나의 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="b05b3-189">이 API에서는 100 텍스트의 최소 제출 toobe를 기록 하는 수백 디자인 된 toodetect 항목은 레코드의 toothousands 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="b05b3-190">토픽 - 작업 제출</span><span class="sxs-lookup"><span data-stu-id="b05b3-190">Topics – Submit job</span></span>
<span data-ttu-id="b05b3-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="b05b3-192">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-192">**Example request**</span></span>

<span data-ttu-id="b05b3-193">아래 hello POST 호출에서 여러 여기서 hello 이름과 성을 입력가 표시 되는 문서 및 두 StopPhrases 포함 하는 100 문서에 대 한 항목이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="b05b3-194">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="b05b3-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="b05b3-195">아래 hello 응답에서 hello 제출 된 작업에 대 한 hello를 JobId를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="b05b3-196">토픽으로 반환할 수 없는 한 단어 또는 여러 단어 문구의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="b05b3-197">매우 일반적인 항목을 사용 하는 toofilter 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="b05b3-198">예를 들어 호텔 리뷰에 대한 데이터 집합에서 "호텔" 및 "호스텔"은 합리적인 중지 문구가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="b05b3-199">토픽 - 작업 결과에 대한 설문 조사</span><span class="sxs-lookup"><span data-stu-id="b05b3-199">Topics – Poll for job results</span></span>
<span data-ttu-id="b05b3-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="b05b3-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="b05b3-201">**예제 요청**</span><span class="sxs-lookup"><span data-stu-id="b05b3-201">**Example request**</span></span>

<span data-ttu-id="b05b3-202">JobId hello '전송 작업' 단계 toofetch hello 결과에서 반환 된 hello를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="b05b3-203">호출 하는이 끝점 상태가 될 때까지 1 분 마다 권장 = hello 응답에 '완료'입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="b05b3-204">작업 toocomplete 이상 동안 수천 개의 레코드를 사용 하 여 작업에 대 한 약 10 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="b05b3-205">처리 하는 동안 hello 응답은 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="b05b3-206">hello API 형식에 따라 hello에 대 한 JSON 형식으로 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="b05b3-207">hello 응답의 각 부분에 대 한 hello 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="b05b3-208">**TopicInfo 속성**</span><span class="sxs-lookup"><span data-stu-id="b05b3-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="b05b3-209">키</span><span class="sxs-lookup"><span data-stu-id="b05b3-209">Key</span></span> | <span data-ttu-id="b05b3-210">설명</span><span class="sxs-lookup"><span data-stu-id="b05b3-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b05b3-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="b05b3-211">TopicId</span></span> |<span data-ttu-id="b05b3-212">각 토픽에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="b05b3-213">Score</span><span class="sxs-lookup"><span data-stu-id="b05b3-213">Score</span></span> |<span data-ttu-id="b05b3-214">레코드의 수가 tootopic를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="b05b3-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="b05b3-215">KeyPhrase</span></span> |<span data-ttu-id="b05b3-216">요약 단어 또는 구를 hello 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="b05b3-217">한 단어 또는 여러 단어가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="b05b3-218">**TopicAssignment 속성**</span><span class="sxs-lookup"><span data-stu-id="b05b3-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="b05b3-219">키</span><span class="sxs-lookup"><span data-stu-id="b05b3-219">Key</span></span> | <span data-ttu-id="b05b3-220">설명</span><span class="sxs-lookup"><span data-stu-id="b05b3-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b05b3-221">Id</span><span class="sxs-lookup"><span data-stu-id="b05b3-221">Id</span></span> |<span data-ttu-id="b05b3-222">Hello 레코드에 대 한 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-222">Identifier for hello record.</span></span> <span data-ttu-id="b05b3-223">Hello 입력에 포함 된 toohello ID를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="b05b3-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="b05b3-224">TopicId</span></span> |<span data-ttu-id="b05b3-225">hello 항목 ID는 hello 레코드에 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="b05b3-226">Distance</span><span class="sxs-lookup"><span data-stu-id="b05b3-226">Distance</span></span> |<span data-ttu-id="b05b3-227">신뢰도 hello 레코드 속해 toohello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="b05b3-228">거리 자세히 toozero에 더 높은 신뢰 수준을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b05b3-228">Distance closer toozero indicates higher confidence.</span></span> |

