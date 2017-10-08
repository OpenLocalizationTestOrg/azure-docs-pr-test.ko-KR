---
title: "SQL Server DB tooAzure aaaMigrate SQL 데이터베이스 | Microsoft Docs"
description: "Toomigrate SQL Server 데이터베이스 tooAzure SQL 데이터베이스에 알아봅니다."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션

SQL Server 이동 데이터베이스 tooAzure SQL 데이터베이스는 세 부분 프로세스-먼저 준비 다음 내보내기 및 다음 hello 데이터베이스를 가져옵니다. 이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]
> * 마이그레이션 tooAzure SQL 데이터베이스에 대 한 SQL Server에 데이터베이스를 준비 hello를 사용 하 여 [데이터 Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Hello 데이터베이스 tooa BACPAC 파일 내보내기
> * Azure SQL 데이터베이스로 hello BACPAC 파일 가져오기

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

- 최신 버전의 설치 된 hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). SSMS 설치 hello SQLPackage 사용 하는 데이터베이스 개발 태스크의 범위 tooautomate 일 수 있는 명령줄 유틸리티의 최신 버전도 설치 합니다. 
- 설치 된 hello [데이터 Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- 액세스 tooa 데이터베이스 toomigrate 있고 식별. 이 자습서에서는 hello [SQL Server 2008 r2 AdventureWorks OLTP 데이터베이스](https://msftdbprodsamples.codeplex.com/releases/view/59211) SQL Server 2008 r2 또는 최신, 인스턴스에 하지만 사용자가 선택한 모든 데이터베이스를 사용할 수 있습니다. toofix 호환성 문제를 사용 하 여 [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>마이그레이션 준비

마이그레이션에 대 한 준비 tooprepare 됩니다. 이러한 단계 toouse hello에 따라  **[데이터 Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello 마이그레이션 tooAzure SQL 데이터베이스에 대 한 데이터베이스의 준비 합니다.

1. 열기 hello **데이터 Migration Assistant**합니다. Toomigrate 계획, hello 호스트 컴퓨터에 SQL Server 인스턴스를 hello tooinstall 불필요 DMA 연결 toohello SQL Server 인스턴스에 포함 된 hello 데이터베이스와 모든 컴퓨터에서 실행할 수 있습니다.

     ![Data Migration Assistant 열기](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Hello 왼쪽 메뉴에서 클릭 **+ 새로 만들기** toocreate는 **평가** 프로젝트. Hello 형식으로 입력 한 **프로젝트 이름** (다른 모든 값의 기본값 유지 해야)를 클릭 하 고 **만들기**합니다. hello **옵션** 페이지가 열립니다.

     ![새 Data Migration Assistant 프로젝트](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Hello에 **옵션** 페이지 **다음**합니다. hello **원본을 선택** 페이지가 열립니다.

     ![새 데이터 마이그레이션 옵션](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Hello에 **원본을 선택** 페이지 toomigrate 계획 hello 서버를 포함 하는 SQL Server 인스턴스의 hello 이름을 입력 합니다. 필요한 경우이 페이지의 다른 값 hello 하는 변경 합니다. **Connect**를 클릭합니다.

     ![새 데이터 마이그레이션 소스 선택](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. Hello에 **원본을 추가** hello 부분의 **원본을 선택** 페이지 hello 데이터베이스 toobe 호환성에 대 한 테스트에 대 한 hello 확인란을 선택 합니다. **추가**를 클릭합니다.

     ![새 데이터 마이그레이션 소스 선택](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. **Start Assessment**(평가 시작)를 클릭합니다.

     ![새 데이터 마이그레이션 평가 시작](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Hello 평가 완료 되 면 먼저 찾습니다 toosee hello 데이터베이스가 충분히 호환 toomigrate 경우. 녹색 원에 hello 확인 표시를 찾습니다.

     ![새 데이터 마이그레이션 호환 평가 결과](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Hello 결과 검토 합니다. hello **대응 되는 SQL Server 기능** 표시 된 결과 hello 기본 결과 tooreview 합니다. 특히 부분적으로 지원 되 고 지원 되지 않는 기능에 대 한 hello 정보 및 권장된 조치에 대 한 정보를 제공 하는 hello 검토 합니다. 

     ![새 데이터 마이그레이션 평가 패리티](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. 검토 hello **호환성 문제** hello 홈페이지에서 해당 옵션을 클릭 하 여 합니다. 특히 검토 hello 마이그레이션 블로 커가, 동작 변경 내용에 대 한 정보 및 각 호환성 수준에 대 한 기능을 사용 되지 않습니다. Hello AdventureWorks2008R2 데이터베이스에 대 한 hello 변경 내용을 검토 tooFull 텍스트 검색 SQL Server 2008 및 hello 이후 SQL Server 2000 이후로 tooSERVERPROPERTY('LCID')를 변경 합니다. 이러한 변경 사항의 자세한 내용에 대한 링크가 제공됩니다. 변경된 다양한 검색 옵션 및 전체 텍스트 검색에 대한 설정 

   > [!IMPORTANT] 
   > 프로그램 데이터베이스 tooAzure SQL 데이터베이스를 마이그레이션한 후 toooperate hello 데이터베이스의 현재 호환성 수준 (수준 100 hello AdventureWorks2008R2 데이터베이스에 대 한) 또는 더 높은 수준에서 데이터베이스를 선택할 수 있습니다. Hello 의미 및 특정 호환성 수준에서 데이터베이스를 운영 하기 위한 옵션에 대 한 자세한 내용은 참조 하십시오. [ALTER DATABASE 호환성 수준](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)합니다. 참고 항목 [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) 추가 데이터베이스 수준 설정에 대 한 정보에 대 한 관련 toocompatibility 수준입니다.
   >

10. 필요에 따라 **보고서 내보내기** toosave hello 보고서를 JSON 파일로 합니다.
11. 데이터 마이그레이션 길잡이 닫기 번호입니다.

## <a name="export-toobacpac-file"></a>내보내기 tooBACPAC 파일 

BACPAC 파일이 hello 메타 데이터 및 SQL Server 데이터베이스에서 데이터가 포함 된 BACPAC의 확장명을 가진 ZIP 파일입니다. BACPAC 파일을 저장할 수 있습니다 또는 마이그레이션-보관 하기 위한 로컬 저장소 또는 Azure blob 저장소에과 같은 SQL Server tooAzure SQL 데이터베이스에서. 트랜잭션 측면에서 일치 하는 내보내기 toobe에 대 한 확인 해야 하거나 없는 쓰기 작업이 hello 내보내기 작업 중에 발생 합니다.

이러한 단계 toouse hello SQLPackage 명령줄 유틸리티 tooexport hello AdventureWorks2008R2 데이터베이스 toolocal 저장소를 따릅니다.

1. Windows 명령 프롬프트를 열고 hello 해야 디렉터리 tooa 폴더를 변경 **130** SQLPackage의-같은 버전 **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**합니다.

2. 다음 명령 프롬프트 tooexport hello hello에서 SQLPackage 명령을 hello 실행 **AdventureWorks2008R2** 에서 데이터베이스를 **localhost** 너무**AdventureWorks2008R2.bacpac**. 적절 한 tooyour 환경으로 다음이 값 중 하나를 변경 합니다.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage 내보내기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Hello 실행이 완료 되 면 hello 생성 된 BACPAC 파일 실행 hello sqlpackage가 있는 hello 디렉터리에 저장 됩니다. 이 예제에서는 C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin에 저장됩니다. 

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인

Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다. Hello SQLPackage 명령줄 유틸리티를 실행 하 고 있는 hello 컴퓨터에서 로그온 hello 생성 hello 방화벽 규칙의 5 단계에서 줄일 수 있습니다.

## <a name="create-a-sql-server-logical-server"></a>SQL Server 논리 서버 만들기

[SQL Server 논리 서버](sql-database-features.md)는 여러 데이터베이스에 대한 중앙 관리 지점의 역할을 합니다. 이러한 단계에 따라 SQL server 논리 서버 toocontain hello toocreate Adventure Works OLTP SQL Server 데이터베이스 마이그레이션. 

1. Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2. 형식 **sql server** hello hello 검색 창에서 **새로 만들기** 선택한 페이지 **SQL 데이터베이스 (논리 서버)** hello에서 필터링 된 목록입니다.

    ![논리 서버 선택](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Hello에 **모든** 페이지 **SQL server (논리 서버)** 클릭 하 고 **만들기** hello에 **SQL Server (논리 서버)** 페이지 .

    ![논리 서버 만들기](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Hello 이미지 앞에 표시 된 대로 hello SQL server (논리 서버) 양식을 사용 hello 다음 정보를 입력 합니다.     

   | 설정       | 제안 값 | 설명 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 전역적으로 고유한 이름 입력 | 유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요. | 
   | **서버 관리자 로그인** | 유효한 이름 입력 | 유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요. |
   | **암호** | 유효한 암호 입력 | 암호가 8 자 이상 있어야 하며 hello 다음 범주 중 세 범주의 문자를 포함 해야 합니다: 대문자, 소문자, 숫자 및 영숫자가 아닌 문자. |
   | **구독** | 구독 선택 | 구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요. |
   | **리소스 그룹** | 기존 리소스 그룹을 선택하거나 새 그룹을 만듭니다(예: **myResourceGroup**). |  유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요. |
   | **위치**: | 새 서버 hello에 대 한 올바른 위치를 입력 합니다. | 지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요. |

   ![논리 서버 만들기 양식 완료](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. 클릭 **만들기** tooprovision hello 논리 서버입니다. 프로비전하는 데 몇 분이 걸립니다. 

> [!IMPORTANT]
> 서버 이름, 서버 관리자 로그인 이름 및 암호를 기억하세요. 이 자습서의 뒷부분에서 이러한 값이 필요합니다.
>

## <a name="create-a-server-level-firewall-rule"></a>서버 수준 방화벽 규칙 만들기

SQL 데이터베이스 서비스 hello 만듭니다는 [hello 서버 수준 방화벽](sql-database-firewall-configure.md) 외부 응용 프로그램 및 도구는 방화벽 규칙 tooopen hello를 만들지 않으면 toohello 서버나 hello 서버에 있는 모든 데이터베이스를 연결 하지 못하도록 방지 하 특정 IP 주소에 대 한 방화벽입니다. 이러한 단계 toocreate hello SQLPackage 명령줄 유틸리티를 실행 하 고 있는 hello 컴퓨터의 hello IP 주소에 대 한 SQL 데이터베이스 서버 수준 방화벽 규칙을 따릅니다. 이 통해 SQLPackage tooconnect toohello SQL serverDatabase 논리 서버 hello Azure SQL 데이터베이스 방화벽을 통해. 

1. 클릭 **모든 리소스** hello 왼쪽 메뉴에서 새 서버 hello에 클릭 **모든 리소스** 페이지. 서버에 대 한 개요 페이지 hello 열리고 더 이상의 구성에 대 한 옵션을 제공 합니다.

     ![논리 서버 개요](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. 클릭 **방화벽** hello 왼쪽 메뉴 아래에서 **설정을** hello 개요 페이지에 있습니다. hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다. 

3. 클릭 **클라이언트 IP 추가** hello 컴퓨터의 hello 도구 모음 tooadd hello IP 주소에 현재 사용 하 고이 클릭 한 다음 **저장**합니다. 이 IP 주소에 대한 서버 수준 방화벽 규칙이 생성됩니다.

     ![set server firewall rule](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. **확인**을 클릭합니다.

이제 tooall 데이터베이스 SQL Server Management Studio 또는 이전에 만든 hello 서버 관리자 계정을 사용 하 여이 IP 주소에서 선택한 다른 도구를 사용 하 여이 서버에 연결할 수 있습니다.

> [!NOTE]
> SQL Database는 포트 1433을 통해 통신합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우에 IT 부서는 포트 1433을 엽니다 하지 않는 한 tooyour Azure SQL 데이터베이스 서버를 연결할 수 없습니다.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>BACPAC 파일 tooAzure SQL 데이터베이스 가져오기 

hello 한 최신 버전의 hello SQLPackage 명령줄 유틸리티에 지정 된 Azure SQL 데이터베이스를 만들기 위한 지원을 제공 [서비스 계층과 성능 수준](sql-database-service-tiers.md)합니다. 가져오기 중 최상의 성능을 위해 높은 서비스 계층과 성능 수준을 선택 하 고 hello 서비스 계층과 성능 수준을 즉시 필요한 것 보다 높은 경우 가져온 후 다음 확장 합니다.

이 단계 사용 하 여 hello SQLPackage 명령줄 유틸리티 tooimport hello AdventureWorks2008R2 데이터베이스 tooAzure SQL 데이터베이스를 따릅니다. 이 작업에 대 한 SQL Server Management Studio를 사용할 수 있지만 SQLPackage는 최대한의 유연성 및 최상의 성능을 위해 대부분의 프로덕션 환경에 대 한 hello 기본 방법입니다. 참조 [SQL Server tooAzure BACPAC 파일을 사용 하 여 SQL 데이터베이스에서에서 마이그레이션](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)합니다.

- 다음 명령 프롬프트 tooimport hello hello에서 SQLPackage 명령을 hello 실행 **AdventureWorks2008R2** 로컬 저장소 toohello SQL server 논리 서버에서 해당 하면 이전에 만든된 tooa 새 데이터베이스를 서비스 데이터베이스 계층 **프리미엄**, 및의 서비스 목표 **P6**합니다. 꺾쇠 괄호 hello 값을 SQL server 논리 서버에 대 한 적절 한 값으로 교체 하 고 hello 새 데이터베이스 (또한 replace hello 꺾쇠 괄호)에 대 한 이름을 지정 합니다. 또한 적절 한 tooyour 환경으로 데이터베이스 버전 및 서비스 objectgive toochange hello 값을 선택할 수 있습니다. 이 자습서의 hello 용도로 hello 마이그레이션된 데이터베이스 라고 **myMigratedDatabase**합니다.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage 가져오기](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> SQL Server 논리 서버는 포트 1433을 수신합니다. Tooconnect tooa SQL server 논리 서버에서 회사 방화벽 내에서 시도 하는 경우 있습니다 toosuccessfully 연결을 위해이 포트 hello 회사 방화벽에서 열려 있는 여야 합니다.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 연결

SQL Server Management Studio tooestablish 연결 tooyour Azure SQL 데이터베이스 서버 및 라는 새로 마이그레이션된 데이터베이스를 사용 하 여 **myMigratedDatabase** 이 자습서에서는 합니다. SQLPackage를 실행 하는 다른 컴퓨터에 SQL Server Management Studio를 실행 하는 경우 hello 단계를 사용 하 여 hello 이전 절차에서이 컴퓨터에 대 한 방화벽 규칙을 만듭니다.

1. SQL Server Management Studio를 엽니다.

2. Hello에 **tooServer 연결** 대화 상자에 hello 다음 정보를 입력 합니다.
   - **서버 유형**: 데이터베이스 엔진을 지정합니다.
   - **서버 이름**: **mynewserver20170403.database.windows.net**과 같은 정규화된 서버 이름을 입력합니다.
   - **인증**: SQL Server 인증을 지정합니다.
   - **로그인**: 서버 관리자 계정을 입력합니다.
   - **암호**: 서버 관리자 계정에 대 한 hello 암호를 입력 합니다.
 
    ![ssms로 연결](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. **Connect**를 클릭합니다. hello 개체 탐색기 창이 열립니다. 

4. 개체 탐색기에서 확장 **데이터베이스** 펼친 다음 **myMigratedDatabase** hello 샘플 데이터베이스의 tooview hello 개체입니다.

## <a name="change-database-properties"></a>데이터베이스 속성 변경

Hello 서비스 계층, 성능 수준 및 SQL Server Management Studio를 사용 하 여 호환성 수준을 변경할 수 있습니다. Hello 가져오기 단계 중 최상의 성능을 위해 tooa 더 높은 성능 계층 데이터베이스를 가져올 하지만 hello 가져오기 가져온된 데이터베이스를 hello 준비 tooactively 사용 될 때까지 toosave money 완료 된 후 확장 하는 것이 좋습니다. Hello 호환성 수준을 변경 더 나은 성능과 액세스 toohello hello Azure SQL 데이터베이스 서비스의 최신 기능을 얻을 수도 있습니다. 이전 데이터베이스를 마이그레이션하는 경우 가져올 hello 데이터베이스와 호환 되는 지원 hello 가장 낮은 수준에서의 데이터베이스 호환성 수준이 유지 됩니다. 자세한 내용은 [Azure SQL Database의 호환성 수준 130을 통해 개선된 쿼리 성능](sql-database-compatibility-level-query-performance-130.md)을 참조하세요.

1. 개체 탐색기에서 **myMigratedDatabase**를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다. 쿼리 창에 연결 된 tooyour 데이터베이스를 열립니다.

2. 너무 명령 tooset hello 서비스 계층을 따라 hello 실행**표준** 성능 수준에 너무 hello 및**S1**합니다.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![서비스 계층 변경](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. 실행 명령 toochange hello 데이터베이스 호환성 수준이 너무 다음 hello**130**합니다.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![호환성 수준 변경](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>다음 단계 
이 자습서에서는 데이터베이스를 준비하고 내보내며 가져왔습니다. 다음에 대해 알아보았습니다.

> [!div class="checklist"]
> * 마이그레이션 tooAzure SQL 데이터베이스에 대 한 SQL Server에 데이터베이스를 준비 합니다.
> * Hello 데이터베이스 tooa BACPAC 파일 내보내기
> * Azure SQL 데이터베이스로 hello BACPAC 파일 가져오기

다음 자습서 toolearn toohello 어떻게 발전 toosecure 데이터베이스입니다.

> [!div class="nextstepaction"]
> [Azure SQL Database 보안](sql-database-security-tutorial.md)


