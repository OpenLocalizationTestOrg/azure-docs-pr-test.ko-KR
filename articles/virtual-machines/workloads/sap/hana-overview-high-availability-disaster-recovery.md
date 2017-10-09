---
title: "(대형 인스턴스) Azure에서 SAP HANA의 aaaHigh 고가용성 및 재해 복구 | Microsoft Docs"
description: "Azure(큰 인스턴스)의 SAP HANA에 대한 고가용성을 달성하고 및 재해 복구를 계획합니다."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
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
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>Azure(큰 인스턴스)의 SAP HANA 고가용성 및 재해 복구 

Azure(큰 인스턴스) 서버에서 업무상 중요한 SAP HANA를 실행할 때 고가용성 및 재해 복구는 중요한 측면입니다. 중요 한 toowork sap, 시스템 통합 업체 또는 Microsoft tooproperly 설계자와 구현 hello 오른쪽 우선-가용성/재해 복구 전략입니다. 중요 한 tooconsider hello 복구 지점 목표 및 복구 시간 목표를 특정 tooyour 환경 이기도 합니다.

## <a name="high-availability"></a>고가용성

Microsoft는 포함 하는 SAP HANA 고가용성 방법을 "hello 상자 부족"를 지원 합니다.

- **저장소 복제:** hello 기능 tooreplicate 저장소 시스템의 모든 데이터 tooanother 위치 (내에서 또는 별도의 hello 동일한 데이터 센터). SAP HANA는 이 메서드와 독립적으로 작동합니다.
- **HANA 시스템 복제:** SAP HANA tooa 별도 SAP HANA 시스템의 모든 데이터의 복제 hello 합니다. hello 복구 시간 목표는 정기적으로 데이터 복제를 통해 최소화 됩니다. 비동기, 동기 메모리 내 및 동기 모드를 지원 하는 SAP HANA (SAP HANA에만 권장 시스템 내에 있는 동일한 데이터 센터 또는 보다 작거나 100 KM 떨어져 있는 hello). 현재 디자인 HANA 큰 인스턴스 스탬프의 hello에서는 고가용성만 HANA 시스템 복제를 사용할 수 있습니다.
- **자동 장애 조치 호스트:** 대체 toosystem 복제로 로컬 오류 복구 솔루션 toouse 합니다. Hello 마스터 노드를 사용할 수 없을 때 SAP HANA tooanother 노드를 통해 자동으로 장애 및 하나 이상의 대기 SAP HANA 노드 확장 모드에서 구성 됩니다.

SAP HANA 고가용성에 대 한 자세한 내용은 다음 SAP 정보 hello를 참조 하세요.

- [SAP HANA 고가용성 백서](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [SAP HANA 관리 가이드](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [SAP HANA 시스템 복제에 대한 SAP Academy 비디오](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP 지원 참고 사항 #1999880 – SAP HANA 시스템 복제에 대한 FAQ](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP 지원 참고 사항 #2165547 – SAP HANA 시스템 복제 환경 내의 SAP HANA 백업 및 복원](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP 지원 참고 사항 #1984882 – 가동 중지 시간이 최소/없는 하드웨어 Exchange에 대한 SAP HANA 시스템 복제 사용](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>재해 복구

Azure(큰 인스턴스)의 SAP HANA가 지역 정책 지역에 있는 여러 Azure 지역에 제공됩니다. 두 개의 서로 다른 지역에 대 한 두 개의 큰 인스턴스 스탬프 hello 사이 재해 복구 시 데이터를 복제에 대 한 네트워크에 직접 연결 합니다. hello 데이터의 hello 복제는 저장소 인프라를 기반으로 합니다. 기본적으로 hello 복제 수행 되지는 않습니다. Hello 재해 복구를 정렬 하는 hello 고객 구성에 대 한 것입니다. Hello 현재 디자인 재해 복구를 위해 HANA 시스템 복제를 사용할 수 없습니다.

그러나 tootake 이점은 toostart toodesign hello 네트워크 연결 toohello 두 개의 서로 다른 Azure 지역 hello 재해 복구 해야 합니다. toodo, 주요 Azure 지역이 및 온-프레미스 tooyour 재해 복구 지역에서 다른 회로 연결에 온-프레미스에서 Azure express 경로 회로 연결을 해야 합니다. 이러한 측정값은 MSEE(Microsoft Enterprise Edge 라우터) 위치를 포함하는 전체 Azure 지역에 문제가 발생한 상황에 적용됩니다.

두 번째 측정값으로 이러한 ExpressRoute 회로의 hello 영역 tooboth 중 하나에 tooSAP HANA Azure (대형 인스턴스)에 연결 하는 모든 Azure 가상 네트워크를 연결할 수 있습니다. 사용 안 함 흐름 방향은 하나만 hello MSEE 위치 Azure와 온-프레미스 위치를 연결 하는 경우가이 측정값을 해결 합니다.

hello 다음 그림과 hello 재해 복구를 위한 최적의 구성:

![재해 복구에 대한 최적의 구성](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

hello 최적의 사례 hello 네트워크의 재해 복구 구성에 대 한는 온-프레미스 toohello 두 개의 서로 다른 Azure 지역에서 두 개의 ExpressRoute 회로 toohave입니다. 하나의 회로 이동 tooregion #1 프로덕션 인스턴스를 실행 합니다. ExpressRoute 회로 두 번째 hello tooregion # 2를 실행 중인 일부 비-프로덕션 HANA 인스턴스를 이동 합니다. (이 hello 눈금 MSEE hello 및 큰 인스턴스 스탬프를 포함 하는 전체 Azure 지역 중 중요 합니다.)

두 번째 측정값으로 hello 다양 한 가상 네트워크는 연결 된 toohello 연결된 tooSAP HANA Azure (대형 인스턴스)에 있는 다양 한 express 경로 회로 합니다. 나중에 설명 된 대로 MSEE, 실패 또는 재해 복구에 대 한 hello 복구 지점 목표를 낮출 수 hello 위치를 무시할 수 있습니다.

에 재해 복구 설치에 대 한 hello 다음 요구 사항:

- hello Sku 프로덕션으로 크기를 동일 하 고 hello 재해 복구 지역에 배포 합니다 (대형 인스턴스) Azure Sku에서 SAP HANA를 주문 해야 합니다. 이러한 인스턴스를 사용 하는 toorun 테스트, 샌드박스 또는 QA HANA 인스턴스 수입니다.
- 순서 지정 해야 재해 복구 프로필 각각의 Sku (대형 인스턴스) Azure에서 SAP HANA 프로그램에 대 한 원하는 toorecover hello 재해 복구 사이트에서 필요한 경우. 이 동작으로 인해 다시 toohello hello 재해 복구 영역에 프로덕션 지역에서 저장소 복제 hello의 hello 대상 저장소 볼륨을 할당 합니다.

Hello 앞에 요구 사항을 충족 시키면 책임 toostart hello 저장소 복제 됩니다. Hello 저장소 인프라 (대형 인스턴스) Azure에서 SAP HANA에 사용 되는 저장소 복제의 hello 기반 저장소 스냅숏을입니다. toostart hello 재해 복구 복제 tooperform이 필요합니다.

- 앞서 설명한 대로 부팅 LUN의 스냅숏
- 앞서 설명한 대로 HANA 관련 볼륨의 스냅숏

이러한 스냅숏을 실행 하 고 나면 hello 볼륨의 초기 복제본 hello 재해 복구 지역에서 재해 복구 프로필 연관 된 hello 볼륨에 마련 됩니다.

Hello 가장 최근의 저장소 스냅숏이 1 시간 마다 사용 이후에 tooreplicate hello 델타 hello 저장소 볼륨을 개발 하는 합니다.

이 구성을 지원 hello 복구 지점 목표 60 too90 분에서입니다. tooachieve 더 빠른 복구 지점 목표 hello 재해 복구 경우 복사 hello HANA에서 트랜잭션 로그 백업에서 SAP HANA toohello Azure (대형 인스턴스)를 다른 Azure 지역입니다. tooachieve이 복구 지점 목표를 사용 하 여 다음 hello지 않습니다.

1. Hello HANA 트랜잭션 로그를 백업 자주 가능한 너무/hana/로그/백업 합니다.
2. 완성 된 tooan toohello SAP HANA (대형 인스턴스) Azure 서버에 연결 된 가상 네트워크에 있는 Azure 가상 컴퓨터 (VM) 될 때 hello 트랜잭션 로그 백업을 복사 합니다.
3. 해당 VM에서 hello 백업 tooa hello 재해 복구 지역에서 가상 네트워크에 있는 VM을 복사 합니다.
4. Hello VM에서에서 해당 지역에서 hello 트랜잭션 로그 백업을 유지 합니다.

재해가 발생할 경우 재해 복구 프로필 hello 실제 서버에 배포한 후 hello 트랜잭션 로그 백업을 복사 hello VM toohello Azure (대형 인스턴스)는 이제 hello hello 재해 복구 영역에 주 서버에서 SAP HANA에서에서 및 이러한 백업을 복원 합니다. 이 복구가 없기 때문에 hello HANA hello 재해 복구 디스크 상태가 HANA 스냅숏 합니다. 추가 트랜잭션 로그 백업 복원에 대 한 hello 오프셋된 지점입니다.

## <a name="backup-and-restore"></a>백업 및 복원

Hello 가장 중요 한 측면 toooperating 데이터베이스 중 하나 있는지 확인 하에서 다양 한 치명적인 이벤트 hello 데이터베이스를 보호할 수 있습니다. 자연 재해 toosimple 사용자 오류 로부터 이러한 이벤트는 아무것도 발생할 수 있습니다.

데이터베이스 데이터베이스 hello 기능 toorestore 것 tooany 지점에서에서 백업 시간 (같은 누군가가 중요 한 데이터를 삭제 하기 전에), 허용 가능한 toohello 방식으로 hello 중단이 발생 한 하기 전의 가까운 복원 tooa 상태입니다.

최상의 결과를 위해 두 가지 백업을 수행해야 합니다.

- 데이터베이스 백업
- 트랜잭션 로그 백업

또한 응용 프로그램 수준에서 수행 toofull 데이터베이스 백업과 할 수 있습니다 더욱 철저 한 저장소 스냅숏과 함께 백업을 수행 하 여. 로그 백업을 수행 hello 데이터베이스 (및 이미 커밋된 트랜잭션에서 tooempty hello 로그) 복원을 위해 중요 이기도 합니다.

Azure(큰 인스턴스)의 SAP HANA는 다음과 같은 두 개의 백업과 옵션을 제공합니다.

- DIY(Do It Yourself) Tooensure 충분 한 디스크 공간을 계산한 후 디스크 백업 방법 (toothose 디스크)를 사용 하 여 전체 데이터베이스 및 로그 백업을 수행 합니다. 시간이 지남에 따라 hello 백업은 복사한 tooan Azure 저장소 계정 (설정한 후 거의 무제한 저장을 사용 하는 Azure 기반 파일 서버) 또는 Azure 백업 자격 증명 모음 또는 Azure 콜드 저장소를 사용 합니다. 다른 방법은 Commvault, toostore hello 백업을 한 후 복사 tooa 저장소 계정 등 toouse 제 3 자 데이터 보호 도구입니다. 백업 옵션 DIY hello toobe 준수 및 감사 목적에 대 한 장기간 저장 해야 하는 데이터에 필요한 수도 있습니다.
- Hello 백업을 사용 하 고 복원 hello (대형 인스턴스) Azure에서 SAP HANA의 기본 인프라 기능을 제공 합니다. 이 옵션 백업에 대 한 hello 요구를 충족 하 고 수동 백업을 (여기서 데이터 백업을 규정 준수를 위해 필요한)를 제외한 거의 사용 되지 않는입니다. 이 섹션에서는 나머지 hello 백업 hello 및 HANA (대형 인스턴스)를 제공 하는 기능을 복원 합니다.

> [!NOTE]
> hello 스냅숏 기술 hello HANA (대형 인스턴스)의 기본 인프라에서 사용 되는 SAP HANA 스냅숏에 대 한 종속성을 갖습니다. SAP HANA 스냅숏은 SAP HANA 다중 테넌트 데이터베이스 컨테이너와 함께 작동하지 않습니다. 결과적으로, 이러한 방식의 백업 사용 하는 toodeploy SAP HANA 다중 테 넌 트 데이터베이스 컨테이너 수 없습니다.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Azure(큰 인스턴스)의 SAP HANA 저장소 스냅숏 사용

hello 저장소 인프라 (대형 인스턴스) Azure에서 SAP HANA를 기본 볼륨의 저장소 스냅숏의 hello 개념을 지원 합니다. 다음 고려 사항 hello로 백업 및 특정 볼륨의 복원은 모두 지원 됩니다.

- 데이터베이스 백업 대신 저장소 볼륨 스냅숏을 자주 사용합니다.
- hello 저장소 스냅숏을 실행 하기 전에 hello 저장소 스냅숏 SAP HANA 스냅숏을 시작 합니다. 이 SAP HANA 스냅숏에 hello 저장소 스냅숏의 복구 후 최종 로그 복원에 대 한 hello 설치 지점입니다.
- Hello 저장소 스냅숏이 성공적으로 실행 된 hello 지점에 hello SAP HANA 스냅숏이 삭제 됩니다.
- 로그 백업은 자주 수행 되며 Azure의 hello 로그 백업 볼륨에 저장 됩니다.
- Hello 데이터베이스를 복원 해야 하는 경우 tooa 특정 지정 시간, 요청이 있는 Azure 서비스 관리 toorestore tooa tooMicrosoft Azure 지원 (프로덕션 작동 중단) 또는 SAP HANA 특정 저장소 (예를 들어 계획 된 복원 샌드박스 시스템의 스냅숏 tooits 원래 상태)입니다.
- hello SAP HANA hello 저장소 스냅숏에 포함 된 스냅숏이 실행 되 고 hello 저장소 스냅숏을 만든 후 저장 된 로그 백업 적용에 대 한 오프셋된 지점입니다.
- 이러한 로그 백업 하는 toorestore hello 데이터베이스 백 tooa 특정 지정 시간입니다.

지정 하 여 hello 백업\_이름 hello 다음 볼륨의 스냅숏을 만듭니다.

- hana/data
- hana/log
- hana/log\_backup(hana/log에 백업으로 탑재됨)
- hana/shared

### <a name="storage-snapshot-considerations"></a>저장소 스냅숏 고려 사항

>[!NOTE]
>추가 저장소 공간이 할당되어야 하기 때문에 저장소 스냅숏은 무료로 제공되지 _않습니다_.

저장소에 대 한 스냅숏 (대형 인스턴스) Azure에서 SAP HANA hello 특정 메커니즘은 다음과 같습니다.

- (시점 hello에서 제외 될 때) 특정 저장소 스냅숏 매우 작은 저장소를 사용 합니다.
- 데이터 변경 내용이 및 SAP HANA 데이터 hello 저장소 볼륨에서 파일 변경의 hello 콘텐츠에 hello 스냅숏 toostore hello 원래 블록 콘텐츠가 필요 합니다.
- hello 저장소 스냅숏 크기가 늘어납니다. hello 긴 hello 스냅숏이 있는, hello 큰 hello 저장소 스냅숏 됩니다.
- 더 많은 변경 내용을 toohello SAP HANA 데이터베이스 볼륨의 저장소 스냅숏 hello 수명 주기 동안 hello, hello 저장소 스냅숏의 hello 큰 hello 공간 소비 됩니다.

(대형 인스턴스) Azure에서 SAP HANA hello SAP HANA 데이터 및 로그 볼륨에 대 한 고정된 볼륨 크기 함께 제공 됩니다. 이러한 볼륨의 스냅숏을 수행를 볼륨 공간으로 무시 (내에서 SAP HANA [큰 인스턴스] Azure 프로세스에 hello)는 책임 tooschedule storage 스냅숏이 되기 때문입니다.

hello 다음 섹션에서는 제공 일반적인 권장 사항을 비롯 한 이러한 스냅숏을 수행 하기 위한 정보:

- Hello 하드웨어 볼륨당 255 스냅숏을 유지할 수 있습니다, 경우에이 번호 보다 유지 하는 것이 좋습니다.
- 스냅숏 저장소를 수행하기 전에 여유 공간을 모니터링하고 추적합니다.
- 사용 가능한 공간에 따라 저장소 스냅숏 낮은 hello 수. 를 유지 하는 스냅숏 toolower hello 수 하거나 tooextend hello 볼륨을 할 수 있습니다. (추가 저장소를 1TB 단위로 주문할 수 있습니다.)
- 시스템 마이그레이션 도구(R3load 또는 백업에서 SAP HANA 데이터베이스 복원)를 사용하여 SAP HANA에 데이터를 이동하는 것과 같은 작업 중에 저장소 스냅숏을 수행하지 않는 것이 좋습니다. (시스템 마이그레이션 새 SAP HANA 시스템에서 수행 중인 경우 저장소 스냅숏을 필요 하지 toobe 수행 합니다.)
- SAP HANA 테이블을 크게 재구성하는 동안 저장소 스냅숏을 가능하면 사용하지 않아야 합니다.
- 저장소 스냅숏은 (대형 인스턴스) Azure에서 SAP HANA의 필수 구성 요소 tooengaging hello 재해 복구 기능입니다.

### <a name="setting-up-storage-snapshots"></a>저장소 스냅숏 설정

1. Perl hello HANA (대형 인스턴스) 서버의 hello Linux 운영 체제에 설치 되어 있는지 확인 합니다.
2. 수정/등/ssh/ssh\_config tooadd hello 줄 _Mac hmac sha1_합니다.
3. SAP HANA 인스턴스마다 (있는 경우)를 실행 하는 hello 마스터 노드에서 SAP HANA backup 사용자 계정을 만듭니다.
4. SAP HANA HDB 클라이언트 hello 모든 SAP HANA (대형 인스턴스) 서버에 설치 되어야 합니다.
5. Hello 첫 번째 SAP HANA (대형 인스턴스) 서버에서 각 영역의 공개 키 tooaccess hello 스냅숏 생성을 제어 하는 저장소 인프라를 기본 생성 되어야 합니다.
6. Azure hello 스크립트 복사\_hana\_의 /scripts toohello 위치에서 backup.pl **hdbsql** 의 hello SAP HANA 설치 합니다.
7. 동일한 /scripts toohello에서 복사 hello HANABackupDetails.txt 파일 Perl 스크립트 hello 위치입니다.
8. Hello 적절 한 고객 사양에 대 한 필요에 따라 hello HANABackupDetails.txt 파일을 수정 합니다.

### <a name="step-1-install-sap-hana-hdbclient"></a>1단계: SAP HANA HDBClient 설치

hello (대형 인스턴스) Azure에서 SAP HANA에 설치 된 Linux hello 폴더를 포함 및 백업 및 재해 복구를 위해 필요한 tooexecute SAP HANA storage 스냅숏의 스크립팅 합니다. 그러나 SAP HANA를 설치 하는 동안 프로그램 책임 tooinstall SAP HANA HDBclient 됩니다. (Microsoft hello HDBclient 아니고 SAP HANA 설치합니다.)

### <a name="step-2-change-etcsshsshconfig"></a>2단계: /etc/ssh/ssh\_config 변경

여기에 표시된 _MACs hmac-sha1_ 줄을 추가하여 /etc/ssh/ssh\_config를 변경합니다.
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>3단계: 공개 키 만들기

Hello에 각 Azure 지역에서 Azure (대형 인스턴스) 서버에서 첫 번째 SAP HANA 스냅샷을 만들 수 있도록 사용 되는 공개 키 toobe tooaccess hello 저장소 인프라를 만듭니다. hello 공개 키 암호 toohello 저장소에 필요한 toosign를 하면 암호 자격 증명이 유지 되지 않습니다. Hello SAP HANA (대형 인스턴스) 서버에 Linux에서 다음 명령을 toogenerate hello에 대 한 공개 키 hello를 실행 합니다.
```
  ssh-keygen –t dsa –b 1024
```
hello 새 위치는 _/root/.ssh/id\_dsa.pub 합니다. 실제 암호를 입력 하지 마십시오. 그렇지 않으면 됩니다 필요 tooenter hello 암호에 로그인 할 때마다 합니다. 을 여러 번 **Enter** tooremove hello 두 번 입력 로그인에 대 한 암호 요구 사항입니다.

Toomake 고쳐지도록 해당 hello 공개 키가 too/root/.ssh/ 폴더를 변경 하 고 hello 다음 실행 하 여 예상 대로 확인 **ls** 명령입니다. Hello 키가 있는 경우에 hello 다음 명령을 실행 하 여 복사할 수 있습니다.

![이 명령을 실행하여 공개 키를 복사합니다.](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

이 시점에서 Azure 서비스 관리에서 SAP HANA에 게 문의 하 고 hello 키를 제공 합니다. hello 서비스 담당자에 게 사용 하 여 hello 공개 키 tooregister hello 저장소 인프라를 내부에 있습니다.

### <a name="step-4-create-an-sap-hana-user-account"></a>4단계: SAP HANA 사용자 계정 만들기

백업을 목적으로 SAP HANA Studio 내에서 SAP HANA 사용자 계정을 만듭니다. 이 계정에는 hello 다음 권한이 있어야 합니다.: _백업 관리자_ 및 _카탈로그 읽기_합니다. 이 예제에서는 hello username SCADMIN 만들어집니다.

![HANA Studio에서 사용자 만들기](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>5 단계: hello SAP HANA 사용자 계정에 권한을 부여합니다

Hello SAP HANA 사용자 계정 (toobe hello 스크립트를 실행할 때마다 권한 부여를 요구 하지 않고 hello 스크립트에서 사용)에 권한을 부여 합니다. SAP HANA 명령 hello `hdbuserstore` hello 하나 이상의 SAP HANA 노드에 저장 되는 SAP HANA 사용자 키를 만들기를 허용 합니다. hello 사용자 키 hello 스크립팅 나중에 설명 하는 프로세스 내에서 toomanage 암호 필요 없이 hello 사용자 tooaccess를 SAP HANA를 수도 있습니다.

>[!IMPORTANT]
>실행 hello 다음으로 명령을 `_root_`합니다. 그렇지 않으면 hello 스크립트는 제대로 작동 수 없습니다.

Hello 입력 `hdbuserstore` 명령은 다음과 같습니다.

![Hello hdbuserstore 명령을 입력 합니다.](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

다음 예에서는 여기서 hello 사용자 SCADMIN01 이며 hello 호스트 이름이 lhanad01 hello hello 명령은 다음과 같습니다.
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
확장 HANA 인스턴스의 단일 서버에서 모든 스크립트를 관리합니다. 이 예에서 각 호스트는 키 관련된 toohello hello 호스트를 반영 하는 방식에 대해 SCADMIN01 hello SAP HANA 키를 변경 해야 합니다. Hello HANA DB의 hello 인스턴스 번호를 사용 하 여 hello SAP HANA 백업 계정이 수정 하는, 즉 **lhanad**합니다. hello 키 할당 된 hello 호스트에서 관리자 권한이 있어야 하 고 hello 확장에 대 한 백업 사용자 액세스 권한 tooall SAP HANA 인스턴스가 있어야 합니다.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>6 단계: hello /scripts 폴더에서 항목 복사

복사 hello 다음 hello에서 항목 을/폴더 (hello 설치의 hello 골드 이미지에 포함 됨) toohello 작업 디렉터리에 대 한 스크립트 **hdbsql**합니다. 현재 HANA 설치의 경우 이 디렉터리는 /hana/shared/D01/exe/linuxx86\_64/hdb입니다.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
OLAP 또는 hello 확장 실행 하는 경우 다음 항목을 복사 합니다.
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
hello HANABackupCustomerDetails.txt 파일이 확장 배포에 대 한 다음과 같이 수정할 수 있습니다. Hello storage 스냅숏을 실행 하는 hello 스크립트에 대 한 hello 컨트롤 및 구성 파일입니다. 받았을 것 hello _저장소 백업 이름_ 및 _저장소 IP 주소_ 인스턴스에 배포 된 경우 Azure 서비스 관리에서 SAP HANA에서 합니다. 순서 지정 hello 시퀀스 수정할 수 없습니다 또는 hello 변수나 hello 스크립트의 모든 간격 제대로 실행 되지 않습니다.

확장 배포에 대 한 hello 구성 파일은 같습니다.
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
확장 구성에 대 한 hello HANABackupCustomerDetailsBW.txt 파일은 같습니다.
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>현재 노드 1 세부 정보만 hello 실제 HANA 저장소 스냅숏 스크립트에 사용 됩니다. 즉, hello 마스터 백업 노드로 변경 되는 경우 이미 확인 했는 다른 노드 대신할 수의 노드 1 hello 세부 정보를 수정 하 여 모든 HANA 노드에서 액세스 tooor를 테스트 하는 것이 좋습니다.

toocheck hello 구성 파일 또는 적절 한 연결 toohello HANA 인스턴스에 hello 올바른 구성에 대 한 hello 스크립트를 다음 중 하나를 실행 합니다.
- 강화 구성의 경우(SAP 워크로드에 독립적임):

 ```
testHANAConnection.pl
```
- 확장 구성의 경우:

 ```
testHANAConnectionBW.pl
```

해당 hello 마스터 HANA 인스턴스에 액세스 필요한 tooall HANA 서버를 확인 합니다. 매개 변수 toohello 스크립트가 없습니다 있지만 끝내십시오 적절 한 HANABackupCustomerDetails hello / HANABackupCustomerDetailsBW 제대로 스크립트 toorun hello에 대 한 파일입니다. 만 hello 셸 명령 오류 코드 반환 되므로 수 없으면 hello 스크립트 tooerror 검사 모든 인스턴스에 대 한 합니다. 그럼에도 hello 스크립트는 몇 가지 유용한 설명이 있습니다 toodouble 확인을 위해 제공.

toorun hello 스크립트:
```
 ./testHANAConnection.pl
```
 Hello 스크립트 hello hello HANA 인스턴스 상태를 얻고 성공적으로 hello HANA 연결 성공 했다는 메시지가 표시 됩니다.

또한 된 형식이 두 번째 스크립트의 toocheck hello 마스터 HANA 인스턴스 서버 기능 toosign toohello 저장소에서 사용할 수 있습니다. Hello azure를 실행 하기 전에\_hana\_백업 (\_bw).pl 스크립트 hello 다음 스크립트를 실행 해야 합니다. 볼륨 스냅숏이 없습니다 있으면가 불가능 한 toodetermine hello 볼륨 단순히 비어 있거나는 ssh 오류 tooobtain hello 스냅숏 정보입니다. 이러한 이유로 hello 스크립트는 두 단계를 실행합니다.

- 해당 hello 저장소 콘솔은 액세스할 수를 확인 합니다.
- HANA 인스턴스에서 각 볼륨의 테스트, 더미 또는 스냅숏을 만듭니다.

이러한 이유로 hello HANA 인스턴스에 대 한 인수로 포함 됩니다. 다시, 가능한 tooprovide 오류 hello 저장소 연결에 대 한 검사는 없지만 hello 스크립트 hello 실행이 실패 하면 유용한 힌트를 제공 합니다.

hello 스크립트는으로 실행 됩니다.
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
또는 다음의 경우 실행됩니다.
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
hello 스크립트에는 적절 하 게 배포 tooyour 저장소 테 넌 트에서 주위 hello 논리 단위 번호 (Lun)을 소유 하는 hello 서버 인스턴스에서 사용 되는 구성 된 수 toosign 있는 없다는 메시지가 표시 됩니다.

첫 번째 저장소 스냅숏 기반 백업을 hello를 실행 하기 전에 hello 다음 스크립트 toomake 해당 hello 구성이 올바른지를 실행 합니다.

이러한 스크립트를 실행 한 후 실행 하 여 hello 스냅숏을 삭제할 수 있습니다.
```
./removeTestStorageSnapshot.pl <hana instance>
```
또는
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>7단계: 주문형 스냅숏 수행

여기에서 설명한 대로 주문형 스냅숏을 수행할 뿐만 아니라 cron를 사용하여 일반 스냅숏을 예약합니다.

확장 구성에 대 한 hello 다음 스크립트를 실행 합니다.
```
./azure_hana_backup.pl lhanad01 customer 20
```
확장 구성에 대 한 hello 다음 스크립트를 실행 합니다.
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
hello 확장 스크립트는 몇 가지 추가 검사 toomake 시키고 모든 HANA 서버에 액세스할 수 있는 모든 HANA 인스턴스 SAP HANA 또는 저장소 스냅숏 만들기를 계속 하기 전에 hello 인스턴스의 적절 한 상태를 반환 합니다.

다음 인수 hello 요소가 필요 합니다.

- hello HANA 인스턴스 필요한 백업입니다.
- hello hello 저장소 스냅숏에 대 한 스냅숏 접두사입니다.
- 스냅숏 toobe hello 특정 접두사에 대 한 보관 hello 수입니다.

```
./azure_hana_backup.pl lhanad01 customer 20
```

hello 스크립트 실행의 hello 이러한 세 가지 단계로 hello 저장소 스냅숏을 만듭니다.

- HANA 스냅숏을 실행합니다.
- 저장소 스냅숏을 실행합니다.
- Hello HANA 스냅숏을 제거 합니다.

에 복사 했던 hello HDB 실행 폴더에서 호출 하 여 hello 스크립트를 실행 합니다. 그 다음 볼륨을 백업 이상 hello 하지만 또한 안녕하세요 명시적 SAP HANA 인스턴스 이름을 hello 볼륨 이름에 있는 모든 볼륨을 백업 합니다.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
(예: 20, 앞에 나온) hello 스크립트를 실행할 때 매개 변수로 제출 스냅숏의 hello 번호로, hello 보존 기간 관리 엄격 하 게 됩니다. 따라서 hello 기간 실행 및 hello hello 스크립트의 hello 호출에는 스냅숏 수의 hello 기간의 함수입니다. Hello 유지 되는 스냅숏의 개수 hello 스크립트의 hello 호출에서 매개 변수로 명명 된 hello 수를 초과 하면 가장 오래 된 저장소 스냅숏이이 레이블의 hello (이전 여기서에서 _사용자 지정_)는 새 스냅숏이 전에 삭제 실행 됩니다. 즉, hello 번호 hello hello 호출의 마지막 매개 변수는 hello 번호 toocontrol hello 스냅숏 수를 사용할 수 있습니다 하는 대로 제공 합니다.

>[!NOTE]
>Hello 레이블을 변경 하는 즉시 다시 시작 hello 계산 됩니다.

제공 하는 Azure 서비스 관리에서 SAP HANA를 인수로 multi-node 환경에서 스냅숏을 만들고 있는 경우 tooinclude hello HANA 인스턴스 이름이 필요 합니다. 단일 노드 환경에서 Azure (대형 인스턴스) 단위에 SAP HANA hello의 hello 이름 만으로는 있지만 hello HANA 인스턴스 이름을 것이 좋습니다.

또한 있습니다 수를 사용 하 여 부팅 volumes\LUNs 백업 hello 동일 스크립트입니다. 처음 HANA를 실행하는 경우 한 번 이상 부팅 볼륨을 백업해야 합니다. 하지만 cron의 부팅에 대해 주간 또는 야간 백업 일정을 사용하는 것이 좋습니다. SAP HANA 인스턴스 이름을 추가, 보다 삽입 하는 대신 _부팅_ hello 스크립트에 인수를 다음과 같이 hello 대로:
```
./azure_hana_backup boot customer 20
```
hello 동일한 보존 정책을 제공 되어 toohello 부팅 볼륨도 합니다. 설명 된 대로 특수 한 경우에만에 이전에 같은 SAP 향상 된 기능, 패키지 (EHP)으로 업그레이드 하는 동안 하거나 toocreate 고유 저장소 스냅숏을 해야 할 때 주문형으로 스냅숏을 사용 합니다.

Cron를 사용 하 여 예약 된 tooperform 저장소 스냅샷 좋습니다 하 고 모든 백업 및 재해 복구 요구 사항 (수정 하 고 hello 스크립트 입력 toomatch hello 백업 시간을 요청한 다양 한)에 동일한 스크립트 hello를 사용 하는 것이 좋습니다. 해당 실행 시간(매시간, 12시간, 매일 또는 매주)에 따라 cron에서 모두 다르게 예약됩니다. hello cron 일정은 위에 설명 된 hello 장기 오프 사이트 백업에 대 한 보존 레이블 지정과 일치 하는 디자인 된 toocreate 저장소 스냅숏입니다. hello 명령 tooback (데이터 및 로그 파일이 백업 시간별, hello 부팅 볼륨은 매일 백업 하는 반면)가 요청 된 빈도 따라 모든 프로덕션 볼륨을 포함 합니다.

hello 항목 hello cron 스크립트 다음에 실행 매시간 hello에 10 분, 10 분 단위 hello 및 hello 10 분 단위에서 매일 12 시간 간격입니다. hello cron 작업 하는 방식에 만들어집니다. 해당 하나만 SAP HANA 저장소 스냅숏을 수행 특정 시간에 하므로 hello 시간 및 일별 백업에서 발생 하지 않는 hello 동일한 시간 (오전 12시 10분). 스냅숏 만들기 및 복제 toohelp 최적화, Azure 서비스 관리에서 SAP HANA hello 권장 toorun 있습니다에 대 한 시간 백업을 제공 합니다.

hello 기본 cron /etc/crontab의 일정은 다음과 같습니다.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
이전 cron 지침 hello (하지 않고 부팅 볼륨) hello HANA 볼륨 hello 레이블로 스냅숏 시간별을 가져옵니다. 이러한 66개의 스냅숏이 유지됩니다. 또한 hello 12 시간 레이블이 있는 14 스냅숏은 보존 됩니다. 잠재적으로 3일 간의 매시간 스냅숏에 추가로 4일 간의 12시간 스냅숏을 얻게 되어 한 주 간의 스냅숏을 제공합니다.

Cron 내에서 예약 hello 스크립트는 몇 분 정도 만큼 지연 표시 하지 않는 한 특정 시간에 하나의 스크립트를 실행 해야 하기 때문에 작업은 복잡할 수 있습니다. 장기 보존에 대 한 매일 백업 하려는 경우 (수와 함께 보존 각 7), 12 시간 스냅숏과 함께 일일 스냅숏은 유지 됩니다 또는 hello 시간별 스냅숏 10 분 후 시차를 두고 진행된 tootake 위치입니다. 하나의 일일 스냅숏은 hello 프로덕션 볼륨에 보관 됩니다.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
여기에 나열 된 hello 주파수는 예일 뿐입니다. tooderive 최적의 수가 스냅숏, 다음 기준을 사용 하 여 hello:

- 지정 시간 복구에 대한 복구 시간 목표의 요구 사항
- 공간 사용
- 잠재적 재해 복구를 위한 복구 지점 목표 및 복구 시간 목표의 요구 사항
- 디스크에 대한 HANA 전체 데이터베이스 백업의 최종 실행 디스크에 대해 전체 데이터베이스 백업 될 때마다 또는 _backint_ 인터페이스를 수행 storage 스냅숏 hello 실행이 실패 합니다. Storage 스냅숏 기반으로 tooexecute 전체 데이터베이스 백업 하려는 경우 저장소 스냅숏 hello 실행이이 시간 동안 사용할 수 없다는 있는지 확인 합니다.

>[!IMPORTANT]
> SAP HANA 백업에 대 한 스냅숏 저장소 hello 사용 hello 스냅숏을 SAP HANA 로그 백업과 함께에서 수행 될 때만 유효 합니다. 이러한 로그 백업 필요 toobe 수 toocover hello hello 저장소 스냅숏 간의 기간 합니다. 30 일의 지정 시간 복구가 약정 toousers를 설정한 경우 hello 다음이 필요 합니다.

- 기능 tooaccess 저장소 스냅숏 30 일입니다.
- Hello 지난 30 일 이내를 통해 연속 로그 백업입니다.

로그 백업의 범위 hello도 hello 백업 로그 볼륨의 스냅숏을 만듭니다. 그러나 수 있는지 tooperform 수 있도록를 정기적인 로그 백업:

- Hello 연속 로그 백업은 지정 시간 복구 tooperform 필요 합니다.
- Hello SAP HANA 로그 볼륨의 공간이 부족에서 방지 합니다.

Hello 마지막 단계 중 하나에서 SAP HANA Studio tooschedule SAP HANA 백업 로그입니다. hello SAP HANA 백업 로그 대상 위치는 특별히 만든 hello hana/로그\_/hana/log/backups hello 탑재 지점은으로 볼륨을 백업 합니다.

![SAP HANA Studio에서 SAP HANA 백업 로그 예약](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

15분보다 더 자주 수행된 백업을 선택할 수 있습니다. 일부 사용자도 1분마다 로그 백업을 수행할 수 있지만 15분 _이상_은 권장하지 않습니다.

hello 최종 단계 tooperform 파일 기반 백업 (이후 hello SAP HANA의 초기 설치) toocreate hello 백업 카탈로그 내에 있어야 하는 단일 백업 항목입니다. 그렇지 않으면 SAP HANA는 지정된 로그 백업을 시작할 수 없습니다.

![파일 기반 백업 toocreate 단일 백업 항목 만들기](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Hello 디스크 볼륨의 스냅숏의 hello 수와 크기를 모니터링합니다.

특정 저장소 볼륨을 스냅숏 및 스냅숏 hello 저장소 소비 hello 수를 모니터링할 수 있습니다. hello `ls` 명령 hello 스냅숏 디렉터리 또는 파일은 표시 되지 않습니다. 그러나 Linux 운영 체제 명령 hello `du` 명령 뒤 hello로 않습니다:

- `du –sh .snapshot`hello 스냅숏 디렉터리 내에서 모든 스냅숏의 합계를 제공 합니다.
- `du –sh --max-depth=1`각 스냅숏의 hello 크기 및 hello.snapshot 폴더에 저장 된 모든 스냅숏을 나열 합니다.
- `du –hc`모든 스냅숏에 사용 되는 hello 전체 크기를 제공 합니다.

이러한 명령을 toomake 수행 되 고 저장 하는 hello 스냅숏 hello 볼륨에서 모든 hello 저장소를 사용 하지는 있는지를 사용 합니다.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>서버에서의 스냅숏 hello 수 줄이기

이전에 설명한 대로 hello의 스냅숏 저장 하는 특정 레이블 수를 줄일 수 있습니다. hello tooretain hello 명령 tooinitiate 스냅숏으로 레이블과 hello 원하는 스냅숏 개수는 두 개의 매개 변수를 지속 합니다.
```
./azure_hana_backup.pl lhanad01 customer 20
```
이전 예에서 hello hello 스냅숏 레이블은 _고객_ 이며이 레이블 toobe 유지를 사용 하 여 스냅숏의 hello 수 _20_합니다. Toodisk 공간 소비를 응답 tooreduce hello 수의 저장 된 스냅숏이 필요할 수 있습니다. hello 쉽게 스냅숏 tooreduce hello 번호는 마지막 매개 변수 집합 too5 hello 사용 하 여 toorun hello 스크립트:
```
./azure_hana_backup.pl lhanad01 customer 5
```
스냅숏, 스냅숏, hello 새 저장소를 포함 하 여 hello 수는이 설정 사용 하 여 hello 스크립트 실행의 결과로 _5_합니다.

 >[!NOTE]
 > 이 스크립트는 hello 가장 최근의 이전 스냅숏 시간 넘은 경우에 hello 스냅숏 수를 줄입니다. hello 스크립트 보다 작거나 1 시간 전의 스냅숏은 삭제 되지 않습니다.

이러한 제한 사항은 관련된 toohello 선택적 재해 복구 기능을 제공 합니다.

하지 않기로 toomaintain의 해당 접두사로 스냅숏 집합을 사용 하 여 hello 스크립트를 실행할 수 없습니다 _0_ hello 보존 번호 tooremove 해당 접두사와 일치 하는 모든 스냅숏으로 합니다. 그러나 모든 스냅숏 제거 재해 복구의 hello 기능 발생할 수 있습니다.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>가장 최근의 HANA 스냅숏으로 toohello 복구

Hello 이벤트에서 프로덕션 다운 시나리오, 저장소 스냅숏에서 복구 과정 hello 발생할 있습니다 시작할 수 있습니다 Azure 서비스 관리에서 SAP HANA 인 고객 인시던트에으로. 이러한 예기치 않은 시나리오는 프로덕션 시스템 및 hello 유일한 방법은 tooretrieve hello 데이터는 toorestore hello 프로덕션 데이터베이스에서 데이터가 삭제 하는 긴급도 높은 것 될 수 있습니다.

Hello에 반면, 지정 시간 복구 낮은 긴급도 될 수 및 일에 대 한 계획입니다. 우선 순위 문제를 발생시키는 대신 Azure의 SAP HANA Service Management를 사용하여 이 복구를 계획할 수 있습니다. 예를 들어 있습니다 수 수립 tootry hello SAP 소프트웨어를 업그레이드 하는 새 향상 패키지 하 고 적용 하 여 다음 toorevert hello EHP 업그레이드 하기 전에 hello 상태를 나타내는 tooa 스냅숏을 백업 해야 합니다.

Hello 요청을 실행 하기 전에 몇 가지 준비 toodo 할 수 있습니다. Azure 서비스 관리 팀에 SAP HANA 다음를 처리 하 여 hello 요청 복원 hello 볼륨입니다. 나중에 hello 스냅숏을 기반으로 하는 tooyou toorestore hello HANA 데이터베이스를 됩니다. 다음은 tooprepare hello에 대 한 요청 방법:

>[!NOTE]
>사용자 인터페이스 스크린샷 SAP HANA 릴리스를 사용 하는 hello에 따라 다음 hello에서 달라질 수 있습니다.

1. 스냅숏 toorestore를 결정 합니다. 라는 메시지가 표시 되 고, 그렇지 않으면만 hello hana/데이터 볼륨을 복원 되지 않습니다.

2. Hello HANA 인스턴스를 종료 합니다.

 ![Hello HANA 인스턴스 종료](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. 각 HANA 데이터베이스 노드에 hello 데이터 볼륨을 분리 하십시오. hello 스냅숏의 hello 복원 hello 데이터 볼륨 탑재 되지 않은 경우 실패 합니다.

 ![각 HANA 데이터베이스 노드에 hello 데이터 볼륨을 분리 합니다.](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. 특정 스냅숏의 Azure 지원 요청 tooinstruct hello 복원을 엽니다.

 - Hello 복원 하는 동안: Azure 서비스 관리에서 SAP HANA tooattend 데이터가 없는 어떠한 손실도 하는 전화 회의 tooensure 요청할 수 있습니다.

 - Hello 복원 후: Azure 서비스 관리에서 SAP HANA 알리는 hello 저장소 스냅숏이 복원 된 경우.

5. Hello 복원 프로세스가 완료 되 면 모든 데이터 볼륨을 다시 탑재 합니다.

 ![모든 데이터 볼륨 다시 탑재](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. 수행 하지 자동으로 만들 수 있기 때문 tooHANA DB SAP HANA Studio를 통해 다시 연결 하면 SAP HANA Studio 내에서 복구 옵션을 선택 합니다. hello 다음 예제에서는 복원 toohello 마지막 HANA 스냅숏 저장소 스냅숏 HANA 스냅숏 하나 포함 되 고 toohello 가장 최근의 저장소 스냅숏으로 복원 하는 가장 최근의 HANA 스냅숏으로 hello 상태 여야 합니다. (Toolocate tooolder storage 스냅숏을 복원 하는 경우 필요한 hello HANA hello 시간 hello 저장소 스냅숏을 기반 스냅숏을.)

 ![SAP HANA Studio 내에서 복구 옵션 선택](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. 선택 **복구 hello 데이터베이스 tooa 특정 데이터 백업이 나 저장소 스냅숏을**합니다.

 ![hello "복구 유형 선택" 창](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. **카탈로그 없이 백업 지정**을 선택합니다.

 ![hello "백업 위치 지정" 창](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. Hello에 **대상 형식** 목록에서 **스냅숏**합니다.

 ![hello "지정 hello 백업 tooRecover" 창](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. 클릭 **마침** toostart hello 복구 프로세스입니다.

 ![Toostart hello 복구 프로세스 "마침"을 클릭 합니다.](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. hello HANA 데이터베이스 복원 되 고 toohello HANA 스냅숏 hello 저장소 스냅숏에 포함 된 복구.

 ![HANA 데이터베이스를 복원 하 고 복구 된 toohello HANA 스냅숏](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Toohello 가장 최근 상태 복구

hello 다음 프로세스 복원 hello 저장소 스냅숏에 포함 된 hello HANA 스냅숏 합니다. 그런 다음 hello 저장소 스냅숏을 복원 하기 전에 hello 트랜잭션 로그 백업을 toohello의 가장 최근 상태 hello 데이터베이스를 복원 합니다.

>[!IMPORTANT]
>계속 진행하기 전에 트랜잭션 로그 백업의 완전한 연속 체인이 있는지 확인합니다. 이러한 백업 없이 hello hello 데이터베이스의 현재 상태를 복원할 수 없습니다.

1. Hello 앞에 "Recovering toohello 가장 최근의 HANA 스냅숏입니다." 절차의 1-6 단계를 완료 합니다.

2. 선택 **hello 데이터베이스 tooits 가장 최근 상태를 복구**합니다.

 !["Hello 데이터베이스 tooits 가장 최근 상태를 복구"를 선택 합니다.](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Hello 가장 최근의 HANA 로그 백업의 hello 위치를 지정 합니다. hello 위치는 toocontain hello HANA 스냅숏 toohello 가장 최근 상태에서 HANA 트랜잭션 로그 백업을 모두 필요합니다.

 ![Hello 가장 최근의 HANA 로그 백업의 hello 위치 지정](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. 백업을 toorecover hello 데이터베이스에서 기본으로 선택 합니다. 예제에서는이 속성은 hello 저장소 스냅숏에 포함 된 hello HANA 스냅숏입니다. (하나만 스냅숏 hello 스크린 샷 뒤에 나열 됩니다.)

 ![백업 toorecover hello 데이터베이스에서 기본으로 선택](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. 지우기 hello **델타 백업을 사용** 확인란 hello HANA 스냅숏의 hello 시간과 hello 가장 최근 상태 간의 델타를 존재 하지 않는 경우.

 ![지우기 hello "델타 백업을 사용" 확인란 없는 델타가 존재 하는 경우](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Hello 요약 화면에서 클릭 **마침** toostart hello 복원 절차입니다.

 ![Hello 요약 화면에서 "마침"을 클릭](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>복구 중 tooanother 지정 시간
toorecover tooa 지정 hello HANA 스냅숏 (hello 저장소 스냅숏에 포함) 사이의 다른 하나는 hello HANA 스냅숏 지정 시간 복구 보다 이후 시간에 따라 hello지 않습니다.

1. Hello HANA 스냅숏 toohello 시간 toorecover 원하는에서 트랜잭션 로그 백업을 모두 있는지 확인 합니다.
2. "Recovering toohello 최신 상태입니다." hello 절차를 시작 합니다.
3. Hello에 hello 절차의 2 단계에서 **복구 유형 선택** 창에서 **지정 시간 복구 hello 데이터베이스 toohello 다음**hello 지정 시간을 지정 하 고 3-6 단계를 완료 합니다.

## <a name="monitoring-hello-execution-of-snapshots"></a>스냅숏 hello 실행 모니터링

스냅숏 저장소 toomonitor hello 실행을 해야합니다. 저장소 스냅숏으로 실행 하는 hello 스크립트 출력 tooa 파일에 쓰고 toohello 저장 hello Perl 스크립트와 같은 위치입니다. 각 스냅숏에 대해 별도 파일을 기록합니다. 각 파일의 hello 출력이 hello 스냅숏 스크립트를 실행 하는 다양 한 단계로 hello를 명확 하 게 표시 됩니다.

- 찾기 toocreate를 필요로 하는 hello 볼륨 스냅숏
- 이러한 볼륨에서 생성 된 hello 스냅숏 찾기
- 최종 기존 스냅숏을 toomatch hello 스냅숏 개수 지정한 삭제
- HANA 스냅숏 만들기
- Hello 볼륨 hello 저장소 스냅숏 만들기
- Hello HANA 스냅샷 삭제
- 가장 최근의 hello 너무 스냅숏 이름 바꾸기**.0**

hello 스크립트의 가장 중요 한 부분 hello은 다음과 같습니다.
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
어떻게 hello 스크립트 레코드 hello hello HANA 스냅숏 만든이이 샘플에서 볼 수 있습니다. Hello 확장의 경우에서이 프로세스는 hello 마스터 노드에서 시작 됩니다. hello 마스터 노드는 각 hello 작업자 노드에서 hello 스냅숏 hello 동기 만들기를 시작합니다. Hello 저장소 스냅숏을 이동 합니다. Hello 저장소 스냅숏 hello 성공적으로 실행 후 hello HANA 스냅숏이 삭제 됩니다.
