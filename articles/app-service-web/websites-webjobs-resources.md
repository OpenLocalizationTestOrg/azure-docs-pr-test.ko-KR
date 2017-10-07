---
title: "aaaAzure WebJobs 설명서 리소스"
description: "학습을 위한 리소스 권장 방법을 toouse Azure WebJobs Azure WebJobs SDK hello 및 합니다."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Azure WebJobs 설명서 리소스
## <a name="overview"></a>개요
이 항목은 연결 방법에 대 한 리소스 toodocumentation toouse Azure WebJobs Azure WebJobs SDK hello 및 합니다. Azure WebJobs 제공 쉽게 toorun 스크립트 또는 프로그램으로 백그라운드 프로세스의 hello 컨텍스트에서 [앱 서비스 웹 앱, API 응용 프로그램 또는 모바일 앱](../app-service/app-service-value-prop-what-is.md)합니다. cmd, bat, exe(.NET), ps1, sh, php, py, js 및 jar와 같은 실행 파일을 업로드하고 실행할 수 있습니다. 이러한 프로그램은 일정에 따라(cron) 또는 지속적으로 WebJob으로 실행됩니다.

hello의 목적은 hello [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) toosimplify hello 코드가 예: 이미지 처리, 처리 큐, RSS 집계, 파일 유지 관리 같은 웹 작업이 수행할 수 있는 일반적인 작업에 대해 작성 되 고 전자 메일 보내기. hello WebJobs SDK는 Azure 저장소 및 서비스 버스 작업을 위한, 작업을 예약 하 고 오류를 처리 및 기타 여러 가지 일반적인 시나리오에 대 한 기본 제공 기능이 있습니다. 또한에 toobe, 확장 가능한 설계 되어 있으므로 [확장에 대 한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)합니다. [Azure 기능](../azure-functions/functions-overview.md) (현재 미리 보기) 버전의 hello WebJobs SDK는 C# 스크립트, Node.js, 및 다른 언어를 기반 합니다. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Visual Studio의 통합 도구를 사용하면 WebJob을 원활하게 만들고, 배포하고, 관리할 수 있습니다. 템플릿에서 WebJob을 만들고, 게시하고 관리(실행, 중지, 모니터링, 디버그)할 수 있습니다. 

hello Azure 포털에서에서 WebJobs 대시보드 hello hello hello 기능 tooinvoke WebJobs 내에서 개별 기능을 포함 하 여 WebJobs 실행에 대 한 모든 권한을 제공 하는 강력한 관리 기능을 제공 합니다. hello 대시보드 함수 런타임 및 로깅 출력에도 표시 됩니다. 

## <a name="getstarted"></a>WebJobs 및 hello WebJobs SDK 시작
* [소개 tooAzure WebJobs](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [놀라운 기능의 Azure WebJobs를 지금 바로 사용해 보세요!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) Troy Hunt의 블로그 게시물입니다.
* [Azure WebJobs 기능](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Hello WebJobs SDK는 무엇입니까](websites-dotnet-webjobs-sdk.md)
* [Microsoft Patterns and Practices에 따른 백그라운드 작업 지침](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [1.1.0 hello 발표 RTM의 Microsoft Azure WebJobs SDK](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Azure WebJobs SDK hello로 시작](websites-dotnet-webjobs-sdk-get-started.md)
* [Toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Toouse Azure blob 저장소 hello WebJobs SDK로 하는 방법](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Toouse Azure 테이블 저장소 hello WebJobs SDK로 하는 방법](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [와 toouse Azure 서비스 버스 방법 hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)
* [Azure WebJobs SDK 빠른 참조(PDF 다운로드)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [GitHub의 WebJobs 설정 설명서](https://github.com/projectkudu/kudu/wiki/Web-jobs)
* 비디오
  * [WebJobs 및 hello WebJobs SDK](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Channel 9의 Azure WebJobs 비디오 시리즈](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [WebJobs Tooling for Visual Studio 소개](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [WebJobs Tooling 및 원격 디버깅](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Pranav Rastogi에서 Azure WebJobs 업데이트 - 릴리스 1.1의 확장성](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

다음 섹션는 hello를 참조 하십시오. [배포 WebJobs](#deploy) 및 [테스트 및 디버깅 WebJobs](#debug)합니다.

## <a name="deploy"></a>WebJobs 배포
* [어떻게 tooDeploy Visual Studio를 사용 하 여 Azure WebJobs](websites-dotnet-deploy-webjobs.md)
* [Toodeploy WebJobs를 사용 하 여 Azure 포털을 hello 하는 방법](web-sites-create-web-jobs.md)
* [Azure WebJobs의 명령줄 또는 연속 배달 사용](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Git 배포는.NET 콘솔 응용 프로그램 tooAzure Webjob 사용](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [F # WebJob tooAzure 배포](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Azure Webjobs로 사용자 지정 서비스 배포](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* 비디오
  * [WebJobs Tooling for Visual Studio 소개](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [WebJobs Tooling 및 원격 디버깅](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>WebJobs 예약
* [hello Azure WebJob 대화 상자 추가](websites-dotnet-deploy-webjobs.md#configure)
* [Hello Azure 포털에서에서 예약 된 WebJob 만들기](web-sites-create-web-jobs.md#CreateScheduled)
* [스케줄러 작업 tooa WebJob 후크](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [cron 식을 사용하여 Azure WebJob 예약](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [WebJobs SDK TimerTrigger hello를 사용 하 여 개별 WebJob 기능 예약](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>WebJob 테스트 및 디버깅
* [Visual Studio의 Azure WebJobs에 대한 새로운 개발자 및 디버깅 기능](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Hello WebJobs 대시보드를 보려면](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [WebJobs SDK hello를 사용 하 여 toowrite을 기록 하는 방법 및 대시보드 hello 설정을 확인합니다](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [원격 디버깅 WebJobs](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Blob 작성 주체](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [호스팅 클라우드 hello에 대화형 코드](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [추적 tooAzure WebJobs를 추가합니다.](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Microsoft Azure 저장소 모니터링, 진단 및 문제 해결](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* 비디오
  * [WebJobs Tooling 및 원격 디버깅](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>WebJobs 크기 조정
* [Azure 웹 사이트로 웹 응용 프로그램 크기 조정](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Azure 앱 서비스: 대규모 업무용 웹앱 보관](https://channel9.msdn.com/Events/Build/2014/3-626). 덮개 hello WebJobs SDK를 포함 하 여 웹 작업을 사용 하 여 웹 앱의 크기를 조정 합니다.
* 비디오
  * [WebJobs 크기 조정](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>추가 WebJobs 리소스
* [Magnus Mårtensson의 Azure WebJobs GA 블로그 게시물](http://magnusmartensson.com/azure-webjobs-ga)
* [Azure 앱 서비스에서 Powershell 웹 작업 실행](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Azure에서 트리거한 WebJobs 완료 시 알림 받기](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [WebJobs를 통한 간단한 웹앱 백업 보존 정책](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [최초 요청 시 느려지는 Azure 웹앱 및 클라우드 서비스](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Toouse WebJobs toosimulate만 hello 표준 가격 책정 계층에 사용할 수 있는 AlwaysOn 기능을 hello 하는 방법을 보여 줍니다.
* [WebJobs 정상 종료](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). WebJobs SDK 정상 종료에 대해서는 [정상 종료](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)를 참조하세요.
* [Azure WebJobs 및 AzCopy를 사용하여 백업 자동화](http://markjbrown.com/azure-webjobs-azcopy/)
* 비디오
  * [Magnus Mårtensson의 Azure WebJobs 비디오](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Channel 9의 Azure WebJobs 비디오 시리즈](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>추가 WebJobs SDK 리소스
* [WebJobs SDK 릴리스 정보](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [WebJobs SDK 소스 코드](https://github.com/Azure/azure-webjobs-sdk)
* [WebJobs SDK extensions 소스 코드](https://github.com/Azure/azure-webjobs-sdk-extensions)와 [자세히 살펴보도록 toohello 확장성 모델](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)합니다.  
* [WebJobs SDK 스크립트 소스 코드](https://github.com/Azure/azure-webjobs-sdk-script/)([Azure Functions](../azure-functions/functions-overview.md)에 사용)
* [WebJobs SDK hello WebJob tooupload FREB tooAzure 저장소 사용 하 여 파일](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [호스트 이점을 Azure에서 로깅 hello로 Azure 외부의 Azure webjobs를 호스팅, webjob](http://bypassion.dk/?p=510)
* [Azure WebJobs를 사용하여 데이터 가져오기 도구 구축](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Azure 함수 개요](../azure-functions/functions-overview.md)
* 비디오
  * [Channel 9의 Azure WebJobs 비디오 시리즈](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>WebJob 응용 프로그램 예제
* [GitHub의 hello WebJobs 팀에서 제공 하는 예제 응용 프로그램](https://github.com/azure/azure-webjobs-sdk-samples)
* [WebJobs 백 엔드 hello WebJobs SDK를 사용 하는 간단한 Azure 웹 앱](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). 예약된 WebJob 및 이벤트 기반 WebJob의 사용 방식을 보여 줍니다. Hello 블로그 게시물을 참조 [재구축 hello Azure WebJobs SDK를 사용 하 여 SiteMonitR](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs)합니다.

## <a name="blogs"></a>블로그
* [Azure 블로그](/blog)
* [Amit Apple의 블로그](http://blog.amitapple.com/). WebJobs (하지 hello SDK)에 초점을 맞춥니다.
* [Magnus Mårtensson의 블로그](http://magnusmartensson.com/)

## <a name="gethelp"></a>WebJobs 관련 도움말 보기
* [WebJobs의 스택 오버플로](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow hello WebJobs SDK에 대 한](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [Azure Functions의 스택 오버플로](http://stackoverflow.com/questions/tagged/azure-functions)
* [Azure 및 ASP.NET 포럼](http://forums.asp.net/1247.aspx)
* [Azure 앱 서비스 웹앱 포럼](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Azure 웹앱 사용자 음성 사이트](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Hello hashtag #AzureWebJobs를 사용 합니다.
* [WebJobs 버그 또는 문제 보고](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

