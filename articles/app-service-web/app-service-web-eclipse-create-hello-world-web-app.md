---
title: "사용 하 여 기본 Azure 웹 앱 aaaCreate Eclipse | Microsoft Docs"
description: "이 자습서에서는 어떻게 toouse hello Azure 도구 키트에 Eclipse toocreate Azure 용 Hello World 웹 응용 프로그램입니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="f7f95-103">Eclipse를 사용하여 기본 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="f7f95-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="f7f95-104">이 자습서에서는 어떻게 toocreate hello를 사용 하 여 기본 Hello World 응용 프로그램 tooAzure 웹 앱으로 배포 및 [Azure Toolkit for Eclipse]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="f7f95-105">기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한, 유사한 단계는 Java 서블릿에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="f7f95-106">이 자습서를 완료 하는 경우 비슷한 toohello 웹 브라우저에서 볼 때 그림을 다음 응용 프로그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][01]

## <a name="prerequisites"></a><span data-ttu-id="f7f95-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7f95-108">Prerequisites</span></span>
* <span data-ttu-id="f7f95-109">JDK(Java 개발자 키트), v 1.8 이상.</span><span class="sxs-lookup"><span data-stu-id="f7f95-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="f7f95-110">Eclipse IDE for Java EE Developers, Luna 이상.</span><span class="sxs-lookup"><span data-stu-id="f7f95-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="f7f95-111"><http://www.eclipse.org/downloads/>에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="f7f95-112">Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: [Apache Tomcat] 또는 [Jetty])</span><span class="sxs-lookup"><span data-stu-id="f7f95-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="f7f95-113">Azure 구독은 <https://azure.microsoft.com/free/> 또는 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="f7f95-114">hello [Azure Toolkit for Eclipse]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="f7f95-115">Hello Azure 도구 키트를 설치 하는 방법에 대 한 정보를 참조 하십시오. [Azure Toolkit for Eclipse 설치 hello]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="f7f95-116">toocreate Hello World 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="f7f95-116">toocreate a Hello World application</span></span>
<span data-ttu-id="f7f95-117">먼저 java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="f7f95-118">Eclipse를 시작 하 고 hello 메뉴 **파일**, 클릭 **새로**, 클릭 하 고 **동적 웹 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="f7f95-119">(표시 되지 않으면 **동적 웹 프로젝트** 클릭 한 후 사용 가능한 프로젝트로 표시 **파일** 및 **새로**, 수행가 다음를 hello 다음: 클릭 **파일**, 클릭 **새로**, 클릭 **프로젝트...** 를 확장 하 고 **웹**, 클릭 **동적 웹 프로젝트**를 클릭 하 고 **다음**.)</span><span class="sxs-lookup"><span data-stu-id="f7f95-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="f7f95-120">이 자습서에서는 이름을 hello 프로젝트 **MyWebApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="f7f95-121">화면에는 비슷한 toohello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-121">Your screen will appear similar toohello following:</span></span>
   
    ![새로운 동적 웹 프로젝트 만들기][02]
3. <span data-ttu-id="f7f95-123">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-123">Click **Finish**.</span></span>
4. <span data-ttu-id="f7f95-124">Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="f7f95-125">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="f7f95-126">Hello에 **JSP 파일 새로** 대화 상자, 이름 hello 파일 **index.jsp**, hello 상위 폴더를 유지 **MyWebApp/WebContent**, 클릭 하 고 **다음**.</span><span class="sxs-lookup"><span data-stu-id="f7f95-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="f7f95-127">Hello에 **JSP 템플릿 선택** 대화 상자에서이 자습서 선택의 목적을 위해 **새 JSP 파일 (html)**, 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="f7f95-128">Eclipse에서 index.jsp 파일이 열리면 텍스트 toodynamically 디스플레이에서 추가 **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="f7f95-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="f7f95-129">hello 기존 내 `<body>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="f7f95-130">업데이트 한 후 `<body>` 콘텐츠 hello 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="f7f95-131">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="f7f95-132">toodeploy 프로그램 응용 프로그램 tooan Azure 웹 응용 프로그램 컨테이너</span><span class="sxs-lookup"><span data-stu-id="f7f95-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="f7f95-133">여러 가지 방법으로 여는 Java 웹 응용 프로그램 tooAzure를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="f7f95-134">이 자습서에서는 가장 간단한 hello 중 하나를 설명: 응용 프로그램에 배포 된 Azure 웹 응용 프로그램 컨테이너 tooan 됩니다-특수 프로젝트 형식 이나 추가 도구 없는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="f7f95-135">hello JDK 및 hello 웹 컨테이너 소프트웨어는 사용자에 게 제공 Azure에서 이므로 없습니다 필요 tooupload 고유한; 하기만 하면 Java 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="f7f95-136">결과적으로, 응용 프로그램에 대 한 게시 프로세스 hello 초, 분 하지 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="f7f95-137">Eclipse의 프로젝트 탐색기에서 **MyWebApp**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="f7f95-138">Hello 상황에 맞는 메뉴에서 선택 **Azure**, 클릭 **Azure 웹 앱으로 게시 중...**</span><span class="sxs-lookup"><span data-stu-id="f7f95-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Azure 웹앱으로 게시][03]
   
    <span data-ttu-id="f7f95-140">또는 hello 프로젝트 탐색기에서에서 웹 응용 프로그램 프로젝트를 선택한 상태에서 클릭할 수 있는 hello **게시** hello 도구 모음을 선택 드롭다운 단추 **Azure 웹 앱으로 게시** 여기에서:</span><span class="sxs-lookup"><span data-stu-id="f7f95-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Azure 웹앱으로 게시][14]
3. <span data-ttu-id="f7f95-142">아직 Eclipse에서 Azure에 등록 하지 않은 경우에 Azure 계정에 증명된 toosign를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Azure 로그인 대화 상자][04]
   
    <span data-ttu-id="f7f95-144">있으면 여러 Azure 계정에 로그인 하는 hello 프롬프트 hello 하는 동안 일부 프로세스 표시 될 수 있습니다 두 번 이상 toobe 나타나는 경우에 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="f7f95-145">이 지침에 설명 된 hello 기호 다음 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="f7f95-146">Azure 계정에 성공적으로 로그인을 한 후 hello **구독 관리** 대화 상자에 자격 증명으로 연결 된 구독 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="f7f95-147">나열 된 여러 구독이 있는 경우 그 중 특정 하위 집합만 toowork toouse 않을 것 hello를 필요에 따라 선택을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="f7f95-148">구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![구독 대화 상자 관리][05]
5. <span data-ttu-id="f7f95-150">Hello 때 **tooAzure 웹 응용 프로그램 컨테이너 배포** 대화 상자가 나타나면 사용자가 이전에 만든 모든 웹 응용 프로그램 컨테이너 표시 됩니다; hello 목록 모든 컨테이너를 만들지 않은 경우 비어 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![TooAzure 웹 응용 프로그램 컨테이너 대화 상자 배포][06]
6. <span data-ttu-id="f7f95-152">하지 Azure 웹 응용 프로그램 컨테이너 전에, 또는 toopublish 원하는 경우 응용 프로그램 tooa 새 컨테이너를 만든 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="f7f95-153">그렇지 않은 경우 기존 웹 응용 프로그램 컨테이너를 선택 하 고 아래의 7 toostep를 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="f7f95-154">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="f7f95-154">Click **New...**</span></span>
      
       ![TooAzure 웹 응용 프로그램 컨테이너 대화 상자 배포][15]
   2. <span data-ttu-id="f7f95-156">hello **새 웹 응용 프로그램 컨테이너** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![새 웹앱 컨테이너 대화 상자][07a]
   3. <span data-ttu-id="f7f95-158">입력 한 **DNS 레이블을** 웹 응용 프로그램 컨테이너;에 대해 Azure에서 웹 응용 프로그램에 대 한 hello 호스트 URL의 hello 리프 DNS 레이블을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="f7f95-159">(해당 hello 이름은 사용 가능 하 고 tooAzure 웹 응용 프로그램의 명명 요구 사항 준수 note).</span><span class="sxs-lookup"><span data-stu-id="f7f95-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="f7f95-160">Hello에 **웹 컨테이너** 드롭 다운 메뉴에서 응용 프로그램에 대 한 선택 hello 적절 한 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="f7f95-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="f7f95-161">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="f7f95-162">Hello 선택한 소프트웨어의 최근 배포를 Azure에서 제공 됩니다 및 Oracle에서 만들어져 Azure에서 제공 하는 JDK 8의 최근 배포에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="f7f95-163">Hello에 **구독** 드롭 다운 메뉴에서 선택 hello 구독 toouse이이 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="f7f95-164">Hello에 **리소스 그룹** 드롭 다운 메뉴에서 사용할 tooassociate 웹 앱 선택 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="f7f95-165">(Azure 리소스 그룹을 사용 하면 toogroup 관련 리소스 함께 예, 삭제할 수 있습니다 함께 있도록.)</span><span class="sxs-lookup"><span data-stu-id="f7f95-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="f7f95-166">Skip toostep g 아래 또는 다음 이러한 사용 하 여 hello 단계 toocreate 새 리소스 그룹 및 (있는 경우 모든) 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="f7f95-167">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="f7f95-167">Click **New...**</span></span>
      * <span data-ttu-id="f7f95-168">hello **새 리소스 그룹** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![새 리소스 그룹 대화 상자][08]
      * <span data-ttu-id="f7f95-170">Hello hello에 **이름** 텍스트 상자에 새 리소스 그룹 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="f7f95-171">Hello hello에 **지역** 드롭 다운 메뉴에서 선택 hello 적절 한 Azure 데이터 센터 리소스 그룹에 대 한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="f7f95-172">선택 사항: 기본적으로 Java 8의 최근 배포 배포 될 Azure에서 자동으로 사용자 JVM으로 tooyour 웹 응용 프로그램 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="f7f95-173">그러나 웹 앱에 필요한 경우 다른 버전과 hello JVM의 분포 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="f7f95-174">웹 앱에 대 한 JDK toospecify hello 클릭 hello **JDK** 탭을 hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="f7f95-175">**Hello 기본 Azure 웹 앱 서비스에서 제공 하는 JDK 배포**:이 옵션의 Java 8 최근 배포를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="f7f95-176">**타사 JDK를 Azure에서 사용할 수 있는 배포**:이 옵션을 통해 Microsoft Azure에서 제공 하는 Jdk의 hello 목록에서 toochoose 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="f7f95-177">**이 다운로드 위치에서 나만의 JDK 배포**:이 옵션을 통해 toospecify 수 ZIP 파일로 패키지 해야 및 tooeither를 공개적으로 사용할 수 있는 다운로드 위치 또는 Azure 저장소 계정에 업로드는 사용자 고유의 JDK 배포 하면 액세스할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="f7f95-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![새 웹앱 컨테이너 대화 상자][07b]
   7. <span data-ttu-id="f7f95-179">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-179">Click **OK**.</span></span>
   8. <span data-ttu-id="f7f95-180">hello **앱 서비스 계획** 드롭 다운 메뉴는 선택한 리소스 그룹 hello와 관련 된 hello 앱 서비스 계획을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="f7f95-181">(앱 서비스 계획 가격 책정 계층 및 계산 인스턴스 크기 hello hello 웹 응용 프로그램의 hello 위치와 같은 정보를 지정 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="f7f95-182">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="f7f95-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="f7f95-183">(있는 경우 하나)는 기존 앱 서비스 계획 선택할 수 있습니다 및 toostep h 아래의 건너뛰거나 이러한 단계 toocreate 새 앱 서비스 계획을 수행 하는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f7f95-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="f7f95-184">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="f7f95-184">Click **New...**</span></span>
      * <span data-ttu-id="f7f95-185">hello **새 앱 서비스 계획** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![새 App Service 계획 대화 상자][09]
      * <span data-ttu-id="f7f95-187">Hello hello에 **이름** 입력란을 새 앱 서비스 계획에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="f7f95-188">Hello hello에 **위치** 드롭 다운 메뉴에서 선택 hello 적절 한 Azure 데이터 센터 hello 계획에 대 한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="f7f95-189">Hello hello에 **가격 책정 계층** 드롭 다운 메뉴에서 선택 hello hello 계획에 대 한 가격 책정 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="f7f95-190">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="f7f95-191">Hello hello에 **인스턴스 크기** 드롭 다운 메뉴에서 hello 계획에 대 한 선택 hello 적절 한 인스턴스 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="f7f95-192">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="f7f95-193">모든 단계는 hello 완료 되 면 hello 새 웹 응용 프로그램 컨테이너 대화 상자 그림 다음 hello와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![새 웹앱 컨테이너 대화 상자][10]
   10. <span data-ttu-id="f7f95-195">클릭 **확인** toocomplete hello 만드는 새 웹 응용 프로그램 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="f7f95-196">에 대 한 hello 목록은 hello 웹 응용 프로그램 컨테이너 toobe 몇 초 기다린 새로 고쳐지고 새로 만든 웹 응용 프로그램 컨테이너 hello 목록에서 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="f7f95-197">이제 웹 응용 프로그램 tooAzure의 준비 toocomplete hello 초기 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![TooAzure 웹 응용 프로그램 컨테이너 대화 상자 배포][11]
   
    <span data-ttu-id="f7f95-199">클릭 **확인** toodeploy Java 응용 프로그램 toohello 웹 응용 프로그램 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="f7f95-200">기본적으로 응용 프로그램의 응용 프로그램 서버 hello 하위 디렉터리로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="f7f95-201">원하는 toobe hello 루트 응용 프로그램으로 배포를 하는 경우 확인 hello **tooroot 배포** 확인란을 클릭 하기 전에 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="f7f95-202">Hello을 다음으로 표시 되어야 **Azure 활동 로그** 보기는 웹 응용 프로그램의 hello 배포 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Azure 동작 로그][12]
   
    <span data-ttu-id="f7f95-204">hello 배포 프로세스를 웹 응용 프로그램 tooAzure 몇 초 이내에 수행 해야 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="f7f95-205">때 응용 프로그램 준비, 나타납니다 이라는 링크가 **게시 됨** hello에 **상태** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="f7f95-206">Hello 링크를 클릭할 때 걸리는 있습니다 tooyour 배포 웹 앱의 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="f7f95-207">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="f7f95-207">Updating your web app</span></span>
<span data-ttu-id="f7f95-208">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="f7f95-209">기존 Java 웹 앱의 hello 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="f7f95-210">추가 Java 응용 프로그램 toohello 게시할 수 동일한 웹 응용 프로그램 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="f7f95-211">두 경우 모두 hello 프로세스는 동일 하 고 몇 초 밖에 걸리지:</span><span class="sxs-lookup"><span data-stu-id="f7f95-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="f7f95-212">Hello Eclipse 프로젝트 탐색기에서 tooan 기존 웹 응용 프로그램 컨테이너를 추가 하거나 tooupdate hello Java 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="f7f95-213">Hello 상황에 맞는 메뉴에 표시 되 면 선택 **Azure** 차례로 **Azure 웹 앱으로 게시 중...**</span><span class="sxs-lookup"><span data-stu-id="f7f95-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="f7f95-214">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="f7f95-215">Java 응용 프로그램 tooand 클릭 다시 게시 하거나 toopublish 하나 선택 hello **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="f7f95-216">몇 초 후 hello **Azure 활동 로그** 보기에 따라 업데이트 된 배포 표시 됩니다 **게시 됨** 하면 웹 브라우저에서 업데이트 된 응용 프로그램 수 tooverify 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="f7f95-217">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7f95-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="f7f95-218">toostart (모든 배포 된 hello Java 응용 프로그램에 포함)는 기존 Azure 웹 앱 컨테이너를 중지, hello를 사용할 수 있습니다 또는 **Azure 탐색기** 보기.</span><span class="sxs-lookup"><span data-stu-id="f7f95-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="f7f95-219">경우 hello **Azure 탐색기** 뷰가 이미 열려 있지 않으면 다음을 클릭 하 여 열 수, **창** Eclipse에서 메뉴를 클릭 한 다음 **보기 표시**, 다음 **다른...** , 다음 **Azure**, 클릭 하 고 **Azure 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="f7f95-220">이전 로그 하지 않은 경우 물어봅니다 toodo 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="f7f95-221">Hello 때 **Azure 탐색기** 뷰가 표시 됩니다, 사용 하 여 이러한 단계 toostart 따르거나 웹 응용 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="f7f95-222">Hello 확장 **Azure** 노드.</span><span class="sxs-lookup"><span data-stu-id="f7f95-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="f7f95-223">Hello 확장 **웹 앱** 노드.</span><span class="sxs-lookup"><span data-stu-id="f7f95-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="f7f95-224">마우스 오른쪽 단추로 클릭 hello 원하는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="f7f95-225">Hello 상황에 맞는 메뉴에 표시 되 면 클릭 **시작**, **중지**, 또는 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="f7f95-226">Note hello 메뉴 선택은 상황에 맞는 인식만 실행 중인 웹 응용 프로그램을 중지 하거나은 현재 실행 되는 웹 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![기존 웹앱 중지][13]

## <a name="next-steps"></a><span data-ttu-id="f7f95-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7f95-228">Next Steps</span></span>
<span data-ttu-id="f7f95-229">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:</span><span class="sxs-lookup"><span data-stu-id="f7f95-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="f7f95-230">[Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f7f95-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f7f95-231">[Azure Toolkit for Eclipse 설치 hello]</span><span class="sxs-lookup"><span data-stu-id="f7f95-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f7f95-232">*Eclipse에서 Azure용 Hello World 웹앱 만들기(이 문서)*</span><span class="sxs-lookup"><span data-stu-id="f7f95-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="f7f95-233">[Hello Azure Toolkit for Eclipse에서 새로운 이란]</span><span class="sxs-lookup"><span data-stu-id="f7f95-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="f7f95-234">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="f7f95-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f7f95-235">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="f7f95-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f7f95-236">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="f7f95-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="f7f95-237">[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]</span><span class="sxs-lookup"><span data-stu-id="f7f95-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="f7f95-238">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="f7f95-239">Azure 웹 앱을 만드는 방법에 대 한 자세한 내용은 참조 hello [웹 응용 프로그램 개요]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f95-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web-intellij-create-hello-world-web-app.md
[Azure Toolkit for Eclipse 설치 hello]: ../azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ../azure-toolkit-for-intellij-installation.md
[Hello Azure Toolkit for Eclipse에서 새로운 이란]: ../azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[웹 응용 프로그램 개요]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
