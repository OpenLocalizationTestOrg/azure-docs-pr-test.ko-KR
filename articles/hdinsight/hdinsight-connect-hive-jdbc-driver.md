---
title: "Azure HDInsight-hello JDBC 드라이버를 통해 Hive aaaQuery | Microsoft Docs"
description: "HDInsight의 Java 응용 프로그램 toosubmit 하이브 쿼리 tooHadoop에서 hello JDBC 드라이버를 사용 합니다. 프로그래밍 방식으로 및 hello 스 쿼 럴 SQL client에서 연결 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>HDInsight의 hello JDBC 드라이버를 통해 하이브 쿼리

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Toouse hello JDBC 드라이버는 Java 응용 프로그램 toosubmit 하이브에서에서 Azure HDInsight의 tooHadoop를 쿼리 하는 방법에 대해 알아봅니다. 이 문서에서 hello 정보를 보여 줍니다 방법을 tooconnect 프로그래밍 방식으로 고 hello 스 쿼 럴 SQL 클라이언트입니다.

Hello 하이브 JDBC 인터페이스에 대 한 자세한 내용은 참조 하십시오. [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)합니다.

## <a name="prerequisites"></a>필수 조건

* HDInsight 클러스터의 Hadoop. Linux 또는 Windows 기반의 클러스터가 작동합니다.

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 3.3 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL은 JDBC 클라이언트 응용 프로그램입니다.

* hello [개발자 키트 JDK (Java) 버전 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상.

* [Apache Maven](https://maven.apache.org). Maven은 프로젝트 빌드 Java 프로젝트에 대 한이 문서와 연결 된 hello 프로젝트에서 사용 되는 시스템입니다.

## <a name="jdbc-connection-string"></a>JDBC 연결 문자열

Azure에서 JDBC 연결 tooan HDInsight 클러스터는 넘는 443 이루어지고 hello 트래픽이 SSL을 사용 하 여 보호 됩니다. hello 클러스터 뒤 sit hello 공용 게이트웨이 hello 트래픽 toohello 포트를 HiveServer2에서 실제로 수신 대기를 리디렉션합니다. hello 다음은 연결 문자열의 예입니다.

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

대체 `CLUSTERNAME` HDInsight 클러스터의 hello 이름의 합니다.

## <a name="authentication"></a>인증

Hello 연결을 설정할 때 hello HDInsight 클러스터 관리자 이름 및 암호 tooauthenticate toohello 클러스터 게이트웨이 사용 해야 합니다. 스 쿼 럴 SQL과 같은 JDBC 클라이언트를 연결할 때 클라이언트 설정에서 hello 관리자 이름 및 암호를 입력 해야 합니다.

Java 응용 프로그램에서 연결을 설정할 때 hello 이름 및 암호 사용 해야 있습니다. 예를 들어 hello 다음 Java 코드 새 연결을 열고 hello 연결 문자열, 관리자 이름 및 암호를 사용 하 여:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>SQuirreL SQL 클라이언트를 사용하여 연결

스 쿼 럴 SQL은 HDInsight 클러스터와 하이브 쿼리를 사용 하는 tooremotely 실행 될 수 있는 JDBC 클라이언트입니다. hello 다음 단계에서는 가정 스 쿼 럴 SQL을 이미 설치 해야 합니다.

1. HDInsight 클러스터에서 hello 하이브 JDBC 드라이버를 복사 합니다.

    * 에 대 한 **Linux 기반 HDInsight**를 사용 하 여 hello 다음 단계 toodownload 필요한 hello jar 파일입니다.

        1. Hello 파일이 포함 된 디렉터리를 만듭니다. 예: `mkdir hivedriver`.

        2. 명령줄에서 사용 하 여 hello 다음 hello HDInsight 클러스터에서 toocopy hello 파일 명령:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            대체 `USERNAME` hello 클러스터에 대 한 hello SSH 사용자 계정 이름을 사용 합니다. 대체 `CLUSTERNAME` hello HDInsight 클러스터 이름을 사용 합니다.

    * 에 대 한 **Windows 기반 HDInsight**를 사용 하 여 hello 다음 단계 toodownload hello jar 파일입니다.

        1. Hello Azure 포털에서에서 HDInsight 클러스터를 선택한 다음 선택 hello **원격 데스크톱** 아이콘입니다.

            ![원격 데스크톱 아이콘](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Hello 원격 데스크톱 블레이드에서 hello를 사용 하 여 **연결** 단추 tooconnect toohello 클러스터입니다. Hello 원격 데스크톱을 사용 하지 않는 경우 hello 양식 tooprovide 사용자 이름 및 암호를 사용 하 여 다음 선택 **사용** hello 클러스터에 대 한 원격 데스크톱 tooenable 합니다.

            ![원격 데스크톱 블레이드](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            **연결**을 선택하면 .rdp 파일이 다운로드됩니다. 이 파일 toolaunch hello 원격 데스크톱 클라이언트를 사용 합니다. 메시지가 표시 되 면 hello 사용자 이름 및 원격 데스크톱 액세스를 위해 입력 한 암호를 사용 합니다.

        3. 연결 되 면 hello hello 원격 데스크톱 세션 tooyour 로컬 컴퓨터에서 다음 파일이 복사 합니다. `hivedriver`라는 이름의 로컬 디렉터리에 넣습니다.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > hello 버전 번호 hello 경로 및 파일 이름에 포함 된 클러스터에 대해 다를 수 있습니다.

        4. Hello 파일 복사 완료 hello 원격 데스크톱 세션 연결을 끊습니다.

2. Hello 스 쿼 럴 SQL 응용 프로그램을 시작 합니다. Hello 창의 hello 왼쪽에서 선택 **드라이버**합니다.

    ![Hello hello 창 왼쪽에 드라이버 탭](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Hello 위쪽 hello에 hello 아이콘에서 **드라이버** 대화 상자에서 선택 hello  **+**  아이콘 toocreate 드라이버입니다.

    ![드라이버 아이콘](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. Hello 드라이버 추가 대화 상자에서 다음 정보는 hello를 추가 합니다.

    * **이름**: Hive
    * **예제 URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **추가 클래스 경로**: 이전에 다운로드 한 hello 추가 단추 tooadd hello jar 파일 사용
    * **클래스 이름**: org.apache.hive.jdbc.HiveDriver

   ![드라이버 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   클릭 **확인** toosave 이러한 설정 합니다.

5. Hello 스 쿼 럴 SQL 창의 hello 왼쪽에서 선택 **별칭**합니다. Hello 클릭  **+**  아이콘 toocreate 연결 별칭입니다.

    ![새 별칭 추가](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Hello에 대 한 값을 사용 하 여 hello 다음 **추가 별칭** 대화 상자.

    * **이름**: Hive on HDInsight

    * **드라이버**: 사용 하 여 hello 드롭다운 tooselect hello **하이브** 드라이버

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        대체 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.

    * **사용자 이름**: HDInsight 클러스터에 대 한 hello 클러스터 로그인 계정 이름입니다. hello 기본값은 `admin`합니다.

    * **암호**: hello 클러스터 로그인 계정에 대 한 hello 암호입니다.

 ![별칭 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    사용 하 여 hello **테스트** 연결이 작동 hello 단추 tooverify 합니다. 때 **연결할: HDInsight의 Hive** 선택 대화 상자가 나타나면 **연결** tooperform hello 테스트 합니다. 표시 hello 테스트에 성공 하면는 **성공적으로 연결** 대화 상자.

    별칭을 사용 하 여 hello toosave hello 연결 **확인** hello 아래쪽 hello의 단추 **추가 별칭** 대화 상자.

7. Hello에서 **연결할** 스 쿼 럴 SQL의 hello 위쪽 드롭다운 선택 **HDInsight의 Hive**합니다. 메시지가 표시되면 **연결**을 선택합니다.

    ![연결 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. 연결 되 면 다음 hello SQL 쿼리 대화 상자에 쿼리를 클릭 한 hello hello 입력 **실행** 아이콘입니다. hello 결과 영역을 hello hello 쿼리 결과 보여 줍니다.

        select * from hivesampletable limit 10;

    ![결과를 포함한 sql 쿼리 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Java 응용 프로그램 예제에서 연결

HDInsight의 Java 클라이언트 tooquery 하이브를 사용 하는 예제에서 제공 됩니다. [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)합니다. Hello 리포지토리 toobuild의 hello 지침에 따르고 hello 샘플을 실행 합니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>예기치 않은 오류가 발생 오류가 tooopen SQL 연결

**증상**: 버전 3.3 또는 3.4 tooan HDInsight 클러스터를 연결할 때 예기치 않은 오류가 발생 한 오류에 나타날 수 있습니다. 이 오류에 대 한 스택 추적 hello hello 다음 줄으로 시작 됩니다.

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**원인**:이 오류는 스 쿼 럴 및 hello hello 하이브 JDBC 구성 요소에 필요한 하나에서 사용 하는 hello commons codec.jar 파일의 hello 버전 불일치로 인해 발생 합니다.

**해결 방법**: toofix이이 오류를 사용 하 여 hello 다음 단계:

1. HDInsight 클러스터에서 hello commons 코덱 jar 파일을 다운로드 합니다.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. 스 쿼 럴을 종료 하 고 스 쿼 럴 시스템에 설치 되어 있는 되 toohello 디렉터리 이동 하십시오. Hello 아래의 hello 스 쿼 럴 디렉터리에서 `lib` 바꾸기 hello 기존 commons-codec.jar hello HDInsight 클러스터에서 다운로드 한 hello로 디렉터리입니다.

3. SQuirreL을 다시 시작합니다. HDInsight의 tooHive 연결할 때 hello 오류가 발생 하지 않습니다.

## <a name="next-steps"></a>다음 단계

이제는 어떻게 하이브를 사용 하 여 hello 뒤와 toouse JDBC toowork 링크 tooexplore Azure HDInsight와 다른 방법으로 toowork 방법을 배웠습니다.

* [데이터 tooHDInsight 업로드](hdinsight-upload-data.md)
* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 MapReduce 작업 사용](hdinsight-use-mapreduce.md)
