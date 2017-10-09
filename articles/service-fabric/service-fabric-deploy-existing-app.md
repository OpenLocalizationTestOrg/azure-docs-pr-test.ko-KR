---
title: "기존 실행 tooAzure 서비스 패브릭 aaaDeploy | Microsoft Docs"
description: "게스트 실행 파일을 사용할 수 있도록으로 기존 응용 프로그램 toopackage tooa 서비스 패브릭 클러스터를 배포 하는 방법에 대 한 연습"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>게스트 실행 tooService 패브릭 배포
Azure Service Fabric에서 Node.js, Java 또는 C++과 같은 모든 종류의 코드를 서비스로 실행할 수 있습니다. 서비스 패브릭 게스트 실행 파일로 toothese 유형의 서비스를 참조합니다.

게스트 실행 파일은 서비스 패브릭에서 상태 비저장 서비스처럼 취급됩니다. 결과적으로 가용성 및 기타 메트릭을 기반으로 클러스터의 노드에 배치됩니다. 이 문서에서는 설명 방법을 toopackage Visual Studio 또는 명령줄 유틸리티를 사용 하 여 게스트 실행 tooa 서비스 패브릭 클러스터를 배포 합니다.

이 문서에서는 hello 단계 toopackage 게스트 실행 파일을 포함 하 고 패브릭 tooService 배포 합니다.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>서비스 패브릭에서 게스트 실행 파일을 실행할 때의 이점
서비스 패브릭 클러스터에서 실행 되는 게스트는 여러 가지 이점을 toorunning:

* 고가용성. Service Fabric에서 실행되는 응용 프로그램은 고가용성 모드입니다. Service Fabric은 응용 프로그램 인스턴스가 실행 중인지 확인합니다.
* 상태 모니터링. Service Fabric 상태 모니터링은 응용 프로그램이 실행 중인지 감지하고 오류가 있으면 진단 정보를 제공합니다.   
* 응용 프로그램 수명 주기 관리. 중단 시간 없이 업그레이드를 제공할 뿐 아니라 서비스 패브릭 보고 업그레이드 하는 동안 잘못 된 상태 이벤트는 경우 자동 롤백 toohello 이전 버전을 제공 합니다.    
* 밀도. 각 응용 프로그램 toorun 자체 하드웨어에 대 한 hello 필요가 없도록 하므로 클러스터의 여러 응용 프로그램을 실행할 수 있습니다.
* 검색 기능: REST를 사용 하 여 호출할 수 있습니다 hello 서비스 패브릭 명명 서비스 toofind 다른 서비스 hello 클러스터에. 

## <a name="samples"></a>샘플
* [게스트 실행 파일을 패키징 및 배포하는 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [REST를 사용 하 여 hello 명명 서비스를 통해 두 개의 게스트 실행 파일 (C# 및 nodejs) 통신의 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>응용 프로그램 및 서비스 매니페스트 파일 개요
게스트 실행 파일을 배포의 일환으로, 것은 유용 toounderstand hello 서비스 패브릭 패키징 및 배포 모델에 설명 된 대로 [응용 프로그램 모델](service-fabric-application-model.md)합니다. 두 개의 XML 파일이 hello 서비스 패브릭 패키징 모델 사용: 응용 프로그램 및 서비스 매니페스트 hello 합니다. hello 스키마 정의 hello ServiceManifest.xml 및 ApplicationManifest.xml 파일은와 함께 설치에 대 한 hello에 서비스 패브릭 SDK *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **응용 프로그램 매니페스트** hello 응용 프로그램 매니페스트는 사용 되는 toodescribe hello 응용 프로그램입니다. 구성 하는 hello 서비스 및 다른 매개 변수를 사용 하는 toodefine 어떻게 하나 이상의 서비스를 배포, hello 인스턴스 수 등을 나열 합니다.

  Service Fabric에서 응용 프로그램은 배포 및 업그레이드 단위입니다. 응용 프로그램은 잠재적인 오류 및 잠재적 롤백이 관리되는 하나의 단위로 업그레이드될 수 있습니다. 서비스 패브릭 보장 hello 업그레이드 프로세스 중 하나는 성공 또는 hello 업그레이드가 실패 하면, 남지 않습니다 hello 응용 프로그램 알 수 없거나 불안정 한 상태가 됩니다.
* **서비스 매니페스트** hello 서비스 매니페스트는 서비스의 hello 구성 요소를 설명 합니다. Hello 이름 및 유형의 서비스를 같은 데이터를 코드 및 구성을 포함 됩니다. hello 서비스 매니페스트도 몇 가지 추가 매개 변수가 포함 될 수 있는 배포 된 후 tooconfigure hello 서비스를 사용 합니다.

## <a name="application-package-file-structure"></a>응용 프로그램 패키지 파일 구조
응용 프로그램 tooService 패브릭 toodeploy hello 응용 프로그램은 미리 정의 된 디렉터리 구조를 따라야 합니다. hello 다음은 해당 구조의 예입니다.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

hello ApplicationPackageRoot hello 응용 프로그램을 정의 하는 hello ApplicationManifest.xml 파일을 포함 합니다. Hello 응용 프로그램에 포함 된 각 서비스에 대 한 하위 디렉터리에 사용 되는 toocontain hello 서비스에 필요한 아티팩트를 hello 모든입니다. 이러한 하위 디렉터리는 hello ServiceManifest.xml 및 일반적으로 다음 hello입니다.

* *Code*. 이 디렉터리는 hello 서비스 코드를 포함합니다.
* *Config*. 이 디렉터리에 Settings.xml 파일 (및 필요에 따라 다른 파일) hello 서비스 런타임 tooretrieve 특정 구성 설정에 액세스할 수 있습니다.
* *Data*. 이는 추가 디렉터리 toostore 추가 로컬 데이터를 hello 할 수도 있습니다. 데이터에 사용 되는 toostore만 임시 데이터 여야 합니다. 서비스 패브릭 hello 서비스 toobe (예: 장애 조치 중) 위치를 변경 해야 하는 경우 변경 내용을 toohello 데이터 디렉터리를 복제 또는 복사 하지 않습니다.

> [!NOTE]
> Toocreate hello 없는 `config` 및 `data` 필요가 없는 경우에 디렉터리입니다.
>
>

## <a name="package-an-existing-executable"></a>기존 실행 파일 패키징
게스트 실행 파일을 패키징할 때 선택할 수 있습니다 어느 toouse Visual Studio 프로젝트 템플릿 또는 너무[hello 응용 프로그램 패키지를 수동으로 만들](#manually)합니다. 응용 프로그램 패키지 구조 hello Visual Studio를 사용 하 고 드립니다 hello 새 프로젝트 템플릿을 통해 매니페스트 파일이 만들어집니다.

> [!TIP]
> hello 가장 쉬운 방법은 toopackage는 기존 Windows 서비스로 실행 파일은 Visual Studio toouse와 Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Visual Studio toopackage를 사용 하 고 기존 실행 파일 배포
Visual Studio는 서비스 패브릭 서비스 템플릿 toohelp을 게스트 실행 tooa 서비스 패브릭 클러스터를 배포 합니다.

1. **파일** > **새 프로젝트**를 선택하여 Service Fabric 응용 프로그램을 만듭니다.
2. 선택 **게스트 실행 파일** hello 서비스 템플릿으로 합니다.
3. 클릭 **찾아보기** tooselect hello 폴더는 실행 파일, hello 매개 변수 toocreate hello 서비스 hello 나머지를 입력 합니다.
   * *코드 패키지 동작*. 수 집합 toocopy 프로그램 폴더 toohello Visual Studio 프로젝트의 모든 hello 콘텐츠 실행 hello 변경 되지 않는 경우에 유용 합니다. Hello 실행 toochange 예상 하 고 새 빌드를 hello 기능 toopick를 동적으로 원하는 대신 toolink toohello 폴더를 선택할 수 있습니다. Visual Studio에서 hello 응용 프로그램 프로젝트를 만들 때 연결 된 폴더를 사용할 수 있습니다. 이렇게 수 있게 tooupdate hello 게스트 실행 파일의 원본 대상에 hello 프로젝트 내에서 toohello 원본 위치에서 연결 됩니다. 이러한 업데이트를 사용 하면 빌드에 hello 응용 프로그램 패키지의 일부가 됩니다.
   * *프로그램* toostart hello 서비스를 실행 해야 하는 hello 실행 파일을 지정 합니다.
   * *인수* 전달 되어야 하는 toohello 실행 hello 인수를 지정 합니다. 인수가 있는 매개 변수 목록이 될 수도 있습니다.
   * *작업 폴더* toobe 시작이 일어나는 hello 프로세스에 대 한 hello 작업 디렉터리를 지정 합니다. 세 가지 값을 지정할 수 있습니다.
     * `CodeBase`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 toohello 코드 디렉터리를 설정 하 고 중임을 지정 합니다 (`Code` hello 파일 구조를 앞에 표시 된 디렉터리).
     * `CodePackage`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 루트 toohello 설정 되기 지정 (`GuestService1Pkg` hello 파일 구조를 앞에 표시).
     * `Work`hello 파일은 작업 라는 하위 디렉터리에 저장을 지정 합니다.
4. 서비스에 이름을 지정하고 **확인**을 클릭합니다.
5. 서비스 끝점 통신을 위해 필요로 한다면 hello 프로토콜, 포트 및 형식 toohello ServiceManifest.xml 파일 이제 추가할 수 있습니다. 예: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
6. 이제 hello 패키지를 사용 하 고 Visual Studio에서 hello 솔루션을 디버그 하 여 로컬 클러스터에 대해 작업을 게시할 수 있습니다. 준비가 되 면 원격 클러스터를 tooa hello 응용 프로그램을 게시 하거나 hello 솔루션 toosource 컨트롤에서 확인 수 있습니다.
7. 이 문서 toosee toohello 끝을 어떻게 이동 tooview 서비스 패브릭 탐색기에서 실행 중인 게스트 실행 서비스.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Yoeman toopackage를 사용 하 여 및 Linux 기반 기존 실행 파일 배포

Linux에서 실행 되는 게스트를 배포 하기 위한 hello 프로시저 csharp 또는 java 응용 프로그램 배포와 동일 hello 됩니다.

1. 터미널에서 `yo azuresfguest`을 입력합니다.
2. 응용 프로그램의 이름을 지정합니다.
3. 서비스 이름을 지정 하 고 hello 실행 파일의 경로 및 사용 하 여 호출 해야 하는 hello 매개 변수를 포함 하 여 hello 세부 정보를 제공 합니다.

Yeoman 응용 프로그램 패키지 hello 적절 한 응용 프로그램으로 만들고와 함께 매니페스트 파일 설치 및 스크립트를 제거 합니다.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>기존 실행 파일을 수동으로 패키징하고 배포하기
수동으로 게스트 실행 파일을 압축 hello 프로세스 hello 일반적인 단계를 기반으로 합니다.

1. Hello 패키지 디렉터리 구조를 만듭니다.
2. Hello 응용 프로그램의 코드 및 구성 파일을 추가 합니다.
3. Hello 서비스 매니페스트 파일을 편집 합니다.
4. Hello 응용 프로그램 매니페스트 파일을 편집 합니다.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Hello 패키지 디렉터리 구조 만들기
Hello 이전 섹션에에서 설명 된 대로 hello 디렉터리 구조를 만들어서 시작할 수 있습니다 "응용 프로그램 패키지 파일 구조입니다."

### <a name="add-hello-applications-code-and-configuration-files"></a>Hello 응용 프로그램의 코드 및 구성 파일 추가
Hello 디렉터리 구조를 만든 후에 hello 코드 및 config 디렉터리 아래의 hello 응용 프로그램의 코드 및 구성 파일을 추가할 수 있습니다. 또한 추가 디렉터리 또는 hello code 또는 config 디렉터리 아래의 하위 디렉터리를 만들 수 있습니다.

서비스 패브릭 않습니다는 `xcopy` hello 응용 프로그램 루트 디렉터리를 두 개의 상위 디렉터리, 코드 및 설정을 만드는 것 외에 없는 미리 정의 된 구조 toouse 이므로 hello 콘텐츠의 합니다. 하지만 원한다면 다른 이름을 선택할 수 있습니다. 자세한 내용은 hello 다음 섹션에 있습니다.)

> [!NOTE]
> 모든 hello 파일 및 응용 프로그램 요구 hello 종속성을 포함 하는 있는지 확인 합니다. 서비스 패브릭 여기서 hello 응용 프로그램의 서비스는 배포 진행 중인 toobe hello 클러스터의 모든 노드에서 hello 응용 프로그램 패키지의 콘텐츠 hello를 복사 합니다. hello 패키지 hello 일일이 toorun 모든 hello 코드를 포함 해야 합니다. Hello 종속성 이미 설치 되어 있음을 가정 하지 마십시오.
>
>

### <a name="edit-hello-service-manifest-file"></a>Hello 서비스 매니페스트 파일을 편집 합니다.
hello 다음 단계는 tooedit hello 서비스 매니페스트 파일 tooinclude hello 다음 정보:

* hello hello 서비스 형식의 이름입니다. 서비스 패브릭 tooidentify 서비스를 사용 하는 ID입니다.
* hello 명령 toouse toolaunch hello 응용 프로그램 (ExeHost)입니다.
* Toobe 해야 하는 모든 스크립트 tooset hello 응용 프로그램 (SetupEntrypoint)을 실행 합니다.

hello 다음은의 예로 `ServiceManifest.xml` 파일:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

다음 섹션 hello hello tooupdate 해야 하는 hello 파일의 다른 부분을 살펴봅니다.

#### <a name="update-servicetypes"></a>ServiceTypes 업데이트
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* `ServiceTypeName`의 이름을 자유롭게 선택할 수 있습니다. hello hello 값은 사용 `ApplicationManifest.xml` 파일 tooidentify hello 서비스입니다.
* `UseImplicitHost="true"`를 지정합니다. 이 특성을 hello 서비스는 자체 포함 된 응용 프로그램을 기반으로 되므로 모든 서비스 패브릭 필요 toodo toolaunch 서비스 패브릭 지시 프로세스로의 상태를 모니터링 하 고 있습니다.

#### <a name="update-codepackage"></a>CodePackage 업데이트
hello CodePackage 요소 hello 서비스 코드의 hello 위치 (및 버전)을 지정합니다.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

hello `Name` 요소 hello 디렉터리 hello 서비스의 코드를 포함 하는 hello 응용 프로그램 패키지에 사용 되는 toospecify hello 이름입니다. `CodePackage`hello 역시 `version` 특성입니다. 이러한 방식은 사용된 toospecify hello 버전의 hello 코드 하며도 수 서비스 패브릭에서 hello 응용 프로그램 수명 주기 관리 인프라를 사용 하 여 tooupgrade hello 서비스 코드를 사용 합니다.

#### <a name="optional-update-setupentrypoint"></a>선택 사항: SetupEntryPoint 업데이트
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
hello SetupEntryPoint 요소는 사용 되는 toospecify hello 서비스 코드를 시작 하기 전에 실행 해야 하는 모든 실행 파일 또는 배치 파일입니다. 이므로 단계는 선택 사항 toobe 초기화가 없으므로 필요한 경우 포함할 필요는 없습니다. SetupEntryPoint hello hello 서비스를 다시 시작 될 때마다 실행 됩니다.

설치 스크립트 toobe hello 응용 프로그램의 설치 여러 스크립트에 필요한 경우 단일 배치 파일에서 그룹화 할 하나만 SetupEntryPoint가. SetupEntryPoint hello 모든 형식의 파일을 실행할 수 있습니다: 실행 파일, 배치 파일 및 PowerShell cmdlet. 자세한 내용은 [SetupEntryPoint 구성](service-fabric-application-runas-security.md)을 참조하세요.

앞 예제는 hello, SetupEntryPoint hello 라는 배치 파일 실행 `LaunchConfig.cmd` 에 있는 hello 즉 `scripts` hello 코드 디렉터리 (WorkingFolder 요소 hello tooCodeBase 설정 가정)의 하위 디렉터리입니다.

#### <a name="update-entrypoint"></a>EntryPoint 업데이트
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

hello `EntryPoint` hello 서비스 매니페스트 파일에 요소가 사용 되는 toospecify 어떻게 toolaunch hello 서비스입니다. hello `ExeHost` hello 실행 파일 (및 인수) 요소를 지정 해야 하는 toolaunch hello 서비스를 사용 합니다.

* `Program`hello hello 서비스를 시작 해야 하는 hello 실행 파일 이름을 지정 합니다.
* `Arguments`전달 되어야 하는 toohello 실행 hello 인수를 지정 합니다. 인수가 있는 매개 변수 목록이 될 수도 있습니다.
* `WorkingFolder`시작 toobe 이동 하는 hello 프로세스에 대 한 hello 작업 디렉터리를 지정 합니다. 세 가지 값을 지정할 수 있습니다.
  * `CodeBase`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 toohello 코드 디렉터리를 설정 하 고 중임을 지정 합니다 (`Code` 디렉터리 hello 파일 구조를 앞에서).
  * `CodePackage`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 루트 toohello 설정 되기 지정 (`GuestService1Pkg` hello 파일 구조를 앞에).
    * `Work`hello 파일은 작업 라는 하위 디렉터리에 저장을 지정 합니다.

hello 작업 폴더는 상대 경로 hello 응용 프로그램이 나 초기화 스크립트에서 사용할 수 있도록 유용한 tooset hello 올바른 작업 디렉터리입니다.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>통신을 위해 끝점을 업데이트하고 명명 서비스에 등록
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
앞 예제는 hello에서 hello `Endpoint` 요소 hello 응용 프로그램에서 수신할 수 있는 hello 끝점을 지정 합니다. 이 예제에서는 hello Node.js 응용 프로그램의 http 포트 3000 수신합니다.

또한 요청 서비스 패브릭 toopublish이 끝점 toohello 명명 서비스 다른 서비스는 hello 끝점 주소 toothis service를 검색할 수 있도록 합니다. 이렇게 하면 게스트 실행 파일 서비스 간의 toobe 수 toocommunicate 있습니다.
hello 게시 된 끝점 주소는 hello 폼의 `UriScheme://IPAddressOrFQDN:Port/PathSuffix`합니다. `UriScheme` 및 `PathSuffix`는 선택적 특성입니다. `IPAddressOrFQDN`이며 hello IP 주소 또는이 실행 파일에 배치 되는 hello 노드의 정규화 된 도메인 이름 수에 대 한 계산 됩니다.

에 hello 다음 예제에서는 hello 서비스에 한 번 배포 되 면 서비스 패브릭 탐색기 표시에서 비슷한 끝점 너무`http://10.1.4.92:3000/myapp/` hello 서비스 인스턴스에 대 한 게시 합니다. 또는 로컬 컴퓨터인 경우, `http://localhost:3000/myapp/`가 표시됩니다.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
이러한 주소를 사용할 수 있습니다 [역방향 프록시](service-fabric-reverseproxy.md) 서비스 간의 toocommunicate 합니다.

### <a name="edit-hello-application-manifest-file"></a>Hello 응용 프로그램 매니페스트 파일을 편집 합니다.
Hello를 구성한 후 `Servicemanifest.xml` 파일을 일부 변경 내용이 toohello toomake 필요한 `ApplicationManifest.xml` hello tooensure 서비스 유형 및 이름을 사용 되는 올바른 파일입니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
Hello에 `ServiceManifestImport` 요소인 tooinclude hello 응용 프로그램에서 지정 하는 하나 이상의 서비스를 지정할 수 있습니다. 사용 하 여 서비스 참조는 `ServiceManifestName`, 여기서 hello hello hello 디렉터리 이름을 지정 하는 `ServiceManifest.xml` 파일은 합니다.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>로깅 설정
게스트 실행 파일에 대 한 hello 응용 프로그램 및 구성 스크립트는 모든 오류를 표시 하는 경우 유용한 toobe 수 toosee 콘솔 로그 toofind 아웃 됩니다.
콘솔 리디렉션을 hello에서 구성할 수 있습니다 `ServiceManifest.xml` hello를 사용 하 여 파일 `ConsoleRedirection` 요소입니다.

> [!WARNING]
> Hello 콘솔 리디렉션 정책 hello 응용 프로그램 장애 조치에 영향을 줄 수 있으므로 프로덕션에 배포 된 응용 프로그램에서 사용 하지 마십시오. 로컬 개발 및 디버깅 목적으로*만* 사용하세요.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`사용 되는 tooredirect 콘솔 출력 (stdout 및 stderr) tooa 작업 디렉터리를 수 있습니다. Hello 설치 또는 hello 서비스 패브릭 클러스터에 hello 응용 프로그램의 실행 중에 오류가 없는 hello 기능 tooverify 제공 합니다.

`FileRetentionCount`hello 작업 디렉터리에 저장 됩니다 파일 수를 결정 합니다. 5, 예를 들어 의미 hello 이전 5 실행에 대 한 로그 파일 hello hello 작업 디렉터리에 저장 됩니다.

`FileMaxSizeInKb`hello hello 로그 파일의 최대 크기를 지정합니다.

로그 파일은 hello 서비스의 작업 디렉터리 중 하나에 저장 됩니다. hello 파일이 있는 toodetermine 서비스 패브릭 탐색기 toodetermine,는 노드 hello 서비스가 실행 되 고 사용 되는 작업 디렉터리를 사용 합니다. 이 프로세스는 이 문서의 뒷부분에서 다루겠습니다.

## <a name="deployment"></a>배포
hello 마지막 단계는 너무[응용 프로그램을 배포](service-fabric-deploy-remove-applications.md)합니다. PowerShell 스크립트 표시 방법을 따르는 hello toodeploy 응용 프로그램 toohello 로컬 개발 클러스터와 새 서비스 패브릭 서비스를 시작 합니다.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) hello 패키지 크거나 많은 파일을 포함 하는 경우 toohello 이미지 저장소를 복사 하기 전에. [여기](service-fabric-deploy-remove-applications.md#upload-the-application-package)서 자세히 알아보세요.
>

서비스 패브릭 서비스를 다양한 "구성"으로 배포할 수 있습니다. 예를 들어 단일 또는 여러 인스턴스로 배포할 수 또는 hello 서비스 패브릭 클러스터의 각 노드에서 hello 서비스의 한 인스턴스가 하는 방식으로 배포할 수 있습니다.

hello `InstanceCount` hello의 매개 변수 `New-ServiceFabricService` cmdlet은 사용 되는 toospecify hello 서비스의 인스턴스 개수 hello 서비스 패브릭 클러스터에서 실행 되어야 합니다. Hello를 설정할 수 있습니다 `InstanceCount` hello 유형의 배포 하는 응용 프로그램에 따라 값을 합니다. 두 hello 가장 일반적인 시나리오입니다.

* `InstanceCount = "1"` 이 경우 hello 서비스의 인스턴스가 하나만 hello 클러스터에 배포 됩니다. 서비스 패브릭 스케줄러 노드 hello 서비스에 배포 된 toobe 되기 결정 합니다.
* `InstanceCount ="-1"` 이 경우 hello 서비스의 인스턴스 하나 hello 서비스 패브릭 클러스터의 모든 노드에 배포 됩니다. hello 결과 (하나만)의 인스턴스가 단 각 노드에 대 한 hello 서비스 hello 클러스터에 문제가 있습니다.

클라이언트 응용 프로그램 필요 너무 "연결" hello 클러스터 toouse hello 끝점의 hello 노드 tooany 때문에 이것이 프런트 엔드 응용 프로그램 (예를 들어 REST 끝점의 경우)에 대 한 유용한 구성 합니다. 예를 들어 hello 서비스 패브릭 클러스터의 모든 노드에 부하 분산 장치 연결된 tooa 하는 경우이 구성은 사용할 수도 있습니다. 클라이언트 트래픽이 hello 클러스터의 모든 노드에서 실행 되는 hello 서비스에서 배포할 수 있습니다.

## <a name="check-your-running-application"></a>실행 중인 응용 프로그램 확인
서비스 패브릭 탐색기 hello 서비스가 실행 되 고 hello 노드를 식별 합니다. 이 예제에서는 Node1에서 실행됩니다.

![서비스가 실행 중인 노드](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Toohello 노드를 탐색 하 고 toohello 응용 프로그램을 찾아볼 경우 hello 필수 노드 정보를 디스크에서의 위치를 포함 하 여 표시 됩니다.

![디스크 상의 위치](./media/service-fabric-deploy-existing-app/locationondisk2.png)

서버 탐색기를 사용 하 여 toohello 디렉터리를 찾을 때는 hello 다음 스크린 샷에서 같이 hello 작업 디렉터리 및 hello 서비스의 로그 폴더를 찾을 수 있습니다. 

![로그 위치](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 어떻게 toopackage 게스트 실행 파일 및 tooService 패브릭 배포 합니다. 다음 관련된 정보 및 작업에 대 한 아티클을 hello를 참조 하십시오.

* [패키징 및 배포 게스트 실행 파일에 대 한 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), hello 패키징 도구의 링크 toohello 시험판 포함
* [REST를 사용 하 여 hello 명명 서비스를 통해 두 개의 게스트 실행 파일 (C# 및 nodejs) 통신의 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [여러 개의 게스트 실행 파일 배포](service-fabric-deploy-multiple-apps.md)
* [Visual Studio를 사용하여 처음으로 서비스 패브릭 응용 프로그램 만들기](service-fabric-create-your-first-application-in-visual-studio.md)
