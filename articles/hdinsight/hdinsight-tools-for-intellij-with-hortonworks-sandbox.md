---
title: "Hortonworks 샌드박스와 IntelliJ 용 Azure 도구 키트 aaaUse | Microsoft Docs"
description: "자세한 내용은 Hortonworks 샌드박스와 IntelliJ 용 Azure 도구 키트에서 toouse HDInsight 도구 방법입니다."
keywords: "hadoop 도구,hive 쿼리,intellij,hortonworks 샌드박스,intellij용 azure 도구 키트"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용

IntelliJ toodevelop Apache Scala 응용 프로그램 및 테스트에 대 한 toouse HDInsight 도구에 응용 프로그램을 hello 하는 방법에 대해 알아봅니다 [Hortonworks 샌드박스](http://hortonworks.com/products/sandbox/) 워크스테이션에서 실행 합니다. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/)는 컴퓨터 소프트웨어를 개발하기 위한 Java IDE(통합 개발 환경)입니다. 개발 하에서 Hortonworks 샌드박스 응용 프로그램을 테스트 한 후 이동할 수 있습니다 너무[Azure HDInsight](hdinsight-hadoop-introduction.md)합니다.

## <a name="prerequisites"></a>필수 조건

이 자습서를 시작하기 전에 다음이 있어야 합니다.

- 로컬 환경에서 실행되는 Hortonworks 샌드박스의 HDP(Hortonworks Data Platform) 2.4. tooconfigure HDP, 참조 [가상 컴퓨터에서 Hadoop 샌드박스와 hello Hadoop 에코 시스템에서 시작](hdinsight-hadoop-emulator-get-started.md)합니다. 
    >[!NOTE]
    >IntelliJ용 HDInsight Tools는 HDP 2.4에서만 테스트되었습니다. tooget HDP 2.4 확장 **Hortonworks 샌드박스 보관** hello에 [Hortonworks 샌드박스 다운로드 사이트](http://hortonworks.com/downloads/#sandbox)합니다.

- [JDK(Java Developer Kit) 버전 1.8 이상](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) IntelliJ에 대 한 hello Azure 도구 키트 JDK가 필요 합니다.

- [IntelliJ 아이디어 community edition](https://www.jetbrains.com/idea/download) hello로 [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) 플러그 인 및 hello [IntelliJ 용 Azure 도구 키트](../azure-toolkit-for-intellij.md) 플러그 인 합니다. IntelliJ 용 HDInsight 도구 hello IntelliJ 용 Azure 도구 키트의 일부분으로 제공 됩니다. 

  플러그 인 tooinstall hello, 다음 hello지 않습니다.

  1. IntelliJ IDEA를 엽니다.
  2. Hello에 **시작** 화면에서 **구성**를 선택한 후 **플러그 인**합니다.
  3. 선택 **플러그 인 설치 JetBrains** hello 왼쪽 아래 모퉁이에 있습니다.
  4. 에 대 한 검색 함수 toosearch hello를 사용 하 여 **Scala**를 선택한 후 **설치**합니다.
  5. 선택 **IntelliJ 아이디어를 다시 시작** toocomplete hello 설치 합니다.
  6. 4, 5 단계를 반복 tooinstall hello **IntelliJ 용 Azure 도구 키트**합니다. 자세한 내용은 참조 [IntelliJ 용 Azure 도구 키트 설치 hello](../azure-toolkit-for-intellij-installation.md)합니다.

## <a name="create-a-spark-scala-application"></a>Spark Scala 응용 프로그램 만들기

이 섹션에서는 IntelliJ IDEA를 사용하여 샘플 Scala 프로젝트를 만듭니다. 다음 섹션인 hello hello 프로젝트를 제출 하기 전에 IntelliJ 아이디어 toohello Hortonworks 샌드박스 (에뮬레이터)를 연결 합니다.

1. 워크스테이션에서 IntelliJ IDEA를 엽니다. Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.

   a. **HDInsight** > **HDInsight의 Spark(Scala)**를 선택합니다.

   b. Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.

    * Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**
    * **SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한

   ![hello 새 프로젝트 대화 상자](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. **다음**을 선택합니다.

3. Hello에 다음 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.

    ![IntelliJ Scala 프로젝트 속성 만들기](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. Hello에 **프로젝트 이름을** 상자에 프로젝트 이름을 입력 합니다.

    b. Hello에 **프로젝트 위치** 상자에 프로젝트 위치를 입력 합니다.

    c. 다음 toohello **프로젝트 SDK** 드롭 다운 목록 **새로**선택, **JDK**, Java JDK 버전 1.7 이상을의 hello 폴더를 지정 합니다. 선택 **Java 1.8** hello Spark 2.x 클러스터 또는 선택에 대 한 **Java 1.7** hello Spark 1.x 클러스터에 대 한 합니다. hello 기본 위치는 C:\Program Files\Java\jdk1.8.x_xxx입니다.

    d. Hello에 **Spark 버전** 드롭 다운 목록에서 Scala 프로젝트 만들기 마법사 Spark SDK 및 Scala SDK에 대 한 hello 적절 한 버전을 통합 합니다. Hello Spark 클러스터 버전이 2.0 보다 이전 이면 선택 **1.x 멤버**합니다. 그렇지 않은 경우 **Spark2.x**를 선택합니다. 이 예제에서는 Spark 1.6.2(Scala 2.10.5)를 사용합니다. Scala 표시 hello 저장소를 사용 하 고 있는지 확인 2.10.x 합니다. Scala 표시 hello 저장소를 사용 하지 마십시오 2.11.x 합니다.

4. **마침**을 선택합니다.

5. 경우 hello **프로젝트** 뷰가 이미 열려 있지 않으면, 키를 눌러 **Alt + 1** tooopen 것입니다.

6. **프로젝트 탐색기**hello 프로젝트를 확장 한 다음 선택, **src**합니다.

7. 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**를 선택한 후 **Scala 클래스**합니다.

8. Hello에 **이름** 상자 hello에 이름을 입력 합니다 **종류** 상자 **개체**를 선택한 후 **확인**합니다.

    ![hello 새 Scala 클래스 만들기 창](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. Hello.scala 파일에서 코드 다음 hello를 붙여 넣습니다.

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. Hello에 **빌드** 메뉴 선택 **빌드 프로젝트**합니다. Hello 컴파일 성공적으로 완료 되었음을 나타내는 있는지 확인 합니다.


## <a name="link-toohello-hortonworks-sandbox"></a>Toohello Hortonworks 샌드박스 연결

Tooa Hortonworks 샌드박스 (에뮬레이터)를 클릭 하십시오. 기존 IntelliJ 응용 프로그램이 있어야 합니다.

toolink tooan 에뮬레이터 다음 hello지 않습니다.

1. IntelliJ에서 열기 hello 프로젝트입니다.

2. Hello에 **보기** 메뉴 선택 **도구 창을**를 선택한 후 **Azure 탐색기**합니다.

3. **Azure**를 확장하고 **HDInsight**를 마우스 오른쪽 단추로 클릭한 다음 **에뮬레이터에 연결**을 선택합니다.

4. Hello에 **링크는 새 에뮬레이터** 창의 hello Hortonworks 샌드박스의 hello 루트 계정에 대 한 구성 하 값 비슷한 toothose hello 스크린 샷, 뒤에 입력 한 다음 선택 하는 hello 암호를 입력 **확인** . 

   ![hello "링크는 새 에뮬레이터" 창](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. 선택 tooconfigure hello 에뮬레이터 **예**합니다.

Hello 에뮬레이터 성공적으로 연결 되 면 hello 에뮬레이터 (Hortonworks 샌드박스) hello HDInsight 노드에 나열 됩니다.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Hello Spark Scala 응용 프로그램 toohello Hortonworks 샌드박스 제출

IntelliJ 아이디어 toohello 에뮬레이터에 연결한 후에 프로젝트를 제출할 수 있습니다.

프로젝트 tooan 에뮬레이터 toosubmit 다음 hello지 않습니다.

1. **프로젝트 탐색기**를 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **제출 Spark 응용 프로그램 tooHDInsight**합니다.

2. 다음 hello지 않습니다.

    a. Hello에 **Spark 클러스터 (Linux에만 해당)** 드롭 다운 목록에서 지역 Hortonworks 샌드박스에 선택 합니다.

    b. Hello에 **Main 클래스 이름** 상자의 선택 하거나 hello 주 클래스 이름을 입력 합니다. 이 자습서에 대 한 hello 이름이 **GroupByTest**합니다.

3. **제출**을 선택합니다. hello 작업 제출 로그 hello Spark 제출 도구 창에 표시 됩니다.

## <a name="next-steps"></a>다음 단계

- IntelliJ, 용 HDInsight 도구를 사용 하 여 HDInsight의 toocreate Spark에 응용 프로그램 너무 이동 toolearn[HDInsight Spark Linux 클러스터에 대 한 IntelliJ toocreate Spark 응용 프로그램에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 여](hdinsight-apache-spark-intellij-tool-plugin.md)합니다.

- IntelliJ, 용 HDInsight 도구에 대 한 비디오 toowatch 너무 이동[Spark 개발을 위한 IntelliJ 용 HDInsight 도구 소개](https://www.youtube.com/watch?v=YTZzYVgut6c)합니다.

- toolearn toodebug Spark 응용 프로그램을 사용 하 여 hello toolkit SSH 통해 HDInsight에 원격으로 어떻게 이동 너무[SSH 통해 IntelliJ 용 Azure 도구 키트에 HDInsight 클러스터에서 Spark 응용 프로그램을 원격으로 디버그](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)합니다.

- toolearn toodebug Spark 응용 프로그램을 사용 하 여 VPN 통해 HDInsight에 원격으로 도구 키트 hello 방법 이동 너무[HDInsight Spark Linux 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 여](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)합니다.

- Eclipse toocreate Spark는 응용 프로그램에 대 한 HDInsight 도구 toouse 너무 이동 toolearn[Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구](hdinsight-apache-spark-eclipse-tool-plugin.md)합니다.

- Eclipse 용 HDInsight 도구에 대 한 비디오 toowatch 너무 이동[Eclipse toocreate Spark 응용 프로그램에 대 한 HDInsight 도구 사용](https://mix.office.com/watch/1rau2mopb6fha)합니다.
