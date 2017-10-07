---
title: "Azure 서비스 패브릭 클러스터 설정 aaaChange | Microsoft Docs"
description: "이 문서에서는 hello 패브릭 설정 및 사용자 지정할 수 있는 hello fabric 업그레이드 정책을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>서비스 패브릭 클러스터 설정 및 패브릭 업그레이드 정책 사용자 지정
이 문서는 다양 한 패브릭 설정 및 서비스 패브릭 클러스터에 대 한 hello fabric 업그레이드 정책 toocustomize hello 하는 방법을 알려줍니다. Hello 포털 또는 Azure 리소스 관리자 템플릿을 사용 하 여 사용자 지정할 수 있습니다.

> [!NOTE]
> 설정의 일부만 hello 포털을 통해 사용할 수 있습니다. 아래에 나열 된 설정은 hello 포털을 통해 사용할 수 없는 경우 사용자는 Azure 리소스 관리자 템플릿을 사용 하 여 지정 합니다.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿으로 Service Fabric 클러스터 설정 사용자 지정
hello 단계 아래에 설명 방법을 tooadd 새 설정 *MaxDiskQuotaInMB* toohello *진단* 섹션.

1. Toohttps://resources.azure.com 이동
2. 확장 하 여 tooyour 구독 이동 구독 그룹-> 리소스-> Microsoft.ServiceFabric-Your 클러스터 이름 >
3. Hello 위 오른쪽 모서리에서 "읽기/쓰기" 선택
4. 편집을 선택 하 고 hello 업데이트 `fabricSettings` JSON 요소 하 고 새 요소를 추가 합니다.

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>사용자 지정할 수 있는 패브릭 설정
다음은 사용자 지정할 수 있는 hello 패브릭 설정입니다.

### <a name="section-name-diagnostics"></a>섹션 이름: Diagnostics
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ConsumerInstances |문자열 |hello DCA 소비자 인스턴스 목록입니다. |
| ProducerInstances |문자열 |hello DCA 생산자 인스턴스 목록입니다. |
| AppEtwTraceDeletionAgeInDays |int, 기본값: 3 |응용 프로그램 ETW 추적을 포함하고 있는 오래된 ETL 파일을 삭제한 이후 경과한 일 수 |
| AppDiagnosticStoreAccessRequiresImpersonation |bool, 기본값: true |여부 hello 응용 프로그램을 대신 하 여 저장 진단에 액세스 하는 경우 가장이 필요 합니다. |
| MaxDiskQuotaInMB |int, 기본값: 65536 |Windows Fabric 로그 파일의 디스크 할당량(MB) |
| DiskFullSafetySpaceInMB |int, 기본값: 1024 |DCA에서 사용에서 MB tooprotect 남은 디스크 공간 |
| ApplicationLogsFormatVersion |int, 기본값: 0 |응용 프로그램 로그 형식의 버전. 지원되는 값은 0과 1입니다. 버전 1 0 버전 보다 hello ETW 이벤트 레코드에서에서 더 많은 필드를 포함합니다. |
| ClusterId |문자열 |hello hello 클러스터의 고유 id입니다. 이 hello 클러스터가 생성 될 때 생성 됩니다. |
| EnableTelemetry |bool, 기본값: true |이 tooenable 가거나 원격 분석을 사용 하지 않도록 설정 합니다. |
| EnableCircularTraceSession |bool, 기본값: false |플래그에서 순환 추적 세션을 사용해야 하는지 여부를 나타냅니다. |

### <a name="section-name-traceetw"></a>섹션 이름: Trace/Etw
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| Level |int, 기본값: 4 |ETW 추적 수준은 1, 2, 3, 4 값을 가질 수 있습니다. 지원 되는 toobe 4에 대 한 hello 추적 수준을 유지 해야 합니다 |

### <a name="section-name-performancecounterlocalstore"></a>섹션 이름: PerformanceCounterLocalStore
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| IsEnabled |bool, 기본값: true |플래그에서 로컬 노드의 성능 카운터 수집을 사용하는지 여부를 나타냅니다. |
| SamplingIntervalInSeconds |int, 기본값: 60 |수집되는 성능 카운터의 샘플링 간격 |
| Counters |문자열 |성능 카운터 toocollect의 쉼표로 구분 된 목록입니다. |
| MaxCounterBinaryFileSizeInMB |int, 기본값: 1 |각 성능 카운터 이진 파일의 최대 크기(MB) |
| NewCounterBinaryFileCreationIntervalInMinutes |int, 기본값: 10 |새 성능 카운터 이진 파일이 만들어지는 최대 간격(초) |

### <a name="section-name-setup"></a>섹션 이름: Setup
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| FabricDataRoot |String |Service Fabric 데이터 루트 디렉터리. Azure에 대한 기본값: d:\svcfab |
| FabricLogRoot |문자열 |Service Fabric 로그 루트 디렉터리. SF 로그 및 추적이 배치되는 위치입니다. |
| ServiceRunAsAccountName |문자열 |toorun 패브릭 호스트 서비스는 hello 계정 이름입니다. |
| ServiceStartupType |문자열 |hello hello 패브릭 호스트 서비스의 시작 유형입니다. |
| SkipFirewallConfiguration |bool, 기본값: false |방화벽 설정 하면 toobe 지정 여부 hello 시스템으로 설정 합니다. Windows 방화벽을 사용하는 경우에만 적용됩니다. 타사 방화벽을 사용 하는 경우 시스템 및 응용 프로그램 toouse hello에 대 한 hello 포트를 열고 해야 |

### <a name="section-name-transactionalreplicator"></a>섹션 이름: TransactionalReplicator
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| MaxCopyQueueSize |uint, 기본값: 16384 |이 hello 최 댓 값 hello hello 큐는 복제 작업에서 유지 관리에 대 한 초기 크기를 정의 합니다. 2의 거듭제곱이어야 합니다. 런타임 동안 hello 큐가 증가 하는 경우 toothis 크기 작업 hello 기본 및 보조 복제기 사이의 제한 됩니다. |
| BatchAcknowledgementInterval | time(초), 기본값: 0.015 | 시간 간격은 초 단위로 지정합니다. Hello 승인을 다시 보내기 전에 작업을 받은 후 복제기 대기 hello는 시간의 양을 결정 합니다. 이 시간 동안 받은 다른 작업 네트워크 트래픽이 감소 하지만 hello 복제기의 잠재적으로 줄여서 hello 처리량-> 승인 단일 메시지로 다시 전송 해야 합니다. |
| MaxReplicationMessageSize |uint, 기본값: 52428800 | 복제 작업의 최대 메시지 크기. 기본값은 50MB입니다. |
| ReplicatorAddress |string, 기본값: "localhost:0" | 문자열-'ip: port' 순서 toosend/수신 작업의 다른 복제본과 hello Windows 패브릭 복제기 tooestablish 연결에 사용 되는 형태의 hello 끝점입니다. |
| InitialPrimaryReplicationQueueSize |uint, 기본값: 64 | 이 값 hello hello에 hello 복제 작업을 기본 유지 관리 하는 hello 큐에 대 한 초기 크기를 정의 합니다. 2의 거듭제곱이어야 합니다.|
| MaxPrimaryReplicationQueueSize |uint, 기본값: 8192 |Hello hello 주 복제 큐에 존재할 수 있는 작업의 최대 수입니다. 2의 거듭제곱이어야 합니다. |
| MaxPrimaryReplicationQueueMemorySize |uint, 기본값: 0 |Hello 바이트 hello 주 복제 큐의 최대 값입니다. |
| InitialSecondaryReplicationQueueSize |uint, 기본값: 64 |이 값에 hello hello 복제 작업을 보조 유지 관리 하는 hello 큐에 대 한 hello 초기 크기를 정의 합니다. 2의 거듭제곱이어야 합니다. |
| MaxSecondaryReplicationQueueSize |uint, 기본값: 16384 |Hello hello 보조 사이트 간 복제 큐에 존재할 수 있는 작업의 최대 수입니다. 2의 거듭제곱이어야 합니다. |
| MaxSecondaryReplicationQueueMemorySize |uint, 기본값: 0 |Hello 바이트 hello 보조 사이트 간 복제 큐의 최대 값입니다. |
| SecondaryClearAcknowledgedOperations |bool, 기본값: false |Bool toohello 기본 (플러시된 toohello 디스크)를 승인 하기 면 hello 보조 복제기에서 hello 작업 지우려면 제어 합니다. 새로운 주 복제본 장애 조치 후 잡고 하는 동안 hello 하는 설정에서이 tooTRUE 추가 디스크 읽기 발생할 수 있습니다. |
| MaxMetadataSizeInKB |int, 기본값: 4 |Hello 로그 스트림 메타 데이터의 최대 크기입니다. |
| MaxRecordSizeInKB |uint, 기본값: 1024 | 로그 스트림 레코드의 최대 크기 |
| CheckpointThresholdInMB |int, 기본값: 50 |Hello 로그 사용량이이 값을 초과할 때 검사점이 시작 됩니다. |
| MaxAccumulatedBackupLogSizeInMB |int, 기본값: 800 |지정된 백업 로그 체인 내 백업 로그의 최대 누적 크기(MB)입니다. Hello 증분 백업 관련 전체 백업을 toobe hello이이 크기 보다 큰 이후 누적 된 hello 백업 로그로 인해 백업 로그를 생성 하는 경우에 증분 백업 요청 실패 합니다. 이러한 경우 사용자가 필요한 tootake 전체 백업 합니다. |
| MaxWriteQueueDepthInKB |int, 기본값: 0 | 최대 Int이이 복제본과 연결 된 hello 로그에 대 한 해당 hello 코어로 거 (킬로바이트)에 지정 된 대로 ְ ײ 큐 깊이 작성 합니다. 이 값은 hello 최대 코어로 거 업데이트 하는 동안 처리 되지 않은 바이트 수입니다. 적절 한 값 또는 4의 배수가 hello 핵심 toocompute로 거에 대 한 0 수도 있습니다. |
| SharedLogId |String |공유 로그 식별자. GUID이며 각 공유 로그마다 고유해야 합니다. |
| SharedLogPath |문자열 |경로 toohello 공유 로그입니다. 이 값이 비어 hello 기본 공유 로그 사용 됩니다. |
| SlowApiMonitoringDuration |시간(초), 기본값: 300 | 경고 상태 이벤트가 발생하기 전에 API 지속 시간을 지정합니다.|
| MinLogSizeInMB |int, 기본값: 0 |Hello 트랜잭션 로그의 최소 크기입니다. hello 로그는이 설정 아래의 tootruncate tooa 크기를 허용 되지 않습니다. 0이 나타냅니다 해당 hello 복제기 tooother 설정에 따라 hello 최소 로그 크기를 결정 합니다. 이 값을 늘리면을 낮추면 잘리지 관련 로그 레코드의 가능성 이후 부분 복사본과 증분 백업을 수행 하는 hello 가능성을 증가 합니다. |

### <a name="section-name-fabricclient"></a>섹션 이름: FabricClient
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| NodeAddresses |string, 기본값: "" |컬렉션 명명 서비스 hello hello로 사용 되는 toocommunicate 일 수 있는 서로 다른 노드에 주소 (연결 문자열)입니다. 클라이언트에서 연결 하는 hello 주소 중 하나를 임의로 선택 hello 처음 합니다. 연결 문자열을 여러 개 제공 되 고 연결이 통신 또는 시간 초과 오류; 인해 실패 hello 클라이언트 전환 toouse hello 다음 주소 순차적으로 합니다. 재시도 의미 체계에 대 한 자세한 내용은 hello 명명 서비스 주소 다시 시도 섹션을 참조 합니다. |
| ConnectionInitializationTimeout |time(초), 기본값: 2 |시간 간격은 초 단위로 지정합니다. 각 시간 클라이언트에 대 한 연결 제한 시간 간격 tooopen toohello 게이트웨이 연결을 시도합니다. |
| PartitionLocationCacheLimit |int, 기본값: 100000 |서비스 확인을 위해 캐시 된 파티션 수 (제한 없음 too0 설정 됨). |
| ServiceChangePollInterval |time(초), 기본값: 120 |시간 간격은 초 단위로 지정합니다. 변경 알림 콜백 등록 된 서비스에 대 한 hello 클라이언트 toohello 게이트웨이에서 hello 서비스에 대 한 연속으로 폴링하는 간격을 변경합니다. |
| KeepAliveIntervalInSeconds |int, 기본값: 20 |hello 간격은 hello FabricClient에 전송 toohello 게이트웨이 연결 유지 메시지를 보냅니다. 0 값인 경우 keepAlive를 사용하지 않도록 설정됩니다. 양수 값이어야 합니다. |
| HealthOperationTimeout |time(초), 기본값: 120 |시간 간격은 초 단위로 지정합니다. 보고서 메시지에 대 한 제한 시간 hello 전송 tooHealth 관리자. |
| HealthReportSendInterval |시간(초), 기본값: 30 |시간 간격은 초 단위로 지정합니다. 보고 구성 요소에서 전송 누적 상태는 hello 간격 tooHealth 관리자를 보고 합니다. |
| HealthReportRetrySendInterval |시간(초), 기본값: 30 |시간 간격은 초 단위로 지정합니다. 누적 상태를 다시 보내는 보고 구성 요소에서 hello 간격 tooHealth 관리자를 보고 합니다. |
| RetryBackoffInterval |time(초), 기본값: 3 |시간 간격은 초 단위로 지정합니다. hello 백오프 간격 hello 작업을 다시 시도 합니다. |
| MaxFileSenderThreads |uint, 기본값: 10 |hello 동시에 전송 되는 파일의 최대 수입니다. |

### <a name="section-name-common"></a>섹션 이름: Common
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| PerfMonitorInterval |time(초), 기본값: 1 |시간 간격은 초 단위로 지정합니다. 성능 모니터링 간격입니다. 설정 too0 또는 음수 값을 모니터링 하는 사용 하지 않습니다. |

### <a name="section-name-healthmanager"></a>섹션 이름: HealthManager
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |bool, 기본값: false |클러스터 상태 평가 정책이며, 응용 프로그램 유형별 상태 평가를 사용하도록 설정됩니다. |

### <a name="section-name-fabricnode"></a>섹션 이름: FabricNode
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| StateTraceInterval |시간(초), 기본값: 300 |시간 간격은 초 단위로 지정합니다. 각 노드를 FM/FMM에 노드를 노드 상태를 추적에 대 한 hello 간격입니다. |

### <a name="section-name-nodedomainids"></a>섹션 이름: NodeDomainIds
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| UpgradeDomainId |string, 기본값: "" |노드가 속한 hello 업그레이드 도메인에 설명 합니다. |
| PropertyGroup |NodeFaultDomainIdCollection |노드가 속한 hello 오류 도메인에 설명 합니다. hello 장애 도메인 hello 데이터 센터의 hello 노드의 hello 위치를 설명 하는 URI를 통해 정의 됩니다.  오류 도메인 Uri는 hello의 서식을 fd: / fd/URI 경로 세그먼트 뒤 합니다.|

### <a name="section-name-nodeproperties"></a>섹션 이름: NodeProperties
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |노드 속성에 대한 문자열 키-값 쌍 컬렉션 |

### <a name="section-name-nodecapacities"></a>섹션 이름: NodeCapacities
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |다양한 메트릭에 대한 노드 용량 컬렉션 |

### <a name="section-name-fabricnode"></a>섹션 이름: FabricNode
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| StartApplicationPortRange |int, 기본값: 0 |하위 시스템을 호스트 하 여 관리 되는 hello 응용 프로그램 포트를 시작 합니다. Hosting(호스팅)에서 EndpointFilteringEnabled가 true인 경우 필수입니다. |
| EndApplicationPortRange |int, 기본값: 0 |하위 시스템을 호스트 하 여 관리 하는 hello 응용 프로그램 포트의 끝 (더 포함)입니다. Hosting(호스팅)에서 EndpointFilteringEnabled가 true인 경우 필수입니다. |
| ClusterX509StoreName |string, 기본값: "My" |클러스터 내 통신을 보호하기 위한 클러스터 인증서가 있는 X.509 인증서 저장소의 이름 |
| ClusterX509FindType |string, 기본값: "FindByThumbprint" |Hello 저장소의 클러스터 인증서에 대 한 toosearch ClusterX509StoreName 지원 되는 값으로 지정 하는 방법을 나타냅니다. "FindByThumbprint"; "FindBySubjectName"와 "FindBySubjectName"; 여러 명의 일치 항목;에 있는 경우 hello hello 바깥쪽 만료 하나를 사용 합니다. |
| ClusterX509FindValue |string, 기본값: "" |Toolocate 클러스터 인증서를 사용 하는 필터 값을 검색 했습니다. |
| ClusterX509FindValueSecondary |string, 기본값: "" |Toolocate 클러스터 인증서를 사용 하는 필터 값을 검색 했습니다. |
| ServerAuthX509StoreName |string, 기본값: "My" |주 서비스에 대한 서버 인증서가 있는 X.509 인증서 저장소의 이름 |
| ServerAuthX509FindType |string, 기본값: "FindByThumbprint" |Hello 저장소에 서버 인증서에 대 한 toosearch ServerAuthX509StoreName 지원 값으로 지정 하는 방법을 나타냅니다: FindByThumbprint; FindBySubjectName 합니다. |
| ServerAuthX509FindValue |string, 기본값: "" |Toolocate 서버 인증서를 사용 하는 필터 값을 검색 했습니다. |
| ServerAuthX509FindValueSecondary |string, 기본값: "" |Toolocate 서버 인증서를 사용 하는 필터 값을 검색 했습니다. |
| ClientAuthX509StoreName |string, 기본값: "My" |Hello FabricClient 기본 관리자 역할에 대 한 인증서가 포함 된 X.509 인증서 저장소의 이름입니다. |
| ClientAuthX509FindType |string, 기본값: "FindByThumbprint" |Hello 저장소에 인증서에 대 한 toosearch ClientAuthX509StoreName 지원 값으로 지정 하는 방법을 나타냅니다: FindByThumbprint; FindBySubjectName 합니다. |
| ClientAuthX509FindValue |string, 기본값: "" | 기본 관리자 역할 FabricClient toolocate 인증서를 사용 하는 필터 값을 검색 했습니다. |
| ClientAuthX509FindValueSecondary |string, 기본값: "" |기본 관리자 역할 FabricClient toolocate 인증서를 사용 하는 필터 값을 검색 했습니다. |
| UserRoleClientX509StoreName |string, 기본값: "My" |Hello FabricClient 기본 사용자 역할에 대 한 인증서가 포함 된 X.509 인증서 저장소의 이름입니다. |
| UserRoleClientX509FindType |string, 기본값: "FindByThumbprint" |Hello 저장소에 인증서에 대 한 toosearch UserRoleClientX509StoreName 지원 값으로 지정 하는 방법을 나타냅니다: FindByThumbprint; FindBySubjectName 합니다. |
| UserRoleClientX509FindValue |string, 기본값: "" |기본 사용자 역할 FabricClient에 toolocate 인증서를 사용 하는 필터 값을 검색 합니다. |
| UserRoleClientX509FindValueSecondary |string, 기본값: "" |기본 사용자 역할 FabricClient에 toolocate 인증서를 사용 하는 필터 값을 검색 합니다. |

### <a name="section-name-paas"></a>섹션 이름: Paas
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ClusterId |string, 기본값: "" |구성을 보호하기 위해 패브릭에서 사용하는 X509 인증서 저장소 |

### <a name="section-name-fabrichost"></a>섹션 이름: FabricHost
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| StopTimeout |시간(초), 기본값: 300 |시간 간격은 초 단위로 지정합니다. 호스팅된 서비스 활성화;에 대 한 hello 제한 시간 비활성화 및 업그레이드 합니다. |
| StartTimeout |시간(초), 기본값: 300 |시간 간격은 초 단위로 지정합니다. fabricactivationmanager 시작에 대한 시간 제한 |
| ActivationRetryBackoffInterval |time(초), 기본값: 5 |시간 간격은 초 단위로 지정합니다. 형식의 백오프 간격 오류 hello 시스템에서 toohello MaxActivationFailureCount 구성에 대 한 hello 활성화 다시 시도; 모든 연속 활성화에 대 한 모든 활성화 오류입니다. hello 다시 시도 간격 마다 try에는 연속 활성화 실패 및 hello 활성화 백오프 간격의 제품입니다. |
| ActivationMaxRetryInterval |시간(초), 기본값: 300 |시간 간격은 초 단위로 지정합니다. Activation(활성화)를 위한 최대 다시 시도 간격입니다. 모든 연속 실패 hello 다시 시도 간격 같이 계산 됩니다. Min (ActivationMaxRetryInterval; 연속 실패 횟수 * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |int, 기본값: 10 |이 값은 hello 최대 개수를 시스템에서 다시 시도를 포기 하기 전에 실패 한 정품 인증 합니다. |
| EnableServiceFabricAutomaticUpdates |bool, 기본값: false |이 Windows Update를 통해 tooenable 패브릭 자동 업데이트 합니다. |
| EnableServiceFabricBaseUpgrade |bool, 기본값: false |이 서버에 대 한 기본 업데이트 tooenable입니다. |
| EnableRestartManagement |bool, 기본값: false |이 tooenable 서버를 다시 시작 합니다. |


### <a name="section-name-failovermanager"></a>섹션 이름: FailoverManager
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |time(초), 기본값: 60.0 * 30 |시간 간격은 초 단위로 지정합니다. 지속형된 복제 작동이 중단 될 때; Windows Fabric 복제본 toocome hello에 대 한이 기간에 대 한 백업 하기 전에 대기 (해야 하는 hello 상태 복사본) 새 대체 복제본 만들기. |
| QuorumLossWaitDuration |time(초), 기본값: MaxValue |시간 간격은 초 단위로 지정합니다. 쿼럼 손실 상태에서 파티션 toobe 위해서는 hello 최대 기간입니다. Hello 파티션이 경우 쿼럼 손실에서 여전히;이 기간 후 hello 파티션 복제본 손실으로 아래로 고려 하면 hello에서 쿼럼 손실에서 복구 됩니다. 이 경우 잠재적으로 데이터 손실이 발생할 수 있습니다. |
| UserStandByReplicaKeepDuration |time(초), 기본값: 3600.0 * 24 * 7 |시간 간격은 초 단위로 지정합니다. 보관된 복제본이 중단된 상태에서 돌아올 때 복제본이 이미 대체되었을 수 있습니다. 이 타이머는 FM 삭제 하기 전에 hello 대기 복제본은 유지 기간 hello를 결정 합니다. |
| UserMaxStandByReplicaCount |int, 기본값: 1 |사용자 서비스에 대 한 hello 시스템이 계속 해 서 StandBy 복제본 hello 기본의 최대 수입니다. |

### <a name="section-name-namingservice"></a>섹션 이름: NamingService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| TargetReplicaSetSize |int, 기본값: 7 |복제본의 hello 수 hello 명명 서비스 저장소의 각 파티션에 대 한 설정합니다. 복제본 집합 증가 hello 수준의 안정성 hello 정보 명명 서비스 저장소; hello에 대 한 hello 수가 증가합니다. 줄이면 정보 hello hello 변경; 있는 노드 실패의 결과로 손실 됩니다. Windows Fabric 및 hello 소요 시간이에 로드가 증가의 비용에 걸리는 시간은 tooperform 업데이트 toohello 명명 데이터.|
|MinReplicaSetSize | int, 기본값: 3 | hello 명명 서비스 복제본 데 필요한 최소 수 toowrite toocomplete로 업데이트 합니다. 보다 적은 복제본이 복제본에서 복원 될 때까지이 활성 hello 시스템 hello 안정성 시스템으로에서 업데이트 toohello 명명 서비스 저장소를 거부 합니다. 이 값은 hello TargetReplicaSetSize 보다 많은 일 수 없습니다. |
|ReplicaRestartWaitDuration | time(초), 기본값: 60.0 * 30| 시간 간격은 초 단위로 지정합니다. 이름 지정 서비스 복제본이 중단될 때 이 타이머가 시작됩니다.  Hello FM 만료 될 때 다운 있는 tooreplace hello 복제본 시작 됩니다 (것 고려 하지 않고 아직 분실). |
|QuorumLossWaitDuration | time(초), 기본값: MaxValue | 시간 간격은 초 단위로 지정합니다. 이름 지정 서비스가 쿼럼 손실 상태가 될 때 이 타이머가 시작됩니다.  복제본을 손실;으로 아래로 hello 적용될지 FM hello 인증서 만료 고 toorecover 쿼럼 시도 합니다. 데이터가 손실될 수 있습니다. |
|StandByReplicaKeepDuration | time(초), 기본값: 3600.0 * 2 | 시간 간격은 초 단위로 지정합니다. 이름 지정 서비스 복제본이 중단된 상태에서 돌아올 때 복제본이 이미 대체되었을 수 있습니다.  이 타이머는 FM 삭제 하기 전에 hello 대기 복제본은 유지 기간 hello를 결정 합니다. |
|PlacementConstraints | string, 기본값: "" | 배치 제약 조건에 대 한 hello 서비스 이름을 지정 합니다. |
|ServiceDescriptionCacheLimit | int, 기본값: 0 | hello LRU 서비스 설명에서 캐시에 유지 되는 항목의 최대 수 hello hello 저장소 서비스 이름 지정 (제한 없음 too0 설정 됨). |
|RepairInterval | time(초), 기본값: 5 | 시간 간격은 초 단위로 지정합니다. 간격은 hello hello 기관 소유자와 이름 소유자 사이의 불일치 복구 명명 시작 됩니다. |
|MaxNamingServiceHealthReports | int, 기본값: 10 | 서비스 비정상 보고서를 한 번에 hello 느린 작업 이름 지정을 저장 하는 최대 수입니다. 0인 경우 모든 느린 작업이 전송됩니다. |
| MaxMessageSize |int, 기본값: 4*1024*1024 |hello 명명을 사용 하는 경우 클라이언트 노드 통신에 대 한 최대 메시지 크기입니다. DOS 공격을 낮추려는 경우 기본값은 4MB입니다. |
| MaxFileOperationTimeout |시간(초), 기본값: 30 |시간 간격은 초 단위로 지정합니다. hello 최대 제한 시간 파일 저장소 서비스 작업에 사용할 수 있습니다. 더 큰 시간 제한을 지정하는 요청은 거부됩니다. |
| MaxOperationTimeout |time(초), 기본값: 600 |시간 간격은 초 단위로 지정합니다. hello 최대 시간 제한을 클라이언트 작업에 사용할 수 있습니다. 더 큰 시간 제한을 지정하는 요청은 거부됩니다. |
| MaxClientConnections |int, 기본값: 1000 |hello 최대 게이트웨이 당 클라이언트 연결 수입니다. |
| ServiceNotificationTimeout |시간(초), 기본값: 30 |시간 간격은 초 단위로 지정합니다. hello 서비스 알림 toohello 클라이언트 배달할 때 사용 되는 시간이 초과 되었습니다. |
| MaxOutstandingNotificationsPerClient |int, 기본값: 1000 |클라이언트를 등록 하기 전에 처리 중인 알림의 hello 최대 수 hello 게이트웨이에서 강제로 닫힙니다. |
| MaxIndexedEmptyPartitions |int, 기본값: 1000 |다시 연결 중인 클라이언트를 동기화 하는 데 hello 알림 캐시에 유지 되는 빈 파티션 hello 최대 수가 인덱싱됩니다. 모든 빈 파티션은이 개수를 초과 하는 조회 버전 오름차순의 hello 인덱스에서 제거 됩니다. 도 동기화 및 누락 된 빈 파티션; 업데이트를 수행할 수 클라이언트를 다시 연결 하지만 hello 동기화 프로토콜 더 듭니다. |
| GatewayServiceDescriptionCacheLimit |int, 기본값: 0 |hello LRU 서비스 설명에서 캐시에 유지 되는 항목의 최대 수 hello hello 명명 게이트웨이 (제한 없음 too0 설정 됨). |
| PartitionCount |int, 기본값: 3 |만든 hello 명명 서비스 저장소 toobe의 파티션 hello 수입니다. 각 파티션에 tooits 인덱스; 해당 하는 단일 파티션 키를 소유 합니다. 따라서 파티션 키 [0; PartitionCount) 존재 합니다. 증가 hello 명명 서비스 파티션 수가 늘어날수록 hello 백업 복제본에 보관 데이터의 평균 크기를 줄여 명명 서비스 hello hello 눈금에 수행할 수 있습니다 설정; 리소스의 증가 사용의 비용 (PartitionCount 이후 * ReplicaSetSize 서비스 복제본을 유지 해야) 합니다.|

### <a name="section-name-runas"></a>섹션 이름: RunAs
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| RunAsAccountName |string, 기본값: "" |Hello RunAs 계정 이름을 나타냅니다. "DomainUser" 또는 "ManagedServiceAccount" 계정 유형에만 필요합니다. 유효한 값: "domain\user" 또는 "user@domain" |
|RunAsAccountType|string, 기본값: "" |Hello RunAs 계정 유형을 나타냅니다. RunAs 섹션에 필요합니다. 유효한 값: "DomainUser/NetworkService/ManagedServiceAccount/LocalSystem"|
|RunAsPassword|string, 기본값: "" |Hello RunAs 계정 암호를 나타냅니다. "DomainUser" 계정 유형에만 필요합니다. |

### <a name="section-name-runasfabric"></a>섹션 이름: RunAs_Fabric
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| RunAsAccountName |string, 기본값: "" |Hello RunAs 계정 이름을 나타냅니다. "DomainUser" 또는 "ManagedServiceAccount" 계정 유형에만 필요합니다. 유효한 값: "domain\user" 또는 "user@domain" |
|RunAsAccountType|string, 기본값: "" |Hello RunAs 계정 유형을 나타냅니다. RunAs 섹션에 필요합니다. 유효한 값: "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem" |
|RunAsPassword|string, 기본값: "" |Hello RunAs 계정 암호를 나타냅니다. "DomainUser" 계정 유형에만 필요합니다. |

### <a name="section-name-runashttpgateway"></a>섹션 이름: RunAs_HttpGateway
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| RunAsAccountName |string, 기본값: "" |Hello RunAs 계정 이름을 나타냅니다. "DomainUser" 또는 "ManagedServiceAccount" 계정 유형에만 필요합니다. 유효한 값: "domain\user" 또는 "user@domain" |
|RunAsAccountType|string, 기본값: "" |Hello RunAs 계정 유형을 나타냅니다. RunAs 섹션에 필요합니다. 유효한 값: "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem" |
|RunAsPassword|string, 기본값: "" |Hello RunAs 계정 암호를 나타냅니다. "DomainUser" 계정 유형에만 필요합니다. |

### <a name="section-name-runasdca"></a>섹션 이름: RunAs_DCA
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| RunAsAccountName |string, 기본값: "" |Hello RunAs 계정 이름을 나타냅니다. "DomainUser" 또는 "ManagedServiceAccount" 계정 유형에만 필요합니다. 유효한 값: "domain\user" 또는 "user@domain" |
|RunAsAccountType|string, 기본값: "" |Hello RunAs 계정 유형을 나타냅니다. RunAs 섹션에 필요합니다. 유효한 값: "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem" |
|RunAsPassword|string, 기본값: "" |Hello RunAs 계정 암호를 나타냅니다. "DomainUser" 계정 유형에만 필요합니다. |

### <a name="section-name-httpgateway"></a>섹션 이름: HttpGateway
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
|IsEnabled|bool, 기본값: false | Httpgateway를 hello 하는 설정/해제 합니다. Httpgateway는 기본적으로 해제 하 고이 구성 집합 tooenable toobe 것입니다. |
|ActiveListeners |uint, 기본값: 50 | 읽기 toopost toohello http 서버 큐의 수입니다. Hello hello HttpGateway에서 충족 될 수 있는 동시 요청 수를 제어 합니다. |
|MaxEntityBodySize |uint, 기본값: 4194304 |  Http 요청에서 예상할 수 있는 hello 본문의 hello 최대 크기를 제공 합니다. 기본값은 4MB입니다. 본문 크기가 이 값보다 크면 Httpgateway 요청이 실패합니다. 최소 읽기 청크 크기가 4,096바이트이므로 이 인해 toobe 하므로 > = 4, 096입니다. |
|HttpGatewayHealthReportSendInterval |시간(초), 기본값: 30 | 시간 간격은 초 단위로 지정합니다. hello는 Http 게이트웨이 보내는 hello 간격 누적 상태 보고서 tooHealth 관리자. |

### <a name="section-name-ktllogger"></a>섹션 이름: KtlLogger
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |int, 기본값: 1 | Hello 메모리 설정을 자동으로 하 고 동적으로 구성 해야 나타내는 플래그입니다. 그런 다음 0 hello 메모리 구성 설정을 직접 사용 하 고 변경 하지 마십시오 시스템 조건에 따라. 한 경우 hello 메모리 설정을 자동으로 구성 되 고 변경 될 수 있습니다 system 조건에 따라. |
|WriteBufferMemoryPoolMinimumInKB |int, 기본값: 8388608 |KB tooinitially hello 수가 hello 쓰기 버퍼 메모리 풀에 할당 합니다. 0 사용 하 여 tooindicate 제한이 기본 SharedLogSizeInMB 아래와 일치 해야 합니다. |
|WriteBufferMemoryPoolMaximumInKB | int, 기본값: 0 |최대 버퍼 메모리 풀 toogrow를 쓰기 하는 hello 수 KB tooallow hello입니다. 사용 하 여 0 tooindicate 제한이 없습니다. |
|MaximumDestagingWriteOutstandingInKB | int, 기본값: 0 | hello 전용된 로그 미리 tooadvance 로그를 공유 하는 hello tooallow hello KB 수입니다. 사용 하 여 0 tooindicate 제한이 없습니다.
|SharedLogPath |string, 기본값: "" | 경로 파일 이름 toolocation tooplace 공유 로그 컨테이너입니다. 패브릭 데이터 루트 아래의 기본 경로를 사용하려면 ""을 사용합니다. |
|SharedLogId |string, 기본값: "" |공유 로그 컨테이너에 대한 고유 GUID. 패브릭 데이터 루트 아래의 기본 경로를 사용하는 경우 ""을 사용합니다. |
|SharedLogSizeInMB |int, 기본값: 8192 | MB tooallocate hello 공유 로그 컨테이너에서 hello 수입니다. |

### <a name="section-name-applicationgatewayhttp"></a>섹션 이름: ApplicationGateway/Http
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
|IsEnabled |bool, 기본값: false | 사용 가능/불가능 HttpApplicationGateway hello 합니다. HttpApplicationGateway는 기본적으로 해제 하 고이 구성 집합 tooenable toobe 것입니다. |
|NumberOfParallelOperations | Uint, 기본값: 5000 | 읽기 toopost toohello http 서버 큐의 수입니다. Hello hello HttpGateway에서 충족 될 수 있는 동시 요청 수를 제어 합니다. |
|DefaultHttpRequestTimeout |시간(초). 기본값은 120입니다. |시간 간격은 초 단위로 지정합니다.  Hello http 응용 프로그램 게이트웨이에서 처리 하는 hello http 요청에 대 한 hello 기본 요청 제한 시간을 제공 합니다. |
|ResolveServiceBackoffInterval |time(초), 기본값: 5 |시간 간격은 초 단위로 지정합니다.  실패 한 확인 서비스 작업을 다시 시도 하기 전에 hello 기본 백오프 간격을 제공 합니다. |
|BodyChunkSize |uint, 기본값: 16384 |  제공 hello hello 청크에 크기 (바이트)에서 tooread hello 본문을 사용 합니다. |
|GatewayAuthCredentialType |string, 기본값: "None" | Hello 유형의 보안 자격 증명 toouse hello http 응용 프로그램 게이트웨이 끝점 유효한 값에 있는지를 나타내는 "없음 / X 509입니다. |
|GatewayX509CertificateStoreName |string, 기본값: "My" | http 앱 게이트웨이에 대한 서버 인증서가 있는 X.509 인증서 저장소의 이름 |
|GatewayX509CertificateFindType |string, 기본값: "FindByThumbprint" | Hello 저장소에 인증서에 대 한 toosearch GatewayX509CertificateStoreName 지원 값으로 지정 하는 방법을 나타냅니다: FindByThumbprint; FindBySubjectName 합니다. |
|GatewayX509CertificateFindValue | string, 기본값: "" | Toolocate hello http 응용 프로그램 게이트웨이 인증서를 사용 하는 필터 값을 검색 했습니다. 이 인증서는 hello https 끝점에서 구성 되 고 hello 서비스에 필요한 경우 hello 앱의 사용된 tooverify hello id 수도 있습니다. 먼저 FindValue를 조회하며. 이 FindValue가 없는 경우 FindValueSecondary를 조회합니다. |
|GatewayX509CertificateFindValueSecondary | string, 기본값: "" |Toolocate hello http 응용 프로그램 게이트웨이 인증서를 사용 하는 필터 값을 검색 했습니다. 이 인증서는 hello https 끝점에서 구성 되 고 hello 서비스에 필요한 경우 hello 앱의 사용된 tooverify hello id 수도 있습니다. 먼저 FindValue를 조회하며. 이 FindValue가 없는 경우 FindValueSecondary를 조회합니다.|

### <a name="section-name-management"></a>섹션 이름: Management
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | 연결 문자열 toohello ImageStore에 대 한 루트입니다. |
| ImageStoreMinimumTransferBPS | int, 기본값: 1024 |hello ImageStore hello 클러스터 사이의 최소 전송 속도입니다. 이 값은 외부 ImageStore hello에 액세스 하는 경우 사용 되는 toodetermine hello 제한 시간입니다. 클러스터 toodownload hello에 대 한 시간이 더 외부 ImageStore hello hello 클러스터 사이의 ImageStore hello 대기 시간이 높은 tooallow 경우에이 값을 변경 합니다. |
|AzureStorageMaxWorkerThreads | int, 기본값: 25 | hello 병렬에서 작업자 스레드의 최대 수입니다. |
|AzureStorageMaxConnections | int, 기본값: 5000 | hello 동시 연결 tooazure 저장소의 최대 수입니다. |
|AzureStorageOperationTimeout | time(초), 기본값: 6000 | 시간 간격은 초 단위로 지정합니다. Xstore 작업 toocomplete에 대 한 제한 시간입니다. |
|ImageCachingEnabled | bool, 기본값: true | 이 구성을 통해 tooenable 또는 캐시 사용 안 함 있습니다. |
|DisableChecksumValidation | bool, 기본값: false | 이 구성은 tooenable를 통해 또는 응용 프로그램 프로 비전 하는 동안 체크섬 유효성 검사를 해제 합니다. |
|DisableServerSideCopy | bool, 기본값: false | 이 구성을 사용 하거나 응용 프로그램 프로 비전 하는 동안 hello ImageStore에서 응용 프로그램 패키지의 서버 쪽 복사본을 사용 하지 않도록 설정 합니다. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>섹션 이름: HealthManager/ClusterHealthPolicy
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ConsiderWarningAsError |bool, 기본값: false |클러스터 상태 평가 정책이며, 경고는 오류로 처리됩니다. |
| MaxPercentUnhealthyNodes | int, 기본값: 0 |상태 평가 정책의 클러스터: 클러스터 toobe hello에 대 한 허용 된 비정상 노드의 최대 % 정상입니다. |
| MaxPercentUnhealthyApplications | int, 기본값: 0 |상태 평가 정책의 클러스터: 클러스터 toobe hello에 대 한 허용 된 비정상 응용 프로그램의 최대 백분율 정상입니다. |
|MaxPercentDeltaUnhealthyNodes | int, 기본값: 10 |업그레이드 상태 평가 정책의 클러스터: 클러스터 toobe hello에 대 한 허용 된 델타 비정상 노드의 최대 % 정상입니다. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | int, 기본값: 15 |업그레이드 상태 평가 정책의 클러스터: 클러스터 toobe hello에 대 한 허용 된 최대 업그레이드 도메인의 비정상 노드의 델타에 % 정상입니다.|

### <a name="section-name-faultanalysisservice"></a>섹션 이름: FaultAnalysisService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| TargetReplicaSetSize |int, 기본값: 0 |NOT_PLATFORM_UNIX_START hello TargetReplicaSetSize FaultAnalysisService에 대 한 합니다. |
| MinReplicaSetSize |int, 기본값: 0 |hello MinReplicaSetSize FaultAnalysisService에 대 한 합니다. |
| ReplicaRestartWaitDuration |time(초), 기본값: 60분|시간 간격은 초 단위로 지정합니다. hello ReplicaRestartWaitDuration FaultAnalysisService에 대 한 합니다. |
| QuorumLossWaitDuration | time(초), 기본값: MaxValue |시간 간격은 초 단위로 지정합니다. hello QuorumLossWaitDuration FaultAnalysisService에 대 한 합니다. |
| StandByReplicaKeepDuration| time(초), 기본값: 60*24*7분 |시간 간격은 초 단위로 지정합니다. hello StandByReplicaKeepDuration FaultAnalysisService에 대 한 합니다. |
| PlacementConstraints | string, 기본값: ""| hello PlacementConstraints FaultAnalysisService에 대 한 합니다. |
| StoredActionCleanupIntervalInSeconds | int, 기본값: 3600 |이 얼마나 자주 hello 저장소 정리 됩니다.  터미널 상태에 있는 작업 및 적어도 CompletedActionKeepDurationInSeconds 전에 완료된 작업만 제거합니다. |
| CompletedActionKeepDurationInSeconds | int, 기본값: 604800 | 이 약 시간 tookeep 작업 터미널 상태에 있는입니다.  이 항목에 따라 달라 집니다 StoredActionCleanupIntervalInSeconds; 이후 hello 작업 toocleanup 해당 간격에만 수행 됩니다. 604800은 7일입니다. |
| StoredChaosEventCleanupIntervalInSeconds | int, 기본값: 3600 |이 얼마나 자주 hello 저장소는 감사 정리;에 대 한 이벤트의 hello 수가 30000; 개 이상의 경우 hello 정리 시작 합니다. |

### <a name="section-name-filestoreservice"></a>섹션 이름: FileStoreService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| NamingOperationTimeout |시간(초), 기본값: 60 |시간 간격은 초 단위로 지정합니다. 명명 작업을 수행 하기 위한 hello 제한 시간입니다. |
| QueryOperationTimeout | 시간(초), 기본값: 60 |시간 간격은 초 단위로 지정합니다. 쿼리 작업을 수행 하기 위한 hello 제한 시간입니다. |
| MaxCopyOperationThreads | uint, 기본값: 0 | hello 최대 개수의 병렬 파일이 해당 보조 데이터베이스는 주에서 복사할 수 있습니다. '0'은 코어 수와 동등합니다. |
| MaxFileOperationThreads | uint, 기본값: 100 | 병렬 스레드 수는 허용 된 tooperform FileOperations (복사/이동)에 기본 hello hello 최대 수입니다. '0'은 코어 수와 동등합니다. |
| MaxStoreOperations | uint, 기본값: 4096 |주 복제본에서 허용 되는 병렬 저장소 트랜잭션 작업과 hello 최대 수입니다. '0'은 코어 수와 동등합니다. |
| MaxRequestProcessingThreads | uint, 기본값: 200 |hello 최대 병렬 스레드 수 tooprocess 요청에서에서 허용 hello 기본. '0'은 코어 수와 동등합니다. |
| MaxSecondaryFileCopyFailureThreshold | uint, 기본값: 25| 파일 복사 시도를 포기 하기 전에 보조 hello hello 최대 수입니다. |
| AnonymousAccessEnabled | bool, 기본값: true |익명 액세스 toohello FileStoreService 공유를 사용 하거나 사용 하지 않습니다. |
| PrimaryAccountType | string, 기본값: "" |hello 주의 hello 주 tooACL hello FileStoreService AccountType을 공유합니다. |
| PrimaryAccountUserName | string, 기본값: "" |기본 계정 hello hello 주 tooACL hello FileStoreService 공유의 사용자 이름입니다. |
| PrimaryAccountUserPassword | SecureString, 기본값: 비어 있음 |hello 기본 계정 암호의 hello 주 tooACL hello FileStoreService 공유합니다. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, 기본값: 비어 있음 | 동일한 toogenerated 초기값으로 사용 된 hello 암호 비밀 NTLM 인증을 사용할 때 암호입니다. |
| PrimaryAccountNTLMX509StoreLocation | string, 기본값: "LocalMachine"| NTLM 인증을 사용할 때 PrimaryAccountNTLMPasswordSecret hello에 toogenerate HMAC를 사용 하는 hello X509 인증서의 hello 저장소 위치입니다. |
| PrimaryAccountNTLMX509StoreName | string, 기본값: "MY"| NTLM 인증을 사용할 때 PrimaryAccountNTLMPasswordSecret hello에 toogenerate HMAC를 사용 하는 hello X509 인증서의 hello 저장소 이름입니다. |
| PrimaryAccountNTLMX509Thumbprint | string, 기본값: ""|NTLM 인증을 사용 하는 경우 hello PrimaryAccountNTLMPasswordSecret에서 toogenerate HMAC를 사용 하는 hello X509 인증서의 지문 안녕하세요 합니다. |
| SecondaryAccountType | string, 기본값: ""| hello 보조의 hello 주 tooACL hello FileStoreService AccountType을 공유합니다. |
| SecondaryAccountUserName | string, 기본값: ""| hello 보조 계정 hello 주 tooACL hello FileStoreService 공유의 사용자 이름입니다. |
| SecondaryAccountUserPassword | SecureString, 기본값: 비어 있음 |hello 보조 계정 암호의 hello 주 tooACL hello FileStoreService 공유합니다.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, 기본값: 비어 있음 | 동일한 toogenerated 초기값으로 사용 된 hello 암호 비밀 NTLM 인증을 사용할 때 암호입니다. |
| SecondaryAccountNTLMX509StoreLocation | string, 기본값: "LocalMachine" |NTLM 인증을 사용할 때 SecondaryAccountNTLMPasswordSecret hello에 toogenerate HMAC를 사용 하는 hello X509 인증서의 hello 저장소 위치입니다. |
| SecondaryAccountNTLMX509StoreName | string, 기본값: "MY" |NTLM 인증을 사용할 때 SecondaryAccountNTLMPasswordSecret hello에 toogenerate HMAC를 사용 하는 hello X509 인증서의 hello 저장소 이름입니다. |
| SecondaryAccountNTLMX509Thumbprint | string, 기본값: ""| NTLM 인증을 사용 하는 경우 hello SecondaryAccountNTLMPasswordSecret에서 toogenerate HMAC를 사용 하는 hello X509 인증서의 지문 안녕하세요 합니다. |

### <a name="section-name-imagestoreservice"></a>섹션 이름: ImageStoreService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| 사용 |bool, 기본값: false |hello ImageStoreService에 대 한 플래그를 사용 합니다. |
| TargetReplicaSetSize | int, 기본값: 7 |hello TargetReplicaSetSize ImageStoreService에 대 한 합니다. |
| MinReplicaSetSize | int, 기본값: 3 |hello MinReplicaSetSize ImageStoreService에 대 한 합니다. |
| ReplicaRestartWaitDuration | time(초), 기본값: 60.0 * 30 | 시간 간격은 초 단위로 지정합니다. hello ReplicaRestartWaitDuration ImageStoreService에 대 한 합니다. |
| QuorumLossWaitDuration | time(초), 기본값: MaxValue | 시간 간격은 초 단위로 지정합니다. hello QuorumLossWaitDuration ImageStoreService에 대 한 합니다. |
| StandByReplicaKeepDuration | time(초), 기본값: 3600.0 * 2 | 시간 간격은 초 단위로 지정합니다. hello StandByReplicaKeepDuration ImageStoreService에 대 한 합니다. |
| PlacementConstraints | string, 기본값: "" | hello PlacementConstraints ImageStoreService에 대 한 합니다. |
| ClientUploadTimeout | time(초), 기본값: 1800 |시간 간격은 초 단위로 지정합니다. 최상위 업로드에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
| ClientCopyTimeout | time(초), 기본값: 1800 | 시간 간격은 초 단위로 지정합니다. 최상위 복사본에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
| ClientDownloadTimeout | time(초), 기본값: 1800 | 시간 간격은 초 단위로 지정합니다. 최상위 다운로드에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
| ClientListTimeout | time(초), 기본값: 600 | 시간 간격은 초 단위로 지정합니다. 최상위 목록에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
| ClientDefaultTimeout | time(초), 기본값: 180 | 시간 간격은 초 단위로 지정합니다. 비-업로드/비-다운로드에 대 한 모든 요청에 대 한 제한 시간 값 (예: 존재, 삭제) tooImage 저장소 서비스. |

### <a name="section-name-imagestoreclient"></a>섹션 이름: ImageStoreClient
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ClientUploadTimeout |time(초), 기본값: 1800 | 시간 간격은 초 단위로 지정합니다. 최상위 업로드에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
| ClientCopyTimeout | time(초), 기본값: 1800 | 시간 간격은 초 단위로 지정합니다. 최상위 복사본에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
|ClientDownloadTimeout | time(초), 기본값: 1800 | 시간 간격은 초 단위로 지정합니다. 최상위 다운로드에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
|ClientListTimeout | time(초), 기본값: 600 |시간 간격은 초 단위로 지정합니다. 최상위 목록에 대 한 제한 시간 값 tooImage 저장소 서비스를 요청 합니다. |
|ClientDefaultTimeout | time(초), 기본값: 180 | 시간 간격은 초 단위로 지정합니다. 비-업로드/비-다운로드에 대 한 모든 요청에 대 한 제한 시간 값 (예: 존재, 삭제) tooImage 저장소 서비스. |

### <a name="section-name-tokenvalidationservice"></a>섹션 이름: TokenValidationService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| 공급자 |string, 기본값: "DSTS" |토큰 유효성 검사 공급자 tooenable 쉼표로 구분 된 목록 (올바른 공급자는: DSTS; AAD)입니다. 현재 단일 공급자만 언제든지 사용할 수 있습니다. |

### <a name="section-name-upgradeorchestrationservice"></a>섹션 이름: UpgradeOrchestrationService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| TargetReplicaSetSize |int, 기본값: 0 |hello TargetReplicaSetSize UpgradeOrchestrationService에 대 한 합니다. |
| MinReplicaSetSize |int, 기본값: 0 | hello MinReplicaSetSize UpgradeOrchestrationService에 대 한 합니다.
| ReplicaRestartWaitDuration | time(초), 기본값: 60분| 시간 간격은 초 단위로 지정합니다. hello ReplicaRestartWaitDuration UpgradeOrchestrationService에 대 한 합니다. |
| QuorumLossWaitDuration | time(초), 기본값: MaxValue | 시간 간격은 초 단위로 지정합니다. hello QuorumLossWaitDuration UpgradeOrchestrationService에 대 한 합니다. |
| StandByReplicaKeepDuration | time(초), 기본값: 60*24*7분 | 시간 간격은 초 단위로 지정합니다. hello StandByReplicaKeepDuration UpgradeOrchestrationService에 대 한 합니다. |
| PlacementConstraints | string, 기본값: "" | hello PlacementConstraints UpgradeOrchestrationService에 대 한 합니다. |
| AutoupgradeEnabled | bool, 기본값: true | 목표 상태(goal-state) 파일에 기반한 자동 폴링 및 업그레이드 작업입니다. |
| UpgradeApprovalRequired | bool, 기본값: false | 설정 toomake 코드 업그레이드는 계속 진행 하기 전에 관리자의 승인이 필요 합니다. |

### <a name="section-name-upgradeservice"></a>섹션 이름: UpgradeService
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| PlacementConstraints |string, 기본값: "" |hello PlacementConstraints 업그레이드 서비스에 대 한 합니다. |
| TargetReplicaSetSize | int, 기본값: 3 | hello TargetReplicaSetSize UpgradeService에 대 한 합니다. |
| MinReplicaSetSize | int, 기본값: 2 | hello MinReplicaSetSize UpgradeService에 대 한 합니다. |
| CoordinatorType | string, 기본값: "WUTest"| hello CoordinatorType UpgradeService에 대 한 합니다. |
| BaseUrl | string, 기본값: "" |UpgradeService의 BaseUrl입니다. |
| ClusterId | string, 기본값: "" | UpgradeService의 ClusterId입니다. |
| X509StoreName | string, 기본값: "My"| UpgradeService의 X509StoreName입니다. |
| X509StoreLocation | string, 기본값: "" | UpgradeService의 X509StoreLocation입니다. |
| X509FindType | string, 기본값: ""| UpgradeService의 X509FindType입니다. |
| X509FindValue | string, 기본값: "" | UpgradeService의 X509FindValue입니다. |
| X509SecondaryFindValue | string, 기본값: "" | UpgradeService의 X509SecondaryFindValue입니다. |
| OnlyBaseUpgrade | bool, 기본값: false | UpgradeService의 OnlyBaseUpgrade입니다. |
| TestCabFolder | string, 기본값: "" | UpgradeService의 TestCabFolder입니다. |

### <a name="section-name-securityclientaccess"></a>섹션 이름: Security/ClientAccess
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| CreateName |string, 기본값: "Admin" |이름 지정 URI 만들기에 대한 보안 구성 |
| DeleteName |string, 기본값: "Admin" |이름 지정 URI 삭제에 대한 보안 구성 |
| PropertyWriteBatch |string, 기본값: "Admin" |이름 지정 속성의 쓰기 작업에 대한 보안 구성 |
| CreateService |string, 기본값: "Admin" | 서비스 만들기에 대한 보안 구성 |
| CreateServiceFromTemplate |string, 기본값: "Admin" |템플릿에서 서비스 만들기에 대한 보안 구성 |
| UpdateService |string, 기본값: "Admin" |서비스 업데이트에 대한 보안 구성 |
| DeleteService  |string, 기본값: "Admin" |서비스 삭제에 대한 보안 구성 |
| ProvisionApplicationType |string, 기본값: "Admin" | 응용 프로그램 유형 프로비전에 대한 보안 구성 |
| CreateApplication |string, 기본값: "Admin" | 응용 프로그램 만들기에 대한 보안 구성 |
| DeleteApplication |string, 기본값: "Admin" | 응용 프로그램 삭제에 대한 보안 구성 |
| UpgradeApplication |string, 기본값: "Admin" | 응용 프로그램 업그레이드 시작 또는 중단에 대한 보안 구성 |
| RollbackApplicationUpgrade |string, 기본값: "Admin" | 응용 프로그램 업그레이드 롤백에 대한 보안 구성 |
| UnprovisionApplicationType |string, 기본값: "Admin" | 응용 프로그램 유형 프로비전 해제에 대한 보안 구성 |
| MoveNextUpgradeDomain |string, 기본값: "Admin" | 명시적 업그레이드 도메인으로 응용 프로그램 업그레이드 다시 시작에 대한 보안 구성 |
| ReportUpgradeHealth |string, 기본값: "Admin" | 현재 업그레이드 진행률 hello와 응용 프로그램 업그레이드를 다시 시작에 대 한 보안 구성입니다. |
| ReportHealth |string, 기본값: "Admin" | 상태 보고에 대한 보안 구성 |
| ProvisionFabric |string, 기본값: "Admin" | MSI 및/또는 클러스터 매니페스트 프로비전에 대한 보안 구성 |
| UpgradeFabric |string, 기본값: "Admin" | 클러스터 업그레이드 시작에 대한 보안 구성 |
| RollbackFabricUpgrade |string, 기본값: "Admin" | 클러스터 업그레이드 롤백에 대한 보안 구성 |
| UnprovisionFabric |string, 기본값: "Admin" | MSI 및/또는 클러스터 매니페스트 프로비전 해제에 대한 보안 구성 |
| MoveNextFabricUpgradeDomain |string, 기본값: "Admin" | 명시적 업그레이드 도메인으로 클러스터 업그레이드 다시 시작에 대한 보안 구성 |
| ReportFabricUpgradeHealth |string, 기본값: "Admin" | 현재 업그레이드 진행률 hello와 클러스터 업그레이드를 다시 시작에 대 한 보안 구성입니다. |
| StartInfrastructureTask |string, 기본값: "Admin" | 인프라 작업 시작에 대한 보안 구성 |
| FinishInfrastructureTask |string, 기본값: "Admin" | 인프라 작업 완료에 대한 보안 구성 |
| ActivateNode |string, 기본값: "Admin" | 노드 활성화에 대한 보안 구성 |
| DeactivateNode |string, 기본값: "Admin" | 단일 노드 비활성화에 대한 보안 구성 |
| DeactivateNodesBatch |string, 기본값: "Admin" | 여러 노드 비활성화에 대한 보안 구성 |
| RemoveNodeDeactivations |string, 기본값: "Admin" | 여러 노드에서 비활성화 되돌리기에 대한 보안 구성 |
| GetNodeDeactivationStatus |string, 기본값: "Admin" | 비활성화 상태 검사에 대한 보안 구성 |
| NodeStateRemoved |string, 기본값: "Admin" | 제거된 노드 상태 보고에 대한 보안 구성 |
| RecoverPartition |string, 기본값: "Admin" | 단일 파티션 복구에 대한 보안 구성 |
| RecoverPartitions |string, 기본값: "Admin" | 여러 파티션 복구에 대한 보안 구성 |
| RecoverServicePartitions |string, 기본값: "Admin" | 서비스 파티션 복구에 대한 보안 구성 |
| RecoverSystemPartitions |string, 기본값: "Admin" | 시스템 서비스 파티션 복구에 대한 보안 구성 |
| ReportFault |string, 기본값: "Admin" | 오류 보고에 대한 보안 구성 |
| InvokeInfrastructureCommand |string, 기본값: "Admin" | 인프라 작업 관리 명령에 대한 보안 구성 |
| FileContent |string, 기본값: "Admin" | 이미지에 대 한 보안 구성 클라이언트 파일 전송 (외부 toocluster)를 저장 합니다. |
| FileDownload |string, 기본값: "Admin" | 이미지 저장소 클라이언트 파일 다운로드 시작 (외부 toocluster)에 대 한 보안 구성입니다. |
| InternalList |string, 기본값: "Admin" | 이미지 저장소 클라이언트 파일 목록 작업(내부)에 대한 보안 구성 |
| 삭제 |string, 기본값: "Admin" | 이미지 저장소 클라이언트 삭제 작업에 대한 보안 구성 |
| 업로드 |string, 기본값: "Admin" | 이미지 저장소 클라이언트 업로드 작업에 대한 보안 구성 |
| GetStagingLocation |string, 기본값: "Admin" | 이미지 저장소 클라이언트 스테이징 위치 검색에 대한 보안 구성 |
| GetStoreLocation |string, 기본값: "Admin" | 이미지 저장소 클라이언트 저장소 위치 검색에 대한 보안 구성 |
| NodeControl |string, 기본값: "Admin" | 노드 시작, 중지 및 다시 시작에 대한 보안 구성 |
| CodePackageControl |string, 기본값: "Admin" | 코드 패키지 다시 시작에 대한 보안 구성 |
| UnreliableTransportControl |string, 기본값: "Admin" | 동작 추가 및 제거에 대한 신뢰할 수 없는 전송 |
| MoveReplicaControl |string, 기본값: "Admin" | 복제본 이동 |
| PredeployPackageToNode |string, 기본값: "Admin" | 배포 전 API |
| StartPartitionDataLoss |string, 기본값: "Admin" | 파티션에 데이터 손실을 유도합니다. |
| StartPartitionQuorumLoss |string, 기본값: "Admin" | 파티션에 쿼럼 손실을 유도합니다. |
| StartPartitionRestart |string, 기본값: "Admin" | 동시에 있는 파티션의 전체 또는 일부 hello 복제본 다시 시작합니다. |
| CancelTestCommand |string, 기본값: "Admin" | 실행 중인 특정 TestCommand를 취소합니다. |
| StartChaos |string, 기본값: "Admin" | 아직 시작되지 않은 Chaos(격리 안 함)를 시작합니다. |
| StopChaos |string, 기본값: "Admin" | 시작된 Chaos를 중지합니다. |
| StartNodeTransition |string, 기본값: "Admin" | 노드 전환 시작에 대한 보안 구성 |
| StartClusterConfigurationUpgrade |string, 기본값: "Admin" | 파티션에 StartClusterConfigurationUpgrade를 유도합니다. |
| GetUpgradesPendingApproval |string, 기본값: "Admin" | 파티션에 GetUpgradesPendingApproval을 유도합니다. |
| StartApprovedUpgrades |string, 기본값: "Admin" | 파티션에 StartApprovedUpgrades를 유도합니다. |
| Ping |string, 기본값: "Admin\|\|User" | 클라이언트 ping에 대한 보안 구성 |
| 쿼리 |string, 기본값: "Admin\|\|User" | 쿼리에 대한 보안 구성 |
| NameExists |string, 기본값: "Admin\|\|User" | 이름 지정 URI 존재 확인에 대한 보안 구성 |
| EnumerateSubnames |string, 기본값: "Admin\|\|User" | 이름 지정 URI 열거형에 대한 보안 구성 |
| EnumerateProperties |string, 기본값: "Admin\|\|User" | 이름 지정 속성 열거형에 대한 보안 구성 |
| PropertyReadBatch |string, 기본값: "Admin\|\|User" | 이름 지정 속성 읽기 작업에 대한 보안 구성 |
| GetServiceDescription |string, 기본값: "Admin\|\|User" | 장기 폴링 서비스 알림 및 읽기 서비스 설명에 대한 보안 구성 |
| ResolveService |string, 기본값: "Admin\|\|User" | 불만 기반 서비스 확인에 대한 보안 구성 |
| ResolveNameOwner |string, 기본값: "Admin\|\|User" | 이름 지정 URI 소유자 확인에 대한 보안 구성 |
| ResolvePartition |string, 기본값: "Admin\|\|User" | 시스템 서비스 확인에 대한 보안 구성 |
| ServiceNotifications |string, 기본값: "Admin\|\|User" | 이벤트 기반 서비스 알림에 대한 보안 구성 |
| PrefixResolveService |string, 기본값: "Admin\|\|User" | 불만 기반 서비스 접두사 확인에 대한 보안 구성 |
| GetUpgradeStatus |string, 기본값: "Admin\|\|User" | 응용 프로그램 업그레이드 상태 폴링에 대한 보안 구성 |
| GetFabricUpgradeStatus |string, 기본값: "Admin\|\|User" | 클러스터 업그레이드 상태 폴링에 대한 보안 구성 |
| InvokeInfrastructureQuery |string, 기본값: "Admin\|\|User" | 인프라 작업 쿼리에 대한 보안 구성 |
| 나열 |string, 기본값: "Admin\|\|User" | 이미지 저장소 클라이언트 파일 목록 작업에 대한 보안 구성 |
| ResetPartitionLoad |string, 기본값: "Admin\|\|User" | failoverUnit의 로드 다시 설정에 대한 보안 구성 |
| ToggleVerboseServicePlacementHealthReporting | string, 기본값: "Admin\|\|User" | Verbose ServicePlacement HealthReporting 전환에 대한 보안 구성 |
| GetPartitionDataLossProgress | string, 기본값: "Admin\|\|User" | Invoke 데이터 손실 api 호출에 대 한 hello 진행률을 인출합니다. |
| GetPartitionQuorumLossProgress | string, 기본값: "Admin\|\|User" | Invoke 쿼럼 손실 api 호출에 대 한 hello 진행률을 인출합니다. |
| GetPartitionRestartProgress | string, 기본값: "Admin\|\|User" | 다시 시작 파티션 api 호출에 대 한 hello 진행률을 인출합니다. |
| GetChaosReport | string, 기본값: "Admin\|\|User" | 특정된 시간 범위 내에 감사 드립니다 hello 상태를 인출합니다. |
| GetNodeTransitionProgress | string, 기본값: "Admin\|\|User" | 노드 전환 명령의 진행률 가져오기에 대한 보안 구성 |
| GetClusterConfigurationUpgradeStatus | string, 기본값: "Admin\|\|User" | 파티션에 GetClusterConfigurationUpgradeStatus를 유도합니다. |
| GetClusterConfiguration | string, 기본값: "Admin\|\|User" | 파티션에 GetClusterConfiguration을 유도합니다. |

### <a name="section-name-reconfigurationagent"></a>섹션 이름: ReconfigurationAgent
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | time(초), 기본값: 900 |시간 간격은 초 단위로 지정합니다. 시스템은 닫기를에 갇힌 복제본이 있는 서비스 호스트를 종료 하기 전에 대기 하는 hello에 대 한 hello 기간입니다. |
| ServiceApiHealthDuration | time(초), 기본값: 30분 | 시간 간격은 초 단위로 지정합니다. ServiceApiHealthDuration 기간은 म 기다리지 서비스 API toorun 비정상적인 것 보고 하기 전에 정의 합니다. |
| ServiceReconfigurationApiHealthDuration | 시간(초), 기본값: 30 | 시간 간격은 초 단위로 지정합니다. ServiceReconfigurationApiHealthDuration 기간에 재구성 서비스 전에 hello 비정상으로 보고 되는지 정의 합니다. |
| PeriodicApiSlowTraceInterval | time(초), 기본값: 5분 | 시간 간격은 초 단위로 지정합니다. PeriodicApiSlowTraceInterval은 hello API 모니터에 의해 투사 됩니다 API에 대 한 느린 호출이 있는 hello 간격을 정의 합니다. |
| NodeDeactivationMaxReplicaCloseDuration | time(초), 기본값: 900 | 시간 간격은 초 단위로 지정합니다. 노드 비활성화를 차단 하는 서비스 호스트를 종료 하기 전에 hello 최대 시간 toowait 합니다. |
| FabricUpgradeMaxReplicaCloseDuration | time(초), 기본값: 900 | 시간 간격은 초 단위로 지정합니다. hello 최대 기간 RA 닫는 중이기 복제 데이터베이스의 서비스 호스트를 종료 하기 전에 대기 합니다. |
| IsDeactivationInfoEnabled | bool, 기본값: true | 이 구성은 업그레이드 하는 기존 클러스터에 대 한 tootrue 설정 해야 하는 새 클러스터에 대 한 기본 다시 투표를 수행 하기 위한 RA가 비활성화 정보를 사용할지 여부를 결정 방법에 hello 릴리스 정보를 참조 하십시오 tooenable이 있습니다. |

### <a name="section-name-placementandloadbalancing"></a>섹션 이름: PlacementAndLoadBalancing
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| TraceCRMReasons |bool, 기본값: true |CRM tootrace 이유 움직임 toohello operational 이벤트 채널 발급 하는지 여부를 지정 합니다. |
| ValidatePlacementConstraint | bool, 기본값: true | 서비스의 ServiceDescription이 업데이트 될 때 서비스에 대 한 식을 PlacementConstraint hello 유효성을 검사할지 여부를 지정 합니다. |
| PlacementConstraintValidationCacheSize | int, 기본값: 10000 | 제한 hello 빠른 유효성 검사에 사용 되 고 배치 제약 조건 식의 캐싱을 hello 테이블의 크기입니다. |
|VerboseHealthReportLimit | int, 기본값: 20 | (자세한 상태 보고가 활성화 됨) 하는 경우 상태 경고에 대 한 보고 되기 전에 복제본의 위치가 지정 되지 않은 toogo 횟수 hello를 정의 합니다. |
|ConstraintViolationHealthReportLimit | int, 기본값: 50 | 복제본을 위반 하는 제약 조건에 toobe 전에 진단이 수행 되 고 상태 보고서 보내지는 영구적으로 고정 되지 않은 횟수 hello를 정의 합니다. |
|DetailedConstraintViolationHealthReportLimit | int, 기본값: 200 | 복제본을 위반 하는 제약 조건에 toobe 진단을 수행 하 고 세부 상태 보고서 보내지는 전에 영구적으로 고정 되지 않은 횟수 hello를 정의 합니다. |
|DetailedVerboseHealthReportLimit | int, 기본값: 200 | Hello 횟수는 위치가 지정 되지 않은 복제본의 toobe 세부 상태 보고서를 내보냅니다 전에 위치가 지정 되지 않은 지속적으로 정의 합니다. |
|ConsecutiveDroppedMovementsHealthReportLimit | int, 기본값: 20 | Hello 연속 횟수 ResourceBalancer 발급 이동 전에 진단이 수행 되 고 상태 경고 보내지는 끌어다 놓은 정의 합니다. 음수: 이 조건에서는 경고를 내보내지 않습니다. |
|DetailedNodeListLimit | int, 기본값: 15 | 위치가 지정 되지 않은 복제본을 보고 하는 hello에 hello 잘림 하기 전에 제약 조건 tooinclude 당 최대 노드 수를 정의 합니다. |
|DetailedPartitionListLimit | int, 기본값: 15 | 진단을에 hello 잘림 하기 전에 제약 조건 tooinclude에 대 한 진단 엔트리 당 파티션 수를 정의합니다. |
|DetailedDiagnosticsInfoListLimit | int, 기본값: 15 | 진단에서의 잘림과 하기 전에 제약 조건 tooinclude 당 hello (세부 정보가 포함 된) 진단 항목 수를 정의합니다.|
|PLBRefreshGap | time(초), 기본값: 1 | 시간 간격은 초 단위로 지정합니다. PLB 상태를 다시 새로 고칩니다 전에 경과 해야 하는 시간의 hello 최소 크기를 정의 합니다. |
|MinPlacementInterval | time(초), 기본값: 1 | 시간 간격은 초 단위로 지정합니다. 두 개의 연속 된 배치 반올림 하기 전에 경과 해야 하는 시간의 hello 최소 크기를 정의 합니다. |
|MinConstraintCheckInterval | time(초), 기본값: 1 | 시간 간격은 초 단위로 지정합니다. Hello 최소한 두 개의 연속 된 제약 조건 라운드 확인 전에 경과 해야 하는 시간을 정의 합니다. |
|MinLoadBalancingInterval | time(초), 기본값: 5 | 시간 간격은 초 단위로 지정합니다. 두 개의 연속 된 분산 반올림 하기 전에 경과 해야 하는 시간의 hello 최소 크기를 정의 합니다. |
|BalancingDelayAfterNodeDown | time(초), 기본값: 120 |시간 간격은 초 단위로 지정합니다. 노드 작동 중단 이벤트 이후 이 기간 내에 작업 분산을 시작하면 안됩니다. |
|BalancingDelayAfterNewNode | time(초), 기본값: 120 |시간 간격은 초 단위로 지정합니다. 새 노드를 추가한 이후 이 기간 내에 작업 분산을 시작하면 안됩니다. |
|ConstraintFixPartialDelayAfterNodeDown | time(초), 기본값: 120 | 시간 간격은 초 단위로 지정합니다. 노드 작동 중단 이후 이 기간 내에 FaultDomain 및 UpgradeDomain 제한 조건 위반을 수정하면 안됩니다. |
|ConstraintFixPartialDelayAfterNewNode | time(초), 기본값: 120 | 시간 간격은 초 단위로 지정합니다. 새 노드를 추가한 이후 이 기간 내에 FaultDomain 및 UpgradeDomain 제약 조건 위반을 수정하면 안됩니다. |
|GlobalMovementThrottleThreshold | uint, 기본값: 1000 | 이동에 허용 된 최대 수에 hello 지난 단계 분산 hello 간격 GlobalMovementThrottleCountingInterval로 표시 합니다. |
|GlobalMovementThrottleThresholdForPlacement | uint, 기본값: 0 | 이동의 최대 수에에서 사용할 수 배치 단계에서 지난 hello GlobalMovementThrottleCountingInterval.0에 표시 된 간격에 제한이 없음을 나타냅니다.|
|GlobalMovementThrottleThresholdForBalancing | uint, 기본값: 0 | 이동 지난 hello에 분산 하는 단계에 사용할 수의 최대 수 간격 GlobalMovementThrottleCountingInterval로 표시 합니다. 0은 제한하지 않음을 나타냅니다. |
|GlobalMovementThrottleCountingInterval | time(초), 기본값: 600 | 시간 간격은 초 단위로 지정합니다. Hello의 hello 길이 나타내는 과거 어떤 tootrack 당 도메인 복제본 움직임 (GlobalMovementThrottleThreshold 함께 사용 됨)에 대 한 간격입니다. 설정할 수 있습니다 too0 tooignore 글로벌 완전히 제한 합니다. |
|MovementPerPartitionThrottleThreshold | uint, 기본값: 50 | 해당 파티션의 복제본에 대 한 관련된 움직임 분산 hello 수에 도달 했거나 MovementPerFailoverUnitThrottleThreshold 지난 hello를 초과 하는 경우 파티션에 대 한 이동 실시할와 관련 된 분산 없음 간격으로 표시 MovementPerPartitionThrottleCountingInterval 합니다. |
|MovementPerPartitionThrottleCountingInterval | time(초), 기본값: 600 | 시간 간격은 초 단위로 지정합니다. Hello의 hello 길이 나타냅니다 (MovementPerPartitionThrottleThreshold 함께 사용 됨) 각 파티션에 대 한 어떤 tootrack 복제본 이동에 대 한 간격 이전 합니다. |
|PlacementSearchTimeout | time(초), 기본값: 0.5 | 시간 간격은 초 단위로 지정합니다. 서비스를 배치할 때 결과를 반환하기 전까지 이 기간에서 최대한 오랫동안 검색합니다. |
|UseMoveCostReports | bool, 기본값: false | 점수 매기기 함수; hello의 hello LB tooignore hello 비용 요소를 지시 합니다. 잠재적으로 많은 수의 더 균형 잡힌된 배치에 대 한 이동으로 인해 발생 합니다. |
|PreventTransientOvercommit | bool, 기본값: false | PLB 즉시 계산 해야 시작 hello 이동 하 여를 확보할 수 있는 리소스에 따라 결정 됩니다. 기본적으로 PLB 밖에 시작한을 일시적인 만들 수 있는 동일한 노드 과도 hello에서으로 이동 합니다. 이 매개 변수 tootrue 프로그램이 설정 된 종류의 overcommits 및 주문형으로 조각 모음 (즉, placementWithMove)를 사용할 수 없습니다. |
|InBuildThrottlingEnabled | bool, 기본값: false | Hello 빌드에 제한이 사용 되는지 여부를 결정 합니다. |
|InBuildThrottlingAssociatedMetric | string, 기본값: "" | hello이 제한에 대 한 메트릭 이름을 연결 합니다. |
|InBuildThrottlingGlobalMaxValue | int, 기본값: 0 |hello 전역으로 허용 하는 빌드에 복제본의 최대 수입니다. |
|SwapPrimaryThrottlingEnabled | bool, 기본값: false| Hello 스왑 기본 제한이 사용 되는지 여부를 결정 합니다. |
|SwapPrimaryThrottlingAssociatedMetric | string, 기본값: ""| hello이 제한에 대 한 메트릭 이름을 연결 합니다. |
|SwapPrimaryThrottlingGlobalMaxValue | int, 기본값: 0 | hello 전역으로 허용 스왑 주 복제본의 최대 수입니다. |
|PlacementConstraintPriority | int, 기본값: 0 | 배치 제약 조건 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|PreferredLocationConstraintPriority | int, 기본값: 2| 기본 위치 제약 조건 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 2: 최적화; 음수: 무시 |
|CapacityConstraintPriority | int, 기본값: 0 | 용량 제약 조건의 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|AffinityConstraintPriority | int, 기본값: 0 | 선호도 제약 조건의 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|FaultDomainConstraintPriority | int, 기본값: 0 | 오류 도메인 제약 조건의 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|UpgradeDomainConstraintPriority | int, 기본값: 1| 업그레이드 도메인 제약 조건의 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|ScaleoutCountConstraintPriority | int, 기본값: 0 | Hello 수 제약 조건 확장 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|ApplicationCapacityConstraintPriority | int, 기본값: 0 | 용량 제약 조건의 hello 우선 순위를 결정: 0: 하드; 1: 소프트; 음수: 무시 합니다. |
|MoveParentToFixAffinityViolation | bool, 기본값: false | 부모 복제본이 될 수 있도록 결정 하는 설정 toofix 선호도 제약 조건 이동 합니다.|
|MoveExistingReplicaForPlacement | bool, 기본값: true |설정 하는 경우를 결정 하는 배치 하는 동안 기존 복제본 toomove 합니다. |
|UseSeparateSecondaryLoad | bool, 기본값: true | 다른 보조 로드를 사용할지 여부를 결정하는 설정 |
|PlaceChildWithoutParent | bool, 기본값: true | 부모 복제본이 없는 경우 자식 서비스 복제본을 배치할 수 있는지 여부를 결정하는 설정 |
|PartiallyPlaceServices | bool, 기본값: true | 제한된 적합한 노드가 지정되면 클러스터에 있는 모든 서비스 복제본을 "모두 배치하거나 전혀 배치하지 않을지"를 결정합니다.|
|InterruptBalancingForAllFailoverUnitUpdates | bool, 기본값: false | 모든 유형의 장애 조치(failover) 단위 업데이트에서 고속 또는 저속 분산 실행을 중단해야 하는지 여부를 결정합니다. "false"로 지정한 경우 FailoverUnit:가 만들어지거나 삭제되거나, 복제본이 누락되거나, 주 복제본 위치가 변경되거나, 복제본 수가 변경되면 분산 실행이 중단됩니다. 다른 경우, 즉 FailoverUnit:에 여분의 복제본이 있거나, 모든 복제본 플래그가 변경되거나, 파티션 버전만 변경되거나, 기타 모든 경우에는 분산 실행이 중단되지 않습니다. |

### <a name="section-name-security"></a>섹션 이름: Security
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ClusterProtectionLevel |None 또는 EncryptAndSign |비보안 클러스터의 경우 None(기본값), 보안 클러스터의 경우 EncryptAndSign |

### <a name="section-name-hosting"></a>섹션 이름: Hosting
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |시간(초), 기본값: 300 |등록 된 패브릭 hello ServiceType toobe에 허용 된 최대 시간 |
| ServiceTypeDisableFailureThreshold |정수, 기본값: 1 |Hello FailoverManager (FM) 이후에 실패 횟수를 받을 toodisable hello 서비스 유형이 해당 노드와 시도 배치에 대 한 다른 노드로 hello 임계값입니다. |
| ActivationRetryBackoffInterval |시간(초), 기본값: 5 |모든 정품 인증 실패 시 형식의 백오프 간격 모든 연속 활성화 실패 시 hello 시스템 재시도 대 한 활성화 toohello MaxActivationFailureCount hello 합니다. hello 다시 시도 간격 마다 try에는 연속 활성화 실패 및 hello 활성화 백오프 간격의 제품입니다. |
| ActivationMaxRetryInterval |시간(초), 기본값: 300 |모든 연속 활성화 실패 시 hello 시스템 재시도 대 한 활성화 tooActivationMaxFailureCount hello 합니다. ActivationMaxRetryInterval은 모든 활성화 실패 후 다시 시도하기 전에 대기 시간 간격을 지정합니다. |
| ActivationMaxFailureCount |정수, 기본값: 10 |시스템이 포기하기 전에 실패한 활성화를 다시 시도하는 횟수 |

### <a name="section-name-failovermanager"></a>섹션 이름: FailoverManager
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |시간(초), 기본값: 10 |빈도 결정 하는이 새 부하 보고서에 대 한 FM 확인 hello |

### <a name="section-name-federation"></a>섹션 이름: Federation
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| LeaseDuration |시간(초), 기본값: 30 |노드 및 해당 이웃 노드 간에 임대가 지속되는 기간 |
| LeaseDurationAcrossFaultDomain |시간(초), 기본값: 30 |장애 도메인에서 노드 및 해당 이웃 노드 간에 임대가 지속되는 기간 |

### <a name="section-name-clustermanager"></a>섹션 이름: ClusterManager
| **매개 변수** | **허용되는 값** | **지침 또는 간단한 설명** |
| --- | --- | --- |
| UpgradeStatusPollInterval |시간(초), 기본값: 60 |응용 프로그램 업그레이드 상태에 대 한 폴링의 hello 주파수입니다. 이 값이 업데이트 한 모든 GetApplicationUpgradeProgress 호출에 대 한 hello 속도 결정합니다. |
| UpgradeHealthCheckInterval |시간(초), 기본값: 60 |모니터링 된 응용 프로그램 업그레이드 중 hello 주파수 상태 확인 |
| FabricUpgradeStatusPollInterval |시간(초), 기본값: 60 |Fabric 업그레이드 상태에 대 한 폴링의 hello 주파수입니다. 이 값이 업데이트 한 모든 GetFabricUpgradeProgress 호출에 대 한 hello 속도 결정합니다. |
| FabricUpgradeHealthCheckInterval |시간(초), 기본값: 60 |모니터링 대상된 Fabric 업그레이드 하는 동안 상태 검사의 hello 빈도 |
|InfrastructureTaskProcessingInterval | 시간(초), 기본값: 10 |시간 간격은 초 단위로 지정합니다. hello 처리 간격 hello 인프라 작업을 처리 상태 시스템에서 사용 합니다. |
|TargetReplicaSetSize |int, 기본값: 7 |hello TargetReplicaSetSize ClusterManager에 대 한 합니다. |
|MinReplicaSetSize |int, 기본값: 3 |hello MinReplicaSetSize ClusterManager에 대 한 합니다. |
|ReplicaRestartWaitDuration |time(초), 기본값: 60.0 * 30|시간 간격은 초 단위로 지정합니다. hello ReplicaRestartWaitDuration ClusterManager에 대 한 합니다. |
|QuorumLossWaitDuration |time(초), 기본값: MaxValue | 시간 간격은 초 단위로 지정합니다. hello QuorumLossWaitDuration ClusterManager에 대 한 합니다. |
|StandByReplicaKeepDuration | time(초), 기본값: 3600.0 * 2|시간 간격은 초 단위로 지정합니다. hello StandByReplicaKeepDuration ClusterManager에 대 한 합니다. |
|PlacementConstraints | string, 기본값: "" |hello PlacementConstraints ClusterManager에 대 한 합니다. |
|SkipRollbackUpdateDefaultService | bool, 기본값: false |CM hello에서 되돌리는 중 업데이트 된 기본 서비스 응용 프로그램 업그레이드 롤백 중 건너뜁니다. |
|EnableDefaultServicesUpgrade | bool, 기본값: false |응용 프로그램 업그레이드 중에 기본 서비스 업그레이드를 사용하도록 설정합니다. 업그레이드 후에 기본 서비스 설명을 덮어씁니다. |
|InfrastructureTaskHealthCheckWaitDuration |time(초), 기본값: 0| 시간 간격은 초 단위로 지정합니다. 사후 인프라 작업을 처리 한 후 상태 검사를 시작 하기 전에 시간 toowait hello 양입니다. |
|InfrastructureTaskHealthCheckStableDuration | time(초), 기본값: 0| 시간 간격은 초 단위로 지정합니다. hello 양의 시간 tooobserve 연속 전달 된 상태 인프라 작업의 사후 처리가 성공적으로 완료 되기 전에 확인 합니다. 실패한 상태 검사를 관찰하면 이 타이머가 다시 설정됩니다. |
|InfrastructureTaskHealthCheckRetryTimeout | 시간(초), 기본값: 60 |시간 간격은 초 단위로 지정합니다. 사후 인프라 작업을 처리 하는 동안 실패 한 상태 검사를 다시 시도 시간 toospend hello 양입니다. 통과한 상태 검사를 관찰하면 이 타이머가 다시 설정됩니다. |
|ImageBuilderTimeoutBuffer |time(초), 기본값: 3 |시간 간격은 초 단위로 지정합니다. Image Builder 지정 제한 시간 오류 tooreturn toohello 클라이언트에 대 한 시간 tooallow hello 양입니다. 버퍼가 너무 작습니다;이 경우 그런 다음 hello 클라이언트 hello 서버 전환 하기 전에 제한 시간이 초과 하 고 일반 시간 제한 오류를 가져옵니다. |
|MinOperationTimeout | 시간(초), 기본값: 60 |시간 간격은 초 단위로 지정합니다. 내부적으로 ClusterManager에 대 한 작업을 처리 하기 위한 최소 글로벌 시간 제한을 hello 합니다. |
|MaxOperationTimeout |time(초), 기본값: MaxValue | 시간 간격은 초 단위로 지정합니다. 내부적으로 ClusterManager에 대 한 작업을 처리 하기 위한 최대 글로벌 시간 제한을 hello 합니다. |
|MaxTimeoutRetryBuffer | time(초), 기본값: 600 |시간 간격은 초 단위로 지정합니다. 최대 작업 시간 초과 hello tootimeouts은 내부적으로 due을 다시 시도 <Original Timeout>  +  <MaxTimeoutRetryBuffer>합니다. 추가 시간 제한은 MinOperationTimeout 증분 단위로 추가됩니다. |
|MaxCommunicationTimeout |time(초), 기본값: 600 |시간 간격은 초 단위로 지정합니다. ClusterManager 및 기타 시스템 서비스 간의 내부 통신에 대 한 최대 제한 시간 (즉, hello 서비스 이름 지정 장애 조치 관리자 및 등)입니다. 각 클라이언트 작업의 시스템 구성 요소 간에 여러 통신이 있을 수 있으므로 이 시간 제한은 전역 MaxOperationTimeout보다 작아야 합니다. |
|MaxDataMigrationTimeout |time(초), 기본값: 600 |시간 간격은 초 단위로 지정합니다. hello Fabric 업그레이드 이루어진 후 데이터 마이그레이션 복구 작업에 대 한 최대 제한 시간입니다. |
|MaxOperationRetryDelay |time(초), 기본값: 5| 시간 간격은 초 단위로 지정합니다. 오류가 발생 한 경우 내부 재시도 대 한 hello 최대 지연입니다. |
|ReplicaSetCheckTimeoutRollbackOverride |time(초), 기본값: 1200 | 시간 간격은 초 단위로 지정합니다. ReplicaSetCheckTimeout dword; toohello 최대 값으로 설정 되어 있는 경우 그런 다음 rollback의 hello 목적을 위해이 구성의 hello 값으로 재정의 하는 합니다. 롤포워드가에 사용 된 hello 값은 절대로 재정의 되지 않습니다. |
|ImageBuilderJobQueueThrottle |int, 기본값: 10 |응용 프로그램 요청의 이미지 작성기 프록시 작업 큐에 대한 스레드 수 제한입니다. |

## <a name="next-steps"></a>다음 단계
클러스터 관리에 대한 자세한 내용은 다음 문서를 읽어보세요.

[Azure 클러스터에서 인증서 추가, 롤오버, 제거 ](service-fabric-cluster-security-update-certs-azure.md) 

