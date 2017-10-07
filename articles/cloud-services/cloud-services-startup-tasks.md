---
title: "Azure 클라우드 서비스의 시작 작업 aaaRun | Microsoft Docs"
description: "시작 작업을 통해 응용 프로그램에 대한 클라우드 서비스 환경을 준비합니다. 이 설명 하 고 시작 작업을 작업 하는 방법 toomake에"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>클라우드 서비스에 대 한 tooconfigure 및 실행 시작 작업 하는 방법
역할 시작 되기 전에 시작 작업 tooperform 작업을 사용할 수 있습니다. Tooperform 알았으므로 작업에는 구성 요소를 설치, COM 구성 요소를 등록, 레지스트리 키 설정 또는 장기 실행 프로세스 시작 포함 됩니다.

> [!NOTE]
> 시작 작업은 적용 가능한 tooVirtual 컴퓨터 tooCloud 서비스 웹 및 작업자 역할 수 없습니다.
> 
> 

## <a name="how-startup-tasks-work"></a>시작 작업 작동 방법
시작 작업은 역할을 시작 하 고 hello에 정의 되기 전에 수행 되는 동작은 [ServiceDefinition.csdef] hello를 사용 하 여 파일 [작업] hello 내의 요소 [시작]요소입니다. 시작 작업은 흔히 배치 파일이지만 PowerShell 스크립트를 시작하는 콘솔 응용 프로그램 또는 배치 파일일 수도 있습니다.

환경 변수는 시작 작업으로 정보를 전달 하 고 로컬 저장소는 시작 작업에서 사용 되는 toopass 정보 일 수 있습니다. 환경 변수 hello 경로 tooa 프로그램을 지정할 수는 예를 들어, tooinstall 원하고 파일 역할에서 다음 나중에 읽을 수 있는 toolocal 저장소를 작성할 수 있습니다.

시작 작업 로그 수 정보 및 hello로 지정 된 오류 toohello 디렉터리 **TEMP** 환경 변수입니다. Hello 시작 작업 중 hello **TEMP** 환경 변수 확인 toohello *c:\\리소스\\temp\\[guid]. [ rolename]\\RoleTemp* hello 클라우드에서 실행 중인 경우에 디렉터리입니다.

시작 작업은 재부팅 사이에 여러 번 실행할 수도 있습니다. 예를 들어 hello 시작 작업 hello 역할이 재활용 될 때마다 실행 되 고 역할 재활용에 재부팅이 포함 되지 않을 수 있습니다. 시작 작업을 여러 번 문제 없이 toorun 수 있도록 하는 방식으로 작성 되어야 합니다.

시작 작업으로 끝나야 합니다.는 **errorlevel** (또는 종료 코드) 시작 프로세스 toocomplete hello에 대 한 0입니다. 시작 작업이 0이 아닌로 끝나는지 **errorlevel**, hello 역할이 시작 되지 것입니다.

## <a name="role-startup-order"></a>역할 시작 순서
hello 다음 Azure의 hello 역할 시작 절차를 나열합니다.

1. hello 인스턴스가로 표시 되어 **시작** 트래픽을 받지 않습니다.
2. 모든 시작 작업이 tootheir에 따라 실행 됩니다 **taskType** 특성입니다.
   
   * hello **간단한** 작업이 동기적으로 실행 되는 한 번에 하나씩 있습니다.
   * hello **배경** 및 **전경** 작업은 비동기적으로 시작 됨, 병렬 toohello 시작 작업이 수행 됩니다.  
     
     > [!WARNING]
     > IIS 구성 되어 있지 않습니다 완전히 hello hello 시작 프로세스의 작업 단계를 시작 하는 동안 역할 관련 데이터를 사용할 수 있습니다. 역할 지정 데이터가 필요한 시작 작업은 [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)를 사용해야 합니다.
     > 
     > 
3. hello 역할 호스트 프로세스가 시작 되 고 hello 사이트가 IIS에서 만들어집니다.
4. hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 메서드를 호출 합니다.
5. hello 인스턴스가로 표시 되어 **준비** 트래픽이 라우트된 toohello 인스턴스입니다.
6. hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드를 호출 합니다.

## <a name="example-of-a-startup-task"></a>시작 작업의 예
시작 작업 hello에 정의 된 [ServiceDefinition.csdef] 파일 hello에 **작업** 요소입니다. hello **commandLine** 특성 hello 이름을 지정 하 고 hello 시작 배치의 매개 변수 파일 또는 콘솔 명령의 hello **executionContext** hello 권한 수준의 hello 시작을 지정 하는 특성 작업 및 hello **taskType** 특성 hello 작업은 실행 하는 방법을 지정 합니다.

이 예제에서는 환경 변수 **MyVersionNumber**hello 시작 작업에 대해 생성 되며 toohello 값 설정 "**1.0.0.0**"입니다.

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

다음 예제는 hello에서 hello **Startup.cmd** 배치 파일 줄에 기록한 hello toohello StartupLog.txt 파일 "hello 현재 버전이 1.0.0.0" hello TEMP 환경 변수로 지정 된 hello 디렉터리에 있습니다. hello `EXIT /B 0` 줄으로 끝나는 해당 hello 시작 작업을 사용 하면는 **errorlevel** 0입니다.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> Visual Studio에서 hello **tooOutput 디렉터리 복사** 시작 배치 파일에 대 한 속성은 너무**항상 복사** toobe 제대로 시작 배치 파일을 Azure에서 tooyour 프로젝트 배포 (**approot\\bin** 웹 역할에 대 한 및 **approot** 작업자 역할에 대 한).
> 
> 

## <a name="description-of-task-attributes"></a>작업 특성 설명
hello 다음 hello의 특성을 설명 hello **작업** hello 요소 [ServiceDefinition.csdef] 파일:

**commandLine** -hello hello 시작 작업에 대 한 명령줄을 지정 합니다.

* hello 명령으로 선택적인 명령줄 매개 변수를 가진 hello 시작 작업을 시작 합니다.
* 자주.cmd 또는.bat 배치 파일의 hello 파일 이름입니다.
* hello 작업은 상대 toohello AppRoot\\hello 배포에 대 한 Bin 폴더입니다. 환경 변수는 hello 경로 hello 작업의 파일을 결정 하는 확장 되지 않습니다. 환경 확장이 필요한 경우 시작 작업을 호출하는 작은 .cmd 스크립트를 만들 수 있습니다.
* 콘솔 응용 프로그램 또는 [PowerShell 스크립트](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task)를 시작하는 배치 파일일 수 있습니다.

**executionContext** -hello 시작 작업에 대 한 hello 권한 수준을 지정 합니다. hello 권한 수준은 제한 되거나 승격 될 수 있습니다.:

* **제한**  
  hello 시작 작업이 hello hello 역할과 동일한 권한으로 실행 합니다. Hello 때 **executionContext** hello에 대 한 특성 [런타임] 요소 이기도 **제한**, 사용자 권한이 사용 됩니다.
* **상승**  
  hello 시작 작업이 관리자 권한으로 실행 합니다. 이렇게 하면 시작 작업이 tooinstall 프로그램, IIS 구성을 변경, hello 역할 자체의 권한 수준을 hello을 늘리지 않고도 레지스트리 변경 및 기타 관리자 수준 작업을 수행 합니다.  

> [!NOTE]
> hello 시작 작업의 권한 수준을 않아도 toobe hello hello 역할 자체와 동일 합니다.
> 
> 

**taskType** -hello 시작 작업 방식으로 실행 되는지 지정 합니다.

* **간단한**  
  Hello에 지정 된 hello 순서로 한 번에 하나씩 작업이 동기적으로 실행 [ServiceDefinition.csdef] 파일입니다. 한 경우 **간단한** 시작 작업으로 끝나는 **errorlevel** 0을 hello 다음 **간단한** 시작 작업이 실행 되 합니다. 더 이상 없으면 **간단한** 시작 작업 tooexecute, 다음 hello 역할 자체가 시작 됩니다.   
  
  > [!NOTE]
  > 경우 hello **간단한** 작업이 0이 아닌 종료 **errorlevel**, hello 인스턴스가 차단 됩니다. 후속 **간단한** 시작 작업과 hello 역할 자체는 시작 되지 것입니다.
  > 
  > 
  
    배치 파일으로 끝나는 tooensure는 **errorlevel** 0을 hello 명령을 실행 `EXIT /B 0` 배치 파일 프로세스의 hello 끝에 합니다.
* **백그라운드**  
  작업은 hello 역할의 시작 hello와 병렬로 비동기적으로 실행 됩니다.
* **포그라운드**  
  작업은 hello 역할의 시작 hello와 병렬로 비동기적으로 실행 됩니다. 주요 차이점 hello는 **전경** 및 **배경** 하는 작업은 한 **전경** 작업 인해 hello 역할 재활용 또는 hello 작업에 포함 될 때까지 종료 되지 종료 되었습니다. hello **배경** 작업에 이러한 제한이 적용 되지 않습니다.

## <a name="environment-variables"></a>환경 변수
환경 변수는 방식으로 toopass 정보 tooa 시작 작업입니다. 예를 들어 프로그램 tooinstall를 포함 하는 hello 경로 tooa blob 또는 역할에서 사용할 포트 번호 또는 시작 작업의 toocontrol 기능 설정 넣을 수 있습니다.

두; 시작 작업에 대 한 환경 변수 hello의 멤버에 따라 정적 환경 변수 및 환경 변수 [ RoleEnvironment] 클래스입니다. 둘 다 hello에 [환경] hello 섹션 [ServiceDefinition.csdef] 파일과 모두 사용 하 여 hello [ 변수] 요소 및 **이름** 특성입니다.

정적 환경 변수 사용 하 여 hello **값** hello 특성 [ 변수] 요소입니다. 위의 hello 예제 hello 환경 변수를 만듭니다. **MyVersionNumber** 정적 값이 있는 "**1.0.0.0**"입니다. 또 다른 예로 toocreate 수는 **StagingOrProduction** 의 toovalues 수동으로 설정할 수 있는 환경 변수 "**준비**"또는"**프로덕션**" tooperform 다른 시작 작업의 hello hello 값에 따라 **StagingOrProduction** 환경 변수입니다.

Hello RoleEnvironment 클래스의 멤버를 기반으로 하는 환경 변수는 hello를 사용 하지 않는 **값** hello 특성 [ 변수] 요소입니다. 대신, hello [RoleInstanceValue] 자식 요소가 적절 한 hello로 **XPath** 특성 값을 사용 하는 toocreate hello의 특정 멤버에 따라 환경 변수는 [ RoleEnvironment] 클래스입니다. Hello에 대 한 값 **XPath** tooaccess 다양 한 특성 [ RoleEnvironment] 값을 찾을 수 [여기](cloud-services-role-config-xpath.md)합니다.

예를 들어 toocreate 않는 환경 변수 "**true**" hello 인스턴스가 hello 계산 에뮬레이터에서 실행 중일 때 및 "**false**" hello 클라우드를 실행할 때 사용 하 여 hello 다음 [ 변수] 및 [RoleInstanceValue] 요소:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>다음 단계
자세한 내용은 방법 tooperform 일부 [일반적인 시작 작업](cloud-services-startup-tasks-common.md) 클라우드 서비스와 합니다.

[포장합니다](cloud-services-model-and-package.md) .  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[작업]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[시작]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[런타임]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[환경]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[ 변수]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
