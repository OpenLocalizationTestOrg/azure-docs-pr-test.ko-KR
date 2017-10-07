---
title: "PowerShell을 사용 하 여 aaaService 패브릭 응용 프로그램 업그레이드 | Microsoft Docs"
description: "이 문서에서는 서비스 패브릭 응용 프로그램을 배포 하 고, hello 코드를 변경 하 고, PowerShell을 사용 하 여 업그레이드 롤아웃 hello 환경을 안내 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>PowerShell을 사용하여 서비스 패브릭 응용 프로그램 업그레이드
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

hello 가장 자주 사용 되며 권장 되는 업그레이드 방법 모니터링 hello 롤링 업그레이드 합니다.  Azure 서비스 패브릭 상태 정책 집합에 따라 업그레이드 중인 hello 응용 프로그램의 hello 상태를 모니터링 합니다. 업그레이드 된 업데이트 도메인 (UD)는 hello 응용 프로그램 상태를 평가 하는 서비스 패브릭 고 toohello 다음 업데이트 도메인을 진행 하거나 hello 상태 정책에 따라 hello 업그레이드에 실패 합니다.

관리 되는 hello 또는 네이티브 Api를 사용 하 여 모니터링 된 응용 프로그램 업그레이드를 수행할 수 있습니다, PowerShell 또는 REST 합니다. Visual Studio를 사용하여 업그레이드를 수행하는 지침은 [Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md)를 참조하세요.

서비스 패브릭 모니터링 롤링 업그레이드, 응용 프로그램 관리자에 게 hello 상태 평가 정책의 hello 응용 프로그램 상태가 경우 서비스 패브릭 toodetermine을 사용 하도록 구성할 수 있습니다. 또한 관리자에 게 (예: 자동 롤백을 수행 하 고 있습니다.) hello 상태 평가 실패 하는 경우 수행 하는 hello 동작 toobe를 구성할 수 있습니다. 이 섹션은 하나는 PowerShell을 사용 하는 hello SDK 샘플에 대 한 모니터링 된 업그레이드를 안내 합니다. hello 다음 Microsoft Virtual Academy 비디오도 안내 합니다 응용 프로그램 업그레이드:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>1 단계: 빌드 및 hello 시각적 개체 예제를 배포 합니다.
작성 하 고 hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 hello 응용 프로그램을 게시 **VisualObjectsApplication,** hello를 선택 하 고 **게시** 명령입니다.  자세한 내용은 [서비스 패브릭 응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md)를 참조하세요.  또는 응용 프로그램 PowerShell toodeploy를 사용할 수 있습니다.

> [!NOTE]
> PowerShell에서 사용할 수 있습니다 hello 서비스 패브릭 명령 중 하나를 먼저 먼저 tooconnect toohello 클러스터 hello를 사용 하 여 `Connect-ServiceFabricCluster` cmdlet. 마찬가지로, 클러스터에 이미 설정 된 로컬 컴퓨터에서 해당 hello를 간주 됩니다. 에 hello 문서를 참조 [서비스 패브릭 개발 환경 설정](service-fabric-get-started.md)합니다.
> 
> 

Visual Studio에서 hello 프로젝트를 빌드한 후 hello PowerShell 명령을 사용 [복사 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy hello 응용 프로그램 패키지 toohello ImageStore 합니다. Tooverify hello 응용 프로그램 패키지를 로컬로 원할 경우 사용 하 여 hello [테스트 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet. hello 다음 단계는 hello를 사용 하 여 tooregister hello 응용 프로그램 toohello 서비스 패브릭 런타임을 [레지스터 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet. hello 마지막 단계는 hello 응용 프로그램의 인스턴스 toostart hello를 사용 하 여 [새로 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.  이러한 세 단계는 유사한 toousing hello **배포** Visual Studio에서 메뉴 항목입니다.

이제, 사용할 수 있습니다 [서비스 패브릭 탐색기 tooview hello 클러스터와 hello 응용 프로그램](service-fabric-visualizing-your-cluster.md)합니다. hello 응용 프로그램에 입력 하 여 Internet Explorer tooin를 탐색할된 수 있는 웹 서비스 [http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) hello 주소 표시줄에 있습니다.  Hello 화면 내에서 이동 부동 일부 시각적 개체에 표시 됩니다.  사용할 수는 또한 [Get ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck hello 응용 프로그램 상태입니다.

## <a name="step-2-update-hello-visual-objects-sample"></a>2 단계: 업데이트 hello 시각적 개체 샘플
1 단계에서에서 배포 된 hello 버전으로 hello 시각적 개체 회전 하지 않습니다 나타날 수 있습니다. 이 응용 프로그램 tooone hello 시각적 개체도 회전 업그레이드 해 보겠습니다.

Hello VisualObjects 솔루션 내에서 hello VisualObjects.ActorService 프로젝트를 선택 하 고 hello StatefulVisualObjectActor.cs 파일을 엽니다. 해당 파일 내에서 toohello 메서드를 이동 `MoveObject`를 주석으로 처리 `this.State.Move()`, 주석 처리를 제거 하 고 `this.State.Move(true)`합니다. 이 변경은 hello 서비스를 업그레이드 한 후 hello 개체를 회전 합니다.

또한 tooupdate hello 필요 *ServiceManifest.xml* hello 프로젝트의 파일 (아래 PackageRoot) **VisualObjects.ActorService**합니다. 업데이트 hello *CodePackage* 서비스 버전 too2.0 hello 및 hello에서 해당 줄 hello *ServiceManifest.xml* 파일입니다.
Hello Visual Studio를 사용할 수 있습니다 *매니페스트 파일 편집* hello 솔루션 toomake hello 매니페스트 파일 변경 내용에서 마우스 오른쪽 단추로 클릭 한 후 옵션입니다.

Hello 매니페스트 hello 다음과 같습니다 hello 변경 된 후 (강조 표시 된 부분 hello 변경 내용을 표시 하는 데 사용):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

이제 hello *ApplicationManifest.xml* 파일 (hello 아래 **VisualObjects** hello 중인 프로젝트 **VisualObjects** 솔루션)의 hello 업데이트tooversion2.0은 **VisualObjects.ActorService** 프로젝트. 또한 hello 응용 프로그램 버전이 1.0.0.0에서 업데이트 된 too2.0.0.0 합니다. hello *ApplicationManifest.xml* hello와 비슷한 모양의 조각을 수행 해야 합니다.

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


이제 정당한 hello를 선택 하 여 hello 프로젝트를 빌드합니다 **ActorService** 프로젝트에 다음 마우스 오른쪽 단추로 클릭 하 고 hello를 선택 하면 **빌드** Visual Studio의 옵션입니다. 선택 하는 경우 **모두 다시 빌드**, hello 코드 변경 후 모든 프로젝트에 대 한 hello 버전을 업데이트 해야 합니다. 그런 다음 패키지 hello 마우스 오른쪽 단추로 클릭 하 여 응용 프로그램을 업데이트 하는 보겠습니다 ***VisualObjectsApplication***hello 서비스 패브릭 메뉴를 선택 하 고 선택 **패키지**합니다. 이 작업을 수행하면 배포 가능한 응용 프로그램 패키지가 만들어집니다.  업데이트 된 응용 프로그램 배포 준비 toobe입니다.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>3단계: 상태 정책 결정 및 매개 변수 업그레이드
Hello를 숙지 [응용 프로그램 업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md) 및 hello [업그레이드 프로세스](service-fabric-application-upgrade.md) tooget hello 다양 한 업그레이드 매개 변수, 제한 시간, 및 적용 상태 조건 이해 . 이 연습에 대 한 hello 서비스 상태 평가 기준을 toohello 기본 설정 (이며 권장) 값을 모든 서비스 및 인스턴스 되어야 함을 의미 *정상* hello 업그레이드 후 합니다.  

그러나 hello 보겠습니다 높일 *HealthCheckStableDuration* too60 초 (있도록 hello 서비스는 20 초 이상 hello 업그레이드 toohello 진행 하기 전에 다음 업데이트 하는 도메인에 대 한 정상)입니다.  Hello 설정도 하겠습니다 *UpgradeDomainTimeout* toobe 1200 초가 고 hello *UpgradeTimeout* toobe 3000 초입니다.

마지막으로, 보겠습니다 또한 설정 hello *UpgradeFailureAction* toorollback 합니다. 이 옵션 hello 업그레이드 하는 동안 문제가 발생 하는 경우 서비스 패브릭 tooroll 백 hello 응용 프로그램 toohello 이전 버전이 필요 합니다. 따라서, (4 단계)의 hello 업그레이드를 시작할 때 hello 다음 매개 변수 지정 됩니다.

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>4단계: 업그레이드를 위한 응용 프로그램 준비
이제 hello 응용 프로그램은 기본 제공 하 고 준비 toobe 업그레이드 됩니다. 관리자로 PowerShell 창을 열고 [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps)을 입력하면 **VisualObjects**의 응용 프로그램 형식 1.0.0.0이 배포되었음을 알려줍니다.  

hello 응용 프로그램 패키지에서 사용 중이면 hello 다음 상대 경로 hello 서비스 패브릭 SDK-압축 여기서 *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*합니다. Hello 응용 프로그램 패키지가 저장 된 해당 디렉터리에 "Package" 폴더를 찾아야 합니다. Hello 타임 스탬프 tooensure hello 최신 빌드 (toomodify hello 경로도 적절 하 게 할 수 있습니다) 인지 확인 합니다.

이제 보겠습니다 복사 hello 응용 프로그램 패키지 toohello 서비스 패브릭 ImageStore (hello 응용 프로그램 패키지의 저장 위치 서비스 패브릭에서)를 업데이트 합니다. 매개 변수를 hello *ApplicationPackagePathInImageStore* hello 응용 프로그램 패키지를 찾을 수 있는 서비스 패브릭 알립니다. 업데이트 하는 hello 응용 프로그램 놓았습니다 "VisualObjects\_V2" hello 다음 (반드시 toomodify 경로 적절 하 게 다시 할 수도) 명령을 사용 합니다.

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

hello 다음 단계는 tooregister hello를 사용 하 여 수행할 수 있는 서비스 패브릭이 응용 프로그램 [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 명령:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Hello 앞의 명령은 성공 하지 못한, 경우 모든 서비스의 다시 작성 해야 할 수 있습니다. 2 단계에서에서 설명 했 듯이 tooupdate을 웹 서비스 버전도 있을 수 있습니다.

## <a name="step-5-start-hello-application-upgrade"></a>5 단계: hello 응용 프로그램 업그레이드를 시작 합니다.
이제 우리는 모든 집합 toostart hello 응용 프로그램 hello를 사용 하 여 업그레이드 [시작 ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) 명령:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


hello 응용 프로그램 이름은 hello 동일 hello에서 설명한 것 처럼 *ApplicationManifest.xml* 파일입니다. 서비스 패브릭 응용 프로그램을 업그레이드를 가져오는 이름 tooidentify이를 사용 합니다. 너무 짧은 hello 제한 시간 toobe로 설정 하면 상태 hello 문제는 오류 메시지가 발생할 수 있습니다. Toohello 문제 해결 섹션을 참조 하거나 hello 제한 시간을 늘리십시오.

이제 응용 프로그램 업그레이드 진행 hello,으로 모니터링할 수 있습니다 서비스 패브릭 탐색기를 사용 하 여 또는 hello를 사용 하 여 [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) PowerShell 명령: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

잠시 후에 PowerShell 명령 앞 hello를 사용 하 여 가져온 hello 상태 모든 업데이트 도메인 업그레이드 된 명시 해야 (완료)입니다. 및 회전 hello 브라우저 창에서 시각적 개체 시작 않은 있습니다!

버전 2 tooversion 3, 또는 버전 2 tooversion 연습으로는 1에서에서 업그레이드를 시도할 수 있습니다. 버전 2 tooversion 1에서에서 이동 업그레이드도 간주 됩니다. 사용할 제한 시간 및 상태 정책 toomake 자신을 살펴봅니다. Tooan Azure 클러스터를 배포 하는 경우 hello 매개 변수 필요성 toobe 집합 적절 하 게 합니다. 것이 좋은 tooset hello 제한 시간 신중 합니다.

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

응용 프로그램 업그레이드를 학습 하 여 호환 되도록 어떻게 toouse [데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)합니다.

Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.

toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)합니다.

