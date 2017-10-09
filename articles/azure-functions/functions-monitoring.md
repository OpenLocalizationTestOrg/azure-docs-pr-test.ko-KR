---
title: "Azure 함수 aaaMonitoring | Microsoft Docs"
description: "자세한 내용은 방법 toomonitor Azure 함수입니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Azure Functions 모니터링

## <a name="overview"></a>개요 


hello **모니터** 탭에 각 기능을 통해 tooreview 있습니다 함수의 각 실행 합니다.

![Azure Functions 모니터 탭](./media/functions-monitoring/monitor-tab.png) 

실행을 클릭 하면 tooreview hello 기간, 입력된 데이터, 오류 및 관련된 로그 파일 수 있습니다. 이 탭은 함수를 디버그하고 성능을 조정하는 데 유용합니다.


> [!IMPORTANT]
> Hello를 사용 하는 경우 [호스팅 계획 소비](functions-overview.md#pricing) Azure 함수에 대 한 hello **모니터링** hello 함수 응용 프로그램 개요 블레이드에서 타일 모든 데이터가 표시 되지 것입니다. Hello 플랫폼에서 동적으로 확장 하 고 이러한 메트릭을 사용 계획에 적용 되므로, 계산 인스턴스를 관리 하는 때문입니다. 기능 앱 toomonitor hello 사용이 문서의 hello 지침을 대신 사용 해야 있습니다.
> 
> 다음 스크린 샷에서 hello 예를 보여 줍니다.
> 
> ![기본 리소스 블레이드 hello에 대 한 모니터링](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>실시간 모니터링

아래와 같이 **라이브 이벤트 스트림**을 클릭하면 실시간 모니터링을 사용할 수 있습니다. 

![라이브 hello 모니터 탭에 대 한 이벤트 스트림 옵션](./media/functions-monitoring/monitor-tab-live-event-stream.png)

아래와 같이 hello 라이브 이벤트 스트림 새 브라우저 탭에서 그래프로 나타낼 됩니다. 

![라이브 이벤트 스트림 예제](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> 입력 하 여 데이터 toofail toobe를 일으킬 수 있는 알려진된 문제가 있습니다. Tooclose hello 브라우저 탭 포함 hello 라이브 이벤트 스트림과 클릭이 발생 하면 할 수 있습니다 **라이브 이벤트 스트림** 다시 tooallow 것 tooproperly 이벤트 스트림 데이터를 채웁니다. 

hello 라이브 이벤트 스트림 hello 함수에 대 한 통계를 다음 그래프 됩니다.

* 초당 시작된 실행
* 초당 완료된 실행
* 초당 실패한 실행
* 평균 실행 시간(밀리초)

이 통계는 실시간 있지만 hello hello 실행 데이터의 그래프 실제 10 초 정도 대기 시간이 있을 수 있습니다.






## <a name="monitoring-log-files-from-a-command-line"></a>명령줄에서 로그 파일 모니터링


로그 파일 tooa 명령줄 세션 hello Azure 명령줄 인터페이스 (CLI) 또는 PowerShell을 사용 하 여 로컬 워크스테이션에서 스트리밍할 수 있습니다.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>함수 hello Azure CLI를 사용 하는 응용 프로그램 로그 파일 모니터링

시작 tooget [hello Azure CLI를 설치 합니다.](../cli-install-nodejs.md)

Hello 다음을 사용 하 여 Azure 계정에 로그인 명령 또는 중 하나를에서 설명 하는 다른 옵션 hello [hello Azure CLI에서에서 tooAzure 로그인](../xplat-cli-connect.md)합니다.

    azure login

사용 하 여 hello 다음 명령은 tooenable Azure CLI 서비스 관리 (ASM) 모드: 합니다.

    azure config mode asm

여러 구독이 있는 경우 구독 및 집합 hello 현재 구독 toohello 구독 함수 앱을 포함 하는 다음 명령을 toolist hello를 사용 합니다.

    azure account list
    azure account set <subscriptionNameOrId>

hello 다음 명령이 스트리밍되지 앱 toohello 함수 명령줄의 hello 로그 파일:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>PowerShell로 함수 앱 로그 파일 모니터링

시작 tooget [Azure PowerShell 설치 및 구성](/powershell/azure/overview)합니다.

Azure 계정 hello 다음 명령을 실행 하 여 추가 합니다.

    PS C:\> Add-AzureAccount

여러 구독이 있는 경우 목록으로 만들면 이름별으로 구독은 현재 선택 된 hello 올바른 hello 기반으로 하는 경우 명령 toosee 다음 hello로 `IsCurrent` 속성:

    PS C:\> Get-AzureSubscription

Tooset hello 활성 구독 toohello 함수 앱을 포함 해야 할 경우 다음 명령을 hello를 사용 합니다.

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

스트림 hello 다음 명령을 hello로 tooyour PowerShell 세션을 기록 합니다.

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

자세한 내용은 참조 너무[하는 방법: 웹 응용 프로그램에 대 한 로그 스트림](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs)합니다. 

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello 참조:

* [기능 테스트](functions-test-a-function.md)
* [기능 크기 조정](functions-scale.md)

