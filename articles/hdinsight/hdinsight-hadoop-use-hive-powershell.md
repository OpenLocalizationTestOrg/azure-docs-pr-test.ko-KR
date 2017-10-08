---
title: "powershell에서 Azure HDInsight Hadoop 하이브 aaaUse | Microsoft Docs"
description: "HDInsight의 Hadoop에서 PowerShell toorun 하이브 쿼리를 사용 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>PowerShell을 사용하여 Hive 쿼리 실행
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

이 문서에서 HDInsight 클러스터에서 Hadoop hello Azure 리소스 그룹 모드 toorun 하이브 쿼리에에서 Azure PowerShell을 사용 하는 예제를 제공 합니다.

> [!NOTE]
> 이 문서는 hello 예제에서 사용 하는 hello HiveQL 문을 수행할 작업에 대 한 자세한 설명을 제공 하지 않습니다. 이 예제에 사용 되는 HiveQL hello에 대 한 자세한 내용은 참조 [HDInsight에서 Hadoop으로 사용 하 여 하이브](hdinsight-use-hive.md)합니다.

**필수 구성 요소**

* **Azure HDInsight 클러스터**: hello 클러스터는 Windows 여부는 중요 하지 않습니다 또는 Linux 기반 합니다.

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* **Azure PowerShell이 포함된 워크스테이션**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Azure PowerShell을 사용하여 Hive 쿼리 실행

Azure PowerShell에는 *cmdlet* HDInsight의 Hive 쿼리 실행 tooremotely 있습니다 수 있는 합니다. 내부적으로 hello cmdlet 확인 REST 호출 너무[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 클러스터에 있습니다.

hello 다음 cmdlet은 사용 되는 원격 HDInsight 클러스터에서 하이브 쿼리를 실행 하는 경우:

* **추가 AzureRmAccount**: Azure PowerShell 인증 tooyour Azure 구독
* **새 AzureRmHDInsightHiveJobDefinition**: 만듭니다는 *작업 정의* hello를 사용 하 여 HiveQL 문은 지정 된
* **시작 AzureRmHDInsightJob**: hello 작업 정의 tooHDInsight hello 작업을 시작 보내고 반환 된 *작업* hello 작업의 사용된 toocheck hello 상태가 될 수 있는 개체
* **대기 AzureRmHDInsightJob**: hello 작업의 hello 작업 개체 toocheck hello 상태를 사용 합니다. Hello 대기 시간을 초과 하거나 hello 작업이 완료 될 때까지 대기 합니다.
* **Get AzureRmHDInsightJobOutput**: hello 작업의 tooretrieve hello 출력 사용
* **호출 AzureRmHDInsightHiveJob**: toorun HiveQL 문을 사용 합니다. 이 cmdlet 블록 hello 쿼리 완료 된 후 hello 결과 반환 합니다.
* **사용 하 여 AzureRmHDInsightCluster**: 집합 hello hello에 대 한 현재 클러스터 toouse **Invoke AzureRmHDInsightHiveJob** 명령

hello 다음 단계 설명 방법을 toouse 이러한 cmdlet toorun HDInsight 클러스터에서 작업:

1. 코드를 다음 hello 저장의 편집기를 사용 하 여 **hivejob.ps1**합니다.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. 새 **Azure PowerShell** 명령 프롬프트를 엽니다. Hello의 디렉터리 toohello 위치를 변경 **hivejob.ps1** 파일을 다음 명령 toorun hello 스크립트 다음 hello를 사용 하 여:

        .\hivejob.ps1

    Hello 스크립트를 실행 하는 경우 메시지 표시 tooenter hello 클러스터 이름 및 hello HTTPS/관리자 계정 자격 증명 hello 클러스터에 대 한 됩니다. Tooyour Azure 구독에서에서 메시지 표시 toolog 수도 있습니다.

3. Hello 작업이 완료 되 면 정보 비슷한 toohello를 thext 다음 반환 합니다.

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. 앞에서 설명한 것 처럼 **Invoke-hive** 사용된 toorun 쿼리일 수 있으며 hello 응답을 기다립니다. 다음 스크립트 toosee Invoke-hive의 작동 원리 hello를 사용 합니다.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    hello 출력 텍스트 다음 hello와 같습니다.

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > HiveQL 쿼리가 길면에 대 한 hello Azure PowerShell을 사용할 수 있습니다 **Here-string** cmdlet 또는 HiveQL 스크립트 파일입니다. 조각과 방법을 따르는 hello toouse hello **Invoke-hive** cmdlet toorun HiveQL 스크립트 파일입니다. hello HiveQL 스크립트 파일이 있어야 업로드할 toowasb: / /입니다.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > **Here-Strings**에 대한 자세한 내용은 <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Windows PowerShell Here-Strings 사용</a>을 참조하세요.

## <a name="troubleshooting"></a>문제 해결

정보가 없는 hello 작업이 완료 되었을 때 반환 되 면 처리 하는 동안 오류가 발생 한 수 있습니다. 이 작업에 대 한 오류 정보 tooview 추가 toohello의 끝 다음 hello hello **hivejob.ps1** 파일을 저장 하 고 다시 실행 합니다.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

이 cmdlet는 hello 작업을 실행할 때 tooSTDERR hello 서버에 작성 된 hello 정보를 반환 합니다.

## <a name="summary"></a>요약

볼 수 있듯이 Azure PowerShell HDInsight 클러스터에서 하이브 쿼리에 쉽게 toorun에는, 모니터 hello 상태, 작업 및 hello 출력을 검색 합니다.

## <a name="next-steps"></a>다음 단계

HDInsight의 Hive에 대한 일반적인 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)
