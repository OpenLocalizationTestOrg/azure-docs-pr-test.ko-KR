---
title: "Azure 알림 허브 및 Bing 공간 데이터가 있는 지역 구분 푸시 알림 | Microsoft Docs"
description: "이 자습서에서는 Azure 알림 허브 및 Bing 공간 데이터로 위치 기반 푸시 알림을 전달하는 방법을 알아봅니다."
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
ms.openlocfilehash: b2a84e0479aac9ded08bb64e1ea20ddee6636cce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="c79c4-104">Azure 알림 허브 및 Bing 공간 데이터가 있는 지역 구분 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="c79c4-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="c79c4-105">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c79c4-106">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c79c4-107">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c79c4-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="c79c4-108">이 자습서에서는 유니버설 Windows 플랫폼 응용 프로그램 내에서 활용된 Azure 알림 허브 및 Bing 공간 데이터로 위치 기반 푸시 알림을 전달하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c79c4-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c79c4-109">Prerequisites</span></span>
<span data-ttu-id="c79c4-110">무엇보다도, 모든 소프트웨어 및 서비스 필수 구성 요소를 갖추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="c79c4-111">[Visual Studio 2015 업데이트 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) 이상([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)도 가능).</span><span class="sxs-lookup"><span data-stu-id="c79c4-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="c79c4-112">최신 버전의 [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c79c4-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="c79c4-113">[Bing 맵 개발자 센터 계정](https://www.bingmapsportal.com/) (무료로 만들거나 Microsoft 계정으로 연결할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="c79c4-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c79c4-114">시작하기</span><span class="sxs-lookup"><span data-stu-id="c79c4-114">Getting Started</span></span>
<span data-ttu-id="c79c4-115">프로젝트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-115">Let’s start by creating the project.</span></span> <span data-ttu-id="c79c4-116">Visual Studio에서 **비어 있는 앱(유니버설 Windows)**형식의 새 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="c79c4-117">프로젝트 생성이 완료되면 앱 자체에 대한 테스트 도구가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="c79c4-118">이제 지역 구분 인프라에 모든 항목을 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="c79c4-119">이에 대해 Bing 서비스를 사용하기 때문에 특정 위치 프레임을 쿼리할 수 있는 공용 REST API 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="c79c4-120">다음 매개 변수를 지정하여 작동시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="c79c4-121">**데이터 원본 ID** 및 **데이터 원본 이름** – Bing 맵 API에서 데이터 원본은 작업하는 위치 및 업무 시간 등 다양하게 버킷 구성된 메타데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="c79c4-122">이에 대한 자세한 내용은 여기에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-122">You can read more about those here.</span></span> 
* <span data-ttu-id="c79c4-123">**엔터티 이름** – 알림에 대한 참조 지점으로 사용하려는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c79c4-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="c79c4-124">**Bing 맵 API 키** – Bing 개발자 센터 계정을 만들 경우 이전에 얻은 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="c79c4-125">위의 요소 각각에 대한 설정에서 자세하게 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="c79c4-126">데이터 소스 설정</span><span class="sxs-lookup"><span data-stu-id="c79c4-126">Setting up the data source</span></span>
<span data-ttu-id="c79c4-127">Bing 맵 개발자 센터에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="c79c4-128">위쪽 탐색 모음에서 **데이터 원본**을 클릭하고 **데이터 원본 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="c79c4-129">이전에 Bing 맵 API로 작업하지 않은 경우 데이터 원본이 존재하지 않을 수 있으므로 데이터 원본에 데이터 업로드를 클릭하여 새 데이터 원본을 바로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="c79c4-130">모든 필수 필드를 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-130">Make sure you fill out all the required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="c79c4-131">데이터 파일의 정의 및 업로드해야 하는 항목이 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="c79c4-132">이 테스트를 완료하기 위해 San Francisco 해안 영역을 둘러싸는 파이프 기반 샘플을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="c79c4-133">위는 이 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-133">The above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="c79c4-134">위의 문자열을 새 파일에 복사하고 붙여 넣은 다음 **NotificationHubsGeofence.pipe**로 저장하고 Bing 개발자 센터에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c79c4-135">**쿼리 키**와 다른 **마스터 키**에 대한 새 키를 지정하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="c79c4-136">대시보드를 통해 새 키를 만들고 데이터 원본 업로드 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="c79c4-137">데이터 파일을 업로드하면 데이터 원본을 게시하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="c79c4-138">위에서처럼 **데이터 원본 관리**로 이동하여 목록에서 데이터 원본을 찾고 **작업** 열에서 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="c79c4-139">**게시된 데이터 원본** 탭에 데이터 원본이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="c79c4-140">**편집**을 클릭하면 설명한 위치를 한 눈에 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="c79c4-141">이 시점에서 포털은 만든 지역 구분에 대한 경계를 보여주지 않습니다. 지정된 위치가 오른쪽 주변에 있다는 것을 확인하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="c79c4-142">이제 데이터 원본에 대한 모든 요구 사항을 갖추었습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="c79c4-143">Bing 맵 개발자 센터에서 API 호출에 대한 요청 URL의 세부 정보를 얻으려면 **데이터 원본**을 클릭하고 **데이터 원본 정보**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="c79c4-144">**쿼리 URL** 은 여기서 살펴볼 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="c79c4-145">장치가 현재 위치의 경계 내에 있는지 여부를 확인하기 위해 쿼리를 실행할 수 있는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="c79c4-146">이 검사를 수행하려면 추가된 다음 매개 변수를 사용하여 쿼리 URL에 대한 가져오기 호출을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="c79c4-147">장치 및 Bing 맵에서 얻은 대상 지점을 지정하는 방식은 자동으로 계산을 수행하여 지역 구분 내에 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="c79c4-148">브라우저(또는 cURL)를 통해 요청을 실행하면 표준 JSON 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="c79c4-149">지점이 실제로 지정된 경계 내에 있는 경우에만 이 응답이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="c79c4-150">그렇지 않은 경우 빈 **결과** 버킷을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="c79c4-151">UWP 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="c79c4-151">Setting up the UWP application</span></span>
<span data-ttu-id="c79c4-152">이제 데이터 원본을 준비했으므로 이전에 부트스트랩된 UWP 응용 프로그램에서 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="c79c4-153">무엇보다도, 응용 프로그램에 위치 서비스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="c79c4-154">이 작업을 수행하려면 **솔루션 탐색기**에서 `Package.appxmanifest` 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="c79c4-155">방금 연 패키지 속성 탭에서 **기능**을 클릭하고 **위치**를 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="c79c4-156">위치 기능을 선언하는 대로 솔루션에 `Core`이라는 새 폴더를 만들고 `LocationHelper.cs`라는 새 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="c79c4-157">`LocationHelper` 클래스 자체는 이 시점에서 비교적 기본으로 시스템 API를 통해 사용자 위치를 찾을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

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

<span data-ttu-id="c79c4-158">공식 [MSDN 문서](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)의 UWP 앱에서 사용자의 위치를 가져오는 방법에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="c79c4-159">위치 취득이 실제로 작동하는지 확인하려면 기본 페이지(`MainPage.xaml.cs`)의 코드 쪽을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="c79c4-160">`MainPage` 생성자에서 `Loaded` 이벤트에 대한 새 이벤트 처리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="c79c4-161">이벤트 처리기의 구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="c79c4-162">`GetCurrentLocation` 이 대기할 수 있고 따라서 비동기 컨텍스트에서 실행되어야 하기 때문에 처리기를 비동기로 선언했습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="c79c4-163">또한 특정 상황에서 null 위치(예: 위치 서비스를 사용하지 않거나 응용 프로그램이 위치에 액세스하는 사용 권한을 거부함)일 수 있기 때문에 null 확인을 제대로 처리했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="c79c4-164">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-164">Run the application.</span></span> <span data-ttu-id="c79c4-165">위치 액세스를 허용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="c79c4-166">응용 프로그램이 시작되면 **출력** 창에서 좌표를 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="c79c4-167">이제 위치 취득이 작동합니다. 로드됨에 대한 테스트 이벤트 처리기를 더 이상 사용하지 않기 때문에 자유롭게 삭제하세요.</span><span class="sxs-lookup"><span data-stu-id="c79c4-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="c79c4-168">다음 단계는 변경된 위치를 파악하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-168">The next step is to capture location changes.</span></span> <span data-ttu-id="c79c4-169">이를 수행하기 위해 `LocationHelper` 클래스로 돌아가서 `PositionChanged`에 이벤트 처리기를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="c79c4-170">구현은 **출력** 창에서 위치 좌표를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="c79c4-171">백 엔드 설정</span><span class="sxs-lookup"><span data-stu-id="c79c4-171">Setting up the backend</span></span>
<span data-ttu-id="c79c4-172">[GitHub에서 .NET 백 엔드 샘플](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="c79c4-173">다운로드가 완료되면 `NotifyUsers` 폴더를 열고 이후 `NotifyUsers.sln` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="c79c4-174">`AppBackend` 프로젝트를 **시작 프로젝트** 로 설정하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="c79c4-175">프로젝트는 이미 대상 장치에 푸시 알림을 전송하도록 구성되었으므로 두 가지가 필요합니다. 알림 허브에 맞는 연결 문자열을 교체하고 사용자가 지역 구분 내에 있는 경우 알림을 보내도록 경계 식별을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="c79c4-176">연결 문자열을 구성하려면 `Models` 폴더에서 `Notifications.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="c79c4-177">`NotificationHubClient.CreateClientFromConnectionString` 함수는 [Azure Portal](https://portal.azure.com)에서 얻을 수 있는 알림 허브에 대한 정보를 포함해야 합니다(**설정**에서 **액세스 정책** 블레이드를 살펴봄).</span><span class="sxs-lookup"><span data-stu-id="c79c4-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="c79c4-178">업데이트된 구성 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-178">Save the updated configuration file.</span></span>

<span data-ttu-id="c79c4-179">이제 Bing 맵 API 결과에 대한 모델을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="c79c4-180">마우스 오른쪽 단추로 `Models` 폴더, **추가** > **클래스**를 클릭하는 것이 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="c79c4-181">이름을 `GeofenceBoundary.cs`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="c79c4-182">완료되면 첫 번째 섹션에서 설명한 API 응답에서 JSON을 복사하고 Visual Studio에서 **편집** > **붙여넣기** > **JSON을 클래스로 붙여넣기**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="c79c4-183">이렇게 의도한 대로 개체를 역직렬화하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="c79c4-184">결과 클래스 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="c79c4-185">다음으로 `Controllers` > `NotificationsController.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="c79c4-186">대상 경도 및 위도에 대한 계정에 게시 호출을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="c79c4-187">이를 위해 함수 시그니처 `latitude` 및 `longitude`라는 두 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="c79c4-188">`ApiHelper.cs` 이라는 프로젝트 내에서 새 클래스를 만들고 Bing에 연결하는 데 사용하여 지점 경계 교차점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="c79c4-189">다음과 같이 `IsPointWithinBounds` 함수를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="c79c4-190">API 끝점을 앞의 Bing 개발자 센터에서 얻은 쿼리 URL로 대체하도록 합니다(API 키에도 동일하게 적용).</span><span class="sxs-lookup"><span data-stu-id="c79c4-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="c79c4-191">쿼리에 대한 결과가 있는 경우, 즉, 지정된 지점이 지역 구분의 경계 내에 있으므로 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="c79c4-192">결과가 없는 경우 Bing은 지점이 조회 프레임 외부에 있다고 알리므로 `false`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="c79c4-193">다시 `NotificationsController.cs`에서 전환 문 앞을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

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

<span data-ttu-id="c79c4-194">이런 방식으로 지점이 경계 내에 있는 경우 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="c79c4-195">UWP 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="c79c4-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="c79c4-196">UWP 앱으로 다시 돌아가면 이제 알림을 테스트할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="c79c4-197">`LocationHelper` 클래스 내에서 새 함수 `SendLocationToBackend`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="c79c4-198">`POST_URL`을 이전 섹션에서 만든 배포된 웹 응용 프로그램의 위치로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="c79c4-199">이제 로컬에서 실행해도 되지만 공용 버전을 배포할 경우 외부 공급자로 호스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="c79c4-200">푸시 알림에 UWP 앱을 등록했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="c79c4-201">Visual Studio에서 **프로젝트** > **저장** > **스토어와 앱 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="c79c4-202">개발자 계정에 로그인하면 기존 앱을 선택하거나 새로 만들고 해당 앱과 패키지를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="c79c4-203">개발자 센터로 이동하고 방금 만든 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="c79c4-204">**서비스** > **푸시 알림** > **라이브 서비스 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="c79c4-205">사이트에서 **응용 프로그램 암호** 및 **패키지 SID**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="c79c4-206">Azure Portal에서 알림 허브를 열고 **설정** > **알림 서비스** > **WNS(Windows)**를 클릭하며 필수 필드에 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="c79c4-207">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-207">Click on **Save**.</span></span>

<span data-ttu-id="c79c4-208">**솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="c79c4-209">**Microsoft Azure 서비스 버스 관리된 라이브러리**에 참조를 추가해야 합니다. `WindowsAzure.Messaging.Managed`를 검색하고 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="c79c4-210">테스트하기 위해 `MainPage_Loaded` 이벤트 처리기를 다시 한 번 만들고 이 코드 조각을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="c79c4-211">위에서는 알림 허브로 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="c79c4-212">준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-212">You are ready to go!</span></span> 

<span data-ttu-id="c79c4-213">`LocationHelper`의 `Geolocator_PositionChanged` 처리기 내부에 강제로 지역 구분 내부의 위치를 배치하는 테스트 코드의 조각을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="c79c4-214">실제 좌표(현재 경계 내에 없을 수 있음)를 전달하지 않고 미리 정의된 테스트 값을 사용하기 때문에 업데이트에 표시된 알림을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="c79c4-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c79c4-215">What’s next?</span></span>
<span data-ttu-id="c79c4-216">위의 단계 이외에 솔루션이 프로덕션을 준비하도록 수행해야 하는 두 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="c79c4-217">무엇보다도, 지역 구분이 동적인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="c79c4-218">기존 데이터 원본 내에서 새 경계를 업로드할 수 있도록 Bing API와 함께 몇 가지 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="c79c4-219">주제에 대한 자세한 내용은 [Bing 공간 데이터 서비스 API 설명서](https://msdn.microsoft.com/library/ff701734.aspx) 를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="c79c4-220">둘째, 맞는 참가자에게 배달했는지 확인하기 위해 작업을 수행하는 경우 [태그 지정](notification-hubs-tags-segment-push-message.md)을 통해 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="c79c4-221">위에 표시된 솔루션은 다양한 대상 플랫폼이 있을 수 있는 시나리오를 설명하므로 시스템 관련 기능에 대해 지역 구분을 제한하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="c79c4-222">즉, 유니버설 Windows 플랫폼은 [지역 구분을 기본으로 검색](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence)하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="c79c4-223">알림 허브 기능에 대한 자세한 내용은 [설명서 포털](https://azure.microsoft.com/documentation/services/notification-hubs/)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c4-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

