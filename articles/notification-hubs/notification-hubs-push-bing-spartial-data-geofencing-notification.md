---
title: "Azure 알림 허브와 Bing 공간 데이터를 사용 하 여 aaaGeo 막힌 푸시 알림을 | Microsoft Docs"
description: "이 자습서에서는 toodeliver 위치 기반 Azure 알림 허브와 Bing 공간 데이터를 사용 하 여 알림을 푸시 하는 방법을 배웁니다."
services: notification-hubs
documentationcenter: windows
keywords: "푸시 알림, 푸시 알림"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="b28da-104">Azure 알림 허브 및 Bing 공간 데이터가 있는 지역 구분 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="b28da-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="b28da-105">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b28da-106">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b28da-107">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b28da-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="b28da-108">이 자습서에서는 위치 기반 toodeliver 푸시 알림 Azure 알림 허브와 Bing 공간 데이터를 활용 하는 유니버설 Windows 플랫폼 응용 프로그램 내에서 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b28da-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b28da-109">Prerequisites</span></span>
<span data-ttu-id="b28da-110">무엇 보다도, toomake 모든 hello 소프트웨어 및 서비스 필수 조건 한지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="b28da-111">[Visual Studio 2015 업데이트 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) 이상([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)도 가능).</span><span class="sxs-lookup"><span data-stu-id="b28da-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="b28da-112">최신 버전의 hello [Azure SDK](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="b28da-113">[Bing 맵 개발자 센터 계정](https://www.bingmapsportal.com/) (무료로 만들거나 Microsoft 계정으로 연결할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b28da-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="b28da-114">시작하기</span><span class="sxs-lookup"><span data-stu-id="b28da-114">Getting Started</span></span>
<span data-ttu-id="b28da-115">Hello 프로젝트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="b28da-116">Visual Studio에서 **비어 있는 앱(유니버설 Windows)**형식의 새 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="b28da-117">Hello 프로젝트 만들기 완료 되 면 hello 앱 자체에 대 한 hello 도구가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="b28da-118">이제 hello 지 오 펜싱 인프라에 대 한 모든 항목을 설정 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="b28da-119">우리는 Bing 서비스이 고 toouse 이므로 tooquery 특정 위치 프레임 수 있는 공용 REST API 끝점:</span><span class="sxs-lookup"><span data-stu-id="b28da-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="b28da-120">Toospecify 해야 작동 매개 변수 tooget 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="b28da-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="b28da-121">**데이터 원본 ID** 및 **데이터 원본 이름** – Bing 맵 API에서 데이터 원본은 작업하는 위치 및 업무 시간 등 다양하게 버킷 구성된 메타데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="b28da-122">이에 대한 자세한 내용은 여기에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-122">You can read more about those here.</span></span> 
* <span data-ttu-id="b28da-123">**엔터티 이름** – hello 알림에 대 한 참조 지점으로 toouse을 만들려는 엔터티 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="b28da-124">**Bing Maps API 키** – hello Bing Dev Center 계정을 만들 때 이전에 얻은 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="b28da-125">위의 hello 요소 각각에 대 한 hello 설정 심층적 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="b28da-126">Hello 데이터 소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-126">Setting up hello data source</span></span>
<span data-ttu-id="b28da-127">Hello Bing Maps 개발자 센터에서에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="b28da-128">클릭 하세요 **데이터 원본** hello 위쪽 탐색 모음 및 선택에서 **데이터 원본 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="b28da-129">Bing Maps API 하기 전에 작업 하지 않았던 가능성이 있습니다 수 없습니다, 모든 데이터 원본 업로드 데이터 tooa 데이터 원본을 클릭 하 여 한 새만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="b28da-130">모든 필수 hello 필드를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="b28da-131">궁금할 것 – hello 데이터 파일을 란 무엇이 고 어떻게 해야 있습니다 수 업로드?</span><span class="sxs-lookup"><span data-stu-id="b28da-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="b28da-132">Hello이이 테스트를 위해 hello 샌프란시스코 waterfront 부문의 프레임 파이프 기반 hello 샘플 수만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="b28da-133">위의 hello이이 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="b28da-134">단순히 복사 위 hello 문자열 새 파일에 붙여 넣고로 저장 **NotificationHubsGeofence.pipe**, hello Bing 개발자 센터에에서 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="b28da-135">Hello에 대 한 새 키 증명된 toospecify 수도 **마스터 키** hello와에서 다른 **쿼리 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="b28da-136">Hello 대시보드 및 새로 고침 hello 데이터 원본 업로드 페이지를 통해 새 키를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="b28da-137">Hello 데이터 파일을 업로드 되 면 toomake hello 데이터 원본을 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="b28da-138">너무 이동**데이터 원본 관리**위에 했던 것과 마찬가지로, hello 목록에서 데이터 원본의 찾을 클릭할 **게시** hello에 **동작** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="b28da-139">에 약간 표시 되어야 hello에 데이터 원본 **게시 된 데이터 원본** 탭:</span><span class="sxs-lookup"><span data-stu-id="b28da-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="b28da-140">클릭 하면 **편집**, 있습니다에 도입 되었습니다 어떤 위치를 한 눈에 수 toosee 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="b28da-141">이 시점에서 hello 포털 경계를 만든 hello geofence hello – 필요한 것은 지정 된 hello 위치 hello 오른쪽 주변에 있는 확인 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="b28da-142">이제 hello 데이터 원본에 대 한 모든 hello 요구 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="b28da-143">hello Bing Maps 개발자 센터에서에서 hello API 호출에 대 한 hello 요청 URL에 tooget hello 세부 정보 클릭 **데이터 원본** 선택 **데이터 원본 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="b28da-144">hello **쿼리 URL** 여기 뒤 우리가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="b28da-145">기준이 실행 수 인지 hello 장치 현재 위치의 hello 경계 내에서 쿼리 toocheck hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="b28da-146">이 확인, 추가 매개 변수 뒤 hello로 hello 쿼리 URL에 대해 GET 호출 tooexecute 필요 tooperform:</span><span class="sxs-lookup"><span data-stu-id="b28da-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="b28da-147">이런 방식으로 hello 장치에서 구한 및 hello geofence 내 인지 Bing Maps hello 계산 toosee를 자동으로 수행 됩니다 있는 대상 지점 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="b28da-148">브라우저 (또는 cURL)를 통해 hello 요청을 실행 하면 일단 받아볼 수 표준 JSON 응답:</span><span class="sxs-lookup"><span data-stu-id="b28da-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="b28da-149">이 응답 hello 실제로 안에 점이 hello 경계를 지정 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="b28da-150">그렇지 않은 경우 빈 **결과** 버킷을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="b28da-151">Hello UWP 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="b28da-151">Setting up hello UWP application</span></span>
<span data-ttu-id="b28da-152">이제 hello 데이터 소스를 준비 했으므로 hello UWP 응용 프로그램에서는 이전 부트스트랩 하는 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="b28da-153">무엇보다도, 응용 프로그램에 위치 서비스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="b28da-154">toodo이, 두 번이 클릭 `Package.appxmanifest` 파일 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="b28da-155">방금 연 hello 패키지 속성 탭에서 클릭 **기능** 선택 했는지 확인 하 고 **위치**:</span><span class="sxs-lookup"><span data-stu-id="b28da-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="b28da-156">Hello 위치 기능이 선언 되는 대로 라는 솔루션에 새 폴더를 만들고 `Core`, 라는 내에서 새 파일을 추가 하 고 `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="b28da-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="b28da-157">hello `LocationHelper` 클래스 자체는 시점에서 매우 기본적인 – hello 시스템 API 통해 tooobtain hello 사용자 위치 수는 것이 전부:</span><span class="sxs-lookup"><span data-stu-id="b28da-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="b28da-158">Hello 공식의 UWP 앱에서 사용자의 위치를 hello 가져오는 방법에 대해 자세히 알아볼 수 있습니다 [MSDN 문서](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="b28da-159">toocheck 실제로 hello 위치 취득이 작동 하는 기본 페이지의 hello 코드 쪽 엽니다 (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="b28da-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="b28da-160">Hello에 대 한 새 이벤트 처리기를 만들고 `Loaded` hello에 대 한 이벤트 `MainPage` 생성자:</span><span class="sxs-lookup"><span data-stu-id="b28da-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="b28da-161">hello 구현의 hello 이벤트 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="b28da-162">म hello 처리기도 선언할 비동기 때문에 `GetCurrentLocation` awaitable, 이며 따라서 toobe 비동기 컨텍스트에서 실행이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="b28da-163">또한 특정 상황에서는 생길 수 null 위치 때문에 (예: hello 위치 서비스를 해제 또는 hello 응용 프로그램 사용 권한 tooaccess 위치 거부 되었습니다) toomake null 확인을 통해 제대로 처리는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="b28da-164">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-164">Run hello application.</span></span> <span data-ttu-id="b28da-165">위치 액세스를 허용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="b28da-166">한 번 실행 하는 경우 응용 프로그램을 hello, hello hello 좌표 수 toosee 있어야 **출력** 창:</span><span class="sxs-lookup"><span data-stu-id="b28da-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="b28da-167">이제 우리 않습니다에서 사용 중 이므로 더 이상 위치 취득 works –의 로드에 대 한 무료 tooremove hello 테스트 이벤트 처리기 느껴집니다 있는지 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="b28da-168">hello 다음 단계는 toocapture 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="b28da-169">이 위해 뒤로 toohello 돌아가겠습니다 `LocationHelper` 클래스에 대 한 hello 이벤트 처리기를 추가 및 `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="b28da-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="b28da-170">hello 구현은 hello에 hello 위치 좌표를 표시 하는 **출력** 창:</span><span class="sxs-lookup"><span data-stu-id="b28da-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="b28da-171">Hello 백 엔드 설정</span><span class="sxs-lookup"><span data-stu-id="b28da-171">Setting up hello backend</span></span>
<span data-ttu-id="b28da-172">Hello 다운로드 [GitHub에서.NET 백 엔드 샘플](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="b28da-173">Hello 다운로드가 완료 되 면 hello 열어 `NotifyUsers` 폴더를 연 이후에 – hello `NotifyUsers.sln` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="b28da-174">집합 hello `AppBackend` hello로 프로젝트 **시작 프로젝트** 시작 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b28da-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="b28da-175">hello 프로젝트는 이미 구성 된 toosend 푸시 알림을 tootarget 장치, toodo만 다음 두 가지 – 되므로 hello 알림 허브에 대 한 올바른 연결 문자열 hello 교체 하 고 경우에 hello 경계 식별 toosend hello 알림 추가 사용자는 hello geofence 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="b28da-176">tooconfigure hello 연결 문자열 hello `Models` 폴더 열림 `Notifications.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="b28da-177">hello `NotificationHubClient.CreateClientFromConnectionString` 함수 hello에서 얻을 수 있는 알림 허브에 대 한 hello 정보를 포함 해야 [Azure 포털](https://portal.azure.com) (hello를 자세히 살펴보고 **액세스 정책을** 블레이드  **설정**).</span><span class="sxs-lookup"><span data-stu-id="b28da-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="b28da-178">Hello 업데이트 된 구성 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="b28da-179">이제 모델 toocreate hello Bing Maps API 결과 대 한 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="b28da-180">hello 마우스 오른쪽 단추로 클릭 하는 가장 쉬운 방법은 toodo hello `Models` 폴더 **추가** > **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="b28da-181">이름을 `GeofenceBoundary.cs`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="b28da-182">Visual Studio 사용 및 hello 첫 번째 섹션에서 설명한 hello API 응답에서 완료 되 면 복사 hello JSON **편집** > **붙여넣기** > **붙여넣기 JSON 클래스로**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="b28da-183">해당 hello 개체 인지를 확인 하는 이런 방식으로 deserialize 되는 원래 대로 정확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="b28da-184">결과 클래스 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="b28da-185">다음으로 `Controllers` > `NotificationsController.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="b28da-186">Hello 대상 경도 및 위도 tootweak hello Post 호출 tooaccount이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="b28da-187">이 위해 두 개의 문자열 toohello 함수 시그니처 –를 추가 하면 `latitude` 및 `longitude`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="b28da-188">라는 hello 프로젝트 내에서 새 클래스 만들기 `ApiHelper.cs` – 때 tooconnect tooBing toocheck 지점 경계 교차점 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="b28da-189">다음과 같이 `IsPointWithinBounds` 함수를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="b28da-190">이전 hello Bing 개발자 센터 (마찬가지 toohello API 키)에서 가져온 hello 쿼리 URL 있는 있는지 toosubstitute hello API 끝점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="b28da-191">결과 toohello 쿼리가 있는 경우 지정 된 지점 hello 즉 이므로 hello geofence의 hello 경계 내에서 반환 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="b28da-192">결과가 없습니다 Bing 알려줍니다 hello 포인트는 외부 hello 조회 프레임을 반환 하므로 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="b28da-193">다시 `NotificationsController.cs`, hello switch 문의 하기 바로 전에 검사를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="b28da-194">이런 방식으로 hello 지점 hello 경계 내에 있을 때 hello 알림이 전송만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="b28da-195">Hello UWP 앱에 푸시 알림을 테스트</span><span class="sxs-lookup"><span data-stu-id="b28da-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="b28da-196">UWP 앱 toohello를 다시 살펴보자면, 우리 있어야 수 tootest 알림.</span><span class="sxs-lookup"><span data-stu-id="b28da-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="b28da-197">Hello 내 `LocationHelper` 클래스, – 새 함수를 만들고 `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="b28da-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="b28da-198">Hello 교체 `POST_URL` hello 이전 섹션에서 만든 배포 된 웹 응용 프로그램의 toohello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="b28da-199">일단, 확인 toorun은 로컬로 하지만 toohost 해야는 공용 버전 배포를 사용할 때는 외부 공급자와 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="b28da-200">이제 되어 있는지 확인 푸시 알림에 대 한 hello UWP 앱을 등록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="b28da-201">Visual Studio에서 클릭 **프로젝트** > **저장** > **hello 스토어와 앱 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="b28da-202">Tooyour 개발자 계정에 로그인 한 후에 기존 앱을 선택 하거나 새로 만들 및 hello 패키지 연관 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="b28da-203">Toohello 개발자 센터와 방금 만든 열기 hello 앱 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="b28da-204">**서비스** > **푸시 알림** > **라이브 서비스 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="b28da-205">Hello 사이트에서 기록해 hello **응용 프로그램 암호** 및 hello **패키지 SID**합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="b28da-206">모두 Azure 포털 – hello에서 알림 허브를 열고에서 클릭 해야 **설정** > **Notification Services** > **WNS (Windows)**hello 필수 필드에 hello 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="b28da-207">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-207">Click on **Save**.</span></span>

<span data-ttu-id="b28da-208">**솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="b28da-209">Tooadd 참조 toohello 필요한 **Microsoft Azure 서비스 버스 관리 되는 라이브러리** – 검색할 `WindowsAzure.Messaging.Managed` tooyour 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="b28da-210">테스트를 위해 hello 만들면 `MainPage_Loaded` 이벤트 처리기를 다시 한 번이 코드 조각 tooit 추가:</span><span class="sxs-lookup"><span data-stu-id="b28da-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="b28da-211">위의 hello hello 앱 hello 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="b28da-212">준비 toogo는!</span><span class="sxs-lookup"><span data-stu-id="b28da-212">You are ready toogo!</span></span> 

<span data-ttu-id="b28da-213">`LocationHelper`, hello 내 `Geolocator_PositionChanged` 처리기를 강제로 hello geofence 안의 hello 위치 시킨 테스트 코드 부분을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="b28da-214">Hello 실제 좌표 (않을 수도 있는 hello 경계 내 hello 순간)에 전달 하는 하 고 미리 정의 된 테스트 값을 사용 하는,에서는 업데이트에 표시 되는 알림을 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="b28da-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b28da-215">What’s next?</span></span>
<span data-ttu-id="b28da-216">Toofollow hello 솔루션이 프로덕션에 사용 가능한 인지 toomake 위에 추가 toohello에서 할 수 있는 단계는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="b28da-217">무엇 보다도, geofences는 동적 tooensure를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="b28da-218">여기에 주문 toobe 수 tooupload hello 기존 데이터 원본 내에서 새 경계에 hello Bing API가 있는 몇 가지 추가 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="b28da-219">Hello 참조 [Bing 공간 데이터 서비스 API 설명서](https://msdn.microsoft.com/library/ff701734.aspx) hello 주제에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="b28da-220">둘째, 작업 tooensure hello 배달 toohello 오른쪽 참가자 했는지 인 경우 tootarget 필요할 수 있습니다를 통해 이러한 [태그 지정](notification-hubs-tags-segment-push-message.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="b28da-221">위에 표시 된 hello 솔루션은 있을 수도 있으므로 hello 지 오 펜싱 toosystem 관련 기능을 제한 하지 않은 다양 한 플랫폼을 대상으로 하는 시나리오를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="b28da-222">즉, 유니버설 Windows 플랫폼 hello 너무 기능을 제공[geofences 오른쪽-의-즉시 검색](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="b28da-223">알림 허브 기능에 대한 자세한 내용은 [설명서 포털](https://azure.microsoft.com/documentation/services/notification-hubs/)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b28da-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

