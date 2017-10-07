---
title: "Azure Data Catalog에서 데이터 레이크 저장소에서 데이터 aaaRegister | Microsoft Docs"
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
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a><span data-ttu-id="b561d-103">Azure Data Catalog에 Data Lake 저장소의 데이터 등록</span><span class="sxs-lookup"><span data-stu-id="b561d-103">Register data from Data Lake Store in Azure Data Catalog</span></span>
<span data-ttu-id="b561d-104">이 문서에서 어떻게 toointegrate Azure 데이터 레이크 데이터를 저장할 Azure Data Catalog toomake와 조직 내에서 검색 가능한 데이터 카탈로그와 통합 하 여 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-104">In this article you will learn how toointegrate Azure Data Lake Store with Azure Data Catalog toomake your data discoverable within an organization by integrating it with Data Catalog.</span></span> <span data-ttu-id="b561d-105">데이터 카탈로그를 만드는 방법에 대한 자세한 내용은 [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b561d-105">For more information on cataloging data, see [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md).</span></span> <span data-ttu-id="b561d-106">데이터 카탈로그를 사용할 수 있는 toounderstand 시나리오 참조 [일반적인 시나리오는 Azure Data Catalog](../data-catalog/data-catalog-common-scenarios.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-106">toounderstand scenarios in which you can use Data Catalog, see [Azure Data Catalog common scenarios](../data-catalog/data-catalog-common-scenarios.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b561d-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b561d-107">Prerequisites</span></span>
<span data-ttu-id="b561d-108">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-108">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="b561d-109">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b561d-109">**An Azure subscription**.</span></span> <span data-ttu-id="b561d-110">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b561d-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b561d-111">**Azure 구독을 사용하도록 설정합니다** .</span><span class="sxs-lookup"><span data-stu-id="b561d-111">**Enable your Azure subscription** for Data Lake Store Public Preview.</span></span> <span data-ttu-id="b561d-112">[지침](data-lake-store-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b561d-112">See [instructions](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="b561d-113">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="b561d-113">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="b561d-114">Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-114">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="b561d-115">이 자습서에서는 **datacatalogstore**라는 Data Lake Store 계정을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-115">For this tutorial, let us create a Data Lake Store account called **datacatalogstore**.</span></span>

    <span data-ttu-id="b561d-116">Hello 계정을 만든 후에 샘플 데이터 집합 tooit을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-116">Once you have created hello account, upload a sample data set tooit.</span></span> <span data-ttu-id="b561d-117">이 자습서에 대 한 hello에서 모든 hello.csv 파일을 업로드 주세요 **AmbulanceData** 폴더 hello에 [Azure 데이터 레이크 Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-117">For this tutorial, let us upload all hello .csv files under hello **AmbulanceData** folder in hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/).</span></span> <span data-ttu-id="b561d-118">와 같은 다양 한 클라이언트를 사용할 수 [Azure 저장소 탐색기](http://storageexplorer.com/), tooupload 데이터 tooa blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-118">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>
* <span data-ttu-id="b561d-119">**Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="b561d-119">**Azure Data Catalog**.</span></span> <span data-ttu-id="b561d-120">조직용 Azure Data Catalog가 이미 생성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-120">Your organization must already have an Azure Data Catalog created for your organization.</span></span> <span data-ttu-id="b561d-121">각 조직에는 카탈로그가 하나만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-121">Only one catalog is allowed for each organization.</span></span>

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a><span data-ttu-id="b561d-122">Data Lake 저장소를 데이터 카탈로그에 대한 원본으로 등록</span><span class="sxs-lookup"><span data-stu-id="b561d-122">Register Data Lake Store as a source for Data Catalog</span></span>

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. <span data-ttu-id="b561d-123">너무 이동`https://azure.microsoft.com/services/data-catalog`를 클릭 하 고 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-123">Go too`https://azure.microsoft.com/services/data-catalog`, and click **Get started**.</span></span>
2. <span data-ttu-id="b561d-124">Hello Azure Data Catalog 포털에 로그인 하 고 클릭 **데이터 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-124">Log into hello Azure Data Catalog portal, and click **Publish data**.</span></span>

    <span data-ttu-id="b561d-125">![데이터 원본 등록](./media/data-lake-store-with-data-catalog/register-data-source.png "데이터 원본 등록")</span><span class="sxs-lookup"><span data-stu-id="b561d-125">![Register a data source](./media/data-lake-store-with-data-catalog/register-data-source.png "Register a data source")</span></span>
3. <span data-ttu-id="b561d-126">Hello 다음 페이지에서 클릭 **응용 프로그램 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-126">On hello next page, click **Launch Application**.</span></span> <span data-ttu-id="b561d-127">Hello 응용 프로그램 매니페스트 파일을 컴퓨터에 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-127">This will download hello application manifest file on your computer.</span></span> <span data-ttu-id="b561d-128">Hello 매니페스트 파일 toostart hello 응용 프로그램을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-128">Double-click hello manifest file toostart hello application.</span></span>
4. <span data-ttu-id="b561d-129">Hello 시작 페이지에서 클릭 **로그인**, 자격 증명을 입력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-129">On hello Welcome page, click **Sign in**, and enter your credentials.</span></span>

    <span data-ttu-id="b561d-130">![시작 화면](./media/data-lake-store-with-data-catalog/welcome.screen.png "시작 화면")</span><span class="sxs-lookup"><span data-stu-id="b561d-130">![Welcome screen](./media/data-lake-store-with-data-catalog/welcome.screen.png "Welcome screen")</span></span>
5. <span data-ttu-id="b561d-131">Hello 데이터 원본 선택 페이지에서 선택 **Azure 데이터 레이크**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-131">On hello Select a Data Source page, select **Azure Data Lake**, and then click **Next**.</span></span>

    <span data-ttu-id="b561d-132">![데이터 원본 선택](./media/data-lake-store-with-data-catalog/select-source.png "데이터 원본 선택")</span><span class="sxs-lookup"><span data-stu-id="b561d-132">![Select data source](./media/data-lake-store-with-data-catalog/select-source.png "Select data source")</span></span>
6. <span data-ttu-id="b561d-133">Hello 다음 페이지에서 hello tooregister 데이터 카탈로그에 원하는 데이터 레이크 저장소 계정 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-133">On hello next page, provide hello Data Lake Store account name that you want tooregister in Data Catalog.</span></span> <span data-ttu-id="b561d-134">기본값으로 hello 다른 옵션을 유지 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-134">Leave hello other options as default and then click **Connect**.</span></span>

    <span data-ttu-id="b561d-135">![Connect toodata 소스](./media/data-lake-store-with-data-catalog/connect-to-source.png "toodata 소스 연결")</span><span class="sxs-lookup"><span data-stu-id="b561d-135">![Connect toodata source](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connect toodata source")</span></span>
7. <span data-ttu-id="b561d-136">hello 세그먼트를 다음으로 hello 다음 페이지를 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-136">hello next page can be divided into hello following segments.</span></span>

    <span data-ttu-id="b561d-137">a.</span><span class="sxs-lookup"><span data-stu-id="b561d-137">a.</span></span> <span data-ttu-id="b561d-138">hello **서버 계층** 상자 hello 데이터 레이크 저장소 계정 폴더 구조를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-138">hello **Server Hierarchy** box represents hello Data Lake Store account folder structure.</span></span> <span data-ttu-id="b561d-139">**$Root** 나타내는 데이터 레이크 저장소 계정 루트 hello 및 **AmbulanceData** 나타냅니다 hello hello 루트의 hello Data Lake 저장소 계정에서 만든 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-139">**$Root** represents hello Data Lake Store account root, and **AmbulanceData** represents hello folder created in hello root of hello Data Lake Store account.</span></span>

    <span data-ttu-id="b561d-140">b.</span><span class="sxs-lookup"><span data-stu-id="b561d-140">b.</span></span> <span data-ttu-id="b561d-141">hello **사용 가능한 개체** hello 파일 및 폴더 hello 아래 상자에 나열 **AmbulanceData** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-141">hello **Available objects** box lists hello files and folders under hello **AmbulanceData** folder.</span></span>

    <span data-ttu-id="b561d-142">c.</span><span class="sxs-lookup"><span data-stu-id="b561d-142">c.</span></span> <span data-ttu-id="b561d-143">**개체 toobe 등록 상자** 목록 hello 파일과 tooregister Azure Data Catalog에서 지정 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-143">**Objects toobe registered box** lists hello files and folders that you want tooregister in Azure Data Catalog.</span></span>

    <span data-ttu-id="b561d-144">![데이터 구조 보기](./media/data-lake-store-with-data-catalog/view-data-structure.png "데이터 구조 보기")</span><span class="sxs-lookup"><span data-stu-id="b561d-144">![View data structure](./media/data-lake-store-with-data-catalog/view-data-structure.png "View data structure")</span></span>
8. <span data-ttu-id="b561d-145">이 자습서에서는 hello 디렉터리에 모든 hello 파일을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-145">For this tutorial, you should register all hello files in hello directory.</span></span> <span data-ttu-id="b561d-146">이 위해 hello 클릭 (![개체 이동](./media/data-lake-store-with-data-catalog/move-objects.png "개체 이동")) 단추 toomove hello 모든 파일을 너무**개체 toobe 등록** 상자.</span><span class="sxs-lookup"><span data-stu-id="b561d-146">For that, click hello (![move objects](./media/data-lake-store-with-data-catalog/move-objects.png "Move objects")) button toomove all hello files too**Objects toobe registered** box.</span></span>

    <span data-ttu-id="b561d-147">Hello 데이터는 조직 전체의 데이터 카탈로그에 등록 됩니다, 되므로 나중에 사용할 수 있는 몇 가지 메타 데이터에는 마스킹할 권장 tooadd 접근 tooquickly hello 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-147">Because hello data will be registered in an organization-wide data catalog, it is a recommened approach tooadd some metadata which you can later use tooquickly locate hello data.</span></span> <span data-ttu-id="b561d-148">예를 들어 (예를 들어 사람은 hello 데이터를 업로드) hello 데이터 소유자 전자 메일 주소를 추가 하거나 태그 tooidentify hello 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-148">For example, you can add an e-mail address for hello data owner (for example, one who is uploading hello data) or add a tag tooidentify hello data.</span></span> <span data-ttu-id="b561d-149">아래 화면 캡처에서 hello toohello 데이터 추가 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-149">hello screen capture below shows a tag that we add toohello data.</span></span>

    <span data-ttu-id="b561d-150">![데이터 구조 보기](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "데이터 구조 보기")</span><span class="sxs-lookup"><span data-stu-id="b561d-150">![View data structure](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "View data structure")</span></span>

    <span data-ttu-id="b561d-151">**Register**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-151">Click **Register**.</span></span>
9. <span data-ttu-id="b561d-152">hello 다음 화면 캡처가 나타냅니다 hello 데이터 hello 데이터 카탈로그에에서 성공적으로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-152">hello following screen capture denotes that hello data is successfully registered in hello Data Catalog.</span></span>

    <span data-ttu-id="b561d-153">![등록 완료](./media/data-lake-store-with-data-catalog/registration-complete.png "데이터 구조 보기")</span><span class="sxs-lookup"><span data-stu-id="b561d-153">![Registration complete](./media/data-lake-store-with-data-catalog/registration-complete.png "View data structure")</span></span>
10. <span data-ttu-id="b561d-154">클릭 **보기 포털** toogo toohello Data Catalog 포털을 백업 하 고 액세스 hello hello 포털에서 데이터를 등록 하는 이제 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-154">Click **View Portal** toogo back toohello Data Catalog portal and verify that you can now access hello registered data from hello portal.</span></span> <span data-ttu-id="b561d-155">toosearch hello 데이터 hello 데이터를 등록 하는 동안 사용 하는 hello 태그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-155">toosearch hello data, you can use hello tag you used while registering hello data.</span></span>

     <span data-ttu-id="b561d-156">![카탈로그에서 데이터 검색](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "카탈로그에서 데이터 검색")</span><span class="sxs-lookup"><span data-stu-id="b561d-156">![Search data in catalog](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Search data in catalog")</span></span>
11. <span data-ttu-id="b561d-157">이제 주석 및 설명서 toohello 데이터를 추가 하는 등 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b561d-157">You can now perform operations like adding annotations and documentation toohello data.</span></span> <span data-ttu-id="b561d-158">자세한 내용은 링크를 따라 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b561d-158">For more information, see hello following links.</span></span>

    * [<span data-ttu-id="b561d-159">데이터 카탈로그에서 데이터 원본에 주석 추가</span><span class="sxs-lookup"><span data-stu-id="b561d-159">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
    * [<span data-ttu-id="b561d-160">데이터 카탈로그에서 데이터 원본 문서화</span><span class="sxs-lookup"><span data-stu-id="b561d-160">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a><span data-ttu-id="b561d-161">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b561d-161">See also</span></span>
* [<span data-ttu-id="b561d-162">데이터 카탈로그에서 데이터 원본에 주석 추가</span><span class="sxs-lookup"><span data-stu-id="b561d-162">Annotate data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-annotate.md)
* [<span data-ttu-id="b561d-163">데이터 카탈로그에서 데이터 원본 문서화</span><span class="sxs-lookup"><span data-stu-id="b561d-163">Document data sources in Data Catalog</span></span>](../data-catalog/data-catalog-how-to-documentation.md)
* [<span data-ttu-id="b561d-164">Data Lake 저장소를 다른 Azure 서비스와 통합</span><span class="sxs-lookup"><span data-stu-id="b561d-164">Integrate Data Lake Store with other Azure services</span></span>](data-lake-store-integrate-with-other-services.md)
