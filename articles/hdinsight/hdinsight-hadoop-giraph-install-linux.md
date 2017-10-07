---
title: "aaaInstall Giraph HDInsight (Hadoop)-Azure에서 사용 하 여 | Microsoft Docs"
description: "Linux 기반 HDInsight의 Giraph tooinstall 스크립트 동작을 사용 하는 클러스터 방법을 알아봅니다. 스크립트 동작 사용 하면 toocustomize hello 클러스터를 만드는 동안 클러스터 구성을 변경 하거나 서비스와 유틸리티를 설치 하 여 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>HDInsight Hadoop 클러스터에서 Giraph를 설치 하 고 Giraph tooprocess 대규모 그래프를 사용 합니다.

자세한 내용은 방법 HDInsight 클러스터에서 Apache Giraph tooinstall 합니다. HDInsight의 hello 스크립트 동작 기능 toocustomize 수 있습니다. 클러스터 bash 스크립트를 실행 합니다. 스크립트 처리 도중과 클러스터를 만든 후 사용 되는 toocustomize 클러스터 수 있습니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="whatis"></a>Giraph 정의

[Apache Giraph](http://giraph.apache.org/) tooperform 그래프 Hadoop을 사용 하 여 처리를 허용 하 고 Azure HDInsight 함께 사용할 수 있습니다. Graph는 개체 간의 관계를 모델링합니다. 예를 들어 대규모 네트워크에 있는 라우터 간 hello 연결 같은 hello 인터넷 또는 소셜 네트워크에 있는 사용자 간의 관계입니다. Graph 처리 하면 그래프를 개체 간의 관계 hello에 대 한 tooreason 같은:

* 현재 관계를 기반으로 하여 잠재적인 친구 파악.

* 네트워크에 두 컴퓨터 간에 hello 최단 경로 식별 합니다.

* 웹 페이지의 hello 페이지 순위를 계산 합니다.

> [!WARNING]
> Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원-Microsoft 지원 tooisolate 도와 관련된 toothese 구성 요소 문제를 해결 합니다.
>
> Giraph, 같은 사용자 지정 구성 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다. Microsoft 지원에는 수 tooresolving hello 문제일 수 있습니다. 그렇지 않으면 해당 기술에 대한 전문 지식을 찾을 수 있는 오픈 소스 커뮤니티를 참조해야 합니다. 예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).


## <a name="what-hello-script-does"></a>어떤 hello이 스크립트는

이 스크립트는 hello 다음 작업을 수행 합니다.

* 너무 Giraph 설치`/usr/hdp/current/giraph`

* 복사본 hello `giraph-examples.jar` toodefault 용 파일 저장소 (WASB) 클러스터:`/example/jars/giraph-examples.jar`

## <a name="install"></a>스크립트 동작을 사용하여 Giraph 설치

HDInsight 클러스터에서 샘플 스크립트 tooinstall Giraph hello 수정할 수 있는 위치에서 제공 됩니다.

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

이 섹션 toouse hello Azure 포털을 사용 하 여 hello 클러스터를 만드는 동안 샘플 스크립트를 hello 하는 방법에 지침을 제공 합니다.

> [!NOTE]
> Hello 메서드를 다음 중 하나를 사용 하 여 스크립트 동작을 적용할 수 있습니다.
> * Azure PowerShell
> * hello Azure CLI
> * hello HDInsight.NET SDK
> * Azure 리소스 관리자 템플릿
> 
> 클러스터를 실행 하는 스크립트 작업 tooalready를 적용할 수 있습니다. 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.

1. hello 단계를 사용 하 여 클러스터를 만들기 시작 [만들 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-create-linux-clusters-portal.md), 하지만 만들기를 완료 하지는 않습니다.

2. Hello에 **옵션 구성** 블레이드를 **스크립트 동작**, hello 다음 정보를 제공 합니다.

   * **이름**: hello 스크립트 동작에 대 한 이름을 입력 합니다.

   * **스크립트 URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**: 이 항목 선택

   * **작업자**: 이 항목을 선택 취소된 상태로 둡니다.

   * **ZOOKEEPER**: 이 항목을 선택 취소된 상태로 둡니다.

   * **PARAMETERS**: 이 필드는 공백으로 둡니다.

3. Hello hello 맨 아래에 **스크립트 동작**, hello를 사용 하 여 **선택** 단추 toosave hello 구성 합니다. 마지막으로 hello를 사용 하 여 **선택** hello 아래쪽 hello의 단추 **선택적 구성** 블레이드 toosave hello 선택적 구성 정보입니다.

4. 에 설명 된 대로 hello 클러스터 만들기를 계속 [만들 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-create-linux-clusters-portal.md)합니다.

## <a name="usegiraph"></a>HDInsight에서 Giraph를 사용하는 방법

Hello 클러스터를 만든 후 다음 단계 toorun hello SimpleShortestPathsComputation 예제 Giraph에 포함 된 hello를 사용 합니다. 이 예에서는 hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) hello 그래프에 있는 개체 사이의 최단 경로 찾기 위한 구현 합니다.

1. SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. 사용 하 여 hello 다음 명령은 toocreate 이라는 파일로 내보내집니다 **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    이 데이터는 hello 형식을 사용 하 여는 방향된 그래프에 있는 개체 사이의 관계를 설명 `[source_id, source_value,[[dest_id], [edge_value],...]]`합니다. 각 줄은 `source_id` 개체와 하나 이상의 `dest_id` 개체 간 관계를 나타냅니다. hello `edge_value` hello 수준 또는 거리 간의 hello 연결의으로 생각할 수 `source_id` 및 `dest\_id`합니다.

    으로 그린 하며 hello 값 (또는 가중치)를 사용 하 여 개체 간의 hello 거리로, hello 데이터 같습니다 다이어그램을 다음 hello:

    ![원과 거리가 다른 선으로 그린 tiny_graph.txt](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. toosave hello 파일을 사용 하 여 **Ctrl + X**, 다음 **Y**, 마지막으로 **Enter** tooaccept hello 파일 이름입니다.

4. HDInsight 클러스터에 대 한 기본 저장소에 같은 toostore hello 데이터가 hello를 사용 합니다.

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. 다음 명령을 hello를 사용 하 여 hello SimpleShortestPathsComputation 예제를 실행 합니다.

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    이 명령과 함께 사용 되는 hello 매개 변수는 hello 다음 표에 설명 되어 있습니다.

   | 매개 변수 | 기능 |
   | --- | --- |
   | `jar` |hello 예가 포함 된 hello jar 파일입니다. |
   | `org.apache.giraph.GiraphRunner` |hello 클래스 toostart hello 예제를 사용 합니다. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |사용 되는 hello 예입니다. 이 예제에서는 ID가 1과 hello 그래프의 다른 모든 Id 간의 hello 최단 경로 계산합니다. |
   | `-ca mapred.job.tracker` |hello 클러스터에 대 한 hello 헤드 노드에 있습니다. |
   | `-vif` |hello hello 입력된 데이터에 대 한 입력된 형식이 toouse 합니다. |
   | `-vip` |hello 입력된 데이터 파일입니다. |
   | `-vof` |hello 출력 형식입니다. 이 예제에서는 일반 텍스트인 ID 및 값입니다. |
   | `-op` |hello 출력 위치입니다. |
   | `-w 2` |작업자 toouse hello 수입니다. 이 예제에서는 2입니다. |

    이러한 오류 코드 및 Giraph 샘플에 사용 되는 다른 매개 변수에 자세한 내용은 참조 hello [Giraph 퀵 스타트](http://giraph.apache.org/quick_start.html)합니다.

6. Hello 작업이 완료 되 면 hello 결과 hello에 저장 되므로 **/example/out/shotestpaths** 디렉터리입니다. hello 출력 파일 이름으로 시작 **파트-m-** 하 고 끝나야 등 파일을 먼저 둘째, hello를 나타내는 숫자입니다. 다음 명령 tooview hello 출력 hello를 사용 합니다.

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    hello 출력 텍스트 다음 비슷한 toohello 같아야 합니다.

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    hello SimpleShortestPathComputation 예제 개체 ID가 1와 하드 코드 된 toostart and hello 가장 짧은 경로 tooother 개체를 찾는입니다. hello 출력 hello 형식으로 되어 `destination_id` 및 `distance`합니다. hello `distance` 가 짧아 지도록 hello 가장자리 hello 값 (또는 가중치) 개체 ID가 1 사이의 hello 대상 id입니다.

    이 데이터를 시각화 ID 1과 다른 모든 개체 사이의 hello 가장 짧은 경로 이동 하 여 hello 결과 확인할 수 있습니다. ID가 1 및 4 ID 간의 가장 짧은 경로 hello은 5입니다. 이 값은 사이의 hello 총 거리 <span style="color:orange">ID 1과 3</span>, 차례로 <span style="color:red">ID가 3 및 4</span>합니다.

    ![가장 짧은 경로와 함께 원으로 그린 개체](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>다음 단계

* [HDInsight 클러스터에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)입니다.

* [HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md).
