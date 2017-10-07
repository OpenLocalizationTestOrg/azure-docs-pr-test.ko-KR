---
title: "Azure 스트림 분석을 사용 하 여 aaaReal 타임 Twitter 감성 분석 | Microsoft Docs"
description: "자세한 내용은 방법 실시간 Twitter 감성 분석에 대 한 스트림 분석 toouse 합니다. 라이브 대시보드 이벤트 생성 toodata에서 단계별 지침입니다."
keywords: "실시간 twitter 분석 추세, 정서 분석, 소셜 미디어 분석, 추세 분석 예제"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Azure Stream Analytics에서 실시간 Twitter 감정 분석

자세한 내용은 toobuild 실시간으로 전환 하 여 소셜 미디어 분석에 대 한 감성 분석 솔루션 Azure 이벤트 허브로 이벤트를 Twitter 하는 방법입니다. Azure 스트림 분석 쿼리 tooanalyze hello 데이터와 둘 중 어떤 저장소 hello 나중에 사용에 대 한 결과 또는 대시보드를 사용 하 여 작성할 수 있습니다 및 [Power BI](https://powerbi.com/) tooprovide insights 실시간으로 합니다.

소셜 미디어 분석 도구는 조직에서 추세 항목을 이해하는 데 도움이 됩니다. 추세 항목은 소셜 미디어에 많은 게시물을 발생시키는 주제 및 입장입니다. 감성 분석 라고도 함 *의견 마이닝*, 제품, 아이디어 및에 대 한 소셜 미디어 분석 도구 toodetermine 태도 사용 합니다. 

실시간 Twitter 추세 분석 hello hashtag 구독 모델 toolisten toospecific 키워드 (해시)을 사용 하면 때문에 분석 도구를 보여 주는 좋은 예는 및의 피드 hello 감성 분석을 개발 합니다.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>시나리오: 소셜 미디어 실시간 감정 분석

뉴스 미디어 웹 사이트에 있는 회사에서는 사이트 콘텐츠 즉시 관련 tooits 판독기는을 통해 경쟁 업체의 이점을 활용에 관심이 많습니다. hello 회사 Twitter 데이터의 실시간 감성 분석을 수행 하 여 관련 tooreaders 되는 항목에서 소셜 미디어 분석을 사용 합니다.

Twitter에서 실시간으로에서 tooidentify 추세 항목 hello 회사 hello 윗 볼륨 및 주요 항목에 대 한 의미에 대 한 실시간 분석 요구 합니다. 즉, hello 필요는 감성 분석 분석 엔진 피드이 소셜 미디어 기반입니다.

## <a name="prerequisites"></a>필수 조건
이 자습서에서는 tooTwitter 연결 하 고 (다음을 설정할 수 있습니다)는 특정 붙일 있는 트 윗 찾습니다 하는 클라이언트 응용 프로그램을 사용 합니다. 순서 대로 toorun hello 응용 프로그램 및 Azure 스트리밍 분석을 사용 하 여 트 윗, 있어야 hello 다음 hello 분석:

* Azure 구독
* Twitter 계정 
* Twitter 응용 프로그램, 그리고 hello [OAuth 액세스 토큰](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) 해당 응용 프로그램에 대 한 합니다. 방법에 대 한 고급 지침 제공 toocreate 나중에 Twitter 응용 프로그램입니다.
* hello TwitterWPFClient 응용 프로그램을 읽는 hello Twitter 피드입니다. tooget이 응용 프로그램, 다운로드 hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) GitHub에서 파일을 컴퓨터의 폴더에 다음 hello 패키지 압축을 풉니다. Toosee hello 소스 코드를 원하는 고 디버거에서 hello 응용 프로그램을 실행에서 hello 소스 코드를 얻을 수 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)합니다. 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Streaming Analytics 입력을 위한 이벤트 허브 만들기

hello 샘플 응용 프로그램 이벤트를 생성 하며 tooan Azure 이벤트 허브를 푸시합니다. Azure 이벤트 허브는 hello 기본 설정 방법 스트림 분석에 대 한 이벤트 수집입니다. 자세한 내용은 참조 hello [Azure 이벤트 허브 설명서](../event-hubs/event-hubs-what-is-event-hubs.md)합니다.


### <a name="create-an-event-hub-namespace-and-event-hub"></a>이벤트 허브 네임스페이스 및 이벤트 허브 만들기
이 절차에서는 이벤트 허브 네임 스페이스를 먼저 만들어야 하 고 이벤트 허브 toothat 네임 스페이스를 추가 하는 합니다. 이벤트 허브 네임 스페이스는 사용 toologically 그룹 관련 이벤트 버스 인스턴스. 

1. 클릭 하 고 toohello Azure 포털에 로그인 **새로** > **사물 인터넷** > **이벤트 허브**합니다. 

2. Hello에 **네임 스페이스 만들기** 블레이드에서 같은 네임 스페이스 이름 입력 `<yourname>-socialtwitter-eh-ns`합니다. Hello 네임 스페이스에 대 한 모든 이름을 사용할 수 있습니다 하지만 hello 이름은 URL에 유효 해야 하 고 Azure 전체에서 고유 해야 합니다. 
    
3. 구독을 선택하고 리소스 그룹을 만들거나 선택한 후 **만들기**를 클릭합니다. 

    ![이벤트 허브 네임스페이스 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Hello 네임 스페이스 배포 완료 되 면 Azure 리소스 목록에 hello 이벤트 허브 네임 스페이스를 찾습니다. 

5. Hello 새 네임 스페이스를 클릭 하 고 hello 네임 스페이스 블레이드에서 클릭  **+ &nbsp;이벤트 허브**합니다. 

    ![새 이벤트 허브를 만들기 위한 hello 이벤트 허브 추가 단추 ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. 이름 hello 새 이벤트 허브 `socialtwitter-eh`합니다. 다른 이름을 사용할 수 있습니다. 이렇게 하면 hello 이름을 나중에 필요 하기 때문에, 메모를 확인 합니다. Hello 이벤트 허브에 대 한 다른 옵션 tooset를 필요 하지 않습니다.

    ![새 이벤트 허브를 만들기 위한 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. **만들기**를 클릭합니다.


### <a name="grant-access-toohello-event-hub"></a>권한 부여 액세스 toohello 이벤트 허브

프로세스 tooan 이벤트 허브 데이터를 보낼 수 있습니다, 전에 hello 이벤트 허브에 적절 한 액세스를 허용 하는 정책이 있어야 합니다. hello 액세스 정책 권한 부여 정보를 포함 하는 연결 문자열을 생성 합니다.

1.  Hello 이벤트 네임 스페이스 블레이드에서 클릭 **이벤트 허브** 새 이벤트 허브의 hello 이름을 클릭 하 고 있습니다.

2.  이벤트 허브 블레이드에서 hello 클릭 **공유 액세스 정책을** 클릭 하 고  **+ &nbsp;추가**합니다.

    >[!NOTE]
    >Hello 이벤트 허브 네임 스페이스가 아니라 hello 이벤트 허브를 사용 하 고 있는지 확인 합니다.

3.  **클레임**에 대해 `socialtwitter-access`라는 이름의 정책을 추가하고 **관리**를 선택합니다.

    ![새 이벤트 허브 액세스 정책을 만들기 위한 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  **만들기**를 클릭합니다.

5.  정책이 배포 된 hello 후, 공유 액세스 정책의 hello 목록에서 클릭 합니다.

6.  찾기 hello 상자 **연결 문자열-기본 키** hello 복사 단추 다음 toohello 연결 문자열을 클릭 합니다. 
    
    ![Hello 액세스 정책에서 hello 기본 연결 문자열 키를 복사합니다.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  연결 문자열을 hello를 텍스트 편집기에 붙여 넣습니다. 몇 가지 약간의 편집 tooit를 변경한 후이 연결 문자열 hello 다음 섹션에 필요 합니다.

    hello 연결 문자열은 다음과 같습니다.

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Hello 연결 문자열을 세미콜론으로 구분 된 여러 키-값 쌍이 들어: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, 및 `EntityPath`합니다.  

    > [!NOTE]
    > 보안을 위해 hello 예제에서 hello 연결 문자열의 일부 제거 되었습니다.

8.  Hello 텍스트 편집기에서 제거 hello `EntityPath` hello 연결 문자열에서 쌍 (tooremove hello 세미콜론 앞에 오는 반드시 함). 완료 되 면 hello 연결 문자열은 다음과 같습니다.

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>구성 되 고 hello Twitter 클라이언트 응용 프로그램 시작
클라이언트 응용 프로그램 hello Twitter에서 직접 윗 이벤트를 가져옵니다. 그렇게 toodo 주문에서 권한 toocall hello 스트리밍 Api Twitter 필요 합니다. tooconfigure 권한, 응용 프로그램에서 만드는 Twitter 고유 자격 증명 (예: OAuth 토큰)를 생성 하는 메시지입니다. 구성할 수 있습니다 클라이언트 응용 프로그램 toouse hello 이러한 자격 증명 API를 호출할 때입니다. 

### <a name="create-a-twitter-application"></a>Twitter 응용 프로그램 만들기
이 자습서에 사용할 수 있는 Twitter 응용 프로그램이 아직 없는 경우 만들 수 있습니다. Twitter 계정이 이미 있어야 합니다.

> [!NOTE]
> 응용 프로그램 만들기 및 hello 키, 암호, 및 토큰을 가져오는 Twitter의 정확한 프로세스 hello 변경 될 수 있습니다. 이러한 지침은 hello Twitter 사이트에 표시 되는 내용 일치 하지 않으면 toohello Twitter 개발자 설명서를 참조 하십시오.

1. Toohello 이동 [Twitter 응용 프로그램 관리 페이지](https://apps.twitter.com/)합니다. 

2. 새 응용 프로그램을 만듭니다. 

    * Hello 웹 사이트 URL에 대 한 올바른 URL을 지정 합니다. 없기 toobe 라이브 사이트입니다. (`localhost`만 지정할 수는 없음)
    * Hello 콜백 필드를 비워 둡니다. 이 자습서에 사용할 클라이언트 응용 프로그램 hello 콜백이 필요 하지 않습니다.

    ![Twitter에서 응용 프로그램 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. 필요에 따라 tooread 전용 hello 응용 프로그램의 사용 권한을 변경 합니다.

4. Hello 응용 프로그램을 만들면 이동 toohello **키와 액세스 토큰이** 페이지.

5. Hello 단추 toogenerate 액세스 토큰 및 액세스 토큰 암호를 클릭 합니다.

Hello 다음 절차에서 필요 하므로이 정보를 유지 합니다.

>[!NOTE]
>hello 키와 hello Twitter 응용 프로그램에 대 한 암호 tooyour Twitter 계정 액세스를 제공합니다. 중요 하 게이 정보를 처리, Twitter 암호와 같은으로 hello 동일 합니다. 예를 들어 tooothers를 지정 하는 응용 프로그램에서이 정보를 포함 하지 않음. 


### <a name="configure-hello-client-application"></a>Hello 클라이언트 응용 프로그램 구성
TooTwitter 데이터를 사용 하 여 연결 하는 클라이언트 응용 프로그램 작성 했습니다 [Twitter의 스트리밍 Api](https://dev.twitter.com/streaming/overview) 항목의 특정 집합에 대 한 트 윗 이벤트 toocollect 합니다. hello 응용 프로그램 hello를 사용 하 여 [Sentiment140](http://help.sentiment140.com/) 감성 값 tooeach 윗 다음 hello를 할당 하는 오픈 소스 도구:

* 0 = 부정적
* 2 = 중립
* 4 = 긍정적

Hello 윗 이벤트 감성 값 할당 된, 후 이전에 만든 toohello 이벤트 허브를 푸시할는 있습니다.

Hello 응용 프로그램을 실행 하기 전에 hello Twitter 키 hello 이벤트 허브 연결 문자열 등의 정보를 특정 필요 합니다. 다음과 같은이 방법으로 hello 구성 정보를 제공할 수 있습니다.

* Hello 응용 프로그램을 실행 하 고 hello 응용 프로그램의 UI tooenter hello 키, 비밀 정보 및 연결 문자열을 사용 합니다. 이 작업을 수행 하는 경우 현재 세션에 대 한 hello 구성 정보를 사용 하지만 저장 되지 않습니다.
* Hello 응용 프로그램의.config 파일 및 설정 hello 값을 편집 합니다. 이 방법은 hello 구성 정보를 유지 하지만 잠재적으로 중요 한 정보가 일반 텍스트로 컴퓨터에 저장 됩니다.

hello 다음 절차에서는 두 가지 방법을 모두 합니다. 

1. 다운로드 하 고 압축을 hello 확인 [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) hello 필수 구성 요소에 나열 된 응용 프로그램입니다.

2. 실행 시 (및 hello 현재 세션에 대해서만), tooset hello 값 실행 hello `TwitterWPFClient.exe` 응용 프로그램입니다. Hello 응용 프로그램 메시지를 표시 하면 hello 다음 값을 입력 합니다.

    * hello Twitter 소비자 키 (API 키)입니다.
    * hello Twitter 사용자 암호 (API Secret)입니다.
    * Twitter 액세스 토큰 번호입니다.
    * hello Twitter 액세스 토큰 암호입니다.
    * 이전에 저장 하는 hello 연결 문자열 정보입니다. Hello를 제거 하는 hello 연결 문자열을 사용 하면 `EntityPath` 키-값 쌍입니다.
    * 에 대 한 toodetermine 정서를 원하는 hello Twitter 키워드입니다.

   ![TwitterWpfClient 응용 프로그램 실행 중, 가려진 설정 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. tooset hello 값은 지속적으로, 텍스트 편집기 tooopen hello TwitterWpfClient.exe.config 파일을 사용합니다. Hello 그런 다음 `<appSettings>` 요소를이 작업을 수행 합니다.

    * 설정 `oauth_consumer_key` toohello Twitter 소비자 키 (API 키)입니다. 
    * 설정 `oauth_consumer_secret` toohello Twitter 사용자 암호 (API Secret)입니다.
    * 설정 `oauth_token` toohello Twitter 액세스 토큰입니다.
    * 설정 `oauth_token_secret` toohello Twitter 액세스 토큰 암호입니다.

    Hello의 뒷부분에 나오는 `<appSettings>` 요소를이 변경 하십시오.

    * 설정 `EventHubName` toohello 이벤트 허브 이름 (즉, hello 엔터티 경로 toohello 값).
    * 설정 `EventHubNameConnectionString` toohello 연결 문자열입니다. Hello를 제거 하는 hello 연결 문자열을 사용 하면 `EntityPath` 키-값 쌍입니다.

    hello `<appSettings>` 섹션 다음 예제는 hello 같습니다. (이해를 돕고 보안을 위해 일부 줄을 래핑하고 일부 문자는 제거했습니다.)

    ![Hello Twitter 키와 비밀 정보 및 hello 이벤트 허브 연결 문자열 정보를 표시 하는 텍스트 편집기에서 TwitterWpfClient 응용 프로그램 구성 파일](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Hello 응용 프로그램을 시작 이미 하지 않은 경우 지금 TwitterWpfClient.exe를 실행 합니다. 

5. Hello toocollect 소셜 감성 녹색 시작 단추를 클릭 합니다. Hello 사용 하 여 트 윗 이벤트 참조 **CreatedAt**, **항목**, 및 **SentimentScore** tooyour 이벤트 허브 전송 되는 값입니다.

    ![TwitterWpfClient 응용 프로그램 실행 중, 트윗 목록 표시](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >오류를 보고 트 윗 hello hello 창 하단에 표시 되는 스트림을 표시 되지 않는 경우에 hello 키 및 암호를 두 번 클릭 합니다. 또한 hello 연결 문자열 확인 (hello를 포함 하지 않는지 확인 `EntityPath` 키와 값입니다.)


## <a name="create-a-stream-analytics-job"></a>Stream Analytics 작업 만들기

트 윗 이벤트는 Twitter에서 실시간에서 스트리밍, 있습니다 수 설정할 스트림 분석 작업 tooanalyze 이러한 이벤트를 실시간으로 합니다.

1. Hello Azure 포털에서에서 클릭 **새로** > **사물 인터넷** > **스트림 분석 작업**합니다.

2. 이름 hello 작업 `socialtwitter-sa-job` 구독, 리소스 그룹 및 위치를 지정 합니다.

    것이 좋습니다 tooplace hello 작업과 hello 이벤트 허브를 hello에 동일한 지역에 대 한 최상의 성능 지역 간 데이터 tootransfer을 지불 하지 않습니다.

    ![새 Stream Analytics 작업 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. **만들기**를 클릭합니다.

    hello 작업은 생성 하 고 hello 포털 작업 세부 정보를 표시 합니다.


## <a name="specify-hello-job-input"></a>Hello 작업 입력 지정

1. 스트림 분석 작업에서 아래 **작업 토폴로지** hello 작업 블레이드의 hello 중간 클릭 **입력**합니다. 

2. Hello에 **입력** 블레이드에서 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.

    * **입력된 별칭**: hello 이름 사용 `TwitterStream`합니다. 다른 이름을 사용하는 경우 나중에 필요하므로 기록해 둡니다.
    * **원본 형식**: **데이터 스트림**을 선택합니다.
    * **원본**: **이벤트 허브**를 선택합니다.
    * **가져오기 옵션**: **현재 구독의 이벤트 허브 사용**을 선택합니다. 
    * **서비스 버스 네임 스페이스**: 이전에 만든 hello 이벤트 허브 네임 스페이스를 선택 (`<yourname>-socialtwitter-eh-ns`).
    * **이벤트 허브**: 이전에 만든 선택 hello 이벤트 허브 (`socialtwitter-eh`).
    * **이벤트 허브 정책 이름**: 이전에 만든 hello 액세스 정책 (`socialtwitter-access`).

    ![Streaming Analytics 작업에 대한 새 입력 만들기](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. **만들기**를 클릭합니다.


## <a name="specify-hello-job-query"></a>Hello 작업 쿼리를 지정 합니다.

Stream Analytics는 변환을 설명하는 간단하고 선언적인 쿼리 모델을 지원합니다. hello 언어에 대해 자세히 toolearn 참조 hello [Azure 스트림 분석 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)합니다.  이 자습서에서는 Twitter 데이터에 대해 여러 쿼리를 작성하고 테스트하도록 도와줍니다.

사용할 수 있습니다 항목 간에 언급 되어 toocompare hello 수는 [연속 창](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello 수가 5 초 마다 항목에서 설명 합니다.

1. 닫기 hello **입력** 블레이드 च ो.

2. Hello 작업 블레이드에서 hello 클릭 **쿼리** 상자입니다. Azure hello 입력 목록과 hello 작업에 대해 구성 되 고 수 있는 쿼리를 만들 수 있습니다는 출력을 toohello 출력 전송 될 때 hello 입력된 스트림 변환 됩니다.

3. 해당 hello TwitterWpfClient 응용 프로그램이 실행 되 고 있는지 확인 합니다. 

3. Hello에 **쿼리** 블레이드에서 hello 점 다음 toohello 클릭 `TwitterStream` 입력 한 다음 선택 **데이터 입력에서 샘플**합니다.

    ![메뉴 옵션 toouse 샘플 hello 스트리밍 분석 작업 항목에 대 한 데이터와 데이터 "샘플 입력에서" 선택](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Tooread hello 입력 스트림을 기간 측면에서 정의 된 샘플 데이터 tooget 양을 지정할 수 있는 블레이드가 열립니다.

4. 설정 **분** too3 클릭 하 고 **확인**합니다. 
    
    !["3 분" 선택 된 입력된 스트림의 hello 샘플링에 대 한 옵션입니다.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure는 3 분 분량의 hello 입력 스트림에서 데이터를 샘플링 하 고 hello 샘플 데이터를 준비 되 면 알려줍니다. (짧은 시간이 소요됩니다.) 

    hello 예제 데이터는 임시로 저장 되었다가 hello 쿼리 창이 열려 있는 동안를 사용할 수 있습니다. Hello 쿼리 창을 닫으면 hello 샘플 데이터가 무시 되 있고 toocreate 새 샘플 데이터 집합입니다. 

5. Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    하는 경우 사용 하지 않은 `TwitterStream` hello 입력 별칭에 대 한 hello로 대 한 별칭으로 대체 `TwitterStream` hello 쿼리에서 합니다.  

    이 쿼리에서 hello를 사용 하 여 **TIMESTAMP BY** 키워드 toospecify hello 임시 계산에서 사용 되는 hello 페이로드 toobe의 타임 스탬프 필드입니다. 이 필드를 지정 하지 않으면 hello 기간 이동 연산은 이벤트 허브 hello에 각 이벤트 도착 하는 hello 시간을 사용 하 여 수행 됩니다. hello "도착 시간 및 응용 프로그램 시간" 섹션에서 자세한 내용을 [스트림 분석 쿼리 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)합니다.

    이 쿼리는 또한 각 창의 hello 끝에 대 한 타임 스탬프 hello를 사용 하 여 액세스 **System.Timestamp** 속성입니다.

5. **테스트**를 클릭합니다. hello 쿼리 하면 샘플링 hello 데이터에 대해 실행 됩니다.
    
6. **Save**를 클릭합니다. 이 hello 스트리밍 분석 작업의 일부로 hello 쿼리를 저장합니다. (Hello 예제 데이터 저장 하지 않습니다.)


## <a name="experiment-using-different-fields-from-hello-stream"></a>서로 다른 필드를 사용 하 여 hello 스트림에서 실험 

hello 다음 표 hello JSON 스트리밍 데이터의 일부인 hello 필드입니다. Hello 쿼리 편집기에서 무료 tooexperiment을 느낍니다.

|JSON 속성 | 정의|
|--- | ---|
|CreatedAt | hello 시간 해당 hello 윗 생성|
|항목 | hello hello와 일치 하는 지정 되는 키워드|
|SentimentScore | Sentiment140에서 hello 감성 점수|
|작성자 | hello 트 윗을 보낼 hello Twitter 핸들|
|텍스트 | hello 윗의 전문을 hello|


## <a name="create-an-output-sink"></a>출력 싱크 만들기

이벤트 스트림, 이벤트 허브 입력된 tooingest 이벤트 및 쿼리 tooperform 변환 hello 스트림을 통해 이제 정의 했습니다. hello 마지막 단계는 hello 작업에 대 한 출력 싱크가 toodefine입니다.  

이 자습서에서는 hello 작업 쿼리 tooAzure Blob 저장소에서에서 집계 하는 hello 윗 이벤트를 기록합니다.  또한 프로그램 결과 tooAzure SQL 데이터베이스, Azure 테이블 저장소에 이벤트 허브를 푸시할 수 있습니다 또는 Power BI 응용 프로그램에 따라 필요한.

## <a name="specify-hello-job-output"></a>Hello 작업 출력을 지정 합니다.

1. Hello에 **작업 토폴로지** 섹션에서 hello **출력** 상자입니다. 

2. Hello에 **출력** 블레이드에서 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.

    * **출력 별칭**: hello 이름 사용 `TwitterStream-Output`합니다. 
    * **싱크**: **Blob Storage**를 선택합니다.
    * **가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.
    * **저장소 계정**. **새 저장소 계정 만들기**를 선택합니다.
    * **저장소 계정**(두 번째 상자). `YOURNAMEsa`를 입력합니다. 여기서 `YOURNAME`은 사용자 이름 또는 다른 고유 문자열입니다. hello 이름은 소문자 및 숫자를 사용할 수 및 Azure 전체에서 고유 해야 합니다. 
    * **컨테이너**. `socialtwitter`을 입력합니다.
    hello 저장소 계정 이름과 컨테이너 이름에 사용 되는 함께 tooprovide 다음과 같이 hello blob 저장소에 대 한 URI는 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Stream Analytics 작업에 대한 “새 출력” 블레이드](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. **만들기**를 클릭합니다. 

    Azure는 hello 저장소 계정을 만들고 키를 자동으로 생성 합니다. 

5. 닫기 hello **출력** 블레이드입니다. 


## <a name="start-hello-job"></a>Hello 작업 시작

작업 입력, 쿼리 및 출력이 지정됩니다. 준비 toostart hello 스트림 분석 작업 됩니다.

1. 해당 hello TwitterWpfClient 응용 프로그램이 실행 되 고 있는지 확인 합니다. 

2. Hello 작업 블레이드에서 클릭 **시작**합니다.

    ![Hello 스트림 분석 작업 시작](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. Hello에 **시작 작업** 블레이드에서 대 한 **작업 출력 시작 시간**선택, **이제** 클릭 하 고 **시작**합니다. 

    ![Hello 스트림 분석 작업에 대 한 블레이드 "작업을 시작 합니다."](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure 알리는 hello 작업이 시작 되 고으로 표시 되 면 hello 상태 hello 작업 블레이드에서 **실행**합니다.

    ![작업 실행 중](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>정서 분석에 대한 출력 보기

작업 실행을 시작 하 고 hello 실시간 Twitter 스트림 처리, 후 감성 분석에 대 한 hello 출력을 볼 수 있습니다.

와 같은 도구를 사용할 수 있습니다 [Azure 저장소 탐색기](https://http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction) tooview 작업 실시간으로 출력 합니다. 여기에서 사용할 수 있습니다 [Power BI](https://powerbi.com/) tooextend 프로그램 응용 프로그램 tooinclude 사용자 지정된 된 대시보드와 같은 hello hello 스크린 샷 뒤에 표시 된 것 하나:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>다른 쿼리 tooidentify 추세 항목 만들기

Twitter 감성 toounderstand에서는 다른 쿼리 기반으로 한 [슬라이딩 윈도우](https://msdn.microsoft.com/library/azure/dn835051.aspx)합니다. 지정된 된 기간에 언급 되어에 대 한 임계값을 교차 하는 항목에 대 한 보면 tooidentify 추세 항목입니다.

이 자습서의 hello 목적에 언급 된 20 배 이상 hello 마지막 5 초 하는 항목에 대 한 확인 합니다.

1. Hello 작업 블레이드에서 클릭 **중지** toostop hello 작업 합니다. 

2. Hello에 **작업 토폴로지** 섹션에서 hello **쿼리** 상자입니다. 

3. Hello 쿼리 toohello 다음을 변경 합니다.

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. **Save**를 클릭합니다.

5. 해당 hello TwitterWpfClient 응용 프로그램이 실행 되 고 있는지 확인 합니다. 

6. 클릭 **시작** hello 새 쿼리를 사용 하 여 toorestart hello 작업 합니다.


## <a name="get-support"></a>지원 받기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
