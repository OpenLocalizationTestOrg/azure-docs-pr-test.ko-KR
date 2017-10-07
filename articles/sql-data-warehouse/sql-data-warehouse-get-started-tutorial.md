---
title: "aaaAzure SQL 데이터 웨어하우스-시작 자습서 | Microsoft Docs"
description: "이 자습서 방식에서는 Azure SQL 데이터 웨어하우스로 데이터 tooprovision 및 로드 합니다. 또한 배율, 일시 중지 및 튜닝 하는 방법에 대 한 hello 기본 사항을 알아봅니다."
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
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="68283-104">SQL Data Warehouse 시작</span><span class="sxs-lookup"><span data-stu-id="68283-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="68283-105">이 자습서에서는 어떻게 tooprovision 및 로드 데이터를 Azure SQL 데이터 웨어하우스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="68283-106">또한 배율, 일시 중지 및 튜닝 하는 방법에 대 한 hello 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68283-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="68283-107">완료 되 면 준비 tooquery 수 하 고 데이터 웨어하우스를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="68283-108">**예상 시간 toocomplete:** hello 필수 구성 요소를 충족 되 면 약 30 분 toocomplete를 사용 하는 예제 코드를 있는 종단 간 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="68283-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="68283-109">Prerequisites</span></span>

<span data-ttu-id="68283-110">hello 자습서에서는 SQL 데이터 웨어하우스 기본 개념에 익숙한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="68283-111">소개가 필요한 경우 [SQL Data Warehouse란 무엇입니까?](sql-data-warehouse-overview-what-is.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68283-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="68283-112">Microsoft Azure에 등록</span><span class="sxs-lookup"><span data-stu-id="68283-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="68283-113">Microsoft Azure 계정이 없는 경우이 서비스가 toosign toouse 하나에 대해 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="68283-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="68283-114">계정이 이미 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="68283-115">Toohello 계정 페이지를 탐색 [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="68283-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="68283-116">무료 Azure 계정을 만들거나 계정을 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="68283-117">Hello 지침에 따라</span><span class="sxs-lookup"><span data-stu-id="68283-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="68283-118">적절한 SQL 클라이언트 드라이버 및 도구 설치</span><span class="sxs-lookup"><span data-stu-id="68283-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="68283-119">대부분의 SQL 클라이언트 도구는 데이터 웨어하우스 tooSQL JDBC, ODBC 또는 ADO.NET을 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="68283-120">Toohello 많은 T-SQL 기능을 지 원하는 SQL 데이터 웨어하우스, 인해 일부 클라이언트 응용 프로그램 SQL 데이터 웨어하우스에 완전히 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="68283-121">Windows 운영 체제를 실행하는 경우 [Visual Studio] 또는 [SQL Server Management Studio]를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="68283-122">SQL Data Warehouse 만들기</span><span class="sxs-lookup"><span data-stu-id="68283-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="68283-123">SQL Data Warehouse는 방대한 병렬 처리를 위해 설계된 데이터베이스의 특수한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="68283-124">hello 데이터베이스 여러 노드에 분산 하 고 동시에 쿼리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="68283-125">SQL 데이터 웨어하우스에 모든 hello 노드의 hello 활동을 오케스트레이션 하는 제어.</span><span class="sxs-lookup"><span data-stu-id="68283-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="68283-126">hello 노드 자체 SQL 데이터베이스 toomanage 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="68283-127">SQL 데이터 웨어하우스를 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="68283-128">자세한 내용은 [SQL Data Warehouse 가격](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68283-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="68283-129">데이터 웨어하우스 만들기</span><span class="sxs-lookup"><span data-stu-id="68283-129">Create a data warehouse</span></span>

1. <span data-ttu-id="68283-130">Hello에 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="68283-131">**새로 만들기** > **데이터베이스** > **SQL Data Warehouse**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="68283-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="68283-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="68283-133">배포 세부 정보 작성</span><span class="sxs-lookup"><span data-stu-id="68283-133">Fill out deployment details</span></span>

    <span data-ttu-id="68283-134">**데이터베이스 이름**: 원하는 모든 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="68283-135">여러 데이터 웨어하우스를 설정한 경우 사용자 이름은 포함 hello 지역, 환경, 예를 들어 같은 세부 정보는 것이 좋습니다 *westus 1 테스트 mydw*합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="68283-136">**구독:** 사용자의 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="68283-137">**리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="68283-138">리소스 그룹은 범위 지정 액세스 제어 및 템플릿 배포와 같은 리소스 관리에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="68283-139">Azure 리소스 그룹 및 모범 사례에 대한 자세한 내용은 [여기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68283-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="68283-140">**원본**: 빈 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="68283-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="68283-141">**서버**: 선택 hello 서버에서 만든 [필수 구성 요소]합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="68283-142">**데이터 정렬**: hello 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="68283-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="68283-143">**성능 선택**: 표준 400DWU hello로 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="68283-144">선택 **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="68283-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="68283-145">데이터 웨어하우스 toodeploy 될 때까지 기다리는!</span><span class="sxs-lookup"><span data-stu-id="68283-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="68283-146">일반적이 프로세스 tootake 몇 분 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="68283-147">hello 포털 데이터 웨어하우스 준비 toouse 때이 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68283-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="68283-148">데이터 웨어하우스 tooSQL 연결</span><span class="sxs-lookup"><span data-stu-id="68283-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="68283-149">이 자습서에서는 SQL Server Management Studio (SSMS) tooconnect toohello 데이터 웨어하우스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="68283-150">이러한 지원 되는 커넥터를 통해 tooSQL 데이터 웨어하우스에 연결할 수 있습니다: ADO.NET, JDBC, ODBC 및 PHP 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="68283-151">Microsoft에서 지원하지 않는 도구의 경우 기능이 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="68283-152">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="68283-152">Get connection information</span></span>

<span data-ttu-id="68283-153">만든 hello 논리 SQL server 통해 tooconnect 해야 tooconnect tooyour 데이터 웨어하우스 [필수 구성 요소]합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="68283-154">Hello 대시보드 또는 리소스에 대 한 검색에서 데이터 웨어하우스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![SQL Data Warehouse 대시보드](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="68283-156">Hello hello 논리 SQL server에 대 한 전체 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-156">Find hello full name for hello logical SQL server.</span></span>

    ![서버 이름 선택](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="68283-158">SSMS를 열고 개체 탐색기 tooconnect toothis 서버 hello 서버 관리자 자격 증명에서 만든를 사용 하 여 사용 하 여 [필수 구성 요소]</span><span class="sxs-lookup"><span data-stu-id="68283-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![SSMS로 연결](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="68283-160">모두 올바르게 되 면 이제 연결된 tooyour 논리 SQL server을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="68283-161">로그온 한 hello 서버 관리자도 이후 hello master 데이터베이스를 포함 하 여 hello 서버에서 호스트 되는 tooany 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="68283-162">하나의 서버 관리자 계정은 않으며 권한이 hello 대부분의 모든 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="68283-163">주의 하지 tooallow 조직 tooknow hello 관리자 암호에 사용자가 너무 많습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="68283-164">Azure Active Directory 관리자 계정도 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="68283-165">여기에 hello 세부 정보 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-165">We don't provide hello details here.</span></span> <span data-ttu-id="68283-166">Azure Active Directory 인증을 사용 하는 방법에 대 한 자세한 toolearn 참조 [Azure AD 인증](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="68283-167">다음으로, 로그인 및 사용자를 추가로 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="68283-168">데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68283-168">Create a database user</span></span>

<span data-ttu-id="68283-169">이 단계에서는 사용자 계정 tooaccess 데이터 웨어하우스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68283-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="68283-170">또한 보여줍니다 어떻게 toogive 해당 사용자 hello 기능 toorun는 다량의 메모리 및 CPU 리소스 사용을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="68283-171">리소스 tooqueries를 할당 하기 위한 리소스 클래스에 대 한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="68283-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="68283-172">tookeep 프로덕션 데이터베이스에 안전 하 고, 데이터 hello 서버 관리자 toorun 쿼리를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="68283-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="68283-173">권한이 hello 대부분의 모든 사용자 및 tooperform 하기를 사용 하 여 사용자 데이터에 대 한 작업 데이터 위험에 놓이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="68283-174">또한 서버 admin 님 안녕하세요 tooperform 관리 작업은 제공 하 고, 이후 작업 메모리 및 CPU 리소스의 작은 할당만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68283-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="68283-175">SQL 데이터 웨어하우스 리소스 클래스, 메모리, CPU 리소스 및 동시성 슬롯 toousers tooallocate 다른 금액을 호출 하는 미리 정의 된 데이터베이스 역할을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="68283-176">각 사용자 tooa 소형, 중형, 대형 또는 초대형 리소스 클래스에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="68283-177">hello 사용자의 리소스 클래스 hello 리소스 hello 사용자에 게 확인 toorun 쿼리 및 로드 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="68283-178">최적의 데이터 압축에 대 한 hello 사용자 tooload와 대형 또는 초대형 리소스 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="68283-179">리소스 클래스에 대한 자세한 내용은 [여기](./sql-data-warehouse-develop-concurrency.md#resource-classes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68283-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="68283-180">데이터베이스를 제어할 수 있는 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="68283-180">Create an account that can control a database</span></span>

<span data-ttu-id="68283-181">Hello 서버 관리자에 현재 로그온 되어 권한 toocreate 로그인 및 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="68283-182">SSMS 또는 또 하나의 쿼리 클라이언트를 사용하여 **master**에 대한 새 쿼리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68283-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![master에서의 새 쿼리](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![master1에서의 새 쿼리](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="68283-185">Hello 쿼리 창에서 한 MedRCLogin 라는 로그인 및 사용자 라는 LoadingUser T-SQL 명령 toocreate이를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="68283-186">이 로그인 toohello 논리 SQL server에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="68283-187">이제 쿼리 하는 hello *SQL 데이터 웨어하우스 데이터베이스*, 기반 데이터베이스 사용자 만들기 hello tooaccess를 만든 로그인 되 고 hello 데이터베이스에 대 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="68283-188">NYT 라는 hello 데이터베이스 사용자 제어 권한을 toohello 데이터베이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="68283-189">데이터베이스 이름에 하이픈 인 경우 수 있는지 toowrap 대괄호에!</span><span class="sxs-lookup"><span data-stu-id="68283-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="68283-190">Hello 사용자 중간 리소스 할당을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="68283-191">이 T-SQL 명령 toomake 실행 it mediumrc 라는 hello 중간 리소스 클래스의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="68283-192">클릭 [여기](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn 동시성 및 리소스 클래스에 대 한 자세한!</span><span class="sxs-lookup"><span data-stu-id="68283-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="68283-193">Hello 새 자격 증명으로 toohello 논리 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="68283-193">Connect toohello logical server with hello new credentials</span></span>

    ![새 로그인으로 로그인](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="68283-195">Azure Blob 저장소에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="68283-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="68283-196">이제 준비 tooload 데이터를 데이터 웨어하우스에.</span><span class="sxs-lookup"><span data-stu-id="68283-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="68283-197">이 단계에서는 tooload 뉴욕시 택시 cab 데이터를 공용 Azure 저장소에서에서 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68283-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="68283-198">SQL 데이터 웨어하우스로 tooload 데이터 toofirst는 일반적으로 hello 데이터 tooAzure blob 저장소를 이동한 다음 데이터 웨어하우스에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="68283-199">toomake 것 보다 쉽게 toounderstand 어떻게 tooload, 우리 뉴욕 택시 cab 데이터 될 공용 Azure 저장소 blob에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="68283-200">나중에 참조할 수, toolearn 어떻게 tooget 데이터 tooAzure blob 저장소 또는 tooload 것 직접 SQL 데이터 웨어하우스로 원본의 참조 hello [개요 로드](sql-data-warehouse-overview-load.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="68283-201">외부 데이터 정의</span><span class="sxs-lookup"><span data-stu-id="68283-201">Define external data</span></span>

1. <span data-ttu-id="68283-202">마스터 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68283-202">Create a master key.</span></span> <span data-ttu-id="68283-203">마스터 키가 데이터베이스에 한 번씩 toocreate를 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68283-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="68283-204">Hello hello 택시 cab 데이터를 포함 하는 Azure blob의 hello 위치를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="68283-205">Hello 외부 파일 형식 정의</span><span class="sxs-lookup"><span data-stu-id="68283-205">Define hello external file formats</span></span>

    <span data-ttu-id="68283-206">hello ```CREATE EXTERNAL FILE FORMAT``` 명령에 사용 되는 toospecify hello 외부 데이터를 포함 하는 파일의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="68283-207">여기에는 구분 기호라고 하는 하나 이상의 문자로 구분된 텍스트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="68283-208">데모용으로 hello 택시 cab 데이터 압축 되지 않은 데이터 및 gzip 압축 된 데이터로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68283-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="68283-209">이러한 실행 T-SQL 명령을 toodefine는 두 가지 형식: 압축을 풀고 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

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

4.  <span data-ttu-id="68283-210">외부 파일 형식에 대한 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68283-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="68283-211">Hello 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68283-211">Create hello external tables.</span></span> <span data-ttu-id="68283-212">이 테이블은 Azure Blob Storage에 저장된 데이터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="68283-213">다음 T-SQL 명령을 toocreate hello는 모든 지점 toohello Azure blob에서는 이전에 정의 된 외부 데이터 원본에 여러 외부 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

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

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="68283-214">Azure blob 저장소의 hello 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="68283-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="68283-215">SQL Data Warehouse는 CTAS(CREATE TABLE AS SELECT)라는 핵심 문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="68283-216">이 문은 select 문의 hello 결과에 따라 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68283-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="68283-217">hello 새 테이블에 hello 결과 hello의 select 문 처럼 동일한 열과 데이터 형식을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="68283-218">이 세련 된 방법 tooimport 데이터를 사용 하 여 SQL 데이터 웨어하우스로 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="68283-219">이 스크립트 tooimport 데이터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-219">Run this script tooimport your data.</span></span>

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

2. <span data-ttu-id="68283-220">로드되는 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="68283-220">View your data as it loads.</span></span>

   <span data-ttu-id="68283-221">몇 GB의 데이터를 로드하고 고성능 클러스터형 columnstore 인덱스에 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="68283-222">Hello 다음 동적 관리 뷰 (Dmv) tooshow hello 상태의 hello 부하를 사용 하 여 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="68283-223">Hello 쿼리를 시작한 후 SQL 데이터 웨어하우스는 몇 가지 중요 한 역할을 커피 및는 스낵을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="68283-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
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

3. <span data-ttu-id="68283-224">모든 시스템 쿼리를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="68283-225">Azure SQL Data Warehouse에 로드된 데이터를 즐깁니다.</span><span class="sxs-lookup"><span data-stu-id="68283-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![로드된 데이터 보기](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="68283-227">쿼리 성능 향상</span><span class="sxs-lookup"><span data-stu-id="68283-227">Improve query performance</span></span>

<span data-ttu-id="68283-228">여러 가지 방법으로 tooimprove 쿼리 성능 및 SQL 데이터 웨어하우스 않는 tooachieve hello 고속 성능을 tooprovide 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="68283-229">쿼리 성능에 크기 조정의 hello 효과를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="68283-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="68283-230">한 가지 방법은 tooimprove 쿼리 성능이 데이터 웨어하우스에 대 한 hello DWU 서비스 수준을 변경 하 여 tooscale 리소스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68283-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="68283-231">각 서비스 수준은 더 많은 비용을 소요하지만 언제든지 리소스를 축소하거나 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="68283-232">이 단계에서는 두 가지 서로 다른 DWU 설정에서 성능을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="68283-233">첫째, 보겠습니다 too100 DWU 하므로 방법을 한 계산 노드의 아이디어를 얻을 수 있습니다는 자체적으로 수행할 수 아래로 hello 크기 조정의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="68283-234">Toohello 포털 이동 하 고 SQL 데이터 웨어하우스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="68283-235">SQL 데이터 웨어하우스 블레이드에서 hello 표시줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![포털에서 DW 크기 조정](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="68283-237">Too100 DWU 막대 hello 성능이 저하 비율과 저장 적중 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![크기 조정 및 저장](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="68283-239">크기 조정 작업 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="68283-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="68283-240">Hello 눈금을 변경 하는 동안 쿼리를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="68283-241">크기 조정 시 현재 실행 중인 쿼리를 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="68283-242">이러한 다시 hello 작업이 완료 되 면 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="68283-243">모든 hello 열에 대 한 hello 상위 백만 항목을 선택 하면 hello 여행 데이터에서 검색 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="68283-244">에 신속 하 게 eager toomove 인 경우 행 수를 줄여 무료 tooselect 느낍니다.</span><span class="sxs-lookup"><span data-stu-id="68283-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="68283-245">Hello 시간이 toorun이이 작업을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="68283-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="68283-246">데이터 웨어하우스 확장 too400 DWU를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="68283-247">다른 계산 노드 tooyour Azure SQL 데이터 웨어하우스를 추가 하는 각 100 DWU를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="68283-248">Hello 쿼리를 다시 실행!</span><span class="sxs-lookup"><span data-stu-id="68283-248">Run hello query again!</span></span> <span data-ttu-id="68283-249">상당한 차이에 주목해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="68283-250">Hello 쿼리가 많은 데이터를 반환 하기 때문에 성능 병목 현상 hello 대역폭 가용성 SSMS를 실행 하는 hello 컴퓨터의 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="68283-251">따라서 성능이 하나도 개선되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="68283-252">SQL Data Warehouse는 대규모 병렬 처리를 사용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="68283-253">Azure SQL 데이터 웨어하우스의 hello 진정한 강점은 경험 하는 검사 또는 수백만 행에서 분석 기능을 수행 하는 쿼리.</span><span class="sxs-lookup"><span data-stu-id="68283-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="68283-254">쿼리 성능에 통계의 hello 효과를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="68283-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="68283-255">조인 hello hello 여행 테이블과 날짜 테이블을 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="68283-255">Run a query that joins hello Date table with hello Trip table</span></span>

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

    <span data-ttu-id="68283-256">SQL 데이터 웨어하우스 hello 조인을 수행 하기 전에 tooshuffle 데이터에 있기 때문에이 쿼리 약간의 시간이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68283-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="68283-257">조인 하지 않은 tooshuffle 데이터 디자인 된 toojoin 데이터 hello에 있더라도 동일한 방식으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68283-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="68283-258">이는 보다 심층적인 주제입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="68283-259">통계를 통해 차이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="68283-260">Hello 조인 열에서이 문 toocreate 통계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="68283-261">SQL DW에서는 통계를 자동으로 관리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="68283-262">통계는 쿼리 성능에 중요하며, 통계를 만들고 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68283-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="68283-263">**이점이 hello 대부분 조인, GROUP by 절 및 열을 찾을 위치 hello에 사용 되는 열에 포함 된 열에서 통계를 포함 하면 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="68283-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="68283-264">필수 구성 요소에서 hello 쿼리를 다시 실행 하 고 성능 차이 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="68283-265">쿼리 성능 면에서 차이가 hello로 수직 확장으로 급격 한 됩니다 하는 동안는 속도 높이고를 알게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="68283-266">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68283-266">Next steps</span></span>

<span data-ttu-id="68283-267">이제 tooquery 준비 하 고 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="68283-268">모범 사례 또는 팁을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68283-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="68283-269">완료 되 면 hello 날에 대 한 탐색 확인 되었는지 toopause 인스턴스에!</span><span class="sxs-lookup"><span data-stu-id="68283-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="68283-270">프로덕션 환경에서 일시 중지 및 toomeet 크기 조정 하 여 상당한 절감 발생할 수 있는 비즈니스 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="68283-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![일시 중지](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="68283-272">유용한 정보</span><span class="sxs-lookup"><span data-stu-id="68283-272">Useful readings</span></span>

<span data-ttu-id="68283-273">[동시성 및 워크로드 관리][]</span><span class="sxs-lookup"><span data-stu-id="68283-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="68283-274">[Azure SQL 데이터 웨어하우스에 대한 모범 사례][]</span><span class="sxs-lookup"><span data-stu-id="68283-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="68283-275">[쿼리 모니터링][]</span><span class="sxs-lookup"><span data-stu-id="68283-275">[Query Monitoring][]</span></span>

<span data-ttu-id="68283-276">[대규모 관계형 데이터 웨어하우스를 구축하기 위한 상위 10가지 모범 사례][](영문)</span><span class="sxs-lookup"><span data-stu-id="68283-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="68283-277">[마이그레이션 데이터 tooAzure SQL 데이터 웨어하우스][]</span><span class="sxs-lookup"><span data-stu-id="68283-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[동시성 및 워크로드 관리]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL 데이터 웨어하우스에 대한 모범 사례]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[쿼리 모니터링]: sql-data-warehouse-manage-monitor.md
[대규모 관계형 데이터 웨어하우스를 구축하기 위한 상위 10가지 모범 사례]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/(영문)
[마이그레이션 데이터 tooAzure SQL 데이터 웨어하우스]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[필수 구성 요소]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
