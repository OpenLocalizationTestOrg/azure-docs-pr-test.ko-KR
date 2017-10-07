---
title: "iOS 모바일 앱 aaaEnable 오프 라인 동기화 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure 앱 서비스 모바일 앱 toocache 및 동기화 오프 라인 iOS 응용 프로그램의 데이터입니다."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>iOS 모바일 앱으로 오프라인 동기화 사용
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>개요
이 자습서에서는 iOS 용 Azure 앱 서비스의 hello 모바일 앱 기능을 오프 라인 상태와 동기화 합니다. 오프 라인 동기화 최종 사용자와 수 모바일 앱 tooview와 상호 작용, 추가 또는 네트워크 연결이 없을 때에 데이터를 수정 합니다. 변경 내용은 로컬 데이터베이스에 저장됩니다. Hello 장치를 다시 온라인 상태가 되 면 hello 원격 백 엔드에서 hello 변경 내용이 동기화 됩니다.

모바일 앱의 첫 번째 사용 환경을 경우 먼저 hello 자습서를 완료 해야 [iOS 앱 만들기]합니다. 다운로드 한 hello 서버 빠른 시작 프로젝트를 사용 하지 않는 경우에 hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다. 서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.

hello 오프 라인 동기화 기능에 대해 자세히 toolearn 참조 [모바일 앱에서 데이터 동기화를 오프 라인]합니다.

## <a name="review-sync"></a>Hello 클라이언트 동기화 코드를 검토 합니다.
hello에 대 한 다운로드 한 hello client 프로젝트 [iOS 앱 만들기] 자습서 로컬 핵심 데이터를 기반으로 데이터베이스를 사용 하 여 오프 라인 동기화를 지 원하는 코드를 이미 포함 되어 있습니다. 이 섹션에서는 이미 hello 자습서 코드에 포함 되어 요약 됩니다. Hello 기능의 개념적인 개요를 참조 하십시오. [모바일 앱에서 데이터 동기화를 오프 라인]합니다.

모바일 앱의 hello 오프 라인 데이터 동기화 기능을 사용 하 여, 최종 사용자에 게 상호 작용할 수 로컬 데이터베이스와 hello 네트워크에 액세스할 수 없는 경우에 합니다. toouse의 hello 동기화 컨텍스트를 초기화 하면 응용 프로그램에서 이러한 기능을 `MSClient` 로컬 저장소를 참조 하 고 있습니다. Hello 통해 테이블을 참조 합니다 **MSSyncTable** 인터페이스입니다.

**QSTodoService.m** (Objective-c) 또는 **ToDoTableViewController.swift** (빠른) 구성 요소 개발자는 hello 멤버 유형을 hello **syncTable** 은  **MSSyncTable**합니다. 오프라인 동기화에는 **MSTable** 대신 이 동기화 테이블 인터페이스가 사용됩니다. 동기화 테이블을 사용 하는 경우 모든 작업 toohello 로컬 저장소를 이동 하 고 명시적 푸시를 통한 원격 백 엔드 hello와만 동기화 및 끌어오기 작업 합니다.

 hello를 사용 하 여 참조 tooa 동기화 테이블 tooget **syncTableWithName** 메서드를 `MSClient`합니다. tooremove 오프 라인 동기화 기능을 사용 하 여 **tableWithName** 대신 합니다.

모든 테이블 작업을 수행할 수 있습니다, 전에 hello 로컬 저장소를 초기화 합니다. Hello 관련 코드는 다음과 같습니다.

* **Objective-C**. Hello에 **QSTodoService.init** 메서드:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**. Hello에 **ToDoTableViewController.viewDidLoad** 메서드:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   이 메서드는 hello를 사용 하 여 로컬 저장소를 만듭니다 `MSCoreDataStore` 인터페이스 hello 모바일 앱 SDK를 제공 합니다. 또는 hello를 구현 하 여 서로 다른 로컬 저장소를 제공할 수 `MSSyncContextDataSource` 프로토콜입니다. 또한 첫 번째 매개 변수를 hello **MSSyncContext** 은 사용 되는 toospecify 충돌 처리기입니다. 지났으므로 `nil`를 얻을 수 있는 hello 기본 충돌 처리기는 모든 충돌에 실패 합니다.

이제 보겠습니다 hello 실제 동기화 작업을 수행 하 고 hello 원격 백 엔드에서 데이터를 가져옵니다.

* **Objective-C**. `syncData`먼저 새 변경 내용을 푸시하고 다음 호출 **pullData** hello 원격 백 엔드에서 tooget 데이터입니다. Hello 차례로 **pullData** 메서드는 쿼리와 일치 하는 새 데이터를 가져옵니다.

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* **Swift**:
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

Objective C hello 버전에서에서 `syncData`를 먼저 호출 **pushWithCompletion** hello 동기화 컨텍스트에서 합니다. 이 메서드는의 구성원 `MSSyncContext` (및 hello 동기화 테이블이 아니라 자체) 이므로 모든 테이블에서 변경 내용을 밀어냅니다. 로컬 (작업을 통해 CUD) 어떤 방식으로든에서 수정 된 레코드만 toohello 서버에 전송 됩니다. 그런 다음 도우미 hello **pullData** 가 호출 되는 호출 **MSSyncTable.pullWithQuery** tooretrieve 원격 데이터 hello 로컬 데이터베이스에 저장 합니다.

Hello Swift 버전에서 hello 푸시 작업에 반드시 필요 없기 때문에 호출이 없습니다 너무**pushWithCompletion**합니다. 푸시 작업을 수행 하는 hello 테이블에 대 한 동기화 컨텍스트 hello에에서 보류 중인 변경 내용을 없으면 끌어오기 항상 발급 푸시를 먼저 합니다. 그러나 여러 개의 동기화 테이블, 있는 경우 최상의 tooexplicitly 호출 푸시 tooensure를 일관 된 관련된 테이블 간에 합니다.

Objective C hello 및 Swift 버전 모두에 hello를 사용할 수 있습니다 **pullWithQuery** 메서드 toospecify 쿼리 toofilter hello tooretrieve 원하는 레코드입니다. 이 예제에서는 hello 쿼리 검색 hello 원격에 있는 모든 레코드 `TodoItem` 테이블입니다.

두 번째 매개 변수를 hello **pullWithQuery** 에 사용 되는 쿼리 id로 *증분 동기화*합니다. 증분 동기화 hello 레코드를 사용 하 여 hello 마지막 동기화 이후 수정 된 레코드만 검색 `UpdatedAt` 타임 스탬프 (호출 `updatedAt` hello 로컬 저장소에) hello 쿼리 ID의 논리적 쿼리마다 고유한 설명이 포함 된 문자열 이어야 합니다 응용 프로그램입니다. tooopt 증분 비동기화 전달 `nil` 대로 hello 쿼리 id입니다. 이런 방법은 각각의 끌어오기 작업에서 모든 레코드가 검색되므로 비효율적일 수 있습니다.

hello Objective C 응용 프로그램을 수정 또는 사용자 hello 새로 고침 제스처를 수행 하면 데이터를 추가 및 실행에 동기화 됩니다.

hello Swift 앱 hello 사용자 hello 새로 고침 제스처를 수행 하는 경우 및 실행에 동기화 됩니다.

Hello 앱 동기화 경우 언제 든 지 데이터 수정 (Objective-c) 또는 (Swift 및 Objective-c) hello 앱 시작 될 때마다 해당 hello 사용자가 온라인 상태 hello 앱 가정 합니다. 이후 섹션에서 오프 라인 상태일 경우에 사용자가 편집할 수 있도록 hello 앱을 업데이트 합니다.

## <a name="review-core-data"></a>검토 hello 코어 데이터 모델
Hello 핵심 데이터 오프 라인 저장소를 사용 하면 데이터 모델의 특정 테이블 및 필드를 정의 해야 합니다. hello 샘플 응용 프로그램에는 hello 정렬 형식 사용 하 여 데이터 모델을 이미 포함 되어 있습니다. 이 섹션에서는 연습 이러한 테이블 tooshow 용도입니다.

**QSDataModel.xcdatamodeld**를 엽니다. 4 개 테이블은 SDK에서 사용 되는 3 개의 hello 정의-및 자체 하나 hello 할 일에 사용 되는 항목:
  * MS_TableOperations: 트랙 hello toobe hello 서버와 동기화 해야 하는 항목입니다.
  * MS_TableOperationErrors: 오프라인 동기화 중에 발생하는 모든 오류를 추적합니다.
  * MS_TableConfig: 트랙 hello hello 모든 끌어오기 작업에 대해 마지막 동기화 작업에 대 한 마지막 업데이트 시간입니다.
  * TodoItem: hello 할 일 항목을 저장합니다. 시스템 열 hello **createdAt**, **updatedAt**, 및 **버전** 선택적인 시스템 속성이 있습니다.

> [!NOTE]
> 모바일 앱 SDK hello로 시작 하는 열 이름을 예약 "**``**"입니다. 시스템 열 이외에 이 접두사를 사용하지 마세요. 그렇지 않으면 원격 백 엔드 hello를 사용 하는 경우 열 이름은 수정 됩니다.
>
>

Hello 오프 라인 동기화 기능을 사용 하 여 hello 3 개의 시스템 테이블 및 hello 데이터 테이블을 정의 합니다.

### <a name="system-tables"></a>시스템 테이블

**MS_TableOperations**  

![MS_TableOperations 테이블 특성][defining-core-data-tableoperations-entity]

| 특성 | 형식 |
| --- | --- |
| id | 정수 64 |
| itemId | String |
| properties | 이진 데이터 |
| 테이블 | String |
| tableKind | 정수 16 |


**MS_TableOperationErrors**

 ![MS_TableOperationErrors 테이블 특성][defining-core-data-tableoperationerrors-entity]

| 특성 | 형식 |
| --- | --- |
| id |문자열 |
| operationId |정수 64 |
| properties |이진 데이터 |
| tableKind |정수 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| 특성 | 형식 |
| --- | --- |
| id |문자열 |
| key |String |
| keyType |정수 64 |
| 테이블 |String |
| 값 |문자열 |

### <a name="data-table"></a>데이터 테이블

**TodoItem**

| 특성 | 유형 | 참고 |
| --- | --- | --- |
| id | 문자열, 필수로 표시 |원격 저장소의 기본 키 |
| complete | Boolean | 할 일 항목 필드 |
| 텍스트 |String |할 일 항목 필드 |
| createdAt | Date | (선택 사항) 너무 매핑합니다**createdAt** 시스템 속성 |
| updatedAt | Date | (선택 사항) 너무 매핑합니다**updatedAt** 시스템 속성 |
| 버전 | 문자열 | (선택 사항) 사용 되는 toodetect 충돌, 지도 tooversion |

## <a name="setup-sync"></a>Hello 응용 프로그램의 hello 동기화 동작을 변경
이 섹션에서는 응용 프로그램 시작 또는 삽입 하 고 항목을 업데이트 하는 경우에 동기화 되지 않는 되도록 hello 앱을 수정 합니다. Hello 새로 고침 제스처 단추 수행 될 때만 동기화 합니다.

**Objective-C**:

1. **QSTodoListViewController.m**, hello 변경 **viewDidLoad** tooremove 메서드 호출을 너무 hello`[self refresh]` hello 메서드의 hello 끝입니다. 이제 hello 데이터 응용 프로그램 시작 시 hello 서버와 동기화 되지 않은 합니다. 대신,이 hello 로컬 저장소의 hello 내용으로 동기화 됩니다.
2. **QSTodoService.m**, hello 정의를 수정할 `addItem` hello 항목을 삽입 한 후 동기화 하지 않습니다. Hello 제거 `self syncData` 차단 하 고 hello 다음으로 바꿉니다.

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Hello 정의를 수정할 `completeItem` 앞서 언급 했 듯이 합니다. 에 대 한 hello 블록을 제거 `self syncData` hello 다음으로 바꿉니다.
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Swift**:

`viewDidLoad`에 **ToDoTableViewController.swift**, 응용 프로그램 시작에서 동기화 할 toostop 여기에 표시 된 hello 두 줄 주석 처리 합니다. 이 문서 작성 hello 시 hello Swift Todo 앱 때 업데이트 되지 않는다 hello 서비스를 다른 사용자를 추가 하거나 항목을 완료 합니다. 응용 프로그램 시작에 대해서만 hello 서비스를 업데이트합니다.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Hello 응용 프로그램 테스트
이 섹션에서는 tooan 잘못 된 URL toosimulate 오프 라인 시나리오를 연결합니다. 보유 하는 데이터 항목을 추가할 때 hello 로컬 핵심 데이터 저장, 하지만 hello 모바일 앱 백 엔드에서 동기화 되지 것입니다.

1. hello 모바일 앱 URL을 변경 **QSTodoService.m** tooan 잘못 된 URL 및 다시 실행된 hello 응용 프로그램:

   **Objective-C**. QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**. ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. 몇 가지 할 일 항목을 추가합니다. Hello 시뮬레이터 (또는 앱 강제 닫기 hello)를 끝낸 후 다시 시작 합니다. 변경 내용이 유지되는지 확인합니다.

3. 원격 hello hello 내용을 보는 **TodoItem** 테이블:
   * Node.js 백 엔드에 대 한 이동 toohello [Azure 포털](https://portal.azure.com/) 모바일 앱 백 엔드에서 클릭 **쉽게 테이블** > **TodoItem**합니다.  
   * .NET 백 엔드의 경우 SQL Server Management Studio와 같은 SQL 도구나 Fiddler 또는 Postman 같은 REST 클라이언트를 사용합니다.  

4. Hello 새 항목이 있는지 확인 하십시오 *하지* 된 hello 서버와 동기화 합니다.

5. 변경 hello URL 백 toohello의 하나를 수정 **QSTodoService.m**, 응용 프로그램을 다시 실행된 hello 합니다.

6. 항목 목록이 hello hello 새로 고침 제스처를 수행 합니다.  
진행률 회전자가 표시됩니다.

7. 보기 hello **TodoItem** 다시 데이터입니다. hello 새로운 기능과 변경 된 할 일 항목이 표시 됩니다.

## <a name="summary"></a>요약
hello 사용 toosupport hello 오프 라인 동기화 기능을 `MSSyncTable` 인터페이스 및 초기화 `MSClient.syncContext` 로컬 저장소와 함께 합니다. 이 경우 hello 로컬 저장소에서 핵심 데이터 기반 데이터베이스.

Hello로 몇 개의 테이블을 정의 해야 핵심 데이터 로컬 저장소를 사용 하면 [시스템 속성을 수정](#review-core-data)합니다.

hello 보통 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 모바일 앱은 작동에 대 한 hello 앱에 여전히 설정 되어 있지만 hello 로컬 저장소에 대해 발생 하는 모든 hello 작업 합니다.

Hello hello 서버와 hello 로컬 저장소를 동기화 했습니다 때 사용한 **MSSyncTable.pullWithQuery** 메서드.

## <a name="additional-resources"></a>추가 리소스
* [모바일 앱에서 데이터 동기화를 오프 라인]
* [클라우드 기능: Azure 모바일 서비스에서 오프 라인 동기화] \(hello 비디오 모바일 서비스에 대 한 이지만 비슷한 방법으로 모바일 앱을 오프 라인 동기화 작동 합니다.\)

<!-- URLs. -->


[iOS 앱 만들기]: app-service-mobile-ios-get-started.md
[모바일 앱에서 데이터 동기화를 오프 라인]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[클라우드 기능: Azure 모바일 서비스에서 오프 라인 동기화]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
