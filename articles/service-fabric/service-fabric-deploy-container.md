---
title: "aaaService 패브릭 및 컨테이너를 배포 합니다. | Microsoft Docs"
description: "서비스 패브릭 및 hello 컨테이너 toodeploy 마이크로 서비스 응용 프로그램의 사용합니다. 이 문서는 컨테이너 및 어떻게 toodeploy Windows 컨테이너는 클러스터로을 이미지에 대 한 서비스 패브릭 제공 하는 hello 기능에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Windows 컨테이너 tooService 패브릭 배포
> [!div class="op_single_selector"]
> * [Windows 컨테이너 배포](service-fabric-deploy-container.md)
> * [Docker 컨테이너 배포](service-fabric-deploy-container-linux.md)
> 
> 

이 문서는 hello Windows 컨테이너에서 컨테이너 화 된 서비스를 만드는 과정을 안내 합니다.

Service Fabric에는 컨테이너 내에서 실행되는 마이크로 서비스로 구성된 응용 프로그램을 빌드하는 데 도움을 주는 몇 가지 기능이 있습니다. 

hello 기능 포함 됩니다.

* 컨테이너 이미지 배포 및 활성화
* 리소스 관리
* 리포지토리 인증
* 컨테이너 포트와 호스트 포트 간 매핑
* 컨테이너 간 검색 및 통신
* 기능 tooconfigure 환경 변수 설정

응용 프로그램에 포함 하는 컨테이너 화 된 서비스 toobe 패키징하는 경우 각 기능은 작동 방식을 살펴 보겠습니다.

## <a name="package-a-windows-container"></a>Windows 컨테이너 패키징
컨테이너를 압축할 때 선택할 수 있습니다 toouse Visual Studio 프로젝트 템플릿 또는 [hello 응용 프로그램 패키지를 수동으로 만들](#manually)합니다.  Visual Studio, hello 응용 프로그램 패키지 구조를 사용 하 고 매니페스트 파일을 만듭니다에서 hello 새 프로젝트 템플릿이 있습니다.

> [!TIP]
> hello 가장 쉬운 방법은 toopackage를 서비스에 기존 컨테이너 이미지는 Visual Studio toouse입니다.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Visual Studio toopackage 기존 컨테이너 이미지를 사용 하 여
Visual Studio는 서비스 패브릭 서비스 템플릿 toohelp을 컨테이너 tooa 서비스 패브릭 클러스터를 배포 합니다.

1. **파일** > **새 프로젝트**를 선택하여 Service Fabric 응용 프로그램을 만듭니다.
2. 선택 **게스트 컨테이너** hello 서비스 템플릿으로 합니다.
3. 선택 **이미지 이름** 저장소 컨테이너에서에서 hello 경로 toohello 이미지를 제공 합니다. 예를 들어 https://hub.docker.com에서 `myrepo/myimage:v1`입니다.
4. 서비스에 이름을 지정하고 **확인**을 클릭합니다.
5. 컨테이너 화 된 서비스 끝점 통신을 위해 필요로 한다면 hello 프로토콜, 포트 및 형식 toohello ServiceManifest.xml 파일 이제 추가할 수 있습니다. 예: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Hello를 제공 하 여 `UriScheme`, 서비스 패브릭 명명 서비스 검색 기능에 대 한 hello로 hello 컨테이너 끝점을 자동으로 등록 합니다. hello 포트 (에서처럼 앞 예제는 hello)를 고정 또는 동적으로 할당 수 있습니다. 포트를 지정 하지 (처럼 모든 서비스와 함께) hello 응용 프로그램 포트 범위에서 할당 동적으로 됩니다.
    또한 tooconfigure hello 컨테이너 toohost 포트 매핑을 지정 하 여 필요한는 `PortBinding` hello 응용 프로그램 매니페스트에서 정책입니다. 자세한 내용은 참조 [컨테이너 toohost 포트 매핑 구성](#Portsection)합니다.
6. 컨테이너에 리소스 관리가 필요할 경우 `ResourceGovernancePolicy`를 추가합니다.
8. 컨테이너와 개인 리포지토리에 tooauthenticate를 필요한 경우 다음 추가 `RepositoryCredentials`합니다.
7. 컨테이너 지원이 설정 된 Windows Server 2016 컴퓨터에서 실행 하는 경우에 hello 패키지를 사용 하 고 작업 toodeploy tooyour 로컬 클러스터를 게시할 수 있습니다. 
8. 준비가 되 면 원격 클러스터를 tooa hello 응용 프로그램을 게시 하거나 hello 솔루션 toosource 컨트롤에서 확인 수 있습니다. 

예를 들어, 체크 아웃 hello에 대 한 [GitHub에서 서비스 패브릭 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Windows Server 2016 클러스터 만들기
toodeploy 컨테이너 화 된 응용 프로그램 해야 toocreate 컨테이너를 지 원하는 Windows Server 2016을 실행 하는 클러스터를 사용 하도록 설정 합니다. 클러스터는 로컬로 실행되거나 Azure에서 Azure Resource Manager를 통해 배포될 수 있습니다. 

Azure 리소스 관리자를 사용 하는 클러스터 toodeploy 선택 hello **컨테이너와 Windows Server 2016** 이미지 Azure의 옵션입니다. Hello 문서 참조 [Azure 리소스 관리자를 사용 하 여 서비스 패브릭 클러스터를 만들](service-fabric-cluster-creation-via-arm.md)합니다. Azure 리소스 관리자 설정에 따라 hello를 사용 하는 것을 확인 합니다.

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Hello를 사용할 수도 있습니다 [5 노드 Azure 리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate 클러스터입니다. 또는 Service Fabric 및 Windows 컨테이너 사용에 대한 커뮤니티 [블로그 게시물](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html)을 참조하세요.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>수동으로 패키징하고 컨테이너 이미지 배포
수동으로 컨테이너 화 된 서비스를 패키지의 hello 프로세스 단계를 수행 하는 hello를 기반으로 합니다.

1. Hello 컨테이너 tooyour 리포지토리를 게시 합니다.
2. Hello 패키지 디렉터리 구조를 만듭니다.
3. Hello 서비스 매니페스트 파일을 편집 합니다.
4. Hello 응용 프로그램 매니페스트 파일을 편집 합니다.

## <a name="deploy-and-activate-a-container-image"></a>컨테이너 이미지 배포 및 활성화
서비스 패브릭 hello에 [응용 프로그램 모델](service-fabric-application-model.md), 컨테이너 되는 여러 서비스 복제본을 배치 하는 응용 프로그램 호스트를 나타냅니다. toodeploy hello 컨테이너 이미지의 put hello 이름, 컨테이너를 활성화 하 고는 `ContainerHost` hello 서비스 매니페스트의 요소입니다.

Hello 서비스 매니페스트에 추가 된 `ContainerHost` hello 진입점에 대 한 합니다. 그런 다음 세트 hello `ImageName` toobe hello 이름 hello 컨테이너 리포지토리 및 이미지입니다. hello 다음 부분 매니페스트가의 예가 나와 toodeploy hello 컨테이너 호출 하는 방법을 `myimage:v1` 라는 리포지토리에서 `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

선택적 명령 toorun hello 컨테이너에서 hello 시작 시 지정할 수 있습니다 `Commands` 요소입니다. 여러 명령의 경우 쉼표로 구분합니다. 

## <a name="understand-resource-governance"></a>리소스 관리 이해
리소스 관리는 hello 호스트에서 컨테이너 hello hello 리소스를 제한 하는 hello 컨테이너의 기능을 사용할 수 있습니다. hello `ResourceGovernancePolicy`, 서비스 코드 패키지에 대 한 사용 되는 toodeclare 리소스 제한을 hello 응용 프로그램 매니페스트에서 지정 합니다. 다음 리소스는 hello에 대 한 리소스 제한은 설정할 수 있습니다.

* 메모리
* MemorySwap
* CpuShares(CPU 상대적 가중치)
* MemoryReservationInMB  
* BlkioWeight(BlockIO 상대적 가중치)

> [!NOTE]
> IOP, 읽기/쓰기 BPS 등과 같은 특정 블록 IO 제한 지정에 대한 지원이 향후 릴리스에 예정되어 있습니다.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>리포지토리 인증
컨테이너 toodownload tooprovide 로그인 자격 증명 toohello 컨테이너 리포지토리를 할 수 있습니다. hello 로그인 자격 증명을 hello 응용 프로그램 매니페스트에 지정은 사용 되는 toospecify hello 로그인 정보, 또는 hello 이미지 리포지토리에서 hello 컨테이너 이미지를 다운로드 하기 위한 SSH 키입니다. hello 다음 예제에서는 호출 계정을 *TestUser* hello 암호를 일반 텍스트로 함께 (*하지* 권장):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Toohello 컴퓨터 배포 된 인증서를 사용 하 여 hello 암호를 암호화 하는 것이 좋습니다.

hello 다음 예제에서는 호출 계정을 *TestUser*이라는 인증서를 사용 하 여 hello 암호를 암호화 하는 경우, *MyCert*합니다. Hello를 사용할 수 있습니다 `Invoke-ServiceFabricEncryptText` hello 암호에 대 한 PowerShell 명령 toocreate hello 비밀 암호화 텍스트입니다. 자세한 내용은 hello 문서 참조 [서비스 패브릭 응용 프로그램의 암호 관리](service-fabric-application-secret-management.md)합니다.

hello toodecrypt hello 암호를 사용 하는 hello 인증서의 개인 키 대역의 메서드에서 배포 toohello 로컬 컴퓨터 여야 합니다. (Azure에서 이 메서드는 Azure Resource Manager입니다.) 그런 다음 서비스 패브릭 hello 서비스 패키지 toohello 컴퓨터를 배포 하면 hello 암호를 해독할 수 있습니다. Hello 계정 이름과 함께 hello 암호를 사용 하 여 다음 hello 컨테이너 리포지토리와 상호 인증할 수 있습니다.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a>컨테이너 toohost 포트 매핑 구성
지정 하 여 hello 컨테이너와 호스트 사용 되는 포트 toocommunicate를 구성할 수 있습니다는 `PortBinding` hello 응용 프로그램 매니페스트에서 합니다. hello 포트 바인딩 지도 hello 포트 toowhich hello 서비스는 hello 컨테이너 tooa 호스트의 포트에 hello 내 수신 대기 합니다.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>컨테이너 간 검색 및 통신 구성
Hello를 사용할 수 있습니다 `PortBinding` 요소 toomap hello 서비스 매니페스트의 컨테이너 포트 tooan 끝점입니다. 다음 예제는 hello에서 끝점 hello `Endpoint1` 8905 고정된 포트를 지정 합니다. 지정할 수도 있습니다 포트 하지 전혀 있습니다을 위해 hello 클러스터의 응용 프로그램 포트 범위에서 임의 포트를 선택한 경우.


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
Hello를 사용 하 여 끝점을 지정 하는 경우 `Endpoint` 게스트 컨테이너 서비스 패브릭의 hello 서비스 매니페스트에서 태그를에서 자동으로이 끝점 toohello 명명 서비스를 게시할 수 있습니다. Hello 클러스터에서 실행 되는 다른 서비스를 확인 하기 위한 hello REST 쿼리를 사용 하 여이 컨테이너를 검색할 따라서 수 있습니다.

Hello 명명 서비스를 등록 하면 수행할 수 있습니다 컨테이너-컨테이너 통신 내 컨테이너에서 hello를 사용 하 여 [역방향 프록시](service-fabric-reverseproxy.md)합니다. 통신은 hello 역방향 프록시 http 수신 포트 및 환경 변수로 toocommunicate 원하는 hello 서비스의 hello 이름을 제공 하 여 수행 됩니다. 자세한 내용은 hello 다음 섹션을 참조 하세요. 

## <a name="configure-and-set-environment-variables"></a>환경 변수 구성 및 설정
각 코드 패키지 서비스 매니페스트 hello에에서 대 한 환경 변수를 지정할 수 있습니다. 이 기능은 컨테이너 또는 프로세스 또는 게스트 실행 파일로 배포되는지 여부에 관계 없이 모든 서비스에 대해 사용할 수 있습니다. Hello 응용 프로그램에서 값 매니페스트 또는 응용 프로그램 매개 변수를 배포 하는 동안 지정 환경 변수를 재정의할 수 있습니다.

hello 다음 서비스 매니페스트 XML 조각 표시 방법의 예제 코드 패키지에 대 한 toospecify 환경 변수:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

이러한 환경 변수는 hello 응용 프로그램 매니페스트 수준에서 재정의할 수 있습니다.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Hello에 대 한 명시적 값을 지정 했기 hello 이전 예에서 `HttpGateway` 환경 변수 (19000), hello 값을 설정 하는 동안 `BackendServiceName` hello 통해 매개 변수 `[BackendSvc]` 응용 프로그램 매개 변수입니다. 이 설정을 통해 toospecify hello 값에 대 한 `BackendServiceName`hello 응용 프로그램을 배포 하 고 hello 매니페스트에 고정된 값이 없는 값입니다.

## <a name="configure-isolation-mode"></a>격리 모드 구성

Windows는 컨테이너 - 프로세스 및 Hyper-V에 대한 두 가지 격리 모드를 지원합니다.  Hello 프로세스 격리 모드에서 실행 되는 모든 hello 컨테이너 hello 호스트와 동일한 호스트 컴퓨터 공유 hello 커널을 hello 합니다. Hello Hyper-v 격리 모드에서 hello 커널 각 Hyper-v 컨테이너와 hello 컨테이너 호스트 간에 격리 됩니다. hello 격리 모드 hello에 지정 된 `ContainerHostPolicies` hello 응용 프로그램 매니페스트 파일의 태그입니다.  지정할 수 있는 hello 격리 모드는 `process`, `hyperv`, 및 `default`합니다. hello `default` 격리 모드 기본값 너무`process` Windows 서버에서 호스팅하고 너무 기본값`hyperv` Windows 10 호스트에서.  hello 다음 코드 조각에서는 hello 격리 모드 hello 응용 프로그램 매니페스트 파일에 지정 되는 방법을

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>응용 프로그램 및 서비스 매니페스트에 대한 전체 예제

예제 응용 프로그램 매니페스트는 다음을 따릅니다.

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

(Hello 응용 프로그램 매니페스트를 앞에 지정 된) 예제 서비스 매니페스트는 다음과 같습니다.

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>다음 단계
이제는 컨테이너 화 된 서비스를 배포한 자세히 배울 방법 toomanage 읽어 주기 [서비스 패브릭 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)합니다.

* [Service Fabric 및 컨테이너 개요](service-fabric-containers-overview.md)
* 예제는 [GitHub에서 Service Fabric 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)을 확인하세요.
