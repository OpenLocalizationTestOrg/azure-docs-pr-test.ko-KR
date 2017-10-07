---
title: "aaaService linux에서 컨테이너를 배포 하 고 패브릭 | Microsoft Docs"
description: "서비스 패브릭 및 hello Linux 컨테이너 toodeploy 마이크로 서비스 응용 프로그램의 사용합니다. 이 문서에서는 서비스 패브릭 컨테이너와 어떻게 toodeploy Linux 컨테이너는 클러스터로을 이미지를 제공 하는 hello 기능 설명"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Linux 컨테이너 tooService 패브릭 배포
> [!div class="op_single_selector"]
> * [Windows 컨테이너 배포](service-fabric-deploy-container.md)
> * [Linux 컨테이너 배포](service-fabric-deploy-container-linux.md)
>
>

이 문서에서는 Linux의 Docker 컨테이너에서 컨테이너화된 서비스를 빌드하는 과정을 안내합니다.

Service Fabric에는 컨테이너화된 마이크로 서비스로 구성된 응용 프로그램을 빌드하는 데 도움을 주는 몇 가지 컨테이너 기능이 있습니다. 이를 컨테이너화된 서비스라고 합니다.

hello 기능에는 다음이 포함 됩니다.

* 컨테이너 이미지 배포 및 활성화
* 리소스 관리
* 리포지토리 인증
* 컨테이너 포트 toohost 포트 매핑
* 컨테이너 간 검색 및 통신
* 기능 tooconfigure 환경 변수 설정

## <a name="packaging-a-docker-container-with-yeoman"></a>yeoman과 함께 docker 컨테이너 패키징
Linux 컨테이너를 패키지할 때 선택할 수 있습니다 어느 toouse yeoman 서식 파일 또는 [hello 응용 프로그램 패키지를 수동으로 만들](#manually)합니다.

서비스 패브릭 응용 프로그램에는 각각 hello 응용 프로그램의 기능을 제공 하 여 특정 역할에 있는 하나 이상의 컨테이너를 포함할 수 있습니다. hello Linux에 대 한 서비스 패브릭 SDK에 포함 되어는 [Yeoman](http://yeoman.io/) 생성기를 쉽게 toocreate를 사용 하면 응용 프로그램 컨테이너 이미지를 추가 합니다. Yeoman toocreate 라는 단일 Docker 컨테이너와 응용 프로그램을 사용 하 여 보겠습니다 *SimpleContainerApp*합니다. 생성 된 hello 매니페스트 파일을 편집 하 여 더 많은 서비스를 나중에 추가할 수 있습니다.

## <a name="install-docker-on-your-development-box"></a>개발 상자에 Docker를 설치합니다.

실행된 hello 다음 Linux 개발 상자 tooinstall docker 명령 (OSX에서 hello vagrant 이미지를 사용 하는 경우 docker는 이미 설치 됨):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기
1. 터미널에서 `yo azuresfcontainer`을 입력합니다.
2. 응용 프로그램 이름을 지정합니다(예: mycontainerap).
3. DockerHub 리포지토리에서 hello 컨테이너 이미지에 대 한 hello URL을 제공 합니다. hello 이미지 매개 변수는 hello 폼 [리포지토리] / [이미지 이름]
4. Hello 이미지에는 작업-진입점이 정의 없는 경우 tooexplicitly 필요한 쉼표로 구분 된 hello 컨테이너를 시작 하 고 나면 실행은 유지 하는 hello 컨테이너 내 toorun 명령 집합이 포함 된 입력된 명령을 지정 합니다.

![컨테이너용 Service Fabric Yeoman 생성기][sf-yeoman]

## <a name="deploy-hello-application"></a>Hello 응용 프로그램 배포

### <a name="using-xplat-cli"></a>플랫폼 간 CLI 사용
Hello 응용 프로그램으로 빌드하고 나면 toohello 로컬 클러스터 hello Azure CLI를 사용 하 여 배포할 수 있습니다.

1. Toohello 로컬 서비스 패브릭 클러스터를 연결 합니다.

    ```bash
    azure servicefabric cluster connect
    ```

2. 사용 하 여 hello 제공 hello 템플릿 toocopy에 hello 응용 프로그램 패키지 toohello 클러스터 이미지 저장소, hello 응용 프로그램 형식 등록 hello 응용 프로그램의 인스턴스를 만들 스크립트를 설치 합니다.

    ```bash
    ./install.sh
    ```

3. 브라우저를 열고 http://localhost:19080/탐색기 (hello Vagrant를 사용 하 여 Mac OS X의 경우 VM의 개인 ip hello 바꾸기 localhost)에서 패브릭 탐색기 tooService 이동 합니다.
4. Hello 응용 프로그램 노드를 확장 하 고 응용 프로그램 종류에 대 한 항목 및 해당 형식의 첫 번째 인스턴스 hello에 대 한 다른 이제입니다.
5. Hello 제거 스크립트를 사용 하는 hello 템플릿 toodelete hello 응용 프로그램 인스턴스에 제공 된 및 hello 응용 프로그램 종류의 등록을 취소 합니다.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Azure CLI 2.0 사용

관리에 hello 참조 문서를 참조 하십시오.는 [Azure CLI 2.0 hello 응용 프로그램 수명 주기를 사용 하 여](service-fabric-application-lifecycle-azure-cli-2-0.md)합니다.

예제 응용 프로그램에 대 한 [GitHub에서 체크 아웃 hello 서비스 패브릭 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>더 많은 서비스 tooan 기존 응용 프로그램 추가

tooadd 다른 컨테이너 서비스를 사용 하 여 이미 만든 tooan 응용 프로그램 `yo`, hello 다음 단계를 수행 합니다.

1. Hello 기존 응용 프로그램의 toohello 루트 디렉터리를 변경 합니다.  예를 들어 `cd ~/YeomanSamples/MyApplication`경우 `MyApplication` 는 Yeoman에서 만든 hello 응용 프로그램입니다.
2. `yo azuresfcontainer:AddService` 실행

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

선택적 hello를 지정 하 여 명령 입력된을 제공할 수 있습니다 `Commands` hello 컨테이너 내 명령 toorun 쉼표로 구분 된 집합이 있는 요소입니다.

> [!NOTE]
> Hello 이미지에는 작업-진입점이 정의 없는 경우 tooexplicitly 필요한 내부 입력된 명령을 지정 `Commands` hello 컨테이너 이후에 실행은 유지 하는 hello 컨테이너 내 명령 toorun 쉼표로 구분 된 집합이 있는 요소 시작 합니다.

## <a name="understand-resource-governance"></a>리소스 관리 이해
리소스 관리는 hello 호스트에서 컨테이너 hello hello 리소스를 제한 하는 hello 컨테이너의 기능을 사용할 수 있습니다. hello `ResourceGovernancePolicy`, 서비스 코드 패키지에 대 한 사용 되는 toodeclare 리소스 제한을 hello 응용 프로그램 매니페스트에서 지정 합니다. 다음 리소스는 hello에 대 한 리소스 제한은 설정할 수 있습니다.

* 메모리
* MemorySwap
* CpuShares(CPU 상대적 가중치)
* MemoryReservationInMB  
* BlkioWeight(BlockIO 상대적 가중치)

> [!NOTE]
> 향후 릴리스에서는 IOP, 읽기/쓰기 BPS 등과 같은 특정 블록 IO 제한 지정에 대한 지원이 포함될 예정입니다.
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

## <a name="configure-container-port-to-host-port-mapping"></a>컨테이너 포트와 호스트 포트 간 매핑 구성
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
Hello를 사용 하 여 `PortBinding` 정책을 컨테이너 포트 tooan 매핑할 수 있습니다 `Endpoint` hello 서비스 매니페스트의 합니다. 끝점 hello `Endpoint1` (예: 포트 80) 고정된 포트를 지정할 수 있습니다. 지정할 수도 있습니다 포트 하지 전혀 있습니다을 위해 hello 클러스터의 응용 프로그램 포트 범위에서 임의 포트를 선택한 경우.

Hello를 사용 하 여 끝점을 지정 하는 경우 `Endpoint` 게스트 컨테이너 서비스 패브릭의 hello 서비스 매니페스트에서 태그를에서 자동으로이 끝점 toohello 명명 서비스를 게시할 수 있습니다. Hello 클러스터에서 실행 되는 다른 서비스를 확인 하기 위한 hello REST 쿼리를 사용 하 여이 컨테이너를 검색할 따라서 수 있습니다.

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

Hello 명명 서비스를 등록 하면 할 수 있는 쉽게 hello 코드에서이 컨테이너에 컨테이너 통신 내 컨테이너에서 hello를 사용 하 여 [역방향 프록시](service-fabric-reverseproxy.md)합니다. 통신은 hello 역방향 프록시 http 수신 포트 및 환경 변수로 toocommunicate 원하는 hello 서비스의 hello 이름을 제공 하 여 수행 됩니다. 자세한 내용은 hello 다음 섹션을 참조 하세요.

## <a name="configure-and-set-environment-variables"></a>환경 변수 구성 및 설정
각 코드 패키지 hello 서비스 매니페스트를 컨테이너에 배포 되는 서비스에 대 한 또는 프로세스/게스트 실행 파일로 배포 된 서비스에 대 한 모두에 대 한 환경 변수를 지정할 수 있습니다. 이러한 환경 변수 값 hello 응용 프로그램 매니페스트에서 구체적으로 재정의 하거나 응용 프로그램 매개 변수로 배포 중에 지정 합니다.

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
* [Hello Azure CLI를 사용 하 여 서비스 패브릭 클러스터와의 상호 작용](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>관련 문서

* [Service Fabric 및 Azure CLI 2.0 시작](service-fabric-azure-cli-2-0.md)
* [Service Fabric 및 XPlat CLI 시작](service-fabric-azure-cli.md)
