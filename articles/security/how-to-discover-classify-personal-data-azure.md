---
title: "aaaDiscover를 식별 하 고, Microsoft Azure에서 개인 데이터를 분류 | Microsoft Docs"
description: "데이터를 검색, 분류, 검색, 식별하는 방법에 대해 자세히 알아보기"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a><span data-ttu-id="01ab4-103">Microsoft Azure에서 개인 데이터 검색, 식별 및 분류</span><span class="sxs-lookup"><span data-stu-id="01ab4-103">Discover, identify, and classify personal data in Microsoft Azure</span></span>

<span data-ttu-id="01ab4-104">이 문서에서는 toodiscover,이 식별 하 고 여러 Azure 도구와 서비스, Azure, Azure HDInsight의 Hadoop 클러스터에 대 한 Azure Data Catalog, Azure Active Directory, SQL 데이터베이스, 파워 쿼리를 사용 하는 등의 개인 데이터를 분류 하는 방법에 지침 제공 Azure Cosmos DB에 대 한 정보 보호, Azure 검색 및 SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-104">This article provides guidance on how toodiscover, identify, and classify personal data in several Azure tools and services, including using Azure Data Catalog, Azure Active Directory, SQL Database, Power Query for Hadoop clusters in Azure HDInsight, Azure Information Protection, Azure Search, and SQL queries for Azure Cosmos DB.</span></span>

## <a name="scenario-problem-statement-and-goal"></a><span data-ttu-id="01ab4-105">시나리오, 문제 설명 및 목표</span><span class="sxs-lookup"><span data-stu-id="01ab4-105">Scenario, problem statement, and goal</span></span>

<span data-ttu-id="01ab4-106">미국 기반 스포츠 회사는 다양한 개인 데이터 및 기타 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-106">A U.S.-based sports company collects a variety of personal and other data.</span></span> <span data-ttu-id="01ab4-107">고객 및 직원 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-107">This includes customers and employee data.</span></span> <span data-ttu-id="01ab4-108">여러 데이터베이스에 유지 하 고 자신의 Azure 환경에서 여러 다른 위치에 저장 하는 hello 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-108">hello company keeps it in multiple databases, and stores it in several different locations in their Azure environment.</span></span> <span data-ttu-id="01ab4-109">또한 tooselling 스포츠 장비, 또한를 호스트 하 고, EU hello에 포함 하는 hello world 정예 운동 이벤트에 대 한 등록을 관리 및 일부의 경우 hello에 수집 된 고객 데이터는 의료 보험 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-109">In addition tooselling sports equipment, they also host and manage registration for elite athletic events around hello world, including in hello EU, and in some cases hello customer data they collect includes medical information.</span></span>

<span data-ttu-id="01ab4-110">Hello 회사 많은 국제 bicycling tours 매년 호스트 많고 hello 전 세계 여러 위치에 임시 직원, 이후 몇 가지 hello 데이터 집합은 매우 큽니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-110">Since hello company hosts many international bicycling tours every year and has contingent staff in locations around hello globe, a couple of hello data sets are quite large.</span></span> <span data-ttu-id="01ab4-111">hello 회사에서 고객 및 직원을 모두 사용 되는 개발자 빌드된 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-111">hello company also has developer-built applications that are used by both customers and employees.</span></span>

<span data-ttu-id="01ab4-112">hello 사는 문제 다음 tooaddress hello:</span><span class="sxs-lookup"><span data-stu-id="01ab4-112">hello company wants tooaddress hello following problems:</span></span>

- <span data-ttu-id="01ab4-113">개인 고객 및 직원 데이터 hello에서 분류/구별 해야 순서 tooensure 적절 한 액세스 및 보안에서 다른 데이터 hello 회사를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-113">Customer and employee personal data must be classified/distinguished from hello other data hello company collects in order tooensure proper access and security.</span></span>
- <span data-ttu-id="01ab4-114">hello 데이터 관리자 야 합니다. tooeasily 다양 한 영역 hello Azure 환경에 걸쳐 hello 위치의 고객 개인 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-114">hello data admin needs tooeasily discover hello location of customer personal data across various areas of hello Azure environment.</span></span>
- <span data-ttu-id="01ab4-115">고객 및 직원 개인 데이터에 표시 되는 공유 문서 및 전자 메일 통신으로 표시 되어야 합니다 toohelp 확인을 안전 하 게 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-115">Customer and employee personal data that appears in shared documents and email communications must be labeled toohelp ensure that it’s kept secure.</span></span>
- <span data-ttu-id="01ab4-116">hello 회사의 응용 프로그램 개발자가 웹 및 모바일 앱에서 개인 데이터를 고객 및 직원에 대 한 방식으로 tooeasily 검색을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-116">hello company’s app developers need a way tooeasily search for customer and employee personal data in their web and mobile apps.</span></span>
- <span data-ttu-id="01ab4-117">또한 개발자 tooquery 자신의 문서 데이터베이스 개인 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-117">Developers also need tooquery their document database for personal data.</span></span>

### <a name="company-goals"></a><span data-ttu-id="01ab4-118">회사 목표</span><span class="sxs-lookup"><span data-stu-id="01ab4-118">Company goals</span></span>

- <span data-ttu-id="01ab4-119">모든 고객 및 직원 개인 데이터를 쉽게 찾을 수 있도록 Azure Data Catalog에서 태그가 지정되거나 주석이 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-119">All customer and employee personal data must be tagged/annotated in Azure Data Catalog so it can be found easily.</span></span> <span data-ttu-id="01ab4-120">이상적으로 고객 및 직원 개인 데이터는 별도로 태그가 지정되거나 주석이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-120">Ideally customer and employee personal data are tagged/annotated separately.</span></span>
- <span data-ttu-id="01ab4-121">고객 및 직원 사용자 프로필의 개인 데이터 및 Azure Active Directory에 있는 작업 정보는 쉽게 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-121">Personal data from customer and employee user profiles and work information residing in Azure Active Directory must be easily located.</span></span>
- <span data-ttu-id="01ab4-122">여러 SQL Databases에 있는 개인 데이터를 쉽게 쿼리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-122">Personal data residing in multiple SQL databases must be easily queried.</span></span> 
- <span data-ttu-id="01ab4-123">Hello 회사의 큰 데이터 집합의 일부 Azure HDInsight를 통해 관리 되 고 Hadoop에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-123">Some of hello company’s large data sets are managed through Azure HDInsight and stored in Hadoop.</span></span> <span data-ttu-id="01ab4-124">해당 데이터는 개인 데이터를 쿼리할 수 있도록 Excel로 가져올 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-124">They must be imported into Excel so they can be queried for personal data.</span></span>
- <span data-ttu-id="01ab4-125">문서 및 전자 메일 통신에서 공유된 개인 데이터는 Azure Information Protection에서 분류되고 레이블이 지정되고 안전하게 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-125">Personal data shared in documents and email communications must be classified, labeled, and kept secure with Azure Information Protection.</span></span>
- <span data-ttu-id="01ab4-126">hello 회사의 응용 프로그램 개발자 해야 수 toodiscover 고객 및 직원 개인 앱에서 데이터 hello 빌드되기 했으므로 Azure 검색 작업을 수행할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-126">hello company’s app developers must be able toodiscover customer and employee personal data in hello apps they’ve built, which they can do with Azure Search.</span></span>
- <span data-ttu-id="01ab4-127">개발자가 자신의 문서 데이터베이스에서 개인 데이터 수 toofind 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-127">Developers must be able toofind personal data in their document database.</span></span>

## <a name="azure-active-directory-data-discovery"></a><span data-ttu-id="01ab4-128">Azure Active Directory: 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="01ab4-128">Azure Active Directory: Data discovery</span></span>

<span data-ttu-id="01ab4-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="01ab4-130">고객 및 직원에 해당 하는 사용자의 프로필 및 개인 데이터를 포함 하는 사용자 작업 정보를 찾을 수 있습니다 프로그램 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) hello를 사용 하 여 (AAD) 환경 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-130">You can locate customer and employee user profiles and user work information that contain personal data in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="01ab4-131">Toofind 하거나 특정 사용자에 대 한 개인 데이터를 변경 하는 경우 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-131">This is particularly helpful if you want toofind or change personal data for a specific user.</span></span> <span data-ttu-id="01ab4-132">또한 사용자 프로필 및 작업 정보를 추가하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-132">You can also add or change user profile and work information.</span></span> <span data-ttu-id="01ab4-133">Hello 디렉터리에 대 한 전역 관리자 인 계정으로 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-133">You must sign in with an account that’s a global admin for hello directory.</span></span>

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a><span data-ttu-id="01ab4-134">사용자 프로필 및 작업 정보를 찾고 보려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="01ab4-134">How do I locate or view user profile and work information?</span></span>

1. <span data-ttu-id="01ab4-135">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-135">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="01ab4-136">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-136">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![사용자 프로필 및 작업 정보를 찾으려면 어떻게 할까요?](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. <span data-ttu-id="01ab4-138">Hello에 **사용자 및 그룹** 블레이드를 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-138">On hello **Users and groups** blade, select **Users**.</span></span>

  ![사용자 및 그룹 열기](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. <span data-ttu-id="01ab4-140">Hello에 **사용자 및 그룹-사용자가** 블레이드를 hello 목록에서 사용자를 선택한 다음 선택 hello 선택한 사용자에 대 한 hello 블레이드에서 **프로필** tooview 개인 데이터가 포함 될 수 있는 사용자 프로필 정보 .</span><span class="sxs-lookup"><span data-stu-id="01ab4-140">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview user profile information that might contain personal data.</span></span>

  ![사용자 선택](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. <span data-ttu-id="01ab4-142">작업을 하 고 다음 hello 명령 모음에서 선택 수를 tooadd 필요 하거나 사용자 프로필 정보를 변경 하는 경우 **저장 합니다.**</span><span class="sxs-lookup"><span data-stu-id="01ab4-142">If you need tooadd or change user profile information, you can do so, and then, in hello command bar, select **Save.**</span></span>
6. <span data-ttu-id="01ab4-143">Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **작업 정보** tooview 개인 데이터를 포함할 수 있는 사용자 작업 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-143">On hello blade for hello selected user, select **Work Info** tooview user work information that may contain personal data.</span></span>

 ![작업 정보 보기](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. <span data-ttu-id="01ab4-145">작업을 하 고 다음 hello 명령 모음에서 선택 수를 tooadd 필요 하거나 사용자 작업 정보를 변경 하는 경우 **저장 합니다.**</span><span class="sxs-lookup"><span data-stu-id="01ab4-145">If you need tooadd or change user work information, you can do so, and then, in hello command bar, select **Save.**</span></span>

## <a name="azure-sql-database-data-discovery"></a><span data-ttu-id="01ab4-146">Azure SQL Database: 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="01ab4-146">Azure SQL Database: Data discovery</span></span>

<span data-ttu-id="01ab4-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)는 개발자가 응용 프로그램을 빌드하고 유지하는 데 유용한 클라우드 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span> <span data-ttu-id="01ab4-148">표준 SQL 쿼리를 사용하여 개인 데이터를 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-148">Personal data can be found in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries.</span></span> <span data-ttu-id="01ab4-149">Azure SQL 탄력적 쿼리 (미리 보기)를 사용 하면 사용자가 tooperform 데이터베이스 간 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-149">Azure SQL elastic query (preview) enables users tooperform cross-database queries.</span></span>

<span data-ttu-id="01ab4-150">자세한 [SQL 데이터베이스](../sql-database/sql-database-technical-overview.md) 자습서의 SQL 데이터베이스를 사용 하 여 많은 측면을 설명 합니다. 방법을 비롯 하 여 하나 toobuild 방법과 toorun 데이터 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-150">A detailed [SQL database](../sql-database/sql-database-technical-overview.md) tutorial explains many aspects of using a SQL database, including how toobuild one and how toorun data queries.</span></span> <span data-ttu-id="01ab4-151">hello 다음은 링크 toospecific 섹션이 포함 된 hello 자습서에서 사용할 수 있는 hello 정보의 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-151">hello following is a summary of hello information available in hello tutorial with links toospecific sections.</span></span>

### <a name="how-do-i-build-a-sql-database"></a><span data-ttu-id="01ab4-152">SQL Database를 빌드하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="01ab4-152">How do I build a SQL database?</span></span>

<span data-ttu-id="01ab4-153">세 가지 방법으로 toodo 하기:</span><span class="sxs-lookup"><span data-stu-id="01ab4-153">There are three ways toodo it:</span></span>

- <span data-ttu-id="01ab4-154">Hello에서 Azure SQL 데이터베이스를 만들 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-154">An Azure SQL database can be created in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="01ab4-155">Hello 자습서에서는 특정 리소스 그룹 및 논리 서버 내에서 계산 및 저장소 리소스 집합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-155">In hello tutorial, you’ll use a specific set of compute and storage resources within a resource group and logical server.</span></span> <span data-ttu-id="01ab4-156">AdventureWorks라는 가상 회사의 샘플 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-156">You’ll use sample data from a fictitious company called AdventureWorks.</span></span> <span data-ttu-id="01ab4-157">서버 수준 방화벽 규칙도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-157">You’ll also create a server-level firewall rule.</span></span> <span data-ttu-id="01ab4-158">toolearn 어떻게 toodo이, 방문 hello [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](../sql-database/sql-database-get-started-portal.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-158">toolearn how toodo this, visit hello [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md) tutorial.</span></span>

  ![Azure SQL Database 만들기](media/how-to-discover-classify-personal-data-azure/create-database.png)
- <span data-ttu-id="01ab4-160">Hello에 SQL 데이터베이스를 만들 수도 있습니다 [Azure 클라우드 셸](https://azure.microsoft.com/features/cloud-shell/) CLI, 브라우저 기반 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-160">A SQL database can also be created in hello [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, a browser-based command-line tool.</span></span> <span data-ttu-id="01ab4-161">hello 도구 hello Azure 포털에서에서 사용할 수 있으며 여기에서 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-161">hello tool is available in hello Azure portal and can be run directly from there.</span></span> <span data-ttu-id="01ab4-162">이 자습서에서는 있습니다 hello 도구를 시작, 스크립트 변수를 정의 리소스 그룹을 만들고 논리 서버 및 서버 방화벽 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-162">In this tutorial, you launch hello tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="01ab4-163">샘플 데이터로 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-163">Then you create a database with sample data.</span></span> <span data-ttu-id="01ab4-164">toolearn 어떻게 toocreate 이러한 방식으로 데이터베이스 방문 hello [hello Azure CLI를 사용 하 여 단일 Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started-cli.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-164">toolearn how toocreate your database this way, visit hello [Create a single Azure SQL database using hello Azure CLI](../sql-database/sql-database-get-started-cli.md) tutorial.</span></span>

  ![CLIT 자습서](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
<span data-ttu-id="01ab4-166">Linux 관리자와 개발자는 일반적으로 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-166">Azure CLI is commonly used by Linux admins and developers.</span></span> <span data-ttu-id="01ab4-167">일부 사용자는 Azure CLI가 세 번째 옵션인 PowerShell보다 더 쉽고 직관적이라고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-167">Some users find it easier and more intuitive than PowerShell, which is your third option.</span></span>

- <span data-ttu-id="01ab4-168">마지막으로, 명령줄/스크립트 사용 되는 도구 toocreate PowerShell을 사용 하 여 SQL 데이터베이스를 만들고 Azure 및 기타 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-168">Finally, you can create a SQL database using PowerShell, which is a command line/script tool used toocreate and manage Azure and other resources.</span></span> <span data-ttu-id="01ab4-169">이 자습서에서는 있습니다 hello 도구를 시작, 스크립트 변수를 정의 리소스 그룹을 만들고 논리 서버 및 서버 방화벽 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-169">In this tutorial, you launch hello tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="01ab4-170">샘플 데이터로 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-170">Then you’ll create a database with sample data.</span></span>

<span data-ttu-id="01ab4-171">hello 자습서 hello Azure PowerShell 모듈 버전 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-171">hello tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="01ab4-172">Get-module-ListAvailable AzureRM toofind 버전을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-172">Run  Get-Module -ListAvailable AzureRM toofind your version.</span></span> <span data-ttu-id="01ab4-173">Tooinstall 또는 업그레이드를 할 경우 설치 하는 Azure PowerShell 모듈을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="01ab4-173">If you need tooinstall or upgrade, see Install Azure PowerShell module.</span></span>

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

<span data-ttu-id="01ab4-174">toolearn 어떻게 toocreate 이러한 방식으로 데이터베이스 방문 hello [Powershell을 사용 하 여 단일 Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started-powershell.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-174">toolearn how toocreate your database this way, visit hello [Create a single Azure SQL database using Powershell](../sql-database/sql-database-get-started-powershell.md) tutorial.</span></span>

>[!Note]
<span data-ttu-id="01ab4-175">Windows 관리자는 PowerShell toouse 경향이 해도 되지만 그 중 일부를 Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="01ab4-175">Windows admins tend toouse PowerShell, but some of them prefer Azure CLI.</span></span>

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a><span data-ttu-id="01ab4-176">SQL 데이터베이스 hello Azure 포털에서에서 개인 데이터를 검색 하려면 어떻게 해야 하나요? * *</span><span class="sxs-lookup"><span data-stu-id="01ab4-176">How do I search for personal data in SQL database in hello Azure portal?**</span></span>

<span data-ttu-id="01ab4-177">개인 데이터에 대 한 hello Azure 포털 toosearch 내 hello 기본 제공 쿼리 편집기 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-177">You can use hello built-in query editor tool inside hello Azure portal toosearch for personal data.</span></span> <span data-ttu-id="01ab4-178">SQL server 관리자 로그인 및 암호를 사용 하 여 toohello 도구에 로그인 하 고 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-178">You’ll log in toohello tool using your SQL server admin login and password, and then enter a query.</span></span>

  ![hello 포털을 사용 하 여 sql를 검색 합니다.](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

<span data-ttu-id="01ab4-180">Hello 자습서의 5 단계 hello 쿼리 편집기 창에서 예제 쿼리 보여주지만 (또한 두 테이블의에서 데이터를 결합 하 고 반환 되는 hello 데이터 집합의 hello 원본 열에 대 한 별칭을 만듭니다) 개인 정보나 기밀 정보에 집중 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-180">Step 5 of hello tutorial shows an example query in hello query editor pane, but it  doesn’t focus on personal or sensitive information(it also combines data from two tables and creates aliases for hello source column in hello data set being returned).</span></span> <span data-ttu-id="01ab4-181">hello 다음 스크린샷은 hello 쿼리 반환 되는 hello 결과 창와 5 단계에서:</span><span class="sxs-lookup"><span data-stu-id="01ab4-181">hello following screenshot shows hello query from Step 5 as well as hello results pane that’s returned:</span></span>

  ![쿼리 편집기](media/how-to-discover-classify-personal-data-azure/query-editor.png)

<span data-ttu-id="01ab4-183">데이터베이스가 MyTable이라고 하는 경우 개인 정보의 샘플 쿼리는 이름, 사회 보장 번호 및 ID 번호를 포함하고 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-183">If your database was called MyTable, a sample query for personal information might include name, Social Security number and ID number and would look like this:</span></span>

<span data-ttu-id="01ab4-184">“SELECT Name, SSN, ID number FROM MyTable”</span><span class="sxs-lookup"><span data-stu-id="01ab4-184">“SELECT Name, SSN, ID number FROM MyTable”</span></span>

<span data-ttu-id="01ab4-185">Hello 쿼리를 실행 하는 hello에서 hello 결과 확인 한 다음 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="01ab4-185">You’d run hello query and then see hello results in hello **Results** pane.</span></span>

<span data-ttu-id="01ab4-186">SQL tooquery hello Azure 포털에서에서 데이터베이스 하는 방법에 대 한 자세한 내용은 방문 hello [hello SQL 데이터베이스 쿼리](../sql-database/sql-database-get-started-portal.md) hello 자습서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-186">For more information on how tooquery a SQL database in hello Azure portal, visit hello [Query hello SQL database](../sql-database/sql-database-get-started-portal.md) section of hello tutorial.</span></span>

### <a name="how-do-i-search-for-data-across-multiple-databases"></a><span data-ttu-id="01ab4-187">여러 데이터베이스 간에 데이터를 검색하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="01ab4-187">How do I search for data across multiple databases?</span></span>

<span data-ttu-id="01ab4-188">SQL 탄력적 쿼리 (미리 보기) 하면 tooperform 데이터베이스 간 및 데이터베이스 쿼리를 여러 개 있으며 단일 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-188">SQL elastic query (preview) enables you tooperform cross-database and multiple database queries and return a single result.</span></span> <span data-ttu-id="01ab4-189">hello [자습서 개요](../sql-database/sql-database-elastic-query-overview.md) 시나리오에 대 한 자세한 설명 및 데이터베이스를 수직 및 수평 분할 hello 차이점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-189">hello [tutorial overview](../sql-database/sql-database-elastic-query-overview.md) includes a detailed description of scenarios and explains hello difference between vertical and horizontal database partitioning.</span></span> <span data-ttu-id="01ab4-190">행 분할은 “분할”이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-190">Horizontal partitioning is called “sharding.”</span></span>

  ![수직 분할](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![행 분할](media/how-to-discover-classify-personal-data-azure/horizontal.png)

<span data-ttu-id="01ab4-193">시작 tooget 방문 hello [Azure SQL 데이터베이스 탄력적 쿼리 개요 (미리 보기)](../sql-database/sql-database-elastic-query-overview.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="01ab4-193">tooget started, visit hello [Azure SQL Database elastic query overview (preview)](../sql-database/sql-database-elastic-query-overview.md) page.</span></span>

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a><span data-ttu-id="01ab4-194">파워 쿼리(Azure HDInsight Hadoop 클러스터 가져오기): 큰 데이터 집합의 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="01ab4-194">Power Query (for importing Azure HDInsight Hadoop clusters): data discovery for large data sets</span></span>

<span data-ttu-id="01ab4-195">Hadoop는 오픈 소스 Apache 저장소이며 Hadoop 클러스터에서 분석되고 저장되는 대규모 데이터 집합에 대한 처리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-195">Hadoop is an open source Apache storage and processing service for large data sets, which are analyzed and stored in Hadoop clusters.</span></span> <span data-ttu-id="01ab4-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) 사용자 toowork Hadoop으로 Azure의 클러스터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) allows users toowork with Hadoop clusters in Azure.</span></span> <span data-ttu-id="01ab4-197">파워 쿼리는 Excel 추가 기능으로 무엇보다도 사용자가 다양한 소스에서 데이터를 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-197">Power Query is an Excel add-in that, among other things, helps users discover data from different sources.</span></span>

<span data-ttu-id="01ab4-198">Azure HDInsight의 Hadoop 클러스터와 연결 된 개인 데이터에는 파워 쿼리를 통해 가져온된 tooExcel 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-198">Personal data associated with Hadoop clusters in Azure HDInsight can be imported tooExcel with Power Query.</span></span> <span data-ttu-id="01ab4-199">Hello 데이터는 Excel에 사용 하 여 쿼리 tooidentify 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-199">Once hello data is in Excel you can use a query tooidentify it.</span></span>

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a><span data-ttu-id="01ab4-200">사용 하는 방법 Excel 파워 쿼리 tooimport Hadoop 클러스터에서 Azure HDInsight를 Excel로?</span><span class="sxs-lookup"><span data-stu-id="01ab4-200">How do I use Excel Power Query tooimport Hadoop clusters in Azure HDInsight into Excel?</span></span>

<span data-ttu-id="01ab4-201">HDInsight 자습서에서는 이 전체 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-201">An HDInsight tutorial will walk you through this entire process.</span></span> <span data-ttu-id="01ab4-202">필수 구성 요소를 설명 하 고 링크 tooa 포함 [Azure HDInsight 시작](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-202">It explains prerequisites, and includes a link tooa [Get started with Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) tutorial.</span></span> <span data-ttu-id="01ab4-203">Excel 2016으로 2013 및 2010 지침은 (단계는 이전 버전의 Excel hello에 대 한 약간 다른).</span><span class="sxs-lookup"><span data-stu-id="01ab4-203">Instructions cover Excel 2016 as well as 2013 and 2010 (steps are slightly different for hello older versions of Excel).</span></span> <span data-ttu-id="01ab4-204">Hello Excel 파워 쿼리 추가 기능에 없다면 hello 자습서에서는 어떻게 tooget 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-204">If you don’t have hello Excel Power Query add-in, hello tutorial shows you how tooget it.</span></span> <span data-ttu-id="01ab4-205">Excel에서는 hello 자습서를 시작 합니다 및 toohave 클러스터와 연결 된 Azure Blob 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-205">You’ll start hello tutorial in Excel and will need toohave an Azure Blob storage account associated with your cluster.</span></span>

  ![Excel에서 쿼리](media/how-to-discover-classify-personal-data-azure/excel.png)

<span data-ttu-id="01ab4-207">toolearn 어떻게 toodo이, 방문 hello [파워 쿼리를 사용 하 여 Excel 연결 tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-207">toolearn how toodo this, visit hello [Connect Excel tooHadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) tutorial.</span></span>

<span data-ttu-id="01ab4-208">원본: [파워 쿼리를 사용 하 여 연결 Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="01ab4-208">Source: [Connect Excel tooHadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)</span></span>

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a><span data-ttu-id="01ab4-209">Azure Information Protection: 문서 및 전자 메일에 대한 개인 데이터 분류</span><span class="sxs-lookup"><span data-stu-id="01ab4-209">Azure Information Protection: personal data classification for documents and email</span></span>

<span data-ttu-id="01ab4-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) Azure 고객 레이블을 tooclassify 적용 내부나 외부 공유 문서를 보호 하 고 통신을 전자 메일로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) can help Azure customers apply labels tooclassify and protect internally or externally shared documents and email communications.</span></span> <span data-ttu-id="01ab4-211">이러한 항목 중 일부는 고객 또는 직원 개인 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-211">Some of these items may contain customer or employee personal information.</span></span> <span data-ttu-id="01ab4-212">관리자 또는 사용자가 자동 또는 수동으로 규칙 및 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-212">Rules and conditions can be defined automatically or manually, by administrators or by users.</span></span> <span data-ttu-id="01ab4-213">예를 들어 사용자가 신용 카드 정보를 포함 하는 문서를 저장 하는 경우 사용자는 볼 hello 관리자가 구성 된 레이블 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-213">For example, if a user is saving a document that includes credit card information, he or she would see a label recommendation that was configured by hello administrator.</span></span>

### <a name="how-do-i-try-it"></a><span data-ttu-id="01ab4-214">시도하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="01ab4-214">How do I try it?</span></span>

<span data-ttu-id="01ab4-215">Hello를 방문 하는 것이 조직에 적합 한 경우에 Azure Information Protection try toosee toogive 싶으면, [빠른 시작 자습서](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial)합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-215">If you’d like toogive Azure Information Protection a try toosee if it might be a fit for your organization, visit hello [Quickstart tutorial](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial).</span></span> <span data-ttu-id="01ab4-216">기본적인 다섯 단계로 안내 합니다-설치 tooconfiguring 정책 tooseeing 분류, 레이블 지정 및 공유 하 고 작업에서에서-30 분 이내로 수행 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-216">It walks you through five basic steps—from installation tooconfiguring policy tooseeing classification, labeling, and sharing in action—and should take less than a half hour.</span></span>

### <a name="how-do-i-deploy-it"></a><span data-ttu-id="01ab4-217">배포하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="01ab4-217">How do I deploy it?</span></span>

<span data-ttu-id="01ab4-218">조직에 대 한 Azure Information Protection toodeploy 싶으면, 방문 hello [분류, 레이블 지정 및 보호에 대 한 배포 로드맵을](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap)합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-218">If you’d like toodeploy Azure Information Protection for your organization, visit hello [deployment roadmap for classification, labeling, and protection](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).</span></span>

### <a name="is-there-anything-else-i-should-know"></a><span data-ttu-id="01ab4-219">알아야 할 다른 항목이 있나요?</span><span class="sxs-lookup"><span data-stu-id="01ab4-219">Is there anything else I should know?</span></span>

<span data-ttu-id="01ab4-220">충분히 검토 방법 tooset 그 방문 하는 데 도움이 되는 상호 보완적인 정보에 대 한 hello [준비를 설정 하 고, 보호!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span><span class="sxs-lookup"><span data-stu-id="01ab4-220">For complementary information that will help you think through how tooset it up, visit hello [Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span></span>
<span data-ttu-id="01ab4-221">블로그 게시물을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-221">blog post.</span></span> <span data-ttu-id="01ab4-222">및 검사 hello Azure Information Protection에 대 한 자세한 아래에 나열 된 링크에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-222">And check hello Learn more links listed below for more on Azure Information Protection.</span></span>

## <a name="azure-search-data-discovery-for-developer-apps"></a><span data-ttu-id="01ab4-223">Azure Search: 개발자 앱에 대한 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="01ab4-223">Azure Search: data discovery for developer apps</span></span>

<span data-ttu-id="01ab4-224">[Azure Search](https://azure.microsoft.com/services/search/)는 클라우드 검색 솔루션 개발자를 위한 기능이며 응용 프로그램에 다양한 데이터 검색 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-224">[Azure Search](https://azure.microsoft.com/services/search/) is a cloud search solution for developers, and provides a rich data search experience for your applications.</span></span> <span data-ttu-id="01ab4-225">Azure 검색 간에 Azure Cosmo DB, Azure SQL 데이터베이스, Azure Blob 저장소, Azure 테이블 저장소 또는 사용자 지정 고객 JSON 데이터에서 제공 하는 사용자 지정 인덱스, toolocate 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-225">Azure Search allows you toolocate data across user-defined indexes, sourced from Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table storage, or custom customer JSON data.</span></span> <span data-ttu-id="01ab4-226">Azure 검색 REST API toosearch hello를 사용 하 여 개인 데이터 형식이 나 특정 개인의 개인 데이터 hello에 대 한 Lucene 쿼리를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-226">You can also structure Lucene queries using hello Azure Search REST API toosearch for personal data types or hello personal data of specific individuals.</span></span> <span data-ttu-id="01ab4-227">기능에는 전체 텍스트 검색, 단순 쿼리 구문 및 Lucene 쿼리 구문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-227">Features include full text search, simple query syntax, and Lucene query syntax.</span></span> 

## <a name="how-do-i-use-sql-tooquery-data"></a><span data-ttu-id="01ab4-228">SQL tooquery 데이터를 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="01ab4-228">How do I use SQL tooquery data?</span></span>

<span data-ttu-id="01ab4-229">hello 기본 사항으로 toobegin 방문 hello [Azure CosmosD DB: 어떻게 SQL을 사용 하 여 tooquery](../cosmos-db/tutorial-query-documentdb.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-229">toobegin with hello basics, visit hello [Azure CosmosD DB: How tooquery using SQL](../cosmos-db/tutorial-query-documentdb.md) tutorial.</span></span> <span data-ttu-id="01ab4-230">hello 자습서 샘플 문서 및 두 개의 샘플 SQL 쿼리 및 결과 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-230">hello tutorial provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="01ab4-231">SQL 쿼리를 빌드하는 방법에 대한 자세한 지침은 [Azure Cosmos DB Document DB API에 대한 SQL 쿼리](../cosmos-db/documentdb-sql-query.md)를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-231">For more in-depth guidance on building SQL queries, visit [SQL queries for Azure Cosmos DB Document DB API.](../cosmos-db/documentdb-sql-query.md)</span></span>

<span data-ttu-id="01ab4-232">Toolearn 같은 toocreate 데이터베이스 컬렉션을 추가 하 고 데이터를 추가 하는 방법 방문 hello와 새 tooAzure Cosmos DB는 경우 [Azure Cosmos DB: DocumentDB API 웹 앱을 빌드할](../cosmos-db/create-documentdb-dotnet.md) 빠른 시작 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-232">If you’re new tooAzure Cosmos DB and would like toolearn how toocreate a database, add a collection, and add data, visit hello [Azure Cosmos DB: Build a DocumentDB API web app](../cosmos-db/create-documentdb-dotnet.md) Quickstart tutorial.</span></span> <span data-ttu-id="01ab4-233">Toodo 원하는 경우.NET, Java, Python, 같은 다른 언어에서이 선택 선호 하는 언어 toohello 사이트를 가져오면 합니다.</span><span class="sxs-lookup"><span data-stu-id="01ab4-233">If you’d like toodo this in a language other than .NET, such as Java or Python, just choose your preferred language once you get toohello site.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01ab4-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01ab4-234">Next steps</span></span>

[<span data-ttu-id="01ab4-235">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="01ab4-235">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50)

[<span data-ttu-id="01ab4-236">SQL Database 정의</span><span class="sxs-lookup"><span data-stu-id="01ab4-236">What is SQL Database?</span></span>](../sql-database/sql-database-technical-overview.md)

<span data-ttu-id="01ab4-237">[Azure Portal에서 사용할 수 있는 SQL Database 쿼리 편집기](https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span><span class="sxs-lookup"><span data-stu-id="01ab4-237">[SQL Database Query Editor available in Azure portal] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span></span>

[<span data-ttu-id="01ab4-238">Azure Information Protection이란?</span><span class="sxs-lookup"><span data-stu-id="01ab4-238">What is Azure Information Protection?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[<span data-ttu-id="01ab4-239">Azure Rights Management란?</span><span class="sxs-lookup"><span data-stu-id="01ab4-239">What is Azure Rights Management?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[<span data-ttu-id="01ab4-240">Azure Information Protection: 준비, 설정, 보호</span><span class="sxs-lookup"><span data-stu-id="01ab4-240">Azure Information Protection: Ready, set, protect!</span></span>](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
