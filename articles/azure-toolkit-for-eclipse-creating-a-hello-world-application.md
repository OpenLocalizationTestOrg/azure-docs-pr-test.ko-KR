---
title: "Hello World 클라우드 서비스 Eclipse에서 Azure에 대 한 aaaCreate"
description: "Toocreate 사용 하 여 간단한 Hello World 응용 프로그램을 Azure Toolkit for Eclipse hello 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a><span data-ttu-id="00702-103">Eclipse에서 Azure용 Hello World 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="00702-103">Create a Hello World Cloud Service for Azure in Eclipse</span></span>
<span data-ttu-id="00702-104">hello 다음 단계 방법을 보여 줍니다 toocreate Eclipse 용 Azure 도구 키트 hello를 사용 하는 기본적인 JSP 응용 프로그램 tooAzure를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-104">hello following steps show you how toocreate and deploy a basic JSP application tooAzure using hello Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="00702-105">JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한 아주 유사한 단계는 Java 서블릿에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-105">A JSP example is shown for simplicity, but highly similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="00702-106">hello 응용 프로그램은 유사한 toohello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-106">hello application will look similar toohello following:</span></span>

![][ic600360]

## <a name="prerequisites"></a><span data-ttu-id="00702-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00702-107">Prerequisites</span></span>
* <span data-ttu-id="00702-108">JDK(Java 개발자 키트), v 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="00702-108">A Java Developer Kit (JDK), v 1.7 or later.</span></span>
* <span data-ttu-id="00702-109">Eclipse IDE for Java EE Developers, Indigo 이상.</span><span class="sxs-lookup"><span data-stu-id="00702-109">Eclipse IDE for Java EE Developers, Indigo or later.</span></span> <span data-ttu-id="00702-110"><http://www.eclipse.org/downloads/>에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-110">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="00702-111">Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: Apache Tomcat, GlassFish, JBoss Application Server, Jetty 또는 IBM® WebSphere® Application Server Liberty Core)</span><span class="sxs-lookup"><span data-stu-id="00702-111">A distribution of a Java-based web server or application server, such as Apache Tomcat, GlassFish, JBoss Application Server, Jetty, or IBM® WebSphere® Application Server Liberty Core.</span></span>
* <span data-ttu-id="00702-112">Azure 구독은 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-112">An Azure subscription, which can be acquired from <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="00702-113">Azure Toolkit for Eclipse 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-113">hello Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="00702-114">자세한 내용은 참조 [Azure Toolkit for Eclipse 설치 hello][Installing hello Azure Toolkit for Eclipse]합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-114">For more information, see [Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="00702-115">toocreate Hello World 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="00702-115">toocreate a Hello World application</span></span>
<span data-ttu-id="00702-116">먼저 java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00702-116">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="00702-117">Eclipse를 시작 하 고 hello 메뉴 **파일**, 클릭 **새로**, 클릭 하 고 **동적 웹 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-117">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="00702-118">(표시 되지 않으면 **동적 웹 프로젝트** 클릭 한 후 사용 가능한 프로젝트로 표시 **파일**, **새로**, 수행가 다음를 hello 다음: 클릭 **파일**, 클릭 **새로**, 클릭 **프로젝트...** 를 확장 하 고 **웹**, 클릭 **동적 웹 프로젝트**를 클릭 하 고 **다음**.)</span><span class="sxs-lookup"><span data-stu-id="00702-118">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File**, **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

1. <span data-ttu-id="00702-119">이 자습서에서는 이름을 hello 프로젝트 **MyHelloWorld**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-119">For purposes of this tutorial, name hello project **MyHelloWorld**.</span></span> <span data-ttu-id="00702-120">(확인이 이름을 사용 하 여,이 자습서의 이후 단계 이름이 MyHelloWorld 프로그램 WAR 파일 toobe 예상).</span><span class="sxs-lookup"><span data-stu-id="00702-120">(Ensure you use this name, subsequent steps in this tutorial expect your WAR file toobe named MyHelloWorld).</span></span> <span data-ttu-id="00702-121">화면에는 비슷한 toohello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-121">Your screen will appear similar toohello following:</span></span>

   ![][ic589576]

1. <span data-ttu-id="00702-122">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-122">Click **Finish**.</span></span>

1. <span data-ttu-id="00702-123">Eclipse의 Project Explorer 뷰 내에서 **MyHelloWorld**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-123">Within Eclipse's Project Explorer view, expand **MyHelloWorld**.</span></span> <span data-ttu-id="00702-124">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-124">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

1. <span data-ttu-id="00702-125">Hello에 **JSP 파일 새로** 대화 상자에서 이름 hello 파일 **index.jsp**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-125">In hello **New JSP File** dialog, name hello file **index.jsp**.</span></span> <span data-ttu-id="00702-126">Hello 상위 폴더를 유지 **MyHelloWorld/WebContent**hello 다음에 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="00702-126">Keep hello parent folder as **MyHelloWorld/WebContent**, as shown in hello following:</span></span>

   ![][ic659262]

1. <span data-ttu-id="00702-127">Hello에 **JSP 템플릿 선택** 대화 상자에서이 자습서 선택의 목적을 위해 **새 JSP 파일 (html)** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-127">In hello **Select JSP Template** dialog, for purposes of this tutorial select **New JSP File (html)** and click **Finish**.</span></span>

1. <span data-ttu-id="00702-128">Eclipse에서 index.jsp 파일이 hello를 열면 텍스트 toodynamically 디스플레이에서 추가 **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="00702-128">When hello index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="00702-129">hello 기존 내 `<body>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="00702-130">업데이트 한 후 `<body>` 콘텐츠가 hello 다음과 같이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-130">Your updated `<body>` content should appear as hello following:</span></span>
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. <span data-ttu-id="00702-131">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a><span data-ttu-id="00702-132">toodeploy 응용 프로그램 tooAzure, hello 빠르고 간편한 방식으로</span><span class="sxs-lookup"><span data-stu-id="00702-132">toodeploy your application tooAzure, hello quick and simple way</span></span>
<span data-ttu-id="00702-133">Java 웹 응용 프로그램 준비 tootest가 되는 즉시 hello 다음 바로 가기 tootry 것으로 직접 hello Azure에 클라우드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-133">As soon as you have a Java web application ready tootest, you can use hello following shortcut tootry it out directly on hello Azure cloud.</span></span>

1. <span data-ttu-id="00702-134">Eclipse의 프로젝트 탐색기에서 **MyHelloWorld**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-134">In Eclipse's Project Explorer, click **MyHelloWorld**.</span></span>

2. <span data-ttu-id="00702-135">Hello Eclipse 도구 모음을 클릭 hello **게시** 단추를 삭제 하 고 클릭 **게시로 Azure 클라우드 서비스**</span><span class="sxs-lookup"><span data-stu-id="00702-135">In hello Eclipse toolbar, click hello **Publish** drop down button and then click **Publish As Azure Cloud Service**</span></span>

   ![][publishDropdownButton]

3. <span data-ttu-id="00702-136">이 응용 프로그램 tooAzure hello에 대 한 처음으로 게시 하기 전에이 응용 프로그램에 대 한 Azure 배포 프로젝트를 만들지 않은 경우 Azure 배포 프로젝트를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="00702-136">If you are publishing this application tooAzure for hello first time and you have not created an Azure deployment project for this application before, an Azure deployment project be created for you automatically.</span></span> <span data-ttu-id="00702-137">Toorun 응용 프로그램 배포 hello 다음 hello JDK 패키지 및 응용 프로그램 될 서버에 자동으로 나열 하는 프롬프트를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-137">You should see hello following prompt, which also lists hello JDK package and application server that will be automatically deployed toorun your application.</span></span>

   ![][ic789598]
   
   <span data-ttu-id="00702-138">이 바로 가기 접근 방식을 hello 기본값에서 다른 JDK 또는 특정 서버 tooconfigure 필요 없이 쉽고 빠르게 tootest Azure 응용을 프로그램의 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-138">This shortcut approach enables a quick and easy way tootest your application in Azure without having tooconfigure a specific server or JDK that is different from hello defaults.</span></span> <span data-ttu-id="00702-139">Hello 기본값에 만족 하는 경우 클릭할 수 있는 **확인** toocontinue 단계를 수행 하는 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-139">If you are satisfied with hello defaults, you can click **OK** toocontinue with hello following steps.</span></span>
   <span data-ttu-id="00702-140">그러나 toochange 하려는 경우 hello JDK 또는 응용 프로그램에 대 한 응용 프로그램 서버 toouse는 나중에를 자동으로 생성 된 hello Azure 배포 프로젝트를 편집 하 여 정의 하거나 클릭할 수 있는 **취소** 지금은 보기 및 읽기 hello **에 대 한 Azure 배포 프로젝트 섹션** 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-140">However, if you want toochange hello JDK or application server toouse for your application, you can do that later by editing hello Azure deployment project that was automatically created for you, or you can click **Cancel** now and read hello **About Azure deployment projects section** of this tutorial.</span></span>

4. <span data-ttu-id="00702-141">Hello에 **tooAzure 게시** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="00702-141">In hello **Publish tooAzure** dialog:</span></span>

   1. <span data-ttu-id="00702-142">에 없는 경우 없는 구독 tooselect hello **구독** 목록 아직 이러한 단계 tooimport 구독 정보를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-142">If there are no subscriptions tooselect in hello **Subscription** list yet, follow these steps tooimport your subscription information:</span></span>
      1. <span data-ttu-id="00702-143">**게시 설정 파일에서 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-143">Click **Import from PUBLISH-SETTINGS file**.</span></span>
      2. <span data-ttu-id="00702-144">Hello에 **구독 정보 가져오기** 대화 상자를 클릭 하 여 **게시 설정 파일 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-144">In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="00702-145">아직 Azure 계정에 로그인 하지 않은 경우에 증명된 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-145">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="00702-146">다음 메시지가 표시 됩니다 toosave Azure 게시 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-146">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="00702-147">Tooyour 로컬 시스템으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-147">Save it tooyour local machine.</span></span>
      3. <span data-ttu-id="00702-148">Hello에 여전히 **구독 정보 가져오기** 대화 상자에서 hello 클릭 **찾아보기** 단추, 선택 hello hello 이전 단계에서 로컬에 저장 된 설정 파일을 게시 하 고 클릭  **열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-148">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally in hello previous step, and then click **Open**.</span></span> <span data-ttu-id="00702-149">화면에는 비슷한 toohello 다음과 같아야 합니다.![][ic644267]</span><span class="sxs-lookup"><span data-stu-id="00702-149">Your screen should look similar toohello following: ![][ic644267]</span></span>
      4. <span data-ttu-id="00702-150">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-150">Click **OK**.</span></span>
   2. <span data-ttu-id="00702-151">에 대 한 **구독**, 배포에 대 한 사용 하려는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-151">For **Subscription**, select hello subscription that you want use for your deployment.</span></span>
   3. <span data-ttu-id="00702-152">에 대 한 **저장소 계정**, 원하는 toouse, 하거나 클릭 하는 hello 저장소 계정을 선택 **새로** toocreate 새 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-152">For **Storage account**, select hello storage account that you want toouse, or click **New** toocreate a new storage account.</span></span>
   4. <span data-ttu-id="00702-153">에 대 한 **서비스 이름**, 원하는 toouse, 하거나 클릭 하는 hello 클라우드 서비스를 선택 **새로** toocreate 새 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-153">For **Service name**, select hello cloud service that you want toouse, or click **New** toocreate a new cloud service.</span></span>
   5. <span data-ttu-id="00702-154">에 대 한 **대상 OS**선택, hello hello 운영 체제 버전을 배포에 대 한 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-154">For **Target OS**, select hello version of hello operating system that you want toouse for your deployment.</span></span>
   6. <span data-ttu-id="00702-155">**대상 환경**의 경우 자습서의 목적에 따라 **스테이징**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-155">For **Target environment**, for purposes of this tutorial, select **Staging**.</span></span> <span data-ttu-id="00702-156">(준비 toodeploy tooyour 프로덕션 사이트를 때 변경이 너무**프로덕션**.)</span><span class="sxs-lookup"><span data-stu-id="00702-156">(When you're ready toodeploy tooyour production site, you'll change this too**Production**.)</span></span>
   7. <span data-ttu-id="00702-157">선택 사항: 되도록 **이전 배포 덮어쓰기** 덮어쓰기 hello 이전 배포에 새 배포 tooautomatically 원하면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-157">Optional: Ensure that **Overwrite previous deployment** is checked if you want your new deployment tooautomatically overwrite hello previous deployment.</span></span> <span data-ttu-id="00702-158">이 옵션을 사용 하도록 설정 하면 할 수 없습니다 "409 충돌" 문제가 발생 toohello 게시할 때 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-158">When you enable this option, you will not experience "409 conflict" issues when publishing toohello same location.</span></span>
      <span data-ttu-id="00702-159">해당 hello 참고 **tooAzure 게시** 대화에 대 한 구역이 포함 **원격 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-159">Note that hello **Publish tooAzure** dialog contains a section for **Remote Access**.</span></span> <span data-ttu-id="00702-160">기본적으로 원격 액세스가 설정되지 않으며 이 예에서도 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-160">By default, Remote Access is not enabled and we will not enable it for this example.</span></span> <span data-ttu-id="00702-161">원격 액세스 tooenable 원격으로 로그인 할 때 사용자 이름 및 암호 toouse를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-161">tooenable Remote Access, you would enter a user name and password toouse when remotely logging in.</span></span> <span data-ttu-id="00702-162">원격 액세스에 대한 자세한 내용은 [Eclipse에서 Azure 배포에 원격 액세스 사용][Enabling Remote Access for Azure Deployments in Eclipse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00702-162">For more information about Remote Access, see [Enabling Remote Access for Azure Deployments in Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].</span></span>
      <span data-ttu-id="00702-163">프로그램 **tooAzure 게시** 대화 상자가 유사 toohello 다음에 표시 됩니다.![][ic719488]</span><span class="sxs-lookup"><span data-stu-id="00702-163">Your **Publish tooAzure** dialog will appear similar toohello following: ![][ic719488]</span></span>

5. <span data-ttu-id="00702-164">클릭 **게시** toopublish toohello 스테이징 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-164">Click **Publish** toopublish toohello Staging environment.</span></span>

   <span data-ttu-id="00702-165">입력 정보 요청된 tooperform 전체 빌드를 클릭 하면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-165">When prompted tooperform a full build, click **Yes**.</span></span> <span data-ttu-id="00702-166">첫 번째 빌드 hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-166">This may take several minutes for hello first build.</span></span>
   <span data-ttu-id="00702-167">**Azure 활동 로그** 는 Eclipse가 탭된 뷰 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-167">An **Azure Activity Log** will display in your Eclipse tabbed views section.</span></span>
   <span data-ttu-id="00702-168">![][ic719489]있습니다 수이 로그를 사용으로 hello **콘솔** 배포의 toosee hello 진행 상황을 볼 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-168">![][ic719489] You can use this log, as well as hello **Console** view, toosee hello progress of your deployment.</span></span> <span data-ttu-id="00702-169">대체 항목은 toohello에 toolog [Azure 관리 포털][Azure Management Portal], hello를 사용 하 여 **클라우드 서비스** toomonitor hello 상태 섹션.</span><span class="sxs-lookup"><span data-stu-id="00702-169">An alternative is toolog in toohello [Azure Management Portal][Azure Management Portal], and use hello **Cloud Services** section toomonitor hello status.</span></span>

6. <span data-ttu-id="00702-170">배포가 성공적으로 배포 되 면 hello **Azure 활동 로그** 의 상태가 표시 됩니다 **게시 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-170">When your deployment is successfully deployed, hello **Azure Activity Log** will show a status of **Published**.</span></span> <span data-ttu-id="00702-171">클릭 **게시 됨**에서 같이 다음 hello 이미지 및 브라우저에는 배포의 인스턴스로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00702-171">Click **Published**, as shown in hello following image, and your browser will open an instance of your deployment.</span></span>

   ![][ic719490]

<span data-ttu-id="00702-172">스테이징 환경 배포 tooa 이것이 있으므로 hello DNS 이름은 hello http://의 것&lt;*guid*&gt;. hello DNS 이름과 응용 프로그램에 대 한 접미사.cloudapp.net 및 hello URL 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-172">Because this was a deployment tooa staging environment, hello DNS name will be of hello form http://&lt;*guid*&gt;.cloudapp.net, and hello URL will contain hello DNS name plus a suffix for your application.</span></span> <span data-ttu-id="00702-173">예를 들어 http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-173">For example, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld.</span></span> <span data-ttu-id="00702-174">(hello **MyHelloWorld** 부분은 대/소문자 구분입니다.) Hello DNS를 확인할 수 있습니다 (내 hello hello 관리 포털의 클라우드 서비스 부분) hello Azure Platform Management 포털에서에서 hello 배포 이름을 클릭 하면 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-174">(hello **MyHelloWorld** portion is case-sensitive.) You can also see hello DNS name if you click hello deployment name in hello Azure Platform Management Portal (within hello Cloud Services portion of hello management portal).</span></span>

<span data-ttu-id="00702-175">이 연습이 스테이징 환경 배포 toohello에 대 한 없었지만, 배포 tooproduction 뒤 hello 내에서 동일한 단계를 제외 하 고 hello **tooAzure 게시** 대화 상자에서 **프로덕션** 대신 **준비** hello에 대 한 **대상 환경**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-175">Although this walk-through was for a deployment toohello staging environment, a deployment tooproduction follows hello same steps, except within hello **Publish tooAzure** dialog, select **Production** instead of **Staging** for hello **Target environment**.</span></span> <span data-ttu-id="00702-176">배포 tooproduction 스테이징에 사용 되는 GUID 대신, 선택한의 hello DNS 이름에 따라 URL이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-176">A deployment tooproduction results in a URL based on hello DNS name of your choice, instead of a GUID as used for staging.</span></span>

> [!WARNING]
> <span data-ttu-id="00702-177">이 시점에서 Azure 응용 프로그램 toohello 클라우드를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-177">At this point you have deployed your Azure application toohello cloud.</span></span> <span data-ttu-id="00702-178">그러나 계속 하기 전에 배포 된 응용 프로그램 실행 중이지 않은 경우에 크기도 구독에 대 한 청구 가능 시간 tooaccrue를 실현 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-178">However, before proceeding, realize that a deployed application, even if it is not running, will continue tooaccrue billable time for your subscription.</span></span> <span data-ttu-id="00702-179">따라서 Azure 구독에서 원하지 않는 배포를 삭제하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-179">Therefore, it is extremely important that you delete unwanted deployments from your Azure subscription.</span></span>
> 
> 

## <a name="about-azure-deployment-projects"></a><span data-ttu-id="00702-180">Azure 배포 프로젝트 정보</span><span class="sxs-lookup"><span data-stu-id="00702-180">About Azure deployment projects</span></span>
<span data-ttu-id="00702-181">주문 toodeploy 하나 이상의 Java 응용 프로그램 tooAzure, Azure 배포 프로젝트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-181">In order toodeploy one or more Java applications tooAzure, an Azure Deployment Project is needed.</span></span> <span data-ttu-id="00702-182">응용 프로그램에서 Azure에 게시 된 순서 toobe 바꿈하여 toobe 필요 "패키지" hello의 hello 역할을 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-182">It plays hello role of hello "package" that your applications need toobe wrapped into in order toobe published on Azure.</span></span>

<span data-ttu-id="00702-183">응용 프로그램에 대 한 hello 정보 외에도 Azure 배포 프로젝트에 대 한 정보도 다른 주요 구성 요소 배포의 가장 중요 하 게: 응용 프로그램 서버 컨테이너 toorun 웹 응용 프로그램에서는 hello 및 Java 런타임 toorun hello 것 켜 집니다.</span><span class="sxs-lookup"><span data-stu-id="00702-183">Besides hello information about your applications, an Azure deployment project also contains information about other key components of your deployment, most importantly: hello application server container toorun your web app in, and hello Java runtime toorun it on.</span></span> <span data-ttu-id="00702-184">Azure에서는 선택할 수 있는 여러 Java 런타임 및 Java 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-184">Azure supports a large selection of Java runtimes and Java application servers you can choose from.</span></span>

<span data-ttu-id="00702-185">Azure 배포 프로젝트도 toocreate 복잡, 확장성, 항상 사용 가능한 수 있는 기타 중요 한 구성 정보를 포함할 수 있습니다 하지만 여기에 hello 예제 교육용으로 상당히 단순화 되었지만 다중 계층 클라우드 서비스를 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-185">Although hello example used here is greatly simplified for educational purposes, an Azure deployment project can also contain other important configuration information that enables you toocreate almost arbitrarily complex, scalable, highly available, multi-tier cloud services with your applications.</span></span> <span data-ttu-id="00702-186">**세션 선호도("고정 세션")**, **빠른 캐싱**, **SSL 오프로딩**, **방화벽/포트 라우팅**, **원격 액세스** 및 다른 다양한 강력한 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-186">You can enable **session affinity ("sticky sessions")**, **fast caching**, **SSL offloading**, **firewall/port routing**, **remote access**, and a number of other powerful capabilities.</span></span>

<span data-ttu-id="00702-187">이 자습서의 hello 이전 단원을 완료 한 경우 ("toodeploy 응용 프로그램 tooAzure, hello 빠르고 간편한 방식으로"), 프로젝트 탐색기 자동으로 생성 되며 이름이 hello에 새 Azure 배포 프로젝트 표시 " **MyHelloWorld_onAzure**"입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-187">If you've completed hello previous section of this tutorial ("toodeploy your application tooAzure, hello quick and simple way"), you will now see a new Azure deployment project in hello Project Explorer generated for you automatically and named "**MyHelloWorld_onAzure**".</span></span>

<span data-ttu-id="00702-188">먼저 빈 Azure 배포 프로젝트를 직접 만드는 하 여 응용 프로그램 tooit 추가 하 여이 자습서를 시작할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-188">You could have also started this tutorial by first creating a blank Azure deployment project yourself and then adding your application(s) tooit.</span></span> <span data-ttu-id="00702-189">더 길 하지만 hello hello 시작 부분에서 초기 구성 보다 더 세밀 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-189">It is a longer process, but giving you more control over hello initial configuration from hello beginning.</span></span>

<span data-ttu-id="00702-190">처음부터 새 Azure 배포 프로젝트 toocreate 클릭 hello **새 Azure 배포 프로젝트** 단추 ![][ic710876]합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-190">toocreate a new Azure deployment project from scratch, click hello **New Azure Deployment Project** button ![][ic710876].</span></span>

<span data-ttu-id="00702-191">여부 이미 기존 Azure 배포 프로젝트를 사용 하거나 처음부터 다시 만드는지에는 관계 없이 수 toochange의 구성 설정과 같은 hello JDK 구성 요소 또는 응용 프로그램 서버를 쉽게 동일 하 게 hello 언제 든 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-191">Regardless of whether you are working with an already existing Azure deployment project, or creating one from scratch, you are able toochange its configuration settings and components, such as hello JDK or hello application server, equally easily at any time.</span></span>

<span data-ttu-id="00702-192">toochange hello JDK, 또는 hello 응용 프로그램 서버 또는 기존 Azure 배포 프로젝트의 응용 프로그램 목록 hello:</span><span class="sxs-lookup"><span data-stu-id="00702-192">toochange hello JDK, or hello application server, or hello application list in an existing Azure deployment project:</span></span>

1. <span data-ttu-id="00702-193">Hello 프로젝트 노드를 확장 (예: **MyHelloWorld_onAzure**) hello 프로젝트 탐색기에서</span><span class="sxs-lookup"><span data-stu-id="00702-193">Expand hello project node (e.g. **MyHelloWorld_onAzure**) in hello Project Explorer</span></span>

2. <span data-ttu-id="00702-194">**WorkerRole1**</span><span class="sxs-lookup"><span data-stu-id="00702-194">Right-click **WorkerRole1**</span></span>

3. <span data-ttu-id="00702-195">Hello 확장 **Azure** hello 상황에 맞는 메뉴에서 하위 메뉴</span><span class="sxs-lookup"><span data-stu-id="00702-195">Expand hello **Azure** submenu in hello context menu</span></span>

4. <span data-ttu-id="00702-196">**서버 구성**</span><span class="sxs-lookup"><span data-stu-id="00702-196">Click **Server Configuration**</span></span>

<span data-ttu-id="00702-197">에 관계 없이, 위에 표시 된 대로 기존 Azure 배포 프로젝트를 편집 하 여 이러한 서버 구성 단계를 시작 또는 새로 처음부터 새로 만드는, 나타납니다 hello 같은 유형의 대화 상자가 tooconfigure JDK, 서버 및 응용 프로그램 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-197">Regardless of whether you started these server configuration steps by editing an existing Azure deployment project as shown above, or creating a new one from scratch, you will see hello same type of dialogs allowing you tooconfigure your JDK, server and application components.</span></span> <span data-ttu-id="00702-198">toolearn 방법을 더 toochange hello 설정을 toochange hello JDK, 예를 들어 이러한 대화 상자에서 응용 프로그램 서버 hello 추가 하거나 제거할 응용 프로그램 배포의 경우 참조 hello [서버 구성 속성] [ Server configuration properties] 문서.</span><span class="sxs-lookup"><span data-stu-id="00702-198">toolearn more how toochange hello settings in those dialogs, for example toochange hello JDK, hello application server and add or remove applications in a deployment, see hello [Server configuration properties][Server configuration properties] article.</span></span>

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a><span data-ttu-id="00702-199">Windows에만 해당: toodeploy 응용 프로그램 toohello 계산 에뮬레이터</span><span class="sxs-lookup"><span data-stu-id="00702-199">Windows only: toodeploy your application toohello compute emulator</span></span>

> [!NOTE]
> <span data-ttu-id="00702-200">Windows hello Azure 에뮬레이터를 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-200">hello Azure emulator is only available on Windows.</span></span> <span data-ttu-id="00702-201">Windows 이외의 운영 체제를 사용하는 경우 이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="00702-201">Skip this section if you are using an operating system other than Windows.</span></span>
> 
> 

<span data-ttu-id="00702-202">응용 프로그램 tooAzure 프로그램을 게시 하 여 이전 버전, 즉, 암시적으로 설명 하는 hello 단계에 따라 새 Azure 배포 프로젝트를 만든 경우 hello JDK 및 로컬 에뮬레이션 아니라 hello 클라우드에 대 한 응용 프로그램 서버가 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-202">If you have created a new Azure deployment project following hello steps described earlier, i.e. implicitly, by publishing your application tooAzure, hello JDK and application servers have been configured for hello cloud, but not for local emulation.</span></span> <span data-ttu-id="00702-203">tooprepare hello 로컬 에뮬레이터에서 테스트할 프로젝트를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-203">tooprepare your project for testing in hello local emulator, follow these steps:</span></span>

1. <span data-ttu-id="00702-204">Eclipse의 프로젝트 탐색기에서 **MyHelloWorld_onAzure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-204">In Eclipse's Project Explorer, click **MyHelloWorld_onAzure**.</span></span>

2. <span data-ttu-id="00702-205">마우스 오른쪽 단추로 **WorkerRole1**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-205">Right-click on **WorkerRole1**.</span></span>

3. <span data-ttu-id="00702-206">Hello 확장 **Azure** hello 상황에 맞는 메뉴에서 하위 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-206">Expand hello **Azure** submenu in hello context menu.</span></span>

4. <span data-ttu-id="00702-207">**서버 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-207">Click **Server Configuration**.</span></span>

5. <span data-ttu-id="00702-208">Hello에 **JDK** 탭에서 hello 도구 키트를 기본 구성 전 확인 로컬 JDK를 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-208">On hello **JDK** tab, check if hello toolkit has pre-configured a default local JDK for you.</span></span> <span data-ttu-id="00702-209">그렇지 않은 경우 또는 toochange hello 기본값 간주 하려는 경우 해당 hello 확인 **로컬 테스트를 위해이 파일 경로의 JDK 사용 하 여 hello** 확인란이 선택 되어 있으며 hello toouse 하려는 JDK 설치 위치가 지정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-209">If not, or if you want toochange hello assumed defaults, ensure that hello **Use hello JDK from this file path for testing locally** checkbox is checked and hello JDK installation location that you want toouse is specified.</span></span> <span data-ttu-id="00702-210">Toochange 하려는 경우, hello 클릭 **찾아보기** 단추 및 hello JDK toouse의 hello 디렉터리 위치를 선택 hello 찾아보기 컨트롤을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-210">If you want toochange it, click hello **Browse** button and using hello browse control, select hello directory location of hello JDK toouse.</span></span>

6. <span data-ttu-id="00702-211">Hello 클릭 **서버** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-211">Click hello **Server** tab.</span></span>

7. <span data-ttu-id="00702-212">Hello에 **로컬 서버 경로** hello hello 대화 상자 맨 아래에 텍스트 상자 hello 유형과 hello 대화 상자에서 hello 맨 아래에서 선택한 hello 서버의 주 버전 번호와 일치 하는 로컬에 설치 된 서버 hello 경로 입력 합니다. hello **이 유형의 서버를 배포** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-212">In hello **Local server path** text box at hello bottom of hello dialog box, enter hello path of a locally-installed server that matches hello type and major version number of hello server selected at hello top of hello dialog box, under hello **Deploy a server of this type** checkbox.</span></span> <span data-ttu-id="00702-213">다른 유형 또는 hello 응용 프로그램 서버의 주 버전 toouse를 원하는 경우 먼저 해당 확인란 아래에서 선택 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-213">If you want toouse a different type or major version of hello application server, change hello selection under that checkbox first.</span></span>

8. <span data-ttu-id="00702-214">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-214">Click **OK**.</span></span>

9. <span data-ttu-id="00702-215">Hello Eclipse 도구 모음을 클릭 hello **Azure 에뮬레이터에서 실행** 단추, ![][ic710879]합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-215">In hello Eclipse toolbar, click hello **Run in Azure Emulator** button, ![][ic710879].</span></span> <span data-ttu-id="00702-216">경우 hello **Azure 에뮬레이터에서 실행** 단추가 활성화 되지 않으면, 되도록 **MyHelloWorld_onAzure** Eclipse의 프로젝트 탐색기에서 선택 되어 있으며 Eclipse 프로젝트 탐색기 hello로 포커스에 있는지 확인 현재 창입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-216">If hello **Run in Azure Emulator** button is not enabled, ensure that **MyHelloWorld_onAzure** is selected in Eclipse's Project Explorer, and ensure that Eclipse's Project Explorer has focus as hello current window.</span></span> <span data-ttu-id="00702-217">프로젝트의 전체 빌드를 처음 시작 되 고 hello 계산 에뮬레이터에서 Java 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-217">This will first start a full build of your project and then launch your Java web application in hello compute emulator.</span></span> <span data-ttu-id="00702-218">(참고 컴퓨터의 성능 특성에 따라는 hello 첫 번째 빌드의 몇 초 tooa 몇 분까지 걸릴 수 있습니다 있지만 후속 빌드는 훨씬 빨라집니다.) Hello 첫 번째 빌드 단계가 완료 된 후 메시지가 표시 됩니다 tooallow Windows 사용자 계정 컨트롤 (UAC)이 명령 toomake tooyour 컴퓨터를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-218">(Note that depending on your computer's performance characteristics, hello first build may take between a few seconds tooa few minutes, but subsequent builds will get faster.) After hello first build step has been completed, you will be prompted by Windows User Account Control (UAC) tooallow this command toomake changes tooyour computer.</span></span> <span data-ttu-id="00702-219">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-219">Click **Yes**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00702-220">Hello UAC 프롬프트를 체크 hello UAC 아이콘에 대 한 Windows 작업 표시줄 hello 및 처음 클릭 표시 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-220">If you do not see hello UAC prompt, check hello Windows taskbar for hello UAC icon and click it first.</span></span> <span data-ttu-id="00702-221">경우에 따라 hello UAC 프롬프트 최상위 창으로 표시 되지 않으면 아니라 작업 표시줄 아이콘 으로만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00702-221">Sometimes hello UAC prompt does not show up as a topmost window, but is visible only as a taskbar icon.</span></span>
> 
> 

1. <span data-ttu-id="00702-222">프로젝트와 함께 모든 문제가 있는 경우 계산 에뮬레이터 UI toodetermine hello의 hello 출력을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-222">Examine hello output of hello compute emulator UI toodetermine if there are any issues with your project.</span></span> <span data-ttu-id="00702-223">배포의 hello 내용에 따라 완전히 hello 계산 에뮬레이터 내에서 시작 하 여 응용 프로그램 toobe 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00702-223">Depending on hello contents of your deployment, it may take a couple minutes for your application toobe fully started within hello compute emulator.</span></span>

2. <span data-ttu-id="00702-224">브라우저를 시작 하 고 hello URL을 사용 하 여 `http://localhost:8080/MyHelloWorld` hello 주소로 (hello `MyHelloWorld` hello URL의 일부는 대/소문자 구분).</span><span class="sxs-lookup"><span data-stu-id="00702-224">Start your browser and use hello URL `http://localhost:8080/MyHelloWorld` as hello address (hello `MyHelloWorld` portion of hello URL is case-sensitive).</span></span> <span data-ttu-id="00702-225">MyHelloWorld 응용 프로그램 (index.jsp의 출력 hello), 다음 이미지와 비슷한 toohello 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-225">You should see your MyHelloWorld application (hello output of index.jsp), similar toohello following image:</span></span>

   ![][ic589579]

<span data-ttu-id="00702-226">준비 toostop hello Eclipse 도구 모음에서 hello 계산 에뮬레이터에서 실행 되는 응용 프로그램 클릭 hello **Azure 에뮬레이터 재설정** 단추, ![][ic710880]합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-226">When you are ready toostop your application from running in hello compute emulator, in hello Eclipse toolbar, click hello **Reset Azure Emulator** button, ![][ic710880].</span></span>

## <a name="toodelete-your-deployment"></a><span data-ttu-id="00702-227">toodelete 배포</span><span class="sxs-lookup"><span data-stu-id="00702-227">toodelete your deployment</span></span>
<span data-ttu-id="00702-228">toodelete hello Eclipse 용 Azure 도구 키트 내에서 배포 되도록 **MyHelloWorld_onAzure** 는 hello Eclipse 프로젝트 탐색기에 초점을 맞추고 하 고 클릭 한 다음 현재 창이 hello 확인 Eclipse의 프로젝트 탐색기에서 선택 hello **게시 취소** 단추 ![][ic710883], hello Eclipse 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-228">toodelete your deployment within hello Azure Toolkit for Eclipse, ensure that **MyHelloWorld_onAzure** is selected in Eclipse's Project Explorer, ensure hello Eclipse Project Explorer has hello current window focus, and then click hello **Unpublish** button, ![][ic710883], in hello Eclipse toolbar.</span></span> <span data-ttu-id="00702-229">(작업을 수행할 수 있습니다 동일한 작업을 마우스 오른쪽 단추로 클릭 하 여 hello **MyHelloWorld_onAzure** 클릭 하면 Eclipse의 프로젝트 탐색기에서 **Azure** 클릭 한 다음 **Azure클라우드에서배포취소**.) Hello 나타납니다 **Azure 프로젝트 게시 취소** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="00702-229">(You could do hello same operation by right-clicking **MyHelloWorld_onAzure** in Eclipse's Project Explorer, clicking **Azure** and then clicking **Undeploy from Azure Cloud**.) This will display hello **Unpublish Azure Project** dialog.</span></span>

![][ic719491]

<span data-ttu-id="00702-230">배포, toodelete를 원하고 클릭 한 다음 선택 hello 배포에 포함 된 hello 구독 및 클라우드 서비스를 선택 **게시 취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-230">Select hello subscription and cloud service that contains your deployment, select hello deployment that you want toodelete, and then click **Unpublish**.</span></span>

<span data-ttu-id="00702-231">(대체 toousing hello toolkit toodelete hello 배포는 toouse hello **클라우드 서비스** hello Azure 관리 포털의 섹션: tooyour 배포를 이동, 선택한 hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="00702-231">(An alternative toousing hello toolkit toodelete hello deployment is toouse hello **Cloud Services** section of hello Azure Management Portal: Navigate tooyour deployment, select it, and then click hello **Delete** button.</span></span> <span data-ttu-id="00702-232">이을 중지 하 고 삭제 한 다음 hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-232">This will stop, and then delete, hello deployment.</span></span> <span data-ttu-id="00702-233">Toostop hello 배포 높은 사람만 삭제 하는 경우 hello를 클릭 합니다. **중지** hello 대신 단추가 **삭제** 단추를 위에서 설명한 대로 하지만 청구 가능한 요금이 hello 배포를 삭제 하지 않는 경우 계속 tooaccrue 배포에 대 한 중지 된 경우에).</span><span class="sxs-lookup"><span data-stu-id="00702-233">If you only want toostop hello deployment and not delete it, click hello **Stop** button instead of hello **Delete** button, but as mentioned above, if you do not delete hello deployment, billable charges will continue tooaccrue for your deployment even if it is stopped).</span></span>

## <a name="see-also"></a><span data-ttu-id="00702-234">참고 항목</span><span class="sxs-lookup"><span data-stu-id="00702-234">See Also</span></span>
<span data-ttu-id="00702-235">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="00702-235">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="00702-236">[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="00702-236">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="00702-237">[Hello Azure Toolkit for Eclipse에서 새로운 이란][What's New in hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="00702-237">[What's New in hello Azure Toolkit for Eclipse][What's New in hello Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="00702-238">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="00702-238">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
