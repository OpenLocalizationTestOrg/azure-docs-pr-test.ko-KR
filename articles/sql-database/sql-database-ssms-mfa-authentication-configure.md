---
title: "aaaConfigure 다단계 인증-Azure SQL | Microsoft Docs"
description: "SQL 데이터베이스 및 SQL Data Warehouse용 SSMS에서 Multi-Factor Authentication 사용"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>SQL Server Management Studio 및 Azure AD에 대한 Multi-factor Authentication(MFA) 구성 

이 항목에서는 SQL Server Management Studio로 toouse Active Directory를 Azure multi-factor authentication (MFA). Azure AD MFA SSMS 또는 SqlPackage.exe tooAzure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스에 연결할 때 사용할 수 있습니다.

Azure SQL Database 다단계 인증에 대한 개요는 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](sql-database-ssms-mfa-authentication.md)을 참조하세요.

## <a name="configuration-steps"></a>구성 단계

1. **Azure Active Directory 구성** -자세한 내용은 참조 [Azure AD 디렉터리 관리](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Azure Active Directory와 온-프레미스 id 통합](../active-directory/active-directory-aadconnect.md), [고유한 도메인 이름을 tooAzure AD 추가](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure에는 이제 Windows Server Active Directory와의 페더레이션을 지원](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), 및 [Windows PowerShell을 사용 하 여 Azure AD 관리 ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **MFA 구성** - 단계별 지침은 [Azure Multi-factor Authentication(MFA)이란?](../multi-factor-authentication/multi-factor-authentication.md), [Azure SQL Database 및 데이터웨어 하우스에서의 조건부 액세스(MFA)](sql-database-conditional-access.md)를 참조하세요. 전체 조건부 액세스에는 Premium Azure AD(Active Directory)가 필요합니다. 표준 Azure AD에서는 제한된 MFA가 제공됩니다.
3. **SQL 데이터베이스 또는 Azure AD 인증에 대 한 SQL 데이터 웨어하우스 구성** -단계별 지침에 대 한 참조 [연결 tooSQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여](sql-database-aad-authentication.md)합니다.
4. **SSMS 다운로드** -hello 클라이언트 컴퓨터에 다운로드에서 최신 SSMS hello [다운로드 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)합니다. 이 항목의 모든 hello 기능에 대해 사용 하 여 이상 년 7 월 2017 년 1 17.2 버전.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>SSMS를 통한 유니버설 인증을 사용하여 연결

단계를 수행 하는 hello tooconnect tooSQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 최신 SSMS hello 방법을 보여 줍니다.

1. 유니버설 인증을 사용 하 여 hello에 tooconnect **tooServer 연결** 대화 상자에서 **Active Directory에서 MFA 지 원하는 유니버설**합니다. (표시 되 면 **Active Directory 유니버설 인증** hello SSMS의 최신 버전에 없는 합니다.)  
   ![1mfa-universal-connect][1]  
2. 전체 hello **사용자 이름** hello 형태로 표시 hello Azure Active Directory 자격 증명을 사용 하 여 상자 `user_name@domain.com`합니다.  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. 게스트 사용자로 연결 하는 경우 클릭 해야 **옵션**, 등과 hello **연결 속성** 대화 상자, 전체 hello **AD 도메인 이름 또는 테 넌 트 ID** 상자입니다. 자세한 내용은 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](sql-database-ssms-mfa-authentication.md)을 참조하세요.
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. 일반적으로 SQL 데이터베이스 및 SQL 데이터 웨어하우스에 대 한 클릭 해야 **옵션** hello에 hello 데이터베이스를 지정 하 고 **옵션** 대화 상자. (사용자가 게스트 사용자 hello 연결 된 경우 (즉, joe@outlook.com), hello 확인란을 선택 하 고 옵션의 일부로 hello 현재 AD 도메인 이름 또는 테 넌 트 ID를 추가 해야 합니다. [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증]()(sql-database-ssms-mfa-authentication.md)을 참조하세요. 그런 다음 **연결**을 클릭합니다.  
5. Hello 때 **tooyour 계정에 로그인** 대화 상자가 나타나면 hello 계정 및 Azure Active Directory id의 암호를 제공 합니다. 사용자가 Azure AD와 페더레이션된 도메인에 속할 경우 암호가 필요하지 않습니다.  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > MFA가 필요하지 않은 계정을 사용하는 유니버설 인증의 경우 이 시점에서 연결합니다. MFA를 필요로 하는 사용자에 대 한 단계를 수행 하는 hello로 계속:
   >  
   
6. 두 개의 MFA 설치 대화 상자가 나타날 수 있습니다. 이 한 번 작업 hello MFA 관리자 설정에 따라 다르며 선택 사항이 될 수 있습니다. MFA 활성화 도메인에 대해이 단계는 경우에 따라 미리 정의 된 (예를 들어 hello 도메인 필요 사용자 toouse 스마트 카드와 핀).  
   ![3mfa-setup][3]  
7. hello 두 번째 가능한 대화 상자에서는 인증 방법의 tooselect hello 세부 정보는 한 번 hello 가능한 옵션은 관리자가 구성 됩니다.  
   ![4mfa-verify-1][4]  
8. Azure Active Directory hello tooyou 정보를 확인 하는 hello를 보냅니다. Hello 확인 코드를 받으면 hello에 입력 **확인 코드 입력** 고 클릭 **로그인**합니다.  
   ![5mfa-verify-2][5]  

확인이 완료되면 SSMS는 일반적으로 가정된 유효한 자격 증명 및 방화벽 액세스를 연결합니다.

## <a name="next-steps"></a>다음 단계

* Azure SQL Database Multi-factor Authentication(MFA) 인증에 대한 개요는 [SQL 데이터베이스 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](sql-database-ssms-mfa-authentication.md)을 참조하세요.
* 다른 tooyour 데이터베이스에 액세스할 권한을 부여할: [SQL 데이터베이스 인증 및 권한 부여: 액세스 부여](sql-database-manage-logins.md)  
다른 사람이 hello 방화벽을 통해 연결할 수 있는지 확인: [Azure 포털 hello Azure SQL 데이터베이스 서버 수준 방화벽 규칙 사용 하는 구성](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

