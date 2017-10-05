---
title: "Eclipse를 사용하여 기본 Azure Web App 만들기 | Microsoft Docs"
description: "이 자습서에서는Eclipse용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다."
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="f8391-103">Eclipse를 사용하여 기본 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="f8391-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="f8391-104">이 자습서에서는 [Eclipse용 Azure 도구 키트]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="f8391-105">기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한, 유사한 단계는 Java 서블릿에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="f8391-106">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][01]

## <a name="prerequisites"></a><span data-ttu-id="f8391-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f8391-108">Prerequisites</span></span>
* <span data-ttu-id="f8391-109">JDK(Java 개발자 키트), v 1.8 이상.</span><span class="sxs-lookup"><span data-stu-id="f8391-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="f8391-110">Eclipse IDE for Java EE Developers, Luna 이상.</span><span class="sxs-lookup"><span data-stu-id="f8391-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="f8391-111"><http://www.eclipse.org/downloads/>에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="f8391-112">Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: [Apache Tomcat] 또는 [Jetty])</span><span class="sxs-lookup"><span data-stu-id="f8391-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="f8391-113">Azure 구독은 <https://azure.microsoft.com/free/> 또는 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="f8391-114">[Eclipse용 Azure 도구 키트].</span><span class="sxs-lookup"><span data-stu-id="f8391-114">The [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="f8391-115">Azure 도구 키트에 대한 자세한 내용은 [Eclipse용 Azure 도구 키트 설치]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8391-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="f8391-116">Hello World 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f8391-116">To create a Hello World application</span></span>
<span data-ttu-id="f8391-117">먼저 java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="f8391-118">Eclipse를 시작하고 메뉴에서 **File**, **New**, **Dynamic Web Project**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-118">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="f8391-119">(**File**, **New**를 차례로 클릭한 후 **Dynamic Web Project**가 사용 가능한 프로젝트로 표시되지 않는 경우 **File**, **New**, **Project...**를 차례로 클릭한 후 **Web**을 확장하고 **Dynamic Web Project**를 클릭한 후 **Next**를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="f8391-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="f8391-120">이 자습서에서는 프로젝트의 이름을 **MyWebApp**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-120">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="f8391-121">화면이 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-121">Your screen will appear similar to the following:</span></span>
   
    ![새로운 동적 웹 프로젝트 만들기][02]
3. <span data-ttu-id="f8391-123">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-123">Click **Finish**.</span></span>
4. <span data-ttu-id="f8391-124">Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="f8391-125">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="f8391-126">**새 JSP 파일** 대화 상자에서 **index.jsp** 파일의 이름을 지정하고 부모 폴더를 **MyWebApp/WebContent**로 유지한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-126">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="f8391-127">**JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)**을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-127">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="f8391-128">Eclipse에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-128">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="f8391-129">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="f8391-129">within the existing `<body>` element.</span></span> <span data-ttu-id="f8391-130">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-130">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="f8391-131">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-131">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="f8391-132">Azure Web App 컨테이너에 응용 프로그램을 배포하려면</span><span class="sxs-lookup"><span data-stu-id="f8391-132">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="f8391-133">몇 가지 방법으로 Azure에 Java 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-133">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="f8391-134">이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-134">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="f8391-135">JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-135">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="f8391-136">따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-136">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="f8391-137">Eclipse의 프로젝트 탐색기에서 **MyWebApp**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="f8391-138">상황에 맞는 메뉴에서 **Azure**를 선택하고 **Azure 웹앱으로 게시...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-138">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Azure 웹앱으로 게시][03]
   
    <span data-ttu-id="f8391-140">또는 프로젝트 탐색기에서 웹 응용 프로그램 프로젝트를 선택한 상태로 도구 모음에서 **게시** 드롭다운 단추를 클릭하고 다음에서 **Azure 웹앱으로 게시**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-140">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Azure 웹앱으로 게시][14]
3. <span data-ttu-id="f8391-142">Eclipse에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-142">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
    ![Azure 로그인 대화 상자][04]
   
    <span data-ttu-id="f8391-144">Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-144">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="f8391-145">이 경우 로그인 지침에 따라 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-145">When this happens, continue following the sign in instructions.</span></span>
4. <span data-ttu-id="f8391-146">Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-146">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="f8391-147">여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 선택적으로 사용할 구독을 선택 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-147">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="f8391-148">구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![구독 대화 상자 관리][05]
5. <span data-ttu-id="f8391-150">**Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-150">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Azure 웹앱 컨테이너에 배포 대화 상자][06]
6. <span data-ttu-id="f8391-152">이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-152">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="f8391-153">그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 7단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-153">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   1. <span data-ttu-id="f8391-154">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="f8391-154">Click **New...**</span></span>
      
       ![Azure 웹앱 컨테이너에 배포 대화 상자][15]
   2. <span data-ttu-id="f8391-156">**새 웹앱 컨테이너** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-156">The **New Web App Container** dialog box will be displayed:</span></span>
      
       ![새 웹앱 컨테이너 대화 상자][07a]
   3. <span data-ttu-id="f8391-158">웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-158">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="f8391-159">(이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f8391-159">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="f8391-160">**웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-160">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="f8391-161">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="f8391-162">선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-162">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="f8391-163">**구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-163">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="f8391-164">**리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="f8391-165">(Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="f8391-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="f8391-166">기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 이들 단계를 통해 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="f8391-167">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="f8391-167">Click **New...**</span></span>
      * <span data-ttu-id="f8391-168">**새 리소스 그룹** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![새 리소스 그룹 대화 상자][08]
      * <span data-ttu-id="f8391-170">**이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="f8391-171">**지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="f8391-172">선택 사항: 기본적으로 Java 8 최신 배포판은 Azure가 자동으로 웹앱 컨테이너에 JVM으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="f8391-173">그러나 웹앱에서 요구하는 경우 JVM의 다른 버전 및 배포판을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="f8391-174">웹앱에 대한 JDK를 지정하려면 **JDK** 탭을 클릭하고 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
        
        * <span data-ttu-id="f8391-175">**Azure Web Apps에서 제공하는 기본 JDK 배포**: 이 옵션을 선택하면 Java 8 최신 배포판이 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="f8391-176">**Azure에 제공되는 타사 JDK 배포**: 이 옵션을 선택하면 Microsoft Azure에서 제공하는 JDK 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="f8391-177">**이 다운로드 위치에서 나의 고유한 JDK 배포**: 이 옵션을 선택하면 사용자 고유의 JDK 배포판을 지정할 수 있으며, 사용자 고유의 배포판을 ZIP 파일로 패키지하여 공개적으로 이용 가능한 다운로드 위치 또는 사용자가 액세스 권한을 갖고 있는 Azure Storage 계정에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![새 웹앱 컨테이너 대화 상자][07b]
   7. <span data-ttu-id="f8391-179">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-179">Click **OK**.</span></span>
   8. <span data-ttu-id="f8391-180">**앱 서비스 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 앱 서비스 계획이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="f8391-181">(App Service 계획은 웹앱의 위치, 가격 책정 계층, 계산 인스턴스 크기 등의 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="f8391-182">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="f8391-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="f8391-183">기존 앱 서비스 계획(있는 경우)을 선택하고 아래 h 단계로 건너뛰거나 이들 단계를 통해 새 앱 서비스 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-183">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="f8391-184">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="f8391-184">Click **New...**</span></span>
      * <span data-ttu-id="f8391-185">**새 앱 서비스 계획** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-185">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![새 App Service 계획 대화 상자][09]
      * <span data-ttu-id="f8391-187">**이름** 텍스트 상자에서 새 앱 서비스 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-187">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="f8391-188">**위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-188">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="f8391-189">**가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-189">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="f8391-190">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="f8391-191">**인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-191">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="f8391-192">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="f8391-193">위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![새 웹앱 컨테이너 대화 상자][10]
   10. <span data-ttu-id="f8391-195">**확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-195">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="f8391-196">웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-196">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
7. <span data-ttu-id="f8391-197">이제 Azure에 웹앱의 초기 배포를 완료할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-197">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
    ![Azure 웹앱 컨테이너에 배포 대화 상자][11]
   
    <span data-ttu-id="f8391-199">**확인** 을 클릭하여 선택한 웹앱 컨테이너에 Java 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-199">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
    <span data-ttu-id="f8391-200">기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-200">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="f8391-201">루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-201">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="f8391-202">이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-202">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Azure 동작 로그][12]
   
    <span data-ttu-id="f8391-204">Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-204">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="f8391-205">응용 프로그램이 준비되면 **게시됨** in the **게시됨** 이라는 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-205">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="f8391-206">이 링크를 클릭하면 배포된 웹앱의 홈 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-206">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="f8391-207">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="f8391-207">Updating your web app</span></span>
<span data-ttu-id="f8391-208">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="f8391-209">기존 Java 웹앱의 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-209">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="f8391-210">동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-210">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="f8391-211">두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-211">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="f8391-212">Eclipse Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-212">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="f8391-213">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-213">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="f8391-214">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="f8391-215">Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-215">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="f8391-216">몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-216">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="f8391-217">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f8391-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="f8391-218">기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-218">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="f8391-219">**Azure 탐색기** 보기가 열려 있지 않은 경우 Eclipse에서 **Window** 메뉴를 클릭한 다음 **보기 표시**, **기타...**, **Azure**, **Azure 탐색기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-219">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="f8391-220">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-220">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="f8391-221">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-221">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="f8391-222">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-222">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="f8391-223">**웹앱** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-223">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="f8391-224">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-224">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="f8391-225">상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-225">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="f8391-226">메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8391-226">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![기존 웹앱 중지][13]

## <a name="next-steps"></a><span data-ttu-id="f8391-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8391-228">Next Steps</span></span>
<span data-ttu-id="f8391-229">Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8391-229">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="f8391-230">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="f8391-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f8391-231">[Eclipse용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="f8391-231">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f8391-232">*Eclipse에서 Azure용 Hello World 웹앱 만들기(이 문서)*</span><span class="sxs-lookup"><span data-stu-id="f8391-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="f8391-233">[Eclipse용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="f8391-233">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="f8391-234">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="f8391-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f8391-235">[IntelliJ용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="f8391-235">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f8391-236">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="f8391-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="f8391-237">[IntelliJ용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="f8391-237">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="f8391-238">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8391-238">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="f8391-239">Azure 웹앱 만들기에 대한 자세한 내용은 [웹앱 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8391-239">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

<span data-ttu-id="f8391-240">[Eclipse용 Azure 도구 키트]: ../azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="f8391-240">[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="f8391-241">[IntelliJ용 Azure 도구 키트]: ../azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="f8391-241">[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md</span></span>
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
<span data-ttu-id="f8391-242">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f8391-242">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f8391-243">[Eclipse용 Azure 도구 키트 설치]: ../azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="f8391-243">[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="f8391-244">[IntelliJ용 Azure 도구 키트 설치]: ../azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="f8391-244">[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="f8391-245">[Eclipse용 Azure 도구 키트의 새로운 기능]: ../azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f8391-245">[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="f8391-246">[IntelliJ용 Azure 도구 키트의 새로운 기능]: ../azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f8391-246">[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="f8391-247">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f8391-247">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f8391-248">[웹앱 개요]: ./app-service-web-overview.md</span><span class="sxs-lookup"><span data-stu-id="f8391-248">[Web Apps Overview]: ./app-service-web-overview.md</span></span>
<span data-ttu-id="f8391-249">[Apache Tomcat]: http://tomcat.apache.org/</span><span class="sxs-lookup"><span data-stu-id="f8391-249">[Apache Tomcat]: http://tomcat.apache.org/</span></span>
<span data-ttu-id="f8391-250">[Jetty]: http://www.eclipse.org/jetty/</span><span class="sxs-lookup"><span data-stu-id="f8391-250">[Jetty]: http://www.eclipse.org/jetty/</span></span>

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
