---
title: "Hive 및 Pig에서 Azure HDInsight에서 Hadoop aaaUse C# | Microsoft Docs"
description: "자세한 방법을 toouse C# 사용자 정의 함수 (UDF) Hive 및 Pig Azure HDInsight 스트리밍."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>HDInsight에서 Hive 및 Pig 스트림과 함께 C# UDF(사용자 정의 함수) 사용

Toouse C# 사용자 HDInsight의 Apache Hive 및 Pig 함수 (UDF)을 정의 하는 방법에 대해 알아봅니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Windows 기반와 Linux 기반 HDInsight 클러스터와 함께 작동합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.

둘 다 Hive 및 Pig 처리를 위해 데이터 tooexternal 응용 프로그램에 전달할 수 있습니다. 이 프로세스를 _스트리밍_이라고 합니다. .NET 응용 프로그램을 사용 하 여 hello 데이터가 전달 됩니다 toohello 응용 프로그램에서 STDIN을 하 고 hello 응용 프로그램 STDOUT에 hello 결과 반환 합니다. tooread STDIN 및 STDOUT에서 쓰기를 사용 하면 `Console.ReadLine()` 및 `Console.WriteLine()` 콘솔 응용 프로그램에서입니다.

## <a name="prerequisites"></a>필수 조건

* .NET Framework 4.5를 대상으로 하는 C# 코드 작성 및 빌드에 대해 잘 알고 있어야 합니다.

    * 원하는 IDE를 사용합니다. [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 또는 [Visual Studio Code](https://code.visualstudio.com/)를 권장합니다. 이 문서 사용 하 여 Visual Studio 2017의에서 hello 단계.

* 방식으로 tooupload.exe 파일을 toohello 클러스터와 Pig 및 Hive 작업을 실행된 합니다. Visual Studio, Azure PowerShell 및 Azure CLI hello 데이터 레이크 도구 좋습니다. hello이 문서의 단계 Visual Studio tooupload hello 파일에 대 한 hello 데이터 레이크 도구를 사용 하 고 hello 예제 하이브 쿼리를 실행 합니다.

    다른 방법으로 toorun 하이브 쿼리 및 Pig 작업에 대 한 내용은 hello 다음 문서를 참조 하세요.

    * [HDInsight에서 Apache Hive 사용](hdinsight-use-hive.md)

    * [HDInsight에서 Apache Pig 사용](hdinsight-use-pig.md)

* HDInsight 클러스터의 Hadoop. 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-provision-clusters.md)를 참조하세요.

## <a name="net-on-hdinsight"></a>HDInsight에서.NET

* __Linux 기반 HDInsight__ 사용 하는 클러스터 [모노 (https://mono-project.com)](https://mono-project.com) toorun.NET 응용 프로그램입니다. Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.

    .NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.

    toouse 모노의 특정 버전 참조 hello [설치 또는 업데이트 모노](hdinsight-hadoop-install-mono.md) 문서.

* __Windows 기반 HDInsight__ 클러스터 hello Microsoft.NET CLR toorun.NET 응용 프로그램을 사용 합니다.

Hello.NET framework 및 HDInsight 버전에 포함 된 모노의 hello 버전에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다.

## <a name="create-hello-c-projects"></a>Hello C 만들기\# 프로젝트

### <a name="hive-udf"></a>Hive UDF

1. Visual Studio를 열고 솔루션을 만듭니다. Hello 프로젝트 형식에 대 한 선택 **콘솔 응용 프로그램 (.NET Framework)**, 및 이름 hello에 대 한 새 프로젝트 **HiveCSharp**합니다.

    > [!IMPORTANT]
    > Linux 기반 HDInsight 클러스터를 사용하는 경우 __.NET Framework 4.5__를 선택합니다. .NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.

2. Hello 내용 바꾸기 **Program.cs** hello 다음과 같이 합니다.

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Hello 프로젝트를 빌드하십시오.

### <a name="pig-udf"></a>Pig UDF

1. Visual Studio를 열고 솔루션을 만듭니다. Hello 프로젝트 형식에 대 한 선택 **콘솔 응용 프로그램**, 및 이름 hello에 대 한 새 프로젝트 **PigUDF**합니다.

2. Hello hello 내용 바꾸기 **Program.cs** 코드 다음 hello로 파일:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Hello Pig에서 보낸 선과 다시 포맷으로 시작 하는 구문 분석 하는이 응용 프로그램 `java.lang.Exception`합니다.

3. 저장 **Program.cs**, 다음 hello 프로젝트를 빌드합니다.

## <a name="upload-toostorage"></a>Toostorage 업로드

1. Visual Studio에서 **서버 탐색기**를 엽니다.

2. **Azure**를 확장한 다음 **HDInsight**를 확장합니다.

3. 메시지가 표시되면 Azure 구독 자격 증명을 입력한 다음 **로그인**을 클릭합니다.

4. Hello HDInsight 클러스터를 toodeploy이 응용이 프로그램을 확장 합니다. Hello 텍스트 있는 항목이 __(기본 저장소 계정)__ 나열 됩니다.

    ![Hello 클러스터에 대 한 hello 저장소 계정을 보여 주는 서버 탐색기](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * 사용 중인 경우이 항목에서 확장할 수는 __Azure 저장소 계정__ hello 클러스터에 대 한 기본 저장소로 합니다. hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello 항목을 확장 하 고 hello 두 번 클릭 __(기본 컨테이너)__합니다.

    * 사용 하는이 항목을 확장할 수 없으면, __Azure 데이터 레이크 저장소__ hello 클러스터에 대 한 기본 저장소 hello로 합니다. hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello를 두 번 클릭 __(기본 저장소 계정)__ 항목입니다.

6. tooupload hello.exe 파일을 사용 하 여 hello 메서드를 다음 중 하나:

    * 사용 하는 경우는 __Azure 저장소 계정__hello 업로드 아이콘을 클릭 한 다음 toohello 찾아보기, **bin\debug** hello에 대 한 폴더 **HiveCSharp** 프로젝트. 마지막으로 hello 선택 **HiveCSharp.exe** 파일을 클릭 하 여 **확인**합니다.

        ![업로드 아이콘](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * 사용 하는 경우 __Azure 데이터 레이크 저장소__를 hello 파일 목록에서 빈 영역을 마우스 오른쪽 단추로 클릭 한 다음 선택 __업로드__합니다. 마지막으로 hello 선택 **HiveCSharp.exe** 파일을 클릭 하 여 **열려**합니다.

    한 번 hello __HiveCSharp.exe__ 업로드가 완료 되 면 hello에 대 한 반복 hello 업로드 프로세스 __PigUDF.exe__ 파일입니다.

## <a name="run-a-hive-query"></a>HIVE 쿼리 실행

1. Visual Studio에서 **서버 탐색기**를 엽니다.

2. **Azure**를 확장한 다음 **HDInsight**를 확장합니다.

3. Hello를 배포 하는 마우스 오른쪽 단추로 클릭 hello 클러스터 **HiveCSharp** , 응용 프로그램을 다음 선택 **는 하이브 쿼리를 작성할**합니다.

4. Hello 하이브 쿼리에 대 한 텍스트 뒤 hello를 사용 합니다.

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Hello를 주석 처리 제거 `add file` hello 유형의 클러스터에 대해 사용 되는 기본 저장소와 일치 하는 문입니다.

    이 쿼리는 hello 선택 `clientid`, `devicemake`, 및 `devicemodel` 에서 필드 `hivesampletable`, hello 필드 toohello HiveCSharp.exe 응용 프로그램을 전달 합니다. hello 쿼리 hello 응용 프로그램 tooreturn 세 개의 필드가으로 저장 되는 예상 `clientid`, `phoneLabel`, 및 `phoneHash`합니다. hello 쿼리는 또한 toofind HiveCSharp.exe hello 기본 저장소 컨테이너의 hello 루트에서 필요합니다.

5. 클릭 **전송** toosubmit hello 작업 toohello HDInsight 클러스터입니다. hello **작업 요약 하이브** 창이 열립니다.

6. 클릭 **새로 고침** 까지 요약 toorefresh hello **작업 상태** 쪽 변경**Completed**합니다. 클릭 tooview hello 작업 출력 **작업 출력**합니다.

## <a name="run-a-pig-job"></a>Pig 작업 실행

1. Hello 메서드 tooconnect tooyour HDInsight 클러스터를 다음 중 하나를 사용 합니다.

    * __Linux 기반__ HDInsight 클러스터를 사용하는 경우 SSH를 사용합니다. 예: `ssh sshuser@mycluster-ssh.azurehdinsight.net`. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.
    
    * 사용 하는 경우는 __Windows 기반__ HDInsight 클러스터 [원격 데스크톱을 사용 하 여 연결 toohello 클러스터](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. 다음 명령은 toostart hello Pig 명령 줄 하나 hello를 사용 합니다.

        pig

    > [!IMPORTANT]
    > Windows 기반 클러스터를 사용 하는 경우 명령 대신 다음 hello를 사용 합니다.
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    `grunt>` 프롬프트가 표시됩니다.

3. Hello toorun hello.NET Framework 응용 프로그램을 사용 하는 Pig 작업을 다음을 입력 합니다.

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    hello `DEFINE` 문을의 별칭을 만들어 `streamer` hello pigudf.exe 응용 프로그램 및 `CACHE` hello 클러스터에 대 한 기본 저장소에서 로드 합니다. 이상에서는 `streamer` hello와 함께 사용 되 `STREAM` 연산자 tooprocess hello 일련의 열으로 로그와 반환 hello 데이터에 포함 된 단일 행.

    > [!NOTE]
    > 스트리밍에 사용 되는 hello 응용 프로그램 이름 hello로 묶어야 \` (억음 악센트 기호) 때 문자 별칭이 지정 하 고 ' (작은따옴표)와 함께 사용할 경우 `SHIP`합니다.

4. Hello 마지막 줄을 입력 한 후 hello 작업을 시작 해야 합니다. 출력 유사한 toohello를 다음 텍스트를 반환 합니다.

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>다음 단계

이 문서에서는 배웠습니다 어떻게 toouse Hive 및 Pig HDInsight의에서.NET Framework 응용 프로그램입니다. Hive 및 Pig, Python toouse 참조 toolearn 원하는 경우 [Hive 및 Pig HDInsight에서 Python 사용](hdinsight-python.md)합니다.

다른 방법으로 toouse Pig 및 Hive, 및 MapReduce 사용에 대 한 toolearn hello 다음 문서를 참조 하세요.

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight와 함께 MapReduce 사용](hdinsight-use-mapreduce.md)
