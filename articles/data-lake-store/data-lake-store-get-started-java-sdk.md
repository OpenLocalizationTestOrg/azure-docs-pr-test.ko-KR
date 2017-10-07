---
title: "aaaUse hello Java SDK toodevelop 응용 프로그램에서 Azure 데이터 레이크 저장소 | Microsoft Docs"
description: "Azure 데이터 레이크 저장소 Java SDK toocreate 데이터 레이크 저장소 계정을 사용 하 고 hello 데이터 레이크 저장소의에서 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="e3cc4-103">Java를 사용하여 Azure Data Lake 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="e3cc4-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3cc4-104">포털</span><span class="sxs-lookup"><span data-stu-id="e3cc4-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="e3cc4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3cc4-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="e3cc4-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="e3cc4-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="e3cc4-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="e3cc4-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="e3cc4-108">REST API</span><span class="sxs-lookup"><span data-stu-id="e3cc4-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="e3cc4-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e3cc4-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="e3cc4-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e3cc4-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="e3cc4-111">Python</span><span class="sxs-lookup"><span data-stu-id="e3cc4-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="e3cc4-112">와 같은 toouse hello Azure 데이터 레이크 저장소 Java SDK tooperform 기본 작업 폴더를 만들려면 어떻게, 업로드 알아보고 등 데이터 파일을 다운로드 합니다. Data Lake에 대한 자세한 내용은 [Azure Data Lake Store](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="e3cc4-113">Azure 데이터 레이크 저장소에 대 한 hello Java SDK API 문서에 액세스할 수 있습니다 [Azure 데이터 레이크 저장소 Java API 문서](https://azure.github.io/azure-data-lake-store-java/javadoc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3cc4-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e3cc4-114">Prerequisites</span></span>
* <span data-ttu-id="e3cc4-115">Java 개발 키트(JDK 7 이상, Java 버전 1.7 이상 사용)</span><span class="sxs-lookup"><span data-stu-id="e3cc4-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="e3cc4-116">Azure Data Lake Store 계정</span><span class="sxs-lookup"><span data-stu-id="e3cc4-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="e3cc4-117">Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="e3cc4-118">[Maven](https://maven.apache.org/install.html)</span><span class="sxs-lookup"><span data-stu-id="e3cc4-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="e3cc4-119">이 자습서에서는 빌드 및 프로젝트 종속성을 위해 Maven을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="e3cc4-120">Maven 또는 Gradle 빌드 시스템을 사용 하지 않고 가능한 toobuild는 아니지만 시스템 확인이 훨씬 더 쉽게 toomanage 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="e3cc4-121">(선택 사항)[IntelliJ IDEA](https://www.jetbrains.com/idea/download/) 또는 [Eclipse](https://www.eclipse.org/downloads/)나 유사한 IDE</span><span class="sxs-lookup"><span data-stu-id="e3cc4-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="e3cc4-122">Azure Active Directory를 사용하여 인증하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="e3cc4-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="e3cc4-123">이 자습서는 Azure AD 응용 프로그램 클라이언트 비밀 tooretrieve Azure Active Directory 토큰 (서비스 간 인증)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="e3cc4-124">이 토큰 toocreate 데이터 레이크 저장소 클라이언트 개체 tooperform 작업 파일 및 디렉터리 작업 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="e3cc4-125">에 대 한 지침은 방법을 사용 하 여 Azure 데이터 레이크 저장소 tooauthenticate hello 클라이언트 암호, 상위 수준 단계를 수행 하는 hello를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="e3cc4-126">Azure AD 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e3cc4-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="e3cc4-127">Hello 클라이언트 ID, 클라이언트 암호 및 hello Azure AD 웹 응용 프로그램에 대 한 토큰 끝점을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="e3cc4-128">데이터 레이크 저장소 파일/폴더에서 Java 응용 프로그램을 만들려는 hello tooaccess 원하는 hello에 hello Azure AD 웹 응용 프로그램에 대 한 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="e3cc4-129">다음이 단계를 참조 하는 tooperform 어떻게에 대 한 지침은 [Active Directory 응용 프로그램을 만들려면](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="e3cc4-130">Azure Active Directory는 다른 옵션도 tooretrieve 토큰을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="e3cc4-131">수에서 선택 하 여 다양 한 다른 인증 메커니즘 toosuit 시나리오에서는 예를 들어 Azure 가상 또는 온-프레미스를 실행 하는 서버 응용 프로그램, 데스크톱 응용 프로그램으로 배포 응용 프로그램 또는 브라우저에서 실행 중인 응용 프로그램 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="e3cc4-132">암호, 인증서, 2단계 인증과 같은 여러 유형의 자격 증명을 선택할 수 있습니다. 또한 Azure Active Directory를 사용 하면 toosynchronize hello 클라우드와 온-프레미스 Active Directory 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="e3cc4-133">자세한 내용은 [Azure Active directory 인증 시나리오](../active-directory/active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="e3cc4-134">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e3cc4-134">Create a Java application</span></span>
<span data-ttu-id="e3cc4-135">사용할 수 있는 코드 샘플 hello [GitHub에서](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) hello 저장소에서 파일을 만들지, 파일을 연결 하는 파일을 다운로드 및 hello 저장소에서 일부 파일을 삭제의 hello 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="e3cc4-136">Hello 코드의 주요 부분은 hello 수 있도록 안내 하는 hello 문서의이 섹션.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="e3cc4-137">사용 하 여 Maven 프로젝트 만들기 [mvn 아키타](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 에서 명령줄 hello 또는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="e3cc4-138">Toocreate Java 프로젝트 IntelliJ를 사용 하 여 하는 방법에 지침은 [여기](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="e3cc4-139">방법에 대 한 지침은 toocreate Eclipse를 사용 하 여 프로젝트 참조 [여기](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="e3cc4-140">추가 종속성 tooyour Maven 다음 hello **pom.xml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="e3cc4-141">Hello 텍스트 조각을 hello 사이 다음 추가  **\</version >** 태그 및 hello  **\</프로젝트 >** 태그:</span><span class="sxs-lookup"><span data-stu-id="e3cc4-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="e3cc4-142">첫 번째 종속성 hello는 toouse hello 데이터 레이크 저장소 SDK (`azure-data-lake-store-sdk`) hello maven 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="e3cc4-143">두 번째 종속성 hello (`slf4j-nop`) toospecify이 응용이 프로그램에 대 한 로깅 프레임 워크 toouse 어떤 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="e3cc4-144">hello 데이터 레이크 저장소 SDK 사용 [slf4j](http://www.slf4j.org/) Java 로깅, logback 등 다양 한 log4j와 같은 인기 있는 로깅 프레임 워크 중에서 선택할 수 있는 로깅 외관 또는 로깅은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="e3cc4-145">이 예제에 대 한 로깅을 비활성화 됩니다, 따라서 사용 하 여 hello **slf4j nop** 바인딩.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="e3cc4-146">toouse 응용 프로그램에서 다른 로깅 옵션 참조 [여기](http://www.slf4j.org/manual.html#projectDep)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="e3cc4-147">Hello 응용 프로그램 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-147">Add hello application code</span></span>
<span data-ttu-id="e3cc4-148">세 가지 주요 부분은 toohello 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="e3cc4-149">Hello Azure Active Directory 토큰을 가져올</span><span class="sxs-lookup"><span data-stu-id="e3cc4-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="e3cc4-150">Hello 토큰 toocreate 데이터 레이크 저장소 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="e3cc4-151">데이터 레이크 저장소 클라이언트 tooperform 작업 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="e3cc4-152">1단계: Azure Active Directory 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="e3cc4-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="e3cc4-153">데이터 레이크 저장소 SDK hello hello 보안 토큰을 관리할 수 있는 편리한 방법이 필요 tootalk toohello Data Lake 저장소 계정이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="e3cc4-154">그러나 hello SDK는 이러한 방법만 사용할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="e3cc4-155">Hello를 사용 하 여 같은 토큰을 가져오는 다른 방법을 사용할 수 있습니다 [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), 또는 사용자 고유의 사용자 지정 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="e3cc4-156">toouse hello hello 앞에서 만든 Active Directory 웹 응용 프로그램에 대 한 데이터 레이크 저장소 SDK tooobtain 토큰의 hello 서브 클래스 중 하나를 사용 합니다. `AccessTokenProvider` (사용 하 여 아래 hello 예제 `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="e3cc4-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="e3cc4-157">메모리에 tooobtain hello 토큰을 사용 하 고 tooexpire에 대 한 hello 토큰을 자동으로 갱신 하는 hello 토큰 공급자 캐시 hello 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="e3cc4-158">가능한 toocreate의 고유한 하위 클래스는 `AccessTokenProvider` 고객 코드에 의해 토큰을 가져오는 하지만 지금은 보겠습니다 hello를 사용 하 여 방금 하나에 제공 된 hello SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="e3cc4-159">대체 **채우기 내부에서 여기** hello hello Azure Active Directory 웹 응용 프로그램에 대 한 실제 값으로.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="e3cc4-160">2단계: Azure Data Lake Store 클라이언트(ADLStoreClient) 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="e3cc4-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="e3cc4-161">만들기는 [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) 개체 toospecify hello Data Lake 저장소 계정 이름 및 hello 토큰 공급자 hello 마지막 단계에서 생성 된 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="e3cc4-162">Note 해당 hello Data Lake 저장소 계정 이름을 toobe 정규화 된 도메인 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="e3cc4-163">예를 들어 **FILL-IN-HERE**를 **mydatalakestore.azuredatalakestore.net**과 같은 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="e3cc4-164">3 단계: hello ADLStoreClient tooperform 파일 및 디렉터리 작업 사용</span><span class="sxs-lookup"><span data-stu-id="e3cc4-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="e3cc4-165">hello 코드 아래에 몇 가지 일반적인 작업의 예제 코드 조각을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="e3cc4-166">전체 hello 볼 수 있습니다 [데이터 레이크 저장소 Java SDK API 문서](https://azure.github.io/azure-data-lake-store-java/javadoc/) 의 hello **ADLStoreClient** toosee 다른 작업 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="e3cc4-167">표준 Java 스트림을 사용하여 파일을 읽고 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="e3cc4-168">즉, 모든 데이터 레이크 저장소에서 표준 Java 기능 (예: 인쇄 스트림 출력 형식은 또는 추가 기능에 대 한 hello 압축 또는 암호화 스트림을 toobenefit 스트리밍하 hello 위에 hello Java 스트림을 계층화 할 수 있습니다. top, 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="e3cc4-169">4 단계: 빌드 및 hello 응용 프로그램을 실행</span><span class="sxs-lookup"><span data-stu-id="e3cc4-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="e3cc4-170">IDE 내에서 toorun 찾아 hello 키를 눌러 **실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="e3cc4-171">Maven에서 사용 하 여에서 toorun [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="e3cc4-172">실행할 수 있는 명령줄 빌드 hello jar에서 포함 된 모든 종속성이 있는 hello를 사용 하 여 독립 실행형 jar tooproduce [Maven 어셈블리 플러그 인](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="e3cc4-173">hello에 pom.xml hello [github의 소스 코드 예제에서는](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) 방법의 예로 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3cc4-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3cc4-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3cc4-174">Next steps</span></span>
* [<span data-ttu-id="e3cc4-175">JavaDoc hello Java SDK에 대 한 탐색</span><span class="sxs-lookup"><span data-stu-id="e3cc4-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="e3cc4-176">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="e3cc4-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="e3cc4-177">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="e3cc4-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e3cc4-178">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="e3cc4-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

