---
title: "aaaInstall (대형 인스턴스) Azure에서 SAP HANA에 SAP HANA | Microsoft Docs"
description: "방법 (대형 인스턴스) Azure에서 SAP HANA에 SAP HANA tooinstall 합니다."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>어떻게 tooinstall Azure에서 SAP HANA (대형 인스턴스)를 구성 하 고

다음은이 가이드를 읽기 전에 몇 가지 중요 한 정의 tooknow입니다. [SAP HANA (큰 인스턴스) 개요 및 Azure 상의 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)에서 HANA 큰 인스턴스 단위의 두 다른 클래스를 도입했습니다.

- S72, S72m, S144, S144m, S192, 및 S192m tooas hello '클래스 I t y'는 Sku입니다.
- S384, S384m, S384xm, S576, S768, 및은 기관 S960 tooas hello Sku의 ' Type II 클래스'.

hello 클래스 지정자는 진행 중인 toobe hello toodifferent 기능 및 HANA 큰 인스턴스 Sku를 기준으로 요구 사항 설명서 tooeventually 참조 HANA 큰 인스턴스 전체에서 사용 됩니다.

우리가 자주 사용하는 다른 정의는 다음과 같습니다.
- **대형 인스턴스 스탬프:** SAP HANA TDI 하드웨어 인프라 스택이 인증 하며 Azure 내에서 SAP HANA 인스턴스 toorun 전용입니다.
- **(대형 인스턴스) Azure에서 SAP HANA:** 에 인증 된 하드웨어에 큰 인스턴스 스탬프 서로 다른 Azure 지역에 배포 된 SAP HANA TDI의 Azure toorun HANA 인스턴스에 hello 제안에 대 한 공식 이름입니다. hello 관련 용어 **HANA 큰 인스턴스** (대형 인스턴스) Azure에서 SAP HANA 짧은 이며 널리이 기술 배포 가이드를 사용 합니다.


SAP HANA의 hello 설치 귀하의 책임 이며 Azure (대형 인스턴스) 서버에 새 SAP HANA의 인계 후 hello 활동을 시작할 수 있습니다. 및 Azure VNet(s) 및 hello HANA 큰 인스턴스 장치 간의 hello 연결 설정 (를) 가져왔습니다. 

> [!Note]
> SAP 정책에 따라 tooperform SAP HANA 설치 인증 된 사용자가 SAP HANA의 hello 설치를 수행 해야 합니다. Hello SAP 기술 연결 인증 시험, SAP HANA 설치 인증 시험을 통과 하는 개인을 통하거나 인증 된 SAP 시스템 통합 업체가 (SI).

특히 tooinstall HANA 2.0을 계획 하는 경우를 다시 확인해 [SAP 지원 참고 #2235581-SAP HANA: 지원 되는 운영 체제](https://launchpad.support.sap.com/#/notes/2235581/E) toomake hello SAP HANA로 OS가 지원 되는 hello 해제 하면 있는지 순서로 tooinstall를 결정 합니다. 지원 되는 OS HANA 2.0은 보다 좀 더 제한 된 hello OS HANA 1.0에 대 한 지원 해당 hello를 생각 합니다. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Hello HANA 큰 인스턴스 장치를 받은 후 첫 번째 단계

**1 단계** 수신 후 HANA 큰 인스턴스 hello 및 tooregister hello 운영 체제의 OS 공급자를 사용 하 여 hello 인스턴스는 toohello 인스턴스 액세스 및 연결을 설정 합니다. 이 단계는 SUSE Linux OS SUSE SMT toohave Azure에서 VM에 배포 해야 하는 인스턴스의 등록 포함 됩니다. hello HANA 큰 인스턴스 단위 toothis SMT 인스턴스 (이 설명서의 뒷부분에 나오는 참조)에 연결할 수 있습니다. 또는 RedHat OS toobe hello를 tooconnect 필요한 Red Hat 구독 관리자에 등록 해야 합니다. 이 [문서](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 설명도 참조하세요. 또한이 단계는 필요한 toobe 수 toopatch hello 운영 체제입니다. Hello 고객의 책임 hello에에서 있는 작업입니다. SUSE에 대 한 설명서 tooinstall 찾아 SMT 구성 [여기](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html)합니다.

**단계를 두 번째** toocheck 새로운 패치 및 hello 특정 OS 릴리스/버전에서 수정 됩니다. Hello 패치 수준의 hello HANA 큰 인스턴스 hello 최신 상태 인지 확인 합니다. OS 패치/릴리스 및 변경 내용을 toohello 이미지 Microsoft 배포할 수에 대 한 타이밍에 따라, 경우도 없는 hello 최신 패치 포함 될 수 있습니다. 따라서 보안, 기능, 가용성 및 성능에 대 한 관련 hello 특정 Linux 공급 업체에서 한편 발표 된 패치와 toobe 적용 해야 하는지 여부를 toocheck HANA 인스턴스가 큰 단위를 통해 수행한 다음 필수 단계입니다.

**세 번째 단계** hello 아웃 toocheck 관련 SAP Note에서 설치 및 구성 SAP HANA hello 특정 OS 릴리스/버전에 대 한 됩니다. Toochanging 권장 사항 또는 변경 tooSAP 인해 메모 또는 개별 설치 시나리오에 의존 하는 구성, Microsoft이 지 것입니다 수 toohave 완벽 하 게 구성 된 인스턴스가 HANA 큰 단위입니다. 따라서 고객으로 tooread hello SAP Note 관련된 tooSAP HANA 정확한 Linux 릴리스에 필수입니다. 또한 hello OS 릴리스/필요한 버전의 hello 구성을 선택 하 고 hello 구성 설정을 적용 여기서 아직 수행 하지 않습니다.

관련 매개 변수를 따르고 결국 조정 hello를 확인 합니다.

- net.core.rmem_max = 16777216
- net.core.wmem_max = 16777216
- net.core.rmem_default = 16777216
- net.core.wmem_default = 16777216
- net.core.optmem_max = 16777216
- net.ipv4.tcp_rmem = 65536 16777216 16777216
- net.ipv4.tcp_wmem = 65536 16777216 16777216

SLES12 s p 1과 RHEL 7.2 부터는 hello /etc/sysctl.d 디렉터리의 구성 파일에 이러한 매개 변수를 설정 해야 합니다. 예를 들어 구성 파일 hello 이름 91-NetApp-HANA.conf을 만들어야 합니다. 이전 SLES 및 RHEL 릴리스의 경우 /etc/sysctl.conf에서 이러한 매개 변수를 설정해야 합니다.

에 대 한 모든 RHEL를 해제 하 고 hello SLES12 부터는 
- sunrpc.tcp_slot_table_entries = 128

매개 변수를 /etc/modprobe.d/sunrpc-local.conf에서 설정해야 합니다. Hello 파일 존재 하지 않는 경우 먼저 hello 다음 항목을 추가 하 여 생성 해야 됩니다. 
- options sunrpc tcp_max_slot_table_entries=128

**네 번째 단계** HANA 대형 인스턴스 단위의 toocheck hello 시스템 시간입니다. hello 인스턴스 HANA 큰 인스턴스 스탬프에 있는 hello Azure 지역 hello의 hello 위치를 나타내는 시스템 표준 시간대로 배포 됩니다. 사용자는 무료 toochange hello 시스템 시간 또는 소유 하는 hello 인스턴스의 표준 시간대입니다. 이렇게 되 고 tooadapt hello 표준 시간대의 hello 새로 인스턴스를 전달 해야 하는 준비 테 넌 트에 더 많은 인스턴스 순서를 지정 합니다. Microsoft 작업 없음에 대 한 정보 hello 시스템 표준 시간대 hello 인계 후 hello 인스턴스와 설정할를 갖습니다. 따라서 새로 배포 된 인스턴스 설정 되어 있지 않습니다 hello에 동일한 표준 시간대로 변경 하나 hello으로 합니다. 결과적으로, 고객 toocheck 책임 이며 필요한 경우 조정으로 전달 하는 hello 인스턴스 hello 표준 시간대입니다. 

**5 단계** toocheck 등/호스트 됩니다. Hello 블레이드 넘기기 가져오기, 대로 용도별로 (다음 섹션 참조)에 대 한 할당 된 서로 다른 IP 주소 갖습니다. Hello 등/호스트 파일을 확인 합니다. 단위 기존 테 넌 트에 추가 되는 경우 원하지 toohave 등/호스트 새로 배포 된 hello 시스템 전달된 시스템 이전 버전의 hello IP 주소와 올바르게 유지 관리 합니다. 따라서 켜져 있습니다 고객 toocheck hello에 대 한 올바른 설정으로, 새로 배포 된 인스턴스 상호 작용 하 고 테 넌 트에 배포 된 단위에 이전 버전의 hello 이름을 확인할 수 있습니다. 

## <a name="networking"></a>네트워킹
Azure Vnet을 디자인 하 고 이러한 문서에 설명 된 대로 해당 Vnet toohello HANA 큰 인스턴스 연결에 hello 권장 사항을 수행 했는지 가정 합니다.

- [Azure에서 SAP HANA(큰 인스턴스) 개요 및 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Azure의 SAP HANA(큰 인스턴스) 인프라 및 연결](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Hello 단일 단위 hello 네트워킹에 대 한 toomention 만한 몇 가지 세부 사항은 있습니다. 모든 인스턴스가 HANA 큰 단위 tootwo 또는 hello 단위의 NIC 포트 세 개 할당 된 IP 주소를 두 개나 세 개 포함 되어 있습니다. 세 개의 IP 주소는 HANA 확장 구성 및 hello HANA 시스템 복제 시나리오에 사용 됩니다. Hello IP 주소 중 하나가 할당 toohello hello 단위의 NIC hello hello에 설명 된 서버 IP 풀 벗어났습니다 [개요 SAP HANA (대형 인스턴스) 및 Azure에서 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)합니다.

단위를 할당 하는 두 개의 IP 주소에 대 한 hello 분포 같이 표시 됩니다.

- eth0.xx는 hello tooMicrosoft 제출 된 서버 IP 풀 주소 범위를 벗어난 IP 주소가 할당 있어야 합니다. 이 IP 주소 hello 운영 체제의 /etc/hosts에 유지 관리에 사용 되어야 합니다.
- eth1.xx는 tooNFS 통신에 사용 되는 IP 주소가 할당 있어야 합니다. 따라서 이러한 주소 방법을 **하지** toobe 등/순서 tooallow 인스턴스 tooinstance 트래픽 hello 테 넌 트 내에 있는 호스트에서 유지 관리 해야 합니다.

HANA 시스템 복제 또는 HANA 확장 배포의 경우 두 개의 IP 주소가 할당된 블레이드 구성은 적합하지 않습니다. 만 지정 된 두 개의 IP 주소 및 toodeploy 그러한 구성이 지원 Azure 서비스 관리 tooget에 SAP HANA에 게 문의 하는 경우 IP 세 번째 세 번째 할당 된 VLAN의에서 주소입니다. HANA 큰 인스턴스 단위 NIC 포트 세 개에 할당 된 세 가지 IP 주소, hello 다음의 사용 규칙이 적용 됩니다.

- eth0.xx는 hello tooMicrosoft 제출 된 서버 IP 풀 주소 범위를 벗어난 IP 주소가 할당 있어야 합니다. 따라서 hello 운영 체제의 /etc/hosts에 유지 관리를 위해이 IP 주소는 사용할 수 없습니다.
- eth1.xx는 tooNFS 저장소 통신에 사용 되는 IP 주소가 할당 있어야 합니다. 따라서 이 주소 유형은 etc/hosts에서 유지 관리되지 않아야 합니다.
- eth2.xx는 독점적으로 사용 되는 toobe 등/hello 다른 인스턴스 간의 통신에 대 한 호스트에서 유지 관리 해야 합니다. 이러한 주소 toobe HANA hello 노드 간 구성에 사용 하는 IP 주소로 확장 HANA 구성에서 유지 관리 해야 하는 hello IP 주소 수도 있습니다.



## <a name="storage"></a>저장소

hello 저장소 레이아웃 (대형 인스턴스) Azure에서 SAP HANA에 대해 구성 된 SAP HANA에 설명 된 대로 안내선을 권장 하는 SAP 통해 Azure 서비스 관리에 의해 [SAP HANA 저장소 요구 사항을](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) 백서에 나와 있습니다. hello에 다른 HANA 대형 인스턴스 Sku 내용이 설명 되어 있는 hello 서로 다른 볼륨의 대략적인 크기 hello [개요 SAP HANA (대형 인스턴스) 및 Azure에서 아키텍처](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

hello hello 저장소 볼륨의 명명 규칙은 다음 표에 hello에 나열 됩니다.

| 저장소 사용 | 탑재 이름 | 볼륨 이름 | 
| --- | --- | ---|
| HANA data | /hana/data/SID/mnt0000<m> | 저장소 IP:/hana_data_SID_mnt00001_tenant_vol |
| HANA log | /hana/log/SID/mnt0000<m> | 저장소 IP:/hana_log_SID_mnt00001_tenant_vol |
| HANA log backup | /hana/log/backups | 저장소 IP:/hana_log_backups_SID_mnt00001_tenant_vol |
| HANA shared | /hana/shared/SID | 저장소 IP:/hana_shared_SID_mnt00001_tenant_vol/shared |
| usr/sap | /usr/sap/SID | 저장소 IP:/hana_shared_SID_mnt00001_tenant_vol/usr_sap |

여기서 SID = hello HANA 인스턴스 시스템 ID 

tenant = 테넌트 배치 시 연산에 대한 내부 열거

공유 HANA 및 usr/sap 공유 볼 수 있듯이 동일한 볼륨 hello 합니다. hello mountpoints의 hello 용어 체계는 hello로 hello HANA 인스턴스 hello 탑재 수의 시스템 ID 포함 합니다. 강화(scale-up) 배포의 경우 탑재가 하나(예: mnt00001)만 있습니다. 반면에 확장(scale-out) 배포의 경우 worker 및 master 노드를 포함하여 많은 탑재를 볼 수 있습니다. Hello 확장 환경, 데이터, 로그, 로그 백업 볼륨 hello 확장 구성에서 공유 일정과 연결 된 tooeach 노드에입니다. 여러 SAP 인스턴스를 실행 하는 구성에 대 한 다른 볼륨 세트는 생성 되 고 연결 된 toohello 인스턴스가 한 큰 단위입니다.

Hello 논문 하 고 인스턴스가 HANA 큰 단위를 찾습니다는 hello 단위 된 제공 아니라 넉 넉 디스크 볼륨 HANA/데이터에 대 한과 볼륨 HANA/로그/백업 된 것을 실현 합니다. hello hello HANA/많아질 수 있으므로 데이터 크기의 म 이유 원인은 hello storage 스냅숏을 사용 하는 고객으로 서 수에 대 한 제공 hello 같은 디스크 볼륨을입니다. 더 많은 저장소 스냅숏을 수행한에서 할당 된 저장소 볼륨의 스냅숏을 더 많은 공간이 사용 되는 hello hello 의미 합니다. hello HANA/로그/백업 볼륨은의 tooput 데이터베이스 백업을 생각 toobe hello 볼륨에 없습니다. 크기의 toobe hello HANA 트랜잭션 로그 백업에 대 한 백업 볼륨으로 사용 되는 경우 이후 버전의 hello 저장소 스냅숏 스냅숏을 자주 셀프 서비스에서는 더 많은 특정 볼륨 toohave이를 대상입니다. 더 자주 사용 하 고 복제 toohello 재해 복구 사이트에서 사용자가 원하는 toooption-hello HANA 큰 인스턴스 인프라에서 제공 하는 hello 재해 복구 기능에 대 한 경우. 자세한 내용은 [Azure의 SAP HANA(큰 인스턴스) 고가용성 및 재해 복구](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요. 

또한 toohello 저장소 제공 스토리지 용량 1TB 단위로 구입할 수 있습니다. 이 추가 저장소를 새 볼륨 tooa HANA 큰 인스턴스도 추가할 수 있습니다.

와 SAP HANA Azure 서비스 관리에 등록 하는 동안 hello 고객이 지정 된 사용자 ID (UID) 및 그룹 ID (GID) hello sidadm sapsys 및 사용자 그룹에 대 한 (예: 1000,500)는 hello SAP HANA 시스템을 설치 하는 동안이 동일한 값을 사용 해야 합니다. 단위에서 여러 HANA 인스턴스 toodeploy을 원하는 만큼 여러 집합을 볼륨 (각 인스턴스에 대해 하나의 집합)을 가져옵니다. 결과적으로, 배포 시 toodefine가 필요합니다.

- hello hello 서로 다른 HANA 인스턴스 (sidadm는 옵트아웃 파생 됨)의 SID입니다.
- Hello 여러 HANA 인스턴스의 메모리 크기입니다. 이후 인스턴스 당 hello 메모리 크기는 각 개별 볼륨 세트에서 hello 볼륨의 hello 크기를 정의 합니다.

저장소 공급자 권장 사항이 모든 탑재 된 볼륨에 대해 구성 된 hello 다음 탑재 옵션에 따라 (부팅 LUN은 제외):

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

이러한 탑재 지점은/등/fstab 그래픽 뒤에 표시 된 hello와 같은 설정:

![HANA 큰 인스턴스 유닛의 탑재된 볼륨의 fstab](./media/hana-installation/image1_fstab.PNG)

hello 명령 df-h S72m HANA 큰 인스턴스 장치에서의 hello 출력은 같습니다.

![HANA 큰 인스턴스 유닛의 탑재된 볼륨의 fstab](./media/hana-installation/image2_df_output.PNG)


hello 저장소 컨트롤러 및 hello 큰 인스턴스 스탬프의 노드는 동기화 된 tooNTP 서버입니다. 동기화는 NTP 서버에 대해 Azure (대형 인스턴스) 단위 및 Azure Vm에서 SAP HANA hello 여러분과 hello 인프라와 Azure 또는 대형 인스턴스 스탬프 hello 계산 단위 간의 없는 상당한 시간이 드리프트 발생 있을 것입니다.

순서 toooptimize 아래 사용 되는 SAP HANA toohello 저장소에서에서 hello SAP HANA 구성 매개 변수를 다음 설정 해야 합니다.

- max_parallel_io_requests 128
- async_read_submit on
- async_write_submit_active on
- async_write_submit_blocks all
 
TooSPS12 SAP HANA 1.0 버전에서는 이러한 매개 변수에 설정할 수 있는 hello hello SAP HANA 데이터베이스를 설치 하는 동안에 설명 된 대로 [SAP 참고 #2267798 hello SAP HANA 데이터베이스의 구성](https://launchpad.support.sap.com/#/notes/2267798)

또한 구성할 수 있습니다 hello 매개 변수 hello SAP HANA 데이터베이스 설치 후 hello hdbparam 프레임 워크를 사용 하 여 합니다. 

SAP HANA 2.0과 함께 hello hdbparam 프레임 워크 되지 않습니다. 따라서 SQL 명령을 사용 하 여 hello 매개 변수를 설정 되어야 합니다. 자세한 내용은 [SAP Note #2399079: HANA 2에서 hdbparam 제거](https://launchpad.support.sap.com/#/notes/2399079)를 참조하세요.


## <a name="operating-system"></a>운영 체제

운영 체제 이미지를 배달 하는 hello 스왑 공간 too2 GB toohello에 따라 설정 되어 [SAP 지원 참고 #1999997 FAQ: SAP HANA 메모리](https://launchpad.support.sap.com/#/notes/1999997/E)합니다. 다른 값으로 설정 원하는 필요 toobe 사용자가 설정한 고객으로 서입니다.

[SAP 응용 프로그램에 대 한 SUSE Linux Enterprise Server 12 SP1](https://www.suse.com/products/sles-for-sap/hana) hello î Linux (대형 인스턴스) Azure에서 SAP HANA에 대해 설치 됩니다. SAP 관련 기능을 제공 하는이 특정 분포 &quot;hello 초기&quot; (SLES에서 SAP를 효과적으로 실행 하기 위한 미리 설정된 된 매개 변수 포함).

참조 [리소스 라이브러리/White Papers](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) hello SUSE 웹 사이트 및 [SUSE에서의 SAP](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) 몇 가지 유용한 리소스 관련 toodeploying SLES (포함 하 여 hello 설정에서 SAP HANA에 대 한 hello SAP 커뮤니티 네트워크 (SCN)에 높은 가용성, 보안 강화 특정 tooSAP 작업 등).

SUSE 관련 링크에 있는 유용한 추가 SAP 정보:

- [SUSE Linux의 SAP HANA 사이트](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [SAP 모범 사례: 복제 큐에 넣기 – SUSE Linux Enterprise 12의 SAP NetWeaver](https://www.suse.com/docrepcontent/container.jsp?containerId=9113)(영문)
- [ClamSAP - SAP용 SLES 바이러스 방지](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap)(SLES 12 for SAP Applications 포함)(영문)

지원 참고 사항 적용 가능한 tooimplementing SLES 12에서 SAP HANA SAP:

- [SAP Support Note #1944799 – SLES 운영 체제 설치를 위한 SAP HANA 지침](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)(영문)
- [SAP Support Note #2205917 – SAP HANA DB: SLES 12 for SAP Applications를 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2205917/E)(영문)
- [SAP Support Note #1984787 – SUSE Linux Enterprise Server 12: 설치 참고](https://launchpad.support.sap.com/#/notes/1984787)(영문)
- [SAP Support Note #171356 – SAP Software on Linux: 일반 정보](https://launchpad.support.sap.com/#/notes/1984787)(영문)
- [SAP Support Note #1391070 – Linux UUID 솔루션](https://launchpad.support.sap.com/#/notes/1391070)(영문)

[SAP HANA용 Red Hat Enterprise Linux](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana)(영문)는 HANA 큰 인스턴스에서 SAP HANA를 실행하기 위한 또 다른 제품입니다. RHEL 6.7 및 7.2 릴리스를 사용할 수 있습니다. 

Red Hat 관련 링크에 있는 유용한 추가 SAP 정보:
- [Red Hat Linux 사이트의 SAP HANA](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat)

Red hat에서 SAP HANA 지원 참고 사항 적용 가능한 tooimplementing SAP:

- [SAP Support Note #2009879 – RHEL(Red Hat Enterprise Linux) 운영 체제를 위한 SAP HANA 지침](https://launchpad.support.sap.com/#/notes/2009879/E)(영문)
- [SAP Support Note #2292690 - SAP HANA DB: RHEL 7을 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2292690)(영문)
- [SAP Support Note #2247020 - SAP HANA DB: RHEL 6.7을 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2247020)(영문)
- [SAP Support Note #1391070 – Linux UUID 솔루션](https://launchpad.support.sap.com/#/notes/1391070)(영문)
- [SAP Support Note #2228351 - Linux: RHEL 6 또는 SLES 11의 SAP HANA Database SPS 11 수정 번호 110 이상](https://launchpad.support.sap.com/#/notes/2228351)(영문)
- [SAP Support Note #2397039 - FAQ: RHEL의 SAP](https://launchpad.support.sap.com/#/notes/2397039)(영문)
- [SAP Support Note #1496410 - Red Hat Enterprise Linux 6.x: 설치 및 업그레이드](https://launchpad.support.sap.com/#/notes/1496410)(영문)
- [SAP Support Note #2002167 - Red Hat Enterprise Linux 7.x: 설치 및 업그레이드](https://launchpad.support.sap.com/#/notes/2002167)(영문)

## <a name="time-synchronization"></a>시간 동기화

Hello SAP NetWeaver 아키텍처를 기반으로 SAP 응용 프로그램은 hello 다양 한 구성 요소를 구성 하는 hello SAP 시스템에 대 한 시간 차이에 중요 한 합니다. SAP ABAP 짧은 덤프 ZDATE의 오류 제목 hello\_LARGE\_시간\_차이 하 게 가능성이 친숙 하 고 이러한 짧은 덤프 나타나는 때 hello 서로 다른 서버 또는 Vm의 시스템 시간이 너무 멀리 떨어져 있는 유동 됩니다.

Azure 대상이 &#39;에서 수행 하는 시간 동기화 (대형 인스턴스) Azure에서 SAP HANA t toohello 계산 단위 hello 큰 인스턴스 스탬프를 적용 합니다. 이 동기화는 원시 Azure VM에서 SAP 응용 프로그램을 실행하는 데는 적용할 수 없습니다. Azure가 시스템 시간이 적절하게 동기화되도록 보장하기 때문입니다. 결과적으로, SAP HANA hello 및 Azure Vm에서 실행 되는 SAP 응용 프로그램 서버에서 사용할 수 있는 별도 시간 서버를 설정 해야 합니다는 데이터베이스에서 HANA 대형 인스턴스에서 실행 중인 인스턴스입니다. hello 저장소 인프라 큰 인스턴스 스탬프의 시간이 NTP 서버와 동기화 됩니다.

## <a name="setting-up-smt-server-for-suse-linux"></a>SUSE Linux용 SMT 서버 설정
SAP HANA 대규모 인스턴스에 직접 연결 toohello 인터넷 필요는 없습니다. 따라서 간단한 프로세스 tooregister toodownload hello OS 공급자와 이러한 단위 아니며 패치를 적용 합니다. SUSE Linux의 hello 경우 한 가지 해결 tooset SMT 서버가 Azure VM에서 발생할 수 있습니다. Azure VM hello 필요한 반면 toobe HANA 큰 인스턴스를 연결 된 toohello는 Azure VNet에서 호스팅됩니다. SMT 서버와 hello HANA 큰 인스턴스 단위는 등록 하 고 패치를 다운로드 수 없습니다. 

SUSE의 [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf)(SLES 12 SP2용 구독 관리 도구) 사이트에 자세한 지침이 제공되어 있습니다. 

HANA 큰 인스턴스에 대 한 hello 작업을 충족 하는 SMT 서버 hello 설치에 대 한 사전 조건,으로 다음이 필요 합니다.

- Azure VNet 연결된 toohello HANA 큰 인스턴스 ER 회로입니다.
- 조직과 연결된 SUSE 계정. 반면 hello 조직 toohave 일부 유효한 SUSE 구독 해야 합니다.

### <a name="installation-of-smt-server-on-azure-vm"></a>Azure VM에 SMT 서버 설치

이 단계에서는 Azure VM에서 hello SMT 서버를 설치합니다. hello 첫 번째 측정값은 toohello에 toolog [SUSE 고객 센터](https://scc.suse.com/)

로그인 할 이동 tooOrganization 조직 자격 증명--> 합니다. 해당 섹션에서 필요한 tooset hello SMT 서버를 사용 되는 자격 증명 hello를 찾아야 합니다.

hello 세 번째 단계는 tooinstall hello Azure VNet의에서 SUSE Linux VM입니다. toodeploy hello VM을 Azure의 SLES 12 SP2 갤러리 이미지를 사용 합니다. Hello 배포 프로세스의 DNS 이름을 정의 하지 않은 하 고이 스크린 샷에 표시 된 대로 고정 IP 주소를 사용 하지 마십시오

![SMT 서버용 VM 배포](./media/hana-installation/image3_vm_deployment.png)

hello 배포 VM 더 작은 VM 인시던트 였으며 hello 10.34.1.4의 Azure VNet의에서 hello 내부 IP 주소를 가져왔습니다. Hello VM 이름이 smtserver 이었습니다. Hello, 설치 후 hello 연결 toohello HANA 큰 인스턴스 장치 선택 되었습니다. 이름 확인을 구성 하는 방식을에 종속 등/hello Azure VM의 호스트 인스턴스가 HANA 큰 단위 hello의 tooconfigure 해상도 할 수 있습니다. 추가 디스크 toohello 이동 toobe toohold hello 패치를 사용 하는 VM을 추가 합니다. hello 부팅 디스크 자체는 너무 작을 수 없습니다. Hello 경우 설명 hello 디스크 hello 스크린 샷 뒤에 표시 된 대로 탑재 된 너무/srv/www/htdocs를 가져왔습니다. 100GB 디스크로 충분합니다.

![SMT 서버용 VM 배포](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Toohello HANA 인스턴스가 큰 단위를 로그인, /etc/hosts 유지 관리 하 고 hello toorun hello SMT 서버 hello 네트워크를 통해 되어 있는 Azure VM에 도달할 수 있는지 확인 합니다.

이 검사를 성공적으로 완료 한 후 toolog toohello hello SMT server를 실행 해야 하는 Azure VM에에서 필요 합니다. Putty toolog toohello VM 사용 하는 경우 tooexecute이이 일련의 명령에에서 필요 bash 창.

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

이러한 명령은 실행 한 후 bash tooactivate hello 설정을 다시 시작 합니다. 그런 다음 YAST를 시작합니다.

YAST, tooSoftware 유지 관리 및 smt에 대 한 검색을 이동 합니다. 아래와 같이 tooyast2 smt 자동으로 전환 smt 선택

![yast의 SMT](./media/hana-installation/image5_smt_in_yast.PNG)


Hello smtserver에서 설치에 대 한 hello 선택을 적용 합니다. 설치 되 면 toohello SMT 서버 구성을 이동한 hello 앞서 검색 SUSE 고객 센터에서에서 hello 조직 자격 증명을 입력 합니다. 또한 hello SMT 서버 URL로 Azure VM 호스트를 입력 합니다. 이 데모에서는 hello 다음 그래픽에 표시 된 대로 https://smtserver 있었습니다.

![SMT 서버 구성](./media/hana-installation/image6_configuration_of_smtserver1.png)

다음 단계로 hello 연결 toohello SUSE 고객 센터 작동 여부 tootest이 필요 합니다. Hello 그래픽 hello 시연에서는 다음에 나와 있는 것 처럼 작동 않았습니다.

![테스트 연결 tooSUSE 고객 센터](./media/hana-installation/image7_test_connect.png)

한 번 hello SMT 설치 시작 tooprovide 데이터베이스 암호 필요. 새로 설치 하는 것 이므로 toodefine hello 다음 그래픽에 표시 된 대로 해당 암호가 필요 합니다.

![데이터베이스에 대한 암호 정의](./media/hana-installation/image8_define_db_passwd.PNG)

인증서를 만들 때 hello 다음 상호 작용 해야 합니다. 다음 예와 같이 hello 대화 상자를 통해 이동 하 고 hello 단계를 진행 해야 합니다.

![SMT 서버의 인증서 만들기](./media/hana-installation/image9_certificate_creation.PNG)

몇 분 hello 구성의 hello 끝에는 '실행 동기화 검사' hello 단계에 소요 된 있을 수 있습니다. Hello 설치 및 hello SMT 서버의 구성을 수행한 후 hello 디렉터리 리포지토리 hello 탑재 지점 /srv/www/htdocs에서 찾아야/일부 하위 디렉터리가 리포지토리 plus입니다. 

Hello SMT 서버와 이러한 명령 사용 하 여 관련된 서비스를 다시 시작 합니다.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>SMT 서버에 패키지 다운로드

결국 hello 서비스를 다시 시작할 선택 hello Yast를 사용 하 여 SMT 관리에서 적절 한 패키지입니다. hello HANA 큰 인스턴스 서버의 hello OS 이미지에 및 SLES 릴리스 hello 또는 버전의 hello VM 실행 중인 hello SMT 서버에 없는 hello 패키지 선택에 따라 다릅니다. Hello 선택 화면의 예는 다음과 같습니다.

![패키지 선택](./media/hana-installation/image10_select_packages.PNG)

Hello 패키지 선택을 마치면 toostart hello 초기 복사본 hello 패키지 선택 toohello SMT 서버를 설정 해야 합니다. 이 복사본 hello 명령 smt 대칭 아래와 같이 사용 하 여 hello 셸에서 트리거됩니다.


![패키지 tooSMT 서버 다운로드](./media/hana-installation/image11_download_packages.PNG)

위에 표시 된 대로 hello 패키지 hello 탑재 지점 /srv/www/htdocs 아래에 생성 하는 hello 디렉터리에 복사 해야 합니다. 이 프로세스는 시간이 어느 정도 걸릴 수 있습니다. 선택한 패키지 수에 종속, tooone 시간 이상를 걸릴 수 있습니다.
이 프로세스를 완료 하는 대로 toomove toohello SMT 클라이언트 설치를 해야 합니다. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>HANA 큰 인스턴스 단위에 hello SMT 클라이언트 설정

이 경우 hello 클라이언트는 hello HANA 인스턴스가 큰 단위입니다. hello 스크립트 clientSetup4SMT.sh hello Azure VM에 복사 하는 hello SMT 서버 설치. Toohello tooconnect tooyour SMT 서버 인스턴스가 HANA 큰 단위를 통해 해당 스크립트를 복사 합니다. Hello-h 옵션으로 hello 스크립트를 시작한 SMT 서버 hello 이름을 매개 변수를 제공 합니다. 이 예제에서는 smtserver입니다.

![SMT 클라이언트 구성](./media/hana-installation/image12_configure_client.PNG)

여기서 hello hello 인증서 hello 클라이언트 hello 서버에서의 부하를 만들었지만 hello 등록 못했습니다 아래와 같이 시나리오 있을 수 있습니다.

![클라이언트 등록 실패](./media/hana-installation/image13_registration_failed.PNG)

Hello 등록에 실패 한 경우이 내용을 읽고 [SUSE 지원 문서](https://www.suse.com/de-de/support/kb/doc/?id=7006024) 있습니다 설명 하는 hello 단계를 실행 합니다.

> [!IMPORTANT] 
> 서버 이름으로 hello 정규화 된 도메인 이름 사용 하지 않고이 case smtserver에 VM hello의 tooprovide hello 이름이 필요 합니다. 방금 hello VM 이름 작동 합니다. 

Tooexecute hello hello HANA 큰 인스턴스 장치에서 다음 명령을 사용 해야 이러한 단계를 실행 한 후

```
SUSEConnect –cleanup
```

> [!Note] 
> 이 테스트에서 항상 했습니다 toowait 해당 단계 후 몇 분입니다. hello 즉시 실행 clientSetup4SMT.sh hello 수정 조치에에서 설명 된 후 hello SUSE 문서 종료 hello 인증서를 사용할 수 없습니다 아직 메시지와 함께 합니다. 대개 5~10분을 기다려서 clientSetup4SMT.sh를 실행하면 클라이언트 구성이 성공적으로 끝납니다.

Toofix hello SUSE 문서의 hello 단계에 따라 필요한 hello 문제를 실행 한 경우 toorestart clientSetup4SMT.sh hello HANA 큰 인스턴스 단위에 다시 필요 합니다. 이제 아래와 같이 성공적으로 완료됩니다.

![클라이언트 등록 성공](./media/hana-installation/image14_finish_client_config.PNG)

이 단계를 통해 hello Azure VM에에서 설치 하는 hello SMT 서버에 대 한 hello HANA 큰 인스턴스 단위 tooconnect의 hello SMT 클라이언트를 구성 합니다. 하면 이제 수 '를 zypper' 또는 '에서 zypper' tooinstall OS 패치 tooHANA 큰 인스턴스 걸리거나 추가 패키지를 설치 합니다. 만 얻을 수 있다는 패치 hello SMT 서버의 하기 전에 다운로드 한 것으로 간주 됩니다.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>HANA 큰 인스턴스에 SAP HANA 설치의 예
이 섹션에서는 어떻게 tooinstall SAP HANA HANA 큰 인스턴스 단위에 합니다. hello 시작 상태는 같습니다.

- 모든 hello 데이터 toodeploy Microsoft를 제공 하면 SAP HANA 큰 인스턴스.
- Microsoft에서 SAP HANA 대형 인스턴스 hello를 발생 했습니다.
- 연결 된 tooyour 온-프레미스 네트워크를 Azure VNet을 만들었습니다.
- HANA 큰 인스턴스 toohello hello ExpressRotue 회로 연결 같은 Azure VNet입니다.
- HANA 큰 인스턴스의 점프 박스로 사용하는 Azure VM을 설치했습니다.
- 그 반대의 hello 점프 상자 tooyour HANA 큰 인스턴스 장치에서 연결할 수 있는지 했습니다.
- 필요한 패키지가 모두 hello 및 패치가 설치 되어 있는지 여부를 선택한 합니다.
- SAP note hello 및 HANA hello 사용 하는 hello OS 버전에 선택한 hello HANA 릴리스를 지원 하는지 확인 하는 운영 체제에는 설치와 관련 된 문서를 읽을 있습니다.

Hello 다음 시퀀스에 표시 된 항목은 hello HANA 설치 패키지 toohello 점프 상자가 경우 hello 패키지 toohello HANA 큰 인스턴스 단위의 hello 복사본 및 hello 시퀀스 hello 설치 프로그램의 Windows OS에서 실행 중인 VM의 hello 다운로드 합니다.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Hello SAP HANA 설치 비트를 다운로드합니다
Hello HANA 큰 인스턴스 단위 직접 연결 toohello 없으므로 인터넷에 직접을 다운로드할 수 없습니다 hello 설치 패키지에서 SAP HANA 큰 인스턴스 VM toohello 합니다. hello 점프 상자를 해야 tooovercome hello 누락 직접 인터넷에 연결 합니다. Hello 패키지 toohello 점프 상자 VM을 다운로드 합니다.

순서 toodownload hello HANA 설치 패키지를 SAP S 사용자 또는 있습니다 tooaccess hello SAP Marketplace를 다른 사용자에 필요 합니다. 로그인한 후 화면의 순서에 따라 이동합니다.

너무 이동[SAP Service Marketplace](https://support.sap.com/en/index.html) > 소프트웨어 다운로드 클릭 > 설치 및 업그레이드 > 사전순 인덱스 > 아래에서 H-SAP HANA 플랫폼 버전 > SAP HANA 플랫폼 버전 2.0 > 설치 > 다운로드 hello 다음 파일

![HANA 설치 다운로드](./media/hana-installation/image16_download_hana.PNG)

Hello 데모 경우에서 SAP HANA 2.0 설치 패키지를 다운로드 했습니다. Hello Azure 점프 상자 VM에서 아래와 같이 hello 디렉터리로 hello 자동 압축 풀기 아카이브를 확장 합니다.

![HANA 설치 추출](./media/hana-installation/image17_extract_hana.PNG)

Hello 보관 파일을 추출한 대로 51052030, 사용자가 만든 디렉터리에 hello /hana/shared 볼륨으로 toohello HANA 큰 인스턴스 단위 위에 hello 경우 hello 추출 하 여 만든 hello 디렉터리를 복사 합니다.

> [!Important]
> 공간 제한 되며 toobe도 다른 프로세스에서 사용 해야 하므로 LUN 부팅 하거나 hello 루트 hello 설치 패키지를 복사 하지 마십시오.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>SAP HANA hello HANA 큰 인스턴스 장치에 설치
순서 tooinstall SAP HANA 사용자 루트로 toolog에 필요합니다. 루트만 충분 한 사용 권한을 tooinstall SAP HANA에 있습니다.
hello 먼저 toodo 필요한 것은 tooset/hana/공유로 복사한 hello 디렉터리에 대 한 권한을 합니다. hello 권한이 같은 tooset 필요

```
chmod –R 744 <Installation bits folder>
```

SAP HANA tooinstall 원하는 그래픽 hello를 사용 하 여 설치 프로그램을 hello gtk2 패키지 요구 toobe hello HANA 큰 인스턴스에 설치 합니다. Hello 명령을 사용 하 여 설치 되어 있는지 확인

```
rpm –qa | grep gtk2
```

추가 단계에 hello 그래픽 사용자 인터페이스를 사용 하 여 hello SAP HANA 설치를 보여 주는 했습니다. 다음 단계로, hello 설치 디렉터리로 이동한 다음 hello 하위 디렉터리 HDB_LCM_LINUX_X86_64 트리로 이동 합니다. 시작

```
./hdblcmgui 
```
해당 디렉터리에서. 이제 시작 안내 스크린의 시퀀스 hello 설치에 대 한 tooprovide hello 데이터를 해야 합니다. Hello 경우 설명 hello SAP HANA 데이터베이스 서버와 hello SAP HANA 클라이언트 구성 요소 설치 합니다. 따라서 아래와 같이 'SAP HANA Database'(SAP HANA 데이터베이스)가 선택됩니다.

![설치 시 HANA 선택](./media/hana-installation/image18_hana_selection.PNG)

Hello 다음 화면에서 선택 hello ' 새 시스템 설치 '

![HANA 신규 설치 선택](./media/hana-installation/image19_select_new.PNG)

또한 설치할 수 있는 몇 가지 추가 구성 요소 간의 tooselect이 단계 필요한 toohello SAP HANA 데이터베이스 서버입니다.

![추가 HANA 구성 요소 선택](./media/hana-installation/image20_select_components.PNG)

이 설명서의 hello 목적으로 SAP HANA 클라이언트 hello 선택한 म 및 SAP HANA Studio hello 합니다. 강화 인스턴스도 설치했습니다. 따라서 toochoose ' 단일 호스트 시스템 ' 필요한 hello 다음 화면에서 

![강화 설치 선택](./media/hana-installation/image21_single_host.PNG)

Hello 다음 화면에서 필요한 tooprovide 일부 데이터

![SAP HANA SID 제공](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> 으로 HANA 시스템 ID (SID)를 해야 tooprovide hello HANA 큰 인스턴스 배포를 정렬 하는 경우 Microsoft 제공 된 동일한 SID를 hello 합니다. Hello 설치 hello 서로 다른 볼륨에 tooaccess 사용 권한 문제로 인해 실패 하면 다른 SID를 선택 합니다.

설치 디렉터리와 hello /hana/shared 디렉터리를 사용합니다. 다음 단계 hello hello HANA 데이터 파일 및 hello HANA 로그 파일에 대 한 tooprovide hello 위치 필요


![HANA 로그 위치 제공](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> 데이터 및 로그 파일 hello hello이이 화면 하기 전에 hello 화면 선택 영역에서 선택한 SID를 포함 하는 hello 탑재 지점이 있는 이미 제공 된 볼륨으로 정의 해야 합니다. 이전에 hello 화면에을 입력 한 하나 hello로 hello SID가 일치 하지 않습니다 돌아가서를 hello hello 탑재 지점에 있는 SID toohello 값을 조정 합니다.

Hello 다음 단계에서 hello 호스트 이름을 검토 하 고 결국를 수정 합니다. 

![호스트 이름 검토](./media/hana-installation/image24_review_host_name.PNG)

Hello 다음 단계에서 tooretrieve 데이터 tooMicrosoft 제공한 hello HANA 큰 인스턴스 배포를 정렬 하는 경우 필요 합니다. 

![시스템 사용자 UID 및 GID 제공](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Tooprovide 필요한 hello 단위 배포를 순서 대로 Microsoft에 제공 된 대로 동일한 시스템 사용자 ID 및 사용자 그룹의 ID를 hello 합니다. 매우 toogive hello를 실패 한 경우 동일한 Id를 hello HANA 큰 인스턴스 단위에 SAP HANA의 hello 설치가 실패 합니다.

에서는이 설명서에 표시 되지 않으면 있는 hello 다음 두 화면 hello SAP HANA 데이터베이스와 hello의 일부로 설치 되는 SAP 호스트 에이전트에 사용 되는 hello sapadm 사용자에 대 한 hello 암호의 hello 시스템 사용자에 대 한 tooprovide hello 암호 필요 hello SAP HANA 데이터베이스 인스턴스입니다.

Hello 암호를 정의한 후 확인 화면이 표시 됩니다. hello 데이터를 모두 나열 하 고 hello 설치를 계속 확인 합니다. 문서 hello hello 하나 아래와 같은 설치 진행률 진행률 화면이

![설치 진행률 확인](./media/hana-installation/image27_show_progress.PNG)

하나를 따르는 hello와 같은 그림 해야 hello 설치 완료

![설치를 마쳤습니다.](./media/hana-installation/image28_install_finished.PNG)

이 시점에서 hello SAP HANA 인스턴스 사용에 대 한 최대 및 실행 되 고 준비가 완료 이어야 합니다. SAP HANA studio에서 수 tooconnect tooit 있어야 합니다. 또한 SAP HANA의 hello 최신 패치를 확인 하 고 패치를 적용 해야 합니다.
























































 







 




