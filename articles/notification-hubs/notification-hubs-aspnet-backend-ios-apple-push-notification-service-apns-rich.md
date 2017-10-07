---
title: "알림 허브 풍부한 푸시 aaaAzure"
description: "Toosend 서식 있는 Azure에서 알림을 tooan iOS 앱을 강제 하는 방법에 대해 알아봅니다. 코드 샘플은 Objective-C 및 C#으로 작성되었습니다."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="73813-104">Azure 알림 허브 다양한 푸시</span><span class="sxs-lookup"><span data-stu-id="73813-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="73813-105">개요</span><span class="sxs-lookup"><span data-stu-id="73813-105">Overview</span></span>
<span data-ttu-id="73813-106">순서 tooengage 풍부한 인스턴트 내용이 포함 된 사용자가 응용 프로그램을 일반 텍스트로 초과 toopush를 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="73813-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="73813-107">이러한 알림은 사용자 조작을 촉진하고 URL, 소리, 이미지/쿠폰 등의 콘텐츠를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="73813-108">Hello를 기반으로 한이 자습서 [사용자에 게 알림](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 항목 toosend 푸시 페이로드 (예: 이미지)를 통합 하는 알림 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73813-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="73813-109">이 자습서는 iOS 7 및 8과 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="73813-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="73813-110">개요:</span><span class="sxs-lookup"><span data-stu-id="73813-110">At a high level:</span></span>

1. <span data-ttu-id="73813-111">앱 백 엔드에서 hello:</span><span class="sxs-lookup"><span data-stu-id="73813-111">hello app backend:</span></span>
   * <span data-ttu-id="73813-112">저장소 hello 풍부한 페이로드 (이 경우 이미지) hello 백 엔드 데이터베이스/로컬 저장소</span><span class="sxs-lookup"><span data-stu-id="73813-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="73813-113">이 풍부한 알림 toohello 장치의 ID를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="73813-114">Hello 장치에서 앱:</span><span class="sxs-lookup"><span data-stu-id="73813-114">App on hello device:</span></span>
   * <span data-ttu-id="73813-115">연락처 hello hello 풍부한 페이로드를 받을 hello ID 요청 하는 백 엔드</span><span class="sxs-lookup"><span data-stu-id="73813-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="73813-116">데이터 검색 완료 되 면 사용자 들은 toolearn 더 많은 하면 즉시 hello 페이로드를 표시 하는 경우 hello 장치에 사용자 알림을 보낸다합니다</span><span class="sxs-lookup"><span data-stu-id="73813-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="73813-117">WebAPI 프로젝트</span><span class="sxs-lookup"><span data-stu-id="73813-117">WebAPI Project</span></span>
1. <span data-ttu-id="73813-118">Visual Studio에서 열고 hello **AppBackend** hello에서 만든 프로젝트 [사용자에 게 알림](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="73813-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="73813-119">이미지, toonotify 사용자 및 파일에 저장 하는 **img** 프로젝트 디렉터리의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="73813-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="73813-120">클릭 **모든 파일 표시** hello 솔루션 탐색기에서 및 너무 hello 폴더를 마우스 오른쪽 단추로**프로젝트에 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="73813-121">선택한 hello 이미지 사용 하 여 속성 창에서 해당 빌드 동작을 너무 변경**포함 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="73813-122">**Notifications.cs**, hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="73813-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="73813-123">전체 업데이트 hello **알림** 코드 다음 hello 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="73813-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="73813-124">있는지 tooreplace 알림 허브 자격 증명 및 이미지 파일 이름을 사용 하 여 hello 자리 표시자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="73813-125">(선택 사항) 너무 참조[어떻게 tooembed 리소스 액세스할 Visual C#을 사용 하 여](http://support.microsoft.com/kb/319292) 방법에 대 한 자세한 내용은 tooadd 고 프로젝트 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="73813-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="73813-126">**NotificationsController.cs**, 재정의 **NotificationsController** 조각 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="73813-127">초기 자동 풍부한 알림 id toodevice 보내고 이미지의 클라이언트 쪽 검색을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="73813-128">순서 toomake이 응용 프로그램 tooan Azure 웹 사이트를 다시 배포 됩니다에서는 이제는 모든 장치에서 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="73813-129">Hello를 마우스 오른쪽 단추로 클릭 **AppBackend** 프로젝트를 마우스 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="73813-130">Azure 웹 사이트를 게시 대상으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="73813-131">Azure 계정으로 로그인을 기존 또는 새 웹 사이트를 선택 하 고 hello 메모 **대상 URL** hello에 대 한 속성 **연결** 탭 합니다. 다음 URL로 toothis 이라고 합니다 프로그램 *백 엔드 끝점* 이 자습서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="73813-132">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="73813-133">Hello iOS 프로젝트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-133">Modify hello iOS project</span></span>
<span data-ttu-id="73813-134">앱 백 엔드 toosend 정당한 hello 수정한 했으므로 *id* 는 알림의에서는 iOS 앱 toohandle 해당 id를 변경 하 고 검색 hello 풍부한 메시지 백 엔드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="73813-135">IOS 프로젝트를 열고 이동 tooyour 기본 응용 프로그램에서 대상에에서 따라 hello 원격 알림을 사용 하도록 설정 **대상** 섹션.</span><span class="sxs-lookup"><span data-stu-id="73813-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="73813-136">클릭 **기능**, 켜기 **백그라운드 모드**, hello를 확인 하 고 **원격 알림** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="73813-137">너무 이동**Main.storyboard**에서 보기 컨트롤러 (참조 된 tooas 뷰 컨트롤러 홈이 자습서에서는)가 설치 되어 있는지 확인 하 고 [사용자에 게 알림](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="73813-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="73813-138">추가 **탐색 컨트롤러** tooyour 스토리 보드 및 컨트롤 끌기를 tooHome 뷰-컨트롤러 toomake hello 것 **보기 루트** 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="73813-139">Hello 있는지 확인 **초기 뷰 컨트롤러** 특성에서 탐색 컨트롤러 hello에 대 한 관리자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="73813-140">추가 **뷰-컨트롤러** toostoryboard 추가 **이미지 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="73813-141">이 hello 페이지 toolearn hello notifiication를 클릭 하 여 더 많은 선택 되 면 사용자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73813-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="73813-142">스토리보드는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73813-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="73813-143">Hello 클릭 **홈 뷰-컨트롤러** 있는지 확인 하 고 스토리 보드에 **homeViewController** 으로 해당 **사용자 지정 클래스** 및 **스토리 보드 ID**hello Identity 관리자에서.</span><span class="sxs-lookup"><span data-stu-id="73813-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="73813-144">로 이미지 뷰-컨트롤러에 대 한 동일 hello 마십시오 **imageViewController**합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="73813-145">그런 다음 라는 제목의 새 뷰-컨트롤러 클래스를 만듭니다 **imageViewController** toohandle hello 방금 만든 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="73813-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="73813-146">**imageViewController.h**, hello toohello 컨트롤러의 인터페이스 선언 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="73813-147">Hello 스토리 보드 이미지 보기 toothese 속성 toolink hello 두에서 toocontrol 끌어서 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="73813-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="73813-148">**imageViewController.m**, hello 끝나기 전에 hello 다음 추가 **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="73813-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="73813-149">**AppDelegate.m**, 만든 가져오기 hello 이미지 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="73813-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="73813-150">인터페이스 섹션 선언 뒤 hello로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="73813-151">**AppDelegate**에서, 반드시 사용자의 앱이 **application: didFinishLaunchingWithOptions**에 자동 알림을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. <span data-ttu-id="73813-152">Hello에 대 한 구현을 뒤에 Subsitute **응용 프로그램: didRegisterForRemoteNotificationsWithDeviceToken** 계정으로 UI가 변경 될 tootake hello 스토리 보드:</span><span class="sxs-lookup"><span data-stu-id="73813-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="73813-153">그런 다음 hello 너무 메서드를 다음을 추가**AppDelegate.m** tooretrieve 끝점에서 이미지 hello 및 검색 완료 되 면 로컬 알림을 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="73813-154">있는지 toosubstitute hello 자리 표시자 확인 `{backend endpoint}` 백 엔드 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="73813-155">Hello 이미지 뷰 컨트롤러에서를 열면 위에 hello 로컬 알림 처리 **AppDelegate.m** 메서드를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="73813-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a><span data-ttu-id="73813-156">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="73813-156">Run hello Application</span></span>
1. <span data-ttu-id="73813-157">XCode에서 실제 iOS 장치 (푸시 알림이 hello 시뮬레이터에서 작동 하지 것입니다) hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="73813-158">Hello iOS 앱 UI에에서 사용자 이름과 암호의 인증에 대 한 값 동일 하 고 클릭 하 여 hello 입력 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="73813-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="73813-159">**푸시 보내기** 를 클릭하면 앱 내 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73813-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="73813-160">클릭 하면 **자세한**, 앱 백엔드에 tooinclude를 선택한 상태로 toohello 이미지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73813-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="73813-161">클릭할 수도 있습니다 **푸시 보내기** 즉시 장치의 hello 홈 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73813-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="73813-162">곧 푸시 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73813-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="73813-163">탭에 자세히를 클릭 하거나, 앱 및 hello 다양 한 이미지 콘텐츠 tooyour 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73813-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
