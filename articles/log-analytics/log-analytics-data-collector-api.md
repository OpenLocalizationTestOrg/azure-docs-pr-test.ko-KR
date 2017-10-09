---
title: "분석 HTTP 데이터 수집기 API aaaLog | Microsoft Docs"
description: "Hello 로그 분석 HTTP 데이터 수집기 API tooadd POST JSON 데이터 toohello 로그 분석 저장소 hello REST API를 호출할 수 있는 모든 클라이언트에서 사용할 수 있습니다. 이 문서에서는 설명 방법을 toouse API hello 방법의 예제는 다양 한 프로그래밍 언어를 사용 하 여 toopublish 데이터입니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>데이터 수집기 API HTTP hello로 데이터 tooLog 분석 보내기
이 문서에서는 toouse REST API 클라이언트에서 HTTP 데이터 수집기 API toosend 데이터 tooLog 분석 hello 하는 방법을 설명 합니다.  스크립트나 응용 프로그램에 의해 수집 된 tooformat 데이터는 요청에 포함 하 고 로그 분석의 승인을 요청 하는 방법을 설명 합니다.  PowerShell, C# 및 Python에 예가 제공됩니다.

## <a name="concepts"></a>개념
REST API를 호출할 수 있는 모든 클라이언트에서 hello HTTP 데이터 수집기 API toosend 데이터 tooLog 분석을 사용할 수 있습니다.  이 runbook을 수 있습니다 관리에서 수집 하는 Azure 자동화에서 데이터에서 Azure 또는 다른 클라우드 또는 것 수 tooconsolidate 로그 분석을 사용 하는 다른 관리 시스템 하며 데이터를 분석 합니다.

Hello 로그 분석 저장소의 모든 데이터는 특정 레코드 종류를 사용 하 여 레코드로 저장 됩니다.  JSON의 여러 레코드도 데이터 toosend toohello HTTP 데이터 수집기 API를 지정합니다.  Hello 데이터를 전송할 때 개별 레코드 hello 요청 페이로드의 각 레코드에 대 한 hello 리포지토리에 만들어집니다.


![HTTP 데이터 수집기 개요](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>요청 만들기
toouse hello HTTP 데이터 수집기 API hello 데이터 toosend에서 개체 JSON (JavaScript Notation)을 포함 하는 POST 요청을 만들 있습니다.  각 요청에 필요한 다음 세 개의 테이블 목록 hello 특성 hello 합니다. 각 특성 hello 문서의 뒷부분에 자세히 설명 합니다.

### <a name="request-uri"></a>요청 URI
| 특성 | 속성 |
|:--- |:--- |
| 메서드 |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| 콘텐츠 형식 |application/json |

### <a name="request-uri-parameters"></a>URI 매개 변수 요청
| 매개 변수 | 설명 |
|:--- |:--- |
| CustomerID |hello hello Microsoft Operations Management Suite 작업 영역에 대 한 고유 식별자입니다. |
| 리소스 |hello API 리소스 이름: / api/로그입니다. |
| API 버전 |이 요청으로 hello API toouse의 hello 버전입니다. 현재 2016-04-01입니다. |

### <a name="request-headers"></a>헤더 요청
| 헤더 | 설명 |
|:--- |:--- |
| 권한 부여 |hello 권한 부여 서명입니다. Hello 문서의 뒷부분에 나오는 방법에 대 한 읽을 수 있습니다는 hmac-sha256 toocreate 헤더입니다. |
| Log-Type |전송 하는 hello 데이터의 hello 레코드 종류를 지정 합니다. 현재 hello 로그 형식은 영숫자 문자로 지원합니다. 숫자 또는 특수 문자는 지원되지 않습니다. |
| x-ms-date |hello 날짜 RFC 1123 형식으로 해당 hello 요청이 처리 되었습니다. |
| time-generated-field |hello 데이터 항목의 hello 타임 스탬프를 포함 하는 hello 데이터에 있는 필드의 hello 이름입니다. 필드를 지정하면 그 내용이 **TimeGenerated**에 사용됩니다. 이 필드를 지정 하지 않으면 hello에 대 한 기본 **TimeGenerated** hello 시간에는 해당 hello 메시지는 수집 된 합니다. hello 메시지 필드의 내용을 hello hello ISO 8601 형식 따라야 합니다.-m M-DDThh:mm:ssZ 합니다. |

## <a name="authorization"></a>권한 부여
모든 요청 toohello 로그 분석 데이터 수집기 API HTTP 권한 부여 헤더를 포함 해야 합니다. 요청을 tooauthenticate 주 hello 또는 hello hello 요청을 수행 하는 hello 작업 영역에 대 한 보조 키 중 하나를 사용 하 여 hello 요청에 서명 해야 합니다. 그런 다음 해당 서명 hello 요청의 일부분으로 전달 합니다.   

다음은 hello 권한 부여 헤더에 대 한 hello 형식이입니다.

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* hello hello Operations Management Suite 작업 영역에 대 한 고유 식별자입니다. *서명* 는 [HMAC 해시 기반 메시지 인증 코드 ()](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) 있는 hello 요청에서 구현 되 고 다음 hello를 사용 하 여 계산 [SHA256 알고리즘](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx)합니다. 그런 다음 Base64 인코딩을 사용하여 인코딩합니다.

이 형식 tooencode hello를 사용 하 여 **에서 SharedKey** 서명 문자열:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

서명 문자열의 예는 다음과 같습니다.

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Hello 서명 문자열을 사용 하 여 인코딩할를 보유 하는 경우 hello u t F-8로 인코딩된 문자열에서 hmac-sha256 알고리즘 hello 하 고 Base64 hello 결과 인코딩하십시오. 이 형식을 사용합니다.

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

hello 샘플 hello 다음 섹션의 샘플 코드 toohelp 권한 부여 헤더를 만들 수 있으며

## <a name="request-body"></a>요청 본문
hello hello 메시지 본문은 JSON에 있어야 합니다. 이 형식으로 hello 속성 이름 및 값 쌍이 있는 레코드를 하나 이상 포함 되어야.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

형식에 따라 hello를 사용 하 여 단일 요청에서 함께 여러 레코드를 일괄 처리할 수 있습니다. 모든 hello 레코드 hello 여야 합니다. 동일한 레코드 종류입니다.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>레코드 유형 및 속성
Hello 로그 분석 HTTP 데이터 수집기 API를 통해 데이터를 전송할 때에 사용자 지정 레코드 종류를 정의 합니다. 현재, 다른 데이터 형식 및 솔루션에 의해 생성 된 레코드 종류 tooexisting 데이터를 쓸 수 없습니다. 로그 분석 hello 들어오는 데이터를 읽고 하 한 다음 입력 한 hello 값의 hello 데이터 형식과 일치 하는 속성을 만듭니다.

로그 분석 API를 포함 해야 하는 각 요청 toohello는 **로그 유형** hello 레코드 종류에 대 한 hello 이름 가진 헤더가 있습니다. hello 접미사 **_CL** toodistinguish 다른 로그에서 사용자 지정 로그도 형식을 입력 하면 자동으로 추가 된 toohello 이름입니다. 예를 들어, hello 이름을 입력 하면 **MyNewRecordType**, 로그 분석 hello 형식을 가진 레코드를 만듭니다. **MyNewRecordType_CL**합니다. 이렇게 하면 사용자가 만든 형식 이름과 Microsoft가 현재 또는 향후에 포함한 이름 사이의 충돌을 방지할 수 있습니다.

tooidentify 속성의 데이터 형식, 로그 분석 접미사 toohello 속성 이름을 추가 합니다. 속성에 null 값이 있으면 hello 속성 해당 레코드에 포함 되지 않습니다. 이 표에서 hello 속성 데이터 형식 및 해당 접미사를 보여 줍니다.

| 속성 데이터 형식 | 접미사 |
|:--- |:--- |
| 문자열 |_s |
| Boolean |_b |
| Double |_d |
| 날짜/시간 |_t |
| GUID |_g |

각 속성에 대 한 로그 분석을 사용 하는 hello 데이터 형식을 hello 레코드 종류 hello 새 레코드에 대해 이미 존재 하는지 여부에 따라 달라 집니다.

* 로그 분석 hello 레코드 종류가 없는 경우 새 브러시를 만듭니다. 로그 분석 hello 새 레코드에 대 한 각 속성에 대 한 hello JSON 형식 유추 toodetermine hello 데이터 형식을 사용합니다.
* Hello 레코드 종류가 있으면 로그 분석 toocreate 기존 속성에 따라 새 레코드를 시도 합니다. Hello hello 새 레코드의 속성에 대 한 데이터 형식 및 하지 않는 경우 일치 하 고 없습니다 기존 형식, 변환 된 toohello 수 경우 hello 존재 하지 않는 속성을 포함 하는 레코드, 로그 분석의 새 속성을 만들고 hello 관련 접미사를 포함 수 있습니다.

예를 들어, 이 제출 항목은 **number_d**, **boolean_b**, **string_s** 등의 세 가지 속성이 있는 레코드를 만듭니다.

![샘플 레코드 1](media/log-analytics-data-collector-api/record-01.png)

다음 문자열 형식으로 지정 하는 모든 값이 다음 항목을 제출 하는 경우에 hello 속성 변경 되지 않습니다. 이러한 값에 변환 된 tooexisting 데이터 형식이 될 수 있습니다.

![샘플 레코드 2](media/log-analytics-data-collector-api/record-02.png)

하지만 그런 다음이 다음 전송을 수행한 경우 로그 분석은 hello 새 속성을 만들 **boolean_d** 및 **string_d**합니다. 이 값은 변환할 수 없습니다.

![샘플 레코드 3](media/log-analytics-data-collector-api/record-03.png)

로그 분석은 세 가지 속성 사용 레코드를 만듭니다 hello hello 레코드 종류를 만들기 전에 항목을 다음에 다음 제출 **number_s**, **boolean_s**, 및 **string_s**. 이 항목에서 문자열로 형식이 각 hello 초기 값:

![샘플 레코드 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>데이터 제한
로그 분석 데이터 컬렉션 API toohello 게시 hello 데이터에 대 한 몇 가지 제약 조건이 있습니다.

* 30MB post tooLog 분석 데이터 수집기 API 당 최대입니다. 이는 단일 게시물에 대한 크기 제한입니다. 경우 30 MB를 초과 하는 단일 게시에서 hello 데이터를 분할 해야 hello 데이터 크기의 toosmaller 분할 하 고 동시에 보내야 합니다.
* 최대 32KB의 필드 값 제한. Hello 필드 값 32KB 보다 클 경우 hello 데이터가 잘립니다.
* 지정된 형식의 권장되는 최대 필드 수는 50개입니다. 이는 사용 편의성 및 검색 환경 관점에서의 실용적인 제한입니다.  

## <a name="return-codes"></a>반환 코드
HTTP 상태 코드 200 hello 처리를 위해 해당 hello 요청을 수신 했음을 의미 합니다. 이 hello 작업이 성공적으로 완료를 나타냅니다.

이 표에서 hello hello 서비스를 반환할 수 있는 상태 코드의 전체 집합을 보여 줍니다.

| 코드 | 가동 상태 | 오류 코드 | 설명 |
|:--- |:--- |:--- |:--- |
| 200 |확인 | |hello 요청이 성공적으로 수락 되었습니다. |
| 400 |잘못된 요청 |InactiveCustomer |작업 영역 hello 종료 되었습니다. |
| 400 |잘못된 요청 |InvalidApiVersion |지정한 hello API 버전 hello 서비스에서 인식할 수 없습니다. |
| 400 |잘못된 요청 |InvalidCustomerId |지정 된 hello 작업 영역 ID 올바르지 않습니다. |
| 400 |잘못된 요청 |InvalidDataFormat |잘못된 JSON이 제출되었습니다. hello 응답 본문 tooresolve 오류 hello 하는 방법에 대 한 자세한 내용은 포함 될 수 있습니다. |
| 400 |잘못된 요청 |InvalidLogType |hello 로그 형식이 포함 된 특수 문자 또는 숫자를 지정 합니다. |
| 400 |잘못된 요청 |MissingApiVersion |hello API 버전이 지정 되지 않았습니다. |
| 400 |잘못된 요청 |MissingContentType |hello 콘텐츠 형식이 지정 되지 않았습니다. |
| 400 |잘못된 요청 |MissingLogType |hello 값 로그 형식이 지정 되지 않은 필요 합니다. |
| 400 |잘못된 요청 |UnsupportedContentType |hello 콘텐츠 형식이 너무 설정 되지 않았습니다.**응용 프로그램/json**합니다. |
| 403 |사용할 수 없음 |InvalidAuthorization |hello 서비스 tooauthenticate hello 요청을 하지 못했습니다. 해당 hello 작업 영역 ID 및 연결 키 올바른지 확인 하십시오. |
| 404 |찾을 수 없음 | | 제공 된 hello URL 잘못 되었거나 hello 요청이 너무 많습니다. |
| 429 |너무 많은 요청 | | hello 서비스 계정에서 데이터 양이 많기 발생 합니다. Hello 요청을 나중에 다시 시도 하십시오. |
| 500 |내부 서버 오류 |UnspecifiedError |hello 서비스 내부 오류가 발생 했습니다. Hello 요청을 다시 시도 하십시오. |
| 503 |서비스를 사용할 수 없음 |ServiceUnavailable |hello 서비스는 현재 사용할 수 없는 tooreceive 요청입니다. 요청을 다시 시도하세요. |

## <a name="query-data"></a>쿼리 데이터
로그 분석 HTTP 데이터 수집기 API, 검색 된 레코드에 대 한 hello 제출한 tooquery 데이터 **형식** 같은 toohello 즉 **LogType** 추가 되므로 사용자가 지정한 값 **_CL**. 예를 들어, **MyCustomLog**를 사용한 경우**Type=MyCustomLog_CL**을 갖는 모든 레코드를 반환합니다.

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>샘플 요청
Hello의 다음 섹션에서 방법 보여 주는 예제를 찾을 수 있습니다 다른 프로그래밍 언어를 사용 하 여 toosubmit 데이터 toohello 로그 분석 HTTP 데이터 수집기 API입니다.

각 샘플에 대해 다음이 단계를 수행 hello 권한 부여 헤더에 대 한 tooset hello 변수:

1. Hello Operations Management Suite 포털에서 선택 hello **설정** 타일을 선택한 후 hello **연결 된 원본** 탭 합니다.
2. 오른쪽 toohello **작업 영역 ID**hello 복사 아이콘을 선택한 다음 hello ID hello의 hello 값으로 붙여 **고객 ID** 변수입니다.
3. 오른쪽 toohello **기본 키**hello 복사 아이콘을 선택한 다음 hello ID hello의 hello 값으로 붙여 **공유 키** 변수입니다.

또는 hello 로그 유형 및 JSON 데이터에 대 한 hello 변수를 변경할 수 있습니다.

### <a name="powershell-sample"></a>PowerShell 샘플
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>C# 샘플
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Python 샘플
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>다음 단계
- 사용 하 여 hello [로그 검색 API](log-analytics-log-search-api.md) hello 로그 분석 저장소에서 tooretrieve 데이터입니다.
