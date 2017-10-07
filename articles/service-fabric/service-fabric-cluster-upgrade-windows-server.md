---
title: "Windows Server에서 독립 실행형 Azure 서비스 패브릭 클러스터 aaaUpgrade | Microsoft Docs"
description: "Hello 클러스터 업데이트 모드 설정을 포함 하는 독립 실행형 서비스 패브릭 클러스터를 실행 하는 구성 및/또는 hello Azure Service Fabric 코드를 업그레이드 합니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Windows Server 클러스터에서 독립 실행형 Azure Service Fabric 업그레이드
> [!div class="op_single_selector"]
> * [Azure 클러스터](service-fabric-cluster-upgrade.md)
> * [독립 실행형 클러스터](service-fabric-cluster-upgrade-windows-server.md)
>
>

모든 최신 시스템 hello 기능 tooupgrade 제품 키 toohello 장기적인 성공을입니다. Azure 서비스 패브릭 클러스터는 사용자가 소유하는 리소스입니다. 이 문서를 만드는 방법을 해당 hello 클러스터 서비스 패브릭 코드와 구성의 지원 되는 버전으로 항상 실행 되는지 설명 합니다.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>클러스터에서 실행 되는 제어 hello 서비스 패브릭 버전
Microsoft는 새 버전 집합 hello를 놓을 때 서비스 패브릭의 클러스터 toodownload 업데이트 tooset **fabricClusterAutoupgradeEnabled** 구성 tootrue를 클러스터 합니다. 프로그램 클러스터 toobe 집합 hello에 원하는 서비스 패브릭의 지원 되는 버전 tooselect **fabricClusterAutoupgradeEnabled** 구성 toofalse를 클러스터 합니다.

> [!NOTE]
> 클러스터가 지원되는 Service Fabric 버전을 항상 실행하는지 확인합니다. Microsoft가 서비스 패브릭의 새 버전의 hello 릴리스 데몬에, hello 이전 버전 지원 종료에 대 한 최소 hello 알림이의 hello 날짜 로부터 60 일 후 표시 됩니다. 새 릴리스 발표 됩니다 [hello 서비스 패브릭 팀 블로그에](https://blogs.msdn.microsoft.com/azureservicefabric/)합니다. hello 새 릴리스는 해당 위치에서 사용할 수 있는 toochoose 되 합니다.
>
>

각 서비스 패브릭 노드는 별도 물리적 컴퓨터 또는 가상 컴퓨터에는 할당은 프로덕션 스타일 노드 구성 사용 중인 경우에 클러스터 toohello 새 버전을 업그레이드할 수 있습니다. 여기서는 단일 물리적 컴퓨터 또는 가상 컴퓨터에 여러 개의 서비스 패브릭 노드는, 개발 클러스터에 있는 경우 다시 hello 새 버전으로 hello 클러스터를 만들어야 합니다.

두 개의 고유 워크플로 클러스터 toohello 최신 버전 또는 지원 되는 서비스 패브릭 버전을 업그레이드할 수 있습니다. 클러스터 자동으로 연결 toodownload hello에 대 한 최신 정보를 한 워크플로입니다. hello 다른 워크플로 연결 toodownload hello 최신 서비스 패브릭 버전을 갖지 않는 클러스터용입니다.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>업그레이드 클러스터 연결 toodownload hello 최신 코드 및 구성
클러스터 노드 인터넷 연결을 너무 있는 경우 이러한 단계 tooupgrade 클러스터 tooa 지원 버전을 사용[http://download.microsoft.com](http://download.microsoft.com)합니다.

너무 연결 된 클러스터에 대 한[http://download.microsoft.com](http://download.microsoft.com), 새 서비스 패브릭 버전의 hello 가용성에 대 한 Microsoft 주기적으로 검사 합니다.

새 서비스 패브릭 버전을 사용할 수 있는 hello 패키지를 로컬로 다운로드 toohello 클러스터 업그레이드에 대 한 프로 비전 합니다. 또한 tooinform hello 고객이 새 버전의 hello 시스템은 명시적 클러스터 상태 경고에 따라 유사한 toohello 표시:

"hello 현재 클러스터 [버전 #] 버전 지원 종료 [Date]."

Hello 클러스터 hello 최신 버전을 실행 한 후 hello 경고가 사라집니다.

#### <a name="cluster-upgrade-workflow"></a>클러스터 업그레이드 워크플로
Hello 클러스터 상태 경고를 본 후 다음 hello지 않습니다.

1. 관리자 액세스 tooall hello 컴퓨터 hello 클러스터의 노드도 나열 되는 모든 컴퓨터에서 toohello 클러스터를 연결 합니다. 이 스크립트에서 실행 되는 hello 컴퓨터에는 hello 클러스터의 일부가 toobe 없습니다.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. 로 업그레이드할 수 있는 서비스 패브릭 버전의 hello 목록을 가져옵니다.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    출력 유사한 toothis을 받습니다.

    ![패브릭 버전 가져오기][getfabversions]
3. 클러스터 업그레이드 tooan 사용 가능한 버전을 사용 하 여 시작 된 [시작 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   toomonitor hello hello 업그레이드의 진행 상황을 서비스 패브릭 탐색기 또는 다음 Windows PowerShell 명령이 실행된 hello를 사용할 수 있습니다.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Hello 클러스터 상태 정책을 충족 되지 않으면 hello 업그레이드가 롤백됩니다. hello에 대 한 사용자 지정 상태 정책을 toospecify **시작 ServiceFabricClusterUpgrade** 명령에 대 한 설명서를 참조 하십시오 [시작 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)합니다.

Hello 롤백이 발생 하는 hello 문제를 해결 한 후 동일한 단계 앞에서 설명한 다음 hello 하 여 hello 업그레이드를 다시 시작 합니다.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>클러스터 업그레이드 <U>에 연결 되지 않은</u> toodownload hello 최신 코드 및 구성
사용 하 여 이러한 단계 tooupgrade 클러스터 지원 tooa 버전 클러스터 노드가 없는 경우 인터넷 연결 너무[http://download.microsoft.com](http://download.microsoft.com)합니다.

> [!NOTE]
> 연결 된 toohello 인터넷 있는 클러스터를 실행 하는 경우 새 버전에 대 한 toomonitor hello 서비스 패브릭 팀 블로그 toolearn을 해야 합니다. 클러스터 상태 경고 tooalert hello 시스템은 표시 되지 않습니다 새 릴리스의 있습니다.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>자동 프로비전 및 수동 프로비전
tooenable 자동 다운로드 및 최신 코드 버전 hello에 대 한 등록 서비스 패브릭 업데이트 서비스를 설정 합니다. Hello 내 Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt toohello 참조 [독립 실행형 패키지](service-fabric-cluster-standalone-package-contents.md) 지침에 대 한 합니다.
수동 프로세스에 대 한 아래의 hello 지침을 따릅니다.

구성 업그레이드를 시작 하기 전에 속성 toofalse 다음 하 여 클러스터 구성 tooset hello를 수정 합니다.

        "fabricClusterAutoupgradeEnabled": false,

너무 참조[시작 ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) 사용 정보에 대 한 합니다. Hello 구성 업그레이드를 시작 하기 전에, JSON에서 있는지 tooupdate 'clusterConfigurationVersion'를 확인 합니다.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>클러스터 업그레이드 워크플로

1. Get ServiceFabricClusterUpgrade hello hello 클러스터 노드 중 하나에서 실행 하 고 hello TargetCodeVersion를 기록해 둡니다.
2. 인터넷 연결된 컴퓨터 toolist에서 다음을 실행된 하는 hello 모든 hello 현재 버전과 호환 되는 버전을 업그레이드 하 고 hello 관련 된 다운로드 링크에서 패키지에 해당 하는 hello를 다운로드 합니다.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. 관리자 액세스 tooall hello 컴퓨터 hello 클러스터의 노드도 나열 되는 모든 컴퓨터에서 toohello 클러스터를 연결 합니다. 이 스크립트에서 실행 되는 hello 컴퓨터 hello 클러스터의 일부가 toobe가 없습니다.

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Hello 클러스터 이미지 저장소 hello 다운로드 한 패키지를 복사 합니다.

5. Hello 복사 된 패키지를 등록 합니다.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. 클러스터 업그레이드 tooan 사용 가능한 버전을 시작 합니다.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   서비스 패브릭 탐색기에 hello 업그레이드의 hello 진행률을 모니터링할 수 있습니다 또는 hello 다음 PowerShell 명령을 실행할 수 있습니다.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Hello 클러스터 상태 정책을 충족 되지 않으면 hello 업그레이드가 롤백됩니다. hello에 대 한 사용자 지정 상태 정책을 toospecify **시작 ServiceFabricClusterUpgrade** 명령에 대 한 hello 설명서를 참조 하십시오 [시작 ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)합니다.

Hello 롤백이 발생 하는 hello 문제를 해결 한 후 동일한 단계 앞에서 설명한 다음 hello 하 여 hello 업그레이드를 다시 시작 합니다.


## <a name="upgrade-hello-cluster-configuration"></a>업그레이드 hello 클러스터 구성
Hello 구성 업그레이드를 시작 하기 전에 hello 독립 실행형 패키지에서 hello powershell 스크립트를 실행 하 여, 새 클러스터 구성 json을 테스트할 수 있습니다.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
또는

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

끝점, 클러스터 이름, 노드 IP 등의 일부 구성은 업그레이드할 수 없습니다. Hello 새 클러스터 구성 json 이전과 hello에 대 한 테스트 되 고 모든 문제가 있는 경우 hello Powershell 창에서 오류를 throw 합니다.

tooupgrade hello 클러스터 구성 업그레이드가 실행 **시작 ServiceFabricClusterConfigurationUpgrade**합니다. hello 구성 업그레이드는 업그레이드 도메인에 의해 처리 된 업그레이드 도메인입니다.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>클러스터 인증서 구성 업그레이드  
클러스터 인증서 클러스터 노드 간 인증에 사용 되, hello 인증서 롤오버 되므로 오류는 클러스터 노드 간에 hello 통신을 차단 하는 것 때문에 추가로 주의 해 서 수행할 수 해야 합니다.  
기술적으로 세 가지 옵션이 지원됩니다.  

1. 단일 인증서 업그레이드: hello 업그레이드 경로 ' (주) 인증서 B (기본)-> 인증서-인증서 C (기본) >->...'입니다.   
2. Double 인증서 업그레이드: hello 업그레이드 경로 ' 인증서 (기본)-> 인증서 (주) 및 (보조) B-인증서 B (기본) > 인증서 B (기본)-> 및 (보조) C-인증서 C (기본) >->...'입니다.
3. 인증서 형식 업그레이드: 지문 기반 인증서 구성 <-> CommonName 기반 인증서 구성입니다. 예를 들어, 인증서 지문 A(기본) 및 지문 B(보조) -> 인증서 CommonName C입니다.


## <a name="next-steps"></a>다음 단계
* 자세한 내용은 방법 toocustomize 일부 [서비스 패브릭 클러스터 설정](service-fabric-cluster-fabric-settings.md)합니다.
* 너무 방법에 대해 알아봅니다[클러스터를 확장 및 축소](service-fabric-cluster-scale-up-down.md)합니다.
* [응용 프로그램 업그레이드](service-fabric-application-upgrade.md)에 대해 알아보기

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
