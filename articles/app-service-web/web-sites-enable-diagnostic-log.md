---
title: "Azure 앱 서비스에서 웹 앱에 대 한 진단 로깅을 aaaEnable"
description: "자세한 방법을 tooenable 진단 로깅 tooaccess hello Azure에 의해 기록 된 정보는 방법에 계측 tooyour 응용 프로그램을 추가 합니다."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Azure 앱 서비스에서 웹앱에 대한 진단 로깅 설정
## <a name="overview"></a>개요
Azure에서 기본 제공 진단 tooassist 디버깅이 설정 된 상태로 제공는 [앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다. 이 문서에서는 알아봅니다 어떻게 tooenable 진단 로깅 tooaccess hello Azure에 의해 기록 된 정보는 방법에 계측 tooyour 응용 프로그램을 추가 합니다.

이 문서에서는 hello [Azure 포털](https://portal.azure.com), Azure PowerShell 및 진단 로그와 hello Azure CLI (명령줄 인터페이스 Azure) toowork 합니다. Visual Studio를 사용하여 진단 로그로 작업하는 방법에 대한 자세한 내용은 [Visual Studio에서 Azure 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>웹 서버 진단 및 응용 프로그램 진단
앱 서비스 웹 앱 hello 웹 서버와 hello 웹 응용 프로그램에서 로깅 정보에 대 한 진단 기능을 제공 합니다. 이는 논리적으로 **웹 서버 진단** 및 **응용 프로그램 진단**으로 구분됩니다.

### <a name="web-server-diagnostics"></a>웹 서버 진단
다음 종류의 로그 hello를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

* **자세한 오류 로깅** - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다. 이 hello 서버 hello 오류 코드를 반환 하는 이유를 확인 하는 데 유용한 정보를 포함할 수 있습니다.
* **요청을 추적 하지 못했습니다.** -hello IIS 구성 요소 사용 tooprocess hello 요청 및 각 구성 요소에서 수행 되는 hello 시간 추적을 포함 하 여 실패 한 요청을 대 한 상세 정보가 있습니다. 반환 된 HTTP 오류 toobe를 특정 원인을 격리 tooincrease 사이트 성능을 하려고 하는 경우에 유용할 수 있습니다.
* **웹 서버 로깅** -hello를 사용 하 여 HTTP 트랜잭션에 대 한 정보 [W3C 확장된 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다. 특정 IP 주소에서 처리 하는 요청의 hello 번호와 같은 전반적인 사이트 메트릭 또는 요청 수를 결정할 때 유용 합니다.

### <a name="application-diagnostics"></a>응용 프로그램 진단
응용 프로그램 진단 toocapture 정보를 웹 응용 프로그램에서 만든 있습니다. ASP.NET 응용 프로그램에서는 hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) 클래스 toolog 정보 toohello 응용 프로그램 진단 로그입니다. 예:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

런타임 시 이러한 로그 toohelp 문제 해결을 검색할 수 있습니다. 자세한 내용은 [Visual Studio에서 Azure 웹앱 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.

앱 서비스 웹 앱도 tooa 콘텐츠 웹 응용 프로그램을 게시할 때 배포 정보를 기록 합니다. 이는 자동으로 수행되며 배포 로깅에 대한 구성 설정은 없습니다. 배포 로깅을 통해 배포에 실패 한 이유 toodetermine 있습니다. 예를 들어 사용자 지정 배포 스크립트를 사용 하는 경우 배포 로깅 toodetermine hello 스크립트가 실패 이유를 사용할 수 있습니다.

## <a name="enablediag"></a>어떻게 tooenable 진단
hello에서 tooenable 진단 [Azure 포털](https://portal.azure.com)웹 앱에 대 한 toohello 블레이드로 이동 하 고 클릭 **설정 > 진단 로그**합니다.

<!-- todo:cleanup dogfood addresses in screenshot -->
![로그 부분](./media/web-sites-enable-diagnostic-log/logspart.png)

사용 하면 **응용 프로그램 진단** hello 선택할 수도 **수준**합니다. 이 설정을 통해 toofilter hello 정보를 너무 캡처**정보**, **경고** 또는 **오류** 정보입니다. 이 너무 설정**verbose** hello 응용 프로그램에서 생성 된 모든 정보를 기록 합니다.

> [!NOTE]
> Hello web.config를 변경 하는 달리 파일을 응용 프로그램 진단을 사용 하도록 설정 하거나 진단 로그 수준을 변경 hello 응용 프로그램 내에서 실행 되는 hello 응용 프로그램 도메인을 재활용 하지 않는 합니다.
>
>

Hello에 [클래식 포털](https://manage.windowsazure.com) 웹 앱 **구성** 탭을 선택할 수 있습니다 **저장소** 또는 **파일 시스템** 에 대 한 **웹 서버 로깅**합니다. 선택 하면 **저장소** tooselect 저장소 계정 및 hello 로그에 쓸 blob 컨테이너에 있습니다. 에 대 한 다른 모든 로그 **사이트 진단** toohello 파일 시스템에만 기록 됩니다.

hello [클래식 포털](https://manage.windowsazure.com) 웹 앱 **구성** 는 응용 프로그램 진단 위한 추가 설정도 탭:

* **파일 시스템** -저장소 hello 응용 프로그램 진단 정보 toohello 웹 응용 프로그램 파일 시스템입니다. 이러한 파일을 액세스 하 여 FTP 또는 hello Azure PowerShell 또는 Azure 명령줄 인터페이스 (Azure CLI)를 사용 하 여를 Zip 보관 파일로 다운로드 수 있습니다.
* **테이블 저장소** -저장소 hello hello 지정 된 Azure 저장소 계정 및 테이블 이름에 응용 프로그램 진단 정보입니다.
* **Blob 저장소** -저장소 hello hello 지정 된 Azure 저장소 계정과 blob 컨테이너에 응용 프로그램 진단 정보입니다.
* **보존 기간** - 기본적으로 로그는 **Blob Storage**에서 자동으로 삭제되지 않습니다. 선택 **보존 설정** hello tookeep 로그 tooautomatically를 원하는 경우 로그를 삭제 하는 일 수를 입력 합니다.

> [!NOTE]
> 경우 있습니다 [저장소 계정의 액세스 키 다시 생성](../storage/common/storage-create-storage-account.md), hello 각 로깅 구성 toouse 업데이트 hello 키를 다시 설정 해야 합니다. toodo이:
>
> 1. Hello에 **구성** 탭 너무 hello 각 로깅 기능을 설정 합니다**오프**합니다. 설정을 저장합니다.
> 2. 로깅 toohello 저장소 계정 blob 또는 테이블을 다시 사용 합니다. 설정을 저장합니다.
>
>

파일 시스템, 테이블 저장소 또는 blob 저장소의 조합이 시간, 동일 하며 개별 로그 수준 구성을 포함 하는 hello에 사용할 수 있습니다. 예를 들어 수도 있습니다 toolog 오류 및 경고 tooblob 저장소 장기 로깅 솔루션으로 자세한 정보 표시 수준으로 파일 시스템 로깅이 활성화 하는 동안.

Hello를 제공 하는 모든 세 저장소 위치 기록 된 이벤트에 대 한 기본 정보를 동일한 **테이블 저장소** 및 **blob 저장소** hello 인스턴스 ID, 스레드 ID 및 더 같은 추가 정보를 기록 합니다. 너무 로깅 보다 세분화 된 타임 스탬프 (눈금 형식)**파일 시스템**합니다.

> [!NOTE]
> **Table Storage** 또는 **Blob Storage**에 저장된 정보는 이러한 저장소 시스템에서 바로 작업할 수 있는 저장소 클라이언트 또는 응용 프로그램을 사용해서만 액세스할 수 있습니다. 예를 들어 Visual Studio 2013 사용된 tooexplore 테이블 또는 blob 저장소 일 수 있는 저장소 탐색기 있어서 HDInsight blob 저장소에 저장 된 데이터에 액세스할 수 있습니다. Hello 중 하나를 사용 하 여 Azure 저장소에 액세스 하는 응용 프로그램을 작성할 수도 있습니다 [Azure Sdk](/downloads/#)합니다.
>
> [!NOTE]
> Hello를 사용 하 여 Azure PowerShell에서 진단을 설정할 수도 있습니다 **집합 AzureWebsite** cmdlet. Azure PowerShell을 설치 하지 않은 경우 또는 구성 하지 toouse Azure 구독을 참조 [어떻게 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)합니다.
>
>

## <a name="download"></a> 방법: 로그 다운로드
저장 된 진단 정보 toohello 웹 응용 프로그램 파일 시스템은 FTP를 사용 하 여 직접 액세스할 수 있습니다. Azure PowerShell 또는 hello Azure 명령줄 인터페이스를 사용 하는 Zip 보관 파일로 다운로드할 수도 있습니다.

hello 로그에 저장 된 hello 디렉터리 구조는 다음과 같습니다.

* **응용 프로그램 로그** - /LogFiles/Application/입니다. 이 폴더에는 응용 프로그램 로깅으로 생성된 정보가 포함된 하나 이상의 텍스트 파일이 포함됩니다.
* **실패한 요청 추적** - /LogFiles/W3SVC#########/입니다. 이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다. Internet Explorer에서 볼 때 hello XSL 파일 hello XML의 hello 내용을 필터링 하 고 서식 지정 기능을 제공 하기 때문에 XML 파일 hello와 동일한 디렉터리에서 파일 hello에 hello XSL 파일을 다운로드 하는 것을 확인 합니다.
* **Detailed Error Logs** - /LogFiles/DetailedErrors/입니다. 이 폴더에는 발생한 HTTP 오류에 대해 방대한 정보를 제공하는 하나 이상의 .htm 파일이 포함되어 있습니다.
* **웹 서버 로그** - /LogFiles/http/RawLogs입니다. 이 폴더에 hello를 사용 하 여 포맷 하는 하나 이상의 텍스트 파일이 [W3C 확장된 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다.
* **Deployment logs** - /LogFiles/Git입니다. 이 폴더 포함 Azure 웹 앱에서 사용 하는 hello 내부 배포 프로세스에 의해 생성 된 로그도 Git 배포에 대 한 기록.

### <a name="ftp"></a>FTP
FTP, 방문 hello를 사용 하 여 tooaccess 진단 정보 **대시보드** hello에서 웹 응용 프로그램의 [클래식 포털](https://manage.windowsazure.com)합니다. Hello에 **눈에 보는** 섹션에서 hello를 사용 하 여 **FTP 진단 로그** tooaccess hello 로그 파일이 FTP를 사용 하 여 연결 합니다. hello **배포/FTP 사용자** 항목에 사용 되는 tooaccess hello FTP 사이트 되어야 하는 hello 사용자 이름을 표시 합니다.

> [!NOTE]
> 경우 hello **배포/FTP 사용자** 항목을 설정 하지 않으면 또는이 사용자에 대 한 hello 암호를 잊어버린, hello를 사용 하 여 새 사용자와 암호를 만들 수 있습니다 **배포 자격 증명 재설정** hello에대한링크**눈에 보는** hello 섹션 **대시보드**합니다.
>
>

### <a name="download-with-azure-powershell"></a>Azure PowerShell로 다운로드
toodownload hello 로그 파일을 Azure PowerShell의 새 인스턴스를 시작한 다음 명령을 hello를 사용 하 여:

    Save-AzureWebSiteLog -Name webappname

그러면 hello로 지정 된 hello 웹 앱에 대 한 hello 로그에 저장 됩니다 **-이름** 명명 된 매개 변수 tooa 파일 **logs.zip** hello 현재 디렉터리에 있습니다.

> [!NOTE]
> Azure PowerShell을 설치 하지 않은 경우 또는 구성 하지 toouse Azure 구독을 참조 [어떻게 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)합니다.
>
>

### <a name="download-with-azure-command-line-interface"></a>Azure 명령줄 인터페이스로 다운로드
hello Azure 명령줄 인터페이스를 사용 하 여 toodownload hello 로그 파일을 새 명령 프롬프트, PowerShell, Bash, 또는 터미널 세션 열고 hello 다음 명령을 입력 합니다.

    azure site log download webappname

그러면 라는 'webappname' tooa 파일 라는 hello 웹 앱에 대 한 hello 로그에 저장 됩니다 **diagnostics.zip** hello 현재 디렉터리에 있습니다.

> [!NOTE]
> Azure 명령줄 인터페이스 (Azure CLI) hello 또는 구성 하지 않은 것 toouse 설치 하지 않은 경우 Azure 구독을 참조 [어떻게 tooUse Azure CLI](../cli-install-nodejs.md)합니다.
>
>

## <a name="how-to-view-logs-in-application-insights"></a>방법: Application Insights에서 로그 보기
Visual Studio Application Insights는 필터링 및 로그 검색에 대 한 요청 및 기타 이벤트와 hello 로그의 상관 관계 도구를 제공 합니다.

1. Visual Studio에서 hello Application Insights SDK tooyour 프로젝트를 추가 합니다.
   * 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 추가를 선택합니다. Application Insights 리소스 만들기를 포함 하는 단계를 안내합니다. [자세히 알아보기](../application-insights/app-insights-asp-net.md)
2. Hello 추적 수신기 패키지 tooyour 프로젝트를 추가 합니다.
   * 프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다. 자동으로 로그를 삭제하려면 `Microsoft.ApplicationInsights.TraceListener` [자세히 알아보기](../application-insights/app-insights-asp-net-trace-logs.md)
3. 프로젝트를 업로드 하 고 toogenerate 로그 데이터를 실행 합니다.
4. Hello에 [Azure 포털](https://portal.azure.com/)tooyour 새 Application Insights 리소스를 찾아 열 **검색**합니다. 요청, 사용법 및 다른 원격 분석와 함께 로그 데이터가 표시됩니다. 일부 원격 분석에는 몇 분 tooarrive 걸릴 수 있습니다: 새로 고침을 클릭 합니다. [자세히 알아보기](../application-insights/app-insights-diagnostic-search.md)

[Application Insights로 추적되는 성능에 대해 알아보기](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a> 방법: 스트림 로그
응용 프로그램을 개발 하는 동안 것이 거의 실시간에 유용한 toosee 로깅 정보입니다. Azure PowerShell 또는 hello Azure 명령줄 인터페이스를 사용 하 여 로깅 정보 tooyour 개발 환경을 스트리밍 함으로써이 수행할 수 있습니다.

> [!NOTE]
> 일부 유형의 로깅 버퍼 쓰기 toohello 로그 파일을 hello 스트림에 순서가 틀린 이벤트 될 수 있습니다. 예를 들어 사용자가 페이지를 방문 하는 경우에 발생 하는 응용 프로그램 로그 항목이 hello 스트림 hello 페이지 요청에 대 한 hello 해당 HTTP 로그 항목 앞에 표시 될 수 있습니다.
>
> [!NOTE]
> 스트리밍 로그 hello에 저장 된 tooany 텍스트 파일에 기록 된 정보 또한 스트리밍되지 **d:\\홈\\LogFiles\\**  폴더입니다.
>
>

### <a name="streaming-with-azure-powershell"></a>Azure PowerShell로 스트리밍
toostream 로깅 정보는 Azure PowerShell의 새 인스턴스를 시작 하 고 다음 명령을 hello를 사용 하 여:

    Get-AzureWebSiteLog -Name webappname -Tail

그러면 hello로 지정 된 toohello 웹 앱에 연결 됩니다 **-이름** 매개 변수 및 이벤트 로그 수행 되 면 hello 웹 응용 프로그램에서 스트리밍되 기 정보 toohello PowerShell 창을 시작 합니다. Hello /LogFiles 디렉터리 (d: / 홈/로그 파일)에 저장 되어 있는.txt,.log, 또는.htm toofiles 작성 된 모든 정보 toohello 로컬 콘솔이 스트리밍됩니다.

hello를 사용 하는 오류와 같은 특정 이벤트를 toofilter **-메시지** 매개 변수입니다. 예:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

HTTP와 같이 toofilter 특정 로그 유형을 사용 하 여 hello **-경로** 매개 변수입니다. 예:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

사용 가능한 경로 사용 하 여 hello-ListPath 매개 변수 목록이 toosee 합니다.

> [!NOTE]
> Azure PowerShell을 설치 하지 않은 경우 또는 구성 하지 toouse Azure 구독을 참조 [어떻게 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)합니다.
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Azure 명령줄 인터페이스로 스트리밍
toostream 로깅 정보는 새 명령 프롬프트, PowerShell, Bash, 또는 터미널 세션 열고 hello 다음 명령을 입력 합니다.

    azure site log tail webappname

'Webappname' 라는 toohello 웹 앱에 연결 되 고 이벤트 로그 수행 되 면 hello 웹 응용 프로그램에서 정보 toohello 창 스트리밍을 시작 합니다. Hello /LogFiles 디렉터리 (d: / 홈/로그 파일)에 저장 되어 있는.txt,.log, 또는.htm toofiles 작성 된 모든 정보 toohello 로컬 콘솔이 스트리밍됩니다.

hello를 사용 하는 오류와 같은 특정 이벤트를 toofilter **-필터** 매개 변수입니다. 예:

    azure site log tail webappname --filter Error

HTTP와 같이 toofilter 특정 로그 유형을 사용 하 여 hello **-경로** 매개 변수입니다. 예:

    azure site log tail webappname --path http

> [!NOTE]
> Azure 명령줄 인터페이스 hello 또는 구성 하지 않은 것 toouse 설치 하지 않은 경우 Azure 구독을 참조 [어떻게 tooUse Azure 명령줄 인터페이스](../cli-install-nodejs.md)합니다.
>
>

## <a name="understandlogs"></a> 방법: 진단 로그 이해
### <a name="application-diagnostics-logs"></a>응용 프로그램 진단 로그
응용 프로그램 진단 로그 toohello 파일 시스템, 테이블 저장소에 저장 또는 blob 저장소에 따라.NET 응용 프로그램에 대 한 특정 형식 정보를 저장 합니다. 저장 된 데이터의 기본 집합 hello 3 개의 저장소 유형을 모두에서 동일 hello hello 날짜 및 시간 hello 이벤트가 발생 한 hello 이벤트, (정보, 경고, 오류,) hello 이벤트 유형 및 hello 이벤트 메시지를 생성 하는 hello 프로세스 ID는.

**파일 시스템**

형식에 따라 hello 각 줄 로깅된 toohello 파일 시스템 또는 스트리밍 사용 하 여 수신 됩니다.

    {Date}  PID[{process id}] {event type/level} {message}

예를 들어 오류 이벤트와 비슷한 toohello 다음 표시:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Toohello 파일 시스템 로깅 정보를 제공 hello 가장 기본적인 hello 세 사용할 수 있는 방법 중 hello 시간, 프로세스 id, 이벤트 수준 및 메시지를 제공 합니다.

**Table Storage**

Tootable 저장소를 로그인 할 때 추가 속성을 사용 하는 toofacilitate hello 이벤트에 보다 자세한 정보를 비롯 하 여 hello 테이블에 저장 된 hello 데이터를 검색 합니다. hello 다음 속성 (열)에 사용 됩니다 hello 테이블에 저장 된 각 엔터티 (행).

| 속성 이름 | 값/형식 |
| --- | --- |
| PartitionKey |YyyyMMddHH 형식에서 hello 이벤트의 날짜/시간 |
| RowKey |이 엔터티를 고유하게 식별하는 GUID 값 |
| Timestamp |hello 날짜와 시간을 hello 이벤트 발생 |
| EventTickCount |hello 날짜와 시간을 hello 이벤트 발생 눈금 형식 (큰 전체 자릿수) |
| ApplicationName |hello 웹 응용 프로그램 이름 |
| Level |이벤트 수준(예: 오류, 경고, 정보) |
| EventId |이 이벤트의 hello 이벤트 ID<p><p>지정 하지 않을 경우 too0 기본값 |
| InstanceId |발생 한도 hello hello 웹 앱의 인스턴스 |
| Pid |프로세스 ID |
| Tid |hello 이벤트를 생성 하는 hello 스레드의 hello 스레드 ID |
| Message |이벤트 세부 정보 메시지 |

**Blob 저장소**

Tooblob 저장소를 로그인 할 때 데이터는 쉼표로 구분 된 값 (CSV) 형식으로 저장 됩니다. 비슷한 tootable 저장소 추가 필드는 기록 된 tooprovide hello 이벤트에 대 한 보다 자세한 정보. hello 다음 속성을 사용 hello CSV의에서 각 행에 대해:

| 속성 이름 | 값/형식 |
| --- | --- |
| Date |hello 날짜와 시간을 hello 이벤트 발생 |
| Level |이벤트 수준(예: 오류, 경고, 정보) |
| ApplicationName |hello 웹 응용 프로그램 이름 |
| InstanceId |발생 한 이벤트 hello hello 웹 앱의 인스턴스 |
| EventTickCount |hello 날짜와 시간을 hello 이벤트 발생 눈금 형식 (큰 전체 자릿수) |
| EventId |이 이벤트의 hello 이벤트 ID<p><p>지정 하지 않을 경우 too0 기본값 |
| Pid |프로세스 ID |
| Tid |hello 이벤트를 생성 하는 hello 스레드의 hello 스레드 ID |
| Message |이벤트 세부 정보 메시지 |

blob에 저장 된 hello 데이터 toohello 다음과 비슷한 형태가 됩니다.

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> 이 예제에 표시 된 대로 hello 로그의 첫 번째 줄 hello hello 열 머리글을 포함 됩니다.
>
>

### <a name="failed-request-traces"></a>실패한 요청 추적
실패한 요청 추적은 **fr######.xml**이라는 XML 파일에 저장됩니다. toomake 것 보다 쉽게 tooview hello 기록 정보, 명명 된 XSL 스타일 시트 **freb.xsl** 에 제공 된 hello 동일 hello XML 파일 처럼 디렉터리입니다. Internet Explorer에서 hello XML 파일 중 하나를 열면 hello XSL 스타일 시트 tooprovide hello 추적 정보의 형식이 지정 된 표시를 사용 합니다. 비슷한 toohello 다음에 표시 됩니다.

![실패 한 요청 hello 브라우저에 표시](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Detailed Error Logs
자세한 오류 로그는 발생한 HTTP 오류에 대해 좀 더 자세한 정보를 제공하는 HTML 문서입니다. 이들은 단순한 HTML 문서이므로 웹 브라우저를 사용하여 볼 수 있습니다.

### <a name="web-server-logs"></a>웹 서버 로그
hello 웹 서버 로그는 서식이 지정 hello를 사용 하 여 [W3C 확장된 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다. 이 정보는 텍스트 편집기를 사용하여 읽거나 [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619)와 같은 유틸리티를 사용하여 구문 분석할 수 있습니다.

> [!NOTE]
> hello Azure 웹 앱에서 생성 된 로그를 지원 하지 않습니다 hello **s-computername**, **s ip**, 또는 **cs 버전** 필드입니다.
>
>

## <a name="nextsteps"></a> 다음 단계
* [어떻게 tooMonitor 웹 응용 프로그램](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Visual Studio에서 Azure 웹앱 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)
* [HDInsight에서 웹앱 로그 분석](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
>
>

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)
* 가이드 toohello hello 이전 포털 toohello 새 포털의 변경 참조: [탐색에 대 한 참조 hello Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)
