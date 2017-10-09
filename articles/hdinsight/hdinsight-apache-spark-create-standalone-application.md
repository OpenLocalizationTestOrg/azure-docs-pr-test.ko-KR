---
title: "Azure HDInsight Spark 클러스터에서 aaaCreate Scala 앱 toorun | Microsoft Docs"
description: "Hello IntelliJ 아이디어를 제공한 Scala에 대 한 시스템 및 기존 Maven 때 전형 빌드 Scala Apache Maven으로 작성 한 Spark 응용 프로그램을 만듭니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>HDInsight의 Apache Spark 클러스터에서 Scala Maven 응용 프로그램 toorun 만들기

자세한 내용은 방법 toocreate Scala IntelliJ 아이디어 Maven을 사용 하 여 작성 한 Spark 응용 프로그램입니다. hello 아티클은 hello 시스템을 작성 하 고 IntelliJ 아이디어를 제공한 Scala에 대 한 기존 Maven 때 전형으로 시작 하는 대로 Apache Maven을 사용 합니다.  IntelliJ 아이디어에 Scala 응용 프로그램을 만드는 단계를 수행 하는 hello 포함 됩니다.

* Maven hello 빌드 시스템으로 사용 합니다.
* 프로젝트 개체 모델 (POM) 파일 tooresolve Spark 모듈 종속성을 업데이트 합니다.
* Scala에서 응용 프로그램을 작성합니다.
* 제출 된 tooHDInsight Spark 클러스터 될 수 있는 jar 파일을 생성 합니다.
* 리비를 사용 하 여 Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.

> [!NOTE]
> 또한 HDInsight 반복 되는 개념 IntelliJ 플러그 인 도구 tooease hello 프로세스 만들기 및 제출 하는 응용 프로그램 tooan Linux에서 HDInsight Spark 클러스터를 제공 합니다. 자세한 내용은 참조 [IntelliJ 아이디어 toocreate 용 HDInsight 도구 플러그인을 사용 하 여 Spark 응용 프로그램을 제출 하 고](hdinsight-apache-spark-intellij-tool-plugin.md)합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.
* Oracle Java Development 키트. [여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.
* Java IDE. 이 문서에서는 IntelliJ IDEA 15.0.1을 사용합니다. [여기](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.

## <a name="install-scala-plugin-for-intellij-idea"></a>IntelliJ IDEA용 Scala 플러그 인 설치
IntelliJ 아이디어 설치 Scala 플러그 인을 사용 하도록 설정 하지 확인 하지 못했습니다 IntelliJ 아이디어를 시작 하 고 hello 단계 tooinstall hello 플러그 인을 다음을 수행 합니다.

1. IntelliJ IDEA를 시작하고 시작 화면에서 **구성**을 클릭한 다음 **플러그 인**을 클릭합니다.
   
    ![scala 플러그 인 활성화](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Hello 다음 화면에서 클릭 **플러그 인 설치 JetBrains** hello 하단 왼쪽된 모서리 쪽에서 합니다. Hello에 **JetBrains 플러그 인 찾아보기** 열리면 Scala 검색 하 고 클릭 한 다음 대화 상자가 **설치**합니다.
   
    ![scala 플러그 인 설치](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Hello 플러그 인이 성공적으로 설치 된 후 클릭 hello **IntelliJ 아이디어를 다시 시작 단추** toorestart hello IDE.

## <a name="create-a-standalone-scala-project"></a>독립 실행형 Scala 프로젝트 만들기
1. IntelliJ IDEA를 시작하고 새 프로젝트를 만듭니다. Hello 새 프로젝트 대화 상자에서 확인 클릭 및 선택 항목을 다음 hello **다음**합니다.
   
    ![Maven 프로젝트 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * 선택 **Maven** hello 프로젝트 형식을 합니다.
   * **프로젝트 SDK**를 지정합니다. 새로 만들기를 클릭 하 고 toohello Java 설치 디렉터리를 일반적으로 이동 `C:\Program Files\Java\jdk1.8.0_66`합니다.
   * 선택 hello **아키타 로부터 만들기** 옵션입니다.
   * 아키타의 hello 목록에서 선택 **tools.archetypes:scala 아키타 단순 org.scala**합니다. Hello 오른쪽 디렉터리 구조를 만들고 필요한 hello 기본 종속성 toowrite Scala 프로그램을 다운로드 합니다.
2. **GroupId**, **ArtifactId** 및 **버전**에 관련 값을 제공합니다. **다음**을 누릅니다.
3. Hello 다음 대화 상자에서 지정할 수 있는 Maven 홈 디렉터리 및 기타 사용자 설정, hello 기본값을 적용 하 고 클릭 **다음**합니다.
4. Hello 마지막 대화 상자에서 프로젝트 이름 및 위치를 지정 하 고 클릭 **마침**합니다.
5. Hello 삭제 **MySpec.Scala** 파일 **src\test\scala\com\microsoft\spark\example**합니다. Hello 응용 프로그램에 대 한이 필요 하지 않습니다.
6. 필요한 경우에 hello 기본 소스 및 테스트 파일을 이름을 바꿉니다. Hello IntelliJ 아이디어에에서 hello 왼쪽된 창에서 이동 너무**src\main\scala\com.microsoft.spark.example**합니다. 마우스 오른쪽 단추로 클릭 **App.scala**, 클릭 **리팩터링**, 이름 바꾸기 파일을 클릭 하 고 hello 대화 상자에서 hello hello 응용 프로그램에 대 한 새 이름을 입력 한 다음 **리팩터링**합니다.
   
    ![파일 이름 바꾸기](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. Hello 이후 단계에서는 hello Spark Scala 응용 프로그램에 대 한 hello pom.xml toodefine hello 종속성을 업데이트 합니다. 이러한 종속성에 대 한 toobe 다운로드 하 고 자동으로 해결 Maven을 적절 하 게 구성 해야 합니다.
   
    ![자동 다운로드를 위해 Maven 구성](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. Hello에서 **파일** 메뉴를 클릭 하 여 **설정을**합니다.
   2. Hello에 **설정** 대화 상자에서 너무 이동**빌드, 실행, 배포** > **빌드 도구** > **Maven**  >  **가져오기**합니다.
   3. Hello 옵션을 너무 선택**가져오기 Maven 프로젝트를 자동으로**합니다.
   4. **적용**을 클릭한 다음 **확인**을 클릭합니다.
8. Hello Scala 소스 파일 tooinclude 응용 프로그램 코드를 업데이트 합니다. 및 hello hello 코드 다음에 함께 존재 하는 샘플 코드를 대체 열고 hello 변경 내용을 저장 합니다. 이 코드 hello HVAC.csv (모든 HDInsight Spark 클러스터에서 사용 가능)에서 hello 데이터를 읽고, hello에 있는 행만 한 자릿수 hello 6 번째 열을 검색 및 너무 hello 출력을 기록**/HVACOut** hello 기본 저장소 hello 클러스터에 대 한 컨테이너입니다.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Hello pom.xml를 업데이트 합니다.
   
   1. 내에서 `<project>\<properties>` hello 다음 추가:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. 내에서 `<project>\<dependencies>` hello 다음 추가:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      변경 내용을 toopom.xml를 저장 합니다.
10. Hello.jar 파일을 만듭니다. IntelliJ IDEA는 프로젝트의 아티팩트로 JAR을 작성할 수 있습니다. Hello 다음 단계를 수행 합니다.
    
    1. Hello에서 **파일** 메뉴를 클릭 하 여 **프로젝트 구조**합니다.
    2. Hello에 **프로젝트 구조** 대화 상자에서 클릭 **아티팩트** 다음 hello 및 기호를 클릭 합니다. Hello 팝업 대화 상자에서 클릭 **JAR**, 클릭 하 고 **종속성이 있는 모듈에서**합니다.
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. Hello에 **모듈에서 JAR 만들** 대화 상자에서 hello 줄임표를 클릭 (![줄임표](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) hello에 대 한 **Main 클래스**합니다.
    4. Hello에 **Main 클래스 선택** 대화 상자, 기본적으로 표시 하 고 클릭 선택 hello 클래스 **확인**합니다.
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. Hello에 **모듈에서 JAR 만들** 대화 상자, 반드시 해당 hello 옵션 너무**toohello 대상 JAR 추출** 을 선택한 다음 클릭 **확인**합니다. 이렇게 하면 모든 종속성이 있는 단일 JAR이 만들어집니다.
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. hello 출력 레이아웃 탭 hello Maven 프로젝트의 일부분으로 포함 된 모든 hello jar를 나열 합니다. 선택할 수 있으며 더는 hello Scala 응용 프로그램 삭제 hello 의존 하지 않고 직접입니다. 제거할 수는 여기 만들기는 hello 응용 프로그램에 대 한 마지막을 제외 하 고 모두 hello (**SparkSimpleApp 컴파일 출력**). Hello jar toodelete를 선택 하 고 hello를 클릭 한 다음 **삭제** 아이콘입니다.
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        있는지 확인 **확인을 토대로** 내용이 해당 hello jar hello 프로젝트를 작성 하거나 업데이트할 때마다 생성 되는 확인란을 선택 합니다. **적용**을 클릭한 다음 **확인**을 클릭합니다.
    7. Hello 메뉴 모음에서 **빌드**, 클릭 하 고 **프로젝트 만들기**합니다. 클릭할 수도 있습니다 **빌드 아티팩트** toocreate hello jar. hello 출력 jar 아래에 생성 됩니다 **\out\artifacts**합니다.
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Hello Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.
수행 해야 toorun hello hello 클러스터에서 응용 프로그램을 hello 다음:

* **Hello 응용 프로그램 jar toohello Azure 저장소 blob 복사** hello 클러스터와 연결 된 합니다. 사용할 수 있습니다 [ **AzCopy**](../storage/common/storage-use-azcopy.md), 명령줄 유틸리티, toodo 되므로 명령입니다. Tooupload 데이터를 사용할 수 있는 다른 클라이언트를도 많이 있습니다. [HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.
* **원격으로 리비 toosubmit 응용 프로그램 작업을 사용 하 여** toohello Spark 클러스터입니다. HDInsight의 Spark 클러스터 리비 REST 끝점 tooremotely 전송 Spark 작업을 노출 하는 포함 되어 있습니다. 자세한 내용은 [HDInsight의 Spark 클러스터와 함께 Livy를 사용하여 원격으로 Spark 작업 제출](hdinsight-apache-spark-livy-rest-interface.md)을 참조하세요.

## <a name="next-step"></a>다음 단계

이 방법에 대해 배웠습니다 문서 toocreate Spark scala 응용 프로그램입니다. 고급 toohello 다음 문서 toolearn 어떻게 toorun HDInsight Spark에이 응용 프로그램 사용 하 여 클러스터 리비 합니다.

> [!div class="nextstepaction"]
>[Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

