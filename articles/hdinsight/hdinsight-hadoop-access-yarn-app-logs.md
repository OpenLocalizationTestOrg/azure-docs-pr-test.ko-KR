---
title: "aaaAccess Hadoop YARN 응용 프로그램 로그-프로그래밍 방식으로 Azure | Microsoft Docs"
description: "HDInsight의 Hadoop 클러스터에서 프로그래밍 방식으로 응용 프로그램 로그에 액세스합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Windows 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스
이 항목에서는 tooaccess 않았기 때문에 Azure HDInsight의 Hadoop Windows 기반 클러스터에서 YARN (아직 다른 리소스 협상 자) 응용 프로그램에 대 한 로그를 hello 하는 방법을 설명합니다

> [!IMPORTANT]
> 이 문서에 hello 정보에는 HDInsight 클러스터 tooWindows 기반만 적용 됩니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. Linux 기반 HDInsight 클러스터에서 YARN 로그 액세스에 대한 정보는 [HDInsight의 Linux 기반 Hadoop에 대한 YARN 응용 프로그램 로그 액세스](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>필수 조건
* Windows 기반 HDInsight 클러스터입니다.  [HDInsight에서 Windows 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

## <a name="yarn-timeline-server"></a>YARN Timeline Server
hello <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN 타임 라인 서버</a> 도 같이 프레임 워크 관련 응용 프로그램 정보 두 가지 다른 인터페이스를 통해 완성 된 응용 프로그램에 일반 정보를 제공 합니다. 구체적으로 살펴보면 다음과 같습니다.

* 3.1.1.374 이상 버전에서는 HDInsight 클러스터에서 제네릭 응용 프로그램 정보를 저장하고 검색할 수 있습니다.
* hello 프레임 워크 관련 응용 프로그램 타임 라인 서버 hello의 구성 요소 정보를 HDInsight 클러스터에서 현재 사용할 수 없는 경우

응용 프로그램에 대 한 일반 정보는 hello 다음 종류의 데이터에 포함 됩니다.

* hello 응용 프로그램 ID, 응용 프로그램의 고유 식별자
* hello 응용 프로그램을 시작한 hello 사용자
* 시도에 정보 toocomplete hello 응용 프로그램 구성
* 시도 하는 특정된 응용 프로그램에서 사용 하는 hello 컨테이너

HDInsight 클러스터에서이 정보는 hello 기본 컨테이너의 기본 Azure 저장소 계정에서 Azure 리소스 관리자 tooa 기록 저장소에 저장 됩니다. 완료된 응용 프로그램에 대한 이 제네릭 데이터는 REST API를 통해 검색할 수 있습니다.

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>YARN 응용 프로그램 및 로그
YARN은 여러 프로그래밍 모델(예: MapReduce)을 지원하여 리소스 관리를 응용 프로그램 예약/모니터링과 분리합니다. 이는 전역 *리소스 관리자*(RM), 작업자 노드별 *노드 관리자*(NM) 및 응용 프로그램별 *응용 프로그램 마스터*(AM)를 통해 이루어집니다. hello 응용 프로그램별 AM 협상 리소스 (CPU, 메모리, 디스크, 네트워크) hello RM.로 응용 프로그램 실행 RM hello 작동 NMs toogrant으로 권한이 부여 된 이러한 리소스를 *컨테이너*합니다. hello AM는 hello RM. 하 여 hello 할당 된 컨테이너 tooit의 hello 진행률 추적 응용 프로그램에 많은 컨테이너 hello 응용 프로그램의 hello 특성에 따라 필요할 수 있습니다.

각 응용 프로그램의 여러 구성 될 수 있습니다 또한 *응용 프로그램 횟수* 순서 toofinish 크래시 또는 AM 간 통신의 toohello 손실 인해 hello 현재 상태에 RM. 및 따라서 컨테이너 응용 프로그램의 특정 시도 tooa 부여 됩니다. 관점에서 컨테이너 YARN 응용 프로그램에 의해 수행 된 작업의 기본 단위에 대 한 hello 컨텍스트를 제공 하 고 hello 단일 작업자 노드는 hello에 할당 된 컨테이너에 컨테이너의 hello 컨텍스트 내에서 수행 하는 모든 작업 수행 됩니다. 자세한 내용은 [YARN 개념][YARN-concepts]을 참조하세요.

응용 프로그램 로그 (및 연결 된 hello 컨테이너 로그)는 문제가 있는 Hadoop 응용 프로그램 디버깅에서 중요 합니다. 수집, 집계 및 hello 사용 하 여 응용 프로그램 로그를 저장 하기 위한 훌륭한 프레임 워크를 제공 하는 YARN [로그 집계] [ log-aggregation] 기능입니다. hello 로그 집계 기능을 사용 하면 응용 프로그램 로그에 액세스 보다 명확한 작업자 노드에 대 한 모든 컨테이너에서 로그를 집계 하 고 응용 프로그램을 완료 한 후 집계 된 로그 파일 작성 단위 작업자 노드 hello 기본 파일 시스템에로 저장 합니다. 응용 프로그램이 수백 또는 수천 개의 컨테이너를 사용할 수 있습니다 되지만 단일 작업자 노드에서 실행 되는 모든 컨테이너에 대 한 로그 항상 됩니다 집계 tooa 단일를 파일, 응용 프로그램에서 사용 하는 작업자 노드 당 하나의 로그 파일이 생성 합니다. 로그를 집계 하는 HDInsight 클러스터에는 기본적으로 사용 됩니다 (버전 3.0 이상), 및 hello 수정할 수 있는 위치에 클러스터의 hello 기본 컨테이너에서 집계 된 로그를 볼 수 있습니다.

    wasb:///app-logs/<user>/logs/<applicationId>

해당 위치에 *사용자* hello 응용 프로그램을 시작한 hello 사용자의 hello 이름인 및 *applicationId* hello YARN RM.가 할당는 응용 프로그램의 고유 식별자 hello

hello 집계 된 로그는 직접 읽을 수 있는 작성 된 대로 [TFile][T-file], [이진 형식] [ binary-format] 컨테이너에 의해 인덱싱됩니다. YARN 제공 CLI 도구 toodump 이러한 로그 일반 텍스트로 응용 프로그램 또는 관심 있는 컨테이너에 대 한 합니다. 일반 텍스트로 hello tooit RDP를 통해 연결) (이후 hello 클러스터 노드에서 직접 YARN 명령이 다음 중 하나를 실행 하 여 이러한 로그를 볼 수 있습니다.

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager UI
hello YARN ResourceManager UI hello 클러스터 헤드 노드에에서 실행 되 고 hello Azure 포털 대시보드를 통해 액세스할 수 있습니다.

1. 역시 로그인[Azure 포털](https://portal.azure.com/)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **찾아보기**, 클릭 **HDInsight 클러스터**를 tooaccess hello YARN 응용 프로그램 로그를 지정 하는 Windows 기반 클러스터를 클릭 합니다.
3. Hello 상단 메뉴에서 클릭 **대시보드**합니다. **HDInsight 쿼리 콘솔**이라는 새 브라우저 탭에 페이지가 열립니다.
4. **HDInsight 쿼리 콘솔**에서 **Yarn UI**를 클릭합니다.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
