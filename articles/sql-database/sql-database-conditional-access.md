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
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a><span data-ttu-id="2c4e2-103">Azure SQL Database 및 데이터 웨어하우스를 사용하여 조건부 액세스(MFA)</span><span class="sxs-lookup"><span data-stu-id="2c4e2-103">Conditional Access (MFA) with Azure SQL Database and Data Warehouse</span></span>  

<span data-ttu-id="2c4e2-104">SQL Database와 SQL Data Warehouse는 Microsoft 조건부 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-104">Both SQL Database and SQL Data Warehouse support Microsoft Conditional Access.</span></span> <span data-ttu-id="2c4e2-105">단계 표시 방법을 따르는 hello tooconfigure SQL 데이터베이스 tooenforce 조건부 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-105">hello following steps show how tooconfigure SQL Database tooenforce a Conditional Access policy.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="2c4e2-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2c4e2-106">Prerequisites</span></span>  
- <span data-ttu-id="2c4e2-107">SQL 데이터베이스 또는 SQL 데이터 웨어하우스 toosupport Azure Active Directory 인증을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-107">You must configure your SQL Database or SQL Data Warehouse toosupport Azure Active Directory authentication.</span></span> <span data-ttu-id="2c4e2-108">자세한 단계는 [SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리](sql-database-aad-authentication-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-108">For specific steps, see [Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication-configure.md).</span></span>  
- <span data-ttu-id="2c4e2-109">다단계 인증을 사용 하는 경우와 최신 SSMS hello와 같은 지원 되는 도구에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-109">When multi-factor authentication is enabled, you must connect with at supported tool, such as hello latest SSMS.</span></span> <span data-ttu-id="2c4e2-110">자세한 내용은 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](sql-database-ssms-mfa-authentication-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-110">For more information, see [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).</span></span>  

## <a name="configure-ca-for-azure-sql-dbdw"></a><span data-ttu-id="2c4e2-111">Azure SQL DB/DW에 대한 CA 구성</span><span class="sxs-lookup"><span data-stu-id="2c4e2-111">Configure CA for Azure SQL DB/DW</span></span>  
1.  <span data-ttu-id="2c4e2-112">Toohello 포털에에서 로그인 선택 **Azure Active Directory**를 선택한 후 **조건부 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-112">Sign in toohello Portal, select **Azure Active Directory**, and then select **Conditional access**.</span></span> <span data-ttu-id="2c4e2-113">자세한 내용은 [Azure Active Directory 조건부 액세스 기술 참조](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-113">For more information, see [Azure Active Directory Conditional Access technical reference](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).</span></span>  
  <span data-ttu-id="2c4e2-114">![조건부 액세스 블레이드](./media/sql-database-conditional-access/conditional-access-blade.png)</span><span class="sxs-lookup"><span data-stu-id="2c4e2-114">![conditional access blade](./media/sql-database-conditional-access/conditional-access-blade.png)</span></span> 
     
2.  <span data-ttu-id="2c4e2-115">Hello에 **조건부 액세스 정책** 블레이드에서 클릭 **새 정책**,으로 이름을 입력 하 고 클릭 **규칙 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-115">In hello **Conditional Access-Policies** blade, click **New policy**, provide a name, and then click **Configure rules**.</span></span>  
3.  <span data-ttu-id="2c4e2-116">아래 **할당**을 선택 **사용자 및 그룹**, 확인 **사용자 및 그룹 선택**, 한 다음 hello 사용자 또는 그룹에 대 한 조건부 액세스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-116">Under **Assignments**, select **Users and groups**, check **Select users and groups**, and then select hello user or group for conditional access.</span></span> <span data-ttu-id="2c4e2-117">클릭 **선택**, 클릭 하 고 **수행** tooaccept 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-117">Click **Select**, and then click **Done** tooaccept your selection.</span></span>  
  <span data-ttu-id="2c4e2-118">![사용자 및 그룹 선택](./media/sql-database-conditional-access/select-users-and-groups.png)</span><span class="sxs-lookup"><span data-stu-id="2c4e2-118">![select users and groups](./media/sql-database-conditional-access/select-users-and-groups.png)</span></span>  

4.  <span data-ttu-id="2c4e2-119">**클라우드 앱**을 선택하고 **앱 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-119">Select **Cloud apps**, click **Select apps**.</span></span> <span data-ttu-id="2c4e2-120">조건부 액세스에 사용할 수 있는 모든 앱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-120">You see all apps available for conditional access.</span></span> <span data-ttu-id="2c4e2-121">선택 **Azure SQL 데이터베이스**, hello 맨 아래에 클릭 **선택**, 클릭 하 고 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-121">Select **Azure SQL Database**, at hello bottom click **Select**, and then click **Done**.</span></span>  
  <span data-ttu-id="2c4e2-122">![SQL Database 선택](./media/sql-database-conditional-access/select-sql-database.png)</span><span class="sxs-lookup"><span data-stu-id="2c4e2-122">![select SQL Database](./media/sql-database-conditional-access/select-sql-database.png)</span></span>  
  <span data-ttu-id="2c4e2-123">찾을 수 없는 경우 **Azure SQL 데이터베이스** hello 세 번째 스크린 샷 뒤에 나열 된, 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-123">If you can’t find **Azure SQL Database** listed in hello following third screen shot, complete hello following steps:</span></span>   
  - <span data-ttu-id="2c4e2-124">SSMS를 사용 하 여 AAD 관리자 계정으로 tooyour Azure SQL DB/DW 인스턴스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-124">Sign in tooyour Azure SQL DB/DW instance using SSMS with an AAD admin account.</span></span>  
  - <span data-ttu-id="2c4e2-125">`CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-125">Execute `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.</span></span>  
  - <span data-ttu-id="2c4e2-126">TooAAD 하 고 Azure SQL 데이터베이스 및 데이터 웨어하우스 프로그램 AAD에서 hello 응용 프로그램에 나열 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-126">Sign in tooAAD and verify that Azure SQL Database and Data Warehouse are listed in hello applications in your AAD.</span></span>  

5.  <span data-ttu-id="2c4e2-127">선택 **컨트롤 액세스**선택, **Grant**, tooapply hello 정책을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-127">Select **Access controls**, select **Grant**, and then check hello policy you want tooapply.</span></span> <span data-ttu-id="2c4e2-128">예를 들어 **다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-128">For this example, we select **Require multi-factor authentication**.</span></span>  
  <span data-ttu-id="2c4e2-129">![액세스 권한 부여 선택](./media/sql-database-conditional-access/grant-access.png)</span><span class="sxs-lookup"><span data-stu-id="2c4e2-129">![select grant access](./media/sql-database-conditional-access/grant-access.png)</span></span>  

## <a name="summary"></a><span data-ttu-id="2c4e2-130">요약</span><span class="sxs-lookup"><span data-stu-id="2c4e2-130">Summary</span></span>  
<span data-ttu-id="2c4e2-131">허용 tooconnect tooAzure SQL DB/DW Azure AD Premium을 사용 하 여 선택 하는 hello 응용 프로그램 (Azure SQL 데이터베이스)는 이제 hello 선택한 조건부 액세스 정책을 적용 **multi-factor authentication 필요 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2c4e2-131">hello selected application (Azure SQL Database) allowing tooconnect tooAzure SQL DB/DW using Azure AD Premium, now enforces hello selected Conditional Access policy, **Required multi-factor authentication.**</span></span>  
<span data-ttu-id="2c4e2-132">다단계 인증 문제에 관한 Azure SQL Database 및 데이터 웨어하우스에 대한 질문은 MFAforSQLDB@microsoft.com에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-132">For questions about Azure SQL Database and Data Warehouse regarding multi-factor authentication, contact MFAforSQLDB@microsoft.com.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2c4e2-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c4e2-133">Next steps</span></span>  

<span data-ttu-id="2c4e2-134">자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c4e2-134">For a tutorial, see [Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>
