---
title: "HDInsight의 Hive 및 Java UDF(사용자 정의 함수) - Azure | Microsoft Docs"
description: "Hive에서 작동하는 Java 기반 UDF(사용자 정의 함수)를 만드는 방법을 알아봅니다. 이 예제 UDF는 텍스트 문자열 테이블을 소문자로 변환합니다."
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="02257-104">HDInsight에서 Hive와 함께 Java UDF 사용</span><span class="sxs-lookup"><span data-stu-id="02257-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="02257-105">Hive에서 작동하는 Java 기반 UDF(사용자 정의 함수)를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="02257-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="02257-106">이 예제의 Java UDF는 텍스트 문자열 테이블을 모두 소문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="02257-107">요구 사항</span><span class="sxs-lookup"><span data-stu-id="02257-107">Requirements</span></span>

* <span data-ttu-id="02257-108">HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="02257-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="02257-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="02257-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="02257-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02257-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="02257-111">이 문서의 단계는 대부분 Windows 및 Linux 기반 클러스터 둘 다에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="02257-112">그러나 클러스터에 컴파일된 UDF를 업로드하고 실행하는 데 사용하는 단계는 Linux 기반 클러스터와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02257-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="02257-113">Windows 기반 클러스터와 함께 사용할 수 있는 정보에 대한 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="02257-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="02257-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 이상(또는 OpenJDK와 같은 이와 동등한 프로그램)</span><span class="sxs-lookup"><span data-stu-id="02257-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="02257-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="02257-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="02257-116">텍스트 편집기 또는 Java IDE</span><span class="sxs-lookup"><span data-stu-id="02257-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="02257-117">Windows 클라이언트에서 Python 파일을 만드는 경우 LF를 줄 끝으로 사용하는 편집기를 이용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="02257-118">편집기에서 LF 또는 CRLF를 사용하는지 여부가 확실하지 않은 경우 CR 문자를 제거하는 단계는 [문제 해결](#troubleshooting) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02257-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="02257-119">예제 Java UDF 만들기</span><span class="sxs-lookup"><span data-stu-id="02257-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="02257-120">명령줄에서 새 Maven을 만들려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02257-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="02257-121">PowerShell을 사용하는 경우 매개 변수를 묶는 따옴표를 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="02257-122">예: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`</span><span class="sxs-lookup"><span data-stu-id="02257-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="02257-123">이 명령은 Maven 프로젝트를 포함하는 **exampleudf**라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02257-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="02257-124">프로젝트를 만들면 프로젝트의 일부로 작성된 **exampleudf/src/test** 디렉터리를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="02257-125">**exampleudf/pom.xml**을 열고 기존 `<dependencies>` 항목을 다음 XML로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02257-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="02257-126">이러한 항목은 HDInsight 3.5와 함께 포함된 Hadoop 및 Hive의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="02257-127">[HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서에서 HDInsight를 제공하는 Hadoop 및 Hive의 버전에 대한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02257-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="02257-128">파일 끝의 `</project>` 줄 앞에 `<build>` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="02257-129">이 섹션에는 다음 XML이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="02257-130">이러한 항목은 프로젝트를 빌드하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-130">These entries define how to build the project.</span></span> <span data-ttu-id="02257-131">특히, 프로젝트에서 사용하는 Java 버전과 클러스터로의 배포를 위한 uberjar를 빌드하는 방법이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="02257-132">변경이 완료되면 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="02257-133">**exampleudf/src/main/java/com/microsoft/examples/App.java**라는 이름을 **ExampleUDF.java**로 바꾸고 편집기에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02257-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="02257-134">**ExampleUDF.java** 파일의 내용을 다음 코드로 바꾼 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="02257-135">이 코드는 문자열 값을 허용하고 문자열의 소문자 버전을 반환하는 UDF를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="02257-136">UDF 빌드 및 설치</span><span class="sxs-lookup"><span data-stu-id="02257-136">Build and install the UDF</span></span>

1. <span data-ttu-id="02257-137">다음 명령을 실행하여 UDF를 컴파일하고 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="02257-138">이 명령은 `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` 파일에 UDF를 빌드하고 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="02257-139">`scp` 명령을 사용하여 파일을 HDInsight 클러스터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="02257-140">`myuser`를 클러스터의 SSH 사용자 계정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02257-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="02257-141">`mycluster`를 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02257-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="02257-142">암호를 사용하여 SSH 계정을 보호할 경우 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="02257-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="02257-143">인증서를 사용하는 경우, `-i` 매개 변수를 사용하여 개인 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="02257-144">SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="02257-145">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02257-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="02257-146">SSH 세션에서 HDInsight 저장소에 jar 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="02257-147">Hive에서 UDF 사용</span><span class="sxs-lookup"><span data-stu-id="02257-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="02257-148">다음을 사용하여 SSH 세션에서 Beeline 클라이언트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="02257-149">이 명령에서는 클러스터에 대한 로그인 계정에 **admin** 의 기본값을 사용했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="02257-150">`jdbc:hive2://localhost:10001/>` 프롬프트가 표시되면 다음을 입력하여 Hive에 UDF를 추가하고 함수로 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="02257-151">이 예제에서는 Azure Storage가 클러스터에 대한 기본 저장소라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="02257-152">클러스터가 Data Lake Store를 대신 사용하는 경우 `wasb:///` 값을 `adl:///`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="02257-153">UDF를 사용하여 검색한 값을 테이블에서 소문자 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="02257-154">이 쿼리는 테이블에서 장치 플랫폼(Android, Windows, iOS 등)을 선택하고 문자열을 소문자로 변환한 다음 표시하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02257-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="02257-155">출력은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="02257-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="02257-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02257-156">Next steps</span></span>

<span data-ttu-id="02257-157">Hive로 작업하는 다른 방법은 [HDInsight와 함께 Hive 사용](hdinsight-use-hive.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02257-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="02257-158">Hive 사용자 정의 함수에 대한 자세한 내용은 apache.org의 Hive wiki에서 [Hive 연산자 및 사용자 정의 함수](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02257-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
