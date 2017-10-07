---
title: "aaaJava 사용자 정의 함수 (UDF)와 Azure HDInsight의 Hive | Microsoft Docs"
description: "어떻게 toocreate Java 기반 사용자 정의 알아봅니다 하이브를 사용 하는 함수 (UDF). 이 예에서는 UDF 텍스트 문자열 toolowercase의 테이블을 변환합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>HDInsight에서 Hive와 함께 Java UDF 사용

어떻게 toocreate Java 기반 사용자 정의 알아봅니다 하이브를 사용 하는 함수 (UDF). 이 예제에서 Java UDF hello 텍스트 문자열 tooall 소문자 문자의 테이블을 변환합니다.

## <a name="requirements"></a>요구 사항

* HDInsight 클러스터 

    > [!IMPORTANT]
    > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

    이 문서의 단계는 대부분 Windows 및 Linux 기반 클러스터 둘 다에서 작동합니다. 그러나 hello는 데 필요한 단계 tooupload hello 컴파일된 UDF toohello 클러스터 및 특정 tooLinux 기반 클러스터 되어 실행 됩니다. 링크에는 Windows 기반 클러스터와 함께 사용할 수 있는 tooinformation을 제공 됩니다.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 이상(또는 OpenJDK와 같은 이와 동등한 프로그램)

* [Apache Maven](http://maven.apache.org/)

* 텍스트 편집기 또는 Java IDE

    > [!IMPORTANT]
    > Hello Windows 클라이언트에서 Python 파일을 생성 하는 경우에 줄 끝으로 LF를 사용 하는 편집기를 사용 해야 합니다. 편집기를 사용 하는지 여부 LF 또는 CRLF 확실 하지 않은 경우 참조 hello [문제 해결](#troubleshooting) 제거에 대 한 단계 hello CR 문자에 대 한 섹션.

## <a name="create-an-example-java-udf"></a>예제 Java UDF 만들기 

1. 명령줄에서 다음 새 Maven 프로젝트 toocreate hello를 사용 합니다.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > PowerShell을 사용 하는 경우에 hello 매개 변수 주위에 따옴표를 넣어야 합니다. 예: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    이 명령은 라는 디렉터리를 만듭니다. **exampleudf**, hello Maven 프로젝트가 들어 있는입니다.

2. Hello 프로젝트를 만든 후 삭제 hello **exampleudf/src/test** hello 프로젝트의 일부로 만든 디렉터리에 있습니다.

3. 열기 hello **exampleudf/pom.xml**, hello 기존 항목 바꾸기 및 `<dependencies>` hello 다음과 같은 XML로 입력 합니다.

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    이러한 항목의 Hadoop 및 Hive HDInsight 3.5에 포함 된 hello 버전을 지정 합니다. Hadoop 및 HDInsight hello에서 제공 하는 하이브 hello 버전에서 정보를 찾을 수 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서.

    추가 `<build>` hello 앞 섹션 `</project>` hello hello 파일 끝에 줄. 이 섹션에는 다음과 같은 XML hello를 포함 되어야 합니다.

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```

    이러한 항목 toobuild 프로젝트 hello 하는 방법을 정의 합니다. 특히, hello Java 버전을 사용 하는 hello 하는 방법과 toobuild toohello 클러스터 배포에 대 한 uberjar 합니다.

    Hello 변경이 이루어진 후 hello 파일을 저장 합니다.

4. 이름 바꾸기 **exampleudf/src/main/java/com/microsoft/examples/App.java** 너무**ExampleUDF.java**, 편집기에서 hello 파일을 엽니다.

5. Hello hello 내용 바꾸기 **ExampleUDF.java** hello 다음과 같이 파일 다음 hello 파일을 저장 합니다.

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    이 코드는 문자열 값을 허용 하 고 hello 문자열의 소문자 버전을 반환 하는 UDF를 구현 합니다.

## <a name="build-and-install-hello-udf"></a>빌드 및 hello UDF를 설치 합니다.

1. 다음 명령은 toocompile hello를 사용 하 여 및 UDF hello 패키지:

    ```bash
    mvn compile package
    ```

    이 명령은 빌드하고 패키지 hello에 UDF hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` 파일입니다.

2. 사용 하 여 hello `scp` 명령 toocopy hello 파일 toohello HDInsight 클러스터입니다.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    대체 `myuser` hello 클러스터에 대 한 SSH 사용자 계정 사용 합니다. 대체 `mycluster` hello 클러스터 이름을 사용 합니다. 암호 toosecure hello SSH 계정을 사용 하는 경우 메시지 표시 tooenter hello 암호입니다. 인증서를 사용한 toouse hello를 할 수 있습니다 `-i` 매개 변수 toospecify hello 개인 키 파일입니다.

3. SSH를 사용 하 여 toohello 클러스터를 연결 합니다.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

4. Hello SSH 세션에서 hello jar 파일 tooHDInsight 저장소를 복사 합니다.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>하이브에서 hello UDF를 사용 하 여

1. Hello toostart hello Beeline 클라이언트 hello SSH 세션에서 다음을 사용 합니다.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    기본값은 hello를 사용 하 여이 명령에서는 **admin** 클러스터에 대 한 hello 로그인 계정에 대 한 합니다.

2. Hello에 도달 하 게 되 면 `jdbc:hive2://localhost:10001/>` 프롬프트 hello tooadd hello UDF tooHive 다음을 입력 하 고 함수로 노출 합니다.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > 이 예제에서는 Azure 저장소 hello 클러스터에 대 한 기본 저장소 있다고 가정 합니다. 클러스터에 데이터 레이크 저장소를 대신 사용 하는 경우 변경 hello `wasb:///` 너무 값`adl:///`합니다.

3. 테이블 toolower 소문자 문자열에서 검색 된 hello UDF tooconvert 값을 사용 합니다.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    선택 hello hello 테이블에서 장치 플랫폼 (Android, Windows, iOS 등)이이 쿼리 hello 문자열 toolower 대/소문자를 변환한 다음이 표시 합니다. hello 출력 텍스트 다음 유사한 toohello 나타납니다.

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a>다음 단계

하이브와 다른 방법으로 toowork, 참조 [HDInsight를 사용 하 여 하이브](hdinsight-use-hive.md)합니다.

Hive User-Defined 함수에 대 한 자세한 내용은 참조 하십시오. [하이브 연산자 및 사용자 정의 함수](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) hello 하이브 wiki apache.org에서의 섹션입니다.
