---
title: "aaaMachine 학습 권장 사항을 API 설명서 | Microsoft Docs"
description: "Hello Microsoft Azure Marketplace에서에서 제공 하는 권장 엔진에 대 한 azure 컴퓨터 학습 권장 사항을 API 설명서입니다."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Azure 기계 학습 권장 사항 API 설명서
> [!NOTE]
> 이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다. hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다. 일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.
> 에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)
> 
> 

이 문서에서는 Microsoft Azure 기계 학습 권장 사항 API에 대해 설명합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. 일반 개요
이 문서는 API 참조입니다. "Azure 기계 학습 권장-빠른 시작" 문서 hello로 시작 해야 합니다.

hello Azure 컴퓨터 학습 권장 사항을 API hello 논리 그룹을 다음으로 나눌 수 있습니다.

* <ins>제한 사항</ins> - 추천 API 제한 사항입니다.
* <ins>일반 정보</ins> - 인증, 서비스 URI 및 버전 관리에 대한 정보입니다.
* <ins>Basic 모델</ins> -toodo hello 대 한 기본 작업 모델을 사용 하는 Api (예: 만들기, 업데이트 및 삭제는 모델).
* <ins>고급 모델링</ins> -hello 모델에 대 한 고급 tooget 데이터 통찰력을 사용 하는 Api입니다.
* <ins>모델 비즈니스 규칙</ins> -hello 모델 권장 구성 결과에 toomanage 비즈니스 규칙을 사용 하는 Api입니다.
* <ins>카탈로그</ins> -toodo 모델 카탈로그에 대 한 기본 작업을 사용 하는 Api입니다. 카탈로그는 hello 사용 현황 데이터의 hello 항목에 대 한 메타 데이터 정보를 포함합니다.
* <ins>기능</ins> -hello 카탈로그로 tooget 항목에 대 한 통찰력을 사용 하도록 설정 하는 Api와 방법을 toouse이 정보 toobuild 더 나은 권장 합니다.
* <ins>사용 현황 데이터</ins> -toodo hello 모델 사용 현황 데이터에 대 한 기본 작업을 사용 하는 Api입니다. Hello 기본 형태로 사용 현황 데이터의 쌍 &#60; userId &#62; 포함 하는 행으로 이루어진, &#60; itemId &#62;.
* <ins>빌드</ins> -tootrigger 모델을 사용할 수 있는 Api 빌드하고 빌드 관련된 toothis 있는 기본 작업 수행 합니다. 유용한 사용 데이터가 있으면 모델 빌드를 트리거할 수 있습니다.
* <ins>권장 사항</ins> -모델의 hello 빌드가 끝난 후 tooconsume 권장 사항을 수 있는 Api입니다.
* <ins>사용자 데이터</ins> -hello 사용자 사용 현황 데이터에 toofetch 정보를 사용 하는 Api입니다.
* <ins>알림</ins> -Api를 사용 하면 문제에 tooreceive 알림 관련 API tooyour 작업 합니다. (예를 들어 보고 하려는 데이터 취득 및 대부분의 처리 실패 하는 hello 이벤트를 통해 사용 현황 데이터. 오류 알림이 발생합니다.

## <a name="2-limitations"></a>2. 제한 사항
* 구독 당 모델의 hello 최대 수는 10입니다.
* 모델에 대해 빌드의 최대 수 hello은 20입니다.
* hello 카탈로그를 보유할 수 있는 항목의 최대 수는 100, 000입니다.
* hello 사용 포인트 유지 되는 최대 수에는 ~ 5,000,000는 합니다. 새로 업로드 되거나 보고 되는 경우 가장 오래 된 hello 삭제 됩니다.
* POST (예: 카탈로그 데이터 가져오기 사용 현황 데이터 가져오기)에 보낼 수 있는 데이터의 최대 크기 hello 사항은 200MB입니다.
* hello 권장 구성을 가져올 때에 대해 질문할 수 있는 항목의 최대 수는 150입니다.

## <a name="3-apis---general-information"></a>3. API – 일반 정보
### <a name="31-authentication"></a>3.1. 인증
인증 문제에 관한 hello Microsoft Azure 마켓플레이스 지침을 따르세요. hello 마켓플레이스 hello Basic 또는 OAuth 인증 방법 중 하나를 지원합니다.

### <a name="32-service-uri"></a>3.2. 서비스 URI
hello hello Azure 컴퓨터 학습 권장 사항을 Api에 대 한 서비스 루트 URI는 [여기 합니다.](https://api.datamarket.azure.com/amla/recommendations/v3/)

hello 전체 서비스 URI는 hello OData 사양의 요소를 사용 하 여 표현 됩니다.  

### <a name="33-api-version"></a>3.3. API 버전
각 API 호출에 hello 끝에 호출 apiVersion too1.0를 설정 해야 하는 쿼리 매개를 변수가 됩니다.

### <a name="34-ids-are-case-sensitive"></a>3.4. ID 대/소문자 구분
Id, hello Api 중 하나에서 반환 된 대/소문자 구분 및 후속 API 호출에 매개 변수로 전달 된 경우 에서처럼 사용 해야 합니다. 예를 들어 모델 ID와 카탈로그 ID는 대/소문자를 구분합니다.

## <a name="4-recommendations-quality-and-cold-items"></a>4. 권장 사항 품질 및 콜드 항목
### <a name="41-recommendation-quality"></a>4.1. 권장 사항 품질
추천 모델을 만드는 것이 일반적으로 충분 한 tooallow hello 시스템 tooprovide 권장 사항입니다. 그럼에도 불구 하 고 권장 사항은 정확성이 처리 hello 사용량에 따라 다르며 hello hello 카탈로그의 검사 됩니다. 예를 들어 hello 시스템 어려움 이러한 항목에 대 한 권장 사항을 제공 하거나 이러한 항목을 사용 하 여 권장 한 최초 항목 (항목 한 사용 하지 않고) 많을 경우 갖습니다. 순서 tooovercome hello 최초 항목 문제가 hello 시스템에는 hello 항목 tooenhance hello 권장 구성의 메타 데이터의 hello 사용할을 수 있습니다. 이 메타 데이터 참조 tooas 기능입니다. 일반적인 기능은 책의 저자 또는 동영상의 배우입니다. 키/값 문자열 hello 형태로 hello 카탈로그를 통해 기능을 제공 합니다. Hello hello 카탈로그 파일의 전체 포맷을 toohello를 참조 하십시오 [카탈로그 섹션을 가져올](#81-import-catalog-data)합니다. 

### <a name="42-rank-build"></a>4.2. 순위 빌드
기능 hello 추천 모델을 향상 시킬 수 있지만 toodo 하려면 hello 의미 있는 기능을 사용 해야 합니다. 이를 위해 순위 빌드라는 새 빌드가 도입되었습니다. 이 빌드 hello 유용성 기능에 순위를 지정 합니다. 의미 있는 기능은 순위 점수가 2 이상인 기능입니다.
Hello 기능이 있는 의미를 이해 한 후 hello 목록 (또는 하위 목록)의 의미 있는 기능을 사용 하 여 권장 사항 빌드를 트리거하십시오. 것이 가능한 toouse 웜 항목과 최초 항목의 hello 향상 된 기능에 대 한 이러한 기능 합니다. Hello 웜 항목에 대 한 해당 순서 toouse에서 `UseFeatureInModel` 빌드 매개 변수를 설정 해야 합니다. 최초 항목에 대 한 순서 toouse 기능에서 hello `AllowColdItemPlacement` 빌드 매개 변수를 사용 해야 합니다.
참고: 것은 가능한 tooenable `AllowColdItemPlacement` 사용 하지 않고 `UseFeatureInModel`합니다.

### <a name="43-recommendation-reasoning"></a>4.3. 권장 사항 추론
권장 사항 추론은 기능 사용의 또 다른 측면입니다. 실제로, hello Azure 시스템 학습 권장 사항 엔진 צ ְ ײ 기능 tooprovide 권장 사항을 설명 (규칙 하위 추론), toomore 신뢰도 hello에 선행 hello 권장 소비자에서 항목을 권장 합니다.
tooenable 추론을 hello `AllowFeatureCorrelation` 및 `ReasoningFeatureList` 매개 변수는 설치 이전 toorequesting 권장 빌드 이어야 합니다.

## <a name="5-model-basic"></a>5. 모델 기본
### <a name="51-create-model"></a>5.1. 모델 만들기
"모델 만들기" 요청을 만듭니다.

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
  **참고**: 모델 ID는 대/소문자를 구분합니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a>5.2. 모델 가져오기
"모델 가져오기" 요청을 만듭니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| id |(대/소문자 구분) hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

요소 다음 hello에서 hello 모델 데이터를 확인할 수 있습니다.

* `feed/entry/content/properties/Id` – 모델의 고유 ID
* `feed/entry/content/properties/Name` – 모델 이름
* `feed/entry/content/properties/Date` - 모델을 만든 날짜
* `feed/entry/content/properties/Status` – 모델 상태 Hello 다음 중 하나입니다.
  * Created - 모델이 생성되었으며 카탈로그 및 사용 현황을 포함하지 않음
  * ReadyForBuild – 모델이 생성되었으며 카탈로그 및 사용 현황을 포함함
* `feed/entry/content/properties/HasActiveBuild`-Hello 모델이 성공적으로 빌드된 경우를 나타냅니다.
* `feed/entry/content/properties/BuildId` – 모델 활성 빌드 ID
* `feed/entry/content/properties/Mpr` – 모델 평균 백분위수 순위(MPR - 자세한 내용은 ModelInsight 참조)
* `feed/entry/content/properties/UserName` – 모델 내부 사용자 이름

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    모든 모델 가져오기
Hello 현재 사용자의 모든 모델을 검색합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

* `feed/entry/content/properties/Id` – 모델의 고유 ID
* `feed/entry/content/properties/Name` – 모델 이름
* `feed/entry/content/properties/Date` - 모델을 만든 날짜
* `feed/entry/content/properties/Status` – 모델 상태 Hello 다음 중 하나입니다.
  * Created - 모델이 생성되었으며 카탈로그 및 사용 현황을 포함하지 않음
  * ReadyForBuild – 모델이 생성되었으며 카탈로그 및 사용 현황을 포함함
* `feed/entry/content/properties/HasActiveBuild`-Hello 모델이 성공적으로 빌드된 경우를 나타냅니다.
* `feed/entry/content/properties/BuildId` – 모델 활성 빌드 ID
* `feed/entry/content/properties/Mpr` – 모델 MPR(자세한 내용은 ModelInsight 참조)
* `feed/entry/content/properties/UserName` – 모델 내부 사용자 이름
* `feed/entry/content/properties/UsageFileNames` – 쉼표로 구분된 모델 사용 파일 목록
* `feed/entry/content/properties/CatalogId` – 모델 카탈로그 ID
* `feed/entry/content/properties/Description` – 모델 설명
* `feed/entry/content/properties/CatalogFileName` – 모델 카탈로그 파일 이름

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    모델 업데이트
Hello 모델 설명을 업데이트 하거나 hello 활성 빌드 id입니다.<br>
<ins>활성 빌드 ID</ins> – 모든 모델에 대한 모든 빌드에는 빌드 ID가 있습니다. hello 활성 빌드 ID는 모든 새 모델의 첫 번째 성공한 빌드의 hello입니다. 활성 빌드 ID 있고 hello에 대 한 추가 빌드 작업을 수행한 후 동일한 모델을 해야 tooexplicitly가 hello 기본 빌드 ID 하려면으로 설정 합니다. 사용 하면 권장 사항, toouse, 하나의 자동으로 사용 됩니다 하는 hello 기본 원하는 hello 빌드 ID를 지정 하지 않습니다.<br>
이 메커니즘을 사용 하면 추천 모델이 프로덕션-toobuild 새 모델에에서 있는 하 고 테스트 하 여 이러한 수준을 올리기 전에 tooproduction-있습니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| id |(대/소문자 구분) hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>참고 설명과 ActiveBuildId 해당 hello XML 태그는 선택 사항입니다. 설명 또는 ActiveBuildId tooset 하지 않으려면 hello 전체 태그를 제거 합니다. |

**응답**:

HTTP 상태 코드: 200

### <a name="55----delete-model"></a>5.5.    모델 삭제
ID별로 기존 모델을 삭제합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| id |(대/소문자 구분) hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. 모델 고급
### <a name="61----model-data-insight"></a>6.1.    모델 데이터 정보
이 모델 빌드된 hello 사용 현황 데이터에 통계 데이터를 반환 합니다.

권장 사항 빌드에만 사용할 수 있습니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 데이터 속성의 컬렉션으로 반환 됩니다.

* `feed/entry/id/content/properties/key`-Hello 속성 이름을 포함 합니다.
* `feed/entry/id/content/properties/value`-Hello 속성 값을 보유합니다.

hello 다음 표에서 각 키를 나타내는 hello 값을 보여 줍니다.

| 키 | 설명 |
|:--- |:--- |
| AvgItemLength |항목당 평균 고유 사용자 수 |
| AvgUserLength |사용자당 평균 고유 항목 수 |
| DensificationNumberOfItems |모델링할 수 없는 항목을 정리한 후의 항목 수 |
| DensificationNumberOfUsers |모델링할 수 없는 사용자 및 항목을 정리한 후의 사용 포인트 수 |
| DensificationNumberOfRecords |모델링할 수 없는 사용자 및 항목을 정리한 후의 사용 포인트 수 |
| MaxItemLength |Hello 가장 인기 있는 항목에 대 한 고유 사용자 수입니다. |
| MaxUserLength |사용자의 최대 고유 항목 수 |
| MinItemLength |항목의 최대 고유 사용자 수 |
| MinUserLength |사용자의 최소 고유 항목 수 |
| RawNumberOfItems |Hello 사용 파일의 항목 수입니다. |
| RawNumberOfUsers |정리하기 전의 사용 포인트 수 |
| RawNumberOfRecords |정리하기 전의 사용 포인트 수 |
| SamplingNumberOfItems |해당 없음 |
| SamplingNumberOfRecords |해당 없음 |
| SamplingNumberOfUsers |해당 없음 |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    모델 정보
Hello 현재 빌드에 대 한 정보를 모델링 하는 반환 (제공 된 경우) 또는 특정 빌드에 있습니다.

권장 사항 빌드에만 사용할 수 있습니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |활성 빌드 ID 사용:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>특정 빌드 ID 사용:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| buildId |(선택 사항) - 성공적인 빌드를 식별하는 번호 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 데이터 속성의 컬렉션으로 반환 됩니다.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

hello 다음 표에서 각 키를 나타내는 hello 값을 보여 줍니다.

| 키 | 설명 |
|:--- |:--- |
| CatalogCoverage |어떤 부분이 hello 카탈로그의 사용 패턴 모델이 될 수 있습니다. hello rest hello 항목의 콘텐츠 기반 기능 할 수 있습니다. |
| Mpr |Hello 모델의 백분위 수 순위를 의미 합니다. 낮을수록 좋습니다. |
| NumberOfDimensions |Hello 행렬 factorization 알고리즘에서 사용 하는 차원 수 있습니다. |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    모델 샘플 가져오기
Hello 추천 모델의 샘플을 가져옵니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>특정 빌드 ID 사용:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

OData XML

원시 텍스트 형식으로 응답이 반환됩니다.

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. 모델 비즈니스 규칙
다음은 지원 되는 규칙의 hello 유형입니다.

* <strong>차단 목록</strong> -차단 목록 사용 하면 tooprovide hello 권장 구성 결과에서 tooreturn 하지 않을 항목의 목록입니다. 
* <strong>FeatureBlockList</strong> -차단 목록 기능을 사용 하면 있습니다 tooblock 항목 기능 hello 값을 기반으로 합니다.

*단일 차단 목록 규칙에 1000개보다 많은 항목을 전송하지 마세요. 호출 시간 제한에 도달할 수 있습니다. 1000 개 이상의 항목 tooblock 해야 할 경우에 여러 개의 차단 목록 호출을 만들 수 있습니다.*

* <strong>Upsale</strong> -Upsale hello 권장 구성 결과에서 tooenforce 항목 tooreturn을 수 있습니다.
* <strong>화이트 리스트</strong> -tooonly 있습니다 항목의 목록에서 권장 사항을 제안 허용 목록을 사용 합니다.
* <strong>FeatureWhiteList</strong> -기능 허용 목록을 사용 하면 특정 기능 값을 가진 tooonly 권장 되는 항목입니다.
* <strong>PerSeedBlockList</strong> -당 시드 차단 목록 당 tooprovide 권장 결과로 반환할 수 없는 항목의 목록 항목을 사용 하도록 설정 합니다.

### <a name="71----get-model-rules"></a>7.1.    모델 규칙 가져오기
| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>예제:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

* `feed/entry/content/properties/Id` – 이 규칙의 고유 식별자
* `feed/entry/content/properties/Type`Hello 규칙의 형식입니다.
* `feed/entry/content/properties/Parameter` – 규칙 매개 변수

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    규칙 추가
| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| 요청 본문 | |

<ins>비즈니스 규칙에 대 한 항목 Id를 제공 될 때마다 toouse hello hello 항목의 외부 Id가 있는지 확인 하십시오 (hello hello 카탈로그 파일에 사용 되는 동일한 Id)</ins><br>
<ins>tooadd 차단 목록 규칙:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd FeatureBlockList 규칙:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>tooadd Upsale 규칙:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd 허용 목록 규칙:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd FeatureWhiteList 규칙:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>tooadd PerSeedBlockList 규칙:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**응답**:

HTTP 상태 코드: 200

hello API의 세부 정보와 함께 규칙을 새로 만든 hello를 반환 합니다. 경로 따라 hello에서 hello 규칙 속성을 검색할 수 있습니다.

* `feed/entry/content/properties/Id` – 이 규칙의 고유 식별자
* `feed/entry/content/properties/Type`-Hello 규칙의 유형을: Upsale 또는 차단 목록입니다.
* `feed/entry/content/properties/Parameter` – 규칙 매개 변수

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    규칙 삭제
| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>예제:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| filterId |Hello 필터의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

### <a name="74----delete-all-rules"></a>7.4.    모든 규칙 삭제
| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>예제:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

## <a name="8-catalog"></a>8. 카탈로그
### <a name="81----import-catalog-data"></a>8.1.    카탈로그 데이터 가져오기
여러 가지 카탈로그 파일 toohello 모델 동일한 여러 호출으로 업로드 하는 경우만 hello 새 카탈로그 항목 삽입 됩니다. 기존 항목 hello 원래 값으로 유지 됩니다. 이 메서드를 사용하여 카탈로그 데이터를 업데이트할 수 없습니다.

hello 카탈로그 데이터 형식에 따라 hello를 따라야 합니다.

* 기능 사용 안 함 - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* 기능 사용 - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

참고: hello 최대 파일 크기 사항은 200MB입니다.

** 형식 세부 정보 **

| 이름 | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| 항목 ID |예 |[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;<br> 최대 길이: 50 |항목의 고유 식별자 |
| Item Name |예 |영숫자 문자<br> 최대 길이: 255 |항목 이름 |
| Item Category |예 |영숫자 문자 <br> 최대 길이: 255 |범주 toowhich이이 항목이 속하는 (예: 요리 책, 드라마...); 비어 있을 수 있습니다. |
| 설명 |아니요, 기능이 없는 경우(그러나 비어 있을 수 있음) |영숫자 문자 <br> 최대 길이: 4000 |이 항목에 대한 설명 |
| Features list |아니요 |영숫자 문자 <br> 최대 길이: 4000; 최대 기능 수: 20 |기능 이름 쉼표로 구분 된 목록을 사용 하는 tooenhance 모델 권장; 일 수 있는 기능 값 = 참조 [고급 항목](#2-advanced-topics) 섹션. |

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| filename |Hello 카탈로그의 텍스트 식별자입니다.<br>문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.<br>최대 길이: 50 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |예(기능 사용):<br/>2406e770-769 c-4189-89de-1c9283f93a96, 클라라 Callan, 책, hello 책 설명 작성 Richard Wright = 게시자 Harper 홍학 캐나다 = 연도 2001 =<br>21bf8088-b6c0-4509-870 c-e1c7ac78304a, hello Forgetting 룸: A 소설 (비잔티움 책), 책, 작성 Nick Bantock = 게시자 = Harpercollins, 연도 1997 =<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,책,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001<br>552a1940-21e4-4399-82bb-594b46d7ed54, 짐승 지지대, 책, hello 책 설명 작성 Magnus 충당 = 게시자 = 아케이드 게시 연도 1998 =</pre> |

**응답**:

HTTP 상태 코드: 200

hello API hello 가져오기에 대 한 보고서를 반환합니다.

* `feed\entry\content\properties\LineCount` – 허용되는 줄 수
* `feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    카탈로그 가져오기
모든 카탈로그 항목을 검색합니다.
hello 카탈로그 됩니다 한 번에 한 페이지를 검색 합니다. 특정 인덱스에서 tooget 항목을 하려는 경우에 hello $skip odata 매개 변수를 사용할 수 있습니다. 예를 들어 tooget 항목 100 위치에서 시작 하려는 경우 추가 hello 매개 변수 $skip = 100 toohello 요청 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>예제:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 응답에는 카탈로그 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `feed/entry/content/properties/ExternalId`-항목 외부 ID를 카탈로그, hello hello 고객에서 제공 합니다.
* `feed/entry/content/properties/InternalId`카탈로그 항목 내부 ID hello Azure 시스템 학습 권장 사항이 생성 하는 것입니다.
* `feed/entry/content/properties/Name` – 카탈로그 항목 이름
* `feed/entry/content/properties/Category` – 카탈로그 항목 범주
* `feed/entry/content/properties/Description` – 카탈로그 항목 설명
* `feed/entry/content/properties/Metadata` – 카탈로그 항목 메타데이터

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    토큰별 카탈로그 항목 가져오기
| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>예제:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| token |토큰 hello 카탈로그 항목의 이름입니다. 3자 이상 포함해야 합니다. |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 응답에는 카탈로그 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `feed/entry/content/properties/InternalId`카탈로그 항목 내부 ID hello Azure 시스템 학습 권장 사항이 생성 하는 것입니다.
* `feed/entry/content/properties/Name` – 카탈로그 항목 이름
* `feed/entry/content/properties/Rating` - (나중에 사용)
* `feed/entry/content/properties/Reasoning` - (나중에 사용)
* `feed/entry/content/properties/Metadata` - (나중에 사용)
* `feed/entry/content/properties/FormattedRating` - (나중에 사용)

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. 사용 데이터
### <a name="91----import-usage-data"></a>9.1.    사용 데이터 가져오기
#### <a name="911-uploading-file"></a>9.1.1. 파일 업로드
이 섹션에서는 어떻게 tooupload 사용 현황 데이터 파일을 사용 하 여 합니다. 사용 데이터를 사용하여 이 API를 여러 번 호출할 수 있습니다. 모든 호출에 대한 모든 사용 데이터가 저장됩니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| filename |Hello 카탈로그의 텍스트 식별자입니다.<br>문자(A-Z, a-z), 숫자(0-9), 하이픈(-) 및 밑줄(_)만 사용할 수 있습니다.<br>최대 길이: 50 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |사용 데이터. 형식:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Name</th><th>필수</th><th>형식</th><th>설명</th></tr><tr><td>User Id</td><td>예</td><td>[A-z], [a-z], [0-9], [_] &#40;밑줄&#41;, [-] &#40;Dash&#41;<br> 최대 길이: 255 </td><td>사용자의 고유 식별자입니다.</td></tr><tr><td>항목 ID</td><td>예</td><td>[A-z], [a-z], [0-9], [&#95;] &#40;밑줄&#41;, [-] &#40;대시&#41;<br> 최대 길이: 50</td><td>항목의 고유 식별자</td></tr><tr><td>Time</td><td>아니요</td><td>날짜(형식): YYYY/MM/DDTHH:MM:SS(예: 2013/06/20T10:00:00)</td><td>데이터의 시간입니다.</td></tr><tr><td>이벤트</td><td>아니요. 지정하는 경우 날짜도 입력해야 함</td><td>Hello 다음 중 하나입니다.<br>• Click<br>• RecommendationClick<br>•    AddShopCart<br>• RemoveShopCart<br>• Purchase</td><td></td></tr></table><br>최대 파일 크기 200MB<br><br>예제:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**응답**:

HTTP 상태 코드: 200

* `Feed\entry\content\properties\LineCount` – 허용되는 줄 수
* `Feed\entry\content\properties\ErrorCount`-Tooan 오류 때문에 삽입 되지 않은 줄 수입니다.
* `Feed\entry\content\properties\FileId` – 파일 식별자

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. 데이터 취득 사용
이 섹션에서는 real에서 toosend 이벤트 웹 사이트에서 일반적으로 tooAzure 시스템 학습 권장 사항으로 하는 방법을 보여 줍니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| apiVersion |1.0 |
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
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
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

### <a name="92----list-model-usage-files"></a>9.2.    모델 사용 파일 나열
모든 모델 사용 파일의 메타데이터를 검색합니다.
hello 사용 파일 됩니다 한 페이지 한 번에 검색할 합니다. 각 페이지는 100개의 항목을 포함합니다. 특정 인덱스에서 tooget 항목을 하려는 경우에 hello $skip odata 매개 변수를 사용할 수 있습니다. 예를 들어 tooget 항목 100 위치에서 시작 하려는 경우 추가 hello 매개 변수 $skip = 100 toohello 요청 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| forModelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 응답에는 사용 현황 파일 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `feed\entry\content\properties\Id` – 사용 파일 ID
* `feed\entry\content\properties\Length` – 사용 파일 길이(MB)
* `feed\entry\content\properties\DateModified`-Hello 사용 현황 파일을 만든 날짜
* `feed\entry\content\properties\UseInModel`-여부 hello 사용 현황 파일 hello 모델에 사용 됩니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    사용 통계 가져오기
사용 통계를 가져옵니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| startDate |시작 날짜입니다. 형식: yyyy/MM/ddTHH:mm:ss |
| endDate |종료 날짜입니다. 형식: yyyy/MM/ddTHH:mm:ss |
| eventTypes |이벤트의 쉼표로 구분 된 문자열 또는 null tooget 모든 이벤트 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

키/값 요소의 컬렉션입니다. 각각 hello 합계의 시간별 특정 이벤트 유형의 이벤트를 포함 합니다.

* `feed\entry[i]\content\properties\Key`-(시간별) hello 시간을 포함 합니다. 및 hello 이벤트 유형입니다.
* `feed\entry[i]\content\properties\Value` - 총 이벤트 수

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    사용 파일 샘플 가져오기
검색 사용 파일 콘텐츠의 첫 번째 2KB hello 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| fileId |Hello 모델 사용 파일의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

원시 텍스트 형식으로 응답이 반환됩니다.

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    모델 사용 파일 가져오기
Hello hello 사용 파일의 전체 콘텐츠를 검색합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| mId |Hello 모델의 고유 식별자 |
| fid |Hello 모델 사용 파일의 고유 식별자 |
| 다운로드 |1 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

원시 텍스트 형식으로 응답이 반환됩니다.

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    사용 파일 삭제
Hello 지정 된 모델 사용 현황 파일을 삭제합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| fileId |Hello 파일 toobe 삭제의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

### <a name="97----delete-all-usage-files"></a>9.7.    모든 사용 파일 삭제
모든 모델 사용 파일을 삭제합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

## <a name="10-features"></a>10. 기능
이 섹션에서는 어떻게 tooretrieve 가져온 hello 기능 및 해당 값, 해당 순위 등의 정보 있을 수 있으며이 순위 할당 된 경우를 보여 줍니다. 기능에서 가져온 hello 카탈로그 데이터의 한 다음 차수 관련 순위 빌드가 수행 되는 경우.
기능 순위에 따라 toohello 패턴의 사용량 데이터 및 항목의 형식을 변경할 수 있습니다. 하지만 hello 순위 일관 된 사용 현황/항목에 대 한 약간의 변동이 있어야 합니다.
기능의 hello 순위 음수가 아닌 숫자입니다. hello 숫자 0 의미 hello 기능을 순위가 지정 되지 않습니다 (첫 번째 순위 빌드 hello이 API 이전 toohello 완료를 호출 하는 경우 수행 됨). hello 날짜 hello 순위 특성이 지정 된 점수 freshness hello 라고 합니다.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. 기능 정보 가져오기(마지막 순위 빌드)
마지막으로 성공한 순위 빌드 hello에 대 한 순위 등의 hello 기능 정보를 검색 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| samplingSize |Hello 카탈로그에 있는 toohello 데이터에 따라 각 기능에 대해 tooinclude 값의 수입니다. <br/>가능한 값은 다음과 같습니다.<br> -1 - 모든 샘플. <br>0 - 샘플링 없음. <br>N - 각 기능 이름별로 N개의 샘플 반환. |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 응답 기능 정보 항목의 목록을 포함합니다. 각 항목에는 다음이 포함됩니다.

* `feed/entry/content/m:properties/d:Name` - 기능 이름
* `feed/entry/content/m:properties/d:RankUpdateDate`-순위는 hello에 할당 된 toothis 기능 라고도 함 된 날짜 점수 유효 시간) 과거 날짜('0001-01-01T00:00:00')는 순위 빌드가 수행되지 않았음을 나타냅니다.
* `feed/entry/content/m:properties/d:Rank` - 기능 순위(부동 소수점). 2.0 이상의 순위가 유용한 기능으로 간주됩니다.
* `feed/entry/content/m:properties/d:SampleValues`-쉼표로 구분 된 목록 toohello 샘플링 크기 요청 값입니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. 기능 정보 가져오기(특정 순위 빌드)
Hello 특정 순위 빌드에 대 한 순위 등의 hello 기능 정보를 검색 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| samplingSize |Hello 카탈로그에 있는 toohello 데이터에 따라 각 기능에 대해 tooinclude 값의 수입니다.<br/> 가능한 값은 다음과 같습니다.<br> -1 - 모든 샘플. <br>0 - 샘플링 없음. <br>N - 각 기능 이름별로 N개의 샘플 반환. |
| rankBuildId |Hello 순위 빌드 또는 hello 마지막 순위 빌드에 대 한-1의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

hello 응답 기능 정보 항목의 목록을 포함합니다. 각 항목에는 다음이 포함됩니다.

* `feed/entry/content/m:properties/d:Name` - 기능 이름
* `feed/entry/content/m:properties/d:RankUpdateDate`-순위는 hello에 할당 된 toothis 기능 라고도 함 된 날짜 점수 유효 시간) 과거 날짜('0001-01-01T00:00:00')는 순위 빌드가 수행되지 않았음을 나타냅니다.
* `feed/entry/content/m:properties/d:Rank` - 기능 순위(부동 소수점). 2.0 이상의 순위가 유용한 기능으로 간주됩니다.
* `feed/entry/content/m:properties/d:SampleValues`-쉼표로 구분 된 목록 toohello 샘플링 크기 요청 값입니다.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. 빌드
  이 섹션에서는 hello toobuilds와 관련 된 다른 Api입니다. 세 가지 유형의 빌드(권장 사항 빌드, 순위 빌드 및 FBT(자주 함께 구매됨) 빌드)가 있습니다.

hello 권장 빌드 목적은 toogenerate 예측에 사용 되는 추천 모델입니다. 예측(이 유형의 빌드 관련)은 다음 두 가지 유형으로 제공됩니다.

* I2I 항목 목록 또는 항목을 제공 된 tooItem 권장 사항을-항목의이 옵션을 예측 하는 가능성이 toobe 높은 관심 있는 항목의 목록입니다.
* U2I 사용자 tooItem-제공 된 권장 사항을 사용자 id (및 필요에 따라 항목의 목록)이이 옵션 가능성이 toobe 사용자 (및 추가 선택 항목)을 지정 하는 hello에 대 한 높은 관심 있는 항목의 목록을 예측 합니다. hello U2I 권장 사항은 toohello 시간 hello 모델 작성 된 hello 사용자에 대 한 관심 있는 항목의 hello 기록을 기반으로 합니다.

순위 빌드 hello 유용성 기능에 대 한 toolearn 수 있는 기술 빌드를 수행 합니다. 일반적으로 순서 tooget hello 최상의 결과에서 기능을 포함 하는 추천 모델에 대 한 단계를 수행 하는 hello를 수행 해야 합니다.

* Hello 기능 점수를 얻을 때까지 기다려 및 ()를 제외 기능 hello 점수 안정적인 순위 빌드를 트리거해야 합니다.
* Hello 호출 하 여 hello 순위 기능을 검색할 [기능 정보 가져오기](#101-get-features-info-for-last-rank-build) API입니다.
* Hello 매개 변수 뒤 권장 빌드를 구성 합니다.
  * `useFeatureInModel`-TooTrue 설정 합니다.
  * `ModelingFeatureList`2.0 이상의 점수 기능 집합 tooa 쉼표로 구분 된 목록 (따르는 toohello 순위 hello 이전 단계에서 검색)입니다.
  * `AllowColdItemPlacement`-TooTrue 설정 합니다.
  * 필요에 따라 설정할 수 있습니다 `EnableFeatureCorrelation` tooTrue 및 `ReasoningFeatureList` toouse (일반적으로 모델링 또는 하위 목록을 사용 되는 기능 목록은 같은 hello) 설명에 대 한 원하는 기능의 toohello 목록입니다.
* Hello로 트리거 hello 권장 빌드 매개 변수를 구성 합니다.

참고: 매개 변수를 구성 하지 않으면 (예: 매개 변수 없이 hello 권장 빌드 호출) 또는 hello 사용 기능을 명시적으로 해제 하지 않으면 (예: `UseFeatureInModel` tooFalse 설정), hello 시스템 hello 기능 관련 매개 변수를 설정 합니다 toohello 순위 빌드가 존재 하는 경우 위의 값을 설명 합니다.

순위 빌드 실행에 제한이 없으며 및 권장 사항을 동시에 빌드할 hello에 대 한 동일한 모델입니다. 그럼에도 불구 하 고 hello hello 동시에 같은 모델에 동일한 입력의 두 빌드를 실행할 수 없습니다.

FBT(자주 함께 구매됨) 빌드는 유형이 다른(같은 유형: 책, 영화, 일부 음식, 패션, 다른 유형: 컴퓨터와 장치, 크로스 도메인, 고도로 다양) 카탈로그에 적합한 “보수적인" 추천이라고도 하는 다른 권장 사항 알고리즘입니다.

참고: hello 사용 파일 경우 업로드 hello 선택적 필드 "이벤트 형식" 다음 FBT "Purchase" 이벤트만 모델링 사용 됩니다. 이벤트 유형이 제공되지 않은 경우에는 모든 이벤트가 구매로 간주됩니다.

#### <a name="111-build-parameters"></a>11.1 빌드 매개 변수
각 빌드 형식은 매개 변수 집합(아래 설명)을 통해 구성될 수 있습니다. Hello 매개 변수를 구성 하지 않는 경우 hello 시스템 toohello 정보 hello 시간에 빌드를 트리거에 따라 toohello 매개 변수 값 특성이 자동으로 됩니다.

##### <a name="1111-usage-condenser"></a>11.1.1. 사용 콘덴서
사용 포인트가 거의 없는 사용자 또는 항목은 정보보다 노이즈를 더 많이 포함할 수 있습니다. hello 시스템 toopredict hello 최소한의 모델에 사용 되는 사용자/항목 toobe 당 사용 포인트를 시도 합니다. 이 번호가 ItemCutoffLowerBound hello 및 항목과 UserCutOffLowerBound hello 및 사용자에 대 한 UserCutoffUpperBound 매개 변수에 의해 정의 된 hello 범위에 대 한 ItemCutoffUpperBound 매개 변수에 의해 정의 된 hello 범위 내에서 됩니다. 해당 범위 toozero hello 중 하나 이상을 설정 하 여 항목이 나 사용자가에 hello 콘덴서 영향을 최소화할 수 있습니다.

##### <a name="1112-rank-build-parameters"></a>11.1.2. 순위 빌드 매개 변수
hello 다음 표에서 순위 빌드에 대 한 hello 빌드 매개 변수를 보여 줍니다.

| 키 | 설명 | 형식 | 유효한 값 |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |hello 수의 반복 hello 모델의 성능을 hello 리플렉션하 전체 시간 및 hello 모델 정확도 계산 합니다. hello hello 크면, hello 더 나은 정확도 받아볼 수 있지만 hello 시간이 오래 걸립니다. 계산 합니다. |Integer |10-50 |
| NumberOfModelDimensions |차원 수가 hello toohello 수가 '기능' hello 모델 toofind 데이터 내에서 시도 관련 됩니다. Hello 차원 수를 늘리면 더 작은 클러스터로 hello 결과의 더 나은 미세 조정할 수 있습니다. 그러나 차원이 너무 많습니다. 항목 간의 상관 관계를 찾을 hello 모델 수 없게 됩니다. |Integer |10-40 |
| ItemCutOffLowerBound |Hello 콘덴서에 대 한 hello 항목 하한값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| ItemCutOffUpperBound |Hello 콘덴서에 대 한 hello 항목 상한 값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| UserCutOffLowerBound |Hello 콘덴서에 대 한 hello 사용자 하한값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| UserCutOffUpperBound |Hello 콘덴서에 대 한 hello 사용자 상한 값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. 권장 사항 빌드 매개 변수
hello 다음 표에서 권장 사항 빌드에 대 한 hello 빌드 매개 변수를 보여 줍니다.

| 키 | 설명 | 형식 | 유효한 값 |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |hello 수의 반복 hello 모델의 성능을 hello 리플렉션하 전체 시간 및 hello 모델 정확도 계산 합니다. hello hello 크면, hello 더 나은 정확도 받아볼 수 있지만 hello 시간이 오래 걸립니다. 계산 합니다. |Integer |10-50 |
| NumberOfModelDimensions |차원 수가 hello toohello 수가 '기능' hello 모델 toofind 데이터 내에서 시도 관련 됩니다. Hello 차원 수를 늘리면 더 작은 클러스터로 hello 결과의 더 나은 미세 조정할 수 있습니다. 그러나 차원이 너무 많습니다. 항목 간의 상관 관계를 찾을 hello 모델 수 없게 됩니다. |Integer |10-40 |
| ItemCutOffLowerBound |Hello 콘덴서에 대 한 hello 항목 하한값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| ItemCutOffUpperBound |Hello 콘덴서에 대 한 hello 항목 상한 값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| UserCutOffLowerBound |Hello 콘덴서에 대 한 hello 사용자 하한값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| UserCutOffUpperBound |Hello 콘덴서에 대 한 hello 사용자 상한 값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| 설명 |빌드 설명 |String |모든 텍스트, 최대 512자 |
| EnableModelingInsights |있습니다 toocompute 메트릭을 hello 추천 모델에서. |Boolean |True/False |
| UseFeaturesInModel |기능 순서 tooenhance hello 추천 모델에서 사용할 수 있는지를 나타냅니다. |Boolean |True/False |
| ModelingFeatureList |쉼표로 구분 된 목록 순서 tooenhance hello 권장 구성의 hello 권장 빌드에 사용 하는 기능 이름은 toobe입니다. |문자열 |기능 이름, too512 문자를 |
| AllowColdItemPlacement |Hello 권장 구성 최초 항목 기능 유사성을 통해 푸시하여도 해야 나타냅니다. |Boolean |True/False |
| EnableFeatureCorrelation |추론에서 기능을 사용할 수 있는지 나타냅니다. |Boolean |True/False |
| ReasoningFeatureList |쉼표로 구분 된 목록 (예: 권장 사항 설명) 문장 추론에 사용 되는 기능 이름은 toobe입니다. |문자열 |기능 이름, too512 문자를 |
| EnableU2I |개인 설정 된 hello 권장 라고도 함 허용 U2I (사용자 tooitem 권장 구성). |Boolean |True/False(기본값 true) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. FBT 빌드 매개 변수
hello 다음 표에서 권장 사항 빌드에 대 한 hello 빌드 매개 변수를 보여 줍니다.

| 키 | 설명 | 형식 | 유효한 값(기본값) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |보수적인 hello 모델은 방법입니다. 모델링을 위한 것으로 간주 하는 항목 toobe 공동 일치의 수입니다. |Integer |3-50 (6) |
| FbtMaxItemSetSize |Hello 수 자주 집합에 있는 항목의 범위입니다. |Integer |2-3(2) |
| FbtMinimalScore |최소 점수 집합을 자주 수행 해야 hello에 포함 되는 순서 toobe에 반환 됩니다. hello 더 높은 번호입니다. |Double |0 이상(0) |
| FbtSimilarityFunction |Hello 유사성 함수 toobe hello 빌드에 의해 사용 되는 정의 합니다. 리프트 serendipity를 우선으로, 예측 가능성을를 우선으로 동시 발생 및 Jaccard hello 2 간 좋은 절충안입니다. |문자열 |cooccurrence, lift, jaccard (lift) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. 권장 사항 빌드 트리거
  기본적으로 이 API는 권장 사항 모델 빌드를 트리거합니다. 순위 tootrigger (순서 tooscore 기능)에서 빌드, hello 빌드 API variant 빌드 형식 매개 변수와 함께 사용 해야 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` (요청 본문을 보내는 경우) |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| userDescription |Hello 카탈로그의 텍스트 식별자입니다. 공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다. 위 예제를 참조하세요.<br>최대 길이: 50 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |비워 두면 hello 빌드 hello 기본 빌드 매개 변수와 함께 실행 됩니다.<br><br>Tooset hello 빌드 매개 변수를 사용 하도록 하려는 경우 다음 예제는 hello와 같이 hello 본문으로 hello 매개 변수 XML로 보냅니다. (에 대 한 설명은 hello 매개 변수는 hello "빌드 매개 변수" 섹션 참조).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**응답**:

HTTP 상태 코드: 200

비동기 API입니다. 응답으로 빌드 ID가 제공됩니다. hello 빌드 끝나면 tooknow, 해야 hello "Get 빌드 상태의 정도 모델" API를 호출 하 고 배치할 있습니다 hello 응답에서이 빌드 ID입니다. Note 빌드 hello hello 데이터 크기에 따라 분 toohours에서 사용할 수 있습니다.

Hello 빌드 끝까지 권장 사항을 소비할 수 없습니다.

유효한 빌드 상태:

* Create - 빌드 요청이 만들어짐
* Queued – 빌드 요청을 보냈으며 큐에 대기됨
* Building – 빌드가 진행 중임
* Success – 빌드가 성공적으로 종료됨
* Error – 오류로 인해 빌드가 종료됨
* Cancelled – 빌드가 취소됨
* 취소 하 고-hello 빌드에 대 한 취소 요청을 보냈습니다.

Note는 hello 빌드 경로 따라 hello에서 ID를 찾을 수 있습니다.`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. 빌드(권장 사항, 순위 또는 FBT) 트리거
| HTTP 메서드 | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` (요청 본문을 보내는 경우) |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| userDescription |Hello 카탈로그의 텍스트 식별자입니다. 공백을 사용하는 경우 대신 %20을 사용하여 인코드해야 합니다. 위 예제를 참조하세요.<br>최대 길이: 50 |
| buildType |Hello 빌드 tooinvoke 유형: <br/> - 권장 사항 빌드의 경우 'Recommendation' <br> - 순위 빌드의 경우 'Ranking' <br/> - FBT 빌드의 경우 'Fbt' |
| apiVersion |1.0 |
|  | |
| 요청 본문 |비워 두면 hello 빌드 hello 기본 빌드 매개 변수와 함께 실행 됩니다.<br><br>원하는 tooset 빌드 매개 변수를 XML로 샘플 다음 hello와 같은 hello 본문으로 보냅니다. (자세한 설명 및 hello 매개 변수의 전체 목록은 hello "빌드 매개 변수" 섹션 참조).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

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
* Cancelled – 빌드가 취소됨
* Cancelling – 빌드 취소 중

Note는 hello 빌드 경로 따라 hello에서 ID를 찾을 수 있습니다.`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a>11.4. 모델의 빌드 상태 가져오기
지정된 모델의 빌드 및 해당 상태를 검색합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| onlyLastBuild |나타냅니다 tooreturn hello 모든 만들 hello 모델의 기록 또는 유일한 hello 상태의 hello 최신 빌드가 있는지 여부를 |
| apiVersion |1.0 |

**응답**:

HTTP 상태 코드: 200

hello 응답 빌드 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `feed/entry/content/properties/UserName`-Hello 사용자의 이름입니다.
* `feed/entry/content/properties/ModelName`-Hello 모델의 이름입니다.
* `feed/entry/content/properties/ModelId` – 모델의 고유 식별자
* `feed/entry/content/properties/IsDeployed`-Hello 빌드 (규칙 하위 배포 여부 활성 빌드)
* `feed/entry/content/properties/BuildId` – 빌드의 고유 식별자
* `feed/entry/content/properties/BuildType`-Hello 빌드의 형식입니다.
* `feed/entry/content/properties/Status` – 빌드 상태 Hello 다음 중 하나일 수 있습니다: 오류, 건물, 대기, 취소, 취소 됨, 성공 합니다.
* `feed/entry/content/properties/StatusMessage`-자세한 상태 메시지 (toospecific 상태에만 적용 됨).
* `feed/entry/content/properties/Progress` – 빌드 진행률(%)
* `feed/entry/content/properties/StartTime` – 빌드 시작 시간
* `feed/entry/content/properties/EndTime` – 빌드 종료 시간
* `feed/entry/content/properties/ExecutionTime` – 빌드 기간
* `feed/entry/content/properties/ProgressStep`-진행 중인 빌드가의 현재 단계 hello에 대 한 세부 정보.

유효한 빌드 상태:

* Created – 빌드 요청 항목이 만들어짐
* Queued – 빌드 요청이 트리거되었으며 큐에 대기됨
* Building – 빌드가 진행 중임
* Success – 빌드가 성공적으로 종료됨
* Error – 오류로 인해 빌드가 종료됨
* Cancelled – 빌드가 취소됨
* Cancelling – 빌드 취소 중

유효한 빌드 형식 값:

* Rank - 순위 빌드
* Recommendation - 권장 사항 빌드

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a>11.5. 빌드 상태 가져오기
사용자의 모든 모델에 대한 빌드 상태를 검색합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| onlyLastBuild |나타냅니다 hello 모든 tooreturn hello 모델의 기록 빌드할지 hello 가장 최근 빌드의 유일한 hello 상태입니다. |
| apiVersion |1.0 |

**응답**:

HTTP 상태 코드: 200

hello 응답 빌드 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `feed/entry/content/properties/UserName`-Hello 사용자의 이름입니다.
* `feed/entry/content/properties/ModelName`-Hello 모델의 이름입니다.
* `feed/entry/content/properties/ModelId` – 모델의 고유 식별자
* `feed/entry/content/properties/IsDeployed`-여부 hello 빌드가 배포 됩니다.
* `feed/entry/content/properties/BuildId` – 빌드의 고유 식별자
* `feed/entry/content/properties/BuildType`-Hello 빌드의 형식입니다.
* `feed/entry/content/properties/Status` – 빌드 상태 Hello 다음 중 하나일 수 있습니다: 오류, 건물, 대기, 취소 됨, 취소, 성공 합니다.
* `feed/entry/content/properties/StatusMessage`-자세한 상태 메시지 (toospecific 상태에만 적용 됨).
* `feed/entry/content/properties/Progress` – 빌드 진행률(%)
* `feed/entry/content/properties/StartTime` – 빌드 시작 시간
* `feed/entry/content/properties/EndTime` – 빌드 종료 시간
* `feed/entry/content/properties/ExecutionTime` – 빌드 기간
* `feed/entry/content/properties/ProgressStep`-진행 중인 빌드가의 현재 단계 hello에 대 한 세부 정보.

유효한 빌드 상태:

* Created – 빌드 요청 항목이 만들어짐
* Queued – 빌드 요청이 트리거되었으며 큐에 대기됨
* Building – 빌드가 진행 중임
* Success – 빌드가 성공적으로 종료됨
* Error – 오류로 인해 빌드가 종료됨
* Cancelled – 빌드가 취소됨
* Cancelling – 빌드 취소 중

유효한 빌드 형식 값:

* Rank - 순위 빌드
* Recommendation - 권장 사항 빌드

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a>11.6. 빌드 삭제
빌드를 삭제합니다.

참고:  <br>활성 빌드는 삭제할 수 없습니다. hello 모델 해야 tooa 다른 활성 빌드를 삭제 하기 전에 업데이트 합니다.<br>진행 중인 빌드는 삭제할 수 없습니다. 호출 하 여 먼저 hello 빌드를 취소 해야 <strong>빌드 취소</strong>합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| buildId |Hello 빌드의 고유 식별자입니다. |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

### <a name="117-cancel-build"></a>11.7. 빌드 취소
빌드 중 상태인 빌드를 취소합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| PUT |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| buildId |Hello 빌드의 고유 식별자입니다. |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

### <a name="118-get-build-parameters"></a>11.8. 빌드 매개 변수 가져오기
빌드 매개 변수를 검색합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| buildId |Hello 빌드의 고유 식별자입니다. |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

이 API는 키/값 요소의 컬렉션을 반환합니다. 각 요소는 매개 변수와 해당 값을 나타냅니다.

* `feed/entry/content/properties/Key` - 빌드 매개 변수 이름.
* `feed/entry/content/properties/Value` - 빌드 매개 변수 값.

hello 다음 표에서 각 키를 나타내는 hello 값을 보여 줍니다.

| 키 | 설명 | 형식 | 유효한 값 |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |hello 수의 반복 hello 모델의 성능을 hello 리플렉션하 전체 시간 및 hello 모델 정확도 계산 합니다. hello hello 크면, hello 더 나은 정확도 받아볼 수 있지만 hello 시간이 오래 걸립니다. 계산 합니다. |Integer |10-50 |
| NumberOfModelDimensions |차원 수가 hello toohello 수가 '기능' hello 모델 toofind 데이터 내에서 시도 관련 됩니다. Hello 차원 수를 늘리면 더 작은 클러스터로 hello 결과의 더 나은 미세 조정할 수 있습니다. 그러나 차원이 너무 많습니다. 항목 간의 상관 관계를 찾을 hello 모델 수 없게 됩니다. |Integer |10-40 |
| ItemCutOffLowerBound |Hello 콘덴서에 대 한 hello 항목 하한값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| ItemCutOffUpperBound |Hello 콘덴서에 대 한 hello 항목 상한 값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| UserCutOffLowerBound |Hello 콘덴서에 대 한 hello 사용자 하한값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| UserCutOffUpperBound |Hello 콘덴서에 대 한 hello 사용자 상한 값을 정의합니다. 위의 사용 콘덴서를 참조하세요. |Integer |2 이상(0 - 콘덴서 사용 안 함) |
| 설명 |빌드 설명 |String |모든 텍스트, 최대 512자 |
| EnableModelingInsights |있습니다 toocompute 메트릭을 hello 추천 모델에서. |Boolean |True/False |
| UseFeaturesInModel |기능 순서 tooenhance hello 추천 모델에서 사용할 수 있는지를 나타냅니다. |Boolean |True/False |
| ModelingFeatureList |쉼표로 구분 된 목록 순서 tooenhance hello 권장 구성의 hello 권장 빌드에 사용 하는 기능 이름은 toobe입니다. |문자열 |기능 이름, too512 문자를 |
| AllowColdItemPlacement |Hello 권장 구성 최초 항목 기능 유사성을 통해 푸시하여도 해야 나타냅니다. |Boolean |True/False |
| EnableFeatureCorrelation |추론에서 기능을 사용할 수 있는지 나타냅니다. |Boolean |True/False |
| ReasoningFeatureList |쉼표로 구분 된 목록 (예: 권장 사항 설명) 문장 추론에 사용 되는 기능 이름은 toobe입니다. |문자열 |기능 이름, too512 문자를 |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. 권장 사항
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. 항목 권장 사항 가져오기(활성 빌드)
형식의 hello 활성 빌드의 권장 사항을 "권장" 메시지가 "Fbt" 초기값 (입력) 항목의 목록에 따라 또는.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| itemIds |쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다. <br>Hello 활성 빌드의 경우 다음 항목을 하나만 보낼 수 FBT를 입력 합니다. <br>최대 길이: 1024 |
| numberOfResults |필요한 결과 수  <br> 최대: 150 |
| includeMetatadata |나중에 사용, 항상 false |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id` - 권장된 항목 ID
* `Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

아래 예제 응답 hello 10 개 권장된 항목이 포함 되어 있습니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. 항목 권장 사항 가져오기(특정 빌드)
특정 빌드 형식 "Recommendation" 또는 "Fbt"의 권장 사항을 가져옵니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| itemIds |쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다. <br>Hello 활성 빌드의 경우 다음 항목을 하나만 보낼 수 FBT를 입력 합니다. <br>최대 길이: 1024 |
| numberOfResults |필요한 결과 수  <br> 최대: 150 |
| includeMetatadata |나중에 사용, 항상 false |
| buildId |hello이 권장 구성 요청에 대 한 id toouse 빌드 |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id` - 권장된 항목 ID
* `Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

12.1의 응답 예제 참조

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. FBT 권장 사항 가져오기(활성 빌드)
시드 (입력) 항목을 기반으로 하는 "Fbt" 형식의 hello 활성 빌드의 권장 사항을 가져옵니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| itemId |에 대 한 항목 toorecommend 합니다. <br>최대 길이: 1024 |
| numberOfResults |필요한 결과 수  <br>최대: 150 |
| minimalScore |결과 반환 하는 집합을 자주 있는 hello에 포함 되는 순서 toobe에 최소 점수 |
| includeMetatadata |나중에 사용, 항상 false |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 권장된 항목 집합 (일반적으로 hello 초기값/입력 항목과 함께 구매 하는 항목 집합) 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id1` - 권장된 항목 ID
* `Feed\entry\content\properties\Name1`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Id2` - 두 번째 권장된 항목 ID(선택 사항).
* `Feed\entry\content\properties\Name2`-(선택 사항) hello 두 번째 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

아래 예제 응답 hello 세 추천된 항목 집합을 포함합니다.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. FBT 권장 사항 가져오기(특정 빌드)
특정 빌드 유형 "Fbt"의 권장 사항 가져오기

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| itemId |에 대 한 항목 toorecommend 합니다. <br>최대 길이: 1024 |
| numberOfResults |필요한 결과 수  <br>최대: 150 |
| minimalScore |결과 반환 하는 집합을 자주 있는 hello에 포함 되는 순서 toobe에 최소 점수 |
| includeMetatadata |나중에 사용, 항상 false |
| buildId |hello이 권장 구성 요청에 대 한 id toouse 빌드 |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 권장된 항목 집합 (일반적으로 hello 초기값/입력 항목과 함께 구매 하는 항목 집합) 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id1` - 권장된 항목 ID
* `Feed\entry\content\properties\Name1`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Id2` - 두 번째 권장된 항목 ID(선택 사항).
* `Feed\entry\content\properties\Name2`-(선택 사항) hello 두 번째 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

12.3의 응답 예제 참조

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. 사용자 권장 사항 가져오기(활성 빌드)
빌드 형식이 활성 빌드로 표시된 "Recommendation"인 사용자 권장 사항을 가져옵니다.

hello API hello 사용자의 사용 현황 toohello에 따라 예측 된 항목의 목록을 반환 합니다.

참고: 

1. FBT 빌드에 대한 사용자 권장 사항은 없습니다.
2. 활성 hello 빌드 이면 FBT이이 메서드는 오류를 반환 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| userId |Hello 사용자의 고유 식별자 |
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

12.1의 응답 예제 참조

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. 항목 목록이 있는 사용자 권장 사항 가져오기(활성 빌드)
추가 항목 목록이 있으며 빌드 형식이 활성 빌드로 표시된 "Recommendation"인 사용자 권장 사항을 가져옵니다.

hello API hello 사용자 및 제공 된 항목을 추가로 hello toohello 현황에 따라 예측 된 항목의 목록을 반환 합니다.

참고: 

1. FBT 빌드에 대한 사용자 권장 사항은 없습니다.
2. 활성 hello 빌드 이면 FBT이이 메서드는 오류를 반환 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| userId |Hello 사용자의 고유 식별자 |
| itemsIds |쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다. 최대 길이: 1024 |
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

12.1의 응답 예제 참조

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. 사용자 권장 사항 가져오기(특정 빌드)
특정 빌드 형식이 "Recommendation"인 사용자 권장 사항을 가져옵니다.

hello API hello 사용자 (hello 특정 빌드에 사용 됨)의 toohello 현황에 따라 예측 된 항목의 목록을 반환 합니다.

참고: FBT 빌드에 대한 사용자 권장 사항은 없습니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| userId |Hello 사용자의 고유 식별자 |
| numberOfResults |필요한 결과 수  |
| includeMetatadata |나중에 사용, 항상 false |
| buildId |hello이 권장 구성 요청에 대 한 id toouse 빌드 |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id` - 권장된 항목 ID
* `Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

12.1의 응답 예제 참조

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. 항목 목록이 있는 사용자 권장 사항 가져오기(특정 빌드)
"권장" 형식의 특정 빌드의 사용자 권장 사항 및 추가 항목 hello 목록을 가져옵니다.

hello API hello 사용자의 toohello 사용 기록 및 hello 항목의 추가 목록에 따라 예측 된 항목의 목록을 반환 합니다.

참고: FBT 빌드에 대한 사용자 권장 사항은 없습니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| userId |Hello 사용자의 고유 식별자 |
| itemIds |쉼표로 구분 된 목록에 대 한 hello 항목 toorecommend입니다. 최대 길이: 1024 |
| numberOfResults |필요한 결과 수  |
| includeMetatadata |나중에 사용, 항상 false |
| buildId |hello이 권장 구성 요청에 대 한 id toouse 빌드 |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id` - 권장된 항목 ID
* `Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Rating`-Hello 권장; 등급 값이 클수록 더 신뢰성을 의미합니다.
* `Feed\entry\content\properties\Reasoning` - 권장 사항 추론(예: 권장 사항 설명)

12.1의 응답 예제 참조

## <a name="13-user-usage-history"></a>13. 사용자 사용 기록
추천 모델 작성 되 면 hello 시스템 tooretrieve hello 사용자 기록 (항목 관련된 tooa 특정 사용자) hello 빌드에 사용 되는 허용 합니다.
이 API는 tooretrieve hello 사용자 기록 허용

참고: hello 사용자 기록은 권장 사항 빌드에 대해서만 찾을 수 없습니다.

### <a name="131-retrieve-user-history"></a>13.1 사용자 기록 검색
활성 hello에 사용 되는 항목 검색 hello 목록을 빌드하거나 hello 지정 된 사용자 id를 지정 하는 hello에 대 한 빌드 합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |Hello 현재 빌드에 대 한 hello 사용자 기록을 가져옵니다.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>빌드를 제공 하는 hello에 대 한 hello 사용자 기록 가져오기`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>예:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |hello hello 모델의 고유 식별자입니다. |
| userId |hello hello 사용자의 고유 식별자입니다. |
| buildId |선택적 매개 변수에서 어떤 빌드에서 hello 사용자 기록 있어야 인출 tooindicate 허용 |
| apiVersion |1.0 |

**응답:**

HTTP 상태 코드: 200

hello 응답에는 추천된 항목 변수당 하나의 항목이 포함 됩니다. 각 항목에 같은 데이터가 hello:

* `Feed\entry\content\properties\Id` - 권장된 항목 ID
* `Feed\entry\content\properties\Name`-Hello 항목의 이름입니다.
* `Feed\entry\content\properties\Rating` 해당 없음
* `Feed\entry\content\properties\Reasoning` 해당 없음

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. 알림
Azure 시스템 학습 권장 사항 hello 시스템에서 영구 오류가 발생 하는 경우 알림을 만듭니다. 다음과 같은 세 가지 유형의 알림이 있습니다.

1. 빌드 오류 – 이 알림은 모든 빌드 오류에 대해 트리거됩니다.
2. 오류-이 알림을 처리 하는 데이터 취득은 100 개 이상의 오류에에서 있는 hello hello 처리 모델에 대해 사용 이벤트의 최근 5 분 동안 때 트리거됩니다.
3. 발생 한 경우 100 개 이상의 오류 hello에 모델에 대해 권장 요청의 hello 처리에서 마지막 5 분 권장 소비 실패-이 알림이 트리거됩니다.

### <a name="141-get-notifications"></a>14.1. 알림 가져오기
모든 모델에 대 한 또는 단일 모델에 대 한 모든 hello 알림을 검색합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| GET |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>모든 모델에 대한 모든 알림 가져오기:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>특정 모델에 대한 알림을 가져오는 예제:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |선택적 매개 변수. 생략한 경우 모든 모델에 대한 모든 알림을 가져옵니다. <br>유효한 값: hello 모델의 고유 식별자입니다. |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답:**

HTTP 상태 코드: 200

OData XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. 모델 알림 삭제
모델에 대한 읽은 알림을 모두 삭제합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>예제:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| modelId |Hello 모델의 고유 식별자 |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

### <a name="143-delete-user-notifications"></a>14.3. 사용자 알림 삭제
모든 모델에 대한 모든 알림을 삭제합니다.

| HTTP 메서드 | URI |
|:--- |:--- |
| 삭제 |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| 매개 변수 이름 | 유효한 값 |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| 요청 본문 |없음 |

**응답**:

HTTP 상태 코드: 200

## <a name="15-legal"></a>15. 법적 정보
이 문서는 "있는 그대로" 제공됩니다. URL 및 기타 인터넷 웹 사이트 참조를 포함하여 본 문서에 명시된 정보 및 보기는 통지 없이 변경될 수 있습니다.<br><br>
여기에서 설명하는 일부 예는 설명 목적으로만 제공되는 가상의 예이며, 어떠한 실제 사례와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다.<br><br>
이 문서에서는 있습니다 법적 권리도 tooany Microsoft 제품의 지적 재산입니다. 이 문서는 내부 참조용으로만 복사 및 사용할 수 있습니다.<br><br>
© 2015 Microsoft. All rights reserved.

