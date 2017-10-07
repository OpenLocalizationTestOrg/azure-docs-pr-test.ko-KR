---
title: "aaaWhat은 클라우드 서비스 모델 및 패키지 | Microsoft Docs"
description: "Hello 클라우드 서비스 모델 (.csdef,.cscfg) 및 Azure에서 패키지 (.cspkg) 설명"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Hello 클라우드 서비스 모델의 정의 및 패키지 하는 방법
세 가지 구성 요소, hello 서비스 정의에서 클라우드 서비스가 만들어질 *(.csdef)*, 서비스 구성 hello *(.cscfg)*, 및 서비스 패키지 *(.cspkg)*합니다. 두 hello **ServiceDefinition.csdef** 및 **ServiceConfig.cscfg** XML 기반 파일과 hello 모델을 전체적으로 이라는 hello 클라우드 서비스 및 구성 된 방식; hello 구조를 설명 합니다. hello **ServicePackage.cspkg** hello에에서 생성 되는 zip 파일은 **ServiceDefinition.csdef** 특히, 모든 필요한 hello 이진 기반 종속성을 포함 합니다. Azure 클라우드 서비스를 모두 hello에서 만듭니다 **ServicePackage.cspkg** 및 hello **ServiceConfig.cscfg**합니다.

Azure의 hello 클라우드 서비스를 실행 하 고 hello를 통해 구성할 수 있습니다 **ServiceConfig.cscfg** 파일인 있지만 hello 정의 변경할 수 없습니다.

## <a name="what-would-you-like-tooknow-more-about"></a>원하는 방법에 대 한 자세한 tooknow?
* Hello에 대 한 자세한 tooknow 원하는 [ServiceDefinition.csdef](#csdef) 및 [ServiceConfig.cscfg](#cscfg) 파일입니다.
* 이미 내용을 알고 있으므로 무엇을 구성할 수 있는지에 대한 [몇 가지 예](#next-steps) 를 보여 주세요.
* Toocreate hello 원하는 [ServicePackage.cspkg](#cspkg)합니다.
* Visual Studio를 사용하여 다음 작업을 수행하려고 합니다.
  * [클라우드 서비스 만들기][vs_create]
  * [기존 클라우드 서비스 재구성][vs_reconfigure]
  * [클라우드 서비스 프로젝트 배포][vs_deploy]
  * [원격 데스크톱에서 클라우드 서비스 인스턴스에 연결][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
hello **ServiceDefinition.csdef** 파일 Azure tooconfigure에서 사용 되는 hello 설정을 지정 하는 클라우드 서비스입니다. hello [Azure Service 정의 스키마 (.csdef 파일)](https://msdn.microsoft.com/library/azure/ee758711.aspx) 서비스 정의 파일에 대 한 hello 허용 되는 형식을 제공 합니다. hello 다음 예제는 hello 웹 및 작업자 역할에 대해 정의할 수 있는 hello 설정.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

그러나 Toohello 참조할 수 있습니다 [서비스 정의 스키마](https://msdn.microsoft.com/library/azure/ee758711.aspx) 이해 여기에 hello XML 스키마의, 다음은 hello 요소 중 일부에 대해 간략하게 설명 합니다.

**Sites**  
I i s 7에서 호스팅되는 웹 사이트 또는 웹 응용 프로그램에 대 한 hello 정의 포함 합니다.

**InputEndpoints**  
포함 된 끝점에 대 한 hello 정의 toocontact hello 클라우드 서비스를 사용 합니다.

**InternalEndpoints**  
역할 인스턴스 toocommunicate 서로 사용 되는 끝점에 대 한 hello 정의 포함 합니다.

**ConfigurationSettings**  
특정 역할의 기능에 대 한 hello 설정 정의 포함합니다.

**인증서**  
역할에 필요한 인증서에 대 한 hello 정의 포함 합니다. hello 이전 코드 예제에서는 Azure Connect의 hello 구성에 사용 되는 인증서를 보여 줍니다.

**LocalResources**  
로컬 저장소 리소스에 대 한 hello 정의 포함합니다. 로컬 저장소 리소스에는 역할 인스턴스가 실행 되 고 있는 hello 가상 컴퓨터의 hello 파일 시스템에 예약 된 디렉터리입니다.

**Imports**  
가져온된 모듈에 대 한 hello 정의 포함합니다. hello 이전 코드 예제에서는 원격 데스크톱 연결 및 Azure Connect에 대 한 hello 모듈을 표시 합니다.

**시작**  
Hello 역할이 시작 될 때 실행 되는 작업이 포함 되어 있습니다. hello 작업은.cmd 또는 실행 파일에서 정의 됩니다.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
클라우드 서비스에 대 한 hello 설정의 hello 구성 hello에 hello 값으로 결정 **ServiceConfiguration.cscfg** 파일입니다. 이 파일에 각 역할에 대 한 toodeploy 되도록 인스턴스의 hello 수를 지정 합니다. hello 서비스 정의 파일에 정의 된 hello 구성 설정에 대 한 hello 값 toohello 서비스 구성 파일에 추가 됩니다. hello 클라우드 서비스와 관련 된 모든 관리 인증서 지문 안녕하세요 toohello 파일도 추가 됩니다. hello [Azure 서비스 구성 스키마 (.cscfg 파일)](https://msdn.microsoft.com/library/azure/ee758710.aspx) 서비스 구성 파일에 대 한 hello 허용 되는 형식을 제공 합니다.

hello 서비스 구성 파일 hello 응용 프로그램과 함께 패키지 되지 않습니다 되지만 별도 파일로 업로드 tooAzure 이며 사용된 tooconfigure hello 클라우드 서비스입니다. 클라우드 서비스를 다시 배포하지 않고 새 서비스 구성 파일을 업로드할 수 있습니다. hello 클라우드 서비스가 실행 중인 동안에 hello 클라우드 서비스에 대 한 hello 구성 값을 변경할 수 있습니다. hello 다음 예제는 hello 웹 및 작업자 역할에 대해 정의할 수 있는 hello 구성 설정.

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Toohello 참조할 수 있습니다 [서비스 구성 스키마](https://msdn.microsoft.com/library/azure/ee758710.aspx) 스키마에 대해 더 나은 이해 hello XML 여기에 여기 인데 hello 요소에 대해 간략하게 설명 합니다.

**인스턴스**  
실행 중인 인스턴스 hello 역할에 대 한 hello 수를 구성 합니다. 클라우드 서비스에서 업그레이드 하는 동안 잠재적으로 사용 하지 못하게 될 tooprevent, 웹 역할의 인스턴스가 둘 이상 배포 하는 것이 좋습니다. Toohello 지침 hello에 둘 이상의 인스턴스를 배포 하 여 준수할 [Azure 계산 서비스 수준 계약 (SLA)](http://azure.microsoft.com/support/legal/sla/), 두 개의 인터넷 연결 역할에 대 한 99.95% 외부 연결성을 보장 하 또는 더 많은 역할 인스턴스는 서비스에 대 한 배포 됩니다.

**ConfigurationSettings**  
역할의 인스턴스를 실행 하는 hello에 대 한 hello 설정을 구성 합니다. hello의 hello 이름 `<Setting>` 요소 hello 서비스 정의 파일의 hello 설정 정의와 일치 해야 합니다.

**인증서**  
Hello 서비스에서 사용 되는 hello 인증서를 구성 합니다. 이전 코드 예제에서는 hello toodefine hello RemoteAccess 모듈에 대 한 인증서를 hello 하는 방법을 보여 줍니다. 값의 hello hello *지문* 특성 hello 인증서 toouse의 toohello 지문을 설정 해야 합니다.

<p/>

> [!NOTE]
> hello 인증서 지문은 hello 텍스트 편집기를 사용 하 여 구성 파일 toohello 추가할 수 있습니다. Hello 값 hello에 추가할 수 있습니다 또는 **인증서** hello 탭 **속성** hello 역할 Visual Studio에서의 페이지입니다.
> 
> 

## <a name="defining-ports-for-role-instances"></a>역할 인스턴스에 대한 포트 정의
Azure 항목 지점 tooa 웹 역할 하나만 허용 됩니다. 하나의 IP 주소를 통해 모든 트래픽이 발생한다는 의미입니다. Hello 호스트 헤더 toodirect hello 요청 toohello 올바른 위치를 구성 하 여 사용자 웹 사이트 tooshare 포트를 구성할 수 있습니다. 또한 hello IP 주소에서 프로그램 응용 프로그램 toolisten toowell 알려진 포트를 구성할 수 있습니다.

hello 다음 샘플 hello 구성을 표시를 웹 사이트와 웹 응용 프로그램과 웹 역할에 대 한 합니다. hello 사이트가 포트 80에서 기본 진입 위치로 hello로 구성 하 고 hello 웹 응용 프로그램은 "mail.mysite.cloudapp.net" 이라고 하는 대체 호스트 헤더에서 구성 된 tooreceive 요청 합니다.

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>역할의 hello 구성 변경
Hello 서비스를 오프 라인 상태로 전환 하지 않고 Azure에서 실행 되는 동안 클라우드 서비스의 hello 구성을 업데이트할 수 있습니다. toochange 구성 정보를 업로드 하거나 새 구성 파일 또는 편집 hello 구성 파일에 배치 하 고 서비스를 실행 하는 tooyour 적용 합니다. hello 다음 변경할 수 있습니다는 서비스의 toohello 구성:

* **구성 설정의 hello 값 변경**  
  구성 설정 변경 사항을, 역할 인스턴스 수 선택 toorecycle hello 인스턴스 tooapply hello 변경 hello 인스턴스가 온라인 상태일 때 또는 정상적으로 하 고 hello 인스턴스가 오프 라인 상태일 때 hello 변경 내용을 적용 합니다.
* **역할 인스턴스의 서비스 토폴로지 hello 변경**  
  인스턴스가 제거되는 경우를 제외하고 토폴로지 변경은 실행 중인 인스턴스에 영향을 주지 않습니다. 모든 나머지 인스턴스 일반적으로 불필요 toobe 재활용; 그러나 선택할 수 있습니다 toorecycle 역할 인스턴스가 응답 tooa 토폴로지 변경.
* **Hello 인증서 지문을 변경**  
  역할 인스턴스가 오프라인인 상태에서는 인증서만 업데이트할 수 있습니다. 인증서를 추가, 삭제 또는 역할 인스턴스가 온라인 상태일 때 변경 된 경우 Azure 정상적으로 hello 인스턴스가 오프 라인 tooupdate hello 인증서 가져오고 온라인 상태로 전환 다시 hello 변경을 완료 한 후 합니다.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>서비스 런타임 이벤트를 사용하여 구성 변경 사항 처리
hello [Azure 런타임 라이브러리](https://msdn.microsoft.com/library/azure/mt419365.aspx) hello 포함 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) hello로 역할에서 Azure 환경과 상호 작용 하기 위한 클래스를 제공 하는 네임 스페이스입니다. hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) hello 다음 구성 변경 전후 발생 하는 이벤트 클래스를 정의 합니다.

* **[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) 이벤트**  
  Hello 구성 변경이 적용 된 tooa 지정된 필요한 경우 hello 역할 인스턴스 아래로 기회 tootake를 제공 하는 역할 인스턴스의 되기 전에 발생 합니다.
* **[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) 이벤트**  
  Hello 구성 변경이 적용된 tooa 지정된는 역할 인스턴스의 한 후에 발생 합니다.

> [!NOTE]
> 인증서 변경을 항상 hello 역할 인스턴스를 오프 라인으로 하기 때문에 hello RoleEnvironment.Changing 또는 RoleEnvironment.Changed 이벤트 발생 하지 않습니다.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
Azure에서 클라우드 서비스로 응용 프로그램 toodeploy hello 적절 한 형식이 첫 번째 패키지 hello 응용 프로그램을 해야합니다. Hello를 사용할 수 있습니다 **CSPack** 명령줄 도구 (hello와 함께 설치 [Azure SDK](https://azure.microsoft.com/downloads/))으로 대체 한 tooVisual Studio toocreate hello 패키지 파일입니다.

**CSPack** 사용 하 여 hello hello 서비스 정의 파일과 서비스 구성 파일 내용의 toodefine hello hello 패키지의 내용입니다. **CSPack** hello를 사용 하 여 응용 프로그램 패키지 파일 (.cspkg) tooAzure를 업로드할 수 생성 [Azure 포털](cloud-services-how-to-create-deploy-portal.md#create-and-deploy)합니다. 기본적으로 hello 패키지 이름은 `[ServiceDefinitionFileName].cspkg`, hello를 사용 하 여 다른 이름을 지정할 수 있지만 `/out` 옵션의 **CSPack**합니다.

**CSPack**은 다음 위치에 있습니다.  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> Hello를 실행 하 여 windows에 CSPack.exe ´ **Microsoft Azure 명령 프롬프트** hello SDK와 함께 설치 되는 바로 가기 합니다.  
> 
> 모든 hello 가능한 스위치와 명령에 대 한 toosee 설명서 단독으로 hello CSPack.exe 프로그램을 실행 합니다.
> 
> 

<p />

> [!TIP]
> Hello에 클라우드 서비스를 로컬로 실행 **Microsoft Azure 계산 에뮬레이터**, hello를 사용 하 여 **/copyonly** 옵션입니다. 이 옵션 hello hello 응용 프로그램 tooa 디렉터리 레이아웃이 있는 hello 계산 에뮬레이터에서 실행 될 수에 대 한 이진 파일을 복사 합니다.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>예제 명령 toopackage 클라우드 서비스
hello 다음 예제에서는 웹 역할에 대 한 hello 정보를 포함 하는 응용 프로그램 패키지 hello 명령 hello 서비스 정의 파일 toouse 지정, 이진 파일이 될 수 있는 hello 디렉터리 발견 하 고 hello hello 패키지 파일의 이름입니다.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Hello 응용 프로그램 웹 역할과 작업자 역할 둘 다 있으면 hello 다음 명령이 사용 됩니다.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

여기서 hello 변수는 다음과 같이 정의 됩니다.

| 변수 | 값 |
| --- | --- |
| \[DirectoryName\] |hello Azure 프로젝트의.csdef 파일 hello를 포함 하는 hello 루트 프로젝트 디렉터리 아래 hello 하위 디렉터리입니다. |
| \[ServiceDefinition\] |hello 서비스 정의 파일의 hello 이름입니다. 기본적으로 이 파일의 이름은 ServiceDefinition.csdef입니다. |
| \[OutputFileName\] |패키지 파일을 생성 하는 hello에 대 한 hello 이름입니다. 일반적으로이 hello 응용 프로그램의 toohello 이름이 설정 됩니다. 으로 hello 응용 프로그램 패키지를 만들 파일 이름은 없으므로 지정 하는 경우 \[ApplicationName\].cspkg입니다. |
| \[RoleName\] |hello 서비스 정의 파일에 정의 된 hello 역할의 hello 이름입니다. |
| \[RoleBinariesDirectory] |hello hello 역할에 대 한 이진 파일의 hello 위치입니다. |
| \[VirtualPath\] |hello hello 서비스 정의의 hello Sites 섹션에 정의 된 각 가상 경로 대 한 실제 디렉터리입니다. |
| \[PhysicalPath\] |hello hello 서비스 정의의 hello 사이트 노드에 정의 된 각 가상 경로 대 한 hello 내용의 실제 디렉터리입니다. |
| \[RoleAssemblyName\] |hello hello 역할에 대 한 이진 파일의 hello 이름입니다. |

## <a name="next-steps"></a>다음 단계
클라우드 서비스 패키지를 만들고 있으며 다음 작업을 수행하려고 합니다.

* [클라우드 서비스 인스턴스에 대해 원격 데스크톱 설정][remotedesktop]
* [클라우드 서비스 프로젝트 배포][deploy]

Visual Studio를 사용하여 다음 작업을 수행하려고 합니다.

* [새 클라우드 서비스 만들기][vs_create]
* [기존 클라우드 서비스 재구성][vs_reconfigure]
* [클라우드 서비스 프로젝트 배포][vs_deploy]
* [클라우드 서비스 인스턴스에 대해 원격 데스크톱 설정][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
