---
title: "Azure Active Directory 인증 구성 - SQL | Microsoft Docs"
description: "Azure Active Directory 인증을 사용하여 SQL Database 및 SQL Data Warehouse에 연결하는 방법을 알아봅니다."
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
ms.openlocfilehash: 61a52813769891aa63373437e9300d4f8f47fab2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a><span data-ttu-id="acb06-103">SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="acb06-103">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span></span>

<span data-ttu-id="acb06-104">이 문서에서는 Azure AD를 만들고 채운 후 Azure SQL Database 및 SQL Data Warehouse에서 Azure AD를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-104">This article shows you how to create and populate Azure AD, and then use Azure AD with Azure SQL Database and SQL Data Warehouse.</span></span> <span data-ttu-id="acb06-105">개요는 [Azure Active Directory 인증](sql-database-aad-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-105">For an overview, see [Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>

>  [!NOTE]  
>  <span data-ttu-id="acb06-106">Azure VM에서 실행되는 SQL Server에 연결하는 경우 Azure Active Directory 계정은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-106">Connecting to SQL Server running on an Azure VM is not supported using an Azure Active Directory account.</span></span> <span data-ttu-id="acb06-107">대신 도메인 Active Directory 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-107">Use a domain Active Directory account instead.</span></span>

## <a name="create-and-populate-an-azure-ad"></a><span data-ttu-id="acb06-108">Azure AD 만들기 및 채우기</span><span class="sxs-lookup"><span data-stu-id="acb06-108">Create and populate an Azure AD</span></span>
<span data-ttu-id="acb06-109">Azure AD를 만들고 사용자 및 그룹으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-109">Create an Azure AD and populate it with users and groups.</span></span> <span data-ttu-id="acb06-110">Azure AD는 최초의 Azure AD 관리 도메인일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-110">Azure AD can be the initial domain Azure AD managed domain.</span></span> <span data-ttu-id="acb06-111">Azure AD는 Azure AD와 페더레이션된 온-프레미스 Active Directory Domain Services일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-111">Azure AD can also be an on-premises Active Directory Domain Services that is federated with the Azure AD.</span></span>

<span data-ttu-id="acb06-112">자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](../active-directory/active-directory-aadconnect.md), [Azure AD에 고유한 도메인 이름 추가](../active-directory/active-directory-add-domain.md), [이제 Microsoft Azure에서 Windows Server Active Directory와의 페더레이션 지원](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Azure AD 디렉터리 관리](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Windows PowerShell을 사용한 Azure AD 관리](/powershell/azure/overview?view=azureadps-2.0) 및 [포트 및 프로토콜이 필요한 하이브리드 ID](../active-directory/active-directory-aadconnect-ports.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-112">For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Manage Azure AD using Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), and [Hybrid Identity Required Ports and Protocols](../active-directory/active-directory-aadconnect-ports.md).</span></span>

## <a name="optional-associate-or-change-the-active-directory-that-is-currently-associated-with-your-azure-subscription"></a><span data-ttu-id="acb06-113">옵션: 현재 Azure 구독과 연결된 Active Directory를 연결하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-113">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
<span data-ttu-id="acb06-114">조직에서 Azure AD 디렉터리에 데이터베이스를 연결하려면 해당 디렉터리가 데이터베이스를 호스팅하는 Azure 구독에서 신뢰할 수 있는 디렉터리여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-114">To associate your database with the Azure AD directory for your organization, make the directory a trusted directory for the Azure subscription hosting the database.</span></span> <span data-ttu-id="acb06-115">자세한 내용은 [Azure 구독과 Azure AD의 연관 관계](https://msdn.microsoft.com/library/azure/dn629581.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-115">For more information, see [How Azure subscriptions are associated with Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).</span></span>

<span data-ttu-id="acb06-116">**추가 정보:** 모든 Azure 구독은 Azure AD 인스턴스와 트러스트 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-116">**Additional information:** Every Azure subscription has a trust relationship with an Azure AD instance.</span></span> <span data-ttu-id="acb06-117">이는 Azure 구독이 사용자, 서비스, 장치를 인증하는 해당 디렉터리를 신뢰함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-117">This means that it trusts that directory to authenticate users, services, and devices.</span></span> <span data-ttu-id="acb06-118">여러 구독에서 동일한 디렉터리를 신뢰할 수 있지만 구독은 하나의 디렉터리만 신뢰합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-118">Multiple subscriptions can trust the same directory, but a subscription trusts only one directory.</span></span> <span data-ttu-id="acb06-119">[https://manage.windowsazure.com/](https://manage.windowsazure.com/) 의 **설정** 탭에서 구독이 신뢰하는 디렉터리를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-119">You can see which directory is trusted by your subscription under the **Settings** tab at [https://manage.windowsazure.com/](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="acb06-120">구독이 디렉터리와 갖는 이 트러스트 관계는 구독이 Azure의 다른 모든 리소스(웹 사이트, 데이터베이스 등)와 갖는 관계와 다르며 구독의 하위 리소스와 더 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-120">This trust relationship that a subscription has with a directory is unlike the relationship that a subscription has with all other resources in Azure (websites, databases, and so on), which are more like child resources of a subscription.</span></span> <span data-ttu-id="acb06-121">구독이 만료되면 구독과 연결된 다른 리소스에 대한 액세스도 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-121">If a subscription expires, then access to those other resources associated with the subscription also stops.</span></span> <span data-ttu-id="acb06-122">하지만 디렉터리는 Azure에 남아 있으며 해당 디렉터리와 다른 구독을 연결하여 디렉터리 사용자를 계속 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-122">But the directory remains in Azure, and you can associate another subscription with that directory and continue to manage the directory users.</span></span> <span data-ttu-id="acb06-123">리소스에 대한 자세한 내용은 [Azure의 리소스 액세스 이해](https://msdn.microsoft.com/library/azure/dn584083.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-123">For more information about resources, see [Understanding resource access in Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).</span></span>

<span data-ttu-id="acb06-124">다음 절차는 특정 구독에 대해 연결된 디렉터리를 변경하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-124">The following procedures show you how to change the associated directory for a given subscription.</span></span>
1. <span data-ttu-id="acb06-125">Azure 구독 관리자를 통해 [Azure 클래식 포털](https://manage.windowsazure.com/) 에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-125">Connect to your [Azure Classic Portal](https://manage.windowsazure.com/) by using an Azure subscription administrator.</span></span>
2. <span data-ttu-id="acb06-126">왼쪽 배너에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-126">On the left banner, select **SETTINGS**.</span></span>
3. <span data-ttu-id="acb06-127">구독이 설정 화면에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-127">Your subscriptions appear in the settings screen.</span></span> <span data-ttu-id="acb06-128">원하는 구독이 나타나지 않으면 위쪽의 **구독**을 클릭하고 **디렉터리로 필터링** 상자를 드롭다운하여 구독이 포함된 디렉터리를 선택한 다음 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-128">If the desired subscription does not appear, click **Subscriptions** at the top, drop down the **FILTER BY DIRECTORY** box and select the directory that contains your subscriptions, and then click **APPLY**.</span></span>
   
    ![구독 선택][4]
4. <span data-ttu-id="acb06-130">**설정** 영역에서 구독을 클릭하고 페이지 아래쪽의 **디렉터리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-130">In the **settings** area, click your subscription, and then click  **EDIT DIRECTORY** at the bottom of the page.</span></span>
   
    ![ad-settings-portal][5]
5. <span data-ttu-id="acb06-132">**디렉터리 편집** 상자에서 SQL Server 또는 SQL Data Warehouse와 연결된 Azure Active Directory를 선택하고 다음 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-132">In the **EDIT DIRECTORY** box, select the Azure Active Directory that is associated with your SQL Server or SQL Data Warehouse, and then click the arrow for next.</span></span>
   
    ![edit-directory-select][6]
6. <span data-ttu-id="acb06-134">**확인** 디렉터리 매핑 대화 상자에서 "**모든 공동 관리자가 제거됩니다.**"를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-134">In the **CONFIRM** directory Mapping dialog box, confirm that "**All co-administrators will be removed.**"</span></span>
   
    ![edit-directory-confirm][7]
7. <span data-ttu-id="acb06-136">확인을 클릭하여 포털을 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-136">Click the check to reload the portal.</span></span>

   > [!NOTE]
   > <span data-ttu-id="acb06-137">디렉터리를 변경하면 모든 공동 관리자, Azure AD 사용자 및 그룹, 디렉터리 기반 리소스 사용자에 대한 액세스가 제거되며 더 이상 이 구독 또는 관련 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-137">When you change the directory, access to all co-administrators, Azure AD users and groups, and directory-backed resource users are removed and they no longer have access to this subscription or its resources.</span></span> <span data-ttu-id="acb06-138">서비스 관리자 본인만 새 디렉터리를 기반으로 하는 주체에 대한 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-138">Only you, as a service administrator, can configure access for principals based on the new directory.</span></span> <span data-ttu-id="acb06-139">이 변경이 모든 리소스에 전파되는 데는 상당한 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-139">This change might take a substantial amount of time to propagate to all resources.</span></span> <span data-ttu-id="acb06-140">디렉터리를 변경하면 SQL 데이터베이스 및 SQL Data Warehouse에 대한 Azure AD 관리자도 변경되며 기존 Azure AD 사용자의 데이터베이스 액세스가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-140">Changing the directory, also changes the Azure AD administrator for SQL Database and SQL Data Warehouse and disallow database access for any existing Azure AD users.</span></span> <span data-ttu-id="acb06-141">Azure AD 관리자를 재설정하고(아래 설명 참조) 새 Azure AD 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-141">The Azure AD admin must be reset (as described below) and new Azure AD users must be created.</span></span>
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a><span data-ttu-id="acb06-142">Azure SQL Server에 대한 Azure AD 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="acb06-142">Create an Azure AD administrator for Azure SQL server</span></span>
<span data-ttu-id="acb06-143">각각의 Azure SQL Server(SQL Database 또는 SQL Data Warehouse를 호스트하는)는 전체 Azure SQL Server의 관리자인 단일 서버 관리자 계정으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-143">Each Azure SQL server (which hosts a SQL Database or SQL Data Warehouse) starts with a single server administrator account that is the administrator of the entire Azure SQL server.</span></span> <span data-ttu-id="acb06-144">Azure AD 계정인 두 번째 SQL Server 관리자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-144">A second SQL Server administrator must be created, that is an Azure AD account.</span></span> <span data-ttu-id="acb06-145">이 주체는 마스터 데이터베이스에 포함된 데이터베이스 사용자로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-145">This principal is created as a contained database user in the master database.</span></span> <span data-ttu-id="acb06-146">관리자인 서버 관리자 계정은 모든 사용자 데이터베이스에서 **db_owner** 역할의 멤버이며 각 사용자 데이터베이스에 **dbo** 사용자로 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-146">As administrators, the server administrator accounts are members of the **db_owner** role in every user database, and enter each user database as the **dbo** user.</span></span> <span data-ttu-id="acb06-147">서버 관리자 계정에 대한 자세한 내용은 [Azure SQL Database에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-147">For more information about the server administrator accounts, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="acb06-148">Azure Active Directory와 함께 지역에서 복제를 사용할 때 Azure Active Directory 관리자는 주 서버와 보조 서버 모두에 대해 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-148">When using Azure Active Directory with geo-replication, the Azure Active Directory administrator must be configured for both the primary and the secondary servers.</span></span> <span data-ttu-id="acb06-149">서버에 Azure Active Directory 관리자가 없는 경우 다음 Azure Active Directory 로그인 및 사용자는 서버에 "연결할 수 없음" 오류를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-149">If a server does not have an Azure Active Directory administrator, then Azure Active Directory logins and users receive a "Cannot connect" to server error.</span></span>

> [!NOTE]
> <span data-ttu-id="acb06-150">Azure AD 계정을 기반으로 하지 않는 사용자(Azure SQL Server 관리자 계정 포함)는 Azure AD에서 제안된 데이터베이스 사용자에 대한 유효성 검사 권한이 없으므로 Azure AD 기반 사용자를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-150">Users that are not based on an Azure AD account (including the Azure SQL server administrator account), cannot create Azure AD-based users, because they do not have permission to validate proposed database users with the Azure AD.</span></span>
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a><span data-ttu-id="acb06-151">Azure SQL Server에 대한 Azure Active Directory 관리자를 프로비전합니다</span><span class="sxs-lookup"><span data-stu-id="acb06-151">Provision an Azure Active Directory administrator for your Azure SQL server</span></span>

<span data-ttu-id="acb06-152">다음 두 절차는 Azure Portal에서나 PowerShell을 사용하여 Azure SQL Server에 대한 Azure Active Directory 관리자를 프로비전하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-152">The following two procedures show you how to provision an Azure Active Directory administrator for your Azure SQL server in the Azure portal and by using PowerShell.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="acb06-153">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="acb06-153">Azure portal</span></span>
1. <span data-ttu-id="acb06-154">[Azure Portal](https://portal.azure.com/)의 상단 오른쪽 끝에서 해당 연결을 클릭하여 가능한 Active Directory 목록을 드롭다운합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-154">In the [Azure portal](https://portal.azure.com/), in the upper-right corner, click your connection to drop down a list of possible Active Directories.</span></span> <span data-ttu-id="acb06-155">정확한 Active Directory를 기본 Azure AD로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-155">Choose the correct Active Directory as the default Azure AD.</span></span> <span data-ttu-id="acb06-156">이 단계는 구독 연결을 Azure SQL Server의 Active Directory와 연결하여 동일한 구독이 두 Azure AD 및 SQL Server에 사용되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-156">This step links the subscription association with Active Directory with Azure SQL server making sure that the same subscription is used for both Azure AD and SQL Server.</span></span> <span data-ttu-id="acb06-157">(Azure SQL Server는 Azure SQL Database 또는 Azure SQL Data Warehouse에서 호스트할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="acb06-157">(The Azure SQL server can be hosting either Azure SQL Database or Azure SQL Data Warehouse.)</span></span>   
    <span data-ttu-id="acb06-158">![choose-ad][8]</span><span class="sxs-lookup"><span data-stu-id="acb06-158">![choose-ad][8]</span></span>   
    
2. <span data-ttu-id="acb06-159">왼쪽 배너에서 **SQL Server**와 해당 **SQL Server**를 선택한 다음 **SQL Server** 블레이드에서 **Active Directory 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-159">In the left banner select **SQL servers**, select your **SQL server**, and then in the **SQL Server** blade, click **Active Directory admin**.</span></span>   
3. <span data-ttu-id="acb06-160">**Active Directory 관리자** 블레이드에서 **관리자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-160">In the **Active Directory admin** blade, click **Set admin**.</span></span>   
    <span data-ttu-id="acb06-161">![active directory 선택](./media/sql-database-aad-authentication/select-active-directory.png)</span><span class="sxs-lookup"><span data-stu-id="acb06-161">![select active directory](./media/sql-database-aad-authentication/select-active-directory.png)</span></span>  
    
4. <span data-ttu-id="acb06-162">**관리자 추가** 블레이드에서 사용자를 검색하고 관리자가 될 사용자 또는 그룹을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-162">In the **Add admin** blade, search for a user, select the user or group to be an administrator, and then click **Select**.</span></span> <span data-ttu-id="acb06-163">Active Directory 관리 블레이드에 해당 Active Directory에 모든 멤버와 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-163">(The Active Directory admin blade shows all members and groups of your Active Directory.</span></span> <span data-ttu-id="acb06-164">회색으로 표시된 사용자나 그룹은 Azure AD 관리자로 지원되지 않기 때문에 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-164">Users or groups that are grayed out cannot be selected because they are not supported as Azure AD administrators.</span></span> <span data-ttu-id="acb06-165">[SQL Database 및 SQL Data Warehouse에서 인증을 위해 Azure Active Directory 인증 사용](sql-database-aad-authentication.md)의 **Azure AD 기능 및 제한 사항** 섹션에서 지원되는 관리자 목록을 참조하세요. 역할 기반 액세스 제어(RBAC)는 포털에만 적용되며 SQL Server에 전파되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-165">(See the list of supported admins in the **Azure AD Features and Limitations** section of [Use Azure Active Directory Authentication for authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication.md).) Role-based access control (RBAC) applies only to the portal and is not propagated to SQL Server.</span></span>   
    <span data-ttu-id="acb06-166">![관리자 선택](./media/sql-database-aad-authentication/select-admin.png)</span><span class="sxs-lookup"><span data-stu-id="acb06-166">![select admin](./media/sql-database-aad-authentication/select-admin.png)</span></span>  
    
5. <span data-ttu-id="acb06-167">**Active directory 관리자** 블레이드 위쪽에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-167">At the top of the **Active Directory admin** blade, click **SAVE**.</span></span>   
    <span data-ttu-id="acb06-168">![관리자 저장](./media/sql-database-aad-authentication/save-admin.png)</span><span class="sxs-lookup"><span data-stu-id="acb06-168">![save admin](./media/sql-database-aad-authentication/save-admin.png)</span></span>   

<span data-ttu-id="acb06-169">관리자 변경 과정에는 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-169">The process of changing the administrator may take several minutes.</span></span> <span data-ttu-id="acb06-170">그런 다음 새 관리자가 **Active Directory 관리자** 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-170">Then the new administrator appears in the **Active Directory admin** box.</span></span>

   > [!NOTE]
   > <span data-ttu-id="acb06-171">Azure AD 관리자를 설정하는 경우, 새 관리자 이름(사용자 또는 그룹)이 SQL Server 인증 사용자로 가상 master 데이터베이스에 있으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-171">When setting up the Azure AD admin, the new admin name (user or group) cannot already be present in the virtual master database as a SQL Server authentication user.</span></span> <span data-ttu-id="acb06-172">새 관리자 이름이 있으면 Azure AD 관리자 설정은 실패하며, 생성 작업을 롤백하고 해당 관리자(이름)이 이미 존재한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-172">If present, the Azure AD admin setup will fail; rolling back its creation and indicating that such an admin (name) already exists.</span></span> <span data-ttu-id="acb06-173">SQL Server 인증 사용자는 Azure AD에 속하지 않기 때문에 Azure AD 인증을 사용하여 서버에 연결하려는 작업은 모두 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-173">Since such a SQL Server authentication user is not part of the Azure AD, any effort to connect to the server using Azure AD authentication fails.</span></span>
   > 


<span data-ttu-id="acb06-174">나중에 관리자를 제거하려면, **Active Directory 관리자** 블레이드 위쪽에서 **관리자 제거**를 클릭하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-174">To later remove an Admin, at the top of the **Active Directory admin** blade, click **Remove admin**, and then click **Save**.</span></span>

### <a name="powershell"></a><span data-ttu-id="acb06-175">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acb06-175">PowerShell</span></span>
<span data-ttu-id="acb06-176">PowerShell cmdlet을 실행하려면 Azure powershell을 설치하고 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-176">To run PowerShell cmdlets, you need to have Azure PowerShell installed and running.</span></span> <span data-ttu-id="acb06-177">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-177">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="acb06-178">Azure AD 관리자를 프로비전하려면 다음 Azure PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-178">To provision an Azure AD admin, execute the following Azure PowerShell commands:</span></span>

* <span data-ttu-id="acb06-179">Add-AzureRmAccount</span><span class="sxs-lookup"><span data-stu-id="acb06-179">Add-AzureRmAccount</span></span>
* <span data-ttu-id="acb06-180">Select-AzureRmSubscription</span><span class="sxs-lookup"><span data-stu-id="acb06-180">Select-AzureRmSubscription</span></span>

<span data-ttu-id="acb06-181">Azure AD 관리자 프로비전 및 관리에 사용되는 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="acb06-181">Cmdlets used to provision and manage Azure AD admin:</span></span>

| <span data-ttu-id="acb06-182">Cmdlet 이름</span><span class="sxs-lookup"><span data-stu-id="acb06-182">Cmdlet name</span></span> | <span data-ttu-id="acb06-183">설명</span><span class="sxs-lookup"><span data-stu-id="acb06-183">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="acb06-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="acb06-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="acb06-185">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-185">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="acb06-186">(현재 구독 설정에서 수행되어야 함).</span><span class="sxs-lookup"><span data-stu-id="acb06-186">(Must be from the current subscription.)</span></span> |
| [<span data-ttu-id="acb06-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="acb06-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="acb06-188">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-188">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
| [<span data-ttu-id="acb06-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="acb06-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="acb06-190">현재 Azure SQL Server 또는 Azure SQL Data Warehouse에 대해 구성된 Azure Active Directory 관리자에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-190">Returns information about an Azure Active Directory administrator currently configured for the Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="acb06-191">각 명령에 대한 자세한 내용을 확인하려면 PowerShell 명령 get-help를 사용합니다(예: ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``).</span><span class="sxs-lookup"><span data-stu-id="acb06-191">Use PowerShell command get-help to see more details for each of these commands, for example ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.</span></span>

<span data-ttu-id="acb06-192">다음 스크립트는 리소스 그룹 **Group-23**에서 **demo_server** 서버에 대해 이름이 **DBA_Group**(개체 ID `40b79501-b343-44ed-9ce7-da4c8cc7353f`)인 Azure AD 관리자 그룹을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-192">The following script provisions an Azure AD administrator group named **DBA_Group** (object id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) for the **demo_server** server in a resource group named **Group-23**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

<span data-ttu-id="acb06-193">**DisplayName** 입력 매개 변수에는 Azure AD 표시 이름이나 사용자 계정 이름이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-193">The **DisplayName** input parameter accepts either the Azure AD display name or the User Principal Name.</span></span> <span data-ttu-id="acb06-194">예를 들어 ``DisplayName="John Smith"`` 또는 ``DisplayName="johns@contoso.com"``입니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-194">For example, ``DisplayName="John Smith"`` and ``DisplayName="johns@contoso.com"``.</span></span> <span data-ttu-id="acb06-195">Azure AD 그룹에는 Azure AD 표시 이름만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-195">For Azure AD groups only the Azure AD display name is supported.</span></span>

> [!NOTE]
> <span data-ttu-id="acb06-196">Azure PowerShell 명령 ```Set-AzureRmSqlServerActiveDirectoryAdministrator```는 지원되지 않는 사용자에 대한 Azure AD 관리자 프로비전을 차단하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-196">The Azure PowerShell  command ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` does not prevent you from provisioning Azure AD admins for unsupported users.</span></span> <span data-ttu-id="acb06-197">지원되지 않는 사용자를 프로비전할 수는 있지만 데이터베이스에 연결할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-197">An unsupported user can be provisioned, but can not connect to a database.</span></span> 
> 

<span data-ttu-id="acb06-198">다음 예제에서는 **ObjectID**옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-198">The following example uses the optional **ObjectID**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> <span data-ttu-id="acb06-199">**DisplayName**이 고유하지 않을 경우 Azure AD **ObjectID**가 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-199">The Azure AD **ObjectID** is required when the **DisplayName** is not unique.</span></span> <span data-ttu-id="acb06-200">**ObjectID** 및 **DisplayName** 값을 검색하려면 Azure 클래식 포털의 Active Directory 섹션을 사용하고 사용자 또는 그룹의 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-200">To retrieve the **ObjectID** and **DisplayName** values, use the Active Directory section of Azure Classic Portal, and view the properties of a user or group.</span></span>
> 

<span data-ttu-id="acb06-201">다음 예제에서는 Azure SQL Server에 대해 현재 Azure AD 관리자 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-201">The following example returns information about the current Azure AD admin for Azure SQL server:</span></span>

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

<span data-ttu-id="acb06-202">다음 예제에서는 Azure AD 관리자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-202">The following example removes an Azure AD administrator:</span></span>

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

<span data-ttu-id="acb06-203">REST API를 사용하여 Azure Active Directory 관리자를 프로비전할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-203">You can also provision an Azure Active Directory Administrator by using the REST APIs.</span></span> <span data-ttu-id="acb06-204">자세한 내용은 [서비스 관리 REST API 참조 및 Azure SQL 데이터베이스에 대한 작업](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span><span class="sxs-lookup"><span data-stu-id="acb06-204">For more information, see [Service Management REST API Reference and Operations for Azure SQL Databases Operations for Azure SQL Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span></span>

### <a name="cli"></a><span data-ttu-id="acb06-205">CLI</span><span class="sxs-lookup"><span data-stu-id="acb06-205">CLI</span></span>  
<span data-ttu-id="acb06-206">또한 다음 CLI 명령을 호출하여 Azure AD 관리자를 구축할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-206">You can also provision an Azure AD admin by calling the following CLI commands:</span></span>
| <span data-ttu-id="acb06-207">명령</span><span class="sxs-lookup"><span data-stu-id="acb06-207">Command</span></span> | <span data-ttu-id="acb06-208">설명</span><span class="sxs-lookup"><span data-stu-id="acb06-208">Description</span></span> |
| --- | --- |
|[<span data-ttu-id="acb06-209">az sql server ad-admin create</span><span class="sxs-lookup"><span data-stu-id="acb06-209">az sql server ad-admin create</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |<span data-ttu-id="acb06-210">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-210">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="acb06-211">(현재 구독 설정에서 수행되어야 함).</span><span class="sxs-lookup"><span data-stu-id="acb06-211">(Must be from the current subscription.)</span></span> |
|[<span data-ttu-id="acb06-212">az sql server ad-admin delete</span><span class="sxs-lookup"><span data-stu-id="acb06-212">az sql server ad-admin delete</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |<span data-ttu-id="acb06-213">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-213">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="acb06-214">az sql server ad-admin list</span><span class="sxs-lookup"><span data-stu-id="acb06-214">az sql server ad-admin list</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |<span data-ttu-id="acb06-215">현재 Azure SQL Server 또는 Azure SQL Data Warehouse에 대해 구성된 Azure Active Directory 관리자에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-215">Returns information about an Azure Active Directory administrator currently configured for the Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="acb06-216">az sql server ad-admin update</span><span class="sxs-lookup"><span data-stu-id="acb06-216">az sql server ad-admin update</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |<span data-ttu-id="acb06-217">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-217">Updates the Active Directory administrator for an Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="acb06-218">CLI 명령에 대한 자세한 내용은 [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-218">For more information about CLI commands, see [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).</span></span>  


## <a name="configure-your-client-computers"></a><span data-ttu-id="acb06-219">클라이언트 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="acb06-219">Configure your client computers</span></span>
<span data-ttu-id="acb06-220">모든 클라이언트 컴퓨터에서 Azure AD를 사용하여 Azure SQL 데이터베이스 또는 Azure SQL Data Warehouse에 연결하는 응용 프로그램 또는 사용자를 통해 다음 소프트웨어를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-220">On all client machines, from which your applications or users connect to Azure SQL Database or Azure SQL Data Warehouse using Azure AD identities, you must install the following software:</span></span>

* <span data-ttu-id="acb06-221">.NET Framework 4.6 이상, [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx)</span><span class="sxs-lookup"><span data-stu-id="acb06-221">.NET Framework 4.6 or later from [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>
* <span data-ttu-id="acb06-222">SQL Server용 Azure Active Directory 인증 라이브러리(**ADALSQL.DLL**)는 다운로드 센터( [Microsoft SQL Server용 Microsoft Active Directory 인증 라이브러리)](http://www.microsoft.com/download/details.aspx?id=48742)에서 여러 언어로 제공됩니다(x86 및 amd64 모두 해당).</span><span class="sxs-lookup"><span data-stu-id="acb06-222">Azure Active Directory Authentication Library for SQL Server (**ADALSQL.DLL**) is available in multiple languages (both x86 and amd64) from the download center at [Microsoft Active Directory Authentication Library for Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).</span></span>

<span data-ttu-id="acb06-223">다음을 통해 이러한 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-223">You can meet these requirements by:</span></span>

* <span data-ttu-id="acb06-224">[SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 또는 [SQL Server Data Tools for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx)를 설치하면 .NET Framework 4.6 요구 사항에 부합합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-224">Installing either [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) or [SQL Server Data Tools for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) meets the .NET Framework 4.6 requirement.</span></span>
* <span data-ttu-id="acb06-225">SSMS이 x86 버전의 **ADALSQL.DLL**을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-225">SSMS installs the x86 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="acb06-226">SSDT가 amd64 버전의 **ADALSQL.DLL**을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-226">SSDT installs the amd64 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="acb06-227">[Visual Studio 다운로드](https://www.visualstudio.com/downloads/download-visual-studio-vs) 의 최신 Visual Studio는 .NET Framework 4.6 요구 사항을 만족하지만, 필요한 amd64 버전의 **ADALSQL.DLL**을 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-227">The latest Visual Studio from [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) meets the .NET Framework 4.6 requirement, but does not install the required amd64 version of **ADALSQL.DLL**.</span></span>

## <a name="create-contained-database-users-in-your-database-mapped-to-azure-ad-identities"></a><span data-ttu-id="acb06-228">Azure AD ID에 매핑된 데이터베이스에서 포함된 데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="acb06-228">Create contained database users in your database mapped to Azure AD identities</span></span>

<span data-ttu-id="acb06-229">Azure Active Directory 인증에는 포함된 데이터베이스 사용자로 만들 데이터베이스 사용자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-229">Azure Active Directory authentication requires database users to be created as contained database users.</span></span> <span data-ttu-id="acb06-230">Azure AD ID를 기반으로 하는 포함된 데이터베이스 사용자는 마스터 데이터베이스에 로그인이 없는 데이터베이스 사용자이며, 데이터베이스와 연결된 Azure AD 디렉터리의 ID에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-230">A contained database user based on an Azure AD identity, is a database user that does not have a login in the master database, and which maps to an identity in the Azure AD directory that is associated with the database.</span></span> <span data-ttu-id="acb06-231">Azure AD ID는 개별 사용자 계정 또는 그룹일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-231">The Azure AD identity can be either an individual user account or a group.</span></span> <span data-ttu-id="acb06-232">포함된 데이터베이스 사용자에 대한 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-232">For more information about contained database users, see [Contained Database Users- Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="acb06-233">데이터베이스 사용자(관리자 예외)는 포털을 사용하여 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-233">Database users (with the exception of administrators) cannot be created using portal.</span></span> <span data-ttu-id="acb06-234">RBAC 역할은 SQL Server, SQL 데이터베이스 또는SQL Data Warehouse에 전파되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-234">RBAC roles are not propagated to SQL Server, SQL Database, or SQL Data Warehouse.</span></span> <span data-ttu-id="acb06-235">Azure RBAC 역할은 Azure 리소스 관리에 사용되며 데이터베이스 사용 권한에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-235">Azure RBAC roles are used for managing Azure Resources, and do not apply to database permissions.</span></span> <span data-ttu-id="acb06-236">예를 들어 **SQL Server 참여자** 역할은 SQL 데이터베이스 또는 SQL Data Warehouse에 연결 권한을 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-236">For example, the **SQL Server Contributor** role does not grant access to connect to the SQL Database or SQL Data Warehouse.</span></span> <span data-ttu-id="acb06-237">TRANSACT-SQL 문을 사용하여 데이터베이스에 직접 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-237">The access permission must be granted directly in the database using Transact-SQL statements.</span></span>
>

<span data-ttu-id="acb06-238">Azure AD 기반의 포함된 데이터베이스 사용자(데이터베이스를 소유한 서버 관리자 아님)를 만들려면 **ALTER ANY USER** 이상의 권한이 있는 사용자인 Azure AD ID를 통해 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-238">To create an Azure AD-based contained database user (other than the server administrator that owns the database), connect to the database with an Azure AD identity, as a user with at least the **ALTER ANY USER** permission.</span></span> <span data-ttu-id="acb06-239">그런 다음 아래 TRANSACT-SQL 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-239">Then use the following Transact-SQL syntax:</span></span>

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="acb06-240">*Azure_AD_principal_name*은 Azure AD 사용자의 사용자 계정 이름이거나 Azure AD 그룹의 표시 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-240">*Azure_AD_principal_name* can be the user principal name of an Azure AD user or the display name for an Azure AD group.</span></span>

<span data-ttu-id="acb06-241">**예:** Azure AD 페더레이션 또는 관리 도메인 사용자를 나타내는 포함된 데이터베이스 사용자를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="acb06-241">**Examples:** To create a contained database user representing an Azure AD federated or managed domain user:</span></span>
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="acb06-242">Azure AD 또는 페더레이션 도메인 그룹을 나타내는 포함된 데이터베이스 사용자를 만들려면 보안 그룹의 표시 이름을 제공하십시오.</span><span class="sxs-lookup"><span data-stu-id="acb06-242">To create a contained database user representing an Azure AD or federated domain group, provide the display name of a security group:</span></span>
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="acb06-243">Azure AD 토큰을 사용하여 연결할 응용 프로그램을 나타내는 포함된 데이터베이스 사용자를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-243">To create a contained database user representing an application that connects using an Azure AD token:</span></span>

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  <span data-ttu-id="acb06-244">Azure 구독과 연결된 Azure Active Directory 이외의 Azure Active Directory에서 사용자를 직접 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-244">You cannot directly create a user from an Azure Active Directory other than the Azure Active Directory that is associated with your Azure subscription.</span></span> <span data-ttu-id="acb06-245">그러나 연결된 Active Directory에서 가져온 사용자(외부 사용자로 알려짐)인 다른 Active Directory의 멤버는 테넌트 Active Directory의 Active Directory 그룹에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-245">However, members of other Active Directories that are imported users in the associated Active Directory (known as external users) can be added to an Active Directory group in the tenant Active Directory.</span></span> <span data-ttu-id="acb06-246">해당 AD 그룹에 대해 포함된 데이터베이스 사용자를 만들면 외부 Active Directory의 사용자는 SQL Database에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-246">By creating a contained database user for that AD group, the users from the external Active Directory can gain access to SQL Database.</span></span>   

<span data-ttu-id="acb06-247">Azure Active Directory 기반의 포함된 데이터베이스 사용자 만들기와 관련한 자세한 내용은 [CREATE USER(Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-247">For more information about creating contained database users based on Azure Active Directory identities, see [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="acb06-248">Azure SQL Server에 대한 Azure Active Directory 관리자를 제거하면 Azure AD 인증 사용자가 서버에 연결되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-248">Removing the Azure Active Directory administrator for Azure SQL server prevents any Azure AD authentication user from connecting to the server.</span></span> <span data-ttu-id="acb06-249">필요한 경우 사용할 수 없는 Azure AD 사용자는 SQL 데이터베이스 관리자가 수동으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-249">If necessary, unusable Azure AD users can be dropped manually by a SQL Database administrator.</span></span>   

>  [!NOTE]
>  <span data-ttu-id="acb06-250">**연결 시간 초과 만료됨**을 수신하면 연결 문자열의 `TransparentNetworkIPResolution` 매개 변수를 false로 설정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-250">If you receive a **Connection Timeout Expired**, you may need to set the `TransparentNetworkIPResolution` parameter of the connection string to false.</span></span> <span data-ttu-id="acb06-251">자세한 내용은 [.NET Framework 4.6.1의 연결 시간 초과 문제 – TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-251">For more information, see [Connection timeout issue with .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).</span></span>   

   
<span data-ttu-id="acb06-252">데이터베이스 사용자를 만들 때 해당 사용자는 **연결** 권한을 부여 받으며 **공용** 역할의 멤버로서 해당 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-252">When you create a database user, that user receives the **CONNECT** permission and can connect to that database as a member of the **PUBLIC** role.</span></span> <span data-ttu-id="acb06-253">처음에 이 사용자에게 제공되는 권한은 **공용** 역할에 부여된 권한이거나 사용자가 속해 있는 Windows 그룹에 부여된 권한 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-253">Initially the only permissions available to the user are any permissions granted to the **PUBLIC** role, or any permissions granted to any Windows groups that they are a member of.</span></span> <span data-ttu-id="acb06-254">Azure AD 기반의 포함된 데이터베이스 사용자를 프로비전한 후에는 다른 사용자 유형에 권한을 부여하는 것과 같은 방식으로 이 사용자에게 추가 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-254">Once you provision an Azure AD-based contained database user, you can grant the user additional permissions, the same way as you grant permission to any other type of user.</span></span> <span data-ttu-id="acb06-255">일반적으로 데이터베이스 역할에 권한을 부여하고 역할에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-255">Typically grant permissions to database roles, and add users to roles.</span></span> <span data-ttu-id="acb06-256">자세한 내용은 [데이터베이스 엔진의 권한 기초](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-256">For more information, see [Database Engine Permission Basics](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx).</span></span> <span data-ttu-id="acb06-257">특수 SQL 데이터베이스 역할에 대한 자세한 내용은 [Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-257">For more information about special SQL Database roles, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="acb06-258">관리 도메인에 가져온 페더레이션된 도메인은 관리되는 도메인 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-258">A federated domain user that is imported into a manage domain, must use the managed domain identity.</span></span>

> [!NOTE]
> <span data-ttu-id="acb06-259">Azure AD 사용자는 데이터베이스 메타데이터에서 E 형식(EXTERNAL_USER) 및 그룹의 경우 X 형식(EXTERNAL_GROUPS)으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-259">Azure AD users are marked in the database metadata with type E (EXTERNAL_USER) and for groups with type X (EXTERNAL_GROUPS).</span></span> <span data-ttu-id="acb06-260">자세한 내용은 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-260">For more information, see [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span> 
>

## <a name="connect-to-the-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a><span data-ttu-id="acb06-261">SSMS 또는 SSDT를 사용하여 사용자 데이터베이스 또는 데이터 웨어하우스에 연결</span><span class="sxs-lookup"><span data-stu-id="acb06-261">Connect to the user database or data warehouse by using SSMS or SSDT</span></span>  
<span data-ttu-id="acb06-262">Azure AD 관리자가 제대로 설정되었는지 확인하려면 Azure AD 관리자 계정을 사용하여 **master** 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-262">To confirm the Azure AD administrator is properly set up, connect to the **master** database using the Azure AD administrator account.</span></span>
<span data-ttu-id="acb06-263">Azure AD 기반의 포함된 데이터베이스 사용자(데이터베이스를 소유한 서버 관리자 아님)를 프로비전하려면 해당 데이터베이스에 대한 액세스가 있는 Azure AD ID로 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-263">To provision an Azure AD-based contained database user (other than the server administrator that owns the database), connect to the database with an Azure AD identity that has access to the database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acb06-264">Azure Active Directory 인증에 대한 지원은 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 Visual Studio 2015의 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-264">Support for Azure Active Directory authentication is available with [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) in Visual Studio 2015.</span></span> <span data-ttu-id="acb06-265">SSMS의 2016년 8월 릴리스에는 관리자가 전화 통화, 문자 메시지, PIN이 있는 스마트 카드 또는 모바일 앱 알림을 사용하여 Multi-Factor Authentication을 요구할 수 있도록 하는 Active Directory 유니버설 인증도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-265">The August 2016 release of SSMS also includes support for Active Directory Universal Authentication, which allows administrators to require Multi-Factor Authentication using a phone call, text message, smart cards with pin, or mobile app notification.</span></span>
 
## <a name="using-an-azure-ad-identity-to-connect-using-ssms-or-ssdt"></a><span data-ttu-id="acb06-266">SSMS 또는 SSDT를 사용하여 연결하는 데 Azure AD ID 사용</span><span class="sxs-lookup"><span data-stu-id="acb06-266">Using an Azure AD identity to connect using SSMS or SSDT</span></span>  

<span data-ttu-id="acb06-267">다음 절차에서는 SQL Server Management Studio 또는 SQL Server Database Tools를 사용하여 SQL Database를 Azure AD ID에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-267">The following procedures show you how to connect to a SQL database with an Azure AD identity using SQL Server Management Studio or SQL Server Database Tools.</span></span>

### <a name="active-directory-integrated-authentication"></a><span data-ttu-id="acb06-268">Active Directory 통합 인증</span><span class="sxs-lookup"><span data-stu-id="acb06-268">Active Directory integrated authentication</span></span>

<span data-ttu-id="acb06-269">페더레이션된 도메인의 Azure Active Directory 자격 증명을 사용하여 Windows에 로그인한 경우 이 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-269">Use this method if you are logged in to Windows using your Azure Active Directory credentials from a federated domain.</span></span>

1. <span data-ttu-id="acb06-270">Management Studio 또는 Data Tools를 시작하고, **서버에 연결**(또는 **데이터베이스 엔진 연결**) 대화 상자의 **인증** 상자에서 **Active Directory 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-270">Start Management Studio or Data Tools and in the **Connect to Server** (or **Connect to Database Engine**) dialog box, in the **Authentication** box, select **Active Directory - Integrated**.</span></span> <span data-ttu-id="acb06-271">연결에 대한 기존 자격 증명이 있으므로 암호 입력이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-271">No password is needed or can be entered because your existing credentials will be presented for the connection.</span></span>   

    ![AD 통합 인증 선택][11]
2. <span data-ttu-id="acb06-273">**옵션** 단추를 클릭하고 **연결 속성** 페이지의 **데이터베이스에 연결** 상자에서 연결하려는 사용자 데이터베이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-273">Click the **Options** button, and on the **Connection Properties** page, in the **Connect to database** box, type the name of the user database you want to connect to.</span></span> <span data-ttu-id="acb06-274">**AD 도메인 이름 또는 테넌트 ID** 옵션은 **MFA 연결 옵션이 있는 유니버설**에서만 지원되며 그 밖의 경우는 회색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-274">(The **AD domain name or tenant ID**” option is only supported for **Universal with MFA connection** options, otherwise it is greyed out.)</span></span>  

    ![데이터베이스 이름 선택][13]

## <a name="active-directory-password-authentication"></a><span data-ttu-id="acb06-276">Active Directory 암호 인증</span><span class="sxs-lookup"><span data-stu-id="acb06-276">Active Directory password authentication</span></span>

<span data-ttu-id="acb06-277">Azure AD 관리 도메인을 사용하여 Azure AD 사용자 이름과 연결할 때 이 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-277">Use this method when connecting with an Azure AD principal name using the Azure AD managed domain.</span></span> <span data-ttu-id="acb06-278">원격 작업 등, 도메인 액세스 없이 페더레이션된 계정에도 이 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-278">You can also use it for federated account without access to the domain, for example when working remotely.</span></span>

<span data-ttu-id="acb06-279">Azure와 페더레이션되지 않은 도메인으로부터 자격 증명을 사용하여 Windows에 로그인하거나, 최초 또는 클라이언트 도메인 기반의 Azure AD를 사용하는 Azure AD 인증을 사용할 경우 이 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-279">Use this method if you are logged in to Windows using credentials from a domain that is not federated with Azure, or when using Azure AD authentication using Azure AD based on the initial or the client domain.</span></span>

1. <span data-ttu-id="acb06-280">Management Studio 또는 Data Tools를 시작하고, **서버에 연결**(또는 **데이터베이스 엔진 연결**) 대화 상자의 **인증** 상자에서 **Active Directory - 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-280">Start Management Studio or Data Tools and in the **Connect to Server** (or **Connect to Database Engine**) dialog box, in the **Authentication** box, select **Active Directory - Password**.</span></span>
2. <span data-ttu-id="acb06-281">**사용자 이름** 상자에 **username@domain.com** 형식으로 Azure Active Directory 사용자 이름을 입력합니다. Azure Active Directory의 계정이거나, Azure Active Directory와 페더레이션된 도메인의 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-281">In the **User name** box, type your Azure Active Directory user name in the format **username@domain.com**. This must be an account from the Azure Active Directory or an account from a domain federate with the Azure Active Directory.</span></span>
3. <span data-ttu-id="acb06-282">**암호** 상자에 Azure Active Directory 계정이나 페더레이션된 도메인 계정의 사용자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-282">In the **Password** box, type your user password for the Azure Active Directory account or federated domain account.</span></span>

    ![AD 암호 인증 선택][12]
4. <span data-ttu-id="acb06-284">**옵션** 단추를 클릭하고 **연결 속성** 페이지의 **데이터베이스에 연결** 상자에서 연결하려는 사용자 데이터베이스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-284">Click the **Options** button, and on the **Connection Properties** page, in the **Connect to database** box, type the name of the user database you want to connect to.</span></span> <span data-ttu-id="acb06-285">(이전 옵션의 그래픽을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="acb06-285">(See the graphic in the previous option.)</span></span>

## <a name="using-an-azure-ad-identity-to-connect-from-a-client-application"></a><span data-ttu-id="acb06-286">클라이언트 응용 프로그램에서 연결하는 데 Azure AD ID 사용</span><span class="sxs-lookup"><span data-stu-id="acb06-286">Using an Azure AD identity to connect from a client application</span></span>

<span data-ttu-id="acb06-287">다음 절차에서는 클라이언트 응용 프로그램에서 SQL Database를 Azure AD ID에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-287">The following procedures show you how to connect to a SQL database with an Azure AD identity from a client application.</span></span>

###  <a name="active-directory-integrated-authentication"></a><span data-ttu-id="acb06-288">Active Directory 통합 인증</span><span class="sxs-lookup"><span data-stu-id="acb06-288">Active Directory integrated authentication</span></span>

<span data-ttu-id="acb06-289">Windows 통합 인증을 사용하려면 도메인의 Active Directory를 Azure Active Directory와 페더레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-289">To use integrated Windows authentication, your domain’s Active Directory must be federated with Azure Active Directory.</span></span> <span data-ttu-id="acb06-290">데이터베이스에 연결되는 클라이언트 응용 프로그램(또는 서비스)은 사용자의 도메인 자격 증명으로 도메인에 가입된 컴퓨터에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-290">Your client application (or a service) connecting to the database must be running on a domain-joined machine under a user’s domain credentials.</span></span>

<span data-ttu-id="acb06-291">통합 인증 및 Azure AD ID를 사용하여 데이터베이스에 연결하려면 데이터베이스 연결 문자열의 인증 키워드가 Active Directory 통합으로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-291">To connect to a database using integrated authentication and an Azure AD identity, the Authentication keyword in the database connection string must be set to Active Directory Integrated.</span></span> <span data-ttu-id="acb06-292">다음 C# 코드 예제에서는 ADO.NET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-292">The following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="acb06-293">연결 문자열 키워드 ``Integrated Security=True``는 Azure SQL Database 연결에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-293">The connection string keyword ``Integrated Security=True`` is not supported for connecting to Azure SQL Database.</span></span> <span data-ttu-id="acb06-294">ODBC 연결을 설정할 때는 공백을 제거하고 인증을 'ActiveDirectoryIntegrated'로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-294">When making an ODBC connection, you will need to remove spaces and set Authentication to 'ActiveDirectoryIntegrated'.</span></span>

### <a name="active-directory-password-authentication"></a><span data-ttu-id="acb06-295">Active Directory 암호 인증</span><span class="sxs-lookup"><span data-stu-id="acb06-295">Active Directory password authentication</span></span>

<span data-ttu-id="acb06-296">통합 인증 및 Azure AD ID를 사용하여 데이터베이스에 연결하려면 인증 키워드가 Active Directory 암호로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-296">To connect to a database using integrated authentication and an Azure AD identity, the Authentication keyword must be set to Active Directory Password.</span></span> <span data-ttu-id="acb06-297">연결 문자열에는 사용자 ID/UID 및 암호/PWD 키워드와 값이 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-297">The connection string must contain User ID/UID and Password/PWD keywords and values.</span></span> <span data-ttu-id="acb06-298">다음 C# 코드 예제에서는 ADO.NET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-298">The following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="acb06-299">[Azure AD 인증 GitHub 데모](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth)에서 사용할 수 있는 데모 코드 샘플을 사용한 Azure AD 인증 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-299">Learn more about Azure AD authentication methods using the demo code samples available at [Azure AD Authentication GitHub Demo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).</span></span>

## <a name="azure-ad-token"></a><span data-ttu-id="acb06-300">Azure AD 토큰</span><span class="sxs-lookup"><span data-stu-id="acb06-300">Azure AD token</span></span>
<span data-ttu-id="acb06-301">이 인증 방법을 사용하면 AAD(Azure Active Directory)에서 토큰을 가져와 Azure SQL 데이터베이스 또는 AzureSQL Data Warehouse에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-301">This authentication method allows middle-tier services to connect to Azure SQL Database or Azure SQL Data Warehouse by obtaining a token from Azure Active Directory (AAD).</span></span> <span data-ttu-id="acb06-302">이는 인증서 기반 인증을 비롯한 정교한 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-302">It enables sophisticated scenarios including certificate-based authentication.</span></span> <span data-ttu-id="acb06-303">Azure AD 토큰 인증을 사용하려면 다음 네 가지 기본 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-303">You must complete four basic steps to use Azure AD token authentication:</span></span>

1. <span data-ttu-id="acb06-304">Azure Active Directory에 응용 프로그램을 등록하고 코드에 대한 클라이언트 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-304">Register your application with Azure Active Directory and get the client id for your code.</span></span> 
2. <span data-ttu-id="acb06-305">응용 프로그램을 나타내는 데이터베이스 사용자를 만듭니다(이전</span><span class="sxs-lookup"><span data-stu-id="acb06-305">Create a database user representing the application.</span></span> <span data-ttu-id="acb06-306">6단계에서 완료).</span><span class="sxs-lookup"><span data-stu-id="acb06-306">(Completed earlier in step 6.)</span></span>
3. <span data-ttu-id="acb06-307">응용 프로그램을 실행하는 클라이언트 컴퓨터에서 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-307">Create a certificate on the client computer runs the application.</span></span>
4. <span data-ttu-id="acb06-308">인증서를 응용 프로그램의 키로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-308">Add the certificate as a key for your application.</span></span>

<span data-ttu-id="acb06-309">샘플 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="acb06-309">Sample connection string:</span></span>

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

<span data-ttu-id="acb06-310">자세한 내용은 [SQL Server 보안 블로그](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-310">For more information, see [SQL Server Security Blog](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).</span></span>

### <a name="sqlcmd"></a><span data-ttu-id="acb06-311">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="acb06-311">sqlcmd</span></span>

<span data-ttu-id="acb06-312">다음 문은 [다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=825643)에서 사용할 수 있는 sqlcmd 버전 13.1을 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acb06-312">The following statements, connect using version 13.1 of sqlcmd, which is available from the [Download Center](http://go.microsoft.com/fwlink/?LinkID=825643).</span></span>

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a><span data-ttu-id="acb06-313">다음 단계</span><span class="sxs-lookup"><span data-stu-id="acb06-313">Next steps</span></span>
- <span data-ttu-id="acb06-314">SQL Database의 액세스 및 제어에 대한 개요는 [SQL Database 액세스 및 제어](sql-database-control-access.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-314">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span></span>
- <span data-ttu-id="acb06-315">SQL Database의 로그인, 사용자 및 데이터베이스 역할에 대한 개요는 [로그인, 사용자 및 데이터베이스 역할](sql-database-manage-logins.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-315">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span></span>
- <span data-ttu-id="acb06-316">데이터베이스 보안 주체에 대한 자세한 내용은 [보안 주체](https://msdn.microsoft.com/library/ms181127.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-316">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
- <span data-ttu-id="acb06-317">데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 역할](https://msdn.microsoft.com/library/ms189121.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-317">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span></span>
- <span data-ttu-id="acb06-318">SQL Database의 방화벽 규칙에 대한 자세한 내용은 [SQL Database 방화벽 규칙](sql-database-firewall-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acb06-318">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span>

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

