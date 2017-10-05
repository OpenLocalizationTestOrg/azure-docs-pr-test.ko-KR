---
title: "Azure SQL Data Warehouse - 시작 자습서 | Microsoft Docs"
description: "이 자습서에서는 데이터를 프로비전하고 Azure SQL Data Warehouse로 로드하는 방법을 배웁니다. 또한 크기 조정, 일시 중지 및 튜닝에 대한 기본 사항을 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 95e14824ba3b705bb909ec983652dd3305b98805
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="e0dd6-104">SQL Data Warehouse 시작</span><span class="sxs-lookup"><span data-stu-id="e0dd6-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="e0dd6-105">이 자습서에서는 데이터를 프로비전하고 Azure SQL Data Warehouse로 로드하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e0dd6-106">또한 크기 조정, 일시 중지 및 튜닝에 대한 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="e0dd6-107">작업이 끝나면 데이터 웨어하우스를 쿼리 및 탐색할 준비가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="e0dd6-108">**예상 완료 시간:** 예제 코드가 포함된 종단 간 자습서로, 필수 조건을 충족한 후 완료하는 데 약 30분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e0dd6-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0dd6-109">Prerequisites</span></span>

<span data-ttu-id="e0dd6-110">이 자습서에서는 SQL Data Warehouse 기본 개념에 대해 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="e0dd6-111">소개가 필요한 경우 [SQL Data Warehouse란 무엇입니까?](sql-data-warehouse-overview-what-is.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="e0dd6-112">Microsoft Azure에 등록</span><span class="sxs-lookup"><span data-stu-id="e0dd6-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="e0dd6-113">Microsoft Azure 계정이 없는 아직 경우 이 서비스를 사용하려면 Microsoft Azure에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="e0dd6-114">계정이 이미 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="e0dd6-115">계정 페이지([https://azure.microsoft.com/account/](https://azure.microsoft.com/account/))로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="e0dd6-116">무료 Azure 계정을 만들거나 계정을 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="e0dd6-117">지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="e0dd6-118">적절한 SQL 클라이언트 드라이버 및 도구 설치</span><span class="sxs-lookup"><span data-stu-id="e0dd6-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="e0dd6-119">대부분의 SQL 클라이언트 도구는 JDBC, ODBC 또는 ADO.NET을 사용하여 SQL Data Warehouse에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="e0dd6-120">SQL Data Warehouse에서 지원하는 많은 T-SQL 기능으로 인해 일부 클라이언트 응용 프로그램은 SQL Data Warehouse와 완벽하게 호환되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="e0dd6-121">Windows 운영 체제를 실행하는 경우 [Visual Studio] 또는 [SQL Server Management Studio]를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="e0dd6-122">SQL Data Warehouse 만들기</span><span class="sxs-lookup"><span data-stu-id="e0dd6-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="e0dd6-123">SQL Data Warehouse는 방대한 병렬 처리를 위해 설계된 데이터베이스의 특수한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="e0dd6-124">데이터베이스는 여러 노드에 배포되고 쿼리를 병렬로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="e0dd6-125">SQL Data Warehouse에는 모든 노드의 활동을 조정하는 제어 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="e0dd6-126">노드 자체가 SQL Database를 사용하여 데이터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="e0dd6-127">SQL Data Warehouse를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="e0dd6-128">자세한 내용은 [SQL Data Warehouse 가격](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="e0dd6-129">데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="e0dd6-129">Create a data warehouse</span></span>

1. <span data-ttu-id="e0dd6-130">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e0dd6-131">**새로 만들기** > **데이터베이스** > **SQL Data Warehouse**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="e0dd6-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="e0dd6-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="e0dd6-133">배포 세부 정보 작성</span><span class="sxs-lookup"><span data-stu-id="e0dd6-133">Fill out deployment details</span></span>

    <span data-ttu-id="e0dd6-134">**데이터베이스 이름**: 원하는 모든 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="e0dd6-135">데이터 웨어하우스가 여러 개 있는 경우, 지역, 환경 등과 같은 자세한 정보를 포함하는 것이 좋습니다(예: *mydw-westus-1-test*).</span><span class="sxs-lookup"><span data-stu-id="e0dd6-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="e0dd6-136">**구독:** 사용자의 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="e0dd6-137">**리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e0dd6-138">리소스 그룹은 범위 지정 액세스 제어 및 템플릿 배포와 같은 리소스 관리에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="e0dd6-139">Azure 리소스 그룹 및 모범 사례에 대한 자세한 내용은 [여기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="e0dd6-140">**원본**: 빈 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e0dd6-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="e0dd6-141">**서버**: [필수 조건]에서 만든 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="e0dd6-142">**데이터 정렬**: 기본 데이터 정렬(SQL_Latin1_General_CP1_CI_AS)을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="e0dd6-143">**성능 선택**: 표준 400DWU로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="e0dd6-144">**대시보드에 고정** ![대시보드에 고정](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-144">Choose **Pin to dashboard** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="e0dd6-145">데이터 웨어하우스가 배포될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="e0dd6-146">일반적으로 이 프로세스는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="e0dd6-147">포털은 데이터 웨어하우스를 사용할 준비가 되면 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="e0dd6-148">SQL Data Warehouse에 연결</span><span class="sxs-lookup"><span data-stu-id="e0dd6-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="e0dd6-149">이 자습서에서는 SSMS(SQL Server Management Studio)를 사용하여 데이터 웨어하우스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="e0dd6-150">지원되는 커넥터인 ADO.NET, JDBC, ODBC 및 PHP를 통해 SQL Data Warehouse에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="e0dd6-151">Microsoft에서 지원하지 않는 도구의 경우 기능이 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="e0dd6-152">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="e0dd6-152">Get connection information</span></span>

<span data-ttu-id="e0dd6-153">데이터 웨어하우스에 연결하려면 [필수 조건]에서 만든 논리 SQL Server를 통해 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="e0dd6-154">대시보드에서 데이터 웨어하우스를 선택하거나 리소스에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![SQL Data Warehouse 대시보드](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="e0dd6-156">논리 SQL 서버의 전체 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-156">Find the full name for the logical SQL server.</span></span>

    ![서버 이름 선택](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="e0dd6-158">SSMS를 열고 개체 탐색기를 사용하여 [필수 조건]에서 만든 서버 관리 자격 증명을 사용하여 이 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![SSMS로 연결](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="e0dd6-160">모든 것이 제대로 수행되었으면 이제 논리 SQL 서버에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="e0dd6-161">서버 관리자로서 로그인했기 때문에 마스터 데이터베이스와 같은 서버에 의해 호스팅되는 모든 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="e0dd6-162">서버 관리자 계정은 하나만 있으며 대부분의 사용자 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="e0dd6-163">조직의 너무 많은 사람들이 관리자 암호를 알지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="e0dd6-164">Azure Active Directory 관리자 계정도 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="e0dd6-165">여기에는 세부 정보를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-165">We don't provide the details here.</span></span> <span data-ttu-id="e0dd6-166">Azure Active Directory 인증을 사용하는 방법에 대한 자세한 내용은 [Azure AD 인증](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="e0dd6-167">다음으로, 로그인 및 사용자를 추가로 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="e0dd6-168">데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e0dd6-168">Create a database user</span></span>

<span data-ttu-id="e0dd6-169">이 단계에서는 데이터 웨어하우스에 액세스할 수 있는 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="e0dd6-170">또한 해당 사용자에게 많은 양의 메모리 및 CPU 리소스를 사용하는 쿼리를 실행하는 권한을 제공하는 방법도 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="e0dd6-171">리소스를 쿼리에 할당하는 리소스 클래스에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="e0dd6-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="e0dd6-172">데이터를 안전하게 유지하려면 프로덕션 데이터베이스에서 서버 관리자를 사용하여 쿼리를 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="e0dd6-173">대부분의 사용자 권한을 가지며 사용자 데이터에 대해 작업을 수행하기 사용하면 사용자 데이터가 위험해집니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="e0dd6-174">또한 서버 관리자는 관리 작업을 수행하기 위한 것이기 때문에, 메모리 및 CPU 리소스가 적게 할당된 작업만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="e0dd6-175">SQL Data Warehouse는 리소스 클래스라고 하는 미리 정의된 데이터베이스 역할을 사용하여 서로 다른 양의 메모리, CPU 리소스, 동시성 슬롯을 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="e0dd6-176">각 사용자는 소형, 중형, 대형 또는 초대형 리소스 클래스에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="e0dd6-177">사용자의 리소스 클래스는 사용자가 쿼리를 실행하고 작업을 로드해야 하는 리소스를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="e0dd6-178">데이터 압축을 최적화하기 위해 사용자는 대형 또는 초대형 리소스 할당을 사용하여 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="e0dd6-179">리소스 클래스에 대한 자세한 내용은 [여기](./sql-data-warehouse-develop-concurrency.md#resource-classes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="e0dd6-180">데이터베이스를 제어할 수 있는 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e0dd6-180">Create an account that can control a database</span></span>

<span data-ttu-id="e0dd6-181">현재 서버 관리자로서 로그인되어 있으므로 로그인 및 사용자를 만들 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="e0dd6-182">SSMS 또는 또 하나의 쿼리 클라이언트를 사용하여 **master**에 대한 새 쿼리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![master에서의 새 쿼리](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![master1에서의 새 쿼리](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="e0dd6-185">쿼리 창에서 MedRCLogin라는 로그인과 LoadingUser라는 사용자를 만들려면 이 T-SQL 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="e0dd6-186">이 로그인은 논리적 SQL 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="e0dd6-187">이제 *SQL Data Warehouse 데이터베이스*를 쿼리하여 데이터베이스에서 액세스하고 작업을 수행하기 위해 만든 로그인을 기반으로 하는 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="e0dd6-188">데이터베이스 사용자에게 NYT라고 하는 데이터베이스에 대한 제어 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="e0dd6-189">데이터베이스 이름에 하이픈(-)이 있으면 대괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="e0dd6-190">사용자에게 중간 리소스 할당 제공</span><span class="sxs-lookup"><span data-stu-id="e0dd6-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="e0dd6-191">이 T-SQL 명령을 실행하여 사용자를 mediumrc라고 하는 중간 리소스 클래스의 멤버로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="e0dd6-192">동시성 및 리소스 클래스에 대한 자세한 내용을 보려면 [여기](sql-data-warehouse-develop-concurrency.md#resource-classes)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="e0dd6-193">새 자격 증명으로 논리 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="e0dd6-193">Connect to the logical server with the new credentials</span></span>

    ![새 로그인으로 로그인](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="e0dd6-195">Azure Blob 저장소에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="e0dd6-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="e0dd6-196">이제 데이터를 데이터 웨어하우스에 로드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="e0dd6-197">이 단계에서는 공용 Azure Storage Blob에서 뉴욕시 택시 데이터를 로드하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="e0dd6-198">데이터를 SQL Data Warehouse로 로드하는 일반적인 방법은 먼저 Azure Blob Storage로 데이터를 이동한 다음 사용자의 데이터 웨어하우스를 로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="e0dd6-199">로드하는 방법을 쉽게 이해하기 위해 공용 Azure Storage Blob에서 이미 호스팅된 뉴욕 택시 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="e0dd6-200">나중에 참조하기 위해 데이터를 Azure Blob Storage로 가져오거나 원본에서 SQL Data Warehouse로 직접 로드하는 방법에 대해 알아보려면 [로드 개요](sql-data-warehouse-overview-load.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="e0dd6-201">외부 데이터 정의</span><span class="sxs-lookup"><span data-stu-id="e0dd6-201">Define external data</span></span>

1. <span data-ttu-id="e0dd6-202">마스터 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-202">Create a master key.</span></span> <span data-ttu-id="e0dd6-203">데이터베이스마다 한 번씩 마스터 키를 만들기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="e0dd6-204">택시 데이터를 포함하는 Azure Blob의 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="e0dd6-205">외부 파일 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-205">Define the external file formats</span></span>

    <span data-ttu-id="e0dd6-206">```CREATE EXTERNAL FILE FORMAT``` 명령은 외부 데이터를 포함하는 파일 형식을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="e0dd6-207">여기에는 구분 기호라고 하는 하나 이상의 문자로 구분된 텍스트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="e0dd6-208">데모용으로 택시 데이터는 압축되지 않은 데이터와 gzip 형식의 압축 데이터로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="e0dd6-209">이들 T-SQL 명령을 실행하여 비압축 및 압축 등 두 가지 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="e0dd6-210">외부 파일 형식에 대한 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="e0dd6-211">외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-211">Create the external tables.</span></span> <span data-ttu-id="e0dd6-212">이 테이블은 Azure Blob Storage에 저장된 데이터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="e0dd6-213">다음 T-SQL 명령을 실행하여 외부 데이터 원본에서 이전에 정의한 Azure Blob을 모두 가리키는 다수의 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="e0dd6-214">Azure Blob Storage에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="e0dd6-215">SQL Data Warehouse는 CTAS(CREATE TABLE AS SELECT)라는 핵심 문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="e0dd6-216">이 문은 select 문의 결과에 따라 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="e0dd6-217">새 테이블은 select 문의 결과에 부합하는 동일한 열과 데이터 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="e0dd6-218">Azure Blob Storage에서 SQL Data Warehouse로 데이터를 가져오는 효과적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="e0dd6-219">이 스크립트를 실행하여 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-219">Run this script to import your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="e0dd6-220">로드되는 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-220">View your data as it loads.</span></span>

   <span data-ttu-id="e0dd6-221">몇 GB의 데이터를 로드하고 고성능 클러스터형 columnstore 인덱스에 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="e0dd6-222">DMV(동적 관리 보기)를 사용하는 다음과 같은 쿼리를 실행하여 로드 상태를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="e0dd6-223">쿼리를 시작한 후 SQL Data Warehouse에서 몇 가지 주요 작업을 수행하는 동안 커피 또는 스낵을 즐기세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="e0dd6-224">모든 시스템 쿼리를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="e0dd6-225">Azure SQL Data Warehouse에 로드된 데이터를 즐깁니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![로드된 데이터 보기](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="e0dd6-227">쿼리 성능 향상</span><span class="sxs-lookup"><span data-stu-id="e0dd6-227">Improve query performance</span></span>

<span data-ttu-id="e0dd6-228">SQL Data Warehouse가 개선시켜야 하는 쿼리 성능 향상과 고속 성능을 달성하기 위한 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="e0dd6-229">쿼리 성능에 대한 크기 조정 효과 참조</span><span class="sxs-lookup"><span data-stu-id="e0dd6-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="e0dd6-230">쿼리 성능을 개선하는 한 가지 방법은 데이터 웨어하우스에 대한 DWU 서비스 수준을 변경하여 리소스의 크기를 조정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="e0dd6-231">각 서비스 수준은 더 많은 비용을 소요하지만 언제든지 리소스를 축소하거나 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="e0dd6-232">이 단계에서는 두 가지 서로 다른 DWU 설정에서 성능을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="e0dd6-233">먼저, 작업을 100DWU로 축소하여 하나의 계산 노드에서 자체적으로 수행할 수 있는 방법에 대한 아이디어를 얻을 수 있도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="e0dd6-234">포털로 이동하여 SQL Data Warehouse를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="e0dd6-235">SQL Data Warehouse 블레이드에서 [크기 조정]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![포털에서 DW 크기 조정](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="e0dd6-237">성능 막대를 100DWU로 낮추고 [저장]을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![크기 조정 및 저장](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="e0dd6-239">크기 조정 작업이 끝날 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e0dd6-240">크기를 조정하는 동안에는 쿼리를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="e0dd6-241">크기 조정 시 현재 실행 중인 쿼리를 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="e0dd6-242">작업이 완료되면 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="e0dd6-243">모든 열에 대해 상위 1백만 개 항목을 선택하여 여행 데이터에서 스캔 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="e0dd6-244">신속하게 넘어가려면 더 적은 수의 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="e0dd6-245">이 작업을 실행하는 데 걸린 시간을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="e0dd6-246">데이터 웨어하우스를 400DWU로 다시 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="e0dd6-247">각각의 100DWU는 Azure SQL Data Warehouse에 또 다른 계산 노드를 추가한다는 것을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="e0dd6-248">쿼리를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-248">Run the query again!</span></span> <span data-ttu-id="e0dd6-249">상당한 차이에 주목해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e0dd6-250">쿼리가 많은 데이터를 반환하기 때문에 SSMS를 실행하는 컴퓨터의 대역폭 가용성에 성능 병목 상태가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-250">Because the query returns a lot of data, the bandwidth availability of the machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="e0dd6-251">따라서 성능이 하나도 개선되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="e0dd6-252">SQL Data Warehouse는 대규모 병렬 처리를 사용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="e0dd6-253">수백만 개의 행에서 검색 또는 분석 기능을 수행하는 쿼리를 통해 Azure SQL Data Warehouse의 진정한 능력을 경험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-253">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="e0dd6-254">쿼리 성능에 대한 통계 효과 참조</span><span class="sxs-lookup"><span data-stu-id="e0dd6-254">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="e0dd6-255">Date 테이블과 Trip 테이블을 조인하는 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-255">Run a query that joins the Date table with the Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="e0dd6-256">SQL Data Warehouse는 조인을 수행하기 전에 데이터 순서를 섞어야 하므로 이 쿼리는 다소 시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-256">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="e0dd6-257">배포된 방식과 같게 데이터를 조인하도록 설계된 경우에는 조인 시 데이터를 섞지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-257">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="e0dd6-258">이는 보다 심층적인 주제입니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="e0dd6-259">통계를 통해 차이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="e0dd6-260">이 문을 실행하여 조인 열에 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-260">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="e0dd6-261">SQL DW에서는 통계를 자동으로 관리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="e0dd6-262">통계는 쿼리 성능에 중요하며, 통계를 만들고 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="e0dd6-263">**조인에 포함된 열, WHERE 절에 사용된 열 및 GROUP BY에 있는 열에서 통계를 유지하면 가장 많은 이득을 획득할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="e0dd6-263">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="e0dd6-264">필수 조건에서 쿼리를 다시 실행하고 성능 차이를 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-264">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="e0dd6-265">쿼리 성능의 차이는 확장하는 만큼 급격한 것은 아니지만 속도 향상에 주목해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-265">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e0dd6-266">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0dd6-266">Next steps</span></span>

<span data-ttu-id="e0dd6-267">이제 쿼리하고 탐색할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-267">You're now ready to query and explore.</span></span> <span data-ttu-id="e0dd6-268">모범 사례 또는 팁을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="e0dd6-269">하루 종일 탐색하는 경우 인스턴스를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-269">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="e0dd6-270">프로덕션 환경에서는 비즈니스 요구에 맞게 일시 중지 및 크기 조정하여 상당한 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0dd6-270">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![일시 중지](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="e0dd6-272">유용한 정보</span><span class="sxs-lookup"><span data-stu-id="e0dd6-272">Useful readings</span></span>

<span data-ttu-id="e0dd6-273">[동시성 및 워크로드 관리][]</span><span class="sxs-lookup"><span data-stu-id="e0dd6-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="e0dd6-274">[Azure SQL 데이터 웨어하우스에 대한 모범 사례][]</span><span class="sxs-lookup"><span data-stu-id="e0dd6-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="e0dd6-275">[쿼리 모니터링][]</span><span class="sxs-lookup"><span data-stu-id="e0dd6-275">[Query Monitoring][]</span></span>

<span data-ttu-id="e0dd6-276">[대규모 관계형 데이터 웨어하우스를 구축하기 위한 상위 10가지 모범 사례][](영문)</span><span class="sxs-lookup"><span data-stu-id="e0dd6-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="e0dd6-277">[Azure SQL Data Warehouse로 데이터 마이그레이션][](영문)</span><span class="sxs-lookup"><span data-stu-id="e0dd6-277">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[동시성 및 워크로드 관리]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL 데이터 웨어하우스에 대한 모범 사례]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[쿼리 모니터링]: sql-data-warehouse-manage-monitor.md
[대규모 관계형 데이터 웨어하우스를 구축하기 위한 상위 10가지 모범 사례]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/(영문)
[Azure SQL Data Warehouse로 데이터 마이그레이션]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/(영문)



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[필수 조건]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
