---
title: "Azure SQL 데이터베이스 aaaManage 그룹 | Microsoft Docs"
description: "탄력적 작업 만들기 및 관리 과정을 단계별로 안내합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>탄력적 작업을 사용하여 규모가 확장된 Azure SQL 데이터베이스 만들기 및 관리(미리 보기)


**탄력적 데이터베이스 작업** 은 스키마 변경, 자격 증명 관리, 참조 데이터 업데이트, 성능 데이터 수집 또는 테넌트(고객) 원격 분석 수집 등의 관리 작업을 실행하여 데이터베이스 그룹의 관리를 간소화합니다. 탄력적 데이터베이스 작업은 현재 Azure 포털 hello 및 PowerShell cmdlet을 통해 사용할 수 있습니다. 그러나이 기능을 제한 하는 Azure 포털 표면 hello tooexecution을 모든 데이터베이스에 걸쳐 제한는 [탄력적 풀 (미리 보기)](sql-database-elastic-pool.md)합니다. tooaccess 추가 기능 및 그룹 영역 또는 사용자 정의 컬렉션을 포함 하 여 데이터베이스에 대 한 스크립트의 실행 설정 (사용 하 여 만든 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-scale-introduction.md)), 참조 [만들기 및 관리 PowerShell을 사용 하 여 작업](sql-database-elastic-jobs-powershell.md)합니다. 작업에 대한 자세한 내용은 [탄력적 데이터베이스 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요. 

## <a name="prerequisites"></a>필수 조건
* Azure 구독. 무료 평가판에 대해서는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* 탄력적 풀. [탄력적 풀에 대한 정보](sql-database-elastic-pool.md)를 참조하세요.
* 탄력적 데이터베이스 작업 서비스 구성 요소의 설치 참조 [hello 탄력적 데이터베이스 작업 서비스를 설치](sql-database-elastic-jobs-service-installation.md)합니다.

## <a name="creating-jobs"></a>작업 만들기
1. Hello를 사용 하 여 [Azure 포털](https://portal.azure.com), 기존 탄력적 데이터베이스 작업 그룹에서 클릭 **만들기 작업**합니다.
2. Hello 작업 제어 데이터베이스 (작업에 대 한 메타 데이터 저장소)에 대 한 hello 사용자 이름 및 hello 데이터베이스 관리자 (만든 설치 작업 시)의 암호를 입력 합니다.
   
    ![Hello 작업 이름을 입력 하거나 코드를 붙여 넣습니다 하 고 실행][1]
3. Hello에 **작업 만들기** 블레이드에서 hello 작업에 대 한 이름 입력 합니다.
4. Hello 사용자 이름 및 암호 tooconnect toohello 대상 데이터베이스에 대 한 스크립트 실행 toosucceed 충분 한 권한이 있는 입력 합니다.
5. 붙여 넣거나 hello T-SQL 스크립트에 입력 합니다.
6. **저장**을 클릭한 다음 **실행**을 클릭합니다.
   
    ![작업 만들기 및 실행][5]

## <a name="run-idempotent-jobs"></a>멱등원 작업 실행
데이터베이스의 집합에 대해 스크립트를 실행 하는 경우에 hello 스크립트 idempotent 인지 확인 해야 합니다. 즉, hello 스크립트 수 toorun 여러 번 하더라도 해야 하기 전에 불완전 한 상태에 실패 했습니다. 예를 들어 스크립트에 실패 하면 hello 작업을 자동으로 재시도 성공할 때까지 (한계 내에서 hello 재시도로 논리 결국 중단 hello을 다시 시도). hello 방식으로 toodo toouse hello "IF EXISTS" 절 이며 새 개체를 만들기 전에 찾은 모든 인스턴스를 삭제 합니다. 아래에 예가 나와 있습니다.

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

또는 새 인스턴스를 만들기 전에 "IF NOT EXISTS" 절을 사용합니다.

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

이 스크립트는 다음 이전에 만든 hello 테이블을 업데이트 합니다.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>작업 상태 확인
작업이 시작된 후에 진행 상태를 확인할 수 있습니다.

1. Hello 탄력적 풀 페이지에서 클릭 **작업 관리**합니다.
   
    !["작업 관리"를 클릭합니다.][2]
2. Hello (a) 작업의 이름을 클릭 합니다. hello **상태** "Completed" 또는 "실패 했습니다." 일 수 있습니다 hello 작업 세부 정보 표시 날짜 및 시간 생성 및 실행 중 (b). 날짜 및 시간 정보를 제공 hello 풀의 각 데이터베이스에 대해 hello 스크립트의 hello 진행 상황을 보여 주는 hello 아래 hello 목록 (c).
   
    ![완료된 작업 확인][3]

## <a name="checking-failed-jobs"></a>실패한 작업 확인
작업이 실패할 경우 실행 로그가 생깁니다. Hello 실패 작업 toosee hello 이름을 세부 정보를 클릭 합니다.

![실패한 작업 확인][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


