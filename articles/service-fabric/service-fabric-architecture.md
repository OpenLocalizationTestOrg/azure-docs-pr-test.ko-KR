---
title: "Azure 서비스 패브릭의 aaaArchitecture | Microsoft Docs"
description: "서비스 패브릭은 hello 클라우드에 대 한 확장성이 뛰어나고 안정적 toobuild 및 응용 프로그램 관리를 사용 하는 분산된 시스템 플랫폼입니다. 이 문서는 서비스 패브릭 hello 아키텍처를 보여 줍니다."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>서비스 패브릭 아키텍처
서비스 패브릭은 계층화된 하위 시스템으로 빌드됩니다. 이러한 하위 시스템에 toowrite 응용 프로그램을 사용 하면:

* 고가용성
* 확장성
* 관리 가능
* 테스트 가능

다이어그램을 다음 hello 서비스 패브릭 hello 주요 하위 시스템을 보여 줍니다.

![서비스 패브릭 아키텍처 다이어그램](media/service-fabric-architecture/service-fabric-architecture.png)

분산된 시스템에서 hello 기능 toosecurely 노드 간에 통신 하는 클러스터는 매우 중요 합니다. Hello hello 스택 로그의 노드 간에 보안 통신을 제공 하는 hello 전송 하위 시스템은입니다. Hello 전송 위에 하위 시스템 서비스 패브릭 수 있도록 오류를 감지, 리더 투표가 수행 일관 된 라우팅을 제공 된 클러스터 (클러스터 이름) 단일 엔터티로 패키지할 서로 다른 노드에 hello hello 페더레이션 하위 시스템을 표시 됩니다. hello 페더레이션 하위 시스템을 기반으로 계층화 hello 안정성 하위 시스템은 복제, 리소스 관리 및 장애 조치 같은 메커니즘을 통해 서비스 패브릭 서비스의 hello 안정성 담당 합니다. hello 페더레이션 하위 시스템에는 hello 호스팅 및 활성화 하위 시스템을 단일 노드에서 응용 프로그램의 hello 수명 주기 관리의 기반이 됩니다. 응용 프로그램 및 서비스의 hello 수명 주기를 관리 하는 hello 관리 하위 시스템입니다. hello 테스트 용이성 하위 시스템에는 응용 프로그램 개발자가 응용 프로그램 및 서비스 tooproduction 환경 배포 전후 시뮬레이션 된 오류를 통해 서비스를 테스트할 수 있습니다. 서비스 패브릭 hello 기능 통신 하위 시스템을 통해 tooresolve 서비스 위치를 제공합니다. hello 응용 프로그램 프로그래밍 모델을 노출 toodevelopers hello 응용 프로그램 모델 tooenable 도구와 함께 이러한 하위 시스템 맨 위 계층에 있습니다.

## <a name="transport-subsystem"></a>전송 하위 시스템
hello 전송 하위 시스템 지점 간 datagram 통신 채널을 구현합니다. 이 채널은 서비스 패브릭 클러스터 내에서 통신 하 고 hello 서비스 패브릭 클러스터와 클라이언트 간 통신에 사용 됩니다. 브로드캐스트, 멀티 캐스트에 구현 하기 위한 hello 기반을 제공 하는 요청-회신 통신 패턴을 페더레이션 레이어 hello와 단방향을 지원 합니다. X509를 사용 하 여 통신을 보호 하는 hello 전송 하위 시스템 인증서 또는 Windows 보안 합니다. 이 하위 시스템 서비스 패브릭에서 내부적으로 사용 되 고 응용 프로그램 프로그래밍에 대 한 직접 액세스할 수 있는 toodevelopers 않습니다.

## <a name="federation-subsystem"></a>페더레이션 하위 시스템
분산된 시스템의 노드 집합에 대 한 순서 tooreason, toohave hello 시스템의 일관 된 뷰 해야합니다. hello 페더레이션 하위 시스템 hello 전송 하위 시스템에서 제공 하는 hello 통신 기본 형식을 사용 하 고 stitches에 대해 추정할 수 있습니다 하는 단일 통합된 클러스터에 여러 개의 노드 hello 합니다. Hello 분산 시스템 기본 형식 필요 하 여 hello 다른 하위 시스템 액세스 실패 감지, 리더 투표 및 일관 된 라우팅을 제공 합니다. hello 페더레이션 하위 시스템은 128 비트 토큰 공백으로 분산된 해시 테이블을 기반으로 작성 됩니다. hello 하위 시스템 hello 링 소유권에 대 한 hello 토큰 공간의 하위 집합에 할당 되 고 각 노드 hello 노드 링 토폴로지를 만듭니다. 실패 감지에 대 한 hello 계층 하트 비트 및 중재에 따라 임대 메커니즘을 사용 합니다. 복잡 한 조인 및 언제 든 지 토큰의 단일 소유자만 있는 출발 프로토콜을 통해 hello 페더레이션 하위 시스템도 보장 합니다. 따라서 리더 선택 및 일관된 라우팅을 보장할 수 있습니다.

## <a name="reliability-subsystem"></a>안정성 하위 시스템
hello 안정성 하위 시스템 제공 hello hello 사용을 통해 항상 사용 가능한 서비스 패브릭 서비스의 hello 메커니즘 toomake hello 상태 *복제기*, *Failover Manager*, 및  *리소스 분산 장치가*합니다.

* hello 복제기 hello 기본 서비스 복제본의 상태 변경을 복제 toosecondary 복제본, 서비스 복제 집합에 있는 hello 기본 및 보조 복제본 사이의 일관성을 유지 하는 자동으로 됩니다 확인 합니다. hello 복제기 hello 복제 세트에 있는 hello 복제본 간에 쿼럼 관리를 담당 합니다. Hello 장애 단위 tooget hello 목록은 operations tooreplicate와 상호 작용 하 고 hello 재구성 에이전트 hello 복제 세트의 hello 구성으로 제공 합니다. 해당 구성을 복제본 hello 작업 toobe 복제할 필요를 나타냅니다. 서비스 패브릭 hello 모델 API toomake hello 서비스 상태 항상 사용 가능 하 고 신뢰할 수 있는 프로그래밍 하 여 사용할 수 있는 패브릭 복제기를 호출 하는 기본 복제기를 제공 합니다.
* Failover Manager hello는 노드는 hello 클러스터에서 제거 tooor 추가 되 면 hello 로드가 자동으로 hello 사용 가능한 노드 간에 보장 합니다. Hello 클러스터의 노드가 실패 하면 hello 클러스터 hello 서비스 복제본 toomaintain 가용성 자동으로 재구성 됩니다.
* 리소스 관리자 hello hello 클러스터의 오류 도메인을 통해 서비스 복제본 하 고 모든 장애 조치 단위가 모두 제대로 작동 하는지 확인 합니다. hello 리소스 관리자는 또한 hello 클러스터 노드 tooachieve 최적의 부하가 균일 분포의 공유 풀 내부에서 서비스 리소스를 조정 합니다.

## <a name="management-subsystem"></a>관리 하위 시스템
hello 관리 하위 시스템 종단 간 서비스 및 응용 프로그램 수명 주기 관리를 제공합니다. PowerShell cmdlet 및 관리 Api tooprovision를 사용 하면, 패치, 업그레이드, 배포 및 가용성의 손실 없이 응용 프로그램 프로 비전 해제할 합니다. hello 관리 하위 시스템 서비스를 수행 하는 hello를 통해이 수행 합니다.

* **클러스터 관리자**: hello 서비스 배치 제약 조건에 따라 hello 노드에서 안정성 tooplace hello 응용 프로그램에서 장애 조치 관리자 hello와 상호 작용 하는 hello 기본 서비스입니다. 장애 조치 하위 시스템에서 리소스 관리자 hello hello 제약 조건이 손상 되지 유지 합니다. hello 클러스터 관리자에서 프로 비전 toode 프로 비전 hello 응용 프로그램의 hello 수명 주기를 관리합니다. 응용 프로그램 가용성 하지 손실 된다는 의미 체계 상태 관점에서 업그레이드 하는 동안 상태 관리자 tooensure를 hello와 통합 합니다.
* **상태 관리자**: 이 서비스는 응용 프로그램, 서비스 및 클러스터 엔터티의 상태를 모니터링합니다. 클러스터 엔터티 (예: 노드, 서비스 파티션 및 복제본)에 다음 hello 중앙 집중식된 상태 저장소로 집계 되는 상태 정보를 보고할 수 있습니다. 이 상태 정보는 hello 서비스와 tootake 있도록 hello 클러스터의 여러 노드에 분산 된 노드는 전체 시간에 상태 스냅숏을 필요한 수정 작업을 제공 합니다. Api를 사용 하면 tooquery hello 상태 이벤트 상태 쿼리 toohello 상태 하위 시스템을 보고 합니다. hello 상태 쿼리 Api 반환 hello 상태에 저장 된 hello 원시 상태 데이터를 저장 또는 hello 집계, 특정 클러스터 엔터티에 대 한 상태 데이터를 해석 합니다.
* **Image Store**:이 서비스에서는 저장소 및 hello의 배포 응용 프로그램 이진 파일입니다. 이 서비스는 hello 응용 프로그램에서 다운로드 한 업로드 tooand 있는 간단한 분산된 파일 저장소를 제공 합니다.

## <a name="hosting-subsystem"></a>호스팅 하위 시스템
hello 클러스터 관리자는 특정 노드에 toomanage 요구에 호스팅 서비스는 하위 시스템 (각 노드에서 실행) 하는 hello에 알립니다. 다음 하위 시스템을 호스팅하는 hello 해당 노드에서 hello 응용 프로그램의 hello 수명 주기를 관리 합니다. Hello 안정성 및 상태 구성 요소 tooensure hello 복제본 올바르게 배치 되었는지 확인 하 고 정상 상태와 상호 작용 합니다.

## <a name="communication-subsystem"></a>통신 하위 시스템
이 하위 시스템 hello 명명 서비스를 통해 hello 클러스터 및 서비스 검색 내에서 신뢰할 수 있는 메시징을 제공 합니다. hello 명명 서비스는 hello 클러스터에서 서비스 이름을 tooa 위치를 확인 하 고 사용자 toomanage 서비스 이름 및 속성을 활성화 합니다. Hello 명명 서비스를 사용 하 고 수 있는 안전 하 게 hello 클러스터 tooresolve의 다른 노드에서 서비스 이름을 통신할 서비스 메타 데이터를 검색 합니다. 간단한 Naming 클라이언트 API를 사용 하 여 서비스 패브릭의 사용자가 서비스와 클라이언트 노드, 경쟁 되거나 다시 hello hello 클러스터의 크기 조정 해도 hello 현재 네트워크 위치를 확인할 수 있는 개발할 수 있습니다.

## <a name="testability-subsystem"></a>테스트 용이성 하위 시스템
테스트 용이성은 서비스 패브릭에서 빌드된 서비스를 테스트하는 데 적합하도록 설계된 도구 모음입니다. hello 도구를 사용 하는 개발자 쉽게 의미 있는 오류를 유도 하 고 테스트 시나리오 tooexercise를 실행 및 유효성 검사 hello 다양 한 상태 및 전환 하는 서비스는 제어 되 고 안전한 방식으로 모두에 해당 수명 주기 동안 발생 합니다. 테스트 용이성 제공 메커니즘 toorun 가용성 그대로 유지 하면서 다양 한 발생 가능한 오류 반복할 수 있는 긴 테스트 합니다. 테스트할 수 있는 프로덕션 환경을 제공합니다.

