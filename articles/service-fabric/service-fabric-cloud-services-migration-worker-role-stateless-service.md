---
title: "Azure 클라우드 서비스 앱 toomicroservices aaaConvert | Microsoft Docs"
description: "클라우드 서비스 tooService 패브릭에서에서 작업자 역할 및 서비스 패브릭 상태 비저장 서비스 toohelp 마이그레이션할와이 가이드는 클라우드 서비스 웹을 비교 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Tooconverting 웹 및 작업자 역할 tooService 패브릭 상태 비저장 서비스를 안내 합니다.
이 문서에서는 설명 방법을 toomigrate 클라우드 서비스 웹 및 작업자 역할 tooService 패브릭 상태 비저장 서비스입니다. 이것은 클라우드 서비스 tooService 패브릭에서에서의 가장 간단한 마이그레이션 경로 hello 응용 프로그램 전체 아키텍처가 될 toostay 대략 hello 동일 합니다.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>클라우드 서비스 프로젝트 tooService 패브릭 응용 프로그램 프로젝트
 클라우드 서비스 프로젝트는 서비스 패브릭 응용 프로그램 프로젝트는 유사한 구조와 모두 나타내는 hello 배포 단위 응용 프로그램-즉, 구성 파일은 각각 정의할 hello 완료 된 패키지를 배포 된 toorun 응용 프로그램에 대 한 합니다. 클라우드 서비스 프로젝트는 하나 이상의 웹 또는 작업자 역할을 포함합니다. 유사하게 서비스 패브릭 응용 프로그램 프로젝트에는 하나 이상의 서비스가 포함되어 있습니다. 

hello 클래스 간의 차이점은 hello 클라우드 서비스 프로젝트 직접 hello VM 배포와 응용 프로그램 배포, VM 구성 설정이 포함 되어 있으므로 반면 hello 서비스 패브릭 응용 프로그램 프로젝트에만 배포 될 응용 프로그램 정의 서비스 패브릭 클러스터에서 기존 Vm의 tooa 집합입니다. 자체 hello 서비스 패브릭 클러스터 리소스 관리자 템플릿을 통해 또는 hello Azure 포털을 통해 및 여러 서비스 패브릭 응용 프로그램 수 tooit를 배포한 후에 배포 됩니다.

![서비스 패브릭 및 클라우드 서비스 프로젝트 비교][3]

## <a name="worker-role-toostateless-service"></a>작업자 역할 toostateless 서비스
개념적으로 작업자 역할은 hello 작업의 모든 인스턴스는 동일 하 고 요청 언제 든 지 라우트된 tooany 인스턴스가 될 수 있습니다 상태 비저장 워크 로드를 나타냅니다. 각 인스턴스가 예상된 tooremember hello에 대 한 이전 요청 되지 않습니다. Hello 워크 로드의 작동 상태에 외부 상태 저장소와 같은 Azure 테이블 저장소 또는 Azure 문서 DB에서 관리 하는 합니다. 서비스 패브릭에서 이러한 유형의 작업은 상태 비저장 서비스에 의해 표시됩니다. hello 가장 간단한 방법은 toomigrating 작업자 역할 tooService 패브릭 가능 하 여 작업자 역할 코드 tooa 상태 비저장 서비스를 변환 합니다.

![작업자 역할 tooStateless 서비스][4]

## <a name="web-role-toostateless-service"></a>웹 역할 toostateless 서비스
비슷한 tooWorker 역할, 웹 역할도 상태 비저장 작업 나타내며 하므로 개념적으로 너무 수 매핑된 tooa 서비스 패브릭 상태 비저장 서비스 합니다. 그러나 웹 역할과 달리 서비스 패브릭은 IIS를 지원하지 않습니다. toomigrate tooa 상태 비저장 서비스 웹 역할에서에서 웹 응용 프로그램 필요 최초의 이동 tooa 웹 프레임 워크를 자체 호스트 될 수 있습니다 및 IIS 또는 ASP.NET Core 1과 같은 System.Web에 종속 되지 않아야 합니다.

| **응용 프로그램** | **지원됨** | **마이그레이션 경로** |
| --- | --- | --- |
| ASP.NET 웹 양식 |아니요 |변환 tooASP.NET 핵심 1 MVC |
| ASP.NET MVC |마이그레이션 사용 |업그레이드 tooASP.NET 핵심 1 MVC |
| ASP.NET Web API |마이그레이션 사용 |자체 호스팅된 서버 또는 ASP.NET Core 1 사용 |
| ASP.NET Core 1 |예 |해당 없음 |

## <a name="entry-point-api-and-lifecycle"></a>진입점 API 및 수명 주기
작업자 역할 및 서비스 패브릭 서비스 API는 비슷한 진입점을 제공합니다. 

| **진입점** | **작업자 역할** | **서비스 패브릭 서비스** |
| --- | --- | --- |
| 처리 중 |`Run()` |`RunAsync()` |
| VM 시작 |`OnStart()` |해당 없음 |
| VM 중지 |`OnStop()` |해당 없음 |
| 클라이언트 요청에 대한 수신기 열기 |해당 없음 |<ul><li> 상태 비저장인 경우 `CreateServiceInstanceListener()`</li><li>상태 저장인 경우 `CreateServiceReplicaListener()`</li></ul> |

### <a name="worker-role"></a>작업자 역할
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>서비스 패브릭 상태 비저장 서비스
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

둘 다는 toobegin 처리 주 "실행" 재정을 가집니다. Service Fabric 서비스는 `Run`, `Start` 및 `Stop`을 단일 액세스 지점, `RunAsync`로 결합합니다. 서비스 작업 하는 경우 시작 해야 `RunAsync` 시작 되 고 해야 작동이 중지 hello `RunAsync` 메서드의 CancellationToken 신호를 받은 합니다. 

몇 가지 주요 차이점 hello 수명 주기 및 작업자 역할 및 서비스 패브릭 서비스의 수명이 있습니다.

* **수명 주기:** hello 가장 큰 차이점은 작업자 역할 VM은 해당 수명 주기는 동 점된 toohello hello VM의 시작 및 중지 시기에 대 한 이벤트를 포함 하는 VM을 합니다. 서비스 패브릭 서비스 주기가 hello VM 수명 주기 별개 이므로 관련 되지 않은 대로 hello VM 또는 컴퓨터를 시작 및 중지를 호스트 하는 경우에 대 한 이벤트 포함 되지 않습니다.
* **수명:** 경우 hello 작업자 역할 인스턴스를 재활용 합니다 `Run` 메서드 종료 됩니다. 그러나 hello `RunAsync` 서비스 패브릭 서비스에서 메서드 및 실행할 수 toocompletion hello 서비스 인스턴스를 유지 됩니다. 

서비스 패브릭은 클라이언트 요청을 수신 대기하는 서비스에 대한 선택적 통신 설정 진입점을 제공합니다. Hello RunAsync와 통신 진입점은 서비스 패브릭 서비스-서비스 수 선택 tooonly 수신 대기 tooclient 요청 또는 처리 루프 또는 둘 다에 실행-이 hello RunAsync 메서드는 허용 하지 않고 tooexit 때문에 옵션 재정의 클라이언트 요청에 대 한 toolisten를 계속할 수 없기 때문에 hello 서비스 인스턴스를 다시 시작 합니다.

## <a name="application-api-and-environment"></a>응용 프로그램 API 및 환경
hello 클라우드 서비스 환경 API 정보 및 다른 VM 역할 인스턴스에 대 한 정보 뿐만 아니라 현재 VM 인스턴스 hello에 대 한 기능을 제공합니다. 서비스 패브릭 tooits 런타임 관련 정보 및 hello 노드는 서비스에 대 한 정보에서 현재 실행 중인를 제공 합니다. 

| **환경 작업** | **클라우드 서비스** | **서비스 패브릭** |
| --- | --- | --- |
| 구성 설정 및 변경 알림 |`RoleEnvironment` |`CodePackageActivationContext` |
| 로컬 저장소 |`RoleEnvironment` |`CodePackageActivationContext` |
| 끝점 정보 |`RoleInstance` <ul><li>현재 인스턴스: `RoleEnvironment.CurrentRoleInstance`</li><li>다른 역할 및 인스턴스: `RoleEnvironment.Roles`</li> |<ul><li>현재 노드 주소의 경우 `NodeContext`</li><li>서비스 끝점 검색의 경우 `FabricClient` 및 `ServicePartitionResolver`</li> |
| 환경 에뮬레이션 |`RoleEnvironment.IsEmulated` |해당 없음 |
| 동시 변경 이벤트 |`RoleEnvironment` |해당 없음 |

## <a name="configuration-settings"></a>구성 설정
클라우드 서비스의 구성 설정 VM 역할에 대해 설정 되 고 tooall 해당 VM 역할 인스턴스를 적용 합니다. 이러한 설정은 ServiceConfiguration.*.cscfg 파일에서 설정된 키-값 쌍이며 RoleEnvironment를 통해 직접 액세스할 수 있습니다. 서비스 패브릭에서 설정이 적용 개별적으로 tooa VM 보다는 tooeach 서비스 tooeach 응용 프로그램 서비스 및 응용 프로그램을 여러 VM를 호스팅할 수 있습니다. 서비스는 세 가지 패키지로 구성됩니다.

* **코드:** hello 서비스 실행 파일, 이진 파일, Dll, 및 기타 파일에 포함 된 서비스가 필요한 toorun 합니다.
* **Config:** 서비스에 대한 모든 구성 파일 및 설정.
* **데이터:** hello 서비스와 연결 된 정적 데이터 파일.

이러한 각 패키지는 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다. API를 통해 비슷한 tooCloud 서비스를 구성 패키지를 프로그래밍 방식으로 액세스할 수 있습니다 및 이벤트는 사용할 수 있는 toonotify hello 서비스의 구성 패키지 변경 합니다. Settings.xml 파일 키-값 구성 및 프로그래밍 방식 액세스 비슷한 toohello 응용 프로그램 설정 섹션의 App.config 파일에 사용할 수 있습니다. 그러나 클라우드 서비스와는 달리 서비스 패브릭 config 패키지는 XML, JSON, YAML 또는 사용자 지정 이진 형식이든 모든 형식의 구성 파일을 포함할 수 있습니다. 

### <a name="accessing-configuration"></a>구성 액세스
#### <a name="cloud-services"></a>클라우드 서비스
ServiceConfiguration.*.cscfg의 구성 설정은 `RoleEnvironment`을(를) 통해 액세스할 수 있습니다. 이러한 설정은 hello에 전체적으로 사용 가능한 tooall 역할 인스턴스는 동일한 클라우드 서비스 배포 합니다.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>서비스 패브릭
각 서비스에는 자체 개별 구성 패키지가 있습니다. 클러스터의 모든 응용 프로그램에서 액세스할 수 있는 전역 구성 설정에 대한 기본 제공 메커니즘이 없습니다. 구성 패키지 내에서 서비스 패브릭 특수 Settings.xml 구성 파일을 사용할 때 가능한 응용 프로그램 수준 구성 설정을 지정 하기 hello 응용 프로그램 수준 Settings.xml에 값을 덮어쓸 수 있습니다.

구성 설정은 hello 서비스를 통해 각 서비스 인스턴스 내의 액세스 `CodePackageActivationContext`합니다.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>구성 업데이트 이벤트
#### <a name="cloud-services"></a>클라우드 서비스
hello `RoleEnvironment.Changed` 이벤트는 사용 되는 toonotify 변경 될 때 모든 역할 인스턴스가 구성 변경 등의 hello 환경에서 발생 합니다. 역할 인스턴스 재활용 하거나 작업자 프로세스를 다시 시작 하지 않고 사용된 tooconsume 구성 업데이트입니다.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>서비스 패브릭
각 hello 세 패키지 형식-코드, 구성, 및 데이터 액세스 서비스에는 패키지 업데이트, 추가 또는 제거 하는 경우 서비스 인스턴스를 알려 주는 이벤트가 있습니다. 서비스는 각 유형의 여러 패키지를 포함할 수 있습니다. 예를 들어 서비스에는 각각 개별적으로 버전이 지정되고 업그레이드 가능한 여러 config 패키지가 있을 수 있습니다. 

이러한 이벤트는 hello 서비스 인스턴스를 다시 시작 하지 않고 서비스 패키지에 사용할 수 있는 tooconsume 변경 합니다.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>시작 작업
시작 작업은 응용 프로그램이 시작되기 전에 수행되는 작업입니다. 시작 작업에는 상승 된 권한을 사용 하 여 일반적으로 사용 되는 toorun 설치 스크립트입니다. 클라우드 서비스와 서비스 패브릭은 시작 작업을 지원합니다. hello 주요 차이점은 해당 클라우드 서비스, 시작 작업은 동률된 tooa VM 역할 인스턴스는 속해 있기 때문에 서비스 패브릭 시작 작업 동률된 tooany 않은 동 점된 tooa 서비스입니다. 반면 특정 VM입니다.

| 클라우드 서비스 | 서비스 패브릭 |
| --- | --- | --- |
| 구성 위치 |ServiceDefinition.csdef |
| 권한 |"제한된" 또는 "상승된" |
| 시퀀싱 |"간단", "백그라운드", "포그라운드" |

### <a name="cloud-services"></a>Cloud Services
클라우드 서비스에서 시작 진입점은 ServiceDefinition.csdef에서 역할별로 구성됩니다. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>서비스 패브릭
서비스 패브릭에서 시작 진입점은 ServiceManifest.xml에서 서비스별로 구성됩니다.

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>개발 환경에 대한 정보
클라우드 서비스와 서비스 패브릭 및 통합 되어 Visual studio 프로젝트 템플릿 디버깅, 구성 및 둘 다를 로컬로 배포에 대 한 지원 및 tooAzure 합니다. 클라우드 서비스와 서비스 패브릭은 로컬 개발 런타임 환경도 제공합니다. hello 차이점은 hello 개발 런타임을 에뮬레이션 하는 클라우드 서비스 hello 실행 되는 Azure 환경, 서비스 패브릭 에뮬레이터를 사용 하지 않는-hello 전체 서비스 패브릭 런타임을 사용 하는 동안 합니다. hello 로컬 개발 컴퓨터에서 실행 되는 환경이 서비스 패브릭 hello 프로덕션 환경에서 실행 되는 동일한 환경입니다.

## <a name="next-steps"></a>다음 단계
서비스 패브릭 신뢰할 수 있는 서비스 및 클라우드 서비스 및 서비스 패브릭 응용 프로그램 아키텍처 toounderstand 서비스 패브릭 기능의 전체 hello tootake 활용을 설정 하는 방법 간의 근본적인 차이점 hello에 대 한 자세한 사용 되는 읽기입니다.

* [서비스 패브릭 신뢰할 수 있는 서비스 시작](service-fabric-reliable-services-quick-start.md)
* [클라우드 서비스 및 서비스 패브릭 간의 개념적 가이드 toohello 차이점](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
