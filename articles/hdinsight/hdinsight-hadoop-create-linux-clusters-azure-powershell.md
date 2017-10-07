---
title: "aaaCreate Hadoop 클러스터 PowerShell-Azure HDInsight를 사용 하 여 | Microsoft Docs"
description: "어떻게 toocreate Hadoop, HBase, 스톰, 또는 Spark 클러스터 Linux에서 HDInsight에 대 한 Azure PowerShell을 사용 하 여에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Azure PowerShell을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell은 toocontrol를 사용 하 고 Microsoft Azure에서 작업의 hello 배포 및 관리를 자동화할 수 있는 강력한 스크립팅 환경입니다. 이 문서는 Azure PowerShell을 사용 하 여 toocreate Linux 기반 HDInsight 클러스터 하는 방법에 대 한 정보를 제공 합니다. 또한 예제 스크립트도 포함됩니다.

> [!NOTE]
> Azure PowerShell은 Windows 클라이언트에서만 사용할 수 있습니다. Linux, Unix, 또는 Mac OS X 클라이언트를 사용 하는 경우 참조 [Azure CLI를 사용 하 여 Linux 기반 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-cli.md) hello Azure CLI toocreate 클러스터 사용에 대 한 정보에 대 한 합니다.

## <a name="prerequisites"></a>필수 조건
이 절차를 시작 하기 전에 hello 다음이 필요 합니다.

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다. Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.
    >
    > Hello 단계에 따라 [Azure PowerShell 설치](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello 최신 버전의 Azure PowerShell. 해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.

## <a name="create-cluster"></a>클러스터 만들기

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Azure PowerShell을 사용 하 여 HDInsight 클러스터 toocreate hello 다음 절차를 완료 해야 합니다.

* Azure 리소스 그룹 만들기
* Azure 저장소 계정 만들기
* Azure Blob 컨테이너 만들기
* HDInsight 클러스터 만들기

hello 다음 스크립트에서는 방법을 toocreate 새 클러스터:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

hello 클러스터 로그인에 대해 지정 하는 hello 값은 사용 되는 toocreate hello hello 클러스터에 대 한 Hadoop 사용자 계정입니다. 이 계정 tooconnect tooservices 웹 Ui 또는 REST Api와 같은 hello 클러스터에서 호스트를 사용 합니다.

hello SSH 사용자에 대해 지정 하는 hello 값은 hello 클러스터에 대 한 사용 되는 toocreate hello SSH 사용자입니다. 이 사용 하 여 원격 SSH 세션 toostart hello 클러스터에서 계정 및 작업을 실행 합니다. 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

> [!IMPORTANT]
> (클러스터를 만들 때 또는 hello 크기 조정 하 여 클러스터를 만든 후) 32 개 이상의 작업자 노드 toouse 하려는 경우에 적어도 8 코어, 14GB ram와 헤드 노드 크기를 지정 해야 합니다.
>
> 노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.

클러스터를 too20 분 toocreate 걸릴 수 있습니다.

## <a name="create-cluster-configuration-object"></a>클러스터 만들기: 구성 개체

또한 `New-AzureRmHDInsightClusterConfig` cmdlet을 사용하여 HDInsight 구성 개체를 만들 수 있습니다. 그런 다음 클러스터에 대해이 구성 개체 tooenable 추가 구성 옵션을 수정할 수 있습니다. 마지막으로 hello를 사용 하 여 `-Config` hello의 매개 변수 `New-AzureRmHDInsightCluster` cmdlet toouse hello 구성 합니다.

hello 다음 스크립트는 구성 개체 tooconfigure를 R 서버에 만듭니다 HDInsight 클러스터 유형. hello 구성을 통해 가장자리 노드, RStudio, 및 추가 저장소 계정 수 있습니다.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> 저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다. 이 예제를 사용할 때는 hello에 hello 추가 저장소 계정을 만들 hello 서버와 동일한 위치 합니다.

## <a name="customize-clusters"></a>클러스터 사용자 지정

* [부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell)을 참조하세요.
* [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계

HDInsight 클러스터를 성공적으로 만든 리소스 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork 합니다.

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

