---
title: "Azure Data Lake 분석 U-SQL Cognitive 기능 aaaUsing | Microsoft Docs"
description: "Toouse U-SQL에 Cognitive 기능의 intelligence hello 하는 방법에 대해 알아봅니다"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: 2c9ac71f490e929070fa0e72b93c3ffdb1ab243b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-hello-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="3dcce-103">자습서: U-SQL의 hello Cognitive 기능 시작</span><span class="sxs-lookup"><span data-stu-id="3dcce-103">Tutorial: Get started with hello Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="3dcce-104">U-SQL에 대 한 cognitive 기능 개발자 toouse intelligence 빅 데이터 프로그램에서 put을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-104">Cognitive capabilities for U-SQL enable developers toouse put intelligence in their big data programs.</span></span> <span data-ttu-id="3dcce-105">단순에서 전체 프로세스를 hello:</span><span class="sxs-lookup"><span data-stu-id="3dcce-105">hello overall process in simple:</span></span>

* <span data-ttu-id="3dcce-106">U-SQL 스크립트 hello에 대 한 hello 참조 어셈블리 문을 tooenable hello 인식 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-106">Use hello REFERENCE ASSEMBLY statement tooenable hello cognitive features for hello U-SQL Script</span></span>
* <span data-ttu-id="3dcce-107">Toouse hello Cognitive 기능 hello 프로세스 작업 호출</span><span class="sxs-lookup"><span data-stu-id="3dcce-107">Call hello PROCESS operation toouse hello Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="3dcce-108">이미징 시나리오</span><span class="sxs-lookup"><span data-stu-id="3dcce-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="3dcce-109">예: 이미지 태그 지정</span><span class="sxs-lookup"><span data-stu-id="3dcce-109">Example: Image tagging</span></span>

<span data-ttu-id="3dcce-110">다음 예제는 hello 이미지에 기능 toodetect 개체 이미징 hello는 종단 간 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-110">hello following example shows an end-to-end use of hello imaging capabilities toodetect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract hello number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="3dcce-111">사람 얼굴에서 감정을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="3dcce-112">사람 얼굴에서 연령 및 성별을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="3dcce-113">이미지 (OCR)에 있는 텍스트를 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="3dcce-114">텍스트 시나리오</span><span class="sxs-lookup"><span data-stu-id="3dcce-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="3dcce-115">데이터 입력</span><span class="sxs-lookup"><span data-stu-id="3dcce-115">Input data</span></span>

<span data-ttu-id="3dcce-116">레프 톨스토이의 "전쟁과 평화"로 구성된 입력이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="3dcce-117">각 단락에 대한 핵심 문구 추출</span><span class="sxs-lookup"><span data-stu-id="3dcce-117">Extract key phrases for each paragraph</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize hello key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="3dcce-118">각 단락에서 감정 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3dcce-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

