---
title: "Azure 논리 앱에 통합 하는 함수 aaaCreate | Microsoft Docs"
description: "Azure 논리 앱 및 Azure Cognitive 서비스 toocategorize 윗 의미와 통합 하는 함수를 만들고 감성 나쁘지 경우 알림을 보내도록 합니다."
services: functions, logic-apps, cognitive-services
keywords: "워크플로, 클라우드 앱, 클라우드 서비스, 비즈니스 프로세스, 시스템 통합, Enterprise Application Integration, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Azure Logic Apps와 통합하는 함수 만들기

Azure 논리 앱 azure 함수 hello 논리 앱 디자이너에에서 통합 됩니다. 이러한 통합에는 오케스트레이션에 서 다른 Azure 및 타사 서비스와 함수의 컴퓨팅 hello를 사용할 수 있습니다. 

이 자습서에서는 toouse Twitter 게시물에서 논리 앱 및 Azure Cognitive 서비스 tooanalyze 의미와 어떻게 작동 합니다. 트리거된 HTTP 함수 트 윗 녹색, 노랑 또는 빨강 hello 감성 점수를 기준으로 분류 합니다. 불량 감정이 감지되면 전자 메일이 전송됩니다. 

![논리 앱 디자이너에서 앱의 처음 2단계를 보여 주는 이미지](media/functions-twitter-email/designer1.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Cognitive Services 계정을 만듭니다.
> * 트윗 감정을 분류하는 함수를 만듭니다.
> * TooTwitter 연결 하는 논리 앱을 만듭니다.
> * 감성 검색 toohello 논리 앱을 추가 합니다. 
> * Hello 논리 앱 toohello 함수를 연결 합니다.
> * Hello 함수에서 hello 응답에 따라 전자 메일을 보냅니다.

## <a name="prerequisites"></a>필수 조건

+ 활성 [Twitter](https://twitter.com/) 계정. 
+ [Outlook.com](https://outlook.com/) 계정(알림 전송용).
+ 이 항목에서 만든의 시작 지점 hello 자원으로 사용 하 여 [hello Azure 포털에서에서 첫 번째 사용자 함수를 만들어](functions-create-first-azure-function.md)합니다.  
그렇게 이미 하지 않은 경우 이러한 단계 지금 toocreate 함수 앱을 완료 합니다.

## <a name="create-a-cognitive-services-account"></a>Cognitive Services 계정 만들기

Cognitive 서비스 계정은 모니터링 되는 트 윗의 필요한 toodetect hello 인지를 나타냅니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.

2. Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

3. **데이터 + 분석** > **Cognitive Services**를 클릭합니다. 그런 다음 hello 설정으로 사용 hello 테이블에 지정 된 hello 조건에 동의 하 고 확인 **Pin toodashboard**합니다.

    ![Cognitive 계정 만들기 블레이드](media/functions-twitter-email/cog_svcs_account.png)

    | 설정      |  제안 값   | 설명                                        |
    | --- | --- | --- |
    | **Name** | MyCognitiveServicesAccnt | 고유한 계정 이름을 선택합니다. |
    | **API 형식** | Text Analytics API | API는 tooanalyze 텍스트를 사용 합니다.  |
    | **위치**: | 미국 서부 | 현재 텍스트 분석은 **미국 서부**만 사용할 수 있습니다. |
    | **가격 책정 계층** | F0 | 가장 낮은 계층 hello로 시작 합니다. 호출 부족 하면 tooa 상위 계층의 크기를 조정 합니다.|
    | **리소스 그룹** | myResourceGroup | 사용 하 여 hello 동일이 자습서의 모든 서비스에 대 한 리소스 그룹입니다.|

4. 클릭 **만들기** toocreate 계정. Hello 계정을 만든 후 새 Cognitive 서비스 계정 toohello 고정 된 대시보드를 클릭 합니다. 

5. Hello 계정에서 클릭 **키**의 hello 값을 복사 하 고 **키 1** 하 고 저장 합니다. 이 키 tooconnect hello 논리 앱 tooyour Cognitive 서비스 계정을 사용 합니다. 
 
    ![구성](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Hello 함수 만들기

함수는 좋은 방법 toooffload 논리 앱 워크플로 처리 작업을 제공 합니다. 이 자습서에서는 트리거된 HTTP 함수 tooprocess 윗 감성에서 점수를 인식 서비스 및 범주 값을 반환 합니다.  

1. 함수 앱 확장을 hello 클릭  **+**  너무 단추 옆**함수**, hello 클릭 **HTTPTrigger** 서식 파일입니다. 형식 `CategorizeSentiment` hello 함수에 대 한 **이름** 클릭 **만들기**합니다.

    ![함수 앱 블레이드, 함수 +](media/functions-twitter-email/add_fun.png)

2. Hello run.csx 파일의 내용을 hello hello 코드를 다음으로 대체 한 다음 클릭 **저장**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    이 함수 코드 hello 요청에서 받은 hello 감성 점수를 기준으로 색 범주를 반환 합니다. 

3. tootest hello 함수 클릭 **테스트** hello 맨 오른쪽 tooexpand hello 테스트 탭에 있습니다. 값을 입력 `0.2` hello에 대 한 **요청 본문**, 클릭 하 고 **실행**합니다. 값이 **빨간색** hello hello 응답 본문에 반환 됩니다. 

    ![Hello Azure 포털의에서 테스트 hello 함수](./media/functions-twitter-email/test.png)

이제 감정 점수를 분류하는 함수가 있습니다. 다음으로 Twitter 및 Cognitive Services 계정과 함수를 통합하는 논리 앱을 만듭니다. 

## <a name="create-a-logic-app"></a>논리 앱 만들기   

1. Hello Azure 포털에서 클릭 hello **새로 만들기** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2. **엔터프라이즈 통합** > **논리 앱**을 클릭합니다. 그런 다음 확인 서 hello 설정 사용 hello 테이블에 지정 된 **Pin toodashboard**를 클릭 하 고 **만들기**합니다.
 
4. 다음을 입력 한 **이름** 같은 `TweetSentiment`, hello 테이블에 지정 된 hello 설정을 사용 하 여 hello 조건에 동의 및 확인 **Pin toodashboard**합니다.

    ![Hello Azure 포털에서에서 논리 앱 만들기](./media/functions-twitter-email/new_logicApp.png)

    | 설정      |  제안 값   | 설명                                        |
    | ----------------- | ------------ | ------------- |
    | **Name** | TweetSentiment | 앱에 적절한 이름을 선택합니다. |
    | **리소스 그룹** | myResourceGroup | API는 tooanalyze 텍스트를 사용 합니다.  |
    | **위치**: | 미국 동부 | 위치 닫기 tooyou를 선택 합니다. |
    | **리소스 그룹** | myResourceGroup | 선택 이전과 같은 기존 리소스 그룹 hello 합니다.|

4. 클릭 **만들기** toocreate 논리 앱. Hello 앱을 만든 후 새 논리 앱 toohello 고정 된 대시보드를 클릭 합니다. 그런 다음 hello 논리 앱 디자이너에서에서 아래로 스크롤하여 하 고 hello 클릭 **빈 논리 앱** 템플릿. 

    ![빈 논리 앱 템플릿](media/functions-twitter-email/blank.png)

이제 hello 논리 앱 디자이너 tooadd 서비스 및 트리거 tooyour 앱을 사용할 수 있습니다.

## <a name="connect-tootwitter"></a>TooTwitter 연결

먼저 연결 tooyour Twitter 계정 만듭니다. 트 윗 hello 앱 toorun를 트리거하는 hello 논리 앱이 폴링합니다.

1. Hello 디자이너에서 클릭 hello **Twitter** 서비스를 마우스 클릭 hello **새 윗이 게시 될 때** 트리거. Tooyour Twitter 계정에에서 로그인 하 고 논리 앱 toouse 사용자 계정에 권한을 부여 합니다.

2. Hello 테이블에 지정 된 hello Twitter 트리거 설정을 사용 합니다. 

    ![Twitter 커넥터 설정](media/functions-twitter-email/azure_tweet.png)

    | 설정      |  제안 값   | 설명                                        |
    | ----------------- | ------------ | ------------- |
    | **검색 텍스트** | #Azure | Hello 선택한 간격에 toogenerate 새 트 윗에 대 한 충분 한 인기 있는 hashtag를 사용 합니다. Hello 무료 계층 및 사용자 hashtag 사용 하 여 너무 많이 사용 되 면 사용할 수 있습니다 신속 하 게 hello 트랜잭션을 Cognitive 서비스 계정에서. |
    | **Frequency(빈도)** | 분 | Twitter 폴링에 사용 되는 hello 빈도 단위입니다.  |
    | **간격** | 15 | 빈도 단위에서 Twitter 요청 간에 경과 된 hello 시간입니다. |

3.  클릭 **저장** tooconnect tooyour Twitter 계정. 

이제 앱에 연결 된 tooTwitter입니다. 다음으로, 수집 된 트 윗의 tootext 분석 toodetect hello 정서를 연결합니다.

## <a name="add-sentiment-detection"></a>감정 검색 추가

1. **새 단계**를 클릭한 다음 **작업 추가**를 선택합니다.

    ![새 단계 후 작업 추가](media/functions-twitter-email/new_step.png)

2. **동작 선택**, 클릭 **텍스트 분석**, hello를 클릭 한 다음 **감성 검색** 동작 합니다.

    ![감정 검색](media/functions-twitter-email/detect_sent.png)

3. 같은 연결 이름을 입력 `MyCognitiveServicesConnection`Cognitive 서비스를 저장 하는 계정에 대 한 hello 키를 붙여 넣고 클릭 **만들기**합니다.  

4. 클릭 **텍스트 tooanalyze** > **텍스트 윗**, 클릭 하 고 **저장**합니다.  

    ![감정 검색](media/functions-twitter-email/ds_tta.png)

감성 검색을 구성 했으므로 hello 감성 점수가 출력을 사용 하는 연결 tooyour 함수를 추가할 수 있습니다.

## <a name="connect-sentiment-output-tooyour-function"></a>연결 감성 출력 tooyour 함수

1. Hello 논리 앱 디자이너, 클릭 **새 단계** > **동작 추가**, 클릭 하 고 **Azure 함수**합니다. 

2. 클릭 **Azure 함수 선택**선택, hello **CategorizeSentiment** 앞에서 만든 함수입니다.  

    ![Azure 함수 선택을 보여 주는 Azure 함수 상자](media/functions-twitter-email/choose_fun.png)

3. **요청 본문**에서 **점수**, **저장**을 차례로 클릭합니다.

    ![Score](media/functions-twitter-email/trigger_score.png)

이제 함수 hello 논리 앱에서 감성 점수를 전송할 때 트리거됩니다. 색으로 구분 된 범주는 toohello 논리 앱 hello 함수에 의해 반환 됩니다. 다음으로 감성 값 보내는 전자 메일 알림을 추가 **빨간색** hello 함수에서 반환 합니다. 

## <a name="add-email-notifications"></a>전자 메일 알림 추가

hello 워크플로의 마지막 부분 hello hello 감성 점수로 때 tootrigger 전자 메일은 _빨간색_합니다. 이 항목에서는 Outlook.com 커넥터를 사용합니다. 유사한 단계 toouse Gmail 또는 Office 365 Outlook 커넥터를 수행할 수 있습니다.   

1. 논리 앱 디자이너 hello 클릭 **새 단계** > **조건 추가**합니다. 

2. **값 선택**을 클릭한 다음 **본문**을 클릭합니다. **같음**을 선택하고 **값 선택**을 클릭하고 `RED`를 입력하고 **저장**을 클릭합니다. 

    ![조건 toohello 논리 앱을 추가 합니다.](media/functions-twitter-email/condition.png)

3. **그러한 경우 아무 작업도 수행**, 클릭 **동작 추가**, 검색할 `outlook.com`, 클릭 **전자 메일 보내기**, tooyour Outlook.com 계정에에서 로그인 합니다.
    
    ![Hello 조건에 대 한 작업을 선택 합니다.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Outlook.com 계정이 없는 경우 Gmail 또는 Office 365 Outlook과 같은 다른 커넥터를 선택할 수 있습니다.

4. Hello에 **전자 메일 보내기** hello 테이블에 동작을 사용 하 여 hello 전자 메일 설정으로 지정 된 합니다. 

    ![Hello 송신 전자 메일 작업에 대 한 hello 전자 메일을 구성 합니다.](media/functions-twitter-email/sendemail.png)

    | 설정      |  제안 값   | 설명  |
    | ----------------- | ------------ | ------------- |
    | **To** | 메일 주소 입력 | hello 알림을 수신 하는 hello 전자 메일 주소입니다. |
    | **제목** | 부정적인 트윗 감정 검색  | hello hello 전자 메일 알림의 제목 줄입니다.  |
    | **본문** | 트윗 텍스트, 위치 | Hello 클릭 **텍스트 윗** 및 **위치** 매개 변수입니다. |

5.  **Save**를 클릭합니다.

Hello 워크플로 완료 했으므로 hello 논리 앱을 사용 하도록 설정 하 고 직장에서 hello 함수를 확인할 수 있습니다.

## <a name="test-hello-workflow"></a>테스트 hello 워크플로

1. Hello 논리가 응용 프로그램 디자이너에서에서 클릭 **실행** toostart hello 앱.

2. Hello 왼쪽된 열에서 클릭 **개요** hello 논리 앱의 toosee hello 상태입니다. 
 
    ![논리 앱 실행 상태](media/functions-twitter-email/over1.png)

3. (선택 사항) Hello 실행 toosee 세부 hello 실행 중 하나를 클릭 합니다.

4. Tooyour 함수 이동한 hello 로그를 확인 한 다음 감성 값 수신 및 처리 된 있는지 확인 합니다.
 
    ![함수 로그 보기](media/functions-twitter-email/sent.png)

5. 잠재적으로 부정적인 감정이 검색되면 전자 메일을 수신합니다. 전자 메일을 받지 못한 경우 될 때마다 hello 함수 코드 tooreturn 빨간색을 변경할 수 있습니다.

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    전자 메일 알림을 확인 한 후 뒤로 toohello 원본 코드를 변경 합니다.

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > 이 자습서를 완료 한 후에 hello 논리 앱을 비활성화 해야 합니다. Hello 앱을 사용 하지 않도록 설정, 수행 하 고 hello 트랜잭션을 Cognitive 서비스 계정에서 사용 하 여 실행에 대 한 청구 하지 마십시오.

이제 얼마나 쉬운지 논리 앱 워크플로로 toointegrate 함수에 살펴보았습니다.

## <a name="disable-hello-logic-app"></a>Hello 논리 앱을 사용 하지 않도록 설정

toodisable hello 논리 앱 클릭 **개요** 클릭 하 고 **사용 하지 않도록 설정** hello hello 화면 위쪽에 있습니다. 그러면 hello 논리 앱에서 실행 되 고 hello 앱을 삭제 하지 않고 요금이 발생 되지 않습니다. 

![함수 로그](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.

> [!div class="checklist"]
> * Cognitive Services 계정을 만듭니다.
> * 트윗 감정을 분류하는 함수를 만듭니다.
> * TooTwitter 연결 하는 논리 앱을 만듭니다.
> * 감성 검색 toohello 논리 앱을 추가 합니다. 
> * Hello 논리 앱 toohello 함수를 연결 합니다.
> * Hello 함수에서 hello 응답에 따라 전자 메일을 보냅니다.

다음 자습서 toolearn toohello 어떻게 발전 toocreate 서버가 없는 API 함수에 대 한 합니다.

> [!div class="nextstepaction"] 
> [Azure Functions를 사용하여 서버 없는 API 만들기](functions-create-serverless-api.md)

논리 앱에 대해 자세히 toolearn 참조 [Azure 논리 앱](../logic-apps/logic-apps-what-are-logic-apps.md)합니다.

