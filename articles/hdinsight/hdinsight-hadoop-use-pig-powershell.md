---
title: "powershell에서 Azure HDInsight Hadoop Pig aaaUse | Microsoft Docs"
description: "Azure PowerShell을 사용 하 여 HDInsight의 toosubmit Pig 작업 tooa Hadoop 클러스터 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>HDInsight와 Azure PowerShell toorun Pig 작업을 사용 하 여

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

이 문서는 HDInsight 클러스터에서 Azure PowerShell toosubmit Pig 작업 tooa Hadoop을 사용 하는 예제를 제공 합니다. Pig은 데이터 변환, 모델링 언어 (Pig 라틴 문자)를 사용 하 여 toowrite MapReduce 작업을 허용 하지 않고 매핑한 함수를 줄입니다.

> [!NOTE]
> 이 문서는 hello 예제에서 사용 되는 hello Pig 라틴 문을 수행할 작업에 대 한 자세한 설명을 제공 하지 않습니다. 이 예에서 사용 된 Pig 라틴 hello에 대 한 정보를 참조 하십시오. [HDInsight에서 Hadoop으로 Pig](hdinsight-use-pig.md)합니다.

## <a id="prereq"></a>필수 조건

* **Azure HDInsight 클러스터**

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* **Azure PowerShell이 포함된 워크스테이션**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>PowerShell을 사용하여 Pig 작업 실행

Azure PowerShell에는 *cmdlet* 수 있는 실행 tooremotely Pig 작업 HDInsight의 합니다. 내부적으로 PowerShell 사용 하 여 REST 호출 너무[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 클러스터에서 실행 합니다.

hello 다음 cmdlet은 사용 되는 원격 HDInsight 클러스터에서 Pig 작업을 실행할 때:

* **로그인 AzureRmAccount**: Azure PowerShell 인증 tooyour Azure 구독
* **새 AzureRmHDInsightPigJobDefinition**: 만듭니다는 *작업 정의* hello를 사용 하 여 Pig 라틴 문 지정
* **시작 AzureRmHDInsightJob**: hello 작업 정의 tooHDInsight hello 작업을 시작 보내고 반환 된 *작업* hello 작업의 사용된 toocheck hello 상태가 될 수 있는 개체
* **대기 AzureRmHDInsightJob**: hello 작업의 hello 작업 개체 toocheck hello 상태를 사용 합니다. Hello 작업이 완료 되었는지 또는 hello 대기 시간을 초과 했습니다 때까지 기다렸다가 합니다.
* **Get AzureRmHDInsightJobOutput**: hello 작업의 tooretrieve hello 출력 사용

hello 다음 단계 설명 방법을 toouse 이러한 cmdlet toorun HDInsight 클러스터에서 작업 합니다.

1. 코드를 다음 hello 저장의 편집기를 사용 하 여 **pigjob.ps1**합니다.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. 새 Windows PowerShell 명령 프롬프트를 엽니다. Hello의 디렉터리 toohello 위치를 변경 **pigjob.ps1** 파일을 다음 명령 toorun hello 스크립트 다음 hello를 사용 하 여:

        .\pigjob.ps1

    Tooyour Azure 구독에서에서 메시지 표시 toolog 됩니다. 그런 다음 hello HTTPs/관리자 계정 이름 및 hello HDInsight 클러스터에 대 한 암호를 묻습니다.

2. Hello 작업이 완료 되 면 면 정보 비슷한 toohello 텍스트 다음 반환 해야 합니다.

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>문제 해결

정보가 없는 hello 작업이 완료 되었을 때 반환 되 면 처리 하는 동안 오류가 발생 한 수 있습니다. 이 작업에 대 한 오류 정보 tooview 추가 명령을 toohello의 끝 다음 hello hello **pigjob.ps1** 파일을 저장 하 고 다시 실행 합니다.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Hello 작업을 실행할 때 tooSTDERR hello 서버에 기록 된 hello 정보를 반환 합니다 되며 hello 작업은 실패 하는 이유 확인 도움이 될 수 있습니다.

## <a id="summary"></a>요약
볼 수 있듯이 Azure PowerShell을 쉽게 toorun Pig 작업에 제공 된 HDInsight 클러스터, 모니터 hello 작업 상태 및 검색 hello 출력 합니다.

## <a id="nextsteps"></a>다음 단계
HDInsight의 Pig에 대한 일반적인 정보:

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)
