---
title: "응용 프로그램 업그레이드: 업그레이드 매개 변수 | Microsoft Docs"
description: "매개 변수 관련된 tooupgrading 상태 검사 tooperform 및 정책 tooautomatically 실행 취소 hello 업그레이드를 포함 하 여 서비스 패브릭 응용 프로그램에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>응용 프로그램 업그레이드 매개 변수
이 문서에서는 hello hello 하는 동안 적용 되는 다양 한 매개 변수는 Azure 서비스 패브릭 응용 프로그램의 업그레이드를 설명 합니다. hello 매개 변수는 hello 이름과 hello 응용 프로그램의 버전을 포함합니다. 노브 hello 시간 제한 및 hello 업그레이드 하는 동안 적용 되는 상태 검사를 제어 하는 하 고 업그레이드에 실패 하면 적용 해야 하는 hello 정책을 지정 합니다.

<br>

| 매개 변수 | 설명 |
| --- | --- |
| ApplicationName |업그레이드 중인 hello 응용 프로그램의 이름입니다. 예: fabric:/VisualObjects, fabric:/ClusterMonitor |
| TargetApplicationTypeVersion |업그레이드 대상 hello hello 응용 프로그램 종류의 hello 버전입니다. |
| FailureAction |서비스 패브릭 hello 업그레이드 실패 시 수행 하는 hello 동작 합니다. hello 응용 프로그램 롤백될 수 있습니다 (롤백) toohello 업데이트 이전 버전 또는 hello 업그레이드 hello 현재 업그레이드 도메인에서 중지 될 수 있습니다. 후자의 경우 hello hello 업그레이드 모드는 변경 된 tooManual 수도 있습니다. 허용되는 값은 Rollback 및 Manual입니다. |
| HealthCheckWaitDurationSec |서비스 패브릭 hello 응용 프로그램의 hello 상태를 반환 하기 전에 hello 업그레이드 후 초 단위로 시간 toowait hello hello 업그레이드 도메인에서 완료 했습니다. 이 기간 동안 정상 간주 될 수 있습니다 전에 응용 프로그램을 실행 해야 하는 hello 시간으로 간주할 수도 있습니다. Hello 상태 검사를 통과 하는 경우 다음 업그레이드 도메인 toohello hello 업그레이드 프로세스에 진행 됩니다.  Hello 상태 검사가 실패 한 경우 hello HealthCheckRetryTimeout에 도달할 때까지 다시 hello 상태 검사를 다시 시도 하기 전에 서비스 패브릭 (hello UpgradeHealthCheckInterval) 간격 동안 대기 합니다. hello 기본 및 권장 되는 값은 0 초입니다. |
| HealthCheckRetryTimeoutSec |hello 기간 (초) 서비스 패브릭 hello 업그레이드를 실패 한 것으로 선언 하기 전에 tooperform 상태 평가 진행 하는입니다. hello 기본값은 600 초입니다. 이 소요 시간은 HealthCheckWaitDuration이 도달한 후 시작합니다. 이 HealthCheckRetryTimeout 내에서 서비스 패브릭 hello 응용 프로그램의 상태 여러 상태 검사를 수행할 수 있습니다. hello 기본값은 10 분 및 응용 프로그램에 대해 적절 하 게 사용자 지정할 합니다. |
| HealthCheckStableDurationSec |hello 기간 (초) tooverify hello 응용 프로그램 이동 toohello 다음 업그레이드 도메인 전에 안정적이 지 또는 업그레이드 hello를 완료 합니다. 이 대기 기간은 상태 변경을 발견 되지 않은 사용 되는 tooprevent hello 상태 검사를 수행한 후입니다. hello 기본값은 120 초 및 응용 프로그램에 대해 적절 하 게 사용자 지정할 합니다. |
| UpgradeDomainTimeoutSec |단일 업그레이드 도메인을 업그레이드 하는 최대 시간(초)입니다. 이 시간 제한에 도달 하면 hello 업그레이드가 중지 하 고 UpgradeFailureAction에 대 한 hello 설정에 따라 진행 됩니다. hello 기본값은 없습니다 (무한) 사용자 지정 해야 적절 하 게 응용 프로그램 및입니다. |
| UpgradeTimeout |제한 시간 (초) hello 전체 업그레이드에 적용 되는 합니다. 이 시간 제한에 도달 하면 업그레이드가 중지 되 hello를 UpgradeFailureAction 트리거됩니다. hello 기본값은 없습니다 (무한) 사용자 지정 해야 적절 하 게 응용 프로그램 및입니다. |
| UpgradeHealthCheckInterval |hello 주파수 hello 상태 상태를 확인 합니다. 이 매개 변수는 hello hello ClusterManager 섹션에에서 지정 된 *클러스터* *매니페스트*, hello 업그레이드 cmdlet의 일부로 지정 하지 않았습니다. hello 기본값은 60 초입니다. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>응용 프로그램을 업그레이드 하는 동안 서비스 상태 평가
<br>
hello 상태 평가 기준이 선택적입니다. 업그레이드를 시작할 때 hello 상태 평가 기준이 지정 되지 않은 경우 서비스 패브릭 hello 응용 프로그램 인스턴스의 ApplicationManifest.xml hello에 지정 된 hello 응용 프로그램 상태 정책을 사용 합니다.

<br>

| 매개 변수 | 설명 |
| --- | --- |
| ConsiderWarningAsError |기본값은 False입니다. 업그레이드 하는 동안 hello 응용 프로그램의 hello 상태를 평가할 때 hello hello 응용 프로그램에 대 한 상태 이벤트를 경고를 오류로 처리 합니다. 기본적으로 서비스 패브릭 hello 업그레이드 경고 이벤트가 없는 경우에 계속 될 수 있도록 경고 상태 이벤트 toobe 오류 (오류)을 평가 하지 않습니다. |
| MaxPercentUnhealthyDeployedApplications |기본 및 권장값은 0입니다. Hello 배포 된 응용 프로그램의 최대 수를 지정 (hello 참조 [상태 섹션](service-fabric-health-introduction.md)) 일 수 있는 하지 정상 hello 응용 프로그램은 비정상 상태로 간주 되 고 실패 hello 업그레이드 하기 전에. 이 매개 변수 hello 노드에서 hello 응용 프로그램 상태를 정의 하 고 업그레이드 하는 동안 문제를 검색 하는 데 도움이 됩니다. 일반적으로 hello 응용 프로그램의 hello 복제본 hello 응용 프로그램 tooappear 정상 hello 업그레이드 tooproceed 수 있도록 허용 하는 다른 노드를 부하 분산 된 toohello를 가져옵니다. 엄격한 MaxPercentUnhealthyDeployedApplications 상태를 지정 하 여 서비스 패브릭 hello 응용 프로그램 패키지와 문제를 신속 하 게 검색 하 고 빠른 업그레이드는 실패를 작성할 수 있도록 수 있습니다. |
| MaxPercentUnhealthyServices |기본 및 권장값은 0입니다. 할 수 있는 정상 hello 응용 프로그램 비정상으로 간주 하 고 hello 업그레이드 실패 하기 전에 hello 응용 프로그램 인스턴스에 hello 최대 서비스 수를 지정 합니다. |
| MaxPercentUnhealthyPartitionsPerService |기본 및 권장값은 0입니다. 할 수 있는 정상 hello 서비스 비정상 간주 되기 전에 서비스의 hello 최대 파티션 수를 지정 합니다. |
| MaxPercentUnhealthyReplicasPerPartition |기본 및 권장값은 0입니다. 파티션의 할 수 있는 정상 hello 파티션 비정상 간주 되기 전에 hello 최대 복제본 수를 지정 합니다. |
| UpgradeReplicaSetCheckTimeout |**상태 비저장 서비스**-단일 업그레이드 도메인 내에서 서비스 패브릭 tooensure hello 서비스의 추가 인스턴스를 사용할 수 있는지를 시도 합니다. Hello 대상 인스턴스 수는 둘 이상의 서비스 패브릭 tooa 최대 시간 제한 값을 사용할 수 있는 둘 이상의 인스턴스 toobe 기다립니다. 이 제한 시간은 hello UpgradeReplicaSetCheckTimeout 속성을 사용 하 여 지정 됩니다. Hello 제한 시간이 만료 되 면 서비스 패브릭 서비스 인스턴스 hello 수에 관계 없이 hello 업그레이드도 진행 됩니다. Hello 대상 인스턴스 수가 1 인 경우 서비스 패브릭 대기 하지 않고 하 고 즉시 hello 업그레이드 진행 됩니다. **상태 저장 서비스**-단일 업그레이드 도메인 내에서 서비스 패브릭 시도 복제본 hello tooensure 집합에 쿼럼이 있습니다. 서비스 패브릭 tooa 최대 시간 제한 값 (hello UpgradeReplicaSetCheckTimeout 속성으로 지정 됨)을 사용할 수는 쿼럼 toobe 기다립니다. Hello 제한 시간이 만료 되 면 서비스 패브릭 쿼럼에 관계 없이 hello 업그레이드도 진행 됩니다. 이 설정은 롤포워드 시 사용 안 함(무한)으로 설정되고, 롤백 시 900초로 설정됩니다. |
| ForceRestart |Hello 서비스 코드를 업데이트 하지 않고 구성 또는 데이터 패키지를 업데이트 하는 경우 hello ForceRestart 속성 tootrue 설정한 경우에 hello 서비스 다시 시작 됩니다. 경우 hello 업데이트가 완료 되 면 서비스 패브릭이를 알리며 hello 서비스는 새 구성 패키지 또는 데이터 패키지를 사용할 수 있습니다. hello 서비스는 hello 변경 내용을 적용 하는 일을 담당 합니다. 필요한 경우 hello 서비스 수 자체적으로 다시 시작 합니다. |

<br>
<br>
응용 프로그램 인스턴스에 대 한 서비스 유형당 hello MaxPercentUnhealthyServices, MaxPercentUnhealthyPartitionsPerService, 및 MaxPercentUnhealthyReplicasPerPartition 조건은 지정할 수 있습니다. 이러한 매개 변수 서비스 당 설정에서는 응용 프로그램 toocontain 다른 서비스에 대 한 형식을 서로 다른 평가 정책 사용 하 여 있습니다. 예를 들어, 상태 비저장 게이트웨이 서비스 형식은 특정 응용 프로그램 인스턴스에 대한 상태 저장 엔진 서비스 형식과는 다른 MaxPercentUnhealthyPartitionsPerService를 가집니다.

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Linux에서 Service Fabric CLI를 사용하여 응용 프로그램 업그레이드](service-fabric-application-lifecycle-sfctl.md#upgrade-application)에서는 Service Fabric CLI를 사용하여 응용 프로그램 업그레이드를 진행하는 과정을 안내합니다.

[Service Fabric Eclipse 플러그 인을 사용하여 응용 프로그램 업그레이드](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

응용 프로그램 업그레이드를 학습 하 여 호환 되도록 어떻게 toouse [데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)합니다.

Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.

toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)합니다.
