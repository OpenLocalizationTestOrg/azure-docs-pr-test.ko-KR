---
title: "aaaDeploy 및 Azure microservices 로컬로 업그레이드 | Microsoft Docs"
description: "로컬 서비스 패브릭 클러스터를 tooset 기존 응용 프로그램 tooit, 배포 하 고 다음 해당 응용 프로그램을 업그레이드 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>로컬 클러스터에서 응용 프로그램 배포 및 업그레이드 시작
hello Azure Service Fabric SDK에서는 사용할 수 있는 전체 로컬 개발 환경을 배포 하 고 로컬 클러스터에 있는 응용 프로그램 관리 tooquickly 시작 합니다. 이 문서에서는 로컬 클러스터 배포는 기존 응용 프로그램 tooit 만들고 해당 응용 프로그램 tooa 새 버전을 Windows PowerShell에서 업그레이드 합니다.

> [!NOTE]
> 이 문서는 이미 [개발 환경을 설정](service-fabric-get-started.md)한 것으로 가정합니다.
> 
> 

## <a name="create-a-local-cluster"></a>로컬 클러스터 만들기
서비스 패브릭 클러스터는 응용 프로그램을 배포할 수 있는 하드웨어 리소스의 집합을 나타냅니다. 일반적으로 클러스터 이루어져 아무 곳 이나 5 toomany 수천 대의 컴퓨터에서에서 합니다. 그러나 hello 서비스 패브릭 SDK는 단일 컴퓨터에서 실행할 수 있는 클러스터 구성에 포함 됩니다.

로컬 서비스 패브릭 클러스터 hello toounderstand 에뮬레이터 또는 시뮬레이터가 유용 합니다. 이 실행 hello 다중 컴퓨터 클러스터에 있는 동일한 플랫폼 코드입니다. hello 유일한 차이점은 hello 플랫폼 프로세스 분산 되는 일반적으로 하나의 시스템에 5 개의 컴퓨터를 실행 합니다.

hello SDK에서는 로컬 클러스터를 두 가지 방법으로 tooset:는 Windows PowerShell 스크립트 및 hello 로컬 클러스터 관리자 시스템 트레이 앱. 이 자습서에서는 hello PowerShell 스크립트를 사용 했습니다.

> [!NOTE]
> Visual Studio에서 응용 프로그램을 배포하여 이미 로컬 클러스터를 만든 경우 이 섹션을 건너뛸 수 있습니다.
> 
> 

1. 새 PowerShell 창을 관리자 권한으로 실행합니다.
2. Hello SDK 폴더에서 hello 클러스터 설치 스크립트를 실행 합니다.
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    클러스터 설치는 몇 분 정도 걸립니다. 설치가 완료된 후 다음과 같은 출력이 표시됩니다.
   
    ![클러스터 설정 출력][cluster-setup-success]
   
    응용 프로그램 tooyour 클러스터 배포 준비 tootry가 나타납니다.

## <a name="deploy-an-application"></a>응용 프로그램 배포
서비스 패브릭 SDK hello 다양 한 프레임 워크 및 개발자 응용 프로그램을 만들기 위한 도구를 포함 합니다. Visual Studio에서 toocreate 응용 프로그램 참조 방법을 학습에 관심이 있는 경우 [Visual Studio에서 첫 번째 서비스 패브릭 응용 프로그램을 만들](service-fabric-create-your-first-application-in-visual-studio.md)합니다.

이 자습서를 사용 하 여 기존 샘플 응용 프로그램 (WordCount 라고 함) hello 플랫폼의 관리 측면 hello에 집중할 수 있도록: 배포, 모니터링 및 업그레이드 합니다.

1. 새 PowerShell 창을 관리자 권한으로 실행합니다.
2. Hello 서비스 패브릭 SDK PowerShell 모듈을 가져옵니다.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. 다운로드 하 고 C:\ServiceFabric 같은 배포 하는 디렉터리 toostore hello 응용 프로그램을 만듭니다.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Hello WordCount 응용 프로그램을 다운로드](http://aka.ms/servicefabric-wordcountapp) 만든 toohello 위치입니다.  참고: hello Microsoft Edge 브라우저 hello 파일을 저장 하는 *.zip* 확장 합니다.  Hello 파일 확장명도 변경*.sfpkg*합니다.
5. Toohello 로컬 클러스터에 연결 합니다.
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. 이름 및 경로 toohello 응용 프로그램 패키지를 사용 하 여 hello SDK 배포 명령을 사용 하 여 새 응용 프로그램을 만듭니다.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    모든 것이 제대로 출력 뒤 hello를 표시 되어야 합니다.
   
    ![응용 프로그램 toohello 로컬 클러스터 배포][deploy-app-to-local-cluster]
7. 작업에서 toosee hello 응용 프로그램 hello 브라우저를 시작 및 탐색 너무[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html)합니다. 다음과 같은 결과가 표시됩니다.
   
    ![배포된 응용 프로그램 UI][deployed-app-ui]
   
    hello WordCount 응용 프로그램은 간단 합니다. 클라이언트 쪽 JavaScript 코드 toogenerate 임의 5 자로 이루어진 "단어"를 포함 하 되 다음 헤더 블록이 릴레이 ASP.NET Web API를 통해 toohello 응용 프로그램입니다. 상태 저장 서비스 계산 단어 hello 수를 추적 합니다. Hello hello 단어의 첫 문자를 기준으로 인덱스가 분할 됩니다. Hello WordCount 앱 hello에 대 한 hello 소스 코드를 찾을 수 있습니다 [클래식 시작 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)합니다.
   
    4 개의 파티션을 포함 하는 hello 응용 프로그램을 배포 합니다. G A로 시작 하는 단어 hello 첫 번째 파티션에 저장 되며, 하므로 – N으로 시작 하는 단어 hello 두 번째 파티션 및 기타 등등에 저장 됩니다.

## <a name="view-application-details-and-status"></a>응용 프로그램 세부 정보 및 상태 보기
Hello 응용 프로그램 배포 म 했으므로 powershell에서 hello 앱 세부 정보 중 일부에서 살펴보겠습니다.

1. Hello 클러스터에 배포 된 모든 응용 프로그램을 쿼리 합니다.
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    만 hello WordCount 응용 프로그램을 배포한 것과 비슷한 참조:
   
    ![PowerShell에 배포된 모든 응용 프로그램 쿼리][ps-getsfapp]
2. Hello hello WordCount 응용 프로그램에 포함 된 서비스 집합을 쿼리하여 toohello 다음 수준을 이동 합니다.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![PowerShell에서 hello 응용 프로그램에 대 한 서비스 나열][ps-getsfsvc]
   
    두 개의 서비스, hello 웹 프런트 엔드 및 단어 hello를 관리 하는 hello 상태 저장 서비스의 hello 응용 프로그램으로 이루어집니다.
3. 마지막으로, WordCountService에 대 한 파티션 목록이 hello 살펴보겠습니다.
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![PowerShell에서 사용 되는 hello 서비스 파티션 보기][ps-getsfpartitions]
   
    hello 같은 모든 서비스 패브릭 PowerShell 명령을 사용 하는 명령 집합, 로컬 또는 원격에 연결할 수 있는 모든 클러스터에 사용할 수 있습니다.
   
    Hello 클러스터와 보다 시각적인 방식으로 toointeract에 대 한 너무 이동 하 여 hello 웹 기반 서비스 패브릭 탐색기 도구를 사용할 수 있습니다[http://localhost:19080/탐색기](http://localhost:19080/Explorer) hello 브라우저에서 합니다.
   
    ![서비스 패브릭 탐색기에서 응용 프로그램 세부 정보 보기][sfx-service-overview]
   
   > [!NOTE]
   > 서비스 패브릭 탐색기에 대해 자세히 toolearn 참조 [서비스 패브릭 탐색기를 사용 하 여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)합니다.
   > 
   > 

## <a name="upgrade-an-application"></a>응용 프로그램 업그레이드
서비스 패브릭 클러스터에 hello에서는 hello 응용 프로그램의 hello 상태를 모니터링 하면 쿼리가 가동 중지 업그레이드를 제공 합니다. Hello WordCount 응용 프로그램의 업그레이드를 수행 합니다.

hello 새 버전의 hello 응용 프로그램을 지금 함께 시작 하는 단어만 계산 합니다. Hello 업그레이드를 시작할 때 hello 응용 프로그램의 동작 변경 내용 두 개 표시 됩니다. 첫째, hello 속도 hello 수는 증가 해야 느림, 단어가 적은 계산 때문입니다. 둘째, hello 첫 번째 파티션에 두 개의 모음 (A 및 E) 하 고 다른 모든 파티션은 하나만 포함 될 각를 해당 개수 결국 시작 해야 toooutpace hello 다른 합니다.

1. [Hello WordCount 버전 2 패키지 다운로드](http://aka.ms/servicefabric-wordcountappv2) toohello hello 버전 1 패키지를 다운로드 하는 동일한 위치입니다.
2. Tooyour PowerShell 창을 반환 하 고 hello SDK 업그레이드 명령을 tooregister hello hello 클러스터에서 새 버전을 사용 합니다. 그런 다음 hello fabric 업그레이드를 시작할: / WordCount 응용 프로그램입니다.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Hello에에서 다음 출력 PowerShell 업그레이드 hello으로 시작 하는 것이 나타납니다.
   
    ![PowerShell에서 업그레이드 진행률][ps-appupgradeprogress]
3. Hello 업그레이드가 계속 동안 하는 경우가 더 쉽게 toomonitor 서비스 패브릭 탐색기에서 해당 상태입니다. 브라우저 창을 시작 하 고 너무 탐색[http://localhost:19080/탐색기](http://localhost:19080/Explorer)합니다. 확장 **응용 프로그램** hello 왼쪽에 hello 트리에서 선택 **WordCount**, 마지막으로 **패브릭: / WordCount**합니다. Hello essentials 탭 hello 클러스터의 업그레이드 도메인을 통해 진행 됨에 따라 hello hello 업그레이드 상태를 참조 합니다.
   
    ![서비스 패브릭 탐색기에서 업그레이드 진행][sfx-upgradeprogress]
   
    각 도메인을 통해 진행 될 hello 업그레이드 상태 검사는 수행된 tooensure hello 응용 프로그램이 제대로 작동 하는 합니다.
4. Hello를 다시 실행 하면 이전 hello 패브릭에서 서비스의 hello 집합에 대 한 쿼리: WordCount 응용 프로그램 hello WordCountService 버전 변경 되었지만 WordCountWebService 버전 hello 통지 하지 않았습니다. /:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![업그레이드 후 응용 프로그램 서비스 쿼리][ps-getsfsvc-postupgrade]
   
    이 예제는 Service Fabric이 응용 프로그램 업그레이드를 관리하는 방법을 보여줍니다. 유일한 hello 집합이 서비스 (또는 해당 서비스 내에서 코드/구성 패키지) 변경 된 hello 업그레이드 프로세스를 보다 빠르고 안정적 낮추는 연결 합니다.
5. 마지막으로, toohello 브라우저 tooobserve hello 동작 hello 새 응용 프로그램 버전을 반환 합니다. 예상 대로 count 진행 속도 느리게 hello 및 hello 첫 번째 파티션에 조금 더 hello 볼륨을 종료 합니다.
   
    ![Hello 브라우저에서 hello 응용 프로그램의 hello 새 버전 보기][deployed-app-ui-v2]

## <a name="cleaning-up"></a>정리
이 배치 하기 전에 로컬 클러스터 hello tooremember 실제 중요 합니다. 응용 프로그램이 제거 하기 전 까지는 hello 백그라운드에서 toorun를 계속 합니다.  응용 프로그램에서는 hello 이기에 따라 실행 중인 응용 프로그램은 컴퓨터에 중요 한 리소스를 걸릴 수 있습니다. 에 몇 가지 옵션 toomanage 응용 프로그램 및 hello 클러스터

1. tooremove 개별 응용 프로그램 및 모든의 데이터를 hello 다음 명령을 실행 합니다.
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    서비스 패브릭 탐색기 hello에서 hello 응용 프로그램을 삭제 또는 **동작** 메뉴 또는 hello 왼쪽 응용 프로그램 목록 뷰에서 hello 상황에 맞는 메뉴입니다.
   
    ![서비스 패브릭 탐색기에서 응용 프로그램 삭제][sfe-delete-application]
2. Hello 클러스터에서 hello 응용 프로그램을 삭제 한 후 버전 1.0.0 및 2.0.0 hello WordCount 응용 프로그램 종류의 등록을 취소 합니다. 삭제는 hello 코드 및 hello 클러스터 이미지 저장소에서 구성을 포함 하는 hello 응용 프로그램 패키지를 제거 합니다.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    서비스 패브릭 탐색기에서 선택 하거나 **해제 형식** hello 응용 프로그램에 대 한 합니다.
3. tooshut hello 클러스터 하지만 유지 hello 응용 프로그램 데이터와 추적을 클릭 하 여 **로컬 클러스터 중지** hello 시스템 트레이 응용 프로그램에서 합니다.
4. toodelete hello 클러스터 완전히 클릭 **로컬 클러스터 제거** hello 시스템 트레이 응용 프로그램에서 합니다. 이 옵션은 다음 Visual Studio에서 f5 키를 누를 때 다른 느린 배포 hello에 발생 합니다. 일정 시간 동안 그 또는 tooreclaim 자원이 필요한 경우 toouse 않으려는 경우에 hello 쿼럼 응답을 제거 합니다.

## <a name="one-node-and-five-node-cluster-mode"></a>1개 노드 및 5개 노드 클러스터 모드
응용 프로그램을 개발할 때 종종 코드 작성, 디버깅, 코드 변경, 디버깅을 빠르게 반복하여 수행합니다. 이 프로세스를 최적화 하는 toohelp, hello 로컬 클러스터는 두 가지 모드에서 실행할 수: 1 개 노드 또는 5 노드. 클러스터 모드는 모두 해당되는 혜택이 있습니다. 5 노드 클러스터 모드에서는 실제 클러스터 toowork 수 있습니다. 장애 조치 시나리오를 테스트하고 더 많은 인스턴스 및 서비스의 복제본을 사용할 수 있습니다. 1 개 노드 클러스터 모드가 최적화 toodo 빠른 배포 및 등록 된 서비스의 toohelp hello 서비스 패브릭 런타임을 사용 하 여 코드를 신속 하 게 유효성 검사입니다.

1개 노드 클러스터 또는 5개 노드 클러스터 모드 모두 에뮬레이터 또는 시뮬레이터가 아닙니다. hello 로컬 개발 클러스터 실행 hello 다중 컴퓨터 클러스터에 있는 동일한 플랫폼 코드입니다.

> [!WARNING]
> Hello 클러스터 모드를 변경 하는 경우에 hello 현재 클러스터 시스템에서 제거 되 고 새 클러스터를 만듭니다. hello 클러스터에 저장 된 hello 데이터 클러스터 모드를 변경 하면 삭제 됩니다.
> 
> 

toochange hello 모드 tooone-노드 클러스터를 선택 **스위치 클러스터 모드** hello 서비스 패브릭 로컬 클러스터 관리자에서에서 합니다.

![클러스터 모드 전환][switch-cluster-mode]

또는 PowerShell을 사용 하 여 hello 클러스터 모드를 변경 합니다.

1. 새 PowerShell 창을 관리자 권한으로 실행합니다.
2. Hello SDK 폴더에서 hello 클러스터 설치 스크립트를 실행 합니다.
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    클러스터 설치는 몇 분 정도 걸립니다. 설치가 완료된 후 다음과 같은 출력이 표시됩니다.
   
    ![클러스터 설정 출력][cluster-setup-success-1-node]

## <a name="next-steps"></a>다음 단계
* 미리 작성된 응용 프로그램을 배포하고 업그레이드했으니 [Visual Studio에서 응용 프로그램 빌드](service-fabric-create-your-first-application-in-visual-studio.md)를 수행해 보겠습니다.
* 이 문서의 hello 로컬 클러스터에 대해 수행 하는 모든 hello 작업에서 수행할 수는 [Azure 클러스터](service-fabric-cluster-creation-via-portal.md) 도 합니다.
* 이 문서에서 수행 했던 hello 업그레이드 기본 이었습니다. Hello 참조 [업그레이드 문서](service-fabric-application-upgrade.md) toolearn hello 강력 하며 유연성 서비스 패브릭 업그레이드 하는 방법에 대 한 자세한 합니다.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
