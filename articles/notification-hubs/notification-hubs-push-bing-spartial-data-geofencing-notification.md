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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Azure 알림 허브 및 Bing 공간 데이터가 있는 지역 구분 푸시 알림
> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02)을 참조하세요.
> 
> 

이 자습서에서는 위치 기반 toodeliver 푸시 알림 Azure 알림 허브와 Bing 공간 데이터를 활용 하는 유니버설 Windows 플랫폼 응용 프로그램 내에서 하는 방법을 배웁니다.

## <a name="prerequisites"></a>필수 조건
무엇 보다도, toomake 모든 hello 소프트웨어 및 서비스 필수 조건 한지 확인 해야 합니다.

* [Visual Studio 2015 업데이트 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) 이상([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)도 가능). 
* 최신 버전의 hello [Azure SDK](https://azure.microsoft.com/downloads/)합니다. 
* [Bing 맵 개발자 센터 계정](https://www.bingmapsportal.com/) (무료로 만들거나 Microsoft 계정으로 연결할 수 있음). 

## <a name="getting-started"></a>시작하기
Hello 프로젝트를 만들어 보겠습니다. Visual Studio에서 **비어 있는 앱(유니버설 Windows)**형식의 새 프로젝트를 시작합니다.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Hello 프로젝트 만들기 완료 되 면 hello 앱 자체에 대 한 hello 도구가 있어야 합니다. 이제 hello 지 오 펜싱 인프라에 대 한 모든 항목을 설정 해 보겠습니다. 우리는 Bing 서비스이 고 toouse 이므로 tooquery 특정 위치 프레임 수 있는 공용 REST API 끝점:

    http://spatial.virtualearth.net/REST/v1/data/

Toospecify 해야 작동 매개 변수 tooget 다음 hello:

* **데이터 원본 ID** 및 **데이터 원본 이름** – Bing 맵 API에서 데이터 원본은 작업하는 위치 및 업무 시간 등 다양하게 버킷 구성된 메타데이터를 포함합니다. 이에 대한 자세한 내용은 여기에서 확인할 수 있습니다. 
* **엔터티 이름** – hello 알림에 대 한 참조 지점으로 toouse을 만들려는 엔터티 hello 합니다. 
* **Bing Maps API 키** – hello Bing Dev Center 계정을 만들 때 이전에 얻은 hello 키입니다.

위의 hello 요소 각각에 대 한 hello 설정 심층적 보겠습니다.

## <a name="setting-up-hello-data-source"></a>Hello 데이터 소스를 설정합니다.
Hello Bing Maps 개발자 센터에서에서 작업할 수 있습니다. 클릭 하세요 **데이터 원본** hello 위쪽 탐색 모음 및 선택에서 **데이터 원본 관리**합니다.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Bing Maps API 하기 전에 작업 하지 않았던 가능성이 있습니다 수 없습니다, 모든 데이터 원본 업로드 데이터 tooa 데이터 원본을 클릭 하 여 한 새만 만들 수 있습니다. 모든 필수 hello 필드를 입력 해야 합니다.

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

궁금할 것 – hello 데이터 파일을 란 무엇이 고 어떻게 해야 있습니다 수 업로드? Hello이이 테스트를 위해 hello 샌프란시스코 waterfront 부문의 프레임 파이프 기반 hello 샘플 수만 사용 합니다.

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

위의 hello이이 엔터티를 나타냅니다.

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

단순히 복사 위 hello 문자열 새 파일에 붙여 넣고로 저장 **NotificationHubsGeofence.pipe**, hello Bing 개발자 센터에에서 업로드 합니다.

> [!NOTE]
> Hello에 대 한 새 키 증명된 toospecify 수도 **마스터 키** hello와에서 다른 **쿼리 키**합니다. Hello 대시보드 및 새로 고침 hello 데이터 원본 업로드 페이지를 통해 새 키를 만들면 됩니다.
> 
> 

Hello 데이터 파일을 업로드 되 면 toomake hello 데이터 원본을 게시 해야 합니다. 

너무 이동**데이터 원본 관리**위에 했던 것과 마찬가지로, hello 목록에서 데이터 원본의 찾을 클릭할 **게시** hello에 **동작** 열입니다. 에 약간 표시 되어야 hello에 데이터 원본 **게시 된 데이터 원본** 탭:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

클릭 하면 **편집**, 있습니다에 도입 되었습니다 어떤 위치를 한 눈에 수 toosee 됩니다.

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

이 시점에서 hello 포털 경계를 만든 hello geofence hello – 필요한 것은 지정 된 hello 위치 hello 오른쪽 주변에 있는 확인 표시 되지 않습니다.

이제 hello 데이터 원본에 대 한 모든 hello 요구 해야 합니다. hello Bing Maps 개발자 센터에서에서 hello API 호출에 대 한 hello 요청 URL에 tooget hello 세부 정보 클릭 **데이터 원본** 선택 **데이터 원본 정보**합니다.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

hello **쿼리 URL** 여기 뒤 우리가 됩니다. 기준이 실행 수 인지 hello 장치 현재 위치의 hello 경계 내에서 쿼리 toocheck hello 끝점입니다. 이 확인, 추가 매개 변수 뒤 hello로 hello 쿼리 URL에 대해 GET 호출 tooexecute 필요 tooperform:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

이런 방식으로 hello 장치에서 구한 및 hello geofence 내 인지 Bing Maps hello 계산 toosee를 자동으로 수행 됩니다 있는 대상 지점 지정 하는 합니다. 브라우저 (또는 cURL)를 통해 hello 요청을 실행 하면 일단 받아볼 수 표준 JSON 응답:

![](./media/notification-hubs-geofence/bing-maps-json.png)

이 응답 hello 실제로 안에 점이 hello 경계를 지정 하는 경우에 발생 합니다. 그렇지 않은 경우 빈 **결과** 버킷을 받습니다.

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Hello UWP 응용 프로그램 설정
이제 hello 데이터 소스를 준비 했으므로 hello UWP 응용 프로그램에서는 이전 부트스트랩 하는 작업을 시작할 수 있습니다.

무엇보다도, 응용 프로그램에 위치 서비스를 사용하도록 설정해야 합니다. toodo이, 두 번이 클릭 `Package.appxmanifest` 파일 **솔루션 탐색기**합니다.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

방금 연 hello 패키지 속성 탭에서 클릭 **기능** 선택 했는지 확인 하 고 **위치**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Hello 위치 기능이 선언 되는 대로 라는 솔루션에 새 폴더를 만들고 `Core`, 라는 내에서 새 파일을 추가 하 고 `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

hello `LocationHelper` 클래스 자체는 시점에서 매우 기본적인 – hello 시스템 API 통해 tooobtain hello 사용자 위치 수는 것이 전부:

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

Hello 공식의 UWP 앱에서 사용자의 위치를 hello 가져오는 방법에 대해 자세히 알아볼 수 있습니다 [MSDN 문서](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)합니다.

toocheck 실제로 hello 위치 취득이 작동 하는 기본 페이지의 hello 코드 쪽 엽니다 (`MainPage.xaml.cs`). Hello에 대 한 새 이벤트 처리기를 만들고 `Loaded` hello에 대 한 이벤트 `MainPage` 생성자:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

hello 구현의 hello 이벤트 처리기는 다음과 같습니다.

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

म hello 처리기도 선언할 비동기 때문에 `GetCurrentLocation` awaitable, 이며 따라서 toobe 비동기 컨텍스트에서 실행이 필요 합니다. 또한 특정 상황에서는 생길 수 null 위치 때문에 (예: hello 위치 서비스를 해제 또는 hello 응용 프로그램 사용 권한 tooaccess 위치 거부 되었습니다) toomake null 확인을 통해 제대로 처리는 필요 합니다.

Hello 응용 프로그램을 실행 합니다. 위치 액세스를 허용하도록 합니다.

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

한 번 실행 하는 경우 응용 프로그램을 hello, hello hello 좌표 수 toosee 있어야 **출력** 창:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

이제 우리 않습니다에서 사용 중 이므로 더 이상 위치 취득 works –의 로드에 대 한 무료 tooremove hello 테스트 이벤트 처리기 느껴집니다 있는지 알고 있습니다.

hello 다음 단계는 toocapture 위치를 변경 합니다. 이 위해 뒤로 toohello 돌아가겠습니다 `LocationHelper` 클래스에 대 한 hello 이벤트 처리기를 추가 및 `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

hello 구현은 hello에 hello 위치 좌표를 표시 하는 **출력** 창:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Hello 백 엔드 설정
Hello 다운로드 [GitHub에서.NET 백 엔드 샘플](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)합니다. Hello 다운로드가 완료 되 면 hello 열어 `NotifyUsers` 폴더를 연 이후에 – hello `NotifyUsers.sln` 파일입니다.

집합 hello `AppBackend` hello로 프로젝트 **시작 프로젝트** 시작 하십시오.

![](./media/notification-hubs-geofence/vs-startup-project.png)

hello 프로젝트는 이미 구성 된 toosend 푸시 알림을 tootarget 장치, toodo만 다음 두 가지 – 되므로 hello 알림 허브에 대 한 올바른 연결 문자열 hello 교체 하 고 경우에 hello 경계 식별 toosend hello 알림 추가 사용자는 hello geofence 이내입니다.

tooconfigure hello 연결 문자열 hello `Models` 폴더 열림 `Notifications.cs`합니다. hello `NotificationHubClient.CreateClientFromConnectionString` 함수 hello에서 얻을 수 있는 알림 허브에 대 한 hello 정보를 포함 해야 [Azure 포털](https://portal.azure.com) (hello를 자세히 살펴보고 **액세스 정책을** 블레이드  **설정**). Hello 업데이트 된 구성 파일을 저장 합니다.

이제 모델 toocreate hello Bing Maps API 결과 대 한 필요합니다. hello 마우스 오른쪽 단추로 클릭 하는 가장 쉬운 방법은 toodo hello `Models` 폴더 **추가** > **클래스**합니다. 이름을 `GeofenceBoundary.cs`로 지정합니다. Visual Studio 사용 및 hello 첫 번째 섹션에서 설명한 hello API 응답에서 완료 되 면 복사 hello JSON **편집** > **붙여넣기** > **붙여넣기 JSON 클래스로**합니다. 

해당 hello 개체 인지를 확인 하는 이런 방식으로 deserialize 되는 원래 대로 정확 하 게 합니다. 결과 클래스 집합은 다음과 같습니다.

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

다음으로 `Controllers` > `NotificationsController.cs`를 엽니다. Hello 대상 경도 및 위도 tootweak hello Post 호출 tooaccount이 필요합니다. 이 위해 두 개의 문자열 toohello 함수 시그니처 –를 추가 하면 `latitude` 및 `longitude`합니다.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

라는 hello 프로젝트 내에서 새 클래스 만들기 `ApiHelper.cs` – 때 tooconnect tooBing toocheck 지점 경계 교차점 사용 해야 합니다. 다음과 같이 `IsPointWithinBounds` 함수를 구현합니다.

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
> 이전 hello Bing 개발자 센터 (마찬가지 toohello API 키)에서 가져온 hello 쿼리 URL 있는 있는지 toosubstitute hello API 끝점을 확인 합니다. 
> 
> 

결과 toohello 쿼리가 있는 경우 지정 된 지점 hello 즉 이므로 hello geofence의 hello 경계 내에서 반환 `true`합니다. 결과가 없습니다 Bing 알려줍니다 hello 포인트는 외부 hello 조회 프레임을 반환 하므로 `false`합니다.

다시 `NotificationsController.cs`, hello switch 문의 하기 바로 전에 검사를 만듭니다.

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

이런 방식으로 hello 지점 hello 경계 내에 있을 때 hello 알림이 전송만 됩니다.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Hello UWP 앱에 푸시 알림을 테스트
UWP 앱 toohello를 다시 살펴보자면, 우리 있어야 수 tootest 알림. Hello 내 `LocationHelper` 클래스, – 새 함수를 만들고 `SendLocationToBackend`:

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
> Hello 교체 `POST_URL` hello 이전 섹션에서 만든 배포 된 웹 응용 프로그램의 toohello 위치입니다. 일단, 확인 toorun은 로컬로 하지만 toohost 해야는 공용 버전 배포를 사용할 때는 외부 공급자와 합니다.
> 
> 

이제 되어 있는지 확인 푸시 알림에 대 한 hello UWP 앱을 등록 했습니다. Visual Studio에서 클릭 **프로젝트** > **저장** > **hello 스토어와 앱 연결**합니다.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Tooyour 개발자 계정에 로그인 한 후에 기존 앱을 선택 하거나 새로 만들 및 hello 패키지 연관 있는지 확인 합니다. 

Toohello 개발자 센터와 방금 만든 열기 hello 앱 이동 합니다. **서비스** > **푸시 알림** > **라이브 서비스 사이트**를 클릭합니다.

![](./media/notification-hubs-geofence/ms-live-services.png)

Hello 사이트에서 기록해 hello **응용 프로그램 암호** 및 hello **패키지 SID**합니다. 모두 Azure 포털 – hello에서 알림 허브를 열고에서 클릭 해야 **설정** > **Notification Services** > **WNS (Windows)**hello 필수 필드에 hello 정보를 입력 합니다.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

**Save**를 클릭합니다.

**솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. Tooadd 참조 toohello 필요한 **Microsoft Azure 서비스 버스 관리 되는 라이브러리** – 검색할 `WindowsAzure.Messaging.Managed` tooyour 프로젝트에 추가 합니다.

![](./media/notification-hubs-geofence/vs-nuget.png)

테스트를 위해 hello 만들면 `MainPage_Loaded` 이벤트 처리기를 다시 한 번이 코드 조각 tooit 추가:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

위의 hello hello 앱 hello 알림 허브에 등록합니다. 준비 toogo는! 

`LocationHelper`, hello 내 `Geolocator_PositionChanged` 처리기를 강제로 hello geofence 안의 hello 위치 시킨 테스트 코드 부분을 추가할 수 있습니다.

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Hello 실제 좌표 (않을 수도 있는 hello 경계 내 hello 순간)에 전달 하는 하 고 미리 정의 된 테스트 값을 사용 하는,에서는 업데이트에 표시 되는 알림을 나타납니다.

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>다음 단계
Toofollow hello 솔루션이 프로덕션에 사용 가능한 인지 toomake 위에 추가 toohello에서 할 수 있는 단계는 두 가지가 있습니다.

무엇 보다도, geofences는 동적 tooensure를 할 수 있습니다. 여기에 주문 toobe 수 tooupload hello 기존 데이터 원본 내에서 새 경계에 hello Bing API가 있는 몇 가지 추가 작업이 필요 합니다. Hello 참조 [Bing 공간 데이터 서비스 API 설명서](https://msdn.microsoft.com/library/ff701734.aspx) hello 주제에 대 한 자세한 내용은 합니다.

둘째, 작업 tooensure hello 배달 toohello 오른쪽 참가자 했는지 인 경우 tootarget 필요할 수 있습니다를 통해 이러한 [태그 지정](notification-hubs-tags-segment-push-message.md)합니다.

위에 표시 된 hello 솔루션은 있을 수도 있으므로 hello 지 오 펜싱 toosystem 관련 기능을 제한 하지 않은 다양 한 플랫폼을 대상으로 하는 시나리오를 설명 합니다. 즉, 유니버설 Windows 플랫폼 hello 너무 기능을 제공[geofences 오른쪽-의-즉시 검색](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence)합니다.

알림 허브 기능에 대한 자세한 내용은 [설명서 포털](https://azure.microsoft.com/documentation/services/notification-hubs/)을 확인합니다.

