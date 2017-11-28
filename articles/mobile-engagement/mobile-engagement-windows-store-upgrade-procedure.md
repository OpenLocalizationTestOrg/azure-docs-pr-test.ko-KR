---
title: "Windows 유니버설 앱 SDK 업그레이드 절차"
description: "Azure Mobile Engagement용 Windows 유니버설 앱 SDK 업그레이드 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="ee4e0-103">Windows 유니버설 앱 SDK 업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="ee4e0-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="ee4e0-104">이전 버전의 Engagement를 응용 프로그램에 이미 통합한 경우에는 SDK를 업그레이드할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="ee4e0-105">여러 SDK 버전을 건너뛴 경우에는 여러 절차를 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="ee4e0-106">예를 들어 0.10.1에서 0.11.0으로 마이그레이션하는 경우에는 먼저 "0.9.0에서 0.10.1로 마이그레이션" 절차를 수행한 후에 "0.10.1에서 0.11.0으로 마이그레이션" 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="ee4e0-107">3.3.0에서 3.4.0으로</span><span class="sxs-lookup"><span data-stu-id="ee4e0-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="ee4e0-108">테스트 로그</span><span class="sxs-lookup"><span data-stu-id="ee4e0-108">Test logs</span></span>
<span data-ttu-id="ee4e0-109">이제 SDK에서 생성된 콘솔 로그를 사용/사용 안 함/필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="ee4e0-110">이를 사용자 지정하려면 속성 `EngagementAgent.Instance.TestLogEnabled`를 `EngagementTestLogLevel` 열거형에서 사용 가능한 값 중 하나로 업데이트합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="ee4e0-111">리소스</span><span class="sxs-lookup"><span data-stu-id="ee4e0-111">Resources</span></span>
<span data-ttu-id="ee4e0-112">도달률 오버레이가 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="ee4e0-113">SDK NuGet 패키지 리소스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="ee4e0-114">새 버전의 SDK로 업그레이드하는 동안 리소스의 오버레이 폴더에서 기존 파일을 보관할 것인지 보관하지 않을 것인지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="ee4e0-115">이전 오버레이가 작동 중이거나 `WebView` 요소를 수동으로 통합하는 경우 기존 파일을 보관하도록 결정하여 계속 작동하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="ee4e0-116">새 오버레이로 업데이트하려는 경우 리소스의 전체 `overlay` 폴더를 SDK 패키지의 새 폴더로 바꿉니다(UWP 앱: 업그레이드 후 새 오버레이 폴더를 %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources에서 가져올 수 있음).</span><span class="sxs-lookup"><span data-stu-id="ee4e0-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="ee4e0-117">새 오버레이를 사용하면 이전 버전에서 설정한 모든 사용자 지정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="ee4e0-118">3.2.0에서 3.3.0으로</span><span class="sxs-lookup"><span data-stu-id="ee4e0-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="ee4e0-119">리소스</span><span class="sxs-lookup"><span data-stu-id="ee4e0-119">Resources</span></span>
<span data-ttu-id="ee4e0-120">이 단계는 사용자 지정된 리소스에만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-120">This step concerns customized resources only.</span></span> <span data-ttu-id="ee4e0-121">SDK(html, 이미지, 오버레이)에서 제공되는 리소스를 사용자 지정한 경우 업그레이드된 리소스에서 사용자 지정한 내용을 업그레이드 및 다시 적용하기 전에 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="ee4e0-122">3.1.0에서 3.2.0으로</span><span class="sxs-lookup"><span data-stu-id="ee4e0-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="ee4e0-123">리소스</span><span class="sxs-lookup"><span data-stu-id="ee4e0-123">Resources</span></span>
<span data-ttu-id="ee4e0-124">이 단계는 사용자 지정된 리소스에만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-124">This step concerns customized resources only.</span></span> <span data-ttu-id="ee4e0-125">SDK(html, 이미지, 오버레이)에서 제공되는 리소스를 사용자 지정한 경우 업그레이드된 리소스에서 사용자 지정한 내용을 업그레이드 및 다시 적용하기 전에 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="ee4e0-126">웹 보기 통합을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-126">Webview integration</span></span>
<span data-ttu-id="ee4e0-127">다른 장치 형식 요인과 일치하는 일부 개선 사항이 이 버전에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="ee4e0-128">Webview 통합이 다음과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="ee4e0-129">XAML 페이지 ()에서:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="ee4e0-130">그리고 연결된 .cs파일에서:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="ee4e0-131">2.0.0에서 3.0.0으로</span><span class="sxs-lookup"><span data-stu-id="ee4e0-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="ee4e0-132">리소스</span><span class="sxs-lookup"><span data-stu-id="ee4e0-132">Resources</span></span>
<span data-ttu-id="ee4e0-133">이 단계는 사용자 지정된 리소스에만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-133">This step concerns customized resources only.</span></span> <span data-ttu-id="ee4e0-134">SDK(html, 이미지, 오버레이)에서 제공되는 리소스를 사용자 지정한 경우 업그레이드된 리소스에서 사용자 지정한 내용을 업그레이드 및 다시 적용하기 전에 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="ee4e0-135">1.1.1에서 2.0.0으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="ee4e0-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="ee4e0-136">아래에서는 SDK 통합을 Capptain SAS 제공 Capptain 서비스에서 Azure Mobile Engagement 구동 앱으로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ee4e0-137">Capptain과 Mobile Engagement는 같은 서비스가 아니며, 아래에서 제공하는 절차에서는 클라이언트 앱을 마이그레이션하는 방법만 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="ee4e0-138">앱에서 SDK를 마이그레이션해도 데이터가 Capptain 서버에서 Mobile Engagement 서버로 마이그레이션되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="ee4e0-139">이전 버전에서 마이그레이션하는 경우에는 Capptain 웹 사이트를 참조하여 1.1.1로 먼저 마이그레이션한 후에 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="ee4e0-140">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="ee4e0-140">Nuget package</span></span>
<span data-ttu-id="ee4e0-141">**Capptain.WindowsPhone**을 **MicrosoftAzure.MobileEngagement** Nuget 패키지로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="ee4e0-142">Mobile Engagement 적용</span><span class="sxs-lookup"><span data-stu-id="ee4e0-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="ee4e0-143">SDK에서는 `Engagement`(이)라는 용어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="ee4e0-144">이 변경 내용에 맞게 프로젝트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="ee4e0-145">현재 Capptain NuGet 패키지는 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="ee4e0-146">Capptain 리소스 폴더의 모든 변경 내용도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="ee4e0-147">해당 폴더의 파일을 보존하려면 복사본을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="ee4e0-148">그런 다음 새 Microsoft Azure Engagement NuGet 패키지를 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="ee4e0-149">해당 패키지는 [NuGet 웹 사이트]에서 직접 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="ee4e0-150">또는 여기서 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-150">or here index.</span></span> <span data-ttu-id="ee4e0-151">이 작업을 수행하면 Engagement에서 사용하는 모든 리소스 파일이 바뀌며 프로젝트 참조에 새 Engagement DLL이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="ee4e0-152">Capptain DLL 참조를 삭제하여 프로젝트 참조를 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="ee4e0-153">이렇게 하지 않으면 Capptain 버전이 충돌하여 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="ee4e0-154">Capptain 리소스를 사용자 지정한 경우 이전 파일 콘텐츠를 복사하여 새 Engagement 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="ee4e0-155">xaml 파일과 cs 파일을 모두 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="ee4e0-156">해당 단계를 완료한 후에는 이전 Capptain 참조만 새 Engagement 참조로 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="ee4e0-157">모든 Capptain 네임스페이스를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="ee4e0-158">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="ee4e0-159">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="ee4e0-160">"Capptain"을 포함하는 모든 Capptain 클래스는 이제 "Engagement"를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="ee4e0-161">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="ee4e0-162">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="ee4e0-163">xaml 파일에서는 Capptain 네임스페이스와 특성도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="ee4e0-164">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="ee4e0-165">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="ee4e0-166">오버레이 페이지 변경</span><span class="sxs-lookup"><span data-stu-id="ee4e0-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ee4e0-167">오버레이도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-167">Overlay also changes.</span></span> <span data-ttu-id="ee4e0-168">새 네임스페이스는 `Microsoft.Azure.Engagement.Overlay`입니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="ee4e0-169">xaml 및 cs 파일에서 모두 이 네임스페이스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="ee4e0-170">또한 `CapptainGrid` 이름은 `EngagementGrid`(으)로, `capptain_notification_content` 및 `capptain_announcement_content` 이름은 `engagement_notification_content` 및 `engagement_announcement_content`(으)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="ee4e0-171">오버레이의 경우 아래 코드는</span><span class="sxs-lookup"><span data-stu-id="ee4e0-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="ee4e0-172">아래와 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="ee4e0-173">Capptain 그림 및 HTML 파일과 같은 기타 리소스도 "Engagement"를 사용하도록 이름이 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="ee4e0-174">프로젝트 선언</span><span class="sxs-lookup"><span data-stu-id="ee4e0-174">Project declaration</span></span>
<span data-ttu-id="ee4e0-175">Package.appxmanifest에서 `File Type Associations` 이(가) 다음과 같이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="ee4e0-176">capptain\_reach\_content를 engagement\_reach\_content로</span><span class="sxs-lookup"><span data-stu-id="ee4e0-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="ee4e0-177">capptain\_log\_file을 engagement\_log\_file로</span><span class="sxs-lookup"><span data-stu-id="ee4e0-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="ee4e0-178">응용 프로그램 ID/SDK 키</span><span class="sxs-lookup"><span data-stu-id="ee4e0-178">Application ID / SDK Key</span></span>
<span data-ttu-id="ee4e0-179">Engagement에서는 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-179">Engagement uses a connection string.</span></span> <span data-ttu-id="ee4e0-180">따라서 Mobile Engagement에서는 응용 프로그램 ID와 SDK 키를 지정할 필요가 없으며 연결 문자열만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="ee4e0-181">EngagementConfiguration 파일에서 연결 문자열을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="ee4e0-182">Engagement 구성은 프로젝트의 `Resources\EngagementConfiguration.xml` 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="ee4e0-183">이 파일을 편집하여 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-183">Edit this file to specify:</span></span>

* <span data-ttu-id="ee4e0-184">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="ee4e0-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="ee4e0-185">이 문자열을 런타임에 지정하려는 경우에는 Engagement 에이전트 초기화 전에 다음 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="ee4e0-186">응용 프로그램의 연결 문자열은 Azure 클래식 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="ee4e0-187">항목 이름 변경</span><span class="sxs-lookup"><span data-stu-id="ee4e0-187">Items name change</span></span>
<span data-ttu-id="ee4e0-188">*capptain*이라는 모든 항목은 *engagement*라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="ee4e0-189">마찬가지로 *Capptain*은 *Engagement*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="ee4e0-190">일반적으로 사용되는 Capptain 항목의 예제:</span><span class="sxs-lookup"><span data-stu-id="ee4e0-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="ee4e0-191">CapptainConfiguration의 이름은 EngagementConfiguration으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="ee4e0-192">CapptainAgent의 이름은 EngagementAgent로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="ee4e0-193">CapptainReach의 이름은 EngagementReach로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="ee4e0-194">CapptainHttpConfig의 이름은 EngagementHttpConfig로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="ee4e0-195">GetCapptainPageName의 이름은 GetEngagementPageName으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="ee4e0-196">이와 같이 바뀐 이름은 재정의되는 메서드에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee4e0-196">Note that rename also affects overridden methods.</span></span>

