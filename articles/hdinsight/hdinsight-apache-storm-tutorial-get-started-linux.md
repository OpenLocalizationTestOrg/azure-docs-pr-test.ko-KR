---
title: "Azure HDInsight의 Apache Storm aaaStorm 스타터 보여 주는 예 | Microsoft Docs"
description: "자세한 방법을 toodo 빅 데이터 분석 및 프로세스 데이터를 실시간으로 Apache Storm를 사용 하 여 하 고 hello HDInsight의 storm 스타터 예제입니다."
keywords: "storm-starter, apache storm 예제"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Hello 스톰 시작 예제를 사용 하 여 HDInsight의 Apache Storm 시작

방법을 사용 하 여 HDInsight의 Apache Storm toouse hello 스톰 스타터 예제에 알아봅니다.

Apache Storm은 데이터 스트림 처리용 확장 가능한 분산형 실시간 계산 시스템입니다. Azure HDInsight의 Storm을 사용하여 실시간 데이터 분석을 수행하는 클라우드 기반 Storm 클러스터를 만들 수 있습니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

* **SSH 및 SCP 사용 경험**. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a name="create-a-storm-cluster"></a>Storm 클러스터 만들기

Hello 단계 toocreate 스톰은 HDInsight 클러스터에서 다음을 사용 합니다.

1. Hello에서 [Azure 포털](https://portal.azure.com)선택, **+ 새로 만들기**, **인텔리전스 + 분석**를 선택한 후 **HDInsight**합니다.

    ![HDInsight 클러스터 만들기](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. Hello에서 **기본 사항** 블레이드에서 hello 다음 정보를 입력 합니다.

    * **클러스터 이름**: hello HDInsight 클러스터의 hello 이름입니다.
    * **구독**: hello 구독 toouse를 선택 합니다.
    * **클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**: HTTPS를 통해 hello 클러스터에 액세스할 때 hello 로그인 합니다. Hello Ambari 웹 UI 또는 REST API와 같은 이러한 자격 증명 tooaccess 서비스를 사용 합니다.
    * **SSH 사용자 이름 보안**: SSH를 통해 hello 클러스터에 액세스할 때 사용 하는 hello 로그인 합니다. 기본적으로 hello 암호 hello 클러스터 로그인 암호와 같은 hello 됩니다.
    * **리소스 그룹**: hello 리소스 그룹 toocreate hello 클러스터에 있습니다.
    * **위치**: hello Azure 지역 toocreate hello 클러스터에 있습니다.

    ![구독 선택](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. 선택 **형식 클러스터**, 집합 hello hello에 값에 따라 다음 **클러스터 구성** 블레이드:

    * **클러스터 유형**: Storm

    * **운영 체제**: Linux

    * **버전**: Storm 1.1.0(HDI 3.6)

    * **클러스터 계층**: 표준

    마지막으로 hello를 사용 하 여 **선택** toosave 설정 단추입니다.

    ![클러스터 유형 선택](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Hello 클러스터 종류를 선택한 후 hello를 사용 하 여 __선택__ tooset hello 클러스터 유형 단추입니다. 를 사용 하 여 hello __다음__ 단추 toofinish 기본 구성입니다.

5. Hello에서 **저장소** 블레이드를 선택 하거나 저장소 계정을 만듭니다. 이 문서의 단계 hello에 대 한 hello 나머지 필드는 둡니다 hello 기본 값이 블레이드를 합니다. 사용 하 여 hello __다음__ 단추 toosave 저장소 구성.

    ![HDInsight에 대 한 저장소 계정 설정을 hello 설정](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. Hello에서 **요약** 블레이드에서 hello 클러스터에 대 한 hello 구성 검토 합니다. 사용 하 여 hello __편집__ toochange 올바르지 않은 설정을 연결 합니다. 마지막으로, the__Create__ 단추 toocreate hello 클러스터를 사용 합니다.

    ![클러스터 구성 요약](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Too20 분 toocreate hello 클러스터를 걸릴 수 있습니다.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>HDInsight에서 storm-starter 샘플 실행

1. SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    입력 정보 요청된 tooenter 모르는 암호 toosecure을 SSH 사용자 계정을 사용 하는 경우 것입니다. 공개 키를 사용 하는 경우 필요한 활용해 hello `-i` 매개 변수 toospecify hello 일치 하는 개인 키입니다. 예: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. 다음 명령 예제에서는 토폴로지 toostart hello를 사용 합니다.

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > HDInsight의 이전 버전의 hello 토폴로지의 hello 클래스 이름으로 `storm.starter.WordCountTopology` 대신 `org.apache.storm.starter.WordCountTopology`합니다.

    이 명령은 '단어 수'의 이름으로 hello 클러스터에서 hello WordCount 토폴로지 예제를 시작합니다. 임의로 hello 문장에서 각 단어의 hello 발생 횟수 및 문장 생성합니다.

    > [!NOTE]
    > Hello를 사용 하기 전에 hello 클러스터를 포함 하는 hello jar 파일을 먼저 복사 해야 토폴로지 toohello 클러스터를 전송할 때 `storm` 명령입니다. 사용 하 여 hello `scp` 명령 toocopy hello 파일입니다. 예를 들어 `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > hello WordCount 예제 및 기타 스톰 시작 예제에서 클러스터에 이미 포함 되어 `/usr/hdp/current/storm-client/contrib/storm-starter/`합니다.

hello 코드를 찾을 수 인 경우 hello 소스 hello 스톰 시작 예제를 보려면 [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter)합니다. 이 링크는 Storm 1.1.x에 해당하며 HDInsight 3.6과 함께 제공됩니다. 다른 버전 Storm의 hello를 사용 하 여 __분기__ 다른 스톰 버전 hello 페이지 tooselect hello 위쪽에 단추입니다.

## <a name="monitor-hello-topology"></a>모니터 hello 토폴로지

hello 스톰 UI 작업 토폴로지, 실행을 위한 웹 인터페이스를 제공 하 고 HDInsight 클러스터에 포함 됩니다.

Hello 단계 toomonitor hello 토폴로지 hello 스톰 UI를 사용 하 여 다음을 사용 합니다.

1. toodisplay hello 스톰 UI, 웹 브라우저 toohttps://CLUSTERNAME.azurehdinsight.net/stormui를 엽니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.

    > [!NOTE]
    > 사용자 이름 및 암호 tooprovide 요청 되 면 hello 클러스터 관리자 (관리자) 및 때 사용한 암호를 입력 hello 클러스터를 생성 합니다.

2. 아래 **토폴로지 요약**선택, hello **wordcount** hello에 항목 **이름** 열입니다. Hello 토폴로지에 대 한 정보가 표시 됩니다.

    ![storm-starter WordCount 토폴로지 정보가 있는 Storm 대시보드.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    이 페이지에서는 hello를 다음 정보를 제공 합니다.

    * **토폴로지 통계** -hello 토폴로지 성능에 대 한 기본 정보가 시간 창으로 구성 합니다.

        > [!NOTE]
        > Hello 페이지의 다른 섹션에 표시 되는 정보에 대 한 특정 시간 창 변경 내용이 hello 시간 창을 선택 합니다.

    * **Spouts** -각 배출구에서 반환 된 hello 마지막 오류를 포함 하 여 spouts에 대 한 기본 정보입니다.

    * **Bolt** - Bolt에 대한 기본 정보입니다.

    * **토폴로지 구성** -hello 토폴로지 구성에 대 한 정보를 자세히 설명 합니다.

    이 페이지에는 hello 토폴로지에 수행 될 작업을 제공 합니다.

    * **활성화** - 비활성화된 토폴로지 처리를 다시 시작합니다.

    * **비활성화** - 실행 중인 토폴로지를 일시 중지합니다.

    * **균형을 다시 조정할** -hello 토폴로지의 hello 병렬 처리를 조정 합니다. 하면 해야 균형을 다시 조정 실행 중인 토폴로지 hello hello 클러스터의 노드 수를 변경한 후 합니다. Hello hello 클러스터의 노드 수 증가/감소에 대 한 병렬 처리 수준 toocompensate를 조정 리 밸런스 합니다. 자세한 내용은 참조 [스톰 토폴로지의 hello parallelism 이해](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)합니다.

    * **Kill** -hello 제한 시간을 지정한 후 스톰 토폴로지를 종료 합니다.

3. 이 페이지에서 hello에서 항목을 선택 **Spouts** 또는 **쐐기** 섹션. Hello 선택한 구성 요소에 대 한 정보가 표시 됩니다.

    ![선택한 구성 요소에 대한 정보가 있는 스톰 대시보드.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    이 페이지는 hello 다음 정보를 표시 합니다.

    * **Stats 배출구/볼트** -hello 구성 요소 성능에 대 한 기본 정보가 시간 창으로 구성 합니다.

        > [!NOTE]
        > Hello 페이지의 다른 섹션에 표시 되는 정보에 대 한 특정 시간 창 변경 내용이 hello 시간 창을 선택 합니다.

    * **Stats 입력** (볼트만)-hello 볼트에서 사용 하는 데이터를 생성 하는 구성 요소에 대 한 정보입니다.

    * **출력 통계** - 이 Bolt에서 내보낸 데이터에 대한 정보입니다.

    * **실행자** - 이 구성 요소의 인스턴스에 대한 정보입니다.

    * **오류** - 이 구성 요소에 의해 생성된 오류입니다.

4. 배출구 또는 번개 hello 세부 정보를 볼 때 hello에서 항목을 선택 **포트** 열 hello에 **Executor** hello 구성의 특정 인스턴스에 대 한 tooview 세부 정보 섹션.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    이 예제에서는 word hello **7** 1493957 번 발생 했습니다. 이 개수는 몇 번이이 토폴로지 시작 된 이후 hello word가 발생 했습니다.

## <a name="stop-hello-topology"></a>Hello 토폴로지를 중지 합니다.

Toohello 반환 **토폴로지 요약** hello 단어 개수 토폴로지에 대 한 페이지 선택한 후 hello **Kill** hello에서 단추 **토폴로지 작업** 섹션. 메시지가 표시 되 면 hello 토폴로지를 중지 하기 전에 10 초 toowait hello에 대 한 입력 합니다. Hello 제한 시간 이후 hello 토폴로지 더 이상 나타나지 않습니다 hello를 방문 하면 **스톰 UI** hello 대시보드의 섹션.

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a id="next"></a>다음 단계

Apache Storm이 자습서에서는 hello의 기본적인 사용 HDInsight의 Storm 알아보았습니다. 배우는 것이 너무 어떻게[Maven를 사용 하 여 개발 하는 Java 기반 토폴로지](hdinsight-storm-develop-java-topology.md)합니다.

이미 익숙한 Java 기반 토폴로지를 개발 하 고는 기존 토폴로지에 tooHDInsight toodeploy 원하는 참조 [배포 HDInsight의 Apache Storm 토폴로지를 관리할 및](hdinsight-storm-deploy-monitor-topology-linux.md)합니다.

.NET 개발자인 경우 Visual Studio를 사용하여 C# 또는 하이브리드 C#/Java 토폴로지를 만들 수 있습니다. 자세한 내용은 [Visual Studio용 Hadoop 도구를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.

HDInsight의 Storm 함께 사용할 수 있는 예제 토폴로지 예제 따르는 hello를 참조 하세요.

* [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
