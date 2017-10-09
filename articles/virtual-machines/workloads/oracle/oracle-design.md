---
title: "Azure에서 데이터베이스 aaaDesign 및 Oracle 구현 | Microsoft Docs"
description: "Azure 환경에서 Oracle 데이터베이스를 설계하고 구현합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Azure에서 Oracle 데이터베이스 설계 및 구현

## <a name="assumptions"></a>가정

- Oracle 데이터베이스에서 온-프레미스 tooAzure toomigrate를 계획 중인 합니다.
- Hello에 대 한 이해가 다양 한 메트릭을 보고서에 있는 Oracle AWR 합니다.
- 응용 프로그램 성능 및 플랫폼 사용률에 대해 기본적으로 이해하고 있습니다.

## <a name="goals"></a>목표

- 이해 어떻게 toooptimize Azure에서 Oracle 배포 합니다.
- Azure 환경에서 Oracle 데이터베이스에 대한 성능 튜닝 옵션을 탐색합니다.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>온-프레미스 간의 차이점을 hello 및 Azure 구현 

다음은 몇 가지 중요 한 마이그레이션하는 경우 고려에서 사항 tookeep 온-프레미스 응용 프로그램 tooAzure입니다. 

중요한 차이점 중 하나는 Azure 구현에서 VM, 디스크 및 가상 네트워크와 같은 리소스가 다른 클라이언트와 공유된다는 것입니다. 또한 리소스 hello 요구 사항에 따라 제한 될 수 있습니다. 보다 MTBF ()를 실패를 방지, Azure는 더 hello 실패 (MTTR) 정상 작동 하는 데 사용 합니다.

hello 다음 표에 온-프레미스 구현 및 Oracle 데이터베이스의 Azure 구현 hello 차이점 있습니다.

> 
> |  | **온-프레미스 구현** | **Azure 구현** |
> | --- | --- | --- |
> | **네트워킹** |LAN/WAN  |SDN(소프트웨어 방식 네트워킹)|
> | **보안 그룹** |IP/포트 제한 도구 |[NSG(네트워크 보안 그룹)](https://azure.microsoft.com/blog/network-security-groups) |
> | **복원력** |MTBF(평균 고장 간격) |MTTR (그리니치 표준시 toorecovery)|
> | **계획된 유지 보수** |패치/업그레이드|[가용성 집합](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)(Azure에서 관리되는 패치/업그레이드) |
> | **리소스** |전용  |다른 클라이언트와 공유|
> | **지역** |데이터 센터 |[지역 쌍](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **저장소** |SAN/실제 디스크 |[Azure 관리 저장소](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **규모** |수직적 확장 |수평적 확장|


### <a name="requirements"></a>요구 사항

- Hello 데이터베이스 크기 및 증가 속도 결정 합니다.
- Oracle AWR 보고서 또는 다른 네트워크 모니터링 도구에 따라 예측할 수 hello IOPS 요구를 확인 합니다.

## <a name="configuration-options"></a>구성 옵션

네 가지 잠재적인 영역은 Azure 환경에서 tooimprove 성능을 튜닝할 수 있습니다.

- 가상 컴퓨터 크기
- 네트워크 처리량
- 디스크 형식 및 구성
- 디스크 캐시 설정

### <a name="generate-an-awr-report"></a>AWR 보고서 생성

Oracle 데이터베이스를 기존 toomigrate tooAzure 계획 하는 경우 몇 가지 옵션이 있습니다. Hello Oracle AWR 보고서 tooget hello 메트릭 (IOPS, Mbps, GiBs, 및 등)를 실행할 수 있습니다. Hello 수집한 hello 메트릭을 기준으로 VM을 선택 합니다. 또는 인프라 팀 tooget 유사한 정보를 문의할 수 있습니다.

일반 및 최대 워크로드 모두에서 AWR 보고서를 실행하여 비교하는 것이 좋을 수도 있습니다. 이러한 보고서에 따라, 크기를 Vm hello 평균 작업 또는 hello 최대 작업 부하에 따라 hello.

다음은 방법의 예로 toogenerate AWR 보고서:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>주요 메트릭

다음은 hello AWR 보고서에서에서 얻을 수 있는 hello 메트릭:

- 총 코어 수
- CPU 클럭 속도
- 전체 메모리(GB)
- CPU 사용률
- 최대 데이터 전송 속도
- I/O 변경률(읽기/쓰기)
- 다시 실행 로그 속도(MBPs)
- 네트워크 처리량
- 네트워크 대기 시간 비율(낮음/높음)
- 데이터베이스 크기(GB)
- SQL을 통해 받은 바이트 *에서 Net / tooclient

### <a name="virtual-machine-size"></a>가상 컴퓨터 크기

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. AWR 보고서 hello에서 CPU, 메모리 및 I/O 사용량에 따라 VM 크기 예측

살펴볼 수 있습니다는 hello 상위 5 개 전경 시간이 지정 된 이벤트를 나타내는 hello 시스템 병목 현상이 있는 합니다.

예를 들어 다음 다이어그램 hello, hello 위쪽에서 hello 로그 파일 동기화가 됩니다. Hello hello는 LGWR hello 로그 버퍼 toohello 다시 실행 로그 파일을 작성 하기 전에 필요 없는 대기 수를 나타냅니다. 이러한 결과는 더 효율적으로 수행되는 저장소 또는 디스크가 필요함을 나타냅니다. 또한 hello 다이어그램은 hello 수가 CPU (코어) 크기 및 메모리 양을 hello 표시 합니다.

![Hello AWR 보고서 페이지의 스크린샷](./media/oracle-design/cpu_memory_info.png)

hello 다음 그림에 대 한 읽기 및 쓰기의 총 I/O hello 합니다. 읽을 59 GB와 247.3 GB hello 보고서의 hello 시간 중에 기록 했습니다.

![Hello AWR 보고서 페이지의 스크린샷](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. VM 선택

Hello AWR 보고서에서에서 수집 하는 hello 정보에 따라 hello 다음 단계는 요구 사항을 충족 하는 비슷한 크기의 VM toochoose입니다. Hello 문서에서 사용 가능한 Vm의 목록을 찾을 수 있습니다 [메모리 액세스에 최적화](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory)합니다.

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Hello ACU에 따라 유사한 VM 시리즈와 hello VM 크기를 미세 조정

Hello VM을 선택한 후에 주의 기울여야 toohello ACU hello VM에 대 한 지불 합니다. Hello 요구 사항에 가장 잘 맞는 ACU 값에 따라 다른 VM을 선택할 수 있습니다. 자세한 내용은 [ACU(Azure Compute 단위)](https://docs.microsoft.com/azure/virtual-machines/windows/acu)를 참조하세요.

![Hello ACU 단위 페이지의 스크린샷](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>네트워크 처리량

다음 다이어그램 hello 처리량 및 iops 수 간에 hello 관계를 보여 줍니다.

![처리량 스크린샷](./media/oracle-design/throughput.png)

hello 총 네트워크 처리량 hello 다음 정보에 따라 예상 됩니다.
- SQL*Net 트래픽
- MBps x 서버 수(Oracle Data Guard와 같은 아웃바운드 스트림)
- 응용 프로그램 복제와 같은 다른 요소

![스크린샷 hello SQL * Net 처리량](./media/oracle-design/sqlnet_info.png)

네트워크 대역폭 요구 사항에 따라는에서 toochoose에 대 한 다양 한 게이트웨이 유형이 있습니다. 여기에는 기본, VpnGw 및 Azure ExpressRoute가 포함됩니다. 자세한 내용은 참조 hello [VPN 게이트웨이 가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h)합니다.

**권장 사항**

- 네트워크 대기 시간이 더 높은 비교 tooan 온-프레미스 배포 됩니다. 네트워크 왕복 수를 줄이면 성능이 크게 향상될 수 있습니다.
- tooreduce 왕복 통합 또는 응용 프로그램을 높은 트랜잭션 "수 다 스러운" 앱 hello에 동일한 가상 컴퓨터.

### <a name="disk-types-and-configurations"></a>디스크 형식 및 구성

- *기본 OS 디스크*: 이러한 디스크 유형은 영구 데이터 및 캐싱을 제공합니다. 시작 시 OS 액세스에 최적화되며, 트랜잭션 또는 데이터 웨어하우스(분석) 워크로드용으로는 설계되지 않았습니다.

- *디스크 관리 되지 않는*: tooyour VM 디스크를 해당 하는 hello 가상 하드 디스크 (VHD) 파일을 저장 하는 hello 저장소 계정의 이러한 디스크 형식으로 관리 합니다. VHD 파일은 Azure Storage 계정에 페이지 Blob으로 저장됩니다.

- *관리 디스크*: Azure가 VM 디스크를 사용 하는 hello 저장소 계정을 관리 합니다. Hello 디스크 유형 (프리미엄 또는 표준)와 필요한 hello 디스크의 hello 크기를 지정 합니다. Azure 만들고에서 hello 디스크를 관리 합니다.

- *프리미엄 저장소 디스크*: 이러한 디스크 유형은 프로덕션 워크로드에 가장 적합합니다. 프리미엄 저장소에서는 VM 디스크 일 수 있는 연결 toospecific 크기 시리즈 Vm DS, DSv2, GS 및 F 시리즈 Vm 등. hello 프리미엄 디스크는 크기가 다양 하 고 32GB too4, 096 GB에서에서 범위의 디스크 중에서 선택할 수 있습니다. 디스크 크기마다 자체 성능 사양이 있습니다. 응용 프로그램 요구 사항에 따라 하나 이상의 디스크 tooyour VM을 연결할 수 있습니다.

Hello hello 포털에서 새 관리 되는 디스크를 만들 때 선택할 수 있습니다 **계정 유형** 원하는 toouse hello 유형의 디스크에 대 한 합니다. 모든 사용 가능한 디스크 hello 드롭 다운 메뉴에 표시 된 염두에서에 둬야 합니다. 특정 VM 크기를 선택한 후만 hello 사용할 수 있는 프리미엄 저장소는 v M 크기를 기반으로 하는 Sku hello 메뉴에 표시 됩니다.

![Hello 관리 되는 디스크 페이지의 스크린샷](./media/oracle-design/premium_disk01.png)

자세한 내용은 [VM의 고성능 Premium Storage 및 관리 디스크](https://docs.microsoft.com/azure/storage/storage-premium-storage)를 참조하세요.

VM의 저장소를 구성한 후에 데이터베이스를 만들기 전에 tooload 테스트 hello 디스크를 할 수 있습니다. 대상 대기 시간으로 처리량을 예상 알면 대기 시간 및 처리량이 모두를 기준으로 hello I/O 속도 수 hello Vm hello를 지원 하는지 확인 합니다.

Oracle Orion, Sysbench 및 Fio와 같이 응용 프로그램 부하 테스트를 위한 여러 가지 도구가 있습니다.

Oracle 데이터베이스를 배포한 후에 hello 부하 테스트를 다시 실행 합니다. 일반와 최대 작업을 시작 하 고 사용자 환경의 초기 hello 결과 표시 hello 키를 누릅니다.

Hello 저장소 크기 보다는 hello IOPS 속도에 따라 더 중요 한 toosize hello 저장 수도 있습니다. 예를 들어 hello IOPS는 5, 000 하지만 200GB 하면 필요한 경우 받게 될 수 있습니다 hello P30 클래스 프리미엄 디스크 저장소 200GB 이상의 함께 제공 하는 경우에 합니다.

hello IOPS 속도 hello AWR 보고서에서에서 얻을 수 있습니다. Hello 다시 실행 로그, 물리적 읽기 및 쓰기 속도 의해 결정 됩니다.

![Hello AWR 보고서 페이지의 스크린샷](./media/oracle-design/awr_report.png)

예를 들어 hello redo 크기는 같은 too11.63 MBPs는 초당 12,200,000 바이트입니다.
hello IOPS는 12,200,000 / 2,358 = 5,174 합니다.

Hello I/O 요구 사항 명확히를 설정한 후 이러한 요구 사항에 가장 적합 한 toomeet 있는 드라이브의 조합을 선택할 수 있습니다.

**권장 사항**

- 데이터 테이블 스페이스에 대 한 분산 hello I/O 작업이 디스크 수가 Oracle ASM 또는 관리 되는 저장소를 사용 하 여 있습니다.
- Hello I/O 블록 크기 증가 읽기 또는 쓰기를 많이 사용 작업에 대 한 데이터 디스크를 추가 합니다.
- 대형 순차 프로세스에 대 한 hello 블록 크기를 늘립니다.
- 데이터 압축 tooreduce I/O를 사용 하 여 (에 대 한 데이터 및 인덱스).
- 개별 데이터 디스크에서 다시 실행 로그, 시스템, 임시 디스크를 분리하고 TS를 실행 취소합니다.
- 기본 OS 디스크(/dev/sda)에 응용 프로그램 파일을 배치하지 않습니다. 이러한 디스크는 빠른 VM 부팅 시간에 맞게 최적화되지 않으며, 응용 프로그램에 좋은 성능을 제공하지 않을 수 있습니다.

### <a name="disk-cache-settings"></a>디스크 캐시 설정

호스트 캐싱에는 세 가지 옵션이 있습니다.

- *읽기 전용*: 모든 요청이 이후 읽기를 위해 캐시됩니다. 모든 쓰기 유지 되는 직접 tooAzure Blob 저장소입니다.

- *읽기-쓰기*: "미리 읽기" 알고리즘입니다. hello를 읽고 쓰기 이후 읽기에 대해 캐시 합니다. 비-통한 쓰기 쓰기는 먼저 toohello 로컬 캐시를 유지 합니다. SQL Server에 대 한 쓰기 쓰기 사용 하기 때문에 지속형된 tooAzure 저장소는입니다. 또한 밝은 작업에 대 한 hello 가장 낮은 디스크 대기 시간을 제공합니다.

- *None* (사용 안 함):이 옵션을 사용 하 여 hello 캐시를 무시할 수 있습니다. 모든 hello 데이터 전송된 toodisk 되어 tooAzure 저장소를 유지 합니다. I/O 집약적인 작업을 위해 높은 I/O 속도 hello를 사용 하는 메서드가 있습니다. 또한 해야 tootake "트랜잭션 비용"를 고려 합니다.

**권장 사항**

toomaximize hello 처리량 권장으로 시작 하는 **None** 캐시 호스트에 대 한 합니다. 프리미엄 저장소에 대 한 염두 hello로 hello 파일 시스템을 탑재 하면 장벽을"hello"를 해제 해야 **ReadOnly** 또는 **None** 옵션입니다. Hello UUID toohello 디스크와 hello /etc/fstab 파일을 업데이트 합니다.

자세한 내용은 [Linux VM용 Premium Storage](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms)를 참조하세요.

![Hello 관리 되는 디스크 페이지의 스크린샷](./media/oracle-design/premium_disk02.png)

- OS 디스크의 경우 기본 **읽기/쓰기** 캐싱을 사용합니다.
- 시스템, 임시 및 실행 취소 디스크의 경우 캐싱에 **없음**을 사용합니다.
- 데이터 디스크의 경우 캐싱에 **없음**을 사용합니다. 그러나 데이터베이스가 읽기 전용이거나 읽기 집약적인 경우 **읽기 전용** 캐싱을 사용합니다.

저장 된 데이터 디스크 설정은 운영 체제 수준 hello에 hello 드라이브를 마운트 해제 하 고 변경 하는 hello를 변경한 후 다시 탑재 하지 않으면 hello 호스트 캐시 설정을 변경할 수 없습니다.


## <a name="security"></a>보안

설정 및 Azure 환경을 구성 해야, hello 다음 단계는 toosecure 네트워크입니다. 몇 가지 권장 사항입니다.

- *NSG 정책*: NSG는 서브넷 또는 NIC에서 정의될 수 있습니다. 것 hello 서브넷 수준 보안 및 응용 프로그램 방화벽 등을 위한 강제로 라우팅에 모두에서 간단한 toocontrol 액세스 합니다.

- *Jumpbox*: 보다 안전한 액세스를 위해 관리자가 연결 하지 않도록 직접 toohello 응용 프로그램 서비스 또는 데이터베이스입니다. jumpbox hello 관리자 컴퓨터와 Azure 리소스 간의 미디어로 사용 됩니다.
![Hello Jumpbox 토폴로지 페이지의 스크린샷](./media/oracle-design/jumpbox.png)

    hello 관리자 컴퓨터만 toohello jumpbox IP 제한 된 액세스를 제공 해야 합니다. hello jumpbox 액세스 toohello 응용 프로그램 및 데이터베이스가 있어야 합니다.

- *개인 네트워크* (서브넷): hello 응용 프로그램 서비스 및 데이터베이스에 있는지 별도 서브넷을 더 세부적으로 제어할 NSG 정책에 의해 설정 될 수 있도록 하는 것이 좋습니다.


## <a name="additional-reading"></a>추가 참조 자료

- [Oracle ASM 구성](configure-oracle-asm.md)
- [Oracle Data Guard 구성](configure-oracle-dataguard.md)
- [Oracle Golden Gate 구성](configure-oracle-golden-gate.md)
- [Oracle 백업 및 복구](oracle-backup-recovery.md)

## <a name="next-steps"></a>다음 단계

- [자습서: 고가용성 VM 만들기](../../linux/create-cli-complete.md)
- [VM 배포 Azure CLI 샘플 탐색](../../linux/cli-samples.md)
