---
title: "aaaMulti 2 단계 인증-Azure SQL | Microsoft Docs"
description: "SQL 데이터베이스 및 SQL Data Warehouse용 SSMS에서 Multi-Factor Authentication 사용"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)
Azure SQL Database 및 Azure SQL Data Warehouse는 *Active Directory 유니버설 인증*을 사용하여 SSMS(SQL Server Management Studio)에서의 연결을 지원합니다. 
**다운로드 최신 SSMS hello** -hello 클라이언트 컴퓨터에서에서 hello SSMS의 최신 버전을 다운로드 [다운로드 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)합니다. 이 항목의 모든 hello 기능에 대해 사용 하 여 이상 년 7 월 2017 년 1 17.2 버전.  연결 대화 상자, 가장 최근의 hello 다음과 같은: ![1mfa universal 연결](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "hello 사용자 이름 상자를 완료 합니다.")  

## <a name="hello-five-authentication-options"></a>hello 5 개 인증 옵션  
- Active Directory 유니버설 인증에서는 hello 두 가지 비 대화형 인증 방법 (`Active Directory - Password` 인증 및 `Active Directory - Integrated` 인증). 비대화형 `Active Directory - Password` 및 `Active Directory - Integrated` 인증 방법은 여러 다른 응용 프로그램(ADO.NET, JDBC, ODBC 등)에서 사용할 수 있습니다. 이러한 두 가지 방법을 사용할 경우 팝업 대화 상자가 절대 표시되지 않습니다.

- `Active Directory - Universal with MFA` 인증은 *Azure MFA(Multi-factor Authentication)*를 지원하는 대화형 방법입니다. Azure MFA 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다. 원하는 수 있도록 사용자 toochoose hello 방법 쉽게 확인 옵션 (전화 통화, 문자 메시지, 스마트 카드와 해당 pin 또는 모바일 앱 알림을) 범위를 통한 강력한 인증을 제공 합니다. Azure AD를 사용하는 대화형 MFA는 유효성 검사를 위한 팝업 대화 상자를 표시할 수 있습니다.

Multi-Factor Authentication에 대한 설명을 보려면 [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)을 참조하세요.
[SQL Server Management Studio에 대한 Azure SQL Database multi-factor authentication 구성](sql-database-ssms-mfa-authentication-configure.md)을 참조하세요.

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Azure AD 도메인 이름 또는 테넌트 ID 매개 변수   

부터는 [SSMS 버전 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), hello로 가져온 사용자가 게스트 사용자로 다른 Azure Active 디렉터리의 현재 Active Directory 나 연결 될 때 테 넌 트 ID를 hello Azure AD 도메인 이름을 제공 수 있다. 게스트 사용자에는 타 Azure AD에서 초대 받은 사용자, outlook.com, hotmail.com, live.com 등의 Microsoft 계정, gmail.com 등의 타 계정이 포함됩니다. 이 정보를 사용 하면 **Active Directory 유니버설 MFA 인증** tooidentify hello 올바른 인증 기관. 이 옵션은 outlook.com, hotmail.com, live.com 또는 MSA 외 계정을 등도 필요한 toosupport Microsoft 계정 (MSA). Id를 이러한 모든 사용자가 자신의 Azure AD 도메인 이름 또는 테 넌 트 유니버설 인증을 사용 하 여 인증 toobe 입력 해야 합니다. 이 매개 변수는 hello 현재 Azure AD 도메인 이름/테 넌 트 ID hello를와 연결 된 Azure 서버를 나타냅니다. 예를 들어, Azure 서버는 Azure AD 도메인에 연결 하는 경우 `contosotest.onmicrosoft.com` 여기서 사용자 `joe@contosodev.onmicrosoft.com` Azure AD 도메인에서 가져온된 사용자로 호스팅되는 `contosodev.onmicrosoft.com`,이 사용자는 도메인 이름이 필요 합니다. tooauthenticate hello `contosotest.onmicrosoft.com`합니다. Hello 사용자의 연결 된 Azure AD tooAzure hello 서버는 기본 사용자가 MSA 계정이 아닙니다, 도메인 이름 또는 테 넌 트 ID가 없습니다.이 필요 합니다. tooenter hello에서에서 매개 변수 (버전 17.2 SSMS로 시작) hello **tooDatabase 연결** 완료 hello 대화 상자, 대화 상자를 선택 하 **Active Directory-mfa Universal** 인증을 클릭 **옵션**, 전체 hello **사용자 이름** 고 hello 클릭 **연결 속성** 탭 합니다. Hello 확인 **AD 도메인 이름 또는 테 넌 트 ID** 고 hello 도메인 이름 예: 인증 권한 제공 (**contosotest.onmicrosoft.com**) 또는 hello 테 넌 트 ID의 GUID를 환영  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Azure AD 비즈니스 toobusiness 지원   
Azure AD 사용자가 게스트 사용자로 Azure AD B2B 시나리오에 대 한 지원 (참조 [Azure B2B 공동 작업 이란](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) tooSQL 데이터베이스 및 SQL 데이터 웨어하우스 현재 Azure AD에서 생성 하 고 수동으로 매핑된 그룹의 구성원의 일부로 서만 연결할 수 있습니다 Transact SQL hello를 사용 하 여 `CREATE USER` 문에 지정된 된 데이터베이스에 있습니다. 예를 들어 경우 `steve@gmail.com` 초대 된 tooAzure AD는 `contosotest` (hello Azure Ad 도메인과 `contosotest.onmicrosoft.com`), 같은 Azure AD 그룹 `usergroup` hello hello 포함 된 Azure AD에서에서 만들어져야 합니다 `steve@gmail.com` 멤버입니다. 그런 다음 Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` 문을 실행하여 Azure AD SQL 관리자 또는 Azure AD DBO로 특정 데이터베이스(즉 MyDatabase)에 대해 이 그룹을 만들어야 합니다. Hello 데이터베이스 사용자를 만든 후 다음 사용자 hello `steve@gmail.com` 너무 로그인 할 수 있습니다`MyDatabase` hello SSMS 인증 옵션을 사용 하 여 `Active Directory – Universal with MFA support`합니다. hello usergroup, 기본적으로는 사용 권한과 toobe hello에 부여 해야 하는 모든 추가 데이터 액세스를 연결 하는 hello만 일반적인 방법입니다. 해당 사용자 참고 `steve@gmail.com` 게스트 사용자가 hello 확인란을 선택 하 고 hello AD 도메인 이름을 추가 하는 대로 `contosotest.onmicrosoft.com` hello SSMS에서에서 **연결 속성** 대화 상자. hello **AD 도메인 이름 또는 테 넌 트 ID** 옵션은만 hello Universal MFA 연결 옵션을 사용에 대 한 지원, 그렇지 않으면 것은 회색으로 표시 합니다.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>SQL 데이터베이스 및 SQL Data Warehouse에 대한 유니버설 인증 제한 사항
* SSMS 및 SqlPackage.exe 현재 Active Directory 유니버설 인증을 통해 MFA에 대해 사용 하는 hello 유일한 도구는입니다.
* SSMS 버전 17.2는 MFA를 통한 유니버설 인증을 사용하는 다중 사용자 동시 액세스를 지원합니다. 유니버설 인증 tooa 단일 Azure Active Directory 계정을 사용 하 여 SSMS의 인스턴스에 대 한 로그를 제한 하는 17.0 및 17.1, 버전. 다른 Azure AD 계정에 toolog, SSMS의 다른 인스턴스를 사용 해야 합니다. (이 제한 사항은 제한 tooActive Directory 유니버설 인증 이며 toodifferent 서버 Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증을 사용 하 여 로그인 할 수 있습니다).
* SSMS는 개체 탐색기, 쿼리 편집기 및 쿼리 저장소 시각화에 대해 Active Directory 유니버설 인증을 지원합니다.
* SSMS 버전 17.2는 데이터 데이터베이스 내보내기/추출/배포를 위한 DacFx Wizard 마법사 지원을 제공합니다. 유니버설 인증을 사용 하 여 hello 초기 인증 대화 상자를 통해 특정 사용자가 인증 되 면 hello DacFx 마법사 함수 hello 동일한 방식으로 다른 모든 인증 방법에 대 한 합니다.
* hello SSMS 테이블 디자이너에서 유니버설 인증을 지원 하지 않습니다.
* 지원되는 버전의 SSMS를 사용해야 한다는 점을 제외하고, Active Directory 유니버설 인증에 대한 추가적인 소프트웨어 요구 사항은 없습니다.  
* 유니버설 인증에 대 한 hello Active Directory 인증 라이브러리 (ADAL) 버전 업데이트 tooits 최신 ADAL.dll 3.13.9 사용할 수 있는 릴리스 버전을 되었습니다. [Active Directory 인증 라이브러리 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)을 참조하세요.


## <a name="next-steps"></a>다음 단계

- [SQL Server Management Studio에 대한 Azure SQL Database multi-factor authentication 구성](sql-database-ssms-mfa-authentication-configure.md)을 참조하세요.
- 다른 tooyour 데이터베이스에 액세스할 권한을 부여할: [SQL 데이터베이스 인증 및 권한 부여: 액세스 부여](sql-database-manage-logins.md)  
- 다른 사람이 hello 방화벽을 통해 연결할 수 있는지 확인: [Azure 포털 hello Azure SQL 데이터베이스 서버 수준 방화벽 규칙 사용 하는 구성](sql-database-configure-firewall-settings.md)  
- [SQL Database 또는 SQL Data Warehouse에서의 Azure Active Directory 인증 구성 및 관리](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework(17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [가져올 BACPAC 파일 tooa 새 Azure SQL 데이터베이스](../sql-database/sql-database-import.md)  
- [Azure SQL 데이터베이스 tooa BACPAC 파일 내보내기](../sql-database/sql-database-export.md)  
- C# 인터페이스 [IUniversalAuthProvider Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
