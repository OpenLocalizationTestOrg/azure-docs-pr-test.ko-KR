---
title: "Azure HDInsight 하이브 ODBC 드라이버-hello로 aaaConnect Excel tooHadoop | Microsoft Docs"
description: "어떻게 tooset를 사용 하 여 hello Excel tooquery 데이터 Microsoft Excel에서 HDInsight 클러스터에 대 한 Microsoft 하이브 ODBC 드라이버에 알아봅니다."
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Azure HDInsight의 Excel tooHadoop hello Microsoft 하이브 ODBC 드라이버를 사용 하 여 연결

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Microsoft의 빅 데이터 솔루션인 Azure HDInsight hello 하 여 배포 된 Apache Hadoop 클러스터와 Microsoft BI (Business Intelligence) 구성 요소를 통합 합니다. 이 통합의 예로 hello 기능 tooconnect Excel toohello 하이브의 데이터 웨어하우스를 hello Microsoft 하이브 데이터베이스 ODBC (Open Connectivity) 드라이버를 사용 하 여 HDInsight의 Hadoop 클러스터.

HDInsight 클러스터와 다른 데이터 소스와 연결 된 가능한 tooconnect hello 데이터 이기도, 다른 (비-HDInsight) 포함 하 여 Hadoop 클러스터 hello를 사용 하 여 Excel에서 Microsoft Power Query 추가 기능에 Excel 용입니다. 설치 및 파워 쿼리 사용에 대 한 정보를 참조 하십시오. [파워 쿼리를 통해 Excel 연결 tooHDInsight][hdinsight-power-query]합니다.

> [!NOTE]
> 단계를 hello 하는 동안이 문서는 Linux 중 하나는 함께 사용할 수 있습니다 이거나 Windows 기반 HDInsight 클러스터를 Windows hello 클라이언트 워크스테이션에 대 한 필요 합니다.
> 
> 

**필수 조건**:

이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **HDInsight 클러스터**. 하나의 toocreate 참조 [Azure HDInsight 시작][hdinsight-get-started]합니다.
* **워크스테이션** 

## <a name="install-microsoft-hive-odbc-driver"></a>Microsoft Hive ODBC 드라이버 설치
에서 다운로드 및 설치 Microsoft ODBC Driver 하이브 hello [다운로드 센터][hive-odbc-driver-download]합니다.

이 드라이버는 32비트 또는 64비트 버전의 Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 및 Windows Server 2012에 설치할 수 있습니다. hello 드라이버를 사용 하면 연결 tooAzure HDInsight (버전 1.6 이상) 및 Azure HDInsight 에뮬레이터 (v.1.0.0.0 및 이후 버전). Hello ODBC 드라이버를 사용 하는 hello 응용 프로그램의 hello 버전과 일치 하는 hello 버전을 설치 해야 합니다. 이 자습서에 대 한 hello 드라이버 Office Excel에서 사용 됩니다.

## <a name="create-hive-odbc-data-source"></a>Hive ODBC 데이터 원본 만들기
hello 다음 단계 방법을 보여 줍니다 toocreate 하이브 ODBC 데이터 원본입니다.

1. Windows 8 또는 Windows 10에서 hello Windows 키 tooopen hello 시작 화면에서를 누르고 다음 입력 **데이터 소스**합니다.
2. Office 버전에 따라 **ODBC 데이터 원본 설정(32비트)** 또는 **ODBC 데이터 원본 설정(64비트)**을 클릭합니다. Windows 7을 사용하는 경우 **관리 도구**에서 **ODBC 데이터 원본(32비트)** 또는 **ODBC 데이터 원본(64비트)**을 선택합니다. Hello 표시 **ODBC 데이터 원본 관리자** 대화 상자.
   
    ![OBDC 데이터 원본 관리자](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "ODBC 데이터 원본 관리자를 사용하여 DSN 구성")

3. 사용자 DNS에서 클릭 **추가** tooopen hello **새 데이터 원본 만들기** 마법사.
4. **Microsoft Hive ODBC 드라이버**를 선택한 후 **마침**을 클릭합니다. Hello 표시 **Microsoft 하이브 ODBC 드라이버 DNS 설정** 대화 상자.
5. 입력 하거나 다음 값에는 hello 선택:
   
   | 속성 | 설명 |
   | --- | --- |
   |  데이터 원본 이름 |이름 tooyour 데이터 소스를 제공 합니다. |
   |  호스트 |&lt;HDInsightClusterName>.azurehdinsight.net을 입력합니다. 예를 들면 myHDICluster.azurehdinsight.net과 같습니다. |
   |  포트 |<strong>443</strong>을 사용합니다. (이 포트를 변경 하지 563 too443에서.) |
   |  데이터베이스 |<strong>기본값</strong>을 사용합니다. |
   |  메커니즘 |<strong>Azure HDInsight Service</strong> 선택 |
   |  사용자 이름 |HDInsight 클러스터 HTTP 사용자의 사용자 이름을 입력합니다. hello 기본 사용자 이름은 <strong>admin</strong>합니다. |
   |  암호 |HDInsight 클러스터 사용자 암호 입력 |
   
    </table>
   
    몇 가지 중요 한 매개 변수 toobe 클릭할 때 알고 있는 **고급 옵션**:
   
   | 매개 변수 | 설명 |
   | --- | --- |
   |  Use Native Query |옵션을 선택 하면 hello ODBC 드라이버는 HiveQL를 tooconvert TSQL 시도 하지 않습니다. 순수 HiveQL 문을 제출하는 것이 확실한 경우에만 이 옵션을 사용합니다. TooSQL 서버 또는 Azure SQL 데이터베이스를 연결할 때 그대로 두어야 선택 취소 합니다. |
   |  Rows fetched per block |많은 수의 레코드를 인출 하는 경우이 매개 변수를 튜닝 최적의 성능이 필요한 tooensure 수 있습니다. |
   |  Default string column length, Binary column length, Decimal column scale |hello 데이터 형식 길이 정밀도 데이터 반환 방법에 영향을 줄 수 있습니다. 잘못 된 정보가 toobe 인해 반환 된 소멸자의 정밀도 및/또는 잘림 tooloss 합니다. |

    ![고급 옵션](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "고급 DSN 구성 옵션")

1. 클릭 **테스트** tootest hello 데이터 원본입니다. 표시 hello 데이터 소스를 올바르게 구성 된 경우 *테스트 완료 되었습니다!*합니다.
2. 클릭 **확인** tooclose hello 테스트 대화 상자. 새 데이터 원본을 hello hello에 나열 되어야은 **ODBC 데이터 원본 관리자**합니다.
3. 클릭 **확인** tooexit hello 마법사.

## <a name="import-data-into-excel-from-hdinsight"></a>HDInsight에서 Excel로 데이터 가져오기
hello 다음 단계에서는 hello 방식으로 하이브 테이블에서 데이터를 tooimport hello 이전 섹션에서 만든 hello ODBC 데이터 원본을 사용 하 여 Excel 통합 문서에.

1. Excel에서 새 통합 문서나 기존 통합 문서를 엽니다.
2. Hello에서 **데이터** 탭을 클릭 **데이터 가져오기**, 클릭 **기타 원본**, 클릭 하 고 **에서 ODBC** toolaunch hello  **데이터 연결 마법사**합니다.
   
    ![데이터 연결 마법사 열기](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "데이터 연결 마법사 열기")
4. 선택 hello 데이터 원본 이름 hello 마지막 섹션에서 만든 등록 한 다음 클릭 **확인**합니다.
5. Hadoop 사용자 이름을 입력 하십시오 (hello 기본 이름은 관리자) 암호를 hello와 클릭 **연결**합니다.
6. 탐색 창에서 **HIVE**를 확장하고 **default**를 확장한 후 **hivesampletable**을 클릭하고 **로드**를 클릭합니다. 걸리는 시간은 몇 초 전에 데이터를 가져온된 tooExcel 가져옵니다.

    ![HDInsight Hive ODBC 탐색기](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "데이터 연결 열기 마법사")


## <a name="next-steps"></a>다음 단계
이 문서에서는 toouse hello HDInsight 서비스에서에서 Microsoft 하이브 ODBC 드라이버 tooretrieve 데이터를 Excel로 hello 하는 방법을 배웠습니다. 마찬가지로, SQL 데이터베이스에 hello HDInsight 서비스에서에서 데이터를 검색할 수 있습니다. HDInsight 서비스에 대 한 가능한 tooupload 데이터 이기도합니다. toolearn 더 참조 하십시오.

* [HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-data]
* [데이터 tooHDInsight 업로드][hdinsight-upload-data]
* [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


