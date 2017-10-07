---
title: "서비스 패브릭 응용 프로그램 배포 aaaAzure | Microsoft Docs"
description: "어떻게 toodeploy 및 제거 PowerShell을 사용 하 여 서비스 패브릭 응용 프로그램입니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>PowerShell을 사용하여 응용 프로그램 배포 및 제거
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

일단 [응용 프로그램 형식이 패키지화되면][10] Azure Service Fabric 클러스터에 배포될 준비가 된 것입니다. 배포에는 세 단계를 수행 하는 hello 포함 됩니다.

1. Hello 응용 프로그램 패키지 toohello 이미지 저장소에 업로드
2. Hello 응용 프로그램 형식 등록
3. Hello 응용 프로그램 인스턴스 만들기

한 후 응용 프로그램이 배포 된 hello 클러스터에서 실행 중인 인스턴스를 hello 응용 프로그램 인스턴스 및 해당 응용 프로그램 종류를 삭제할 수 있습니다. hello 클러스터에서 응용 프로그램 toocompletely 제거 단계를 수행 하는 hello 포함 됩니다.

1. 응용 프로그램 인스턴스를 실행 하는 hello 제거 (또는 삭제)
2. 필요 없는 hello 응용 프로그램 종류를 등록 취소
3. Hello 이미지 저장소에서 hello 응용 프로그램 패키지를 제거 합니다.

사용 하는 경우 [배포 및 응용 프로그램 디버깅에 대 한 Visual Studio](service-fabric-publish-app-remote-cluster.md) 앞의 단계를 hello 모든 로컬 개발 클러스터에는 PowerShell 스크립트를 통해 자동으로 처리 됩니다.  이 스크립트는 hello에서 발견 되 *스크립트* hello 응용 프로그램 프로젝트의 폴더입니다. 이 문서에서는 수행할 수 있도록 해당 스크립트가 수행 하는 작업에 배경 제공 hello Visual Studio 외부에서 이와 동일한 작업을 합니다. 
 
## <a name="connect-toohello-cluster"></a>Toohello 클러스터에 연결
이 문서에는 PowerShell 명령을 실행 하기 전에 항상 사용 하 여 시작 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello 서비스 패브릭 클러스터입니다. tooconnect toohello 로컬 개발 클러스터 hello 다음 실행:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Tooa 원격 클러스터 또는 클러스터 X509 Azure Active Directory를 사용 하 여 보안 연결의 예제를 보려면 인증서 또는 Windows Active Directory 참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md)합니다.

## <a name="upload-hello-application-package"></a>Hello 응용 프로그램 패키지 업로드
Hello 응용 프로그램 패키지를 업로드 하는 중 내부 서비스 패브릭 구성 요소에서 액세스할 수 있는 위치에 배치 됩니다.
Tooverify hello 응용 프로그램 패키지를 로컬로 원할 경우 사용 하 여 hello [테스트 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

hello [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 업로드 응용 프로그램 패키지 toohello 클러스터 이미지 저장소 hello 명령입니다.
hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.  tooimport hello SDK 모듈을 실행 합니다.

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Visual Studio 2015에서 *MyApplication*이라는 응용 프로그램을 빌드하고 패키지한다고 가정해 보겠습니다. 기본적으로 hello 응용 프로그램 유형 이름은 ApplicationManifest.xml hello에 나열 된 "MyApplicationType"는 합니다.  hello hello 필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드/config/데이터 패키지를 포함 하는 응용 프로그램 패키지에 있는 *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*합니다. 

hello 다음 명령은 나열 hello hello 응용 프로그램 패키지 내용의 압축 합니다.

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Hello 응용 프로그램 패키지 큰 많은 파일의 경우, 다음을 할 수 있습니다 [압축](service-fabric-package-apps.md#compress-a-package)합니다. hello 압축 hello 크기와 파일 hello 수가 줄어듭니다.
hello 부작용은 해당 등록 및 등록을 취소 hello 응용 프로그램 종류는 경우 더욱 빠릅니다. 업로드 시간이 느려질 수 있습니다 현재 hello 타임 toocompress hello 패키지를 포함 하는 경우에 특히. 

패키지를 사용 하 여 toocompress hello 동일 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령입니다. 압축에서에서 수행할 수 있습니다 별도 업로드 hello를 사용 하 여 `SkipCopy` 플래그를 지정 하거나 hello와 함께 작업을 업로드 합니다. 압축된 패키지에 압축을 적용하면 아무런 변화가 없습니다.
압축된 된 패키지를 사용 하 여 toouncompress hello 동일 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello로 명령을 `UncompressPackage` 전환 합니다.

hello 다음 cmdlet 압축 hello 패키지 toohello 이미지 저장소를 복사 하지 않고 합니다. hello 패키지는 이제 hello에 대 한 압축 된 파일을 포함 `Code` 및 `Config` 패키지 합니다. hello 응용 프로그램 및 서비스 매니페스트 hello 하지 압축 된, 많은 내부 작업 (예: 공유, 특정 유효성 검사에 대 한 응용 프로그램 유형 이름 및 버전 추출 패키지)에 필요 하기 때문입니다. 이동식 hello 매니페스트는 비효율적인 이러한 작업을 확인 합니다.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

대형 응용 프로그램 패키지에 대 한 hello 압축 시간이 걸립니다. 최상의 결과를 얻으려면 빠른 SSD 드라이브를 사용합니다. hello 압축 시간과 hello 압축 된 패키지의 hello 크기 또한 hello 패키지 내용에 따라 다릅니다.
예를 들어 일부 패키지에는 초기 hello를 표시 하 고 hello 압축 시간으로 압축 된 패키지 크기 hello에 대 한 압축 통계 같습니다.

|초기 크기(MB)|파일 수|압축 시간|압축된 패키지 크기(MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

패키지 압축 되 면 필요에 따라 여러 서비스 패브릭 클러스터 또는 업로드 된 tooone 수 있습니다. hello 배포 메커니즘은 압축 된 백업과 압축 되지 않은 패키지에 대 한 동일 합니다. Hello 패키지 압축 된 경우 hello 클러스터 이미지 저장소에 따라서 저장 되 고 hello 응용 프로그램을 실행 하기 전에 hello 노드에서 압축 합니다.


hello 다음 예제에서는 hello 패키지 toohello 이미지 저장소에 업로드 "MyApplicationV1" 라는 폴더:

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.  tooimport hello SDK 모듈을 실행 합니다.

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Hello를 지정 하지 않으면 *-ApplicationPackagePathInImageStore* hello 응용 프로그램 패키지 매개 변수는 hello 이미지 저장소에 hello "Debug" 폴더에 복사 됩니다.

hello 시간이 tooupload 패키지 여러 요인에 따라 달라 집니다. 이러한 요소 중 일부는 hello hello 패키지, 패키지 크기 hello 및 hello 파일 크기의 파일 수입니다. hello 원본 컴퓨터와 hello 서비스 패브릭 클러스터 간의 네트워크 속도가 hello hello 업로드 시간에도 영향을 줍니다. 기본 시간 제한을 hello [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 30 분입니다.
에 따라 설명된 요소 hello, tooincrease hello 제한 시간을 할 수 있습니다. Tooalso hello 복사 호출에서 hello 패키지를 압축 하는 경우 해야 hello 압축 시간을 고려 합니다.

참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.

## <a name="register-hello-application-package"></a>Hello 응용 프로그램 패키지를 등록 합니다.
hello 응용 프로그램 유형 및 버전 hello 응용 프로그램 패키지를 등록 하면 사용 하기 위해 사용할 수 있게 하는 hello 응용 프로그램 매니페스트에 선언 합니다. hello 시스템 hello 이전 단계에서 업로드 된 hello 패키지가, hello 패키지를 확인, hello 패키지 내용 처리 읽고 처리 하는 hello 패키지 tooan 내부 시스템 위치에 복사 합니다.  

Hello 실행 [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello hello 클러스터에서 응용 프로그램 종류 및 배포에 사용할 수 있도록 합니다.

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

"MyApplicationV1"는 hello 응용 프로그램 패키지가 위치한 hello 이미지 저장소 hello 폴더입니다. hello 응용 프로그램 유형 이름이 "MyApplicationType" 고 버전이 "1.0.0" (둘 다에 있습니다. 응용 프로그램 매니페스트 hello)이 이제 hello 클러스터에 등록 됩니다.

hello [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 명령은 hello 시스템에 성공적으로 등록 된 hello 응용 프로그램 패키지 한 후에 반환 합니다. 시간 등록은 hello 크기와 hello 응용 프로그램 패키지의 내용에 따라 달라 집니다. 필요한 경우 hello **-TimeoutSec** 매개 변수를 사용 하는 toosupply 긴 시간 제한 수 (hello 기본 제한 시간은 60 초)입니다.

패키지 또는 hello를 사용 하 여 시간 초과 발생 하는 경우 큰 응용 프로그램의 경우 **-Async** 매개 변수입니다. hello 명령은 hello 클러스터 hello 등록 명령을 수락 하 고 필요에 따라 hello 처리가 계속를 반환 합니다.
hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 모든 성공적으로 등록 된 응용 프로그램 유형 버전 및 해당 등록 상태를 나열 합니다. 이 명령은 toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기
Hello를 사용 하 여 성공적으로 등록 된 모든 응용 프로그램 종류 버전에서 응용 프로그램을 인스턴스화할 수 [새로 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet. 각 응용 프로그램의 hello 이름 hello로 시작 해야 *"fabric:"* 구성표 및 각 응용 프로그램 인스턴스에 대해 고유 해야 합니다. Hello 대상 응용 프로그램 종류의 응용 프로그램 매니페스트 hello에에서 정의 된 기본 서비스 만들어집니다.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
등록된 응용 프로그램 형식의 주어진 어떤 버전에 대해서도 여러 개의 응용 프로그램 인스턴스를 만들 수 있습니다. 각 응용 프로그램 인스턴스는 자체 작업 디렉터리 및 프로세스와는 별도로 실행됩니다.

hello를 실행 하는 hello 클러스터에서 실행 하는 앱 및 서비스 이라는 toosee [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 및 [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>응용 프로그램 제거
응용 프로그램 인스턴스가 필요 하지 않은 경우 제거할 수 없습니다 영구적으로 hello를 사용 하 여 이름 [제거 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. [제거 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) 도, 영구적으로 모든 서비스 상태를 제거 하는 toohello 응용 프로그램에 포함 된 모든 서비스를 자동으로 제거 합니다. 

> [!WARNING]
> 이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>응용 프로그램 유형 등록 취소
Hello를 사용 하 여 hello 응용 프로그램 종류를 등록 취소 해야 응용 프로그램 종류의 특정 버전은 더 이상 필요 없는, [등록 취소 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. 등록을 취소 사용 하지 않는 응용 프로그램 종류 버전 저장소 공간 hello 이미지 저장소에서 사용 하는입니다. 응용 프로그램 형식은 이에 대해 인스턴스화된 응용 프로그램이나 이를 참조하는 보류 중인 응용 프로그램이 없는 한 등록 취소할 수 있습니다.

실행 [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello 응용 프로그램 종류는 현재 hello 클러스터에 등록 되어 있습니다.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

실행 [등록 취소 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister 특정 응용 프로그램 종류:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Hello 이미지 저장소에서 응용 프로그램 패키지를 제거 합니다.
응용 프로그램 패키지 더 이상 필요 하면 시스템 리소스를 hello 이미지 저장소 toofree에서 삭제할 수 없습니다.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>문제 해결
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage가 ImageStoreConnectionString을 요청함
서비스 패브릭 SDK 환경 hello hello 기본값을 설정 하 고 올바른 이미 있어야 합니다. 하지만 해당 hello 서비스 패브릭 클러스터를 사용 하 여 모든 명령에 대 한 hello ImageStoreConnectionString 해야 hello 값 필요한 경우 일치 합니다. Hello ImageStoreConnectionString hello 클러스터 매니페스트에서 찾을 수 있습니다 hello를 사용 하 여 검색 [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 및 Get ImageStoreConnectionStringFromClusterManifest 명령:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.  tooimport hello SDK 모듈을 실행 합니다.

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

hello ImageStoreConnectionString은 hello 클러스터 매니페스트에 있습니다.

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.

### <a name="deploy-large-application-package"></a>대형 응용 프로그램 패키지 배포
문제: 대형 응용 프로그램 패키지(GB 단위)에 대한 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 시간이 초과되었습니다.
다음을 시도해 보세요.
- [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다. 기본적으로 hello 제한 시간 30 분입니다.
- 원본 컴퓨터와 클러스터 간에 hello 네트워크 연결을 확인 합니다. Hello 연결이 느린 경우에 컴퓨터를 사용 하 여 더 나은 네트워크 연결을 사용 하는 것이 좋습니다.
Hello 클라이언트 컴퓨터가 hello 클러스터와 다른 지역에 있는 경우에 hello 클러스터와 가깝거나 동일한 지역에 클라이언트 컴퓨터를 사용 하는 것이 좋습니다.
- 외부 제한에 도달하고 있는지 확인합니다. 예를 들어 hello 이미지 저장소에 구성 된 toouse azure 저장소가, 업로드 제한 될 수 있습니다.

문제: 패키지 업로드가 성공적으로 완료되었지만 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 시간이 초과되었습니다. 다음을 시도해 보세요.
- [Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에.
hello 압축 hello 크기가 줄어들고에 hello 트래픽 양이 감소 하 고 해당 서비스 패브릭 작업 hello 수의 파일을 수행 해야 합니다. hello 업로드 작업 (특히 포함 하는 경우 hello 압축 시간)에 속도가 느려질 수 있습니다, 하지만 등록 및 등록을 취소할 hello 응용 프로그램 종류는 더 빠릅니다.
- [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.
- [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `Async` 스위치를 지정합니다. hello 명령은 hello 클러스터 hello 명령을 수락 하 고 hello 응용 프로그램 종류의 hello 등록 계속 비동기식으로 반환 합니다. 이러한 이유로 있습니다 없습니다 필요 toospecify 정하도록이 경우. hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 모든 성공적으로 등록 된 응용 프로그램 유형 버전 및 해당 등록 상태를 나열 합니다. 이 명령은 toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>많은 파일이 있는 응용 프로그램 패키지 배포
문제: 많은 파일(1,000개 단위)이 있는 응용 프로그램 패키지에 대한 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 시간이 초과되었습니다.
다음을 시도해 보세요.
- [Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에. hello 압축 hello 파일 수를 줄입니다.
- [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.
- [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `Async` 스위치를 지정합니다. hello 명령은 hello 클러스터 hello 명령을 수락 하 고 hello 응용 프로그램 종류의 hello 등록 계속 비동기식으로 반환 합니다.
이러한 이유로 있습니다 없습니다 필요 toospecify 정하도록이 경우. hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 모든 성공적으로 등록 된 응용 프로그램 유형 버전 및 해당 등록 상태를 나열 합니다. 이 명령은 toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>다음 단계
[서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

[서비스 패브릭 상태 소개](service-fabric-health-introduction.md)

[서비스 패브릭 서비스 진단 및 문제 해결](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[서비스 패브릭에서 응용 프로그램 모델링](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
