---
title: "실행 Azure HDInsight의 Apache Spark aaaDebug 작업 | Microsoft Docs"
description: "작업 사용 하 여 YARN UI, Spark UI 및 Spark 기록 서버 tootrack 및 디버그 Azure HDInsight의 Spark 클러스터에서 실행 중인"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Azure HDInsight에서 실행 중인 Apache Spark 작업 디버그

이 문서에서 tootrack 및 디버그 멤버 hello YARN UI Spark UI를 사용 하 여 HDInsight 클러스터에서 실행 중인 작업 하 고 스파크 기록 서버 hello 방법을 배웁니다. 이 문서에 대 한 hello Spark 클러스터를 사용할 수 있는 노트북을 사용 하 여 Spark 작업을 시작 하겠습니다 **기계 학습: MLLib를 사용 하 여 음식 검사 데이터에서 예측 분석**합니다. Tootrack 제출한 다른 방법을 사용도를 사용 하 여 예를 들어 응용 프로그램 아래 hello 단계를 사용할 수 있습니다 **spark 제출**합니다.

## <a name="prerequisites"></a>필수 조건
Hello 다음이 필요 합니다.

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.
* Hello 노트북 실행를 시작한 해야  **[기계 학습: MLLib를 사용 하 여 음식 검사 데이터에서 예측 분석](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**합니다. 방법에 대 한 지침은 toorun이이 노트북 hello 링크를 수행 합니다.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Hello YARN UI에서에서 응용 프로그램 추적
1. Hello YARN UI를 시작 합니다. Hello 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **YARN**합니다.
   
    ![YARN UI 시작](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > 또는 hello Ambari UI에서에서 hello YARN UI를 시작할 수 있습니다. hello 클러스터 블레이드에서 toolaunch hello Ambari UI 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다. Ambari UI hello에서 클릭 **YARN**, 클릭 **빠른 링크**, hello 활성 리소스 관리자를 클릭 하 고 클릭 **ResourceManager UI**합니다.    
   > 
   > 
2. Hello 응용 프로그램에 hello 이름이 Jupyter 노트북을 사용 하 여 hello Spark 작업을 시작 했으므로 **remotesparkmagics** (이것이 hello 전자 필기장에서 시작 된 모든 응용 프로그램에 대 한 hello 이름). Hello 작업에 대 한 자세한 내용은 응용 프로그램 이름 tooget hello에 대 한 hello 응용 프로그램 ID를 클릭 합니다. Hello 응용 프로그램 보기를 시작합니다.
   
    ![Spark 응용 프로그램 ID 찾기](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Hello Jupyter 노트북에서 시작 하는 이러한 응용 프로그램에 대 한 hello 상태는 항상 **실행** hello 노트북 종료 될 때까지 합니다.
3. Hello 응용 프로그램 보기에서 hello 응용 프로그램 및 hello 로그 (stdout/stderr)와 관련 된 hello 컨테이너 아웃 toofind 추가로 드릴 수 있습니다. Hello 해당 toohello 링크를 클릭 하 여 hello Spark UI를 시작할 수도 있습니다 **추적 URL**다음과 같이 합니다. 
   
    ![컨테이너 로그 다운로드](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Hello Spark UI에서에서 응용 프로그램 추적
Spark UI hello에서 앞에서 시작 하는 hello 응용 프로그램에서 생성 하는 hello Spark 작업으로 다운 드릴 수 있습니다.

1. hello에 대 한 hello 링크를 클릭 하는 hello 응용 프로그램 보기에서 toolaunch hello Spark UI **추적 URL**위의 hello 화면 캡처에 나타난 것 처럼 합니다. Hello Jupyter 노트북에서 실행 되는 hello 응용 프로그램에 의해 실행 되는 모든 hello Spark 작업을 볼 수 있습니다.
   
    ![Spark 작업 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Hello 클릭 **Executor** toosee 처리 및 저장 각 실행 기에 대 한 정보를 탭 합니다. Hello를 클릭 하 여 hello 호출 스택을 검색할 수도 있습니다 **스레드 덤프** 링크 합니다.
   
    ![Spark 실행자 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Hello 클릭 **단계** hello 응용 프로그램과 관련 된 toosee hello 단계를 탭 합니다.
   
    ![Spark 단계 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    각 단계에서는 아래와 같이 실행 통계를 볼 수 있는 여러 작업이 있습니다.
   
    ![Spark 단계 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Hello 단계 세부 정보 페이지에서 DAG 시각화를 시작할 수 있습니다. Hello 확장 **DAG 시각화** 아래와 같이 hello hello 페이지 위쪽에 링크 합니다.
   
    ![Spark 단계 DAG 시각화 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG 또는 직접 Aclyic 그래프 hello hello 응용 프로그램에 다른 단계를 나타냅니다. Hello 그래프의 각 파랑 상자 hello 응용 프로그램에서 호출한 Spark 작업을 나타냅니다.
5. Hello 단계 세부 정보 페이지에서 hello 응용 프로그램 타임 라인 보기를 시작할 수 있습니다. Hello 확장 **이벤트 타임 라인** 아래와 같이 hello hello 페이지 위쪽에 링크 합니다.
   
    ![Spark 단계 이벤트 타임라인 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Hello Spark 이벤트 hello 시간대 형식으로 표시 됩니다. hello 시간 표시 막대 뷰는 사용할 수 있는 세 가지 수준에서 작업, 작업, 내에서, 단계 내에서 합니다. 위의 hello 이미지는 지정 된 단계에 대 한 hello 시간 표시 막대 뷰를 캡처합니다.
   
   > [!TIP]
   > Hello를 선택 하는 경우 **확대/축소를 사용 하도록 설정** 확인란을 스크롤할 수 왼쪽과 오른쪽 hello 타임 라인 보기.
   > 
   > 
6. Hello Spark UI에서에서 다른 탭도 hello Spark 인스턴스에 대 한 유용한 정보를 제공 합니다.
   
   * 저장소 탭-응용 프로그램 만들기는 RDDs hello 저장소 탭에 대 한 정보를 찾을 수 합니다.
   * 환경 탭-이 탭에서는 많은 hello 같은 Spark 인스턴스에 대 한 유용한 정보 
     * Scala 버전
     * Hello 클러스터와 연결 된 이벤트 로그 디렉터리
     * Hello 응용 프로그램에 대 한 실행자 코어 수
     * 등

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Spark 기록 서버 hello를 사용 하 여 완료 된 작업에 대 한 정보 찾기
작업이 완료 되 면 hello 작업에 대 한 hello 정보 Spark 기록 서버 hello에 유지 됩니다.

1. toolaunch hello Spark 기록 서버 hello 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Spark 기록 서버**합니다.
   
    ![Spark 기록 서버 시작](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > 또는 hello Ambari UI에서에서 hello Spark 기록 서버 UI를 시작할 수 있습니다. hello 클러스터 블레이드에서 toolaunch hello Ambari UI 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다. Hello Ambari UI에서에서 클릭 **Spark**, 클릭 **빠른 링크**, 클릭 하 고 **Spark 기록 서버 UI**합니다.
   > 
   > 
2. 나열 된 모든 완료 hello 응용 프로그램에 표시 됩니다. 자세한 내용은 응용 프로그램으로 아래로 응용 프로그램 ID toodrill를 클릭 합니다.
   
    ![Spark 기록 서버 시작](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>참고 항목
*  [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>데이터 분석가

* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석](hdinsight-spark-analyze-application-insight-logs.md)
* [분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Spark 개발자

* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


