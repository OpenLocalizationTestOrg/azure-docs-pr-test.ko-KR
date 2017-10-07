---
title: "빠른 시작: Azure Machine Learning Recommendations API(버전 1)| Microsoft Docs"
description: "Azure 기계 학습 권장 사항 - 빠른 시작 가이드"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a>Hello 컴퓨터 학습 권장 사항을 API (버전 1)에 대 한 빠른 시작 가이드

> [!NOTE]
> Hello를 사용 하 여 시작 해야 [권장 API Cognitive 서비스](https://www.microsoft.com/cognitive-services/recommendations-api) 이 버전 대신 합니다. hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다. 일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.
>
> 에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)합니다.
> 
> 

이 문서에서는 설명 방법을 tooonboard 서비스 또는 응용 프로그램 toouse Microsoft Azure 시스템 학습 권장 사항입니다. Hello에 권장 사항을 API hello에 자세한 내용을 볼 수 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2)합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>일반 개요
Azure 시스템 학습 권장 사항 toouse tootake hello 단계를 수행 해야 합니다.

* 모델 만들기-모델은 사용 현황 데이터, 카탈로그 데이터와 hello 추천 모델의 컨테이너입니다.
* 데이터 카탈로그 가져오기-카탈로그 hello 항목에 대 한 메타 데이터 정보를 포함합니다. 
* 사용 데이터 가져오기 - 다음 두 가지 방법 중 하나(또는 둘 다)로 사용 데이터를 업로드할 수 있습니다.
  * Hello 사용 현황 데이터를 포함 하는 파일을 업로드 합니다.
  * 데이터 취득 이벤트를 전송합니다.
    일반적으로 순서 toobe 수 toocreate (부트스트랩)는 초기 추천 모델의에서 사용 파일을 업로드 한 hello 시스템 hello 데이터 취득 형식을 사용 하 여 충분 한 데이터가 수집 될 때까지 사용 합니다.
* 추천 모델을 작성-이 작업은 비동기 작업은 hello에서 추천 시스템 모든 hello 사용 현황 데이터를 가져와 추천 모델을 만듭니다. 이 작업에는 몇 분 정도 걸릴 수 있습니다 또는 hello에 따라 몇 시간이 데이터의 크기 hello와 hello 빌드 구성 매개 변수입니다. Hello 빌드를 트리거 id가 빌드 ID가 발생 합니다. Tooconsume 권장 구성을 시작 하기 전에 hello 빌드 프로세스가 종료 되는 경우 toocheck을 사용 합니다.
* 권장 사항 소비 – 특정 항목 또는 항목 목록에 대한 권장 사항을 가져옵니다.

위의 모든 hello 단계 hello Azure 컴퓨터 학습 권장 사항을 API를 통해 수행 됩니다.  각 hello에서 이러한 단계를 구현 하는 예제 응용 프로그램을 다운로드할 수 있습니다 [갤러리 뿐입니다.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>제한 사항
* 구독 당 모델의 hello 최대 수는 10입니다.
* hello 카탈로그를 보유할 수 있는 항목의 최대 수는 100, 000입니다.
* hello 사용 포인트 유지 되는 최대 수에는 ~ 5,000,000는 합니다. 새로 업로드 되거나 보고 되는 경우 가장 오래 된 hello 삭제 됩니다.
* POST (예를 들어 카탈로그 데이터 가져오기 사용 현황 데이터 가져오기)에 보낼 수 있는 데이터의 최대 크기 hello 사항은 200MB입니다.
* hello 활성화 되지 않은 추천 모델 빌드에 대 한 초당 트랜잭션 수는 ~ 2TPS 합니다. 활성화 된 추천 모델 빌드 too20TPS를 보유할 수 있습니다.

## <a name="integration"></a>통합
### <a name="authentication"></a>인증
Microsoft Azure Marketplace hello Basic 또는 OAuth 인증 방법 중 하나를 지원합니다. 쉽게 찾을 수 hello 계정 키 toohello 키 아래에서 hello 시장에서 이동 하 여 [계정 설정을](https://datamarket.azure.com/account/keys)합니다. 

#### <a name="basic-authentication"></a>기본 인증
Hello 권한 부여 헤더를 추가 합니다.

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

TooBase64 변환 (C#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

TooBase64 변환 (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>서비스 URI
hello hello Azure 컴퓨터 학습 권장 사항을 Api에 대 한 서비스 루트 URI는 [여기 합니다.](https://api.datamarket.azure.com/amla/recommendations/v2/)

hello 전체 서비스 URI는 hello OData 사양의 요소를 사용 하 여 표현 됩니다.

### <a name="api-version"></a>API 버전
각 API 호출 갖게 될 예정 hello 끝에 쿼리 라는 매개 변수를 설정 해야 하는 apiVersion 너무 "1.0"입니다.

### <a name="ids-are-case-sensitive"></a>ID 대/소문자 구분
Hello, Api 중 하나에서 반환 된 Id, 대/소문자 및 후속 API 호출에 매개 변수로 전달 된 경우 에서처럼 사용 해야 합니다. 예를 들어 모델 ID와 카탈로그 ID는 대/소문자를 구분합니다.

### <a name="create-a-model"></a>모델 만들기
"모델 만들기" 요청 만들기:

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelName |문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.<br>최대 길이: 20 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

* `feed/entry/content/properties/id`--Hello 모델 ID를 포함 하는 중
  Hello 모델 ID가 대/소문자 구분을 참고 합니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a>카탈로그 데이터 가져오기
여러 가지 카탈로그 파일 toohello 모델 동일한 여러 호출으로 업로드 하는 경우만 hello 새 카탈로그 항목 삽입 됩니다. 기존 항목 hello 원래 값으로 유지 됩니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |(대/소문자 구분) hello 모델의 고유 식별자 |
| filename |Hello 카탈로그의 텍스트 식별자입니다.<br>문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.<br>최대 길이: 50 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |카탈로그 데이터. 형식:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Name</th><th>필수</th><th>형식</th><th>설명</th></tr><tr><td>항목 ID</td><td>예</td><td>영숫자, 최대 길이 50</td><td>항목의 고유 식별자</td></tr><tr><td>Item Name</td><td>예</td><td>영숫자, 최대 길이 255</td><td>항목 이름</td></tr><tr><td>Item Category</td><td>예</td><td>영숫자, 최대 길이 255</td><td>(예: 요리 책 드라마...)이 항목이 속한 범주 toowhich</td></tr><tr><td>설명</td><td>아니요</td><td>영숫자, 최대 길이 4000</td><td>이 항목에 대한 설명</td></tr></table><br>최대 파일 크기는 200MB입니다.<br><br>예제:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**응답**:

HTTP 상태 코드: 200

* `Feed\entry\content\properties\LineCount` – 허용되는 줄 수
* `Feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a>사용 데이터 가져오기
#### <a name="uploading-a-file"></a>파일 업로드
이 섹션에서는 어떻게 tooupload 사용 현황 데이터 파일을 사용 하 여 합니다. 사용 데이터를 사용하여 이 API를 여러 번 호출할 수 있습니다. 모든 호출에 대한 모든 사용 데이터가 저장됩니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |(대/소문자 구분) hello 모델의 고유 식별자 |
| filename |Hello 카탈로그의 텍스트 식별자입니다.<br>문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.<br>최대 길이: 50 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |사용 데이터. 형식:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Name</th><th>필수</th><th>형식</th><th>설명</th></tr><tr><td>User Id</td><td>예</td><td>영숫자</td><td>사용자의 고유 식별자</td></tr><tr><td>항목 ID</td><td>예</td><td>영숫자, 최대 길이 50</td><td>항목의 고유 식별자</td></tr><tr><td>Time</td><td>아니요</td><td>날짜(형식): YYYY/MM/DDTHH:MM:SS(예: 2013/06/20T10:00:00)</td><td>데이터의 시간</td></tr><tr><td>이벤트</td><td>아니요. 지정하는 경우 날짜도 입력해야 함</td><td>Hello 다음 중 하나입니다.<br>• Click<br>• RecommendationClick<br>•    AddShopCart<br>• RemoveShopCart<br>• Purchase</td><td></td></tr></table><br>최대 파일 크기는 200MB입니다.<br><br>예제:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**응답**:

HTTP 상태 코드: 200

* `Feed\entry\content\properties\LineCount` – 허용되는 줄 수
* `Feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.
* `Feed\entry\content\properties\FileId` – 파일 식별자

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a>데이터 취득 사용
이 섹션에서는 real에서 toosend 이벤트 웹 사이트에서 일반적으로 tooAzure 시스템 학습 권장 사항으로 하는 방법을 보여 줍니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| 요청 본문 |이벤트 데이터 입력 원하는 toosend 각 이벤트에 대 한 합니다. Hello 동일한 사용자 또는 브라우저 세션 hello hello 세션 Id 필드에 동일한 ID에 대 한 보내야 합니다. 아래 이벤트 본문 샘플을 참조하세요. |

* 'Click' 이벤트의 예:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* 'RecommendationClick' 이벤트의 예:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* 'AddShopCart' 이벤트의 예:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* 'RemoveShopCart' 이벤트의 예:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* 'Purchase' 이벤트의 예:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* 두 개의 이벤트 'Click' 및 'AddShopCart'를 보내는 예:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**응답**: HTTP 상태 코드: 200

### <a name="build-a-recommendation-model"></a>권장 사항 모델 작성
| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |(대/소문자 구분) hello 모델의 고유 식별자 |
| userDescription |Hello 카탈로그의 텍스트 식별자입니다. 공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다. 위 예제를 참조하세요.<br>최대 길이: 50 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

비동기 API입니다. 응답으로 빌드 ID가 제공됩니다. hello 빌드 끝나면 tooknow, 해야 hello "Get 빌드 상태의 정도 모델" API를 호출 하 고 배치할 있습니다 hello 응답에서이 빌드 ID입니다. Note 빌드 hello hello 데이터 크기에 따라 분 toohours에서 사용할 수 있습니다.

Hello 빌드 끝까지 권장 사항을 소비할 수 없습니다.

유효한 빌드 상태:

* Create – 모델을 만듦
* Queued – 모델 빌드가 트리거되고 쿼리됨
* Building – 모델을 빌드하는 중
* Success – 빌드가 성공적으로 종료됨
* Error – 오류로 인해 빌드가 종료됨
* Canceled – 빌드가 취소됨
* Canceling – 빌드 취소 중

Note는 hello 빌드 경로 따라 hello에서 ID를 찾을 수 있습니다.`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a>모델의 빌드 상태 가져오기
| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |(대/소문자 구분) hello 모델의 고유 식별자 |
| onlyLastBuild |나타냅니다 hello 모든 tooreturn hello 모델의 기록 빌드할지 hello 가장 최근 빌드의 유일한 hello 상태입니다. |
| apiVersion |1.0 |

**응답**:

HTTP 상태 코드: 200

hello 응답 빌드 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `feed/entry/content/properties/UserName`– Hello 사용자의 이름입니다.
* `feed/entry/content/properties/ModelName`– Hello 모델의 이름입니다.
* `feed/entry/content/properties/ModelId` – 모델의 고유 식별자
* `feed/entry/content/properties/IsDeployed`– Hello 빌드 (규칙 하위 배포 여부 활성 빌드)
* `feed/entry/content/properties/BuildId` – 빌드의 고유 식별자
* `feed/entry/content/properties/BuildType`-Hello 빌드의 형식입니다.
* `feed/entry/content/properties/Status` – 빌드 상태 Hello 다음 중 하나일 수 있습니다: 오류, 건물, 대기, 취소, 취소 됨, 성공
* `feed/entry/content/properties/StatusMessage`– 자세한 상태 메시지 (toospecific 상태에만 적용 됨).
* `feed/entry/content/properties/Progress` – 빌드 진행률(%)
* `feed/entry/content/properties/StartTime` – 빌드 시작 시간
* `feed/entry/content/properties/EndTime` – 빌드 종료 시간
* `feed/entry/content/properties/ExecutionTime` – 빌드 기간
* `feed/entry/content/properties/ProgressStep`– 빌드가 진행 중인 hello 현재 단계에 대 한 세부 정보입니다.

유효한 빌드 상태:

* Created – 빌드 요청 항목이 만들어짐
* Queued – 빌드 요청이 트리거되었으며 큐에 대기됨
* Building – 빌드가 진행 중임
* Success – 빌드가 성공적으로 종료됨
* Error – 오류로 인해 빌드가 종료됨
* Canceled – 빌드가 취소됨
* Canceling – 빌드 취소 중

유효한 빌드 형식 값:

* Rank - 순위 빌드 (순위에 대 한 빌드 정보, toohello "컴퓨터 학습 권장 API 설명서" 문서를 참조 하십시오.)
* Recommendation - 권장 사항 빌드
* Fbt - 자주 함께 구매됨 빌드

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a>권장 사항 가져오기
| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |(대/소문자 구분) hello 모델의 고유 식별자 |
| itemIds |쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다.<br>최대 길이: 1024 |
| numberOfResults |필요한 결과 수  |
| includeMetatadata |나중에 사용, 항상 false |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id` - 권장된 항목 ID
* `Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

OData XML

아래 예제 응답 hello 10 개 권장된 항목이 포함 됩니다.

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a>모델 업데이트
Hello 모델 설명을 업데이트 하거나 hello 활성 빌드 id입니다.
*활성 빌드 ID* – 모든 모델에 대한 모든 빌드에는 빌드 ID가 있습니다. hello 활성 빌드 ID는 모든 새 모델의 첫 번째 성공한 빌드의 hello입니다. 활성 빌드 ID 있고 hello에 대 한 추가 빌드 작업을 수행한 후 동일한 모델을 해야 tooexplicitly가 hello 기본 빌드 ID 하려면으로 설정 합니다. 사용 하면 권장 사항, toouse, 하나의 자동으로 사용 됩니다 하는 hello 기본 원하는 hello 빌드 ID를 지정 하지 않습니다.

이 메커니즘을 사용 하면 추천 모델이 프로덕션-toobuild 새 모델에에서 있는 하 고 테스트 하 여 이러한 수준을 올리기 전에 tooproduction-있습니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| id |(대/소문자 구분) hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>참고 설명과 ActiveBuildId 해당 hello XML 태그는 선택 사항입니다. 설명 또는 ActiveBuildId tooset 하지 않으려면 hello 전체 태그를 제거 합니다. |

**응답**:

HTTP 상태 코드: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>법적 정보
이 문서는 "있는 그대로" 제공됩니다. URL 및 기타 인터넷 웹 사이트 참조를 포함하여 본 문서에 명시된 정보 및 보기는 통지 없이 변경될 수 있습니다. 여기에서 설명하는 일부 예는 설명 목적으로만 제공되는 가상의 예이며, 어떠한 실제 사례와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다. 이 문서에서는 있습니다 법적 권리도 tooany Microsoft 제품의 지적 재산입니다. 이 문서는 내부 참조용으로만 복사 및 사용할 수 있습니다. © 2014 Microsoft. All rights reserved. 

