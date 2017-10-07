---
title: "클라우드 서비스 수명 주기 이벤트 aaaHandle | Microsoft Docs"
description: ".NET에서 클라우드 서비스 역할의 hello 수명 주기 메서드를 사용할 수 있는 방법을 알아봅니다"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Hello.NET에서 웹 또는 작업자 역할의 수명 주기를 사용자 지정
Hello를 확장 하는 작업자 역할을 만들 때 [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) toooverride 수 있는 사용자에 대 한 메서드를 제공 하는 클래스 toolifecycle 이벤트에 응답 합니다. 웹 역할에 대 한이 클래스는 선택 사항 이므로 toorespond toolifecycle 이벤트 사용 해야 합니다.

## <a name="extend-hello-roleentrypoint-class"></a>Hello RoleEntryPoint 클래스 확장
hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) 클래스 Azure에 의해 호출 된 메서드가 포함 됩니다 때 것 **시작**, **실행**, 또는 **중지** 웹 또는 작업자 역할입니다. 필요에 따라 이러한 방법 toomanage 역할 초기화, 역할 종료 시퀀스 또는 hello 역할의 hello 실행 스레드를 재정의할 수 있습니다. 

확장 하면 **RoleEntryPoint**, hello 메서드의 동작을 수행 하는 hello 알고 있어야 합니다.

* hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 및 [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 가능한 tooreturn 되기 때문 메서드는 부울 값을 반환 **false** 이러한 방법 중에서 합니다.
  
   코드를 반환 하는 경우 **false**, 갑자기 종료 된 hello 역할 프로세스, 종료 시퀀스가 실행 하지 않고 현재 위치에 있을 수 있습니다. 반환 되지 않도록 해야 일반적으로 **false** hello에서 **OnStart** 메서드.
* **RoleEntryPoint** 메서드의 오버 로드 내 확인할 수 없는 예외는 처리되지 않는 예외로 취급됩니다.
  
   Azure에서 hello hello 수명 주기 메서드 중 하나에서 예외가 발생 하는 경우 발생 [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) 이벤트를 다음 hello 프로세스가 종료 됩니다. 역할이 오프라인 상태가 되었거나, Azure에서 다시 시작할 수 있습니다. 처리 되지 않은 예외가 발생할 때 hello [중지](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) 이벤트 발생 하지 않은 및 hello **OnStop** 메서드가 호출 되지 않습니다.

역할이 시작 되지 않으면 또는 hello 초기화, 사용 중 및 중지 중 상태 사이 재활용 되는 경우 코드 각 시간 hello 역할이 다시 시작 하는 hello 수명 주기 이벤트 중 하나에서 처리 되지 않은 예외를 throw 할 수 있습니다. 이 경우 hello를 사용 하 여 [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) 이벤트 toodetermine hello hello 예외를 발생 하 고 적절 하 게 처리 합니다. 사용자의 역할 hello에서 반환 될 수도 있으며 [실행](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) hello 역할 toorestart 메서드에 합니다. 배포 상태에 대 한 자세한 내용은 참조 [일반적인 문제는 원인 역할 tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)합니다.

> [!NOTE]
> Hello를 사용 하는 경우 **Azure Tools for Microsoft Visual Studio** toodevelop 응용 프로그램 역할 프로젝트 템플릿은 hello hello 자동 확장 **RoleEntryPoint** 클래스를 hello에*WebRole.cs* 및 *WorkerRole.cs* 파일입니다.
> 
> 

## <a name="onstart-method"></a>Onstart 메서드
hello **OnStart** 역할 인스턴스가 Azure에서 온라인 상태가 되 면 메서드가 호출 됩니다. Hello 역할 인스턴스가로 표시 되어 hello OnStart 코드가 실행 되는 동안 **Busy** 외부 트래픽을 hello 부하 분산 장치에 의해 지정 된 tooit 됩니다. 이벤트 처리기를 구현 하 고 시작 등이 메서드 tooperform 초기화 작업을 재정의할 수 [Azure 진단](cloud-services-how-to-monitor.md)합니다.

경우 **OnStart** 반환 **true**, hello 인스턴스가 초기화 되 고 호출 하는 Azure hello **RoleEntryPoint.Run** 메서드. 경우 **OnStart** 반환 **false**, hello 역할 계획된 된 종료 시퀀스를 실행 하지 않고 즉시 종료 합니다.

코드 예제에서 보여 주는 방법을 다음 hello toooverride hello **OnStart** 메서드. 이 메서드를 구성 하 고 hello 역할 인스턴스가 시작 되 고 tooa 저장소 계정 데이터 로깅의 전송을 설정할 때 진단 모니터를 시작 합니다.

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>OnStop 메서드
hello **OnStop** 메서드 후 역할 인스턴스가 되었습니다에서 오프 라인 Azure hello 프로세스 종료 되기 전에 호출 됩니다. 이 메서드 toocall 코드를 종료 하 여 역할 인스턴스 toocleanly에 필요한 재정의할 수 있습니다.

> [!IMPORTANT]
> Hello에서 실행 되는 코드 **OnStop** 사용자가 시작한 종료 이외의 이유로 호출 될 때 메서드에 제한 된 시간 toofinish 합니다. 이 시간이 지난 후 hello 프로세스 종료 되므로 해야 하며 해당 코드 hello에 **OnStop** 메서드 신속 하 게 실행 하거나 실행 되지 않는 toocompletion 것을 허용 합니다. hello **OnStop** hello 후 메서드는 **중지** 이벤트가 발생 합니다.
> 
> 

## <a name="run-method"></a>Run 메서드
Hello를 재정의할 수 **실행** 메서드 tooimplement 역할 인스턴스에 대 한 장기 실행 스레드입니다.

Hello 재정의 **실행** 메서드는 필요 하지 않으면 hello 기본 구현은 영원히 중지 되는 스레드를 시작 합니다. Hello를 재정의 하는 경우 **실행** 메서드를 코드 무기한으로 차단 됩니다. 경우 hello **실행** hello 역할이 자동으로 정상적으로 재활용 됩니다; Azure 발생 하는 즉, 메서드가 반환 hello **중지** 이벤트 및 호출 hello **OnStop** 메서드 하므로 오프 라인 종료 시퀀스가 hello 역할 하기 전에 실행 될 수 있습니다.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>웹 역할에 대 한 hello ASP.NET 수명 주기 메서드 구현
또한 toothose hello가 제공 hello ASP.NET 수명 주기 메서드를 사용할 수 있습니다 **RoleEntryPoint** 클래스를 웹 역할에 대 한 toomanage 초기화 및 종료 시퀀스입니다. 이 기존 ASP.NET 응용 프로그램 tooAzure 이식 하는 경우 호환성을 위해 유용할 수 있습니다. hello ASP.NET 수명 주기 메서드는 hello 내에서 호출 **RoleEntryPoint** 메서드. hello **응용 프로그램\_시작** hello 후 메서드는 **RoleEntryPoint.OnStart** 메서드가 완료 된 합니다. hello **응용 프로그램\_끝** hello 전에 메서드가 호출 되 **RoleEntryPoint.OnStop** 메서드를 호출 합니다.

## <a name="next-steps"></a>다음 단계
너무 방법에 대해 알아봅니다[클라우드 서비스 패키지 만들기](cloud-services-model-and-package.md)합니다.

