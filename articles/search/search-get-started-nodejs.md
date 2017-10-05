---
title: "Node.js에서 Azure Search 시작 | Microsoft Docs"
description: "Node.js를 프로그래밍 언어로 사용하여 사용자 지정 Azure에서 호스트된 클라우드 검색 서비스의 검색 응용 프로그램을 빌드하는 과정을 안내합니다."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="672c8-103">Node.js에서 Azure Search 시작</span><span class="sxs-lookup"><span data-stu-id="672c8-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="672c8-104">포털</span><span class="sxs-lookup"><span data-stu-id="672c8-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="672c8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="672c8-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="672c8-106">검색 환경에 Azure Search를 사용하는 사용자 지정 Node.js 검색 응용 프로그램을 빌드하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="672c8-107">이 자습서에서는 [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/dn798935.aspx) 를 사용하여 이 연습에서 사용되는 개체 및 작업을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="672c8-108">이 코드를 개발하고 테스트하는 데에는 [Node.js](https://Nodejs.org) 및 NPM, [Sublime Text 3](http://www.sublimetext.com/3) 및 Windows 8.1의 Windows PowerShell이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="672c8-109">이 샘플을 실행하려면 [Azure Portal](https://portal.azure.com)에서 등록할 수 있는 Azure Search 서비스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="672c8-110">단계별 지침은 [포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="672c8-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="672c8-111">데이터 정보</span><span class="sxs-lookup"><span data-stu-id="672c8-111">About the data</span></span>
<span data-ttu-id="672c8-112">이 샘플 응용 프로그램에서는 데이터 집합 크기를 줄이기 위해 Rhode Island 주에 대해 필터링된 [USGS(United States Geological Services)](http://geonames.usgs.gov/domestic/download_data.htm)의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="672c8-113">이 데이터를 사용하여 병원 및 학교와 같은 랜드마크 빌딩뿐만 아니라 강, 호수, 산 등의 지질학적 특징을 반환하는 검색 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="672c8-114">이 응용 프로그램에서 **DataIndexer** 프로그램은 [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) 구문을 사용하여 인덱스를 빌드 및 로드하며, 이를 통해 Azure SQL 데이터베이스에서 필터링된 USGS 데이터 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="672c8-115">온라인 데이터 원본에 대한 자격 증명 및 연결 정보는 프로그램 코드에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="672c8-116">추가 구성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="672c8-117">무료 가격 책정 계층의 문서 제한(10,000개) 미만으로 유지하기 위해 이 데이터 집합에 필터를 적용했습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="672c8-118">표준 계층을 사용하는 경우에는 이 제한이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="672c8-119">각 가격 책정 계층의 용량에 대한 자세한 내용은 [검색 서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="672c8-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="672c8-120">Azure 검색 서비스의 서비스 이름 및 api-key 찾기</span><span class="sxs-lookup"><span data-stu-id="672c8-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="672c8-121">서비스를 만든 후 포털로 돌아가서 URL 또는 `api-key`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="672c8-122">검색 서비스에 연결하려면 URL과 호출을 인증할 `api-key` 가 둘 다 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="672c8-123">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="672c8-124">점프 모음에서 **검색 서비스**를 클릭하여 구독에 프로비전된 모든 Azure Search 서비스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="672c8-125">사용하려는 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="672c8-126">서비스 대시보드에는 관리 키에 액세스할 수 있는 키 아이콘과 같은 필수 정보에 대한 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="672c8-127">서비스 URL, 관리 키 및 쿼리 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="672c8-128">세 항목 모두 나중에 config.js 파일에 추가할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="672c8-129">샘플 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="672c8-129">Download the sample files</span></span>
<span data-ttu-id="672c8-130">다음 방법 중 하나를 사용하여 샘플을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="672c8-131">[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="672c8-132">**Download ZIP**을 클릭하고 .zip 파일을 저장한 다음 포함된 모든 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="672c8-133">이후의 모든 파일 수정 및 실행 문은 이 폴더의 파일에 대해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="672c8-134">검색 서비스 URL 및 api-key로</span><span class="sxs-lookup"><span data-stu-id="672c8-134">Update the config.js.</span></span> <span data-ttu-id="672c8-135">config.js를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="672c8-136">앞에서 복사한 URL 및 api-key를 사용하여 구성 파일에서 URL, admin-key 및 query-key를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="672c8-137">관리 키는 인덱스 만들기 또는 삭제 및 문서 로드를 포함하여 서비스 작업에 대한 모든 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="672c8-138">반면, 쿼리 키는 읽기 전용 작업용이며, 일반적으로 Azure 검색에 연결하는 클라이언트 응용 프로그램에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="672c8-139">이 샘플에는 클라이언트 응용 프로그램에서 쿼리 키를 사용하는 모범 사례를 보강하는 데 도움이 되는 쿼리 키가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="672c8-140">다음 스크린샷에서는 텍스트 편집기에서 열려 있는 **config.js**를 보여 줍니다. 검색 서비스에 유효한 값으로 파일을 업데이트할 위치를 알 수 있도록 관련 항목이 경계선으로 구분되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="672c8-141">샘플에 대한 런타임 환경 호스트</span><span class="sxs-lookup"><span data-stu-id="672c8-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="672c8-142">이 샘플에는 npm을 사용하여 전역적으로 설치할 수 있는 HTTP 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="672c8-143">PowerShell 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="672c8-144">**package.json** 파일이 들어 있는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="672c8-145">`npm install`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-145">Type `npm install`.</span></span>
3. <span data-ttu-id="672c8-146">`npm install -g http-server`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="672c8-147">인덱스 빌드 및 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="672c8-147">Build the index and run the application</span></span>
1. <span data-ttu-id="672c8-148">`npm run indexDocuments`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="672c8-149">`npm run build`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="672c8-150">`npm run start_server`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="672c8-151">브라우저에서 `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="672c8-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="672c8-152">USGS 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="672c8-152">Search on USGS data</span></span>
<span data-ttu-id="672c8-153">USGS 데이터 집합에는 Rhode Island 주와 관련된 레코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="672c8-154">빈 검색 상자에서 **검색**을 클릭하면 기본적으로 상위 50개 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="672c8-155">검색 용어를 입력하면 검색 엔진이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="672c8-156">지역 이름을 입력해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-156">Try entering a regional name.</span></span> <span data-ttu-id="672c8-157">“Roger Williams”는 Rhode Island의 최초 주지사였습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="672c8-158">유명한 공원, 빌딩 및 학교가 그의 이름을 따라 이름을 지었습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="672c8-159">다음과 같은 용어를 입력해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="672c8-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="672c8-160">Pawtucket</span></span>
* <span data-ttu-id="672c8-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="672c8-161">Pembroke</span></span>
* <span data-ttu-id="672c8-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="672c8-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="672c8-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="672c8-163">Next steps</span></span>
<span data-ttu-id="672c8-164">이것은 Node.js 및 USGS 데이터 집합을 기반으로 하는 첫 번째 Azure Search 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="672c8-165">앞으로 이 자습서를 확장하여 사용자 지정 솔루션에서 사용할 수 있는 추가 검색 기능을 보여 드릴 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="672c8-166">Azure 검색에 대한 약간의 배경 지식이 이미 있는 경우 이 샘플을 기반으로 suggesters(사전 입력 또는 자동 완성 쿼리), 필터 및 패싯 탐색을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="672c8-167">또한 사용자가 결과 페이지를 차례로 탐색할 수 있도록 개수를 추가하고 문서를 일괄 처리하여 검색 결과 페이지를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="672c8-168">Azure 검색을 처음 사용하세요?</span><span class="sxs-lookup"><span data-stu-id="672c8-168">New to Azure Search?</span></span> <span data-ttu-id="672c8-169">다른 자습서를 통해 만들 수 있는 항목에 대한 이해를 높여 보세요.</span><span class="sxs-lookup"><span data-stu-id="672c8-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="672c8-170">더 많은 리소스를 보려면 [설명서 페이지](https://azure.microsoft.com/documentation/services/search/) 를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="672c8-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="672c8-171">[비디오 및 자습서](search-video-demo-tutorial-list.md) 의 링크를 통해 추가 정보를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="672c8-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
