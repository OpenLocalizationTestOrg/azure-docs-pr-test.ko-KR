---
title: "Node.js에서 Azure 검색 시작 aaaGet | Microsoft Docs"
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="6d7c4-103">Node.js에서 Azure Search 시작</span><span class="sxs-lookup"><span data-stu-id="6d7c4-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d7c4-104">포털</span><span class="sxs-lookup"><span data-stu-id="6d7c4-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="6d7c4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6d7c4-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="6d7c4-106">사용자 지정 Node.js toobuild 검색 경험에 대 한 Azure 검색을 사용 하는 응용 프로그램을 검색 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="6d7c4-107">이 자습서에서는 hello [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 개체 및이 연습에서 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="6d7c4-108">사용 [Node.js](https://Nodejs.org) 및 NPM [Sublime 텍스트 3](http://www.sublimetext.com/3), 및 Windows 8.1 toodevelop에서 Windows PowerShell이이 코드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="6d7c4-109">toorun이이 샘플에서는 있어야 hello에에 등록할 수 있는 Azure 검색 서비스 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6d7c4-110">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 단계별 지침.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="6d7c4-111">Hello 데이터에 대 한</span><span class="sxs-lookup"><span data-stu-id="6d7c4-111">About hello data</span></span>
<span data-ttu-id="6d7c4-112">이 샘플 응용 프로그램 데이터 hello에서 사용 하 여 [United States 지리 서비스 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)hello 로드 아일랜드 상태 tooreduce hello 데이터 집합 크기에 필터링 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="6d7c4-113">이 데이터 toobuild 호수, 스트림과 summits 같은 지리 기능 뿐만 아니라 병원 학교와 같은 이정표 건물을 반환 하는 검색 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="6d7c4-114">이 응용 프로그램에서는 hello **DataIndexer** 프로그램을 빌드하고 로드 hello를 사용 하 여 인덱스는 [인덱서](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello 검색 구문 공용 Azure SQL 데이터베이스에서 USG 데이터 집합을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="6d7c4-115">자격 증명 및 연결 정보 toohello 온라인 데이터 원본을 hello 프로그램 코드에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="6d7c4-116">추가 구성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="6d7c4-117">Hello 10, 000 문서 제한의 hello 무료 가격 책정 계층에서이 데이터 집합 toostay에 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="6d7c4-118">표준 계층 hello를 사용 하는 경우이 제한이 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="6d7c4-119">각 가격 책정 계층의 용량에 대한 자세한 내용은 [검색 서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="6d7c4-120">Hello 서비스 이름 및 Azure 검색 서비스의 api 키 찾기</span><span class="sxs-lookup"><span data-stu-id="6d7c4-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="6d7c4-121">Hello 서비스를 만든 후 반환 toohello 포털 tooget hello URL 또는 `api-key`합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="6d7c4-122">연결 tooyour 검색 서비스가 있어야 두 hello URL 및 `api-key` tooauthenticate hello 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="6d7c4-123">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6d7c4-124">Hello 점프 막대에서 클릭 **검색 서비스** toolist 구독에 대 한 모든 Azure 검색 서비스를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="6d7c4-125">Toouse hello 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="6d7c4-126">Hello 서비스 대시보드에서 타일 hello 관리자 키에 액세스 하기 위한 키 아이콘 hello와 같은 중요 한 정보에 대 한 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="6d7c4-127">Hello 서비스 URL, 관리자 키 및 쿼리 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="6d7c4-128">나중에 세 가지 모두 필요 하면 toohello config.js 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="6d7c4-129">Hello 샘플 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="6d7c4-129">Download hello sample files</span></span>
<span data-ttu-id="6d7c4-130">Hello 접근 방식을 toodownload hello 샘플 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="6d7c4-131">너무 이동[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="6d7c4-132">클릭 **zip 파일 다운로드**, hello.zip 파일을 저장 한 다음 포함 된 모든 hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="6d7c4-133">이후의 모든 파일 수정 및 실행 문은 이 폴더의 파일에 대해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="6d7c4-134">Hello config.js를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-134">Update hello config.js.</span></span> <span data-ttu-id="6d7c4-135">config.js를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="6d7c4-136">URL 및 api 키가 이전에 복사 하는 hello를 사용 하 여 구성 파일에 URL hello 관리자 키 및 쿼리 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="6d7c4-137">관리 키는 인덱스 만들기 또는 삭제 및 문서 로드를 포함하여 서비스 작업에 대한 모든 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="6d7c4-138">이와 달리 쿼리 키는 tooAzure 검색을 연결 하는 클라이언트 응용 프로그램에서 일반적으로 사용 하는 읽기 전용 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="6d7c4-139">이 샘플에서는 키 toohelp hello hello 쿼리 키를 사용 하 여 클라이언트 응용 프로그램에서 모범 사례를 보완 하는 hello 쿼리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="6d7c4-140">다음 스크린 샷에 표시 hello **config.js** hello로 텍스트 편집기에 열려 있는 hello로 tooupdate hello 파일 값을 볼 수 있도록 demarcated 관련 항목은 검색 서비스에 대해 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="6d7c4-141">호스트 hello 샘플에 대 한 런타임 환경</span><span class="sxs-lookup"><span data-stu-id="6d7c4-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="6d7c4-142">hello 샘플 필요 HTTP 서버는 전역적으로 npm을 사용 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="6d7c4-143">다음 명령을 hello에 대 한 PowerShell 창을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="6d7c4-144">Hello 있는 toohello 폴더 탐색 **package.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="6d7c4-145">`npm install`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-145">Type `npm install`.</span></span>
3. <span data-ttu-id="6d7c4-146">`npm install -g http-server`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="6d7c4-147">Hello 응용 hello 인덱스를 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="6d7c4-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="6d7c4-148">`npm run indexDocuments`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="6d7c4-149">`npm run build`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="6d7c4-150">`npm run start_server`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="6d7c4-151">브라우저에서 `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="6d7c4-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="6d7c4-152">USGS 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="6d7c4-152">Search on USGS data</span></span>
<span data-ttu-id="6d7c4-153">hello USG 데이터 집합에 로드 아일랜드의 관련 toohello 상태 레코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="6d7c4-154">클릭 하면 **검색** 빈 검색 상자에서 얻게 hello 상위 50 개의 항목 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="6d7c4-155">검색어를 입력 제공 hello 검색 엔진 항목 합계에 toogo 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="6d7c4-156">지역 이름을 입력해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-156">Try entering a regional name.</span></span> <span data-ttu-id="6d7c4-157">"Roger Williams" hello 로드 아일랜드의 첫 번째 관리자 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="6d7c4-158">유명한 공원, 빌딩 및 학교가 그의 이름을 따라 이름을 지었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="6d7c4-159">다음과 같은 용어를 입력해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="6d7c4-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="6d7c4-160">Pawtucket</span></span>
* <span data-ttu-id="6d7c4-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="6d7c4-161">Pembroke</span></span>
* <span data-ttu-id="6d7c4-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="6d7c4-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d7c4-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d7c4-163">Next steps</span></span>
<span data-ttu-id="6d7c4-164">Node.js 및 hello USG 데이터 집합에 따라 hello 첫 번째 Azure 검색 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="6d7c4-165">시간이 지남에 따라 추가 검색 기능을 사용자 지정 솔루션에서 toouse 할 수 있습니다이 자습서 toodemonstrate를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="6d7c4-166">Azure 검색에 대한 약간의 배경 지식이 이미 있는 경우 이 샘플을 기반으로 suggesters(사전 입력 또는 자동 완성 쿼리), 필터 및 패싯 탐색을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="6d7c4-167">또한 개수를 추가 하 고 hello 결과 통해 사용자가 페이지로 이동할 수 있도록 문서를 일괄 처리 하 여 hello 검색 결과 페이지를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="6d7c4-168">새 tooAzure 검색?</span><span class="sxs-lookup"><span data-stu-id="6d7c4-168">New tooAzure Search?</span></span> <span data-ttu-id="6d7c4-169">다른 자습서 toodevelop 만들 수는 이해 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="6d7c4-170">방문 우리의 [설명서 페이지](https://azure.microsoft.com/documentation/services/search/) toofind 리소스를 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="6d7c4-171">Hello에 대 한 링크를 볼 수도 있습니다 우리의 [비디오 및 자습서 목록](search-video-demo-tutorial-list.md) tooaccess 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="6d7c4-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
