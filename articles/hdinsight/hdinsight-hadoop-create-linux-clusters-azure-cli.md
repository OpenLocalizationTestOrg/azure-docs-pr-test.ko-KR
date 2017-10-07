---
title: "hello 명령줄-Azure HDInsight를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "Toocreate HDInsight 클러스터를 사용 하 여 플랫폼 간 Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 HDInsight 클러스터를 만들려면

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

이 문서 연습이 hello Azure CLI 1.0을 사용 하 여 3.5 HDInsight 클러스터 만들기의 hello 단계.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.


## <a name="prerequisites"></a>필수 조건

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

* **Azure CLI**. 이 문서의 단계 hello Azure CLI 버전 0.10.14와 마지막 테스트 되었습니다.

    > [!IMPORTANT]
    > 이 문서의 단계 hello Azure CLI 2.0과 함께 작동 하지 않습니다. Azure CLI 2.0은 HDInsight 클러스터 만들기를 지원하지 않습니다.

## <a name="log-in-tooyour-azure-subscription"></a>Azure 구독 tooyour에 로그인

설명 하는 hello 단계에 따라 [hello Azure CLI (명령줄 인터페이스 Azure)에서 tooan Azure 구독 연결](../xplat-cli-connect.md) hello를 사용 하 여 tooyour 구독을 연결 하 고 **로그인** 메서드.

## <a name="create-a-cluster"></a>클러스터 만들기

단계를 수행 하는 hello PowerShell 또는 Bash 등의 명령줄에서 수행 되어야 합니다.

1. 사용 하 여 hello 다음 명령 tooauthenticate tooyour Azure 구독을 사용할 수 있습니다.

        azure login

    사용자 이름 및 암호 입력 정보 요청된 tooprovide 됩니다. 여러 Azure 구독이 있으면 사용 하 여 `azure account set <subscriptionname>` Azure CLI hello tooset hello 구독 명령을 사용 합니다.

2. 다음 명령을 hello를 사용 하 여 tooAzure 리소스 관리자 모드를 전환 합니다.

        azure config mode arm

3. 리소스 그룹을 만듭니다. 이 리소스 그룹 hello HDInsight 클러스터를 포함 하 고 연결 된 저장소 계정입니다.

        azure group create groupname location

    * 대체 `groupname` hello 그룹에 대 한 고유한 이름을 사용 합니다.

    * 대체 `location` toocreate hello 그룹에서 원하는 hello 지리적 지역에 있습니다.

       목록이 유효한 위치에 대 한 hello를 사용 하 여 `azure location list` 명령을 실행 하 고 다음 hello에서 hello 위치 중 하나를 사용 하 여 `Name` 열입니다.

4. 저장소 계정을 만듭니다. 이 저장소 계정은 hello HDInsight 클러스터에 대 한 hello 기본 저장소로 사용 됩니다.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * 대체 `groupname` hello 이전 단계에서 만든 hello 그룹의 hello 이름으로 합니다.

    * 대체 `location` hello 이전 단계에서 동일한 위치에 사용 되는 hello로 합니다.

    * 대체 `storagename` hello 저장소 계정에 대 한 고유한 이름을 사용 합니다.

        > [!NOTE]
        > 이 명령을 사용 하는 hello 매개 변수에 대 한 자세한 내용은 사용 하 여 `azure storage account create -h` 이 명령에 대 한 tooview 도움말입니다.

5. 검색 hello 키 tooaccess hello 저장소 계정을 사용합니다.

        azure storage account keys list -g groupname storagename

    * 대체 `groupname` hello 리소스 그룹 이름을 사용 합니다.
    * 대체 `storagename` hello hello 저장소 계정의 이름으로 사용 합니다.

     반환 되는 hello 데이터 저장 hello `key` 값 `key1`합니다.

6. HDInsight 클러스터 만들기

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * 대체 `groupname` hello 리소스 그룹 이름을 사용 합니다.

    * 대체 `Hadoop` toocreate 한다고 hello 클러스터 유형입니다. 예를 들어 `Hadoop`, `HBase`, `Kafka`, `Spark` 또는 `Storm`입니다.

     > [!IMPORTANT]
     > HDInsight 클러스터 hello 기술에 대 한 튜닝 또는 클러스터 해당 toohello 작업 부하는 다양 한 형식으로 제공 합니다. Storm 및 한 개의 클러스터에서 HBase 같은 여러 형식을 결합 하는 클러스터는 지원 되는 방법은 toocreate 없습니다.

    * 대체 `location` 이전 단계에서 사용 되는 동일한 위치 hello로 합니다.

    * 대체 `storagename` 을 hello 저장소 계정 이름입니다.

    * 대체 `storagekey` hello 이전 단계에서 얻은 hello 키입니다.

    * Hello에 대 한 `--defaultStorageContainer` 매개 변수를 사용 하 여 hello hello 클러스터에 대 한 사용 하 여 이름을 동일 합니다.

    * 대체 `admin` 및 `httppassword` hello 이름 및 암호로 원하는 toouse HTTPS를 통해 hello 클러스터에 액세스할 때.

    * 대체 `sshuser` 및 `sshuserpassword` hello 사용자 이름 및 암호와 함께 원하는 toouse SSH를 사용 하 여 hello 클러스터에 액세스할 때

    > [!IMPORTANT]
    > 이 예제에서는 2개의 작업자 노드를 사용하여 클러스터를 만듭니다. 크기 조정 작업을 수행 하 여 클러스터를 만든 후 hello 작업자 노드 수를 변경할 수 있습니다. 사용하려는 작업자 노드 수가 32개를 초과하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다. Hello를 사용 하 여 hello 헤드 노드 크기를 설정할 수 있습니다 `--headNodeSize` 클러스터를 만드는 동안 매개 변수입니다.
    >
    > 노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.

    클러스터 만들기 프로세스 toofinish hello에 대 일 분 정도 걸릴 수 있습니다. 일반적으로 약 15분이 걸립니다.

## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계

Hello Azure CLI를 사용 하 여 HDInsight 클러스터를 성공적으로 만든 했으므로 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork:

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
