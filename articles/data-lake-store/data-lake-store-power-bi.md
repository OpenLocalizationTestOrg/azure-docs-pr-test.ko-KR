---
title: "Power BI를 사용 하 여 데이터 레이크 저장소의 데이터를 aaaAnalyze | Microsoft Docs"
description: "Azure 데이터 레이크 저장소에 저장 된 Power BI tooanalyze 데이터를 사용 하 여"
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
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="b23e2-103">Power BI를 사용하여 Data Lake 저장소의 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="b23e2-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="b23e2-104">이 문서에 설명 합니다 방법을 toouse Power BI Desktop tooanalyze 및 Azure 데이터 레이크 저장소에 저장 된 데이터를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-104">In this article you will learn how toouse Power BI Desktop tooanalyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b23e2-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b23e2-105">Prerequisites</span></span>
<span data-ttu-id="b23e2-106">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-106">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="b23e2-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-107">**An Azure subscription**.</span></span> <span data-ttu-id="b23e2-108">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b23e2-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b23e2-109">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="b23e2-110">Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-110">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="b23e2-111">이 문서에서는 호출에 데이터 레이크 저장소 계정이 이미 만들었다고 가정 **mybidatalakestore**, 예제 데이터 파일을 업로드 (**Drivers.txt**) tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) tooit.</span></span> <span data-ttu-id="b23e2-112">이 샘플 파일은 [Azure Data Lake Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="b23e2-113">**Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="b23e2-113">**Power BI Desktop**.</span></span> <span data-ttu-id="b23e2-114">[Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=45331)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="b23e2-115">Power BI Desktop에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="b23e2-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="b23e2-116">컴퓨터에서 Power BI Desktop을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="b23e2-117">Hello에서 **홈** 리본에서 클릭 **데이터 가져오기**, 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-117">From hello **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="b23e2-118">Hello에 **데이터 가져오기** 대화 상자를 클릭 **Azure**, 클릭 **Azure 데이터 레이크 저장소**, 클릭 하 고 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-118">In hello **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="b23e2-119">![Connect tooData Lake 저장소](./media/data-lake-store-power-bi/get-data-lake-store-account.png "연결 tooData Lake 저장소")</span><span class="sxs-lookup"><span data-stu-id="b23e2-119">![Connect tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect tooData Lake Store")</span></span>
3. <span data-ttu-id="b23e2-120">개발 단계에 있는 것 hello 커넥터에 대 한 대화 상자를 표시 하는 경우 toocontinue 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-120">If you see a dialog box about hello connector being in a development phase, opt toocontinue.</span></span>
4. <span data-ttu-id="b23e2-121">Hello에 **Microsoft Azure 데이터 레이크 저장소** 대화 상자, hello URL tooyour Data Lake 저장소 계정에를 입력 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-121">In hello **Microsoft Azure Data Lake Store** dialog box, provide hello URL tooyour Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="b23e2-122">![Data Lake Store URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store URL")</span><span class="sxs-lookup"><span data-stu-id="b23e2-122">![URL for Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="b23e2-123">Hello 다음 대화 상자에서 클릭 **로그인** toosign Data Lake 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-123">In hello next dialog box, click **Sign in** toosign into Data Lake Store account.</span></span> <span data-ttu-id="b23e2-124">됩니다 tooyour 조직의 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-124">You will be redirected tooyour organization's sign in page.</span></span> <span data-ttu-id="b23e2-125">Hello 프롬프트 toosign hello 계정으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-125">Follow hello prompts toosign into hello account.</span></span>
   
    <span data-ttu-id="b23e2-126">![Data Lake Store에 로그인](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Data Lake Store에 로그인")</span><span class="sxs-lookup"><span data-stu-id="b23e2-126">![Sign into Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="b23e2-127">성공적으로 로그인한 후에 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="b23e2-128">![Connect tooData Lake 저장소](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "연결 tooData Lake 저장소")</span><span class="sxs-lookup"><span data-stu-id="b23e2-128">![Connect tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect tooData Lake Store")</span></span>
7. <span data-ttu-id="b23e2-129">다음 대화 상자 hello tooyour 데이터 레이크 저장소 계정에 업로드할 hello 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-129">hello next dialog box shows hello file that you uploaded tooyour Data Lake Store account.</span></span> <span data-ttu-id="b23e2-130">Hello 정보를 확인 한 다음 클릭 **부하**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-130">Verify hello info and then click **Load**.</span></span>
   
    <span data-ttu-id="b23e2-131">![Data Lake Store에서 데이터 로드](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Data Lake Store에서 데이터 로드")</span><span class="sxs-lookup"><span data-stu-id="b23e2-131">![Load data from Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="b23e2-132">Hello 데이터가 Power BI에 성공적으로 로드 된 hello의 필드를 다음 hello 나타납니다 **필드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-132">After hello data has been successfully loaded into Power BI, you will see hello following fields in hello **Fields** tab.</span></span>
   
    <span data-ttu-id="b23e2-133">![가져온 필드](./media/data-lake-store-power-bi/imported-fields.png "가져온 필드")</span><span class="sxs-lookup"><span data-stu-id="b23e2-133">![Imported fields](./media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="b23e2-134">그러나 toovisualize hello 데이터를 분석 하 고, hello 데이터 toobe 필드 뒤 hello 당 사용 가능한 것이 좋습니다</span><span class="sxs-lookup"><span data-stu-id="b23e2-134">However, toovisualize and analyze hello data, we prefer hello data toobe available per hello following fields</span></span>
   
    <span data-ttu-id="b23e2-135">![원하는 필드](./media/data-lake-store-power-bi/desired-fields.png "원하는 필드")</span><span class="sxs-lookup"><span data-stu-id="b23e2-135">![Desired fields](./media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="b23e2-136">Hello 다음 단계에서 hello 쿼리 tooconvert hello 가져온 데이터를 원하는 형식 hello 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-136">In hello next steps, we will update hello query tooconvert hello imported data in hello desired format.</span></span>
9. <span data-ttu-id="b23e2-137">Hello에서 **홈** 리본에서 클릭 **쿼리 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-137">From hello **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="b23e2-138">![쿼리 편집](./media/data-lake-store-power-bi/edit-queries.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="b23e2-138">![Edit queries](./media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="b23e2-139">Hello에서 hello 쿼리 편집기에서에서 **콘텐츠** 열을 클릭 하 여 **이진**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-139">In hello Query Editor, under hello **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="b23e2-140">![쿼리 편집](./media/data-lake-store-power-bi/convert-query1.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="b23e2-140">![Edit queries](./media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="b23e2-141">Hello를 나타내는 파일 아이콘을 나타납니다 **Drivers.txt** 업로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-141">You will see a file icon, that represents hello **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="b23e2-142">Hello 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 **CSV**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-142">Right-click hello file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="b23e2-143">![쿼리 편집](./media/data-lake-store-power-bi/convert-query2.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="b23e2-143">![Edit queries](./media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="b23e2-144">아래와 같이 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-144">You should see an output as shown below.</span></span> <span data-ttu-id="b23e2-145">데이터는 toocreate 시각화를 사용할 수 있는 형식으로 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-145">Your data is now available in a format that you can use toocreate visualizations.</span></span>
    
    <span data-ttu-id="b23e2-146">![쿼리 편집](./media/data-lake-store-power-bi/convert-query3.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="b23e2-146">![Edit queries](./media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="b23e2-147">Hello에서 **홈** 리본에서 클릭 **닫고 적용**, 클릭 하 고 **닫고 적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-147">From hello **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="b23e2-148">![쿼리 편집](./media/data-lake-store-power-bi/load-edited-query.png "쿼리 편집")</span><span class="sxs-lookup"><span data-stu-id="b23e2-148">![Edit queries](./media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="b23e2-149">Hello 쿼리를 업데이트 후 hello **필드** 탭 hello 시각화에 사용할 수 있는 새 필드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-149">Once hello query is updated, hello **Fields** tab will show hello new fields available for visualization.</span></span>
    
    <span data-ttu-id="b23e2-150">![업데이트된 필드](./media/data-lake-store-power-bi/updated-query-fields.png "업데이트된 필드")</span><span class="sxs-lookup"><span data-stu-id="b23e2-150">![Updated fields](./media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="b23e2-151">주세요 특정된 국가 대 한 각 도시에 원형 차트 toorepresent hello 드라이버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-151">Let us create a pie chart toorepresent hello drivers in each city for a given country.</span></span> <span data-ttu-id="b23e2-152">따라서 toodo 다음 항목을 선택 하는 hello를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-152">toodo so, make hello following selections.</span></span>
    
    1. <span data-ttu-id="b23e2-153">Hello 시각화 탭에서 원형 차트에 대 한 hello 기호를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-153">From hello Visualizations tab, click hello symbol for a pie chart.</span></span>
       
        <span data-ttu-id="b23e2-154">![원형 차트 만들기](./media/data-lake-store-power-bi/create-pie-chart.png "원형 차트 만들기")</span><span class="sxs-lookup"><span data-stu-id="b23e2-154">![Create pie chart](./media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="b23e2-155">toouse는 하겠습니다 hello 열 **열 4** (hello 도시 이름) 및 **열 7** (hello 국가 이름).</span><span class="sxs-lookup"><span data-stu-id="b23e2-155">hello columns that we are going toouse are **Column 4** (name of hello city) and **Column 7** (name of hello country).</span></span> <span data-ttu-id="b23e2-156">이러한 열을 끌어 **필드** 너무 탭**시각화** 아래와 같이 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-156">Drag these columns from **Fields** tab too**Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="b23e2-157">![시각화 만들기](./media/data-lake-store-power-bi/create-visualizations.png "시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="b23e2-157">![Create visualizations](./media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="b23e2-158">hello 아래와 같은 hello 원형 차트 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-158">hello pie chart should now resemble like hello one shown below.</span></span>
       
        <span data-ttu-id="b23e2-159">![원형 차트](./media/data-lake-store-power-bi/pie-chart.png "시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="b23e2-159">![Pie chart](./media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="b23e2-160">Hello 페이지 수준 필터에서 특정 국가 선택 하면 선택한 hello 국가의 각 도시에 있는 드라이버 hello 수 이제 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-160">By selecting a specific country from hello page level filters, you can now see hello number of drivers in each city of hello selected country.</span></span> <span data-ttu-id="b23e2-161">예를 들어 hello에서 **시각화** 탭의 **페이지 수준 필터**선택, **브라질**합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-161">For example, under hello **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="b23e2-162">![국가 선택](./media/data-lake-store-power-bi/select-country.png "국가 선택")</span><span class="sxs-lookup"><span data-stu-id="b23e2-162">![Select a country](./media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="b23e2-163">hello 원형 차트는 브라질의 hello 도시에 자동으로 업데이트 된 toodisplay hello 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-163">hello pie chart is automatically updated toodisplay hello drivers in hello cities of Brazil.</span></span>
    
    <span data-ttu-id="b23e2-164">![국가의 드라이버](./media/data-lake-store-power-bi/driver-per-country.png "국가별 드라이버")</span><span class="sxs-lookup"><span data-stu-id="b23e2-164">![Drivers in a country](./media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="b23e2-165">Hello에서 **파일** 메뉴를 클릭 하 여 **저장** toosave hello 시각화를 Power BI Desktop 파일로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-165">From hello **File** menu, click **Save** toosave hello visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-toopower-bi-service"></a><span data-ttu-id="b23e2-166">보고서 tooPower BI 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-166">Publish report tooPower BI service</span></span>
<span data-ttu-id="b23e2-167">Power BI Desktop에서 hello 시각화를 만든 후 toohello Power BI 서비스를 게시 하 여 다른 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-167">Once you have created hello visualizations in Power BI Desktop, you can share it with others by publishing it toohello Power BI service.</span></span> <span data-ttu-id="b23e2-168">방법에 대 한 참조는 toodo [Power BI Desktop에서 게시](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b23e2-168">For instructions on how toodo that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="b23e2-169">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b23e2-169">See also</span></span>
* [<span data-ttu-id="b23e2-170">Data Lake 분석을 사용하여 Data Lake 저장소의 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="b23e2-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

