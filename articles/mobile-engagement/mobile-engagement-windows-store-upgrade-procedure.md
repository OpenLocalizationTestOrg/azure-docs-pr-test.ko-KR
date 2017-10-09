---
title: "aaaWindows 유니버설 앱 SDK 업그레이드 절차"
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
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="0ece7-103">Windows 유니버설 앱 SDK 업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="0ece7-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="0ece7-104">통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="0ece7-105">여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="0ece7-106">예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="0ece7-107">3.3.0에서 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="0ece7-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="0ece7-108">테스트 로그</span><span class="sxs-lookup"><span data-stu-id="0ece7-108">Test logs</span></span>
<span data-ttu-id="0ece7-109">Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="0ece7-110">toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="0ece7-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="0ece7-111">리소스</span><span class="sxs-lookup"><span data-stu-id="0ece7-111">Resources</span></span>
<span data-ttu-id="0ece7-112">hello Reach 오버레이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="0ece7-113">Hello SDK NuGet 패키지 리소스의 일부인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="0ece7-114">Toohello hello SDK의 새 버전을 업그레이드 하는 동안 여부 hello에서 기존 파일의 리소스 폴더를 오버레이 tookeep 할지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="0ece7-115">Hello 이전 오버레이를 작동 하거나 hello를 통합 하는 경우 `WebView` 요소 수동으로 tookeep 기존 파일을 결정할 수, 한 다음 계속 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="0ece7-116">Tooupdate toohello 새 오버레이 정당한 바꾸기 hello 전체 경우 `overlay` hello SDK 패키지에서 새 hello로 리소스에서 폴더 (UWP 앱: hello 업그레이드 후 hello 새 오버레이 폴더 % USERPROFILE %에서 얻을 수 있습니다\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="0ece7-117">Hello 새 오버레이 사용 하 여 hello 이전 버전에서 적용 된 모든 사용자 지정을 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="0ece7-118">3.2.0에서 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="0ece7-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="0ece7-119">리소스</span><span class="sxs-lookup"><span data-stu-id="0ece7-119">Resources</span></span>
<span data-ttu-id="0ece7-120">이 단계는 사용자 지정된 리소스에만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-120">This step concerns customized resources only.</span></span> <span data-ttu-id="0ece7-121">Toobackup 있는 hello (html, 이미지, 오버레이) SDK에서 제공 하는 hello 리소스를 사용자 지정한 경우 업그레이드 하 고 다시 적용 하기 전에에 사용자 지정 업그레이드 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="0ece7-122">3.1.0에서 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="0ece7-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="0ece7-123">리소스</span><span class="sxs-lookup"><span data-stu-id="0ece7-123">Resources</span></span>
<span data-ttu-id="0ece7-124">이 단계는 사용자 지정된 리소스에만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-124">This step concerns customized resources only.</span></span> <span data-ttu-id="0ece7-125">Toobackup 있는 hello (html, 이미지, 오버레이) SDK에서 제공 하는 hello 리소스를 사용자 지정한 경우 업그레이드 하 고 다시 적용 하기 전에에 사용자 지정 업그레이드 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="0ece7-126">웹 보기 통합을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0ece7-126">Webview integration</span></span>
<span data-ttu-id="0ece7-127">몇 가지 향상 된 기능 toomatch 다른 장치 폼 팩터가이 버전에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="0ece7-128">Hello webview의 통합 hello 다음 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="0ece7-129">XAML 페이지 ()에서:</span><span class="sxs-lookup"><span data-stu-id="0ece7-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="0ece7-130">그리고 연결된 .cs파일에서:</span><span class="sxs-lookup"><span data-stu-id="0ece7-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
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
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="0ece7-131">2.0.0에서 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="0ece7-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="0ece7-132">리소스</span><span class="sxs-lookup"><span data-stu-id="0ece7-132">Resources</span></span>
<span data-ttu-id="0ece7-133">이 단계는 사용자 지정된 리소스에만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-133">This step concerns customized resources only.</span></span> <span data-ttu-id="0ece7-134">Toobackup 있는 hello (html, 이미지, 오버레이) SDK에서 제공 하는 hello 리소스를 사용자 지정한 경우 업그레이드 하 고 다시 적용 하기 전에에 사용자 지정 업그레이드 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="0ece7-135">1.1.1에서 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ece7-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="0ece7-136">hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0ece7-137">Capptain 및 Mobile Engagement는 동일한 서비스 하지 hello 및 아래에 주어진 hello 프로시저 어떻게 toomigrate hello 클라이언트 응용 프로그램을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="0ece7-138">Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="0ece7-139">이전 버전에서 마이그레이션하려는 경우 하십시오 hello Capptain 웹 사이트 toomigrate too1.1.1를 먼저 참조 다음 절차를 수행 하는 hello를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="0ece7-140">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="0ece7-140">Nuget package</span></span>
<span data-ttu-id="0ece7-141">**Capptain.WindowsPhone**을 **MicrosoftAzure.MobileEngagement** Nuget 패키지로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="0ece7-142">Mobile Engagement 적용</span><span class="sxs-lookup"><span data-stu-id="0ece7-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="0ece7-143">hello SDK hello 단어를 사용 하 여 `Engagement`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="0ece7-144">Tooupdate 프로젝트 toomatch 해야이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="0ece7-145">Toouninstall 현재 Capptain nuget 패키지를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="0ece7-146">Capptain 리소스 폴더의 모든 변경 내용도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="0ece7-147">Tookeep 하려는 경우 해당 파일의 복사본을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="0ece7-148">그 후 hello 새 Microsoft Azure Engagement nuget 패키지를 프로젝트에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="0ece7-149">해당 패키지는 [NuGet 웹 사이트]에서 직접 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="0ece7-150">또는 여기서 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-150">or here index.</span></span> <span data-ttu-id="0ece7-151">프로젝트 참조를 Engagement에서 사용 되는 및 hello 새 Engagement DLL tooyour 추가 하는 모든 리소스 파일에이 작업으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="0ece7-152">해야 tooclean 프로젝트 참조 Capptain DLL 참조를 삭제 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="0ece7-153">이 적용 하지 않을 경우 hello 버전 Capptain의 충돌 하는 및 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="0ece7-154">Capptain 리소스를 사용자 지정한 경우 이전 파일 내용을 복사한 hello 새 Engagement 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="0ece7-155">Xaml 및 cs 파일을 모두 업데이트 toobe 한지 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0ece7-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="0ece7-156">이러한 단계가 완료 되 면 hello 새 Engagement 참조에 의해 tooreplace 이전 Capptain 참조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="0ece7-157">모든 Capptain 네임 스페이스 업데이트 toobe가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="0ece7-158">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="0ece7-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="0ece7-159">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="0ece7-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="0ece7-160">"Capptain"을 포함하는 모든 Capptain 클래스는 이제 "Engagement"를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="0ece7-161">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="0ece7-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="0ece7-162">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="0ece7-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="0ece7-163">xaml 파일에서는 Capptain 네임스페이스와 특성도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="0ece7-164">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="0ece7-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="0ece7-165">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="0ece7-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="0ece7-166">오버레이 페이지 변경</span><span class="sxs-lookup"><span data-stu-id="0ece7-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0ece7-167">오버레이도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-167">Overlay also changes.</span></span> <span data-ttu-id="0ece7-168">새 네임스페이스는 `Microsoft.Azure.Engagement.Overlay`입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="0ece7-169">Cs와 xaml 파일에서 사용 되는 toobe를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="0ece7-170">또한 `CapptainGrid` toobe 라는 `EngagementGrid`, `capptain_notification_content` 및 `capptain_announcement_content` 이름은 `engagement_notification_content` 및 `engagement_announcement_content`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="0ece7-171">오버레이의 경우 아래 코드는</span><span class="sxs-lookup"><span data-stu-id="0ece7-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="0ece7-172">아래와 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="0ece7-173">Hello에 대 한 Capptain 사진 및 HTML 파일 등의 다른 리소스 참고는 또한 있다가 이름이 바뀐된 toouse "계약"입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="0ece7-174">프로젝트 선언</span><span class="sxs-lookup"><span data-stu-id="0ece7-174">Project declaration</span></span>
<span data-ttu-id="0ece7-175">Package.appxmanifest에서 `File Type Associations` 이(가) 다음과 같이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="0ece7-176">capptain\_도달\_콘텐츠 tooengagement\_도달\_콘텐츠</span><span class="sxs-lookup"><span data-stu-id="0ece7-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="0ece7-177">capptain\_로그\_tooengagement 파일\_로그\_파일</span><span class="sxs-lookup"><span data-stu-id="0ece7-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="0ece7-178">응용 프로그램 ID/SDK 키</span><span class="sxs-lookup"><span data-stu-id="0ece7-178">Application ID / SDK Key</span></span>
<span data-ttu-id="0ece7-179">Engagement에서는 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-179">Engagement uses a connection string.</span></span> <span data-ttu-id="0ece7-180">응용 프로그램 ID 및 Mobile Engagement와 SDK 키 toospecify 없는, 하기만 하면 toospecify 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="0ece7-181">EngagementConfiguration 파일에서 연결 문자열을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="0ece7-182">hello Engagement 구성에서 설정할 수 있습니다 프로그램 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="0ece7-183">이 파일 toospecify를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="0ece7-184">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="0ece7-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="0ece7-185">런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:</span><span class="sxs-lookup"><span data-stu-id="0ece7-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="0ece7-186">응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="0ece7-187">항목 이름 변경</span><span class="sxs-lookup"><span data-stu-id="0ece7-187">Items name change</span></span>
<span data-ttu-id="0ece7-188">*capptain*이라는 모든 항목은 *engagement*라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="0ece7-189">마찬가지로 *Capptain* 너무*Engagement*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="0ece7-190">일반적으로 사용되는 Capptain 항목의 예제:</span><span class="sxs-lookup"><span data-stu-id="0ece7-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="0ece7-191">CapptainConfiguration의 이름은 EngagementConfiguration으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="0ece7-192">CapptainAgent의 이름은 EngagementAgent로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="0ece7-193">CapptainReach의 이름은 EngagementReach로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="0ece7-194">CapptainHttpConfig의 이름은 EngagementHttpConfig로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="0ece7-195">GetCapptainPageName의 이름은 GetEngagementPageName으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="0ece7-196">이와 같이 바뀐 이름은 재정의되는 메서드에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ece7-196">Note that rename also affects overridden methods.</span></span>

