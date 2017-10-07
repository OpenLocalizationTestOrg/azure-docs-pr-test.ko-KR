---
title: "aaaLoad 데이터를 Azure SQL 데이터 웨어하우스에 – Data Factory | Microsoft Docs"
description: "이 자습서에서는 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스로 데이터를 로드 하 고 hello 데이터 원본으로 SQL Server 데이터베이스를 사용 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="0b0ad-103">Data Factory와 함께 SQL Data Warehouse로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="0b0ad-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="0b0ad-104">Azure Data Factory tooload 데이터를 사용 하 여 hello 중 하나에서 Azure SQL 데이터 웨어하우스로 [원본 데이터 저장소를 지원](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0b0ad-105">예를 들어 Data Factory를 사용하여 Azure SQL Database 또는 Oracle 데이터베이스에서 SQL Data Warehouse로 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="0b0ad-106">이 문서의 자습서 tooload 데이터는 온-프레미스 SQL Server에서 SQL 데이터 웨어하우스 데이터베이스 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="0b0ad-107">**예상 시간**: hello 전제 조건이 충족 되 면이 자습서는 10-15 분 toocomplete에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b0ad-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0b0ad-108">Prerequisites</span></span>

- <span data-ttu-id="0b0ad-109">필요한는 **SQL Server 데이터베이스** hello 데이터가 포함 된 테이블이 있는 toobe 복사한 toohello SQL 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="0b0ad-110">온라인 **SQL Data Warehouse**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="0b0ad-111">데이터 웨어하우스 아직 없는 경우 너무 방법을 알아볼[Azure SQL 데이터 웨어하우스를 만들](sql-data-warehouse-get-started-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="0b0ad-112">**Azure Storage 계정**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="0b0ad-113">저장소 계정이 아직 없는 경우 너무 방법을 알아볼[저장소 계정 만들기](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0b0ad-114">최상의 성능을 위해 hello 저장소 계정을 찾는 및 hello에 hello 데이터 웨어하우스 동일한 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="0b0ad-115">Data Factory 구성</span><span class="sxs-lookup"><span data-stu-id="0b0ad-115">Configure a data factory</span></span>
1. <span data-ttu-id="0b0ad-116">Toohello 로그인 [Azure 포털][]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="0b0ad-117">데이터 웨어하우스를 찾아 클릭 tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="0b0ad-118">Hello 주 블레이드에서 클릭 **데이터 로드** > **Azure Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![데이터 로드 마법사 시작](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="0b0ad-120">Azure 구독에는 데이터 팩터리 없는 경우 표시는 **새 데이터 팩터리** hello 브라우저의 별도 탭에서 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="0b0ad-121">Hello에 요청 된 정보를 누르고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="0b0ad-122">Hello 데이터 팩터리를 만든 후 hello **새 데이터 팩터리** 대화 상자가 닫히고 hello 참조 **데이터 팩터리 선택** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="0b0ad-123">Hello 참조 hello Azure 구독에 이미 하나 이상의 데이터 팩터리를 사용 하도록 설정한 경우 **데이터 팩터리 선택** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="0b0ad-124">이 대화 상자에서 기존 데이터 팩토리를 선택 하거나 클릭 **새 데이터 팩터리 만들기** toocreate 새 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![데이터 팩터리 구성](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="0b0ad-126">Hello에 **데이터 팩터리 선택** 대화 상자, hello **데이터 로드** 옵션은 기본적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="0b0ad-127">클릭 **다음** toostart 태스크를 로드 하는 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="0b0ad-128">Hello 데이터 팩터리의 속성 구성</span><span class="sxs-lookup"><span data-stu-id="0b0ad-128">Configure hello data factory properties</span></span>
<span data-ttu-id="0b0ad-129">데이터 팩터리를 만들었으므로 이제 hello 다음 단계는 tooconfigure hello 데이터 로드 작업 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="0b0ad-130">**작업 이름**에 **DWLoadData-fromSQLServer**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="0b0ad-131">Hello 기본값을 사용 하 여 **이제 한 번 실행** 옵션을 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![로드 일정 구성](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="0b0ad-133">Hello 원본 데이터 저장소 및 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="0b0ad-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="0b0ad-134">이제 Data Factory tooload 데이터 원하는 hello 온-프레미스 SQL Server 데이터베이스에 대 한 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="0b0ad-135">선택 **SQL Server** 지원 hello 원본 데이터에서 카탈로그를 저장 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![SQL Server 원본 선택](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="0b0ad-137">A **지정 hello 온-프레미스 SQL Server 데이터베이스** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="0b0ad-138">먼저 hello **연결 이름** 필드는 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="0b0ad-139">hello 두 번째 필드의 hello hello 이름에 대 한 요청 **게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="0b0ad-140">게이트웨이 이미가지고 있는 기존 데이터 팩토리를 사용 하는 hello 드롭 다운 목록에서 선택 하 여 hello 게이트웨이 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="0b0ad-141">Hello 클릭 **게이트웨이 만들기** toocreate 데이터 관리 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="0b0ad-142">Hello 원본 데이터를 저장 하는 경우 온-프레미스 이거나 Azure IaaS 가상 컴퓨터에서 데이터 관리 게이트웨이가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="0b0ad-143">게이트웨이는 Data Factory와 1-1 관계를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="0b0ad-144">다른 data factory에서 사용할 수 없지만 hello에 있는 작업을 로드 하는 여러 데이터에서 사용할 수 같은 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="0b0ad-145">게이트웨이는 데이터 로드 작업을 실행할 때 사용 되는 tooconnect toomultiple 데이터 저장소를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="0b0ad-146">Hello 게이트웨이에 대 한 자세한 내용은 참조 [데이터 관리 게이트웨이](../data-factory/data-factory-data-management-gateway.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="0b0ad-147">**게이트웨이 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="0b0ad-148">이름에는 **GatewayForDWLoading**을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="0b0ad-149">**게이트웨이 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="0b0ad-150">클릭 **이 컴퓨터에 빠른 설치를 시작** tooautomatically 다운로드, 설치 및 현재 시스템에 데이터 관리 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="0b0ad-151">hello 진행률 팝업 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="0b0ad-152">Hello 컴퓨터 toohello 데이터 저장소에 연결할 수 없는 경우 수동으로 실행할 수 있습니다 [hello 게이트웨이 다운로드 및 설치](https://www.microsoft.com/download/details.aspx?id=39717) toohello 데이터를 연결할 수 있는 컴퓨터에 저장 하 고 다음 키 tooregister hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="0b0ad-153">빠른 설치 hello Microsoft Edge 및 Internet Explorer에서 고유 하 게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="0b0ad-154">Google Chrome을 사용 하는 경우 먼저 크롬 웹 저장소에서 hello ClickOnce 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![빠른 설치 시작](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="0b0ad-156">Hello 게이트웨이 설치 toocomplete 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="0b0ad-157">Hello 게이트웨이 등록 하 고 온라인 상태를 hello 팝업 창이 닫히고 hello 새 게이트웨이 hello 게이트웨이 필드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="0b0ad-158">다음 채우기 hello rest에서 필수 필드 다음과 같이, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="0b0ad-159">**서버 이름**: hello의 이름 온-프레미스 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="0b0ad-160">**데이터베이스 이름**: SQL Server 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="0b0ad-161">**자격 증명 암호화**: 웹 브라우저"에서" hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="0b0ad-162">**인증 유형**: hello 사용 중인 인증 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="0b0ad-163">**사용자 이름** 및 **암호**: 권한 toocopy hello 데이터를 가진 사용자에 대 한 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![빠른 설치 시작](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="0b0ad-165">hello 다음 단계는 toocopy hello 데이터에서 toochoose hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="0b0ad-166">키워드를 사용 하 여 hello 테이블을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="0b0ad-167">및 hello 아래쪽 패널에서 hello 데이터와 테이블 스키마를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="0b0ad-168">선택을 완료했으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-168">After you finish your selection, click **Next**.</span></span>

    ![테이블 선택](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="0b0ad-170">Hello 대상, SQL 데이터 웨어하우스 구성</span><span class="sxs-lookup"><span data-stu-id="0b0ad-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="0b0ad-171">이제 Data Factory hello 대상 정보에 대 한 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="0b0ad-172">SQL Data Warehouse 연결 정보가 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="0b0ad-173">Hello 사용자 이름에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="0b0ad-174">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-174">and click **Next**.</span></span>

    ![대상 구성](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="0b0ad-176">지능형 테이블 매핑 테이블 이름에 따라 소스 toodestination 테이블을 매핑하는 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="0b0ad-177">Hello 테이블이 hello 대상에 존재 하지 않는 경우 기본적으로 ADF 만들어집니다 hello로 동일한 이름 (이 적용 tooSQL 서버 또는 원본으로 Azure SQL 데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="0b0ad-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="0b0ad-178">또한 toomap tooan 기존 테이블을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="0b0ad-179">검토하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-179">Review and click **Next**.</span></span>

    ![맵 테이블](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="0b0ad-181">Hello 스키마 매핑을 검토 하 고 오류 또는 경고 메시지를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="0b0ad-182">지능형 매핑은 열 이름을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="0b0ad-183">Hello 원본 및 대상 열 간에 변환 하는 지원 되지 않는 데이터 형식 변환을 이면 hello 해당 테이블과 함께 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="0b0ad-184">Toolet Data Factory 자동을 선택 하면 hello 테이블 만들기, 적절 한 데이터 형식 변환이 필요한 소스 및 대상 저장소 간 toofix hello 호환 되지 않는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![맵 스키마](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="0b0ad-186">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="0b0ad-187">Hello 성능 설정 구성</span><span class="sxs-lookup"><span data-stu-id="0b0ad-187">Configure hello performance settings</span></span>
<span data-ttu-id="0b0ad-188">Azure 저장소 계정을 사용 하 여 SQL 데이터 웨어하우스 효율적으로 로드 하기 전에 hello 데이터 준비에 사용 되는 hello 성능 구성에서 구성한 [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="0b0ad-189">Hello 복사를 완료 한 후 hello 중간 데이터 저장소에는 자동으로 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="0b0ad-190">기존 Azure Storage 계정을 선택하거나 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![준비 Blob 구성](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="0b0ad-192">요약 정보를 검토 하 고 hello 파이프라인 배포</span><span class="sxs-lookup"><span data-stu-id="0b0ad-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="0b0ad-193">Hello 구성을 검토 하 고 클릭 **마침** 단추 toodeploy hello 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![데이터 팩터리 배포](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="0b0ad-195">데이터 로드 진행 상태 모니터</span><span class="sxs-lookup"><span data-stu-id="0b0ad-195">Monitor data loading progress</span></span>

<span data-ttu-id="0b0ad-196">Hello 배포 진행률과 hello에 결과 볼 수 있습니다 **배포** 페이지.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="0b0ad-197">Hello 배포 작업이 완료 되 면 hello 링크는 클릭 **toomonitor 복사 파이프라인 여기를 클릭** toomonitor 데이터 진행 상태를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![파이프라인 모니터링](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="0b0ad-199">새로 만든 hello **DWLoadData fromSQLServer** 데이터 로드 파이프라인은 자동으로 hello 왼쪽에서 선택 **리소스 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![파이프라인 보기](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="0b0ad-201">Hello 가운데에 hello 파이프라인에는 클릭 패널 toosee hello tooan 활동을 매핑하는 각 테이블에 대 한 상태를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![테이블 활동 보기](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="0b0ad-203">작업 내부로 누르고 데이터 크기, 행, 처리량 등을 포함 하 여 hello 오른쪽 패널에서 세부 정보를 로드 하는 hello 데이터 참조 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![테이블 활동 세부 정보 보기](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="0b0ad-205">toolaunch이 모니터링 보기 이상, 이동 tooyour SQL 데이터 웨어하우스, 클릭 **데이터 로드 > Azure Data Factory**공장을 선택 하 고 선택 **작업 로드를 기존 모니터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b0ad-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b0ad-206">Next steps</span></span>

<span data-ttu-id="0b0ad-207">toomigrate 프로그램 데이터베이스 tooSQL 데이터 웨어하우스 참조 [마이그레이션 개요](sql-data-warehouse-overview-migrate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0ad-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="0b0ad-208">Azure Data Factory와 해당 데이터 이동 기능에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="0b0ad-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="0b0ad-209">소개 tooAzure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="0b0ad-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="0b0ad-210">복사 작업을 사용하여 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="0b0ad-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="0b0ad-211">Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로부터 데이터 tooand 이동</span><span class="sxs-lookup"><span data-stu-id="0b0ad-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="0b0ad-212">tooexplore SQL 데이터 웨어하우스에 데이터 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="0b0ad-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="0b0ad-213">Visual Studio와 SSDT를 사용 하 여 데이터 웨어하우스 tooSQL 연결</span><span class="sxs-lookup"><span data-stu-id="0b0ad-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="0b0ad-214">[Power BI를 사용하여 시각적 데이터](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="0b0ad-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure 포털]: https://portal.azure.com
