---
title: "데이터 레이크 저장소와 Sqoop를 사용 하 여 Azure SQL 데이터베이스 간에 데이터 aaaCopy | Microsoft Docs"
description: "Azure SQL 데이터베이스와 데이터 레이크 저장소 Sqoop toocopy 데이터를 사용 하 여"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Sqoop를 사용하여 Data Lake 저장소와 Azure SQL 데이터베이스 간에 데이터 복사
자세한 내용은 방법 간에 Azure SQL 데이터베이스 및 데이터 레이크 저장소 toouse Apache Sqoop tooimport 및 내보내기 데이터입니다.

## <a name="what-is-sqoop"></a>Sqoop 정의
빅 데이터 응용 프로그램은 로그 및 파일과 같은 비구조적 및 반구조적 데이터를 처리하기 위한 자연스러운 선택입니다. 그러나 수도 있습니다 관계형 데이터베이스에 저장 된 필요 tooprocess 구조화 된 데이터입니다.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) 은 설계 된 도구 tootransfer 관계형 데이터베이스와 같은 데이터 레이크 저장소는 빅 데이터 저장소 간에 데이터입니다. 데이터 레이크 저장소로 tooimport 데이터 Azure SQL 데이터베이스 같은 관계형 데이터베이스 관리 시스템 RDBMS ()를에서 것 사용할 수 있습니다. 다음이 변환 하 고 및 빅 데이터 워크 로드를 사용 하 여 hello 데이터를 분석 하 고, 다음 RDBMS에 다시 hello 데이터를 내보낼 수 있습니다. 이 자습서에서 관계형 데이터베이스 tooimport/내보내기를으로 Azure SQL 데이터베이스를 사용 합니다.

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* **Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다. [Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요. 이 문서에서는 Data Lake 저장소가 있는 HDInsight Linux 클러스터 액세스 권한이 있는 것으로 가정합니다.
* **Azure SQL 데이터베이스**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>비디오로 빠르게 배우시겠습니까?
[이 비디오를 시청](https://mix.office.com/watch/1butcdjxmu114) 방법에 Azure 저장소 Blob와 DistCp를 사용 하 여 데이터 레이크 저장소 간에 toocopy 데이터입니다.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Hello Azure SQL 데이터베이스에서에서 예제 테이블 만들기
1. toostart는 hello Azure SQL 데이터베이스에에서 두 개의 샘플 테이블을 만듭니다. 사용 하 여 [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 또는 Visual Studio tooconnect toohello Azure SQL 데이터베이스 실행된 hello 쿼리를 따르십시오.

    **Table1 만들기**

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    **Table2 만들기**

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. **Table1**에서 몇 가지 샘플 데이터를 추가합니다. **Table2** 를 빈 상태로 둡니다. **Table1** 에서 Data Lake 저장소로 데이터를 가져옵니다. 그런 다음 Data Lake 저장소에서 **Table2**로 데이터를 내보냅니다. 다음 코드 조각 hello를 실행 합니다.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>사용 하는 HDInsight 클러스터에서 사용 하 여 Sqoop tooData 레이크 스토어에 액세스
HDInsight 클러스터에 사용할 수 있는 hello Sqoop 패키지에 이미 있습니다. 추가 저장소로 hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 경우 (이 예에서는 Azure SQL 데이터베이스)의 관계형 데이터베이스 간의 구성 변경) (없이 Sqoop tooimport/내보내기 데이터를 사용할 수 있습니다 및 데이터 레이크 저장소 계정입니다.

1. 이 자습서에서는 SSH tooconnect toohello 클러스터를 사용 해야 하는 Linux 클러스터 만들어지므로 한다고 가정 합니다. 참조 [연결 tooa Linux 기반 HDInsight 클러스터](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.
2. 데이터 레이크 저장소 계정 hello hello 클러스터에서 액세스할 수 있는지 확인 합니다. Hello hello SSH 프롬프트에서 다음 명령을 실행 합니다.

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    이 hello Data Lake 저장소 계정에서에서 파일/폴더의 목록을 제공 해야 합니다.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Azure SQL 데이터베이스에서 Data Lake 저장소로 데이터 가져오기
1. Sqoop 패키지를 사용할 수 있는 toohello 디렉터리를 이동 합니다. 일반적으로 `/usr/hdp/<version>/sqoop/bin`에 있습니다.
2. Hello 데이터를 가져올 **Table1** hello Data Lake 저장소 계정에 있습니다. 구문 다음 hello를 사용 합니다.

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    **데이터베이스 서버 이름 sql** 자리 표시자 hello Azure SQL 데이터베이스 실행 되 고 있는 hello 서버 hello 이름을 나타냅니다. **sql 데이터베이스 이름** 자리 표시자 hello 실제 데이터베이스 이름을 나타냅니다.

    예를 들면 다음과 같습니다.


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. 된 데이터는 해당 hello 전송 toohello 데이터 레이크 저장소 계정을 확인 합니다. Hello 다음 명령을 실행 합니다.

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    다음 출력 hello를 표시 되어야 합니다.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    각 **파트-m-*** 파일 hello 원본 테이블의 tooa 행은 해당 **Table1**합니다. -M-hello 부분의 hello 내용을 볼 수 * tooverify 파일입니다.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Data Lake 저장소에서 Azure SQL 데이터베이스로 데이터 내보내기
1. 데이터 레이크 저장소 계정 toohello 빈 테이블을에서 hello 데이터 내보내기 **Table2**, hello Azure SQL 데이터베이스에에서 있습니다. 구문 다음 hello를 사용 합니다.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    예를 들면 다음과 같습니다.


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. 데이터를 해당 hello 업로드 toohello SQL 데이터베이스 테이블을 확인 합니다. 사용 하 여 [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 또는 Visual Studio tooconnect toohello Azure SQL 데이터베이스 누른 실행된 hello 다음 쿼리 합니다.

        SELECT * FROM TABLE2

    이 출력을 따라 hello가 있어야 합니다.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Sqoop 사용에 대한 성능 고려 사항

성능 튜닝에 Sqoop 작업 toocopy 데이터 tooData 레이크 저장소, 참조 [Sqoop 성능 문서](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)합니다.

## <a name="see-also"></a>참고 항목
* [Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사](data-lake-store-copy-data-azure-storage-blob.md)
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
