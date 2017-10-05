---
title: "Azure에서 첫 번째 Java 웹앱 만들기"
description: "기본 Java 앱을 배포하여 App Service에서 웹앱을 실행하는 방법을 알아봅니다."
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
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="b83d4-103">Azure에서 첫 번째 Java 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b83d4-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="b83d4-104">[Azure App Service](../app-service/app-service-value-prop-what-is.md)의 [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 기능은 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b83d4-105">이 빠른 시작에서는 [Eclipse IDE for Java EE Developers](http://www.eclipse.org/)를 사용하여 App Service에 Java 웹앱을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="b83d4-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b83d4-108">Prerequisites</span></span>

<span data-ttu-id="b83d4-109">이 빠른 시작을 완료하려면 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="b83d4-110">무료 [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b83d4-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="b83d4-111">이 빠른 시작은 Eclipse Neon을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="b83d4-112">[Eclipse용 Azure 도구 키트](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="b83d4-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="b83d4-113">Eclipse에서 동적 웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b83d4-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="b83d4-114">Eclipse에서 **파일** > **새로 만들기** > **동적 웹 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="b83d4-115">**새 동적 웹 프로젝트** 대화 상자에서 프로젝트의 이름을 **MyFirstJavaOnAzureWebApp**으로 지정하고 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![새 동적 웹 프로젝트 대화 상자](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="b83d4-117">JSP 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="b83d4-117">Add a JSP page</span></span>

<span data-ttu-id="b83d4-118">프로젝트 탐색기 표시되지 않으면 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-118">If Project Explorer is not displayed, restore it.</span></span>

![Eclipse용 Java EE 작업 영역](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="b83d4-120">프로젝트 탐색기에서 **MyFirstJavaOnAzureWebApp** 프로젝트를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="b83d4-121">**WebContent**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** > **JSP 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![프로젝트 탐색기에서 새 JSP 파일에 대한 메뉴](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="b83d4-123">**새 JSP 파일** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="b83d4-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="b83d4-124">파일 이름을 **index.jsp**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="b83d4-125">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-125">Select **Finish**.</span></span>

  ![새 JSP 파일 대화 상자](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="b83d4-127">index.jsp 파일에서 `<body></body>` 요소를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="b83d4-128">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="b83d4-129">Azure에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="b83d4-129">Publish the web app to Azure</span></span>

<span data-ttu-id="b83d4-130">프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **Azure** > **Azure 웹앱으로 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Azure 웹앱으로 게시 상황에 맞는 메뉴](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="b83d4-132">**Azure 로그인** 대화 상자에서 **대화형** 옵션을 유지한 다음 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="b83d4-133">로그인 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="b83d4-134">웹앱 배포 대화 상자</span><span class="sxs-lookup"><span data-stu-id="b83d4-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="b83d4-135">Azure 계정에 로그인하면 **웹앱 배포** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="b83d4-136">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-136">Select **Create**.</span></span>

![웹앱 배포 대화 상자](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="b83d4-138">앱 서비스 만들기 대화 상자</span><span class="sxs-lookup"><span data-stu-id="b83d4-138">Create App Service dialog box</span></span>

<span data-ttu-id="b83d4-139">기본 값으로 **App Service 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="b83d4-140">다음 이미지에 표시된 숫자 **170602185241**은 대화 상자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![앱 서비스 만들기 대화 상자](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="b83d4-142">**App Service 만들기** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="b83d4-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="b83d4-143">웹앱에 대해 생성된 이름을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="b83d4-144">이 이름은 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-144">This name must be unique across Azure.</span></span> <span data-ttu-id="b83d4-145">이름은 웹앱에 대한 URL 주소의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="b83d4-146">예: 웹앱 이름이 **MyJavaWebApp**이면 URL은 *myjavawebapp.azurewebsites.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="b83d4-147">기본 웹 컨테이너를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-147">Keep the default web container.</span></span>
* <span data-ttu-id="b83d4-148">Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="b83d4-149">**App Service 계획** 탭에서:</span><span class="sxs-lookup"><span data-stu-id="b83d4-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="b83d4-150">**새로 만들기**: App Service 계획의 이름인 기본값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="b83d4-151">**위치**: **유럽 서부** 또는 인접 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="b83d4-152">**가격 책정 계층**: 무료 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="b83d4-153">기능의 경우 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b83d4-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![앱 서비스 만들기 대화 상자](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="b83d4-155">리소스 그룹 탭</span><span class="sxs-lookup"><span data-stu-id="b83d4-155">Resource group tab</span></span>

<span data-ttu-id="b83d4-156">**리소스 그룹** 탭을 선택합니다. 리소스 그룹에 대해 기본 생성된 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![리소스 그룹 탭](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="b83d4-158">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="b83d4-159">Azure 도구 키트는 웹앱을 만들고 진행률 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![App Service 만들기 진행률 대화 상자](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="b83d4-161">웹앱 배포 대화 상자</span><span class="sxs-lookup"><span data-stu-id="b83d4-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="b83d4-162">**웹앱 배포** 대화 상자에서 **루트에 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="b83d4-163">앱 서비스가 *wingtiptoys.azurewebsites.net*에 있는데 이 루트에 배포하지 않으면 **MyFirstJavaOnAzureWebApp** 웹앱이 *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![웹앱 배포 대화 상자](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="b83d4-165">대화 상자는 Azure, JDK 및 웹 컨테이너 선택 영역을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="b83d4-166">**배포**를 선택하여 Azure에 웹앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="b83d4-167">게시 작업을 마치면 **Azure 활동 로그** 대화 상자에서 **게시됨** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Azure 활동 로그 대화 상자](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="b83d4-169">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-169">Congratulations!</span></span> <span data-ttu-id="b83d4-170">Azure에 웹앱을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-170">You have successfully deployed your web app to Azure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="b83d4-173">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="b83d4-173">Update the web app</span></span>

<span data-ttu-id="b83d4-174">샘플 JSP 코드를 다른 메시지로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="b83d4-175">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-175">Save the changes.</span></span>

<span data-ttu-id="b83d4-176">프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **Azure** > **Azure 웹앱으로 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="b83d4-177">**웹앱 배포** 대화 상자가 표시되고 이전에 만든 앱 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="b83d4-178">게시할 때마다 **루트에 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="b83d4-179">웹앱을 선택하고 변경 사항을 게시하는 **배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="b83d4-180">**게시** 링크가 표시되는 경우 웹앱으로 이동하도록 선택하고 변경 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="b83d4-181">웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="b83d4-181">Manage the web app</span></span>

<span data-ttu-id="b83d4-182">만든 웹앱을 보려면 <a href="https://portal.azure.com" target="_blank">Azure Portal</a>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="b83d4-183">왼쪽 메뉴에서 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-183">From the left menu, select **Resource Groups**.</span></span>

![리소스 그룹으로 포털 탐색](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="b83d4-185">리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-185">Select the resource group.</span></span> <span data-ttu-id="b83d4-186">페이지에서 이 빠른 시작에서 만든 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-186">The page shows the resources that you created in this quickstart.</span></span>

![리소스 그룹 myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="b83d4-188">웹앱을 선택합니다(이전 이미지에서 **webapp-170602193915**).</span><span class="sxs-lookup"><span data-stu-id="b83d4-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="b83d4-189">**개요** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-189">The **Overview** page appears.</span></span> <span data-ttu-id="b83d4-190">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="b83d4-191">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="b83d4-192">페이지의 왼쪽에 있는 탭에서는 열 수 있는 다른 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83d4-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Azure Portal의 App Service 페이지](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="b83d4-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b83d4-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b83d4-195">사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="b83d4-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
