---
title: "앱 서비스 모바일 앱 hello로 aaaWorking 관리 되는 클라이언트 라이브러리 (Windows | Microsoft Docs"
description: "자세한 내용은 방법 toouse 창 및 Xamarin 앱과 Azure 앱 서비스 모바일 앱 용.NET 클라이언트입니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>개요
이 가이드에서는 tooperform 일반적인 시나리오 hello를 사용 하 여 Azure 앱 서비스 모바일 앱에 대 한 Windows 및 Xamarin 앱 용 클라이언트 라이브러리를 관리 하는 방법을 알아봅니다. 첫 번째 완료 hello를 고려해 야 새로운 tooMobile 앱 인 경우 [Azure 모바일 앱 빠른 시작] [ 1] 자습서입니다. 이 가이드에 집중 hello 클라이언트 SDK를 관리 합니다. 모바일 앱에 대 한 서버 쪽 Sdk hello, hello에 대 한 hello 설명서를 참조에 대해 더 알아봅니다 toolearn [.NET 서버 SDK] [ 2] 또는 [Node.js 서버 SDK] [ 3].

## <a name="reference-documentation"></a>참조 설명서
hello hello 클라이언트 SDK에 대 한 참조 설명서는 여기에서 찾을: [Azure 모바일 앱.NET 클라이언트 참조][4]합니다.
Hello에 여러 클라이언트 샘플을 찾을 수도 [Azure 샘플 GitHub 리포지토리][5]합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼
.NET 플랫폼 hello hello 다음 플랫폼을 지원 합니다.

* API 19-24(Nougat를 통한 KitKat)용 Xamarin Android 릴리스
* iOS 버전 8.0 이상을 위한 Xamarin iOS 릴리스
* 범용 Windows 플랫폼
* Windows Phone 8.1
* Silverlight 응용 프로그램을 제외한 Windows Phone 8.0

hello "서버 흐름" 인증 UI를 표시 하는 hello에 대 한 보기를 사용 합니다.  Hello 장치가 수 toopresent WebView UI가 아닌 경우를 다른 인증 방법에는 필요 합니다.  따라서 이 SDK는 Watch 유형 또는 그와 비슷하게 제한된 장치에는 적합하지 않습니다.

## <a name="setup"></a>설정 및 필수 조건
하나 이상의 테이블에 포함된 모바일 앱 백 엔드 프로젝트를 이미 만들고 게시했다고 가정합니다.  Hello 테이블의 이름이이 항목에서 사용 하는 hello 코드, `TodoItem` hello 열 뒤에 있고: `Id`, `Text`, 및 `Complete`합니다. 이 테이블은 동일한 테이블 완료 하면 만들어집니다 hello는 [Azure 모바일 앱 빠른 시작][1]합니다.

hello 해당 형식화 된 클라이언트 쪽에 있는 C# 형식이 클래스를 다음 hello:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

hello [JsonPropertyAttribute] [ 6] 는 사용 되는 toodefine hello *PropertyName* hello client 필드와 hello 테이블 필드 간의 매핑입니다.

toocreate 테이블 모바일 앱 백 엔드에 어떻게 toolearn 참조 hello [.NET 서버 SDK 항목] [ 7] 또는 hello [Node.js 서버 SDK 항목] [ 8] . 모바일 앱 백 엔드를 만든 경우 Azure hello 퀵 스타트 hello 사용 하 여 포털, hello를 사용할 수도 있습니다 **쉽게 테이블** hello 설정을 [Azure 포털]합니다.

### <a name="how-to-install-hello-managed-client-sdk-package"></a>방법: 설치 hello 클라이언트 SDK 패키지 관리
Hello tooinstall hello 메서드를 다음 중 하나를 사용 클라이언트 SDK 패키지에서 모바일 앱에 대 한 관리 되는 [NuGet][9]:

* **Visual Studio** 프로젝트를 마우스 오른쪽 단추로 클릭 하 여, **NuGet 패키지 관리**, hello에 대 한 검색 `Microsoft.Azure.Mobile.Client` 패키지 하 고, 한 다음 클릭 **설치**합니다.
* **Xamarin Studio** 프로젝트를 마우스 오른쪽 단추로 클릭 하 여, **추가** > **NuGet 패키지 추가**, hello에 대 한 검색 `Microsoft.Azure.Mobile.Client `패키지를 선택한 다음 클릭 **추가 패키지**합니다.

기본 활동 파일에서 기억 tooadd hello 다음 **를 사용 하 여** 문:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>방법: Visual Studio에서 디버그 작업
hello Microsoft.Azure.Mobile 네임 스페이스에 대 한 hello 기호에서 사용할 수 있는 [SymbolSource][10]합니다.  Toothe 참조 [SymbolSource 지침] [ 11] toointegrate SymbolSource Visual Studio와 함께 합니다.

## <a name="create-client"></a>Hello 모바일 앱 클라이언트 만들기
hello 다음 코드에서는 hello [MobileServiceClient] [ 12] 개체를 사용 하는 tooaccess 모바일 앱 백 합니다.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

Hello 코드 앞에, 바꿉니다 `MOBILE_APP_URL` hello 모바일 앱 백 엔드의 hello url,에 있는 hello에 모바일 앱 백 엔드에 대 한 블레이드 [Azure 포털]합니다. hello MobileServiceClient 개체는 단일 항목 이어야 합니다.

## <a name="work-with-tables"></a>테이블 작업
다음 섹션 세부 정보를 어떻게 hello toosearch 레코드를 검색 하 고 hello hello 테이블 내에 데이터를 수정 합니다.  hello 다음 항목에 설명 합니다.

* [테이블 참조 만들기](#instantiating)
* [쿼리 데이터](#querying)
* [반환된 데이터 필터링](#filtering)
* [반환된 데이터 정렬](#sorting)
* [페이지에서 데이터 반환](#paging)
* [특정 열 선택](#selecting)
* [ID로 레코드 조회](#lookingup)
* [형식화되지 않은 쿼리 처리](#untypedqueries)
* [데이터 삽입](#inserting)
* [데이터 업데이트](#updating)
* [데이터 삭제](#deleting)
* [충돌 해결 및 낙관적 동시성](#optimisticconcurrency)
* [바인딩 tooa Windows 사용자 인터페이스](#binding)
* [Hello 페이지 크기 변경](#pagesize)

### <a name="instantiating"></a>방법: 테이블 참조 만들기
Hello에 함수를 호출 하는 백 엔드 테이블의 데이터 액세스 또는 수정 되는 모든 hello 코드가 `MobileServiceTable` 개체입니다. Hello를 호출 하 여 참조 toohello 테이블을 가져올 [GetTable] 다음과 같이 메서드:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

hello는 hello 형식의 serialization 모델을 사용 하는 개체를 반환 합니다. 형식화되지 않은 직렬화 모델도 지원됩니다. 다음 예제에서는 [참조 tooan 형식화 되지 않은 테이블을 만들고]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

형식화 되지 않은 쿼리에 hello 기본 OData 쿼리 문자열을 지정 해야 합니다.

### <a name="querying"></a>방법: 모바일 앱에서 데이터 쿼리
이 섹션에서는 tooissue hello 다음 기능을 포함 하는 toohello 모바일 앱 백엔드를 쿼리 하는 방법을 설명 합니다.

* [반환된 데이터 필터링](#filtering)
* [반환된 데이터 정렬](#sorting)
* [페이지에서 데이터 반환](#paging)
* [특정 열 선택](#selecting)
* [ID를 기준으로 데이터 조회](#lookingup)

> [!NOTE]
> 서버 기반의 페이지 크기는 모든 행 반환 되지 않도록 적용된 tooprevent입니다.  페이징은 hello 서비스에 부정적인 영향을 미치고에서 큰 데이터 집합에 대 한 기본 요청을 유지 합니다.  hello를 사용 하 여 50 개 행 보다 tooreturn `Skip` 및 `Take` 메서드를에 설명 된 대로 [데이터 페이지를 반환](#paging)합니다.

### <a name="filtering"></a>방법: 반환된 데이터 필터링
hello 다음 코드에서는 방법을 포함 하 여 toofilter 데이터는 `Where` 쿼리의 절에에서 합니다. 모든 항목 반환 `todoTable` 인 `Complete` 속성은 너무`false`합니다. hello [여기서] 함수는 행 필터링 hello 테이블에 대 한 hello 쿼리 조건자를 적용 합니다.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

메시지 검사 소프트웨어 같은 브라우저 개발자 도구를 사용 하 여 hello hello 보낸 요청 toohello 백 엔드의 URI를 볼 수 있습니다 또는 [Fiddler]합니다. Hello 요청 URI 보면 hello 쿼리 문자열을 수정 하는 사항을 참고 하십시오.

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

이 OData 요청 hello 서버 SDK에서 SQL 쿼리로 변환 됩니다.

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

toohello 전달 된 함수는 hello `Where` 메서드는 임의 개수의 조건 가질 수 있습니다.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

이 예제는 hello 서버 SDK에서 SQL 쿼리도 변환할 수는:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

이 쿼리는 여러 절로 분할될 수도 있습니다.

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

hello 두 메서드가 동일 하며, 같은 의미로 사용할 수 있습니다.  첫 번째 옵션 hello&mdash;한 쿼리에서 여러 조건자를 연결 하&mdash;보다 간단 하 고 권장 됩니다.

hello `Where` 절 수 있는 작업을 지원 hello OData 하위 집합으로 변환 합니다. 작업에는 다음 항목이 포함됩니다.

* 관계형 연산자(==, !=, <, <=, >, >=),
* 산술 연산자(+, -, /, *, %),
* 숫자 정밀도(Math.Floor, Math.Ceiling),
* 문자열 함수(Length, Substring, Replace, IndexOf, StartsWith, EndsWith),
* 날짜 속성(연도, 월, 일, 시, 분, 초),
* 개체의 액세스 속성,
* 이러한 연산자를 결합하는 식.

무엇을 고려할 때 hello 서버 SDK에서 지 원하는 경우 hello를 고려할 수 있는 [OData v3 설명서]합니다.

### <a name="sorting"></a>방법: 반환된 데이터 정렬
hello 다음 코드에서는 방법을 포함 하 여 toosort 데이터는 [OrderBy] 또는 [OrderByDescending] hello 쿼리에서 함수입니다. 항목을 반환 `todoTable` hello로 오름차순으로 정렬 `Text` 필드입니다.

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <a name="paging"></a>방법: 페이지에서 데이터 반환
기본적으로 hello 백 엔드 첫 50 행만 hello을 반환합니다. Hello를 호출 하 여 반환 된 행의 hello 수를 늘려도 [걸릴] 메서드. 사용 하 여 `Take` hello 함께 [Skip] 메서드 toorequest 특정 "페이지" hello 전체 데이터 집합의 hello 쿼리에서 반환 합니다. hello 다음 쿼리를 실행 하면 hello 상위 3 개의 항목 반환 hello 표에 합니다.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

hello 다음 수정 된 쿼리에서 건너뜁니다 hello 처음 세 결과 및 반환 hello 다음 세 개의 결과입니다. 이 쿼리는 hello의 두 번째 "페이지" 여기서 hello 페이지 크기는 세 가지 항목 데이터를 생성 합니다.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

hello [IncludeTotalCount] 메서드 요청에 대 한 총 개수 hello *모든* 반환 되는, 지정 된 모든 paging/limit 절을 무시 하는 레코드 hello:

```
query = query.IncludeTotalCount();
```

실제 앱에서 페이지 간에 이동할 수 쿼리 비슷한 toohello 앞에 페이저 컨트롤 또는 UI를 비교할 수 있는 예제를 사용할 수 있습니다.

> [!NOTE]
> 모바일 앱 백 엔드에서 toooverride hello 50 행 제한을 적용 해야 hello [EnableQueryAttribute] toohello 공용 GET 메서드 및 hello 페이징 동작을 지정 합니다. 때 적용 된 toohello 메서드를 다음 hello 반환 되는 최대 행 too1000을 설정 합니다.
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>방법: 특정 열 선택
추가 하 여 결과 집합 hello에 tooinclude 속성을 지정할 수는 [선택] 절 tooyour 쿼리 합니다. 예를 들어 코드에서 보여 주는 방법을 따르는 hello tooselect 한 필드와도 방법을 tooselect 하 고 여러 필드의 서식을 지정:

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

지금까지 설명한 함수 hello 모든 우리 수 유지 체인에 있으므로 추가 됩니다. 연결 된 각 호출에 hello 쿼리 중에 영향을 줍니다. 한 가지 예를 더 들면 다음과 같습니다.

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>방법: ID를 기준으로 데이터 조회
hello [LookupAsync] 함수는 특정 ID 사용 하 여 hello 데이터베이스에서 개체를 사용 하는 toolook 수 있습니다.

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>방법: 형식화되지 않은 쿼리 실행
OData 쿼리 문자열 hello를 호출 하 여 명시적으로 지정 해야 형식화 되지 않은 테이블 개체를 사용 하 여 쿼리를 실행할 때 [ReadAsync]와 같이, 다음 예제는 hello:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

속성 모음처럼 사용할 수 있는 JSON 값이 반환됩니다. JToken 및 Newtonsoft Json.NET에 자세한 내용은 참조 hello [Json.NET] 사이트입니다.

### <a name="inserting"></a>방법: 모바일 앱 백 엔드에 데이터 삽입
모든 클라이언트 형식은 **ID**라는 멤버를 포함해야 하며 이는 기본적으로 문자열입니다. 이 **Id** CRUD 작업을 수행 하는 데 필요 하 고 오프 라인 동기화. hello 코드 다음에 대해 보여 줍니다 방법을 toouse hello [InsertAsync] 메서드 tooinsert 새 행을 테이블로 합니다. hello 매개 변수는 hello 데이터 toobe.NET 개체로 삽입을 포함 합니다.

```
await todoTable.InsertAsync(todoItem);
```

고유한 사용자 지정 ID 값은 hello에 포함 되지 않은 경우 `todoItem` 삽입 시 GUID hello 서버에 의해 생성 됩니다.
검색할 수 있습니다 hello hello 호출 반환 후 hello 개체를 검사 하 여 Id를 생성 합니다.

tooinsert 데이터 형식화 되지 않은, Json.NET 이용할 수 있습니다.

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

다음은 메일 주소를 고유 문자열 id로 사용하는 예제입니다.

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>ID 값으로 작업
모바일 앱 hello 테이블에 대 한 고유한 사용자 지정 문자열 값을 지원 하며 **id** 열입니다. 문자열 값을 사용 하면 응용 프로그램 toouse hello id 사용자 이름 또는 전자 메일 주소와 같은 사용자 지정 값  문자열 Id 이점을 다음 hello를 제공 합니다.

* Id가 왕복 toohello 데이터베이스를 만들지 않고 생성 됩니다.
* 레코드는 서로 다른 테이블 또는 데이터베이스에서 보다 쉽게 toomerge 합니다.
* 응용 프로그램의 논리를 통해 ID 값이 더 효율적으로 통합될 수 있습니다.

Hello 모바일 앱 백 엔드 ID에 대 한 고유한 값을 생성 하는 문자열 ID 값을 삽입된 한 레코드에 설정 하지 않으면 때 Hello를 사용할 수 있습니다 [Guid.NewGuid] 메서드 toogenerate hello 백 엔드 또는 hello 클라이언트에서 고유한 ID 값입니다.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>방법: 모바일 앱 백 엔드의 데이터 수정
hello 다음 코드에서는 어떻게 toouse hello [UpdateAsync] 새 정보로 ID 같습니다 메서드 tooupdate hello로 기존 레코드입니다. hello 매개 변수는 hello 데이터 toobe.NET 개체로 업데이트를 포함 합니다.

```
await todoTable.UpdateAsync(todoItem);
```

이용할 수 있습니다, tooupdate 데이터 형식화 되지 않은 [Json.NET] 다음과 같습니다.

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

업데이트할 때 `id` 필드를 지정해야 합니다. hello 백 엔드에서 사용 hello `id` 필드 tooidentify tooupdate 행입니다. hello `id` hello의 hello 결과에서 필드를 가져올 수 있습니다 `InsertAsync` 호출 합니다. `ArgumentException` hello를 제공 하지 않고 tooupdate 항목을 시도 하면 발생 `id` 값입니다.

### <a name="deleting"></a>방법: 모바일 앱 백 엔드의 데이터 삭제
hello 다음 코드에서는 어떻게 toouse hello [DeleteAsync] 메서드 toodelete 기존 인스턴스. hello 인스턴스 hello로 식별 됩니다 `id` hello에 설정 된 필드 `todoItem`합니다.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete 데이터 형식화 되지 않은 다음과 같이 Json.NET의 이점은 걸릴 수 있습니다.

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

삭제를 요청할 때 ID를 지정해야 합니다. 다른 속성 toohello 서비스가 전달 되지 않은 또는 hello 서비스에서 무시 됩니다. hello의 결과 `DeleteAsync` 호출은 일반적으로 `null`합니다. hello ID toopass hello의 hello 결과에서 얻을 수 있습니다 `InsertAsync` 호출 합니다. A `MobileServiceInvalidOperationException` hello를 지정 하지 않고 항목 toodelete 려 할 때 throw 되 `id` 필드입니다.

### <a name="optimisticconcurrency"></a>방법: 충돌 해결에 낙관적 동시성 사용
둘 이상의 클라이언트가 작성할 수 변경 toohello 동일 항목 hello에서 동일한 시간입니다. 충돌 감지 하지 않고 hello 마지막 쓰기가 이전의 업데이트 덮어씁니다. **낙관적 동시성 제어** 에서는 각 트랜잭션이 커밋할 수 있으므로 리소스 잠금을 사용하지 않는다고 가정합니다.  트랜잭션을 커밋하기 전에 낙관적 동시성 제어는 다른 트랜잭션이 없어야 hello 데이터 수정 않았는지 확인 합니다. Hello 데이터가 수정 된 트랜잭션 커밋은 hello가 롤백됩니다.

모바일 앱 hello를 사용 하 여 변경 내용을 tooeach 항목을 추적 하 여 낙관적 동시성 제어를 지 원하는 `version` 모바일 앱 백 엔드의 각 테이블에 대해 정의 된 시스템 속성 열입니다. 기록이 업데이트 될 때마다 모바일 앱 설정 hello `version` 속성에 대 한 tooa 새 값을 기록 합니다. 각 업데이트 요청을 하는 동안 hello `version` hello 요청에 포함 된 hello 레코드의 속성은 비교 toohello hello 서버의 hello 레코드에 대 한 동일한 속성입니다. 버전은 전달 된 hello 요청 hello 백 엔드에 맞지 않는 경우 hello 클라이언트 라이브러리를 발생 시킵니다는 `MobileServicePreconditionFailedException<T>` 예외입니다. hello hello 예외에 포함 된 형식은 hello 백 엔드 포함 hello 서버 버전의 hello 레코드 hello 레코드 합니다. hello 응용 프로그램을 유도할 수 있습니다이 정보 toodecide 여부 올바른 hello 사용 하 여 다시 tooexecute hello 업데이트 요청 `version` hello 백 엔드 toocommit 변경 된 내용에서 값입니다.

Hello 테이블 클래스 hello에 대 한 열을 정의 `version` 시스템 속성 tooenable 낙관적 동시성 합니다. 예:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

형식화 되지 않은 테이블을 사용 하는 응용 프로그램 hello 설정 하 여 낙관적 동시성을 사용 `Version` 에 플래그는 `SystemProperties` hello의 테이블 다음과 같습니다.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

또한 tooenabling 낙관적 동시성도 hello를 catch 해야 `MobileServicePreconditionFailedException<T>` 를 호출할 때 코드에서 예외 [UpdateAsync]합니다.  올바른 hello를 적용 하 여 hello 충돌을 해결 `version` toothe 업데이트 레코드 및 호출 [UpdateAsync] hello로 레코드를 확인 합니다. 코드 다음 hello tooresolve 쓰기 충돌이 한 번만 검색 하는 방법을 보여 줍니다.

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

자세한 내용은 참조 hello [Azure 모바일 앱에서 데이터 동기화 오프 라인] 항목입니다.

### <a name="binding"></a>방법: Bind 모바일 앱 데이터 tooa Windows 사용자 인터페이스
이 섹션에서는 toodisplay Windows 앱에서 UI 요소를 사용 하 여 데이터 개체를 반환 하는 방법을 보여 줍니다.  다음 예제 코드의 불완전 한 항목에 대 한 쿼리를 사용 하 여 hello 목록 toohello 소스에 바인딩합니다. [MobileServiceCollection]은 Mobile Apps 인식 바인딩 컬렉션을 만듭니다.

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

일부 컨트롤 hello에 관리 인터페이스를 호출 하는 런타임 지원이 [ISupportIncrementalLoading]합니다. 이 인터페이스에서는 컨트롤 toorequest hello 사용자가를 스크롤할 때 추가 데이터입니다. 이 인터페이스에 대 한 유니버설 Windows 앱을 통해 기본적으로 지원 [MobileServiceIncrementalLoadingCollection], hello 컨트롤에서 호출 하 여 자동으로 처리 합니다. 다음과 같이 Windows 앱에서 `MobileServiceIncrementalLoadingCollection` 을 사용합니다.

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello "Silverlight" 및 Windows Phone 8 앱을 사용 하 여 hello에서 새 컬렉션 `ToCollection` 에 확장 메서드 `IMobileServiceTableQuery<T>` 및 `IMobileServiceTable<T>`합니다. tooload 데이터 호출 `LoadMoreItemsAsync()`합니다.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

호출 하 여 만든 hello 컬렉션을 사용 하면 `ToCollectionAsync` 또는 `ToCollection`, 바인딩된 tooUI 컨트롤로 사용할 수 있는 컬렉션을 가져옵니다.  이 컬렉션은 페이징을 인식합니다.  Hello 컬렉션이 네트워크에서 데이터를 로드, 하므로 경우에 따라 로드 실패 합니다. toohandle hello를 재정의 하는 이러한 오류 `OnException` 메서드를 `MobileServiceIncrementalLoadingCollection` 너무 호출에서 발생 한 예외 toohandle`LoadMoreItemsAsync`합니다.

테이블에 여러 필드가 있지만 toodisplay 알아보려는 경우 고려 컨트롤에서 그 중 일부입니다. Hello 앞 섹션에서에서 hello 지침을 사용할 수 있습니다 "[특정 열을 선택](#selecting)" hello UI에서에서 특정 열 toodisplay tooselect 합니다.

### <a name="pagesize"></a>페이지 크기 변경 hello
Azure Mobile Apps는 기본적으로 요청당 최대 50개의 항목을 반환합니다.  Hello 클라이언트와 서버 모두에서 hello 최대 페이지 크기를 늘려 hello 페이징 크기를 변경할 수 있습니다.  tooincrease hello 요청 된 페이지 크기를 지정 `PullOptions` 사용 하는 경우 `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Hello 사항을 가정 `PageSize` hello 서버 내에서 100 보다 큰 같은 tooor 요청 최대 100 개의 항목을 반환 합니다.

## <a name="#offlinesync"></a>오프라인 데이터 작업
오프 라인 테이블 오프 라인일 때 사용 하기 위해 로컬 SQLite 저장소 toostore 데이터를 사용 합니다.  Hello에 대 한 작업은 수행 하는 테이블의 모든 로컬 SQLite hello 원격 서버 저장소 대신 저장 합니다.  toocreate를 오프 라인 테이블에는 먼저 프로젝트를 준비 합니다.

1. Visual Studio에서 hello 솔루션 탐색기에서 > **솔루션에 대 한 NuGet 패키지 관리...** 다음 검색 하 고 설치는 **Microsoft.Azure.Mobile.Client.SQLiteStore** hello 솔루션의 모든 프로젝트에 대 한 NuGet 패키지 합니다.
2. (선택 사항) toosupport Windows 장치 hello SQLite 런타임 패키지를 다음 중 하나를 설치 합니다.

   * **Windows 8.1 런타임:** [Windows 8.1][3]용 SQLite를 설치합니다.
   * **Windows Phone 8.1:** [Windows Phone 8.1][4]용 SQLite를 설치합니다.
   * **유니버설 Windows 플랫폼** 설치 [유니버설 Windows hello에 대 한 SQLite][5]합니다.
3. (선택 사항). Windows 장치에 대 한 클릭 **참조** > **참조 추가...** , hello 확장 **Windows** 폴더 > **확장**, 적절 한 hello를 사용 하도록 설정 하면 **Windows 용 SQLite** hello 함께SDK **Windows 용 visual c + + 2013 런타임** SDK입니다.
    hello SQLite SDK 이름은 조금씩 각 Windows 플랫폼입니다.

테이블 참조를 만들 수 있습니다, 전에 hello 로컬 저장소를 준비 해야 합니다.

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

저장소 초기화 hello 클라이언트를 만든 직후에 일반적으로 수행 됩니다.  hello **OfflineDbPath** 지 원하는 모든 플랫폼에서 사용 하기에 적합 한 파일 이름 이어야 합니다.  Hello 경로 정규화 된 경로 이면 (즉,이 메서드는 먼저 슬래시), 아니면 해당 경로 사용 합니다.  Hello 경로 정규화 되지 않은 경우 hello 파일이 플랫폼 관련 위치에 배치 됩니다.

* IOS 및 Android 장치에 대 한 hello 기본 경로 hello "개인 Files" 폴더입니다.
* Windows 장치에 대 한 hello 기본 경로 hello 응용 프로그램별 "AppData" 폴더입니다.

Hello를 사용 하 여 테이블 참조를 가져올 수 있습니다 `GetSyncTable<>` 메서드:

```
var table = client.GetSyncTable<TodoItem>();
```

오프 라인 테이블 tooauthenticate toouse가 필요가 없습니다.  Hello 백 엔드 서비스와 통신 하는 경우에 tooauthenticate가 필요 합니다.

### <a name="syncoffline"></a>오프라인 테이블 동기화
기본적으로 오프 라인 테이블 hello 백 엔드와 동기화 되지 않습니다.  동기화는 두 부분으로 분할됩니다.  새 항목 다운로드에서 별도로 변경 내용을 푸시할 수 있습니다.  다음은 일반적인 동기화 메서드입니다.

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

하는 경우 첫 번째 인수를 너무 hello`PullAsync` 매개 변수가 null 이면 증분 동기화가 사용 되지 않습니다.  각 동기화 작업은 모든 레코드를 가져옵니다.

hello SDK 수행 암시적 `PushAsync()` 레코드를 끌어오려면 먼저 합니다.

`PullAsync()` 메서드에서 충돌 처리가 발생합니다.  처리할 수 있는 충돌을 방지 hello와 동일한 방법으로 온라인 테이블입니다.  hello 충돌 생성 되는 경우 `PullAsync()` 대신 hello 삽입, 업데이트 또는 삭제 하는 동안 호출 되어 합니다. 여러 충돌이 발생하는 경우 단일 MobileServicePushFailedException에 함께 포함됩니다.  각 오류를 개별적으로 처리합니다.

## <a name="#customapi"></a>사용자 지정 API 작업
사용자 지정 API toodefine 사용자 지정 끝점을 서버 기능을 노출 하는 또는 하지 않는 매핑할 tooan 삽입, 업데이트, 삭제, 읽기 작업이 있습니다. 사용자 지정 API를 사용하면 HTTP 메시지 헤더 읽기와 설정 및 JSON 이외의 메시지 본문 형식 정의를 비롯하여 더 효율적으로 메시징을 제어할 수 있습니다.

Hello 중 하나를 호출 하 여 사용자 지정 API 호출 [InvokeApiAsync] hello 클라이언트에 대 한 메서드. 예를 들어 다음 코드 줄을 hello 보냅니다 POST 요청 toohello **completeAll** hello 백 엔드에 API:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

이 폼은 형식화 된 메서드 호출 하며 해당 hello **MarkAllResult** 형식이 정의 반환 합니다. 형식화된 메서드와 형식화되지 않은 메서드가 모두 지원됩니다.

hello InvokeApiAsync() 메서드 앞에 추가 한다고 toocall API hello로 시작 하지 않는 한 ' / api/toohello API는 '/'입니다.
예:

* `InvokeApiAsync("completeAll",...)`hello 백 엔드에 /api/completeAll을 호출합니다.
* `InvokeApiAsync("/.auth/me",...)`hello 백 엔드에 /.auth/me를 호출합니다.

Azure 모바일 앱으로 정의 되어 있지 않은 해당 WebAPIs를 포함 하 여 모든 WebAPI InvokeApiAsync toocall를 사용할 수 있습니다.  InvokeApiAsync()를 사용 하는 경우 인증 헤더를 포함 하 여 hello 적절 한 헤더 hello 요청과 함께 전송 됩니다.

## <a name="authentication"></a>사용자 인증
Mobile Apps는 Facebook, Google, Microsoft 계정, Twitter 및 Azure Active Directory와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다. 권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다. 서버 스크립트에 인증 된 사용자 tooimplement 권한 부여 규칙의 hello id를도 사용할 수 있습니다. 자세한 내용은 hello 자습서를 참조 하십시오. [추가 인증 tooyour 앱]합니다.

두 가지의 인증 흐름이 지원 됩니다: *클라이언트 관리* 및 *서버 관리* 흐름입니다. hello 서버 관리 흐름 hello 공급자의 웹 인증 인터페이스를 사용 hello 가장 간단한 인증 경험을 제공 합니다. 더 구체적인 통합 장치 관련 기능을 공급자 특정 장치 관련 Sdk를 사용 hello 클라이언트에서 관리 하는 흐름 수 있습니다.

> [!NOTE]
> 프로덕션 앱에서 클라이언트 관리 흐름을 사용하는 것이 좋습니다.

인증을 tooset, 하나 이상의 id 공급자와 앱을 등록 해야 합니다.  hello id 공급자는 클라이언트 ID 및 앱에 대 한 클라이언트 암호를 생성합니다.  이러한 값은 프로그램 백 엔드 tooenable Azure 앱 서비스 인증/권한 부여에에서 설정 됩니다.  자세한 내용은 hello 자습서에서 필요한 세부 정보 [추가 인증 tooyour 앱]합니다.

이 섹션의 hello 다음 항목을 다룹니다.

* [클라이언트 관리 인증](#clientflow)
* [서버 관리 인증](#serverflow)
* [캐싱 hello 인증 토큰](#caching)

### <a name="clientflow"></a>클라이언트 관리 인증
앱은 hello id 공급자를 독립적으로 문의 하 고 백 엔드를 로그인 하는 동안 hello 반환 된 토큰을 제공할 수 있습니다. 이 클라이언트 흐름 tooprovide를 사용자나 hello id 공급자 로부터 tooretrieve 추가 사용자 데이터에 대 한 single sign on 환경이 있습니다. 클라이언트 흐름 인증은 기본 toousing 서버 흐름 hello id 공급자 SDK 원래의 UX 느낌을 제공 하 고 추가 사용자 지정을 허용 합니다.

클라이언트 흐름 인증 패턴을 따른 hello에 대 한 예제가 제공 됩니다.

* [Active Directory 인증 라이브러리](#adal)
* [Facebook 또는 Google](#client-facebook)
* [Live SDK](#client-livesdk)

#### <a name="adal"></a>Active Directory 인증 라이브러리 hello로 사용자를 인증
Azure Active Directory 인증을 사용 하 여 hello 클라이언트로부터 hello Active Directory 인증 라이브러리 (ADAL) tooinitiate 사용자 인증을 사용할 수 있습니다.

1. 다음 hello 하 여 AAD 로그온에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법] 자습서입니다. 네이티브 클라이언트 응용 프로그램 등록 되었는지 toocomplete hello 선택적 단계를 확인 합니다.
2. Visual Studio 또는 Xamarin Studio에서 프로젝트를 열고 추가 참조 toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet 패키지 합니다. 검색할 때 시험판 버전을 포함합니다.
3. 다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 플랫폼에 따라 hello를 추가 합니다. , 각 교체를 수행 하는 hello를 확인 합니다.

   * 대체 **INSERT-기관-여기** hello 테 넌 트 응용 프로그램을 프로 비전 하는 hello 이름의 합니다. 형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다. Hello에 Azure Active Directory에서 hello 도메인 탭에서이 값을 복사할 수 있습니다 [Azure 클래식 포털]합니다.
   * 대체 **리소스 ID 여기 삽입** 모바일 앱 백 엔드에 대 한 hello 클라이언트 ID로 합니다. Hello에서 hello 클라이언트 ID를 가져올 수 **고급** 탭의 **Azure Active Directory 설정** hello 포털에서입니다.
   * 대체 **클라이언트 ID 여기 삽입** hello 네이티브 클라이언트 응용 프로그램에서 복사한 hello 클라이언트 ID로 합니다.
   * 대체 **리디렉션 URI 여기 삽입** 웹 사이트와 */.auth/login/done* hello HTTPS 체계를 사용 하 여 끝점입니다. 이 값은 형태가 됩니다 너무*https://contoso.azurewebsites.net/.auth/login/done*합니다.

     각 플랫폼에 대해 필요한 hello 코드가 다음과 같습니다.

     **Windows:**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     **Xamarin.iOS**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     **Xamarin.Android**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <a name="client-facebook"></a>Facebook 또는 Google의 토큰을 사용하는 Single Sign-On
Facebook 또는 Google에 대 한이 코드 조각에 나와 있는 것 처럼 hello 클라이언트 흐름을 사용할 수 있습니다.

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <a name="client-livesdk"></a>Single Sign On와 Microsoft 계정을 사용 하 여 hello 라이브 SDK
tooauthenticate 사용자 hello Microsoft 계정 개발자 센터에서 앱을 등록 해야 합니다. 모바일 앱 백 엔드의 등록 세부 정보를 구성합니다. 단계를 완료 하는 hello toocreate Microsoft 계정 등록 및 tooyour 모바일 앱 백 엔드에서 연결, [등록 하면 앱 toouse Microsoft 계정 로그인]합니다. Windows 스토어 및 Windows Phone 8/Silverlight 버전 모두 응용 프로그램의 경우 hello Windows 스토어 버전을 먼저 등록 합니다.

hello 다음 코드 라이브 SDK를 사용 하 여 인증 사용 하 여 hello tooyour 모바일 앱 백 엔드에서 toosign 토큰을 반환 합니다.

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

자세한 내용은 참조 hello [Windows Live SDK] 설명서입니다.

### <a name="serverflow"></a>서버 관리 인증
Id 공급자를 등록 하면 호출 hello [LoginAsync] 메서드 [MobileServiceClient] hello로 hello [MobileServiceAuthenticationProvider] 공급자의 값입니다. 예를 들어 hello 다음 코드 시작 한 서버 흐름 로그인에서 Facebook을 사용 하 여 합니다.

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

Facebook 이외의 id 공급자를 사용 하는 경우의 hello 값 변경 [MobileServiceAuthenticationProvider] toohello 값 공급자입니다.

서버 흐름 Azure 앱 서비스는 hello 선택한 공급자의 hello 로그인 페이지를 표시 하 여 hello OAuth 인증 흐름을 관리 합니다.  한 번 hello identity provider 반환, Azure 앱 서비스 앱 서비스 인증 토큰을 생성 합니다. hello [LoginAsync] 메서드가 반환 되는 [MobileServiceUser], 모두 hello를 제공 하는 [UserId] hello 인증 사용자 및 hello [ MobileServiceAuthenticationToken], JSON 웹 토큰 (JWT). 이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다. 자세한 내용은 참조 [캐싱 hello 인증 토큰](#caching)합니다.

### <a name="caching"></a>캐싱 hello 인증 토큰
경우에 따라 hello 공급자 로부터 hello 인증 토큰을 저장 하 여 hello 통화 toohello 로그인 방법 hello 첫 번째 인증을 거친 후 피할 수 있습니다.  Windows 스토어 및 UWP 앱 צ ְ ײ [PasswordVault] toocache 현재 인증 토큰을 성공적으로 로그인 한 후 다음과 같습니다.

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

사용자 Id 값 hello hello hello 자격 증명의 사용자 이름으로 저장 됩니다 및 hello 토큰은 hello 암호 hello로 저장 합니다. 후속 업체 hello 확인할 수 있습니다 **PasswordVault** 캐시 된 자격 증명에 대 한 합니다. hello 다음 예제에서는 캐시 된 자격 증명은 검색 되 고 그렇지 않으면 tooauthenticate hello 백 엔드를 사용 하 여 다시 시도 하는 경우:

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

로그 아웃 하면 사용자를 제거 해야 hello 저장 된 자격 증명 다음과 같습니다.

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Xamarin 앱 hello를 사용 하 여 [Xamarin.Auth] Api toosecurely 저장 자격 증명에는 **계정** 개체입니다. 이러한 Api를 사용 하는 예제를 참조 hello [AuthStore.cs] hello에서 코드 파일 [ContosoMoments 사진 샘플 공유](https://github.com/azure-appservice-samples/ContosoMoments)합니다.

클라이언트에서 관리 하는 인증을 사용 하면 Facebook 또는 Twitter와 같은 공급자 로부터 얻은 hello 액세스 토큰을 캐시할 수도 있습니다. 이 토큰은 제공 된 toorequest hello 백 엔드에 있는 새 인증 토큰을 다음과 같이 될 수 있습니다.

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>푸시 알림
hello 다음 항목을 설명 푸시 알림:

* [푸시 알림 등록](#register-for-push)
* [Windows 스토어 패키지 SID 가져오기](#package-sid)
* [플랫폼 간 템플릿을 사용하여 등록](#register-xplat)

### <a name="register-for-push"></a>방법: 푸시 알림 등록
모바일 앱 클라이언트 hello Azure 알림 허브에 푸시 알림을 tooregister가 있습니다. Hello 플랫폼별에서 가져와야 하는 핸들을 가져오고를 등록할 때 푸시 알림 서비스 (PNS). 그런 다음 hello 등록을 만들 때 모든 태그와 함께이 값을 제공 합니다. hello 다음 코드를 등록 푸시 알림에 대 한 Windows 앱 Windows 알림 서비스 (WNS) hello로:

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

TooWNS를 밀어 넣는 경우 다음을 수행 해야 [Windows 스토어 패키지 SID를 가져올](#package-sid)합니다.  Windows 앱에 대 한 자세한 내용은 tooregister 템플릿 등록에 대 한 참조를 포함 하 여 [추가 푸시 알림 tooyour 앱]합니다.

Hello 클라이언트에서 태그를 요청 하는 것은 지원 되지 않습니다.  태그 요청은 등록에서 자동으로 삭제됩니다.
태그와 장치 tooregister 하려는 경우 사용자 대신 hello 알림 허브 API tooperform hello 등록을 사용 하는 사용자 지정 API를 만듭니다.  [Hello 사용자 지정 API 호출](#customapi) hello 대신 `RegisterNativeAsync()` 메서드.

### <a name="package-sid"></a>방법: Windows 스토어 패키지 SID 가져오기
Windows 스토어 앱에서 푸시 알림 사용에 패키지 SID가 필요합니다.  패키지 SID tooreceive hello Windows 저장소로 응용 프로그램을 등록 합니다.

tooobtain이이 값:

1. Visual Studio 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello Windows 스토어 응용 프로그램 프로젝트에서에서 클릭 **저장소** > **hello 저장소로 응용 프로그램 연결 중...** .
2. Hello 마법사에서 **다음**, इ न क ा Microsoft ख에서 응용 프로그램에 대 한 이름을 입력 **새로운 앱 이름 예약**, 클릭 **예약**합니다.
3. Hello 앱 등록을 성공적으로 만든 hello 응용 프로그램 이름 되 면 클릭 **다음**, 클릭 하 고 **연결**합니다.
4. Toohello 로그인 [Windows 개발자 센터] Microsoft 계정을 사용 하 여 합니다. 아래 **My apps**를 만든 hello 앱 등록을 클릭 합니다.
5. 클릭 **앱 관리** > **응용 프로그램 id**, 한 다음 toofind 아래로 스크롤하여 프로그램 **패키지 SID**합니다.

Hello 패키지 SID의 다양 한 용도로로 처리는 URI toouse 필요한 경우 *ms-app: / /* hello 구성표로 합니다. 패키지 SID 접두사로이 값을 연결 하 여 형성의 hello 버전을 기록해 둡니다.

Xamarin 앱 몇 가지 추가 코드 toobe 수 tooregister hello iOS 또는 Android 플랫폼에서 실행 되는 앱이 필요 합니다. 자세한 내용은 플랫폼 hello 항목을 참조 하십시오.

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>방법: 레지스터 푸시 템플릿 toosend 플랫폼 간 알림
tooregister 템플릿을 사용 하 여 hello `RegisterAsync()` 다음과 같이 hello 템플릿으로 메서드:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

템플릿이 있어야 `JObject` 가 입력 하 고 JSON 형식에 따라 hello에 템플릿이 여러 개 포함 될 수 있습니다.

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

메서드를 hello **RegisterAsync()** 도 보조 타일을 허용 합니다.

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

보안을 위해 등록하는 동안 모든 태그가 제거됩니다. tooadd tooinstallations 또는 템플릿을 설치 내에서 태그를 삽입 하 고 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK와 작업]을 참조 하십시오.

등록 된 이러한 템플릿을 활용 toosend 알림을 참조 toohello [알림 허브 Api]합니다.

## <a name="misc"></a>기타 토픽
### <a name="errors"></a>방법: 오류 처리
Hello 백 엔드에 오류가 발생 하는 경우 hello client SDK를 발생 한 `MobileServiceInvalidOperationException`합니다.  다음 예제에서는 어떻게 toohandle hello 백엔드에서 반환 되는 예외:

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

Hello에 오류 조건 처리 하는 또 다른 예로 있습니다 [모바일 앱 파일 샘플]합니다. [LoggingHandler] 예제는 로깅 대리자 처리기 toolog hello 요청을 보내는 toohello 백 엔드를 제공 합니다.

### <a name="headers"></a>방법: 요청 헤더 사용자 지정
toosupport 특정 앱 시나리오에서는 모바일 앱 백 엔드에서 hello와 toocustomize 통신을 할 수 있습니다. 예를 들어 원하는 tooadd 사용자 지정 헤더 tooevery 나가는 요청 또는 응답 상태 코드를 변경할 수도 수 있습니다. 사용자 지정을 사용할 수 있습니다 [DelegatingHandler]와 같이, 다음 예제는 hello:

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[추가 인증 tooyour 앱]: app-service-mobile-windows-store-dotnet-get-started-users.md
[Azure 모바일 앱에서 데이터 동기화 오프 라인]: app-service-mobile-offline-data-sync.md
[추가 푸시 알림 tooyour 앱]: app-service-mobile-windows-store-dotnet-get-started-push.md
[등록 하면 앱 toouse Microsoft 계정 로그인]: app-service-mobile-how-to-configure-microsoft-authentication.md
[tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[참조 tooan 형식화 되지 않은 테이블을 만들고]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[걸릴]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[선택]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[여기서]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure 포털]: https://portal.azure.com/
[Azure 클래식 포털]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows 개발자 센터]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[알림 허브 Api]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[모바일 앱 파일 샘플]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 설명서]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
