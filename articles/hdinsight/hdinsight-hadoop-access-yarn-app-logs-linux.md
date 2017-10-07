---
title: "Linux 기반 HDInsight-Azure에 aaaAccess Hadoop YARN 응용 프로그램 로그온 | Microsoft Docs"
description: "Tooaccess YARN 응용 프로그램 명령줄 hello와 웹 브라우저를 사용 하는 Linux 기반 HDInsight (Hadoop) 클러스터에 로그온 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Linux 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스

Tooaccess Azure HDInsight의 Hadoop 클러스터의 YARN (아직 다른 리소스 협상 자) 응용 프로그램에 대 한 로그를 hello 하는 방법에 대해 알아봅니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="YARNTimelineServer"></a>YARN Timeline Server

hello [YARN 타임 라인 서버](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) 완성 된 응용 프로그램 및 두 가지 다른 인터페이스를 통해 응용 프로그램 프레임 워크 관련 정보에 대해 일반 정보를 제공 합니다. 구체적으로 살펴보면 다음과 같습니다.

* 3.1.1.374 이상 버전에서는 HDInsight 클러스터에서 제네릭 응용 프로그램 정보를 저장하고 검색할 수 있습니다.
* hello 프레임 워크 관련 응용 프로그램 타임 라인 서버 hello의 구성 요소 정보를 HDInsight 클러스터에서 현재 사용할 수 없는 경우

응용 프로그램에 대 한 일반 정보는 데이터의 형식 다음 hello를 포함 되어 있습니다.

* hello 응용 프로그램 ID, 응용 프로그램의 고유 식별자
* hello 응용 프로그램을 시작한 hello 사용자
* 시도에 정보 toocomplete hello 응용 프로그램 구성
* 시도 하는 특정된 응용 프로그램에서 사용 하는 hello 컨테이너

## <a name="YARNAppsAndLogs"></a>YARN 응용 프로그램 및 로그

YARN은 여러 프로그래밍 모델(예: MapReduce)을 지원하여 리소스 관리를 응용 프로그램 예약/모니터링과 분리합니다. YARN은 *리소스 관리자*(RM), 작업자 노드별 *노드 관리자*(NM) 및 응용 프로그램별 *응용 프로그램 마스터*(AM)를 사용합니다. hello 응용 프로그램별 AM 협상 리소스 (CPU, 메모리, 디스크, 네트워크) hello RM.로 응용 프로그램 실행 RM hello 작동 NMs toogrant으로 권한이 부여 된 이러한 리소스를 *컨테이너*합니다. hello AM는 hello RM. 하 여 hello 할당 된 컨테이너 tooit의 hello 진행률 추적 응용 프로그램에 많은 컨테이너 hello 응용 프로그램의 hello 특성에 따라 필요할 수 있습니다.

각 응용 프로그램은 여러 *응용 프로그램 시도*로 구성될 수 있습니다. 응용 프로그램이 실패할 경우 새 시도로 다시 시도할 수 있습니다. 각 시도는 하나의 컨테이너에서 실행됩니다. 즉, 컨테이너 YARN 응용 프로그램에 의해 수행 된 작업의 기본 단위에 대 한 hello 컨텍스트를 제공 합니다. 컨테이너의 hello 컨텍스트 내에서 수행 하는 모든 작업은 hello 단일 작업자 노드는 hello에 할당 된 컨테이너에서 수행 됩니다. 자세한 내용은 [YARN 개념][YARN-concepts]을 참조하세요.

응용 프로그램 로그 (및 연결 된 hello 컨테이너 로그)는 문제가 있는 Hadoop 응용 프로그램 디버깅에서 중요 합니다. 수집, 집계 및 hello 사용 하 여 응용 프로그램 로그를 저장 하기 위한 훌륭한 프레임 워크를 제공 하는 YARN [로그 집계] [ log-aggregation] 기능입니다. hello 로그 집계 기능을 사용 하면 응용 프로그램 로그에 액세스를 보다 명확히 구분 합니다. 이 기능은 작업자 노드의 모든 컨테이너에서 로그를 집계한 후 작업자 노드당 하나의 집계된 로그 파일로 저장합니다. 응용 프로그램이 완료 된 후 hello 로그 hello 기본 파일 시스템에 저장 됩니다. 응용 프로그램이 수백 또는 수천 개의 컨테이너를 사용할 수 있습니다 하지만 단일 작업자 노드에서 실행 되는 모든 컨테이너에 대 한 로그는 단일 파일 집계 tooa 항상. 따라서 응용 프로그램에서 사용하는 작업자 노드당 하나의 로그만 있습니다. 로그 집계는 HDInsight 클러스터 버전 3.0 이상에서 기본적으로 사용됩니다. 집계 된 로그는 hello 클러스터에 대 한 기본 저장소에 있습니다. 경로 따라 hello은 hello HDFS 경로 toohello 로그입니다.

    /app-logs/<user>/logs/<applicationId>

Hello 경로에 `user` hello hello 응용 프로그램을 시작한 hello 사용자 이름입니다. hello `applicationId` 는 hello YARN RM.로 hello 할당 된 고유 식별자 tooan 응용 프로그램

hello 집계 된 로그는 직접 읽을 수 있는 작성 된 대로 [TFile][T-file], [이진 형식] [ binary-format] 컨테이너에 의해 인덱싱됩니다. 이 로그 사용 하 여 hello YARN ResourceManager 기록 또는 CLI 도구 tooview 이러한 일반 텍스트로 응용 프로그램이 나 관심 있는 컨테이너에 대 한 합니다.

## <a name="yarn-cli-tools"></a>YARN CLI 도구

toouse hello YARN CLI 도구를 먼저 toohello HDInsight 클러스터 SSH를 사용 하 여 연결 해야 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

일반 텍스트로 hello 다음 명령 중 하나를 실행 하 여 이러한 로그를 볼 수 있습니다.

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Hello 지정 &lt;applicationId >, &lt;사용자-사용자-시작-응용 프로그램 >, &lt;containerId >, 및 &lt;작업자 노드 주소 > 이러한 명령을 실행 하는 경우 정보입니다.

## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager UI

hello YARN ResourceManager UI hello 클러스터 헤드 노드에에서 실행 됩니다. Hello Ambari web UI 통해 액세스 합니다. 사용 하 여 hello 단계 tooview hello YARN 다음 기록 합니다.

1. 웹 브라우저에서 toohttps://CLUSTERNAME.azurehdinsight.net 이동 합니다. CLUSTERNAME를 HDInsight 클러스터의 hello 이름을 바꿉니다.
2. Hello hello 왼쪽에 있는 서비스 목록에서 선택 **YARN**합니다.

    ![선택한 Yarn 서비스](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. Hello에서 **빠른 링크** 드롭다운에서 hello 클러스터 헤드 노드 중 하나를 선택 하 고 다음 선택 **ResourceManager 로그**합니다.

    ![Yarn 빠른 링크](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    링크 tooYARN 로그의 목록으로 표시 됩니다.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
