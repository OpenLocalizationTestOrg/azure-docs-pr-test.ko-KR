---
title: "Application Insights에 대한 릴리스 주석 | Microsoft Docs"
description: "Application Insights에서 배포 또는 빌드 표식을 메트릭 탐색기 차트에 추가합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="31b06-103">Application Insights의 메트릭 차트에 대한 주석</span><span class="sxs-lookup"><span data-stu-id="31b06-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="31b06-104">[메트릭 탐색기](app-insights-metrics-explorer.md) 차트의 주석은 새 빌드를 배포한 위치 또는 다른 중요한 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="31b06-105">릴리스 주석으로 변경 내용이 응용 프로그램의 성능에 영향을 주는지 여부를 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="31b06-106">릴리스 주석은 [Visual Studio Team Services 빌드 시스템](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs)에서 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="31b06-107">[PowerShell에서 만들어](#create-annotations-from-powershell) 원하는 이벤트에 대한 플래그를 지정하는 주석을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![서버 응답 시간과 상관 관계가 표시된 주석 예제](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="31b06-109">VSTS 빌드를 사용한 릴리스 주석</span><span class="sxs-lookup"><span data-stu-id="31b06-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="31b06-110">릴리스 주석은 클라우드 기반 빌드 기능 및 Visual Studio Team Services 릴리스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="31b06-111">주석 확장 설치(한 번)</span><span class="sxs-lookup"><span data-stu-id="31b06-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="31b06-112">릴리스 주석을 만들려면 Visual Studio 마켓플레이스에서 사용 가능한 여러 Team Service 확장 중 하나를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="31b06-113">[Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) 프로젝트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="31b06-114">Visual Studio 마켓플레이스의 [릴리스 주석 확장을 가져와서](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)팀 서비스 계정에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![Team Services 웹 페이지의 오른쪽 위에서 마켓플레이스를 엽니다.](./media/app-insights-annotations/10.png)

<span data-ttu-id="31b06-117">Visual Studio Team Services 계정에 대해 이 작업을 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="31b06-118">이제 계정의 모든 프로젝트에 대해 릴리스 주석을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="31b06-119">릴리스 주석 구성</span><span class="sxs-lookup"><span data-stu-id="31b06-119">Configure release annotations</span></span>

<span data-ttu-id="31b06-120">각 VSTS 릴리스 템플릿에 대한 별도의 API 키를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="31b06-121">[Microsoft Azure 포털](https://portal.azure.com) 에 로그인하고 응용 프로그램을 모니터링하는 Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="31b06-122">(또는 아직 만들지 않은 경우 [지금 만듭니다](app-insights-overview.md).)</span><span class="sxs-lookup"><span data-stu-id="31b06-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="31b06-123">**API 액세스**, **Application Insights ID**를 차례로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![portal.azure.com에서 Application Insights 리소스를 열고 설정을 선택합니다.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="31b06-127">별도의 브라우저 창에서, Visual Studio Team Services에서 배포를 관리하는 릴리스 템플릿을 열거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="31b06-128">작업을 추가하고 메뉴에서 Application Insights 릴리스 주석 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="31b06-129">API 액세스 블레이드에서 복사한 **응용 프로그램 ID** 를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![Visual Studio Team Services에서 릴리스를 열고 릴리스 정의를 선택하고 편집을 선택합니다.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="31b06-133">**APIKey** 필드를 변수 `$(ApiKey)`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="31b06-134">Azure 창으로 돌아가 새 API 키를 만들어 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Azure 창의 API 액세스 블레이드에서 API 키 만들기를 클릭합니다.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="31b06-138">릴리스 템플릿의 구성 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="31b06-139">`ApiKey`에 대한 변수 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="31b06-140">ApiKey 변수 정의에 API 키를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![Team Services 창에서 구성 탭을 선택하고 변수 추가를 클릭합니다.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="31b06-143">마지막으로 릴리스 정의를 **저장** 합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="31b06-144">주석 보기</span><span class="sxs-lookup"><span data-stu-id="31b06-144">View annotations</span></span>
<span data-ttu-id="31b06-145">이제 릴리스 템플릿을 사용하여 새 릴리스를 배포할 때마다 주석이 Application Insights로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="31b06-146">주석은 메트릭 탐색기의 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="31b06-147">주석 마커를 클릭하면 요청자, 소스 제어 분기, 릴리스 정의, 환경 등 릴리스에 대한 세부 정보가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![릴리스 주석 마커를 클릭합니다.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="31b06-149">PowerShell에서 사용자 지정 주석 만들기</span><span class="sxs-lookup"><span data-stu-id="31b06-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="31b06-150">VS Team 시스템을 사용하지 않고 원하는 모든 프로세스에서 주석을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="31b06-151">[GitHub에서 Powershell 스크립트](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)의 로컬 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="31b06-152">응용 프로그램 ID를 가져오고 API 액세스 블레이드에서 API 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="31b06-153">다음과 같은 스크립트를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="31b06-154">과거에 대한 주석을 만드는 등 이 스크립트를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31b06-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31b06-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31b06-155">Next steps</span></span>

* [<span data-ttu-id="31b06-156">작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="31b06-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="31b06-157">PowerShell을 사용한 자동화</span><span class="sxs-lookup"><span data-stu-id="31b06-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
