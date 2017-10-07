# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Azure Stream Analytics 사용 시작 : 실시간 부정 행위 감지

이 자습서는 방법의 종단 간 그림을 제공 toouse Azure 스트림 분석 합니다. 다음 방법에 대해 알아봅니다. 

* 스트리밍 이벤트를 Azure Event Hubs의 인스턴스로 전환합니다. 이 자습서에서는 휴대폰 메타데이터 레코드 스트림을 시뮬레이션하도록 제공하는 앱을 사용합니다.

* 정보 집계 또는 패턴을 찾고 있습니다. SQL과 유사한 스트림 분석 쿼리 tootransform 데이터를 작성 합니다. 어떻게 toouse 쿼리 tooexamine 들어오는 스트림을 hello를 찾아서 클릭 사기 될 수 있는 호출에 대 한 나타납니다.

* 보낼 hello 결과 tooan 출력 싱크 (저장소)를 추가로 insights를 분석할 수 있습니다. 이 경우 hello 의심 스러운 호출 데이터 tooAzure Blob 저장소를 보내 드립니다.

이 자습서에서는 전화 통화 데이터를 기반으로 하는 실시간 사기 감지의 hello 예제를 사용 합니다. 하지만 hello 기술을 설명할 사기 감지 신용 카드 사기 또는 id 도용 같은 다른 형식에도 적합 합니다. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>시나리오: 실시간으로 통신 및 SIM 사기 감지

통신 회사에는 많은 양의 들어오는 호출 데이터가 있습니다. hello 사는 고객에 게 알림 하거나 특정 수에 대 한 서비스를 종료할 수 있도록 toodetect 사기성 실시간으로 호출 합니다. 한 가지 유형의 SIM 사기 포함 hello에서 여러 번 호출 됩니다. hello 주위 동일한 id 시간이 하지만 서로 다른 지리적 위치입니다. toodetect이이 유형의 사기, 회사 요구 tooexamine 들어오는 전화 레코드 hello 찾은 특정 패턴에 대 한-이 경우에 대 한 호출 주위 hello 각각 다른 국가에서 동시 합니다. 이 범주에 해당 하는 모든 전화 레코드 toostorage 이후 분석을 위해 기록 됩니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에서는 샘플 전화 통화 메타데이터를 생성하는 클라이언트 앱을 사용하여 전화 통화 데이터를 시뮬레이션합니다. 일부 앱 hello hello 레코드 모양을 사기성 호출을 생성 합니다. 

시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.

* Azure 계정.
* hello 호출 이벤트 생성기는 응용 프로그램. Hello를 다운로드 하 여 가져올 수 있습니다 [TelcoGenerator.zip 파일](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) hello Microsoft 다운로드 센터에서에서. 컴퓨터의 폴더에 이 패키지의 압축을 풉니다. Toosee hello 소스 코드를 디버거에서 실행된 hello 앱을 원하는 hello 앱 소스 코드에서 얻을 수 있습니다 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)합니다. 

    >[!NOTE]
    >Windows는 hello를 다운로드 한.zip 파일을 차단할 수 있습니다. 풀고 수 없는 경우 hello 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. Hello 표시 되 면 "파일인 다른 컴퓨터에서이 및 보호할 수 있습니다 수 차단 된 toohelp이이 컴퓨터" 메시지, 선택 hello **차단 해제** 옵션 선택한 다음 클릭 **적용**합니다.

Hello 스트리밍 분석 작업의 tooexamine hello 결과 찾으려는 경우 또한 Azure Blob 저장소 컨테이너의 hello 내용을 보기 위한 도구를 필요 합니다. Visual Studio를 사용하는 경우 [Visual Studio용 Azure 도구](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) 또는 [Visual Studio 클라우드 탐색기](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer)를 사용할 수 있습니다. 또는 [Azure Storage 탐색기](http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)와 같은 독립 실행형 도구를 설치할 수 있습니다. 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Azure 이벤트 허브 tooingest 이벤트를 만듭니다.

데이터 스트림, tooanalyze 있습니다 *수집* Azure로 합니다. 일반적인 방법은 tooingest 데이터는 다음과 같은 toouse [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md), 수백만 개의 초당 이벤트를 수집 하 고 다음 처리를 hello 이벤트 정보를 저장할 수 있습니다. 이 자습서에서는 이벤트 허브 만들고 hello 호출 이벤트 생성기 앱 송신 호출 데이터 toothat 이벤트 허브를 해야 합니다. 이벤트 허브에 대 한 자세한 참조 hello [Azure 서비스 버스 설명서](https://docs.microsoft.com/en-us/azure/service-bus/)합니다.

>[!NOTE]
>이 절차의 보다 자세한 버전용 참조 [는 이벤트 허브 네임 스페이스를 만들고 Azure 포털 hello 사용 하 여 이벤트 허브](../event-hubs/event-hubs-create.md)합니다. 

### <a name="create-a-namespace-and-event-hub"></a>네임스페이스 및 이벤트 허브 만들기
이 절차에서는 이벤트 허브 네임 스페이스를 먼저 만들어야 하 고 이벤트 허브 toothat namepsace를 추가 하는 합니다. 이벤트 허브 네임 스페이스는 사용 toologically 그룹 관련 이벤트 버스 인스턴스. 

1. Hello Azure 포털에 로그인 하 고 클릭 **새로** > **사물 인터넷** > **이벤트 허브**합니다. 

2. Hello에 **네임 스페이스 만들기** 블레이드에서 같은 네임 스페이스 이름 입력 `<yourname>-eh-ns-demo`합니다. Hello 네임 스페이스에 대 한 모든 이름을 사용할 수 있습니다 하지만 hello 이름은 URL에 유효 해야 하 고 Azure 전체에서 고유 해야 합니다. 
    
3. 구독을 선택하고 리소스 그룹을 만들거나 선택한 후 **만들기**를 클릭합니다. 

    ![이벤트 허브 네임스페이스 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Hello 네임 스페이스 배포 완료 되 면 Azure 리소스 목록에 hello 이벤트 허브 네임 스페이스를 찾습니다. 

5. Hello 새 네임 스페이스를 클릭 하 고 hello 네임 스페이스 블레이드에서 클릭  **+ &nbsp;이벤트 허브**합니다. 

    ![새 이벤트 허브를 만들기 위한 hello 이벤트 허브 추가 단추 ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. 이름 hello 새 이벤트 허브 `sa-eh-frauddetection-demo`합니다. 다른 이름을 사용할 수 있습니다. 이렇게 하면 hello 이름을 나중에 필요 하기 때문에, 메모를 확인 합니다. 않아도 tooset 다른 옵션 hello 이벤트 허브에 대 한 현재 됩니다.

    ![새 이벤트 허브를 만들기 위한 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. **만들기**를 클릭합니다.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>액세스 toohello 이벤트 허브를 부여 하 고 연결 문자열을 가져올

프로세스 tooan 이벤트 허브 데이터를 보낼 수 있습니다, 전에 hello 이벤트 허브에 적절 한 액세스를 허용 하는 정책이 있어야 합니다. hello 액세스 정책 권한 부여 정보를 포함 하는 연결 문자열을 생성 합니다.

1.  Hello 이벤트 네임 스페이스 블레이드에서 클릭 **이벤트 허브** 새 이벤트 허브의 hello 이름을 클릭 하 고 있습니다.

2.  이벤트 허브 블레이드에서 hello 클릭 **공유 액세스 정책을** 클릭 하 고  **+ &nbsp;추가**합니다.

    >[!NOTE]
    >Hello 이벤트 허브 네임 스페이스가 아니라 hello 이벤트 허브를 사용 하 고 있는지 확인 합니다.

3.  **클레임**에 대해 `sa-policy-manage-demo`라는 이름의 정책을 추가하고 **관리**를 선택합니다.

    ![새 이벤트 허브 액세스 정책을 만들기 위한 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  **만들기**를 클릭합니다.

5.  정책이 배포 된 hello 후, 공유 액세스 정책의 hello 목록에서 클릭 합니다.

6.  찾기 hello 상자 **연결 문자열-기본 키** hello 복사 단추 다음 toohello 연결 문자열을 클릭 합니다. 
    
    ![Hello 액세스 정책에서 hello 기본 연결 문자열 키를 복사합니다.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  연결 문자열을 hello를 텍스트 편집기에 붙여 넣습니다. 몇 가지 약간의 편집 tooit를 변경한 후이 연결 문자열 hello 다음 섹션에 필요 합니다.

    hello 연결 문자열은 다음과 같습니다.

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Hello 연결 문자열을 세미콜론으로 구분 된 여러 키-값 쌍이 들어: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, 및 `EntityPath`합니다.  

## <a name="configure-and-start-hello-event-generator-application"></a>구성 되 고 hello 이벤트 생성기 응용 프로그램 시작

Hello TelcoGenerator 앱을 시작 하기 전에 수 있도록 구성 방금 만든 호출 레코드 toohello 이벤트 허브를 전송 합니다.

### <a name="configure-hello-telcogeneratorapp"></a>Hello TelcoGeneratorapp 구성

1.  Hello 편집기 hello 연결 문자열을 복사한 위치에 hello 기록해 `EntityPath` 값을 복사한 후 제거 hello `EntityPath` 쌍 (tooremove hello 세미콜론 앞에 오는 반드시 함). 

2.  Hello TelcoGenerator.zip 파일의 압축을 푼 hello 폴더에서 hello telcodatagen.exe.config 편집기에서에서 파일을 엽니다. (둘 이상의.config 파일은, hello 오른쪽으로 한 열 해야 합니다.)

3.  Hello에 `<appSettings>` 요소를이 작업을 수행 합니다.

    * Hello의 hello 값 설정 `EventHubName` 키 toohello 이벤트 허브 이름 (즉, hello 엔터티 경로 toohello 값).
    * Hello의 hello 값 설정 `Microsoft.ServiceBus.ConnectionString` toohello 연결 문자열을 입력 합니다. 

    hello `<appSettings>` 섹션은 다음 예제는 hello 같습니다. (명확성을 위해 우리 줄 바꿈된 hello 줄 및 hello 인증 토큰에서 일부 문자를 제거 합니다.)

    ![Hello 이벤트 허브 이름 및 연결 문자열을 보여 주는 TelcoGenerator 응용 프로그램 구성 파일](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Hello 파일을 저장 합니다. 

### <a name="start-hello-app"></a>Hello 응용 프로그램을 시작
1.  명령 창을 열고 hello TelcoGenerator 앱 압축 되지 않습니다 toohello 폴더를 변경 합니다.
2.  Hello 다음 명령을 입력 합니다.

        telcodatagen.exe 1000 .2 2

    hello 매개 변수는. 

    * 시간당 CDR 수. 
    * SIM 카드 사기 확률: 모든 호출의 백분율로 서 얼마나 자주 hello 이러한 앱을 시뮬레이션 해야 사기성 호출 합니다. hello 값.2가 기록 하는 hello 호출의 약 20% 사기성 한지를 의미 합니다.
    * 기간(시간). hello 수 시간 hello 응용 프로그램을 실행 해야 합니다. 작업을 hello 명령줄에서 Ctrl + C를 눌러 언제 든 지 hello 앱으로 중지할 수도 있습니다.

    몇 초 후 hello 앱 toohello 이벤트 허브에 전송할 때 hello 화면에 전화 통화 레코드를 표시를 시작 합니다.

이 실시간 사기 감지 응용 프로그램에서 사용 하 여 hello 키 필드는 hello 다음 다음과 같습니다.

|**레코드**|**정의**|
|----------|--------------|
|`CallrecTime`|hello timestamp 안녕 호출에 대 한 시작 시간입니다. |
|`SwitchNum`|hello 전화 스위치 tooconnect hello 호출을 사용합니다. 예를 들어 hello 스위치는 hello 국가별 (미국, 중국, 영국, 독일에 또는 오스트레일리아의 경우)을 나타내는 문자열입니다. |
|`CallingNum`|hello 호출자의 hello 전화 번호입니다. |
|`CallingIMSI`|국제 모바일 IMSI (Subscriber Identity) 번호입니다. Hello hello 호출자의 고유 식별자입니다. |
|`CalledNum`|hello 호출 수신자의 hello 전화 번호입니다. |
|`CalledIMSI`|국제 모바일 구독자 ID(IMSI) Hello hello 호출 수신자의 고유 식별자입니다. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>스트리밍 데이터 스트림 분석 작업 toomanage 만들기

이제 호출 이벤트 스트림이 있고 Stream Analytics 작업을 설정할 수 있습니다. hello 작업은 설정 하는 hello 이벤트 허브에서 데이터를 읽습니다. 

### <a name="create-hello-job"></a>Hello 작업 만들기 

1. Hello Azure 포털에서에서 클릭 **새로** > **사물 인터넷** > **스트림 분석 작업**합니다.

2. 이름 hello 작업 `sa_frauddetection_job_demo`, 구독, 리소스 그룹 및 위치를 지정 합니다.

    것이 좋습니다 tooplace hello 작업과 hello 이벤트 허브를 hello에 동일한 지역에 대 한 최상의 성능 지역 간 데이터 tootransfer을 지불 하지 않습니다.

    ![새 Stream Analytics 작업 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. **만들기**를 클릭합니다.

    hello 작업은 생성 하 고 hello 포털 작업 세부 정보를 표시 합니다. 아무 것도 실행 되 고 아직 하지만-시작 하기 전에 tooconfigure hello 작업 해야 합니다.

### <a name="configure-job-input"></a>작업 입력 구성

1. Hello 대시보드 또는 hello **모든 리소스** 블레이드, 찾기 및 선택 hello `sa_frauddetection_job_demo` 스트림 분석 작업 합니다. 
2. Hello에 **작업 토폴로지** hello 스트림 분석 작업 블레이드의 섹션에 있는 클릭 hello **입력** 상자입니다.

    ![Hello 스트리밍 분석 작업 블레이드에서 토폴로지에서 입력된 상자](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.

    * **입력된 별칭**: hello 이름 사용 `CallStream`합니다. 다른 이름을 사용하는 경우 나중에 필요하므로 기록해 둡니다.
    * **원본 형식**: **데이터 스트림**을 선택합니다. (**참조 데이터** 이 자습서에서 사용 하지 않으며 toostatic 조회 데이터를 참조 합니다.)
    * **원본**: **이벤트 허브**를 선택합니다.
    * **가져오기 옵션**: **현재 구독의 이벤트 허브 사용**을 선택합니다. 
    * **서비스 버스 네임 스페이스**: 이전에 만든 hello 이벤트 허브 네임 스페이스를 선택 (`<yourname>-eh-ns-demo`).
    * **이벤트 허브**: 이전에 만든 선택 hello 이벤트 허브 (`sa-eh-frauddetection-demo`).
    * **이벤트 허브 정책 이름**: 이전에 만든 hello 액세스 정책 (`sa-policy-manage-demo`).

    ![Streaming Analytics 작업에 대한 새 입력 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. **만들기**를 클릭합니다.

## <a name="create-queries-tootransform-real-time-data"></a>실시간 데이터 tootransform 쿼리 만들기

이 시점에서 스트림 분석 작업 tooread 들어오는 데이터 스트림을 설정 해야 합니다. hello 다음 단계는 toocreate hello 데이터를 실시간으로 분석 하는 변환입니다. 쿼리를 만들어 이 작업을 수행합니다. Stream Analytics는 실시간 처리에 대해 변환을 설명하는 간단하고 선언적인 쿼리 모델을 지원합니다. hello 쿼리 일부 확장 특정 toostream 분석 있는 SQL 유사 언어를 사용 합니다. 

매우 간단한 쿼리는 hello 들어오는 모든 데이터를 읽어 단순히 수도 있습니다. 그러나 자주 표시 된 특정 데이터에 대 한 또는 hello 데이터의 관계에 대 한 쿼리를 만듭니다. Hello 자습서의이 섹션에서는 만들고 테스트 하면 몇 가지 쿼리 toolearn 몇 가지 방법으로 분석을 위한 입력된 스트림을 변형할 수 있습니다. 

여기서 만드는 hello 쿼리 hello 변환 된 데이터 toohello 화면을 표시만 합니다. 이후 섹션에는 출력 싱크 및 hello 변환 된 데이터 toothat 싱크를 작성 하는 쿼리를 구성 합니다.

hello 언어에 대해 자세히 toolearn 참조 hello [Azure 스트림 분석 쿼리 언어 참조](https://msdn.microsoft.com/library/dn834998.aspx)합니다.

### <a name="get-sample-data-for-testing-queries"></a>쿼리를 테스트하기 위한 샘플 데이터 가져오기

hello TelcoGenerator 앱에서 보내는 호출 레코드 toohello 이벤트 허브 및 스트림 분석 작업은 hello 이벤트 허브에서 구성 된 tooread 합니다. 쿼리 tootest hello 작업 toomake 올바르게 읽거나 있는지를 사용할 수 있습니다. 너무 hello Azure 콘솔에에서는 쿼리를 테스트 하 고 예제 데이터를 해야 합니다. 이 연습에서는 hello 이벤트 허브에 들어오는 hello 스트림에서 샘플 데이터를 추출할 수 있습니다.

1. Hello TelcoGenerator 이러한 앱을 실행 하 고 기록 하는 호출을 생성 해야 합니다.
2. Hello 포털에서 toohello 스트리밍 분석 작업 블레이드를 반환 합니다. (Hello 블레이드를 닫은 경우 검색할 `sa_frauddetection_job_demo` hello에 **모든 리소스** 블레이드.)
3. Hello 클릭 **쿼리** 상자입니다. Azure hello 입력 목록과 hello 작업에 대해 구성 되 고 수 있는 쿼리를 만들 수 있습니다는 출력을 toohello 출력 전송 될 때 hello 입력된 스트림 변환 됩니다.
4. Hello에 **쿼리** 블레이드에서 hello 점 다음 toohello 클릭 `CallStream` 입력 한 다음 선택 **데이터 입력에서 샘플**합니다.

    ![메뉴 옵션 toouse 샘플 hello 스트리밍 분석 작업 항목에 대 한 데이터와 데이터 "샘플 입력에서" 선택](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Tooread hello 입력 스트림을 기간 측면에서 정의 된 샘플 데이터 tooget 양을 지정할 수 있는 블레이드가 열립니다.

5. 설정 **분** too3 클릭 하 고 **확인**합니다. 
    
    !["3 분" 선택 된 입력된 스트림의 hello 샘플링에 대 한 옵션입니다.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure는 3 분 분량의 hello 입력 스트림에서 데이터를 샘플링 하 고 hello 샘플 데이터를 준비 되 면 알려줍니다. (짧은 시간이 소요됩니다.) 

hello 예제 데이터는 임시로 저장 되었다가 hello 쿼리 창이 열려 있는 동안를 사용할 수 있습니다. Hello 쿼리 창을 닫으면 hello 샘플 데이터가 무시 되 고 해야 합니다. toocreate 새 샘플 데이터 집합입니다. 

대신에 샘플 데이터.json 파일을 가져올 수 있습니다 [GitHub에서](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), 한 다음 해당.json 파일 toouse hello에 대 한 예제 데이터로 업로드 `CallStream` 입력 합니다. 

### <a name="test-using-a-pass-through-query"></a>통과 쿼리를 사용하여 테스트

모든 이벤트 tooarchive 하려는 경우 모든 hello 필드 hello 이벤트의 페이로드를 hello에 통과 쿼리 tooread를 사용할 수 있습니다.

1. Hello 쿼리 창에서이 쿼리를 입력 합니다.

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >SQL처럼 키워드는 대/소문자를 구분하지 않고 공백은 중요하지 않습니다.

    이 쿼리에서 `CallStream` 는 hello 별칭 hello 입력을 만들 때 지정한 합니다. 다른 별칭을 사용하는 경우 대신 해당 이름을 사용합니다.

2. **테스트**를 클릭합니다.

    hello 스트림 분석 작업 hello 샘플 데이터에 대해 hello 쿼리를 실행 하 고 hello hello 창 맨 아래에 hello 출력을 표시 합니다. 이 알 수 hello 이벤트 허브 및 hello 스트리밍 분석 작업을 올바르게 구성 되어 있습니다. (앞에서 설명한 것 처럼 나중에 만들게 출력 싱크가 해당 hello 쿼리 데이터를 쓸 수 있습니다.)

    ![Stream Analytics 작업 출력, 73개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    표시 되는 레코드의 수를 정확 하 게 hello 레코드 수를 3 분 샘플에서 캡처된에 따라 달라 집니다.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>열 투영을 사용 하 여 필드의 hello 수 줄이기

대부분의 경우에서 분석 hello 입력 스트림에서 모든 hello 열이 필요 하지 않습니다. 보다 적은 집합의 필드 보다 hello 통과 쿼리에서 반환 된 쿼리 tooproject를 사용할 수 있습니다.

1. Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. **테스트**를 다시 클릭합니다. 

    ![프로젝션에 대한 Stream Analytics 작업 출력, 25개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>지역별로 들어오는 호출 수: 집계를 포함하는 연속 창

Toocount hello 개수의 들어오는 호출 / 지역당 한다고 가정 합니다. 데이터 스트리밍에서 tooperform, 횟수와 같은 집계 함수를 원하는 때 toosegment hello 스트림이 필요 임시 단위로 (효과적으로 무한 hello 데이터 스트림 자체 이므로). Streaming Analytics [window 함수](stream-analytics-window-functions.md)를 사용하여 이 작업을 수행합니다. 그런 다음 해당 창 내부의 hello 데이터와 하나의 단위로 작업할 수 있습니다.

이 변환의 경우 겹치지 않는 temporal 창 시퀀스를 원하며 각 창에는 그룹화 및 집계할 수 있는 불연속 데이터 집합이 있습니다. 이 창 유형은 참조 tooas는 *연속 창* 합니다. Hello 텀블 링 창 내에서 그룹화 된 걸려오는 전화를 hello의 개수를 가져올 수 있습니다 `SwitchNum`, hello 국가 hello 호출 발생을 나타냅니다. 

1. Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    이 쿼리에서 hello를 사용 하 여 `Timestamp By` hello 키워드 `FROM` 절 toospecify hello에는 타임 스탬프 필드 입력 스트림 toouse toodefine hello 연속 창. 이 경우 hello 창 나눕니다 hello 데이터 세그먼트로 hello `CallRecTime` 각 레코드의 필드입니다. (필드가 없으면 지정 된 경우 hello 기간 이동 연산은 사용 하 여 hello 이벤트 허브에 각 이벤트 도착 하는 hello 시간입니다. [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)에서 “도착 시간과 응용 프로그램 시간”을 참조하세요. 

    hello 프로젝션에 `System.Timestamp`, 각 창의 hello 끝에 대 한 타임 스탬프를 반환 하는 합니다. 

    hello를 사용 하면 원하는 toouse 연속 창 toospecify, [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) 함수 hello에 `GROUP BY `절. Hello 함수 (마이크로초 tooa 날)에서 든 시간 단위 및 창 크기 (단위)를 지정합니다. 이 예제에서는 hello 연속 창 개의 5 초 간격으로 이루어지며 5 초 마다 동안의 호출에 대 한 국가별 개수를 받게 됩니다.

2. **테스트**를 다시 클릭합니다. Hello 결과 얻으려면 해당 hello 타임 스탬프에서 알 수 있듯이 **WindowEnd** 5 초 단위로 됩니다.

    ![집계에 대한 Stream Analytics 작업 출력, 13개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>셀프 조인을 사용하여 SIM 사기 감지

이 예를 고려할 수도 있지만 사기성 사용 toobe 호출에서에서 생성 되는 hello 동일 사용자 서로 5 초 안에 서로 다른 위치에서 합니다. 예를 들어 hello 동일한 사용자 없습니다 합법적인 방식으로에서 전화를 걸거나 hello 미국 및 오스트레일리아 hello에서 같은 시간입니다. 

이러한 경우에 대 한 toocheck, 스트리밍 데이터 toojoin hello 스트림 tooitself hello에 따라 hello의 자체 조인을 사용할 수 있습니다 `CallRecTime` 값입니다. 여기서 hello 호출 기록에 대 한 다음 확인할 수 있습니다 `CallingIMSI` 동일 값 (원래 수 hello) hello은 있지만 hello `SwitchNum` 값 (원점 국가)은 동일한 hello 되지 않습니다.

조인을 사용 하 여 스트리밍 데이터 행을 일치 시켜 얼마나 hello에 대 한 몇 가지 제한 시간으로 구분 되어 있을 수 hello 조인 입력 해야 합니다. (앞에서 설명한 대로 hello 스트리밍 데이터를 효과적으로 무한.) hello 내 hello 관계에 대 한 hello 시간 범위에서 지정 된 `ON` hello를 사용 하 여 hello 조인의 절 `DATEDIFF` 함수입니다. 이 경우 hello 조인의 호출 데이터는 5 초 간격 기준입니다.

1. Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다. 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    이 쿼리는 hello 제외한 모든 SQL 조인 같습니다 `DATEDIFF` hello 조인에는 함수입니다. 버전이이 `DATEDIFF` 특정 tooStreaming 분석, 이며 hello에 표시 되어야 `ON...BETWEEN` 절. hello 매개 변수는 시간 단위 (이 예제에서는 초)와 hello 조인에 대 한 hello 두 소스의 hello 별칭입니다. (이 다른 표준 SQL hello `DATEDIFF` 함수입니다.) 

    hello `WHERE` hello 사기성 호출 플래그를 지정 하는 hello 조건 절에 포함 되어: hello 원래 스위치는 동일한 hello 되지 않습니다. 

2. **테스트**를 다시 클릭합니다. 

    ![셀프 조인에 대한 Stream Analytics 작업 출력, 6개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. **Save**를 클릭합니다. 이 hello 스트리밍 분석 작업의 일부로 hello 자체 조인 쿼리를 저장합니다. (Hello 예제 데이터 저장 하지 않습니다.)

    ![Stream Analytics 작업 저장](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>출력 싱크 변환 toostore 데이터 만들기

Hello 스트림을 통해 이벤트 스트림, 이벤트 허브 입력된 tooingest 이벤트 및 쿼리 tooperform 변환 정의 했습니다. hello 마지막 단계는 hello 작업에 대 한 출력 싱크가 toodefine-즉, 전체 toowrite hello 변환 스트림입니다. 

SQL Server Database, Table Storage, Data Lake Storage, Power BI 및 다른 이벤트 허브 등 많은 리소스를 출력 싱크로 사용할 수 있습니다. 이 자습서에서는 hello 스트림 tooAzure는 구조화 되지 않은 데이터를 수용 하는 것 때문에 나중에 분석할 수에 대 한 이벤트 정보를 수집 하기 위한 일반적인 선택 하는 Blob 저장소를 작성 합니다.

기존 Blob Storage 계정이 있는 경우 기존 계정을 사용할 수 있습니다. 이 자습서에서는 보여줍니다 어떻게 toocreate 새 저장소는이 자습서에 대 한을 고려 합니다.

### <a name="create-an-azure-blob-storage-account"></a>Azure Blob Storage 계정 만들기

1. Azure 포털 hello toohello 스트리밍 분석 작업 블레이드를 반환 합니다. (Hello 블레이드를 닫은 경우 검색할 `sa_frauddetection_job_demo` hello에 **모든 리소스** 블레이드.)
2. Hello에 **작업 토폴로지** 섹션에서 hello **출력** 상자입니다. 
3. Hello에 **출력** 블레이드에서 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.

    * **출력 별칭**: hello 이름 사용 `CallStream-FraudulentCalls`합니다. 
    * **싱크**: **Blob Storage**를 선택합니다.
    * **가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.
    * **저장소 계정**. **새 저장소 계정 만들기**를 선택합니다.
    * **저장소 계정**(두 번째 상자). `YOURNAMEsademo`를 입력합니다. 여기서 `YOURNAME`은 사용자 이름 또는 다른 고유 문자열입니다. hello 이름은 소문자 및 숫자를 사용할 수 및 Azure 전체에서 고유 해야 합니다. 
    * **컨테이너**. `sa-fraudulentcalls-demo`을 입력합니다.
    hello 저장소 계정 이름과 컨테이너 이름에 사용 되는 함께 tooprovide 다음과 같이 hello blob 저장소에 대 한 URI는 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Stream Analytics 작업에 대한 “새 출력” 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. **만들기**를 클릭합니다. 

    Azure는 hello 저장소 계정을 만들고 키를 자동으로 생성 합니다. 

5. 닫기 hello **출력** 블레이드입니다. 

## <a name="start-hello-streaming-analytics-job"></a>Hello 스트리밍 분석 작업 시작

hello 작업이 구성 되었습니다. 입력 (hello 이벤트 허브), (hello 쿼리 toolook 사기성 호출에 대 한), 변환 및 출력 (blob storage)를 지정 했습니다. 이제 hello 작업을 시작할 수 있습니다. 

1. Hello TelcoGenerator 앱이 실행 되 고 있는지 확인 합니다.

2. Hello 작업 블레이드에서 클릭 **시작**합니다.

    ![Hello 스트림 분석 작업 시작](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. Hello에 **시작 작업** 작업 출력의 시작 시간을 선택에 대 한 블레이드 **이제**합니다. 

4. **시작**을 클릭합니다. 

    ![Hello 스트림 분석 작업에 대 한 블레이드 "작업을 시작 합니다."](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure 알리는 hello 작업이 시작 되 고으로 표시 되 면 hello 상태 hello 작업 블레이드에서 **실행**합니다.

    ![Stream Analytics 작업 상태, “실행 중” 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>변환 하는 hello 데이터 검사

이제 Streaming Analytics 작업을 완료합니다. hello 작업 전화 통화 메타 데이터의 스트림을 검사, 실시간으로 사기성 전화 통화를 찾고 및 이러한 사기성 호출 toostorage에 대 한 정보를 기록 합니다. 

toocomplete이이 자습서에서는 toolook hello 스트리밍 분석 작업에서 캡처되는 hello 데이터에서 할 수 있습니다. hello 데이터 tooAzure 블로그 저장소 청크 (파일)에 기록 됩니다. Azure Blob Storage를 읽는 데 아무 도구나 사용할 수 있습니다. Hello 전제 조건 섹션에서에서 설명한 대로, Visual Studio에서 Azure 확장을 사용할 수 있습니다 또는 같은 도구를 사용할 수 있습니다 [Azure 저장소 탐색기](http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)합니다. 

Blob 저장소에 파일의 내용을 hello를 살펴보면 hello 다음과 볼 수 있습니다.

![Streaming Analytics 출력이 있는 Azure Blob Storage](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>리소스 정리

Hello 사기 감지 시나리오를 계속 하 고이 자습서에서 만든 hello 리소스를 사용 하는 추가 문서 개가 있습니다. Toocontinue hello 제안 아래를 참조 하십시오 **다음 단계** 나중입니다.

그러나 수행 하는 경우에 만든 hello 리소스를 필요 하지 않습니다 삭제할 수 있습니다 이러한를 불필요 한 요금이 발생 하지 않습니다. 이 경우 다음 hello 수행을 제안 합니다.

1. Hello 스트리밍 분석 작업을 중지 합니다. Hello에 **작업** 블레이드에서 클릭 **중지** hello 위쪽에 있습니다.
2. Hello Telco 생성기 앱을 중지 합니다. Hello 앱을 빠르게 hello 명령 창에서 Ctrl + C를 누릅니다.
3. 이 자습서에 대해 새 Blob Storage 계정을 만든 경우 계정을 삭제합니다. 
4. Hello 스트리밍 분석 작업을 삭제 합니다.
5. Hello 이벤트 허브를 삭제 합니다.
6. Hello 이벤트 허브 네임 스페이스를 삭제 합니다.

## <a name="get-support"></a>지원 받기

추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계

다음 문서는 hello와이 자습서를 진행할 수 있습니다.

* [Stream Analytics 및 Power BI: 스트리밍 데이터에 대한 실시간 분석 대시보드](stream-analytics-power-bi-dashboard.md). 이 문서에서는 toosend hello hello 스트림 분석의 출력을 TelCo tooPower BI 실시간 시각화 및 분석을 위해 작업 하는 방법을 보여 줍니다.
* [어떻게 Azure 함수를 사용 하는 Azure Redis Cache에서 Azure 스트림 분석에서 toostore 데이터](stream-analytics-functions-redis.md)합니다. 이 문서에서는 toouse Azure 함수 toowrite 사기성 tooan Azure Redis 캐시 서비스 버스 큐를 통해 호출 하는 방법을 보여 줍니다.

일반적인 Stream Analytics에 대한 자세한 내용은 다음 문서를 살펴보세요.

* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
