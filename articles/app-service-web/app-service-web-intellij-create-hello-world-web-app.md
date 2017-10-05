---
title: "IntelliJ에서 기본 Azure Web App 만들기 | Microsoft Docs"
description: "이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다."
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="c6021-103">IntelliJ에서 기본 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="c6021-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="c6021-104">이 자습서에서는 [IntelliJ용 Azure 도구 키트]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="c6021-105">기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한, 유사한 단계는 Java 서블릿에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="c6021-106">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![샘플 웹 페이지][01]

## <a name="prerequisites"></a><span data-ttu-id="c6021-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c6021-108">Prerequisites</span></span>
* <span data-ttu-id="c6021-109">JDK(Java 개발자 키트), v 1.8 이상.</span><span class="sxs-lookup"><span data-stu-id="c6021-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="c6021-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="c6021-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="c6021-111"><https://www.jetbrains.com/idea/download/index.html>에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="c6021-112">Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: [Apache Tomcat] 또는 [Jetty])</span><span class="sxs-lookup"><span data-stu-id="c6021-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="c6021-113">Azure 구독은 <https://azure.microsoft.com/free/> 또는 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="c6021-114">[IntelliJ용 Azure 도구 키트].</span><span class="sxs-lookup"><span data-stu-id="c6021-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="c6021-115">Azure 도구 키트에 대한 자세한 내용은 [IntelliJ용 Azure 도구 키트 설치]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6021-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="c6021-116">Hello World 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="c6021-116">To create a Hello World application</span></span>
<span data-ttu-id="c6021-117">먼저 java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="c6021-118">IntelliJ를 시작하고 **File** 메뉴를 클릭한 후 **New**를 클릭하고 **Project**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![파일 새로 만들기 프로젝트][02]
2. <span data-ttu-id="c6021-120">New Project 대화 상자에서 **Java**를 선택하고 **Web Application**을 선택한 후 **New**를 클릭하여 프로젝트 SDK를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![새 프로젝트 대화 상자][03a]
   
3. <span data-ttu-id="c6021-122">Select Home Directory for JDK 대화 상자에서 JDK가 설치되어 있는 폴더를 선택한 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="c6021-123">New Project 대화 상자에서 **Next**를 클릭하여 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![JDK 홈 디렉터리 지정][03b]
4. <span data-ttu-id="c6021-125">이 자습서의 목적에 따라 프로젝트의 이름을 **Java-Web-App-On-Azure**로 지정하고 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![새 프로젝트 대화 상자][04]
5. <span data-ttu-id="c6021-127">IntelliJ의 Project Explorer 보기 내에서 **Java-Web-App-On-Azure**를 확장한 다음 **web**을 확장하고 **index.jsp**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![인덱스 페이지 열기][05c]
6. <span data-ttu-id="c6021-129">IntelliJ에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="c6021-130">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="c6021-130">within the existing `<body>` element.</span></span> <span data-ttu-id="c6021-131">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="c6021-132">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="c6021-133">Azure Web App 컨테이너에 응용 프로그램을 배포하려면</span><span class="sxs-lookup"><span data-stu-id="c6021-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="c6021-134">몇 가지 방법으로 Azure에 Java 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="c6021-135">이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="c6021-136">JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="c6021-137">따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="c6021-138">응용 프로그램을 게시하기 전에 먼저 모듈 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="c6021-139">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c6021-140">IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="c6021-141">상황에 맞는 메뉴가 나타나면 **모듈 설정 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![모듈 설정 열기][05a]
2. <span data-ttu-id="c6021-143">프로젝트 구조 대화 상자가 나타나면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="c6021-144">a.</span><span class="sxs-lookup"><span data-stu-id="c6021-144">a.</span></span> <span data-ttu-id="c6021-145">**프로젝트 설정** 목록에서 **아티팩트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="c6021-146">b.</span><span class="sxs-lookup"><span data-stu-id="c6021-146">b.</span></span> <span data-ttu-id="c6021-147">**이름** 상자에서 아티팩트 이름에 공백 또는 특수 문자가 포함되지 않도록 이름을 변경합니다. 이 작업은 해당 이름이 URI(Uniform Resource Identifier)에 사용되기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="c6021-148">c.</span><span class="sxs-lookup"><span data-stu-id="c6021-148">c.</span></span> <span data-ttu-id="c6021-149">**형식**을 **웹 응용 프로그램: 보관**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="c6021-150">d.</span><span class="sxs-lookup"><span data-stu-id="c6021-150">d.</span></span> <span data-ttu-id="c6021-151">**확인**을 클릭하여 프로젝트 구조 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![모듈 설정 열기][05b]

<span data-ttu-id="c6021-153">모듈 설정을 구성한 경우 다음 단계를 사용하여 Azure에 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="c6021-154">IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="c6021-155">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure 게시 상황에 맞는 메뉴][06]
2. <span data-ttu-id="c6021-157">IntelliJ에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="c6021-158">Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="c6021-159">이 경우 로그인 지침에 따라 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Azure 로그인 대화 상자][07]
3. <span data-ttu-id="c6021-161">Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="c6021-162">여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 사용하지 않을 구독의 선택을 취소하면 됩니다. 구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![구독 관리][08]
4. <span data-ttu-id="c6021-164">**Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![앱 컨테이너][09]
5. <span data-ttu-id="c6021-166">이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="c6021-167">그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 6단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="c6021-168">**+**</span><span class="sxs-lookup"><span data-stu-id="c6021-168">Click **+**</span></span>
      
       ![앱 컨테이너 추가][10]
   2. <span data-ttu-id="c6021-170">다음 몇 개 단계에서 사용되는 **새 웹앱 컨테이너** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![새 앱 컨테이너][11a]
   3. <span data-ttu-id="c6021-172">웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="c6021-173">이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="c6021-174">**웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="c6021-175">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="c6021-176">선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="c6021-177">**구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="c6021-178">**리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="c6021-179">(Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="c6021-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="c6021-180">기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 다음 단계를 통해 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="c6021-181">**리소스 그룹** 드롭다운 메뉴에서 **&lt;&lt;새 리소스 그룹 만들기&gt;&gt;**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="c6021-182">**새 리소스 그룹** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![새 리소스 그룹][12]
      * <span data-ttu-id="c6021-184">**이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="c6021-185">**지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="c6021-186">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-186">Click **OK**.</span></span>
   7. <span data-ttu-id="c6021-187">**앱 서비스 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 앱 서비스 계획이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="c6021-188">앱 서비스 계획은 웹 앱, 가격 책정 계층 및 계산 인스턴스 크기의 위치와 같은 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="c6021-189">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c6021-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="c6021-190">기존 App Service 계획(있는 경우)을 선택하고 아래 h 단계로 건너뛰거나 다음 단계를 통해 새 App Service 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="c6021-191">**App Service 계획** 드롭다운 메뉴에서 **&lt;&lt;새 App Service 계획 만들기&gt;&gt;**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="c6021-192">**새 앱 서비스 계획** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![새 앱 서비스 계획][13]
      * <span data-ttu-id="c6021-194">**이름** 텍스트 상자에서 새 앱 서비스 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="c6021-195">**위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="c6021-196">**가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="c6021-197">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="c6021-198">**인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="c6021-199">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="c6021-200">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-200">Click **OK**.</span></span>
   8. <span data-ttu-id="c6021-201">(선택 사항) 기본적으로 Java 8 최신 배포판은 자동으로 Azure에 의해 웹앱 컨테이너에 JVM으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="c6021-202">그러나 JVM의 다른 버전 및 배포판을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="c6021-203">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="c6021-204">**새 웹앱 컨테이너** 대화 상자에서 **JDK** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="c6021-205">다음 두 가지 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="c6021-206">Azure에서 제공하는 기본 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="c6021-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="c6021-207">Azure에서 사용할 수 있는 추가 JDK 드롭다운 목록에서 타사 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="c6021-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="c6021-208">사용자 지정 JDK 배포(이 JDK는 ZIP 파일로 패키지된 후 공개적으로 제공되거나 Azure Storage 계정에 제공되어야 함)</span><span class="sxs-lookup"><span data-stu-id="c6021-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![새 앱 컨테이너 JDK 탭][11b]
   9. <span data-ttu-id="c6021-210">위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![새 앱 컨테이너][14]
   10. <span data-ttu-id="c6021-212">**확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="c6021-213">웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="c6021-214">이제 Azure에 대한 웹앱의 초기 배포를 완료할 준비가 되었습니다. **확인**을 클릭하여 Java 응용 프로그램을 선택한 웹앱 컨테이너에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="c6021-215">기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="c6021-216">루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Azure에 배포][15]
7. <span data-ttu-id="c6021-218">이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![진행률 표시기][16]
   
    <span data-ttu-id="c6021-220">Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="c6021-221">응용 프로그램이 준비되면 **게시됨** in the **Published** 라는 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="c6021-222">이 링크를 클릭하여 배포된 웹앱의 홈페이지로 이동하거나, 다음 섹션의 단계를 사용하여 해당 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="c6021-223">Azure에서 웹앱 검색</span><span class="sxs-lookup"><span data-stu-id="c6021-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="c6021-224">Azure에서 웹앱을 검색하려면 **Azure 탐색기** 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="c6021-225">**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="c6021-226">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="c6021-227">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="c6021-228">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="c6021-229">**웹앱** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="c6021-230">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="c6021-231">상황에 맞는 메뉴가 나타나면 **브라우저에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![웹앱 찾아보기][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="c6021-233">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="c6021-233">Updating your web app</span></span>
<span data-ttu-id="c6021-234">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="c6021-235">기존 Java 웹앱의 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="c6021-236">동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="c6021-237">두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="c6021-238">IntelliJ Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="c6021-239">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="c6021-240">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="c6021-241">Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="c6021-242">몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="c6021-243">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="c6021-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="c6021-244">기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="c6021-245">**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="c6021-246">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="c6021-247">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="c6021-248">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="c6021-249">**웹앱** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="c6021-250">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="c6021-251">상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="c6021-252">메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6021-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![웹 앱 중지][18]

## <a name="next-steps"></a><span data-ttu-id="c6021-254">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6021-254">Next Steps</span></span>
<span data-ttu-id="c6021-255">Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6021-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="c6021-256">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="c6021-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c6021-257">[Eclipse용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="c6021-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c6021-258">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="c6021-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="c6021-259">[Eclipse용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="c6021-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="c6021-260">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="c6021-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c6021-261">[IntelliJ용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="c6021-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c6021-262">*IntelliJ에서 Azure용 Hello World 웹앱 만들기(이 문서)*</span><span class="sxs-lookup"><span data-stu-id="c6021-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="c6021-263">[IntelliJ용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="c6021-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="c6021-264">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c6021-264">See Also</span></span>
<span data-ttu-id="c6021-265">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6021-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="c6021-266">Azure 웹앱 만들기에 대한 자세한 내용은 [웹앱 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6021-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ../azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ../azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Eclipse용 Azure 도구 키트 설치]: ../azure-toolkit-for-eclipse-installation.md
[IntelliJ용 Azure 도구 키트 설치]: ../azure-toolkit-for-intellij-installation.md
[Eclipse용 Azure 도구 키트의 새로운 기능]: ../azure-toolkit-for-eclipse-whats-new.md
[IntelliJ용 Azure 도구 키트의 새로운 기능]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[웹앱 개요]: ./app-service-web-overview.md
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
