---
title: "aaaUse HDInsight-Azure와 Ambari Tez 보기 | Microsoft Docs"
description: "Toouse hello Ambari Tez HDInsight의 toodebug Tez 작업을 표시 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Ambari 뷰 toodebug Tez 작업을 사용 하 여 HDInsight의

HDInsight에 대 한 웹 UI Ambari hello Tez를 사용 하는 사용 되는 toounderstand 및 디버그 작업이 될 수 있는 Tez 보기를 포함 합니다. hello Tez 보기가 있습니다 toovisualize hello 작업이 연결 된 항목에 대 한 그래프는 각 항목을 더 자세히 분석 하 고 통계 및 로깅 정보를 검색 합니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

* Linux 기반 HDInsight 클러스터입니다. 클러스터를 만드는 단계는 [Linux 기반 HDInsight 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.
* HTML5를 지원하는 최신 웹 브라우저

## <a name="understanding-tez"></a>Tez 이해

Tez는 기존의 MapReduce 처리보다 빠른 속도를 제공하는 Hadoop의 데이터 처리에 대해 확장 가능한 프레임워크입니다. Linux 기반 HDInsight 클러스터에 대 한 하이브 hello 기본 엔진입니다.

Tez 전달 된 비순환 그래프 (DAG) 작업에 필요한 작업의 hello 순서를 설명 하는 만듭니다. 개별 작업 꼭지점 라고 하며 실행 hello에 조각의 전체 작업 합니다. hello 꼭지점에서 설명 하는 hello 작업의 실제 실행 작업을 라고 및 hello 클러스터의 여러 노드에 배포할 수 있습니다.

### <a name="understanding-hello-tez-view"></a>이해 hello Tez 보기

hello Tez 보기는 실행 중인 프로세스에 기록 정보 및 정보 둘 다를 제공 합니다. 이 정보는 작업이 클러스터 사이에서 분산된 방식을 보여줍니다. 또한 작업 및 꼭지점에 사용 된 카운터를 표시 하 고 toohello 작업와 관련 된 오류 정보입니다. Hello 다음 시나리오에에서 유용한 정보를 제공할 수 있습니다.

* 장기 실행 프로세스, 보기 모니터링 hello 지도의 진행률 및 감소 작업 합니다.
* 실패 한 이유 또는 처리 개선할 수 있는 방법을 toolearn 성공 또는 실패 한 프로세스에 대 한 데이터를 분석 합니다.

## <a name="generate-a-dag"></a>DAG 생성

현재 실행 중인 되었거나 이전에 실행 된 하는 hello Tez 보기 데이터를 사용 하는 작업 hello Tez 엔진 경우만 포함 되어 있습니다. 간단한 Hive 쿼리는 Tez를 사용하지 않고도 확인할 수 있습니다. 필터링, 그룹화, 정렬, 조인 등을 수행하는 복잡한 쿼리는 hello Tez 엔진을 사용 합니다.

다음 단계 toorun Tez를 사용 하는 하이브 쿼리 hello를 사용 합니다.

1. 웹 브라우저에서 탐색 toohttps://CLUSTERNAME.azurehdinsight.net, 여기서 **CLUSTERNAME** HDInsight 클러스터의 hello 이름입니다.

2. Hello hello 페이지의 hello 위쪽 메뉴에서 선택 hello **뷰** 아이콘입니다. 이 아이콘은 여러 개의 사각형처럼 생겼습니다. 나타나는 hello 드롭다운 목록을 선택 **보기 하이브**합니다.

    ![Hive 뷰 선택](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. 로드 될 때 hello 하이브 뷰 붙여넣기 hello 다음 hello 쿼리 편집기에서 쿼리할을 클릭 한 다음 **실행**합니다.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Hello에 표시 하는 hello 출력이 표시 hello 작업이 완료 되 면 **쿼리 프로세스 결과** 섹션. hello 결과 텍스트 다음 비슷한 toohello 됩니다.

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. 선택 hello **로그** 탭 합니다. 정보 비슷한 toohello 텍스트 다음 표시 됩니다.

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Hello 저장 **앱 id** 값으로이 값은 hello 다음 섹션에 사용 됩니다.

## <a name="use-hello-tez-view"></a>Hello Tez 보기를 사용 하 여

1. Hello hello 페이지의 hello 위쪽 메뉴에서 선택 hello **뷰** 아이콘입니다. 나타나는 hello 드롭다운 목록을 선택 **Tez 보기**합니다.

    ![Tez 뷰 선택](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Hello Tez 보기 로드 되 면 hello 클러스터에서 현재 실행 중인 이거나 받아야 하는 하이브 쿼리 목록이 실행 볼 수 있습니다.

    ![모든 DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. 항목이 하나만 있는 경우 hello 이전 섹션에서를 실행 하는 hello 쿼리의입니다. 항목이 여러 개 있는 경우에 hello hello 페이지 위쪽에 hello 필드를 사용 하 여 검색할 수 있습니다.

4. 선택 hello **쿼리 ID** 하이브 쿼리에 대 한 합니다. Hello 쿼리 하는 방법에 대 한 정보가 표시 됩니다.

    ![DAG 세부 정보](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. 이 페이지에 hello 탭을 사용 하면 다음 정보는 tooview hello:

    * **세부 정보를 쿼리**: hello 하이브 쿼리 하는 방법에 대 한 세부 정보입니다.
    * **타임라인**: 각 처리 단계가 진행되는 데 걸린 시간에 대한 정보입니다.
    * **구성을**:이 쿼리에 사용 된 hello 구성 합니다.

    __쿼리 세부 정보__ hello에 대 한 hello 링크 toofind 정보를 사용할 수 있습니다 __응용 프로그램__ 또는 hello __DAG__ 이 쿼리에 대 한 합니다.
    
    * hello __응용 프로그램__ 링크 hello이이 쿼리에 대해 YARN 응용 프로그램에 대 한 정보를 표시 합니다. 여기에서 hello YARN 응용 프로그램 로그에 액세스할 수 있습니다.
    * hello __DAG__ 링크는이 쿼리에 대 한 지정된 된 비순환 그래프 hello에 대 한 정보를 표시 합니다. 여기에서 그래픽으로 나타낸 hello DAG 볼 수 있습니다. Hello 꼭지점 hello DAG에 대 한 정보를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이제 toouse hello Tez 보는 방법을 배웠습니다를 보다 자세히 배울에 대 한 [를 사용 하 여 HDInsight의 Hive](hdinsight-use-hive.md)합니다.

Tez 대 한 기술 정보를 자세한 참조 hello [Hortonworks Tez 페이지](http://hortonworks.com/hadoop/tez/)합니다.

Ambari HDInsight 사용에 대 한 자세한 내용은 참조 하세요. [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)
