---
title: "신뢰할 수 있는 Azure microservices aaaConfigure | Microsoft Docs"
description: "Azure 서비스 패브릭에서 상태 저장 Reliable Services를 구성하는 방법을 알아봅니다."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>상태 저장 Reliable Services 구성
Reliable Services에는 두 가지 구성 설정 집합이 있습니다. 하나의 집합 hello 클러스터의 모든 신뢰할 수 있는 서비스에 대 한 전역 상태인 hello 다른 집합은 특정 tooa 특정 신뢰할 수 있는 서비스입니다.

## <a name="global-configuration"></a>전역 구성
hello 신뢰할 수 있는 글로벌 서비스 구성은 hello KtlLogger 섹션 아래의 hello 클러스터에 대 한 hello 클러스터 매니페스트에 지정 됩니다. 공유 hello 로그 위치 및 크기를 더한 hello 글로벌 메모리 제한 hello로 거에서 사용 하는 구성을 수 있습니다. hello 클러스터 매니페스트는 설정과 tooall 노드와 hello 클러스터에서 서비스에 적용 되는 구성을 포함 하는 단일 XML 파일입니다. hello 파일에는 일반적으로 ClusterManifest.xml 호출 됩니다. 나타나면 hello Get ServiceFabricClusterManifest powershell 명령을 사용 하 여 클러스터에 대 한 hello 클러스터 매니페스트 합니다.

### <a name="configuration-names"></a>구성 이름
| 이름 | 단위 | 기본값 | 설명 |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |킬로바이트 |8388608 |최소한 KB tooallocate hello로 거에 대 한 커널 모드에서의 버퍼 메모리 풀을 작성 합니다. 이 메모리 풀 toodisk를 쓰기 전에 상태 정보를 캐시에 사용 됩니다. |
| WriteBufferMemoryPoolMaximumInKB |킬로바이트 |제한 없음 |최대 크기 toowhich hello로 거 쓰기 버퍼 메모리 풀이 증가할 수 있습니다. |
| SharedLogId |GUID |"" |Hello 기본 공유 로그 파일의에서 모든 노드에서 hello 클러스터 hello SharedLogId 특정 서비스 구성에 지정 하지 않는 모든 신뢰할 수 있는 서비스에서 사용 하는 식별 하기 위한 고유 GUID toouse를 지정 합니다. SharedLogId가 지정된 경우 SharedLogPath도 지정해야 합니다. |
| SharedLogPath |정규화된 경로 이름 |"" |Hello hello SharedLogPath 특정 서비스 구성에 지정 하지 않는 hello 클러스터의 모든 노드에 있는 모든 신뢰할 수 있는 서비스에서 사용 하는 로그 파일을 공유 하는 있는 hello 정규화 된 경로 지정 합니다. 그러나 SharedLogPath가 지정된 경우 SharedLogId도 지정해야 합니다. |
| SharedLogSizeInMB |메가바이트 |8192 |Hello 수를 지정 MB의 디스크 공간 toostatically hello 공유 로그에 대 한 할당 합니다. hello 값은 2048 이상 이어야 합니다. |

ARM Azure 또는 온-프레미스 JSON 템플릿에서 hello 감시할 toochange hello hello 공유 트랜잭션 로그를 가져오는 만드는 방법을 tooback 상태 저장 서비스에 대 한 신뢰할 수 있는 모든 컬렉션 보여 줍니다.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>샘플 로컬 개발자 클러스터 매니페스트 섹션
원하는 toochange이 로컬 개발 환경에서 tooedit hello 로컬 clustermanifest.xml 파일이 필요 합니다.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>설명
hello로 거를 사용할 수 있는 tooall 신뢰할 수 있는 노드에 있는 서비스를 신뢰할 수 있는 서비스 복제본 hello와 연결 된 toohello 전용된 로그에 기록 되기 전에 상태 데이터를 캐시에 대 한 페이징되지 않은 커널 메모리에서 할당 된 메모리의 전역 풀을 있습니다. hello 풀 크기 WriteBufferMemoryPoolMinimumInKB hello 및 WriteBufferMemoryPoolMaximumInKB 설정에 의해 제어 됩니다. WriteBufferMemoryPoolMinimumInKB 둘 다 hello이 메모리 풀의 초기 크기 및 hello 가장 낮은 크기 toowhich hello 메모리 풀 줄어들 수 있습니다를 지정 합니다. WriteBufferMemoryPoolMaximumInKB는 hello 가장 높은 크기 toowhich hello 메모리 풀이 증가할 수 있습니다. 열려 있는 각 신뢰할 수 있는 서비스 복제본 tooWriteBufferMemoryPoolMaximumInKB 결정 하는 시스템 양만큼 hello 메모리 풀의 hello 크기를 증가할 수 있습니다. 사용 가능한 것 보다 hello 메모리 풀에서 메모리에 대 한 자세한 요구 하는 경우에 사용 가능한 메모리를 메모리에 대 한 요청 지연 됩니다. 따라서 특정 구성에 대 한 hello 쓰기 버퍼 메모리 풀 너무 작습니다. 성능이 저하 될 수 있습니다.

hello SharedLogId 및 SharedLogPath 설정은 항상 함께 사용 되는 toodefine hello GUID 및 hello 기본 위치는 hello 클러스터의 모든 노드에 대 한 로그를 공유 합니다. hello 기본 공유 로그 hello 특정 서비스에 대 한 hello settings.xml에 hello 설정을 지정 하지 않는 모든 신뢰할 수 있는 서비스에 사용 됩니다. 최상의 성능을 위해 공유 로그 파일은 공유 hello 로그 파일 tooreduce 경합 하는 용도로 사용 되는 디스크에 저장할 수 있습니다.

SharedLogSizeInMB 모든 노드에서 hello 기본 공유 로그에 대 한 디스크 공간 toopreallocate hello 크기를 지정합니다.  SharedLogId 및 SharedLogPath SharedLogSizeInMB toobe 지정에 대 한 순서에 지정 된 toobe가 필요 하지 않습니다.

## <a name="service-specific-configuration"></a>서비스별 구성
Hello 구성 패키지 (구성)를 사용 하 여 상태 저장 Reliable Services의 기본 구성을 수정 하거나 서비스 구현 (코드) hello 수 있습니다.

* **Config** -hello 구성 패키지를 통해 구성 hello Microsoft Visual Studio 패키지 루트 hello 응용 프로그램의 각 서비스에 대 한 hello Config 폴더에서 생성 되는 hello Settings.xml 파일을 변경 하 여 수행 됩니다.
* **코드** -ReliableStateManagerConfiguration 개체를 사용 하 여 hello 적절 한 옵션 집합과 ReliableStateManager를 만들어 구성 코드를 통해 수행 됩니다.

기본적으로 hello Azure 서비스 패브릭 런타임을 hello Settings.xml 파일에 미리 정의 된 섹션 이름을 찾는 하 고 hello 기본 런타임 구성 요소를 만드는 동안 hello 구성 값을 사용 합니다.

> [!NOTE]
> 수행 **하지** tooconfigure 코드를 통해 서비스를 하려는 경우가 아니면 hello Visual Studio 솔루션에서 생성 되는 hello Settings.xml 파일에는 구성을 따르고 hello의 hello 섹션 이름을 삭제 합니다.
> Hello 구성 패키지 또는 섹션 이름 이름 바꾸기 ReliableStateManager hello를 구성할 때 코드를 변경을 해야 합니다.
> 
> 

### <a name="replicator-security-configuration"></a>복제자 보안 구성
복제기 보안 구성을 복제 하는 동안 사용 되는 사용 되는 toosecure hello 통신 채널 됩니다. 즉, 서비스는 다른 사용자의 복제 트래픽을 인지 확인 하는 hello는 데이터에 항상 사용 가능한도 보안 수 toosee 수 없습니다. 기본적으로 빈 보안 구성 섹션에서는 복제 보안이 되지 않습니다.

### <a name="default-section-name"></a>기본 섹션 이름
ReplicatorSecurityConfig

> [!NOTE]
> toochange 재정의 hello replicatorSecuritySectionName 매개 변수 toohello ReliableStateManagerConfiguration 생성자 hello ReliableStateManager이 서비스를 만들 때이 섹션 이름입니다.
> 
> 

### <a name="replicator-configuration"></a>복제자 구성
복제기 구성 hello 상태 저장 신뢰할 수 있는 서비스의 상태를 복제 하 고 로컬로 hello 상태를 유지 하 여 매우 안정적 게 hello 복제기를 구성 합니다.
hello 기본 구성에서 hello Visual Studio 템플릿이 생성 되 고 충분 합니다. 이 섹션은 사용할 수 있는 tootune hello 복제기 추가 구성에 대 한 설명입니다.

### <a name="default-section-name"></a>기본 섹션 이름
ReplicatorConfig

> [!NOTE]
> toochange 재정의 hello replicatorSettingsSectionName 매개 변수 toohello ReliableStateManagerConfiguration 생성자 hello ReliableStateManager이 서비스를 만들 때이 섹션 이름입니다.
> 
> 

### <a name="configuration-names"></a>구성 이름
| 이름 | 단위 | 기본값 | 설명 |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |초 |0.015 |Hello 보조 대기를 보내기 전에 다시 승인을 toohello 기본 작업을 받은 후에 hello 복제기에 대 한 시간 간격입니다. 이 간격 내에서 처리 하는 작업에 대 한 보낸 승인 toobe 하나의 응답으로 전송 됩니다. |
| ReplicatorEndpoint |해당 없음 |기본값 없음--필수 매개 변수 |IP 주소와 포트를 주/보조 복제기 hello toocommunicate hello 복제 세트에 다른 복제기를 사용 합니다. 이 서비스 매니페스트의 hello TCP 리소스 끝점을 참조 해야 합니다. 너무 참조[서비스 매니페스트 리소스](service-fabric-service-manifest-resources.md) tooread 서비스 매니페스트에 끝점 리소스를 정의 하는 방법에 대 한 자세한 합니다. |
| MaxPrimaryReplicationQueueSize |작업의 수 |8192 |Hello 기본 큐에서 작업의 최대 수입니다. Hello 기본 복제기에서 모든 hello 보조 복제기에서 승인을 받은 후에 작업을 해제 됩니다. 이 값은 64보다 크고 2의 제곱이어야 합니다. |
| MaxSecondaryReplicationQueueSize |작업의 수 |16384 |Hello 보조 큐에 있는 작업의 최대 수입니다. 작업은 지속성을 통해 상태를 항상 사용 가능하도록 설정한 후 해제됩니다. 이 값은 64보다 크고 2의 제곱이어야 합니다. |
| CheckpointThresholdInMB |MB |50 |로그 파일 공간 이후에 hello 상태는 검사점의 양입니다. |
| MaxRecordSizeInKB |KB |1024 |복제기 hello 있는 최대 레코드 크기 hello 로그에 쓸 수 있습니다. 이 값은 4의 배수이고 16보다 커야 합니다. |
| MinLogSizeInMB |MB |0(시스템 결정) |Hello 트랜잭션 로그의 최소 크기입니다. hello 로그는이 설정 아래의 tootruncate tooa 크기를 허용 되지 않습니다. 0이 나타냅니다 해당 hello 복제기 hello 최소 로그 크기를 결정 합니다. 이 값을 늘리면을 낮추면 잘리지 관련 로그 레코드의 가능성 이후 부분 복사본과 증분 백업을 수행 하는 hello 가능성을 증가 합니다. |
| TruncationThresholdFactor |비율 |2 |잘림은 트리거되지 hello 로그의 크기를 결정 합니다. 잘림 임계값은 MinLogSizeInMB와 TruncationThresholdFactor를 곱한 값으로 결정됩니다. TruncationThresholdFactor는 1보다 커야 합니다. MinLogSizeInMB * TruncationThresholdFactor는 MaxStreamSizeInMB보다 작아야 합니다. |
| ThrottlingThresholdFactor |비율 |4 |제한 되 고 hello 복제본은 시작 하는 hello 로그의 크기를 결정 합니다. 제한 임계값(MB)은 Max((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor))에 의해 결정됩니다. 제한 임계값(MB)은 잘림 임계값(MB)보다 커야 합니다. 잘림 임계값(MB)은 MaxStreamSizeInMB보다 작아야 합니다. |
| MaxAccumulatedBackupLogSizeInMB |MB |800 |지정된 백업 로그 체인 내 백업 로그의 최대 누적 크기(MB)입니다. Hello 증분 백업 관련 전체 백업을 toobe hello이이 크기 보다 큰 이후 누적 된 hello 백업 로그로 인해 백업 로그를 생성 하는 경우에 증분 백업 요청 실패 합니다. 이러한 경우 사용자가 필요한 tootake 전체 백업 합니다. |
| SharedLogId |GUID |"" |이 복제본과 함께 사용 되는 hello 공유 되는 로그 파일을 식별 하기 위한 고유 GUID toouse를 지정 합니다. 일반적으로 서비스는 이 설정을 사용해서는 안 됩니다. 그러나 SharedLogId가 지정된 경우 SharedLogPath도 지정해야 합니다. |
| SharedLogPath |정규화된 경로 이름 |"" |이 복제본에 대 한 hello 공유 로그 파일이 만들어지는 hello 정규화 된 경로 지정 합니다. 일반적으로 서비스는 이 설정을 사용해서는 안 됩니다. 그러나 SharedLogPath가 지정된 경우 SharedLogId도 지정해야 합니다. |
| SlowApiMonitoringDuration |초 |300 |Hello 모니터링 관리 되는 API 호출에 대 한 간격을 설정 합니다. 예: 사용자 제공 백업 콜백 함수. Hello 간격이 지나면 toohello 상태 관리자 경고 상태 보고서를 전송 됩니다. |

### <a name="sample-configuration-via-code"></a>코드를 통한 샘플 구성
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>샘플 구성 파일
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
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


### <a name="remarks"></a>설명
BatchAcknowledgementInterval은 복제 대기 시간을 제어합니다. 값이 '0' (더 많은 승인 메시지를 전송 및 처리를 각각 포함 된 더 적은 승인 해야)으로 hello 가능한 최저의 대기 시간, 처리량의 hello 비용이 발생 합니다.
hello, BatchAcknowledgementInterval에 더 큰 hello 값 hello 더 높은 hello 전반적인 hello 비용을 더 높은 작업 대기 시간에 복제 처리량입니다. 트랜잭션 커밋의 대기 시간 toohello 직접 변환 됩니다.

복제기 hello 하는 디스크 공간의 CheckpointThresholdInMB 컨트롤 hello 크기에 대 한 hello 값 hello 복제 데이터베이스의 전용된 로그 파일에 toostore 상태 정보를 사용할 수 있습니다. Hello 기본 새 복제 toohello 집합을 추가 하는 경우 재구성 시간을 단축 될 수 있는 보다 tooa 더 높은 값을 늘리면 합니다. 이 hello 로그에 작업의 자세한 기록의 가용성을 toohello 인해 일어나는 toohello 부분 상태 전송 때문입니다. 충돌이 발생 한 후 복제본의 복구 시간 hello 증가할 수 있습니다이 있습니다.

hello MaxRecordSizeInKB 설정은 hello hello 복제 기가 hello 로그 파일에 쓸 수 있는 레코드의 최대 크기를 정의 합니다. 대부분의 경우에서 hello 기본 1024 KB 레코드 크기는 최적입니다. 그러나 hello 서비스 hello 상태 정보의 큰 항목 toobe 일부 데이터를 발생 시킨 경우 다음이 값 해야 toobe 증가 합니다. 작아집니다 MaxRecordSizeInKB 1024 보다 작은 레코드가 hello 작은 레코드에 필요한 hello 공간만 사용 하 여 거의 의미가 없습니다. 이 값 toobe 드문 경우에 변경 해야 하 라고 생각 됩니다.

hello SharedLogId 및 SharedLogPath 설정을 사용 하는 함께 toomake hello 노드에 대 한 서비스 사용 hello 기본 공유 로그에서 별도 공유 로그는 항상입니다. 최상의 효율성을 높이기 위해 만큼 서비스에 최대한 hello를 지정 해야 로그 동일한 공유 합니다. 공유 로그 파일은 공유 hello 로그 파일 tooreduce 헤드 이동 경합 하는 용도로 사용 되는 디스크에 저장할 수 있습니다. 이 값 toobe 드문 경우에 변경 해야 하 라고 생각 됩니다.

## <a name="next-steps"></a>다음 단계
* [Visual Studio에서 서비스 패브릭 응용 프로그램 디버깅](service-fabric-debugging-your-application.md)
* [신뢰할 수 있는 서비스에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/dn706529.aspx)

