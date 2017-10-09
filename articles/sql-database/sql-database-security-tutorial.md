---
title: "aaaSecure Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure SQL 데이터베이스를 기술 및 기능 toosecure에 알아봅니다."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Azure SQL Database 보안

SQL 데이터베이스에서 방화벽 규칙, id 및 권한 부여 toodata 역할 기반 구성원 자격 및 권한을 통해 통해서도 사용자 tooprove 하도록 하는 인증 메커니즘을 사용 하 여 액세스 tooyour 데이터베이스를 제한 하 여 데이터를 보호 행 수준 보안 및 동적 데이터 마스킹입니다.

악의적인 사용자 또는 몇 가지 간단한 단계만 무단된 액세스 로부터 사용자 데이터베이스의 hello 보호를 향상 시킬 수 있습니다. 이 자습서에서는 다음에 대해 알아봅니다. 

> [!div class="checklist"]
> * Hello Azure 포털에서에서 해당 서버에 대 한 서버 수준 방화벽 규칙 설정
> * SSMS를 사용하여 데이터베이스에 대해 데이터베이스 수준 방화벽 규칙 설정
> * Tooyour 데이터베이스 보안 연결 문자열을 사용 하 여 연결
> * 사용자 액세스 관리
> * 암호화로 데이터 보호
> * SQL Database 감사 사용
> * SQL Database 위협 감지 사용

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이 자습서, 확인을 준비 해야 다음 hello:

- 최신 버전의 설치 된 hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Microsoft Excel
- Azure SQL server 및 데이터베이스-만든 참조 [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](sql-database-get-started-portal.md), [hello Azure CLI를 사용 하 여 단일 Azure SQL 데이터베이스 만들기](sql-database-get-started-cli.md), 및 [단일 Azure Sql PowerShell을 사용 하 여 데이터베이스](sql-database-get-started-powershell.md)합니다. 

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인

Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Hello Azure 포털에에서 서버 수준 방화벽 규칙을 만들려면

Azure에서 SQL Database는 방화벽으로 보호됩니다. 기본적으로 모든 연결 toohello 서버와 hello 데이터베이스 hello 서버 내부에서 다른 Azure 서비스의 연결을 제외 하 고 거부 됩니다. 자세한 내용은 [Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성](sql-database-firewall-configure.md)을 참조하세요.

hello 가장 안전한 구성은 tooset 대 한 액세스 허용 tooAzure 서비스' tooOFF 합니다. Azure VM 또는 클라우드 서비스에서 tooconnect toohello 데이터베이스를 두어야 하는 경우 만든는 [예약 된 IP](../virtual-network/virtual-networks-reserved-public-ip.md) hello 예약 된 IP 주소 액세스만 허용 hello 방화벽을 통해 및 합니다. 

이러한 단계 toocreate에 따라 한 [SQL 데이터베이스 서버 수준 방화벽 규칙](sql-database-firewall-configure.md) 특정 IP 주소에서 서버 tooallow 연결용입니다. 

> [!NOTE]
> 이전 자습서 hello 또는 퀵 스타트 되며 중 하나를 사용 하 여 Azure에서 예제 데이터베이스를 만든 경우 hello가 있는 컴퓨터에서이 자습서를 수행 합니다. 동일한 IP 주소를 이러한 자습서를 통해 진행할 때 이전를 건너뛸 수 있습니다이 단계는 것 이미 서버 수준 방화벽 규칙을 만들었습니다.
>

1. 클릭 **SQL 데이터베이스** hello 왼쪽 메뉴 hello 데이터베이스에서 원하는 hello에서 tooconfigure hello 방화벽 규칙에 대 한 **SQL 데이터베이스** 페이지. hello 완벽 하 게 hello 보여 주는 데이터베이스 열리면 프로그램에 대 한 개요 페이지에 정규화 된 서버 이름 (같은 **mynewserver 20170313.database.windows.net**) 하 고 더 이상의 구성에 대 한 옵션을 제공 합니다.

      ![서버 방화벽 규칙](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. 클릭 **서버 방화벽 설정** hello 이전 그림에 나와 있는 것 처럼 hello 도구 모음입니다. hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다. 

3. 클릭 **클라이언트 IP 추가** 에 hello와 hello 컴퓨터 연결 된 toohello 포털의 도구 모음 tooadd hello 공용 IP 주소 또는 hello 방화벽 규칙을 수동으로 입력 한 다음 클릭 **저장**합니다.

      ![set server firewall rule](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. 클릭 **확인** hello를 클릭 한 다음 **X** tooclose hello **방화벽 설정** 페이지.

지정 된 hello로 tooany 데이터베이스 hello 서버에 연결할 수 있습니다 IP 주소 또는 IP 주소 범위입니다.

> [!NOTE]
> SQL Database는 포트 1433을 통해 통신합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우 됩니다 수 tooconnect tooyour Azure SQL 데이터베이스 서버 않으면 IT 부서는 포트 1433을 엽니다.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>SSMS를 사용하여 데이터베이스 수준 방화벽 규칙 만들기

데이터베이스 수준 방화벽 규칙을 사용 하는 휴대용-hello 중에 데이터베이스를 따른다는 동일한 논리 서버 및 toocreate 방화벽 규칙 hello 내에서 서로 다른 데이터베이스에 대 한 toocreate 다른 방화벽 설정을 하면는 [장애 조치 ](sql-database-geo-replication-overview.md) hello SQL server에 저장 되지 않고 있습니다. 데이터베이스 수준 방화벽 규칙 hello 첫 번째 서버 수준 방화벽 규칙을 구성 하면 TRANSACT-SQL 문을 사용 하 여 구성 되 고 유일한을 수만 있습니다. 자세한 내용은 [Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성](sql-database-firewall-configure.md)을 참조하세요.

이러한 단계 toocreate 데이터베이스 관련 방화벽 규칙을 따릅니다.

1. 예를 사용 하 여 tooyour 데이터베이스 연결 [SQL Server Management Studio](./sql-database-connect-query-ssms.md)합니다.

2. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 tooadd 방화벽에 대 한 규칙을 클릭 하 여 hello 데이터베이스 **새 쿼리**합니다. 빈 쿼리 창이 열립니다 tooyour 연결 된 데이터베이스입니다.

3. Hello 쿼리 창에서 hello IP 주소 tooyour 공용 IP 주소를 수정 하 고 hello 다음 쿼리를 실행 합니다.

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Hello 도구 모음에서 **Execute** toocreate hello 방화벽 규칙입니다.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>응용 프로그램 tooyour tooconnect 데이터베이스 보안 연결 문자열을 사용 하는 방법 보기

클라이언트 응용 프로그램과 SQL 데이터베이스 간에 암호화 된 보안 연결 tooensure hello 연결 문자열에 toobe 하도록 구성 합니다.

- 암호화된 연결을 요청하고
- toonot hello 서버 인증서를 신뢰 합니다. 

이 보안 TLS (전송 계층)를 사용 하 여 연결을 설정 하 고 hello의 중간자 개입 공격 위험 감소 합니다. 가져올 수 있습니다 올바르게 구성 된 연결 문자열 지원 되는 클라이언트에 대 한 SQL 데이터베이스에 대 한 드라이버 hello Azure 포털에서에서 ADO.net에 대 한이 스크린 샷에 표시 된 것 처럼.

1. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.

2. Hello에 **개요** 데이터베이스 페이지에서 클릭 **데이터베이스 연결 문자열 표시**합니다.

3. 전체 검토 hello **ADO.NET** 연결 문자열입니다.

    ![ADO.NET 연결 문자열](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>데이터베이스 사용자 만들기

사용자를 만들기 전에 먼저 Azure SQL Database가 지원하는 두 가지 인증 유형 중 하나를 선택해야 합니다. 

**SQL 인증**, 로그인에 대 한 사용자 이름 및 암호를 사용 하 및 유효한에 있는 사용자는 논리 서버 내에서 특정 데이터베이스의 컨텍스트에서 hello 합니다. 

**Azure Active Directory 인증**은 Azure Active Directory에서 관리되는 ID를 사용합니다. 

Toouse 하려는 경우 [Azure Active Directory](./sql-database-aad-authentication.md) SQL 데이터베이스에 대해 tooauthenticate, 지정된 된 Azure Active Directory를 계속 하려면 먼저 존재 해야 합니다.

이러한 단계 toocreate SQL 인증을 사용 하 여 사용자를 수행 합니다.

1. 예를 사용 하 여 tooyour 데이터베이스 연결 [SQL Server Management Studio](./sql-database-connect-query-ssms.md) 서버 관리자 자격 증명을 사용 하 여 합니다.

2. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 hello 데이터베이스에서 새 사용자 tooadd 원하는 하 고 클릭 **새 쿼리**합니다. 빈 쿼리 창이 열립니다 연결 된 toohello 선택한 데이터베이스입니다.

3. Hello 쿼리 창에서 다음 쿼리는 hello를 입력 합니다.

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Hello 도구 모음에서 **Execute** toocreate hello 사용자입니다.

5. 기본적으로 hello 사용자 toohello 데이터베이스를 연결할 수 있지만 사용 권한을 tooread 또는 쓰기 데이터가 없습니다. toogrant 이러한 사용 권한을 toohello 새로 만든 사용자, 새 쿼리 창에서 두 명령의 다음 hello를 실행 합니다.

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

것이 모범 사례 toocreate hello 데이터베이스 수준 tooconnect tooyour에서 이러한 관리자가 아닌 계정 데이터베이스 tooexecute 관리자 작업 같은 새 사용자를 만드는 경우를 제외 합니다. Hello를 검토 하십시오 [Azure Active Directory 자습서](./sql-database-aad-authentication-configure.md) 방법에 Azure Active Directory를 사용 하 여 tooauthenticate 합니다.


## <a name="protect-your-data-with-encryption"></a>암호화로 데이터 보호

Azure SQL 데이터베이스 투명 한 데이터 암호화 (TDE)는 자동으로 모든 변경 내용을 toohello 응용 프로그램에 액세스 hello 암호화 된 데이터베이스를 요구 하지 않고을 미사용 데이터를 암호화 합니다. 새로 만든 데이터베이스의 경우 TDE는 기본적으로 켜져 있습니다. TDE가 켜져 있는 tooverify 또는 데이터베이스에 대 한 TDE tooenable 다음이 단계를 따르십시오.

1. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지. 

2. 클릭 **투명 한 데이터 암호화** TDE에 대 한 tooopen hello 구성 페이지입니다.

    ![투명한 데이터 암호화](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. 필요한 경우 설정 **데이터 암호화** tooON 클릭 **저장**합니다.

hello 암호화 프로세스가 hello 백그라운드에서 시작 됩니다. 연결 tooSQL 데이터베이스를 사용 하 여 hello 진행률을 모니터링할 수 [SQL Server Management Studio](./sql-database-connect-query-ssms.md) hello의 hello encryption_state 열을 쿼리하여 `sys.dm_database_encryption_keys` 보기.

## <a name="enable-sql-database-auditing-if-necessary"></a>필요한 경우 SQL Database 감사를 사용합니다.

Azure SQL 데이터베이스 감사 데이터베이스 이벤트를 추적 하 고 Azure 저장소 계정에 tooan 감사 로그를 기록 합니다. 감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 잠재적인 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다. 이러한 단계 toocreate SQL 데이터베이스에 대 한 기본 감사 정책을 따르십시오.

1. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지. 

2. Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다. 서버 수준 감사 없게 임을 있고 있다는 **서버 설정을 보려면** 링크 tooview를 허용 하 고이 컨텍스트에서 hello 서버 감사 설정을 수정 합니다.

    ![감사 블레이드](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Tooenable는 감사 형식 (또는 위치?)를 선호 하는 경우 hello 서버 수준에서 지정 된 hello와에서 다른 설정 **ON** 감사 hello 선택 **Blob** 감사 유형이 있습니다. 서버 Blob 감사를 사용 하는 경우 hello 구성 된 데이터베이스 감사 hello 서버 Blob 감사와 함께 존재 합니다.

    ![감사 설정](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. 선택 **저장소 세부 정보** tooopen hello 감사 로그 저장소 블레이드입니다. 로그를 저장할 선택 hello Azure 저장소 계정 및 hello 보존 기간을 어떤 hello 이전 로그 삭제 후, 클릭 **확인** hello 맨 아래에 있습니다. 

   > [!TIP]
   > 사용 하 여 hello 동일 hello 감사를 최대한 활용 하는 모든 감사 데이터베이스 tooget hello에 대 한 저장소 계정을 서식 파일을 보고 합니다.
   > 

5. **Save**를 클릭합니다.

> [!IMPORTANT]
> Toocustomize hello 감사 이벤트를 하려는 경우 이렇게 하려면 PowerShell 또는 REST API 액세스를 통해 참조 hello [자동화 (PowerShell / REST API)](sql-database-auditing.md#subheading-7) 자세한 내용은 섹션.
>

## <a name="enable-sql-database-threat-detection"></a>SQL Database 위협 감지 사용

위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다. 사용자는 시도 tooaccess, 위반에서에서 발생 하거나 hello 데이터베이스의에서 데이터를 이용할 경우 toodetermine SQL 데이터베이스 감사를 사용 하 여 hello 의심 스러운 이벤트를 탐색할 수 있습니다. 위협 요소 탐지 하면 간단한 tooaddress 잠재적인 위협 toohello 데이터베이스 없이 hello 필요 toobe 보안 전문가 또는 시스템 모니터링 하는 고급 보안을 관리 합니다.
예를 들어 위협 감지는 잠재적인 SQL 삽입 시도를 나타내는 비정상적인 데이터베이스 활동을 감지합니다. SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다. 공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 졌는 지 또는 hello 데이터베이스의 데이터 수정에 대 한 응용 프로그램 입력 필드에 합니다.

1. Hello toomonitor 사용할 SQL 데이터베이스의 구성 블레이드에서 toohello 이동 합니다. Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다.

    ![탐색 창](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. Hello에 **감사 및 위협 요소 탐지** 구성 블레이드 turn **ON** 감사를 위해 표시 하는 hello 위협 검색 설정 합니다.

3. 위협 감지를 **켭니다**.

4. 검색 비정상 데이터베이스 작업에 대해 보안 경고를 받을 전자 메일의 hello 목록을 구성 합니다.

5. 클릭 **저장** hello에 **감사 및 위협 검색** 블레이드 toosave hello 신규 또는 업데이트 된 감사 및 위협 검색 정책입니다.

    ![탐색 창](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    비정상적인 데이터베이스 활동이 감지되면 이에 대한 이메일 알림을 받게 됩니다. hello 전자 메일 hello 비정상적인 활동, 데이터베이스 이름, 서버 이름 및 hello 이벤트 시간의 hello 특성을 포함 하 여 hello 의심 되는 보안 이벤트를 처리 정보를 제공 합니다. 또한, 가능한 원인에 정보를 제공 합니다 및 작업 tooinvestigate 권장 하 고 hello 잠재적인 위협 toohello 데이터베이스 완화 합니다. 이러한 메일 수신 하는 hello 어떤 toodo를 통해 수행 해야 하는 다음 단계 워크:

    ![위협 감지 전자 메일](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. Hello 전자 메일의 hello에서 클릭 **Azure SQL 감사 로그** 링크를 hello Azure 포털을 시작 하 고 hello 의심 스러운 이벤트의 hello 시간대 hello 관련 된 감사 레코드가 표시 됩니다.

    ![감사 레코드](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. SQL 문 처럼 hello 데이터베이스 의심 스러운 활동에 대 한 자세한 내용은 hello 감사 레코드 tooview 클릭 실패 이유 및 클라이언트 IP입니다.

    ![레코드 세부 정보](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. Hello 감사 레코드 블레이드에서 클릭 **Excel에서 열기** tooopen 미리 구성 된 excel 서식 파일 tooimport 및 hello 의심 스러운 이벤트의 hello 시간대 hello 감사 로그의 심층 분석을 실행된 합니다.

    > [!NOTE]
    > Excel 2010 또는 나중에 파워 쿼리 및 hello **빠른 결합** 설정은 필수입니다.

    ![Excel에서 레코드 열기](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. tooconfigure hello **빠른 결합** hello에 설정- **파워 쿼리** 리본 탭 **옵션** toodisplay hello 옵션 대화 상자. Hello 개인 정보 섹션을 선택 하 고 hello 두 번째 옵션-'hello 개인 정보 수준을 무시 하 고 잠재적으로 성능 향상'를 선택 합니다.

    ![Excel 빠른 결합](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. tooload SQL 감사 로그 hello 매개 변수가 확인 hello 설정 탭에서 올바르게 설정 하 고 다음 hello '데이터' 리본 선택 hello ' 모두 새로 고침 ' 단추를 클릭 합니다.

    ![Excel 매개 변수](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. hello에 hello 결과가 표시 **SQL 감사 로그** 시트 발견 되 고 응용 프로그램에서 hello 보안 이벤트의 hello 영향을 완화 하는 hello 비정상적인 활동의 심층 분석 toorun 있습니다.


## <a name="next-steps"></a>다음 단계
악의적인 사용자 또는 몇 가지 간단한 단계만 무단된 액세스 로부터 사용자 데이터베이스의 hello 보호를 향상 시킬 수 있습니다. 이 자습서에서는 다음에 대해 알아봅니다. 

> [!div class="checklist"]
> * 서버 및 데이터베이스에 대한 방화벽 규칙 설정
> * Tooyour 데이터베이스 보안 연결 문자열을 사용 하 여 연결
> * 사용자 액세스 관리
> * 암호화로 데이터 보호
> * SQL Database 감사 사용
> * SQL Database 위협 감지 사용

> [!div class="nextstepaction"]
>[SQL Database 성능 향상](sql-database-performance-tutorial.md)

