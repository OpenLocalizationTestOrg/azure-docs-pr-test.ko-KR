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
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a><span data-ttu-id="401a5-103">SQL Database 또는 SQL Data Warehouse에서 Azure Active Directory 인증 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="401a5-103">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span></span>

<span data-ttu-id="401a5-104">이 문서에서는 어떻게 toocreate 및 Azure AD를 채운 다음 Azure AD를 사용 하 여 Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-104">This article shows you how toocreate and populate Azure AD, and then use Azure AD with Azure SQL Database and SQL Data Warehouse.</span></span> <span data-ttu-id="401a5-105">개요는 [Azure Active Directory 인증](sql-database-aad-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-105">For an overview, see [Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>

>  [!NOTE]  
>  <span data-ttu-id="401a5-106">Azure VM에서 실행 중인 서버에 Azure Active Directory 계정을 사용 하 여 지원 되지 않습니다 tooSQL를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-106">Connecting tooSQL Server running on an Azure VM is not supported using an Azure Active Directory account.</span></span> <span data-ttu-id="401a5-107">대신 도메인 Active Directory 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-107">Use a domain Active Directory account instead.</span></span>

## <a name="create-and-populate-an-azure-ad"></a><span data-ttu-id="401a5-108">Azure AD 만들기 및 채우기</span><span class="sxs-lookup"><span data-stu-id="401a5-108">Create and populate an Azure AD</span></span>
<span data-ttu-id="401a5-109">Azure AD를 만들고 사용자 및 그룹으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-109">Create an Azure AD and populate it with users and groups.</span></span> <span data-ttu-id="401a5-110">Azure AD는 hello 초기 도메인 Azure AD 관리 되는 도메인을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-110">Azure AD can be hello initial domain Azure AD managed domain.</span></span> <span data-ttu-id="401a5-111">Azure AD는 온-프레미스 Active Directory 도메인 서비스는 hello Azure AD와 페더레이션된 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-111">Azure AD can also be an on-premises Active Directory Domain Services that is federated with hello Azure AD.</span></span>

<span data-ttu-id="401a5-112">자세한 내용은 참조 [Azure Active Directory와 온-프레미스 id 통합](../active-directory/active-directory-aadconnect.md), [고유한 도메인 이름을 tooAzure AD 추가](../active-directory/active-directory-add-domain.md), [Microsoft Azure와의 페더레이션을 지원 Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Azure AD 디렉터리 관리](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Windows PowerShell을 사용 하 여 Azure AD 관리](/powershell/azure/overview?view=azureadps-2.0), 및 [하이브리드 Id 필요한 포트 및 프로토콜](../active-directory/active-directory-aadconnect-ports.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-112">For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name tooAzure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Manage Azure AD using Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), and [Hybrid Identity Required Ports and Protocols](../active-directory/active-directory-aadconnect-ports.md).</span></span>

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a><span data-ttu-id="401a5-113">옵션: 연결 하거나 현재 Azure 구독과 연결 되어 있는 hello active directory 변경</span><span class="sxs-lookup"><span data-stu-id="401a5-113">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
<span data-ttu-id="401a5-114">tooassociate 조직에 대 한 hello Azure AD 디렉터리와 데이터베이스 hello 디렉터리가 설정 hello Azure 구독 호스팅 hello 데이터베이스에 대 한 신뢰할 수 있는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-114">tooassociate your database with hello Azure AD directory for your organization, make hello directory a trusted directory for hello Azure subscription hosting hello database.</span></span> <span data-ttu-id="401a5-115">자세한 내용은 [Azure 구독과 Azure AD의 연관 관계](https://msdn.microsoft.com/library/azure/dn629581.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-115">For more information, see [How Azure subscriptions are associated with Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).</span></span>

<span data-ttu-id="401a5-116">**추가 정보:** 모든 Azure 구독은 Azure AD 인스턴스와 트러스트 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-116">**Additional information:** Every Azure subscription has a trust relationship with an Azure AD instance.</span></span> <span data-ttu-id="401a5-117">즉, 트러스트 하 여 해당 디렉터리 tooauthenticate 사용자, 서비스 및 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-117">This means that it trusts that directory tooauthenticate users, services, and devices.</span></span> <span data-ttu-id="401a5-118">여러 구독 hello 신뢰할 수 있는 동일한 디렉터리만 구독 디렉터리를 하나만 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-118">Multiple subscriptions can trust hello same directory, but a subscription trusts only one directory.</span></span> <span data-ttu-id="401a5-119">어떤 디렉터리는 hello 구독에서 트러스트 나타나면 **설정** 에서 tab 키 [https://manage.windowsazure.com/](https://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-119">You can see which directory is trusted by your subscription under hello **Settings** tab at [https://manage.windowsazure.com/](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="401a5-120">구독에 보다 가깝습니다 구독의 자식 리소스 (웹 사이트, 데이터베이스 및 등)는 Azure의 다른 모든 리소스와 hello 관계와 달리 디렉터리와 구독에이 트러스트 관계가입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-120">This trust relationship that a subscription has with a directory is unlike hello relationship that a subscription has with all other resources in Azure (websites, databases, and so on), which are more like child resources of a subscription.</span></span> <span data-ttu-id="401a5-121">구독이 만료 되 면 toothose hello 구독과 연결 된 다른 리소스에 액세스 하는 경우 또한 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-121">If a subscription expires, then access toothose other resources associated with hello subscription also stops.</span></span> <span data-ttu-id="401a5-122">하지만 Azure의 hello 디렉터리 남아 있으며 해당 디렉터리와 다른 구독을 연결 하 고 계속 toomanage hello directory 사용자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-122">But hello directory remains in Azure, and you can associate another subscription with that directory and continue toomanage hello directory users.</span></span> <span data-ttu-id="401a5-123">리소스에 대한 자세한 내용은 [Azure의 리소스 액세스 이해](https://msdn.microsoft.com/library/azure/dn584083.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-123">For more information about resources, see [Understanding resource access in Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).</span></span>

<span data-ttu-id="401a5-124">hello 다음 절차 보여 toochange hello 지정된 된 구독에 대 한 디렉터리를 연결 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-124">hello following procedures show you how toochange hello associated directory for a given subscription.</span></span>
1. <span data-ttu-id="401a5-125">Tooyour 연결 [Azure 클래식 포털](https://manage.windowsazure.com/) Azure 구독 관리자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-125">Connect tooyour [Azure Classic Portal](https://manage.windowsazure.com/) by using an Azure subscription administrator.</span></span>
2. <span data-ttu-id="401a5-126">왼쪽된 배너 hello 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-126">On hello left banner, select **SETTINGS**.</span></span>
3. <span data-ttu-id="401a5-127">구독은 hello 설정 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-127">Your subscriptions appear in hello settings screen.</span></span> <span data-ttu-id="401a5-128">클릭 하 여 hello 구독 표시 되지 않으면 원하는 경우 **구독** hello 위쪽에, 드롭 다운 hello **필터에서 디렉터리** 상자 구독을 포함 하는 hello 디렉터리를 선택 하 고 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-128">If hello desired subscription does not appear, click **Subscriptions** at hello top, drop down hello **FILTER BY DIRECTORY** box and select hello directory that contains your subscriptions, and then click **APPLY**.</span></span>
   
    ![구독 선택][4]
4. <span data-ttu-id="401a5-130">Hello에 **설정** 영역에서 구독을 클릭 한 다음 클릭 **디렉터리 편집** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-130">In hello **settings** area, click your subscription, and then click  **EDIT DIRECTORY** at hello bottom of hello page.</span></span>
   
    ![ad-settings-portal][5]
5. <span data-ttu-id="401a5-132">Hello에 **디렉터리 편집** 상자 hello 연결 된 SQL Server 또는 SQL 데이터 웨어하우스, Azure Active Directory를 선택 하 고 다음에 대 한 hello 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-132">In hello **EDIT DIRECTORY** box, select hello Azure Active Directory that is associated with your SQL Server or SQL Data Warehouse, and then click hello arrow for next.</span></span>
   
    ![edit-directory-select][6]
6. <span data-ttu-id="401a5-134">Hello에 **확인** 디렉터리 매핑 대화 상자를 확인 하는 "**모든 공동 관리자가 제거 됩니다.**"</span><span class="sxs-lookup"><span data-stu-id="401a5-134">In hello **CONFIRM** directory Mapping dialog box, confirm that "**All co-administrators will be removed.**"</span></span>
   
    ![edit-directory-confirm][7]
7. <span data-ttu-id="401a5-136">Hello 검사 tooreload hello 포털을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-136">Click hello check tooreload hello portal.</span></span>

   > [!NOTE]
   > <span data-ttu-id="401a5-137">Hello 디렉터리, 액세스 tooall 공동 관리자, Azure AD 사용자 및 그룹을 변경 및 디렉터리 백업 리소스 사용자 제거 되 고 액세스 toothis 구독 또는 리소스를 더 이상는 경우.</span><span class="sxs-lookup"><span data-stu-id="401a5-137">When you change hello directory, access tooall co-administrators, Azure AD users and groups, and directory-backed resource users are removed and they no longer have access toothis subscription or its resources.</span></span> <span data-ttu-id="401a5-138">만, 서비스 관리자는 액세스를 구성할 수 hello 새 디렉터리에 따라 주체에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-138">Only you, as a service administrator, can configure access for principals based on hello new directory.</span></span> <span data-ttu-id="401a5-139">이러한 변경에는 상당한 양의 시간 toopropagate tooall 리소스 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-139">This change might take a substantial amount of time toopropagate tooall resources.</span></span> <span data-ttu-id="401a5-140">Hello 디렉터리를 변경 하는, 또한 SQL 데이터베이스 및 SQL 데이터 웨어하우스 용 Azure AD 관리자 hello 변경과 기존 Azure AD 사용자에 대 한 데이터베이스 액세스를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-140">Changing hello directory, also changes hello Azure AD administrator for SQL Database and SQL Data Warehouse and disallow database access for any existing Azure AD users.</span></span> <span data-ttu-id="401a5-141">admin 님 안녕하세요 Azure AD 이어야 합니다 (아래 설명 참조)으로 다시 설정 새로운 Azure AD 사용자가 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-141">hello Azure AD admin must be reset (as described below) and new Azure AD users must be created.</span></span>
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a><span data-ttu-id="401a5-142">Azure SQL Server에 대한 Azure AD 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="401a5-142">Create an Azure AD administrator for Azure SQL server</span></span>
<span data-ttu-id="401a5-143">각 Azure SQL server (호스트 하는 SQL 데이터베이스 또는 SQL 데이터 웨어하우스) hello 전체 Azure SQL server의 관리자에 게는 단일 서버 관리자 계정으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-143">Each Azure SQL server (which hosts a SQL Database or SQL Data Warehouse) starts with a single server administrator account that is hello administrator of hello entire Azure SQL server.</span></span> <span data-ttu-id="401a5-144">Azure AD 계정인 두 번째 SQL Server 관리자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-144">A second SQL Server administrator must be created, that is an Azure AD account.</span></span> <span data-ttu-id="401a5-145">이 보안 주체는 hello master 데이터베이스에 포함 된 데이터베이스 사용자로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-145">This principal is created as a contained database user in hello master database.</span></span> <span data-ttu-id="401a5-146">관리자와 hello 서버 관리자 계정이의 멤버인 hello **db_owner** 모든 사용자의 역할, 데이터베이스 및 hello로 각 사용자 데이터베이스를 입력 **dbo** 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-146">As administrators, hello server administrator accounts are members of hello **db_owner** role in every user database, and enter each user database as hello **dbo** user.</span></span> <span data-ttu-id="401a5-147">Hello 서버 관리자 계정에 대 한 자세한 내용은 참조 [데이터베이스 및 Azure SQL 데이터베이스에서 로그인 관리](sql-database-manage-logins.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-147">For more information about hello server administrator accounts, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="401a5-148">Azure Active Directory 지역에서 복제를 사용 하는 경우 Azure Active Directory 관리자에 게 기본 hello와 hello 보조 서버에 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-148">When using Azure Active Directory with geo-replication, hello Azure Active Directory administrator must be configured for both hello primary and hello secondary servers.</span></span> <span data-ttu-id="401a5-149">서버에 Azure Active Directory 관리자가 없는 경우 다음 Azure Active Directory 로그인 및 사용자가 "연결할 수 없습니다" tooserver 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-149">If a server does not have an Azure Active Directory administrator, then Azure Active Directory logins and users receive a "Cannot connect" tooserver error.</span></span>

> [!NOTE]
> <span data-ttu-id="401a5-150">Hello Azure AD로 데이터베이스 사용자가 제안 된 사용 권한 toovalidate 없기 때문에 Azure AD 계정의 (hello Azure SQL server 관리자 계정 포함)를 기반으로 하는 사용자가 Azure AD 기반 사용자를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-150">Users that are not based on an Azure AD account (including hello Azure SQL server administrator account), cannot create Azure AD-based users, because they do not have permission toovalidate proposed database users with hello Azure AD.</span></span>
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a><span data-ttu-id="401a5-151">Azure SQL Server에 대한 Azure Active Directory 관리자를 프로비전합니다</span><span class="sxs-lookup"><span data-stu-id="401a5-151">Provision an Azure Active Directory administrator for your Azure SQL server</span></span>

<span data-ttu-id="401a5-152">표시 하는 다음 두 절차를 수행 하는 hello tooprovision hello Azure 포털에서에서 하 고 PowerShell을 사용 하 여 Azure SQL server에 대 한 Azure Active Directory 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-152">hello following two procedures show you how tooprovision an Azure Active Directory administrator for your Azure SQL server in hello Azure portal and by using PowerShell.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="401a5-153">Azure portal</span><span class="sxs-lookup"><span data-stu-id="401a5-153">Azure portal</span></span>
1. <span data-ttu-id="401a5-154">Hello에 [Azure 포털](https://portal.azure.com/)에서 오른쪽 위 모서리 hello 클릭 하 여 연결 toodrop 가능한 활성 디렉터리 목록 아래로 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-154">In hello [Azure portal](https://portal.azure.com/), in hello upper-right corner, click your connection toodrop down a list of possible Active Directories.</span></span> <span data-ttu-id="401a5-155">Hello 선택 hello 기본 Azure AD로 Active Directory를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-155">Choose hello correct Active Directory as hello default Azure AD.</span></span> <span data-ttu-id="401a5-156">이 단계 링크 hello 구독 연결이 Active Directory와 동일한 구독 hello를 확인 하는 Azure SQL server와 함께 사용 되는 둘 다에 대해 Azure AD 및 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="401a5-156">This step links hello subscription association with Active Directory with Azure SQL server making sure that hello same subscription is used for both Azure AD and SQL Server.</span></span> <span data-ttu-id="401a5-157">(Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 hello Azure SQL server을 호스팅 될 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="401a5-157">(hello Azure SQL server can be hosting either Azure SQL Database or Azure SQL Data Warehouse.)</span></span>   
    <span data-ttu-id="401a5-158">![choose-ad][8]</span><span class="sxs-lookup"><span data-stu-id="401a5-158">![choose-ad][8]</span></span>   
    
2. <span data-ttu-id="401a5-159">왼쪽 배너 선택 hello에 **SQL server**을 선택 프로그램 **SQL server**, 한 다음 hello **SQL Server** 블레이드에서 클릭 **ActiveDirectory관리자**.</span><span class="sxs-lookup"><span data-stu-id="401a5-159">In hello left banner select **SQL servers**, select your **SQL server**, and then in hello **SQL Server** blade, click **Active Directory admin**.</span></span>   
3. <span data-ttu-id="401a5-160">Hello에 **Active Directory 관리자** 블레이드에서 클릭 **관리자를 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-160">In hello **Active Directory admin** blade, click **Set admin**.</span></span>   
    <span data-ttu-id="401a5-161">![active directory 선택](./media/sql-database-aad-authentication/select-active-directory.png)</span><span class="sxs-lookup"><span data-stu-id="401a5-161">![select active directory](./media/sql-database-aad-authentication/select-active-directory.png)</span></span>  
    
4. <span data-ttu-id="401a5-162">Hello에 **관리자 추가** 블레이드에서 사용자, 선택 hello 사용자 또는 그룹 toobe 관리자 검색 하 고 클릭 한 다음 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-162">In hello **Add admin** blade, search for a user, select hello user or group toobe an administrator, and then click **Select**.</span></span> <span data-ttu-id="401a5-163">(Active Directory 관리 블레이드 hello 모든 멤버와 Active Directory의 그룹을 표시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-163">(hello Active Directory admin blade shows all members and groups of your Active Directory.</span></span> <span data-ttu-id="401a5-164">회색으로 표시된 사용자나 그룹은 Azure AD 관리자로 지원되지 않기 때문에 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-164">Users or groups that are grayed out cannot be selected because they are not supported as Azure AD administrators.</span></span> <span data-ttu-id="401a5-165">(Hello에서 지원 되는 관리자가 사용자의 hello 목록을 **Azure AD 기능 및 제한 사항** 섹션 [SQL 데이터 웨어하우스 또는 SQL 데이터베이스에서 인증을 위해 사용 하 여 Azure Active Directory 인증](sql-database-aad-authentication.md).) 역할 기반 액세스 제어 (RBAC) toohello 포털에만 적용 되며 없습니다 전파 tooSQL 서버.</span><span class="sxs-lookup"><span data-stu-id="401a5-165">(See hello list of supported admins in hello **Azure AD Features and Limitations** section of [Use Azure Active Directory Authentication for authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication.md).) Role-based access control (RBAC) applies only toohello portal and is not propagated tooSQL Server.</span></span>   
    <span data-ttu-id="401a5-166">![관리자 선택](./media/sql-database-aad-authentication/select-admin.png)</span><span class="sxs-lookup"><span data-stu-id="401a5-166">![select admin](./media/sql-database-aad-authentication/select-admin.png)</span></span>  
    
5. <span data-ttu-id="401a5-167">Hello의 hello 위쪽 **Active Directory 관리자** 블레이드에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-167">At hello top of hello **Active Directory admin** blade, click **SAVE**.</span></span>   
    <span data-ttu-id="401a5-168">![관리자 저장](./media/sql-database-aad-authentication/save-admin.png)</span><span class="sxs-lookup"><span data-stu-id="401a5-168">![save admin](./media/sql-database-aad-authentication/save-admin.png)</span></span>   

<span data-ttu-id="401a5-169">관리자에 게 변경 hello 과정은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-169">hello process of changing hello administrator may take several minutes.</span></span> <span data-ttu-id="401a5-170">Hello에 새 관리자에 게 표시 한 다음 **Active Directory 관리자** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-170">Then hello new administrator appears in hello **Active Directory admin** box.</span></span>

   > [!NOTE]
   > <span data-ttu-id="401a5-171">Admin 님 안녕하세요 Azure AD 설정할 때는 hello 새 관리자 이름 (사용자 또는 그룹) 이미 있을 수 없습니다 hello 가상 master 데이터베이스에 SQL Server 인증 사용자로.</span><span class="sxs-lookup"><span data-stu-id="401a5-171">When setting up hello Azure AD admin, hello new admin name (user or group) cannot already be present in hello virtual master database as a SQL Server authentication user.</span></span> <span data-ttu-id="401a5-172">있는 경우 hello Azure AD 관리자 설치가 실패 합니다. 롤링 다시 생성 하 고 해당 그러한 관리자 (이름)을 이미 나타내는 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-172">If present, hello Azure AD admin setup will fail; rolling back its creation and indicating that such an admin (name) already exists.</span></span> <span data-ttu-id="401a5-173">SQL Server 인증 사용자 hello Azure AD의 일부 이므로 Azure AD 인증을 사용 하 여 모든 노력 tooconnect toohello 서버 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-173">Since such a SQL Server authentication user is not part of hello Azure AD, any effort tooconnect toohello server using Azure AD authentication fails.</span></span>
   > 


<span data-ttu-id="401a5-174">toolater hello 위쪽 hello에 관리자를 제거 **Active Directory 관리자** 블레이드에서 클릭 **관리자 제거**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-174">toolater remove an Admin, at hello top of hello **Active Directory admin** blade, click **Remove admin**, and then click **Save**.</span></span>

### <a name="powershell"></a><span data-ttu-id="401a5-175">PowerShell</span><span class="sxs-lookup"><span data-stu-id="401a5-175">PowerShell</span></span>
<span data-ttu-id="401a5-176">PowerShell cmdlet toorun toohave Azure PowerShell 설치 되어 있고 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-176">toorun PowerShell cmdlets, you need toohave Azure PowerShell installed and running.</span></span> <span data-ttu-id="401a5-177">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-177">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="401a5-178">가 Azure AD 관리자 tooprovision hello 다음 Azure PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-178">tooprovision an Azure AD admin, execute hello following Azure PowerShell commands:</span></span>

* <span data-ttu-id="401a5-179">Add-AzureRmAccount</span><span class="sxs-lookup"><span data-stu-id="401a5-179">Add-AzureRmAccount</span></span>
* <span data-ttu-id="401a5-180">Select-AzureRmSubscription</span><span class="sxs-lookup"><span data-stu-id="401a5-180">Select-AzureRmSubscription</span></span>

<span data-ttu-id="401a5-181">Tooprovision를 사용 하 고 Azure AD 관리자를 관리 하는 Cmdlet:</span><span class="sxs-lookup"><span data-stu-id="401a5-181">Cmdlets used tooprovision and manage Azure AD admin:</span></span>

| <span data-ttu-id="401a5-182">Cmdlet 이름</span><span class="sxs-lookup"><span data-stu-id="401a5-182">Cmdlet name</span></span> | <span data-ttu-id="401a5-183">설명</span><span class="sxs-lookup"><span data-stu-id="401a5-183">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="401a5-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="401a5-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="401a5-185">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-185">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="401a5-186">(Hello 현재 구독에서 여야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="401a5-186">(Must be from hello current subscription.)</span></span> |
| [<span data-ttu-id="401a5-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="401a5-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="401a5-188">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-188">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
| [<span data-ttu-id="401a5-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="401a5-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="401a5-190">Azure Active Directory 관리자가 현재 hello Azure SQL server 또는 Azure SQL 데이터 웨어하우스 구성에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-190">Returns information about an Azure Active Directory administrator currently configured for hello Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="401a5-191">PowerShell 명령 g e t-h toosee 내용이 다음이 명령을 각각에 대 한 예를 사용 하 여 ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-191">Use PowerShell command get-help toosee more details for each of these commands, for example ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.</span></span>

<span data-ttu-id="401a5-192">Azure AD 관리자 그룹의 이름을 스크립트 프로 비전 다음 hello **DBA_Group** (개체 id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) hello에 대 한 **demo_server** 이라는 리소스 그룹에 서버 **그룹-23** :</span><span class="sxs-lookup"><span data-stu-id="401a5-192">hello following script provisions an Azure AD administrator group named **DBA_Group** (object id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) for hello **demo_server** server in a resource group named **Group-23**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

<span data-ttu-id="401a5-193">hello **DisplayName** hello Azure AD 표시 이름 또는 hello 사용자 계정 이름 입력된 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-193">hello **DisplayName** input parameter accepts either hello Azure AD display name or hello User Principal Name.</span></span> <span data-ttu-id="401a5-194">예를 들어 ``DisplayName="John Smith"`` 또는 ``DisplayName="johns@contoso.com"``입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-194">For example, ``DisplayName="John Smith"`` and ``DisplayName="johns@contoso.com"``.</span></span> <span data-ttu-id="401a5-195">Azure AD 그룹만 hello Azure AD에 대 한 표시 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-195">For Azure AD groups only hello Azure AD display name is supported.</span></span>

> [!NOTE]
> <span data-ttu-id="401a5-196">Azure PowerShell 명령 hello ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` 에서 지원 되지 않는 사용자에 대 한 Azure AD 관리자를 프로 비전 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-196">hello Azure PowerShell  command ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` does not prevent you from provisioning Azure AD admins for unsupported users.</span></span> <span data-ttu-id="401a5-197">지원 되지 않는 사용자를 프로비저닝할 수 있지만 tooa 데이터베이스를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-197">An unsupported user can be provisioned, but can not connect tooa database.</span></span> 
> 

<span data-ttu-id="401a5-198">hello 다음 예제에서는 선택적 hello **ObjectID**:</span><span class="sxs-lookup"><span data-stu-id="401a5-198">hello following example uses hello optional **ObjectID**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> <span data-ttu-id="401a5-199">Azure AD hello **ObjectID** 는 필요한 경우 hello **DisplayName** 고유 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-199">hello Azure AD **ObjectID** is required when hello **DisplayName** is not unique.</span></span> <span data-ttu-id="401a5-200">tooretrieve hello **ObjectID** 및 **DisplayName** 값, Azure 클래식 포털의 Active Directory 섹션 hello를 사용 하 고 사용자 또는 그룹의 hello 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-200">tooretrieve hello **ObjectID** and **DisplayName** values, use hello Active Directory section of Azure Classic Portal, and view hello properties of a user or group.</span></span>
> 

<span data-ttu-id="401a5-201">다음 예에서는 hello Azure SQL server에 대 한 admin 님 안녕하세요 현재 Azure AD에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-201">hello following example returns information about hello current Azure AD admin for Azure SQL server:</span></span>

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

<span data-ttu-id="401a5-202">다음 예에서는 hello Azure AD 관리자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-202">hello following example removes an Azure AD administrator:</span></span>

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

<span data-ttu-id="401a5-203">또한 hello REST Api를 사용 하 여 Azure Active Directory 관리자를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-203">You can also provision an Azure Active Directory Administrator by using hello REST APIs.</span></span> <span data-ttu-id="401a5-204">자세한 내용은 [서비스 관리 REST API 참조 및 Azure SQL 데이터베이스에 대한 작업](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span><span class="sxs-lookup"><span data-stu-id="401a5-204">For more information, see [Service Management REST API Reference and Operations for Azure SQL Databases Operations for Azure SQL Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span></span>

### <a name="cli"></a><span data-ttu-id="401a5-205">CLI</span><span class="sxs-lookup"><span data-stu-id="401a5-205">CLI</span></span>  
<span data-ttu-id="401a5-206">또한 호출 hello CLI 명령을 수행 하 여 Azure AD 관리자를 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-206">You can also provision an Azure AD admin by calling hello following CLI commands:</span></span>
| <span data-ttu-id="401a5-207">명령</span><span class="sxs-lookup"><span data-stu-id="401a5-207">Command</span></span> | <span data-ttu-id="401a5-208">설명</span><span class="sxs-lookup"><span data-stu-id="401a5-208">Description</span></span> |
| --- | --- |
|[<span data-ttu-id="401a5-209">az sql server ad-admin create</span><span class="sxs-lookup"><span data-stu-id="401a5-209">az sql server ad-admin create</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |<span data-ttu-id="401a5-210">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-210">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="401a5-211">(Hello 현재 구독에서 여야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="401a5-211">(Must be from hello current subscription.)</span></span> |
|[<span data-ttu-id="401a5-212">az sql server ad-admin delete</span><span class="sxs-lookup"><span data-stu-id="401a5-212">az sql server ad-admin delete</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |<span data-ttu-id="401a5-213">Azure SQL Server 또는 Azure SQL Data Warehouse에 대한 Azure Active Directory 관리자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-213">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="401a5-214">az sql server ad-admin list</span><span class="sxs-lookup"><span data-stu-id="401a5-214">az sql server ad-admin list</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |<span data-ttu-id="401a5-215">Azure Active Directory 관리자가 현재 hello Azure SQL server 또는 Azure SQL 데이터 웨어하우스 구성에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-215">Returns information about an Azure Active Directory administrator currently configured for hello Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="401a5-216">az sql server ad-admin update</span><span class="sxs-lookup"><span data-stu-id="401a5-216">az sql server ad-admin update</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |<span data-ttu-id="401a5-217">Azure SQL server 또는 Azure SQL 데이터 웨어하우스에 대 한 Active Directory 관리자에 게 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-217">Updates hello Active Directory administrator for an Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="401a5-218">CLI 명령에 대한 자세한 내용은 [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-218">For more information about CLI commands, see [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).</span></span>  


## <a name="configure-your-client-computers"></a><span data-ttu-id="401a5-219">클라이언트 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="401a5-219">Configure your client computers</span></span>
<span data-ttu-id="401a5-220">모든 클라이언트 컴퓨터에서 응용 프로그램 또는 사용자 연결 있는 tooAzure SQL 데이터베이스 또는 Azure AD id를 사용 하 여 Azure SQL 데이터 웨어하우스 hello 다음 소프트웨어를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-220">On all client machines, from which your applications or users connect tooAzure SQL Database or Azure SQL Data Warehouse using Azure AD identities, you must install hello following software:</span></span>

* <span data-ttu-id="401a5-221">.NET Framework 4.6 이상, [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx)</span><span class="sxs-lookup"><span data-stu-id="401a5-221">.NET Framework 4.6 or later from [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>
* <span data-ttu-id="401a5-222">SQL Server 용 azure Active Directory 인증 라이브러리 (**ADALSQL 합니다. DLL**)는 여러 언어로 제공 됩니다 (x86 및 amd64) hello 다운로드 센터에서 [Microsoft SQL Server 용 Microsoft Active Directory 인증 라이브러리](http://www.microsoft.com/download/details.aspx?id=48742)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-222">Azure Active Directory Authentication Library for SQL Server (**ADALSQL.DLL**) is available in multiple languages (both x86 and amd64) from hello download center at [Microsoft Active Directory Authentication Library for Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).</span></span>

<span data-ttu-id="401a5-223">다음을 통해 이러한 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-223">You can meet these requirements by:</span></span>

* <span data-ttu-id="401a5-224">하나라도 설치 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 또는 [Visual Studio 2015 용 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) 충족 hello.NET Framework 4.6 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-224">Installing either [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) or [SQL Server Data Tools for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) meets hello .NET Framework 4.6 requirement.</span></span>
* <span data-ttu-id="401a5-225">Hello x86 버전을 설치 하는 SSMS **ADALSQL 합니다. DLL**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-225">SSMS installs hello x86 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="401a5-226">Hello amd64 버전을 설치 하는 SSDT **ADALSQL 합니다. DLL**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-226">SSDT installs hello amd64 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="401a5-227">hello에서 최신 Visual Studio [Visual Studio 다운로드](https://www.visualstudio.com/downloads/download-visual-studio-vs) hello.NET Framework 4.6 요구 사항을 충족할 수 있지만 필요한 amd64 버전의 hello를 설치 하지 않는 **ADALSQL 합니다. DLL**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-227">hello latest Visual Studio from [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) meets hello .NET Framework 4.6 requirement, but does not install hello required amd64 version of **ADALSQL.DLL**.</span></span>

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a><span data-ttu-id="401a5-228">AD id에 매핑된 데이터베이스 tooAzure 포함 된 데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="401a5-228">Create contained database users in your database mapped tooAzure AD identities</span></span>

<span data-ttu-id="401a5-229">Azure Active Directory 인증에 포함 된 데이터베이스 사용자로 만든 데이터베이스 사용자가 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-229">Azure Active Directory authentication requires database users toobe created as contained database users.</span></span> <span data-ttu-id="401a5-230">Azure AD id에 따라 포함 된 데이터베이스 사용자는 데이터베이스 사용자를 로그인 hello master 데이터베이스에 없고에 어떤 지도 tooan id hello hello 데이터베이스와 연결 된 Azure AD 디렉터리 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-230">A contained database user based on an Azure AD identity, is a database user that does not have a login in hello master database, and which maps tooan identity in hello Azure AD directory that is associated with hello database.</span></span> <span data-ttu-id="401a5-231">hello Azure AD id에는 개별 사용자 계정 또는 그룹 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-231">hello Azure AD identity can be either an individual user account or a group.</span></span> <span data-ttu-id="401a5-232">포함된 데이터베이스 사용자에 대한 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-232">For more information about contained database users, see [Contained Database Users- Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="401a5-233">(예외로 hello 관리자) 데이터베이스 사용자 포털을 사용 하 여 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-233">Database users (with hello exception of administrators) cannot be created using portal.</span></span> <span data-ttu-id="401a5-234">RBAC 역할은 서버, SQL 데이터베이스 또는 SQL 데이터 웨어하우스 전파 tooSQL 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-234">RBAC roles are not propagated tooSQL Server, SQL Database, or SQL Data Warehouse.</span></span> <span data-ttu-id="401a5-235">Azure RBAC 역할 Azure 리소스 관리를 위해 사용 되 고 toodatabase 사용 권한을 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-235">Azure RBAC roles are used for managing Azure Resources, and do not apply toodatabase permissions.</span></span> <span data-ttu-id="401a5-236">예를 들어 hello **SQL Server 참가자** 역할 액세스 tooconnect toohello SQL 데이터베이스 또는 SQL 데이터 웨어하우스를 부여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-236">For example, hello **SQL Server Contributor** role does not grant access tooconnect toohello SQL Database or SQL Data Warehouse.</span></span> <span data-ttu-id="401a5-237">TRANSACT-SQL 문을 사용 하 여 hello 데이터베이스에서 직접 hello 액세스 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-237">hello access permission must be granted directly in hello database using Transact-SQL statements.</span></span>
>

<span data-ttu-id="401a5-238">Azure AD 기반 포함 된 데이터베이스 사용자 (관리자 외의 다른 hello 서버 hello 데이터베이스를 소유한) 있는 사용자로 Azure AD id가 있는 toohello 데이터베이스를 연결 하는 toocreate 이상 hello **ALTER ANY USER** 권한.</span><span class="sxs-lookup"><span data-stu-id="401a5-238">toocreate an Azure AD-based contained database user (other than hello server administrator that owns hello database), connect toohello database with an Azure AD identity, as a user with at least hello **ALTER ANY USER** permission.</span></span> <span data-ttu-id="401a5-239">다음 TRANSACT-SQL 구문 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="401a5-239">Then use hello following Transact-SQL syntax:</span></span>

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="401a5-240">*Azure_AD_principal_name* hello Azure AD 그룹에 대 한 Azure AD 사용자 또는 hello 표시 이름을 사용자 계정 이름 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-240">*Azure_AD_principal_name* can be hello user principal name of an Azure AD user or hello display name for an Azure AD group.</span></span>

<span data-ttu-id="401a5-241">**예:** toocreate 포함된 된 데이터베이스 사용자는 Azure AD를 나타내는 페더레이션 또는 도메인 사용자를 관리 대상:</span><span class="sxs-lookup"><span data-stu-id="401a5-241">**Examples:** toocreate a contained database user representing an Azure AD federated or managed domain user:</span></span>
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="401a5-242">toocreate 포함된 된 데이터베이스 사용자는 Azure AD를 나타내는 또는 도메인 그룹을 페더레이션 보안 그룹의 hello 표시 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-242">toocreate a contained database user representing an Azure AD or federated domain group, provide hello display name of a security group:</span></span>
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="401a5-243">포함된 된 데이터베이스 사용자는 Azure AD 토큰을 사용 하 여 연결 하는 응용 프로그램을 나타내는 toocreate:</span><span class="sxs-lookup"><span data-stu-id="401a5-243">toocreate a contained database user representing an application that connects using an Azure AD token:</span></span>

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  <span data-ttu-id="401a5-244">Hello Azure 구독과 연결 된 Azure Active Directory 이외의 다른 Azure Active Directory에서 사용자를 직접 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-244">You cannot directly create a user from an Azure Active Directory other than hello Azure Active Directory that is associated with your Azure subscription.</span></span> <span data-ttu-id="401a5-245">그러나 Active Directory 노드와 연결 된 가져온된 사용자 hello에 다른 활성 디렉터리의 구성원 (이 외부 사용자 라고 함) hello Active Directory 테 넌 트의 tooan Active Directory 그룹 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-245">However, members of other Active Directories that are imported users in hello associated Active Directory (known as external users) can be added tooan Active Directory group in hello tenant Active Directory.</span></span> <span data-ttu-id="401a5-246">해당 AD 그룹에 대 한 포함 된 데이터베이스 사용자를 만들면 hello hello에서 사용자가 외부 Active Directory를 얻을 수 액세스 tooSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-246">By creating a contained database user for that AD group, hello users from hello external Active Directory can gain access tooSQL Database.</span></span>   

<span data-ttu-id="401a5-247">Azure Active Directory 기반의 포함된 데이터베이스 사용자 만들기와 관련한 자세한 내용은 [CREATE USER(Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-247">For more information about creating contained database users based on Azure Active Directory identities, see [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="401a5-248">Toohello 서버를 연결할 모든 Azure AD 인증 사용자를 방지 하는 Azure SQL server에 대 한 hello Azure Active Directory 관리자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-248">Removing hello Azure Active Directory administrator for Azure SQL server prevents any Azure AD authentication user from connecting toohello server.</span></span> <span data-ttu-id="401a5-249">필요한 경우 사용할 수 없는 Azure AD 사용자는 SQL 데이터베이스 관리자가 수동으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-249">If necessary, unusable Azure AD users can be dropped manually by a SQL Database administrator.</span></span>   

>  [!NOTE]
>  <span data-ttu-id="401a5-250">표시 되 면 한 **연결 제한 시간이 만료**, tooset hello를 할 수 있습니다 `TransparentNetworkIPResolution` hello 연결 문자열 toofalse의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-250">If you receive a **Connection Timeout Expired**, you may need tooset hello `TransparentNetworkIPResolution` parameter of hello connection string toofalse.</span></span> <span data-ttu-id="401a5-251">자세한 내용은 [.NET Framework 4.6.1의 연결 시간 초과 문제 – TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-251">For more information, see [Connection timeout issue with .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).</span></span>   

   
<span data-ttu-id="401a5-252">해당 사용자를 hello 받을 데이터베이스 사용자를 만들 때 **연결** 권한 toothat 데이터베이스 hello의 멤버로 연결할 수 있습니다 **공용** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-252">When you create a database user, that user receives hello **CONNECT** permission and can connect toothat database as a member of hello **PUBLIC** role.</span></span> <span data-ttu-id="401a5-253">처음 사용 가능한 toohello 사용자는 모든 사용 권한이 부여 toohello 권한만 hello **공용** 역할 또는 사용 권한을 부여 tooany Windows 그룹의 구성원 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-253">Initially hello only permissions available toohello user are any permissions granted toohello **PUBLIC** role, or any permissions granted tooany Windows groups that they are a member of.</span></span> <span data-ttu-id="401a5-254">Azure AD 기반 포함 된 데이터베이스 사용자를 프로 비전 한 번, 다른 유형의 사용자 권한을 tooany을 부여 하는 방식으로 동일한 hello hello 사용자 추가 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-254">Once you provision an Azure AD-based contained database user, you can grant hello user additional permissions, hello same way as you grant permission tooany other type of user.</span></span> <span data-ttu-id="401a5-255">일반적으로 toodatabase 역할 권한을 부여 하 고 사용자가 tooroles를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-255">Typically grant permissions toodatabase roles, and add users tooroles.</span></span> <span data-ttu-id="401a5-256">자세한 내용은 [데이터베이스 엔진의 권한 기초](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-256">For more information, see [Database Engine Permission Basics](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx).</span></span> <span data-ttu-id="401a5-257">특수 SQL 데이터베이스 역할에 대한 자세한 내용은 [Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-257">For more information about special SQL Database roles, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="401a5-258">관리 도메인으로 가져온 페더레이션된 도메인 사용자는 관리 되는 hello 도메인 id를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-258">A federated domain user that is imported into a manage domain, must use hello managed domain identity.</span></span>

> [!NOTE]
> <span data-ttu-id="401a5-259">Azure AD 사용자가 붙습니다 hello 데이터베이스 메타 데이터에 형식과 E (EXTERNAL_USER) 및 그룹에 대 한 X (EXTERNAL_GROUPS) 형식.</span><span class="sxs-lookup"><span data-stu-id="401a5-259">Azure AD users are marked in hello database metadata with type E (EXTERNAL_USER) and for groups with type X (EXTERNAL_GROUPS).</span></span> <span data-ttu-id="401a5-260">자세한 내용은 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-260">For more information, see [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span> 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a><span data-ttu-id="401a5-261">SSMS 또는 SSDT를 사용 하 여 toohello 사용자 데이터베이스 또는 데이터 웨어하우스 연결</span><span class="sxs-lookup"><span data-stu-id="401a5-261">Connect toohello user database or data warehouse by using SSMS or SSDT</span></span>  
<span data-ttu-id="401a5-262">관리자에 게 Azure AD tooconfirm 제대로 설정, toohello 연결 **마스터** hello Azure AD 관리자 계정을 사용 하 여 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-262">tooconfirm hello Azure AD administrator is properly set up, connect toohello **master** database using hello Azure AD administrator account.</span></span>
<span data-ttu-id="401a5-263">Azure AD 기반 포함 된 데이터베이스 사용자 (관리자 외의 다른 hello 서버 hello 데이터베이스를 소유한) tooprovision 액세스 toohello 데이터베이스가 있는 Azure AD id로 toohello 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-263">tooprovision an Azure AD-based contained database user (other than hello server administrator that owns hello database), connect toohello database with an Azure AD identity that has access toohello database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="401a5-264">Azure Active Directory 인증에 대한 지원은 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 및 Visual Studio 2015의 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-264">Support for Azure Active Directory authentication is available with [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) in Visual Studio 2015.</span></span> <span data-ttu-id="401a5-265">SSMS 2016 년 8 월 릴리스 hello에서는 관리자가 있는 Active Directory 유니버설 인증에 대 한 지원이 포함 되어 toorequire Multi-factor Authentication 전화 통화, 문자 메시지, 스마트 카드를 사용 하 여 pin 또는 모바일 앱 알림을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-265">hello August 2016 release of SSMS also includes support for Active Directory Universal Authentication, which allows administrators toorequire Multi-Factor Authentication using a phone call, text message, smart cards with pin, or mobile app notification.</span></span>
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a><span data-ttu-id="401a5-266">SSMS 또는 SSDT를 사용 하는 Azure AD identity tooconnect를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="401a5-266">Using an Azure AD identity tooconnect using SSMS or SSDT</span></span>  

<span data-ttu-id="401a5-267">다음 절차를 수행 하는 hello tooconnect tooa SQL SQL Server Management Studio 또는 SQL Server 데이터베이스 도구를 사용 하 여 Azure AD id로 데이터베이스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-267">hello following procedures show you how tooconnect tooa SQL database with an Azure AD identity using SQL Server Management Studio or SQL Server Database Tools.</span></span>

### <a name="active-directory-integrated-authentication"></a><span data-ttu-id="401a5-268">Active Directory 통합 인증</span><span class="sxs-lookup"><span data-stu-id="401a5-268">Active Directory integrated authentication</span></span>

<span data-ttu-id="401a5-269">TooWindows 페더레이션된 도메인에서 Azure Active Directory 자격 증명을 사용 하 여 로그인 하는 경우이 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-269">Use this method if you are logged in tooWindows using your Azure Active Directory credentials from a federated domain.</span></span>

1. <span data-ttu-id="401a5-270">Management Studio 또는 데이터 도구를 시작 및 hello **tooServer 연결** (또는 **tooDatabase 엔진 연결**) 대화 상자에서 hello **인증** 상자을 선택**통합-active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-270">Start Management Studio or Data Tools and in hello **Connect tooServer** (or **Connect tooDatabase Engine**) dialog box, in hello **Authentication** box, select **Active Directory - Integrated**.</span></span> <span data-ttu-id="401a5-271">암호가 필요 하거나 hello 연결에 대 한 기존 자격 증명 나타납니다 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-271">No password is needed or can be entered because your existing credentials will be presented for hello connection.</span></span>   

    ![AD 통합 인증 선택][11]
2. <span data-ttu-id="401a5-273">Hello 클릭 **옵션** 단추를 hello에 **연결 속성** 페이지 hello **toodatabase 연결** 상자 hello 이름을 입력 합니다 tooconnect hello 사용자 데이터베이스의 원하는 받는 사람.</span><span class="sxs-lookup"><span data-stu-id="401a5-273">Click hello **Options** button, and on hello **Connection Properties** page, in hello **Connect toodatabase** box, type hello name of hello user database you want tooconnect to.</span></span> <span data-ttu-id="401a5-274">(hello **AD 도메인 이름 또는 테 넌 트 ID**"에 대 한 옵션은만 지원 **MFA 연결과 유니버설** 옵션, 그렇지 않으면 것은 회색으로 표시 합니다.)</span><span class="sxs-lookup"><span data-stu-id="401a5-274">(hello **AD domain name or tenant ID**” option is only supported for **Universal with MFA connection** options, otherwise it is greyed out.)</span></span>  

    ![Hello 데이터베이스 이름 선택][13]

## <a name="active-directory-password-authentication"></a><span data-ttu-id="401a5-276">Active Directory 암호 인증</span><span class="sxs-lookup"><span data-stu-id="401a5-276">Active Directory password authentication</span></span>

<span data-ttu-id="401a5-277">도메인 관리 hello Azure AD를 사용 하 여 Azure AD 사용자 이름으로 연결 하는 경우이 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-277">Use this method when connecting with an Azure AD principal name using hello Azure AD managed domain.</span></span> <span data-ttu-id="401a5-278">예를 들어 원격으로 작업 하는 경우 액세스 toohello 도메인 없이 페더레이션된 계정에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-278">You can also use it for federated account without access toohello domain, for example when working remotely.</span></span>

<span data-ttu-id="401a5-279">TooWindows 자격 증명을 사용 하 여 azure에 페더레이션 되지 않아서 있는 도메인에서 로그인 하거나 Azure AD 또는 초기 hello에 따라 클라이언트 도메인 hello 사용 하 여 Azure AD 인증을 사용 하는 경우이 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-279">Use this method if you are logged in tooWindows using credentials from a domain that is not federated with Azure, or when using Azure AD authentication using Azure AD based on hello initial or hello client domain.</span></span>

1. <span data-ttu-id="401a5-280">Management Studio 또는 데이터 도구를 시작 및 hello **tooServer 연결** (또는 **tooDatabase 엔진 연결**) 대화 상자에서 hello **인증** 상자을 선택**Active Directory-암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-280">Start Management Studio or Data Tools and in hello **Connect tooServer** (or **Connect tooDatabase Engine**) dialog box, in hello **Authentication** box, select **Active Directory - Password**.</span></span>
2. <span data-ttu-id="401a5-281">Hello에 **사용자 이름** hello 형식에 Azure Active Directory 사용자 이름을 입력 합니다  **username@domain.com** 합니다. Hello Azure Active Directory에서에서 계정 이거나 hello Azure Active Directory와 페더레이션 할 도메인에서 계정을이 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-281">In hello **User name** box, type your Azure Active Directory user name in hello format **username@domain.com**. This must be an account from hello Azure Active Directory or an account from a domain federate with hello Azure Active Directory.</span></span>
3. <span data-ttu-id="401a5-282">Hello에 **암호** 상자 hello Azure Active Directory 계정에 대 한 사용자 암호를 입력 하거나 계정 도메인을 페더레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-282">In hello **Password** box, type your user password for hello Azure Active Directory account or federated domain account.</span></span>

    ![AD 암호 인증 선택][12]
4. <span data-ttu-id="401a5-284">Hello 클릭 **옵션** 단추를 hello에 **연결 속성** 페이지 hello **toodatabase 연결** 상자 hello 이름을 입력 합니다 tooconnect hello 사용자 데이터베이스의 원하는 받는 사람.</span><span class="sxs-lookup"><span data-stu-id="401a5-284">Click hello **Options** button, and on hello **Connection Properties** page, in hello **Connect toodatabase** box, type hello name of hello user database you want tooconnect to.</span></span> <span data-ttu-id="401a5-285">(Hello 모양이 hello 이전 옵션 참조).</span><span class="sxs-lookup"><span data-stu-id="401a5-285">(See hello graphic in hello previous option.)</span></span>

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a><span data-ttu-id="401a5-286">클라이언트 응용 프로그램에서 Azure AD identity tooconnect는를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="401a5-286">Using an Azure AD identity tooconnect from a client application</span></span>

<span data-ttu-id="401a5-287">다음 절차를 수행 하는 hello tooconnect tooa SQL 클라이언트 응용 프로그램에서 Azure AD id로 데이터베이스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-287">hello following procedures show you how tooconnect tooa SQL database with an Azure AD identity from a client application.</span></span>

###  <a name="active-directory-integrated-authentication"></a><span data-ttu-id="401a5-288">Active Directory 통합 인증</span><span class="sxs-lookup"><span data-stu-id="401a5-288">Active Directory integrated authentication</span></span>

<span data-ttu-id="401a5-289">toouse 통합 Windows 인증, 도메인의 Active Directory를 Azure Active Directory와 페더레이션 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-289">toouse integrated Windows authentication, your domain’s Active Directory must be federated with Azure Active Directory.</span></span> <span data-ttu-id="401a5-290">클라이언트 응용 프로그램 (또는 서비스) 연결 중 toohello 데이터베이스 사용자의 도메인 자격 증명으로 도메인에 가입 된 컴퓨터에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-290">Your client application (or a service) connecting toohello database must be running on a domain-joined machine under a user’s domain credentials.</span></span>

<span data-ttu-id="401a5-291">인증 및 Azure AD id 통합 tooconnect tooa 데이터베이스를 사용 하 여, hello 데이터베이스 연결 문자열에 hello 인증 키워드 tooActive 디렉터리 통합 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-291">tooconnect tooa database using integrated authentication and an Azure AD identity, hello Authentication keyword in hello database connection string must be set tooActive Directory Integrated.</span></span> <span data-ttu-id="401a5-292">hello 다음 C# 코드 샘플에서는 ADO.NET 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-292">hello following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="401a5-293">연결 문자열 키워드 hello ``Integrated Security=True`` tooAzure SQL 데이터베이스를 연결 하기 위한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-293">hello connection string keyword ``Integrated Security=True`` is not supported for connecting tooAzure SQL Database.</span></span> <span data-ttu-id="401a5-294">Tooremove 공백이 필요 하 고 인증 too'ActiveDirectoryIntegrated 설정는 ODBC 연결을 만들 때는 '.</span><span class="sxs-lookup"><span data-stu-id="401a5-294">When making an ODBC connection, you will need tooremove spaces and set Authentication too'ActiveDirectoryIntegrated'.</span></span>

### <a name="active-directory-password-authentication"></a><span data-ttu-id="401a5-295">Active Directory 암호 인증</span><span class="sxs-lookup"><span data-stu-id="401a5-295">Active Directory password authentication</span></span>

<span data-ttu-id="401a5-296">인증 및 Azure AD id 통합 tooconnect tooa 데이터베이스를 사용 하 여, hello 인증 키워드 tooActive 디렉터리 암호를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-296">tooconnect tooa database using integrated authentication and an Azure AD identity, hello Authentication keyword must be set tooActive Directory Password.</span></span> <span data-ttu-id="401a5-297">hello 연결 문자열은 사용자 ID/UID 및 PWD 암호/키워드와 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-297">hello connection string must contain User ID/UID and Password/PWD keywords and values.</span></span> <span data-ttu-id="401a5-298">hello 다음 C# 코드 샘플에서는 ADO.NET 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-298">hello following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="401a5-299">사용할 수 있는 hello 데모 코드 샘플을 사용 하 여 Azure AD 인증 방법에 대 한 자세한 [Azure AD 인증 GitHub 데모](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-299">Learn more about Azure AD authentication methods using hello demo code samples available at [Azure AD Authentication GitHub Demo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).</span></span>

## <a name="azure-ad-token"></a><span data-ttu-id="401a5-300">Azure AD 토큰</span><span class="sxs-lookup"><span data-stu-id="401a5-300">Azure AD token</span></span>
<span data-ttu-id="401a5-301">이 인증 방법에서 Azure Active Directory (AAD) 토큰을 가져와서 중간 계층 서비스 tooconnect tooAzure를 SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-301">This authentication method allows middle-tier services tooconnect tooAzure SQL Database or Azure SQL Data Warehouse by obtaining a token from Azure Active Directory (AAD).</span></span> <span data-ttu-id="401a5-302">이는 인증서 기반 인증을 비롯한 정교한 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-302">It enables sophisticated scenarios including certificate-based authentication.</span></span> <span data-ttu-id="401a5-303">네 가지 기본 단계 toouse Azure AD 토큰 인증을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-303">You must complete four basic steps toouse Azure AD token authentication:</span></span>

1. <span data-ttu-id="401a5-304">Azure Active Directory와 응용 프로그램을 등록 하 고 코드에 대 한 hello 클라이언트 id를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-304">Register your application with Azure Active Directory and get hello client id for your code.</span></span> 
2. <span data-ttu-id="401a5-305">데이터베이스 사용자 나타내는 hello 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-305">Create a database user representing hello application.</span></span> <span data-ttu-id="401a5-306">6단계에서 완료).</span><span class="sxs-lookup"><span data-stu-id="401a5-306">(Completed earlier in step 6.)</span></span>
3. <span data-ttu-id="401a5-307">Hello 응용 프로그램에 클라이언트 컴퓨터 실행 hello 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-307">Create a certificate on hello client computer runs hello application.</span></span>
4. <span data-ttu-id="401a5-308">응용 프로그램에 대 한 키로 hello 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-308">Add hello certificate as a key for your application.</span></span>

<span data-ttu-id="401a5-309">샘플 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="401a5-309">Sample connection string:</span></span>

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

<span data-ttu-id="401a5-310">자세한 내용은 [SQL Server 보안 블로그](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-310">For more information, see [SQL Server Security Blog](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).</span></span>

### <a name="sqlcmd"></a><span data-ttu-id="401a5-311">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="401a5-311">sqlcmd</span></span>

<span data-ttu-id="401a5-312">명령문 안녕, 13.1 hello에서 사용할 수 있는 sqlcmd의 버전을 사용 하 여 연결 [다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=825643)합니다.</span><span class="sxs-lookup"><span data-stu-id="401a5-312">hello following statements, connect using version 13.1 of sqlcmd, which is available from hello [Download Center](http://go.microsoft.com/fwlink/?LinkID=825643).</span></span>

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a><span data-ttu-id="401a5-313">다음 단계</span><span class="sxs-lookup"><span data-stu-id="401a5-313">Next steps</span></span>
- <span data-ttu-id="401a5-314">SQL Database의 액세스 및 제어에 대한 개요는 [SQL Database 액세스 및 제어](sql-database-control-access.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-314">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span></span>
- <span data-ttu-id="401a5-315">SQL Database의 로그인, 사용자 및 데이터베이스 역할에 대한 개요는 [로그인, 사용자 및 데이터베이스 역할](sql-database-manage-logins.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-315">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span></span>
- <span data-ttu-id="401a5-316">데이터베이스 보안 주체에 대한 자세한 내용은 [보안 주체](https://msdn.microsoft.com/library/ms181127.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-316">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
- <span data-ttu-id="401a5-317">데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 역할](https://msdn.microsoft.com/library/ms189121.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-317">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span></span>
- <span data-ttu-id="401a5-318">SQL Database의 방화벽 규칙에 대한 자세한 내용은 [SQL Database 방화벽 규칙](sql-database-firewall-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="401a5-318">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span>

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

