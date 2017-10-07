---
title: "모바일 앱을 사용 하 여 유니버설 Windows 플랫폼 (UWP) 앱에 대 한 오프 라인 동기화 aaaEnable | Microsoft Docs"
description: "자세한 내용은 방법 toouse는 Azure 모바일 앱 toocache 및 동기화 오프 라인 응용 프로그램에서 데이터 유니버설 Windows 플랫폼 (UWP)."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Windows 앱에 대해 오프라인 동기화 사용
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>개요
이 자습서 tooadd 오프 라인으로 Azure 모바일 앱 백 엔드를 사용 하 여 tooa 유니버설 Windows 플랫폼 (UWP) 앱을 지 원하는 방법을 보여 줍니다. 오프 라인 동기화 최종 사용자가 toointeract 보기, 추가 또는 네트워크 연결이 없는 경우에 데이터 요금-수정-모바일 앱을 허용 합니다. 변경 내용은 로컬 데이터베이스에 저장됩니다. Hello 장치를 다시 온라인 상태가 되 면 hello 원격 백 엔드와 이러한 변경 내용이 동기화 됩니다.

이 자습서에서는 hello 자습서에서 hello UWP 앱 프로젝트를 업데이트할 [Windows 앱을 만듭니다] toosupport hello Azure 모바일 앱의 오프 라인 기능입니다. 사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다. 서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.

hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.

## <a name="requirements"></a>요구 사항
이 자습서는 hello를 다음 사전 요구 사항이 필요 합니다.

* Windows 8.1 이상에서 실행 중인 Visual Studio 2013
* [Windows 앱 만들기][Windows 앱 만들기]을 참조하세요.
* [Azure Mobile Services SQLite Store][sqlite store nuget]
* [유니버설 Windows 플랫폼용 SQLite 개발](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Hello 클라이언트 응용 프로그램 toosupport 오프 라인 기능 업데이트
Azure 모바일 앱 오프 라인 기능을 사용 하면 로컬 데이터베이스와 toointeract 오프 라인 시나리오는 경우. toouse 응용 프로그램에서 이러한 기능을 초기화 한 [SyncContext] [ synccontext] tooa 로컬 저장소입니다. 그런 다음 hello 통해 테이블을 참조할 [IMobileServiceSyncTable][IMobileServiceSyncTable] 인터페이스입니다. SQLite는 hello hello 장치의 로컬 저장소로 사용 됩니다.

1. Hello 설치 [hello 유니버설 Windows 플랫폼에 대해 SQLite 런타임을](http://sqlite.org/2016/sqlite-uwp-3120200.vsix)합니다.
2. Visual Studio에서 hello에서 완료 된 hello UWP 앱 프로젝트에 대 한 hello NuGet 패키지 관리자를 열고 [Windows 앱을 만듭니다] 자습서입니다.
    검색 하 고 hello 설치 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 패키지 합니다.
3. 솔루션 탐색기에서 마우스 오른쪽 단추로 **참조** > **참조 추가...** > **유니버설 Windows** > **확장**을 클릭하고 **유니버설 Windows 플랫폼용 SQLite** 및 **유니버설 Windows 플랫폼 앱용 Visual C++ 2015 런타임**을 둘 다 사용하도록 설정합니다.

    ![SQLite UWP 참조 추가][1]
4. Hello MainPage.xaml.cs 파일을 열고 hello를 주석 처리 제거 `#define OFFLINE_SYNC_ENABLED` 정의 합니다.
5. Visual Studio에서 hello 키를 누릅니다. **F5** toorebuild 있고 실행된 hello 클라이언트 응용 프로그램 키입니다. hello 앱 hello 오프 라인 동기화를 사용 하도록 설정 하기 전과 같은 방법으로 작동 합니다. 그러나 hello 로컬 데이터베이스 이제 오프 라인 시나리오에서 사용할 수 있는 데이터로 채워집니다.

## <a name="update-sync"></a>Hello 백 엔드에서 hello 앱 toodisconnect 업데이트
이 섹션에서는 hello 연결 tooyour 모바일 앱 백 엔드 toosimulate 오프 라인 상황을 중단합니다. 데이터 항목을 추가할 때 예외 처리기 hello 이러한 앱은 오프 라인 모드에서 알려 줍니다. 이 상태에서 로컬 hello에 추가 된 새 항목 저장 하 고 푸시가 연결된 된 상태에서 실행 하는 경우 모바일 앱 백 엔드에서 hello에 동기화 됩니다.

1. App.xaml.cs hello 공유 프로젝트에 편집 합니다. Hello hello 초기화 주석 **MobileServiceClient** hello 다음 줄에 잘못 된 모바일 앱 URL을 사용 하 여 추가:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    또한 wifi 및 hello 장치의 셀룰러 네트워크를 사용 하지 않도록 설정 하 여 오프 라인 동작을 보여 줍니다. 하거나 비행기 모드를 사용할 수 있습니다.
2. 키를 눌러 **F5** hello 앱 toobuild 및 실행 합니다. 응용 프로그램을 시작할 때 hello 새로 고침에 실패 했습니다. 동기화를 확인 합니다.
3. 새 항목을 입력하고 [저장] 을 클릭할 때마다 푸시가 **CancelledByNetworkError**상태로 실패하는지 확인합니다. 그러나 새 할 일 항목 hello toohello 모바일 앱 백 엔드에서 푸시할 수 있습니다 때까지 hello 로컬 저장소에 존재 합니다.  프로덕션 hello 클라이언트 응용 프로그램 처럼 동작에 여전히 이러한 예외를 표시 하지 않는 경우 앱 toohello 모바일 앱 백 엔드 연결 되어 있습니다.
4. Hello 응용 프로그램을 닫고 tooverify hello 새 항목이 만든 지속형된 toohello 로컬 저장소 지 다시 시작 합니다.
5. (옵션) Visual Studio에서 **서버 탐색기**를 엽니다. tooyour 데이터베이스 이동 **Azure**->**SQL 데이터베이스**합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다. 이제 tooyour SQL 데이터베이스 테이블 및 해당 콘텐츠를 이동할 수 있습니다. Hello 백 엔드 데이터베이스의 hello 데이터가 변경 되지 않았음을 확인 합니다.
6. (선택 사항) 양식에서 GET 쿼리를 사용 하 여 모바일 백 엔드 Fiddler 또는 우체부 tooquery 같은 REST 도구를 사용 하 여 `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`합니다.

## <a name="update-online-app"></a>모바일 앱 백 엔드 hello 앱 tooreconnect 업데이트
이 섹션에서는 앱 toohello 모바일 앱 백 엔드에서 hello에 다시 연결합니다. 이러한 변경 내용은 hello 응용 프로그램에 네트워크 재연결을 시뮬레이트합니다.

Hello 응용 프로그램을 처음 실행할 때 hello `OnNavigatedTo` 이벤트 처리기 호출 `InitLocalStoreAsync`합니다. 이 메서드가 호출 하 여 `SyncAsync` toosync 로컬 hello 백 엔드 데이터베이스에 저장 합니다. hello 앱 시작 시에 toosync를 시도합니다.

1. App.xaml.cs hello 공유 프로젝트에서 열고 이전에 초기화의 주석 처리 제거 `MobileServiceClient` toouse hello 올바른 hello 모바일 앱 URL입니다.
2. 키를 눌러 hello **F5** 키 toorebuild 및 실행된 hello 앱. hello 앱 로컬 변경 내용이와 동기화 때 hello 밀어넣기 및 끌어오기 작업을 사용 하 여 hello Azure 모바일 앱 백 엔드에서 `OnNavigatedTo` 이벤트 처리기를 실행 합니다.
3. (선택 사항) 보기 hello SQL Server 개체 탐색기 또는 Fiddler와 같은 나머지 도구를 사용 하 여 데이터를 업데이트 합니다. 공지 hello 데이터 hello Azure 모바일 앱 백 엔드 데이터베이스 hello 로컬 저장소와 동기화 되었습니다.
4. Hello 응용 프로그램에서 hello 확인을 클릭 box 몇 가지 항목 toocomplete 옆에 있는 hello 로컬 저장소에 있습니다.

   `UpdateCheckedTodoItem`호출 `SyncAsync` hello 모바일 앱 백 엔드와 toosync 각 완료 된 항목입니다. `SyncAsync` 는 푸시와 끌어오기를 둘 다 호출합니다. 그러나 **hello 클라이언트에 대 한 변경 내용이 있는 테이블에 대 한 끌어오기를 실행할 때마다, 밀어넣기는 항상 자동으로 실행**합니다. 이 동작은 보장 hello 관계와 함께 로컬 저장소의 모든 테이블 일관성을 유지 합니다. 이 동작으로 예기치 않은 푸시가 발생할 수도 있습니다.  이 동작에 대한 자세한 내용은 [Azure 모바일 앱에서 데이터 동기화를 오프 라인]를 참조하세요.

## <a name="api-summary"></a>API 요약
hello 사용 toosupport 모바일 서비스의 오프 라인 기능을 hello, [IMobileServiceSyncTable] 인터페이스 및 초기화 [MobileServiceClient.SyncContext] [ synccontext] 로컬 SQLite 데이터베이스입니다. 때 오프 라인으로 hello 모바일 앱에 대 한 기본 CRUD 작업 처럼 작업 hello 작업 hello 로컬 저장소에 대해 발생 하는 동안 hello 앱은 계속 연결 되어 있습니다. hello 다음 메서드는 사용 되는 toosynchronize hello hello 서버와 로컬 저장소:

* **[PushAsync]**  이 메서드는의 구성원 이므로 [IMobileServicesSyncContext], 모든 테이블의 변경 내용이 toohello 백 엔드 푸시됩니다. 로컬 변경 내용이 지정 된 레코드만 toohello 서버에 전송 됩니다.
* **[PullAsync]** 끌어오기는 [IMobileServiceSyncTable]에서 시작됩니다. Hello 테이블에 변경 내용이 있을 때에 암시적 푸시 toomake hello 관계와 함께 로컬 저장소의 모든 테이블 일관성을 유지 하 고 있는지 실행 됩니다. hello *pushOtherTables* 암시적 푸시에서 밀어넣은 hello 컨텍스트에서 테이블 다른 여부를 제어 합니다. hello *쿼리* 매개 변수는 [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] 또는 OData 쿼리 문자열 toofilter hello 데이터를 반환 합니다. hello *queryId* 매개 변수는 사용 toodefine 증분 동기화 합니다. 자세한 내용은 [Azure Mobile Apps에서 오프라인 데이터 동기화](app-service-mobile-offline-data-sync.md#how-sync-works)를 참조하세요.
* **[PurgeAsync]**  hello 로컬 저장소에서 앱이 메서드 toopurge 부실 데이터를 주기적으로 호출 해야 합니다. 사용 하 여 hello *강제로* toopurge 아직 동기화 되지 않은 모든 변경 내용이 필요한 경우 매개 변수입니다.

이 개념에 대한 자세한 내용은 [Azure 모바일 앱에서 오프라인 데이터 동기화](app-service-mobile-offline-data-sync.md#how-sync-works)를 참조하세요.

## <a name="more-info"></a>자세한 정보
hello 다음 항목에서는 추가 배경 정보 모바일 앱의 hello 오프 라인 동기화 기능.

* [Azure 모바일 앱에서 데이터 동기화를 오프 라인]
* [Azure Mobile Apps .NET SDK 사용 방법][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[Azure 모바일 앱에서 데이터 동기화를 오프 라인]: app-service-mobile-offline-data-sync.md
[Windows 앱 만들기]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[저장]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
