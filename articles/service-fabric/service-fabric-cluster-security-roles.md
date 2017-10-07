---
title: "Service Fabric 클러스터 보안: 클라이언트 역할 | Microsoft Docs"
description: "이 문서에는 hello 두 클라이언트 역할 및 toohello 역할을 제공 하는 hello 권한에 대해 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>서비스 패브릭 클라이언트용 역할 기반 액세스 제어
Azure 서비스 패브릭 연결된 tooa 서비스 패브릭 클러스터에 있는 클라이언트에 대 한 두 개의 서로 다른 액세스 제어 유형을 지원: 관리자와 사용자입니다. 액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다.  

**관리자** 기능이 대 한 모든 권한을 toomanagement (읽기/쓰기 기능만 포함). 기본적으로 **사용자** 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스를 하나만 있습니다.

각각에 대해 별도 인증서를 제공 하 여 클러스터 생성 hello 시 hello 두 클라이언트 역할 (관리자 및 클라이언트)을 지정 합니다. 안전한 서비스 패브릭 클러스터를 설정하는 방법에 대한 자세한 내용은 [서비스 패브릭 클러스터 보안](service-fabric-cluster-security.md) 을 참조하세요.

## <a name="default-access-control-settings"></a>기본 액세스 제어 설정
hello 관리자 액세스 제어 형식에 대 한 모든 권한을 tooall hello FabricClient Api 있습니다. 모든 읽기 및 쓰기 작업을 수행 하는 hello를 포함 하 여 hello 서비스 패브릭 클러스터에서 수행할 수 있습니다.:

### <a name="application-and-service-operations"></a>응용 프로그램 및 서비스 작업
* **CreateService**: 서비스 만들기                             
* **CreateServiceFromTemplate**: 템플릿에서 서비스 만들기                             
* **UpdateService**: 서비스 업데이트                             
* **DeleteService**: 서비스 삭제                             
* **ProvisionApplicationType**: 응용 프로그램 형식 프로비전                             
* **CreateApplication**: 응용 프로그램 만들기                               
* **DeleteApplication**: 응용 프로그램 삭제                             
* **UpgradeApplication**: 응용 프로그램 업그레이드 시작 또는 중단                             
* **UnprovisionApplicationType**: 응용 프로그램 형식 프로비전 해제                             
* **MoveNextUpgradeDomain**: 명시적 업데이트 도메인으로 응용 프로그램 업그레이드 다시 시작                             
* **ReportUpgradeHealth**: hello 현재 업그레이드 진행률와 응용 프로그램 업그레이드를 다시 시작                             
* **ReportHealth**: 상태 보고                             
* **PredeployPackageToNode**: 사전 배포 API                            
* **CodePackageControl**: 코드 패키지 다시 시작                             
* **RecoverPartition**: 파티션 복구                             
* **RecoverPartitions**: 파티션 복구                             
* **RecoverServicePartitions**: 서비스 파티션 복구                             
* **RecoverSystemPartitions**: 시스템 서비스 파티션 복구                             

### <a name="cluster-operations"></a>클러스터 작업
* **ProvisionFabric**: MSI 및/또는 클러스터 매니페스트 프로비전                             
* **UpgradeFabric**: 클러스터 업그레이드 시작                             
* **UnprovisionFabric**: MSI 및/또는 클러스터 매니페스트 프로비전 해제                         
* **MoveNextFabricUpgradeDomain**: 명시적 업데이트 도메인으로 클러스터 업그레이드 다시 시작                             
* **ReportFabricUpgradeHealth**: hello 현재 업그레이드 진행률와 클러스터 업그레이드를 다시 시작                             
* **StartInfrastructureTask**: 인프라 작업 시작                             
* **FinishInfrastructureTask**: 인프라 작업 완료                             
* **InvokeInfrastructureCommand**: 인프라 작업 관리 명령                              
* **ActivateNode**: 노드 활성화                             
* **DeactivateNode**: 노드 비활성화                             
* **DeactivateNodesBatch**: 다중 노드 비활성화                             
* **RemoveNodeDeactivations**: 다중 노드에서 비활성화 되돌리기                             
* **GetNodeDeactivationStatus**: 비활성화 상태 확인                             
* **NodeStateRemoved**: 노드 상태 제거됨 보고                             
* **ReportFault**: 오류 보고                             
* **FileContent**: 저장소 클라이언트 파일 전송 (외부 toocluster) 이미지                             
* **FileDownload**: 저장소 클라이언트 파일 다운로드 시작 (외부 toocluster) 이미지                             
* **InternalList**: 이미지 저장소 클라이언트 파일 목록 작업(내부)                             
* **Delete**: 이미지 저장소 클라이언트 삭제 작업                              
* **Upload**: 이미지 저장소 클라이언트 업로드 작업                             
* **NodeControl**: 노드 시작, 중지 및 다시 시작                             
* **MoveReplicaControl**: 하나의 노드만 tooanother에서 복제 데이터베이스를 이동                             

### <a name="miscellaneous-operations"></a>기타 작업
* **Ping**: 클라이언트 Ping                             
* **Query**: 허용된 모든 쿼리
* **NameExists**: 이름 지정 URI 존재 확인                             

hello 사용자 액세스 제어 형식, 기본적으로는 작업을 수행 하는 제한 된 toohello: 

* **EnumerateSubnames**: 이름 지정 URI 열거                             
* **EnumerateProperties**: 이름 지정 속성 열거                             
* **PropertyReadBatch**: 이름 지정 속성 읽기 작업                             
* **GetServiceDescription**: 긴 폴링 서비스 알림 및 서비스 설명 읽기                             
* **ResolveService**: 불만 기반 서비스 확인                             
* **ResolveNameOwner**: 이름 지정 URI 소유자 확인                             
* **ResolvePartition**: 시스템 서비스 확인                             
* **ServiceNotifications**: 이벤트 기반 서비스 알림                             
* **GetUpgradeStatus**: 응용 프로그램 업그레이드 상태 폴링                             
* **GetFabricUpgradeStatus**: 클러스터 업그레이드 상태 폴링                             
* **InvokeInfrastructureQuery**: 인프라 작업 쿼리                             
* **List**: 이미지 저장소 클라이언트 파일 목록 작업                             
* **ResetPartitionLoad**: 장애 조치(failover) 단위에 대한 부하 초기화                             
* **ToggleVerboseServicePlacementHealthReporting**: 자세한 정보 표시 서비스 배치 상태 보고 설정/해제                             

hello 관리자 액세스 제어는 액세스 toohello 작업 앞에 있습니다.

## <a name="changing-default-settings-for-client-roles"></a>클라이언트 역할의 기본 설정 변경
Hello 클러스터 매니페스트 파일에 필요한 경우 관리 기능 toohello 클라이언트에 제공할 수 있습니다. Toohello 이동 하 여 hello 기본값을 변경할 수 **패브릭 설정이** 중 옵션 [클러스터 만들기](service-fabric-cluster-creation-via-portal.md), hello hello 설정을 앞에 제공 하 고 **이름**, **admin**, **사용자**, 및 **값** 필드입니다.

## <a name="next-steps"></a>다음 단계
[서비스 패브릭 클러스터 보안](service-fabric-cluster-security.md)

[서비스 패브릭 클러스터 만들기](service-fabric-cluster-creation-via-portal.md)

