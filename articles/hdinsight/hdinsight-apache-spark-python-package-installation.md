---
title: "aaaScript 작업-Python 설치 패키지를 Azure HDInsight의 Jupyter | Microsoft Docs"
description: "HDInsight Spark와 함께 사용할 수 있는 toouse 스크립트 동작 tooconfigure Jupyter 노트북 toouse 외부 python 패키지를 클러스터 하는 방법에 대해 단계별로 설명 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>스크립트 동작 tooinstall 외부 Python 패키지를 사용 하 여 HDInsight의 Apache Spark 클러스터에서 Jupyter 노트북에 대 한
> [!div class="op_single_selector"]
> * [셀 매직 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [스크립트 작업 사용](hdinsight-apache-spark-python-package-installation.md)
>
>

자세한 방법을 toouse 스크립트 동작 tooconfigure HDInsight (Linux) toouse 외부에는 Apache Spark 클러스터 커뮤니티 제공 **python** 하지 않은 패키지를 hello 클러스터에 기본적으로 포함 합니다.

> [!NOTE]
> 사용 하 여 Jupyter 노트북을 구성할 수도 있습니다 `%%configure` 매직 toouse 외부 패키지 합니다. 지침에 대해서는 [HDInsight의 Apache Spark 클러스터에서 Jupyter Notebook과 함께 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)을 참조하세요.
> 
> 

Hello를 검색할 수 있습니다 [패키지 인덱스](https://pypi.python.org/pypi) 사용할 수 있는 패키지의 전체 목록은 hello에 대 한 합니다. 다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다. 예를 들어 [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) 또는 [conda-forge](https://conda-forge.github.io/feedstocks.html)를 통해 제공되는 패키지를 설치할 수 있습니다.

이 문서에서는 살펴보겠습니다 방법을 tooinstall hello [TensorFlow](https://www.tensorflow.org/) Actoin 스크립트를 사용 하 여 클러스터에 패키지 하 고 hello Jupyter 노트북을 통해 사용 합니다.

## <a name="prerequisites"></a>필수 조건
Hello 다음이 필요 합니다.

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

   > [!NOTE]
   > Hdinsight Linux에 Spark 클러스터가 아직 없는 경우 클러스터를 만드는 동안 스크립트 작업을 실행할 수 있습니다. Hello 설명서 방문 [toouse 사용자 지정 스크립트 작업을 어떻게](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)합니다.
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Jupyter 노트북에서 외부 패키지 사용

1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.   

2. Hello Spark 클러스터 블레이드에서 클릭 **스크립트 동작** 아래 **사용**합니다. Hello hello 헤드 노드 및 hello 작업자 노드에 TensorFlow를 설치 하는 사용자 지정 작업을 실행 합니다. hello bash 스크립트에서 참조할 수 있습니다:에 대 한 방문을 hello 설명서 https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh [toouse 사용자 지정 스크립트 작업을 어떻게](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)합니다.

   > [!NOTE]
   > Hello 클러스터 설치는 두 개의 python 합니다. Spark hello Anaconda python 설치에 있는 사용할지 `/usr/bin/anaconda/bin`합니다. `/usr/bin/anaconda/bin/pip` 및 `/usr/bin/anaconda/bin/conda`를 통해 사용자 지정 작업에서 해당 설치 프로그램을 참조하세요.
   > 
   > 

3. PySpark Jupyter 노트북을 엽니다.

    ![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "새 Jupyter 노트북 만들기")

4. 새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다. Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.

    ![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")

5. 이제 `import tensorflow` 및 hello world 예제를 실행합니다. 

    코드 toocopy:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    hello 결과 다음과 같이 표시 됩니다.
    
    ![TensorFlow 코드 실행](./media/hdinsight-apache-spark-python-package-installation/execution.png "TensorFlow 코드 실행")



## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [HDInsight의 Apache Spark 클러스터에서 Jupyter 노트북과 함께 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
