---
title: "aaaStreaming 로그 및 콘솔"
description: "스트리밍 로그 및 콘솔 개요"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>스트리밍 로그 및 hello 콘솔
## <a name="streaming-logs"></a>스트리밍 로그
hello **Azure 포털** 는 통합된 스트리밍 로그 뷰어를 제공 추적 이벤트를 볼 수 있는 프로그램 **앱 서비스** 실시간으로 앱입니다.  

이 기능을 설정하려면 몇 가지 간단한 단계를 수행해야 합니다.

* 코드에 추적 쓰기
* 앱에 대해 응용 프로그램 **진단 로그**를 사용하도록 설정
* 기본 제공 hello에서에서 보기 hello 스트림을 **스트리밍 로그** hello에 대 한 UI **Azure 포털**합니다.

### <a name="how-toowrite-traces-in-your-code"></a>Toowrite 코드에서 추적 하는 방법
코드에 추적을 쓰는 작업은 쉽습니다.  C#에서 코드 다음 hello로 손쉽게입니다.

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Trace 클래스 hello hello System.Diagnostics 네임 스페이스에서 실행 됩니다.

Node.js 응용 프로그램에이 코드를 작성할 수 tooachieve hello 동일한 결과:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>어떻게 tooenable 뷰와 hello 스트리밍 로그
![][BrowseSitesScreenshot] 진단은 앱별로 사용하도록 설정됩니다. 이 기능을 원하는 tooenable toohello 사이트를 탐색 하 여 시작 합니다.  

![][DiagnosticsLogs]설정 메뉴에서 toohello 아래로 스크롤하여 **모니터링** 섹션을 클릭할 **(1) 진단 로그**합니다. 그런 다음 **(2) enable** **응용 프로그램 로깅 (파일 시스템)** 또는 **응용 프로그램 로깅 (blob)** hello **수준** 옵션을 사용 하면 hello 변경 추적 toocapture의 심각도 수준입니다. Hello 기능에 익숙한 tooget 방금 넣으려는 경우 hello 수준을 설정 너무**Verbose** tooensure 모든 추적 문을 수집 됩니다.

클릭 **저장** hello 블레이드의 hello 위쪽에는 준비 tooview 로그 합니다.

> [!NOTE]
> hello 더 높은 hello **심각도** hello 더 많은 리소스를 소비 된 toolog 및 hello 자세한 추적이 생성 됩니다. 있는지 확인 **심각도** 프로덕션 또는 트래픽 혼잡 사이트에 대 한 세부 정보 구성된 toohello 올바른 표시 됩니다. 
> 
> 

![][StreamingLogsScreenshot]tooview hello **스트리밍 로그** 에서 hello Azure 포털 내에서 클릭 하 여 **(1) 로그 스트림** hello에도 **모니터링** hello 설정 메뉴의 섹션입니다. 응용 프로그램은 추적 문을 작성 하는 중인 경우 hello에 표시 됩니다 **UI 로그 (2) 스트리밍** 거의 실시간으로 합니다.

## <a name="console"></a>콘솔
hello **Azure 포털** 콘솔 액세스 tooyour 응용 프로그램을 제공 합니다. 앱의 파일 시스템을 탐색하고 powershell/cmd 스크립트를 실행할 수 있습니다. Hello 콘솔 명령을 실행할 때 응용 프로그램 코드를 실행 하 여으로 동일한 사용 권한을 설정 하 여 바인딩됩니다. 액세스 tooprotected 디렉터리 또는 상승 된 권한이 필요 하는 스크립트 실행이 차단 됩니다.  

![][ConsoleScreenshot]설정 메뉴에서 아래로 스크롤하여 너무**개발 도구** 섹션을 클릭할 **(1) 콘솔** 및 hello **(2) 콘솔** UI toohello 오른쪽 열립니다.

hello에 익숙한 tooget **콘솔**, 시도 같은 기본 명령을:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
