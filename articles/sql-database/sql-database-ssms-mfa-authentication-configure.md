---
title: "Multi-Factor Authentication 구성 - Azure SQL | Microsoft Docs"
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
ms.openlocfilehash: fd78b34e8bbefdaa79a73d69ff2a0e3c1c342e98
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a><span data-ttu-id="907e0-103">SQL Server Management Studio 및 Azure AD에 대한 Multi-factor Authentication(MFA) 구성 </span><span class="sxs-lookup"><span data-stu-id="907e0-103">Configure multi-factor authentication for SQL Server Management Studio and Azure AD</span></span>

<span data-ttu-id="907e0-104">이 항목에서는 SQL Server Management Studio에서 Azure Active Directory Multi-factor Authentication(MFA)을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-104">This topic shows you how to use Azure Active Directory multi-factor authentication (MFA) with SQL Server Management Studio.</span></span> <span data-ttu-id="907e0-105">Azure SQL Database 및 Azure SQL Data Warehouse에 SSMS 또는 SqlPackage.exe를 연결할 때 Azure AD MFA를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-105">Azure AD MFA can be used when connecting SSMS or SqlPackage.exe to Azure SQL Database and Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="907e0-106">Azure SQL Database 다단계 인증에 대한 개요는 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](sql-database-ssms-mfa-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-106">For an overview of Azure SQL Database multi-factor authentication, see [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>

## <a name="configuration-steps"></a><span data-ttu-id="907e0-107">구성 단계</span><span class="sxs-lookup"><span data-stu-id="907e0-107">Configuration steps</span></span>

1. <span data-ttu-id="907e0-108">**Azure Active Directory 구성** - 자세한 내용은 [Azure AD 디렉터리 관리](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Azure Active Directory와 온-프레미스 ID 통합](../active-directory/active-directory-aadconnect.md), [Azure AD에 고유한 도메인 이름 추가](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure는 이제 Windows Server Active Directory와의 페더레이션 지원](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/) 및 [Windows PowerShell을 사용하여 Azure AD 관리](https://msdn.microsoft.com/library/azure/jj151815.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-108">**Configure an Azure Active Directory** - For more information, see [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), and [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span></span>
2. <span data-ttu-id="907e0-109">**MFA 구성** - 단계별 지침은 [Azure Multi-factor Authentication(MFA)이란?](../multi-factor-authentication/multi-factor-authentication.md), [Azure SQL Database 및 데이터웨어 하우스에서의 조건부 액세스(MFA)](sql-database-conditional-access.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-109">**Configure MFA** - For step-by-step instructions, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md), [Conditional Access (MFA) with Azure SQL Database and Data Warehouse](sql-database-conditional-access.md).</span></span> <span data-ttu-id="907e0-110">전체 조건부 액세스에는 Premium Azure AD(Active Directory)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-110">(Full conditional access requires a Premium Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="907e0-111">표준 Azure AD에서는 제한된 MFA가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-111">Limited MFA is available with a standard Azure AD.)</span></span>
3. <span data-ttu-id="907e0-112">**Azure AD 인증을 위해 SQL Database 또는 SQL Data Warehouse 구성** - 단계별 지침은 [Azure Active Directory 인증을 사용하여 SQL Database 또는 SQL Data Warehouse에 연결](sql-database-aad-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-112">**Configure SQL Database or SQL Data Warehouse for Azure AD Authentication** - For step-by-step instructions, see [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>
4. <span data-ttu-id="907e0-113">**SSMS 다운로드** - 클라이언트 컴퓨터에서 최신 SSMS를 [SSMS(SQL Server Management Studio) 다운로드](https://msdn.microsoft.com/library/mt238290.aspx)에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-113">**Download SSMS** - On the client computer, download the latest SSMS, from [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> <span data-ttu-id="907e0-114">이 항목의 모든 기능에서는 2017년 7월 버전 17.2 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-114">For all the features in this topic, use at least July 2017, version 17.2.</span></span>  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a><span data-ttu-id="907e0-115">SSMS를 통한 유니버설 인증을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="907e0-115">Connecting by using universal authentication with SSMS</span></span>

<span data-ttu-id="907e0-116">다음 단계에서는 최신 SSMS를 사용하여 SQL 데이터베이스 또는 SQL Data Warehouse에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-116">The following steps show how to connect to SQL Database or SQL Data Warehouse by using the latest SSMS.</span></span>

1. <span data-ttu-id="907e0-117">유니버설 인증을 사용하여 연결하려면 **서버에 연결** 대화 상자에서 **Active Directory - MFA 지원을 통한 유니버설 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-117">To connect using Universal Authentication, on the **Connect to Server** dialog box, select **Active Directory - Universal with MFA support**.</span></span> <span data-ttu-id="907e0-118">**Active Directory 유니버설 인증**이 표시되면 최신 SSMS이 아닌 것입니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-118">(If you see **Active Directory Universal Authentication** you are not on the latest version of SSMS.)</span></span>  
   <span data-ttu-id="907e0-119">![1mfa-universal-connect][1]</span><span class="sxs-lookup"><span data-stu-id="907e0-119">![1mfa-universal-connect][1]</span></span>  
2. <span data-ttu-id="907e0-120">Azure Active Directory 자격 증명을 사용하여 **사용자 이름** 상자를 `user_name@domain.com` 형식으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-120">Complete the **User name** box with the Azure Active Directory credentials, in the format `user_name@domain.com`.</span></span>  
   <span data-ttu-id="907e0-121">![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)</span><span class="sxs-lookup"><span data-stu-id="907e0-121">![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)</span></span>   
3. <span data-ttu-id="907e0-122">게스트 사용자로 연결하는 경우 **옵션**을 클릭하고 **연결 속성** 대화 상자에서 **AD 도메인 이름 또는 테넌트 ID** 상자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-122">If you are connecting as a guest user, you must click **Options**, and on the **Connection Property** dialog box, complete the **AD domain name or tenant ID** box.</span></span> <span data-ttu-id="907e0-123">자세한 내용은 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](sql-database-ssms-mfa-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-123">For more information, see [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>
   <span data-ttu-id="907e0-124">![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)</span><span class="sxs-lookup"><span data-stu-id="907e0-124">![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)</span></span>   
4. <span data-ttu-id="907e0-125">SQL Database 및 SQL Data Warehouse에 대해 평소처럼 **옵션**을 클릭하고 **옵션** 대화 상자에서 데이터베이스를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-125">As usual for SQL Database and SQL Data Warehouse, you must click **Options** and specify the database on the **Options** dialog box.</span></span> <span data-ttu-id="907e0-126">연결된 사용자가 게스트 사용자이면(즉 joe@outlook.com) 상자를 선택하고 현재 AD 도메인 이름이나 테넌트 ID를 옵션의 일부로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-126">(If the connected user is a guest user ( i.e. joe@outlook.com), you must check the box and add the current AD domain name or tenant ID as part of Options.</span></span> <span data-ttu-id="907e0-127">[SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증]()(sql-database-ssms-mfa-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-127">See [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)]()(sql-database-ssms-mfa-authentication.md.</span></span> <span data-ttu-id="907e0-128">그런 다음 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-128">Then click **Connect**.</span></span>  
5. <span data-ttu-id="907e0-129">**사용자 계정 로그인** 대화 상자가 나타나면 Azure Active Directory ID의 계정 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-129">When the **Sign in to your account** dialog box appears, provide the account and password of your Azure Active Directory identity.</span></span> <span data-ttu-id="907e0-130">사용자가 Azure AD와 페더레이션된 도메인에 속할 경우 암호가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-130">No password is required if a user is part of a domain federated with Azure AD.</span></span>  
   <span data-ttu-id="907e0-131">![2mfa-sign-in][2]</span><span class="sxs-lookup"><span data-stu-id="907e0-131">![2mfa-sign-in][2]</span></span>  

   > [!NOTE]
   > <span data-ttu-id="907e0-132">MFA가 필요하지 않은 계정을 사용하는 유니버설 인증의 경우 이 시점에서 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-132">For Universal Authentication with an account that does not require MFA, you connect at this point.</span></span> <span data-ttu-id="907e0-133">MFA가 필요한 사용자는 다음 단계를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-133">For users requiring MFA, continue with the following steps:</span></span>
   >  
   
6. <span data-ttu-id="907e0-134">두 개의 MFA 설치 대화 상자가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-134">Two MFA setup dialog boxes might appear.</span></span> <span data-ttu-id="907e0-135">이 일회성 작업은 MFA 관리자 설정에 따라 다르므로 선택적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-135">This one time operation depends on the MFA administrator setting, and therefore may be optional.</span></span> <span data-ttu-id="907e0-136">MFA 사용 도메인의 경우 이 단계는 경우에 따라 미리 정의됩니다(예를 들어 도메인은 사용자에게 스마트 카드와 핀을 사용하도록 요구함).</span><span class="sxs-lookup"><span data-stu-id="907e0-136">For an MFA enabled domain this step is sometimes pre-defined (for example, the domain requires users to use a smartcard and pin).</span></span>  
   ![3mfa-setup][3]  
7. <span data-ttu-id="907e0-138">두 번째 가능한 일회성 대화 상자를 사용하여 인증 방법의 세부 정보를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-138">The second possible one time dialog box allows you to select the details of your authentication method.</span></span> <span data-ttu-id="907e0-139">가능한 옵션은 관리자가 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-139">The possible options are configured by your administrator.</span></span>  
   ![4mfa-verify-1][4]  
8. <span data-ttu-id="907e0-141">Azure Active Directory는 사용자에게 확인 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-141">The Azure Active Directory sends the confirming information to you.</span></span> <span data-ttu-id="907e0-142">확인 코드를 받게되면 **확인 코드 입력** 상자에 해당 코드를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-142">When you receive the verification code, enter it into the **Enter verification code** box, and click **Sign in**.</span></span>  
   <span data-ttu-id="907e0-143">![5mfa-verify-2][5]</span><span class="sxs-lookup"><span data-stu-id="907e0-143">![5mfa-verify-2][5]</span></span>  

<span data-ttu-id="907e0-144">확인이 완료되면 SSMS는 일반적으로 가정된 유효한 자격 증명 및 방화벽 액세스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="907e0-144">When verification is complete, SSMS connects normally presuming valid credentials and firewall access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="907e0-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="907e0-145">Next steps</span></span>

* <span data-ttu-id="907e0-146">Azure SQL Database Multi-factor Authentication(MFA) 인증에 대한 개요는 [SQL 데이터베이스 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](sql-database-ssms-mfa-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e0-146">For an overview of Azure SQL Database multi-factor authentication, see Universal Authentication with [SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>
* <span data-ttu-id="907e0-147">데이터베이스에 대한 액세스를 부여합니다. [SQL Database 인증 및 권한 부여: 액세스 부여](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="907e0-147">Grant others access to your database: [SQL Database Authentication and Authorization: Granting Access](sql-database-manage-logins.md)</span></span>  
<span data-ttu-id="907e0-148">방화벽을 통해 연결할 수 있는지 확인합니다. [Azure Portal을 사용하여 Azure SQL Database 서버 수준 방화벽 규칙 구성](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="907e0-148">Make sure others can connect through the firewall: [Configure an Azure SQL Database server-level firewall rule using the Azure portal](sql-database-configure-firewall-settings.md)</span></span>


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

