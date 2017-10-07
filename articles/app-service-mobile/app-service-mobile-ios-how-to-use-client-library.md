---
title: "aaaHow tooUse iOS Azure 모바일 앱에 대 한 SDK"
description: "어떻게 tooUse iOS Azure 모바일 앱에 대 한 SDK"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>어떻게 tooUse iOS Azure 모바일 앱에 대 한 클라이언트 라이브러리
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

이 가이드 최신 버전의 hello를 사용 하 여 tooperform 일반적인 시나리오에 설명 [Azure 모바일 앱 iOS SDK][1]합니다. 새로운 tooAzure 모바일 앱의 경우 먼저 완료 [Azure 모바일 앱 빠른 시작] toocreate을 백 엔드는 테이블을 만들고 미리 작성 된 iOS Xcode 프로젝트를 다운로드 합니다. 이 가이드에서는 hello 클라이언트 쪽 iOS SDK 집중 합니다. 에 대해 더 알아봅니다 toolearn hello 백 엔드에 대 한 서버 쪽 SDK hello 하 hello 서버 SDK, 방법을 참조 하십시오.

## <a name="reference-documentation"></a>참조 설명서
hello hello iOS 클라이언트 SDK에 대 한 참조 설명서는 여기에서 찾을: [Azure 모바일 앱 iOS 클라이언트 참조][2]합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼
hello iOS SDK는 iOS 버전 8.0 이상에 대 한 프로젝트 Objective-c, Swift 2.2 프로젝트 및 Swift 2.3 프로젝트를 지원합니다.

hello "서버 흐름" 인증 UI를 표시 하는 hello에 대 한 보기를 사용 합니다.  Hello 장치가 아닌 경우 수 toopresent WebView UI를 다른 인증 방법이 필요 hello 제품의 외부 hello 범위입니다.  
따라서 이 SDK는 Watch 유형 또는 그와 비슷하게 제한된 장치에는 적합하지 않습니다.

## <a name="Setup"></a>설정 및 필수 조건
이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다. 이 가이드에서는 해당 hello 테이블 해당 자습서에 hello 테이블과 같은 스키마를 가진 가정 합니다. 또한 이 가이드에서는 코드에서 `MicrosoftAzureMobile.framework`를 참조하고 `MicrosoftAzureMobile/MicrosoftAzureMobile.h`를 가져온다고 가정합니다.

## <a name="create-client"></a>방법: 클라이언트 만들기
프로젝트에는 Azure 모바일 앱 백 엔드 tooaccess 만들기는 `MSClient`합니다. 대체 `AppUrl` hello 앱 url입니다. `gatewayURLString` 및 `applicationKey`는 비워둘 수 있습니다. 인증에 대 한 게이트웨이 설정 하는 경우 채우기 `gatewayURLString` hello 게이트웨이 url입니다.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Swift**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>방법: 테이블 참조 만들기
tooaccess 또는 update 데이터 참조 toohello 백 엔드 테이블을 만듭니다. 대체 `TodoItem` 테이블의 이름으로 hello와

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Swift**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>방법: 데이터 쿼리
데이터베이스 쿼리 toocreate 쿼리 hello `MSTable` 개체입니다. hello 다음 쿼리에서 모든 항목을 가져옵니다 hello `TodoItem` 로그 hello 각 항목의 텍스트 및 합니다.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>방법: 반환된 데이터 필터링
toofilter 결과 사용할 수 있는 여러 옵션이 있습니다.

조건자를 사용 하 여 사용 하 여 toofilter는 `NSPredicate` 및 `readWithPredicate`합니다. hello 다음 반환 된 데이터 toofind만 불완전 한 일 항목을 필터링합니다.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>방법: MSQuery 사용
(정렬 및 포함 페이징), 복잡 한 쿼리를 만들 tooperform는 `MSQuery` 개체를 직접 또는 조건자를 사용 하 여:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Swift**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` 를 사용하여 여러 쿼리 동작을 제어할 수 있습니다.

* 결과의 순서 지정
* 어떤 필드 tooreturn 제한
* 레코드 tooreturn 제한
* 응답의 총 수 지정
* 요청에서 사용자 지정 쿼리 문자열 매개 변수 지정
* 추가 함수 적용

실행 프로그램 `MSQuery` 호출 하 여 쿼리 `readWithCompletion` hello 개체에 있습니다.

## <a name="sorting"></a>방법: MSQuery를 사용하여 데이터 정렬
toosort 결과 예를 살펴보겠습니다. 필드 'text' 오름차순 다음 'complete' 내림차순으로 toosort 호출 `MSQuery` 같이:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>방법: MSQuery를 사용하여 필드 제한 및 쿼리 문자열 매개 변수 확장
hello에 hello 필드의 hello 이름을 지정 하는 쿼리에서 반환 된 toolimit 필드 toobe **selectFields** 속성입니다. 이 예에서는 hello 텍스트 및 완료 된 필드를 반환합니다.

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**Swift**:

```
query.selectFields = ["text", "complete"]
```

서버 hello에에서 tooinclude 추가 쿼리 문자열 매개 변수 (예를 들어 있기 때문에 요청 하는 사용자 지정 서버 쪽 스크립트 사용)를 채울 `query.parameters` 같이:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Swift**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>방법: 페이지 크기 구성
Azure 모바일 앱으로 hello 페이지 크기 컨트롤 hello 백 엔드 테이블에서 한 번에는 찾아볼 수 있는 레코드 수가 hello 합니다. 호출을 통해서도`pull` 데이터는 다음 없습니다 자세한 레코드 toopull 없을 때까지이 페이지 크기에 따라 데이터를 일괄 처리 합니다.

가능한 tooconfigure 사용 하 여 페이지 크기는 **MSPullSettings** 다음과 같이 합니다. hello 기본 페이지 크기는 50, 한 hello 감시할 다시 too3입니다.

성능상의 이유로 다른 페이지 크기를 구성할 수 있습니다. 많은 수의 작은 데이터 레코드를 설정한 경우 높은 페이지 크기는 hello 서버 왕복 횟수를 줄입니다.

이 설정은 hello 클라이언트 쪽에서만 hello 페이지 크기를 제어합니다. Hello 페이지 크기는 hello 클라이언트 hello 모바일 앱 백 엔드 지 원하는 것 보다 더 큰 페이지 크기에 대 한 요청을 하면 구성 된 toosupport는 hello 최대 hello 백 엔드 제한 됩니다.

이 설정은 hello 이기도 *번호* 데이터 레코드의 하지 hello *바이트 크기*합니다.

Hello 클라이언트 페이지 크기를 늘리면 hello 서버의 hello 페이지 크기를 늘려야 합니다. 참조 ["방법: hello 테이블 페이징 크기 조정"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello 단계 toodo이 있습니다.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Swift**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>방법: 데이터 삽입
tooinsert 새 테이블 행을 만듭니다는 `NSDictionary` 호출 `table insert`합니다. 경우 [동적 스키마] 은 활성화 hello Azure 앱 서비스 모바일 백 엔드를 자동으로 생성 hello를 기반으로 새 열 `NSDictionary`합니다.

경우 `id` 을 제공 하지 않으면 새 고유 ID를 자동으로 생성 하는 hello 백 엔드 사용자 고유의 제공 `id` toouse 전자 메일 주소, 사용자 이름, 또는 사용자 고유의 사용자 지정 값을 id입니다. 고유한 ID를 제공하면 조인 및 비즈니스 지향적인 데이터베이스 논리가 쉬을 수 있습니다.

hello `result` hello 삽입 된 새 항목을 포함 합니다. 사용자 서버 논리에 따라 추가 있을 수 있습니다 또는 수정 된 데이터 비교 toowhat toohello 서버에 전달 되었습니다.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>방법: 데이터 수정
기존 행 tooupdate 수정 항목 및 호출 `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

Hello 행 ID 및 업데이트 하는 hello 필드 입력 또는:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

최소한 hello `id` 로 업데이트할 때 특성을 설정 해야 합니다.

## <a name="deleting"></a>방법: Blob 삭제
항목을 toodelete 호출 `delete` hello 항목:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

또는 행 ID를 제공하여 삭제합니다.

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

최소한 hello `id` 을 삭제 하는 경우 특성을 설정 해야 합니다.

## <a name="customapi"></a>방법: 사용자 지정 API 호출
사용자 지정 API를 사용하여 백 엔드 기능을 노출할 수 있습니다. Toomap tooa 테이블 작업이 되어 있지 않습니다. 메시징를 보다 상세하게 할 경우에 마찬가지 수 뿐만 아니라 읽기/set 헤더 및 hello 응답 본문 형식을 변경 합니다. hello 백 엔드에 사용자 지정 API toocreate 읽으려면 어떻게 toolearn [사용자 지정 Api](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

사용자 지정 API toocall 호출 `MSClient.invokeAPI`합니다. hello 요청 및 응답 콘텐츠를 JSON으로 처리 됩니다. toouse 다른 미디어 유형에 [사용의 다른 오버 로드를 hello `invokeAPI` ] [ 5]합니다.  toomake는 `GET` 대신의 요청에 대 한 `POST` 집합 매개 변수를 요청 `HTTPMethod` 너무`"GET"` 및 매개 변수 `body` 너무`nil` (없으므로 GET 요청 메시지의 본문입니다.) 사용자 지정 API가 다른 HTTP 동사를 지원하는 경우 `HTTPMethod`을(를) 적절하게 변경합니다.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Swift**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>방법: 레지스터 푸시 템플릿 toosend 플랫폼 간 알림
tooregister 템플릿을 사용 하 여 템플릿을 전달 프로그램 **client.push registerDeviceToken** 클라이언트 응용 프로그램에서 메서드.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Swift**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

템플릿을은 NSDictionary 형식의 이며 형식에 따라 hello에 템플릿이 여러 개 포함 될 수 있습니다.

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Swift**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

모든 태그는 보안에 대 한 hello 요청에서 제거 됩니다.  tooadd 태그 tooinstallations 또는 설치에서 템플릿을 참조 하십시오. [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][4]합니다.  등록 된 이러한 템플릿을 사용 하 여 toosend 알림 작업할 [알림 허브 Api][3]합니다.

## <a name="errors"></a>방법: 오류 처리
Hello 완성 블록에 포함 되어 Azure 앱 서비스 모바일 백 엔드를 호출 하는 경우는 `NSError` 매개 변수입니다. 오류가 발생하면 이 매개 변수는 null이 아닌 값입니다. 코드에서이 매개 변수를 확인 하 고 hello 앞에 코드 조각에서에서와 같이 필요에 따라 hello 오류를 처리 해야 합니다.

hello 파일 [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] hello 상수를 정의 `MSErrorResponseKey`, `MSErrorRequestKey`, 및 `MSErrorServerItemKey`합니다. tooget 더 많은 데이터가 관련 toohello 오류:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Swift**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

또한 hello 파일 각 오류 코드에 대 한 상수를 정의합니다.

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**Swift**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>방법: Active Directory 인증 라이브러리 hello로 사용자를 인증
Hello Active Directory 인증 라이브러리 (ADAL) toosign 사용자가 Azure Active Directory를 사용 하 여 응용 프로그램에 사용할 수 있습니다. 클라이언트 흐름 인증 id 공급자 SDK를 사용 하는 것이 좋습니다 toousing hello `loginWithProvider:completion:` 메서드.  클라이언트 흐름 인증은 UX 느낌을 그대로 제공하고 추가 사용자 지정을 허용하기 때문입니다.

1. 다음 hello 하 여 AAD 로그인에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법] [ 7] 자습서입니다. 네이티브 클라이언트 응용 프로그램 등록 되었는지 toocomplete hello 선택적 단계를 확인 합니다. Ios의 경우 해당 hello 리디렉션 URI는 hello 폼의 권장 `<app-scheme>://<bundle-id>`합니다. 자세한 내용은 참조 hello [ADAL iOS 퀵 스타트][8]합니다.
2. Cocoapods를 사용하여 ADAL을 설치합니다. 다음 정의 대체 Podfile tooinclude hello 편집 **귀하가 프로젝트** Xcode 프로젝트의 hello 이름의:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   및 Pod hello:

        pod 'ADALiOS'
3. 실행 하는 hello 터미널을 사용 하 여 `pod install` hello 디렉터리에서 프로젝트를 포함 하 고 다음 생성 된 hello hello 프로젝트가 아닌 Xcode 작업 영역을 엽니다.
4. 다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 언어에 따라 hello를 추가 합니다. 각 코드에서 다음과 같이 값을 바꿉니다.

   * 대체 **INSERT-기관-여기** hello 테 넌 트 응용 프로그램을 프로 비전 하는 hello 이름의 합니다. 형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다. Hello [Azure 클래식 포털]에서 Azure Active Directory의 hello 도메인 탭에서이 값을 복사할 수 있습니다.
   * 대체 **리소스 ID 여기 삽입** 모바일 앱 백 엔드에 대 한 hello 클라이언트 ID로 합니다. Hello에서 클라이언트 ID를 가져올 수 **고급** 탭의 **Azure Active Directory 설정** hello 포털에서입니다.
   * 대체 **클라이언트 ID 여기 삽입** hello 네이티브 클라이언트 응용 프로그램에서 복사한 hello 클라이언트 ID로 합니다.
   * 대체 **리디렉션 URI 여기 삽입** 웹 사이트와 */.auth/login/done* hello HTTPS 체계를 사용 하 여 끝점입니다. 이 값은 형태가 됩니다 너무*https://contoso.azurewebsites.net/.auth/login/done*합니다.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Swift**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>방법: iOS 용 hello Facebook SDK로 사용자를 인증
Facebook을 사용 하 여 응용 프로그램에 iOS toosign 사용자를 위한 hello Facebook SDK를 사용할 수 있습니다.  선호 toousing hello은 클라이언트 흐름 인증을 사용 하 여 `loginWithProvider:completion:` 메서드.  원래의 UX 느낌을 제공 하 고 추가 사용자 지정을 허용 하는 hello 클라이언트 흐름 인증 합니다.

1. Facebook 로그인에 대 한 모바일 앱 백 엔드에 따라 구성의 [tooconfigure Facebook 로그인에 대 한 서비스 응용 프로그램 방법] [ 9] 자습서입니다.
2. 다음 hello 하 여 iOS 용 hello Facebook SDK 설치 [Facebook SDK for iOS-시작] [ 10] 설명서입니다. 응용 프로그램을 만드는 대신 hello iOS 플랫폼 tooyour 기존 등록을 추가할 수 있습니다.
3. Facebook의 설명서는 hello 응용 프로그램 대리자에에서 일부 Objective C 코드를 포함합니다. 사용 중인 경우 **Swift**, hello 다음 AppDelegate.swift에 대 한 번역을 사용할 수 있습니다.

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. 또한 tooadding에서 `FBSDKCoreKit.framework` tooyour 프로젝트를 너무 한 참조도 추가`FBSDKLoginKit.framework` hello에서 같은 방식으로 합니다.
5. 다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 언어에 따라 hello를 추가 합니다.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Swift**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>방법: iOS용 Twitter Fabric을 사용하여 사용자 인증
Twitter를 사용 하 여 응용 프로그램에 iOS toosign 사용자에 대 한 패브릭을 사용할 수 있습니다. 흐름 인증 클라이언트는 것이 좋습니다 toousing hello `loginWithProvider:completion:` 메서드를 더 UX 느낌을 제공 하며 추가 사용자 지정을 허용 합니다.

1. Twitter 로그인에 대 한 모바일 앱 백 엔드 hello를 수행 하 여 구성 [tooconfigure Twitter 로그인에 대 한 서비스 응용 프로그램 방법](app-service-mobile-how-to-configure-twitter-authentication.md) 자습서입니다.
2. 다음 hello 하 여 패브릭 tooyour 프로젝트 추가 [iOS-시작에 대 한 패브릭] 설명서 및 TwitterKit를 설정 합니다.

   > [!NOTE]
   > 기본적으로 패브릭은 사용자를 위해 Twitter 응용 프로그램을 만듭니다. Hello 소비자 키와 이전 코드 조각 다음 hello를 사용 하 여 만든 소비자 암호를 등록 하 여 응용 프로그램을 만드는 것을 방지할 수 있습니다.    또는 hello 소비자 키를 대체할 수 있습니다 및 hello에서 tooApp 서비스 hello로 값을 제공 하는 소비자 암호 값을 참조 [패브릭 대시보드]합니다. 이 옵션을 선택 하면 값이 될 있는지 tooset hello 콜백 URL tooa 자리 표시자와 같은 `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`합니다.
   >
   >

    Toouse 앞에서 만든 hello 비밀을 선택 하면 다음 응용 프로그램 대리자 코드 tooyour hello를 추가 합니다.

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Swift**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. 다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 언어에 따라 hello를 추가 합니다.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Swift**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>방법: iOS 용 Google 로그인 SDK hello로 사용자를 인증
Google 계정을 사용 하 여 응용 프로그램에 iOS toosign 사용자를 위한 hello Google 로그인 SDK를 사용할 수 있습니다.  Google에 변경 내용을 tootheir OAuth 보안 정책을 최근에 발표 했습니다.  이러한 정책 변경 내용은 향후 hello에서 Google SDK의 hello 사용을 해야 합니다.

1. 다음 hello 여 Google 로그인에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Google 로그인에 대 한 서비스 응용 프로그램 방법](app-service-mobile-how-to-configure-google-authentication.md) 자습서입니다.
2. 다음 hello 하 여 iOS 용 hello Google SDK 설치 [Google 로그인 iOS-에 대 한 통합을 시작](https://developers.google.com/identity/sign-in/ios/start-integrating) 설명서입니다. Hello "인증를 사용 하 여 백 엔드" 섹션을 건너뛸 수 있습니다.
3. Hello tooyour 대리자의 다음 추가 `signIn:didSignInForUser:withError:` 메서드를 사용 하는 toohello 언어에 따라 합니다.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Swift**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Hello 너무 후에 추가 하 고 있는지 확인`application:didFinishLaunchingWithOptions:` 응용 프로그램에서 대리자를 해당 사용한 tooconfigure 앱 서비스 1 단계에서 ID 같습니다 "SERVER_CLIENT_ID" hello 경로로 바꿉니다.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Swift**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Hello hello를 구현 하는 UIViewController 코드 tooyour 응용 프로그램에 따라 추가 `GIDSignInUIDelegate` 프로토콜을 사용 하는 toohello 언어에 따라 합니다.  로그인을 다시 하기 전에 로그 아웃 하 고 승인 대화 상자 표시 필요 없는 tooenter 자격 증명 다시 있지만 키를 누릅니다.  Hello 세션 토큰이 만료 된 경우에이 메서드를 호출 합니다.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure 모바일 앱 빠른 시작]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[동적 스키마]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[패브릭 대시보드]: https://www.fabric.io/home
[iOS-시작에 대 한 패브릭]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
