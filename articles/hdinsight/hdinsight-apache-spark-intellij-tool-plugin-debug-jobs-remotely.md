---
title: "IntelliJ-HDInsight Spark에 원격으로 디버그 응용 프로그램에 대 한 도구 키트 aaaAzure | Microsoft Docs"
description: "자세한 내용은 방법 IntelliJ tooremotely 디버그 실행 중인 응용 프로그램 vpn 통해 HDInsight Spark 클러스터에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Azure 도구 키트를 사용 하 여 VPN 통해 HDInsight Spark에 원격으로 IntelliJ toodebug 응용 프로그램에 대 한

디버깅을 통해 원격으로 spark applicaltion ssh hello 방식 으로를 사용 하는 것이 좋습니다. 자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)를 참조하세요.

이 문서에서는 toouse IntelliJ toosubmit HDInsight Spark 클러스터에서 Spark 작업에 대 한 Azure 도구 키트의 HDInsight 도구 hello 하 고 다음 데스크톱 컴퓨터에서 원격으로 디버깅 하는 방법에 대 한 단계별 지침을 제공 합니다. toodo hello 상위 수준 단계를 수행 해야 하는.

1. 사이트 간 또는 지점 및 사이트 간 Azure 가상 네트워크를 만듭니다. 이 문서에 hello 단계는 사이트 간 네트워크를 사용 하는 가정 합니다.
2. Hello 사이트 및 사이트 간 Azure 가상 네트워크의 일부인 Azure HDInsight의 Spark 클러스터를 만듭니다.
3. Hello hello 클러스터 헤드 노드 및 데스크톱 연결 상태를 확인 합니다.
4. IntelliJ IDEA에서 Scala 응용 프로그램을 만들고 원격 디버깅을 위해 구성합니다.
5. 실행 하 고 hello 응용 프로그램을 디버깅 합니다.

## <a name="prerequisites"></a>필수 조건
* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.
* Oracle Java Development 키트. [여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.
* IntelliJ IDEA. 이 문서에서는 버전 2017.1을 사용합니다. [여기](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.
* IntelliJ용 Azure 도구 키트의 HDInsight 도구. IntelliJ에 대 한 HDInsight 도구를 사용할 수 hello IntelliJ 용 Azure 도구 키트의 일환으로 합니다. 에 대 한 지침은 어떻게 tooinstall hello Azure 도구 키트를 참조 하세요. [IntelliJ 용 Azure 도구 키트 설치 hello](../azure-toolkit-for-intellij-installation.md)합니다.
* IntelliJ IDEA에서 Azure 구독에 로그인. Hello 지침에 따라 [여기](hdinsight-apache-spark-intellij-tool-plugin.md)합니다.
* Windows 컴퓨터에서 원격 디버깅을 위해 Spark Scala 응용 프로그램을 실행 하는 동안 발생할 수에 설명 된 대로 예외 [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) tooa 누락 인해 발생 하는 Windows에서 WinUtils.exe 합니다. 이 오류를 해결 toowork를 수행 해야 [여기에서 실행 하는 hello 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 위치 **C:\WinUtils\bin**합니다. 그런 다음 환경 변수를 추가 해야 **HADOOP_HOME** 너무 hello hello 변수 값을 설정 하 고**C\WinUtils**합니다.

## <a name="step-1-create-an-azure-virtual-network"></a>1단계: Azure 가상 네트워크 만들기
아래 링크 toocreate Azure 가상 네트워크는 hello에서 hello 지침에 따라 하 고 hello 데스크톱 및 Azure 가상 네트워크 간의 hello 연결을 확인 합니다.

* [Azure 포털을 사용하여 사이트 간 VPN 연결로 VNet 만들기](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [PowerShell을 사용하여 사이트 간 VPN 연결로 VNet 만들기](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [PowerShell을 사용 하 여 지점 및 사이트 연결 tooa 가상 네트워크 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>2단계: HDInsight Spark 클러스터 만들기
또한 hello 만든 Azure 가상 네트워크의 일부인 Azure HDInsight의 Apache Spark 클러스터를 만들어야 합니다. 사용할 수 있는 hello 정보를 사용 하 여 [HDInsight에서 클러스터 만들기 Linux 기반](hdinsight-hadoop-provision-linux-clusters.md)합니다. 선택적 구성의 일부로 hello hello 이전 단계에서 만든 Azure 가상 네트워크를 선택 합니다.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>3 단계: 클러스터 헤드 노드에 hello와 데스크톱 사이 hello 연결을 확인 하십시오.
1. Hello 헤드 노드에의 hello IP 주소를 가져옵니다. Hello 클러스터에 대 한 Ambari UI를 엽니다. Hello 클러스터 블레이드에서 클릭 **대시보드**합니다.

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Hello 오른쪽 위 모서리에서 hello Ambari UI에서에서 클릭 **호스트**합니다.

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. 헤드 노드, 작업자 노드 및 zookeeper 노드 목록이 표시됩니다. hello headnodes 있는 hello **hn*** 접두사입니다. 첫 번째 헤드 노드에 hello를 클릭 합니다.

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Hello hello에서 열리는 hello 페이지 맨 아래에 **요약** 상자의 hello 헤드 노드에 및 hello 호스트 이름을 복사 hello IP 주소입니다.

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Hello IP 주소 및 hello 헤드 노드에 toohello의 hello 호스트 이름 포함 **호스트** toorun 원하는 및 hello Spark 작업을 원격으로 디버그 hello 컴퓨터에서 파일입니다. 이렇게 하면 toocommunicate hello IP 주소 뿐만 아니라 hello 호스트 이름을 사용 하 여 hello 헤드 노드에 사용 합니다.

   1. 관리자 권한으로 메모장을 엽니다. Hello 파일 메뉴에서 클릭 **열려** hello 호스트 파일의 toohello 위치를 이동 합니다. Windows 컴퓨터에서 `C:\Windows\System32\Drivers\etc\hosts`입니다.
   2. Hello toohello 다음 추가 **호스트** 파일입니다.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Toohello hello HDInsight 클러스터에서 사용 되는 Azure 가상 네트워크를 연결 하는 hello 컴퓨터에서 모두 hello headnodes hello IP 주소 뿐만 아니라 hello 호스트 이름을 사용 하 여 ping 수 있는지를 확인 합니다.
7. Hello 지침을 사용 하 여 클러스터 헤드 노드에 hello에 대 한 SSH [SSH를 사용 하 여 연결 tooan HDInsight 클러스터](hdinsight-hadoop-linux-use-ssh-unix.md)합니다. Hello 클러스터 헤드 노드에에서 hello 데스크톱 컴퓨터의 hello IP 주소를 ping 합니다. Hello 네트워크 연결에 대해 하나씩 toohello 컴퓨터를 할당 하는 연결 tooboth hello IP 주소를 테스트 해야 하 고 hello 컴퓨터 hello Azure 가상 네트워크에 대 한 다른 hello에 연결 되어 있습니다.
8. Hello도 다른 헤드 노드에 hello 단계를 반복 합니다.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>4 단계: IntelliJ Azure 도구 키트의 hello HDInsight 도구를 사용 하 여 Spark Scala 응용 프로그램을 만들고 원격 디버깅 구성
1. IntelliJ IDEA를 시작하고 새 프로젝트를 만듭니다. Hello 새 프로젝트 대화 상자에서 확인 클릭 및 선택 항목을 다음 hello **다음**합니다.

    ![Spark Scala 응용 프로그램 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Hello 왼쪽된 창에서 선택 **HDInsight**합니다.
   * Hello 오른쪽 창에서 선택 **(Scala) HDInsight의 Spark**합니다.
   * **다음**을 누릅니다.
2. Hello 다음 창의 hello 다음 프로젝트 세부 정보를 입력 한 다음 **마침**합니다.  
   - 프로젝트 이름과 프로젝트 위치를 제공합니다.
   - **프로젝트 SDK**의 경우 Spark 2.x 클러스터에 Java 1.8을 사용하고 Spark 1.x 클러스터에 Java 1.7을 사용합니다.
   - **Spark 버전**의 경우 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK.에 대한 적절한 버전을 통합합니다. 더 낮은 2.0 hello spark 클러스터 버전을 사용 하는 경우 선택 1.x 멤버입니다. 그렇지 않으면 Spark 2.x를 선택해야 합니다. 이 예제에서는 Spark 2.0.2(Scala 2.11.8)를 사용합니다.
       ![Spark Scala 응용 프로그램 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. hello Spark 프로젝트는 자동으로 만들 아티팩트입니다. toosee hello 아티팩트를 다음이 단계를 수행 합니다.

   1. Hello에서 **파일** 메뉴를 클릭 하 여 **프로젝트 구조**합니다.
   2. Hello에 **프로젝트 구조** 대화 상자를 클릭 **아티팩트** 만들어진 toosee hello 기본 아티팩트입니다.
   ![JAR 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      사용자 고유의 아티팩트를 만들 수도 있습니다 bly hello 클릭 하면  **+**  아이콘을 위 hello 이미지에서 강조 표시 됩니다.

4. 라이브러리 tooyour 프로젝트를 추가 합니다. 라이브러리를 tooadd hello 프로젝트 트리에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 **모듈 설정 열기**합니다. Hello에 **프로젝트 구조** hello 왼쪽된 창에서 대화 상자를 클릭 **라이브러리**, hello (+) 기호를 클릭 하 고 클릭 **에서 Maven**합니다.

    ![라이브러리 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    Hello에 **Maven 리포지토리에서 라이브러리 다운로드** 대화 상자, 검색 및 라이브러리를 수행 하는 hello를 추가 합니다.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. 복사 `yarn-site.xml` 및 `core-site.xml` hello에서 toohello 프로젝트를 추가 하 고 클러스터 헤드 노드에 있습니다. 다음 명령은 toocopy hello 파일이 hello를 사용 합니다. 사용할 수 있습니다 [Cygwin](https://cygwin.com/install.html) toorun hello 다음 `scp` hello 클러스터 headnodes에서 toocopy hello 파일 명령입니다.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Hello 클러스터 헤드 노드에 IP 주소 및 호스트 이름은 fo hello 호스트 hello 바탕 화면에 파일을 이미 추가 했으므로 hello를 사용할 수 있습니다 **scp** hello 방식으로 다음에 명령 합니다.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Hello에서 복사 하 여 이러한 파일 tooyour 프로젝트 추가 **/src** 예를 들어 프로그램 프로젝트 트리에서 폴더 `<your project directory>\src`합니다.
6. 업데이트 hello `core-site.xml` toomake hello 변경 내용을 수행 합니다.

   1. `core-site.xml`hello 클러스터와 연결 된 암호화 hello 키 toohello 저장소 계정이 포함 됩니다. Hello에 `core-site.xml` toohello 프로젝트, 바꾸기 hello hello 기본 저장소 계정에 연결 된 hello 실제 저장소 키로 암호화 된 키를 추가 합니다. [저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)를 참조하세요.

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Hello에서 항목을 다음 hello 제거 `core-site.xml`합니다.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Hello 파일을 저장 합니다.
7. 응용 프로그램에 대 한 hello 기본 클래스를 추가 합니다. Hello에서 **프로젝트 탐색기**를 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**, 클릭 하 고 **Scala 클래스**합니다.

    ![소스 코드 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. Hello에 **새 Scala 클래스 만들기** 대화 상자에서 대 한 이름을 제공 **종류** 선택 **개체**, 클릭 하 고 **확인**합니다.

    ![소스 코드 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. Hello에 `MyClusterAppMain.scala` 파일, 코드 다음 hello를 붙여 넣습니다. 이 코드 hello Spark 컨텍스트 연결을 만들고 시작 프로그램 `executeJob` hello 메서드에서 `SparkSample` 개체입니다.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. 8 단계와 9 단계 위에 새 Scala 개체 라는 tooadd 반복 `SparkSample`합니다. toothis 클래스 코드 다음 hello를 추가 합니다. 이 코드 hello HVAC.csv (모든 HDInsight Spark 클러스터에서 사용 가능)에서 hello 데이터를 읽고, hello hello CSV의에서 일곱 번째 열에 숫자를 하나만 hello 행을 검색 및 너무 hello 출력을 기록**/HVACOut** hello 기본 hello 클러스터에 대 한 저장소 컨테이너입니다.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. 8, 9 라는 새 클래스가 tooadd 위의 단계를 반복 `RemoteClusterDebugging`합니다. 이 클래스는 응용 프로그램 디버깅에 사용 되는 hello Spark 테스트 프레임 워크를 구현 합니다. 다음 코드 toohello hello 추가 `RemoteClusterDebugging` 클래스입니다.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     여기에 중요 한 사항이 toonote 몇:

   * 에 대 한 `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, Spark 어셈블리 JAR hello hello 지정된 경로에 hello 클러스터 저장소에 사용할 수 있는지 확인 합니다.
   * 에 대 한 `setJars`, hello 아티팩트 jar 만들어지는 hello 위치를 지정 합니다. 일반적으로 `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`입니다.
12. Hello에 `RemoteClusterDebugging` 클래스, hello를 마우스 오른쪽 단추로 클릭 `test` 키워드와 선택 **RemoteClusterDebugging 구성 만들기**합니다.

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Hello 대화 상자에서 hello 구성에 대 한 이름을 입력 하 고 hello를 선택 **종류 테스트** 으로 **테스트 이름**합니다. 기본적으로 다른 모든 값을 그대로 두고 **적용**을 클릭한 다음 **확인**을 클릭합니다.

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. 이제는 **원격 실행** 드롭 다운 hello 메뉴 모음에서 구성 합니다.

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>5 단계: hello 응용 프로그램을 디버그 모드에서 실행
1. IntelliJ 아이디어 프로젝트를 열고 `SparkSample.scala` 중단점 다음 too'val rdd1 만들고 '. 중단점을 만들기 위한 hello 팝업 메뉴에서 선택 **함수 executeJob에 줄**합니다.

    ![중단점 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Hello 클릭 **실행 디버그** 단추 다음 toohello **원격 실행** 구성 드롭 다운 toostart hello 응용 프로그램을 실행 합니다.

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Hello 프로그램 실행 hello 중단점에 도달 하면 표시 됩니다는 **디버거** hello 아래쪽 창의 탭 합니다.

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Hello 클릭 (**+**) 아이콘 tooadd hello 이미지 아래에 나와 있는 것 처럼 감시 합니다.

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Hello 변수 하기 전에 hello 응용 프로그램 중단 때문에 여기서 `rdd1` 를 사용 하 여 만들어진 hello 변수에서 처음 5 개 행을 hello은 무엇을 볼 수 있습니다이 조사식 `rdd`합니다. **ENTER**키를 누릅니다.

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    런타임 시 데이터와 디버그 terrabytes 쿼리할 수는 위의 hello 그림에서 볼 수 있는 방법을 응용 프로그램 진행 합니다. 예를 들어 위의 hello 이미지에 표시 된 hello 출력에 나타나면 해당 hello hello 출력의 첫 번째 행은 헤더가 있습니다. 이에 따라 필요한 경우 응용 프로그램 코드 tooskip hello 머리글 행을 수정할 수 있습니다.
5. Hello을 클릭할 수 있습니다 **Resume 프로그램** 아이콘 tooproceed와 응용 프로그램을 실행 합니다.

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Hello 응용 프로그램 성공적으로 완료 되 면 hello 다음과 같은 출력을 표시 됩니다.

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>데모
* Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* 원격 디버그 (비디오): [HDInsight 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트 사용](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [IntelliJ toocreate에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 고 스파크 Scala 개 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [SSH 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트를 사용 합니다.](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
