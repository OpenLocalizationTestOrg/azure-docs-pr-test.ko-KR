---
title: "HDInsight에서 Hadoop으로 aaaMapReduce | Microsoft Docs"
description: "HDInsight 클러스터의 MapReduce toorun Hadoop에서 작업 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>HDInsight에서 Hadoop과 MapReduce 사용

HDInsight 클러스터에서 toorun MapReduce 작업 하는 방법에 대해 알아봅니다. 다음 테이블 toodiscover hello MapReduce HDInsight와 사용할 수 있도록 하는 다양 한 방법으로 hello를 사용 합니다.

| **사용 기능**... | **...toodo가** | ... **클러스터 운영 체제** | ... **클라이언트 운영 체제** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |통해 hello Hadoop 명령을 사용 하 여 **SSH** |Linux |Linux, Unix, Mac OS X, 또는 Windows |
| [REST (영문)](hdinsight-hadoop-use-mapreduce-curl.md) |사용 하 여 hello 작업을 원격으로 제출 **REST** (예제 cURL를 사용 하는 데 사용) |Linux 또는or Windows |Linux, Unix, Mac OS X, 또는 Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |사용 하 여 hello 작업을 원격으로 제출 **Windows PowerShell** |Linux 또는or Windows |Windows |
| [원격 데스크톱](hdinsight-hadoop-use-mapreduce-remote-desktop.md)(HDInsight 3.2 및 3.3) |통해 hello Hadoop 명령을 사용 하 여 **원격 데스크톱** |Windows |Windows |

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a id="whatis"></a>MapReduce란

Hadoop MapReduce는 방대한 양의 데이터를 처리하는 작업을 작성하기 위한 소프트웨어 프레임워크입니다. 입력된 데이터는 다음 클러스터의 hello 노드에서 동시에 처리 되는 독립 청크로 분할 됩니다. MapReduce 작업은 두 함수로 구성됩니다.

* **매퍼**: 입력된 데이터를 소비하고 분석하며(일반적으로 필터 및 정렬 작업) 튜플을 내보냅니다.(키-값 쌍)

* **리 듀 서**: hello 맵 편집기에서 내보낸 된 튜플을 소비 하 고 더 작은, 결합 된 결과 hello 매퍼 데이터 로부터 만드는 요약 연산을 수행

기본적인 word count MapReduce 작업 예제는 hello 다음 다이어그램에서에서 보여 줍니다.

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

이 작업의 hello 출력은 각 단어 hello 텍스트 분석 된에서 발생 했습니다. 몇 번의 개수입니다.

* hello 매퍼 각 줄을 입력으로 hello 입력된 텍스트에서 걸리며 단어로 나눕니다. 내보낸 키/값 쌍 단어 나올 때마다 hello 단어의 뒤에 1입니다. hello 출력이 tooreducer 보내기 전에 정렬 됩니다.
* hello 리 듀 서 각 단어에 대 한 이러한 개별 수의 합계를 계산 하 고 hello 단어 하나 다음에 발생 빈도의 hello 합계를 포함 하는 단일 키/값 쌍을 내보냅니다.

MapReduce는 다양한 언어로 구현할 수 있습니다. Java는 hello 가장 일반적인 구현 하며이 문서의 설명을 위해 사용 됩니다.

## <a name="development-languages"></a>개발 언어

언어 또는 hello Java 가상 컴퓨터 및 Java를 기반으로 하는 프레임 워크는 MapReduce 작업으로 직접 실행 수 있습니다. 이 문서에 사용 되는 hello 예제는 MapReduce Java 응용 프로그램. C#, Python, 독립 실행형 실행 파일 등의 비-Java 언어는 Hadoop 스트리밍을 사용해야 합니다.

Hadoop 스트리밍 STDIN 및 STDOUT hello 매퍼 및 리 듀 서와 통신합니다. hello 매퍼 및 리 듀 서 데이터 줄에서 STDIN 한 번에 읽고 hello 출력 tooSTDOUT 작성 합니다. 각 줄 읽기 또는 hello 매퍼 및 리 듀 서에서 내보낸 탭 문자로 구분 된 키/값 쌍의 hello 형식 이어야 합니다.

    [key]/t[value]

자세한 내용은 [Hadoop 스트리밍](http://hadoop.apache.org/docs/r1.2.1/streaming.html)을 참조하세요.

Hadoop 스트리밍 HDInsight를 사용 하 여의 예 hello 다음 문서를 참조 합니다.

* [C# MapReduce 작업 개발](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Python MapReduce 작업 개발](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>예제 데이터

HDInsight hello에 저장 되는 다양 한 예제 데이터 집합을 제공 `/example/data` 및 `/HdiSamples` 디렉터리입니다. 클러스터에 대 한 hello 기본 저장소에이 디렉터리는. 이 문서를 사용 하 여 hello `/example/data/gutenberg/davinci.txt` 파일입니다. 이 파일의 레오나르도 다빈치 hello 전자 필기장 포함 되어 있습니다.

## <a id="job"></a>예제 MapReduce

MapReduce 단어 수 세기 응용 프로그램 예가 HDInsight 클러스터에 포함되어 있습니다. 이 예제에는 `/example/jars/hadoop-mapreduce-examples.jar` hello 기본 저장소 클러스터에 대해에서 합니다.

다음 Java 코드는 hello은 hello hello에 포함 된 MapReduce 응용 프로그램의 hello 소스 `hadoop-mapreduce-examples.jar` 파일:

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

지침 toowrite MapReduce 응용 프로그램 hello 다음 문서 참조:

* [HDInsight용 Java MapReduce 프로그램 개발](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [HDInsight용 Python MapReduce 프로그램 개발](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>MapReduce hello를 실행 합니다.

HDInsight는 다양한 메서드를 사용하여 HiveQL 작업을 실행할 수 있습니다. 어느 방법이 적합 한, 테이블 toodecide 다음 hello를 사용 하 여 다음 연습은 hello 링크를 따라 이동 합니다.

| **사용 기능**... | **...toodo가** | ... **클러스터 운영 체제** | ... **클라이언트 운영 체제** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |통해 hello Hadoop 명령을 사용 하 여 **SSH** |Linux |Linux, Unix, Mac OS X, 또는 Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |사용 하 여 hello 작업을 원격으로 제출 **REST** |Linux 또는or Windows |Linux, Unix, Mac OS X, 또는 Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |사용 하 여 hello 작업을 원격으로 제출 **Windows PowerShell** |Linux 또는or Windows |Windows |
| [원격 데스크톱](hdinsight-hadoop-use-mapreduce-remote-desktop.md)(HDInsight 3.2 및 3.3) |통해 hello Hadoop 명령을 사용 하 여 **원격 데스크톱** |Windows |Windows |

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a id="nextsteps"></a>다음 단계

HDInsight에서 데이터 작업에 대해 자세히 toolearn hello 다음 문서를 참조 하십시오.

* [HDInsight용 Java MapReduce 프로그램 개발](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [HDInsight용 Python 스트리밍 MapReduce 프로그램 개발](hdinsight-hadoop-streaming-python.md)

* [HDInsight에서 Apache Hadoop을 사용하여 Scalding MapReduce 작업 개발](hdinsight-hadoop-mapreduce-scalding.md)

* [HDInsight에서 Hive 사용][hdinsight-use-hive]

* [HDInsight에서 Pig 사용][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
