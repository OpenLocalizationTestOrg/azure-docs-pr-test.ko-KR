---
title: "IntelliJ용 Azure 도구 키트: HDInsight 클러스터용 Spark 응용 프로그램 만들기 | Microsoft Docs"
description: "IntelliJ toodevelop Spark 작성 된 응용 프로그램 Scala에 대 한 hello Azure 도구 키트를 사용 하 고 tooan HDInsight Spark 클러스터에 전송 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Azure 도구 키트를 사용 하 여 HDInsight 클러스터에 대 한 IntelliJ toocreate Spark 응용 프로그램에 대 한

IntelliJ 플러그 인 toodevelop Spark 작성 된 응용 프로그램 Scala에 대 한 hello Azure 도구 키트를 사용 하 여 하 고 tooan hello IntelliJ 통합된 개발 환경 (IDE)에서 직접 HDInsight Spark 클러스터 제출 합니다. Hello 플러그 인에 몇 가지 방법을 사용할 수 있습니다.

* HDInsight Spark 클러스터에서 Scala Spark 응용 프로그램을 개발 및 제출합니다.
* Azure HDInsight Spark 클러스터 리소스에 액세스합니다.
* Scala Spark 응용 프로그램을 로컬로 개발 및 실행합니다.

toocreate 프로젝트, 보기 hello [hello IntelliJ 용 Azure 도구 키트로 Spark 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) 비디오.

> [!IMPORTANT]
> 이 플러그 인 toocreate를 사용 하 여 수 있으며 Linux에서 HDInsight Spark 클러스터는에 대 한 응용 프로그램을 제출할 수 있습니다.
> 

## <a name="prerequisites"></a>필수 조건

- HDInsight Linux의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.
- Oracle Java Development 키트. Hello에서 설치할 수 있습니다 [Oracle 웹 사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)합니다.
- IntelliJ IDEA. 이 문서에서는 버전 2017.1을 사용합니다. Hello에서 설치할 수 있습니다 [JetBrains 웹 사이트](https://www.jetbrains.com/idea/download/)합니다.

## <a name="install-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트 설치
설치 지침에 대해서는 [IntelliJ용 Azure 도구 키트 설치](../azure-toolkit-for-intellij-installation.md)를 참조하세요.

## <a name="sign-in-tooyour-azure-subscription"></a>Azure 구독 tooyour에 로그인

1. Hello IntelliJ IDE를 시작 하 고 Azure 탐색기를 엽니다. Hello에 **보기** 메뉴 선택 **도구 창**를 선택한 후 **Azure 탐색기**합니다.
       
   ![hello Azure 탐색기 링크](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. 마우스 오른쪽 단추로 클릭 hello **Azure** 노드를 선택한 후 **로그인**합니다.

3. Hello에 **Azure 로그인** 대화 상자에서 **로그인**, 한 다음 Azure 자격 증명을 입력 합니다.

    ![hello Azure 로그인 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. 로그인, 후 hello **구독 선택** 연관 된 Azure 구독을 hello 모든 대화 상자 목록 hello 자격 증명입니다. 선택 hello **선택** 단추입니다.

    ![hello 구독 선택 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Hello에 **Azure 탐색기** 탭을 확장 하 고 **HDInsight** 구독에 있는 tooview hello HDInsight Spark 클러스터입니다.
   
    ![Azure 탐색기의 HDInsight Spark 클러스터](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello 리소스 (예를 들어 저장소 계정) hello 클러스터와 연결 된 클러스터 이름 노드를 추가로 확장할 수 있습니다.
   
    ![확장된 클러스터-이름 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에서 Spark Scala 응용 프로그램 실행

1. IntelliJ IDEA를 시작하고 프로젝트를 만듭니다. Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다. 

   a. **HDInsight** > **HDInsight의 Spark(Scala)**를 선택합니다.

   b. Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.

      * Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**
      * **SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한

    ![hello 새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. **다음**을 선택합니다.

3. hello Scala 프로젝트 만들기 마법사는 자동으로 hello Scala 플러그 인을 설치 했는데 있는지 여부를 검색 합니다. **설치**를 선택합니다.

   ![Scala 플러그 인 검사](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. 플러그 인을 선택 Scala toodownload hello **확인**합니다. Hello 지침 toorestart IntelliJ 따릅니다. 

   ![hello Scala 플러그 인 설치 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Hello에 **새 프로젝트** 창에서 다음 hello지 않습니다.  

    ![Hello Spark SDK를 선택합니다.](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. 프로젝트 이름 및 위치를 입력합니다.

   b. Hello에 **프로젝트 SDK** 드롭 다운 목록 **Java 1.8** hello Spark 2.x 클러스터 또는 선택에 대 한 **Java 1.7** hello Spark 1.x 클러스터에 대 한 합니다.

   c. Hello에 **Spark 버전** 드롭 다운 목록에서 Scala 프로젝트 만들기 마법사 Spark SDK 및 Scala SDK에 대 한 hello 적절 한 버전을 통합 합니다. Hello Spark 클러스터 버전이 2.0 보다 이전 이면 선택 **1.x 멤버**합니다. 그렇지 않은 경우 **Spark2.x**를 선택합니다. 이 예제에서는 **Spark 2.0.2(Scala 2.11.8)**를 사용합니다.

6. **마침**을 선택합니다.

7. hello Spark 프로젝트를 아티팩트를 자동으로 만듭니다. tooview hello 아티팩트 다음 hello지 않습니다.

   a. Hello에 **파일** 메뉴 선택 **프로젝트 구조**합니다.

   b. Hello에 **프로젝트 구조** 대화 상자에서 **아티팩트** 만들어진 tooview hello 기본 아티팩트입니다. Hello 더하기 기호를 선택 하 여 사용자 고유의 아티팩트를 만들 수도 있습니다 (**+**).

      ![Hello 대화 상자에서 아티팩트 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Hello 다음을 수행 하 여 응용 프로그램 소스 코드를 추가 합니다.

   a. 프로젝트 탐색기에서 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**를 선택한 후 **Scala 클래스**합니다.
      
      ![프로젝트 탐색기에서 Scala 클래스 만들기에 대한 명령](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. Hello에 **새 Scala 클래스 만들기** 대화 상자, 이름을 제공 하 고, 선택 **개체** hello에 **종류** 상자를 선택한 후 **확인**합니다.
      
      ![새 Scala 클래스 만들기 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. Hello에 **MyClusterApp.scala** 파일, 코드 다음 hello를 붙여 넣습니다. hello 코드 HVAC.csv (모든 HDInsight Spark 클러스터에서 사용 가능)에서 hello 데이터를 읽고, hello hello CSV 파일의 일곱 번째 열에는 하나의 진수가 hello 행을 검색 및 너무 hello 출력을 기록**/HVACOut** hello 기본 hello 클러스터에 대 한 저장소 컨테이너입니다.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Hello 다음을 수행 하 여 HDInsight Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.

   a. 프로젝트 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **Spark 응용 프로그램 제출 tooHDInsight**합니다.
      
      ![hello Spark 응용 프로그램 제출 tooHDInsight 명령](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. 하면 Azure 구독 자격 증명된 tooenter 됩니다. Hello에 **Spark 제출** 대화 상자에서 다음 값을 hello를 지정 하 고 다음 선택 **전송**합니다.
      
      * 에 대 한 **클러스터 (Linux에만 해당) 멤버**, 선택 hello toorun 원하는 HDInsight Spark 클러스터 응용 프로그램입니다.

      * Hello IntelliJ 프로젝트에서 아티팩트를 선택 하거나 hello 하드 드라이브에서 선택 합니다.

      * Hello에 **Main 클래스 이름** 상자 선택 hello 줄임표 (**...** ) hello 주 클래스에서 응용 프로그램 소스 코드를 선택한 다음 선택 **확인**합니다.

        ![hello Main 클래스 선택 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * 이 예에서 응용 프로그램 코드 hello 명령줄 인수도 필요 하지 않거나 Jar 또는 파일 참조를 때문에 남아 있는 빈 상자 hello를 둘 수 있습니다. 모든 hello 정보를 제공한 후 hello 대화 상자 이미지를 수행 하는 hello와 비슷해야 합니다.
        
        ![hello Spark 제출 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. hello **Spark 제출** hello hello 창의 맨 아래에 탭 hello 진행률을 표시 하기 시작 해야 합니다. Hello에 빨간색 hello 단추를 선택 하 여 hello 응용 프로그램을 중지할 수도 있습니다 **Spark 제출** 창.
      
      ![hello Spark 전송 창](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn tooaccess hello 작업 출력 참조 hello "액세스 IntelliJ 용 Azure 도구 키트를 사용 하 여 HDInsight Spark 클러스터를 관리 하 고"이이 문서의 뒷부분에 나오는 섹션.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에서 Spark Scala 응용 프로그램 실행 또는 디버그
또한 hello Spark 응용 프로그램 toohello 클러스터를 제출 하는 또 다른 방법은 좋습니다. Hello에서 hello 매개 변수를 설정 하 여 그렇게 할 수 **실행/디버그 구성을** IDE. 자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)를 참조하세요.

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트를 사용하여 HDInsight Spark 클러스터 액세스 및 관리
IntelliJ용 Azure 도구 키트를 사용하여 다양한 작업을 수행할 수 있습니다.

### <a name="access-hello-job-view"></a>액세스 hello 작업 보기
1. Azure 탐색기에서 확장 **HDInsight**hello Spark 클러스터 이름을 확장 하 고 다음 선택 **작업**합니다.  

    ![작업 보기 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Hello 오른쪽 창에서 hello **Spark 작업 보기** hello 클러스터에서 실행 된 모든 hello 응용 프로그램 탭에 표시 됩니다. 보려는 toosee 자세히 hello 응용 프로그램의 hello 이름을 선택 합니다.

    ![응용 프로그램 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay 기본 실행 중인 작업 정보를 hello 작업 그래프를 가리키도록 합니다. 모든 작업을 생성 하는 정보와 tooview hello 단계 그래프 hello 작업 그래프에서 노드를 선택 합니다.

    ![작업 단계 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview 자주 사용 되는 로그와 같은 *드라이버 Stderr*, *드라이버 Stdout*, 및 *디렉터리 정보*선택, hello **로그** 탭 합니다.

    ![로그 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. 또한 hello hello 창의 맨 아래에 링크를 선택 하 여 hello Spark 기록 UI 및 hello hello 응용 프로그램 수준에서 YARN UI를 볼 수 있습니다.

### <a name="access-hello-spark-history-server"></a>Hello Spark 기록 서버에 액세스
1. Azure 탐색기에서 **HDInsight**를 확장하고, 마우스 오른쪽 단추로 Spark 클러스터 이름을 클릭한 다음 **Spark 기록 UI 열기**를 선택합니다. 

2. 메시지가 나타나면 hello 클러스터를 설정할 때 지정 하는 hello 클러스터 관리 자격 증명을 입력 합니다.

3. 대시보드에서 hello Spark 기록 서버 hello 응용 프로그램 실행이 방금 완료에 대 한 응용 프로그램 이름 toolook hello를 사용할 수 있습니다. Hello 앞에 코드를 사용 하 여 hello 응용 프로그램 이름을 설정 `val conf = new SparkConf().setAppName("MyClusterApp")`합니다. 따라서 Spark 응용 프로그램 이름은 **MyClusterApp**입니다.

### <a name="start-hello-ambari-portal"></a>Hello Ambari 포털 시작
1. Azure 탐색기에서 **HDInsight**를 확장하고, 마우스 오른쪽 단추로 Spark 클러스터 이름을 클릭한 다음 **클러스터 관리 포털(Ambari) 열기**를 선택합니다. 

2. 메시지가 나타나면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다. 이러한 자격 증명 hello 클러스터 설치 과정에서 지정 합니다.

### <a name="manage-azure-subscriptions"></a>Azure 구독 관리
기본적으로 IntelliJ 용 Azure 도구 키트는 모든 Azure 구독에서 hello Spark 클러스터를 나열 합니다. 필요한 경우 tooaccess hello 구독을 지정할 수 있습니다. 

1. Azure 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Azure** 루트 노드를 선택한 후 **구독 관리**합니다. 

2. 선택을 취소 hello 확인란 다음 toohello 구독 tooaccess, 원하는 되 고 다음을 선택 하지 않는 hello 대화 상자에서 **닫기**합니다. 선택할 수도 있습니다 **로그 아웃** toosign Azure 구독에서 하려는 경우.

## <a name="run-a-spark-scala-application-locally"></a>로컬로 Spark Scala 응용 프로그램 실행
사용할 수 있습니다 Azure 도구 키트 IntelliJ toorun Spark Scala 응용 프로그램에 대 한 로컬 워크스테이션에 설치 합니다. hello 응용 프로그램 일반적으로 액세스 하지 않기 필요 toocluster 주고받는 저장 컨테이너 및 실행 하 고 로컬로 테스트할 수 있습니다.

### <a name="prerequisite"></a>필수 요소
에 설명 된 대로 예외를 hello 로컬 Spark Scala 응용 프로그램을 Windows 컴퓨터에서 실행 하는 동안 발생할 수 있습니다 [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)합니다. hello 예외가 Windows에서 WinUtils.exe 없기 때문에 발생 합니다. 

tooresolve이이 오류를 [hello 실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 위치와 같은 **C:\WinUtils\bin**합니다. 그런 다음 hello 환경 변수를 추가 **HADOOP_HOME**, 너무 hello hello 변수 값을 설정 하 고**C\WinUtils**합니다.

### <a name="run-a-local-spark-scala-application"></a>로컬 Spark Scala 응용 프로그램 실행
1. IntelliJ IDEA를 시작하고 프로젝트를 만듭니다. 

2. Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.
   
    a. **HDInsight** > **HDInsight의 Spark 로컬 실행 샘플(Scala)**을 선택합니다.

    b. Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.

      * Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**
      * **SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한

    ![hello 새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. **다음**을 선택합니다.
 
4. Hello 다음 창에서 수행 hello를 수행 합니다.
   
    a. 프로젝트 이름 및 위치를 입력합니다.

    b. Hello에 **프로젝트 SDK** 드롭 다운 목록 1.7 버전 보다 최신인 Java 버전을 선택 합니다.

    c. Hello에 **Spark 버전** 드롭 다운 목록, 버전, 선택 hello Scala toouse 원하는: Scala Spark 2.0 또는 Scala 2.11.x 2.10.x Spark 1.6에 대 한 합니다.

    ![hello 새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. **마침**을 선택합니다.

6. 샘플 코드를 추가 하는 hello 템플릿 (**LogQuery**) hello에서 **src** 폴더를 컴퓨터에 로컬로 실행할 수 있습니다.
   
    ![LogQuery 위치](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. 마우스 오른쪽 단추로 클릭 hello **LogQuery** 응용 프로그램을 마우스 선택 **실행 'LogQuery'**합니다. Hello에 **실행** 탭 hello 다음과 같은 출력 hello 맨 아래에 표시 합니다.
   
   ![Spark 응용 프로그램 로컬 실행 결과](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>IntelliJ에 대 한 기존 IntelliJ 아이디어 응용 프로그램 toouse Azure 도구 키트 변환
Hello Spark Scala는 기존 응용 프로그램에서에서 만든 IntelliJ 아이디어 toobe Azure 도구 키트 호환 IntelliJ에 대 한 변환할 수 있습니다. 그런 다음 hello 플러그 인 toosubmit hello 응용 프로그램 tooan HDInsight Spark 클러스터를 사용할 수 있습니다.

1. 응용 프로그램에 대해 기존 Spark Scala IntelliJ 아이디어를 통해 생성 된, hello 관련된.iml 파일을 엽니다.

2. Hello 루트에 수준은 **모듈** hello 다음과 같은 요소:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Hello 요소 tooadd 편집 `UniqueKey="HDInsightTool"` 하는 hello 하므로 **모듈** 요소 hello 다음과 같습니다.
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Hello 변경 내용을 저장 합니다. 이제 응용 프로그램이 IntelliJ용 Azure 도구 키트와 호환됩니다. 프로젝트 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 여 테스트할 수 있습니다. hello 팝업 메뉴에는 이제 hello 옵션에 **Spark 응용 프로그램 제출 tooHDInsight**합니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>로컬 실행에서 *더 큰 힙 크기를 사용하세요.* 오류 발생
로컬 실행 하는 동안 32 비트 Java SDK를 사용 하 여 Spark 1.6에서 다음 오류 hello를 발생할 수 있습니다.

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

이러한 오류 hello 힙 크기 Spark toorun에 없기 때문에 발생 합니다. Spark에는 적어도 471MB가 필요합니다. 자세한 내용은 [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081)을 참조하세요. 하나의 간단한 솔루션은 64 비트 Java SDK toouse입니다. Hello 다음 옵션을 추가 하 여 IntelliJ의 hello JVM 설정 또한 변경할 수 있습니다.

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![IntelliJ에 "VM 옵션" 상자 옵션 toohello 추가](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>FAQ
응용 프로그램 tooAzure 데이터 레이크 저장소 toosubmit 선택 **Interactive'** hello Azure 로그인 프로세스 중 모드입니다. **자동화된** 모드를 선택하는 경우 오류가 발생할 수 있습니다.

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

현재 이 오류는 해결했습니다. 어떤 로그인 방법으로 Azure 데이터 레이크 클러스터 toosubmit 응용 프로그램을 선택할 수 있습니다.

## <a name="feedback-and-known-issues"></a>사용자 의견 및 알려진 문제
현재 직접 Spark 출력 보기는 지원되지 않습니다.

제안 또는 피드백이 있거나 이 플러그 인을 사용할 때 문제가 발생하는 경우 hdivstool@microsoft.com으로 메일을 보내 주시기 바랍니다.

## <a name="seealso"></a>다음 단계
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>데모
* Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* 원격 디버그 (비디오): [HDInsight 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트 사용](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [Spark와 기계 학습: HVAC 데이터를 사용 하 여 온도 구축 하는 HDInsight tooanalyze에서 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight toobuild 실시간 스트리밍 응용 프로그램에서 사용 하 여 Spark Spark 스트리밍:](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [Azure 도구 키트를 사용 하 여 VPN 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [SSH 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트를 사용 합니다.](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

