---
title: "잘못 된 게이트웨이 aaaFix 502, 503 서비스 사용할 수 없음 오류 | Microsoft Docs"
description: "Azure 앱 서비스에서 호스트되는 웹앱의 502 잘못된 게이트웨이 및 503 서비스를 사용할 수 없음 오류를 해결합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 잘못된 게이트웨이, 503 서비스를 사용할 수 없음, 오류 503, 오류 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>Azure 웹앱의 "502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" HTTP 오류 해결
"502 잘못된 게이트웨이" 및 "503 서비스를 사용할 수 없음" 오류는 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)에서 호스트되는 웹앱에서 일반적으로 나타나는 오류입니다. 이 문서는 이러한 오류를 해결하는 데 도움이 됩니다.

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 을 클릭할 **Get Support**합니다.

## <a name="symptom"></a>증상
HTTP 반환 toohello 웹 앱을 찾아볼 때 "502 잘못 된 게이트웨이" 오류 또는 HTTP "503 서비스를 사용할 수 없음" 오류입니다.

## <a name="cause"></a>원인
이 문제는 응용 프로그램 수준 문제가 원인이 되는 경우가 많습니다. 예를 들어:

* 긴 요청 시간
* 높은 메모리/CPU를 사용하는 응용 프로그램
* tooan 예외 인해 충돌 하는 응용 프로그램입니다.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>단계 toosolve "502 잘못 된 게이트웨이" 및 "503 서비스를 사용할 수 없음" 오류 문제 해결
문제 해결은 해결하는 순서대로 세 가지로 구분할 수 있습니다.

1. [응용 프로그램 작동을 관찰 및 감시](#observe)
2. [데이터 수집](#collect)
3. [Hello 문제를 완화](#mitigate)

[App Service Web Apps](/services/app-service/web/)는 각 단계별로 다양한 옵션을 제공합니다.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. 응용 프로그램 작동을 관찰 및 감시 
#### <a name="track-service-health"></a>서비스 상태를 추적합니다.
Microsoft Azure는 서비스가 중단되거나 성능이 저하될 때마다 경고를 표시합니다. Hello에서 hello 서비스의 hello 상태를 추적할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. 자세한 내용은 [서비스 상태 추적](../monitoring-and-diagnostics/insights-service-health.md)을 참조하세요.

#### <a name="monitor-your-web-app"></a>웹앱 모니터링
응용 프로그램 문제가 있는 경우 아웃 toofind가 있습니다. 웹 앱 블레이드 클릭 hello **요청 및 오류** 바둑판식으로 배열입니다. hello **메트릭을** 블레이드를 추가할 수 있습니다 하는 모든 hello 메트릭이 표시 됩니다.

알았으므로 toomonitor 웹 앱에 대 한 hello 메트릭 중 일부는

* 평균 메모리 작업 집합
* 평균 응답 시간
* CPU 시간
* 메모리 작업 집합
* 요청

![웹앱을 모니터링하여 502 잘못된 게이트웨이 및 503 서비스를 사용할 수 없음 HTTP 오류 해결](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

자세한 내용은 다음을 참조하세요.

* [Azure App Service에서 Web Apps 모니터링](web-sites-monitor.md)
* [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. 데이터 수집
#### <a name="use-hello-azure-app-service-support-portal"></a>Azure 앱 서비스 지원 포털 hello를 사용 하 여
웹 앱을 사용 하면 HTTP 로그, 이벤트 로그, 프로세스 덤프 및 자세히 확인 하 여 hello 기능 tootroubleshoot 문제 관련된 tooyour 웹 앱으로 할 수 있습니다. **http://&lt;your app name>.scm.azurewebsites.net/Support**에서 지원 포털을 사용하여 모든 정보에 액세스할 수 있습니다.

hello Azure 앱 서비스 지원 포털 세 가지 별도 탭 toosupport hello의 세 단계는 일반적인 문제 해결 시나리오를 제공 합니다.

1. 현재 동작을 관찰하기
2. 진단 정보 수집 및 기본 제공 분석기 hello를 실행 하 여 분석
3. 완화

지금 바로 hello 문제 상황을 클릭 하 여 **분석** > **진단** > **이제 진단** toocreate, 진단 세션을 HTTP를 수집 합니다는 기록, 이벤트 뷰어 로그 메모리 덤프, PHP 오류 로그 및 PHP 보고서를 처리 합니다.

Hello 데이터 수집 되 면 또한 hello 데이터에 대 한 분석을 실행 하 고 HTML 보고서를 제공 합니다.

기본적으로 toodownload hello 데이터를 원하는 경우에 hello D:\home\data\DaaS 폴더에 저장 됩니다.

Azure 앱 서비스 지원 포털 hello에 대 한 자세한 내용은 참조 하십시오. [새 업데이트 tooSupport Azure 웹 사이트에 대 한 사이트 확장](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)합니다.

#### <a name="use-hello-kudu-debug-console"></a>Hello Kudu 디버그 콘솔을 사용 하 여
Web Apps는 사용자 환경에 대한 정보를 얻을 수 있는 JSON 끝점과 비슷한 디버깅, 탐색, 파일 업로드할 수 있는 디버그 콘솔과 함께 제공됩니다. Hello 라고 *Kudu 콘솔* 또는 hello *SCM 대시보드* 웹 앱에 대 한 합니다.

Toohello 링크 이동 하 여이 대시보드에 액세스할 수 **https://&lt;응용 프로그램 이름 >.scm.azurewebsites.net/**합니다.

Kudu는 제공 하는 hello 것은 다음과 같습니다.

* 응용 프로그램에 대한 환경 설정
* 로그 스트림
* 진단 덤프
* Powershell cmdlet 및 기본 DOS 명령을 실행할 수 있는 콘솔을 디버깅합니다.

Kudu의 또 다른 유용한 특징은, 응용 프로그램 첫째 예외를 throw 하는 경우에 대비 Kudu를 사용할 수 있습니다 hello SysInternals 도구 Procdump toocreate 메모리 덤프입니다. 이러한 메모리 덤프 hello 프로세스의 스냅숏입니다 및 웹 앱과 함께 보다 복잡 한 문제를 해결 하는 데 도움이 될 수 있습니다.

Kudu에서 사용 가능한 기능에 대한 자세한 내용은 [사용자가 꼭 알아야 할 Azure 웹 사이트 온라인 도구](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)를 참조하세요.

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Hello 문제를 완화
#### <a name="scale-hello-web-app"></a>배율 hello 웹 응용 프로그램
향상 된 성능 / 처리량에 대 한 Azure 앱 서비스의 응용 프로그램을 실행 하는 hello 눈금을 조정할 수 있습니다. 두 개의 관련 된 동작에서는 웹 앱 확장: toohello 높은 가격 책정 계층을 전환한 후 특정 설정을 구성 하 고 가격 책정 계층을 더 높은 완료 된 앱 서비스 계획 tooa 변경 합니다.

크기 조정에 대한 자세한 내용은 [Azure App Service에서 웹앱 크기 조정](web-sites-scale.md)을 참조하세요.

또한 둘 이상의 인스턴스에서 응용 프로그램 toorun를 선택할 수 있습니다. 더 많은 처리 기능을 제공할 만 아니라, 어느 정도의 내결함성을 제공합니다. Hello 프로세스의 작동이 1 인스턴스에서 hello 다른 인스턴스는 여전히 계속 요청 처리 합니다.

Hello toobe 수동 또는 자동 크기 조정을 설정할 수 있습니다.

#### <a name="use-autoheal"></a>AutoHeal를 사용
AutoHeal (예: 구성 변경, 요청, 메모리 기반 제한 또는 hello 시간 tooexecute 요청 필요)를 선택 하는 설정에 따라 응용 프로그램에 대 한 hello 작업자 프로세스를 재활용 합니다. 대부분의 hello 재활용 hello 프로세스는 문제로 인해 hello 가장 빠른 방법은 toorecover 합니다. 경우에 항상 hello Azure 포털 내에서 직접 hello 웹 앱에서 다시 시작할 수 있습니다, AutoHeal 까 자동으로 드립니다. 웹 앱에 대 한 hello 루트 web.config에 몇 가지는 트리거를 추가 하면 toodo 됩니다. 참고는 이러한 설정이 작동 하는 hello 동일한 방식으로 된 경우에 응용 프로그램 하나.Net 합니다.

자세한 내용은 [Auto-Healing Azure Websites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)를 참조하세요.

#### <a name="restart-hello-web-app"></a>Hello 웹 앱을 다시 시작
이 일회성 문제에서 가장 간단한 방법은 toorecover hello 자주 발생 합니다. Hello에 [Azure 포털](https://portal.azure.com/), 웹 앱의 블레이드에서 hello 옵션 toostop 했거나 응용 프로그램을 다시 시작 합니다.

 ![응용 프로그램 toosolve HTTP 오류 502 잘못 된 게이트웨이 및 사용할 수 없는 503 서비스를 다시 시작](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

또한, Azure Powershell을 사용하여 웹앱을 관리할 수 있습니다. 자세한 내용은 [Azure 리소스 관리자에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

