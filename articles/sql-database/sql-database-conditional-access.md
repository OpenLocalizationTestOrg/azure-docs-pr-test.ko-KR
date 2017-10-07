---
title: "Azure SQL 데이터베이스 및 데이터 웨어하우스 aaaConditional 액세스-| Microsoft 문서"
description: "자세한 내용은 Azure SQL 데이터베이스 및 데이터 웨어하우스에 대 한 조건부 액세스를 tooconfigure 방법입니다."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Azure SQL Database 및 데이터 웨어하우스를 사용하여 조건부 액세스(MFA)  

SQL Database와 SQL Data Warehouse는 Microsoft 조건부 액세스를 지원합니다. 단계 표시 방법을 따르는 hello tooconfigure SQL 데이터베이스 tooenforce 조건부 액세스 정책.  

## <a name="prerequisites"></a>필수 조건  
- SQL 데이터베이스 또는 SQL 데이터 웨어하우스 toosupport Azure Active Directory 인증을 구성 해야 합니다. 자세한 단계는 [SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리](sql-database-aad-authentication-configure.md)를 참조하세요.  
- 다단계 인증을 사용 하는 경우와 최신 SSMS hello와 같은 지원 되는 도구에 연결 해야 합니다. 자세한 내용은 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](sql-database-ssms-mfa-authentication-configure.md)을 참조하세요.  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Azure SQL DB/DW에 대한 CA 구성  
1.  Toohello 포털에에서 로그인 선택 **Azure Active Directory**를 선택한 후 **조건부 액세스**합니다. 자세한 내용은 [Azure Active Directory 조건부 액세스 기술 참조](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference)를 참조하세요.  
  ![조건부 액세스 블레이드](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  Hello에 **조건부 액세스 정책** 블레이드에서 클릭 **새 정책**,으로 이름을 입력 하 고 클릭 **규칙 구성**합니다.  
3.  아래 **할당**을 선택 **사용자 및 그룹**, 확인 **사용자 및 그룹 선택**, 한 다음 hello 사용자 또는 그룹에 대 한 조건부 액세스를 선택 합니다. 클릭 **선택**, 클릭 하 고 **수행** tooaccept 선택 합니다.  
  ![사용자 및 그룹 선택](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  **클라우드 앱**을 선택하고 **앱 선택**을 클릭합니다. 조건부 액세스에 사용할 수 있는 모든 앱이 표시됩니다. 선택 **Azure SQL 데이터베이스**, hello 맨 아래에 클릭 **선택**, 클릭 하 고 **수행**합니다.  
  ![SQL Database 선택](./media/sql-database-conditional-access/select-sql-database.png)  
  찾을 수 없는 경우 **Azure SQL 데이터베이스** hello 세 번째 스크린 샷 뒤에 나열 된, 단계를 수행 하는 hello를 완료 합니다.   
  - SSMS를 사용 하 여 AAD 관리자 계정으로 tooyour Azure SQL DB/DW 인스턴스에 로그인 합니다.  
  - `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`를 실행합니다.  
  - TooAAD 하 고 Azure SQL 데이터베이스 및 데이터 웨어하우스 프로그램 AAD에서 hello 응용 프로그램에 나열 되어 있는지 확인 합니다.  

5.  선택 **컨트롤 액세스**선택, **Grant**, tooapply hello 정책을 확인 합니다. 예를 들어 **다단계 인증 필요**를 선택합니다.  
  ![액세스 권한 부여 선택](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>요약  
허용 tooconnect tooAzure SQL DB/DW Azure AD Premium을 사용 하 여 선택 하는 hello 응용 프로그램 (Azure SQL 데이터베이스)는 이제 hello 선택한 조건부 액세스 정책을 적용 **multi-factor authentication 필요 합니다.**  
다단계 인증 문제에 관한 Azure SQL Database 및 데이터 웨어하우스에 대한 질문은 MFAforSQLDB@microsoft.com에 문의합니다.  

## <a name="next-steps"></a>다음 단계  

자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.
