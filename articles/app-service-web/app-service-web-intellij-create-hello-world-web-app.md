---
title: "IntelliJ의 기본 Azure 웹 앱 aaaCreate | Microsoft Docs"
description: "이 자습서에서는 어떻게 toouse hello Azure 도구 키트 IntelliJ toocreate에 대 한 Azure 용 Hello World 웹 응용 프로그램입니다."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="5cea1-103">IntelliJ에서 기본 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="5cea1-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="5cea1-104">이 자습서에서는 어떻게 toocreate hello를 사용 하 여 기본 Hello World 응용 프로그램 tooAzure 웹 앱으로 배포 및 [IntelliJ 용 Azure 도구 키트]합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="5cea1-105">기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한, 유사한 단계는 Java 서블릿에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="5cea1-106">이 자습서를 완료 하는 경우 비슷한 toohello 웹 브라우저에서 볼 때 그림을 다음 응용 프로그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![샘플 웹 페이지][01]

## <a name="prerequisites"></a><span data-ttu-id="5cea1-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5cea1-108">Prerequisites</span></span>
* <span data-ttu-id="5cea1-109">JDK(Java 개발자 키트), v 1.8 이상.</span><span class="sxs-lookup"><span data-stu-id="5cea1-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="5cea1-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="5cea1-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="5cea1-111"><https://www.jetbrains.com/idea/download/index.html>에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="5cea1-112">Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: [Apache Tomcat] 또는 [Jetty])</span><span class="sxs-lookup"><span data-stu-id="5cea1-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="5cea1-113">Azure 구독은 <https://azure.microsoft.com/free/> 또는 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="5cea1-114">hello [IntelliJ 용 Azure 도구 키트]합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="5cea1-115">Hello Azure 도구 키트를 설치 하는 방법에 대 한 정보를 참조 하십시오. [IntelliJ 용 Azure 도구 키트 설치 hello]합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="5cea1-116">toocreate Hello World 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5cea1-116">toocreate a Hello World application</span></span>
<span data-ttu-id="5cea1-117">먼저 java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="5cea1-118">IntelliJ를 시작 하 고 hello 클릭 **파일** 메뉴를 클릭 한 다음 **새로 만들기**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![파일 새로 만들기 프로젝트][02]
2. <span data-ttu-id="5cea1-120">Hello 새 프로젝트 대화 상자에서 선택 **Java**, 다음 **웹 응용 프로그램**, 클릭 하 고 **새로** tooadd 프로젝트 SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![새 프로젝트 대화 상자][03a]
   
3. <span data-ttu-id="5cea1-122">홈 디렉터리 선택 JDK 대화 상자에 대 한 hello, 선택 hello JDK가 설치 되어 있는 폴더와 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="5cea1-123">클릭 **다음** hello 새 프로젝트 대화 상자 toocontinue에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![JDK 홈 디렉터리 지정][03b]
4. <span data-ttu-id="5cea1-125">이 자습서에서는 이름을 hello 프로젝트 **Java 웹-응용 프로그램-에-Azure**, 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![새 프로젝트 대화 상자][04]
5. <span data-ttu-id="5cea1-127">IntelliJ의 Project Explorer 보기 내에서 **Java-Web-App-On-Azure**를 확장한 다음 **web**을 확장하고 **index.jsp**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![인덱스 페이지 열기][05c]
6. <span data-ttu-id="5cea1-129">IntelliJ에서 index.jsp 파일이 열리면 텍스트 toodynamically 디스플레이에서 추가 **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="5cea1-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="5cea1-130">hello 기존 내 `<body>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="5cea1-131">업데이트 한 후 `<body>` 콘텐츠 hello 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="5cea1-132">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="5cea1-133">toodeploy 프로그램 응용 프로그램 tooan Azure 웹 응용 프로그램 컨테이너</span><span class="sxs-lookup"><span data-stu-id="5cea1-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="5cea1-134">여러 가지 방법으로 여는 Java 웹 응용 프로그램 tooAzure를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="5cea1-135">이 자습서에서는 가장 간단한 hello 중 하나를 설명: 응용 프로그램에 배포 된 Azure 웹 응용 프로그램 컨테이너 tooan 됩니다-특수 프로젝트 형식 이나 추가 도구 없는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="5cea1-136">hello JDK 및 hello 웹 컨테이너 소프트웨어는 사용자에 게 제공 Azure에서 이므로 없습니다 필요 tooupload 고유한; 하기만 하면 Java 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="5cea1-137">결과적으로, 응용 프로그램에 대 한 게시 프로세스 hello 초, 분 하지 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="5cea1-138">응용 프로그램을 게시 하기 전에 먼저 tooconfigure 모듈 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="5cea1-139">따라서 toodo 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="5cea1-140">IntelliJ의 프로젝트 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Java 웹-응용 프로그램-에-Azure** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5cea1-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="5cea1-141">Hello 상황에 맞는 메뉴에 표시 되 면 클릭 **모듈 설정 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![모듈 설정 열기][05a]
2. <span data-ttu-id="5cea1-143">Hello 프로젝트 구조 대화 상자가 나타나는 경우:</span><span class="sxs-lookup"><span data-stu-id="5cea1-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="5cea1-144">a.</span><span class="sxs-lookup"><span data-stu-id="5cea1-144">a.</span></span> <span data-ttu-id="5cea1-145">클릭 **아티팩트** hello 목록에 **프로젝트 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="5cea1-146">b.</span><span class="sxs-lookup"><span data-stu-id="5cea1-146">b.</span></span> <span data-ttu-id="5cea1-147">Hello hello 아티팩트 이름 변경 **이름** 상자를 공백이 나 특수 문자가 포함 되어 있지 않습니다;이 hello 이름 hello 식별자 URI (Uniform Resource)에 사용 되므로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="5cea1-148">c.</span><span class="sxs-lookup"><span data-stu-id="5cea1-148">c.</span></span> <span data-ttu-id="5cea1-149">변경 hello **형식** 너무**웹 응용 프로그램: 보관**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="5cea1-150">d.</span><span class="sxs-lookup"><span data-stu-id="5cea1-150">d.</span></span> <span data-ttu-id="5cea1-151">클릭 **확인** tooclose hello 프로젝트 구조 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5cea1-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![모듈 설정 열기][05b]

<span data-ttu-id="5cea1-153">모듈 설정으로 구성한 경우에 단계를 수행 하는 hello를 사용 하 여 응용 프로그램 tooAzure를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="5cea1-154">IntelliJ의 프로젝트 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Java 웹-응용 프로그램-에-Azure** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5cea1-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="5cea1-155">Hello 상황에 맞는 메뉴에 표시 되 면 선택 **Azure**, 클릭 하 고 **Azure 웹 앱으로 게시 중...**</span><span class="sxs-lookup"><span data-stu-id="5cea1-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure 게시 상황에 맞는 메뉴][06]
2. <span data-ttu-id="5cea1-157">아직 IntelliJ에서 Azure에 등록 하지 않은 경우 Azure 계정에 증명된 toosign 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="5cea1-158">(Azure 계정을 여러 개 있는 경우 일부 hello hello 로그인 프로세스 중에 메시지가 표시 될 수 있습니다 두 번 이상 toobe 나타나는 경우에 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="5cea1-159">이 경우, 지침에 설명 된 toofollow hello 기호를 계속 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5cea1-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Azure 로그인 대화 상자][07]
3. <span data-ttu-id="5cea1-161">Azure 계정에 성공적으로 로그인을 한 후 hello **구독 관리** 대화 상자에 자격 증명으로 연결 된 구독 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="5cea1-162">(나열 된 여러 구독이 있는 경우 그 중 특정 하위 집합만 toowork 있습니다 수 필요에 따라 선택 취소 toouse 원하는 hello 구독 합니다.) 구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![구독 관리][08]
4. <span data-ttu-id="5cea1-164">Hello 때 **tooAzure 웹 응용 프로그램 컨테이너 배포** 대화 상자가 나타나면 사용자가 이전에 만든 모든 웹 응용 프로그램 컨테이너 표시 됩니다; hello 목록 모든 컨테이너를 만들지 않은 경우 비어 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![앱 컨테이너][09]
5. <span data-ttu-id="5cea1-166">하지 Azure 웹 응용 프로그램 컨테이너 전에, 또는 toopublish 원하는 경우 응용 프로그램 tooa 새 컨테이너를 만든 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="5cea1-167">그렇지 않은 경우 기존 웹 응용 프로그램 컨테이너를 선택 하 고 아래 6 toostep를 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="5cea1-168">**+**</span><span class="sxs-lookup"><span data-stu-id="5cea1-168">Click **+**</span></span>
      
       ![앱 컨테이너 추가][10]
   2. <span data-ttu-id="5cea1-170">hello **새 웹 응용 프로그램 컨테이너** 대화 상자가 표시 됩니다, 될 hello에 대 한 다음 몇 단계 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![새 앱 컨테이너][11a]
   3. <span data-ttu-id="5cea1-172">입력 한 **DNS 레이블을** 웹 응용 프로그램 컨테이너;에 대해 Azure에서 웹 응용 프로그램에 대 한 hello 호스트 URL의 hello 리프 DNS 레이블을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="5cea1-173">Note hello 이름이 사용 가능 해지고 tooAzure 웹 응용 프로그램의 명명 요구 사항 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="5cea1-174">Hello에 **웹 컨테이너** 드롭 다운 메뉴에서 응용 프로그램에 대 한 선택 hello 적절 한 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="5cea1-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="5cea1-175">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="5cea1-176">Hello 선택한 소프트웨어의 최근 배포를 Azure에서 제공 됩니다 및 Oracle에서 만들어져 Azure에서 제공 하는 JDK 8의 최근 배포에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="5cea1-177">Hello에 **구독** 드롭 다운 메뉴에서 선택 hello 구독 toouse이이 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="5cea1-178">Hello에 **리소스 그룹** 드롭 다운 메뉴에서 사용할 tooassociate 웹 앱 선택 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="5cea1-179">(Azure 리소스 그룹을 사용 하면 toogroup 관련 리소스 함께 예, 삭제할 수 있습니다 함께 있도록.)</span><span class="sxs-lookup"><span data-stu-id="5cea1-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="5cea1-180">Skip toostep g 아래 또는 사용 하 여 hello 다음 toocreate 새 리소스 그룹을 단계와 (한) 경우에 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="5cea1-181">선택  **&lt; &lt; 새 리소스 그룹 만들기 &gt; &gt;**  hello에 **리소스 그룹** 드롭 다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5cea1-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="5cea1-182">hello **새 리소스 그룹** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![새 리소스 그룹][12]
      * <span data-ttu-id="5cea1-184">Hello hello에 **이름** 텍스트 상자에 새 리소스 그룹 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="5cea1-185">Hello hello에 **지역** 드롭 다운 메뉴에서 선택 hello 적절 한 Azure 데이터 센터 리소스 그룹에 대 한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="5cea1-186">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-186">Click **OK**.</span></span>
   7. <span data-ttu-id="5cea1-187">hello **앱 서비스 계획** 드롭 다운 메뉴는 선택한 리소스 그룹 hello와 관련 된 hello 앱 서비스 계획을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="5cea1-188">(앱 서비스 계획 가격 책정 계층 및 계산 인스턴스 크기 hello hello 웹 응용 프로그램의 hello 위치와 같은 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="5cea1-189">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="5cea1-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="5cea1-190">(있는 경우 하나)는 기존 앱 서비스 계획 선택할 수 있습니다 및 toostep h 아래의 건너뛰거나 단계 toocreate 새 앱 서비스 계획을 따르는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5cea1-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="5cea1-191">선택  **&lt; &lt; 새 앱 서비스 계획 만들기 &gt; &gt;**  hello에 **앱 서비스 계획** 드롭 다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5cea1-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="5cea1-192">hello **새 앱 서비스 계획** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![새 앱 서비스 계획][13]
      * <span data-ttu-id="5cea1-194">Hello hello에 **이름** 입력란을 새 앱 서비스 계획에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="5cea1-195">Hello hello에 **위치** 드롭 다운 메뉴에서 선택 hello 적절 한 Azure 데이터 센터 hello 계획에 대 한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="5cea1-196">Hello hello에 **가격 책정 계층** 드롭 다운 메뉴에서 선택 hello hello 계획에 대 한 가격 책정 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="5cea1-197">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="5cea1-198">Hello hello에 **인스턴스 크기** 드롭 다운 메뉴에서 hello 계획에 대 한 선택 hello 적절 한 인스턴스 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="5cea1-199">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="5cea1-200">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-200">Click **OK**.</span></span>
   8. <span data-ttu-id="5cea1-201">(선택 사항) 기본적으로 Java 8의 최근 분포 자동으로 배포 될 예정 프로그램 JVM Azure tooyour 웹 응용 프로그램 컨테이너에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="5cea1-202">그러나 다른 버전 및 hello JVM의 분포를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="5cea1-203">따라서 toodo 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="5cea1-204">Hello 클릭 **JDK** hello 탭 **새 웹 응용 프로그램 컨테이너** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5cea1-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="5cea1-205">Hello 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="5cea1-206">Hello 기본 Azure에서 제공 되는 JDK를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="5cea1-207">Azure에서 사용할 수 있는 추가 JDK 드롭다운 목록에서 타사 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="5cea1-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="5cea1-208">사용자 지정 JDK 배포(이 JDK는 ZIP 파일로 패키지된 후 공개적으로 제공되거나 Azure Storage 계정에 제공되어야 함)</span><span class="sxs-lookup"><span data-stu-id="5cea1-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![새 앱 컨테이너 JDK 탭][11b]
   9. <span data-ttu-id="5cea1-210">모든 단계는 hello 완료 되 면 hello 새 웹 응용 프로그램 컨테이너 대화 상자 그림 다음 hello와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![새 앱 컨테이너][14]
   10. <span data-ttu-id="5cea1-212">클릭 **확인** toocomplete hello 만드는 새 웹 응용 프로그램 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="5cea1-213">에 대 한 hello 목록은 hello 웹 응용 프로그램 컨테이너 toobe 몇 초 기다린 새로 고쳐지고 새로 만든 웹 응용 프로그램 컨테이너 hello 목록에서 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="5cea1-214">웹 앱 tooAzure;의 준비 toocomplete hello 초기 배포는 이제 클릭 **확인** toodeploy Java 응용 프로그램 toohello 웹 응용 프로그램 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="5cea1-215">기본적으로 응용 프로그램의 응용 프로그램 서버 hello 하위 디렉터리로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="5cea1-216">원하는 toobe hello 루트 응용 프로그램으로 배포를 하는 경우 확인 hello **tooroot 배포** 확인란을 클릭 하기 전에 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![TooAzure 배포][15]
7. <span data-ttu-id="5cea1-218">Hello을 다음으로 표시 되어야 **Azure 활동 로그** 보기는 웹 응용 프로그램의 hello 배포 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![진행률 표시기][16]
   
    <span data-ttu-id="5cea1-220">hello 배포 프로세스를 웹 응용 프로그램 tooAzure 몇 초 이내에 수행 해야 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="5cea1-221">때 응용 프로그램 준비, 나타납니다 이라는 링크가 **게시 됨** hello에 **상태** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="5cea1-222">Hello 링크를 클릭 하면 배포 tooyour 웹 앱의 홈 페이지로 이동 합니다 또는 hello 섹션 toobrowse tooyour 웹 앱을 다음의 hello 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="5cea1-223">Azure에서 웹 앱 tooyour 검색</span><span class="sxs-lookup"><span data-stu-id="5cea1-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="5cea1-224">toobrowse tooyour Azure에서 웹 응용 프로그램에서는 hello **Azure 탐색기** 보기.</span><span class="sxs-lookup"><span data-stu-id="5cea1-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="5cea1-225">경우 hello **Azure 탐색기** 뷰가 이미 열려 있지 않으면 다음을 클릭 하 여 열 수, **보기** IntelliJ, 메뉴를 클릭 **도구 창**, 클릭 하 고  **서비스 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="5cea1-226">이전 로그 하지 않은 경우 물어봅니다 toodo 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="5cea1-227">Hello 때 **Azure 탐색기** 사용 하 여 이러한 단계 toobrowse tooyour 웹 응용 프로그램에 따라, 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="5cea1-228">Hello 확장 **Azure** 노드.</span><span class="sxs-lookup"><span data-stu-id="5cea1-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="5cea1-229">Hello 확장 **웹 앱** 노드.</span><span class="sxs-lookup"><span data-stu-id="5cea1-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="5cea1-230">마우스 오른쪽 단추로 클릭 hello 원하는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="5cea1-231">Hello 상황에 맞는 메뉴에 표시 되 면 클릭 **브라우저에서 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![웹앱 찾아보기][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="5cea1-233">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="5cea1-233">Updating your web app</span></span>
<span data-ttu-id="5cea1-234">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="5cea1-235">기존 Java 웹 앱의 hello 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="5cea1-236">추가 Java 응용 프로그램 toohello 게시할 수 동일한 웹 응용 프로그램 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="5cea1-237">두 경우 모두 hello 프로세스는 동일 하 고 몇 초 밖에 걸리지:</span><span class="sxs-lookup"><span data-stu-id="5cea1-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="5cea1-238">Hello IntelliJ 프로젝트 탐색기에서 tooan 기존 웹 응용 프로그램 컨테이너를 추가 하거나 tooupdate hello Java 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="5cea1-239">Hello 상황에 맞는 메뉴에 표시 되 면 선택 **Azure** 차례로 **Azure 웹 앱으로 게시 중...**</span><span class="sxs-lookup"><span data-stu-id="5cea1-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="5cea1-240">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="5cea1-241">Java 응용 프로그램 tooand 클릭 다시 게시 하거나 toopublish 하나 선택 hello **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="5cea1-242">몇 초 후 hello **Azure 활동 로그** 보기에 따라 업데이트 된 배포 표시 됩니다 **게시 됨** 하면 웹 브라우저에서 업데이트 된 응용 프로그램 수 tooverify 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="5cea1-243">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5cea1-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="5cea1-244">toostart (모든 배포 된 hello Java 응용 프로그램에 포함)는 기존 Azure 웹 앱 컨테이너를 중지, hello를 사용할 수 있습니다 또는 **Azure 탐색기** 보기.</span><span class="sxs-lookup"><span data-stu-id="5cea1-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="5cea1-245">경우 hello **Azure 탐색기** 뷰가 이미 열려 있지 않으면 다음을 클릭 하 여 열 수, **보기** IntelliJ, 메뉴를 클릭 **도구 창**, 클릭 하 고  **서비스 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="5cea1-246">이전 로그 하지 않은 경우 물어봅니다 toodo 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="5cea1-247">Hello 때 **Azure 탐색기** 뷰가 표시 됩니다, 사용 하 여 이러한 단계 toostart 따르거나 웹 응용 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="5cea1-248">Hello 확장 **Azure** 노드.</span><span class="sxs-lookup"><span data-stu-id="5cea1-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="5cea1-249">Hello 확장 **웹 앱** 노드.</span><span class="sxs-lookup"><span data-stu-id="5cea1-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="5cea1-250">마우스 오른쪽 단추로 클릭 hello 원하는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="5cea1-251">Hello 상황에 맞는 메뉴에 표시 되 면 클릭 **시작**, **중지**, 또는 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="5cea1-252">Note hello 메뉴 선택은 상황에 맞는 인식만 실행 중인 웹 응용 프로그램을 중지 하거나은 현재 실행 되는 웹 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![웹 앱 중지][18]

## <a name="next-steps"></a><span data-ttu-id="5cea1-254">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cea1-254">Next Steps</span></span>
<span data-ttu-id="5cea1-255">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:</span><span class="sxs-lookup"><span data-stu-id="5cea1-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="5cea1-256">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="5cea1-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5cea1-257">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="5cea1-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5cea1-258">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="5cea1-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="5cea1-259">[Hello Azure Toolkit for Eclipse에서 새로운 이란]</span><span class="sxs-lookup"><span data-stu-id="5cea1-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="5cea1-260">[IntelliJ 용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="5cea1-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5cea1-261">[IntelliJ 용 Azure 도구 키트 설치 hello]</span><span class="sxs-lookup"><span data-stu-id="5cea1-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5cea1-262">*IntelliJ에서 Azure용 Hello World 웹앱 만들기(이 문서)*</span><span class="sxs-lookup"><span data-stu-id="5cea1-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="5cea1-263">[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]</span><span class="sxs-lookup"><span data-stu-id="5cea1-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="5cea1-264">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5cea1-264">See Also</span></span>
<span data-ttu-id="5cea1-265">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="5cea1-266">Azure 웹 앱을 만드는 방법에 대 한 자세한 내용은 참조 hello [웹 응용 프로그램 개요]합니다.</span><span class="sxs-lookup"><span data-stu-id="5cea1-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ../azure-toolkit-for-eclipse.md
[IntelliJ 용 Azure 도구 키트]: ../azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ../azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 Azure 도구 키트 설치 hello]: ../azure-toolkit-for-intellij-installation.md
[Hello Azure Toolkit for Eclipse에서 새로운 이란]: ../azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[웹 응용 프로그램 개요]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
