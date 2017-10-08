---
title: "Azure 서비스 패브릭 응용 프로그램 관리 aaaAutomate | Microsoft Docs"
description: "PowerShell을 사용하여 서비스 패브릭 응용 프로그램 배포, 업그레이드, 테스트 및 제거"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>PowerShell을 사용 하 여 hello 응용 프로그램 수명 주기를 자동화 합니다.
여러 가지 hello [서비스 패브릭 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md) 자동화할 수 있습니다.  이 문서에서는 toouse PowerShell tooautomate 일반 배포, 업그레이드, 제거 및 Azure 서비스 패브릭 응용 프로그램 테스트에 대 한 작업 하는 방법을 보여 줍니다.  앱 관리를 위한 관리되는 API 및 HTTP API도 사용 가능합니다. 자세한 내용은 [앱 수명 주기](service-fabric-application-lifecycle.md) 를 참조하세요.  

## <a name="prerequisites"></a>필수 조건
Hello 문서의 toohello 작업을 이동 하기 전에 야 합니다.

* 에 설명 된 hello 서비스 패브릭 개념을 잘 알고 [서비스 패브릭의 기술 개요](service-fabric-technical-overview.md)합니다.
* [Hello 런타임, SDK 및 도구 설치](service-fabric-get-started.md), hello 설치 **ServiceFabric** PowerShell 모듈입니다.
* [PowerShell 스크립트 실행을 활성화](service-fabric-get-started.md#enable-powershell-script-execution)합니다.
* 로컬 클러스터를 시작합니다.  관리자 권한으로 새 PowerShell 창을 시작 하 고 hello SDK 폴더에서 hello 클러스터 설치 스크립트를 실행 하십시오.`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* 이 문서에는 PowerShell 명령을 실행 하기 전에 먼저 연결 toohello 로컬 서비스 패브릭 클러스터를 사용 하 여 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* 작업을 수행 하는 hello v1 응용 프로그램 패키지 toodeploy 및 v2 응용 프로그램 패키지를 업그레이드 해야 합니다. Hello 다운로드 [ **WordCount** 샘플 응용 프로그램](http://aka.ms/servicefabricsamples) (hello Getting Started 샘플에 있음). 빌드하고 Visual Studio에서 hello 응용 프로그램 패키지 (마우스 오른쪽 단추로 클릭 **WordCount** 솔루션 탐색기에서 선택 **패키지**). Hello v1 패키지에서 복사 `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` 너무`C:\Temp\WordCount`합니다. 복사 `C:\Temp\WordCount` 너무`C:\Temp\WordCountV2`, 업그레이드에 대 한 hello v2 응용 프로그램 패키지 만들기. 텍스트 편집기에서 `C:\Temp\WordCountV2\ApplicationManifest.xml` 파일을 엽니다. Hello에 **ApplicationManifest** 요소, 변경 hello **ApplicationTypeVersion** 너무 "1.0.0"에서 특성 "2.0.0" tooupdate hello 응용 프로그램 버전 번호입니다. 변경 하는 hello ApplicationManifest.xml 파일을 저장 합니다.

## <a name="task-deploy-a-service-fabric-application"></a>작업: 서비스 패브릭 응용 프로그램 배포
사용자 작성 하 고 hello 응용 프로그램 패키지 (하거나 hello 응용 프로그램 패키지를 다운로드 한)을 후에 로컬 서비스 패브릭 클러스터에 hello 응용 프로그램을 배포할 수 있습니다. 배포, hello 응용 프로그램 패키지를 업로드 하 고, hello 응용 프로그램 종류를 등록 하 고, hello 응용 프로그램 인스턴스를 만드는 포함 됩니다. 이 섹션 toodeploy 새 응용 프로그램 tooa 클러스터의에서 hello 지침을 사용 합니다.

### <a name="step-1-upload-hello-application-package"></a>1 단계: hello 응용 프로그램 패키지 업로드
Hello 응용 프로그램 패키지 toohello 업로드 이미지 저장소에에서 배치 위치 액세스할 수 있는 toointernal 서비스 패브릭 구성 요소입니다.  hello 필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드, 구성 및 데이터 패키지 toocreate hello 응용 프로그램 및 서비스 인스턴스 hello 응용 프로그램 패키지에 포함 되어 있습니다. Tooverify hello 응용 프로그램 패키지를 로컬로 원할 경우 사용 하 여 hello [테스트 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.  hello [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 업로드 패키지 hello 명령입니다. 예:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>2 단계: hello 응용 프로그램 형식 등록
Hello 응용 프로그램 패키지를 등록 하면 hello 응용 프로그램 종류 및 버전을 사용 하기 위해 사용할 수 있는 hello 응용 프로그램 매니페스트에 선언 있습니다. hello 시스템 hello 1 단계에서 업로드 하는 hello 패키지를 읽고, hello 패키지 확인 (해당 toorunning [테스트 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) 로컬로), hello 패키지 콘텐츠를 처리 하 고 처리 하는 hello 패키지 tooan 복사 내부 시스템 위치입니다.  Hello 실행 [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
hello를 실행 하는 hello 클러스터에 등록 된 모든 hello 응용 프로그램 종류 toosee [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>3 단계: hello 응용 프로그램 인스턴스 만들기
응용 프로그램에 hello를 사용 하 여 성공적으로 등록 된 모든 응용 프로그램 종류 버전을 사용 하 여 인스턴스화할 수 [새로 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) 명령입니다. hello 각 응용 프로그램의 이름이 선언에서 시간을 배포 하 고 hello로 시작 해야 **패브릭:** 구성표 및 각 응용 프로그램 인스턴스에 대해 고유 해야 합니다. hello 응용 프로그램 유형 이름 및 응용 프로그램 종류 버전에에서도 선언 됩니다 hello **ApplicationManifest.xml** hello 응용 프로그램 패키지의 파일입니다. 기본 서비스는 hello 대상 응용 프로그램 종류의 응용 프로그램 매니페스트 hello에에서 정의 된,이 이번에 생성 됩니다 하는 것입니다.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 명령은 각각의 전반적인 상태와 함께 성공적으로 생성 된 모든 응용 프로그램 인스턴스를 나열 합니다. hello [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) hello 서비스 인스턴스는 특정된 응용 프로그램 인스턴스 내에서 성공적으로 생성 된 모든 명령을 나열 합니다. 기본 서비스(있는 경우)가 나열됩니다.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>작업: 서비스 패브릭 응용 프로그램 업그레이드
업데이트된 응용 프로그램 패키지를 사용하여 이전에 배포된 서비스 패브릭 응용 프로그램을 업그레이드할 수 있습니다. 이 작업에 배포 된 hello WordCount 응용 프로그램 업그레이드 "작업: 서비스 패브릭 응용 프로그램을 배포 합니다." 자세한 내용은 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md) 를 읽어보세요.

이 예제에서는 응용 프로그램 버전 번호만 hello에 대 한 가지 간단한 tookeep hello WordCountV2 hello 필수 구성 요소에서 만든 패키지를 응용 프로그램에서 업데이트 되었습니다. 보다 실제적인 시나리오는 서비스 코드, 구성 또는 데이터 파일을 업데이트 한 다음 다시 작성 및 업데이트 된 버전 번호를 가진 hello 응용 프로그램 패키지에 포함 됩니다.  

### <a name="step-1-upload-hello-updated-application-package"></a>1 단계: hello 업데이트 된 응용 프로그램 패키지 업로드
hello WordCount v1 응용 프로그램은 업그레이드 준비 toobe입니다. 관리자 및 형식으로 PowerShell 창을 열 경우 [ **Get ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), 해당 버전 1.0.0 hello WordCount 응용 프로그램 종류의 배포를 표시 합니다.  

이제 복사 hello (hello 응용 프로그램 패키지의 저장 위치 서비스 패브릭에서) 응용 프로그램 패키지 toohello 서비스 패브릭 이미지 저장소를 업데이트 합니다. 매개 변수를 hello **ApplicationPackagePathInImageStore** hello 응용 프로그램 패키지를 찾을 수 있는 서비스 패브릭 알립니다. 다음 명령을 복사 응용 프로그램 패키지를 너무 hello hello**WordCountV2** hello 이미지 저장소에서:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>2 단계: 레지스터 hello 업데이트 응용 프로그램 종류
hello 다음 단계는 tooregister hello 새 버전의 hello를 사용 하 여 수행할 수 있는 서비스 패브릭 응용 프로그램 hello [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>3 단계: hello 업그레이드를 시작 합니다.
다양 한 업그레이드 매개 변수, 제한 시간 및 상태 기준이 적용된 tooapplication 업그레이드 될 수 있습니다. Hello 자세히 읽고 [응용 프로그램 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 및 [업그레이드 프로세스](service-fabric-application-upgrade.md) toolearn 자세한에 대해 설명 합니다. 모든 서비스 및 인스턴스 있어야 *정상* hello 업그레이드 후 합니다.  집합 hello **HealthCheckStableDuration** too60 초 (있도록 hello 서비스는 20 초 이상 hello 업그레이드 toohello 진행 하기 전에 다음 업그레이드 도메인에 대 한 정상)입니다.  또한 집합 hello **UpgradeDomainTimeout** too1200 시간 (초) 및 hello **UpgradeTimeout** too3000 초입니다. 마지막으로 hello를 설정 **UpgradeFailureAction** 너무**롤백**, 어떤 업그레이드 하는 동안 오류가 발생 하는 경우 서비스 패브릭 롤백하는 요청 hello 응용 프로그램 toohello 이전 버전입니다.

Hello를 사용 하 여 hello 응용 프로그램 업그레이드를 시작할 수 있습니다 [시작 ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

해당 hello 응용 프로그램 이름을 hello v1.0.0 응용 프로그램 이름을 이전에 배포 하는 대로 동일 hello는 참고 (패브릭: / WordCount). 서비스 패브릭 응용 프로그램을 업그레이드를 가져오는 이름 tooidentify이를 사용 합니다. 너무 짧은 hello 제한 시간 toobe로 설정 하면 상태 hello 문제는 시간 초과 오류 메시지가 발생할 수 있습니다. 너무 참조[응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md), 하거나 hello 제한 시간을 늘리십시오.

### <a name="step-4-check-upgrade-progress"></a>4단계: 업그레이드 진행률 확인
사용 하 여 응용 프로그램 업그레이드 진행률을 모니터링할 수 있습니다 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md), 또는 hello를 사용 하 여 [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

잠시 후에 hello [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet 모든 업그레이드 도메인 업그레이드 된 보여 줍니다 (완료)입니다.

## <a name="task-test-a-service-fabric-application"></a>작업: 서비스 패브릭 응용 프로그램 테스트
toowrite 고품질 서비스 개발자 toobe 수 tooinduce 신뢰할 수 없는 인프라 오류 tootest hello의 안정성 들이 서비스를 필요합니다. 서비스 패브릭에서는 개발자가 hello 기능 tooinduce 오류 동작 및 hello 현재 상태를 사용 하 여 실패의 테스트 서비스 hello 테스트 시나리오 chaos 및 장애 조치 합니다.  자세히 읽고 [소개 toohello 오류 분석 서비스](service-fabric-testability-overview.md) 추가 정보에 대 한 합니다.

### <a name="step-1-run-hello-chaos-test-scenario"></a>1 단계: hello chaos 테스트 시나리오를 실행합니다.
hello chaos 테스트 시나리오 hello 전체 서비스 패브릭 클러스터 전체에서 오류를 생성 합니다. hello 시나리오는 일반적으로 볼 수 개월 또는 수 년 tooa 위에 몇 시간 오류를 압축 합니다. 높은 오류 속도와 인터리브된 오류의 hello 조합은 그렇지 않은 경우 누락 됩니다 코너 케이스를 찾습니다. hello 다음 예제에서는 실행 hello chaos 테스트 시나리오 60 분이 소요 됩니다.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>2 단계: hello 장애 조치 테스트 시나리오를 실행합니다.
영향을 받지 않은 다른 서비스를 벗어나 및 hello 장애 조치 hello 전체 클러스터 대신 특정 서비스 파티션을 대상 시나리오를 테스트 합니다. hello 시나리오는 비즈니스 논리 실행 되는 동안 서비스 유효성 검사에서 시뮬레이션 된 오류의 시퀀스를 반복 합니다. 서비스 유효성 검사에서 오류가 발생하면 추가 조사가 필요한 문제가 있다는 의미입니다. 여러 오류를 유도할 수 있는 것과 반대로 toohello chaos 테스트 시나리오와 한 번에 하나의 오류를 적용 하는 hello 장애 조치 테스트 합니다. hello 다음 예제에서는 테스트를 실행 hello 장애 조치 60 분 동안 hello 패브릭에 대해: / WordCount/WordCountService 서비스입니다.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>작업: 서비스 패브릭 응용 프로그램 제거
배포 된 응용 프로그램의 인스턴스를 삭제, hello 클러스터에서 프로 비전 하는 hello 응용 프로그램 종류를 제거 하 고 hello ImageStore에서에서 hello 응용 프로그램 패키지를 제거할 수 있습니다.

### <a name="step-1-remove-an-application-instance"></a>1단계: 응용 프로그램 인스턴스 제거
응용 프로그램 인스턴스가 필요 하지 않은 경우 제거할 수 없습니다 영구적으로 hello를 사용 하 여 [제거 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. 이 서비스의 모든 상태를 영구적으로 제거 toohello 응용 프로그램에 속한 모든 서비스를 자동으로 제거 됩니다. 이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>2 단계: 응용 프로그램 종류 hello 등록 취소
응용 프로그램 종류의 특정 버전을 더 이상 해야 하는 경우 등록을 취소 hello를 사용 하 여 [등록 취소 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. 등록을 취소 사용 되지 않는 형식 버전에서 사용한 저장 공간이 hello 이미지 저장소에 hello 응용 프로그램 패키지입니다. 응용 프로그램 형식은 이에 대해 인스턴스화된 응용 프로그램이나 이를 참조하는 보류 중인 응용 프로그램이 없는 한 등록 취소할 수 있습니다.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>3 단계: hello 응용 프로그램 패키지를 제거 합니다.
Hello 응용 프로그램 패키지를 hello를 사용 하 여 hello 이미지 저장소에서 제거할 수 hello 응용 프로그램 종류를 등록 취소 한 후 [제거 ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>다음 단계
[서비스 패브릭 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)

[응용 프로그램 배포](service-fabric-deploy-remove-applications.md)

[응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

[Azure Service Fabric cmdlet](/powershell/azure/overview?view=azureservicefabricps)

