---
title: "Hadoop-Azure HDInsight에 대 한 Java MapReduce aaaCreate | Microsoft Docs"
description: "자세한 내용은 어떻게 toouse Apache Maven Java 기반 toocreate MapReduce 응용 프로그램을 다음 실행 Hadoop으로 Azure HDInsight의 합니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>HDInsight의 Hadoop용 Java MapReduce 프로그램 개발

자세한 내용은 어떻게 toouse Apache Maven Java 기반 toocreate MapReduce 응용 프로그램을 다음 실행 Hadoop으로 Azure HDInsight의 합니다.

> [!NOTE]
> 이 예제는 HDInsight 3.6에서 가장 최근에 테스트되었습니다.

## <a name="prerequisites"></a>필수 조건

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 이상(또는 OpenJDK와 같은 이와 동등한 프로그램).
    
    > [!NOTE]
    > HDInsight 버전 3.4 이전은 Java 7을 사용합니다. HDInsight 3.5 이상은 Java 8을 사용합니다.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>개발 환경 구성

hello 다음과 같은 환경 변수 설정 되어 있습니다 Java 및 hello JDK 설치. 그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.

* `JAVA_HOME`-toohello hello Java runtime environment (JRE)가 설치 디렉터리를 가리켜야 합니다. 예를 들어, OS X, Unix 또는 Linux 시스템에서 그 값이 있어야 비슷한 너무`/usr/lib/jvm/java-7-oracle`합니다. Windows에서 동일 하 게과 유사한 값 너무`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-경로 따라 hello를 포함 해야 합니다.
  
  * `JAVA_HOME`(또는 hello 해당 하는 경로)

  * `JAVA_HOME\bin`(또는 hello 해당 하는 경로)

  * Maven 설치 되어 있는 hello 디렉터리

## <a name="create-a-maven-project"></a>Maven 프로젝트 만들기

1. 터미널 세션 또는 개발 환경에서 명령줄에서 toostore이이 프로젝트를 원하는 디렉터리 toohello 위치를 변경 합니다.

2. 사용 하 여 hello `mvn` Maven에서 hello 프로젝트에 대 한 스 캐 폴딩 toogenerate hello 함께 설치 된 명령입니다.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > PowerShell을 사용 하는 경우 hello 묶어야 `-D` 큰따옴표로 매개 변수입니다.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    이 명령은 hello 지정 된 이름의 hello 디렉터리를 만듭니다 `artifactID` 매개 변수 (**wordcountjava** 이 예에서.) 이 디렉터리는 다음 항목 hello를 포함 되어 있습니다.

   * `pom.xml`-hello [Project 개체 모델 (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) 정보를 포함 하 고 구성 정보 toobuild hello 프로젝트를 사용 합니다.

   * `src`-hello 응용 프로그램이 있는 hello 디렉터리입니다.

3. Hello 삭제 `src/test/java/org/apache/hadoop/examples/apptest.java` 파일입니다. 이 예제에서는 사용되지 않습니다.

## <a name="add-dependencies"></a>종속성 추가

1. Hello 편집 `pom.xml` 파일을 텍스트 hello 안에 다음 hello 추가 `<dependencies>` 섹션:
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    이 항목은 특정 버전(&lt;version\>에 나열됨)을 사용하는 필수 라이브러리(&lt;artifactId\> 내에 나열됨)를 정의합니다. 컴파일 타임에 이러한 종속성은 hello 기본 Maven 저장소에서 다운로드 됩니다. Hello를 사용할 수 있습니다 [Maven 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview 더 합니다.
   
    hello `<scope>provided</scope>` 지시 Maven 이러한 종속성 hello 응용 프로그램과 함께 패키징되 지 해야 런타임 시 hello HDInsight 클러스터에 의해 제공 되는 대로 합니다.

    > [!IMPORTANT]
    > 사용 되는 hello 버전 hadoop 클러스터에 있는 hello 버전을 일치 해야 합니다. 버전에 대 한 자세한 내용은 참조 hello [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서.

2. Hello toohello 다음 추가 `pom.xml` 파일입니다. 이 텍스트는 hello 내부에 있어야 합니다. `<project>...</project>` hello 파일에, 즉 예를 들어 태그 `</dependencies>` 및 `</project>`합니다.

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    hello 첫 번째 플러그 인 구성 hello [Maven 음영 플러그 인](http://maven.apache.org/plugins/maven-shade-plugin/), 어떤가 사용 되는 toobuild hello 응용 프로그램에 필요한 종속성을 포함 하는 uberjar (한 fatjar 라고도 함). 또한 일부 시스템에서 문제를 일으킬 수 있는 hello jar 패키지 내에서 라이선스의 중복을 방지 합니다.

    두 번째 플러그 인 hello hello 대상 Java 버전을 구성합니다.

    > [!NOTE]
    > HDInsight 3.4 이전은 Java 7 사용합니다. HDInsight 3.5 이상은 Java 8을 사용합니다.

3. Hello 저장 `pom.xml` 파일입니다.

## <a name="create-hello-mapreduce-application"></a>Hello MapReduce 응용 프로그램 만들기

1. Toohello 이동 `wordcountjava/src/main/java/org/apache/hadoop/examples` 디렉터리 및 이름 바꾸기 hello `App.java` 파일 너무`WordCount.java`합니다.

2. 열기 hello `WordCount.java` 텍스트 편집기에서 파일을 텍스트 다음 hello hello 내용을 바꿉니다.
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    공지 hello 패키지 이름이 `org.apache.hadoop.examples` hello 클래스 이름은 `WordCount`합니다. Hello MapReduce 작업을 제출 하는 경우에 이러한 이름을 사용 합니다.

3. Hello 파일을 저장 합니다.

## <a name="build-hello-application"></a>Hello 응용 프로그램 빌드

1. Toohello 변경 `wordcountjava` 디렉터리를 사용할 수 없는 경우 이미 있습니다.

2. 다음 명령을 toobuild JAR 파일 hello 응용 프로그램을 포함 하는 hello를 사용 합니다.

   ```
   mvn clean package
   ```

    이 명령은 모든 이전 빌드 아티팩트를 정리 하, 모든 설치 되지 않은 이미, 종속성 및 빌드합니다 hello 응용 프로그램 패키지를 다운로드 합니다.

3. Hello 명령이 완료 된 hello 되 면 `wordcountjava/target` 라는 파일을 포함 하는 디렉터리 `wordcountjava-1.0-SNAPSHOT.jar`합니다.
   
   > [!NOTE]
   > hello `wordcountjava-1.0-SNAPSHOT.jar` 파일 뿐만 아니라 hello WordCount 작업을 포함 하는 uberjar 했지만 런타임 시 종속성 hello 작업에 필요 합니다.

## <a id="upload"></a>Hello jar 업로드

다음 명령은 tooupload hello jar 파일 toohello HDInsight 헤드 노드에 hello를 사용 합니다.

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

이 명령은 hello 로컬 시스템 toohello 헤드 노드에서 hello 파일을 복사합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a name="run"></a>Hadoop에서 hello MapReduce 작업 실행

1. TooHDInsight SSH를 사용 하 여 연결 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. Hello SSH 세션에서 명령을 toorun hello MapReduce 응용 프로그램을 다음 hello를 사용 합니다.
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    이 명령은 hello WordCount MapReduce 응용 프로그램을 시작합니다. hello 입력된 파일은 `/example/data/gutenberg/davinci.txt`, hello 출력 디렉터리는 및 `/example/data/wordcountout`합니다. Hello 입력 파일과 출력은 hello 클러스터에 대 한 저장된 toohello 기본 저장소입니다.

3. Hello 작업이 완료 되 면 다음 명령 tooview hello 결과 hello를 사용 합니다.
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    값 비슷한 toohello 텍스트 다음으로 단어와 개수 목록을 받아야:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>다음 단계

이 문서에서는 배웠습니다 어떻게 toodevelop Java MapReduce 작업 합니다. Hello 다음 HDInsight와 다른 방법으로 toowork에 대 한 문서를 참조 하십시오.

* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [HDInsight와 함께 MapReduce 사용](hdinsight-use-mapreduce.md)

자세한 내용은 참고 항목 hello [Java 개발자 센터](https://azure.microsoft.com/develop/java/)합니다.

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

