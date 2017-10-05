---
title: "Azure Data Catalog에 Data Lake Store의 데이터 등록 | Microsoft 문서"
description: "Azure Data Catalog에 Data Lake 저장소의 데이터 등록"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 41f7ca0d638479b013e77cb949a71c566bc66aa4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a><span data-ttu-id="c7626-103">Azure Data Catalog에 Data Lake 저장소의 데이터 등록</span><span class="sxs-lookup"><span data-stu-id="c7626-103">Register data from Data Lake Store in Azure Data Catalog</span></span>
<span data-ttu-id="c7626-104">이 문서에서는 데이터 카탈로그와 데이터를 통합하여 조직 내에서 데이터를 검색할 수 있도록 만들기 위해 Azure Data Lake 저장소와 Azure Data Catalog를 통합하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-104">In this article you will learn how to integrate Azure Data Lake Store with Azure Data Catalog to make your data discoverable within an organization by integrating it with Data Catalog.</span></span> <span data-ttu-id="c7626-105">데이터 카탈로그를 만드는 방법에 대한 자세한 내용은 [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7626-105">For more information on cataloging data, see [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md).</span></span> <span data-ttu-id="c7626-106">데이터 카탈로그를 사용할 수 있는 시나리오를 이해하려면 [Azure Data Catalog 일반적인 시나리오](../data-catalog/data-catalog-common-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7626-106">To understand scenarios in which you can use Data Catalog, see [Azure Data Catalog common scenarios](../data-catalog/data-catalog-common-scenarios.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7626-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c7626-107">Prerequisites</span></span>
<span data-ttu-id="c7626-108">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-108">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="c7626-109">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="c7626-109">**An Azure subscription**.</span></span> <span data-ttu-id="c7626-110">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7626-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c7626-111">**Azure 구독을 사용하도록 설정합니다** .</span><span class="sxs-lookup"><span data-stu-id="c7626-111">**Enable your Azure subscription** for Data Lake Store Public Preview.</span></span> <span data-ttu-id="c7626-112">[지침](data-lake-store-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7626-112">See [instructions](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="c7626-113">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="c7626-113">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="c7626-114">[Azure Portal을 사용하여 Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)에 있는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-114">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="c7626-115">이 자습서에서는 **datacatalogstore**라는 Data Lake Store 계정을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-115">For this tutorial, let us create a Data Lake Store account called **datacatalogstore**.</span></span>

    <span data-ttu-id="c7626-116">계정을 만든 후에 그 계정에 샘플 데이터 집합을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-116">Once you have created the account, upload a sample data set to it.</span></span> <span data-ttu-id="c7626-117">이 자습서에서는, **Azure Data Lake Git 리포지토리** 의 [AmbulanceData](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/)폴더에 있는 모든 .csv 파일을 업로드하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-117">For this tutorial, let us upload all the .csv files under the **AmbulanceData** folder in the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/).</span></span> <span data-ttu-id="c7626-118">[Azure 저장소 탐색기](http://storageexplorer.com/)와 같은 다양한 클라이언트를 사용하여 Blob 컨테이너에 데이터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-118">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>
* <span data-ttu-id="c7626-119">**Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="c7626-119">**Azure Data Catalog**.</span></span> <span data-ttu-id="c7626-120">조직용 Azure Data Catalog가 이미 생성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-120">Your organization must already have an Azure Data Catalog created for your organization.</span></span> <span data-ttu-id="c7626-121">각 조직에는 카탈로그가 하나만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-121">Only one catalog is allowed for each organization.</span></span>

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a><span data-ttu-id="c7626-122">Data Lake 저장소를 데이터 카탈로그에 대한 원본으로 등록</span><span class="sxs-lookup"><span data-stu-id="c7626-122">Register Data Lake Store as a source for Data Catalog</span></span>

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. <span data-ttu-id="c7626-123">`https://azure.microsoft.com/services/data-catalog`로 이동하여 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-123">Go to `https://azure.microsoft.com/services/data-catalog`, and click **Get started**.</span></span>
2. <span data-ttu-id="c7626-124">Azure Data Catalog 포털에 로그인하고 **데이터 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-124">Log into the Azure Data Catalog portal, and click **Publish data**.</span></span>

    <span data-ttu-id="c7626-125">![데이터 원본 등록](./media/data-lake-store-with-data-catalog/register-data-source.png "데이터 원본 등록")</span><span class="sxs-lookup"><span data-stu-id="c7626-125">![Register a data source](./media/data-lake-store-with-data-catalog/register-data-source.png "Register a data source")</span></span>
3. <span data-ttu-id="c7626-126">다음 페이지에서 **응용 프로그램 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-126">On the next page, click **Launch Application**.</span></span> <span data-ttu-id="c7626-127">컴퓨터에 응용 프로그램 매니페스트 파일이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-127">This will download the application manifest file on your computer.</span></span> <span data-ttu-id="c7626-128">매니페스트 파일을 두 번 클릭하여 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-128">Double-click the manifest file to start the application.</span></span>
4. <span data-ttu-id="c7626-129">시작 페이지에서 **로그인**을 클릭하고 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-129">On the Welcome page, click **Sign in**, and enter your credentials.</span></span>

    <span data-ttu-id="c7626-130">![시작 화면](./media/data-lake-store-with-data-catalog/welcome.screen.png "시작 화면")</span><span class="sxs-lookup"><span data-stu-id="c7626-130">![Welcome screen](./media/data-lake-store-with-data-catalog/welcome.screen.png "Welcome screen")</span></span>
5. <span data-ttu-id="c7626-131">데이터 원본 선택 페이지에서 **Azure Data Lake**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-131">On the Select a Data Source page, select **Azure Data Lake**, and then click **Next**.</span></span>

    <span data-ttu-id="c7626-132">![데이터 원본 선택](./media/data-lake-store-with-data-catalog/select-source.png "데이터 원본 선택")</span><span class="sxs-lookup"><span data-stu-id="c7626-132">![Select data source](./media/data-lake-store-with-data-catalog/select-source.png "Select data source")</span></span>
6. <span data-ttu-id="c7626-133">다음 페이지에서, 데이터 카탈로그에 등록할 Data Lake 저장소 계정 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-133">On the next page, provide the Data Lake Store account name that you want to register in Data Catalog.</span></span> <span data-ttu-id="c7626-134">다른 옵션은 기본값으로 두고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-134">Leave the other options as default and then click **Connect**.</span></span>

    <span data-ttu-id="c7626-135">![데이터 원본에 연결](./media/data-lake-store-with-data-catalog/connect-to-source.png "데이터 원본에 연결")</span><span class="sxs-lookup"><span data-stu-id="c7626-135">![Connect to data source](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connect to data source")</span></span>
7. <span data-ttu-id="c7626-136">다음 페이지는 다음과 같은 세그먼트로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-136">The next page can be divided into the following segments.</span></span>

    <span data-ttu-id="c7626-137">a.</span><span class="sxs-lookup"><span data-stu-id="c7626-137">a.</span></span> <span data-ttu-id="c7626-138">**서버 계층 구조** 상자는 Data Lake 저장소 계정 폴더 구조를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-138">The **Server Hierarchy** box represents the Data Lake Store account folder structure.</span></span> <span data-ttu-id="c7626-139">**$Root**는 Data Lake Store 계정 루트를, **AmbulanceData**는 Data Lake Store 계정의 루트에 생성된 폴더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-139">**$Root** represents the Data Lake Store account root, and **AmbulanceData** represents the folder created in the root of the Data Lake Store account.</span></span>

    <span data-ttu-id="c7626-140">b.</span><span class="sxs-lookup"><span data-stu-id="c7626-140">b.</span></span> <span data-ttu-id="c7626-141">**사용 가능한 개체** 상자에 **AmbulanceData** 폴더의 하위 파일과 폴더가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-141">The **Available objects** box lists the files and folders under the **AmbulanceData** folder.</span></span>

    <span data-ttu-id="c7626-142">c.</span><span class="sxs-lookup"><span data-stu-id="c7626-142">c.</span></span> <span data-ttu-id="c7626-143">**등록할 개체** 상자에는 Azure Data Catalog에 등록할 파일과 폴더가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-143">**Objects to be registered box** lists the files and folders that you want to register in Azure Data Catalog.</span></span>

    <span data-ttu-id="c7626-144">![데이터 구조 보기](./media/data-lake-store-with-data-catalog/view-data-structure.png "데이터 구조 보기")</span><span class="sxs-lookup"><span data-stu-id="c7626-144">![View data structure](./media/data-lake-store-with-data-catalog/view-data-structure.png "View data structure")</span></span>
8. <span data-ttu-id="c7626-145">이 자습서에서는, 디렉터리의 모든 파일을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-145">For this tutorial, you should register all the files in the directory.</span></span> <span data-ttu-id="c7626-146">이를 위해, (![개체 이동](./media/data-lake-store-with-data-catalog/move-objects.png "개체 이동")) 단추를 클릭하여 모든 파일을 **등록할 개체** 상자로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-146">For that, click the (![move objects](./media/data-lake-store-with-data-catalog/move-objects.png "Move objects")) button to move all the files to **Objects to be registered** box.</span></span>

    <span data-ttu-id="c7626-147">데이터를 조직 전체의 데이터 카탈로그에 등록하는 것이므로, 나중에 데이터를 신속하게 찾는 데 사용할 수 있는 메타데이터를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-147">Because the data will be registered in an organization-wide data catalog, it is a recommened approach to add some metadata which you can later use to quickly locate the data.</span></span> <span data-ttu-id="c7626-148">예를 들어, 데이터 소유자(예: 데이터를 업로드한 사람)의 전자 메일 주소를 추가하거나 데이터 식별을 위한 태그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-148">For example, you can add an e-mail address for the data owner (for example, one who is uploading the data) or add a tag to identify the data.</span></span> <span data-ttu-id="c7626-149">아래 스크린 캡처에서 데이터에 추가하는 태그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-149">The screen capture below shows a tag that we add to the data.</span></span>

    <span data-ttu-id="c7626-150">![데이터 구조 보기](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "데이터 구조 보기")</span><span class="sxs-lookup"><span data-stu-id="c7626-150">![View data structure](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "View data structure")</span></span>

    <span data-ttu-id="c7626-151">**Register**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-151">Click **Register**.</span></span>
9. <span data-ttu-id="c7626-152">다음 화면 캡처는 데이터가 데이터 카탈로그에 성공적으로 등록된 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-152">The following screen capture denotes that the data is successfully registered in the Data Catalog.</span></span>

    <span data-ttu-id="c7626-153">![등록 완료](./media/data-lake-store-with-data-catalog/registration-complete.png "데이터 구조 보기")</span><span class="sxs-lookup"><span data-stu-id="c7626-153">![Registration complete](./media/data-lake-store-with-data-catalog/registration-complete.png "View data structure")</span></span>
10. <span data-ttu-id="c7626-154">**포털 보기** 를 클릭하고 데이터 카탈로그로 돌아가서, 이제 포털에서 등록된 데이터를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-154">Click **View Portal** to go back to the Data Catalog portal and verify that you can now access the registered data from the portal.</span></span> <span data-ttu-id="c7626-155">데이터 검색을 위해, 데이터를 등록할 때 사용한 태그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-155">To search the data, you can use the tag you used while registering the data.</span></span>

     <span data-ttu-id="c7626-156">![카탈로그에서 데이터 검색](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "카탈로그에서 데이터 검색")</span><span class="sxs-lookup"><span data-stu-id="c7626-156">![Search data in catalog](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Search data in catalog")</span></span>
11. <span data-ttu-id="c7626-157">이제 데이터에 주석 및 설명서를 추가하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7626-157">You can now perform operations like adding annotations and documentation to the data.</span></span> <span data-ttu-id="c7626-158">자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7626-158">For more information, see the following links.</span></span>

    * [<span data-ttu-id="c7626-159">데이터 카탈로그에서 데이터 원본에 주석 추가</span><span class="sxs-lookup"><span data-stu-id="c7626-159">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
    * [<span data-ttu-id="c7626-160">데이터 카탈로그에서 데이터 원본 문서화</span><span class="sxs-lookup"><span data-stu-id="c7626-160">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a><span data-ttu-id="c7626-161">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c7626-161">See also</span></span>
* [<span data-ttu-id="c7626-162">데이터 카탈로그에서 데이터 원본에 주석 추가</span><span class="sxs-lookup"><span data-stu-id="c7626-162">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
* [<span data-ttu-id="c7626-163">데이터 카탈로그에서 데이터 원본 문서화</span><span class="sxs-lookup"><span data-stu-id="c7626-163">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)
* [<span data-ttu-id="c7626-164">Data Lake 저장소를 다른 Azure 서비스와 통합</span><span class="sxs-lookup"><span data-stu-id="c7626-164">Integrate Data Lake Store with other Azure services</span></span>](data-lake-store-integrate-with-other-services.md)
