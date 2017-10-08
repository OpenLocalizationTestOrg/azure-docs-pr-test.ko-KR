---
title: "서비스 패브릭에서 aaaApplication 수명 주기 | Microsoft Docs"
description: "서비스 패브릭 응용 프로그램 개발, 배포, 테스트, 업그레이드, 유지 관리 및 제거를 설명합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 08837cca-5aa7-40da-b087-2b657224a097
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 36cd6081010e83cb8226c8f85d1e912ac9eebd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-lifecycle"></a>서비스 패브릭 응용 프로그램 수명 주기
다른 플랫폼에서 Azure 서비스 패브릭 응용 프로그램 보통 단계를 수행 하는 hello 처럼: 디자인, 개발, 테스트, 배포, 업그레이드, 유지 관리 및 제거 합니다. 서비스 패브릭 hello 전체 응용 프로그램 수명 주기에서 개발, 배포, 일상적인 관리 및 유지 관리 tooeventual 서비스 해제를 통해 클라우드 응용 프로그램의 기본 지원을 제공합니다. hello 서비스 모델에는 여러 가지 다양 한 역할 tooparticipate를 hello 응용 프로그램 수명 주기에서 독립적으로 수 있습니다. 이 문서는 hello Api의 개요 및 hello 단계의 hello 서비스 패브릭 응용 프로그램 수명 주기 전체에서 hello 다른 역할에서 어떻게 사용 되는지를 제공 합니다.

hello 다음 Microsoft Virtual Academy 비디오 설명 방법을 toomanage 응용 프로그램 수명:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-application-lifecycle/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="service-model-roles"></a>서비스 모델 역할
hello 서비스 모델 역할은:

* **개발자 서비스**: 용도가 변경 하 고 hello의 여러 응용 프로그램에서 사용할 수 있는 모듈식 및 일반 서비스 개발 하 고, 같은 종류나 다른 종류입니다. 예를 들어 큐 서비스를 사용하여 발권 응용 프로그램(헬프데스크) 또는 전자 상거래 응용 프로그램(장바구니)을 만들 수 있습니다.
* **응용 프로그램 개발자**: 특정 요구 사항이 나 시나리오에 특정 서비스 toosatisfy의 컬렉션을 통합 하 여 응용 프로그램을 만듭니다. 전자 상거래 웹 사이트를 사용 하 여 "JSON 상태 비저장 프런트 엔드 서비스", 수 통합 하는 예를 들어, "경매 상태 저장 서비스" 및 "큐 상태 저장 서비스" toobuild 여 경매 솔루션입니다.
* **응용 프로그램 관리자**: hello 응용 프로그램 구성 (hello 구성 템플릿 매개 변수 입력), (tooavailable 리소스 매핑), 배포 및 서비스 품질에 대 한 결정을 내립니다. 예를 들어 응용 프로그램 관리자는 hello hello 응용 프로그램의 언어 로캘 (영어 미국이 나 hello에 대 한 예를 들어 일본의 경우 일본어)을 결정합니다. 배포된 다른 응용 프로그램을 다르게 설정할 수 있습니다.
* **연산자**: hello 응용 프로그램 구성 및 응용 프로그램 관리자에 게로 지정 된 요구 사항에 따라 응용 프로그램을 배포 합니다. 예를 들어 연산자 프로 비전 및 hello 응용 프로그램을 배포 하 고 Azure에서 실행 되 고 있는지 확인 합니다. 연산자는 응용 프로그램 상태 및 성능 정보를 모니터링 하 고 필요에 따라 hello 실제 인프라 유지 관리 합니다.

## <a name="develop"></a>개발
1. A *개발자 서비스* 다양 한 유형의 hello를 사용 하 여 서비스를 개발 [Reliable Actors](service-fabric-reliable-actors-introduction.md) 또는 [신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md) 프로그래밍 모델입니다.
2. A *개발자 서비스* 하나 이상의 코드, 구성 및 데이터 패키지로 구성 된 서비스 매니페스트 파일에서 hello 개발한 서비스 형식을 선언적으로 설명 합니다.
3. 그런 다음 *응용 프로그램 개발자* 는 다른 서비스 유형을 사용하여 응용 프로그램을 빌드합니다.
4. *응용 프로그램 개발자* hello 구성 서비스의 hello 서비스 매니페스트를 참조 하 고 적절 하 게 재정의 / 매개 변수화 하 여 응용 프로그램 매니페스트에서 hello 응용 프로그램 종류를 선언적으로 설명 서로 다른 구성 및 배포 설정을 hello 구성 서비스입니다.

이에 대한 예는 [Reliable Actors 시작](service-fabric-reliable-actors-get-started.md) 및 [Reliable Services 시작](service-fabric-reliable-services-quick-start.md)을 참조하세요.

## <a name="deploy"></a>배포
1. *응용 프로그램 관리자* hello hello의 적절 한 매개 변수를 지정 하 여 응용 프로그램 종류 tooa 특정 응용 프로그램 배포 toobe tooa 서비스 패브릭 클러스터를 hello가 **스토어로**hello 응용 프로그램 매니페스트에서 요소입니다.
2. *연산자* 업로드 hello를 사용 하 여 응용 프로그램 패키지 toohello 클러스터 이미지 저장소 hello [ **CopyApplicationPackage** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) 또는 hello [  **복사 ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)합니다. hello 응용 프로그램 매니페스트 및 서비스 패키지의 hello 컬렉션 hello 응용 프로그램 패키지에 포함 되어 있습니다. 서비스 패브릭 응용 프로그램에서 Azure blob 저장소 또는 hello 서비스 패브릭 시스템 서비스는 hello 이미지 저장소에 저장 된 hello 응용 프로그램 패키지를 배포 합니다.
3. hello *연산자* 다음 hello를 사용 하 여 hello 업로드 된 응용 프로그램 패키지에서 hello 대상 클러스터에서 응용 프로그램 종류 hello를 프로 비전 [ **ProvisionApplicationAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **레지스터 ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), 또는 hello [ **응용 프로그램 프로 비전** REST작업](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
4. Hello 응용 프로그램을 프로 비전 한 후 프로그램 *연산자* 시작 hello에서 제공 하는 hello 매개 변수가 있는 응용 프로그램을 hello *응용 프로그램 관리자* hello를 사용 하 여 [  **CreateApplicationAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CreateApplicationAsync_System_Fabric_Description_ApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **새로 ServiceFabricApplication** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricapplication), 또는 hello [ **만들기 응용 프로그램** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/create-an-application)합니다.
5. Hello 응용 프로그램을 배포한 후는 *연산자* 사용 하 여 hello [ **CreateServiceAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_CreateServiceAsync_System_Fabric_Description_ServiceDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **새 ServiceFabricService** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice), 또는 hello [ **서비스 만들기** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/create-a-service) toocreate hello 응용 프로그램에 대 한 새 서비스 인스턴스 기반 사용 가능한 서비스 형식입니다.
6. hello 응용 프로그램 hello 서비스 패브릭 클러스터에서 실행 됩니다.

예는 [응용 프로그램 배포](service-fabric-deploy-remove-applications.md) 를 참조하세요.

## <a name="test"></a>테스트
1. 로컬 개발 클러스터 toohello 또는 테스트 클러스터를 배포한 후는 *개발자 서비스* 실행 hello를 사용 하 여 기본 제공 장애 조치 테스트 시나리오를 hello [ **FailoverTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenarioparameters#System_Fabric_Testability_Scenario_FailoverTestScenarioParameters) 및 [ **FailoverTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenario#System_Fabric_Testability_Scenario_FailoverTestScenario) 클래스 또는 hello [ **Invoke ServiceFabricFailoverTestScenario** cmdlet ](/powershell/module/servicefabric/invoke-servicefabricfailovertestscenario?view=azureservicefabricps). 계속 사용할 수 있고 작동 인지는 중요 한 전환 및 장애 조치 tooensure을 통해 지정된 된 서비스를 실행 하는 hello 장애 조치 테스트 시나리오.
2. hello *개발자 서비스* 실행 hello hello를 사용 하 여 기본 제공 chaos 테스트 시나리오는 다음 [ **ChaosTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenarioparameters#System_Fabric_Testability_Scenario_ChaosTestScenarioParameters) 및 [  **ChaosTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenario#System_Fabric_Testability_Scenario_ChaosTestScenario) 클래스 또는 hello [ **Invoke ServiceFabricChaosTestScenario** cmdlet](/powershell/module/servicefabric/invoke-servicefabricchaostestscenario?view=azureservicefabricps)합니다. hello chaos 테스트 시나리오는 임의로 hello 클러스터에 여러 노드, 코드 패키지 및 복제 오류를 적용 합니다.
3. hello *개발자 서비스* [서비스 간 통신 테스트](service-fabric-testability-scenarios-service-communication.md) hello 클러스터 중심 주 복제본을 이동 하는 테스트 시나리오를 작성 합니다.

참조 [소개 toohello 오류 분석 서비스](service-fabric-testability-overview.md) 자세한 정보에 대 한 합니다.

## <a name="upgrade"></a>업그레이드
1. A *개발자 서비스* hello hello 인스턴스화된 응용 프로그램의 구성 서비스를 업데이트 및/또는 버그를 수정 하 고 hello 서비스 매니페스트의 새 버전을 제공 합니다.
2. *응용 프로그램 개발자* 재정의 및 hello 구성 서비스의 구성 및 배포 설정을 hello 매개 변수화 하 고 hello 응용 프로그램 매니페스트의 새 버전을 제공 합니다. hello 응용 프로그램 개발자는 다음 hello 서비스 매니페스트의 새 버전 hello hello 응용 프로그램에 통합 하 고 업데이트 된 응용 프로그램 패키지에 대 한 hello 응용 프로그램 유형의 새 버전을 제공 합니다.
3. *응용 프로그램 관리자* hello 적절 한 매개 변수를 업데이트 하 여 hello 응용 프로그램 유형의 새 버전 hello hello 대상 응용 프로그램에 통합 합니다.
4. *연산자* 업로드 hello hello를 사용 하 여 업데이트 된 응용 프로그램 패키지 toohello 클러스터 이미지 저장소 [ **CopyApplicationPackage** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) 또는 hello [ **복사 ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)합니다. hello 응용 프로그램 매니페스트 및 서비스 패키지의 hello 컬렉션 hello 응용 프로그램 패키지에 포함 되어 있습니다.
5. *연산자* 프로 비전 hello를 사용 하 여 새 버전의 hello 대상 클러스터의 hello 응용 프로그램을 hello [ **ProvisionApplicationAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **레지스터 ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), 또는 hello [ **응용 프로그램 프로 비전** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application)합니다.
6. *연산자* 업그레이드 대상 응용 프로그램 toohello 새 버전 hello를 사용 하 여 hello [ **UpgradeApplicationAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpgradeApplicationAsync_System_Fabric_Description_ApplicationUpgradeDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **시작 ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationupgrade), 또는 hello [ **응용 프로그램 업그레이드** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/upgrade-an-application)합니다.
7. *연산자* 검사 hello hello를 사용 하 여 업그레이드의 진행률 [ **GetApplicationUpgradeProgressAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_GetApplicationUpgradeProgressAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Get ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricapplicationupgrade), 또는 hello [ **응용 프로그램 업그레이드 진행률 가져오기** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/get-the-progress-of-an-application-upgrade1)합니다.
8. 필요한 경우 hello *연산자* 수정 하 고 hello를 사용 하 여 hello 현재 응용 프로그램 업그레이드의 hello 매개 변수를 다시 적용 [ **UpdateApplicationUpgradeAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpdateApplicationUpgradeAsync_System_Fabric_Description_ApplicationUpgradeUpdateDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **업데이트 ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/update-servicefabricapplicationupgrade), 또는 hello [ **업데이트 응용 프로그램 업그레이드** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/update-an-application-upgrade).
9. 필요한 경우 hello *연산자* hello를 사용 하 여 hello 현재 응용 프로그램 업그레이드 롤백합니다 [ **RollbackApplicationUpgradeAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RollbackApplicationUpgradeAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [ **시작 ServiceFabricApplicationRollback** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationrollback), 또는 hello [ **롤백 응용 프로그램 업그레이드** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/rollback-an-application-upgrade)합니다.
10. 서비스 패브릭 업그레이드 hello 대상 응용 프로그램의 구성 요소 서비스의 가용성을 hello 그대로 유지 하면서 hello 클러스터에서를 실행 합니다.

Hello 참조 [응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md) 예입니다.

## <a name="maintain"></a>유지 관리
1. 운영 체제 업그레이드 및 패치 서비스 패브릭 hello Azure 인프라 tooguarantee 가용성 hello 클러스터에서 실행 되는 모든 hello 응용 프로그램의 상호 작용 합니다.
2. 업그레이드 및 패치와 관련 toohello 서비스 패브릭 플랫폼에 대 한 서비스 패브릭 업그레이드 자체 hello 클러스터에서 실행 되는 hello 응용 프로그램의 가용성을 유지 하면서 합니다.
3. *응용 프로그램 관리자* hello의 추가 또는 제거 하는 클러스터에서 노드 용량 사용량 데이터 및 향후의 예상된 수요를 분석 한 후 승인 합니다.
4. *연산자* 뷰에 추가 되거나 제거 hello로 지정 된 노드 *응용 프로그램 관리자*합니다.
5. Hello 클러스터에서 tooor 기존 노드를 제거 하는 새 노드를 추가, 서비스 패브릭 자동으로 부하 분산 hello hello 클러스터 tooachieve 최적의 성능의 모든 노드에서 응용 프로그램을 실행 합니다.

## <a name="remove"></a>제거
1. *연산자* hello를 사용 하 여 hello 전체 응용 프로그램을 제거 하지 않고 hello 클러스터에서 실행 중인 서비스의 특정 인스턴스를 삭제할 수 [ **DeleteServiceAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_DeleteServiceAsync_System_Fabric_Description_DeleteServiceDescription_System_TimeSpan_System_Threading_CancellationToken_) hello [ **제거 ServiceFabricService** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricservice), 또는 hello [ **서비스 삭제** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/delete-a-service)합니다.  
2. *연산자* 응용 프로그램 인스턴스 및 모든 hello를 사용 하 여 서비스 삭제할 수도 [ **DeleteApplicationAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_DeleteApplicationAsync_System_Fabric_Description_DeleteApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **제거 ServiceFabricApplication** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricapplication), 또는 hello [ **응용 프로그램 삭제** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/delete-an-application)합니다.
3. Hello 응용 프로그램 및 서비스 중지 되 면 hello *연산자* hello를 사용 하 여 hello 응용 프로그램 유형의 프로 비전 해제 수 [ **UnprovisionApplicationAsync** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UnprovisionApplicationAsync_System_String_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **등록 취소 ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype), 또는 hello [ **응용 프로그램을 프로 비전 해제** REST 작업](https://docs.microsoft.com/rest/api/servicefabric/unprovision-an-application). Hello 응용 프로그램 유형을 구축 해제 hello ImageStore에서에서 hello 응용 프로그램 패키지를 제거 하지 않습니다. Hello 응용 프로그램 패키지를 수동으로 제거 해야 합니다.
4. *연산자* 에서 제거 hello 응용 프로그램 패키지는 ImageStore hello를 사용 하 여 hello [ **RemoveApplicationPackage** 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RemoveApplicationPackage_System_String_System_String_) 또는 hello [ **제거 ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps)합니다.

예는 [응용 프로그램 배포](service-fabric-deploy-remove-applications.md) 를 참조하세요.

## <a name="next-steps"></a>다음 단계
서비스 패브릭 응용 프로그램 및 서비스의 개발, 테스트 및 관리에 대한 자세한 내용은 다음 항목을 참조하세요.

* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Reliable Services](service-fabric-reliable-services-introduction.md)
* [응용 프로그램 배포](service-fabric-deploy-remove-applications.md)
* [응용 프로그램 업그레이드](service-fabric-application-upgrade.md)
* [테스트 용이성 개요](service-fabric-testability-overview.md)
