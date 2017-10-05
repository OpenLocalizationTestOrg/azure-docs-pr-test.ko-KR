---
title: "Blob Storage에서 SQL Database로 데이터 복사 - Azure | Microsoft Docs"
description: "이 자습서에서는 Azure Data Factory 파이프라인에서 복사 작업을 사용하여 Blob 저장소에서 SQL 데이터베이스로 데이터를 복사하는 방법을 보여 줍니다."
keywords: "Blob SQL, Blob 저장소, 데이터 복사"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="042df-104">자습서: 데이터 팩터리를 사용하여 Blob Storage에서 SQL Database로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="042df-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="042df-105">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="042df-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="042df-106">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="042df-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="042df-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="042df-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="042df-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="042df-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="042df-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="042df-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="042df-110">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="042df-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="042df-111">REST API</span><span class="sxs-lookup"><span data-stu-id="042df-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="042df-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="042df-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="042df-113">이 자습서에서는 파이프라인을 포함한 데이터 팩터리를 만들어서 Blob 저장소에서 SQL 데이터베이스로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="042df-114">복사 작업은 Azure Data Factory에서 데이터 이동을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="042df-115">다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="042df-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="042df-116">복사 작업에 대한 자세한 내용은 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="042df-117">데이터 팩터리 서비스에 대한 자세한 개요는 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="042df-118">자습서의 필수 조건</span><span class="sxs-lookup"><span data-stu-id="042df-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="042df-119">이 자습서를 시작하기 전에 다음 필수 조건이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="042df-120">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="042df-120">**Azure subscription**.</span></span>  <span data-ttu-id="042df-121">구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="042df-122">자세한 내용은 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="042df-123">**Azure 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="042df-123">**Azure Storage Account**.</span></span> <span data-ttu-id="042df-124">이 자습서에서는 Blob 저장소를 **원본** 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="042df-125">Azure Storage 계정이 없는 경우 새로 만드는 단계는 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="042df-126">**Azure SQL 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="042df-126">**Azure SQL Database**.</span></span> <span data-ttu-id="042df-127">이 자습서에서는 Azure SQL 데이터베이스를 **대상** 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="042df-128">자습서에서 사용할 수 있는 Azure SQL 데이터베이스가 없는 경우 [Azure SQL 데이터베이스를 만들고 구성하는 방법](../sql-database/sql-database-get-started.md) 을 참조하여 새로 만드세요.</span><span class="sxs-lookup"><span data-stu-id="042df-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="042df-129">**SQL Server 2012/2014 또는 Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="042df-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="042df-130">SQL Server Management Studio 또는 Visual Studio를 사용하여 샘플 데이터베이스를 만들고 데이터베이스에서 결과 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="042df-131">Blob 저장소 계정 이름 및 키 수집</span><span class="sxs-lookup"><span data-stu-id="042df-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="042df-132">이 자습서를 수행하려면 Azure Storage 계정의 계정 이름과 계정 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="042df-133">Azure Storage 계정의 **계정 이름**과 **계정 키**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="042df-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="042df-134">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="042df-135">왼쪽 메뉴의 **더 많은 서비스**를 클릭하고 **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![찾아보기 - 저장소 계정](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="042df-137">**저장소 계정** 블레이드에서, 이 자습서에서 사용하려는 **Azure 저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="042df-138">**설정** 아래에 있는 **액세스 키** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="042df-139">**저장소 계정 이름** 텍스트 상자 옆에 있는 **복사**(이미지) 단추를 클릭하고 텍스트 파일 등에 저장/붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="042df-140">이전 단계를 반복하여 복사하거나 **key1**을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="042df-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![저장소 액세스 키](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="042df-142">**X**를 클릭하여 모든 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="042df-143">SQL server, 데이터베이스, 사용자 이름 수집</span><span class="sxs-lookup"><span data-stu-id="042df-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="042df-144">이 자습서를 수행하려면 Azure SQL Server, 데이터베이스 및 사용자의 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="042df-145">Azure SQL 데이터베이스의 **서버**, **데이터베이스** 및 **사용자**의 이름을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="042df-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="042df-146">**Azure 포털**에서 왼쪽의 **더 많은 서비스**를 클릭하고 **SQL 데이터베이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="042df-147">**SQL 데이터베이스 블레이드**에서, 이 자습서에서 사용하려는 **데이터베이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="042df-148">**데이터베이스 이름**을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="042df-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="042df-149">**SQL 데이터베이스** 블레이드에서 **설정** 아래의 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="042df-150">**서버 이름** 및 **서버 관리자 로그인**의 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="042df-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="042df-151">**X**를 클릭하여 모든 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="042df-152">Azure 서비스가 SQL server에 액세스하도록 허용</span><span class="sxs-lookup"><span data-stu-id="042df-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="042df-153">데이터 팩터리 서비스가 Azure SQL Server에 액세스할 수 있도록 Azure SQL Server에 대해 **Azure 서비스에 대한 액세스 허용** 설정이 **ON**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="042df-154">이 설정을 확인하고 켜려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="042df-155">왼쪽의 **더 많은 서비스** 허브를 클릭하고 **SQL 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="042df-156">서버를 선택하고 **설정** 아래의 **방화벽**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="042df-157">**방화벽 설정** 블레이드에서 **Azure 서비스에 대한 액세스 허용**에 대해 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="042df-158">**X**를 클릭하여 모든 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="042df-159">Blob 저장소 및 SQL 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="042df-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="042df-160">이제 다음 단계를 수행하여 자습서에서 사용할 Azure Blob 저장소 및 Azure SQL 데이터베이스를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="042df-161">메모장을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-161">Launch Notepad.</span></span> <span data-ttu-id="042df-162">다음 텍스트를 복사하여 **emp.txt**로 하드 드라이브의 **C:\ADFGetStarted** 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="042df-163">[Azure Storage Explorer](http://storageexplorer.com/)와 같은 도구를 사용하여 **adftutorial** 컨테이너를 만들고 **emp.txt** 파일을 이 컨테이너에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure 저장소 탐색기.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="042df-166">다음 SQL 스크립트를 사용하여 **emp** 테이블을 Azure SQL 데이터베이스에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="042df-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="042df-167">**컴퓨터에 SQL Server 2012/2014가 설치된 경우:** [SQL Server Management Studio를 사용하여 Azure SQL Database 관리](../sql-database/sql-database-manage-azure-ssms.md)의 지침에 따라 Azure SQL 서버에 연결하고 SQL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="042df-168">이 문서에서는 [새 Azure 포털](https://portal.azure.com)이 아닌 [Azure 클래식 포털](http://manage.windowsazure.com)을 사용하여 Azure SQL Server의 방화벽을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="042df-169">클라이언트가 Azure SQL Server에 액세스할 수 없는 경우 컴퓨터(IP 주소)의 액세스를 허용하도록 Azure SQL Server의 방화벽을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="042df-170">Azure SQL Server의 방화벽을 구성하는 단계는 [이 문서](../sql-database/sql-database-configure-firewall-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="042df-171">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="042df-171">Create a data factory</span></span>
<span data-ttu-id="042df-172">필수 조건을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-172">You have completed the prerequisites.</span></span> <span data-ttu-id="042df-173">다음 방법 중 하나를 사용하여 데이터 팩터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="042df-174">위쪽의 드롭다운 목록에 있는 옵션 또는 다음 링크 중 하나를 클릭하여 자습서를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="042df-175">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="042df-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="042df-176">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="042df-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="042df-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="042df-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="042df-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="042df-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="042df-179">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="042df-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="042df-180">REST API</span><span class="sxs-lookup"><span data-stu-id="042df-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="042df-181">.NET API</span><span class="sxs-lookup"><span data-stu-id="042df-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="042df-182">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="042df-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="042df-183">출력 데이터를 생성하기 위해 입력 데이터를 변환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="042df-184">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="042df-185">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정하여 두 활동을 연결하면 해당 활동을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="042df-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="042df-186">자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="042df-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
