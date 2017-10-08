---
title: "Azure Service Fabric 컨테이너 응용 프로그램 aaaCreate | Microsoft Docs"
description: "Azure Service Fabric에서 첫 번째 Windows 컨테이너 응용 프로그램을 만듭니다.  Python 응용 프로그램과 함께 Docker 이미지를 작성, hello 이미지 tooa 컨테이너 레지스트리 푸시, 빌드 및 서비스 패브릭 컨테이너 응용 프로그램을 배포 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Windows에서 첫 번째 Service Fabric 컨테이너 응용 프로그램 만들기
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

서비스 패브릭 클러스터에서 Windows 컨테이너에서 기존 응용 프로그램을 실행 하면 모든 변경 내용을 tooyour 응용 프로그램이 필요 하지 않습니다. 이 문서에서는 Python을 포함 하는 Docker 이미지를 만드는 과정 [플라스](http://flask.pocoo.org/) 웹 응용 프로그램 및 tooa 서비스 패브릭 클러스터를 배포 합니다.  또한 [Azure Container Registry](/azure/container-registry/)를 통해 컨테이너화된 응용 프로그램을 공유할 수도 있습니다.  이 문서에서는 Docker에 대한 기본적으로 이해하고 있다고 가정합니다. 읽는 hello 하 여 Docker에 알아볼 수 있습니다 [Docker 개요](https://docs.docker.com/engine/understanding-docker/)합니다.

## <a name="prerequisites"></a>필수 조건
다음을 실행하는 개발 컴퓨터
* Visual Studio 2015 또는 Visual Studio 2017.
* [Service Fabric SDK 및 도구](service-fabric-get-started.md)
*  Windows용 Docker  [Windows용 Docker CE 가져오기(안정화)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) 설치 및 Docker 시작 hello 트레이 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **tooWindows 컨테이너 스위치**합니다. 이 Windows에 따라 필요한 toorun Docker 이미지입니다.

컨테이너를 사용하여 Windows Server 2016에서 실행되는 3개 이상의 노드가 있는 Windows 클러스터 - [클러스터를 만들](service-fabric-cluster-creation-via-portal.md)거나 [체험판으로 Service Fabric을 사용](https://aka.ms/tryservicefabric)하세요.

Azure Container Registry의 레지스트리 - Azure 구독 내에서 [컨테이너 레지스트리를 만듭니다](../container-registry/container-registry-get-started-portal.md).

## <a name="define-hello-docker-container"></a>Hello Docker 컨테이너를 정의 합니다.
Hello를 기반으로 이미지 빌드 [Python 이미지](https://hub.docker.com/_/python/) Docker 허브에 위치 합니다.

Dockerfile에서 Docker 컨테이너를 정의합니다. Dockerfile hello 컨테이너 내 hello 환경 설정 toorun, 원하는 hello 응용 프로그램을 로드 하 고 포트 매핑 하기 위한 지침이 포함 되어 있습니다. Dockerfile hello는 hello 입력된 toohello `docker build` 명령을 hello 이미지를 만듭니다.

빈 디렉터리를 만들고 hello 파일을 만들 *Dockerfile* (확장명이 없는 파일). Hello 너무 다음 추가*Dockerfile* 변경 내용을 저장 합니다.

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

읽기 hello [Dockerfile 참조](https://docs.docker.com/engine/reference/builder/) 자세한 정보에 대 한 합니다.

## <a name="create-a-simple-web-application"></a>간단한 웹 응용 프로그램 만들기
"Hello World!"를 반환하는 포트 80에서 수신 대기하는 Flask 웹 응용 프로그램을 만듭니다.  동일한 디렉터리 hello 하 hello 파일을 만들 *requirements.txt*합니다.  Hello 다음 추가 하 고 변경 내용을 저장 합니다.
```
Flask
```

Hello를 만들 수도 *app.py* 파일을 hello 다음 추가:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Hello 이미지 만들기
Hello 실행 `docker build` 웹 응용 프로그램을 실행 하는 명령 toocreate hello 이미지입니다. PowerShell 창을 열고 hello Dockerfile을 포함 하는 toohello 디렉터리를 이동 합니다. Hello 다음 명령을 실행 합니다.

```
docker build -t helloworldapp .
```

이 명령은 빌드 hello 프로그램 Dockerfile의 hello 지침을 사용 하 여 새 이미지 이름 지정 (-t 태그 지정) hello 이미지 "helloworldapp"입니다. 이미지 hello 기본 이미지를 Docker 허브에서 끌어와 빌드하고 hello 기본 이미지를 기반으로 응용 프로그램을 추가 하는 새 이미지를 만듭니다.  

Hello 빌드 명령이 완료 되 면 실행 hello `docker images` 명령 hello 새 이미지에 toosee 정보:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Hello 응용 프로그램을 로컬로 실행
로컬로 하기 전에 hello 컨테이너 레지스트리 이미지를 확인 합니다.  

Hello 응용 프로그램을 실행 합니다.

```
docker run -d --name my-web-site helloworldapp
```

*이름* (hello 컨테이너 ID)가 아닌 컨테이너를 실행 하는 이름을 toohello를 제공 합니다.

Hello 컨테이너 시작 되 면 브라우저에서 컨테이너를 실행 하는 tooyour 연결할 수 있도록 IP 주소를 찾기:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

컨테이너를 실행 하는 toohello를 연결 합니다.  Toohello 반환 된 IP 주소, 예를 들어 "http://172.31.194.61"를 가리키는 웹 브라우저를 엽니다. "Hello World!" 제목 hello를 나타나야 합니다. hello 브라우저에 표시 합니다.

toostop 컨테이너를 실행 합니다.

```
docker stop my-web-site
```

개발 컴퓨터에서 hello 컨테이너를 삭제 합니다.

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>푸시 hello 이미지 toohello 컨테이너 레지스트리
개발 컴퓨터에서 실행 되는 해당 hello 컨테이너를 확인 한 후 Azure 컨테이너 레지스트리에 hello 이미지 tooyour 레지스트리를 푸시하십시오.

실행 ``docker login`` 와 tooyour 컨테이너 레지스트리에 toolog 프로그램 [레지스트리 자격 증명](../container-registry/container-registry-authentication.md)합니다.

hello 다음 예제에서는 전달 hello ID와 Azure Active Directory의 암호 [서비스 사용자](../active-directory/active-directory-application-objects.md)합니다. 예를 들어 수 할당 했는지 자동화 시나리오에 대 한 서비스 주체 tooyour 레지스트리 합니다. 또는 레지스트리 사용자 이름과 암호를 사용하여 로그인할 수 있습니다.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

hello 다음 명령은 태그 또는 hello 이미지의 별칭으로 정규화 된 경로 tooyour 레지스트리 합니다. 이 예에서는 위치 hello hello에 이미지 ```samples``` hello 레지스트리 hello 루트 네임 스페이스 tooavoid 좀 더 합니다.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

푸시 hello 이미지 tooyour 컨테이너 레지스트리:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Visual Studio에서 컨테이너 화 된 hello 서비스 만들기
hello 서비스 패브릭 SDK 및 도구 제공 서비스 템플릿 toohelp 컨테이너 화 된 응용 프로그램을 만듭니다.

1. Visual Studio를 시작합니다.  **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
2. **Service Fabric 응용 프로그램**을 선택하고 "MyFirstContainer"라는 이름을 지정하고 **확인**을 클릭합니다.
3. 선택 **게스트 컨테이너** hello 목록에서 **서비스 템플릿은**합니다.
4. **이미지 이름** tooyour 컨테이너 리포지토리 푸시 hello 이미지 "myregistry.azurecr.io/samples/helloworldapp"를 입력 합니다.
5. 서비스에 이름을 지정하고 **확인**을 클릭합니다.

## <a name="configure-communication"></a>통신 구성
컨테이너 화 된 hello 서비스 통신을 위해 끝점을 필요합니다. 추가 `Endpoint` hello 프로토콜, 포트 및 형식 toohello ServiceManifest.xml 파일에 있는 요소입니다. 이 문서에 대 한 컨테이너 화 된 hello 서비스 포트 8081에서 수신합니다.  이 예제에서는 고정된 8081 포트가 사용됩니다.  지정 된 포트가 hello 응용 프로그램 포트 범위에서 임의 포트 선택 됩니다.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

서비스 패브릭 끝점을 정의 하 여 hello 끝점 toohello 명명 서비스를 게시 합니다.  Hello 클러스터에서 실행 중인 다른 서비스가이 컨테이너를 해결할 수 있습니다.  Hello를 사용 하 여 컨테이너-컨테이너 통신을 수행할 수 있습니다 [역방향 프록시](service-fabric-reverseproxy.md)합니다.  통신은 hello 역방향 프록시 HTTP 수신 포트 및 환경 변수로 toocommunicate 원하는 hello 서비스의 hello 이름을 제공 하 여 수행 됩니다.

## <a name="configure-and-set-environment-variables"></a>환경 변수 구성 및 설정
각 코드 패키지 서비스 매니페스트 hello에에서 대 한 환경 변수를 지정할 수 있습니다. 이 기능은 컨테이너 또는 프로세스 또는 게스트 실행 파일로 배포되는지 여부에 관계 없이 모든 서비스에 대해 사용할 수 있습니다. Hello 응용 프로그램에서 값 매니페스트 또는 응용 프로그램 매개 변수를 배포 하는 동안 지정 환경 변수를 재정의할 수 있습니다.

hello 다음 서비스 매니페스트 XML 조각 표시 방법의 예제 코드 패키지에 대 한 toospecify 환경 변수:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Hello 응용 프로그램 매니페스트에서 이러한 환경 변수를 재정의할 수 있습니다.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>컨테이너 포트-호스트 포트 매핑 및 컨테이너-컨테이너 검색 구성
Hello 컨테이너와 호스트 사용 되는 포트 toocommunicate를 구성 합니다. 포트 바인딩 hello hello 컨테이너 tooa 호스트의 포트에 hello 내 수신 하는 서비스는 hello에 hello 포트를 매핑합니다. 추가 `PortBinding` 요소 `ContainerHostPolicies` hello ApplicationManifest.xml 파일의 요소입니다.  이 문서에 대 한 `ContainerPort` 은 80 (hello 컨테이너에 지정 된 hello Dockerfile로 포트 80을 노출 하는 데 사용) 및 `EndpointRef` "Guest1TypeEndpoint"은 (hello hello 서비스 매니페스트에 이전에 정의 된 끝점).  포트 8081에서 toohello 서비스는 들어오는 요청 tooport 80 hello 컨테이너에 매핑됩니다.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>컨테이너 레지스트리 인증 구성
컨테이너 레지스트리 인증을 추가 하 여 구성 `RepositoryCredentials` 너무`ContainerHostPolicies` hello ApplicationManifest.xml 파일의 합니다. Hello 계정 및 암호 hello myregistry.azurecr.io 컨테이너 레지스트리에 hello 리포지토리에서 hello 서비스 toodownload hello 컨테이너 이미지를 추가 합니다.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Hello 클러스터의 tooall 노드에 배포 된 암호화 인증서를 사용 하 여 hello 저장소 암호를 암호화 하는 것이 좋습니다. 서비스 패브릭 hello 서비스 패키지 toohello 클러스터를 배포 하면 hello 암호화 인증서가 사용 되는 toodecrypt hello 암호화 텍스트입니다.  hello Invoke ServiceFabricEncryptText cmdlet은 toohello ApplicationManifest.xml 파일 추가 되는 hello 암호를 사용 하는 toocreate hello 암호화 텍스트입니다.

hello 다음 스크립트 새 자체 서명 된 인증서를 만들고 tooa PFX 파일을 내보냅니다.  hello 인증서는 기존 키 자격 증명 모음에 가져오는 되지 않으며 다음 toohello 서비스 패브릭 클러스터를 배포 합니다.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Hello를 사용 하 여 hello 암호 암호화 [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Hello 암호 hello에서 반환 된 hello 암호화 텍스트 대체 [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet 설정 `PasswordEncrypted` 너무 "true"입니다.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>격리 모드 구성
Windows는 컨테이너, 즉 프로세스 및 Hyper-V에 대한 두 가지 격리 모드를 지원합니다. Hello 프로세스 격리 모드에서 실행 되는 모든 hello 컨테이너 hello 호스트와 동일한 호스트 컴퓨터 공유 hello 커널을 hello 합니다. Hello Hyper-v 격리 모드에서 hello 커널 각 Hyper-v 컨테이너와 hello 컨테이너 호스트 간에 격리 됩니다. hello 격리 모드 hello에 지정 된 `ContainerHostPolicies` hello 응용 프로그램 매니페스트 파일의 요소입니다. 지정할 수 있는 hello 격리 모드는 `process`, `hyperv`, 및 `default`합니다. hello 기본 격리 모드 기본값 너무`process` Windows 서버에서 호스팅하고 너무 기본값`hyperv` Windows 10 호스트에서. hello 다음 코드 조각에서는 hello 격리 모드 hello 응용 프로그램 매니페스트 파일에 지정 되는 방법을

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>리소스 관리 구성
[리소스 관리](service-fabric-resource-governance.md) hello hello 호스트에서 컨테이너 hello 리소스를 사용할 수를 제한 합니다. hello `ResourceGovernancePolicy` hello 응용 프로그램 매니페스트에 지정 된 요소는 서비스 코드 패키지에 대 한 사용 되는 toodeclare 리소스 제한 합니다. 다음 리소스는 hello에 대 한 리소스 제한을 설정할 수 있습니다: 메모리, MemorySwap, CpuShares (CPU 상대적 가중치), MemoryReservationInMB, BlkioWeight (BlockIO 상대 가중치).  이 예제에서는 서비스 패키지 Guest1Pkg 위치로 hello 클러스터 노드에서 코어가 두 개를 가져옵니다.  메모리 한도 때문에 hello 코드 패키지는 제한 된 too1024 절대 MB의 메모리만 (및 동일 hello의 보증 소프트 예약). 코드 패키지 (컨테이너 또는 프로세스) toodo 시점과이 제한 보다 더 많은 메모리는 메모리 부족 예외가 발생 하는 수 tooallocate 않습니다. 리소스 제한 적용 toowork 서비스 패키지 내의 모든 코드 패키지에 지정 된 메모리 제한 해야 합니다.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Hello 컨테이너 응용 프로그램 배포
모든 변경 내용을 저장 하 고 hello 응용 프로그램을 빌드하십시오. toopublish 응용 프로그램을 마우스 오른쪽 단추로 클릭 **MyFirstContainer** 솔루션 탐색기에서 선택 **게시**합니다.

**연결 끝점**, hello 클러스터에 대 한 hello 관리 끝점을 입력 합니다.  예를 들어 "containercluster.westus2.cloudapp.azure.com:19000"이 있습니다. Hello 클라이언트 연결을 찾을 수 hello에서 클러스터에 대 한 hello 개요 블레이드에서 끝점 [Azure 포털](https://portal.azure.com)합니다.

**게시**를 클릭합니다.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 Service Fabric 클러스터에서 응용 프로그램 및 노드를 검사 및 관리하기 위한 웹 기반 도구입니다. 브라우저를 열고 탐색 toohttp://containercluster.westus2.cloudapp.azure.com:19080/탐색기/hello 응용 프로그램 배포를 수행 합니다.  hello 응용 프로그램을 배포 하지만 hello 이미지 (있음 hello 이미지 크기에 따라 몇 시간이 걸릴 수 있습니다) hello 클러스터 노드에 다운로드 될 때까지 작업이 오류 상태가: ![오류][1]

hello 응용 프로그램에 있을 때 가능 ```Ready``` 상태: ![준비][2]

브라우저를 열고 toohttp://containercluster.westus2.cloudapp.azure.com:8081 이동 합니다. "Hello World!" 제목 hello를 나타나야 합니다. hello 브라우저에 표시 합니다.

## <a name="clean-up"></a>정리
Hello 클러스터에서 실행 되는 동안 tooincur 요금이 계속, 고려 [클러스터 삭제](service-fabric-get-started-azure-cluster.md#remove-the-cluster)합니다.  [파티 클러스터](http://tryazureservicefabric.westus.cloudapp.azure.com/)는 몇 시간 후 자동으로 삭제됩니다.

Hello 이미지 toohello 컨테이너 레지스트리 강제 한 후에 개발 컴퓨터에서 hello 로컬 이미지를 삭제할 수 있습니다.

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Service Fabric 응용 프로그램 및 서비스 매니페스트의 전체 예제
Hello 완전 한 서비스 및 응용 프로그램 매니페스트가이 문서에 사용 되는 다음과 같습니다.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>컨테이너를 강제로 종료하기 전 시간 간격 구성

Hello 서비스 삭제 (또는 이동 tooanother 노드)이 시작 된 후 hello 컨테이너를 제거 하기 전에 hello 런타임 toowait에 대 한 시간 간격을 구성할 수 있습니다. 구성 hello 시간 간격 보냅니다 hello `docker stop <time in seconds>` 명령 toohello 컨테이너입니다.   자세한 내용은 [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)을 참조하세요. hello 시간 간격 toowait hello 아래에 지정 된 `Hosting` 섹션. 클러스터 매니페스트 조각 다음 hello tooset hello 간격을 대기 하는 방법을 보여 줍니다.

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
hello 기본 시간 간격을 설정 too10 초입니다. 이 구성은 동적 이므로 config hello 클러스터 업데이트 hello 제한 시간에만 업그레이드 합니다. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Hello 런타임 tooremove 구성 사용 하지 않는 컨테이너 이미지

서비스 패브릭 클러스터 tooremove hello를 구성할 수 있습니다 hello 노드에서 사용 하지 않는 컨테이너 이미지입니다. 이 구성은 너무 많은 컨테이너 이미지는 hello 노드에 지정할 경우 빼앗길 디스크 공간 toobe를 허용 합니다.  tooenable이 기능을 업데이트 hello `Hosting` hello 다음 코드 조각에에서 나와 있는 것 처럼 hello 클러스터 매니페스트 섹션: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

삭제 하지 않아야 하는 이미지에 대 한 리소스를 지정 하면 hello에서 `ContainerImagesToSkip` 매개 변수입니다. 



## <a name="next-steps"></a>다음 단계
* [Service Fabric의 컨테이너](service-fabric-containers-overview.md)를 실행하는 방법에 대해 자세히 알아봅니다.
* 읽기 hello [컨테이너에서.NET 응용 프로그램 배포](service-fabric-host-app-in-a-container.md) 자습서입니다.
* 서비스 패브릭 hello에 대 한 자세한 내용은 [응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)합니다.
* 체크 아웃 hello [서비스 패브릭 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers) GitHub에서 합니다.

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
