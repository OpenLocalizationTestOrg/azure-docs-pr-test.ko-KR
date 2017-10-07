---
title: "Azure 모바일 앱에서 데이터 동기화 aaaOffline | Microsoft Docs"
description: "개념적 참조 및 Azure 모바일 앱에 대 한 hello 오프 라인 데이터 동기화 기능 개요"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Azure 모바일 앱에서 오프라인 데이터 동기화
## <a name="what-is-offline-data-sync"></a>오프라인 데이터 동기화 정의
오프 라인 데이터 동기화 클라이언트 및 서버 네트워크 연결 없이 작동 하는 개발자가 toocreate 앱에 대 한 활용할 수 있는 Azure 모바일 앱의 SDK 기능에는.

오프 라인 모드에서 앱이 있는 경우 여전히 만들 고 tooa 로컬 저장소에 저장 되는 데이터를 수정할 수 있습니다. Hello 앱이 다시 온라인 상태 이면 로컬 변경 내용이 Azure 모바일 앱 백 엔드와 동기화 할 수 있습니다. hello 기능에는 둘 다에서 동일한 레코드를 변경 하는 hello 클라이언트 hello 및 백 엔드 hello 때 충돌 확인에 대 한 지원이 포함 됩니다. 충돌은 hello 서버 또는 클라이언트 hello에 처리할 수 있습니다.

오프라인 동기화의 몇 가지 혜택은 다음과 같습니다.

* Hello 장치에서 로컬로 서버 데이터를 캐시 하 여 앱 응답성을 향상
* 네트워크 문제가 있는 경우 유용한 강력한 앱 만들기
* 최종 사용자가 toocreate 허용 하 고 네트워크 액세스가 없는 거의 또는 전혀 연결 시나리오를 지 원하는 경우에 데이터를 수정 합니다.
* 여러 장치 간에 데이터를 동기화 하 고 hello 동일한 레코드가 수정 될 때 두 장치에서 충돌을 검색 합니다.
* 지연 시간이 길거나 요금제인 네트워크에 대한 네트워크 사용 제한

자습서를 따라 hello tooadd 오프 라인으로 Azure 모바일 앱을 사용 하 여 tooyour 모바일 클라이언트를 동기화 하는 방법을 보여 줍니다.

* [Android: 오프라인 동기화 사용]
* [Apache Cordova: 오프라인 동기화 사용](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: 오프라인 동기화 사용]
* [Xamarin iOS: 오프라인 동기화 사용]
* [Xamarin Android: 오프라인 동기화 사용]
* [Xamarin.Forms: 오프라인 동기화 사용](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [유니버설 Windows 플랫폼: 오프라인 동기화 사용]

## <a name="what-is-a-sync-table"></a>동기화 테이블 정의
tooaccess hello "/ 테이블" Sdk와 같은 인터페이스를 제공 하는 hello Azure 모바일 클라이언트 끝점 `IMobileServiceTable` (.NET 클라이언트 SDK) 또는 `MSTable` (iOS 클라이언트). 이러한 Api toohello Azure 모바일 앱 백 엔드에 직접 연결 하 고 hello 클라이언트 장치는 네트워크 연결 되어 있지 않은 경우 실패 합니다.

toosupport 오프 라인으로 사용할 응용 프로그램을 대신 사용 해야 hello *동기화 테이블* Api와 같은 `IMobileServiceSyncTable` (.NET 클라이언트 SDK) 또는 `MSSyncTable` (iOS 클라이언트). 동일한 CRUD 작업 (만들기, 읽기, 업데이트, 삭제) 동기화에 대해 작동 하는 모든 hello Api 테이블 또는에서 읽도록 이제를 제외 하 고 쓸 tooa *로컬 저장소*합니다. 모든 동기화 테이블 작업을 수행할 수 있습니다, 전에 hello 로컬 저장소를 초기화 합니다.

## <a name="what-is-a-local-store"></a>로컬 저장소 정의
로컬 저장소는 hello 클라이언트 장치에 hello 데이터 지 속성 계층입니다. hello Azure 모바일 앱 클라이언트 Sdk를 로컬 기본 제공 저장소 구현을 합니다. Windows, Xamarin 및 Android에서는 SQLite에 기반합니다. iOS에서는 코어 데이터에 기반합니다.

toouse hello SQLite 기반 구현 Windows 스토어 8.1 또는 Windows Phone tooinstall SQLite 확장 해야합니다. 자세한 내용은 [유니버설 Windows 플랫폼: 오프라인 동기화 사용]을 참조하세요. Android 및 iOS 버전 SQLite의 hello 장치 운영 체제 자체에 필요한 tooreference 되기 때문 SQLite의 고유한 버전에서에서 함께 제공 됩니다.

또한 개발자는 자신의 로컬 저장소를 구현할 수 있습니다. 예를 들어 hello 모바일 클라이언트에서 암호화 된 형식으로 toostore 데이터를 원할 경우 SQLCipher 암호화에 사용 하는 로컬 저장소를 정의할 수 있습니다.

## <a name="what-is-a-sync-context"></a>동기화 컨텍스트 정의
*동기화 컨텍스트*는 모바일 클라이언트 개체와 연결되고(예: `IMobileServiceClient` 또는 `MSClient`) 동기화 테이블에 적용된 변경 내용을 추적합니다. hello 동기화 컨텍스트를 유지 관리는 *작업 큐*, 아니므로 나중에 CUD 작업 (Create, Update, Delete)의 정렬된 된 목록을 유지 관리 하는 toohello 서버 보낼 수 있습니다.

로컬 저장소에 연결 된 같은 초기화 메서드를 사용 하 여 hello 동기화 상황에 맞는 `IMobileServicesSyncContext.InitializeAsync(localstore)` hello에 [.NET 클라이언트 SDK]합니다.

## <a name="how-sync-works"></a>오프라인 동기화 작동 방법
동기화 테이블을 사용할 경우 클라이언트 코드는 로컬 변경이 Azure 모바일 앱 백 엔드와 동기화하는 시기를 제어합니다. 너무 호출 될 때까지 toohello 백 엔드 보내집니다 아무*푸시* 로컬 변경 내용이 있습니다. 마찬가지로, 로컬 저장소 hello 데이터로 채워지는 새 없을 때만 호출 너무*끌어오기* 데이터입니다.

* **푸시**:는 hello 동기화 컨텍스트에서 작업 밀어넣기와 hello 마지막 푸시 이후의 모든 CUD 변경 내용을 보냅니다. 한다는 참고 ¿¡´ 불가능 toosend 개별 테이블의 변경 내용만 그렇지 않으면 작업을 보낼 수 순서가 합니다. 푸시 일련의 REST 호출 tooyour Azure 모바일 앱 백 엔드, 그러면 서버 데이터베이스를 수정 하는 실행 합니다.
* **끌어오기**: 끌어오기 구독는 테이블당 별로 수행 될 수 있습니다 및 사용자 지정 된 쿼리 tooretrieve hello 서버 데이터의 하위 집합만 합니다. Azure 모바일 클라이언트 Sdk hello 다음 hello 로컬 저장소에 hello 결과 데이터를 삽입 합니다.
* **암시적 푸시**: 끌어오기를 로컬에서 업데이트 중인 테이블에 대해 실행 될 경우 hello 끌어오기 먼저 실행 하는 `push()` hello 동기화 컨텍스트에서 합니다. 이 푸시에 이미 대기 중인 변경 내용 및 hello 서버에서 새 데이터 간의 충돌을 최소화 하는 데 도움이 됩니다.
* **증분 동기화**: hello 첫 번째 매개 변수 toohello 끌어오기 작업은 한 *쿼리 이름* hello 클라이언트 에서만 사용 되는 합니다. Null이 아닌 쿼리 이름을 사용 하는 경우 Azure Mobile SDK hello 수행는 *증분 동기화*합니다. 가져오기 작업을 결과 집합이 반환 될 때마다 최신 hello `updatedAt` 해당 결과 집합의 타임 스탬프를 hello SDK 로컬 시스템 테이블에 저장 됩니다. 후속 끌어오기 작업은 해당 timestamp 이후의 레코드만 검색합니다.

  toouse 증분 동기화 서버에 의미 있는 반환 해야 `updatedAt` 값 및이 필드 별로 정렬도 지원 해야 합니다. 그러나 고유한 정렬 hello updatedAt 필드에 추가 하는 hello SDK, 있으므로 끌어오기 쿼리 자체를 사용할 수 없습니다 `orderBy` 절.

  hello 쿼리 이름을 선택 하면 문자열일 수 있지만 응용 프로그램에서 각 논리적 쿼리에 대 한 고유 해야 합니다.
  그렇지 않으면 서로 다른 끌어오기 작업 hello를 덮어쓸 수 동일한 증분 동기화 타임 스탬프와 쿼리는 잘못 된 결과 반환할 수 있습니다.

  Hello 쿼리에 매개 변수가 있으면는 한 가지 방법은 toocreate 고유 쿼리 이름을 tooincorporate hello 매개 변수 값입니다.
  예를 들어 userid를 필터링할 경우 사용자 쿼리 이름은 C#으로 다음과 같을 수 있습니다.

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  증분 동기화 되지 않음 tooopt 전달 `null` 대로 hello 쿼리 id입니다. 이 경우 모든 레코드를 검색 모든 호출에 대해 너무`PullAsync`, 잠재적으로 효율적인있지 않습니다.
* **에 한 제거**: hello 로컬 저장소를 사용 하 여 hello 내용을 지울 수 `IMobileServiceSyncTable.PurgeAsync`합니다.
  Hello 클라이언트 데이터베이스에서 오래 된 데이터가 있는 경우 또는 toodiscard 모든 보류 중인 변경 내용에의 한 제거를 할 수 있습니다.

  비우는 hello 로컬 저장소에서 테이블을 지웁니다. 있는 경우에 작업 하지 않는 한 hello 서버 데이터베이스, 예외가 hello 지우기 throw와의 동기화를 대기 중 hello *제거를 강제로* 매개 변수를 설정 합니다.

  클라이언트 hello에 유효 하지 않은 데이터의 예를 들어 가정 hello "할 일 목록" 예에서 장치 1만 완료 되지 않은 항목을 끌어오는 합니다. todoitem 표시 되어 "우유 구매" hello 서버에서 다른 장치에서 완료 합니다. 그러나 장치 1에 아직 hello 로컬 저장소에 대 한 todoitem "우유 구매" 되지 않은 항목 가려고만 때문에 완료로 표시 합니다. 제거는 이 오래된 항목을 지웁니다.

## <a name="next-steps"></a>다음 단계
* [iOS: 오프라인 동기화 사용]
* [Xamarin iOS: 오프라인 동기화 사용]
* [Xamarin Android: 오프라인 동기화 사용]
* [유니버설 Windows 플랫폼: 오프라인 동기화 사용]

<!-- Links -->
[.NET 클라이언트 SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: 오프라인 동기화 사용]: app-service-mobile-android-get-started-offline-data.md
[iOS: 오프라인 동기화 사용]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: 오프라인 동기화 사용]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: 오프라인 동기화 사용]: app-service-mobile-xamarin-android-get-started-offline-data.md
[유니버설 Windows 플랫폼: 오프라인 동기화 사용]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
