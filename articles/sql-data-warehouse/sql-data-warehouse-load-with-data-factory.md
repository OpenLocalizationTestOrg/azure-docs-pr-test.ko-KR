---
title: "Azure SQL Data Warehouse에 데이터 로드 – Data Factory | Microsoft Docs"
description: "이 자습서에서는 Azure Data Factory를 사용하여 Azure SQL Data Warehouse에 데이터를 로드하고 데이터 원본으로 SQL Server 데이터베이스를 사용합니다."
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
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="1aa3a-103">Data Factory와 함께 SQL Data Warehouse로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="1aa3a-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="1aa3a-104">Azure Data Factory를 사용하여 [지원되는 원본 데이터 저장소](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)에서 Azure SQL Data Warehouse로 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1aa3a-105">예를 들어 Data Factory를 사용하여 Azure SQL Database 또는 Oracle 데이터베이스에서 SQL Data Warehouse로 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="1aa3a-106">이 문서의 자습서에서는 온-프레미스 SQL Server 데이터베이스에서 SQL Data Warehouse로 데이터를 로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="1aa3a-107">**예상 시간**: 이 자습서를 완료하는 데는 필수 조건이 충족된 경우 10-15분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aa3a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1aa3a-108">Prerequisites</span></span>

- <span data-ttu-id="1aa3a-109">SQL Data Warehouse에 복사할 데이터가 포함된 테이블이 있는 **SQL Server 데이터베이스**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="1aa3a-110">온라인 **SQL Data Warehouse**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="1aa3a-111">데이터 웨어하우스가 아직 없는 경우 [Azure SQL Data Warehouse를 만드는 방법](sql-data-warehouse-get-started-provision.md)을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="1aa3a-112">**Azure Storage 계정**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="1aa3a-113">저장소 계정이 아직 없을 경우 [저장소 계정을 만드는 방법](../storage/common/storage-create-storage-account.md)을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1aa3a-114">최적의 성능을 위해 저장소 계정 및 데이터 웨어하우스를 동일한 Azure 지역에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="1aa3a-115">Data Factory 구성</span><span class="sxs-lookup"><span data-stu-id="1aa3a-115">Configure a data factory</span></span>
1. <span data-ttu-id="1aa3a-116">[Azure 포털][]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="1aa3a-117">데이터 웨어하우스를 찾고 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="1aa3a-118">주 블레이드에서 **데이터 로드** > **Azure Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![데이터 로드 마법사 시작](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="1aa3a-120">Azure 구독에 Data Factory가 없으면 브라우저의 별도 탭에 **새 Data Factory** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="1aa3a-121">요청된 정보를 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="1aa3a-122">Data Factory를 만들면 **새 Data Factory** 대화 상자가 닫히고 **Data Factory 선택** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="1aa3a-123">Azure 구독에 이미 하나 이상의 Data Factory가 있는 경우 **Data Factory 선택** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="1aa3a-124">이 대화 상자에서 기존 Data Factory를 선택하거나 **새 Data Factory 만들기**를 클릭하여 새 Data Factory를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![데이터 팩터리 구성](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="1aa3a-126">**데이터 팩터리 선택** 대화 상자에는 **데이터 로드** 옵션이 기본적으로 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="1aa3a-127">**다음**을 클릭하여 데이터 로드 작업 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="1aa3a-128">데이터 팩터리 속성 구성</span><span class="sxs-lookup"><span data-stu-id="1aa3a-128">Configure the data factory properties</span></span>
<span data-ttu-id="1aa3a-129">이제 데이터 팩터리를 만들었고 다음 단계에서는 데이터 로딩 일정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="1aa3a-130">**작업 이름**에 **DWLoadData-fromSQLServer**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="1aa3a-131">기본 **지금 한 번 실행** 옵션을 사용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![로드 일정 구성](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="1aa3a-133">원본 데이터 저장소 및 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="1aa3a-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="1aa3a-134">이제 Data Factory에 데이터를 로드할 원본 온-프레미스 SQL Server 데이터베이스에 대한 정보를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="1aa3a-135">지원되는 원본 데이터 저장소 카탈로그에서 **SQL Server**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![SQL Server 원본 선택](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="1aa3a-137">**온-프레미스 SQL Server 데이터베이스 지정** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="1aa3a-138">첫 번째 **연결 이름** 필드는 자동으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="1aa3a-139">두 번째 필드는 **게이트웨이** 이름을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="1aa3a-140">이미 게이트웨이가 있는 기존 Data Factory를 사용하는 경우 드롭다운 목록에서 게이트웨이를 선택하여 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="1aa3a-141">**게이트웨이 만들기** 링크를 클릭하여 데이터 관리 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="1aa3a-142">원본 데이터 저장소가 온-프레미스 또는 Azure IaaS 가상 컴퓨터에 있는 경우 데이터 관리 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="1aa3a-143">게이트웨이는 Data Factory와 1-1 관계를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="1aa3a-144">다른 Data Factory에서는 사용할 수 없지만 동일한 Data Factory에서 여러 데이터 로드 작업으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="1aa3a-145">게이트웨이는 데이터 로드 작업을 실행할 때 여러 데이터 저장소에 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="1aa3a-146">게이트웨이에 대한 자세한 내용은 [데이터 관리 게이트웨이](../data-factory/data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="1aa3a-147">**게이트웨이 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="1aa3a-148">이름에는 **GatewayForDWLoading**을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="1aa3a-149">**게이트웨이 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="1aa3a-150">**이 컴퓨터에서 빠른 설치 시작**을 클릭하여 현재 컴퓨터에 데이터 관리 게이트웨이를 자동으로 다운로드, 설치 및 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="1aa3a-151">진행 상태가 팝업 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="1aa3a-152">컴퓨터를 데이터 저장소에 연결할 수 없는 경우 데이터 저장소에 연결할 수 있는 컴퓨터에 수동으로 [게이트웨이를 다운로드하고 설치](https://www.microsoft.com/download/details.aspx?id=39717)한 다음 키를 사용하여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="1aa3a-153">빠른 설치는 Microsoft Edge 및 Internet Explorer에서 고유하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="1aa3a-154">Google Chrome을 사용 중인 경우 먼저 Chrome 웹 스토어에서 ClickOnce 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![빠른 설치 시작](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="1aa3a-156">게이트웨이 설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="1aa3a-157">게이트웨이가 성공적으로 등록되고 온라인 상태이면 팝업 창이 닫히고 새 게이트웨이가 게이트웨이 필드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="1aa3a-158">그런 다음 나머지 필수 필드를 다음과 같이 채운 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="1aa3a-159">**서버 이름**: 온-프레미스 SQL Server의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="1aa3a-160">**데이터베이스 이름**: SQL Server 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="1aa3a-161">**자격 증명 암호화**: 기본값인 "웹 브라우저"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="1aa3a-162">**인증 유형**: 사용 중인 인증 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="1aa3a-163">**사용자 이름** 및 **암호**: 데이터를 복사할 권한이 있는 사용자에 대한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![빠른 설치 시작](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="1aa3a-165">다음 단계는 데이터를 복사할 원본 테이블을 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="1aa3a-166">키워드를 사용하여 테이블을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="1aa3a-167">아래쪽 패널에서 데이터 및 테이블 스키마를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="1aa3a-168">선택을 완료했으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-168">After you finish your selection, click **Next**.</span></span>

    ![테이블 선택](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="1aa3a-170">대상으로 SQL Data Warehouse 구성</span><span class="sxs-lookup"><span data-stu-id="1aa3a-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="1aa3a-171">이제 Data Factory에 대상 정보를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="1aa3a-172">SQL Data Warehouse 연결 정보가 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="1aa3a-173">사용자 이름 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-173">Enter the password for the user name.</span></span> <span data-ttu-id="1aa3a-174">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-174">and click **Next**.</span></span>

    ![대상 구성](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="1aa3a-176">테이블 이름에 따라 원본을 대상 테이블에 매핑하는 지능형 테이블 매핑이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="1aa3a-177">테이블이 대상에 없는 경우 기본적으로 ADF가 같은 이름을 사용하여 하나를 만듭니다(SQL Server 또는 Azure SQL Database에 원본으로 적용됨).</span><span class="sxs-lookup"><span data-stu-id="1aa3a-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="1aa3a-178">또한 기존 테이블에 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="1aa3a-179">검토하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-179">Review and click **Next**.</span></span>

    ![맵 테이블](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="1aa3a-181">스키마 매핑을 검토하고 오류 또는 경고 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="1aa3a-182">지능형 매핑은 열 이름을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="1aa3a-183">원본 및 대상 열 간에 지원되지 않는 데이터 형식이 있는 경우 해당 테이블과 함께 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="1aa3a-184">데이터 팩터리에서 테이블을 자동으로 만들 수 있도록 선택하는 경우 소스 및 대상 저장소 간의 비 호환성을 해결할 필요성이 있으면 적절한 데이터 형식 변환이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![맵 스키마](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="1aa3a-186">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="1aa3a-187">성능 설정 구성</span><span class="sxs-lookup"><span data-stu-id="1aa3a-187">Configure the performance settings</span></span>
<span data-ttu-id="1aa3a-188">성능 구성에서 [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly)를 사용하여 성능 기준에 맞게 데이터를 SQL Data Warehouse에 로드하기 전에 데이터 준비에 사용할 Azure Storage 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="1aa3a-189">복사가 완료되면 저장소의 중간 데이터는 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="1aa3a-190">기존 Azure Storage 계정을 선택하거나 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![준비 Blob 구성](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="1aa3a-192">요약 정보 검토 및 파이프라인 배포</span><span class="sxs-lookup"><span data-stu-id="1aa3a-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="1aa3a-193">구성을 검토하고 **마침** 단추를 클릭하여 파이프라인을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![데이터 팩터리 배포](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="1aa3a-195">데이터 로드 진행 상태 모니터</span><span class="sxs-lookup"><span data-stu-id="1aa3a-195">Monitor data loading progress</span></span>

<span data-ttu-id="1aa3a-196">**배포** 페이지서 배포 진행률 및 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="1aa3a-197">배포가 완료되면 **복사 파이프라인을 모니터링하려면 여기를 클릭** 링크를 클릭하여 데이터 로딩 진행 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![파이프라인 모니터링](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="1aa3a-199">새로 만든 **DWLoadData fromSQLServer** 데이터 로드 파이프라인이 왼쪽의 **리소스 탐색기**에서 자동 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![파이프라인 보기](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="1aa3a-201">중간 패널에서 파이프라인을 클릭하여 활동에 매핑되는 각 테이블에 대한 자세한 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![테이블 활동 보기](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="1aa3a-203">활동을 추가로 클릭하면 오른쪽 창에 데이터 크기, 행, 처리량 등 데이터 로딩 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![테이블 활동 세부 정보 보기](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="1aa3a-205">이 모니터링 보기를 나중에 시작하려면 SQL Data Warehouse로 이동하고 **데이터 로드 > Azure Data Factory**를 클릭한 후 팩터리를 선택하고 **기존 로딩 작업 모니터링**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa3a-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1aa3a-206">Next steps</span></span>

<span data-ttu-id="1aa3a-207">데이터베이스를 SQL Data Warehouse로 마이그레이션하려면 [마이그레이션 개요](sql-data-warehouse-overview-migrate.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="1aa3a-208">Azure Data Factory 및 데이터 이동 기능에 대한 자세한 내용을 보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="1aa3a-209">Azure Data Factory 소개</span><span class="sxs-lookup"><span data-stu-id="1aa3a-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="1aa3a-210">복사 작업을 사용하여 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="1aa3a-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="1aa3a-211">Azure Data Factory를 사용하여 Azure SQL Data Warehouse 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="1aa3a-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="1aa3a-212">SQL Data Warehouse의 데이터를 탐색하려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa3a-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="1aa3a-213">Visual Studio 및 SSDT를 사용하여 SQL Data Warehouse에 연결</span><span class="sxs-lookup"><span data-stu-id="1aa3a-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="1aa3a-214">[Power BI를 사용하여 시각적 데이터](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="1aa3a-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure 포털]: https://portal.azure.com
