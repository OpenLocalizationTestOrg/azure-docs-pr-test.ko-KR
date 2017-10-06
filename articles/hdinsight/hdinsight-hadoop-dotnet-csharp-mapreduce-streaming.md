---
title: "C#에서 Azure HDInsight에서 Hadoop MapReduce로 aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 Azure HDInsight에서 Hadoop으로 toouse C# toocreate MapReduce 솔루션입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>HDInsight의 Hadoop에서 MapReduce와 함께 C# 사용

자세한 내용은 방법 toouse C# toocreate HDInsight에서 MapReduce 솔루션입니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.

Hadoop 스트리밍는 스크립트 또는 실행 파일을 사용 하 여 toorun MapReduce 작업을 허용 하는 유틸리티입니다. 이 예제에서는.NET은 사용 되는 tooimplement hello 매퍼 및 리 듀 서 단어 개수 솔루션에 대 한 합니다.

## <a name="net-on-hdinsight"></a>HDInsight에서.NET

__Linux 기반 HDInsight__ 사용 하 여 클러스터 [모노 (https://mono-project.com)](https://mono-project.com) toorun.NET 응용 프로그램입니다. Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다. HDInsight에 포함 된 모노 길이의 hello에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다. toouse 모노의 특정 버전 참조 hello [설치 또는 업데이트 모노](hdinsight-hadoop-install-mono.md) 문서.

.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.

## <a name="how-hadoop-streaming-works"></a>Hadoop 스트리밍 작동 방식

이 문서에 스트리밍에 사용 되는 hello 기본 프로세스는 다음과 같습니다.

1. Hadoop에서 STDIN 데이터 toohello 매퍼 (이 예제의 mapper.exe)를 전달합니다.
2. hello 매퍼 hello 데이터를 처리 하 고 탭으로 구분 된 키/값 쌍 tooSTDOUT를 내보냅니다.
3. hello 출력 hadoop를 읽고 STDIN의 toohello 리 듀 서 (이 예제의 reducer.exe)를 전달 합니다.
4. hello 리 듀 서 hello 탭으로 구분 된 키/값 쌍을 읽습니다 하 고 hello 데이터를 처리 하 고 STDOUT에 탭으로 구분 된 키/값 쌍으로 hello 결과 내보냅니다.
5. hello 출력 hadoop 읽고 toohello 출력 디렉터리를 씁니다.

스트리밍에 대한 자세한 내용은 [Hadoop 스트리밍(https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)을 참조하세요.

## <a name="prerequisites"></a>필수 조건

* .NET Framework 4.5를 대상으로 하는 C# 코드 작성 및 빌드에 대해 잘 알고 있어야 합니다. 이 문서 사용 하 여 Visual Studio 2017의에서 hello 단계.

* 방식으로 tooupload.exe 파일을 toohello 클러스터 합니다. hello 단계가이 문서에 사용 하 여 hello 데이터 레이크 도구 hello 클러스터에 대 한 Visual Studio tooupload hello 파일 tooprimary 저장소에 대 한 합니다.

* Azure PowerShell 또는 SSH 클라이언트

* HDInsight 클러스터의 Hadoop. 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-provision-clusters.md)를 참조하세요.

## <a name="create-hello-mapper"></a>Hello 매퍼 만들기

Visual Studio에서 __mapper__라는 새 __콘솔 응용 프로그램__을 만듭니다. Hello 응용 프로그램에 대 한 코드 다음 hello를 사용 합니다.

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Hello 응용 프로그램을 만든 후 빌드합니다 tooproduce hello `/bin/Debug/mapper.exe` hello 프로젝트 디렉터리의 파일입니다.

## <a name="create-hello-reducer"></a>Hello 리 듀 서 만들기

Visual Studio에서 __reducer__라는 새 __콘솔 응용 프로그램__을 만듭니다. Hello 응용 프로그램에 대 한 코드 다음 hello를 사용 합니다.

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Hello 응용 프로그램을 만든 후 빌드합니다 tooproduce hello `/bin/Debug/reducer.exe` hello 프로젝트 디렉터리의 파일입니다.

## <a name="upload-toostorage"></a>Toostorage 업로드

1. Visual Studio에서 **서버 탐색기**를 엽니다.

2. **Azure**를 확장한 다음 **HDInsight**를 확장합니다.

3. 메시지가 표시되면 Azure 구독 자격 증명을 입력한 다음 **로그인**을 클릭합니다.

4. Hello HDInsight 클러스터를 toodeploy이 응용이 프로그램을 확장 합니다. Hello 텍스트 있는 항목이 __(기본 저장소 계정)__ 나열 됩니다.

    ![Hello 클러스터에 대 한 hello 저장소 계정을 보여 주는 서버 탐색기](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * 사용 중인 경우이 항목에서 확장할 수는 __Azure 저장소 계정__ hello 클러스터에 대 한 기본 저장소로 합니다. hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello 항목을 확장 하 고 hello 두 번 클릭 __(기본 컨테이너)__합니다.

    * 사용 하는이 항목을 확장할 수 없으면, __Azure 데이터 레이크 저장소__ hello 클러스터에 대 한 기본 저장소 hello로 합니다. hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello를 두 번 클릭 __(기본 저장소 계정)__ 항목입니다.

5. tooupload hello.exe 파일을 사용 하 여 hello 메서드를 다음 중 하나:

    * 사용 하는 경우는 __Azure 저장소 계정__hello 업로드 아이콘을 클릭 한 다음 toohello 찾아보기, **bin\debug** hello에 대 한 폴더 **매퍼** 프로젝트. 마지막으로 hello 선택 **mapper.exe** 파일을 클릭 하 여 **확인**합니다.

        ![업로드 아이콘](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * 사용 하는 경우 __Azure 데이터 레이크 저장소__를 hello 파일 목록에서 빈 영역을 마우스 오른쪽 단추로 클릭 한 다음 선택 __업로드__합니다. 마지막으로 hello 선택 **mapper.exe** 파일을 클릭 하 여 **열려**합니다.

    한 번 hello __mapper.exe__ 업로드가 완료 되 면 hello에 대 한 반복 hello 업로드 프로세스 __reducer.exe__ 파일입니다.

## <a name="run-a-job-using-an-ssh-session"></a>작업 실행: SSH 세션 사용

1. SSH tooconnect toohello HDInsight 클러스터를 사용 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. Hello 명령 toostart hello MapReduce 작업을 다음 중 하나를 사용 합니다.

    * 기본 저장소로 __Data Lake Store__를 사용하는 경우

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * 기본 저장소로 __Azure Storage__를 사용하는 경우

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    hello 목록 다음 각 매개 변수에 용도 설명 합니다.

    * `hadoop-streaming.jar`: hello 스트리밍 MapReduce 기능을 포함 하는 hello jar 파일입니다.
    * `-files`: Hello 추가 `mapper.exe` 및 `reducer.exe` 파일 toothis 작업 합니다. hello `adl:///` 또는 `wasb:///` 각 파일은 hello 클러스터에 대 한 기본 저장소의 hello 경로 toohello 루트 전에 합니다.
    * `-mapper`: Hello 맵 편집기를 구현 하는 파일을 지정 합니다.
    * `-reducer`: Hello 리 듀 서를 구현 하는 파일을 지정 합니다.
    * `-input`: hello 입력 데이터를 필터링 합니다.
    * `-output`: hello 출력 디렉터리입니다.

3. Hello MapReduce 작업 완료 되 면 다음 tooview hello 결과 hello를 사용 합니다.

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    hello 다음 텍스트는이 명령에서 반환 된 hello 데이터의 예입니다.

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>작업 실행: PowerShell 사용

PowerShell 스크립트 toorun MapReduce 작업을 수행 하는 hello를 사용 하 고 hello 결과 다운로드 합니다.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

이 스크립트를 hello 클러스터 로그인 계정 이름 및 hello HDInsight 클러스터 이름 함께 암호를 묻습니다. Hello 출력은 다운로드 한 toohello hello 작업이 완료 되 면 `output.txt` hello 디렉터리 hello 스크립트에는 파일에서 실행 됩니다. hello 다음 텍스트는 hello에 hello 데이터의 예로 `output.txt` 파일:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>다음 단계

HDInsight에서 MapReduce 사용에 대한 자세한 내용은 [HDInsight에서 MapReduce 사용](hdinsight-use-mapreduce.md)을 참조하세요.

Hive 및 Pig에서 C#을 사용하는 방법에 대한 자세한 내용은 [Hive 및 Pig에서 C# 사용자 정의 기능 사용](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)을 참조하세요.

HDInsight의 Storm에서 C# 사용에 대한 자세한 내용은 [HDInsight에서 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.