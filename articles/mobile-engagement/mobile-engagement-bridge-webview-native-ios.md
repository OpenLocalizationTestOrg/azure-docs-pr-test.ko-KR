---
title: "네이티브 Mobile Engagement ios SDK aaaBridge iOS 웹 보기"
description: "설명 방법을 toocreate Javascript 및 hello 네이티브 Mobile Engagement iOS SDK를 실행 하는 웹 보기 간의 브리지"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="64285-103">iOS WebView와 네이티브 Mobile Engagement iOS SDK 브리지</span><span class="sxs-lookup"><span data-stu-id="64285-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64285-104">Android 브리지</span><span class="sxs-lookup"><span data-stu-id="64285-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="64285-105">iOS 브리지</span><span class="sxs-lookup"><span data-stu-id="64285-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="64285-106">일부 모바일 응용 프로그램은 여기서 hello 응용 프로그램 자체가 Objective-c 네이티브 iOS 개발을 사용 하 여 개발 된 되지만 일부 또는 모든 hello 화면 웹 보기 iOS 내에서 렌더링 되는 하이브리드 응용 프로그램으로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64285-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="64285-107">이 자습서에서는 설명 하 고 이러한 응용 프로그램 내에서 Mobile Engagement iOS SDK 소비 될 수 있습니다 어떻게 toogo이 작업을 수행 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="64285-108">두 가지 접근 방식을 tooachieve이 있지만 둘 다 하지 문서화 된:</span><span class="sxs-lookup"><span data-stu-id="64285-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="64285-109">첫 번째 방식은 웹 보기에 `UIWebViewDelegate`를 등록하는 것과 관련된 이 [링크](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip)에 설명되어 있으며, Javascript에서 수행된 위치 변경을 catch하고 즉시 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="64285-110">이에 따라 하나는 두 번째 [WWDC 2013 세션](https://developer.apple.com/videos/play/wwdc2013/615), 먼저 hello 보다 깔끔한 되 고이 가이드에 대 한 따라야 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="64285-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="64285-111">이 접근 방식은 iOS7 이상에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="64285-112">Hello iOS 브리지 샘플에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="64285-113">통해 수행한 tooensure 해야 우선, 우리의 [시작 자습서](mobile-engagement-ios-get-started.md) toointegrate hello 하이브리드 앱에서 Mobile Engagement iOS SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="64285-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="64285-114">필요에 따라 테스트 hello 웹 보기에서 트리거할 것 처럼 hello SDK 메서드를 볼 수 있도록 다음과 같이 로깅을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64285-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="64285-115">이제 하이브리드 앱에 WebView가 표시된 화면이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="64285-116">Toohello를 추가할 수 있습니다 `Main.storyboard` hello 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="64285-117">이 웹 보기와 연결 하면 **ViewController** 클릭 하 고 hello webview hello 보기 컨트롤러 장면 toohello에서 끌어서 `ViewController.h` hello 바로 아래에 배치 하는 화면에서 편집 `@interface` 줄.</span><span class="sxs-lookup"><span data-stu-id="64285-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="64285-118">그러면 이름을 묻는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="64285-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="64285-119">으로 hello 이름을 지정 **webView**합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="64285-120">프로그램 `ViewController.h` 파일 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64285-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="64285-121">Hello 업데이트할 것 `ViewController.m` 나중에 파일 있지만 먼저 SDK 메서드 일부 자주 사용 되는 Mobile Engagement iOS를 통해 래퍼를 생성 하는 hello 연결 파일을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64285-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="64285-122">새 헤더 파일을 만들 **EngagementJsExports.h** hello를 사용 하 여 `JSExport` 앞에서 언급 한 hello에 설명 된 메커니즘 [세션](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello 네이티브 iOS 메서드.</span><span class="sxs-lookup"><span data-stu-id="64285-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. <span data-ttu-id="64285-123">다음 hello hello 연결 파일의 두 번째 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64285-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="64285-124">파일을 만들 **EngagementJsExports.m** 있는 hello 구현 hello Mobile Engagement iOS SDK 메서드를 호출 하 여 hello 실제 래퍼를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="64285-125">Hello 구문 분석은 म 참고 또한 `extras` hello webview javascript에서 전달 되 고 해당 넣는 `NSMutableDictionary` 개체 toobe 호출 Engagement SDK 메서드 hello로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. <span data-ttu-id="64285-126">이제 우리 toohello 돌아와서 **ViewController.m** 코드 다음 hello로 업데이트:</span><span class="sxs-lookup"><span data-stu-id="64285-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. <span data-ttu-id="64285-127">Hello에 대 한 참고 hello 다음 가리키는 **ViewController.m** 파일:</span><span class="sxs-lookup"><span data-stu-id="64285-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="64285-128">Hello에 `loadWebView` 메서드, 우리를 로드 하는 이라는 로컬 HTML 파일 **LocalPage.html** 다음 검토할 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="64285-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="64285-129">Hello에 `webViewDidFinishLoad` 메서드를 hello를 끄는 것 `JsContext` 와 연관 래퍼 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="64285-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="64285-130">이렇게 우리의 래퍼의 hello 핸들을 사용 하는 SDK 메서드를 호출 하면 **EngagementJs** hello 웹 보기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="64285-131">파일을 만들 **LocalPage.html** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="64285-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. <span data-ttu-id="64285-132">위의 hello HTML 파일에 대 한 참고 hello 다음 지점:</span><span class="sxs-lookup"><span data-stu-id="64285-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="64285-133">이벤트, 작업, 오류, AppInfo의 이름으로 사용 되는 데이터 toobe을 제공할 수 있는 입력란의 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="64285-134">Hello 단추 다음 tooit 클릭할 때 toohello 결국 hello 브리지 파일 toopass에서 hello 메서드를 호출 toohello Mobile Engagement iOS SDK이 호출 하는 Javascript 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="64285-135">우리는 태그 지정에 몇 가지 추가 정보를 정적 toohello 이벤트, 작업 및 오류 toodemonstrate도 방법을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64285-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="64285-136">이 추가 정보 보내집니다는 JSON 문자열 hello를 보면 `EngagementJsExports.m` 파일, 구문 분석 되 고 보내는 이벤트, 작업, 및 오류와 함께 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="64285-137">Mobile Engagement 작업이 10 초 동안 실행 하 고 종료 hello 입력된 상자에 지정한 hello 이름으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="64285-138">Mobile Engagement appinfo 또는 태그와 'customer_name' hello 정적 키와 입력 한 hello 입력에 hello 값으로 hello 태그에 대 한 hello 값 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64285-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="64285-139">실행된 hello 앱 hello 다음에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64285-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="64285-140">이제 다음 hello와 같은 테스트 이벤트에 대 한 몇 가지 이름을 제공 하 고 클릭 **보낼** 다음 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="64285-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="64285-141">이제 toohello 이동 **모니터** 앱과 검토의 탭 **이벤트 세부 정보->**, hello 정적 응용 프로그램 정보를 전송 하는 함께 표시 하는이 이벤트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64285-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
