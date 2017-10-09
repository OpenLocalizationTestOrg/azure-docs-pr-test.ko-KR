---
title: "Azure에서 클러스터 aaaRun MariaDB (MySQL) | Microsoft Docs"
description: "Azure 가상 컴퓨터에 MariaDB + Galera MySQL 클러스터를 만듭니다."
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>MariaDB(MySQL) 클러스터: Azure 자습서
> [!IMPORTANT]
> Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 대부분의 새로운 배포 hello Azure 리소스 관리자 모델을 사용 하는 것이 좋습니다.

> [!NOTE]
> 이제 MariaDB Enterprise 클러스터 hello Azure Marketplace에서에서 제공 됩니다. hello 새 제공 MariaDB Galera 클러스터에서 Azure 리소스 관리자를 자동으로 배포 됩니다. 새 제공 hello를 사용 해야 [Azure 마켓플레이스](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/)합니다.
>
>

이 문서에서는 다중 마스터 toocreate [Galera](http://galeracluster.com/products/) 의 클러스터 [MariaDBs](https://mariadb.org/en/about/) (MySQL에 대 한 대체 하는 강력 하 고 확장 가능한 신뢰할 수 있는 방법) toowork Azure에서 항상 사용 가능한 환경에서 가상 컴퓨터입니다.

## <a name="architecture-overview"></a>아키텍처 개요
이 문서에서는 다음 toocomplete hello 단계 방법을 설명 합니다.

- 3개 노드 클러스터를 만듭니다.
- Hello OS 디스크에서 데이터 디스크를 별도 hello입니다.
- RAID 0/스트라이프 설정 tooincrease IOPS에에서 hello 데이터 디스크를 만듭니다.
- Hello 3 노드에 대 한 Azure 부하 분산 장치 toobalance hello 부하를 사용 합니다.
- 반복적인 toominimize 작동 MariaDB + Galera를 포함 하는 VM 이미지를 만들고 사용 하 여 toocreate hello 다른 클러스터 Vm입니다.

![시스템 아키텍처](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> 이 항목에서는 hello [Azure CLI](../../../cli-install-nodejs.md) 도구, 만들어지므로 toodownload 있는지를 확인 하 toohello 지침에 따라 tooyour Azure 구독에 연결 합니다. Hello Azure CLI에서에서 사용할 수 있는 참조 toohello 명령 필요한 경우 참조 hello [Azure CLI 명령 참조](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다. 너무 필요 합니다[인증을 위해 SSH 키를 만들려면] hello.pem 파일 위치 메모 합니다.
>
>

## <a name="create-hello-template"></a>Hello 템플릿 만들기
### <a name="infrastructure"></a>인프라
1. 선호도 그룹 toohold hello 리소스를 함께 만듭니다.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. 가상 네트워크를 만듭니다.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. 저장소 계정 toohost 우리의 모든 디스크를 만듭니다. Hello에 40 개 이상의 많이 사용 되는 디스크를 추가 하지 않아야 하면 동일한 저장소 계정 tooavoid hello 20, 000 IOPS 저장소 계정 제한에 도달 합니다. 이 경우 하 한도 보다 상당히 있으므로 hello 단순성에 동일한 계정에서 모든 항목이 저장 됩니다.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. CentOS 7 hello 가상 컴퓨터 이미지의 hello 이름을 찾습니다.

        azure vm image list | findstr CentOS
   다음과 같이 hello 출력 됩니다 `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`합니다.

   Hello 단계 다음에 해당 이름을 사용 합니다.
5. Hello VM 템플릿을 만들고 /path/to/key.pem 생성 hello.pem SSH 키를 저장 하는 hello 경로로 바꿉니다.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. 4 개의 500GB 데이터 디스크 toohello VM hello RAID 구성에서 사용 하기 위해 연결 합니다.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. SSH toosign toohello 템플릿에서 mariadbhatemplate.cloudapp.net:22 때 만든 VM 사용 하 고 사용자의 개인 키를 사용 하 여 연결 합니다.

### <a name="software"></a>소프트웨어
1. Hello 루트를 가져옵니다.

        sudo su

2. RAID 지원을 설치합니다.

    a. mdadm을 설치합니다.

              yum install mdadm

    b. EXT4 파일 시스템으로 hello RAID0/stripe 구성을 만듭니다.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Hello 탑재 지점 디렉터리를 만듭니다.

              mkdir /mnt/data
    d. Hello hello 새로 만든 RAID 장치의 UUID를 검색 합니다.

              blkid | grep /dev/md0
    e. /etc/fstab을 편집합니다.

              vi /etc/fstab
    f. 다시 시작할 때 hello UUID hello 값으로 대체 탑재 hello 장치 tooenable 자동 이전 hello에서 가져온 추가 **blkid** 명령입니다.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. 새 파티션을 hello 탑재 합니다.

              mount /mnt/data

3. MariaDB를 설치합니다.

    a. Hello MariaDB.repo 파일을 만듭니다.

                vi /etc/yum.repos.d/MariaDB.repo

    b. 콘텐츠를 다음 hello로 hello 리포지토리 파일을 채웁니다.

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid 충돌 기존 후 위 및 mariadb 라이브러리를 제거 합니다.

           yum remove postfix mariadb-libs-*
    d. Galera와 함께 MariaDB를 설치합니다.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Hello MySQL 데이터 디렉터리 toohello RAID 블록 장치를 이동 합니다.

    a. 새 위치에 hello 현재 MySQL 디렉터리를 복사 하 고 hello 이전 디렉터리를 제거 합니다.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Hello 새 디렉터리에 대 한 사용 권한을 적절 하 게 설정 합니다.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Hello 이전 디렉터리 toohello 새 위치에 hello RAID 파티션 가리키는 기호화 된 링크를 만듭니다.

           ln -s /mnt/data/mysql /var/lib/mysql

5. 때문에 [SELinux hello 클러스터 작동을 방해](http://galeracluster.com/documentation-webpages/configuration.html#selinux), 필요한 toodisable는 hello 현재 세션에 대 한 것입니다. 편집 `/etc/selinux/config` toodisable 후속 다시 시작에 대 한 것입니다.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. MySQL 실행의 유효성을 검사합니다.

   a. MySQL을 시작합니다.

           service mysql start
   b. MySQL 설치 hello를 보호, hello 루트 암호를 설정, 익명 사용자에 게 toodisable 원격 루트 로그인을 제거 및 hello 테스트 데이터베이스를 제거 합니다.

           mysql_secure_installation
   c. 클러스터 작업에 대 한 및 필요에 따라 응용 프로그램에 대 한 hello 데이터베이스에 대 한 사용자를 만듭니다.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. MySQL을 중지합니다.

            service mysql stop
7. 구성 자리 표시자를 만듭니다.

   a. Hello MySQL 구성 toocreate hello 클러스터 설정에 대 한 자리 표시자를 편집 합니다. Hello를 대체 하지 않고  **`<Variables>`**  또는 지금 주석 처리를 제거 합니다. 이 템플릿에서 VM을 만든 후에 그렇게 됩니다.

            vi /etc/my.cnf.d/server.cnf
   b. Hello 편집  **[galera]**  섹션 및 확인란의 선택을 취소 합니다.

   c. Hello 편집 **[mariadb]** 섹션.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. CentOS 7 FirewallD를 사용 하 여 hello 방화벽에 필요한 포트를 엽니다.

   * MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * 다시 로드 hello 방화벽:`firewall-cmd --reload`

9. Hello 시스템 성능을 최적화 합니다. 자세한 내용은 [성능 조정 전략](optimize-mysql.md)을 참조하세요.

   a. 다시 hello 된 MySQL 구성 파일을 편집 합니다.

            vi /etc/my.cnf.d/server.cnf
   b. Hello 편집 **[mariadb]** 섹션 및 hello 다음 콘텐츠를 추가 합니다.

   > [!NOTE]
   > innodb\_buffer\_pool_size를 VM 메모리의 70%로 설정하는 것이 좋습니다. 이 예제에서는 그가 설정 된 2.45 GB hello 중간의 RAM이 3.5 g B를 사용 하 여 Azure VM에 대 한 합니다.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. MySQL을 중지, 시작 tooavoid hello 클러스터 노드를 추가 하는 경우 중단에서 실행 되지 않도록 MySQL 서비스를 사용 하지 않도록 설정 하 고 hello 컴퓨터를 프로 비전 해제.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Hello 포털을 통해 VM hello를 캡처하십시오. (현재 [hello Azure CLI 도구에서 #1268 발급](https://github.com/Azure/azure-xplat-cli/issues/1268) hello Azure CLI 도구에서 캡처한 이미지 hello 연결 된 데이터 디스크를 캡처하지 않으면 hello 팩트에 설명 합니다.)

    a. Hello 포털을 통해 hello 컴퓨터를 종료 합니다.

    b. 클릭 **캡처** hello 이미지 이름으로 지정 하 고 **mariadb galera 이미지**합니다. 설명을 입력하고 "waagent를 실행했습니다." 확인란을 선택합니다.
      
      ![Hello 가상 컴퓨터 캡처](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Hello 클러스터 만들기
사용자를 만든 다음 구성 하 고 hello 클러스터를 시작 하는 hello 템플릿을 사용 하 여 세 개의 Vm을 만듭니다.

1. Hello mariadb galera 이미지에서 첫 번째 CentOS 7 VM 이미지를 만든 hello 다음 정보를 제공 하는 hello를 만듭니다.

 - 가상 네트워크 이름: mariadbvnet
 - 서브넷: mariadb
 - 컴퓨터 크기: medium
 - 클라우드 서비스 이름: mariadbha (또는 원하는 이름 원하는 toobe mariadbha.cloudapp.net를 통해 액세스)
 - 컴퓨터 이름: mariadb1
 - 사용자 이름: azureuser
 - SSH 액세스: enabled
 - Hello SSH 인증서.pem 파일을 전달 하 고 /path/to/key.pem 생성 hello.pem SSH 키를 저장 하는 hello 경로로 대체 합니다.

   > [!NOTE]
   > hello 다음 명령을 분할 명확성을 위해 여러 줄에 있지만 각각 한 줄으로 입력 해야 합니다.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Toohello mariadbha 클라우드 서비스를 연결 하 여 두 개 더 많은 가상 컴퓨터를 만듭니다. Hello VM 이름 변경 및 SSH 포트 tooa 고유한 포트의 다른 Vm와 충돌 하지 hello hello 동일한 클라우드 서비스입니다.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  MariaDB3의 경우:

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. Hello 다음 단계에 대 한 hello 3 개의 Vm 각각의 tooget hello 내부 IP 주소에 필요 합니다.

    ![IP 주소 가져오기](./media/mariadb-mysql-cluster/IP.png)
4. SSH toosign toohello 세 Vm에서 사용 하 고는 각각에 대해 hello 구성 파일을 편집 합니다.

        sudo vi /etc/my.cnf.d/server.cnf

    주석 처리 제거  **`wsrep_cluster_name`**  및  **`wsrep_cluster_address`**  hello를 제거 하 여  **#**  hello 줄의 hello 시작 합니다.
    또한 대체  **`<ServerIP>`**  에  **`wsrep_node_address`**  및  **`<NodeName>`**  에  **`wsrep_node_name`**  hello로 VM의 IP 주소 및 이름을 각각 지정 하 고도 해당 줄의 주석 처리 제거 합니다.
5. MariaDB1에 hello 클러스터를 시작 하 고 시작 시 실행 되기를 기다립니다.

        sudo service mysql bootstrap
        chkconfig mysql on
6. MariaDB2 및 MariaDB3에서 MySQL을 시작하고 시작 시 실행되도록 합니다.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>부하 분산 hello 클러스터
클러스터 된 hello Vm을 만들 때 추가한 clusteravset tooensure 이러한 서로 다른 장애 도메인과 업데이트 도메인에 추가 된 하 고 있는지 Azure 되지 않는 모든 컴퓨터에서 유지 관리 한 번에 호출 하는 가용성 집합에 있습니다. 이 구성은 hello Azure 서비스 수준 계약 (SLA)에서 지 원하는 toobe hello 요구 사항을 충족 합니다.

이제 Azure 부하 분산 장치 toobalance 요청 hello 3 개 노드 사이 사용 합니다.

Hello hello Azure CLI를 사용 하 여 명령을 컴퓨터에 다음을 실행 합니다.

hello 명령 매개 변수 구조는 같습니다.`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

hello CLI hello 부하 분산 장치 프로브 간격 too15 초 약간 너무 오래 될 수 있는 설정 합니다. Hello 포털에서 변경 **끝점** hello Vm 중 하나에 대 한 합니다.

![끝점 편집](./media/mariadb-mysql-cluster/Endpoint.PNG)

선택 **Load-Balanced 설정 Reconfigure hello**합니다.

![다시 구성 hello 부하 분산 된 집합](./media/mariadb-mysql-cluster/Endpoint2.PNG)

변경 **프로브 간격** too5 시간 (초) 하 고 변경 내용을 저장 합니다.

![프로브 간격 변경](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Hello 클러스터 유효성 검사
hello 복잡 한 작업이 수행 됩니다. hello 클러스터에서 액세스할 수 이제 해야 `mariadbha.cloudapp.net:3306`hello 부하 분산 장치를 적중 하는, 및 원활 하 고 효율적으로 사이의 경로 요청 hello 세 개의 Vm입니다.

즐겨 찾는 MySQL 클라이언트 tooconnect 사용 하거나이 클러스터가 작동 하는 hello Vm tooverify 중 하나에서 연결 합니다.

     mysql -u cluster -h mariadbha.cloudapp.net -p

그런 다음 데이터베이스를 만들고 일부 데이터로 채웁니다.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

hello 데이터베이스를 만든 다음 표에 hello를 반환 합니다.

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
이 문서에서는 CentOS 7을 실행하는 Azure 가상 컴퓨터에 3개 노드 MariaDB + Galera 고가용성 클러스터를 만들었습니다. hello Vm Azure 부하 분산 장치와 부하가 분산 됩니다.

toolook 할 수 있습니다 [또 다른 방법은 toocluster Linux에서 MySQL](mysql-cluster.md) 방법 너무[최적화 하 고 Azure Linux Vm에서 MySQL 성능 테스트](optimize-mysql.md)합니다.

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[인증을 위해 SSH 키를 만들려면]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
