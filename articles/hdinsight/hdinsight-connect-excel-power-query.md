---
title: "파워 쿼리-Azure HDInsight를 통해 Excel tooHadoop aaaConnect | Microsoft Docs"
description: "Business intelligence 구성 요소와 파워 쿼리를 사용 하 여 Excel tooaccess 데이터에 대 한 tootake 활용 HDInsight의 Hadoop에 저장 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>파워 쿼리를 사용 하 여 Excel tooHadoop 연결
Hello Microsoft 빅 데이터 솔루션의 주요 기능 중 하나는 hello Azure HDInsight의 Hadoop 클러스터와 Microsoft business intelligence (BI) 구성 요소를 통합 합니다. 기본 예제는 hello 기능 tooconnect Excel toohello Excel 추가 기능에 대 한 hello Microsoft 파워 쿼리를 사용 하 여 Hadoop 클러스터와 연결 된 hello 데이터를 포함 하는 Azure 저장소 계정입니다. 이 문서를 tooset 및 사용 하 여 Hadoop 클러스터와 연결 된 파워 쿼리 tooquery 데이터 HDInsight와 관리 하는 방법을 안내 합니다.

### <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **HDInsight 클러스터**. 하나의 tooconfigure 참조 [Azure HDInsight 시작][hdinsight-get-started]합니다.
* **워크스테이션** .
* **Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, Excel 2013 Standalone 또는 Office 2010 Professional Plus**.

## <a name="install-power-query"></a>파워 쿼리 설치
파워 쿼리는 출력되었거나 HDInsight 클러스터에 대해 실행되는 Hadoop 작업에서 생성된 데이터를 가져올 수 있습니다.

Excel 2016의 파워 쿼리는 간단한 Get & 변환 섹션 아래의 hello 데이터 리본에 통합 되어 있습니다. 이전 Excel 버전에 대 한 Microsoft Power Query for Excel hello에서 다운로드 [Microsoft 다운로드 센터] [ powerquery-download] 하 고 설치 합니다.

## <a name="import-hdinsight-data-into-excel"></a>Excel로 HDInsight 데이터 가져오기
파워 쿼리 추가 기능에 Excel 용 hello 쉽게 tooimport 데이터를를 Excel PowerPivot 및 파워 맵 등의 BI 도구 수 사용된 tooinspect 수, 분석 및 hello 데이터를 제공 하는 위치에 HDInsight 클러스터에 있습니다.

**HDInsight 클러스터에서 tooimport 데이터**

1. Excel을 엽니다.
2. 비어 있는 새 통합 문서를 만듭니다.
3. Hello hello Excel 버전에 따라 단계를 수행 합니다.

    - Excel 2016

        - Hello 클릭 **데이터** 메뉴에서 클릭 **데이터 가져오기** hello에서 **데이터 가져오기 및 변환** 리본에서 클릭 **에서 Azure**, 를클릭한다음 **Azure HDInsight(HDFS)에서**합니다.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Hello 클릭 **파워 쿼리** 메뉴를 클릭 **에서 Azure**, 클릭 하 고 **Microsoft Azure HDInsight에서**합니다.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **참고:** hello 표시 되지 않으면 **파워 쿼리** 메뉴 너무 이동**파일** > **옵션** > **추가기능**를 선택 하 고 **COM 추가 기능** hello 드롭다운 목록에서 **관리** 상자 hello hello 페이지 맨 아래에 있습니다. 선택 hello **이동 중...**  단추 및 Excel 추가 기능에 대 한 파워 쿼리 hello 검사 된에 대 한 hello 상자를 확인 합니다.
       
        **참고:** 파워 쿼리 수도 있습니다 tooimport 데이터 HDFS에서 클릭 하 여 **기타 원본**합니다.
4. 에 대 한 **계정 이름**의 hello Azure Blob 저장소 계정에 클러스터와 연결 된 hello 이름을 입력 한 다음 클릭 **확인**합니다. 이 계정은 hello 수 [기본 저장소 계정](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) 또는 연결 된 저장소 계정입니다.  hello 형식은 *https://&lt;StorageAccountName >.blob.core.windows.net/*합니다.
5. 에 대 한 **계정 키**hello Blob 저장소 계정에 대 한 hello 키를 입력 한 다음 클릭 **저장**합니다. (필요 tooenter hello 계정 정보만 hello 처음으로이 저장소에 액세스 합니다.)
6. Hello에 **탐색기** hello 쿼리 편집기의 왼쪽 창에서 hello, hello Blob 저장소 컨테이너 이름을 두 번 클릭 합니다. 기본적으로 컨테이너 이름을 hello는 hello 동일 hello 클러스터 이름으로 이름입니다.
7. 찾을 **HiveSampleData.txt** hello에 **이름** 열 (hello 폴더 경로 **... / hive/웨어하우스/hivesampletable/**)를 클릭 하 고 **이진** HiveSampleData.txt 창의 hello 왼쪽에 있습니다. HiveSampleData.txt 모든 hello 클러스터 함께 제공 됩니다. 필요에 따라 사용자의 파일을 사용할 수 있습니다.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. 원하는 경우 hello 열 이름을 바꿀 수 있습니다. 준비가 되면 **닫은 후 로드**를 클릭합니다.  hello 데이터는 로드 tooyour 통합 되었습니다.
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>다음 단계
이 문서에서는 방법에 대해 배웠습니다 toouse HDInsight Excel의에서 파워 쿼리 tooretrieve 데이터입니다. 마찬가지로 HDInsight에서 Azure SQL 데이터베이스로 데이터를 가져올 수 있습니다. HDInsight에 가능한 tooupload 데이터 이기도합니다. 더 toolearn hello 다음 문서를 참조:

* [Microsoft ODBC Driver 하이브 hello를 사용 하 여 Excel tooHDInsight 연결][hdinsight-ODBC]
* [데이터 tooHDInsight 업로드][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
