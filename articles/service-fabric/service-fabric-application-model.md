---
title: "서비스 패브릭 응용 프로그램 모델 aaaAzure | Microsoft Docs"
description: "어떻게 toomodel 및 응용 프로그램 및 서비스 패브릭에서 서비스에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>서비스 패브릭에서 응용 프로그램 모델링
이 문서에서는 hello Azure 서비스 패브릭 응용 프로그램 모델과 어떻게 toodefine 응용 프로그램 및 서비스를 통해 매니페스트 파일에 대 한 개요를 제공 합니다.

## <a name="understand-hello-application-model"></a>Hello 응용 프로그램 모델 이해
응용 프로그램은 특정 기능을 수행하는 구성 서비스 컬렉션입니다. 서비스는 완전한 독립 실행형 기능을 수행하며 다른 서비스와 독립적으로 시작할 수 있습니다.  서비스는 코드, 구성 및 데이터로 이루어집니다. 각 서비스에 대 한 코드 hello 실행 이진 이루어져, 구성은 런타임 시 로드할 수 있는 서비스 설정으로 구성 됩니다 및 데이터 hello 서비스에서 사용 하는 정적 데이터를 임의 toobe 구성 됩니다. 이 계층형 응용 프로그램 모델의 각 구성 요소를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.

![hello 서비스 패브릭 응용 프로그램 모델][appmodel-diagram]

응용 프로그램 유형은 응용 프로그램에 대한 분류이며 여러 서비스 유형으로 구성됩니다. 서비스 유형은 서비스에 대한 분류입니다. 다양 한 설정 및 구성의 경우, hello 분류 가질 수 있습니다 하지만 hello 핵심 기능은 상태로 유지 됩니다 hello 동일 합니다. hello의 인스턴스는 서비스는 hello 다른 서비스 구성 변형 hello의 동일 서비스 유형입니다.  

응용 프로그램 및 서비스의 클래스(또는 "형식")는 XML 파일(응용 프로그램 매니페스트 및 서비스 매니페스트)을 통해 설명됩니다.  hello 매니페스트는 대상 응용 프로그램에서에서 인스턴스화할 수 hello 클러스터 이미지 저장소 hello 템플릿입니다. hello hello ServiceManifest.xml 및 ApplicationManifest.xml 파일에 대 한 스키마 정의 hello 서비스 패브릭 SDK와 함께 설치 되 고 너무 도구*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

다른 응용 프로그램 인스턴스에 대 한 hello 코드가 별도 프로세스에서 호스팅되는 경우에 hello 동일한 서비스 패브릭 노드 대로 실행 합니다. 또한 (예: 업그레이드) 각 응용 프로그램 인스턴스의 hello 수명 주기를 관리할 수 있습니다 독립적으로 합니다. hello 다음 다이어그램 구성을 보여 줍니다 응용 프로그램 종류는 코드, 구성 및 데이터 패키지의 구성 되는 서비스 유형입니다. toosimplify hello 다이어그램에 대 한 hello 코드/config/데이터 패키지만 `ServiceType4` 각 서비스 유형에 포함 일부 또는 모든 패키지 유형의 경우에 표시 됩니다.

![서비스 패브릭 응용 프로그램 유형 및 서비스 유형][cluster-imagestore-apptypes]

서로 다른 두 매니페스트 파일은 사용 되는 toodescribe 응용 프로그램 및 서비스: 서비스 매니페스트 및 응용 프로그램 매니페스트 hello 합니다. 매니페스트는 hello 다음 섹션에서에서 자세히 설명 합니다.

인스턴스가 있을 수 있으며 하나 이상의 서비스 유형의 hello 클러스터의 활성 합니다. 예를 들어, 상태 저장 서비스 인스턴스 또는 복제본 hello 클러스터의 서로 다른 노드에 있는 복제본 간에 상태를 복제 하 여 높은 안정성을 유지 합니다. 기본적으로 복제는 클러스터의 한 노드가 실패 한 경우에 사용할 수 있는 hello 서비스 toobe에 대 한 중복성을 제공 합니다. A [서비스 분할](service-fabric-concepts-partitioning.md) 나눕니다 추가 hello 클러스터의 노드에서 해당 상태 (및 액세스 패턴 toothat 상태).

hello 다음 다이어그램에서는 응용 프로그램 및 서비스 인스턴스, 파티션 및 복제본 간의 hello 관계

![서비스 내의 파티션 및 복제본][cluster-application-instances]

> [!TIP]
> Http://에서 사용할 수 있는 hello 서비스 패브릭 탐색기 도구를 사용 하는 클러스터에서 응용 프로그램의 hello 레이아웃을 볼 수 있습니다&lt;yourclusteraddress&gt;: 19080/탐색기. 자세한 내용은 [Service Fabric Explorer를 사용하여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 참조하세요.
> 
> 

## <a name="describe-a-service"></a>서비스 설명
hello 서비스 매니페스트 hello 서비스 유형 및 버전을 선언적으로 정의합니다. 서비스 유형, 상태 속성, 부하 분산 메트릭, 서비스 바이너리, 구성 파일 등의 서비스 메타데이터를 지정합니다.  즉,이 패키지에 설명 hello 코드, 구성 및 데이터 서비스 패키지 toosupport를 구성 하는 서비스 유형을 하나 이상 있습니다. 다음은 서비스 매니페스트의 간단한 예입니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**버전** 특성은 구조화 되지 않은 문자열 및 hello 시스템에서 구문 분석 되지 않습니다. 버전 특성은 사용 되는 tooversion 업그레이드에 대 한 각 구성 요소입니다.

**ServiceTypes**는 이 매니페스트의 **CodePackages**에서 지원하는 서비스 유형을 선언합니다. 이러한 서비스 유형 중 하나에 대해 서비스가 인스턴스화되면 코드 패키지의 진입점을 실행하여 이 매니페스트에 선언된 모든 코드 패키지가 활성화됩니다. hello 결과 프로세스는 실행 시 예상된 tooregister 지원 hello 서비스 형식입니다. 서비스 형식은 코드 패키지 수준이 아닌 hello hello 매니페스트 수준에서 선언 됩니다. 따라서 여러 코드 패키지를 모두 활성화 되는 때마다 hello 시스템 hello 서비스 형식을 선언 중 하나를 찾습니다.

**SetupEntryPoint** hello 서비스 패브릭으로 동일한 자격 증명으로 실행 되는 권한 있는 요소입니다 (일반적으로 hello *LocalSystem* 계정) 다른 진입점 하기 전에. hello 실행 파일에서 지정한 **EntryPoint** hello 장기 실행 서비스 호스트는 일반적으로 합니다. 별도 설치 진입점의 hello 존재는 피할 수 높은 권한 가진 toorun hello 서비스 호스트 오랜 시간에 대 한 합니다. hello 실행 파일에서 지정한 **EntryPoint** 후 실행 **SetupEntryPoint** 정상적으로 종료 합니다. Hello 결과 프로세스를 모니터링 하 고 다시 시작 hello 프로세스는 현재까지 종료 또는 충돌, 하는 경우 (다시 부터는 **SetupEntryPoint**).  

사용에 대 한 일반적인 시나리오 **SetupEntryPoint** hello 서비스가 시작 되기 전에 실행 파일을 실행 하거나 관리자 권한으로 작업을 수행할 때 됩니다. 예:

* 설정 하 고 서비스의 실행 요구 hello 환경 변수를 초기화 합니다. 이것이 hello 서비스 패브릭 프로그래밍 모델을 통해 작성 된 제한 tooonly 실행 파일입니다. 예를 들어 npm.exe 파일에는 node.js 응용 프로그램 배포를 위해 구성되는 환경 변수가 필요합니다.
* 보안 인증서를 설치하여 액세스 제어를 설정합니다.

방법에 대 한 자세한 내용은 tooconfigure hello **SetupEntryPoint** 참조 [서비스 설치 시작 지점에 대 한 hello 정책 구성](service-fabric-application-runas-security.md)

**EnvironmentVariables**는 이 코드 패키지에 대해 설정된 환경 변수 목록을 제공합니다. Hello에서 Environmentment 변수를 재정의할 수 있습니다 `ApplicationManifest.xml` tooprovide 서로 다른 서비스 인스턴스에 대 한 다른 값입니다. 

**DataPackage** hello로 명명 된 폴더를 선언 **이름** 런타임 시 hello 프로세스로 사용 되는 임의의 정적 데이터 toobe 포함 된 특성입니다.

**됩니다** hello로 명명 된 폴더를 선언 **이름** 특성을 포함 하는 *Settings.xml* 파일입니다. hello 설정 파일 hello 프로세스 실행 시 다시 읽을 수 있는 사용자 정의 키-값 쌍 설정의 섹션을 포함 합니다. 경우에 업그레이드 하는 동안 hello **됩니다** **버전** 변경 된 후 프로세스를 실행 하는 hello 다시 시작 되지 않습니다. 대신, 콜백을 hello 프로세스를 동적으로 로드 될 수 있도록 구성 설정이 변경 되었음을 알립니다. 다음은 *Settings.xml* 파일의 예입니다.

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> 서비스 매니페스트는 여러 코드, 구성 및 데이터 패키지를 포함할 수 있습니다. 이들 항목에 대해 각각 독립적으로 버전을 지정할 수 있습니다.
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>응용 프로그램 설명
hello 응용 프로그램 매니페스트는 hello 응용 프로그램 유형 및 버전에 선언적으로 설명합니다. 안정적인 이름, 파티션 구성표, 인스턴스 수/복제 요소, 보안/격리 정책, 배치 제약 조건, 구성 재정의, 구성 서비스 유형 등의 서비스 구성 메타데이터를 지정합니다. hello 응용 프로그램으로 이동 하는 hello 부하 분산 도메인도 설명 되어 있습니다.

따라서 응용 프로그램 매니페스트 hello 응용 프로그램 수준에서 요소를 설명 하 고 하나를 참조 하거나 더 많은 서비스 매니페스트 toocompose 응용 프로그램의 종류입니다. 다음은 응용 프로그램 매니페스트의 간단한 예입니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

서비스 매니페스트를 같은 **버전** 특성은 구조화 되지 않은 문자열 및 hello 시스템에서 구문 분석 되지 않은 합니다. 버전 특성은 또한 tooversion 사용 되는 업그레이드에 대 한 각 구성 요소입니다.

**ServiceManifestImport** 이 응용 프로그램 종류를 구성 하는 참조 tooservice 매니페스트를 포함 합니다. 가져온 서비스 매니페스트는 이 응용 프로그램 유형 내에서 유효한 있는 서비스 유형을 결정합니다. 내 ServiceManifestImport hello ServiceManifest.xml 파일에서 Settings.xml 및 환경 변수에서 구성 값 재정의합니다. 


**DefaultServices** 는 이 응용 프로그램 유형에 대해 응용 프로그램이 인스턴스화할 때마다 자동으로 생성되는 서비스 인스턴스를 선언합니다. 기본 서비스는 편리하기는 하지만 생성된 후 모든 면에서 일반 서비스처럼 동작합니다. hello 응용 프로그램 인스턴스에 있는 다른 서비스와 함께 업그레이드 되 고도 제거 됩니다.

> [!NOTE]
> 응용 프로그램 매니페스트는 여러 서비스 매니페스트 가져오기 및 기본 서비스를 포함할 수 있습니다. 각 서비스 매니페스트 가져오기를 독립적으로 버전 지정할 수 있습니다.
> 
> 

toomaintain 다른 응용 프로그램 및 개별 환경에 대 한 서비스 매개 변수를 확인 하려면 어떻게 toolearn [여러 환경에 대 한 응용 프로그램 매개 변수 관리](service-fabric-manage-multiple-environment-app-configuration.md)합니다.

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>다음 단계
[응용 프로그램 패키지](service-fabric-package-apps.md) toodeploy 준비 된 것을 확인 합니다.

[배포 및 응용 프로그램을 제거할] [ 10] 설명 방법을 toouse PowerShell toomanage 응용 프로그램 인스턴스.

[여러 환경에 대 한 응용 프로그램 매개 변수 관리] [ 11] 설명 방법을 tooconfigure 매개 변수 및 다른 응용 프로그램 인스턴스에 대 한 환경 변수입니다.

[응용 프로그램에 대 한 보안 정책을 구성] [ 12] toorun 보안 정책 toorestrict 액세스에서 서비스 하는 방법에 대해 설명 합니다.

[응용 프로그램 호스팅 모델][13]에서는 배포된 서비스 및 서비스 호스트 프로세스 복제본(또는 인스턴스) 간의 관계에 대해 설명합니다.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
