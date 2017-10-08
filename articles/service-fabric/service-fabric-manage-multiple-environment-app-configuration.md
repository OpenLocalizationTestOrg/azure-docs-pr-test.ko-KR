---
title: "aaaManage 서비스 패브릭에서 여러 환경 | Microsoft Docs"
description: "서비스 패브릭 응용 프로그램에서 컴퓨터의 한 컴퓨터 toothousands 클러스터에서 실행할 수 있습니다. 일부 경우 tooconfigure 다르게 이러한 다양 한 환경에 대 한 응용 프로그램 원할 수 있습니다. 이 문서에서는 어떻게 환경당 toodefine 다른 응용 프로그램 매개 변수입니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>여러 환경에 대한 응용 프로그램 매개 변수 관리
하나의 toomany 수천 대의 컴퓨터에서에서 임의의 위치를 사용 하 여 Azure 서비스 패브릭 클러스터를 만들 수 있습니다. 응용 프로그램 이진 파일은이 다양 한 환경에서 수정 없이 실행할 수, 하는 동안 경우가 종종 있습니다 tooconfigure hello 응용 프로그램 다르게 hello에 배포 하는 컴퓨터 수에 따라.

간단한 예로 상태 비저장 서비스에 대해 `InstanceCount` 를 고려합니다. Azure에서 응용 프로그램을 실행 하는 경우 일반적으로 원하는 tooset "-1"이 매개 변수 toohello 특수 값입니다. 이 구성 서비스 hello 클러스터 (또는 배치 제약 조건을 설정 하는 경우 hello 노드 유형에 서 모든 노드)의 모든 노드에서 실행 되 고 있는지 확인 합니다. 그러나이 구성은 적합 하지 않은 단일 컴퓨터 클러스터에 대 한 동일한 hello에서 수신 하는 여러 프로세스를 가질 수 없으므로 단일 컴퓨터에서 끝점입니다. 일반적으로 설정 대신 `InstanceCount` 너무 "1".

## <a name="specifying-environment-specific-parameters"></a>환경 특정 매개 변수 지정
hello 솔루션 toothis 구성 문제는 매개 변수가 있는 기본 서비스 및 해당 매개 변수 값에 대 한 지정된 된 환경에서 작성 하는 응용 프로그램 매개 변수 파일의 집합입니다. 기본 서비스 및 응용 프로그램 매개 변수 서비스 매니페스트 및 hello 응용 프로그램에서 구성 됩니다. hello hello ServiceManifest.xml 및 ApplicationManifest.xml 파일에 대 한 스키마 정의 hello 서비스 패브릭 SDK와 함께 설치 및 도구 너무*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>기본 서비스
서비스 패브릭 응용 프로그램은 서비스 인스턴스의 컬렉션으로 이루어 집니다. Toocreate 빈 응용 프로그램에 대 한 불가능 하 고 다음 모든 서비스 인스턴스를 동적으로 만들, 대부분의 응용 프로그램에는 hello 응용 프로그램 인스턴스화될 때 항상 생성 해야 하는 핵심 서비스입니다. 이들은 참조 tooas "기본 서비스"입니다. Hello 응용 프로그램 매니페스트는 대괄호에 포함 된-환경 구성에 대 한 자리 표시자에 지정 됩니다.

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

각 명명 된 매개 변수는 hello hello 응용 프로그램 매니페스트의 hello 매개 변수 요소 내에서 정의 되어야 합니다.

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

hello DefaultValue 특성 hello 값 toobe hello는 보다 구체적인 매개 변수가 없는 경우 지정된 된 환경에 대 한 사용을 지정 합니다.

> [!NOTE]
> 모든 서비스 인스턴스 매개 변수가 환경 단위 구성에 적합하지는 않습니다. 위의 hello 예제 LowKey hello 및 hello 서비스의 파티션 구성표에 대 한 HighKey 값 hello 파티션 범위는 hello 환경이 아닌 hello 데이터 도메인의 함수 때문에 명시적으로 hello 서비스의 모든 인스턴스에 대해 정의 됩니다.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>환경 단위 서비스 구성 설정
hello [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md) 활성화 서비스는 런타임에 읽을 수 있는 사용자 지정 키-값 쌍을 포함 하는 tooinclude 구성 패키지 합니다. 이러한 설정의 hello 값 수를 지정 하 여도 환경으로 구분 하는 수는 `ConfigOverride` hello 응용 프로그램 매니페스트에서 합니다.

Hello에 대 한 hello Config\Settings.xml 파일의 설정에 따라 hello 있다고 가정 하 고 `Stateful1` 서비스:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
toooverride 특정 응용 프로그램/환경 쌍에 대 한이 값 만들기는 `ConfigOverride` hello 응용 프로그램 매니페스트에서 hello 서비스 매니페스트를 가져올 때.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
이 매개 변수는 위에 표시된 대로 환경에서 구성될 수 있습니다. Hello 응용 프로그램 매니페스트의 hello 매개 변수 섹션에서 선언 하 고 hello 응용 프로그램 매개 변수 파일에서 환경 관련 값을 지정 하 여이 수행할 수 있습니다.

> [!NOTE]
> Hello 경우 서비스 구성 설정의 세 위치는 hello 키 값을 설정할 수 있습니다: hello 서비스 구성 패키지, 응용 프로그램 매니페스트 hello 및 hello 응용 프로그램 매개 변수 파일입니다. 서비스 패브릭은 항상 hello 응용 프로그램 매개 변수 파일에서 먼저 지정 하는 경우, 다음 응용 프로그램 매니페스트를 hello 선택한 구성 패키지를 마지막으로 hello 합니다.
> 
> 

### <a name="setting-and-using-environment-variables"></a>환경 변수 설정 및 사용 
지정 하 고 및 hello ServiceManifest.xml 파일에서 환경 변수를 설정 하 고, 인스턴스별로에 hello ApplicationManifest.xml 파일에서이 재정의할 수 있습니다.
아래 hello 예제에서는 두 개의 환경 변수를 보여 줍니다. 설정 값을 가진 및 다른 hello 재정의 됩니다. Hello에 tooset 환경 변수 값 방식으로 구성 재정의에 사용 된 해당 이러한 동일한 응용 프로그램 매개 변수를 사용할 수 있습니다.

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
hello ApplicationManifest.xml, hello로 hello ServiceManifest의에서 참조 hello 코드 패키지에서에서 toooverride hello 환경 변수 `EnvironmentOverrides` 요소입니다.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 명명 된 인스턴스를 서비스 하는 hello 만들어지면 hello 환경 변수 코드에서 액세스할 수 있습니다. 예를 들어 C#에서 할 수 있는 hello 다음

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Service Fabric 환경 변수
Service Fabric에는 각 서비스 인스턴스에 대해 설정된 기본 제공 환경 변수가 있습니다. hello 전체 목록은 환경 변수는 아래 hello에 굵게 표시 된 hello 서비스에 사용 됩니다 하는 경우 hello 되 고 다른 서비스 패브릭 런타임에서 사용 합니다. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[YourServiceName]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

hello 코드 belows toolist 서비스 패브릭 환경 변수를 hello 하는 방법을 보여 줍니다.
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
hello 다음은 예제 호출 응용 프로그램 종류에 대 한 환경 변수의 `GuestExe.Application` 서비스 유형으로 호출 `FrontEndService` 로컬 개발 컴퓨터에서 실행 합니다.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>응용 프로그램 매개 변수 파일
hello 서비스 패브릭 응용 프로그램 프로젝트는 하나 이상의 응용 프로그램 매개 변수 파일을 포함할 수 있습니다. 각각의 hello hello 응용 프로그램 매니페스트에서 정의 된 hello 매개 변수에 대 한 특정 값을 정의 합니다.

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
기본적으로 새 응용 프로그램은 Local.1Node.xml, Local.5Node.xml 및 Cloud.xml라는 세 응용 프로그램 매개 변수 파일을 포함합니다.

![솔루션 탐색기에서 응용 프로그램 매개 변수 파일][app-parameters-solution-explorer]

toocreate 매개 변수 파일 단순히 복사 하 고 기존 붙여 하 고 새 이름을 지정 합니다.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>배포하는 동안 환경 단위 매개 변수 식별
배포 시 응용 프로그램과 함께 toochoose hello 적절 한 매개 변수 파일 tooapply가 필요 합니다. Visual Studio에서 hello 게시 대화 상자를 통해 또는 PowerShell을 통해 수행할 수 있습니다.

### <a name="deploy-from-visual-studio"></a>Visual Studio에서 배포
Visual Studio에서 응용 프로그램을 게시할 때 사용할 수 있는 매개 변수 파일의 hello 목록에서 선택할 수 있습니다.

![Hello 게시 대화 상자에서 매개 변수 파일 선택][publishdialog]

### <a name="deploy-from-powershell"></a>PowerShell에서 배포
hello `Deploy-FabricApplication.ps1` hello 응용 프로그램 프로젝트 템플릿을에 포함 된 PowerShell 스크립트를 매개 변수로 게시 프로필을 받아들이고 hello PublishProfile 참조 toohello 응용 프로그램 매개 변수 파일을 포함 합니다.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>다음 단계
이 항목에서 설명 하는 hello 핵심 개념 중 일부에 대해 자세히 toolearn 참조 hello [서비스 패브릭 기술 개요](service-fabric-technical-overview.md)합니다. Visual Studio에서 사용할 수 있는 다른 앱 관리 기능에 대한 정보는 [Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)를 참조하세요.

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
