---
title: "Azure Cosmos DB 커넥터에 대 한 aaaPower BI 자습서 | Microsoft Docs"
description: "이 Power BI 자습서 tooimport JSON을 사용 하 고, 통찰력 있는 보고서를 만들 하 고 및 hello Azure Cosmos DB와 Power BI 커넥터를 사용 하 여 데이터를 시각화 합니다."
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
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a><span data-ttu-id="be4d2-104">Azure Cosmos DB에 대 한 power BI 자습서: Power BI 커넥터 hello를 사용 하 여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="be4d2-104">Power BI tutorial for Azure Cosmos DB: Visualize data using hello Power BI connector</span></span>
<span data-ttu-id="be4d2-105">[PowerBI.com](https://powerbi.microsoft.com/) 은 온라인 서비스 만들기 및 중요 한 tooyou 및 조직 된 데이터로 대시보드 및 보고서를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-105">[PowerBI.com](https://powerbi.microsoft.com/) is an online service where you can create and share dashboards and reports with data that's important tooyou and your organization.</span></span>  <span data-ttu-id="be4d2-106">Power BI Desktop에는 전용 제작 도구를 사용 하면입니다 tooretrieve에서에서 보고서 데이터를 다양 한 데이터 원본, 병합 및 hello 데이터 변환, 강력한 보고서 및 시각화를 만들고 게시 hello 보고서 tooPower BI은 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-106">Power BI Desktop is a dedicated report authoring tool that enables you tooretrieve data from various data sources, merge and transform hello data, create powerful reports and visualizations, and publish hello reports tooPower BI.</span></span>  <span data-ttu-id="be4d2-107">Hello Power BI Desktop의 최신 버전으로 Power BI에 대 한 hello Cosmos DB 커넥터를 통해 tooyour Cosmos DB 계정 이제 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-107">With hello latest version of Power BI Desktop, you can now connect tooyour Cosmos DB account via hello Cosmos DB connector for Power BI.</span></span>   

<span data-ttu-id="be4d2-108">이 Power BI 자습서 hello 단계 tooconnect tooa Cosmos DB 계정 Power BI Desktop의 과정을 안내 했습니다,이 tooa 컬렉션 변환 JSON 데이터를 Power BI Desktop 쿼리를 사용 하 여 테이블 형식으로 탐색 창의 hello를 사용 하 여 tooextract hello 데이터를 원하는 위치로 이동 편집기 및 작성 하 고 보고서 tooPowerBI.com 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-108">In this Power BI tutorial, we walk through hello steps tooconnect tooa Cosmos DB account in Power BI Desktop, navigate tooa collection where we want tooextract hello data using hello Navigator, transform JSON data into tabular format using Power BI Desktop Query Editor, and build and publish a report tooPowerBI.com.</span></span>

<span data-ttu-id="be4d2-109">이 Power BI 자습서를 완료 하면 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-109">After completing this Power BI tutorial, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="be4d2-110">Power BI Desktop을 사용하여 Cosmos DB의 데이터로 보고서를 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="be4d2-110">How can I build reports with data from Cosmos DB using Power BI Desktop?</span></span>
* <span data-ttu-id="be4d2-111">Power BI Desktop에서 tooa Cosmos DB 계정은 어떻게 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="be4d2-111">How can I connect tooa Cosmos DB account in Power BI Desktop?</span></span>
* <span data-ttu-id="be4d2-112">Power BI 데스크톱의 컬렉션에서 데이터를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="be4d2-112">How can I retrieve data from a collection in Power BI Desktop?</span></span>
* <span data-ttu-id="be4d2-113">Power BI 데스크톱에서 중첩된 JSON 데이터를 변환하는 방법</span><span class="sxs-lookup"><span data-stu-id="be4d2-113">How can I transform nested JSON data in Power BI Desktop?</span></span>
* <span data-ttu-id="be4d2-114">PowerBI.com에서 내 보고서를 게시 및 공유하는 방법</span><span class="sxs-lookup"><span data-stu-id="be4d2-114">How can I publish and share my reports in PowerBI.com?</span></span>

> [!NOTE]
> <span data-ttu-id="be4d2-115">Cosmos DB Azure 용 hello Power BI 커넥터 추출 및 데이터 변환에 대 한 BI Desktop tooPower 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-115">hello Power BI connector for Azure Cosmos DB connects tooPower BI Desktop for extraction and transformation of data.</span></span> <span data-ttu-id="be4d2-116">Power BI Desktop에서 만든 보고서 게시 tooPowerBI.com 될 수 있습니다. Azure Cosmos DB 데이터의 직접 추출 및 변환은 PowerBI.com에서 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-116">Reports created in Power BI Desktop can then be published tooPowerBI.com. Direct extraction and transformation of Azure Cosmos DB data cannot be performed in PowerBI.com.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="be4d2-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="be4d2-117">Prerequisites</span></span>
<span data-ttu-id="be4d2-118">이 Power BI 자습서 hello 지침을 수행 하기 전에 다음 리소스 액세스 toohello 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-118">Before following hello instructions in this Power BI tutorial, ensure that you have access toohello following resources:</span></span>

* <span data-ttu-id="be4d2-119">[Power BI Desktop의 최신 버전 hello](https://powerbi.microsoft.com/desktop)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-119">[hello latest version of Power BI Desktop](https://powerbi.microsoft.com/desktop).</span></span>
* <span data-ttu-id="be4d2-120">액세스 tooour 데모 계정 또는 Cosmos DB 계정의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-120">Access tooour demo account or data in your Cosmos DB account.</span></span>
  * <span data-ttu-id="be4d2-121">hello 데모 계정이이 자습서의 예제는 hello 화산 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-121">hello demo account is populated with hello volcano data shown in this tutorial.</span></span> <span data-ttu-id="be4d2-122">이 데모 계정은 SLA와 연결되지 않으며 데모용으로만 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-122">This demo account is not bound by any SLAs and is meant for demonstration purposes only.</span></span>  <span data-ttu-id="be4d2-123">Hello 오른쪽 toomake 수정 toothis 데모 계정을 포함 하는 예약 되어있습니다 하지만 변경, 액세스를 제한 하는 hello 키를 변경 하는 계정이 hello 및 이유 또는 사전 통지 없이 언제 든 지 hello 데이터를 delete 종료에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-123">We reserve hello right toomake modifications toothis demo account including but not limited to, terminating hello account, changing hello key, restricting access, changing, and delete hello data, at any time without advance notice or reason.</span></span>
    * <span data-ttu-id="be4d2-124">URL: https://analytics.documents.azure.com</span><span class="sxs-lookup"><span data-stu-id="be4d2-124">URL: https://analytics.documents.azure.com</span></span>
    * <span data-ttu-id="be4d2-125">읽기 전용 키: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span><span class="sxs-lookup"><span data-stu-id="be4d2-125">Read-only key: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span></span>
  * <span data-ttu-id="be4d2-126">또는 toocreate 사용자 고유의 계정 참조 [hello Azure 포털을 사용 하 여 Azure Cosmos DB 데이터베이스 계정 만들기](https://azure.microsoft.com/documentation/articles/create-account/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-126">Or, toocreate your own account, see [Create an Azure Cosmos DB database account using hello Azure portal](https://azure.microsoft.com/documentation/articles/create-account/).</span></span> <span data-ttu-id="be4d2-127">그런 다음 tooget 샘플 화산 데이터 비슷한 toowhat는이 자습서에 사용 (hello GeoJSON 블록을 포함 하지 않는) 참조 하십시오 hello [NOAA 사이트](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) 다음 hello를 사용 하 여 hello 데이터를 가져올 [Azure Cosmos DB 데이터 마이그레이션 도구](import-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-127">Then, tooget sample volcano data that's similar toowhat's used in this tutorial (but does not contain hello GeoJSON blocks), see hello [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) and then import hello data using hello [Azure Cosmos DB data migration tool](import-data.md).</span></span>

<span data-ttu-id="be4d2-128">tooshare 보고서를 PowerBI.com에서 PowerBI.com에서 계정이 있어야 합니다.  Power BI 무료 및 Power BI Pro에 대 한 자세한 정보는 toolearn 방문 [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-128">tooshare your reports in PowerBI.com, you must have an account in PowerBI.com.  toolearn more about Power BI for Free and Power BI Pro, visit [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).</span></span>

## <a name="lets-get-started"></a><span data-ttu-id="be4d2-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-129">Let's get started</span></span>
<span data-ttu-id="be4d2-130">이 자습서에서는 화산 hello 전 세계의 내용을 파악 geologist 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-130">In this tutorial, let's imagine that you are a geologist studying volcanoes around hello world.</span></span>  <span data-ttu-id="be4d2-131">hello 화산 데이터 Cosmos DB 계정에 저장 됩니다 및 샘플 문서 다음 hello 같이 hello JSON 문서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-131">hello volcano data is stored in a Cosmos DB account and hello JSON documents look like hello following sample document.</span></span>

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

<span data-ttu-id="be4d2-132">원하는 tooretrieve hello 화산 데이터 hello Cosmos DB에서에서 계정 및 보고서를 수행 하는 hello와 같은 대화형 Power BI 보고서에서 데이터를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-132">You want tooretrieve hello volcano data from hello Cosmos DB account and visualize data in an interactive Power BI report like hello following report.</span></span>

![Hello Power BI 커넥터와 함께이 Power BI 자습서를 완료 하 여 Power BI Desktop 화산 보고서 hello 사용 하 여 수 toovisualize 데이터 됩니다.](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

<span data-ttu-id="be4d2-134">준비 toogive 시도?</span><span class="sxs-lookup"><span data-stu-id="be4d2-134">Ready toogive it a try?</span></span> <span data-ttu-id="be4d2-135">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-135">Let's get started.</span></span>

1. <span data-ttu-id="be4d2-136">워크스테이션에서 Power BI 데스크톱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-136">Run Power BI Desktop on your workstation.</span></span>
2. <span data-ttu-id="be4d2-137">Power BI 데스크톱이 시작되면 *시작* 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-137">Once Power BI Desktop is launched, a *Welcome* screen is displayed.</span></span>
   
    ![Power BI 데스크톱 시작 화면 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. <span data-ttu-id="be4d2-139">할 수 있습니다 **데이터 가져오기**, 참조 **최근 소스**, 또는 **다른 보고서 열기** hello에서 직접 *시작* 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-139">You can **Get Data**, see **Recent Sources**, or **Open Other Reports** directly from hello *Welcome* screen.</span></span>  <span data-ttu-id="be4d2-140">Hello 오른쪽 위 모서리 tooclose hello 화면에 hello X를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-140">Click hello X at hello top right corner tooclose hello screen.</span></span> <span data-ttu-id="be4d2-141">hello **보고서** Power BI Desktop의 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-141">hello **Report** view of Power BI Desktop is displayed.</span></span>
   
    ![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. <span data-ttu-id="be4d2-143">선택 hello **홈** 리본을 클릭 한 다음 **데이터 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-143">Select hello **Home** ribbon, then click on **Get Data**.</span></span>  <span data-ttu-id="be4d2-144">hello **데이터 가져오기** 창이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-144">hello **Get Data** window should appear.</span></span>
5. <span data-ttu-id="be4d2-145">**Azure**를 클릭하고 **Microsoft Azure DocumentDB(베타)**를 클릭한 다음 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-145">Click on **Azure**, select **Microsoft Azure DocumentDB (Beta)**, and then click **Connect**.</span></span> 

    ![Power BI 데스크톱 데이터 가져오기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. <span data-ttu-id="be4d2-147">Hello에 **미리 보기 커넥터** 페이지 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-147">On hello **Preview Connector** page, click **Continue**.</span></span> <span data-ttu-id="be4d2-148">hello **Microsoft Azure DocumentDB Connect** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-148">hello **Microsoft Azure DocumentDB Connect** window appears.</span></span>
7. <span data-ttu-id="be4d2-149">Tooretrieve hello 데이터를 아래와 같이 선택한 다음 클릭 hello Cosmos DB 계정 끝점 URL 지정 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-149">Specify hello Cosmos DB account endpoint URL you would like tooretrieve hello data from as shown below, and then click **OK**.</span></span> <span data-ttu-id="be4d2-150">toouse 사용자 고유의 계정 hello hello URI에서에서 URL 상자 hello에 검색할 수 있습니다  **[키](manage-account.md#keys)**  블레이드 hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="be4d2-150">toouse your own account, you can retrieve hello URL from hello URI box in hello **[Keys](manage-account.md#keys)** blade of hello Azure portal.</span></span> <span data-ttu-id="be4d2-151">toouse hello 계정 데모, 입력 `https://analytics.documents.azure.com` hello URL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-151">toouse hello demo account, enter `https://analytics.documents.azure.com` for hello URL.</span></span> 
   
    <span data-ttu-id="be4d2-152">비워 hello 데이터베이스 이름, 컬렉션 이름 및 SQL 문 처럼 이러한 필드는 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="be4d2-152">Leave hello database name, collection name, and SQL statement blank as these fields are optional.</span></span>  <span data-ttu-id="be4d2-153">대신, hello 탐색기 tooselect hello 데이터베이스 및 컬렉션 tooidentify hello 데이터에서 제공 하는 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-153">Instead, we will use hello Navigator tooselect hello Database and Collection tooidentify where hello data comes from.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 데스크톱 연결 창](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. <span data-ttu-id="be4d2-155">을 연결 하는 hello에 대 한 toothis 끝점 처음으로 hello 계정 키에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-155">If you are connecting toothis endpoint for hello first time, you are prompted for hello account key.</span></span> <span data-ttu-id="be4d2-156">사용자 고유의 계정에 대 한 hello에서 hello 키 검색 **기본 키** 상자 hello에  **[읽기 전용 키](manage-account.md#keys)**  블레이드 hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="be4d2-156">For your own account, retrieve hello key from hello **Primary Key** box in hello **[Read-only Keys](manage-account.md#keys)** blade of hello Azure portal.</span></span> <span data-ttu-id="be4d2-157">Hello 데모 계정에 대 한 hello 키는 `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-157">For hello demo account, hello key is `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`.</span></span> <span data-ttu-id="be4d2-158">Hello 적절 한 키를 입력 한 다음 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-158">Enter hello appropriate key and then click **Connect**.</span></span>
   
    <span data-ttu-id="be4d2-159">보고서를 작성할 때 hello 읽기 전용 키를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-159">We recommend that you use hello read-only key when building reports.</span></span>  <span data-ttu-id="be4d2-160">이렇게 하면 hello 마스터 키 toopotential 보안 위험의 불필요 하 게 노출이 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-160">This will prevent unnecessary exposure of hello master key toopotential security risks.</span></span> <span data-ttu-id="be4d2-161">hello 읽기 전용 키가 hello에서 사용할 수 있는 [키](manage-account.md#keys) hello Azure 포털의 블레이드 위에 제공 된 hello 데모 계정 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-161">hello read-only key is available from hello [Keys](manage-account.md#keys) blade of hello Azure portal or you can use hello demo account information provided above.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 계정 키](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > <span data-ttu-id="be4d2-163">오류가 발생할 경우 "hello 지정 된 데이터베이스를 찾을 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="be4d2-163">If you get an error that says "hello specified database was not found."</span></span> <span data-ttu-id="be4d2-164">hello 해결 방법은이 단계를 참조 [Power BI 문제](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-164">see hello workaround steps in this [Power BI issue](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).</span></span>
    
9. <span data-ttu-id="be4d2-165">Hello 계정을 성공적으로 연결 되 면 hello **탐색기** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-165">When hello account is successfully connected, hello **Navigator** will appear.</span></span>  <span data-ttu-id="be4d2-166">hello **탐색기** hello 계정에서 데이터베이스 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-166">hello **Navigator** will show a list of databases under hello account.</span></span>
10. <span data-ttu-id="be4d2-167">클릭 하 고 여기서 hello 데이터 hello 데모 계정을 사용 하 여 hello 보고서에서 옵니다에 대 한 선택 hello 데이터베이스에서 확장 **volcanodb**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-167">Click and expand on hello database where hello data for hello report will come from, if you're using hello demo account, select **volcanodb**.</span></span>   
11. <span data-ttu-id="be4d2-168">이제 있습니다 hello 데이터를 검색 하는 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-168">Now, select a collection that you will retrieve hello data from.</span></span> <span data-ttu-id="be4d2-169">데모 계정 hello를 사용 하는 경우 선택 **volcano1**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-169">If you're using hello demo account, select **volcano1**.</span></span>
    
    <span data-ttu-id="be4d2-170">hello 미리 보기 창에는 목록이 표시 **레코드** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-170">hello Preview pane shows a list of **Record** items.</span></span>  <span data-ttu-id="be4d2-171">문서는 Power BI에서 **레코드** 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-171">A Document is represented as a **Record** type in Power BI.</span></span> <span data-ttu-id="be4d2-172">마찬가지로, 문서 내의 중첩된 JSON 블록도 **레코드**입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-172">Similarly, a nested JSON block inside a document is also a **Record**.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 탐색기 창](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. <span data-ttu-id="be4d2-174">클릭 **편집** toolaunch hello 쿼리 편집기에서 새 창 tootransform hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-174">Click **Edit** toolaunch hello Query Editor in a new window tootransform hello data.</span></span>

## <a name="flattening-and-transforming-json-documents"></a><span data-ttu-id="be4d2-175">JSON 문서 평면화 및 변환</span><span class="sxs-lookup"><span data-stu-id="be4d2-175">Flattening and transforming JSON documents</span></span>
1. <span data-ttu-id="be4d2-176">여기서 hello toohello Power BI 쿼리 편집기 창 전환 **문서** hello 가운데 창에서 열.</span><span class="sxs-lookup"><span data-stu-id="be4d2-176">Switch toohello Power BI Query Editor window, where hello **Document** column in hello center pane.</span></span>
   <span data-ttu-id="be4d2-177">![Power BI 데스크톱 쿼리 편집기](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span><span class="sxs-lookup"><span data-stu-id="be4d2-177">![Power BI Desktop Query Editor](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span></span>
2. <span data-ttu-id="be4d2-178">Hello 확장기 hello의 hello 오른쪽 클릭 **문서** 열 머리글입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-178">Click on hello expander at hello right side of hello **Document** column header.</span></span>  <span data-ttu-id="be4d2-179">필드 목록 사용 하 여 hello 상황에 맞는 메뉴가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-179">hello context menu with a list of fields will appear.</span></span>  <span data-ttu-id="be4d2-180">예를 들어, 보고서에 필요한 hello 필드, 화산 이름, 국가, 지역, 위치, 권한 상승, 유형, 상태 및 마지막 알고 폭발 및 클릭 한 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-180">Select hello fields you need for your report, for instance,  Volcano Name, Country, Region, Location, Elevation, Type, Status and Last Know Eruption, and then click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 문서 확장](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. <span data-ttu-id="be4d2-182">hello 가운데 창의 hello 필드가 선택 된 hello 결과의 미리 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-182">hello center pane will display a preview of hello result with hello fields selected.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 결과 평면화](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. <span data-ttu-id="be4d2-184">예에서 hello Location 속성은 문서에서 GeoJSON 블록.</span><span class="sxs-lookup"><span data-stu-id="be4d2-184">In our example, hello Location property is a GeoJSON block in a document.</span></span>  <span data-ttu-id="be4d2-185">보이는 것처럼 위치는 Power BI 데스크톱에서 **레코드** 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-185">As you can see, Location is represented as a **Record** type in Power BI Desktop.</span></span>  
5. <span data-ttu-id="be4d2-186">Hello hello 위치 열 머리글의 오른쪽에 hello 확장기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-186">Click on hello expander at hello right side of hello Location column header.</span></span>  <span data-ttu-id="be4d2-187">유형 및 좌표 필드와 hello 상황에 맞는 메뉴가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-187">hello context menu with type and coordinates fields will appear.</span></span>  <span data-ttu-id="be4d2-188">보겠습니다 hello 좌표 필드를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-188">Let's select hello coordinates field and click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 위치 레코드](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. <span data-ttu-id="be4d2-190">hello 가운데 창 이제 표시의 좌표 열 **목록** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-190">hello center pane now shows a coordinates column of **List** type.</span></span>  <span data-ttu-id="be4d2-191">Hello 자습서의 hello 시작 부분에 표시 된 것과 같이 hello이이 자습서에서는 GeoJSON 데이터 지점 형식의 hello 좌표 배열에 기록 된 위도 및 경도 값이 포함 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-191">As shown at hello beginning of hello tutorial, hello GeoJSON data in this tutorial is of Point type with Latitude and Longitude values recorded in hello coordinates array.</span></span>
   
    <span data-ttu-id="be4d2-192">hello 좌표 [0] 요소는 [1] 좌표는 위도 나타내는 동안 경도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-192">hello coordinates[0] element represents Longitude while coordinates[1] represents Latitude.</span></span>
    <span data-ttu-id="be4d2-193">![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 좌표 목록](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span><span class="sxs-lookup"><span data-stu-id="be4d2-193">![Power BI tutorial for Azure Cosmos DB Power BI connector - Coordinates list](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span></span>
7. <span data-ttu-id="be4d2-194">tooflatten hello 좌표 배열, 만듭니다는 **사용자 지정 열** LatLong를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-194">tooflatten hello coordinates array, we will create a **Custom Column** called LatLong.</span></span>  <span data-ttu-id="be4d2-195">선택 hello **열 추가** 리본을 클릭할 **사용자 지정 열 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-195">Select hello **Add Column** ribbon and click on **Add Custom Column**.</span></span>  <span data-ttu-id="be4d2-196">hello **사용자 지정 열 추가** 창이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-196">hello **Add Custom Column** window should appear.</span></span>
8. <span data-ttu-id="be4d2-197">예를 들어 LatLong hello 새 열에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-197">Provide a name for hello new column, e.g. LatLong.</span></span>
9. <span data-ttu-id="be4d2-198">그런 다음 hello hello 새 열에 대 한 사용자 지정 수식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-198">Next, specify hello custom formula for hello new column.</span></span>  <span data-ttu-id="be4d2-199">이 예에서는 다음 수식을 hello를 사용 하 여 아래와 같이 쉼표로 구분 된 hello 위도 및 경도 값 연결 합니다: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-199">For our example, we will concatenate hello Latitude and Longitude values separated by a comma as shown below using hello following formula: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`.</span></span> <span data-ttu-id="be4d2-200">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-200">Click **OK**.</span></span>
   
    <span data-ttu-id="be4d2-201">DAX 함수를 포함한 데이터 분석 식(DAX)에 대한 자세한 내용은 [Power BI 데스크톱의 DAX 기초](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="be4d2-201">For more information on Data Analysis Expressions (DAX) including DAX functions, please visit [DAX Basic in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).</span></span>
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 사용자 지정 열 추가](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. <span data-ttu-id="be4d2-203">이제 hello 가운데 창 위도 hello로 채워진 hello 새 LatLong 열 및 경도 값을 쉼표로 구분 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-203">Now, hello center pane will show hello new LatLong column populated with hello Latitude and Longitude values separated by a comma.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 사용자 지정 LatLong 열](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    <span data-ttu-id="be4d2-205">Hello 새 열에는 오류가 나타나면 쿼리 설정 단계 적용 hello hello 다음 그림 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-205">If you receive an Error in hello new column, make sure that hello applied steps under Query Settings match hello following figure:</span></span>
    
    ![적용된 단계는 원본, 탐색, 확장된 문서, 확장된 Document.Location, 추가된 사용자 지정이어야 합니다.](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    <span data-ttu-id="be4d2-207">삭제 단계를 다른 경우 추가 단계를 hello 및 hello 사용자 지정 열을 다시 추가 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="be4d2-207">If your steps are different, delete hello extra steps and try adding hello custom column again.</span></span> 
11. <span data-ttu-id="be4d2-208">표 형식으로 flattening hello 데이터를 완료 했으므로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-208">We have now completed flattening hello data into tabular format.</span></span>  <span data-ttu-id="be4d2-209">모든 쿼리 편집기 tooshape hello에서 사용할 수 있는 hello 기능을 활용할 수 있으며 Cosmos DB에는 데이터를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-209">You can leverage all of hello features available in hello Query Editor tooshape and transform data in Cosmos DB.</span></span>  <span data-ttu-id="be4d2-210">Hello 샘플을 사용 하는 hello 데이터 형식을 변경 권한 상승을 위해 너무**정수** hello를 변경 하 여 **데이터 형식** hello에 **홈** 리본.</span><span class="sxs-lookup"><span data-stu-id="be4d2-210">If you're using hello sample, change hello data type for Elevation too**Whole number** by changing hello **Data Type** on hello **Home** ribbon.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 열 형식 변경](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. <span data-ttu-id="be4d2-212">클릭 **닫고 적용** toosave hello 데이터 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-212">Click **Close and Apply** toosave hello data model.</span></span>
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 닫기 및 적용](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a><span data-ttu-id="be4d2-214">빌드 hello 보고서</span><span class="sxs-lookup"><span data-stu-id="be4d2-214">Build hello reports</span></span>
<span data-ttu-id="be4d2-215">Power BI Desktop 보고서 보기는 toovisualize 데이터 보고서를 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-215">Power BI Desktop Report view is where you can start creating reports toovisualize data.</span></span>  <span data-ttu-id="be4d2-216">Hello에 필드를 끌어다 보고서를 만들 수 **보고서** 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-216">You can create reports by dragging and dropping fields into hello **Report** canvas.</span></span>

![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

<span data-ttu-id="be4d2-218">보고서 보기 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-218">In hello Report view, you should find:</span></span>

1. <span data-ttu-id="be4d2-219">hello **필드** 창은 필드가 보고서에 사용할 수 있는 데이터 모델 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-219">hello **Fields** pane, this is where you will see a list of data models with fields you can use for your reports.</span></span>
2. <span data-ttu-id="be4d2-220">hello **시각화** 창.</span><span class="sxs-lookup"><span data-stu-id="be4d2-220">hello **Visualizations** pane.</span></span> <span data-ttu-id="be4d2-221">보고서는 단일 또는 여러 시각화 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-221">A report can contain a single or multiple visualizations.</span></span>  <span data-ttu-id="be4d2-222">Hello에서 사용자의 요구에 맞추는 방식 hello 시각적 개체 형식 선택 **시각화** 창.</span><span class="sxs-lookup"><span data-stu-id="be4d2-222">Pick hello visual types fitting your needs from hello **Visualizations** pane.</span></span>
3. <span data-ttu-id="be4d2-223">hello **보고서** 캔버스,이 보고서에 대 한 hello 시각적 개체가 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-223">hello **Report** canvas, this is where you will build hello visuals for your report.</span></span>
4. <span data-ttu-id="be4d2-224">hello **보고서** 페이지.</span><span class="sxs-lookup"><span data-stu-id="be4d2-224">hello **Report** page.</span></span> <span data-ttu-id="be4d2-225">Power BI 데스크톱에서 여러 보고서 페이지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-225">You can add multiple report pages in Power BI Desktop.</span></span>

<span data-ttu-id="be4d2-226">hello 다음 hello 간단한 대화형 지도 보기 보고서를 만드는 기본 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-226">hello following shows hello basic steps of creating a simple interactive Map view report.</span></span>

1. <span data-ttu-id="be4d2-227">이 예에서는 각 화산의 hello 위치를 표시 하는 지도 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-227">For our example, we will create a map view showing hello location of each volcano.</span></span>  <span data-ttu-id="be4d2-228">Hello에 **시각화** 창 위의 hello 스크린샷에 강조 표시 된 대로 hello 지도 시각적 종류를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-228">In hello **Visualizations** pane, click on hello Map visual type as highlighted in hello screenshot above.</span></span>  <span data-ttu-id="be4d2-229">Hello에 그릴 hello 지도 시각적 형식이 나타납니다 **보고서** 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-229">You should see hello Map visual type painted on hello **Report** canvas.</span></span>  <span data-ttu-id="be4d2-230">hello **시각화** 창 해야 속성 관련된 toohello 지도 시각적 유형 집합을 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-230">hello **Visualization** pane should also display a set of properties related toohello Map visual type.</span></span>
2. <span data-ttu-id="be4d2-231">이제 hello LatLong 필드를에서 끌어서 hello **필드** 창 toohello **위치** 속성 **시각화** 창.</span><span class="sxs-lookup"><span data-stu-id="be4d2-231">Now, drag and drop hello LatLong field from hello **Fields** pane toohello **Location** property in **Visualizations** pane.</span></span>
3. <span data-ttu-id="be4d2-232">다음으로, 끌어서 놓기 hello 화산 이름 필드 toohello **범례** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-232">Next, drag and drop hello Volcano Name field toohello **Legend** property.</span></span>  
4. <span data-ttu-id="be4d2-233">그런 다음 끌어서 놓기 hello 상승 필드 toohello **크기** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-233">Then, drag and drop hello Elevation field toohello **Size** property.</span></span>  
5. <span data-ttu-id="be4d2-234">이제 거품 hello hello 화산 toohello 상승 상관 관계를 지정 하는 hello 거품 크기와 각 화산의 hello 위치를 나타내는 집합을 보여 주는 시각적 맵 hello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-234">You should now see hello Map visual showing a set of bubbles indicating hello location of each volcano with hello size of hello bubble correlating toohello elevation of hello volcano.</span></span>
6. <span data-ttu-id="be4d2-235">이제 기본 보고서를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-235">You now have created a basic report.</span></span>  <span data-ttu-id="be4d2-236">더 많은 시각화를 추가 하 여 hello 보고서를 추가로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-236">You can further customize hello report by adding more visualizations.</span></span>  <span data-ttu-id="be4d2-237">경우에 slicer toomake hello 화산 형식 보고서 대화형 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-237">In our case, we added a Volcano Type slicer toomake hello report interactive.</span></span>  
   
    ![Power BI 자습서 hello Azure Cosmos DB에 대 한 완료 되 면 hello 최종 Power BI Desktop 보고서의 스크린샷](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a><span data-ttu-id="be4d2-239">보고서 게시 및 공유</span><span class="sxs-lookup"><span data-stu-id="be4d2-239">Publish and share your report</span></span>
<span data-ttu-id="be4d2-240">tooshare 보고서를 PowerBI.com에서 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-240">tooshare your report, you must have an account in PowerBI.com.</span></span>

1. <span data-ttu-id="be4d2-241">Power BI Desktop hello hello 클릭 **홈** 리본.</span><span class="sxs-lookup"><span data-stu-id="be4d2-241">In hello Power BI Desktop, click on hello **Home** ribbon.</span></span>
2. <span data-ttu-id="be4d2-242">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-242">Click **Publish**.</span></span>  <span data-ttu-id="be4d2-243">PowerBI.com 계정에 대 한 증명된 tooenter hello 사용자 이름 및 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-243">You will be prompted tooenter hello user name and password for your PowerBI.com account.</span></span>
3. <span data-ttu-id="be4d2-244">Hello 자격 증명 인증 되 면 hello 보고서는 선택한 게시 된 tooyour 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-244">Once hello credential has been authenticated, hello report is published tooyour destination you selected.</span></span>
4. <span data-ttu-id="be4d2-245">클릭 **Power BI에서 열기 'PowerBITutorial.pbix'** toosee PowerBI.com에서 보고서를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-245">Click **Open 'PowerBITutorial.pbix' in Power BI** toosee and share your report on PowerBI.com.</span></span>
   
    ![게시 tooPower BI 성공!](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a><span data-ttu-id="be4d2-248">PowerBI.com에서 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="be4d2-248">Create a dashboard in PowerBI.com</span></span>
<span data-ttu-id="be4d2-249">이제 보고서가 있으니 PowerBI.com에서 공유하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-249">Now that you have a report, lets share it on PowerBI.com</span></span>

<span data-ttu-id="be4d2-250">TooPowerBI.com Power BI Desktop에서에서 보고서를 게시 하는 경우에 생성 한 **보고서** 및 **데이터 집합** PowerBI.com 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-250">When you publish your report from Power BI Desktop tooPowerBI.com, it generates a **Report** and a **Dataset** in your PowerBI.com tenant.</span></span> <span data-ttu-id="be4d2-251">예를 들어 이라는 보고서 게시 후 **PowerBITutorial** tooPowerBI.com, PowerBITutorial에에서 나타나는 두 hello **보고서** 및 **데이터 집합** 섹션에서 PowerBI.com 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-251">For example, after you published a report called **PowerBITutorial** tooPowerBI.com, you will see PowerBITutorial in both hello **Reports** and **Datasets** sections on PowerBI.com.</span></span>

   ![새 보고서 및 PowerBI.com에서 데이터 집합의 스크린 샷 hello](./media/powerbi-visualize/powerbi-reports-datasets.png)

<span data-ttu-id="be4d2-253">toocreate 공유할 수 있는 대시보드 클릭 hello **라이브 고정 페이지** PowerBI.com 보고서에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-253">toocreate a sharable dashboard, click hello **Pin Live Page** button on your PowerBI.com report.</span></span>

   ![새 보고서 및 PowerBI.com에서 데이터 집합의 스크린 샷 hello](./media/powerbi-visualize/power-bi-pin-live-tile.png)

<span data-ttu-id="be4d2-255">hello 지침에 따라 [보고서에서 타일 고정](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate 새 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-255">Then follow hello instructions in [Pin a tile from a report](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate a new dashboard.</span></span> 

<span data-ttu-id="be4d2-256">또한 대시보드를 만들기 전에 tooreport 임시 수정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-256">You can also do ad hoc modifications tooreport before creating a dashboard.</span></span> <span data-ttu-id="be4d2-257">그러나 tooperform hello 수정 내용을 Power BI Desktop을 사용 하 고 hello 보고서 tooPowerBI.com 다시 게시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-257">However, it's recommended that you use Power BI Desktop tooperform hello modifications and republish hello report tooPowerBI.com.</span></span>

## <a name="refresh-data-in-powerbicom"></a><span data-ttu-id="be4d2-258">PowerBI.com에서 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="be4d2-258">Refresh data in PowerBI.com</span></span>
<span data-ttu-id="be4d2-259">두 가지 toorefresh 데이터, 임시 및 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-259">There are two ways toorefresh data, ad hoc and scheduled.</span></span>

<span data-ttu-id="be4d2-260">임시 새로 고침을 클릭 하세요 (...) hello eclipses hello 하 여 **Dataset**, 예: PowerBITutorial 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-260">For an ad hoc refresh, simply click on hello eclipses (…) by hello **Dataset**, e.g. PowerBITutorial.</span></span> <span data-ttu-id="be4d2-261">**지금 새로 고침**을 포함한 작업의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-261">You should see a list of actions including **Refresh Now**.</span></span> <span data-ttu-id="be4d2-262">클릭 **지금 새로 고침** toorefresh hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-262">Click **Refresh Now** toorefresh hello data.</span></span>

![PowerBI.com에서 지금 새로 고침의 스크린샷](./media/powerbi-visualize/power-bi-refresh-now.png)

<span data-ttu-id="be4d2-264">예약 된 새로 수행 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-264">For a scheduled refresh, do hello following.</span></span>

1. <span data-ttu-id="be4d2-265">클릭 **새로 고침 예약** hello 작업 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-265">Click **Schedule Refresh** in hello action list.</span></span> 

    ![PowerBI.com에서 새로 고침 예약 hello의 스크린샷](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. <span data-ttu-id="be4d2-267">Hello에 **설정** 페이지 **데이터 원본 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-267">In hello **Settings** page, expand **Data source credentials**.</span></span> 
3. <span data-ttu-id="be4d2-268">**자격 증명 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-268">Click on **Edit credentials**.</span></span> 
   
    <span data-ttu-id="be4d2-269">hello 구성 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-269">hello Configure popup appears.</span></span> 
4. <span data-ttu-id="be4d2-270">해당 데이터 집합에 대 한 hello 키 tooconnect toohello Cosmos DB 계정을 입력 한 다음 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-270">Enter hello key tooconnect toohello Cosmos DB account for that data set, then click **Sign in**.</span></span> 
5. <span data-ttu-id="be4d2-271">확장 **새로 고침 예약** toorefresh hello 데이터 집합을 원하는 hello 일정을 설정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-271">Expand **Schedule Refresh** and set up hello schedule you want toorefresh hello dataset.</span></span> 
6. <span data-ttu-id="be4d2-272">클릭 **적용** 있고 완료 된 hello 예약 된 새로 고침을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-272">Click **Apply** and you are done setting up hello scheduled refresh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be4d2-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be4d2-273">Next steps</span></span>
* <span data-ttu-id="be4d2-274">Power BI에 대해 자세히 toolearn 참조 [Power BI 시작](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-274">toolearn more about Power BI, see [Get started with Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).</span></span>
* <span data-ttu-id="be4d2-275">Cosmos DB에 대해 자세히 toolearn 참조 hello [Azure Cosmos DB 설명서 방문 페이지](https://azure.microsoft.com/documentation/services/documentdb/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be4d2-275">toolearn more about Cosmos DB, see hello [Azure Cosmos DB documentation landing page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

