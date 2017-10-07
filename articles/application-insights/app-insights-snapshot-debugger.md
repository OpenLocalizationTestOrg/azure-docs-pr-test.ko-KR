---
title: ".NET 응용 프로그램에 대 한 응용 프로그램 통찰력 스냅숏 디버거 aaaAzure | Microsoft Docs"
description: "프로덕션 .NET 앱에서 예외가 throw되면 디버그 스냅숏이 자동으로 수집됨"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>.NET 앱의 예외에 대한 디버그 스냅숏

예외가 발생할 때 라이브 웹 응용 프로그램에서 자동으로 디버그 스냅숏을 수집할 수 있습니다. hello 스냅숏 소스 코드의 hello 상태를 보여주며, hello 순간 hello 예외에서 변수 throw 되었습니다. hello 스냅숏 디버거 (미리 보기)에서 [Azure Application Insights](app-insights-overview.md) 웹 앱에서 예외 원격 분석을 모니터링 합니다. 프로덕션에서 toodiagnose 문제 필요한 hello 정보를 프로그램 최상위 예외를 throw 한 예외에 스냅숏을 수집 합니다. Hello 포함 [스냅숏 수집기 NuGet 패키지](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램 및 필요에 따라 컬렉션 매개 변수에서 구성 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)합니다. 스냅숏은 표시에 [예외](app-insights-asp-net-exceptions.md) hello Application Insights 포털에서 합니다.

Hello 포털 toosee hello 호출 스택에 있는 디버그 스냅숏을 볼 수 있으며 각 호출 스택 프레임에서 변수를 검사 수 있습니다. 소스 코드를 하 여 Visual Studio 2017 Enterprise를 사용 하 여 열고 스냅숏 더 강력한 디버깅 환경 tooget [Visual Studio에 대 한 hello 스냅숏 디버거 확장을 다운로드](https://aka.ms/snapshotdebugger)합니다.

스냅숏 컬렉션을 다음에 사용할 수 있습니다.
* .NET Framework 및 .NET Framework 4.5 이상을 실행하는 ASP.NET 응용 프로그램
* .NET Core 2.0 및 Windows에서 실행되는 ASP.NET Core 2.0 응용 프로그램

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>ASP.NET 응용 프로그램에 대한 스냅숏 컬렉션 구성

1. 이 작업을 아직 수행하지 않은 경우 [웹앱에서 Application Insights를 사용하도록 설정](app-insights-asp-net.md)합니다.

2. Hello 포함 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램에서 NuGet 패키지 합니다. 

3. 패키지를 너무 추가 hello hello 기본 옵션을 검토[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. 스냅숏은 보고 tooApplication Insights 예외에 대해서만 수집 됩니다. 경우에 따라 (예를 들어 hello.NET 플랫폼의 이전 버전) 할 수 있습니다 너무[예외 수집을 구성](app-insights-asp-net-exceptions.md#exceptions) hello 포털에서 스냅숏과 함께 toosee 예외입니다.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>ASP.NET Core 2.0 응용 프로그램에 대한 스냅숏 컬렉션 구성

1. 이 작업을 아직 수행하지 않은 경우 [ASP.NET Core 웹앱에서 Application Insights를 사용하도록 설정](app-insights-asp-net-core.md)합니다.

2. Hello 포함 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램에서 NuGet 패키지 합니다.

3. Hello 수정 `ConfigureServices` 응용 프로그램에서 `Startup` tooadd hello 스냅숏 수집기의 원격 분석 프로세서 클래스입니다. hello 참조 되는 버전의 hello Microsoft.ApplicationInsights.ASPNETCore NuGet 패키지에 추가 해야 하는 hello 코드에 따라 다릅니다.

   Microsoft.ApplicationInsights.AspNetCore 2.1.0의 경우 다음을 추가합니다.
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Microsoft.ApplicationInsights.AspNetCore 2.1.1의 경우 다음을 추가합니다.
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>다른 .NET 응용 프로그램에 대한 스냅숏 컬렉션 구성

1. 응용 프로그램은 이미 Application insights 계측 되지 않는 경우 하 여 시작 [Application Insights 및 설정 hello 계측 키를 사용 하도록 설정](app-insights-windows-desktop.md)합니다.

2. Hello 추가 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) 응용 프로그램에서 NuGet 패키지 합니다.

3. 스냅숏은 보고 tooApplication Insights 예외에 대해서만 수집 됩니다. 코드 tooreport toomodify를 할 수 있습니다 이러한. 응용 프로그램의 hello 구조 hello 예외 처리 코드를 고려해 지만 아래 예제는:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>권한 부여

Hello Azure 구독 소유자는 스냅숏을 조사할 수 있습니다. 다른 사용자는 소유자에 의해 권한이 부여되어야 합니다.

toogrant 권한, 할당 hello `Application Insights Snapshot Debugger` 역할 toousers 스냅숏을 검사 하 게 합니다. Tooindividual 사용자 또는 hello 대상 Application Insights 리소스에 대 한 구독 소유자가 그룹 또는 리소스 그룹이 나 구독에는이 역할을 할당할 수 있습니다.

1. Hello 액세스 제어 (IAM) 블레이드를 엽니다.
1. 안녕하세요 + 추가 단추를 클릭 합니다.
1. Hello 역할 드롭 다운 목록에서 응용 프로그램 통찰력 스냅숏 디버거를 선택 합니다.
1. 검색 하 여 사용자 tooadd hello에 대 한 이름을 입력 합니다.
1. Hello 저장 단추 tooadd hello 사용자 toohello 역할을 클릭 합니다.


[!IMPORTANT]
    스냅숏은 변수 및 매개 변수 값의 개인 정보 및 기타 중요한 정보를 포함할 수 있습니다.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>디버그 hello Application Insights 포털의 스냅숏

주어진된 예외 또는 문제 ID에 대 한 스냅숏을 경우는 **디버그 스냅숏 열기** hello에 단추가 표시 [예외](app-insights-asp-net-exceptions.md) hello Application Insights 포털에서 합니다.

![예외에서 디버그 스냅숏 열기 단추](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

Hello 디버그 스냅숏 보기, 호출 스택 및 변수 창 표시 합니다. 선택 하면 hello 호출 스택 창에 프레임 hello 호출 스택, 지역 변수를 볼 수 있습니다 및 hello 변수 창에서 해당 함수에 대 한 매개 변수를 호출 합니다.

![Hello 포털에서 디버그 스냅숏 보기](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

스냅숏에는 중요한 정보가 포함될 수 있으며 기본적으로는 볼 수 없습니다. tooview 스냅숏이 있어야 hello `Application Insights Snapshot Debugger` tooyou 할당 된 역할입니다.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Visual Studio 2017 Enterprise에서 스냅숏 디버그
1. Hello 클릭 **다운로드 스냅숏** 단추 toodownload는 `.diagsession` 파일을 Visual Studio 2017 Enterprise에서 열 수 있습니다. 

2. tooopen hello `.diagsession` 파일을 먼저 [다운로드 하 고 Visual Studio에 대 한 hello 스냅숏 디버거 확장을 설치](https://aka.ms/snapshotdebugger)합니다.

3. Hello 스냅숏 파일을 연 후에 Visual Studio에서 hello 미니 덤프 디버깅 페이지가 표시 됩니다. 클릭 **관리 코드 디버그** toostart hello 스냅숏 디버깅 합니다. hello 스냅숏 toohello hello hello 프로세스의 현재 상태를 디버깅할 수 있도록 hello 예외가 throw 된 코드 줄을 엽니다.

    ![Visual Studio에서 디버그 스냅숏 보기](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

다운로드 된 스냅숏 hello 웹 응용 프로그램 서버에서 발견 된 모든 기호 파일을 포함 합니다. 이러한 기호 파일은 소스 코드를 사용 하 여 필요한 tooassociate 스냅숏 데이터. 앱 서비스 앱에 대 한 웹 앱을 게시할 때 tooenable 기호 배포 되어 있는지 확인 합니다.

## <a name="how-snapshots-work"></a>스냅숏 작동 방식

응용 프로그램이 시작되면 응용 프로그램에서 스냅숏 요청을 모니터링하는 별도 스냅숏 업로더 프로세스가 생성됩니다. 스냅숏을 요청 될 때 프로세스를 실행 하는 hello의 섀도 복사본이 약 10 too20 분 후에 이루어집니다. hello 섀도 프로세스 다음 분석 되 고 스냅숏이 hello 주 프로세스 계속 toorun 동안 만들어지고 트래픽 toousers 제공 합니다. hello 스냅숏 위 항목은 다음 업로드 된 tooApplication Insights 파일인 관련 기호 (.pdb) 파일을 함께 필요한 tooview hello 스냅숏 합니다.

## <a name="current-limitations"></a>현재 제한 사항

### <a name="publish-symbols"></a>기호 게시
hello 스냅숏 디버거 기호 파일을 hello 프로덕션 서버 toodecode 변수 및 tooprovide Visual Studio의 디버깅 환경에 필요합니다. Visual Studio 2017 hello 15.2 릴리스의 tooApp 서비스 게시 되 면 기본적으로 릴리스 빌드에 대 한 기호를 게시 합니다. 이전 버전에서는 tooadd hello 다음 필요한 줄 tooyour 게시 프로필 `.pubxml` 기호 릴리스 모드에서 게시 된 파일:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Azure 계산 및 다른 형식에 대 한 hello 기호 파일이 되도록 hello에 hello 주 응용 프로그램.dll의 같은 폴더 (일반적으로 `wwwroot/bin`) 또는 hello 현재 경로에 사용할 수 있습니다.

### <a name="optimized-builds"></a>최적화된 빌드
경우에 따라 hello 빌드 프로세스 동안 적용 되는 최적화로 인해 지역 변수 릴리스 빌드에서 볼 수 없습니다.

## <a name="troubleshooting"></a>문제 해결

이러한 팁에는 스냅숏 디버거 hello로 문제를 해결 하는 데 유용 합니다.

### <a name="verify-hello-instrumentation-key"></a>Hello 계측 키를 확인 합니다.

게시 된 응용 프로그램에서 hello 올바른 계측 키를 사용 하는 있는지 확인 합니다. 일반적으로 Application Insights 계측 키를 hello를 hello ApplicationInsights.config 파일에서 읽습니다. hello 값은 hello 동일 hello 포털에서 볼 수 있는 hello Application Insights 리소스에 대 한 hello 계측 키로 확인 합니다.

### <a name="check-hello-uploader-logs"></a>Hello 업 로더 로그를 확인 합니다.

스냅숏을 만들면 디스크에 미니덤프 파일(.dmp)이 생성됩니다. 별도 업 로더 프로세스는 미니 덤프 파일을 사용 하 고 모든 관련된 Pdb tooApplication Insights 스냅숏 디버거 저장소와 함께,를 업로드 합니다. Hello 미니 덤프에 성공적으로 업로드 한 후 디스크에서 삭제 됩니다. 미니 덤프 업 로더 hello에 대 한 hello 로그 파일은 디스크에 유지 됩니다. App Service 환경에서는 `D:\Home\LogFiles\Uploader_*.log`에서 이러한 로그를 찾을 수 있습니다. 사용 하 여 hello Kudu 관리 사이트에 대 한 앱 서비스 toofind 이러한 로그 파일입니다.

1. Hello Azure 포털에서에서 응용 프로그램 서비스 응용 프로그램을 엽니다.

2. 선택 hello **고급 도구** 블레이드에서 또는 검색에 대 한 **Kudu**합니다.
3. **이동**을 클릭합니다.
4. Hello에 **디버그 콘솔** 드롭다운 목록 상자에서 **CMD**합니다.
5. **LogFiles**를 클릭합니다.

이름이 `Uploader_`로 시작하고 확장명이 `.log`인 파일이 하나 이상 있어야 합니다. Hello 해당 아이콘 toodownload 있는 모든 로그 파일을 클릭 하거나 브라우저에서 열.
hello 파일 이름에는 hello 컴퓨터 이름이 포함합니다. App Service 인스턴스가 둘 이상의 컴퓨터에서 호스팅되는 경우 각 컴퓨터에 대한 별도의 로그 파일이 있습니다. Hello 업 로더 새 미니 덤프 파일을 감지 하면 hello 로그 파일에 기록 됩니다. 성공적인 업로드의 예는 다음과 같습니다.

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

이전 예에서 hello hello 계측 키는 `c12a605e73c44346a984e00000000000`합니다. 이 값은 응용 프로그램에 대 한 hello 계측 키를 일치 해야 합니다.
hello 미니 덤프 스냅숏으로 hello ID와 연관 된 `139e411a23934dc0b9ea08a626db16c5`합니다. 이 ID를 사용할 수 이후 toolocate hello Insights 분석 응용 프로그램에서에서 예외 원격 분석에 연결 합니다.

hello 업 로더 15 분 마다 한 번에 대 한 새 Pdb를 검색합니다. 예를 들면 다음과 같습니다.

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

응용 프로그램을 _하지_ hello hello 업 로더 로그는 앱 서비스에서 호스트를 hello 미니 덤프와 같은 폴더: `%TEMP%\Dumps\<ikey>` (여기서 `<ikey>` 계측 키입니다).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Application Insights를 사용 하 여 검색 스냅숏과 함께 toofind 예외

예외를 throw 하는 hello 스냅숏 id 태그가 지정 된 스냅숏을 만들 때 보고 된 tooApplication Insights hello 예외 원격 분석을 사용 하는 경우 해당 스냅숏 ID가 사용자 지정 속성으로 포함 합니다. Application Insights에서 검색 블레이드 hello를 사용 hello로 모든 원격 분석을 찾을 수 `ai.snapshot.id` 사용자 지정 속성입니다.

1. Hello Azure 포털에서에서 tooyour Application Insights 리소스를 찾아봅니다.
2. **검색**을 클릭합니다.
3. 형식 `ai.snapshot.id` 에 검색 텍스트 상자 hello 하 고 Enter 키를 누릅니다.

![Hello 포털에서 스냅숏 ID로 원격 분석을 위한 검색](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

이 검색 결과 반환 하면 스냅숏이 없습니다 hello 선택한 시간 범위에서 응용 프로그램에 대해 보고 된 tooApplication Insights 했습니다.

hello 업 로더 로그에서 특정 스냅숏 ID에 대 한 toosearch hello 검색 상자에 해당 ID를 입력 합니다. 업로드된 것을 알고 있는 스냅숏에 대한 원격 분석을 찾을 수 없는 경우 다음 단계를 따릅니다.

1. 찾고 Application Insights 리소스를 오른쪽 hello hello 계측 키를 확인 하 여 다시 확인 하십시오.

2. Hello 업 로더 로그에서 hello 타임 스탬프를 사용 하 여이 시간 범위 hello 검색 toocover의 시간 범위 필터 hello 조정 합니다.

해당 스냅숏 ID 사용 하 여 예외를 표시 되지 않는 경우 hello 예외 원격 분석 보고 tooApplication Insights 없습니다. 걸리는 hello 스냅숏 후 응용 프로그램에서 충돌 하지만 hello 예외 원격 분석을 보고 하기 전에 이러한 상황이 발생할 수 있습니다. 이 경우 앱 서비스에서 기록 하는 hello 확인 `Diagnose and solve problems` toosee 예상 되지 않았습니다 경우 다시 시작 하거나 처리 되지 않은 예외입니다.

## <a name="next-steps"></a>다음 단계

* [코드에 snappoints 설정](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) 예외를 기다리지 않고 tooget 스냅숏을 합니다.
* [웹 응용 프로그램의 예외를 진단](app-insights-asp-net-exceptions.md) 설명 방법을 toomake 자세한 예외 표시 tooApplication Insights 합니다. 
* [스마트 검색](app-insights-proactive-diagnostics.md)은 성능 예외를 자동으로 검색합니다.
