---
title: "HDInsight toocustomize 클러스터-Azure에서에서 R aaaUse | Microsoft Docs"
description: "자세한 방법을 스크립트 tooinstall R를 사용 하 여 동작 및 HDInsight 클러스터에서 R 사용 합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>HDInsight Hadoop 클러스터에 R 설치 및 사용

Windows toocustomize r 스크립트 동작을 사용 하 여 HDInsight 클러스터에 기반 하는 방법 및 HDInsight의 R toouse 클러스터 방법에 대해 알아봅니다. hello [HDInsight 제공](https://azure.microsoft.com/pricing/details/hdinsight/) HDInsight 클러스터의 일부로 R 서버를 포함 합니다. 이렇게 하면 R 스크립트 toouse MapReduce 및 Spark distributed toorun 계산 합니다. 자세한 내용은 [HDInsight에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요. Linux 기반 클러스터와 함께 R을 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)](hdinsight-hadoop-r-scripts-linux.md)을 참조하세요.

*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 R을 설치할 수 있습니다. HDInsight 클러스터에서 샘플 스크립트 tooinstall R에서 읽기 전용 Azure 저장소 blob에서 사용할 수는 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)합니다.

**관련된 문서**

* [HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.
* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>R이란?
hello <a href="http://www.r-project.org/" target="_blank">for Statistical Computing R 프로젝트</a> 는 오픈 소스 언어 및 환경 통계 컴퓨팅입니다. R은 수백 개의 통계 함수와 기능 및 개체 지향 프로그래밍의 측면을 결합하는 자체 프로그래밍 언어를 제공합니다. 또한 광범위한 그래픽 기능도 제공합니다. R은 전문적인 통계학자 및 다양 한 필드에에서 과학자 hello 기본 프로그래밍 환경입니다.

R은 Azure Blob 저장소(WASB)와 호환되므로 HDInsight의 R을 사용하여 이 저장소에 저장된 데이터를 처리할 수 있습니다.  

## <a name="install-r"></a>R 설치
A [샘플 스크립트](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R는 HDInsight 클러스터에는 Azure 저장소에 읽기 전용 blob에서 사용할 수 있습니다. 이 섹션에서는 toouse hello Azure 포털을 사용 하 여 hello 클러스터를 만드는 동안 샘플 스크립트를 hello 하는 방법에 대 한 지침을 제공 합니다.

> [!NOTE]
> hello 샘플 스크립트는 HDInsight 클러스터 버전이 3.1에 도입 되었습니다. HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.
>
>

1. Hello 포털에서에서 하는 HDInsight 클러스터를 만들 때 클릭 **옵션 구성**, 클릭 하 고 **스크립트 동작**합니다.
2. Hello에 **스크립트 동작** 페이지에서 다음 값에는 hello를 입력 합니다.

    ![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")

    <table border='1'>
        <tr><th>속성</th><th>값</th></tr>
        <tr><td>이름</td>
            <td>예를 들어 hello 스크립트 동작의 이름을 지정 <b>R 설치</b>합니다.</td></tr>
        <tr><td>스크립트 URI</td>
            <td>예를 들어 호출 된 toocustomize hello 클러스터 있는 hello URI toohello 스크립트 지정 <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>노드 유형</td>
            <td>Hello 사용자 지정 스크립트가 실행 되는 hello 노드를 지정 합니다. <b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.
        <tr><td>매개 변수</td>
            <td>Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다. 그러나, hello 스크립트 tooinstall R이을 비워 둘 수 있도록 매개 변수가 필요 하지 않습니다.</td></tr>
    </table>

    Hello 클러스터에서 둘 이상의 스크립트 동작 tooinstall 여러 구성 요소를 추가할 수 있습니다. Hello 스크립트를 추가한 후에 hello 확인 표시가 toostart hello 클러스터를 만들 수 있는 클릭 합니다.

Azure PowerShell 또는 hello HDInsight.NET SDK를 사용 하 여 HDInsight의 hello 스크립트 tooinstall R를 사용할 수 있습니다. 이 절차에 대한 자세한 내용은 이 문서의 뒷부분에 제공됩니다.

## <a name="run-r-scripts"></a>R 스크립트 실행
이 섹션에서는 HDInsight와 toorun R 스크립트 hello Hadoop에 클러스터 되는 방법을 설명 합니다.

1. **원격 데스크톱 연결 toohello 클러스터 설정**: hello 포털에서에서 R 설치를 사용 하 여 만든 hello 클러스터에 대 한 원격 데스크톱을 사용 하 고 다음 toohello 클러스터에 연결 합니다. 자세한 내용은 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.
2. **열기 hello R 콘솔**: hello R 설치 hello 헤드 노드의 hello 바탕 화면에서 링크 toohello R 콘솔을 넣습니다. 클릭 하 여 조치 tooopen hello R 콘솔.
3. **Hello R 스크립트 실행**: 붙여 넣어을 선택 하 고 ENTER 키를 눌러 여 hello R 콘솔에서 직접 hello R 스크립트를 실행할 수 있습니다. 숫자 1 too100 hello를 생성 하 고 2로 곱하여 하는 간단한 예제 스크립트는 다음과 같습니다.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

hello 처음 두 줄 호출 hello RHadoop 라이브러리 오른쪽과 함께 설치 된 hello 마지막 줄 인쇄 hello 결과 toohello 콘솔. hello 출력은 다음과 같이 표시 됩니다.

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Azure PowerShell을 사용하여 R 설치
[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.  hello 샘플 방법을 tooinstall Azure PowerShell을 사용 하 여 Spark 합니다. Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)합니다.

## <a name="install-r-using-net-sdk"></a>.NET SDK를 사용하여 R 설치
[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요. hello 샘플 방법을 tooinstall Spark.NET SDK hello를 사용 하 여 합니다. Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)합니다.

## <a name="see-also"></a>참고 항목
* [HDInsight Hadoop 클러스터에 R 설치 및 사용(Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.
* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)
* [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.
* [HDInsight 클러스터에서 Giraph 설치](hdinsight-hadoop-giraph-install.md): Giraph 설치에 대한 스크립트 작업 샘플입니다.
* [HDInsight 클러스터에서 Solr 설치](hdinsight-hadoop-solr-install-linux.md): Solr 설치에 대한 스크립트 작업 샘플입니다.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
