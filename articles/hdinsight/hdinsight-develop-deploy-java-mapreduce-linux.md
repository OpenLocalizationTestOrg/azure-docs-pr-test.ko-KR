---
title: "Hadoop용 Java MapReduce 만들기 - Azure HDInsight | Microsoft Docs"
description: "Apache Maven을 사용하여 Java 기반 MapReduce 응용 프로그램을 만든 다음 Azure HDInsight의 Hadoop과 함께 실행하는 방법을 알아봅니다."
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
ms.openlocfilehash: 11d63f22204eb2acb530378f53ac72f16a35a4f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="1770b-103">HDInsight의 Hadoop용 Java MapReduce 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="1770b-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="1770b-104">Apache Maven을 사용하여 Java 기반 MapReduce 응용 프로그램을 만든 다음 Azure HDInsight의 Hadoop과 함께 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="1770b-105">이 예제는 HDInsight 3.6에서 가장 최근에 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="1770b-106"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="1770b-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="1770b-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 이상(또는 OpenJDK와 같은 이와 동등한 프로그램).</span><span class="sxs-lookup"><span data-stu-id="1770b-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1770b-108">HDInsight 버전 3.4 이전은 Java 7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="1770b-109">HDInsight 3.5 이상은 Java 8을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="1770b-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="1770b-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="1770b-111">개발 환경 구성</span><span class="sxs-lookup"><span data-stu-id="1770b-111">Configure development environment</span></span>

<span data-ttu-id="1770b-112">Java 및 JDK를 설치할 때 다음 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-112">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="1770b-113">하지만 변수가 존재하며 시스템에 대한 올바른 값을 포함하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-113">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="1770b-114">`JAVA_HOME` - JRE(Java runtime environment)가 설치된 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-114">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="1770b-115">예를 들어 OS X, Unix 또는 Linux 시스템에서는 `/usr/lib/jvm/java-7-oracle`과 유사한 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-115">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="1770b-116">Windows에서는 `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="1770b-116">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="1770b-117">`PATH` - 다음 경로를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-117">`PATH` - should contain the following paths:</span></span>
  
  * <span data-ttu-id="1770b-118">`JAVA_HOME`(또는 그와 동등한 경로)</span><span class="sxs-lookup"><span data-stu-id="1770b-118">`JAVA_HOME` (or the equivalent path)</span></span>

  * <span data-ttu-id="1770b-119">`JAVA_HOME\bin`(또는 그와 동등한 경로)</span><span class="sxs-lookup"><span data-stu-id="1770b-119">`JAVA_HOME\bin` (or the equivalent path)</span></span>

  * <span data-ttu-id="1770b-120">Maven이 설치된 디렉터리</span><span class="sxs-lookup"><span data-stu-id="1770b-120">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="1770b-121">Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1770b-121">Create a Maven project</span></span>

1. <span data-ttu-id="1770b-122">터미널 세션 또는 개발 환경의 명령줄에서 이 프로젝트를 저장할 위치로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-122">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span></span>

2. <span data-ttu-id="1770b-123">Maven과 함께 설치되는 `mvn` 명령을 사용하여 프로젝트에 대한 스캐폴딩을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-123">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="1770b-124">PowerShell을 사용하는 경우 큰 따옴표로 `-D` 매개 변수를 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-124">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="1770b-125">이 명령은 `artifactID` 매개 변수(이 예제에서는 **wordcountjava**)로 지정된 이름으로 디렉터리를 만듭니다. 이 디렉터리에는 다음과 같은 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-125">This command creates a directory with the name specified by the `artifactID` parameter (**wordcountjava** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="1770b-126">`pom.xml` - [프로젝트 개체 모델(POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)은 프로젝트를 빌드하는 데 사용된 정보 및 구성 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span></span>

   * <span data-ttu-id="1770b-127">`src` - 응용 프로그램을 포함하는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-127">`src` - The directory that contains the application.</span></span>

3. <span data-ttu-id="1770b-128">`src/test/java/org/apache/hadoop/examples/apptest.java` 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="1770b-129">이 예제에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="1770b-130">종속성 추가</span><span class="sxs-lookup"><span data-stu-id="1770b-130">Add dependencies</span></span>

1. <span data-ttu-id="1770b-131">`pom.xml` 파일을 편집하고 `<dependencies>` 섹션 내에 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-131">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="1770b-132">이 항목은 특정 버전(&lt;version\>에 나열됨)을 사용하는 필수 라이브러리(&lt;artifactId\> 내에 나열됨)를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="1770b-133">컴파일 시 이러한 종속성이 기본 Maven 리포지토리에서 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-133">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="1770b-134">[Maven 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) 을 사용하여 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-134">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span></span>
   
    <span data-ttu-id="1770b-135">`<scope>provided</scope>`는 이러한 종속성은 런타임에 HDInsight 클러스터에서 제공되므로 응용 프로그램과 함께 패키징해서는 안 된다는 점을 Maven에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-135">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1770b-136">사용되는 버전은 클러스터에 있는 Hadoop 버전과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-136">The version used should match the version of Hadoop present on your cluster.</span></span> <span data-ttu-id="1770b-137">버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1770b-137">For more information on versions, see the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="1770b-138">`pom.xml` 파일에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-138">Add the following to the `pom.xml` file.</span></span> <span data-ttu-id="1770b-139">이 텍스트는 파일의 `<project>...</project>` 태그 내에 있어야 합니다. 예를 들어 `</dependencies>`와 `</project>` 사이에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-139">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="1770b-140">첫 번째 플러그 인은 응용 프로그램에 필요한 종속성을 포함하는 uberjar(fatjar이라고도 함)을 빌드하는 데 사용되는 [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-140">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span></span> <span data-ttu-id="1770b-141">또한 일부 시스템에서 문제를 일으킬 수 있는 jar 패키지 내 라이선스 중복을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-141">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="1770b-142">두 번째 플러그 인은 대상 Java 버전을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-142">The second plugin configures the target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1770b-143">HDInsight 3.4 이전은 Java 7 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="1770b-144">HDInsight 3.5 이상은 Java 8을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="1770b-145">`pom.xml` 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-145">Save the `pom.xml` file.</span></span>

## <a name="create-the-mapreduce-application"></a><span data-ttu-id="1770b-146">MapReduce 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1770b-146">Create the MapReduce application</span></span>

1. <span data-ttu-id="1770b-147">`wordcountjava/src/main/java/org/apache/hadoop/examples` 디렉터리로 이동하여 `App.java` 파일의 이름을 `WordCount.java`으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-147">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span></span>

2. <span data-ttu-id="1770b-148">텍스트 편집기에서 `WordCount.java` 파일을 열고 내용을 다음 텍스트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-148">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span></span>
   
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
   
    <span data-ttu-id="1770b-149">패키지 이름은 `org.apache.hadoop.examples`이며 클래스 이름은 `WordCount`입니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-149">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span></span> <span data-ttu-id="1770b-150">MapReduce 작업을 제출할 때 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-150">You use these names when you submit the MapReduce job.</span></span>

3. <span data-ttu-id="1770b-151">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-151">Save the file.</span></span>

## <a name="build-the-application"></a><span data-ttu-id="1770b-152">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="1770b-152">Build the application</span></span>

1. <span data-ttu-id="1770b-153">아직 이동하지 않은 경우 `wordcountjava` 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-153">Change to the `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="1770b-154">다음 명령을 사용하여 응용 프로그램을 포함하는 JAR 파일을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-154">Use the following command to build a JAR file containing the application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="1770b-155">이 명령은 이전 빌드 아티팩트를 정리하고, 아직 설치되지 않은 모든 종속성을 다운로드한 후 응용 프로그램을 빌드 및 패키지화합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span></span>

3. <span data-ttu-id="1770b-156">명령이 마무리되면 `wordcountjava/target` 디렉터리는 `wordcountjava-1.0-SNAPSHOT.jar` 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-156">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1770b-157">`wordcountjava-1.0-SNAPSHOT.jar` 파일은 는 WordCount 작업뿐만 아니라 런타임 시 작업에서 필요로 하는 종속성을 포함하는 uberjar입니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-157">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span></span>

## <span data-ttu-id="1770b-158"><a id="upload"></a>jar 업로드</span><span class="sxs-lookup"><span data-stu-id="1770b-158"><a id="upload"></a>Upload the jar</span></span>

<span data-ttu-id="1770b-159">다음 명령을 사용하여 HDInsight 헤드 노드에 jar 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-159">Use the following command to upload the jar file to the HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

<span data-ttu-id="1770b-160">이 명령은 로컬 시스템에서 헤드 노드로 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-160">This command copies the files from the local system to the head node.</span></span> <span data-ttu-id="1770b-161">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1770b-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="1770b-162"><a name="run"></a>Hadoop에서 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="1770b-162"><a name="run"></a>Run the MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="1770b-163">SSH를 사용하여 HDInsight에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-163">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="1770b-164">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1770b-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1770b-165">SSH 세션에서 다음 명령을 사용하여 MapReduce 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-165">From the SSH session, use the following command to run the MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="1770b-166">이 명령은 WordCount MapReduce 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-166">This command starts the WordCount MapReduce application.</span></span> <span data-ttu-id="1770b-167">입력된 파일은 `/example/data/gutenberg/davinci.txt`이며 출력 디렉터리는 `/example/data/wordcountout`입니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-167">The input file is `/example/data/gutenberg/davinci.txt`, and the output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="1770b-168">입력 파일과 출력 모두 클러스터의 기본 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-168">Both the input file and output are stored to the default storage for the cluster.</span></span>

3. <span data-ttu-id="1770b-169">작업이 완료되면 다음 명령을 사용하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-169">Once the job completes, use the following command to view the results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="1770b-170">다음 텍스트와 유사한 값을 가진 단어 및 개수 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-170">You should receive a list of words and counts, with values similar to the following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="1770b-171"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="1770b-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1770b-172">이 문서에서는 Java MapReduce 작업을 개발하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1770b-172">In this document, you have learned how to develop a Java MapReduce job.</span></span> <span data-ttu-id="1770b-173">HDInsight로 작업하는 다른 방법은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1770b-173">See the following documents for other ways to work with HDInsight.</span></span>

* <span data-ttu-id="1770b-174">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1770b-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1770b-175">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1770b-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="1770b-176">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="1770b-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1770b-177">자세한 내용은 [Java 개발자 센터](https://azure.microsoft.com/develop/java/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1770b-177">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

