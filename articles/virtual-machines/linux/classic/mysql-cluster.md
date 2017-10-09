---
title: "부하 분산 된 집합으로 MySQL aaaClusterize | Microsoft Docs"
description: "Azure의 hello 클래식 배포 모델을 사용 하 여 Linux MySQL 클러스터 만든 부하 분산, 높은 가용성을 설정 합니다."
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>부하 분산 집합 tooclusterize MySQL을 사용 하 여 Linux에서
> [!IMPORTANT]
> Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. A [리소스 관리자 템플릿](https://azure.microsoft.com/documentation/templates/mysql-replication/) toodeploy MySQL 클러스터 해야 할 경우에 사용할 수 있습니다.

이 문서를 탐색 하 고 hello 두 가지 방법을 사용할 수 있는 toodeploy 항상 사용 가능한 Linux 기반 Microsoft Azure에서 서비스, 탐색을 입문서로 MySQL Server의 고가용성을 보여 줍니다. 이 접근 방법을 보여 주는 비디오는 [채널 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)(영문)에서 사용할 수 있습니다.

여기서는 DRBD, Corosync 및 Pacemaker에 기반한 비공유 2개 노드 단일 마스터 MySQL 고가용성 솔루션을 개괄적으로 설명합니다. 한 번에 하나의 노드만 MySQL을 실행합니다. Hello DRBD 리소스에서에서 읽기와 쓰기 이기도 제한 tooonly 한 노드에서 한 번에 합니다.

Microsoft Azure tooprovide 라운드 로빈 기능과 끝점 검색, 제거 및 hello VIP의 적절 한 복구에 대 한 부하 분산 집합을 사용 하 여 때문에 같은 LVS, VIP 솔루션에 대 한 않아도가 됩니다. hello VIP는 hello 클라우드 서비스를 처음 만들 때 Microsoft Azure에 의해 할당 되는 전역적으로 라우팅 가능 IPv4 주소입니다.

MySQL(NBD Cluster, Percona 및 Galera 포함) 및 여러 개의 미들웨어 솔루션([VM Depot](http://vmdepot.msopentech.com)에서 VM으로 사용할 수 있는 하나 이상의 솔루션 포함)에 가능한 다른 아키텍처가 있습니다. 이러한 솔루션 유니캐스트 및 멀티 캐스트 또는 브로드캐스트에 복제할 수 있고 공유 저장소 또는 여러 개의 네트워크 인터페이스에 의존 하지 않습니다, hello 시나리오에는 Microsoft Azure에서 쉽게 toodeploy 이어야 합니다.

Tooother 제품 PostgreSQL OpenLDAP 유사한 방식으로 확장할 수 있습니다 이러한 아키텍처를 클러스터링. 예를 들어 공유되지 않은 이러한 부하 분산 절차는 다중 마스터 OpenLDAP를 사용하여 성공적으로 테스트되었으며, 채널 9 블로그에서 볼 수 있습니다.

## <a name="get-ready"></a>준비
Hello 다음 필요한 리소스 및 기능:

  - 두 개 이상의 Vm 수 toocreate 유효한 구독을 사용 하면 Microsoft Azure 계정 (XS이이 예제에서 사용 되었습니다.)
  - 네트워크 및 서브넷
  - 선호도 그룹
  - 가용성 집합
  - 기능 toocreate Vhd hello hello 클라우드 서비스와 동일한 지역 hello와 toohello Linux Vm에 연결

### <a name="tested-environment"></a>테스트된 환경
* Ubuntu 13.10
  * DRBD
  * MySQL Server
  * Corosync 및 Pacemaker

### <a name="affinity-group"></a>선호도 그룹
Toohello Azure 클래식 포털에에서 로그인 하 여 hello 솔루션에 대 한 선호도 그룹 만들기를 선택 하 **설정을**, 및 선호도 그룹 만들기. 나중에 만들어진 할당 된 리소스 toothis 선호도 그룹에 할당 됩니다.

### <a name="networks"></a>네트워크
새 네트워크를 만들고 서브넷 hello 네트워크 내부에 만들어집니다. 이 예제에서는 내부에 /24 서브넷 하나만 있는 10.10.10.0/24 네트워크를 사용합니다.

### <a name="virtual-machines"></a>가상 컴퓨터
첫 번째 Ubuntu 13.10 VM Endorsed Ubuntu 갤러리 이미지를 사용 하 여 만들어지고 라고 hello `hadb01`합니다. 새 클라우드 서비스는 hadb 라고 하는 hello 프로세스에서 생성 됩니다. 이 이름은 hello를, 이전에 공유 리소스를 더 추가 되 면 hello 서비스 있는 부하 분산 된 특성을 보여 줍니다. 만들기 hello `hadb01` hello 포털을 사용 하 여 정상적인 시간 및 완료 된 됩니다. SSH에 대 한 끝점은 자동으로 만들어지고 hello 새 네트워크를 선택 합니다. 이제 가용성 집합 hello Vm 만들 수 있습니다.

만듭니다 (기술적으로 hello 클라우드 서비스를 만드는 경우) 첫 번째 VM이 생성 하는 hello, 후 두 번째 VM hello `hadb02`합니다. Hello에 대 한 VM의 두 번째, hello 포털을 사용 하 여 hello 갤러리에서에서 Ubuntu 13.10 VM을 사용 하지만 기존 클라우드 서비스를 사용 하 여 `hadb.cloudapp.net`, 새로 만드는 대신 합니다. hello 네트워크 및 가용성 집합을 자동으로 선택 해야 합니다. SSH 끝점도 만들어집니다.

두 Vm을 만든 후 기록해 hello SSH 포트가 `hadb01` (TCP 22) 및 `hadb02` (자동으로 할당 된 Azure에서).

### <a name="attached-storage"></a>연결된 저장소
새 디스크 tooboth Vm 꽂고 hello 프로세스에 5GB 디스크를 만듭니다. hello 디스크는 주 운영 체제 디스크에 대 한 사용 hello VHD 컨테이너에 호스트 됩니다. 디스크를 만들고 연결 된 후 없습니다 필요 toorestart Linux 되므로 hello 커널 hello 새 장치에 표시 됩니다. 이 장치는 대개 `/dev/sdc`입니다. 확인 `dmesg` hello 출력에 대 한 합니다.

각 VM에서 사용 하 여 파티션을 만들려면 `cfdisk` (Linux, 주 파티션) hello 새 파티션 테이블을 작성 합니다. 이 파티션에는 파일 시스템을 만들면 안 됩니다.

## <a name="set-up-hello-cluster"></a>Hello 클러스터 설정
APT tooinstall Corosync, Pacemaker, 및 DRBD 두 Ubuntu Vm에서 사용 합니다. toodo 사용 `apt-get`실행 hello 다음 코드:

    sudo apt-get install corosync pacemaker drbd8-utils.

지금 MySQL을 설치하면 안 됩니다. Debian 및 Ubuntu 설치 스크립트에 MySQL 데이터 디렉터리를 초기화 합니다 `/var/lib/mysql`, 하지만 나중에 MySQL tooinstall hello 디렉터리는 DRBD 파일 시스템에 의해 교체 됩니다, 때문에 필요 합니다.

확인 (사용 하 여 `/sbin/ifconfig`) 두 Vm hello 10.10.10.0/24 서브넷의 주소 및 이러한 ping 수 있는지 다른 이름으로 사용 하는 합니다. 사용할 수도 있습니다 `ssh-keygen` 및 `ssh-copy-id` toomake 두 Vm 암호를 요구 하지 않고 SSH를 통해 통신할 수 있는지 합니다.

### <a name="set-up-drbd"></a>DRBD 설치
기본 hello를 사용 하 여 DRBD 리소스 만들기 `/dev/sdc1` tooproduce 파티션는 `/dev/drbd1` ext3를 사용 하 여 포맷 하 고 기본 및 보조 노드에서 사용할 수 있는 리소스입니다.

1. 열기 `/etc/drbd.d/r0.res` 복사 hello 두 Vm에서 리소스 정의 따라:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Hello 리소스를 사용 하 여 초기화 `drbdadm` 두 Vm에서:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. 주 VM hello (`hadb01`)를 강제로 hello DRBD 리소스의 소유권이 (주 서버):

        sudo drbdadm primary --force r0

/ Proc/drbd의 hello 내용을 검사 하는 경우 (`sudo cat /proc/drbd`) 두 Vm에서 표시 되어야 `Primary/Secondary` 에 `hadb01` 및 `Secondary/Primary` 에 `hadb02`hello 솔루션과 시점에서 일관 된 합니다. hello 5GB 디스크에 없는 충전 toocustomers hello 10.10.10.0/24 네트워크를 통해 동기화 됩니다.

Hello 디스크 동기화 된 후에 hello 파일 시스템을 만들 수 있습니다 `hadb01`합니다. 테스트를 위해 e x t 2를 사용 하지만 코드 다음 hello ext3 파일 시스템 만들어집니다.

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Hello DRBD 리소스 탑재
이제 준비 toomount hello DRBD 리소스에는 `hadb01`합니다. Debian 및 파생 배포판은 `/var/lib/mysql` 을 MySQL 데이터 디렉터리로 사용합니다. MySQL를 설치 하지 않은 때문에 hello 디렉터리 만들고 hello DRBD 리소스 탑재 합니다. tooperform hello 코드 다음을 실행 하는이 옵션을 `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>MySQL 설치
이제 준비 tooinstall MySQL에서 `hadb01`:

    sudo apt-get install mysql-server

`hadb02`의 경우 두 가지 옵션이 있습니다. Mysql 서버 /var/lib/mysql, 새 데이터 디렉터리를 채울 만들고 다음 hello 콘텐츠를 제거를 설치할 수 있습니다. tooperform hello 코드 다음을 실행 하는이 옵션을 `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

hello 두 번째 방법은 toofailover 너무`hadb02` 다음 mysql 서버 있습니다를 설치 합니다. 설치 스크립트는 hello 기존 설치 및 것을 미치지 않습니다.

실행 hello 다음 코드에 `hadb01`:

    sudo drbdadm secondary –force r0

실행 hello 다음 코드에 `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Toofailover DRBD을 지금 않으려는 hello 첫 번째 옵션 이지만 다소 덜 세련 된 쉽습니다. 설정이 완료되면 MySQL 데이터베이스에 대해 작업을 시작할 수 있습니다. 실행 hello 다음 코드에 `hadb02` (또는 hello 서버 중 하나가 활성 상태 이면 tooDRBD에 따라):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> 이 마지막 문은이 테이블에 루트 사용자 hello에 대 한 인증을 효과적으로 해제합니다. 이 문은 프로덕션급 GRANT 문으로 바꾼 후 예시 용도로만 포함해야 합니다.

(즉,이 가이드의 목적은 hello) 외부 hello Vm에서 toomake 쿼리를 원하는 경우 MySQL에 대 한 네트워킹 tooenable를 해야 합니다. 두 Vm에서 엽니다 `/etc/mysql/my.cnf` 너무 이동`bind-address`합니다. Hello 주소 127.0.0.1에서 변경 too0.0.0.0 합니다. Hello 파일을 저장 후 실행 하는 `sudo service mysql restart` 현재 주입니다.

### <a name="create-hello-mysql-load-balanced-set"></a>Hello MySQL 부하 분산 된 집합 만들기
Toohello 포털 돌아가서, 너무 이동`hadb01`, 선택 **끝점**합니다. hello 드롭 다운 목록 및 선택에서 MySQL (TCP 3306)를 선택 하는 끝점, toocreate **만들기 새 부하 분산 집합**합니다. 이름 hello 부하 분산 끝점 `lb-mysql`합니다. 설정 **시간** 최소 too5 초입니다.

Hello 끝점을 만든 후 너무 이동`hadb02`, 선택 **끝점**, 한 끝점을 만듭니다. 선택 `lb-mysql`, MySQL hello 드롭 다운 목록에서 선택 합니다. 또한이 단계에 대 한 hello Azure CLI를 사용할 수 있습니다.

이제 hello 클러스터의 수동 작업을 위해 필요한 모든 항목이 만들어졌습니다.

### <a name="test-hello-load-balanced-set"></a>Hello 부하 분산 집합을 테스트 합니다.
MySQL 클라이언트를 사용하거나 Azure 웹 사이트로 실행되는 phpMyAdmin과 같은 특정 응용 프로그램을 사용하여 외부 컴퓨터에서 테스트를 수행할 수 있습니다. 이 경우 다른 Linux 상자에서 다음과 같은 MySQL의 명령줄 도구를 사용했습니다.

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>수동 장애 조치(Failover)
MySQL을 종료하고 DRBD의 기본 노드를 전환한 다음 MySQL을 다시 시작하여 장애 조치를 시뮬레이션할 수 있습니다.

tooperform hello hadb01에 코드를 다음을 실행 하는이 작업을 합니다.

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

그런 후 hadb02에서 다음을 실행합니다.

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

수동으로 장애 조치를 수행한 후에는 원격 쿼리를 반복할 수 있으며 완벽하게 작동합니다.

## <a name="set-up-corosync"></a>Corosync 설치
Corosync는 Pacemaker toowork에 필요한 hello 기반이 되는 클러스터 인프라입니다. 하트 비트 (및 Ultramonkey와 같은 기타 다른 방법) Corosync는 hello CRM 기능 분할 때 유사한 tooHeartbeat Pacemaker 기능입니다.

Azure에서 Corosync에 대 한 hello 기본적인 제약 Corosync 유니캐스트 통신 보다 브로드캐스트를 통해 멀티 캐스트를 선호 하지만 Microsoft Azure 네트워킹 유니캐스트 지원입니다.

다행히도 Corosync에는 작동 가능한 유니캐스트 모드가 있습니다. hello 유일한 제약 조건은 모든 노드가 서로 통신 하지 않습니다, 때문에 해당 IP 주소를 포함 하 여 구성 파일에서 toodefine hello 노드를 필요로 한다는입니다. 유니캐스트 및 변경 바인딩 주소, 노드 목록 및 로깅 디렉터리에 대 한 hello Corosync 예제 파일을 사용할 수 있습니다 (사용 하 여 Ubuntu `/var/log/corosync` hello 예제 파일에서 사용 하는 동안 `/var/log/cluster`), 쿼럼 도구를 사용 하도록 설정 합니다.

> [!NOTE]
> Hello 다음을 사용 하 여 `transport: udpu` 지시문과 hello 수동으로 두 노드 모두에 대 한 IP 주소를 정의 합니다.

실행 hello 다음 코드에 `/etc/corosync/corosync.conf` 노드 모두에 대해:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

두 VM에서 이 구성 파일을 복사하고 다음과 같이 두 노드에서 Corosync를 시작합니다.

    sudo service start corosync

Hello 서비스를 시작한 후에 곧 hello 클러스터 hello 현재 링에 반영할 수 및 쿼럼을 구성 해야 합니다. 이 기능은 코드 다음 hello를 실행 하거나 로그를 검토 하 여 확인할 수 있습니다.

    sudo corosync-quorumtool –l

다음 이미지는 출력 유사한 toohello를 표시 됩니다.

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Pacemaker 설치
Pacemaker 사용 하 여 리소스에 대 한 클러스터 toomonitor hello를 정의한 기본 아래로 이동 하는 경우 이러한 리소스 toosecondaries 전환 합니다. 리소스는 여러 방법이 있지만 사용 가능한 스크립트 집합이나 LSB(init-like) 스크립트에서 정의할 수 있습니다.

Pacemaker 너무 "직접" hello DRBD 리소스, hello 탑재 지점 및 hello MySQL 서비스 주시기 바랍니다. Pacemaker DRBD 켜거나 끌 수, 하는 경우 탑재 및 분리를 하 고으로 시작 및 중지 MySQL hello 순서 때 문제가 발생 하는 기본, hello로 설치가 완료 되 고 오른쪽 합니다.

Pacemaker를 처음 설치할 때는 구성이 다음과 같이 단순합니다.

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. 실행 하 여 hello 구성을 확인 `sudo crm configure show`합니다.
2. 파일을 만듭니다 (같은 `/tmp/cluster.conf`) 리소스 다음 hello로:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Hello 구성에 hello 파일을 로드 합니다. 하기만 하면 toodo이를 하나의 노드에 됩니다.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. 두 노드에서 부팅할 때 Pacemaker가 시작되는지 확인합니다.

        sudo update-rc.d pacemaker defaults

5. 사용 하 여 `sudo crm_mon –L`, hello 클러스터에 대 한 hello 마스터 바뀌었기 노드 중 하나 및 hello 리소스를 모두 실행 되 고 확인 합니다. 탑재 및 ps toocheck hello 리소스를 실행 하는 사용할 수 있습니다.

다음 스크린 샷에 표시 hello `crm_mon` 하나의 노드가 중지 (Ctrl + C를 선택 하 여 종료):

![crm_mon node stopped](./media/mysql-cluster/image002.png)

다음 스크린샷에서는 두 노드, 즉 하나의 마스터와 하나의 슬레이브를 보여 줍니다.

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>테스트
자동 장애 조치(Failover) 시뮬레이션을 위한 준비가 되었습니다. 두 가지 방법으로 toodo이: 소프트 및 하드 합니다.

hello 소프트 방식으로 함수 사용 하 여 hello 클러스터의 종료: ``crm_standby -U `uname -n` -v on``합니다. 이 사용 하 여 hello 마스터 hello 슬레이브 빠른 방법을 제공 합니다. 이 백 toooff tooset를 기억 합니다. 이렇게 하지 않으면 crm_mon에서 대기 중인 노드 하나를 표시합니다.

hello 복잡 한 과정을 종료 하 고 hello 다운 기본 VM (hadb01) hello 포털을 통해 또는 변경 하 여 hello hello (즉, 중지, 종료) VM에서 실행 수준입니다. 아래로 hello 마스터 하락 신호를 보내 Corosync 및 Pacemaker를 지원 합니다. 이 테스트할 수 있습니다 (유지 관리 기간에 유용) 하지만 VM hello 고정 하 여 hello 시나리오를 강제할 수도 있습니다.

## <a name="stonith"></a>STONITH
가능한 tooissue hello Azure CLI STONITH 스크립트는 물리적 장치를 제어 하는 대신이 대화 상자를 통해 VM 종료 이어야 합니다. 사용할 수 있습니다 `/usr/lib/stonith/plugins/external/ssh` 자료 및 STONITH hello 클러스터 구성에서 사용 합니다. Azure CLI 전역으로 설치 해야 하 고 hello 게시 설정 hello 클러스터의 사용자에 대 한 프로필을 로드 해야 합니다.

Hello 리소스에 대 한 예제 코드에서 사용할 수는 [GitHub](https://github.com/bureado/aztonith)합니다. Hello 너무 다음을 추가 하 여 hello 클러스터의 구성을 변경`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> hello 스크립트 위쪽/아래쪽 검사를 수행 하지 않습니다. hello 원래 SSH 리소스 15 ping 검사 있지만 Azure VM에 대 한 복구 시간에 더 많은 변수가 될 수 있습니다.

## <a name="limitations"></a>제한 사항
다음과 같은 제한을 hello에 적용 됩니다.

* linbit DRBD 리소스 스크립트의 Pacemaker 사용 리소스로 DRBD를 관리 하는 hello `drbdadm down` hello 노드 대기 것 이죠 하는 경우에 노드를 종료 합니다. 이 않으므로 이상적인 hello 슬레이브 됩니다 하지 수 hello DRBD 리소스 동안 동기화 hello 마스터 쓰기를 가져옵니다. Hello 마스터 정중 실패 하지 않는 경우 hello 슬레이브 오래 된 파일 시스템 상태가 대신할 수 있습니다. 이러한 문제를 해결할 수 있는 방법에는 다음 두 가지가 있습니다.
  * 로컬(클러스터화되지 않은) Watchdog을 통해 모든 클러스터 노드에서 `drbdadm up r0` 적용
  * Hello linbit DRBD 스크립트를 편집 하 고 있는지 확인 합니다 `down` 호출 하지 않습니다`/usr/lib/ocf/resource.d/linbit/drbd`
* hello 부하 분산 장치는 응용 프로그램 클러스터와 되어야 시간 제한의 보다 적절 하 게 되므로 적어도 5 초 toorespond가 필요 합니다. 앱 내 큐 및 쿼리 미들웨어와 같은 다른 아키텍처도 도움이 될 수 있습니다.
* MySQL 튜닝 필요한 tooensure 관리 가능한 속도로 작성이 수행 되며 캐시 플러시 toodisk를 가능한 toominimize 메모리 손실로 자주 됩니다.
* 쓰기 성능 VM에 따라 달라 집니다.이 속성은 DRBD tooreplicate hello 장치에서 사용 하는 hello 메커니즘 때문에 hello 가상 스위치에 상호 연결 합니다.
