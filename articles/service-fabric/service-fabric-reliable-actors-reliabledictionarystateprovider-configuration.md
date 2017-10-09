---
title: "Azure microservices의 aaaChange ReliableDictionaryActorStateProvider 설정 | Microsoft Docs"
description: "'ReliableDictionaryActorStateProvider' 형식의 Azure 서비스 패브릭 상태 저장 행위자 구성에 대해 알아봅니다."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Reliable Actors 구성--ReliableDictionaryActorStateProvider
ReliableDictionaryActorStateProvider의 기본 구성은 hello hello Visual Studio 패키지 루트 hello 지정 된 작업자에 대해 hello Config 폴더에서 생성 된 hello settings.xml 파일을 변경 하 여 수정할 수 있습니다.

hello Azure 서비스 패브릭 런타임을 hello settings.xml 파일에 미리 정의 된 섹션 이름을 찾는 하 고 hello 기본 런타임 구성 요소를 만드는 동안 hello 구성 값을 사용 합니다.

> [!NOTE]
> 수행 **하지** 삭제 하거나 hello Visual Studio 솔루션에서에서 생성 되는 hello settings.xml 파일에는 구성을 따르고 hello의 hello 섹션 이름을 수정 합니다.
> 
> 

ReliableDictionaryActorStateProvider의 hello 구성에 영향을 주는 전역 설정도 있습니다.

## <a name="global-configuration"></a>전역 구성
hello 글로벌 구성 hello KtlLogger 섹션 아래의 hello 클러스터에 대 한 hello 클러스터 매니페스트에 지정 됩니다. 공유 hello 로그 위치 및 크기를 더한 hello 글로벌 메모리 제한 hello로 거에서 사용 하는 구성을 수 있습니다. Note는 hello 클러스터 매니페스트 변경 되는지 ReliableDictionaryActorStateProvider를 사용 하는 모든 서비스 및 신뢰할 수 있는 상태 저장 서비스입니다.

hello 클러스터 매니페스트는 설정과 tooall 노드와 hello 클러스터에서 서비스에 적용 되는 구성을 포함 하는 단일 XML 파일입니다. hello 파일에는 일반적으로 ClusterManifest.xml 호출 됩니다. 나타나면 hello Get ServiceFabricClusterManifest powershell 명령을 사용 하 여 클러스터에 대 한 hello 클러스터 매니페스트 합니다.

### <a name="configuration-names"></a>구성 이름
| 이름 | 단위 | 기본값 | 설명 |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |킬로바이트 |8388608 |최소한 KB tooallocate hello로 거에 대 한 커널 모드에서의 버퍼 메모리 풀을 작성 합니다. 이 메모리 풀 toodisk를 쓰기 전에 상태 정보를 캐시에 사용 됩니다. |
| WriteBufferMemoryPoolMaximumInKB |킬로바이트 |제한 없음 |최대 크기 toowhich hello로 거 쓰기 버퍼 메모리 풀이 증가할 수 있습니다. |
| SharedLogId |GUID |"" |Hello 기본 공유 로그 파일의에서 모든 노드에서 hello 클러스터 hello SharedLogId 특정 서비스 구성에 지정 하지 않는 모든 신뢰할 수 있는 서비스에서 사용 하는 식별 하기 위한 고유 GUID toouse를 지정 합니다. SharedLogId가 지정된 경우 SharedLogPath도 지정해야 합니다. |
| SharedLogPath |정규화된 경로 이름 |"" |Hello hello SharedLogPath 특정 서비스 구성에 지정 하지 않는 hello 클러스터의 모든 노드에 있는 모든 신뢰할 수 있는 서비스에서 사용 하는 로그 파일을 공유 하는 있는 hello 정규화 된 경로 지정 합니다. 그러나 SharedLogPath가 지정된 경우 SharedLogId도 지정해야 합니다. |
| SharedLogSizeInMB |메가바이트 |8192 |Hello 수를 지정 MB의 디스크 공간 toostatically hello 공유 로그에 대 한 할당 합니다. hello 값은 2048 이상 이어야 합니다. |

### <a name="sample-cluster-manifest-section"></a>샘플 클러스터 매니페스트 섹션
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>설명
hello로 거를 사용할 수 있는 tooall 신뢰할 수 있는 노드에 있는 서비스를 신뢰할 수 있는 서비스 복제본 hello와 연결 된 toohello 전용된 로그에 기록 되기 전에 상태 데이터를 캐시에 대 한 페이징되지 않은 커널 메모리에서 할당 된 메모리의 전역 풀을 있습니다. hello 풀 크기 WriteBufferMemoryPoolMinimumInKB hello 및 WriteBufferMemoryPoolMaximumInKB 설정에 의해 제어 됩니다. WriteBufferMemoryPoolMinimumInKB 둘 다 hello이 메모리 풀의 초기 크기 및 hello 가장 낮은 크기 toowhich hello 메모리 풀 줄어들 수 있습니다를 지정 합니다. WriteBufferMemoryPoolMaximumInKB는 hello 가장 높은 크기 toowhich hello 메모리 풀이 증가할 수 있습니다. 열려 있는 각 신뢰할 수 있는 서비스 복제본 tooWriteBufferMemoryPoolMaximumInKB 결정 하는 시스템 양만큼 hello 메모리 풀의 hello 크기를 증가할 수 있습니다. 사용 가능한 것 보다 hello 메모리 풀에서 메모리에 대 한 자세한 요구 하는 경우에 사용 가능한 메모리를 메모리에 대 한 요청 지연 됩니다. 따라서 특정 구성에 대 한 hello 쓰기 버퍼 메모리 풀 너무 작습니다. 성능이 저하 될 수 있습니다.

hello SharedLogId 및 SharedLogPath 설정은 항상 함께 사용 되는 toodefine hello GUID 및 hello 기본 위치는 hello 클러스터의 모든 노드에 대 한 로그를 공유 합니다. hello 기본 공유 로그 hello 특정 서비스에 대 한 hello settings.xml에 hello 설정을 지정 하지 않는 모든 신뢰할 수 있는 서비스에 사용 됩니다. 최상의 성능을 위해 공유 로그 파일은 공유 hello 로그 파일 tooreduce 경합 하는 용도로 사용 되는 디스크에 저장할 수 있습니다.

SharedLogSizeInMB 모든 노드에서 hello 기본 공유 로그에 대 한 디스크 공간 toopreallocate hello 크기를 지정합니다.  SharedLogId 및 SharedLogPath SharedLogSizeInMB toobe 지정에 대 한 순서에 지정 된 toobe가 필요 하지 않습니다.

## <a name="replicator-security-configuration"></a>복제자 보안 구성
복제기 보안 구성을 복제 하는 동안 사용 되는 사용 되는 toosecure hello 통신 채널 됩니다. 즉, 서비스는 다른 사용자의 복제 트래픽을 볼 수 없는 등과 hello는 데이터에 항상 사용 가능한 보안 이기도 합니다.
기본적으로 빈 보안 구성 섹션에서는 복제 보안이 되지 않습니다.

### <a name="section-name"></a>섹션 이름
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>복제자 구성
복제기 구성은 복제 하 고 로컬로 hello 상태를 유지 하 여 hello 행위자 상태 공급자 상태를 안정성이 높아야 하 게 사용 되는 tooconfigure hello 복제기 됩니다.
hello 기본 구성에서 hello Visual Studio 템플릿이 생성 되 고 충분 합니다. 이 섹션은 사용할 수 있는 tootune hello 복제기 추가 구성에 대 한 설명입니다.

### <a name="section-name"></a>섹션 이름
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>구성 이름
| 이름 | 단위 | 기본값 | 설명 |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |초 |0.015 |Hello 보조 대기를 보내기 전에 다시 승인을 toohello 기본 작업을 받은 후에 hello 복제기에 대 한 시간 간격입니다. 이 간격 내에서 처리 하는 작업에 대 한 보낸 승인 toobe 하나의 응답으로 전송 됩니다. |
| ReplicatorEndpoint |해당 없음 |기본값 없음--필수 매개 변수 |IP 주소와 포트를 주/보조 복제기 hello toocommunicate hello 복제 세트에 다른 복제기를 사용 합니다. 이 서비스 매니페스트의 hello TCP 리소스 끝점을 참조 해야 합니다. 너무 참조[서비스 매니페스트 리소스](service-fabric-service-manifest-resources.md) tooread 서비스 매니페스트에 끝점 리소스를 정의 하는 방법에 대 한 자세한 합니다. |
| MaxReplicationMessageSize |바이트 |50MB |단일 메시지에서 전송할 수 있는 복제 데이터의 최대 크기. |
| MaxPrimaryReplicationQueueSize |작업의 수 |8192 |Hello 기본 큐에서 작업의 최대 수입니다. Hello 기본 복제기에서 모든 hello 보조 복제기에서 승인을 받은 후에 작업을 해제 됩니다. 이 값은 64보다 크고 2의 제곱이어야 합니다. |
| MaxSecondaryReplicationQueueSize |작업의 수 |16384 |Hello 보조 큐에 있는 작업의 최대 수입니다. 작업은 지속성을 통해 상태를 항상 사용 가능하도록 설정한 후 해제됩니다. 이 값은 64보다 크고 2의 제곱이어야 합니다. |
| CheckpointThresholdInMB |MB |200 |로그 파일 공간 이후에 hello 상태는 검사점의 양입니다. |
| MaxRecordSizeInKB |KB |1024 |복제기 hello 있는 최대 레코드 크기 hello 로그에 쓸 수 있습니다. 이 값은 4의 배수이고 16보다 커야 합니다. |
| OptimizeLogForLowerDiskUsage |Boolean |true |True 인 경우 hello 로그 만들어지도록 hello 복제 데이터베이스의 전용된 로그 파일은 NTFS 스파스 파일을 사용 하 여 구성 됩니다. 이렇게 하면 hello 파일에 대 한 hello 실제 디스크 공간 사용이 줄어듭니다. False 인 경우 hello 최상의 쓰기 성능을 제공 하는 고정 할당 hello 파일이 만들어집니다. |
| SharedLogId |GUID |"" |이 복제본과 함께 사용 되는 hello 공유 되는 로그 파일을 식별 하기 위한 고유 guid toouse를 지정 합니다. 일반적으로 서비스는 이 설정을 사용해서는 안 됩니다. 그러나 SharedLogId가 지정된 경우 SharedLogPath도 지정해야 합니다. |
| SharedLogPath |정규화된 경로 이름 |"" |이 복제본에 대 한 hello 공유 로그 파일이 만들어지는 hello 정규화 된 경로 지정 합니다. 일반적으로 서비스는 이 설정을 사용해서는 안 됩니다. 그러나 SharedLogPath가 지정된 경우 SharedLogId도 지정해야 합니다. |

## <a name="sample-configuration-file"></a>샘플 구성 파일
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## <a name="remarks"></a>설명
hello BatchAcknowledgementInterval 매개 변수는 복제 대기 시간을 제어합니다. 값이 '0' (더 많은 승인 메시지를 전송 및 처리를 각각 포함 된 더 적은 승인 해야)으로 hello 가능한 최저의 대기 시간, 처리량의 hello 비용이 발생 합니다.
hello, BatchAcknowledgementInterval에 더 큰 hello 값 hello 더 높은 hello 전반적인 hello 비용을 더 높은 작업 대기 시간에 복제 처리량입니다. 트랜잭션 커밋의 대기 시간 toohello 직접 변환 됩니다.

hello 복제 데이터베이스의 전용된 로그 파일에 toostore 상태 정보를 사용할 수 있는 hello CheckpointThresholdInMB 매개 변수 컨트롤 hello 크기의 복제기 hello 디스크 공간입니다. Hello 기본 새 복제 toohello 집합을 추가 하는 경우 재구성 시간을 단축 될 수 있는 보다 tooa 더 높은 값을 늘리면 합니다. 이 hello 로그에 작업의 자세한 기록의 가용성을 toohello 인해 일어나는 toohello 부분 상태 전송 때문입니다. 충돌이 발생 한 후 복제본의 복구 시간 hello 증가할 수 있습니다이 있습니다.

OptimizeForLowerDiskUsage tootrue로 설정 하면 비활성 복제본 더 적은 디스크 공간만 사용 하 여는 동안 활성 복제본의 로그 파일에서 자세한 상태 정보 저장할 수 있도록 로그 파일 공간 초과 프로 비전 됩니다. 이렇게 하면 가능한 toohost 노드에서 이상의 복제본입니다. OptimizeForLowerDiskUsage toofalse로 설정 하면 hello 상태 정보가 toohello 로그 파일 보다 신속 하 게 기록 됩니다.

hello MaxRecordSizeInKB 설정은 hello hello 복제 기가 hello 로그 파일에 쓸 수 있는 레코드의 최대 크기를 정의 합니다. 대부분의 경우에서 hello 기본 1024 KB 레코드 크기는 최적입니다. 그러나 hello 서비스 hello 상태 정보의 큰 항목 toobe 일부 데이터를 발생 시킨 경우 다음이 값 해야 toobe 증가 합니다. 작아집니다 MaxRecordSizeInKB 1024 보다 작은 레코드가 hello 작은 레코드에 필요한 hello 공간만 사용 하 여 거의 의미가 없습니다. 이 값 toobe 드문 경우에만 변경 해야 하 라고 생각 됩니다.

hello SharedLogId 및 SharedLogPath 설정을 사용 하는 함께 toomake hello 노드에 대 한 서비스 사용 hello 기본 공유 로그에서 별도 공유 로그는 항상입니다. 최상의 효율성을 높이기 위해 만큼 서비스에 최대한 hello를 지정 해야 로그 동일한 공유 합니다. 공유 로그 파일은 hello 공유 로그 파일을 tooreduce 헤드 이동 경합 용 으로만 사용 되는 디스크에 저장할 수 있습니다. 이러한 값 toobe 드문 경우에만 변경 해야 하 라고 생각 됩니다.

