---
title: "aaaCreate Azure에서 첫 번째 Java 웹 앱"
description: "기본 Java 응용 프로그램을 배포 하 여 toorun 앱 서비스에서 앱 웹 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="671b2-103">Azure에서 첫 번째 Java 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="671b2-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="671b2-104">hello [웹 앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 의 기능 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 자체 패치, 확장성이 뛰어난 웹 호스팅 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="671b2-105">이 퀵 스타트의 toodeploy Java 앱 tooApp 서비스 hello를 사용 하 여 웹 하는 방법을 보여 줍니다. [Eclipse IDE for Java EE Developers](http://www.eclipse.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="671b2-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="671b2-108">Prerequisites</span></span>

<span data-ttu-id="671b2-109">toocomplete이 빠른이 시작 설치:</span><span class="sxs-lookup"><span data-stu-id="671b2-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="671b2-110">무료 hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="671b2-111">이 빠른 시작은 Eclipse Neon을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="671b2-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="671b2-113">Eclipse에서 동적 웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="671b2-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="671b2-114">Eclipse에서 **파일** > **새로 만들기** > **동적 웹 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="671b2-115">Hello에 **새 동적 웹 프로젝트** 대화 상자, 이름 hello 프로젝트 **MyFirstJavaOnAzureWebApp**를 선택 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![새 동적 웹 프로젝트 대화 상자](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="671b2-117">JSP 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="671b2-117">Add a JSP page</span></span>

<span data-ttu-id="671b2-118">프로젝트 탐색기 표시되지 않으면 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-118">If Project Explorer is not displayed, restore it.</span></span>

![Eclipse용 Java EE 작업 영역](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="671b2-120">프로젝트 탐색기에서 확장 hello **MyFirstJavaOnAzureWebApp** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="671b2-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="671b2-121">**WebContent**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** > **JSP 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![프로젝트 탐색기에서 새 JSP 파일에 대한 메뉴](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="671b2-123">Hello에 **JSP 파일 새로** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="671b2-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="671b2-124">이름 hello 파일 **index.jsp**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="671b2-125">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-125">Select **Finish**.</span></span>

  ![새 JSP 파일 대화 상자](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="671b2-127">Hello index.jsp 파일에서 대체 hello `<body></body>` 요소 태그를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="671b2-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="671b2-128">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="671b2-129">웹 앱 tooAzure hello 게시</span><span class="sxs-lookup"><span data-stu-id="671b2-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="671b2-130">프로젝트 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Azure** > **Azure 웹 앱으로 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Azure 웹앱으로 게시 상황에 맞는 메뉴](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="671b2-132">Hello에 **Azure 로그인** 대화 상자, 유지 hello **Interactive'** 옵션을 선택한 다음 선택 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="671b2-133">Hello 로그인 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="671b2-134">웹앱 배포 대화 상자</span><span class="sxs-lookup"><span data-stu-id="671b2-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="671b2-135">Tooyour Azure 계정에에서 로그인 한 후 hello **웹 응용 프로그램 배포** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="671b2-136">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-136">Select **Create**.</span></span>

![웹앱 배포 대화 상자](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="671b2-138">앱 서비스 만들기 대화 상자</span><span class="sxs-lookup"><span data-stu-id="671b2-138">Create App Service dialog box</span></span>

<span data-ttu-id="671b2-139">hello **응용 프로그램 서비스 만들기** 기본 값으로 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="671b2-140">번호 hello **170602185241** hello 뒤에 표시 된 이미지 대화 상자에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![앱 서비스 만들기 대화 상자](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="671b2-142">Hello에 **응용 프로그램 서비스 만들기** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="671b2-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="671b2-143">Hello 웹 앱에 대 한 이름을 생성 하는 hello를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="671b2-144">이 이름은 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-144">This name must be unique across Azure.</span></span> <span data-ttu-id="671b2-145">hello 이름은 hello 웹 앱에 대 한 hello URL 주소의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="671b2-146">예를 들어: hello 웹 응용 프로그램 이름이 **MyJavaWebApp**, URL은 hello *myjavawebapp.azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="671b2-147">Hello 기본 웹 컨테이너를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-147">Keep hello default web container.</span></span>
* <span data-ttu-id="671b2-148">Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="671b2-149">Hello에 **앱 서비스 계획** 탭:</span><span class="sxs-lookup"><span data-stu-id="671b2-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="671b2-150">**새로 만들기**: 이름인 hello hello 앱 서비스 계획의 hello 기본값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="671b2-151">**위치**: **유럽 서부** 또는 인접 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="671b2-152">**가격 책정 계층**: 선택 hello 무료 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="671b2-153">기능의 경우 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="671b2-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![앱 서비스 만들기 대화 상자](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="671b2-155">리소스 그룹 탭</span><span class="sxs-lookup"><span data-stu-id="671b2-155">Resource group tab</span></span>

<span data-ttu-id="671b2-156">선택 hello **리소스 그룹** 탭 합니다. Hello 리소스 그룹에 대 한 hello 생성 된 기본 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![리소스 그룹 탭](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="671b2-158">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="671b2-159">hello Azure 도구 키트 hello 웹 앱을 만들고 한 진행률 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![App Service 만들기 진행률 대화 상자](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="671b2-161">웹앱 배포 대화 상자</span><span class="sxs-lookup"><span data-stu-id="671b2-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="671b2-162">Hello에 **웹 응용 프로그램 배포** 대화 상자에서 **tooroot 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="671b2-163">응용 프로그램 서비스에 있는 경우 *wingtiptoys.azurewebsites.net* toohello 루트, 라는 hello 웹 앱을 배포 하지 않는 및 **MyFirstJavaOnAzureWebApp** 너무 배포 *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![웹앱 배포 대화 상자](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="671b2-165">hello 대화 상자 표시 hello Azure, JDK, 및 웹 컨테이너 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="671b2-166">선택 **배포** toopublish hello 웹 응용 프로그램 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="671b2-167">Hello 게시 완료 되 면 선택 hello **게시 됨** hello에 대 한 링크 **Azure 활동 로그** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="671b2-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Azure 활동 로그 대화 상자](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="671b2-169">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-169">Congratulations!</span></span> <span data-ttu-id="671b2-170">웹 앱 tooAzure 성공적으로 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="671b2-173">Hello 웹 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="671b2-173">Update hello web app</span></span>

<span data-ttu-id="671b2-174">Hello 샘플 JSP 코드 tooa 서로 다른 메시지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="671b2-175">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-175">Save hello changes.</span></span>

<span data-ttu-id="671b2-176">프로젝트 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Azure** > **Azure 웹 앱으로 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="671b2-177">hello **웹 응용 프로그램 배포** 표시 hello 이전에 만든 응용 프로그램 서비스와 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="671b2-178">선택 **tooroot 배포** 게시 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="671b2-179">Hello 웹 사이트를 선택 하 고 선택 **배포**,이 명령은 hello 변경 내용을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="671b2-180">Hello 때 **게시** 링크가 표시 toobrowse toohello 웹 앱을 선택 하 고 hello 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="671b2-181">Hello 웹 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="671b2-181">Manage hello web app</span></span>

<span data-ttu-id="671b2-182">Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toosee hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="671b2-183">Hello 왼쪽된 메뉴에서 선택 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-183">From hello left menu, select **Resource Groups**.</span></span>

![포털 탐색 tooresource 그룹](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="671b2-185">Hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-185">Select hello resource group.</span></span> <span data-ttu-id="671b2-186">hello 페이지에는이 빠른 시작에서 만든 hello 리소스가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-186">hello page shows hello resources that you created in this quickstart.</span></span>

![리소스 그룹 myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="671b2-188">웹 앱 선택 hello (**webapp 170602193915** hello 이미지 앞에).</span><span class="sxs-lookup"><span data-stu-id="671b2-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="671b2-189">hello **개요** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-189">hello **Overview** page appears.</span></span> <span data-ttu-id="671b2-190">이 페이지에서는 hello 응용 프로그램에서 수행 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="671b2-191">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="671b2-192">hello 탭 hello hello 페이지의 왼쪽에 열 수 있는 다양 한 구성 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="671b2-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Azure Portal의 App Service 페이지](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="671b2-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="671b2-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="671b2-195">사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="671b2-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
