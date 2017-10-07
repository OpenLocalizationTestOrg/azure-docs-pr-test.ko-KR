---
title: "Azure HDInsight에 대화형 하이브 aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 대화형 (하이브 LLAP에) HDInsight의 Hive toouse 합니다."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>HDInsight에서 대화형 Hive 사용(미리 보기)
대화형 Hive(즉, [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP))는 새로운 HDInsight [클러스터 유형](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)입니다.  대화형 Hive에서는 메모리 내 캐싱이 가능하여 Hive 쿼리의 대화형 방식을 강화하고 빠르게 만들 수 있습니다. 이 새로운 기능을 통해 hello 중 하나는 HDInsight 세계에서 대부분 성능이 나 유연 하며 열기 빅 데이터 솔루션 hello 클라우드에서 (Hive 및 Spark 사용) 하는 메모리 내 캐시와 고급 R 서비스와 완벽 한 통합을 통해 분석 합니다. 

hello 대화형 하이브 클러스터는 hello Hadoop 클러스터와에서 다릅니다. 만 hello 하이브 서비스를 포함 합니다. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie 및 기타 서비스는 이 클러스터 유형에서 곧 제거될 예정입니다.
> hello hello 대화형 하이브 클러스터에서 하이브 서비스는 hello Ambari 하이브 보기, Beeline, 및 하이브 ODBC를 통해 액세스할 수만 있습니다. Hive 콘솔, Templeton, Azure CLI 및 Azure PowerShell을 통해서는 액세스할 수 없습니다. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>대화형 Hive 클러스터 만들기
대화형 Hive 클러스터는 Linux 기반 클러스터에서만 지원됩니다. HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

## <a name="execute-hive-from-interactive-hive"></a>대화형 Hive에서 Hive 실행
Hive 쿼리를 실행하는 방식에 대한 다양한 옵션이 있습니다.

* Hello Ambari 하이브 보기를 사용 하 여 하이브를 실행 합니다.
  
    Hello 하이브 보기를 사용 하는 방법에 대 한 hello 내용은 [사용 하 여 hello HDInsight에서 Hadoop으로 하이브 보기](hdinsight-hadoop-use-hive-ambari-view.md)합니다.
* Beeline을 사용하여 Hive 실행
  
    Hello에 대 한 내용은 Beeline HDInsight에서 사용 하 여 참조 [Beeline 포함 하는 HDInsight에서 Hadoop으로 사용 하 여 하이브](hdinsight-hadoop-use-hive-beeline.md)합니다.
  
    헤드 노드에 hello 또는 빈 가장자리 노드 중 하나에서 Beeline를 사용합니다.  빈 에지 노드에서 Beeline을 사용하는 것이 좋습니다.  빈 에지 노드로 HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.
* Hive ODBC를 사용하여 Hive 실행
  
    Hello에 대 한 내용은 하이브 ODBC를 사용 하 여 참조 [hello Microsoft 하이브 ODBC 드라이버와 함께 Excel 연결 tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)합니다.

**toofind hello JDBC 연결 문자열:**

1. TooAmbari url hello를 사용 하 여 로그온: https://<ClusterName>합니다. AzureHDInsight.net 합니다.
2. 클릭 **하이브** hello 왼쪽된 메뉴에서 합니다.
3. 강조 표시 하는 hello 아이콘 toocopy hello URL을 클릭 합니다.
   
   ![HDInsight Hadoop 대화형 Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>참고 항목
* [HDInsight에서 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-provision-linux-clusters.md): 대화형 하이브 toocreate HDInsight 클러스터를 방법에 대해 알아봅니다.
* [하이브를 사용 하 여 Beeline 포함 하는 HDInsight에서 Hadoop으로](hdinsight-hadoop-use-hive-beeline.md): 자세한 방법을 toouse Beeline toosubmit 하이브 쿼리 합니다.
* [Hello Microsoft 하이브 ODBC 드라이버를 사용 하 여 Excel tooHadoop 연결](hdinsight-connect-excel-hive-odbc-driver.md): 자세한 방법을 tooconnect Excel tooHive 합니다.

