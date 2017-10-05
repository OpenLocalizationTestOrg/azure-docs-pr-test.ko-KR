---
title: "Azure Cosmos DB 커넥터에 대한 Power BI 자습서 | Microsoft Docs"
description: "이 Power BI 자습서를 사용하여 JSON을 가져오고, 통찰력 있는 보고서를 만들고, Azure Cosmos DB 및 Power BI 커넥터를 사용하여 데이터를 시각화할 수 있습니다."
keywords: "power bi 자습서, 데이터 시각화, power bi 커넥터"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: 7f56f6d89a9990ab7e7f50a86993e9e22b73d646
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-the-power-bi-connector"></a><span data-ttu-id="8dcfc-104">Azure Cosmos DB에 대한 Power BI 자습서: Power BI 커넥터를 사용하여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="8dcfc-104">Power BI tutorial for Azure Cosmos DB: Visualize data using the Power BI connector</span></span>
<span data-ttu-id="8dcfc-105">[PowerBI.com](https://powerbi.microsoft.com/) 은 사용자 및 조직에 중요한 데이터로 대시보드와 보고서를 만들어 공유할 수 있는 온라인 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-105">[PowerBI.com](https://powerbi.microsoft.com/) is an online service where you can create and share dashboards and reports with data that's important to you and your organization.</span></span>  <span data-ttu-id="8dcfc-106">Power BI 데스크톱은 다양한 데이터 원본에서 데이터를 검색하고, 데이터를 병합 및 변환하며, 강력한 보고서 및 시각화를 제작하고, 보고서를 Power BI에 게시할 수 있는 전용 보고서 제작 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-106">Power BI Desktop is a dedicated report authoring tool that enables you to retrieve data from various data sources, merge and transform the data, create powerful reports and visualizations, and publish the reports to Power BI.</span></span>  <span data-ttu-id="8dcfc-107">Power BI Desktop의 최신 버전에서는 이제 Power BI용 Cosmos DB 커넥터를 통해 Cosmos DB 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-107">With the latest version of Power BI Desktop, you can now connect to your Cosmos DB account via the Cosmos DB connector for Power BI.</span></span>   

<span data-ttu-id="8dcfc-108">이 Power BI 자습서에서는 Power BI Desktop의 Cosmos DB 계정에 연결하고, 탐색기를 사용하여 데이터를 추출할 컬렉션으로 이동하고, Power BI Desktop 쿼리 편집기를 사용하여 JSON 데이터를 테이블 형식으로 변환하고, 보고서를 빌드하여 PowerBI.com에 게시하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-108">In this Power BI tutorial, we walk through the steps to connect to a Cosmos DB account in Power BI Desktop, navigate to a collection where we want to extract the data using the Navigator, transform JSON data into tabular format using Power BI Desktop Query Editor, and build and publish a report to PowerBI.com.</span></span>

<span data-ttu-id="8dcfc-109">이 Power BI 자습서를 완료하고 나면 다음을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-109">After completing this Power BI tutorial, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="8dcfc-110">Power BI Desktop을 사용하여 Cosmos DB의 데이터로 보고서를 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="8dcfc-110">How can I build reports with data from Cosmos DB using Power BI Desktop?</span></span>
* <span data-ttu-id="8dcfc-111">Power BI Desktop에서 Cosmos DB 계정에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="8dcfc-111">How can I connect to a Cosmos DB account in Power BI Desktop?</span></span>
* <span data-ttu-id="8dcfc-112">Power BI 데스크톱의 컬렉션에서 데이터를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="8dcfc-112">How can I retrieve data from a collection in Power BI Desktop?</span></span>
* <span data-ttu-id="8dcfc-113">Power BI 데스크톱에서 중첩된 JSON 데이터를 변환하는 방법</span><span class="sxs-lookup"><span data-stu-id="8dcfc-113">How can I transform nested JSON data in Power BI Desktop?</span></span>
* <span data-ttu-id="8dcfc-114">PowerBI.com에서 내 보고서를 게시 및 공유하는 방법</span><span class="sxs-lookup"><span data-stu-id="8dcfc-114">How can I publish and share my reports in PowerBI.com?</span></span>

> [!NOTE]
> <span data-ttu-id="8dcfc-115">Azure Cosmos DB용 Power BI 커넥터는 데이터 추출 및 변환을 위해 Power BI Desktop에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-115">The Power BI connector for Azure Cosmos DB connects to Power BI Desktop for extraction and transformation of data.</span></span> <span data-ttu-id="8dcfc-116">Power BI Desktop에서 만든 보고서를 PowerBI.com에 게시할 수 있습니다. Azure Cosmos DB 데이터의 직접 추출 및 변환은 PowerBI.com에서 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-116">Reports created in Power BI Desktop can then be published to PowerBI.com. Direct extraction and transformation of Azure Cosmos DB data cannot be performed in PowerBI.com.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8dcfc-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8dcfc-117">Prerequisites</span></span>
<span data-ttu-id="8dcfc-118">이 Power BI 자습서의 지침을 따르기 전에 다음 리소스에 액세스할 수 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-118">Before following the instructions in this Power BI tutorial, ensure that you have access to the following resources:</span></span>

* <span data-ttu-id="8dcfc-119">[최신 버전의 Power BI Desktop](https://powerbi.microsoft.com/desktop).</span><span class="sxs-lookup"><span data-stu-id="8dcfc-119">[The latest version of Power BI Desktop](https://powerbi.microsoft.com/desktop).</span></span>
* <span data-ttu-id="8dcfc-120">데모 계정 또는 Cosmos DB 계정의 데이터 액세스.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-120">Access to our demo account or data in your Cosmos DB account.</span></span>
  * <span data-ttu-id="8dcfc-121">데모 계정은 이 자습서에 표시된 화산 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-121">The demo account is populated with the volcano data shown in this tutorial.</span></span> <span data-ttu-id="8dcfc-122">이 데모 계정은 SLA와 연결되지 않으며 데모용으로만 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-122">This demo account is not bound by any SLAs and is meant for demonstration purposes only.</span></span>  <span data-ttu-id="8dcfc-123">Microsoft는 계정 종료, 키 변경, 액세스 제한, 데이터 변경 및 삭제 등을 망라하여, 언제든 사전 고지나 이유 없이 이 데모 계정을 수정할 권리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-123">We reserve the right to make modifications to this demo account including but not limited to, terminating the account, changing the key, restricting access, changing, and delete the data, at any time without advance notice or reason.</span></span>
    * <span data-ttu-id="8dcfc-124">URL: https://analytics.documents.azure.com</span><span class="sxs-lookup"><span data-stu-id="8dcfc-124">URL: https://analytics.documents.azure.com</span></span>
    * <span data-ttu-id="8dcfc-125">읽기 전용 키: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span><span class="sxs-lookup"><span data-stu-id="8dcfc-125">Read-only key: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span></span>
  * <span data-ttu-id="8dcfc-126">또는 고유 계정을 만들려면 [Azure Portal을 사용하여 Azure Cosmos DB 데이터베이스 계정 만들기](https://azure.microsoft.com/documentation/articles/create-account/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-126">Or, to create your own account, see [Create an Azure Cosmos DB database account using the Azure portal](https://azure.microsoft.com/documentation/articles/create-account/).</span></span> <span data-ttu-id="8dcfc-127">그런 다음 이 자습서에서 사용된 것과 유사하지만 GeoJSON 블록이 포함되지 않은 샘플 화산 데이터를 가져오려면 [NOAA 사이트](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5)를 참조하고, [Azure Cosmos DB 데이터 마이그레이션 도구](import-data.md)를 사용하여 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-127">Then, to get sample volcano data that's similar to what's used in this tutorial (but does not contain the GeoJSON blocks), see the [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) and then import the data using the [Azure Cosmos DB data migration tool](import-data.md).</span></span>

<span data-ttu-id="8dcfc-128">PowerBI.com에서 보고서를 공유하려면 PowerBI.com에 계정이 있어야 합니다.  무료 Power BI 및 Power BI Pro에 대한 자세한 내용은 [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-128">To share your reports in PowerBI.com, you must have an account in PowerBI.com.  To learn more about Power BI for Free and Power BI Pro, visit [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).</span></span>

## <a name="lets-get-started"></a><span data-ttu-id="8dcfc-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-129">Let's get started</span></span>
<span data-ttu-id="8dcfc-130">이 자습서에서는 전세계 화산을 연구하는 지질학자라고 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-130">In this tutorial, let's imagine that you are a geologist studying volcanoes around the world.</span></span>  <span data-ttu-id="8dcfc-131">화산 데이터는 Cosmos DB 계정에 저장되며 JSON 문서는 다음 샘플 문서와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-131">The volcano data is stored in a Cosmos DB account and the JSON documents look like the following sample document.</span></span>

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

<span data-ttu-id="8dcfc-132">Cosmos DB 계정에서 화산 데이터를 검색하고 다음 보고서와 같은 대화형 Power BI 보고서에서 데이터를 시각화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-132">You want to retrieve the volcano data from the Cosmos DB account and visualize data in an interactive Power BI report like the following report.</span></span>

![Power BI 커넥터를 사용하여 이 Power BI 자습서를 완료하여 Power BI Desktop 화산 보고서를 사용하여 데이터를 시각화할 수 있습니다.](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

<span data-ttu-id="8dcfc-134">해 볼 준비가 되셨나요?</span><span class="sxs-lookup"><span data-stu-id="8dcfc-134">Ready to give it a try?</span></span> <span data-ttu-id="8dcfc-135">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-135">Let's get started.</span></span>

1. <span data-ttu-id="8dcfc-136">워크스테이션에서 Power BI 데스크톱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-136">Run Power BI Desktop on your workstation.</span></span>
2. <span data-ttu-id="8dcfc-137">Power BI 데스크톱이 시작되면 *시작* 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-137">Once Power BI Desktop is launched, a *Welcome* screen is displayed.</span></span>
   
    ![Power BI 데스크톱 시작 화면 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. <span data-ttu-id="8dcfc-139">**시작** 화면에서 직접 데이터를 **가져오고** , 최근 **원본을 보거나** , 다른 보고서를 직접 *열 수* 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-139">You can **Get Data**, see **Recent Sources**, or **Open Other Reports** directly from the *Welcome* screen.</span></span>  <span data-ttu-id="8dcfc-140">화면을 닫으려면 오른쪽 상단 모서리의 X를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-140">Click the X at the top right corner to close the screen.</span></span> <span data-ttu-id="8dcfc-141">Power BI 데스크톱의 **보고서** 뷰가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-141">The **Report** view of Power BI Desktop is displayed.</span></span>
   
    ![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. <span data-ttu-id="8dcfc-143">**홈** 리본 메뉴를 선택한 다음 **데이터 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-143">Select the **Home** ribbon, then click on **Get Data**.</span></span>  <span data-ttu-id="8dcfc-144">**데이터 가져오기** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-144">The **Get Data** window should appear.</span></span>
5. <span data-ttu-id="8dcfc-145">**Azure**를 클릭하고 **Microsoft Azure DocumentDB(베타)**를 클릭한 다음 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-145">Click on **Azure**, select **Microsoft Azure DocumentDB (Beta)**, and then click **Connect**.</span></span> 

    ![Power BI 데스크톱 데이터 가져오기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. <span data-ttu-id="8dcfc-147">**커넥터 미리 보기** 페이지에서 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-147">On the **Preview Connector** page, click **Continue**.</span></span> <span data-ttu-id="8dcfc-148">**Microsoft Azure DocumentDB 연결** 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-148">The **Microsoft Azure DocumentDB Connect** window appears.</span></span>
7. <span data-ttu-id="8dcfc-149">아래와 같이 데이터를 가져올 Cosmos DB 계정 끝점 URL을 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-149">Specify the Cosmos DB account endpoint URL you would like to retrieve the data from as shown below, and then click **OK**.</span></span> <span data-ttu-id="8dcfc-150">자신의 계정을 사용하려는 경우 Azure Portal의 **[키](manage-account.md#keys)** 블레이드에 있는 URI 상자에서 URL을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-150">To use your own account, you can retrieve the URL from the URI box in the **[Keys](manage-account.md#keys)** blade of the Azure portal.</span></span> <span data-ttu-id="8dcfc-151">데모 계정을 사용하려면 URL로 `https://analytics.documents.azure.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-151">To use the demo account, enter `https://analytics.documents.azure.com` for the URL.</span></span> 
   
    <span data-ttu-id="8dcfc-152">데이터베이스 이름, 컬렉션 이름 및 SQL 문을 비워 둡니다. 이러한 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-152">Leave the database name, collection name, and SQL statement blank as these fields are optional.</span></span>  <span data-ttu-id="8dcfc-153">대신 데이터의 출처를 식별하기 위해 탐색기를 사용하여 데이터베이스와 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-153">Instead, we will use the Navigator to select the Database and Collection to identify where the data comes from.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 데스크톱 연결 창](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. <span data-ttu-id="8dcfc-155">처음으로 이 끝점에 연결하는 경우 계정 키를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-155">If you are connecting to this endpoint for the first time, you are prompted for the account key.</span></span> <span data-ttu-id="8dcfc-156">자신의 계정을 사용하는 경우 Azure Portal의 **[읽기 전용 키](manage-account.md#keys)** 블레이드에 있는 **기본 키** 상자에서 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-156">For your own account, retrieve the key from the **Primary Key** box in the **[Read-only Keys](manage-account.md#keys)** blade of the Azure portal.</span></span> <span data-ttu-id="8dcfc-157">데모 계정의 경우 키는 `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`입니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-157">For the demo account, the key is `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`.</span></span> <span data-ttu-id="8dcfc-158">적절한 키를 입력하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-158">Enter the appropriate key and then click **Connect**.</span></span>
   
    <span data-ttu-id="8dcfc-159">보고서를 작성할 때는 읽기 전용 키를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-159">We recommend that you use the read-only key when building reports.</span></span>  <span data-ttu-id="8dcfc-160">이렇게 하면 불필요하게 마스터 키가 잠재적인 보안 위험에 노출되는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-160">This will prevent unnecessary exposure of the master key to potential security risks.</span></span> <span data-ttu-id="8dcfc-161">읽기 전용 키는 Azure 포털의 [키](manage-account.md#keys) 블레이드에서 가져오거나, 위에서 제공한 데모 계정 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-161">The read-only key is available from the [Keys](manage-account.md#keys) blade of the Azure portal or you can use the demo account information provided above.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 계정 키](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > <span data-ttu-id="8dcfc-163">"지정된 데이터베이스를 찾을 수 없습니다."라는 오류가 발생할 경우</span><span class="sxs-lookup"><span data-stu-id="8dcfc-163">If you get an error that says "The specified database was not found."</span></span> <span data-ttu-id="8dcfc-164">이 [Power BI 문제](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200) 커뮤니티의 문제 해결 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-164">see the workaround steps in this [Power BI issue](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).</span></span>
    
9. <span data-ttu-id="8dcfc-165">계정이 성공적으로 연결되면 **탐색기** 가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-165">When the account is successfully connected, the **Navigator** will appear.</span></span>  <span data-ttu-id="8dcfc-166">**탐색기** 는 계정의 데이터베이스 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-166">The **Navigator** will show a list of databases under the account.</span></span>
10. <span data-ttu-id="8dcfc-167">보고서의 데이터를 가져올 데이터베이스를 클릭하여 확장합니다. 데모 계정을 사용하는 경우 **volcanodb**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-167">Click and expand on the database where the data for the report will come from, if you're using the demo account, select **volcanodb**.</span></span>   
11. <span data-ttu-id="8dcfc-168">이제 데이터를 가져올 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-168">Now, select a collection that you will retrieve the data from.</span></span> <span data-ttu-id="8dcfc-169">데모 계정을 사용하는 경우 **volcano1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-169">If you're using the demo account, select **volcano1**.</span></span>
    
    <span data-ttu-id="8dcfc-170">미리 보기 창에는 **레코드** 항목의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-170">The Preview pane shows a list of **Record** items.</span></span>  <span data-ttu-id="8dcfc-171">문서는 Power BI에서 **레코드** 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-171">A Document is represented as a **Record** type in Power BI.</span></span> <span data-ttu-id="8dcfc-172">마찬가지로, 문서 내의 중첩된 JSON 블록도 **레코드**입니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-172">Similarly, a nested JSON block inside a document is also a **Record**.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 탐색기 창](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. <span data-ttu-id="8dcfc-174">**편집**을 클릭하여 새 창에서 쿼리 편집기를 시작해 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-174">Click **Edit** to launch the Query Editor in a new window to transform the data.</span></span>

## <a name="flattening-and-transforming-json-documents"></a><span data-ttu-id="8dcfc-175">JSON 문서 평면화 및 변환</span><span class="sxs-lookup"><span data-stu-id="8dcfc-175">Flattening and transforming JSON documents</span></span>
1. <span data-ttu-id="8dcfc-176">Power BI 쿼리 편집기 창으로 전환합니다. 가운데 창에 **문서** 열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-176">Switch to the Power BI Query Editor window, where the **Document** column in the center pane.</span></span>
   <span data-ttu-id="8dcfc-177">![Power BI 데스크톱 쿼리 편집기](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span><span class="sxs-lookup"><span data-stu-id="8dcfc-177">![Power BI Desktop Query Editor](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span></span>
2. <span data-ttu-id="8dcfc-178">**문서** 열 머리글의 오른쪽에서 확장 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-178">Click on the expander at the right side of the **Document** column header.</span></span>  <span data-ttu-id="8dcfc-179">필드 목록이 있는 상황에 맞는 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-179">The context menu with a list of fields will appear.</span></span>  <span data-ttu-id="8dcfc-180">화산 이름, 국가, 지역, 위치, 상승, 유형, 상태, 마지막 분출일 등, 보고서에 필요한 필드를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-180">Select the fields you need for your report, for instance,  Volcano Name, Country, Region, Location, Elevation, Type, Status and Last Know Eruption, and then click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 문서 확장](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. <span data-ttu-id="8dcfc-182">가운데 창에는 선택한 필드와 함께 결과의 미리 보기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-182">The center pane will display a preview of the result with the fields selected.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 결과 평면화](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. <span data-ttu-id="8dcfc-184">이 예제에서 위치 속성은 문서의 GeoJSON 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-184">In our example, the Location property is a GeoJSON block in a document.</span></span>  <span data-ttu-id="8dcfc-185">보이는 것처럼 위치는 Power BI 데스크톱에서 **레코드** 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-185">As you can see, Location is represented as a **Record** type in Power BI Desktop.</span></span>  
5. <span data-ttu-id="8dcfc-186">위치 열 머리글의 오른쪽에서 확장 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-186">Click on the expander at the right side of the Location column header.</span></span>  <span data-ttu-id="8dcfc-187">유형 및 좌표 필드가 있는 상황에 맞는 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-187">The context menu with type and coordinates fields will appear.</span></span>  <span data-ttu-id="8dcfc-188">좌표 필드를 선택하고 **확인**을 클릭해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-188">Let's select the coordinates field and click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 위치 레코드](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. <span data-ttu-id="8dcfc-190">이제 가운데 창에는 **목록** 유형의 좌표 열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-190">The center pane now shows a coordinates column of **List** type.</span></span>  <span data-ttu-id="8dcfc-191">자습서의 시작 부분에서 본 것처럼 이 자습서의 GeoJSON 데이터는 지점 유형으로, 위도와 경도 값이 좌표 배열에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-191">As shown at the beginning of the tutorial, the GeoJSON data in this tutorial is of Point type with Latitude and Longitude values recorded in the coordinates array.</span></span>
   
    <span data-ttu-id="8dcfc-192">좌표 [0] 요소는 경도를, 좌표 [1]은 위도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-192">The coordinates[0] element represents Longitude while coordinates[1] represents Latitude.</span></span>
    <span data-ttu-id="8dcfc-193">![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 좌표 목록](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span><span class="sxs-lookup"><span data-stu-id="8dcfc-193">![Power BI tutorial for Azure Cosmos DB Power BI connector - Coordinates list](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span></span>
7. <span data-ttu-id="8dcfc-194">좌표 배열을 평면화하기 위해 이름이 LatLong인 **사용자 지정 열** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-194">To flatten the coordinates array, we will create a **Custom Column** called LatLong.</span></span>  <span data-ttu-id="8dcfc-195">**열 추가** 리본을 선택하고 **사용자 지정 열 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-195">Select the **Add Column** ribbon and click on **Add Custom Column**.</span></span>  <span data-ttu-id="8dcfc-196">**사용자 지정 열 추가** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-196">The **Add Custom Column** window should appear.</span></span>
8. <span data-ttu-id="8dcfc-197">LatLong 등, 새 열에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-197">Provide a name for the new column, e.g. LatLong.</span></span>
9. <span data-ttu-id="8dcfc-198">다음으로 새 열에 사용자 지정 수식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-198">Next, specify the custom formula for the new column.</span></span>  <span data-ttu-id="8dcfc-199">이 예에서는 `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`수식을 사용하여 쉼표로 구분하여 위도와 경도 값을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-199">For our example, we will concatenate the Latitude and Longitude values separated by a comma as shown below using the following formula: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`.</span></span> <span data-ttu-id="8dcfc-200">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-200">Click **OK**.</span></span>
   
    <span data-ttu-id="8dcfc-201">DAX 함수를 포함한 데이터 분석 식(DAX)에 대한 자세한 내용은 [Power BI 데스크톱의 DAX 기초](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-201">For more information on Data Analysis Expressions (DAX) including DAX functions, please visit [DAX Basic in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 사용자 지정 열 추가](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. <span data-ttu-id="8dcfc-203">이제 가운데 창에 쉼표로 구분한 위도와 경도 값이 입력된 새 LatLong 열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-203">Now, the center pane will show the new LatLong column populated with the Latitude and Longitude values separated by a comma.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 사용자 지정 LatLong 열](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    <span data-ttu-id="8dcfc-205">새 열에 오류를 수신하는 경우 쿼리 설정에서 적용된 단계가 다음 그림과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-205">If you receive an Error in the new column, make sure that the applied steps under Query Settings match the following figure:</span></span>
    
    ![적용된 단계는 원본, 탐색, 확장된 문서, 확장된 Document.Location, 추가된 사용자 지정이어야 합니다.](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    <span data-ttu-id="8dcfc-207">단계가 다른 경우 추가 단계를 삭제하고 사용자 지정 열을 다시 추가해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-207">If your steps are different, delete the extra steps and try adding the custom column again.</span></span> 
11. <span data-ttu-id="8dcfc-208">이제 탭 형식으로 데이터를 평면화했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-208">We have now completed flattening the data into tabular format.</span></span>  <span data-ttu-id="8dcfc-209">쿼리 편집기에서 사용 가능한 모든 기능을 활용하여 Cosmos DB에서 데이터를 형성 및 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-209">You can leverage all of the features available in the Query Editor to shape and transform data in Cosmos DB.</span></span>  <span data-ttu-id="8dcfc-210">샘플을 사용하는 경우 **홈** 리본 메뉴에서 **데이터 형식**을 변경하여 상승의 데이터 형식을 **정수**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-210">If you're using the sample, change the data type for Elevation to **Whole number** by changing the **Data Type** on the **Home** ribbon.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 열 형식 변경](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. <span data-ttu-id="8dcfc-212">**닫고 적용** 을 클릭하여 데이터 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-212">Click **Close and Apply** to save the data model.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 닫기 및 적용](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-the-reports"></a><span data-ttu-id="8dcfc-214">보고서 작성</span><span class="sxs-lookup"><span data-stu-id="8dcfc-214">Build the reports</span></span>
<span data-ttu-id="8dcfc-215">Power BI Desktop 보고서 보기에서는 데이터를 시각화하는 보고서 만들기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-215">Power BI Desktop Report view is where you can start creating reports to visualize data.</span></span>  <span data-ttu-id="8dcfc-216">필드를 끌어서 **보고서** 캔버스에 놓으면 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-216">You can create reports by dragging and dropping fields into the **Report** canvas.</span></span>

![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

<span data-ttu-id="8dcfc-218">보고서 보기에는 다음과 같은 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-218">In the Report view, you should find:</span></span>

1. <span data-ttu-id="8dcfc-219">**필드** 창. 보고서에 사용할 수 있는 필드와 데이터 모델 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-219">The **Fields** pane, this is where you will see a list of data models with fields you can use for your reports.</span></span>
2. <span data-ttu-id="8dcfc-220">**시각화** 창.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-220">The **Visualizations** pane.</span></span> <span data-ttu-id="8dcfc-221">보고서는 단일 또는 여러 시각화 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-221">A report can contain a single or multiple visualizations.</span></span>  <span data-ttu-id="8dcfc-222">**시각화** 창에서 필요에 부합하는 시각화 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-222">Pick the visual types fitting your needs from the **Visualizations** pane.</span></span>
3. <span data-ttu-id="8dcfc-223">**보고서** 캔버스. 보고서의 시각적 요소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-223">The **Report** canvas, this is where you will build the visuals for your report.</span></span>
4. <span data-ttu-id="8dcfc-224">**보고서** 페이지.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-224">The **Report** page.</span></span> <span data-ttu-id="8dcfc-225">Power BI 데스크톱에서 여러 보고서 페이지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-225">You can add multiple report pages in Power BI Desktop.</span></span>

<span data-ttu-id="8dcfc-226">다음은 간단한 대화형 지도 보기 보고서를 만드는 기본적은 단계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-226">The following shows the basic steps of creating a simple interactive Map view report.</span></span>

1. <span data-ttu-id="8dcfc-227">이 예에서는 각 화산의 위치를 나타내는 지도를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-227">For our example, we will create a map view showing the location of each volcano.</span></span>  <span data-ttu-id="8dcfc-228">**시각화** 창에서 위의 스크린샷에 강조 표시된 대로 지도 시각 유형을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-228">In the **Visualizations** pane, click on the Map visual type as highlighted in the screenshot above.</span></span>  <span data-ttu-id="8dcfc-229">**보고서** 캔버스에 지도 시각 형식이 칠해져 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-229">You should see the Map visual type painted on the **Report** canvas.</span></span>  <span data-ttu-id="8dcfc-230">**시각화** 창에도 지도 시각 유형과 관련한 속성 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-230">The **Visualization** pane should also display a set of properties related to the Map visual type.</span></span>
2. <span data-ttu-id="8dcfc-231">**필드** 창에서 LatLong 필드를 끌어서 **시각화** 창의 **위치** 속성에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-231">Now, drag and drop the LatLong field from the **Fields** pane to the **Location** property in **Visualizations** pane.</span></span>
3. <span data-ttu-id="8dcfc-232">다음으로 화산 이름 필드를 끌어서 **범례** 에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-232">Next, drag and drop the Volcano Name field to the **Legend** property.</span></span>  
4. <span data-ttu-id="8dcfc-233">이제 상승 필드를 끌어서 **크기** 속성에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-233">Then, drag and drop the Elevation field to the **Size** property.</span></span>  
5. <span data-ttu-id="8dcfc-234">이제 맵에 화산의 상승 위치에 따른 크기의 버블로 각 화산의 위치를 시각적으로 나타내는 버블 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-234">You should now see the Map visual showing a set of bubbles indicating the location of each volcano with the size of the bubble correlating to the elevation of the volcano.</span></span>
6. <span data-ttu-id="8dcfc-235">이제 기본 보고서를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-235">You now have created a basic report.</span></span>  <span data-ttu-id="8dcfc-236">다른 시각화 요소를 추가하여 보고서를 상세히 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-236">You can further customize the report by adding more visualizations.</span></span>  <span data-ttu-id="8dcfc-237">여기서는 화산 유형 슬라이서를 추가하여 보고서를 대화형으로 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-237">In our case, we added a Volcano Type slicer to make the report interactive.</span></span>  
   
    ![Azure Cosmos DB에 대한 Power BI 자습서 완료 시의 최종 Power BI Desktop 보고서 스크린샷](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a><span data-ttu-id="8dcfc-239">보고서 게시 및 공유</span><span class="sxs-lookup"><span data-stu-id="8dcfc-239">Publish and share your report</span></span>
<span data-ttu-id="8dcfc-240">보고서를 공유하려면 PowerBI.com에 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-240">To share your report, you must have an account in PowerBI.com.</span></span>

1. <span data-ttu-id="8dcfc-241">Power BI 데스크톱에서 **홈** 리본을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-241">In the Power BI Desktop, click on the **Home** ribbon.</span></span>
2. <span data-ttu-id="8dcfc-242">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-242">Click **Publish**.</span></span>  <span data-ttu-id="8dcfc-243">PowerBI.com 계정의 사용자 이름 및 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-243">You will be prompted to enter the user name and password for your PowerBI.com account.</span></span>
3. <span data-ttu-id="8dcfc-244">자격 증명이 인증되면 보고서가 선택한 대상에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-244">Once the credential has been authenticated, the report is published to your destination you selected.</span></span>
4. <span data-ttu-id="8dcfc-245">**Power BI에서 'PowerBITutorial.pbix' 열기** 를 클릭하여 PowerBI.com에서 보고서를 보고 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-245">Click **Open 'PowerBITutorial.pbix' in Power BI** to see and share your report on PowerBI.com.</span></span>
   
    ![Power BI에 게시 성공!](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a><span data-ttu-id="8dcfc-248">PowerBI.com에서 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="8dcfc-248">Create a dashboard in PowerBI.com</span></span>
<span data-ttu-id="8dcfc-249">이제 보고서가 있으니 PowerBI.com에서 공유하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-249">Now that you have a report, lets share it on PowerBI.com</span></span>

<span data-ttu-id="8dcfc-250">보고서를 Power BI 데스크톱에서 PowerBI.com에 게시하는 경우 PowerBI.com 테넌트에 **보고서** 및 **데이터 집합**을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-250">When you publish your report from Power BI Desktop to PowerBI.com, it generates a **Report** and a **Dataset** in your PowerBI.com tenant.</span></span> <span data-ttu-id="8dcfc-251">예를 들어 **PowerBITutorial**이라는 보고서를 PowerBI.com에 게시한 후 PowerBI.com의 **보고서** 및 **데이터 집합** 섹션 모두에서 PowerBITutorial이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-251">For example, after you published a report called **PowerBITutorial** to PowerBI.com, you will see PowerBITutorial in both the **Reports** and **Datasets** sections on PowerBI.com.</span></span>

   ![PowerBI.com에서 새 보고서 및 데이터 집합의 스크린샷](./media/powerbi-visualize/powerbi-reports-datasets.png)

<span data-ttu-id="8dcfc-253">공유할 수 있는 대시보드를 만들려면 PowerBI.com 보고서의 **라이브 페이지 고정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-253">To create a sharable dashboard, click the **Pin Live Page** button on your PowerBI.com report.</span></span>

   ![PowerBI.com에서 새 보고서 및 데이터 집합의 스크린샷](./media/powerbi-visualize/power-bi-pin-live-tile.png)

<span data-ttu-id="8dcfc-255">그런 다음 [보고서에서 타일을 고정](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) 의 지침을 따라 새 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-255">Then follow the instructions in [Pin a tile from a report](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) to create a new dashboard.</span></span> 

<span data-ttu-id="8dcfc-256">또한 대시보드를 만들기 전에 보고서에 대한 임시 수정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-256">You can also do ad hoc modifications to report before creating a dashboard.</span></span> <span data-ttu-id="8dcfc-257">그러나 Power BI 데스크톱을 사용하여 수정 작업을 수행하고 보고서를 PowerBI.com 다시 게시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-257">However, it's recommended that you use Power BI Desktop to perform the modifications and republish the report to PowerBI.com.</span></span>

## <a name="refresh-data-in-powerbicom"></a><span data-ttu-id="8dcfc-258">PowerBI.com에서 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="8dcfc-258">Refresh data in PowerBI.com</span></span>
<span data-ttu-id="8dcfc-259">임시 및 예약의 두 가지 방법으로 데이터를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-259">There are two ways to refresh data, ad hoc and scheduled.</span></span>

<span data-ttu-id="8dcfc-260">임시 새로 고침의 경우 **데이터 집**으로 줄임표(...)를 클릭합니다(예: PowerBITutorial).</span><span class="sxs-lookup"><span data-stu-id="8dcfc-260">For an ad hoc refresh, simply click on the eclipses (…) by the **Dataset**, e.g. PowerBITutorial.</span></span> <span data-ttu-id="8dcfc-261">**지금 새로 고침**을 포함한 작업의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-261">You should see a list of actions including **Refresh Now**.</span></span> <span data-ttu-id="8dcfc-262">**지금 새로 고침**을 클릭하여 데이터를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-262">Click **Refresh Now** to refresh the data.</span></span>

![PowerBI.com에서 지금 새로 고침의 스크린샷](./media/powerbi-visualize/power-bi-refresh-now.png)

<span data-ttu-id="8dcfc-264">예약된 새로 고침의 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-264">For a scheduled refresh, do the following.</span></span>

1. <span data-ttu-id="8dcfc-265">작업 목록에서 **새로 고침 예약** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-265">Click **Schedule Refresh** in the action list.</span></span> 

    ![PowerBI.com에서 새로 고침 예약의 스크린샷](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. <span data-ttu-id="8dcfc-267">**설정** 페이지에서 **데이터 원본 자격 증명**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-267">In the **Settings** page, expand **Data source credentials**.</span></span> 
3. <span data-ttu-id="8dcfc-268">**자격 증명 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-268">Click on **Edit credentials**.</span></span> 
   
    <span data-ttu-id="8dcfc-269">구성 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-269">The Configure popup appears.</span></span> 
4. <span data-ttu-id="8dcfc-270">키를 입력하여 해당 데이터 집합에 대한 Cosmos DB 계정에 연결한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-270">Enter the key to connect to the Cosmos DB account for that data set, then click **Sign in**.</span></span> 
5. <span data-ttu-id="8dcfc-271">**새로 고침 예약** 을 확장하고 데이터 집합을 새로 고치려는 일정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-271">Expand **Schedule Refresh** and set up the schedule you want to refresh the dataset.</span></span> 
6. <span data-ttu-id="8dcfc-272">**적용** 을 클릭하고 예약된 새로 고침 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-272">Click **Apply** and you are done setting up the scheduled refresh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dcfc-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8dcfc-273">Next steps</span></span>
* <span data-ttu-id="8dcfc-274">Power BI에 대한 자세한 내용은 [Power BI 시작](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-274">To learn more about Power BI, see [Get started with Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).</span></span>
* <span data-ttu-id="8dcfc-275">Cosmos DB에 대한 자세한 내용은 [Azure Cosmos DB 설명서 방문 페이지](https://azure.microsoft.com/documentation/services/documentdb/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dcfc-275">To learn more about Cosmos DB, see the [Azure Cosmos DB documentation landing page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

