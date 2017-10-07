---
title: "aaaUse MapReduce 및 Hadoop-Azure HDInsight를 사용 하 여 PowerShell | Microsoft Docs"
description: "어떻게 toouse PowerShell tooremotely MapReduce 작업으로 실행 Hadoop HDInsight에 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>PowerShell을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

이 문서 toorun Azure PowerShell을 사용 하는 예제에는 Hadoop MapReduce 작업 HDInsight 클러스터에 제공 합니다.

## <a id="prereq"></a>필수 조건

* **Azure HDInsight(HDInsight의 Hadoop) 클러스터**

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* **Azure PowerShell이 포함된 워크스테이션**.

## <a id="powershell"></a>Azure PowerShell을 사용하여 MapReduce 작업 실행

Azure PowerShell에는 *cmdlet* 수 있는 실행 tooremotely MapReduce 작업 HDInsight의 합니다. 너무 REST 호출을 사용 하 여이 작업을 수행 하는 내부적으로[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (이전의 Templeton) HDInsight 클러스터 hello에서 실행 합니다.

hello 다음 cmdlet은 사용 되는 원격 HDInsight 클러스터의 MapReduce 작업을 실행할 때.

* **로그인 AzureRmAccount**: Azure PowerShell 인증 tooyour Azure 구독.

* **새 AzureRmHDInsightMapReduceJobDefinition**: 새 *작업 정의* hello를 사용 하 여 MapReduce 정보를 지정 합니다.

* **시작 AzureRmHDInsightJob**: hello 작업 정의 tooHDInsight hello 작업을 시작 보내고 반환 된 *작업* hello 작업의 사용된 toocheck hello 상태가 될 수 있는 개체입니다.

* **대기 AzureRmHDInsightJob**: hello 작업의 hello 작업 개체 toocheck hello 상태를 사용 합니다. Hello 대기 시간을 초과 하거나 hello 작업이 완료 될 때까지 대기 합니다.

* **Get AzureRmHDInsightJobOutput**: hello 작업의 tooretrieve hello 출력을 사용 합니다.

hello 다음 단계 설명 방법을 toouse 이러한 cmdlet toorun HDInsight 클러스터에서 작업 합니다.

1. 코드를 다음 hello 저장의 편집기를 사용 하 여 **mapreducejob.ps1**합니다.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. 새 **Azure PowerShell** 명령 프롬프트를 엽니다. Hello의 디렉터리 toohello 위치를 변경 **mapreducejob.ps1** 파일을 다음 명령 toorun hello 스크립트 다음 hello를 사용 하 여:

        .\mapreducejob.ps1

    Hello 스크립트를 실행 하면 hello HDInsight 클러스터의 hello 이름 및 hello HTTPS/관리자 계정 이름 및 hello 클러스터에 대 한 암호를 묻는 메시지가 나타납니다. 입력 정보 요청된 tooauthenticate tooyour Azure 구독을 수도 있습니다.

3. Hello 작업이 완료 되 면 출력 유사한 toohello를 텍스트 다음 나타납니다.

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    이 출력 hello 작업 완료를 나타냅니다.

    > [!NOTE]
    > 경우 hello **ExitCode** 는 값을 0이 아닌 참조 [문제 해결](#troubleshooting)합니다.

    이 예제에는 또한 hello 다운로드 한 파일 tooan 저장 **output.txt 라는** hello 스크립트를 실행 하는 hello 디렉터리의 파일입니다.

### <a name="view-output"></a>출력 보기

열기 hello **output.txt 라는** 파일 텍스트 편집기 toosee hello에 특정 단어 및 hello 작업에 의해 생성 된 수를 계산 합니다.

> [!NOTE]
> MapReduce 작업의 hello 출력 파일은 변경할 수 있습니다. 따라서이 샘플을 다시 실행 하는 경우에 hello 출력 파일의 toochange hello 이름이 필요 합니다.

## <a id="troubleshooting"></a>문제 해결

정보가 없는 hello 작업이 완료 되었을 때 반환 되 면 처리 하는 동안 오류가 발생 한 수 있습니다. 이 작업에 대 한 오류 정보 tooview 추가 명령을 toohello의 끝 다음 hello hello **mapreducejob.ps1** 파일을 저장 하 고 다시 실행 합니다.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

이 cmdlet hello 작업을 실행할 때 tooSTDERR hello 서버에 기록 된 hello 정보를 반환 하 고 hello 작업은 실패 하는 이유 확인 도움이 될 수 있습니다.

## <a id="summary"></a>요약

볼 수 있듯이 Azure PowerShell을 쉽게 toorun MapReduce 작업에 제공 된 HDInsight 클러스터, 모니터 hello 작업 상태 및 검색 hello 출력 합니다.

## <a id="nextsteps"></a>다음 단계

HDInsight의 MapReduce 작업에 대한 일반적인 정보:

* [HDInsight Hadoop에서 MapReduce 사용](hdinsight-use-mapreduce.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
