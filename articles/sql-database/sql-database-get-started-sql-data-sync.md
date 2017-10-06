---
title: "Azure SQL 데이터 동기화 (미리 보기) aaaGetting 시작 | Microsoft Docs"
description: "이 자습서는 Azure SQL 데이터 동기화(미리 보기)를 시작하도록 도와줍니다."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Azure SQL 데이터 동기화 시작(미리 보기)
이 자습서에서는 하이브리드 동기화 그룹을 만들어 Azure SQL 데이터 동기화를 tooset Azure SQL 데이터베이스와 SQL Server 인스턴스를 포함 하는 방법을 배웁니다. hello 새 동기화 그룹 구성 완벽 하 게 되 고 설정한 hello 일정에 따라 동기화 됩니다.

이 자습서에서는 사용자가 SQL Database 및 SQL Server를 사용해본 경험이 있다고 가정합니다. 

SQL 데이터 동기화의 개요는 [데이터 동기화](sql-database-sync-data.md)를 참조하세요.

전체 PowerShell 보여 주는 예제 tooconfigure SQL 데이터 동기화 hello 다음 문서를 참조 하는 방법:
-   [여러 Azure SQL 데이터베이스 간에 toosync PowerShell을 사용 하 여](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Azure SQL 데이터베이스와 SQL Server 온-프레미스 데이터베이스 간의 toosync PowerShell을 사용 하 여](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> hello 전체 기술 설명서 MSDN에 있는 이전 Azure SQL 데이터 동기화에 대 한 집합은 사용할 수는 있습니다. PDF 문서입니다. [여기](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)에서 다운로드하세요.

## <a name="step-1---create-sync-group"></a>1단계 - 동기화 그룹 만들기

### <a name="locate-hello-data-sync-settings"></a>Hello 데이터 동기화를 찾아보려면

1.  브라우저에서 toohello Azure 포털을 탐색 합니다.

2.  Hello 포털에서 SQL 데이터베이스를 대시보드 또는 hello SQL 데이터베이스 아이콘에서 hello 도구 모음에서 찾습니다.

    ![Azure SQL Database 목록](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  Hello에 **SQL 데이터베이스** 블레이드, 선택 hello 기존 SQL 데이터베이스는 원하는 toouse hello 허브 데이터베이스 데이터 동기화. hello SQL 데이터베이스 블레이드를 엽니다.

4.  Hello 선택한 데이터베이스에 대 한 SQL 데이터베이스 블레이드에서 hello 선택 **tooother 데이터베이스를 동기화**합니다. hello 데이터 동기화 블레이드를 엽니다.

    ![Sync tooother 데이터베이스 옵션](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>새 동기화 그룹 만들기

1.  Hello 데이터 동기화 블레이드에서 선택 **새 동기화 그룹**합니다. hello **새 동기화 그룹** 단계 1, 블레이드에서 열립니다 **동기화 그룹 만들기**, 강조 표시 합니다. hello **데이터 동기화 그룹 만들기** 블레이드를 엽니다.

2.  Hello에 **데이터 동기화 그룹 만들기** 블레이드에서 작업 다음 hello지 않습니다:

    1.  Hello에 **동기화 그룹 이름은** 필드 hello 새 동기화 그룹에 대 한 이름을 입력 합니다.

    2.  Hello에 **동기화 메타 데이터 데이터베이스** 섹션에서 toocreate (권장) 새 데이터베이스 또는 toouse 기존의 데이터베이스 여부를 선택 합니다.

        > [!NOTE]
        > 동기화 메타 데이터 데이터베이스 hello으로 빈 새 데이터베이스 toouse를 만들어야 하는 것이 좋습니다. 데이터 동기화는 이 데이터베이스에서 테이블을 만들고 자주 실행되는 워크로드를 실행합니다. 이 데이터베이스는 자동으로 모든 hello 선택한 지역에서 동기화 그룹에 대 한 동기화 메타 데이터 데이터베이스 hello로 공유 됩니다. Hello 동기화 메타 데이터 데이터베이스, 해당 이름 또는 서비스 수준이 놓지 않고 변경할 수 없습니다.

        **새 데이터베이스**를 선택한 경우 **새 데이터베이스 만들기**를 선택합니다. hello **SQL 데이터베이스** 블레이드를 엽니다. Hello에 **SQL 데이터베이스** 블레이드에서 이름을 지정 하 고 hello 새 데이터베이스를 구성 합니다. 그런 다음 **확인**을 선택합니다.

        선택한 경우 **기존 데이터베이스를 사용 하 여**선택, hello 목록에서 hello 데이터베이스.

    3.  Hello에 **자동 동기화** 섹션을 먼저 선택 **에** 또는 **오프**합니다.

        선택한 경우 **에**, hello에 **동기화 빈도** 섹션 번호를 입력 하 고 초, 분, 시간 또는 일을 선택 합니다.

        ![동기화 빈도 지정](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  Hello에 **충돌 해결** 섹션에서 "허브 wins" 또는 "멤버 wins."를 선택 합니다.

        ![충돌 해결 방법 지정](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  선택 **확인** hello 새 동기화 그룹 toobe 만들고 배포 될 때까지 기다립니다.

## <a name="step-2---add-sync-members"></a>2단계 - 동기화 구성원 추가

Hello 새 동기화 그룹을 만들고 배포 하 고, 2 단계 후 **동기화 멤버 추가**, hello에서 강조 표시 됩니다 **새 동기화 그룹** 블레이드입니다.

Hello에 **허브 데이터베이스** 섹션에서 어떤 hello 허브 데이터베이스가 hello SQL 데이터베이스 서버에 대 한 hello 기존 자격 증명을 입력 합니다. 이 섹션에서 *새* 자격 증명을 입력하지 않습니다.

![허브 데이터베이스가 toosync 그룹 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Azure SQL Database 추가

Hello에 **멤버 데이터베이스** 섹션에서 필요에 따라 선택 하 여 Azure SQL 데이터베이스 toohello 동기화 그룹을 추가할 **Azure 데이터베이스를 추가할**합니다. hello **Azure 데이터베이스를 구성** 블레이드를 엽니다.

Hello에 **Azure 데이터베이스를 구성** 블레이드에서 작업 다음 hello지 않습니다:

1.  Hello에 **동기화 멤버 이름** 필드 hello 새 동기화 멤버에 대 한 이름을 입력 합니다. 이 이름은 hello 데이터베이스 자체의 hello 이름과 구별 됩니다.

2.  Hello에 **구독** 필드를 선택 하는 hello 청구 용 Azure 구독에 연결 합니다.

3.  Hello에 **Azure SQL Server** 기존 SQL 데이터베이스 서버 hello 필드를 선택 합니다.

4.  Hello에 **Azure SQL 데이터베이스** 기존 SQL 데이터베이스 hello 필드를 선택 합니다.

5.  Hello에 **동기화 방향이** 필드에서는 양방향 동기화, 허브 toohello 선택 또는 hello 허브입니다.

    ![새 SQL Database 동기화 구성원 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  Hello에 **Username** 및 **암호** 필드는 hello 멤버 데이터베이스가 hello SQL 데이터베이스 서버에 대 한 hello 기존 자격 증명을 입력 합니다. 이 섹션에서 *새* 자격 증명을 입력하지 않습니다.

7.  선택 **확인** hello 새 동기화 멤버 toobe 만들고 배포 될 때까지 기다립니다.

    ![새 SQL Database 동기화 구성원 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>온-프레미스 SQL Server 데이터베이스 추가

Hello에 **멤버 데이터베이스** 섹션에서 필요에 따라 온-프레미스 SQL Server toohello 동기화 그룹을 선택 하 여 추가 **온-프레미스 데이터베이스를 추가할**합니다. hello **구성 온-프레미스** 블레이드를 엽니다.

Hello에 **구성 온-프레미스** 블레이드에서 작업 다음 hello지 않습니다:

1.  선택 **선택 hello 동기화 에이전트 게이트웨이**합니다. hello **동기화 에이전트 선택** 블레이드를 엽니다.

    ![Hello 동기화 에이전트 게이트웨이 선택](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  Hello에 **선택 hello 동기화 에이전트 게이트웨이** 블레이드에서 선택 여부를 toouse 기존 에이전트 하거나 새 에이전트를 만듭니다.

    선택한 경우 **기존 에이전트**, 선택 hello hello 목록에서 기존 에이전트입니다.

    선택한 경우 **새 에이전트를 만들고**, 작업이 다음 hello지 않습니다:

    1.  제공 하는 hello 링크 hello 클라이언트 동기화 에이전트 소프트웨어를 다운로드 하 고 hello SQL Server가 있는 hello 컴퓨터에 설치 합니다.
 
        > [!IMPORTANT]
        > Tooopen 아웃 바운드 TCP 포트 1433 hello 방화벽 toolet hello 클라이언트 에이전트의 hello 서버와 통신 해야 합니다.


    2.  Hello 에이전트에 대 한 이름을 입력 합니다.

    3.  **키 만들기 및 생성**을 선택합니다.

    4.  Hello 에이전트 키 toohello 클립보드에 복사 합니다.
        
        ![새 동기화 에이전트 만들기](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  선택 **확인** tooclose hello **동기화 에이전트 선택** 블레이드입니다.

    6.  SQL Server 컴퓨터-hello에서 찾아 hello 클라이언트 동기화 에이전트 응용 프로그램을 실행 합니다.

        ![hello 데이터 동기화 클라이언트 에이전트 응용 프로그램](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  Hello 동기화 에이전트 app **에이전트 키 전송**합니다. hello **동기화 메타 데이터 데이터베이스 구성** 대화 상자가 열립니다.

    8.  Hello에 **동기화 메타 데이터 데이터베이스 구성** 대화 상자, 붙여넣기에 hello 에이전트 키 hello Azure 포털에서에서 복사 합니다. 또한 hello는 hello 메타 데이터 데이터베이스가 hello Azure SQL 데이터베이스 서버에 대 한 기존 자격 증명을 제공 합니다. (새 메타 데이터 데이터베이스를 만든 경우이 데이터베이스는 hello hello 허브 데이터베이스와 같은 서버입니다.) 선택 **확인** hello 구성 toofinish 될 때까지 기다립니다.

        ![Hello 에이전트 키 및 서버 자격 증명을 입력 합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   이 시점에서 방화벽 오류를 발생 하면 toocreate 방화벽 규칙이 있는 hello SQL Server 컴퓨터에서 Azure tooallow 트래픽을 합니다. Hello 포털에서 수동으로 hello 규칙을 만들 수 있지만 toocreate 더 쉽게 찾을 수 있습니다이 SQL Server Management Studio (SSMS). SSMS에서 Azure에서 tooconnect toohello 허브 데이터베이스를 시도 합니다. 데이터베이스 이름을 \<hub_database_name\>.database.windows.net으로 입력합니다. Hello 대화 상자 tooconfigure hello Azure 방화벽 규칙의 hello 단계를 수행 합니다. Toohello 클라이언트 동기화 에이전트 응용 프로그램을 반환 합니다.

    9.  Hello 클라이언트 동기화 에이전트 응용 프로그램에서 클릭 **등록** tooregister hello 에이전트와 SQL Server 데이터베이스입니다. hello **SQL Server 구성** 대화 상자가 열립니다.

        ![SQL Server 데이터베이스를 추가하고 구성합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. Hello에 **SQL Server 구성** 대화 상자에서 선택 하는지 여부를 SQL Server 인증 또는 Windows 인증을 사용 하 여 tooconnect 합니다. SQL Server 인증을 선택한 경우 hello 기존 자격 증명을 입력 합니다. 원하는 toosync hello SQL Server 이름과 hello hello 데이터베이스 이름을 제공 합니다. 선택 **연결 테스트** tootest 설정 합니다. 그런 다음 **저장**을 선택합니다. hello 등록된 데이터베이스 hello 목록에 나타납니다.

        ![SQL Server 데이터베이스를 지금 등록합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. 이제 hello 클라이언트 동기화 에이전트 앱을 닫을 수 있습니다.

    12. Hello 포털 hello **구성 온-프레미스** 블레이드를 **선택 hello 데이터베이스입니다.** hello **데이터베이스 선택** 블레이드를 엽니다.

    13. Hello에 **데이터베이스 선택** 블레이드 hello **동기화 멤버 이름** 필드 hello 새 동기화 멤버에 대 한 이름을 입력 합니다. 이 이름은 hello 데이터베이스 자체의 hello 이름과 구별 됩니다. Hello 데이터베이스 hello 목록에서 선택 합니다. Hello에 **동기화 방향이** 필드에서는 양방향 동기화, 허브 toohello 선택 또는 hello 허브입니다.

        ![내부 데이터베이스에 대 한 hello를 선택 합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. 선택 **확인** tooclose hello **데이터베이스 선택** 블레이드입니다. 그런 다음 선택 **확인** tooclose hello **구성 온-프레미스** 블레이드에 대 한 대기 hello에 대 한 새 멤버 toobe을 만들고 배포한 동기화 합니다. 마지막으로, 클릭 **확인** tooclose hello **동기화 멤버 선택** 블레이드입니다.

        ![내부 데이터베이스에서 toosync 그룹 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL 데이터 동기화 및 hello 로컬 에이전트 사용자 이름이 toohello 역할 추가 `DataSync_Executor`합니다. 데이터 동기화는 hello SQL Server 인스턴스에서이 역할을 만듭니다.

## <a name="step-3---configure-sync-group"></a>3단계 - 동기화 그룹 구성

Hello 새 동기화 그룹 멤버가 생성 되어 배포 3 단계 후 **동기화 그룹 구성**, hello에서 강조 표시 됩니다 **새 동기화 그룹** 블레이드입니다.

1.  Hello에 **테이블** 블레이드에서 선택 데이터베이스 동기화의 hello 목록에서 멤버를 그룹화 한 다음 선택 **스키마 새로 고침**합니다.

2.  사용 가능한 테이블 hello 목록에서 원하는 toosync hello 테이블을 선택 합니다.

    ![테이블 선택 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Hello 테이블의 모든 열은 기본적으로 선택 됩니다. 않으려면 toosync 모든 hello 열, toosync 않도록 hello 열에 대 한 hello 확인란을 사용 하지 않도록 설정 합니다. Tooleave hello 기본 키 열을 선택 해야 합니다.

    ![필드 선택 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  마지막으로 **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계
축하합니다. SQL Database 인스턴스와 SQL Server 데이터베이스가 모두 포함된 동기화 그룹을 만들었습니다.

SQL Database 및 SQL 데이터 동기화에 대한 자세한 내용은 다음을 참조하세요.

-   [Hello 전체 SQL 데이터 동기화 기술 설명서를 다운로드 합니다.](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Hello SQL 데이터 동기화 REST API 설명서 다운로드](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [SQL 데이터베이스 개요](sql-database-technical-overview.md)
-   [데이터베이스 수명 주기 관리](https://msdn.microsoft.com/library/jj907294.aspx)
