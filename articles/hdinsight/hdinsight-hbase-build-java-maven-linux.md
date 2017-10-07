---
title: "aaaJava HBase 클라이언트-Azure HDInsight | Microsoft Docs"
description: "자세한 내용은 방법 toouse Apache Maven Java 기반 toobuild Apache HBase 응용 프로그램에 배포 tooHBase Azure HDInsight의 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a>Apache HBase에 대한 Java 응용 프로그램 빌드

자세한 내용은 방법 toocreate는 [Apache HBase](http://hbase.apache.org/) java에서 응용 프로그램입니다. 다음 hello 응용 프로그램을 사용 하 여 Azure HDInsight에서 HBase를 사용 합니다.

이 문서 사용의 단계를 hello [Maven](http://maven.apache.org/) toocreate 및 빌드 hello 프로젝트. Maven는 소프트웨어 프로젝트 관리 및 이해 도구 toobuild 소프트웨어, 설명서 및 Java 프로젝트에 대 한 보고서입니다.

> [!NOTE]
> hello이 문서의 단계에서는 가장 최근에 테스트 HDInsight 3.6 사용 합니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="requirements"></a>요구 사항

* [Java 플랫폼 JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 이상.

    > [!NOTE]
    > HDInsight 3.5 이상에는 Java 8이 필요합니다. 이전 버전의 HDInsight를 사용하려면 Java 7이 필요합니다.

* [Maven](http://maven.apache.org/)

* [Linux 기반 Azure HDInsight 클러스터 및 HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > 이 문서의 단계 hello HDInsight 클러스터 버전 3.4 및 3.5와 테스트 되었습니다. 예제에 제공 된 hello 기본값 3.5 HDInsight 클러스터에 대 한 됩니다.

## <a name="create-hello-project"></a>Hello 프로젝트 만들기

1. Hello 명령줄에서 개발 환경에서 디렉터리 toohello 저장할 위치 toocreate hello 프로젝트 예를 들어 변경 `cd code\hbase`합니다.

2. 사용 하 여 hello **mvn** Maven에서 hello 프로젝트에 대 한 스 캐 폴딩 toogenerate hello 함께 설치 된 명령입니다.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > PowerShell을 사용 하는 경우 hello 묶어야 `-D` 큰따옴표로 매개 변수입니다.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    이 명령은 이름이 hello hello로 디렉터리를 만듭니다 **의 artifactID** 매개 변수 (**hbaseapp** 이 예에서.) 이 디렉터리는 다음 항목 hello를 포함 되어 있습니다.

   * **pom.xml**: hello Project 개체 모델 ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) 정보 및 구성 사용 세부 정보 toobuild hello 프로젝트를 포함 합니다.
   * **src**: hello를 포함 하는 hello 디렉터리 **main/java/com/microsoft/예제** hello 응용 프로그램을 작성할 수 있는 디렉터리입니다.

3. Hello 삭제 `src/test/java/com/microsoft/examples/apptest.java` 파일입니다. 이 예제에서는 사용되지 않았습니다.

## <a name="update-hello-project-object-model"></a>업데이트 hello Project 개체 모델

1. Hello 편집 `pom.xml` 파일을 hello hello 내부에서 코드를 다음 추가 `<dependencies>` 섹션:

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    이 섹션 나타냅니다 해당 hello 프로젝트 **hbase 클라이언트** 및 **피닉스 코어** 구성 요소입니다. 컴파일 타임에 이러한 종속성은 hello 기본 Maven 저장소에서 다운로드 됩니다. Hello를 사용할 수 있습니다 [Maven 중앙 리포지토리 검색](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn이이 종속성에 대 한 자세한 합니다.

   > [!IMPORTANT]
   > hello hbase 클라이언트의 버전 번호 hello hello 버전의 HDInsight 클러스터와 함께 제공 되는 HBase 일치 해야 합니다. 다음 테이블 toofind hello 올바른 버전 번호는 hello를 사용 합니다.

   | HDInsight 클러스터 버전 | HBase 버전 toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 및 3.6 |1.1.2 |

    HDInsight 버전 및 구성 요소에 대 한 자세한 내용은 참조 하십시오. [hello 다른 Hadoop 구성 요소 HDInsight를 사용할 수 있는](hdinsight-component-versioning.md)합니다.

3. 다음 코드 toohello hello 추가 **pom.xml** 파일입니다. 이 텍스트는 hello 내부에 있어야 합니다. `<project>...</project>` 사이 hello에 태그 파일 예를 들어, `</dependencies>` 및 `</project>`합니다.

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
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
        </plugins>
    </build>
   ```

    이 섹션은 HBase에 대한 구성 정보를 포함하는 리소스(`conf/hbase-site.xml`)를 구성합니다.

   > [!NOTE]
   > 또한 코드를 통해 구성 값을 설정할 수도 있습니다. Hello에 hello 메모를 참조 하십시오. `CreateTable` 예제입니다.

    이 섹션에는 또한 hello 구성 [Maven 컴파일러 플러그 인](http://maven.apache.org/plugins/maven-compiler-plugin/) 및 [Maven 음영 플러그 인](http://maven.apache.org/plugins/maven-shade-plugin/)합니다. hello 컴파일러 플러그 인에 사용 되는 toocompile hello 토폴로지 됩니다. 플러그 인 hello 음영 Maven에 의해 빌드되는 hello JAR 패키지에서 사용 되는 tooprevent 라이선스 중복입니다. 이 플러그 인 hello HDInsight 클러스터에서 실행 시 사용 되는 tooprevent "라이선스 파일 중복" 오류입니다. Maven-음영-플러그 인을 사용 하 여 hello로 `ApacheLicenseResourceTransformer` 구현 hello 오류를 방지 합니다.

    hello maven 음영 플러그인도 hello 응용 프로그램에 필요한 모든 hello 종속성을 포함 하는 uber jar를 생성 합니다.

4. Hello 저장 `pom.xml` 파일입니다.

5. 라는 디렉터리를 만들고 `conf` hello에 `hbaseapp` 디렉터리입니다. 이 디렉터리는 tooHBase 연결 하는 데 사용 되는 toohold 구성 정보입니다.

6. 사용 하 여 hello 다음 명령은 hello HBase 클러스터 toohello에서 toocopy hello HBase 구성을 `conf` 디렉터리입니다. 대체 `USERNAME` SSH 로그인의 hello 이름으로 합니다. `CLUSTERNAME`을 HDInsight 클러스터 이름으로 바꿉니다.

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   `ssh` 및 `scp` 사용에 관한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기

1. Toohello 이동 `hbaseapp/src/main/java/com/microsoft/examples` 디렉터리 및 이름 바꾸기 hello app.java 파일 너무`CreateTable.java`합니다.

2. 열기 hello `CreateTable.java` 파일 및 텍스트 다음 hello hello 기존 내용을 바꿉니다.

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    이 코드는 hello **CreateTable** 라는 테이블을 만듭니다는 클래스 **사람** 미리 정의 된 사용자로 구성 된 채웁니다.

3. Hello 저장 `CreateTable.java` 파일입니다.

4. Hello에 `hbaseapp/src/main/java/com/microsoft/examples` 디렉터리 라는 파일을 만들어 `SearchByEmail.java`합니다. 이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    hello **SearchByEmail** 클래스에는 전자 메일 주소로 행에 대 한 사용된 tooquery 될 수 있습니다. 정규식 필터를 사용 하기 때문에 hello 클래스를 사용 하는 경우 문자열이 나 정규식을 제공할 수 있습니다.

5. Hello 저장 `SearchByEmail.java` 파일입니다.

6. Hello에 `hbaseapp/src/main/hava/com/microsoft/examples` 디렉터리 라는 파일을 만들어 `DeleteTable.java`합니다. 이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    이 클래스 정리 hello HBase 테이블을 사용 하지 않도록 설정 하 여이 예제에서 만든 하 고 hello에서 만든 hello 테이블 삭제 `CreateTable` 클래스입니다.

7. Hello 저장 `DeleteTable.java` 파일입니다.

## <a name="build-and-package-hello-application"></a>Hello 응용 프로그램을 빌드 및 패키지

1. Hello에서 `hbaseapp` 디렉터리를 사용 하 여 hello 다음 명령은 toobuild hello 응용 프로그램을 포함 하는 JAR 파일:

    ```bash
    mvn clean package
    ```

    이 명령은 빌드하고 패키지 hello.jar 파일에 응용 프로그램.

2. Hello 명령이 완료 되 면 hello `hbaseapp/target` 라는 파일을 포함 하는 디렉터리 `hbaseapp-1.0-SNAPSHOT.jar`합니다.

   > [!NOTE]
   > hello `hbaseapp-1.0-SNAPSHOT.jar` uber jar 파일이 있습니다. 모든 hello 종속성 필요한 toorun hello 응용 프로그램을 포함합니다.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Hello JAR를 업로드 하 고 (SSH) 작업 실행

다음 단계 사용 하 여 hello `scp` toocopy hello JAR toohello 기본의 헤드 노드 HDInsight 클러스터에서 HBase 프로그램. hello `ssh` tooconnect toohello 클러스터를 사용 하 고 hello 예제 hello 헤드 노드에서 직접 실행 명령입니다.

1. tooupload hello jar toohello 클러스터에서 다음 명령을 사용 하 여 hello:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    대체 `USERNAME` SSH 로그인의 hello 이름으로 합니다. `CLUSTERNAME`을 HDInsight 클러스터 이름으로 바꿉니다.

2. tooconnect toohello HBase 클러스터 hello 다음 명령을 사용 합니다.

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    대체 `USERNAME` hello 이름 SSH 로그인입니다. `CLUSTERNAME`을 HDInsight 클러스터 이름으로 바꿉니다.

3. 사용 하 여 HBase 테이블 toocreate hello Java 응용 프로그램, 다음 명령을 사용 하 여 hello:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    이 명령은 **people**이라는 HBase 테이블을 만들고 데이터로 채웁니다.

4. 다음 명령을 사용 하 여 hello hello 테이블에 저장 하는 전자 메일 주소에 대 한 toosearch:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    결과 다음 hello를 나타납니다.

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. 다음 명령을 사용 하 여 hello toodelete hello 표:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Hello JAR를 업로드 하 고 작업 (PowerShell)을 실행

단계를 수행 하는 hello HBase 클러스터에 대 한 Azure PowerShell tooupload hello JAR toohello 기본 저장소를 사용 합니다. HDInsight cmdlet은 사용 되는 toorun 예제를 원격으로 hello 다음입니다.

1. Azure PowerShell을 설치 및 구성한 후 `hbase-runner.psm1`이라는 파일을 만듭니다. 이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    이 파일에는 다음 두 모듈이 포함됩니다.

   * **추가 HDInsightFile** -사용 tooupload 파일 toohello 클러스터
   * **시작 HBaseExample** -사용 되는 이전에 만든 toorun hello 클래스

2. Hello 저장 `hbase-runner.psm1` 파일입니다.

3. 새 Azure PowerShell 창을 열고, 디렉터리 toohello 변경 `hbaseapp` 디렉터리 누른 실행된 hello 다음 명령:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Hello의 hello 경로 toohello 위치 변경 `hbase-runner.psm1` 앞에서 만든 파일입니다. 이 명령은 Azure PowerShell을 사용한 hello 모듈을 등록합니다.

4. 사용 하 여 hello 다음 명령은 tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour 클러스터입니다.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    대체 `hdinsightclustername` 클러스터의 hello 이름을 사용 합니다. hello 명령 업로드 hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` hello 클러스터에 대 한 기본 저장소에 위치 합니다.

5. 사용 하 여 테이블 toocreate hello `hbaseapp`, hello 다음 명령을 사용 하 여:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    대체 `hdinsightclustername` 클러스터의 hello 이름을 사용 합니다.

    이 명령은 HDInsight 클러스터에 HBase의 **people**이라는 테이블을 만듭니다. 이 명령은 hello 콘솔 창에서 어떠한 출력도 표시 되지 않습니다.

6. 다음 명령을 사용 하 여 hello hello 테이블의 엔터티에 대 한 toosearch:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    대체 `hdinsightclustername` 클러스터의 hello 이름을 사용 합니다.

    이 명령은 hello를 사용 하 여 `SearchByEmail` 여기서 hello toosearch 모든 행에 대 한 클래스 `contactinformation` 열 제품군 및 hello `email` hello 문자열을 포함 하는 열, `contoso.com`합니다. 결과 다음 hello을 받게 됩니다.

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    사용 하 여 **fabrikam.com** hello에 대 한 `-emailRegex` 값이 있는 hello 사용자가 반환 **fabrikam.com** hello 전자 메일 필드에 있습니다. Hello 검색 용어로 정규식을 사용할 수도 있습니다. 예를 들어 **^ r** 반환 전자 메일 hello 문자 'r'로 시작 하는 주소입니다.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Start-HBaseExample을 사용할 경우 결과가 없거나 예기치 않은 결과가 표시됨

사용 하 여 hello `-showErr` 매개 변수 tooview hello 표준 오류 (STDERR) 실행 중인 hello 작업 하는 동안 생성 되는 합니다.

## <a name="delete-hello-table"></a>Hello 테이블 삭제

Hello 예제를 완료 하는 경우 다음 toodelete hello hello를 사용 하 여 **사람** 이 예에서 사용 된 테이블:

__`ssh` 세션에서__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Azure PowerShell에서__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>다음 단계

[자세한 내용은 방법 toouse 스 쿼 럴 SQL HBase로](hdinsight-hbase-phoenix-squirrel-linux.md)
