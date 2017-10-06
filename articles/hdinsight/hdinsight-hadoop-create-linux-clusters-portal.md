---
title: "웹 브라우저-Azure HDInsight를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "Azure preview 포털 hello와 어떻게 toocreate Hadoop, HBase, 스톰, 또는 Spark 클러스터로 Linux 웹 브라우저를 사용 하 여 HDInsight에 대 한 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 HDInsight의 Linux 기반 클러스터를 만들려면
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure 포털 hello는 서비스 및 hello Microsoft Azure 클라우드에서 호스트 되는 리소스에 대 한 웹 기반 관리 도구입니다. 이 문서에서 toocreate Linux 기반 HDInsight 클러스터 hello 포털을 사용 하는 방법을 배웁니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Azure 구독**. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* **최신 웹 브라우저**. Azure 포털 hello HTML5 및 Javascript를 사용 하 여 및 이전 버전의 웹 브라우저에서 제대로 작동 하지 않을 수 있습니다.

## <a name="create-clusters"></a>클러스터 만들기
Azure 포털 hello hello 클러스터 속성의 대부분을 표시합니다. Azure Resource Manager 템플릿을 사용하여 이러한 많은 속성을 숨길 수 있습니다. 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **+**, **인텔리전스 + 분석** 및 **HDInsight**를 차례로 클릭합니다.
   
    ![Hello Azure 포털에서에서 새 클러스터를 만드는](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "hello Azure 포털에서에서 새 클러스터 만들기")

3. Hello에 **HDInsight** 블레이드에서 클릭 **(크기, 설정, 응용 프로그램) 사용자 지정**, 클릭 **기본 사항**, hello 다음 정보를 입력 합니다.

    ![Hello Azure 포털에서에서 새 클러스터를 만드는](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "hello Azure 포털에서에서 새 클러스터 만들기")

    * **클러스터 이름**입력: 이 이름은 전역적으로 고유해야 합니다.

    * Hello에서 **구독** 드롭다운 목록에서 선택 hello hello 클러스터에 사용할 Azure 구독.

    * **클러스터 유형**을 클릭한 후 다음을 선택합니다.
   
        * **클러스터 유형**: 어떤 toochoose를 모르는 경우 선택 **Hadoop**합니다. Hello 가장 인기 있는 클러스터 형식입니다.
     
            > [!IMPORTANT]
            > HDInsight 클러스터 hello 기술에 대 한 튜닝 또는 클러스터 toohello 작업 부하를 해당 형식에 제공 합니다. Storm 및 한 개의 클러스터에서 HBase 같은 여러 형식을 결합 하는 클러스터는 지원 되는 방법은 toocreate 없습니다. 
            > 
            > 
        
        * **운영 체제**: **Linux**를 선택합니다.
        
        * **버전**: 어떤 toochoose 모르는 경우 hello 기본 버전을 사용 합니다. 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.
        * **계층 클러스터**: 두 가지 범주의 hello 빅 데이터 클라우드 서비스를 제공 하는 Azure HDInsight: 표준 계층과 고급 계층입니다. 자세한 내용은 [클러스터 계층](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)을 참조하세요.

    * 에 대 한 **클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**, hello 사용자 이름 및 hello 관리: 사용자에 대 한 암호를 제공 합니다.

    * 입력 한 **SSH 사용자 이름** toohave hello SSH 암호가 이전에 지정한 관리자 암호와 동일 hello를 사용 하도록 하려는 경우 선택 hello **동일한 암호를 사용 하 여 클러스터 로그인으로** 확인란 합니다. 그렇지 않은 경우 제공 중 하나는 **암호** 또는 **공개 키**를 사용 하는 tooauthenticate hello SSH 사용자 수 있습니다. 공개 키를 사용 하 여 hello 권장 접근법입니다. 클릭 **선택** hello 아래쪽 toosave hello 자격 증명 구성 시.
   
        자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

    * 에 대 한 **리소스 그룹**, 여부를 지정할 toocreate 새 리소스 그룹을 원하는 기존 집합을 사용 합니다.

    * 데이터 센터 지정 **위치** hello 클러스터를 만들 위치입니다.

    * **다음**을 누릅니다.

4. Hello에 **저장소** 블레이드를 기본 저장소로 Azure 저장소 (WASB) 또는 데이터 레이크 저장소 사용할지를 지정 합니다. 자세한 내용은 아래 hello 표 확인 합니다.

    ![Hello Azure 포털에서에서 새 클러스터를 만드는](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "hello Azure 포털에서에서 새 클러스터 만들기")

    | 저장소                                      | 설명 |
    |----------------------------------------------|-------------|
    | **기본 저장소인 Azure Storage Blob**   | <ul><li>**기본 저장소 형식**으로 **Azure Storage**를 선택합니다. 그 후에 대 한 **선택 방법을**를 선택할 수 있습니다 **내 구독** Azure 구독에 포함 된 저장소 계정 및 저장소 계정 선택 hello toospecify 하려는 경우. 그렇지 않으면 클릭 **선택 키** 외부 Azure 구독에서 toochoose 되도록 hello 저장소 계정에 대 한 hello 정보를 제공 합니다.</li><li>에 대 한 **기본 컨테이너**를 직접 지정 하거나 toogo hello 포털에 제안 된 hello 기본 컨테이너 이름으로 선택할 수 있습니다.</li><li>WASB를 기본 저장소로 사용 하는 경우 클릭할 수 있는 (선택 사항) **추가 저장소 계정을** toospecify 추가 저장소 계정 hello 클러스터와 tooassociate 합니다. Hello에 **Azure 저장소 키** 블레이드에서 클릭 **저장소 키를 추가**, 다음 제공할 수 있습니다는 저장소 계정을 Azure 구독 또는 다른 구독에서 (함으로써 hello 저장소 계정 선택 키)입니다.</li><li>WASB를 기본 저장소로 사용 하는 경우 클릭할 수 있는 (선택 사항) **데이터 레이크 저장소 액세스** toospecify 추가 저장소로 Azure 데이터 레이크 저장소입니다. 자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</li></ul> |
    | **기본 저장소로 Azure Data Lake Store** | 에 대 한 **기본 저장소 형식**선택, **데이터 레이크 저장소** toohello 문서를 참조 하십시오 [Azure 포털을 사용 하 여 데이터 레이크 저장소는 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) 에 대 한 지침입니다. |
    | **외부 Metastore**                      | 필요에 따라 SQL 데이터베이스 toosave Hive 및 Oozie 메타 데이터 hello 클러스터와 연결 된 지정할 수 있습니다. 에 대 한 **하이브에 대 한 SQL 데이터베이스를 선택 합니다.** SQL 데이터베이스를 선택 하 고 다음 hello 데이터베이스에 대 한 hello 사용자 이름/암호를 제공 합니다. Oozie 메타데이터에 대해 이러한 단계를 반복합니다.<br><br>metastores에 대한 Azure SQL Database를 사용하는 동안 몇 가지 고려 사항입니다. <ul><li>hello Azure SQL 데이터베이스 metastore hello에 사용 되는 연결 tooother Azure HDInsight를 포함 한 Azure 서비스를 허용 해야 합니다. Hello Azure SQL 데이터베이스 대시보드 hello 오른쪽에에서 hello 서버 이름을 클릭 합니다. 어떤 hello SQL 데이터베이스 인스턴스가 실행 중인 hello 서버입니다. Hello 서버 보기에서 후 클릭 **구성**, 고 **Azure 서비스**, 클릭 **예**, 클릭 하 고 **저장**합니다.</li><li>Metastore는를 만들 때는 hello 클러스터 만들기 프로세스 toofail 생길 수 있으므로 대시 또는 하이픈을 포함 하는 데이터베이스 이름을 사용 하지 마십시오.</li></ul>                                                                                                                                                                       |

    **다음**을 누릅니다. 

    > [!WARNING]
    > 추가 저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.

5. 필요에 따라 **응용 프로그램** HDInsight 클러스터와 함께 작동 하는 tooinstall 응용 프로그램입니다. Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다. 자세한 내용은 [HDInsight 응용 프로그램 설치](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation)를 참조하세요.


6. 클릭 **클러스터 크기** 이 클러스터에 대해 생성 되는 hello 노드에 대 한 toodisplay 정보입니다. Hello hello 클러스터에 필요한 작업자 노드 수를 설정 합니다. hello 예상 비용 hello 클러스터의 hello 블레이드 내에서 표시 됩니다.
   
    ![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "클러스터 노드 수 지정")
   
   > [!IMPORTANT]
   > 32 개 이상의 작업자 노드를 하려는 경우 클러스터를 만들 때 또는 적어도 8 코어, 14GB에 헤드 노드 크기를 선택 해야 합니다를 만든 후 hello 클러스터를 확장 하 여 ram.
   > 
   > 노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.
   > 
   > 
   
   클릭 **다음** toosave hello 노드 가격 구성 합니다.

7. 클릭 **고급 설정** tooconfigure 사용 하는 등 기타 옵션 설정 **스크립트 동작** toocustomize 클러스터 tooinstall 조인 또는 사용자 지정 구성 요소는 **가상네트워크**. 자세한 내용은 아래 hello 표 확인 합니다.

    ![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "클러스터 노드 수 지정")

    | 옵션 | 설명 |
    |--------|-------------|
    | **스크립트 작업** | Hello 클러스터를 만드는 중으로 toouse 사용자 지정 스크립트 toocustomize는 클러스터를 원하는 경우이 옵션을 사용 합니다. 스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요. |
    | **Virtual Network** | Tooplace hello 클러스터 내 가상 네트워크에 Azure 가상 네트워크 및 hello 서브넷을 선택 합니다. HDInsight를 사용 하 여 hello 가상 네트워크에 대 한 특정 구성 요구 사항을 포함 하 여 가상 네트워크에 대 한 내용은 [Azure 가상 네트워크를 사용 하 여 HDInsight 확장 기능](hdinsight-extend-hadoop-virtual-network.md)합니다. |

    **다음**을 누릅니다.

8. Hello에 **요약** 블레이드에서 이전에 입력 한 hello 정보를 확인 하 고 클릭 **만들기**합니다.

    ![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "클러스터 노드 수 지정")
    
    > [!NOTE]
    > 일반적으로 약 15 분을 만든 hello 클러스터 toobe 약간의 시간이 걸립니다. Hello 타일 hello 시작 보드를 사용 하거나 hello **알림** hello 페이지 toocheck의 프로 비전 프로세스는 hello에 남아 있는 hello에 대 한 항목입니다.
    > 
    > 
12. Hello 생성 프로세스가 완료 되 면 hello 시작 보드 toolaunch hello 클러스터 블레이드에서 hello 클러스터에 대 한 hello 타일을 클릭 합니다. hello 클러스터 블레이드 hello 다음 정보를 제공 합니다.
    
    ![클러스터 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "클러스터 속성")
    
    이 블레이드의 hello 위쪽 toounderstand hello 아이콘 다음 hello를 사용 합니다.
    
    * **개요** 탭 hello 이름, hello hello 위치, hello 운영 체제 hello 클러스터 대시보드 등에 대 한 URL에 포함 된 리소스 그룹이 같은 hello 클러스터에 대 한 모든 hello 필수 정보를 제공 합니다.
    * **대시보드** hello 클러스터와 연결 된 toohello Ambari 포털을 알려 줍니다.
    * **Secure Shell**: tooaccess hello 클러스터 SSH를 사용 하는 데 필요한 정보입니다.
    * **크기 조정 클러스터** hello hello 클러스터와 연결 된 작업자 노드 수를 늘릴 수 있습니다.
    * **삭제**: hello HDInsight 클러스터를 삭제 합니다.
    

## <a name="customize-clusters"></a>클러스터 사용자 지정
* [부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md)을 참조하세요.
* [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계
HDInsight 클러스터를 성공적으로 만든 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork:

### <a name="hadoop-clusters"></a>Hadoop 클러스터
* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight와 함께 MapReduce 사용](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase 클러스터
* [HDInsight에서 HBase 시작](hdinsight-hbase-tutorial-get-started-linux.md)
* [HDInsight에서 HBase용 Java 응용 프로그램 개발](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm 클러스터
* [HDInsight에서 Storm용 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)
* [HDInsight의 Storm에서 Python 구성 요소 사용](hdinsight-storm-develop-python-topology.md)
* [HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark 클러스터
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)

