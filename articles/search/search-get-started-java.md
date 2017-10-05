---
title: "Java에서 Azure 검색 시작 | Microsoft Docs"
description: "Java를 프로그래밍 언어로 사용하여 Azure에서 호스트된 클라우드 검색 응용 프로그램을 빌드하는 방법입니다."
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
ms.openlocfilehash: f6ca06a0349def97b38a1bf6d0d8f36236077e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="c7601-103">Java에서 Azure 검색 시작</span><span class="sxs-lookup"><span data-stu-id="c7601-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7601-104">포털</span><span class="sxs-lookup"><span data-stu-id="c7601-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="c7601-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c7601-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="c7601-106">검색 환경에 Azure 검색을 사용하는 사용자 지정 Java 검색 응용 프로그램을 빌드하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="c7601-107">이 자습서에서는 [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/dn798935.aspx) 를 사용하여 이 연습에서 사용되는 개체 및 작업을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="c7601-108">이 샘플을 실행하려면 [Azure 포털](https://portal.azure.com)에서 등록할 수 있는 Azure 검색 서비스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="c7601-109">단계별 지침은 [포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7601-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="c7601-110">이 샘플을 빌드 및 테스트하는 데 사용된 소프트웨어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-110">We used the following software to build and test this sample:</span></span>

* <span data-ttu-id="c7601-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="c7601-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="c7601-112">EE 버전을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-112">Be sure to download the EE version.</span></span> <span data-ttu-id="c7601-113">확인 단계 중 하나에 이 버전에만 있는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-113">One of the verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="c7601-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="c7601-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="c7601-115">Apache는 Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="c7601-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-the-data"></a><span data-ttu-id="c7601-116">데이터 정보</span><span class="sxs-lookup"><span data-stu-id="c7601-116">About the data</span></span>
<span data-ttu-id="c7601-117">이 샘플 응용 프로그램에서는 데이터 집합 크기를 줄이기 위해 Rhode Island 주에 대해 필터링된 [USGS(United States Geological Services)](http://geonames.usgs.gov/domestic/download_data.htm)의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="c7601-118">이 데이터를 사용하여 병원 및 학교와 같은 랜드마크 빌딩뿐만 아니라 강, 호수, 산 등의 지질학적 특징을 반환하는 검색 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="c7601-119">이 응용 프로그램에서 **SearchServlet.java** 프로그램은 [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) 구문을 사용하여 인덱스를 빌드 및 로드하며, 이를 통해 Azure SQL 데이터베이스에서 필터링된 USGS 데이터 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="c7601-120">온라인 데이터 원본에 대한 미리 정의된 자격 증명 및 연결 정보는 프로그램 코드에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span></span> <span data-ttu-id="c7601-121">데이터 액세스 측면에서 추가 구성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="c7601-122">무료 가격 책정 계층의 문서 제한(10,000개) 미만으로 유지하기 위해 이 데이터 집합에 필터를 적용했습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-122">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="c7601-123">표준 계층을 사용하는 경우에는 이 제한이 적용되지 않으며 이 코드를 수정하여 더 큰 데이터 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-123">If you use the standard tier, this limit does not apply, and you can modify this code to use a bigger dataset.</span></span> <span data-ttu-id="c7601-124">각 가격 책정 계층의 용량에 대한 자세한 내용은 [제한 및 제약 조건](search-limits-quotas-capacity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7601-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-the-program-files"></a><span data-ttu-id="c7601-125">프로그램 파일 정보</span><span class="sxs-lookup"><span data-stu-id="c7601-125">About the program files</span></span>
<span data-ttu-id="c7601-126">다음 목록에서는 이 샘플과 관련된 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-126">The following list describes the files that are relevant to this sample.</span></span>

* <span data-ttu-id="c7601-127">Search.jsp: 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-127">Search.jsp: Provides the user interface</span></span>
* <span data-ttu-id="c7601-128">SearchServlet.java: 메서드(MVC의 컨트롤러와 유사)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span></span>
* <span data-ttu-id="c7601-129">SearchServiceClient.java: HTTP 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="c7601-130">SearchServiceHelper.java: 정적 메서드를 제공하는 도우미 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="c7601-131">Document.java: 데이터 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-131">Document.java: Provides the data model</span></span>
* <span data-ttu-id="c7601-132">config.properties: 검색 서비스 URL 및 api-key를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-132">config.properties: Sets the Search service URL and api-key</span></span>
* <span data-ttu-id="c7601-133">Pom.xml: Maven 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="c7601-134">Azure 검색 서비스의 서비스 이름 및 api-key 찾기</span><span class="sxs-lookup"><span data-stu-id="c7601-134">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="c7601-135">Azure 검색에 대한 모든 REST API 호출에는 서비스 URL 및 api-key를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span></span> 

1. <span data-ttu-id="c7601-136">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-136">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c7601-137">점프 모음에서 **검색 서비스** 를 클릭하여 구독에 프로비전된 Azure 검색 서비스를 모두 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="c7601-138">사용하려는 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-138">Select the service you want to use.</span></span>
4. <span data-ttu-id="c7601-139">서비스 대시보드에 필수 정보에 대한 타일 및 관리 키에 액세스할 수 있는 키 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="c7601-140">서비스 URL 및 관리 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-140">Copy the service URL and an admin key.</span></span> <span data-ttu-id="c7601-141">나중에 **config.properties** 파일에 추가할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-141">You will need them later, when you add them to the **config.properties** file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="c7601-142">샘플 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="c7601-142">Download the sample files</span></span>
1. <span data-ttu-id="c7601-143">GitHub의 [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-143">Go to [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="c7601-144">**Download ZIP**을 클릭하고 .zip 파일을 디스크에 저장한 다음 포함된 모든 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span></span> <span data-ttu-id="c7601-145">나중에 프로젝트를 쉽게 찾을 수 있도록 Java 작업 영역에 파일을 추출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span></span>
3. <span data-ttu-id="c7601-146">샘플 파일은 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-146">The sample files are read-only.</span></span> <span data-ttu-id="c7601-147">폴더 속성을 마우스 오른쪽 단추로 클릭하고 읽기 전용 특성을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-147">Right-click folder properties and clear the read-only attribute.</span></span>

<span data-ttu-id="c7601-148">이후의 모든 파일 수정 및 실행 문은 이 폴더의 파일에 대해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="c7601-149">프로젝트 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7601-149">Import project</span></span>
1. <span data-ttu-id="c7601-150">Eclipse에서 **File** > **Import** > **General** > **Existing Projects into Workspace**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="c7601-151">**Select root directory**에서 샘플 파일이 들어 있는 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-151">In **Select root directory**, browse to the folder containing sample files.</span></span> <span data-ttu-id="c7601-152">.project 폴더가 포함된 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-152">Select the folder that contains the .project folder.</span></span> <span data-ttu-id="c7601-153">**Projects** 목록에 선택한 항목으로 프로젝트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-153">The project should appear in the **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="c7601-154">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-154">Click **Finish**.</span></span>
4. <span data-ttu-id="c7601-155">**Project Explorer** 를 사용하여 파일을 보고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-155">Use **Project Explorer** to view and edit the files.</span></span> <span data-ttu-id="c7601-156">아직 열지 않은 경우 **Window** > **Show View** > **Project Explorer**를 클릭하거나 바로 가기를 사용하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span></span>

## <a name="configure-the-service-url-and-api-key"></a><span data-ttu-id="c7601-157">서비스 URL 및 api-key 구성</span><span class="sxs-lookup"><span data-stu-id="c7601-157">Configure the service URL and api-key</span></span>
1. <span data-ttu-id="c7601-158">**Project Explorer**에서 **config.properties**를 두 번 클릭하여 서버 이름 및 api-key가 포함된 구성 설정을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span></span>
2. <span data-ttu-id="c7601-159">이 문서의 이전 단계를 참조하여 [config.properties](https://portal.azure.com)에 입력할 값을 가져오도록 **Azure 포털**에서 서비스 URL 및 api-key를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="c7601-160">**config.properties**에서 "Api Key"를 서비스의 api-key로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span></span> <span data-ttu-id="c7601-161">그러면 서비스 이름(URL http://servicename.search.windows.net의 첫 번째 구성 요소)이 동일한 파일의 "service name"을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span></span>
   
    ![][5]

## <a name="configure-the-project-build-and-runtime-environments"></a><span data-ttu-id="c7601-162">프로젝트, 빌드 및 런타임 환경 구성</span><span class="sxs-lookup"><span data-stu-id="c7601-162">Configure the project, build and runtime environments</span></span>
1. <span data-ttu-id="c7601-163">Eclipse의 Project Explorer에서 프로젝트 > **Properties** > **Project Facets**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="c7601-164">**Dynamic Web Module**, **Java** 및 **JavaScript**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="c7601-165">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-165">Click **Apply**.</span></span>
4. <span data-ttu-id="c7601-166"><seg>
  **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**를 선택합니다.</seg></span><span class="sxs-lookup"><span data-stu-id="c7601-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="c7601-167">Apache를 확장하고 이전에 설치한 Apache Tomcat 서버의 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="c7601-168">예제 시스템에는 버전 8이 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="c7601-169">다음 페이지에서 Tomcat 설치 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-169">On the next page, specify the Tomcat installation directory.</span></span> <span data-ttu-id="c7601-170">Windows 컴퓨터의 경우 일반적으로 C:\Program Files\Apache Software Foundation\Tomcat *버전*입니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="c7601-171">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-171">Click **Finish**.</span></span>
8. <span data-ttu-id="c7601-172">**Window** > **Preferences** > **Java** > **Installed JREs** > **Add**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="c7601-173">**Add JRE**에서 **Standard VM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="c7601-174">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-174">Click **Next**.</span></span>
11. <span data-ttu-id="c7601-175">JRE 정의의 JRE 홈에서 **Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="c7601-176">**Program Files** > **Java**로 이동하여 이전에 설치한 JDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span></span> <span data-ttu-id="c7601-177">JDK를 JRE로 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-177">It's important to select the JDK as the JRE.</span></span>
13. <span data-ttu-id="c7601-178">Installed JREs에서 **JDK**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-178">In Installed JREs, choose the **JDK**.</span></span> <span data-ttu-id="c7601-179">설정은 다음 스크린샷과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-179">Your settings should look similar to the following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="c7601-180">필요에 따라 **Window** > **Web Browser** > **Internet Explorer**를 선택하여 외부 브라우저 창에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span></span> <span data-ttu-id="c7601-181">외부 브라우저를 사용하면 웹 응용 프로그램 환경이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="c7601-182">이제 구성 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-182">You have now completed the configuration tasks.</span></span> <span data-ttu-id="c7601-183">다음으로, 프로젝트를 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-183">Next, you'll build and run the project.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="c7601-184">프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="c7601-184">Build the project</span></span>
1. <span data-ttu-id="c7601-185">Project Explorer에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **Run As** > **Maven build...**를 선택하여 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span></span>
   
    ![][10]
2. <span data-ttu-id="c7601-186">Edit Configuration에서 Goals에 "clean install"을 입력하고 **Run**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="c7601-187">콘솔 창에 상태 메시지가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-187">Status messages are output to the console window.</span></span> <span data-ttu-id="c7601-188">오류 없이 빌드에 성공했음을 나타내는 BUILD SUCCESS가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-188">You should see BUILD SUCCESS indicating the project built without errors.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="c7601-189">앱 실행</span><span class="sxs-lookup"><span data-stu-id="c7601-189">Run the app</span></span>
<span data-ttu-id="c7601-190">이 마지막 단계에서는 로컬 서버 런타임 환경에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-190">In this last step, you will run the application in a local server runtime environment.</span></span>

<span data-ttu-id="c7601-191">Eclipse에서 서버 런타임 환경을 아직 지정하지 않은 경우 이 작업을 먼저 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span></span>

1. <span data-ttu-id="c7601-192">Project Explorer에서 **WebContent**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="c7601-193">**Search.jsp** > **Run As** > **Run on Server**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="c7601-194">Apache Tomcat 서버를 선택하고 **Run**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-194">Select the Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="c7601-195">기본이 아닌 작업 영역을 사용하여 프로젝트를 저장한 경우 서버 시작 오류를 방지하기 위해 프로젝트 위치를 가리키도록 **Run Configuration** 을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-195">If you used a non-default workspace to store your project, you'll need to modify **Run Configuration** to point to the project location to avoid a server start-up error.</span></span> <span data-ttu-id="c7601-196">Project Explorer에서 **Search.jsp** > **Run As** > **Run Configurations**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="c7601-197">Apache Tomcat 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-197">Select the Apache Tomcat server.</span></span> <span data-ttu-id="c7601-198">**Arguments**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-198">Click **Arguments**.</span></span> <span data-ttu-id="c7601-199">**Workspace** 또는 **File System**을 클릭하여 프로젝트가 포함된 폴더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-199">Click **Workspace** or **File System** to set the folder containing the project.</span></span>
> 
> 

<span data-ttu-id="c7601-200">응용 프로그램을 실행하면 용어를 입력할 수 있는 검색 상자를 제공하는 브라우저 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="c7601-201">1분 정도 기다렸다가 **Search** 를 클릭하여 인덱스를 만들고 로드할 서비스 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span></span> <span data-ttu-id="c7601-202">HTTP 404 오류가 발생하는 경우 좀 더 기다렸다가 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="c7601-203">USGS 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="c7601-203">Search on USGS data</span></span>
<span data-ttu-id="c7601-204">USGS 데이터 집합에는 Rhode Island 주와 관련된 레코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="c7601-205">빈 검색 상자에서 **검색** 을 클릭하면 기본적으로 상위 50개 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="c7601-206">검색 용어를 입력하면 검색 엔진이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-206">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="c7601-207">지역 이름을 입력해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-207">Try entering a regional name.</span></span> <span data-ttu-id="c7601-208">“Roger Williams”는 Rhode Island의 최초 주지사였습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-208">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="c7601-209">유명한 공원, 빌딩 및 학교가 그의 이름을 따라 이름을 지었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="c7601-210">다음과 같은 용어를 입력해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="c7601-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="c7601-211">Pawtucket</span></span>
* <span data-ttu-id="c7601-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="c7601-212">Pembroke</span></span>
* <span data-ttu-id="c7601-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="c7601-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7601-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7601-214">Next steps</span></span>
<span data-ttu-id="c7601-215">이것은 Java 및 USGS 데이터 집합을 기반으로 하는 첫 번째 Azure 검색 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span></span> <span data-ttu-id="c7601-216">앞으로 이 자습서를 확장하여 사용자 지정 솔루션에서 사용할 수 있는 추가 검색 기능을 보여 드릴 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="c7601-217">Azure 검색에 대한 약간의 배경 지식이 있는 경우 [검색 페이지](search-pagination-page-layout.md)를 보강하거나 [패싯 탐색](search-faceted-navigation.md)을 구현하는 등 이 샘플을 기반으로 추가 실험을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="c7601-218">또한 사용자가 결과 페이지를 차례로 탐색할 수 있도록 개수를 추가하고 문서를 일괄 처리하여 검색 결과 페이지를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="c7601-219">Azure 검색을 처음 사용하세요?</span><span class="sxs-lookup"><span data-stu-id="c7601-219">New to Azure Search?</span></span> <span data-ttu-id="c7601-220">다른 자습서를 통해 만들 수 있는 항목에 대한 이해를 높여 보세요.</span><span class="sxs-lookup"><span data-stu-id="c7601-220">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="c7601-221">더 많은 리소스를 보려면 [설명서 페이지](https://azure.microsoft.com/documentation/services/search/) 를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c7601-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="c7601-222">[비디오 및 자습서](search-video-demo-tutorial-list.md) 의 링크를 통해 추가 정보를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7601-222">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

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
