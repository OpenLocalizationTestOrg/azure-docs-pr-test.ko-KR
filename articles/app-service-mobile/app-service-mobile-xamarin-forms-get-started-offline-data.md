---
title: "Azure 모바일 앱 (Xamarin.Forms)에 대 한 오프 라인 동기화 aaaEnable | Microsoft Docs"
description: "자세한 내용은 방법 toouse 앱 서비스 모바일 앱 toocache 및 동기화 오프 라인 응용 프로그램에서 데이터 Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Xamarin.Forms 모바일 앱에 대해 오프라인 동기화 사용
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>개요
이 자습서에서는 Xamarin.Forms에 대 한 Azure 모바일 앱의 hello 오프 라인 동기화 기능을 소개 합니다. 오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다. 변경 내용은 로컬 데이터베이스에 저장됩니다. Hello 장치를 다시 온라인 상태가 되 면 이러한 변경 내용은 hello 원격 서비스와 동기화 됩니다.

이 자습서는 자습서 [Xamarin iOS 앱 만들기]를 완료할 때 만드는 모바일 앱에 대 한 hello Xamarin.Forms 퀵 스타트 솔루션을 기반으로 합니다. Xamarin.Forms에 대 한 퀵 스타트 솔루션 hello hello 코드 toosupport 수 오프 라인 동기화 toobe 사용 하도록 설정 하기만 포함 되어 있습니다. 이 자습서에서는 Azure 모바일 앱의 hello 오프 라인 기능에 hello 퀵 스타트 솔루션 tooturn을 업데이트할 수 있습니다. Hello 오프 라인 관련 코드가 hello 앱에도 강조 표시합니다. 다운로드 한 hello 퀵 스타트 솔루션을 사용 하지 않으면 hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다. 서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][1]합니다.

hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인][2]합니다.

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Hello 퀵 스타트 솔루션의 오프 라인 동기화 기능을 사용 하도록 설정
hello 오프 라인 동기화 코드는 C# 전처리기 지시문을 사용 하 여 hello 프로젝트에 포함 됩니다. Hello 때 **오프 라인\_동기화\_ENABLED** 기호를 정의 이러한 코드 경로 hello 빌드에 포함 됩니다. Windows 앱 용 hello SQLite 플랫폼도 설치 해야 합니다.

1. Visual Studio에서 hello 솔루션 탐색기에서 > **솔루션에 대 한 NuGet 패키지 관리...** 다음 검색 하 고 설치는 **Microsoft.Azure.Mobile.Client.SQLiteStore** hello 솔루션의 모든 프로젝트에 대 한 NuGet 패키지 합니다.
2. Hello 솔루션 탐색기에서에서 사용 하 여 hello 프로젝트에서 hello TodoItemManager.cs 파일을 열어 **휴대용** 이식 가능한 클래스 라이브러리 프로젝트는 hello 이름에 전처리기 지시문 다음 hello 그런 다음 아래:

        #define OFFLINE_SYNC_ENABLED
3. (선택 사항) toosupport Windows 장치 hello SQLite 런타임 패키지를 다음 중 하나를 설치 합니다.

   * **Windows 8.1 런타임:** [Windows 8.1][3]용 SQLite를 설치합니다.
   * **Windows Phone 8.1:** [Windows Phone 8.1][4]용 SQLite를 설치합니다.
   * **유니버설 Windows 플랫폼** 설치 [유니버설 Windows 유니버설 hello에 대 한 SQLite][5]합니다.

     Hello 퀵 스타트 유니버설 Windows 프로젝트를 포함 하지 않으면 있지만 Xamarin forms hello 유니버설 Windows 플랫폼은 지원 됩니다.
4. (선택 사항) 각 Windows 앱 프로젝트에서 마우스 오른쪽 단추로 클릭 **참조** > **참조 추가...** , hello 확장 **Windows** 폴더 > **확장**합니다.
    적절 한 hello를 사용 하도록 설정 **Windows 용 SQLite** hello 함께 SDK **Visual c + + 2013 런타임 for Windows** SDK입니다.
    hello SQLite SDK 이름은 조금씩 각 Windows 플랫폼입니다.

## <a name="review-hello-client-sync-code"></a>Hello 클라이언트 동기화 코드를 검토 합니다.
Hello 자습서 코드 hello 내에 이미 포함 된 항목의 간략 한 개요는 다음과 같습니다 `#if OFFLINE_SYNC_ENABLED` 지시문입니다. 오프 라인 동기화 기능은 hello 이식 가능한 클래스 라이브러리 프로젝트의 hello TodoItemManager.cs 프로젝트 파일에 있습니다. Hello 기능의 개념적인 개요를 참조 하십시오. [Azure 모바일 앱에서 데이터 동기화 오프 라인][2]합니다.

* 모든 테이블 작업을 수행할 수 있습니다, 전에 hello 로컬 저장소를 초기화 합니다. hello 로컬 저장소 데이터베이스에서에서 초기화 hello **TodoItemManager** 코드 다음 hello를 사용 하 여 클래스 생성자:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    이 코드에서는 hello를 사용 하 여 새 로컬 SQLite 데이터베이스 **MobileServiceSQLiteStore** 클래스입니다.

    hello **DefineTable** 메서드 hello hello 제공 된 형식의 필드와 일치 하는 hello 로컬 저장소의 테이블을 만듭니다.  hello 형식 hello 원격 데이터베이스에 있는 모든 hello 열 tooinclude 되어 있지 않습니다. 가능한 toostore 열의 하위 집합은
* hello **todoTable** 필드에 **TodoItemManager** 는 **IMobileServiceSyncTable** 형식 대신 **IMobileServiceTable**합니다. 이 클래스는 hello 로컬 데이터베이스 모두에 대 한 만들기, 읽기, 업데이트 및 삭제 (CRUD) 테이블 작업 합니다. 때 이러한 변경 내용을 밀어넣은 toohello 모바일 앱 백 엔드를 호출 하 여 결정 **PushAsync** hello에 **IMobileServiceSyncContext**합니다. hello 동기화 상황에 맞는 사용 하면 추적 하 고 클라이언트 응용 프로그램은 수정 될 때 모든 테이블의 변경 내용 밀어넣기 테이블 관계 보존 **PushAsync** 호출 됩니다.

    hello 다음 **SyncAsync** 메서드는 hello 모바일 앱 백 엔드와 toosync:

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
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

            // Simple error/conflict handling.
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

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    이 샘플은 간단한 오류 처리 hello 기본 동기화 처리기를 사용 합니다. 실제 응용 프로그램 서버 및 네트워크 상태와 같은 다양 한 오류는 사용자 지정을 사용 하 여 충돌 하는 hello 처리 하는 것 **IMobileServiceSyncHandler** 구현 합니다.

## <a name="offline-sync-considerations"></a>오프라인 동기화 고려 사항
Hello 샘플에서 hello **SyncAsync** 시작 및 동기화를 요청 하는 경우에 메서드가 호출 됩니다.  tooinitiate Android 또는 iOS 응용 프로그램에서는 hello 항목 목록;에 있는 풀 다운에서 동기화 windows hello를 사용 하 여 **동기화** 단추입니다. 실제 응용 프로그램에서는 hello 네트워크 상태가 변경 될 때 hello 동기화 트리거 또한 되도록 수 있습니다.

끌어오기 보류 중이 있는 테이블에 대해 실행 되 로컬에서 업데이트 이전 컨텍스트 푸시를 가져오는 작업을 자동으로 트리거 hello 컨텍스트별 추적 합니다. 생략할 수 새로 고침,를 추가 하 고이 샘플에 있는 항목을 완료 하는 경우 명시적 hello **PushAsync** 호출 합니다.

Hello 원격 TodoItem 테이블의 모든 레코드를 제공 하는 hello 코드에서 쿼리, 것 뿐만 아니라 가능한 toofilter 레코드는 쿼리 id 및 쿼리를 전달 하 여 너무**PushAsync**합니다. 자세한 내용은 hello 섹션을 참조 하십시오. *증분 동기화* 에 [Azure 모바일 앱에서 데이터 동기화 오프 라인][2]합니다.

## <a name="run-hello-client-app"></a>Hello 클라이언트 앱 실행
이제 사용 하도록 설정 하는 오프 라인 동기화를 hello 클라이언트 응용 프로그램이 각 플랫폼 toopopulate hello 로컬 저장소 데이터베이스에서 한 번 이상 실행 합니다. 나중 오프 라인 시나리오를 시뮬레이션 하 고 hello 앱 오프 라인 상태인 동안 hello 로컬 저장소의 hello 데이터를 수정 합니다.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Hello 클라이언트 응용 프로그램의 hello 동기화 동작을 업데이트 합니다.
이 섹션에서는 백 엔드에 대 한 잘못 된 응용 프로그램 URL을 사용 하 여 hello 클라이언트 프로젝트 toosimulate 오프 라인 시나리오를 수정 합니다. 또는 해제할 수 있습니다 네트워크 연결 장치를 너무 이동 하 여 "비행기 모드입니다."  이러한 변경 내용은 hello 로컬 저장소에 보관 있고 동기화 되지를 추가 하거나 데이터 항목을 변경할 때 hello 연결이 다시 설정 될 때까지 toohello 백 엔드 데이터 저장소입니다.

1. 솔루션 탐색기 hello에서 hello에서 hello Constants.cs 프로젝트 파일을 엽니다 **휴대용** 의 hello 값을 변경 하 고 프로젝트 `ApplicationURL` toopoint tooan 잘못 된 URL:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Hello에서 열기 hello TodoItemManager.cs 파일 **휴대용** 프로젝트를 선택한 다음 추가 **catch** 기본 hello에 대 한 **예외** 클래스 toohello **try … catch** 블록 **SyncAsync**합니다. 이 **catch** 블록 같이 hello 예외 메시지 toohello 콘솔을 작성 합니다.

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. 빌드하고 hello 클라이언트 응용 프로그램을 실행 합니다.  새 항목을 추가합니다. 공지 예외가 hello 백 엔드와 각 시도 toosync에 대 한 hello 콘솔에 기록 됩니다. 이러한 ' 새 항목 toohello 모바일 백 엔드 푸시할 수 있습니다 때까지 hello 로컬 저장소에만 존재 합니다. 클라이언트 응용 프로그램 hello는 연결 된 toohello 백 엔드를 지 원하는 모든 만들기, 읽기, 업데이트, 삭제 (CRUD) 작업 처럼 동작 합니다.
4. Hello 응용 프로그램을 닫고 tooverify hello 새 항목이 만든 지속형된 toohello 로컬 저장소 지 다시 시작 합니다.
5. (선택 사항) Visual Studio tooview hello 데이터 hello 백 엔드 데이터베이스에 변경 되지 않은 Azure SQL 데이터베이스 테이블 toosee 프로그램을 사용 합니다.

    Visual Studio에서 **서버 탐색기**를 엽니다. tooyour 데이터베이스 이동 **Azure**->**SQL 데이터베이스**합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다. 이제 tooyour SQL 데이터베이스 테이블 및 해당 콘텐츠를 이동할 수 있습니다.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>클라이언트 응용 프로그램 tooreconnect hello 모바일 백 엔드 업데이트
이 섹션에서는 hello 앱 toohello 수 모바일 백엔드 tooan 온라인 상태로 돌아오는 hello 앱을 시뮬레이션 다시 연결 합니다. Hello 새로 고침 제스처를 수행 하는 경우 데이터는 동기화 된 tooyour 모바일 백 엔드 합니다.

1. Constants.cs를 다시 엽니다. 올바른 hello `applicationURL` toopoint toohello URL을 수정 합니다.
2. 다시 작성 하 고 hello 클라이언트 응용 프로그램을 실행 합니다. hello 응용 프로그램을 시작한 후 hello 모바일 앱 백 엔드와 toosync을 시도합니다. 예외가 발생 하지 않을 hello 디버그 콘솔 로그인 되어 있는지 확인 합니다.
3. (선택 사항) 업데이트 된 SQL Server 개체 탐색기 또는 Fiddler와 같은 나머지 도구를 사용 하 여 데이터를 보기 hello 또는 [우체부][6]합니다. 공지 hello 데이터 hello 백 엔드 데이터베이스 hello 로컬 저장소와 동기화 되었습니다.

    고 hello 데이터 hello 데이터베이스 hello 로컬 저장소와 동기화 된 앱 끊어져도 추가한 hello 항목이 포함 됩니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure Mobile Apps에서 오프라인 데이터 동기화][2]
* [Azure Mobile Apps .NET SDK 사용 방법][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
