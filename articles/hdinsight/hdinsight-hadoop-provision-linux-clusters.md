---
title: "Hadoop, Spark, Kafka, HBase, 또는 R 서버-Azure HDInsight에 대 한 aaaCluster 설치 | Microsoft Docs"
description: "브라우저, hello Azure CLI, Azure PowerShell, REST, 또는 SDK에서 HDInsight Hadoop, Kafka, Spark, HBase, R 서버 또는 Storm 클러스터를 설정 합니다."
keywords: "hadoop 클러스터 설정, kafka 클러스터 설정, spark 클러스터 설정, hadoop에서 클러스터란"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Hadoop, Spark, Kafka 등으로 HDInsight에서 클러스터를 설정

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

자세한 방법을 tooset 및 HDInsight Hadoop, Spark, Kafka, 대화형 하이브, HBase, R 서버 또는 Storm의에서 클러스터를 구성 합니다. 또한 toocustomize 클러스터 방법을 알아보고 tooa 도메인을 조인 하 여 보안을 추가 합니다.

Hadoop 클러스터는 작업의 분산 처리에 사용되는 여러 가상 컴퓨터(노드)로 구성됩니다. Azure HDInsight 되므로 tooprovide 일반 구성 정보를 하나만 설치의 구현 세부 정보 및 구성의 개별 노드를 처리 합니다. 

> [!IMPORTANT]
>HDInsight 클러스터 결제 클러스터 만들어지고 hello 클러스터를 삭제할 때 중지 되 면 시작 합니다. 분 단위로 청구되므로 더 이상 사용하지 않으면 항상 클러스터를 삭제해야 합니다. 너무 방법에 대해 알아봅니다[클러스터를 삭제 합니다.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>클러스터 설정 방법
hello 다음 표에 다양 한 방법을 hello tooset HDInsight 클러스터를 사용할 수 있습니다.

| 다음을 사용하여 만든 클러스터 | 웹 브라우저 사용 | 명령 줄 | REST API | SDK) | 
| --- |:---:|:---:|:---:|:---:|
| [Azure 포털](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure 데이터 팩터리](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Azure 리소스 관리자 템플릿](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>빨리 만들기: 기본 클러스터 설정
이 문서에서는 hello에 대 한 설치 프로그램을 통해 [Azure 포털](https://portal.azure.com)사용 하 여 HDInsight 클러스터를 만들 수 있습니다, *빨리 만들기* 또는 *사용자 지정*합니다. 

Hello 화면 toodo 기본 클러스터 설치 프로그램에 지침을 따릅니다. 다음 사항에 대한 세부 정보가 아래에 제공됩니다.

* [리소스 그룹 이름](#resource-group-name)
* [클러스터 유형 및 구성](#cluster-types) 
* [클러스터 로그인 및 SSH 사용자 이름](#cluster-login-and-ssh-username)
* [위치](#location)

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 3.3 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.
>

## <a name="resource-group-name"></a>리소스 그룹 이름 

[Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 작업할 hello 리소스 그룹, 참조 tooas로 응용 프로그램에 Azure 리소스 그룹은 데 도움이 됩니다. 배포 업데이트 하거나 모니터링 조정 된 단일 작업에서 응용 프로그램에 대 한 모든 hello 리소스를 삭제할 수 있습니다.

## <a name="cluster-types"></a> 클러스터 유형 및 구성
Azure HDInsight는 현재 hello 다음 클러스터 종류의 구성 요소 tooprovide 집합을 가진 특정 기능을 제공 합니다.

> [!IMPORTANT]
> HDInsight 클러스터는 각 단일 워크로드 또는 기술에 다양한 유형으로 사용 가능합니다. Storm 및 한 개의 클러스터에서 HBase 같은 여러 형식을 결합 하는 클러스터는 지원 되는 방법은 toocreate 없습니다. 솔루션에 여러 HDInsight 클러스터 형식 간에 분산 되어 있는 기술 요구 하는 경우는 [Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network) hello 필요한 클러스터 종류를 연결할 수 있습니다. 
>
>

| 클러스터 유형 | 기능 |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |저장된 데이터의 일괄 처리 쿼리 및 분석 |
| [HBase](hdinsight-hbase-overview.md) |많은 양의 스키마 없는 NoSQL 데이터에 대한 처리 |
| [Storm](hdinsight-storm-overview.md) |실시간 이벤트 처리 |
| [Spark](hdinsight-apache-spark-overview.md) |메모리 내 처리, 대화형 쿼리, 마이크로 배치 스트림 처리 |
| [Kafka (미리 보기)](hdinsight-apache-kafka-introduction.md) | 사용 되는 toobuild 실시간 스트리밍 데이터 파이프라인 및 응용 프로그램 일 수 있는 분산된 스트리밍 플랫폼 |
| [R Server](hdinsight-hadoop-r-server-overview.md) |다양한 빅 데이터 통계, 예측 모델링 및 기계 학습 기능 |
| [대화형 Hive(미리 보기)](hdinsight-hadoop-use-interactive-hive.md) |대화형 및 더 빠른 Hive 쿼리에 대한 메모리 내 캐싱 |

### <a name="number-of-nodes-for-each-cluster-type"></a>각 클러스터 유형에 대한 노드 수
각 클러스터 유형에는 자체 노드 수, 노드에 대한 용어 및 기본 VM 크기가 있습니다. 다음 표에서 hello, 각 노드 형식에 대 한 노드 수 hello 괄호 안의 항목은 합니다.

| 형식 | 노드 | 다이어그램 |
| --- | --- | --- |
| Hadoop은 |헤드 노드(2), 데이터 노드(1+) |![HDInsight Hadoop 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |헤드 서버(2), 지역 서버(1+), 마스터/ZooKeeper 노드(3) |![HDInsight HBase 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nimbus 노드(2), 감독자 서버(1+), ZooKeeper 노드(3) |![HDInsight Storm 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |헤드 노드(2), 작업자 노드(1+), ZooKeeper 노드(3)(A1 ZooKeeper VM 크기의 경우 무료) |![HDInsight Spark 클러스터 노드](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

자세한 내용은 참조 [기본 클러스터 노드 구성 및 가상 컴퓨터 크기](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) 에 "hello Hadoop 구성 요소 및 HDInsight의 버전이 무엇 인가요?"

### <a name="hdinsight-version"></a>HDInsight 버전
이 클러스터에 대 한 HDInsight hello 버전을 선택 합니다. 자세한 내용은 [지원되는 HDInsight 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.

### <a name="cluster-tiers"></a>클러스터 계층: HDInsight 서비스 계층

Azure HDInsight hello 빅 데이터 클라우드 서비스의 두 가지 서비스 계층을 제공: Standard 및 Premium입니다.  자세한 내용은 [HDInsight Standard 및 HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)을 참조하세요.

hello 다음 스크린샷은 hello 클러스터 종류를 선택 하기 위한 Azure 포털 정보입니다.

![HDInsight 프리미엄 구성](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>클러스터 로그인 및 SSH 사용자 이름
HDInsight 클러스터를 사용하면 클러스터 생성 중에 다음과 같은 두 개의 사용자 계정을 구성할 수 있습니다.

* HTTP 사용자: hello 기본 사용자 이름인 *admin*합니다. Hello Azure 포털에서 기본 구성을 hello를 사용합니다. 경우에 따라 "클러스터 사용자"라고도 합니다.
* SSH 사용자 (Linux 클러스터): SSH 통해 사용 되는 tooconnect toohello 클러스터입니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a name="location"></a>클러스터 및 저장소 위치(영역)

Toospecify hello 클러스터 위치를 명시적으로 필요 하지 않습니다: hello 클러스터가 hello에 있고 동일한 hello 기본 저장소 위치입니다. 지원 되는 지역 목록은 hello 클릭 **지역** 드롭 다운 목록에서 [HDInsight 가격](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)합니다.

## <a name="storage-endpoints-for-clusters"></a>클러스터에 대한 저장소 끝점

Hadoop의 온-프레미스 설치에서는 hello 클러스터에서 저장소를 Hadoop 분산 파일 시스템 (HDFS) hello 하지만 hello에서 클라우드 저장소 끝점을 사용 하 여 toocluster을 연결 합니다. HDInsight 클러스터는 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) 또는 [Azure Storage의 Blob](hdinsight-hadoop-use-blob-storage.md)을 사용합니다. Azure 저장소 서비스 또는 데이터 레이크 저장소를 사용 하 여 데이터를 유지 하면서 계산을 위해 사용 하는 hello HDInsight 클러스터를 삭제 해도 의미 합니다. 

> [!WARNING]
> 추가 저장소 계정을 사용 하 여 hello HDInsight 클러스터에서 다른 위치에 지원 되지 않습니다.

구성 하는 동안 hello 기본 저장소 끝점을 지정할 수는 Azure 저장소 계정 또는 데이터 레이크 저장소의 blob 컨테이너 있습니다. hello 기본 저장소에 응용 프로그램 및 시스템 로그 합니다. 필요에 따라 추가 연결 된 Azure 저장소 계정과 클러스터 hello Data Lake 저장소 계정에 액세스할 수를 지정할 수 있습니다. hello HDInsight 클러스터와 hello 종속 저장소 계정에 있어야 합니다. hello 동일한 Azure 위치입니다.

![클러스터 저장소 설정: HDFS 호환 저장소 끝점](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>선택적 Metastore
선택적 하이브 또는 Oozie Metastore를 만들 수 있습니다. 그러나 일부 클러스터 형식은 Metastore를 지원하지 않으며, Azure SQL Data Warehouse는 Metastore와 호환되지 않습니다. 

> [!IMPORTANT]
> 사용자 지정 metastore를 만들 때에 대시, 하이픈 또는 hello 데이터베이스 이름에 공백이 사용 하지 마십시오. 이 인해 hello 클러스터 만들기 프로세스 toofail 수 있습니다.

### <a name="use-hiveoozie-metastore"></a>Hive metastore

원할 경우 tooretain 하이브 테이블 HDInsight 클러스터를 삭제 한 후 사용자 지정 metastore를 사용 합니다. 그런 다음 hello metastore tooanother HDInsight 클러스터를 연결할 수 있습니다.

특정 HDInsight 클러스터 버전에 대해 만든 HDInsight metastore는 여러 다른 HDInsight 클러스터 버전 간에 공유할 수 없습니다. HDInsight 버전 목록은 [지원되는 HDInsight 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.

### <a name="oozie-metastore"></a>Oozie Metastore

tooincrease 성능 Oozie를 사용 하는 경우 사용자 지정 metastore를 사용 합니다. Metastore는 클러스터를 삭제 한 후 tooOozie 작업 데이터에 액세스를 제공할 수도 있습니다. 

> [!IMPORTANT]
> 사용자 지정 Oozie Metastore는 다시 사용할 수 없습니다. 사용자 지정 Oozie metastore toouse hello HDInsight 클러스터를 만들 때 빈 Azure SQL 데이터베이스를 제공 해야 합니다.

## <a name="configure-cluster-size"></a>클러스터 크기 구성

존재 하는 hello 클러스터 노드 사용량에 대 한 요금이 청구 됩니다. 클러스터를 만들면 청구 시작 되 고 중지 hello 클러스터 삭제 될 때입니다. 클러스터의 경우 할당을 취소하거나 보류할 수 없습니다.

hello 비용 HDInsight 클러스터의 노드 및 노드 hello에 대 한 hello 가상 컴퓨터 크기의 hello 수로 결정 됩니다. 

클러스터 유형마다 서로 다른 노드 유형, 노드 수 및 노드 크기를 포함합니다.
* Hadoop 클러스터 유형 기본값: 
    * *헤드 노드* 2개  
    * *데이터 노드* 4개
* Storm 클러스터 유형 기본값: 
    * *Nimbus 노드* 2개
    * *ZooKeeper 노드* 3개
    * *감독자 노드* 4개 

HDInsight만 사용하려는 경우, 하나의 데이터 노드를 사용하는 것이 좋습니다. HDInsight 가격에 대한 자세한 내용은 [HDInsight 가격](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)을 참조하세요.

> [!NOTE]
> hello 클러스터 크기 한도 Azure 구독 마다 다릅니다. 연락처 [Azure 청구 지원](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello 제한 합니다.
>

Hello 노드 크기 hello를 통해 사용할 수는 hello Azure 포털 tooconfigure hello 클러스터를 사용할 때는 **노드 가격 책정 계층** 블레이드입니다. Hello 포털에서 확인할 수 있습니다 hello hello 다양 한 노드 크기와 관련 된 비용입니다. 

![HDInsight VM 노드 크기](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>가상 컴퓨터 크기 
클러스터를 배포 하는 경우 선택 기반 계산 리소스 hello 솔루션 toodeploy 계획 합니다. hello 다음 Vm은 HDInsight 클러스터에 사용 됩니다.
* A 및 D1-4 시리즈 VM: [범용 Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* D11-14 시리즈 VM: [메모리 최적화 Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

값 초과 toofind toospecify VM 크기를 사용 하 여 클러스터를 만드는 동안 다양 한 Sdk hello 또는 Azure PowerShell을 사용 하는 동안 참조를 사용 해야 [VM의 크기를 조정 하는 HDInsight 클러스터에 대 한 toouse](../cloud-services/cloud-services-sizes-specs.md#size-tables)합니다. 이 연결 된 문서에서 값을 사용할 hello hello **크기** hello 테이블의 열입니다.

> [!IMPORTANT]
> 클러스터에 필요한 작업자 노드 수가 32개를 초과하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.
>
>

자세한 내용은 [가상 컴퓨터의 크기](../virtual-machines/windows/sizes.md)를 참조하세요. 다양 한 크기의 hello 가격에 대 한 정보를 참조 하십시오. [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight)합니다.   

## <a name="custom-cluster-setup"></a>사용자 지정 클러스터 설정
빠른 hello에 사용자 지정 클러스터 설치 빌드 설정을 만들고 hello 다음 옵션을 추가 합니다.
- [HDInsight 응용 프로그램](#hdinsight-applications)
- [클러스터 크기](#cluster-size):
- 고급 설정
  - [스크립트 동작](#customize-clusters-using-script-action)
  - [가상 네트워크](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>클러스터에 HDInsight 응용 프로그램 설치

HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다. Microsoft, 타사에서 제공하거나 또는 직접 개발한 응용 프로그램을 사용할 수 있습니다. 자세한 내용은 [Azure HDInsight에 타사 Hadoop 응용 프로그램 설치](hdinsight-apps-install-applications.md)를 참조하세요.

빈 가장자리 노드에 대부분의 hello HDInsight 응용 프로그램이 설치 됩니다.  빈 가장자리 노드는 동일한 클라이언트 도구 설치 및 헤드 노드 hello와 같이 구성 hello로 Linux 가상 컴퓨터. Hello 클러스터에 액세스, 클라이언트 응용 프로그램을 테스트 하 고, 클라이언트 응용 프로그램을 호스팅하기 위한 hello 가장자리 노드를 사용할 수 있습니다. 자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.

## <a name="advanced-settings-script-actions"></a>고급 설정: 스크립트 작업

만드는 동안 스크립트를 사용하여 추가 구성 요소를 설치하거나 클러스터 구성을 사용자 지정할 수 있습니다. 이러한 스크립트를 통해 호출 되는 **스크립트 동작**, hello Azure 포털, HDInsight Windows PowerShell cmdlet 또는 hello HDInsight.NET SDK에서 사용할 수 있는 구성 옵션은입니다. 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)(영문)을 참조하세요.

Mahout 및 Cascading와 같은 일부 네이티브 Java 구성 요소가 JAR (Java Archive) 파일로 hello 클러스터에서 실행할 수 있습니다. 이러한 JAR 파일 분산된 tooAzure 저장 될 수 있습니다 및 tooHDInsight 클러스터 Hadoop 작업 전송 메커니즘으로 전송 합니다. 자세한 내용은 [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.

> [!NOTE]
> JAR 파일 tooHDInsight 클러스터 배포 문제 또는 문의 HDInsight 클러스터에서 JAR 파일을 호출할 경우 [Microsoft 지원](https://azure.microsoft.com/support/options/)합니다.
>
> Cascading은 HDInsight에서 지원되지 않으며 Microsoft 지원 대상이 아닙니다. 지원 되는 구성의 목록에 대 한 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)합니다.
>
>

경우에 따라 원하는 hello 만드는 프로세스 동안 구성 파일을 다음 tooconfigure hello:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

자세한 내용은 [부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md)을 참조하세요.

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>고급 설정: 가상 네트워크를 사용하여 클러스터 확장
솔루션에 여러 HDInsight 클러스터 형식 간에 분산 되어 있는 기술 요구 하는 경우는 [Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network) hello 필요한 클러스터 종류를 연결할 수 있습니다. Toodirectly 서로 통신이 구성에서는 hello 클러스터 및 toothem 배포한 모든 코드를 허용 합니다.

HDInsight와 함께 Azure Virtual Network를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.

Azure Virtual Network 내에서 두 개의 클러스터 유형을 사용하는 예제는 [Storm 및 HBase의 센서 데이터 분석](hdinsight-storm-sensor-data-analysis.md)을 참조하세요. HDInsight를 사용 하 여 hello 가상 네트워크에 대 한 특정 구성 요구 사항을 포함 하 여 가상 네트워크에 대 한 자세한 내용은 참조 하십시오. [Azure 가상 네트워크를 사용 하 여 HDInsight 확장 기능](hdinsight-extend-hadoop-virtual-network.md)합니다.

## <a name="troubleshoot-access-control-issues"></a>액세스 제어 문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계

- [HDInsight, hello Hadoop 에코 시스템 및 Hadoop 클러스터는 무엇입니까?](hdinsight-hadoop-introduction.md)
- [HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Windows PC에서 HDInsight의 Hadoop 작업](hdinsight-hadoop-windows-tools.md)
