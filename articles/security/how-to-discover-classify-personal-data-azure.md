---
title: "Microsoft Azure에서 개인 데이터 검색, 식별 및 분류 | Microsoft Docs"
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
ms.openlocfilehash: 6ccb064a9a76e7041d4f365b3997673dc9182e0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a><span data-ttu-id="39813-103">Microsoft Azure에서 개인 데이터 검색, 식별 및 분류</span><span class="sxs-lookup"><span data-stu-id="39813-103">Discover, identify, and classify personal data in Microsoft Azure</span></span>

<span data-ttu-id="39813-104">이 문서에서는 Azure Data Catalog, Azure Active Directory, SQL Database, Azure HDInsight의 Hadoop 클러스터에 대한 파워 쿼리, Azure Information Protection, Azure Search 및 Azure Cosmos DB용 SQL 쿼리를 비롯한 여러 Azure 도구와 서비스에서 개인 데이터를 검색, 식별 및 분류하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-104">This article provides guidance on how to discover, identify, and classify personal data in several Azure tools and services, including using Azure Data Catalog, Azure Active Directory, SQL Database, Power Query for Hadoop clusters in Azure HDInsight, Azure Information Protection, Azure Search, and SQL queries for Azure Cosmos DB.</span></span>

## <a name="scenario-problem-statement-and-goal"></a><span data-ttu-id="39813-105">시나리오, 문제 설명 및 목표</span><span class="sxs-lookup"><span data-stu-id="39813-105">Scenario, problem statement, and goal</span></span>

<span data-ttu-id="39813-106">미국 기반 스포츠 회사는 다양한 개인 데이터 및 기타 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-106">A U.S.-based sports company collects a variety of personal and other data.</span></span> <span data-ttu-id="39813-107">고객 및 직원 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-107">This includes customers and employee data.</span></span> <span data-ttu-id="39813-108">회사는 데이터를 여러 데이터베이스에 유지하고 해당 Azure 환경에서 여러 다른 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-108">The company keeps it in multiple databases, and stores it in several different locations in their Azure environment.</span></span> <span data-ttu-id="39813-109">스포츠 장비 판매 외에도 EU를 비롯한 전 세계에서 유명한 운동 이벤트에 대한 등록을 호스트하고 관리하며 경우에 따라 수집한 고객 데이터는 의료 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-109">In addition to selling sports equipment, they also host and manage registration for elite athletic events around the world, including in the EU, and in some cases the customer data they collect includes medical information.</span></span>

<span data-ttu-id="39813-110">회사가 매년 많은 국제 자전거 투어를 호스트하고 전 세계의 여러 위치에 직원을 파견하기 때문에 몇 가지 데이터 집합의 규모가 매우 큽니다.</span><span class="sxs-lookup"><span data-stu-id="39813-110">Since the company hosts many international bicycling tours every year and has contingent staff in locations around the globe, a couple of the data sets are quite large.</span></span> <span data-ttu-id="39813-111">회사에는 고객 및 직원이 모두 사용하는 개발자 빌드 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-111">The company also has developer-built applications that are used by both customers and employees.</span></span>

<span data-ttu-id="39813-112">회사에서는 다음과 같은 문제를 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-112">The company wants to address the following problems:</span></span>

- <span data-ttu-id="39813-113">고객 및 직원 개인 데이터는 적절한 액세스 및 보안을 보장하기 위해 회사에서 수집하는 다른 데이터와 분류/구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-113">Customer and employee personal data must be classified/distinguished from the other data the company collects in order to ensure proper access and security.</span></span>
- <span data-ttu-id="39813-114">데이터 관리자는 Azure 환경의 다양한 영역에 걸친 고객 개인 데이터의 위치를 쉽게 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-114">The data admin needs to easily discover the location of customer personal data across various areas of the Azure environment.</span></span>
- <span data-ttu-id="39813-115">공유 문서 및 전자 메일 통신에 표시되는 고객 및 직원 개인 데이터의 보안을 유지할 수 있도록 레이블이 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-115">Customer and employee personal data that appears in shared documents and email communications must be labeled to help ensure that it’s kept secure.</span></span>
- <span data-ttu-id="39813-116">회사의 앱 개발자는 웹 및 모바일 앱에서 고객 및 직원 개인 데이터를 쉽게 검색할 수 있는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-116">The company’s app developers need a way to easily search for customer and employee personal data in their web and mobile apps.</span></span>
- <span data-ttu-id="39813-117">또한 개발자는 개인 데이터에 대한 해당 문서 데이터베이스를 쿼리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-117">Developers also need to query their document database for personal data.</span></span>

### <a name="company-goals"></a><span data-ttu-id="39813-118">회사 목표</span><span class="sxs-lookup"><span data-stu-id="39813-118">Company goals</span></span>

- <span data-ttu-id="39813-119">모든 고객 및 직원 개인 데이터를 쉽게 찾을 수 있도록 Azure Data Catalog에서 태그가 지정되거나 주석이 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-119">All customer and employee personal data must be tagged/annotated in Azure Data Catalog so it can be found easily.</span></span> <span data-ttu-id="39813-120">이상적으로 고객 및 직원 개인 데이터는 별도로 태그가 지정되거나 주석이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="39813-120">Ideally customer and employee personal data are tagged/annotated separately.</span></span>
- <span data-ttu-id="39813-121">고객 및 직원 사용자 프로필의 개인 데이터 및 Azure Active Directory에 있는 작업 정보는 쉽게 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-121">Personal data from customer and employee user profiles and work information residing in Azure Active Directory must be easily located.</span></span>
- <span data-ttu-id="39813-122">여러 SQL Databases에 있는 개인 데이터를 쉽게 쿼리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-122">Personal data residing in multiple SQL databases must be easily queried.</span></span> 
- <span data-ttu-id="39813-123">회사의 대규모 데이터 집합의 일부는 Azure HDInsight를 통해 관리되고 Hadoop에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="39813-123">Some of the company’s large data sets are managed through Azure HDInsight and stored in Hadoop.</span></span> <span data-ttu-id="39813-124">해당 데이터는 개인 데이터를 쿼리할 수 있도록 Excel로 가져올 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-124">They must be imported into Excel so they can be queried for personal data.</span></span>
- <span data-ttu-id="39813-125">문서 및 전자 메일 통신에서 공유된 개인 데이터는 Azure Information Protection에서 분류되고 레이블이 지정되고 안전하게 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="39813-125">Personal data shared in documents and email communications must be classified, labeled, and kept secure with Azure Information Protection.</span></span>
- <span data-ttu-id="39813-126">회사의 앱 개발자는 Azure Search에서와 같이 빌드된 앱에서 고객 및 직원 개인 데이터를 검색할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-126">The company’s app developers must be able to discover customer and employee personal data in the apps they’ve built, which they can do with Azure Search.</span></span>
- <span data-ttu-id="39813-127">개발자는 해당 문서 데이터베이스에서 개인 데이터를 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-127">Developers must be able to find personal data in their document database.</span></span>

## <a name="azure-active-directory-data-discovery"></a><span data-ttu-id="39813-128">Azure Active Directory: 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="39813-128">Azure Active Directory: Data discovery</span></span>

<span data-ttu-id="39813-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="39813-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="39813-130">[Azure Portal](https://portal.azure.com/)을 사용하여 [AAD(Azure Active Directory)](https://azure.microsoft.com/services/active-directory/) 환경에서 개인 데이터를 포함하는 고객 및 직원 사용자 프로필 및 사용자 작업 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-130">You can locate customer and employee user profiles and user work information that contain personal data in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="39813-131">특정 사용자에 대한 개인 데이터를 찾거나 변경하려는 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-131">This is particularly helpful if you want to find or change personal data for a specific user.</span></span> <span data-ttu-id="39813-132">또한 사용자 프로필 및 작업 정보를 추가하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-132">You can also add or change user profile and work information.</span></span> <span data-ttu-id="39813-133">디렉터리에 대한 전역 관리자인 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-133">You must sign in with an account that’s a global admin for the directory.</span></span>

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a><span data-ttu-id="39813-134">사용자 프로필 및 작업 정보를 찾고 보려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-134">How do I locate or view user profile and work information?</span></span>

1. <span data-ttu-id="39813-135">디렉터리에 대한 전역 관리자인 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-135">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="39813-136">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-136">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 프로필 및 작업 정보를 찾으려면 어떻게 할까요?](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. <span data-ttu-id="39813-138">**사용자 및 그룹** 블레이드에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-138">On the **Users and groups** blade, select **Users**.</span></span>

  ![사용자 및 그룹 열기](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. <span data-ttu-id="39813-140">**사용자 및 그룹 - 사용자** 블레이드에서 목록의 사용자를 선택한 다음 선택한 사용자에 대한 블레이드에서 **프로필**을 선택하여 개인 데이터를 포함할 수 있는 사용자 프로필 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-140">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view user profile information that might contain personal data.</span></span>

  ![사용자 선택](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. <span data-ttu-id="39813-142">사용자 프로필 정보를 추가하거나 변경해야 하는 경우 명령 모음에서 수행한 후에 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-142">If you need to add or change user profile information, you can do so, and then, in the command bar, select **Save.**</span></span>
6. <span data-ttu-id="39813-143">선택한 사용자에 대한 블레이드에서 **작업 정보**를 선택하여 개인 데이터를 포함할 수 있는 사용자 작업 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-143">On the blade for the selected user, select **Work Info** to view user work information that may contain personal data.</span></span>

 ![작업 정보 보기](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. <span data-ttu-id="39813-145">사용자 작업 정보를 추가하거나 변경해야 하는 경우 명령 모음에서 수행한 후에 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-145">If you need to add or change user work information, you can do so, and then, in the command bar, select **Save.**</span></span>

## <a name="azure-sql-database-data-discovery"></a><span data-ttu-id="39813-146">Azure SQL Database: 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="39813-146">Azure SQL Database: Data discovery</span></span>

<span data-ttu-id="39813-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)는 개발자가 응용 프로그램을 빌드하고 유지하는 데 유용한 클라우드 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="39813-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span> <span data-ttu-id="39813-148">표준 SQL 쿼리를 사용하여 개인 데이터를 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-148">Personal data can be found in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries.</span></span> <span data-ttu-id="39813-149">Azure SQL 탄력적 쿼리(미리 보기)를 사용하면 데이터베이스 간 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-149">Azure SQL elastic query (preview) enables users to perform cross-database queries.</span></span>

<span data-ttu-id="39813-150">자세한 [SQL Database](../sql-database/sql-database-technical-overview.md) 자습서에서는 데이터 쿼리를 빌드하고 실행하는 방법을 포함하여 SQL Database를 사용하는 여러 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-150">A detailed [SQL database](../sql-database/sql-database-technical-overview.md) tutorial explains many aspects of using a SQL database, including how to build one and how to run data queries.</span></span> <span data-ttu-id="39813-151">특정 섹션에 대한 링크가 있는 자습서에서 사용할 수 있는 정보의 요약은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-151">The following is a summary of the information available in the tutorial with links to specific sections.</span></span>

### <a name="how-do-i-build-a-sql-database"></a><span data-ttu-id="39813-152">SQL Database를 빌드하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-152">How do I build a SQL database?</span></span>

<span data-ttu-id="39813-153">수행할 수 있는 세 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-153">There are three ways to do it:</span></span>

- <span data-ttu-id="39813-154">[Azure Portal](https://portal.azure.com/)에서 Azure SQL Database를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-154">An Azure SQL database can be created in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="39813-155">이 자습서에서는 리소스 그룹 및 논리 서버 내에서 계산 및 저장소 리소스의 특정 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-155">In the tutorial, you’ll use a specific set of compute and storage resources within a resource group and logical server.</span></span> <span data-ttu-id="39813-156">AdventureWorks라는 가상 회사의 샘플 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-156">You’ll use sample data from a fictitious company called AdventureWorks.</span></span> <span data-ttu-id="39813-157">서버 수준 방화벽 규칙도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39813-157">You’ll also create a server-level firewall rule.</span></span> <span data-ttu-id="39813-158">이를 수행하는 방법을 알아보려면 [Azure Portal에서 Azure SQL Database 만들기](../sql-database/sql-database-get-started-portal.md) 자습서를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-158">To learn how to do this, visit the [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md) tutorial.</span></span>

  ![Azure SQL Database 만들기](media/how-to-discover-classify-personal-data-azure/create-database.png)
- <span data-ttu-id="39813-160">SQL Database는 브라우저 기반 명령줄 도구인 [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI에서 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-160">A SQL database can also be created in the [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, a browser-based command-line tool.</span></span> <span data-ttu-id="39813-161">이 도구는 Azure Portal에서 사용할 수 있으며 거기서 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-161">The tool is available in the Azure portal and can be run directly from there.</span></span> <span data-ttu-id="39813-162">이 자습서에서는 도구를 시작하고, 스크립트 변수를 정의하고, 리소스 그룹 및 논리 서버를 만들고, 서버 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-162">In this tutorial, you launch the tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="39813-163">샘플 데이터로 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39813-163">Then you create a database with sample data.</span></span> <span data-ttu-id="39813-164">이러한 방식으로 데이터베이스를 만드는 방법을 알아보려면 [Azure CLI를 사용하여 단일 Azure SQL Database 만들기](../sql-database/sql-database-get-started-cli.md) 자습서를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-164">To learn how to create your database this way, visit the [Create a single Azure SQL database using the Azure CLI](../sql-database/sql-database-get-started-cli.md) tutorial.</span></span>

  ![CLIT 자습서](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
<span data-ttu-id="39813-166">Linux 관리자와 개발자는 일반적으로 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-166">Azure CLI is commonly used by Linux admins and developers.</span></span> <span data-ttu-id="39813-167">일부 사용자는 Azure CLI가 세 번째 옵션인 PowerShell보다 더 쉽고 직관적이라고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-167">Some users find it easier and more intuitive than PowerShell, which is your third option.</span></span>

- <span data-ttu-id="39813-168">마지막으로 Azure 및 기타 리소스를 만들고 관리하는 데 사용하는 명령줄/스크립트 도구인 PowerShell을 사용하여 SQL Database를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-168">Finally, you can create a SQL database using PowerShell, which is a command line/script tool used to create and manage Azure and other resources.</span></span> <span data-ttu-id="39813-169">이 자습서에서는 도구를 시작하고, 스크립트 변수를 정의하고, 리소스 그룹 및 논리 서버를 만들고, 서버 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-169">In this tutorial, you launch the tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="39813-170">샘플 데이터로 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39813-170">Then you’ll create a database with sample data.</span></span>

<span data-ttu-id="39813-171">자습서에는 Azure PowerShell 모듈 버전 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-171">The tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="39813-172">Get-module-ListAvailable AzureRM을 실행하여 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-172">Run  Get-Module -ListAvailable AzureRM to find your version.</span></span> <span data-ttu-id="39813-173">설치 또는 업그레이드해야 하는 경우 Azure PowerShell 모듈 설치를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39813-173">If you need to install or upgrade, see Install Azure PowerShell module.</span></span>

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

<span data-ttu-id="39813-174">이러한 방식으로 데이터베이스를 만드는 방법을 알아보려면 [Powershell을 사용하여 단일 Azure SQL Database 만들기](../sql-database/sql-database-get-started-powershell.md) 자습서를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-174">To learn how to create your database this way, visit the [Create a single Azure SQL database using Powershell](../sql-database/sql-database-get-started-powershell.md) tutorial.</span></span>

>[!Note]
<span data-ttu-id="39813-175">Windows 관리자는 PowerShell을 사용하는 경향이 있지만 일부는 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-175">Windows admins tend to use PowerShell, but some of them prefer Azure CLI.</span></span>

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-the-azure-portal"></a><span data-ttu-id="39813-176">Azure Portal의 SQL Database에서 개인 데이터를 검색하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="39813-176">How do I search for personal data in SQL database in the Azure portal?**</span></span>

<span data-ttu-id="39813-177">개인 데이터를 검색하기 위해 Azure Portal 내에서 기본 제공 쿼리 편집기 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-177">You can use the built-in query editor tool inside the Azure portal to search for personal data.</span></span> <span data-ttu-id="39813-178">SQL Server 관리자 로그인 및 암호를 사용하여 도구에 로그인하고 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-178">You’ll log in to the tool using your SQL server admin login and password, and then enter a query.</span></span>

  ![포털을 사용하여 SQL 검색](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

<span data-ttu-id="39813-180">자습서의 5단계에서는 쿼리 편집기 창에서 예제 쿼리를 보여주지만 개인 정보나 중요한 정보에 집중하지 않습니다.(또한 두 테이블의 데이터를 결합하고 반환되는 데이터 집합에서 원본 열의 별칭을 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="39813-180">Step 5 of the tutorial shows an example query in the query editor pane, but it  doesn’t focus on personal or sensitive information(it also combines data from two tables and creates aliases for the source column in the data set being returned).</span></span> <span data-ttu-id="39813-181">다음 스크린샷에서는 반환되는 결과 창뿐만 아니라 5단계의 쿼리를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="39813-181">The following screenshot shows the query from Step 5 as well as the results pane that’s returned:</span></span>

  ![쿼리 편집기](media/how-to-discover-classify-personal-data-azure/query-editor.png)

<span data-ttu-id="39813-183">데이터베이스가 MyTable이라고 하는 경우 개인 정보의 샘플 쿼리는 이름, 사회 보장 번호 및 ID 번호를 포함하고 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-183">If your database was called MyTable, a sample query for personal information might include name, Social Security number and ID number and would look like this:</span></span>

<span data-ttu-id="39813-184">“SELECT Name, SSN, ID number FROM MyTable”</span><span class="sxs-lookup"><span data-stu-id="39813-184">“SELECT Name, SSN, ID number FROM MyTable”</span></span>

<span data-ttu-id="39813-185">쿼리를 실행한 후 **결과** 창에서 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-185">You’d run the query and then see the results in the **Results** pane.</span></span>

<span data-ttu-id="39813-186">Azure Portal의 SQL Database를 쿼리하는 방법에 대한 자세한 내용은 자습서의 [SQL Database 쿼리](../sql-database/sql-database-get-started-portal.md) 섹션을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-186">For more information on how to query a SQL database in the Azure portal, visit the [Query the SQL database](../sql-database/sql-database-get-started-portal.md) section of the tutorial.</span></span>

### <a name="how-do-i-search-for-data-across-multiple-databases"></a><span data-ttu-id="39813-187">여러 데이터베이스 간에 데이터를 검색하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-187">How do I search for data across multiple databases?</span></span>

<span data-ttu-id="39813-188">SQL 탄력적인 쿼리(미리 보기)를 사용하면 데이터베이스 및 여러 데이터베이스 쿼리 간에 작업을 수행하고 단일 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-188">SQL elastic query (preview) enables you to perform cross-database and multiple database queries and return a single result.</span></span> <span data-ttu-id="39813-189">[자습서 개요](../sql-database/sql-database-elastic-query-overview.md)는 시나리오에 대한 자세한 설명을 포함하고 수직 및 행 데이터베이스 분할 간에 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-189">The [tutorial overview](../sql-database/sql-database-elastic-query-overview.md) includes a detailed description of scenarios and explains the difference between vertical and horizontal database partitioning.</span></span> <span data-ttu-id="39813-190">행 분할은 “분할”이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-190">Horizontal partitioning is called “sharding.”</span></span>

  ![수직 분할](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![행 분할](media/how-to-discover-classify-personal-data-azure/horizontal.png)

<span data-ttu-id="39813-193">시작하려면 [Azure SQL Database 탄력적 쿼리 개요(미리 보기)](../sql-database/sql-database-elastic-query-overview.md) 페이지를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-193">To get started, visit the [Azure SQL Database elastic query overview (preview)](../sql-database/sql-database-elastic-query-overview.md) page.</span></span>

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a><span data-ttu-id="39813-194">파워 쿼리(Azure HDInsight Hadoop 클러스터 가져오기): 큰 데이터 집합의 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="39813-194">Power Query (for importing Azure HDInsight Hadoop clusters): data discovery for large data sets</span></span>

<span data-ttu-id="39813-195">Hadoop는 오픈 소스 Apache 저장소이며 Hadoop 클러스터에서 분석되고 저장되는 대규모 데이터 집합에 대한 처리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="39813-195">Hadoop is an open source Apache storage and processing service for large data sets, which are analyzed and stored in Hadoop clusters.</span></span> <span data-ttu-id="39813-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/)를 사용하면 Azure에서 Hadoop 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) allows users to work with Hadoop clusters in Azure.</span></span> <span data-ttu-id="39813-197">파워 쿼리는 Excel 추가 기능으로 무엇보다도 사용자가 다양한 소스에서 데이터를 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-197">Power Query is an Excel add-in that, among other things, helps users discover data from different sources.</span></span>

<span data-ttu-id="39813-198">파워 쿼리를 사용하여 Azure HDInsight의 Hadoop 클러스터와 연결된 개인 데이터를 Excel로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-198">Personal data associated with Hadoop clusters in Azure HDInsight can be imported to Excel with Power Query.</span></span> <span data-ttu-id="39813-199">데이터가 Excel 형식이면 쿼리를 사용하여 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-199">Once the data is in Excel you can use a query to identify it.</span></span>

#### <a name="how-do-i-use-excel-power-query-to-import-hadoop-clusters-in-azure-hdinsight-into-excel"></a><span data-ttu-id="39813-200">Excel 파워 쿼리를 사용하여 Azure HDInsight의 Hadoop 클러스터를 Excel로 가져오려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-200">How do I use Excel Power Query to import Hadoop clusters in Azure HDInsight into Excel?</span></span>

<span data-ttu-id="39813-201">HDInsight 자습서에서는 이 전체 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-201">An HDInsight tutorial will walk you through this entire process.</span></span> <span data-ttu-id="39813-202">필수 구성 요소를 설명하고 [Azure HDInsight 시작](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) 자습서에 대한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-202">It explains prerequisites, and includes a link to a [Get started with Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) tutorial.</span></span> <span data-ttu-id="39813-203">지침은 Excel 2016, 2013 및 2010을 다룹니다(단계는 이전 버전의 Excel와 약간 다름).</span><span class="sxs-lookup"><span data-stu-id="39813-203">Instructions cover Excel 2016 as well as 2013 and 2010 (steps are slightly different for the older versions of Excel).</span></span> <span data-ttu-id="39813-204">Excel 파워 쿼리 추가 기능이 설치되지 않은 경우 이 자습서에서는 가져오는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="39813-204">If you don’t have the Excel Power Query add-in, the tutorial shows you how to get it.</span></span> <span data-ttu-id="39813-205">Excel에서 자습서를 시작하고 클러스터와 연결된 Azure Blob Storage 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-205">You’ll start the tutorial in Excel and will need to have an Azure Blob storage account associated with your cluster.</span></span>

  ![Excel에서 쿼리](media/how-to-discover-classify-personal-data-azure/excel.png)

<span data-ttu-id="39813-207">이 작업을 수행하는 방법을 알아보려면 [파워 쿼리를 사용하여 Hadoop에 Excel 연결](../hdinsight/hdinsight-connect-excel-power-query.md) 자습서를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-207">To learn how to do this, visit the [Connect Excel to Hadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) tutorial.</span></span>

<span data-ttu-id="39813-208">소스: [파워 쿼리를 사용하여 Hadoop에 Excel 연결](../hdinsight/hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="39813-208">Source: [Connect Excel to Hadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)</span></span>

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a><span data-ttu-id="39813-209">Azure Information Protection: 문서 및 전자 메일에 대한 개인 데이터 분류</span><span class="sxs-lookup"><span data-stu-id="39813-209">Azure Information Protection: personal data classification for documents and email</span></span>

<span data-ttu-id="39813-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection)을 통해 Azure 고객이 내부나 외부에서 공유 문서 및 전자 메일 통신을 분류하고 보호하는 레이블을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) can help Azure customers apply labels to classify and protect internally or externally shared documents and email communications.</span></span> <span data-ttu-id="39813-211">이러한 항목 중 일부는 고객 또는 직원 개인 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-211">Some of these items may contain customer or employee personal information.</span></span> <span data-ttu-id="39813-212">관리자 또는 사용자가 자동 또는 수동으로 규칙 및 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-212">Rules and conditions can be defined automatically or manually, by administrators or by users.</span></span> <span data-ttu-id="39813-213">예를 들어 사용자가 신용 카드 정보를 포함하는 문서를 저장하는 경우 관리자가 구성한 레이블 권장 사항을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39813-213">For example, if a user is saving a document that includes credit card information, he or she would see a label recommendation that was configured by the administrator.</span></span>

### <a name="how-do-i-try-it"></a><span data-ttu-id="39813-214">시도하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-214">How do I try it?</span></span>

<span data-ttu-id="39813-215">조직에는 적합한지 확인하기 위해 Azure Information Protection을 사용해 보려는 경우 [빠른 시작 자습서](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial)를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-215">If you’d like to give Azure Information Protection a try to see if it might be a fit for your organization, visit the [Quickstart tutorial](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial).</span></span> <span data-ttu-id="39813-216">설치, 정책 구성, 분류 확인, 레이블 지정, 작업 중 공유 등 다섯 가지 기본 단계를 30분 이내에 설명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-216">It walks you through five basic steps—from installation to configuring policy to seeing classification, labeling, and sharing in action—and should take less than a half hour.</span></span>

### <a name="how-do-i-deploy-it"></a><span data-ttu-id="39813-217">배포하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-217">How do I deploy it?</span></span>

<span data-ttu-id="39813-218">조직에 Azure Information Protection을 배포하려는 경우 [분류, 레이블 지정 및 보호를 위한 배포 로드맵](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-218">If you’d like to deploy Azure Information Protection for your organization, visit the [deployment roadmap for classification, labeling, and protection](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).</span></span>

### <a name="is-there-anything-else-i-should-know"></a><span data-ttu-id="39813-219">알아야 할 다른 항목이 있나요?</span><span class="sxs-lookup"><span data-stu-id="39813-219">Is there anything else I should know?</span></span>

<span data-ttu-id="39813-220">설정하는 방법을 검토하는 데 도움이 되는 상호 보완적인 정보는 [준비, 설정, 보호](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span><span class="sxs-lookup"><span data-stu-id="39813-220">For complementary information that will help you think through how to set it up, visit the [Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span></span>
<span data-ttu-id="39813-221">블로그 게시물을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-221">blog post.</span></span> <span data-ttu-id="39813-222">Azure Information Protection에 대한 자세한 내용은 아래 나열된 링크 자세히 알아보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-222">And check the Learn more links listed below for more on Azure Information Protection.</span></span>

## <a name="azure-search-data-discovery-for-developer-apps"></a><span data-ttu-id="39813-223">Azure Search: 개발자 앱에 대한 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="39813-223">Azure Search: data discovery for developer apps</span></span>

<span data-ttu-id="39813-224">[Azure Search](https://azure.microsoft.com/services/search/)는 클라우드 검색 솔루션 개발자를 위한 기능이며 응용 프로그램에 다양한 데이터 검색 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-224">[Azure Search](https://azure.microsoft.com/services/search/) is a cloud search solution for developers, and provides a rich data search experience for your applications.</span></span> <span data-ttu-id="39813-225">Azure Search를 사용하면 Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table 저장소 또는 사용자 지정 고객 JSON 데이터에서 소싱된 사용자 정의 인덱스에서 데이터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-225">Azure Search allows you to locate data across user-defined indexes, sourced from Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table storage, or custom customer JSON data.</span></span> <span data-ttu-id="39813-226">개인 데이터 형식 또는 특정 개인의 개인 데이터를 검색하도록 Azure Search REST API를 사용하여 Lucene 쿼리를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39813-226">You can also structure Lucene queries using the Azure Search REST API to search for personal data types or the personal data of specific individuals.</span></span> <span data-ttu-id="39813-227">기능에는 전체 텍스트 검색, 단순 쿼리 구문 및 Lucene 쿼리 구문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="39813-227">Features include full text search, simple query syntax, and Lucene query syntax.</span></span> 

## <a name="how-do-i-use-sql-to-query-data"></a><span data-ttu-id="39813-228">SQL을 사용하여 데이터를 쿼리하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="39813-228">How do I use SQL to query data?</span></span>

<span data-ttu-id="39813-229">기본 사항을 시작하려면 [Azure CosmosD DB: SQL을 사용하여 쿼리하는 방법](../cosmos-db/tutorial-query-documentdb.md) 자습서를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-229">To begin with the basics, visit the [Azure CosmosD DB: How to query using SQL](../cosmos-db/tutorial-query-documentdb.md) tutorial.</span></span> <span data-ttu-id="39813-230">이 자습서에서는 샘플 문서 및 두 가지 샘플 SQL 쿼리와 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-230">The tutorial provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="39813-231">SQL 쿼리를 빌드하는 방법에 대한 자세한 지침은 [Azure Cosmos DB Document DB API에 대한 SQL 쿼리](../cosmos-db/documentdb-sql-query.md)를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-231">For more in-depth guidance on building SQL queries, visit [SQL queries for Azure Cosmos DB Document DB API.](../cosmos-db/documentdb-sql-query.md)</span></span>

<span data-ttu-id="39813-232">Azure Cosmos DB 처음 사용하고 데이터베이스 만들기, 컬렉션 추가, 데이터 추가 방법을 알아보려는 경우 [Azure Cosmos DB: DocumentDB API 웹앱 빌드](../cosmos-db/create-documentdb-dotnet.md) 빠른 시작 자습서를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-232">If you’re new to Azure Cosmos DB and would like to learn how to create a database, add a collection, and add data, visit the [Azure Cosmos DB: Build a DocumentDB API web app](../cosmos-db/create-documentdb-dotnet.md) Quickstart tutorial.</span></span> <span data-ttu-id="39813-233">Java, Python과 같은 .NET 이외의 언어로 작업을 수행하려는 경우 사이트를 가져오면 기본 설정된 언어를 선택하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="39813-233">If you’d like to do this in a language other than .NET, such as Java or Python, just choose your preferred language once you get to the site.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39813-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39813-234">Next steps</span></span>

[<span data-ttu-id="39813-235">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="39813-235">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50)

[<span data-ttu-id="39813-236">SQL Database 정의</span><span class="sxs-lookup"><span data-stu-id="39813-236">What is SQL Database?</span></span>](../sql-database/sql-database-technical-overview.md)

<span data-ttu-id="39813-237">[Azure Portal에서 사용할 수 있는 SQL Database 쿼리 편집기](https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span><span class="sxs-lookup"><span data-stu-id="39813-237">[SQL Database Query Editor available in Azure portal] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span></span>

[<span data-ttu-id="39813-238">Azure Information Protection이란?</span><span class="sxs-lookup"><span data-stu-id="39813-238">What is Azure Information Protection?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[<span data-ttu-id="39813-239">Azure Rights Management란?</span><span class="sxs-lookup"><span data-stu-id="39813-239">What is Azure Rights Management?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[<span data-ttu-id="39813-240">Azure Information Protection: 준비, 설정, 보호</span><span class="sxs-lookup"><span data-stu-id="39813-240">Azure Information Protection: Ready, set, protect!</span></span>](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
