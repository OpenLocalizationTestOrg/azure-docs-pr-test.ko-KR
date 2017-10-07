---
title: "Hadoop에서 Giraph Azure HDInsight 클러스터를 aaaInstall 및 사용 | Microsoft Docs"
description: "고 toocustomize HDInsight 클러스터 Giraph,으로 하는 방법에 대해 알아봅니다 toouse Giraph 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Windows 기반 HDInsight 클러스터에서 Giraph 설치 및 사용

고 toocustomize Windows와 Giraph 스크립트 동작을 사용 하 여 HDInsight 클러스터를 기반으로 하는 방법에 대해 알아봅니다 toouse Giraph tooprocess 대규모 그래프입니다. Linux 기반 클러스터와 함께 Giraph를 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Giraph 설치(Linux)](hdinsight-hadoop-giraph-install-linux.md)를 참조하세요.

> [!IMPORTANT]
> 이 문서 에서만 작동 하는 Windows 기반 HDInsight 클러스터의에서 hello 단계. HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. 방법에 대 한 Linux 기반 HDInsight 클러스터에서 Giraph tooinstall 참조 [HDInsight Hadoop 클러스터 (Linux)에서 설치 Giraph](hdinsight-hadoop-giraph-install-linux.md)합니다.


*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 Giraph를 설치할 수 있습니다. HDInsight 클러스터에서 샘플 스크립트 tooinstall Giraph에서 읽기 전용 Azure 저장소 blob에서 사용할 수는 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)합니다. hello 샘플 스크립트는 HDInsight 클러스터 버전 3.1과만 작동합니다. HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.

**관련된 문서**

* [HDInsight Hadoop 클러스터에 Giraph 설치(Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.
* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)

## <a name="what-is-giraph"></a>Giraph 정의
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> tooperform 그래프 Hadoop을 사용 하 여 처리를 허용 하 고 Azure HDInsight 함께 사용할 수 있습니다. 인터넷, hello와 같은 대규모 네트워크에 있는 라우터 간 hello 연결 등의 개체 간의 관계를 모델링 하는 그래프 또는 소셜 네트워크 (경우에 따라 참조 tooas 소셜 그래프)에 사용자 간의 관계입니다. Graph 처리 하면 그래프를 개체 간의 관계 hello에 대 한 tooreason 같은:

* 현재 관계를 기반으로 하여 잠재적인 친구 파악.
* 네트워크에 두 컴퓨터 간에 hello 최단 경로 식별 합니다.
* 웹 페이지의 hello 페이지 순위를 계산 합니다.

## <a name="install-giraph-using-portal"></a>포털을 사용하여 Giraph 설치
1. Hello를 사용 하 여 클러스터를 만들기 시작 **사용자 지정 만들기** 옵션에 설명 된 대로 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-provision-clusters.md)합니다.
2. Hello에 **스크립트 동작** 페이지 hello 마법사의 클릭 **스크립트 동작 추가** 아래와 같이 tooprovide hello 스크립트 동작에 대 한 세부 정보:

    ![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")

    <table border='1'>
        <tr><th>속성</th><th>값</th></tr>
        <tr><td>이름</td>
            <td>Hello 스크립트 동작에 대 한 이름을 지정 합니다. 예: <b>Install Giraph</b></td></tr>
        <tr><td>스크립트 URI</td>
            <td>호출 된 toocustomize hello 클러스터는 hello 식별자 URI (Uniform Resource) toohello 스크립트를 지정 합니다. 예: <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>노드 유형</td>
            <td>Hello 사용자 지정 스크립트가 실행 되는 hello 노드를 지정 합니다. <b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.
        <tr><td>매개 변수</td>
            <td>Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다. hello 스크립트 tooinstall Giraph 모든 매개 변수를 필요 하지 않으므로이 비워 둘 수 있습니다.</td></tr>
    </table>

    Hello 클러스터에서 둘 이상의 스크립트 동작 tooinstall 여러 구성 요소를 추가할 수 있습니다. Hello 스크립트를 추가한 후 hello 확인 표시 toostart hello 클러스터 만들기를 클릭 합니다.

## <a name="use-giraph"></a>Giraph 사용
사용 하 여 hello SimpleShortestPathsComputation 예제 toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> hello 그래프에 있는 개체 사이의 최단 경로 찾기 위한 구현 합니다. 다음 단계 tooupload hello 샘플 데이터와 hello 샘플 jar, hello SimpleShortestPathsComputation 예제 및 hello 결과 보기를 사용 하 여 작업을 실행 하는 hello를 사용 합니다.

1. 예제 데이터 파일 tooAzure Blob 저장소에 업로드 합니다. 로컬 워크스테이션에서 **tiny_graph.txt**라는 새 파일을 만듭니다. 위의 삼각형 hello가 있어야 합니다.

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Hello tiny_graph.txt 파일 toohello 기본 저장소에 HDInsight 클러스터를 업로드 합니다. 방법에 대 한 지침은 tooupload 데이터 참조 [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드](hdinsight-upload-data.md)합니다.

    Hello 형식을 사용 하 여는 방향된 그래프에 있는 개체 사이의 관계를 설명 하는이 데이터 [소스\_id, 소스\_값 [[dest\_id]를 [가장자리\_값],...]]. 각 줄은 **source\_id** 개체와 하나 이상의 **dest\_id** 개체 간 관계를 나타냅니다. hello **가장자리\_값** (또는 가중치) hello 수준 또는 거리 간의 hello 연결의으로 생각할 수 **source_id** 및 **dest\_id**.

    으로 그린 hello 값 (또는 가중치)를 사용 하 여 개체 간의 hello 거리로, 데이터 위에 hello 다음과 같은 형식 및:

    ![원과 거리가 다른 선으로 그린 tiny_graph.txt](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Hello SimpleShortestPathsComputation 예제를 실행 합니다. 입력으로 hello tiny_graph.txt 파일을 사용 하 여 다음 Azure PowerShell cmdlet toorun hello 예제 hello를 사용 합니다.

    > [!IMPORTANT]
    > Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다. Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.
    >
    > Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell. 해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    위 예제는 hello, 바꿉니다 **clustername** Giraph 설치 되어 있는 HDInsight 클러스터의 hello 이름으로 합니다.
3. Hello 결과 확인 합니다. Hello 결과 hello에 두 개의 출력 파일에 저장 될 hello 작업이 완료 되 면 **wasb: / / / 예제/out/shotestpaths** 폴더입니다. hello 파일 이라고 **파트-m-00001** 및 **00002-m-부분이**합니다. Hello 단계 toodownload 및 보기 hello 출력 다음을 수행 합니다.

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    이렇게 하면 hello 만들어집니다 **예제/출력/shortestpaths** hello 워크스테이션 및 다운로드 hello 두 출력 파일 toothat 위치에서 현재 디렉터리에서 디렉터리 구조입니다.

    사용 하 여 hello **Cat** hello 파일 내용의 toodisplay hello cmdlet:

        Cat example/output/shortestpaths/part*

    hello 출력에는 비슷한 toohello 다음과 같아야 합니다.

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    hello SimpleShortestPathComputation 예제 개체 ID가 1와 하드 코드 된 toostart and hello 가장 짧은 경로 tooother 개체를 찾는입니다. Hello 출력으로 읽어야 하므로 `destination_id distance`여기서 거리는 hello 가장자리 짧아 지도록 hello 값 (또는 가중치) 개체 ID가 1 사이의 hello 대상 id입니다.

    이 시각화를 ID 1과 다른 모든 개체 사이의 hello 가장 짧은 경로 이동 하 여 hello 결과 확인할 수 있습니다. ID가 1에서 ID 4 사이의 최단 경로 hello 참고는 5입니다. 이 hello 사이의 총 거리 <span style="color:orange">ID 1과 3</span>, 차례로 <span style="color:red">ID가 3 및 4</span>합니다.

    ![가장 짧은 경로와 함께 원으로 그린 개체](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Aure PowerShell을 사용하여 Giraph 설치
[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.  hello 샘플 방법을 tooinstall Azure PowerShell을 사용 하 여 Spark 합니다. Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)합니다.

## <a name="install-giraph-using-net-sdk"></a>.NET SDK을 사용하여 Giraph 설치
[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요. hello 샘플 방법을 tooinstall Spark.NET SDK hello를 사용 하 여 합니다. Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)합니다.

## <a name="see-also"></a>참고 항목
* [HDInsight Hadoop 클러스터에 Giraph 설치(Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.
* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)
* [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.
* [HDInsight 클러스터에서 R 설치][hdinsight-install-r]: R 설치에 대한 스크립트 작업 샘플입니다.
* [HDInsight 클러스터에서 Solr 설치](hdinsight-hadoop-solr-install.md): Solr 설치에 대한 스크립트 작업 샘플입니다.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
