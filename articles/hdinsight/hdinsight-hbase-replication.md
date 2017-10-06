---
title: "가상 네트워크-Azure 내에서 HBase 클러스터 복제 aaaConfigure | Microsoft Docs"
description: "자세한 내용은 어떻게 부하 분산, 고가용성, 0-가동 중지 시간 마이그레이션/업데이트에서 하나의 HDInsight 버전 tooanother 및 재해 복구에 대 한 tooconfigure HBase 복제 합니다."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>가상 네트워크 내에서 HBase 클러스터 복제 구성

자세한 방법을 하나의 가상 네트워크 (VNet) 내에서 또는 두 개의 가상 네트워크 간에 tooconfigure HBase 복제 합니다.

클러스터 복제에서는 원본-푸시 방법을 사용합니다. HBase 클러스터는 원본 또는 대상이 될 수도 있고, 한 번에 두 가지 역할을 모두 수행할 수도 있습니다. 복제는 비동기적 이며 및 hello 복제 ´ ֲ 결과적 일관성. Hello 소스 편집 tooa 열 제품군 사용 하도록 설정 하는 복제를 받을 때 편집은 전파 tooall 대상 클러스터입니다. 하나의 클러스터 tooanother에서 데이터가 복제 되므로 hello 원본 클러스터와 hello 데이터 이미 있는 모든 클러스터 추적된 tooprevent 복제 루프 됩니다.

이 자습서에서는 원본-대상 복제를 구성합니다. 다른 클러스터 토폴로지는 [Apache HBase 참조 가이드](http://hbase.apache.org/book.html#_cluster_replication)를 참조하세요.

단일 가상 네트워크에 대한 HBase 복제 사용 사례:

* 부하 분산-예를 들어 검색 또는 MapReduce 작업 hello 대상 클러스터에서 실행 중 이며 hello 원본 클러스터에서 데이터를 수집 하는 방법
* 고가용성
* 하나의 HBase 클러스터 tooanother에서 데이터 마이그레이션
* 한 버전 tooanother에서 Azure HDInsight 클러스터를 업그레이드합니다.

두 가상 네트워크에 대한 HBase 복제 사용 사례:

* 재해 복구
* 부하 분산 및 분할 hello 응용 프로그램
* 고가용성

[GitHub](https://github.com/Azure/hbase-utils/tree/master/replication)에 있는 [스크립트 동작](hdinsight-hadoop-customize-cluster-linux.md) 스크립트를 사용하여 클러스터를 복제합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

## <a name="configure-hello-environments"></a>Hello 환경 구성

다음과 같이 세 가지 가능한 구성이 있습니다.

- 1개 Azure 가상 네트워크에 2개 HBase 클러스터 구성
- 서로 다른 두 개의 가상 네트워크에 두 개의 HBase 클러스터 hello 동일한 지역
- 별도의 2개 지역에 있는 2개 다른 가상 네트워크에 2개 HBase 클러스터 구성(지리적 복제)

toomake 것 보다 쉽게 tooconfigure hello 환경에서 만든 일부 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-overview.md)합니다. 다른 방법을 사용 하 여 tooconfigure hello 환경을 선호 하는 경우 참조:

- [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)
- [Azure Virtual Network에 HBase 클러스터 만들기](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>1개 가상 네트워크 구성

Hello 다음 hello에 이미지 toocreate 두 HBase 클러스터를 클릭 합니다. 동일한 가상 네트워크입니다. hello 서식 파일에 저장 된 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/)합니다.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Hello에 두 개의 가상 네트워크를 구성 합니다. 동일한 지역

다음 이미지 toocreate 두 가상 네트워크 VNet 피어 링 및 두 개의 HBase 클러스터 hello에서 사용 하 여 hello를 클릭 합니다. 동일한 지역입니다. hello 서식 파일에 저장 된 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/)합니다.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



이 시나리오에는 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)이 필요하며, hello 템플릿 VNet 피어 링 수 있습니다.   

HBase 복제 hello 사육 Vm의 IP 주소를 사용합니다. Hello 대상 HBase 사육 노드에 대 한 고정 IP 주소를 구성 해야 합니다.

**tooconfigure 고정 IP 주소**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **리소스 그룹**합니다.
3. Hello 대상 HBase 클러스터를 포함 하 여 리소스 그룹을 클릭 합니다. 리소스 관리자 템플릿 toocreate hello 환경 hello를 사용 하는 때를 지정 하는 hello 리소스 그룹입니다. Hello 목록 아래로 hello 필터 toonarrow를 사용할 수 있습니다. Hello 두 가상 네트워크를 포함 하는 리소스의 목록을 볼 수 있습니다.
4. Hello 대상 HBase 클러스터를 포함 하는 hello 가상 네트워크를 클릭 합니다. 예를 들어 **xxxx-vnet2**를 클릭합니다. **nic-zookeepermode-**로 시작하는 이름을 가진 세 개의 장치를 볼 수 있습니다. 이러한 장치는 hello 3 사육 Vm입니다.
5. Hello 사육 Vm 중 하나를 클릭 합니다.
6. **IP 구성**을 클릭합니다.
7. 클릭 **ipConfig1** hello 목록에서 합니다.
8. 클릭 **정적**, hello 실제 IP 주소를 적어 둡니다. Hello 스크립트 동작 tooenable 복제를 실행할 때 hello IP 주소가 필요 합니다.

  ![HDInsight HBase 복제 ZooKeeper 고정 IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. 다른 두 사육 노드 hello에 대 한 단계 6 tooset hello 고정 IP 주소를 반복 합니다.

Hello VNet 간 시나리오에 대 한 hello를 사용 해야 **ip** hello를 호출할 때 전환 **hdi_enable_replication.sh** 작업을 스크립팅 합니다.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>별도의 2개 지역에 2개 가상 네트워크 구성

다음 이미지 toocreate 두 가상 네트워크에 두 개의 서로 다른 지역 hello를 클릭 합니다. hello 템플릿은 공용 Azure Blob 컨테이너에 저장 됩니다.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Hello 두 가상 네트워크 간의 VPN 게이트웨이 만듭니다. 지침은 [사이트 간 연결로 VNet 만들기](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)를 참조하세요.

HBase 복제 hello 사육 Vm의 IP 주소를 사용합니다. Hello 대상 HBase 사육 노드에 대 한 고정 IP 주소를 구성 해야 합니다. tooconfigure 고정 IP이 문서의 hello "에서 구성 두 가상 네트워크는 동일한 지역 hello" 섹션을 참조 하세요.

Hello VNet 간 시나리오에 대 한 hello를 사용 해야 **ip** hello를 호출할 때 전환 **hdi_enable_replication.sh** 작업을 스크립팅 합니다.

## <a name="load-test-data"></a>테스트 데이터 로드

클러스터를 복제 하면 테이블 tooreplicate hello를 지정 해야 합니다. 이 섹션에서는 hello 원본 클러스터로 일부 데이터를 로드 합니다. 다음 섹션인 hello hello 두 클러스터 간 복제를 설정 합니다.

Hello 지침에 따라 [HBase 자습서: HDInsight에서 Linux 기반 Hadoop으로 HBase Apache를 사용 하 여 시작](hdinsight-hbase-tutorial-get-started-linux.md) toocreate는 **연락처** 테이블 및 일부 데이터 hello 테이블에 삽입 합니다.

## <a name="enable-replication"></a>복제 활성화

단계를 수행 하는 hello toocall hello Azure 포털에서에서 스크립트 동작 스크립트 hello 하는 방법을 보여 줍니다. Azure PowerShell을 hello Azure CLI (명령줄 인터페이스)를 사용 하 여 스크립트 작업을 실행 하는 것에 대 한 참조 [스크립트 동작을 사용 하 여 사용자 지정 하는 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-customize-cluster-linux.md)합니다.

**hello Azure 포털에서에서 tooenable HBase 복제**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 원본 HBase 클러스터를 엽니다.
3. Hello 클러스터 메뉴에서 클릭 **스크립트 동작**합니다.
4. 클릭 **새 제출** hello hello 블레이드 맨 위에서 합니다.
5. 선택 하거나 hello 다음 정보를 입력 합니다.

  - **이름**: **복제 사용**을 입력합니다.
  - **Bash 스크립트 URL**: **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**를 입력합니다.
  - **헤드**: 선택합니다. 다른 노드 형식 hello 선택을 취소 합니다.
  - **매개 변수**: hello 다음 hello 원본 클러스터 toohello 대상 클러스터에서 모든 hello 데이터를 복사 및 매개 변수 hello 기존의 모든 테이블에 대 한 복제를 사용 하는 샘플:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. **만들기**를 클릭합니다. hello 스크립트에는 다소 시간이 걸릴 수 hello-copydata 인수를 사용 하는 경우에 특히 합니다.

필수 인수:

|이름|설명|
|----|-----------|
|-s, --src-cluster | Hello hello 원본 HBase 클러스터 DNS 이름을 지정 합니다. 예: -s hbsrccluster, --src-cluster=hbsrccluster |
|-d, --dst-cluster | Hello hello 대상 (복제본) HBase 클러스터 DNS 이름을 지정 합니다. 예: -s dsthbcluster, --src-cluster=dsthbcluster |
|-sp, --src-ambari-password | Hello 소스 HBase 클러스터에서 Ambari에 대 한 hello 관리자 암호를 지정 합니다. |
|-dp, --dst-ambari-password | Ambari에 대 한 hello 대상 HBase 클러스터에 hello 관리자 암호를 지정 합니다.|

선택적 인수:

|이름|설명|
|----|-----------|
|-su, --src-ambari-user | Ambari에 대 한 hello 원본 HBase 클러스터에 hello 관리자 권한을 가진 사용자를 지정 합니다. hello 기본값은 **admin**합니다. |
|-du, --dst-ambari-user | Ambari에 대 한 hello 대상 HBase 클러스터에 hello 관리자 권한을 가진 사용자를 지정 합니다. hello 기본값은 **admin**합니다. |
|-t, --table-list | Hello 테이블 toobe 복제를 지정 합니다. 예: --table-list="table1;table2;table3". 테이블을 지정하지 않으면 기존의 모든 HBase 테이블을 복제합니다.|
|-m, --machine | Hello 헤드 노드 hello 스크립트 동작 실행 될 위치를 지정 합니다. hello 값은 hn1 또는 hn0 합니다. 대개 hn0이 더 바쁘기 때문에 hn1을 사용하는 것이 좋습니다. Hello HDInsight 포털 또는 Azure PowerShell에서 스크립트 동작으로 hello $0 스크립트를 실행 하는 경우이 옵션을 사용 합니다.|
|-ip | 이 인수는 두 개의 가상 네트워크 간에 복제를 사용할 때 필요하며, 이 인수는 스위치 toouse hello 정적 Ip의 사육 노드 클러스터를 복제본 클러스터 FQDN 이름 대신 역할을 합니다. hello 정적 Ip toobe 복제를 활성화 하기 전에 미리 구성 해야 합니다. |
|-cp, -copydata | 복제를 사용 하는 hello 테이블에서 기존 데이터의 hello 마이그레이션을 사용 하도록 설정 합니다. |
|-rpm, -replicate-phoenix-meta | Phoenix 시스템 테이블에서 복제를 사용하도록 설정합니다. <br><br>*이 옵션은 주의해서 사용해야 합니다.* 이 스크립트를 사용하기 전에 복제본 클러스터에서 Phoenix 테이블을 다시 만드는 것이 좋습니다. |
|-h, --help | 사용 정보를 표시합니다. |

hello print_usage() 섹션 hello [스크립트](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) 매개 변수를 자세히 설명 합니다.

Hello 스크립트 작업을 성공적으로 후 배포 SSH tooconnect toohello 대상 HBase 클러스터를 사용 하 여 있고 hello 데이터 복제 되었는지 확인 합니다.

### <a name="replication-scenarios"></a>복제 시나리오

hello 다음 목록을 보면 몇 가지 일반 사용 사례 및 해당 매개 변수 설정:

- **Hello 두 클러스터 간의 모든 테이블에서 복제 사용**합니다. 이 시나리오 hello 복사/hello 테이블에서 기존 데이터의 마이그레이션에 필요 하지 및 피닉스 테이블을 사용 하지 않습니다. 매개 변수 뒤 hello를 사용 합니다.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **특정 테이블에서 복제를 사용하도록 설정** - Hello 매개 변수 tooenable 복제 table1, table2 및 표 3에서 다음을 사용 합니다.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **특정 테이블에서 복제를 사용 하도록 설정 하 고 hello 기존 데이터를 복사**합니다. Hello 매개 변수 tooenable 복제 table1, table2 및 표 3에서 다음을 사용 합니다.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **소스 toodestination에서 피닉스 메타 데이터를 복제 된 모든 테이블에서 복제 사용**합니다. Phoenix 메타데이터 복제는 완벽하지 않으므로 주의해서 사용해야 합니다.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>데이터 복사 및 마이그레이션

복제를 사용하도록 설정한 후에 데이터를 복사/마이그레이션하기 위한 두 개의 스크립트 동작 스크립트가 별도로 있습니다.

- [작은 테이블에 대 한 스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (몇 기가바이트 크기 및 전반적인 복사본에서 1 시간 안에 예상된 toofinish를가 하는 데 사용)

- [대형 테이블에 대 한 스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (1 시간 toocopy 보다 긴 tootake 예상)

따를 수 있습니다에 같은 프로시저 hello [복제 사용](#enable-replication) toocall hello 스크립트 동작 매개 변수 뒤 hello로:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

hello print_usage() 섹션 hello [스크립트](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) 매개 변수에 대 한 자세한 설명을 제공 합니다.

### <a name="scenarios"></a>시나리오

- **지금(현재 타임스탬프)까지 편집된 모든 행에 대한 특정 테이블(test1, test2 및 test3) 복사**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  또는

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **지정된 시간 범위의 특정 테이블 복사**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>복제 사용 안 함

에 있는 다른 스크립트 동작 스크립트 사용 toodisable 복제 [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)합니다. 따를 수 있습니다에 같은 프로시저 hello [복제 사용](#enable-replication) toocall hello 스크립트 동작 매개 변수 뒤 hello로:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

hello print_usage() 섹션 hello [스크립트](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) 매개 변수를 자세히 설명 합니다.

### <a name="scenarios"></a>시나리오

- **모든 테이블에서 복제를 사용하지 않도록 설정**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  또는

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **지정된 테이블(table1, table2 및 table3)에서 복제를 사용하지 않도록 설정**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>다음 단계

이 자습서에서는 방법에 대해 배웠습니다 두 데이터 센터에서 tooconfigure HBase 복제 합니다. toolearn 더 및에 대 한 HDInsight HBase를 참조 하세요.

* [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]
* [HDInsight HBase 개요][hdinsight-hbase-overview]
* [Azure Virtual Network에 HBase 클러스터 만들기][hdinsight-hbase-provision-vnet]
* [HBase를 사용하여 Twitter 데이터 실시간 분석][hdinsight-hbase-twitter-sentiment]
* [HDInsight(Hadoop)에서 Apache Storm 및 HBase를 사용하여 센서 데이터 분석][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
