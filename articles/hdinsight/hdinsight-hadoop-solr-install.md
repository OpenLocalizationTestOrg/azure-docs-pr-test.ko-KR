---
title: "Hadoop 클러스터-Azure에서 aaaUse 스크립트 동작 tooinstall Solr | Microsoft Docs"
description: "스크립트 동작을 사용 하 여 Solr 인 toocustomize HDInsight 클러스터를 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Windows 기반 HDInsight 클러스터에서 Solr 설치 및 사용

스크립트 동작을 사용 하 여 Solr 인 toocustomize Windows 기반 HDInsight 클러스터를 방법 등에 대해 알아보기 toouse Solr toosearch 데이터입니다.

> [!IMPORTANT]
> 이 문서 에서만 작동 하는 Windows 기반 HDInsight 클러스터의에서 hello 단계. HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. Linux 기반 클러스터와 함께 Solr을 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Solr 설치 및 사용(Linux)](hdinsight-hadoop-solr-install-linux.md)을 참조하세요.


*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 Solr을 설치할 수 있습니다. HDInsight 클러스터에서 샘플 스크립트 tooinstall Solr에서 읽기 전용 Azure 저장소 blob에서 사용할 수는 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)합니다.

hello 샘플 스크립트는 HDInsight 클러스터 버전 3.1과만 작동합니다. HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.

이 항목에 사용 된 hello 샘플 스크립트는 특정 구성으로 Windows 기반 Solr 클러스터를 만듭니다. Tooconfigure hello Solr 클러스터에 다른 컬렉션, 분할 된 데이터베이스, 스키마, 복제본 등을 사용 하도록 하려는 경우 수정 해야 hello 스크립트 및 Solr 이진 적절 하 게 합니다.

**관련된 문서**

* [HDInsight Hadoop 클러스터에서 Solr 설치 및 사용(Linux)](hdinsight-hadoop-solr-install-linux.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.
* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)

## <a name="what-is-solr"></a>Solr이란?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a>은 데이터에 대한 강력한 전체 텍스트 검색을 가능하게 해주는 엔터프라이즈 검색 플랫폼입니다. Hadoop에 저장 하 고 방대한 양의 데이터를 관리 있습니다, Apache Solr hello 검색 기능이 제공 tooquickly hello 데이터를 검색 합니다.

## <a name="install-solr-using-portal"></a>포털을 사용하여 Solr 설치
1. Hello를 사용 하 여 클러스터를 만들기 시작 **사용자 지정 만들기** 옵션에 설명 된 대로 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-provision-clusters.md)합니다.
2. Hello에 **스크립트 동작** 페이지 hello 마법사의 클릭 **스크립트 동작 추가** 아래와 같이 tooprovide hello 스크립트 동작에 대 한 세부 정보:

    ![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")

    <table border='1'>
        <tr><th>속성</th><th>값</th></tr>
        <tr><td>이름</td>
            <td>Hello 스크립트 동작에 대 한 이름을 지정 합니다. 예를 들면 <b>Install Solr</b>과 같습니다.</td></tr>
        <tr><td>스크립트 URI</td>
            <td>호출 된 toocustomize hello 클러스터는 hello 식별자 URI (Uniform Resource) toohello 스크립트를 지정 합니다. 예를 들면 <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>과 같습니다.</td></tr>
        <tr><td>노드 유형</td>
            <td>Hello 사용자 지정 스크립트가 실행 되는 hello 노드를 지정 합니다. <b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.
        <tr><td>매개 변수</td>
            <td>Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다. hello 스크립트 tooinstall Solr 모든 매개 변수를 필요 하지 않으므로이 비워 둘 수 있습니다.</td></tr>
    </table>

    Hello 클러스터에서 둘 이상의 스크립트 동작 tooinstall 여러 구성 요소를 추가할 수 있습니다. Hello 스크립트를 추가한 후 hello 확인 표시 toostart hello 클러스터 만들기를 클릭 합니다.

## <a name="use-solr"></a>Solr 사용
데이터 파일로 Solr을 인덱싱하는 것부터 시작해야 합니다. Toorun 검색 쿼리 Solr hello 인덱싱된 데이터에 사용할 수 있습니다. Hello 단계 toouse Solr HDInsight 클러스터에서 다음을 수행 합니다.

1. **Tooremote 프로토콜 RDP (원격 데스크톱)를 사용 하 여 설치 Solr와 hello HDInsight 클러스터에**합니다. Hello Azure 포털에서에서 Solr 설치 되어 있으며 다음 원격으로 hello 클러스터를 사용 하 여 만든 hello 클러스터에 대 한 원격 데스크톱을 사용 합니다. 자세한 내용은 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.
2. **데이터 파일을 업로드하여 Solr을 인덱싱**합니다. Solr 인덱싱하면 기록 하는 모든 문서 toosearch에 필요할 수 있는 합니다. tooindex Solr 사용 하 여 RDP tooremote hello 클러스터로 이동 toohello 데스크톱 hello Hadoop 명령줄을 열고 너무 이동**C:\apps\dist\solr-4.7.2\example\exampledocs**합니다. Hello 다음 명령을 실행 합니다.

        java -jar post.jar solr.xml monitor.xml

    Hello hello 콘솔에 출력 뒤에 표시 됩니다.

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    hello post.jar 유틸리티 두 예제 문서를 사용 하 여 Solr를 인덱스 **solr.xml** 및 **monitor.xml**합니다. hello post.jar 유틸리티 및 hello 샘플 문서는 Solr 설치 합니다.
3. **Hello 내에서 사용 하 여 hello Solr 대시보드 toosearch 인덱싱된 문서**합니다. Hello RDP 세션 toohello HDInsight 클러스터, Internet Explorer를 열어 및 시작 시 hello Solr 대시보드 **http://headnodehost:8983/solr / #/**합니다. Hello 왼쪽 창의 hello에서 **코어 선택기** 드롭다운 목록에서 선택 **collection1**, 클릭 하 고 **쿼리**합니다. 예, tooselect 및 반환 Solr에서 모든 hello docs hello 다음 값을 제공 합니다.

   * Hello에 **q** 텍스트 상자에 입력  **\*:**\*합니다. 이렇게 하면 Solr에 인덱싱된 모든 hello 문서가 반환 됩니다. Toosearch hello 문서 내에서 특정 문자열을 하려는 경우에 여기에 해당 문자열을 입력할 수 있습니다.
   * Hello에 **wt** 텍스트 상자, 선택 hello 출력 형식입니다. 기본값은 **json**입니다. **Execute Query**를 클릭합니다.

     ![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "쿼리 Solr 대시보드에서 실행")

     hello 출력 hello 인덱싱 Solr에 대해 두 명의 문서를 반환 합니다. hello 출력 hello 다음과 유사합니다.

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **권장: hello 백업 Solr tooAzure hello HDInsight 클러스터와 연결 된 Blob 저장소에서에서 데이터를 인덱싱할**합니다. 것이 좋습니다 Azure Blob 저장소에 hello Solr 클러스터 노드에서 hello 인덱싱된 데이터를 백업 해야 합니다. Hello 단계 toodo 되므로 다음을 수행 합니다.

   1. Hello RDP 세션에서 Internet Explorer 및 지점 toohello url을 엽니다.

           http://localhost:8983/solr/replication?command=backup

       다음과 같은 응답이 표시됩니다.

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. Hello 원격 세션에서 탐색 너무 {SOLR_HOME}\{컬렉션} \data 합니다. 이 hello 샘플 스크립트를 통해 만든 hello 클러스터에 대 한 해야 **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**합니다. 이 위치에서 사용 하 여 만든 이름을 비슷한 너무 스냅숏 폴더를 표시 되어야**스냅숏.* 타임 스탬프** *입니다.
   3. TooAzure Blob 저장소에 업로드 하 고 hello 스냅숏 폴더를 압축 합니다. Hello Hadoop 명령줄에서 다음 명령을 hello를 사용 하 여 toohello hello 스냅숏 폴더 위치를 이동 합니다.

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       이 명령은 복사본 hello 스냅숏 너무/예제/데이터/hello 기본 저장소 내 hello 컨테이너에서 hello 클러스터와 연결 된 계정입니다.

## <a name="install-solr-using-aure-powershell"></a>Aure PowerShell을 사용하여 Solr 설치
[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.  hello 샘플 방법을 tooinstall Azure PowerShell을 사용 하 여 Spark 합니다. Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)합니다.

## <a name="install-solr-using-net-sdk"></a>.NET SDK를 사용하여 Solr 설치
[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요. hello 샘플 방법을 tooinstall Spark.NET SDK hello를 사용 하 여 합니다. Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)합니다.

## <a name="see-also"></a>참고 항목
* [HDInsight Hadoop 클러스터에서 Solr 설치 및 사용(Linux)](hdinsight-hadoop-solr-install-linux.md)
* [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.
* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)
* [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.
* [HDInsight 클러스터에서 R 설치][hdinsight-install-r]: R 설치에 대한 스크립트 작업 샘플입니다.
* [HDInsight 클러스터에서 Giraph 설치](hdinsight-hadoop-giraph-install.md): Giraph 설치에 대한 스크립트 작업 샘플입니다.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
