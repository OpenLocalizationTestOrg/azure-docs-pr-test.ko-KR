---
title: "Azure SQL 데이터베이스 백업에서 단일 테이블 aaaRestore | Microsoft Docs"
description: "어떻게 toorestore 단일은 Azure SQL 데이터베이스 백업에서을 테이블에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>어떻게 toorestore 단일은 Azure SQL 데이터베이스 백업에서을 테이블합니다
실수로 SQL 데이터베이스의 일부 데이터를 수정 하는 상황이 발생할 수 있습니다 하 고 나면 toorecover hello 단일 영향을 받는 테이블 합니다. 이 문서에서 설명 하는 방법을 toorestore는 단일 테이블에 있는 데이터베이스 hello SQL 데이터베이스 중 하나를 [자동 백업](sql-database-automated-backups.md)합니다.

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>준비 단계: hello 테이블 이름을 바꾸고 hello 데이터베이스의 복사본을 복원
1. Hello tooreplace 복원 hello 복사본으로 지정 하 여 Azure SQL 데이터베이스에는 테이블을 식별 합니다. Microsoft SQL Management Studio toorename hello 테이블을 사용 합니다. 예를 들어 hello 테이블 이름 바꾸기 &lt;테이블 이름&gt;_old 합니다.
   
   > [!NOTE]
   > 차단 되 고 tooavoid 바꾸려는 hello 테이블에서 실행 중인 작업이 없을 있는지 확인 합니다. 문제가 발생하면 유지 관리 기간 동안 이 절차를 수행해야 합니다.
   >

2. 프로그램 데이터베이스 tooa 지정 시간 toorecover toousing hello 원하는의 백업을 복원 [지점 In_Time 복원](sql-database-recovery-using-backups.md#point-in-time-restore) 단계입니다.
   
   > [!NOTE]
   > hello DBName + 타임 스탬프 형식으로 복원 하는 hello 데이터베이스의 hello 이름은 됩니다. 예를 들어 **01 01T22 12Z Adventureworks2012_2016**합니다. 이 단계 hello 서버에서 기존 데이터베이스 이름을 hello 덮어쓰기 안전 조치 이며 것은 tooallow tooverify hello 복원할 데이터베이스의 현재 데이터베이스를 삭제 한 프로덕션 용도로 hello 복원 된 데이터베이스의 이름을 바꾸거나 되기 전에 합니다.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Hello SQL 데이터베이스 마이그레이션 도구를 사용 하 여 데이터베이스를 복원 하는 hello에서 복사 hello 테이블

1. 다운로드 및 설치 hello [SQL 데이터베이스 마이그레이션 마법사](https://sqlazuremw.codeplex.com)합니다.
2. Hello의 SQL 데이터베이스 마이그레이션 마법사 열기 hello **프로세스 선택** 페이지에서 선택 **분석/마이그레이션 데이터베이스**, 클릭 하 고 **다음**합니다.

   ![SQL 데이터베이스 마이그레이션 마법사 - 프로세스 선택](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. Hello에 **tooServer 연결** 대화 상자에서 다음 설정을 hello 적용:

   * 서버 이름: **SQL server**
   * 응용 프로그램: **SQL Server Authentication**
   * 로그인: **로그인**
   * 암호: **암호**
   * 데이터베이스: **Master DB (모든 데이터베이스 나열)**
   
   > [!NOTE]
   > 기본적으로 hello 마법사는 로그인 정보를 저장합니다. 저장하지 않으려면 **로그인 정보 삭제**를 선택합니다.
   >
   
     ![SQL 데이터베이스 마이그레이션 마법사 - 원본 선택 - 1단계](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. Hello에 **원본 선택** 대화 상자, hello에서 데이터베이스 이름 선택 hello 복원 **준비 단계** 를 소스로 섹션 및 다음 클릭 **다음**합니다.
   
    ![SQL 데이터베이스 마이그레이션 마법사 - 원본 선택 - 2단계](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. Hello에 **개체 선택** 대화 상자, 선택 hello **특정 데이터베이스 개체 선택** 옵션을 선택한 다음 hello table(or tables) 원하는 toomigrate toohello 대상 서버를 선택 합니다.
   ![SQL 데이터베이스 마이그레이션 마법사 - 개체 선택](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. Hello에 **스크립트 마법사 요약** 페이지 **예** 용인지 준비 toogenerate SQL 스크립트에 대 한 프롬프트 메시지가 나타날 때. Hello 옵션 toosave hello TSQL 스크립트 나중에 사용할 수 있습니다.
   ![SQL 데이터베이스 마이그레이션 마법사 - 스크립트 마법사 요약](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. Hello에 **결과 요약** 페이지 **다음**합니다.
   ![SQL 데이터베이스 마이그레이션 마법사 - 결과 요약](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. Hello에 **대상 서버 연결 설정** 페이지에서 클릭 **tooServer 연결**, hello 세부 정보를 다음과 같이 입력 합니다.
   
   * **서버 이름**: 대상 서버 인스턴스
   * **인증**: **SQL Server 인증** 로그인 자격 증명을 입력합니다.
   * **데이터베이스**: **마스터 DB(모든 데이터베이스를 나열)**. 이 옵션은 hello 대상 서버에서 모든 hello 데이터베이스를 나열합니다.
     
     ![SQL 데이터베이스 마이그레이션 마법사 - 대상 서버 연결 설정](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. 클릭 **연결**선택, toomove hello 테이블을 클릭 한 다음 hello 대상 데이터베이스 **다음**합니다. Hello 이전에 생성 된 스크립트를 실행을 완료 해야이 하 고 hello 복사한 toohello 대상 데이터베이스 테이블을 새로 이동 표시 됩니다.

## <a name="verification-step"></a>확인 단계

- 쿼리하고 새로 복사 hello 테이블 toomake hello 데이터가 그대로 유지 되는지 테스트 합니다. 이름을 바꿀 hello 테이블 형식에 따라 삭제할 수 있습니다 **준비 단계** 섹션. (예를 들어 &lt;테이블 이름&gt;_old).

## <a name="next-steps"></a>다음 단계
[SQL 데이터베이스 자동 백업](sql-database-automated-backups.md)

