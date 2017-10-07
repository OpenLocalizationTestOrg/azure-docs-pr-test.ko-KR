---
title: "Azure Blob 저장소 tooSQL 데이터베이스-aaaCopy 데이터로 | Microsoft Docs"
description: "이 자습서에서는 Azure Data Factory에서 복사 작업 toouse toocopy 데이터베이스의에서 데이터를 Blob 저장소 tooSQL 파이프라인 하는 방법을 보여 줍니다."
keywords: "Blob SQL, Blob 저장소, 데이터 복사"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>자습서: Blob 저장소 tooSQL 데이터 팩터리를 사용 하 여 데이터베이스에서에서 데이터를 복사 합니다.
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

이 자습서에서는 Blob 저장소 tooSQL 데이터베이스에서 파이프라인 toocopy 데이터를 사용 하 여 데이터 팩터리를 만듭니다.

Azure Data Factory에 hello 데이터 이동을 수행 하는 hello 복사 작업 합니다. 다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다. 참조 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업에 대 한 세부 정보에 대 한 문서입니다.  

> [!NOTE]
> 데이터 팩터리 서비스 hello의 자세한 개요를 참조 hello [소개 tooAzure Data Factory](data-factory-introduction.md) 문서.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Hello 자습서에 대 한 필수 구성 요소
이 자습서를 시작 하기 전에 다음 필수 구성 요소는 hello가 있어야 합니다.

* **Azure 구독**.  구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. Hello 참조 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/) 을 참조 합니다.
* **Azure Storage 계정**. Hello blob 저장소로 사용 하는 **소스** 이 자습서에서는 데이터를 저장 합니다. Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계 toocreate 하나에 대 한 문서입니다.
* **Azure SQL 데이터베이스**. 이 자습서에서는 Azure SQL 데이터베이스를 **대상** 데이터 저장소로 사용합니다. 참조 hello 자습서에서 사용할 수 있는 Azure SQL 데이터베이스에 없는 경우 [어떻게 toocreate 및 Azure SQL 데이터베이스 구성](../sql-database/sql-database-get-started.md) toocreate 하나입니다.
* **SQL Server 2012/2014 또는 Visual Studio 2013**. Hello 데이터베이스의 SQL Server Management Studio 또는 Visual Studio toocreate 예제 데이터베이스와 tooview hello 결과 데이터를 사용합니다.  

## <a name="collect-blob-storage-account-name-and-key"></a>Blob 저장소 계정 이름 및 키 수집
Azure 저장소의 이름 및 계정 키 계정 toodo이이 자습서는 hello 계정이 필요 합니다. Azure Storage 계정의 **계정 이름**과 **계정 키**를 적어둡니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **더 많은 서비스** 왼쪽 메뉴 및 선택 hello에 **저장소 계정은**합니다.

    ![찾아보기 - 저장소 계정](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. Hello에 **저장소 계정은** 블레이드, 선택 hello **Azure 저장소 계정** 이 자습서에서는 toouse 되도록 합니다.
4. **설정** 아래에 있는 **액세스 키** 링크를 선택합니다.
5. 클릭 **복사** (이미지) 너무 단추 옆**저장소 계정 이름** 텍스트 상자 및 저장/붙여넣기 것 위치 (예: 텍스트 파일에).
6. 이전 단계 toocopy hello 또는 hello 기록해 반복 **key1**합니다.

    ![저장소 액세스 키](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. 클릭 하 여 모든 hello 블레이드를 닫고 **X**합니다.

## <a name="collect-sql-server-database-user-names"></a>SQL server, 데이터베이스, 사용자 이름 수집
이 자습서에서는 Azure SQL server, 데이터베이스 및 사용자 toodo의 hello 이름이 필요합니다. Azure SQL 데이터베이스의 **서버**, **데이터베이스** 및 **사용자**의 이름을 적어둡니다.

1. Hello에 **Azure 포털**, 클릭 **더 많은 서비스** 왼쪽과 선택 hello에 **SQL 데이터베이스**합니다.
2. Hello에 **SQL 데이터베이스 블레이드**선택, hello **데이터베이스** 이 자습서에서는 toouse 되도록 합니다. Hello 기록해 **데이터베이스 이름**합니다.  
3. Hello에 **SQL 데이터베이스** 블레이드에서 클릭 **속성** 아래 **설정을**합니다.
4. 에 대 한 hello 값 아래로 참고 **서버 이름** 및 **서버 관리자 로그인**합니다.
5. 클릭 하 여 모든 hello 블레이드를 닫고 **X**합니다.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Azure 서비스 tooaccess SQL server
되도록 **tooAzure 서비스 액세스를 허용** 설정이 **ON** 해당 hello 데이터 팩터리 서비스에서 Azure SQL server에 액세스할 수 있도록 Azure SQL server에 대 한 합니다. 다음 단계 tooverify 및이 설정 설정 hello지 않습니다.

1. 클릭 **더 많은 서비스** hello 왼쪽에 클릭 허브 **SQL server**합니다.
2. 서버를 선택하고 **설정** 아래의 **방화벽**을 클릭합니다.
3. Hello에 **방화벽 설정** 블레이드에서 클릭 **ON** 에 대 한 **tooAzure 서비스 액세스를 허용**합니다.
4. 클릭 하 여 모든 hello 블레이드를 닫고 **X**합니다.

## <a name="prepare-blob-storage-and-sql-database"></a>Blob 저장소 및 SQL 데이터베이스 준비
이제 Azure blob 저장소 및 Azure SQL 데이터베이스 hello 자습서 수행 하 여 준비 단계를 수행 하는 hello:  

1. 메모장을 시작합니다. Hello 텍스트 다음 복사 하 고로 저장 **emp.txt** 너무**C:\ADFGetStarted** 하드 드라이브에 폴더입니다.

    ```
    John, Doe
    Jane, Doe
    ```
2. 와 같은 도구를 사용 하 여 [Azure 저장소 탐색기](http://storageexplorer.com/) toocreate hello **adftutorial** 컨테이너 및 tooupload hello **emp.txt** 파일 toohello 컨테이너입니다.

    ![Azure 저장소 탐색기. Blob 저장소 tooSQL 데이터베이스에서 데이터 복사](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. 다음 SQL 스크립트 toocreate hello 사용 하 여 hello **emp** Azure SQL 데이터베이스의 테이블에에서 있습니다.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **SQL Server 2012/2014이 컴퓨터에 설치 되어 있으면:** 지침을 따릅니다 [Azure SQL 데이터베이스 관리 SQL Server Management Studio를 사용 하 여](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server 및 실행 hello SQL 스크립트. 이 문서에서는 hello [Azure 클래식 포털](http://manage.windowsazure.com), 하지 hello [새 Azure 포털](https://portal.azure.com), Azure SQL server에 대 한 방화벽 tooconfigure 합니다.

    클라이언트 tooaccess hello Azure SQL server에 허용 되지 않습니다 해야 tooconfigure 방화벽 프로그램 Azure SQL server tooallow 액세스에 대 한 컴퓨터 (IP 주소)에서. 참조 [이 여기서](../sql-database/sql-database-configure-firewall-settings.md) Azure SQL server에 대 한 단계 tooconfigure hello 방화벽에 대 한 합니다.

## <a name="create-a-data-factory"></a>데이터 팩터리를 만듭니다.
Hello 필수 구성 요소를 완료 했습니다. Hello 방법으로 다음 중 하나를 사용 하 여 데이터 팩터리를 만들 수 있습니다. Hello 맨 위 또는 링크 tooperform hello 자습서 hello에 hello 드롭 다운 목록에서 hello 옵션 중 하나를 클릭 합니다.     

* [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
* [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
* [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> 이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다. 입력된 데이터 tooproduce 출력 데이터를 변환 하지 않습니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: Hadoop 클러스터를 사용 하 여 첫 번째 파이프라인 tootransform 데이터 빌드](data-factory-build-your-first-pipeline.md)합니다.
> 
> Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요. 
