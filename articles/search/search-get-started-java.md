---
title: "Java에서 Azure 검색 시작 aaaGet | Microsoft Docs"
description: "호스트 된 클라우드 toobuild Java 프로그래밍 언어를 사용 하 여 Azure에서 응용 프로그램 검색 하는 방법입니다."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="3a31f-103">Java에서 Azure 검색 시작</span><span class="sxs-lookup"><span data-stu-id="3a31f-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a31f-104">포털</span><span class="sxs-lookup"><span data-stu-id="3a31f-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="3a31f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3a31f-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="3a31f-106">사용자 지정 Java toobuild 검색 경험에 대 한 Azure 검색을 사용 하는 응용 프로그램을 검색 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="3a31f-107">이 자습서에서는 hello [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 개체 및이 연습에서 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="3a31f-108">toorun이이 샘플에서는 있어야 hello에에 등록할 수 있는 Azure 검색 서비스 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="3a31f-109">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 단계별 지침.</span><span class="sxs-lookup"><span data-stu-id="3a31f-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="3a31f-110">다음 소프트웨어 toobuild hello를 사용 하 고이 샘플을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="3a31f-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="3a31f-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="3a31f-112">있는지 toodownload hello EE 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="3a31f-113">Hello 확인 단계 중 하나에이 버전에만 있는 기능이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="3a31f-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="3a31f-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="3a31f-115">Apache는 Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="3a31f-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="3a31f-116">Hello 데이터에 대 한</span><span class="sxs-lookup"><span data-stu-id="3a31f-116">About hello data</span></span>
<span data-ttu-id="3a31f-117">이 샘플 응용 프로그램 데이터 hello에서 사용 하 여 [United States 지리 서비스 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)hello 로드 아일랜드 상태 tooreduce hello 데이터 집합 크기에 필터링 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="3a31f-118">이 데이터 toobuild 호수, 스트림과 summits 같은 지리 기능 뿐만 아니라 병원 학교와 같은 이정표 건물을 반환 하는 검색 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="3a31f-119">이 응용 프로그램에서는 hello **SearchServlet.java** 프로그램을 빌드하고 로드 hello를 사용 하 여 인덱스는 [인덱서](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello 검색 구문 공용 Azure SQL 데이터베이스에서 USG 데이터 집합을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="3a31f-120">미리 정의 된 자격 증명 및 연결 정보 toohello 온라인 데이터 원본 hello 프로그램 코드에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="3a31f-121">데이터 액세스 측면에서 추가 구성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="3a31f-122">Hello 10, 000 문서 제한의 hello 무료 가격 책정 계층에서이 데이터 집합 toostay에 필터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="3a31f-123">표준 계층 hello를 사용 하는 경우이 제한이 적용 되지 않습니다 하 고이 코드 toouse 큰 데이터 집합을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="3a31f-124">각 가격 책정 계층의 용량에 대한 자세한 내용은 [제한 및 제약 조건](search-limits-quotas-capacity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a31f-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="3a31f-125">Hello 프로그램 파일에 대 한</span><span class="sxs-lookup"><span data-stu-id="3a31f-125">About hello program files</span></span>
<span data-ttu-id="3a31f-126">hello 다음 목록에서는 관련 toothis 샘플 있는 hello 파일.</span><span class="sxs-lookup"><span data-stu-id="3a31f-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="3a31f-127">Search.jsp: hello 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="3a31f-128">SearchServlet.java: (MVC에서 유사한 tooa 컨트롤러) 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="3a31f-129">SearchServiceClient.java: HTTP 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="3a31f-130">SearchServiceHelper.java: 정적 메서드를 제공하는 도우미 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="3a31f-131">Hello 데이터 모델을 제공 하는 Document.java:</span><span class="sxs-lookup"><span data-stu-id="3a31f-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="3a31f-132">config.properties: hello 검색 서비스 URL 및 api 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="3a31f-133">Pom.xml: Maven 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="3a31f-134">Hello 서비스 이름 및 Azure 검색 서비스의 api 키 찾기</span><span class="sxs-lookup"><span data-stu-id="3a31f-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="3a31f-135">Azure 검색에 대 한 모든 REST API 호출 hello 서비스 URL 및 api 키를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="3a31f-136">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3a31f-137">Hello 점프 막대에서 클릭 **검색 서비스** toolist hello Azure 검색 서비스의 모든 구독에 대 한 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="3a31f-138">Toouse hello 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="3a31f-139">Hello 서비스 대시보드 타일에 대 한 중요 한 정보 뿐만 아니라 hello hello 관리자 키에 액세스 하기 위한 키 아이콘이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="3a31f-140">Hello 서비스 URL 및 관리자 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="3a31f-141">나중에 필요 합니다에, toohello를 추가할 때 **config.properties** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="3a31f-142">Hello 샘플 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="3a31f-142">Download hello sample files</span></span>
1. <span data-ttu-id="3a31f-143">너무 이동[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="3a31f-144">클릭 **zip 파일 다운로드**hello.zip 파일 toodisk 저장 한 다음 포함 된 모든 hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="3a31f-145">추출 하는 것이 좋습니다. hello로 파일 Java 작업 영역 toomake 것 보다 쉽게 toofind hello 프로젝트 나중입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="3a31f-146">hello 예제 파일은 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-146">hello sample files are read-only.</span></span> <span data-ttu-id="3a31f-147">폴더 속성 및 지우기 hello 읽기 전용 특성을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="3a31f-148">이후의 모든 파일 수정 및 실행 문은 이 폴더의 파일에 대해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="3a31f-149">프로젝트 가져오기</span><span class="sxs-lookup"><span data-stu-id="3a31f-149">Import project</span></span>
1. <span data-ttu-id="3a31f-150">Eclipse에서 **File** > **Import** > **General** > **Existing Projects into Workspace**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="3a31f-151">**Select의 루트 디렉터리**, 샘플 파일이 포함 된 toohello 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="3a31f-152">Hello 폴더가 포함 된 hello.project 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="3a31f-153">hello 프로젝트 hello에 표시될지 **프로젝트** 선택한 항목으로 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="3a31f-154">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-154">Click **Finish**.</span></span>
4. <span data-ttu-id="3a31f-155">사용 하 여 **프로젝트 탐색기** tooview 및 편집 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="3a31f-156">열려 있지 않으면 클릭 **창** > **보기 표시** > **프로젝트 탐색기** 하거나 바로 가기 tooopen hello를 사용 하 여 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="3a31f-157">Hello 서비스 URL 및 api 키 구성</span><span class="sxs-lookup"><span data-stu-id="3a31f-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="3a31f-158">**프로젝트 탐색기**를 두 번 클릭 **config.properties** tooedit hello 서버 이름 및 api 키를 포함 하는 hello 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="3a31f-159">Hello에 hello 서비스 URL 및 api 키가 발견 되는 위치,이 문서의 앞부분에 toohello 단계 참조 [Azure 포털](https://portal.azure.com), 이제 입력할 예정 tooget hello 값 **config.properties**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="3a31f-160">**config.properties**, "Api 키" 서비스에 대 한 hello api 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="3a31f-161">다음으로, 서비스 이름 (hello 첫 번째 구성 요소 hello URL http://servicename.search.windows.net)을 대체 "서비스 이름인" hello 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="3a31f-162">Hello 프로젝트, 빌드 및 런타임 환경 구성</span><span class="sxs-lookup"><span data-stu-id="3a31f-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="3a31f-163">Eclipse 프로젝트 탐색기에서에서 hello 프로젝트를 마우스 오른쪽 단추로 > **속성** > **프로젝트 패싯**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="3a31f-164">**Dynamic Web Module**, **Java** 및 **JavaScript**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="3a31f-165">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-165">Click **Apply**.</span></span>
4. <span data-ttu-id="3a31f-166"><seg>
  **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**를 선택합니다.</seg></span><span class="sxs-lookup"><span data-stu-id="3a31f-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="3a31f-167">Apache를 확장 하 고 이전에 설치한 hello Apache Tomcat 서버 hello 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="3a31f-168">예제 시스템에는 버전 8이 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="3a31f-169">Hello 다음 페이지에서 hello Tomcat 설치 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="3a31f-170">Windows 컴퓨터의 경우 일반적으로 C:\Program Files\Apache Software Foundation\Tomcat *버전*입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="3a31f-171">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-171">Click **Finish**.</span></span>
8. <span data-ttu-id="3a31f-172">**Window** > **Preferences** > **Java** > **Installed JREs** > **Add**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="3a31f-173">**Add JRE**에서 **Standard VM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="3a31f-174">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-174">Click **Next**.</span></span>
11. <span data-ttu-id="3a31f-175">JRE 정의의 JRE 홈에서 **Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="3a31f-176">너무 이동**Program Files** > **Java** hello 이전에 설치한 JDK를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="3a31f-177">중요 한 tooselect hello JDK 프로토콜은 JRE hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="3a31f-178">설치 된 JREs 선택 hello **JDK**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="3a31f-179">비슷한 toohello 스크린 샷 다음 설정에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="3a31f-180">필요에 따라 선택 **창** > **웹 브라우저** > **Internet Explorer** 외부 브라우저 창에서 tooopen hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="3a31f-181">외부 브라우저를 사용하면 웹 응용 프로그램 환경이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="3a31f-182">이제 hello 구성 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="3a31f-183">다음으로 작성 하 고 hello 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="3a31f-184">Hello 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="3a31f-184">Build hello project</span></span>
1. <span data-ttu-id="3a31f-185">프로젝트 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **실행** > **Maven 빌드 중...**  tooconfigure hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="3a31f-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="3a31f-186">Edit Configuration에서 Goals에 "clean install"을 입력하고 **Run**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="3a31f-187">상태 메시지는 출력 toohello 콘솔 창입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="3a31f-188">빌드 성공 나타내는 hello 프로젝트 오류 없이 구축 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="3a31f-189">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="3a31f-189">Run hello app</span></span>
<span data-ttu-id="3a31f-190">이 마지막 단계에서는 로컬 서버 런타임 환경에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="3a31f-191">Eclipse에서 서버 런타임 환경을 아직 지정 하지 않은 경우 해야 toodo을 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="3a31f-192">Project Explorer에서 **WebContent**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="3a31f-193">**Search.jsp** > **Run As** > **Run on Server**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="3a31f-194">Hello Apache Tomcat 서버를 선택한 다음 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="3a31f-195">를 사용 하는 기본이 아닌 작업 영역의 toostore 프로젝트 toomodify 맞춰야 **실행 구성** toopoint toohello 프로젝트 위치 tooavoid 서버 시작 시 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="3a31f-196">Project Explorer에서 **Search.jsp** > **Run As** > **Run Configurations**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="3a31f-197">Hello Apache Tomcat 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="3a31f-198">**Arguments**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-198">Click **Arguments**.</span></span> <span data-ttu-id="3a31f-199">클릭 **작업 영역** 또는 **파일 시스템** hello 프로젝트가 포함 된 tooset hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="3a31f-200">Hello 응용 프로그램을 실행 하면 표시 됩니다는 브라우저 창 용어를 입력 하기 위한 검색 상자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="3a31f-201">클릭 하기 전에 1 분 정도 기다렸다가 **검색** toogive hello 서비스 시간 toocreate 및 부하 hello 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="3a31f-202">HTTP 404 오류가 발생 하는 경우 하기만 하면 toowait 약간 더 긴 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a31f-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="3a31f-203">USGS 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="3a31f-203">Search on USGS data</span></span>
<span data-ttu-id="3a31f-204">hello USG 데이터 집합에 로드 아일랜드의 관련 toohello 상태 레코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="3a31f-205">클릭 하면 **검색** 빈 검색 상자에 항목을 가져오게 됩니다 hello 상위 50 개의 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="3a31f-206">검색어를 입력 합니다 hello 검색 엔진 어떤 toogo에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="3a31f-207">지역 이름을 입력해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-207">Try entering a regional name.</span></span> <span data-ttu-id="3a31f-208">"Roger Williams" hello 로드 아일랜드의 첫 번째 관리자 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="3a31f-209">유명한 공원, 빌딩 및 학교가 그의 이름을 따라 이름을 지었습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="3a31f-210">다음과 같은 용어를 입력해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="3a31f-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="3a31f-211">Pawtucket</span></span>
* <span data-ttu-id="3a31f-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="3a31f-212">Pembroke</span></span>
* <span data-ttu-id="3a31f-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="3a31f-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a31f-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a31f-214">Next steps</span></span>
<span data-ttu-id="3a31f-215">Java 및 hello USG 데이터 집합에 따라 hello 첫 번째 Azure 검색 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="3a31f-216">시간이 지남에 따라 추가 검색 기능을 사용자 지정 솔루션에서 toouse 할 수 있습니다이 자습서 toodemonstrate를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="3a31f-217">Azure 검색의 몇 가지 배경 이미 있는 경우으로 사용할 수 있습니다이 예제는 springboard 추가 실험에 대 한 hello 아마도 확대 [검색 페이지](search-pagination-page-layout.md), 구현 또는 [패싯 탐색](search-faceted-navigation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="3a31f-218">또한 개수를 추가 하 고 hello 결과 통해 사용자가 페이지로 이동할 수 있도록 문서를 일괄 처리 하 여 hello 검색 결과 페이지를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="3a31f-219">새 tooAzure 검색?</span><span class="sxs-lookup"><span data-stu-id="3a31f-219">New tooAzure Search?</span></span> <span data-ttu-id="3a31f-220">다른 자습서 toodevelop 만들 수는 이해 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="3a31f-221">방문 우리의 [설명서 페이지](https://azure.microsoft.com/documentation/services/search/) toofind 리소스를 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a31f-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="3a31f-222">Hello에 대 한 링크를 볼 수도 있습니다 우리의 [비디오 및 자습서 목록](search-video-demo-tutorial-list.md) tooaccess 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="3a31f-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
