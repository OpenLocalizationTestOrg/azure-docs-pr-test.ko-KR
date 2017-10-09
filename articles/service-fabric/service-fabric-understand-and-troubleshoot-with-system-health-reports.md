---
title: "시스템 상태 보고서와 aaaTroubleshoot | Microsoft Docs"
description: "클러스터 문제 해결 또는 응용 프로그램 문제에 대 한 Azure 서비스 패브릭 구성 요소 및 해당 사용 하 여 전송 된 hello 상태 보고서에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>시스템 상태 보고서 tootroubleshoot를 사용 하 여
Azure 서비스 패브릭 구성 요소 hello 초기에 보고서 hello 클러스터의 모든 엔터티가 됩니다. hello [상태 저장소](service-fabric-health-introduction.md#health-store) 만들고 hello 시스템 보고서를 기반으로 엔터티를 삭제 합니다. 또한 엔터티 상호 작용을 캡처하는 계층 구조에서 보고서를 구성합니다.

> [!NOTE]
> toounderstand 상태 관련 개념에서 자세한 내용을 [서비스 패브릭 상태 모델](service-fabric-health-introduction.md)합니다.
> 
> 

시스템 상태 보고서는 상태를 통해 클러스터 및 응용 프로그램의 기능 및 플래그 문제에 대한 가시성을 제공합니다. 응용 프로그램 및 서비스에 대 한 시스템 상태 보고서 엔터티 구현 되 고 hello 서비스 패브릭 관점에서에서 제대로 동작을 확인 합니다. hello 보고서 hello 서비스의 비즈니스 논리 hello 또는 검색 응답 하지 않는 프로세스의 상태 모니터링을 제공 하지 않습니다. 사용자 서비스 정보 특정 tootheir 논리를 사용 하 여 hello 상태 데이터를 보강할 수 있습니다.

> [!NOTE]
> Watchdogs 상태 보고서는 볼 수만 *후* hello 시스템 구성 요소는 엔터티를 만듭니다. 엔터티가 삭제 된 hello 상태 저장소 연결 된 모든 상태 보고서를 자동으로 삭제 합니다. hello 같은 기준이 hello 엔터티의 새 인스턴스를 만들 때 (예를 들어 새 지속된 서비스 상태 저장 복제본 인스턴스를 만들 됩니다). Hello 이전 인스턴스와 연결 된 모든 보고서는 삭제 하 고 hello 저장소에서 정리 됩니다.
> 
> 

hello 시스템 구성 요소 보고서로 식별 됩니다 hello로 시작 하는 hello 소스 "**시스템.**" 식별됩니다. 잘못 된 매개 변수가 있는 보고서는 거부로 watchdogs hello 소스에 관계에 대 한 접두사를 사용할 수 없습니다.
일부 시스템에 보고 toounderstand 원인 하 고 나타내는 toocorrect hello 문제가 발생 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 서비스 패브릭 tooadd hello 클러스터 및 응용 프로그램에서 일어나는에 대 한 가시성을 개선 하는의 관심 조건에는 보고서를 계속 합니다. 기존 보고서 향상 될 수 있습니다 더 자세한 설명이 나옵니다 toohelp 문제를 해결 hello 속도가 빨라집니다.
> 
> 

## <a name="cluster-system-health-reports"></a>클러스터 시스템 상태 보고서
hello 클러스터 상태 엔터티 hello health store에서 자동으로 만들어집니다. 모든 것이 제대로 작동하면 시스템 보고서는 없습니다.

### <a name="neighborhood-loss"></a>환경 손실
**System.Federation** 은 환경 손실을 감지하면 오류를 보고합니다. 개별 노드에서 hello 보고서 이며 hello 속성 이름에 hello 노드 ID가 포함 됩니다. 한 환경에서 전체 서비스 패브릭 링 hello 무시할 경우에 일반적으로 두 개의 이벤트 (hello 간격이 보고서의 양쪽 모두)을 예상할 수 있습니다. 더 많은 환경이 손실된 경우 더 많은 이벤트가 있습니다.

hello 보고서 toolive hello 시간으로 hello 글로벌 임대 제한 시간을 지정합니다. hello 조건이 활성 상태로 hello 보고서에 대 한 hello TTL 기간 중 모든 절반 다시 보내집니다. hello 이벤트 만료 될 때 자동으로 제거 됩니다. 만료 된 동작은 hello 보고서는 정리 되도록 hello health store에서 올바르게 hello 보고 노드가 다운 되는 경우에 보장 하는 경우 제거 합니다.

* **SourceId**: System.Federation
* **Property**: **환경**으로 시작되고 노드 정보를 포함합니다.
* **다음 단계**: hello 환경 (예: 클러스터 노드 간 검사 hello 통신) 손실 된 이유를 조사 합니다.

## <a name="node-system-health-reports"></a>노드 시스템 상태 보고서
**System.FM**, 클러스터 노드에 대 한 정보를 관리 하는 hello 기관이 hello Failover Manager service를 나타내는입니다. 모든 노드는 상태를 보여주는 System.FM로부터 하나의 보고서를 가져야 합니다. hello 노드 상태 제거 되 면 hello 노드 엔터티가 제거 됩니다 (참조 [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>노드 위/아래
System.FM은 hello 노드 (실행은) hello 링을 조인 하는 경우 ' 확인 '으로 보고 합니다. Hello 노드 필수 hello 링 하는 경우에 오류를 보고 (인지 하나를 업그레이드 하기 위한 단순히 실패 했기 때문에). hello 상태 저장소에 의해 작성 된 상태 계층 구조의 hello System.FM 노드 보고서와의 상관 관계의 배포 된 엔터티에 작업을 수행 합니다. Hello 노드는 모든 배포 된 가상 부모 간주합니다. hello 노드 위로 System.FM, hello로 동일한 인스턴스 hello 엔터티와 연결 된 hello 인스턴스로 보고 하는 경우 해당 노드에 배포 된 hello 엔터티 쿼리를 통해 노출 됩니다. Hello 상태 저장소를 System.FM를 보고할 때 해당 hello 노드가 다운 되거나 (새 인스턴스)를 다시 시작에 hello 이전 인스턴스의 hello 노드 또는 노드 아래로 hello에 대해서만 존재할 수 있는 배포 된 hello 엔터티를 자동으로 정리 합니다.

* **SourceId**: System.FM
* **Property**: State
* **다음 단계**: hello 노드 업그레이드를 위한 다운 되는 경우 그 해야 상태가 업그레이드 되 면입니다. 이 경우 hello 상태 백 tooOK 전환 해야 합니다. Hello 노드 다시 제공 되지 않았거나 실패 하면 그 hello 문제 추가 조사가 필요 합니다.

hello 다음 예제에서는 표시 노드에 대 한 확인의 성능 상태를 사용 하 여 hello System.FM 이벤트:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>인증서가 만료
**System.FabricNode** hello 노드에서 사용 하는 인증서 만료 나갈 때 경고를 보고 합니다. 노드당 **Certificate_cluster**, **Certificate_server** 및 **Certificate_default_client**의 3가지 인증서가 있습니다. Hello 만료 적어도 2 주 후 이면 hello 보고서 상태 확인입니다. Hello 만료 2 주 내에 있으면 hello 보고서 종류는 경고입니다. 이러한 이벤트의 TTL 제한 되어 노드 hello 클러스터를 벗어날 때 제거 됩니다.

* **SourceId**: System.FabricNode
* **속성**:로 시작 **인증서** hello 인증서 종류에 대 한 자세한 정보를 포함 하 고
* **다음 단계**: 만료 있더라도 hello 인증서를 업데이트 합니다.

### <a name="load-capacity-violation"></a>부하 용량 위반
서비스 패브릭 부하 분산 장치 hello 노드 용량 위반을 검색 하는 경우 경고를 보고 합니다.

* **SourceId**: System.PLB
* **Property**: **용량**으로 시작합니다.
* **다음 단계**: 검사 hello 노드에서 hello 현재 용량 메트릭 및 보기를 제공 합니다.

## <a name="application-system-health-reports"></a>응용 프로그램 시스템 상태 보고서
**System.CM**, hello 클러스터 관리자 서비스를 나타내는, 응용 프로그램에 대 한 정보를 관리 하는 hello 기관이입니다.

### <a name="state"></a>시스템 상태
System.CM로 보고 확인 hello 응용 프로그램 생성 또는 업데이트 된 때 합니다. 알립니다 hello 상태 저장소를 hello 응용 프로그램 삭제 된 경우 저장소에서 제거할 수 있도록 합니다.

* **SourceId**: System.CM
* **Property**: State
* **다음 단계**: hello 응용 프로그램 생성 또는 업데이트 된 경우 hello 클러스터 관리자 상태 보고서를 포함 해야 합니다. 그렇지 않은 경우 쿼리를 실행 하 여 hello 응용 프로그램의 hello 상태를 확인 (예를 들어 PowerShell cmdlet을 hello **Get ServiceFabricApplication ApplicationName *applicationName***).

hello 다음 예제에서는 hello 상태 이벤트 hello **패브릭: / WordCount** 응용 프로그램:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>서비스 시스템 상태 보고서
**System.FM**, hello 기관 서비스에 대 한 정보를 관리 하는 hello Failover Manager service를 나타내는입니다.

### <a name="state"></a>시스템 상태
System.FM로 보고 확인 hello 서비스를 만들 때 합니다. Hello 서비스가 삭제 되었을 때 hello health store에서 hello 엔터티를 삭제 합니다.

* **SourceId**: System.FM
* **Property**: State

hello 다음 예제에서는 hello 상태 이벤트 hello 서비스 **패브릭: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>서비스 상관 관계 오류 
**System.PLB** 업데이트 하는 데 필요한 다른 서비스가 상호 관련 서비스 toobe 선호도 그룹이 만들어지는 것을 발견 하면 오류를 보고 합니다. hello 보고서는 성공적으로 업데이트가 발생할 때 지워집니다.

* **SourceId**: System.PLB
* **속성**: ServiceDescription
* **다음 단계**: 검사 hello 상관 서비스 설명 합니다.

## <a name="partition-system-health-reports"></a>파티션 시스템 상태 보고서
**System.FM**, 서비스 파티션에 대 한 정보를 관리 하는 hello 기관이 hello Failover Manager service를 나타내는입니다.

### <a name="state"></a>시스템 상태
System.FM로 보고 확인 hello 파티션이 만든 정상이 경우 합니다. Hello 파티션 삭제 되 면 hello health store에서 hello 엔터티를 삭제 합니다.

Hello 파티션 hello 최소 복제본 수 아래에 있으면 오류를 보고 합니다. Hello 파티션이 hello 최소 복제본 수 아래에 있지 않으면 hello 대상 복제본 개수 보다 낮으면 표시 되지만 경고를 보고 합니다. Hello 파티션이 쿼럼 손실에서 경우 System.FM 오류를 보고 합니다.

Hello 재구성 hello 빌드 예상 보다 오래 걸리면 및 예상 보다 오래 걸리면 경고를 포함 하는 기타 중요 한 이벤트입니다. hello 빌드 및 재구성에 대 한 예상 hello 시간 서비스 시나리오에 따라 다르게 구성할 수 있습니다. 예를 들어 한 서비스에 SQL 데이터베이스 같은 상태는 테라바이트 임 hello 빌드 적은 양의 상태를 사용 하 여 서비스에 대 한 보다 오래 걸립니다.

* **SourceId**: System.FM
* **Property**: State
* **다음 단계**: hello 상태 확인 없는 경우는 일부 복제본 않은 만들거나 열지 승격 tooprimary 또는 secondary 상태 올바르게 가능 합니다. 대부분의 경우 hello 근본 원인에는 hello open 또는 역할 변경을 구현에서 서비스 버그입니다.

다음 예제는 hello 정상 파티션 보여 줍니다.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

hello 다음 예제에서는 대상 복제본 수 아래에 있는 파티션의 hello 상태 hello 다음 단계는 구성 되어 나타나는 tooget hello 파티션 설명: **MinReplicaSetSize** 3 개 및 **TargetReplicaSetSize** 는 7입니다. Hello 클러스터의 노드 수가 hello를 가져온 후: 5입니다. 따라서이 경우 두 개의 복제본 배치할 수 없습니다 hello 사용할 수 있는 노드 수가 보다 최신 hello 대상 복제본 수입니다.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>복제본 제약 조건 위반
**System.PLB**는 복제본 제약 조건 위반을 감지하고 일부 파티션 복제본을 배치할 수 없는 경우 경고를 보고합니다. hello 보고서 세부 정보는 제약 조건에 나타나며 속성 hello 복제본 배치 하지 마세요.

* **SourceId**: System.PLB
* **Property**: **ReplicaConstraintViolation**으로 시작합니다.

## <a name="replica-system-health-reports"></a>복제본 시스템 상태 보고서
**System.RA**,이 hello 복제 데이터베이스 상태에 대 한 hello 기관 이므로 hello 재구성 에이전트 구성 요소를 나타냅니다.

### <a name="state"></a>시스템 상태
**System.RA** hello 복제본 생성 되 면 확인을 보고 합니다.

* **SourceId**: System.RA
* **Property**: State

다음 예제는 hello 정상 복제를 보여 줍니다.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>복제본 열린 상태
이 상태 보고서의 hello 설명 hello API 호출이 호출 된 hello 시작 시간 (협정 세계시)를 포함 합니다.

**System.RA** hello 복제본 열기 hello 구성 된 기간 보다 오래 걸리는 경우 경고를 보고 합니다. (기본값: 30 분)입니다. Hello API 서비스 가용성에 영향을 줍니다, 하는 경우 (기본값은 30 초를 사용 하 여는 구성 가능한 간격) hello 보고서 훨씬 빠르게 실행 됩니다. 측정 hello 시간을 hello 복제기 열기 및 열려 hello 서비스 계산 하는 hello 시간이 포함 됩니다. hello 속성 변경 내용을 tooOK hello 열을 완료 합니다.

* **SourceId**: System.RA
* **Property**에 상태 이벤트를 보여 줍니다. **ReplicaOpenStatus**
* **다음 단계**: hello 상태 확인 없으면 hello 복제본 열기 예상 보다 오래 걸리면 이유를 조사 합니다.

### <a name="slow-service-api-call"></a>느린 서비스 API 호출
**System.RAP** 및 **System.Replicator** 호출 toohello 사용자 서비스 코드를 구성 하는 hello 시간 보다 오래 걸리는 경우 경고를 보고 합니다. hello 경고 hello 호출이 완료 될 때 지워집니다.

* **SourceId**: System.RAP 또는 System.Replicator
* **속성**: hello 느린 API의 hello 이름입니다. hello 설명 hello 시간 hello API에 대 한 자세한 내용은 보류 된 제공 합니다.
* **다음 단계**: hello 호출 예상 보다 오래 걸리면 이유를 조사 합니다.

다음 예제는 hello 쿼럼 손실 되 고 이유가 무엇 인지 hello 조사 완료 단계 toofigure의 파티션을 보여 줍니다. Hello 복제본 중 하나에 해당 상태를 가져오기 있으므로 경고 성능 상태입니다. hello 서비스 작업이 예상 보다 오랫동안, System.RAP에서 보고 된 이벤트를 표시 합니다. 이 정보를 받은 후 hello 다음 단계 hello 서비스 코드에서 toolook 이며 조사 있습니다. 이 경우에 대 한 hello **RunAsync** hello 상태 저장 서비스의 구현 처리 되지 않은 예외를 throw 합니다. hello 복제본이 재순환 됩니다 hello 경고 상태에 있는 모든 복제본 나타나지 않을 수 있습니다. 가져오는 hello 성능 상태를 다시 시도 하 고 hello 복제본 ID에 모든 차이점을 확인 수 있습니다. 경우에 따라 hello 재시도 수를 통해 알.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Hello 디버거에서 hello 결함이 있는 응용 프로그램을 시작할 때 hello 진단 이벤트 창을 표시 RunAsync에서 throw 된 hello 예외:

![Visual Studio 2015 진단 이벤트: fabric:/HelloWorldStatefulApplication에서 RunAsync 실패][1]

Visual Studio 2015 진단 이벤트: **fabric:/HelloWorldStatefulApplication**에서 RunAsync 실패

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>복제 큐 전체
**System.Replicator** hello 복제 큐가 가득 찬 경우 경고를 보고 합니다. 기본 hello, 복제 큐 일반적으로 수 전체 하나 이상의 보조 복제본은 느린 tooacknowledge 작업 때문에 있습니다. Hello 보조에이 상황이 hello 서비스는 느린 tooapply hello 작업 합니다. hello 큐가 꽉 더 이상 hello 경고가 지워집니다.

* **SourceId**: System.Replicator
* **속성**: **PrimaryReplicationQueueStatus** 또는 **SecondaryReplicationQueueStatus**hello 복제본 역할에 따라

### <a name="slow-naming-operations"></a>느린 이름 지정 작업
**System.NamingService**는 이름 지정 작업이 허용 가능한 시간보다 오래 걸리는 경우 주 복제본에 해당 상태를 보고합니다. 이름 지정 작업의 예는 [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 또는 [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync)입니다. FabricClient에서 더 많은 메서드를 찾을 수 있습니다. 예를 들어 [서비스 관리 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) 또는 [속성 관리 메서드](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient)에서입니다.

> [!NOTE]
> hello 명명 서비스는 hello 클러스터에서 서비스 이름을 tooa 위치를 확인 하 고 사용자 toomanage 서비스 이름 및 속성을 활성화 합니다. 서비스 패브릭 분할된 지속형 서비스입니다. Hello 파티션 중 하나는 hello를 모든 서비스 패브릭 이름 및 서비스에 대 한 메타 데이터를 포함 하는 기관 소유자를 나타냅니다. hello 서비스 패브릭 이름은 hello 서비스는 확장할 수 있으므로 이름 소유자 파티션을 이라는 매핑된 toodifferent 파티션 됩니다. [이름 지정 서비스](service-fabric-architecture.md)에 대해 자세히 알아봅니다.
> 
> 

Hello에 대 한 경고 보고서 hello 작업 플래그가 Naming 작업이 예상 보다 오래 걸리면, *서비스 파티션 이름이 hello의 주 복제본 역할 hello 작업*합니다. Hello 작업이 성공적으로 완료 되 면 hello 경고가 지워집니다. 오류가 발생 하 여 hello 작업이 완료 되 면 hello 상태 보고서 hello 오류에 대 한 세부 정보를 포함 합니다.

* **SourceId**: System.NamingService
* **속성**: 접두사로 시작 **Duration_** hello 느리게 작동 및 연산이 적용 되는 hello에 hello 서비스 패브릭 이름을 식별 하 고 있습니다. 예를 들어 경우 이름 패브릭에서 서비스 만들기: / MyApp/MyService 시간이 너무 오래 걸리는 경우 hello 속성은 Duration_AOCreateService.fabric:/MyApp/MyService 합니다. AO 포인트 toohello hello이 이름 및 작업에 대 한 이름 지정 파티션의 역할입니다.
* **다음 단계**: hello Naming 작업이 실패 하는 이유 확인 합니다. 각 작업에는 다른 원인이 있을 수 있습니다. 예를 들어 삭제 hello 응용 프로그램 호스트 유지 hello 서비스 코드의 tooa 사용자 버그로 인해 노드에 장애가 발생 하기 때문에 서비스 노드에 남아 있을 수 있습니다.

다음 예제는 hello 만들기 서비스 작업을 보여 줍니다. hello 작업 hello 구성 된 기간 보다 오래 걸렸습니다. AO 다시 시도 하 고 작업 tooNO를 보냅니다. 없음 완료 된 hello 마지막 작업을 제한 합니다. 이 경우 hello 동일한 복제본은 AO hello 및 역할이 모두에 대 한 주입니다.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>DeployedApplication 시스템 상태 보고서
**System.Hosting** 는 배포 된 엔터티에 대 한 hello 기관입니다.

### <a name="activation"></a>활성화
System.Hosting으로 확인 때 보고 응용 프로그램 hello 노드에서 활성화 되었습니다. 그렇지 않으면 오류를 보고합니다.

* **SourceId**: System.Hosting
* **속성**: hello 롤아웃 버전을 포함 하 여 정품 인증
* **다음 단계**: hello 응용 프로그램 상태가 정상이 아닌 경우 hello 정품 인증에 실패 한 이유를 조사 합니다.

hello 다음 예제는 성공적인 활성화.

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>다운로드
**System.Hosting** hello 응용 프로그램 패키지 다운로드가 실패할 경우 오류를 보고 합니다.

* **SourceId**: System.Hosting
* **Property**: **Download:*RolloutVersion***
* **다음 단계**: hello 노드에서 hello 다운로드에 실패 한 이유를 조사 합니다.

## <a name="deployedservicepackage-system-health-reports"></a>DeployedServicePackage 시스템 상태 보고서
**System.Hosting** 는 배포 된 엔터티에 대 한 hello 기관입니다.

### <a name="service-package-activation"></a>서비스 패키지 활성화
System.Hosting은 hello 노드에서 hello 서비스 패키지 활성화가 성공한 경우 확인으로 보고 합니다. 그렇지 않으면 오류를 보고합니다.

* **SourceId**: System.Hosting
* **Property**: Activation
* **다음 단계**: hello 정품 인증에 실패 한 이유를 조사 합니다.

### <a name="code-package-activation"></a>코드 패키지 활성화
**System.Hosting** hello 활성화가 성공한 경우 각 코드 패키지에 대 한 ' 확인 '으로 보고 합니다. Hello 활성화에 실패 하는 경우 구성 된 대로 경고를 보고 합니다. 경우 **CodePackage** tooactivate 실패 하거나 구성 하는 hello 보다 큰 오류와 함께 종료 **CodePackageHealthErrorThreshold**, 호스트 오류를 보고 합니다. 서비스 패키지에 여러 코드 패키지가 있다면 각 패키지에 대해 생성된 활성화 보고서가 있습니다.

* **SourceId**: System.Hosting
* **속성**: hello 접두사를 사용 하 여 **CodePackageActivation** hello 코드 패키지 및 hello 진입점의 hello 이름을 포함 하 고  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint** * (예를 들어 **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>서비스 유형 등록
**System.Hosting** hello 서비스 종류에 성공적으로 등록 된 경우 ' 확인 '으로 보고 합니다. Hello 등록 시간에 수행 되지 않은 경우 오류를 보고 (사용 하 여 구성 된 대로 **ServiceTypeRegistrationTimeout**). Hello 런타임 닫혀 있는 경우 hello 서비스 유형이 hello 노드에서 등록 되어 있지 않은 및 호스팅 경고를 보고 합니다.

* **SourceId**: System.Hosting
* **속성**: hello 접두사를 사용 하 여 **ServiceTypeRegistration** hello 서비스 유형 이름을 포함 하 고 (예를 들어 **ServiceTypeRegistration:FileStoreServiceType**)

다음 예제는 hello 정상 배포 된 서비스 패키지를 보여 줍니다.

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>다운로드
**System.Hosting** hello 서비스 패키지 다운로드가 실패할 경우 오류를 보고 합니다.

* **SourceId**: System.Hosting
* **Property**: **Download:*RolloutVersion***
* **다음 단계**: hello 노드에서 hello 다운로드에 실패 한 이유를 조사 합니다.

### <a name="upgrade-validation"></a>유효성 검사 업그레이드
**System.Hosting** hello 노드에 대 한 업그레이드가 실패할 경우 hello 또는 hello 업그레이드 하는 동안 유효성 검사에 실패할 경우 오류를 보고 합니다.

* **SourceId**: System.Hosting
* **속성**: hello 접두사를 사용 하 여 **FabricUpgradeValidation** hello 업그레이드 버전을 포함 합니다.
* **설명**: 가리키는 toohello 오류가 발생 했습니다.

## <a name="next-steps"></a>다음 단계
[서비스 패브릭 상태 보고서 보기](service-fabric-view-entities-aggregated-health.md)

[어떻게 tooreport 및 확인 서비스 상태](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[로컬로 서비스 모니터링 및 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

