---
title: "Toolkit for Eclipse-HDInsight Spark에 대 한 응용 프로그램 만들기 Scala aaaAzure | Microsoft Docs"
description: "Eclipse toodevelop Spark 작성 된 응용 프로그램 Scala에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 고 전송할 tooan HDInsight Spark 클러스터에 hello Eclipse IDE에서 직접 있습니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Azure 도구 키트를 사용 하 여 HDInsight 클러스터에 대 한 Eclipse toocreate Spark 응용 프로그램에 대 한

Toodevelop Eclipse 용 Azure 도구 키트의 HDInsight 도구를 사용 하 여 멤버 Scala 작성 된 응용 프로그램 및 hello Eclipse IDE에서 직접 tooan Azure HDInsight Spark 클러스터에 전송 합니다. Hello HDInsight 도구는 몇 가지 방법에서 플러그 인을 사용할 수 있습니다.

* toodevelop HDInsight Spark 클러스터에 있는 Scala Spark 응용 프로그램을 제출 하 고
* tooaccess Azure HDInsight Spark 클러스터 리소스
* toodevelop 및 Scala Spark 응용 프로그램을 로컬로 실행

> [!IMPORTANT]
> 이 도구 사용된 toocreate를 수 있으며 Linux에서 HDInsight Spark 클러스터는에 대 한 응용 프로그램 제출 됩니다.
> 
> 

## <a name="prerequisites"></a>필수 조건

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.
* Oracle Java 개발 키트 버전 8 hello Eclipse IDE 런타임에 사용 되는입니다. Hello에서 다운로드할 수 있습니다 [Oracle 웹 사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)합니다.
* Eclipse IDE. 이 문서에서는 Eclipse Neon을 사용합니다. Hello에서 설치할 수 있습니다 [Eclipse 웹 사이트](https://www.eclipse.org/downloads/)합니다.   
* Spark SDK. [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409)에서 다운로드할 수 있습니다.


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Azure 도구 키트에 Eclipse 및 Scala 플러그 인에 대 한 HDInsight 도구를 설치
### <a name="install-hdinsight-tools"></a>HDInsight Tools 설치
Eclipse용 HDInsight Tools는 Eclipse용 Azure 도구 키트의 일부분으로 제공됩니다. 설치 지침은 [Eclipse용 Azure 도구 키트 설치](../azure-toolkit-for-eclipse-installation.md)를 참조하세요.
### <a name="install-scala-plugin"></a>Scala 플러그 인 설치
Intellij hello를 열 때 hello HDInsight 도구 자동 여부 Scala 플러그 인 설치 되어 있는지 여부를 검색 합니다. 클릭 **확인** hello Eclipse 마켓플레이스 하 여 hello 지침 tooinstall toocontinue 및 수행 합니다.

 ![자동 설치 Scala 플러그 인](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Azure 구독 tooyour에 로그인
1. Hello Eclipse IDE를 시작 하 고 Azure 탐색기를 엽니다. Hello에 **창** 메뉴를 클릭 하 여 **보기 표시**, 클릭 하 고 **다른**합니다. Hello 대화 상자가 열리면 확장 **Azure**, 클릭 **Azure 탐색기**, 클릭 하 고 **확인**합니다.

    ![보기 표시 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. 마우스 오른쪽 단추로 클릭 hello **Azure** 노드를 차례로 클릭 한 다음 **로그인**합니다.
3. Hello에 **Azure 로그인** 대화 상자 hello 인증 방법을 선택 하 고 클릭 **로그인**, Azure 자격 증명을 입력 하 고 있습니다.
   
    ![Azure 로그인 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. 로그인, 후 hello **구독 선택** hello 자격 증명으로 연결 된 Azure 구독을 hello 모든 대화 상자 목록입니다. 클릭 **선택** tooclose hello 대화 상자.

    ![구독 선택 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Hello에 **Azure 탐색기** 탭을 확장 하 고 **HDInsight** 구독에서 HDInsight Spark 클러스터 toosee hello 합니다.
   
    ![Azure 탐색기의 HDInsight Spark 클러스터](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. 클러스터 이름 노드 toosee hello 리소스 (예를 들어 저장소 계정) hello 클러스터와 연결 된 추가로 확장할 수 있습니다.
   
    ![클러스터 이름 toosee 리소스를 확장합니다.](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에 Spark Scala 프로젝트 설정

1. Hello Eclipse IDE 작업 영역에서 클릭 **파일**, 클릭 **새로**, 클릭 하 고 **프로젝트**합니다. 
2. Hello 새 프로젝트 마법사에서 확장 **HDInsight**선택, **(Scala) HDInsight의 Spark**, 클릭 하 고 **다음**합니다.

    ![HDInsight (Scala) 프로젝트에서 Spark hello를 선택합니다.](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. hello Scala 프로젝트 만들기 마법사 자동 여부 Scala 플러그 인 설치 되어 있는지 여부를 검색 합니다. 클릭 **확인** toocontinue hello Scala 플러그 인을 다음에 따라 hello 지침 toorestart Eclipse 다운로드 합니다.

    ![Scala 확인](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. Hello에 **새 HDInsight Scala 프로젝트** 대화 상자에서 다음 값을 hello를 입력 한 다음 **다음**:
   * Hello 프로젝트에 대 한 이름을 입력 합니다.
   * Hello에 **JRE** 영역에서 다음 사항을 확인 **JRE 실행 환경을 사용 하 여** 너무 설정 되어**JavaSE 1.7** 이상.
   * Spark SDK hello SDK 다운로드 toohello 위치 설정 인지 확인 합니다. hello 링크 toohello 다운로드 위치에에서 연결 되어 hello [필수 구성 요소](#prerequisites) 이 문서의 앞부분에 있습니다. Hello에서 hello SDK를 다운로드할 수도 hello 대화 상자에 포함 된 링크.

    ![새 HDInsight Scala 프로젝트 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  Hello 다음 대화 상자에서 클릭 hello **라이브러리** 탭 하 고 hello 기본값을 유지 한 다음 클릭 **마침**합니다. 
   
    ![라이브러리 탭](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에 대한 Scala 응용 프로그램 만들기

1. Hello 패키지 탐색기에서 Eclipse IDE에서에서 이전에 만든 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**, 클릭 하 고 **다른**합니다.
2. Hello에 **마법사 선택** 대화 상자에서 **Scala 마법사**, 클릭 **Scala 개체**, 클릭 하 고 **다음**합니다.
   
    ![마법사 대화 상자 선택](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. Hello에 **새 파일 만들기** hello 개체에 대 한 이름을 입력 하 고 클릭 하는 대화 상자, **마침**합니다.
   
    ![새 파일 대화 상자 만들기](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Hello를 hello 텍스트 편집기에서 코드 다음에 붙여 넣습니다.
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. HDInsight Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.
   
   1. 패키지 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **Spark 응용 프로그램 제출 tooHDInsight**합니다.        
   2. Hello에 **Spark 제출** 대화 상자에서 다음 값을 hello를 입력 한 다음 **전송**:
      
      * 에 대 한 **클러스터 이름**, 선택 hello toorun 원하는 HDInsight Spark 클러스터 응용 프로그램입니다.
      * Hello Eclipse 프로젝트에서 아티팩트를 선택 하거나 하드 드라이브에서 선택 합니다. hello 기본값 패키지 탐색기에서 마우스 오른쪽 단추로 클릭 하는 hello 항목에 따라 달라 집니다.
      * Hello에 **Main 클래스 이름** dropdownlist, 제출 마법사에는 선택한 프로젝트에서 모든 개체 이름이 표시 됩니다. 선택 하거나 하나를 입력 toorun 되도록 합니다. 하드 디스크에서 아티팩트를 선택하는 경우 기본 클래스 이름을 직접 입력해야 합니다. 
      * 이 예에서 응용 프로그램 코드 hello 어떤 명령줄 인수도 필요 하지 않거나 Jar 또는 파일 참조를 때문에 남아 있는 빈 입력란 hello를 둘 수 있습니다.
        
       ![Spark 제출 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. hello **Spark 제출** 탭 hello 진행률을 표시 하기 시작 해야 합니다. Hello hello 빨간색 단추를 클릭 하 여 hello 응용 프로그램을 중지할 수 있습니다 **Spark 제출** 창. Hello 지구 아이콘 (hello 이미지의 hello 파란색 상자로 표시 됨)를 클릭 하 여 실행이 특정 응용 프로그램에 대 한 hello 로그를 볼 수 있습니다.
      
       ![Spark 제출 창](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 HDInsight Spark 클러스터 액세스 및 관리
Hello 작업 출력을 액세스를 포함 하는 HDInsight 도구를 사용 하 여 다양 한 작업을 수행할 수 있습니다.

### <a name="access-hello-job-view"></a>액세스 hello 작업 보기
1. Azure 탐색기에서 확장 **HDInsight**hello Spark 클러스터 이름을 확장 하 고 클릭 **작업**합니다. 

    ![작업 보기 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Hello 클릭 **작업** 노드. hello HDInsight 도구 자동 검색 여부 hello E (fx) clipse 플러그 인을 설치 여부. 클릭 **확인** toocontinue 및 따라 hello 지침은 tooinstall Eclipse 마켓플레이스 hello 및 Eclipse를 다시 시작 합니다.

    ![E(fx)clipse 설치](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Hello에서 열기 hello 작업 보기 **작업** 노드. Hello 오른쪽 창에서 hello **Spark 작업 보기** hello 클러스터에서 실행 된 모든 hello 응용 프로그램 탭에 표시 됩니다. Hello을 구하려는 toosee 자세히 hello 응용 프로그램 이름을 클릭 합니다.

    ![응용 프로그램 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Hello 작업 그래프에서 마우스 포인터를 기본 실행 중인 작업 정보를 표시 됩니다. Hello 작업 그래프 클릭 하면 hello 단계 그래프 및 모든 작업을 생성 하는 정보를 표시 합니다.

    ![작업 단계 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Stderr 드라이버, 드라이버 Stdout 및 디렉터리 정보를 포함 하는 자주 사용 되는 로그가 hello에 나열 됩니다 **로그** 탭 합니다.

    ![로그 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Hello 창의 위쪽에 hello hello 해당 하이퍼링크를 클릭 하 여 hello Spark 기록 UI 및 hello hello 응용 프로그램 수준에서 YARN UI를 열 수도 있습니다.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Hello 클러스터에 대 한 액세스 hello 저장소 컨테이너
1. Azure 탐색기에서 확장 hello **HDInsight** 루트 노드 toosee HDInsight Spark 클러스터에 사용할 수 있는 목록입니다.
2. Hello 클러스터 이름 toosee hello 저장소 계정 및 hello 클러스터에 대 한 hello 기본 저장소 컨테이너를 확장 합니다.
   
    ![저장소 계정 및 기본 저장소 컨테이너](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Hello 클러스터와 연결 된 hello 저장소 컨테이너 이름을 클릭 합니다. Hello 오른쪽 창에서 hello를 두 번 클릭 **HVACOut** 폴더입니다. Hello 중 하나를 열려면 **파트-** hello 응용 프로그램의 toosee hello 출력 파일입니다.

### <a name="access-hello-spark-history-server"></a>Hello Spark 기록 서버에 액세스
1. Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **Spark 기록 UI 열기**를 선택합니다. 메시지가 나타나면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다. 지정 해야 hello 클러스터를 프로 비전 할 때 이러한 합니다.
2. Hello Spark 기록 서버 대시보드 hello 응용 프로그램 실행이 방금 완료에 대 한 응용 프로그램 이름 toolook hello를 사용 합니다. Hello 앞에 코드를 사용 하 여 hello 응용 프로그램 이름을 설정 `val conf = new SparkConf().setAppName("MyClusterApp")`합니다. 그러므로 Spark 응용 프로그램의 이름은 **MyClusterApp**입니다.

### <a name="start-hello-ambari-portal"></a>Hello Ambari 포털 시작
1. Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **클러스터 관리 포털(Ambari) 열기**를 선택합니다. 
2. 메시지가 나타나면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다. 지정 해야 hello 클러스터를 프로 비전 할 때 이러한 합니다.

### <a name="manage-azure-subscriptions"></a>Azure 구독 관리
Eclipse 용 Azure 도구 키트의 HDInsight 도구 기본적으로 모든 Azure 구독에서 hello Spark 클러스터를 나열합니다. 필요한 경우 tooaccess hello 클러스터 원하는 hello 구독을 지정할 수 있습니다. 

1. Azure 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Azure** 루트 노드를 찾은 다음 클릭 **구독 관리**합니다. 
2. Hello 대화 상자에서 tooaccess, 원하는 및 클릭 하지 않는 hello 구독에 대 한 hello 확인란의 선택을 취소 **닫기**합니다. 클릭할 수도 있습니다 **로그 아웃** toosign Azure 구독에서 하려는 경우.

## <a name="run-a-spark-scala-application-locally"></a>로컬로 Spark Scala 응용 프로그램 실행
사용할 수 있습니다 HDInsight 도구 Azure 도구 키트에 Eclipse toorun Spark Scala 응용 프로그램에 대 한 로컬 워크스테이션에 설치 합니다. 일반적으로 이러한 응용 프로그램 저장소 컨테이너와 같은 toocluster 리소스에 액세스 하지 않아도 하 고 실행 하 고 로컬로 테스트할 수 있습니다.

### <a name="prerequisite"></a>필수 요소
에 설명 된 대로 예외가 발생할 수 hello 로컬 Spark Scala 응용 프로그램을 Windows 컴퓨터에서 실행 하는 동안 [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)합니다. 이 예외는 Windows에 **WinUtils.exe**가 없기 때문에 발생합니다. 

tooresolve 해야이 오류를 [hello 실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 위치 **C:\WinUtils\bin**합니다. 그런 다음 hello 환경 변수를 추가 해야 **HADOOP_HOME** 너무 hello hello 변수 값을 설정 하 고**C\WinUtils**합니다.

### <a name="run-a-local-spark-scala-application"></a>로컬 Spark Scala 응용 프로그램 실행
1. Eclipse를 시작하고 프로젝트를 만듭니다. Hello에 **새 프로젝트** 대화 상자, hello 선택 옵션을 다음을 확인 한 다음 클릭 **다음**합니다.
   
   * Hello 왼쪽된 창에서 선택 **HDInsight**합니다.
   * Hello 오른쪽 창에서 선택 **HDInsight의 로컬 실행 되는 샘플 (Scala)의 Spark**합니다.

    ![새 프로젝트 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. tooprovide hello 프로젝트 세부 정보를 작업 단계 3-6에서 이전 섹션 hello [HDInsight Spark 클러스터에 대 한 Spark Scala 프로젝트 설정](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster)합니다.
3. 샘플 코드를 추가 하는 hello 템플릿 (**LogQuery**) hello에서 **src** 폴더를 컴퓨터에 로컬로 실행할 수 있습니다.
   
    ![LogQuery 위치](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. 마우스 오른쪽 단추로 클릭 hello **LogQuery** 응용 프로그램을 너무 가리킨**계정으로 실행**, 클릭 하 고 **Scala 응용 프로그램 1**합니다. Hello에서 다음과 같은 출력을 보게 **콘솔** hello 아래쪽에 탭:
   
   ![Spark 응용 프로그램 로컬 실행 결과](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>FAQ
응용 프로그램 tooAzure 데이터 레이크 저장소 toosubmit 선택 **Interactive'** hello Azure 로그인 프로세스 중 모드입니다. **자동화된** 모드를 선택하는 경우 오류가 발생할 수 있습니다.

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

현재 이 오류는 해결했습니다. 어떤 로그인 방법으로 Azure 데이터 레이크 클러스터 toosubmit 응용 프로그램을 선택할 수 있습니다.

## <a name="feedback-and-known-issues"></a>사용자 의견 및 알려진 문제
현재 직접 Spark 출력 보기는 지원되지 않습니다.

모든 제안이 나 의견이, 또는이 도구를 사용할 때 문제가 발생 하는 경우 느껴집니다 무료 toosend us에 전자 메일 hdivstool@microsoft.com합니다.

## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ toocreate에 대 한 Azure 도구 키트를 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Azure 도구 키트를 사용 하 여 VPN 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [SSH 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트를 사용 합니다.](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

