---
title: "Azure Cosmos DB를 사용한 Java 응용 프로그램 개발 자습서 | Microsoft Docs"
description: "이 Java 웹 응용 프로그램 자습서에서는 Azure Cosmos DB 및 DocumentDB API를 사용하여 Azure Websites에 호스트된 Java 응용 프로그램에서 데이터를 저장하고 액세스하는 방법을 보여 줍니다."
keywords: "응용 프로그램 개발, 데이터베이스 자습서, java 응용 프로그램, java 웹 응용 프로그램 자습서, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="03a94-104">Azure Cosmos DB 및 DocumentDB API를 사용하여 Java 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="03a94-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03a94-105">.NET</span><span class="sxs-lookup"><span data-stu-id="03a94-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="03a94-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="03a94-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="03a94-107">Java</span><span class="sxs-lookup"><span data-stu-id="03a94-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="03a94-108">Python</span><span class="sxs-lookup"><span data-stu-id="03a94-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="03a94-109">이 Java 웹 응용 프로그램 자습서에서는 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스를 사용하여 Azure App Service Web Apps에 호스트된 Java 응용 프로그램에서 데이터를 저장하고 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="03a94-110">이 항목에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="03a94-111">Eclipse에서 기본 JSP(JavaServer Pages) 응용 프로그램을 빌드하는 방법.</span><span class="sxs-lookup"><span data-stu-id="03a94-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="03a94-112">[Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java)를 사용하여 Azure Cosmos DB 서비스로 작업하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="03a94-113">이 Java 응용 프로그램 자습서에서는 다음 이미지에 표시된 것처럼 작업을 생성 및 검색하고 완료로 표시할 수 있게 해주는 웹 기반 작업 관리 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="03a94-114">할 일 목록에 있는 각 작업은 Azure Cosmos DB에서 JSON 문서로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![My ToDo List Java 응용 프로그램](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="03a94-116">이 응용 프로그램 개발 자습서에서는 이전에 Java를 사용한 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="03a94-117">Java 또는 [필수 구성 요소 도구](#Prerequisites)를 처음 사용하는 경우 GitHub에서 전체 [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) 프로젝트를 다운로드하고 [이 문서의 끝에 있는 지침](#GetProject)을 사용하여 이 프로젝트를 빌드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="03a94-118">프로젝트를 빌드하고 나면 이 문서를 검토하여 프로젝트의 컨텍스트에서 코드를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="03a94-119"><a id="Prerequisites"></a>이 Java 웹 응용 프로그램 자습서의 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="03a94-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="03a94-120">이 응용 프로그램 개발 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="03a94-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="03a94-121">An active Azure account.</span></span> <span data-ttu-id="03a94-122">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="03a94-123">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="03a94-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="03a94-124">또는</span><span class="sxs-lookup"><span data-stu-id="03a94-124">OR</span></span>

    <span data-ttu-id="03a94-125">[Azure Cosmos DB 에뮬레이터](local-emulator.md)의 로컬 설치</span><span class="sxs-lookup"><span data-stu-id="03a94-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="03a94-126">[JDK(Java Development Kit) 7 이상](http://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="03a94-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="03a94-127">Eclipse IDE for Java EE Developers</span><span class="sxs-lookup"><span data-stu-id="03a94-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="03a94-128">Java 런타임 환경(예: Tomcat 또는 Jetty)을 사용하는 Azure 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="03a94-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="03a94-129">이러한 도구를 처음 설치하는 경우, coreservlets.com에서 제공되는 단계별 설치 지침을 따르세요. 이 지침은 [자습서: TomCat7 설치 및 Eclipse에서 사용](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) 문서의 빠른 시작 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="03a94-130"><a id="CreateDB"></a>1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="03a94-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="03a94-131">Azure Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="03a94-132">계정이 있거나 이 자습서에 Azure Cosmos DB 에뮬레이터를 사용하고 있는 경우 [2단계: Java JSP 응용 프로그램 만들기](#CreateJSP)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="03a94-133"><a id="CreateJSP"></a>2단계: Java JSP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="03a94-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="03a94-134">JSP 응용 프로그램을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-134">To create the JSP application:</span></span>

1. <span data-ttu-id="03a94-135">먼저, Java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="03a94-136">Eclipse를 시작한 후 **파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="03a94-137">**동적 웹 프로젝트**가 사용 가능한 프로젝트로 나열되지 않았으면 다음을 수행합니다. **파일**, **새로 만들기**, **프로젝트**…를 차례로 클릭하고 **웹**을 확장한 후 **동적 웹 프로젝트**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java 응용 프로그램 개발](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="03a94-139">**프로젝트 이름** 상자에 프로젝트 이름을 입력하고 **대상 런타임** 드롭다운 메뉴에서 선택적으로 값(예: Apache Tomcat v7.0)을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="03a94-140">대상 런타임을 선택하면 Eclipse를 통해 프로젝트를 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="03a94-141">Eclipse의 Project Explorer 보기에서 프로젝트를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="03a94-142">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="03a94-143">**새 JSP 파일** 대화 상자에서 파일 이름을 **index.jsp**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="03a94-144">다음 그림에 표시된 것처럼 상위 폴더를 **WebContent**로 유지하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![새 JSP 파일 만들기 - Java 웹 응용 프로그램 자습서](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="03a94-146">**JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)**을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="03a94-147">index.jsp 파일이 Eclipse에서 열리면 **Hello World!**를 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="03a94-148">기존 <body> 요소 내.</span><span class="sxs-lookup"><span data-stu-id="03a94-148">within the existing <body> element.</span></span> <span data-ttu-id="03a94-149">업데이트된 <body> 콘텐츠는 다음 코드와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="03a94-150">index.jsp 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="03a94-151">2단계에서 대상 런타임을 설정했으면 **프로젝트**, **실행**을 차례로 클릭하여 JSP 응용 프로그램을 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World - Java 응용 프로그램 자습서](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="03a94-153"><a id="InstallSDK"></a>3단계: DocumentDB Java SDK 설치</span><span class="sxs-lookup"><span data-stu-id="03a94-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="03a94-154">DocumentDB Java SDK 및 해당 종속성을 가져오는 가장 쉬운 방법은 [Apache Maven](http://maven.apache.org/)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="03a94-155">이렇게 하려면 다음 단계를 수행해서 프로젝트를 maven 프로젝트로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="03a94-156">프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **구성**을 클릭한 후 **Maven 프로젝트로 변환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="03a94-157">**새 POM 만들기** 창에서 기본값을 수락하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="03a94-158">**프로젝트 탐색기**에서 pom.xml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="03a94-159">**종속성** 탭의 **종속성** 창에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="03a94-160">**종속성 선택** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="03a94-161">**그룹 ID** 상자에 com.microsoft.azure를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="03a94-162">**아티팩트 ID** 상자에 azure-documentdb를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="03a94-163">**버전** 상자에 1.5.1을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![DocumentDB Java 응용 프로그램 SDK 설치](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="03a94-165">또는 텍스트 편집기를 통해 Group ID 및 Artifact ID에 대한 종속성 XML을 pom.xml에 직접 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="03a94-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="03a94-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="03a94-167">**확인**을 클릭하면 Maven이 DocumentDB Java SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="03a94-168">pom.xml 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="03a94-169"><a id="UseService"></a>4단계: Java 응용 프로그램에서 Azure Cosmos DB 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="03a94-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="03a94-170">먼저 TodoItem.java에서 TodoItem 개체를 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="03a94-171">이 프로젝트에서는 [Project Lombok](http://projectlombok.org/) 을 사용해서 생성자, getter, setter 및 작성기를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="03a94-172">또는 이 코드를 수동으로 작성하거나 IDE에서 생성하도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="03a94-173">Azure Cosmos DB 서비스를 호출하려면 새 **DocumentClient**를 인스턴스화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="03a94-174">일반적으로 각 후속 요청에 대해 새 클라이언트를 생성하는 것보다는 **DocumentClient** 를 다시 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="03a94-175">**DocumentClientFactory**에 클라이언트를 래핑하면 클라이언트를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="03a94-176">DocumentClientFactory.java에서 [1단계](#CreateDB)에서 클립보드에 저장한 URI 및 기본 키 값을 붙여 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="03a94-177">[YOUR\_ENDPOINT\_HERE]를 해당 URI로 바꾸고 [YOUR\_KEY\_HERE]를 해당 기본 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="03a94-178">이제 DAO(Data Access Object)를 만들어서 영구적인 ToDo 항목을 Azure Cosmos DB로 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="03a94-179">ToDo 항목을 컬렉션에 저장하려면 클라이언트는 유지할 데이터베이스 및 컬렉션(셀프 link로 참조)을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="03a94-180">일반적으로 데이터베이스로의 추가 왕복을 방지할 수 있을 때 데이터베이스 및 컬렉션을 캐시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="03a94-181">다음 코드에서는 데이터베이스 및 컬렉션이 있는 경우 검색하고 없는 경우 새로 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="03a94-182">다음 단계에서는 TodoItems를 컬렉션에 저장하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="03a94-183">이 예제에서는 [Gson](https://code.google.com/p/google-gson/) 을 사용하여 TodoItem POJO(Plain Old Java Object)를 JSON 문서에 직렬화하고 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="03a94-184">Azure Cosmos DB 데이터베이스 및 컬렉션과 마찬가지로 문서도 셀프 link로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="03a94-185">다음 도우미 함수에서는 셀프 link가 아닌 다른 특성(예: "id")으로 문서를 검색해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="03a94-186">5단계의 도우미 메서드를 사용하여 ID로 TodoItem JSON 문서를 검색한 다음 POJO로 역직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="03a94-187">또한 DocumentClient를 사용하여 DocumentDB SQL을 사용하는 TodoItem의 컬렉션 또는 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="03a94-188">여러 가지 방법으로 DocumentClient가 포함된 문서를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="03a94-189">여기의 Todo 목록 응용 프로그램에서는 TodoItem이 완료되었는지 여부를 전환할 수 있게 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="03a94-190">이를 위해서는 문서 내에서 "complete" 특성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="03a94-191">끝으로, 목록에서 TodoItem을 삭제할 수 있는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="03a94-192">이를 위해 앞서 작성한 도우미 메서드를 사용하여 셀프 link를 검색한 다음 클라이언트에 삭제하도록 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="03a94-193"><a id="Wire"></a>5단계: Java 응용 프로그램 개발 프로젝트의 나머지 부분 연결</span><span class="sxs-lookup"><span data-stu-id="03a94-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="03a94-194">이제 재미있는 부분을 마쳤으므로 빠른 사용자 인터페이스를 빌드하고 DAO에 연결하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="03a94-195">먼저 DAO를 호출하는 컨트롤러를 빌드하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-195">First, let's start with building a controller to call our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="03a94-196">보다 복잡한 응용 프로그램에서는 컨트롤러에서 DAO 위에 복잡한 비즈니스 논리를 수용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="03a94-197">다음으로 컨트롤러에 HTTP 요청을 서블릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="03a94-198">사용자에게 표시할 웹 사용자 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="03a94-199">앞에서 만든 index.jsp를 다시 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- The ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="03a94-200">끝으로, 웹 사용자 인터페이스와 서블릿을 연결하는 클라이언트 쪽 JavaScript를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api to update todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install the TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="03a94-201">멋집니다!</span><span class="sxs-lookup"><span data-stu-id="03a94-201">Awesome!</span></span> <span data-ttu-id="03a94-202">이제 응용 프로그램을 테스트하는 일만 남았습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="03a94-203">응용 프로그램을 로컬로 실행하고 항목 이름과 범주를 입력하고 **작업 추가**를 클릭하여 Todo 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="03a94-204">항목이 표시되면 확인란을 설정/해제하고 **작업 업데이트**를 클릭하여 항목의 완료 여부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="03a94-205"><a id="Deploy"></a>6단계: Azure 웹 사이트에 Java 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="03a94-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="03a94-206">Azure 웹 사이트에서는 Java 응용 프로그램을 간단히 배포할 수 있습니다. 즉, 응용 프로그램을 WAR 파일로 내보내고 소스 제어(예: Git) 또는 FTP를 통해 업로드하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="03a94-207">응용 프로그램을 WAR 파일로 내보내려면 **프로젝트 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **내보내기**를 클릭한 후 **WAR 파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="03a94-208">**WAR 내보내기** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="03a94-209">웹 프로젝트 상자에 azure-documentdb-java-sample을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="03a94-210">대상 상자에서 WAR 파일을 저장할 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="03a94-211">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-211">Click **Finish**.</span></span>
3. <span data-ttu-id="03a94-212">이제 WAR 파일이 준비되었으므로 간단히 Azure 웹 사이트의 **webapps** 디렉터리로 업로드하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="03a94-213">파일 업로드에 대한 자세한 내용은 [Azure App Service Web Apps에 Java 응용 프로그램 추가](../app-service-web/web-sites-java-add-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03a94-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="03a94-214">WAR 파일이 webapps 디렉터리에 업로드되면 런타임 환경에서 이 파일이 추가되었음을 감지하고 자동으로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="03a94-215">완료된 제품을 보려면 http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/로 이동하고 작업 추가를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="03a94-216"><a id="GetProject"></a>GitHub에서 프로젝트 가져오기</span><span class="sxs-lookup"><span data-stu-id="03a94-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="03a94-217">이 자습서의 모든 샘플은 GitHub의 [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) 프로젝트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="03a94-218">Todo 프로젝트를 Eclipse로 가져오려면 [필수 조건](#Prerequisites) 섹션에 나열된 소프트웨어 및 리소스가 있는지 확인한 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="03a94-219">[Project Lombok](http://projectlombok.org/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="03a94-220">Lombok은 프로젝트에서 생성자, getter, setter를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="03a94-221">lombok.jar 파일을 다운로드한 다음에는 두 번 클릭하여 설치하거나 명령줄을 사용해서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="03a94-222">Eclipse가 열려 있으면 닫고 다시 시작해서 Lombok을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="03a94-223">Eclipse의 **파일** 메뉴에서 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="03a94-224">**가져오기** 창에서 **Git**, **Git의 프로젝트**, **다음**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="03a94-225">**리포지토리 원본 선택** 화면에서 **URI 복제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="03a94-226">**원본 Git 리포지토리** 화면의 **URI** 상자에 https://github.com/Azure-Samples/java-todo-app.git을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="03a94-227">**분기 선택** 화면에서 **마스터**가 선택되었는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="03a94-228">**로컬 대상** 화면에서 **찾아보기**를 클릭하여 리포지토리를 복사할 수 있는 폴더를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="03a94-229">**프로젝트 가져오기에 사용할 마법사 선택** 화면에서 **기존 프로젝트 가져오기**가 선택되었는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="03a94-230">**프로젝트 가져오기** 화면에서 **DocumentDB** 프로젝트를 선택 취소한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="03a94-231">DocumentDB 프로젝트에는 종속성으로 추가할 Azure Cosmos DB Java SDK가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="03a94-232">**프로젝트 탐색기**에서 azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java로 이동하고 HOST 및 MASTER_KEY 값을 각각 해당 Azure Cosmos DB 계정의 URI 및 기본 키로 바꾸고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="03a94-233">자세한 내용은 [1단계를 참조하세요. Azure Cosmos DB 데이터베이스 계정 만들기](#CreateDB)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03a94-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="03a94-234">**프로젝트 탐색기**에서 **azure-documentdb-java-sample**을 마우스 오른쪽 단추로 클릭하고 **빌드 경로**를 클릭한 후 **빌드 경로 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="03a94-235">**Java 빌드 경로** 화면의 오른쪽 창에서 **라이브러리** 탭을 선택한 후 **외부 JAR 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="03a94-236">lombok.jar 파일의 위치로 이동하고 **열기**를 클릭한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="03a94-237">12단계를 수행해서 **속성** 창을 다시 열고 왼쪽 창에서 **대상 런타임**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="03a94-238">**대상 런타임** 화면에서 **새로 만들기**를 클릭하고 **Apache Tomcat v7.0**을 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="03a94-239">12단계를 수행해서 **속성** 창을 다시 열고 왼쪽 창에서 **프로젝트 패싯**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="03a94-240">**프로젝트 패싯** 화면에서 **동적 웹 모듈** 및 **Java**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="03a94-241">화면 하단에 있는 **서버** 탭에서 **로컬 호스트의 Tomcat v7.0 서버**를 마우스 오른쪽 단추로 클릭하고 **추가 및 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="03a94-242">**추가 및 제거** 창에서 **azure-documentdb-java-sample**을 **구성됨** 상자로 이동하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="03a94-243">**서버** 탭에서 **로컬 호스트의 Tomcat v7.0 서버**를 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="03a94-244">브라우저에서 http://localhost:8080/azure-documentdb-java-sample/로 이동하고 작업 목록에 추가를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="03a94-245">기본 포트 값을 변경한 경우 8080을 선택한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="03a94-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="03a94-246">프로젝트를 Azure 웹 사이트에 배포하려면 [6단계. Azure 웹 사이트에 응용 프로그램 배포](#Deploy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03a94-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
