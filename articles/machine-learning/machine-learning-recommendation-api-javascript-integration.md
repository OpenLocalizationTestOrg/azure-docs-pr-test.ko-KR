---
title: "Machine Learning 권장 사항: JavaScript 통합 | Microsoft Docs"
description: "Azure Machine Learning 권장 사항 - JavaScript 통합 - 설명서"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Azure 기계 학습 권장 사항 - JavaScript 통합
> [!NOTE]
> 이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다. hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다. 일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.
> 에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)
> 
> 

이 문서를 보여 주는 방법을 toointegrate JavaScript를 사용 하 여 사이트입니다. hello JavaScript를 사용 하면 toosend 데이터 취득 이벤트 및 tooconsume 권장 사항 추천 모델을 작성 한 후입니다. JS를 통해 수행하는 모든 작업은 서버 쪽에서도 수행할 수 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. 일반 개요
Azure ML 권장 사항과 사이트를 통합하는 과정은 다음 두 단계로 이루어집니다.

1. Azure ML 권장 사항으로 이벤트를 전송합니다. 이렇게 하면 toobuild 추천 모델입니다.
2. Hello 권장 사항을 사용 합니다. Hello 모델의 빌드 후 hello 권장 사항을 사용할 수 있습니다. (이 문서의 설명 하지 않습니다 방법을 toobuild 모델을 읽을 hello 퀵 스타트 가이드 tooget 방법은).

<ins>I단계</ins>

Hello 수 있도록 하는 작은 JavaScript 라이브러리를 html 페이지에 삽입 하는 첫 번째 단계 (데이터 마켓)를 통해 Azure ML 권장 사항을 서버에 hello html 페이지에 나타나는 순서 대로 페이지 toosend 이벤트를 hello:

![Drawing1][1]

<ins>II단계</ins>

Hello에 hello 페이지 tooshow hello 권장 구성 하려는 경우 두 번째 단계 중 하나를 선택 hello 다음 옵션:

1. (페이지 렌더링의 hello 단계)의 서버 (데이터 마켓)를 통해 Azure ML 권장 사항을 서버 tooget 권장 사항을 호출합니다. hello 결과 항목 id 목록이 포함 됩니다. 서버는 hello 항목 메타 데이터 (예: 이미지, 설명)를 사용 하 여 tooenrich hello 결과 되어야 하며 보낼 hello toohello 브라우저 페이지를 생성 합니다.

![Drawing2][2]

2. hello 다른 옵션은 toouse hello 작은 JavaScript 파일 단계 하나의 tooget 추천된 항목의 단순 목록입니다. 여기에 수신 hello 데이터는 hello 첫 번째 옵션에 hello 하나 보다 보다 간결 하 게 합니다.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. 필수 조건
1. Hello Api를 사용 하 여 새 모델을 만듭니다. 방법에 hello 빠른 시작 가이드를 참조 하십시오. toodo 것입니다.
2. &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt;를 base64로 인코딩합니다. (이 사용 hello 기본 인증 tooenable hello JS 코드 toocall hello Api에 대 한).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. JavaScript를 사용하여 데이터 취득 이벤트 전송
이벤트 전송을 원활 하는 단계를 수행 하는 hello:

1. JQuery 라이브러리를 코드에 포함합니다. Hello url에 nuget에서 다운로드할 수 있습니다.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Hello url에서 hello 권장 사항을 자바 스크립트 라이브러리를 포함: http://aka.ms/RecoJSLib1
3. Hello 적절 한 매개 변수를 사용 하 여 Azure ML 권장 라이브러리를 초기화 합니다.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. 송신 hello에 대 한 적절 한 이벤트입니다. 이벤트의 모든 형식에 대해 아래 세부 섹션을 참조하세요(클릭 이벤트의 예) <script> if (typeof AzureMLRecommendationsEvent==“undefined”) {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    제한 사항 및 브라우저 지원
참조 구현이며, 있는 그대로 제공됩니다. 모든 주요 브라우저를 지원합니다.

### <a name="32----type-of-events"></a>3.2.    이벤트 형식
형식은 5 개 이벤트 라이브러리 지원 hello: 쇼핑 카트 및 구매에서 클릭, 권장 사항을 클릭 제거 tooShop 카트에 추가 합니다. 컨텍스트가 사용 되는 tooset hello 사용자 로그인을 호출 하는 추가 이벤트가 있습니다.

#### <a name="321-click-event"></a>3.2.1. Click 이벤트
이 이벤트는 사용자가 항목을 클릭할 때마다 사용해야 합니다. Hello 항목 세부 정보;로 새 페이지를 연 사용자가 항목을 클릭할 때 일반적으로 이 페이지에이 이벤트가 트리거되어 야 합니다.

매개 변수

* event(문자열, 필수) - "click"
* 항목 (문자열, 필수)-hello 항목의 고유 식별자
* 항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름
* itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명
* itemCategory (문자열, 선택 사항)-hello hello 항목 범주
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

또는 선택적 데이터를 포함합니다.

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Recommendation Click 이벤트
이 이벤트는 사용자가 Azure ML 권장 사항에서 권장 항목으로 받은 항목을 클릭할 때마다 사용해야 합니다. Hello 항목 세부 정보;로 새 페이지를 연 사용자가 항목을 클릭할 때 일반적으로 이 페이지에이 이벤트가 트리거되어 야 합니다.

매개 변수

* event(문자열, 필수) - "recommendationclick"
* 항목 (문자열, 필수)-hello 항목의 고유 식별자
* 항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름
* itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명
* itemCategory (문자열, 선택 사항)-hello hello 항목 범주
* 초기값 (문자열 배열, 선택 사항)-hello 초기값 hello 권장 사항 쿼리를 생성 합니다.
* (문자열 배열, 선택 사항)-recoList hello hello 클릭 된 항목을 생성 하는 hello 권장 요청의 결과입니다.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

또는 선택적 데이터를 포함합니다.

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Add Shopping Cart 이벤트
이 이벤트를 사용 해야 hello 사용자 쇼핑 카트는 항목 toohello를 추가 하는 경우.
매개 변수

* event(문자열, 필수) - "addshopcart"
* 항목 (문자열, 필수)-hello 항목의 고유 식별자
* 항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름
* itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명
* itemCategory (문자열, 선택 사항)-hello hello 항목 범주
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Remove Shopping Cart 이벤트
Hello 사용자 toohello 쇼핑 카트에 항목을 제거 하는 경우이 이벤트를 사용 해야 합니다.

매개 변수

* event(문자열, 필수) - "removeshopcart"
* 항목 (문자열, 필수)-hello 항목의 고유 식별자
* 항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름
* itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명
* itemCategory (문자열, 선택 사항)-hello hello 항목 범주
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Purchase 이벤트
Hello 사용자의 쇼핑 카트를 구매할 때이 이벤트를 사용 해야 합니다.

매개 변수

* event(문자열) – "purchase"
* items(Purchased) – 구매한 각 항목에 대한 항목이 저장되는 배열<br><br>
  Purchased 형식:
  * 항목 (string)-hello 항목의 고유 식별자입니다.
  * count(정수 또는 문자열) – 구매한 항목 수
  * 가격 (float 또는 문자열)-선택적 필드-hello 가격 hello 항목의 합니다.

3 구매 되는 hello 코드 항목 (33, 34, 35) 2 대와 모든 필드가 채워집니다 (항목, count, 가격)과 (항목 34) 없는 가격입니다.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. User Login 이벤트
Azure ML 권장 사항을 이벤트 라이브러리를 만듭니다 및에서 제공 된 순서 tooidentify 이벤트에서 쿠키를 사용 하 여 같은 브라우저를 hello 합니다. 순서 tooimprove hello 모델의 결과 Azure ML 권장 사항을 tooset을 hello 쿠키 사용을 재정의 하는 사용자 고유 id를 수 있습니다.

Hello 사용자 로그인 tooyour 사이트 후이 이벤트를 사용할 수 있습니다.

매개 변수

* event(문자열) – "userlogin"
* 사용자 (string)-hello 사용자의 고유 id입니다.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. JavaScript 통해 권장 사항 사용
hello 추천을 사용 하는 hello 코드 hello 클라이언트의 웹 페이지에서 일부 JavaScript 이벤트에 의해 트리거됩니다. hello 권장 응답에는 권장 항목 Id, 이름 및 해당 등급 hello 포함 됩니다. 것이 가장 좋은 toouse hello 서버 쪽 통합에서 hello 추천 항목 보다 복잡 한 처리 (예: hello 항목의 메타 데이터 추가)의 목록 표시 하는 데에이 옵션을 완료 해야 합니다.

### <a name="41-consume-recommendations"></a>4.1 권장 사항 사용
tooconsume 권장 사항을 tooinclude hello 필요 페이지 및 toocall AzureMLRecommendationsStart JavaScript 라이브러리를 필요 합니다. 섹션 2를 참조하세요.

메서드를 호출 하는 toocall 필요 하나 이상의 항목에 대 한 권장 사항을 tooconsume: AzureMLRecommendationsGetI2IRecommendation 합니다.

매개 변수

* (문자열의 배열)-에 대 한 하나 이상의 항목 tooget 권장 항목합니다. Fbt 빌드를 사용하는 경우 하나의 항목만 설정할 수 있습니다.
* numberOfResults(int) – 필요한 결과 수
* (부울, 선택 사항)-includeMetadata 경우 too'true 설정 ' hello 결과에 해당 hello 메타 데이터 필드를 채워야 나타냅니다.
* 처리 기능-hello 권장 사항을 처리 하는 함수 반환 됩니다. hello 데이터의 배열로 반환 됩니다.
  * Item - 항목의 고유 ID
  * name – 항목 이름(카탈로그에 있는 경우)
  * rating - 권장 사항 등급
  * 메타 데이터-hello 항목의 hello 메타 데이터를 나타내는 문자열

예: 코드 다음 hello 요청 "64f6eb0d-947a-4c18-a16c-888da9e228ba" 항목에 대 한 8 권장 사항 (및 지정 하 여 includeMetadata-암시적으로 표시 메타 데이터가 필요 하다), 다음 버퍼에 hello 결과 연결 합니다.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
