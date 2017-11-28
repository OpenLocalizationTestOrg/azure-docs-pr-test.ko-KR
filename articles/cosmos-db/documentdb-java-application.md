---
title: "Azure Cosmos DB를 사용 하 여 aaaJava 응용 프로그램 개발 자습서 | Microsoft Docs"
description: "이 Java 웹 응용 프로그램 자습서 toouse를 Azure Cosmos DB hello 및 DocumentDB API toostore hello 및 Azure 웹 사이트에서 호스팅되는 Java 응용 프로그램에서 데이터 액세스 방법을 보여 줍니다."
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
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="0a69f-104">Azure Cosmos DB 및 hello DocumentDB API를 사용 하는 Java 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="0a69f-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a69f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0a69f-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="0a69f-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0a69f-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="0a69f-107">Java</span><span class="sxs-lookup"><span data-stu-id="0a69f-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="0a69f-108">Python</span><span class="sxs-lookup"><span data-stu-id="0a69f-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="0a69f-109">이 Java 웹 응용 프로그램 자습서에서는 어떻게 toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) toostore 및 액세스 데이터를 Azure 앱 서비스 웹 앱에서 호스트 되는 Java 응용 프로그램에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="0a69f-110">이 항목에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="0a69f-111">어떻게 toobuild Eclipse에서 기본 JavaServer 페이지 (JSP) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="0a69f-112">Hello Azure Cosmos DB로 toowork hello를 사용 하 여 서비스 어떻게 [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="0a69f-113">Java 응용 프로그램에 대해 설명 방식과 toocreate 있습니다, 검색, 및 표시 수 있는 웹 기반 toocreate 작업 관리 응용 프로그램 작업 완료 상태로 hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="0a69f-114">각 hello 작업 hello 할 일 목록에는 Azure Cosmos DB에서 JSON 문서도 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![My ToDo List Java 응용 프로그램](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="0a69f-116">이 응용 프로그램 개발 자습서에서는 이전에 Java를 사용한 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="0a69f-117">새 tooJava 또는 hello [필수 구성 요소 도구](#Prerequisites), 전체 hello를 다운로드 하는 것이 좋습니다 [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) 를 GitHub를 사용 하 여 프로젝트 [hello hello 끝이에 대 한 지침 문서](#GetProject)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="0a69f-118">작성 된, 일단 hello 프로젝트의 hello 컨텍스트에서 hello 코드에 hello 문서 toogain 대 한 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="0a69f-119"><a id="Prerequisites"></a>이 Java 웹 응용 프로그램 자습서의 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0a69f-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="0a69f-120">이 응용 프로그램 개발 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="0a69f-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="0a69f-121">An active Azure account.</span></span> <span data-ttu-id="0a69f-122">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0a69f-123">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="0a69f-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="0a69f-124">또는</span><span class="sxs-lookup"><span data-stu-id="0a69f-124">OR</span></span>

    <span data-ttu-id="0a69f-125">Hello의 로컬 설치 [Azure Cosmos DB 에뮬레이터](local-emulator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="0a69f-126">[JDK(Java Development Kit) 7 이상](http://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="0a69f-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="0a69f-127">Eclipse IDE for Java EE Developers</span><span class="sxs-lookup"><span data-stu-id="0a69f-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="0a69f-128">Java 런타임 환경(예: Tomcat 또는 Jetty)을 사용하는 Azure 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="0a69f-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="0a69f-129">이러한 도구 hello에 대 한 처음으로 설치 하는 경우 coreservlets.com의 hello 빠른 시작 섹션에 hello 설치 프로세스의 단계를 제공 하는 해당 [자습서: TomCat7 설치 및 사용 하 여 Eclipse와](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) 문서.</span><span class="sxs-lookup"><span data-stu-id="0a69f-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="0a69f-130"><a id="CreateDB"></a>1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0a69f-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="0a69f-131">Azure Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="0a69f-132">계정이 이미 없거나 사용 중인 경우이 자습서에 대 한 Azure Cosmos DB 에뮬레이터 hello 건너뛰어도 너무[2 단계: hello Java JSP 응용 프로그램 만들기](#CreateJSP)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="0a69f-133"><a id="CreateJSP"></a>2 단계: hello Java JSP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0a69f-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="0a69f-134">toocreate hello JSP 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="0a69f-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="0a69f-135">먼저, Java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="0a69f-136">Eclipse를 시작한 후 **파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="0a69f-137">표시 되지 않으면 **동적 웹 프로젝트** 다음 hello 않는 사용 가능한 프로젝트로 표시: 클릭 **파일**, 클릭 **새로**, 클릭 **프로젝트**..., 확장 **웹**, 클릭 **동적 웹 프로젝트**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java 응용 프로그램 개발](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="0a69f-139">Hello에 프로젝트 이름을 입력 **프로젝트 이름** 상자 및 hello **대상 런타임** 드롭 다운 메뉴에서 필요에 따라 (예:: Apache Tomcat v7.0) 값을 선택 하 고 클릭 **마침**.</span><span class="sxs-lookup"><span data-stu-id="0a69f-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="0a69f-140">대상 런타임을 선택 하면 Eclipse 통해 로컬 프로젝트 있습니다 toorun 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="0a69f-141">Eclipse에서 hello 프로젝트 탐색기 보기에서 프로젝트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="0a69f-142">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="0a69f-143">Hello에 **JSP 파일 새로** 대화 상자, 이름 hello 파일 **index.jsp**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="0a69f-144">Hello 상위 폴더를 유지 **WebContent**클릭 하 고 다음 그림에서는 hello에 나타난 것 처럼 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![새 JSP 파일 만들기 - Java 웹 응용 프로그램 자습서](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="0a69f-146">Hello에 **JSP 템플릿 선택** 대화 상자에서이 자습서 select hello 목적을 위해 **새 JSP 파일 (html)**, 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="0a69f-147">Eclipse에서 index.jsp 파일이 hello를 열면 텍스트 toodisplay 추가 **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="0a69f-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="0a69f-148">hello 기존 내 <body> 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-148">within hello existing <body> element.</span></span> <span data-ttu-id="0a69f-149">업데이트 한 후 <body> 콘텐츠 코드 다음 hello 같아야 합니다.:</span><span class="sxs-lookup"><span data-stu-id="0a69f-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="0a69f-150">Hello index.jsp 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="0a69f-151">2 단계에서 대상 런타임을 설정 하는 경우 클릭할 수 있는 **프로젝트** 차례로 **실행** toorun 로컬로 JSP 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="0a69f-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World - Java 응용 프로그램 자습서](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="0a69f-153"><a id="InstallSDK"></a>3 단계: hello DocumentDB Java SDK 설치</span><span class="sxs-lookup"><span data-stu-id="0a69f-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="0a69f-154">hello hello DocumentDB Java SDK 및 해당 종속성에 가장 쉬운 방법은 toopull 방식은 [Apache Maven](http://maven.apache.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="0a69f-155">toodo이 hello 다음 단계를 완료 하 여 프로젝트 tooa maven 프로젝트가 tooconvert를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="0a69f-156">Hello 프로젝트 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 여, **구성**, 클릭 **tooMaven 프로젝트 변환**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="0a69f-157">Hello에 **새 POM 만들** 창의 hello 기본값을 적용 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="0a69f-158">**프로젝트 탐색기**열고 hello pom.xml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="0a69f-159">Hello에 **종속성** 탭 hello **종속성** 창에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="0a69f-160">Hello에 **선택 종속성** 창에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="0a69f-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="0a69f-161">Hello에 **그룹 Id** 상자 com.microsoft.azure를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="0a69f-162">Hello에 **아티팩트 Id** 상자에 azure documentdb를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="0a69f-163">Hello에 **버전** 상자 1.5.1를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![DocumentDB Java 응용 프로그램 SDK 설치](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="0a69f-165">그룹 Id 및 아티팩트 Id에 대 한 hello 종속성 XML을 추가 또는 텍스트 편집기를 통해 직접 toohello pom.xml:</span><span class="sxs-lookup"><span data-stu-id="0a69f-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="0a69f-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="0a69f-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="0a69f-167">클릭 **확인** Maven hello DocumentDB Java SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="0a69f-168">Hello pom.xml 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="0a69f-169"><a id="UseService"></a>4 단계: hello Azure Cosmos DB 서비스를 사용 하 여 Java 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="0a69f-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="0a69f-170">첫째, 보겠습니다 TodoItem.java의 hello TodoItem 개체를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="0a69f-171">이 프로젝트를 사용 하 여 [프로젝트 Lombok](http://projectlombok.org/) toogenerate hello 생성자, getter, setter 및 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="0a69f-172">이 코드를 수동으로 작성 또는 있을 수 있습니다 또는 IDE hello 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="0a69f-173">tooinvoke hello Azure Cosmos DB 서비스를 인스턴스화해야 새 **DocumentClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="0a69f-174">가장 좋은 tooreuse hello 일반적으로 **DocumentClient** -대신 보다 각각의 후속 요청에 대 한 새 클라이언트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="0a69f-175">Hello 클라이언트에 래핑하여 hello 클라이언트를 다시 사용할 수 있습니다는 **DocumentClientFactory**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="0a69f-176">Toopaste hello URI 및 기본 키 값 tooyour 클립보드에 저장 해야 DocumentClientFactory.java, [1 단계](#CreateDB)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="0a69f-177">[YOUR\_ENDPOINT\_HERE]를 해당 URI로 바꾸고 [YOUR\_KEY\_HERE]를 해당 기본 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="0a69f-178">이제 할 일 항목 tooAzure Cosmos DB 우리의 유지 개체 DAO (Data Access) tooabstract를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="0a69f-179">순서로 toosave 할 일 항목 tooa 컬렉션, hello 클라이언트 필요한 tooknow 어떤 데이터베이스 및 컬렉션 toopersist 너무 (에서 참조 하므로 자체 링크)입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="0a69f-180">일반적으로 최상의 toocache hello 데이터베이스와 가능한 경우 컬렉션은 tooavoid 추가 왕복 toohello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="0a69f-181">hello 다음 코드에서는 어떻게 tooretrieve 우리의 데이터베이스 및 컬렉션, 존재 하거나 존재 하지 않는 경우 새 필터를 만들 경우:</span><span class="sxs-lookup"><span data-stu-id="0a69f-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="0a69f-182">hello 다음 단계는 toowrite toohello 컬렉션에 있는 일부 코드 toopersist hello TodoItems 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="0a69f-183">이 예제에서는 사용 [Gson](https://code.google.com/p/google-gson/) tooserialize TodoItem 이전 일반 Java 개체 (POJOs) tooJSON 문서를 역직렬화 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="0a69f-184">Azure Cosmos DB 데이터베이스 및 컬렉션과 마찬가지로 문서도 셀프 link로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="0a69f-185">자체 링크 하지 않고 hello 도우미 함수 사용 하면 다음 us 검색 문서 다른 특성 (예: "id"):</span><span class="sxs-lookup"><span data-stu-id="0a69f-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
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
6. <span data-ttu-id="0a69f-186">다음 tooa POJO deserialize를 id 별로 5 단계 tooretrieve TodoItem JSON 문서 hello 도우미 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="0a69f-187">또한 hello DocumentClient tooget 컬렉션 또는 TodoItems DocumentDB SQL을 사용 하 여 목록을 사용할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="0a69f-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="0a69f-188">Hello DocumentClient 사용 하 여 문서를 여러 방법으로 tooupdate가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="0a69f-189">할 일 목록 응용 프로그램에서는 완료 된 TodoItem 인지 toobe 수 tootoggle를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="0a69f-190">Hello hello 문서 내에서 "전체" 특성을 업데이트 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="0a69f-191">목록에서 hello 기능 toodelete a TodoItem을 마지막으로, 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="0a69f-192">toodo이를 이전에 작성 하는 hello 도우미 메서드를 사용할 수 있습니다 tooretrieve 자체 링크 hello 고 hello 클라이언트 toodelete 하기:</span><span class="sxs-lookup"><span data-stu-id="0a69f-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="0a69f-193"><a id="Wire"></a>5 단계: hello hello Java 응용 프로그램 개발 프로젝트의 나머지를 함께 연결</span><span class="sxs-lookup"><span data-stu-id="0a69f-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="0a69f-194">이전 읽었으면 hello 재미 했으므로 비트-즉는 toobuild 빠른 사용자 인터페이스 및 DAO tooour를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="0a69f-195">먼저,이 DAO 컨트롤러 toocall 작성 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-195">First, let's start with building a controller toocall our DAO:</span></span>
   
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
   
    <span data-ttu-id="0a69f-196">더 복잡 한 응용 프로그램에서는 hello 컨트롤러 hello DAO 기반으로 복잡 한 비즈니스 논리를 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="0a69f-197">다음으로 servlet tooroute HTTP 요청 toohello 컨트롤러를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
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
3. <span data-ttu-id="0a69f-198">웹 사용자 인터페이스 toodisplay toohello 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="0a69f-199">다시 작성해 보겠습니다 hello index.jsp 앞에서 만든:</span><span class="sxs-lookup"><span data-stu-id="0a69f-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
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
   
            <!-- hello ToDo List -->
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
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="0a69f-200">마지막으로 일부 클라이언트 쪽 JavaScript tootie hello 웹 사용자 인터페이스를 작성 하 고 함께 servlet hello:</span><span class="sxs-lookup"><span data-stu-id="0a69f-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
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
   
              // Call api tooupdate todo items.
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
           * Install hello TodoApp
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
5. <span data-ttu-id="0a69f-201">멋집니다!</span><span class="sxs-lookup"><span data-stu-id="0a69f-201">Awesome!</span></span> <span data-ttu-id="0a69f-202">이제 tootest hello 응용 프로그램은 남았습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="0a69f-203">Hello 응용 프로그램을 로컬로 실행 하 고 hello 항목 이름 및 범주를 입력 하 고 클릭 하 여 일부 할 일 항목 추가 **작업 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="0a69f-204">완료 되 면 hello 확인란을 설정/해제 하 고 클릭 하 여 여부를 업데이트할 수 hello 항목 표시 될 때 **작업 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="0a69f-205"><a id="Deploy"></a>6 단계: Java 응용 프로그램 tooAzure 웹 사이트 배포</span><span class="sxs-lookup"><span data-stu-id="0a69f-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="0a69f-206">Azure 웹 사이트에서는 Java 응용 프로그램을 간단히 배포할 수 있습니다. 즉, 응용 프로그램을 WAR 파일로 내보내고 소스 제어(예: Git) 또는 FTP를 통해 업로드하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="0a69f-207">tooexport WAR 파일으로 응용 프로그램에서 프로젝트에서 마우스 오른쪽 단추로 **프로젝트 탐색기**, 클릭 **내보내기**, 클릭 하 고 **WAR 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="0a69f-208">Hello에 **WAR 내보내기** 창에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="0a69f-209">Documentdb java 샘플 azure hello 웹 프로젝트 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="0a69f-210">Hello 대상 상자 대상 toosave hello WAR 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="0a69f-211">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-211">Click **Finish**.</span></span>
3. <span data-ttu-id="0a69f-212">WAR 파일을 맡은 단순히 업로드 tooyour Azure 웹 사이트의 **webapps** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="0a69f-213">Hello 파일 업로드에 대 한 지침을 참조 하십시오. [Java 응용 프로그램 tooAzure 앱 서비스 웹 앱 추가](../app-service-web/web-sites-java-add-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="0a69f-214">Hello WAR 파일 업로드 toohello webapps 디렉터리를 추가 했으므로 하 고 자동으로 로드 합니다 hello 런타임 환경을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="0a69f-215">tooview 완성 된 제품을 toohttp://YOUR 이동\_사이트\_NAME.azurewebsites.net/azure-java-sample/ 및 작업 추가 시작!</span><span class="sxs-lookup"><span data-stu-id="0a69f-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="0a69f-216"><a id="GetProject"></a>GitHub에서 hello 프로젝트 가져오기</span><span class="sxs-lookup"><span data-stu-id="0a69f-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="0a69f-217">이 자습서에서는 모든 hello 샘플 hello에 포함 된 [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) GitHub에 대 한 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="0a69f-218">Eclipse에 tooimport hello todo 프로젝트 hello 소프트웨어 및 hello에 나열 된 리소스는 확인 [필수 구성 요소](#Prerequisites) 섹션에서 다음 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="0a69f-219">[Project Lombok](http://projectlombok.org/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="0a69f-220">Lombok 사용 되는 toogenerate 생성자, getter, setter hello 프로젝트에서입니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="0a69f-221">Hello lombok.jar 파일을 다운로드 한 후 두 번 클릭 tooinstall 것 하거나 hello 명령줄에서 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="0a69f-222">Eclipse 열려 있으면 닫고 tooload Lombok 다시 시작.</span><span class="sxs-lookup"><span data-stu-id="0a69f-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="0a69f-223">Hello에 Eclipse에서 **파일** 메뉴를 클릭 하 여 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="0a69f-224">Hello에 **가져오기** 창 클릭 **Git**, 클릭 **프로젝트에서 Git**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="0a69f-225">Hello에 **리포지토리 원본 선택** 화면 **복제 URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="0a69f-226">Hello에 **소스 Git 리포지토리에** 화면의 hello에 **URI** 상자 https://github.com/Azure-Samples/java-todo-app.git, 입력 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="0a69f-227">Hello에 **분기 선택** 화면에서 **마스터** 을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="0a69f-228">Hello에 **로컬 대상** 화면 **찾아보기** tooselect 여기 hello 리포지토리를 복사할 수 있습니다 하 한 다음 클릭 폴더 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="0a69f-229">Hello에 **프로젝트 가져오기 마법사 toouse 선택** 화면에서 **기존 프로젝트를 가져올** 을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="0a69f-230">Hello에 **가져오기 프로젝트** 화면, 선택을 취소 hello **DocumentDB** 프로젝트를 마우스 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="0a69f-231">hello DocumentDB 프로젝트에 hello Azure Cosmos DB Java SDK 대신 종속성으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="0a69f-232">**프로젝트 탐색기**tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java 이동한 hello URI 및 기본 키를 사용 하 여 hello 호스트와 MASTER_KEY 값을 대체 합니다. Cosmos DB Azure 계정, 및 다음 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="0a69f-233">자세한 내용은 [1단계를 참조하세요. Azure Cosmos DB 데이터베이스 계정 만들기](#CreateDB)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a69f-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="0a69f-234">**프로젝트 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **azure documentdb-java 샘플**, 클릭 **빌드 경로**, 클릭 하 고 **빌드 경로 구성**.</span><span class="sxs-lookup"><span data-stu-id="0a69f-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="0a69f-235">Hello에 **Java 빌드 경로** hello 오른쪽 창에서 선택 hello 화면 **라이브러리** 탭을 클릭 한 다음 **외부 단지 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="0a69f-236">Toohello hello lombok.jar 파일 위치를 찾아서 클릭 **열려**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="0a69f-237">사용 하 여 12 단계 tooopen hello **속성** 에 창 hello 왼쪽된 창에서 다음을 클릭 하 고 **대상으로 하는 런타임**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="0a69f-238">Hello에 **대상으로 하는 런타임** 화면에서 **새로**을 선택 **Apache Tomcat v7.0**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="0a69f-239">사용 하 여 12 단계 tooopen hello **속성** 에 창 hello 왼쪽된 창에서 다음을 클릭 하 고 **프로젝트 패싯**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="0a69f-240">Hello에 **프로젝트 패싯** 화면에서 **동적 웹 모듈** 및 **Java**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="0a69f-241">Hello에 **서버** hello hello 화면 맨 아래에 탭을 마우스 오른쪽 단추로 클릭 **Tomcat 서버 로컬 호스트에 v7.0** 클릭 하 고 **추가 및 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="0a69f-242">Hello에 **추가 및 제거** 창 이동 **azure documentdb-java 샘플** toohello **자동 구성** 상자를 선택한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="0a69f-243">Hello에 **서버** 탭을 마우스 오른쪽 단추로 클릭 **Tomcat 서버 로컬 호스트에 v7.0**, 클릭 하 고 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="0a69f-244">브라우저에서 탐색 toohttp://localhost:8080 / azure documentdb-java 샘플 / tooyour 작업 목록에 추가 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="0a69f-245">기본 포트 값을 변경한 경우 선택한 8080 toohello 값을 변경 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="0a69f-246">toodeploy 프로그램 프로젝트 tooan Azure 웹 사이트 참조 [6 단계. 웹 사이트에 응용 프로그램 tooAzure 배포](#Deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a69f-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
