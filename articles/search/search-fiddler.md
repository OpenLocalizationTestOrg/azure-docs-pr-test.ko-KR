---
title: "aaaHow toouse Fiddler tooevaluate 및 Azure 검색 REST Api 테스트 | Microsoft Docs"
description: "Fiddler를 사용 하 여 코드 않는 접근 방법 tooverifying Azure 검색 가용성 및 시험적으로 hello REST Api에 대 한 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Fiddler tooevaluate를 사용 하 여 및 Azure 검색 REST Api를 테스트 합니다.
> [!div class="op_single_selector"]
>
> * [개요](search-query-overview.md)
> * [검색 탐색기](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST (영문)](search-query-rest-api.md)
>
>

이 문서에서는 설명 어떻게 toouse Fiddler로 사용할 수는 [Telerik의 무료 다운로드](http://www.telerik.com/fiddler), tooissue HTTP 요청 tooand 응답 보기 hello Azure 검색 REST API를 사용 하 여 모든 코드 toowrite 필요 없이 합니다. Azure 검색은 Microsoft Azure에서 완벽하게 관리되는 호스트된 클라우드 검색 서비스이며 .NET 및 REST API를 통해 쉽게 프로그래밍 가능합니다. Azure 검색 서비스 REST Api에 설명 되어 hello [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx)합니다.

단계를 수행 하는 hello, 인덱스를 만들, 문서, 쿼리 hello 인덱스 및 쿼리 hello 시스템 서비스 정보를 업로드 합니다.

이 단계는 toocomplete, 해야 Azure 검색 서비스 및 `api-key`합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) tooget 시작 하는 방법에 대 한 지침은 합니다.

## <a name="create-an-index"></a>인덱스 만들기
1. Fiddler를 시작합니다. Hello에 **파일** 메뉴 해제 **트래픽 캡처** toohide 잘못 사용 된 HTTP 활동을 관련 없는 toohello 현재 작업 합니다.
2. Hello에 **작성기** 탭 스크린 샷 다음 hello 처럼 보이는 요청 공식화 합니다.

      ![][1]
3. **PUT**을 선택합니다.
4. Hello 서비스 URL, 요청 특성 및 hello api 버전을 지정 하는 URL을 입력 합니다. 염두에서 몇 가지 포인터 tookeep:

   * HTTPS를 사용 하 여 hello 접두사로 합니다.
   * 요청 특성은 "/indexes/hotels"입니다. 검색 toocreate '호텔' 이름이 인덱스를 인지 나타냅니다.
   * api-version은 소문자이며 "?api-version=2016-09-01"로 지정됩니다. Azure 검색은 주기적으로 업데이트를 배포하므로 API 버전이 중요합니다. 드문 경우 이지만 서비스 업데이트에는 주요 변경 toohello API 발생할 수 있습니다. 이러한 이유로 Azure 검색은 각 요청에 API 버전이 필요하므로 어떤 것을 사용할지 전체를 제어합니다.

     hello 전체 URL에는 다음 예제와 비슷한 toohello 찾아야 합니다.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. 서비스에 대해 사용할 수 있는 값을 가진 hello 호스트와 api 키를 대체 hello 요청 헤더를 지정 합니다.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. 요청 본문에서 hello 인덱스 정의 구성 하는 hello 필드에 붙여 넣습니다.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. **실행**을 클릭합니다.

몇 초 후에 HTTP 201 응답 hello 세션 목록에 표시 됩니다, 그리고 나타내는 hello 인덱스를 성공적으로 만들었습니다.

HTTP 504 발생 하는 경우 HTTPS를 지정 하는 hello URL을 확인 합니다. HTTP 400 또는 404 나타나면 본문 tooverify 있습니다 복사-붙여넣기 오류가 없으면 hello 요청을 확인 합니다. HTTP 403에는 일반적으로 hello api 키 (잘못 된 키 또는 hello api 키를 지정 하는 방법을 문제가 구문)에 문제가 있음을 나타냅니다.

## <a name="load-documents"></a>문서 로드
Hello에 **작성기** 탭 요청 toopost 문서 hello 다음과 같습니다. hello hello 요청 본문에는 4 호텔 hello 검색 데이터가 포함 됩니다.

   ![][2]

1. **POST**를 선택합니다.
2. HTTPS, 서비스 URL, "/indexes/<'indexname'>/docs/index?api-version=2016-09-01" 순으로 URL을 입력합니다. hello 전체 URL에는 다음 예제와 비슷한 toohello 찾아야 합니다.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. 요청 헤더 해야 수 hello 동일한 이전과 합니다. 서비스에 대해 사용할 수 있는 값으로 hello 호스트와 api 키를 대체 해야 합니다.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. 요청 본문 hello 4 개의 문서 toobe 추가 toohello 호텔 인덱스를 포함 합니다.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. **실행**을 클릭합니다.

몇 초 후에 HTTP 200 응답 hello 세션 목록에 표시 됩니다. 이 문서 성공적으로 만들어졌습니다. hello를 나타냅니다. 207 발생 하는 경우 하나 이상의 문서 tooupload를 못했습니다. 404 발생 하는 경우 hello 헤더 또는 hello 요청 본문에 구문 오류가 포함 됩니다.

## <a name="query-hello-index"></a>쿼리 hello 인덱스
이제 인덱스와 문서가 로드되었으므로 쿼리를 실행할 수 있습니다.  Hello에 **작성기** 탭은 **가져오기** 명령 서비스를 쿼리 하는 비슷한 toohello 다음 스크린 샷에 표시 됩니다.

   ![][3]

1. **GET**을 선택합니다.
2. HTTPS, 서비스 URL, "/indexes/<'indexname'>/docs?", 쿼리 매개 변수 순으로 URL을 입력합니다. 예를 들어 hello url, hello 샘플 호스트 이름이 서비스에 대 한 적합 한 대체를 사용 합니다.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   이 쿼리는 hello 용어 "motel"를 검색 하 고 등급에 대 한 패싯 범주를 검색 합니다.
3. 요청 헤더 해야 수 hello 동일한 이전과 합니다. 서비스에 대해 사용할 수 있는 값으로 hello 호스트와 api 키를 대체 해야 합니다.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

hello 응답 코드는 200 여야 하 고 hello 응답 출력은 유사한 toohello 스크린 샷 다음를 표시 합니다.

   ![][4]

hello 다음 예제 쿼리는 hello에서 [검색 인덱스 작업 (Azure 검색 API)](http://msdn.microsoft.com/library/dn798927.aspx) msdn 합니다. 이 항목의 hello 예제 쿼리는 대부분 Fiddler에 허용 되지 않는 공백이 포함 됩니다. 공간이와 a + 문자 Fiddler에 hello 쿼리를 시도 하기 전에 쿼리 문자열 hello에 붙여 넣어 전에 교체 합니다.

**공백을 바꾸기 전:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**공백을 +로 바꾼 후:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>쿼리 hello 시스템
Hello는 시스템 tooget 문서 개수 및 저장소 사용을 쿼리할 수도 있습니다. Hello에 **작성기** 탭 요청 비슷한 toohello 다음 모양과 hello 응답 문서 및 사용 되는 공간 hello 수에 대 한 수를 반환 합니다.

 ![][5]

1. **GET**을 선택합니다.
2. 해당 서비스 URL과 그 뒤에 "/indexes/hotels/stats?api-version=2016-09-01"을 포함하는 URL을 입력합니다.

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. 서비스에 대해 사용할 수 있는 값을 가진 hello 호스트와 api 키를 대체 hello 요청 헤더를 지정 합니다.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hello 요청 본문을 비워 둡니다.
5. **실행**을 클릭합니다. HTTP 200 상태 코드가 hello 세션 목록에 표시 됩니다. 명령에 대 한 게시 hello 항목을 선택 합니다.
6. Hello 클릭 **검사자** 탭에서 hello **헤더** 탭을 클릭 한 다음 선택 hello JSON 형식입니다. Hello 문서 개수 및 저장소 크기 (KB)를 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계
참조 [에서 Azure 검색 서비스 관리](search-manage.md) 코드 없는 접근 방식 toomanaging 및 Azure 검색을 사용 합니다.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
