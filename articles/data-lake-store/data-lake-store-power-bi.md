---
title: "Power BI를 사용하여 Data Lake Store 데이터 분석 | Microsoft 문서"
description: "Power BI를 사용하여 Azure Data Lake 저장소에 저장된 데이터 분석"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0cf7e385ef2edd650479e120f52469bc6632f2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="9a4c7-103">Power BI를 사용하여 Data Lake 저장소의 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="9a4c7-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="9a4c7-104">이 문서에서는 Power BI Desktop을 사용하여 Azure Data Lake 저장소에 저장된 데이터를 분석하고 시각화하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-104">In this article you will learn how to use Power BI Desktop to analyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a4c7-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a4c7-105">Prerequisites</span></span>
<span data-ttu-id="9a4c7-106">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-106">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="9a4c7-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-107">**An Azure subscription**.</span></span> <span data-ttu-id="9a4c7-108">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9a4c7-109">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="9a4c7-110">[Azure Portal을 사용하여 Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)에 있는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="9a4c7-111">이 문서에서는 이미 **mybidatalakestore**라는 Data Lake Store 계정을 만들어 샘플 데이터 파일(**Drivers.txt**)을 업로드했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) to it.</span></span> <span data-ttu-id="9a4c7-112">이 샘플 파일은 [Azure Data Lake Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="9a4c7-113">**Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-113">**Power BI Desktop**.</span></span> <span data-ttu-id="9a4c7-114">[Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=45331)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="9a4c7-115">Power BI Desktop에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="9a4c7-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="9a4c7-116">컴퓨터에서 Power BI Desktop을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="9a4c7-117">**홈** 리본 메뉴에서 **데이터 가져오기**, [자세히]를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-117">From the **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="9a4c7-118">**데이터 가져오기** 대화 상자에서 **Azure**, **Azure Data Lake Store**, **연결**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-118">In the **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="9a4c7-119">![Data Lake Store에 연결](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Data Lake Store에 연결")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-119">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect to Data Lake Store")</span></span>
3. <span data-ttu-id="9a4c7-120">커넥터가 개발 단계에 있다는 대화 상자가 표시되면, 계속 진행하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-120">If you see a dialog box about the connector being in a development phase, opt to continue.</span></span>
4. <span data-ttu-id="9a4c7-121">**Microsoft Azure Data Lake Store** 대화 상자에서 Data Lake Store 계정에 대한 URL을 제공한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-121">In the **Microsoft Azure Data Lake Store** dialog box, provide the URL to your Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="9a4c7-122">![Data Lake Store URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store URL")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-122">![URL for Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="9a4c7-123">다음 대화 상자에서 **로그인** 을 클릭하여 Data Lake 저장소 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-123">In the next dialog box, click **Sign in** to sign into Data Lake Store account.</span></span> <span data-ttu-id="9a4c7-124">사용자가 속한 조직의 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-124">You will be redirected to your organization's sign in page.</span></span> <span data-ttu-id="9a4c7-125">프롬프트에 따라 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-125">Follow the prompts to sign into the account.</span></span>
   
    <span data-ttu-id="9a4c7-126">![Data Lake Store에 로그인](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Data Lake Store에 로그인")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-126">![Sign into Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="9a4c7-127">성공적으로 로그인한 후에 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="9a4c7-128">![Data Lake Store에 연결](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Data Lake Store에 연결")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-128">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect to Data Lake Store")</span></span>
7. <span data-ttu-id="9a4c7-129">다음 대화 상자에서 Data Lake 저장소 계정에 업로드한 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-129">The next dialog box shows the file that you uploaded to your Data Lake Store account.</span></span> <span data-ttu-id="9a4c7-130">정보를 확인한 다음 **로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-130">Verify the info and then click **Load**.</span></span>
   
    <span data-ttu-id="9a4c7-131">![Data Lake Store에서 데이터 로드](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Data Lake Store에서 데이터 로드")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-131">![Load data from Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="9a4c7-132">데이터가 Power BI에 성공적으로 로드된 후에, **필드** 탭에 다음 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-132">After the data has been successfully loaded into Power BI, you will see the following fields in the **Fields** tab.</span></span>
   
    <span data-ttu-id="9a4c7-133">![가져온 필드](./media/data-lake-store-power-bi/imported-fields.png "가져온 필드")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-133">![Imported fields](./media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="9a4c7-134">하지만, 데이터를 시각화하고 분석하려면, 다음과 같은 필드에 따라 데이터가 제공되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-134">However, to visualize and analyze the data, we prefer the data to be available per the following fields</span></span>
   
    <span data-ttu-id="9a4c7-135">![원하는 필드](./media/data-lake-store-power-bi/desired-fields.png "원하는 필드")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-135">![Desired fields](./media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="9a4c7-136">다음 단계에서는 가져온 데이터를 원하는 형식으로 변환하기 위해 쿼리를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-136">In the next steps, we will update the query to convert the imported data in the desired format.</span></span>
9. <span data-ttu-id="9a4c7-137">**홈** 리본 메뉴에서 **쿼리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-137">From the **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="9a4c7-138">![쿼리 편집](./media/data-lake-store-power-bi/edit-queries.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-138">![Edit queries](./media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="9a4c7-139">[쿼리 편집기]에서 **콘텐츠** 열 아래쪽의 **이진**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-139">In the Query Editor, under the **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="9a4c7-140">![쿼리 편집](./media/data-lake-store-power-bi/convert-query1.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-140">![Edit queries](./media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="9a4c7-141">업로드해 놓은 **Drivers.txt** 파일을 나타내는 파일 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-141">You will see a file icon, that represents the **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="9a4c7-142">파일을 마우스 오른쪽 단추로 클릭하고 **CSV**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-142">Right-click the file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="9a4c7-143">![쿼리 편집](./media/data-lake-store-power-bi/convert-query2.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-143">![Edit queries](./media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="9a4c7-144">아래와 같이 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-144">You should see an output as shown below.</span></span> <span data-ttu-id="9a4c7-145">이제 시각화를 만드는 데 사용할 수 있는 형식으로 데이터가 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-145">Your data is now available in a format that you can use to create visualizations.</span></span>
    
    <span data-ttu-id="9a4c7-146">![쿼리 편집](./media/data-lake-store-power-bi/convert-query3.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-146">![Edit queries](./media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="9a4c7-147">**홈** 리본 메뉴에서 **닫기 및 적용**을 클릭한 다음 **닫기 및 적용**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-147">From the **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="9a4c7-148">![쿼리 편집](./media/data-lake-store-power-bi/load-edited-query.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-148">![Edit queries](./media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="9a4c7-149">쿼리가 업데이트되면, 시각화에 사용할 수 있는 새로운 필드가 **Fields** (필드) 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-149">Once the query is updated, the **Fields** tab will show the new fields available for visualization.</span></span>
    
    <span data-ttu-id="9a4c7-150">![업데이트된 필드](./media/data-lake-store-power-bi/updated-query-fields.png "업데이트된 필드")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-150">![Updated fields](./media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="9a4c7-151">특정 국가에 대한 각 도시의 드라이버를 나타내는 원형 차트를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-151">Let us create a pie chart to represent the drivers in each city for a given country.</span></span> <span data-ttu-id="9a4c7-152">이렇게 하려면, 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-152">To do so, make the following selections.</span></span>
    
    1. <span data-ttu-id="9a4c7-153">Visualizations(시각화) 탭에서 원형 차트 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-153">From the Visualizations tab, click the symbol for a pie chart.</span></span>
       
        <span data-ttu-id="9a4c7-154">![원형 차트 만들기](./media/data-lake-store-power-bi/create-pie-chart.png "원형 차트 만들기")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-154">![Create pie chart](./media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="9a4c7-155">사용할 열은 **열 4**(도시 이름) 및 **열 7**(국가 이름)입니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-155">The columns that we are going to use are **Column 4** (name of the city) and **Column 7** (name of the country).</span></span> <span data-ttu-id="9a4c7-156">아래와 같이 열을 **필드** 탭에서 **시각화** 탭으로 끌어갑니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-156">Drag these columns from **Fields** tab to **Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="9a4c7-157">![시각화 만들기](./media/data-lake-store-power-bi/create-visualizations.png "시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-157">![Create visualizations](./media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="9a4c7-158">이제 원형 차트가 아래와 비슷하게 표시되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-158">The pie chart should now resemble like the one shown below.</span></span>
       
        <span data-ttu-id="9a4c7-159">![원형 차트](./media/data-lake-store-power-bi/pie-chart.png "시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-159">![Pie chart](./media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="9a4c7-160">페이지 수준 필터에서 특정 국가를 선택하면, 선택한 국가의 각 도시 내 드라이버의 수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-160">By selecting a specific country from the page level filters, you can now see the number of drivers in each city of the selected country.</span></span> <span data-ttu-id="9a4c7-161">예를 들어 **시각화** 탭의 **페이지 수준 필터**에서 **브라질**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-161">For example, under the **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="9a4c7-162">![국가 선택](./media/data-lake-store-power-bi/select-country.png "국가 선택")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-162">![Select a country](./media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="9a4c7-163">원형 차트가 브라질의 도시 내 드라이버를 나타내도록 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-163">The pie chart is automatically updated to display the drivers in the cities of Brazil.</span></span>
    
    <span data-ttu-id="9a4c7-164">![국가의 드라이버](./media/data-lake-store-power-bi/driver-per-country.png "국가별 드라이버")</span><span class="sxs-lookup"><span data-stu-id="9a4c7-164">![Drivers in a country](./media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="9a4c7-165">**파일** 메뉴에서 **저장**을 클릭하여 시각화를 Power BI Desktop 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-165">From the **File** menu, click **Save** to save the visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-to-power-bi-service"></a><span data-ttu-id="9a4c7-166">Power BI 서비스에 보고서 게시</span><span class="sxs-lookup"><span data-stu-id="9a4c7-166">Publish report to Power BI service</span></span>
<span data-ttu-id="9a4c7-167">Power BI Desktop에서 시각화를 만들고 나면, Power BI 서비스에 게시하여 다른 사람들과 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-167">Once you have created the visualizations in Power BI Desktop, you can share it with others by publishing it to the Power BI service.</span></span> <span data-ttu-id="9a4c7-168">수행하는 방법에 대한 지침은 [Power BI Desktop에서 게시](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4c7-168">For instructions on how to do that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="9a4c7-169">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9a4c7-169">See also</span></span>
* [<span data-ttu-id="9a4c7-170">Data Lake 분석을 사용하여 Data Lake 저장소의 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="9a4c7-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

