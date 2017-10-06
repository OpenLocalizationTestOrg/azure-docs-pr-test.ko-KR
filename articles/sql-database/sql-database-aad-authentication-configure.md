---
title: "aaaConfigure Azure Active Directory 인증-SQL | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect tooSQL 데이터베이스 및 Azure Active Directory 인증을 사용 하 여 SQL 데이터 웨어하우스 합니다."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리

이 문서에서는 어떻게 toocreate 및 Azure AD를 채운 다음 Azure AD를 사용 하 여 Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스 사용 합니다. 개요는 [Azure Active Directory 인증](sql-database-aad-authentication.md)을 참조하세요.

>  [!NOTE]  
>  Azure VM에서 실행 중인 서버에 Azure Active Directory 계정을 사용 하 여 지원 되지 않습니다 tooSQL를 연결 합니다. 대신 도메인 Active Directory 계정을 사용합니다.

## <a name="create-and-populate-an-azure-ad"></a>Azure AD 만들기 및 채우기
Azure AD를 만들고 사용자 및 그룹으로 채웁니다. Azure AD는 hello 초기 도메인 Azure AD 관리 되는 도메인을 수 있습니다. Azure AD는 온-프레미스 Active Directory 도메인 서비스는 hello Azure AD와 페더레이션된 될 수도 있습니다.

자세한 내용은 참조 [Azure Active Directory와 온-프레미스 id 통합](../active-directory/active-directory-aadconnect.md), [고유한 도메인 이름을 tooAzure AD 추가](../active-directory/active-directory-add-domain.md), [Microsoft Azure와의 페더레이션을 지원 Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Azure AD 디렉터리 관리](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Windows PowerShell을 사용 하 여 Azure AD 관리](/powershell/azure/overview?view=azureadps-2.0), 및 [하이브리드 Id 필요한 포트 및 프로토콜](../active-directory/active-directory-aadconnect-ports.md)합니다.

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>옵션: 연결 하거나 현재 Azure 구독과 연결 되어 있는 hello active directory 변경
tooassociate 조직에 대 한 hello Azure AD 디렉터리와 데이터베이스 hello 디렉터리가 설정 hello Azure 구독 호스팅 hello 데이터베이스에 대 한 신뢰할 수 있는 디렉터리입니다. 자세한 내용은 [Azure 구독과 Azure AD의 연관 관계](https://msdn.microsoft.com/library/azure/dn629581.aspx)를 참조하세요.

**추가 정보:** 모든 Azure 구독은 Azure AD 인스턴스와 트러스트 관계가 있습니다. 즉, 트러스트 하 여 해당 디렉터리 tooauthenticate 사용자, 서비스 및 장치입니다. 여러 구독 hello 신뢰할 수 있는 동일한 디렉터리만 구독 디렉터리를 하나만 신뢰 합니다. 어떤 디렉터리는 hello 구독에서 트러스트 나타나면 **설정** 에서 tab 키 [https://manage.windowsazure.com/](https://manage.windowsazure.com/)합니다. 구독에 보다 가깝습니다 구독의 자식 리소스 (웹 사이트, 데이터베이스 및 등)는 Azure의 다른 모든 리소스와 hello 관계와 달리 디렉터리와 구독에이 트러스트 관계가입니다. 구독이 만료 되 면 toothose hello 구독과 연결 된 다른 리소스에 액세스 하는 경우 또한 중지 됩니다. 하지만 Azure의 hello 디렉터리 남아 있으며 해당 디렉터리와 다른 구독을 연결 하 고 계속 toomanage hello directory 사용자 수 있습니다. 리소스에 대한 자세한 내용은 [Azure의 리소스 액세스 이해](https://msdn.microsoft.com/library/azure/dn584083.aspx)를 참조하세요.

hello 다음 절차 보여 toochange hello 지정된 된 구독에 대 한 디렉터리를 연결 하는 방식입니다.
1. Tooyour 연결 [Azure 클래식 포털](https://manage.windowsazure.com/) Azure 구독 관리자를 사용 하 여 합니다.
2. 왼쪽된 배너 hello 선택 **설정을**합니다.
3. 구독은 hello 설정 화면에 표시 됩니다. 클릭 하 여 hello 구독 표시 되지 않으면 원하는 경우 **구독** hello 위쪽에, 드롭 다운 hello **필터에서 디렉터리** 상자 구독을 포함 하는 hello 디렉터리를 선택 하 고 클릭 **적용**합니다.
   
    ![구독 선택][4]
4. Hello에 **설정** 영역에서 구독을 클릭 한 다음 클릭 **디렉터리 편집** hello hello 페이지 맨 아래에 있습니다.
   
    ![ad-settings-portal][5]
5. Hello에 **디렉터리 편집** 상자 hello 연결 된 SQL Server 또는 SQL 데이터 웨어하우스, Azure Active Directory를 선택 하 고 다음에 대 한 hello 화살표를 클릭 합니다.
   
    ![edit-directory-select][6]
6. Hello에 **확인** 디렉터리 매핑 대화 상자를 확인 하는 "**모든 공동 관리자가 제거 됩니다.**"
   
    ![edit-directory-confirm][7]
7. Hello 검사 tooreload hello 포털을 클릭 합니다.

   > [!NOTE]
   > Hello 디렉터리, 액세스 tooall 공동 관리자, Azure AD 사용자 및 그룹을 변경 및 디렉터리 백업 리소스 사용자 제거 되 고 액세스 toothis 구독 또는 리소스를 더 이상는 경우. 만, 서비스 관리자는 액세스를 구성할 수 hello 새 디렉터리에 따라 주체에 대 한 합니다. 이러한 변경에는 상당한 양의 시간 toopropagate tooall 리소스 걸릴 수 있습니다. Hello 디렉터리를 변경 하는, 또한 SQL 데이터베이스 및 SQL 데이터 웨어하우스 용 Azure AD 관리자 hello 변경과 기존 Azure AD 사용자에 대 한 데이터베이스 액세스를 허용 하지 않습니다. admin 님 안녕하세요 Azure AD 이어야 합니다 (아래 설명 참조)으로 다시 설정 새로운 Azure AD 사용자가 만들어야 합니다.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Azure SQL Server에 대한 Azure AD 관리자 만들기
각 Azure SQL server (호스트 하는 SQL 데이터베이스 또는 SQL 데이터 웨어하우스) hello 전체 Azure SQL server의 관리자에 게는 단일 서버 관리자 계정으로 시작 합니다. Azure AD 계정인 두 번째 SQL Server 관리자를 만들어야 합니다. 이 보안 주체는 hello master 데이터베이스에 포함 된 데이터베이스 사용자로 생성 됩니다. 관리자와 hello 서버 관리자 계정이의 멤버인 hello **db_owner** 모든 사용자의 역할, 데이터베이스 및 hello로 각 사용자 데이터베이스를 입력 **dbo** 사용자입니다. Hello 서버 관리자 계정에 대 한 자세한 내용은 참조 [데이터베이스 및 Azure SQL 데이터베이스에서 로그인 관리](sql-database-manage-logins.md)합니다.

Azure Active Directory 지역에서 복제를 사용 하는 경우 Azure Active Directory 관리자에 게 기본 hello와 hello 보조 서버에 구성 되어야 합니다. 서버에 Azure Active Directory 관리자가 없는 경우 다음 Azure Active Directory 로그인 및 사용자가 "연결할 수 없습니다" tooserver 오류가 나타납니다.

> [!NOTE]
> Hello Azure AD로 데이터베이스 사용자가 제안 된 사용 권한 toovalidate 없기 때문에 Azure AD 계정의 (hello Azure SQL server 관리자 계정 포함)를 기반으로 하는 사용자가 Azure AD 기반 사용자를 만들 수 없습니다.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Azure SQL Server에 대한 Azure Active Directory 관리자를 프로비전합니다

표시 하는 다음 두 절차를 수행 하는 hello tooprovision hello Azure 포털에서에서 하 고 PowerShell을 사용 하 여 Azure SQL server에 대 한 Azure Active Directory 관리자입니다.

### <a name="azure-portal"></a>Azure portal
1. Hello에 [Azure 포털](https://portal.azure.com/)에서 오른쪽 위 모서리 hello 클릭 하 여 연결 toodrop 가능한 활성 디렉터리 목록 아래로 합니다. Hello 선택 hello 기본 Azure AD로 Active Directory를 수정 합니다. 이 단계 링크 hello 구독 연결이 Active Directory와 동일한 구독 hello를 확인 하는 Azure SQL server와 함께 사용 되는 둘 다에 대해 Azure AD 및 SQL Server. (Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 hello Azure SQL server을 호스팅 될 수 있습니다.)   
    ![choose-ad][8]   
    
2. 왼쪽 배너 선택 hello에 **SQL server**을 선택 프로그램 **SQL server**, 한 다음 hello **SQL Server** 블레이드에서 클릭 **ActiveDirectory관리자**.   
3. Hello에 **Active Directory 관리자** 블레이드에서 클릭 **관리자를 설정**합니다.   
    ![active directory 선택](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. Hello에 **관리자 추가** 블레이드에서 사용자, 선택 hello 사용자 또는 그룹 toobe 관리자 검색 하 고 클릭 한 다음 **선택**합니다. (Active Directory 관리 블레이드 hello 모든 멤버와 Active Directory의 그룹을 표시 하는 데 사용 합니다. 회색으로 표시된 사용자나 그룹은 Azure AD 관리자로 지원되지 않기 때문에 선택할 수 없습니다. (Hello에서 지원 되는 관리자가 사용자의 hello 목록을 **Azure AD 기능 및 제한 사항** 섹션 [SQL 데이터 웨어하우스 또는 SQL 데이터베이스에서 인증을 위해 사용 하 여 Azure Active Directory 인증](sql-database-aad-authentication.md).) 역할 기반 액세스 제어 (RBAC) toohello 포털에만 적용 되며 없습니다 전파 tooSQL 서버.   
    ![관리자 선택](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Hello의 hello 위쪽 **Active Directory 관리자** 블레이드에서 클릭 **저장**합니다.   
    ![관리자 저장](./media/sql-database-aad-authentication/save-admin.png)   

관리자에 게 변경 hello 과정은 몇 분 정도 걸릴 수 있습니다. Hello에 새 관리자에 게 표시 한 다음 **Active Directory 관리자** 상자입니다.

   > [!NOTE]
   > Admin 님 안녕하세요 Azure AD 설정할 때는 hello 새 관리자 이름 (사용자 또는 그룹) 이미 있을 수 없습니다 hello 가상 master 데이터베이스에 SQL Server 인증 사용자로. 있는 경우 hello Azure AD 관리자 설치가 실패 합니다. 롤링 다시 생성 하 고 해당 그러한 관리자 (이름)을 이미 나타내는 존재 합니다. SQL Server 인증 사용자 hello Azure AD의 일부 이므로 Azure AD 인증을 사용 하 여 모든 노력 tooconnect toohello 서버 실패 합니다.
   > 


toolater hello 위쪽 hello에 관리자를 제거 **Active Directory 관리자** 블레이드에서 클릭 **관리자 제거**, 클릭 하 고 **저장**합니다.

### <a name="powershell"></a>PowerShell
PowerShell cmdlet toorun toohave Azure PowerShell 설치 되어 있고 실행 해야 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

가 Azure AD 관리자 tooprovision hello 다음 Azure PowerShell 명령을 실행 합니다.

* Add-AzureRmAccount
* Select-AzureRmSubscription

Tooprovision를 사용 하 고 Azure AD 관리자를 관리 하는 Cmdlet:

| Cmdlet 이름 | 설명 |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 프로비전합니다. (Hello 현재 구독에서 여야 합니다.) |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 제거합니다. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Azure Active Directory 관리자가 현재 hello Azure SQL server 또는 Azure SQL 데이터 웨어하우스 구성에 대 한 정보를 반환 합니다. |

PowerShell 명령 g e t-h toosee 내용이 다음이 명령을 각각에 대 한 예를 사용 하 여 ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``합니다.

Azure AD 관리자 그룹의 이름을 스크립트 프로 비전 다음 hello **DBA_Group** (개체 id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) hello에 대 한 **demo_server** 이라는 리소스 그룹에 서버 **그룹-23** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

hello **DisplayName** hello Azure AD 표시 이름 또는 hello 사용자 계정 이름 입력된 매개 변수를 허용 합니다. 예를 들어 ``DisplayName="John Smith"`` 또는 ``DisplayName="johns@contoso.com"``입니다. Azure AD 그룹만 hello Azure AD에 대 한 표시 이름을 사용할 수 있습니다.

> [!NOTE]
> Azure PowerShell 명령 hello ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` 에서 지원 되지 않는 사용자에 대 한 Azure AD 관리자를 프로 비전 방지 하지 않습니다. 지원 되지 않는 사용자를 프로비저닝할 수 있지만 tooa 데이터베이스를 연결할 수 없습니다. 
> 

hello 다음 예제에서는 선택적 hello **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Azure AD hello **ObjectID** 는 필요한 경우 hello **DisplayName** 고유 하지 않습니다. tooretrieve hello **ObjectID** 및 **DisplayName** 값, Azure 클래식 포털의 Active Directory 섹션 hello를 사용 하 고 사용자 또는 그룹의 hello 속성을 확인 합니다.
> 

다음 예에서는 hello Azure SQL server에 대 한 admin 님 안녕하세요 현재 Azure AD에 대 한 정보를 반환 합니다.

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

다음 예에서는 hello Azure AD 관리자를 제거 합니다.

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

또한 hello REST Api를 사용 하 여 Azure Active Directory 관리자를 제공할 수 있습니다. 자세한 내용은 [서비스 관리 REST API 참조 및 Azure SQL 데이터베이스에 대한 작업](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
또한 호출 hello CLI 명령을 수행 하 여 Azure AD 관리자를 프로 비전 할 수 있습니다.
| 명령 | 설명 |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 프로비전합니다. (Hello 현재 구독에서 여야 합니다.) |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 제거합니다. |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Azure Active Directory 관리자가 현재 hello Azure SQL server 또는 Azure SQL 데이터 웨어하우스 구성에 대 한 정보를 반환 합니다. |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Azure SQL server 또는 Azure SQL 데이터 웨어하우스에 대 한 Active Directory 관리자에 게 업데이트합니다. |

CLI 명령에 대한 자세한 내용은 [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server)을 참조하세요.  


## <a name="configure-your-client-computers"></a>클라이언트 컴퓨터 구성
모든 클라이언트 컴퓨터에서 응용 프로그램 또는 사용자 연결 있는 tooAzure SQL 데이터베이스 또는 Azure AD id를 사용 하 여 Azure SQL 데이터 웨어하우스 hello 다음 소프트웨어를 설치 해야 합니다.

* .NET Framework 4.6 이상, [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx)
* SQL Server 용 azure Active Directory 인증 라이브러리 (**ADALSQL 합니다. DLL**)는 여러 언어로 제공 됩니다 (x86 및 amd64) hello 다운로드 센터에서 [Microsoft SQL Server 용 Microsoft Active Directory 인증 라이브러리](http://www.microsoft.com/download/details.aspx?id=48742)합니다.

다음을 통해 이러한 요구 사항을 충족할 수 있습니다.

* 하나라도 설치 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 또는 [Visual Studio 2015 용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) 충족 hello.NET Framework 4.6 요구 사항입니다.
* Hello x86 버전을 설치 하는 SSMS **ADALSQL 합니다. DLL**합니다.
* Hello amd64 버전을 설치 하는 SSDT **ADALSQL 합니다. DLL**합니다.
* hello에서 최신 Visual Studio [Visual Studio 다운로드](https://www.visualstudio.com/downloads/download-visual-studio-vs) hello.NET Framework 4.6 요구 사항을 충족할 수 있지만 필요한 amd64 버전의 hello를 설치 하지 않는 **ADALSQL 합니다. DLL**합니다.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>AD id에 매핑된 데이터베이스 tooAzure 포함 된 데이터베이스 사용자 만들기

Azure Active Directory 인증에 포함 된 데이터베이스 사용자로 만든 데이터베이스 사용자가 toobe가 필요 합니다. Azure AD id에 따라 포함 된 데이터베이스 사용자는 데이터베이스 사용자를 로그인 hello master 데이터베이스에 없고에 어떤 지도 tooan id hello hello 데이터베이스와 연결 된 Azure AD 디렉터리 합니다. hello Azure AD id에는 개별 사용자 계정 또는 그룹 일 수 있습니다. 포함된 데이터베이스 사용자에 대한 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.

> [!NOTE]
> (예외로 hello 관리자) 데이터베이스 사용자 포털을 사용 하 여 만들 수 없습니다. RBAC 역할은 서버, SQL 데이터베이스 또는 SQL 데이터 웨어하우스 전파 tooSQL 다릅니다. Azure RBAC 역할 Azure 리소스 관리를 위해 사용 되 고 toodatabase 사용 권한을 적용 되지 않습니다. 예를 들어 hello **SQL Server 참가자** 역할 액세스 tooconnect toohello SQL 데이터베이스 또는 SQL 데이터 웨어하우스를 부여 하지 않습니다. TRANSACT-SQL 문을 사용 하 여 hello 데이터베이스에서 직접 hello 액세스 권한을 부여 해야 합니다.
>

Azure AD 기반 포함 된 데이터베이스 사용자 (관리자 외의 다른 hello 서버 hello 데이터베이스를 소유한) 있는 사용자로 Azure AD id가 있는 toohello 데이터베이스를 연결 하는 toocreate 이상 hello **ALTER ANY USER** 권한. 다음 TRANSACT-SQL 구문 다음 hello를 사용 하 여:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* hello Azure AD 그룹에 대 한 Azure AD 사용자 또는 hello 표시 이름을 사용자 계정 이름 될 수 있습니다.

**예:** toocreate 포함된 된 데이터베이스 사용자는 Azure AD를 나타내는 페더레이션 또는 도메인 사용자를 관리 대상:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate 포함된 된 데이터베이스 사용자는 Azure AD를 나타내는 또는 도메인 그룹을 페더레이션 보안 그룹의 hello 표시 이름을 제공 합니다.
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

포함된 된 데이터베이스 사용자는 Azure AD 토큰을 사용 하 여 연결 하는 응용 프로그램을 나타내는 toocreate:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Hello Azure 구독과 연결 된 Azure Active Directory 이외의 다른 Azure Active Directory에서 사용자를 직접 만들 수 없습니다. 그러나 Active Directory 노드와 연결 된 가져온된 사용자 hello에 다른 활성 디렉터리의 구성원 (이 외부 사용자 라고 함) hello Active Directory 테 넌 트의 tooan Active Directory 그룹 추가할 수 있습니다. 해당 AD 그룹에 대 한 포함 된 데이터베이스 사용자를 만들면 hello hello에서 사용자가 외부 Active Directory를 얻을 수 액세스 tooSQL 데이터베이스입니다.   

Azure Active Directory 기반의 포함된 데이터베이스 사용자 만들기와 관련한 자세한 내용은 [CREATE USER(Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx)를 참조하세요.

> [!NOTE]
> Toohello 서버를 연결할 모든 Azure AD 인증 사용자를 방지 하는 Azure SQL server에 대 한 hello Azure Active Directory 관리자를 제거 합니다. 필요한 경우 사용할 수 없는 Azure AD 사용자는 SQL 데이터베이스 관리자가 수동으로 삭제할 수 있습니다.   

>  [!NOTE]
>  표시 되 면 한 **연결 제한 시간이 만료**, tooset hello를 할 수 있습니다 `TransparentNetworkIPResolution` hello 연결 문자열 toofalse의 매개 변수입니다. 자세한 내용은 [.NET Framework 4.6.1의 연결 시간 초과 문제 – TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/)을 참조하세요.   

   
해당 사용자를 hello 받을 데이터베이스 사용자를 만들 때 **연결** 권한 toothat 데이터베이스 hello의 멤버로 연결할 수 있습니다 **공용** 역할입니다. 처음 사용 가능한 toohello 사용자는 모든 사용 권한이 부여 toohello 권한만 hello **공용** 역할 또는 사용 권한을 부여 tooany Windows 그룹의 구성원 지 합니다. Azure AD 기반 포함 된 데이터베이스 사용자를 프로 비전 한 번, 다른 유형의 사용자 권한을 tooany을 부여 하는 방식으로 동일한 hello hello 사용자 추가 권한을 부여할 수 있습니다. 일반적으로 toodatabase 역할 권한을 부여 하 고 사용자가 tooroles를 추가 합니다. 자세한 내용은 [데이터베이스 엔진의 권한 기초](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx)를 참조하세요. 특수 SQL 데이터베이스 역할에 대한 자세한 내용은 [Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요.
관리 도메인으로 가져온 페더레이션된 도메인 사용자는 관리 되는 hello 도메인 id를 사용 해야 합니다.

> [!NOTE]
> Azure AD 사용자가 붙습니다 hello 데이터베이스 메타 데이터에 형식과 E (EXTERNAL_USER) 및 그룹에 대 한 X (EXTERNAL_GROUPS) 형식. 자세한 내용은 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)를 참조하세요. 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>SSMS 또는 SSDT를 사용 하 여 toohello 사용자 데이터베이스 또는 데이터 웨어하우스 연결  
관리자에 게 Azure AD tooconfirm 제대로 설정, toohello 연결 **마스터** hello Azure AD 관리자 계정을 사용 하 여 데이터베이스입니다.
Azure AD 기반 포함 된 데이터베이스 사용자 (관리자 외의 다른 hello 서버 hello 데이터베이스를 소유한) tooprovision 액세스 toohello 데이터베이스가 있는 Azure AD id로 toohello 데이터베이스를 연결 합니다.

> [!IMPORTANT]
> Azure Active Directory 인증에 대한 지원은 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 Visual Studio 2015의 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)에서 사용 가능합니다. SSMS 2016 년 8 월 릴리스 hello에서는 관리자가 있는 Active Directory 유니버설 인증에 대 한 지원이 포함 되어 toorequire Multi-factor Authentication 전화 통화, 문자 메시지, 스마트 카드를 사용 하 여 pin 또는 모바일 앱 알림을 사용 합니다.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>SSMS 또는 SSDT를 사용 하는 Azure AD identity tooconnect를 사용 하 여  

다음 절차를 수행 하는 hello tooconnect tooa SQL SQL Server Management Studio 또는 SQL Server 데이터베이스 도구를 사용 하 여 Azure AD id로 데이터베이스 하는 방법을 보여 줍니다.

### <a name="active-directory-integrated-authentication"></a>Active Directory 통합 인증

TooWindows 페더레이션된 도메인에서 Azure Active Directory 자격 증명을 사용 하 여 로그인 하는 경우이 메서드를 사용 합니다.

1. Management Studio 또는 데이터 도구를 시작 및 hello **tooServer 연결** (또는 **tooDatabase 엔진 연결**) 대화 상자에서 hello **인증** 상자을 선택**통합-active Directory**합니다. 암호가 필요 하거나 hello 연결에 대 한 기존 자격 증명 나타납니다 입력할 수 있습니다.   

    ![AD 통합 인증 선택][11]
2. Hello 클릭 **옵션** 단추를 hello에 **연결 속성** 페이지 hello **toodatabase 연결** 상자 hello 이름을 입력 합니다 tooconnect hello 사용자 데이터베이스의 원하는 받는 사람. (hello **AD 도메인 이름 또는 테 넌 트 ID**"에 대 한 옵션은만 지원 **MFA 연결과 유니버설** 옵션, 그렇지 않으면 것은 회색으로 표시 합니다.)  

    ![Hello 데이터베이스 이름 선택][13]

## <a name="active-directory-password-authentication"></a>Active Directory 암호 인증

도메인 관리 hello Azure AD를 사용 하 여 Azure AD 사용자 이름으로 연결 하는 경우이 메서드를 사용 합니다. 예를 들어 원격으로 작업 하는 경우 액세스 toohello 도메인 없이 페더레이션된 계정에 대해 사용할 수 있습니다.

TooWindows 자격 증명을 사용 하 여 azure에 페더레이션 되지 않아서 있는 도메인에서 로그인 하거나 Azure AD 또는 초기 hello에 따라 클라이언트 도메인 hello 사용 하 여 Azure AD 인증을 사용 하는 경우이 방법을 사용 합니다.

1. Management Studio 또는 데이터 도구를 시작 및 hello **tooServer 연결** (또는 **tooDatabase 엔진 연결**) 대화 상자에서 hello **인증** 상자을 선택**Active Directory-암호**합니다.
2. Hello에 **사용자 이름** hello 형식에 Azure Active Directory 사용자 이름을 입력 합니다  **username@domain.com** 합니다. Hello Azure Active Directory에서에서 계정 이거나 hello Azure Active Directory와 페더레이션 할 도메인에서 계정을이 합니다.
3. Hello에 **암호** 상자 hello Azure Active Directory 계정에 대 한 사용자 암호를 입력 하거나 계정 도메인을 페더레이션 합니다.

    ![AD 암호 인증 선택][12]
4. Hello 클릭 **옵션** 단추를 hello에 **연결 속성** 페이지 hello **toodatabase 연결** 상자 hello 이름을 입력 합니다 tooconnect hello 사용자 데이터베이스의 원하는 받는 사람. (Hello 모양이 hello 이전 옵션 참조).

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>클라이언트 응용 프로그램에서 Azure AD identity tooconnect는를 사용 하 여

다음 절차를 수행 하는 hello tooconnect tooa SQL 클라이언트 응용 프로그램에서 Azure AD id로 데이터베이스 하는 방법을 보여 줍니다.

###  <a name="active-directory-integrated-authentication"></a>Active Directory 통합 인증

toouse 통합 Windows 인증, 도메인의 Active Directory를 Azure Active Directory와 페더레이션 되도록 해야 합니다. 클라이언트 응용 프로그램 (또는 서비스) 연결 중 toohello 데이터베이스 사용자의 도메인 자격 증명으로 도메인에 가입 된 컴퓨터에서 실행 되어야 합니다.

인증 및 Azure AD id 통합 tooconnect tooa 데이터베이스를 사용 하 여, hello 데이터베이스 연결 문자열에 hello 인증 키워드 tooActive 디렉터리 통합 설정 해야 합니다. hello 다음 C# 코드 샘플에서는 ADO.NET 합니다.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

연결 문자열 키워드 hello ``Integrated Security=True`` tooAzure SQL 데이터베이스를 연결 하기 위한 지원 되지 않습니다. Tooremove 공백이 필요 하 고 인증 too'ActiveDirectoryIntegrated 설정는 ODBC 연결을 만들 때는 '.

### <a name="active-directory-password-authentication"></a>Active Directory 암호 인증

인증 및 Azure AD id 통합 tooconnect tooa 데이터베이스를 사용 하 여, hello 인증 키워드 tooActive 디렉터리 암호를 설정 해야 합니다. hello 연결 문자열은 사용자 ID/UID 및 PWD 암호/키워드와 값이 있어야 합니다. hello 다음 C# 코드 샘플에서는 ADO.NET 합니다.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

사용할 수 있는 hello 데모 코드 샘플을 사용 하 여 Azure AD 인증 방법에 대 한 자세한 [Azure AD 인증 GitHub 데모](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth)합니다.

## <a name="azure-ad-token"></a>Azure AD 토큰
이 인증 방법에서 Azure Active Directory (AAD) 토큰을 가져와서 중간 계층 서비스 tooconnect tooAzure를 SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스를 수 있습니다. 이는 인증서 기반 인증을 비롯한 정교한 시나리오를 지원합니다. 네 가지 기본 단계 toouse Azure AD 토큰 인증을 완료 해야 합니다.

1. Azure Active Directory와 응용 프로그램을 등록 하 고 코드에 대 한 hello 클라이언트 id를 가져옵니다. 
2. 데이터베이스 사용자 나타내는 hello 응용 프로그램을 만듭니다. 6단계에서 완료).
3. Hello 응용 프로그램에 클라이언트 컴퓨터 실행 hello 인증서를 만듭니다.
4. 응용 프로그램에 대 한 키로 hello 인증서를 추가 합니다.

샘플 연결 문자열:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

자세한 내용은 [SQL Server 보안 블로그](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)를 참조하세요.

### <a name="sqlcmd"></a>sqlcmd

명령문 안녕, 13.1 hello에서 사용할 수 있는 sqlcmd의 버전을 사용 하 여 연결 [다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=825643)합니다.

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>다음 단계
- SQL Database의 액세스 및 제어에 대한 개요는 [SQL Database 액세스 및 제어](sql-database-control-access.md)를 참조하세요.
- SQL Database의 로그인, 사용자 및 데이터베이스 역할에 대한 개요는 [로그인, 사용자 및 데이터베이스 역할](sql-database-manage-logins.md)을 참조하세요.
- 데이터베이스 보안 주체에 대한 자세한 내용은 [보안 주체](https://msdn.microsoft.com/library/ms181127.aspx)를 참조하세요.
- 데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 역할](https://msdn.microsoft.com/library/ms189121.aspx)을 참조하세요.
- SQL Database의 방화벽 규칙에 대한 자세한 내용은 [SQL Database 방화벽 규칙](sql-database-firewall-configure.md)을 참조하세요.

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

