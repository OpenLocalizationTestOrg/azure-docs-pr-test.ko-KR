---
title: "aaaImport Azure Application Insights에서 사용자 데이터 tooAnalytics | Microsoft Docs"
description: "정적 데이터 toojoin 된 응용 프로그램 원격 분석 가져오거나 분석을 별도 데이터 스트림 tooquery 가져올 합니다."
services: application-insights
keywords: "개방형 스키마, 데이터 가져오기"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Analytics로 데이터 가져오기

모든 테이블 형식 데이터를 가져올 [분석](app-insights-analytics.md), 어느 toojoin 사용 하 여 [Application Insights](app-insights-overview.md) 응용 프로그램에서 원격 분석 또는 별도 스트림으로 분석할 수 있도록 합니다. 분석은 원격 분석의 강력한 쿼리 언어 잘 맞는 tooanalyzing 대용량 타임 스탬프 스트림을입니다.

사용자 고유의 스키마를 사용하여 Analytics로 데이터를 가져올 수 있습니다. 요청 또는 추적 같은 toouse hello 표준 Application Insights 스키마 되어 있지 않습니다.

JSON 또는 DSV(구분 기호 쉼표, 세미콜론 또는 탭으로 구분된 값) 파일을 가져올 수 있습니다.

가지 tooAnalytics 가져오기는 유용한 세 가지 상황이 있습니다.

* **앱 원격 분석에 연결** 예를 들어 Url에서 웹 사이트 toomore 읽을 수 있는 페이지 제목에 매핑하는 테이블을 가져올 수 있습니다. 분석에서 웹 사이트의 hello 10 개의 가장 인기 있는 페이지를 보여 주는 대시보드 차트 보고서를 만들 수 있습니다. 이제 hello 페이지 제목 hello Url 대신 표시할 수 있어 합니다.
* **응용 프로그램 원격 분석**과 네트워크 트래픽, 서버 데이터 또는 CDN 로그 파일 등의 다른 소스 간에 상관 관계를 형성합니다.
* **분석 tooa 별도 데이터 스트림에 적용 됩니다.** Application Insights Analytics는 타임스탬프가 스파스 스트림에 잘 작동하는 강력한 도구로, 많은 경우에 SQL보다 훨씬 유용합니다. 다른 소스에서 이러한 스트림이 제공되면 Analytics에서 분석할 수 있습니다.

보내는 데이터 tooyour 데이터 원본을 쉽습니다. 

1. (한 번) 데이터의 '데이터 원본' hello 스키마를 정의 합니다.
2. (주기적으로) 데이터 tooAzure 저장소에 업로드 하 고 새 데이터 수집에 대 한 기다리고 우리 hello REST API toonotify을 호출 합니다. 몇 분 안에 hello 데이터는 분석에서 쿼리를 실행할 수 있습니다.

hello hello 업로드 횟수가 정의 된 사용자에 의해 및 쿼리에 사용할 수 있는 사용자 데이터 toobe 시겠습니까 속도입니다. 1GB 보다 더 않고 더 큰 청크로 구성의 보다 효율적인 tooupload 데이터.

> [!NOTE]
> *다양 한 데이터 원본 tooanalyze 있으세요?* [*사용 하는 것이 좋습니다* logstash *tooship Application Insights로 데이터입니다.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>시작하기 전에

다음 작업을 수행해야 합니다.

1. Microsoft Azure의 Application Insights 리소스.

 * Tooanalyze 다른 원격 분석에서 개별적으로 데이터를 원하는 경우 [새 Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다.
 * 조인 또는 Application Insights로 이미 설정 하는 응용 프로그램에서 원격 분석을 사용 하 여 데이터를 비교 하는 경우 해당 앱에 대 한 hello 리소스를 사용할 수 있습니다.
 * 기여자 또는 소유자 액세스 toothat 리소스입니다.
 
2. Azure 저장소의 Blob을 나타냅니다. TooAzure 저장소를 업로드 하 고 분석 여기에서 데이터를 가져옵니다. 

 * Blob에 대한 전용 저장소 계정을 만드는 것이 좋습니다. Blob를 다른 프로세스와 공유 하는 경우 시간이 오래 걸리는 프로세스 tooread 취급에 대 한 blob입니다.


## <a name="define-your-schema"></a>스키마 정의

데이터를 가져올 수 있습니다, 전에 정의 해야는 *데이터 소스* hello 데이터 스키마를 지정 하는 합니다.
Too50 데이터 원본에는 단일 Application Insights 리소스를 만들 수 있습니다.

1. Hello 데이터 원본 마법사를 시작 합니다. "새 데이터 원본 추가" 버튼을 사용합니다. 또는 오른쪽 위 모서리에서 설정 단추를 클릭하고 드롭다운 메뉴에서 "데이터 원본"을 선택합니다.

    ![새 데이터 원본 추가](./media/app-insights-analytics-import/add-new-data-source.png)

    새 데이터 원본의 이름을 제공합니다.

2. 업로드 하는 hello 파일의 형식을 정의 합니다.

    Hello 형식을 수동으로 정의 하거나 샘플 파일을 업로드할 수 있습니다.

    Hello 데이터가 CSV 형식의 이면 hello hello 샘플의 첫 번째 행에 열 머리글 수 있습니다. Hello 다음 단계에서 hello 필드 이름을 변경할 수 있습니다.

    hello 샘플 최소 10 개의 행 이나 데이터의 레코드에 포함 되어야 합니다.

    열 또는 필드 이름은 공백이나 문장 부호 없는 영숫자 이름이어야 합니다.

    ![샘플 파일 업로드](./media/app-insights-analytics-import/sample-data-file.png)


3. 마법사 hello 검토 hello 스키마 이었죠. 샘플에서 hello 형식 유추, 경우에 tooadjust 유추 hello 유형의 hello 열을 할 수 있습니다.

    ![검토 hello 유추 된 스키마](./media/app-insights-analytics-import/data-source-review-schema.png)

 * 선택 사항입니다. 스키마 정의를 업로드합니다. 다음과 같은 hello 형식을 참조 하십시오.

 * 타임스탬프를 선택합니다. Analytics의 모든 데이터에는 타임스탬프 필드가 있어야 합니다. 형식이 있어야 `datetime`, 하지만 'timestamp' 라는 toobe 필요 하지 않습니다. 데이터 ISO 형식으로 시간과 날짜를 포함 하는 열이 있으면 hello 타임 스탬프 열으로 선택 하십시오. 그렇지 않으면 "데이터로 도착"를 선택 하 고 hello 가져오기 프로세스는 타임 스탬프 필드를 추가 합니다.

5. Hello 데이터 원본을 만듭니다.

### <a name="schema-definition-file-format"></a>스키마 정의 파일 형식

UI에 hello 스키마를 편집 하는 대신 hello 스키마 정의 파일에서 로드할 수 있습니다. hello 스키마 정의 형식은 다음과 같습니다. 

구분된 형식 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

JSON 형식 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
각 열은 hello 위치, 이름 및 유형으로 식별 됩니다. 

* 위치 – 구분 기호로 분리 된 파일 형식 지정에 대 한 hello 매핑된 값의 hello 위치는입니다. JSON 형식으로 hello 매핑된 키의 hello jpath입니다.
* 이름-hello hello 열의 이름을 표시 합니다.
* 형식 hello 해당 열의 데이터 형식입니다.
 
샘플 데이터를 사용 하 고 파일 형식을 구분에 경우 hello 스키마 정의 모든 열을 매핑할 하 고 hello 끝에 새 열을 추가 해야 합니다. 

따라서 hello JSON 형식의 스키마 정의 없는 toomap 샘플 데이터에 있는 모든 키, JSON 데이터와 hello 부분 간의 매핑이 있습니다. Hello 샘플 데이터의 일부가 아닌 열은 매핑할 수도 있습니다. 

## <a name="import-data"></a>데이터 가져오기

tooimport 데이터 tooAzure 저장소에 업로드 하 고,에 대 한 선택 키를 만들려면 다음 REST API 호출을 확인 합니다.

![새 데이터 원본 추가](./media/app-insights-analytics-import/analytics-upload-process.png)

설정 자동화 된 시스템 toodo를 일정 한 간격 또는 프로세스를 수동으로 수행 하는 hello를 수행할 수 있습니다. 이 단계를 보려면 toofollow 이러한 tooimport 하려는 데이터의 각 블록에 대 한 합니다.

1. 너무 hello 데이터 업로드[Azure blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다. 

 * Blob를 too1GB 압축 되지 않은 모든 크기 될 수 있습니다. 성능 측면에서는 수백 MB 단위의 큰 blob이 이상적입니다.
 * Gzip tooimprove 업로드 시간 및 hello 데이터 toobe 쿼리를 실행할 수에 대 한 대기 시간을 압축할 수 있습니다. 사용 하 여 hello `.gz` 파일 이름 확장명입니다.
 * 최상의 toouse 별도 저장소 계정을이 목적을 성능이 느려질 수 있으므로 서로 다른 서비스에서 tooavoid 호출 됩니다.
 * 자주 발생 하는 데이터를 보낼 때 몇 초 마다 좋습니다 toouse 두 개 이상의 성능상의 이유로 한 저장소 계정.

 
2. [Hello blob에 대 한 공유 액세스 서명 키를 만들](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)합니다. hello 키 1 일에 만료 기간이 고 읽기 권한을 부여 해야 합니다.
3. REST 호출 toonotify 데이터를 기다리고 있는 Application Insights를 확인 합니다.

 * 끝점: `https://dc.services.visualstudio.com/v2/track`
 * HTTP 메서드: POST
 * 페이로드:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

hello 자리 표시자는:

* `Blob URI with Shared Access Key`: 키를 만들기 위한 hello 프로시저에서 가져옵니다. 특정 toohello blob은
* `Schema ID`: hello에 정의 된 스키마에 대해 생성 된 스키마 ID입니다. 이 blob의 데이터를 hello toohello 스키마를 따라야 합니다.
* `DateTime`: hello 시간은 hello에 요청이 전송 될 UTC입니다. 허용되는 형식: ISO8601(예: "2016-01-01 13:45:01"), RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"), RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"), RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").
* Application Insights 리소스의 `Instrumentation key`

몇 분 후 hello 데이터를 분석에서 사용할 수 있습니다.

## <a name="error-responses"></a>오류 응답

* **400 잘못 된 요청**: 해당 hello 요청 페이로드가 잘못 되었음을 나타냅니다. 다음을 확인하세요.
 * 올바른 계측 키
 * 유효한 시간 값. UTC 이제 hello 시간 이어야 합니다.
 * Hello 이벤트의 JSON toohello 스키마를 준수합니다.
* **403**: 발송 한 hello blob에 액세스할 수 없으면입니다. 그 hello 공유 액세스 키가 유효 하 고 만료 되지 않았는지 확인 합니다.
* **404 찾을 수 없음**:
 * hello blob이 존재 하지 않습니다.
 * hello 원본 Id가 잘못 되었습니다.

더 자세한 정보는 hello 응답 오류 메시지에 있습니다.


## <a name="sample-code"></a>샘플 코드

이 코드 hello를 사용 하 여 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet 패키지 합니다.

### <a name="classes"></a>클래스

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>데이터 수집

각 blob에 대한 이 코드를 사용합니다. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>다음 단계

* [로그 분석 쿼리 언어 hello 둘러보기](app-insights-analytics-tour.md)
* [사용 하 여 *Logstash* toosend 데이터 tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
