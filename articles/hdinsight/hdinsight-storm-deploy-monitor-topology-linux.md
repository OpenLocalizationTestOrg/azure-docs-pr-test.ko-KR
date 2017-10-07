---
title: "aaaDeploy 및 Linux 기반 HDInsight의 Apache Storm 토폴로지 관리 | Microsoft Docs"
description: "Toodeploy를 모니터링 하 고 hello 스톰 대시보드를 사용 하 여 Linux 기반 HDInsight의 Apache Storm 토폴로지를 관리 하는 방법에 대해 알아봅니다. Visual Studio용 Hadoop 도구를 사용합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>HDInsight에서 Apache Storm 토폴로지 배포 및 관리

이 문서에서 관리 및 모니터링 스톰에서 HDInsight 클러스터에서 실행 되는 스톰 토폴로지 hello 기본 사항에 알아봅니다.

> [!IMPORTANT]
> hello이 문서의 단계 필요 HDInsight 클러스터에서 Linux 기반 스톰 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. 
>
> Windows 기반 HDInsight에서 토폴로지의 배포 및 모니터링에 대한 정보는 [Windows 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>필수 조건

* **HDInsight 클러스터의 Linux 기반 Storm**: 클러스터를 만드는 단계는 [HDInsight에서 Apache Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md) 을 참조하세요.

* (선택 사항) **SSH 및 SCP의 기본적인 지식**: 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

* (선택 사항) **Visual Studio**: Azure SDK 2.5.1 나 최신 Visual Studio에 대 한 데이터 레이크 도구 hello 및 합니다. 자세한 내용은 [Data Lake Tools for Visual Studio 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.

    다음 버전의 Visual Studio hello 중 하나입니다.

  * Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015(모든 버전)

  * Visual Studio 2017(모든 버전) 데이터 레이크 Tools for Visual Studio 2017 hello Azure 작업의 일부로 설치 됩니다.

## <a name="submit-a-topology-visual-studio"></a>토폴로지 제출: Visual Studio

hello HDInsight 도구에 사용 되는 toosubmit C# 또는 하이브리드 토폴로지에 tooyour Storm 클러스터 될 수 있습니다. 샘플 응용 프로그램을 사용 하는 hello 단계를 수행 합니다. Hello HDInsight 도구를 사용 하 여 사용자 고유의 토폴로지를 만드는 방법은 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio에 대 한 개발 C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.

1. Visual Studio 용 hello 최신 버전의 hello 데이터 레이크 도구를 아직 설치 하지 있을 경우 참조 [데이터 레이크 도구를 사용 하 여 Visual Studio 용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.

    > [!NOTE]
    > hello 데이터 레이크 Tools for Visual Studio는 Visual Studio에 대 한 hello HDInsight 도구 호출 이전 되었습니다.
    >
    > 데이터 레이크 Tools for Visual Studio hello에 포함 된 __Azure 작업__ Visual Studio 2017에 대 한 합니다.

2. Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.

3. Hello에 **새 프로젝트** 대화 상자에서 **설치 됨** > **템플릿**를 선택한 후 **HDInsight**합니다. Hello 템플릿 목록에서 선택 **스톰 샘플**합니다. Hello 대화 상자의 hello 아래쪽 hello 응용 프로그램에 대 한 이름을 입력 합니다.

    ![이미지](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. **솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **HDInsight의 tooStorm 제출**합니다.

   > [!NOTE]
   > 메시지가 표시 되 면 Azure 구독에 대 한 hello 로그인 자격 증명을 입력 합니다. 구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.

5. Hello에서 HDInsight 클러스터에서 프로그램 스톰 선택 **Storm 클러스터** 드롭 다운 목록에서 선택한 후 **전송**합니다. Hello 제출은 hello를 사용 하 여 성공 여부를 모니터링할 수 있습니다 **출력** 창.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>토폴로지 전송: SSH 및 hello 스톰 명령

1. SSH tooconnect toohello HDInsight 클러스터를 사용 합니다. 대체 **USERNAME** hello 이름 SSH 로그인입니다. **CLUSTERNAME** 을 HDInsight 클러스터 이름으로 바꿉니다.

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    클러스터 SSH tooconnect tooyour HDInsight를 사용 하 여 대 한 자세한 내용은 참조 하십시오. [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

2. 다음 명령 예제에서는 토폴로지 toostart hello를 사용 합니다.

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    이 명령은 hello 클러스터에서 hello WordCount 토폴로지 예제를 시작합니다. 이 토폴로지는 임의로 hello 문장에서 문장을 하 고 각 단어 hello 발생 횟수를 생성 합니다.

   > [!NOTE]
   > Hello를 사용 하기 전에 hello 클러스터를 포함 하는 hello jar 파일을 먼저 복사 해야 toohello 클러스터 토폴로지를 전송할 때 `storm` 명령입니다. toocopy hello 파일 toohello 클러스터 hello를 사용할 수 있습니다 `scp` 명령입니다. 예를 들어 `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > hello WordCount 예제 및 기타 스톰 시작 예제에서 클러스터에 이미 포함 되어 `/usr/hdp/current/storm-client/contrib/storm-starter/`합니다.

## <a name="submit-a-topology-programmatically"></a>토폴로지 제출: 프로그래밍 방식으로

Hello 클러스터에서 호스팅되는 Nimbus 서비스와 통신 하 여 HDInsight의 토폴로지 tooStorm를 프로그래밍 방식으로 배포할 수 있습니다. [https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) 보여 주는 Java 응용 프로그램 예제를 제공 방법을 toodeploy hello Nimbus 서비스를 통해 토폴로지를 시작 합니다.

## <a name="monitor-and-manage-visual-studio"></a>모니터링 및 관리: Visual Studio

토폴로지가 제출 될 때 성공적으로 Visual Studio를 사용 하 여, hello **스톰 토폴로지** 보기 hello 클러스터 나타납니다. 토폴로지를 실행 하는 hello에 대 한 hello 목록 tooview 정보에서 hello 토폴로지를 선택 합니다.

![VISUAL STUDIO 모니터](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> **Azure** > **HDInsight**를 확장한 다음 HDInsight의 Storm 클러스터를 마우스 오른쪽 단추로 클릭하고 **Storm 토폴로지 보기**를 선택하여 **서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.

Hello spouts 또는 쐐기 이러한 구성 요소에 대 한 tooview 정보에 대 한 hello 셰이프를 선택 합니다. 선택한 각 항목에 대해 새 창이 열립니다.

### <a name="deactivate-and-reactivate"></a>비활성화 및 다시 활성화

토폴로지를 비활성화하면 작업을 중단하거나 다시 활성화할 때까지 일시 중지합니다. tooperform 이러한 작업을 사용 하 여 hello __비활성화__ 및 __다시 활성화__ hello hello 위쪽에 단추 __토폴로지 요약__합니다.

### <a name="rebalance"></a>균형 재조정

한 토폴로지를 리 밸런스 hello 시스템 toorevise hello의 병렬 처리 수준이 hello 토폴로지 수 있습니다. 예를 들어, 크기를 조정 했습니다 hello 클러스터 tooadd 메모를 더 이상를 리 밸런스 하면 구성 토폴로지 toosee hello 새 노드 합니다.

toorebalance 토폴로지를 사용 하 여 hello __균형을 다시 조정할__ hello hello 위쪽에 단추 __토폴로지 요약__합니다.

> [!WARNING]
> 먼저 토폴로지를 리 밸런스 hello 토폴로지를 비활성화 한 다음 hello 클러스터 전체에서 균등 하 게 작업자를 재배포 하 다음 마지막으로 hello 토폴로지 toohello의 상태로 작업 재 분산 발생 하기 전에 반환 합니다. 따라서 hello 토폴로지를 활성화 한 경우 그 다시 활성화 됩니다. 비활성화되어 있다면 비활성화된 상태를 유지합니다.

### <a name="kill-a-topology"></a>토폴로지 종료

Storm 토폴로지는 중지 하거나 hello 클러스터를 삭제할 때까지 실행을 계속 합니다. toostop 토폴로지를 사용 하 여 hello __Kill__ hello hello 위쪽에 단추 __토폴로지 요약__합니다.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>모니터링 및 관리: SSH 및 hello 스톰 명령

hello `storm` 유틸리티 토폴로지 hello 명령줄에서 실행 된 toowork을 수 있습니다. 전체 명령 목록에는 `storm -h` 를 사용합니다.

### <a name="list-topologies"></a>목록 토폴로지

모든 실행 중인 토폴로지에 명령 toolist 다음 hello를 사용 합니다.

    storm list

이 명령은 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>비활성화 및 다시 활성화

토폴로지를 비활성화하면 작업을 중단하거나 다시 활성화할 때까지 일시 중지합니다. 다음 명령은 toodeactivate hello를 사용 하 고 다시 활성화:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>실행 중인 토폴로지를 중단합니다.

Storm 토폴로지가 일단 시작되면 중지될 때까지 계속 실행됩니다. toostop 토폴로지에서 다음 명령을 사용 하 여 hello:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>균형 재조정

한 토폴로지를 리 밸런스 hello 시스템 toorevise hello의 병렬 처리 수준이 hello 토폴로지 수 있습니다. 예를 들어, 크기를 조정 했습니다 hello 클러스터 tooadd 메모를 더 이상를 리 밸런스 하면 구성 토폴로지 toosee hello 새 노드 합니다.

> [!WARNING]
> 먼저 토폴로지를 리 밸런스 hello 토폴로지를 비활성화 한 다음 hello 클러스터 전체에서 균등 하 게 작업자를 재배포 하 다음 마지막으로 hello 토폴로지 toohello의 상태로 작업 재 분산 발생 하기 전에 반환 합니다. 따라서 hello 토폴로지를 활성화 한 경우 그 다시 활성화 됩니다. 비활성화되어 있다면 비활성화된 상태를 유지합니다.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>모니터링 및 관리: Storm UI

hello 스톰 UI 작업 토폴로지, 실행을 위한 웹 인터페이스를 제공 하 고 HDInsight 클러스터에 포함 됩니다. tooview hello 스톰 UI를 사용 하 여 웹 브라우저 tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**여기서 **CLUSTERNAME** hello 클러스터 이름입니다.

> [!NOTE]
> 사용자 이름 및 암호 tooprovide 요청 되 면 hello 클러스터 관리자 (관리자) 및 때 사용한 암호를 입력 hello 클러스터를 생성 합니다.

### <a name="main-page"></a>기본 페이지

hello 스톰 UI의 기본 페이지 hello hello를 다음 정보를 제공 합니다.

* **클러스터 요약**: hello Storm 클러스터에 대 한 기본 정보입니다.
* **토폴로지 요약**: 실행 중인 토폴로지 목록입니다. 자세한 내용은이 섹션 tooview의 hello 링크 사용 하 여 특정 토폴로지에 대 한 합니다.
* **요약 감독자**: hello 스톰 감독자에 대 한 정보입니다.
* **Nimbus 구성**: hello 클러스터에 대 한 Nimbus 구성 합니다.

### <a name="topology-summary"></a>토폴로지 요약

Hello에서 링크를 선택 하면 **토폴로지 요약** hello hello 토폴로지에 대 한 정보를 다음 섹션에 표시 됩니다.

* **토폴로지 요약**: hello 토폴로지에 대 한 기본 정보입니다.
* **토폴로지 작업**: hello 토폴로지에 대해 수행할 수 있는 관리 작업입니다.

  * **활성화**- 비활성화된 토폴로지 처리를 다시 시작합니다.
  * **비활성화**- 실행 중인 토폴로지를 일시 중지합니다.
  * **균형을 다시 조정할**: hello 토폴로지의 hello 병렬 처리를 조정 합니다. 하면 해야 균형을 다시 조정 실행 중인 토폴로지 hello hello 클러스터의 노드 수를 변경한 후 합니다. 이 작업에는 hello에 대 한 hello 토폴로지 tooadjust 병렬 처리 수준 toocompensate hello 클러스터의 노드 수가 늘어나거나 수 있습니다.

    자세한 내용은 참조 <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">스톰 토폴로지의 hello parallelism 이해</a>합니다.
  * **Kill**: hello 제한 시간을 지정한 후 스톰 토폴로지를 종료 합니다.
* **토폴로지 통계**: hello 토폴로지에 대 한 통계입니다. tooset hello hello 페이지에 항목이 남아 있는 hello에 대 한 시간 범위, hello 링크를 사용 하 여 hello에 **창** 열입니다.
* **Spouts**: hello spouts hello 토폴로지에서 사용 합니다. 특정 spouts에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.
* **쐐기**: hello 볼트 hello 토폴로지에서 사용 합니다. 특정 볼트에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.
* **토폴로지 구성**: 선택한 hello 토폴로지의 hello 구성 합니다.

### <a name="spout-and-bolt-summary"></a>Spout 및 Bolt 요약

배출구 hello에서 선택 하면 **Spouts** 또는 **쐐기** hello 다음 hello 선택 항목에 대 한 정보를 표시 하는 섹션:

* **구성 요소 요약**: hello 배출구 또는 번개에 대 한 기본 정보입니다.
* **Stats 배출구/볼트**: hello에 대 한 통계 spout 또는 볼트 합니다. tooset hello hello 페이지에 항목이 남아 있는 hello에 대 한 시간 범위, hello 링크를 사용 하 여 hello에 **창** 열입니다.
* **Stats 입력** (볼트): hello에 대 한 정보 입력 스트림을 hello 볼트에서 사용 합니다.
* **통계를 출력**:이에서 내보내는 hello 스트림에 대 한 정보 spout 또는 볼트 합니다.
* **단일 실행**: hello 배출구 또는 볼트의 인스턴스를 hello에 대 한 정보입니다. 선택 hello **포트** 이 인스턴스에 대 한 특정 실행자 tooview에 대 한 항목 진단 정보에 대 한 로그를 생성 합니다.
* **오류**: 이 Spout 또는 Bolt에 대한 오류 정보입니다.

## <a name="monitor-and-manage-rest-api"></a>모니터링 및 관리: REST API

hello 스톰 UI 비슷한 관리 및 모니터링 기능 hello REST API를 사용 하 여 수행할 수 있도록 hello REST API를 기반으로 만들어집니다. 관리 및 모니터링 스톰 토폴로지 hello REST API toocreate 사용자 지정 도구를 사용할 수 있습니다.

자세한 내용은 [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html)를 참조하세요. hello 다음 정보는 특정 toousing hello HDInsight의 Apache Storm를 사용 하 여 REST API입니다.

> [!IMPORTANT]
> hello 스톰 REST API를 공개적으로 사용할 수 없는 이상 인터넷 hello 및에서 SSH 터널 toohello HDInsight 클러스터 헤드 노드를 사용 하 여 액세스 해야 합니다. 만들고 SSH 터널을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [사용 하 여 SSH 터널링 tooaccess Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie, 및 기타 웹 Ui](hdinsight-linux-ambari-ssh-tunnel.md)합니다.

### <a name="base-uri"></a>기본 URI

hello hello REST API는 Linux 기반 HDInsight 클러스터에 대 한 기본 URI에 있는 hello에 헤드 노드 **https://HEADNODEFQDN:8744/api/v1/**합니다. hello 도메인 hello 헤드 노드의 이름에 클러스터를 만드는 동안 생성 되 고 static이 아닙니다.

여러 가지 방법으로 hello hello 클러스터 헤드 노드에 대 한 정규화 된 도메인 이름 (FQDN)을 찾을 수 있습니다.

* **한 SSH 세션에서**: hello 명령을 사용 하 여 `headnode -f` SSH 세션 toohello 클러스터에서 합니다.
* **Ambari Web에서**: 선택 **서비스** hello hello 페이지의 위쪽에서 선택 **스톰**합니다. Hello에서 **요약** 탭에서 **스톰 UI 서버**합니다. hello hello 페이지 위쪽에 hello hello 스톰 UI 및 REST API를 실행 하는 hello 노드의 FQDN입니다.
* **Ambari REST API에서**: hello 명령을 사용 하 여 `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` 스톰 UI 및 REST API hello hello 노드에 대 한 tooretrieve 정보에서 실행 되 고 있습니다. 대체 **암호** hello 클러스터에 대 한 hello 관리자 암호를 사용 합니다. 대체 **CLUSTERNAME** hello 클러스터 이름을 사용 합니다. Hello 응답 hello "host_name" 항목 hello hello 노드의 FQDN을 포함합니다.

### <a name="authentication"></a>인증

REST API를 사용 해야 하는 요청 toohello **기본 인증**이므로 hello HDInsight 클러스터 관리자 이름 및 암호를 사용 합니다.

> [!NOTE]
> 일반 텍스트를 사용 하 여 기본 인증 보내지므로 해야 **항상** hello 클러스터와 toosecure HTTPS 통신을 사용 합니다.

### <a name="return-values"></a>반환 값

REST API만 hello 클러스터 내에서 사용할 수 있습니다 또는 가상 컴퓨터에 hello 클러스터와 동일한 Azure 가상 네트워크를 환영 hello에서 반환 되는 정보입니다. 예를 들어 hello 정규화 된 도메인 이름 (FQDN) 사육 서버에 대해 반환 되는 hello 인터넷에서에서 액세스할 수 없습니다.

## <a name="next-steps"></a>다음 단계

이제 toodeploy / 모니터 토폴로지를 사용 하 여 스톰 대시보드 hello 하는 방법을 배운, 자세히 배울 방법 너무[Maven를 사용 하 여 개발 하는 Java 기반 토폴로지](hdinsight-storm-develop-java-topology.md)합니다.

추가 예제 토폴로지 목록은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.
