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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="c6db9-103">HDInsight의 Hadoop용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="c6db9-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="c6db9-104">자세한 내용은 어떻게 toouse Apache Maven Java 기반 toocreate MapReduce 응용 프로그램을 다음 실행 Hadoop으로 Azure HDInsight의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="c6db9-105">이 예제는 HDInsight 3.6에서 가장 최근에 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="c6db9-106"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="c6db9-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="c6db9-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 이상(또는 OpenJDK와 같은 이와 동등한 프로그램).</span><span class="sxs-lookup"><span data-stu-id="c6db9-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c6db9-108">HDInsight 버전 3.4 이전은 Java 7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="c6db9-109">HDInsight 3.5 이상은 Java 8을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="c6db9-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="c6db9-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="c6db9-111">개발 환경 구성</span><span class="sxs-lookup"><span data-stu-id="c6db9-111">Configure development environment</span></span>

<span data-ttu-id="c6db9-112">hello 다음과 같은 환경 변수 설정 되어 있습니다 Java 및 hello JDK 설치.</span><span class="sxs-lookup"><span data-stu-id="c6db9-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="c6db9-113">그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="c6db9-114">`JAVA_HOME`-toohello hello Java runtime environment (JRE)가 설치 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="c6db9-115">예를 들어, OS X, Unix 또는 Linux 시스템에서 그 값이 있어야 비슷한 너무`/usr/lib/jvm/java-7-oracle`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="c6db9-116">Windows에서 동일 하 게과 유사한 값 너무`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="c6db9-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="c6db9-117">`PATH`-경로 따라 hello를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="c6db9-118">`JAVA_HOME`(또는 hello 해당 하는 경로)</span><span class="sxs-lookup"><span data-stu-id="c6db9-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="c6db9-119">`JAVA_HOME\bin`(또는 hello 해당 하는 경로)</span><span class="sxs-lookup"><span data-stu-id="c6db9-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="c6db9-120">Maven 설치 되어 있는 hello 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c6db9-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="c6db9-121">Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c6db9-121">Create a Maven project</span></span>

1. <span data-ttu-id="c6db9-122">터미널 세션 또는 개발 환경에서 명령줄에서 toostore이이 프로젝트를 원하는 디렉터리 toohello 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="c6db9-123">사용 하 여 hello `mvn` Maven에서 hello 프로젝트에 대 한 스 캐 폴딩 toogenerate hello 함께 설치 된 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="c6db9-124">PowerShell을 사용 하는 경우 hello 묶어야 `-D` 큰따옴표로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="c6db9-125">이 명령은 hello 지정 된 이름의 hello 디렉터리를 만듭니다 `artifactID` 매개 변수 (**wordcountjava** 이 예에서.) 이 디렉터리는 다음 항목 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="c6db9-126">`pom.xml`-hello [Project 개체 모델 (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) 정보를 포함 하 고 구성 정보 toobuild hello 프로젝트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="c6db9-127">`src`-hello 응용 프로그램이 있는 hello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="c6db9-128">Hello 삭제 `src/test/java/org/apache/hadoop/examples/apptest.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="c6db9-129">이 예제에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="c6db9-130">종속성 추가</span><span class="sxs-lookup"><span data-stu-id="c6db9-130">Add dependencies</span></span>

1. <span data-ttu-id="c6db9-131">Hello 편집 `pom.xml` 파일을 텍스트 hello 안에 다음 hello 추가 `<dependencies>` 섹션:</span><span class="sxs-lookup"><span data-stu-id="c6db9-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="c6db9-132">이 항목은 특정 버전(&lt;version\>에 나열됨)을 사용하는 필수 라이브러리(&lt;artifactId\> 내에 나열됨)를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="c6db9-133">컴파일 타임에 이러한 종속성은 hello 기본 Maven 저장소에서 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="c6db9-134">Hello를 사용할 수 있습니다 [Maven 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="c6db9-135">hello `<scope>provided</scope>` 지시 Maven 이러한 종속성 hello 응용 프로그램과 함께 패키징되 지 해야 런타임 시 hello HDInsight 클러스터에 의해 제공 되는 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c6db9-136">사용 되는 hello 버전 hadoop 클러스터에 있는 hello 버전을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="c6db9-137">버전에 대 한 자세한 내용은 참조 hello [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c6db9-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="c6db9-138">Hello toohello 다음 추가 `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="c6db9-139">이 텍스트는 hello 내부에 있어야 합니다. `<project>...</project>` hello 파일에, 즉 예를 들어 태그 `</dependencies>` 및 `</project>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="c6db9-140">hello 첫 번째 플러그 인 구성 hello [Maven 음영 플러그 인](http://maven.apache.org/plugins/maven-shade-plugin/), 어떤가 사용 되는 toobuild hello 응용 프로그램에 필요한 종속성을 포함 하는 uberjar (한 fatjar 라고도 함).</span><span class="sxs-lookup"><span data-stu-id="c6db9-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="c6db9-141">또한 일부 시스템에서 문제를 일으킬 수 있는 hello jar 패키지 내에서 라이선스의 중복을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="c6db9-142">두 번째 플러그 인 hello hello 대상 Java 버전을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c6db9-143">HDInsight 3.4 이전은 Java 7 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="c6db9-144">HDInsight 3.5 이상은 Java 8을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="c6db9-145">Hello 저장 `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="c6db9-146">Hello MapReduce 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c6db9-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="c6db9-147">Toohello 이동 `wordcountjava/src/main/java/org/apache/hadoop/examples` 디렉터리 및 이름 바꾸기 hello `App.java` 파일 너무`WordCount.java`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="c6db9-148">열기 hello `WordCount.java` 텍스트 편집기에서 파일을 텍스트 다음 hello hello 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="c6db9-149">공지 hello 패키지 이름이 `org.apache.hadoop.examples` hello 클래스 이름은 `WordCount`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="c6db9-150">Hello MapReduce 작업을 제출 하는 경우에 이러한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="c6db9-151">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="c6db9-152">Hello 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="c6db9-152">Build hello application</span></span>

1. <span data-ttu-id="c6db9-153">Toohello 변경 `wordcountjava` 디렉터리를 사용할 수 없는 경우 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="c6db9-154">다음 명령을 toobuild JAR 파일 hello 응용 프로그램을 포함 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="c6db9-155">이 명령은 모든 이전 빌드 아티팩트를 정리 하, 모든 설치 되지 않은 이미, 종속성 및 빌드합니다 hello 응용 프로그램 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="c6db9-156">Hello 명령이 완료 된 hello 되 면 `wordcountjava/target` 라는 파일을 포함 하는 디렉터리 `wordcountjava-1.0-SNAPSHOT.jar`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c6db9-157">hello `wordcountjava-1.0-SNAPSHOT.jar` 파일 뿐만 아니라 hello WordCount 작업을 포함 하는 uberjar 했지만 런타임 시 종속성 hello 작업에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="c6db9-158"><a id="upload"></a>Hello jar 업로드</span><span class="sxs-lookup"><span data-stu-id="c6db9-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="c6db9-159">다음 명령은 tooupload hello jar 파일 toohello HDInsight 헤드 노드에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="c6db9-160">이 명령은 hello 로컬 시스템 toohello 헤드 노드에서 hello 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="c6db9-161">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6db9-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="c6db9-162"><a name="run"></a>Hadoop에서 hello MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c6db9-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="c6db9-163">TooHDInsight SSH를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="c6db9-164">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6db9-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c6db9-165">Hello SSH 세션에서 명령을 toorun hello MapReduce 응용 프로그램을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="c6db9-166">이 명령은 hello WordCount MapReduce 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="c6db9-167">hello 입력된 파일은 `/example/data/gutenberg/davinci.txt`, hello 출력 디렉터리는 및 `/example/data/wordcountout`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="c6db9-168">Hello 입력 파일과 출력은 hello 클러스터에 대 한 저장된 toohello 기본 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="c6db9-169">Hello 작업이 완료 되 면 다음 명령 tooview hello 결과 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="c6db9-170">값 비슷한 toohello 텍스트 다음으로 단어와 개수 목록을 받아야:</span><span class="sxs-lookup"><span data-stu-id="c6db9-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="c6db9-171"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6db9-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c6db9-172">이 문서에서는 배웠습니다 어떻게 toodevelop Java MapReduce 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="c6db9-173">Hello 다음 HDInsight와 다른 방법으로 toowork에 대 한 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c6db9-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="c6db9-174">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c6db9-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c6db9-175">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c6db9-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="c6db9-176">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="c6db9-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c6db9-177">자세한 내용은 참고 항목 hello [Java 개발자 센터](https://azure.microsoft.com/develop/java/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6db9-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

