---
title: "Azure 가상 컴퓨터에서 aaaMove 데이터 tooSQL 서버 | Microsoft Docs"
description: "Azure VM에서 온-프레미스 SQL Server tooSQL 서버 또는 플랫 파일에서 데이터를 이동 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Azure 가상 컴퓨터에서 데이터 tooSQL 서버 이동
이 항목에서는 플랫 파일 (CSV 또는 TSV 형식)에서 또는 온-프레미스 SQL Server tooSQL 서버에서에서 Azure 가상 컴퓨터 내의 데이터를 이동 하는 것에 대 한 hello 옵션을 설명 합니다. 이동 데이터가 toohello 클라우드에 대 한 이러한 작업은 일부 hello 팀 데이터 과학 프로세스입니다.

기계 학습에 대 한 이동 데이터 tooan Azure SQL 데이터베이스에 대 한 hello 옵션에 간략하게 설명 하는 항목을 참조 하십시오. [Azure 기계 학습에 대 한 데이터 tooan Azure SQL 데이터베이스를 이동](machine-learning-data-science-move-sql-azure.md)합니다.

hello **메뉴** hello 데이터 저장 끌어다 하는 동안 처리할 수 있는 다른 대상 환경으로 데이터 tooingest 팀 데이터 과학 프로세스 (TDSP) hello 하는 방법을 설명 하는 링크 tootopics 아래 합니다.

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

hello 다음 표에 요약 되어 Azure 가상 컴퓨터에서 이동 데이터 tooSQL 서버에 대 한 hello 옵션입니다.

| <b>원본</b> | <b>대상: Azure VM의 SQL Server</b> |
| --- | --- |
| <b>플랫 파일</b> |1. <a href="#insert-tables-bcp">명령줄 BCP(대량 복사 유틸리티)</a><br> 2. <a href="#insert-tables-bulkquery">대량 삽입 SQL 쿼리</a><br> 3. <a href="#sql-builtin-utilities">SQL Server의 기본 제공 그래픽 유틸리티</a> |
| <b>온-프레미스 SQL Server</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사</a><br> 2. <a href="#export-flat-file">Tooa 내보내기 플랫 파일</a><br> 3. <a href="#sql-migration">SQL Database 마이그레이션 마법사</a> <br> 4. <a href="#sql-backup">데이터베이스 백업 및 복원</a><br> |

이 문서는 SQL Server Management Studio 또는 Visual Studio 데이터베이스 탐색기에서 SQL 명령을 실행하는 것으로 가정합니다.

> [!TIP]
> 사용할 수 있습니다 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate 하 고 Azure에서 데이터 tooa SQL Server VM을 이동 합니다 하는 파이프라인을 예약 합니다. 자세한 내용은 [Azure 데이터 팩터리를 사용하여 데이터 복사(복사 작업)](../data-factory/data-factory-data-movement-activities.md)를 참조하세요.
>
>

## <a name="prereqs"></a>필수 조건
이 자습서에서는 사용자가 다음을 보유하고 있다고 가정합니다.

* **Azure 구독**. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.
* **Azure 저장소 계정**. 이 자습서에 hello 데이터를 저장 하기 위한 Azure 저장소 계정을 사용 합니다. Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서. Hello 저장소 계정을 만든 후 tooobtain hello 계정 키 tooaccess hello 저장소를 사용 해야 합니다. [저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)를 참조하세요.
* 프로비전된 **Azure VM의 SQL Server**. 자세한 내용은 [고급 분석을 위해 Azure SQL Server 가상 컴퓨터를 IPython Notebook 서버로 설정](machine-learning-data-science-setup-sql-server-virtual-machine.md)을 참조하세요.
* 로컬로 설치 및 구성된 **Azure PowerShell** . 자세한 내용은 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="filesource_to_sqlonazurevm"></a>Azure VM에서 플랫 파일 원본 tooSQL 서버에서에서 데이터를 이동
(행/열 형식으로 정렬) 플랫 파일에 데이터가 있으면 hello 다음 메서드를 통해 이동된 tooSQL Azure에서 서버 VM 수 있습니다.

1. [명령줄 BCP(대량 복사 유틸리티)](#insert-tables-bcp)
2. [대량 삽입 SQL 쿼리 ](#insert-tables-bulkquery)
3. [SQL Server의 기본 제공 그래픽 유틸리티(가져오기/내보내기, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>명령줄 BCP(대량 복사 유틸리티)
BCP는 SQL Server와 함께 설치 하는 명령줄 유틸리티 및 hello 가장 빠른 방법으로 toomove 데이터 중 하나입니다. 이는 모든 SQL Server 버전(온-프레미스 SQL Server, SQL Azure 및 Azure 기반의 SQL Server VM)에서 작동합니다.

> [!NOTE]
> **BCP를 사용하려면 데이터가 어디에 있어야 하나요?**  
> 에 있는 원본 데이터를 포함 하는 파일이 필요 하지 않은 동안 hello 더 빠르게 hello 대상 SQL Server와 동일한 컴퓨터에 대 한 허용 (네트워크 속도 및 로컬 디스크 IO 속도)을 전송 합니다. Hello 플랫 파일을 포함 하는 데이터 toohello 컴퓨터를 이동할 수 있습니다를 사용 하 여 SQL Server가 설치 된와 같은 도구 다양 한 파일을 복사 [AZCopy](../storage/common/storage-use-azcopy.md), [Azure 저장소 탐색기](http://storageexplorer.com/) 또는 원격을 통해 windows 복사/붙여넣기 데스크톱 (RDP) 프로토콜입니다.
>
>

1. Hello 데이터베이스와 hello 테이블 hello 대상 SQL Server 데이터베이스에 생성 되어 있음을 확인 합니다. 방법의 예로 toodo hello 사용 하 여 해당 `Create Database` 및 `Create Table` 명령:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Hello 서식 파일 hello hello hello 컴퓨터의 명령줄에서 다음 명령을 실행 하 여 hello 테이블에 대 한 hello 스키마를 설명 하는 bcp가 설치 되어 있는 생성 합니다.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. 다음과 같이 hello bcp 명령을 사용 하 여 hello 데이터베이스로 hello 데이터를 삽입 합니다. Hello SQL Server 컴퓨터에 설치 되어 동일한 이라고 가정할 hello 명령줄에서 작동 합니다.

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **BCP 삽입 최적화** hello 다음 문서를 참조 하십시오 ['대량 가져오기 최적화에 대 한 지침이'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize 이러한 삽입 합니다.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>더 빠른 데이터 이동을 위한 병렬 처리
Hello 데이터를 이동 하는 큰 경우 하면 작업 속도를 높일 수 동시에 PowerShell 스크립트에서 동시에 여러 BCP 명령을 실행 하 여 합니다.

> [!NOTE]
> **빅 데이터 수집** toooptimize 데이터 로드 크고 매우 큰 데이터 집합에 대 한 여러 파일 그룹 및 파티션 테이블을 사용 하 여 논리적 및 물리적 데이터베이스 테이블을 분할 합니다. 만들기 및 데이터 toopartition 테이블에 로드 하는 방법에 대 한 자세한 내용은 참조 [부하 SQL 파티션 테이블 병렬](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)합니다.
>
>

hello 아래 샘플 PowerShell 스크립트 보여 bcp를 사용 하 여 병렬 삽입:

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>대량 삽입 SQL 쿼리
[대량 삽입 SQL 쿼리](https://msdn.microsoft.com/library/ms188365) 행/열 기반 파일에서 hello 데이터베이스에 사용 되는 tooimport 데이터가 될 수 있습니다 (지원 hello 형식을 다룹니다는[대량 내보내기 또는 가져오기 (SQL Server)에 대 한 데이터 준비](https://msdn.microsoft.com/library/ms188609)) 항목입니다.

아래는 대량 삽입을 위한 몇 가지 샘플 명령입니다.  

1. 데이터를 분석 하 고 해당 hello SQL Server 데이터베이스에 동일한 날짜와 같은 특수 한 모든 필드에 대 한 형식 hello 가정 하는지 toomake 가져오기 전에 모든 사용자 지정 옵션을 설정 합니다. Tooset hello 날짜에 서식을 지정 방법으로 연도-월-일 (hello 연도-월-일 형식의 날짜를 포함 하는 데이터) 하는 경우의 예는 다음과 같습니다.

        SET DATEFORMAT ymd;    
2. bulk import 문을 사용하여 데이터 가져오기

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>SQL Server의 기본 제공 그래픽 유틸리티
플랫 파일에서 Azure에서 SQL Server VM에 SQL Server Integrations Services (SSIS) tooimport 데이터를 사용할 수 있습니다.
SSIS는 두 가지 스튜디오 환경에서 사용할 수 있습니다. 자세한 내용은 [SSIS(Integration Services) 및 스튜디오 환경](https://technet.microsoft.com/library/ms140028.aspx)을 참조하세요.

* SQL Server 데이터 도구에 대한 자세한 내용은 [Microsoft SQL Server 데이터 도구](https://msdn.microsoft.com/data/tools.aspx)  
* Hello 가져오기/내보내기 마법사에 대 한 세부 정보를 참조 하십시오. [SQL Server 가져오기 및 내보내기 마법사](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Azure VM에서 온-프레미스 SQL Server tooSQL 서버에서에서 데이터를 이동
마이그레이션 전략을 따라 hello를 사용할 수 있습니다.

1. [배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [TooFlat 파일 내보내기](#export-flat-file)
3. [SQL 데이터베이스 마이그레이션 마법사](#sql-migration)
4. [데이터베이스 백업 및 복원](#sql-backup)

아래는 각 방법에 대한 설명입니다.

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사
hello **배포는 SQL Server 데이터베이스 tooa Microsoft Azure VM 마법사** 온-프레미스 SQL Server 인스턴스 tooSQL Azure VM에 서버에서에서 간단 하 고 권장 방법 toomove 데이터입니다. 자세한 단계와 같은 다른 방법에 대 한 내용은 참조 하세요. [데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션하려면](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)합니다.

### <a name="export-flat-file"></a>TooFlat 파일 내보내기
Hello에 설명 된 대로 다양 한 방법을 사용 하는 toobulk 온-프레미스 SQL Server의 데이터를 내보내는 될 수 있습니다 [대량 가져오기 및 데이터의 내보내기 (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) 항목입니다. 이 문서에서는 예를 들어 hello 프로그램 BCP (대량 복사)을 설명 합니다. 데이터를 플랫 파일로 내보낸 후 가져온된 tooanother SQL server 대량 가져오기 작업을 사용 하 여 가능 합니다.

1. 온-프레미스 SQL Server tooa 파일에서에서 hello 데이터 내보내기 hello bcp 유틸리티를 사용 하 여 다음과 같이

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Hello를 사용 하 여 Azure에서 SQL Server VM에서 hello 데이터베이스 및 hello 테이블을 만드는 `create database` 및 `create table` 1 단계에서 내보낸 hello 테이블 스키마에 대 한 합니다.
3. Hello 데이터를 내보내고 가져올 되 고 hello 테이블 스키마를 설명 하기 위해 서식 파일을 만듭니다. Hello 서식 파일의 세부 정보에 설명 되어 [서식 파일 (SQL Server)을 만들](https://msdn.microsoft.com/library/ms191516.aspx)합니다.

    때 SQL Server 컴퓨터 hello 실행 BCP에서 서식 파일 생성

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    SQL Server에 대해 원격으로 BCP를 실행하는 경우 서식 파일 생성

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. 섹션에 설명 된 hello 방법 중 하나를 사용 하 여 [파일 원본에서 데이터 이동](#filesource_to_sqlonazurevm) 플랫 파일 tooa SQL Server의에서 toomove hello 데이터입니다.

### <a name="sql-migration"></a>SQL 데이터베이스 마이그레이션 마법사
[SQL Server 데이터베이스 마이그레이션 마법사](http://sqlazuremw.codeplex.com/) 편리한 방법 toomove 두 SQL server 인스턴스 간에 데이터를 제공 합니다. 원본 및 대상 테이블 사이 hello 사용자 toomap hello 데이터 스키마를 통해, 열 유형 및 다른 다양 한 기능을 선택 합니다. BCP (대량 복사)를 사용 하 여 hello 내부적입니다. Hello의 스크린 샷 시작 화면에 대 한 hello SQL 데이터베이스 마이그레이션 마법사는 다음과 같습니다.  

![SQL Server 마이그레이션 마법사][2]

### <a name="sql-backup"></a>데이터베이스 백업 및 복원
SQL Server는 다음을 지원합니다.

1. [데이터베이스 백업 및 복원 기능](https://msdn.microsoft.com/library/ms187048.aspx) (모두 tooa 로컬 파일 또는 bacpac 내보내기 tooblob) 및 [데이터 계층 응용 프로그램](https://msdn.microsoft.com/library/ee210546.aspx) (bacpac를 사용 하 여).
2. 기능 toodirectly 복사 된 데이터베이스 또는 복사 tooan 기존 SQL Azure 데이터베이스와 Azure에서 SQL Server Vm을 만듭니다. 자세한 내용은 참조 하십시오. [데이터베이스 복사 마법사 사용 하 여 hello](https://msdn.microsoft.com/library/ms188664.aspx)합니다.

데이터베이스 백업 hello 스크린 샷 위쪽/복원 옵션에서 SQL Server Management Studio는 다음과 같습니다.

![SQL Server 가져오기 도구][1]

## <a name="resources"></a>리소스
[데이터베이스 tooSQL Azure VM에서 서버 마이그레이션](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Azure Virtual Machines의 SQL Server 개요](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
