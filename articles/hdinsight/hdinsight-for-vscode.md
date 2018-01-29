---
title: "Azure HDInsight Tools - Hive, LLAP 또는 pySpark용 Visual Studio Code 사용 | Microsoft Docs"
description: "Azure HDInsight Tools for Visual Studio Code를 사용하여 쿼리와 스크립트를 만들고 제출하는 방법에 대해 알아봅니다."
Keywords: VS Code,Azure HDInsight Tools,Hive,Python,PySpark,Spark,HDInsight,Hadoop,LLAP,Interactive Hive,Interactive Query
services: HDInsight
documentationcenter: 
author: jejiang
manager: 
editor: jgao
tags: azure-portal
ms.assetid: 
ms.service: HDInsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/27/2017
ms.author: jejiang
ms.openlocfilehash: 89e83dc02f32f6f2a781cf2e35040b29cc3d3c06
ms.sourcegitcommit: 4bd369fc472dced985239aef736fece42fecfb3b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2018
---
# <a name="use-azure-hdinsight-tools-for-visual-studio-code"></a>Azure HDInsight Tools for Visual Studio Code 사용

Azure HDInsight Tools for Visual Studio Code(VS Code)를 사용하여 Hive 배치, 대화형 Hive 쿼리 및 pySpark 스크립트를 만들고 제출하는 방법에 대해 알아봅니다. Azure HDInsight Tools는 VS Code에서 지원하는 플랫폼에 설치할 수 있습니다. 여기에는 Windows, Linux, macOS가 포함됩니다. 다양한 플랫폼에 대한 필수 조건을 찾을 수 있습니다.


## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 완료하려면 다음 항목이 필요합니다.

- HDInsight 클러스터.  클러스터를 만들려면 [HDInsight 시작]( hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.
- [Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx)
- [Mono](http://www.mono-project.com/docs/getting-started/install/). Mono는 Linux 및 macOS에만 필요합니다.

## <a name="install-the-hdinsight-tools"></a>HDInsight Tools 설치
   
필수 구성 요소를 설치한 후 Azure HDInsight Tools for VS Code를 설치할 수 있습니다. 

**Azure HDInsight Tools를 설치하려면**

1. Visual Studio Code를 엽니다.

2. 왼쪽 창에서 **확장**을 선택합니다. 검색 상자에 **HDInsight**를 입력합니다.

3. **Azure HDInsight Tools** 옆에 있는 **설치**를 선택합니다. 몇 초 후에 **설치** 단추가 **다시 로드**로 변경됩니다.

4. **다시 로드**를 선택하여 **Azure HDInsight Tools** 확장을 활성화합니다.

5. **창 다시 로드**를 선택하여 확인합니다. **확장** 창에서 **Azure HDInsight Tools**를 확인할 수 있습니다.

   ![HDInsight for Visual Studio Code Python 설치](./media/hdinsight-for-vscode/install-hdInsight-plugin.png)

## <a name="open-hdinsight-workspace"></a>HDInsight 작업 영역 열기

Azure에 연결하려면 먼저 VS Code에서 작업 영역을 만듭니다.

**작업 영역을 열려면**

1. **파일** 메뉴에서 **폴더 열기**를 선택합니다. 그런 다음 기존 폴더를 작업 폴더로 지정하거나 새 작업 폴더를 만듭니다. 해당 폴더가 왼쪽 창에 나타납니다.

2. 왼쪽 창에서 작업 폴더 옆의 **새 파일** 아이콘을 선택합니다.

   ![새 파일](./media/hdinsight-for-vscode/new-file.png)

3. .hql(Hive 쿼리) 또는 .py(Spark 스크립트) 파일 확장명 중 하나를 사용하여 새 파일 이름을 지정합니다. **XXXX_hdi_settings.json** 구성 파일이 작업 폴더에 자동으로 추가됩니다.

4. **탐색기**에서 **XXXX_hdi_settings.json**을 열거나 스크립트 편집기를 마우스 오른쪽 단추로 클릭하여 **구성 설정**을 선택합니다. 파일에서 샘플에 표시된 것처럼 로그인 항목, 기본 클러스터 및 작업 제출 매개 변수를 구성할 수 있습니다. 나머지 매개 변수를 비워 둘 수도 있습니다.

## <a name="connect-to-azure"></a>Azure에 연결

VS Code에서 HDInsight 클러스터에 스크립트를 제출하려면 먼저 Azure 계정에 연결해야 합니다.

**Azure에 연결하려면**

1. 새 작업 폴더 및 새 스크립트 파일을 만듭니다(아직 없는 경우).

2. 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **HDInsight: Login**을 선택합니다. **Ctrl+Shift+P**를 누르고 **HDInsight: Login**을 입력할 수도 있습니다.

    ![HDInsight Tools for Visual Studio Code 로그인](./media/hdinsight-for-vscode/hdinsight-for-vscode-extension-login.png)

3. 로그인하려면 **출력** 창의 로그인 지침을 따릅니다.

    **Azure:** ![HDInsight Tools for Visual Studio Code 로그인 정보](./media/hdinsight-for-vscode/hdinsight-for-vscode-extension-Azurelogin-info.png)

    일단 연결되면 Azure 계정 이름이 VS Code 창 왼쪽 하단 상태 표시줄에 표시됩니다. 

    > [!NOTE]
    > 알려진 Azure 인증 문제 때문에 개인 모드 또는 incognito 모드에서 브라우저를 열어야 합니다. Azure 계정에서 두 가지 요소를 사용하도록 설정한 경우 PIN 인증 대신 전화 인증을 사용하는 것이 좋습니다.
  

4. 스크립트 편집기를 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 엽니다. 상황에 맞는 메뉴에서 다음 작업을 수행할 수 있습니다.

    - 로그아웃
    - 클러스터 나열
    - 기본 클러스터 설정
    - 대화형 Hive 쿼리 제출
    - Hive 배치 스크립트 제출
    - 대화형 PySpark 쿼리 제출
    - PySpark 배치 스크립트 제출
    - 구성 설정

## <a name="list-hdinsight-clusters"></a>HDInsight 클러스터 나열

연결을 테스트하기 위해 HDInsight 클러스터를 나열할 수 있습니다.

**Azure 구독의 HDInsight 클러스터를 나열하려면**
1. 작업 영역을 열고 Azure에 연결합니다. 자세한 내용은 [HDInsight 작업 영역 열기](#open-hdinsight-workspace) 및 [Azure에 연결](#connect-to-azure)을 참조하세요.

2. 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **HDInsight: List Cluster**를 선택합니다. 

3. **출력** 창에 Hive 및 Spark 클러스터가 나타납니다.

    ![기본 클러스터 구성 설정](./media/hdinsight-for-vscode/list-cluster-result.png)

## <a name="set-a-default-cluster"></a>기본 클러스터 설정
1. 작업 영역을 열고 Azure에 연결합니다. [HDInsight 작업 영역 열기](#open-hdinsight-workspace) 및 [Azure에 연결](#connect-to-azure)을 참조하세요.

2. 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **HDInsight: Set Default Cluster**를 선택합니다. 

3. 현재 스크립트 파일에 대한 기본 클러스터로 사용할 클러스터를 선택합니다. **XXXX_hdi_settings.json** 구성 파일이 자동으로 업데이트됩다. 

   ![기본 클러스터 구성 설정](./media/hdinsight-for-vscode/set-default-cluster-configuration.png)

## <a name="set-the-azure-environment"></a>Azure 환경 설정 
1. **Ctrl+Shift+P**를 선택하여 명령 팔레트를 엽니다.

2. **HDInsight: Set Azure Environment**를 입력합니다.

3. 기본 로그인 항목으로 Azure와 AzureChina 중 하나를 선택합니다.

4. 그렇지만 사용자의 기본 로그인 항목은 **XXXX_hdi_settings.json**이미 저장되어 있습니다. 이 구성 파일에서 기본 로그인 항목을 직접 업데이트할 수도 있습니다. 

   ![기본 로그인 항목 구성 설정](./media/hdinsight-for-vscode/set-default-login-entry-configuration.png)

## <a name="submit-interactive-hive-queries"></a>대화형 Hive 쿼리 제출

HDInsight Tools for VS Code를 사용하면 HDInsight 대화형 쿼리 클러스터에 대화형 Hive 쿼리를 제출할 수 있습니다.

1. 새 작업 폴더 및 새 Hive 스크립트 파일을 만듭니다(아직 없는 경우).

2. Azure 계정에 연결한 다음 기본 클러스터를 구성합니다(아직 구성하지 않은 경우).

3. 다음 코드를 복사하여 Hive 파일에 붙여넣은 후 파일을 저장합니다.

    ```hiveql
    SELECT * FROM hivesampletable;
    ```
3. 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **HDInsight: Hive Interactive**를 선택하여 쿼리를 제출합니다. 이 도구에서는 상황에 맞는 메뉴를 사용하여 전체 스크립트 파일 대신 코드 블록을 제출할 수도 있습니다. 잠시 후 다음과 같이 새 탭에 쿼리 결과가 표시됩니다.

   ![대화형 Hive 결과](./media/hdinsight-for-vscode/interactive-hive-result.png)

    - **결과** 패널: 전체 결과를 CSV, JSON 또는 Excel 파일로 로컬 경로에 저장하거나 여러 줄을 선택할 수 있습니다.

    - **메시지** 패널: **줄** 번호를 선택하면 실행 중인 스크립트의 첫 번째 줄로 이동합니다.

[Hive 배치 작업 실행](#submit-hive-batch-scripts)에 비해 대화형 쿼리 실행이 훨씬 더 빠릅니다.

## <a name="submit-hive-batch-scripts"></a>Hive 배치 스크립트 제출

1. 새 작업 폴더 및 새 Hive 스크립트 파일을 만듭니다(아직 없는 경우).

2. Azure 계정에 연결한 다음 기본 클러스터를 구성합니다(아직 구성하지 않은 경우).

3. 다음 코드를 복사하여 Hive 파일에 붙여넣은 후 파일을 저장합니다.

    ```hiveql
    SELECT * FROM hivesampletable;
    ```
3. 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **HDInsight: Hive Batch**를 선택하여 Hive 작업을 제출합니다. 

4. 제출하려는 클러스터를 선택합니다.  

    Hive 작업을 제출하면 제출 성공 정보 및 jobid가 **출력** 패널에 표시됩니다. Hive 작업은 **웹 브라우저**도 열어 실시간 작업 로그 및 상태를 표시합니다.

   ![Hive 작업 결과 제출](./media/hdinsight-for-vscode/submit-Hivejob-result.png)

[대화형 Hive 쿼리 제출](#submit-interactive-hive-queries)이 일괄 작업 제출보다 훨씬 더 빠릅니다.

## <a name="submit-interactive-pyspark-queries"></a>대화형 PySpark 쿼리 제출
또한 VS Code용 HDInsight 도구를 사용하면 Spark 클러스터에 대화형 PySpark 쿼리를 제출할 수 있습니다.
1. 새 작업 폴더 및 확장명이 .py인 새 스크립트 파일을 만듭니다(아직 없는 경우).

2. Azure 계정에 아직 연결하지 않은 경우 연결합니다.

3. 다음 코드를 복사하여 스크립트 파일에 붙여넣습니다.
   ```python
   from operator import add
   lines = spark.read.text("/HdiSamples/HdiSamples/FoodInspectionData/README").rdd.map(lambda r: r[0])
   counters = lines.flatMap(lambda x: x.split(' ')) \
                .map(lambda x: (x, 1)) \
                .reduceByKey(add)

   coll = counters.collect()
   sortedCollection = sorted(coll, key = lambda r: r[1], reverse = True)

   for i in range(0, 5):
        print(sortedCollection[i])
   ```
4. 이러한 스크립트를 강조 표시합니다. 그런 후 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **HDInsight: PySpark Interactive**를 선택합니다.

5. VS Code에서 **Python** 확장을 아직 설치하지 않은 경우 다음 그림과 같이 **설치** 단추를 선택합니다.

    ![HDInsight for Visual Studio Code Python 설치](./media/hdinsight-for-vscode/hdinsight-vscode-install-python.png)

6. 시스템에 Python 환경을 아직 설치하지 않은 경우 설치합니다. 
   - Windows에서 [Python](https://www.python.org/downloads/)을 다운로드하고 설치합니다. 그런 다음 시스템 경로에 `Python` 및 `pip`가 있는지 확인합니다.

   - macOS 및 Linux용 지침은 [Visual Studio Code용 PySpark 대화형 환경 설정](set-up-pyspark-interactive-environment.md)을 참조하세요.

7. PySpark 쿼리를 제출할 클러스터를 선택합니다. 잠시 후 다음과 같이 오른쪽의 새 탭에 쿼리 결과가 표시됩니다.

   ![Python 작업 결과 제출](./media/hdinsight-for-vscode/pyspark-interactive-result.png) 
8. 이 도구는 **SQL 절** 쿼리도 지원합니다.

   ![Python 결과 작업 제출](./media/hdinsight-for-vscode/pyspark-ineteractive-select-result.png) 쿼리를 실행할 때 제출 상태가 아래쪽 상태 표시줄의 왼쪽에 표시됩니다. 상태가 **PySpark 커널(작업 중)**이면 다른 쿼리를 제출하지 마세요. 

>[!NOTE]
>클러스터는 세션 정보를 유지할 수 있습니다. 정의된 변수, 함수 및 해당 값은 세션에 유지되므로 동일한 클러스터에 대한 여러 서비스 호출에서 참조될 수 있습니다. 
 

## <a name="submit-pyspark-batch-job"></a>PySpark 배치 작업 제출

1. 새 작업 폴더 및 확장명이 .py인 새 스크립트 파일을 만듭니다(아직 없는 경우).

2. Azure 계정에 아직 연결하지 않은 경우 연결합니다.

3. 다음 코드를 복사하여 스크립트 파일에 붙여넣습니다.

    ```python
    from __future__ import print_function
    import sys
    from operator import add
    from pyspark.sql import SparkSession
    if __name__ == "__main__":
        spark = SparkSession\
            .builder\
            .appName("PythonWordCount")\
            .getOrCreate()
    
        lines = spark.read.text('/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv').rdd.map(lambda r: r[0])
        counts = lines.flatMap(lambda x: x.split(' '))\
                    .map(lambda x: (x, 1))\
                    .reduceByKey(add)
        output = counts.collect()
        for (word, count) in output:
            print("%s: %i" % (word, count))
        spark.stop()
    ```
4. 스크립트 편집기를 마우스 오른쪽 단추로 클릭한 다음 **HDInsight: PySpark Batch**를 선택합니다. 

5. PySpark 작업을 제출할 클러스터를 선택합니다. 

   ![Python 작업 결과 제출](./media/hdinsight-for-vscode/submit-pythonjob-result.png) 

Python 작업을 제출한 후 전송 로그가 VS Code의 **출력** 창에 나타납니다. **Spark UI URL** 및 **Yarn UI URL**도 표시됩니다. 웹 브라우저에서 URL을 열어 작업 상태를 추적할 수 있습니다.


## <a name="additional-features"></a>추가 기능

HDInsight for VS Code에서 지원하는 기능은 다음과 같습니다.

- **IntelliSense 자동 완성**. 키워드, 메서드, 변수 등에 대한 추천 항목이 팝업됩니다. 다음과 같이 다양한 아이콘이 여러 형식의 개체를 나타냅니다.

    ![HDInsight Tools for Visual Studio Code IntelliSense 개체 형식](./media/hdinsight-for-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **IntelliSense 오류 표식**. 언어 서비스에서 Hive 스크립트에 대한 편집 오류에 밑줄을 표시합니다.     
- **구문 강조 표시**. 언어 서비스는 변수, 키워드, 데이터 형식, 함수 등을 구분하기 위해 서로 다른 색상을 사용합니다. 

    ![HDInsight Tools for Visual Studio Code 구문 강조 표시](./media/hdinsight-for-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>다음 단계

### <a name="demo"></a>데모
* HDInsight for VS Code: [비디오](https://go.microsoft.com/fwlink/?linkid=858706)

### <a name="tools-and-extensions"></a>도구 및 확장

* [IntelliJ용 Azure 도구 키트를 사용하여 VPN을 통해 원격으로 Spark 응용 프로그램 디버그](spark/apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 원격으로 Spark 응용 프로그램 디버그](spark/apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용](hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Eclipse용 Azure 도구 키트의 HDInsight 도구를 사용하여 Spark 응용 프로그램 만들기](spark/apache-spark-eclipse-tool-plugin.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](spark/apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](spark/apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](spark/apache-spark-jupyter-notebook-use-external-packages.md)
* [컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결](spark/apache-spark-jupyter-notebook-install-locally.md)
* [Azure HDInsight에서 Microsoft Power BI를 사용하여 Hive 데이터 시각화](hadoop/apache-hadoop-connect-hive-power-bi.md)
* [Azure HDInsight에서 Power BI를 사용하여 대화형 쿼리 Hive 데이터 시각화](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md)
* [Visual Studio Code용 PySpark 대화형 환경 설정](set-up-pyspark-interactive-environment.md)
* [Azure HDInsight에서 Zeppelin을 사용하여 Hive 쿼리 실행](./hdinsight-connect-hive-zeppelin.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](spark/apache-spark-use-bi-tools.md)
* 
            [Machine Learning과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](spark/apache-spark-ipython-notebook-machine-learning.md)
* 
            [Machine Learning과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용](spark/apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](spark/apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](spark/apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-running-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](spark/apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](spark/apache-spark-livy-rest-interface.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리](spark/apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](spark/apache-spark-job-debugging.md)



