---
title: "Azure 웹 앱에 대 한 aaaApplication 성능 Faq | Microsoft Docs"
description: "가용성, 성능 및 Azure 앱 서비스의 hello 웹 응용 프로그램 기능에 대 한 응용 프로그램 문제에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Azure의 Web Apps에 대한 응용 프로그램 성능 FAQ

이 문서는 hello에 대 한 응용 프로그램 성능 문제에 대 한 질문과 대답 (Faq) 답변 toofrequently 되어 [Azure 앱 서비스의 웹 응용 프로그램 기능](https://azure.microsoft.com/services/app-service/web/)합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>내 앱이 느린 이유는 무엇인가요?

여러 요소로 tooslow 앱 성능 영향을 줄 수 있습니다. 자세한 문제 해결 단계는 [느린 웹앱 성능 문제 해결](app-service-web-troubleshoot-performance-degradation.md)을 참조하세요.

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>높은 CPU 사용 시나리오의 문제는 어떻게 해결하나요?

일부 높은 CPU 사용 시나리오의 경우 앱에는 실제로 더 많은 컴퓨팅 리소스가 필요할 수 있습니다. 이 경우 hello 응용 프로그램에 필요한 모든 hello 리소스 가져옵니다 하므로 tooa 더 높은 서비스 계층을 확장 하는 것이 좋습니다. 다른 경우에 높은 CPU 사용은 잘못된 반복이나 코딩 사례로 인해 발생할 수 있습니다. CPU 사용 증가를 트리거하는 항목을 파악하는 프로세스는 두 부분으로 구성됩니다. 먼저 프로세스 덤프를 만들고 hello 프로세스 덤프를 분석 합니다. 자세한 내용은 [Capture and analyze a dump file for high CPU consumption for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/)(Web Apps의 높은 CPU 사용에 대한 덤프 파일 캡처 및 분석)를 참조하세요.

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>높은 메모리 사용 시나리오의 문제는 어떻게 해결하나요?

일부 높은 메모리 사용 시나리오의 경우 앱에는 실제로 더 많은 컴퓨팅 리소스가 필요할 수 있습니다. 이 경우 hello 응용 프로그램에 필요한 모든 hello 리소스 가져옵니다 하므로 tooa 더 높은 서비스 계층을 확장 하는 것이 좋습니다. 다른 시간 hello 코드의 버그 메모리 누수가 발생할 수 있습니다. 코딩 사례가 메모리 사용을 증가시킬 수도 있습니다. 높은 메모리 사용을 트리거하는 항목을 파악하는 프로세스는 두 부분으로 구성됩니다. 먼저 프로세스 덤프를 만들고 hello 프로세스 덤프를 분석 합니다. Hello Azure 사이트 확장 갤러리에서에서 충돌 진단 도구 모두 다음이 단계를 효율적으로 수행할 수 있습니다. 자세한 내용은 [Capture and analyze a dump file for intermittent high memory for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/)(Web Apps의 간헐적 높은 메모리에 대한 덤프 파일 캡처 및 분석)를 참조하세요.

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>PowerShell를 사용하여 App Service Web Apps를 어떻게 자동화할 수 있나요?

PowerShell cmdlet toomanage를 사용할 수 있으며 앱 서비스 웹 앱을 유지 관리할 수 있습니다. 이라는 블로그 게시물에서 [PowerShell을 사용 하 여 Azure 앱 서비스에서 호스팅되는 웹 응용 프로그램을 자동화](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), 설명 방법을 toouse Azure 리소스 관리자 기반 PowerShell cmdlet tooautomate 일반적인 작업입니다. hello 블로그 게시물에는 다음과 같은 다양 한 웹 앱 관리 작업에 대 한 샘플 코드가 있습니다. 모든 App Service Web Apps cmdlet에 대한 설명과 구문은 [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0)를 참조하세요.

## <a name="how-do-i-view-my-web-apps-event-logs"></a>내 웹앱의 이벤트 로그는 어떻게 볼 수 있나요?

tooview 웹 앱의 이벤트를 기록합니다.

1. Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.
2. Hello 메뉴에서 선택 **디버그 콘솔** > **CMD**합니다.
3. 선택 hello **LogFiles** 폴더입니다.
4. tooview 이벤트 로그 선택 hello 연필 아이콘 옆 너무**eventlog.xml**합니다.
5. hello PowerShell cmdlet을 실행 하는 toodownload hello 로그 `Save-AzureWebSiteLog -Name webappname`합니다.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>내 웹앱의 사용자 모드 메모리 덤프는 어떻게 캡처할 수 있나요?

웹 응용 프로그램의 사용자 모드 메모리 덤프 toocapture:

1. Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.
2. 선택 hello **프로세스 탐색기** 메뉴.
3. 마우스 오른쪽 단추로 클릭 hello **w3wp.exe** 프로세스 또는 WebJob 프로세스입니다.
4. **Download Memory Dump**(메모리 덤프 다운로드) > **Full Dump**(전체 덤프)를 선택합니다.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>내 웹앱의 프로세스 수준 정보는 어떻게 볼 수 있나요?

웹앱에 대한 프로세스 수준 정보를 보는 데는 두 가지 옵션이 있습니다.

*   Azure 포털 hello에서:
    1. 열기 hello **프로세스 탐색기** hello 웹 앱에 대 한 합니다.
    2. toosee hello 세부 정보 선택 hello **w3wp.exe** 프로세스입니다.
*   Hello Kudu 콘솔:
    1. Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.
    2. 선택 hello **프로세스 탐색기** 메뉴.
    3. Hello에 대 한 **w3wp.exe** 프로세스를 **속성**합니다.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>"오류 403-웹 앱이 중지 되었습니다." 참조 toomy 응용 프로그램을 검색 하는 경우 이 문제를 해결하려면 어떻게 해야 하나요?

이 오류는 세 가지 조건으로 인해 발생할 수 있습니다.

* hello 웹 앱에는 청구 제한에 도달 했습니다 및 사이트가 비활성화 되었습니다.
* 웹 앱 hello hello 포털에서 중지 되었습니다.
* 웹 앱 hello tooa 무료 또는 공유 규모 서비스 계획 적용 될 수 있는 리소스 할당량 한도 도달 했습니다.

toosee의 단계를 hello 오류 및 tooresolve hello 문제, 따라 hello 원인을 [웹 앱: "오류 403-이 웹 앱이 중지 되었습니다."](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/)합니다.

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>다양한 App Service 계획의 할당량 및 한도에 대한 자세한 내용은 어디서 알아볼 수 있나요?

할당량 및 한도에 대한 자세한 내용은 [App Service 한도](../azure-subscription-service-limits.md#app-service-limits)를 참조하세요. 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>유휴 시간 후 hello 첫 번째 요청에 대 한 hello 응답 시간을 줄일 하는 어떻게 하나요?

기본적으로 웹앱은 일정 기간 유휴 상태인 경우 언로드됩니다. 이러한 방식으로 hello 시스템 리소스를 절약할 수 있습니다. hello 단점은 hello 응답 toohello 첫 번째 요청이 hello 웹 응용 프로그램 로드 된 후 깁니다, tooallow 웹 응용 프로그램 tooload hello 및 응답을 처리 하는 시작입니다. 기본 및 표준 서비스 계획에서 설정할 수 있습니다 hello **Always On** 설정 tookeep hello 앱을 항상 로드 합니다. 이렇게 하면 로드 시간이 더 hello 앱이 유휴 상태 후 없습니다. toochange hello **Always On** 설정:

1. Azure 포털 hello tooyour 웹 응용 프로그램을 이동 합니다.
2. **응용 프로그램 설정**을 선택합니다.
3. **무중단**에 대해 **켜기**를 선택합니다.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>실패한 요청 추적을 어떻게 켰나요?

실패 한 요청 추적에 tooturn:

1. Azure 포털 hello tooyour 웹 응용 프로그램을 이동 합니다.
3. **모든 설정** > **진단 로그**를 선택합니다.
4. **실패한 요청 추적**에 대해 **켜기**를 선택합니다.
5. **저장**을 선택합니다.
6. Hello 웹 앱 블레이드 선택 **도구**합니다.
7. **Visual Studio Online**을 선택합니다.
8. Hello 설정이 되지 않은 경우 **에**선택, **에**합니다.
9. **이동**을 선택합니다.
10. **Web.config**를 선택합니다.
11. System.webServer,이 구성은 (toocapture 특정 URL)를 추가 합니다.

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. tootroubleshoot 속도가 느린 성능 문제를 (hello 캡처 요청에는 30 초 이상 소요 되) 하는 경우이 구성을 추가 합니다.
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. toodownload hello 실패 요청 추적을 hello [포털](https://portal.azure.com)이동, tooyour 웹 사이트입니다.
15. **도구** > **Kudu** > **이동**을 선택합니다.
18. Hello 메뉴에서 선택 **디버그 콘솔** > **CMD**합니다.
19. 선택 hello **LogFiles** 폴더 및로 시작 하는 이름으로 선택한 후 hello 폴더 **W3SVC**합니다.
20. toosee hello XML 파일 선택 hello 연필 아이콘입니다.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Hello 메시지 표시 "작업자 프로세스가 재생을 요청 due too'Percent 메모리 ' 제한 합니다." 이 문제를 어떻게 해결하나요?

hello 사용 가능한 메모리의 최대 크기는 32 비트 프로세스에 대 한 (64 비트 운영 체제) 에서도 2GB입니다. 기본적으로 hello 작업자 프로세스가 too32 비트 앱 서비스에서 (레거시 웹 응용 프로그램과 호환성)에 대 한 설정 됩니다.

웹 작업자 역할에서 사용할 수 있는 추가 메모리 hello 수 있도록 too64 비트 프로세스를 전환 하는 것이 좋습니다. 이렇게 하면 웹앱 다시 시작이 트리거되므로 이에 따라 일정이 트리거됩니다.

또한 64비트 환경에는 기본 또는 표준 서비스 계획이 필요합니다. 무료 및 공유 계획은 항상 32비트 환경에서 실행됩니다.

자세한 내용은 [Azure 앱 서비스에서 웹 앱 구성](https://docs.microsoft.com/azure/app-service-web/web-sites-configure)을 참조하세요.

## <a name="why-does-my-request-time-out-after-240-seconds"></a>240초 후 요청 시간이 초과되는 이유는 무엇인가요?

Azure Load Balancer에는 4분의 기본 유휴 시간 제한 설정이 있습니다. 이 설정은 일반적으로 웹 요청에 대한 합리적인 응답 시간 제한입니다. 웹앱에 백그라운드 처리가 필요한 경우 Azure WebJobs를 사용하는 것이 좋습니다. hello Azure 웹 앱 WebJobs를 호출할 수 있습니다 및 백그라운드 처리가 완료 될 때 알림을 받으려면 합니다. 큐 및 트리거를 포함하여 WebJobs를 사용하기 위한 여러 방법 중에서 선택할 수 있습니다.

WebJobs는 백그라운드에서 처리되도록 디자인됩니다. WebJob에서 원하는 만큼 백그라운드 처리를 수행할 수 있습니다. WebJobs에 대한 자세한 내용은 [WebJob으로 백그라운드 작업 실행](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs)을 참조하세요.

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>App Service에서 호스트되는 ASP.NET Core 응용 프로그램이 때때로 응답을 중지합니다. 이 문제를 어떻게 해결하나요?

이전 알려진된 문제로 [Kestrel 버전](https://github.com/aspnet/KestrelHttpServer/issues/1182) toointermittently 중지 응답 앱 서비스에서 호스팅되는 ASP.NET Core 1.0 응용 프로그램을 발생할 수 있습니다. 이 메시지가 표시 될 수 있습니다: "hello" 지정 된 CGI 응용 프로그램 오류 및 hello 종료 서버 hello 프로세스에서 발생 합니다.

이 문제는 Kestrel 버전 1.0.2에서 해결되었습니다. 이 버전은 hello ASP.NET Core 1.0.3 업데이트에에서 포함 됩니다. tooresolve이 문제를 응용 프로그램 종속성 toouse Kestrel 1.0.2 업데이트 해야 합니다. Hello 블로그 게시물에 설명 되어 있는 두 가지 해결 방법 중 하나를 사용할 수 또는 [앱 서비스 웹 응용 프로그램에서 ASP.NET Core 1.0 느린 성능 문제](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites)합니다.


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>웹 응용 프로그램의 hello 파일 구조에서 로그 파일 내 없을 때 어떻게 찾을 수 있나요?

앱 서비스의 hello 로컬 캐시 기능을 사용 하 여 hello 로그 파일의 hello 폴더 구조 및 데이터 폴더 응용 프로그램 서비스 인스턴스에 대 한 영향을 받습니다. 로컬 캐시를 사용 하면 하위 폴더는 hello 저장소 로그 파일 및 데이터 폴더에 생성 됩니다. hello 하위 폴더 사용 이름 지정 패턴 "고유 식별자" + 타임 스탬프 hello 합니다. 각 하위 폴더는 hello에 웹 앱이 실행 중이거나 실행 tooa VM 인스턴스를 해당 합니다.

toodetermine 로컬 캐시를 사용 하는 여부 확인 앱 서비스 **응용 프로그램 설정** 탭 합니다. 로컬 캐시를 사용 하는 경우 앱 설정 hello `WEBSITE_LOCAL_CACHE_OPTION` 너무 설정`Always`합니다. 로컬 캐시에 대 한 자세한 내용은 참조 hello [응용 프로그램 서비스 로컬 캐시 개요](https://docs.microsoft.com/azure/app-service/app-service-local-cache)합니다.

로컬 캐시를 사용하고 있지 않고 이 문제가 발생하지 않으면 지원 요청을 제출합니다.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Hello 메시지 표시 "시도 된 tooaccess 소켓 액세스 권한에 의해 방식으로 수행 합니다." 이 문제를 해결하려면 어떻게 해야 하나요?

이 오류는 일반적으로 hello hello VM 인스턴스에서 아웃 바운드 TCP 연결을 사용 하는 경우에 발생 합니다. 앱 서비스에서 각 VM 인스턴스에 대해 설정할 수 있는 아웃 바운드 연결의 최대 수 hello에 대 한 한도가 적용 됩니다. 자세한 내용은 [Cross-VM numerical limits](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits)(VM 간 숫자 제한)를 참조하세요.

또한이 오류 응용 프로그램에서 tooaccess 로컬 주소를 시도 하는 경우에 발생할 수 있습니다. 자세한 내용은 [Local address requests](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests)(로컬 주소 요청)를 참조하세요.

웹 앱의 아웃 바운드 연결에 대 한 자세한 내용은 hello 블로그에 대 한 게시물을 참조 하십시오. [연결 tooAzure 웹 사이트를 나가는](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/)합니다.

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Visual Studio tooremote 디버그 앱 서비스 웹 응용 프로그램으로 사용 방법

Visual Studio를 사용 하 여 웹 응용 프로그램 참조 하는 toodebug 방법을 보여 주는 자세한 연습은 [앱 서비스 웹 앱을 디버그 하는 원격](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/)합니다.
