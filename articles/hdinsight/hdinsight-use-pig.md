---
title: "HDInsight의 Hadoop Pig aaaUse | Microsoft Docs"
description: "자세한 내용은 HDInsight에서 Hadoop으로 toouse Pig 하는 방법입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>HDInsight에서 Hadoop과 Pig 사용

자세한 내용은 방법 toouse [Apache Pig](http://pig.apache.org/) HDInsight와 중...

Pig는 *Pig Latin*이라는 절차형 언어를 사용하여 Hadoop용 프로그램을 생성하기 위한 플랫폼입니다. Pig 되는 대체 tooJava 작성용 *MapReduce* 솔루션, 되며 Azure HDInsight에 포함 합니다. 다음 테이블 toodiscover hello 다양 한 방법으로 Pig HDInsight와 사용할 수 있도록 하는 hello를 사용 합니다.

| **이것을 사용** 하세요... | ... **대화형** 셸 | ...**배치** 처리 | ... **클러스터 운영 체제** | ... **클라이언트 운영 체제** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X, 또는 Windows |
| [REST API](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux 또는or Windows |Linux, Unix, Mac OS X, 또는 Windows |
| [Hadoop용 .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux 또는or Windows |Windows(당분간) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux 또는or Windows |Windows |
| [원격 데스크톱](hdinsight-hadoop-use-pig-remote-desktop.md)(HDInsight 3.2 및 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a id="why"></a>Pig를 사용하는 이유

Hadoop MapReduce을 사용 하 여 데이터 처리의 hello 과제 중 하나은 지도 및 reduce 함수를 사용 하 여 처리 논리를 구현 합니다. 있습니다 종종 복잡 한 처리에 대 한 함께 tooachieve hello 원하는 결과 여러 개의 MapReduce 작업으로 처리 toobreak 연결.

Pig 처리를 일련의 hello tooproduce hello 원하는 출력을 통해 데이터 흐름 변환 toodefine가 있습니다.

hello Pig 라틴 문자 언어 있습니다 toodescribe hello에서에서 데이터 흐름 tooproduce hello 원하는 출력 하나 이상의 변형을 통해 원시 입력을 허용합니다. Pig Latin 프로그램이 일반적인 패턴을 따릅니다:

* **부하**: hello 파일 시스템에서 조작 하는 데이터 toobe 읽기

* **변환**: hello 데이터 조작

* **덤프 또는 저장**: 데이터 toohello 화면 출력 또는 처리를 위해 저장

### <a name="user-defined-functions"></a>사용자 정의 함수

Pig 라틴 사용자 정의 함수 (UDF) 수 있는 지원 하기 어려운 toomodel Pig 라틴 문자에는 논리를 구현 하는 tooinvoke 외부 구성 요소입니다.

Pig Latin에 대한 자세한 내용은 [Pig Latin 참조 설명서 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) 및 [Pig Latin 참조 설명서 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html)를 참조하십시오.

Udf를 사용 하 여 Pig 사용의 예를 들어 hello 다음 문서를 참조 하십시오.

* [HDInsight에서 HDInsight와 함께 Pig 사용](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu는 Apache에서 유지 관리하는 유용한 UDF의 컬렉션입니다.
* [HDInsight에서 Pig 및 Hive와 함께 Python 사용](hdinsight-python.md)
* [HDInsight에서 Hive 및 Pig와 함께 C# 사용](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>예제 데이터

HDInsight hello에 저장 되는 다양 한 예제 데이터 집합을 제공 `/example/data` 및 `/HdiSamples` 디렉터리입니다. 클러스터에 대 한 hello 기본 저장소에이 디렉터리는. 이 문서에 hello Pig 예제 hello를 사용 하 여 *log4j* 에서 파일을 `/example/data/sample.log`합니다.

Hello 파일 내의 각 로그를 포함 하는 필드의 줄으로 구성 됩니다는 `[LOG LEVEL]` tooshow hello 유형 및 hello 심각도 예를 들어 필드:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

Hello 이전 예에서 hello 로그 수준에는 오류입니다.

> [!NOTE]
> Hello를 사용 하 여 log4j 파일을 생성할 수도 있습니다 [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) 도구 로깅 및 다음 해당 파일 tooyour blob을 업로드 합니다. 참조 [데이터 업로드 tooHDInsight](hdinsight-upload-data.md) 지침에 대 한 합니다. HDInsight와 함께 Azure Blob 저장소를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.

## <a id="job"></a>예제 작업

hello Pig 라틴 작업 로드 hello `sample.log` HDInsight 클러스터에 대 한 hello 기본 저장소 파일이 있습니다. 그런 다음 일련의 여러 번 각 로그 수준에서 오류가 발생 했습니다 hello 입력된 데이터는 방법의 수에 발생 하는 변환 수행 합니다. hello 결과가 tooSTDOUT 기록 됩니다.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

hello 다음 그림에서는 각 변환을 수행 toohello 데이터에 대 한 요약

![Hello 변환의 그래픽 표현][image-hdi-pig-data-transformation]

## <a id="run"></a>Hello Pig 라틴 작업 실행

HDInsight는 다양한 메서드를 사용하여 Pig Latin 작업을 실행할 수 있습니다. 어느 방법이 적합 한, 테이블 toodecide 다음 hello를 사용 하 여 다음 연습은 hello 링크를 따라 이동 합니다.

| **이것을 사용** 하세요... | ... **대화형** 셸 | ...**배치** 처리 | ... **클러스터 운영 체제** | ...**클라이언트** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X, 또는 Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux 또는or Windows |Linux, Unix, Mac OS X, 또는 Windows |
| [Hadoop용 .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux 또는or Windows |Windows(당분간) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux 또는or Windows |Windows |
| [원격 데스크톱](hdinsight-hadoop-use-pig-remote-desktop.md)(HDInsight 3.2 및 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="pig-and-sql-server-integration-services"></a>Pig 및 SQL Server Integration Services

SQL Server Integration Services (SSIS) toorun Pig 작업을 사용할 수 있습니다. SSIS 용 Azure 기능 팩 hello 다음과 같은 구성 요소가에 HDInsight Pig 작업을 사용 하는 hello를 제공 합니다.

* [Azure HDInsight Pig 작업][pigtask]

* [Azure 구독 연결 관리자][connectionmanager]

자세한 정보 hello Azure 기능 팩에 대 한 SSIS [여기][ssispack]합니다.

## <a id="nextsteps"></a>다음 단계
이제는 어떻게 toouse HDInsight 사용 하 여 hello 뒤와 Pig 링크 tooexplore Azure HDInsight와 다른 방법으로 toowork 방법을 배웠습니다.

* [데이터 tooHDInsight 업로드][hdinsight-upload-data]
* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Sqoop 사용](hdinsight-use-sqoop.md)
* [HDInsight에서 Oozie 사용](hdinsight-use-oozie.md)
* [HDInsight에서 MapReduce 작업 사용][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
