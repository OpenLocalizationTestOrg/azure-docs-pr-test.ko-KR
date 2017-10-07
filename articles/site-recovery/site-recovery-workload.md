---
title: "aaaWhat 작업 수 Azure Site Recovery를 사용 하 여 보호?"
description: "Azure Site Recovery hello 복제, 장애 조치 및 온-프레미스 가상 컴퓨터 및 물리적 서버 tooAzure 또는 tooa 보조 온-프레미스 사이트의 복구를 조정 하 여 작업 및 응용 프로그램 보호"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Azure Site Recovery로 어떤 워크로드를 보호할 수 있습니까?
이 문서에서는 작업 및 복제 하는 hello Azure Site Recovery 서비스와 응용 프로그램을 설명 합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="overview"></a>개요
조직은 계획 되거나 계획 되지 않은 가동 중지 시간 동안 안전 하 고 사용할 수 있는 비즈니스 연속성 및 재해 복구 (BCDR) 전략 tookeep 작업 및 데이터가 필요 하 고 가능한 한 빨리 tooregular 작업 조건 복구.

사이트 복구는 tooyour BCDR 전략에 기여 하는 Azure 서비스입니다. 사이트 복구를 사용 하 여 응용 프로그램 인식 복제 toohello 클라우드 또는 tooa 보조 사이트를 배포할 수 있습니다. 여부 앱은 Windows 또는 Linux 기반, VMware 또는 Hyper-v, 물리적 서버에서 실행 중인 Site Recovery tooorchestrate 복제를 사용 하 여, 재해 복구 테스트를 수행 하 고 실행할 수 장애 조치 및 장애 복구 합니다.

사이트 복구는 SharePoint, Exchange, Dynamics, SQL Server 및 Active Directory를 포함하여 Microsoft 응용 프로그램을 통합합니다. Oracle, SAP, IBM 및 Red Hat을 비롯한 선두 공급 업체와도 긴밀히 협력 중입니다. 앱 단위로 복제 솔루션을 사용자 지정할 수 있습니다.

## <a name="why-use-site-recovery-for-application-replication"></a>응용 프로그램 복제에 Site Recovery를 사용해야 하는 이유
사이트 복구 적용 tooapplication 수준의 보호 및 복구를 다음과 같이 됩니다.

* 지원되는 컴퓨터에서 실행 중인 모든 워크로드에 복제를 제공하는 앱 중립성.
* 낮은 30 초 toomeet hello 요구 사항을 가장 중요 한 비즈니스 응용 프로그램의 Rpo 있는 거의 동기 복제 합니다.
* 단일 또는 다중 계층 응용 프로그램에 대한 앱 일관성 스냅숏.
* AD 복제, SQL AlwaysOn, Exchange 데이터베이스 가용성 그룹(DAG) 및 Oracle Data Guard를 포함하는 다른 응용 프로그램 수준 복제 기술을 사용하여 SQL Server AlwaysOn, 파트너쉽과 통합합니다.
* 한 번 클릭 하는 전체 응용 프로그램 스택과 toorecover를 사용 하 고 hello 계획에 tooinclude 외부 스크립트 및 수동 작업을 포함 하는 유연한 복구 계획
* 고급 사이트 복구 및 Azure toosimplify의 네트워크 관리 hello 기능 tooreserve IP 주소를 포함 하 여 응용 프로그램 네트워크 요구 사항 구성 부하 분산 및 통합 Azure 트래픽 관리자와 낮은 RTO 네트워크 switchovers에 대 한 합니다.
* 다운로드하고 복구 계획과 통합할 수 있는 프로덕션 준비된 응용 프로그램 특정 스크립트를 제공하는 다양한 자동화 라이브러리입니다.

## <a name="workload-summary"></a>워크로드 요약
Site Recovery는 지원되는 컴퓨터에서 실행 중인 모든 앱을 복제할 수 있습니다. 또한 추가 응용 프로그램별 테스트 아웃 제품 팀 toocarry와 협력 합니다.

| **워크로드** | **Hyper-v Vm tooa 보조 사이트를 복제 합니다.** | **Hyper-v Vm tooAzure 복제** | **VMware Vm tooa 보조 사이트를 복제 합니다.** | **VMware Vm tooAzure 복제** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |Y |Y |Y |Y |
| 웹앱(IIS, SQL) |Y |Y |Y |Y |
| System Center Operations Manager |Y |Y |Y |Y |
| Sharepoint |Y |Y |Y |Y |
| SAP<br/><br/>SAP 사이트 tooAzure 아닌 클러스터에 대 한 복제 |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |
| Exchange(비 DAG) |Y |Y |Y |Y |
| 원격 데스크톱/VDI |Y |Y |Y |해당 없음 |
| Linux(운영 체제 및 앱) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |
| Dynamics AX |Y |Y |Y |Y |
| Dynamics CRM |Y |서비스 예정 |Y |서비스 예정 |
| Oracle |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |예(Microsoft에서 테스트) |
| Windows 파일 서버 |Y |Y |Y |Y |
| Citrix XenApp 및 XenDesktop |해당 없음 |Y |해당 없음 |Y |

## <a name="replicate-active-directory-and-dns"></a>Active Directory 및 DNS 복제
Active Directory 및 DNS 인프라는 필수적인 toomost 엔터프라이즈 앱. 재해 복구 시 tooprotect 필요 하 고 작업 및 응용 프로그램을 복구 하기 전에 이러한 인프라 구성 요소를 복구 합니다.

Active Directory 및 DNS에 대 한 사이트 복구 toocreate 완전 자동화 된 재해 복구 계획을 사용할 수 있습니다. 예를 들어, SharePoint 및 기본 tooa 보조 사이트에서의 SAP 통해 toofail를 하려는 경우 먼저 Active Directory를 통해 실패 하는 복구 계획을 설정할 수 있습니다는 추가 하는 응용 프로그램별 복구 계획 하 toofail hello를 통해 활성에 의존 하는 다른 앱 디렉터리입니다.

Active Directory 및 DNS 보호에 대하여 [자세히 알아봅니다](site-recovery-active-directory.md).

## <a name="protect-sql-server"></a>SQL Server 보호
SQL Server는 온-프레미스 데이터 센터에서 많은 비즈니스 앱에 대한 데이터 서비스의 데이터 서비스 기반을 제공합니다.  SQL Server를 사용 하 여 tooprotect 엔터프라이즈 다중 계층 응용 프로그램, SQL Server HA/DR 기술을 함께 사이트 복구를 사용할 수 있습니다. 사이트 복구는 다음을 제공합니다.

* SQL Server에 대해 간단하고 비용 효율적인 재해 복구 솔루션. 여러 버전 및 에디션의 SQL Server 독립 실행형 서버 및 클러스터, tooAzure 또는 tooa 보조 사이트를 복제 합니다.  
* SQL AlwaysOn 가용성 그룹, toomanage 장애 조치 및 Azure 사이트 복구 복구 계획 장애 복구와 통합 합니다.
* Hello SQL Server 데이터베이스를 포함 하 여 응용 프로그램에서 모든 계층 hello에 대 한 종단 간 복구 계획 합니다.
* Azure에서 더 큰 IaaS 가상 컴퓨터로 "폭발적으로 증가"하여 Site Recovery와 함께 최대 부하에 대한 SQL Server의 규모 증가.
* SQL Server 재해 복구의 간편한 테스트. Tooanalyze 데이터 테스트 장애 조치를 실행 하 고 프로덕션 환경에 영향을 주지 않고 규정 준수 검사를 실행할 수 있습니다.

[자세히 알아봅니다](site-recovery-sql.md) .

## <a name="protect-sharepoint"></a>SharePoint 보호
Azure Site Recovery를 사용하면 다음과 같이 SharePoint 배포를 보호할 수 있습니다.

* Hello 요구 및 재해 복구를 위해 대기 팜에 대 한 연결 된 인프라 비용을 제거합니다. 사이트 복구 tooreplicate은 전체 팜 (웹, 앱 및 데이터베이스 계층) tooAzure 또는 tooa 보조 사이트를 사용 합니다.
* 응용 프로그램 배포 및 관리를 간소화합니다. 배포 된 업데이트 toohello 주 사이트 자동으로 복제 되며 따라서 사용할 수 장애 조치 및 보조 사이트에 팜 복구 후. 또한 hello 관리 복잡성과 대기 팜을 최신 상태로 유지 하는 데 관련 된 비용을 낮춥니다.
* 테스트 및 디버깅에 프로덕션 환경과 유사한 복사본 주문형 복사본 환경을 만들어 SharePoint 응용 프로그램 개발 및 테스트를 용이하게 합니다.
* 사이트 복구 toomigrate SharePoint 배포 tooAzure를 사용 하 여 전환 toohello 클라우드를 간소화 합니다.

[자세히 알아봅니다](site-recovery-sharepoint.md) .

## <a name="protect-dynamics-ax"></a>Dynamics AX 보호
Azure Site Recovery를 사용하면 다음과 같이 Dynamics AX ERP 솔루션을 보호하도록 합니다.

* 전체 Dynamics AX 환경의 (웹 및 AOS 계층, SharePoint 데이터베이스 계층)의 복제를 조정 tooAzure, 또는 tooa 보조 사이트입니다.
* Dynamics AX 배포 toohello 클라우드 (Azure)의 마이그레이션을 단순화 합니다.
* 테스트 및 디버깅에 프로덕션 환경과 유사한 복사본 주문형을 만들어 Dynamics AX 응용 프로그램 개발 및 테스트를 용이하게 합니다.

[자세히 알아봅니다](site-recovery-dynamicsax.md) .

## <a name="protect-rds"></a>RDS 보호
원격 데스크톱 서비스 (RDS)에서는 가상 데스크톱 인프라 (VDI), 세션 기반 데스크톱 및 응용 프로그램, 사용자가 toowork 아무 곳 이나 수 있으므로. Azure Site Recovery를 통해 다음을 수행할 수 있습니다.

* 관리 되거나 관리 되지 않는 풀링된 가상 데스크톱 tooa 보조 사이트 및 원격 응용 프로그램 및 세션 tooa 보조 사이트 또는 Azure에 복제 합니다.
* 복제할 수 있는 항목은 다음과 같습니다.

| **RDS** | **Hyper-v Vm tooa 보조 사이트를 복제 합니다.** | **Hyper-v Vm tooAzure 복제** | **VMware Vm tooa 보조 사이트를 복제 합니다.** | **VMware Vm tooAzure 복제** | **물리적 서버 tooa 보조 사이트를 복제 합니다.** | **물리적 서버 tooAzure 복제** |
| --- | --- | --- | --- | --- | --- | --- |
| **풀링된 가상 데스크톱(관리되지 않음)** |예 |아니요 |예 |아니요 |예 |아니요 |
| **풀링된 가상 데스크톱(관리됨/UPD 없음)** |예 |아니요 |예 |아니요 |예 |아니요 |
| **원격 응용 프로그램 및 데스크톱 세션(UPD 없음)** |예 |예 |예 |예 |예 |예 |

[자세히 알아봅니다](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) .

## <a name="protect-exchange"></a>Exchange 보호
Site Recovery를 사용하면 다음과 같이 Exchange를 보호할 수 있습니다.

* 단일 컴퓨터 또는 독립 실행형 서버와 같은 작은 Exchange 배포에 대 한 Site Recovery는 복제 하 고 tooAzure 또는 tooa 보조 사이트 장애 조치할 수 있습니다.
* 대규모 배포의 경우 Site Recovery가 Exchange DAGS와 통합됩니다.
* Exchange Dag는 hello를 기업에 Exchange 재해 복구를 위한 솔루션을 권장 합니다.  사이트 복구 복구 계획 Dag를 사이트에 걸쳐 tooorchestrate DAG 장애 조치를 포함할 수 있습니다.

[자세히 알아봅니다](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) .

## <a name="protect-sap"></a>SAP 보호
사이트 복구 tooprotect, SAP 배포를 다음과 같이 사용 합니다.

* TooAzure 구성 요소를 복제 하 여 온-프레미스를 실행 하는 SAP NetWeaver 및 비-NetWeaver 프로덕션 응용 프로그램의 보호를 사용 하도록 설정 합니다.
* 구성 요소 tooanother Azure 데이터 센터에 복제 하 여 Azure에서 실행 하는 SAP NetWeaver 및 비-NetWeaver 프로덕션 응용 프로그램의 보호를 사용 하도록 설정 합니다.
* SAP 배포 tooAzure toomigrate Site Recovery를 사용 하 여 클라우드 마이그레이션을 간소화 합니다.
* SAP 응용 프로그램 테스팅을 위해 온디맨드로 프로덕션 클론을 만들어 SAP 프로젝트 업그레이드, 테스트 및 프로토타입 생성을 단순화합니다.

[자세히 알아봅니다](site-recovery-sap.md) .

## <a name="protect-iis"></a>IIS 보호
사이트 복구 tooprotect IIS 배포를 다음과 같이 사용 합니다.

Azure Site Recovery 환경 tooa 콜드 원격 사이트 또는 공용 클라우드의 Microsoft Azure의 hello 중요 한 구성 요소를 복제 하 여 재해 복구를 제공 합니다. 없기 때문에 웹 서버 hello와 hello 데이터베이스 hello 가상 컴퓨터 복제 toohello 복구 사이트 되는, 요구 사항 toobackup 구성 파일이 나 인증서 별도로 합니다. 응용 프로그램 매핑 hello 및 변경 된 후 장애 조치 되는 환경 변수에 의존 하는 바인딩 hello 재해 복구 계획에 통합 하는 스크립트를 통해 업데이트할 수 있습니다. 가상 컴퓨터는 장애 조치 hello 이벤트에만 hello 복구 사이트에서 제기 된 합니다. 이 뿐만 아니라 Azure Site Recovery 하기도 쉽습니다 hello 끝 tooend 장애 조치 기능을 다음 hello를 제공 하 여 오케스트레이션:

-   시퀀싱 hello 종료 및 시작에 있는 가상 컴퓨터의 다양 한 계층 hello 합니다.
-   시작한 후 hello 가상 컴퓨터에서 응용 프로그램 종속성 및 바인딩의 tooallow 업데이트 스크립트를 추가 합니다. hello 스크립트에 사용 되는 tooupdate hello DNS 서버 toopoint toohello 복구 사이트 일 수도 있습니다.
-   Hello 기본 및 복구 네트워크를 매핑하는 방법으로 IP 주소 toovirtual 컴퓨터 이전 장애 조치를 할당 하 고 따라서 toobe 업데이트 사후 장애 조치는 필요 하지 않은 스크립트를 사용 하 여 키를 누릅니다.
-   재해의 hello 이벤트에서 혼동 hello 범위 헤드 hello 웹 서버의 여러 웹 응용 프로그램에 대 한 한 번의 클릭 장애 조치를 수행할 수 있습니다.
-   Tootest hello 복구 계획 DR 드릴에 대 한 격리 된 환경에서 기능 하 고 있습니다.

IIS 웹 팜을 보호하는 방법에 대한 [자세한 내용](https://aka.ms/asr-iis)

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Citrix XenApp 및 XenDesktop 보호
사이트 복구 tooprotect 하면 Citrix XenApp 및 XenDesktop 배포를 다음과 같이 사용 합니다.

* 다양 한 배포를 복제 하 여 Citrix XenApp 및 XenDesktop 배포 hello 보호 사용 (AD DNS 서버, SQL 데이터베이스 서버, Citrix 배달 컨트롤러 StoreFront 서버, XenApp 마스터 (VDA) Citrix XenApp 라이선스 서버)를 포함 하 여 계층화 tooAzure 합니다.
* 클라우드 마이그레이션 프로그램 Citrix XenApp 및 XenDesktop 배포 tooAzure toomigrate Site Recovery를 사용 하 여 단순화 합니다.
* 테스트 및 디버깅을 위해 프로덕션 환경과 유사한 주문형 복사본을 만들어 Citrix XenApp/XenDesktop 테스트를 간소화합니다.
* 이 솔루션은 Windows Server 운영 체제 가상 데스크톱에만 적용할 수 있으며 Azure의 라이선스에 대해 아직 지원되지 않는 클라이언트 가상 데스크톱에는 적용할 수 없습니다.
Azure의 클라이언트/서버 데스크톱용 라이선스에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/licensing-faq/).

Citrix XenApp 및 XenDesktop 배포 보호에 대해 [자세히 알아보세요](site-recovery-citrix-xenapp-and-xendesktop.md). Hello를 참조할 수 있습니다 또는 [Citrix에서 백서](https://aka.ms/citrix-xenapp-xendesktop-with-asr) 동일 hello에 대해 자세히 설명 합니다.

## <a name="next-steps"></a>다음 단계
[필수 구성 요소 확인](site-recovery-prereq.md)
