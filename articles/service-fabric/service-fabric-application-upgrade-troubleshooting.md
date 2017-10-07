---
title: "응용 프로그램 업그레이드 aaaTroubleshooting | Microsoft Docs"
description: "이 문서에서는 서비스 패브릭 응용 프로그램을 업그레이드 주위 몇 가지 일반적인 문제 및 방법을 tooresolve 해당 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>응용 프로그램 업그레이드 문제 해결
이 문서에서는 Azure 서비스 패브릭 응용 프로그램을 업그레이드 주위 hello 일반적인 문제 중 일부와 방법을 tooresolve 해당 합니다.

## <a name="troubleshoot-a-failed-application-upgrade"></a>응용 프로그램 업그레이드 실패 문제 해결
업그레이드에 실패 한 경우, hello의 hello 출력 **Get ServiceFabricApplicationUpgrade** 명령 hello 실패 디버깅에 대 한 추가 정보를 포함 합니다.  hello 다음 목록에 지정 hello 추가 정보를 어떻게 사용할 수 있습니다.

1. Hello 오류 유형을 식별 합니다.
2. Hello 실패 이유를 식별 합니다.
3. 추가 조사를 위해 하나 이상의 오류 구성 요소를 분리합니다.

이 정보를 사용할 수 있는지 여부를 hello에 관계 없이 hello 오류를 발견 하면 서비스 패브릭 **FailureAction** tooroll 백 되었거나 hello 업그레이드를 일시 중단 합니다.

### <a name="identify-hello-failure-type"></a>Hello 실패 유형 식별
hello 출력에서 **Get ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** hello 타임 스탬프 (UTC)는 업그레이드 오류가 서비스 패브릭에서 감지 된 식별 및  **FailureAction** 트리거 되었습니다. **FailureReason** hello 실패의 세 가지 잠재적인 높은 수준의 원인 중 하나를 식별 합니다.

1. UpgradeDomainTimeout-특정 업그레이드 도메인 toocomplete 너무 오래 걸리는 시간이 길다는 것을 나타냅니다 및 **UpgradeDomainTimeout** 만료 되었습니다.
2. 전체 업그레이드는 hello toocomplete 너무 오래 걸렸습니다 OverallUpgradeTimeout-나타냅니다 및 **UpgradeTimeout** 만료 되었습니다.
3. -상태는 업데이트 도메인을 업그레이드 한 후 hello 응용 프로그램을 비정상 상태로 나타냅니다 상태 정책을 지정 toohello에 따라 및 **HealthCheckRetryTimeout** 만료 되었습니다.

이러한 항목 표시 hello 출력 hello 업그레이드가 실패 하 고 다시 시작 합니다. 자세한 hello 유형의 hello 오류에 따라 표시 됩니다.

### <a name="investigate-upgrade-timeouts"></a>업그레이드 시간 제한 조사
업그레이드 시간 제한 오류는 서비스 가용성 문제로 인해 가장 일반적으로 발생합니다. 이 단락이 다음 hello 출력이 업그레이드 서비스 복제본 또는 인스턴스가 새 코드 버전 hello에에서 toostart 실패입니다. hello **UpgradeDomainProgressAtFailure** 필드 hello 오류가 발생 한 시점에서 보류 중인 업그레이드 작업의 스냅숏을 캡처합니다.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

이 예제에서는 hello 업그레이드에서 실패 했습니다 업그레이드 도메인 *MYUD1* 및 두 개의 파티션 (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* 및 *4b43f4d8-b26b-424e-9307-7a7a62e79750*) 중단 되었습니다. hello 파티션을 hello 런타임 tooplace 수 없습니다 주 복제본 때문에 중단 되었습니다 (*WaitForPrimaryPlacement*) 대상 노드에서 *Node1* 및 *Node4*합니다.

hello **Get ServiceFabricNode** 명령은 두 노드 업그레이드 도메인에 있는 tooverify 사용된 될 수 있습니다 *MYUD1*합니다. hello *UpgradePhase* 에 따르면 *PostUpgradeSafetyCheck*, 즉, 이러한 안전 검사 hello 업그레이드 도메인의 모든 노드에서 업그레이드를 완료 한 후 발생 합니다. 이러한 모든 정보 tooa hello hello 응용 프로그램 코드의 새 버전으로 잠재적인 문제를 가리킵니다. hello 가장 일반적인 문제는 hello open 또는 프로 모션 tooprimary 코드 경로에서 서비스 오류가 발생 합니다.

*UpgradePhase* 의 *PreUpgradeSafetyCheck* 개가 다음을 수행 하기 전 hello 업그레이드 도메인을 준비 하는 문제를 의미 합니다. 이 경우 hello 가장 일반적인 문제 hello 닫기 또는 수준 내리기 주 코드 경로에서 서비스 오류가 생성 됩니다.

현재 hello **UpgradeState** 은 *RollingBackCompleted*hello 원래 업그레이드가 롤백이와 수행 해야 하므로 **FailureAction**는 자동으로 실패 시 hello 업그레이드가 롤백됩니다. 수동으로 hello 원래 업그레이드를 실행 하는 경우 **FailureAction**, hello 업그레이드 대신 것에 일시 중단 된 상태로 tooallow 라이브 hello 응용 프로그램의 디버깅 합니다.

### <a name="investigate-health-check-failures"></a>상태 확인 오류 조사
상태 확인 오류는 업그레이드 도메인의 모든 노드가 업그레이드를 완료하고 모든 안전 검사를 통과한 후 발생할 수 있는 다양한 문제로 인해 트리거될 수 있습니다. 이 단락이 다음 hello 출력이 toofailed 상태 검사 되는 업그레이드 오류가입니다. hello **UnhealthyEvaluations** 필드 hello 시점 toohello 지정에 따라 hello 업그레이드에 실패 한 상태 검사에 대 한 스냅숏을 캡처합니다 [상태 정책](service-fabric-health-introduction.md)합니다.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

상태 확인 오류를 조사 하 고 먼저 알아야 할 hello 서비스 패브릭 상태 모델입니다. 두 서비스 요소가 정상 상태 인지 확인할 수 있습니다 이러한 프로그램을 깊이 있게 이해 없이 하지만: *패브릭: / demoapp 가/Svc3* 및 *패브릭: / demoapp 가/Svc2*, hello 오류 상태 보고서 ("InjectedFault 함께 "이 경우). 이 예제에서는 2 중 4 서비스 없는 정상, 비정상 0 %hello 기본 대상 미만입니다 (*MaxPercentUnhealthyServices*).

hello 업그레이드를 일시 중지 실패 시 지정 하는 **FailureAction** 의 경우에 수동 업그레이드 hello를 시작 합니다. 이 모드 통해 추가 작업을 수행 하기 전에 tooinvestigate hello 라이브 시스템 hello 실패 상태에 있습니다.

### <a name="recover-from-a-suspended-upgrade"></a>일시 중단된 업그레이드 복구
롤백을와 **FailureAction**는 hello 업그레이드 실패 시 다시 자동 전환 되기 때문에 필요한 복구 합니다. 수동 **FailureAction**을 사용하면 몇 가지 복구 옵션이 존재합니다.

1.  롤백 트리거
2. 수동으로 hello 나머지 hello 업그레이드를 진행 합니다.
3. Resume hello 모니터링 업그레이드

hello **시작 ServiceFabricApplicationRollback** 명령은 모든 시간 toostart 롤백하는 hello 응용 프로그램에서 사용할 수 있습니다. Hello 명령이 성공적으로 반환 되 면 hello 롤백 요청이 hello 시스템에 등록 하 고 잠시 후 시작 합니다.

hello **Resume-servicefabricapplicationupgrade** 명령을 사용 하 여 tooproceed hello 나머지 hello 통해 수동으로, 한 번에 하나의 업그레이드 도메인을 업그레이드 합니다. 이 모드에서는 hello 시스템만 안전 검사를 수행 합니다. 더 이상의 상태 검사는 수행되지 않습니다. 이 명령은 경우 hello에 사용할 수 있습니다 *UpgradeState* 표시 *RollingForwardPending*, 해당 hello 현재 업그레이드 도메인을 의미 하는 업그레이드 완료 했습니다. 있지만 hello 다음 하나가 시작 되지 않았습니다 (보류 중).

hello **업데이트 ServiceFabricApplicationUpgrade** 명령을 안전 및 보건 모두 검사를 사용 하 여 사용 되는 tooresume 모니터링 hello 업그레이드 중인를 수행할 수 있습니다.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

마지막 중단 된 hello 업그레이드 도메인 및 업그레이드 동일한 매개 변수 및 앞으로 상태 정책을 사용 하 여 hello hello 업그레이드가 계속 됩니다. 필요한 경우 hello 업그레이드 매개 변수 및 hello 출력 앞에 표시 된 상태 정책을 hello hello 업그레이드를 다시 시작 하는 경우 동일한 명령에서 변경할 수 있습니다. 이 예제에서는 hello 업그레이드 hello 변수와 변경 하지 않고 hello 상태 정책을 사용 하 여 모니터링 된 모드에서 다시 시작 되었습니다.

## <a name="further-troubleshooting"></a>추가 문제 해결
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>서비스 패브릭은 지정 된 hello 따르지 상태 정책
가능한 원인 1:

서비스 패브릭 상태 평가 대 한 모든 백분율 실제 수의 엔터티 (예를 들어 복제본, 파티션 및 서비스)로 변환 하 고 toowhole 엔터티를 항상 반올림 합니다. 예를 들어 경우 hello, 최대 *MaxPercentUnhealthyReplicasPerPartition* %21이 고 서비스 패브릭 tootwo 비정상 복제본을 사용 하면 다음 5 개의 복제본 않는 (즉,`Math.Ceiling (5*0.21)`). 따라서 상태 정책도 그에 따라 설정해야 합니다.

가능한 원인 2:

상태 정책은 특정 서비스 인스턴스가 아닌 총 서비스의 백분율을 기준으로 지정됩니다. 응용 프로그램에 네 개의 하는 경우 업그레이드 하기 전에 예를 들어, 서비스 인스턴스 A, B, C 및 D, D 서비스가 정상이 아님을 여기서 하지만 거의 영향 toohello 응용 프로그램입니다. 업그레이드 및 설정 hello 매개 변수 중 비정상적인 서비스 D 알 tooignore hello 원하는 *MaxPercentUnhealthyServices* toobe 25%, A, B 및 C 가정 toobe 정상 필요 합니다.

그러나 hello 업그레이드 하는 동안 D 동안 될 수 정상 C가 비정상입니다. hello 서비스의 25%만 정상 상태가 아닌 여전히 hello 업그레이드 성공 합니다. 하지만 예기치 못한 오류 tooC 되 고 인해 4. 대신 비정상 예기치 않게 발생할 수 있습니다 이 경우 A에서 다른 서비스 유형으로 D를 모델링 B와 C 서비스 유형 마다 상태 정책을 지정 하므로 다른 비정상 비율 임계값 적용된 toodifferent 서비스 될 수 있습니다. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>응용 프로그램 업그레이드에 대 한 상태 정책을 지정 하지 않았습니다 I 하지만 hello 업그레이드 하지 지정 하는 몇 가지 제한 시간에 대 한 계속 실패 하면
Hello에서 수행 되는 상태 정책을 toohello 업그레이드 요청에 제공 되지 않습니다 *ApplicationManifest.xml* hello 현재 응용 프로그램 버전입니다. 예를 들어 버전 1.0 tooversion 2.0에서에서 X 응용 프로그램을 업그레이드 하 버전 1.0에에서 대 한 지정 된 응용 프로그램 상태 정책은 사용 됩니다. Hello 업그레이드를 위해 다른 상태 정책을 사용 하면, hello 정책 toobe hello 응용 프로그램 업그레이드 API 호출의 일부로 지정 해야 합니다. hello hello API 호출의 일부로 지정 된 정책 중에 적용 hello 업그레이드 합니다. Hello 정책 hello에 지정 된 hello 업그레이드가 완료 되 면 *ApplicationManifest.xml* 사용 됩니다.

### <a name="incorrect-time-outs-are-specified"></a>잘못된 제한 시간 지정
시간 초과가 일관되지 않게 설정될 때 어떤 문제가 발생할지 궁금할 수 있습니다. 예를 들어 있을 수 있습니다는 *UpgradeTimeout* hello 보다 작은 *UpgradeDomainTimeout*합니다. hello 그것은 오류가 반환 됩니다. 경우 hello 오류가 반환 됩니다 *UpgradeDomainTimeout* 의 hello 합계 보다 작으면 *HealthCheckWaitDuration* 및 *HealthCheckRetryTimeout*, if 또는  *UpgradeDomainTimeout* 의 hello 합계 보다 작으면 *HealthCheckWaitDuration* 및 *HealthCheckStableDuration*합니다.

### <a name="my-upgrades-are-taking-too-long"></a>업그레이드에 시간이 너무 오래 걸립니다.
업그레이드 toocomplete에 대 한 hello 시간 hello 상태 검사 및 지정 된 제한 시간에 따라 달라 집니다. 상태 검사 및 제한 시간 toocopy 데 걸리는 시간에 따라 달라 집니다, 그리고 배포 및 안정화 hello 응용 프로그램입니다. 제한 시간을 너무 촉박하게 지정하면 업그레이드에 더 많이 실패할 수 있으므로 더 긴 제한 시간으로 신중하게 시작하는 것이 바람직합니다.

Hello 제한 시간 hello 업그레이드 시간 상호 작용 하는 방법에 소개 다음과 같습니다.

업그레이드 도메인에 대한 업그레이드는 *HealthCheckWaitDuration* + *HealthCheckStableDuration*보다 빠르게 완료할 수 없습니다.

*HealthCheckWaitDuration* + *HealthCheckRetryTimeout*보다 빠르면 업그레이드 오류가 발생할 수 있습니다.

hello 업그레이드 도메인에 대 한 업그레이드 시간으로 제한 됩니다 *UpgradeDomainTimeout*합니다.  경우 *HealthCheckRetryTimeout* 및 *HealthCheckStableDuration* 가 둘 다 0이 아닌 및 hello 업그레이드 트랜잭션이 시간 초과 에다음hello응용프로그램의hello상태유지하며앞뒤로전환 *UpgradeDomainTimeout*합니다. *UpgradeDomainTimeout* hello 현재 업그레이드 도메인 시작에 대 한 시작를 한 번 계산 hello 업그레이드 합니다.

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

응용 프로그램 업그레이드를 학습 하 여 호환 되도록 어떻게 toouse [데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)합니다.

Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.
