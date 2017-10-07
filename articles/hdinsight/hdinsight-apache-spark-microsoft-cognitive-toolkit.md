---
title: "심층 학습에 대 한 Azure HDInsight spark Cognitive Toolkit aaaMicrosoft | Microsoft Docs"
description: "알아봅니다 방법는 숙련 된 Microsoft Cognitive 도구 키트 심층 학습 모델에는 Azure HDInsight Spark 클러스터에 hello Spark Python API를 사용 하 여 적용 된 tooa dataset 될 수 있습니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Azure HDInsight Spark 클러스터에서 Microsoft Cognitive 도구 키트 심층 학습 모델 사용

이 문서에서는 다음 단계 hello 수행 있습니다.

1. Azure HDInsight Spark 클러스터에서 사용자 지정 스크립트 tooinstall Microsoft Cognitive 도구 키트를 실행 합니다.

2. Jupyter 노트북 toohello Spark 클러스터 toosee을 어떻게 업로드는 숙련 된 Microsoft Cognitive 도구 키트 학습 hello를 사용 하 여 Azure Blob 저장소 계정에 모델 toofiles 심층 tooapply [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>필수 조건

* **Azure 구독** - 이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다. [지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free)를 참조하세요.

* **Azure HDInsight Spark 클러스터** - 이 문서에서는 Spark 2.0 클러스터를 만듭니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="how-does-this-solution-flow"></a>이 솔루션을 전달하는 방법

이 솔루션은 이 문서와 이 자습서의 일부로 업로드하는 Jupyter 노트북으로 분할되어 있습니다. 이 문서의 단계를 수행 하는 hello를 완료 합니다.

* Tooinstall Microsoft Cognitive Toolkit 및 Python 패키지 HDInsight Spark 클러스터에서 스크립트 작업을 실행 합니다.
* Hello 솔루션 toohello HDInsight Spark 클러스터를 실행 하는 hello Jupyter 노트북을 업로드 합니다.

hello 다음 나머지 단계에에서 설명 되어 hello Jupyter 노트북 합니다.

- Spark RDD(Resilient Distributed Dataset)에 샘플 이미지 로드
   - 모듈 로드 및 사전 설정 정의
   - Hello Spark 클러스터에서 로컬로 hello 데이터 집합 다운로드
   - RDD hello 데이터 집합 변환
- 그러면 Cognitive 도구 키트를 사용 하 여 hello 이미지 점수를 매깁니다.
   - 학습 hello Cognitive Toolkit 모델 toohello Spark 클러스터를 다운로드 합니다.
   - 작업자 노드에서 사용 하는 함수 toobe 정의
   - 작업자 노드 점수 hello 이미지
   - 모델 정확도 평가


## <a name="install-microsoft-cognitive-toolkit"></a>Microsoft Cognitive 도구 키트 설치

스크립트 동작을 사용하여 Spark 클러스터에 Microsoft Cognitive 도구 키트를 설치할 수 있습니다. 기본적으로 사용할 수 없는 hello 클러스터에서 사용자 지정 스크립트 tooinstall 구성 요소를 사용 하는 스크립트 동작 합니다. HDInsight.NET SDK를 사용 하 여 또는 Azure PowerShell을 사용 하 여 hello hello Azure 포털에서에서 사용자 지정 스크립트를 사용할 수 있습니다. 또한 hello 스크립트 tooinstall hello 도구 키트를 hello 클러스터가 실행 되 고 후 또는 클러스터 만들기의 일부로 사용할 수 있습니다. 

이 문서에서는 hello 클러스터를 만든 후 hello 포털 tooinstall hello 도구 키트를 사용 합니다. 다른 방법으로 toorun hello 사용자 지정 스크립트를 참조 하십시오. [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md)합니다.

### <a name="using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여

Toouse hello Azure 포털 toorun 작업을 스크립팅 하는 방법에 지침은 [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)합니다. 다음 입력 tooinstall Microsoft Cognitive Toolkit hello를 제공 하는지 확인 합니다.

* 스크립트 작업 이름이 hello에 대 한 값을 제공 합니다.

* **Bash 스크립트 URI**의 경우 `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`를 입력합니다.

* 헤드 노드와 작업자 노드 hello에 대해서만 hello 스크립트를 실행 하 고 다른 확인란의 선택 모든 hello 선택을 취소 해야 합니다.

* **만들기**를 클릭합니다.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Hello Jupyter 노트북 tooAzure HDInsight Spark 클러스터를 업로드 합니다.

toouse hello Microsoft Cognitive Toolkit hello Azure HDInsight Spark 클러스터와 hello Jupyter 노트북을 로드 해야 **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark 클러스터입니다. 이 노트북은 GitHub의 [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)에서 사용할 수 있습니다.

1. 복제 hello GitHub 리포지토리 [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)합니다. 지침 tooclone 참조 [리포지토리 복제](https://help.github.com/articles/cloning-a-repository/)합니다.

2. Hello Azure 포털에서에서 이미 클릭 클라우드를 프로 비전 하는 hello Spark 클러스터 블레이드를 여세요 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다.

    Toohello URL을 이동 하 여 hello Jupyter 노트북을 시작할 수도 있습니다 `https://<clustername>.azurehdinsight.net/jupyter/`합니다. 대체 \<clustername > HDInsight 클러스터의 hello 이름의 합니다.

3. Hello Jupyter 노트북에서 클릭 **업로드** 에 오른쪽 위 모퉁이 hello 이동한 후 toohello 위치 hello GitHub 리포지토리를 복제 합니다.

    ![Jupyter 노트북 tooAzure HDInsight Spark 클러스터 업로드](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "업로드 Jupyter 노트북 tooAzure HDInsight Spark 클러스터")

4. **업로드**를 다시 클릭합니다.

5. Hello 노트북을 업로드 한 후 hello 전자 필기장의 hello 이름을 클릭 한 다음 tooload 데이터 집합을 hello 하 고 hello 자습서를 수행 하는 방법에 자체 hello 전자 필기장의 hello 지시를 따릅니다.

## <a name="see-also"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
