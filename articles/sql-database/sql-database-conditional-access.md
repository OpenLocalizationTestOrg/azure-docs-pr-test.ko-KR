---
title: "조건부 액세스 - Azure SQL Database 및 데이터 웨어하우스 | Microsoft Doc"
description: "Azure SQL Database 및 데이터 웨어하우스에 대한 조건부 액세스를 구성하는 방법에 대해 알아봅니다."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: 0dcec61c03a84197e2c351761c743683caa98a06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a><span data-ttu-id="b39c6-103">Azure SQL Database 및 데이터 웨어하우스를 사용하여 조건부 액세스(MFA)</span><span class="sxs-lookup"><span data-stu-id="b39c6-103">Conditional Access (MFA) with Azure SQL Database and Data Warehouse</span></span>  

<span data-ttu-id="b39c6-104">SQL Database와 SQL Data Warehouse는 Microsoft 조건부 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-104">Both SQL Database and SQL Data Warehouse support Microsoft Conditional Access.</span></span> <span data-ttu-id="b39c6-105">다음 단계에서는 조건부 액세스 정책을 적용하기 위해 SQL Database를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-105">The following steps show how to configure SQL Database to enforce a Conditional Access policy.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b39c6-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b39c6-106">Prerequisites</span></span>  
- <span data-ttu-id="b39c6-107">Azure Active Directory 인증을 지원하도록 SQL Database 또는 SQL Data Warehouse를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-107">You must configure your SQL Database or SQL Data Warehouse to support Azure Active Directory authentication.</span></span> <span data-ttu-id="b39c6-108">자세한 단계는 [SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리](sql-database-aad-authentication-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b39c6-108">For specific steps, see [Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication-configure.md).</span></span>  
- <span data-ttu-id="b39c6-109">다단계 인증을 사용하는 경우 최신 SSMS와 같은 지원되는 도구에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-109">When multi-factor authentication is enabled, you must connect with at supported tool, such as the latest SSMS.</span></span> <span data-ttu-id="b39c6-110">자세한 내용은 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](sql-database-ssms-mfa-authentication-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b39c6-110">For more information, see [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).</span></span>  

## <a name="configure-ca-for-azure-sql-dbdw"></a><span data-ttu-id="b39c6-111">Azure SQL DB/DW에 대한 CA 구성</span><span class="sxs-lookup"><span data-stu-id="b39c6-111">Configure CA for Azure SQL DB/DW</span></span>  
1.  <span data-ttu-id="b39c6-112">포털에 로그인하고 **Azure Active Directory**를 선택한 다음 **조건부 액세스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-112">Sign in to the Portal, select **Azure Active Directory**, and then select **Conditional access**.</span></span> <span data-ttu-id="b39c6-113">자세한 내용은 [Azure Active Directory 조건부 액세스 기술 참조](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b39c6-113">For more information, see [Azure Active Directory Conditional Access technical reference](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).</span></span>  
  <span data-ttu-id="b39c6-114">![조건부 액세스 블레이드](./media/sql-database-conditional-access/conditional-access-blade.png)</span><span class="sxs-lookup"><span data-stu-id="b39c6-114">![conditional access blade](./media/sql-database-conditional-access/conditional-access-blade.png)</span></span> 
     
2.  <span data-ttu-id="b39c6-115">**조건부 액세스 정책** 블레이드에서 **새 정책**을 클릭하고 이름을 입력한 다음 **규칙 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-115">In the **Conditional Access-Policies** blade, click **New policy**, provide a name, and then click **Configure rules**.</span></span>  
3.  <span data-ttu-id="b39c6-116">**할당** 아래에서 **사용자 및 그룹**을 선택하고 **사용자 및 그룹 선택**을 선택한 다음 조건부 액세스에 대한 사용자 또는 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-116">Under **Assignments**, select **Users and groups**, check **Select users and groups**, and then select the user or group for conditional access.</span></span> <span data-ttu-id="b39c6-117">**선택**을 클릭한 다음 **완료**를 클릭하여 선택 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-117">Click **Select**, and then click **Done** to accept your selection.</span></span>  
  <span data-ttu-id="b39c6-118">![사용자 및 그룹 선택](./media/sql-database-conditional-access/select-users-and-groups.png)</span><span class="sxs-lookup"><span data-stu-id="b39c6-118">![select users and groups](./media/sql-database-conditional-access/select-users-and-groups.png)</span></span>  

4.  <span data-ttu-id="b39c6-119">**클라우드 앱**을 선택하고 **앱 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-119">Select **Cloud apps**, click **Select apps**.</span></span> <span data-ttu-id="b39c6-120">조건부 액세스에 사용할 수 있는 모든 앱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-120">You see all apps available for conditional access.</span></span> <span data-ttu-id="b39c6-121">**Azure SQL Database**를 선택하고 아래쪽에서 **선택**을 클릭한 다음 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-121">Select **Azure SQL Database**, at the bottom click **Select**, and then click **Done**.</span></span>  
  <span data-ttu-id="b39c6-122">![SQL Database 선택](./media/sql-database-conditional-access/select-sql-database.png)</span><span class="sxs-lookup"><span data-stu-id="b39c6-122">![select SQL Database](./media/sql-database-conditional-access/select-sql-database.png)</span></span>  
  <span data-ttu-id="b39c6-123">다음 세 번째 스크린샷에 나열된 **Azure SQL Database**를 찾을 수 없는 경우 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-123">If you can’t find **Azure SQL Database** listed in the following third screen shot, complete the following steps:</span></span>   
  - <span data-ttu-id="b39c6-124">SSMS를 사용하여 AAD 관리자 계정으로 Azure SQL DB/DW 인스턴스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-124">Sign in to your Azure SQL DB/DW instance using SSMS with an AAD admin account.</span></span>  
  - <span data-ttu-id="b39c6-125">`CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-125">Execute `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.</span></span>  
  - <span data-ttu-id="b39c6-126">AAD에 로그인하고 Azure SQL Database 및 데이터 웨어하우스가 AAD의 응용 프로그램에 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-126">Sign in to AAD and verify that Azure SQL Database and Data Warehouse are listed in the applications in your AAD.</span></span>  

5.  <span data-ttu-id="b39c6-127">**액세스 제어**를 선택하고 **권한 부여**를 선택한 다음 적용하려는 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-127">Select **Access controls**, select **Grant**, and then check the policy you want to apply.</span></span> <span data-ttu-id="b39c6-128">예를 들어 **다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-128">For this example, we select **Require multi-factor authentication**.</span></span>  
  <span data-ttu-id="b39c6-129">![액세스 권한 부여 선택](./media/sql-database-conditional-access/grant-access.png)</span><span class="sxs-lookup"><span data-stu-id="b39c6-129">![select grant access](./media/sql-database-conditional-access/grant-access.png)</span></span>  

## <a name="summary"></a><span data-ttu-id="b39c6-130">요약</span><span class="sxs-lookup"><span data-stu-id="b39c6-130">Summary</span></span>  
<span data-ttu-id="b39c6-131">Azure AD Premium을 사용하여 Azure SQL DB/DW에 대한 연결을 허용하는 선택한 응용 프로그램(Azure SQL Database)은 이제 선택한 조건부 액세스 정책, **필요한 다단계 인증**을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-131">The selected application (Azure SQL Database) allowing to connect to Azure SQL DB/DW using Azure AD Premium, now enforces the selected Conditional Access policy, **Required multi-factor authentication.**</span></span>  
<span data-ttu-id="b39c6-132">다단계 인증 문제에 관한 Azure SQL Database 및 데이터 웨어하우스에 대한 질문은 MFAforSQLDB@microsoft.com에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c6-132">For questions about Azure SQL Database and Data Warehouse regarding multi-factor authentication, contact MFAforSQLDB@microsoft.com.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b39c6-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b39c6-133">Next steps</span></span>  

<span data-ttu-id="b39c6-134">자습서는 [Azure SQL Database 보안](sql-database-security-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b39c6-134">For a tutorial, see [Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>
