---
title: "로컬로 aaaInstall Jupyter & tooan Azure HDInsight Spark 클러스터에 연결 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall Jupyter 노트북 컴퓨터에 로컬로 Azure HDInsight의 Apache Spark 클러스터 tooan 연결 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Jupyter 노트북 컴퓨터에 설치 하 고 tooApache HDInsight의 Spark를 연결 합니다.

이 문서에서는 설명 어떻게 hello로 tooinstall Jupyter 노트북 (Python)에 대 한 사용자 지정 PySpark 및 매직, 멤버 및 hello 노트북 tooan HDInsight 클러스터에 연결을 사용 하는 (Scala) 용 Spark 커널을 합니다. 다양 한 이유로 tooinstall Jupyter 로컬 컴퓨터에 있을 수 있으며 다른 문제가 발생할 수 있습니다. 이 대 한 자세한에 대 한 hello 섹션을 참조 [내 컴퓨터에서에 Jupyter 설치 해야 이유](#why-should-i-install-jupyter-on-my-computer) hello이이 문서의 뒷부분에 있습니다.

Jupyter 및 hello Spark 매직 컴퓨터에 설치에 관련 된 세 가지 주요 단계가 있습니다.

* Jupyter 노트북 설치
* Spark 매직 hello로 PySpark hello 및 Spark 커널 설치
* HDInsight의 Spark 매직 tooaccess Spark 클러스터를 구성 합니다.

사용자 지정 커널 hello 및 HDInsight 클러스터와 Jupyter 노트북에 사용할 수 있는 hello Spark 매직에 대 한 자세한 내용은 참조 [HDInsight의 Apache Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 클러스터](hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.

## <a name="prerequisites"></a>필수 조건
여기에 나열 된 hello 필수 Jupyter 설치를 위한 않습니다. 이들은 연결 hello Jupyter 노트북 tooan HDInsight 클러스터에 대 한 hello 노트북에 설치 되 면입니다.

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="install-jupyter-notebook-on-your-computer"></a>컴퓨터에 Jupyter 노트북 설치

Jupyter 노트북을 설치하려면 먼저 Python을 설치해야 합니다. Python 및 Jupyter 둘 다 사용할 수 있는 hello의 일부로 [Anaconda 배포](https://www.continuum.io/downloads)합니다. Anaconda를 설치할 때 Python 배포를 설치하게 됩니다. Anaconda가 설치 되 면 적절 한 명령을 실행 하 여 hello Jupyter 설치를 추가 합니다.

1. Hello 다운로드 [Anaconda installer](https://www.continuum.io/downloads) 플랫폼과 실행된 hello 설치에 대 한 합니다. Hello 설치 마법사를 실행 하는 동안 hello 옵션 tooadd Anaconda tooyour 경로 변수를 선택 했는지 확인 합니다.
2. 다음 명령은 tooinstall Jupyter hello를 실행 합니다.

        conda install jupyter

    Jupyter 설치에 대한 자세한 내용은 [Anaconda를 사용하여 Jupyter 설치](http://jupyter.readthedocs.io/en/latest/install.html)를 참조하세요.

## <a name="install-hello-kernels-and-spark-magic"></a>Hello 커널 및 Spark 매직 설치

Tooinstall hello Spark 매직, PySpark hello 및 Spark 커널 hello hello 설치 지침을 따라 방법에 대 한 지침은 [sparkmagic 설명서](https://github.com/jupyter-incubator/sparkmagic#installation) GitHub에서 합니다. hello 첫 번째 hello Spark 매직 설명서의 단계 tooinstall Spark 매직 합니다. Hello 링크의 첫 번째 단계에 명령에 연결 하는 hello HDInsight 클러스터의 hello 버전에 따라 다음 hello로 대체 합니다. 그 후 hello 남은 hello Spark 매직 설명서에 나와 있는 단계를 따릅니다. Tooinstall hello 다른 커널 원한다 면 hello Spark 매직 설치 지침 섹션에서에서 3 단계를 수행 해야 합니다.

* 클러스터 v3.4의 경우 `pip install sparkmagic==0.2.3`을 실행하여 sparkmagic 0.2.3을 설치합니다.

* 클러스터 v3.5 및 v3.6의 경우 `pip install sparkmagic==0.11.2`를 실행하여 sparkmagic 0.11.2를 설치합니다.

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Spark 매직 tooconnect tooHDInsight Spark 클러스터를 구성 합니다.

이 섹션에서는 Azure HDInsight에서 이미 만든 해야 하는 이전 tooconnect tooan Apache Spark 클러스터를 설치 하는 hello Spark 매직을 구성 합니다.

1. hello Jupyter 구성 정보는 일반적으로 hello 사용자가 홈 디렉터리에 저장 됩니다. toolocate 모든 OS 플랫폼의 경우 다음 형식 hello 홈 디렉터리는 명령입니다.

    Hello Python 셸을 시작 합니다. 명령 창에서 hello 다음을 입력 합니다.

        python

    Python 셸 hello hello 명령 toofind hello 홈 디렉터리를 다음을 입력 합니다.

        import os
        print(os.path.expanduser('~'))

2. Toohello 홈 디렉터리를 이동 하 고 라는 폴더를 만들어 **.sparkmagic** 아직 없는 경우.
3. Hello 폴더 내의 파일을 만들 **config.json** hello 다음 JSON 코드 조각은 그 안에 추가 합니다.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. **{USERNAME}**, **{CLUSTERDNSNAME}** 및 **{BASE64ENCODEDPASSWORD}**를 적합한 값으로 바꿉니다. 실제 암호에 대 한 다양 한 즐겨 찾는 프로그래밍 언어 또는 온라인 toogenerate base64 인코딩된 암호에서 유틸리티를 사용할 수 있습니다.

5. hello 오른쪽 하트 비트 설정을 구성 `config.json`합니다. 이러한 설정은 hello hello로 동일한 수준에 추가 해야 `kernel_python_credentials` 및 `kernel_scala_credentials` 조각에 추가 된 이전 합니다. 이 tooadd hello 하트 비트 설정 방법 및 위치에 대 한 예제를 보려면 [샘플 config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)합니다.

    * `sparkmagic 0.2.3`(v3.4 클러스터)의 경우 다음을 포함합니다.

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * `sparkmagic 0.11.2`(v3.5 및 v3.6 클러스터)의 경우 다음을 포함합니다.

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >하트 비트 세션 유출 되지 않습니다 tooensure를 전송 됩니다. 컴퓨터 toosleep 라인 또는 종료 될 때 hello 하트 비트를 보내지 않습니다, 그리고 정리 hello 세션 중에 발생 합니다. 클러스터 v3.4 toodisable이이 동작을 원하는 경우 설정할 수 있는 hello 리비 config `livy.server.interactive.heartbeat.timeout` 너무`0` hello Ambari UI에서에서 합니다. 클러스터 v 3.5에 대 한 위의 3.5 hello 구성 설정 하지 않으면 hello 세션 삭제 되지 않습니다.

6. Jupyter를 시작합니다. Hello hello 명령 프롬프트에서 다음 명령을 사용 합니다.

        jupyter notebook

7. Hello Jupyter 노트북 및 사용할 수 있는 hello Spark 매직 hello 커널 사용할 수 있는 사용 하 여 toohello 클러스터에 연결할 수 있는지 확인 합니다. Hello 다음 단계를 수행 합니다.

    a. 새 Notebook을 만듭니다. Hello 오른쪽 모서리에서 클릭 **새로**합니다. Hello 기본 커널 표시 되어야 **Python2** 를 설치 하는 두 개의 새 커널 hello 및 **PySpark** 및 **Spark**합니다. **PySpark**를 클릭합니다.

    ![Jupyter 노트북의 커널](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter 노트북의 커널")

    b. 다음 코드 조각 hello를 실행 합니다.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Hello 출력 성공적으로 가져오면 연결 toohello HDInsight 클러스터에이 테스트 됩니다.

    >[!TIP]
    >Tooupdate hello 노트북 구성 tooconnect tooa 다른 클러스터를 사용 하도록 하려는 경우에 위의 3 단계에서에서와 같이 hello config.json hello 새로운 집합의 값을 업데이트 합니다.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>내 컴퓨터에 Jupyter를 설치해야 해야 이유는 무엇인가요?
숫자일 수 HDInsight의 Spark tooa 클러스터 이유 이유 수도 tooinstall Jupyter 컴퓨터에 있으며 다음 연결 중입니다.

* Jupyter 노트북을 이미 Azure HDInsight의 Spark 클러스터 hello에서 사용할 수 있는 경우에 로컬로 전자 필기장 옵션 toocreate hello, 실행 중인 클러스터에 대 한 응용 프로그램을 테스트 및 hello를 업로드 한 다음 제공 Jupyter 컴퓨터에 설치 노트북 toohello 클러스터입니다. tooupload hello 전자 필기장 toohello 클러스터 하거나 업로드 하면 클러스터를 실행 하는 hello Jupyter 노트북 또는 hello를 사용 하 여 또는 hello 클러스터와 연결 된 hello 저장소 계정에서 toohello /HdiNotebooks 폴더를 저장 합니다. 전자 필기장 hello 클러스터에 저장 되는 방법에 대 한 자세한 내용은 참조 하십시오. [Jupyter 노트북 저장 되어 있는](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* 로컬에서 사용할 수 있는 hello 전자 필기장 응용 프로그램 요구 사항에 따라 toodifferent Spark 클러스터 연결할 수 있습니다.
* GitHub tooimplement 소스 제어 시스템을 사용할 수 있으며 hello 전자 필기장에 대 한 버전 제어. 공동 작업 환경에 여러 사용자가 작업할 수 hello 동일한 점이 전자 필기장 합니다.
* 클러스터 없이 로컬로 Notebook을 사용할 수 있습니다. 하기만 하면 클러스터 tootest 전자 필기장에 대 한, 하지 toomanually 전자 필기장 또는 개발 환경을 관리 합니다.
* 그 보다 쉽게 tooconfigure tooconfigure hello Jupyter 설치 hello 클러스터에서 보다 직접 로컬 개발 환경 수 있습니다.  하나 이상의 원격 클러스터를 구성 하지 않고 로컬로 설치 된 모든 hello 소프트웨어 활용할 수 있습니다.

> [!WARNING]
> 로컬 컴퓨터에 설치 된 Jupyter, 여러 사용자가 hello 실행할 수 있습니다 hello hello에 동일한 Spark 클러스터에서 동일한 전자 필기장 동시 합니다. 이러한 상황에서 여러 Livy 세션이 생성됩니다. 문제를 실행 하 고 원하는 어떤 리비 세션 속한 toowhich 사용자 복잡 한 작업 tootrack 하다는 점을, toodebug 합니다.
>
>

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
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
